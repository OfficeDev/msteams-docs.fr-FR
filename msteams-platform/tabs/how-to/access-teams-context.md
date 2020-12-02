---
title: Obtenir le contexte de votre onglet
description: Indique comment obtenir le contexte utilisateur dans vos onglets
keywords: contexte utilisateur des onglets teams
ms.openlocfilehash: 5c52e6eea21f0c059f3cd650770e1076f903fb8e
ms.sourcegitcommit: bfdcd122b6b4ffc52d92320d4741f870c07f0542
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/02/2020
ms.locfileid: "49552436"
---
# <a name="get-context-for-your-microsoft-teams-tab"></a><span data-ttu-id="4bb6c-104">Obtenir le contexte de votre onglet Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="4bb6c-104">Get context for your Microsoft Teams tab</span></span>

<span data-ttu-id="4bb6c-105">Votre onglet peut nécessiter des informations contextuelles pour afficher le contenu pertinent.</span><span class="sxs-lookup"><span data-stu-id="4bb6c-105">Your tab might require contextual information to display relevant content.</span></span>

* <span data-ttu-id="4bb6c-106">L’onglet peut nécessiter des informations de base sur l’utilisateur, l’équipe ou la société.</span><span class="sxs-lookup"><span data-stu-id="4bb6c-106">Your tab might need basic information about the user, team, or company.</span></span>
* <span data-ttu-id="4bb6c-107">L’onglet peut nécessiter des paramètres régionaux et des informations sur les thèmes.</span><span class="sxs-lookup"><span data-stu-id="4bb6c-107">Your tab might need locale and theme information.</span></span>
* <span data-ttu-id="4bb6c-108">Il se peut que votre onglet doive lire le `entityId` ou `subEntityId` identifie le contenu de cet onglet.</span><span class="sxs-lookup"><span data-stu-id="4bb6c-108">Your tab might need to read the `entityId` or `subEntityId` that identifies what is in this tab.</span></span>

## <a name="user-context"></a><span data-ttu-id="4bb6c-109">Contexte utilisateur</span><span class="sxs-lookup"><span data-stu-id="4bb6c-109">User context</span></span>

<span data-ttu-id="4bb6c-110">Le contexte de l’utilisateur, de l’équipe ou de la société peut être particulièrement utile lorsque</span><span class="sxs-lookup"><span data-stu-id="4bb6c-110">Context about the user, team or company can be especially useful when</span></span>

* <span data-ttu-id="4bb6c-111">Vous devez créer ou associer des ressources dans votre application à l’utilisateur ou à l’équipe spécifié.</span><span class="sxs-lookup"><span data-stu-id="4bb6c-111">You need to create or associate resources in your app with the specified user or team.</span></span>
* <span data-ttu-id="4bb6c-112">Vous souhaitez lancer un flux d’authentification auprès d’Azure Active Directory ou d’un autre fournisseur d’identité, et vous ne voulez pas demander à l’utilisateur de saisir de nouveau son nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4bb6c-112">You want to initiate an authentication flow against Azure Active Directory or other identity provider, and you don't want to require the user to enter their username again.</span></span> <span data-ttu-id="4bb6c-113">(Pour plus d’informations sur l’authentification au sein de votre onglet Microsoft Teams, consultez la rubrique [authentifier un utilisateur sous votre onglet Microsoft teams](~/concepts/authentication/authentication.md).)</span><span class="sxs-lookup"><span data-stu-id="4bb6c-113">(For more information on authenticating within your Microsoft Teams tab, see [Authenticate a user in your Microsoft Teams tab](~/concepts/authentication/authentication.md).)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4bb6c-114">Bien que ces informations utilisateur permettent d’assurer une expérience utilisateur sans complication, vous ne devez *pas* l’utiliser comme preuve d’identité.</span><span class="sxs-lookup"><span data-stu-id="4bb6c-114">Although this user information can help provide a smooth user experience, you should *not* use it as proof of identity.</span></span> <span data-ttu-id="4bb6c-115">Par exemple, un agresseur pourrait charger votre page dans un « navigateur incorrect » et afficher des informations ou des demandes nuisibles.</span><span class="sxs-lookup"><span data-stu-id="4bb6c-115">For example, an attacker could load your page in a "bad browser" and render harmful information or requests.</span></span>

## <a name="accessing-context"></a><span data-ttu-id="4bb6c-116">Contexte d’accès</span><span class="sxs-lookup"><span data-stu-id="4bb6c-116">Accessing context</span></span>

<span data-ttu-id="4bb6c-117">Vous pouvez accéder aux informations de contexte de deux manières :</span><span class="sxs-lookup"><span data-stu-id="4bb6c-117">You can access context information in two ways:</span></span>

