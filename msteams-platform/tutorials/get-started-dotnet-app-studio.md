---
title: 'Didacticiel - Créer votre première application à l’aide de C #'
description: Découvrez comment commencer à créer des applications Microsoft Teams avec C#/.NET.
keywords: mise en place de .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: c28c4d00c375b8e37f82c343eec2c5405ae0c1c8
ms.sourcegitcommit: fa64b83c0b534bf7a89f256880d5b5ca193e4b04
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/28/2021
ms.locfileid: "50037038"
---
# <a name="create-your-first-microsoft-teams-app-using-c"></a>Créer votre première application Microsoft Teams à l’aide de C #

Ce didacticiel vous aide à commencer à créer une application Microsoft Teams en C# sur .NET.

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a>Obtenir les conditions préalables

Pour effectuer ce didacticiel, vous devez obtenir les outils suivants :

- [Installer Git](https://git-scm.com/downloads)
- [Installez Visual Studio](https://www.visualstudio.com/downloads/). Vous pouvez installer l’édition communautaire gratuite.

Si vous voyez une option à ajouter au chemin d’accès lors `git` de l’installation, choisissez de le faire. Ce sera pratique.

Vérifiez votre `git` installation en exécutant ce qui suit dans une fenêtre terminal :
> [!NOTE]
> Utilisez la fenêtre terminal la plus à l’aise sur votre plateforme. Ces exemples utilisent Bash, mais s’exécutent sur la plupart des plateformes.

```bash
$ git --version
git version 2.17.1.windows.2

```

Assurez-vous de lancer la dernière version de Visual Studio et d’installer les mises à jour si elles sont affichées.

Vous pouvez continuer à utiliser cette fenêtre terminal pour exécuter les commandes qui suivent dans ce didacticiel.

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a>Télécharger l’exemple

Nous avons fourni un simple [Hello World !](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) exemple en C# pour vous aider à démarrer. Dans une fenêtre terminal, exécutez la commande suivante pour cloner l’exemple de référentiel sur votre ordinateur local :

```bash
git clone https://github.com/OfficeDev/msteams-samples-hello-world-csharp.git
```

> [!TIP]
> Vous pouvez [bifurquer](https://help.github.com/articles/fork-a-repo/) [ce référentiel](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) si vous souhaitez modifier et vérifier vos modifications dans GitHub pour référence ultérieure.

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a>Création et exécution de l’exemple

Une fois le dépôt cloné, utilisez Visual Studio pour ouvrir le fichier de solution à partir du répertoire racine de l’exemple, puis cliquez dans `Microsoft.Teams.Samples.HelloWorld.sln` `Build Solution` le `Build` menu. Vous pouvez exécuter l’exemple en appuyant `F5` ou en choisissant `Start Debugging` dans le `Debug` menu.

Lorsque l’application démarre, une fenêtre de navigateur s’ouvre avec la racine de l’application lancée. Vous pouvez accéder aux URL suivantes pour vérifier que toutes les URL d’application sont en cours de chargement :

- [http://localhost:3333](http://localhost:3333)
- [http://localhost:3333/hello](http://localhost:3333/hello)
- [http://localhost:3333/first](http://localhost:3333/first)
- [http://localhost:3333/second](http://localhost:3333/second)

<a name="HostSample"></a>

> [!Note]
> Si vous recevez une erreur telle `Could not find a part of the path … bin\roslyn\csc.exe` que , essayez de mettre à jour le package avec la `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` commande. Consultez [cette question sur StackOverflow pour](https://stackoverflow.com/questions/32780315) plus d’informations.

## <a name="host-the-sample-app"></a>Héberger l’exemple d’application

N’oubliez pas que les applications dans Microsoft Teams sont des applications web qui exposent une ou plusieurs fonctionnalités. Pour que la plateforme Teams charge votre application, votre application doit être accessible à partir d’Internet. Pour rendre votre application accessible à partir d’Internet, vous devez l’héberger. Vous pouvez l’héberger gratuitement dans Microsoft Azure ou créer un tunnel vers le processus local sur votre ordinateur de développement à l’aide `ngrok` de . Lorsque vous avez terminé l’hébergement de votre application, notez son URL racine. Il ressemblera à : `https://yourteamsapp.ngrok.io` ou `https://yourteamsapp.azurewebsites.net` .

### <a name="tunnel-using-ngrok"></a>Tunnel utilisant ngrok

Pour des tests rapides, vous pouvez exécuter l’application sur votre ordinateur local et y créer un tunnel via un point de terminaison web. [ngrok est](https://ngrok.com) un outil gratuit qui vous permet de le faire. Avec ngrok, vous pouvez obtenir une adresse web telle que `https://d0ac14a5.ngrok.io` (cette URL n’est qu’un exemple). Vous pouvez [télécharger et installer](https://ngrok.com/download) ngrok pour votre environnement. Veillez à l’ajouter à un emplacement dans votre `PATH` .

Une fois l’installation installée, vous pouvez ouvrir une nouvelle fenêtre terminal et exécuter la commande suivante pour créer un tunnel. L’exemple utilise le port 3333, donc n’oubliez pas de le spécifier ici.

```bash
ngrok http 3333 -host-header=localhost:3333
```

Ngrok écoutera les demandes provenant d’Internet et les routera vers votre application en cours d’exécution sur le port 3333. Vous pouvez vérifier en ouvrant votre navigateur et en allant `https://d0ac14a5.ngrok.io/hello` charger la page Hello de votre application. Assurez-vous d’utiliser l’adresse de forwarding affichée par ngrok dans votre session console au lieu de cette URL.

> [!NOTE]
> Si vous avez utilisé un [](#build-and-run-the-sample) autre port dans la build et l’étape d’utilisation ci-dessus, veillez à utiliser le même numéro de port pour configurer le `ngrok` tunnel.
> [!TIP]
> Il est bon de l’exécuter dans une autre fenêtre terminal pour la maintenir en cours d’exécution sans interférer avec l’application que vous de devez peut-être arrêter, reconstruire et `ngrok` réexécuter par la suite. La `ngrok` session retourne des informations de débogage utiles dans cette fenêtre.

L’application sera disponible uniquement pendant la session en cours sur votre ordinateur de développement. Si l’ordinateur est arrêté ou en veille, le service n’est plus disponible. N’oubliez pas cela lors du partage de l’application pour les tests effectués par d’autres utilisateurs. Si vous devez redémarrer le service, il retourne une nouvelle adresse et vous devez mettre à jour chaque endroit qui utilise cette adresse. La version payante de Ngrok n’a pas cette limitation.

### <a name="host-in-azure"></a>Hôte dans Azure

Microsoft Azure vous permet d’héberger votre application .NET sur un niveau gratuit à l’aide d’une infrastructure partagée. Cela sera suffisant pour exécuter cet `Hello World` exemple. Pour plus [d’informations, voir](https://azure.microsoft.com/free/) la création d’un compte gratuit.

Visual Studio la prise en charge intégrée du déploiement d’applications pour différents fournisseurs, y compris Azure.

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a>Mettre à jour les informations d’identification de votre application hébergée

L’exemple d’application nécessite que les variables d’environnement suivantes soient définies sur les valeurs que vous avez not es précédemment.

Ouvrez le fichier appsettings.jssur. Mettez à *jour la valeur MicrosoftAppId* avec votre ID de bot que vous avez enregistré précédemment. Mettez à jour *MicrosoftAppPassword avec* le mot de passe bot que vous avez enregistré précédemment.

<img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

Une fois ces modifications apportées, resserez l’application. Si vous utilisez ngrok, exécutez l’application localement et si vous hébergez dans Azure redéployer l’application.

## <a name="configure-the-app-tab"></a>Configurer l’onglet de l’application

Une fois que vous avez installé l’application dans une équipe, vous devez la configurer pour afficher le contenu. Go to a channel in the team where you installed the sample app and click on the **'+'** button to add a new tab. Vous pouvez ensuite choisir `Hello World` dans la liste Ajouter un **onglet.** Une boîte de dialogue de configuration s’est ensuite présentée. Cette boîte de dialogue vous permet de choisir l’onglet à afficher dans ce canal. Une fois que vous avez sélectionné l’onglet et cliqué dessus, vous pouvez voir l’onglet chargé `Save` `Hello World` avec l’onglet que vous avez choisi.

<img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a>Tester votre bot dans Teams

Vous pouvez désormais interagir avec le bot dans Teams. Choisissez un canal dans l’équipe où vous avez inscrit votre application, puis tapez `@your-bot-name` . C’est ce qu’on appelle **\@ une mention.** Le message que vous envoyez au bot vous sera renvoyé en tant que réponse.

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a>Tester votre extension de messagerie

Pour tester votre extension de messagerie, vous pouvez cliquer sur les trois points sous la zone d’entrée dans l’affichage conversation. Un menu apparaît avec **l’application « Hello World** » dans celui-ci. Lorsque vous cliquez dessus, un grand nombre de textes aléatoires s’affichent. Vous pouvez choisir l’un d’eux et celui-ci sera inséré dans votre conversation.

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

Choisissez l’un des textes aléatoires et vous verrez une carte mise en forme et prête à être envoyé avec votre propre message en bas.

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
