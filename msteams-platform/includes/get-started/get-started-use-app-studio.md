### <a name="use-app-studio-to-update-the-app-package"></a>Utilisez App Studio pour mettre à jour le package de l’application

App Studio est une application Teams que vous pouvez installer à partir du magasin Teams’argent. Il simplifie la création et l’enregistrement d’une application.

Remplissez les étapes suivantes pour mettre à jour le package de l’application :

1. Pour installer App Studio en Teams, sélectionnez **l’icône Apps** en bas de la barre de gauche et recherchez **App Studio**:

    <img  width="450px" alt="Finding App Studio in the Store View" src="~/assets/images/get-started/searchforAppStudio.png"/>

1. Sélectionnez **la vignette App Studio** et choisissez **Installer**. L’App Studio est installé :

    <img  width="450px" alt="Installing App Studio" src="~/assets/images/get-started/InstallingAppStudio.png"/>

1. Pour créer le package d’application pour votre application Teams, sélectionnez **l’onglet Éditeur Manifeste** dans App **Studio**:

    <img  width="450px" alt="App Studio" src="~/assets/images/get-started/AppStudio.png"/>

    L’échantillon est livré avec son propre manifeste et est conçu pour construire un paquet d’applications lorsque le projet est construit. Sur .NET cela se fait en Visual Studio et sur Node.js cela se fait en tapant `gulp` à la ligne de commande dans l’annuaire racine du projet.

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

1. Maintenant, pour modifier ce paquet d’applications, **sélectionnez Importer une application existante** dans **l’éditeur Manifeste**:

    <img  width="450px" alt="Importing an existing app" src="~/assets/images/get-started/Importinganapp.png"/>

1. Sélectionnez **la vignette Hello World** pour votre application nouvellement importée :

    <img  width="450px" alt="Newly imported app view" src="~/assets/images/get-started/HelloWorldappdetails.png"/>

L’image suivante montre le paquet d’applications importées dans App Studio :

<img  width="450px" alt="Importing the app package" src="~/assets/images/get-started/Importinganapp2.png"/>

Sur le côté gauche de l’éditeur Manifeste il y a une liste d’étapes. Sur le côté droit il ya une liste de propriétés qui doivent être remplies pour chaque étape. Comme vous avez commencé avec une application d’échantillon, une grande partie de l’information est déjà terminée. Les prochaines étapes vous permettent de mettre à jour les propriétés de l’application Hello World.

#### <a name="app-details"></a>Détails de l’application

Sélectionnez **les détails de l’application** sous **Détails**. Sélectionnez le **bouton Générer** pour créer un nouvel identifiant d’application.

Votre nouvel ID app est similaire à `2322041b-72bf-459d-b107-f4f335bc35bd` .

Passez en compte les détails de l’application dans le volet droit, y compris les informations **sur les développeurs et les** **détails de l’image** de marque. Ces détails sont importants si vous écrivez une nouvelle application pour la distribution.

#### <a name="tabs"></a>Onglets

Il est simple d’ajouter des onglets à une application Teams’eau. L’exemple d’application prend déjà en charge plusieurs onglets, et vous pouvez les activer.

##### <a name="team-tab"></a>Onglet Équipe

Votre application ne peut avoir qu’un seul onglet Équipe :

<img  width="450px" alt="Adding a Teams tab" src="~/assets/images/get-started/TeamTab.png"/>

