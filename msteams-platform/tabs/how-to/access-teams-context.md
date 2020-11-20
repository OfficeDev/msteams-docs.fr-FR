---
title: Obtenir le contexte de votre onglet
description: Indique comment obtenir le contexte utilisateur dans vos onglets
keywords: contexte utilisateur des onglets teams
ms.openlocfilehash: 8c94c4fd895896186ddda20bfaafd1d6ccdc1e73
ms.sourcegitcommit: 64acd30eee8af5fe151e9866c13226ed3f337c72
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/18/2020
ms.locfileid: "49346797"
---
# <a name="get-context-for-your-microsoft-teams-tab"></a><span data-ttu-id="42260-104">Obtenir le contexte de votre onglet Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="42260-104">Get context for your Microsoft Teams tab</span></span>

<span data-ttu-id="42260-105">Votre onglet peut nécessiter des informations contextuelles pour afficher le contenu pertinent.</span><span class="sxs-lookup"><span data-stu-id="42260-105">Your tab might require contextual information to display relevant content.</span></span>

* <span data-ttu-id="42260-106">L’onglet peut nécessiter des informations de base sur l’utilisateur, l’équipe ou la société.</span><span class="sxs-lookup"><span data-stu-id="42260-106">Your tab might need basic information about the user, team, or company.</span></span>
* <span data-ttu-id="42260-107">L’onglet peut nécessiter des paramètres régionaux et des informations sur les thèmes.</span><span class="sxs-lookup"><span data-stu-id="42260-107">Your tab might need locale and theme information.</span></span>
* <span data-ttu-id="42260-108">Il se peut que votre onglet doive lire le `entityId` ou `subEntityId` identifie le contenu de cet onglet.</span><span class="sxs-lookup"><span data-stu-id="42260-108">Your tab might need to read the `entityId` or `subEntityId` that identifies what is in this tab.</span></span>

## <a name="user-context"></a><span data-ttu-id="42260-109">Contexte utilisateur</span><span class="sxs-lookup"><span data-stu-id="42260-109">User context</span></span>

<span data-ttu-id="42260-110">Le contexte de l’utilisateur, de l’équipe ou de la société peut être particulièrement utile lorsque</span><span class="sxs-lookup"><span data-stu-id="42260-110">Context about the user, team or company can be especially useful when</span></span>

* <span data-ttu-id="42260-111">Vous devez créer ou associer des ressources dans votre application à l’utilisateur ou à l’équipe spécifié.</span><span class="sxs-lookup"><span data-stu-id="42260-111">You need to create or associate resources in your app with the specified user or team.</span></span>
* <span data-ttu-id="42260-112">Vous souhaitez lancer un flux d’authentification auprès d’Azure Active Directory ou d’un autre fournisseur d’identité, et vous ne voulez pas demander à l’utilisateur de saisir de nouveau son nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="42260-112">You want to initiate an authentication flow against Azure Active Directory or other identity provider, and you don't want to require the user to enter their username again.</span></span> <span data-ttu-id="42260-113">(Pour plus d’informations sur l’authentification au sein de votre onglet Microsoft Teams, consultez la rubrique [authentifier un utilisateur sous votre onglet Microsoft teams](~/concepts/authentication/authentication.md).)</span><span class="sxs-lookup"><span data-stu-id="42260-113">(For more information on authenticating within your Microsoft Teams tab, see [Authenticate a user in your Microsoft Teams tab](~/concepts/authentication/authentication.md).)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="42260-114">Bien que ces informations utilisateur permettent d’assurer une expérience utilisateur sans complication, vous ne devez *pas* l’utiliser comme preuve d’identité.</span><span class="sxs-lookup"><span data-stu-id="42260-114">Although this user information can help provide a smooth user experience, you should *not* use it as proof of identity.</span></span> <span data-ttu-id="42260-115">Par exemple, un agresseur peut charger votre page dans un « navigateur incorrect » et lui fournir toutes les informations souhaitées.</span><span class="sxs-lookup"><span data-stu-id="42260-115">For example, an attacker could you load your page in a "bad browser" and provide it with any information they want.</span></span>

