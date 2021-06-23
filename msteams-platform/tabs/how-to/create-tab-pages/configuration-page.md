---
title: Créer une page de configuration
author: surbhigupta
description: Comment créer une page de configuration
keywords: Canal de groupe onglets teams configurable
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 041ef78fcc6e3f5203842e808949e86e8dd3aae4
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069212"
---
# <a name="create-a-configuration-page"></a><span data-ttu-id="361a3-104">Créer une page de configuration</span><span class="sxs-lookup"><span data-stu-id="361a3-104">Create a configuration page</span></span>

<span data-ttu-id="361a3-105">Une page de configuration est un type spécial [de page de contenu.](content-page.md)</span><span class="sxs-lookup"><span data-stu-id="361a3-105">A configuration page is a special type of [content page](content-page.md).</span></span> <span data-ttu-id="361a3-106">Les utilisateurs configurent certains aspects de l’application Microsoft Teams à l’aide de la page de configuration et utilisent cette configuration dans le cadre des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="361a3-106">The users configure some aspects of the Microsoft Teams app using the configuration page and use that configuration as part of the following:</span></span>

* <span data-ttu-id="361a3-107">Onglet de conversation de canal ou de groupe : recueillez des informations auprès des utilisateurs et définissez `contentUrl` la page de contenu à afficher.</span><span class="sxs-lookup"><span data-stu-id="361a3-107">A channel or group chat tab: Collect information from the users and set the `contentUrl` of the content page to display.</span></span>
* <span data-ttu-id="361a3-108">Une [extension de messagerie](~/messaging-extensions/what-are-messaging-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="361a3-108">A [messaging extension](~/messaging-extensions/what-are-messaging-extensions.md).</span></span>
* <span data-ttu-id="361a3-109">Un [connecteur Office 365 .](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)</span><span class="sxs-lookup"><span data-stu-id="361a3-109">An [Office 365 Connector](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md).</span></span>

## <a name="configuring-a-channel-or-group-chat-tab"></a><span data-ttu-id="361a3-110">Configuration d’un onglet de conversation de canal ou de groupe</span><span class="sxs-lookup"><span data-stu-id="361a3-110">Configuring a channel or group chat tab</span></span>

<span data-ttu-id="361a3-111">L’application doit référencer [le Microsoft Teams SDK client JavaScript et](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) appeler `microsoft.initialize()` .</span><span class="sxs-lookup"><span data-stu-id="361a3-111">The application must reference the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) and call `microsoft.initialize()`.</span></span> <span data-ttu-id="361a3-112">En outre, les URL utilisées doivent être sécurisées par des points de terminaison HTTPS et disponibles à partir du cloud.</span><span class="sxs-lookup"><span data-stu-id="361a3-112">Also, the URLs used must be secured HTTPS endpoints and available from the cloud.</span></span> 

### <a name="example"></a><span data-ttu-id="361a3-113">Exemple</span><span class="sxs-lookup"><span data-stu-id="361a3-113">Example</span></span>

<span data-ttu-id="361a3-114">Un exemple de page de configuration est illustré dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="361a3-114">An example of a configuration page is shown in the following image:</span></span> 

<img src="~/assets/images/tab-images/configuration-page.png" alt="Configuration page" width="400"/>

<span data-ttu-id="361a3-115">Le code correspondant à la page de configuration est indiqué dans la section suivante :</span><span class="sxs-lookup"><span data-stu-id="361a3-115">The corresponding code for configuration page is shown in the following section:</span></span>

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
    </body>
