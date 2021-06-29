### <a name="_layoutcshtml"></a><span data-ttu-id="e88a6-101">_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="e88a6-101">_Layout.cshtml</span></span>

<span data-ttu-id="e88a6-102">Pour que votre onglet s’affiche dans Teams, vous devez inclure le **SDK client JavaScript Microsoft Teams** et inclure un appel après le chargement de `microsoftTeams.initialize()` votre page.</span><span class="sxs-lookup"><span data-stu-id="e88a6-102">For your tab to display in Teams, you must include the **Microsoft Teams JavaScript client SDK** and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="e88a6-103">Voici comment votre onglet et le client Teams communiquent :</span><span class="sxs-lookup"><span data-stu-id="e88a6-103">This is how your tab and the Teams client communicate:</span></span>

<span data-ttu-id="e88a6-104">Go to the **Shared** folder, open **_Layout.cshtml**, and add the following to the `<head>` tag:</span><span class="sxs-lookup"><span data-stu-id="e88a6-104">Go to the **Shared** folder, open **_Layout.cshtml**, and add the following to the `<head>` tag:</span></span>

```html
<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
```

>[!IMPORTANT]
> <span data-ttu-id="e88a6-105">Ne copiez pas et collez les URL de cette page, car elles peuvent ne pas représenter `<script src="...">` la dernière version.</span><span class="sxs-lookup"><span data-stu-id="e88a6-105">Do not copy and paste the `<script src="...">` URLs from this page, as they may not represent the latest version.</span></span> <span data-ttu-id="e88a6-106">Pour obtenir la dernière version du SDK, toujours Microsoft Teams [API JavaScript](https://www.npmjs.com/package/@microsoft/teams-js).</span><span class="sxs-lookup"><span data-stu-id="e88a6-106">To get the latest version of the SDK, always go to [Microsoft Teams JavaScript API](https://www.npmjs.com/package/@microsoft/teams-js).</span></span>

### <a name="tabcshtml"></a><span data-ttu-id="e88a6-107">Tab.cshtml</span><span class="sxs-lookup"><span data-stu-id="e88a6-107">Tab.cshtml</span></span>

<span data-ttu-id="e88a6-108">**Pour mettre à jour le script incorporé**</span><span class="sxs-lookup"><span data-stu-id="e88a6-108">**To update the embedded script**</span></span>

1. <span data-ttu-id="e88a6-109">Dans Visual Studio, **ouvrez Tab.cshtml** pour mettre à jour l’incorporé `<script>` .</span><span class="sxs-lookup"><span data-stu-id="e88a6-109">In Visual Studio, open **Tab.cshtml** to update the embedded `<script>`.</span></span>

1. <span data-ttu-id="e88a6-110">En haut du script, appelez `microsoftTeams.initialize()` .</span><span class="sxs-lookup"><span data-stu-id="e88a6-110">At the top of the script, call `microsoftTeams.initialize()`.</span></span>

1. <span data-ttu-id="e88a6-111">Mettez à `websiteUrl` jour les `contentUrl` valeurs de chaque fonction avec l’URL HTTPS ngrok sur votre onglet.</span><span class="sxs-lookup"><span data-stu-id="e88a6-111">Update the `websiteUrl` and `contentUrl` values in each function with the HTTPS ngrok URL to your tab.</span></span>

    <span data-ttu-id="e88a6-112">Votre code doit maintenant ressembler à ce qui suit avec **y8rCgT2b** remplacé par votre URL ngrok :</span><span class="sxs-lookup"><span data-stu-id="e88a6-112">Your code should now look like the following with **y8rCgT2b** replaced with your ngrok URL:</span></span>

    ```javascript
        microsoftTeams.initialize();
    
        let saveGray = () => {
            microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
                microsoftTeams.settings.setSettings({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/gray/`,
                    entityId: "grayIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                saveEvent.notifySuccess();
            });
        }

        let saveRed = () => {
            microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
                microsoftTeams.settings.setSettings({
                    websiteUrl: `https://y8rCgT2b.ngrok.io`,
                    contentUrl: `https://y8rCgT2b.ngrok.io/red/`,
                    entityId: "redIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                saveEvent.notifySuccess();
            });
        }
    ```

1. <span data-ttu-id="e88a6-113">Veillez à enregistrer le **tab.cshtml mis à jour.**</span><span class="sxs-lookup"><span data-stu-id="e88a6-113">Make sure to save the updated **Tab.cshtml**.</span></span>

## <a name="build-and-run-your-application"></a><span data-ttu-id="e88a6-114">Créer et exécuter votre application</span><span class="sxs-lookup"><span data-stu-id="e88a6-114">Build and run your application</span></span>

<span data-ttu-id="e88a6-115">Dans Visual Studio, appuyez **sur F5** ou choisissez **Démarrer le débogage** dans le menu **Débogage.**</span><span class="sxs-lookup"><span data-stu-id="e88a6-115">In Visual Studio, press **F5** or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="e88a6-116">Vérifiez que **ngrok** fonctionne correctement en ouvrant votre navigateur et en allant sur votre page de contenu via l’URL HTTPS ngrok fournie dans la fenêtre d’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="e88a6-116">Verify that **ngrok** is running and working properly by opening your browser and going to your content page via the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

> [!TIP]
> <span data-ttu-id="e88a6-117">Votre application doit être en cours d’exécution Visual Studio et ngrok.</span><span class="sxs-lookup"><span data-stu-id="e88a6-117">You need to have both your application in Visual Studio and ngrok running.</span></span> <span data-ttu-id="e88a6-118">Si vous devez arrêter l’exécution de votre application dans Visual Studio pour travailler dessus, **ngrok est toujours en cours d’exécution.**</span><span class="sxs-lookup"><span data-stu-id="e88a6-118">If you need to stop running your application in Visual Studio to work on it **keep ngrok running**.</span></span> <span data-ttu-id="e88a6-119">Il continuera à écouter et reprendra le routage de la demande de votre application lors de son redémarrage dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e88a6-119">It will continue to listen and will resume routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="e88a6-120">Si vous devez redémarrer le service ngrok, il retourne une nouvelle URL et vous devez mettre à jour votre application avec la nouvelle URL.</span><span class="sxs-lookup"><span data-stu-id="e88a6-120">If you have to restart the ngrok service, it will return a new URL and you will have to update your application with the new URL.</span></span>

## <a name="upload-your-tab"></a><span data-ttu-id="e88a6-121">Télécharger onglet</span><span class="sxs-lookup"><span data-stu-id="e88a6-121">Upload your tab</span></span>

>[!Note]
> <span data-ttu-id="e88a6-122">App Studio peut être utilisé pour modifier votre **manifest.jsfichier** et télécharger le package terminé dans Teams.</span><span class="sxs-lookup"><span data-stu-id="e88a6-122">App Studio can be used to edit your **manifest.json** file and upload the completed package to Teams.</span></span> <span data-ttu-id="e88a6-123">Vous pouvez également modifier manuellement le **fichiermanifest.jssi** vous préférez.</span><span class="sxs-lookup"><span data-stu-id="e88a6-123">You can also manually edit the **manifest.json** file if you prefer.</span></span> <span data-ttu-id="e88a6-124">Si vous le faites, assurez-vous de générer à nouveau la solution pour créertab.zip **fichier** à télécharger.</span><span class="sxs-lookup"><span data-stu-id="e88a6-124">If you do, be sure to build the solution again to create the **tab.zip** file to upload.</span></span>

<span data-ttu-id="e88a6-125">**Pour télécharger votre onglet**</span><span class="sxs-lookup"><span data-stu-id="e88a6-125">**To upload your tab**</span></span>

1. <span data-ttu-id="e88a6-126">Go to Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="e88a6-126">Go to Microsoft Teams.</span></span> <span data-ttu-id="e88a6-127">Si vous utilisez la [version web,](https://teams.microsoft.com) vous pouvez inspecter votre code frontal à l’aide des outils de développement [de votre navigateur.](~/tabs/how-to/developer-tools.md)</span><span class="sxs-lookup"><span data-stu-id="e88a6-127">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>

1. <span data-ttu-id="e88a6-128">Go to **App Studio** and select the **Manifest editor** tab.</span><span class="sxs-lookup"><span data-stu-id="e88a6-128">Go to **App Studio** and select the **Manifest editor** tab.</span></span>

1. <span data-ttu-id="e88a6-129">Sélectionnez **Importer une application existante dans** l’éditeur de manifeste pour commencer à mettre à jour le package d’application pour votre onglet. Le code source est livré avec son propre manifeste partiellement complet.</span><span class="sxs-lookup"><span data-stu-id="e88a6-129">Select **Import an existing app** in the Manifest editor to begin updating the app package for your tab. The source code comes with its own partially complete manifest.</span></span> <span data-ttu-id="e88a6-130">Le nom de votre package d’application **esttab.zip**.</span><span class="sxs-lookup"><span data-stu-id="e88a6-130">The name of your app package is **tab.zip**.</span></span> <span data-ttu-id="e88a6-131">Il est disponible ici :</span><span class="sxs-lookup"><span data-stu-id="e88a6-131">It is available here:</span></span>

    ```bash
    /bin/Debug/netcoreapp2.2/tab.zip
    ```

1. <span data-ttu-id="e88a6-132">Télécharger **tab.zip** app Studio.</span><span class="sxs-lookup"><span data-stu-id="e88a6-132">Upload **tab.zip** to App Studio.</span></span>

### <a name="update-your-app-package-with-manifest-editor"></a><span data-ttu-id="e88a6-133">Mettre à jour votre package d’application avec l’éditeur de manifeste</span><span class="sxs-lookup"><span data-stu-id="e88a6-133">Update your app package with Manifest editor</span></span>

<span data-ttu-id="e88a6-134">Une fois que vous avez chargé votre package d’application dans App Studio, vous devez terminer sa configuration.</span><span class="sxs-lookup"><span data-stu-id="e88a6-134">After you have uploaded your app package into App Studio, you must finish configuring it.</span></span>

<span data-ttu-id="e88a6-135">Sélectionnez la vignette de votre onglet nouvellement importé dans le panneau droit de la page d’accueil de l’éditeur de manifeste.</span><span class="sxs-lookup"><span data-stu-id="e88a6-135">Select the tile for your newly imported tab in the right panel of the Manifest editor welcome page.</span></span>

<span data-ttu-id="e88a6-136">Il existe une liste d’étapes dans le côté gauche de l’éditeur de manifeste, et à droite, une liste de propriétés qui doivent avoir des valeurs pour chacune de ces étapes.</span><span class="sxs-lookup"><span data-stu-id="e88a6-136">There is a list of steps in the left-hand side of the Manifest editor, and on the right, a list of properties that must have values for each of those steps.</span></span> <span data-ttu-id="e88a6-137">La plupart des informations ont été fournies par votre **manifest.js,** mais vous devez mettre à jour certains champs :</span><span class="sxs-lookup"><span data-stu-id="e88a6-137">Much of the information has been provided by your **manifest.json** but there are a few fields that you must update:</span></span>

#### <a name="details-app-details"></a><span data-ttu-id="e88a6-138">Détails : détails de l’application</span><span class="sxs-lookup"><span data-stu-id="e88a6-138">Details: App details</span></span>

<span data-ttu-id="e88a6-139">Dans la section **Détails de l’application** :</span><span class="sxs-lookup"><span data-stu-id="e88a6-139">In the **App details** section:</span></span>

1. <span data-ttu-id="e88a6-140">Sous **Identification,** **sélectionnez Générer** pour remplacer l’ID d’espace réservé par le GUID requis pour votre onglet.</span><span class="sxs-lookup"><span data-stu-id="e88a6-140">Under **Identification**, select **Generate** to replace the placeholder ID with the required GUID for your tab.</span></span>

1. <span data-ttu-id="e88a6-141">Sous **Informations sur le développeur,** mettez à jour le site **web** avec votre URL HTTPS **ngrok.**</span><span class="sxs-lookup"><span data-stu-id="e88a6-141">Under **Developer information**, update **Website** with your **ngrok** HTTPS URL.</span></span>

1. <span data-ttu-id="e88a6-142">Sous **URL d’application,** mettez à jour la déclaration **de confidentialité** et les conditions `https://<yourngrokurl>/privacy` **d’utilisation** `https://<yourngrokurl>/tou`>.</span><span class="sxs-lookup"><span data-stu-id="e88a6-142">Under **App URLs**, update the **Privacy statement** to `https://<yourngrokurl>/privacy` and **Terms of use** to `https://<yourngrokurl>/tou`>.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="e88a6-143">Fonctionnalités : onglets</span><span class="sxs-lookup"><span data-stu-id="e88a6-143">Capabilities: Tabs</span></span>

