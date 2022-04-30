---
title: Gérer vos applications avec le Developer Portal
description: Découvrez comment configurer, distribuer et gérer vos applications à l’aide de la Developer Portal pour Microsoft Teams.
keywords: prise en main des équipes du portail des développeurs
ms.localizationpriority: high
ms.topic: overview
ms.author: surbhigupta
ms.openlocfilehash: f55ecd7e44760a353a6058e004ea3cf6cdb769b2
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111793"
---
# <a name="manage-your-apps-with-the-developer-portal-for-microsoft-teams"></a>Gérer vos applications avec le Portail des développeurs pour Microsoft Teams

<a href="https://dev.teams.microsoft.com" target="_blank">Portail des développeurs pour Teams</a> est l’outil principal pour configurer, distribuer et gérer vos applications Microsoft Teams. Avec le Developer Portal, vous pouvez collaborer avec des collègues sur votre application, configurer des environnements d’exécution et bien plus encore.

:::image type="content" source="../../assets/images/tdp/tdp_home_1.png" alt-text="capture d’écran montrant la page d’accueil du Developer Portal pour Teams.":::

> [!NOTE]
>
> * Actuellement, Developer Portal n’est pas disponible pour les locataires Cloud de la communauté du secteur public (GCC), GCC-High ou department of Defense (DOD).
> * Toutefois, vous pouvez utiliser un locataire standard pour créer une application dans le Developer Portal, télécharger l’application et charger l’application à l’aide de [Microsoft Graph](/graph/api/teamsapp-publish?view=graph-rest-1.0&tabs=http&preserve-view=true) dans un cloud national. Pour plus d’informations, consultez [Déploiements cloud nationaux](/graph/deployments).

## <a name="register-an-app"></a>Inscrire une application

Le Developer Portal fournit deux façons d’inscrire une application Teams :

* Inscrire une toute nouvelle application
* Importer un package d’application existant

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

## <a name="use-tools-to-create-app-features"></a>Utiliser des outils pour créer des fonctionnalités d’application

Le Developer Portal inclut également des outils pour vous aider à créer certaines fonctionnalités clés des applications Teams. Voici quelques-uns de ces outils :

* **Scene Studio**: concevez [des scènes en mode Ensemble personnalisées](~/apps-in-teams-meetings/teams-together-mode.md) pour les réunions Teams.
* **Cartes adaptatives** de l’éditeur : créez et affichez un aperçu Cartes adaptatives à inclure avec vos applications.
* **Gestion de la plateforme d'identité Microsoft** : Enregistrez vos apps auprès d'Azure Active Directory pour aider les utilisateurs à se connecter et leur donner accès aux API.

## <a name="see-also"></a>Voir aussi

[Inclure une offre SaaS avec votre application Microsoft Teams](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md)
