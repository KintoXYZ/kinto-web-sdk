# Kinto SDK

Kinto SDK is a JavaScript library that allows applications to connect to the Kinto Wallet. Kinto is an Ethereum Layer 2 (L2) solution designed to provide fast and cost-efficient transactions. This SDK provides methods to connect a Kinto Wallet, send transactions, and create new wallets.

## Table of Contents

- [Installation](#installation)
- [Usage](#usage)
  - [Initialization](#initialization)
  - [Connecting to Kinto Wallet](#connecting-to-kinto-wallet)
  - [Sending Transactions](#sending-transactions)
  - [Creating a New Wallet](#creating-a-new-wallet)
- [API](#api)
  - [KintoSDK](#kintosdk)
    - [connect()](#connect)
    - [sendTransaction()](#sendtransaction)
    - [createNewWallet()](#createnewwallet)
- [Contributing](#contributing)
- [License](#license)

## Installation

You can install the Kinto SDK via npm:

```bash
npm install my-kinto-sdk
```

## Usage

### Initialization

To use the Kinto SDK, you need to initialize it with your application's address.

```javascript
import { createKintoSDK } from 'my-kinto-sdk';

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

## Contributing

Contributions are welcome! Please open an issue or submit a pull request on [GitHub](https://github.com/your-repo/my-kinto-sdk).

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

For more information about Kinto, visit [docs.kinto.xyz](https://docs.kinto.xyz).