<span data-ttu-id="e88a6-144">Dans la section **Onglets** :</span><span class="sxs-lookup"><span data-stu-id="e88a6-144">In the **Tabs** section:</span></span>

1. <span data-ttu-id="e88a6-145">Sous **l’onglet Équipe,** **sélectionnez Ajouter.**</span><span class="sxs-lookup"><span data-stu-id="e88a6-145">Under **Team tab**, select **Add**.</span></span>

1. <span data-ttu-id="e88a6-146">Dans la fenêtre **pop-up de** l’onglet Équipe, mettez à jour l’URL **de configuration** sur `https://<yourngrokurl>/tab` .</span><span class="sxs-lookup"><span data-stu-id="e88a6-146">In the **Team tab** pop-up window, update the **Configuration URL** to `https://<yourngrokurl>/tab`.</span></span>

1. <span data-ttu-id="e88a6-147">Assurez-vous **que les case**  à cocher Mettre à jour la configuration ? , **Équipe** et Groupe sont sélectionnées et sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="e88a6-147">Ensure the **Can update configuration?**, **Team**, and **Group chat** checkboxes are selected and select **Save**.</span></span>

#### <a name="finish-domains-and-permissions"></a><span data-ttu-id="e88a6-148">Finish: Domains and permissions</span><span class="sxs-lookup"><span data-stu-id="e88a6-148">Finish: Domains and permissions</span></span>

