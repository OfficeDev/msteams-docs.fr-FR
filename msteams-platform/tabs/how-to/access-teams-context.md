---
title: Obtenir un contexte Teams pour votre onglet
description: Décrit comment obtenir du contexte utilisateur dans vos onglets
localization_priority: Normal
ms.topic: how-to
keywords: Contexte utilisateur sous l’onglet Équipes
ms.openlocfilehash: 0d9224a941ae4f6a5ad125c93d5877ec49b6df28
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566865"
---
# <a name="get-context-for-your-microsoft-teams-tab"></a><span data-ttu-id="dbb41-104">Obtenir un contexte pour votre onglet Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="dbb41-104">Get context for your Microsoft Teams tab</span></span>

<span data-ttu-id="dbb41-105">Votre onglet doit exiger des informations contextuelles pour afficher le contenu pertinent :</span><span class="sxs-lookup"><span data-stu-id="dbb41-105">Your tab must require contextual information to display relevant content:</span></span>

* <span data-ttu-id="dbb41-106">Informations de base sur l’utilisateur, l’équipe ou l’entreprise.</span><span class="sxs-lookup"><span data-stu-id="dbb41-106">Basic information about the user, team, or company.</span></span>
* <span data-ttu-id="dbb41-107">Informations locales et thématiques.</span><span class="sxs-lookup"><span data-stu-id="dbb41-107">Locale and theme information.</span></span>
* <span data-ttu-id="dbb41-108">Lisez le `entityId` ou qui identifie ce qui est dans cet `subEntityId` onglet.</span><span class="sxs-lookup"><span data-stu-id="dbb41-108">Read the `entityId` or `subEntityId` that identifies what is in this tab.</span></span>

## <a name="user-context"></a><span data-ttu-id="dbb41-109">Contexte utilisateur</span><span class="sxs-lookup"><span data-stu-id="dbb41-109">User context</span></span>

<span data-ttu-id="dbb41-110">Le contexte de l’utilisateur, de l’équipe ou de l’entreprise peut être particulièrement utile lorsque :</span><span class="sxs-lookup"><span data-stu-id="dbb41-110">Context about the user, team or company can be especially useful when:</span></span>

* <span data-ttu-id="dbb41-111">Vous créez ou associez des ressources de votre application à l’utilisateur ou à l’équipe spécifié.</span><span class="sxs-lookup"><span data-stu-id="dbb41-111">You create or associate resources in your app with the specified user or team.</span></span>
* <span data-ttu-id="dbb41-112">Vous lancez un flux d’authentification contre Azure Active Directory ou un autre fournisseur d’identité, et vous ne souhaitez pas exiger de l’utilisateur qu’il entre à nouveau son nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="dbb41-112">You initiate an authentication flow against Azure Active Directory or other identity provider, and you don't want to require the user to enter their username again.</span></span> <span data-ttu-id="dbb41-113">Pour plus d’informations sur l’authentification Microsoft Teams onglet, voir [Authentifier un utilisateur dans votre onglet Microsoft Teams’utilisateur](~/concepts/authentication/authentication.md).</span><span class="sxs-lookup"><span data-stu-id="dbb41-113">For more information on authenticating within your Microsoft Teams tab, see [Authenticate a user in your Microsoft Teams tab](~/concepts/authentication/authentication.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dbb41-114">Bien que ces informations utilisateur contribuent à faciliter l’expérience utilisateur, vous ne devez *pas* l’utiliser comme preuve d’identité.</span><span class="sxs-lookup"><span data-stu-id="dbb41-114">Although this user information can help provide a smooth user experience, you should *not* use it as proof of identity.</span></span> <span data-ttu-id="dbb41-115">Par exemple, un utilisateur malveillant peut charger votre page dans un « navigateur malveillant » et rendre des informations ou demandes potentiellement dangereuses.</span><span class="sxs-lookup"><span data-stu-id="dbb41-115">For example, an attacker could load your page in a "bad browser" and render harmful information or requests.</span></span>

## <a name="accessing-context"></a><span data-ttu-id="dbb41-116">Accès au contexte</span><span class="sxs-lookup"><span data-stu-id="dbb41-116">Accessing context</span></span>

<span data-ttu-id="dbb41-117">Vous pouvez accéder aux informations de contexte de deux façons :</span><span class="sxs-lookup"><span data-stu-id="dbb41-117">You can access context information in two ways:</span></span>

