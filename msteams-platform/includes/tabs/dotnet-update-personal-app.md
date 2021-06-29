## <a name="update-your-application"></a><span data-ttu-id="73384-101">Mettre à jour votre application</span><span class="sxs-lookup"><span data-stu-id="73384-101">Update your application</span></span>

### <a name="_layoutcshtml"></a><span data-ttu-id="73384-102">_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="73384-102">_Layout.cshtml</span></span>

<span data-ttu-id="73384-103">Pour que votre onglet s’affiche dans Teams, vous devez inclure le **SDK client JavaScript Microsoft Teams** et inclure un appel après le chargement de `microsoftTeams.initialize()` votre page.</span><span class="sxs-lookup"><span data-stu-id="73384-103">For your tab to display in Teams, you must include the **Microsoft Teams JavaScript client SDK** and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="73384-104">Voici comment votre onglet et l’application Teams communiquent :</span><span class="sxs-lookup"><span data-stu-id="73384-104">This is how your tab and the Teams app communicate:</span></span>

<span data-ttu-id="73384-105">Go to the **Shared** folder, open **_Layout.cshtml**, and add the following to the `<head>` tags section:</span><span class="sxs-lookup"><span data-stu-id="73384-105">Go to the **Shared** folder, open **_Layout.cshtml**, and add the following to the `<head>` tags section:</span></span>

```html
<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>
<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>
```

### <a name="personaltabcshtml"></a><span data-ttu-id="73384-106">PersonalTab.cshtml</span><span class="sxs-lookup"><span data-stu-id="73384-106">PersonalTab.cshtml</span></span>

<span data-ttu-id="73384-107">Ouvrez **PersonalTab.cshtml** et mettez à jour les `<script>` balises incorporées en appelant `microsoftTeams.initialize()` .</span><span class="sxs-lookup"><span data-stu-id="73384-107">Open **PersonalTab.cshtml** and update the embedded `<script>` tags by calling `microsoftTeams.initialize()`.</span></span>

<span data-ttu-id="73384-108">Veillez à enregistrer votre **fichier PersonalTab.cshtml** mis à jour.</span><span class="sxs-lookup"><span data-stu-id="73384-108">Ensure you save your updated **PersonalTab.cshtml** file.</span></span>