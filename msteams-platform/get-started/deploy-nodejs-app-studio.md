---
title: Déployer votre première application à l'Node.js dans App Studio
description: Découvrez comment déployer des applications Microsoft Teams avec Node.js dans App Studio
keywords: mise en node.js App Studio
ms.custom: scenarios:getting-started; languages:ASP,Node.js
ms.localizationpriority: medium
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: ea6e85f2552504cdb98959ef8ab585f9afa90e6f
ms.sourcegitcommit: 22c9e44437720d30c992a4a3626a2a9f745983c1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2021
ms.locfileid: "60720942"
---
# <a name="update-nodejs-app-package-in-app-studio"></a>Mettre à jour Node.js package d’application dans App Studio

> [!TIP]
> **Essayez le portail du développeur**: App Studio a évolué. Configurez, distribuez et gérez vos applications Teams avec le nouveau [portail du développeur.](https://dev.teams.microsoft.com/)

App Studio est une application Teams que vous pouvez installer à partir du Teams store. Cela simplifie la création et l’inscription d’une application.

Pour mettre à jour le package d’application, vous suivrez les étapes suivantes :

1. Pour installer App Studio dans Teams,  sélectionnez l’icône Applications en bas de la barre de gauche, puis recherchez **App Studio**:

    <img  width="450px" alt="Finding App Studio in the Store View" src="~/assets/images/get-started/searchforAppStudio.png"/>

1. Sélectionnez la **vignette App Studio** et choisissez **Installer.** App Studio est installé :

    <img  width="450px" alt="Installing App Studio" src="~/assets/images/get-started/InstallingAppStudio.png"/>

1. Pour créer le package d’application pour votre application Teams, sélectionnez l’onglet Éditeur de **manifeste** dans **App Studio**:

    <img  width="450px" alt="App Studio" src="~/assets/images/get-started/AppStudio.png"/>

    L’exemple est livré avec son propre manifeste et est conçu pour créer un package d’application lorsque le projet est créé. Sur Node.js, cette fonction est effectuée en tapant la ligne de commande dans le répertoire `gulp` racine du projet.

    Vous pouvez créer le package d’application Node.js en tapant sur la ligne de commande dans le répertoire `gulp` racine du projet.

    ```bash
    $ gulp
    [13:39:27] Using gulpfile ~\documents\github\msteams-samples-hello-world-nodejs\gulpfile.js
    [13:39:27] Starting 'clean'...
    [13:39:27] Starting 'generate-manifest'...
    [13:39:27] Finished 'generate-manifest' after 11 ms
    [13:39:27] Finished 'clean' after 21 ms
    [13:39:27] Starting 'default'...
    Build completed. Output in manifest folder
    [13:39:27] Finished 'default' after 62 μs
    ```

    Le nom du package d’application généré est **helloworldapp.zip**. Vous pouvez rechercher ce fichier si l’emplacement n’est pas clair dans l’outil que vous utilisez.

1. Maintenant, pour modifier ce package d’application, **sélectionnez Importer** une application existante dans l’éditeur **de manifeste**:

    <img  width="450px" alt="Importing an existing app" src="~/assets/images/get-started/Importinganapp.png"/>

1. Sélectionnez **la vignette Hello World** pour votre application nouvellement importée :

    <img  width="450px" alt="Newly imported app view" src="~/assets/images/get-started/HelloWorldappdetails.png"/>

    L’image suivante montre le package d’application importé dans App Studio :

    <img  width="450px" alt="Importing the app package" src="~/assets/images/get-started/Importinganapp2.png"/>

    Sur le côté gauche de l’éditeur de manifeste se trouve une liste d’étapes. Sur le côté droit se trouve une liste des propriétés qui doivent être remplies pour chaque étape. Lorsque vous avez commencé avec un exemple d’application, la plupart des informations sont déjà terminées. Les étapes suivantes vous permettent de mettre à jour les propriétés de l’application Hello World.

#### <a name="app-details"></a>Détails de l’application

Sélectionnez **les détails de l’application** **sous Détails.** Sélectionnez **le bouton** Générer pour créer un ID d’application.

Votre nouvel ID d’application est similaire à `2322041b-72bf-459d-b107-f4f335bc35bd` .

Dans le volet droit, vous allez voir  les détails de l’application, y compris les informations sur le développeur et les **détails de** pertinence. Ces détails sont importants si vous écrivez une nouvelle application pour la distribution.

#### <a name="tabs"></a>Onglets

Il est simple d’ajouter des onglets à une Teams application. L’exemple d’application prend déjà en charge plusieurs onglets et vous pouvez les activer.

##### <a name="team-tab"></a>Onglet Équipe

Votre application ne peut avoir qu’un seul onglet d’équipe :

<img  width="450px" alt="Adding a Teams tab" src="~/assets/images/get-started/TeamTab.png"/>

Dans cet exemple, l’onglet Équipe est l’endroit où votre page de configuration s’affiche. Sélectionnez **le symbole ...** de l’URL de configuration de l’onglet et choisissez **Modifier** dans le menu déroulant.  Remplacez l’URL par l’URL que vous avez utilisée lors de `https://yourteamsapp.ngrok.io/configure` `yourteamsapp.ngrok.io` l’hébergement de votre application.

##### <a name="personal-tabs"></a>Onglets personnels

Votre application peut avoir jusqu’à 16 onglets, y compris l’onglet Équipe.

Les onglets personnels sont différents de l’onglet Équipe. **L’onglet Hello** est déjà répertorié dans la liste des onglets personnels avec une valeur d’espace `com.contoso.helloworld.hellotab` réservé. Sélectionnez **le symbole ...** de l’URL de configuration de l’onglet et choisissez **Modifier** dans le menu déroulant.  La boîte de dialogue suivante s’affiche :

<img  width="450px" alt="Adding a personal tab dialog" src="~/assets/images/get-started/PersonalTab.png"/>

Mettez à jour les zones suivantes avec l’URL de votre application :

- Modifier la **zone URL** de contenu en `https://yourteamsapp.ngrok.io/hello`
- Modifier la zone **URL du site** web en `https://yourteamsapp.ngrok.io/hello`

Remplacez `yourteamsapp.ngrok.io` par l’URL que vous avez utilisée lors de l’hébergement de votre application.

#### <a name="bots"></a>Bots

Il est facile d’ajouter la fonctionnalité bots à votre application. **L’exemple d’application Hello World** possède déjà un bot dans le cadre de l’exemple, mais vous devez l’inscrire auprès de Microsoft :

<img  width="450px" alt="Adding a bot" src="~/assets/images/get-started/Bots.png"/>

Le bot qui a été importé à partir de l’exemple n’a pas d’ID d’application associé. Vous devez créer un bot pour qu’App Studio puisse créer un ID d’application et l’inscrire auprès de Microsoft.

> [!NOTE]
> L’ID d’application créé par App Studio pour le bot est différent de l’ID d’application créé pour l’application. Chaque bot d’une application nécessite son propre ID d’application.

Pour configurer votre bot, complétez les étapes suivantes :

1. Sélectionnez **Supprimer** en face du bot importé dans la liste des bots. Il ne reste plus aucun bot à afficher. 
1. Sélectionnez **Programme d’installation** pour afficher la boîte de dialogue Configurer **un bot.**

    <img  width="450px" alt="Adding a bot dialog" src="~/assets/images/get-started/Setupbot.png"/>

1. Ajoutez un nom de bot **Contoso bot** et cochez les trois cases sous **Étendue**.
1. Sélectionnez **Enregistrer** pour quitter la boîte de dialogue. App Studio enregistre votre bot auprès de Microsoft et affiche votre nouveau bot dans la liste des bots. 
1. À présent, ouvrez un fichier texte dans le bloc-notes et copiez-y votre nouvel ID de bot.
1. Cliquez **sur Générer un nouveau** mot de passe et notez le mot de passe dans le même fichier texte que celui où vous avez noté votre ID d’application de bot.
1. Mettez à jour **l’adresse du point** de terminaison du bot et remplacez-la par l’URL que vous avez `https://yourteamsapp.ngrok.io/api/messages` utilisée lors de `yourteamsapp.ngrok.io` l’hébergement de votre application.
1. Enregistrez maintenant votre fichier texte, car vous devez ajouter les informations du fichier à votre application hébergée pour permettre une communication sécurisée avec votre bot.

#### <a name="messaging-extensions"></a>Extensions de messagerie

Les extensions de messagerie permet aux utilisateurs de demander des informations à votre service et de publier ces informations. Les informations sont publiées sous forme de cartes dans la conversation de canal. Les extensions de messagerie apparaissent en bas de la zone de composition.

Pour configurer votre extension de messagerie, complétez les étapes suivantes :

1. Sélectionnez **les extensions de messagerie** sous **Fonctionnalités** dans le volet gauche d’App Studio pour configurer l’extension de messagerie :

    <img  width="450px" alt="Adding a messaging extension" src="~/assets/images/get-started/Messagingextensions.png"/>

    L’exemple d’extension de messagerie est répertorié dans le volet **Extensions** de messagerie.

1. Sélectionnez **Supprimer** pour supprimer l’extension de messagerie, sélectionnez **Configurer** et suivez les mêmes étapes que pour les [bots.](#bots) La **boîte de dialogue Extension** de messagerie s’affiche.
1. Sélectionnez **l’onglet Utiliser le bot** existant et **sélectionnez l’un de mes bots existants.**
1. Sélectionnez le bot que vous avez créé dans le menu déroulant. Ajoutez un **nom de bot** et **sélectionnez Enregistrer** pour fermer la boîte de dialogue.
1. Sous la section **Commande,** sélectionnez **Ajouter.** Pour ajouter une commande basée sur la recherche, sélectionnez l’option Autoriser les utilisateurs à interroger votre service pour obtenir des informations et insérez-la dans une option **de message.**
1. Dans la **boîte de dialogue Nouvelle commande,** entrez les valeurs suivantes :

    Sous **nouvelle commande**:

    - **ID de commande**: entrer du texte aléatoire
    - **Titre**: entrer un titre aléatoire
    - **Description**: entrez une description aléatoire

    Sous **paramètre**:

    - **Name**: Entrez le nom du paramètre
    - **Titre**: entrez le titre de la carte
    - **Description**: entrez la description de la carte

1. Après avoir entré les informations, **sélectionnez Enregistrer** pour fermer la boîte de dialogue.

#### <a name="register-your-app-in-teams"></a>Inscrire votre application dans Teams

Une fois que vous avez entré les détails de votre application, complétez les étapes suivantes pour inscrire votre application dans Teams :

1. Utilisez **Test et distribuez** App Studio pour installer votre application dans Teams. 
1. Mettez à jour votre application hébergée avec l’ID d’application et le mot de passe de votre bot. Pour l’exemple d’application, utilisez les mêmes ID d’application et mot de passe pour le bot et l’extension de messagerie. 
1. Sélectionnez **Test et distribuez-le** **sous Terminer** dans le volet gauche d’App Studio :

    <img  width="450px" alt="Testing your app" src="~/assets/images/get-started/Testanddistribute.png"/>

1. Pour télécharger votre application sur Teams, sélectionnez le bouton **Installer** sous **Tester et distribuer**:

    <img  width="450px" alt="Adding a messaging extension dialog" src="~/assets/images/get-started/InstallingHelloWorld.png"/>

    > [!NOTE]
    > Si vous ne parvenez pas à charger une version de version de chargement de l’application, vérifiez si vous avez activé le téléchargement [d’applications personnalisées.](../get-started/get-started-dotnet-app-studio.md#enable-sideloading-option)

1. Sélectionnez **la zone de** recherche dans la section Ajouter à **une** équipe et sélectionnez une équipe pour ajouter l’exemple d’application. Vous pouvez configurer une équipe spéciale pour les tests.
1. Sélectionnez **le bouton** Installer en bas de la boîte de dialogue.

    Votre application est désormais disponible dans Teams. Toutefois, le bot et l’extension de messagerie ne fonctionneront pas tant que vous n’aurez pas mis à jour l’environnement d’applications hébergée avec les ID d’application et les mots de passe.

    <img  width="450px" alt="The finished app" src="~/assets/images/get-started/Finishedhelloworld.png"/>

## <a name="update-the-credentials-for-your-hosted-app"></a>Mettre à jour les informations d’identification de votre application hébergée

L’exemple d’application nécessite que les variables d’environnement suivantes soient définies sur les valeurs que vous avez not es précédemment :

```
MICROSOFT_APP_ID=<YOUR BOT'S APP ID>
MICROSOFT_APP_PASSWORD=<YOUR BOT'S PASSWORD>
WEBSITE_NODE_DEFAULT_VERSION=8.9.4
```

Les variables d’environnement font partie de votre environnement. Seul le code de votre application peut y accéder. Elles ne sont exposées à aucun tiers.

Si vous exécutez l’application à l’aide de ngrok, vous devez configurer des variables d’environnement local. Vous pouvez utiliser Visual Studio Code pour ajouter une [configuration de lancement](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations):

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

- Les informations d’identification d’autorisation pour votre bot sont les suivantes :
  - MICROSOFT_APP_ID est l’ID
  - MICROSOFT_APP_PASSWORD mot de passe
- NODE_DEBUG vous montrer ce qui se passe dans votre bot dans la console Visual Studio Code débogage
- NODE_CONFIG_DIR pointe vers le répertoire à la racine du référentiel (par défaut, lorsque l’application est exécuté localement, elle recherche le répertoire racine dans le `src` dossier).

> [!Note]
> Si vous n’avez pas arrêté npm plus tôt dans le didacticiel, vous devrez l’exécuter pour que Visual Studio Code collecte correctement vos variables de `npm stop` configuration de lancement.

<a name="ConfigureTheAppTab"></a>

## <a name="test-the-app-capabilities-in-teams"></a>Tester les fonctionnalités de l’application dans Teams

Après avoir installé l’application dans Teams, vous devez la configurer pour afficher le contenu.

### <a name="test-your-tab-in-teams"></a>Testez votre onglet dans Teams

1. Go to a channel in Teams, and select the **'+'** button to add a new tab.
1. Vous pouvez ensuite choisir `Hello World` dans la liste Ajouter un **onglet.**
1. Dans la boîte de dialogue de configuration, sélectionnez l’onglet à afficher dans le canal. Ensuite, sélectionnez **Enregistrer.** 

Vous pouvez voir `Hello World` l’onglet chargé avec l’onglet que vous avez choisi :

<img width="430px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png"/>

### <a name="test-your-bot-in-teams"></a>Testez votre bot dans Teams

Vous pouvez désormais interagir avec le bot dans Teams. Choisissez un canal dans l’équipe où vous avez inscrit votre application, puis tapez `@your-bot-name` , suivi de votre message. Ce type de message est appelé **\@ mention.** Le message que vous envoyez au bot vous sera renvoyé en tant que réponse :

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png"/>

<a name="ComposeRichMessages"></a>

### <a name="test-your-messaging-extension"></a>Tester votre extension de messagerie

**Pour tester votre extension de messagerie**
1. Sélectionnez les trois points sous la zone d’entrée dans votre affichage conversation. Un menu avec **l’application « Hello World** » s’affiche.
1. Sélectionnez le menu. Un ensemble de textes aléatoires s’affiche. Vous pouvez sélectionner l’un des textes aléatoires insérés dans votre conversation.

    <img width="430px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu1.png" />

    <img width="430px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result1.png" />

1. Sélectionnez l’un des textes aléatoires. La carte mise en forme apparaît prête à être envoyé avec votre propre message inclus en bas :

    <img width="430px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />


| &nbsp; | &nbsp; |
|:--- | ---:|
|[Back](get-started-overview.md) | &nbsp; |
|