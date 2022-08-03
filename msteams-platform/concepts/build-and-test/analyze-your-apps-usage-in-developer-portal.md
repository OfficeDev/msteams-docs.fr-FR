---
title: Analyser l’utilisation de votre application dans le portail des développeurs
description: Dans ce module, découvrez comment analyser l’utilisation de votre application dans le portail des développeurs
ms.localizationpriority: medium
ms.topic: overview
ms.author: surbhigupta
ms.openlocfilehash: 43758fdebd1f2e76318880a51d9173469b0ed604
ms.sourcegitcommit: 990a36fb774e614146444d4adaa2c9bcdb835998
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2022
ms.locfileid: "67232379"
---
# <a name="analyze-your-apps-usage-in-developer-portal"></a>Analyser l’utilisation de votre application dans le portail des développeurs

Dans le portail des développeurs pour Teams, dans la page **Vue d’ensemble** , vous pouvez voir le nombre total d’utilisateurs actifs pour votre application.

> [!NOTE]
> L’analytique de l’utilisation est actuellement disponible uniquement pour les nouvelles applications personnalisées publiées sur votre organisation via le **Portail des développeurs** pour Teams ou importées dans le **portail des développeurs** pour Teams après avril 2022. L’analyse de l’utilisation de toutes les applications publiées dans le magasin Teams est disponible dans **l’Espace partenaires** pour plus d’informations sur [le rapport d’utilisation des applications Teams](/office/dev/store/teams-apps-usage).

| Métrique | Définition |
| :-----------------------| :------------------------------------------------------------------------------------------------------|
| *R30 mensuel* | Métrique d’utilisation par défaut. Il affiche le nombre d’utilisateurs actifs uniques qui ont utilisé votre application dans cette fenêtre de 30 jours en UTC. |
| *Tous les jours* | Il affiche le nombre d’utilisateurs actifs uniques qui ont utilisé votre application au cours d’un jour donné en UTC. |

L’utilisation des applications pour un jour donné est reflétée dans les 24 à 48 heures, et les données d’utilisation des nouvelles applications peuvent prendre jusqu’à trois à cinq jours pour être reflétées dans les graphiques.

Vous pouvez afficher l’utilisation de votre application et d’autres insights à partir de la page **Analytics** . Pour accéder à la page :

