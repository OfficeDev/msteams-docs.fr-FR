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
# <a name="get-context-for-your-microsoft-teams-tab"></a>Obtenir un contexte pour votre onglet Microsoft Teams

Votre onglet doit nécessiter des informations contextuelles pour afficher le contenu pertinent :

* Informations de base sur l’utilisateur, l’équipe ou l’entreprise.
* Informations sur les paramètres régionaux et le thème.
* Lisez `entityId` ou identifie ce qui se trouve dans cet `subEntityId` onglet.

## <a name="user-context"></a>Contexte utilisateur

Le contexte de l’utilisateur, de l’équipe ou de l’entreprise peut être particulièrement utile lorsque :

* Vous créez ou associez des ressources dans votre application à l’utilisateur ou à l’équipe spécifié.
* Vous lancez un flux d’authentification par rapport à Azure Active Directory ou à un autre fournisseur d’identité, et vous ne souhaitez pas obliger l’utilisateur à entrer à nouveau son nom d’utilisateur. Pour plus d’informations sur l’authentification dans votre onglet Microsoft Teams, voir Authentifier un utilisateur dans [Microsoft Teams onglet .](~/concepts/authentication/authentication.md)

> [!IMPORTANT]
> Bien que ces informations utilisateur contribuent à faciliter l’expérience utilisateur, vous ne devez *pas* l’utiliser comme preuve d’identité. Par exemple, un utilisateur malveillant peut charger votre page dans un « navigateur malveillant » et rendre des informations ou demandes potentiellement dangereuses.

## <a name="accessing-context"></a>Accès au contexte

Vous pouvez accéder aux informations de contexte de deux façons :

* Insérez des valeurs d’espace réservé d’URL.
* Utilisez le [Microsoft Teams SDK client JavaScript.](/javascript/api/overview/msteams-client)

### <a name="getting-context-by-inserting-url-placeholder-values"></a>Obtenir du contexte en insérant des valeurs d’espace réservé d’URL

Utilisez des espaces réservés dans vos URL de configuration ou de contenu. Microsoft Teams remplace les espaces réservés par les valeurs appropriées lorsqu’il détermine l’URL de configuration ou de contenu. Les espaces réservé disponibles incluent tous les champs de l’objet [Contexte](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true). Voici les scénarios les plus courants :

* {entityId} : ID que vous avez fourni pour l’élément dans cet onglet lors de la première [configuration de l’onglet](~/tabs/how-to/create-tab-pages/configuration-page.md).
* {subEntityId} : ID que vous avez fourni lors de la génération d’un [lien ciblé](~/concepts/build-and-test/deep-links.md) pour un élément spécifique _dans_ cet onglet. Elle doit être utilisée pour restaurer un état spécifique au sein d’une entité. par exemple, le défilement vers un contenu spécifique ou l’activation d’un contenu spécifique.
* {loginHint} : valeur appropriée comme indication de connexion pour Azure AD. Il s’agit généralement du nom de connexion de l’utilisateur actuel, dans son client.
* {userPrincipalName} : nom d’utilisateur principal de l’utilisateur actuel, dans le client actuel.
* {userObjectId} : ID d’objet Azure AD de l’utilisateur actuel dans le locataire actuel.
* {theme} : le thème d’interface utilisateur actuel, tel `default`, `dark`ou `contrast`.
* {groupId} : ID du groupe Office 365 dans lequel se trouve l’onglet.
* {tid}: ID de client Azure AD de l’utilisateur actuel.
* {locale}: paramètres régionaux actuels de l’utilisateur au format languageId-countryId. Par exemple, en-us.

>[!NOTE]
>L’espace réservé `{upn}`précédent est désormais supprimé. Pour des raisons de compatibilité ascendante, il s'agit actuellement d'un synonyme de `{loginHint}`.

Par exemple, supposons que, dans le manifeste de votre onglet, vous définissez l’attribut sur , l’utilisateur inscrit possède `configURL` `"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"` les attributs suivants :

* Leur nom d’utilisateur est « user@example.com ».
* Leur ID de locataire d’entreprise est « e2653c-etc ».
* Ils sont membres du groupe Office 365 avec l’ID « 00209384-etc ».
* L’utilisateur a Teams thème « dark ».

Lorsqu’ils configurent votre onglet, Teams l’URL suivante :

`https://www.contoso.com/config?name=user@example.com&tenant=e2653c-etc&group=00209384-etc&theme=dark`

### <a name="getting-context-by-using-the-microsoft-teams-javascript-library"></a>Obtenir du contexte à l’aide de la bibliothèque JavaScript de Microsoft Teams

Vous pouvez également extraire les informations mentionnées ci-dessus à l’aide du client [Microsoft Teams JavaScript Client SDK](/javascript/api/overview/msteams-client) en appelant `microsoftTeams.getContext(function(context) { /* ... */ })`.

La variable de contexte ressemble à l’exemple suivant :

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

## <a name="retrieving-context-in-private-channels"></a>Récupération de contexte dans les canaux privés

> [!Note]
> Les canaux privés sont actuellement en prévisualisation du développeur privé.

Lorsque votre page de contenu est chargée dans un canal privé, les données que vous recevez de l’appel `getContext` sont masquées pour protéger la confidentialité du canal. Les champs suivants sont modifiés lorsque votre page de contenu se trouve dans un canal privé. Si votre page utilise l’une des valeurs ci-dessous, vous devez vérifier le champ `channelType` pour déterminer si votre page est chargée dans un canal privé et y répondre de façon appropriée.

* `groupId`: Non définie pour les canaux privés
* `teamId`: définir sur le threadId du canal privé
* `teamName`: Définir sur le nom du canal privé
* `teamSiteUrl`: Définir sur l’URL d’un site SharePoint distinct et unique pour le canal privé
* `teamSitePath`: Définir sur le chemin d’accès d’un site SharePoint distinct et unique pour le canal privé
* `teamSiteDomain`: Définir sur le domaine d’un domaine de site SharePoint unique et distinct pour le canal privé

> [!Note]
>  teamSiteUrl fonctionne également bien pour les canaux standard.

## <a name="theme-change-handling"></a>Gestion des changements de thème

Vous pouvez enregistrer votre application pour vous faire savoir si le thème change en appelant `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })`.

L’`theme`argument de la fonction est une chaîne qui a une valeur `default`, `dark`ou `contrast`.
