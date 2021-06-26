---
title: Obtenir un contexte Teams pour votre onglet
description: Décrit comment obtenir du contexte utilisateur dans vos onglets
localization_priority: Normal
ms.topic: how-to
keywords: Contexte utilisateur sous l’onglet Équipes
ms.openlocfilehash: 29f574ae924ddde52b63590aba3fcc06a3d446af
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140277"
---
# <a name="get-context-for-your-tab"></a><span data-ttu-id="d8d98-104">Obtenir un contexte Teams pour votre onglet</span><span class="sxs-lookup"><span data-stu-id="d8d98-104">Get context for your tab</span></span>

<span data-ttu-id="d8d98-105">Votre onglet nécessite des informations contextuelles pour afficher le contenu pertinent :</span><span class="sxs-lookup"><span data-stu-id="d8d98-105">Your tab requires contextual information to display relevant content:</span></span>

* <span data-ttu-id="d8d98-106">Informations de base sur l’utilisateur, l’équipe ou l’entreprise.</span><span class="sxs-lookup"><span data-stu-id="d8d98-106">Basic information about the user, team, or company.</span></span>
* <span data-ttu-id="d8d98-107">Informations sur les paramètres régionaux et le thème.</span><span class="sxs-lookup"><span data-stu-id="d8d98-107">Locale and theme information.</span></span>
* <span data-ttu-id="d8d98-108">Lisez `entityId` ou identifie ce qui se trouve dans cet `subEntityId` onglet.</span><span class="sxs-lookup"><span data-stu-id="d8d98-108">Read the `entityId` or `subEntityId` that identifies what is in this tab.</span></span>

## <a name="user-context"></a><span data-ttu-id="d8d98-109">Contexte utilisateur</span><span class="sxs-lookup"><span data-stu-id="d8d98-109">User context</span></span>

<span data-ttu-id="d8d98-110">Le contexte de l’utilisateur, de l’équipe ou de l’entreprise peut être particulièrement utile lorsque :</span><span class="sxs-lookup"><span data-stu-id="d8d98-110">Context about the user, team, or company can be especially useful when:</span></span>

* <span data-ttu-id="d8d98-111">Vous créez ou associez des ressources dans votre application à l’utilisateur ou à l’équipe spécifié.</span><span class="sxs-lookup"><span data-stu-id="d8d98-111">You create or associate resources in your app with the specified user or team.</span></span>
* <span data-ttu-id="d8d98-112">Vous lancez un flux d’authentification à partir de Azure Active Directory (AAD) ou d’un autre fournisseur d’identité, et vous n’avez pas besoin que l’utilisateur entre à nouveau son nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d8d98-112">You initiate an authentication flow from Azure Active Directory (AAD) or other identity provider, and you do not require the user to enter their username again.</span></span> <span data-ttu-id="d8d98-113">Pour plus d’informations, [voir authentifier un utilisateur dans Microsoft Teams onglet .](~/concepts/authentication/authentication.md)</span><span class="sxs-lookup"><span data-stu-id="d8d98-113">For more information, see [authenticate a user in your Microsoft Teams tab](~/concepts/authentication/authentication.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d8d98-114">Bien que ces informations utilisateur contribuent à une expérience utilisateur fluide, vous ne devez pas les utiliser comme preuve d’identité.</span><span class="sxs-lookup"><span data-stu-id="d8d98-114">Although this user information can help provide a smooth user experience, you must not use it as proof of identity.</span></span> <span data-ttu-id="d8d98-115">Par exemple, un attaquant peut charger votre page dans un navigateur et restituer des informations ou des demandes dangereuses.</span><span class="sxs-lookup"><span data-stu-id="d8d98-115">For example, an attacker can load your page in a browser and render harmful information or requests.</span></span>

## <a name="access-context-information"></a><span data-ttu-id="d8d98-116">Accéder aux informations de contexte</span><span class="sxs-lookup"><span data-stu-id="d8d98-116">Access context information</span></span>

<span data-ttu-id="d8d98-117">Vous pouvez accéder aux informations de contexte de deux façons :</span><span class="sxs-lookup"><span data-stu-id="d8d98-117">You can access context information in two ways:</span></span>

* <span data-ttu-id="d8d98-118">Insérez des valeurs d’espace réservé d’URL.</span><span class="sxs-lookup"><span data-stu-id="d8d98-118">Insert URL placeholder values.</span></span>
* <span data-ttu-id="d8d98-119">Utilisez le [Microsoft Teams SDK client JavaScript.](/javascript/api/overview/msteams-client)</span><span class="sxs-lookup"><span data-stu-id="d8d98-119">Use the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client).</span></span>

