### <a name="_layoutcshtml"></a><span data-ttu-id="e1b77-101">_Layout. cshtml</span><span class="sxs-lookup"><span data-stu-id="e1b77-101">_Layout.cshtml</span></span>

<span data-ttu-id="e1b77-102">Pour que votre onglet s’affiche dans Teams, vous devez inclure le **Kit de développement logiciel (SDK) JavaScript client Microsoft teams** et inclure un appel à `microsoftTeams.initialize()` après le chargement de votre page.</span><span class="sxs-lookup"><span data-stu-id="e1b77-102">For your tab to display in Teams, you must include the **Microsoft Teams JavaScript client SDK** and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="e1b77-103">Voici comment votre onglet et le client teams communiquent :</span><span class="sxs-lookup"><span data-stu-id="e1b77-103">This is how your tab and the Teams client communicate:</span></span>

- <span data-ttu-id="e1b77-104">Naviguez jusqu’au dossier **partagé** , ouvrez **_Layout. cshtml**et ajoutez ce qui suit à `<head>` la balise :</span><span class="sxs-lookup"><span data-stu-id="e1b77-104">Navigate to the **Shared** folder, open **_Layout.cshtml**, and add the following to the `<head>` tag:</span></span>

```html
<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
```

>[!IMPORTANT]
><span data-ttu-id="e1b77-105">Ne copiez pas/ `<script src="...">` collez les URL à partir de cette page, car elles ne représentent pas nécessairement la dernière version.</span><span class="sxs-lookup"><span data-stu-id="e1b77-105">Don't copy/paste the `<script src="...">` URLs from this page, as they may not represent the latest version.</span></span> <span data-ttu-id="e1b77-106">Pour obtenir la dernière version du kit de développement logiciel (SDK), accédez toujours à : [Microsoft teams JavaScript API](https://www.npmjs.com/package/@microsoft/teams-js.com).</span><span class="sxs-lookup"><span data-stu-id="e1b77-106">To get the latest version of the SDK, always go to: [Microsoft Teams JavaScript API](https://www.npmjs.com/package/@microsoft/teams-js.com).</span></span>

### <a name="tabcshtml"></a><span data-ttu-id="e1b77-107">Tab. cshtml</span><span class="sxs-lookup"><span data-stu-id="e1b77-107">Tab.cshtml</span></span>

<span data-ttu-id="e1b77-108">Ouvrez **Tab. cshtml** et mettez à jour `<script>` l’incorporé comme suit :</span><span class="sxs-lookup"><span data-stu-id="e1b77-108">Open **Tab.cshtml** and update the embedded `<script>` as follows:</span></span>

- <span data-ttu-id="e1b77-109">En haut du script, appelez `microsoftTeams.initialize()`.</span><span class="sxs-lookup"><span data-stu-id="e1b77-109">At the top of the script, call `microsoftTeams.initialize()`.</span></span>

- <span data-ttu-id="e1b77-110">Mettez à `websiteUrl` jour `contentUrl` les valeurs et dans chaque fonction avec l’URL HTTPS ngrok sur votre onglet.</span><span class="sxs-lookup"><span data-stu-id="e1b77-110">Update the `websiteUrl` and `contentUrl` values in each function with the HTTPS ngrok URL to your tab.</span></span>

<span data-ttu-id="e1b77-111">Votre code doit maintenant ressembler à ce qui suit avec **y8rCgT2b** remplacé par votre URL ngrok :</span><span class="sxs-lookup"><span data-stu-id="e1b77-111">Your code should now look like the following with **y8rCgT2b** replaced with your ngrok URL:</span></span>

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

<span data-ttu-id="e1b77-112">Veillez à enregistrer la **tabulation. cshtml**mise à jour.</span><span class="sxs-lookup"><span data-stu-id="e1b77-112">Make sure to save the updated **Tab.cshtml**.</span></span>

## <a name="build-and-run-your-application"></a><span data-ttu-id="e1b77-113">Création et exécution de votre application</span><span class="sxs-lookup"><span data-stu-id="e1b77-113">Build and run your application</span></span>