1. Accédez au **[portail des développeurs pour Teams](https://dev.teams.microsoft.com)**.
1. Sélectionnez **Applications** dans le volet gauche.
1. Sélectionnez l’application requise dans la page **Applications** .
1. Sélectionnez **Analyse** sous **Vue d’ensemble** ou sélectionnez **Afficher les détails** sous la carte **Utilisateurs actifs (préversion** ).

 :::image type="content" source="../../assets/images/tdp/dev-app-portal.png" alt-text="Les captures d’écran vous montrent la page Analytique de votre application dans le portail des développeurs."lightbox="../../assets/images/tdp/dev-app-portal.png":::

Lorsque vous explorez des métriques individuelles sur cette page, vous pouvez utiliser le bouton **Filtrer** pour analyser l’utilisation de votre application à partir des options de filtre suivantes :

* Type d’agrégation : ce filtre vous permet de regrouper les métriques suivantes par un nombre d’utilisateurs distincts ou un nombre de locataires ou de clients distincts.
* Plateforme
* Système d’exploitation
* Zone

 :::image type="content" source="../../assets/images/tdp/dev-analytics-filter.png" alt-text="Les captures d’écran vous montrent le filtre de page d’analyse dans le portail des développeurs.":::

Une fois que vous avez sélectionné les filtres souhaités, vous pouvez explorer les widgets individuels suivants :

* [Utilisation par période](#usage-by-time-period)
* [Utilisation par plateforme et système d’exploitation](#usage-by-platform-and-os)
* [Utilisation par état de rétention](#usage-by-retention-state)
* [Intensité de l’utilisation](#usage-intensity)

## <a name="usage-by-time-period"></a>Utilisation par période

Le graphique **Utilisation par période** affiche le nombre d’utilisateurs ou de locataires actifs qui ont ouvert et utilisé votre application sur différentes périodes.

 :::image type="content" source="../../assets/images/tdp/usage-by-time-period.png" alt-text="Les captures d’écran vous montrent l’utilisation par graphique de période de temps pour votre application publiée.":::

| Métrique | Définition |
| :-----------------------| :------------------------------------------------------------------------------------------------------|
| R30 mensuel | Chaque point de données représente une période R30 donnée (30 jours propagés). |
| R28 mensuel | Chaque point de données représente une période R28 donnée (28 jours propagés). |
| R7 hebdomadaire| Chaque point de données représente une période R7 donnée (7 jours consécutifs). |
| En jours | Chaque point de données représente une période R1 donnée (1 jour propagé). |

## <a name="usage-by-platform-and-os"></a>Utilisation par plateforme et système d’exploitation

Le graphique **Utilisation par plateforme et système d’exploitation** montre l’utilisation active de votre application sur différents points de terminaison, tels que **Windows**, **Mac**, **iOS**, **Android** et **Web**. Le même utilisateur ou locataire peut utiliser une application sur plusieurs points de terminaison. Chaque point de données représente une période R30 donnée (30 jours propagés).

 :::image type="content" source="../../assets/images/tdp/usage-by-platform-OS.png" alt-text="Les captures d’écran vous montrent l’utilisation par plateforme et graphique du système d’exploitation pour votre application publiée.":::

## <a name="usage-by-retention-state"></a>Utilisation par état de rétention

Le graphique **Utilisation par état de rétention** vous permet de suivre quatre métriques de rétention ou d’attrition clés pour votre application au fil du temps.

:::image type="content" source="../../assets/images/tdp/usage-by-retention-state.png" alt-text="Les captures d’écran vous montrent l’utilisation par graphique d’état de rétention pour votre application publiée.":::

| Métrique | Définition |
| :-----------------------| :------------------------------------------------------------------------------------------------------|
| Nouveaux utilisateurs ou locataires | Utilisateurs ou locataires actifs qui sont nouveaux et n’ont pas utilisé votre application. |
| Retour d’utilisateurs ou de locataires | Utilisateurs ou locataires actifs qui ont utilisé votre application pendant une période R30 donnée (30 jours propagés) et la période R30 immédiatement précédente. |
| Utilisateurs ou locataires réactivés | Utilisateurs ou locataires actifs qui ont utilisé votre application une ou plusieurs fois avant, mais pas dans la période R30 immédiatement précédente. |
| Utilisateurs ou locataires non convertis | Utilisateurs ou locataires actifs qui n’ont pas été vus pendant une période R30 donnée, mais qui ont été vus au cours de la période R30 immédiatement précédente. |

## <a name="usage-intensity"></a>Intensité de l’utilisation

Le graphique **d’intensité d’utilisation** affiche les principales métriques d’intensité d’utilisation pour votre application.

 :::image type="content" source="../../assets/images/tdp/usage-intensity.png" alt-text="Les captures d’écran vous montrent le graphique d’intensité d’utilisation de votre application publiée.":::

| Métrique | Définition |
| :-----------------------| :------------------------------------------------------------------------------------------------------|
| Jours médians utilisés par mois | Nombre médian de jours pendant lesquels votre application a été ouverte au cours de la dernière période R30 (30 jours propagés). |
| % de l’utilisation de 5 jours et plus | % des utilisateurs actifs qui ont ouvert ou utilisé l’application plus de cinq jours au cours de la dernière période R30. |
| DAU/MAU | Ratio du nombre moyen d’utilisateurs ou de locataires uniques qui ont utilisé votre application chaque jour divisé par les utilisateurs actifs mensuels pour la période R30 sélectionnée. |

## <a name="app-dashboard"></a>Tableau de bord de l’application

Le tableau **de bord Mon application** affiche les données R30 les plus récentes (30 jours consécutifs) pour chacune des métriques des quatre catégories précédentes, ainsi que la modification du mois sur le mois. Utilisez le sélecteur d’heure en haut à gauche et sélectionnez la date souhaitée. Vous pouvez voir les données R30 quotidiennes pour les 75 derniers jours et les données R30 de fin de mois jusqu’à 12 mois.

Vous pouvez sélectionner chacun de ces **noms de métriques** pour afficher les tendances au fil du temps.

 :::image type="content" source="../../assets/images/tdp/app-dashboard.png" alt-text="Les captures d’écran montrent le graphique du tableau de bord De l’application pour votre application publiée.":::

## <a name="see-also"></a>Voir aussi

[Inclure une offre SaaS avec votre application Microsoft Teams](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md)
