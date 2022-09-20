---
title: Vue d’ensemble du kit de ressources Teams
author: zyxiaoyuer
description: Dans ce module, découvrez le Kit de ressources Teams, l’installation de Teams Toolkit et le parcours utilisateur du Kit de ressources Teams
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/24/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: bdcf92b52956eee6db21eb03d115a494c0f063e9
ms.sourcegitcommit: dccb48902e08484692ab927415bcd3d61dc50db2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/19/2022
ms.locfileid: "67806772"
---
# <a name="teams-toolkit-overview"></a>Vue d’ensemble du kit de ressources Teams

Teams Toolkit est une fonctionnalité qui vous permet d’effectuer plusieurs fonctions dans Microsoft Visual Studio Code et Visual Studio. Avec l’aide de Teams Toolkit, vous pouvez automatiser le processus, de la création au déploiement et à la personnalisation de votre application. Les différentes fonctionnalités et avantages du Kit de ressources Teams sont décrits dans la documentation correspondante des environnements que vous choisissez.

::: zone pivot="visual-studio-code"

## <a name="teams-toolkit-overview-for--visual-studio-code"></a>Vue d’ensemble du Kit de ressources Teams pour Visual Studio Code

Teams Toolkit vous permet de créer, déboguer et déployer votre application Teams directement à partir de Visual Studio Code.App développement avec le kit de ressources présente les avantages suivants :

* Identité intégrée
* Accès au stockage cloud
* Données de Microsoft Graph
* Services Azure et Microsoft 365 avec une approche de configuration zéro.

Pour le développement d’applications Teams, similaire au Kit de ressources Teams pour Visual Studio, vous pouvez utiliser l’[outil CLI](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md), qui se compose de toolkit `teamsfx`.

## <a name="user-journey-of-teams-toolkit"></a>Parcours utilisateur du Kit de ressources Teams

Teams Toolkit automatise le travail manuel et offre une excellente intégration des ressources Teams et Azure. L’image suivante montre le parcours utilisateur du Kit de ressources Teams :

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-toolkit-user-journey2.png" alt-text="Parcours utilisateur du Kit de ressources Teams" lightbox="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-toolkit-user-journey2.png":::

Les principaux jalons de ce parcours sont les suivants :

1. Commencez par créer un projet ou essayer un exemple d’application Teams.
1. Ajoutez des fonctionnalités ou modifiez le fichier manifeste si nécessaire.
1. Utilisez Microsoft 365 compte pour générer et déboguer votre application Teams.
1. Utilisez un compte Azure pour provisionner et déployer votre application dans le cloud.
1. Publiez votre application dans Teams.

Le tableau suivant vous aide à obtenir la vue d’ensemble du Kit de ressources Teams dans Visual Studio Code :

| Processus | Description |
| ---- | ---- |
| Installer Teams Toolkit | Vous pouvez installer Teams Toolkit de deux manières : <br> - Utilisation de Visual Studio Code <br> - Utilisation de Visual Studio Code Marketplace|
| Prise en charge des environnements de génération | Vous avez deux types d’environnement différents : <br> - Javascript ou Typescript <br> - SPFx |
| Prise en charge des types d’applications et de la fonction Azure | Il existe deux types d’applications différents : <br> - Application basée sur les fonctionnalités, telle que l’onglet, le bot, l’extension de message  <br> - Application Teams basée sur un scénario, telle que le bot de notification, le bot de commandes et l’onglet personnel activé pour l’authentification unique |
| Développer votre application Teams | Il contient : <br> - Ajouter et gérer un environnement <br> - Créer une application multi-fonctionnalités <br> - Créer des ressources cloud basées sur des fonctionnalités <br> - Intégrer une API tierce <br> - Personnaliser le fichier manifeste <br> - Kit de développement logiciel (SDK) TeamsFx |
| Déboguer votre Teams application | Il contient : <br> - Déboguer votre application Teams localement <br> - Déboguer le processus en arrière-plan|
| Héberger votre application Teams | Il contient : <br> - Approvisionner des ressources dans le cloud <br> - Déployer dans le cloud|
| Tester votre application Teams | Il contient : <br> - Intégrer et collabrate <br> - Package de métadonnées Zip Teams <br> - Charger et tester une application dans l’environnement Teams <br> - Tester le comportement de l’application dans un environnement différent|
| Publier votre application Teams | Il contient : <br> - Publier votre application <br> - Gérer l’approbation de l’administrateur <br> - Publier sur le store <br> - Intégrer au portail des développeurs |

### <a name="entities-integrated-with-teams-toolkit"></a>Entités intégrées à Teams Toolkit

Teams Toolkit est une extension dans Visual Studio Code. Il est intégré aux entités suivantes dans Teams Toolkit.such as Azure AD and Microsoft 365, Developer Portal and Microsoft graph. Toutes les entités sont intégrées au Kit de ressources Teams et aident les utilisateurs à créer une application.