- <span data-ttu-id="e1b77-114">Dans Visual Studio, appuyez sur **F5**ou sélectionnez **Démarrer le débogage** dans le menu **Déboguer** .</span><span class="sxs-lookup"><span data-stu-id="e1b77-114">In Visual Studio press **F5**, or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="e1b77-115">Vérifiez que **ngrok** est en cours d’exécution et qu’il fonctionne correctement en ouvrant votre navigateur et en accédant à votre page de contenu via l’URL HTTPS ngrok qui a été fournie dans votre fenêtre d’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="e1b77-115">Verify that **ngrok** is running and working properly by opening your browser and going to your content page via the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

>[!TIP]
><span data-ttu-id="e1b77-116">Vous devez avoir à la fois votre application dans Visual Studio et ngrok en cours d’exécution pour effectuer ce démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="e1b77-116">You need to have both your application in Visual Studio and ngrok running to complete this quickstart.</span></span> <span data-ttu-id="e1b77-117">Si vous devez arrêter l’exécution de votre application dans Visual Studio pour qu’elle fonctionne, **laissez ngrok en cours d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="e1b77-117">If you need to stop running your application in Visual Studio to work on it **keep ngrok running**.</span></span> <span data-ttu-id="e1b77-118">Il continuera à écouter et reprendra le routage de la demande de votre application lorsqu’elle redémarrera dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e1b77-118">It will continue to listen and will resume routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="e1b77-119">Si vous devez redémarrer le service ngrok, il renverra une nouvelle URL et vous devrez mettre à jour votre application avec la nouvelle URL.</span><span class="sxs-lookup"><span data-stu-id="e1b77-119">If you have to restart the ngrok service it will return a new URL and you'll have to update your application with the new URL.</span></span>

## <a name="upload-your-tab-to-teams-with-app-studio"></a><span data-ttu-id="e1b77-120">Télécharger votre onglet vers teams avec App Studio</span><span class="sxs-lookup"><span data-stu-id="e1b77-120">Upload your tab to Teams with App Studio</span></span>

>[!Note]
> <span data-ttu-id="e1b77-121">Nous utilisons App Studio pour modifier votre fichier **Manifest. JSON** et télécharger le package terminé vers Teams.</span><span class="sxs-lookup"><span data-stu-id="e1b77-121">We use App Studio to edit your **manifest.json** file and upload the completed package to Teams.</span></span> <span data-ttu-id="e1b77-122">Vous pouvez également modifier manuellement le fichier **Manifest. JSON** si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="e1b77-122">You can also manually edit the **manifest.json** file if you prefer.</span></span> <span data-ttu-id="e1b77-123">Si vous le faites, veillez à créer à nouveau la solution pour créer le fichier **. zip de tabulation** à télécharger.</span><span class="sxs-lookup"><span data-stu-id="e1b77-123">If you do, be sure to build the solution again to create the **tab.zip** file to upload.</span></span>

