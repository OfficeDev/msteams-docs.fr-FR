### <a name="use-app-studio-to-update-the-app-package"></a>Utiliser app Studio pour mettre à jour le package d’application

App Studio est une application de teams que vous pouvez installer à partir du Store Teams. Il simplifie la création et l’inscription d’une application.

Pour installer App Studio dans Teams, cliquez sur l’icône App Store en bas de la barre de gauche, puis recherchez App Studio.

<img  width="450px" alt="Finding App Studio in the Store View" src="~/assets/images/get-started/searchforAppStudio.png"/>

Une fois que vous avez trouvé la vignette pour App Studio, cliquez dessus et choisissez *installer* dans la boîte de dialogue qui s’affiche.

<img  width="450px" alt="Installing App Studio" src="~/assets/images/get-started/InstallingAppStudio.png"/>

Une fois que vous avez installé App Studio, cliquez sur l’onglet Éditeur de manifeste pour commencer à créer le package d’application pour votre application Teams.

<img  width="450px" alt="App Studio" src="~/assets/images/get-started/AppStudio.png"/>

L’exemple est fourni avec son propre manifeste prédéfini, et est conçu pour créer un package d’application lors de la création du projet. Sur .NET, cette opération est exécutée dans Visual Studio, ainsi que sur le nœud JS pour cela, en tapant `gulp` à la ligne de commande dans le répertoire racine du projet.

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

Le nom du package d’application généré est *helloworldapp.zip*. Vous pouvez rechercher ce fichier s’il n’est pas clair dans l’outil que vous utilisez.

Dans la partie suivante de cette procédure pas à pas, vous allez modifier ce package d’application en sélectionnant la vignette *Importer une application existante* dans l’éditeur de manifeste.

<img  width="450px" alt="Importing an existing app" src="~/assets/images/get-started/Importinganapp.png"/>

Une fois le package d’application importé, l’application Studio doit ressembler à ce qui suit :

<img  width="450px" alt="Importing the app package" src="~/assets/images/get-started/Importinganapp2.png"/>

Cliquez sur la mosaïque de votre application nouvellement importée, *Hello World*.

<img  width="450px" alt="Newly imported app view" src="~/assets/images/get-started/HelloWorldappdetails.png"/>

Il y a une liste d’étapes dans la partie gauche de l’éditeur de manifeste, et sur la droite une liste de propriétés qui doivent être renseignées pour chacune de ces étapes. Étant donné que vous avez commencé avec un exemple d’application, la plupart des informations sont déjà renseignées. Les étapes suivantes vous permettront de modifier les composants qui doivent encore être mis à jour.

#### <a name="app-details"></a>Détails de l’application

Cliquez sur l’entrée détails de l' *application* sous *Détails*. Cliquez sur le bouton *générer* pour créer un ID d’application.

Votre ID d’application doit ressembler à ceci : `2322041b-72bf-459d-b107-f4f335bc35bd` .

Examinez les autres détails de l’application dans le volet droit, et familiarisez-vous avec certaines entrées, telles que les *informations sur les développeurs* et la *personnalisation*. Ces sections sont importantes si vous écrivez une nouvelle application pour la distribution.

#### <a name="capabilities-tabs"></a>Fonctionnalités : onglets

Les onglets sont parmi les éléments les plus simples à ajouter à une application Teams. L’exemple d’application prend déjà en charge plusieurs onglets, et vous pouvez les activer comme suit.

##### <a name="team-tab"></a>Onglet équipe

Votre application ne peut avoir qu’un seul onglet équipe.

<img  width="450px" alt="Adding a Teams tab" src="~/assets/images/get-started/TeamTab.png"/>

Dans cet exemple, l’onglet équipe est l’endroit où se trouve votre page de configuration. Cliquez sur le symbole *...* à la fin de l’entrée, puis sélectionnez *modifier* dans la liste déroulante. Modifiez l’URL de telle sorte qu' `https://yourteamsapp.ngrok.io/configure` `yourteamsapp.ngrok.io` elle soit remplacée par l’URL que vous avez utilisée ci-dessus lors de l’hébergement de votre application.

##### <a name="personal-tabs"></a>Onglets personnels

Votre application peut comporter jusqu’à 16 onglets, y compris l’onglet équipe.

Les onglets personnels sont représentés différemment à partir de l’onglet équipe. L' *onglet Hello* doit déjà figurer dans la liste des onglets personnels. Au moment où elle a une valeur d’espace réservé `com.contoso.helloworld.hellotab` . Cliquez sur le symbole *...* à la fin de l’entrée, puis sélectionnez *modifier* dans la liste déroulante. La boîte de dialogue suivante s’affiche.

<img  width="450px" alt="Adding a personal tab dialog" src="~/assets/images/get-started/PersonalTab.png"/>

Deux champs doivent être mis à jour avec l’URL de votre application.

- Modifier l’URL de contenu en `https://yourteamsapp.ngrok.io/hello`
- Modifier l’URL du site Web en `https://yourteamsapp.ngrok.io/hello`

Où `yourteamsapp.ngrok.io` doit être remplacé par l’URL que vous avez utilisée ci-dessus lors de l’hébergement de votre application.

#### <a name="bots"></a>Bots

Les robots sont les plus courants pour ajouter des fonctionnalités à votre application. L’exemple Hello World a déjà un bot dans le cadre de l’exemple, mais il n’a pas encore été inscrit auprès de Microsoft.

<img  width="450px" alt="Adding a bot" src="~/assets/images/get-started/Bots.png"/>

