---
title: Prise en main d’App Studio et de Node.js
description: Commencer à créer des applications intéressantes dans Microsoft teams à l’aide de Node.js et d’App Studio
keywords: mise en route node.js NodeJS App Studio
ms.topic: tutorial
ms.custom: scenarios:getting-started; languages:JavaScript,Node.js
ms.openlocfilehash: 3d86738d32c049d31a84c6c47746e275db5e6349
ms.sourcegitcommit: 99c35de7e2c604bd8bce392242c2c2fa709cd50b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/06/2020
ms.locfileid: "48931812"
---
# <a name="get-started-on-the-microsoft-teams-platform-with-nodejs-and-app-studio"></a>Prise en main de la plateforme Microsoft teams avec Node.js et App Studio

La plateforme de développement [Microsoft teams](/microsoftteams/) vous permet d’étendre facilement teams et d’intégrer vos propres applications et services de façon transparente dans l’espace de travail de teams. Ces applications peuvent ensuite être distribuées à votre entreprise ou pour teams dans le monde entier.

Pour étendre Microsoft Teams, vous devez créer une application Microsoft Teams. Une application Microsoft teams est une application Web que vous hébergez. Cette application peut ensuite être intégrée dans l’espace de travail de l’utilisateur dans Teams.

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="DownloadAndHost"></a>

## <a name="download-and-host-your-app"></a>Télécharger et héberger votre application

Procédez comme suit pour télécharger et héberger une application « Hello World » simple dans Teams.

<a name="GetPrerequisites"></a>

### <a name="get-prerequisites"></a>Obtenir les conditions préalables

Pour effectuer ce didacticiel, vous avez besoin des outils suivants. Si vous ne les avez pas encore installés, vous pouvez les installer à partir de ces liens.

