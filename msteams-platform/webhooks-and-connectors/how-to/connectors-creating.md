---
title: Créer des connecteurs Office 365
author: laujan
description: Décrit comment commencer avec les connecteurs Office 365 dans Microsoft Teams
keywords: 'équipes connecteur O365 '
localization_priority: Normal
ms.topic: conceptual
ms.date: 06/16/2021
ms.openlocfilehash: 28a2b35e868baf34e35a11a00e10b30b0f09c236
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179754"
---
# <a name="create-office-365-connectors"></a><span data-ttu-id="e631f-104">Créer des connecteurs Office 365</span><span class="sxs-lookup"><span data-stu-id="e631f-104">Create Office 365 Connectors</span></span>

<span data-ttu-id="e631f-105">Avec Microsoft Teams applications, vous pouvez ajouter votre connecteur Office 365 existant ou en créer un nouveau dans Teams.</span><span class="sxs-lookup"><span data-stu-id="e631f-105">With Microsoft Teams apps, you can add your existing Office 365 Connector or build a new one within Teams.</span></span> <span data-ttu-id="e631f-106">Pour plus d’informations, [voir créer votre propre connecteur.](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector)</span><span class="sxs-lookup"><span data-stu-id="e631f-106">For more information, see [build your own connector](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector).</span></span>

## <a name="add-a-connector-to-teams-app"></a><span data-ttu-id="e631f-107">Ajouter un connecteur à Teams application</span><span class="sxs-lookup"><span data-stu-id="e631f-107">Add a connector to Teams app</span></span>

<span data-ttu-id="e631f-108">Vous pouvez [packager](~/concepts/build-and-test/apps-package.md) [et publier](~/concepts/deploy-and-publish/apps-publish.md) votre connecteur dans le cadre de votre soumission AppSource.</span><span class="sxs-lookup"><span data-stu-id="e631f-108">You can [package](~/concepts/build-and-test/apps-package.md) and [publish](~/concepts/deploy-and-publish/apps-publish.md) your connector as part of your AppSource submission.</span></span> <span data-ttu-id="e631f-109">Vous pouvez distribuer votre connecteur inscrit dans le cadre de votre package Teams’application.</span><span class="sxs-lookup"><span data-stu-id="e631f-109">You can distribute your registered connector as part of your Teams app package.</span></span> <span data-ttu-id="e631f-110">Pour plus d’informations sur les points d’entrée Teams’application, voir [fonctionnalités.](~/concepts/extensibility-points.md)</span><span class="sxs-lookup"><span data-stu-id="e631f-110">For information on entry points for Teams app, see [capabilities](~/concepts/extensibility-points.md).</span></span> <span data-ttu-id="e631f-111">Vous pouvez également fournir le package aux utilisateurs directement pour le chargement dans Teams.</span><span class="sxs-lookup"><span data-stu-id="e631f-111">You can also provide the package to users directly for uploading within Teams.</span></span>

