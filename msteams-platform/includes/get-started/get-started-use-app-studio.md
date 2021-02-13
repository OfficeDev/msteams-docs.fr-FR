### <a name="use-app-studio-to-update-the-app-package"></a><span data-ttu-id="8bdac-101">Utiliser App Studio pour mettre à jour le package d’application</span><span class="sxs-lookup"><span data-stu-id="8bdac-101">Use App Studio to update the app package</span></span>

<span data-ttu-id="8bdac-102">App Studio est une application Teams que vous pouvez installer à partir du Magasin Teams.</span><span class="sxs-lookup"><span data-stu-id="8bdac-102">App Studio is a Teams app that you can install from the Teams store.</span></span> <span data-ttu-id="8bdac-103">Cela simplifie la création et l’inscription d’une application.</span><span class="sxs-lookup"><span data-stu-id="8bdac-103">It simplifies the creation and registration of an app.</span></span>

<span data-ttu-id="8bdac-104">Pour installer App Studio dans Teams, sélectionnez l’icône **Applications** en bas de la barre de gauche, puis recherchez **App Studio.**</span><span class="sxs-lookup"><span data-stu-id="8bdac-104">To install App Studio in Teams, select the **Apps** icon at the bottom of the left-hand bar, and search for **App Studio**.</span></span>

<img  width="450px" alt="Finding App Studio in the Store View" src="~/assets/images/get-started/searchforAppStudio.png"/>

<span data-ttu-id="8bdac-105">Sélectionnez la **vignette App Studio** et choisissez **Installer.**</span><span class="sxs-lookup"><span data-stu-id="8bdac-105">Select the **App Studio** tile and choose **Install**.</span></span> <span data-ttu-id="8bdac-106">App Studio est installé.</span><span class="sxs-lookup"><span data-stu-id="8bdac-106">The App Studio is installed.</span></span>

<img  width="450px" alt="Installing App Studio" src="~/assets/images/get-started/InstallingAppStudio.png"/>

<span data-ttu-id="8bdac-107">Sélectionnez **l’onglet Éditeur de** manifeste pour créer le package d’application pour votre application Teams.</span><span class="sxs-lookup"><span data-stu-id="8bdac-107">Select the **Manifest editor** tab to create the app package for your Teams app.</span></span>

<img  width="450px" alt="App Studio" src="~/assets/images/get-started/AppStudio.png"/>

<span data-ttu-id="8bdac-108">L’exemple est livré avec son propre manifeste pré-créé et est conçu pour créer un package d’application lorsque le projet est créé.</span><span class="sxs-lookup"><span data-stu-id="8bdac-108">The sample comes with its own pre-made manifest and is designed to build an app package when the project is built.</span></span> <span data-ttu-id="8bdac-109">Sur .NET, cela est effectué dans Visual Studio, et sur le nœud JS, cela s’fait en tapant sur la ligne de commande dans le répertoire racine `gulp` du projet.</span><span class="sxs-lookup"><span data-stu-id="8bdac-109">On .NET this is done in Visual Studio, and on Node JS this is done by typing `gulp` at the command line in the root directory of the project.</span></span>

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

<span data-ttu-id="8bdac-110">Le nom du package d’application généré est **helloworldapp.zip**.</span><span class="sxs-lookup"><span data-stu-id="8bdac-110">The name of the generated app package is **helloworldapp.zip**.</span></span> <span data-ttu-id="8bdac-111">Vous pouvez rechercher ce fichier si l’emplacement n’est pas clair dans l’outil que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="8bdac-111">You can search for this file if the location is not clear in the tool you are using.</span></span>

<span data-ttu-id="8bdac-112">Maintenant, pour modifier ce package d’application, sélectionnez la vignette Importer une **application** existante dans l’éditeur **de manifeste.**</span><span class="sxs-lookup"><span data-stu-id="8bdac-112">Now to modify this app package, select the **Import an existing app** tile in the **Manifest editor**.</span></span>

<img  width="450px" alt="Importing an existing app" src="~/assets/images/get-started/Importinganapp.png"/>

