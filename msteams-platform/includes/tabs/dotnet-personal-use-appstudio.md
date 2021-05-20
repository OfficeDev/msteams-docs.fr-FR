## <a name="upload-your-tab-to-teams-with-app-studio"></a><span data-ttu-id="7f3dd-101">Télécharger votre onglet pour Teams avec App Studio</span><span class="sxs-lookup"><span data-stu-id="7f3dd-101">Upload your tab to Teams with App Studio</span></span>

>[!NOTE]
> <span data-ttu-id="7f3dd-102">Nous utilisons App Studio pour modifier vos **manifest.jsdans le** fichier et télécharger le paquet terminé à Teams.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-102">We use App Studio to edit your **manifest.json** file and upload the completed package to Teams.</span></span> <span data-ttu-id="7f3dd-103">Vous pouvez également modifier manuellement **manifest.jssur si** vous préférez.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-103">You can also manually edit **manifest.json** if you prefer.</span></span> <span data-ttu-id="7f3dd-104">Si vous le faites, assurez-vous de construire la solution à nouveau pour **créerTab.zip** fichier à télécharger.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-104">If you do, be sure to build the solution again to create the **Tab.zip** file to upload.</span></span>

- <span data-ttu-id="7f3dd-105">Ouvrez le Microsoft Teams client.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-105">Open the Microsoft Teams client.</span></span> <span data-ttu-id="7f3dd-106">Si vous utilisez la [version Web, vous pouvez](https://teams.microsoft.com) inspecter votre code front-end à l’aide des outils de développement de votre [navigateur](~/tabs/how-to/developer-tools.md).</span><span class="sxs-lookup"><span data-stu-id="7f3dd-106">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>

- <span data-ttu-id="7f3dd-107">Ouvrez le studio App et sélectionnez **l’onglet Éditeur** Manifeste.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-107">Open App studio and select the **Manifest editor** tab.</span></span>

- <span data-ttu-id="7f3dd-108">Sélectionnez **l’importation d’une vignette d’application** existante dans l’éditeur Manifeste pour commencer à mettre à jour le paquet d’application pour votre onglet. Le code source est livré avec son propre manifeste partiellement complet.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-108">Select the **Import an existing app** tile in the Manifest editor to begin updating the app package for your tab. The source code comes with its own partially complete manifest.</span></span> <span data-ttu-id="7f3dd-109">Le nom de votre package d’application **esttab.zip**.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-109">The name of your app package is **tab.zip**.</span></span> <span data-ttu-id="7f3dd-110">Il devrait être trouvé ici:</span><span class="sxs-lookup"><span data-stu-id="7f3dd-110">It should be found here:</span></span>

    ```bash
    /bin/Debug/netcoreapp2.2/Tab.zip
    ```

- <span data-ttu-id="7f3dd-111">Télécharger **Tab.zipà** App Studio.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-111">Upload **Tab.zip** to App Studio.</span></span>

### <a name="update-your-app-package-with-manifest-editor"></a><span data-ttu-id="7f3dd-112">Mettez à jour votre package d’application avec l’éditeur Manifest</span><span class="sxs-lookup"><span data-stu-id="7f3dd-112">Update your app package with Manifest editor</span></span>

<span data-ttu-id="7f3dd-113">Une fois que vous avez téléchargé votre paquet d’applications dans App Studio, vous devrez finir de le configurer.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-113">Once you've uploaded your app package into App Studio, you'll need to finish configuring it.</span></span>

- <span data-ttu-id="7f3dd-114">Sélectionnez la vignette pour votre onglet nouvellement importé dans le panneau droit de la page de bienvenue de l’éditeur Manifeste.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-114">Select the tile for your newly imported tab in the right panel of the Manifest editor welcome page.</span></span>

<span data-ttu-id="7f3dd-115">Il ya une liste d’étapes dans le côté gauche de l’éditeur Manifeste, et sur la droite, une liste de propriétés qui doivent avoir des valeurs pour chacune de ces étapes.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-115">There's a list of steps in the left-hand side of the Manifest editor, and on the right, a list of properties that need to have values for each of those steps.</span></span> <span data-ttu-id="7f3dd-116">Une grande partie de l’information a été *fournie parmanifest.jssur,* mais il ya quelques domaines que vous aurez besoin de mettre à jour:</span><span class="sxs-lookup"><span data-stu-id="7f3dd-116">Much of the information has been provided by your *manifest.json* but there are a few fields that you'll need to update:</span></span>

#### <a name="details-app-details"></a><span data-ttu-id="7f3dd-117">Détails: Détails de l’application</span><span class="sxs-lookup"><span data-stu-id="7f3dd-117">Details: App details</span></span>

<span data-ttu-id="7f3dd-118">Dans la section **Détails de l’application** :</span><span class="sxs-lookup"><span data-stu-id="7f3dd-118">In the **App details** section:</span></span>

- <span data-ttu-id="7f3dd-119">Sous **Identification** **sélectionnez Générer** pour générer un nouvel id d’application pour votre application.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-119">Under **Identification** select **Generate** to generate a new App Id for your app.</span></span>

- <span data-ttu-id="7f3dd-120">Sous les **informations du développeur** mettre à jour **l’URL** du site Web avec votre URL **HTTPS ngrok.**</span><span class="sxs-lookup"><span data-stu-id="7f3dd-120">Under **Developer information** update the **Website URL** with your **ngrok** HTTPS URL.</span></span>

