---
title: Créer une page de configuration
author: laujan
description: comment créer une page de configuration
keywords: équipes onglets canal de groupe configurable
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: aeab1cf96d1e875db79d9143fefd0e46348f585a
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566683"
---
# <a name="create-a-configuration-page"></a><span data-ttu-id="056fa-104">Créer une page de configuration</span><span class="sxs-lookup"><span data-stu-id="056fa-104">Create a configuration page</span></span>

<span data-ttu-id="056fa-105">Une page de configuration est un type spécial de [page de contenu](content-page.md).</span><span class="sxs-lookup"><span data-stu-id="056fa-105">A configuration page is a special type of [content page](content-page.md).</span></span> <span data-ttu-id="056fa-106">Les utilisateurs configurent certains aspects de l’application Microsoft Teams’utilisation de la page de configuration et utilisent cette configuration dans le cadre des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="056fa-106">The users configure some aspects of the Microsoft Teams app using the configuration page and use that configuration as part of the following:</span></span>

* <span data-ttu-id="056fa-107">Onglet de chat de canal ou de groupe : Collectez des informations auprès des utilisateurs et définissez `contentUrl` la page de contenu à afficher.</span><span class="sxs-lookup"><span data-stu-id="056fa-107">A channel or group chat tab: Collect information from the users and set the `contentUrl` of the content page to display.</span></span>
* <span data-ttu-id="056fa-108">Une [extension de messagerie](~/messaging-extensions/what-are-messaging-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="056fa-108">A [messaging extension](~/messaging-extensions/what-are-messaging-extensions.md).</span></span>
* <span data-ttu-id="056fa-109">Un [connecteur Office 365 de travail](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md).</span><span class="sxs-lookup"><span data-stu-id="056fa-109">An [Office 365 Connector](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md).</span></span>

## <a name="configuring-a-channel-or-group-chat-tab"></a><span data-ttu-id="056fa-110">Configuration d’un canal ou d’un onglet de chat de groupe</span><span class="sxs-lookup"><span data-stu-id="056fa-110">Configuring a channel or group chat tab</span></span>

<span data-ttu-id="056fa-111">L’application doit faire référence [Microsoft Teams client JavaScript SDK et](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) appeler `microsoft.initialize()` .</span><span class="sxs-lookup"><span data-stu-id="056fa-111">The application must reference the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) and call `microsoft.initialize()`.</span></span> <span data-ttu-id="056fa-112">En outre, les URL utilisées doivent être sécurisées points de terminaison HTTPS et disponibles à partir du nuage.</span><span class="sxs-lookup"><span data-stu-id="056fa-112">Also, the URLs used must be secured HTTPS endpoints and available from the cloud.</span></span> 

### <a name="example"></a><span data-ttu-id="056fa-113">Exemple</span><span class="sxs-lookup"><span data-stu-id="056fa-113">Example</span></span>

<span data-ttu-id="056fa-114">Un exemple de page de configuration est affiché dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="056fa-114">An example of a configuration page is shown in the following image:</span></span> 

<img src="~/assets/images/tab-images/configuration-page.png" alt="Configuration page" width="400"/>

<span data-ttu-id="056fa-115">Le code correspondant pour la page de configuration est affiché dans la section suivante :</span><span class="sxs-lookup"><span data-stu-id="056fa-115">The corresponding code for configuration page is shown in the following section:</span></span>

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

<span data-ttu-id="056fa-116">Choisissez le **bouton Sélectionnez** gris **ou sélectionnez** rouge dans la page de configuration, pour afficher le contenu de l’onglet avec une icône grise ou rouge.</span><span class="sxs-lookup"><span data-stu-id="056fa-116">Choose either **Select Gray** or **Select Red** button in the configuration page, to display the tab content with a gray or red icon.</span></span> 

<span data-ttu-id="056fa-117">L’image suivante affiche le contenu de l’onglet avec icône grise :</span><span class="sxs-lookup"><span data-stu-id="056fa-117">The following image displays the tab content with gray icon:</span></span>

<img src="~/assets/images/tab-images/configure-tab-with-gray.png" alt="Configure tab with select gray" width="400"/>

<span data-ttu-id="056fa-118">L’image suivante affiche le contenu de l’onglet avec icône rouge :</span><span class="sxs-lookup"><span data-stu-id="056fa-118">The following image displays the tab content with red icon:</span></span>

