# Utexo SDK

This is the underlying SDK used by RGB client applications. It provides a complete set of bindings for interacting with the **RGB** and managing **RGB**-based transfers.

With this SDK, developers can:

* Generate RGB invoices
* Create and manage UTXOs
* Sign PSBTs using local private keys or hardware signing flows
* Fetch asset balances, transfer status, and other RGB-related state

## Capabilities of `@utexo/rgb-sdk` (via `WalletManager`)

The primary wallet class is **`UTEXOWallet`**: initialize with a mnemonic (or seed) and optional `{ network, dataDir }`, then call `await wallet.initialize()` before use. It combines standard RGB operations with UTEXO features (Lightning, on-chain deposit/withdrawal).

| Method / Function                                                           | Description                                                                                       |
| --------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| `generateKeys(network?)`                                                    | Generate new wallet keys (mnemonic, xpubs, master fingerprint) – top-level function               |
| `restoreUtxoWalletFromBackup({ backupPath, password, targetDir })`          | Restore UTEXO wallet from file backup (layer1 + utexo) – top-level function                       |
| `restoreUtxoWalletFromVss({ mnemonic, targetDir, config?, vssServerUrl? })` | Restore UTEXO wallet from VSS cloud backup – top-level function                                   |
| `deriveKeysFromMnemonic(network, mnemonic)`                                 | Derive wallet keys from existing mnemonic                                                         |
| `deriveKeysFromSeed(network, seed)`                                         | Derive wallet keys from BIP39 seed                                                                |
| `getAddress()`                                                              | Get deposit address (async)                                                                       |
| `getBtcBalance()`                                                           | Get on-chain BTC balance (async)                                                                  |
| `getXpub()`                                                                 | Get vanilla and colored xpubs                                                                     |
| `getNetwork()`                                                              | Get current network                                                                               |
| `listUnspents()`                                                            | List unspent UTXOs                                                                                |
| `listAssets()`                                                              | List RGB assets held                                                                              |
| `getAssetBalance(assetId)`                                                  | Get balance for a specific asset                                                                  |
| `createUtxos({ num?, size?, upTo? })`                                       | Create UTXOs (async; combines begin, sign, end; feeRate defaults to 1)                            |
| `createUtxosBegin({ upTo?, num?, size? })`                                  | Start creating UTXOs (returns unsigned PSBT)                                                      |
| `createUtxosEnd({ signedPsbt, skipSync? })`                                 | Finalize UTXO creation with signed PSBT                                                           |
| `blindReceive({ assetId, amount, minConfirmations?, durationSeconds? })`    | Generate blinded UTXO for receiving                                                               |
| `witnessReceive({ assetId, amount, minConfirmations?, durationSeconds? })`  | Generate witness UTXO for receiving                                                               |
| `issueAssetNia({ ticker, name, amounts, precision })`                       | Issue a new Non-Inflationary Asset                                                                |
| `send({ invoice, assetId, amount, witnessData? })`                          | Complete send (begin → sign → end; use `witnessData` for witness invoices; feeRate defaults to 1) |
| `sendBegin({ invoice, assetId, amount, witnessData?, ... })`                | Prepare transfer (returns unsigned PSBT)                                                          |
| `sendEnd({ signedPsbt, skipSync? })`                                        | Complete transfer with signed PSBT                                                                |
| `signPsbt(psbt, mnemonic?)`                                                 | Sign PSBT using wallet mnemonic (async)                                                           |
| `refreshWallet()`                                                           | Sync and refresh wallet state                                                                     |
| `syncWallet()`                                                              | Trigger wallet sync                                                                               |
| `listTransactions()`                                                        | List BTC-level transactions                                                                       |
| `listTransfers(assetId?)`                                                   | List RGB transfer history for asset                                                               |
| `failTransfers(params)`                                                     | Mark waiting transfers as failed                                                                  |
| `createBackup({ backupPath, password })`                                    | Create encrypted backup (layer1 + utexo in one folder)                                            |
| `vssBackup(config?, mnemonic?)`                                             | Backup to VSS (config optional; built from mnemonic + default server URL)                         |
| `vssBackupInfo(config?, mnemonic?)`                                         | Get VSS backup info                                                                               |
| _On-chain_                                                                  |                                                                                                   |
| `onchainReceive(params)`                                                    | Generate invoice for depositing from mainnet to UTEXO                                             |
| `onchainSendBegin(params)`                                                  | Start on-chain withdraw (returns unsigned PSBT)                                                   |
| `onchainSendEnd(params)`                                                    | Finalize on-chain withdraw with signed PSBT                                                       |
| `onchainSend(params, mnemonic?)`                                            | Complete on-chain withdraw (begin → sign → end)                                                   |
| `getOnchainSendStatus(invoice)`                                             | Get status of on-chain withdraw                                                                   |
| _Lightning_                                                                 |                                                                                                   |
| `createLightningInvoice(params)`                                            | Create Lightning invoice for receiving                                                            |
| `payLightningInvoiceBegin(params)`                                          | Start Lightning payment (returns unsigned PSBT)                                                   |
| `payLightningInvoiceEnd(params)`                                            | Finalize Lightning payment with signed PSBT                                                       |
| `payLightningInvoice(params, mnemonic?)`                                    | Complete Lightning payment (begin → sign → end)                                                   |
| `getLightningSendRequest(lnInvoice)`                                        | Get status of Lightning send                                                                      |
| `getLightningReceiveRequest(lnInvoice)`                                     | Get status of Lightning receive                                                                   |
| `listLightningPayments()`                                                   | List Lightning payments                                                                           |

