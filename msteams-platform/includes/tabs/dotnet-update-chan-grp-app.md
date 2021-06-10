### <a name="_layoutcshtml"></a><span data-ttu-id="6f4b2-101">_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="6f4b2-101">_Layout.cshtml</span></span>

<span data-ttu-id="6f4b2-102">Pour que votre onglet s’affiche dans Teams, vous devez inclure le **SDK client JavaScript Microsoft Teams** et inclure un appel après le chargement de `microsoftTeams.initialize()` votre page.</span><span class="sxs-lookup"><span data-stu-id="6f4b2-102">For your tab to display in Teams, you must include the **Microsoft Teams JavaScript client SDK** and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="6f4b2-103">Voici comment votre onglet et le client Teams communiquent :</span><span class="sxs-lookup"><span data-stu-id="6f4b2-103">This is how your tab and the Teams client communicate:</span></span>

- <span data-ttu-id="6f4b2-104">Accédez au **dossier** partagé, **ouvrez _Layout.cshtml** et ajoutez ce qui suit à la `<head>` balise :</span><span class="sxs-lookup"><span data-stu-id="6f4b2-104">Navigate to the **Shared** folder, open **_Layout.cshtml**, and add the following to the `<head>` tag:</span></span>

    ```html
    <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
    <script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
    ```

>[!IMPORTANT]
><span data-ttu-id="6f4b2-105">Ne copiez/collez pas les URL de cette page, car elles peuvent ne pas représenter `<script src="...">` la dernière version.</span><span class="sxs-lookup"><span data-stu-id="6f4b2-105">Don't copy/paste the `<script src="...">` URLs from this page, as they may not represent the latest version.</span></span> <span data-ttu-id="6f4b2-106">Pour obtenir la dernière version du SDK, toujours aller à : [Microsoft Teams API JavaScript](https://www.npmjs.com/package/@microsoft/teams-js).</span><span class="sxs-lookup"><span data-stu-id="6f4b2-106">To get the latest version of the SDK, always go to: [Microsoft Teams JavaScript API](https://www.npmjs.com/package/@microsoft/teams-js).</span></span>

### <a name="tabcshtml"></a><span data-ttu-id="6f4b2-107">Tab.cshtml</span><span class="sxs-lookup"><span data-stu-id="6f4b2-107">Tab.cshtml</span></span>

<span data-ttu-id="6f4b2-108">Ouvrez **Tab.cshtml** et mettez à jour l’incorporé `<script>` comme suit :</span><span class="sxs-lookup"><span data-stu-id="6f4b2-108">Open **Tab.cshtml** and update the embedded `<script>` as follows:</span></span>

- <span data-ttu-id="6f4b2-109">En haut du script, appelez `microsoftTeams.initialize()` .</span><span class="sxs-lookup"><span data-stu-id="6f4b2-109">At the top of the script, call `microsoftTeams.initialize()`.</span></span>

- <span data-ttu-id="6f4b2-110">Mettez à `websiteUrl` jour les `contentUrl` valeurs de chaque fonction avec l’URL HTTPS ngrok sur votre onglet.</span><span class="sxs-lookup"><span data-stu-id="6f4b2-110">Update the `websiteUrl` and `contentUrl` values in each function with the HTTPS ngrok URL to your tab.</span></span>

<span data-ttu-id="6f4b2-111">Votre code doit maintenant ressembler à ce qui suit avec **y8rCgT2b** remplacé par votre URL ngrok :</span><span class="sxs-lookup"><span data-stu-id="6f4b2-111">Your code should now look like the following with **y8rCgT2b** replaced with your ngrok URL:</span></span>

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

<span data-ttu-id="6f4b2-112">Veillez à enregistrer le **tab.cshtml mis à jour.**</span><span class="sxs-lookup"><span data-stu-id="6f4b2-112">Make sure to save the updated **Tab.cshtml**.</span></span>

## <a name="build-and-run-your-application"></a><span data-ttu-id="6f4b2-113">Créer et exécuter votre application</span><span class="sxs-lookup"><span data-stu-id="6f4b2-113">Build and run your application</span></span>

- <span data-ttu-id="6f4b2-114">Dans Visual Studio **appuyez sur F5** ou choisissez **Démarrer le débogage** dans le menu **Débogage.**</span><span class="sxs-lookup"><span data-stu-id="6f4b2-114">In Visual Studio press **F5**, or choose **Start Debugging** from the **Debug** menu.</span></span> <span data-ttu-id="6f4b2-115">Vérifiez que **ngrok** fonctionne correctement en ouvrant votre navigateur et en allant sur votre page de contenu via l’URL HTTPS ngrok fournie dans la fenêtre d’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="6f4b2-115">Verify that **ngrok** is running and working properly by opening your browser and going to your content page via the ngrok HTTPS URL that was provided in your command prompt window.</span></span>

