### <a name="use-app-studio-to-update-the-app-package"></a><span data-ttu-id="47274-101">Utiliser app Studio pour mettre à jour le package d’application</span><span class="sxs-lookup"><span data-stu-id="47274-101">Use App Studio to update the app package</span></span>

<span data-ttu-id="47274-102">App Studio est une application de teams que vous pouvez installer à partir du Store Teams.</span><span class="sxs-lookup"><span data-stu-id="47274-102">App Studio is a Teams app that you can install from the Teams store.</span></span> <span data-ttu-id="47274-103">Il simplifie la création et l’inscription d’une application.</span><span class="sxs-lookup"><span data-stu-id="47274-103">It simplifies the creation and registration of an app.</span></span>

<span data-ttu-id="47274-104">Pour installer App Studio dans Teams, cliquez sur l’icône App Store en bas de la barre de gauche, puis recherchez App Studio.</span><span class="sxs-lookup"><span data-stu-id="47274-104">To install App Studio in Teams, click on the app store icon at the bottom of the left hand bar, and search for App Studio.</span></span>

<img  width="450px" title="Recherche d’App Studio dans le Store" src="~/assets/images/get-started/app-studio-store.png"/>

<span data-ttu-id="47274-106">Une fois que vous avez trouvé la vignette pour App Studio, cliquez dessus et choisissez *installer* dans la boîte de dialogue qui s’affiche.</span><span class="sxs-lookup"><span data-stu-id="47274-106">Once you find the tile for App Studio, click on it and choose *install* in the dialog that pops up.</span></span>

<img  width="450px" title="Installation d’App Studio" src="~/assets/images/get-started/app-studio-install.png"/>

<span data-ttu-id="47274-108">Une fois que vous avez installé App Studio, cliquez sur l’onglet Éditeur de manifeste pour commencer à créer le package d’application pour votre application Teams.</span><span class="sxs-lookup"><span data-stu-id="47274-108">Once App Studio is installed click on the Manifest editor tab to begin creating the app package for your Teams app.</span></span>

<img  width="450px" title="App Studio" src="~/assets/images/get-started/app-studio.png"/>

<span data-ttu-id="47274-110">L’exemple est fourni avec son propre manifeste prédéfini, et est conçu pour créer un package d’application lors de la création du projet.</span><span class="sxs-lookup"><span data-stu-id="47274-110">The sample comes with its own pre-made manifest, and is designed to build an app package when the project is built.</span></span> <span data-ttu-id="47274-111">Sur .NET, cette opération est exécutée dans Visual Studio, ainsi que sur le nœud JS `gulp` pour cela, en tapant à la ligne de commande dans le répertoire racine du projet.</span><span class="sxs-lookup"><span data-stu-id="47274-111">On .NET this is done in Visual Studio, and on Node JS this is done by typing `gulp` at the command line in the root directory of the project.</span></span>

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

<span data-ttu-id="47274-112">Le nom du package d’application généré est *HelloWorldApp. zip*.</span><span class="sxs-lookup"><span data-stu-id="47274-112">The name of the generated app package is *helloworldapp.zip*.</span></span> <span data-ttu-id="47274-113">Vous pouvez rechercher ce fichier s’il n’est pas clair dans l’outil que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="47274-113">You can search for this file if the location is not clear in the tool you are using.</span></span>

<span data-ttu-id="47274-114">Dans la partie suivante de cette procédure pas à pas, vous allez modifier ce package d’application en sélectionnant la vignette *Importer une application existante* dans l’éditeur de manifeste.</span><span class="sxs-lookup"><span data-stu-id="47274-114">In the next part of this walkthrough you are going to modify this app package by selecting the *Import an existing app* tile in the Manifest Editor.</span></span>

<img  width="450px" title="Importation d’une application" src="~/assets/images/get-started/app-studio-import.png"/>