- <span data-ttu-id="7f3dd-121">Sous **les URL d’application mettre à** jour **l’instruction de confidentialité** et les conditions `https://<yourngrokurl>/privacy` **d’utilisation** `https://<yourngrokurl>/tou`>.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-121">Under **App URLs** update the **Privacy statement** to `https://<yourngrokurl>/privacy` and **Terms of use** to `https://<yourngrokurl>/tou`>.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="7f3dd-122">Capacités: Onglets</span><span class="sxs-lookup"><span data-stu-id="7f3dd-122">Capabilities: Tabs</span></span>

<span data-ttu-id="7f3dd-123">Dans la section *Onglets* :</span><span class="sxs-lookup"><span data-stu-id="7f3dd-123">In the *Tabs* section:</span></span>

- <span data-ttu-id="7f3dd-124">Sous **Ajouter un onglet personnel sélectionnez** **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-124">Under **Add a personal tab** select **Add**.</span></span> <span data-ttu-id="7f3dd-125">Vous serez présenté avec une fenêtre de dialogue pop-up.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-125">You will be presented with a pop-up dialogue window.</span></span>

- <span data-ttu-id="7f3dd-126">Complétez le **champ** Nom.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-126">Complete the **Name** field.</span></span>

- <span data-ttu-id="7f3dd-127">Complétez le champ **Id entité.**</span><span class="sxs-lookup"><span data-stu-id="7f3dd-127">Complete the **Entity Id** field.</span></span>

- <span data-ttu-id="7f3dd-128">Mettez à jour **le champ URL** de contenu avec à `https://<yourngrokurl>/personalTab` .</span><span class="sxs-lookup"><span data-stu-id="7f3dd-128">Update the **Content URL** field with to `https://<yourngrokurl>/personalTab`.</span></span>

- <span data-ttu-id="7f3dd-129">Laissez le champ **URL du** site Web vide.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-129">Leave the **Website URL** field blank.</span></span>

- <span data-ttu-id="7f3dd-130">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-130">Select **Save**.</span></span>

#### <a name="finish-domains-and-permissions"></a><span data-ttu-id="7f3dd-131">Finition : Domaines et autorisations</span><span class="sxs-lookup"><span data-stu-id="7f3dd-131">Finish: Domains and permissions</span></span>

<span data-ttu-id="7f3dd-132">Dans la section **Domaines et autorisations,** les **domaines de votre champ onglets** doivent contenir votre URL ngrok sans préfixe HTTPS - `<yourngrokurl>.ngrok.io/` .</span><span class="sxs-lookup"><span data-stu-id="7f3dd-132">In the **Domains and permissions** section, the **Domains from your tabs** field should contain your ngrok URL without the HTTPS prefix - `<yourngrokurl>.ngrok.io/`.</span></span>

##### <a name="finish-test-and-distribute"></a><span data-ttu-id="7f3dd-133">Finition: Test et distribuer</span><span class="sxs-lookup"><span data-stu-id="7f3dd-133">Finish: Test and distribute</span></span>

>[!IMPORTANT]
><span data-ttu-id="7f3dd-134">Dans le **champ Description** à droite, vous verrez l’avertissement suivant :</span><span class="sxs-lookup"><span data-stu-id="7f3dd-134">In the **Description** field on the right you'll see the following warning:</span></span>
>
><span data-ttu-id="7f3dd-135">&#9888; "**Le tableau « validDomains » ne peut pas contenir un site de tunnelage...**»</span><span class="sxs-lookup"><span data-stu-id="7f3dd-135">&#9888; "**The 'validDomains' array cannot contain a tunneling site...**"</span></span>
>
><span data-ttu-id="7f3dd-136">Cet avertissement peut être ignoré lors de l’essai de votre onglet.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-136">This warning can be ignored while testing your tab.</span></span>

<span data-ttu-id="7f3dd-137">Dans la section **Test et distribution** :</span><span class="sxs-lookup"><span data-stu-id="7f3dd-137">In the **Test and distribute** section:</span></span>

- <span data-ttu-id="7f3dd-138">Sélectionnez **Installer**.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-138">Select **Install**.</span></span>

- <span data-ttu-id="7f3dd-139">Dans la fenêtre pop-up assurez-vous que **Ajouter pour vous** est défini sur **Oui** et Ajouter à une équipe **ou chat** est défini à **No**.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-139">In the pop-up window make sure that **Add for you** is set to **Yes** and **Add to a team or chat** is set to **No**.</span></span>

- <span data-ttu-id="7f3dd-140">Sélectionnez **Installer**.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-140">Select **Install**.</span></span>

- <span data-ttu-id="7f3dd-141">Dans la prochaine fenêtre **contexturée, sélectionnez Ouvrir** et votre onglet s’affiche.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-141">In the next pop-up window select **Open** and your tab will be displayed.</span></span>

## <a name="view-your-personal-tab"></a><span data-ttu-id="7f3dd-142">Consultez votre onglet personnel</span><span class="sxs-lookup"><span data-stu-id="7f3dd-142">View your personal tab</span></span>

- <span data-ttu-id="7f3dd-143">Dans la barre de navigation située à l’extrême gauche de l’application Teams, sélectionnez le `...` menu.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-143">In the navigation bar located at the far-left of the Teams App, select the `...` menu.</span></span> <span data-ttu-id="7f3dd-144">Vous serez présenté avec une liste d’applications personnelles.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-144">You'll be presented with a list of personal apps.</span></span>

- <span data-ttu-id="7f3dd-145">Sélectionnez votre onglet dans la liste à afficher.</span><span class="sxs-lookup"><span data-stu-id="7f3dd-145">Select your tab from the list to view.</span></span>