* <span data-ttu-id="dbb41-118">Insérez les valeurs de placeholder URL.</span><span class="sxs-lookup"><span data-stu-id="dbb41-118">Insert URL placeholder values.</span></span>
* <span data-ttu-id="dbb41-119">Utilisez le [Microsoft Teams client JavaScript SDK](/javascript/api/overview/msteams-client).</span><span class="sxs-lookup"><span data-stu-id="dbb41-119">Use the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client).</span></span>

### <a name="getting-context-by-inserting-url-placeholder-values"></a><span data-ttu-id="dbb41-120">Obtenir du contexte en insérant des valeurs d’espace réservé d’URL</span><span class="sxs-lookup"><span data-stu-id="dbb41-120">Getting context by inserting URL placeholder values</span></span>

<span data-ttu-id="dbb41-121">Utilisez des espaces réservés dans vos URL de configuration ou de contenu.</span><span class="sxs-lookup"><span data-stu-id="dbb41-121">Use placeholders in your configuration or content URLs.</span></span> <span data-ttu-id="dbb41-122">Microsoft Teams remplace les espaces réservés par les valeurs appropriées lorsqu’il détermine l’URL de configuration ou de contenu.</span><span class="sxs-lookup"><span data-stu-id="dbb41-122">Microsoft Teams replaces the placeholders with the relevant values when determining the actual configuration or content URL.</span></span> <span data-ttu-id="dbb41-123">Les espaces réservé disponibles incluent tous les champs de l’objet [Contexte](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="dbb41-123">The available placeholders include all fields on the [Context](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) object.</span></span> <span data-ttu-id="dbb41-124">Voici les scénarios les plus courants :</span><span class="sxs-lookup"><span data-stu-id="dbb41-124">Common placeholders include the following:</span></span>

* <span data-ttu-id="dbb41-125">{entityId} : ID que vous avez fourni pour l’élément dans cet onglet lors de la première [configuration de l’onglet](~/tabs/how-to/create-tab-pages/configuration-page.md).</span><span class="sxs-lookup"><span data-stu-id="dbb41-125">{entityId}: The ID you supplied for the item in this tab when first [configuring the tab](~/tabs/how-to/create-tab-pages/configuration-page.md).</span></span>
* <span data-ttu-id="dbb41-126">{subEntityId} : ID que vous avez fourni lors de la génération d’un [lien ciblé](~/concepts/build-and-test/deep-links.md) pour un élément spécifique _dans_ cet onglet. Elle doit être utilisée pour restaurer un état spécifique au sein d’une entité. par exemple, le défilement vers un contenu spécifique ou l’activation d’un contenu spécifique.</span><span class="sxs-lookup"><span data-stu-id="dbb41-126">{subEntityId}: The ID you supplied when generating a [deep link](~/concepts/build-and-test/deep-links.md) for a specific item _within_ this tab. This should be used to restore to a specific state within an entity; for example, scrolling to or activating a specific piece of content.</span></span>
* <span data-ttu-id="dbb41-127">{loginHint} : valeur appropriée comme indication de connexion pour Azure AD. Il s’agit généralement du nom de connexion de l’utilisateur actuel, dans son client.</span><span class="sxs-lookup"><span data-stu-id="dbb41-127">{loginHint}: A value suitable as a login hint for Azure AD.This is usually the login name of the current user, in their home tenant.</span></span>
* <span data-ttu-id="dbb41-128">{userPrincipalName} : nom d’utilisateur principal de l’utilisateur actuel, dans le client actuel.</span><span class="sxs-lookup"><span data-stu-id="dbb41-128">{userPrincipalName}: The User Principal Name of the current user, in the current tenant.</span></span>
* <span data-ttu-id="dbb41-129">{userObjectId} : ID d’objet Azure AD de l’utilisateur actuel dans le locataire actuel.</span><span class="sxs-lookup"><span data-stu-id="dbb41-129">{userObjectId}: The Azure AD object ID of the current user, in the current tenant.</span></span>
* <span data-ttu-id="dbb41-130">{theme} : le thème d’interface utilisateur actuel, tel `default`, `dark`ou `contrast`.</span><span class="sxs-lookup"><span data-stu-id="dbb41-130">{theme}: The current UI theme such as `default`, `dark`, or `contrast`.</span></span>
* <span data-ttu-id="dbb41-131">{groupId} : ID du groupe Office 365 dans lequel se trouve l’onglet.</span><span class="sxs-lookup"><span data-stu-id="dbb41-131">{groupId}: The ID of the Office 365 Group in which the tab resides.</span></span>
* <span data-ttu-id="dbb41-132">{tid}: ID de client Azure AD de l’utilisateur actuel.</span><span class="sxs-lookup"><span data-stu-id="dbb41-132">{tid}: The Azure AD tenant ID of the current user.</span></span>
* <span data-ttu-id="dbb41-133">{local}: Le lieu actuel de l’utilisateur formaté comme languageId-countryId.</span><span class="sxs-lookup"><span data-stu-id="dbb41-133">{locale}: The current locale of the user formatted as languageId-countryId.</span></span> <span data-ttu-id="dbb41-134">Par exemple, en-us.</span><span class="sxs-lookup"><span data-stu-id="dbb41-134">For example, en-us.</span></span>

>[!NOTE]
><span data-ttu-id="dbb41-135">L’espace réservé `{upn}`précédent est désormais supprimé.</span><span class="sxs-lookup"><span data-stu-id="dbb41-135">The previous `{upn}` placeholder is now deprecated.</span></span> <span data-ttu-id="dbb41-136">Pour des raisons de compatibilité ascendante, il s'agit actuellement d'un synonyme de `{loginHint}`.</span><span class="sxs-lookup"><span data-stu-id="dbb41-136">For backward compatibility, it is currently a synonym for `{loginHint}`.</span></span>

<span data-ttu-id="dbb41-137">Par exemple, supposons que dans votre manifeste d’onglets vous `configURL` définissez `"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"` l’attribut à , l’utilisateur connecté a les attributs suivants:</span><span class="sxs-lookup"><span data-stu-id="dbb41-137">For example, suppose in your tab manifest you set the `configURL` attribute to `"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"`, the signed-in user has the following attributes:</span></span>

* <span data-ttu-id="dbb41-138">Leur nom d’utilisateur est « user@example.com ».</span><span class="sxs-lookup"><span data-stu-id="dbb41-138">Their username is 'user@example.com'.</span></span>
* <span data-ttu-id="dbb41-139">Leur identifiant de locataire d’entreprise est 'e2653c-etc'.</span><span class="sxs-lookup"><span data-stu-id="dbb41-139">Their company tenant ID is 'e2653c-etc'.</span></span>
* <span data-ttu-id="dbb41-140">Ils sont membres du groupe Office 365 avec id '00209384-etc'.</span><span class="sxs-lookup"><span data-stu-id="dbb41-140">They are a member of the Office 365 group with id '00209384-etc'.</span></span>
* <span data-ttu-id="dbb41-141">L’utilisateur a défini Teams thème de la zone de travail à « sombre ».</span><span class="sxs-lookup"><span data-stu-id="dbb41-141">The user has set their Teams theme to 'dark'.</span></span>

<span data-ttu-id="dbb41-142">Lorsqu’ils configurent votre onglet, Teams appelle l’URL suivante :</span><span class="sxs-lookup"><span data-stu-id="dbb41-142">When they configure your tab, Teams calls the following URL:</span></span>

`https://www.contoso.com/config?name=user@example.com&tenant=e2653c-etc&group=00209384-etc&theme=dark`

### <a name="getting-context-by-using-the-microsoft-teams-javascript-library"></a><span data-ttu-id="dbb41-143">Obtenir du contexte à l’aide de la bibliothèque JavaScript de Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="dbb41-143">Getting context by using the Microsoft Teams JavaScript library</span></span>

<span data-ttu-id="dbb41-144">Vous pouvez également extraire les informations mentionnées ci-dessus à l’aide du client [Microsoft Teams JavaScript Client SDK](/javascript/api/overview/msteams-client) en appelant `microsoftTeams.getContext(function(context) { /* ... */ })`.</span><span class="sxs-lookup"><span data-stu-id="dbb41-144">You can also retrieve the information listed above using the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client) by calling `microsoftTeams.getContext(function(context) { /* ... */ })`.</span></span>

