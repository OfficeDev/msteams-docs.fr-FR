## <a name="upload-your-tab-with-app-studio"></a><span data-ttu-id="ca225-101">Télécharger onglet avec App Studio</span><span class="sxs-lookup"><span data-stu-id="ca225-101">Upload your tab with App Studio</span></span>

>[!NOTE]
> <span data-ttu-id="ca225-102">Nous utilisons **App Studio** pour modifier votre **manifest.jsfichier** et charger le package terminé dans Teams.</span><span class="sxs-lookup"><span data-stu-id="ca225-102">We use **App Studio** to edit your **manifest.json** file and upload the completed package to Teams.</span></span> <span data-ttu-id="ca225-103">Vous pouvez également modifier manuellement **manifest.jssur**.</span><span class="sxs-lookup"><span data-stu-id="ca225-103">You can also manually edit **manifest.json**.</span></span> <span data-ttu-id="ca225-104">Si vous le faites, veillez à générer à nouveau la solution pour créerTab.zip **fichier** à télécharger.</span><span class="sxs-lookup"><span data-stu-id="ca225-104">If you do, ensure that you build the solution again to create the **Tab.zip** file to upload.</span></span>

<span data-ttu-id="ca225-105">**Pour télécharger votre onglet avec App Studio**</span><span class="sxs-lookup"><span data-stu-id="ca225-105">**To upload your tab with App Studio**</span></span>

