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

# A propos de Deployment Risk

{{site.data.keyword.DRA_short}} Deployment Risk fournit un grand nombre d'informations sur vos déploiements, et en particulier sur les risques. Vous pouvez l'utiliser pour automatiser la protection de la qualité dans votre pipeline de distribution à l'aide de politiques et de jalons. Il propose des données relatives à la génération et à la fréquence de déploiement, en même temps que la couverture du code et les tendances des tests.
{:shortdesc}

Après avoir ouvert {{site.data.keyword.DRA_short}} à partir de la chaîne d'outils, cliquez sur **Deployment Risk**. A partir de là, vous pouvez sélectionner une catégorie d'analyse pour explorer davantage ce qui se passe avec vos déploiements.  

Vous pouvez utiliser Deployment Risk pour appliquer des normes de qualité dans votre chaîne d'outils grâce à des politiques et des jalons. Les politiques sont des ensembles de règles ; les jalons appliquent les politiques. Vous pouvez ainsi créer une politique "Test d'unité et couverture de test" qui exige des générations qu'elles répondent à des normes de test d'unité et de couverture de test. Vous pouvez ensuite ajouter un jalon qui se réfère à cette politique dans votre processus de distribution continue. Les générations qui ne satisfont pas la politique sont arrêtées au jalon. 

## Analyse des risques

Avec l'analyse des risques, vous pouvez obtenir une vue d'ensemble des risques associés aux applications en environnements de préproduction et de production. Vous pouvez procéder à un examen plus poussé pour mieux comprendre la couverture du code, les performances des tests et les rapports de sécurité. Les tableaux de bord sont automatiquement remplis avec les informations les plus récentes provenant des tests {{site.data.keyword.DRA_short}} de vos pipelines.

## Fréquence de déploiement

Vous pouvez afficher les tendances de fréquence de déploiement pour vos environnements de préproduction et de production ou pour d'autres environnements. Cette vue montre aussi les réussites et échecs de déploiement. Vous pouvez cliquer sur un déploiement particulier pour afficher des détails à son sujet. Si vous êtes membre d'une équipe active, vous constaterez un accroissement de la fréquence de déploiement dans le temps. 

## Fréquence de génération

Vous pouvez afficher les tendances de fréquence de génération pour vos branches à exécution longue. Cette vue montre aussi les réussites et échecs de génération. Vous pouvez cliquer sur un point d'intéret et voir les détails de génération. Si vous êtes membre d'une équipe active, vous voulez voir un grand nombre de générations quotidiennes dans la branche d'intégration. Si ce n'est pas le cas, votre équipe ne fusionne pas son code fréquemment.

## Tendances de tests d'unité

Vous pouvez afficher les tendances pour les tests d'unité relatifs aux générations en provenance d'une certaine branche ou déployées dans un environnent spécifique. Ainsi, vous pouvez voir les tendances de tests pour les générations provenant de la branche maître. Si certains tests échouent pour des générations qui sont déjà passées en mode production, vous pouvez être amené à effectuer certaines actions. De plus, une diminution du nombre des tests peut devenir un sujet de préoccupation.

## Tendances des tests fonctionnels de vérification

Vous pouvez afficher les tendances pour les tests fonctionnels de vérification relatifs aux générations en provenance d'une certaine branche ou déployées dans un environnent spécifique. Ainsi, vous pouvez voir les tendances de tests pour les générations provenant de la branche maître. Si certains tests échouent pour des générations qui sont déjà passées en mode production, vous pouvez être amené à effectuer certaines actions. De plus, une diminution du nombre des tests peut devenir un sujet de préoccupation.

## Tendances de la couverture du code

Vous pouvez afficher les tendances de la couverture du code pour les générations déployées dans un environnent spécifique. Ainsi, vous pouvez voir les tendances de la couverture du code pour les générations qui sont allées en production. Idéalement, vous devez voir une amélioration de la couverture du code au fil du temps pour les générations qui vont en production. Si la couverture du code décroît, vous pouvez être amené à mettre en place une action.

## Politiques

Les politiques sont des ensembles de règles qui contrôlent les jalons de votre pipeline de distribution. Si votre code ne satisfait pas, dans un sens ou dans l'autre, une politique appliquée à un jalon particulier, le déploiement est arrêté dans le but d'empêcher la publication de changements risqués.


## Prérequis
{: #prerequisites}

Deployment Risk requiert une configuration plus poussée que la configuration décrite dans [Initiation à {{site.data.keyword.DRA_short}}](/docs/services/DevOpsInsights/index.html).

Pour utiliser Deployment Risk, vous avez besoin de deux éléments :

* Une instance de {{site.data.keyword.deliverypipeline}} ou un projet Jenkins
* Les tests que vous souhaitez utiliser pour évaluer votre projet

## Informations sur l'intégration

Deployment Risk s'intègre avec {{site.data.keyword.deliverypipeline}}, qui fait partie d'{{site.data.keyword.contdelivery_full}}, et avec les projets Jenkins. A un niveau élevé, les instructions d'utilisation de l'un ou de l'autre sont similaires.  

Si vous utilisez {{site.data.keyword.deliverypipeline}}, suivez les étapes ci-après :

1. [Créez des politiques et des règles](risk_policies.html) qui seront gérées par {{site.data.keyword.DRA_short}}.
2. [Préparez les étapes de votre pipeline](risk_cd.html) en vue de l'intégration avec {{site.data.keyword.DRA_short}}.
3. [Créez ou éditez des travaux de test](risk_cd.html) dans le pipeline qui téléchargent les résultats vers {{site.data.keyword.DRA_short}}.
4. [Ajoutez des jalons](risk_cd.html) au pipeline qui prend les décisions de promotion en fonction de ces résultats et de vos politiques.
5. Exécutez le pipeline et [affichez les résultats](results.html).

Si vous utilisez Jenkins, procédez comme suit :

1. [Créez des politiques et des règles](risk_policies.html) qui seront gérées par {{site.data.keyword.DRA_short}}.
2. [Installez et configurez le plug-in Jenkins](https://wiki.jenkins.io/display/JENKINS/IBM+Cloud+DevOps+Plugin).
3. [Créez les travaux de test et les jalons comme décrit dans les instructions du plug-in](https://wiki.jenkins.io/display/JENKINS/IBM+Cloud+DevOps+Plugin). Les tests téléchargent les résultats vers {{site.data.keyword.DRA_short}} en vue de l'analyse et les jalons utilisent ces résultats pour prendre les décisions quant aux promotions.
4. Exécutez le projet et [affichez les résultats](results.html). 

Peu importe la manière dont vous générez et déployez votre code, les résultats sont identiques : les générations qui satisfont les normes passent les jalons Deployment Risk et les générations qui ne répondent pas aux normes sont arrêtées. 
