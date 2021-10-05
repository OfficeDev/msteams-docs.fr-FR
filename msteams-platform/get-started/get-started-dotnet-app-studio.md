---
title: 'Didacticiel - Créer votre première application à l’aide de C #'
description: Découvrez comment commencer à créer des applications Microsoft Teams avec C# ou .NET.
keywords: mise en place de .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
ms.localizationpriority: medium
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: 9e830b6681797fcac032c2345a56163e634c446c
ms.sourcegitcommit: 6573881f7e69d8e5ec8861f54df84e7d519f0511
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/04/2021
ms.locfileid: "60096690"
---
# <a name="build-your-first-teams-app-using-c"></a>Créer votre première application Teams en C #

Dans ce didacticiel, vous allez apprendre à créer votre toute première application Microsoft Teams à l’aide de .NET ou C#. Il vous permet également de suivre les étapes suivantes :

1. [Préparer votre environnement](#prepare-your-environment)
1. [Obtenir les conditions préalables](#GetPrerequisites)
1. [Télécharger l’exemple](#DownloadSample)
1. [Création et exécution de l’exemple](#BuildRun)
1. [Héberger l’exemple d’application](#hostsample)
1. [Mettre à jour les informations d’identification de votre application hébergée](#updatecredentials)
1. [Configurer l’onglet de l’application](#configureapptab)

<a name="prepare-your-environment"></a>
[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a>Obtenir les conditions préalables

Pour terminer ce didacticiel, vous devez installer les outils suivants :

- [Installer Git](https://git-scm.com/downloads)
- [Installer Visual Studio](https://www.visualstudio.com/downloads/)

Vous pouvez installer l’édition communautaire gratuite de Visual Studio. Lors de l’installation, s’il existe une option à `git` ajouter au chemin d’accès, sélectionnez-la. Dans une fenêtre terminal, exécutez la commande suivante pour vérifier votre `git` installation :

```bash
$ git --version
git version 2.17.1.windows.2

```

> [!NOTE]
> Utilisez une fenêtre terminal appropriée sur votre plateforme. Ces exemples utilisent Git Bash, mais peuvent être exécutés sur la plupart des plateformes.

Ouvrez la dernière version de Visual Studio et installez les mises à jour.

Vous pouvez utiliser la même fenêtre terminal pour exécuter les commandes de ce didacticiel.

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a>Télécharger l’exemple

Vous pouvez commencer avec un simple [Hello World !](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp) exemple dans C#. Dans une fenêtre terminal, exécutez la commande suivante pour cloner l’exemple de référentiel sur votre ordinateur :

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> Vous pouvez [bifurcation](https://help.github.com/articles/fork-a-repo/) [de ce repo](https://github.com/OfficeDev/Microsoft-Teams-Samples) pour modifier et enregistrer vos modifications dans GitHub.

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a>Création et exécution de l’exemple

Vous pouvez créer et exécuter l’exemple après son clonage. 

**Pour créer et exécuter l’exemple cloné**

1. Ouvrez le fichier de solution **Microsoft.Teams. Samples.HelloWorld.sln** à partir du répertoire **Microsoft-Teams-Samples/samples/app-hello-world/csharp** de l’exemple.
1. Sélectionnez **Solution de** build dans **le** menu Build.
1. Sélectionnez **la touche F5** ou démarrez **le débogage** dans le menu **Débogage** pour exécuter l’exemple.

    Lorsque l’application démarre, une fenêtre de navigateur s’ouvre avec la racine de l’application lancée. Vous pouvez utiliser les URL suivantes pour vérifier que toutes les URL d’application sont en cours de chargement :

    - `https://localhost:44327/`
    - `https://localhost:44327/hello`
    - `https://localhost:44327/first`
    - `https://localhost:44327/second`

    > [!Note]
    > Si vous recevez une `Could not find a part of the path … bin\roslyn\csc.exe` erreur, mettez à jour le package avec la `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` commande. Pour plus d’informations, [consultez cette question sur Stack Overflow.](https://stackoverflow.com/questions/32780315)

    <a name="hostsample"></a>
    ## <a name="deploy-your-sample-app"></a>Déployer votre exemple d’application

    Les applications Microsoft Teams sont des applications web qui fournissent une ou plusieurs fonctionnalités. Pour que la Teams charge votre application, votre application doit être disponible sur Internet. Pour ce faire, vous devez héberger votre application. Vous pouvez l’héberger dans Microsoft Azure gratuitement ou créer un tunnel vers le processus local sur votre ordinateur à l’aide `ngrok` de . Après avoir héberger votre application, notez son URL racine, par exemple `https://yourteamsapp.ngrok.io` ou `https://yourteamsapp.azurewebsites.net` .

### <a name="tunnel-using-ngrok"></a>Tunnel à l’aide de ngrok

Pour des tests rapides, vous pouvez exécuter l’application sur votre ordinateur et y créer un tunnel via un point de terminaison web. [`ngrok`](https://ngrok.com) est un outil gratuit avec lequel vous pouvez obtenir une adresse web, telle que `https://d0ac14a5.ngrok.io` . Vous pouvez [télécharger et installer](https://ngrok.com/download) ngrok et l’ajouter à un emplacement dans votre `PATH` .

Après l’installation, `ngrok` ouvrez une nouvelle fenêtre terminal et exécutez la commande suivante pour créer un tunnel :

```bash
ngrok http 44327 -host-header=localhost:44327
```

`Ngrok` répond aux demandes provenant d’Internet et les approvisionnement vers votre application en cours d’exécution sur le port 44327. 

**Pour vérifier la réponse**

1. Ouvrez votre navigateur, puis accédez à `https://d0ac14a5.ngrok.io/hello`. Cela charge la page Hello de votre application.
1. Au lieu de l’URL mentionnée à l’étape 1, utilisez l’adresse de forwarding affichée `ngrok` dans votre session console.
    > [!NOTE]
    > Si vous avez utilisé un autre port à l’étape [de](#build-and-run-the-sample) build et d’utilisation, veillez à utiliser le même numéro de port pour configurer le `ngrok` tunnel.
    > [!TIP]
    > Il est bon de l’exécuter `ngrok` dans une autre fenêtre terminal. Cela permet de ne pas `ngrok` s’exécute sans interférer avec l’application. Vous devez arrêter, reconstruire et réexécuter l’application. La `ngrok` session fournit des informations de débogage utiles dans cette fenêtre.

    L’application est disponible uniquement pendant la session en cours sur votre ordinateur. Si l’ordinateur est arrêté ou en veille, le service n’est plus disponible. N’oubliez pas que vous partagez l’application pour le test à d’autres utilisateurs. Si vous devez redémarrer le service, l’application renvoie une nouvelle adresse et vous devez mettre à jour chaque emplacement qui utilise cette adresse. La version payante `ngrok` de n’a pas cette limitation.

### <a name="host-in-azure"></a>Hôte dans Azure

Microsoft Azure héberge votre application .NET sur un niveau gratuit à l’aide d’une infrastructure partagée. Cela suffit pour exécuter `Hello World` l’exemple. Pour plus d’informations, [voir la création d’un compte Azure gratuit.](https://azure.microsoft.com/free/)

Visual Studio la prise en charge intégrée du déploiement d’applications pour différents fournisseurs, notamment Azure :

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

**Mettre à jour le package d’application**

> [!NOTE]
>  App Studio sera bientôt supprimé. Configurez, distribuez et gérez vos applications Teams avec le nouveau [portail du développeur.](https://dev.teams.microsoft.com/)

# <a name="app-studio"></a>[App Studio](#tab/AS)

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

# <a name="developer-portal"></a>[Portail du développeur](#tab/DP)

**Pour configurer le package d’application dans le Portail des développeurs (prévisualisation) dans Teams**


1. 1.Go to **[Developer portal](https://dev.teams.microsoft.com/)**.

     <img width="600px" alt="Screenshot of TDP" src="~/assets/images/tdp/tdp_home_1.png"/>

1. Go to **Apps**.

    <img width="600px" alt="Open Apps" src="~/assets/images/tdp/screen2.png"/>

1. Sélectionnez **Importer une application existante.**

    <img width="600px" alt="Screenshot of import app in tdp" src="~/assets/images/tdp/screen3.png"/>

1. Sélectionnez **Hello World** et **sélectionnez Importer.** **L’application Hello World** est importée dans le Portail des développeurs. 

    Vous pouvez configurer votre application à l’aide du portail Teams développeur. Le manifeste se trouve sous Distribuer. Vous pouvez utiliser le manifeste pour configurer des fonctionnalités, des ressources requises et d’autres attributs importants pour votre application. Pour plus d’informations sur la configuration de votre application à l’aide du Portail du développeur, voir [Teams Portail du développeur.](../concepts/build-and-test/teams-developer-portal.md)

    <img width="600px" alt="Screenshot of configure tdp" src="~/assets/images/tdp/Screen4.png"/>
---

<a name="updatecredentials"></a>
## <a name="update-the-credentials-for-your-hosted-app"></a>Mettre à jour les informations d’identification de votre application hébergée

L’exemple d’application nécessite que les variables d’environnement soient définies sur les valeurs que vous avez enregistrées dans le fichier texte.

**Pour mettre à jour les informations d’identification de votre application hébergée**

1. Ouvrez le fichier `appsettings.json`. 
1. Mettez à **jour la valeur MicrosoftAppId** avec votre ID de bot que vous avez enregistré dans le fichier texte. 
1. Mettez à jour **MicrosoftAppPassword avec** le mot de passe du bot que vous avez enregistré.

    <img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

    Une fois ces modifications apportées, resserez l’application. Si vous utilisez ngrok, exécutez l’application localement et si vous hébergez dans Azure, redéployer l’application.

<a name="configureapptab"></a>
## <a name="configure-the-app-tab"></a>Configurer l’onglet de l’application

Après avoir installé l’application dans Teams, vous devez la configurer pour afficher le contenu. 

**Pour configurer l’onglet de l’application**

1. Go to a channel in the team where you installed the sample app and select the **'+'** button to add a new tab.
1. Sélectionnez **Hello World** dans la **liste Ajouter un** onglet. Une boîte de dialogue de configuration s’affiche pour vous permettre de sélectionner l’onglet à afficher dans ce canal. 
1. Sélectionnez **Enregistrer**. `Hello World`L’onglet est chargé avec l’onglet.

    <img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a>Testez votre bot dans Teams

Vous pouvez maintenant tester le bot dans Teams. 

**Pour tester votre bot**

* Sélectionnez un canal dans l’équipe où vous avez inscrit votre application et tapez `@your-bot-name` . C’est ce qu’on appelle **\@ une mention.** Le bot répond à n’importe quel message que vous envoyez.

    <img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a>Tester votre extension de messagerie

**Pour tester votre extension de messagerie**
1. **Sélectionnez...** sous la zone d’entrée dans l’affichage de votre conversation. Un menu avec **l’application « Hello World** » s’affiche. 
1. Sélectionnez le menu, un ensemble de textes aléatoires s’affiche. Vous pouvez sélectionner l’un des textes aléatoires insérés dans votre conversation.

    <img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu1.png" />

    <img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result1.png" />

1. Sélectionnez l’un des textes aléatoires. Une carte mise en forme et prête à envoyer votre propre message s’affiche.

    <img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />

## <a name="see-also"></a>Voir aussi

* [Présentation des didacticiels](code-samples.md)
* [Créer une application de bot de conversation](first-app-bot.md)
* [Créer une extension de messagerie](first-message-extension.md)
* [Exemples de code](https://github.com/OfficeDev/Microsoft-Teams-Samples)
