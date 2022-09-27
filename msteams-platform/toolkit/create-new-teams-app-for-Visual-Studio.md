---
title: Créer une application Teams dans Visual Studio
author: surbhigupta
description: Dans ce module, découvrez comment créer une application Teams à l’aide du Kit de ressources Teams pour Visual Studio
ms.author: v-amprasad
ms.localizationpriority: high
ms.topic: overview
ms.date: 07/29/2022
ms.openlocfilehash: 12f0b74726aed8cdca50d9f5c078acd0f22cbeaa
ms.sourcegitcommit: 65ae3ccc2312ddc6cdaa05096e30bdf9dca10c3f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2022
ms.locfileid: "68027435"
---
# <a name="create-new-teams-app-in-visual-studio"></a>Créer une application Teams dans Visual Studio

Teams Toolkit fournit des modèles d’application Microsoft Teams dans Visual Studio pour créer une application Teams.  Vous pouvez rechercher et sélectionner le modèle d’application Teams dont vous avez besoin lorsque vous créez un projet. Vous pouvez avoir des modèles d’application Teams pour la création.

* Application Tab
* Bot de commandes
* Bot de notification
* Extension de message

## <a name="prerequisites"></a>Conditions préalables

| &nbsp; | Installer | Pour l’utilisation... |
| --- | --- | --- |
| &nbsp; | **Obligatoire** | &nbsp; |
| &nbsp; | Visual Studio version 17.3 | Vous pouvez installer l’édition Entreprise de Visual Studio et installer la charge de travail « ASP.NET » et les outils de développement Microsoft Teams. |
| &nbsp; | Toolkit Teams | Extension Visual Studio qui crée une structure de projet pour votre application. Utilisez la dernière version. |
| &nbsp; | [Microsoft Teams](https://www.microsoft.com/microsoft-teams/download-app) | Microsoft Teams pour collaborer avec toutes les personnes avec lesquelles vous travaillez via les applications pour les conversations, les réunions, les appels, le tout au même endroit. |
 | &nbsp; | [Préparer votre client Microsoft Office 365](../concepts/build-and-test/prepare-your-o365-tenant.md) | Accès au compte Teams avec les autorisations appropriées pour installer une application. |

1. Sélectionnez **Créer un projet** dans la section **Prise en main** lorsque vous lancez Visual Studio.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-create-new-project1.png" alt-text="Créer un projet à partir de la prise en main":::

   Vous pouvez également créer un projet directement à partir de l’application.

1. Sélectionnez **le menu Fichier** .
1. Sélectionnez  **Nouveau**.
1. Sélectionnez **Projet**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-create-new-project2.png" alt-text="Créer un projet à partir du menu fichier":::

1. Recherchez l’application Microsoft **Teams** dans la liste.
1. Sélectionnez **l’application Microsoft Teams**.
1. Sélectionnez **Suivant**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-ms-teams-app.png" alt-text="Rechercher et choisir l’application Microsoft Teams":::

1. Sélectionnez **le nom du** projet et entrez le nom de votre projet.
1. Sélectionnez **Créer**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-ms-teams-app-project-name.png" alt-text="Nommer votre application":::

1. Sélectionnez le **type d’application Teams** que vous souhaitez créer.
1. Sélectionnez **Créer**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-ms-teams-app-type.png" alt-text="Sélectionner le type d’application Teams":::

## <a name="teams-app-templates-in-teams-toolkit-for-visual-studio"></a>Modèles d’application Teams dans le Kit de ressources Teams pour Visual Studio

Vous pouvez voir les modèles d’application Teams déjà renseignés dans le Kit de ressources Teams pour différents types d’application Teams. Le tableau suivant répertorie tous les modèles disponibles :

|Modèle d’application Teams  |Description  |
|---------|---------|
|Notification Bot     |L’application Bot de notification peut envoyer une notification à votre client Teams. Il existe plusieurs façons de déclencher la notification. Par exemple, déclenchez la notification par requête HTTP ou par heure. Vous pouvez également sélectionner une notification déclenchée en fonction de votre scénario métier.         |
|Bot de commandes     |Les utilisateurs peuvent taper une commande pour interagir avec le bot à l’aide de l’application Command Bot.         |
|Tab     |L’application Tab affiche une page web dans Teams et active l’authentification unique à l’aide d’un compte Teams.         |
|Message Extension     |L’application d’extension de message implémente des fonctionnalités simples telles que la création d’une carte adaptative, la recherche de packages De la pépite, le déploiement de liens pour le domaine « dev.botframework.com ».         |

> [!NOTE]
>Une fois le projet créé, le Kit de ressources Teams ouvre automatiquement La prise en main. Vous pouvez maintenant voir les instructions de prise en main et découvrir les différentes fonctionnalités du Kit de ressources Teams.

## <a name="see-also"></a>Voir aussi

* [Provisionner des ressources cloud à l’aide de Visual Studio](provision-cloud-resources.md)
* [Déployer une application Teams dans le cloud à l’aide de Visual Studio](deploy-teams-app.md)