By using this SDK, developers have full control over:

* Transfer orchestration
* UTXO selection
* Invoice lifecycle
* Signing policy

This pattern enables advanced use cases, such as:

* Integrating with third-party identity/auth layers
* Applying custom fee logic or batching
* Implementing compliance and audit tracking

## Getting Started

#### Prerequisites

This SDK uses `rgb-protocol libraries`. All operations are performed locally.

#### Default Endpoints

The SDK uses default endpoints for RGB transport and Bitcoin indexing. These are automatically used if not specified:

**Transport Endpoints** (RGB protocol communication):

* **Mainnet**: `rpcs://rgb-proxy-mainnet.utexo.com/json-rpc`
* **Testnet**: `rpcs://rgb-proxy-testnet3.utexo.com/json-rpc`
* **Testnet4**: `rpcs://proxy.iriswallet.com/0.2/json-rpc`
* **Signet**: `rpcs://rgb-proxy-utexo.utexo.com/json-rpc`
* **Regtest**: `rpcs://proxy.iriswallet.com/0.2/json-rpc`

**Indexer URLs** (Bitcoin blockchain data):

* **Mainnet**: `ssl://electrum.iriswallet.com:50003`
* **Testnet**: `ssl://electrum.iriswallet.com:50013`
* **Testnet4**: `ssl://electrum.iriswallet.com:50053`
* **Signet**: `https://esplora-api.utexo.com`
* **Regtest**: `tcp://regtest.thunderstack.org:50001`

UTEXOWallet uses network (`testnet` / `mainnet`) that define indexer and transport endpoints internally.

### Installation

```bash
npm install @utexo/rgb-sdk
```

#### Node.js only

This SDK is designed for **Node.js** and is not browser-compatible. Use it in Node.js applications, scripts, and backends.<br>

## Basic Usage

{% stepper %}
{% step %}
### Generate wallet keys

```javascript
const { UTEXOWallet, generateKeys } = require('@utexo/rgb-sdk');

// 1. Generate wallet keys (async)
const keys = await generateKeys('testnet');
console.log('Mnemonic:', keys.mnemonic); // Store securely!
```
{% endstep %}

{% step %}
### Initialize wallet

```javascript
const wallet = new UTEXOWallet(keys.mnemonic, { network: 'testnet' });
await wallet.initialize();
```
{% endstep %}

{% step %}
### Get a derived deposit address

```javascript
const address = await wallet.getAddress();
console.log('Wallet address:', address);
```
{% endstep %}

{% step %}
### Check balance

<pre class="language-javascript"><code class="lang-javascript">const balance = await wallet.getBtcBalance();
<a data-footnote-ref href="#user-content-fn-1">console.log('BTC Balance:', balance);</a>
</code></pre>
{% endstep %}
{% endstepper %}

## Core Workflows

### Wallet Initialization

{% stepper %}
{% step %}
### Generate keys and initialize

