---
description: A class that lets you create and manage Kleros Escrow transactions.
---

# Escrow SDK

This class lets you create and manage Kleros Escrow transactions. Use this Kleros Escrow SDK to easily integrate on-chain escrow features on your platform.

```javascript
import KlerosEscrow from "@kleros/components/kleros-escrow";

//...
```

## Methods

## `constructor`

Constructs a `KlerosEscrow` instance.

### Params `(web3, archon)`

| Name | Type | Description | Default |
| :--- | :--- | :--- | :--- |
| web3\* | `Web3` | A Web3 instance. |  |
| archon | `Archon` | An [Archon](https://archon.readthedocs.io/) instance. | `new Archon(web3.currentProvider, "https://ipfs.kleros.io")` |

### Returns `(KlerosEscrow)`

A `KlerosEscrow` instance.

## `klerosEscrow.getAccount`

### Returns `(Promise<object>)`

A promise for the current account of the set Web3 instance or the one chosen in the prompt to connect when none is set.

## `klerosEscrow.setCourtAndCurrency`

Sets the court and currency that escrow transactions will use.

### Params `(court = "blockchain-non-technical", currency)`

| Name | Type | Description | Default |
| :--- | :--- | :--- | :--- |
| court | `string` | The court that will rule over any disputes arising from a transaction. `"general"` or `"blockchain-non-technical"`, or a custom [arbitrable transaction contract](https://github.com/kleros/escrow-contracts) address. | `"blockchain-non-technical"` |
| currency | `string` | The address of the token the transaction should be paid in. Leave this undefined to use ETH. |  |

### Returns `(Promise)`

A promise that resolves when the court and currency are set.

## `klerosEscrow.upload`

Uploads files to Kleros' IPFS node.

### Params `(fileName, bufferOrJSON)`

| Name | Type | Description | Default |  |  |
| :--- | :--- | :--- | :--- | :--- | :--- |
| fileName\* | `string` | The file name of the file to upload. |  |  |  |
| bufferOrJSON\* | \`string | Buffer | object\` | The file to upload. |  |

### Returns `(Promise<string>)`

A promise for the uploaded's file IPFS URI.

## `klerosEscrow.getTransactions`

Gets the list of transactions an address is involved in.

### Params `(address)`

| Name | Type | Description | Default |
| :--- | :--- | :--- | :--- |
| address | `string` | The address to get transactions for. | `(await web3.eth.getAccounts())[0]` |

### Returns `(Promise<object[]>)`

A promise for the list of transactions.

## `klerosEscrow.isSender`

Checks if the current Web3 account is the sender of a transaction.

### Params `(transactionID)`

| Name | Type | Description | Default |
| :--- | :--- | :--- | :--- |
| transactionID\* | `string` | The ID of the transaction. |  |

### Returns `(Promise<boolean>)`

A promise for the answer.

## `klerosEscrow.createTransaction`

Creates an escrow transaction.

### Params `(amount, recipient, timeout, metaEvidence)`

| Name | Type | Description | Default |  |  |
| :--- | :--- | :--- | :--- | :--- | :--- |
| amount\* | \`number | string | BN\` | The amount escrowed. |  |
| recipient\* | `string` | The address of the recipient. |  |  |  |
| timeout\* | \`number | string | BN\` | The time in seconds until the transaction becomes executable. |  |
| metaEvidence\* | `object` | The [meta evidence object](https://github.com/ethereum/EIPs/issues/1497) for any potential disputes arising. You can add an additional `file` property with a buffer, string, or object, and it will be uploaded to IPFS and `fileURI` will be set appropiately. |  |  |  |

### Returns `(Promise<object>)`

A promise for the transaction's creation transaction.

## `klerosEscrow.pay`

Pays an amount of an escrowed transaction the current account is a sender in, to the recipient.

### Params `(transactionID, amount)`

| Name | Type | Description | Default |  |  |
| :--- | :--- | :--- | :--- | :--- | :--- |
| transactionID\* | `string` | The ID of the transaction. |  |  |  |
| amount\* | \`number | string | BN\` | The amount to pay. |  |

### Returns `(Promise<object>)`

A promise for the payment's transaction.

## `klerosEscrow.reimburse`

Pays an amount of an escrowed transaction the current account is a recipient in, to the sender.

### Params `(transactionID, amount)`

| Name | Type | Description | Default |  |  |
| :--- | :--- | :--- | :--- | :--- | :--- |
| transactionID\* | `string` | The ID of the transaction. |  |  |  |
| amount\* | \`number | string | BN\` | The amount to pay. |  |

### Returns `(Promise<object>)`

A promise for the payment's transaction.

## `klerosEscrow.executeTransaction`

Executes a transaction where the timeout has passed.

### Params `(transactionID)`

| Name | Type | Description | Default |
| :--- | :--- | :--- | :--- |
| transactionID\* | `string` | The ID of the transaction. |  |

### Returns `(Promise<object>)`

A promise for the execution's transaction.

## `klerosEscrow.timeout`

Timesout the other party of an escrowed transaction the current account is involved in. This is for when they miss the deadline to pay arbitration fees.

### Params `(transactionID)`

| Name | Type | Description | Default |
| :--- | :--- | :--- | :--- |
| transactionID\* | `string` | The ID of the transaction. |  |

### Returns `(Promise<object>)`

A promise for the timeout's transaction.

## `klerosEscrow.payArbitrationFee`

Pays arbitration fees for a transaction the current account is involved in.

### Params `(transactionID, amount)`

| Name | Type | Description | Default |  |  |
| :--- | :--- | :--- | :--- | :--- | :--- |
| transactionID\* | `string` | The ID of the transaction. |  |  |  |
| amount\* | \`number | string | BN\` | The amount to pay. |  |

### Returns `(Promise<object>)`

A promise for the payment's transaction.

## `klerosEscrow.submitEvidence`

Uploads evidence to Kleros' IPFS node and submits it for a transaction.

### Params `(transactionID, evidence)`

| Name | Type | Description | Default |
| :--- | :--- | :--- | :--- |
| transactionID\* | `string` | The ID of the transaction. |  |
| evidence\* | `object` | The [evidence object](https://github.com/ethereum/EIPs/issues/1497) for any potential disputes arising. You can add an additional `file` property with a buffer, string, or object, and it will be uploaded to IPFS and `fileURI` will be set appropiately. |  |

### Returns `(Promise<object>)`

A promise for the submission's transaction.

