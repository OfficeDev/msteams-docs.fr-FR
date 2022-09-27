---
title: Vue d’ensemble du Kit de ressources Teams pour Visual Studio
author: surbhigupta
description: Dans ce module, découvrez la vue d’ensemble du Kit de ressources Teams pour Visual Studio
ms.author: v-amprasad
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/24/2022
ms.openlocfilehash: 3685d105f13024507b880c35040b9d798a6d845f
ms.sourcegitcommit: 65ae3ccc2312ddc6cdaa05096e30bdf9dca10c3f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2022
ms.locfileid: "68027431"
---
# <a name="teams-toolkit-overview-for-visual-studio"></a>Vue d’ensemble du Kit de ressources Teams pour Visual Studio

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

:::image type="content" source="../assets/images/teams-toolkit-overview/teams-toolkit-user-journey.png" alt-text="Parcours utilisateur du kit de ressources Teams":::

Les principaux jalons de ce parcours sont les suivants :

1. Vous pouvez commencer par créer un projet ou essayer de créer un exemple d’application Teams.
1. Vous pouvez ensuite modifier le code ou le fichier manifeste en fonction des besoins.
1. Pour créer et déboguer l’application Teams, vous pouvez utiliser votre compte Microsoft 365.
1. Pour l’approvisionnement et le déploiement de votre application dans le cloud, vous pouvez utiliser votre compte Azure.
1. Vous pouvez enfin publier votre application dans Teams.

## <a name="install-teams-toolkit-for-visual-studio"></a>Extension de kit de ressources Teams pour Visual Studio

Vous pouvez télécharger le dernier programme d’installation de Visual Studio à partir de la [page de téléchargement de Visual Studio](https://visualstudio.microsoft.com).

> [!NOTE]
> Vous devez d’abord installer le programme d’installation de Visual Studio avant d’installer Visual Studio.

Après avoir ouvert le programme d’installation de Visual Studio, dans la fenêtre Charges de travail contextuelles.

1. Sélectionnez la zone ASP.NET et la charge de **travail de développement web** .
1. Sélectionnez la zone **Outils de développement Microsoft Teams** dans le panneau détails de l’installation.
1. Sélectionnez **Installer**.

   :::image type="content" source="../assets/images/teams-toolkit-overview/visual-studio-install1.png" alt-text="Installation de Visual Studio":::

1. Sélectionnez **Lancer** pour ouvrir Visual Studio.

    :::image type="content" source="../assets/images/teams-toolkit-overview/visual-studio-launch.png" alt-text="Lancer Visual Studio":::

   > [!IMPORTANT]
   > Nous vous recommandons de télécharger Visual Studio 2022 version 17.3.0, car Teams Toolkit pour Visual Studio est en disponibilité générale dans cette version. Cet article est écrit pour Visual Studio 2022 version 17.3.0. Teams Toolkit version 17.3.* ou ultérieure.

## <a name="take-a-tour-of-teams-toolkit"></a>Visite guidée du Kit de ressources Teams

Après avoir installé Teams Toolkit, vous pouvez examiner brièvement les différentes options de menu du Kit de ressources Teams :

1. Sélectionnez **Projet**.
1. Sélectionnez **Teams Toolkit**.
1. Vous pouvez désormais accéder aux options du **menu du Kit de ressources Teams** .

   :::image type="content" source="../assets/images/teams-toolkit-overview/teams-toolkit-operations-menu.png" alt-text="Menu des opérations du kit de ressources Teams":::

   Vous pouvez également accéder au menu du Kit de ressources Teams à partir de Explorateur de solutions.

4. Cliquez avec le bouton droit sur votre **projet**.
5. Sélectionnez les options de menu Teams **Toolkit** > **Teams Toolkit** .

   :::image type="content" source="../assets/images/teams-toolkit-overview/teams-toolkit-operations-menu1.png" alt-text="Opérations du kit de ressources Teams à partir de Project":::

   > [!NOTE]
   > Dans ce scénario, le nom du projet est **MyTeamsApp1**.

Vous pouvez effectuer les fonctions suivantes sur le Kit de ressources Teams pour Visual Studio :

|Fonction  |Description  |
|---------|---------|
|Créer un projet Teams     |Créer un projet Teams à l’aide d’un modèle Teams dans Visual Studio         |
|Préparer les dépendances d’application Teams     |Avant d’effectuer un débogage local, cette étape vous permet de configurer les dépendances de débogage locales et d’inscrire l’application Teams dans la plateforme Teams. Vous avez besoin d’un compte Microsoft 365. Pour plus d’informations, consultez [Déboguer votre application Teams localement à l’aide de Visual Studio](debug-teams-app-visual-studio.md)         |
|Ouvrir le fichier manifeste     |Pour ouvrir le fichier manifeste Teams, vous pouvez pointer sur les paramètres pour afficher un aperçu des valeurs. Pour plus d’informations, consultez [modifier le manifeste de l’application Teams à l’aide de Visual Studio](VS-TeamsFx-preview-and-customize-app-manifest.md)         |
|Mettre à jour le manifeste dans le portail des développeurs Teams     |Lorsque vous mettez à jour le fichier manifeste, vous pouvez redéployer le fichier manifeste sur Azure sans redéployer l’ensemble du projet. Utilisez cette commande pour mettre à jour vos modifications à distance. Pour plus d’informations, consultez [modifier le manifeste de l’application Teams à l’aide de Visual Studio](VS-TeamsFx-preview-and-customize-app-manifest.md)       |
|Provisionner dans le cloud     |Cette option vous permet de créer des ressources Azure qui hébergent votre application Teams. Pour plus d’informations, consultez [Provisionner des ressources cloud à l’aide de Visual Studio](provision-cloud-resources.md)        |
|Déployer dans le cloud     |Cette option vous permet de copier votre code vers les ressources Azure créées lorsque vous avez effectué « Provisionner dans le cloud ». Pour plus d’informations, consultez [Déployer l’application Teams dans le cloud à l’aide de Visual Studio](deploy-teams-app.md)        |
|Préversion dans Teams     |Cette option lance le client web Teams et vous permet d’afficher un aperçu de l’application Teams dans son navigateur.         |
|Package d’application zip     |Cette option génère un package d’application Teams dans le `Build` dossier sous le projet. Vous pouvez charger le package sur le client Teams et exécuter l’application Teams.         |

Les opérations suivantes ne sont pas encore prises en charge dans le Kit de ressources Teams pour Visual Studio par rapport à Teams Toolkit pour Visual Studio Code, mais elles sont planifiées dans la feuille de route du produit à venir.

* Ajoutez d’autres fonctionnalités Teams à votre application Teams.
* Ajouter d’autres ressources Azure à votre application Teams
* Ajoutez l’authentification unique à votre application Teams.
* Ajoutez une connexion d’API à votre application Teams.
* Personnalisez le manifeste Azure AD.
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

## <a name="see-also"></a>Voir aussi

* [Créer une application Teams dans Visual Studio](create-new-teams-app-for-Visual-Studio.md)
* [Provisionner des ressources cloud à l’aide de Visual Studio](provision-cloud-resources.md)
* [Déployer une application Teams dans le cloud à l’aide de Visual Studio](deploy-teams-app.md)
