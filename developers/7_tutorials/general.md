
## General

##  Address structure, Format, block, time, and other

**What is the standard Bitshares address structure and format?**

address = ‘BTS’+base58(ripemd(sha512(compressed_pub))) (checksum obviated) But addresses are not used directly, instead you have an account (that can be controlled by one or more address, pubkey or another account). https://bitshares.org/technology/dynamic-account-permissions/


**What is the format of the block header?**

    struct block_header
       {
          digest_type                   digest()const;
          block_id_type                 previous;
          uint32_t                      block_num()const { return num_from_id(previous) + 1; }
          fc::time_point_sec            timestamp;
          witness_id_type               witness;
          checksum_type                 transaction_merkle_root;
          extensions_type               extensions;

          static uint32_t num_from_id(const block_id_type& id);
       };

**What is the maximum bitshares block size?**

Configurable by chain parameters.

    struct chain_parameters
    {
       /** using a smart ref breaks the circular dependency created between operations and the fee schedule */
       smart_ref<fee_schedule> current_fees;                       ///< current schedule of fees
       uint8_t                 block_interval                      = GRAPHENE_DEFAULT_BLOCK_INTERVAL; ///< interval in seconds between blocks
       uint32_t                maintenance_interval                = GRAPHENE_DEFAULT_MAINTENANCE_INTERVAL; ///< interval in sections between blockchain maintenance events
       uint8_t                 maintenance_skip_slots              = GRAPHENE_DEFAULT_MAINTENANCE_SKIP_SLOTS; ///< number of block_intervals to skip at maintenance time
       uint32_t                committee_proposal_review_period    = GRAPHENE_DEFAULT_COMMITTEE_PROPOSAL_REVIEW_PERIOD_SEC; ///< minimum time in seconds that a proposed transaction requiring committee authority may not be signed, prior to expiration
       uint32_t                maximum_transaction_size            = GRAPHENE_DEFAULT_MAX_TRANSACTION_SIZE; ///< maximum allowable size in bytes for a transaction
       uint32_t                maximum_block_size                  = GRAPHENE_DEFAULT_MAX_BLOCK_SIZE; ///< maximum allowable size in bytes for a block
       uint32_t                maximum_time_until_expiration       = GRAPHENE_DEFAULT_MAX_TIME_UNTIL_EXPIRATION; ///< maximum lifetime in seconds for transactions to be valid, before expiring
       uint32_t                maximum_proposal_lifetime           = GRAPHENE_DEFAULT_MAX_PROPOSAL_LIFETIME_SEC; ///< maximum lifetime in seconds for proposed transactions to be kept, before expiring
       uint8_t                 maximum_asset_whitelist_authorities = GRAPHENE_DEFAULT_MAX_ASSET_WHITELIST_AUTHORITIES; ///< maximum number of accounts which an asset may list as authorities for its whitelist OR blacklist
       uint8_t                 maximum_asset_feed_publishers       = GRAPHENE_DEFAULT_MAX_ASSET_FEED_PUBLISHERS; ///< the maximum number of feed publishers for a given asset
       uint16_t                maximum_witness_count               = GRAPHENE_DEFAULT_MAX_WITNESSES; ///< maximum number of active witnesses
       uint16_t                maximum_committee_count             = GRAPHENE_DEFAULT_MAX_COMMITTEE; ///< maximum number of active committee_members
       uint16_t                maximum_authority_membership        = GRAPHENE_DEFAULT_MAX_AUTHORITY_MEMBERSHIP; ///< largest number of keys/accounts an authority can have
       uint16_t                reserve_percent_of_fee              = GRAPHENE_DEFAULT_BURN_PERCENT_OF_FEE; ///< the percentage of the network's allocation of a fee that is taken out of circulation
       uint16_t                network_percent_of_fee              = GRAPHENE_DEFAULT_NETWORK_PERCENT_OF_FEE; ///< percent of transaction fees paid to network
       uint16_t                lifetime_referrer_percent_of_fee    = GRAPHENE_DEFAULT_LIFETIME_REFERRER_PERCENT_OF_FEE; ///< percent of transaction fees paid to network
       uint32_t                cashback_vesting_period_seconds     = GRAPHENE_DEFAULT_CASHBACK_VESTING_PERIOD_SEC; ///< time after cashback rewards are accrued before they become liquid
       share_type              cashback_vesting_threshold          = GRAPHENE_DEFAULT_CASHBACK_VESTING_THRESHOLD; ///< the maximum cashback that can be received without vesting
       bool                    count_non_member_votes              = true; ///< set to false to restrict voting privlegages to member accounts
       bool                    allow_non_member_whitelists         = false; ///< true if non-member accounts may set whitelists and blacklists; false otherwise
       share_type              witness_pay_per_block               = GRAPHENE_DEFAULT_WITNESS_PAY_PER_BLOCK; ///< CORE to be allocated to witnesses (per block)
       uint32_t                witness_pay_vesting_seconds         = GRAPHENE_DEFAULT_WITNESS_PAY_VESTING_SECONDS; ///< vesting_seconds parameter for witness VBO's
       share_type              worker_budget_per_day               = GRAPHENE_DEFAULT_WORKER_BUDGET_PER_DAY; ///< CORE to be allocated to workers (per day)
       uint16_t                max_predicate_opcode                = GRAPHENE_DEFAULT_MAX_ASSERT_OPCODE; ///< predicate_opcode must be less than this number
       share_type              fee_liquidation_threshold           = GRAPHENE_DEFAULT_FEE_LIQUIDATION_THRESHOLD; ///< value in CORE at which accumulated fees in blockchain-issued market assets should be liquidated
       uint16_t                accounts_per_fee_scale              = GRAPHENE_DEFAULT_ACCOUNTS_PER_FEE_SCALE; ///< number of accounts between fee scalings
       uint8_t                 account_fee_scale_bitshifts         = GRAPHENE_DEFAULT_ACCOUNT_FEE_SCALE_BITSHIFTS; ///< number of times to left bitshift account registration fee at each scaling
       uint8_t                 max_authority_depth                 = GRAPHENE_MAX_SIG_CHECK_DEPTH;
       extensions_type         extensions;
    
       /** defined in fee_schedule.cpp */
       void validate()const;
    };


