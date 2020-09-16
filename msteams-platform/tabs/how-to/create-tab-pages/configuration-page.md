---
title: Créer une page de configuration
author: laujan
description: procédure de création d’une page de configuration
keywords: onglet teams groupe de canaux configurable
ms.topic: conceptualF
ms.author: lajanuar
ms.openlocfilehash: 6288fc8c296ebf0aa85ffe8e08234e5faf22a1ef
ms.sourcegitcommit: e8dfcb167274e996395b77d65999991a18f2051a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/15/2020
ms.locfileid: "47819024"
---
# <a name="create-a-configuration-page"></a><span data-ttu-id="411e9-104">Créer une page de configuration</span><span class="sxs-lookup"><span data-stu-id="411e9-104">Create a configuration page</span></span>

<span data-ttu-id="411e9-105">Une page de configuration est un type spécial de [page de contenu](content-page.md) qui permet à vos utilisateurs de configurer certains aspects de votre application de teams.</span><span class="sxs-lookup"><span data-stu-id="411e9-105">A configuration page is a special type of [content page](content-page.md) that allows your users to configure some aspect of your Teams app.</span></span> <span data-ttu-id="411e9-106">En règle générale, ces éléments sont utilisés dans les cas suivants :</span><span class="sxs-lookup"><span data-stu-id="411e9-106">Typically these are used as part of:</span></span>

* <span data-ttu-id="411e9-107">Onglet de conversation de canal ou de groupe : la page de configuration vous permet de recueillir des informations auprès de vos utilisateurs et de définir la `contentUrl` page de contenu à afficher.</span><span class="sxs-lookup"><span data-stu-id="411e9-107">A channel or group chat tab - The configuration page allows you to collect information from your users and set the `contentUrl` of the content page to display.</span></span>
* <span data-ttu-id="411e9-108">Une [extension de messagerie](~/messaging-extensions/what-are-messaging-extensions.md)</span><span class="sxs-lookup"><span data-stu-id="411e9-108">A [messaging extension](~/messaging-extensions/what-are-messaging-extensions.md)</span></span>
* <span data-ttu-id="411e9-109">Un [Connecteur Office 365](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)</span><span class="sxs-lookup"><span data-stu-id="411e9-109">A [Office 365 Connector](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)</span></span>

## <a name="configuring-a-channel-or-group-chat-tab"></a><span data-ttu-id="411e9-110">Configuration d’un onglet de conversation de canal ou de groupe</span><span class="sxs-lookup"><span data-stu-id="411e9-110">Configuring a channel or group chat tab</span></span>

<span data-ttu-id="411e9-111">Une page de configuration informe la page de contenu de la façon dont elle doit s’afficher.</span><span class="sxs-lookup"><span data-stu-id="411e9-111">A configuration page informs the content page how it should render.</span></span> <span data-ttu-id="411e9-112">Votre application doit référencer le [Kit de développement logiciel (SDK) du client JavaScript Microsoft teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) et appeler `microsoft.initialize()` .</span><span class="sxs-lookup"><span data-stu-id="411e9-112">Your application must reference the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) and call `microsoft.initialize()`.</span></span> <span data-ttu-id="411e9-113">En outre, vos URL doivent être des points de terminaison HTTPs sécurisés et disponibles dans le Cloud.</span><span class="sxs-lookup"><span data-stu-id="411e9-113">Additionally, your URLs must be secure HTTPS endpoints and available from the cloud.</span></span> <span data-ttu-id="411e9-114">Vous trouverez ci-dessous un exemple de page de configuration.</span><span class="sxs-lookup"><span data-stu-id="411e9-114">Below is a configuration page example.</span></span>

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

<span data-ttu-id="411e9-115">Ici, l’utilisateur voit apparaître deux cases d’option, **Sélectionner le gris** ou le **rouge** pour afficher le contenu de l’onglet avec une icône rouge ou grise.</span><span class="sxs-lookup"><span data-stu-id="411e9-115">Here, the user is presented with two option buttons, **Select Gray** or **Select Red** to display the tab content with either a red or gray icon.</span></span> <span data-ttu-id="411e9-116">Le choix du bouton relatif déclenche `saveGray()` ou `saveRed()` l’appel des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="411e9-116">Choosing the relative button fires `saveGray()` or `saveRed()` and invokes the following:</span></span>