<span data-ttu-id="47274-116">Une fois le package d’application importé, l’application Studio doit ressembler à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="47274-116">Once the app package has been imported App Studio should look like this:</span></span>

<img  width="450px" title="Importation d’une application" src="~/assets/images/get-started/app-studio-imported-app.png"/>

<span data-ttu-id="47274-118">Cliquez sur la mosaïque de votre application nouvellement importée, *Hello World*.</span><span class="sxs-lookup"><span data-stu-id="47274-118">Click on the tile for your newly imported app, *Hello World*.</span></span>

<img  width="450px" title="Importation d’une application" src="~/assets/images/get-started/app-studio-manifest-editor.png"/>

<span data-ttu-id="47274-120">Il y a une liste d’étapes dans la partie gauche de l’éditeur de manifeste, et sur la droite une liste de propriétés qui doivent être renseignées pour chacune de ces étapes.</span><span class="sxs-lookup"><span data-stu-id="47274-120">There is a list of steps in the left-hand side of the Manifest editor, and on the right a list of properties that need to be filled in for each of those steps.</span></span> <span data-ttu-id="47274-121">Étant donné que vous avez commencé avec un exemple d’application, la plupart des informations sont déjà renseignées. Les étapes suivantes vous permettront de modifier les composants qui doivent encore être mis à jour.</span><span class="sxs-lookup"><span data-stu-id="47274-121">Since you started with a sample app, much of the information is already filled out. The next steps will walk you through changing the parts that still need to be updated.</span></span>

#### <a name="app-details"></a><span data-ttu-id="47274-122">Détails de l’application</span><span class="sxs-lookup"><span data-stu-id="47274-122">App details</span></span>

<span data-ttu-id="47274-123">Cliquez sur l’entrée détails de l' *application* sous *Détails*.</span><span class="sxs-lookup"><span data-stu-id="47274-123">Click on the *App details* entry under *Details*.</span></span> <span data-ttu-id="47274-124">Cliquez sur le bouton *générer* pour créer un ID d’application.</span><span class="sxs-lookup"><span data-stu-id="47274-124">Click the *Generate* button to create a new app id.</span></span>

<span data-ttu-id="47274-125">Votre ID d’application doit ressembler à `2322041b-72bf-459d-b107-f4f335bc35bd`ceci :.</span><span class="sxs-lookup"><span data-stu-id="47274-125">Your new app id should look something like: `2322041b-72bf-459d-b107-f4f335bc35bd`.</span></span>

<span data-ttu-id="47274-126">Examinez les autres détails de l’application dans le volet droit, et familiarisez-vous avec certaines entrées, telles que les *informations sur les développeurs* et la *personnalisation*.</span><span class="sxs-lookup"><span data-stu-id="47274-126">Look through the rest of the App details in the right hand pane, and familiarize yourself with some of the entries such as *Developer information* and *Branding*.</span></span> <span data-ttu-id="47274-127">Ces sections sont importantes si vous écrivez une nouvelle application pour la distribution.</span><span class="sxs-lookup"><span data-stu-id="47274-127">These sections are important if you are writing a new app for distribution.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="47274-128">Fonctionnalités : onglets</span><span class="sxs-lookup"><span data-stu-id="47274-128">Capabilities: Tabs</span></span>

<span data-ttu-id="47274-129">Les onglets sont parmi les éléments les plus simples à ajouter à une application Teams.</span><span class="sxs-lookup"><span data-stu-id="47274-129">Tabs are among the simplest elements to add to a Teams app.</span></span> <span data-ttu-id="47274-130">L’exemple d’application prend déjà en charge plusieurs onglets, et vous pouvez les activer comme suit.</span><span class="sxs-lookup"><span data-stu-id="47274-130">The sample app already supports several tabs, and you can enable them as follows.</span></span>

##### <a name="team-tab"></a><span data-ttu-id="47274-131">Onglet équipe</span><span class="sxs-lookup"><span data-stu-id="47274-131">Team tab</span></span>

