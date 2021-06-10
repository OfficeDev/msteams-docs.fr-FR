## <a name="update-your-application"></a><span data-ttu-id="2bd80-101">Mettre à jour votre application</span><span class="sxs-lookup"><span data-stu-id="2bd80-101">Update your application</span></span>

### <a name="_layoutcshtml"></a><span data-ttu-id="2bd80-102">_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="2bd80-102">_Layout.cshtml</span></span>

<span data-ttu-id="2bd80-103">Pour que votre onglet s’affiche dans Teams, vous devez inclure le **SDK client JavaScript Microsoft Teams** et inclure un appel après le chargement de `microsoftTeams.initialize()` votre page.</span><span class="sxs-lookup"><span data-stu-id="2bd80-103">For your tab to display in Teams, you must include the **Microsoft Teams JavaScript client SDK** and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="2bd80-104">Voici comment votre onglet et l’application Teams communiquent :</span><span class="sxs-lookup"><span data-stu-id="2bd80-104">This is how your tab and the Teams app communicate:</span></span>

- <span data-ttu-id="2bd80-105">Accédez au **dossier** partagé, **ouvrez _Layout.cshtml** et ajoutez ce qui suit à la `<head>` section des balises :</span><span class="sxs-lookup"><span data-stu-id="2bd80-105">Navigate to the **Shared** folder, open **_Layout.cshtml**, and add the following to the `<head>` tags section:</span></span>

    ```html
    `<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>`
    `<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>`
    ```

### <a name="personaltabcshtml"></a><span data-ttu-id="2bd80-106">PersonalTab.cshtml</span><span class="sxs-lookup"><span data-stu-id="2bd80-106">PersonalTab.cshtml</span></span>

<span data-ttu-id="2bd80-107">Ouvrez **PersonalTab.cshtml** et mettez à jour les `<script>` balises incorporées en appelant `microsoftTeams.initialize()` .</span><span class="sxs-lookup"><span data-stu-id="2bd80-107">Open **PersonalTab.cshtml** and update the embedded `<script>` tags by calling `microsoftTeams.initialize()`.</span></span>

<span data-ttu-id="2bd80-108">Veillez à enregistrer votre **PersonalTab.cshtml** mis à jour.</span><span class="sxs-lookup"><span data-stu-id="2bd80-108">Make sure to save your updated **PersonalTab.cshtml**.</span></span>