## Building on Ubuntu

### Available Versions
- Ubuntu 16.04 LTS
- Ubuntu 16.04 LTS
- Boost: between 1.57 and 1.65
- OpenSSL: 1.0.x range

## Ubuntu 14.04 LTS

### 1.Install Dependencies
This is necessary for clean installation.

    sudo apt-get update
    sudo apt-get install cmake make libbz2-dev libdb++-dev libdb-dev libssl-dev openssl libreadline-dev autoconf libtool git ntp libcurl4-openssl-dev g++ libcurl4-openssl-dev

### 2.Build Boost 1.57.0

Download the Boost tarball for Boost 1.57.0. (*Ubuntu 14.04 ships old version of Boost.) 

**Note:** 1.58.0 requires C++14 and will not build on Ubuntu 14.04 LTS; this requirement was an accident, see this mailing list post.

    BOOST_ROOT=$HOME/opt/boost_1_57_0
    sudo apt-get update
    sudo apt-get install autotools-dev build-essential libbz2-dev libicu-dev python-dev
    wget -c 'http://sourceforge.net/projects/boost/files/boost/1.57.0/boost_1_57_0.tar.bz2/download' -O boost_1_57_0.tar.bz2
    [ $( sha256sum boost_1_57_0.tar.bz2 | cut -d ' ' -f 1 ) == "910c8c022a33ccec7f088bd65d4f14b466588dda94ba2124e78b8c57db264967" ] || ( echo 'Corrupt download' ; exit 1 )
    tar xjf boost_1_57_0.tar.bz2
    cd boost_1_57_0/
    ./bootstrap.sh "--prefix=$BOOST_ROOT"
    ./b2 install

### 3.Build BitShares Core

    cd ..
    git clone https://github.com/bitshares/bitshares-core.git
    cd bitshares-core
    git submodule update --init --recursive
    cmake -DBOOST_ROOT="$BOOST_ROOT" -DCMAKE_BUILD_TYPE=Release .
    make 

***

## Ubuntu 16.04 LTS

### 1.Install Dependencies
Ubuntu 16.04 LTS ships with Boost 1.58 libraries, so no need to build from source.

    sudo apt-get install libboost-all-dev


### 2.Build BitShares Core
(*These are the same steps.) 

    cd ..
    git clone https://github.com/bitshares/bitshares-core.git
    cd bitshares-core
    git submodule update --init --recursive
    cmake -DBOOST_ROOT="$BOOST_ROOT" -DCMAKE_BUILD_TYPE=Release .
    make 


## Error 

### Error `{"message":"Timer Expired"}` in Ubuntu 16.04 LTS

If error `{"message":"Timer Expired"}` dropped then it could be issue with websocketpp in linux kernel > 4.4.

Details [here](https://github.com/DECENTfoundation/DECENT-Network/issues/194).

Steps to fix:

    cd ~/bitshares-core/libraries/fc/vendor/websocketpp
    git remote set-url origin https://github.com/DECENTfoundation/websocketpp.git
    git fetch
    git checkout 

And then build BitShares Core.


***




