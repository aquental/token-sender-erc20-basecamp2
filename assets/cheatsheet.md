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

Enter private key:
Enter password:
Created new encrypted keystore file: /Users/aquental/projects/starknet/token-sender-erc20-basecamp2/wallets/erc20/usr_keystore.json
Public key: 0x002b091e333b5e8757a766ca1ce48a91472863955d01785d8f6beb971b424ef9
```

# 2 - [_Signers_](https://book.starkli.rs/signers)

## 2.1 - criando conta

```sh
starkli account oz init $WALLET/usr_account.json

Enter keystore password:
Created new account config file: /Users/aquental/projects/starknet/token-sender-erc20-basecamp2/wallets/erc20/usr_account.json

Once deployed, this account will be available at:
    0x048c1439fc0151535234636810fc546a460f302ed9ff1671b5c6fea3b8e5034e

Deploy this account by running:
    starkli account deploy /Users/aquental/projects/starknet/token-sender-erc20-basecamp2/wallets/erc20/usr_account.json

starkli account deploy $WALLET/usr_account.json

Enter keystore password:
The estimated account deployment fee is 0.000010962449475380 ETH. However, to avoid failure, fund at least:
    0.000016443674213070 ETH
to the following address:
    0x048c1439fc0151535234636810fc546a460f302ed9ff1671b5c6fea3b8e5034e
Press [ENTER] once you've funded the address.
Account deployment transaction: 0x00fd1d372bd26adc6d58a0ab5eaa31ec0058c1a5c8fa7e8ef180e53e4acf460d
Waiting for transaction 0x00fd1d372bd26adc6d58a0ab5eaa31ec0058c1a5c8fa7e8ef180e53e4acf460d to confirm. If this process is interrupted, you will need to run `starkli account fetch` to update the account file.
Transaction not confirmed yet...
Transaction 0x00fd1d372bd26adc6d58a0ab5eaa31ec0058c1a5c8fa7e8ef180e53e4acf460d confirmed

export ACC="0x048c1439fc0151535234636810fc546a460f302ed9ff1671b5c6fea3b8e5034e"
```

## 2.2 - conectando com a conta local

```sh
export STARKNET_ACCOUNT="$WALLET/usr_account.json"

cat $STARKNET_ACCOUNT
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

starkli declare ./target/dev/token_sender_AQuentalToken.contract_class.json --account $WALLET/usr_account.json

Enter keystore password:
Sierra compiler version not specified. Attempting to automatically decide version to use...
Network detected: sepolia. Using the default compiler version for this network: 2.7.1. Use the --compiler-version flag to choose a different version.
Declaring Cairo 1 class: 0x043088b4fd786972c13e23e2ec36f83c7560895910ddabf25f61679da919717f
Compiling Sierra class to CASM with compiler version 2.7.1...
CASM class hash: 0x00789ba119feecf7bb2697e1910645846205f7c22d32600f499dddc3ad145b5c
Contract declaration transaction: 0x0112f69613f41d6508bddd057d291ba5cf76d415df0738521abc6e90c82ca6ae
Class hash declared:
0x043088b4fd786972c13e23e2ec36f83c7560895910ddabf25f61679da919717f
```

## 3.2 - deploy [docs]()

```sh
starkli deploy 0x043088b4fd786972c13e23e2ec36f83c7560895910ddabf25f61679da919717f u256:1000000000 $ACC

Enter keystore password:
Deploying class 0x043088b4fd786972c13e23e2ec36f83c7560895910ddabf25f61679da919717f with salt 0x00996bf2f84cdcd183830abbef772d330fd4c1b4ef231e543d12bdf3efc9fce8...
The contract will be deployed at address 0x00640b0646b8344fed536aeb519c6a696cd03311ee03edd9a0e518eb0d4d07fa
Contract deployment transaction: 0x0029eafe189d5dadfb7563c20c4e8d4ceb1567e8101c8fcee49997e2ea65d484
Contract deployed:
0x00640b0646b8344fed536aeb519c6a696cd03311ee03edd9a0e518eb0d4d07fa
```

[sepolia contract](https://sepolia.voyager.online/contract/0x00640b0646b8344fed536aeb519c6a696cd03311ee03edd9a0e518eb0d4d07fa)