>[!TIP]
><span data-ttu-id="6f4b2-116">Vous devez avoir votre application en cours d Visual Studio et ngrok en cours d’exécution pour effectuer ce démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="6f4b2-116">You need to have both your application in Visual Studio and ngrok running to complete this quickstart.</span></span> <span data-ttu-id="6f4b2-117">Si vous devez arrêter l’exécution de votre application dans Visual Studio pour travailler dessus, **ngrok est toujours en cours d’exécution.**</span><span class="sxs-lookup"><span data-stu-id="6f4b2-117">If you need to stop running your application in Visual Studio to work on it **keep ngrok running**.</span></span> <span data-ttu-id="6f4b2-118">Il continuera à écouter et reprendra le routage de la demande de votre application lors de son redémarrage dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6f4b2-118">It will continue to listen and will resume routing your application's request when it restarts in Visual Studio.</span></span> <span data-ttu-id="6f4b2-119">Si vous devez redémarrer le service ngrok, il retourne une nouvelle URL et vous devez mettre à jour votre application avec la nouvelle URL.</span><span class="sxs-lookup"><span data-stu-id="6f4b2-119">If you have to restart the ngrok service it will return a new URL and you'll have to update your application with the new URL.</span></span>

## <a name="upload-your-tab-to-teams"></a><span data-ttu-id="6f4b2-120">Télécharger votre onglet pour Teams</span><span class="sxs-lookup"><span data-stu-id="6f4b2-120">Upload your tab to Teams</span></span>

>[!Note]
> <span data-ttu-id="6f4b2-121">Nous utilisons App Studio pour modifier votre **manifest.jsfichier** et charger le package terminé dans Teams.</span><span class="sxs-lookup"><span data-stu-id="6f4b2-121">We use App Studio to edit your **manifest.json** file and upload the completed package to Teams.</span></span> <span data-ttu-id="6f4b2-122">Vous pouvez également modifier manuellement le **fichiermanifest.jssi** vous préférez.</span><span class="sxs-lookup"><span data-stu-id="6f4b2-122">You can also manually edit the **manifest.json** file if you prefer.</span></span> <span data-ttu-id="6f4b2-123">Si vous le faites, n’oubliez pas de générer à nouveau la solution pour créertab.zip **fichier** à télécharger.</span><span class="sxs-lookup"><span data-stu-id="6f4b2-123">If you do, be sure to build the solution again to create the **tab.zip** file to upload.</span></span>

