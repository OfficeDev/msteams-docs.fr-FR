## <a name="upload-your-tab-to-teams-with-app-studio"></a><span data-ttu-id="56ed6-101">Télécharger votre onglet vers teams avec App Studio</span><span class="sxs-lookup"><span data-stu-id="56ed6-101">Upload your tab to Teams with App Studio</span></span>

>[!NOTE]
> <span data-ttu-id="56ed6-102">Nous utilisons App Studio pour modifier votre fichier **Manifest. JSON** et télécharger le package terminé vers Teams.</span><span class="sxs-lookup"><span data-stu-id="56ed6-102">We use App Studio to edit your **manifest.json** file and upload the completed package to Teams.</span></span> <span data-ttu-id="56ed6-103">Vous pouvez également modifier manuellement le fichier **Manifest. JSON** si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="56ed6-103">You can also manually edit the **manifest.json** file if you prefer.</span></span> <span data-ttu-id="56ed6-104">Si vous le faites, veillez à créer à nouveau la solution pour créer le fichier **. zip de tabulation** à télécharger.</span><span class="sxs-lookup"><span data-stu-id="56ed6-104">If you do, be sure to build the solution again to create the **tab.zip** file to upload.</span></span>

- <span data-ttu-id="56ed6-105">Ouvrez le client Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="56ed6-105">Open the Microsoft Teams client.</span></span> <span data-ttu-id="56ed6-106">Si vous utilisez la [version basée sur le Web](https://teams.microsoft.com) , vous pouvez inspecter votre code frontal à l’aide des [outils de développement](~/tabs/how-to/developer-tools.md)de votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="56ed6-106">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>

- <span data-ttu-id="56ed6-107">Ouvrez l’application App Studio et sélectionnez l’onglet **éditeur de manifeste** .</span><span class="sxs-lookup"><span data-stu-id="56ed6-107">Open the App Studio app and select the **Manifest editor** tab.</span></span>

- <span data-ttu-id="56ed6-108">Sélectionnez la vignette **Importer une application existante** dans l’éditeur de manifeste pour commencer à mettre à jour le package d’application pour votre onglet. Le code source est fourni avec son propre manifeste partiellement complet.</span><span class="sxs-lookup"><span data-stu-id="56ed6-108">Select the **Import an existing app** tile in the Manifest editor to begin updating the app package for your tab. The source code comes with its own partially complete manifest.</span></span> <span data-ttu-id="56ed6-109">Le nom de votre package d’application est **Tab. zip**.</span><span class="sxs-lookup"><span data-stu-id="56ed6-109">The name of your app package is **tab.zip**.</span></span> <span data-ttu-id="56ed6-110">Il doit se trouver ici :</span><span class="sxs-lookup"><span data-stu-id="56ed6-110">It should be found here:</span></span>

```bash
/bin/Debug/netcoreapp2.2/tab.zip
```

- <span data-ttu-id="56ed6-111">Téléchargez **Tab. zip** dans App Studio.</span><span class="sxs-lookup"><span data-stu-id="56ed6-111">Upload **tab.zip** to App Studio.</span></span>

### <a name="update-your-app-package-with-manifest-editor"></a><span data-ttu-id="56ed6-112">Mettre à jour votre package d’application avec l’éditeur de manifeste</span><span class="sxs-lookup"><span data-stu-id="56ed6-112">Update your app package with Manifest editor</span></span>

<span data-ttu-id="56ed6-113">Une fois que vous avez téléchargé votre package d’application dans App Studio, vous devez terminer de le configurer.</span><span class="sxs-lookup"><span data-stu-id="56ed6-113">Once you've uploaded your app package into App Studio, you'll need to finish configuring it.</span></span>

- <span data-ttu-id="56ed6-114">Sélectionnez la mosaïque de votre onglet nouvellement importé dans le volet droit de la page d’accueil de l’éditeur de manifeste.</span><span class="sxs-lookup"><span data-stu-id="56ed6-114">Select the tile for your newly imported tab in the right panel of the Manifest editor welcome page.</span></span>

<span data-ttu-id="56ed6-115">Il y a une liste d’étapes dans le côté gauche de l’éditeur de manifeste, et à droite, une liste de propriétés qui doivent avoir des valeurs pour chacune de ces étapes.</span><span class="sxs-lookup"><span data-stu-id="56ed6-115">There's a list of steps in the left-hand side of the Manifest editor, and on the right, a list of properties that need to have values for each of those steps.</span></span> <span data-ttu-id="56ed6-116">La plupart des informations ont été fournies par votre *fichier manifest. JSON* , mais il existe quelques champs que vous devrez mettre à jour :</span><span class="sxs-lookup"><span data-stu-id="56ed6-116">Much of the information has been provided by your *manifest.json* but there are a few fields that you'll need to update:</span></span>

#### <a name="details-app-details"></a><span data-ttu-id="56ed6-117">Détails : détails de l’application</span><span class="sxs-lookup"><span data-stu-id="56ed6-117">Details: App details</span></span>

- <span data-ttu-id="56ed6-118">Sous *identification* , sélectionnez **générer** pour générer un nouvel ID d’application pour votre application.</span><span class="sxs-lookup"><span data-stu-id="56ed6-118">Under *Identification* select **Generate** to generate a new App Id for your app.</span></span>

- <span data-ttu-id="56ed6-119">Sous *informations sur le développeur* , mettez à jour le champ **URL du site Web** avec votre URL HTTPS *ngrok* .</span><span class="sxs-lookup"><span data-stu-id="56ed6-119">Under *Developer information* update the **Website URL** field with your *ngrok* HTTPS URL.</span></span>

- <span data-ttu-id="56ed6-120">Sous *URL* de l’application \*\*\*\* `https://<yourngrokurl>/privacy` , mettez à jour la déclaration de confidentialité et les **conditions d’utilisation** pour `https://<yourngrokurl>/tou`>.</span><span class="sxs-lookup"><span data-stu-id="56ed6-120">Under *App URLs* update the **Privacy statement** to `https://<yourngrokurl>/privacy` and **Terms of use** to `https://<yourngrokurl>/tou`>.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="56ed6-121">Fonctionnalités : onglets</span><span class="sxs-lookup"><span data-stu-id="56ed6-121">Capabilities: Tabs</span></span>

<span data-ttu-id="56ed6-122">Dans la section *onglets* :</span><span class="sxs-lookup"><span data-stu-id="56ed6-122">In the *Tabs* section:</span></span>

- <span data-ttu-id="56ed6-123">Sous l' *onglet équipe* , sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="56ed6-123">Under *Team Tab* select **Add**.</span></span>

- <span data-ttu-id="56ed6-124">Dans la fenêtre contextuelle de l’onglet équipe, mettez à jour l' `https://<yourngrokurl>/tab`URL de *configuration* vers.</span><span class="sxs-lookup"><span data-stu-id="56ed6-124">In the Team tab pop-up window update the *Configuration URL* to `https://<yourngrokurl>/tab`.</span></span>

- <span data-ttu-id="56ed6-125">Enfin, assurez-vous que la \*mise à jour de la configuration est possible ? \*Les cases Team et *Group chat* sont cochées, puis sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="56ed6-125">Finally, make sure the *can update configuration? Team*, and *Group chat* boxes are checked and select **Save**.</span></span>

#### <a name="finish-domains-and-permissions"></a><span data-ttu-id="56ed6-126">Terminer : domaines et autorisations</span><span class="sxs-lookup"><span data-stu-id="56ed6-126">Finish: Domains and permissions</span></span>

<span data-ttu-id="56ed6-127">Dans la section *domaines et autorisations* , les *domaines de votre champ d’onglets* doivent contenir votre URL ngrok sans le préfixe `<yourngrokurl>.ngrok.io/`HTTPS-.</span><span class="sxs-lookup"><span data-stu-id="56ed6-127">In the *Domains and permissions* section, the *Domains from your tabs* field should contain your ngrok URL without the HTTPS prefix - `<yourngrokurl>.ngrok.io/`.</span></span>

#### <a name="finish-test-and-distribute"></a><span data-ttu-id="56ed6-128">Terminer : tester et distribuer</span><span class="sxs-lookup"><span data-stu-id="56ed6-128">Finish: Test and distribute</span></span>

>[!IMPORTANT]
><span data-ttu-id="56ed6-129">Dans le champ **Description** à droite, vous verrez l’avertissement suivant :</span><span class="sxs-lookup"><span data-stu-id="56ed6-129">In the **Description** field on the right you'll see the following warning:</span></span>
>
><span data-ttu-id="56ed6-130">&#9888;**le tableau « validDomains » ne peut pas contenir de site de tunneling...**</span><span class="sxs-lookup"><span data-stu-id="56ed6-130">&#9888; "**The 'validDomains' array cannot contain a tunneling site...**"</span></span>
>
><span data-ttu-id="56ed6-131">Cet avertissement peut être ignoré lors du test de votre onglet.</span><span class="sxs-lookup"><span data-stu-id="56ed6-131">This warning can be ignored while testing your tab.</span></span>

<span data-ttu-id="56ed6-132">Dans la section *test et distribution* :</span><span class="sxs-lookup"><span data-stu-id="56ed6-132">In the *Test and distribute* section:</span></span>

- <span data-ttu-id="56ed6-133">Sélectionnez **Installer**.</span><span class="sxs-lookup"><span data-stu-id="56ed6-133">Select **Install**.</span></span>

- <span data-ttu-id="56ed6-134">Dans la fenêtre contextuelle *Ajouter à un champ d’équipe ou de conversation* , entrez votre équipe et sélectionnez **installer**.</span><span class="sxs-lookup"><span data-stu-id="56ed6-134">In the pop-up window's *Add to a team or chat* field enter your team and select **Install**.</span></span>

- <span data-ttu-id="56ed6-135">Dans la fenêtre contextuelle suivante, sélectionnez le canal d’équipe dans lequel vous souhaitez afficher l’onglet, puis sélectionnez **configurer**.</span><span class="sxs-lookup"><span data-stu-id="56ed6-135">In the next pop-up window choose the team channel where you would like the tab displayed and select **Set up**.</span></span>

- <span data-ttu-id="56ed6-136">Dans la fenêtre contextuelle finale, sélectionnez une valeur pour la page d’onglet (icône rouge ou gris) et sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="56ed6-136">In the final pop-up window select a value for the tab page (either a red or gray icon) and select **Save**.</span></span>

<span data-ttu-id="56ed6-137">Pour afficher votre onglet, accédez à l’équipe sur laquelle vous l’avez installé, puis sélectionnez-le dans la barre d’onglets.</span><span class="sxs-lookup"><span data-stu-id="56ed6-137">To view your tab, navigate to the team you installed it on, and select it from the tab bar.</span></span> <span data-ttu-id="56ed6-138">La page que vous avez choisie lors de la configuration doit s’afficher.</span><span class="sxs-lookup"><span data-stu-id="56ed6-138">The page that you chose during configuration should be displayed.</span></span>