1. <span data-ttu-id="ca225-106">Go to Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="ca225-106">Go to Microsoft Teams.</span></span> <span data-ttu-id="ca225-107">Si vous utilisez la [version web,](https://teams.microsoft.com) vous pouvez inspecter votre code frontal à l’aide des outils de développement [de votre navigateur.](~/tabs/how-to/developer-tools.md)</span><span class="sxs-lookup"><span data-stu-id="ca225-107">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>

1. <span data-ttu-id="ca225-108">Go to **App Studio** and select the **Manifest editor** tab.</span><span class="sxs-lookup"><span data-stu-id="ca225-108">Go to **App Studio** and select the **Manifest editor** tab.</span></span>

1. <span data-ttu-id="ca225-109">Sélectionnez **Importer une application existante dans** l’éditeur de manifeste pour commencer à mettre à jour le package d’application pour votre onglet.  Le code source est livré avec son propre manifeste partiellement complet.</span><span class="sxs-lookup"><span data-stu-id="ca225-109">Select **Import an existing app** in the **Manifest editor** to begin updating the app package for your tab. The source code comes with its own partially complete manifest.</span></span> <span data-ttu-id="ca225-110">Le nom de votre package d’application **esttab.zip**.</span><span class="sxs-lookup"><span data-stu-id="ca225-110">The name of your app package is **tab.zip**.</span></span> <span data-ttu-id="ca225-111">Il est disponible à partir du chemin d’accès suivant :</span><span class="sxs-lookup"><span data-stu-id="ca225-111">It is available from the following path:</span></span>

    ```bash
    /bin/Debug/netcoreapp2.2/tab.zip
    ```

1. <span data-ttu-id="ca225-112">Télécharger **tab.zip** **app Studio.**</span><span class="sxs-lookup"><span data-stu-id="ca225-112">Upload **tab.zip** to **App Studio**.</span></span>

### <a name="update-your-app-package-with-manifest-editor"></a><span data-ttu-id="ca225-113">Mettre à jour votre package d’application avec l’éditeur de manifeste</span><span class="sxs-lookup"><span data-stu-id="ca225-113">Update your app package with Manifest editor</span></span>

<span data-ttu-id="ca225-114">Après avoir chargé votre package d’application dans App Studio, vous devez le configurer.</span><span class="sxs-lookup"><span data-stu-id="ca225-114">After you have uploaded your app package into App Studio, you must configure it.</span></span>

<span data-ttu-id="ca225-115">Sélectionnez la vignette de votre onglet nouvellement importé dans le panneau droit de la page d’accueil de l’éditeur de manifeste.</span><span class="sxs-lookup"><span data-stu-id="ca225-115">Select the tile for your newly imported tab in the right panel of the Manifest editor welcome page.</span></span>

<span data-ttu-id="ca225-116">Il existe une liste d’étapes dans le côté gauche de l’éditeur de manifeste, et à droite, une liste de propriétés qui doivent avoir des valeurs pour chacune de ces étapes.</span><span class="sxs-lookup"><span data-stu-id="ca225-116">There is a list of steps in the left-hand side of the Manifest editor, and on the right, a list of properties that must have values for each of those steps.</span></span> <span data-ttu-id="ca225-117">La plupart des informations ont été fournies par votre **manifest.js,** mais vous devez mettre à jour certains champs.</span><span class="sxs-lookup"><span data-stu-id="ca225-117">Much of the information has been provided by your **manifest.json** but there are fields that you must update.</span></span>

#### <a name="details-app-details"></a><span data-ttu-id="ca225-118">Détails : détails de l’application</span><span class="sxs-lookup"><span data-stu-id="ca225-118">Details: App details</span></span>

<span data-ttu-id="ca225-119">Dans la section **Détails de l’application** :</span><span class="sxs-lookup"><span data-stu-id="ca225-119">In the **App details** section:</span></span>

1. <span data-ttu-id="ca225-120">Sous **Identification,** **sélectionnez Générer** pour générer un nouvel ID d’application pour votre application.</span><span class="sxs-lookup"><span data-stu-id="ca225-120">Under **Identification**, select **Generate** to generate a new App Id for your app.</span></span>

1. <span data-ttu-id="ca225-121">Sous **Informations sur le développeur,** mettez à jour le site **web** avec votre URL HTTPS **ngrok.**</span><span class="sxs-lookup"><span data-stu-id="ca225-121">Under **Developer information**, update the **Website** with your **ngrok** HTTPS URL.</span></span>

1. <span data-ttu-id="ca225-122">Sous **URL d’application,** mettez à jour la déclaration **de confidentialité** et les conditions `https://<yourngrokurl>/privacy` **d’utilisation** `https://<yourngrokurl>/tou`>.</span><span class="sxs-lookup"><span data-stu-id="ca225-122">Under **App URLs**, update the **Privacy statement** to `https://<yourngrokurl>/privacy` and **Terms of use** to `https://<yourngrokurl>/tou`>.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="ca225-123">Fonctionnalités : onglets</span><span class="sxs-lookup"><span data-stu-id="ca225-123">Capabilities: Tabs</span></span>

<span data-ttu-id="ca225-124">Dans la section **Onglets** :</span><span class="sxs-lookup"><span data-stu-id="ca225-124">In the **Tabs** section:</span></span>

1. <span data-ttu-id="ca225-125">Sous **Ajouter un onglet personnel,** sélectionnez **Ajouter.**</span><span class="sxs-lookup"><span data-stu-id="ca225-125">Under **Add a personal tab**, select **Add**.</span></span> <span data-ttu-id="ca225-126">Une boîte de dialogue s’affiche.</span><span class="sxs-lookup"><span data-stu-id="ca225-126">A pop-up dialog box appears.</span></span>

1. <span data-ttu-id="ca225-127">Entrez un nom pour l’onglet personnel dans **Nom**.</span><span class="sxs-lookup"><span data-stu-id="ca225-127">Enter a name for the personal tab in **Name**.</span></span>

1. <span data-ttu-id="ca225-128">Entrez **l’ID d’entité**.</span><span class="sxs-lookup"><span data-stu-id="ca225-128">Enter the **Entity ID**.</span></span>

1. <span data-ttu-id="ca225-129">Mettre à **jour l’URL de** contenu avec `https://<yourngrokurl>/personalTab` .</span><span class="sxs-lookup"><span data-stu-id="ca225-129">Update **Content URL** with `https://<yourngrokurl>/personalTab`.</span></span>

    <span data-ttu-id="ca225-130">Laissez le **champ URL** du site web vide.</span><span class="sxs-lookup"><span data-stu-id="ca225-130">Leave the **Website URL** field blank.</span></span>

1. <span data-ttu-id="ca225-131">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="ca225-131">Select **Save**.</span></span>

#### <a name="finish-domains-and-permissions"></a><span data-ttu-id="ca225-132">Finish: Domains and permissions</span><span class="sxs-lookup"><span data-stu-id="ca225-132">Finish: Domains and permissions</span></span>

<span data-ttu-id="ca225-133">Dans la section **Domaines et autorisations,** le champ Domaines de vos **onglets** doit contenir votre URL ngrok sans le préfixe HTTPS. `<yourngrokurl>.ngrok.io/`</span><span class="sxs-lookup"><span data-stu-id="ca225-133">In the **Domains and permissions** section, the **Domains from your tabs** field must contain your ngrok URL without the HTTPS prefix `<yourngrokurl>.ngrok.io/`.</span></span>

##### <a name="finish-test-and-distribute"></a><span data-ttu-id="ca225-134">Fin : Tester et distribuer</span><span class="sxs-lookup"><span data-stu-id="ca225-134">Finish: Test and distribute</span></span>

>[!IMPORTANT]
> <span data-ttu-id="ca225-135">À droite, dans **Description,** vous voyez l’avertissement suivant :</span><span class="sxs-lookup"><span data-stu-id="ca225-135">On the right, in **Description**, you see the following warning:</span></span>
>
> <span data-ttu-id="ca225-136">&#9888; tableau **« validDomains » ne peut pas contenir de site de tunneling...**</span><span class="sxs-lookup"><span data-stu-id="ca225-136">&#9888; **The 'validDomains' array cannot contain a tunneling site...**</span></span>
>
><span data-ttu-id="ca225-137">Cet avertissement peut être ignoré lors du test de votre onglet.</span><span class="sxs-lookup"><span data-stu-id="ca225-137">This warning can be ignored while testing your tab.</span></span>

1. <span data-ttu-id="ca225-138">Dans la section **Tester et distribuer,** sélectionnez **Installer.**</span><span class="sxs-lookup"><span data-stu-id="ca225-138">In the **Test and Distribute** section, select **Install**.</span></span>

1. <span data-ttu-id="ca225-139">Dans la boîte de dialogue qui s’affiche, **sélectionnez** Ajouter et votre onglet s’affiche avec deux options.</span><span class="sxs-lookup"><span data-stu-id="ca225-139">In the pop-up dialog box, select **Add** and your tab is displayed with two options.</span></span>

1. <span data-ttu-id="ca225-140">Dans les options de l’onglet, **sélectionnez Gris** ou **Rouge.**</span><span class="sxs-lookup"><span data-stu-id="ca225-140">From the options in the tab, choose either **Select Gray** or **Select Red**.</span></span> <span data-ttu-id="ca225-141">L’onglet s’affiche en fonction de la couleur que vous avez sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="ca225-141">The tab is displayed according to the color you selected.</span></span>
 
    ![Onglet personnel ASPNETMVC chargé](../../assets/images/tab-images/personaltabaspnetmvcuploaded.png)

## <a name="view-your-personal-tab"></a><span data-ttu-id="ca225-143">Afficher votre onglet personnel</span><span class="sxs-lookup"><span data-stu-id="ca225-143">View your personal tab</span></span>

1. <span data-ttu-id="ca225-144">Dans la barre de navigation située à l’extrême gauche de l’application Teams, sélectionnez les &#x25CF;&#x25CF;&#x25CF;.</span><span class="sxs-lookup"><span data-stu-id="ca225-144">In the navigation bar located at the far left of the Teams app, select the ellipses &#x25CF;&#x25CF;&#x25CF;.</span></span> <span data-ttu-id="ca225-145">Une liste d’applications personnelles s’affiche.</span><span class="sxs-lookup"><span data-stu-id="ca225-145">A list of personal apps is shown.</span></span>

1. <span data-ttu-id="ca225-146">Sélectionnez votre onglet dans la liste pour l’afficher.</span><span class="sxs-lookup"><span data-stu-id="ca225-146">Select your tab from the list to view it.</span></span>
