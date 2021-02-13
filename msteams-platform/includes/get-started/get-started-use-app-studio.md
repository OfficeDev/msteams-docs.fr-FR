### <a name="use-app-studio-to-update-the-app-package"></a>Utiliser App Studio pour mettre à jour le package d’application

App Studio est une application Teams que vous pouvez installer à partir du Magasin Teams. Cela simplifie la création et l’inscription d’une application.

Pour installer App Studio dans Teams, sélectionnez l’icône **Applications** en bas de la barre de gauche, puis recherchez **App Studio.**

<img  width="450px" alt="Finding App Studio in the Store View" src="~/assets/images/get-started/searchforAppStudio.png"/>

Sélectionnez la **vignette App Studio** et choisissez **Installer.** App Studio est installé.

<img  width="450px" alt="Installing App Studio" src="~/assets/images/get-started/InstallingAppStudio.png"/>

Sélectionnez **l’onglet Éditeur de** manifeste pour créer le package d’application pour votre application Teams.

<img  width="450px" alt="App Studio" src="~/assets/images/get-started/AppStudio.png"/>

L’exemple est livré avec son propre manifeste pré-créé et est conçu pour créer un package d’application lorsque le projet est créé. Sur .NET, cela est effectué dans Visual Studio, et sur le nœud JS, cela s’fait en tapant sur la ligne de commande dans le répertoire racine `gulp` du projet.

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

Maintenant, pour modifier ce package d’application, sélectionnez la vignette Importer une **application** existante dans l’éditeur **de manifeste.**

<img  width="450px" alt="Importing an existing app" src="~/assets/images/get-started/Importinganapp.png"/>

Cliquez sur **la vignette Hello World** pour votre application nouvellement importée.

<img  width="450px" alt="Newly imported app view" src="~/assets/images/get-started/HelloWorldappdetails.png"/>

L’image suivante montre le package d’application importé dans App Studio :

<img  width="450px" alt="Importing the app package" src="~/assets/images/get-started/Importinganapp2.png"/>

Il existe une liste d’étapes sur le côté gauche de l’éditeur de manifeste et sur le côté droit, une liste des propriétés qui doivent être remplies pour chacune de ces étapes. Depuis que vous avez commencé avec un exemple d’application, une grande partie des informations sont déjà remplies. Les étapes suivantes vous aidera à modifier les composants qui doivent encore être mis à jour.

#### <a name="app-details"></a>Détails de l’application

Cliquez sur *l’entrée Détails de l’application* sous *Détails.* Cliquez sur *le bouton* Générer pour créer un ID d’application.

Votre nouvel ID d’application doit ressembler à : `2322041b-72bf-459d-b107-f4f335bc35bd` .

Regardez le reste des détails de l’application dans le volet droit et  familiarisez-vous avec certaines des entrées telles que les informations de développement et la *pertinence.* Ces sections sont importantes si vous écrivez une nouvelle application pour la distribution.

#### <a name="capabilities-tabs"></a>Fonctionnalités : onglets

Les onglets sont parmi les éléments les plus simples à ajouter à une application Teams. L’exemple d’application prend déjà en charge plusieurs onglets et vous pouvez les activer comme suit.

##### <a name="team-tab"></a>Onglet Équipe

Votre application ne peut avoir qu’un seul onglet d’équipe.

<img  width="450px" alt="Adding a Teams tab" src="~/assets/images/get-started/TeamTab.png"/>

Dans cet exemple, l’onglet Équipe est l’endroit où se trouve votre page de configuration. Cliquez sur le *symbole ...* à la fin de l’entrée et choisissez *Modifier* dans la drop-down. Remplacez l’URL par l’URL que vous avez utilisée ci-dessus lors de `https://yourteamsapp.ngrok.io/configure` `yourteamsapp.ngrok.io` l’hébergement de votre application.

##### <a name="personal-tabs"></a>Onglets personnels

Votre application peut avoir jusqu’à 16 onglets, y compris l’onglet d’équipe.

Les onglets personnels sont représentés différemment de l’onglet d’équipe. L’onglet *Hello doit* déjà être répertorié dans la liste des onglets personnels. Pour le moment, il a une valeur d’espace `com.contoso.helloworld.hellotab` réservé. Cliquez sur le *symbole ...* à la fin de l’entrée et choisissez *Modifier* dans la drop-down. La boîte de dialogue suivante s’affiche.

<img  width="450px" alt="Adding a personal tab dialog" src="~/assets/images/get-started/PersonalTab.png"/>

Vous devez mettre à jour deux champs avec l’URL de votre application.

- Modifier l’URL de contenu en `https://yourteamsapp.ngrok.io/hello`
- Modifier l’URL du site web en `https://yourteamsapp.ngrok.io/hello`

Où `yourteamsapp.ngrok.io` doit être remplacé par l’URL que vous avez utilisée ci-dessus lors de l’hébergement de votre application.

#### <a name="bots"></a>Bots

Les bots sont le moyen le plus courant d’ajouter des fonctionnalités à votre application. L’exemple Hello World possède déjà un bot dans le cadre de l’exemple, mais il n’a pas encore été inscrit auprès de Microsoft.

<img  width="450px" alt="Adding a bot" src="~/assets/images/get-started/Bots.png"/>

Aucun ID d’application n’est encore associé au bot importé à partir de l’exemple. Vous devez créer un bot pour qu’App Studio puisse créer un ID d’application et l’inscrire auprès de Microsoft. Notez qu’il s’agit de l’ID d’application pour le bot, qui est différent de l’ID d’application créé pour l’application. Chaque bot d’une application nécessite son propre ID d’application.