1. <span data-ttu-id="411e9-117">`settings.setValidityState(true)`Est défini sur true.</span><span class="sxs-lookup"><span data-stu-id="411e9-117">The `settings.setValidityState(true)` is set to true.</span></span>
1. <span data-ttu-id="411e9-118">Le `microsoftTeams.settings.registerOnSaveHandler()` Gestionnaire d’événements est déclenché.</span><span class="sxs-lookup"><span data-stu-id="411e9-118">The `microsoftTeams.settings.registerOnSaveHandler()` event handler is triggered.</span></span>
1. <span data-ttu-id="411e9-119">Le bouton **Enregistrer** de la page de configuration de l’application, chargé dans Teams, est activé.</span><span class="sxs-lookup"><span data-stu-id="411e9-119">The **Save** button on the app's configuration page, uploaded in Teams, is enabled.</span></span>

<span data-ttu-id="411e9-120">Ce code permet aux équipes de reconnaître que les exigences de configuration ont été satisfaites et que l’installation peut être effectuée.</span><span class="sxs-lookup"><span data-stu-id="411e9-120">This code lets Teams know that the configuration requirements have been satisfied and the installation can proceed.</span></span> <span data-ttu-id="411e9-121">Lors de l' **enregistrement**, les paramètres de `settings.setSettings()` sont définis, comme défini par l' `Settings` interface, pour l’instance actuelle (voir [interface des paramètres](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest) ).</span><span class="sxs-lookup"><span data-stu-id="411e9-121">On **Save**, the parameters of `settings.setSettings()` are set, as defined by the `Settings` interface, for the current instance (See [Settings interface](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest) ).</span></span> <span data-ttu-id="411e9-122">Enfin, `saveEvent.notifySuccess()` est appelé pour indiquer que l’URL de contenu a été résolue avec succès.</span><span class="sxs-lookup"><span data-stu-id="411e9-122">Finally, `saveEvent.notifySuccess()` is called to indicate that the content URL has successfully resolved.</span></span>

>[!NOTE]
>
>* <span data-ttu-id="411e9-123">Si un gestionnaire d’enregistrement a été inscrit à l’aide de `microsoftTeams.settings.registerOnSaveHandler()` , le rappel doit appeler `saveEvent.notifySuccess()` ou `saveEvent.notifyFailure()` pour indiquer le résultat de la configuration.</span><span class="sxs-lookup"><span data-stu-id="411e9-123">If a save handler was registered using `microsoftTeams.settings.registerOnSaveHandler()`, the callback must invoke `saveEvent.notifySuccess()` or `saveEvent.notifyFailure()` to indicate the outcome of the configuration.</span></span>
>* <span data-ttu-id="411e9-124">Si aucun gestionnaire d’enregistrement n’a été enregistré, l' `saveEvent.notifySuccess()` appel est automatiquement effectué dès que l’utilisateur sélectionne le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="411e9-124">If no save handler was registered, the `saveEvent.notifySuccess()` call is automatically made immediately upon the user selecting the **Save** button.</span></span>

### <a name="get-context-data-for-your-tab-settings"></a><span data-ttu-id="411e9-125">Obtenir les données de contexte pour les paramètres de votre onglet</span><span class="sxs-lookup"><span data-stu-id="411e9-125">Get context data for your tab settings</span></span>

<span data-ttu-id="411e9-126">Votre onglet peut nécessiter des informations contextuelles pour afficher le contenu pertinent.</span><span class="sxs-lookup"><span data-stu-id="411e9-126">Your tab might require contextual information to display relevant content.</span></span> <span data-ttu-id="411e9-127">Les informations contextuelles peuvent améliorer davantage l’attrait de votre onglet en fournissant une expérience utilisateur plus personnalisée.</span><span class="sxs-lookup"><span data-stu-id="411e9-127">Contextual information can further enhance your tab's appeal by providing a more customized user experience.</span></span>

<span data-ttu-id="411e9-128">L' [interface de contexte](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest) teams définit les propriétés qui peuvent être utilisées pour votre configuration d’onglets.</span><span class="sxs-lookup"><span data-stu-id="411e9-128">The Teams [Context interface](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest) defines the properties that can be used for your tab configuration.</span></span> <span data-ttu-id="411e9-129">Vous pouvez collecter les valeurs des variables de données de contexte de deux façons :</span><span class="sxs-lookup"><span data-stu-id="411e9-129">You can collect the values of context data variables in two ways:</span></span>

