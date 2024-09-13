---
title: Optimistic zkEVM
lang: fr-FR
keywords: [morph, couche2, preuve de validité, zk-rollup optimiste]
description: Améliorez votre expérience blockchain avec Morph - la solution zk-rollup optimiste sécurisée, décentralisée, économique et performante. Essayez-la maintenant !
---

![RVP](../../assets/docs/protocol/resvapro/rvpbanner1.jpg)

## Introduction à la Vérification d'État

La vérification d'état de la couche 2 se divise traditionnellement en deux catégories : les preuves de fraude et les preuves de validité. Morph introduit une nouvelle méthode de vérification appelée Preuve de Validité Réactive (RVP), qui combine les avantages des deux approches pour surmonter leurs limites. Les preuves de fraude, bien qu'efficaces, souffrent d'une inefficacité capitalistique et de faibles hypothèses de sécurité. De plus, aucun Optimistic Rollup (OP-Rollup) n'a pleinement mis en œuvre un mécanisme de défi de preuve de fraude sans autorisation. En revanche, les preuves de validité offrent une grande sécurité, mais rencontrent des problèmes pratiques de coût et d'efficacité qui freinent l'évolutivité des Rollups.

## Le Problème des Optimistic Rollups

Dans ce modèle, la couche 2 (L2) suppose de manière optimiste que les modifications d'état soumises par le séquenceur sont valides sans vérifier activement leur authenticité. Au lieu de cela, une période de défi est introduite avant que les modifications d'état ne soient confirmées sur la couche 1 (L1). Pendant cette période, des challengers externes vérifient les soumissions du séquenceur en fonction de leur propre statut de réseau synchronisé. S'ils trouvent des écarts, les challengers peuvent déclencher un processus de défi sur L1 pour empêcher la confirmation d'états incorrects.

**Mécanisme de Défi** : Bien que tous les rollups optimistes prétendent mettre en œuvre des preuves de fraude, seul Arbitrum les a déployées avec succès sur le mainnet. De plus, les challengers sont souvent limités à plusieurs adresses sur liste blanche. Les preuves de fraude dans les projets actuels de rollup optimiste peuvent être classées en deux types :

**Preuves de Fraude Non-Interactives** : Lorsqu'un nouvel état soumis par le séquenceur est contesté, L1 réexécute toutes les transactions correspondantes de L2 pour générer un état valide à comparer avec l'état soumis par le séquenceur. Ce processus entraîne des coûts de gaz significatifs et peut provoquer des écarts entre L2 et L1, car certaines transactions peuvent produire des résultats différents sur L2 par rapport à L1, ou L1 peut ne pas être capable d'exécuter certaines transactions de L2. Optimism (OP) a un jour utilisé cette approche, mais l'a abandonnée en raison de ces problèmes.

**Preuves de Fraude Interactives** : Pour résoudre les problèmes des preuves de fraude non-interactives, des preuves de fraude interactives multi-tours ont été introduites. Cette méthode consiste à déterminer l'exécution d'instructions spécifiques qui ont causé l'erreur grâce à plusieurs tours d'interaction entre le séquenceur et le challenger, puis à confirmer la fraude en exécutant les instructions correspondantes sur L1. Cette approche réduit les coûts computationnels et diminue le problème de résultats incongrus entre L1 et L2. Cependant, elle introduit des complexités, telles que :
- Une difficulté d'implémentation plus élevée
- Des périodes de défi plus longues (un temps suffisant doit être réservé pour des interactions complexes)
- Des normes accrues, impactant la motivation des challengers

Actuellement, seuls quelques OP Rollups ont mis en œuvre un mécanisme complet de preuve de fraude interactive sur son mainnet parmi les projets de rollup optimiste. En revanche, plusieurs projets ZK-rollup ont déjà été lancés sur le mainnet.

Ces complexités soulignent la nécessité d'améliorer les modèles de rollup optimiste existants. C'est pourquoi Morph introduit la Preuve de Validité Réactive (RVP).

