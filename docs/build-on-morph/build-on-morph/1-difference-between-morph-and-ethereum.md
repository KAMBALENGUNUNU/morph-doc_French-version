---
title: Différence entre Morph et Ethereum
lang: fr-FR
keywords: [morph, ethereum, rollup, layer2, preuve de validité, zk-rollup optimiste]
description: Améliorez votre expérience blockchain avec Morph - la solution de zk-rollup optimiste sécurisée, décentralisée, rentable et performante. Essayez-la maintenant !
---

Il existe plusieurs différences techniques entre l'EVM d'Ethereum et le zkEVM optimiste de Morph.

Nous avons compilé une liste pour vous aider à mieux comprendre ces distinctions.


:::tip
Pour la plupart des développeurs Solidity, ces détails techniques n'affecteront pas beaucoup votre expérience de développement.
:::

## Opcodes de l'EVM


| Opcode                      | Équivalent Solidity  | Comportement de Morph                                                                                   |
| --------------------------- | ------------------- | -------------------------------------------------------------------------------------------------------- |
| `BLOCKHASH`                 | `block.blockhash`   | Retourne `keccak(chain_id \|\| block_number)` pour les 256 derniers blocs.                            |
| `COINBASE`                  | `block.coinbase`    | Retourne l'adresse du contrat de coffre de frais pré-déployé. Voir [Contrats](../../build-on-morph/developer-resources/1-contracts.md) |
| `DIFFICULTY` / `PREVRANDAO` | `block.difficulty`  | Retourne 0.                                                                                            |
| `BASEFEE`                   | `block.basefee`     | Désactivé. Si l'opcode est rencontré, la transaction sera annulée.                                   |
| `SELFDESTRUCT`              | `selfdestruct`      | Désactivé. Si l'opcode est rencontré, la transaction sera annulée.                                   |

## Précompilations de l'EVM

Les précompilations `RIPEMD-160` (adresse `0x3`), `blake2f` (adresse `0x9`), et `évaluation de point` (adresse `0x0a`) ne sont actuellement pas prises en charge. Les appels aux contrats précompilés non pris en charge seront annulés. Nous prévoyons d'activer ces précompilations dans les futures mises à jour majeures.

La précompilation `modexp` est prise en charge mais ne prend en charge que des entrées de taille inférieure ou égale à 32 octets (c'est-à-dire `u256`).

La précompilation `ecPairing` est prise en charge, mais le nombre de points (ensembles, paires) est limité à 4, au lieu de 6.

Les autres précompilations de l'EVM sont toutes prises en charge : `ecRecover`, `identity`, `ecAdd`, `ecMul`.

### Limites de précompilation

En raison de la taille limitée des circuits zkEVM, il y a une limite supérieure sur le nombre d'appels qui peuvent être effectués pour certaines précompilations. Ces transactions ne seront pas annulées, mais simplement ignorées par le séquenceur si elles ne peuvent pas tenir dans l'espace du circuit.

| Précompilation / Opcode | Limite | 
| ----------------------- | ------ |
| `keccak256`            | 3157   |
| `ecRecover`            | 119    |
| `modexp`               | 23     |
| `ecAdd`                | 50     |
| `ecMul`                | 50     |
| `ecPairing`            | 2      |

:::tip OpCode de la mise à niveau Dencun non disponible

Les opcodes de la mise à niveau Dencun ne sont pas encore disponibles sur Morph, y compris `MCOPY`, `TSTORE`, `TLOAD`, `BLOBHASH` et `BLOBBASEFEE`. De plus, [EIP-4788](https://eips.ethereum.org/EIPS/eip-4788) pour accéder à la racine de bloc de la Beacon Chain n'est pas pris en charge. Nous recommandons d'utiliser `shanghai` comme votre cible EVM et d'éviter d'utiliser une version de Solidity supérieure à `0.8.23`.

:::

## Compte d'État

### **Champs supplémentaires**

Nous avons ajouté deux champs dans l'objet `StateAccount` actuel : `PoseidonCodehash` et `CodeSize`.

```go
type StateAccount struct {
	Nonce    uint64
	Balance  *big.Int
	Root     common.Hash // racine Merkle du trie de stockage
	KeccakCodeHash []byte // toujours le Keccak codehash
	// champs ajoutés
	PoseidonCodeHash []byte // le codehash Poseidon
	CodeSize uint64
}
```
### **CodeHash**

En rapport avec cela, nous maintenons deux types de codehash pour chaque bytecode de contrat : le hachage Keccak et le hachage Poseidon.

`KeccakCodeHash` est conservé pour maintenir la compatibilité avec `EXTCODEHASH`. `PoseidonCodeHash` est utilisé pour vérifier l'exactitude des bytecodes chargés dans le zkEVM, où le hachage Poseidon est beaucoup plus efficace.

### CodeSize

Lors de la vérification de `EXTCODESIZE`, il est coûteux de charger toutes les données du contrat dans le zkEVM. Au lieu de cela, nous stockons la taille du contrat dans le stockage lors de la création du contrat. De cette façon, nous n'avons pas besoin de charger le code — une preuve de stockage est suffisante pour vérifier cet opcode.

## Temps de Bloc

:::tip Temps de Bloc Suje à Changements

Les blocs sont produits chaque seconde, avec un bloc vide généré s'il n'y a pas de transactions pendant 5 secondes. Cependant, cette fréquence peut changer à l'avenir.
:::

Pour comparaison, Ethereum a un temps de bloc d'environ 12 secondes.

Raisons d'un Temps de Bloc Plus Rapide dans Morph
Expérience Utilisateur :

- Un temps de bloc plus rapide et constant fournit un retour d'information plus rapide, améliorant l'expérience utilisateur.

- Optimisation : À mesure que nous affinons les circuits zkEVM dans nos testnets, nous pouvons atteindre un débit plus élevé qu'Ethereum, même avec une limite de gaz par bloc ou par lot plus petite.

Avis :
- `TIMESTAMP` retournera le timestamp du bloc. Il sera mis à jour chaque seconde.
- `BLOCKNUMBER` retournera un numéro de bloc réel. Il sera mis à jour chaque seconde. La correspondance un à un entre les blocs et les transactions ne s'appliquera plus.

## Futures EIPs

Morph surveille de près les propositions d'amélioration d'Ethereum (EIPs) émergentes et les adopte lorsqu'elles sont appropriées. Pour plus de détails, rejoignez notre forum communautaire ou notre Discord pour des discussions.

## [Frais de Transaction](../../build-on-morph/build-on-morph/4-understand-transaction-cost-on-morph.md)