## <a name="accessing-context"></a><span data-ttu-id="42260-116">Contexte d’accès</span><span class="sxs-lookup"><span data-stu-id="42260-116">Accessing context</span></span>

<span data-ttu-id="42260-117">Vous pouvez accéder aux informations de contexte de deux manières :</span><span class="sxs-lookup"><span data-stu-id="42260-117">You can access context information in two ways:</span></span>

* <span data-ttu-id="42260-118">Insérer des valeurs d’espace réservé d’URL</span><span class="sxs-lookup"><span data-stu-id="42260-118">Insert URL placeholder values</span></span>
* <span data-ttu-id="42260-119">Utiliser le [Kit de développement logiciel (SDK) JavaScript client Microsoft teams](/javascript/api/overview/msteams-client)</span><span class="sxs-lookup"><span data-stu-id="42260-119">Use the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client)</span></span>

### <a name="getting-context-by-inserting-url-placeholder-values"></a><span data-ttu-id="42260-120">Obtenir le contexte en insérant des valeurs d’espace réservé URL</span><span class="sxs-lookup"><span data-stu-id="42260-120">Getting context by inserting URL placeholder values</span></span>

<span data-ttu-id="42260-121">Utilisez des espaces réservés dans vos URL de configuration ou de contenu.</span><span class="sxs-lookup"><span data-stu-id="42260-121">Use placeholders in your configuration or content URLs.</span></span> <span data-ttu-id="42260-122">Microsoft teams remplace les espaces réservés par les valeurs appropriées lors de la détermination de l’URL de contenu ou de configuration réelle à atteindre.</span><span class="sxs-lookup"><span data-stu-id="42260-122">Microsoft Teams replaces the placeholders with the relevant values when determining the actual configuration or content URL to navigate to.</span></span> <span data-ttu-id="42260-123">Les espaces réservés disponibles incluent tous les champs de l’objet de [contexte](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest) .</span><span class="sxs-lookup"><span data-stu-id="42260-123">The available placeholders include all fields on the [Context](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest) object.</span></span> <span data-ttu-id="42260-124">Les espaces réservés courants sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="42260-124">Common placeholders include the following:</span></span>