### <a name="get-context-by-inserting-url-placeholder-values"></a><span data-ttu-id="d8d98-120">Obtenir le contexte en insérant des valeurs d’espace réservé d’URL</span><span class="sxs-lookup"><span data-stu-id="d8d98-120">Get context by inserting URL placeholder values</span></span>

<span data-ttu-id="d8d98-121">Utilisez des espaces réservés dans vos URL de configuration ou de contenu.</span><span class="sxs-lookup"><span data-stu-id="d8d98-121">Use placeholders in your configuration or content URLs.</span></span> <span data-ttu-id="d8d98-122">Microsoft Teams remplace les espaces réservés par les valeurs appropriées lorsqu’il détermine l’URL de configuration ou de contenu.</span><span class="sxs-lookup"><span data-stu-id="d8d98-122">Microsoft Teams replaces the placeholders with the relevant values when determining the actual configuration or content URL.</span></span> <span data-ttu-id="d8d98-123">Les espaces réservé disponibles incluent tous les champs de [l’objet](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) de contexte.</span><span class="sxs-lookup"><span data-stu-id="d8d98-123">The available placeholders include all fields on the [context](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) object.</span></span> <span data-ttu-id="d8d98-124">Voici les scénarios les plus courants :</span><span class="sxs-lookup"><span data-stu-id="d8d98-124">Common placeholders include the following:</span></span>

* <span data-ttu-id="d8d98-125">{entityId} : ID que vous avez fourni pour l’élément dans cet onglet lors de la première [configuration de l’onglet](~/tabs/how-to/create-tab-pages/configuration-page.md).</span><span class="sxs-lookup"><span data-stu-id="d8d98-125">{entityId}: The ID you supplied for the item in this tab when first [configuring the tab](~/tabs/how-to/create-tab-pages/configuration-page.md).</span></span>
* <span data-ttu-id="d8d98-126">{subEntityId}: ID que vous [avez](~/concepts/build-and-test/deep-links.md) fourni lors de la génération d’un lien profond pour un élément spécifique dans cet onglet. Cela doit être utilisé pour restaurer un état spécifique au sein d’une entité ; par exemple, le défilement vers ou l’activation d’un élément de contenu spécifique.</span><span class="sxs-lookup"><span data-stu-id="d8d98-126">{subEntityId}: The ID you supplied when generating a [deep link](~/concepts/build-and-test/deep-links.md) for a specific item within this tab. This must be used to restore to a specific state within an entity; for example, scrolling to or activating a specific piece of content.</span></span>
* <span data-ttu-id="d8d98-127">{loginHint}: valeur appropriée comme conseil de connexion pour AAD.</span><span class="sxs-lookup"><span data-stu-id="d8d98-127">{loginHint}: A value suitable as a login hint for AAD.</span></span> <span data-ttu-id="d8d98-128">Il s’agit généralement du nom de connexion de l’utilisateur actuel dans son client d’accueil.</span><span class="sxs-lookup"><span data-stu-id="d8d98-128">This is usually the login name of the current user in their home tenant.</span></span>
* <span data-ttu-id="d8d98-129">{userPrincipalName} : nom d’utilisateur principal de l’utilisateur actuel dans le client actuel.</span><span class="sxs-lookup"><span data-stu-id="d8d98-129">{userPrincipalName}: The User Principal Name of the current user in the current tenant.</span></span>
* <span data-ttu-id="d8d98-130">{userObjectId}: ID d’objet AAD de l’utilisateur actuel dans le client actuel.</span><span class="sxs-lookup"><span data-stu-id="d8d98-130">{userObjectId}: The AAD object ID of the current user in the current tenant.</span></span>
* <span data-ttu-id="d8d98-131">{theme}: Le thème de l’interface utilisateur actuelle (IU) tel `default` que , `dark` ou `contrast` .</span><span class="sxs-lookup"><span data-stu-id="d8d98-131">{theme}: The current user interface (UI) theme such as `default`, `dark`, or `contrast`.</span></span>
* <span data-ttu-id="d8d98-132">{groupId}: ID du groupe Office 365 dans lequel réside l’onglet.</span><span class="sxs-lookup"><span data-stu-id="d8d98-132">{groupId}: The ID of the Office 365 group in which the tab resides.</span></span>
* <span data-ttu-id="d8d98-133">{tid}: ID de client AAD de l’utilisateur actuel.</span><span class="sxs-lookup"><span data-stu-id="d8d98-133">{tid}: The AAD tenant ID of the current user.</span></span>
* <span data-ttu-id="d8d98-134">{locale}: paramètres régionaux actuels de l’utilisateur au format languageId-countryId.</span><span class="sxs-lookup"><span data-stu-id="d8d98-134">{locale}: The current locale of the user formatted as languageId-countryId.</span></span> <span data-ttu-id="d8d98-135">Par exemple, en-us.</span><span class="sxs-lookup"><span data-stu-id="d8d98-135">For example, en-us.</span></span>

