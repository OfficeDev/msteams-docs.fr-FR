---
title: Déployer votre première application à l’aide de C# dans App Studio
description: Découvrez comment déployer des applications Microsoft Teams avec C# ou .NET. dans App Studio
keywords: prise en main de .net c# csharp app studio
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
ms.localizationpriority: medium
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: 6fa0b290b0d0918c02427959b96eb897931aa4de
ms.sourcegitcommit: c398dfdae9ed96f12e1401ac7c8d0228ff9c0a2b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/30/2022
ms.locfileid: "66558456"
---
# <a name="update-c-app-package-in-app-studio"></a>Mettre à jour le package d’application C# dans App Studio

> [!TIP]
> **Essayez le portail des développeurs** : App Studio a évolué. Configurez, distribuez et gérez vos applications Teams avec la nouvelle [Developer Portal](https://dev.teams.microsoft.com/).

App Studio est une application Teams que vous pouvez installer à partir du Magasin Teams. Elle simplifie la création et l’inscription d’une application.

Effectuez les étapes suivantes pour mettre à jour le package d’application :

1. Pour installer App Studio dans Teams, sélectionnez l’icône **Applications** en bas de la barre de gauche, puis recherchez **App Studio** :

    <img  width="450px" alt="Finding App Studio in the Store View" src="~/assets/images/get-started/searchforAppStudio.png"/>

1. Sélectionnez la vignette **App Studio** et choisissez **Installer**. App Studio est installé :

    <img  width="450px" alt="Installing App Studio" src="~/assets/images/get-started/InstallingAppStudio.png"/>

1. Pour créer le package d’application pour votre application Teams, sélectionnez l’onglet **Éditeur de manifeste** dans **App Studio** :

    <img  width="450px" alt="App Studio" src="~/assets/images/get-started/AppStudio.png"/>

    L’exemple est fourni avec son propre manifeste et est conçu pour générer un package d’application lors de la génération du projet. Le fichier manifest.json peut se trouver dans Visual Studio dans le manifeste sous ```Microsoft.Teams.Samples.HelloWorld.Web```.

     Dans Visual Studio, le fichier manifest.json se trouve sous **Manifest** in `Microsoft.Teams.Samples.HelloWorld.Web`. Cette étape est décrite par l’image suivante :  

    <img  width="450px" alt="Build the app package on .NET with Visual Studio" src="~/assets/images/get-started/app-package-on-.NET-with-Visual-Studio.png"/>

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

- Remplacez la zone **URL de contenu** par `https://yourteamsapp.ngrok.io/hello`
- Remplacez la zone **URL du site web** par `https://yourteamsapp.ngrok.io/hello`

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

    - **ID de commande** : entrez du texte aléatoire
    - **Titre** : Entrer un titre aléatoire
    - **Description** : Entrez une description aléatoire

    Sous **Paramètre** :

    - **Nom** : entrez le nom du paramètre
    - **Titre** : Entrez le titre de la carte
    - **Description** : Entrer la description de la carte

1. Après avoir entré les informations, **sélectionnez Enregistrer** pour fermer la boîte de dialogue.

#### <a name="register-your-app-in-teams"></a>Inscrire votre application dans Teams

Après avoir entré les détails de votre application, effectuez les étapes suivantes pour inscrire votre application dans Teams :

1. Utilisez **test et distribution** d’App Studio pour installer votre application dans Teams.
1. Mettez à jour votre application hébergée avec l’ID d’application et le mot de passe de votre bot. Pour l’exemple d’application, utilisez le même ID d’application et le même mot de passe pour l’extension de bot et de messagerie.
1. Sélectionnez **Tester et distribuez**  sous **Terminer** dans le volet gauche d’App Studio :

    <img  width="450px" alt="Testing your app" src="~/assets/images/get-started/Testanddistribute.png"/>

1. Pour charger votre application dans Teams, sélectionnez le bouton **Installer** sous **Tester et distribuer** :

    <img  width="450px" alt="Adding a messaging extension dialog" src="~/assets/images/get-started/InstallingHelloWorld.png"/>

    > [!NOTE]
    > Si vous ne parvenez pas à charger une version test de l’application, vérifiez si vous avez [activé le chargement d’application personnalisée](../get-started/get-started-dotnet-app-studio.md#enable-sideloading-option).

1. Sélectionnez la zone **de recherche** dans la section **Ajouter à une équipe** , puis sélectionnez une équipe pour ajouter l’exemple d’application. Vous pouvez configurer une équipe spéciale pour les tests.
1. Sélectionnez le bouton **Installer** en bas de la boîte de dialogue.

    Votre application est désormais disponible dans Teams. Toutefois, le bot et l’extension de messagerie ne fonctionnent pas tant que vous n’avez pas mis à jour l’environnement des applications hébergées avec les ID d’application et les mots de passe.

    <img  width="450px" alt="The finished app" src="~/assets/images/get-started/Finishedhelloworld.png"/>

## <a name="register-your-app-in-teams"></a>Inscrire votre application dans Teams

Après avoir entré les détails de votre application, effectuez les étapes suivantes pour inscrire votre application dans Teams :

1. Utilisez la **préversion** du portail des développeurs pour installer votre application dans Teams.

    :::image type="content" source="../assets/images/teams-toolkit-v2/preview-in-teams.png" alt-text="Image montrant le bouton Aperçu":::

1. Mettez à jour votre application hébergée avec l’ID d’application et le mot de passe de votre bot. Pour l’exemple d’application, utilisez le même ID d’application et le même mot de passe pour l’extension de bot et de messagerie.

1. Sélectionnez **Publier pour stocker**  sous **Publier** dans le volet gauche du portail des développeurs :

    :::image type="content" source="../assets/images/teams-toolkit-v2/devp-publish-left-pane.png" alt-text="Image montrant l’option Publier dans le volet gauche":::

    > [!NOTE]
    > Si vous ne parvenez pas à charger une version test de l’application, vérifiez si vous avez [activé le chargement d’application personnalisée](../get-started/get-started-dotnet-app-studio.md#enable-sideloading-option).

1. Sélectionnez **Ajouter** pour installer l’application sur Teams.

    Votre application est désormais disponible dans Teams. Toutefois, le bot et l’extension de messagerie ne fonctionnent pas tant que vous n’avez pas mis à jour l’environnement des applications hébergées avec les ID d’application et les mots de passe.

## <a name="update-the-credentials-for-your-hosted-app"></a>Mettre à jour les informations d’identification de votre application hébergée

L’exemple d’application nécessite que les variables d’environnement soient définies sur les valeurs que vous avez enregistrées dans le fichier texte.

1. Ouvrez le Explorateur de solutions.

    :::image type="content" source="../assets/images/get-started/csharp-repo-cloned.png" alt-text="Exemple de référentiel pour l’application Teams c#":::

1. Ouvrez le fichier `appsettings.json`.

    :::image type="content" source="../assets/images/teams-toolkit-v2/csharp-appsetting-json.png" alt-text="Image montrant le fichier appsettings.json":::

1. Mettez à jour la valeur **MicrosoftAppId** avec l’ID de votre bot que vous avez enregistré dans le fichier texte.
1. Mettez à jour **MicrosoftAppPassword** avec le mot de passe du bot que vous avez enregistré.

    :::image type="content" source="../assets/images/get-started/get-started-net-azure-add-keys.png" alt-text="Image montrant l’ajout de clés Azure":::

    Après avoir apporté ces modifications, régénérez l’application. Si vous utilisez ngrok, vous pouvez exécuter l’application localement et, si vous l’avez hébergée dans Azure, redéployez l’application.

## <a name="test-the-app-capabilities-in-teams"></a>Tester les fonctionnalités de l’application dans Teams

### <a name="test-your-tab"></a>Tester votre onglet

Une fois que vous avez installé l’application dans Teams, configurez-la pour afficher l’onglet que vous souhaitez que l’application charge.

Pour configurer l’onglet Application :

1. Accédez à un canal de l’équipe dans laquelle vous avez installé l’exemple d’application, puis sélectionnez le bouton **« + »** pour ajouter un nouvel onglet.
1. Sélectionnez **Hello World** dans la liste **Ajouter un onglet**. Une boîte de dialogue de configuration s’affiche pour vous permettre de sélectionner l’onglet à afficher dans ce canal.
1. Sélectionnez **Enregistrer**. L’onglet `Hello World` est chargé avec l’onglet.

    <img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a>Tester votre bot dans Teams

Vous pouvez maintenant tester le bot dans Teams.

Pour tester votre bot :

- Sélectionnez un canal dans l’équipe dans laquelle vous avez inscrit votre application et tapez `@your-bot-name`. Ce type de message est appelé **mention\@**. Le bot répond à tout message que vous envoyez.

    <img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a>Tester votre extension de messagerie

Pour tester votre extension de messagerie :

1. Sélectionnez **...** sous la zone d’entrée dans votre vue de conversation. Un menu avec l’application **« Hello World »** s’affiche.
1. Sélectionnez le menu. Un ensemble de textes aléatoires s’affiche. Vous pouvez sélectionner l’un des textes aléatoires insérés dans votre conversation.

    <img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu1.png" />

    <img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result1.png" />

1. Sélectionnez l’un des textes aléatoires. Une carte mise en forme et prête à être envoyée avec votre propre message s’affiche.

    <img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />

| &nbsp; | &nbsp; |
|:--- | ---:|
|[Back](get-started-overview.md) | &nbsp; |
|