<span data-ttu-id="e631f-112">Pour distribuer votre connecteur, vous devez vous inscrire via [le Tableau de bord du développeur de connecteurs.](https://outlook.office.com/connectors/home/login/#/publish)</span><span class="sxs-lookup"><span data-stu-id="e631f-112">To distribute your connector, you must register through [Connectors Developer Dashboard](https://outlook.office.com/connectors/home/login/#/publish).</span></span> <span data-ttu-id="e631f-113">Lorsqu’un connecteur est inscrit, il est supposé qu’il fonctionne dans tous les produits Office 365 qui prend en charge les applications, y compris Outlook et Teams.</span><span class="sxs-lookup"><span data-stu-id="e631f-113">When a connector is registered, it is assumed that it works in all Office 365 products that support applications, including Outlook and Teams.</span></span> <span data-ttu-id="e631f-114">Si ce n’est pas le cas et que vous devez créer un connecteur qui fonctionne uniquement dans Microsoft Teams, contactez : Microsoft Teams [e-mail soumissions d’applications](mailto:teamsubm@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="e631f-114">If that is not the case and you must create a connector that only works in Microsoft Teams, contact: [Microsoft Teams App Submissions email](mailto:teamsubm@microsoft.com).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e631f-115">Votre connecteur est enregistré après avoir sélectionné **Enregistrer** dans le tableau de bord du développeur de connecteurs.</span><span class="sxs-lookup"><span data-stu-id="e631f-115">Your connector is registered after you select **Save** in the Connectors Developer Dashboard.</span></span> <span data-ttu-id="e631f-116">Si vous souhaitez publier votre connecteur dans AppSource, suivez les instructions de publication de votre [application Microsoft Teams dans AppSource.](~/concepts/deploy-and-publish/apps-publish.md)</span><span class="sxs-lookup"><span data-stu-id="e631f-116">If you want to publish your connector in AppSource, follow the instructions in [publish your Microsoft Teams app to AppSource](~/concepts/deploy-and-publish/apps-publish.md).</span></span> <span data-ttu-id="e631f-117">Si vous ne souhaitez pas publier votre application dans AppSource, distribuez-la directement à l’organisation.</span><span class="sxs-lookup"><span data-stu-id="e631f-117">If you do not want to publish your app in AppSource, distribute it directly to the organization.</span></span> <span data-ttu-id="e631f-118">Après [la publication des connecteurs pour votre organisation,](#publish-connectors-for-the-organization)aucune action supplémentaire n’est requise sur le tableau de bord du connecteur.</span><span class="sxs-lookup"><span data-stu-id="e631f-118">After [publishing connectors for your organization](#publish-connectors-for-the-organization), no further action is required on the Connector Dashboard.</span></span>

### <a name="integrate-the-configuration-experience"></a><span data-ttu-id="e631f-119">Intégrer l’expérience de configuration</span><span class="sxs-lookup"><span data-stu-id="e631f-119">Integrate the configuration experience</span></span>

<span data-ttu-id="e631f-120">Les utilisateurs peuvent terminer toute l’expérience de configuration du connecteur sans avoir à quitter Teams client.</span><span class="sxs-lookup"><span data-stu-id="e631f-120">Users can complete the entire connector configuration experience without having to leave the Teams client.</span></span> <span data-ttu-id="e631f-121">Pour obtenir l’expérience, Teams pouvez incorporer votre page de configuration directement dans un iframe.</span><span class="sxs-lookup"><span data-stu-id="e631f-121">To get the experience, Teams can embed your configuration page directly within an iframe.</span></span> <span data-ttu-id="e631f-122">La séquence d’opérations est la suivante :</span><span class="sxs-lookup"><span data-stu-id="e631f-122">The sequence of operations is as follows:</span></span>

1. <span data-ttu-id="e631f-123">L’utilisateur sélectionne le connecteur pour commencer le processus de configuration.</span><span class="sxs-lookup"><span data-stu-id="e631f-123">The user selects the connector to begin the configuration process.</span></span>
1. <span data-ttu-id="e631f-124">L’utilisateur interagit avec l’expérience web pour terminer la configuration.</span><span class="sxs-lookup"><span data-stu-id="e631f-124">The user interacts with the web experience to complete the configuration.</span></span>
1. <span data-ttu-id="e631f-125">L’utilisateur sélectionne **Enregistrer,** ce qui déclenche un rappel dans le code.</span><span class="sxs-lookup"><span data-stu-id="e631f-125">The user selects **Save**, which triggers a callback in code.</span></span>

    > [!NOTE]
    > * <span data-ttu-id="e631f-126">Le code peut traiter l’événement d’enregistrer en récupérant les paramètres de webhook.</span><span class="sxs-lookup"><span data-stu-id="e631f-126">The code can process the save event by retrieving the webhook settings.</span></span> <span data-ttu-id="e631f-127">Votre code stocke le webhook pour publier des événements ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="e631f-127">Your code stores the webhook to post events later.</span></span>
    > * <span data-ttu-id="e631f-128">L’expérience de configuration est chargée de Teams.</span><span class="sxs-lookup"><span data-stu-id="e631f-128">The configuration experience is loaded inline within Teams.</span></span>

<span data-ttu-id="e631f-129">Vous pouvez réutiliser votre expérience de configuration web existante ou créer une version distincte à héberger spécifiquement dans Teams.</span><span class="sxs-lookup"><span data-stu-id="e631f-129">You can reuse your existing web configuration experience or create a separate version to be hosted specifically in Teams.</span></span> <span data-ttu-id="e631f-130">Votre code doit inclure le Microsoft Teams SDK JavaScript.</span><span class="sxs-lookup"><span data-stu-id="e631f-130">Your code must include the Microsoft Teams JavaScript SDK.</span></span> <span data-ttu-id="e631f-131">Cela permet à votre code d’accéder aux API pour effectuer des opérations courantes, telles que l’obtention du contexte de l’utilisateur, du canal ou de l’équipe actuel et lancer des flux d’authentification.</span><span class="sxs-lookup"><span data-stu-id="e631f-131">This gives your code access to APIs to perform common operations, such as getting the current user, channel, or team context and initiate authentication flows.</span></span>

<span data-ttu-id="e631f-132">**Pour intégrer l’expérience de configuration**</span><span class="sxs-lookup"><span data-stu-id="e631f-132">**To integrate the configuration experience**</span></span>

1. <span data-ttu-id="e631f-133">Initialisez le kit de développement logiciel (SDK) en appelant `microsoftTeams.initialize()`.</span><span class="sxs-lookup"><span data-stu-id="e631f-133">Initialize the SDK by calling `microsoftTeams.initialize()`.</span></span>
1. <span data-ttu-id="e631f-134">Appel `microsoftTeams.settings.setValidityState(true)` pour activer **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="e631f-134">Call `microsoftTeams.settings.setValidityState(true)` to enable **Save**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e631f-135">Vous devez appeler en réponse à la sélection de `microsoftTeams.settings.setValidityState(true)` l’utilisateur ou à la mise à jour du champ.</span><span class="sxs-lookup"><span data-stu-id="e631f-135">You must call `microsoftTeams.settings.setValidityState(true)` as a response to user selection or field update.</span></span>

1. <span data-ttu-id="e631f-136">Enregistrez  `microsoftTeams.settings.registerOnSaveHandler()` le handler d’événements, qui est appelé lorsque l’utilisateur sélectionne **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="e631f-136">Register  `microsoftTeams.settings.registerOnSaveHandler()` event handler, which is called when the user selects **Save**.</span></span>
1. <span data-ttu-id="e631f-137">Appelez `microsoftTeams.settings.setSettings()` pour enregistrer les paramètres du connecteur.</span><span class="sxs-lookup"><span data-stu-id="e631f-137">Call `microsoftTeams.settings.setSettings()` to save the connector settings.</span></span> <span data-ttu-id="e631f-138">Les paramètres enregistrés sont également affichés dans la boîte de dialogue de configuration si l’utilisateur tente de mettre à jour une configuration existante pour votre connecteur.</span><span class="sxs-lookup"><span data-stu-id="e631f-138">The saved settings are also shown in the configuration dialog if the user tries to update an existing configuration for your connector.</span></span>
1. <span data-ttu-id="e631f-139">Appelez `microsoftTeams.settings.getSettings()` pour récupérer les propriétés du webhook, y compris l’URL.</span><span class="sxs-lookup"><span data-stu-id="e631f-139">Call `microsoftTeams.settings.getSettings()` to fetch webhook properties, including the URL.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e631f-140">Vous devez appeler lorsque votre page est chargée pour la première fois `microsoftTeams.settings.getSettings()` en cas de reconfiguration.</span><span class="sxs-lookup"><span data-stu-id="e631f-140">You must call `microsoftTeams.settings.getSettings()` when your page is first loaded in case of reconfiguration.</span></span>

1. <span data-ttu-id="e631f-141">Enregistrez `microsoftTeams.settings.registerOnRemoveHandler()` le handler d’événements, qui est appelé lorsque l’utilisateur supprime le connecteur.</span><span class="sxs-lookup"><span data-stu-id="e631f-141">Register `microsoftTeams.settings.registerOnRemoveHandler()` event handler, which is called when the user removes connector.</span></span>

<span data-ttu-id="e631f-142">Cet événement permet à votre service d’effectuer des actions de nettoyage.</span><span class="sxs-lookup"><span data-stu-id="e631f-142">This event gives your service an opportunity to perform any cleanup actions.</span></span>

<span data-ttu-id="e631f-143">Le code suivant fournit un exemple de code HTML pour créer une page de configuration de connecteur sans le support technique et le service clientèle :</span><span class="sxs-lookup"><span data-stu-id="e631f-143">The following code provides a sample HTML to create a connector configuration page without the customer service and support:</span></span>

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

<span data-ttu-id="e631f-144">Pour authentifier l’utilisateur dans le cadre du chargement de votre page, consultez flux d’authentification pour les [onglets](~/tabs/how-to/authentication/auth-flow-tab.md) pour intégrer la signature lorsque votre page est incorporée.</span><span class="sxs-lookup"><span data-stu-id="e631f-144">To authenticate the user as part of loading your page, see [authentication flow for tabs](~/tabs/how-to/authentication/auth-flow-tab.md) to integrate sign in when your page is embedded.</span></span>

> [!NOTE]
> <span data-ttu-id="e631f-145">Pour des raisons de compatibilité entre clients, votre code doit appeler avec l’URL et les méthodes de rappel de réussite ou `microsoftTeams.authentication.registerAuthenticationHandlers()` d’échec avant d’appeler. `authenticate()`</span><span class="sxs-lookup"><span data-stu-id="e631f-145">Due to cross client compatibility reasons, your code must call `microsoftTeams.authentication.registerAuthenticationHandlers()` with the URL and success or failure callback methods before calling `authenticate()`.</span></span>

#### <a name="getsettings-response-properties"></a><span data-ttu-id="e631f-146">`GetSettings` propriétés de réponse</span><span class="sxs-lookup"><span data-stu-id="e631f-146">`GetSettings` response properties</span></span>

>[!NOTE]
><span data-ttu-id="e631f-147">Les paramètres renvoyés par l’appel sont différents lorsque vous appelez cette méthode à partir d’un onglet et diffèrent de ceux `getSettings` documentés dans [les paramètres js](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="e631f-147">The parameters returned by the `getSettings` call are different when you invoke this method from a tab and differ from those documented in [js settings](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest&preserve-view=true).</span></span>

<span data-ttu-id="e631f-148">Le tableau suivant fournit les paramètres et les détails des propriétés `GetSetting` de réponse :</span><span class="sxs-lookup"><span data-stu-id="e631f-148">The following table provides the parameters and the details of `GetSetting` response properties:</span></span>

| <span data-ttu-id="e631f-149">Paramètres</span><span class="sxs-lookup"><span data-stu-id="e631f-149">Parameters</span></span>   | <span data-ttu-id="e631f-150">Détails</span><span class="sxs-lookup"><span data-stu-id="e631f-150">Details</span></span> |
|-------------|---------|
| `entityId`       | <span data-ttu-id="e631f-151">ID d’entité, tel que définie par votre code lors de `setSettings()` l’appel.</span><span class="sxs-lookup"><span data-stu-id="e631f-151">The entity ID, as set by your code when calling `setSettings()`.</span></span> |
| `configName`  | <span data-ttu-id="e631f-152">Nom de la configuration, tel que définie par votre code lors de `setSettings()` l’appel.</span><span class="sxs-lookup"><span data-stu-id="e631f-152">The configuration name, as set by your code when calling `setSettings()`.</span></span> |
| `contentUrl` | <span data-ttu-id="e631f-153">URL de la page de configuration, définie par votre code lors de `setSettings()` l’appel.</span><span class="sxs-lookup"><span data-stu-id="e631f-153">The URL of the configuration page, as set by your code when calling `setSettings()`.</span></span> |
| `webhookUrl` | <span data-ttu-id="e631f-154">URL de webhook créée pour le connecteur.</span><span class="sxs-lookup"><span data-stu-id="e631f-154">The webhook URL created for the connector.</span></span> <span data-ttu-id="e631f-155">Utilisez l’URL de webhook pour post JSON structuré pour envoyer des cartes au canal.</span><span class="sxs-lookup"><span data-stu-id="e631f-155">Use the webhook URL to POST structured JSON to send cards to the channel.</span></span> <span data-ttu-id="e631f-156">Elle `webhookUrl` est renvoyée uniquement lorsque l’application renvoie des données avec succès.</span><span class="sxs-lookup"><span data-stu-id="e631f-156">The `webhookUrl` is returned only when the application returns data successfully.</span></span> |
| `appType` | <span data-ttu-id="e631f-157">Les valeurs renvoyées peuvent être `mail` `groups` respectivement Office 365 `teams` mail, Office 365 ou Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="e631f-157">The values returned can be `mail`, `groups`, or `teams` corresponding to the Office 365 Mail, Office 365 Groups, or Microsoft Teams respectively.</span></span> |
| `userObjectId` | <span data-ttu-id="e631f-158">ID unique correspondant à l’Office 365 qui a initié la mise en place du connecteur.</span><span class="sxs-lookup"><span data-stu-id="e631f-158">The unique ID corresponding to the Office 365 user who initiated the set up of the connector.</span></span> <span data-ttu-id="e631f-159">Elle doit être sécurisée.</span><span class="sxs-lookup"><span data-stu-id="e631f-159">It must be secured.</span></span> <span data-ttu-id="e631f-160">Cette valeur peut être utilisée pour associer l’utilisateur dans Office 365, qui a installé la configuration dans votre service.</span><span class="sxs-lookup"><span data-stu-id="e631f-160">This value can be used to associate the user in Office 365, who has set up the configuration in your service.</span></span> |

#### <a name="handle-edits"></a><span data-ttu-id="e631f-161">Gérer les modifications</span><span class="sxs-lookup"><span data-stu-id="e631f-161">Handle edits</span></span>

<span data-ttu-id="e631f-162">Votre code doit gérer les utilisateurs qui reviennent pour modifier une configuration de connecteur existante.</span><span class="sxs-lookup"><span data-stu-id="e631f-162">Your code must handle users who return to edit an existing connector configuration.</span></span> <span data-ttu-id="e631f-163">Pour ce faire, appelez `microsoftTeams.settings.setSettings()` pendant la configuration initiale avec les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="e631f-163">To do this, call `microsoftTeams.settings.setSettings()` during the initial configuration with the following parameters:</span></span>

- <span data-ttu-id="e631f-164">`entityId` est l’ID personnalisé qui représente ce que l’utilisateur a configuré et compris par votre service.</span><span class="sxs-lookup"><span data-stu-id="e631f-164">`entityId` is the custom ID that represents what the user has configured and understood by your service.</span></span>
- <span data-ttu-id="e631f-165">`configName` est un nom que le code de configuration peut récupérer.</span><span class="sxs-lookup"><span data-stu-id="e631f-165">`configName` is a name that configuration code can retrieve.</span></span>
- <span data-ttu-id="e631f-166">`contentUrl` est une URL personnalisée qui est chargée lorsqu’un utilisateur modifie une configuration de connecteur existante.</span><span class="sxs-lookup"><span data-stu-id="e631f-166">`contentUrl` is a custom URL that gets loaded when a user edits an existing connector configuration.</span></span>

<span data-ttu-id="e631f-167">Cet appel est effectué dans le cadre de votre économiseur d’événements.</span><span class="sxs-lookup"><span data-stu-id="e631f-167">This call is made as part of your save event handler.</span></span> <span data-ttu-id="e631f-168">Ensuite, lorsque le code est chargé, votre code doit appeler pour pré-remplir les paramètres ou `contentUrl` `getSettings()` formulaires de votre interface utilisateur de configuration.</span><span class="sxs-lookup"><span data-stu-id="e631f-168">Then, when the `contentUrl` is loaded, your code must call `getSettings()` to pre populate any settings or forms in your configuration user interface.</span></span>

#### <a name="handle-removals"></a><span data-ttu-id="e631f-169">Gérer les suppressions</span><span class="sxs-lookup"><span data-stu-id="e631f-169">Handle removals</span></span>

<span data-ttu-id="e631f-170">Vous pouvez exécuter un programme de gestion d’événements lorsque l’utilisateur supprime une configuration de connecteur existante.</span><span class="sxs-lookup"><span data-stu-id="e631f-170">You can execute an event handler when the user removes an existing connector configuration.</span></span> <span data-ttu-id="e631f-171">Vous inscrivez ce handler en appelant `microsoftTeams.settings.registerOnRemoveHandler()` .</span><span class="sxs-lookup"><span data-stu-id="e631f-171">You register this handler by calling `microsoftTeams.settings.registerOnRemoveHandler()`.</span></span> <span data-ttu-id="e631f-172">Ce handler est utilisé pour effectuer des opérations de nettoyage, telles que la suppression d’entrées d’une base de données.</span><span class="sxs-lookup"><span data-stu-id="e631f-172">This handler is used to perform cleanup operations, such as removing entries from a database.</span></span>

### <a name="include-the-connector-in-your-manifest"></a><span data-ttu-id="e631f-173">Inclure le connecteur dans votre manifeste</span><span class="sxs-lookup"><span data-stu-id="e631f-173">Include the connector in your Manifest</span></span>

<span data-ttu-id="e631f-174">Téléchargez la version automatique générée `Teams app manifest` à partir du portail.</span><span class="sxs-lookup"><span data-stu-id="e631f-174">Download the auto generated `Teams app manifest` from the portal.</span></span> <span data-ttu-id="e631f-175">Avant de tester ou de publier l’application, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="e631f-175">Perform the following steps, before testing or publishing the app:</span></span>

1. <span data-ttu-id="e631f-176">[Incluez deux icônes](../../concepts/build-and-test/apps-package.md#app-icons).</span><span class="sxs-lookup"><span data-stu-id="e631f-176">[Include two icons](../../concepts/build-and-test/apps-package.md#app-icons).</span></span>
1. <span data-ttu-id="e631f-177">Modifiez la partie du manifeste pour inclure les noms de fichier des icônes au lieu `icons` des URL.</span><span class="sxs-lookup"><span data-stu-id="e631f-177">Modify the `icons` portion of the manifest to include the file names of the icons instead of URLs.</span></span>

<span data-ttu-id="e631f-178">Le fichier manifest.jssuivant contient les éléments nécessaires pour tester et soumettre l’application :</span><span class="sxs-lookup"><span data-stu-id="e631f-178">The following manifest.json file contains the elements needed to test and submit the app:</span></span>

> [!NOTE]
> <span data-ttu-id="e631f-179">Remplacez `id` `connectorId` et dans l’exemple suivant par le GUID du connecteur.</span><span class="sxs-lookup"><span data-stu-id="e631f-179">Replace `id` and `connectorId` in the following example with the GUID of the connector.</span></span>

#### <a name="example-of-manifestjson-with-connector"></a><span data-ttu-id="e631f-180">Exemple d'manifest.jsavec connecteur</span><span class="sxs-lookup"><span data-stu-id="e631f-180">Example of manifest.json with connector</span></span>

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
    "full": "This is a small sample app we made for you! This app has samples of all capabilities Microsoft Teams supports.",
    "short": "This is a small sample app we made for you!"
  },
  "icons": {
    "outline": "sampleapp-outline.png",
    "color": "sampleapp-color.png"
  },
  "connectors": [
    {
      "connectorId": "e9343a03-0a5e-4c1f-95a8-263a565505a5",
      "scopes": [
        "team"
      ]
    }
  ],
  "name": {
    "short": "Sample App",
    "full": "Sample App"
  },
  "accentColor": "#FFFFFF",
  "needsIdentity": "true"
}
```

## <a name="enable-or-disable-connectors-in-teams"></a><span data-ttu-id="e631f-181">Activer ou désactiver des connecteurs dans Teams</span><span class="sxs-lookup"><span data-stu-id="e631f-181">Enable or disable connectors in Teams</span></span>

<span data-ttu-id="e631f-182">Le module Exchange Online PowerShell V2 utilise l’authentification moderne et fonctionne avec l’authentification multifacteur, appelée authentification multifacteur, pour la connexion à tous les environnements PowerShell Exchange dans Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="e631f-182">The Exchange Online PowerShell V2 module uses modern authentication and works with multi factor authentication, called MFA for connecting to all Exchange related PowerShell environments in Microsoft 365.</span></span> <span data-ttu-id="e631f-183">Les administrateurs peuvent utiliser Exchange Online PowerShell pour désactiver les connecteurs pour un client entier ou une boîte aux lettres de groupe spécifique, affectant tous les utilisateurs de ce client ou de cette boîte aux lettres.</span><span class="sxs-lookup"><span data-stu-id="e631f-183">Admins can use Exchange Online PowerShell to disable connectors for an entire tenant or a specific group mailbox, affecting all users in that tenant or mailbox.</span></span> <span data-ttu-id="e631f-184">Il n’est pas possible de désactiver pour certains et non pour d’autres.</span><span class="sxs-lookup"><span data-stu-id="e631f-184">It is not possible to disable for some and not others.</span></span> <span data-ttu-id="e631f-185">En outre, les connecteurs sont désactivés par défaut pour Cloud de la communauté du secteur public, appelés Cloud de la communauté du secteur public client.</span><span class="sxs-lookup"><span data-stu-id="e631f-185">Also, connectors are disabled by default for Government Community Cloud, called GCC tenants.</span></span>

<span data-ttu-id="e631f-186">Le paramètre au niveau du client remplace le paramètre au niveau du groupe.</span><span class="sxs-lookup"><span data-stu-id="e631f-186">The tenant level setting overrides the group level setting.</span></span> <span data-ttu-id="e631f-187">Par exemple, si un administrateur active les connecteurs pour le groupe et les désactive sur le client, les connecteurs pour le groupe sont désactivés.</span><span class="sxs-lookup"><span data-stu-id="e631f-187">For example, if an admin enables connectors for the group and disables them on the tenant, connectors for the group is disabled.</span></span> <span data-ttu-id="e631f-188">Pour activer un connecteur dans Teams, connectez-vous [à Exchange Online PowerShell](/powershell/exchange/connect-to-exchange-online-powershell?view=exchange-ps#connect-to-exchange-online-powershell-using-modern-authentication-with-or-without-mfa&preserve-view=true) à l’aide de l’authentification moderne avec ou sans authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="e631f-188">To enable a connector in Teams, [connect to Exchange Online PowerShell](/powershell/exchange/connect-to-exchange-online-powershell?view=exchange-ps#connect-to-exchange-online-powershell-using-modern-authentication-with-or-without-mfa&preserve-view=true) using modern authentication with or without MFA.</span></span>

### <a name="commands-to-enable-or-disable-connectors"></a><span data-ttu-id="e631f-189">Commandes permettant d’activer ou de désactiver des connecteurs</span><span class="sxs-lookup"><span data-stu-id="e631f-189">Commands to enable or disable connectors</span></span>

<span data-ttu-id="e631f-190">Dans Exchange Online PowerShell, exécutez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="e631f-190">Run the following commands in Exchange Online PowerShell:</span></span>

* <span data-ttu-id="e631f-191">Pour désactiver les connecteurs pour le client : `Set-OrganizationConfig -ConnectorsEnabled:$false` .</span><span class="sxs-lookup"><span data-stu-id="e631f-191">To disable connectors for the tenant: `Set-OrganizationConfig -ConnectorsEnabled:$false`.</span></span>
* <span data-ttu-id="e631f-192">Pour désactiver les messages actionnables pour le client : `Set-OrganizationConfig -ConnectorsActionableMessagesEnabled:$false` .</span><span class="sxs-lookup"><span data-stu-id="e631f-192">To disable actionable messages for the tenant: `Set-OrganizationConfig -ConnectorsActionableMessagesEnabled:$false`.</span></span>
* <span data-ttu-id="e631f-193">Pour activer les connecteurs pour Teams, exécutez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="e631f-193">To enable connectors for Teams, run the following commands:</span></span>
  * `Set-OrganizationConfig -ConnectorsEnabled:$true `
  * `Set-OrganizationConfig -ConnectorsEnabledForTeams:$true`
  * `Set-OrganizationConfig -ConnectorsActionableMessagesEnabled:$true`

<span data-ttu-id="e631f-194">Pour plus d’informations sur l’échange de module PowerShell, voir [Set-OrganizationConfig](/powershell/module/exchange/Set-OrganizationConfig?view=exchange-ps&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="e631f-194">For more information on PowerShell module exchange, see [Set-OrganizationConfig](/powershell/module/exchange/Set-OrganizationConfig?view=exchange-ps&preserve-view=true).</span></span> <span data-ttu-id="e631f-195">Pour activer ou désactiver les connecteurs Outlook, [connectez](https://support.microsoft.com/topic/connect-apps-to-your-groups-in-outlook-ed0ce547-038f-4902-b9b3-9e518ae6fbab?ui=en-us&rs=en-us&ad=us)des applications à vos groupes dans Outlook .</span><span class="sxs-lookup"><span data-stu-id="e631f-195">To enable or disable Outlook connectors, [connect apps to your groups in Outlook](https://support.microsoft.com/topic/connect-apps-to-your-groups-in-outlook-ed0ce547-038f-4902-b9b3-9e518ae6fbab?ui=en-us&rs=en-us&ad=us).</span></span>

## <a name="test-your-connector"></a><span data-ttu-id="e631f-196">Tester votre connecteur</span><span class="sxs-lookup"><span data-stu-id="e631f-196">Test your connector</span></span>

<span data-ttu-id="e631f-197">Pour tester votre connecteur, téléchargez-le vers une équipe avec n’importe quelle autre application.</span><span class="sxs-lookup"><span data-stu-id="e631f-197">To test your connector, upload it to a team with any other app.</span></span> <span data-ttu-id="e631f-198">Vous pouvez créer un package .zip à l’aide du fichier manifeste à partir des deux fichiers d’icône et connecteurs du Tableau de bord du développeur, modifié comme indiqué dans Inclure le connecteur dans [votre manifeste.](#include-the-connector-in-your-manifest)</span><span class="sxs-lookup"><span data-stu-id="e631f-198">You can create a .zip package using the manifest file from the two icon files and connectors Developer Dashboard, modified as directed in [Include the connector in your Manifest](#include-the-connector-in-your-manifest).</span></span>

<span data-ttu-id="e631f-199">Après avoir téléchargé l’application, ouvrez la liste des connecteurs à partir de n’importe quel canal.</span><span class="sxs-lookup"><span data-stu-id="e631f-199">After you upload the app, open the connectors list from any channel.</span></span> <span data-ttu-id="e631f-200">Faites défiler vers le bas pour voir votre application dans la section **Téléchargée** :</span><span class="sxs-lookup"><span data-stu-id="e631f-200">Scroll to the bottom to see your app in the **Uploaded** section:</span></span>

![Capture d’écran d’une section téléchargée dans la boîte de dialogue connecteur](~/assets/images/connectors/connector_dialog_uploaded.png)

> [!NOTE]
> <span data-ttu-id="e631f-202">Le flux se produit entièrement au sein Microsoft Teams en tant qu’expérience hébergée.</span><span class="sxs-lookup"><span data-stu-id="e631f-202">The flow occurs entirely within Microsoft Teams as a hosted experience.</span></span>

<span data-ttu-id="e631f-203">Pour vérifier que `HttpPOST` l’action fonctionne correctement, [envoyez des messages à votre connecteur.](~/webhooks-and-connectors/how-to/connectors-using.md)</span><span class="sxs-lookup"><span data-stu-id="e631f-203">To verify that `HttpPOST` action is working correctly, [send messages to your connector](~/webhooks-and-connectors/how-to/connectors-using.md).</span></span>

## <a name="publish-connectors-for-the-organization"></a><span data-ttu-id="e631f-204">Publier des connecteurs pour l’organisation</span><span class="sxs-lookup"><span data-stu-id="e631f-204">Publish connectors for the organization</span></span>

<span data-ttu-id="e631f-205">Si vous souhaitez que le connecteur soit disponible uniquement pour les utilisateurs de votre organisation, vous pouvez télécharger votre application de connecteur personnalisée dans le catalogue [d’applications de votre organisation.](~/concepts/deploy-and-publish/apps-publish.md)</span><span class="sxs-lookup"><span data-stu-id="e631f-205">If you want the connector to be available only to the users in your organization, you can upload your custom connector app to your [organization's app catalog](~/concepts/deploy-and-publish/apps-publish.md).</span></span>

<span data-ttu-id="e631f-206">Après avoir téléchargé le package d’application pour configurer et utiliser le connecteur dans une équipe, installez le connecteur à partir du catalogue d’applications de l’organisation.</span><span class="sxs-lookup"><span data-stu-id="e631f-206">After uploading the app package to configure and use the connector in a team, install the connector from the organization's app catalog.</span></span>

<span data-ttu-id="e631f-207">**Pour configurer un connecteur**</span><span class="sxs-lookup"><span data-stu-id="e631f-207">**To set up a connector**</span></span>

1. <span data-ttu-id="e631f-208">Sélectionnez **Applications** dans la barre de navigation de gauche.</span><span class="sxs-lookup"><span data-stu-id="e631f-208">Select **Apps** from the left navigation bar.</span></span>
1. <span data-ttu-id="e631f-209">Dans la section **Applications,** sélectionnez **Connecteurs.**</span><span class="sxs-lookup"><span data-stu-id="e631f-209">In the **Apps** section, select **Connectors**.</span></span>
1. <span data-ttu-id="e631f-210">Sélectionnez le connecteur que vous souhaitez ajouter.</span><span class="sxs-lookup"><span data-stu-id="e631f-210">Select the connector that you want to add.</span></span> <span data-ttu-id="e631f-211">Une fenêtre de boîte de dialogue s’affiche.</span><span class="sxs-lookup"><span data-stu-id="e631f-211">A pop up dialog window appears.</span></span>
1. <span data-ttu-id="e631f-212">Dans le menu déroulant, **sélectionnez Ajouter à une équipe.**</span><span class="sxs-lookup"><span data-stu-id="e631f-212">From the dropdown menu, select **Add to a team**.</span></span>
1. <span data-ttu-id="e631f-213">Dans la zone de recherche, tapez un nom d’équipe ou de canal.</span><span class="sxs-lookup"><span data-stu-id="e631f-213">In the search box, type a team or channel name.</span></span>
1. <span data-ttu-id="e631f-214">Sélectionnez **Configurer un connecteur dans** le menu déroulant dans le coin inférieur droit de la fenêtre de dialogue.</span><span class="sxs-lookup"><span data-stu-id="e631f-214">Select **Set up a Connector** from the dropdown menu in the bottom right corner of the dialog window.</span></span>

<span data-ttu-id="e631f-215">Le connecteur est disponible dans la section &#9679;&#9679;&#9679; > **Plus d’options** Connecteurs Tous les connecteurs pour  >    >    >  **votre** équipe pour cette équipe.</span><span class="sxs-lookup"><span data-stu-id="e631f-215">The connector is available in the section &#9679;&#9679;&#9679; > **More options** > **Connectors** > **All** > **Connectors for your team** for that team.</span></span> <span data-ttu-id="e631f-216">Vous pouvez naviguer en accédant à cette section ou rechercher l’application connecteur.</span><span class="sxs-lookup"><span data-stu-id="e631f-216">You can navigate by scrolling to this section or search for the connector app.</span></span> <span data-ttu-id="e631f-217">Pour configurer ou modifier le connecteur, sélectionnez **Configurer**.</span><span class="sxs-lookup"><span data-stu-id="e631f-217">To configure or modify the connector, select **Configure**.</span></span>

## <a name="distribute-webhook-and-connector"></a><span data-ttu-id="e631f-218">Distribuer un webhook et un connecteur</span><span class="sxs-lookup"><span data-stu-id="e631f-218">Distribute webhook and connector</span></span>

1. <span data-ttu-id="e631f-219">[Configurer un webhook entrant](~/webhooks-and-connectors/how-to/add-incoming-webhook.md?branch=pr-en-us-3076#create-incoming-webhook) directement pour votre équipe.</span><span class="sxs-lookup"><span data-stu-id="e631f-219">[Set up an Incoming Webhook](~/webhooks-and-connectors/how-to/add-incoming-webhook.md?branch=pr-en-us-3076#create-incoming-webhook) directly for your team.</span></span>
1. <span data-ttu-id="e631f-220">Ajoutez [une page de configuration](~/webhooks-and-connectors/how-to/connectors-creating.md?branch=pr-en-us-3076#integrate-the-configuration-experience) et [publiez votre webhook entrant](~/webhooks-and-connectors/how-to/connectors-creating.md?branch=pr-en-us-3076#publish-connectors-for-the-organization) dans un connecteur O365.</span><span class="sxs-lookup"><span data-stu-id="e631f-220">Add a [configuration page](~/webhooks-and-connectors/how-to/connectors-creating.md?branch=pr-en-us-3076#integrate-the-configuration-experience) and [publish your Incoming Webhook](~/webhooks-and-connectors/how-to/connectors-creating.md?branch=pr-en-us-3076#publish-connectors-for-the-organization) in a O365 Connector.</span></span>
1. <span data-ttu-id="e631f-221">Packagez et publiez votre connecteur dans le cadre de [votre soumission AppSource.](~/concepts/deploy-and-publish/office-store-guidance.md)</span><span class="sxs-lookup"><span data-stu-id="e631f-221">Package and publish your connector as part of your [AppSource](~/concepts/deploy-and-publish/office-store-guidance.md) submission.</span></span>

## <a name="code-sample"></a><span data-ttu-id="e631f-222">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="e631f-222">Code sample</span></span>

<span data-ttu-id="e631f-223">Le tableau suivant fournit le nom de l’exemple et sa description :</span><span class="sxs-lookup"><span data-stu-id="e631f-223">The following table provides the sample name and its description:</span></span>

|<span data-ttu-id="e631f-224">**Exemple de nom**</span><span class="sxs-lookup"><span data-stu-id="e631f-224">**Sample name**</span></span> | <span data-ttu-id="e631f-225">**Description**</span><span class="sxs-lookup"><span data-stu-id="e631f-225">**Description**</span></span> | <span data-ttu-id="e631f-226">**.NET**</span><span class="sxs-lookup"><span data-stu-id="e631f-226">**.NET**</span></span> | <span data-ttu-id="e631f-227">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="e631f-227">**Node.js**</span></span> |
|----------------|------------------|--------|----------------|
| <span data-ttu-id="e631f-228">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="e631f-228">Connectors</span></span>    | <span data-ttu-id="e631f-229">Exemple Office 365 connecteur générant des notifications vers Teams canal.</span><span class="sxs-lookup"><span data-stu-id="e631f-229">Sample Office 365 Connector generating notifications to Teams channel.</span></span>|   [<span data-ttu-id="e631f-230">View</span><span class="sxs-lookup"><span data-stu-id="e631f-230">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-todo-notification/csharp) | [<span data-ttu-id="e631f-231">View</span><span class="sxs-lookup"><span data-stu-id="e631f-231">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-github-notification/nodejs)|
| <span data-ttu-id="e631f-232">Exemple de connecteurs génériques</span><span class="sxs-lookup"><span data-stu-id="e631f-232">Generic connectors sample</span></span> |<span data-ttu-id="e631f-233">Exemple de code pour un connecteur générique facile à personnaliser pour tout système qui prend en charge les webhooks.</span><span class="sxs-lookup"><span data-stu-id="e631f-233">Sample code for a generic connector that is easy to customize for any system that supports webhooks.</span></span>|  | [<span data-ttu-id="e631f-234">View</span><span class="sxs-lookup"><span data-stu-id="e631f-234">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-generic/nodejs)|

## <a name="see-also"></a><span data-ttu-id="e631f-235">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="e631f-235">See also</span></span>

* [<span data-ttu-id="e631f-236">Créer et envoyer des messages</span><span class="sxs-lookup"><span data-stu-id="e631f-236">Create and send messages</span></span>](~/webhooks-and-connectors/how-to/connectors-using.md)
* [<span data-ttu-id="e631f-237">Créer un webhook entrant</span><span class="sxs-lookup"><span data-stu-id="e631f-237">Create an Incoming Webhook</span></span>](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [<span data-ttu-id="e631f-238">Créer un connecteur Office 365</span><span class="sxs-lookup"><span data-stu-id="e631f-238">Create an Office 365 Connector</span></span>](~/webhooks-and-connectors/how-to/connectors-creating.md)