> [!NOTE]
> <span data-ttu-id="d8d98-136">L’espace réservé `{upn}`précédent est désormais supprimé.</span><span class="sxs-lookup"><span data-stu-id="d8d98-136">The previous `{upn}` placeholder is now deprecated.</span></span> <span data-ttu-id="d8d98-137">Pour des raisons de compatibilité ascendante, il s'agit actuellement d'un synonyme de `{loginHint}`.</span><span class="sxs-lookup"><span data-stu-id="d8d98-137">For backward compatibility, it is currently a synonym for `{loginHint}`.</span></span>

<span data-ttu-id="d8d98-138">Par exemple, dans votre manifeste d’onglet, vous définissez l’attribut sur , l’utilisateur qui est inscrit `configURL` `"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"` possède les attributs suivants :</span><span class="sxs-lookup"><span data-stu-id="d8d98-138">For example, in your tab manifest you set the `configURL` attribute to `"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"`, the signed-in user has the following attributes:</span></span>

* <span data-ttu-id="d8d98-139">Leur nom d’utilisateur **est user@example.com**.</span><span class="sxs-lookup"><span data-stu-id="d8d98-139">Their username is **user@example.com**.</span></span>
* <span data-ttu-id="d8d98-140">Leur ID de locataire d’entreprise **est e2653c-etc.**</span><span class="sxs-lookup"><span data-stu-id="d8d98-140">Their company tenant ID is **e2653c-etc**.</span></span>
* <span data-ttu-id="d8d98-141">Ils sont membres du groupe Office 365 avec l’ID **00209384-etc.**</span><span class="sxs-lookup"><span data-stu-id="d8d98-141">They are a member of the Office 365 group with id **00209384-etc**.</span></span>
* <span data-ttu-id="d8d98-142">L’utilisateur a Teams thème **foncé.**</span><span class="sxs-lookup"><span data-stu-id="d8d98-142">The user has set their Teams theme to **dark**.</span></span>

<span data-ttu-id="d8d98-143">Lorsqu’ils configurent l’onglet, Teams appelle l’URL suivante :</span><span class="sxs-lookup"><span data-stu-id="d8d98-143">When they configure the tab, Teams calls the following URL:</span></span>

`https://www.contoso.com/config?name=user@example.com&tenant=e2653c-etc&group=00209384-etc&theme=dark`

### <a name="get-context-by-using-the-microsoft-teams-javascript-library"></a><span data-ttu-id="d8d98-144">Obtenir du contexte à l’aide de Microsoft Teams bibliothèque JavaScript</span><span class="sxs-lookup"><span data-stu-id="d8d98-144">Get context by using the Microsoft Teams JavaScript library</span></span>

<span data-ttu-id="d8d98-145">Vous pouvez également extraire les informations mentionnées ci-dessus à l’aide du client [Microsoft Teams JavaScript Client SDK](/javascript/api/overview/msteams-client) en appelant `microsoftTeams.getContext(function(context) { /* ... */ })`.</span><span class="sxs-lookup"><span data-stu-id="d8d98-145">You can also retrieve the information listed above using the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client) by calling `microsoftTeams.getContext(function(context) { /* ... */ })`.</span></span>

<span data-ttu-id="d8d98-146">Le code suivant fournit un exemple de variable de contexte :</span><span class="sxs-lookup"><span data-stu-id="d8d98-146">The following code provides an example of context variable:</span></span>

