---
author: surbhigupta
title: Déboguer votre application Teams pour Visual Studio
description: Dans ce module, découvrez comment déboguer votre application Teams localement dans Visual Studio à l’aide de Teams Toolkit
ms.author: v-amprasad
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/21/2022
ms.openlocfilehash: cff0b3e18f63bc7943a7fc16875294f41257a37c
ms.sourcegitcommit: 65ae3ccc2312ddc6cdaa05096e30bdf9dca10c3f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2022
ms.locfileid: "68027430"
---
# <a name="debug-your-teams-app-locally-using-visual-studio"></a>Déboguer votre application Teams localement à l’aide de Visual Studio

Teams Toolkit vous aide à déboguer et à afficher un aperçu de votre application Microsoft Teams localement. Le débogage est un processus de création, de vérification, de détection et de correction des problèmes ou bogues dans votre application. Le débogage garantit que le programme s’exécute correctement. Visual Studio vous permet de déboguer l’onglet, le bot et l’extension de message. Teams Shared Computer Toolkit prend en charge les fonctionnalités de débogage suivantes :

* Préparer les dépendances d’application Teams
* Démarrer le débogage
* Basculez les points d’arrêt.
* Recharge à chaud
* Arrêter le débogage

Pendant le processus de débogage, le Kit de ressources Teams démarre automatiquement les services d’application, lance le débogage et charge l’application Teams. Après le débogage, vous pouvez afficher un aperçu de l’application Teams dans le client web Teams. Vous pouvez également personnaliser les paramètres de débogage pour utiliser vos points de terminaison de bot ou des variables d’environnement pour charger votre application configurée.

## <a name="prerequisites"></a>Conditions préalables

