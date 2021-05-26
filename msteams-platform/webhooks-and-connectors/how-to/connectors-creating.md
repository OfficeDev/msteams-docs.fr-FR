---
title: Connecteurs Office 365
description: Décrit comment commencer avec les connecteurs Office 365 dans Microsoft Teams
keywords: 'équipes connecteur O365 '
localization_priority: Normal
ms.topic: conceptual
ms.date: 04/19/2019
ms.openlocfilehash: 1598b84fc1c36547aa4c814cdf03404a3833779e
ms.sourcegitcommit: c55b0d2a4c1f8945e49b0b7c0b08c0eb3da3d2be
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/25/2021
ms.locfileid: "52646321"
---
# <a name="creating-office-365-connectors-for-microsoft-teams"></a><span data-ttu-id="6af94-104">Création de connecteurs Office 365 pour Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="6af94-104">Creating Office 365 Connectors for Microsoft Teams</span></span>

<span data-ttu-id="6af94-105">Avec Microsoft Teams applications, vous pouvez ajouter votre connecteur Office 365 existant ou en créer un nouveau à inclure dans Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="6af94-105">With Microsoft Teams apps, you can add your existing Office 365 Connector or build a new one to include in Microsoft Teams.</span></span> <span data-ttu-id="6af94-106">Pour [plus d’informations, voir](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector) Créer votre propre connecteur.</span><span class="sxs-lookup"><span data-stu-id="6af94-106">See [Build your own Connector](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector) for more information.</span></span>

## <a name="adding-a-connector-to-your-teams-app"></a><span data-ttu-id="6af94-107">Ajout d’un connecteur à votre application Teams web</span><span class="sxs-lookup"><span data-stu-id="6af94-107">Adding a Connector to your Teams App</span></span>

<span data-ttu-id="6af94-108">Vous pouvez distribuer votre connecteur inscrit dans le cadre de votre package d’application Teams.</span><span class="sxs-lookup"><span data-stu-id="6af94-108">You can distribute your registered Connector as part of your Teams app package.</span></span> <span data-ttu-id="6af94-109">Qu’il s’agit d’une solution autonome ou de l’une des [](~/concepts/build-and-test/apps-package.md) nombreuses [](~/concepts/deploy-and-publish/apps-publish.md) fonctionnalités que votre expérience active dans Teams, vous pouvez packager et publier votre connecteur dans le cadre de votre soumission AppSource, ou vous pouvez le fournir aux utilisateurs directement pour le chargement dans Teams. [](~/concepts/extensibility-points.md)</span><span class="sxs-lookup"><span data-stu-id="6af94-109">Whether as a standalone solution, or one of several [capabilities](~/concepts/extensibility-points.md) that your experience enables in Teams, you can [package](~/concepts/build-and-test/apps-package.md) and [publish](~/concepts/deploy-and-publish/apps-publish.md) your Connector as part of your AppSource submission, or you can provide it to users directly for uploading within Teams.</span></span>

