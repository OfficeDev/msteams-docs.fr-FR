## <a name="upload-your-tab-to-teams-with-app-studio"></a><span data-ttu-id="19d94-101">Télécharger votre onglet pour Teams avec App Studio</span><span class="sxs-lookup"><span data-stu-id="19d94-101">Upload your tab to Teams with App Studio</span></span>

>[!NOTE]
> <span data-ttu-id="19d94-102">Nous utilisons App Studio pour modifier votre **manifest.jsfichier** et charger le package terminé dans Teams.</span><span class="sxs-lookup"><span data-stu-id="19d94-102">We use App Studio to edit your **manifest.json** file and upload the completed package to Teams.</span></span> <span data-ttu-id="19d94-103">Vous pouvez également modifier manuellement **manifest.jssi** vous préférez.</span><span class="sxs-lookup"><span data-stu-id="19d94-103">You can also manually edit **manifest.json** if you prefer.</span></span> <span data-ttu-id="19d94-104">Si vous le faites, n’oubliez pas de générer à nouveau la solution pour créerTab.zip **fichier** à télécharger.</span><span class="sxs-lookup"><span data-stu-id="19d94-104">If you do, be sure to build the solution again to create the **Tab.zip** file to upload.</span></span>

- <span data-ttu-id="19d94-105">Ouvrez le client Microsoft Teams client.</span><span class="sxs-lookup"><span data-stu-id="19d94-105">Open the Microsoft Teams client.</span></span> <span data-ttu-id="19d94-106">Si vous utilisez la [version web,](https://teams.microsoft.com) vous pouvez inspecter votre code frontal à l’aide des outils de développement [de votre navigateur.](~/tabs/how-to/developer-tools.md)</span><span class="sxs-lookup"><span data-stu-id="19d94-106">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>

- <span data-ttu-id="19d94-107">Ouvrez App studio et sélectionnez **l’onglet Éditeur de** manifeste.</span><span class="sxs-lookup"><span data-stu-id="19d94-107">Open App studio and select the **Manifest editor** tab.</span></span>

- <span data-ttu-id="19d94-108">Sélectionnez **la vignette Importer une application** existante dans l’éditeur de manifeste pour commencer à mettre à jour le package d’application pour votre onglet. Le code source est livré avec son propre manifeste partiellement complet.</span><span class="sxs-lookup"><span data-stu-id="19d94-108">Select the **Import an existing app** tile in the Manifest editor to begin updating the app package for your tab. The source code comes with its own partially complete manifest.</span></span> <span data-ttu-id="19d94-109">Le nom de votre package d’application **esttab.zip**.</span><span class="sxs-lookup"><span data-stu-id="19d94-109">The name of your app package is **tab.zip**.</span></span> <span data-ttu-id="19d94-110">Il doit être trouvé ici :</span><span class="sxs-lookup"><span data-stu-id="19d94-110">It should be found here:</span></span>

    ```bash
    /bin/Debug/netcoreapp2.2/Tab.zip
    ```

- <span data-ttu-id="19d94-111">Télécharger **Tab.zip** app Studio.</span><span class="sxs-lookup"><span data-stu-id="19d94-111">Upload **Tab.zip** to App Studio.</span></span>

### <a name="update-your-app-package-with-manifest-editor"></a><span data-ttu-id="19d94-112">Mettre à jour votre package d’application avec l’éditeur de manifeste</span><span class="sxs-lookup"><span data-stu-id="19d94-112">Update your app package with Manifest editor</span></span>

<span data-ttu-id="19d94-113">Une fois que vous avez chargé votre package d’application dans App Studio, vous devez terminer sa configuration.</span><span class="sxs-lookup"><span data-stu-id="19d94-113">Once you've uploaded your app package into App Studio, you'll need to finish configuring it.</span></span>

- <span data-ttu-id="19d94-114">Sélectionnez la vignette de votre onglet nouvellement importé dans le panneau droit de la page d’accueil de l’éditeur de manifeste.</span><span class="sxs-lookup"><span data-stu-id="19d94-114">Select the tile for your newly imported tab in the right panel of the Manifest editor welcome page.</span></span>

<span data-ttu-id="19d94-115">Il existe une liste d’étapes dans le côté gauche de l’éditeur de manifeste, et à droite, une liste des propriétés qui doivent avoir des valeurs pour chacune de ces étapes.</span><span class="sxs-lookup"><span data-stu-id="19d94-115">There's a list of steps in the left-hand side of the Manifest editor, and on the right, a list of properties that need to have values for each of those steps.</span></span> <span data-ttu-id="19d94-116">La plupart des informations ont été fournies par votre *manifest.js,* mais il existe quelques champs que vous devrez mettre à jour :</span><span class="sxs-lookup"><span data-stu-id="19d94-116">Much of the information has been provided by your *manifest.json* but there are a few fields that you'll need to update:</span></span>

#### <a name="details-app-details"></a><span data-ttu-id="19d94-117">Détails : détails de l’application</span><span class="sxs-lookup"><span data-stu-id="19d94-117">Details: App details</span></span>

<span data-ttu-id="19d94-118">Dans la section **Détails de l’application** :</span><span class="sxs-lookup"><span data-stu-id="19d94-118">In the **App details** section:</span></span>

- <span data-ttu-id="19d94-119">Sous **Identification,** **sélectionnez Générer** pour générer un nouvel ID d’application pour votre application.</span><span class="sxs-lookup"><span data-stu-id="19d94-119">Under **Identification** select **Generate** to generate a new App Id for your app.</span></span>

- <span data-ttu-id="19d94-120">Sous **Informations du développeur,** mettez à jour **l’URL du site** web avec votre URL HTTPS **ngrok.**</span><span class="sxs-lookup"><span data-stu-id="19d94-120">Under **Developer information** update the **Website URL** with your **ngrok** HTTPS URL.</span></span>

- <span data-ttu-id="19d94-121">Sous **URL d’application,** mettez à jour la déclaration **de confidentialité** et les conditions `https://<yourngrokurl>/privacy` **d’utilisation** `https://<yourngrokurl>/tou`>.</span><span class="sxs-lookup"><span data-stu-id="19d94-121">Under **App URLs** update the **Privacy statement** to `https://<yourngrokurl>/privacy` and **Terms of use** to `https://<yourngrokurl>/tou`>.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="19d94-122">Fonctionnalités : onglets</span><span class="sxs-lookup"><span data-stu-id="19d94-122">Capabilities: Tabs</span></span>

<span data-ttu-id="19d94-123">Dans la section *Onglets* :</span><span class="sxs-lookup"><span data-stu-id="19d94-123">In the *Tabs* section:</span></span>

- <span data-ttu-id="19d94-124">Sous **Ajouter un onglet personnel, sélectionnez** **Ajouter.**</span><span class="sxs-lookup"><span data-stu-id="19d94-124">Under **Add a personal tab** select **Add**.</span></span> <span data-ttu-id="19d94-125">Une fenêtre de dialogue s’ouvrira.</span><span class="sxs-lookup"><span data-stu-id="19d94-125">You will be presented with a pop-up dialogue window.</span></span>

- <span data-ttu-id="19d94-126">Remplissez le **champ** Nom.</span><span class="sxs-lookup"><span data-stu-id="19d94-126">Complete the **Name** field.</span></span>

- <span data-ttu-id="19d94-127">Terminez **le champ ID de l’entité.**</span><span class="sxs-lookup"><span data-stu-id="19d94-127">Complete the **Entity Id** field.</span></span>

- <span data-ttu-id="19d94-128">Mettez à jour **le champ URL** de contenu avec `https://<yourngrokurl>/personalTab` .</span><span class="sxs-lookup"><span data-stu-id="19d94-128">Update the **Content URL** field with to `https://<yourngrokurl>/personalTab`.</span></span>

- <span data-ttu-id="19d94-129">Laissez le **champ URL** du site web vide.</span><span class="sxs-lookup"><span data-stu-id="19d94-129">Leave the **Website URL** field blank.</span></span>

- <span data-ttu-id="19d94-130">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="19d94-130">Select **Save**.</span></span>

#### <a name="finish-domains-and-permissions"></a><span data-ttu-id="19d94-131">Finish: Domains and permissions</span><span class="sxs-lookup"><span data-stu-id="19d94-131">Finish: Domains and permissions</span></span>

<span data-ttu-id="19d94-132">Dans la section **Domaines et autorisations,** le champ Domaines de vos **onglets** doit contenir votre URL ngrok sans le préfixe HTTPS - `<yourngrokurl>.ngrok.io/` .</span><span class="sxs-lookup"><span data-stu-id="19d94-132">In the **Domains and permissions** section, the **Domains from your tabs** field should contain your ngrok URL without the HTTPS prefix - `<yourngrokurl>.ngrok.io/`.</span></span>

##### <a name="finish-test-and-distribute"></a><span data-ttu-id="19d94-133">Fin : Tester et distribuer</span><span class="sxs-lookup"><span data-stu-id="19d94-133">Finish: Test and distribute</span></span>

>[!IMPORTANT]
><span data-ttu-id="19d94-134">Dans le **champ Description** à droite, vous verrez l’avertissement suivant :</span><span class="sxs-lookup"><span data-stu-id="19d94-134">In the **Description** field on the right you'll see the following warning:</span></span>
>
><span data-ttu-id="19d94-135">&#9888; «**Le tableau « validDomains » ne peut** pas contenir un site de tunneling... »</span><span class="sxs-lookup"><span data-stu-id="19d94-135">&#9888; "**The 'validDomains' array cannot contain a tunneling site...**"</span></span>
>
><span data-ttu-id="19d94-136">Cet avertissement peut être ignoré lors du test de votre onglet.</span><span class="sxs-lookup"><span data-stu-id="19d94-136">This warning can be ignored while testing your tab.</span></span>

<span data-ttu-id="19d94-137">Dans la section **Tester et distribuer** :</span><span class="sxs-lookup"><span data-stu-id="19d94-137">In the **Test and distribute** section:</span></span>

- <span data-ttu-id="19d94-138">Sélectionnez **Installer**.</span><span class="sxs-lookup"><span data-stu-id="19d94-138">Select **Install**.</span></span>

- <span data-ttu-id="19d94-139">Dans la fenêtre pop-up, assurez-vous que La valeur Ajouter pour vous est définie sur **Oui** et que l’ajout à une équipe ou à une **conversation** est définie sur **Non**. </span><span class="sxs-lookup"><span data-stu-id="19d94-139">In the pop-up window make sure that **Add for you** is set to **Yes** and **Add to a team or chat** is set to **No**.</span></span>

- <span data-ttu-id="19d94-140">Sélectionnez **Installer**.</span><span class="sxs-lookup"><span data-stu-id="19d94-140">Select **Install**.</span></span>

- <span data-ttu-id="19d94-141">Dans la fenêtre pop-up suivante, sélectionnez **Ouvrir** et votre onglet s’affiche.</span><span class="sxs-lookup"><span data-stu-id="19d94-141">In the next pop-up window select **Open** and your tab will be displayed.</span></span>

## <a name="view-your-personal-tab"></a><span data-ttu-id="19d94-142">Afficher votre onglet personnel</span><span class="sxs-lookup"><span data-stu-id="19d94-142">View your personal tab</span></span>

- <span data-ttu-id="19d94-143">Dans la barre de navigation située à l’extrême gauche de l’Teams App, sélectionnez le `...` menu.</span><span class="sxs-lookup"><span data-stu-id="19d94-143">In the navigation bar located at the far-left of the Teams App, select the `...` menu.</span></span> <span data-ttu-id="19d94-144">Une liste d’applications personnelles vous sera présentée.</span><span class="sxs-lookup"><span data-stu-id="19d94-144">You'll be presented with a list of personal apps.</span></span>

- <span data-ttu-id="19d94-145">Sélectionnez votre onglet dans la liste à afficher.</span><span class="sxs-lookup"><span data-stu-id="19d94-145">Select your tab from the list to view.</span></span>
