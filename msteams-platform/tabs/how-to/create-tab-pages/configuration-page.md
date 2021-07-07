---
title: Créer une page de configuration
author: surbhigupta
description: Comment créer une page de configuration
keywords: Canal de groupe onglets teams configurable
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 6f79480fb3ec6eb50de622e0b67b70e021d8cce7
ms.sourcegitcommit: a6253e89cb8c8c34d45b06e08c9668daeebc30a3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/06/2021
ms.locfileid: "53300311"
---
# <a name="create-a-configuration-page"></a><span data-ttu-id="e1bb2-104">Créer une page de configuration</span><span class="sxs-lookup"><span data-stu-id="e1bb2-104">Create a configuration page</span></span>

<span data-ttu-id="e1bb2-105">Une page de configuration est un type spécial de [page de contenu.](content-page.md)</span><span class="sxs-lookup"><span data-stu-id="e1bb2-105">A configuration page is a special type of [content page](content-page.md).</span></span> <span data-ttu-id="e1bb2-106">Les utilisateurs configurent certains aspects de l’application Microsoft Teams à l’aide de la page de configuration et utilisent cette configuration dans le cadre des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="e1bb2-106">The users configure some aspects of the Microsoft Teams app using the configuration page and use that configuration as part of the following:</span></span>

* <span data-ttu-id="e1bb2-107">Onglet de conversation de canal ou de groupe : recueillez des informations auprès des utilisateurs et définissez la page de contenu `contentUrl` à afficher.</span><span class="sxs-lookup"><span data-stu-id="e1bb2-107">A channel or group chat tab: Collect information from the users and set the `contentUrl` of the content page to be displayed.</span></span>
* <span data-ttu-id="e1bb2-108">Une [extension de messagerie](~/messaging-extensions/what-are-messaging-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="e1bb2-108">A [messaging extension](~/messaging-extensions/what-are-messaging-extensions.md).</span></span>
* <span data-ttu-id="e1bb2-109">Un [connecteur Office 365 .](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)</span><span class="sxs-lookup"><span data-stu-id="e1bb2-109">An [Office 365 Connector](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md).</span></span>

## <a name="configure-a-channel-or-group-chat-tab"></a><span data-ttu-id="e1bb2-110">Configurer un onglet de conversation de canal ou de groupe</span><span class="sxs-lookup"><span data-stu-id="e1bb2-110">Configure a channel or group chat tab</span></span>

<span data-ttu-id="e1bb2-111">L’application doit référencer [le Microsoft Teams SDK client JavaScript et](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) appeler `microsoft.initialize()` .</span><span class="sxs-lookup"><span data-stu-id="e1bb2-111">The application must reference the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) and call `microsoft.initialize()`.</span></span> <span data-ttu-id="e1bb2-112">Les URL utilisées doivent être sécurisées par des points de terminaison HTTPS et disponibles à partir du cloud.</span><span class="sxs-lookup"><span data-stu-id="e1bb2-112">The URLs used must be secured HTTPS endpoints and available from the cloud.</span></span>

### <a name="example"></a><span data-ttu-id="e1bb2-113">Exemple</span><span class="sxs-lookup"><span data-stu-id="e1bb2-113">Example</span></span>

<span data-ttu-id="e1bb2-114">Un exemple de page de configuration est illustré dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="e1bb2-114">An example of a configuration page is shown in the following image:</span></span>

<img src="~/assets/images/tab-images/configuration-page.png" alt="Configuration page" width="400"/>

<span data-ttu-id="e1bb2-115">Le code suivant est un exemple de code correspondant pour la page de configuration :</span><span class="sxs-lookup"><span data-stu-id="e1bb2-115">The following code is an example of corresponding code for the configuration page:</span></span>