<span data-ttu-id="e88a6-149">Dans la section **Domaines et autorisations,** les domaines de vos **onglets** doivent contenir votre URL ngrok sans le préfixe HTTPS. `<yourngrokurl>.ngrok.io/`</span><span class="sxs-lookup"><span data-stu-id="e88a6-149">In the **Domains and permissions** section, **Domains from your tabs** must contain your ngrok URL without the HTTPS prefix `<yourngrokurl>.ngrok.io/`.</span></span>

#### <a name="finish-test-and-distribute"></a><span data-ttu-id="e88a6-150">Fin : Tester et distribuer</span><span class="sxs-lookup"><span data-stu-id="e88a6-150">Finish: Test and distribute</span></span>

>[!IMPORTANT]
> <span data-ttu-id="e88a6-151">À droite, dans **Description,** vous voyez l’avertissement suivant :</span><span class="sxs-lookup"><span data-stu-id="e88a6-151">On the right, in **Description**, you see the following warning:</span></span>
>
> <span data-ttu-id="e88a6-152">&#9888; «**Le tableau « validDomains » ne peut** pas contenir un site de tunneling... »</span><span class="sxs-lookup"><span data-stu-id="e88a6-152">&#9888; "**The 'validDomains' array cannot contain a tunneling site...**"</span></span>
>
> <span data-ttu-id="e88a6-153">Cet avertissement peut être ignoré lors du test de votre onglet.</span><span class="sxs-lookup"><span data-stu-id="e88a6-153">This warning can be ignored while testing your tab.</span></span>

