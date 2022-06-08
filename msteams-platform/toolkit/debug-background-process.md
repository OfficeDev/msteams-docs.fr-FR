---
title: Déboguer les processus en arrière-plan
author: zyxiaoyuer
description: Fonctionnement du code Visual studio et du Teams Toolkit pendant le débogage local
ms.author: surbhigupta
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/03/2022
ms.openlocfilehash: d692f3f6869767e4b9948b36e521a56d799ebe4b
ms.sourcegitcommit: ff31cbe4840191f004d8fc61dd4fd93d35fcaecb
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/07/2022
ms.locfileid: "65938925"
---
# <a name="debug-background-processes"></a>Déboguer les processus en arrière-plan

Le flux de travail de débogage local implique les fichiers `.vscode/launch.json`et`.vscode/tasks.json` pour configurer le débogueur dans Visual Studio Code (VS Code). Le code VS lance les débogueurs, et Microsoft Edge ou Google Chrome lance une nouvelle instance de navigateur comme suit :

1. Le fichier `launch.json` configure le débogueur dans Visual Studio Code.

2. Visual Studio Code exécute le fichier composé **preLaunchTask**, **Vérification de pré-débogage et démarrer tout** dans le fichier `.vscode/tasks.json`.

3. Visual Studio Code lance ensuite les débogueurs spécifiés dans les configurations de fichier composé, telles que **Attacher au bot**, **Attacher au serveur principal**, **Attacher au serveur frontal** et **Lancer le bot**.

4. Microsoft Edge ou Google Chrome lance une nouvelle instance de navigateur et ouvre une page web pour charger le client Teams.

## <a name="prerequisites"></a>Conditions préalables

Teams Toolkit vérifie les conditions préalables suivantes pendant le processus de débogage :

* Node.js, applicable pour les types de projets suivants :

  |Type de projet|Version LTS Node.js|
  |----------|--------------------------------|
  |Tab | 14, 16 (recommandé) |
  |Onglet SPFx | 12, 14 (recommandé)|
  |Bot |  14, 16 (recommandé)|
  |Extension de message | 14, 16 (recommandé) |

* Si vous avez un compte Microsoft 365 avec des informations d'identification valides, le Teams Toolkit vous invite à vous connecter au compte Microsoft 365, si vous ne l'avez pas encore fait.
* Le chargement indépendant ou le chargement d’une application personnalisée pour votre locataire développeur est activé. Si ce n’est pas le cas, le débogage local se termine.
* La version binaire de Ngrok 2.3 est applicable pour l'extension des robots et des messages. Si Ngrok n'est pas installé ou si la version ne correspond pas aux exigences, le Teams Toolkit installe le paquet Ngrok NPM `ngrok@4.2.2`dans`~/.fx/bin/ngrok` le fichier . Le paquet NPM Ngrok gère le`/.fx/bin/ngrok/node modules/ngrok/bin` binaire Ngrok.
* Azure Functions Core Tools version 3, si Azure Functions Core Tools n'est pas installé ou si la version ne correspond pas aux exigences, le Teams Toolkit installe le paquet NPM Azure Functions Core Tools, azure-functions-core-tools@3 pour **Windows** et pour **macOs** dans`~/.fx/bin/func`.. Le package NPM Azure Functions Core Tools gère `~/.fx/bin/func/node_modules/azure-functions-core-tools/bin` les outils azure Functions Core Tools binaires. Pour Linux, le débogage local se termine.
* Version du SDK .NET Core applicable à Azure Functions, si le SDK .NET Core n'est pas installé ou si la version ne correspond pas aux exigences, le Teams Toolkit installe le SDK .NET Core pour Windows et MacOS dans `~/.fx/bin/dotnet`. Pour Linux, le débogage local se termine.
* La version binaire de Ngrok 2.3 est applicable pour l'extension des robots et des messages. Si Ngrok n'est pas installé ou si la version ne correspond pas aux exigences, le Teams Toolkit installe le paquet Ngrok NPM `ngrok@4.2.2`dans`~/.fx/bin/ngrok` le fichier . Le fichier binaire Ngrok est géré par le package NPM Ngrok dans `/.fx/bin/ngrok/node modules/ngrok/bin`.
* Azure Functions Core Tools version 4, si Azure Functions Core Tools n’est pas installé ou si la version ne correspond pas à la configuration requise, le Kit de ressources Teams installe Azure Functions Core Tools package NPM, azure-functions-core-tools@3 pour **Windows** et pour **MacOs** dans `~/.fx/bin/func`. Le paquet Azure Functions Core Tools NPM gère le binaire `~/.fx/bin/func/node_modules/azure-functions-core-tools/bin`Azure Functions Core Tools. Pour Linux, le débogage local se termine.
* Version applicable du Kit de développement logiciel (SDK) .NET Core pour Azure Functions. Si le Kit de développement logiciel (SDK) .NET Core n’est pas installé ou si la version ne correspond pas à la configuration requise, le Kit de ressources Teams installe le Kit de développement logiciel (SDK) .NET Core pour Windows et MacOS dans `~/.fx/bin/dotnet`. Pour Linux, le débogage local se termine.

  Le tableau suivant répertorie les versions .NET Core :

  | Plateforme  | Logiciels|
  | --- | --- |
  |Windows, macOs (x64) et Linux | **3.1 (recommandé)**, 5.0, 6.0 |
  |macOs (arm64) |6.0 |