```json
{
    "teamId": "The Microsoft Teams ID in the format 19:[id]@thread.skype",
    "teamName": "The name of the current team",
    "channelId": "The channel ID in the format 19:[id]@thread.skype",
    "channelName": "The name of the current channel",
    "chatId": "The chat ID in the format 19:[id]@thread.skype",
    "locale": "The current locale of the user formatted as languageId-countryId (for example, en-us)",
    "entityId": "The developer-defined unique ID for the entity this content points to",
    "subEntityId": "The developer-defined unique ID for the sub-entity this content points to",
    "loginHint": "A value suitable as a login hint for Azure AD. This is usually the login name of the current user, in their home tenant",
    "userPrincipalName": "The principal name of the current user, in the current tenant",
    "userObjectId": "The Azure AD object id of the current user, in the current tenant",
    "tid": "The Azure AD tenant ID of the current user",
    "groupId": "Guid identifying the current O365 Group ID",
    "theme": "The current UI theme: default | dark | contrast",
    "isFullScreen": "Indicates if the tab is in full-screen",
    "teamType": "The type of team",
    "teamSiteUrl": "The root SharePoint site associated with the team",
    "teamSiteDomain": "The domain of the root SharePoint site associated with the team",
    "teamSitePath": "The relative path to the SharePoint site associated with the team",
    "channelRelativeUrl": "The relative path to the SharePoint folder associated with the channel",
    "sessionId": "The unique ID for the current Teams session for use in correlating telemetry data",
    "userTeamRole": "The user's role in the team",
    "isTeamArchived": "Indicates if team is archived",
    "hostClientType": "The type of host client. Possible values are android, ios, web, desktop, rigel",
    "frameContext": "The context where tab URL is loaded (for example, content, task, setting, remove, sidePanel)",
    "sharepoint": "The SharePoint context is available only when hosted in SharePoint",
    "tenantSKU": "The license type for the current user tenant. Possible values are enterprise, free, edu, unknown",
    "userLicenseType": "The license type for the current user",
    "parentMessageId": "The parent message ID from which this task module is launched",
    "ringId": "The current ring ID",
    "appSessionId": "The unique ID for the current session used for correlating telemetry data",
    "isCallingAllowed": "Indicates if calling is allowed for the current logged in user",
    "isPSTNCallingAllowed": "Indicates if PSTN calling is allowed for the current logged in user",
    "meetingId": "The meeting ID used by tab when running in meeting context",
    "defaultOneNoteSectionId": "The OneNote section ID that is linked to the channel"
}
```

## <a name="retrieve-context-in-private-channels"></a><span data-ttu-id="d8d98-147">Récupérer le contexte dans les canaux privés</span><span class="sxs-lookup"><span data-stu-id="d8d98-147">Retrieve context in private channels</span></span>

> [!Note]
> <span data-ttu-id="d8d98-148">Les canaux privés sont actuellement en prévisualisation du développeur privé.</span><span class="sxs-lookup"><span data-stu-id="d8d98-148">Private channels are currently in private developer preview.</span></span>

<span data-ttu-id="d8d98-149">Lorsque votre page de contenu est chargée dans un canal privé, les données que vous recevez de l’appel sont obscurcies pour protéger la confidentialité `getContext` du canal.</span><span class="sxs-lookup"><span data-stu-id="d8d98-149">When your content page is loaded in a private channel, the data you receive from the `getContext` call is obfuscated to protect the privacy of the channel.</span></span> <span data-ttu-id="d8d98-150">Les champs suivants sont modifiés lorsque votre page de contenu se trouve dans un canal privé :</span><span class="sxs-lookup"><span data-stu-id="d8d98-150">The following fields are changed when your content page is in a private channel:</span></span>

* <span data-ttu-id="d8d98-151">`groupId`: Non définie pour les canaux privés</span><span class="sxs-lookup"><span data-stu-id="d8d98-151">`groupId`: Undefined for private channels</span></span>
* <span data-ttu-id="d8d98-152">`teamId`: définir sur le threadId du canal privé</span><span class="sxs-lookup"><span data-stu-id="d8d98-152">`teamId`: Set to the threadId of the private channel</span></span>
* <span data-ttu-id="d8d98-153">`teamName`: Définir sur le nom du canal privé</span><span class="sxs-lookup"><span data-stu-id="d8d98-153">`teamName`: Set to the name of the private channel</span></span>
* <span data-ttu-id="d8d98-154">`teamSiteUrl`: Définir sur l’URL d’un site SharePoint distinct et unique pour le canal privé</span><span class="sxs-lookup"><span data-stu-id="d8d98-154">`teamSiteUrl`: Set to the URL of a distinct, unique SharePoint site for the private channel</span></span>
* <span data-ttu-id="d8d98-155">`teamSitePath`: Définir sur le chemin d’accès d’un site SharePoint distinct et unique pour le canal privé</span><span class="sxs-lookup"><span data-stu-id="d8d98-155">`teamSitePath`: Set to the path of a distinct, unique SharePoint site for the private channel</span></span>
* <span data-ttu-id="d8d98-156">`teamSiteDomain`: Définir sur le domaine d’un domaine de site SharePoint unique et distinct pour le canal privé</span><span class="sxs-lookup"><span data-stu-id="d8d98-156">`teamSiteDomain`: Set to the domain of a distinct, unique SharePoint site domain for the private channel</span></span>