- <span data-ttu-id="6f4b2-124">Ouvrez le client Microsoft Teams client.</span><span class="sxs-lookup"><span data-stu-id="6f4b2-124">Open the Microsoft Teams client.</span></span> <span data-ttu-id="6f4b2-125">Si vous utilisez la [version web,](https://teams.microsoft.com) vous pouvez inspecter votre code frontal à l’aide des outils de développement [de votre navigateur.](~/tabs/how-to/developer-tools.md)</span><span class="sxs-lookup"><span data-stu-id="6f4b2-125">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>

- <span data-ttu-id="6f4b2-126">Ouvrez App studio et sélectionnez **l’onglet Éditeur de** manifeste.</span><span class="sxs-lookup"><span data-stu-id="6f4b2-126">Open App studio and select the **Manifest editor** tab.</span></span>

- <span data-ttu-id="6f4b2-127">Sélectionnez **la vignette Importer une application existante** dans l’éditeur de manifeste pour commencer à mettre à jour le package d’application pour votre onglet. Le code source est livré avec son propre manifeste partiellement complet.</span><span class="sxs-lookup"><span data-stu-id="6f4b2-127">Select the **Import an existing app** tile in the Manifest editor to begin updating the app package for your tab. The source code comes with its own partially complete manifest.</span></span> <span data-ttu-id="6f4b2-128">Le nom de votre package d’application **esttab.zip**.</span><span class="sxs-lookup"><span data-stu-id="6f4b2-128">The name of your app package is **tab.zip**.</span></span> <span data-ttu-id="6f4b2-129">Il doit être trouvé ici :</span><span class="sxs-lookup"><span data-stu-id="6f4b2-129">It should be found here:</span></span>

    ```bash
    /bin/Debug/netcoreapp2.2/tab.zip
    ```

- <span data-ttu-id="6f4b2-130">Télécharger **tab.zip** app Studio.</span><span class="sxs-lookup"><span data-stu-id="6f4b2-130">Upload **tab.zip** to App Studio.</span></span>

### <a name="update-your-app-package-with-manifest-editor"></a><span data-ttu-id="6f4b2-131">Mettre à jour votre package d’application avec l’éditeur de manifeste</span><span class="sxs-lookup"><span data-stu-id="6f4b2-131">Update your app package with Manifest editor</span></span>

<span data-ttu-id="6f4b2-132">Une fois que vous avez chargé votre package d’application dans App Studio, vous devez terminer sa configuration.</span><span class="sxs-lookup"><span data-stu-id="6f4b2-132">Once you've uploaded your app package into App Studio, you'll need to finish configuring it.</span></span>

- <span data-ttu-id="6f4b2-133">Sélectionnez la vignette de votre onglet nouvellement importé dans le panneau droit de la page d’accueil de l’éditeur de manifeste.</span><span class="sxs-lookup"><span data-stu-id="6f4b2-133">Select the tile for your newly imported tab in the right panel of the Manifest editor welcome page.</span></span>

<span data-ttu-id="6f4b2-134">Il existe une liste d’étapes dans le côté gauche de l’éditeur de manifeste, et à droite, une liste de propriétés qui doivent avoir des valeurs pour chacune de ces étapes.</span><span class="sxs-lookup"><span data-stu-id="6f4b2-134">There's a list of steps in the left-hand side of the Manifest editor, and on the right, a list of properties that need to have values for each of those steps.</span></span> <span data-ttu-id="6f4b2-135">La plupart des informations ont été fournies par votre *manifest.js,* mais il existe quelques champs que vous devrez mettre à jour :</span><span class="sxs-lookup"><span data-stu-id="6f4b2-135">Much of the information has been provided by your *manifest.json* but there are a few fields that you'll need to update:</span></span>

#### <a name="details-app-details"></a><span data-ttu-id="6f4b2-136">Détails : détails de l’application</span><span class="sxs-lookup"><span data-stu-id="6f4b2-136">Details: App details</span></span>

<span data-ttu-id="6f4b2-137">Dans la section *Détails de l’application* :</span><span class="sxs-lookup"><span data-stu-id="6f4b2-137">In the *App details* section:</span></span>

- <span data-ttu-id="6f4b2-138">*Identification*: **sélectionnez Générer** pour remplacer l’ID d’espace réservé par le GUID requis pour votre onglet.</span><span class="sxs-lookup"><span data-stu-id="6f4b2-138">*Identification*: select **Generate** to replace the placeholder id with the required GUID for your tab.</span></span>

- <span data-ttu-id="6f4b2-139">*Informations sur le* développeur : mettez à jour **le champ URL** du site web avec votre URL HTTPS *ngrok.*</span><span class="sxs-lookup"><span data-stu-id="6f4b2-139">*Developer information*: update the **Website URL** field with your *ngrok* HTTPS URL.</span></span>

- <span data-ttu-id="6f4b2-140">*URL d’application*: mettez à jour **la déclaration de confidentialité** et les conditions `https://<yourngrokurl>/privacy` **d’utilisation** `https://<yourngrokurl>/tou`>.</span><span class="sxs-lookup"><span data-stu-id="6f4b2-140">*App URLs*: update the **Privacy statement** to `https://<yourngrokurl>/privacy` and **Terms of use** to `https://<yourngrokurl>/tou`>.</span></span>

#### <a name="capabilities-tabs"></a><span data-ttu-id="6f4b2-141">Fonctionnalités : onglets</span><span class="sxs-lookup"><span data-stu-id="6f4b2-141">Capabilities: Tabs</span></span>

<span data-ttu-id="6f4b2-142">Dans la section *Onglets* :</span><span class="sxs-lookup"><span data-stu-id="6f4b2-142">In the *Tabs* section:</span></span>

- <span data-ttu-id="6f4b2-143">*Onglet Équipe*: sélectionnez **Ajouter.**</span><span class="sxs-lookup"><span data-stu-id="6f4b2-143">*Team Tab*: select **Add**.</span></span>

- <span data-ttu-id="6f4b2-144">Dans la fenêtre pop-up de l’onglet Équipe, mettez à jour *l’URL de configuration* sur `https://<yourngrokurl>/tab` .</span><span class="sxs-lookup"><span data-stu-id="6f4b2-144">In the Team tab pop-up window update the *Configuration URL* to `https://<yourngrokurl>/tab`.</span></span>

- <span data-ttu-id="6f4b2-145">Enfin, assurez-vous que la *configuration peut être mise à jour ? Les cases* de *conversation* d’équipe et de groupe sont cochées, puis **sélectionnez Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="6f4b2-145">Finally, make sure the *can update configuration? Team*, and *Group chat* boxes are checked and select **Save**.</span></span>

#### <a name="finish-domains-and-permissions"></a><span data-ttu-id="6f4b2-146">Finish: Domains and permissions</span><span class="sxs-lookup"><span data-stu-id="6f4b2-146">Finish: Domains and permissions</span></span>

<span data-ttu-id="6f4b2-147">Dans la section *Domaines et autorisations* :</span><span class="sxs-lookup"><span data-stu-id="6f4b2-147">In the *Domains and permissions* section:</span></span>

- <span data-ttu-id="6f4b2-148">Les *domaines à partir de vos onglets* doivent contenir votre URL ngrok sans le préfixe HTTPS - `<yourngrokurl>.ngrok.io/` .</span><span class="sxs-lookup"><span data-stu-id="6f4b2-148">The *Domains from your tabs* field should contain your ngrok URL without the HTTPS prefix - `<yourngrokurl>.ngrok.io/`.</span></span>

#### <a name="finish-test-and-distribute"></a><span data-ttu-id="6f4b2-149">Fin : Tester et distribuer</span><span class="sxs-lookup"><span data-stu-id="6f4b2-149">Finish: Test and distribute</span></span>

>[!IMPORTANT]
><span data-ttu-id="6f4b2-150">Dans le **champ Description** à droite, vous verrez l’avertissement suivant :</span><span class="sxs-lookup"><span data-stu-id="6f4b2-150">In the **Description** field on the right you'll see the following warning:</span></span>
>
><span data-ttu-id="6f4b2-151">&#9888; «**Le tableau « validDomains » ne peut** pas contenir un site de tunneling... »</span><span class="sxs-lookup"><span data-stu-id="6f4b2-151">&#9888; "**The 'validDomains' array cannot contain a tunneling site...**"</span></span>
>
><span data-ttu-id="6f4b2-152">Cet avertissement peut être ignoré lors du test de votre onglet.</span><span class="sxs-lookup"><span data-stu-id="6f4b2-152">This warning can be ignored while testing your tab.</span></span>

<span data-ttu-id="6f4b2-153">Dans la section *Tester et distribuer* :</span><span class="sxs-lookup"><span data-stu-id="6f4b2-153">In the *Test and distribute* section:</span></span>

- <span data-ttu-id="6f4b2-154">Sélectionnez **Installer**.</span><span class="sxs-lookup"><span data-stu-id="6f4b2-154">Select **Install**.</span></span>

- <span data-ttu-id="6f4b2-155">Dans la fenêtre pop-up Ajouter à une équipe ou un champ *de conversation,* entrez votre équipe et sélectionnez **Installer.**</span><span class="sxs-lookup"><span data-stu-id="6f4b2-155">In the pop-up window's *Add to a team or chat* field enter your team and select **Install**.</span></span>

- <span data-ttu-id="6f4b2-156">Dans la fenêtre pop-up suivante, choisissez le canal d’équipe où vous souhaitez que l’onglet s’affiche, puis **sélectionnez Configurer.**</span><span class="sxs-lookup"><span data-stu-id="6f4b2-156">In the next pop-up window choose the team channel where you would like the tab displayed and select **Set up**.</span></span>

- <span data-ttu-id="6f4b2-157">Dans la fenêtre pop-up finale, sélectionnez une valeur pour la page d’onglet (icône rouge ou grise), puis sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="6f4b2-157">In the final pop-up window select a value for the tab page (either a red or gray icon) and select **Save**.</span></span>

<span data-ttu-id="6f4b2-158">Pour afficher votre onglet, accédez à l’équipe sur qui vous l’avez installé et sélectionnez-le dans la barre d’onglets.</span><span class="sxs-lookup"><span data-stu-id="6f4b2-158">To view your tab, navigate to the team you installed it on, and select it from the tab bar.</span></span> <span data-ttu-id="6f4b2-159">La page que vous avez choisie lors de la configuration doit être affichée.</span><span class="sxs-lookup"><span data-stu-id="6f4b2-159">The page that you chose during configuration should be displayed.</span></span>