<span data-ttu-id="47274-132">Votre application ne peut avoir qu’un seul onglet équipe.</span><span class="sxs-lookup"><span data-stu-id="47274-132">Your app can only have one Team tab.</span></span>

<img  width="450px" title="Ajout d’un onglet teams" src="~/assets/images/get-started/app-studio-manifest-editor-tabs.png"/>

<span data-ttu-id="47274-134">Dans cet exemple, l’onglet équipe est l’endroit où se trouve votre page de configuration.</span><span class="sxs-lookup"><span data-stu-id="47274-134">In this sample, the Team tab is where your configuration page goes.</span></span> <span data-ttu-id="47274-135">Cliquez sur le symbole *...* à la fin de l’entrée, puis sélectionnez *modifier* dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="47274-135">Click on the *...* symbol at the end of the entry and choose *Edit* from the drop-down.</span></span> <span data-ttu-id="47274-136">Modifiez l’URL de `https://yourteamsapp.ngrok.io/configure` telle `yourteamsapp.ngrok.io` sorte qu’elle soit remplacée par l’URL que vous avez utilisée ci-dessus lors de l’hébergement de votre application.</span><span class="sxs-lookup"><span data-stu-id="47274-136">Change the URL to `https://yourteamsapp.ngrok.io/configure` where `yourteamsapp.ngrok.io` should be replaced by the URL that you used above when hosting your app.</span></span>

##### <a name="personal-tabs"></a><span data-ttu-id="47274-137">Onglets personnels</span><span class="sxs-lookup"><span data-stu-id="47274-137">Personal tabs</span></span>

<span data-ttu-id="47274-138">Votre application peut comporter jusqu’à 16 onglets, y compris l’onglet équipe.</span><span class="sxs-lookup"><span data-stu-id="47274-138">Your app can have up to 16 tabs, including the team tab.</span></span>

<span data-ttu-id="47274-139">Les onglets personnels sont représentés différemment à partir de l’onglet équipe. L' *onglet Hello* doit déjà figurer dans la liste des onglets personnels.</span><span class="sxs-lookup"><span data-stu-id="47274-139">Personal tabs are represented differently from the team tab. You should see *Hello Tab* already listed in the personal tabs list.</span></span> <span data-ttu-id="47274-140">Au moment où elle a une valeur `com.contoso.helloworld.hellotab`d’espace réservé.</span><span class="sxs-lookup"><span data-stu-id="47274-140">At the moment it has a placeholder value `com.contoso.helloworld.hellotab`.</span></span> <span data-ttu-id="47274-141">Cliquez sur le symbole *...* à la fin de l’entrée, puis sélectionnez *modifier* dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="47274-141">Click on the *...* symbol at the end of the entry and choose *Edit* from the drop-down.</span></span> <span data-ttu-id="47274-142">La boîte de dialogue suivante s’affiche.</span><span class="sxs-lookup"><span data-stu-id="47274-142">The following dialog will appear.</span></span>

<img  width="450px" title="Ajout d’une boîte de dialogue d’onglet personnel" src="~/assets/images/get-started/app-studio-manifest-editor-p-tabs-dialog.png"/>

<span data-ttu-id="47274-144">Deux champs doivent être mis à jour avec l’URL de votre application.</span><span class="sxs-lookup"><span data-stu-id="47274-144">There are two fields that you need to update with your app URL.</span></span>

- <span data-ttu-id="47274-145">Modifier l’URL de contenu en`https://yourteamsapp.ngrok.io/hello`</span><span class="sxs-lookup"><span data-stu-id="47274-145">Change Content URL to `https://yourteamsapp.ngrok.io/hello`</span></span>
- <span data-ttu-id="47274-146">Modifier l’URL du site Web en`https://yourteamsapp.ngrok.io/hello`</span><span class="sxs-lookup"><span data-stu-id="47274-146">Change Website URL to `https://yourteamsapp.ngrok.io/hello`</span></span>

