---
title: Déboguer votre application Teams localement
author: surbhigupta
description: Dans ce module, découvrez comment déboguer votre application Teams localement dans le Kit de ressources Teams et les principales fonctionnalités du Kit de ressources Teams
ms.author: v-amprasad
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/21/2022
ms.openlocfilehash: 68999351232deb60015259840147d2a1ab55681a
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/07/2022
ms.locfileid: "67616549"
---
# <a name="debug-your-microsoft-teams-app-locally"></a>Déboguer votre application Microsoft Teams localement

Microsoft Teams Toolkit vous aide à déboguer et à afficher un aperçu de votre application Teams localement. Pendant le processus de débogage, le Kit de ressources Teams démarre automatiquement les services d’application, lance les débogueurs et charge l’application Teams de manière test. Vous pouvez afficher un aperçu de votre application Teams dans le client web Teams localement après le débogage. Vous devez configurer Teams Toolkit avant de déboguer votre application.

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

## <a name="see-also"></a>Voir aussi

* [Utiliser Teams Shared Computer Toolkit pour mettre en service des ressources cloud](provision.md)
* [Ajouter des fonctionnalités à vos applications Teams](add-capability.md)
* [Déployer à partir du cloud](deploy.md)
* [Gérer plusieurs environnements dans Teams Shared Computer Toolkit](TeamsFx-multi-env.md)
