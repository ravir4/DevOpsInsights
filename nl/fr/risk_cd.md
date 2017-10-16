---

copyright:
  years: 2016, 2017
lastupdated: "2017-09-18"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Intégration de Deployment Risk Analytics à Continuous Delivery

Vous pouvez instrumenter des pipelines pour {{site.data.keyword.contdelivery_full}} afin d'utiliser les fonctions Deployment Risk Analysis de {{site.data.keyword.DRA_short}}. Ensuite, vous pouvez publier des données à partir de ces travaux et ajouter des jalons destinés à appliquer les politiques d'administration du risque. 

Pour voir une explication détaillée du composant Deployment Risk Analysis de {{site.data.keyword.DRA_short}}, voir [A propos de Deployment Risk](./about_risk.html).

Pour plus d'informations sur les pipelines de distribution continue, voir la [documentation officielle](../ContinuousDelivery/pipeline_working.html).

## Etapes et travaux de préparation du pipeline
{: #integrate_pipeline}

Pour commencer, vous devez instrumenter votre pipeline afin de communiquer avec {{site.data.keyword.DRA_short}}. Pour ce faire, définissez des variables d'environnement spécifiques pour tous vos travaux de pipeline permettant de générer, tester ou déployer du code. Vous devez également ajouter des variables d'environnement qui appliquent des politiques d'administration du risque en utilisant le type de testeur DevOps Insights Gate. 

* Enregistrements de génération
* Enregistrements de déploiement
* Résultats de test

Les résultats de test doivent fournir des données dans l'un des formats pris en charge suivants :

| Type de test                 | Formats pris en charge                                               |
|------------------------------|-----------------------------------------------------------------|
| Test de vérification fonctionnelle| Mocha, xUnit                                                    |
| Test d'unité                 | Mocha, xUnit, Karma/Mocha                                       |
| Couverture de code           | Istanbul, Blanket.js, Cobertura, lcov                                           |
| Analyse application statique | Analyses d'application statiques fournies par IBM Application Security on Cloud  |
| Analyse application dynamique| Analyses d'application dynamiques fournies par IBM Application Security on Cloud  |
| SonarQube                    | Données d'analyse fournies par les analyses SonarQube                             |

Les variables d'environnement que vous définissez dans le pipeline fournissent du contexte pour la publication de ces enregistrements. Vous pouvez les définir en utilisant la commande `export` dans les scripts de vos travaux. Vous pouvez également les définir dans le menu Propriétés d'environnement de chaque étape de pipeline. 

Variables d'environnement :

| Variable d'environnement | Objectif | Obligatoire dans |
|-----------|-------- |-------------|
| `LOGICAL_APP_NAME`  | Définit le nom de l'application sur le tableau de bord. | Tous les travaux permettant de générer, tester, déployer et appliquer des politiques d'administration du risque {{site.data.keyword.DRA_short}}. |
| `BUILD_PREFIX`  | Texte qui est ajouté comme préfixe aux générations d'étape. Ce texte apparaît également sur le tableau de bord.| Tous les travaux permettant de générer, tester, déployer et appliquer des politiques d'administration du risque {{site.data.keyword.DRA_short}}. |
| `LOGICAL_ENV_NAME`  | Environnement dans lequel l'application s'exécute. | Travaux de test et de déploiement. |

### Configuration de travaux de génération

Pour le dernier travail de génération d'une étape, définissez des variables d'environnement pour un nom d'application et un préfixe de génération. Un exemple de script doit inclure les commandes suivantes : 

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"
```

Lorsque ce travail de génération est terminé, le pipeline publie un message sur {{site.data.keyword.DRA_short}} indiquant qu'une génération SampleApp est terminée. 

### Configuration des travaux de déploiement

Pour le dernier travail de déploiement de l'étape, définissez un nom d'application, un préfixe de génération et un nom d'environnement. Un exemple de script doit inclure les commandes suivantes : 

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"
export LOGICAL_ENV_NAME="Production"
```

Lorsque votre travail de déploiement est terminé, le pipeline publie un message sur {{site.data.keyword.DRA_short}} indiquant que la génération et l'application spécifiées ont été déployées sur un environnement. 

### Configuration des travaux de test

Pour tous les travaux qui produisent des résultats de test, définissez un nom d'application et un préfixe de génération. 

Si le travail génère des résultats de test de vérification fonctionnelle, vous devez également indiquer comme nom d'environnement logique l'emplacement sur lequel ces tests se déroulent. 

Un exemple de script doit inclure les commandes suivantes : 

```
export LOGICAL_APP_NAME="SampleApp"
export BUILD_PREFIX="master"
# The LOGICAL_ENV_NAME variable is only needed when publishing FVT results.
export LOGICAL_ENV_NAME="Production"
```

Vérifiez que les noms d'application et les environnements correspondent chaque fois que cela est nécessaire. Par exemple, vous souhaiterez qu'un travail de test de production exécuté sur un déploiement de production comporte des valeurs `LOGICAL_ENV_NAME` identiques. 

## Publication de données de test sur DevOps Insights
{: #configure_pipeline_jobs}

{{site.data.keyword.DRA_short}} utilise les résultats de test à partir de vos travaux pour générer des rapports et appliquer des politiques d'administration du risque. Vous pouvez publier des données de test à partir de tous les types de travail. 

Vous pouvez publier des résultats de test de deux façons :

* En appelant une interface de ligne de commande simple dans le script d'un travail.

* En ajoutant un travail de test avec le type Advanced Tester à votre pipeline.

Lorsque vous utilisez la méthode Advanced Tester, vous ne publiez pas les résultats à l'aide de l'interface de ligne de commande. A la place, vous spécifiez l'emplacement des fichiers de résultats dans le travail de pipeline, et le travail télécharge les résultats dès qu'ils sont disponibles. 

Quelle que soit la méthode de publication que vous utilisez, les résultats de test doivent être dans l'un des formats pris en charge par {{site.data.keyword.DRA_short}} :

<table><thead>
<tr>
<th>Type de test</th>
<th>Formats pris en charge</th>
</tr>
</thead><tbody>
<tr>
<td>Test de vérification fonctionnelle</td>
<td>Mocha, xUnit</td>
</tr>
<tr>
<td>Test d'unité</td>
<td>Mocha, xUnit, Karma/Mocha</td>
</tr>
<tr>
<td>Couverture de code</td>
<td>Istanbul, Blanket.js</td>
</tr>
</tbody></table>

### Publication de données de test à partir de n'importe quel type de travail

Dans un pipeline, vous pouvez utiliser n'importe quel type de travail pour exécuter un test. Après avoir exécuté ce test, vous pouvez télécharger ses résultats sur {{site.data.keyword.DRA_short}}. Vous téléchargez les résultats en appelant une interface de ligne de commande dans le script shell du travail.  

Vous pouvez télécharger ces types de résultats de test à partir de l'interface de ligne de commande :

* Tests d'unité
* Couverture de code
* Tests de vérification fonctionnelle
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

Pour en savoir plus sur la commande `idra`, voir la [page sur le package grunt-idra3 sur npm](https://www.npmjs.com/package/grunt-idra3). 

### Publication de données de test à partir de travaux Advanced Tester

Vous pouvez ajouter des travaux de test avec le type Advanced Tester à un pipeline. Une fois exécutés, ils téléchargent automatiquement leurs résultats sur {{site.data.keyword.DRA_short}}. 

1. A l'étape au cours de laquelle vous souhaitez ajouter le travail qui télécharge les résultats, cliquez sur l'icône **Configuration de l'étape** ![Icône de configuration de l'étape de pipeline](images/pipeline-stage-configuration-icon.png). Cliquez sur **Configurer l'étape**.
2. Créez un travail de test et entrez un nom associé. 
3. Pour le type de travail, sélectionnez **Advanced Tester**.
4. Renseignez les zones **Commande de test** et **Répertoire de travail** comme vous le feriez pour un travail de test de pipeline normal. 
5. Renseignez les autres zones afin de télécharger les résultats de test pour un type de test particulier. 

 1. Choisissez le type de mesure qui correspond à ce que vous avez défini dans la politique {{site.data.keyword.DRA_short}} que vous voulez utiliser.
 2. Indiquez l'emplacement du fichier de résultats. Cet emplacement est relatif par rapport au répertoire de travail. 

6. Si vous souhaitez télécharger les résultats d'un second type de test du même travail, renseignez les zones qui ont pour préfixe *Additional*.
7. Cliquez sur **Sauvegarder** pour revenir au pipeline.

La figure 1 représente un travail de test configuré pour exécuter des tests d'unité, télécharger les résultats au format Mocha et télécharger les résultats de couverture de code au format Istanbul.

![Travail de téléchargement DevOps Insights](images/insights_upload_job.png)
*Figure 1. Téléchargement des résultats dans DevOps Insights*



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