<span data-ttu-id="47274-147">Où `yourteamsapp.ngrok.io` doit être remplacé par l’URL que vous avez utilisée ci-dessus lors de l’hébergement de votre application.</span><span class="sxs-lookup"><span data-stu-id="47274-147">Where `yourteamsapp.ngrok.io` should be replaced by the URL that you used above when hosting your app.</span></span>

#### <a name="bots"></a><span data-ttu-id="47274-148">Bots</span><span class="sxs-lookup"><span data-stu-id="47274-148">Bots</span></span>

<span data-ttu-id="47274-149">Les robots sont les plus courants pour ajouter des fonctionnalités à votre application.</span><span class="sxs-lookup"><span data-stu-id="47274-149">Bots are the most common way to add functionality to your app.</span></span> <span data-ttu-id="47274-150">L’exemple Hello World a déjà un bot dans le cadre de l’exemple, mais il n’a pas encore été inscrit auprès de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="47274-150">The hello world sample already has a bot as part of the sample, but it has not been registered with Microsoft yet.</span></span>

<img  width="450px" title="Ajout d’un bot" src="~/assets/images/get-started/app-studio-manifest-editor-bots.png"/>

<span data-ttu-id="47274-152">Aucun ID d’application n’est associé au robot qui a été importé à partir de l’exemple.</span><span class="sxs-lookup"><span data-stu-id="47274-152">The bot that was imported from the sample does not have an App ID associated with it yet.</span></span> <span data-ttu-id="47274-153">Vous devrez créer un nouveau Bot afin que l’application Studio puisse créer un ID d’application et l’inscrire auprès de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="47274-153">You will have to create a new bot so that App Studio can create a new App ID and register it with Microsoft.</span></span> <span data-ttu-id="47274-154">Notez qu’il s’agit de l’ID d’application pour le bot, qui est différent de l’ID d’application que nous avons créé pour l’application dans une étape précédente.</span><span class="sxs-lookup"><span data-stu-id="47274-154">Note that this is the App ID for the bot, which is different from the App ID that we created for the app in a earlier step.</span></span> <span data-ttu-id="47274-155">Chaque bot d’une application requiert son propre ID d’application.</span><span class="sxs-lookup"><span data-stu-id="47274-155">Each bot in an app requires its own App ID.</span></span>

<span data-ttu-id="47274-156">Cliquez sur le bouton *Delete (supprimer* ) en regard du *bot importé* dans la liste bot.</span><span class="sxs-lookup"><span data-stu-id="47274-156">Click the *delete* button next to the *Imported bot* in the bot list.</span></span>

<span data-ttu-id="47274-157">À présent, il n’y a aucun bots à afficher.</span><span class="sxs-lookup"><span data-stu-id="47274-157">Now there are no bots left to show.</span></span> <span data-ttu-id="47274-158">Cliquez sur *configurer*.</span><span class="sxs-lookup"><span data-stu-id="47274-158">Click *Setup*.</span></span> <span data-ttu-id="47274-159">Cette opération affiche la boîte *de dialogue Configurer un bot* .</span><span class="sxs-lookup"><span data-stu-id="47274-159">This will display the *Set up a bot* dialog.</span></span>

<img  width="450px" title="Ajout d’une boîte de dialogue de robot" src="~/assets/images/get-started/app-studio-manifest-editor-bots-setup-dialog.png"/>

<span data-ttu-id="47274-161">Ajoutez un nom de bot tel `Contoso bot`que, puis cliquez sur les deux boutons sous *étendue*.</span><span class="sxs-lookup"><span data-stu-id="47274-161">Add a bot name such as `Contoso bot`, and click both the buttons under *scope*.</span></span>

