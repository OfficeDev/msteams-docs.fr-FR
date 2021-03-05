### <a name="use-app-studio-to-update-the-app-package"></a><span data-ttu-id="01e19-101">Utiliser App Studio pour mettre à jour le package d’application</span><span class="sxs-lookup"><span data-stu-id="01e19-101">Use App Studio to update the app package</span></span>

<span data-ttu-id="01e19-102">App Studio est une application Teams que vous pouvez installer à partir du Magasin Teams.</span><span class="sxs-lookup"><span data-stu-id="01e19-102">App Studio is a Teams app that you can install from the Teams store.</span></span> <span data-ttu-id="01e19-103">Cela simplifie la création et l’inscription d’une application.</span><span class="sxs-lookup"><span data-stu-id="01e19-103">It simplifies the creation and registration of an app.</span></span>

<span data-ttu-id="01e19-104">Pour mettre à jour le package d’application, vous suivrez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="01e19-104">Complete the following steps to update the app package:</span></span>

1. <span data-ttu-id="01e19-105">Pour installer App Studio dans Teams, sélectionnez l’icône **Applications** en bas de la barre de gauche, puis recherchez **App Studio.**</span><span class="sxs-lookup"><span data-stu-id="01e19-105">To install App Studio in Teams, select the **Apps** icon at the bottom of the left-hand bar, and search for **App Studio**.</span></span>

<img  width="450px" alt="Finding App Studio in the Store View" src="~/assets/images/get-started/searchforAppStudio.png"/>

2. <span data-ttu-id="01e19-106">Sélectionnez la **vignette App Studio** et choisissez **Installer.**</span><span class="sxs-lookup"><span data-stu-id="01e19-106">Select the **App Studio** tile and choose **Install**.</span></span> <span data-ttu-id="01e19-107">App Studio est installé.</span><span class="sxs-lookup"><span data-stu-id="01e19-107">The App Studio is installed.</span></span>

<img  width="450px" alt="Installing App Studio" src="~/assets/images/get-started/InstallingAppStudio.png"/>

3. <span data-ttu-id="01e19-108">Pour créer le package d’application pour votre application Teams, sélectionnez l’onglet **Éditeur de** manifeste dans **App Studio.**</span><span class="sxs-lookup"><span data-stu-id="01e19-108">To create the app package for your Teams app, select the **Manifest editor** tab in **App Studio**.</span></span>

<img  width="450px" alt="App Studio" src="~/assets/images/get-started/AppStudio.png"/>

<span data-ttu-id="01e19-109">L’exemple est livré avec son propre manifeste et est conçu pour créer un package d’application lorsque le projet est créé.</span><span class="sxs-lookup"><span data-stu-id="01e19-109">The sample comes with its own manifest and is designed to build an app package when the project is built.</span></span> <span data-ttu-id="01e19-110">Sur .NET, cela s’Visual Studio et sur Node.js en tapant sur la ligne de commande dans le répertoire racine `gulp` du projet.</span><span class="sxs-lookup"><span data-stu-id="01e19-110">On .NET this is done in Visual Studio and on Node.js this is done by typing `gulp` at the command line in the root directory of the project.</span></span>

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

<span data-ttu-id="01e19-111">Le nom du package d’application généré est **helloworldapp.zip**.</span><span class="sxs-lookup"><span data-stu-id="01e19-111">The name of the generated app package is **helloworldapp.zip**.</span></span> <span data-ttu-id="01e19-112">Vous pouvez rechercher ce fichier si l’emplacement n’est pas clair dans l’outil que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="01e19-112">You can search for this file if the location is not clear in the tool you are using.</span></span>

4. <span data-ttu-id="01e19-113">Maintenant, pour modifier ce package d’application, **sélectionnez Importer** une application existante dans l’éditeur **de manifeste.**</span><span class="sxs-lookup"><span data-stu-id="01e19-113">Now to modify this app package, select **Import an existing app** in the **Manifest editor**.</span></span>

