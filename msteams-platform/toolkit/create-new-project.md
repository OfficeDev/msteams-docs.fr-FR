---
title: Créer une application Teams à l’aide du Kit de ressources Teams
author: zyxiaoyuer
description: Créer une application Teams à l’aide du Kit de ressources Teams
ms.author: surbhigupta
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/14/2022
ms.openlocfilehash: d44f757141d31faaf4639a58fbbd31e5729e6f02
ms.sourcegitcommit: 1e77573e47fad51a19545949fdac1241b13052e2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/24/2022
ms.locfileid: "65656151"
---
# <a name="create-a-new-teams-app-using-teams-toolkit"></a>Créer une application Teams à l’aide du Kit de ressources Teams

Pour créer une application Teams à l’aide du Kit de ressources Teams, vous pouvez sélectionner l’une des options suivantes :

* [Créer une application Teams](create-new-project.md#create-a-new-teams-app)
* [Afficher des exemples](create-new-project.md#create-a-new-teams-app-using-view-samples)

### <a name="create-a-new-teams-app"></a>Créer une application Teams

1. Ouvrez Visual Studio Code.
1. Sélectionnez l’icône :::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.PNG" border="true"::: du kit de ressources Teams dans la barre latérale Visual Studio Code.
1. Sélectionnez **Créer une application Teams**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar.png" alt-text="Barre latérale du kit de ressources Teams":::

1. Vous pouvez sélectionner **Créer une application Teams** ou **Démarrer à partir d’un exemple**.
   
   :::image type="content" source="../assets/images/teams-toolkit-v2/select-create-app.png" alt-text="Créer une application":::
   
1. Si vous sélectionnez **Créer une application Teams**, l’image suivante s’affiche avec des modèles de trois catégories : application Teams basée sur un scénario, application Teams de base et applications Teams étendues dans Microsoft 365 : 

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams-capabilities.png" alt-text="Fonctionnalités de l'application Teams":::

1. Sélectionnez au moins une option pour commencer à créer l’application Teams.


### <a name="create-a-new-teams-app-using-view-samples"></a>Créer une application Teams à l’aide d’exemples de vues

Vous pouvez créer une application en explorant **Afficher les exemples** et en sélectionnant un exemple existant. L’exemple sélectionné peut déjà avoir certaines fonctionnalités, par exemple une liste de tâches avec un serveur principal Azure ou une intégration avec le kit de ressources Microsoft Graph.

 1. Ouvrez la **Boîte à outils Teams** à partir de Microsoft Visual Studio Code.
 1. Sélectionnez la section **DÉVELOPPEMENT** dans Treeview.
 1. Sélectionnez **Afficher les exemples**. 

    :::image type="content" source="../assets/images/teams-toolkit-v2/view-samples.png" alt-text="Afficher des exemples":::

    L’exemple de galerie s’affiche comme illustré dans l’image suivante :
   
    :::image type="content" source="../assets/images/teams-toolkit-v2/sample-gallery.png" alt-text="Exemple de galerie":::

  Vous pouvez explorer l’exemple de galerie comme suit :

  1. Sélectionnez un exemple pour parcourir les informations détaillées.
  1. Sélectionnez **Créer** dans la page d’informations de chaque exemple pour le télécharger. 
  1. Exécutez votre application localement ou à distance pour afficher un aperçu dans le client web Teams en suivant les instructions qui s’ouvrent automatiquement après avoir téléchargé l’exemple.
  1. Si vous ne souhaitez pas télécharger les exemples, vous pouvez sélectionner **Afficher sur GitHub** pour ouvrir l’exemple dans le référentiel d’exemples GitHub et parcourir le code source.

## <a name="step-by-step-guides-using-teams-toolkit"></a>Guides pas à pas à l’aide du Kit de ressources Teams

* [Créer une application Teams à l’aide de Blazor](../sbs-gs-blazorupdate.yml)
* [Créer une application Teams avec JavaScript à l’aide de React](../sbs-gs-javascript.yml)
* [Créer une application Teams avec SPFx](../sbs-gs-spfx.yml)
* [Créer une application Teams avec C# ou .NET](../sbs-gs-csharp.yml)
* [Envoyer une notification à Teams](../sbs-gs-notificationbot.yml)
* [Générer un bot de commandes](../sbs-gs-commandbot.yml)

## <a name="see-also"></a>Voir aussi

* [Provisionner des ressources cloud](provision.md)
* [Déployer l’application Teams dans le cloud](deploy.md)
* [Publier votre application Teams](../concepts/deploy-and-publish/appsource/publish.md)
* [Gérer plusieurs environnements](TeamsFx-multi-env.md)
* [Collaborer avec d’autres développeurs sur des projets Teams](TeamsFx-collaboration.md)