<span data-ttu-id="47274-162">Sélectionnez *créer un bot* pour quitter la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="47274-162">Choose *Create bot* to exit the dialog.</span></span> <span data-ttu-id="47274-163">App Studio passera un moment à l’inscription de votre robot auprès de Microsoft, puis affichera votre nouveau robot dans la liste des robots.</span><span class="sxs-lookup"><span data-stu-id="47274-163">App Studio will spend a moment registering your bot with Microsoft, and then should display your new bot in the bot list.</span></span> <span data-ttu-id="47274-164">Maintenant, nous vous conseillons d’ouvrir un fichier texte dans le bloc-notes et de copier et coller votre nouvel ID de robot dans celui-ci.</span><span class="sxs-lookup"><span data-stu-id="47274-164">Now would be a good time to open a text file in notepad and copy and paste your new bot id into it.</span></span> <span data-ttu-id="47274-165">Vous aurez besoin de cet ID ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="47274-165">You will need this id later.</span></span>

<span data-ttu-id="47274-166">Cliquez sur *générer un nouveau mot de passe*, puis notez le mot de passe dans le même fichier texte que vous avez noté l’ID de votre application bot dans.</span><span class="sxs-lookup"><span data-stu-id="47274-166">Click *Generate New Password*, and make a note of the password in the same text file you noted your Bot app ID in.</span></span> <span data-ttu-id="47274-167">Il s’agit de la seule fois que votre mot de passe est affiché, donc n’oubliez pas de le faire maintenant.</span><span class="sxs-lookup"><span data-stu-id="47274-167">This is the only time your password will be shown, so be sure to do this now.</span></span>

<span data-ttu-id="47274-168">Mettez à jour l’adresse du `https://yourteamsapp.ngrok.io/api/messages`point de `yourteamsapp.ngrok.io` *terminaison du bot* vers, où doit être remplacée par l’URL que vous avez utilisée ci-dessus lors de l’hébergement de votre application.</span><span class="sxs-lookup"><span data-stu-id="47274-168">Update the *Bot endpoint address* to `https://yourteamsapp.ngrok.io/api/messages`, where `yourteamsapp.ngrok.io` should be replaced by the URL that you used above when hosting your app.</span></span>

<span data-ttu-id="47274-169">Maintenant, nous vous conseillons d’enregistrer votre fichier texte si vous ne l’avez pas encore fait.</span><span class="sxs-lookup"><span data-stu-id="47274-169">Now would be a good time to save your text file if you have not done so already.</span></span> <span data-ttu-id="47274-170">Vous ajouterez ces informations à l’application hébergée plus loin dans cette procédure pas à pas, ce qui permettra la communication sécurisée avec votre robot.</span><span class="sxs-lookup"><span data-stu-id="47274-170">You will add this information to your hosted app later in this walkthrough, which will allow secure communication with your bot.</span></span>

#### <a name="messaging-extensions"></a><span data-ttu-id="47274-171">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="47274-171">Messaging extensions</span></span>

<span data-ttu-id="47274-172">Les extensions de messagerie permettent aux utilisateurs de demander des informations à votre service et de publier ces informations, sous la forme de cartes, directement dans la conversation de canal.</span><span class="sxs-lookup"><span data-stu-id="47274-172">Messaging extensions let users ask for information from your service and post that information, in the form of cards, right into the channel conversation.</span></span> <span data-ttu-id="47274-173">Les extensions de messagerie apparaissent au bas de la zone de composition.</span><span class="sxs-lookup"><span data-stu-id="47274-173">Messaging extensions appear along the bottom of the compose box.</span></span>

<span data-ttu-id="47274-174">Cliquez sur *extensions de messagerie* sous *capacités* dans la colonne gauche de l’application Studio pour commencer à configurer l’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="47274-174">Click on *Messaging extensions* under *Capabilities* in the left hand column of App Studio to begin configuring the messaging extension.</span></span>

<img  width="450px" title="Ajout d’une extension de messagerie" src="~/assets/images/get-started/app-studio-manifest-editor-mess-ext.png"/>