Cliquez sur *le bouton* supprimer en dessous du *bot importé* dans la liste des bots.

Il ne reste plus aucun bot à afficher. Cliquez sur *Installer.* La boîte de dialogue Configurer *un bot* s’affiche.

<img  width="450px" alt="Adding a bot dialog" src="~/assets/images/get-started/Setupbot.png"/>

Ajoutez un nom de bot tel `Contoso bot` que , puis sélectionnez les trois boutons sous **Étendue**.

Choisissez *Créer un bot* pour quitter la boîte de dialogue. App Studio inscrit votre bot auprès de Microsoft et affiche votre nouveau bot dans la liste des bots. Il serait maintenant temps d’ouvrir un fichier texte dans le bloc-notes et de copier et coller votre nouvel ID de bot dans ce fichier. Vous aurez besoin de cet ID ultérieurement.

Cliquez *sur Générer un nouveau* mot de passe, puis notez le mot de passe dans le même fichier texte que celui dans qui vous avez indiqué votre ID d’application bot. C’est la seule fois que votre mot de passe s’affiche, alors assurez-vous de le faire maintenant.

Mettez à *jour l’adresse du point* de terminaison du bot sur , où doit être remplacée par l’URL que vous avez utilisée `https://yourteamsapp.ngrok.io/api/messages` `yourteamsapp.ngrok.io` ci-dessus lors de l’hébergement de votre application.

Si vous ne l’avez pas déjà fait, il serait temps d’enregistrer votre fichier texte. Vous ajouterez ces informations à votre application hébergée plus loin dans cette walkthrough, ce qui permettra une communication sécurisée avec votre bot.

#### <a name="messaging-extensions"></a>Extensions de messagerie

Les extensions de messagerie permet aux utilisateurs de demander des informations à votre service et de publier ces informations, sous forme de cartes, directement dans la conversation de canal. Les extensions de messagerie apparaissent en bas de la zone de composition.

Sélectionnez **les extensions de messagerie** sous **Fonctionnalités** dans la colonne de gauche d’App Studio pour configurer l’extension de messagerie.

<img  width="450px" alt="Adding a messaging extension" src="~/assets/images/get-started/Messagingextensions.png"/>

L’exemple d’extension de messagerie est répertorié dans le volet droit sous **Extensions de messagerie.** Sélectionnez **à** nouveau Supprimer pour supprimer  cette entrée, puis cliquez sur le bouton Configurer en suivant les mêmes étapes que vous avez suivies pour les bots. La boîte de dialogue *Extension de messagerie* s’affiche.

Sélectionnez *l’onglet Utiliser le bot* existant, puis sélectionnez l’un de mes *bots existants.* Dans le menu déroulant, sélectionnez le bot que vous avez créé dans la section ci-dessus. Ajoutez un *nom de bot* et cliquez sur *Enregistrer* pour fermer la boîte de dialogue.

Sous la section *Commande,* cliquez sur *Ajouter.* Nous ajoutons une commande basée sur la recherche, donc choisissez l’option Autoriser les utilisateurs à interroger *votre service...*

Dans la **boîte de dialogue Nouvelle commande,** entrez les valeurs suivantes.

Sous *nouvelle commande*:

- *ID de commande*  = getRandomText
- *Titre*       = Obtenir du texte aléatoire pour le plaisir
- *Description* = Obtient du texte et des images aléatoires

Sous *paramètre*:

- *Name*        = cardTitle
- *Titre*       = Titre de la carte
- *Description* = Titre de carte à utiliser

Une fois que vous avez entré les informations, cliquez sur *Enregistrer* pour fermer la boîte de dialogue.

#### <a name="register-your-app-in-teams"></a>Inscrire votre application dans Teams

Vous avez maintenant terminé d’entrer les détails de votre application, mais les deux étapes suivantes restent :
1. Utilisez la section Tester et distribuer d’App Studio pour installer votre application dans Teams.
1. Mettez à jour votre application hébergée avec l’ID d’application et le mot de passe de votre bot. N’oubliez pas que l’exemple s’attend à utiliser les mêmes ID d’application et mot de passe pour le bot et l’extension de messagerie.

Sélectionnez **l’élément Test et** distribuez-le sous **Terminer** dans la colonne de gauche d’App Studio.

<img  width="450px" alt="Testing your app" src="~/assets/images/get-started/Testanddistribute.png"/>

Pour télécharger votre application dans Teams, cliquez sur le bouton *Installer* sous *Tester et distribuer.*

<img  width="450px" alt="Adding a messaging extension dialog" src="~/assets/images/get-started/InstallingHelloWorld.png"/>

Sélectionnez **la zone de** recherche dans la section Ajouter à une équipe et sélectionnez une équipe à ajouter à l’exemple d’application.  En règle générale, vous pouvez configurer une équipe spéciale pour les tests.

Sélectionnez **le bouton** Installer en bas de la boîte de dialogue.

Cela termine la partie App Studio de cette walkthrough. Votre application doit maintenant s’exécute dans Teams, mais le bot et l’extension de messagerie ne fonctionneront pas tant que vous n’aurez pas mis à jour l’environnement d’applications hébergées pour connaître les ID d’application et les mots de passe.

<img  width="450px" alt="The finished app" src="~/assets/images/get-started/Finishedhelloworld.png"/>
