## <a name="update-your-application"></a><span data-ttu-id="b2c5a-101">Mettre à jour votre application</span><span class="sxs-lookup"><span data-stu-id="b2c5a-101">Update your application</span></span>

### <a name="_layoutcshtml"></a><span data-ttu-id="b2c5a-102">_Layout. cshtml</span><span class="sxs-lookup"><span data-stu-id="b2c5a-102">_Layout.cshtml</span></span>

<span data-ttu-id="b2c5a-103">Pour que votre onglet s’affiche dans Teams, vous devez inclure le **Kit de développement logiciel (SDK) JavaScript client Microsoft teams** et inclure un appel à `microsoftTeams.initialize()` après le chargement de votre page.</span><span class="sxs-lookup"><span data-stu-id="b2c5a-103">For your tab to display in Teams, you must include the **Microsoft Teams JavaScript client SDK** and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="b2c5a-104">Voici comment votre onglet et l’application teams communiquent :</span><span class="sxs-lookup"><span data-stu-id="b2c5a-104">This is how your tab and the Teams app communicate:</span></span>

- <span data-ttu-id="b2c5a-105">Naviguez jusqu’au dossier **partagé** , ouvrez **_Layout. cshtml**et ajoutez ce qui suit à `<head>` la section des balises :</span><span class="sxs-lookup"><span data-stu-id="b2c5a-105">Navigate to the **Shared** folder, open **_Layout.cshtml**, and add the following to the `<head>` tags section:</span></span>

```html
`<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.4.1.min.js"></script>`
`<script src="https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js"></script>`
```

### <a name="personaltabcshtml"></a><span data-ttu-id="b2c5a-106">PersonalTab. cshtml</span><span class="sxs-lookup"><span data-stu-id="b2c5a-106">PersonalTab.cshtml</span></span>

<span data-ttu-id="b2c5a-107">Ouvrez **PersonalTab. cshtml** et mettez à jour `<script>` les balises `microsoftTeams.initialize()`incorporées en appelant.</span><span class="sxs-lookup"><span data-stu-id="b2c5a-107">Open **PersonalTab.cshtml** and update the embedded `<script>` tags by calling `microsoftTeams.initialize()`.</span></span>

<span data-ttu-id="b2c5a-108">Veillez à enregistrer votre mise à jour de *PersonalTab. cshtml*.</span><span class="sxs-lookup"><span data-stu-id="b2c5a-108">Make sure to save your updated *PersonalTab.cshtml*.</span></span>