<span data-ttu-id="6af94-110">Pour distribuer votre connecteur, vous devez vous inscrire à l’aide du tableau de bord du [développeur de connecteurs.](https://outlook.office.com/connectors/home/login/#/publish)</span><span class="sxs-lookup"><span data-stu-id="6af94-110">To distribute your Connector, you need to register by using the [Connectors Developer Dashboard](https://outlook.office.com/connectors/home/login/#/publish).</span></span> <span data-ttu-id="6af94-111">Par défaut, une fois qu’un connecteur est inscrit, il est supposé que votre connecteur fonctionne dans tous les produits Office 365 qui les prend en charge, y compris Outlook et Teams.</span><span class="sxs-lookup"><span data-stu-id="6af94-111">By default, once a Connector is registered, it's assumed that your Connector will work in all Office 365 products that support them, including Outlook and Teams.</span></span> <span data-ttu-id="6af94-112">Si ce _n’est_ pas le cas et que vous devez créer un connecteur qui fonctionne uniquement dans Microsoft Teams, contactez-nous directement à l’Microsoft Teams [soumissions d’applications.](mailto:teamsubm@microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="6af94-112">If that is _not_ the case and you need to create a Connector that only works in Microsoft Teams, contact us directly at [Microsoft Teams App Submissions](mailto:teamsubm@microsoft.com).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6af94-113">Une fois que **vous avez choisi Enregistrer** dans le tableau de bord du développeur de connecteurs, votre connecteur est enregistré.</span><span class="sxs-lookup"><span data-stu-id="6af94-113">After you choose **Save** in the Connectors Developer Dashboard, your Connector is registered.</span></span> <span data-ttu-id="6af94-114">Si vous souhaitez publier votre connecteur dans AppSource, suivez les instructions dans Publier votre [application Microsoft Teams dans AppSource.](~/concepts/deploy-and-publish/apps-publish.md)</span><span class="sxs-lookup"><span data-stu-id="6af94-114">If you want to publish your Connector in AppSource, follow the instructions in [Publish your Microsoft Teams app to AppSource](~/concepts/deploy-and-publish/apps-publish.md).</span></span> <span data-ttu-id="6af94-115">Si vous ne souhaitez pas publier votre application dans AppSource et simplement la distribuer directement à votre organisation uniquement, vous pouvez le faire en publiant dans [votre organisation.](#publish-connectors-for-your-organization)</span><span class="sxs-lookup"><span data-stu-id="6af94-115">If you do not wish to publish your app in AppSource, and rather simply distribute it directly to your organization only, you can do so by [publishing to your organization](#publish-connectors-for-your-organization).</span></span> <span data-ttu-id="6af94-116">Si vous souhaitez uniquement publier dans votre organisation, aucune action supplémentaire n’est nécessaire sur le tableau de bord du connecteur.</span><span class="sxs-lookup"><span data-stu-id="6af94-116">If you only want to publish to your organization, no further action is necessary on the Connector dashboard.</span></span>

### <a name="integrating-the-configuration-experience"></a><span data-ttu-id="6af94-117">Intégration de l’expérience de configuration</span><span class="sxs-lookup"><span data-stu-id="6af94-117">Integrating the configuration experience</span></span>

<span data-ttu-id="6af94-118">Vos utilisateurs termineront toute l’expérience de configuration du connecteur sans avoir à quitter Teams client.</span><span class="sxs-lookup"><span data-stu-id="6af94-118">Your users will complete the entire Connector configuration experience without having to leave the Teams client.</span></span> <span data-ttu-id="6af94-119">Pour obtenir cette expérience, Teams intégrera votre page de configuration directement dans un iframe.</span><span class="sxs-lookup"><span data-stu-id="6af94-119">To achieve this experience, Teams will embed your configuration page directly within an iframe.</span></span> <span data-ttu-id="6af94-120">La séquence d’opérations est la suivante :</span><span class="sxs-lookup"><span data-stu-id="6af94-120">The sequence of operations is as follows:</span></span>

1. <span data-ttu-id="6af94-121">L’utilisateur clique sur votre connecteur pour commencer le processus de configuration.</span><span class="sxs-lookup"><span data-stu-id="6af94-121">The user clicks on your connector to begin the configuration process.</span></span>
2. <span data-ttu-id="6af94-122">Teams charge votre expérience de configuration en ligne.</span><span class="sxs-lookup"><span data-stu-id="6af94-122">Teams will load your configuration experience in line.</span></span>
3. <span data-ttu-id="6af94-123">L’utilisateur interagit avec votre expérience web pour terminer la configuration.</span><span class="sxs-lookup"><span data-stu-id="6af94-123">The user interacts with your web experience to complete the configuration.</span></span>
4. <span data-ttu-id="6af94-124">L’utilisateur appuie sur « Enregistrer », ce qui déclenche un rappel dans votre code.</span><span class="sxs-lookup"><span data-stu-id="6af94-124">The user presses "Save", which triggers a callback in your code.</span></span>
5. <span data-ttu-id="6af94-125">Votre code traitera l’événement d’enregistrer en récupérant les paramètres de webhook (documentés ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="6af94-125">Your code will process the save event by retrieving the webhook settings (documented below).</span></span> <span data-ttu-id="6af94-126">Votre code doit ensuite stocker le webhook pour publier des événements ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="6af94-126">Your code should then store the webhook to post events later.</span></span>

<span data-ttu-id="6af94-127">Vous pouvez réutiliser votre expérience de configuration web existante ou créer une version distincte à héberger spécifiquement dans Teams.</span><span class="sxs-lookup"><span data-stu-id="6af94-127">You can reuse your existing web configuration experience or create a separate version to be hosted specifically in Teams.</span></span> <span data-ttu-id="6af94-128">Votre code doit :</span><span class="sxs-lookup"><span data-stu-id="6af94-128">Your code should:</span></span>

1. <span data-ttu-id="6af94-129">Incluez le Microsoft Teams SDK JavaScript.</span><span class="sxs-lookup"><span data-stu-id="6af94-129">Include the Microsoft Teams JavaScript SDK.</span></span> <span data-ttu-id="6af94-130">Cela permet à votre code d’accéder aux API pour effectuer des opérations courantes telles que l’obtention du contexte utilisateur/canal/équipe actuel et l’initiateur des flux d’authentification.</span><span class="sxs-lookup"><span data-stu-id="6af94-130">This gives your code access to APIs to perform common operations like getting the current user/channel/team context and initiating authentication flows.</span></span> <span data-ttu-id="6af94-131">Initialisez le kit de développement logiciel (SDK) en appelant `microsoftTeams.initialize()`.</span><span class="sxs-lookup"><span data-stu-id="6af94-131">Initialize the SDK by calling `microsoftTeams.initialize()`.</span></span>
2. <span data-ttu-id="6af94-132">Appelez `microsoftTeams.settings.setValidityState(true)` lorsque vous souhaitez activer le bouton Enregistrer.</span><span class="sxs-lookup"><span data-stu-id="6af94-132">Call `microsoftTeams.settings.setValidityState(true)` when you want to enable the Save button.</span></span> <span data-ttu-id="6af94-133">Vous devez le faire en réponse à une entrée utilisateur valide, telle qu’une sélection ou une mise à jour de champ.</span><span class="sxs-lookup"><span data-stu-id="6af94-133">You should do this as a response to valid user input, such as a selection or field update.</span></span>
3. <span data-ttu-id="6af94-134">Inscrivez un `microsoftTeams.settings.registerOnSaveHandler()` handler d’événements, qui est appelé lorsque l’utilisateur clique sur Enregistrer.</span><span class="sxs-lookup"><span data-stu-id="6af94-134">Register a `microsoftTeams.settings.registerOnSaveHandler()` event handler, which gets called when the user clicks Save.</span></span>
4. <span data-ttu-id="6af94-135">Appelez `microsoftTeams.settings.setSettings()` pour enregistrer les paramètres du connecteur.</span><span class="sxs-lookup"><span data-stu-id="6af94-135">Call `microsoftTeams.settings.setSettings()` to save the connector settings.</span></span> <span data-ttu-id="6af94-136">Les informations enregistrées ici sont également affichées dans la boîte de dialogue de configuration si l’utilisateur tente de mettre à jour une configuration existante pour votre connecteur.</span><span class="sxs-lookup"><span data-stu-id="6af94-136">What's saved here is also what will be shown in the configuration dialog if the user tries to update an existing configuration for your connector.</span></span>
5. <span data-ttu-id="6af94-137">Appelez `microsoftTeams.settings.getSettings()` pour récupérer les propriétés du webhook, y compris l’URL proprement dite.</span><span class="sxs-lookup"><span data-stu-id="6af94-137">Call `microsoftTeams.settings.getSettings()` to fetch webhook properties, including the URL itself.</span></span> <span data-ttu-id="6af94-138">Vous devez l’appeler en plus de l’événement d’enregistrer, vous devez également l’appeler lorsque votre page est chargée pour la première fois dans le cas d’une nouvelle configuration.</span><span class="sxs-lookup"><span data-stu-id="6af94-138">You should call this  In addition to during the save event, you should also call this when your page is first loaded in the case of a re-configuration.</span></span>
6. <span data-ttu-id="6af94-139">(Facultatif) Inscrivez un `microsoftTeams.settings.registerOnRemoveHandler()` handler d’événements, qui est appelé lorsque l’utilisateur supprime votre connecteur.</span><span class="sxs-lookup"><span data-stu-id="6af94-139">(Optional) Register a `microsoftTeams.settings.registerOnRemoveHandler()` event handler, which gets called when the user removes your connector.</span></span> <span data-ttu-id="6af94-140">Cet événement permet à votre service d’effectuer des actions de nettoyage.</span><span class="sxs-lookup"><span data-stu-id="6af94-140">This event gives your service an opportunity to perform any cleanup actions.</span></span>

<span data-ttu-id="6af94-141">Voici un exemple de code HTML pour créer une page de configuration de connecteur sans CSS :</span><span class="sxs-lookup"><span data-stu-id="6af94-141">Here's a sample HTML to create a Connector configuration page without the CSS:</span></span>

```html
<h2>Send notifications when tasks are:</h2>
<div class="col-md-8">
    <section id="configSection">
        <form id="configForm">
            <input type="radio" name="notificationType" value="Create" onclick="onClick()"> Created
            <br>
            <br>
            <input type="radio" name="notificationType" value="Update" onclick="onClick()"> Updated
        </form>
    </section>
</div>

<script src="https://statics.teams.microsoft.com/sdk/v1.5.2/js/MicrosoftTeams.min.js" crossorigin="anonymous"></script>
<script src="/Scripts/jquery-1.10.2.js"></script>

<script type="text/javascript">

        function onClick() {
            microsoftTeams.settings.setValidityState(true);
        }

        microsoftTeams.initialize();
        microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
            var radios = document.getElementsByName('notificationType');

            var eventType = '';
            if (radios[0].checked) {
                eventType = radios[0].value;
            } else {
                eventType = radios[1].value;
            }

            microsoftTeams.settings.setSettings({
                 entityId: eventType,
                contentUrl: "https://YourSite/Connector/Setup",
                removeUrl:"https://YourSite/Connector/Setup",
                 configName: eventType
                });

            microsoftTeams.settings.getSettings(function (settings) {
                // We get the Webhook URL in settings.webhookUrl which needs to be saved. 
                // This can be used later to send notification.
            });

            saveEvent.notifySuccess();
        });

        microsoftTeams.settings.registerOnRemoveHandler(function (removeEvent) {
            alert("Removed" + JSON.stringify(removeEvent));
        });

</script>
```

#### <a name="getsettings-response-properties"></a><span data-ttu-id="6af94-142">`GetSettings()` propriétés de réponse</span><span class="sxs-lookup"><span data-stu-id="6af94-142">`GetSettings()` response properties</span></span>

>[!Note]
><span data-ttu-id="6af94-143">Les paramètres renvoyés par l’appel ici sont différents de ceux que vous avez appelés à partir d’un onglet et diffèrent de ceux documentés `getSettings` [ici.](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="6af94-143">The parameters returned by the `getSettings` call here are different than if you were to invoke this method from a tab, and differ from those documented [here](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true).</span></span>

| <span data-ttu-id="6af94-144">Paramètre</span><span class="sxs-lookup"><span data-stu-id="6af94-144">Parameter</span></span>   | <span data-ttu-id="6af94-145">Détails</span><span class="sxs-lookup"><span data-stu-id="6af94-145">Details</span></span> |
|-------------|---------|
| `entityId`       | <span data-ttu-id="6af94-146">L’ID d’entité, tel que définie par votre code lors de `setSettings()` l’appel.</span><span class="sxs-lookup"><span data-stu-id="6af94-146">The entity ID, as set by your code when calling `setSettings()`.</span></span> |
| `configName`  | <span data-ttu-id="6af94-147">Nom de la configuration, tel que définie par votre code lors de `setSettings()` l’appel.</span><span class="sxs-lookup"><span data-stu-id="6af94-147">The configuration name, as set by your code when calling `setSettings()`.</span></span> |
| `contentUrl` | <span data-ttu-id="6af94-148">URL de la page de configuration, définie par votre code lors de `setSettings()` l’appel.</span><span class="sxs-lookup"><span data-stu-id="6af94-148">The URL of the configuration page, as set by your code when calling `setSettings()`.</span></span> |
| `webhookUrl` | <span data-ttu-id="6af94-149">URL de webhook créée pour ce connecteur.</span><span class="sxs-lookup"><span data-stu-id="6af94-149">The webhook URL created for this connector.</span></span> <span data-ttu-id="6af94-150">Persistez l’URL de webhook et utilisez-la pour post JSON structuré pour envoyer des cartes au canal.</span><span class="sxs-lookup"><span data-stu-id="6af94-150">Persist the webhook URL and use it to POST structured JSON to send cards to the channel.</span></span> <span data-ttu-id="6af94-151">L’élément `webhookUrl` est renvoyé uniquement lorsque l’application effectue un renvoi.</span><span class="sxs-lookup"><span data-stu-id="6af94-151">The `webhookUrl` is returned only when application returns successfully.</span></span> |
| `appType` | <span data-ttu-id="6af94-152">Les valeurs renvoyées peuvent être `mail`, `groups` ou `teams` correspondant à la messagerie Office 365, aux groupes Office 365 ou à Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="6af94-152">The values returned can be `mail`, `groups` or `teams` corresponding to the Office 365 Mail, Office 365 Groups or Microsoft Teams respectively.</span></span> |
| `userObjectId` | <span data-ttu-id="6af94-153">Il s’agit de l’ID unique correspondant à l’Office 365 qui a initié la configuration du connecteur.</span><span class="sxs-lookup"><span data-stu-id="6af94-153">This is the unique id corresponding to the Office 365 user who initiated setup of the connector.</span></span> <span data-ttu-id="6af94-154">Il doit être sécurisé.</span><span class="sxs-lookup"><span data-stu-id="6af94-154">It should be secured.</span></span> <span data-ttu-id="6af94-155">Cette valeur peut être utilisée pour associer l’utilisateur dans Office 365 qui a défini la configuration à l’utilisateur dans votre service.</span><span class="sxs-lookup"><span data-stu-id="6af94-155">This value can be used to associate the user in Office 365 who set up the configuration to the user in your service.</span></span> |

<span data-ttu-id="6af94-156">Si vous devez authentifier l’utilisateur dans le cadre du [](~/tabs/how-to/authentication/auth-flow-tab.md) chargement de votre page à l’étape 2 ci-dessus, reportez-vous à ce lien pour plus d’informations sur la façon d’intégrer la connexion lorsque votre page est incorporée.</span><span class="sxs-lookup"><span data-stu-id="6af94-156">If you need to authenticate the user as part of loading your page in step 2 above, refer to [this link](~/tabs/how-to/authentication/auth-flow-tab.md) for details on how you can integrate login when your page is embedded.</span></span>

> [!NOTE]
> <span data-ttu-id="6af94-157">Pour des raisons de compatibilité entre clients, votre code devra appeler avec l’URL et les méthodes de rappel de `microsoftTeams.authentication.registerAuthenticationHandlers()` réussite/échec avant d’appeler. `authenticate()`</span><span class="sxs-lookup"><span data-stu-id="6af94-157">Due to cross-client compatibility reasons, your code will need to call `microsoftTeams.authentication.registerAuthenticationHandlers()` with the URL and success/failure callback methods before calling `authenticate()`.</span></span>

#### <a name="handling-edits"></a><span data-ttu-id="6af94-158">Gestion des modifications</span><span class="sxs-lookup"><span data-stu-id="6af94-158">Handling edits</span></span>

<span data-ttu-id="6af94-159">Votre code doit gérer les utilisateurs qui reviennent dans le but de modifier une configuration de connecteur existante.</span><span class="sxs-lookup"><span data-stu-id="6af94-159">Your code should handle users returning to edit an existing connector configuration.</span></span> <span data-ttu-id="6af94-160">Pour ce faire, appelez `microsoftTeams.settings.setSettings()` pendant la configuration initiale avec les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="6af94-160">To do this, call `microsoftTeams.settings.setSettings()` during the initial configuration with the following parameters:</span></span>

- <span data-ttu-id="6af94-161">`entityId` est l’ID personnalisé compris par votre service et qui représente ce que l’utilisateur a configuré.</span><span class="sxs-lookup"><span data-stu-id="6af94-161">`entityId` is the custom ID that is understood by your service and represents what the user has configured.</span></span>
- <span data-ttu-id="6af94-162">`configName` est un nom convivial que votre code de configuration peut récupérer</span><span class="sxs-lookup"><span data-stu-id="6af94-162">`configName` is a friendly name that your configuration code can retrieve</span></span>
- <span data-ttu-id="6af94-163">`contentUrl` est une URL personnalisée qui est chargée lorsqu’un utilisateur modifie une configuration de connecteur existante.</span><span class="sxs-lookup"><span data-stu-id="6af94-163">`contentUrl` is a custom URL that gets loaded when a user edits an existing connector configuration.</span></span> <span data-ttu-id="6af94-164">Vous pouvez utiliser cette URL pour faciliter la tâche de modification de votre code.</span><span class="sxs-lookup"><span data-stu-id="6af94-164">You can use this URL to make it easier for your code to handle the edit case.</span></span>

<span data-ttu-id="6af94-165">En règle générale, cet appel est effectué dans le cadre de votre économiseur d’événements.</span><span class="sxs-lookup"><span data-stu-id="6af94-165">Typically, this call is made as part of your save event handler.</span></span> <span data-ttu-id="6af94-166">Ensuite, lorsque le code ci-dessus est chargé, votre code doit appeler pour prére remplir les paramètres ou formulaires de votre `contentUrl` interface utilisateur de `getSettings()` configuration.</span><span class="sxs-lookup"><span data-stu-id="6af94-166">Then, when the `contentUrl` above is loaded, your code should call `getSettings()` to prepopulate any settings or forms in your configuration UI.</span></span>

#### <a name="handling-removals"></a><span data-ttu-id="6af94-167">Gestion des suppressions</span><span class="sxs-lookup"><span data-stu-id="6af94-167">Handling removals</span></span>

<span data-ttu-id="6af94-168">Vous pouvez éventuellement exécuter un handler d’événements lorsque l’utilisateur supprime une configuration de connecteur existante.</span><span class="sxs-lookup"><span data-stu-id="6af94-168">You can optionally execute an event handler when the user removes an existing connector configuration.</span></span> <span data-ttu-id="6af94-169">Vous inscrivez ce handler en appelant `microsoftTeams.settings.registerOnRemoveHandler()` .</span><span class="sxs-lookup"><span data-stu-id="6af94-169">You register this handler by calling `microsoftTeams.settings.registerOnRemoveHandler()`.</span></span> <span data-ttu-id="6af94-170">Ce handler peut être utilisé pour effectuer des opérations de nettoyage telles que la suppression d’entrées d’une base de données.</span><span class="sxs-lookup"><span data-stu-id="6af94-170">This handler can be used to perform cleanup operations such as removing entries from a database.</span></span>

### <a name="including-the-connector-in-your-manifest"></a><span data-ttu-id="6af94-171">Inclure le connecteur dans votre manifeste</span><span class="sxs-lookup"><span data-stu-id="6af94-171">Including the Connector in your Manifest</span></span>

<span data-ttu-id="6af94-172">Vous pouvez télécharger le manifeste de l’application Teams généré automatiquement à partir du portail.</span><span class="sxs-lookup"><span data-stu-id="6af94-172">You can download the auto-generated Teams app manifest from the portal.</span></span> <span data-ttu-id="6af94-173">Toutefois, avant de pouvoir l’utiliser pour tester ou publier votre application, vous devez :</span><span class="sxs-lookup"><span data-stu-id="6af94-173">Before you can use it to test or publish your app, though, you must do the following:</span></span>

- <span data-ttu-id="6af94-174">[Incluez deux icônes](../../concepts/build-and-test/apps-package.md#app-icons).</span><span class="sxs-lookup"><span data-stu-id="6af94-174">[Include two icons](../../concepts/build-and-test/apps-package.md#app-icons).</span></span>
- <span data-ttu-id="6af94-175">Modifiez la partie `icons` du manifeste pour faire référence aux noms de fichier des icônes au lieu des URL.</span><span class="sxs-lookup"><span data-stu-id="6af94-175">Modify the `icons` portion of the manifest to refer to the file names of the icons instead of URLs.</span></span>

<span data-ttu-id="6af94-176">Le fichier manifest.json suivant contient les éléments de base nécessaires pour tester et envoyer votre application.</span><span class="sxs-lookup"><span data-stu-id="6af94-176">The following manifest.json file contains the basic elements needed to test and submit your app.</span></span>

> [!NOTE]
> <span data-ttu-id="6af94-177">Remplacez `id` et `connectorId` de l’exemple suivant par le GUID de votre connecteur.</span><span class="sxs-lookup"><span data-stu-id="6af94-177">Replace `id` and `connectorId` in the following example with the GUID of your Connector.</span></span>

#### <a name="example-manifestjson-with-connector"></a><span data-ttu-id="6af94-178">Exemple de fichier manifest.json avec Connecteur</span><span class="sxs-lookup"><span data-stu-id="6af94-178">Example manifest.json with Connector</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "id": "e9343a03-0a5e-4c1f-95a8-263a565505a5",
  "version": "1.0",
  "packageName": "com.sampleapp",
  "developer": {
    "name": "Publisher",
    "websiteUrl": "https://www.microsoft.com",
    "privacyUrl": "https://www.microsoft.com",
    "termsOfUseUrl": "https://www.microsoft.com"
  },
  "description": {
    "full": "This is a sample manifest for an app with a connector with an inline configuration experience.",
    "short": "This is a sample manifest for an app with a connector."
  },
  "icons": {
    "outline": "sampleapp-outline.png",
    "color": "sampleapp-color.png"
  },
  "connectors": [
    {
      "connectorId": "e9343a03-0a5e-4c1f-95a8-263a565505a5",
      "configurationUrl": "https://teamstodoappconnectorwithinlineconfig.azurewebsites.net/Connector/Setup",
      "scopes": [
        "team"
      ]
    }
  ],
  "name": {
    "short": "Sample App",
    "full": "Sample App Long Name"
  },
  "accentColor": "#FFFFFF"
}
```

## <a name="disable-or-enable-connectors-in-teams"></a><span data-ttu-id="6af94-179">Désactiver ou activer des connecteurs dans Teams</span><span class="sxs-lookup"><span data-stu-id="6af94-179">Disable or enable connectors in Teams</span></span>

<span data-ttu-id="6af94-180">Le module Exchange Online PowerShell V2 utilise l’authentification moderne et fonctionne avec l’authentification multifacteur (MFA) pour la connexion à tous les environnements PowerShell Exchange dans Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="6af94-180">The Exchange Online PowerShell V2 module uses modern authentication and works with multi-factor authentication (MFA) for connecting to all Exchange-related PowerShell environments in Microsoft 365.</span></span> <span data-ttu-id="6af94-181">Les administrateurs peuvent utiliser Exchange Online PowerShell pour désactiver les connecteurs pour un client entier ou une boîte aux lettres de groupe spécifique, affectant tous les utilisateurs de ce client ou de cette boîte aux lettres.</span><span class="sxs-lookup"><span data-stu-id="6af94-181">Admins can use Exchange Online PowerShell to disable connectors for an entire tenant or a specific group mailbox, affecting all users in that tenant or mailbox.</span></span> <span data-ttu-id="6af94-182">Il n’est pas possible de désactiver pour certains et non pour d’autres.</span><span class="sxs-lookup"><span data-stu-id="6af94-182">It is not possible to disable for some and not others.</span></span> <span data-ttu-id="6af94-183">En outre, les connecteurs sont désactivés par défaut pour Cloud de la communauté du secteur public client.</span><span class="sxs-lookup"><span data-stu-id="6af94-183">Also, connectors are disabled by default for GCC tenants.</span></span>

<span data-ttu-id="6af94-184">Le paramètre au niveau du client remplace le paramètre au niveau du groupe.</span><span class="sxs-lookup"><span data-stu-id="6af94-184">The tenant-level setting overrides the group-level setting.</span></span> <span data-ttu-id="6af94-185">Par exemple, si un administrateur active les connecteurs pour le groupe et les désactive sur le client, les connecteurs pour le groupe seront désactivés.</span><span class="sxs-lookup"><span data-stu-id="6af94-185">For example, if an admin enables connectors for the group and disables them on the tenant, connectors for the group will be disabled.</span></span> <span data-ttu-id="6af94-186">Pour activer un connecteur dans Teams, connectez-vous [à Exchange Online PowerShell](/powershell/exchange/connect-to-exchange-online-powershell?view=exchange-ps#connect-to-exchange-online-powershell-using-modern-authentication-with-or-without-mfa&preserve-view=true) à l’aide de l’authentification moderne avec ou sans authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="6af94-186">To enable a connector in Teams, [connect to Exchange Online PowerShell](/powershell/exchange/connect-to-exchange-online-powershell?view=exchange-ps#connect-to-exchange-online-powershell-using-modern-authentication-with-or-without-mfa&preserve-view=true) using modern authentication with or without MFA.</span></span>

### <a name="commands-to-disable-or-enable-connectors"></a><span data-ttu-id="6af94-187">Commandes permettant de désactiver ou d’activer des connecteurs</span><span class="sxs-lookup"><span data-stu-id="6af94-187">Commands to disable or enable connectors</span></span>

<span data-ttu-id="6af94-188">**Exécuter la commande dans Exchange Online PowerShell**</span><span class="sxs-lookup"><span data-stu-id="6af94-188">**Run the command in Exchange Online PowerShell**</span></span>

* <span data-ttu-id="6af94-189">Pour désactiver les connecteurs pour le client : `Set-OrganizationConfig -ConnectorsEnabled:$false` .</span><span class="sxs-lookup"><span data-stu-id="6af94-189">To disable connectors for the tenant: `Set-OrganizationConfig -ConnectorsEnabled:$false`.</span></span>
* <span data-ttu-id="6af94-190">Pour désactiver les messages actionnables pour le client : `Set-OrganizationConfig -ConnectorsActionableMessagesEnabled:$false` .</span><span class="sxs-lookup"><span data-stu-id="6af94-190">To disable actionable messages for the tenant: `Set-OrganizationConfig -ConnectorsActionableMessagesEnabled:$false`.</span></span>
* <span data-ttu-id="6af94-191">Pour activer les connecteurs pour Teams, exécutez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="6af94-191">To enable connectors for Teams, run the following commands:</span></span>
    * `Set-OrganizationConfig -ConnectorsEnabled:$true `
    * `Set-OrganizationConfig -ConnectorsEnabledForTeams:$true`
    * `Set-OrganizationConfig -ConnectorsActionableMessagesEnabled:$true`

<span data-ttu-id="6af94-192">Pour plus d’informations sur l’échange de module PowerShell, voir [Set-OrganizationConfig](/powershell/module/exchange/Set-OrganizationConfig?view=exchange-ps&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="6af94-192">For more information on PowerShell module exchange, see [Set-OrganizationConfig](/powershell/module/exchange/Set-OrganizationConfig?view=exchange-ps&preserve-view=true).</span></span> <span data-ttu-id="6af94-193">Pour activer ou désactiver les connecteurs Outlook, [connectez](https://support.microsoft.com/topic/connect-apps-to-your-groups-in-outlook-ed0ce547-038f-4902-b9b3-9e518ae6fbab?ui=en-us&rs=en-us&ad=us)des applications à vos groupes dans Outlook .</span><span class="sxs-lookup"><span data-stu-id="6af94-193">To enable or disable Outlook connectors, [connect apps to your groups in Outlook](https://support.microsoft.com/topic/connect-apps-to-your-groups-in-outlook-ed0ce547-038f-4902-b9b3-9e518ae6fbab?ui=en-us&rs=en-us&ad=us).</span></span>

## <a name="testing-your-connector"></a><span data-ttu-id="6af94-194">Test du connecteur</span><span class="sxs-lookup"><span data-stu-id="6af94-194">Testing your Connector</span></span>

<span data-ttu-id="6af94-195">Pour tester le connecteur, téléchargez-le dans une équipe comme vous le feriez avec une autre application.</span><span class="sxs-lookup"><span data-stu-id="6af94-195">To test your Connector, upload it to a team as you would with any other app.</span></span> <span data-ttu-id="6af94-196">Vous pouvez créer un package .zip à l’aide du fichier manifeste à partir du tableau de bord du développeur de connecteurs (modifié comme indiqué dans la section précédente) et des deux fichiers d’icône.</span><span class="sxs-lookup"><span data-stu-id="6af94-196">You can create a .zip package using the manifest file from the Connectors Developer Dashboard (modified as directed in the preceding section) and the two icon files.</span></span>

<span data-ttu-id="6af94-197">Une fois que vous avez téléchargé l’application, ouvrez la liste des connecteurs à partir de n’importe quel canal.</span><span class="sxs-lookup"><span data-stu-id="6af94-197">After you upload the app, open the Connectors list from any channel.</span></span> <span data-ttu-id="6af94-198">Faites défiler la page vers le bas pour afficher votre application dans la section **Téléchargé**.</span><span class="sxs-lookup"><span data-stu-id="6af94-198">Scroll to the bottom to see your app in the **Uploaded** section.</span></span>

![Capture d’écran de la section téléchargée dans la boîte de dialogue connecteur](~/assets/images/connectors/connector_dialog_uploaded.png)

<span data-ttu-id="6af94-200">Vous pouvez à présent lancer l’expérience de configuration.</span><span class="sxs-lookup"><span data-stu-id="6af94-200">You can now launch the configuration experience.</span></span> <span data-ttu-id="6af94-201">N’ignorez pas que ce flux se produit entièrement dans Microsoft Teams en tant qu’expérience hébergée.</span><span class="sxs-lookup"><span data-stu-id="6af94-201">Be aware that this flow occurs entirely within Microsoft Teams as a hosted experience.</span></span>

<span data-ttu-id="6af94-202">Pour vérifier `HttpPOST` qu’une action fonctionne correctement, [envoyez des messages à votre connecteur.](~/webhooks-and-connectors/how-to/connectors-using.md)</span><span class="sxs-lookup"><span data-stu-id="6af94-202">To verify that an `HttpPOST` action is working correctly, [send messages to your connector](~/webhooks-and-connectors/how-to/connectors-using.md).</span></span>

## <a name="publish-connectors-for-your-organization"></a><span data-ttu-id="6af94-203">Publier des connecteurs pour votre organisation</span><span class="sxs-lookup"><span data-stu-id="6af94-203">Publish Connectors for your organization</span></span>

<span data-ttu-id="6af94-204">Parfois, vous ne souhaitez peut-être pas publier votre application de connecteur dans l’AppSource/Store public, mais vous souhaitez qu’elle soit disponible uniquement pour les utilisateurs de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="6af94-204">Sometimes, you may not want to publish your connector app to the public AppSource/Store but would like it to be available only to the users in your organization.</span></span> <span data-ttu-id="6af94-205">Dans ce cas, vous pouvez charger votre application de connecteur personnalisé vers le catalogue [d’applications de votre organisation.](~/concepts/deploy-and-publish/apps-publish.md)</span><span class="sxs-lookup"><span data-stu-id="6af94-205">In such cases, you can upload your custom connector app to your [organization's App Catalog](~/concepts/deploy-and-publish/apps-publish.md).</span></span> <span data-ttu-id="6af94-206">Ainsi, votre application de connecteur sera disponible uniquement pour cette organisation et vous n’aurez pas besoin de publier votre connecteur dans le magasin public.</span><span class="sxs-lookup"><span data-stu-id="6af94-206">This way, your connector app will be available only to that organization, and you will not need to publish your connector to the public store.</span></span>

<span data-ttu-id="6af94-207">Une fois que vous avez chargé votre package d’application, pour configurer et utiliser le connecteur dans une équipe, il peut être installé à partir du catalogue d’applications de l’organisation en suivant les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="6af94-207">Once you've uploaded your app package, to configure and use the connector in a Team it can be installed from the organization's app catalog by following these steps:</span></span>

1. <span data-ttu-id="6af94-208">Sélectionnez l’icône des applications dans la barre de navigation verticale à l’extrême gauche.</span><span class="sxs-lookup"><span data-stu-id="6af94-208">Select the apps icon from the far left vertical navigation bar.</span></span>
1. <span data-ttu-id="6af94-209">Dans la **fenêtre Applications,** **sélectionnez Connecteurs.**</span><span class="sxs-lookup"><span data-stu-id="6af94-209">In the **Apps** window select **Connectors**.</span></span>
1. <span data-ttu-id="6af94-210">Sélectionnez le connecteur que vous souhaitez ajouter et une fenêtre de boîte de dialogue s’affiche.</span><span class="sxs-lookup"><span data-stu-id="6af94-210">Select the connector that you want to add and a pop-up dialog window will display.</span></span>
1. <span data-ttu-id="6af94-211">Sélectionnez **Ajouter à une barre d’équipe.**</span><span class="sxs-lookup"><span data-stu-id="6af94-211">Select the **Add to a team** bar.</span></span>
1. <span data-ttu-id="6af94-212">Dans la fenêtre de boîte de dialogue suivante, tapez un nom d’équipe ou de canal.</span><span class="sxs-lookup"><span data-stu-id="6af94-212">In the next dialog window type a team or channel name.</span></span>
1. <span data-ttu-id="6af94-213">Sélectionnez **la barre Configurer un connecteur** dans le coin inférieur droit de la fenêtre de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="6af94-213">Select the **Set up a connector** bar from the bottom right corner of dialog window.</span></span>
1. <span data-ttu-id="6af94-214">Le connecteur sera disponible dans la section &#9679;&#9679;&#9679; => *Options* supplémentaires Connecteurs Tous les connecteurs pour votre équipe  =>    =>    =>   pour cette équipe.</span><span class="sxs-lookup"><span data-stu-id="6af94-214">The connector will be available in the  section &#9679;&#9679;&#9679; => *More options* => *Connectors* => *All* => *Connectors for you team* for that team.</span></span> <span data-ttu-id="6af94-215">Vous pouvez naviguer en accédant à cette section ou rechercher l’application connecteur.</span><span class="sxs-lookup"><span data-stu-id="6af94-215">You can navigate by scrolling to this section or search for the connector app.</span></span>
1. <span data-ttu-id="6af94-216">Pour configurer ou modifier le connecteur, sélectionnez **la barre Configurer.**</span><span class="sxs-lookup"><span data-stu-id="6af94-216">To configure or modify the connector select the **Configure** bar.</span></span>

## <a name="code-sample"></a><span data-ttu-id="6af94-217">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="6af94-217">Code sample</span></span>
|<span data-ttu-id="6af94-218">**Exemple de nom**</span><span class="sxs-lookup"><span data-stu-id="6af94-218">**Sample name**</span></span> | <span data-ttu-id="6af94-219">**Description**</span><span class="sxs-lookup"><span data-stu-id="6af94-219">**Description**</span></span> | <span data-ttu-id="6af94-220">**.NET**</span><span class="sxs-lookup"><span data-stu-id="6af94-220">**.NET**</span></span> | <span data-ttu-id="6af94-221">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="6af94-221">**Node.js**</span></span> |
|----------------|------------------|--------|----------------|
| <span data-ttu-id="6af94-222">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="6af94-222">Connectors</span></span>    | <span data-ttu-id="6af94-223">Exemple Office 365 connecteur générant des notifications au canal Teams.</span><span class="sxs-lookup"><span data-stu-id="6af94-223">Sample Office 365 Connector generating notifications to teams channel.</span></span>|   [<span data-ttu-id="6af94-224">View</span><span class="sxs-lookup"><span data-stu-id="6af94-224">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-todo-notification/csharp) | [<span data-ttu-id="6af94-225">View</span><span class="sxs-lookup"><span data-stu-id="6af94-225">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-github-notification/nodejs)|
| <span data-ttu-id="6af94-226">Exemple de connecteurs génériques</span><span class="sxs-lookup"><span data-stu-id="6af94-226">Generic connectors sample</span></span> |<span data-ttu-id="6af94-227">Exemple de code pour un connecteur générique facile à personnaliser pour n’importe quel système qui prend en charge les webhooks.</span><span class="sxs-lookup"><span data-stu-id="6af94-227">Sample code for a generic connector that's easy to customize for any system which supports webhooks.</span></span>|  | [<span data-ttu-id="6af94-228">View</span><span class="sxs-lookup"><span data-stu-id="6af94-228">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-generic/nodejs)|