* <span data-ttu-id="42260-125">{entityId} : ID que vous avez fourni pour l’élément dans cet onglet lors de la première [configuration de l’onglet](~/tabs/how-to/create-tab-pages/configuration-page.md).</span><span class="sxs-lookup"><span data-stu-id="42260-125">{entityId}: The ID you supplied for the item in this tab when first [configuring the tab](~/tabs/how-to/create-tab-pages/configuration-page.md).</span></span>
* <span data-ttu-id="42260-126">{subEntityId} : ID que vous avez fourni lors de la génération d’un [lien profond](~/concepts/build-and-test/deep-links.md) pour un élément spécifique _dans_ cet onglet. Il doit être utilisé pour restaurer un état spécifique au sein d’une entité ; par exemple, faire défiler ou activer une partie de contenu spécifique.</span><span class="sxs-lookup"><span data-stu-id="42260-126">{subEntityId}: The ID you supplied when generating a [deep link](~/concepts/build-and-test/deep-links.md) for a specific item _within_ this tab. This should be used to restore to a specific state within an entity; for example, scrolling to or activating a specific piece of content.</span></span>
* <span data-ttu-id="42260-127">{loginHint} : valeur appropriée en tant qu’indication de connexion pour Azure AD. Il s’agit généralement du nom de connexion de l’utilisateur actuel, dans son client d’origine.</span><span class="sxs-lookup"><span data-stu-id="42260-127">{loginHint}: A value suitable as a login hint for Azure AD.This is usually the login name of the current user, in their home tenant.</span></span>
* <span data-ttu-id="42260-128">{userPrincipalName} : nom d’utilisateur principal de l’utilisateur actuel, dans le client actuel.</span><span class="sxs-lookup"><span data-stu-id="42260-128">{userPrincipalName}: The User Principal Name of the current user, in the current tenant.</span></span>
* <span data-ttu-id="42260-129">{userObjectId} : ID d’objet Azure AD de l’utilisateur actuel, dans le client actuel.</span><span class="sxs-lookup"><span data-stu-id="42260-129">{userObjectId}: The Azure AD object ID of the current user, in the current tenant.</span></span>
* <span data-ttu-id="42260-130">{Theme} : le thème de l’interface utilisateur actuel, `default` `dark` , ou `contrast` .</span><span class="sxs-lookup"><span data-stu-id="42260-130">{theme}: The current UI theme such as `default`, `dark`, or `contrast`.</span></span>
* <span data-ttu-id="42260-131">{groupId} : ID du groupe Office 365 dans lequel réside l’onglet.</span><span class="sxs-lookup"><span data-stu-id="42260-131">{groupId}: The ID of the Office 365 Group in which the tab resides.</span></span>
* <span data-ttu-id="42260-132">{TID} : ID de client Azure AD de l’utilisateur actuel.</span><span class="sxs-lookup"><span data-stu-id="42260-132">{tid}: The Azure AD tenant ID of the current user.</span></span>
* <span data-ttu-id="42260-133">{locale} : paramètres régionaux actuels de l’utilisateur mis en forme en tant que languageId-countryId (par exemple, en-US).</span><span class="sxs-lookup"><span data-stu-id="42260-133">{locale}: The current locale of the user formatted as languageId-countryId (for example, en-us).</span></span>
* <span data-ttu-id="42260-134">{osLocaleInfo} : informations plus détaillées sur les paramètres régionaux du système d’exploitation de l’utilisateur, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="42260-134">{osLocaleInfo}: More detailed locale info from the user's OS if available.</span></span> <span data-ttu-id="42260-135">Peut être utilisé conjointement avec :</span><span class="sxs-lookup"><span data-stu-id="42260-135">Can be used together with:</span></span>
    * <span data-ttu-id="42260-136">le @microsoft/Globe NPM package pour vérifier que votre application respecte la date de système d’exploitation de l’utilisateur et</span><span class="sxs-lookup"><span data-stu-id="42260-136">the @microsoft/globe NPM package to ensure your app respects the user's OS date and</span></span>
    * <span data-ttu-id="42260-137">configuration du format de l’heure.</span><span class="sxs-lookup"><span data-stu-id="42260-137">time format configuration.</span></span>
