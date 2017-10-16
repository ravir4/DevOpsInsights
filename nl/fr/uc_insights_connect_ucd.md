---

copyright:
  years: 2017

lastupdated: "2017-07-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Affichage des données des serveurs IBM UrbanCode Deploy
{: #connect_ucd}

Pour afficher les données d'un serveur IBM UrbanCode Deploy dans Delivery Insights, vous devez configurer une instance de DevOps Connect, installer un correctif sur le serveur, puis connecter ce serveur à DevOps Connect.
{:shortdesc}

## Prérequis
{: #prereqs}

Pour afficher des informations provenant de vos serveurs IBM UrbanCode Deploy dans {{site.data.keyword.DRA_short}}, vous devez héberger une instance de DevOps Connect sur un système qui peut se connecter à vos serveurs IBM UrbanCode Deploy. Ce système peut être un ordinateur physique ou une machine virtuelle. 

Le système qui héberge DevOps Connect doit satisfaire les conditions requises suivantes :
- Le système doit disposer d'un environnement JRE (Java Runtime Environment) version 8 ou ultérieure.
- La variable `PATH` du système doit inclure l'emplacement du JRE.
- Le système doit autoriser DevOps Connect à créer des connexions sortantes vers IBM Bluemix.

Votre serveur IBM UrbanCode Deploy doit également être à la version 6.2 ou ultérieure.

## Configuration du service {{site.data.keyword.DRA_short}}
{: #configure_service}

Si vous ne disposez pas du service {{site.data.keyword.DRA_short}}, ajoutez-le :
1. Connectez-vous à {{site.data.keyword.Bluemix}} et cliquez sur **Services > Tableau de bord**.
1. Cliquez sur **Créez un service**.
1. Cliquez sur le service {{site.data.keyword.DRA_short}}.
1. Sélectionnez un plan de tarification, puis cliquez sur **Créer**.
1. Cliquez sur **Gérer**, puis, sous "Obtenez des analyses sur les déploiements effectués par UrbanCode", cliquez sur **Commencez ici**.
1. Dans la fenêtre de modèle de chaîne d'outils, cliquez sur **Créer**.  
Delivery Insights crée une chaîne d'outils pour votre organisation. Les chaînes d'outils sont des collections d'intégrations d'outil et, dans ce cas, IBM UrbanCode Deploy et {{site.data.keyword.DRA_short}} font partie de votre chaîne d'outils. Pour plus d'informations sur les chaînes d'outils, voir [Utilisation des chaînes d'outils](../ContinuousDelivery/toolchains_working.html).
1. Dans la chaîne d'outils, cliquez sur l'outil IBM UrbanCode Deploy.
1. Cliquez sur le bouton de paramètres, puis sur **Configuration**.

A partir de maintenant, vous pourrez accéder à {{site.data.keyword.DRA_short}} en cliquant sur **Services > Tableau de bord** et en cliquant sur l'instance du service {{site.data.keyword.DRA_short}}. 

Si vous disposez déjà d'une chaîne d'outils, vous pouvez y ajouter les outils IBM UrbanCode Deploy et {{site.data.keyword.DRA_short}} et accéder à Delivery Insights via ces derniers. Cliquez ensuite sur l'outil IBM UrbanCode Deploy, cliquez sur le bouton de paramètres, puis sur **Configuration**.

A présent, vous pouvez suivre les instructions de la page **Instructions de configuration** pour installer DevOps Connect et le connecter à {{site.data.keyword.DRA_short}}, comme indiqué dans la section qui suit. 

## Installation de DevOps Connect et connexion à {{site.data.keyword.DRA_short}}
{: #install_connect}

1. Sur la page **Instructions de configuration**, suivez la procédure pour configurer DevOps Connect et connectez vos serveurs IBM UrbanCode Deploy. Procédez comme suit :
{: #set_up_connect}
  1. Configurez un système pour exécuter DevOps Connect, comme décrit dans [Prérequis](uc_insights_connect_ucd.html#prereqs).
  1. Téléchargez DevOps Connect, qui est fourni sous la forme d'un fichier JAR exécutable.

  1. Si vous utilisez un proxy pour vous connecter à Internet, affectez la valeur suivante à la variable système `_JAVA_OPTIONS` :
    * Si le proxy utilise HTTPS, affectez à `_JAVA_OPTIONS` la valeur `-Dhttps.proxyHost=HOSTNAME -Dhttps.proxyPort=PORT`, où `HOSTNAME` est le nom d'hôte du serveur proxy et `PORT` est le port HTTPS du serveur proxy. 
    * Si le proxy utilise HTTP, affectez à `_JAVA_OPTIONS` la valeur `-Dhttp.proxyHost=HOSTNAME -Dhttp.proxyPort=PORT`, où `HOSTNAME` est le nom d'hôte du serveur proxy et `PORT` est le port HTTP du serveur proxy. 

  1. Copiez la commande à partir de la page **Instructions de configuration**. Cette commande démarre DevOps Connect avec un jeton qui l'autorise à se connecter à votre organisation sur {{site.data.keyword.Bluemix}}.
  1. DevOps Connect s'exécute par défaut sur le port 8443, tout comme le serveur IBM UrbanCode Deploy. Par conséquent, si le serveur IBM UrbanCode Deploy ou n'importe quel autre service s'exécute sur le port 844s, modifiez le port pour DevOps Connect en ajoutant le paramètre `-Dserver.port` à la commande. Par exemple, pour configurer DevOps Connect afin qu'il utilise le port 8888, vous devez faire débuter la commande comme illustré ci-dessous :  
```bash
java -Dserver.port=8888 -jar devops-connect-2.0.92clear0618.jar -Dserver.port=8888
```  

La commande complète contient des informations relatives à votre compte Bluemix, et configure DevOps Connect automatiquement, comme dans l'exemple suivant :

```bash
java -Dserver.port=8888 -jar devops-connect-2.0.920618.jar --sync.id=a2c12cb9-9a09-9832-479b01bf --sync.token=j0zs325U6qp080pzpcQ  --sync.registrar=jsmith@example.com
```

  1. Exécutez la commande et attendez le démarrage de DevOps Connect. 

  1. Connectez vos serveurs IBM UrbanCode Deploy à DevOps Connect, comme indiqué dans la section suivante.

## Connexion des serveurs IBM UrbanCode Deploy à DevOps Connect
{: #connect_ucd_to_connect}

1. Si la version de votre serveur IBM UrbanCode Deploy est antérieure à la version 6.2.5, installez un correctif sur le serveur. Les versions 6.2.5 et ultérieures ne nécessitent pas de correctif.
  1. Téléchargez le correctif adapté à votre version d'IBM UrbanCode Deploy depuis la page suivante. Par exemple, le fichier correctif pour IBM UrbanCode Deploy 6.2.4.x s'appelle [ucd-6.2.4.0-WI161775-Devops-Insights-Patch.jar](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/6_2_4_X/ucd-6.2.4.0-WI161775-Devops-Insights-Patch.jar).  
  
    [http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/)

  1. Arrêtez le serveur. Voir [Démarrage et arrêt du serveur](https://www.ibm.com/support/knowledgecenter/SS4GSP_6.2.5/com.ibm.udeploy.install.doc/topics/run_server.html).

  1. Placez les fichiers correctifs dans le dossier <code><em>application_data</em>/patches</code>, où <code><em>application_data</em></code> est le dossier des données d'application. Le dossier des données d'application par défaut est `/opt/ibm-ucd/server/appdata` sur Linux et `C:\Program Files\ibm-ucd\server\appdata` sous Windows. Sur les systèmes à haute disponibilité, le dossier des données d'application se trouve toujours sur une unité réseau partagée à laquelle chaque serveur peut accéder.

  1. Facultatif : lorsque le serveur est arrêté, si vous souhaitez augmenter les performances de l'importation de données à partir de ce serveur, exécutez les commandes SQL suivantes sur la base de données. Ces commandes ne sont pas nécessaires sur la version 6.2.5 et sur les versions ultérieures.   
  `create index rt_cpr_submitted_time on MyUCDDatabase.rt_app_process_request(submitted_time);`  
  `create index rt_cpr_submitted_time on MyUCDDatabase.rt_comp_process_request(component_id, submitted_time);`  
  Indiquez le nom de votre base de données pour `MyUCDDatabase`.
  <!-- Ross says that this will not be necessary for versions 6.2.4.1 and later if he gets his code changes in. -->

  1. Démarrez le serveur. 

    **Remarque :** Le démarrage du serveur IBM UrbanCode Deploy risque de prendre plus de temps que d'habitude. S'il ne démarre pas, ou s'il ne fonctionne pas normalement, supprimez les fichiers correctifs et redémarrez-le. Les fichiers correctifs n'affectent pas le serveur de manière définitive.

1. Certaines versions d'IBM UrbanCode Deploy requièrent un correctif supplémentaire pour que le serveur puisse se connecter à DevOps Connect. Si vous utilisez IBM UrbanCode Deploy versions 6.2 à 6.2.1.2, vous devez installer le correctif supplémentaire suivant sur le serveur :
  1. Téléchargez le correctif : [http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/ucd-6.2.1.1-WI149200-CLI-Updates-for-UCSync.jar](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/ucd-6.2.1.1-WI149200-CLI-Updates-for-UCSync.jar).
  1. Arrêtez le serveur.
  1. Placez le fichier correctif dans le dossier <code><em>application_data</em>/patches</code>.
  1. Démarrez le serveur.

1. Créez une intégration entre DevOps Connect et le serveur IBM UrbanCode Deploy :  

  **Important :** Lors de la première exécution de l'intégration, DevOps Connect extrait les données des 90 jours précédents. Si vous disposez d'un grand volume de données de déploiement, ce processus peut durer longtemps. Pour extraire les données sur une durée inférieure à 90 jours, voir [Traitement des incidents](uc_insights_connect_ucd.html#troubleshooting).
  1. Dans IBM UrbanCode Deploy, créez un jeton d'authentification. Voir [Jetons](https://www.ibm.com/support/knowledgecenter/SS4GSP_6.2.5/com.ibm.udeploy.admin.doc/topics/security_token.html).
  1. Dans DevOps Connect, cliquez sur **Integrations**, puis sur **Add New**.
  1. Indiquez un nom et une description pour l'intégration. L'emplacement par défaut de DevOps Connect est `https://hostname:8443/`, où `hostname` est le nom d'hôte du système qui héberge DevOps Connect.
  1. Dans la liste **Integration Type**, sélectionnez **IBM UrbanCode Deploy for Cloud Reporting**.
  1. Dans la zone **Server URI**, entrez l'URL publique du serveur IBM UrbanCode Deploy, par exemple `https://my_UCD.example.com:8447`.
  1. Dans la zone **Authentication Token**, entrez ou collez le jeton d'authentification généré par IBM UrbanCode Deploy.
  1. Dans la zone **Admin User**, entrez une liste d'IBMid séparés par des virgules pour donner accès à l'interface DevOps Connect.
  1. Facultatif : cliquez sur **Run Integration** pour exécuter l'intégration immédiatement. Par défaut, les intégrations s'exécutent toutes les minutes.
  1. Cliquez sur **Save**.

  ![Configuration de l'intégration dans DevOps Connect](images/uc_insights_dc_integration.gif)

Vos données sont maintenant synchronisées avec Delivery Insights. Vous pouvez désormais créer et afficher des rapports qui reposent sur ces données. Mappez ensuite les environnements de vos serveurs IBM UrbanCode Deploy à des environnements logiques dans Delivery Insights.

## Mappage d'environnements à des rapports
{: #mapping}

### Environnements logiques

Delivery Insights regroupe vos environnements IBM UrbanCode Deploy (également appelés *environnements physiques*) en un ou plusieurs environnements logiques. Vous pouvez ainsi collecter des environnements en groupes qui sont pertinents pour vous et votre organisation. Par exemple, si vous disposez de plusieurs environnements de production pour plusieurs applications, vous pouvez regrouper tous ces environnements en un seul environnement logique et combiner les mesures de tous ces environnements en un seul tableau de bord d'environnement de production. Le mappage s'effectue par chaîne de recherche. Vous pouvez donc regrouper les environnements comme vous le souhaitez en fonction de vos serveurs IBM UrbanCode Deploy.

### Environnements logiques par défaut

Par défaut, vos rapports incluent des environnements logiques qui correspondent aux environnements IBM UrbanCode Deploy grâce à des chaînes. Par exemple, tous les environnements dont le nom comporte "dev" sont mappés à l'environnement logique DEV, et tous les environnements dont le nom inclut "prod" sont mappés à l'environnement logique PROD.

![Environnements logiques par défaut](images/uc_insights_mapping.gif)

### Mappage des environnements à des environnements logiques

Vous pouvez mapper manuellement des environnements physiques à des environnements logiques, ou vous pouvez utiliser des masques pour associer dynamiquement des environnements physiques à des environnements logiques.

Pour mapper des environnements physiques à des environnements logiques, procédez comme suit :

1. Ouvrez Delivery Insights, cliquez sur le bouton de paramètres, puis sur **Mapper des environnements**.
1. Sur la page Mappage d'environnement, cliquez sur un environnement logique existant ou créez un environnement logique en cliquant sur **Ajouter un environnement logique**.
1. Avec un environnement logique sélectionné, vous pouvez spécifier des masques pour mapper des environnements à cet environnement logique. Sous **Masques inclus**, cliquez sur **Ajouter un masque** et spécifiez un masque à utiliser. Tous les environnements dont les noms correspondent au masque, y compris les environnements que vous créerez ultérieurement, sont ajoutés à l'environnement logique. Vous pouvez utiliser l'astérisque (*) comme caractère générique. Par exemple, le masque `env` correspond aux environnements `env1`, `env2` et `env`.
1. Pour mapper manuellement des environnements à des environnements logiques, cliquez sur **Add Manually** et sélectionnez les environnements à ajouter ou à retirer.
1. Vérifiez que l'environnement logique contient les environnements que vous souhaitez.

![Configuration du mappage d'environnement logique](images/uc_insights_mapping_manually.gif)

Maintenant que vous avez mappé des environnements à des environnements logiques, vous pouvez agréger les informations des rapports en fonction de ces environnements logiques.

## Mappage d'applications à des secteurs d'activité
{: #lines}

Les secteurs d'activité sont des groupes d'applications dédiés à un usage professionnel commun. Vous pouvez mapper des applications à des secteurs d'activité afin de faciliter le filtrage des applications dans des graphiques. Vous pouvez aussi créer des graphiques basés sur des secteurs d'activité. 

Pour configurer des secteurs d'activité, (éléments LOB), procédez comme suit :

1. Dans {{site.data.keyword.DRA_short}}, cliquez successivement sur **Delivery Insights**, sur le bouton de paramètres, puis sur **Mapper des secteurs d'activité**.
1. Sur la page Mappage de secteurs d'activité, cliquez sur un élément LOB existant ou créez un élément LOB en tapant un nom et en cliquant sur **Créer**.
1. Avec un élément LOB sélectionné, vous pouvez spécifier des masques pour mapper des applications à cet élément LOB. Sous **Masques inclus**, cliquez sur **Ajouter un masque** et spécifiez un masque à utiliser. Toutes les applications dont les noms correspondent au masque, y compris les applications que vous créerez ultérieurement, sont ajoutées à l'élément LOB. Vous pouvez utiliser l'astérisque (*) comme caractère générique. Par exemple, le masque `env` correspond aux environnements `env1`, `env2` et `env`.
1. Vous pouvez aussi mapper des applications à l'élément LOB manuellement en cliquant sur **Applications mappées individuellement**, puis sur **Ajouter des applications**.

Après avoir configuré des éléments LOB, vous pouvez filtrer des graphiques afin d'afficher uniquement les applications contenues dans certains éléments LOB. Les autres graphiques présentent des métriques basées sur des éléments LOB. 

## Création de rapports

Pour créer un rapport, ouvrez {{site.data.keyword.DRA_short}}, cliquez sur **Delivery Insights**, puis sur **Ajouter un rapport**. Si vous ne voyez pas **Ajouter un rapport**, cela signifie que vos serveurs IBM UrbanCode Deploy ne sont pas connectés. Cliquez sur le bouton de paramètres, puis sur **Configuration** pour connecter vos serveurs.

Dans le rapport, vous pouvez ajouter des cartes dans la section **Metrics**, filtrer l'activité sous **Recent application activity** et ajouter des graphiques dans la section **Report Details**. Vous pouvez appliquer un filtre et une personnalisation individuelle à chaque graphique de la section **Report Details**. Pour afficher les données brutes derrière un graphique, cliquez sur le bouton des paramètres du graphique en haut à droite de ce dernier, puis cliquez sur **Report Data**.

Pour modifier l'ordre des graphiques, cliquez sur le bouton des paramètres en haut à droite de la page, puis cliquez sur **Edit Chart Layout**. Vous pouvez ensuite faire glisser et déposer les graphiques pour définir l'ordre du rapport.

## Partage de rapports
Par défaut, vous ne pouvez afficher que vos rapports Delivery Insights. Vous pouvez partager un rapport avec d'autres utilisateurs de votre organisation Bluemix. Pour ce faire, ouvrez le rapport et cliquez sur le bouton des paramètres situé en haut à droite de ce dernier, puis cliquez sur **Share**.  

![Partage d'un rapport](images/uc_insights_sharing.gif).

## Création de rapports d'audit

Les rapports d'audit affichent une liste complète de toutes les activités qui correspondent aux filtres que vous avez définis, sous forme de PDF. Pour créer un rapport d'audit, cliquez sur **Delivery Insights**, cliquez sur le bouton de paramètres, puis sur **Créer un rapport d'audit**. Indiquez ensuite les informations relatives au rapport, notamment un nom. Définissez également le contexte du rapport, par exemple, pour une application, un environnement logique ou un environnement sur un serveur IBM UrbanCode Deploy (un environnement physique). A partir de là, sélectionnez les données à afficher dans le rapport et cliquez sur **Create**. 

## Traitement des incidents
{: #troubleshooting}

Si de nombreuses demandes de processus de composant et d'application sont stockées dans votre base de données sur le serveur IBM UrbanCode Deploy, des erreurs sont susceptibles de se produire lors du processus d'extraction. Un message similaire au texte suivant est enregistré dans le journal de sortie du serveur :

`ORA-01652: unable to extend temp segment by 128 in tablespace TEMP`

Pour contourner ce comportement, éditez le fichier `plugin.properties` pour que le plug-in réduise la valeur du nombre de jours de données à extraire. Le fichier `plugin.properties` se trouve dans le répertoire `~/.ibm/cloud-sync/plugins/settings/reporting-ucd-plugin/` sur l'ordinateur sur lequel vous avez installé DevOps Connect. Editez la ligne suivante pour supprimer le signe dièse (#) et réduire le nombre de jours :

`#numDaysToRetrieve=90`

Par exemple, modifiez la ligne comme suit pour n'extraire les données que sur les 30 derniers jours :

`numDaysToRetrieve=30`

Sauvegardez le fichier, puis exécutez à nouveau l'intégration. Examinez les journaux du serveur pour vérifier que l'erreur ne se produit plus.