* <span data-ttu-id="4bb6c-118">Insérer des valeurs d’espace réservé d’URL</span><span class="sxs-lookup"><span data-stu-id="4bb6c-118">Insert URL placeholder values</span></span>
* <span data-ttu-id="4bb6c-119">Utiliser le [Kit de développement logiciel (SDK) JavaScript client Microsoft teams](/javascript/api/overview/msteams-client)</span><span class="sxs-lookup"><span data-stu-id="4bb6c-119">Use the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client)</span></span>

### <a name="getting-context-by-inserting-url-placeholder-values"></a><span data-ttu-id="4bb6c-120">Obtenir le contexte en insérant des valeurs d’espace réservé URL</span><span class="sxs-lookup"><span data-stu-id="4bb6c-120">Getting context by inserting URL placeholder values</span></span>

<span data-ttu-id="4bb6c-121">Utilisez des espaces réservés dans vos URL de configuration ou de contenu.</span><span class="sxs-lookup"><span data-stu-id="4bb6c-121">Use placeholders in your configuration or content URLs.</span></span> <span data-ttu-id="4bb6c-122">Microsoft teams remplace les espaces réservés par les valeurs appropriées lors de la détermination de l’URL de contenu ou de configuration réelle.</span><span class="sxs-lookup"><span data-stu-id="4bb6c-122">Microsoft Teams replaces the placeholders with the relevant values when determining the actual configuration or content URL.</span></span> <span data-ttu-id="4bb6c-123">Les espaces réservés disponibles incluent tous les champs de l’objet de [contexte](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) .</span><span class="sxs-lookup"><span data-stu-id="4bb6c-123">The available placeholders include all fields on the [Context](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) object.</span></span> <span data-ttu-id="4bb6c-124">Les espaces réservés courants sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="4bb6c-124">Common placeholders include the following:</span></span>

* <span data-ttu-id="4bb6c-125">{entityId} : ID que vous avez fourni pour l’élément dans cet onglet lors de la première [configuration de l’onglet](~/tabs/how-to/create-tab-pages/configuration-page.md).</span><span class="sxs-lookup"><span data-stu-id="4bb6c-125">{entityId}: The ID you supplied for the item in this tab when first [configuring the tab](~/tabs/how-to/create-tab-pages/configuration-page.md).</span></span>
* <span data-ttu-id="4bb6c-126">{subEntityId} : ID que vous avez fourni lors de la génération d’un [lien profond](~/concepts/build-and-test/deep-links.md) pour un élément spécifique _dans_ cet onglet. Il doit être utilisé pour restaurer un état spécifique au sein d’une entité ; par exemple, faire défiler ou activer une partie de contenu spécifique.</span><span class="sxs-lookup"><span data-stu-id="4bb6c-126">{subEntityId}: The ID you supplied when generating a [deep link](~/concepts/build-and-test/deep-links.md) for a specific item _within_ this tab. This should be used to restore to a specific state within an entity; for example, scrolling to or activating a specific piece of content.</span></span>
* <span data-ttu-id="4bb6c-127">{loginHint} : valeur appropriée en tant qu’indication de connexion pour Azure AD. Il s’agit généralement du nom de connexion de l’utilisateur actuel, dans son client d’origine.</span><span class="sxs-lookup"><span data-stu-id="4bb6c-127">{loginHint}: A value suitable as a login hint for Azure AD.This is usually the login name of the current user, in their home tenant.</span></span>
* <span data-ttu-id="4bb6c-128">{userPrincipalName} : nom d’utilisateur principal de l’utilisateur actuel, dans le client actuel.</span><span class="sxs-lookup"><span data-stu-id="4bb6c-128">{userPrincipalName}: The User Principal Name of the current user, in the current tenant.</span></span>
* <span data-ttu-id="4bb6c-129">{userObjectId} : ID d’objet Azure AD de l’utilisateur actuel, dans le client actuel.</span><span class="sxs-lookup"><span data-stu-id="4bb6c-129">{userObjectId}: The Azure AD object ID of the current user, in the current tenant.</span></span>
* <span data-ttu-id="4bb6c-130">{Theme} : le thème de l’interface utilisateur actuel, `default` `dark` , ou `contrast` .</span><span class="sxs-lookup"><span data-stu-id="4bb6c-130">{theme}: The current UI theme such as `default`, `dark`, or `contrast`.</span></span>
* <span data-ttu-id="4bb6c-131">{groupId} : ID du groupe Office 365 dans lequel réside l’onglet.</span><span class="sxs-lookup"><span data-stu-id="4bb6c-131">{groupId}: The ID of the Office 365 Group in which the tab resides.</span></span>
* <span data-ttu-id="4bb6c-132">{TID} : ID de client Azure AD de l’utilisateur actuel.</span><span class="sxs-lookup"><span data-stu-id="4bb6c-132">{tid}: The Azure AD tenant ID of the current user.</span></span>
* <span data-ttu-id="4bb6c-133">{locale} : paramètres régionaux actuels de l’utilisateur mis en forme en tant que languageId-countryId (par exemple, en-US).</span><span class="sxs-lookup"><span data-stu-id="4bb6c-133">{locale}: The current locale of the user formatted as languageId-countryId (for example, en-us).</span></span>

