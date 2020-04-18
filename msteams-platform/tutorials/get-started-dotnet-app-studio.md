---
title: Prise en main de C#/.NET
description: Commencer à créer des applications intéressantes dans Microsoft teams à l’aide de C#/.NET
keywords: mise en route .net c# CSharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: 61237cd3178fcb41357230536827f732faf65ee4
ms.sourcegitcommit: 510ae42f72798fb24ddef0afa771ecd9d38e5348
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/17/2020
ms.locfileid: "43550958"
---
# <a name="get-started-on-the-microsoft-teams-platform-with-cnet-and-app-studio"></a>Prise en main de la plateforme Microsoft teams avec C#/.NET et App Studio

La plateforme de développement [Microsoft teams](/microsoftteams/) vous permet d’étendre facilement teams et d’intégrer vos propres applications et services de façon transparente dans l’espace de travail de teams. Ces applications peuvent ensuite être distribuées à votre entreprise ou pour teams dans le monde entier.

Pour étendre Microsoft Teams, vous devez créer une application Microsoft Teams. Une application Microsoft teams est une application Web que vous hébergez. Cette application peut ensuite être intégrée dans l’espace de travail de l’utilisateur dans Teams.

Ce didacticiel vous permet de commencer à créer une application Microsoft teams à l’aide de C# sur .NET. Vous pouvez tester l’application en la chargeant dans une équipe pour laquelle vous disposez d’autorisations, ou dans un client test créé à l’aide du programme de développement Office.

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a>Obtenir les conditions préalables

Pour effectuer ce didacticiel, vous devez obtenir les outils suivants :