```javascript
const { UTEXOWallet, generateKeys, restoreUtxoWalletFromBackup, restoreUtxoWalletFromVss } = require('@utexo/rgb-sdk');

// Generate new wallet keys (async)
const keys = await generateKeys('testnet');

// Initialize UTEXO wallet with mnemonic
const wallet = new UTEXOWallet(keys.mnemonic, { network: 'testnet' });
await wallet.initialize();

// Optional: use dataDir for persistent storage (same layout as restore)
const walletWithDir = new UTEXOWallet(keys.mnemonic, { network: 'testnet', dataDir: './wallet-data' });
await walletWithDir.initialize();

```
{% endstep %}

{% step %}
### Restore from mnemonic

<pre class="language-javascript"><code class="lang-javascript"><strong>// Restore from file backup (layer1 + lightning in one folder)
</strong>const { targetDir } = restoreUtxoWalletFromBackup({
    backupPath: './backup-folder',
    password: 'your-password',
    targetDir: './restored-wallet',
});
const restoredWallet = new UTEXOWallet(keys.mnemonic, { dataDir: targetDir, network: 'testnet' });
await restoredWallet.initialize();

// Restore from VSS (mnemonic required; vssServerUrl optional, uses default)
const { targetDir: vssDir } = await restoreUtxoWalletFromVss({
    mnemonic: keys.mnemonic,
    targetDir: './restored-from-vss',
});
const fromVss = new UTEXOWallet(keys.mnemonic, { dataDir: vssDir, network: 'testnet' });
await fromVss.initialize();
</code></pre>
{% endstep %}
{% endstepper %}

### UTXO Management

{% stepper %}
{% step %}
### Begin UTXO creation

```javascript
// Option 1: Create UTXOs in one call (begin → sign → end)
const count = await wallet.createUtxos({ num: 5, size: 1000 });
await wallet.syncWallet();
console.log(`Created ${count} UTXOs`);
```
{% endstep %}

{% step %}
### Sign PSBT

```javascript
const psbt = await wallet.createUtxosBegin({ num: 5, size: 1000 });
const signedPsbt = await wallet.signPsbt(psbt);
```
{% endstep %}

{% step %}
### Finalize UTXO creation

```javascript
const utxosCreated = await wallet.createUtxosEnd({ signedPsbt });
await wallet.syncWallet();
console.log(`Created ${utxosCreated} UTXOs`);
```
{% endstep %}
{% endstepper %}

### Asset Issuance

```javascript
// Issue a new NIA
const asset = await wallet.issueAssetNia({
    ticker: "USD Token",
    name: "USDT",
    amounts: [1000, 500],
    precision: 6
});

console.log('Asset issued:', asset.asset?.assetId);
```

### Asset Transfers

{% stepper %}
{% step %}
### Create blind receive (receiver)

```javascript
// Receiver: create blind or witness invoice
const receiveData = receiverWallet.blindReceive({
    assetId: assetId,
    amount: 100,
    minConfirmations: 3,
    durationSeconds: 2000
});
// For witness invoices, sender must pass witnessData when sending
const witnessData = await receiverWallet.witnessReceive({ assetId, amount: 50 });
```
{% endstep %}

{% step %}
### Begin transfer (sender builds PSBT)

```javascript
// Sender: Option 2 – begin/end flow for custom signing
const sendPsbt = await senderWallet.sendBegin({
    invoice: receiveData.invoice,
    assetId,
    amount: 100
});
```
{% endstep %}

{% step %}
### Sign the PSBT

```javascript
const signedSendPsbt = await senderWallet.signPsbt(sendPsbt);
```
{% endstep %}

{% step %}
### Finalize transfer

```javascript
await senderWallet.sendEnd({ signedPsbt: signedSendPsbt });
```
{% endstep %}

{% step %}
### Alternative: Complete send in one call

```javascript
// For witness invoice:
await senderWallet.send({
    invoice: witnessData.invoice,
    assetId,
    amount: 50,
    witnessData: { amountSat: 1000 }
});
```
{% endstep %}

{% step %}
### Refresh wallets to sync transfer

```javascript
// Refresh both wallets and list transfers
await senderWallet.refreshWallet();
await receiverWallet.refreshWallet();
const transfers = await receiverWallet.listTransfers(assetId);
```
{% endstep %}
{% endstepper %}