| Entités | Description |
| ---- | ---- |
| Azure AD  | Azure Active Directory (Azure AD) est un service de gestion des identités et des accès basé sur le cloud. Ce service permet à vos employés d’accéder à des ressources externes, telles que Microsoft 365, le Portail Azure et des milliers d’autres applications SaaS. |
| Microsoft 365  | Compte de développeur Teams lors du développement d’une application.|
| Portail des développeurs | Portail des développeurs pour Teams est l’outil principal pour configurer, distribuer et gérer vos applications Microsoft Teams. Avec le Developer Portal, vous pouvez collaborer avec des collègues sur votre application, configurer des environnements d’exécution et bien plus encore. |
| Microsoft Graph | Microsoft Graph est une passerelle qui vous permet d’accéder aux données et aux renseignements dans Microsoft 365. Elle fournit un modèle de programmabilité unifié qui vous permet d’accéder à la quantité impressionnante de données disponibles dans Microsoft 365, Windows et Enterprise Mobility + Security. |

Teams Toolkit propose tous les outils nécessaires à la création d’une application Teams au même endroit.

## <a name="manage-your-apps-using-developer-portal"></a>Gérer vos applications à l’aide du portail des développeurs

Étant donné que Teams Toolkit est intégré au portail des développeurs, vous pouvez configurer, distribuer et gérer votre application à l’aide [du portail des développeurs pour Teams](../concepts/build-and-test/teams-developer-portal.md) sous DÉPLOIEMENT après avoir créé une application. Pour plus d’informations, consultez [gérer vos applications Teams à l’aide du portail des développeurs](../concepts/build-and-test/manage-your-apps-in-developer-portal.md).

:::image type="content" source="../assets/images/teams-toolkit-v2/build-environment-developer-portal-1.png" alt-text="Portail des développeurs":::

::: zone-end

::: zone pivot="visual-studio"

## <a name="teams-toolkit-overview-for-visual-studio"></a>Vue d’ensemble du Kit de ressources Teams pour Visual Studio

Teams Toolkit pour Visual Studio vous aide à créer, déboguer et déployer des applications Microsoft Teams. Le Kit de ressources Teams pour Visual Studio est en disponibilité générale dans Visual Studio 2022 version 17.3. Le développement d’applications avec Teams Toolkit présente les avantages suivants :

* Identité intégrée
* Accès au stockage cloud
* Données de Microsoft Graph
* Services Azure et Microsoft 365 avec une approche de configuration zéro

Pour le développement d’applications Teams, vous pouvez également utiliser [l’outil CLI](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md), similaire à Teams Toolkit pour Microsoft Visual Studio code qui inclut Toolkit `teamsfx`.

Teams Toolkit apporte tous les outils nécessaires à la création d’une application Teams au même endroit.

> [!NOTE]
> Teams Toolkit n’est pas disponible dans d’autres versions.

## <a name="user-journey-of-teams-toolkit"></a>Parcours utilisateur du Kit de ressources Teams

Teams Toolkit automatise le travail manuel et vous offre une intégration parfaite des ressources Teams et Azure. L’image suivante montre le parcours utilisateur :

:::image type="content" source="../assets/images/teams-toolkit-overview/teams-toolkit-user-journey.png" alt-text="Parcours utilisateur du kit de ressources Teams" lightbox="../assets/images/teams-toolkit-overview/teams-toolkit-user-journey.png":::

Les principaux jalons de ce parcours sont les suivants :

1. Vous pouvez commencer par créer un projet ou essayer de créer un exemple d’application Teams.
1. Vous pouvez ensuite modifier le code ou le fichier manifeste en fonction des besoins.
1. Pour créer et déboguer l’application Teams, vous pouvez utiliser votre compte Microsoft 365.
1. Pour l’approvisionnement et le déploiement de votre application dans le cloud, vous pouvez utiliser votre compte Azure.
1. Vous pouvez enfin publier votre application dans Teams.

Les opérations suivantes ne sont pas encore prises en charge dans le Kit de ressources Teams pour Visual Studio par rapport à Teams Toolkit pour Microsoft Visual Studio Code, mais elles sont planifiées dans la future feuille de route du produit.

* Ajoutez d’autres fonctionnalités Teams à votre application Teams.
* Ajouter d’autres ressources Azure à votre application Teams
* Ajoutez l’authentification unique (SSO) à votre application Teams.
* Ajoutez une connexion d’API à votre application Teams.
* Personnalisez le manifeste Microsoft Azure Active Directory (Azure AD).
* Ajoutez des pipelines CI/CD.
* Gérer plusieurs environnements cloud.
* Collaborez sur des projets Teams.
* Publier l’application Teams.

### <a name="teamsfx-net-sdk-reference-docs"></a>Documentation de référence sur le Kit de développement logiciel (SDK) .NET TeamsFx

* [Espace de noms Microsoft.Extensions.DependencyInjection](/../dotnet/api/Microsoft.Extensions.DependencyInjection)
* [Espace de noms Microsoft.TeamsFx](/../dotnet/api/Microsoft.TeamsFx)
* [Espace de noms Microsoft.TeamsFx.Configuration](/../dotnet/api/Microsoft.TeamsFx.Configuration)
* [Espace de noms Microsoft.TeamsFx.Conversation](/../dotnet/api/Microsoft.TeamsFx.Conversation)
* [Espace de noms Microsoft.TeamsFx.Helper](/../dotnet/api/Microsoft.TeamsFx.Helper)

::: zone-end

## <a name="see-also"></a>Voir aussi

* [Créer une application Teams dans Visual Studio](create-new-teams-app-for-Visual-Studio.md)
* [Provisionner des ressources cloud à l’aide de Visual Studio](provision-cloud-resources.md)
* [Déployer une application Teams dans le cloud à l’aide de Visual Studio](deploy-teams-app.md)

