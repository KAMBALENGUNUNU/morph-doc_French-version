---
title: Pont
lang: fr-FR
keywords: [morph, ethereum, rollup, couche2, preuve de validité, zk-rollup optimiste]
description: Améliorez votre expérience blockchain avec Morph - la solution zk-rollup optimiste sécurisée, décentralisée, rentable et performante. Essayez-le maintenant !
---

# Dépôt de Holesky au Testnet Morph

## Instructions :

:::tip Utilisez le pont ici

 https://bridge-holesky.morphl2.io
 
:::

1. Ouvrez votre portefeuille MetaMask et passez au réseau **Holesky**. 

![image1](../../assets/docs/quick-start/bridge/01.png)
![image1](../../assets/docs/quick-start/bridge/02.png)

2. Dans l'application Bridge de Morph, cliquez sur **Connecter le portefeuille**, sélectionnez MetaMask, et approuvez la connexion si demandé.

![image2](../../assets/docs/quick-start/bridge/03.png)

3. Assurez-vous que **Holesky** est sélectionné sous ‘De’ et Morph L2 sous ‘À’. Si ce n'est pas le cas, cliquez sur le bouton "↓" pour changer leurs positions.

4. Sélectionnez le jeton que vous souhaitez transférer. 

5. Cliquez sur le bouton Envoyer pour initier le dépôt.

:::tip
Si c'est la première fois que vous transférez un jeton ERC20, vous devez approuver le contrat de pont **Holesky** pour accéder à votre jeton ERC20.
:::

6. Une fenêtre apparaîtra demandant la confirmation de la transaction de transfert, cliquez sur **Dépôt**.

![image3](../../assets/docs/quick-start/bridge/04.png)

7. Cliquez sur le bouton Confirmer dans MetaMask. Une fois la transaction de transfert finalisée, le jeton sera déduit de votre adresse de portefeuille **Holesky**.

![image5](../../assets/docs/quick-start/bridge/05.png)

8. Pendant que vous attendez, vous pouvez vérifier l'état de vos transactions en cliquant sur le bouton des transactions.

![image6](../../assets/docs/quick-start/bridge/06.png)


## Combien de temps faut-il pour qu'un jeton arrive au Testnet Morph ?

Un transfert de jeton de **Holesky** au Testnet Morph peut prendre de 8 à 14 minutes (temps pour que le bloc soit sûr sur **Holesky**) avant d'apparaître dans votre portefeuille Morph. Pour vérifier l'avancement de vos transactions de dépôt, suivez ces étapes :

1. Cliquez sur votre adresse de portefeuille en haut à droite de l'application web Bridge.

![image6](../../assets/docs/quick-start/bridge/07.png)

2. Cliquez sur Transactions. Un panneau contextuel affichera vos transactions récentes.

:::tip
Note : Pour les transactions de dépôt (L1 -> L2), une fois que votre transaction est confirmée comme sûre sur **Holesky** (8 à 14 minutes), vous verrez un statut **Succès**. Vos fonds seront alors transmis à L2.
:::

![image8](../../assets/docs/quick-start/bridge/08.png)

3. Cliquez sur le dernier hachage de transaction **Holesky**.

![image9](../../assets/docs/quick-start/bridge/09.png)

4. Vous serez dirigé vers une page de Détails de la transaction dans l'Explorateur. Vérifiez le statut de votre transaction (cette transaction est confirmée sur **Holesky**). 

![image10](../../assets/docs/quick-start/bridge/10.png)

5. Une fois que le statut de votre transaction montre *succès* sur L2, retournez à l'application Bridge pour voir un hachage de transaction et des fonds dans votre portefeuille Morph L2.

![image11](../../assets/docs/quick-start/bridge/11.png)

![image12](../../assets/docs/quick-start/bridge/12.png)

# Retrait du Testnet Morph vers Holesky

Pour retirer des fonds du Testnet Morph, suivez ces étapes :
1. Initiez le retrait sur le Testnet Morph.
2. Attendez que la racine du retrait soit publiée sur L1 (**Holesky**). Cela prend généralement quelques minutes, mais cela peut prendre plus de temps en cas de panne.
3. Prouvez le retrait.
4. Attendez la période de challenge de vérification, qui dure sept jours à partir du moment où le retrait est prouvé sur L1 (**Holesky**).
5. Réclamez votre retrait.

## Initier le retrait

1. Cliquez sur Connecter le portefeuille et sélectionnez MetaMask. Si demandé, approuvez la connexion dans votre portefeuille.

2. Sélectionnez Retrait. Choisissez l'actif et le montant que vous souhaitez retirer.

![image13](../../assets/docs/quick-start/bridge/13.png)

3. Cliquez sur Envoyer ETH à **Holesky**.

![image14](../../assets/docs/quick-start/bridge/14.png)

4. Cliquez sur Initier le retrait, attendez quelques minutes pour confirmer. Une fois terminé, vous devez changer le réseau dans votre portefeuille, puis prouver le retrait sur **Holesky**.

![image15](../../assets/docs/quick-start/bridge/15.png)

![image16](../../assets/docs/quick-start/bridge/16.png)

5. Attendez que la soumission du lot soit terminée.

![image17](../../assets/docs/quick-start/bridge/17.png)

![image18](../../assets/docs/quick-start/bridge/18.png)

## Attente de la période de challenge de vérification

1. Cliquez sur votre adresse dans le coin supérieur droit.

2. Cliquez sur Transactions, puis sur Retraits. Cela affichera une liste de vos retraits récents et de leur statut. Vous pouvez aussi trouver une notification dans la zone supérieure en cliquant sur le bouton Voir le compte (voir l'image ci-dessous).

![image19](../../assets/docs/quick-start/bridge/19.png)

![image20](../../assets/docs/quick-start/bridge/20.png)

![image21](../../assets/docs/quick-start/bridge/21.png)

3. Vous pouvez rechercher le hachage de la transaction sur l'Explorateur Morph.

![image22](../../assets/docs/quick-start/bridge/22.png)

![image23](../../assets/docs/quick-start/bridge/23.png)

4. Cliquez sur la transaction de soumission de la racine d'état L1 pour voir quand la transaction a été écrite sur L1 (**Holesky**).

![image24](../../assets/docs/quick-start/bridge/24.png)

![image25](../../assets/docs/quick-start/bridge/25.png)

## Réclamer le retrait

1. Une fois la période de challenge terminée, le statut changera en Réclamer.

2. Cliquez sur Réclamer le retrait.

![image26](../../assets/docs/quick-start/bridge/26.png)

3. Confirmez le retrait dans le portefeuille.

![image27](../../assets/docs/quick-start/bridge/27.png)

4. Attendez que le retrait soit terminé.

![image28](../../assets/docs/quick-start/bridge/28.png)