<span data-ttu-id="8bdac-113">Cliquez sur **la vignette Hello World** pour votre application nouvellement importée.</span><span class="sxs-lookup"><span data-stu-id="8bdac-113">Click the **Hello World** tile for your newly imported app.</span></span>

<img  width="450px" alt="Newly imported app view" src="~/assets/images/get-started/HelloWorldappdetails.png"/>

<span data-ttu-id="8bdac-114">L’image suivante montre le package d’application importé dans App Studio :</span><span class="sxs-lookup"><span data-stu-id="8bdac-114">The following image shows the imported app package in App Studio:</span></span>

<img  width="450px" alt="Importing the app package" src="~/assets/images/get-started/Importinganapp2.png"/>

<span data-ttu-id="8bdac-115">Il existe une liste d’étapes sur le côté gauche de l’éditeur de manifeste et sur le côté droit, une liste des propriétés qui doivent être remplies pour chacune de ces étapes.</span><span class="sxs-lookup"><span data-stu-id="8bdac-115">There is a list of steps on the left-hand side of the Manifest editor and on the right-hand side, a list of properties that need to be filled in for each of those steps.</span></span> <span data-ttu-id="8bdac-116">Depuis que vous avez commencé avec un exemple d’application, une grande partie des informations sont déjà remplies. Les étapes suivantes vous aidera à modifier les composants qui doivent encore être mis à jour.</span><span class="sxs-lookup"><span data-stu-id="8bdac-116">Since you started with a sample app, much of the information is already filled out. The next steps will walk you through changing the parts that still need to be updated.</span></span>

#### <a name="app-details"></a><span data-ttu-id="8bdac-117">Détails de l’application</span><span class="sxs-lookup"><span data-stu-id="8bdac-117">App details</span></span>

<span data-ttu-id="8bdac-118">Cliquez sur *l’entrée Détails de l’application* sous *Détails.*</span><span class="sxs-lookup"><span data-stu-id="8bdac-118">Click on the *App details* entry under *Details*.</span></span> <span data-ttu-id="8bdac-119">Cliquez sur *le bouton* Générer pour créer un ID d’application.</span><span class="sxs-lookup"><span data-stu-id="8bdac-119">Click the *Generate* button to create a new app id.</span></span>

<span data-ttu-id="8bdac-120">Votre nouvel ID d’application doit ressembler à : `2322041b-72bf-459d-b107-f4f335bc35bd` .</span><span class="sxs-lookup"><span data-stu-id="8bdac-120">Your new app id should look something like: `2322041b-72bf-459d-b107-f4f335bc35bd`.</span></span>

<span data-ttu-id="8bdac-121">Regardez le reste des détails de l’application dans le volet droit et  familiarisez-vous avec certaines des entrées telles que les informations de développement et la *pertinence.*</span><span class="sxs-lookup"><span data-stu-id="8bdac-121">Look through the rest of the App details in the right-hand pane, and familiarize yourself with some of the entries such as *Developer information* and *Branding*.</span></span> <span data-ttu-id="8bdac-122">Ces sections sont importantes si vous écrivez une nouvelle application pour la distribution.</span><span class="sxs-lookup"><span data-stu-id="8bdac-122">These sections are important if you are writing a new app for distribution.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="8bdac-123">Fonctionnalités : onglets</span><span class="sxs-lookup"><span data-stu-id="8bdac-123">Capabilities: Tabs</span></span>

<span data-ttu-id="8bdac-124">Les onglets sont parmi les éléments les plus simples à ajouter à une application Teams.</span><span class="sxs-lookup"><span data-stu-id="8bdac-124">Tabs are among the simplest elements to add to a Teams app.</span></span> <span data-ttu-id="8bdac-125">L’exemple d’application prend déjà en charge plusieurs onglets et vous pouvez les activer comme suit.</span><span class="sxs-lookup"><span data-stu-id="8bdac-125">The sample app already supports several tabs, and you can enable them as follows.</span></span>