<img  width="450px" alt="Importing an existing app" src="~/assets/images/get-started/Importinganapp.png"/>

5. <span data-ttu-id="01e19-114">Sélectionnez **la vignette Hello World** pour votre application nouvellement importée.</span><span class="sxs-lookup"><span data-stu-id="01e19-114">Select the **Hello World** tile for your newly imported app.</span></span>

<img  width="450px" alt="Newly imported app view" src="~/assets/images/get-started/HelloWorldappdetails.png"/>

<span data-ttu-id="01e19-115">L’image suivante montre le package d’application importé dans App Studio :</span><span class="sxs-lookup"><span data-stu-id="01e19-115">The following image shows the imported app package in App Studio:</span></span>

<img  width="450px" alt="Importing the app package" src="~/assets/images/get-started/Importinganapp2.png"/>

<span data-ttu-id="01e19-116">Sur le côté gauche de l’éditeur de manifeste se trouve une liste d’étapes.</span><span class="sxs-lookup"><span data-stu-id="01e19-116">On the left-hand side of the Manifest editor there is a list of steps.</span></span> <span data-ttu-id="01e19-117">Sur le côté droit se trouve une liste des propriétés qui doivent être remplies pour chaque étape.</span><span class="sxs-lookup"><span data-stu-id="01e19-117">On the right-hand side there is a list of properties that need to be filled in for each step.</span></span> <span data-ttu-id="01e19-118">Lorsque vous avez commencé avec un exemple d’application, la plupart des informations sont déjà terminées.</span><span class="sxs-lookup"><span data-stu-id="01e19-118">As you started with a sample app, much of the information is already completed.</span></span> <span data-ttu-id="01e19-119">Les étapes suivantes vous permettent de mettre à jour les propriétés de l’application Hello World.</span><span class="sxs-lookup"><span data-stu-id="01e19-119">The next steps enable you to update the properties of the Hello World app.</span></span>

#### <a name="app-details"></a><span data-ttu-id="01e19-120">Détails de l’application</span><span class="sxs-lookup"><span data-stu-id="01e19-120">App details</span></span>

<span data-ttu-id="01e19-121">Sélectionnez **les détails de l’application** **sous Détails.**</span><span class="sxs-lookup"><span data-stu-id="01e19-121">Select **App details** under **Details**.</span></span> <span data-ttu-id="01e19-122">Sélectionnez **le bouton** Générer pour créer un ID d’application.</span><span class="sxs-lookup"><span data-stu-id="01e19-122">Select the **Generate** button to create a new App ID.</span></span>

<span data-ttu-id="01e19-123">Votre nouvel ID d’application est similaire à `2322041b-72bf-459d-b107-f4f335bc35bd` .</span><span class="sxs-lookup"><span data-stu-id="01e19-123">Your new App ID is similar to `2322041b-72bf-459d-b107-f4f335bc35bd`.</span></span>

<span data-ttu-id="01e19-124">Dans le volet droit, vous allez voir  les détails de l’application, y compris les informations sur le développeur et les **détails de** pertinence.</span><span class="sxs-lookup"><span data-stu-id="01e19-124">Go through the app details in the right-hand pane including **Developer information** and **Branding** details.</span></span> <span data-ttu-id="01e19-125">Ces détails sont importants si vous écrivez une nouvelle application pour la distribution.</span><span class="sxs-lookup"><span data-stu-id="01e19-125">These details are important if you are writing a new app for distribution.</span></span>

#### <a name="tabs"></a><span data-ttu-id="01e19-126">Onglets</span><span class="sxs-lookup"><span data-stu-id="01e19-126">Tabs</span></span>

