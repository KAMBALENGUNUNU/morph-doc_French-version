[**@morph-l2/sdk**](../globals.md) • **Docs**

***

[@morph-l2/sdk](../globals.md) / estimateTotalGasCost

# Fonction : estimateTotalGasCost()

> **estimateTotalGasCost**(`l2Provider`, `tx`) : `Promise`\<`BigNumber`\>

Estime le coût total en gaz pour une transaction L2 donnée en wei.

## Paramètres

• **l2Provider** : [`ProviderLike`](../type-aliases/ProviderLike.md)

Fournisseur L2 pour interroger l'utilisation du gaz.

• **tx** : `TransactionRequest`

Transaction pour laquelle estimer le coût total en gaz.

## Renvoie

`Promise`\<`BigNumber`\>

Coût total en gaz estimé.

## Source

src/l2-provider.ts:136