##### <a name="team-tab"></a><span data-ttu-id="8bdac-126">Onglet Équipe</span><span class="sxs-lookup"><span data-stu-id="8bdac-126">Team tab</span></span>

<span data-ttu-id="8bdac-127">Votre application ne peut avoir qu’un seul onglet d’équipe.</span><span class="sxs-lookup"><span data-stu-id="8bdac-127">Your app can only have one Team tab.</span></span>

<img  width="450px" alt="Adding a Teams tab" src="~/assets/images/get-started/TeamTab.png"/>

<span data-ttu-id="8bdac-128">Dans cet exemple, l’onglet Équipe est l’endroit où se trouve votre page de configuration.</span><span class="sxs-lookup"><span data-stu-id="8bdac-128">In this sample, the Team tab is where your configuration page goes.</span></span> <span data-ttu-id="8bdac-129">Cliquez sur le *symbole ...* à la fin de l’entrée et choisissez *Modifier* dans la drop-down.</span><span class="sxs-lookup"><span data-stu-id="8bdac-129">Click on the *...* symbol at the end of the entry and choose *Edit* from the drop-down.</span></span> <span data-ttu-id="8bdac-130">Remplacez l’URL par l’URL que vous avez utilisée ci-dessus lors de `https://yourteamsapp.ngrok.io/configure` `yourteamsapp.ngrok.io` l’hébergement de votre application.</span><span class="sxs-lookup"><span data-stu-id="8bdac-130">Change the URL to `https://yourteamsapp.ngrok.io/configure` where `yourteamsapp.ngrok.io` should be replaced by the URL that you used above when hosting your app.</span></span>

##### <a name="personal-tabs"></a><span data-ttu-id="8bdac-131">Onglets personnels</span><span class="sxs-lookup"><span data-stu-id="8bdac-131">Personal tabs</span></span>

<span data-ttu-id="8bdac-132">Votre application peut avoir jusqu’à 16 onglets, y compris l’onglet d’équipe.</span><span class="sxs-lookup"><span data-stu-id="8bdac-132">Your app can have up to 16 tabs, including the team tab.</span></span>

<span data-ttu-id="8bdac-133">Les onglets personnels sont représentés différemment de l’onglet d’équipe. L’onglet *Hello doit* déjà être répertorié dans la liste des onglets personnels.</span><span class="sxs-lookup"><span data-stu-id="8bdac-133">Personal tabs are represented differently from the team tab. You should see *Hello Tab* already listed in the personal tabs list.</span></span> <span data-ttu-id="8bdac-134">Pour le moment, il a une valeur d’espace `com.contoso.helloworld.hellotab` réservé.</span><span class="sxs-lookup"><span data-stu-id="8bdac-134">At the moment it has a placeholder value `com.contoso.helloworld.hellotab`.</span></span> <span data-ttu-id="8bdac-135">Cliquez sur le *symbole ...* à la fin de l’entrée et choisissez *Modifier* dans la drop-down.</span><span class="sxs-lookup"><span data-stu-id="8bdac-135">Click on the *...* symbol at the end of the entry and choose *Edit* from the drop-down.</span></span> <span data-ttu-id="8bdac-136">La boîte de dialogue suivante s’affiche.</span><span class="sxs-lookup"><span data-stu-id="8bdac-136">The following dialog will appear.</span></span>

<img  width="450px" alt="Adding a personal tab dialog" src="~/assets/images/get-started/PersonalTab.png"/>

<span data-ttu-id="8bdac-137">Vous devez mettre à jour deux champs avec l’URL de votre application.</span><span class="sxs-lookup"><span data-stu-id="8bdac-137">There are two fields that you need to update with your app URL.</span></span>

- <span data-ttu-id="8bdac-138">Modifier l’URL de contenu en `https://yourteamsapp.ngrok.io/hello`</span><span class="sxs-lookup"><span data-stu-id="8bdac-138">Change Content URL to `https://yourteamsapp.ngrok.io/hello`</span></span>
- <span data-ttu-id="8bdac-139">Modifier l’URL du site web en `https://yourteamsapp.ngrok.io/hello`</span><span class="sxs-lookup"><span data-stu-id="8bdac-139">Change Website URL to `https://yourteamsapp.ngrok.io/hello`</span></span>