>[!NOTE]
><span data-ttu-id="4bb6c-134">L' `{upn}` espace réservé précédent est maintenant obsolète.</span><span class="sxs-lookup"><span data-stu-id="4bb6c-134">The previous `{upn}` placeholder is now deprecated.</span></span> <span data-ttu-id="4bb6c-135">Pour des raisons de compatibilité descendante, il s’agit actuellement d’un synonyme de `{loginHint}` .</span><span class="sxs-lookup"><span data-stu-id="4bb6c-135">For backward compatibility, it is currently a synonym for `{loginHint}`.</span></span>

<span data-ttu-id="4bb6c-136">Par exemple, supposons dans votre manifeste d’onglets que vous avez défini l' `configURL` attribut sur</span><span class="sxs-lookup"><span data-stu-id="4bb6c-136">For example, suppose in your tab manifest you set the `configURL` attribute to</span></span>

`"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"`

<span data-ttu-id="4bb6c-137">Et l’utilisateur connecté possède les attributs suivants :</span><span class="sxs-lookup"><span data-stu-id="4bb6c-137">And the signed-in user has the following attributes:</span></span>

* <span data-ttu-id="4bb6c-138">Le nom d’utilisateur est « user@example.com ».</span><span class="sxs-lookup"><span data-stu-id="4bb6c-138">Their username is 'user@example.com'</span></span>
* <span data-ttu-id="4bb6c-139">L’ID de client de son entreprise est « e2653c-etc »</span><span class="sxs-lookup"><span data-stu-id="4bb6c-139">Their company tenant ID is 'e2653c-etc'</span></span>
* <span data-ttu-id="4bb6c-140">Il s’agit d’un membre du groupe Office 365 avec l’ID « 00209384-etc. »</span><span class="sxs-lookup"><span data-stu-id="4bb6c-140">They are a member of the Office 365 group with id '00209384-etc'</span></span>
* <span data-ttu-id="4bb6c-141">L’utilisateur a défini son thème teams sur « Dark »</span><span class="sxs-lookup"><span data-stu-id="4bb6c-141">The user has set their Teams theme to 'dark'</span></span>

<span data-ttu-id="4bb6c-142">Lorsqu’ils configurent votre onglet, teams appelle cette URL :</span><span class="sxs-lookup"><span data-stu-id="4bb6c-142">When they configure your tab, Teams calls this URL:</span></span>

`https://www.contoso.com/config?name=user@example.com&tenant=e2653c-etc&group=00209384-etc&theme=dark`

### <a name="getting-context-by-using-the-microsoft-teams-javascript-library"></a><span data-ttu-id="4bb6c-143">Obtention de contexte à l’aide de la bibliothèque JavaScript Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="4bb6c-143">Getting context by using the Microsoft Teams JavaScript library</span></span>

<span data-ttu-id="4bb6c-144">Vous pouvez également récupérer les informations ci-dessus à l’aide du [Kit de développement logiciel (SDK) JavaScript client Microsoft teams](/javascript/api/overview/msteams-client) en appelant `microsoftTeams.getContext(function(context) { /* ... */ })` .</span><span class="sxs-lookup"><span data-stu-id="4bb6c-144">You can also retrieve the information listed above using the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client) by calling `microsoftTeams.getContext(function(context) { /* ... */ })`.</span></span>

<span data-ttu-id="4bb6c-145">La variable de contexte se présente comme dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="4bb6c-145">The context variable will look like the following example.</span></span>

```json
{
    "teamId": "The Microsoft Teams ID in the format 19:[id]@thread.skype",
    "teamName": "The name of the current team",
    "channelId": "The channel ID in the format 19:[id]@thread.skype",
    "channelName": "The name of the current channel",
    "chatId": "The chat ID in the in the format 19:[id]@thread.skype",
    "locale": "The current locale of the user formatted as languageId-countryId (for example, en-us)",
    "entityId": "The developer-defined unique ID for the entity this content points to",
    "subEntityId": "The developer-defined unique ID for the sub-entity this content points to",
    "loginHint": "A value suitable as a login hint for Azure AD. This is usually the login name of the current user, in their home tenant",
    "userPrincipalName": "The User Principal Name of the current user, in the current tenant",
    "userObjectId": "The Azure AD object id of the current user, in the current tenant",
    "tid": "The Azure AD tenant ID of the current user",
    "groupId": "Guid identifying the current O365 Group ID",
    "theme": "The current UI theme: default | dark | contrast",
    "isFullScreen": "Indicates whether the tab is in full-screen mode",
    "userLicenseType": "Indicates the user licence type in the given SKU (for example, student or teacher)",
    "tenantSKU": "Indicates the SKU category of the tenant (for example, EDU)",
    "channelType": "microsoftTeams.ChannelType.Private | microsoftTeams.ChannelType.Regular"
}
```

