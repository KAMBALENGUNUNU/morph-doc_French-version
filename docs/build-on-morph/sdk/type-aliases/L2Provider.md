[**@morph-l2/sdk**](../globals.md) • **Docs**

***

[@morph-l2/sdk](../globals.md) / L2Provider

# Alias de type : L2Provider\<TProvider\>

> **L2Provider**\<`TProvider`\>: `TProvider` & `object`

Représente une version étendue d'un fournisseur ethers normal qui retourne des informations supplémentaires sur L2 et
dispose de fonctions spéciales pour les interactions spécifiques à L2.

## Déclaration de type

### \_isL2Provider

> **\_isL2Provider**: `true`

Propriété interne pour déterminer si un fournisseur est un L2Provider.
Vous cherchez probablement la fonction isL2Provider.

### estimateL1Gas()

Estime le gaz L1 (données) requis pour une transaction.

#### Paramètres

• **tx**: `TransactionRequest`

Transaction pour laquelle estimer le gaz L1.

#### Renvoie

`Promise`\<`BigNumber`\>

Gaz L1 estimé.

### estimateL1GasCost()

Estime le coût du gaz L1 (données) pour une transaction en wei en multipliant le coût estimé du gaz L1
par le prix du gaz L1 actuel.

#### Paramètres

• **tx**: `TransactionRequest`

Transaction pour laquelle estimer le coût du gaz L1.

#### Renvoie

`Promise`\<`BigNumber`\>

Coût estimé du gaz L1.

### estimateL2GasCost()

Estime le coût du gaz L2 (exécution) pour une transaction en wei en multipliant le coût estimé du gaz L1
par le prix du gaz L2 actuel. C'est une simple multiplication du résultat de
getGasPrice et estimateGas pour la demande de transaction donnée.

#### Paramètres

• **tx**: `TransactionRequest`

Transaction pour laquelle estimer le coût du gaz L2.

#### Renvoie

`Promise`\<`BigNumber`\>

Coût estimé du gaz L2.

### estimateTotalGasCost()

Estime le coût total du gaz pour une transaction en wei en ajoutant le coût estimé du gaz L1
et le coût estimé du gaz L2.

#### Paramètres

• **tx**: `TransactionRequest`

Transaction pour laquelle estimer le coût total du gaz.

#### Renvoie

`Promise`\<`BigNumber`\>

Coût total estimé du gaz.

### getL1GasPrice()

Obtient le prix actuel du gaz L1 (données).

#### Renvoie

`Promise`\<`BigNumber`\>

Prix actuel du gaz de données L1 en wei.

## Paramètres de type

• **TProvider** *étend* `Provider`

## Source

src/interfaces/l2-provider.ts:43
