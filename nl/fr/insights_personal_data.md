---

copyright:
  years: 2018
lastupdated: "2018-4-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Gestion des données personnelles dans DevOps Insights
{: insights_personal_data}

Vous pouvez supprimer des données personnelles qui sont collectées et stockées dans {{site.data.keyword.DRA_full}}.
{: shortdesc}

Les données stockées dans {{site.data.keyword.DRA_short}} sont indexées par l'ID de chaîne d'outils. Quand vous supprimez une chaîne d'outils, toutes les données qui sont liées au référentiel collecté en tant qu'élément de la chaîne d'outils sont supprimées.

## Suppression de données depuis {{site.data.keyword.DRA_short}}
{: #insights_delete_data}

Le tableau suivant répertorie les scénarios de suppression des données depuis {{site.data.keyword.DRA_short}} et décrit leur impact sur chacune des catégories {{site.data.keyword.DRA_short}}.

|  | Developer et Team Insights | Deployment Risk | Security Insights |
|---------|-------------|-------------|-------------|
| [Suppression d'un référentiel![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](/docs/services/ContinuousDelivery/cd_personal_data.html#managing_grit_data){: new_window} |	Toutes les données liées au référentiel sont supprimées. | N/A | N/A |
| [Suppression d'un outil d'intégration {{site.data.keyword.DRA_short}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](/docs/services/ContinuousDelivery/cd_personal_data.html#managing_toolchains){: new_window} |	Toutes les données liées au référentiel sont supprimées. | Toutes les données qui sont associées à la chaîne d'outils dont fait partie l'intégration d'outils sont supprimées. | Toutes les données liées au référentiel et associées à la chaîne d'outils dont fait partie l'intégration d'outils sont supprimées. |
| [Suppression d'une chaîne d'outils![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](/docs/services/ContinuousDelivery/cd_personal_data.html#managing_toolchains){: new_window} | Toutes les données liées au référentiel et associées à la chaîne d'outils sont supprimées. | Toutes les données associées à la chaîne d'outils sont supprimées. | Toutes les données associées à la chaîne d'outils sont supprimées. |
| [Suppression d'un pipeline![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](/docs/services/ContinuousDelivery/cd_personal_data.html#managing_pipeline_data){: new_window} | N/A | N/A | N/A |
{:caption="Tableau 1. Scénarios de suppression des données" caption-side="top"}

## Suppression d'un outil d'intégration {{site.data.keyword.DRA_short}}
{: #insights_delete_integration}

Si vous supprimez une intégration d'outils de votre chaîne d'outils, la suppression est irréversible.

1. Dans le tableau de bord DevOps, dans la page **Chaînes d'outils**, cliquez sur une chaîne d'outils afin d'ouvrir la page Vue
d'ensemble correspondante. Vous pouvez également, depuis la page de présentation de l'application, sur la carte Distribution continue, cliquer sur **Afficher la chaîne d'outils**, puis sur **Présentation**.
1. Sur la carte associée à l'intégration d'outils {{site.data.keyword.DRA_short}}, cliquez sur le menu pour accéder aux options de configuration.
1. Pour supprimer l'intégration d'outils de votre chaîne d'outils, cliquez sur **Supprimer**.

  ![Menu de configuration](images/delete_insights_integration.png)

1. Confirmez en cliquant sur **Supprimer**. 