### Balance and Asset Management

```javascript
// Get BTC balance (async)
const btcBalance = await wallet.getBtcBalance();

// List all assets
const assets = await wallet.listAssets();

// Get specific asset balance
const assetBalance = await wallet.getAssetBalance(assetId);

// List unspent UTXOs
const unspents = await wallet.listUnspents();

// List transactions
const transactions = await wallet.listTransactions();

// List transfers for specific asset
const transfers = await wallet.listTransfers(assetId);
```

## Setup wallet and issue asset

{% stepper %}
{% step %}
### Generate and initialize wallet

```javascript
const { UTEXOWallet, generateKeys } = require('@utexo/rgb-sdk');

async function demo() {
    const keys = await generateKeys('testnet');
    const wallet = new UTEXOWallet(keys.mnemonic, { network: 'testnet' });
    await wallet.initialize();

    const address = await wallet.getAddress();
    const balance = await wallet.getBtcBalance();

    // Create UTXOs and issue asset
    const count = await wallet.createUtxos({ num: 5, size: 1000 });
    await wallet.syncWallet();

    const asset = await wallet.issueAssetNia({
        ticker: 'DEMO',
        name: 'Demo Token',
        amounts: [1000],
        precision: 2
    });

    const assets = await wallet.listAssets();
    const assetBalance = await wallet.getAssetBalance(asset.assetId);

    await wallet.dispose();
}
```
{% endstep %}
{% endstepper %}

## Security

### Key Management

```javascript
const { generateKeys, deriveKeysFromMnemonic } = require('@utexo/rgb-sdk');

// Generate new wallet keys (async)
const keys = await generateKeys('testnet');
const mnemonic = keys.mnemonic; // Sensitive - protect at rest

// Store mnemonic securely for later restoration
// Use environment variables for production
const storedMnemonic = process.env.WALLET_MNEMONIC;

// Restore keys from mnemonic
const restoredKeys = await deriveKeysFromMnemonic('testnet', storedMnemonic);

// Sign and verify arbitrary messages (Schnorr signatures)
const seedHex = process.env.WALLET_SEED_HEX; // 64-byte hex string
const { signature, accountXpub } = await signMessage({
  message: 'Hello RGB!',
  seed: seedHex,
  network: 'testnet',
});
const isValid = await verifyMessage({
  message: 'Hello RGB!',
  signature,
  accountXpub,
  network: 'testnet',
});
```

### Full Examples

* [new-wallet](https://github.com/UTEXO-Protocol/rgb-sdk/blob/main/examples/new-wallet.mjs) – Generate keys and create a new UTEXO wallet
* [read-wallet](https://github.com/UTEXO-Protocol/rgb-sdk/blob/main/examples/read-wallet.mjs) – Initialize by mnemonic and call getXpub, getNetwork, getAddress, getBtcBalance, listAssets
* [create-utxos-asset](https://github.com/UTEXO-Protocol/rgb-sdk/blob/main/examples/create-utxos-asset.mjs) – Create UTXOs and issue a NIA asset
* [transfer](https://github.com/UTEXO-Protocol/rgb-sdk/blob/main/examples/transfer.mjs) – Two wallets: witness + blind receive, refresh, listTransfers (requires ASSET\_ID and funded wallets)
* [onchain-flow](https://github.com/UTEXO-Protocol/rgb-sdk/blob/main/examples/onchain-flow.mjs) – On-chain transfer: receive + send
* [lightning-flow](https://github.com/UTEXO-Protocol/rgb-sdk/blob/main/examples/lightning-flow.mjs) – Lightning transfer: createLightningInvoice + payLightningInvoice
* [utexo-vss-backup-restore](https://github.com/UTEXO-Protocol/rgb-sdk/blob/main/examples/utexo-vss-backup-restore.mjs) – VSS backup and restore
* [utexo-file-backup-restore](https://github.com/UTEXO-Protocol/rgb-sdk/blob/main/examples/utexo-file-backup-restore.mjs) – File backup and restore

See [examples/README.md](https://github.com/UTEXO-Protocol/rgb-sdk/blob/main/examples/README.md) for run commands. CLI: [cli/](https://github.com/UTEXO-Protocol/rgb-sdk/blob/main/cli).

[^1]: 