1. <span data-ttu-id="411e9-130">Insérez des espaces réservés de chaîne de requête d’URL dans votre manifeste `configurationURL` .</span><span class="sxs-lookup"><span data-stu-id="411e9-130">Insert URL query string placeholders in your manifest's `configurationURL`.</span></span>

1. <span data-ttu-id="411e9-131">Utilisez la méthode du [Kit de développement logiciel teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) `microsoftTeams.getContext((context) =>{}` .</span><span class="sxs-lookup"><span data-stu-id="411e9-131">Use the [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) `microsoftTeams.getContext((context) =>{}` method.</span></span>

#### <a name="insert-placeholders-in-the-configurationurl"></a><span data-ttu-id="411e9-132">Insérer des espaces réservés dans le `configurationURL`</span><span class="sxs-lookup"><span data-stu-id="411e9-132">Insert placeholders in the `configurationURL`</span></span>

<span data-ttu-id="411e9-133">Des espaces réservés d’interface de contexte peuvent être ajoutés à votre base `configurationUrl` .</span><span class="sxs-lookup"><span data-stu-id="411e9-133">Context interface placeholders can be added to your base `configurationUrl`.</span></span> <span data-ttu-id="411e9-134">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="411e9-134">For example:</span></span>

##### <a name="base-url"></a><span data-ttu-id="411e9-135">URL de base</span><span class="sxs-lookup"><span data-stu-id="411e9-135">Base Url</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config",
...
```

#### <a name="base-url-with-query-strings"></a><span data-ttu-id="411e9-136">URL de base avec des chaînes de requête</span><span class="sxs-lookup"><span data-stu-id="411e9-136">Base URL with query strings</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config?team={teamId}&channel={channelId}&{locale}"
...
```

<span data-ttu-id="411e9-137">Une fois que votre page a été téléchargée, les espaces réservés de chaîne de requête sont mis à jour par teams avec les valeurs pertinentes.</span><span class="sxs-lookup"><span data-stu-id="411e9-137">After your page has uploaded, the query string placeholders will be updated by Teams with the relevant values.</span></span> <span data-ttu-id="411e9-138">Vous pouvez inclure une logique dans votre page de configuration pour récupérer et utiliser ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="411e9-138">You can include logic in your configuration page to retrieve and use those values.</span></span> <span data-ttu-id="411e9-139">Pour plus d’informations sur l’utilisation des chaînes de requête d’URL, voir [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) dans notification Web docs. Voici un exemple d’extraction d’une valeur à partir de la propriété ci-dessus `configurationURL` :</span><span class="sxs-lookup"><span data-stu-id="411e9-139">For more information on working with URL query strings see [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) in MDN web docs. Here is an example of how to extract a value from the above `configurationURL` property:</span></span>

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

### <a name="use-the-getcontext-function-to-retrieve-context"></a><span data-ttu-id="411e9-140">Utiliser la `getContext()` fonction pour extraire le contexte</span><span class="sxs-lookup"><span data-stu-id="411e9-140">Use the `getContext()` function to retrieve context</span></span>

<span data-ttu-id="411e9-141">Lorsqu’elle est appelée, la `microsoftTeams.getContext((context) => {})` fonction récupère l' [interface de contexte](/javascript/api/@microsoft/teams-js//microsoftteams.context?view=msteams-client-js-latest).</span><span class="sxs-lookup"><span data-stu-id="411e9-141">When invoked, the `microsoftTeams.getContext((context) => {})` function retrieves the [Context interface](/javascript/api/@microsoft/teams-js//microsoftteams.context?view=msteams-client-js-latest).</span></span> <span data-ttu-id="411e9-142">Vous pouvez ajouter cette fonction à votre page de configuration pour extraire les valeurs de contexte :</span><span class="sxs-lookup"><span data-stu-id="411e9-142">You can add this function to your configuration page to retrieve context values:</span></span>

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

## <a name="context-and-authentication"></a><span data-ttu-id="411e9-143">Contexte et authentification</span><span class="sxs-lookup"><span data-stu-id="411e9-143">Context and Authentication</span></span>

