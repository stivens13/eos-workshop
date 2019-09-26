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

`cleos wallet list`

`cleos wallet create --to-console`

`cleos wallet open`

`cleos wallet list`

`cleos wallet unlock`

`cleos wallet list`

`cleos wallet create_key`

`cleos wallet import`

`eosio` dev master key `5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3`