```html
<head>
    <script src='https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js'></script>
</head>
<body>
    <button onclick="(document.getElementById('icon').src = '/images/iconGray.png'); colorClickGray()">Select Gray</button>
    <img id="icon" src="/images/teamsIcon.png" alt="icon" style="width:100px" />
    <button onclick="(document.getElementById('icon').src = '/images/iconRed.png'); colorClickRed()">Select Red</button>

    <script>
        microsoftTeams.initialize();
        let saveGray = () => {
            microsoftTeams.settings.registerOnSaveHandler((saveEvent) => {
                microsoftTeams.settings.setSettings({
                    websiteUrl: "https://yourWebsite.com",
                    contentUrl: "https://yourWebsite.com/gray",
                    entityId: "grayIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                saveEvent.notifySuccess();
            });
        }
        let saveRed = () => {
            microsoftTeams.settings.registerOnSaveHandler((saveEvent) => {
                microsoftTeams.settings.setSettings({
                    websiteUrl: "https://yourWebsite.com",
                    contentUrl: "https://yourWebsite.com/red",
                    entityId: "redIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                saveEvent.notifySuccess();
            });
        }

        let gr = document.getElementById("gray").style;
        let rd = document.getElementById("red").style;

        const colorClickGray = () => {
            gr.display = "block";
            rd.display = "none";
            microsoftTeams.settings.setValidityState(true);
            saveGray()
        }

        const colorClickRed = () => {
            rd.display = "block";
            gr.display = "none";
            microsoftTeams.settings.setValidityState(true);
            saveRed();
        }
    </script>
    ...
</body>
```

<span data-ttu-id="e1bb2-116">Choisissez le **bouton Sélectionner gris** ou **Rouge** dans la page de configuration pour afficher le contenu de l’onglet avec une icône grise ou rouge.</span><span class="sxs-lookup"><span data-stu-id="e1bb2-116">Choose either **Select Gray** or **Select Red** button in the configuration page, to display the tab content with a gray or red icon.</span></span>

<span data-ttu-id="e1bb2-117">L’image suivante affiche le contenu de l’onglet avec une icône grise :</span><span class="sxs-lookup"><span data-stu-id="e1bb2-117">The following image displays the tab content with a gray icon:</span></span>

<img src="~/assets/images/tab-images/configure-tab-with-gray.png" alt="Configure tab with select gray" width="400"/>

<span data-ttu-id="e1bb2-118">L’image suivante affiche le contenu de l’onglet avec une icône rouge :</span><span class="sxs-lookup"><span data-stu-id="e1bb2-118">The following image displays the tab content with a red icon:</span></span>

<img src="~/assets/images/tab-images/configure-tab-with-red.png" alt="Configure tab with select red" width="400"/>

<span data-ttu-id="e1bb2-119">Le choix du bouton approprié déclenche l’une `saveGray()` ou `saveRed()` l’autre des déclencheurs et appelle les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="e1bb2-119">Choosing the appropriate button triggers either `saveGray()` or `saveRed()`, and invokes the following:</span></span>

* <span data-ttu-id="e1bb2-120">Définir `settings.setValidityState(true)` sur true.</span><span class="sxs-lookup"><span data-stu-id="e1bb2-120">Set `settings.setValidityState(true)` to true.</span></span> 
* <span data-ttu-id="e1bb2-121">Le `microsoftTeams.settings.registerOnSaveHandler()` handler d’événements est déclenché.</span><span class="sxs-lookup"><span data-stu-id="e1bb2-121">The `microsoftTeams.settings.registerOnSaveHandler()` event handler is triggered.</span></span>
* <span data-ttu-id="e1bb2-122">**L’enregistrer** sur la page de configuration de l’application est activé.</span><span class="sxs-lookup"><span data-stu-id="e1bb2-122">**Save** on the app's configuration page, is enabled.</span></span>

