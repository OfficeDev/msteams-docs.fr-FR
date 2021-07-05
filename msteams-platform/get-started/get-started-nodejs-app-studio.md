---
title: 'Didacticiel : créer votre première application à l’aide Node.js'
description: Découvrez comment commencer à créer des applications Microsoft Teams avec Node.js.
keywords: mise en node.js nodejs App Studio
ms.topic: tutorial
localization_priority: Normal
ms.custom: scenarios:getting-started; languages:JavaScript,Node.js
ms.openlocfilehash: 84c3452c739f67c2908d698b627b5651ff9d5d7a
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254351"
---
# <a name="build-your-first-microsoft-teams-app-using-nodejs"></a>Créer votre première application Microsoft Teams l’aide Node.js

Dans ce didacticiel, vous allez apprendre à créer votre toute première application Microsoft Teams l’aide Node.js. Il vous permet également de suivre les étapes suivantes : 

1. [Préparer votre environnement](#prepare-environment)
1. [Obtenir les conditions préalables](#GetPrerequisites)
1. [Télécharger l’exemple](#DownloadSample)
1. [Création et exécution de l’exemple](#BuildRun)
1. [Héberger l’exemple d’application](#HostSample)
1. [Mettre à jour les informations d’identification de votre application hébergée](#updatecredentials)
1. [Configurer l’onglet de l’application](#ConfigureTheAppTab)

<a name="prepare-environment"></a>

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

### <a name="download-and-host-your-app"></a>Télécharger et héberger votre application

Suivez ces étapes pour télécharger et héberger une application « hello world » simple dans Teams.

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a>Obtenir les conditions préalables

Pour effectuer ce didacticiel, vous avez besoin des outils suivants. Si vous ne les avez pas encore, vous pouvez les installer à partir de ces liens.

- [Git](https://git-scm.com/downloads)
- [Node.js et NPM](https://nodejs.org/)
- Obtenez n’importe quel éditeur de texte ou IDE. Vous pouvez installer et utiliser [Visual Studio Code](https://code.visualstudio.com/download) gratuitement.

Si des options s’offrent à vous pour ajouter , et pour le CHEMIN d’accès lors de `git` `node` `npm` `code` l’installation, sélectionnez les options. 

Vérifiez que les outils sont disponibles en exécutant ce qui suit dans une fenêtre terminal :

> [!NOTE]
> Utilisez la fenêtre terminal avec qui vous êtes le plus à l’aise sur votre plateforme. Ces exemples utilisent Bash (qui est inclus dans Git), mais ces scripts s’exécuteront sur la plupart des plateformes.

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

Vous pouvez avoir une version différente de ces applications. Cela ne doit pas être un problème, à l’exception de Gulp. Pour gulp, vous devez utiliser la version 4.0.0 ou ultérieure.

Si gulp n’est pas installé (ou si la version est mal installée), exécutez-le maintenant dans la `npm install gulp` fenêtre de votre terminal.

Si vous avez installé Visual Studio Code, vous pouvez vérifier l’installation en exécutant :

```bash
code --version
1.28.2
929bacba01ef658b873545e26034d1a8067445e9
```

Vous pouvez continuer à utiliser cette fenêtre terminal pour exécuter les commandes qui suivent dans ce didacticiel.

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a>Télécharger l’exemple

Nous avons fourni un simple [Hello World !](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/nodejs) pour commencer. Dans une fenêtre terminal, exécutez la commande suivante pour cloner l’exemple de référentiel sur votre ordinateur local :

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> Vous pouvez [bifurcation](https://help.github.com/articles/fork-a-repo/) [de ce repo](https://github.com/OfficeDev/Microsoft-Teams-Samples) si vous souhaitez modifier et vérifier vos modifications apportées à votre GitHub de données pour référence ultérieure.

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a>Création et exécution de l’exemple

Une fois le référentiel cloné, exécutez la commande de répertoire de modification dans le terminal pour changer le répertoire en exemple :

```bash
cd Microsoft-Teams-Samples/samples/app-hello-world/nodejs/
```

Pour créer l’exemple, vous devez installer toutes ses dépendances. Pour ce faire, exécutez la commande suivante :

```bash
npm install
```

Vous devriez voir un grand nombre de dépendances installées. Après l’installation, vous pouvez exécuter l’application avec la commande suivante :

```bash
npm start
```

Lorsque l’application Hello World démarre, elle s’affiche `App started listening on port 3333` dans la fenêtre du terminal.

> [!NOTE]
> Si vous voyez un autre numéro de port affiché dans le message ci-dessus, c’est parce que vous avez un ensemble de variables d’environnement PORT. Vous pouvez continuer à utiliser ce port ou modifier votre variable d’environnement en 3333.

À ce stade, vous pouvez ouvrir une fenêtre de navigateur et accéder aux URL suivantes pour vérifier que toutes les URL d’application sont en cours de chargement :

- `http://localhost:3333`
- `http://localhost:3333/hello`
- `http://localhost:3333/first`
- `http://localhost:3333/second`

<a name="HostSample"></a>

## <a name="deploy-your-sample-app"></a>Déployer votre exemple d’application

N’oubliez pas que les applications Microsoft Teams sont des applications web qui exposent une ou plusieurs fonctionnalités. Pour que la Teams charge votre application, votre application doit être accessible à partir d’Internet. Pour rendre votre application accessible à partir d’Internet, vous devez *l’héberger.*

Pour les tests locaux, vous pouvez exécuter l’application sur votre ordinateur local et créer un tunnel vers celui-ci avec un point de terminaison web. [ngrok est](https://ngrok.com) un outil gratuit qui vous permet de le faire. Avec *ngrok,* vous pouvez obtenir une adresse web telle que `https://d0ac14a5.ngrok.io` (cette URL n’est qu’un exemple). Vous pouvez [télécharger et installer](https://ngrok.com/download) *ngrok* pour votre environnement. Veillez à l’ajouter à un emplacement dans votre `PATH` .

Après l’avoir installée, vous pouvez ouvrir une nouvelle fenêtre terminal et exécuter la commande suivante pour créer un tunnel. L’exemple utilise le port 3333, donc n’oubliez pas de le spécifier ici :

```bash
ngrok http 3333 -host-header=localhost:3333
```

*Ngrok écoutera* les demandes provenant d’Internet et les dirigera vers votre application en cours d’exécution sur le port 3333. Vous pouvez vérifier en ouvrant votre navigateur et en allant `https://d0ac14a5.ngrok.io/hello` charger la page Hello de votre application. Assurez-vous d’utiliser l’adresse de forwarding affichée par *ngrok dans* votre session console au lieu de cette URL.

> [!NOTE]
> Si vous avez utilisé un [](#build-and-run-the-sample) autre port dans la build et l’étape d’utilisation ci-dessus, veillez à utiliser le même numéro de port pour configurer le tunnel *ngrok.*
> [!TIP]
> Il est bon d’exécuter *ngrok* dans une autre fenêtre terminal pour la maintenir en cours d’exécution sans interférer avec l’application de nœud que vous de devez peut-être arrêter, reconstruire et réexécuter par la suite. La session *ngrok* retourne des informations de débogage utiles dans cette fenêtre.

Il existe une version payante de *ngrok* qui autorise les noms persistants. Si vous utilisez la version gratuite, votre application sera disponible uniquement pendant la session en cours sur votre ordinateur de développement. Si l’ordinateur est arrêté ou en veille, le service n’est plus disponible. N’oubliez pas cela lors du partage de l’application pour les tests effectués par d’autres utilisateurs. Si vous devez redémarrer le service, il retourne une nouvelle adresse et vous devez mettre à jour chaque endroit qui utilise cette adresse.

Notez l’URL de votre application. Vous en aurez besoin ultérieurement lorsque vous enregistrerez l’application auprès Teams App Studio ou le portail du développeur.

<a name="DeployToTeams"></a>

## <a name="deploy-your-app-to-microsoft-teams"></a>Déployer votre application sur Microsoft Teams

À ce stade, vous avez une application hébergée sur Internet, mais vous n’avez pas encore le moyen d’Teams où la rechercher, ni même ce que votre application appelle. Pour ce faire, vous devez maintenant créer un package d’application. Il s’agit d’un peu plus qu’un fichier texte qui contient le manifeste de l’application et certaines icônes que le client Teams utilisera pour afficher et marque correctement votre application. Vous pouvez créer manuellement ce package d’application, ou vous pouvez utiliser App Studio ou le portail de développement, des outils qui s’exécutent dans Teams, ce qui simplifie le processus d’inscription de l’application. App Studio et le portail de développement sont les méthodes recommandées pour créer et mettre à jour le package d’application.

Pour l’une ou l’autre des méthodes, vous aurez besoin des méthodes suivantes :

- URL dans laquelle votre application est disponible sur Internet.
- Icônes que Teams utilisera pour brander votre application. L’exemple est livré avec des icônes d’espace réservé situées dans « src\static\images ». App Studio fournit également des icônes par défaut si nécessaire.

**Mettre à jour le package d’application**

# <a name="app-studio"></a>[App Studio](#tab/AS)

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

# <a name="developer-portal"></a>[Portail du développeur](#tab/DP)

**Pour installer le portail du développeur (prévisualisation) dans Teams**

1. Sélectionnez **l’icône** Applications en bas de la barre de gauche, puis recherchez **Portail du développeur.**

    <img width="430px" alt="Screenshot of TDP" src="~/assets/images/Screen1.png"/>

1. Sélectionnez **Portail du développeur** et **Ouvrez.**

    <img width="430px" alt="Screenshot of TDP Open" src="~/assets/images/screen2.png"/>

1. Sélectionnez l’onglet Applications et **sélectionnez Importer une application existante.**

    <img width="430px" alt="Screenshot of import app in tdp" src="~/assets/images/screen3.png"/>

1. Sélectionnez **Hello World** et **sélectionnez Importer.** **L’application Hello World** est importée dans le Portail des développeurs. 

    Vous pouvez configurer votre application à l’aide du portail Teams développeur. Le manifeste se trouve sous Distribuer. Vous pouvez utiliser le manifeste pour configurer des fonctionnalités, des ressources requises et d’autres attributs importants pour votre application. Pour plus d’informations sur la configuration de votre application à l’aide du Portail du développeur, voir [Teams Portail du développeur.](../concepts/build-and-test/teams-developer-portal.md)

    <img width="430px" alt="Screenshot of configure tdp" src="~/assets/images/Screen4.png"/>

---
<a name="updatecredentials"></a>

## <a name="update-the-credentials-for-your-hosted-app"></a>Mettre à jour les informations d’identification de votre application hébergée

L’exemple d’application nécessite que les variables d’environnement suivantes soient définies sur les valeurs que vous avez not es précédemment :

```
MICROSOFT_APP_ID=<YOUR BOT'S APP ID>
MICROSOFT_APP_PASSWORD=<YOUR BOT'S PASSWORD>
WEBSITE_NODE_DEFAULT_VERSION=8.9.4
```

La façon dont vous le faites diffère en fonction de la façon dont vous avez hébergé votre application. L’élément important de l’utilisation des variables d’environnement est que ces valeurs font partie de votre environnement : elles sont accessibles par le code de votre application, mais elles ne sont pas exposées à des tiers qui peuvent examiner les fichiers qui constitueront votre site.

Si vous exécutez l’application à l’aide de ngrok, vous devez configurer certaines variables d’environnement local. Il existe plusieurs façons de le faire, mais la plus simple, si vous utilisez Visual Studio Code, consiste à ajouter une [configuration de lancement](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations):

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

Où :

MICROSOFT_APP_ID et MICROSOFT_APP_PASSWORD est l’ID et le mot de passe, respectivement, pour votre bot.
NODE_DEBUG vous montre ce qui se passe dans votre bot dans la console Visual Studio Code débogage.
NODE_CONFIG_DIR pointe vers le répertoire à la racine du référentiel (par défaut, lorsque l’application est exécuté localement, elle le recherche dans le dossier src).

> [!Note]
> Si vous n’avez pas arrêté npm plus tôt dans le didacticiel, vous devrez l’exécuter pour que Visual Studio Code collecte correctement vos variables de `npm stop` configuration de lancement.

<a name="ConfigureTheAppTab"></a>

## <a name="configure-the-app-tab"></a>Configurer l’onglet de l’application

Après avoir installé l’application dans une équipe, vous devez la configurer pour afficher le contenu. Go to a channel in the team and click on the **'+'** button to add a new tab. Vous pouvez ensuite choisir `Hello World` dans la liste Ajouter un **onglet.** Une boîte de dialogue de configuration s’est ensuite présentée. Cette boîte de dialogue vous permet de choisir l’onglet à afficher dans ce canal. Une fois que vous avez sélectionné l’onglet et cliqué sur **Enregistrer,** vous pouvez voir l’onglet chargé `Hello World` avec l’onglet que vous avez choisi :

<img width="430px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png"/>

### <a name="test-your-bot-in-teams"></a>Testez votre bot dans Teams

Vous pouvez désormais interagir avec le bot dans Teams. Choisissez un canal dans l’équipe où vous avez inscrit votre application, puis tapez `@your-bot-name` , suivi de votre message. C’est ce qu’on appelle **\@ une mention.** Le message que vous envoyez au bot vous sera renvoyé en tant que réponse :

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png"/>

<a name="ComposeRichMessages"></a>

### <a name="test-your-messaging-extension"></a>Tester votre extension de messagerie

**Pour tester votre extension de messagerie**
1. Sélectionnez les trois points sous la zone d’entrée dans votre affichage conversation. Un menu avec **l’application « Hello World** » s’affiche.
1. Sélectionnez le menu. Un ensemble de textes aléatoires s’affiche. Vous pouvez sélectionner l’un des textes aléatoires insérés dans votre conversation.

    <img width="430px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu1.png" />

    <img width="430px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result1.png" />

1. Sélectionnez l’un des textes aléatoires et vous verrez une carte mise en forme et prête à être envoyé avec votre propre message en bas :

    <img width="430px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />

 ## <a name="see-also"></a>Voir aussi

* [Présentation des didacticiels](code-samples.md)
* [Créer une application de bot de conversation](first-app-bot.md)
* [Créer une extension de messagerie](first-message-extension.md)
* [Exemples de code](https://github.com/OfficeDev/Microsoft-Teams-Samples)