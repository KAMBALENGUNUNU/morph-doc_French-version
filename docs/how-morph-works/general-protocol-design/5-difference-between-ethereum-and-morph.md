---
title: Différence entre Morph et Ethereum
lang: fr-FR
keywords: [morph,ethereum,rollup,layer2,preuve de validité,optimistic zk-rollup]
description: Améliorez votre expérience blockchain avec Morph - la solution optimistic zk-rollup sécurisée, décentralisée, rentable et performante. Essayez-le maintenant !
---
Il existe plusieurs différences techniques entre l'EVM d'Ethereum et l'optimistic zkEVM de Morph. Nous avons compilé une liste pour vous aider à mieux comprendre ces distinctions.

:::tip
Pour la plupart des développeurs Solidity, ces détails techniques n'auront pas d'impact significatif sur votre expérience de développement.
:::

## Opcodes EVM

| Opcode                      | Équivalent en Solidity | Comportement de Morph                                                                                      |
| --------------------------- | --------------------- | ----------------------------------------------------------------------------------------------------------- |
| `BLOCKHASH`                 | `block.blockhash`     | Renvoie `keccak(chain_id \|\| block_number)` pour les 256 derniers blocs.                                  |
| `COINBASE`                  | `block.coinbase`      | Renvoie l'adresse du contrat de frais pré-déployé. Voir [Contrats](../../build-on-morph/developer-resources/1-contracts.md). |
| `DIFFICULTY` / `PREVRANDAO` | `block.difficulty`    | Renvoie 0.                                                                                                  |
| `BASEFEE`                   | `block.basefee`       | Désactivé. Si l'opcode est rencontré, la transaction sera annulée.                                         |
| `SELFDESTRUCT`              | `selfdestruct`        | Désactivé. Si l'opcode est rencontré, la transaction sera annulée.                                         |

## Précompilations EVM

Les précompilations `RIPEMD-160` (adresse `0x3`), `blake2f` (adresse `0x9`) et `évaluation de point` (adresse `0x0a`) ne sont actuellement pas supportées. Les appels à des contrats précompilés non supportés seront annulés. Nous prévoyons d'activer ces précompilations dans de futures mises à jour.

