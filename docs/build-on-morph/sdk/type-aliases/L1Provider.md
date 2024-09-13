[**@morph-l2/sdk**](../globals.md) • **Docs**

***

[@morph-l2/sdk](../globals.md) / L1Provider

# Alias de type : L1Provider\<TProvider\>

> **L1Provider**\<`TProvider`\>: `TProvider` & `object`

Représente une version étendue d'un fournisseur ethers normal qui retourne des informations supplémentaires sur L1 et
dispose de fonctions spéciales pour les interactions spécifiques à L1.

## Déclaration de type

### \_isL1Provider

> **\_isL1Provider**: `true`

Propriété interne pour déterminer si un fournisseur est un L1Provider.
Vous cherchez probablement la fonction isL2Provider.

### estimateCrossDomainMessageFee()

Obtient le prix du gaz L1 (données) actuel.

#### Paramètres

• **l1Provider**: [`ProviderLike`](ProviderLike.md)

• **sender**: `string`

• **gasLimit**: `number` \| `bigint` \| `BigNumber`

#### Renvoie

`Promise`\<`BigNumber`\>

Prix du gaz de données L1 actuel en wei.

## Paramètres de type

• **TProvider** *étend* `Provider`

## Source

src/interfaces/l1-provider.ts:11
