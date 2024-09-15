## 1 - criando pasta

```sh
mkdir ./wallets
mkdir ./wallets/erc20

export WALLET="$PWD/wallets/erc20"

echo $WALLET
```

# 1 - Key

## 1.1 - criando _nova_ pvt key (não existe)

```sh
starkli signer keystore new $WALLET/usr_keystore.json

export STARKNET_KEYSTORE="$WALLET/usr_keystore.json"

echo $STARKNET_KEYSTORE
```

## 1.2 - conectando com a pvt local (caso já exista)

```sh
starkli signer keystore from-key $STARKNET_KEYSTORE
```

# 2 - [_Signers_](https://book.starkli.rs/signers)

## 2.1 - criando conta

```sh
starkli account oz init $WALLET/usr_account.json

Enter keystore password:
Created new account config file: /Users/aquental/projects/starknet/token-sender-erc20-basecamp2/wallets/erc20/usr_account.json

Once deployed, this account will be available at:
    0x06ce402762229fdcf7970969b79473d80b528503e69f8bd4c73a29a9e4d808c1

Deploy this account by running:
    starkli account deploy /Users/aquental/projects/starknet/token-sender-erc20-basecamp2/wallets/erc20/usr_account.json


starkli account deploy $WALLET/usr_account.json

Enter keystore password:
The estimated account deployment fee is 0.000007968074030020 ETH. However, to avoid failure, fund at least:
    0.000011952111045030 ETH
to the following address:
    0x06ce402762229fdcf7970969b79473d80b528503e69f8bd4c73a29a9e4d808c1
Press [ENTER] once you've funded the address.
Account deployment transaction: 0x02ff8b02890eeacbf873dc731ecdb8d4e475943d3a6ac37b5e7bccc2f992028d
Waiting for transaction 0x02ff8b02890eeacbf873dc731ecdb8d4e475943d3a6ac37b5e7bccc2f992028d to confirm. If this process is interrupted, you will need to run `starkli account fetch` to update the account file.
Transaction not confirmed yet...
Transaction 0x02ff8b02890eeacbf873dc731ecdb8d4e475943d3a6ac37b5e7bccc2f992028d confirmed

export ACC="0x06ce402762229fdcf7970969b79473d80b528503e69f8bd4c73a29a9e4d808c1"
```

## 2.2 - conectando com a conta local

```sh
cat $WALLET/usr_account.json
echo $ACC

starkli account fetch $ACC --output $WALLET/usr_account.json

Account contract type identified as: OpenZeppelin
Description: OpenZeppelin account contract v0.13.0 compiled with cairo v2.6.3
Downloaded new account config file: /Users/aquental/projects/starknet/token-sender-erc20-basecamp2/wallets/erc20/usr_account.json
```

# 3 - Deploy

## 3.1 - declarando o token

### free RPC endpoint [services](https://www.starknet.io/fullnodes-rpc-services/)

|        Org | testnet                                     | mainnet                                     |
| ---------: | ------------------------------------------- | ------------------------------------------- |
|       Lava | https://rpc.starknet-testnet.lava.build:443 | https://rpc.starknet.lava.build:443         |
|      Blast | https://starknet-sepolia.public.blastapi.io | https://starknet-mainnet.public.blastapi.io |
| Nethermind | https://free-rpc.nethermind.io/sepolia-juno | https://free-rpc.nethermind.io/mainnet-juno |

```sh
export STARKNET_RPC="https://free-rpc.nethermind.io/sepolia-juno"

echo $STARKNET_KEYSTORE
echo $STARKNET_ACCOUNT
echo $STARKNET_RPC

starkli declare ./target/dev/token_sender_AQuentalToken.compiled_contract_class.json --account $WALLET/usr_account.json
```
