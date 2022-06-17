---
title: Déployer votre première application à l’aide de Node.js dans App Studio
description: Découvrez comment déployer des applications Microsoft Teams avec Node.js dans App Studio
keywords: prise en main de node.js App Studio
ms.custom: scenarios:getting-started; languages:ASP,Node.js
ms.localizationpriority: medium
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: 15b5837fb8155d8b34b2c337a550ecbaaae9d86a
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142520"
---
# <a name="update-nodejs-app-package-in-app-studio"></a>Mettre à jour Node.js package d’application dans App Studio

> [!TIP]
> **Essayez le portail des développeurs** : App Studio a évolué. Configurez, distribuez et gérez vos applications Teams avec la nouvelle [Developer Portal](https://dev.teams.microsoft.com/).

App Studio est une application Teams que vous pouvez installer à partir du magasin Teams. Elle simplifie la création et l’inscription d’une application.

Effectuez les étapes suivantes pour mettre à jour le package d’application :

1. Pour installer App Studio dans Teams, sélectionnez l’icône **Applications** en bas de la barre de gauche, puis recherchez **App Studio** :

    <img  width="450px" alt="Finding App Studio in the Store View" src="~/assets/images/get-started/searchforAppStudio.png"/>

1. Sélectionnez la vignette **App Studio** et choisissez **Installer**. App Studio est installé :

    <img  width="450px" alt="Installing App Studio" src="~/assets/images/get-started/InstallingAppStudio.png"/>

1. Pour créer le package d’application pour votre application Teams, sélectionnez l’onglet **Éditeur de manifeste** dans **App Studio** :

    <img  width="450px" alt="App Studio" src="~/assets/images/get-started/AppStudio.png"/>

    L’exemple est fourni avec son propre manifeste et est conçu pour générer un package d’application lors de la génération du projet. Sur Node.js, cette opération est effectuée en tapant `gulp` la ligne de commande dans le répertoire racine du projet.

    Vous pouvez générer le package d’application sur Node.js en tapant `gulp` la ligne de commande dans le répertoire racine du projet.

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

    Le nom du package d’application généré est `helloworldapp.zip`. Vous pouvez rechercher ce fichier si l’emplacement n’est pas clair dans l’outil que vous utilisez.

1. Maintenant, pour modifier ce package d’application, sélectionnez **Importer une application existante** dans **l’éditeur de manifeste :**

    <img  width="450px" alt="Importing an existing app" src="~/assets/images/get-started/Importinganapp.png"/>

1. Sélectionnez la vignette **Hello World** pour votre application nouvellement importée :

    <img  width="450px" alt="Newly imported app view" src="~/assets/images/get-started/HelloWorldappdetails.png"/>

    L’image suivante montre le package d’application importé dans App Studio :

    <img  width="450px" alt="Importing the app package" src="~/assets/images/get-started/Importinganapp2.png"/>

    Sur le côté gauche de l’éditeur de manifeste se trouve une liste d’étapes. Sur le côté droit se trouve une liste de propriétés qui doivent être renseignées pour chaque étape. Lorsque vous avez commencé avec un exemple d’application, une grande partie des informations est déjà terminée. Les étapes suivantes vous permettent de mettre à jour les propriétés de l’application Hello World.

## <a name="app-details"></a>Détails de l’application

Sélectionnez **Les détails de l’application** sous **Détails**. Sélectionnez le bouton **Générer** pour créer un ID d’application.

Votre nouvel ID d’application est similaire à `2322041b-72bf-459d-b107-f4f335bc35bd`.

Parcourez les détails de l’application dans le volet droit, y compris les **informations du développeur** et les détails **de personnalisation** . Ces détails sont importants si vous écrivez une nouvelle application pour la distribution.

## <a name="tabs"></a>Onglets

Il est simple d’ajouter des onglets à une application Teams. L’exemple d’application prend déjà en charge plusieurs onglets, et vous pouvez les activer.

### <a name="team-tab"></a>Onglet Équipe

Votre application ne peut avoir qu’un seul onglet Équipe :

<img  width="450px" alt="Adding a Teams tab" src="~/assets/images/get-started/TeamTab.png"/>

Dans cet exemple, l’onglet Équipe est l’emplacement où votre page de configuration s’affiche. Sélectionnez le symbole **...** de **l’URL de configuration Tab** , puis choisissez **Modifier** dans le menu déroulant. Remplacez l’URL `https://yourteamsapp.ngrok.io/configure` `yourteamsapp.ngrok.io` par celle que vous avez utilisée lors de l’hébergement de votre application.

### <a name="personal-tabs"></a>Onglets personnels

Votre application peut contenir jusqu’à 16 onglets, y compris l’onglet Équipe.

Les onglets personnels sont différents de l’onglet Équipe. **L’onglet Hello** est déjà répertorié dans la liste des onglets personnels avec une valeur `com.contoso.helloworld.hellotab`d’espace réservé. Sélectionnez le symbole **...** de **l’URL de configuration Tab** , puis choisissez **Modifier** dans le menu déroulant. La boîte de dialogue suivante s’affiche :

<img  width="450px" alt="Adding a personal tab dialog" src="~/assets/images/get-started/PersonalTab.png"/>

Mettez à jour les zones suivantes avec l’URL de votre application :

* Remplacez la zone **URL de contenu** par `https://yourteamsapp.ngrok.io/hello`
* Remplacez la zone **URL du site web** par `https://yourteamsapp.ngrok.io/hello`

Remplacez `yourteamsapp.ngrok.io` par l’URL que vous avez utilisée lors de l’hébergement de votre application.

#### <a name="bots"></a>Bots

Il est facile d’ajouter les fonctionnalités des bots à votre application. **L’exemple d’application Hello World** possède déjà un bot dans le cadre de l’exemple, mais vous devez l’inscrire auprès de Microsoft :

<img  width="450px" alt="Adding a bot" src="~/assets/images/get-started/Bots.png"/>

Le bot qui a été importé à partir de l’exemple n’a pas d’ID d’application associé. Vous devez créer un bot afin qu’App Studio puisse créer un ID d’application et l’inscrire auprès de Microsoft.

> [!NOTE]
> L’ID d’application créé par App Studio pour le bot est différent de l’ID d’application créé pour l’application. Chaque bot d’une application nécessite son propre ID d’application.

Effectuez les étapes suivantes pour configurer votre bot :

1. Sélectionnez **Supprimer** en regard du bot importé dans la liste des bots. Il n’y a plus de bots à afficher.
1. Sélectionnez **Configurer** pour afficher la boîte de dialogue **Configurer un bot** .

    <img  width="450px" alt="Adding a bot dialog" src="~/assets/images/get-started/Setupbot.png"/>

1. Ajoutez un **bot contoso** et activez les trois cases à cocher sous **Étendue**.
1. Choisissez **Enregistrer** pour quitter la boîte de dialogue. App Studio inscrit votre bot auprès de Microsoft et affiche votre nouveau bot dans la liste des bots.
1. Ouvrez maintenant un fichier texte dans le Bloc-notes et copiez et collez votre nouvel ID de bot.
1. Cliquez sur **Générer un nouveau mot de passe** et notez le mot de passe dans le même fichier texte que celui que vous avez noté pour votre ID d’application de bot.
1. Mettez à jour **l’adresse** `https://yourteamsapp.ngrok.io/api/messages`du point de terminaison du bot et remplacez-la par `yourteamsapp.ngrok.io` l’URL que vous avez utilisée lors de l’hébergement de votre application.
1. Enregistrez maintenant votre fichier texte, car vous devez ajouter les informations du fichier à votre application hébergée pour permettre une communication sécurisée avec votre bot.

#### <a name="messaging-extensions"></a>Extensions de messagerie

Les extensions de messagerie permettent aux utilisateurs de demander des informations à votre service et de publier ces informations. Les informations sont publiées sous la forme de cartes dans la conversation de canal. Les extensions de messagerie apparaissent en bas de la zone de rédaction.

Effectuez les étapes suivantes pour configurer votre extension de messagerie :

1. Sélectionnez **Extensions de messagerie** sous **Fonctionnalités** dans le volet gauche d’App Studio pour configurer l’extension de messagerie :

    <img  width="450px" alt="Adding a messaging extension" src="~/assets/images/get-started/Messagingextensions.png"/>

    L’exemple d’extension de messagerie est répertorié dans le volet **Extensions de messagerie** .

1. Sélectionnez **Supprimer** pour supprimer l’extension de messagerie, **sélectionnez Configurer** et suivez les mêmes [étapes que pour les bots](#bots). La boîte **de dialogue Extension de messagerie** s’affiche.
1. Sélectionnez l’onglet **Utiliser un bot existant** , puis **Sélectionnez dans l’un de mes bots existants**.
1. Sélectionnez le bot que vous avez créé dans le menu déroulant. Ajoutez un **nom de bot** , puis **sélectionnez Enregistrer** pour fermer la boîte de dialogue.
1. Dans la section **Commande** , sélectionnez **Ajouter**. Pour ajouter une commande basée sur la recherche, sélectionnez **autoriser les utilisateurs à interroger votre service pour obtenir des informations, puis insérez-les dans une option de message** .
1. Dans la boîte de **dialogue Nouvelle commande** , entrez les valeurs suivantes :

    Sous **Nouvelle commande** :

    * **ID de commande** : entrez du texte aléatoire
    * **Titre** : Entrer un titre aléatoire
    * **Description** : Entrez une description aléatoire

    Sous **Paramètre** :

    * **Nom** : entrez le nom du paramètre
    * **Titre** : Entrez le titre de la carte
    * **Description** : Entrer la description de la carte

1. Après avoir entré les informations, **sélectionnez Enregistrer** pour fermer la boîte de dialogue.

#### <a name="register-your-app-in-teams"></a>Inscrire votre application dans Teams

Après avoir entré les détails de votre application, effectuez les étapes suivantes pour inscrire votre application dans Teams :

1. Utilisez **Test et distribution** d’App Studio pour installer votre application dans Teams.
1. Mettez à jour votre application hébergée avec l’ID d’application et le mot de passe de votre bot. Pour l’exemple d’application, utilisez le même ID d’application et le même mot de passe pour l’extension de bot et de messagerie.
1. Sélectionnez **Tester et distribuez**  sous **Terminer** dans le volet gauche d’App Studio :

    <img  width="450px" alt="Testing your app" src="~/assets/images/get-started/Testanddistribute.png"/>

1. Pour charger votre application sur Teams, sélectionnez le bouton **Installer** sous **Tester et distribuer** :

    <img  width="450px" alt="Adding a messaging extension dialog" src="~/assets/images/get-started/InstallingHelloWorld.png"/>

    > [!NOTE]
    > Si vous ne parvenez pas à charger une version test de l’application, vérifiez si vous avez [activé le chargement d’application personnalisée](../get-started/get-started-dotnet-app-studio.md#enable-sideloading-option).

1. Sélectionnez la zone **de recherche** dans la section **Ajouter à une équipe** , puis sélectionnez une équipe pour ajouter l’exemple d’application. Vous pouvez configurer une équipe spéciale pour les tests.
1. Sélectionnez le bouton **Installer** en bas de la boîte de dialogue.

    Votre application est désormais disponible dans Teams. Toutefois, le bot et l’extension de messagerie ne fonctionnent pas tant que vous n’avez pas mis à jour l’environnement des applications hébergées avec les ID d’application et les mots de passe.

    <img  width="450px" alt="The finished app" src="~/assets/images/get-started/Finishedhelloworld.png"/>

## <a name="update-the-credentials-for-your-hosted-app"></a>Mettre à jour les informations d’identification de votre application hébergée

L’exemple d’application nécessite que les variables d’environnement suivantes soient définies sur les valeurs que vous avez notagées précédemment :

```
MICROSOFT_APP_ID=<YOUR BOT'S APP ID>
MICROSOFT_APP_PASSWORD=<YOUR BOT'S PASSWORD>
WEBSITE_NODE_DEFAULT_VERSION=8.9.4
```

Les variables d’environnement font partie de votre environnement. Seul le code de votre application peut y accéder. Ils ne sont exposés à aucun tiers.

Si vous exécutez l’application à l’aide de ngrok, vous devez configurer des variables d’environnement locales. Vous pouvez utiliser Visual Studio Code pour ajouter une [configuration de lancement](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations) :

```json
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

Emplacement :

* Les informations d’identification d’autorisation de votre bot sont les suivantes :
  * MICROSOFT_APP_ID est ID.
  * MICROSOFT_APP_PASSWORD est un mot de passe.
* NODE_DEBUG vous montrer ce qui se passe dans votre bot dans la console de débogage Visual Studio Code
* NODE_CONFIG_DIR pointe vers le répertoire à la racine du référentiel (par défaut, lorsque l’application est exécutée localement, elle recherche le répertoire racine dans le `src` dossier).

> [!Note]
> Si vous n’avez pas arrêté npm plus tôt dans le didacticiel, vous devez `npm stop` exécuter pour que Visual Studio Code collecte correctement vos variables de configuration de lancement.

<a name="ConfigureTheAppTab"></a>

## <a name="test-the-app-capabilities-in-teams"></a>Tester les fonctionnalités de l’application dans Teams

Après avoir installé l’application dans Teams, vous devez la configurer pour afficher le contenu.

### <a name="test-your-tab-in-teams"></a>Tester votre onglet dans Teams

1. Accédez à un canal dans Teams, puis sélectionnez le bouton **« + »** pour ajouter un nouvel onglet.
1. Vous pouvez ensuite choisir `Hello World` dans la liste **Ajouter un onglet** .
1. Dans la boîte de dialogue de configuration, sélectionnez l’onglet à afficher dans le canal. Ensuite, **sélectionnez Enregistrer**.

Vous pouvez voir l’onglet `Hello World` chargé avec l’onglet que vous avez choisi :

<img width="430px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png"/>

### <a name="test-your-bot-in-teams"></a>Tester votre bot dans Teams

Vous pouvez désormais interagir avec le bot dans Teams. Choisissez un canal dans l’équipe où vous avez inscrit votre application, puis tapez `@your-bot-name`, suivi de votre message. Ce type de message est appelé **mention\@**. Le message que vous envoyez au bot vous sera renvoyé en réponse :

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png"/>

<a name="ComposeRichMessages"></a>

### <a name="test-your-messaging-extension"></a>Tester votre extension de messagerie

Pour tester votre extension de messagerie :

1. Sélectionnez les trois points sous la zone d’entrée dans votre vue de conversation. Un menu avec l’application **« Hello World »** s’affiche.
1. Sélectionnez le menu. Un ensemble de textes aléatoires s’affiche. Vous pouvez sélectionner l’un des textes aléatoires insérés dans votre conversation.

    <img width="430px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu1.png" />

    <img width="430px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result1.png" />

1. Sélectionnez l’un des textes aléatoires. La carte mise en forme apparaît prête à être envoyée avec votre propre message inclus en bas :

    <img width="430px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />

| &nbsp; | &nbsp; |
|:--- | ---:|
|[Back](get-started-overview.md) | &nbsp; |
|