<span data-ttu-id="dbb41-145">La variable contextative ressemble à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="dbb41-145">The context variable looks like the following example:</span></span>

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

## <a name="retrieving-context-in-private-channels"></a><span data-ttu-id="dbb41-146">Récupération de contexte dans les canaux privés</span><span class="sxs-lookup"><span data-stu-id="dbb41-146">Retrieving context in private channels</span></span>

> [!Note]
> <span data-ttu-id="dbb41-147">Les canaux privés sont actuellement en prévisualisation du développeur privé.</span><span class="sxs-lookup"><span data-stu-id="dbb41-147">Private channels are currently in private developer preview.</span></span>

<span data-ttu-id="dbb41-148">Lorsque votre page de contenu est chargée dans un canal privé, les données que vous recevez de l’appel `getContext` sont masquées pour protéger la confidentialité du canal.</span><span class="sxs-lookup"><span data-stu-id="dbb41-148">When your content page is loaded in a private channel, the data you receive from the `getContext` call will be obfuscated to protect the privacy of the channel.</span></span> <span data-ttu-id="dbb41-149">Les champs suivants sont modifiés lorsque votre page de contenu se trouve dans un canal privé.</span><span class="sxs-lookup"><span data-stu-id="dbb41-149">The following fields are changed when your content page is in a private channel.</span></span> <span data-ttu-id="dbb41-150">Si votre page utilise l’une des valeurs ci-dessous, vous devez vérifier le champ `channelType` pour déterminer si votre page est chargée dans un canal privé et y répondre de façon appropriée.</span><span class="sxs-lookup"><span data-stu-id="dbb41-150">If your page makes use of any of the values below, you'll need to check the `channelType` field to determine if your page is loaded in a private channel, and respond appropriately.</span></span>