...
```

<span data-ttu-id="361a3-116">Choisissez le **bouton Sélectionner gris** ou **Rouge** dans la page de configuration pour afficher le contenu de l’onglet avec une icône grise ou rouge.</span><span class="sxs-lookup"><span data-stu-id="361a3-116">Choose either **Select Gray** or **Select Red** button in the configuration page, to display the tab content with a gray or red icon.</span></span> 

<span data-ttu-id="361a3-117">L’image suivante affiche le contenu de l’onglet avec une icône grise :</span><span class="sxs-lookup"><span data-stu-id="361a3-117">The following image displays the tab content with gray icon:</span></span>

<img src="~/assets/images/tab-images/configure-tab-with-gray.png" alt="Configure tab with select gray" width="400"/>

<span data-ttu-id="361a3-118">L’image suivante affiche le contenu de l’onglet avec l’icône rouge :</span><span class="sxs-lookup"><span data-stu-id="361a3-118">The following image displays the tab content with red icon:</span></span>

<img src="~/assets/images/tab-images/configure-tab-with-red.png" alt="Configure tab with select red" width="400"/>

<span data-ttu-id="361a3-119">Le choix du bouton relatif déclenche l’une `saveGray()` ou `saveRed()` l’autre des déclencheurs et appelle les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="361a3-119">Choosing the relative button triggers either `saveGray()` or `saveRed()`, and invokes the following:</span></span>

1. <span data-ttu-id="361a3-120">La `settings.setValidityState(true)` valeur est true.</span><span class="sxs-lookup"><span data-stu-id="361a3-120">The `settings.setValidityState(true)` is set to true.</span></span>
1. <span data-ttu-id="361a3-121">Le `microsoftTeams.settings.registerOnSaveHandler()` handler d’événements est déclenché.</span><span class="sxs-lookup"><span data-stu-id="361a3-121">The `microsoftTeams.settings.registerOnSaveHandler()` event handler is triggered.</span></span>
1. <span data-ttu-id="361a3-122">Le **bouton** Enregistrer sur la page de configuration de l’application, téléchargé dans Teams, est activé.</span><span class="sxs-lookup"><span data-stu-id="361a3-122">The **Save** button on the app's configuration page, uploaded in Teams, is enabled.</span></span>

<span data-ttu-id="361a3-123">Le code de la page de configuration informe Teams que les exigences de configuration sont satisfaites et que l’installation peut se poursuivre.</span><span class="sxs-lookup"><span data-stu-id="361a3-123">The configuration page code informs the Teams that the configuration requirements are satisfied and the installation can proceed.</span></span> <span data-ttu-id="361a3-124">Lorsque l’utilisateur sélectionne **Enregistrer,** les paramètres `settings.setSettings()` sont définis, comme défini par l’interface. `Settings`</span><span class="sxs-lookup"><span data-stu-id="361a3-124">When the user selects **Save**, the parameters of `settings.setSettings()` are set, as defined by the `Settings` interface.</span></span> <span data-ttu-id="361a3-125">Pour plus d’informations, [voir Paramètres interface utilisateur.](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="361a3-125">For more information, see [Settings interface](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="361a3-126">Dans la dernière étape, `saveEvent.notifySuccess()` est appelée pour indiquer que l’URL de contenu a été correctement résolue.</span><span class="sxs-lookup"><span data-stu-id="361a3-126">In the last step, `saveEvent.notifySuccess()` is called to indicate that the content URL has successfully resolved.</span></span>

>[!NOTE]
>
>* <span data-ttu-id="361a3-127">Si vous inscrivez un handler d’enregistrement à l’aide de , le rappel doit appeler ou `microsoftTeams.settings.registerOnSaveHandler()` indiquer le résultat de la `saveEvent.notifySuccess()` `saveEvent.notifyFailure()` configuration.</span><span class="sxs-lookup"><span data-stu-id="361a3-127">If you register a save handler using `microsoftTeams.settings.registerOnSaveHandler()`, the callback must invoke `saveEvent.notifySuccess()` or `saveEvent.notifyFailure()` to indicate the outcome of the configuration.</span></span>
>* <span data-ttu-id="361a3-128">Si vous n’enregistrez pas de handler d’enregistrement, l’appel est effectué automatiquement lorsque l’utilisateur `saveEvent.notifySuccess()` sélectionne **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="361a3-128">If you don't register a save handler, the `saveEvent.notifySuccess()` call is made automatically when the user selects **Save**.</span></span>

### <a name="get-context-data-for-your-tab-settings"></a><span data-ttu-id="361a3-129">Obtenir des données de contexte pour les paramètres de l’onglet</span><span class="sxs-lookup"><span data-stu-id="361a3-129">Get context data for your tab settings</span></span>

<span data-ttu-id="361a3-130">Votre onglet peut nécessiter des informations contextuelles pour afficher du contenu pertinent.</span><span class="sxs-lookup"><span data-stu-id="361a3-130">Your tab might require contextual information to display relevant content.</span></span> <span data-ttu-id="361a3-131">Les informations contextuelles améliorent davantage l’appel de votre onglet en offrant une expérience utilisateur plus personnalisée.</span><span class="sxs-lookup"><span data-stu-id="361a3-131">Contextual information further enhances your tab's appeal by providing a more customized user experience.</span></span>

<span data-ttu-id="361a3-132">Pour plus d’informations sur les propriétés utilisées pour la configuration de l’onglet, voir [l’interface de contexte.](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="361a3-132">For more information on the properties used for tab configuration, see [Context interface](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="361a3-133">Collectez les valeurs des variables de données de contexte des deux manières suivantes :</span><span class="sxs-lookup"><span data-stu-id="361a3-133">Collect the values of context data variables in the following two ways:</span></span>

1. <span data-ttu-id="361a3-134">Insérez des espaces de caractères de chaîne de requête d’URL dans le `configurationURL` manifeste.</span><span class="sxs-lookup"><span data-stu-id="361a3-134">Insert URL query string placeholders in your manifest's `configurationURL`.</span></span>

1. <span data-ttu-id="361a3-135">Utilisez la [Teams SDK.](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})`</span><span class="sxs-lookup"><span data-stu-id="361a3-135">Use the [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})` method.</span></span>

#### <a name="insert-placeholders-in-the-configurationurl"></a><span data-ttu-id="361a3-136">Insérer des espaces réservé dans le `configurationUrl`</span><span class="sxs-lookup"><span data-stu-id="361a3-136">Insert placeholders in the `configurationUrl`</span></span>

<span data-ttu-id="361a3-137">Ajoutez des espaces réservé à l’interface de contexte à votre `configurationUrl` base.</span><span class="sxs-lookup"><span data-stu-id="361a3-137">Add context interface placeholders to your base `configurationUrl`.</span></span> <span data-ttu-id="361a3-138">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="361a3-138">For example:</span></span>

##### <a name="base-url"></a><span data-ttu-id="361a3-139">URL de base</span><span class="sxs-lookup"><span data-stu-id="361a3-139">Base URL</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config",
...
```

