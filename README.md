# eos-workshop

# Install EOSIO and EOSIO.CDT
 
## Mac OS X Brew Install:

```
brew tap eosio/eosio
brew install eosio

brew tap eosio/eosio.cdt
brew install eosio.cdt
```

## Ubuntu 18.04 Debian Package Install
```
wget https://github.com/EOSIO/eos/releases/download/v1.7.0/eosio_1.7.0-1-ubuntu-18.04_amd64.deb
sudo apt install ./eosio_1.7.0-1-ubuntu-18.04_amd64.deb

wget https://github.com/EOSIO/eosio.cdt/releases/download/v1.6.1/eosio.cdt_1.6.1-1_amd64.deb
sudo apt install ./eosio.cdt_1.6.1-1_amd64.deb
```
Note, for other Ubuntu distros change distro number

## Windows

Follow this article https://medium.com/@TeaSea1/how-to-install-eos-on-windows-ac1b6c7d8369

# Launch

## Start keosd

```keosd &```

## Start nodeos

```
nodeos -e -p eosio \
--plugin eosio::producer_plugin \
--plugin eosio::chain_api_plugin \
--plugin eosio::http_plugin \
--plugin eosio::history_plugin \
--plugin eosio::history_api_plugin \
--access-control-allow-origin='*' \
--contracts-console \
--http-validate-host=false \
--verbose-http-errors >> nodeos.log 2>&1 &

curl http://localhost:8888/v1/chain/get_info
```

# Wallet 

## Set up

`cleos wallet list`

`cleos wallet create --to-console`

`cleos wallet open`

`cleos wallet list`

`cleos wallet unlock`

`cleos wallet list`

`cleos wallet create_key`

`cleos wallet import`

`eosio` dev master key `5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3`

## Create Test Accounts

```
cleos create account eosio bob EOS5CgziDQ9Lqa9USmeP1kV8zK76CZKCaER6F375dRYb6b5smWSBT 
cleos create account eosio alice EOS5CgziDQ9Lqa9USmeP1kV8zK76CZKCaER6F375dRYb6b5smWSBT
```

`cleos get account alice`

# Submit Smart Contracts to the Blockchain

## Compile your .cpp file

`eosio-cpp hello.cpp -o hello.wasm`

## Create Smart Contract account interface

Choose a public key from
`cleos wallet keys`

And then use it to create an interface account
`cleos create account eosio hello {PUBLIC_KEY} -p eosio@active`

`cleos set contract hello CONTRACT_ABSOLUTE_PATH -p hello@active`

## Interact with it

```
cleos push action hello hi '["bob"]' -p bob@active
cleos push action hello hi '["bob"]' -p alice@active
```

## Change it

Add another line to hi() 
```
void hi( name user ) {
   require_auth( user );
   print( "Hello, ", name{user} );
}
```
Recompile 
`eosio-cpp -abigen -o hello.wasm hello.cpp`
Submit to network
`cleos set contract hello CONTRACTS_DIR/hello -p hello@active`

Try again 
`cleos push action hello hi '["bob"]' -p alice@active`
