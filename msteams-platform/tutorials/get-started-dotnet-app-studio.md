---
title: 'Didacticiel - Créer votre première application à l’aide de C #'
description: Découvrez comment commencer à créer des applications Microsoft Teams avec C# ou .NET.
keywords: mise en place de .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: ededd0800c7f789469e79e2a475c125b7fc37795
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449318"
---
# <a name="create-your-first-teams-app-using-c-or-net"></a>Créer votre première application Teams à l’aide C# ou .NET

Ce didacticiel vous aide à créer une application Microsoft Teams à l’aide C# ou .NET. Pour ce faire, vous devez :

* Préparer votre environnement
* Obtenir les conditions préalables
* Télécharger l’exemple
* Création et exécution de l’exemple
* Héberger l’exemple d’application
* Mettre à jour les informations d’identification de votre application hébergée
* Configurer l’onglet de l’application

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
> Vous pouvez [bifurquer](https://help.github.com/articles/fork-a-repo/) [ce référentiel pour](https://github.com/OfficeDev/Microsoft-Teams-Samples) modifier et enregistrer vos modifications dans GitHub.

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a>Création et exécution de l’exemple

Une fois le dépôt cloné, utilisez Visual Studio pour ouvrir le fichier de solution **Microsoft.Teams.Samples.HelloWorld.sln** à partir du répertoire **Microsoft-Teams-Samples/samples/app-hello-world/csharp** de l’exemple. Ensuite, **sélectionnez Solution de build** dans **le** menu Build. Pour exécuter l’exemple, appuyez **sur F5** ou sélectionnez **Démarrer le débogage** dans le menu **Débogage.**

Lorsque l’application démarre, une fenêtre de navigateur s’ouvre avec la racine de l’application lancée. Vous pouvez utiliser les URL suivantes pour vérifier que toutes les URL d’application sont en cours de chargement :

- [https://localhost:44327/](https://localhost:44327/)
- [https://localhost:44327/hello](https://localhost:44327/hello)
- [https://localhost:44327/first](https://localhost:44327/first)
- [https://localhost:44327/second]https://localhost:44327/second)

<a name="HostSample"></a>

> [!Note]
> Si vous recevez une `Could not find a part of the path … bin\roslyn\csc.exe` erreur, mettez à jour le package avec la `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` commande. Pour plus d’informations, [consultez cette question sur Stack Overflow.](https://stackoverflow.com/questions/32780315)

## <a name="host-the-sample-app"></a>Héberger l’exemple d’application

Les applications dans Microsoft Teams sont des applications web qui fournissent une ou plusieurs fonctionnalités. Pour que la plateforme Teams charge votre application, votre application doit être disponible sur Internet. Pour ce faire, vous devez héberger votre application. Vous pouvez l’héberger gratuitement dans Microsoft Azure ou créer un tunnel vers le processus local sur votre ordinateur à l’aide `ngrok` de . Après avoir héberger votre application, notez son URL racine, par exemple `https://yourteamsapp.ngrok.io` ou `https://yourteamsapp.azurewebsites.net` .

### <a name="tunnel-using-ngrok"></a>Tunnel utilisant ngrok

Pour des tests rapides, vous pouvez exécuter l’application sur votre ordinateur et y créer un tunnel via un point de terminaison web. [`ngrok`](https://ngrok.com) est un outil gratuit avec lequel vous pouvez obtenir une adresse web, telle que `https://d0ac14a5.ngrok.io` . Vous pouvez [télécharger et installer](https://ngrok.com/download) ngrok et l’ajouter à un emplacement dans votre `PATH` .

Après avoir `ngrok` installé, ouvrez une nouvelle fenêtre terminal et exécutez la commande suivante pour créer un tunnel :

```bash
ngrok http 44327 -host-header=localhost:44327
```

`Ngrok` écoute les demandes provenant d’Internet et les approvisionnement vers votre application en cours d’exécution sur le port 44327. Pour vérifier, ouvrez votre navigateur et allez `https://d0ac14a5.ngrok.io/hello` charger la page Hello de votre application. Au lieu de cette URL, utilisez l’adresse de forwarding affichée dans `ngrok` votre session console.

> [!NOTE]
> Si vous avez utilisé un autre port à l’étape [de](#build-and-run-the-sample) build et d’utilisation, veillez à utiliser le même numéro de port pour configurer le `ngrok` tunnel.

> [!TIP]
> Il est bon de l’exécuter `ngrok` dans une autre fenêtre terminal. Cela permet de ne pas `ngrok` s’exécute sans interférer avec l’application. Vous devez arrêter, reconstruire et réexécuter l’application. La `ngrok` session fournit des informations de débogage utiles dans cette fenêtre.

L’application est disponible uniquement pendant la session en cours sur votre ordinateur. Si l’ordinateur est arrêté ou en veille, le service n’est plus disponible. N’oubliez pas que vous partagez l’application pour le test à d’autres utilisateurs. Si vous devez redémarrer le service, l’application renvoie une nouvelle adresse et vous devez mettre à jour chaque emplacement qui utilise cette adresse. La version payante `ngrok` de n’a pas cette limitation.

### <a name="host-in-azure"></a>Hôte dans Azure

Microsoft Azure héberge votre application .NET sur un niveau gratuit à l’aide d’une infrastructure partagée. Cela suffit pour exécuter `Hello World` l’exemple. Pour plus d’informations, [voir la création d’un compte Azure gratuit.](https://azure.microsoft.com/free/)

Visual Studio la prise en charge intégrée du déploiement d’applications pour différents fournisseurs, y compris Azure.

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a>Mettre à jour les informations d’identification de votre application hébergée

L’exemple d’application nécessite que les variables d’environnement soient définies sur les valeurs que vous avez enregistrées dans le [fichier texte.](~/includes/get-started/get-started-use-app-studio.md#bots)

Ouvrez le appsettings.jsfichier on. Mettez à **jour la valeur MicrosoftAppId** avec votre ID de bot que vous avez enregistré dans le fichier texte. Mettez à jour **MicrosoftAppPassword avec** le mot de passe du bot que vous avez enregistré.

<img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

Une fois ces modifications apportées, resserez l’application. Si vous utilisez ngrok, exécutez l’application localement et si vous hébergez dans Azure, redéployer l’application.

## <a name="configure-the-app-tab"></a>Configurer l’onglet de l’application

Une fois que vous avez installé l’application dans une équipe, vous devez la configurer pour afficher le contenu. Go to a channel in the team where you installed the sample app and select the **'+'** button to add a new tab. Choisissez **Hello World dans** la liste Ajouter **un** onglet. Une boîte de dialogue de configuration s’affiche pour vous permettre de choisir l’onglet à afficher dans ce canal. Une fois que vous avez sélectionné l’onglet et que vous avez sélectionné **Enregistrer,** l’onglet `Hello World` est chargé avec l’onglet.

<img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a>Tester votre bot dans Teams

Vous pouvez maintenant tester le bot dans Teams. Sélectionnez un canal dans l’équipe où vous avez inscrit votre application et tapez `@your-bot-name` . C’est ce qu’on appelle **\@ une mention.** Le bot répond à tout message que vous envoyez.

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a>Tester votre extension de messagerie

Pour tester votre extension de messagerie, vous pouvez **sélectionner...** sous la zone d’entrée de votre affichage conversation. Un menu avec **l’application « Hello World** » s’affiche. Lorsque vous le sélectionnez, un ensemble de textes aléatoires s’affiche. Vous pouvez sélectionner l’un des textes aléatoires insérés dans votre conversation.

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

Sélectionnez l’un des textes aléatoires. Une carte mise en forme et prête à envoyer votre propre message s’affiche.

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