* <span data-ttu-id="42260-138">{sessionId} : ID unique de la session teams actuelle à utiliser pour corréler les données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="42260-138">{sessionId}: Unique ID for the current Teams session for use in correlating telemetry data.</span></span>
* <span data-ttu-id="42260-139">{channelId} : ID Microsoft teams pour le canal auquel le contenu est associé.</span><span class="sxs-lookup"><span data-stu-id="42260-139">{channelId}: The Microsoft Teams ID for the channel with which the content is associated.</span></span>
* <span data-ttu-id="42260-140">{channelName} : nom du canal auquel le contenu est associé.</span><span class="sxs-lookup"><span data-stu-id="42260-140">{channelName}: The name for the channel with which the content is associated.</span></span>
* <span data-ttu-id="42260-141">{chatId} : ID Microsoft teams de la conversation à laquelle le contenu est associé.</span><span class="sxs-lookup"><span data-stu-id="42260-141">{chatId}: The Microsoft Teams ID for the chat with which the content is associated.</span></span>
* <span data-ttu-id="42260-142">{URL} : URL de contenu de cet onglet.</span><span class="sxs-lookup"><span data-stu-id="42260-142">{url}: Content URL of this tab.</span></span>
* <span data-ttu-id="42260-143">{websiteUrl} : URL du site Web de cet onglet.</span><span class="sxs-lookup"><span data-stu-id="42260-143">{websiteUrl}: Website URL of this tab.</span></span>
* <span data-ttu-id="42260-144">{favoriteChannelsOnly} : indicateur qui autorise la sélection de canaux favoris uniquement.</span><span class="sxs-lookup"><span data-stu-id="42260-144">{favoriteChannelsOnly}: Flag allowing to select favorite channels only.</span></span>
* <span data-ttu-id="42260-145">{favoriteTeamsOnly} : indicateur autorisant à sélectionner les équipes favorites uniquement.</span><span class="sxs-lookup"><span data-stu-id="42260-145">{favoriteTeamsOnly}: Flag allowing to select favorite teams only.</span></span>
* <span data-ttu-id="42260-146">{userTeamRole} : rôle de l’utilisateur actuel dans l’équipe.</span><span class="sxs-lookup"><span data-stu-id="42260-146">{userTeamRole}: Role of current user in the team.</span></span>
* <span data-ttu-id="42260-147">{teamType} : le type de l’équipe.</span><span class="sxs-lookup"><span data-stu-id="42260-147">{teamType}: The type of the team.</span></span>
* <span data-ttu-id="42260-148">{isTeamLocked} : état verrouillé de l’équipe.</span><span class="sxs-lookup"><span data-stu-id="42260-148">{isTeamLocked}: The locked status of the team.</span></span>
* <span data-ttu-id="42260-149">{isTeamArchived} : état archivé de l’équipe.</span><span class="sxs-lookup"><span data-stu-id="42260-149">{isTeamArchived}: The archived status of the team.</span></span>
* <span data-ttu-id="42260-150">{isFullScreen} : indique si l’onglet est en mode plein écran.</span><span class="sxs-lookup"><span data-stu-id="42260-150">{isFullScreen}: Indication whether the tab is in full-screen mode.</span></span>
* <span data-ttu-id="42260-151">{teamSiteUrl} : site SharePoint racine associé à l’équipe.</span><span class="sxs-lookup"><span data-stu-id="42260-151">{teamSiteUrl}: The root SharePoint site associated with the team.</span></span>
* <span data-ttu-id="42260-152">{teamSiteDomain} : domaine du site SharePoint racine associé à l’équipe.</span><span class="sxs-lookup"><span data-stu-id="42260-152">{teamSiteDomain}: The domain of the root SharePoint site associated with the team.</span></span>
* <span data-ttu-id="42260-153">{teamSitePath} : chemin d’accès relatif au site SharePoint associé à l’équipe.</span><span class="sxs-lookup"><span data-stu-id="42260-153">{teamSitePath}: The relative path to the SharePoint site associated with the team.</span></span>
* <span data-ttu-id="42260-154">{channelRelativeUrl} : chemin d’accès relatif au dossier SharePoint associé au canal.</span><span class="sxs-lookup"><span data-stu-id="42260-154">{channelRelativeUrl}: The relative path to the SharePoint folder associated with the channel.</span></span>
* <span data-ttu-id="42260-155">{tenantSKU} : le type de licence pour le client actuel des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="42260-155">{tenantSKU}: The type of license for the current users tenant.</span></span>
* <span data-ttu-id="42260-156">{ringId} : ID d’appel en cours.</span><span class="sxs-lookup"><span data-stu-id="42260-156">{ringId}: Current ring ID.</span></span>
* <span data-ttu-id="42260-157">{appSessionId} : ID unique de la session en cours à utiliser pour corréler les données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="42260-157">{appSessionId}: Unique ID for the current session for use in correlating telemetry data.</span></span>
* <span data-ttu-id="42260-158">{completionBotId} : spécifie un ID de bot pour envoyer le résultat de l’interaction de l’utilisateur avec le module de tâche.</span><span class="sxs-lookup"><span data-stu-id="42260-158">{completionBotId}: Specifies a bot ID to send the result of the user's interaction with the task module.</span></span>
* <span data-ttu-id="42260-159">{conversationId} : ID de la conversation.</span><span class="sxs-lookup"><span data-stu-id="42260-159">{conversationId}: The Id of the conversation.</span></span>
* <span data-ttu-id="42260-160">{hostClientType} : type du client hôte. (Les valeurs possibles sont les suivantes : Android, iOS, Web, Desktop et Rigel.)</span><span class="sxs-lookup"><span data-stu-id="42260-160">{hostClientType}: Type of the host client.(Possible values are: android, ios, web, desktop, and rigel.)</span></span>
* <span data-ttu-id="42260-161">{frameContext} : contexte dans lequel l’URL de l’onglet est chargée (contenu, tâche, définition, suppression, sidePanel).</span><span class="sxs-lookup"><span data-stu-id="42260-161">{frameContext}: The context where the tab url is loaded (content, task, setting, remove, sidePanel).</span></span>
* <span data-ttu-id="42260-162">{SharePoint} : cette date est disponible uniquement lorsqu’elle est hébergée dans SharePoint.</span><span class="sxs-lookup"><span data-stu-id="42260-162">{sharepoint}: This is only available when hosted in SharePoint.</span></span>
* <span data-ttu-id="42260-163">{meetingId} : elle est utilisée par Tab lors de l’exécution dans le contexte de la réunion.</span><span class="sxs-lookup"><span data-stu-id="42260-163">{meetingId}: It is used by tab when running in meeting context.</span></span>
* <span data-ttu-id="42260-164">{userLicenseType} Type de licence pour l’utilisateur actuel.</span><span class="sxs-lookup"><span data-stu-id="42260-164">{userLicenseType} The license type for the current user.</span></span>

