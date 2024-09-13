[**@morph-l2/sdk**](../globals.md) • **Docs**

***

[@morph-l2/sdk](../globals.md) / L2BlockWithTransactions

# Interface : L2BlockWithTransactions

Représentation JSON d'un bloc lorsqu'il est retourné par les nœuds L2Geth. C'est un bloc normal, mais avec
des objets L2Transaction au lieu de l'objet de réponse standard pour les transactions.

## Étend

- `BlockWithTransactions`

## Propriétés

### \_difficulty

> **\_difficulty** : `BigNumber`

#### Hérité de

`BlockWithTransactions._difficulty`

#### Source

node_modules/@ethersproject/abstract-provider/lib/index.d.ts:41

***

### baseFeePerGas?

> `optionnel` **baseFeePerGas** : `BigNumber`

#### Hérité de

`BlockWithTransactions.baseFeePerGas`

#### Source

node_modules/@ethersproject/abstract-provider/lib/index.d.ts:46

***

### difficulty

> **difficulty** : `number`

#### Hérité de

`BlockWithTransactions.difficulty`

#### Source

node_modules/@ethersproject/abstract-provider/lib/index.d.ts:40

***

### extraData

> **extraData** : `string`

#### Hérité de

`BlockWithTransactions.extraData`

#### Source

node_modules/@ethersproject/abstract-provider/lib/index.d.ts:45

***

### gasLimit

> **gasLimit** : `BigNumber`

#### Hérité de

`BlockWithTransactions.gasLimit`

#### Source

node_modules/@ethersproject/abstract-provider/lib/index.d.ts:42

***

### gasUsed

> **gasUsed** : `BigNumber`

#### Hérité de

`BlockWithTransactions.gasUsed`

#### Source

node_modules/@ethersproject/abstract-provider/lib/index.d.ts:43

***

### hash

> **hash** : `string`

#### Hérité de

`BlockWithTransactions.hash`

#### Source

node_modules/@ethersproject/abstract-provider/lib/index.d.ts:35

***

### miner

> **miner** : `string`

#### Hérité de

`BlockWithTransactions.miner`

#### Source

node_modules/@ethersproject/abstract-provider/lib/index.d.ts:44

***

### nonce

> **nonce** : `string`

#### Hérité de

`BlockWithTransactions.nonce`

#### Source

node_modules/@ethersproject/abstract-provider/lib/index.d.ts:39

***

### number

> **number** : `number`

#### Hérité de

`BlockWithTransactions.number`

#### Source

node_modules/@ethersproject/abstract-provider/lib/index.d.ts:37

***

### parentHash

> **parentHash** : `string`

#### Hérité de

`BlockWithTransactions.parentHash`

#### Source

node_modules/@ethersproject/abstract-provider/lib/index.d.ts:36

***

### stateRoot

> **stateRoot** : `string`

#### Source

src/interfaces/l2-provider.ts:35

***

### timestamp

> **timestamp** : `number`

#### Hérité de

`BlockWithTransactions.timestamp`

#### Source

node_modules/@ethersproject/abstract-provider/lib/index.d.ts:38

***

### transactions

> **transactions** : [[`L2Transaction`](L2Transaction.md)]

#### Remplace

`BlockWithTransactions.transactions`

#### Source

src/interfaces/l2-provider.ts:36
