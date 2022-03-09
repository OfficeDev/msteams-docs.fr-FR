---
title: Obtenir un contexte Teams pour votre onglet
description: Décrit comment obtenir du contexte utilisateur dans vos onglets
ms.localizationpriority: medium
ms.topic: how-to
keywords: Contexte utilisateur sous l’onglet Équipes
ms.openlocfilehash: b4e693e127b06469a1f31a486fa8db9cc7ab4ba5
ms.sourcegitcommit: 830fdc80556a5fde642850dd6b4d1b7efda3609d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/09/2022
ms.locfileid: "63398805"
---
# <a name="get-context-for-your-tab"></a>Obtenir un contexte Teams pour votre onglet

Votre onglet nécessite des informations contextuelles pour afficher le contenu pertinent :

* Informations de base sur l’utilisateur, l’équipe ou l’entreprise.
* Informations sur les paramètres régionaux et le thème.
* Lisez ou `entityId` identifie `subEntityId` ce qui se trouve dans cet onglet.

## <a name="user-context"></a>Contexte utilisateur

Le contexte de l’utilisateur, de l’équipe ou de l’entreprise peut être particulièrement utile lorsque :

* Vous créez ou associez des ressources dans votre application à l’utilisateur ou à l’équipe spécifié.
* Vous lancez un flux d’authentification à partir de Microsoft Azure Active Directory (Azure AD) ou d’un autre fournisseur d’identité et vous n’exigez pas que l’utilisateur entre à nouveau son nom d’utilisateur.

Pour plus d’informations, [voir authentifier un utilisateur dans votre Microsoft Teams](~/concepts/authentication/authentication.md).

> [!IMPORTANT]
> Bien que ces informations utilisateur contribuent à une expérience utilisateur fluide, vous ne devez pas les utiliser comme preuve d’identité.  Par exemple, un attaquant peut charger votre page dans un navigateur et restituer des informations ou des demandes dangereuses.

## <a name="access-context-information"></a>Accéder aux informations de contexte

Vous pouvez accéder aux informations de contexte de deux façons :

* Insérez des valeurs d’espace réservé d’URL.
* Utilisez le [Microsoft Teams SDK client JavaScript.](/javascript/api/overview/msteams-client)

### <a name="get-context-by-inserting-url-placeholder-values"></a>Obtenir le contexte en insérant des valeurs d’espace réservé d’URL

Utilisez des espaces réservés dans vos URL de configuration ou de contenu. Microsoft Teams remplace les espaces réservés par les valeurs appropriées lorsqu’il détermine l’URL de configuration ou de contenu. Les espaces disponibles incluent tous les champs de [l’objet de](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) contexte. Voici les scénarios les plus courants :

* {entityId} : ID que vous avez fourni pour l’élément dans cet onglet lors de la première [configuration de l’onglet](~/tabs/how-to/create-tab-pages/configuration-page.md).
* {subEntityId}: ID que [vous avez fourni](~/concepts/build-and-test/deep-links.md) lors de la génération d’un lien profond pour un élément spécifique dans cet onglet. Cela doit être utilisé pour restaurer un état spécifique au sein d’une entité ; par exemple, le défilement vers ou l’activation d’un élément de contenu spécifique.
* {loginHint}: valeur appropriée comme conseil de connexion pour Azure AD. Il s’agit généralement du nom de connexion de l’utilisateur actuel dans son client d’accueil.
* {userPrincipalName} : nom d’utilisateur principal de l’utilisateur actuel dans le client actuel.
* {userObjectId}: ID Azure AD’objet de l’utilisateur actuel dans le client actuel.
* {theme}: Thème de l’interface utilisateur actuelle (IU) tel `default`que , `dark`ou `contrast`.
* {groupId}: ID du groupe Office 365 dans lequel réside l’onglet.
* {tid}: ID de client Azure AD de l’utilisateur actuel.
* {locale}: paramètres régionaux actuels de l’utilisateur au format languageId-countryId(en-us).

> [!NOTE]
> L’espace réservé `{upn}`précédent est désormais supprimé. Pour des raisons de compatibilité ascendante, il s'agit actuellement d'un synonyme de `{loginHint}`.

Par exemple, dans le manifeste de votre onglet `configURL` `"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"`, vous définissez l’attribut sur , l’utilisateur qui est inscrit possède les attributs suivants :

* Leur nom d’utilisateur **est user@example.com**.
* Leur ID de locataire d’entreprise **est e2653c-etc**.
* Ils sont membres du groupe Office 365 avec l’ID **00209384, etc**.
* L’utilisateur a Teams **thème foncé.**

Lorsqu’ils configurent l’onglet, Teams appelle l’URL suivante :

`https://www.contoso.com/config?name=user@example.com&tenant=e2653c-etc&group=00209384-etc&theme=dark`

### <a name="get-context-by-using-the-microsoft-teams-javascript-library"></a>Obtenir du contexte à l’aide de Microsoft Teams bibliothèque JavaScript

