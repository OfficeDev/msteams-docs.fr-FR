---
title: Connecteurs Office 365
description: Décrit comment commencer avec les connecteurs Office 365 en Microsoft Teams
keywords: 'équipes connecteur O365 '
localization_priority: Normal
ms.topic: conceptual
ms.date: 04/19/2019
ms.openlocfilehash: 9eaaedf88d907dd7a7422068ab5d20450345f0e7
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566809"
---
# <a name="creating-office-365-connectors-for-microsoft-teams"></a><span data-ttu-id="b7a58-104">Création Office 365 connecteurs pour Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="b7a58-104">Creating Office 365 Connectors for Microsoft Teams</span></span>

><span data-ttu-id="b7a58-105">Avec Microsoft Teams applications, vous pouvez ajouter votre connecteur Office 365 existant ou en créer un nouveau pour l’inclure dans Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="b7a58-105">With Microsoft Teams apps, you can add your existing Office 365 Connector or build a new one to include in Microsoft Teams.</span></span> <span data-ttu-id="b7a58-106">Voir [Construire votre propre connecteur pour plus](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector) d’informations.</span><span class="sxs-lookup"><span data-stu-id="b7a58-106">See [Build your own Connector](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector) for more information.</span></span>

## <a name="adding-a-connector-to-your-teams-app"></a><span data-ttu-id="b7a58-107">Ajout d’un connecteur à votre application Teams’argent</span><span class="sxs-lookup"><span data-stu-id="b7a58-107">Adding a Connector to your Teams App</span></span>

<span data-ttu-id="b7a58-108">Vous pouvez distribuer votre connecteur inscrit dans le cadre de votre package d’application Teams.</span><span class="sxs-lookup"><span data-stu-id="b7a58-108">You can distribute your registered Connector as part of your Teams app package.</span></span> <span data-ttu-id="b7a58-109">Que ce soit en tant que solution autonome ou l’une des [plusieurs fonctionnalités](~/concepts/extensibility-points.md) que votre expérience permet en Teams, vous [pouvez emballer et](~/concepts/build-and-test/apps-package.md) [publier](~/concepts/deploy-and-publish/apps-publish.md) votre connecteur dans le cadre de votre soumission AppSource, ou vous pouvez le fournir directement aux utilisateurs pour téléchargement dans les Teams.</span><span class="sxs-lookup"><span data-stu-id="b7a58-109">Whether as a standalone solution, or one of several [capabilities](~/concepts/extensibility-points.md) that your experience enables in Teams, you can [package](~/concepts/build-and-test/apps-package.md) and [publish](~/concepts/deploy-and-publish/apps-publish.md) your Connector as part of your AppSource submission, or you can provide it to users directly for uploading within Teams.</span></span>

