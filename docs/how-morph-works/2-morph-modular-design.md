---
title: Conception Modulaire de Morph
lang: fr-FR
keywords: [morph,ethereum,rollup,layer2,preuve de validité,optimistic zk-rollup]
description: Améliorez votre expérience blockchain avec Morph - la solution de rollup optimiste zk sécurisée, décentralisée, économique et performante. Essayez-le maintenant !
---

La conception modulaire de la technologie blockchain, connue pour sa meilleure composition, est devenue une tendance répandue. Morph tire parti de ce principe de conception pour améliorer son architecture et sa fonctionnalité.

![architecture](../../assets/docs/protocol/archi.png)

## Vue d'ensemble

Une conception modulaire divise généralement une blockchain de couche 1 en quatre fonctions principales :

1. Consensus
2. Exécution
3. Disponibilité des données
4. Règlements

Morph applique cette approche modulaire à sa solution de couche 2 en la divisant en trois modules principaux, chacun responsable de fonctions spécifiques.


### 3 Modules Principaux de Morph

#### Réseau de Séquenceurs - Consensus et Exécution

![Réseau de Séquenceurs](../../assets/docs/protocol/dese/seq1.png)

Le réseau de séquenceurs est responsable de l'exécution et du consensus des transactions de couche 2. Pour plus de détails, veuillez consulter les [séquenceurs décentralisés de Morph](../how-morph-works/decentralized-sequencers/morph-decentralized-sequencer-network).

#### Optimistic zkEVM - Règlement

![Optimistic zkEVM](../../assets/docs/protocol/resvapro/opzk.png)

La vérification d'état garantit que les changements d'état sur la couche 2 sont valides sur la couche 1. Morph introduit Optimistic zkEVM, une solution hybride combinant zk-rollups et optimistic rollups pour la vérification d'état. Le processus implique une innovation de Morph connue sous le nom de Preuve de Validité Réactive (RVP). Cette approche innovante finalise et règle efficacement les transactions et états de couche 2. Pour plus de détails, consultez la documentation sur la [Preuve de Validité Réactive](../how-morph-works/optimistic-zkevm).

#### Rollup - Disponibilité des Données

![Rollup](../../assets/docs/protocol/general/rollup/rollup.png)

Le processus de [Rollup](../how-morph-works/general-protocol-design/1-rollup.md) implique la soumission de transactions et d'états de couche 2 à la couche 1, garantissant la disponibilité des données. La stratégie de rollup de Morph maximise l'efficacité en compressant le contenu des blocs à l'aide de zk-preuves, ce qui aide à gérer le coût de la disponibilité des données de couche 1. 


### 5 Rôles de Morph

#### Séquenceurs

Les séquenceurs jouent un rôle crucial dans le réseau en :

- Recevant les transactions des utilisateurs de couche 2 et en formant des blocs.
- Atteignant un consensus avec d'autres séquenceurs.
- Exécutant des blocs et appliquant des transitions d'état.
- Groupant les blocs et les soumettant à la couche 1.
- Synchronisant les blocs avec des nœuds complets.
- Générant des preuves de validité lorsqu'ils sont contestés.


#### Preuveur

Les preuveurs sont essentiels pour générer des zk preuves lorsqu'un séquenceur est contesté. Ils synchronisent les informations de transaction de couche 2 et produisent les zk preuves nécessaires pour valider les changements d'état.

#### Validateur

Les validateurs peuvent être n'importe quel utilisateur et jouent un rôle clé dans l'assurance de l'exactitude des états soumis par les séquenceurs à la couche 1. Ils maintiennent un nœud L2 pour synchroniser les transactions et les changements d'état, déclenchant des contestations lorsqu'ils identifient des états incorrects.

#### Nœuds

Les nœuds facilitent l'accès plus facile aux transactions et aux états de couche 2 sans participer activement aux opérations du réseau. L'exécution d'un nœud L2 est ouverte à tous et ne nécessite pas d'autorisation.

#### Couche 1

Chaque solution de couche 2 repose sur une blockchain de couche 1 pour les règlements finaux et la disponibilité des données. Pour Morph, ce rôle est rempli par Ethereum. Les contrats clés sur la couche 1 garantissent la sécurité et la finalité des transactions et états de couche 2.

### 6 Composants de Morph

#### Nœud L2

Le nœud L2 est central dans l'architecture de Morph, interagissant avec divers modules et rôles. Il comprend des sous-composants tels que :
- Gestionnaire de Transactions (Mempool) : Gère toutes les transactions de couche 2, acceptant et stockant les transactions initiées par les utilisateurs.
- Exécuteur : Applique les transitions d'état et maintient le statut en temps réel de la couche 2.
- Synchroniseur : Synchronise les données entre les nœuds L2 pour restaurer le statut du réseau.

#### Soumissionnaire de Lots
Le Soumissionnaire de Lots fait partie du séquenceur, responsable de l'obtention continue des blocs L2, de leur emballage en lots et de l'assemblage des lots en transactions de couche 1, qui sont ensuite soumises au contrat de couche 1.

#### Client de Consensus
Chaque séquenceur exécute un client de consensus pour atteindre un consensus avec d'autres séquenceurs. La conception actuelle utilise le client Tendermint pour garantir une intégration transparente et une convivialité pour les développeurs.

#### zkEVM
zkEVM fait partie du Preuveur et est une machine virtuelle adaptée aux zk, utilisée pour générer des zk preuves pour les blocs et les changements d'état d'Ethereum. Ces zk preuves sont finalement utilisées pour prouver la validité des transactions et états de L2.

#### Agrégateurs
Les agrégateurs travaillent avec zkEVM pour réduire le coût de vérification des zk preuves en les agrégeant pour la production de blocs.

#### Contrat de Couche 1
Ces contrats sur Ethereum stockent les transactions de couche 2, exécutent des changements d'état globaux et relient les actifs et les informations entre la couche 2 et la couche 1. Ils gèrent également l'élection et la gouvernance de l'ensemble des séquenceurs, héritant de la sécurité d'Ethereum.


### Intégration des Composants, Rôles et Modules

![modulaire](../../assets/docs/about/overview/modu.png)

Les composants forment la base des différents rôles dans Morph. Par exemple, exécuter un nœud L2 permet de devenir un Nœud, tandis qu'ajouter des fonctionnalités de soumissionnaire de lots et de client de consensus permet d'assumer le rôle de Séquenceur. Ces rôles collaborent pour réaliser les fonctions essentielles de Morph, créant une solution de rollup complète et efficace.
