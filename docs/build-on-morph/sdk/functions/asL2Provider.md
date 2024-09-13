[**@morph-l2/sdk**](../globals.md) • **Docs**

***

[@morph-l2/sdk](../globals.md) / asL2Provider

# Fonction : asL2Provider()

> **asL2Provider**\<`TProvider`\>(`provider`) : [`L2Provider`](../type-aliases/L2Provider.md)\<`TProvider`\>

Renvoie un fournisseur enveloppé en tant que fournisseur Morph L2. Ajoute quelques fonctions d'aide supplémentaires pour
simplifier le processus d'estimation de l'utilisation du gaz pour une transaction sur Morph. Renvoie une COPIE
du fournisseur original.

## Paramètres de type

• **TProvider** *s'étend* `Provider`\<`TProvider`\>

## Paramètres

• **provider** : `TProvider`

Fournisseur à envelopper en tant que fournisseur L2.

## Renvoie

[`L2Provider`](../type-aliases/L2Provider.md)\<`TProvider`\>

Fournisseur enveloppé en tant que fournisseur L2.

## Source

src/l2-provider.ts:171