<span data-ttu-id="47274-176">L’exemple d’extension de messagerie est affiché dans le volet de droite sous *extensions de messagerie*.</span><span class="sxs-lookup"><span data-stu-id="47274-176">The sample messaging extension is listed in the right hand pane under *Messaging Extensions*.</span></span> <span data-ttu-id="47274-177">Cliquez à nouveau sur *supprimer* pour supprimer cette entrée, puis cliquez sur le bouton *configurer* en suivant les mêmes étapes que celles suivies pour les robots.</span><span class="sxs-lookup"><span data-stu-id="47274-177">Click *Delete* again to remove this entry, and then click the *Set up* button following the same steps as you followed for bots.</span></span> <span data-ttu-id="47274-178">Cette opération affiche la boîte de dialogue *extension de messagerie* .</span><span class="sxs-lookup"><span data-stu-id="47274-178">This will display the *Messaging Extension* dialog.</span></span>

<span data-ttu-id="47274-179">Sélectionnez l’onglet *utiliser un bot existant* , puis *Sélectionnez l’une de mes robots existants*.</span><span class="sxs-lookup"><span data-stu-id="47274-179">Select the *Use existing bot* tab, then *Select from one of my existing bots*.</span></span> <span data-ttu-id="47274-180">Dans le menu déroulant, sélectionnez le bot que vous avez créé dans la section ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="47274-180">In the drop-down menu, select the bot you created in the section above.</span></span> <span data-ttu-id="47274-181">Ajoutez un *nom de bot* et cliquez sur *Enregistrer* pour fermer la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="47274-181">Add a *Bot name* and click *Save* to close the dialog.</span></span>

<span data-ttu-id="47274-182">Sous la section *commande* , cliquez sur *Ajouter*.</span><span class="sxs-lookup"><span data-stu-id="47274-182">Under the *Command* section, click *Add*.</span></span> <span data-ttu-id="47274-183">Nous ajoutons une commande basée sur la recherche, donc choisissez l’option *autoriser les utilisateurs à interroger votre service...* .</span><span class="sxs-lookup"><span data-stu-id="47274-183">We're adding a search-based command, so choose the *Allow users to query your service...* option.</span></span>

<span data-ttu-id="47274-184">Dans la boîte de dialogue *nouvelle commande* , entrez les valeurs suivantes.</span><span class="sxs-lookup"><span data-stu-id="47274-184">In the *New command* dialog enter the following values.</span></span>

<span data-ttu-id="47274-185">Sous *nouvelle commande*:</span><span class="sxs-lookup"><span data-stu-id="47274-185">Under *New command*:</span></span>

- <span data-ttu-id="47274-186">*ID de commande* = getRandomText</span><span class="sxs-lookup"><span data-stu-id="47274-186">*Command ID*  = getRandomText</span></span>
- <span data-ttu-id="47274-187">*Title* = obtenir du texte aléatoire pour vous amuser</span><span class="sxs-lookup"><span data-stu-id="47274-187">*Title*       = Get some random text for fun</span></span>
- <span data-ttu-id="47274-188">*Description* = obtient du texte et des images aléatoires</span><span class="sxs-lookup"><span data-stu-id="47274-188">*Description* = Gets some random text and images</span></span>

<span data-ttu-id="47274-189">Sous le *paramètre*:</span><span class="sxs-lookup"><span data-stu-id="47274-189">Under *Parameter*:</span></span>

- <span data-ttu-id="47274-190">*Nom* = cardTitle</span><span class="sxs-lookup"><span data-stu-id="47274-190">*Name*        = cardTitle</span></span>
- <span data-ttu-id="47274-191">*Titre* = titre de la carte</span><span class="sxs-lookup"><span data-stu-id="47274-191">*Title*       = Card title</span></span>
- <span data-ttu-id="47274-192">*Description* = titre de la carte à utiliser</span><span class="sxs-lookup"><span data-stu-id="47274-192">*Description* = Card title to use</span></span>