**Are there any sharding mechanics currently deployed?**

No

**How are SPV clients handled?**

No SPV clients at the moment, each full node can expose a public websocket/http api.

**How is time addressed in the blockchain? Is NTP used or some other protocol?**

NTP

**How do new clients bootstrap into the network?**

Trusted seed nodes. Knowledge of initial witness keys.

**What is the average block time?**

Current 3 seconds, configurable by chain parameters.

**How is accounting addressed in Bitshares? Is it a Nxt style accounting model or like Bitcoin’s UTXO**

Each account has a finite set of balances, one for each asset type.

## Protocol

**Are there any special affordances made for privacy?**

…such as using CoinJoin or a ZK-SNARK based privacy scheme like Zerocash? If mixing is integrated at the protocl level are you using the standards set forth by the BNMCKF Mixcoin proposal

Confidential values (same as blockstream elements using the same secp256k1-zkp lib) + stealth addresses. https://github.com/Ele

**Does the protocol provide mechanisms for overlay protocols to interact such as OR_RETURN?**

Yes, using a custom_operation.

    struct custom_operation : public base_operation
       {
          struct fee_parameters_type {
             uint64_t fee = GRAPHENE_BLOCKCHAIN_PRECISION;
             uint32_t price_per_kbyte = 10;
          };

          asset                     fee;
          account_id_type           payer;
          flat_set<account_id_type> required_auths;
          uint16_t                  id = 0;
          vector<char>              data;

          account_id_type   fee_payer()const { return payer; }
          void              validate()const;
          share_type        calculate_fee(const fee_parameters_type& k)const;
       };

**Is this done via a gossip protocol or through a federate relay?**

Each node immediately broadcast the data it receives to its peers after validating it https://github.com/cryptonomex/graphene/blob/master/libraries/p2p/design.md


## Data Structures

**What data structures are used in the blockchain?**

::
    Blocks => transactions => operations => objects.

The blockchain state is contained in an object database that is affected by the operations. Example objects::

    account_object
    asset_object
    account_balance_object
    ...


    class account_balance_object : public abstract_object<account_balance_object>
       {
          public:
             static const uint8_t space_id = implementation_ids;
             static const uint8_t type_id  = impl_account_balance_object_type;

             account_id_type   owner;
             asset_id_type     asset_type;
             share_type        balance;

             asset get_balance()const { return asset(balance, asset_type); }
             void  adjust_balance(const asset& delta);
       };


## Public key system

**What public key system is used? If elliptic curve, then what is the curve?**

Same as Bitcoin, secp256k1.

## Scripting Language ?
**Is there a specification for Bitshares scripting language? (assuming there is one)**

No scripting

**Is the scripting language turing complete?**

No scripting

# BitShares Decentralised Exchange (DEX)


## Distributed Access to the BitShares Decentralised Exchange (DEX)

I hope to encourage and promote more access points and backup WebSocket (wss) gateways for BitShares. This is the logical progression from Run your own decentralised exchange post. BitShares ###Distributed Access to the BitShares Network