* <span data-ttu-id="dbb41-151">`groupId`: Non défini pour les chaînes privées</span><span class="sxs-lookup"><span data-stu-id="dbb41-151">`groupId`: Undefined for private channels</span></span>
* <span data-ttu-id="dbb41-152">`teamId`: Mis au filId de la chaîne privée</span><span class="sxs-lookup"><span data-stu-id="dbb41-152">`teamId`: Set to the threadId of the private channel</span></span>
* <span data-ttu-id="dbb41-153">`teamName`: Défini au nom de la chaîne privée</span><span class="sxs-lookup"><span data-stu-id="dbb41-153">`teamName`: Set to the name of the private channel</span></span>
* <span data-ttu-id="dbb41-154">`teamSiteUrl`: Défini sur l’URL d’un site SharePoint distinct et unique pour la chaîne privée</span><span class="sxs-lookup"><span data-stu-id="dbb41-154">`teamSiteUrl`: Set to the URL of a distinct, unique SharePoint site for the private channel</span></span>
* <span data-ttu-id="dbb41-155">`teamSitePath`: Mis sur le chemin d’un site de SharePoint distinct et unique pour la chaîne privée</span><span class="sxs-lookup"><span data-stu-id="dbb41-155">`teamSitePath`: Set to the path of a distinct, unique SharePoint site for the private channel</span></span>
* <span data-ttu-id="dbb41-156">`teamSiteDomain`: Défini au domaine d’un domaine de site distinct SharePoint unique pour le canal privé</span><span class="sxs-lookup"><span data-stu-id="dbb41-156">`teamSiteDomain`: Set to the domain of a distinct, unique SharePoint site domain for the private channel</span></span>

> [!Note]
>  <span data-ttu-id="dbb41-157">teamSiteUrl fonctionne également bien pour les canaux standard.</span><span class="sxs-lookup"><span data-stu-id="dbb41-157">teamSiteUrl works well for standard channels also.</span></span>

## <a name="theme-change-handling"></a><span data-ttu-id="dbb41-158">Gestion des changements de thème</span><span class="sxs-lookup"><span data-stu-id="dbb41-158">Theme change handling</span></span>

<span data-ttu-id="dbb41-159">Vous pouvez enregistrer votre application pour vous faire savoir si le thème change en appelant `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })`.</span><span class="sxs-lookup"><span data-stu-id="dbb41-159">You can register your app to be told if the theme changes by calling `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })`.</span></span>

<span data-ttu-id="dbb41-160">L’`theme`argument de la fonction est une chaîne qui a une valeur `default`, `dark`ou `contrast`.</span><span class="sxs-lookup"><span data-stu-id="dbb41-160">The `theme` argument in the function will be a string with a value of `default`, `dark`, or `contrast`.</span></span>
