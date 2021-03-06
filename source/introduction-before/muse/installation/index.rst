
.. _muse-instllation:

Installation MUSE
==============

This section describes the installation procedure and the build process for
those that want to compile from the source.

Downloads Muse
-----------------------

Precompile Executables
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Compiled executeables are available for `download from github`_.


.. _download from github: https://github.com/peertracksinc/muse/releases/latest



Sources Muse
--------------------

The sources are located at `github`_ and can be downloaded
with `git`.

.. code-block:: sh

    git clone https://github.com/peertracksinc/muse

Since the repository makes use of so called *submodules* which are repositories
on their own, we need to refresh those.

.. code-block:: sh

    git submodule update --init --recursive


.. _github: http://github.com



Building from Sources
-----------------------------

Downloading the sources
^^^^^^^^^^^^^^^^^^^

The sources can be downloaded from github as described 
:doc:`here <../installation/Sources>`.

Dependencies
^^^^^^^^^^^^^^^^^^^^^

Development Toolkit
~~~~~~~~~~~~~~~~~~~~~~~~

The following dependencies were necessary for a clean install of Ubuntu 14.04
LTS:

.. code-block:: sh

    sudo apt-get install gcc-4.9 g++-4.9 cmake make \
                         libbz2-dev libdb++-dev libdb-dev \
                         libssl-dev openssl libreadline-dev \
                         autoconf libtool git

Boost 1.57
~~~~~~~~~~~~~~~

The Boost which ships with Ubuntu 15.04 is too old.  You need to download the
Boost tarball for Boost 1.57.0 (Note, 1.58.0 requires C++14 and will not build
on Ubuntu LTS; this requirement was an accident, see `this mailing list post`_).

.. code-block:: sh

    BOOST_ROOT=$HOME/opt/boost_1_57_0
    sudo apt-get update
    sudo apt-get install autotools-dev build-essential \
                         g++ libbz2-dev libicu-dev python-dev
    wget -c 'http://sourceforge.net/projects/boost/files/boost/1.57.0/boost_1_57_0.tar.bz2/download'\
         -O boost_1_57_0.tar.bz2
    sha256sum boost_1_57_0.tar.bz2
    # "910c8c022a33ccec7f088bd65d4f14b466588dda94ba2124e78b8c57db264967"
    tar xjf boost_1_57_0.tar.bz2
    cd boost_1_57_0/
    ./bootstrap.sh "--prefix=$BOOST_ROOT"
    ./b2 install

.. _this mailing list post: http://boost.2283326.n4.nabble.com/1-58-1-bugfix-release-necessary-td4674686.html

QT 5.5
^^^^^^^^^^^

Qt 5.5 is a dependency if you wish to build `light_client`.  Building it from
source requires the following dependencies on Ubuntu LTS:

.. code-block:: sh

    sudo apt-get install libxcb1 libxcb1-dev libx11-xcb1 libx11-xcb-dev \
                         libxcb-keysyms1 libxcb-keysyms1-dev libxcb-image0 libxcb-image0-dev \
                         libxcb-shm0 libxcb-shm0-dev libxcb-icccm4 libxcb-icccm4-dev libxcb-sync1 \
                         libxcb-sync-dev

Qt 5.5 can be built as follows:

.. code-block:: sh

    QT_ROOT=$HOME/opt/qt5.5.0

    wget http://download.qt.io/official_releases/qt/5.5/5.5.0/single/qt-everywhere-opensource-src-5.5.0.tar.gz
    sha256sum qt-everywhere-opensource-src-5.5.0.tar.gz
    # "bf3cfc54696fe7d77f2cf33ade46c2cc28841389e22a72f77bae606622998e82"
    tar xzf qt-everywhere-opensource-src-5.5.0.tar.gz
    cd qt-everywhere-opensource-src-5.5.0
    ./configure -prefix "$QT_ROOT" -opensource -nomake tests
    make # -j4
    make install

Next we need to tell `cmake` where to find them.  If you have ever run CMake in
this tree before, we must first delete some leftovers:

.. code-block:: sh

    make clean
    rm -f CMakeCache.txt
    find . -name CMakeFiles | xargs rm -Rf

To actually run `cmake` we now need the following parameters:

.. code-block:: sh

    cmake -DCMAKE_PREFIX_PATH="$QT_ROOT" \
          -DCMAKE_MODULE_PATH="$QT_ROOT/lib/cmake/Qt5Core" \
          -DQT_QMAKE_EXECUTABLE="$QT_ROOT/bin/qmake" -DBUILD_QT_GUI=TRUE \
           -DGRAPHENE_EGENESIS_JSON="$GENESIS_JSON" \
           -DBOOST_ROOT="$BOOST_ROOT" -DCMAKE_BUILD_TYPE=Debug   .
    cd ..

	
Building MUSE
^^^^^^^^^^^^^^^^^^^^^^^

After downloading the muse sources according to :doc:`the download
page <./Sources>`, we can run ``cmake`` for configuration and compile with
``make``:

.. code-block:: sh

    cmake -DBOOST_ROOT="$BOOST_ROOT" -DCMAKE_BUILD_TYPE=Release .
    make 

Note that the environmental variable ``$BOOST_ROOT`` should point to your
install directory of boost if you have installed it manually.

Distribution Specific Settings
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Ubuntu 14.04
~~~~~~~~~~~~~~~~~

As ``g++-4.9`` isn't available in 14.04 LTS, you need to do this first:

.. code-block:: sh

    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update

If you get build failures due to abi incompatibilities, just use gcc 4.9

.. code-block:: sh

    CC=gcc-4.9 CXX=g++-4.9 cmake .


Ubuntu 15.04
^^^^^^^^^^^^^^

Ubuntu 15.04 uses gcc 5, which has the c++11 ABI as default, but the boost
libraries were compiled with the cxx11 ABI (this is an issue in many distros).
If you get build failures due to abi incompatibilities, just use gcc 4.9:

.. code-block:: sh

    CC=gcc-4.9 CXX=g++-4.9 cmake .


Upgrading
----------------------------

Recompiling from Sources
^^^^^^^^^^^^^^^^^^^^

For upgrading from source you only need to execute:

.. code-block:: sh

    git fetch
    git checkout <version>
    git submodule update --init --recursive
    cmake .
    make
	
	
	