## BitShares node setup

Run your own decentralised exchange

Once you have a full node setup, you can allow BitShares shareholders secure access to your server to trade and check their accounts by following these steps. >A DNS Alias (CNAME) is required to point to your server ip address. >See dyn.com for DNS Alias setup. >You may have to wait a few days for the DNS to work through the internet. >Please change altcap.io to your DNS alias in the examples below.

## Create a New User

I recommend creating a new user on your server to run the Bitshares gui and give the user sudo access. >You can use any name - I have used bitshares in this example

    sudo adduser bitshares
    sudo gpasswd -a bitshares sudo
    sudo gpasswd -a bitshares users

## Install Nginx

Install Nginx web server

    # ssh into your new user bitshares
    ssh bitshares@altcap.io
    sudo apt-get install nginx
    # check version
    nginx -v
    # add user to web server group
    sudo gpasswd -a bitshares www-data
    # start nginx
    sudo service nginx start

This will start Nginx default web server. Check it by typing the ip address of your server in a web browser or your alias altcap.io

### Configure Nginx

To configure the web server, edit the default site and save as new DNS alias name using http port 80 only until you setup letsencrypt.org SSL Certificate.

### Create your web folder

    sudo mkdir -p /var/www/altcap.io/public_html
    sudo chown -R bitshares:bitshares var/www/altcap.io/public_html
    sudo chmod 755 /var/www


### Configure Nginx

    # edit default setup and save as altcap.io
    sudo nano /etc/nginx/sites-available/default

Point to your new virtual host

    ###### altcap.io ######
    server {
        listen 80;
        server_name altcap.io;
        #rewrite ^ https://$server_name$request_uri? permanent;
        #rewrite ^ https://altcap.io$uri permanent;
        #
        root /var/www/altcap.io/public_html;
        # Add index.php to the list if you are using PHP
        index index.html index.htm;
        #
        location / {
            # First attempt to serve request as file, then
            # as directory, then fall back to displaying a 404.
            try_files $uri $uri/ =404;
        }
    }

    CTRL+O to save as altcap.io (^O Write Out)

### Update Virtual Host File

    sudo cp altcap.io /etc/nginx/sites-available/altcap.io

### Activate sim link and disable default web server

    sudo ln -s /etc/nginx/sites-available/altcap.io /etc/nginx/sites-enabled/altcap.io
    sudo rm /etc/nginx/sites-enabled/default

### Link local folder to www root and add a simple index.html

    ln -s /var/www/altcap.io/public_html ~/public_html
    nano ~/public_html/index.html

Add some text to index.html

    <html>
        <head>
        <title>altcap.io</title>
      </head>
      <body>
        <h1>altcap.io - Virtual Host</h1>
      </body>
    </html>

    CTRL+X to save as index.html (^X Exit) ###Restart Nginx

    sudo service nginx restart

Now you have setup a simple web server. DigitalOcean has a great article for more information on Virtual Host setup.

## Install Letsencrypt

    sudo apt-get install letsencrypt
    
**Obtain your SSL certificate**

    sudo letsencrypt certonly --webroot -w /var/www/altcap.io/public_html -d altcap.io

Follow the instructions and add an email address

**Check your certificate**

    sudo ls -l /etc/letsencrypt/live/altcap.io
    # and check it will update
    sudo letsencrypt renew --dry-run --agree-tos
    sudo letsencrypt renew

**Setup a renew cronjob for your new SSL certificate**

    sudo crontab -e

Add this line to run the job every 6 hours on the 16th minute

    16 */6 * * *  /usr/bin/letsencrypt renew >> /var/log/letsencrypt-renew.log

    CTRL+X to save (^X Exit)

    # check your crontab
    sudo crontab -l

**Generate Strong Diffie-Hellman Group cert**

    sudo openssl dhparam -out /etc/ssl/certs/dhparam.pem 2048


## Add SSL to Nginx settings

Make a copy of altcap.io just in case.

    cp altcap.io alcap.io.no.ssl

