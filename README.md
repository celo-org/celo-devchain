# celo-devchain

Ganache setup with core Celo contracts for local testing and development.
Now supports `node18`.

## Usage

```
> npm install --save-dev @celo/celo-devchain
> npx celo-devchain --port 7545
```

```
# Run sanity tests and print all core contract addresses:
> npx @celo/celo-devchain --test
```


NOTE: @celo/ganache-cli currently doesn't support locally signed transactions. If you send
a locally signed transaction it will throw: `Error: Number can only safely store up to 53 bits`
error and crash. Thus you have to make sure your ContractKit doesn't actually have the private
keys for test addresses and send transactions to be signed by ganache-cli itself.

Example code that uses this package: https://github.com/zviadm/celo-hellocontracts

## Chain Data

Chain data in `./chains` folder is generated using steps described here: https://docs.celo.org/developer-guide/development-chain.
```
# Start with a fresh checkout to avoid build complications.
> git clone https://github.com/celo-org/celo-monorepo.git
> git fetch --all --tags
> git tag -l core-contracts*
> git checkout tags/core-contracts.v{version}

# Yarn commands can take a while to run.
> yarn
> yarn build

> cd packages/protocol
# NOTE: The following command is based on the number of migrations available in the protocol package. 
# At some point the desired `--upto` flag can change based on changes in core-contracts, 
# thus you might have to adjust it too, depending on which version of core-contracts
# you are attempting to build.
> yarn devchain generate-tar .tmp/devchain.tar.gz --migration_override ../dev-utils/src/migration-override.json --upto 28
```

You can also use `celo-devchain` with custom generated chain data:
```
> npx celo-devchain --file <path to custom chain data>
```