<span data-ttu-id="d8d98-157">Si votre page utilise l’une de ces valeurs, vous devez vérifier le champ pour déterminer si votre page est chargée dans un canal privé et y `channelType` répondre de manière appropriée.</span><span class="sxs-lookup"><span data-stu-id="d8d98-157">If your page makes use of any of these values, you must check the `channelType` field to determine if your page is loaded in a private channel and respond appropriately.</span></span>

> [!Note]
> <span data-ttu-id="d8d98-158">`teamSiteUrl` fonctionne également bien pour les canaux standard.</span><span class="sxs-lookup"><span data-stu-id="d8d98-158">`teamSiteUrl` also works well for standard channels.</span></span>

## <a name="handle-theme-change"></a><span data-ttu-id="d8d98-159">Gérer la modification du thème</span><span class="sxs-lookup"><span data-stu-id="d8d98-159">Handle theme change</span></span>

<span data-ttu-id="d8d98-160">Vous pouvez inscrire votre application pour être informée si le thème change en `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })` appelant.</span><span class="sxs-lookup"><span data-stu-id="d8d98-160">You can register your app to be informed if the theme changes by calling `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })`.</span></span>

<span data-ttu-id="d8d98-161">`theme`L’argument dans la fonction est une chaîne avec une valeur de , ou `default` `dark` `contrast` .</span><span class="sxs-lookup"><span data-stu-id="d8d98-161">The `theme` argument in the function is a string with a value of `default`, `dark`, or `contrast`.</span></span>

## <a name="see-also"></a><span data-ttu-id="d8d98-162">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="d8d98-162">See also</span></span>

* [<span data-ttu-id="d8d98-163">Recommandations en matière de conception d’onglets</span><span class="sxs-lookup"><span data-stu-id="d8d98-163">Tab design guidelines</span></span>](~/tabs/how-to/build-adaptive-card-tabs.md)
* [<span data-ttu-id="d8d98-164">Teams onglets</span><span class="sxs-lookup"><span data-stu-id="d8d98-164">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="d8d98-165">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="d8d98-165">Prerequisites</span></span>](~/tabs/how-to/tab-requirements.md)
* [<span data-ttu-id="d8d98-166">Créer un onglet personnel</span><span class="sxs-lookup"><span data-stu-id="d8d98-166">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
* [<span data-ttu-id="d8d98-167">Créer un onglet de canal ou de groupe</span><span class="sxs-lookup"><span data-stu-id="d8d98-167">Create a channel or group tab</span></span>](~/tabs/how-to/create-channel-group-tab.md)
* [<span data-ttu-id="d8d98-168">Créer une page de contenu</span><span class="sxs-lookup"><span data-stu-id="d8d98-168">Create a content page</span></span>](~/tabs/how-to/create-tab-pages/content-page.md)
* [<span data-ttu-id="d8d98-169">Créer une page de configuration</span><span class="sxs-lookup"><span data-stu-id="d8d98-169">Create a configuration page</span></span>](~/tabs/how-to/create-tab-pages/configuration-page.md)
* [<span data-ttu-id="d8d98-170">Créer une page de suppression pour votre onglet</span><span class="sxs-lookup"><span data-stu-id="d8d98-170">Create a removal page for your tab</span></span>](~/tabs/how-to/create-tab-pages/removal-page.md)
* [<span data-ttu-id="d8d98-171">Onglets sur les appareils mobiles</span><span class="sxs-lookup"><span data-stu-id="d8d98-171">Tabs on mobile</span></span>](~/tabs/design/tabs-mobile.md)
* [<span data-ttu-id="d8d98-172">Déploiement du lien des onglets et vue des étapes</span><span class="sxs-lookup"><span data-stu-id="d8d98-172">Tabs link unfurling and Stage View</span></span>](~/tabs/tabs-link-unfurling.md)
* [<span data-ttu-id="d8d98-173">Créer des onglets de conversation</span><span class="sxs-lookup"><span data-stu-id="d8d98-173">Create conversational tabs</span></span>](~/tabs/how-to/conversational-tabs.md)
* [<span data-ttu-id="d8d98-174">Modifications des marges de l’onglet</span><span class="sxs-lookup"><span data-stu-id="d8d98-174">Tab margin changes</span></span>](~/resources/removing-tab-margins.md)

## <a name="next-step"></a><span data-ttu-id="d8d98-175">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="d8d98-175">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d8d98-176">Créer des onglets avec les Cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="d8d98-176">Build tabs with Adaptive Cards</span></span>](~/tabs/how-to/build-adaptive-card-tabs.md)