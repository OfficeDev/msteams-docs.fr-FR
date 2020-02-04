---
title: Obtenir le contexte de votre onglet
description: Indique comment obtenir le contexte utilisateur dans vos onglets
keywords: contexte utilisateur des onglets teams
ms.openlocfilehash: 01919999e38d6b659f014b0f05b76d3f332db9ab
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673548"
---
# <a name="get-context-for-your-microsoft-teams-tab"></a>Obtenir le contexte de votre onglet Microsoft teams

Votre onglet peut nécessiter des informations contextuelles pour afficher le contenu pertinent.

* L’onglet peut nécessiter des informations de base sur l’utilisateur, l’équipe ou la société.
* L’onglet peut nécessiter des paramètres régionaux et des informations sur les thèmes.
* Il se peut que votre onglet doive `entityId` lire `subEntityId` le ou identifie le contenu de cet onglet.

## <a name="user-context"></a>Contexte utilisateur

Le contexte de l’utilisateur, de l’équipe ou de la société peut être particulièrement utile lorsque

* Vous devez créer ou associer des ressources dans votre application à l’utilisateur ou à l’équipe spécifié.
* Vous souhaitez lancer un flux d’authentification auprès d’Azure Active Directory ou d’un autre fournisseur d’identité, et vous ne voulez pas demander à l’utilisateur de saisir de nouveau son nom d’utilisateur. (Pour plus d’informations sur l’authentification au sein de votre onglet Microsoft Teams, consultez la rubrique [authentifier un utilisateur sous votre onglet Microsoft teams](~/concepts/authentication/authentication.md).)

> [!IMPORTANT]
> Bien que ces informations utilisateur permettent d’assurer une expérience utilisateur sans complication, vous ne devez *pas* l’utiliser comme preuve d’identité. Par exemple, un agresseur peut charger votre page dans un « navigateur incorrect » et lui fournir toutes les informations souhaitées.

## <a name="accessing-context"></a>Contexte d’accès

Vous pouvez accéder aux informations de contexte de deux manières :

* Insérer des valeurs d’espace réservé d’URL
* Utiliser le [Kit de développement logiciel (SDK) JavaScript client Microsoft teams](/javascript/api/overview/msteams-client)

### <a name="getting-context-by-inserting-url-placeholder-values"></a>Obtenir le contexte en insérant des valeurs d’espace réservé URL

Utilisez des espaces réservés dans vos URL de configuration ou de contenu. Microsoft teams remplace les espaces réservés par les valeurs appropriées lors de la détermination de l’URL de contenu ou de configuration réelle à atteindre. Les espaces réservés disponibles incluent tous les champs de l’objet de [contexte](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest) . Les espaces réservés courants sont les suivants :

* {entityId} : ID que vous avez fourni pour l’élément dans cet onglet lors de la première [configuration de l’onglet](~/tabs/how-to/create-tab-pages/configuration-page.md).
* {subEntityId} : ID que vous avez fourni lors de la génération d’un [lien profond](~/concepts/build-and-test/deep-links.md) pour un élément spécifique _dans_ cet onglet. Il doit être utilisé pour restaurer un état spécifique au sein d’une entité ; par exemple, faire défiler ou activer une partie de contenu spécifique.
* {loginHint} : valeur appropriée en tant qu’indication de connexion pour Azure AD. Il s’agit généralement du nom de connexion de l’utilisateur actuel, dans son client d’origine.
* {userPrincipalName} : nom d’utilisateur principal de l’utilisateur actuel, dans le client actuel.
* {userObjectId} : ID d’objet Azure AD de l’utilisateur actuel, dans le client actuel.
* {Theme} : le thème `default`de l’interface utilisateur `dark`actuel, `contrast`, ou.
* {groupId} : ID du groupe Office 365 dans lequel réside l’onglet.
* {TID} : ID de client Azure AD de l’utilisateur actuel.
* {locale} : paramètres régionaux actuels de l’utilisateur mis en forme en tant que languageId-countryId (par exemple, en-US).

>[!NOTE]
>L’espace `{upn}` réservé précédent est maintenant obsolète. Pour des raisons de compatibilité descendante, il s' `{loginHint}`agit actuellement d’un synonyme de.

Par exemple, supposons dans votre manifeste d’onglets `configURL` que vous avez défini l’attribut sur

`"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"`

Et l’utilisateur connecté possède les attributs suivants :

* Le nom d’utilisateur est « user@example.com ».
* L’ID de client de son entreprise est « e2653c-etc »
* Il s’agit d’un membre du groupe Office 365 avec l’ID « 00209384-etc. »
* L’utilisateur a défini son thème teams sur « Dark »

Lorsqu’ils configurent votre onglet, teams appelle cette URL :

`https://www.contoso.com/config?name=user@example.com&tenant=e2653c-etc&group=00209384-etc&theme=dark`

### <a name="getting-context-by-using-the-microsoft-teams-javascript-library"></a>Obtention de contexte à l’aide de la bibliothèque JavaScript Microsoft teams

Vous pouvez également récupérer les informations ci-dessus à l’aide du [Kit de développement logiciel (SDK) JavaScript client Microsoft teams](/javascript/api/overview/msteams-client) en appelant `microsoftTeams.getContext(function(context) { /* ... */ })`.

La variable de contexte se présente comme dans l’exemple suivant.

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

## <a name="retrieving-context-in-private-channels"></a>Récupération du contexte dans les canaux privés

> [!Note]
> Les canaux privés sont actuellement en version préliminaire pour les développeurs privés.

Lorsque votre page de contenu est chargée dans un canal privé, les données que vous recevez `getContext` de l’appel seront obscurcies pour protéger la confidentialité du canal. Les champs suivants sont modifiés lorsque votre page de contenu se trouve dans un canal privé. Si votre page utilise l’une des valeurs ci-dessous, vous devez vérifier le `channelType` champ afin de déterminer si votre page est chargée dans un canal privé et de répondre de manière appropriée.

* `groupId`-Non défini pour les canaux privés
* `teamId`-Défini sur le threadId du canal privé
* `teamName`-Défini sur le nom du canal privé
* `teamSiteUrl`-Défini sur l’URL d’un site SharePoint distinct unique pour le canal privé
* `teamSitePath`-Défini sur le chemin d’accès à un site SharePoint distinct unique pour le canal privé
* `teamSiteDomain`-Défini sur le domaine d’un domaine de site SharePoint distinct unique pour le canal privé

## <a name="theme-change-handling"></a>Gestion des modifications de thème

Vous pouvez inscrire votre application pour être informée si le thème change en `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })`appelant.

L' `theme` argument de la fonction sera une chaîne avec la valeur `default`, `dark`ou. `contrast`