* Certificat de développement, si le certificat de développement pour localhost n'est pas installé pour l'onglet dans Windows ou MacOS, le Teams Toolkit vous invite à l'installer.
* Extensions de liaison Azure Functions définies dans `api/extensions.csproj`. Si les extensions de liaison Azure Functions ne sont pas installées, le Kit de ressources Teams installe des extensions de liaison Azure Functions.
* Packages NPM, applicables à l'application tabulation, application de robot, à l'application d'extension de messagerie et aux fonctions Azure. Si NPM n’est pas installé, le Kit de ressources Teams installe tous les packages NPM.
* Extension de bot et de message. Le Kit de ressources Teams démarre Ngrok pour créer un tunnel HTTP pour le bot et l’extension de message.
* Ports disponibles. Si les ports tabulation, bot, extension de message et Azure Functions ne sont pas disponibles, le débogage local se termine.

  Le tableau suivant répertorie les ports disponibles pour les composants :

  | Composant  | Port |
  | --- | --- |
  | Tab | 53000 |
  | Bot ou extension de message | 3978 |
  | Inspecteur de nœud pour l’extension de bot ou de messagerie | 9239 |
  | Azure Functions | 7071 |
  | Inspecteur de nœud pour les fonctions Azure | 9229 |

<!-- The following table lists the limitations if the required software is unavailable for debugging:

|Project type|Installation| Limitation|
|----------|--------------------------------|-----|
|Tab without Azure functions | Node.js LTS versions 10, 12, **14 (recommended)**, 16 | The local debug terminates, if Node.js isn't installed or the version doesn't match the requirement.|
|Tab with Azure functions | Node.js LTS versions 10, 12, **14 (recommended)** |The local debug terminates, if Node.js isn't installed or the version doesn't match the requirement.|
|Bot | Node.js LTS versions 10, 12, **14 (recommended)**, 16|The local debug terminates, if Node.js isn't installed or the version doesn't match the requirement.|
|Message extension | Node.js LTS versions 10, 12, **14 (recommended)**, 16 |The local debug terminates, if Node.js isn't installed or the version doesn't match the requirement.|
|Sign-in to Microsoft 365 account | Microsoft 365 credentials |Teams Toolkit prompts you to sign-in to Microsoft 365 account, if you haven't signed in. |
|Bot, message extension | Ngrok version 2.3| • If Ngrok isn't installed or the version doesn't match the requirement, the Teams Toolkit installs Ngrok NPM package `ngrok@4.2.2` in `~/.fx/bin/ngrok`. </br> • The Ngrok binary is managed by Ngrok NPM package in `/.fx/bin/ngrok/node modules/ngrok/bin`.|
|Azure functions | Azure Functions Core Tools version 3| • If Azure Functions Core Tools isn't installed or the version doesn't match the requirement, the Teams Toolkit installs Azure Functions Core Tools NPM package, azure-functions-core-tools@3 for **Windows** and for **macOs** in  `~/.fx/bin/func`. </br> • The Azure Functions Core Tools NPM package in `~/.fx/bin/func/node_modules/azure-functions-core-tools/bin` manages Azure Functions Core Tools binary. For Linux, the local debug terminates.|
|Azure functions |.NET Core SDK version|• If .NET Core SDK isn't installed or the version  doesn't match the requirement, the Toolkit installs .NET Core SDK for Windows and macOS in `~/.fx/bin/dotnet`.</br> • For Linux, the local debug terminates.|
|Azure functions | Azure functions binding extensions defined in `api/extensions.csproj`| If Azure functions binding extensions isn't installed, the Toolkit installs Azure functions binding extensions.|
|NPM packages| NPM packages for tab app, bot app, message extension app, and Azure functions|If NPM isn't installed, the Toolkit installs all NPM packages.|
|Bot and message extension | Ngrok |Toolkit starts Ngrok to create a HTTP tunnel for bot and message extension. |

> [!NOTE]
> If tab, bot, message extension, and Azure functions ports are unavailable, the local debug terminates.

Use the following .NET Core versions:

| Platform  | Software|
| --- | --- |
|Windows, macOs (x64), Linux | **3.1 (recommended)**, 5.0, 6.0 |
|macOs (arm64) |6.0 |

> [!NOTE]
> If the development certificate for localhost isn't installed for tab in Windows or MacOS, the Teams Toolkit prompts you to install it.</br> -->

Lorsque vous sélectionnez **Lancer le débogage (F5)**, le canal de sortie du Teams Toolkit affiche la progression et le résultat de la vérification des conditions préalables.

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/prerequisites-debugcheck.png" alt-text="Conditions préalables":::

## <a name="register-and-configure-teams-app"></a>Enregistrer et configurer l'application Teams

Au cours du processus d'installation, le Kit de ressources Teams prépare les enregistrements et les configurations suivants pour votre application Teams :