<span data-ttu-id="8bdac-140">Où `yourteamsapp.ngrok.io` doit être remplacé par l’URL que vous avez utilisée ci-dessus lors de l’hébergement de votre application.</span><span class="sxs-lookup"><span data-stu-id="8bdac-140">Where `yourteamsapp.ngrok.io` should be replaced by the URL that you used above when hosting your app.</span></span>

#### <a name="bots"></a><span data-ttu-id="8bdac-141">Bots</span><span class="sxs-lookup"><span data-stu-id="8bdac-141">Bots</span></span>

<span data-ttu-id="8bdac-142">Les bots sont le moyen le plus courant d’ajouter des fonctionnalités à votre application.</span><span class="sxs-lookup"><span data-stu-id="8bdac-142">Bots are the most common way to add functionality to your app.</span></span> <span data-ttu-id="8bdac-143">L’exemple Hello World possède déjà un bot dans le cadre de l’exemple, mais il n’a pas encore été inscrit auprès de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8bdac-143">The hello world sample already has a bot as part of the sample, but it has not been registered with Microsoft yet.</span></span>

<img  width="450px" alt="Adding a bot" src="~/assets/images/get-started/Bots.png"/>

<span data-ttu-id="8bdac-144">Aucun ID d’application n’est encore associé au bot importé à partir de l’exemple.</span><span class="sxs-lookup"><span data-stu-id="8bdac-144">The bot that was imported from the sample does not have an App ID associated with it yet.</span></span> <span data-ttu-id="8bdac-145">Vous devez créer un bot pour qu’App Studio puisse créer un ID d’application et l’inscrire auprès de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8bdac-145">You will have to create a new bot so that App Studio can create a new App ID and register it with Microsoft.</span></span> <span data-ttu-id="8bdac-146">Notez qu’il s’agit de l’ID d’application pour le bot, qui est différent de l’ID d’application créé pour l’application.</span><span class="sxs-lookup"><span data-stu-id="8bdac-146">Note that this is the App ID for the bot, which is different from the App ID created for the app.</span></span> <span data-ttu-id="8bdac-147">Chaque bot d’une application nécessite son propre ID d’application.</span><span class="sxs-lookup"><span data-stu-id="8bdac-147">Each bot in an app requires its own App ID.</span></span>

<span data-ttu-id="8bdac-148">Cliquez sur *le bouton* supprimer en dessous du *bot importé* dans la liste des bots.</span><span class="sxs-lookup"><span data-stu-id="8bdac-148">Click the *delete* button next to the *Imported bot* in the bot list.</span></span>

<span data-ttu-id="8bdac-149">Il ne reste plus aucun bot à afficher.</span><span class="sxs-lookup"><span data-stu-id="8bdac-149">Now there are no bots left to show.</span></span> <span data-ttu-id="8bdac-150">Cliquez sur *Installer.*</span><span class="sxs-lookup"><span data-stu-id="8bdac-150">Click *Setup*.</span></span> <span data-ttu-id="8bdac-151">La boîte de dialogue Configurer *un bot* s’affiche.</span><span class="sxs-lookup"><span data-stu-id="8bdac-151">This will display the *Set up a bot* dialog.</span></span>

<img  width="450px" alt="Adding a bot dialog" src="~/assets/images/get-started/Setupbot.png"/>

<span data-ttu-id="8bdac-152">Ajoutez un nom de bot tel `Contoso bot` que , puis sélectionnez les trois boutons sous **Étendue**.</span><span class="sxs-lookup"><span data-stu-id="8bdac-152">Add a bot name such as `Contoso bot`, and select all three buttons under **Scope**.</span></span>

