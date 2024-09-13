---
title: Conception du Système de Staking de Morph
lang: fr-FR
keywords: [morph,ethereum,rollup,layer2,preuve de validité,zk-rollup optimiste]
description: Améliorez votre expérience blockchain avec Morph, la solution zk-rollup optimiste sécurisée, décentralisée, et performante. Essayez-la dès maintenant !
---

# Qu'est-ce que le système de staking de Morph ?

:::tip
Actuellement, le système de staking est en phase de test bêta. Le design décrit dans ce document changera au fur et à mesure du processus de test, et ne représente pas l'expérience finale sur le réseau principal.
:::

Le staking de Morph est un système économique et technique complet basé sur le réseau de séquenceurs décentralisés pour assurer l'opération et la sécurité du réseau.

Il se divise en deux parties :

**Staking d'ETH**

Sur Ethereum, les séquenceurs potentiels doivent staker de l'ETH dans le contrat de staking de la couche 1 pour devenir un staker.

Le staking d'ETH sert à augmenter le coût du comportement malveillant des séquenceurs.

En cas de malhonnêteté ou de négligence confirmée par un séquenceur, l'ETH staké sera pénalisé. Le montant de l'ETH requis pour le staking est immuable.

**Staking de tokens Morph**

Le token Morph est le token de gouvernance de Morph (le token de gaz est l'ETH). Dans le système de staking, il joue les rôles suivants :

Le staker est élu comme séquenceur en fonction du nombre de tokens Morph que les détenteurs de tokens lui ont délégués. Ainsi, les stakers doivent attirer les détenteurs de tokens Morph à déléguer leurs tokens à eux. Seuls les séquenceurs peuvent recevoir les récompenses du réseau.
Les détenteurs de tokens Morph peuvent déléguer leurs tokens à n'importe quel staker, ce qui détermine si les stakers peuvent être sélectionnés comme séquenceur. Les séquenceurs reçoivent des récompenses grâce à l'inflation des tokens Morph en fonction de la contribution du séquenceur, et les délégants partagent une partie des récompenses en fonction de leur montant de délégation.

## Rôles dans le système de staking :

1. **Staker (candidat séquenceur)** : Toute personne (inscrite sur la liste blanche au début) peut staker de l'ETH dans le contrat de staking L1 et devenir un staker. Seuls les stakers peuvent participer à l'élection des séquenceurs.
2. **Séquenceur** : Les séquenceurs peuvent effectuer les tâches de séquenceur et être récompensés pour cela. Les séquenceurs sont sélectionnés en fonction du montant de délégation des tokens Morph.
3. **Délégant** : Les détenteurs de tokens Morph peuvent déléguer leurs tokens à n'importe quel staker. Les délégants peuvent partager les récompenses obtenues par le séquenceur délégué, en fonction des montants de délégation.

## Détails de l'élection de l'ensemble des séquenceurs :

La détermination de l'ensemble des séquenceurs se fait selon deux points :

1. Les séquenceurs doivent avoir staké un montant fixe d'ETH dans le contrat de staking de la couche 1.
2. En supposant que la taille maximale de l'ensemble des séquenceurs soit X, en fonction du montant de délégation des tokens Morph, jusqu'à X séquenceurs sont sélectionnés parmi tous les candidats valides pour former l'ensemble des séquenceurs.

L'ensemble des séquenceurs sera mis à jour en temps réel sur la base de ces principes.

Lorsqu'un nouveau token Morph est staké, le contrat de staking L2 vérifiera si cela entraînera un changement dans l'ensemble des séquenceurs, et mettra à jour l'ensemble des séquenceurs si nécessaire.

Rejoindre l'ensemble des séquenceurs signifie que tous les séquenceurs auront le droit de participer aux opérations du réseau actuel pour gagner des récompenses, tout en assumant la responsabilité de maintenir le bon fonctionnement du réseau.

En pratique, chaque séquenceur, quel que soit le montant de délégation, a le même poids.

Les séquenceurs peuvent sortir à tout moment. Ils doivent soumettre une demande de sortie sur le contrat de staking L1, puis entrer dans une période de verrouillage. Une fois que les contrats de la couche 2 ont terminé le processus de sortie et ont atteint la hauteur de bloc de déverrouillage, ils sont déverrouillés et peuvent récupérer l'ETH staké.

## Récompenses et Pénalités

### Récompenses

Il existe trois récompenses potentielles pour les séquenceurs au sein de l'écosystème Morph.

**Récompenses de staking du token Morph L2 :**

Le token Morph est inflationniste, augmentant de 6% du total maximal initial chaque année sous forme de récompenses de staking du token Morph L2.

Ces 6% seront distribués chaque jour (une journée est une époque) à tous les séquenceurs en activité.

Les séquenceurs prélèveront une commission en premier, puis distribueront le reste aux délégants en fonction de leurs montants de délégation.

**Revenu de gaz L2 :**

Les séquenceurs reçoivent de l'ETH des utilisateurs de la couche 2 (revenu L2) et dépensent de l'ETH pour soumettre des lots à la couche 1 (coût L1).

Si le coût de la couche 1 est inférieur au revenu de la couche 2, la valeur restante devient théoriquement le profit de la couche 2.

Au tout début, le réseau collecte tous les revenus de la couche 2 et paie de l'ETH aux séquenceurs pour couvrir leurs coûts de la couche 1. À l'avenir, un plan plus détaillé sera mis en place sur l'utilisation de ces fonds.

**Rendement du re-staking d'ETH :**

Pour améliorer l'efficacité du capital, nous prévoyons d'exploiter le dépôt d'ETH des stakers pour générer un rendement dans des produits de re-staking, et ce rendement sera toujours alloué aux stakers.

#### Comment déterminer les récompenses de MorphToken de chaque séquenceur ?

Cela se base sur les enregistrements de production de blocs.

À chaque époque, la récompense totale reçue par chaque séquenceur et ses délégants est calculée comme suit :

**récompense_séquenceur = (blocs_produits_par_séquenceur / blocs_totaux_produits) * inflation_totale_token_morph**

Les récompenses des séquenceurs sont finalement distribuées aux délégants (bien que les séquenceurs puissent être leurs propres délégants). Le séquenceur peut fixer un taux de commission pour en prendre une part, et ce taux est ajustable.

**commission_séquenceur = récompense_séquenceur * taux_de_commission**

La récompense que chaque délégant de ce séquenceur reçoit est la portion restante multipliée par le pourcentage de leur montant de délégation :

**récompense_délégant = (récompense_séquenceur - commission_séquenceur) * montant_de_délégation / délégation_totale**

Les récompenses de délégation de l'utilisateur seront calculées à partir de l'époque suivante après le staking de l'utilisateur.

**Exemple :**

Si l'inflation totale de Morph pour aujourd'hui (cette époque) est de 100, et qu'il y a 100 blocs produits durant cette époque.

Le séquenceur A a produit 10 blocs durant cette époque, il recevra donc :

**récompense_séquenceur = (séquenceur_bloc_produit / total_blocs_produits) * total_inflation_token_morph  = (10/100) * 100 = 10 MorphToken.**

Si le taux de commission du séquenceur est de 5% :

**commission_séquenceur = récompense_séquenceur * taux_de_commission = 10 * 0.05 = 5 MorphToken**

Si un délégataire a délégué 100 MorphToken et qu’il y a un total de 1000 MorphToken délégués au séquenceur :

**récompense_délégataire = (récompense_séquenceur - commission_séquenceur) * montant_délégation / montant_total_délégation = (100 - 5) * (100/1000) = 9.5 MorphToken**

Idéalement, puisque le poids de chaque séquenceur est le même, chaque séquenceur pourra produire la même quantité de blocs au cours d'une certaine époque. Ainsi, leurs récompenses devraient être les mêmes.

Cependant, si le séquenceur n'a pas rempli ses fonctions, la production de blocs sera bien plus faible et, par conséquent, ses récompenses seront également bien inférieures.

### Slash

Sur la base de la conception du zkEVM optimiste, des validateurs vérifieront constamment le lot soumis par les séquenceurs, et s'ils estiment que les séquenceurs ont commis une fraude, les validateurs lanceront une contestation via le contrat de rollup L1.

[Lisez plus sur la contestation ici :](../3-optimistic-zkevm.md)

Pour éviter que les comportements frauduleux des Séquenceurs n'affectent la sécurité du réseau, les règles suivantes sont établies :

- Les validateurs contesteront un lot fixe, et tous les séquenceurs ayant signé ce lot seront collectivement contestés.
- Lorsqu'un séquenceur prend le rôle de soumissionnaire de lots, des délais d'attente répétés peuvent entraîner la déduction de récompenses ou la suppression du séquenceur du groupe (pas encore entièrement implémenté).
- Les séquenceurs qui n'ont pas produit de blocs pendant de longues périodes seront retirés du groupe de séquenceurs (pas encore entièrement implémenté).

:::tip
La rotation des soumissionnaires et le délai de soumission font partie de la conception du rollup décentralisé, vous pouvez lire les détails [ici](../general-protocol-design/1-rollup.md).
:::

Pour les fonctionnalités de récompense et de slash, nous avons deux contrats :

- Contrat d'Enregistrement L2 : Les données hors chaîne affectant les récompenses et les pénalités seront collectées et enregistrées dans le contrat d'Enregistrement L2 via un Oracle, principalement constitué de données de rollup et de données de blocs.
- Contrat de Distribution L2 : Les séquenceurs et les délégataires réclameront manuellement les récompenses en fonction de l'Enregistrement.

## Gouvernance :

Nous avons actuellement un contrat de gouvernance qui décide de certains paramètres du réseau. Actuellement, seuls les séquenceurs peuvent créer des propositions et voter.

Dans la prochaine phase de la feuille de route, nous prévoyons de construire un système de gouvernance complet qui permettra à tous les détenteurs de tokens Morph de décider de chaque aspect du réseau.

## Processus Principal

### Sélection du Séquenceur & Staking

Le staking des tokens Morph sera divisé en deux phases en fonction de l'état du réseau :

- Phase 1 : L'inflation des tokens Morph et les récompenses de staking ne sont pas encore commencées.
Les élections des séquenceurs seront FCFS au début, mais la délégation de staking est autorisée. Pas de récompenses en tokens Morph car il n'y a pas encore de génération de nouveaux tokens.

- Phase 2 : L'inflation des tokens Morph et les récompenses de staking ont commencé.
L'élection des séquenceurs commencera officiellement et en fonction du montant délégué des tokens Morph, les récompenses commenceront également à être distribuées.

Comment est généré le groupe de séquenceurs ?

1. `Contrat de Staking L1` : Ajouter les séquenceurs potentiels à la liste blanche.
2. `Contrat de Staking L1` : Les séquenceurs potentiels pourront s'inscrire et miser de l'ETH sur Ethereum pour devenir éligibles à l'élection des séquenceurs (devenir staker).
3. Un message `add staker` sera envoyé comme message cross-layer du contrat de staking L1 au contrat de staking L2.
4. `Contrat de Staking L2` : Mettra à jour les stakers avec le message synchronisé.
5. `Contrat de Staking L2` : Les utilisateurs pourront déléguer/retirer la délégation de tokens Morph à un staker.
6. `Contrat de Séquenceur L2` : Le contrat de staking L2 mettra à jour le groupe de séquenceurs en appelant le contrat de séquenceur L2 en fonction du classement du montant délégué des tokens Morph. Le staker principal sera élu comme séquenceur.

### Consensus du Réseau Séquenceur & Vérification sur la Couches 1

- Chaque lot soumis nécessite la signature BLS de plus des 2/3 des séquenceurs au sein du groupe pour être accepté par le contrat de rollup L1.

Remarque : Actuellement, le contrat pré-compilé BLS 12-381 n'a pas été implémenté sur Ethereum. Par conséquent, le contrat de rollup L1 ne peut pas vérifier si le lot est signé par le groupe de séquenceurs L2.
Jusqu'à ce que cette fonctionnalité soit disponible, les contrats de rollup autorisent uniquement la soumission de lots par des stakers inclus dans la liste blanche. Cette mesure est en place pour permettre de réduire le dépôt d'ETH en cas de soumissions frauduleuses. Une fois la vérification de signature implémentée, le soumissionnaire sera autorisé sans permission, et les séquenceurs ayant signé le lot frauduleux seront pénalisés au lieu du soumissionnaire.

Processus :

1. `Contrat de Rollup L1` : Le soumissionnaire du lot s'engage à soumettre le lot au contrat de rollup.
2. `Contrat de Rollup L1` : Le contrat de rollup vérifie la signature BLS du lot et la compare avec le groupe de séquenceurs synchronisé depuis le contrat de staking L1. Il n'acceptera le lot que si la vérification est réussie.

### Slash pour les Séquenceurs

#### Que se passe-t-il si les validateurs réussissent à contester les séquenceurs ?

- Le séquenceur sera pénalisé, tout son ETH misé sera perdu, et il sera retiré du groupe de séquenceurs si le contestataire réussit.
- Même s'il est prouvé qu'il y a eu fraude à plusieurs reprises, chaque séquenceur ne sera pénalisé qu'une seule fois.
- La récompense pour le contestataire en cas de succès est une proportion fixe du montant misé.
- Si la réduction fait tomber tous les séquenceurs, alors le L2 cessera de fonctionner. Nous pourrons redémarrer en mettant à jour le contrat de staking L1, en réinitialisant les stakers et les groupes de séquenceurs. Cela n'affecte pas l'état de la Couches 2, car aucune transaction ne sera traitée à cause de cela.

Processus :

1. `Contrat de Staking L1` : Réduire l'ETH misé des séquenceurs ayant signé le lot frauduleux et les retirer du groupe.
2. `Contrat de Staking L1` : Distribuer les récompenses aux validateurs.
3. Un message `remove staker` sera envoyé comme message cross-layer du contrat de staking L1 au contrat de staking L2.
4. `Contrat de Staking L2` : Mise à jour du groupe de séquenceurs.

### Délégation de Stake

1. `Contrat de Staking L2` : Le staker fixe son propre taux de commission pour la délégation.
2. `Oracle L2` : Téléverser les enregistrements de travail des séquenceurs (enregistrements de production de blocs, enregistrements de soumission, enregistrements attendus) sur une base d'époque (une époque est un jour).
3. `Contrat de Token Morph L2` : Créer des tokens Morph (inflation) comme récompense de délégation et les envoyer au contrat distributeur L2.
4. `Contrat de Staking L2` : Les utilisateurs réclament leur récompense de délégation, les séquenceurs réclament leur commission.

### Sortie des Stakers/Séquenceurs

La période de verrouillage de la sortie doit être suffisamment longue pour garantir que les stakers et séquenceurs sur la Couches 2 ont été mis à jour et supérieure à la période de contestation du dernier bloc produit par le séquenceur (si le staker est également séquenceur).

Processus :

1. `Contrat de Staking L1` : Les stakers demandent à sortir, leur ETH misé est verrouillé pour entrer dans la période de verrouillage.
2. Un message `remove staker` sera envoyé comme message cross-layer du contrat de staking L1 au contrat de staking L2.
3. `Contrat de Staking L2` : Recevoir le message, retirer le staker et les séquenceurs (si ce staker est également un séquenceur) du groupe de séquenceurs.
4. `Contrat de Rollup L1` : Le soumissionnaire s'engage à soumettre le lot au contrat de rollup.

:::warning
La sortie du groupe de séquenceurs n'est pas encore implémentée et est encore en cours de conception.
:::

### Oracle & Récompenses Automatiques

La récompense des séquenceurs et des délégataires est le calcul basé sur l'inflation du total de tokens Morph au sein du réseau de la Couches 2. L'enregistrement des données est traité par un Oracle qui est essentiellement le Rollup ZKP complet produit par le séquenceur.