<img src="~/assets/images/tab-images/configure-tab-with-red.png" alt="Configure tab with select red" width="400"/>

<span data-ttu-id="056fa-119">Le choix du bouton relatif déclenche ou `saveGray()` `saveRed()` , et invoque ce qui suit:</span><span class="sxs-lookup"><span data-stu-id="056fa-119">Choosing the relative button triggers either `saveGray()` or `saveRed()`, and invokes the following:</span></span>

1. <span data-ttu-id="056fa-120">`settings.setValidityState(true)`L’est réglé à vrai.</span><span class="sxs-lookup"><span data-stu-id="056fa-120">The `settings.setValidityState(true)` is set to true.</span></span>
1. <span data-ttu-id="056fa-121">Le `microsoftTeams.settings.registerOnSaveHandler()` gestionnaire d’événements est déclenché.</span><span class="sxs-lookup"><span data-stu-id="056fa-121">The `microsoftTeams.settings.registerOnSaveHandler()` event handler is triggered.</span></span>
1. <span data-ttu-id="056fa-122">Le **bouton Enregistrer** sur la page de configuration de l’application, téléchargé dans Teams, est activé.</span><span class="sxs-lookup"><span data-stu-id="056fa-122">The **Save** button on the app's configuration page, uploaded in Teams, is enabled.</span></span>