<span data-ttu-id="8bdac-153">Choisissez *Créer un bot* pour quitter la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="8bdac-153">Choose *Create bot* to exit the dialog.</span></span> <span data-ttu-id="8bdac-154">App Studio inscrit votre bot auprès de Microsoft et affiche votre nouveau bot dans la liste des bots.</span><span class="sxs-lookup"><span data-stu-id="8bdac-154">App Studio registers your bot with Microsoft and displays your new bot in the bot list.</span></span> <span data-ttu-id="8bdac-155">Il serait maintenant temps d’ouvrir un fichier texte dans le bloc-notes et de copier et coller votre nouvel ID de bot dans ce fichier.</span><span class="sxs-lookup"><span data-stu-id="8bdac-155">Now would be a good time to open a text file in notepad and copy and paste your new bot id into it.</span></span> <span data-ttu-id="8bdac-156">Vous aurez besoin de cet ID ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="8bdac-156">You will need this id later.</span></span>

<span data-ttu-id="8bdac-157">Cliquez *sur Générer un nouveau* mot de passe, puis notez le mot de passe dans le même fichier texte que celui dans qui vous avez indiqué votre ID d’application bot.</span><span class="sxs-lookup"><span data-stu-id="8bdac-157">Click *Generate New Password*, and make a note of the password in the same text file you noted your Bot app ID in.</span></span> <span data-ttu-id="8bdac-158">C’est la seule fois que votre mot de passe s’affiche, alors assurez-vous de le faire maintenant.</span><span class="sxs-lookup"><span data-stu-id="8bdac-158">This is the only time your password will be shown, so be sure to do this now.</span></span>

<span data-ttu-id="8bdac-159">Mettez à *jour l’adresse du point* de terminaison du bot sur , où doit être remplacée par l’URL que vous avez utilisée `https://yourteamsapp.ngrok.io/api/messages` `yourteamsapp.ngrok.io` ci-dessus lors de l’hébergement de votre application.</span><span class="sxs-lookup"><span data-stu-id="8bdac-159">Update the *Bot endpoint address* to `https://yourteamsapp.ngrok.io/api/messages`, where `yourteamsapp.ngrok.io` should be replaced by the URL that you used above when hosting your app.</span></span>

<span data-ttu-id="8bdac-160">Si vous ne l’avez pas déjà fait, il serait temps d’enregistrer votre fichier texte.</span><span class="sxs-lookup"><span data-stu-id="8bdac-160">Now would be a good time to save your text file if you have not done so already.</span></span> <span data-ttu-id="8bdac-161">Vous ajouterez ces informations à votre application hébergée plus loin dans cette walkthrough, ce qui permettra une communication sécurisée avec votre bot.</span><span class="sxs-lookup"><span data-stu-id="8bdac-161">You will add this information to your hosted app later in this walkthrough, which will allow secure communication with your bot.</span></span>

#### <a name="messaging-extensions"></a><span data-ttu-id="8bdac-162">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="8bdac-162">Messaging extensions</span></span>

<span data-ttu-id="8bdac-163">Les extensions de messagerie permet aux utilisateurs de demander des informations à votre service et de publier ces informations, sous forme de cartes, directement dans la conversation de canal.</span><span class="sxs-lookup"><span data-stu-id="8bdac-163">Messaging extensions let users ask for information from your service and post that information, in the form of cards, right into the channel conversation.</span></span> <span data-ttu-id="8bdac-164">Les extensions de messagerie apparaissent en bas de la zone de composition.</span><span class="sxs-lookup"><span data-stu-id="8bdac-164">Messaging extensions appear along the bottom of the compose box.</span></span>

<span data-ttu-id="8bdac-165">Sélectionnez **les extensions de messagerie** sous **Fonctionnalités** dans la colonne de gauche d’App Studio pour configurer l’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="8bdac-165">Select **Messaging extensions** under **Capabilities** in the left-hand column of App Studio to configure the messaging extension.</span></span>

<img  width="450px" alt="Adding a messaging extension" src="~/assets/images/get-started/Messagingextensions.png"/>

