---
title: Gérer vos applications avec le Portail du développeur
description: Découvrez comment gérer vos applications à l’aide du portail de développement pour Microsoft Teams.
keywords: mise en place des équipes du portail de développement
ms.localizationpriority: medium
ms.topic: overview
ms.author: surbhigupta
ms.openlocfilehash: 41aade2eaedee2095e60288a7e4021897bb1a3fa
ms.sourcegitcommit: ece03efbb0e9d1fea5bd01c9c05a2bc232c1a1c3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/15/2021
ms.locfileid: "60378911"
---
# <a name="manage-your-apps-with-the-developer-portal-for-microsoft-teams"></a>Gérer vos applications avec le Portail des développeurs pour Microsoft Teams

Le <a href="https://dev.teams.microsoft.com" target="_blank">Portail des développeurs pour Teams</a> est l’outil principal pour configurer, distribuer et gérer vos applications Microsoft Teams client. Avec le portail du développeur, vous pouvez collaborer avec des collègues sur votre application, configurer des environnements d’runtime, et bien plus encore.

:::image type="content" source="../../assets/images/tdp/tdp_home_1.png" alt-text="Capture d’écran montrant la page d’accueil du portail de développement pour Teams.":::

## <a name="register-an-app"></a>Inscrire une application

Vous pouvez inscrire votre application Teams dans le Portail des développeurs de l’une des manières suivantes :

* Inscrire une nouvelle application
* Importer un package d’application existant

> [!NOTE]
> Si vous créez une application à [l’aide Microsoft Teams Shared Computer Toolkit pour Visual Studio Code,](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)vous pouvez gérer cette application dans le Portail du développeur.

## <a name="set-up-an-environment"></a>Configurer un environnement

Vous pouvez configurer des environnements et des variables globales pour faciliter la transition de votre application de votre runtime local vers la production. Les variables globales sont utilisées dans tous les environnements.

**Pour configurer un environnement**

1. Dans le portail du développeur, sélectionnez l’application sur qui vous travaillez.
2. Go to **Environments** and select **+ Add an environment**.
3. Sélectionnez **+ Ajoutez une variable** pour créer des variables de configuration pour votre environnement.

**Pour utiliser des variables**

Utilisez les noms de variables au lieu de valeurs codées en dur pour définir les configurations de votre application.

1. Entrez `{{` n’importe quel champ dans le portail du développeur. Une dropdown avec toutes les variables que vous avez créées pour l’environnement choisi ainsi que les variables globales s’affiche.  
1. Avant de télécharger votre package d’application (par exemple, lorsque vous êtes prêt à publier sur le Teams Store), sélectionnez l’environnement que vous souhaitez utiliser. Les configurations de votre application sont mises à jour automatiquement en fonction de l’environnement. 

## <a name="identify-app-owners"></a>Identifier les propriétaires d’applications

Chaque application inclut **les propriétaires,** où vous pouvez partager l’inscription de votre application avec des collègues de votre organisation. Le **rôle Collaborateur** dispose des mêmes autorisations que le rôle **Propriétaire,** à l’exception de la possibilité de supprimer une application.

## <a name="configure-your-apps-capabilities-and-other-important-metadata"></a>Configurer les fonctionnalités de votre application et d’autres métadonnées importantes

Une Teams est une application web. Comme toutes les applications web, son code source est généralement développé dans un éditeur de code ou IDE et hébergé quelque part dans le cloud (comme Azure).

Pour installer et restituer votre application dans Teams, vous devez inclure un ensemble de configurations Teams reconnu. Pour ce faire, il s’agit généralement d’un manifeste d’application, un fichier JSON qui contient toutes les métadonnées dont Teams a besoin pour afficher le contenu de votre application. Le Portail des développeurs fait abstraction de ce processus et inclut de nouvelles fonctionnalités et outils pour vous aider à réussir.

### <a name="basic-app-configuration"></a>Configuration d’application de base 

**Informations de base sur l’application :** Les utilisateurs voient sur la page de détails de votre application dans Teams, tels que l’ID de l’application, les noms d’application, les descriptions, les informations du développeur, la version, les URL d’application et l’ID Microsoft Partner Network.

**Image de marque :** Les applications nécessitent une icône de couleur et de plan au format PNG. Pour publier votre application dans Teams store, les icônes doivent répondre à des exigences de taille spécifiques.

**Fonctionnalités :** Teams fonctionnalités que vous pouvez inclure dans votre application. Vous pouvez ajouter une ou plusieurs fonctionnalités en fonction des cas d’utilisation de votre application.

