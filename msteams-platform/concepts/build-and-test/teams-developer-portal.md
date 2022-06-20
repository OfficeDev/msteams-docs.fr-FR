---
title: Gérer vos applications avec le Developer Portal
description: Dans ce module, découvrez comment configurer, distribuer et gérer vos applications à l’aide du portail des développeurs pour Microsoft Teams.
ms.localizationpriority: medium
ms.topic: overview
ms.author: surbhigupta
ms.openlocfilehash: 391d6c671bf7c34a734eed3202df50ebdc4f9eae
ms.sourcegitcommit: e429131d01df7103a467df2c42cdfe41ab822b10
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/20/2022
ms.locfileid: "66164240"
---
# <a name="manage-your-teams-apps-using-developer-portal"></a>Gérer vos applications Teams à l’aide du portail des développeurs

<a href="https://dev.teams.microsoft.com" target="_blank">Portail des développeurs pour Teams</a> est l’outil principal pour configurer, distribuer et gérer vos applications Microsoft Teams. Avec le Developer Portal, vous pouvez collaborer avec des collègues sur votre application, configurer des environnements d’exécution et bien plus encore.

:::image type="content" source="../../assets/images/tdp/tdp_home_1.png" alt-text="capture d’écran montrant la page d’accueil du Developer Portal pour Teams.":::

> [!NOTE]
>
> * Actuellement, Developer Portal n’est pas disponible pour les locataires Cloud de la communauté du secteur public (GCC), GCC-High ou department of Defense (DOD).
> * Toutefois, vous pouvez utiliser un locataire standard pour créer une application dans le Developer Portal, télécharger l’application et charger l’application à l’aide de [Microsoft Graph](/graph/api/teamsapp-publish?view=graph-rest-1.0&tabs=http&preserve-view=true) dans un cloud national. Pour plus d’informations, consultez [Déploiements cloud nationaux](/graph/deployments).

> [!IMPORTANT]
> Si vous effectuez une migration d’App Studio vers le portail des développeurs, le tableau suivant fournit les informations détaillées sur les fonctionnalités prises en charge dans le portail des développeurs :

| Fonctionnalités | App Studio | Portail des développeurs |
| --- | --- | --- |
| Analyse des applications* | ❌ | ✔️ |
| Fonctionnalités de l’application - Bots | ✔️ | ✔️ |
| Fonctionnalités de l’application - Connecteurs | ✔️ | ✔️ |
| Fonctionnalités de l’application - Extension de messagerie | ✔️ | ✔️ |
| Fonctionnalités de l’application - Extension réunion | ❌ | ✔️ |
| Fonctionnalités de l’application - Applications personnelles | ✔️ | ✔️ |
| Fonctionnalités de l’application - Onglets | ✔️ | ✔️ |
| Environnements d’application | ❌ | ✔️ |
| Langues de l’application | ✔️ | ✔️ |
| Aperçu et téléchargement du manifeste d’application | ✔️ | ✔️ |
| Plans d’application et tarification | ❌ | ✔️ |
| Publication d’applications | ✔️ | ✔️ |
| Autorisations d’application | ❌ | ✔️ |
| Partage d’applications avec les co-développeurs | ❌ | ✔️ |
| Validation d’application | ✔️ | ✔️ |
| Créer une application | ✔️ | ✔️ |
| Transmettre un package zip | ✔️ | ✔️ |

\**L’analytique des applications sera bientôt disponible en disponibilité générale.*

## <a name="register-an-app"></a>Inscrire une application

Le Developer Portal fournit deux façons d’inscrire une application Teams :

* Inscrivez une toute nouvelle application.
* Importez un package d’application existant.

> [!NOTE]
> Si vous créez une application à l’aide du kit de ressources [Microsoft Teams pour Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension), vous pouvez gérer cette application dans le Developer Portal.

## <a name="set-up-an-environment"></a>Configurer un environnement

Vous pouvez configurer des environnements et des variables globales pour faciliter la transition de votre application de votre runtime local vers la production. Les variables globales sont utilisées dans tous les environnements.

Pour configurer un environnement :

1. Dans le Developer Portal, sélectionnez l’application sur laquelle vous travaillez.
2. Accédez à la page **environnements** et sélectionnez **+ Ajouter un environnement**.
3. Sélectionnez **+ Ajouter une variable** pour créer des variables de configuration pour votre environnement.

Pour utiliser des variables :

Utilisez les noms de variables au lieu de valeurs codées en dur pour définir les configurations de votre application.

