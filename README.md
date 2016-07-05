Perma ("permaledger") bootstrapping guidelines
---

- Genesis block is determined by Ethereum hard fork block hash / timestamp. Network id 42.
    - Testnet uses proposed soft fork parameters, network id 43
- Quick and dirty distribution with exponentially decaying block rewards has two goals:

    - It emulates a proof of burn from the ETH miners and holders directly after the hard fork block.
    - It should quickly reach an equilibrium state where transaction fees pay for POW to the extent that apps collectively can and want to subsidize the chain's security.

- The base token, "FEE", is to be framed as a claim on finite future network resources (especially cpu-hours). The supply converges to 1 FEE.
- `bootstrap.txt` is insignficant when not "instantiated" in a chain. "It" can be "modified"; the bootstrap document actually encoded in Perma cannot.


#### Join "Tempa1" Test Network

clone geth fork:

    git clone https://github.com/permaledger/go-perma
    cd go-perma
    git checkout perma-1.4.9-dev
    make geth

`tempa1_genesis.json`:

    {
        "nonce": "0x35f59c4c569b9973450e8d738f9e8027139c235169114690951dc2e8a159894d",
        "timestamp": "0x57754AF2",
        "parentHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
        "extraData": "0x1",
        "gasLimit": "0x80000000",
        "difficulty": "0x424242",
        "mixhash": "0x0000000000000000000000000000000000000000000000000000000000000000",
        "coinbase": "0x0000000000000000000000000000000000000000",
        "alloc": {}
    }

initialize:

    ./build/bin/geth --datadir ~/.tempa1 --keystore ~/.tempa1-keystore init tempa1_genesis.json

connect:

    ./build/bin/geth --datadir ~/.tempa1 --keystore ~/.tempa1-keystore --networkid 43

mine with new account:

    ./build/bin/geth --datadir ~/.tempa1 --keystore ~/.tempa1-keystore account new
    ./build/bin/geth --datadir ~/.tempa1 --keystore ~/.tempa1-keystore --networkid 43 --mine

Submit your bootnodes in the issues.