<span data-ttu-id="b7a58-110">Pour distribuer votre connecteur, vous devez vous inscrire en utilisant le tableau de bord [des développeurs de connecteurs.](https://outlook.office.com/connectors/home/login/#/publish)</span><span class="sxs-lookup"><span data-stu-id="b7a58-110">To distribute your Connector, you need to register by using the [Connectors Developer Dashboard](https://outlook.office.com/connectors/home/login/#/publish).</span></span> <span data-ttu-id="b7a58-111">Par défaut, une fois qu’un connecteur est enregistré, il est supposé que votre connecteur fonctionnera dans tous les produits Office 365 qui les soutiennent, y compris les Outlook et Teams.</span><span class="sxs-lookup"><span data-stu-id="b7a58-111">By default, once a Connector is registered, it's assumed that your Connector will work in all Office 365 products that support them, including Outlook and Teams.</span></span> <span data-ttu-id="b7a58-112">Si ce _n’est_ pas le cas et que vous devez créer un connecteur qui ne fonctionne qu’en Microsoft Teams, contactez-nous [directement à Microsoft Teams d’applications](mailto:teamsubm@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="b7a58-112">If that is _not_ the case and you need to create a Connector that only works in Microsoft Teams, contact us directly at [Microsoft Teams App Submissions](mailto:teamsubm@microsoft.com).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b7a58-113">Une fois que vous **avez choisi Enregistrer** dans le tableau de bord des développeurs de connecteurs, votre connecteur est enregistré.</span><span class="sxs-lookup"><span data-stu-id="b7a58-113">After you choose **Save** in the Connectors Developer Dashboard, your Connector is registered.</span></span> <span data-ttu-id="b7a58-114">Si vous souhaitez publier votre connecteur dans AppSource, suivez les instructions de [Publier votre application Microsoft Teams à AppSource](~/concepts/deploy-and-publish/apps-publish.md).</span><span class="sxs-lookup"><span data-stu-id="b7a58-114">If you want to publish your Connector in AppSource, follow the instructions in [Publish your Microsoft Teams app to AppSource](~/concepts/deploy-and-publish/apps-publish.md).</span></span> <span data-ttu-id="b7a58-115">Si vous ne souhaitez pas publier votre application dans AppSource, et plutôt simplement la distribuer directement à votre organisation uniquement, vous pouvez le faire en [publiant à votre organisation](#publish-connectors-for-your-organization).</span><span class="sxs-lookup"><span data-stu-id="b7a58-115">If you do not wish to publish your app in AppSource, and rather simply distribute it directly to your organization only, you can do so by [publishing to your organization](#publish-connectors-for-your-organization).</span></span> <span data-ttu-id="b7a58-116">Si vous souhaitez uniquement publier sur votre organisation, aucune autre action n’est nécessaire sur le tableau de bord Connector.</span><span class="sxs-lookup"><span data-stu-id="b7a58-116">If you only want to publish to your organization, no further action is necessary on the Connector dashboard.</span></span>

### <a name="integrating-the-configuration-experience"></a><span data-ttu-id="b7a58-117">Intégration de l’expérience de configuration</span><span class="sxs-lookup"><span data-stu-id="b7a58-117">Integrating the configuration experience</span></span>

<span data-ttu-id="b7a58-118">Vos utilisateurs compléteront toute l’expérience de configuration connecteur sans avoir à quitter le Teams client.</span><span class="sxs-lookup"><span data-stu-id="b7a58-118">Your users will complete the entire Connector configuration experience without having to leave the Teams client.</span></span> <span data-ttu-id="b7a58-119">Pour réaliser cette expérience, Teams intégrera votre page de configuration directement dans un iframe.</span><span class="sxs-lookup"><span data-stu-id="b7a58-119">To achieve this experience, Teams will embed your configuration page directly within an iframe.</span></span> <span data-ttu-id="b7a58-120">La séquence des opérations est la suivante :</span><span class="sxs-lookup"><span data-stu-id="b7a58-120">The sequence of operations is as follows:</span></span>

1. <span data-ttu-id="b7a58-121">L’utilisateur clique sur votre connecteur pour commencer le processus de configuration.</span><span class="sxs-lookup"><span data-stu-id="b7a58-121">The user clicks on your connector to begin the configuration process.</span></span>
2. <span data-ttu-id="b7a58-122">Teams chargera votre expérience de configuration en ligne.</span><span class="sxs-lookup"><span data-stu-id="b7a58-122">Teams will load your configuration experience in line.</span></span>
3. <span data-ttu-id="b7a58-123">L’utilisateur interagit avec votre expérience Web pour compléter la configuration.</span><span class="sxs-lookup"><span data-stu-id="b7a58-123">The user interacts with your web experience to complete the configuration.</span></span>
4. <span data-ttu-id="b7a58-124">L’utilisateur appuie sur « Enregistrer », ce qui déclenche un rappel dans votre code.</span><span class="sxs-lookup"><span data-stu-id="b7a58-124">The user presses "Save", which triggers a callback in your code.</span></span>
5. <span data-ttu-id="b7a58-125">Votre code traitera l’événement d’sauvegarde en récupérant les paramètres webhook (documentés ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="b7a58-125">Your code will process the save event by retrieving the webhook settings (documented below).</span></span> <span data-ttu-id="b7a58-126">Votre code doit ensuite stocker le webhook pour afficher des événements plus tard.</span><span class="sxs-lookup"><span data-stu-id="b7a58-126">Your code should then store the webhook to post events later.</span></span>

<span data-ttu-id="b7a58-127">Vous pouvez réutiliser votre expérience de configuration Web existante ou créer une version distincte qui sera hébergée spécifiquement dans Teams.</span><span class="sxs-lookup"><span data-stu-id="b7a58-127">You can reuse your existing web configuration experience or create a separate version to be hosted specifically in Teams.</span></span> <span data-ttu-id="b7a58-128">Votre code doit :</span><span class="sxs-lookup"><span data-stu-id="b7a58-128">Your code should:</span></span>

1. <span data-ttu-id="b7a58-129">Incluez le Microsoft Teams JavaScript SDK.</span><span class="sxs-lookup"><span data-stu-id="b7a58-129">Include the Microsoft Teams JavaScript SDK.</span></span> <span data-ttu-id="b7a58-130">Cela donne à votre code l’accès aux API pour effectuer des opérations courantes comme obtenir le contexte utilisateur/canal/équipe actuel et initier des flux d’authentification.</span><span class="sxs-lookup"><span data-stu-id="b7a58-130">This gives your code access to APIs to perform common operations like getting the current user/channel/team context and initiating authentication flows.</span></span> <span data-ttu-id="b7a58-131">Initialisez le kit de développement logiciel (SDK) en appelant `microsoftTeams.initialize()`.</span><span class="sxs-lookup"><span data-stu-id="b7a58-131">Initialize the SDK by calling `microsoftTeams.initialize()`.</span></span>
2. <span data-ttu-id="b7a58-132">Appelez `microsoftTeams.settings.setValidityState(true)` lorsque vous souhaitez activer le bouton Enregistrer.</span><span class="sxs-lookup"><span data-stu-id="b7a58-132">Call `microsoftTeams.settings.setValidityState(true)` when you want to enable the Save button.</span></span> <span data-ttu-id="b7a58-133">Vous devez le faire en réponse à l’entrée utilisateur valide, comme une sélection ou une mise à jour sur le terrain.</span><span class="sxs-lookup"><span data-stu-id="b7a58-133">You should do this as a response to valid user input, such as a selection or field update.</span></span>
3. <span data-ttu-id="b7a58-134">Enregistrez `microsoftTeams.settings.registerOnSaveHandler()` un gestionnaire d’événements, qui est appelé lorsque l’utilisateur clique enregistrer.</span><span class="sxs-lookup"><span data-stu-id="b7a58-134">Register a `microsoftTeams.settings.registerOnSaveHandler()` event handler, which gets called when the user clicks Save.</span></span>
4. <span data-ttu-id="b7a58-135">Appelez `microsoftTeams.settings.setSettings()` pour enregistrer les paramètres du connecteur.</span><span class="sxs-lookup"><span data-stu-id="b7a58-135">Call `microsoftTeams.settings.setSettings()` to save the connector settings.</span></span> <span data-ttu-id="b7a58-136">Ce qui est enregistré ici est également ce qui sera affiché dans le dialogue de configuration si l’utilisateur tente de mettre à jour une configuration existante pour votre connecteur.</span><span class="sxs-lookup"><span data-stu-id="b7a58-136">What's saved here is also what will be shown in the configuration dialog if the user tries to update an existing configuration for your connector.</span></span>
5. <span data-ttu-id="b7a58-137">Appelez `microsoftTeams.settings.getSettings()` pour récupérer les propriétés webhook, y compris l’URL elle-même.</span><span class="sxs-lookup"><span data-stu-id="b7a58-137">Call `microsoftTeams.settings.getSettings()` to fetch webhook properties, including the URL itself.</span></span> <span data-ttu-id="b7a58-138">Vous devez appeler cela En plus de l’événement enregistrer, vous devez également appeler cela lorsque votre page est chargée pour la première fois dans le cas d’une re-configuration.</span><span class="sxs-lookup"><span data-stu-id="b7a58-138">You should call this  In addition to during the save event, you should also call this when your page is first loaded in the case of a re-configuration.</span></span>
6. <span data-ttu-id="b7a58-139">(Facultatif) Enregistrez `microsoftTeams.settings.registerOnRemoveHandler()` un gestionnaire d’événements, qui est appelé lorsque l’utilisateur supprime votre connecteur.</span><span class="sxs-lookup"><span data-stu-id="b7a58-139">(Optional) Register a `microsoftTeams.settings.registerOnRemoveHandler()` event handler, which gets called when the user removes your connector.</span></span> <span data-ttu-id="b7a58-140">Cet événement donne à votre service l’occasion d’effectuer toutes les actions de nettoyage.</span><span class="sxs-lookup"><span data-stu-id="b7a58-140">This event gives your service an opportunity to perform any cleanup actions.</span></span>

<span data-ttu-id="b7a58-141">Voici un exemple HTML pour créer une page de configuration Connector sans le CSS :</span><span class="sxs-lookup"><span data-stu-id="b7a58-141">Here's a sample HTML to create a Connector configuration page without the CSS:</span></span>

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

#### <a name="getsettings-response-properties"></a><span data-ttu-id="b7a58-142">`GetSettings()` propriétés de réponse</span><span class="sxs-lookup"><span data-stu-id="b7a58-142">`GetSettings()` response properties</span></span>

>[!Note]
><span data-ttu-id="b7a58-143">Les paramètres retournés par `getSettings` l’appel ici sont différents que si vous deuriez invoquer cette méthode à partir d’un onglet, et diffèrent de ceux documentés [ici](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="b7a58-143">The parameters returned by the `getSettings` call here are different than if you were to invoke this method from a tab, and differ from those documented [here](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest&preserve-view=true).</span></span>

| <span data-ttu-id="b7a58-144">Paramètre</span><span class="sxs-lookup"><span data-stu-id="b7a58-144">Parameter</span></span>   | <span data-ttu-id="b7a58-145">Détails</span><span class="sxs-lookup"><span data-stu-id="b7a58-145">Details</span></span> |
|-------------|---------|
| `entityId`       | <span data-ttu-id="b7a58-146">L’ID de l’entité, tel qu’il est défini par votre code lors de l’appel `setSettings()` .</span><span class="sxs-lookup"><span data-stu-id="b7a58-146">The entity ID, as set by your code when calling `setSettings()`.</span></span> |
| `configName`  | <span data-ttu-id="b7a58-147">Le nom de configuration, tel que défini par votre code lors de l’appel `setSettings()` .</span><span class="sxs-lookup"><span data-stu-id="b7a58-147">The configuration name, as set by your code when calling `setSettings()`.</span></span> |
| `contentUrl` | <span data-ttu-id="b7a58-148">L’URL de la page de configuration, tel que défini par votre code lors de l’appel `setSettings()` .</span><span class="sxs-lookup"><span data-stu-id="b7a58-148">The URL of the configuration page, as set by your code when calling `setSettings()`.</span></span> |
| `webhookUrl` | <span data-ttu-id="b7a58-149">L’URL webhook créée pour ce connecteur.</span><span class="sxs-lookup"><span data-stu-id="b7a58-149">The webhook URL created for this connector.</span></span> <span data-ttu-id="b7a58-150">Persistez l’URL webhook et utilisez-la pour POSTER JSON structuré pour envoyer des cartes au canal.</span><span class="sxs-lookup"><span data-stu-id="b7a58-150">Persist the webhook URL and use it to POST structured JSON to send cards to the channel.</span></span> <span data-ttu-id="b7a58-151">L’élément `webhookUrl` est renvoyé uniquement lorsque l’application effectue un renvoi.</span><span class="sxs-lookup"><span data-stu-id="b7a58-151">The `webhookUrl` is returned only when application returns successfully.</span></span> |
| `appType` | <span data-ttu-id="b7a58-152">Les valeurs renvoyées peuvent être `mail`, `groups` ou `teams` correspondant à la messagerie Office 365, aux groupes Office 365 ou à Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="b7a58-152">The values returned can be `mail`, `groups` or `teams` corresponding to the Office 365 Mail, Office 365 Groups or Microsoft Teams respectively.</span></span> |
| `userObjectId` | <span data-ttu-id="b7a58-153">Il s’agit de l’id unique correspondant Office 365 utilisateur qui a initié la configuration du connecteur.</span><span class="sxs-lookup"><span data-stu-id="b7a58-153">This is the unique id corresponding to the Office 365 user who initiated setup of the connector.</span></span> <span data-ttu-id="b7a58-154">Il doit être sécurisé.</span><span class="sxs-lookup"><span data-stu-id="b7a58-154">It should be secured.</span></span> <span data-ttu-id="b7a58-155">Cette valeur peut être utilisée pour associer l’utilisateur dans Office 365 qui a défini la configuration à l’utilisateur dans votre service.</span><span class="sxs-lookup"><span data-stu-id="b7a58-155">This value can be used to associate the user in Office 365 who set up the configuration to the user in your service.</span></span> |

<span data-ttu-id="b7a58-156">Si vous devez authentifier l’utilisateur dans le cadre du chargement de votre page à l’étape 2 ci-dessus, consultez ce [lien pour](~/tabs/how-to/authentication/auth-flow-tab.md) plus de détails sur la façon dont vous pouvez intégrer la connexion lorsque votre page est intégrée.</span><span class="sxs-lookup"><span data-stu-id="b7a58-156">If you need to authenticate the user as part of loading your page in step 2 above, refer to [this link](~/tabs/how-to/authentication/auth-flow-tab.md) for details on how you can integrate login when your page is embedded.</span></span>

> [!NOTE]
> <span data-ttu-id="b7a58-157">Pour des raisons de compatibilité inter-clients, votre code devra appeler avec `microsoftTeams.authentication.registerAuthenticationHandlers()` l’URL et les méthodes de rappel de succès/échec avant d’appeler `authenticate()` .</span><span class="sxs-lookup"><span data-stu-id="b7a58-157">Due to cross-client compatibility reasons, your code will need to call `microsoftTeams.authentication.registerAuthenticationHandlers()` with the URL and success/failure callback methods before calling `authenticate()`.</span></span>

#### <a name="handling-edits"></a><span data-ttu-id="b7a58-158">Manipulation des modifications</span><span class="sxs-lookup"><span data-stu-id="b7a58-158">Handling edits</span></span>

<span data-ttu-id="b7a58-159">Votre code doit gérer les utilisateurs qui reviennent dans le but de modifier une configuration de connecteur existante.</span><span class="sxs-lookup"><span data-stu-id="b7a58-159">Your code should handle users returning to edit an existing connector configuration.</span></span> <span data-ttu-id="b7a58-160">Pour ce faire, appelez `microsoftTeams.settings.setSettings()` lors de la configuration initiale avec les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="b7a58-160">To do this, call `microsoftTeams.settings.setSettings()` during the initial configuration with the following parameters:</span></span>

- <span data-ttu-id="b7a58-161">`entityId` est l’iD personnalisé qui est compris par votre service et représente ce que l’utilisateur a configuré.</span><span class="sxs-lookup"><span data-stu-id="b7a58-161">`entityId` is the custom ID that is understood by your service and represents what the user has configured.</span></span>
- <span data-ttu-id="b7a58-162">`configName` est un nom amical que votre code de configuration peut récupérer</span><span class="sxs-lookup"><span data-stu-id="b7a58-162">`configName` is a friendly name that your configuration code can retrieve</span></span>
- <span data-ttu-id="b7a58-163">`contentUrl` est une URL personnalisée qui est chargée lorsqu’un utilisateur modifie une configuration de connecteur existante.</span><span class="sxs-lookup"><span data-stu-id="b7a58-163">`contentUrl` is a custom URL that gets loaded when a user edits an existing connector configuration.</span></span> <span data-ttu-id="b7a58-164">Vous pouvez utiliser cette URL pour faciliter le gestion de l’étui de modification par votre code.</span><span class="sxs-lookup"><span data-stu-id="b7a58-164">You can use this URL to make it easier for your code to handle the edit case.</span></span>

<span data-ttu-id="b7a58-165">En règle générale, cet appel est effectué dans le cadre de votre gestionnaire d’événements d’enregistrer.</span><span class="sxs-lookup"><span data-stu-id="b7a58-165">Typically, this call is made as part of your save event handler.</span></span> <span data-ttu-id="b7a58-166">Ensuite, lorsque ce qui `contentUrl` précède est chargé, votre code doit appeler `getSettings()` pour prépeupler tous les paramètres ou formulaires de votre interface utilisateur de configuration.</span><span class="sxs-lookup"><span data-stu-id="b7a58-166">Then, when the `contentUrl` above is loaded, your code should call `getSettings()` to prepopulate any settings or forms in your configuration UI.</span></span>

#### <a name="handling-removals"></a><span data-ttu-id="b7a58-167">Traitement des déménagements</span><span class="sxs-lookup"><span data-stu-id="b7a58-167">Handling removals</span></span>

<span data-ttu-id="b7a58-168">Vous pouvez exécuter un gestionnaire d’événements en option lorsque l’utilisateur supprime une configuration de connecteur existante.</span><span class="sxs-lookup"><span data-stu-id="b7a58-168">You can optionally execute an event handler when the user removes an existing connector configuration.</span></span> <span data-ttu-id="b7a58-169">Vous enregistrez ce gestionnaire en appelant `microsoftTeams.settings.registerOnRemoveHandler()` .</span><span class="sxs-lookup"><span data-stu-id="b7a58-169">You register this handler by calling `microsoftTeams.settings.registerOnRemoveHandler()`.</span></span> <span data-ttu-id="b7a58-170">Ce gestionnaire peut être utilisé pour effectuer des opérations de nettoyage telles que la suppression des entrées d’une base de données.</span><span class="sxs-lookup"><span data-stu-id="b7a58-170">This handler can be used to perform cleanup operations such as removing entries from a database.</span></span>

### <a name="including-the-connector-in-your-manifest"></a><span data-ttu-id="b7a58-171">Inclure le connecteur dans votre manifeste</span><span class="sxs-lookup"><span data-stu-id="b7a58-171">Including the Connector in your Manifest</span></span>

<span data-ttu-id="b7a58-172">Vous pouvez télécharger le manifeste d’application Teams généré automatiquement à partir du portail.</span><span class="sxs-lookup"><span data-stu-id="b7a58-172">You can download the auto-generated Teams app manifest from the portal.</span></span> <span data-ttu-id="b7a58-173">Avant de pouvoir l’utiliser pour tester ou publier votre application, cependant, vous devez faire ce qui suit:</span><span class="sxs-lookup"><span data-stu-id="b7a58-173">Before you can use it to test or publish your app, though, you must do the following:</span></span>

- <span data-ttu-id="b7a58-174">[Incluez deux icônes](../../concepts/build-and-test/apps-package.md#app-icons).</span><span class="sxs-lookup"><span data-stu-id="b7a58-174">[Include two icons](../../concepts/build-and-test/apps-package.md#app-icons).</span></span>
- <span data-ttu-id="b7a58-175">Modifiez la partie `icons` du manifeste pour faire référence aux noms de fichier des icônes au lieu des URL.</span><span class="sxs-lookup"><span data-stu-id="b7a58-175">Modify the `icons` portion of the manifest to refer to the file names of the icons instead of URLs.</span></span>

<span data-ttu-id="b7a58-176">Le fichier manifest.json suivant contient les éléments de base nécessaires pour tester et envoyer votre application.</span><span class="sxs-lookup"><span data-stu-id="b7a58-176">The following manifest.json file contains the basic elements needed to test and submit your app.</span></span>

> [!NOTE]
> <span data-ttu-id="b7a58-177">Remplacez `id` et `connectorId` de l’exemple suivant par le GUID de votre connecteur.</span><span class="sxs-lookup"><span data-stu-id="b7a58-177">Replace `id` and `connectorId` in the following example with the GUID of your Connector.</span></span>

#### <a name="example-manifestjson-with-connector"></a><span data-ttu-id="b7a58-178">Exemple de fichier manifest.json avec Connecteur</span><span class="sxs-lookup"><span data-stu-id="b7a58-178">Example manifest.json with Connector</span></span>

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

## <a name="testing-your-connector"></a><span data-ttu-id="b7a58-179">Test du connecteur</span><span class="sxs-lookup"><span data-stu-id="b7a58-179">Testing your Connector</span></span>

<span data-ttu-id="b7a58-180">Pour tester le connecteur, téléchargez-le dans une équipe comme vous le feriez avec une autre application.</span><span class="sxs-lookup"><span data-stu-id="b7a58-180">To test your Connector, upload it to a team as you would with any other app.</span></span> <span data-ttu-id="b7a58-181">Vous pouvez créer un package .zip à l’aide du fichier manifeste à partir du tableau de bord du développeur de connecteurs (modifié comme indiqué dans la section précédente) et des deux fichiers d’icône.</span><span class="sxs-lookup"><span data-stu-id="b7a58-181">You can create a .zip package using the manifest file from the Connectors Developer Dashboard (modified as directed in the preceding section) and the two icon files.</span></span>

<span data-ttu-id="b7a58-182">Une fois que vous avez téléchargé l’application, ouvrez la liste des connecteurs à partir de n’importe quel canal.</span><span class="sxs-lookup"><span data-stu-id="b7a58-182">After you upload the app, open the Connectors list from any channel.</span></span> <span data-ttu-id="b7a58-183">Faites défiler la page vers le bas pour afficher votre application dans la section **Téléchargé**.</span><span class="sxs-lookup"><span data-stu-id="b7a58-183">Scroll to the bottom to see your app in the **Uploaded** section.</span></span>

![Capture d’écran de la section téléchargée dans la boîte de dialogue connecteur](~/assets/images/connectors/connector_dialog_uploaded.png)

<span data-ttu-id="b7a58-185">Vous pouvez à présent lancer l’expérience de configuration.</span><span class="sxs-lookup"><span data-stu-id="b7a58-185">You can now launch the configuration experience.</span></span> <span data-ttu-id="b7a58-186">Sachez que ce flux se produit entièrement dans Microsoft Teams comme une expérience hébergée.</span><span class="sxs-lookup"><span data-stu-id="b7a58-186">Be aware that this flow occurs entirely within Microsoft Teams as a hosted experience.</span></span>

<span data-ttu-id="b7a58-187">Pour vérifier `HttpPOST` qu’une action fonctionne correctement, envoyez [des messages à votre connecteur](~/webhooks-and-connectors/how-to/connectors-using.md).</span><span class="sxs-lookup"><span data-stu-id="b7a58-187">To verify that an `HttpPOST` action is working correctly, [send messages to your connector](~/webhooks-and-connectors/how-to/connectors-using.md).</span></span>

## <a name="publish-connectors-for-your-organization"></a><span data-ttu-id="b7a58-188">Publiez connecteurs pour votre organisation</span><span class="sxs-lookup"><span data-stu-id="b7a58-188">Publish Connectors for your organization</span></span>

<span data-ttu-id="b7a58-189">Parfois, vous ne souhaitez peut-être pas publier votre application connecteur sur l’AppSource/Store public, mais vous souhaitez qu’elle ne soit disponible que pour les utilisateurs de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="b7a58-189">Sometimes, you may not want to publish your connector app to the public AppSource/Store but would like it to be available only to the users in your organization.</span></span> <span data-ttu-id="b7a58-190">Dans de tels cas, vous pouvez télécharger votre application de connecteur personnalisée sur le [catalogue d’applications de votre organisation.](~/concepts/deploy-and-publish/apps-publish.md)</span><span class="sxs-lookup"><span data-stu-id="b7a58-190">In such cases, you can upload your custom connector app to your [organization's App Catalog](~/concepts/deploy-and-publish/apps-publish.md).</span></span> <span data-ttu-id="b7a58-191">De cette façon, votre application de connecteur ne sera disponible que pour cette organisation, et vous n’aurez pas besoin de publier votre connecteur au magasin public.</span><span class="sxs-lookup"><span data-stu-id="b7a58-191">This way, your connector app will be available only to that organization, and you will not need to publish your connector to the public store.</span></span>

<span data-ttu-id="b7a58-192">Une fois que vous avez téléchargé votre paquet d’applications, pour configurer et utiliser le connecteur dans une équipe, il peut être installé à partir du catalogue d’applications de l’organisation en suivant ces étapes :</span><span class="sxs-lookup"><span data-stu-id="b7a58-192">Once you've uploaded your app package, to configure and use the connector in a Team it can be installed from the organization's app catalog by following these steps:</span></span>

1. <span data-ttu-id="b7a58-193">Sélectionnez l’icône apps à partir de la barre de navigation verticale d’extrême gauche.</span><span class="sxs-lookup"><span data-stu-id="b7a58-193">Select the apps icon from the far left vertical navigation bar.</span></span>
1. <span data-ttu-id="b7a58-194">Dans la **fenêtre Apps** sélectionnez **Connecteurs**.</span><span class="sxs-lookup"><span data-stu-id="b7a58-194">In the **Apps** window select **Connectors**.</span></span>
1. <span data-ttu-id="b7a58-195">Sélectionnez le connecteur que vous souhaitez ajouter et une fenêtre de dialogue contexturée s’affichera.</span><span class="sxs-lookup"><span data-stu-id="b7a58-195">Select the connector that you want to add and a pop-up dialog window will display.</span></span>
1. <span data-ttu-id="b7a58-196">Sélectionnez **l’ajout à une barre** d’équipe.</span><span class="sxs-lookup"><span data-stu-id="b7a58-196">Select the **Add to a team** bar.</span></span>
1. <span data-ttu-id="b7a58-197">Dans la fenêtre de dialogue suivante, tapez une équipe ou un nom de canal.</span><span class="sxs-lookup"><span data-stu-id="b7a58-197">In the next dialog window type a team or channel name.</span></span>
1. <span data-ttu-id="b7a58-198">Sélectionnez la **barre de connecteur de** l’angle inférieur droit de la fenêtre de dialogue.</span><span class="sxs-lookup"><span data-stu-id="b7a58-198">Select the **Set up a connector** bar from the bottom right corner of dialog window.</span></span>
1. <span data-ttu-id="b7a58-199">Le connecteur sera disponible dans la section &#9679;&#9679;&#9679; => *options*  =>  *Connecteurs*  =>  *Tous*  =>  *connecteurs pour votre équipe* pour cette équipe.</span><span class="sxs-lookup"><span data-stu-id="b7a58-199">The connector will be available in the  section &#9679;&#9679;&#9679; => *More options* => *Connectors* => *All* => *Connectors for you team* for that team.</span></span> <span data-ttu-id="b7a58-200">Vous pouvez naviguer en faisant défiler vers cette section ou rechercher l’application connecteur.</span><span class="sxs-lookup"><span data-stu-id="b7a58-200">You can navigate by scrolling to this section or search for the connector app.</span></span>
1. <span data-ttu-id="b7a58-201">Pour configurer ou modifier le connecteur, sélectionnez **la barre Configure.**</span><span class="sxs-lookup"><span data-stu-id="b7a58-201">To configure or modify the connector select the **Configure** bar.</span></span>

## <a name="code-sample"></a><span data-ttu-id="b7a58-202">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="b7a58-202">Code sample</span></span>
|<span data-ttu-id="b7a58-203">**Nom de l’échantillon**</span><span class="sxs-lookup"><span data-stu-id="b7a58-203">**Sample name**</span></span> | <span data-ttu-id="b7a58-204">**Description**</span><span class="sxs-lookup"><span data-stu-id="b7a58-204">**Description**</span></span> | <span data-ttu-id="b7a58-205">**.NET (en)**</span><span class="sxs-lookup"><span data-stu-id="b7a58-205">**.NET**</span></span> | <span data-ttu-id="b7a58-206">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="b7a58-206">**Node.js**</span></span> |
|----------------|------------------|--------|----------------|
| <span data-ttu-id="b7a58-207">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="b7a58-207">Connectors</span></span>    | <span data-ttu-id="b7a58-208">Exemple Office 365 connecteur générant des notifications au canal des équipes.</span><span class="sxs-lookup"><span data-stu-id="b7a58-208">Sample Office 365 Connector generating notifications to teams channel.</span></span>|   [<span data-ttu-id="b7a58-209">View</span><span class="sxs-lookup"><span data-stu-id="b7a58-209">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-todo-notification/csharp) | [<span data-ttu-id="b7a58-210">View</span><span class="sxs-lookup"><span data-stu-id="b7a58-210">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-github-notification/nodejs)|
| <span data-ttu-id="b7a58-211">Échantillon générique de connecteurs</span><span class="sxs-lookup"><span data-stu-id="b7a58-211">Generic connectors sample</span></span> |<span data-ttu-id="b7a58-212">Exemple de code pour un connecteur générique facile à personnaliser pour n’importe quel système qui prend en charge les webhooks.</span><span class="sxs-lookup"><span data-stu-id="b7a58-212">Sample code for a generic connector that's easy to customize for any system which supports webhooks.</span></span>|  | [<span data-ttu-id="b7a58-213">View</span><span class="sxs-lookup"><span data-stu-id="b7a58-213">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-generic/nodejs)|