<span data-ttu-id="056fa-123">Le code de la page de configuration informe Teams que les exigences de configuration sont satisfaites et que l’installation peut se poursuivre.</span><span class="sxs-lookup"><span data-stu-id="056fa-123">The configuration page code informs the Teams that the configuration requirements are satisfied and the installation can proceed.</span></span> <span data-ttu-id="056fa-124">Lorsque l’utilisateur sélectionne **Enregistrer,** les paramètres de sont `settings.setSettings()` définis, tels que définis par `Settings` l’interface.</span><span class="sxs-lookup"><span data-stu-id="056fa-124">When the user selects **Save**, the parameters of `settings.setSettings()` are set, as defined by the `Settings` interface.</span></span> <span data-ttu-id="056fa-125">Pour plus d’informations, [Paramètres interface](/javascript/api/@microsoft/teams-js/_settings?view=msteams-client-js-latest&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="056fa-125">For more information, see [Settings interface](/javascript/api/@microsoft/teams-js/_settings?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="056fa-126">Dans la dernière étape, `saveEvent.notifySuccess()` est appelé à indiquer que l’URL de contenu a résolu avec succès.</span><span class="sxs-lookup"><span data-stu-id="056fa-126">In the last step, `saveEvent.notifySuccess()` is called to indicate that the content URL has successfully resolved.</span></span>

>[!NOTE]
>
>* <span data-ttu-id="056fa-127">Si vous enregistrez un gestionnaire d’enregistrement à `microsoftTeams.settings.registerOnSaveHandler()` l’aide, le rappel doit `saveEvent.notifySuccess()` `saveEvent.notifyFailure()` invoquer ou indiquer le résultat de la configuration.</span><span class="sxs-lookup"><span data-stu-id="056fa-127">If you register a save handler using `microsoftTeams.settings.registerOnSaveHandler()`, the callback must invoke `saveEvent.notifySuccess()` or `saveEvent.notifyFailure()` to indicate the outcome of the configuration.</span></span>
>* <span data-ttu-id="056fa-128">Si vous n’enregistrez pas un gestionnaire d’enregistrement, `saveEvent.notifySuccess()` l’appel est effectué automatiquement lorsque l’utilisateur sélectionne **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="056fa-128">If you don't register a save handler, the `saveEvent.notifySuccess()` call is made automatically when the user selects **Save**.</span></span>

### <a name="get-context-data-for-your-tab-settings"></a><span data-ttu-id="056fa-129">Obtenez des données context contextées pour les paramètres de vos onglets</span><span class="sxs-lookup"><span data-stu-id="056fa-129">Get context data for your tab settings</span></span>

<span data-ttu-id="056fa-130">Votre onglet peut nécessiter des informations contextuelles pour afficher du contenu pertinent.</span><span class="sxs-lookup"><span data-stu-id="056fa-130">Your tab might require contextual information to display relevant content.</span></span> <span data-ttu-id="056fa-131">Les informations contextuelles améliorent encore l’attrait de votre onglet en offrant une expérience utilisateur plus personnalisée.</span><span class="sxs-lookup"><span data-stu-id="056fa-131">Contextual information further enhances your tab's appeal by providing a more customized user experience.</span></span>

<span data-ttu-id="056fa-132">Pour plus d’informations sur les propriétés utilisées pour la configuration de l’onglet, voir [interface Context](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="056fa-132">For more information on the properties used for tab configuration, see [Context interface](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="056fa-133">Recueillir les valeurs des variables de données contextatives de deux façons suivantes :</span><span class="sxs-lookup"><span data-stu-id="056fa-133">Collect the values of context data variables in the following two ways:</span></span>

1. <span data-ttu-id="056fa-134">Insérez les espaces réservés de chaîne de requête d’URL dans votre `configurationURL` manifeste.</span><span class="sxs-lookup"><span data-stu-id="056fa-134">Insert URL query string placeholders in your manifest's `configurationURL`.</span></span>

1. <span data-ttu-id="056fa-135">Utilisez la [Teams SDK.](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})`</span><span class="sxs-lookup"><span data-stu-id="056fa-135">Use the [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})` method.</span></span>

#### <a name="insert-placeholders-in-the-configurationurl"></a><span data-ttu-id="056fa-136">Insérez les espaces réservés dans le `configurationUrl`</span><span class="sxs-lookup"><span data-stu-id="056fa-136">Insert placeholders in the `configurationUrl`</span></span>

<span data-ttu-id="056fa-137">Ajoutez des espaces réservés à l’interface context context à votre base `configurationUrl` .</span><span class="sxs-lookup"><span data-stu-id="056fa-137">Add context interface placeholders to your base `configurationUrl`.</span></span> <span data-ttu-id="056fa-138">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="056fa-138">For example:</span></span>

##### <a name="base-url"></a><span data-ttu-id="056fa-139">URL de base</span><span class="sxs-lookup"><span data-stu-id="056fa-139">Base URL</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config",
...
```

#### <a name="base-url-with-query-strings"></a><span data-ttu-id="056fa-140">URL de base avec chaînes de requêtes</span><span class="sxs-lookup"><span data-stu-id="056fa-140">Base URL with query strings</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config?team={teamId}&channel={channelId}&{locale}"
...
```

<span data-ttu-id="056fa-141">Après le téléchargement de votre page, le Teams les espaces réservés aux requêtes avec les valeurs pertinentes.</span><span class="sxs-lookup"><span data-stu-id="056fa-141">After your page uploads, the Teams updates the query string placeholders with relevant values.</span></span> <span data-ttu-id="056fa-142">Inclure la logique dans la page de configuration pour récupérer et utiliser ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="056fa-142">Include logic in the configuration page to retrieve and use those values.</span></span> <span data-ttu-id="056fa-143">Pour plus d’informations sur le travail avec les chaînes de requêtes URL, [consultez URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) dans MDN Web Docs. L’exemple suivant décrit la façon d’extraire une valeur de la `configurationUrl` propriété :</span><span class="sxs-lookup"><span data-stu-id="056fa-143">For more information on working with URL query strings, see [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) in MDN Web Docs. The following example describes the way to extract a value from the `configurationUrl` property:</span></span>

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

### <a name="use-the-getcontext-function-to-retrieve-context"></a><span data-ttu-id="056fa-144">Utilisez la `getContext()` fonction pour récupérer le contexte</span><span class="sxs-lookup"><span data-stu-id="056fa-144">Use the `getContext()` function to retrieve context</span></span>

<span data-ttu-id="056fa-145">La `microsoftTeams.getContext((context) => {})` fonction récupère [l’interface Context lorsqu’elle](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) est invoquée.</span><span class="sxs-lookup"><span data-stu-id="056fa-145">The `microsoftTeams.getContext((context) => {})` function retrieves the [Context interface](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) when invoked.</span></span> <span data-ttu-id="056fa-146">Ajoutez cette fonction à la page de configuration pour récupérer les valeurs de contexte :</span><span class="sxs-lookup"><span data-stu-id="056fa-146">Add this function to the configuration page to retrieve context values:</span></span>

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

## <a name="context-and-authentication"></a><span data-ttu-id="056fa-147">Contexte et authentification</span><span class="sxs-lookup"><span data-stu-id="056fa-147">Context and authentication</span></span>

 <span data-ttu-id="056fa-148">Authentifiez avant de permettre à un utilisateur de configurer votre application.</span><span class="sxs-lookup"><span data-stu-id="056fa-148">Authenticate before allowing a user to configure your app.</span></span> <span data-ttu-id="056fa-149">Dans le cas contraire, votre contenu peut inclure des sources qui ont leurs protocoles d’authentification.</span><span class="sxs-lookup"><span data-stu-id="056fa-149">Otherwise, your content might include sources that have their authentication protocols.</span></span> <span data-ttu-id="056fa-150">Pour plus d’informations, [voir Authentifier un utilisateur dans un onglet Microsoft Teams’utilisateur](~/tabs/how-to/authentication/auth-flow-tab.md). Utilisez les informations context contextées pour construire les urls de la page d’authentification et d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="056fa-150">For more information, see [Authenticate a user in a Microsoft Teams tab](~/tabs/how-to/authentication/auth-flow-tab.md). Use context information to construct the authentication requests and authorization page URLs.</span></span>
<span data-ttu-id="056fa-151">Assurez-vous que tous les domaines utilisés dans vos pages d’onglets sont répertoriés dans `manifest.json` le tableau et le `validDomains` tableau.</span><span class="sxs-lookup"><span data-stu-id="056fa-151">Ensure that all domains used in your tab pages are listed in the `manifest.json` and `validDomains` array.</span></span>

## <a name="modify-or-remove-a-tab"></a><span data-ttu-id="056fa-152">Modifier ou supprimer un onglet</span><span class="sxs-lookup"><span data-stu-id="056fa-152">Modify or remove a tab</span></span>

<span data-ttu-id="056fa-153">Les options de suppression prises en charge affinant davantage l’expérience utilisateur.</span><span class="sxs-lookup"><span data-stu-id="056fa-153">Supported removal options further refine the user experience.</span></span> <span data-ttu-id="056fa-154">Réglez la propriété de votre `canUpdateConfiguration` manifeste à , qui permet aux utilisateurs de `true` modifier, reconfigurer ou renommer un onglet de groupe ou de canal. Indiquez également ce qui arrive au contenu lorsqu’un onglet est supprimé, en incluant une page d’options de suppression dans l’application et en fixant une `removeUrl` valeur pour la propriété dans la  `setSettings()` configuration.</span><span class="sxs-lookup"><span data-stu-id="056fa-154">Set your manifest's `canUpdateConfiguration` property to `true`, that enables the users to modify, reconfigure, or rename a group or channel tab. Also, indicate what happens to the content when a tab is removed, by including a removal options page in the app and setting a value for the `removeUrl` property in the  `setSettings()` configuration.</span></span> <span data-ttu-id="056fa-155">L’utilisateur peut désinstaller les onglets personnels mais ne peut pas les modifier.</span><span class="sxs-lookup"><span data-stu-id="056fa-155">The user can uninstall the Personal tabs but cannot modify them.</span></span> <span data-ttu-id="056fa-156">Pour plus d’informations, [voir Créer une page de suppression pour votre onglet](~/tabs/how-to/create-tab-pages/removal-page.md).</span><span class="sxs-lookup"><span data-stu-id="056fa-156">For more information, see [Create a removal page for your tab](~/tabs/how-to/create-tab-pages/removal-page.md).</span></span>

<span data-ttu-id="056fa-157">Microsoft Teams configuration setSettings () pour la page de suppression :</span><span class="sxs-lookup"><span data-stu-id="056fa-157">Microsoft Teams setSettings() configuration for removal page:</span></span>

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add unique name here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "add website URL here //Required field for configurable tabs on Mobile Clients",
    removeUrl: "add removal page URL here"
});
```

## <a name="mobile-clients"></a><span data-ttu-id="056fa-158">Clients mobiles</span><span class="sxs-lookup"><span data-stu-id="056fa-158">Mobile clients</span></span>

<span data-ttu-id="056fa-159">Si vous choisissez d’avoir votre onglet canal ou groupe sur les Teams clients mobiles, la `setSettings()` configuration doit avoir une valeur pour la `websiteUrl` propriété.</span><span class="sxs-lookup"><span data-stu-id="056fa-159">If you choose to have your channel or group tab appear on the Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property.</span></span> <span data-ttu-id="056fa-160">Pour plus d’informations, consultez [les conseils pour les onglets sur mobile](~/tabs/design/tabs-mobile.md).</span><span class="sxs-lookup"><span data-stu-id="056fa-160">For more information, see [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md).</span></span>
