---
title: Réseau de Séquenceurs Décentralisés de Morph
lang: fr-FR
keywords: [morph,ethereum,rollup,couche2,preuve de validité,optimistic zk-rollup]
description: Améliorez votre expérience blockchain avec Morph - une solution zk-rollup optimiste décentralisée, sécurisée, économique et performante. Essayez-la dès maintenant !
---


![PVR](../../../assets/docs/protocol/dese/dseq1.jpg)


## L'Importance des Séquenceurs Décentralisés



### Qu'est-ce qu'un séquenceur et quel est son rôle ?

Dans une blockchain de couche 1 traditionnelle, les transactions sont regroupées et traitées par des mineurs dans les systèmes de preuve de travail ou par des nœuds validateurs dans les systèmes de preuve d'enjeu. Ces entités obtiennent l'autorité pour regrouper, séquencer et produire des blocs soit par la tâche concurrentielle du minage, soit par des élections basées sur le staking.

Cependant, beaucoup de conceptions actuelles de la couche 2 emploient un rôle unique, non soumis à la concurrence ou aux coûts de staking, responsable du regroupement et de la séquence de toutes les transactions de la couche 2. Cette entité est connue sous le nom de "séquenceur". Ses tâches ne se limitent pas à la séquence, mais comprennent également la génération de blocs L2, l'engagement périodique des transactions et des changements d'état de la couche 2 à la couche 1, ainsi que la gestion de tout défi potentiel à ses soumissions.

Les séquenceurs centralisés posent un problème en raison de leur contrôle exclusif sur le regroupement et la séquence des transactions de la couche 2, soulevant des préoccupations liées à ce contrôle centralisé.


### Quels sont les problèmes avec les séquenceurs centralisés ?

#### Vulnérabilité d'un Point Unique de Défaillance

Le bon fonctionnement de la couche 2 est intrinsèquement lié à l'opération du séquenceur. Si le séquenceur cesse de fonctionner, les transactions de tous les utilisateurs de la couche 2 ne seront pas traitées, entraînant un arrêt des opérations de la couche 2. Ce problème est amplifié lorsqu'une seule entité contrôle le séquenceur. Si cette entité échoue, l'ensemble de la couche 2 est paralysé, rendant le système vulnérable à un point unique de défaillance. Par conséquent, les séquenceurs centralisés représentent un risque important pour la stabilité de la couche 2.

#### Censure Excessive des Transactions

Les séquenceurs centralisés peuvent rejeter les transactions soumises par les utilisateurs, les rendant inaccessibles — une forme manifeste de censure des transactions. Dans un scénario où une couche 2 centralisée bloque délibérément des transactions impliquant ses tokens de gouvernance, la panique et la vente massive parmi les utilisateurs peuvent suivre.
Certaines solutions permettent aux utilisateurs de soumettre leurs transactions directement sur la couche 1. Cependant, ce processus est long, souvent plusieurs heures, et oblige les utilisateurs à payer des frais de gaz de la couche 1. Par conséquent, cette alternative ne résout pas fondamentalement le problème.
Dans un cadre de séquenceur décentralisé, si un séquenceur refuse une transaction, les utilisateurs peuvent toujours la relayer à d'autres séquenceurs. Le contenu du prochain bloc est déterminé par consensus, garantissant qu'aucune entité ne puisse censurer les transactions selon ses intérêts personnels.


#### Monopole sur la MEV

Le séquenceur, en déterminant l'ordre (ou "séquence") des transactions reçues, détient un monopole sur toute la valeur extractible par les mineurs (MEV). Dans ce scénario, les utilisateurs doivent supporter les pertes potentielles causées par le contrôle exclusif du séquenceur sur la MEV, créant ainsi un besoin supplémentaire et injustifié de faire confiance au séquenceur.
Les séquenceurs décentralisés introduisent une dynamique concurrentielle entre plusieurs entités visant la MEV. Cette concurrence élimine le monopole d'un seul séquenceur, atténuant les effets négatifs de la MEV incontrôlée sur les utilisateurs.



## Quelle est l'approche de Morph pour les Séquenceurs Décentralisés ?

Morph se distingue des autres projets Rollup en mettant l'accent dès le début sur l'établissement d'un réseau de séquenceurs décentralisé. Cette conception repose sur les principes clés suivants :

### Efficacité :
Morph est avant tout une solution de mise à l'échelle d'Ethereum, axée sur l'amélioration de l'efficacité et la réduction des coûts. Notre solution doit garantir une exécution rapide et une confirmation des transactions en couche 2 tout en maintenant le plus haut niveau possible de décentralisation.

