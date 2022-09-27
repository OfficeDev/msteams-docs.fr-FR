---
title: Déboguer votre application Teams localement
author: surbhigupta
description: Dans ce module, découvrez comment déboguer votre application Teams localement dans le Kit de ressources Teams et les principales fonctionnalités du Kit de ressources Teams
ms.author: v-amprasad
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/21/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: 24d231ef7a76ede1d45176d5869caa9a76a791be
ms.sourcegitcommit: c1032ea4f48c4bbf5446798ff7d46d7e6e9f55d2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2022
ms.locfileid: "68026961"
---
# <a name="debug-your-teams-app-locally"></a>Déboguer votre application Teams localement

Teams Toolkit vous aide à déboguer et à afficher un aperçu de votre application Microsoft Teams localement. Pendant le processus de débogage, le Kit de ressources Teams démarre automatiquement les services d’application, lance les débogueurs et charge l’application Teams de manière test. Vous pouvez afficher un aperçu de votre application Teams dans le client web Teams localement après le débogage.

::: zone pivot="visual-studio-code"

## <a name="debug-your-microsoft-teams-app-locally-for-visual-studio-code"></a>Déboguer votre application Microsoft Teams localement pour Visual Studio Code

Le Kit de ressources Teams dans Visual Studio Code vous offre les fonctionnalités permettant d’automatiser le débogage de votre application Teams localement. Visual Studio vous permet de déboguer l’extension d’onglet, de bot et de message. Vous devez configurer Teams Toolkit avant de déboguer votre application.

## <a name="set-up-your-teams-toolkit-for-debugging"></a>Configurer votre kit de ressources Teams pour le débogage

Les étapes suivantes vous aident à configurer votre Kit de ressources Teams avant de lancer le processus de débogage :

# <a name="windows"></a>[Fenêtres](#tab/Windows)

1. Sélectionnez **Déboguer (Edge)** ou **Déboguer (Chrome)** dans la barre d’activité dans la liste déroulante **RUN AND DEBUG ▷** .

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/debug-run.png" alt-text="Option de navigateur":::

1. Sélectionnez **Exécuter** > **démarrer le débogage (F5).**

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/start-debugging.png" alt-text="Démarrer le débogage":::

3. Sélectionnez **Comptes** et connectez-vous à votre compte Microsoft 365.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/microsoft365-signin.png" alt-text="Connexion":::

   > [!TIP]
   > Vous pouvez sélectionner **En savoir plus pour** en savoir plus sur Microsoft 365 programme pour les développeurs. Votre navigateur web par défaut s’ouvre pour vous permettre de vous connecter à votre compte Microsoft 365 avec vos informations d’identification.

4. Sélectionnez **Installer** pour installer le certificat de développement pour localhost.

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/install-certificate.png" alt-text="Certificat":::

   > [!TIP]
   > Vous pouvez sélectionner **En savoir plus** sur le certificat de développement.

5. Sélectionnez **Oui** dans la boîte **de dialogue Avertissement de sécurité** :

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/development-certificate.png" alt-text="Autorité de certification":::

Toolkit lance une nouvelle instance du navigateur Edge ou Chrome en fonction de votre sélection et ouvre une page web pour charger le client Teams.  

# <a name="macos"></a>[MacOS](#tab/macOS)

1. Sélectionnez **Debug Edge** ou **Debug Chrome** dans la liste **déroulante RUN AND DEBUG ▷** .

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/debug-run.png" alt-text="Listes des navigateurs":::

1. **Sélectionnez Démarrer le débogage (F5)** ou **Exécuter** pour exécuter votre application Teams en mode débogage.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/start-debugging.png" alt-text="Déboguer votre application":::

3. Sélectionnez **Comptes** et connectez-vous à votre compte Microsoft 365.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/microsoft365-signin.png" alt-text="Se connectee au compte M365":::

   > [!TIP]
   > Vous pouvez sélectionner **En savoir plus pour** en savoir plus sur Microsoft 365 programme pour les développeurs. Votre navigateur web par défaut s’ouvre pour vous laisser vous Microsoft 365 à l’aide de vos informations d’identification.

4. Sélectionnez **Installer** pour installer le certificat de développement pour localhost.

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/install-certificate.png" alt-text="Certificat":::

   > [!TIP]
   > Vous pouvez sélectionner **En savoir plus** sur le certificat de développement.

5. Entrez votre **nom d’utilisateur** et **votre mot de passe**, puis sélectionnez **Mettre à jour les paramètres**.

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/mac-settings.png" alt-text="se connecter à mac":::

Teams Toolkit lance votre instance de navigateur et ouvre une page web pour charger le client Teams.

---

## <a name="debug-your-app"></a>Déboguer votre application

Après le processus de configuration initiale, Teams Toolkit démarre les processus suivants :