## Qu'est-ce que RVP ?

![RVP](../../assets/docs/protocol/resvapro/compare3.png)

La Preuve de Validité Réactive (RVP) intègre des preuves de validité basées sur les ZK dans le cadre du rollup optimiste. Le processus est le suivant :

Lorsque des challengers détectent que le séquenceur a soumis des données incorrectes, ils initient une demande de défi au séquenceur sur la couche 1 (L1). Le séquenceur doit alors générer la preuve de Zéro Connaissance (ZK) correspondante dans un délai spécifié (période de défi) et passer la vérification du contrat L1. Si la vérification réussit, le défi échoue ; sinon, le défi réussit. Ce processus combine les avantages des rollups optimistes et des ZK-rollups, offrant une approche équilibrée de la sécurité et de l'efficacité.

### Avantages de RVP par Rapport aux Preuves de Fraude Interactives

1. **Période de Défi Plus Courte** : RVP peut réduire la période de défi de 7 jours habituels à seulement 1-3 jours, améliorant ainsi l'efficacité et l'expérience utilisateur.
2. **Coûts de Soumission L2 Réduits** : En utilisant des preuves de validité, la couche 2 (L2) n'a pas besoin d'inclure la plupart des octets de transaction, ce qui réduit considérablement les coûts de soumission.
3. **Expérience Améliorée pour les Challengers** : Avec RVP, les challengers n'ont qu'à initier le défi. Le séquenceur doit prouver sa validité en générant et en vérifiant la preuve ZK correspondante, simplifiant ainsi les responsabilités du challenger.
4. **Transition Fluide vers ZK-Rollup** : La conception architecturale de RVP permet une transition facile vers un ZK-rollup complet. Le principal changement requis est d'ajuster les méthodes de soumission de preuve ZK du séquenceur, de réactif à actif.

RVP améliore le modèle de rollup optimiste en intégrant des preuves ZK, offrant une solution plus efficace, économique et sécurisée. Elle aborde les limites des preuves de fraude traditionnelles et ouvre la voie à une transition fluide vers des implémentations complètes de ZK-rollup à l'avenir.

### Comment RVP Peut-elle Raccourcir la Période de Défi d'un Rollup Optimiste ?	
#### La Nécessité d'une Période de Défi
Les rollups optimistes intègrent une période de défi (ou période de retrait) pour s'assurer que toute soumission malveillante par le séquenceur peut être identifiée et contestée. Cette période permet aux challengers de vérifier les transactions, de réaliser des preuves de fraude et de compléter le processus de défi, garantissant ainsi que seules les modifications d'état valides sont confirmées sur la couche 1 (L1).
Deux principaux facteurs influencent la durée de la période de défi :
1. Temps de Complétion : Le temps nécessaire aux deux parties pour compléter le processus de défi.
2. Atténuation des Comportements Malveillants : S'assurer qu'il y a suffisamment de temps pour traiter les tentatives des séquenceurs de bloquer malicieusement les transactions des challengers sur L1.

#### Solutions pour Raccourcir la Période de Défi
**Processus de Défi Concis et Direct** : Pour les preuves de fraude interactives multi-tours, le processus de défi complet peut nécessiter plusieurs tours d'interaction, chacun demandant beaucoup de temps. Par exemple, si le processus nécessite 10 tours, au moins 20 blocs de temps sont nécessaires pour compléter le défi, en tenant compte des réponses de va-et-vient.
En revanche, RVP simplifie le processus de défi en ne nécessitant qu'une seule interaction : le séquenceur télécharge la preuve ZK du lot, qui est ensuite vérifiée sur L1. Ce processus rationalisé aborde le principal problème de savoir si les challengers ont suffisamment de temps pour détecter et prouver l'incorrectness, réduisant ainsi considérablement la période de défi.

