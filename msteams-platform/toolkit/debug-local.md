---
title: Déboguer votre Teams application
description: Dans ce module, découvrez comment déboguer votre application Teams localement dans le Kit de ressources Teams et les principales fonctionnalités du Kit de ressources Teams
ms.author: surbhigupta
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/21/2022
ms.openlocfilehash: 5cc1d14122a7977170e3c4fa04aba782b0146af9
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142226"
---
# <a name="debug-your-teams-app-locally"></a>Déboguer votre application Teams localement

Teams Shared Computer Toolkit vous permet de déboguer et de prévisualiser votre application Teams localement. Le débogage est le processus de vérification, de détection et de correction des problèmes ou des bogues pour garantir que le programme s’exécute correctement. Visual Studio Code vous permet de déboguer l’onglet, le bot, l’extension de message et Azure Functions. Teams Shared Computer Toolkit prend en charge les fonctionnalités de débogage suivantes :

* [Démarrer le débogage](#start-debugging)
* [Débogage multi-cibles](#multi-target-debugging)
* [Basculer les points d’arrêt](#toggle-breakpoints)
* [Recharge à chaud](#hot-reload)
* [Arrêter le débogage](#stop-debugging)  

Pendant le processus de débogage, Teams Toolkit démarre automatiquement les services de l'application, lance les débogueurs et met l'application Teams sur la touche. L'application Teams est disponible en avant-première dans le client web Teams en local après débogage. Vous pouvez également personnaliser les paramètres de débogage pour utiliser les points de terminaison de votre robot, le certificat de développement ou le composant de débogage partiel pour charger votre application configurée.

## <a name="prerequisite"></a>Conditions préalables

[Installer la dernière version d’Office](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)

## <a name="key-features-of-teams-toolkit"></a>Principales fonctionnalités de Teams Shared Computer Toolkit

La liste suivante fournit les principales fonctionnalités du Kit de ressources Teams :

### <a name="start-debugging"></a>Démarrer le débogage

Vous pouvez effectuer une seule opération, sélectionnez **F5** pour démarrer le débogage. Le Kit de ressources Teams commence à vérifier les prérequis, inscrit l’application Azure Active Directory, l’application Teams et inscrit le bot, démarre les services et lance le navigateur.

### <a name="multi-target-debugging"></a>Débogage multi-cibles

Teams Toolkit utilise la fonctionnalité de débogage multi-cible pour déboguer simultanément l’onglet, le bot, l’extension de message et Azure Functions.

### <a name="toggle-breakpoints"></a>Basculez les points d’arrêt.

Vous pouvez activer/désactiver les points d’arrêt sur les codes sources des onglets, des bots, des extensions de message et des Azure Functions. Les points d'arrêt s'exécutent lorsque vous interagissez avec l'application Teams dans un navigateur Web. L’image suivante montre les points d’arrêt bascule :

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/toggle-points.png" alt-text="basculez les points d’arrêt":::.

### <a name="hot-reload"></a>Recharge à chaud

Vous pouvez mettre à jour et enregistrer les codes sources de tabulation, de bot, d’extension de message et de Azure Functions en même temps que vous déboguez l’application Teams. L’application se recharge et le débogueur se rattache aux langages de programmation.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/hot-reload.png" alt-text="recharge à chaud pour les codes sources":::

### <a name="stop-debugging"></a>Arrêter le débogage

Lorsque vous avez terminé le débogage local, vous pouvez sélectionner **Arrêter** ou **Déconnecter** dans la barre d'outils de débogage flottante pour arrêter toutes les sessions de débogage et terminer les tâches. L'image suivante montre l'action d'arrêt du débogage :

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/stop-debug.png" alt-text="arrêter le débogage":::

## <a name="debug-your-app-locally"></a>Déboguer votre application localement

Les étapes suivantes vous aident à déboguer votre application Teams localement :

### <a name="set-up-your-teams-toolkit"></a>1. Configurer votre Teams Shared Computer Toolkit

Effectuez les étapes suivantes pour déboguer votre application après avoir créé une nouvelle application à l'aide du Teams Toolkit :

# <a name="windows"></a>[Fenêtres](#tab/Windows)

1. **Sélectionnez Déboguer Edge** **ou Déboguer Chrome** à partir des **paramètres Exécuter et Déboguer** dans la barre d’activité.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/debug-run.png" alt-text="Option de navigateur" border="false":::

1. **Sélectionnez Démarrer le débogage (F5)** ou **Exécuter** pour exécuter votre application Teams en mode débogage.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/start-debugging.png" alt-text="Démarrer le débogage" border="false":::

3. Sélectionnez **Comptes** et connectez-vous à votre compte Microsoft 365.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/microsoft365-signin.png" alt-text="Connexion" border="true":::

   > [!TIP]
   > Vous pouvez sélectionner **En savoir plus pour** en savoir plus sur Microsoft 365 programme pour les développeurs. Votre navigateur web par défaut s’ouvre pour vous laisser vous Microsoft 365 à l’aide de vos informations d’identification.

4. Sélectionnez **Installer** pour installer le certificat de développement pour localhost.

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/install-certificate.png" alt-text="Certificat" border="true":::

   > [!TIP]
   > Vous pouvez sélectionner **En savoir plus** sur le certificat de développement.

5. Sélectionnez **Oui** si la boîte de dialogue suivante s’affiche :

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/development-certificate.png" alt-text="Autorité de certification" border="true":::

Toolkit lance une nouvelle instance du navigateur Edge ou Chrome en fonction de votre sélection et ouvre une page web pour charger le client Teams.  

# <a name="macos"></a>[MacOS](#tab/macOS)

1. **Sélectionnez Déboguer Edge** **ou Déboguer Chrome** à partir des **paramètres Exécuter et Déboguer** dans la barre d’activité.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/debug-run.png" alt-text="Listes des navigateurs" border="false":::

1. **Sélectionnez Démarrer le débogage (F5)** ou **Exécuter** pour exécuter votre application Teams en mode débogage.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/start-debugging.png" alt-text="Déboguer votre application" border="false":::

3. Sélectionnez **Comptes** et connectez-vous à votre compte Microsoft 365.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/microsoft365-signin.png" alt-text="Se connectee au compte M365" border="true":::

   > [!TIP]
   > Vous pouvez sélectionner **En savoir plus pour** en savoir plus sur Microsoft 365 programme pour les développeurs. Votre navigateur web par défaut s’ouvre pour vous laisser vous Microsoft 365 à l’aide de vos informations d’identification.

4. Sélectionnez **Installer** pour installer le certificat de développement pour localhost.

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/install-certificate.png" alt-text="Certificat" border="true":::

   > [!TIP]
   > Vous pouvez sélectionner **En savoir plus** sur le certificat de développement.

5. Entrez votre **nom d’utilisateur** et votre **mot de passe**, puis sélectionnez **Mettre les paramètres à jour** dans la boîte de dialogue suivante :

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/mac-settings.png" alt-text="se connecter à mac" border="true":::

Shared Computer Toolkit lance une nouvelle instance de navigateur Edge ou Chrome en fonction de votre sélection et ouvre une page web pour charger Teams client.

---

### <a name="debug-your-app"></a>Déboguer votre application

Après le processus de mise en place initial, le Teams Shared Computer Toolkit démarre les processus suivants :

<br>

<details>
<summary><b>Démarre les services d’application</b>.</summary>

Exécute les tâches définies comme `.vscode/tasks.json` suit :

|  Composant |  Nom de la tâche  | Folder |
| --- | --- | --- |
|  Tab |  **Démarrer frontal** |  onglets |
|  Extensions de bot ou de message |  **Démarrer le bot** |  robot |
|  Azure Functions |  **Démarrer le back-end** |  API |

L’image suivante affiche les noms des tâches sous l’onglet **Sortie****Terminal** de Visual Studio Code lors de l’exécution de l’onglet, de l’extension de bot ou de message, et Azure Functions.

:::image type="content" source="../assets/images/teams-toolkit-v2/debug/Terminal.png" alt-text="Démarrer les services d’application":::

</details>
<details>
<summary><b>Lance les débogueurs</b>.</summary>

Lance les configurations de débogage définies comme `.vscode/launch.json` suit :

:::image type="content" source="../assets/images/teams-toolkit-v2/debug/launch-debuggers.png" alt-text="Débogueur de lancement":::

Le tableau suivant répertorie les noms et types de configuration de débogage pour le projet avec application onglet et application bot :

|  Composant |  Nom de configuration de débogage  | Type de configuration de débogage |
| --- | --- | --- |
|  Tab |  **Attacher au frontal (Edge)** ou **attacher au frontal (Chrome)**  |  pwa-msedge ou pwa-chrome  |
|  Extensions de bot ou de message |   **Attacher au bot** |  pwa-node |
| Azure Functions |   **Attacher au backend** |  pwa-node |

Le tableau suivant répertorie les noms et les types de configuration de débogage pour le projet avec bot app et sans tab app :

|  Composant |  Nom de configuration de débogage  | Type de configuration de débogage  |
| --- | --- | --- |
|  Bot ou extension de message  | **Bot de lancement (Edge)** ou  **Bot de lancement (Chrome)**  |   pwa-msedge ou pwa-chrome  |
|  Bot ou extension de message  |   **Attacher au bot** |  pwa-node  |
|  Azure Functions |  **Attacher au backend** |  pwa-node |

</details>
<details>
<summary><b>Désactiver l'application Teams</b></summary>

La configuration **Attacher au bot frontal** ou **de lancement** lance une nouvelle instance de navigateur Edge ou Chrome et ouvre une page web pour charger Teams client. Une fois le client Teams chargé, Teams sideload l'application Teams contrôlée par l'URL sideload définie dans les configurations de lancement [Microsoft Teams](https://teams.microsoft.com/l/app/>${localTeamsAppId}?installAppPackage=true&webjoin=true&${account-hint}). Lorsque Teams client se charge dans le navigateur web, sélectionnez **Ajouter** ou sélectionner un client dans la liste de listes.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/hello-local-debug.png" alt-text="débogage local" border="true":::

   Votre application est ajoutée à Teams !

</details>

## <a name="customize-debug-settings"></a>Personnaliser les paramètres de débogage

Teams Toolkit supprime certains prérequis et vous permet de personnaliser les paramètres de débogage pour créer votre onglet ou votre robot :

<br>

<details>
<summary><b>Utiliser le point de terminaison de votre bot</b></summary>

1. Dans Visual Studio Code paramètres, **assurez-vous que Ngrok est installé et démarré (ngrok).**

1. Définissez `siteEndpoint`la configuration`.fx/configs/config.local.json` de votre point de terminaison.

```json
{
    "bot": {
        "siteEndpoint": "https://your-bot-tunneling-url"
    }
}

```

:::image type="content" source="../assets/images/teams-toolkit-v2/debug/bot-endpoint.png" alt-text="Personnaliser le point de terminaison du bot":::

</details>

<details>
<summary><b>Utiliser votre certificat de développement</b></summary>

1. Dans Visual Studio Code paramètres de développement, désévérez vérifier que le certificat de développement est **approuvé (devCert).**

1. Définissez la configuration de `sslCertFile` et `sslKeyFile` dans `.fx/configs/config.local.json` sur le chemin d’accès au fichier du certificat et le chemin d’accès au fichier clé.

```json
{
    "frontend": {
        "sslCertFile": "",
        "sslKeyFile": ""
    }
}
```

:::image type="content" source="../assets/images/teams-toolkit-v2/debug/development-certificate-customize.png" alt-text="Personnaliser le certificat":::

</details>

<details>
<summary><b>Utiliser vos scripts de démarrage pour démarrer les services d’application</b></summary>

1. Pour l’onglet, mettez à jour `dev:teamsfx` le script dans `tabs/package.json`.

1. Pour l’extension de bot ou de message, mettez à jour le script `dev:teamsfx` dans `bot/package.json`.

1. Pour les fonctions Azure, mettez à jour le `dev:teamsfx` script dans `api/package.json` et pour le script de mise à `watch:teamsfx` jour TypeScript.

   > [!NOTE]
   > Actuellement, l’onglet, le bot, les applications d’extension de message et les ports Azure Functions ne prennent pas en charge la personnalisation.

</details>

<details>
<summary><b>Ajouter des variables d’environnement</b></summary>

Vous pouvez ajouter des variables d’environnement à `.env.teamsfx.local` fichier pour l’onglet, le bot, l’extension de message et Azure Functions. Teams Shared Computer Toolkit charge les variables d’environnement que vous avez ajoutées pour démarrer les services pendant le débogage local.

 > [!NOTE]
 > Assurez-vous de démarrer un nouveau débogage local après avoir ajouté de nouvelles variables d'environnement, car celles-ci ne prennent pas en charge le rechargement à chaud.

</details>

<details>
<summary><b>Débogage d’un composant partiel</b></summary>

Teams Toolkit utilise Visual Studio Code débogage multi-cible pour déboguer simultanément l’onglet, le bot, l’extension de message et Azure Functions. Vous pouvez mettre à jour `.vscode/launch.json` et `.vscode/tasks.json` déboguer un composant partiel. Si vous souhaitez déboguer l'onglet uniquement dans un projet tab plus bot avec Azure Functions, utilisez les étapes suivantes :

1. Commentez **joindre au bot** et **joindre au back-end** à partir du composant de débogage dans `.vscode/launch.json`.

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

2. Commentez **démarrer le backend** et démarrer.le bot à partir de Start All Task dans .vscode/tasks.json.

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

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Processus de débogage en arrière-plan](debug-background-process.md)

## <a name="see-also"></a>Voir aussi

* [Utiliser Teams Shared Computer Toolkit pour mettre en service des ressources cloud](provision.md)
* [Ajouter des fonctionnalités à vos applications Teams](add-capability.md)
* [Déployer à partir du cloud](deploy.md)
* [Gérer plusieurs environnements dans Teams Shared Computer Toolkit](TeamsFx-multi-env.md)
