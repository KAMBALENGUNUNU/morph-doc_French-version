[**@morph-l2/sdk**](../globals.md) • **Docs**

***

[@morph-l2/sdk](../globals.md) / L2Transaction

# Interface : L2Transaction

Représentation JSON d'une transaction lorsqu'elle est retournée par les nœuds L2Geth. C'est simplement une extension au type de réponse standard pour les transactions. Vous n'avez PAS besoin d'utiliser ce type, sauf si vous souhaitez avoir un accès typé aux champs spécifiques à L2.

## Étend

- `TransactionResponse`

## Propriétés

### accessList?

> `optionnel` **accessList** : `AccessList`

#### Hérité de

`TransactionResponse.accessList`

#### Source

node_modules/@ethersproject/transactions/lib/index.d.ts:40

***

### blockHash?

> `optionnel` **blockHash** : `string`

#### Hérité de

`TransactionResponse.blockHash`

#### Source

node_modules/@ethersproject/abstract-provider/lib/index.d.ts:26

***

### blockNumber?

> `optionnel` **blockNumber** : `number`

#### Hérité de

`TransactionResponse.blockNumber`

#### Source

node_modules/@ethersproject/abstract-provider/lib/index.d.ts:25

***

### chainId

> **chainId** : `number`

#### Hérité de

`TransactionResponse.chainId`

#### Source

node_modules/@ethersproject/transactions/lib/index.d.ts:35

***

### confirmations

> **confirmations** : `number`

#### Hérité de

`TransactionResponse.confirmations`

#### Source

node_modules/@ethersproject/abstract-provider/lib/index.d.ts:28

***

### data

> **data** : `string`

#### Hérité de

`TransactionResponse.data`

#### Source

node_modules/@ethersproject/transactions/lib/index.d.ts:33

***

### from

> **from** : `string`

#### Hérité de

`TransactionResponse.from`

#### Source

node_modules/@ethersproject/abstract-provider/lib/index.d.ts:29

***

### gasLimit

> **gasLimit** : `BigNumber`

#### Hérité de

`TransactionResponse.gasLimit`

#### Source

node_modules/@ethersproject/transactions/lib/index.d.ts:31

***

### gasPrice?

> `optionnel` **gasPrice** : `BigNumber`

#### Hérité de

`TransactionResponse.gasPrice`

#### Source

node_modules/@ethersproject/transactions/lib/index.d.ts:32

***
### hash

> **hash** : `string`

#### Hérité de

`TransactionResponse.hash`

#### Source

node_modules/@ethersproject/abstract-provider/lib/index.d.ts:24

***

### l1BlockNumber

> **l1BlockNumber** : `number`

#### Source

src/interfaces/l2-provider.ts:16

***

### l1TxOrigin

> **l1TxOrigin** : `string`

#### Source

src/interfaces/l2-provider.ts:17

***

### maxFeePerGas?

> `optionnel` **maxFeePerGas** : `BigNumber`

#### Hérité de

`TransactionResponse.maxFeePerGas`

#### Source

node_modules/@ethersproject/transactions/lib/index.d.ts:42

***

### maxPriorityFeePerGas?

> `optionnel` **maxPriorityFeePerGas** : `BigNumber`

#### Hérité de

`TransactionResponse.maxPriorityFeePerGas`

#### Source

node_modules/@ethersproject/transactions/lib/index.d.ts:41

***

### nonce

> **nonce** : `number`

#### Hérité de

`TransactionResponse.nonce`

#### Source

node_modules/@ethersproject/transactions/lib/index.d.ts:30

***

### queueOrigin

> **queueOrigin** : `string`

#### Source

src/interfaces/l2-provider.ts:18

***

### r?

> `optionnel` **r** : `string`

#### Hérité de

`TransactionResponse.r`

#### Source

node_modules/@ethersproject/transactions/lib/index.d.ts:36

***

### raw?

> `optionnel` **raw** : `string`

#### Hérité de

`TransactionResponse.raw`

#### Source

node_modules/@ethersproject/abstract-provider/lib/index.d.ts:30

***

### rawTransaction

> **rawTransaction** : `string`

#### Source

src/interfaces/l2-provider.ts:19

***

### s?

> `optionnel` **s** : `string`

#### Hérité de

`TransactionResponse.s`

#### Source

node_modules/@ethersproject/transactions/lib/index.d.ts:37

***

### timestamp?

> `optionnel` **timestamp** : `number`

#### Hérité de

`TransactionResponse.timestamp`

#### Source

node_modules/@ethersproject/abstract-provider/lib/index.d.ts:27

***

### to?

> `optionnel` **to** : `string`

#### Hérité de

`TransactionResponse.to`

#### Source

node_modules/@ethersproject/transactions/lib/index.d.ts:28

***

### type?

> `optionnel` **type** : `number`

#### Hérité de

`TransactionResponse.type`

#### Source

node_modules/@ethersproject/transactions/lib/index.d.ts:39

***

### v?

> `optionnel` **v** : `number`

#### Hérité de

`TransactionResponse.v`

#### Source

node_modules/@ethersproject/transactions/lib/index.d.ts:38

***

### value

> **value** : `BigNumber`

#### Hérité de

`TransactionResponse.value`

#### Source

node_modules/@ethersproject/transactions/lib/index.d.ts:34

***

### wait()

> **wait** : (`confirmations`?) => `Promise`\<`TransactionReceipt`\>

#### Paramètres

• **confirmations?** : `number`

#### Retourne

`Promise`\<`TransactionReceipt`\>

#### Hérité de

`TransactionResponse.wait`

#### Source

node_modules/@ethersproject/abstract-provider/lib/index.d.ts:31
