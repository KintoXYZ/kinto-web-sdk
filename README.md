# Kinto Wallet SDK

Kinto SDK is a JavaScript library that allows applications to connect to the Kinto Wallet. Kinto is an Ethereum Layer 2 (L2) solution designed to provide fast and cost-efficient transactions. This SDK provides methods to connect a Kinto Wallet, send transactions, and create new wallets.

## Table of Contents

- [Principles](#principles)
- [Installation](#installation)
- [Usage](#usage)
  - [Prerequisites](#prerequisites)
  - [Initialization](#initialization)
  - [Connecting to Kinto Wallet](#connecting-to-kinto-wallet)
  - [Sending Transactions](#sending-transactions)
  - [Creating a New Wallet](#creating-a-new-wallet)
- [API](#api)
  - [KintoSDK](#kintosdk)
    - [connect()](#connect)
    - [sendTransaction()](#sendtransaction)
    - [createNewWallet()](#createnewwallet)
  - [Types](#types)
- [Contributing](#contributing)
- [License](#license)

## Design Principles

The Kinto SDK has been designed with the following principles in mind:

- **No Dependencies**: The SDK is built without external dependencies to minimize its size and maximize security. This ensures that it doesn't rely on any third-party libraries.

- **No UI**: The SDK does not provide any user interface components. This allows app developers the flexibility to design their own UI and remain unopinionated about the user experience.

- **No Web3 Packages**: The SDK is agnostic to specific Ethereum libraries. You can use any library you prefer, such as `viem`, `ethers`, or `web3js`. The SDK itself doesn't require any of these packages.

## Installation

You can install the Kinto SDK via npm:

```bash
npm install kinto-web-sdk
```

## Usage

### Prerequisites

Before using the Kinto SDK, ensure you have completed the following steps:

1. **Kinto Wallet**: You need to have a Kinto wallet. Create an account by visiting [Kinto Onboarding](https://engen.kinto.xyz/onboarding).

2. **Developer Account**: Create a developer account, deploy a contract, and create the application. Use your main contract address as the app address. Visit [Kinto Developers](https://engen.kinto.xyz/developers) to get started.

### Initialization

To use the Kinto SDK, you need to initialize it with your application's address.

```javascript
import { createKintoSDK } from 'kinto-web-sdk';

const appAddress = 'your-app-address';
const kintoSDK = createKintoSDK(appAddress);
```

### Connecting to Kinto Wallet

To connect to the Kinto Wallet, use the `connect` method. This method opens a modal for the user to connect their wallet.

```javascript
kintoSDK.connect()
  .then((accountInfo) => {
    console.log('Connected account info:', accountInfo);
  })
  .catch((error) => {
    console.error('Failed to connect:', error);
  });
```

### Sending Transactions

To send transactions, use the `sendTransaction` method. This method accepts an array of transaction objects.

```javascript
const transactions = [
  {
    to: '0xRecipientAddress',
    value: '1000000000000000000', // 1 ETH in wei`
    data: '0x'
  }
];

kintoSDK.sendTransaction(transactions)
  .then((hash) => {
    console.log('Transaction successful, hash:', hash);
  })
  .catch((error) => {
    console.error('Transaction failed:', error);
  });
```

### Creating a New Wallet

To create a new wallet, use the `createNewWallet` method. This method opens a popup for the user to create a new wallet in Kinto website. Alternatively, you can instruct users to visit [Kinto](https://engen.kinto.xyz/onboarding) to create an account.

```javascript
kintoSDK.createNewWallet()
  .then(() => {
    console.log('New wallet created successfully');
  })
  .catch((error) => {
    console.error('Failed to create new wallet:', error);
  });
```

## API

### KintoSDK

#### connect()

Starts a connection with a logged-in Kinto Wallet and returns the account information.

**Returns**: `Promise<KintoAccountInfo>`

#### sendTransaction(txs: TxCall[]): Promise<void>

Sends transactions through the Kinto Wallet.

- `txs`: An array of transaction objects.

**Returns**: `Promise<void>`

#### createNewWallet(): Promise<void>

Opens a popup for the user to create a new wallet.

**Returns**: `Promise<void>`

### Types

#### AppMetadata

```javascript
export interface AppMetadata {
  parent: `0x${string}`;
  paymasterBalance: number;
  tokenId: number;
  dsaEnabled: boolean;
  rateLimitPeriod: number;
  rateLimitNumber: number;
  gasLimitPeriod: number;
  gasLimitCost: number;
  name: string;
  devEOAs: string[];
  appContracts: string[];
}
```

#### KintoAccountInfo

```javascript
export interface KintoAccountInfo {
  exists: boolean;
  approval?: boolean;
  walletAddress?: `0x${string}`;
  app: AppMetadata;
  appKey?: `0x${string}`;
}
```

#### TxCall

```javascript
export interface TxCall {
  to: `0x${string}`;
  data: `0x${string}`;
  value: bigint;
}
```

## Contributing

Contributions are welcome! Please open an issue or submit a pull request on [GitHub](https://github.com/your-repo/my-kinto-sdk).

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

For more information about Kinto, visit [docs.kinto.xyz](https://docs.kinto.xyz).