**Protection Contre les Comportements Malveillants** : Dans les systèmes de preuves de fraude interactives, la partie contestée pourrait tenter d'interférer avec le progrès du défi, par exemple en lançant une attaque DoS sur L1 pour empêcher les challengers d'interagir avec L1 et de soumettre des preuves.
Avec RVP, les challengers n'ont qu'à déclencher le défi. Une fois le défi lancé, le séquenceur n'a aucune opportunité d'interférer. Le séquenceur doit ensuite prouver la validité de sa soumission grâce à la preuve ZK. Cela garantit que le processus de défi normal n'est pas affecté par un comportement malveillant, réduisant encore la période de défi.

#### Avantages Clés de RVP pour Réduire la Période de Contestation
- **Efficacité** : L'interaction unique requise pour RVP simplifie le processus de contestation, réduisant le temps nécessaire pour la résolution.
- **Sécurité** : En s'appuyant sur des preuves ZK, RVP fournit un mécanisme solide pour valider les changements d'état sans longues interactions.
- **Rentabilité** : La réduction du nombre d'interactions diminue les coûts de gaz associés aux processus de contestation sur L1.

En abordant ces facteurs, RVP réduit efficacement la période de contestation de 7 jours traditionnels à seulement 1-3 jours, offrant une solution plus efficace et sécurisée pour les rollups optimistes.

### Pourquoi le Coût d'Exploitation est-il Plus Bas pour L2 Basé sur RVP?	

#### Compression des Transactions

Dans les ZK-rollups, la validité de chaque transaction est confirmée par une preuve ZK soumise, ce qui élimine la nécessité d'inclure des détails de transaction étendus. Par exemple, la longueur d'une transaction Ethereum est d'environ 110 octets, la signature occupant environ 68 octets. Dans les rollups optimistes, comme les transactions doivent être rejouées sur L1, ces signatures doivent être incluses pour garantir la validité. Cela augmente le coût.
Cependant, les ZK-rollups n'ont besoin de conserver que les informations de base sur les transactions car la preuve de validité couvre tout le lot. Cette capacité de compression réduit la quantité de données à soumettre à L1, ce qui diminue considérablement les coûts.

#### Soumission Efficace des Données

RVP utilise des preuves ZK pour valider les transactions, adoptant l'avantage de compression des transactions des ZK-rollups lors de la soumission de données par lots. Cela réduit le volume total de données et les coûts associés. De plus, lorsqu'il n'y a pas de contestations, le séquenceur n'encourt pas le coût de génération et de soumission des preuves ZK, ce qui réduit encore les dépenses opérationnelles.

#### Comparaison avec les Solutions Existantes

La conception de RVP garantit que le coût des opérations de rollup est inférieur à celui des rollups optimistes existants et des ZK-rollups traditionnels. Cette efficacité est réalisée en :
- Réduisant le besoin de rejouer des transactions détaillées sur L1.
- Utilisant des preuves ZK uniquement lorsque cela est nécessaire, minimisant ainsi les coûts de génération de preuves inutiles.

### RVP est Amical pour les Contestants
Le cœur de RVP est l'utilisation de preuves de validité pour valider finalement les données contestées. Cela bénéficie aux contestataires de la manière suivante :
1. **Processus de Contestation Simplifié :**
- Dans RVP, le séquenceur est responsable de la génération et de la vérification des preuves. Les contestataires n'ont qu'à initier une contestation en pariant, réduisant ainsi la complexité et le fardeau pour les contestataires.
- Cela contraste avec les preuves de fraude traditionnelles, où les contestataires doivent interagir plusieurs fois avec le séquenceur, rendant le processus lourd et complexe.
2. **Seuil Plus Bas pour les Contestataires** :
- Dans de nombreux projets de couche 2, les séquenceurs ont un fort incitatif à agir de manière malveillante en raison de rendements potentiellement élevés. En revanche, les contestataires voient généralement moins d'avantages directs, ce qui entraîne un manque de motivation à contester les transactions frauduleuses.
- RVP abaisse le seuil pour les contestataires en déplaçant la responsabilité de la génération de preuves vers les séquenceurs, augmentant ainsi la probabilité de détecter et de corriger un comportement frauduleux.
3. **Atténuer les Contestations Malveillantes** :
- Bien qu'il existe un risque que des contestataires initient des contestations inutiles pour augmenter les coûts pour les séquenceurs, RVP atténue cela en exigeant que les contestataires compensent les séquenceurs pour les coûts encourus si une contestation échoue.
- Ce mécanisme décourage les contestations frivoles et garantit que seules des disputes légitimes sont soulevées.

