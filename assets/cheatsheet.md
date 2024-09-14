## 1 - criando pasta

```sh
mkdir ./wallets
mkdir ./wallets/erc20
```

# 1 - Key

## 1.1 - criando _nova_ pvt key (não existe)

```sh
starkli signer keystore new ./wallets/erc20/usr_keystore.json

export STARKNET_KEYSTORE="$PWD/wallets/erc20/usr_keystore.json"

echo $STARKNET_KEYSTORE
```

## 1.2 - conectando com a pvt local (caso já exista)

```sh
starkli signer keystore from-key $STK_KS
```

# 2 - [_Signers_](https://book.starkli.rs/signers)

## 2.1 - criando conta

```sh
starkli account oz init ./wallets/erc20/usr_account.json
Enter keystore password:
Created new account config file: /Users/aquental/projects/starknet/token-sender-erc20-basecamp2/wallets/erc20/usr_account.json

Once deployed, this account will be available at:
    0x00c8101fa47aaf8aee8942e042aa102f9be6fe4049fc88c301d0bf8211dc6479

Deploy this account by running:
    starkli account deploy ./wallets/erc20/usr_account.json


starkli account deploy ./wallets/erc20/usr_account.json
WARNING: you're using neither --rpc (STARKNET_RPC) nor --network (STARKNET_NETWORK). The `sepolia` network is used by default. See https://book.starkli.rs/providers for more details.
Enter keystore password:
The estimated account deployment fee is 0.000049167346023640 ETH. However, to avoid failure, fund at least:
    0.000073751019035460 ETH
to the following address:
    0x00c8101fa47aaf8aee8942e042aa102f9be6fe4049fc88c301d0bf8211dc6479
Press [ENTER] once you've funded the address.
Account deployment transaction: 0x01a95bc2594734a04857746a0145ded79dc91cb4df488e12836572e5e0b143cb
Waiting for transaction 0x01a95bc2594734a04857746a0145ded79dc91cb4df488e12836572e5e0b143cb to confirm. If this process is interrupted, you will need to run `starkli account fetch` to update the account file.
Transaction not confirmed yet...
Transaction 0x01a95bc2594734a04857746a0145ded79dc91cb4df488e12836572e5e0b143cb confirmed
```

## 2.2 - conectando com a conta local

```sh
cat ./wallets/erc20/usr_account.json

starkli account fetch 0x00c8101fa47aaf8aee8942e042aa102f9be6fe4049fc88c301d0bf8211dc6479 --rpc <???> --output ./wallets/erc20/usr_account.json
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
starkli declare target/dev/token_sender_AQuentalToken.compiled_contract_class.json --rpc
```