<span data-ttu-id="8bdac-166">L’exemple d’extension de messagerie est répertorié dans le volet droit sous **Extensions de messagerie.**</span><span class="sxs-lookup"><span data-stu-id="8bdac-166">The sample messaging extension is listed in the right-hand pane under **Messaging Extensions**.</span></span> <span data-ttu-id="8bdac-167">Sélectionnez **à** nouveau Supprimer pour supprimer  cette entrée, puis cliquez sur le bouton Configurer en suivant les mêmes étapes que vous avez suivies pour les bots.</span><span class="sxs-lookup"><span data-stu-id="8bdac-167">Select **Delete** again to remove this entry, and then click the *Set up* button following the same steps as you followed for bots.</span></span> <span data-ttu-id="8bdac-168">La boîte de dialogue *Extension de messagerie* s’affiche.</span><span class="sxs-lookup"><span data-stu-id="8bdac-168">This will display the *Messaging Extension* dialog.</span></span>

<span data-ttu-id="8bdac-169">Sélectionnez *l’onglet Utiliser le bot* existant, puis sélectionnez l’un de mes *bots existants.*</span><span class="sxs-lookup"><span data-stu-id="8bdac-169">Select the *Use existing bot* tab, then *Select from one of my existing bots*.</span></span> <span data-ttu-id="8bdac-170">Dans le menu déroulant, sélectionnez le bot que vous avez créé dans la section ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="8bdac-170">In the drop-down menu, select the bot you created in the section above.</span></span> <span data-ttu-id="8bdac-171">Ajoutez un *nom de bot* et cliquez sur *Enregistrer* pour fermer la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="8bdac-171">Add a *Bot name* and click *Save* to close the dialog.</span></span>

<span data-ttu-id="8bdac-172">Sous la section *Commande,* cliquez sur *Ajouter.*</span><span class="sxs-lookup"><span data-stu-id="8bdac-172">Under the *Command* section, click *Add*.</span></span> <span data-ttu-id="8bdac-173">Nous ajoutons une commande basée sur la recherche, donc choisissez l’option Autoriser les utilisateurs à interroger *votre service...*</span><span class="sxs-lookup"><span data-stu-id="8bdac-173">We're adding a search-based command, so choose the *Allow users to query your service...* option.</span></span>

<span data-ttu-id="8bdac-174">Dans la **boîte de dialogue Nouvelle commande,** entrez les valeurs suivantes.</span><span class="sxs-lookup"><span data-stu-id="8bdac-174">In the **New command** dialog, enter the following values.</span></span>

<span data-ttu-id="8bdac-175">Sous *nouvelle commande*:</span><span class="sxs-lookup"><span data-stu-id="8bdac-175">Under *New command*:</span></span>

- <span data-ttu-id="8bdac-176">*ID de commande*  = getRandomText</span><span class="sxs-lookup"><span data-stu-id="8bdac-176">*Command ID*  = getRandomText</span></span>
- <span data-ttu-id="8bdac-177">*Titre*       = Obtenir du texte aléatoire pour le plaisir</span><span class="sxs-lookup"><span data-stu-id="8bdac-177">*Title*       = Get some random text for fun</span></span>
- <span data-ttu-id="8bdac-178">*Description* = Obtient du texte et des images aléatoires</span><span class="sxs-lookup"><span data-stu-id="8bdac-178">*Description* = Gets some random text and images</span></span>

<span data-ttu-id="8bdac-179">Sous *paramètre*:</span><span class="sxs-lookup"><span data-stu-id="8bdac-179">Under *Parameter*:</span></span>

- <span data-ttu-id="8bdac-180">*Name*        = cardTitle</span><span class="sxs-lookup"><span data-stu-id="8bdac-180">*Name*        = cardTitle</span></span>
- <span data-ttu-id="8bdac-181">*Titre*       = Titre de la carte</span><span class="sxs-lookup"><span data-stu-id="8bdac-181">*Title*       = Card title</span></span>
- <span data-ttu-id="8bdac-182">*Description* = Titre de carte à utiliser</span><span class="sxs-lookup"><span data-stu-id="8bdac-182">*Description* = Card title to use</span></span>