- <span data-ttu-id="e1b77-124">Ouvrez le client Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="e1b77-124">Open the Microsoft Teams client.</span></span> <span data-ttu-id="e1b77-125">Si vous utilisez la [version basée sur le Web](https://teams.microsoft.com) , vous pouvez inspecter votre code frontal à l’aide des [outils de développement](~/tabs/how-to/developer-tools.md)de votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="e1b77-125">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>

- <span data-ttu-id="e1b77-126">Ouvrez l’application Studio et sélectionnez l’onglet **éditeur de manifeste** .</span><span class="sxs-lookup"><span data-stu-id="e1b77-126">Open App studio and select the **Manifest editor** tab.</span></span>

- <span data-ttu-id="e1b77-127">Sélectionnez la vignette **Importer une application existante** dans l’éditeur de manifeste pour commencer à mettre à jour le package d’application pour votre onglet. Le code source est fourni avec son propre manifeste partiellement complet.</span><span class="sxs-lookup"><span data-stu-id="e1b77-127">Select the **Import an existing app** tile in the Manifest editor to begin updating the app package for your tab. The source code comes with its own partially complete manifest.</span></span> <span data-ttu-id="e1b77-128">Le nom de votre package d’application est **Tab. zip**.</span><span class="sxs-lookup"><span data-stu-id="e1b77-128">The name of your app package is **tab.zip**.</span></span> <span data-ttu-id="e1b77-129">Il doit se trouver ici :</span><span class="sxs-lookup"><span data-stu-id="e1b77-129">It should be found here:</span></span>

```bash
/bin/Debug/netcoreapp2.2/tab.zip
```

- <span data-ttu-id="e1b77-130">Téléchargez **Tab. zip** dans App Studio.</span><span class="sxs-lookup"><span data-stu-id="e1b77-130">Upload **tab.zip** to App Studio.</span></span>

### <a name="update-your-app-package-with-manifest-editor"></a><span data-ttu-id="e1b77-131">Mettre à jour votre package d’application avec l’éditeur de manifeste</span><span class="sxs-lookup"><span data-stu-id="e1b77-131">Update your app package with Manifest editor</span></span>

<span data-ttu-id="e1b77-132">Une fois que vous avez téléchargé votre package d’application dans App Studio, vous devez terminer de le configurer.</span><span class="sxs-lookup"><span data-stu-id="e1b77-132">Once you've uploaded your app package into App Studio, you'll need to finish configuring it.</span></span>

- <span data-ttu-id="e1b77-133">Sélectionnez la mosaïque de votre onglet nouvellement importé dans le volet droit de la page d’accueil de l’éditeur de manifeste.</span><span class="sxs-lookup"><span data-stu-id="e1b77-133">Select the tile for your newly imported tab in the right panel of the Manifest editor welcome page.</span></span>

<span data-ttu-id="e1b77-134">Il y a une liste d’étapes dans le côté gauche de l’éditeur de manifeste, et à droite, une liste de propriétés qui doivent avoir des valeurs pour chacune de ces étapes.</span><span class="sxs-lookup"><span data-stu-id="e1b77-134">There's a list of steps in the left-hand side of the Manifest editor, and on the right, a list of properties that need to have values for each of those steps.</span></span> <span data-ttu-id="e1b77-135">La plupart des informations ont été fournies par votre *fichier manifest. JSON* , mais il existe quelques champs que vous devrez mettre à jour :</span><span class="sxs-lookup"><span data-stu-id="e1b77-135">Much of the information has been provided by your *manifest.json* but there are a few fields that you'll need to update:</span></span>

#### <a name="details-app-details"></a><span data-ttu-id="e1b77-136">Détails : détails de l’application</span><span class="sxs-lookup"><span data-stu-id="e1b77-136">Details: App details</span></span>

- <span data-ttu-id="e1b77-137">Sous *identification* , sélectionnez ***générer*** pour remplacer l’ID d’espace réservé par le GUID requis pour votre onglet.</span><span class="sxs-lookup"><span data-stu-id="e1b77-137">Under *Identification* select ***Generate*** to replace the placeholder id with the required GUID for your tab.</span></span>

- <span data-ttu-id="e1b77-138">Sous *informations sur le développeur* , mettez à jour le champ **URL du site Web** avec votre URL HTTPS *ngrok* .</span><span class="sxs-lookup"><span data-stu-id="e1b77-138">Under *Developer information* update the **Website URL** field with your *ngrok* HTTPS URL.</span></span>

- <span data-ttu-id="e1b77-139">Sous *URL* de l’application, mettez à jour les champs **déclaration de confidentialité** et **conditions d’utilisation** avec votre URL HTTPS *ngrok* .</span><span class="sxs-lookup"><span data-stu-id="e1b77-139">Under *App URLs* update the **Privacy statement** and **Terms of use** URL fields with your *ngrok* HTTPS URL.</span></span> <span data-ttu-id="e1b77-140">N’oubliez pas d’inclure les chemins d’accès */Privacy* et */tou* à la fin des URL.</span><span class="sxs-lookup"><span data-stu-id="e1b77-140">Remember to include the */privacy* and */tou* paths at the end of the URLs.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="e1b77-141">Fonctionnalités : onglets</span><span class="sxs-lookup"><span data-stu-id="e1b77-141">Capabilities: Tabs</span></span>

<span data-ttu-id="e1b77-142">Dans la section *onglets* :</span><span class="sxs-lookup"><span data-stu-id="e1b77-142">In the *Tabs* section:</span></span>

- <span data-ttu-id="e1b77-143">Sous l' *onglet équipe* , sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="e1b77-143">Under *Team Tab* select **Add**.</span></span>

- <span data-ttu-id="e1b77-144">Dans la fenêtre contextuelle de l’onglet équipe, mettez à jour l' `https://<yourngrokurl>/tab`URL de *configuration* vers.</span><span class="sxs-lookup"><span data-stu-id="e1b77-144">In the Team tab pop-up window update the *Configuration URL* to `https://<yourngrokurl>/tab`.</span></span>

- <span data-ttu-id="e1b77-145">Enfin, assurez-vous que la \*mise à jour de la configuration est possible ? \*Les cases Team et *Group chat* sont cochées, puis sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="e1b77-145">Finally, make sure the *can update configuration? Team*, and *Group chat* boxes are checked and select **Save**.</span></span>

#### <a name="finish-domains-and-permissions"></a><span data-ttu-id="e1b77-146">Terminer : domaines et autorisations</span><span class="sxs-lookup"><span data-stu-id="e1b77-146">Finish: Domains and permissions</span></span>

<span data-ttu-id="e1b77-147">Dans la section *domaines et autorisations* , les *domaines de votre champ d’onglets* doivent contenir votre URL ngrok sans le préfixe `<yourngrokurl>.ngrok.io/`HTTPS-.</span><span class="sxs-lookup"><span data-stu-id="e1b77-147">In the *Domains and permissions* section, the *Domains from your tabs* field should contain your ngrok URL without the HTTPS prefix - `<yourngrokurl>.ngrok.io/`.</span></span>

#### <a name="test-and-distribute-test-and-distribute"></a><span data-ttu-id="e1b77-148">Test et distribution : test et distribution</span><span class="sxs-lookup"><span data-stu-id="e1b77-148">Test and distribute: Test and distribute</span></span>

>[!IMPORTANT]
><span data-ttu-id="e1b77-149">Dans le champ **Description** à droite, vous verrez l’avertissement suivant :</span><span class="sxs-lookup"><span data-stu-id="e1b77-149">In the **Description** field on the right you'll see the following warning:</span></span>
>
><span data-ttu-id="e1b77-150">&#9888;**le tableau « validDomains » ne peut pas contenir de site de tunneling...**</span><span class="sxs-lookup"><span data-stu-id="e1b77-150">&#9888; "**The 'validDomains' array cannot contain a tunneling site...**"</span></span>
>
><span data-ttu-id="e1b77-151">Cet avertissement peut être ignoré lors du test de votre onglet.</span><span class="sxs-lookup"><span data-stu-id="e1b77-151">This warning can be ignored while testing your tab.</span></span>

<span data-ttu-id="e1b77-152">Dans la section *test et distribution* :</span><span class="sxs-lookup"><span data-stu-id="e1b77-152">In the *Test and distribute* section:</span></span>

- <span data-ttu-id="e1b77-153">Sélectionnez **Installer**.</span><span class="sxs-lookup"><span data-stu-id="e1b77-153">Select **Install**.</span></span>

- <span data-ttu-id="e1b77-154">Dans la fenêtre contextuelle *Ajouter à un champ d’équipe ou de conversation* , entrez votre équipe et sélectionnez **installer**.</span><span class="sxs-lookup"><span data-stu-id="e1b77-154">In the pop-up window's *Add to a team or chat* field enter your team and select **Install**.</span></span>

- <span data-ttu-id="e1b77-155">Dans la fenêtre contextuelle suivante, sélectionnez le canal d’équipe dans lequel vous souhaitez afficher l’onglet, puis sélectionnez **configurer**.</span><span class="sxs-lookup"><span data-stu-id="e1b77-155">In the next pop-up window choose the team channel where you would like the tab displayed and select **Set up**.</span></span>

- <span data-ttu-id="e1b77-156">Dans la fenêtre contextuelle finale, sélectionnez une valeur pour la page d’onglet (icône rouge ou gris) et sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="e1b77-156">In the final pop-up window select a value for the tab page (either a red or gray icon) and select **Save**.</span></span>

<span data-ttu-id="e1b77-157">Pour afficher votre onglet, accédez à l’équipe sur laquelle vous l’avez installé, puis sélectionnez-le dans la barre d’onglets.</span><span class="sxs-lookup"><span data-stu-id="e1b77-157">To view your tab, navigate to the team you installed it on, and select it from the tab bar.</span></span> <span data-ttu-id="e1b77-158">La page que vous avez choisie lors de la configuration doit s’afficher.</span><span class="sxs-lookup"><span data-stu-id="e1b77-158">The page that you chose during configuration should be displayed.</span></span>