Dans cet exemple, l’onglet Équipe est l’endroit où votre page de configuration est affichée. Sélectionnez **le symbole ...** de **l’url de configuration** tab et choisissez **Modifier** dans le menu drop-down. Modifiez l’URL à `https://yourteamsapp.ngrok.io/configure` `yourteamsapp.ngrok.io` l’endroit où doit être remplacée par l’URL que vous avez utilisée lors de [l’hébergement de votre application](#host-the-sample-app).

##### <a name="personal-tabs"></a>Onglets personnels

Votre application peut avoir jusqu’à 16 onglets, y compris l’onglet Équipe.

Les onglets personnels sont différents de l’onglet Équipe. **Hello Tab est** déjà répertorié dans la liste des onglets personnels avec une valeur de placeholder `com.contoso.helloworld.hellotab` . Sélectionnez **le symbole ...** de **l’url de configuration** tab et choisissez **Modifier** dans le menu drop-down. La boîte de dialogue suivante apparaît :

<img  width="450px" alt="Adding a personal tab dialog" src="~/assets/images/get-started/PersonalTab.png"/>

Mettez à jour les cases suivantes avec l’URL de votre application :

- Modifiez la **boîte d’URL** de contenu en `https://yourteamsapp.ngrok.io/hello`
- Modifiez la **boîte URL du** site Web pour `https://yourteamsapp.ngrok.io/hello`

Remplacez `yourteamsapp.ngrok.io` par l’URL que vous avez utilisée lors de l’hébergement de votre application.

#### <a name="bots"></a>Bots

Il est facile d’ajouter les fonctionnalités bots à votre application. **L’application hello** world a déjà un bot dans le cadre de l’échantillon, mais vous devez l’enregistrer auprès de Microsoft:

<img  width="450px" alt="Adding a bot" src="~/assets/images/get-started/Bots.png"/>

Le bot qui a été importé de l’échantillon n’a pas d’identifiant app associé. Vous devez créer un nouveau bot afin qu’App Studio puisse créer un nouvel identifiant d’application et l’enregistrer auprès de Microsoft.

> [!NOTE]
> L’ID app créé par App Studio pour le bot est différent de l’ID App créé pour l’application. Chaque bot dans une application nécessite son propre identifiant d’application.

Remplissez les étapes suivantes pour configurer votre bot :

1. Sélectionnez **Supprimer** à côté du bot importé dans la liste des bots. Maintenant, il n’y a plus de bots à montrer. 
1. Sélectionnez **Configuration** pour afficher la **configuration d’une boîte de** dialogue bot.

    <img  width="450px" alt="Adding a bot dialog" src="~/assets/images/get-started/Setupbot.png"/>

1. Ajoutez un bot nom **Contoso bot et sélectionnez** les trois cases à cocher sous **Scope**.
1. Choisissez **Enregistrer pour** sortir de la boîte de dialogue. App Studio enregistre votre bot auprès de Microsoft et affiche votre nouveau bot dans la liste des bots. 
1. Maintenant, ouvrez un fichier texte dans le bloc-notes et copier et coller votre nouvel ID bot en elle.
1. Cliquez **sur Générer un nouveau mot de** passe , et notez le mot de passe dans le même fichier texte que vous avez noté votre ID d’application bot.
1. Mettez à jour **l’adresse du point de terminaison Bot** et `https://yourteamsapp.ngrok.io/api/messages` `yourteamsapp.ngrok.io` remplacez-la par l’URL que vous avez utilisée lors de l’hébergement de votre application.
1. Enregistrez maintenant votre fichier texte car vous devez ajouter les informations du fichier à votre application hébergée pour permettre une communication sécurisée avec votre bot.

#### <a name="messaging-extensions"></a>Extensions de messagerie

Les extensions de messagerie permettent aux utilisateurs de demander des informations à votre service et de publier ces informations. L’information est affichée sous forme de cartes dans la conversation du canal. Les extensions de messagerie apparaissent en bas de la boîte de composition.

Complétez les étapes suivantes pour configurer votre extension de messagerie :

1. Sélectionnez **les extensions** de **messagerie sous capacités** dans le volet gauche d’App Studio pour configurer l’extension de messagerie :

    <img  width="450px" alt="Adding a messaging extension" src="~/assets/images/get-started/Messagingextensions.png"/>

    L’extension de messagerie d’échantillon est répertoriée **dans le volet Extensions** de messagerie.

1. Sélectionnez **Supprimer** pour supprimer l’extension de messagerie, **sélectionnez Configurer** et suivez les mêmes étapes utilisées pour [les bots.](#bots) La **boîte de dialogue** d’extension de messagerie s’affiche.
1. Sélectionnez **l’onglet Utiliser l’onglet bot** **existant et sélectionnez parmi l’un de mes bots existants**.
1. Sélectionnez le bot que vous avez créé à partir du menu drop-down. Ajoutez un **nom Bot et** sélectionnez Enregistrer **pour** fermer la boîte de dialogue.
1. Sous **la** section Commandez, sélectionnez **Ajouter**. Pour ajouter une commande basée sur la recherche, sélectionnez les **utilisateurs autoriser à interroger votre service pour obtenir des informations et à les insérer dans une** option de message.
1. Dans la **nouvelle boîte de** dialogue de commande, entrez les valeurs suivantes :

    Sous **un nouveau commandement**:

    - **ID de commande**: Entrez le texte aléatoire
    - **Titre**: Entrez le titre aléatoire
    - **Description**: Entrez la description aléatoire

    Sous **Paramètre**:

    - **Nom**: Entrez le nom du paramètre
    - **Titre**: Entrez le titre de la carte
    - **Description**: Entrez la description de la carte

1. Après avoir saisi les informations, sélectionnez **Enregistrer pour** fermer la boîte de dialogue.

#### <a name="register-your-app-in-teams"></a>Enregistrez votre application dans Teams

Après avoir entré les détails de votre application, remplissez les étapes suivantes pour enregistrer votre application dans Teams :

1. Utilisez **Test et distribuez** App Studio pour installer votre application dans Teams. 
1. Mettez à jour votre application hébergée avec l’identifiant de l’application et le mot de passe de votre bot. Pour l’exemple d’application, utilisez le même identifiant d’application et le même mot de passe pour l’extension bot et messagerie. 
1. Sélectionnez **Test et distribuez** **sous Finish** dans le volet gauche d’App Studio :

    <img  width="450px" alt="Testing your app" src="~/assets/images/get-started/Testanddistribute.png"/>

1. Pour télécharger votre application sur Teams, sélectionnez le bouton **Installer** sous **Test et Distribuer**:

    <img  width="450px" alt="Adding a messaging extension dialog" src="~/assets/images/get-started/InstallingHelloWorld.png"/>

1. Sélectionnez la **case** Recherche dans la section **Ajouter à une** équipe et sélectionnez une équipe pour ajouter l’exemple d’application. Vous pouvez mettre en place une équipe spéciale pour les tests.
1. Sélectionnez **le bouton** Installer en bas de la boîte de dialogue.

Votre application est maintenant disponible en Teams. Toutefois, le bot et l’extension de messagerie ne fonctionnera pas tant que vous n’aurez pas mis à jour l’environnement des applications hébergées avec les ID et mots de passe de l’application.

<img  width="450px" alt="The finished app" src="~/assets/images/get-started/Finishedhelloworld.png"/>