<span data-ttu-id="8bdac-183">Une fois que vous avez entré les informations, cliquez sur *Enregistrer* pour fermer la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="8bdac-183">Once you're entered the information, click *Save* to close the dialog.</span></span>

#### <a name="register-your-app-in-teams"></a><span data-ttu-id="8bdac-184">Inscrire votre application dans Teams</span><span class="sxs-lookup"><span data-stu-id="8bdac-184">Register your app in Teams</span></span>

<span data-ttu-id="8bdac-185">Vous avez maintenant terminé d’entrer les détails de votre application, mais les deux étapes suivantes restent :</span><span class="sxs-lookup"><span data-stu-id="8bdac-185">You have now completed entering the details of your app, but the following two steps remain:</span></span>
1. <span data-ttu-id="8bdac-186">Utilisez la section Tester et distribuer d’App Studio pour installer votre application dans Teams.</span><span class="sxs-lookup"><span data-stu-id="8bdac-186">Use the Test and Distribute section of App Studio to install your app in Teams.</span></span>
1. <span data-ttu-id="8bdac-187">Mettez à jour votre application hébergée avec l’ID d’application et le mot de passe de votre bot.</span><span class="sxs-lookup"><span data-stu-id="8bdac-187">Update your hosted application with the App ID and password for your bot.</span></span> <span data-ttu-id="8bdac-188">N’oubliez pas que l’exemple s’attend à utiliser les mêmes ID d’application et mot de passe pour le bot et l’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="8bdac-188">Remember that the sample expects to use the same App ID and password for both the bot and the messaging extension.</span></span>

<span data-ttu-id="8bdac-189">Sélectionnez **l’élément Test et** distribuez-le sous **Terminer** dans la colonne de gauche d’App Studio.</span><span class="sxs-lookup"><span data-stu-id="8bdac-189">Select the **Test and distribute** item under **Finish** in the left-hand column of App Studio.</span></span>

<img  width="450px" alt="Testing your app" src="~/assets/images/get-started/Testanddistribute.png"/>

<span data-ttu-id="8bdac-190">Pour télécharger votre application dans Teams, cliquez sur le bouton *Installer* sous *Tester et distribuer.*</span><span class="sxs-lookup"><span data-stu-id="8bdac-190">In order to upload your app to Teams, click the *Install* button under *Test and Distribute*.</span></span>

<img  width="450px" alt="Adding a messaging extension dialog" src="~/assets/images/get-started/InstallingHelloWorld.png"/>

<span data-ttu-id="8bdac-191">Sélectionnez **la zone de** recherche dans la section Ajouter à une équipe et sélectionnez une équipe à ajouter à l’exemple d’application. </span><span class="sxs-lookup"><span data-stu-id="8bdac-191">Select the **Search** box in the **Add to a team** section and select a team to add the sample app to.</span></span> <span data-ttu-id="8bdac-192">En règle générale, vous pouvez configurer une équipe spéciale pour les tests.</span><span class="sxs-lookup"><span data-stu-id="8bdac-192">Usually, you can set up a special team for testing.</span></span>

<span data-ttu-id="8bdac-193">Sélectionnez **le bouton** Installer en bas de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="8bdac-193">Select the **Install** button at the bottom of the dialog.</span></span>

<span data-ttu-id="8bdac-194">Cela termine la partie App Studio de cette walkthrough.</span><span class="sxs-lookup"><span data-stu-id="8bdac-194">This finishes the App Studio portion of this walkthrough.</span></span> <span data-ttu-id="8bdac-195">Votre application doit maintenant s’exécute dans Teams, mais le bot et l’extension de messagerie ne fonctionneront pas tant que vous n’aurez pas mis à jour l’environnement d’applications hébergées pour connaître les ID d’application et les mots de passe.</span><span class="sxs-lookup"><span data-stu-id="8bdac-195">You should now see your app running in Teams, however, the bot and the messaging extension will not work until you update the hosted applications environment to know what the App IDs and passwords are.</span></span>

<img  width="450px" alt="The finished app" src="~/assets/images/get-started/Finishedhelloworld.png"/>