La précompilation `modexp` est supportée mais ne prend en charge que les entrées de taille inférieure ou égale à 32 octets (c'est-à-dire `u256`).

La précompilation `ecPairing` est supportée, mais le nombre de points (ensembles, paires) est limité à 4, au lieu de 6.

Les autres précompilations EVM sont toutes supportées : `ecRecover`, `identity`, `ecAdd`, `ecMul`.

### Limites de précompilation

En raison de la taille limitée des circuits zkEVM, il existe une limite supérieure sur le nombre d'appels qui peuvent être effectués pour certaines précompilations. Ces transactions ne seront pas annulées, mais simplement ignorées par le séquenceur si elles ne peuvent pas s'insérer dans l'espace du circuit.

| Précompilation / Opcode | Limite |
| ----------------------- | ------ |
| `keccak256`            | 3157   |
| `ecRecover`            | 119    |
| `modexp`               | 23     |
| `ecAdd`                | 50     |
| `ecMul`                | 50     |
| `ecPairing`            | 2      |

:::tip Opcodes de mise à jour Dencun non disponibles

Les opcodes de la mise à jour Dencun ne sont pas encore disponibles sur Morph, y compris `MCOPY`, `TSTORE`, `TLOAD`, `BLOBHASH` et `BLOBBASEFEE`. De plus, [EIP-4788](https://eips.ethereum.org/EIPS/eip-4788) pour accéder à la racine de bloc de la Beacon Chain n'est pas supporté. Nous vous recommandons d'utiliser `shanghai` comme cible EVM et d'éviter d'utiliser une version de Solidity supérieure à `0.8.23`.

:::

## Compte d'État

### **Champs supplémentaires**

Nous avons ajouté deux champs dans l'objet `StateAccount` actuel : `PoseidonCodehash` et `CodeSize`.

```go
type StateAccount struct {
	Nonce    uint64
	Balance  *big.Int
	Root     common.Hash // racine merkle du trie de stockage
	KeccakCodeHash []byte // toujours le Keccak codehash
	// champs ajoutés
	PoseidonCodeHash []byte // le Poseidon codehash
	CodeSize uint64
}

```
### **CodeHash**

En rapport avec cela, nous maintenons deux types de codehash pour chaque bytecode de contrat : le hash Keccak et le hash Poseidon.

`KeccakCodeHash` est conservé pour maintenir la compatibilité avec `EXTCODEHASH`. `PoseidonCodeHash` est utilisé pour vérifier l'exactitude des bytecodes chargés dans le zkEVM, où le hachage Poseidon est beaucoup plus efficace.

### CodeSize

Lors de la vérification de `EXTCODESIZE`, il est coûteux de charger l'ensemble des données du contrat dans le zkEVM. Au lieu de cela, nous stockons la taille du contrat dans le stockage lors de la création du contrat. De cette manière, nous n'avons pas besoin de charger le code — une preuve de stockage suffit pour vérifier cet opcode.

## Temps de Bloc

:::tip Temps de Bloc Suceptible de Changement

Les blocs sont produits chaque seconde, avec un bloc vide généré s'il n'y a pas de transactions pendant 5 secondes. Cependant, cette fréquence peut changer à l'avenir.
:::

Pour comparer, Ethereum a un temps de bloc d'environ 12 secondes.

Raisons d'un Temps de Bloc Plus Rapide dans Morph
Expérience Utilisateur : 

- Un temps de bloc plus rapide et constant offre un retour d'information plus rapide, améliorant l'expérience utilisateur.

- Optimisation : À mesure que nous affinons les circuits zkEVM dans nos testnets, nous pouvons atteindre un meilleur débit qu'Ethereum, même avec une limite de gaz plus petite par bloc ou par lot.

Remarques :
- `TIMESTAMP` renverra le timestamp du bloc. Il sera mis à jour chaque seconde.
- `BLOCKNUMBER` renverra un numéro de bloc réel. Il sera mis à jour chaque seconde. Le mappage un-à-un entre les blocs et les transactions ne s'appliquera plus.

<!--
Nous introduisons également le concept de transactions système qui sont créées par le `op-node`, et qui sont utilisées pour exécuter des dépôts et mettre à jour la vue de L2 sur L1. Elles ont les attributs suivants :

- Chaque bloc contiendra au moins une transaction système appelée la transaction de dépôt d'attributs L1. Ce sera toujours la première transaction dans le bloc.
- Certains blocs contiendront une ou plusieurs transactions déposées par les utilisateurs.
- Toutes les transactions système ont un type de transaction compatible avec [EIP-2718](https://eips.ethereum.org/EIPS/eip-2718) de `0x7E`.
- Toutes les transactions système ne sont pas signées et définissent leurs champs `v`, `r` et `s` sur `null`.

:::Warning Problème Connu
Certaines bibliothèques de clients Ethereum, comme Web3js, ne peuvent pas analyser les champs de signature `null` décrits ci-dessus. Pour contourner ce problème, vous devrez filtrer manuellement les transactions système avant de les transmettre à la bibliothèque.
:::
-->

## EIPs Futurs

Morph surveille de près les propositions d'amélioration d'Ethereum (EIPs) émergentes et les adopte lorsque cela est approprié. Pour plus de détails, rejoignez notre forum communautaire ou [Discord](https://discord.gg/L2Morph) pour des discussions.

<!-- ## Version cible EVM 

Pour éviter des comportements inattendus dans vos contrats, nous recommandons d'utiliser 'london' comme version cible lors de la compilation de vos contrats intelligents.

Vous pouvez lire en plus de détails sur les différences entre le hard fork de Shanghai et London sur les [spécifications d'exécution Ethereum](https://github.com/ethereum/execution-specs/tree/master/network-upgrades/mainnet-upgrades/shanghai.md) et comment la nouvelle instruction PUSH0 [impacte le compilateur Solidity](https://blog.soliditylang.org/2023/05/10/solidity-0.8.20-release-announcement/).
-->