- [Installer Git](https://git-scm.com/downloads)
- [Installez Visual Studio](https://www.visualstudio.com/downloads/). Vous pouvez installer la version gratuite de la communauté.

Si vous voyez une option à ajouter `git` au chemin d’accès pendant l’installation, choisissez de le faire. Il sera pratique.

Vérifiez votre `git` installation en exécutant la commande suivante dans une fenêtre de terminal :
> [!NOTE]
> Utilisez la fenêtre de terminal qui vous convient le mieux sur votre plateforme. Ces exemples utilisent bash, mais s’exécuteront sur la plupart des plateformes.

```bash
$ git --version
git version 2.17.1.windows.2

```

Veillez à lancer la dernière version de Visual Studio et à installer toutes les mises à jour, le cas échéant.

Vous pouvez continuer à utiliser cette fenêtre de terminal pour exécuter les commandes qui suivent dans ce didacticiel.

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a>Télécharger l’exemple

Nous avons fourni un simple [Hello, World !](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) exemple en C# pour vous aider à démarrer. Dans une fenêtre de terminal, exécutez la commande suivante pour cloner le référentiel de l’exemple sur votre ordinateur local :

```bash
git clone https://github.com/OfficeDev/msteams-samples-hello-world-csharp.git
```

> [!TIP]
> Vous pouvez [bifurquer](https://help.github.com/articles/fork-a-repo/) sur cette [référentiel](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) si vous voulez modifier et archiver les modifications apportées à GitHub à des fins de référence ultérieure.

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a>Création et exécution de l’exemple

Une fois le référentiel cloné, utilisez Visual Studio pour ouvrir le fichier `Microsoft.Teams.Samples.HelloWorld.sln` de solution à partir du répertoire racine de l’exemple, `Build Solution` puis cliquez `Build` sur dans le menu. Vous pouvez exécuter l’exemple en appuyant `F5` sur `Start Debugging` ou en `Debug` sélectionnant dans le menu.

Lorsque l’application démarre, une fenêtre de navigateur s’ouvre avec la racine de l’application lancée. Vous pouvez accéder aux URL suivantes pour vérifier que toutes les URL d’application sont en cours de chargement :

- [http://localhost:3333](http://localhost:3333)
- [http://localhost:3333/hello](http://localhost:3333/hello)
- [http://localhost:3333/first](http://localhost:3333/first)
- [http://localhost:3333/second](http://localhost:3333/second)

<a name="HostSample"></a>

> [!Note]
> Si vous recevez une erreur telle `Could not find a part of the path … bin\roslyn\csc.exe`que, essayez de mettre à jour le package `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r`à l’aide de la commande. Pour plus d’informations, consultez [cette question sur StackOverflow](https://stackoverflow.com/questions/32780315) .

## <a name="host-the-sample-app"></a>Héberger l’exemple d’application

N’oubliez pas que les applications dans Microsoft teams sont des applications Web qui exposent une ou plusieurs fonctionnalités. Pour que la plateforme teams charge votre application, votre application doit être accessible à partir d’Internet. Pour permettre à votre application d’être accessible à partir d’Internet, vous devez héberger votre application. Vous pouvez l’héberger dans Microsoft Azure gratuitement ou créer un tunnel vers le processus local sur votre ordinateur de développement à `ngrok`l’aide de. Une fois que vous avez terminé d’héberger votre application, prenez note de son URL racine. Il ressemblera à ceci `https://yourteamsapp.ngrok.io` : `https://yourteamsapp.azurewebsites.net`ou.

### <a name="tunnel-using-ngrok"></a>Tunnel à l’aide de ngrok

Pour un test rapide, vous pouvez exécuter l’application sur votre ordinateur local et y créer un tunnel via un point de terminaison Web. [ngrok](https://ngrok.com) est un outil gratuit qui vous permet d’effectuer cette opération. Avec ngrok, vous pouvez obtenir une adresse Web telle `https://d0ac14a5.ngrok.io` que (cette URL n’est qu’un exemple). Vous pouvez [Télécharger et installer](https://ngrok.com/download) ngrok pour votre environnement. Veillez à l’ajouter à un emplacement dans votre `PATH`.

Une fois que vous l’avez installé, vous pouvez ouvrir une nouvelle fenêtre de terminal et exécuter la commande suivante pour créer un tunnel. L’exemple utilise le port 3333, veillez donc à le spécifier ici.

```bash
ngrok http 3333 -host-header=localhost:3333
```

Ngrok écoutera les demandes en provenance d’Internet et les acheminera vers votre application en cours d’exécution sur le port 3333. Vous pouvez vérifier en ouvrant votre navigateur et en accédant à `https://d0ac14a5.ngrok.io/hello` pour charger la page Hello de votre application. Veillez à utiliser l’adresse de transfert affichée par ngrok dans votre session de console au lieu de cette URL.

> [!NOTE]
> Si vous avez utilisé un autre port dans l’étape de [création et d’exécution](#build-and-run-the-sample) ci-dessus, vérifiez que vous utilisez le même numéro `ngrok` de port pour configurer le tunnel.
> [!TIP]
> Il est judicieux de s’exécuter `ngrok` dans une autre fenêtre de terminal pour qu’elle continue de s’exécuter sans interférer avec l’application que vous devrez peut-être arrêter, reconstruire et réexécuter. La `ngrok` session renverra des informations utiles sur le débogage dans cette fenêtre.

L’application sera disponible uniquement pendant la session en cours sur votre ordinateur de développement. Si l’ordinateur est arrêté ou passe en mode veille, le service n’est plus disponible. Souvenez-vous de ceci lors du partage de l’application pour le test par d’autres utilisateurs. Si vous devez redémarrer le service, il renverra une nouvelle adresse et vous devrez mettre à jour chaque emplacement qui utilise cette adresse. La version payante de Ngrok n’a pas cette limitation.

### <a name="host-in-azure"></a>Hôte dans Azure

Microsoft Azure vous permet d’héberger votre application .NET sur une couche libre à l’aide de l’infrastructure partagée. Cela sera suffisant pour exécuter cet `Hello World` exemple. Pour plus d’informations, consultez [la rubrique Création d’un compte gratuit](https://azure.microsoft.com/free/) .

Visual Studio prend en charge le déploiement d’applications sur différents fournisseurs, dont Azure.

<img width="530px" src="~/assets/images/get-started/publishtoazure1.png" title="Visual Studio"/>

[!include[Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a>Mettre à jour les informations d’identification pour votre application hébergée

L’exemple d’application requiert que les variables d’environnement suivantes soient définies sur les valeurs que vous avez notées précédemment.

Ouvrez le fichier Web. config et recherchez la section *appSettings* . Mettez à jour la valeur *MicrosoftAppId* avec votre ID bot que vous avez enregistré précédemment. Mettez à jour le *MicrosoftAppPassword* avec le mot de passe du bot que vous avez enregistré précédemment.

<img width="560px" src="~/assets/images/get-started/get-started-net-azure-add-keys.png" title="définition des clés"/>

Une fois ces modifications effectuées, régénérez l’application. Si vous utilisez ngrok, exécutez l’application localement et, si vous hébergez dans Azure, redéployez l’application.

## <a name="configure-the-app-tab"></a>Configurer l’onglet application

Une fois que vous avez installé l’application dans une équipe, vous devez la configurer pour afficher le contenu. Accédez à un canal de l’équipe où vous avez installé l’exemple d’application, puis cliquez sur le bouton **« + »** pour ajouter un nouvel onglet. Vous pouvez ensuite choisir `Hello World` dans la liste **Ajouter un onglet** . Une boîte de dialogue de configuration s’affiche. Cette boîte de dialogue vous permet de choisir l’onglet à afficher dans ce canal. Une fois que vous avez sélectionné l’onglet `Save` , puis cliqué sur, `Hello World` vous pouvez voir l’onglet chargé avec l’onglet que vous avez choisi.

<img width="530px" src="~/assets/images/samples-hello-world-tab-configure.png" title="Capture d’écran de la configuration" />

### <a name="test-your-bot-in-teams"></a>Tester votre robot dans teams

Vous pouvez désormais interagir avec le bot dans Teams. Sélectionnez un canal dans l’équipe où vous avez enregistré votre application, puis `@your-bot-name`tapez. Il s’agit d’une ** \@mention**. Tout message que vous envoyez au bot vous sera renvoyé en tant que réponse.

<img width="450px" title="Réponses de robot" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a>Tester votre extension de messagerie

Pour tester votre extension de messagerie, vous pouvez cliquer sur les trois points sous la zone d’entrée de votre affichage conversation. Un menu s’affiche avec l’application **« Hello World »** . Lorsque vous cliquez dessus, un ensemble de textes aléatoires s’affichent. Vous pouvez choisir l’un d’entre eux et l’insérer dans votre conversation.

<img width="530px" title="Menu extension de messagerie" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" title="Résultat de l’extension de messagerie" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

Choisissez l’un des textes aléatoires, et vous verrez une carte formatée et prête à envoyer avec votre propre message en bas.

<img width="530px" title="Envoi d’extension de messagerie" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