#### <a name="base-url-with-query-strings"></a><span data-ttu-id="361a3-140">URL de base avec chaînes de requête</span><span class="sxs-lookup"><span data-stu-id="361a3-140">Base URL with query strings</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config?team={teamId}&channel={channelId}&{locale}"
...
```

<span data-ttu-id="361a3-141">Une fois votre page téléchargée, la Teams les espaces réservé de chaîne de requête avec les valeurs pertinentes.</span><span class="sxs-lookup"><span data-stu-id="361a3-141">After your page uploads, the Teams updates the query string placeholders with relevant values.</span></span> <span data-ttu-id="361a3-142">Incluez la logique dans la page de configuration pour récupérer et utiliser ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="361a3-142">Include logic in the configuration page to retrieve and use those values.</span></span> <span data-ttu-id="361a3-143">Pour plus d’informations sur l’working with URL query strings, see [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) in MDN Web Docs. L’exemple suivant décrit la façon d’extraire une valeur de la `configurationUrl` propriété :</span><span class="sxs-lookup"><span data-stu-id="361a3-143">For more information on working with URL query strings, see [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) in MDN Web Docs. The following example describes the way to extract a value from the `configurationUrl` property:</span></span>

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

### <a name="use-the-getcontext-function-to-retrieve-context"></a><span data-ttu-id="361a3-144">Utiliser la `getContext()` fonction pour récupérer le contexte</span><span class="sxs-lookup"><span data-stu-id="361a3-144">Use the `getContext()` function to retrieve context</span></span>

<span data-ttu-id="361a3-145">La `microsoftTeams.getContext((context) => {})` fonction récupère [l’interface Context](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) lorsqu’elle est invoquée.</span><span class="sxs-lookup"><span data-stu-id="361a3-145">The `microsoftTeams.getContext((context) => {})` function retrieves the [Context interface](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) when invoked.</span></span> <span data-ttu-id="361a3-146">Ajoutez cette fonction à la page de configuration pour récupérer les valeurs de contexte :</span><span class="sxs-lookup"><span data-stu-id="361a3-146">Add this function to the configuration page to retrieve context values:</span></span>

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

## <a name="context-and-authentication"></a><span data-ttu-id="361a3-147">Contexte et authentification</span><span class="sxs-lookup"><span data-stu-id="361a3-147">Context and authentication</span></span>

 <span data-ttu-id="361a3-148">Authentifier avant d’autoriser un utilisateur à configurer votre application.</span><span class="sxs-lookup"><span data-stu-id="361a3-148">Authenticate before allowing a user to configure your app.</span></span> <span data-ttu-id="361a3-149">Dans le cas contraire, votre contenu peut inclure des sources qui ont leurs protocoles d’authentification.</span><span class="sxs-lookup"><span data-stu-id="361a3-149">Otherwise, your content might include sources that have their authentication protocols.</span></span> <span data-ttu-id="361a3-150">Pour plus d’informations, [voir Authentifier un](~/tabs/how-to/authentication/auth-flow-tab.md)utilisateur dans un Microsoft Teams onglet . Utilisez les informations de contexte pour construire les demandes d’authentification et les URL de page d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="361a3-150">For more information, see [Authenticate a user in a Microsoft Teams tab](~/tabs/how-to/authentication/auth-flow-tab.md). Use context information to construct the authentication requests and authorization page URLs.</span></span>
<span data-ttu-id="361a3-151">Assurez-vous que tous les domaines utilisés dans vos pages d’onglets sont répertoriés dans le `manifest.json` tableau et dans `validDomains` celui-ci.</span><span class="sxs-lookup"><span data-stu-id="361a3-151">Ensure that all domains used in your tab pages are listed in the `manifest.json` and `validDomains` array.</span></span>

## <a name="modify-or-remove-a-tab"></a><span data-ttu-id="361a3-152">Modifier ou supprimer un onglet</span><span class="sxs-lookup"><span data-stu-id="361a3-152">Modify or remove a tab</span></span>

<span data-ttu-id="361a3-153">Les options de suppression prise en charge améliorent davantage l’expérience utilisateur.</span><span class="sxs-lookup"><span data-stu-id="361a3-153">Supported removal options further refine the user experience.</span></span> <span data-ttu-id="361a3-154">Définissez la propriété de votre manifeste sur , qui permet aux utilisateurs de modifier, reconfigurer ou renommer un onglet de groupe `canUpdateConfiguration` `true` ou de canal. Indiquez également ce qu’il advient du contenu lorsqu’un onglet est supprimé, en incluant une page d’options de suppression dans l’application et en fixant une valeur pour la propriété `removeUrl` dans la  `setSettings()` configuration.</span><span class="sxs-lookup"><span data-stu-id="361a3-154">Set your manifest's `canUpdateConfiguration` property to `true`, that enables the users to modify, reconfigure, or rename a group or channel tab. Also, indicate what happens to the content when a tab is removed, by including a removal options page in the app and setting a value for the `removeUrl` property in the  `setSettings()` configuration.</span></span> <span data-ttu-id="361a3-155">L’utilisateur peut désinstaller les onglets Personnels, mais ne peut pas les modifier.</span><span class="sxs-lookup"><span data-stu-id="361a3-155">The user can uninstall the Personal tabs but cannot modify them.</span></span> <span data-ttu-id="361a3-156">Pour plus d’informations, [voir Créer une page de suppression pour votre onglet.](~/tabs/how-to/create-tab-pages/removal-page.md)</span><span class="sxs-lookup"><span data-stu-id="361a3-156">For more information, see [Create a removal page for your tab](~/tabs/how-to/create-tab-pages/removal-page.md).</span></span>

<span data-ttu-id="361a3-157">Microsoft Teams configuration setSettings() pour la page de suppression :</span><span class="sxs-lookup"><span data-stu-id="361a3-157">Microsoft Teams setSettings() configuration for removal page:</span></span>

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add unique name here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "add website URL here //Required field for configurable tabs on Mobile Clients",
    removeUrl: "add removal page URL here"
});
```

## <a name="mobile-clients"></a><span data-ttu-id="361a3-158">Clients mobiles</span><span class="sxs-lookup"><span data-stu-id="361a3-158">Mobile clients</span></span>

<span data-ttu-id="361a3-159">Si vous choisissez que votre onglet de canal ou de groupe apparaisse sur les clients mobiles Teams, la configuration doit avoir `setSettings()` une valeur pour `websiteUrl` .</span><span class="sxs-lookup"><span data-stu-id="361a3-159">If you choose to have your channel or group tab appear on the Teams mobile clients, the `setSettings()` configuration must have a value for `websiteUrl`.</span></span> <span data-ttu-id="361a3-160">Pour plus d’informations, [voir les conseils pour les onglets sur mobile.](~/tabs/design/tabs-mobile.md)</span><span class="sxs-lookup"><span data-stu-id="361a3-160">For more information, see [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md).</span></span>