<span data-ttu-id="47274-193">Une fois que vous avez entré les informations, cliquez sur *Enregistrer* pour fermer la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="47274-193">Once you're entered the information, click *Save* to close the dialog.</span></span>

#### <a name="register-your-app-in-teams"></a><span data-ttu-id="47274-194">Inscrire votre application dans teams</span><span class="sxs-lookup"><span data-stu-id="47274-194">Register your app in Teams</span></span>

<span data-ttu-id="47274-195">Vous avez maintenant entré les détails de votre application, mais deux étapes subsistent.</span><span class="sxs-lookup"><span data-stu-id="47274-195">You have now completed entering the details of your app, but two steps remain.</span></span> <span data-ttu-id="47274-196">Tout d’abord, vous devez utiliser la section test et distribution d’App Studio pour installer votre application dans Teams, puis vous devez mettre à jour votre application hébergée avec l’ID d’application et le mot de passe de votre bot.</span><span class="sxs-lookup"><span data-stu-id="47274-196">First you must use the Test and Distribute section of App Studio to install your app in Teams, and second you must update your hosted application with the App ID and password for your bot.</span></span> <span data-ttu-id="47274-197">N’oubliez pas que l’exemple prévoit d’utiliser les mêmes ID d’application et mot de passe pour le robot et l’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="47274-197">Remember that the sample expects to use the same App ID and password for both the bot and the messaging extension.</span></span>

<span data-ttu-id="47274-198">Cliquez sur l’élément de *test et de distribution* sous *Terminer* dans la colonne de gauche de l’application Studio.</span><span class="sxs-lookup"><span data-stu-id="47274-198">Click on the *Test and distribute* item under *Finish* in the left hand column of App Studio.</span></span>

<img  width="450px" title="Test de votre application" src="~/assets/images/get-started/app-studio-manifest-editor-test.png"/>

<span data-ttu-id="47274-200">Pour télécharger votre application dans Teams, cliquez sur le bouton *installer* sous *tester et distribuer*.</span><span class="sxs-lookup"><span data-stu-id="47274-200">In order to upload your app to Teams, click the *Install* button under *Test and Distribute*.</span></span>

<img  width="450px" title="Ajout d’une boîte de dialogue d’extension de messagerie" src="~/assets/images/get-started/app-studio-manifest-editor-test-dialog.png"/>

<span data-ttu-id="47274-202">Cliquez sur la zone de *recherche* dans la section *Ajouter à une équipe* et sélectionnez une équipe à laquelle ajouter l’exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="47274-202">Click on the *Search* box in the *Add to a team* section and select a team to add the sample app to.</span></span> <span data-ttu-id="47274-203">En règle générale, vous souhaiterez configurer une équipe spéciale à des fins de test.</span><span class="sxs-lookup"><span data-stu-id="47274-203">Usually you will want to set up a special team for testing.</span></span>

<span data-ttu-id="47274-204">Cliquez sur le bouton *installer* en bas de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="47274-204">Click the *Install* button at the bottom of the dialog.</span></span>

<span data-ttu-id="47274-205">Cette procédure termine la partie App Studio de cette procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="47274-205">This finishes the App Studio portion of this walkthrough.</span></span> <span data-ttu-id="47274-206">Vous devez maintenant voir votre application en cours d’exécution dans Teams, mais le robot et l’extension de messagerie ne fonctionnent pas tant que vous n’avez pas mis à jour l’environnement des applications hébergées afin de connaître les ID et les mots de passe d’application.</span><span class="sxs-lookup"><span data-stu-id="47274-206">You should now see your app running in Teams, however the bot and the messaging extension will not work until you update the hosted applications environment to know what the App IDs and passwords are.</span></span>

<img  width="450px" title="Application terminée" src="~/assets/images/get-started/app-studio-finished-app.png"/>