1. <span data-ttu-id="e88a6-154">Dans la section **Tester et distribuer,** sélectionnez **Installer.**</span><span class="sxs-lookup"><span data-stu-id="e88a6-154">In the **Test and Distribute** section, select **Install**.</span></span>

1. <span data-ttu-id="e88a6-155">Dans la boîte de dialogue  de fenêtre instantanée, sélectionnez Ajouter à une équipe ou, dans la zone de la boîte de dialogue, sélectionnez Ajouter **à une conversation.**</span><span class="sxs-lookup"><span data-stu-id="e88a6-155">In the pop-up dialog box, select **Add to a team** or from the drop-down, select **Add to a chat**.</span></span>

1. <span data-ttu-id="e88a6-156">Choisissez l’équipe ou la conversation dans laquelle vous souhaitez afficher l’onglet, puis sélectionnez **Configurer un onglet.**</span><span class="sxs-lookup"><span data-stu-id="e88a6-156">Choose the team or chat where you want the tab to be displayed and select **Set up a tab**.</span></span>

1. <span data-ttu-id="e88a6-157">Dans la boîte de dialogue de fenêtre pop-up suivante, sélectionnez **Gris** ou **Rouge,** puis sélectionnez **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="e88a6-157">In the next pop-up dialog box, choose either **Select Gray** or **Select Red**, and select **Save**.</span></span>

1. <span data-ttu-id="e88a6-158">Pour afficher votre onglet, allez dans l’équipe où vous avez installé l’onglet, puis sélectionnez-le dans la barre d’onglets.</span><span class="sxs-lookup"><span data-stu-id="e88a6-158">To view your tab, go to the team where you installed the tab, and select it from the tab bar.</span></span> <span data-ttu-id="e88a6-159">La page que vous avez choisie lors de la configuration s’affiche.</span><span class="sxs-lookup"><span data-stu-id="e88a6-159">The page that you chose during configuration is displayed.</span></span>

    ![Onglet canal ASPNETMVC chargé](../../assets/images/tab-images/channeltabaspnetmvcuploaded.png)