<span data-ttu-id="01e19-127">Il est simple d’ajouter des onglets à une application Teams.</span><span class="sxs-lookup"><span data-stu-id="01e19-127">It is simple to add tabs to a Teams app.</span></span> <span data-ttu-id="01e19-128">L’exemple d’application prend déjà en charge plusieurs onglets et vous pouvez les activer.</span><span class="sxs-lookup"><span data-stu-id="01e19-128">The sample app already supports several tabs, and you can enable them.</span></span>

##### <a name="team-tab"></a><span data-ttu-id="01e19-129">Onglet Équipe</span><span class="sxs-lookup"><span data-stu-id="01e19-129">Team tab</span></span>

<span data-ttu-id="01e19-130">Votre application ne peut avoir qu’un seul onglet d’équipe.</span><span class="sxs-lookup"><span data-stu-id="01e19-130">Your app can only have one Team tab.</span></span>

<img  width="450px" alt="Adding a Teams tab" src="~/assets/images/get-started/TeamTab.png"/>

<span data-ttu-id="01e19-131">Dans cet exemple, l’onglet Équipe est l’endroit où votre page de configuration s’affiche.</span><span class="sxs-lookup"><span data-stu-id="01e19-131">In this sample, the Team tab is where your configuration page is displayed.</span></span> <span data-ttu-id="01e19-132">Sélectionnez **le symbole ...** de l’URL de configuration de l’onglet et choisissez **Modifier** dans le menu déroulant. </span><span class="sxs-lookup"><span data-stu-id="01e19-132">Select the **...** symbol of the **Tab configuration url** and choose **Edit** from the drop-down menu.</span></span> <span data-ttu-id="01e19-133">Remplacez l’URL par l’URL que vous avez utilisée lors de `https://yourteamsapp.ngrok.io/configure` `yourteamsapp.ngrok.io` [l’hébergement de votre application.](#host-the-sample-app)</span><span class="sxs-lookup"><span data-stu-id="01e19-133">Change the URL to `https://yourteamsapp.ngrok.io/configure` where `yourteamsapp.ngrok.io` must be replaced with the URL that you used when [hosting your app](#host-the-sample-app).</span></span>

##### <a name="personal-tabs"></a><span data-ttu-id="01e19-134">Onglets personnels</span><span class="sxs-lookup"><span data-stu-id="01e19-134">Personal tabs</span></span>

<span data-ttu-id="01e19-135">Votre application peut avoir jusqu’à 16 onglets, y compris l’onglet Équipe.</span><span class="sxs-lookup"><span data-stu-id="01e19-135">Your app can have up to 16 tabs, including the Team tab.</span></span>

<span data-ttu-id="01e19-136">Les onglets personnels sont différents de l’onglet Équipe. **L’onglet Hello** est déjà répertorié dans la liste des onglets personnels avec une valeur d’espace `com.contoso.helloworld.hellotab` réservé.</span><span class="sxs-lookup"><span data-stu-id="01e19-136">Personal tabs are different from the Team tab. **Hello Tab** is already listed in the personal tabs list with a placeholder value `com.contoso.helloworld.hellotab`.</span></span> <span data-ttu-id="01e19-137">Sélectionnez **le symbole ...** de l’URL de configuration de l’onglet et choisissez **Modifier** dans le menu déroulant. </span><span class="sxs-lookup"><span data-stu-id="01e19-137">Select the **...** symbol of the **Tab configuration url** and choose **Edit** from the drop-down menu.</span></span> <span data-ttu-id="01e19-138">La boîte de dialogue suivante s’affiche :</span><span class="sxs-lookup"><span data-stu-id="01e19-138">The following dialog box appears:</span></span>

<img  width="450px" alt="Adding a personal tab dialog" src="~/assets/images/get-started/PersonalTab.png"/>

<span data-ttu-id="01e19-139">Mettez à jour les zones suivantes avec l’URL de votre application :</span><span class="sxs-lookup"><span data-stu-id="01e19-139">Update the following boxes with your app URL:</span></span>

- <span data-ttu-id="01e19-140">Modifier la **zone URL** de contenu en `https://yourteamsapp.ngrok.io/hello`</span><span class="sxs-lookup"><span data-stu-id="01e19-140">Change the **Content URL** box to `https://yourteamsapp.ngrok.io/hello`</span></span>
- <span data-ttu-id="01e19-141">Modifier la zone **URL du site** web en `https://yourteamsapp.ngrok.io/hello`</span><span class="sxs-lookup"><span data-stu-id="01e19-141">Change the **Website URL** box to `https://yourteamsapp.ngrok.io/hello`</span></span>

<span data-ttu-id="01e19-142">Remplacez `yourteamsapp.ngrok.io` par l’URL que vous avez utilisée lors de l’hébergement de votre application.</span><span class="sxs-lookup"><span data-stu-id="01e19-142">Replace `yourteamsapp.ngrok.io` by the URL that you used when hosting your app.</span></span>

#### <a name="bots"></a><span data-ttu-id="01e19-143">Bots</span><span class="sxs-lookup"><span data-stu-id="01e19-143">Bots</span></span>

<span data-ttu-id="01e19-144">Il est facile d’ajouter la fonctionnalité bots à votre application.</span><span class="sxs-lookup"><span data-stu-id="01e19-144">It is easy to add the bots functionality to your app.</span></span> <span data-ttu-id="01e19-145">**L’exemple d’application Hello World** possède déjà un bot dans le cadre de l’exemple, mais vous devez l’inscrire auprès de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="01e19-145">The **Hello World** sample app already has a bot as part of the sample, but you must register it with Microsoft.</span></span>

<img  width="450px" alt="Adding a bot" src="~/assets/images/get-started/Bots.png"/>

<span data-ttu-id="01e19-146">Le bot qui a été importé à partir de l’exemple n’a pas d’ID d’application associé.</span><span class="sxs-lookup"><span data-stu-id="01e19-146">The bot that was imported from the sample does not have an associated App ID.</span></span> <span data-ttu-id="01e19-147">Vous devez créer un bot pour qu’App Studio puisse créer un ID d’application et l’inscrire auprès de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="01e19-147">You must create a new bot so that App Studio can create a new App ID and register it with Microsoft.</span></span>

> [!NOTE]
> <span data-ttu-id="01e19-148">L’ID d’application créé par App Studio pour le bot est différent de l’ID d’application créé pour l’application.</span><span class="sxs-lookup"><span data-stu-id="01e19-148">The App ID created by App Studio for the bot is different from the App ID created for the app.</span></span> <span data-ttu-id="01e19-149">Chaque bot d’une application nécessite son propre ID d’application.</span><span class="sxs-lookup"><span data-stu-id="01e19-149">Each bot in an app requires its own App ID.</span></span>

<span data-ttu-id="01e19-150">Pour configurer votre bot, complétez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="01e19-150">Complete the following steps to setup your bot:</span></span>

1. <span data-ttu-id="01e19-151">Sélectionnez **Supprimer** en face du bot importé dans la liste des bots.</span><span class="sxs-lookup"><span data-stu-id="01e19-151">Select **Delete** next to the imported bot in the bot list.</span></span> <span data-ttu-id="01e19-152">Il ne reste plus aucun bot à afficher.</span><span class="sxs-lookup"><span data-stu-id="01e19-152">Now there are no bots left to show.</span></span> 
2. <span data-ttu-id="01e19-153">Sélectionnez **Le programme** d’installation pour afficher la boîte de dialogue Configurer **un bot.**</span><span class="sxs-lookup"><span data-stu-id="01e19-153">Select **Setup** to display the **Set up a bot** dialog box.</span></span>

<img  width="450px" alt="Adding a bot dialog" src="~/assets/images/get-started/Setupbot.png"/>

3. <span data-ttu-id="01e19-154">Ajoutez un nom de bot **Contoso bot** et cochez les trois cases sous **Étendue**.</span><span class="sxs-lookup"><span data-stu-id="01e19-154">Add a bot name **Contoso bot** and select all three check boxes under **Scope**.</span></span>
4. <span data-ttu-id="01e19-155">Sélectionnez **Enregistrer** pour quitter la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="01e19-155">Choose **Save** to exit the dialog box.</span></span> <span data-ttu-id="01e19-156">App Studio enregistre votre bot auprès de Microsoft et affiche votre nouveau bot dans la liste des bots.</span><span class="sxs-lookup"><span data-stu-id="01e19-156">App Studio registers your bot with Microsoft and displays your new bot in the bot list.</span></span> 
5. <span data-ttu-id="01e19-157">À présent, ouvrez un fichier texte dans le bloc-notes et copiez-y votre nouvel ID de bot.</span><span class="sxs-lookup"><span data-stu-id="01e19-157">Now open a text file in notepad and copy and paste your new bot ID into it.</span></span>
6. <span data-ttu-id="01e19-158">Cliquez **sur Générer un nouveau** mot de passe et notez le mot de passe dans le même fichier texte que celui où vous avez noté votre ID d’application de bot.</span><span class="sxs-lookup"><span data-stu-id="01e19-158">Click **Generate New Password**, and note the password in the same text file you noted your bot App ID.</span></span>
7. <span data-ttu-id="01e19-159">Mettez à jour **l’adresse du point** de terminaison du bot et remplacez-la par l’URL que vous avez `https://yourteamsapp.ngrok.io/api/messages` utilisée lors de `yourteamsapp.ngrok.io` l’hébergement de votre application.</span><span class="sxs-lookup"><span data-stu-id="01e19-159">Update the **Bot endpoint address** to `https://yourteamsapp.ngrok.io/api/messages`, and replace `yourteamsapp.ngrok.io` with the URL that you used when hosting your app.</span></span>
8. <span data-ttu-id="01e19-160">Enregistrez maintenant votre fichier texte, car vous devez ajouter les informations du fichier à votre application hébergée pour permettre une communication sécurisée avec votre bot.</span><span class="sxs-lookup"><span data-stu-id="01e19-160">Now save your text file as you must add the information from the file to your hosted app to allow secure communication with your bot.</span></span>

#### <a name="messaging-extensions"></a><span data-ttu-id="01e19-161">Extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="01e19-161">Messaging extensions</span></span>

<span data-ttu-id="01e19-162">Les extensions de messagerie permet aux utilisateurs de demander des informations à votre service et de publier ces informations.</span><span class="sxs-lookup"><span data-stu-id="01e19-162">Messaging extensions let users ask for information from your service and post that information.</span></span> <span data-ttu-id="01e19-163">Les informations sont publiées sous forme de cartes dans la conversation de canal.</span><span class="sxs-lookup"><span data-stu-id="01e19-163">The information is posted in the form of cards into the channel conversation.</span></span> <span data-ttu-id="01e19-164">Les extensions de messagerie apparaissent en bas de la zone de composition.</span><span class="sxs-lookup"><span data-stu-id="01e19-164">Messaging extensions appear at the bottom of the compose box.</span></span>

<span data-ttu-id="01e19-165">Pour configurer votre extension de messagerie, complétez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="01e19-165">Complete the following steps to setup your messaging extension:</span></span>

1. <span data-ttu-id="01e19-166">Sélectionnez **les extensions de messagerie** sous **Fonctionnalités** dans le volet gauche d’App Studio pour configurer l’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="01e19-166">Select **Messaging extensions** under **Capabilities** in the left-hand pane of App Studio to configure the messaging extension.</span></span>

<img  width="450px" alt="Adding a messaging extension" src="~/assets/images/get-started/Messagingextensions.png"/>

<span data-ttu-id="01e19-167">L’exemple d’extension de messagerie est répertorié dans le volet **Extensions** de messagerie.</span><span class="sxs-lookup"><span data-stu-id="01e19-167">The sample messaging extension is listed in the **Messaging Extensions** pane.</span></span>

2. <span data-ttu-id="01e19-168">Sélectionnez **Supprimer** pour supprimer l’extension de messagerie, sélectionnez **Configurer** et suivez les mêmes étapes que pour les [bots.](#bots)</span><span class="sxs-lookup"><span data-stu-id="01e19-168">Select **Delete** to remove the messaging extension, select **Set up**, and follow the same steps used for [bots](#bots).</span></span> <span data-ttu-id="01e19-169">La **boîte de dialogue Extension** de messagerie s’affiche.</span><span class="sxs-lookup"><span data-stu-id="01e19-169">The **Messaging Extension** dialog box is displayed.</span></span>
3. <span data-ttu-id="01e19-170">Sélectionnez **l’onglet Utiliser le bot** existant et **sélectionnez l’un de mes bots existants.**</span><span class="sxs-lookup"><span data-stu-id="01e19-170">Select the **Use existing bot** tab and **Select from one of my existing bots**.</span></span>
4. <span data-ttu-id="01e19-171">Sélectionnez le bot que vous avez créé dans le menu déroulant.</span><span class="sxs-lookup"><span data-stu-id="01e19-171">Select the bot you created from the drop-down menu.</span></span> <span data-ttu-id="01e19-172">Ajoutez un **nom de bot** et **sélectionnez Enregistrer** pour fermer la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="01e19-172">Add a **Bot name** and select **Save** to close the dialog box.</span></span>
5. <span data-ttu-id="01e19-173">Sous la section **Commande,** sélectionnez **Ajouter.**</span><span class="sxs-lookup"><span data-stu-id="01e19-173">Under the **Command** section, select **Add**.</span></span> <span data-ttu-id="01e19-174">Pour ajouter une commande basée sur la recherche, sélectionnez l’option Autoriser les utilisateurs à interroger votre service pour obtenir des informations et insérez-la dans une option **de message.**</span><span class="sxs-lookup"><span data-stu-id="01e19-174">To add a search-based command, select the **Allow users to query your service for information and insert that into a message** option.</span></span>
6. <span data-ttu-id="01e19-175">Dans la **boîte de dialogue Nouvelle commande,** entrez les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="01e19-175">In the **New command** dialog box, enter the following values:</span></span>

<span data-ttu-id="01e19-176">Sous **nouvelle commande**:</span><span class="sxs-lookup"><span data-stu-id="01e19-176">Under **New command**:</span></span>

- <span data-ttu-id="01e19-177">**ID de commande**: entrer du texte aléatoire</span><span class="sxs-lookup"><span data-stu-id="01e19-177">**Command ID**: Enter random text</span></span>
- <span data-ttu-id="01e19-178">**Titre**: entrer un titre aléatoire</span><span class="sxs-lookup"><span data-stu-id="01e19-178">**Title**: Enter random title</span></span>
- <span data-ttu-id="01e19-179">**Description**: entrez une description aléatoire</span><span class="sxs-lookup"><span data-stu-id="01e19-179">**Description**: Enter random description</span></span>

<span data-ttu-id="01e19-180">Sous **paramètre**:</span><span class="sxs-lookup"><span data-stu-id="01e19-180">Under **Parameter**:</span></span>

- <span data-ttu-id="01e19-181">**Name**: Entrez le nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="01e19-181">**Name**: Enter the parameter name</span></span>
- <span data-ttu-id="01e19-182">**Titre**: entrez le titre de la carte</span><span class="sxs-lookup"><span data-stu-id="01e19-182">**Title**: Enter the card title</span></span>
- <span data-ttu-id="01e19-183">**Description**: entrez la description de la carte</span><span class="sxs-lookup"><span data-stu-id="01e19-183">**Description**: Enter card description</span></span>

7. <span data-ttu-id="01e19-184">Après avoir entré les informations, **sélectionnez Enregistrer** pour fermer la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="01e19-184">After you enter the information, select **Save** to close the dialog box.</span></span>

#### <a name="register-your-app-in-teams"></a><span data-ttu-id="01e19-185">Inscrire votre application dans Teams</span><span class="sxs-lookup"><span data-stu-id="01e19-185">Register your app in Teams</span></span>

<span data-ttu-id="01e19-186">Une fois que vous avez entré les détails de votre application, complétez les étapes suivantes pour inscrire votre application dans Teams :</span><span class="sxs-lookup"><span data-stu-id="01e19-186">After entering the details of your app, complete the following steps to register your app in Teams:</span></span>

1. <span data-ttu-id="01e19-187">Utilisez **Test et distribuez** App Studio pour installer votre application dans Teams.</span><span class="sxs-lookup"><span data-stu-id="01e19-187">Use **Test and distribute** of App Studio to install your app in Teams.</span></span> 
2. <span data-ttu-id="01e19-188">Mettez à jour votre application hébergée avec l’ID d’application et le mot de passe de votre bot.</span><span class="sxs-lookup"><span data-stu-id="01e19-188">Update your hosted application with the App ID and password for your bot.</span></span> <span data-ttu-id="01e19-189">Pour l’exemple d’application, utilisez les mêmes ID d’application et mot de passe pour le bot et l’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="01e19-189">For the sample app, use the same App ID and password for both bot and messaging extension.</span></span> 
3. <span data-ttu-id="01e19-190">Sélectionnez **Test et distribuez-le** **sous Terminer** dans le volet gauche d’App Studio.</span><span class="sxs-lookup"><span data-stu-id="01e19-190">Select **Test and distribute**  under **Finish** in the left-hand pane of App Studio.</span></span>

<img  width="450px" alt="Testing your app" src="~/assets/images/get-started/Testanddistribute.png"/>

4. <span data-ttu-id="01e19-191">Pour télécharger votre application dans Teams, sélectionnez le bouton **Installer** sous **Tester et distribuer.**</span><span class="sxs-lookup"><span data-stu-id="01e19-191">To upload your app to Teams, select the **Install** button under **Test and Distribute**.</span></span>

<img  width="450px" alt="Adding a messaging extension dialog" src="~/assets/images/get-started/InstallingHelloWorld.png"/>

5. <span data-ttu-id="01e19-192">Sélectionnez **la zone de** recherche dans la section Ajouter à une équipe et sélectionnez une équipe pour ajouter l’exemple d’application. </span><span class="sxs-lookup"><span data-stu-id="01e19-192">Select the **Search** box in the **Add to a team** section and select a team to add the sample app.</span></span> <span data-ttu-id="01e19-193">Vous pouvez configurer une équipe spéciale pour les tests.</span><span class="sxs-lookup"><span data-stu-id="01e19-193">You can set up a special team for testing.</span></span>
6. <span data-ttu-id="01e19-194">Sélectionnez **le bouton** Installer en bas de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="01e19-194">Select the **Install** button at the bottom of the dialog box.</span></span>

<span data-ttu-id="01e19-195">Votre application est désormais disponible dans Teams.</span><span class="sxs-lookup"><span data-stu-id="01e19-195">Your app is now available in Teams.</span></span> <span data-ttu-id="01e19-196">Toutefois, le bot et l’extension de messagerie ne fonctionneront pas tant que vous n’aurez pas mis à jour l’environnement d’applications hébergée avec les ID d’application et les mots de passe.</span><span class="sxs-lookup"><span data-stu-id="01e19-196">However, the bot and the messaging extension will not work until you update the hosted applications environment with the App IDs and passwords.</span></span>

<img  width="450px" alt="The finished app" src="~/assets/images/get-started/Finishedhelloworld.png"/>
