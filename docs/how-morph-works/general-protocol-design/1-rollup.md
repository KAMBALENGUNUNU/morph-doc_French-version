---
title: Rollup
lang: fr-FR
keywords: [morph, ethereum, rollup]
description: Explication du processus de rollup dans Morph
---

:::info
En tant que fondement d'un projet de Couches 2, le processus de "Rollup" fait référence à la méthode par laquelle la Couches 2 assemble les transactions et l'état de la L2 en lots, puis les soumet à la L1, ainsi que l'état de la L2.

Dans l'[architecture de Morph](../2-morph-modular-design.md), ce processus de Rollup est exécuté par les composants ```Batch Submitter```.
:::

### Vue d'ensemble du design Rollup de Morph :

![rollup](../../../assets/docs/protocol/general/rollup/rollup.png)

## Construction du Lot

Le nœud L2 au sein du séquenceur génère des blocs L2 basés sur les résultats de consensus et met à jour l'état local de la L2. Le soumetteur de lots doit interroger le nœud L2 pour récupérer les derniers blocs L2.

Le soumetteur de lots reconstruit ensuite les blocs L2, en compilant :

- Transactions : Toutes les transactions contenues dans les blocs.
- InfoBloc : Informations essentielles de chaque bloc.

Le soumetteur de lots continue de récupérer et de reconstruire des blocs jusqu'à ce qu'il traite un bloc avec une signature BLS, indiquant que le point du lot est atteint. Les données du bloc reconstruit sont utilisées pour construire un lot, qui contient :

- dernierNuméroBloc : Le numéro du bloc final dans le lot.
- Transactions : Transactions encodées dans le lot.
- TémoignageBloc : Informations de bloc encodées, utilisées pour la preuve zk.
- PréEtatRacine : La racine d'état avant l'application du lot.
- PostEtatRacine : La racine d'état après l'application du lot.
- RacineRetrait : Racine de l'arbre Merkle des retraits L2.
- Signature : La signature BLS du lot.

:::info
L'InfoBloc (TémoignageBloc) est nécessaire puisque Morph utilise la technologie zk pour prouver l'exactitude des données du lot soumis. Il sert de témoin dans la Preuve Zero-Knowledge.
:::

## Regroupement de plusieurs lots dans une seule transaction de Rollup

Bien qu'il soit courant pour les projets de rollup d'inclure un seul lot par transaction L1, Morph optimise en insérant autant de lots que possible dans une seule transaction L1.  
Cette approche axée sur l'efficacité réduit considérablement les coûts globaux, car les frais L1 sont un composant prédominant des coûts de transaction associés à la L2. En optimisant l'utilisation de l'espace disponible, Morph réalise des économies sans compromettre l'intégrité des transactions.

## Soumission des données du lot au contrat de Rollup

Le soumetteur de lots finira par envoyer une transaction Ethereum depuis son compte L1 vers le contrat principal de Morph.

Les données du lot sont contenues dans la calldata de la transaction.

:::info
En fonction du processus de développement de l'ERC-4337, les futures données de lots seront probablement incorporées dans une nouvelle structure de ‘blob’ pour réduire davantage les coûts.
:::

Une fois la transaction soumise et confirmée sur Ethereum, les nœuds validateurs peuvent reconstruire et vérifier la validité des soumissions des séquenceurs en utilisant les données transactionnelles du lot.

## Finalisation des lots

Si les lots sont valides selon les normes de preuve de validité réactive de Morph [responsive validity proof](../3-optimistic-zkevm.md), toutes les transactions contenues dans les lots seront finalisées, y compris les transactions de retrait.

En conséquence, les demandes de retrait seront satisfaites et les actifs bloqués correspondants sur la Couches 1 seront libérés.

# Soumetteur de lots décentralisé

## Qu'est-ce qu'un Soumetteur de Lots ?

Un Soumetteur de Lots joue un rôle crucial dans le processus de "rollup", servant de pont qui connecte les données de la Couches 2 (L2) avec Ethereum (Couches 1 ou L1). Leurs responsabilités principales incluent :

- Collecter les transactions L2 et les données des blocs, les assembler en un lot cohérent.
- Intégrer ces données de lot dans une transaction de Couches 1.
- Exécuter cette transaction en appelant le contrat de Couches 1 pour terminer le processus de rollup.


![rollup](../../../assets/docs/protocol/general/rollup/rollup.png)

## Quelle est la relation entre les Séquenceurs et les Soumetteurs de Lots ?

La fonction du soumetteur de lots est souvent intégrée dans le rôle plus large de "séquenceur". Dans une architecture de réseau de séquenceurs décentralisée, chaque séquenceur est équipé d'un composant soumetteur de lots ou y a accès. Cette intégration est essentielle pour atteindre et maintenir les plus hauts niveaux de décentralisation.

Cette structure garantit que les données téléchargées sur la Couches 1 restent décentralisées, empêchant une seule entité de contrôler le processus de rollup.

## Comment décentraliser le Soumetteur de Lots ?

Pour respecter les principes mentionnés ci-dessus, il est essentiel de s'assurer que plusieurs séquenceurs puissent partager les tâches de rollup de manière équitable dans le même cadre temporel. Notre approche pour atteindre cet objectif implique un système de rotation pour que les séquenceurs prennent à tour de rôle la responsabilité d'appeler le soumetteur de lots, comme détaillé ci-dessous :

### Rotation des Soumetteurs

- **Changement de Rôle à Chaque Cycle d'Époque** : Les séquenceurs alternent les rôles de soumetteurs de lots au sein d'un cycle d'Époque établi.
- **Capacité d'Exécution Inter-Époques** : Tout Séquenceur peut effectuer un Rollup pour l'Époque d'un autre Séquenceur.
- **Enregistrement des Timeouts** : Le système enregistre les cas où aucun rollup ne se produit pendant une époque, celle-ci sera marquée comme "timeout", ainsi que le séquenceur responsable.

### Timeout

- **Identification du Timeout** : Si une époque se termine sans rollup (soumission de lots), elle est identifiée comme un "timeout". Le timing d'un rollup est lié au temps de confirmation de la transaction de rollup sur la Couches 1.

- **Rotation des Époques** : La durée d'une époque et le calendrier de rotation sont régis par la gouvernance du réseau de séquenceurs. Les séquenceurs se voient attribuer des index qui déterminent leur responsabilité pour une époque. Avec les changements dans l'ensemble des séquenceurs, les index sont réassignés, et les époques tournent en conséquence en fonction de ces nouvelles attributions.

### Pénalités en cas de Timeout

- **Pénalités Accumulées** : Les séquenceurs qui affichent fréquemment des comportements de timeout peuvent faire face à des pénalités liées à leur staking en ETH sur la Couches 1. Si le nombre de timeouts atteint un certain niveau, le séquenceur peut/sera exclu du réseau de séquenceurs.

## Conception des Modules

Vous trouverez ci-dessous les contrats responsables de chaque module et leurs responsabilités :

### Couches 1
- **RollupContract** : Enregistre l'exécuteur du rollup et synchronise avec la Couches 2.

### Couches 2
- **SequencerContract** : Synchronise les Séquenceurs.
- **GovContract** : Gère les Paramètres de Lots et d'Époques.
- **SubmitterContract** :
  - Enregistre les informations des Époques.
  - Enregistre l'historique des Rollups.
  - Enregistre la Charge de Travail des Soumetteurs.
  - Enregistre les Timeouts des Soumetteurs.
- **IncentiveContract** : Applique les actions d'Incitations et de Pénalités.
