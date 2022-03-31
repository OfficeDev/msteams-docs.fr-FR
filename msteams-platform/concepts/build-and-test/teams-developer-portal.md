---
title: Gérer vos applications avec le Portail du développeur
description: Découvrez comment configurer, distribuer et gérer vos applications à l’aide du portail de développement pour Microsoft Teams.
keywords: mise en place des équipes du portail de développement
ms.localizationpriority: medium
ms.topic: overview
ms.author: surbhigupta
ms.openlocfilehash: c6c5ea448d8b1f793b2aa881c62325a1016f4508
ms.sourcegitcommit: d9daad3d5818d5774911b96fdc7bde45b04c9908
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/29/2022
ms.locfileid: "64511233"
---
# <a name="manage-your-apps-with-the-developer-portal-for-microsoft-teams"></a>Gérer vos applications avec le Portail des développeurs pour Microsoft Teams

Le <a href="https://dev.teams.microsoft.com" target="_blank">Portail des développeurs pour Teams</a> est le principal outil de configuration, de distribution et de gestion de Microsoft Teams applications. Avec le portail du développeur, vous pouvez collaborer avec des collègues sur votre application, configurer des environnements d’runtime, et bien plus encore.

:::image type="content" source="../../assets/images/tdp/tdp_home_1.png" alt-text="Capture d’écran montrant la page d’accueil du portail de développement pour Teams.":::

> [!NOTE]
>
> * Pour l’instant, le portail du développeur n’est pas disponible pour les Cloud de la communauté du secteur public (Cloud de la communauté du secteur public), Cloud de la communauté du secteur public-Haut ou Département de la Défense (DOD).
> * Toutefois, vous pouvez utiliser un client normal pour créer une application dans le portail du développeur, télécharger l’application et télécharger l’application à l’aide de [Microsoft Graph](/graph/api/teamsapp-publish?view=graph-rest-1.0&tabs=http&preserve-view=true) dans un cloud national. Pour plus d’informations, voir [Déploiements dans le cloud national](/graph/deployments).

## <a name="register-an-app"></a>Inscrire une application

Le Portail des développeurs propose deux façons d’inscrire une Teams application :

* Inscrire une toute nouvelle application
* Importer un package d’application existant

> [!NOTE]
> Si vous créez une application à [l’Microsoft Teams Shared Computer Toolkit pour Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension), vous pouvez gérer cette application dans le Portail des développeurs.

## <a name="set-up-an-environment"></a>Configurer un environnement

Vous pouvez configurer des environnements et des variables globales pour faciliter la transition de votre application de votre runtime local vers la production. Les variables globales sont utilisées dans tous les environnements.

Pour configurer un environnement :

1. Dans le portail du développeur, sélectionnez l’application sur qui vous travaillez.
2. Go to the **Environments** page and select **+ Add an environment**.
3. **Sélectionnez + Ajoutez une variable** pour créer des variables de configuration pour votre environnement.

Pour utiliser des variables :

Utilisez les noms de variables au lieu de valeurs codées en dur pour définir les configurations de votre application.

1. Entrez `{{` n’importe quel champ dans le portail du développeur. Une dropdown avec toutes les variables que vous avez créées pour l’environnement choisi ainsi que les variables globales s’affiche.  
1. Avant de télécharger votre package d’application (par exemple, lorsque vous êtes prêt à publier sur le Teams Store), sélectionnez l’environnement que vous souhaitez utiliser. Les configurations de votre application sont automatiquement mises à jour en fonction de l’environnement.

## <a name="identify-app-owners"></a>Identifier les propriétaires d’applications

Chaque application inclut une page **Propriétaires** , dans laquelle vous pouvez partager l’inscription de votre application avec des collègues de votre organisation. Le **rôle Collaborateur** dispose des mêmes autorisations que le rôle **Propriétaire** , à l’exception de la possibilité de supprimer une application.

## <a name="configure-your-apps-capabilities-and-other-important-metadata"></a>Configurer les fonctionnalités de votre application et d’autres métadonnées importantes

Une Teams est une application web. Comme toutes les applications web, son code source est généralement développé dans un éditeur de code ou IDE et hébergé quelque part dans le cloud (comme Azure).

Pour installer et restituer votre application dans Teams, vous devez inclure un ensemble de configurations que Teams reconnaît. Pour ce faire, il s’agit généralement d’un manifeste d’application, un fichier JSON qui contient toutes les métadonnées dont Teams a besoin pour afficher le contenu de votre application. Le Portail des développeurs fait abstraction de ce processus et inclut de nouvelles fonctionnalités et outils pour vous aider à réussir.

## <a name="test-your-app-directly-in-teams"></a>Testez votre application directement dans Teams

Le Portail des développeurs fournit des options de test et de débogage de votre application :

* Dans la page **Vue d’ensemble**, vous pouvez voir un instantané de la validation des configurations de votre application par rapport Teams cas de test du Store.
* **L’aperçu Teams** vous permet de lancer rapidement votre application dans le client Teams pour le débogage.

## <a name="distribute-your-app"></a>Distribuer votre application.

À partir du portail du développeur,  utilisez le bouton Distribuer pour télécharger un package d’application, publier dans votre organisation ou publier sur le Teams store.

Pour plus d’informations, [voir distribuer votre Teams app.](~/concepts/deploy-and-publish/apps-publish-overview.md)

## <a name="use-tools-to-create-app-features"></a>Utiliser des outils pour créer des fonctionnalités d’application

Le Portail des développeurs inclut également des outils pour vous aider à créer certaines fonctionnalités clés de Teams applications. Voici quelques-uns de ces outils :

* **Scene studio :** concevoir [des scènes personnalisées en mode](~/apps-in-teams-meetings/teams-together-mode.md) ensemble pour Teams réunions.
* **Éditeur de cartes adaptatives** : créez et affichez un aperçu des cartes adaptatives à inclure avec vos applications.
* **Plateforme d'identités Microsoft gestion des** applications : inscrivez vos applications auprès Azure Active Directory pour aider les utilisateurs à se connecter et à fournir l’accès aux API.

## <a name="see-also"></a>Voir aussi

[Inclure une offre SaaS avec votre application Microsoft Teams](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md)
