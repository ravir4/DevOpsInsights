---

copyright:
  years: 2016, 2018
lastupdated: "2017-10-25"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Intégration de Deployment Risk Analytics à Continuous Delivery

{{site.data.keyword.DRA_short}} effectue le suivi du risque de déploiement basé sur les données de test que vous y publiez. Ces données peuvent inclure des tests d'unité, une couverture du code, des tests fonctionnels de vérification, des données SonarQube ou des données d'analyse provenant d'IBM Application Security on Cloud. Après avoir publié ces données, vous pouvez ajouter des jalons à vos pipelines de façon à vous permettre d'arrêter les générations qui ne respectent pas les politiques d'administration du risque.

Pour voir une explication détaillée du composant Deployment Risk Analysis de {{site.data.keyword.DRA_short}}, voir [A propos de Deployment Risk](./about_risk.html).

Pour plus d'informations sur les pipelines de distribution continue, voir la [documentation officielle](../ContinuousDelivery/pipeline_working.html).

## Présentation
{: #integrate_pipeline}

{{site.data.keyword.DRA_short}} requiert les informations ci-après en provenance de votre pipeline afin d'analyser le risque de déploiement :

* Enregistrements de génération
* Enregistrements de déploiement
* Résultats de test

Les résultats de test doivent fournir des données dans l'un des formats pris en charge suivants :

| Type de test                    | Formats pris en charge                                               |
|------------------------------|-----------------------------------------------------------------|
| Test fonctionnel de vérification | Mocha, xUnit                                                    |
| Test d'unité                    | Mocha, xUnit, Karma/Mocha                                       |
| Couverture de code                | Istanbul, Blanket.js, Cobertura, lcov                                           |
| Analyse application statique              | Analyses d'application statiques fournies par IBM Application Security on Cloud  |
| Analyse application dynamique             | Analyses d'application dynamiques fournies par IBM Application Security on Cloud |
| SonarQube                    | Données d'analyse fournies par les analyses SonarQube                           |

Les variables d'environnement que vous définissez dans le pipeline fournissent du contexte pour la publication de ces enregistrements. Vous pouvez les définir en utilisant la commande `export` dans les scripts de vos travaux. Vous pouvez également les définir dans le menu Propriétés d'environnement de chaque étape de pipeline.

Variables d'environnement :

| Variable d'environnement  | Objectif | Obligatoire dans |
|-----------------------|-------- |-------------|
| `LOGICAL_APP_NAME`    | Définit le nom de l'application sur le tableau de bord. | Tous les travaux permettant de générer, tester, déployer et appliquer des politiques d'administration du risque {{site.data.keyword.DRA_short}}. |
| `BUILD_PREFIX`  | Texte qui est ajouté comme préfixe aux générations d'étape. Ce texte apparaît également sur le tableau de bord. | Tous les travaux permettant de générer, tester, déployer et appliquer des politiques d'administration du risque {{site.data.keyword.DRA_short}}. |
| `LOGICAL_ENV_NAME`  | Environnement dans lequel l'application s'exécute. | Travaux de test et de déploiement. |

Prenez soin d'utiliser ces variables de façon cohérente :

* Pour une application particulière, servez-vous de la même variable `LOGICAL_APP_NAME` dans tous les travaux ou étapes. 
* La valeur `BUILD_PREFIX` doit être la même pour une application et un type de génération particulier. Ainsi, pour les générations provenant de la branche maître, `BUILD_PREFIX` pourrait être `"master"`. 
* Utilisez la même valeur `LOGICAL_ENVIRONMENT_NAME` dans les travaux de test et de déploiement correspondants. Si vous utilisez la valeur `LOGICAL_ENVIRONMENT_NAME` de `"PRODUCTION"` dans un travail de déploiement, utilisez la même valeur quand vous publiez des résultats à partir de tests qui s'exécutent aussi dans cet environnement.

## Variables d'environnement de travail de génération

Pour le dernier travail de génération d'une étape, définissez des variables d'environnement pour un nom d'application et un préfixe de génération. Un exemple de script doit inclure les commandes suivantes :

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"
```

Lorsque ce travail de génération est terminé, le pipeline publie un message sur {{site.data.keyword.DRA_short}} indiquant qu'une génération SampleApp est terminée.

## Variables d'environnement de travail de déploiement

Pour le dernier travail de déploiement de l'étape, définissez un nom d'application, un préfixe de génération et un nom d'environnement. Un exemple de script doit inclure les commandes suivantes :

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"
export LOGICAL_ENV_NAME="Production"
```

Lorsque votre travail de déploiement est terminé, le pipeline publie un message sur {{site.data.keyword.DRA_short}} indiquant que la génération et l'application spécifiées ont été déployées sur un environnement.

## Variables d'environnement de travail de test

Pour tous les travaux qui produisent des résultats de test, définissez un nom d'application et un préfixe de génération.

Si le travail génère des résultats de test  fonctionnel de vérification vous devez également indiquer comme nom d'environnement logique l'emplacement sur lequel ces tests se déroulent.

Un exemple de script doit inclure les commandes suivantes :

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"

# The LOGICAL_ENV_NAME variable is only needed when publishing FVT results.
export LOGICAL_ENV_NAME="Production"
```

## Publication de résultats de test
{: #configure_pipeline_jobs}

{{site.data.keyword.DRA_short}} utilise les résultats de test à partir de vos travaux pour générer des rapports et appliquer des politiques d'administration du risque.

Dans un pipeline, vous pouvez utiliser n'importe quel type de travail pour exécuter un test. Après avoir exécuté ce test, vous pouvez télécharger ses résultats sur {{site.data.keyword.DRA_short}}. Vous téléchargez les résultats en appelant une interface de ligne de commande dans le script shell du travail. 

Vous pouvez télécharger ces types de résultats de test à partir de l'interface de ligne de commande :

* Tests d'unité
* Couverture de code
* Tests fonctionnels de vérification
* Résultats SonarQube
* Résultats d'analyse d'application statique et dynamique à partir d'IBM Application Security on Cloud. 

Il s'agit d'un exemple de script qui exécute des tests, puis télécharge les résultats sur {{site.data.keyword.DRA_short}} : 

```
# Run tests and generate a test results file here.
...

# Then, publish results to DevOps Insights
export PATH=/opt/IBM/node-v4.2/bin:$PATH
npm install -g grunt-idra3
idra --publishtestresult --filelocation=fvttest.json --type=fvt
```

Dans cet exemple, la commande `idra`, qui s'exécute avec l'indicateur `--publishtestresult`, spécifie que le script  télécharge les résultats. L'indicateur `--filelocation` signale l'emplacement du fichier de résultats de test relativement au répertoire racine du travail. L'indicateur `--type` précise le type de test qui s'exécute.

La commande `idra` prend en charge les valeurs de `type` suivantes : 

| Type | Description |
|------|-------------|
| `unittest` | Résultats de test d'unité | 
| `fvt` | Résultats de test fonctionnel de vérification|
| `code` | Résultats de couverture de code| 
| `sonarqube` | Résultats d'analyse SonarQube| 
| `staticsecurityscan` | Résultats d'analyse de sécurité statique à partir d'IBM Application Security on Cloud |
| `dynamicsecurityscan` | Résultats d'analyse de sécurité dynamique  à partir d'IBM Application Security on Cloud |

Pour en savoir plus sur la commande `idra`, voir la [page sur le package grunt-idra3 sur npm](https://www.npmjs.com/package/grunt-idra3). 

## Définition de jalons
{: #configure_pipeline_gates}

Les jalons {{site.data.keyword.DRA_short}} vérifient si vos résultats de test sont conformes à une politique définie. Si la politique n'est pas satisfaite, le jalon {{site.data.keyword.DRA_short}} échoue par défaut. Vous pouvez également configurer des jalons destinés à jouer un rôle de conseil pour autoriser la progression du pipeline même après un échec.

Le tableau de bord Deployment Risk repose sur la présence d'un jalon après un travail de déploiement de préproduction. Si vous voulez utiliser le tableau de bord, vérifiez qu'il existe un jalon après le déploiement vers l'environnement de préproduction, mais avant le déploiement vers un environnement de production.

Les jalons sont généralement placés avant la promotion de la génération dans votre pipeline. Ces emplacements sont parfaits pour le contrôle de la qualité de la génération par rapport aux politiques dans le but de garantir la sécurité de la promotion entre deux environnements. Toutefois, vous pouvez placer des jalons dans le pipeline à tout emplacement auquel vous voulez vérifier un critère spécifique. Les jalons placés avant le déploiement vers un environnement de préproduction appliquent les politiques, mais n'apparaissent pas dans le tableau de bord Deployment Risk.

1. Au cours d'une étape, cliquez sur l'icône **Configuration de l'étape** ![Icône de configuration d'étape de pipeline](images/pipeline-stage-configuration-icon.png), puis sur **Configurer l'étape**.
2. Cliquez sur **Ajouter un travail**. Pour le type de travail, sélectionnez **Tester**.
3. Pour le type de testeur, sélectionnez **{{site.data.keyword.DRA_short}} Gate**.
4. Indiquez le nom d'environnement. Assurez-vous que cette valeur correspond à celle définie dans vos [propriétés d'environnement](#toolchain_pipeline_props).
5. Entrez le nom de la politique à vérifier à ce jalon.

 Ce nom doit correspondre à l'un des noms de politique que vous avez définis. Vous ne pouvez indiquer que les politiques définies dans la même organisation {{site.data.keyword.Bluemix_notm}} que votre chaîne d'outils.

6. Facultatif : pour créer une fonction de jalon en mode recommandation, décochez la case **Arrêter d'exécuter cette étape si ce travail échoue**. En mode recommandation, {{site.data.keyword.DRA_short}} effectue la même analyse de politique au jalon et génère des rapports, mais en cas de panne, le pipeline n'est pas arrêté.
7. Cliquez sur **Sauvegarder** pour revenir au pipeline.
8. Configurez des jalons pour toutes vos politiques {{site.data.keyword.DRA_short}} en répétant ces étapes.

![Travail Mocha Deployment Risk](images/insights_gate_job.png)
*Figure 2. Jalon DevOps Insights*

Une fois que vous avez configuré le pipeline, commencez à utiliser {{site.data.keyword.DRA_short}}. 
