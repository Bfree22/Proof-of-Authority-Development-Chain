# Setting-up-Proof-of-Authority-Development-Chain


### This repo contains instructions on how to setup and run a testnet blockchain for your organization ZBank.

____________________________________


## Geth

* Download the appropriate Geth (Go Ethereum) version from the following link: https://geth.ethereum.org/downloads/ 

* Unzip the folder and Open Git bash / Terminal inside the folder.


## Create Nodes

1. Create two accounts for node1 and node2 using the following command

- ./geth account new --datadir node1
- ./geth account new --datadir node2

* ( It will give you a public key and a secret key file. Make sure to save both from each node somewhere. It will look something like 0x3F35k9GBnq98l0C2587DsAplOnbg81FhjkK )


## Genesis Block

 2. Create genesis block

* Run the following commands:

- ./puppeth

- Network_name

- Configure a new genesis block

- Choose Clique (Proof of Authority) algorithm

- Copy both addresses from step 1 and paste them into the list of account to seal.

- Paste the addresses again into the accounts to pre-fund

- Type "no" for pre-funding compiler

- Add a chain ID. ( This can be any number, for example : 55 )

- Complete the rest of the prompts, and when you are back at the main menu, choose the "Manage existing genesis" option.

- Export genesis configurations. This will fail to create two of the files, but you only need 'network_name.json'. (Check to see if the nodes are inside the folder)


3. Initialize the Nodes

* Run the following commands using Geth.

- ./geth init network_name.json --datadir node1
- ./geth init network_name.json --datadir node2


4. Set the nodes to mine blocks and Synchronize

* Open up 2 seperate terminal windows inside the same geth folder and run the following commands in a seperate terminal:

- ./geth --datadir node1 --unlock "Public Address for Node1" --mine --rpc --allow-insecure-unlock
-  ./geth --datadir node2 --unlock "Public Address for Node2" --mine --port 30304 --bootnodes "enode://SEALER_ONE_ENODE_ADDRESS@127.0.0.1:30304" --ipcdisable --allow-insecure-unlock

* You should now see both nodes producing new blocks, congratulations!



## Send a test transaction

* Use the MyCrypto GUI wallet to connect to the node with the exposed RPC port.

* You will need to use a custom network, and include the chain ID, and use ETH as the currency.

* Import the keystore file from the node1/keystore directory into MyCrypto. This will import the private key.

* Send a transaction from the node1 account to the node2 account. ( Do this buy going to the dropdown menu at the top and clicking "Send Ether Tokens", then paste the address of node2 )

![transaction_metadata](/Screenshots/Transaction-metadata.png)

* Congrats, you just created a blockchain and sent a transaction!