1. Entrez `{{` dans n’importe quel champ du Developer Portal. Une liste déroulante contenant toutes les variables que vous avez créées pour l’environnement choisi ainsi que les variables globales s’affiche.  
1. Avant de télécharger votre package d’application (par exemple, lors de la préparation de la publication dans le Magasin Teams), sélectionnez l’environnement que vous souhaitez utiliser. Les configurations de votre application sont mises à jour automatiquement en fonction de l’environnement.

## <a name="identify-app-owners"></a>Identifier les propriétaires d’applications

Chaque application comprend une page **Propriétaires**, où vous pouvez partager l'enregistrement de votre application avec des collègues de votre organisation. Le rôle de **contributeur** dispose des mêmes autorisations que le rôle de **propriétaire**, à l'exception de la possibilité de supprimer une application.

## <a name="configure-your-apps-capabilities-and-other-important-metadata"></a>Configurer les fonctionnalités de votre application et d’autres métadonnées importantes

Une application Teams est une application web. Comme toutes les applications web, son code source est généralement développé dans un éditeur de code ou IDE et hébergé quelque part dans le cloud (comme Azure).

Pour installer et afficher votre application dans Teams, vous devez inclure un ensemble de configurations que Teams reconnaît. Pour ce faire, vous devez généralement créer un manifeste d’application, un fichier JSON qui contient toutes les métadonnées dont Teams a besoin pour afficher le contenu de votre application. Le Developer Portal résume ce processus et inclut de nouvelles fonctionnalités et outils pour vous aider à réussir.

## <a name="test-your-app-directly-in-teams"></a>Tester votre application directement dans Teams

Le Developer Portal fournit des options pour tester et déboguer votre application :

* Dans la page **Vue d’ensemble** , vous pouvez voir un instantané indiquant si les configurations de votre application sont validées par rapport aux cas de test du Magasin Teams.
* Le bouton **Aperçu dans Teams** vous permet de lancer rapidement votre application dans le client Teams pour le débogage.

## <a name="distribute-your-app"></a>Distribuer votre application.

À partir du Developer Portal, utilisez le bouton **Distribuer** pour télécharger un package d’application, publier sur votre organisation ou publier dans le magasin Teams.

Pour plus d’informations, consultez [distribuer votre application Teams](~/concepts/deploy-and-publish/apps-publish-overview.md).

## <a name="analyze-your-apps-usage"></a>Analyser l’utilisation de votre application

Dans le portail des développeurs pour Teams, dans la page **Vue d’ensemble**, vous pouvez voir le nombre total d’utilisateurs actifs pour votre application.

> [!NOTE]
> L’analytique de l’utilisation est actuellement disponible uniquement pour les nouvelles applications personnalisées publiées sur votre organisation via **le portail** des développeurs pour Teams (anciennement App Studio) ou importées dans le **portail** des développeurs pour Teams après avril 2022. L’analyse de l’utilisation de toutes les applications publiées dans le magasin Teams est disponible dans **l’Espace partenaires**, pour plus d’informations [Teams rapport d’utilisation des applications](/office/dev/store/teams-apps-usage).

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

 :::image type="content" source="../../assets/images/tdp/dev-app-portal.PNG" alt-text="dev-Portal-analytics"lightbox="../../assets/images/tdp/dev-app-portal.PNG":::

Lorsque vous explorez des métriques individuelles sur cette page, vous pouvez utiliser le bouton **Filtrer** pour analyser l’utilisation de votre application à partir des options de filtre suivantes :

* Type d’agrégation : ce filtre vous permet de regrouper les métriques suivantes par un nombre d’utilisateurs distincts ou un nombre de locataires ou de clients distincts.
* Plateforme
* Système d’exploitation
* Zone

 :::image type="content" source="../../assets/images/tdp/dev-analytics-filter.PNG" alt-text="Filtre":::

Une fois que vous avez sélectionné les filtres souhaités, vous pouvez explorer les widgets individuels suivants :