En adoptant ces stratégies, RVP assure un processus plus équitable et efficace pour valider les transactions de couche 2, réduisant finalement les coûts d'exploitation et renforçant la sécurité et l'intégrité du réseau.

### Pourquoi les séquenceurs doivent-ils assumer la responsabilité de soumettre des preuves ZK?​ 

Certaines propositions ont suggéré que les contestataires pourraient démontrer la fausse déclaration d'un séquenceur en fournissant leur propre soumission et la preuve ZK correspondante. Les deux soumissions pourraient ensuite être comparées pour identifier toute activité frauduleuse par le séquenceur. Cependant, cette approche pose d'importantes préoccupations :

Les contestataires devraient générer des preuves ZK en utilisant les transactions fournies par le séquenceur. Si le séquenceur soumet des transactions invalides, les contestataires ne peuvent pas créer de preuves ZK qui peuvent être authentifiées sur la couche 1 (L1). Il est donc plus efficace pour les séquenceurs de prouver la validité de leurs soumissions. Cette approche garantit que l'entité responsable des transactions vérifie leur exactitude, maintenant ainsi l'intégrité du système.

### Pourquoi ne pas simplement utiliser des ZK-Rollups? 

Bien que vérifier la validité de chaque soumission d'état par le séquenceur à travers de nombreux calculs cryptographiques, comme on le voit dans les ZK-rollups actuels, offre théoriquement une sécurité supérieure, cette approche présente plusieurs défis :

#### Le Coût des ZK-Rollups

Actuellement, des projets tels que zkSync et Polygon zkEVM ont été lancés sur le mainnet, montrant que la génération et la vérification des preuves ZK ne sont plus le problème le plus pressant. Cependant, ces preuves ZK font toujours face à des contraintes de coût et d'efficacité. Par exemple, le coût moyen de transaction sur zkSync Era varie de 0,51 $ à 310 $, en fonction des frais de gaz de L1. C'est beaucoup plus cher que les coûts de transaction des projets de rollup optimistes comme Arbitrum et Optimism. En revanche, avec RVP, le coût élevé est évité pendant le fonctionnement normal du réseau en ne compressant les données de transaction en utilisant des preuves ZK que lorsque cela est contesté. Le fonctionnement normal entraîne des coûts minimaux, maintenant l'efficacité et l'abordabilité.

#### Temps de Finalisation de Bloc dans les ZK-Rollups

Théoriquement, les ZK-rollups ne devraient pas avoir de période de retrait car l'ensemble du processus de vérification des transitions d'état L2 par preuve ZK devrait être terminé en quelques minutes, voire en secondes. Cependant, la réalité pratique est différente. En raison de limitations techniques, le temps requis pour la vérification finale des preuves ZK sur L1 est beaucoup plus lent que prévu. Par exemple, zkSync Era prend environ 20-24 heures pour finaliser les blocs L2, ce qui n'est pas très différent des périodes de retrait optimisées des rollups optimistes.

#### Transition Fluide avec des Rollups Basés sur RVP

Les solutions de mise à l'échelle L2 intégrant la technologie RVP peuvent être conçues en utilisant le cadre des ZK-rollups, permettant une transition facile des L2 basés sur RVP vers des L2 standard ZK-rollup à mesure que la technologie ZK mûrit. Le principal ajustement nécessaire consiste à modifier les méthodes de soumission de preuves ZK du séquenceur, passant de réactives à actives. Ainsi, les systèmes basés sur RVP peuvent adopter sans problème tous les avantages des ZK-rollups à l'avenir.