>[!NOTE]
><span data-ttu-id="42260-165">L' `{upn}` espace réservé précédent est maintenant obsolète.</span><span class="sxs-lookup"><span data-stu-id="42260-165">The previous `{upn}` placeholder is now deprecated.</span></span> <span data-ttu-id="42260-166">Pour des raisons de compatibilité descendante, il s’agit actuellement d’un synonyme de `{loginHint}` .</span><span class="sxs-lookup"><span data-stu-id="42260-166">For backward compatibility, it is currently a synonym for `{loginHint}`.</span></span>

<span data-ttu-id="42260-167">Par exemple, supposons dans votre manifeste d’onglets que vous avez défini l' `configURL` attribut sur</span><span class="sxs-lookup"><span data-stu-id="42260-167">For example, suppose in your tab manifest you set the `configURL` attribute to</span></span>

`"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"`

<span data-ttu-id="42260-168">Et l’utilisateur connecté possède les attributs suivants :</span><span class="sxs-lookup"><span data-stu-id="42260-168">And the signed-in user has the following attributes:</span></span>

* <span data-ttu-id="42260-169">Le nom d’utilisateur est « user@example.com ».</span><span class="sxs-lookup"><span data-stu-id="42260-169">Their username is 'user@example.com'</span></span>
* <span data-ttu-id="42260-170">L’ID de client de son entreprise est « e2653c-etc »</span><span class="sxs-lookup"><span data-stu-id="42260-170">Their company tenant ID is 'e2653c-etc'</span></span>
* <span data-ttu-id="42260-171">Il s’agit d’un membre du groupe Office 365 avec l’ID « 00209384-etc. »</span><span class="sxs-lookup"><span data-stu-id="42260-171">They are a member of the Office 365 group with id '00209384-etc'</span></span>
* <span data-ttu-id="42260-172">L’utilisateur a défini son thème teams sur « Dark »</span><span class="sxs-lookup"><span data-stu-id="42260-172">The user has set their Teams theme to 'dark'</span></span>

<span data-ttu-id="42260-173">Lorsqu’ils configurent votre onglet, teams appelle cette URL :</span><span class="sxs-lookup"><span data-stu-id="42260-173">When they configure your tab, Teams calls this URL:</span></span>

`https://www.contoso.com/config?name=user@example.com&tenant=e2653c-etc&group=00209384-etc&theme=dark`

### <a name="getting-context-by-using-the-microsoft-teams-javascript-library"></a><span data-ttu-id="42260-174">Obtention de contexte à l’aide de la bibliothèque JavaScript Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="42260-174">Getting context by using the Microsoft Teams JavaScript library</span></span>

<span data-ttu-id="42260-175">Vous pouvez également récupérer les informations ci-dessus à l’aide du [Kit de développement logiciel (SDK) JavaScript client Microsoft teams](/javascript/api/overview/msteams-client) en appelant `microsoftTeams.getContext(function(context) { /* ... */ })` .</span><span class="sxs-lookup"><span data-stu-id="42260-175">You can also retrieve the information listed above using the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client) by calling `microsoftTeams.getContext(function(context) { /* ... */ })`.</span></span>

