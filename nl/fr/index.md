---

copyright:
  years: 2016, 2018
lastupdated: "2018-4-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Initiation à DevOps Insights (Bêta)
{: #gettingstarted}

{{site.data.keyword.DRA_full}} applique l'analyse du développeur, de l'équipe et de déploiement à vos projets DevOps les plus actifs. Il vous permet de savoir dans quelle mesure votre équipe se conforme aux pratiques DevOps et du développeur, de gérer les risques du codebase et d'appliquer des normes de qualité dans des projets de distribution continue.
{:shortdesc}

**Remarque** : {{site.data.keyword.DRA_short}} n'est disponible que dans la région Sud des Etats-Unis.

{{site.data.keyword.DRA_short}} comprend plusieurs groupes de fonctionnalités :

   * Developer Insights fournit une méthode globale permettant d'explorer la maturité de développement de votre projet. Vous pouvez identifier les fichiers présentant une prédisposition élevée aux erreurs et obtenir une vue de conformité du projet par rapport aux pratiques du développeur.

   * Team utilise l'analyse du codage social pour vous aider à déterminer comment votre équipe collabore et à comprendre ce qui peut être modifié pour un meilleur fonctionnement.

   * Deployment Risk est comparable à un filet de sécurité pour votre pipeline de distribution continue. Il analyse les résultats provenant des tests d'unité, tests fonctionnels, analyses de sécurité, analyses d'application et outils de couverture du code pour des jalons spécifiques de votre processus de déploiement, et empêche la publication des changements risqués. Il affiche des graphiques de tendances dans la couverture du code, les générations et les déploiements.

{{site.data.keyword.DRA_short}} est une intégration figurant dans le catalogue des chaînes d'outils ouvertes Bluemix. Pour plus d'informations sur les chaînes d'outils, voir [Utilisation des chaînes d'outils](/docs/services/ContinuousDelivery/toolchains_working.html).

Pour utiliser {{site.data.keyword.DRA_short}}, vous devez l'ajouter à une chaîne d'outils. De nombreux modèles de chaîne d'outils incluent déjà {{site.data.keyword.DRA_short}}. Veillez à également [l'ajouter à votre organisation {{site.data.keyword.Bluemix_notm}} en tant que service](/docs/services/reqnsi.html) pour pouvoir visualiser des informations sur {{site.data.keyword.DRA_short}} et accéder à certains modèles de chaîne d'outils qui l'incluent à partir de votre tableau de bord {{site.data.keyword.Bluemix_notm}}.  

De plus, IBM exécute Developer Insights et Team sur la plupart des projets open source aboutis sur GitHub. Accédez à [DevOpsInsights.io](http://devopsinsights.io/) pour voir leur développement et les données d'équipe.

## Ajout de DevOps Insights à une chaîne d'outils
{: #catalog}

{{site.data.keyword.DRA_short}} est disponible via l'intégration aux chaînes d'outils {{site.data.keyword.contdelivery_full}}. Vous pouvez ajouter {{site.data.keyword.DRA_short}} à n'importe quelle chaîne d'outils en sélectionnant cette dernière dans le catalogue des intégrations d'outil.

{{site.data.keyword.DRA_short}} est également inclus dans de nombreux modèles de chaîne d'outils. Si vous créez une chaîne d'outils à partir d'un modèle qui comprend {{site.data.keyword.DRA_short}}, veillez à ce que {{site.data.keyword.DRA_short}} soit défini sur **Avancé**. Créez ensuite la chaîne d'outils et passez à [Utilisation de DevOps Insights](/docs/services/DevOpsInsights/index.html#using).

Pour ajouter {{site.data.keyword.DRA_short}} à une chaîne d'outils :

1. Cliquez sur **Ajouter un outil**.

2. Cliquez sur **{{site.data.keyword.DRA_short}}**.

3. Cliquez sur **Créer une intégration**.

{{site.data.keyword.DRA_short}} est maintenant disponible sur la page de présentation de votre chaîne d'outils. Une recherche de données est automatiquement effectuée sur votre référentiel et votre système de suivi des problèmes.

## Utilisation de DevOps Insights
{: #using}

Si votre chaîne d'outils inclut GitHub, GitLab ou JIRA, {{site.data.keyword.DRA_short}} vous fournit automatiquement des informations sur votre codebase et votre équipe après un premier rassemblement et une analyse initiale des données. Si votre chaîne d'outils n'inclut aucune de ces intégrations, ajoutez-en une, puis procédez comme suit :

1. Sur la page de présentation de votre chaîne d'outils, cliquez sur **{{site.data.keyword.DRA_short}}**.

2. Cliquez sur **Team ** ou **Developer Insights** puis choisissez une catégorie de données.

3. Explorez les données de votre projet en affichant les tableaux de bord dans la catégorie de données. Si vous voulez en savoir plus sur un graphique ou savoir ce que vous pouvez faire de ces informations, cliquez sur **Informations** ou sur **Conseils**.

Après avoir exploré Team et Developer Insights, configurez [Deployment Risk](/docs/services/DevOpsInsights/about_risk.html) pour faciliter l'application de la qualité du code. Deployment Risk est compatible à la fois avec Delivery Pipeline pour {{site.data.keyword.contdelivery_short}} et Jenkins.
