---
title: Tutoriel - Créez votre première application à l’aide de Node.js
description: Découvrez comment commencer à créer des applications Microsoft Teams avec Node.js.
keywords: commencer node.js nœuds App Studio
ms.topic: tutorial
localization_priority: Normal
ms.custom: scenarios:getting-started; languages:JavaScript,Node.js
ms.openlocfilehash: 46272671443e07432513b667af424b5c5be05f2e
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566538"
---
# <a name="create-your-first-microsoft-teams-app-using-nodejs"></a>Créez votre première application Microsoft Teams à l’aide Node.js

Ce tutoriel vous aide à démarrer la création d’une application Microsoft Teams en utilisant Node.js.

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="DownloadAndHost"></a>

## <a name="download-and-host-your-app"></a>Téléchargez et hébergez votre application

Suivez ces étapes pour télécharger et héberger une simple application « hello world » en Teams.

<a name="GetPrerequisites"></a>

### <a name="get-prerequisites"></a>Obtenez des conditions préalables

Pour compléter ce tutoriel, vous avez besoin des outils suivants. Si vous ne les avez pas déjà, vous pouvez les installer à partir de ces liens.

- [Git](https://git-scm.com/downloads)
- [Node.js et NPM](https://nodejs.org/)
- Obtenez n’importe quel éditeur de texte ou IDE. Vous pouvez installer et [utiliser Visual Studio Code](https://code.visualstudio.com/download) gratuitement.

Si vous voyez des options à `git` ajouter, `node` , et à la PATH lors de `npm` `code` l’installation, choisissez de le faire. Ce sera pratique.

Vérifiez que les outils sont disponibles en exécutant ce qui suit dans une fenêtre terminale :

> [!NOTE]
> Utilisez la fenêtre terminale avec qui vous êtes le plus à l’aise sur votre plate-forme. Ces exemples utilisent Bash (qui est inclus dans Git), mais ces scripts s’exécuteront sur la plupart des plates-formes.

```bash
$ git --version
git version 2.19.0.windows.1

$ node -v
v8.9.3

$ npm -v
5.5.1

$ gulp -v
CLI version 2.3.0
Local version 4.0.2
```

Vous pouvez avoir une version différente de ces applications. Cela ne devrait pas être un problème, sauf pour la gorgée. Pour avaler, vous devrez utiliser la version 4.0.0 ou plus tard.

Si vous n’avez pas installé de gorgée (ou si vous n’avez pas installé la mauvaise version), faites-le maintenant en courant `npm install gulp` dans la fenêtre de votre terminal.

Si vous avez installé des Visual Studio Code, vous pouvez vérifier l’installation en exécutant :

```bash
code --version
1.28.2
929bacba01ef658b873545e26034d1a8067445e9
```

Vous pouvez continuer à utiliser cette fenêtre terminale pour exécuter les commandes qui suivent dans ce tutoriel.

<a name="DownloadSample"></a>

### <a name="download-the-sample"></a>Télécharger l’échantillon

Nous avons fourni un simple [Bonjour, Monde!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/nodejs) échantillon pour vous aider à démarrer. Dans une fenêtre terminale, exécutez la commande suivante pour cloner le référentiel d’échantillons à votre machine locale :

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> Vous pouvez [fourre-tout](https://help.github.com/articles/fork-a-repo/) [ce repo](https://github.com/OfficeDev/Microsoft-Teams-Samples) si vous souhaitez modifier et vérifier vos modifications à votre GitHub repo pour référence future.

<a name="BuildRun"></a>

### <a name="build-and-run-the-sample"></a>Création et exécution de l’exemple

Une fois le repo cloné, modifiez l’annuaire qui contient l’échantillon :

```bash
cd Microsoft-Teams-Samples/samples/app-hello-world/nodejs/
```

Afin de construire l’échantillon, vous devez installer toutes ses dépendances. Exécutez la commande suivante pour ce faire :

```bash
npm install
```

Vous devriez voir un tas de dépendances s’installer. Une fois qu’ils sont terminés, vous pouvez exécuter l’application:

```bash
npm start
```

Lorsque l’application hello-world démarre, elle `App started listening on port 3333` s’affiche dans la fenêtre terminale.

> [!NOTE]
> Si vous voyez un numéro de port différent affiché dans le message ci-dessus, c’est parce que vous avez un ensemble variable d’environnement PORT. Vous pouvez continuer à utiliser ce port ou modifier votre variable environnement à 3333.

À ce stade, vous pouvez ouvrir une fenêtre de navigateur et naviguer vers les URL suivantes pour vérifier que toutes les URL de l’application sont le chargement:

- `http://localhost:3333`
- `http://localhost:3333/hello`
- `http://localhost:3333/first`
- `http://localhost:3333/second`

<a name="HostSample"></a>

### <a name="host-the-sample-app"></a>Hébergez l’exemple d’application

N’oubliez pas que les applications Microsoft Teams sont des applications Web exposant une ou plusieurs fonctionnalités. Pour que Teams plate-forme pour charger votre application, votre application doit être accessible à partir d’Internet. Pour rendre votre application accessible à partir d’Internet, vous devez *héberger* votre application.

Pour les tests locaux, vous pouvez exécuter l’application sur votre machine locale et créer un tunnel vers elle avec un point de terminaison Web. [ngrok](https://ngrok.com) est un outil gratuit qui vous permet de le faire. Avec *ngrok vous* pouvez obtenir une adresse Web telle que `https://d0ac14a5.ngrok.io` (cette URL n’est qu’un exemple). Vous pouvez [télécharger et installer](https://ngrok.com/download) *ngrok* pour votre environnement. Assurez-vous de l’ajouter à un emplacement dans votre `PATH` .

Une fois que vous l’installez, vous pouvez ouvrir une nouvelle fenêtre terminale et exécuter la commande suivante pour créer un tunnel. L’échantillon utilise le port 3333, alors assurez-vous de le spécifier ici:

```bash
ngrok http 3333 -host-header=localhost:3333
```

*Ngrok écoutera* les demandes d’Internet et les acheminera vers votre application fonctionnant sur le port 3333. Vous pouvez vérifier en ouvrant votre navigateur et en allant `https://d0ac14a5.ngrok.io/hello` charger la page bonjour de votre application. S’il vous plaît assurez-vous d’utiliser l’adresse de forwarding *affichée par ngrok* dans votre session console au lieu de cette URL.

> [!NOTE]
> Si vous avez utilisé un port différent dans la construction [et courez étape](#build-and-run-the-sample) au-dessus, assurez-vous d’utiliser le même numéro de port pour configurer le tunnel *ngrok.*
> [!TIP]
> C’est une bonne idée *d’exécuter ngrok* dans une fenêtre terminale différente pour le garder en cours d’exécution sans interférer avec l’application nœud que vous pourriez plus tard avoir à arrêter, reconstruire et réexécuter. La session *ngrok* retournera des informations utiles de débogage dans cette fenêtre.

Il existe une version payante de *ngrok qui permet* des noms persistants. Si vous utilisez la version gratuite, votre application ne sera disponible que pendant la session en cours sur votre machine de développement. Si la machine est arrêtée ou s’enort, le service ne sera plus disponible. Rappelez-vous cela lorsque vous partagez l’application pour les tests par d’autres utilisateurs. Si vous devez redémarrer le service, il vous retournera une nouvelle adresse et vous devrez mettre à jour chaque endroit qui utilise cette adresse.

N’oubliez pas, notez l’URL de votre application car vous en aurez besoin plus tard lorsque vous enregistrez l’application avec Teams’Application studio. Bloc-notes fonctionne très bien à cette fin.

<a name="DeployToTeams"></a>

## <a name="deploy-your-app-to-microsoft-teams"></a>Déployez votre application Microsoft Teams

À ce stade, vous avez une application hébergée sur Internet, mais vous n’avez aucun moyen encore de dire à Teams où le chercher, ou même ce que votre application est appelée. Pour ce faire, vous devez maintenant créer un package d’application. Ce n’est guère plus qu’un fichier texte qui contient le manifeste de l’application et certaines icônes que le client Teams utilisera pour afficher et brandiner correctement votre application. Vous pouvez créer manuellement ce package d’application, ou vous pouvez utiliser App Studio, un outil qui s’exécute en Teams qui simplifiera le processus d’enregistrement de l’application. App Studio est le moyen recommandé de créer et de mettre à jour le package de l’application.

Pour l’une ou l’autre méthode, vous aurez besoin des éléments suivants :

- L’URL où votre application peut être trouvée sur Internet.
- Icônes que Teams utiliseront pour la marque de votre application. L’échantillon est livré avec des icônes placeholder situé dans « src\static\images. App Studio fournira également des icônes par défaut si nécessaire.

[!include[Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-your-hosted-app"></a>Mettre à jour votre application hébergée

L’exemple d’application nécessite que les variables d’environnement suivantes soient définies en fonction des valeurs que vous avez notées précédemment :

```
MICROSOFT_APP_ID=<YOUR BOT'S APP ID>
MICROSOFT_APP_PASSWORD=<YOUR BOT'S PASSWORD>
WEBSITE_NODE_DEFAULT_VERSION=8.9.4
```

La façon dont vous faites cela diffère selon la façon dont vous avez hébergé votre application. La chose importante au sujet de l’utilisation des variables de l’environnement est que ces valeurs font partie de votre environnement - ils peuvent être consultés par le code de votre application, mais ils ne sont pas exposés à des tiers qui pourraient examiner les fichiers qui composent votre site.

Si vous utilisez l’application à l’aide de ngrok, vous devrez configurer certaines variables d’environnement local. Il existe de nombreuses façons de le faire, mais le plus facile, si vous utilisez Visual Studio Code, est d’ajouter une [configuration de lancement](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations):

``` 
{
    "type": "node",
    "request": "launch",
    "name": "Launch - Teams Debug",
    "program": "${workspaceRoot}/src/app.js",
    "cwd": "${workspaceFolder}/src",
    "env": {
        "BASE_URI": "https://yourNgrokURL.ngrok.io",
        "MICROSOFT_APP_ID": "00000000-0000-0000-0000-000000000000",
        "MICROSOFT_APP_PASSWORD": "yourBotAppPassword",
        "NODE_DEBUG": "botbuilder",
        "SUPPRESS_NO_CONFIG_WARNING": "y",
        "NODE_CONFIG_DIR": "../config"
    }
}
```

Où :

MICROSOFT_APP_ID et MICROSOFT_APP_PASSWORD l’identité et le mot de passe, respectivement, pour votre bot.
NODE_DEBUG vous montrera ce qui se passe dans votre bot dans la console Visual Studio Code débog.
NODE_CONFIG_DIR indique l’annuaire à la racine du référentiel (par défaut, lorsque l’application est gérée localement, elle le recherche dans le dossier src).

> [!Note]
> Si vous n’avez pas arrêté npm de plus tôt dans le tutoriel, vous aurez besoin `npm stop` d’exécuter afin que Visual Studio Code de ramasser vos variables de configuration de lancement correctement.

<a name="ConfigureTheAppTab"></a>

## <a name="configure-the-app-tab"></a>Configurer l’onglet app

Une fois que vous installez l’application dans une équipe, vous devrez la configurer pour afficher le contenu. Allez sur un canal dans l’équipe et cliquez sur **le bouton '+'** pour ajouter un nouvel onglet. Vous pouvez ensuite choisir parmi `Hello World` la liste ajouter **un** onglet. Vous serez alors présenté avec un dialogue de configuration. Ce dialogue vous permettra de choisir l’onglet à afficher dans ce canal. Une fois que vous sélectionnez l’onglet et cliquez `Save` sur vous pouvez voir l’onglet chargé avec `Hello World` l’onglet que vous avez choisi:

<img width="430px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png"/>

### <a name="test-your-bot-in-teams"></a>Testez votre bot en Teams

Vous pouvez maintenant interagir avec le bot dans Teams. Choisissez un canal dans l’équipe où vous avez enregistré votre application, et `@your-bot-name` tapez , suivi de votre message. C’est ce qu’on **\@ appelle une mention**. Quel que soit le message que vous envoyez au bot vous sera renvoyé en réponse :

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png"/>

<a name="ComposeRichMessages"></a>

### <a name="test-your-messaging-extension"></a>Testez votre extension de messagerie

Pour tester votre extension de messagerie, vous pouvez cliquer sur les trois points sous la boîte d’entrée dans votre vue conversation. Un menu apparaîtra avec **l’application 'Hello World'.** Lorsque vous cliquez dessus, vous verrez un certain nombre de textes aléatoires. Vous pouvez choisir l’un d’eux et il sera inséré dans votre conversation:

<img width="430px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="430px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

Choisissez l’un des textes aléatoires, et vous verrez une carte formatée et prête à envoyer avec votre propre message en bas :

<img width="430px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
