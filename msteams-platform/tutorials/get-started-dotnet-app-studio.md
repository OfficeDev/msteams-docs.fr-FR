---
title: 'Tutoriel - Créez votre première application à l’aide de C #'
description: Découvrez comment commencer à créer des Microsoft Teams applications avec C# ou .NET.
keywords: commencer .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
localization_priority: Normal
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: eaa37f1ccb7944ee18bb62ae47882dc4a715b165
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566886"
---
# <a name="create-your-first-teams-app-using-c"></a>Créez votre première application Teams en utilisant C #

Ce tutoriel vous aide à créer une application Microsoft Teams en utilisant C#. Pour ce faire, vous devez :

* Préparer votre environnement
* Obtenez des conditions préalables
* Télécharger l’échantillon
* Création et exécution de l’exemple
* Hébergez l’exemple d’application
* Mettre à jour les informations d’identification de votre application hébergée
* Configurer l’onglet app

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a>Obtenez des conditions préalables

Pour compléter ce tutoriel, vous devez installer les outils suivants :

- [Installer Git](https://git-scm.com/downloads)
- [Installer Visual Studio](https://www.visualstudio.com/downloads/)

Vous pouvez installer l’édition communautaire gratuite de Visual Studio. Lors de l’installation, s’il y a une option `git` à ajouter au chemin, sélectionnez-le. Dans une fenêtre terminale, exécutez la commande suivante pour vérifier votre `git` installation :

```bash
$ git --version
git version 2.17.1.windows.2

```

> [!NOTE]
> Utilisez une fenêtre terminale appropriée sur votre plate-forme. Ces exemples utilisent Git Bash mais peuvent être exécutés sur la plupart des plates-formes.

Ouvrez la dernière version de Visual Studio installez toutes les mises à jour.

Vous pouvez utiliser la même fenêtre terminale pour exécuter les commandes de ce tutoriel.

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a>Télécharger l’échantillon

Vous pouvez commencer avec un simple [Bonjour, Monde!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp) échantillon en C#. Dans une fenêtre terminale, exécutez la commande suivante pour cloner le référentiel d’échantillons sur votre ordinateur :

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> Vous pouvez [fourre-tout](https://help.github.com/articles/fork-a-repo/) [ce repo](https://github.com/OfficeDev/Microsoft-Teams-Samples) pour modifier et enregistrer vos modifications à GitHub.

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a>Création et exécution de l’exemple

Une fois le repo cloné, utilisez Visual Studio pour ouvrir le fichier de solution **Microsoft.Teams. Samples.HelloWorld.sln** de **l’annuaire Microsoft-Teams-Samples/samples/app-hello-world/csharp** de l’échantillon. Sélectionnez ensuite **Build Solution** dans le menu **Build.** Pour exécuter l’échantillon, **appuyez sur F5** ou **sélectionnez Démarrer le débogage** dans le menu **Debug.**

Lorsque l’application démarre, une fenêtre de navigateur s’ouvre avec la racine de l’application lancée. Vous pouvez vous rendre aux URL suivantes pour vérifier que toutes les URL de l’application sont en train de charger :

- `https://localhost:44327/`
- `https://localhost:44327/hello`
- `https://localhost:44327/first`
- `https://localhost:44327/second`

<a name="HostSample"></a>

> [!Note]
> Si vous recevez une `Could not find a part of the path … bin\roslyn\csc.exe` erreur, mettez à jour le paquet avec la commande `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` . Pour plus d’informations, [voir cette question sur Stack Overflow](https://stackoverflow.com/questions/32780315).

## <a name="host-the-sample-app"></a>Hébergez l’exemple d’application

Les applications Microsoft Teams sont des applications Web qui fournissent une ou plusieurs fonctionnalités. Pour que Teams plate-forme pour charger votre application, votre application doit être disponible sur Internet. Pour ce faire, vous devez héberger votre application. Vous pouvez soit l’héberger Microsoft Azure gratuitement ou créer un tunnel vers le processus local sur votre ordinateur en utilisant `ngrok` . Après avoir héberger votre application, notez son URL racine, telle `https://yourteamsapp.ngrok.io` ou `https://yourteamsapp.azurewebsites.net` .

### <a name="tunnel-using-ngrok"></a>Tunnel’utilisation de ngrok

Pour des tests rapides, vous pouvez exécuter l’application sur votre ordinateur et créer un tunnel vers elle à travers un point d’évaluation web. [`ngrok`](https://ngrok.com) est un outil gratuit avec lequel vous pouvez obtenir une adresse Web, comme `https://d0ac14a5.ngrok.io` . Vous pouvez [télécharger et installer](https://ngrok.com/download) ngrok et l’ajouter à un emplacement dans votre `PATH` .

Après votre `ngrok` installation, ouvrez une nouvelle fenêtre terminale et exécutez la commande suivante pour créer un tunnel :

```bash
ngrok http 44327 -host-header=localhost:44327
```

`Ngrok` écoute les demandes d’Internet et les a adage vers votre application fonctionnant sur le port 44327. Pour vérifier, ouvrez votre navigateur et allez `https://d0ac14a5.ngrok.io/hello` charger la page bonjour de votre application. Au lieu de cette URL, utilisez l’adresse de forwarding affichée dans `ngrok` votre session console.

> [!NOTE]
> Si vous avez utilisé un port différent dans l’étape [de construction et d’exécuter,](#build-and-run-the-sample) assurez-vous d’utiliser le même numéro de port pour configurer `ngrok` le tunnel.

> [!TIP]
> C’est une bonne idée de courir `ngrok` dans une fenêtre terminale différente. Ceci est fait pour empêcher de `ngrok` courir sans interférer avec l’application. Vous devez arrêter, reconstruire et réexécuter l’application. La `ngrok` session fournit des informations utiles de débogage dans cette fenêtre.

L’application n’est disponible que pendant la session en cours sur votre ordinateur. Si la machine est arrêtée ou s’en veille, le service n’est plus disponible. Rappelez-vous cela lorsque vous partagez l’application pour les tests à d’autres utilisateurs. Si vous devez redémarrer le service, l’application renvoie une nouvelle adresse et vous devez mettre à jour chaque emplacement qui utilise cette adresse. La version payante de `ngrok` n’a pas cette limitation.

### <a name="host-in-azure"></a>Hôte en Azure

Microsoft Azure votre application .NET sur un niveau gratuit en utilisant l’infrastructure partagée. Cela suffit pour exécuter `Hello World` l’échantillon. Pour plus d’informations, [voir création d’un nouveau compte Azure gratuit](https://azure.microsoft.com/free/).

Visual Studio a intégré la prise en charge du déploiement d’applications à différents fournisseurs, y compris Azure :

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a>Mettre à jour les informations d’identification de votre application hébergée

L’exemple d’application nécessite que les variables de l’environnement soient définies en fonction des valeurs que vous avez enregistrées dans le fichier texte.

Ouvrez le fichier `appsettings.json`. Mettez à jour **la valeur MicrosoftAppId** avec votre identifiant bot que vous avez enregistré dans le fichier texte. Mettez à jour **le MicrosoftAppPassword avec le** mot de passe bot que vous avez enregistré.

<img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

Une fois ces modifications apportées, reconstruisez l’application. Si vous utilisez ngrok, exécutez l’application localement et si vous hébergez azure, redéploiez l’application.

## <a name="configure-the-app-tab"></a>Configurer l’onglet app

Une fois que vous installez l’application dans une équipe, vous devez la configurer pour afficher le contenu. Rendez-vous sur un canal de l’équipe où vous avez installé l’exemple **d’application et sélectionnez le bouton '+'** pour ajouter un nouvel onglet. Choisissez **Hello World dans** la liste Ajouter **un** onglet. Une boîte de dialogue de configuration est affichée qui vous permet de choisir l’onglet à afficher dans ce canal. Après avoir sélectionné l’onglet et sélectionné **Enregistrer l’onglet** `Hello World` est chargé avec l’onglet.

<img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a>Testez votre bot en Teams

Maintenant, vous pouvez tester le bot dans Teams. Sélectionnez un canal dans l’équipe où vous avez enregistré votre application et tapez `@your-bot-name` . C’est ce qu’on **\@ appelle une mention**. Le bot répond à tout message que vous envoyez.

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a>Testez votre extension de messagerie

Pour tester votre extension de messagerie, vous pouvez sélectionner ... en **dessous de** la boîte d’entrée dans votre vue de conversation. Un menu avec **l’application 'Hello World'** est affiché. Lorsque vous le sélectionnez, un ensemble de textes aléatoires s’affiche. Vous pouvez sélectionner l’un des textes aléatoires et qui est inséré dans votre conversation.

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

Sélectionnez l’un des textes aléatoires. Une carte formatée et prête à envoyer avec votre propre message est affichée.

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