<span data-ttu-id="411e9-144">Vous devrez peut-être demander une authentification avant d’autoriser un utilisateur à configurer votre application ou votre contenu peut inclure des sources ayant leurs propres protocoles d’authentification.</span><span class="sxs-lookup"><span data-stu-id="411e9-144">You might require authentication before allowing a user to configure your app or your content might include sources that have their own authentication protocols.</span></span> <span data-ttu-id="411e9-145">Voir [authentifier un utilisateur dans une application Microsoft teams](~/tabs/how-to/authentication/auth-flow-tab.md) les informations de contexte peuvent être utilisées pour vous aider à créer des demandes d’authentification et des URL de page d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="411e9-145">See [Authenticate a user in a Microsoft Teams tab](~/tabs/how-to/authentication/auth-flow-tab.md) Context information can be used to help construct authentication requests and authorization page URLs.</span></span>
<span data-ttu-id="411e9-146">Assurez-vous que tous les domaines utilisés dans vos pages d’onglets sont répertoriés dans le `manifest.json` `validDomains` tableau.</span><span class="sxs-lookup"><span data-stu-id="411e9-146">Make sure that all domains used in your tab pages are listed in the `manifest.json` `validDomains` array.</span></span>

## <a name="modify-or-remove-a-tab"></a><span data-ttu-id="411e9-147">Modifier ou supprimer un onglet</span><span class="sxs-lookup"><span data-stu-id="411e9-147">Modify or remove a tab</span></span>

<span data-ttu-id="411e9-148">Les options de suppression prises en charge peuvent affiner l’expérience utilisateur.</span><span class="sxs-lookup"><span data-stu-id="411e9-148">Supported removal options can further refine the user experience.</span></span> <span data-ttu-id="411e9-149">Vous pouvez permettre aux utilisateurs de modifier, de reconfigurer ou de renommer un onglet de groupe/canal en définissant la propriété de votre manifeste `canUpdateConfiguration` sur `true` .</span><span class="sxs-lookup"><span data-stu-id="411e9-149">You can enable users to modify, reconfigure, or rename a group/channel tab by setting your manifest's `canUpdateConfiguration` property to `true`.</span></span>  <span data-ttu-id="411e9-150">En outre, vous pouvez indiquer ce qu’il advient du contenu lorsqu’un onglet est supprimé en incluant une page Options de suppression dans votre application et en définissant une valeur pour la `removeUrl` propriété dans la  `setSettings()` Configuration (voir ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="411e9-150">In addition, you can designate what happens to the content when a tab is removed by including a removal options page in your app and setting a value for the `removeUrl` property in the  `setSettings()` configuration (see below).</span></span> <span data-ttu-id="411e9-151">Les onglets personnels ne peuvent pas être modifiés, mais peuvent être désinstallés par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="411e9-151">Personal tabs can't be modified but can be uninstalled by the user.</span></span> <span data-ttu-id="411e9-152">Pour plus d’informations, consultez [la rubrique créer une page de suppression pour votre onglet](~/tabs/how-to/create-tab-pages/removal-page.md).</span><span class="sxs-lookup"><span data-stu-id="411e9-152">For more information, see [Create a removal page for your tab](~/tabs/how-to/create-tab-pages/removal-page.md).</span></span>

## <a name="mobile-clients"></a><span data-ttu-id="411e9-153">Clients mobiles</span><span class="sxs-lookup"><span data-stu-id="411e9-153">Mobile clients</span></span>

<span data-ttu-id="411e9-154">Si vous choisissez d’afficher l’onglet canal/groupe sur les clients mobiles Teams, la `setSettings()` configuration doit avoir une valeur pour la `websiteUrl` propriété (voir ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="411e9-154">If you choose to have your channel/group tab appear on Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property (see below).</span></span> <span data-ttu-id="411e9-155">La prise en charge complète des onglets sur les clients mobiles sera bientôt disponible.</span><span class="sxs-lookup"><span data-stu-id="411e9-155">Full support for tabs on mobile clients will be released soon.</span></span> <span data-ttu-id="411e9-156">Pour préparer la mise à jour, suivez les [instructions pour les onglets sur les appareils mobiles](~/tabs/design/tabs-mobile.md) lors de la création des onglets.</span><span class="sxs-lookup"><span data-stu-id="411e9-156">To prepare for the update, you should follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md) when creating your tabs.</span></span>

<span data-ttu-id="411e9-157">Microsoft teams setSettings () configuration pour la page de suppression et/ou les clients mobiles :</span><span class="sxs-lookup"><span data-stu-id="411e9-157">Microsoft Teams setSettings() configuration for removal page and/or mobile clients:</span></span>

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add unique name here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "URL REQUIRED FOR MOBILE CLIENTS",
    removeUrl: "ADD REMOVAL PAGE URL HERE"
});
```
