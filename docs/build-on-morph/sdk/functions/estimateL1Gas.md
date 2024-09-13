[**@morph-l2/sdk**](../globals.md) • **Docs**

***

[@morph-l2/sdk](../globals.md) / estimateL1Gas

# Fonction : estimateL1Gas()

> **estimateL1Gas**(`l2Provider`, `tx`) : `Promise`\<`BigNumber`\>

Estime la quantité de gaz L1 requise pour une transaction L2 donnée.

## Paramètres

• **l2Provider** : [`ProviderLike`](../type-aliases/ProviderLike.md)

Fournisseur L2 pour interroger l'utilisation du gaz.

• **tx** : `TransactionRequest`

Transaction pour laquelle estimer le gaz L1.

## Renvoie

`Promise`\<`BigNumber`\>

Gaz L1 estimé.

## Source

src/l2-provider.ts:71
