---
title: L'Architecture de Morph
lang: fr-FR
keywords: [morph,layer2,preuve de validité,optimistic zk-rollup]
description: Améliorez votre expérience blockchain avec Morph - la solution optimistic zk-rollup sécurisée, décentralisée et performante. Essayez-le maintenant !
---

:::tip

Cette vue d'ensemble offre une introduction concise à la technologie de rollup de Morph. Pour une compréhension approfondie, veuillez consulter la section "Comment Fonctionne Morph" de notre documentation.

:::

![Archi](../../assets/docs/about/architecture/archi.png)

## L'Approche Modulaire en Layer 2

Traditionnellement, le concept de modularité a été appliqué aux blockchains de Layer 1, les segmentant en couches distinctes. Chez Morph, nous avons étendu cette philosophie modulaire au Layer 2, construisant notre plateforme autour de ce principe.

Dans une blockchain typique de Layer 1, l'architecture se compose de quatre grandes couches :
- Consensus : Le mécanisme par lequel un accord est atteint dans le réseau.
- Exécution : Lieu où le traitement des transactions et les opérations de contrats intelligents se produisent.
- Règlement : Le processus de finalisation des transactions.
- Disponibilité des Données : Assurer que les informations nécessaires sont accessibles pour la validation.

Dans le contexte du Layer 2, Morph réinterprète ces couches avec des fonctionnalités uniques :

- **Consensus et Exécution via le Réseau de Séquenceurs Décentralisés** : Chez Morph, ces fonctions sont intégrées et gérées par notre réseau de séquenceurs décentralisés. Les séquenceurs orchestrent, traitent et atteignent un consensus sur les transactions de Layer 2, formant l'interface principale pour les interactions des utilisateurs.

![Archi](../../assets/docs/about/overview/seq1.png)

- **Règlement avec Optimistic zkEVM** : Le règlement dans Morph fait référence à la finalisation des transactions de Layer 2 au niveau d'Ethereum. Cela implique l'étape cruciale de validation des états de Layer 2. Morph utilise l'optimistic zkEVM à cet effet, une approche hybride mêlant le meilleur des optimistic rollups et des zk-rollups. Les états de Layer 2 seront finalement finalisés par une période de défi significativement plus courte ou, s'ils sont contestés, par une preuve zk correspondante.

![Archi](../../assets/docs/about/overview/opzk.png)

- **Disponibilité des Données grâce au Processus de 'Rollup'** : Cela consiste à transférer les données essentielles de Layer 2 vers Ethereum. Dans Morph, cela se fait par le processus de 'Rollup', où un soumissionnaire de lots compile des blocs en lots et les soumet en tant que transactions de Layer 1 sur Ethereum.

![Archi](../../assets/docs/about/architecture/rollup.png)

## Fonctions Indépendantes mais Collaboratives

Chacune de ces fonctions majeures opère de manière indépendante, facilitant des tâches asynchrones et des mises en œuvre interchangeables :
1. Réseau de Séquenceurs : Exécute les transactions de Layer 2 et met à jour l'état local.
2. Module de Rollup : Transforme les blocs de Layer 2 en lots pour soumission à Layer 1.
3. Vérification d'État : Utilise la sécurité de Layer 1 pour vérifier les états de Layer 2 sous les règles de l'optimistic zkEVM.

Cette architecture modulaire améliore la flexibilité, l'adaptabilité et la composabilité au sein de l'écosystème Morph.

## Rôles Divers

L'architecture de Morph est également définie par cinq rôles clés : Séquenceurs, Validateurs, Nœuds, Preuveurs, et Layer 1 (Ethereum). Chaque rôle a des responsabilités spécifiques et utilise des composants distincts pour remplir sa fonction, contribuant au bon fonctionnement du réseau.

Pour une compréhension plus approfondie de l'architecture de Morph, veuillez visiter notre [Documentation Développeur](../build-on-morph/0-developer-navigation-page.md).
