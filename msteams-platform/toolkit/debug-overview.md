---
title: Déboguer votre Teams application
author: surbhigupta
description: Dans ce module, découvrez comment déboguer votre application Teams dans le Kit de ressources Teams et les fonctionnalités clés du Kit de ressources Teams
ms.author: v-amprasad
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/21/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: 111f45a8ed0b5246a75d1a1adbda9b124c1e9578
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833148"
---
# <a name="debug-your-teams-app"></a>Déboguer votre Teams application

Teams Toolkit vous permet de déboguer et d’afficher un aperçu de votre application Microsoft Teams. Le débogage est le processus de vérification, de détection et de correction des problèmes ou des bogues pour garantir que le programme s’exécute correctement dans Teams.

::: zone pivot="visual-studio-code"

## <a name="debug-your-teams-app-for-visual-studio-code"></a>Déboguer votre application Teams pour Visual Studio Code

Teams Toolkit dans Microsoft Visual Studio Code automatise le processus de débogage. Vous pouvez détecter les erreurs et les corriger, ainsi qu’afficher un aperçu de l’application Teams. Vous pouvez également personnaliser les paramètres de débogage pour créer votre onglet ou bot.

## <a name="debug-your-microsoft-teams-app-for-visual-studio-code"></a>Déboguer votre application Microsoft Teams pour Visual Studio Code

Teams Toolkit dans Visual Studio Code automatise le processus de débogage. Vous pouvez détecter les erreurs et les corriger, ainsi qu’afficher un aperçu de l’application Teams. Vous pouvez également personnaliser les paramètres de débogage pour créer votre onglet ou bot.

Pendant le processus de débogage :

* Teams Toolkit démarre automatiquement les services d’application, lance les débogueurs et charge une version test de l’application Teams.
* Teams Toolkit vérifie les prérequis pendant le processus de débogage en arrière-plan.
* Votre application Teams est disponible en préversion dans le client web Teams localement après le débogage.
* Vous pouvez également personnaliser les paramètres de débogage pour utiliser les points de terminaison de votre robot, le certificat de développement ou le composant de débogage partiel pour charger votre application configurée.
* Microsoft Visual Studio Code vous permet de déboguer l’onglet, le bot, l’extension de message et Azure Functions.

## <a name="key-debug-features-of-teams-toolkit"></a>Principales fonctionnalités de débogage du Kit de ressources Teams

Teams Shared Computer Toolkit prend en charge les fonctionnalités de débogage suivantes :