| &nbsp; | Installer | Pour l’utilisation... |
| --- | --- | --- |
| &nbsp; | **Obligatoire** | &nbsp; |
| &nbsp; | Visual Studio 2022 version 17.3 | Vous pouvez installer l’édition Entreprise de Visual Studio et installer la charge de travail « ASP.NET » et les outils de développement Microsoft Teams. |
| &nbsp; | Toolkit Teams | Extension Visual Studio qui crée une structure de projet pour votre application. Utilisez la dernière version. |
| &nbsp; | [Microsoft Teams](https://www.microsoft.com/microsoft-teams/download-app) | Microsoft Teams pour collaborer avec toutes les personnes avec lesquelles vous travaillez via les applications pour les conversations, les réunions, les appels, le tout au même endroit. |
| &nbsp; | [Préparer votre client Microsoft Office 365](../concepts/build-and-test/prepare-your-o365-tenant.md) | Accès au compte Teams avec les autorisations appropriées pour installer une application. |
| &nbsp; | [Compte de développeur Microsoft 365](/../concepts/build-and-test/prepare-your-o365-tenant) | Accès au compte Teams avec les autorisations appropriées pour installer une application. |
| &nbsp; | Azure Tools et [Microsoft Azure CLI](/cli/azure/install-azure-cli) | Outils Azure pour accéder aux données stockées ou déployer un backend cloud pour votre application Teams dans Azure. |
|&nbsp;  | **Optional** | &nbsp; |
|&nbsp; |[Ngrok](https://ngrok.com/) | Ngrok est utilisé pour transférer des messages externes d’Azure Bot Framework vers votre ordinateur local.|

## <a name="debug-your-app-locally"></a>Déboguer votre application localement

Vous pouvez déboguer votre application localement dans Visual Studio à l’aide du Kit de ressources Teams en effectuant les opérations suivantes :

### <a name="set-up-ngrok-only-for-bot-and-message-extension-app"></a>Configurer ngrok (uniquement pour l’application Bot et Extension de message)

Utilisez une invite de commandes pour exécuter cette commande :

```
ngrok http 5130
```

### <a name="set-up-your-teams-toolkit"></a>1. Configurer votre Teams Shared Computer Toolkit

Effectuez les étapes suivantes à l’aide du Kit de ressources Teams pour déboguer votre application après avoir créé un projet :

1. Cliquez avec le bouton droit sur votre **projet**.
1. Sélectionnez **Teams Toolkit**.
1. Sélectionnez **Préparer les dépendances d’application Teams**.

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-teamsappdependencies.png" alt-text="Dépendances d’application Teams pour le débogage local":::

   > [!NOTE]
   > Dans ce scénario, le nom du projet est MyTeamsApp1

   Votre compte Microsoft 365 doit disposer de l’autorisation de chargement latéral avant de vous connecter.  Assurez-vous que votre application Teams peut être chargée sur le locataire, sinon votre application Teams peut ne pas s’exécuter dans le client Teams.

1. Connectez-vous à votre **compte Microsoft 365**.
1. Sélectionnez **Continuer**
   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-signin-m365.png" alt-text="la connexion au compte Microsoft 365":::

   > [!Note]
   > En savoir plus sur l’autorisation de chargement indépendant en visitant <https://aka.ms/teamsfx-sideloading-option>.

1. Sélectionnez **Déboguer**.
1. Sélectionnez **Démarrer le débogage** ou sélectionnez directement **F5**.

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-Startdebug.png" alt-text="Démarrer le débogage":::

   Visual Studio lance l’application Teams dans le client Microsoft Teams dans votre navigateur.

   > [!Note]
   > En savoir plus en visitant <https://aka.ms/teamsfx-vs-debug>.

1. Une fois Microsoft Teams chargé, **sélectionnez Ajouter** pour installer votre application dans Teams.

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-add-loadapp.png" alt-text="Sélectionner Ajouter pour charger l’application":::

   > [!TIP]
   > Vous pouvez également utiliser la fonction de rechargement à chaud de Visual Studio pendant le débogage. En savoir plus en visitant <https://aka.ms/teamsfx-vs-hotreload>.

   > [!NOTE]
   > Veillez à publier une requête HTTP sur «<http://localhost:5130/api/notification> » pour déclencher une notification, lorsque vous déboguez l’application Bot de notification. Si vous avez sélectionné le déclencheur HTTP lors de la création du projet, vous pouvez utiliser tous les outils API tels que curl (invite de commandes Windows), Postman, etc.

   > [!TIP]
   > Si vous apportez des modifications au fichier manifeste de l’application Teams (/templates/appPackage/manifest.template.json), veillez à exécuter la commande Préparer les dépendances d’application Teams. Avant d’essayer de réexécuter l’application Teams localement.

## <a name="key-features-of-teams-toolkit"></a>Principales fonctionnalités de Teams Shared Computer Toolkit

Vous pouvez voir les fonctionnalités clés suivantes du Kit de ressources Teams, qui automatisent le processus de débogage local de votre application Teams :

### <a name="prepare-teams-app-dependencies"></a>Préparer les dépendances d’application Teams

Teams Toolkit prépare les dépendances de débogage locales et inscrit votre application Teams dans le locataire de votre compte. Pour les applications Bot et Extension de message, Teams Toolkit s’inscrit et configure le bot.

### <a name="start-debugging"></a>Démarrer le débogage

Vous pouvez effectuer le débogage avec une seule opération, appuyez sur **F5** pour démarrer le débogage. Teams Toolkit génère du code, démarre des services et lance l’application dans votre navigateur.

### <a name="toggle-breakpoints"></a>Basculez les points d’arrêt.

Vous pouvez basculer les points d’arrêt dans les codes sources des onglets, des bots, des extensions de message et des fonctions Azure. Les points d’arrêt s’exécutent lorsque vous interagissez avec l’application Teams dans votre navigateur web.
L’image suivante montre les points d’arrêt bascule :

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-toggle-breakpoint.png" alt-text="Points d’arrêt bascule de débogage local":::

### <a name="hot-reload"></a>Recharge à chaud

Sélectionnez **Rechargement à chaud** pour appliquer vos modifications dans votre application Teams lorsque vous souhaitez mettre à jour et enregistrer les codes sources simultanément pendant le débogage.

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-hot-reload.png" alt-text="Sélectionner l’icône de rechargement à chaud":::

Sélectionnez l’option **Rechargement à chaud sur l’enregistrement de fichier** dans la liste déroulante pour activer le rechargement automatique à chaud.

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-hot-reload-filesave.png" alt-text="Sélectionner le rechargement à chaud lors de l’enregistrement de fichier":::
  
   > [!Tip]
   > Pour en savoir plus sur Rechargement à chaud fonction de Visual Studio pendant le débogage, vous pouvez visiter <https://aka.ms/teamsfx-vs-hotreload>.

### <a name="stop-debugging"></a>Arrêter le débogage

Sélectionnez **Arrêter le débogage** une fois le débogage local terminé.

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-Stopdebug.png" alt-text="Sélectionner l’icône Arrêter le débogage":::

## <a name="customize-debug-settings"></a>Personnaliser les paramètres de débogage

Vous pouvez personnaliser le paramètre de débogage pour votre application Teams afin d’utiliser vos points de terminaison de bot et d’ajouter des variables d’environnement :

### <a name="use-your-bot-endpoint"></a>Utiliser le point de terminaison de votre bot

Vous pouvez définir la configuration siteEndpoint dans **.fx/configs/config.local.json** sur votre point de terminaison.

```
"bot": {
    "siteEndpoint": "https://baidu.com"
}
```

### <a name="add-environment-variables"></a>Ajouter des variables d’environnement

Vous pouvez ajouter **environmentVariables** au fichier **launchSettings.json** .

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-environment-variables.png" alt-text="Ajouter des variables d’environnement personnalisées":::

### <a name="launch-teams-app-as-a-web-app"></a>Lancer l’application Teams en tant qu’application web

Vous pouvez lancer l’application Teams en tant qu’application web au lieu de l’exécuter dans le client Teams.

1. Sélectionnez **Propriétés** > **launchSettings.json** dans Explorateur de solutions panneau sous votre projet.
1. Supprimez « **launchUrl »** du fichier.

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-launch-teamsapp-webapp.png" alt-text="Lancer des équipes en tant qu’application web en supprimant launchurl":::

1. Cliquez avec le bouton droit sur **Solution**.
1. Sélectionnez **Propriétés**.

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-solution-properties.png" alt-text="Cliquez avec le bouton droit sur la solution et sélectionnez les propriétés":::

1. Sélectionnez **Configuration des propriétés** >  de configuration dans la boîte de dialogue.
1. Sélectionnez décocher la zone **Déployer** le processus.
1. Sélectionnez **OK**.

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-disable-deploy.png" alt-text="Décocher le déploiement dans les propriétés de configuration ":::

## <a name="see-also"></a>Voir aussi

* [Provisionner des ressources cloud à l’aide de Visual Studio](provision-cloud-resources.md)
* [Déployer une application Teams dans le cloud à l’aide de Visual Studio](deploy-teams-app.md)
* [Modifier le manifeste de l’application Teams à l’aide de Visual Studio](VS-TeamsFx-preview-and-customize-app-manifest.md)