<span data-ttu-id="42260-176">La variable de contexte se présente comme dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="42260-176">The context variable will look like the following example.</span></span>

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

## <a name="retrieving-context-in-private-channels"></a><span data-ttu-id="42260-177">Récupération du contexte dans les canaux privés</span><span class="sxs-lookup"><span data-stu-id="42260-177">Retrieving context in private channels</span></span>

> [!Note]
> <span data-ttu-id="42260-178">Les canaux privés sont actuellement en version préliminaire pour les développeurs privés.</span><span class="sxs-lookup"><span data-stu-id="42260-178">Private channels are currently in private developer preview.</span></span>

<span data-ttu-id="42260-179">Lorsque votre page de contenu est chargée dans un canal privé, les données que vous recevez de l' `getContext` appel seront obscurcies pour protéger la confidentialité du canal.</span><span class="sxs-lookup"><span data-stu-id="42260-179">When your content page is loaded in a private channel, the data you receive from the `getContext` call will be obfuscated to protect the privacy of the channel.</span></span> <span data-ttu-id="42260-180">Les champs suivants sont modifiés lorsque votre page de contenu se trouve dans un canal privé.</span><span class="sxs-lookup"><span data-stu-id="42260-180">The following fields are changed when your content page is in a private channel.</span></span> <span data-ttu-id="42260-181">Si votre page utilise l’une des valeurs ci-dessous, vous devez vérifier le `channelType` champ afin de déterminer si votre page est chargée dans un canal privé et de répondre de manière appropriée.</span><span class="sxs-lookup"><span data-stu-id="42260-181">If your page makes use of any of the values below, you'll need to check the `channelType` field to determine if your page is loaded in a private channel, and respond appropriately.</span></span>

* <span data-ttu-id="42260-182">`groupId` -Non défini pour les canaux privés</span><span class="sxs-lookup"><span data-stu-id="42260-182">`groupId` - Undefined for private channels</span></span>
* <span data-ttu-id="42260-183">`teamId` -Défini sur le threadId du canal privé</span><span class="sxs-lookup"><span data-stu-id="42260-183">`teamId` - Set to the threadId of the private channel</span></span>
* <span data-ttu-id="42260-184">`teamName` -Défini sur le nom du canal privé</span><span class="sxs-lookup"><span data-stu-id="42260-184">`teamName` - Set to the name of the private channel</span></span>
* <span data-ttu-id="42260-185">`teamSiteUrl` -Défini sur l’URL d’un site SharePoint distinct unique pour le canal privé</span><span class="sxs-lookup"><span data-stu-id="42260-185">`teamSiteUrl` - Set to the URL of a distinct, unique SharePoint site for the private channel</span></span>
* <span data-ttu-id="42260-186">`teamSitePath` -Défini sur le chemin d’accès à un site SharePoint distinct unique pour le canal privé</span><span class="sxs-lookup"><span data-stu-id="42260-186">`teamSitePath` - Set to the path of a distinct, unique SharePoint site for the private channel</span></span>
* <span data-ttu-id="42260-187">`teamSiteDomain` -Défini sur le domaine d’un domaine de site SharePoint distinct unique pour le canal privé</span><span class="sxs-lookup"><span data-stu-id="42260-187">`teamSiteDomain` - Set to the domain of a distinct, unique SharePoint site domain for the private channel</span></span>

## <a name="theme-change-handling"></a><span data-ttu-id="42260-188">Gestion des modifications de thème</span><span class="sxs-lookup"><span data-stu-id="42260-188">Theme change handling</span></span>

<span data-ttu-id="42260-189">Vous pouvez inscrire votre application pour être informée si le thème change en appelant `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })` .</span><span class="sxs-lookup"><span data-stu-id="42260-189">You can register your app to be told if the theme changes by calling `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })`.</span></span>

<span data-ttu-id="42260-190">L' `theme` argument de la fonction sera une chaîne avec la valeur `default` , `dark` ou `contrast` .</span><span class="sxs-lookup"><span data-stu-id="42260-190">The `theme` argument in the function will be a string with a value of `default`, `dark`, or `contrast`.</span></span>
