# Chainlink Smart Contracts

> [!IMPORTANT]
> Since v1.5.0 of the Chainlink contracts, some dependencies are no longer vendored. 
> This change results in the use of remappings to resolve import paths.
>
> Since v1.4.0 of the Chainlink contracts, the contracts have been moved to their own repository:
> [chainlink-evm](https://github.com/smartcontractkit/chainlink-evm).
> Prior to that, the contracts were part of the [main Chainlink repository](https://github.com/smartcontractkit/chainlink)

## Installation

### NPM

```sh
# pnpm
$ pnpm add @chainlink/contracts
```

```sh
# npm
$ npm install @chainlink/contracts --save
```

## Environment Setup

### Update your project's remappings

#### Foundry/Hardhat 3:

[Foundry](https://getfoundry.sh/guides/project-setup/project-layout#project-layout) and [Hardhat 3](https://hardhat.org/docs) consume a `remappings.txt` file from the project root. Create or update `remappings.txt` with:

```
@chainlink/=node_modules/@chainlink
@openzeppelin/contracts@4.7.3=node_modules/@openzeppelin/contracts-4.7.3
@openzeppelin/contracts@4.8.3=node_modules/@openzeppelin/contracts-4.8.3
@openzeppelin/contracts@4.9.6=node_modules/@openzeppelin/contracts-4.9.6
@openzeppelin/contracts@5.0.2=node_modules/@openzeppelin/contracts-5.0.2
@openzeppelin/contracts@5.1.0=node_modules/@openzeppelin/contracts-5.1.0
@openzeppelin/contracts-upgradeable/=node_modules/@openzeppelin/contracts-upgradeable/
@arbitrum/=node_modules/@arbitrum/
@eth-optimism/=node_modules/@eth-optimism/
@scroll-tech/=node_modules/@scroll-tech/
@zksync/=node_modules/@zksync/
```

If your compilation reports unresolved imports from dependencies, add the corresponding additional remappings to `remappings.txt` (the format is `<prefix>=<resolved-path>/`).

See the [Foundry starter kit](https://github.com/smartcontractkit/foundry-starter-kit) or [Hardhat 3 starter kit](https://github.com/smartcontractkit/hardhat-starter-kit/tree/hardhat3) for working examples.

#### Foundry (Optional):

In your project's `foundry.toml`, update the libs array to include the `node_modules` directory.

```
libs = ['lib', "node_modules"]
```

#### Hardhat 2 (preprocessor):

Hardhat 2 does not read `remappings.txt` natively as seen in Foundry/Hardhat 3. To remap the import paths, you may opt to use a preprocessor that remaps the import paths at compile time. To see remapping examples in Hardhat 2, review the [Hardhat 2 starter kit](https://github.com/smartcontractkit/hardhat-starter-kit/tree/hardhat2).

#### Remix (no extra setup)

Remix works out of the box. Use standard imports and compile:

```solidity
import "@chainlink/contracts/src/v0.8/...";
```

### Directory Structure

> [!IMPORTANT]
> Since v1.5.0 of the Chainlink contracts, ABI files have been reorganized into subdirectories.
> Additionally, ABI files have seen a minor change in naming scheme.

```sh
@chainlink/contracts
├── src # Solidity contracts
│   └── v0.8
└── abi # ABI json output
    └── v0.8
```

### Usage

The solidity smart contracts themselves can be imported via the `src` directory of `@chainlink/contracts`:

```solidity
import {IVerifier} from '@chainlink/contracts/src/v0.8/llo-feeds/v0.5.0/interfaces/IVerifier.sol';
```

---

## Local Development

**Note:** Contracts in `dev/` directories or with a typeAndVersion ending in `-dev` are under active development and are likely unaudited. Please refrain from using these in production applications.

```bash
# Clone Chainlink repository
$ git clone https://github.com/smartcontractkit/chainlink.git
$ cd contracts/
$ pnpm
```

Each Chainlink project has its own directory under `src/` which can be targeted using Foundry profiles. To test a specific project, run:

```bash
# Replace <project> with the product you want to test
export FOUNDRY_PROFILE=<project>
forge test
```

To test the llo-feeds (data steams) project:

```bash
export FOUNDRY_PROFILE=llo-feeds
forge test
```

## Contributing

Please adhere to the [Solidity Style Guide](https://github.com/smartcontractkit/chainlink-evm/blob/develop/contracts/STYLE_GUIDE.md).

Contributions are welcome! Please refer to
[Chainlink's contributing guidelines](https://github.com/smartcontractkit/chainlink/blob/develop/docs/CONTRIBUTING.md) for detailed
contribution information.

Thank you!

### Changesets

We use [changesets](https://github.com/changesets/changesets) to manage versioning the contracts.

Every PR that modifies any configuration or code, should most likely accompanied by a changeset file.

To install `changesets`:

1. Install `pnpm` if it is not already installed - [docs](https://pnpm.io/installation).
2. Run `pnpm install`.

Either after or before you create a commit, run the `pnpm changeset` command in the `contracts` directory to create an accompanying changeset entry which will reflect on the CHANGELOG for the next release.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),

and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).
