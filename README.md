Gnosis Safe Deployments
=======================

## Install
- npm - `npm i @gnosis.pm/safe-deployments`
- yarn - `yarn add @gnosis.pm/safe-deployments`

## Usage

It is possible to directly use the json files in the [assets folder](./src/assets/) that contain the addresses and abi definitions.

An alternative is to use the JavaScript library methods to query the correct deployment. The library supports different methods to get the deployment of a specific contract.

Each of the method takes an optional `DeploymentFilter` as a parameter.

```ts
interface DeploymentFilter {
    version?: string,
    released?: boolean, // Defaults to true if no filter is specified
    network?: string // Chain id of the network
}
```

The method will return a `SingletonDeployment` object or `undefined` if no deployment was found for the specified filter.

```ts
interface SingletonDeployment {
    defaultAddress: string, // Address the contract was deployed to by the Gnosis team
    version: string,
    abi: any[],
    networkAddresses: Record<string, string>, // Address of the contract by network
    contractName: string,
    released: boolean // A released version was audited and has a running bug bounty
}
```

- Gnosis Safe
```ts
const safeSingleton = getSafeSingletonDeployment()

// Returns latest contract version, even if not finally released yet
const safeSingletonNightly = getSafeSingletonDeployment({ released: undefined })

// Returns released contract version for specific network
const safeSingletonGörli = getSafeSingletonDeployment({ network: "5" })

// Returns released contract version for specific version
const safeSingleton100 = getSafeSingletonDeployment({ version: "1.0.0" })

// Version with additional events used on L2 networks
const safeL2Singleton = getSafeL2SingletonDeployment()
```

- Factories
```ts
const proxyFactory = getProxyFactoryDeployment()
```

- Libraries
```ts
const multiSendLib = getMultiSendDeployment()

const multiSendCallOnlyLib = getMultiSendCallOnlyDeployment()

const createCallLib = getCreateCallDeployment()
```

- Handler
```ts
// Returns recommended handler
const fallbackHandler = getFallbackHandlerDeployment()

const callbackHandler = getDefaultCallbackHandlerDeployment()

const compatHandler = getCompatibilityFallbackHandlerDeployment()
```

Security and Liability
----------------------
All contracts are WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

License
-------
All code is released under LGPL-3.0