- [Git](https://git-scm.com/downloads)
- [Node.js et NPM](https://nodejs.org/)
- Obtenir un éditeur de texte ou IDE. Vous pouvez installer et utiliser [Visual Studio code](https://code.visualstudio.com/download) gratuitement.

Si vous voyez des options permettant d’ajouter `git` ,, `node` `npm` , et `code` le chemin d’accès pendant l’installation, choisissez de le faire. Il sera pratique.

Vérifiez que les outils sont disponibles en exécutant ce qui suit dans une fenêtre de terminal :

> [!NOTE]
> Utilisez la fenêtre de terminal qui vous convient le mieux sur votre plateforme. Ces exemples utilisent bash (inclus dans Git), mais ces scripts s’exécuteront sur la plupart des plateformes.

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

Vous disposez peut-être d’une autre version de ces applications. Cela ne doit pas être un problème, à l’exception de Gulp. Pour Gulp, vous devez utiliser la version 4.0.0 ou une version ultérieure.

Si Gulp n’est pas installé (ou si vous n’avez pas installé la version incorrecte), faites-le maintenant en exécutant la `npm install gulp` fenêtre de votre terminal.

Si vous avez installé Visual Studio code, vous pouvez vérifier l’installation en exécutant :

```bash
code --version
1.28.2
929bacba01ef658b873545e26034d1a8067445e9
```

Vous pouvez continuer à utiliser cette fenêtre de terminal pour exécuter les commandes qui suivent dans ce didacticiel.

<a name="DownloadSample"></a>

### <a name="download-the-sample"></a>Télécharger l’exemple

Nous avons fourni un simple [Hello, World !](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs) exemple pour vous aider à démarrer. Dans une fenêtre de terminal, exécutez la commande suivante pour cloner le référentiel de l’exemple sur votre ordinateur local :

```bash
git clone https://github.com/OfficeDev/msteams-samples-hello-world-nodejs.git
```

> [!TIP]
> Vous pouvez [bifurquer](https://help.github.com/articles/fork-a-repo/) sur cette [référentiel](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs) si vous voulez modifier et archiver les modifications apportées à votre référentiel GitHub à des fins de référence ultérieure.

<a name="BuildRun"></a>

### <a name="build-and-run-the-sample"></a>Création et exécution de l’exemple

Une fois le référentiel cloné, accédez au répertoire qui contient l’exemple :

```bash
cd msteams-samples-hello-world-nodejs
```

Pour générer l’exemple, vous devez installer toutes ses dépendances. Pour ce faire, exécutez la commande suivante :

```bash
npm install
```

Vous devriez voir une série de dépendances installées. Une fois ces opérations terminées, vous pouvez exécuter l’application :

```bash
npm start
```

Lors du démarrage de l’application Hello-World, celle-ci s’affiche `App started listening on port 3333` dans la fenêtre du terminal.

> [!NOTE]
> Si vous voyez un numéro de port différent affiché dans le message ci-dessus, c’est qu’une variable d’environnement de PORT est définie. Vous pouvez continuer à utiliser ce port ou modifier votre variable d’environnement sur 3333.

À ce stade, vous pouvez ouvrir une fenêtre de navigateur et accéder aux URL suivantes pour vérifier que toutes les URL d’application sont en cours de chargement :

- [http://localhost:3333](http://localhost:3333)
- [http://localhost:3333/hello](http://localhost:3333/hello)
- [http://localhost:3333/first](http://localhost:3333/first)
- [http://localhost:3333/second](http://localhost:3333/second)

<a name="HostSample"></a>

### <a name="host-the-sample-app"></a>Héberger l’exemple d’application

N’oubliez pas que les applications dans Microsoft teams sont des applications Web qui exposent une ou plusieurs fonctionnalités. Pour que la plateforme teams charge votre application, votre application doit être accessible à partir d’Internet. Pour permettre à votre application d’être accessible à partir d’Internet, vous devez *héberger* votre application.

Pour les tests locaux, vous pouvez exécuter l’application sur votre ordinateur local et y créer un tunnel à l’aide d’un point de terminaison Web. [ngrok](https://ngrok.com) est un outil gratuit qui vous permet d’effectuer cette opération. Avec *ngrok* , vous pouvez obtenir une adresse Web telle que `https://d0ac14a5.ngrok.io` (cette URL n’est qu’un exemple). Vous pouvez [Télécharger et installer](https://ngrok.com/download) *ngrok* pour votre environnement. Veillez à l’ajouter à un emplacement dans votre `PATH` .

Une fois que vous l’avez installé, vous pouvez ouvrir une nouvelle fenêtre de terminal et exécuter la commande suivante pour créer un tunnel. L’exemple utilise le port 3333, veillez donc à le spécifier ici.

```bash
ngrok http 3333 -host-header=localhost:3333
```

*Ngrok* écoutera les demandes en provenance d’Internet et les acheminera vers votre application en cours d’exécution sur le port 3333. Vous pouvez vérifier en ouvrant votre navigateur et en accédant à `https://d0ac14a5.ngrok.io/hello` pour charger la page Hello de votre application. Veillez à utiliser l’adresse de transfert affichée par *ngrok* dans votre session de console au lieu de cette URL.

> [!NOTE]
> Si vous avez utilisé un port différent dans l’étape de [création et d’exécution](#build-and-run-the-sample) ci-dessus, assurez-vous d’utiliser le même numéro de port pour configurer le tunnel *ngrok* .
> [!TIP]
> Il est judicieux d’exécuter *ngrok* dans une autre fenêtre de terminal pour continuer à fonctionner sans interférer avec l’application de nœud que vous devrez peut-être arrêter, reconstruire et réexécuter. La session *ngrok* renverra des informations utiles sur le débogage dans cette fenêtre.

Il existe une version payante d' *ngrok* qui autorise les noms persistants. Si vous utilisez la version gratuite, votre application ne sera disponible que pendant la session en cours sur votre ordinateur de développement. Si l’ordinateur est arrêté ou passe en mode veille, le service n’est plus disponible. Souvenez-vous de ceci lors du partage de l’application pour le test par d’autres utilisateurs. Si vous devez redémarrer le service, il renverra une nouvelle adresse et vous devrez mettre à jour chaque emplacement qui utilise cette adresse.

N’oubliez pas d’indiquer l’URL de votre application, car vous en aurez besoin plus tard lors de l’inscription de l’application auprès de teams à l’aide d’App Studio. Le bloc-notes fonctionne à cet effet.

<a name="DeployToTeams"></a>

## <a name="deploy-your-app-to-microsoft-teams"></a>Déployer votre application dans Microsoft teams

À ce stade, vous disposez d’une application hébergée sur Internet, mais vous n’avez aucun moyen d’indiquer à teams où le Rechercher, ni même ce que votre application est appelée. Pour ce faire, vous devez maintenant créer un package d’application. Il ne s’agit que d’un fichier texte qui contient le manifeste de l’application et de certaines icônes que le client teams utilisera pour afficher et personnaliser correctement votre application. Vous pouvez créer manuellement ce package d’application, ou vous pouvez utiliser app Studio, un outil qui s’exécute dans teams pour simplifier le processus d’inscription de l’application. Il est recommandé d’App Studio pour créer et mettre à jour le package d’application.

Pour les deux méthodes, vous aurez besoin des éléments suivants :

- URL où votre application peut être trouvée sur Internet.
- Icônes que teams utilisera pour personnaliser votre application. L’exemple est fourni avec des icônes d’espace réservé situées dans «src\static\images. App Studio fournira également les icônes par défaut si nécessaire.

[!include[Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-your-hosted-app"></a>Mettre à jour votre application hébergée

L’exemple d’application requiert que les variables d’environnement suivantes soient définies sur les valeurs que vous avez notées précédemment.

```
MICROSOFT_APP_ID=<YOUR BOT'S APP ID>
MICROSOFT_APP_PASSWORD=<YOUR BOT'S PASSWORD>
WEBSITE_NODE_DEFAULT_VERSION=8.9.4
```

La manière dont vous effectuez cette opération diffère selon la manière dont vous avez hébergé votre application. L’utilisation de variables d’environnement est importante dans la mesure où ces valeurs font partie de votre environnement : elles sont accessibles par le code de votre application, mais elles ne sont pas exposées à des tiers qui peuvent examiner les fichiers qui composent votre site.

Si vous exécutez l’application à l’aide de ngrok, vous devez configurer certaines variables d’environnement locales. Il existe de nombreuses façons de le faire, mais le plus simple, si vous utilisez Visual Studio code, est d’ajouter une [configuration de lancement](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations):

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

MICROSOFT_APP_ID et MICROSOFT_APP_PASSWORD sont respectivement l’ID et le mot de passe de votre robot.
NODE_DEBUG vous montrera ce qui se passe dans votre bot dans la console de débogage de code Visual Studio.
NODE_CONFIG_DIR pointe vers le répertoire situé à la racine du référentiel (par défaut, lorsque l’application est exécutée localement, elle la recherche dans le dossier src).

> [!Note]
> Si vous n’avez pas arrêté NPM de la version antérieure dans le didacticiel, vous devrez exécuter pour que `npm stop` Visual Studio code collecte correctement vos variables de configuration de lancement.

<a name="ConfigureTheAppTab"></a>

## <a name="configure-the-app-tab"></a>Configurer l’onglet application

Une fois que vous avez installé l’application dans une équipe, vous devez la configurer pour afficher le contenu. Accédez à un canal de l’équipe et cliquez sur le bouton **« + »** pour ajouter un nouvel onglet. Vous pouvez ensuite choisir `Hello World` dans la liste **Ajouter un onglet** . Une boîte de dialogue de configuration s’affiche. Cette boîte de dialogue vous permet de choisir l’onglet à afficher dans ce canal. Une fois que vous avez sélectionné l’onglet, puis cliqué sur, `Save` vous pouvez voir l' `Hello World` onglet chargé avec l’onglet que vous avez choisi.

<img width="430px" src="~/assets/images/samples-hello-world-tab-configure.png" alt-text="Screenshot of configure" />

### <a name="test-your-bot-in-teams"></a>Tester votre robot dans teams

Vous pouvez désormais interagir avec le bot dans Teams. Sélectionnez un canal dans l’équipe où vous avez enregistré votre application, puis tapez `@your-bot-name` , suivi de votre message. Il s’agit d’une **\@ mention**. Tout message que vous envoyez au bot vous sera renvoyé en tant que réponse.

<img width="450px" alt-text="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

<a name="ComposeRichMessages"></a>

### <a name="test-your-messaging-extension"></a>Tester votre extension de messagerie

Pour tester votre extension de messagerie, vous pouvez cliquer sur les trois points sous la zone d’entrée de votre affichage conversation. Un menu s’affiche avec l’application **« Hello World »** . Lorsque vous cliquez dessus, vous verrez un certain nombre de textes aléatoires. Vous pouvez choisir l’un d’entre eux et l’insérer dans votre conversation.

<img width="430px" alt-text="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="430px" alt-text="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

Choisissez l’un des textes aléatoires, et vous verrez une carte formatée et prête à envoyer avec votre propre message en bas.

<img width="430px" alt-text="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