* [Démarrer le débogage](#start-debugging)
* [Débogage multi-cibles](#multi-target-debugging)
* [Basculer les points d’arrêt](#toggle-breakpoints)
* [Recharge à chaud](#hot-reload)
* [Arrêter le débogage](#stop-debugging)

Teams Toolkit effectue des fonctions d’arrière-plan pendant le processus de débogage, notamment la vérification des conditions préalables requises pour le débogage. Vous pouvez voir la progression du processus de vérification dans le canal de sortie du Kit de ressources Teams. Dans le processus d’installation, vous pouvez inscrire et configurer votre application Teams.

### <a name="start-debugging"></a>Démarrer le débogage

Vous pouvez appuyer sur **F5** en tant qu’opération unique pour démarrer le débogage. Le Kit de ressources Teams commence à vérifier les prérequis, inscrit l’application Azure Active Directory, l’application Teams et inscrit le bot, démarre les services et lance le navigateur.

### <a name="multi-target-debugging"></a>Débogage multi-cibles

Teams Toolkit utilise la fonctionnalité de débogage multi-cible pour déboguer simultanément l’onglet, le bot, l’extension de message et Azure Functions.

### <a name="toggle-breakpoints"></a>Basculez les points d’arrêt.

Vous pouvez activer/désactiver les points d’arrêt sur les codes sources des onglets, des bots, des extensions de message et des Azure Functions. Les points d'arrêt s'exécutent lorsque vous interagissez avec l'application Teams dans un navigateur Web. L’image suivante montre le point d’arrêt bascule :

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/toggle-points.png" alt-text="basculez les points d’arrêt" lightbox="../assets/images/teams-toolkit-v2/debug/toggle-points.png":::.

### <a name="hot-reload"></a>Recharge à chaud

Vous pouvez mettre à jour et enregistrer les codes sources d’onglet, de bot, d’extension de message et d’Azure Functions en même temps lorsque vous déboguez l’application Teams. L'application se recharge et le débogueur se rattache aux langages de programmation.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/hot-reload.png" alt-text="recharge à chaud pour les codes sources" lightbox="../assets/images/teams-toolkit-v2/debug/hot-reload.png":::

### <a name="stop-debugging"></a>Arrêter le débogage

Lorsque vous avez terminé le débogage local, vous pouvez sélectionner **Arrêter (Maj+F5)** ou **[Alt] Déconnecter (Maj+F5)** dans la barre d’outils de débogage flottante pour arrêter toutes les sessions de débogage et arrêter les tâches. L’image suivante illustre l’action d’arrêt du débogage :

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/stop-debug.png" alt-text="arrêter le débogage":::

## <a name="prepare-for-debug"></a>Préparer le débogage

Les étapes suivantes vous aident à préparer le débogage :

### <a name="sign-in-to-microsoft-365"></a>Connectez-vous à Microsoft 365.

Si vous êtes déjà inscrit à Microsoft 365, connectez-vous à Microsoft 365. Pour plus d’informations, consultez [Programme pour les développeurs Microsoft 365](tools-prerequisites.md#microsoft-365-developer-program)

### <a name="toggle-breakpoints"></a>Basculez les points d’arrêt.

Vérifiez que vous pouvez activer les points d’arrêt sur les codes sources des onglets, des bots, des extensions de message et des Azure Functions pour plus d’informations, consultez [Basculer les points d’arrêt](#toggle-breakpoints).

## <a name="customize-debug-settings"></a>Personnaliser les paramètres de débogage

Teams Toolkit vous permet de personnaliser les paramètres de débogage pour créer votre onglet ou bot. Pour plus d’informations sur la liste complète des options personnalisables, consultez la [documentation sur les paramètres de débogage](https://aka.ms/teamsfx-debug-tasks).

### <a name="customize-scenarios"></a>Personnaliser les scénarios

<br>

<details>

<summary><b>Ignorer les vérifications des prérequis</b></summary>

 > `"prerequisites"``"Validate & install prerequisites"``"args"` > Sous `.fx/configs/tasks.json` , mettez à jour les vérifications des prérequis que vous souhaitez ignorer.

  :::image type="content" source="../assets/images/teams-toolkit-v2/debug/skip-prerequisite-checks.png" alt-text="ignorer les vérifications des prérequis":::

</details>

<details>
<summary><b>Utiliser votre certificat de développement</b></summary>

1. Dans `.fx/configs/tasks.json`, décochez `"devCert"` sous`"prerequisites"``"Validate & install prerequisites"``"args"` >  >  .
1. Définissez « SSL_CRT_FILE » et « SSL_KEY_FILE » dans sur `.env.teamsfx.local` le chemin d’accès au fichier de certificat et au fichier de clé.

</details>

<details>
<summary><b>Personnaliser les arguments d’installation de npm</b></summary>

Dans `.fx/configs/tasks.json`, définissez npmInstallArgs sous `"Install npm packages"`.
  
   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/customize-npm-install.png" alt-text="Installer le package npm":::

</details>

<details>
<summary><b>Modifier les ports</b></summary>

* Bot
  1. `"3978"` Recherchez dans votre projet et recherchez des apparences dans `tasks.json`, `ngrok.yml` et `index.js`.
  1. Remplacez-le par votre port.
     :::image type="content" source="../assets/images/teams-toolkit-v2/debug/modify-ports-bot.png" alt-text="Remplacer votre port par bot":::
* Tab
  1. Dans `.fx/configs/tasks.json`, recherchez `"53000"`.
  1. Remplacez-le par votre port.
     :::image type="content" source="../assets/images/teams-toolkit-v2/debug/modify-ports-tab.png" alt-text="Remplacez votre port par l’onglet":::

</details>

<details>
<summary><b>Utiliser votre propre package d’application</b></summary>

Dans `.fx/configs/tasks.json`, définissez `"appPackagePath"` sous `"Build & upload Teams manifest"` sur le chemin d’accès de votre package d’application.

  :::image type="content" source="../assets/images/teams-toolkit-v2/debug/app-package-path.png" alt-text="utiliser votre propre chemin d’accès au package d’application":::

</details>

<details>
<summary><b>Utiliser votre propre tunnel</b></summary>

1. `"Start Teams App Locally"`Sous `.fx/configs/tasks.json` , vous pouvez mettre à jour `"Start Local tunnel"`.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/start-local-tunnel.png" alt-text="Utiliser votre propre tunnel":::
1. Lancez votre propre service de tunnel, puis mettez à jour `"botMessagingEndpoint"` vers votre propre point de terminaison de message dans sous `.fx/configs/tasks.json` `"Set up bot"`.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/set-up-bot.png" alt-text="mettre à jour le point de terminaison de messagerie":::

</details>

<details>

<summary><b>Ajouter des variables d’environnement</b></summary>

Vous pouvez ajouter des variables d’environnement à `.env.teamsfx.local` fichier pour l’onglet, le bot, l’extension de message et Azure Functions. Teams Shared Computer Toolkit charge les variables d’environnement que vous avez ajoutées pour démarrer les services pendant le débogage local.

 > [!NOTE]
 > Veillez à démarrer un nouveau débogage local après avoir ajouté de nouvelles variables d’environnement, car les variables d’environnement ne prennent pas en charge le rechargement à chaud.

</details>

<details>
<summary><b>Débogage d’un composant partiel</b></summary>

Teams Toolkit utilise Visual Studio Code débogage multi-cible pour déboguer simultanément l’onglet, le bot, l’extension de message et Azure Functions. Vous pouvez mettre à jour `.vscode/launch.json` et `.vscode/tasks.json` déboguer un composant partiel. Si vous souhaitez déboguer l'onglet uniquement dans un projet tab plus bot avec Azure Functions, utilisez les étapes suivantes :

1. Mettez à jour `"Attach to Bot"` et `"Attach to Backend"` à partir du composé de débogage dans `.vscode/launch.json`.

   ```json
   {
       "name": "Debug (Edge)",
        "configurations": [
           "Attach to Frontend (Edge)",
           // "Attach to Bot",
           // "Attach to Backend""
           ],
           "preLaunchTask": "Pre Debug Check & Start All",
           "presentation": {
               "group": "all",
               "order": 1
           },
           "stopAll": true

   }
   ```

2. Mettre à jour `"Start Backend"` et `"Start Bot"` à partir de La tâche Démarrer tout dans .vscode/tasks.json.

   ```json
   {
                                           
       "label": "Start All",
       "dependsOn": [
           "Start Frontend",
             // "Start Backend",
             // "Start Bot"

         ]
              
   }
   ```

</details>

## <a name="next"></a>Next

> [!div class="nextstepaction"]
> [Déboguer votre application localement](debug-local.md)

::: zone-end

::: zone pivot="visual-studio"

## <a name="debug-your-teams-app-using-visual-studio"></a>Déboguer votre application Teams à l’aide de Visual Studio

Teams Toolkit automatise les services de démarrage d’application, lance le débogage et charge l’application Teams. Après le débogage, vous pouvez afficher un aperçu de l’application Teams dans le client web Teams. Vous pouvez également personnaliser les paramètres de débogage pour utiliser vos points de terminaison de bot ou des variables d’environnement pour charger votre application configurée. Visual Studio vous permet de déboguer l’onglet, le bot et l’extension de message. Pendant le processus de débogage, Teams Toolkit prend en charge les fonctionnalités de débogage suivantes :

* Préparer les dépendances d’application Teams
* Démarrer le débogage
* Basculez les points d’arrêt.
* Recharge à chaud
* Arrêter le débogage

## <a name="prerequisites"></a>Configuration requise

| &nbsp; | Installer | Pour l’utilisation... |
| --- | --- | --- |
| &nbsp; | **Obligatoire** | &nbsp; |
| &nbsp; | Visual Studio 2022 version 17.3 | Vous pouvez installer l’édition Entreprise de Visual Studio et installer la charge de travail « ASP.NET » et les outils de développement Microsoft Teams. |
| &nbsp; | Toolkit Teams | Extension Visual Studio qui crée une structure de projet pour votre application. Utilisez la dernière version. |
| &nbsp; | [Microsoft Teams](https://www.microsoft.com/microsoft-teams/download-app) | Microsoft Teams pour collaborer avec toutes les personnes avec lesquelles vous travaillez via les applications pour les conversations, les réunions, les appels, le tout au même endroit. |
| &nbsp; | [Préparer votre client Microsoft Office 365](../concepts/build-and-test/prepare-your-o365-tenant.md) | Accès au compte Teams avec les autorisations appropriées pour installer une application. |
| &nbsp; | [Compte de développeur Microsoft 365](../concepts/build-and-test/prepare-your-o365-tenant.md) | Accès au compte Teams avec les autorisations appropriées pour installer une application. |
| &nbsp; | Outils Azure et [Microsoft Azure CLI](/cli/azure/install-azure-cli) | Outils Azure permettant d’accéder aux données stockées ou de déployer un back-end basé sur le cloud pour votre application Teams dans Azure. |
|&nbsp;  | **Optional** | &nbsp; |
|&nbsp; |[Ngrok](https://ngrok.com/) | Ngrok est utilisé pour transférer des messages externes d’Azure Bot Framework à votre ordinateur local.|

## <a name="key-features-of-teams-toolkit"></a>Principales fonctionnalités de Teams Shared Computer Toolkit

Vous pouvez voir les fonctionnalités clés suivantes du Kit de ressources Teams, qui automatisent le processus de débogage local de votre application Teams :

### <a name="prepare-teams-app-dependencies"></a>Préparer les dépendances d’application Teams

Teams Toolkit prépare les dépendances de débogage locales et inscrit votre application Teams dans le locataire de votre compte. Pour les applications Bot et Extension de message, Teams Toolkit inscrit et configure le bot.

### <a name="start-debugging"></a>Démarrer le débogage

Vous pouvez effectuer le débogage avec une seule opération, appuyez sur **F5** pour démarrer le débogage. Teams Toolkit génère du code, démarre des services et lance l’application dans votre navigateur.

### <a name="toggle-breakpoints"></a>Basculez les points d’arrêt.

Vous pouvez activer/désactiver les points d’arrêt dans les codes sources des onglets, des bots, des extensions de message et des fonctions Azure. Les points d’arrêt s’exécutent lorsque vous interagissez avec l’application Teams dans votre navigateur web.
L’image suivante montre les points d’arrêt bascule :

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-toggle-breakpoint.png" alt-text="Basculement des points d’arrêt de débogage locaux" lightbox="../assets/images/debug-teams-app/vs-localdebug-toggle-breakpoint.png":::

### <a name="hot-reload"></a>Recharge à chaud

Sélectionnez **Rechargement à chaud** pour appliquer vos modifications dans votre application Teams lorsque vous souhaitez mettre à jour et enregistrer les codes sources simultanément pendant le débogage.

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-hot-reload.png" alt-text="Sélectionner l’icône de rechargement à chaud":::

Sélectionnez l’option **Rechargement à chaud enregistrer le fichier** dans la liste déroulante pour activer le rechargement automatique à chaud.

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-hot-reload-filesave.png" alt-text="Sélectionner le rechargement à chaud lors de l’enregistrement de fichier":::
  
   > [!Tip]
   > Pour en savoir plus sur Rechargement à chaud fonction de Visual Studio pendant le débogage, vous pouvez visiter <https://aka.ms/teamsfx-vs-hotreload>.

### <a name="stop-debugging"></a>Arrêter le débogage

Sélectionnez **Arrêter le débogage** une fois le débogage local terminé.

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-Stopdebug.png" alt-text="Sélectionner l’icône Arrêter le débogage":::

## <a name="customize-debug-settings"></a>Personnaliser les paramètres de débogage

Vous pouvez personnaliser le paramètre de débogage pour votre application Teams afin d’utiliser les points de terminaison de votre bot et d’ajouter des variables d’environnement :

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

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-launch-teamsapp-webapp.png" alt-text="Lancer teams en tant qu’application web en supprimant launchurl" lightbox="../assets/images/debug-teams-app/vs-localdebug-launch-teamsapp-webapp.png":::

1. Cliquez avec le bouton droit sur **Solution** , puis sélectionnez **Propriétés**.

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-solution-properties.png" alt-text="Cliquez avec le bouton droit sur la solution et sélectionnez propriétés" lightbox="../assets/images/debug-teams-app/vs-localdebug-solution-properties.png":::

1. Sélectionnez **Propriétés** >  de configuration **Configuration** dans la boîte de dialogue.
1. Décochez la case **Déployer** .
1. Sélectionnez **OK**.

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-disable-deploy.png" alt-text="Décochez déployer dans les propriétés de configuration." lightbox="../assets/images/debug-teams-app/vs-localdebug-disable-deploy.png":::

::: zone-end

## <a name="see-also"></a>Voir aussi

* [Processus de débogage en arrière-plan](debug-background-process.md)
* [Utiliser Teams Shared Computer Toolkit pour mettre en service des ressources cloud](provision.md)
* [Déployer à partir du cloud](deploy.md)
* [Prévisualiser et personnaliser le manifeste de l'application Teams](TeamsFx-preview-and-customize-app-manifest.md)