## <a name="retrieving-context-in-private-channels"></a><span data-ttu-id="4bb6c-146">Récupération du contexte dans les canaux privés</span><span class="sxs-lookup"><span data-stu-id="4bb6c-146">Retrieving context in private channels</span></span>

> [!Note]
> <span data-ttu-id="4bb6c-147">Les canaux privés sont actuellement en version préliminaire pour les développeurs privés.</span><span class="sxs-lookup"><span data-stu-id="4bb6c-147">Private channels are currently in private developer preview.</span></span>

<span data-ttu-id="4bb6c-148">Lorsque votre page de contenu est chargée dans un canal privé, les données que vous recevez de l' `getContext` appel seront obscurcies pour protéger la confidentialité du canal.</span><span class="sxs-lookup"><span data-stu-id="4bb6c-148">When your content page is loaded in a private channel, the data you receive from the `getContext` call will be obfuscated to protect the privacy of the channel.</span></span> <span data-ttu-id="4bb6c-149">Les champs suivants sont modifiés lorsque votre page de contenu se trouve dans un canal privé.</span><span class="sxs-lookup"><span data-stu-id="4bb6c-149">The following fields are changed when your content page is in a private channel.</span></span> <span data-ttu-id="4bb6c-150">Si votre page utilise l’une des valeurs ci-dessous, vous devez vérifier le `channelType` champ afin de déterminer si votre page est chargée dans un canal privé et de répondre de manière appropriée.</span><span class="sxs-lookup"><span data-stu-id="4bb6c-150">If your page makes use of any of the values below, you'll need to check the `channelType` field to determine if your page is loaded in a private channel, and respond appropriately.</span></span>

* <span data-ttu-id="4bb6c-151">`groupId` -Non défini pour les canaux privés</span><span class="sxs-lookup"><span data-stu-id="4bb6c-151">`groupId` - Undefined for private channels</span></span>
* <span data-ttu-id="4bb6c-152">`teamId` -Défini sur le threadId du canal privé</span><span class="sxs-lookup"><span data-stu-id="4bb6c-152">`teamId` - Set to the threadId of the private channel</span></span>
* <span data-ttu-id="4bb6c-153">`teamName` -Défini sur le nom du canal privé</span><span class="sxs-lookup"><span data-stu-id="4bb6c-153">`teamName` - Set to the name of the private channel</span></span>
* <span data-ttu-id="4bb6c-154">`teamSiteUrl` -Défini sur l’URL d’un site SharePoint distinct unique pour le canal privé</span><span class="sxs-lookup"><span data-stu-id="4bb6c-154">`teamSiteUrl` - Set to the URL of a distinct, unique SharePoint site for the private channel</span></span>
* <span data-ttu-id="4bb6c-155">`teamSitePath` -Défini sur le chemin d’accès à un site SharePoint distinct unique pour le canal privé</span><span class="sxs-lookup"><span data-stu-id="4bb6c-155">`teamSitePath` - Set to the path of a distinct, unique SharePoint site for the private channel</span></span>
* <span data-ttu-id="4bb6c-156">`teamSiteDomain` -Défini sur le domaine d’un domaine de site SharePoint distinct unique pour le canal privé</span><span class="sxs-lookup"><span data-stu-id="4bb6c-156">`teamSiteDomain` - Set to the domain of a distinct, unique SharePoint site domain for the private channel</span></span>

> [!Note]
>  <span data-ttu-id="4bb6c-157">teamSiteUrl fonctionne également pour les canaux standard.</span><span class="sxs-lookup"><span data-stu-id="4bb6c-157">teamSiteUrl works well for standard channels also.</span></span>

## <a name="theme-change-handling"></a><span data-ttu-id="4bb6c-158">Gestion des modifications de thème</span><span class="sxs-lookup"><span data-stu-id="4bb6c-158">Theme change handling</span></span>

<span data-ttu-id="4bb6c-159">Vous pouvez inscrire votre application pour être informée si le thème change en appelant `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })` .</span><span class="sxs-lookup"><span data-stu-id="4bb6c-159">You can register your app to be told if the theme changes by calling `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })`.</span></span>

<span data-ttu-id="4bb6c-160">L' `theme` argument de la fonction sera une chaîne avec la valeur `default` , `dark` ou `contrast` .</span><span class="sxs-lookup"><span data-stu-id="4bb6c-160">The `theme` argument in the function will be a string with a value of `default`, `dark`, or `contrast`.</span></span>