Aucun ID d’application n’est associé au robot qui a été importé à partir de l’exemple. Vous devrez créer un nouveau Bot afin que l’application Studio puisse créer un ID d’application et l’inscrire auprès de Microsoft. Notez qu’il s’agit de l’ID d’application pour le bot, qui est différent de l’ID d’application que nous avons créé pour l’application dans une étape précédente. Chaque bot d’une application requiert son propre ID d’application.

Cliquez sur le bouton *Delete (supprimer* ) en regard du *bot importé* dans la liste bot.

À présent, il n’y a aucun bots à afficher. Cliquez sur *configurer*. Cette opération affiche la boîte *de dialogue Configurer un bot* .

<img  width="450px" alt="Adding a bot dialog" src="~/assets/images/get-started/Setupbot.png"/>

Ajoutez un nom de robot `Contoso bot` , puis sélectionnez les trois boutons sous *étendue*.

Sélectionnez *créer un bot* pour quitter la boîte de dialogue. App Studio passera un moment à l’inscription de votre robot auprès de Microsoft, puis affichera votre nouveau robot dans la liste des robots. Maintenant, nous vous conseillons d’ouvrir un fichier texte dans le bloc-notes et de copier et coller votre nouvel ID de robot dans celui-ci. Vous aurez besoin de cet ID ultérieurement.

Cliquez sur *générer un nouveau mot de passe*, puis notez le mot de passe dans le même fichier texte que vous avez noté l’ID de votre application bot dans. Il s’agit de la seule fois que votre mot de passe est affiché, donc n’oubliez pas de le faire maintenant.

Mettez à jour l' *adresse du point de terminaison du bot* vers `https://yourteamsapp.ngrok.io/api/messages` , où `yourteamsapp.ngrok.io` doit être remplacée par l’URL que vous avez utilisée ci-dessus lors de l’hébergement de votre application.

Maintenant, nous vous conseillons d’enregistrer votre fichier texte si vous ne l’avez pas encore fait. Vous ajouterez ces informations à l’application hébergée plus loin dans cette procédure pas à pas, ce qui permettra la communication sécurisée avec votre robot.

#### <a name="messaging-extensions"></a>Extensions de messagerie

Les extensions de messagerie permettent aux utilisateurs de demander des informations à votre service et de publier ces informations, sous la forme de cartes, directement dans la conversation de canal. Les extensions de messagerie apparaissent au bas de la zone de composition.

Cliquez sur *extensions de messagerie* sous *capacités* dans la colonne gauche de l’application Studio pour commencer à configurer l’extension de messagerie.

<img  width="450px" alt="Adding a messaging extension" src="~/assets/images/get-started/Messagingextensions.png"/>

L’exemple d’extension de messagerie est affiché dans le volet de droite sous *extensions de messagerie*. Cliquez à nouveau sur *supprimer* pour supprimer cette entrée, puis cliquez sur le bouton *configurer* en suivant les mêmes étapes que celles suivies pour les robots. Cette opération affiche la boîte de dialogue *extension de messagerie* .

Sélectionnez l’onglet *utiliser un bot existant* , puis *Sélectionnez l’une de mes robots existants*. Dans le menu déroulant, sélectionnez le bot que vous avez créé dans la section ci-dessus. Ajoutez un *nom de bot* et cliquez sur *Enregistrer* pour fermer la boîte de dialogue.

Sous la section *commande* , cliquez sur *Ajouter*. Nous ajoutons une commande basée sur la recherche, donc choisissez l’option *autoriser les utilisateurs à interroger votre service...* .

Dans la boîte de dialogue *nouvelle commande* , entrez les valeurs suivantes.

Sous *nouvelle commande*:

- *ID de commande*  = getRandomText
- *Title*       = obtenir du texte aléatoire pour vous amuser
- *Description* = obtient du texte et des images aléatoires

Sous le *paramètre*:

- *Nom*        = cardTitle
- *Titre*       = titre de la carte
- *Description* = titre de la carte à utiliser

Une fois que vous avez entré les informations, cliquez sur *Enregistrer* pour fermer la boîte de dialogue.

#### <a name="register-your-app-in-teams"></a>Inscrire votre application dans teams

Vous avez maintenant entré les détails de votre application, mais deux étapes subsistent. Tout d’abord, vous devez utiliser la section test et distribution d’App Studio pour installer votre application dans Teams, puis vous devez mettre à jour votre application hébergée avec l’ID d’application et le mot de passe de votre bot. N’oubliez pas que l’exemple prévoit d’utiliser les mêmes ID d’application et mot de passe pour le robot et l’extension de messagerie.

Cliquez sur l’élément de *test et de distribution* sous *Terminer* dans la colonne de gauche de l’application Studio.

<img  width="450px" alt="Testing your app" src="~/assets/images/get-started/Testanddistribute.png"/>

Pour télécharger votre application dans Teams, cliquez sur le bouton *installer* sous *tester et distribuer*.

<img  width="450px" alt="Adding a messaging extension dialog" src="~/assets/images/get-started/InstallingHelloWorld.png"/>

Cliquez sur la zone de *recherche* dans la section *Ajouter à une équipe* et sélectionnez une équipe à laquelle ajouter l’exemple d’application. En règle générale, vous souhaiterez configurer une équipe spéciale à des fins de test.

Cliquez sur le bouton *installer* en bas de la boîte de dialogue.

Cette procédure termine la partie App Studio de cette procédure pas à pas. Vous devez maintenant voir votre application en cours d’exécution dans Teams, mais le robot et l’extension de messagerie ne fonctionnent pas tant que vous n’avez pas mis à jour l’environnement des applications hébergées afin de connaître les ID et les mots de passe d’application.

<img  width="450px" alt="The finished app" src="~/assets/images/get-started/Finishedhelloworld.png"/>