### Extensible et Gérable :
La conception du réseau de séquenceurs privilégie la facilité de maintenance, d'expansion et de mise à jour. Si une fonctionnalité du réseau nécessite une maintenance, elle ne doit pas perturber le fonctionnement des autres fonctionnalités. De plus, le réseau de séquenceurs doit être adaptable et facilement évolutif à mesure que de nouvelles solutions plus efficaces émergent.

### Solutions Formulées sur Ces Principes
Avec ces principes, la conception du réseau de séquenceurs de Morph inclut :
 - Modularité : La structure met l'accent sur des composants modulaires qui sont faiblement connectés, permettant des mises à jour ou des remplacements rapides.
 - Consensus Tolérant aux Pannes Byzantines (BFT) : Les séquenceurs emploient un consensus BFT pour la génération de blocs L2.
 - Signature BLS pour la Signature de Lots : Les séquenceurs signent collectivement des blocs L2 en utilisant la méthode de signature BLS. Le contrat L1 vérifie ensuite ce consensus L2 à travers la signature BLS.


:::tip
Pourquoi la signature BLS ?

Un algorithme de signature de base actuel tel que l'ECDSA dans Ethereum a un coût excessif. Ce problème se pose car les données de signature doivent être soumises au contrat de la couche 1 et nécessitent le paiement du coût correspondant. À mesure que le nombre de validateurs augmente, ce coût augmentera proportionnellement. En utilisant les signatures BLS, le coût de téléchargement des signatures peut être maintenu à un niveau constant, indépendamment de la croissance progressive du nombre de séquenceurs.

:::



### Architecture

Voici une illustration simple de l'architecture du réseau de séquenceurs décentralisé de Morph.


![Réseau de Séquenceurs](../../../assets/docs/protocol/dese/seq1.png)


#### Sélection du Groupe de Séquenceurs

Un réseau complet de séquenceurs décentralisé Morph se compose de deux parties :

- **Groupe de Séquenceurs** : Il forme le groupe central qui fournit les services de séquence.
- **Contrat de Staking des Séquenceurs** : Ce contrat facilite la sélection du groupe de séquenceurs via un processus électoral.

Grâce au contrat de staking des séquenceurs, des membres sont élus dans le groupe de séquenceurs, où ils fournissent des services de manière collaborative pour le réseau Morph. Périodiquement, les résultats des élections sont synchronisés avec le contrat de Rollup de la couche 1. Ces données synchronisées sont utilisées pour obtenir les signatures agrégées BLS des participants du réseau de séquenceurs à des fins de comparaison et de vérification.

### Génération de Blocs de la Couche 2

Grâce à la conception modulaire de Morph, chaque séquenceur exploite un client de consensus qui exécute le BFT pour communiquer avec d'autres séquenceurs.

![Génération de Blocs](../../../assets/docs/protocol/dese/block-con.png)

Conformément au protocole de consensus BFT, le séquenceur sélectionné extrait les transactions du mempool, construit des blocs et les synchronise avec d'autres séquenceurs pour les soumettre à la vérification et au vote. Le résultat final est la génération de nouveaux blocs de la couche 2.

### Regroupement

En tenant compte des coûts liés au téléchargement et à la validation des signatures sur la couche 1, les séquenceurs signeront un lot de blocs avec des signatures BLS à des points de contrôle désignés.

![Signature de Blocs](../../../assets/docs/protocol/dese/batch-sign.png)

Après la signature, le séquenceur désigné transmet le lot collectif de blocs à la couche 1 via son composant soumetteur de lots.

### Vérification du Consensus

Le séquenceur sélectionné doit soumettre au contrat de la couche 1 :

- Les signatures BLS agrégées
- Le lot de transactions
- L'état déterminé par consensus

Le contrat de la couche 1 vérifiera la signature soumise pour confirmer le consensus de la transaction.

## Résumé 

- Morph exploite un réseau de séquenceurs décentralisé natif basé sur le consensus BFT.
- Grâce à l'optimisation du protocole et du réseau, Morph maximise la scalabilité d'Ethereum tout en garantissant la décentralisation.
- Grâce aux signatures BLS, les autres participants des couches 1 et 2 peuvent efficacement vérifier les résultats de consensus de la couche 2, garantissant ainsi que la sécurité fournie par le réseau de séquenceurs soit confirmée au niveau de la couche 1.


## Feuille de Route

**Étape 1**: Test fermé sur le testnet beta de Morph

**Étape 2**: Réseau de séquenceurs décentralisé en direct sur le mainnet

**Étape 3**: Élection ouverte du groupe de séquenceurs

Rejoignez Morph dès maintenant pour un avenir blockchain plus décentralisé, sécurisé et efficace !