* [Démarre les services d’application](#starts-app-services).
* [Lance les configurations de débogage](#launches-debug-configurations)
* [Désactiver l'application Teams](#sideloads-the-teams-app)

### <a name="starts-app-services"></a>Démarre les services d’application.

Exécute des tâches telles que définies dans `.vscode/tasks.json`.

|  Composant |  Nom de la tâche  | Folder |
| --- | --- | --- |
|  Tab |  **Démarrer frontal** |  onglets |
|  Extensions de bot ou de message |  **Démarrer le bot** |  robot |
|  Azure Functions |  **Démarrer le back-end** |  API |

L’image suivante affiche les noms des tâches dans les onglets **OUTPUT** et **TERMINAL** de Visual Studio Code lors de l’exécution de l’onglet, du bot ou de l’extension de message, et Azure Functions.

:::image type="content" source="../assets/images/teams-toolkit-v2/debug/Terminal.png" alt-text="Démarrer les services d’application":::

### <a name="launches-debug-configurations"></a>Lance les configurations de débogage

Lance les configurations de débogage telles que définies dans `.vscode/launch.json`.

:::image type="content" source="../assets/images/teams-toolkit-v2/debug/launch-debuggers.png" alt-text="Débogueur de lancement":::

Le tableau suivant répertorie les noms et types de configuration de débogage pour le projet avec l’application d’extension de tabulation, de bot ou de message, et Azure Functions :

|  Composant |  Nom de configuration de débogage  | Type de configuration de débogage |
| --- | --- | --- |
|  Tab |  **Attacher au frontal (Edge)** ou **attacher au frontal (Chrome)**  |  pwa-msedge ou pwa-chrome  |
|  Extensions de bot ou de message |   **Attacher au bot** |  pwa-node |
| Azure Functions |   **Attacher au backend** |  pwa-node |

Le tableau suivant répertorie les noms et types de configuration de débogage pour le projet avec application bot, Azure Functions et sans application onglet :

|  Composant |  Nom de configuration de débogage  | Type de configuration de débogage  |
| --- | --- | --- |
|  Bot ou extension de message  | **Bot de lancement (Edge)** ou  **Bot de lancement (Chrome)**  |   pwa-msedge ou pwa-chrome  |
|  Bot ou extension de message  |   **Attacher au bot** |  pwa-node  |
|  Azure Functions |  **Attacher au backend** |  pwa-node |

### <a name="sideloads-the-teams-app"></a>Désactiver l'application Teams

**L’attachement de configuration au serveur frontal** ou **au bot de** lancement lance une instance de navigateur Edge ou Chrome pour charger le client Teams dans la page web. Une fois le client Teams chargé, Teams charge l’application Teams qui est contrôlée par l’URL de chargement indépendant définie dans les configurations de lancement [de Microsoft Teams](https://teams.microsoft.com/l/app/>${localTeamsAppId}?installAppPackage=true&webjoin=true&${account-hint}). Lorsque le client Teams se charge dans le navigateur web, sélectionnez **Ajouter** ou sélectionner une option dans la liste déroulante en fonction de vos besoins.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/hello-local-debug.png" alt-text="Ajouter un débogage local" lightbox="../assets/images/teams-toolkit-v2/debug/hello-local-debug.png":::

   Votre application est ajoutée à Teams !

## <a name="next"></a>Next

> [!div class="nextstepaction"]
> [Déboguer les processus en arrière-plan](debug-background-process.md)

::: zone-end

::: zone pivot="visual-studio"

## <a name="debug-your-teams-app-locally-using-visual-studio"></a>Déboguer votre application Teams localement à l’aide de Visual Studio

Teams Toolkit vous aide à déboguer et à afficher un aperçu de votre application Microsoft Teams localement. Visual Studio vous permet de déboguer l’extension d’onglet, de bot et de message. Vous pouvez déboguer votre application localement dans Visual Studio à l’aide du Kit de ressources Teams en effectuant les opérations suivantes :

### <a name="set-up-ngrok-only-for-bot-and-message-extension-app"></a>Configurer ngrok (uniquement pour l’application Bot et Extension de message)

Utilisez une invite de commandes pour exécuter cette commande :

```
ngrok http 5130
```

### <a name="set-up-your-teams-toolkit"></a>1. Configurer votre Teams Shared Computer Toolkit

Effectuez les étapes suivantes à l’aide du Kit de ressources Teams pour déboguer votre application après avoir créé un projet :

1. Cliquez avec le bouton droit sur votre **projet**.
1. Sélectionnez **Le kit de ressources** >  Teams **prépare les dépendances d’application Teams**.

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-teamsappdependencies.png" alt-text="Dépendances d’application Teams pour le débogage local" lightbox="../assets/images/debug-teams-app/vs-localdebug-teamsappdependencies.png":::

   > [!NOTE]
   > Dans ce scénario, le nom du projet est MyTeamsApp1

   Votre compte Microsoft 365 doit disposer de l’autorisation de chargement latéral avant de vous connecter.  Assurez-vous que votre application Teams peut être chargée sur le locataire, sinon votre application Teams peut ne pas s’exécuter dans le client Teams.

1. Connectez-vous à votre **compte Microsoft 365**, puis **sélectionnez Continuer**

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-signin-m365.png" alt-text="Se connecter au compte Microsoft 365":::

   > [!Note]
   > En savoir plus sur l’autorisation de chargement indépendant en visitant <https://aka.ms/teamsfx-sideloading-option>.

1. Sélectionnez **Déboguer** > **Démarrer le débogage** ou sélectionnez directement **F5**.

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

::: zone-end

## <a name="see-also"></a>Voir aussi

* [Utiliser Teams Shared Computer Toolkit pour mettre en service des ressources cloud](provision.md)
* [Ajouter des fonctionnalités à vos applications Teams](add-capability.md)
* [Déployer à partir du cloud](deploy.md)
* [Gérer plusieurs environnements dans Teams Shared Computer Toolkit](TeamsFx-multi-env.md)