1. [Enregistre et configure l'application Azure AD](#registers-and-configures-azure-ad-application) : Teams Toolkit enregistre et configure votre application Azure AD.

1. [Inscrit et configure le bot](#registers-and-configures-bot) : le Kit de ressources Teams inscrit et configure votre bot pour l’application d’onglet ou d’extension de message.

1. [Enregistre et configure l'application Teams](#registers-and-configures-teams-app): Teams Toolkit enregistre et configure votre application Teams.

### <a name="registers-and-configures-azure-ad-application"></a>Enregistrement et configuration de l'application Azure AD

1. Inscrire une application Azure AD.

1. Crée une secret client.

1. Expose une API.

    a. Configure l'URI d'identification de l'application. Pour l’onglet, `api://localhost/{appId}`. Pour l’extension de bot ou de message,  `api://botid-{botid}`.

    b. Ajoute une étendue nommée `access_as_user`. L’active pour les **administrateurs et les utilisateurs**.

4. Configure les autorisations d’API. Ajoute l’autorisation Graph Microsoft à **User.Read**.

    Le tableau suivant répertorie la configuration de l’authentification comme suit :

      | Type de projet | URIs de redirection pour le web | URIs de redirection pour une application à page unique |
      | --- | --- | --- |
      | Tab | `https://localhost:53000/auth-end.html` | `https://localhost:53000/auth-end.html?clientId={appId>}` |
      | Bot ou extension de message | `https://ngrok.io/auth-end.html` | N/A |

    Le tableau suivant répertorie les configurations de l'application client Microsoft 365 avec les ID client :

      | Application client Microsoft 365 | ID du client |
      | --- | --- |
      | Teams bureau, mobile | 1fec8e78-bce4-4aaf-ab1b-5451cc387264 |
      | Web Teams | 5e3ce6c0-2b1f-4285-8d4b-75ee78787346 |
      | Office.com | 4345a7b9-9a63-4910-a426-35363201d503 |
      | Office.com | 4765445b-32c6-49b0-83e6-1d93765276ca |
      | Version de bureau d’Office | 0ec893e0-5785-4de6-99da-4ed124e5296c |
      | Version de bureau d’Outlook | d3590ed6-52b3-4102-aeff-aad2292ab01c |
      | Outlook Web Access | 00000002-0000-0ff1-ce00-000000000000 |
      | Outlook Web Access | bc59ab01-8403-45c6-8796-ac3ef710b3e3 |

### <a name="registers-and-configures-bot"></a>Enregistre et configure le bot

Pour l’application d’onglet ou l’application d’extension de messagerie :

1. Inscrire une application Azure AD.

1. Crée une secret client pour l’application Azure AD client.

1. Enregistre un bot dans [Microsoft Bot Framework](https://dev.botframework.com/) en utilisant l'application Azure AD.

1. Ajoute le canal Teams.

1. Configure le point de terminaison de messagerie comme `https://{ngrokTunnelId}.ngrok.io/api/messages`.

### <a name="registers-and-configures-teams-app"></a>Enregistrement et configuration de l'application Teams

Enregistrez une application Teams dans [Developer](https://dev.teams.microsoft.com/home) en utilisant le modèle de manifeste dans `templates/appPackage/manifest.template.json`.

Après l'enregistrement et la configuration de l'application, les fichiers de débogage locaux sont générés.

## <a name="take-a-tour-of-your-app-source-code"></a>Suivre une visite guidée du code source

Vous pouvez visualiser les dossiers et les fichiers du projet sous **Explorer** dans VS Code après que le Teams Toolkit ait enregistré et configuré votre application. Le tableau suivant répertorie les fichiers de débogage locaux et les types de configuration :

| Nom du dossier| Sommaire| Type de configuration de débogage |
| --- | --- | --- |
|  `.fx/configs/config.local.json` | Fichier de configuration de débogage local | Les valeurs de chaque configuration génèrent et enregistrent pendant le débogage local. |
|  `templates/appPackage/manifest.template.json` | Teams modèle de manifeste d’application pour le débogage local | Les espaces réservés dans le fichier pendant le débogage local. |
|  `tabs/.env.teams.local`  | Fichier de variables d’environnement pour l’onglet | Les valeurs de chaque variable d’environnement génèrent et enregistrent pendant le débogage local. |
|  `bot/.env.teamsfx.local` | Fichier de variables d’environnement pour l’extension de bot et de messagerie| Les valeurs de chaque variable d’environnement génèrent et enregistrent pendant le débogage local. |
| `api/.env.teamsfx.local`  | Fichier de variables d’environnement pour les fonctions Azure | Les valeurs de chaque variable d’environnement génèrent et enregistrent pendant le débogage local. |

## <a name="see-also"></a>Voir aussi

* [ Déboguer votre application Teams à l'aide de Teams Toolkit ](debug-local.md)
* [Utiliser Teams Shared Computer Toolkit pour mettre en service des ressources cloud](provision.md)
* [Déployer à partir du cloud](deploy.md)
* [Prévisualiser et personnaliser le manifeste de l'application Teams](TeamsFx-preview-and-customize-app-manifest.md)