<span data-ttu-id="e1bb2-123">Le code de la page de configuration Teams que les exigences de configuration sont satisfaites et que l’installation peut se poursuivre.</span><span class="sxs-lookup"><span data-stu-id="e1bb2-123">The configuration page code informs Teams that the configuration requirements are satisfied and the installation can proceed.</span></span> <span data-ttu-id="e1bb2-124">Lorsque l’utilisateur sélectionne **Enregistrer,** les paramètres `settings.setSettings()` sont définis, comme défini par l’interface. `Settings`</span><span class="sxs-lookup"><span data-stu-id="e1bb2-124">When the user selects **Save**, the parameters of `settings.setSettings()` are set, as defined by the `Settings` interface.</span></span> <span data-ttu-id="e1bb2-125">Pour plus d’informations, voir [l’interface des paramètres.](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="e1bb2-125">For more information, see [settings interface](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="e1bb2-126">`saveEvent.notifySuccess()` est appelée pour indiquer que l’URL de contenu a été résolue avec succès.</span><span class="sxs-lookup"><span data-stu-id="e1bb2-126">`saveEvent.notifySuccess()` is called to indicate that the content URL has successfully resolved.</span></span>

>[!NOTE]
>
>* <span data-ttu-id="e1bb2-127">Si vous inscrivez un handler d’enregistrement à l’aide de , le rappel doit appeler ou `microsoftTeams.settings.registerOnSaveHandler()` indiquer le résultat de la `saveEvent.notifySuccess()` `saveEvent.notifyFailure()` configuration.</span><span class="sxs-lookup"><span data-stu-id="e1bb2-127">If you register a save handler using `microsoftTeams.settings.registerOnSaveHandler()`, the callback must invoke `saveEvent.notifySuccess()` or `saveEvent.notifyFailure()` to indicate the outcome of the configuration.</span></span>
>* <span data-ttu-id="e1bb2-128">Si vous n’enregistrez pas de handler d’enregistrement, l’appel est effectué automatiquement lorsque `saveEvent.notifySuccess()` l’utilisateur sélectionne **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="e1bb2-128">If you do not register a save handler, the `saveEvent.notifySuccess()` call is made automatically when the user selects **Save**.</span></span>

### <a name="get-context-data-for-your-tab-settings"></a><span data-ttu-id="e1bb2-129">Obtenir des données de contexte pour les paramètres de l’onglet</span><span class="sxs-lookup"><span data-stu-id="e1bb2-129">Get context data for your tab settings</span></span>

<span data-ttu-id="e1bb2-130">Votre onglet nécessite des informations contextuelles pour afficher le contenu pertinent.</span><span class="sxs-lookup"><span data-stu-id="e1bb2-130">Your tab requires contextual information to display relevant content.</span></span> <span data-ttu-id="e1bb2-131">Les informations contextuelles améliorent davantage l’appel de votre onglet en offrant une expérience utilisateur plus personnalisée.</span><span class="sxs-lookup"><span data-stu-id="e1bb2-131">Contextual information further enhances your tab's appeal by providing a more customized user experience.</span></span>

<span data-ttu-id="e1bb2-132">Pour plus d’informations sur les propriétés utilisées pour la configuration de l’onglet, voir [l’interface de contexte.](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="e1bb2-132">For more information on the properties used for tab configuration, see [context interface](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="e1bb2-133">Collectez les valeurs des variables de données de contexte des deux manières suivantes :</span><span class="sxs-lookup"><span data-stu-id="e1bb2-133">Collect the values of context data variables in the following two ways:</span></span>

* <span data-ttu-id="e1bb2-134">Insérez des espaces de caractères de chaîne de requête d’URL dans le `configurationURL` manifeste.</span><span class="sxs-lookup"><span data-stu-id="e1bb2-134">Insert URL query string placeholders in your manifest's `configurationURL`.</span></span>

* <span data-ttu-id="e1bb2-135">Utilisez la [Teams SDK.](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})`</span><span class="sxs-lookup"><span data-stu-id="e1bb2-135">Use the [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})` method.</span></span>

#### <a name="insert-placeholders-in-the-configurationurl"></a><span data-ttu-id="e1bb2-136">Insérer des espaces réservé dans le `configurationUrl`</span><span class="sxs-lookup"><span data-stu-id="e1bb2-136">Insert placeholders in the `configurationUrl`</span></span>

<span data-ttu-id="e1bb2-137">Ajoutez des espaces réservé à l’interface de contexte à votre `configurationUrl` base.</span><span class="sxs-lookup"><span data-stu-id="e1bb2-137">Add context interface placeholders to your base `configurationUrl`.</span></span> <span data-ttu-id="e1bb2-138">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="e1bb2-138">For example:</span></span>

##### <a name="base-url"></a><span data-ttu-id="e1bb2-139">URL de base</span><span class="sxs-lookup"><span data-stu-id="e1bb2-139">Base URL</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config",
...
```

#### <a name="base-url-with-query-strings"></a><span data-ttu-id="e1bb2-140">URL de base avec chaînes de requête</span><span class="sxs-lookup"><span data-stu-id="e1bb2-140">Base URL with query strings</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config?team={teamId}&channel={channelId}&{locale}"
...
```

<span data-ttu-id="e1bb2-141">Une fois votre page téléchargée, Teams les espaces réservé de chaîne de requête avec les valeurs pertinentes.</span><span class="sxs-lookup"><span data-stu-id="e1bb2-141">After your page uploads, Teams updates the query string placeholders with relevant values.</span></span> <span data-ttu-id="e1bb2-142">Incluez la logique dans la page de configuration pour récupérer et utiliser ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="e1bb2-142">Include logic in the configuration page to retrieve and use those values.</span></span> <span data-ttu-id="e1bb2-143">Pour plus d’informations sur l’working with URL query strings, see [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) in MDN Web Docs. L’exemple de code suivant permet d’extraire une valeur de la `configurationUrl` propriété :</span><span class="sxs-lookup"><span data-stu-id="e1bb2-143">For more information on working with URL query strings, see [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) in MDN Web Docs. The following code example provides the way to extract a value from the `configurationUrl` property:</span></span>

```html
<script>
   microsoftTeams.initialize();
   const getId = () => {
        let urlParams = new URLSearchParams(document.location.search.substring(1));
        let blueTeamId = urlParams.get('team');
        return blueTeamId
    }
//For testing, you can invoke the following to view the pertinent value:
document.write(getId());
</script>
```

### <a name="use-the-getcontext-function-to-retrieve-context"></a><span data-ttu-id="e1bb2-144">Utiliser la `getContext()` fonction pour récupérer le contexte</span><span class="sxs-lookup"><span data-stu-id="e1bb2-144">Use the `getContext()` function to retrieve context</span></span>

<span data-ttu-id="e1bb2-145">La `microsoftTeams.getContext((context) => {})` fonction récupère [l’interface de contexte](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) lorsqu’elle est invoquée.</span><span class="sxs-lookup"><span data-stu-id="e1bb2-145">The `microsoftTeams.getContext((context) => {})` function retrieves the [context interface](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) when invoked.</span></span>

<span data-ttu-id="e1bb2-146">Le code suivant fournit un exemple d’ajout de cette fonction à la page de configuration pour récupérer des valeurs de contexte :</span><span class="sxs-lookup"><span data-stu-id="e1bb2-146">The following code provides an example of adding this function to the configuration page to retrieve context values:</span></span>

```html
<!-- `userPrincipalName` will render in the span with the id "user". -->

<span id="user"></span>
...
<script>
    microsoftTeams.getContext((context) =>{
        let userId = document.getElementById('user');
        userId.innerHTML = context.userPrincipalName;
    });
</script>
...
```

## <a name="context-and-authentication"></a><span data-ttu-id="e1bb2-147">Contexte et authentification</span><span class="sxs-lookup"><span data-stu-id="e1bb2-147">Context and authentication</span></span>

<span data-ttu-id="e1bb2-148">Authentifier avant d’autoriser un utilisateur à configurer votre application.</span><span class="sxs-lookup"><span data-stu-id="e1bb2-148">Authenticate before allowing a user to configure your app.</span></span> <span data-ttu-id="e1bb2-149">Dans le cas contraire, votre contenu peut inclure des sources qui ont leurs protocoles d’authentification.</span><span class="sxs-lookup"><span data-stu-id="e1bb2-149">Otherwise, your content might include sources that have their authentication protocols.</span></span> <span data-ttu-id="e1bb2-150">Pour plus d’informations, [voir authentifier un utilisateur dans un Microsoft Teams onglet .](~/tabs/how-to/authentication/auth-flow-tab.md) Utilisez les informations de contexte pour construire les demandes d’authentification et les URL de page d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="e1bb2-150">For more information, see [authenticate a user in a Microsoft Teams tab](~/tabs/how-to/authentication/auth-flow-tab.md). Use context information to construct the authentication requests and authorization page URLs.</span></span> <span data-ttu-id="e1bb2-151">Assurez-vous que tous les domaines utilisés dans vos pages d’onglets sont répertoriés dans le `manifest.json` tableau et dans `validDomains` celui-ci.</span><span class="sxs-lookup"><span data-stu-id="e1bb2-151">Ensure that all domains used in your tab pages are listed in the `manifest.json` and `validDomains` array.</span></span>

## <a name="modify-or-remove-a-tab"></a><span data-ttu-id="e1bb2-152">Modifier ou supprimer un onglet</span><span class="sxs-lookup"><span data-stu-id="e1bb2-152">Modify or remove a tab</span></span>

<span data-ttu-id="e1bb2-153">Définissez la propriété de votre manifeste sur , qui permet aux utilisateurs de modifier, reconfigurer ou renommer un canal `canUpdateConfiguration` ou un onglet de `true` groupe. Indiquez également ce qu’il advient du contenu lorsqu’un onglet est supprimé, en incluant une page d’options de suppression dans l’application et en fixant une valeur pour la propriété `removeUrl` dans la  `setSettings()` configuration.</span><span class="sxs-lookup"><span data-stu-id="e1bb2-153">Set your manifest's `canUpdateConfiguration` property to `true`, that enables the users to modify, reconfigure, or rename a channel or group tab. Also, indicate what happens to the content when a tab is removed, by including a removal options page in the app and setting a value for the `removeUrl` property in the  `setSettings()` configuration.</span></span> <span data-ttu-id="e1bb2-154">L’utilisateur peut désinstaller les onglets personnels, mais ne peut pas les modifier.</span><span class="sxs-lookup"><span data-stu-id="e1bb2-154">The user can uninstall personal tabs but cannot modify them.</span></span> <span data-ttu-id="e1bb2-155">Pour plus d’informations, [voir créer une page de suppression pour votre onglet.](~/tabs/how-to/create-tab-pages/removal-page.md)</span><span class="sxs-lookup"><span data-stu-id="e1bb2-155">For more information, see [create a removal page for your tab](~/tabs/how-to/create-tab-pages/removal-page.md).</span></span>

<span data-ttu-id="e1bb2-156">`setSettings()`Microsoft Teams configuration de la page de suppression :</span><span class="sxs-lookup"><span data-stu-id="e1bb2-156">Microsoft Teams `setSettings()` configuration for removal page:</span></span>

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add unique name here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "add website URL here //Required field for configurable tabs on Mobile Clients",
    removeUrl: "add removal page URL here"
});
```

## <a name="mobile-clients"></a><span data-ttu-id="e1bb2-157">Clients mobiles</span><span class="sxs-lookup"><span data-stu-id="e1bb2-157">Mobile clients</span></span>

<span data-ttu-id="e1bb2-158">Si vous choisissez que votre onglet de canal ou de groupe apparaisse sur les clients mobiles Teams, la configuration doit avoir `setSettings()` une valeur pour `websiteUrl` .</span><span class="sxs-lookup"><span data-stu-id="e1bb2-158">If you choose to have your channel or group tab appear on the Teams mobile clients, the `setSettings()` configuration must have a value for `websiteUrl`.</span></span> <span data-ttu-id="e1bb2-159">Pour plus d’informations, [voir les conseils pour les onglets sur mobile.](~/tabs/design/tabs-mobile.md)</span><span class="sxs-lookup"><span data-stu-id="e1bb2-159">For more information, see [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="e1bb2-160">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="e1bb2-160">See also</span></span>

* [<span data-ttu-id="e1bb2-161">Teams onglets</span><span class="sxs-lookup"><span data-stu-id="e1bb2-161">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="e1bb2-162">Créer un onglet personnel</span><span class="sxs-lookup"><span data-stu-id="e1bb2-162">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
* [<span data-ttu-id="e1bb2-163">Créer un onglet de canal ou de groupe</span><span class="sxs-lookup"><span data-stu-id="e1bb2-163">Create a channel or group tab</span></span>](~/tabs/how-to/create-channel-group-tab.md)
* [<span data-ttu-id="e1bb2-164">Créer une page de contenu</span><span class="sxs-lookup"><span data-stu-id="e1bb2-164">Create a content page</span></span>](~/tabs/how-to/create-tab-pages/content-page.md)
* [<span data-ttu-id="e1bb2-165">Onglets sur les appareils mobiles</span><span class="sxs-lookup"><span data-stu-id="e1bb2-165">Tabs on mobile</span></span>](~/tabs/design/tabs-mobile.md)

## <a name="next-step"></a><span data-ttu-id="e1bb2-166">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="e1bb2-166">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e1bb2-167">Créer une page de suppression pour votre onglet</span><span class="sxs-lookup"><span data-stu-id="e1bb2-167">Create a removal page for your tab</span></span>](~/tabs/how-to/create-tab-pages/removal-page.md)
