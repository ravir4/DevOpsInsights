---

copyright:
  years: 2016, 2018
lastupdated: "2018-3-28"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Foire aux questions
{: #faqs}

Cette page est une liste souvent mise à jour des questions fréquemment posées à propos d'{{site.data.keyword.DRA_full}}.

## Comment retirer des données extraites suite à l'exploration d'un référentiel par {{site.data.keyword.DRA_short}} ?

Modifiez le filtre de données du référentiel de façon à exclure les données que vous voulez retirer. 

Pour changer le filtre de données {{site.data.keyword.DRA_short}}, cliquez sur **Paramètres** puis sur **Filtres**. 

## Certains des problèmes que je rencontre ne figurent pas ici. Comment puis-je les ajouter ?

Si le système de suivi des problèmes ne fait pas partie de votre chaîne d'outils, ajoutez-le. {{site.data.keyword.DRA_short}} n'explore que les services qui font partie de la chaîne d'outils. 

Si le système de suivi des problèmes est inclus dans votre chaîne d'outils, vérifiez que les étiquettes {{site.data.keyword.DRA_short}} sont mappées aux étiquettes utilisées par votre service. Cliquez sur **Paramètres** et sur **Etiquettes** puis vérifiez le mappage.

En dernier recours, retirez le service de suivi des problèmes de votre chaînes d'outils puis ajoutez-le à nouveau. {{site.data.keyword.DRA_short}} procède à l'exploration du nouveau service et à l'extraction des données, opération qui peut durer quelques heures. 

## Comment recréer un référentiel pour exploration ?

Supprimez l'intégration {{site.data.keyword.DRA_short}} de votre chaîne d'outils puis ajoutez-la à nouveau.

## Comment ajouter un référentiel à explorer ?

Ajoutez-le à une chaîne d'outils en cliquant sur **Ajouter un outil** dans la page de présentation de la chaîne d'outils. Une fois que le référentiel fait partie de votre chaîne d'outils, Insights procède à l'exploration de vos données pour inclure ce référentiel.

Cochez la case **Activer GitHub Issues** lors de l'ajout d'un référentiel afin d'activer l'exploration des problèmes. 

## Pourquoi est-ce que je ne vois aucune génération ou aucun déploiement ?

DevOps Insights explore automatiquement les référentiels de code et les problèmes qui font partie d'une chaîne d'outils mais vous devez configurer votre pipeline pour rendre possible une surveillance des générations et des déploiements. 

Assurez-vous d'abord que vous disposez d'un pipeline Continuous Delivery ou Jenkins dans votre chaîne d'outils. 

Vérifiez ensuite que votre pipeline est configuré pour la génération et la surveillance du déploiement. Pour savoir comment configurer votre pipeline, voir [Intégration de Deployment Risk Analytics à Continuous Delivery](risk_cd.html) ou [la documentation relative à l'intégration Jenkins](https://wiki.jenkins.io/display/JENKINS/IBM+Cloud+DevOps+Plugin).