* [Utilisation par période](#usage-by-time-period)
* [Utilisation par plateforme et système d’exploitation](#usage-by-platform-and-os)
* [Utilisation par état de rétention](#usage-by-retention-state)
* [Intensité de l’utilisation](#usage-intensity)

### <a name="usage-by-time-period"></a>Utilisation par période

Le graphique **Utilisation par période** affiche le nombre d’utilisateurs ou de locataires actifs qui ont ouvert et utilisé votre application sur différentes périodes.

 :::image type="content" source="../../assets/images/tdp/usage-by-time-period.png" alt-text="Period":::

| Métrique | Définition |
| :-----------------------| :------------------------------------------------------------------------------------------------------|
| R30 mensuel | Chaque point de données représente une période R30 donnée (30 jours propagés). |
| R28 mensuel | Chaque point de données représente une période R28 donnée (28 jours propagés). |
| R7 hebdomadaire| Chaque point de données représente une période R7 donnée (7 jours consécutifs). |
| Journalière | Chaque point de données représente une période R1 donnée (1 jour propagé). |

### <a name="usage-by-platform-and-os"></a>Utilisation par plateforme et système d’exploitation

Le graphique **Utilisation par plateforme et système d’exploitation** montre l’utilisation active de votre application sur différents points de terminaison, tels que **Windows**, **Mac**, **iOS**, **Android** et **Web**. Le même utilisateur ou locataire peut utiliser une application sur plusieurs points de terminaison. Chaque point de données représente une période R30 donnée (30 jours propagés).

 :::image type="content" source="../../assets/images/tdp/usage-by-platform-OS.png" alt-text="Plateforme":::

### <a name="usage-by-retention-state"></a>Utilisation par état de rétention

Le graphique **Utilisation par état de rétention** vous permet de suivre quatre métriques de rétention ou d’attrition clés pour votre application au fil du temps.

:::image type="content" source="../../assets/images/tdp/usage-by-retention-state.png" alt-text="Retention":::

| Métrique | Définition |
| :-----------------------| :------------------------------------------------------------------------------------------------------|
| Nouveaux utilisateurs ou locataires | Utilisateurs ou locataires actifs qui sont nouveaux et n’ont pas utilisé votre application. |
| Retour d’utilisateurs ou de locataires | Utilisateurs ou locataires actifs qui ont utilisé votre application pendant une période R30 donnée (30 jours propagés) et la période R30 immédiatement précédente. |
| Utilisateurs ou locataires réactivés | Utilisateurs ou locataires actifs qui ont utilisé votre application une ou plusieurs fois avant, mais pas dans la période R30 immédiatement précédente. |
| Utilisateurs ou locataires non convertis | Utilisateurs ou locataires actifs qui n’ont pas été vus pendant une période R30 donnée, mais qui ont été vus au cours de la période R30 immédiatement précédente. |

### <a name="usage-intensity"></a>Intensité de l’utilisation

Le graphique **d’intensité d’utilisation** affiche les principales métriques d’intensité d’utilisation pour votre application.

 :::image type="content" source="../../assets/images/tdp/usage-intensity.png" alt-text="Intensité":::

| Métrique | Définition |
| :-----------------------| :------------------------------------------------------------------------------------------------------|
| Jours médians utilisés par mois | Nombre médian de jours pendant lesquels votre application a été ouverte au cours de la dernière période R30 (30 jours propagés). |
| % de l’utilisation de 5 jours et plus | % des utilisateurs actifs qui ont ouvert ou utilisé l’application plus de cinq jours au cours de la dernière période R30. |
| DAU/MAU | Ratio du nombre moyen d’utilisateurs ou de locataires uniques qui ont utilisé votre application chaque jour divisé par les utilisateurs actifs mensuels pour la période R30 sélectionnée. |

### <a name="app-dashboard"></a>Tableau de bord de l’application

Le tableau **de bord Mon application** affiche les données R30 les plus récentes (30 jours consécutifs) pour chacune des métriques des quatre catégories précédentes, ainsi que la modification du mois sur le mois. Utilisez le sélecteur d’heure en haut à gauche et sélectionnez la date souhaitée. Vous pouvez voir les données R30 quotidiennes pour les 75 derniers jours et les données R30 de fin de mois jusqu’à 12 mois.

Vous pouvez sélectionner chacun de ces **noms de métriques** pour afficher les tendances au fil du temps.

 :::image type="content" source="../../assets/images/tdp/app-dashboard.png" alt-text="application":::

## <a name="use-tools-to-create-app-features"></a>Utiliser des outils pour créer des fonctionnalités d’application

Le Developer Portal inclut également des outils pour vous aider à créer certaines fonctionnalités clés des applications Teams. Voici quelques-uns de ces outils :

* **Scene Studio**: concevez [des scènes en mode Ensemble personnalisées](~/apps-in-teams-meetings/teams-together-mode.md) pour les réunions Teams.
* **Cartes adaptatives** de l’éditeur : créez et affichez un aperçu Cartes adaptatives à inclure avec vos applications.
* **Gestion de la plateforme d'identité Microsoft** : Enregistrez vos apps auprès d'Azure Active Directory pour aider les utilisateurs à se connecter et leur donner accès aux API.

## <a name="see-also"></a>Voir aussi

[Inclure une offre SaaS avec votre application Microsoft Teams](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md)