Vous pouvez également extraire les informations mentionnées ci-dessus à l’aide du client [Microsoft Teams JavaScript Client SDK](/javascript/api/overview/msteams-client) en appelant `microsoftTeams.getContext(function(context) { /* ... */ })`.

Le code suivant fournit un exemple de variable de contexte :

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
    "groupId": "Guid identifying the current Office 365 Group ID",
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
    "defaultOneNoteSectionId": "The OneNote section ID that is linked to the channel",
    "isMultiWindow": "The indication whether the tab is in a pop out window"
}
```

## <a name="retrieve-context-in-private-channels"></a>Récupérer le contexte dans les canaux privés

Lorsque votre page de contenu est chargée dans un canal privé, `getContext` les données que vous recevez de l’appel sont obscurcies pour protéger la confidentialité du canal.

Les champs suivants sont modifiés lorsque votre page de contenu se trouve dans un canal privé :

* `groupId`: Non définie pour les canaux privés
* `teamId`: définir sur le threadId du canal privé
* `teamName`: Définir sur le nom du canal privé
* `teamSiteUrl`: Définir sur l’URL d’un site SharePoint distinct et unique pour le canal privé
* `teamSitePath`: Définir sur le chemin d’accès d’un site SharePoint distinct et unique pour le canal privé
* `teamSiteDomain`: Définir sur le domaine d’un domaine de site SharePoint unique distinct pour le canal privé

Si votre page utilise l’une de ces valeurs, `channelType` `Private` la valeur du champ doit être pour déterminer si votre page est chargée dans un canal privé et peut répondre de manière appropriée.

## <a name="retrieve-context-in-microsoft-teams-connect-shared-channels"></a>Récupérer le contexte dans Microsoft Teams Connecter canaux partagés

> [!NOTE]
> Actuellement, les Microsoft Teams Connecter partagés sont en [prévisualisation développeur](../../resources/dev-preview/developer-preview-intro.md) uniquement.

Lorsque votre page de contenu est chargée dans un canal partagé Microsoft Teams Connecter, `getContext` les données que vous recevez de l’appel sont modifiées en raison de la liste unique d’utilisateurs dans les canaux partagés.

Les champs suivants sont modifiés lorsque votre page de contenu se trouve dans un canal partagé :

* `groupId`: Non définie pour les canaux partagés.
* `teamId`: Définie sur l’équipe `threadId` , le canal est partagé pour l’utilisateur actuel. Si l’utilisateur a accès à plusieurs équipes, `teamId` l’équipe qui héberge (crée) le canal partagé est définie.
* `teamName`: Définie sur le nom de l’équipe, le canal est partagé pour l’utilisateur actuel. Si l’utilisateur a accès à plusieurs équipes, `teamName` l’équipe qui héberge (crée) le canal partagé est définie.
* `teamSiteUrl`: définissez l’URL d’un site SharePoint distinct et unique pour le canal partagé.
* `teamSitePath`: définir sur le chemin d’accès d’un site SharePoint distinct et unique pour le canal partagé.
* `teamSiteDomain`: définissez ce domaine sur le domaine d’un SharePoint de site distinct et unique pour le canal partagé.

Outre ces modifications de champ, deux nouveaux champs sont disponibles pour les canaux partagés :

* `hostTeamGroupId`: définir sur l’équipe `groupId` associée à l’équipe d’hébergement ou l’équipe qui a créé le canal partagé. La propriété peut faire en sorte que les appels Graph API Microsoft récupèrent l’appartenance au canal partagé.
* `hostTeamTenantId`: définir sur l’équipe `tenantId` associée à l’équipe d’hébergement ou l’équipe qui a créé le canal partagé. La propriété peut être référencé avec l’ID `tid` `getContext` de locataire de l’utilisateur actuel trouvé dans le champ pour déterminer si l’utilisateur est interne ou externe au client de l’équipe d’hébergement.

Si votre page utilise l’une de ces valeurs, `channelType` `Shared` la valeur du champ doit être pour déterminer si votre page est chargée dans un canal partagé et peut répondre de manière appropriée.

## <a name="handle-theme-change"></a>Gérer la modification du thème

Vous pouvez inscrire votre application pour être informée si le thème change en appelant `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })`.

L’argument `theme` dans la fonction est une chaîne avec une valeur `default`de , `dark`ou `contrast`.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créer des onglets avec les Cartes adaptatives](~/tabs/how-to/build-adaptive-card-tabs.md)

## <a name="see-also"></a>Voir aussi

* [Recommandations en matière de conception d’onglets](../../tabs/design/tabs.md)
* [Teams onglets](~/tabs/what-are-tabs.md)
* [Créer un onglet personnel](~/tabs/how-to/create-personal-tab.md)
* [Créer un onglet de canal ou de groupe](~/tabs/how-to/create-channel-group-tab.md)
* [Utiliser des modules de tâche dans les onglets](~/task-modules-and-cards/task-modules/task-modules-tabs.md)
