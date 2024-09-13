[**@morph-l2/sdk**](../globals.md) • **Docs**

***

[@morph-l2/sdk](../globals.md) / isL2Provider

# Fonction : isL2Provider()

> **isL2Provider**\<`TProvider`\>(`provider`) : `provider est L2Provider<TProvider>`

Détermine si un fournisseur donné est un L2Provider. Cela forcera le type
si c'est vrai.

## Paramètres de type

• **TProvider** *étend* `Provider`\<`TProvider`\>

## Paramètres

• **provider** : `TProvider`

Le fournisseur à vérifier.

## Retourne

`provider est L2Provider<TProvider>`

Booléen

## Exemple

```ts
if (isL2Provider(provider)) {
  // typescript sait maintenant qu'il s'agit d'un type L2Provider
  const gasPrice = await provider.estimateL2GasPrice(tx)
}
```

## Source

src/l2-provider.ts:157