**Edit altcap.io**

    nano altcap.io

    ###### altcap.io ######
    server {
        listen 80;
        server_name altcap.io;
        #rewrite ^ https://$server_name$request_uri? permanent;
        rewrite ^ https://altcap.io$uri permanent;
        #
        root /var/www/altcap.io/public_html;
        # Add index.php to the list if you are using PHP
        index index.html index.htm;
        #
        location / {
            # First attempt to serve request as file, then
            # as directory, then fall back to displaying a 404.
            try_files $uri $uri/ =404;
        }
    }


    ###### altcap.io websockets


    upstream websockets {
        server localhost:8090;
    }


    ###### altcap.io ssl
    server {
        listen 443 ssl;
        #
        server_name altcap.io;
        #
        root /var/www/altcap.io/public_html;
        # Add index.php to the list if you are using PHP
        index index.html index.htm;
        #
        ssl_certificate /etc/letsencrypt/live/altcap.io/fullchain.pem;
        ssl_certificate_key /etc/letsencrypt/live/altcap.io/privkey.pem;
        #
        ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
        ssl_prefer_server_ciphers on;
        ssl_dhparam /etc/ssl/certs/dhparam.pem;
        ssl_ciphers 'ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:DHE-DSS-AES128-GCM-SHA256:kEDH+AESGCM:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA:ECDHE-ECDSA-AES256-SHA:DHE-RSA-AES128-SHA256:DHE-RSA-AES128-SHA:DHE-DSS-AES128-SHA256:DHE-RSA-AES256-SHA256:DHE-DSS-AES256-SHA:DHE-RSA-AES256-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128-SHA256:AES256-SHA256:AES128-SHA:AES256-SHA:AES:CAMELLIA:DES-CBC3-SHA:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!aECDH:!EDH-DSS-DES-CBC3-SHA:!EDH-RSA-DES-CBC3-SHA:!KRB5-DES-CBC3-SHA';
        ssl_session_timeout 1d;
        ssl_session_cache shared:SSL:50m;
        ssl_stapling on;
        ssl_stapling_verify on;
        add_header Strict-Transport-Security max-age=15768000;
        #
        # Note: You should disable gzip for SSL traffic.
        # See: https://bugs.debian.org/773332
        #
        # Read up on ssl_ciphers to ensure a secure configuration.
        # See: https://bugs.debian.org/765782
        #
        # Self signed certs generated by the ssl-cert package
        # Don't use them in a production server!
        #
        # include snippets/snakeoil.conf;
        #
        location / {
            # First attempt to serve request as file, then
            # as directory, then fall back to displaying a 404.
            try_files $uri $uri/ =404;
        }
        location ~ /ws/? {
            access_log off;
            proxy_pass http://websockets;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header Host $host;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_http_version 1.1;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection "upgrade";
        }
    }
    ###### altcap.io ######

    CTRL+X to save (^X Exit)

You have now setup an SSL secured web server with a WebSocket connected to your local BitShares witness_node (listening on port 8090 - see [his post](https://steemit.com/bitshares/@ihashfury/run-your-own-decentralised-exchange) for more information) ###Update altcap.io www virtual host

    sudo cp altcap.io /etc/nginx/sites-available/altcap.io

**Restart Nginx**

    sudo service nginx restart

Now you have setup an SSL web server. More information on SSL setup can be found here. 
- [DigitalOcean letsencrypt SSL](https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-14-04) 
- [LetsEncrypt CertBot](https://letsencrypt.org/)

***

## Install BitShares web gui

**Install NVM (Node Version Manager)**

    curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.30.2/install.sh | bash

exit bash (terminal) and reconnect

    ssh bitshares@altcap.io
    nvm install v5
    nvm use v5

**Download BitShares gui**

    git clone https://github.com/bitshares/bitshares-2-ui.git

**Setup light wallet**

    cd /bitshares-2-ui/

Before building the light wallet, you need to edit SettingsStore.js line 19 and 99 wss WebSocket.

    nano /bitshares-2-ui/dl/src/stores/SettingsStore.js

Change line 19

    connection: "wss://altcap.io/ws",

Add your new wss WebSocket to line 99

            connection: [
                "wss://altcap.io/ws",
                "wss://bitshares.openledger.info/ws",
                "wss://bitshares.dacplay.org:8089/ws",
                "wss://dele-puppy.com/ws",
                "wss://valen-tin.fr:8090/ws"

    CTRL+X to save (^X Exit)

    ###Setup install
    cd dl; npm install
    cd ../web; npm install

**Link web root to gui build folder**

    ln -s ~/public_html/ dist

**Build light wallet**

    npm run build

You have now created another Access point to the BitShares Decentralised Exchange. The more the merrier. Please remember to check your firewall and SSH is up-to-date and configured correctly. DigitalOcean has firewall and Secure SSH tutorials for more help.

## SSL test

You can also check how secure your new web server is compared to your bank. Add this link to a web browser and wait for the results.

    https://www.ssllabs.com/ssltest/analyze.html?d=altcap.io

Now change altcap.io to your local bank’s domain name in the link and post the results below. >Thank you `svk <https://steemit.com/@svk>`__ for your advice and guidance.


    