**Autorisations :** Spécifiez à quoi les utilisateurs doivent consentir lors de l’utilisation de votre application.

**Sign-on unique :** Configurez votre application pour authentifier les utilisateurs à l’authentification unique (SSO).

**Domaines :** List all the domains your app needs to navigate to. Utilisez des caractères génériques pour inclure plusieurs sous-domaine. Par exemple, `*.example.com`.

### <a name="advanced-app-configuration"></a>Configuration d’application avancée

**Contenu de l’application :** Configurez les fonctionnalités facultatives telles que l’indicateur de chargement et le mode plein écran pour votre application.

**Personnalisation de l’application :** Sélectionnez les propriétés que Teams administrateurs peuvent personnaliser sur votre application.

**Paramètres de première partie :** Fonctionnalités pour les applications tierces qui s’étendent au-delà des fonctionnalités publiques.

### <a name="distribute-your-app"></a>Distribuer votre application.

**Package d’application :** Le package d’application décrit la configuration, les fonctionnalités, les ressources requises et d’autres attributs importants de votre application. Par exemple, le schéma de manifeste.

**Vols :** Contrôler qui obtient les mises à jour de l’application. Par exemple, vous pouvez publier une mise à jour pour les employés de Microsoft afin d’identifier et de corriger les bogues avant de les publier au public.

**Publier dans votre organisation (Microsoft) :** Rendez votre application accessible aux membres de votre organisation. Une fois approuvée par votre administrateur informatique, votre application sera Teams sous Applications > conçues pour votre organisation.

**Publiez dans le Teams store :** L’outil de validation d’application vérifie votre package d’application par rapport aux cas de test que Microsoft utilise, lors de la révision de votre application. Résolvez les erreurs ou avertissements et lisez la liste de vérification avant de l’envoyer.

## <a name="test-your-app-directly-in-teams"></a>Testez votre application directement dans Teams

Le Portail des développeurs fournit des options de test et de débogage de votre application :

* Dans **Vue d’ensemble,** vous pouvez voir un instantané de la validation des configurations de votre application par rapport Teams cas de test du Store.
* **La prévisualisation Teams** vous permet de lancer rapidement votre application dans le client Teams pour le débogage.

## <a name="distribute-your-app"></a>Distribuer votre application.

À partir du portail du développeur, utilisez **Distribute** pour télécharger un package d’application, publier sur votre organisation ou publier sur le Teams store.

Pour plus d’informations, [voir distribuer votre Teams app.](~/concepts/deploy-and-publish/apps-publish-overview.md)

## <a name="analyze-your-apps-usage"></a>Analyser l’utilisation de votre application

Dans **Vue d’ensemble,** vous pouvez voir le nombre total d’utilisateurs actifs pour votre application. Ces mesures sont disponibles pour les applications publiées dans le Teams store ou le catalogue d’applications d’une organisation via le Portail du développeur et limitées à l’ID d’application.

| Métrique | Définition |
| :-----------------------| :------------------------------------------------------------------------------------------------------|
| *R30 mensuel* | Mesure d’utilisation par défaut. Il indique le nombre d’utilisateurs actifs uniques, qui ont utilisé votre application dans cette fenêtre de 30 jours en temps UTC. |
| *Tous les jours* | Indique le nombre d’utilisateurs actifs uniques, qui ont utilisé votre application dans un jour donné au cours de l’UTC. |

L’utilisation mensuelle et quotidienne est indiquée pour les sept derniers jours, 30 jours et 60 jours. L’utilisation doit être reflétée pour un jour donné dans les 24 à 48 heures. L’affichage des nouvelles applications peut prendre jusqu’à 3 à 5 jours.

## <a name="use-tools-to-create-app-features"></a>Utiliser des outils pour créer des fonctionnalités d’application

Le Portail des développeurs inclut également des outils pour vous aider à créer certaines fonctionnalités clés de Teams applications. Voici quelques-uns de ces outils :

* **Scene studio :** concevoir [des scènes personnalisées](~/apps-in-teams-meetings/teams-together-mode.md) en mode ensemble pour Teams réunions.
* **Éditeur de cartes adaptatives**: créez et prévisualiser des cartes adaptatives à inclure avec vos applications.
* **Plateforme d'identités Microsoft gestion** des applications : inscrivez vos applications avec Azure Active Directory (Azure AD) pour aider les utilisateurs à se connecter et à fournir l’accès aux API.

## <a name="see-also"></a>Voir aussi

[Inclure une offre SaaS avec votre application Microsoft Teams application](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md)
