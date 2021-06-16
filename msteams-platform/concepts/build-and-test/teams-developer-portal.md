---
title: Gérer vos applications avec le Portail du développeur
description: Découvrez comment gérer vos applications à l’aide du portail de développement pour Microsoft Teams.
keywords: mise en place des équipes du portail de développement
localization_priority: Normal
ms.topic: overview
ms.author: surbhigupta
ms.openlocfilehash: 6dca8723248441c3cf672931295b4b68e02cc24c
ms.sourcegitcommit: 9f499908437655d6ebdc6c4b3c3603ee220315b7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/15/2021
ms.locfileid: "52949685"
---
# <a name="manage-your-apps-with-the-developer-portal-for-microsoft-teams"></a>Gérer vos applications avec le Portail des développeurs pour Microsoft Teams

> [!NOTE]
> Le Portail des développeurs pour Teams est actuellement en prévisualisation [pour les développeurs publics.](~/resources/dev-preview/developer-preview-intro.md)

Le <a href="https://dev.teams.microsoft.com" target="_blank">Portail des développeurs pour Teams</a> est le principal outil de configuration, de distribution et de gestion de Microsoft Teams applications. Avec le Portail des développeurs, vous pouvez collaborer avec des collègues sur votre application, configurer des environnements d’runtime, et bien plus encore.

:::image type="content" source="../../assets/images/tdp/tdp_home_1.png" alt-text="Capture d’écran montrant la page d’accueil du portail de développement pour Teams.":::

## <a name="register-an-app"></a>Inscrire une application

Le Portail des développeurs propose deux façons d’inscrire une Teams application :

* Inscrire une toute nouvelle application
* Importer un package d’application existant

> [!NOTE]
> Si vous créez une application à [l’aide Microsoft Teams Shared Computer Toolkit pour Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension), vous pouvez gérer cette application dans le Portail des développeurs.

## <a name="set-up-an-environment"></a>Configurer un environnement

Vous pouvez configurer des environnements et des variables globales pour faciliter la transition de votre application de votre runtime local vers la production. Les variables globales sont utilisées dans tous les environnements.

**Pour configurer un environnement**

1. Dans le portail du développeur, sélectionnez l’application sur qui vous travaillez.
2. Go to the **Environments** page and select **+ Add an environment**.
3. Sélectionnez **+ Ajoutez une variable** pour créer des variables de configuration pour votre environnement.

**Pour utiliser des variables**

Utilisez les noms de variables au lieu de valeurs codées en dur pour définir les configurations de votre application.

1. Entrez `{{` n’importe quel champ dans le portail du développeur. Une dropdown avec toutes les variables que vous avez créées pour l’environnement choisi ainsi que les variables globales s’affiche.  
1. Avant de télécharger votre package d’application (par exemple, lorsque vous êtes prêt à publier sur le Teams Store), sélectionnez l’environnement que vous souhaitez utiliser. Les configurations de votre application sont mises à jour automatiquement en fonction de l’environnement. 

## <a name="identify-app-owners"></a>Identifier les propriétaires d’applications

Chaque application inclut une page **Propriétaires,** dans laquelle vous pouvez partager l’inscription de votre application avec des collègues de votre organisation. Le **rôle Collaborateur** dispose des mêmes autorisations que le rôle **Propriétaire,** à l’exception de la possibilité de supprimer une application.

## <a name="configure-your-apps-capabilities-and-other-important-metadata"></a>Configurer les fonctionnalités de votre application et d’autres métadonnées importantes

Une Teams est une application web. Comme toutes les applications web, son code source est généralement développé dans un éditeur de code ou IDE et hébergé quelque part dans le cloud (comme Azure).

Pour installer et restituer votre application dans Teams, vous devez inclure un ensemble de configurations Teams reconnu. Pour ce faire, il s’agit généralement d’un manifeste d’application, un fichier JSON qui contient toutes les métadonnées dont Teams a besoin pour afficher le contenu de votre application. Le Portail des développeurs fait abstraction de ce processus et inclut de nouvelles fonctionnalités et outils pour vous aider à réussir.

## <a name="test-your-app-directly-in-teams"></a>Testez votre application directement dans Teams

Le Portail des développeurs fournit des options pour tester et déboguer votre application :

* Dans la page **Vue d’ensemble,** vous pouvez voir un instantané de la validation des configurations de votre application par rapport Teams cas de test du Store.
* **L’aperçu Teams** bouton vous permet de lancer rapidement votre application dans le client Teams pour le débogage.

## <a name="distribute-your-app"></a>Distribuer votre application.

À partir du portail  du développeur, utilisez le bouton Distribuer pour télécharger un package d’application, publier dans votre organisation ou publier sur le Teams store.

Pour plus d’informations, [voir distribuer votre Teams application.](~/concepts/deploy-and-publish/apps-publish-overview.md)

## <a name="analyze-your-apps-usage"></a>Analyser l’utilisation de votre application

Dans **la** page Vue d’ensemble, vous pouvez voir le nombre total d’utilisateurs actifs pour votre application. Ces mesures sont disponibles pour les applications publiées dans le Teams store ou le catalogue d’applications d’une organisation via le Portail du développeur et limitées à l’ID de l’application.

| Métrique | Définition |
| :-----------------------| :------------------------------------------------------------------------------------------------------|
| *R30 mensuel* | Mesure d’utilisation par défaut. Il indique le nombre d’utilisateurs actifs uniques qui ont utilisé votre application dans cette fenêtre de 30 jours en temps UTC. |
| *Tous les jours* | Indique le nombre d’utilisateurs actifs uniques qui ont utilisé votre application dans un jour donné en UTC. |

L’utilisation mensuelle et quotidienne est indiquée pour les sept, 30 et 60 derniers jours. L’utilisation doit être reflétée pour un jour donné dans les 24 à 48 heures. L’affichage des nouvelles applications peut prendre jusqu’à 3 à 5 jours.

## <a name="use-tools-to-create-app-features"></a>Utiliser des outils pour créer des fonctionnalités d’application

Le Portail des développeurs inclut également des outils pour vous aider à créer certaines fonctionnalités clés de Teams applications. Voici quelques-uns de ces outils :

* **Scene studio :** concevoir [des scènes personnalisées](~/apps-in-teams-meetings/teams-together-mode.md) en mode ensemble pour Teams réunions.
* **Éditeur de cartes adaptatives**: créez et prévisualiser des cartes adaptatives à inclure avec vos applications.
* **Plateforme d’identités Microsoft gestion des** applications : inscrivez vos applications avec Azure Active Directory (Azure AD) pour aider les utilisateurs à se connecter et à fournir l’accès aux API.
