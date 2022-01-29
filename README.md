# How to Setup Ethereum Private Network #

***Step 1 : Create few sample accounts to use on the network***

    $ geth --datadir "nodedata" account new

![Step 1](/assets/Step1.png)

***Step 2 : Use `puppeth` to initialize network***

    $ puppeth

> Geth 1.6 ships a new tool called puppeth, which aims to solve this particular pain point. Puppeth is a CLI wizard that aids in creating a new Ethereum network down to the genesis, bootnodes, signers, ethstats, faucet, dashboard and more, without the hassle that it would normally take to configure all these services one by one. Puppeth uses ssh to dial into remote servers, and builds its network components out of docker containers using docker-compose. The user is guided through the process via a command line wizard that does the heavy lifting and topology configuration automatically behind the scenes.


    
*Follow the wizard steps*

![Step 2](/assets/Step2.png) 

*... and continue few more steps*

![Step 3](/assets/Step3.png) 

    Ctrl + D 
    [to exit puppets prompt]


***Step 3 : Initiate blockchain with genesis block***

    $ geth --datadir ./nodedata/ init ajit.json

![Step 4](/assets/Step4.png)


***Step 4 : Run Node***

    $ geth --identity "AJIT" --networkid "5777" --datadir "nodedata" --http --http.port "8545" --unlock "0" --http.corsdomain "*" --http.api "miner,eth,net,web3,personal" --allow-insecure-unlock --nodiscover --miner.etherbase "0x3f6006424f39039C7ab161A8b442be4DAd7f503c"

![Step 5](/assets/Step5.png)

> At this point the ethereum node is ready. The account 0x3f6006424f39039C7ab161A8b442be4DAd7f503c is the one which we created in first step. This account will be used as "etherbase", which means "mining" rewards will be transferred to this account.

> Next step we need to attach this node using IPC. You can locate IPC path in Step 4 output

![Step 6](/assets/Step6.png)

> Open new terminal and run following command

    $ geth attach ipc:/{working directory path}/nodedata/geth.ipc

> This command will connect Geth JavaScript console to the ethernet node created in earlier step

![Step 7](/assets/Step7.png)

> 1. Note that AJIT is the instance of the node in this example. 
> 2. Coinbase (etherbase) account is 0x3f6006424f39039C7ab161A8b442be4DAd7f503c which we configured. 
> 3. Node data (blocks) will be stored at directory "nodedata"
> 4. We have enabled accounts "admin", "debug", "eth", "ethash", "miner", "net", "personal", "rpc", "txpool" and "web3" while running the note in Step 4

> Now to start auto-mining on this node run following command in Geth JavaScript console

    $ miner.start()

![Step 8](/assets/Step8.png)

> Go to the terminal instance in which we have started the node, you will observe polling status to mine the block. If try to do any "transfer" at this point, it will be auto mined.

![Step 9](/assets/Step9.png)

***Step 4 : Transfer Ether***

> We have only one account active in our node and that is the "coinbase" account. Let's create two more account so that we can trasnfer ether between accounts. Follow Step 1 to create two mode accounts

![Step 10](/assets/Step10.png)


> Following two accounts are now ready to use 0xE481bc9a0bD07D9aDD366277D4f0181464a6f341 and 0xbE2186604DFaB58FeA8b675268db31D2e0678f58
> Use eth.accounts and eth.getBalance commands to list the accounts and check balance


![Step 11](/assets/Step11.png)

> Newly created accout has zero balance. First account has some balance since we have mentioned to fund it while creating genesis block. We can also pre-create accounts and then mention opening balance of the account in genesis config file, in our case we could mention in ajit.congig file
> Use following command to transfer some Wei (Geth JavaScript console). 

    $ eth.sendTransaction({from: '0x3f6006424f39039C7ab161A8b442be4DAd7f503c', to: '0xe481bc9a0bd07d9add366277d4f0181464a6f341', value: 100})


![Step 12](/assets/Step12.png)

> 0xf1b5e15e371a7a0edac4edc9661cccaa1b338c472c754f2d8efabb17c947454b is the transaction hash
> Also observe mining log in "node termin console"

![Step 13](/assets/Step13.png)

> Run following command in Geth console to view details of the transaction

    $ eth.getTransaction('0xf1b5e15e371a7a0edac4edc9661cccaa1b338c472c754f2d8efabb17c947454b')

![Step 14](/assets/Step14.png)

> Check balance again. 0xe481bc9a0bd07d9add366277d4f0181464a6f341 account has 100 Wei now.

![Step 15](/assets/Step15.png)


## Useful Links ##


### Some communities that you can join: ###

- [Gitter](https://gitter.im/ethereum/home)
- [Reddit](https://www.reddit.com/r/ethereum/)
- [Stack Exchange](https://ethereum.stackexchange.com/)
- [KBA Official Telegram Channel](https://t.me/joinchat/EvALMU17xeIpb8NPWA3NFQ)
- [KBA Facebook](https://m.facebook.com/profile.php?id=667759250100685&ref=content_filter)
- [KBA Official LinkedIn Group](https://www.linkedin.com/groups/13861449/)
- [Go Ethereum Discord Channel](https://discord.gg/24NwzHqm)
- [Blockchain Education Network](https://www.blockchainedu.org/)
- [Ethereum Community List](https://ethereum.org/en/community/)

### The below links are some points of interest: ###

- [Capture the Ether](https://capturetheether.com/)
- [ETH.Build](https://eth.build/)
- [Gitcoin](https://gitcoin.co/)
- [Scaffold-ETH](https://github.com/austintgriffith/scaffold-eth)
- [Damn Vulnerable Defi](https://www.damnvulnerabledefi.xyz/)
- [Ethereum Mainnet Statistics](https://www.ethernodes.org/)
- [Cryptozombies.io][(https://cryptozombies.io/)
- [Solidity by example](https://solidity-by-example.org/)
- [Hardhat](https://hardhat.org/)

### Ethereum Frameworks and pre-made stacks ###

- [Vyper](https://vyper.readthedocs.io/en/stable/)
- [Ethereum Learning tools](https://ethereum.org/en/developers/learning-tools/)
- [Ethereum Dev Articles](https://ethereum.org/en/developers/tutorials/)
- [Ethereum Offical Doc](https://ethereum.org/en/developers/docs/)
- [TypeChain](https://github.com/ethereum-ts/TypeChain)


### Test Nets

#### Ropsten
- https://faucet.ropsten.be/
- https://faucet.dimensions.network/
- https://ropsten.chain.link/
– https://ropsten.etherscan.io/

#### Kovan
- https://faucet.kovan.network/
– https://kovan.etherscan.io/

#### Goerli
- https://goerli-faucet.slock.it/
- https://faucet.goerli.mudit.blog/
– https://goerli.etherscan.io/

#### Rinkeby
- https://faucet.rinkeby.io/
– https://rinkeby.etherscan.io/

#### Mainnet
- https://etherscan.io/

#### web3.js - Ethereum JavaScript API
- https://web3js.readthedocs.io/en/v1.2.11/

#### Gas Metrics chart
- https://docs.google.com/spreadsheets/d/1n6mRqkBz3iWcOlRem_mO09GtSKEKrAsfO7Frgx18pNU/edit#gid=0
