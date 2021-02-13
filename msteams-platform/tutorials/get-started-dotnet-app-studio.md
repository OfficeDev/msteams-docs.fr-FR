---
title: 'Didacticiel - Créer votre première application à l’aide de C #'
description: Découvrez comment commencer à créer des applications Microsoft Teams avec C# ou .NET.
keywords: mise en place de .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: b37a8d555117e38383504dc99d82d564439a3ebf
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231522"
---
# <a name="create-your-first-teams-app-using-c-or-net"></a>Créer votre première application Teams en C# ou .NET

Ce didacticiel vous aide à créer une application Microsoft Teams en C# ou .NET.

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a>Obtenir les conditions préalables

Pour effectuer ce didacticiel, vous devez obtenir les outils suivants :

- [Installer Git](https://git-scm.com/downloads)
- [Installez Visual Studio](https://www.visualstudio.com/downloads/). Vous pouvez installer l’édition communautaire gratuite.

Lors de l’installation, s’il existe une option d’ajout au chemin d’accès, `git` sélectionnez-la.

Dans une fenêtre terminal, exécutez la commande suivante pour vérifier votre `git` installation :

```bash
$ git --version
git version 2.17.1.windows.2

```

> [!NOTE]
> Utilisez une fenêtre terminal appropriée sur votre plateforme. Ces exemples utilisent Bash, mais s’exécutent sur la plupart des plateformes.

Veillez à lancer la dernière version de Visual Studio et à installer les mises à jour.

Vous pouvez utiliser la même fenêtre terminal pour exécuter les commandes de ce didacticiel.

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a>Télécharger l’exemple

Vous pouvez commencer avec un simple [Hello World !](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) exemple en C#. Dans une fenêtre terminal, exécutez la commande suivante pour cloner l’exemple de référentiel sur votre ordinateur local :

```bash
git clone https://github.com/OfficeDev/msteams-samples-hello-world-csharp.git
```

> [!TIP]
> Vous pouvez [bifurquer](https://help.github.com/articles/fork-a-repo/) [ce référentiel pour](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) modifier et enregistrer vos modifications dans GitHub pour référence.

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a>Création et exécution de l’exemple

Une fois le dépôt cloné, utilisez Visual Studio pour ouvrir le fichier de solution à partir du répertoire racine de l’exemple et sélectionnez-le `Microsoft.Teams.Samples.HelloWorld.sln` `Build Solution` dans le `Build` menu. Pour exécuter l’exemple, `F5` appuyez ou choisissez `Start Debugging` dans le `Debug` menu.

Lorsque l’application démarre, une fenêtre de navigateur s’ouvre avec la racine de l’application lancée. Vous pouvez accéder aux URL suivantes pour vérifier que toutes les URL d’application sont en cours de chargement :

- [https://localhost:44327/](https://localhost:44327/)
- [https://localhost:44327/hello](https://localhost:44327/hello)
- [https://localhost:44327/first](https://localhost:44327/first)
- [https://localhost:44327/second]https://localhost:44327/second)

<a name="HostSample"></a>

> [!Note]
> Si vous recevez une `Could not find a part of the path … bin\roslyn\csc.exe` erreur, mettez à jour le package avec la `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` commande. Pour plus d’informations, [consultez cette question sur StackOverflow.](https://stackoverflow.com/questions/32780315)

## <a name="host-the-sample-app"></a>Héberger l’exemple d’application

Les applications dans Microsoft Teams sont des applications web qui fournissent une ou plusieurs fonctionnalités. Pour que la plateforme Teams charge votre application, votre application doit être accessible à partir d’Internet. Pour rendre votre application accessible à partir d’Internet, vous devez l’héberger. Vous pouvez l’héberger gratuitement dans Microsoft Azure ou créer un tunnel vers le processus local sur votre ordinateur de développement à l’aide `ngrok` de . Lorsque vous avez terminé l’hébergement de votre application, notez son URL racine. Par exemple, `https://yourteamsapp.ngrok.io` ou `https://yourteamsapp.azurewebsites.net` .

### <a name="tunnel-using-ngrok"></a>Tunnel utilisant ngrok

Pour des tests rapides, vous pouvez exécuter l’application sur votre ordinateur local et y créer un tunnel via un point de terminaison web. [ngrok est](https://ngrok.com) un outil gratuit avec lequel vous pouvez obtenir une adresse web telle que `https://d0ac14a5.ngrok.io` . Vous pouvez [télécharger et installer](https://ngrok.com/download) ngrok. Veillez à l’ajouter à un emplacement dans votre `PATH` .

Après avoir installé ngrok, ouvrez une nouvelle fenêtre terminal et exécutez la commande suivante pour créer un tunnel :

```bash
ngrok http 44327 -host-header=localhost:44327
```

L’exemple utilise le port 44327 et assurez-vous de le spécifier.

Ngrok écoute les demandes provenant d’Internet et les approvisionnement vers votre application en cours d’exécution sur le port 44327. Pour vérifier, ouvrez votre navigateur et allez `https://d0ac14a5.ngrok.io/hello` charger la page Hello de votre application. Au lieu de cette URL, utilisez l’adresse de forwarding affichée par ngrok dans votre session console.

> [!NOTE]
> Si vous avez utilisé un [](#build-and-run-the-sample) autre port lors de l’étape de build et d’utilisation, veillez à utiliser le même numéro de port pour configurer le `ngrok` tunnel.

> [!TIP]
> Il est bon de l’exécuter `ngrok` dans une autre fenêtre terminal. Cette étape est effectuée pour empêcher ngrok de s’exécute sans interférer avec l’application, que vous devez arrêter, reconstruire et réexécuter. La `ngrok` session fournit des informations de débogage utiles dans cette fenêtre.

L’application est disponible uniquement pendant la session en cours sur votre ordinateur de développement. Si l’ordinateur est arrêté ou en veille, le service n’est plus disponible. N’oubliez pas que vous partagez l’application pour le test à d’autres utilisateurs. Si vous devez redémarrer le service, l’application renvoie une nouvelle adresse et vous devez mettre à jour chaque emplacement qui utilise cette adresse. La version payante de ngrok n’a pas cette limitation.

### <a name="host-in-azure"></a>Hôte dans Azure

Microsoft Azure héberge votre application .NET sur un niveau gratuit à l’aide d’une infrastructure partagée. Cela suffit pour exécuter `Hello World` l’exemple. Pour plus d’informations, [voir la création d’un compte gratuit.](https://azure.microsoft.com/free/)

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

Vous pouvez désormais interagir avec le bot dans Teams. Choisissez un canal dans l’équipe où vous avez inscrit votre application et tapez `@your-bot-name` . C’est ce qu’on appelle **\@ une mention.** Le message que vous envoyez au bot vous sera renvoyé en tant que réponse.

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a>Tester votre extension de messagerie

Pour tester votre extension de messagerie, vous pouvez cliquer sur les trois points sous la zone d’entrée dans l’affichage conversation. Un menu apparaît avec **l’application « Hello World** » dans celui-ci. Lorsque vous cliquez dessus, un grand nombre de textes aléatoires s’affichent. Vous pouvez choisir l’un d’eux et celui-ci est inséré dans votre conversation.

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

Choisissez l’un des textes aléatoires et vous verrez une carte mise en forme et prête à être envoyé avec votre propre message en bas.

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
