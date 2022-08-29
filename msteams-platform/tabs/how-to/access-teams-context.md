---
title: Obtenir un contexte Teams pour votre onglet
description: Découvrez comment mettre en contexte votre onglet, le contexte de l’utilisateur, de l’équipe ou de l’entreprise, accéder aux informations, récupérer le contexte dans des canaux privés ou partagés et gérer les modifications de thème.
ms.localizationpriority: high
ms.topic: how-to
ms.openlocfilehash: ddd3d35d9069dd185fa4e77913ca0873e2d31b24
ms.sourcegitcommit: 87bba925d005eb331d876a0b9b75154f8100e911
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2022
ms.locfileid: "67450386"
---
# <a name="get-context-for-your-tab"></a>Obtenir un contexte Teams pour votre onglet

Votre onglet nécessite des informations contextuelles pour afficher le contenu pertinent :

* Informations de base sur l’utilisateur, l’équipe ou l’entreprise.
* Paramètres régionaux et informations de thème.
* `page.subPageId` Qui `page.id` identifient ce qui se trouve dans cet onglet (appelé `entityId` et `subEntityId` antérieur à TeamsJS v.2.0.0).

## <a name="user-context"></a>Contexte utilisateur

Le contexte de l’utilisateur, de l’équipe ou de l’entreprise peut être particulièrement utile quand :

* Vous créez ou associez des ressources dans votre application à l’utilisateur ou à l’équipe spécifié.
* Vous lancez un flux d’authentification à partir d’Microsoft Azure Active Directory (Azure AD) ou d’un autre fournisseur d’identité, et vous n’avez pas besoin que l’utilisateur entre à nouveau son nom d’utilisateur.

Pour plus d’informations, consultez [authentifier un utilisateur dans votre Microsoft Teams](~/concepts/authentication/authentication.md).

> [!IMPORTANT]
> Bien que ces informations utilisateur puissent vous aider à fournir une expérience utilisateur fluide, vous ne devez pas les utiliser comme preuve d’identité.  Par exemple, un attaquant peut charger votre page dans un navigateur et afficher des informations ou des demandes dangereuses.

## <a name="access-context-information"></a>Accéder aux informations de contexte

Vous pouvez accéder aux informations de contexte de deux façons :

* Utilisation des [valeurs d’espace réservé d’URL](#get-context-by-inserting-url-placeholder-values).
* À partir de l’objet [de contexte](/javascript/api/@microsoft/teams-js/app.context) du kit de développement logiciel (SDK) client JavaScript Microsoft Teams.

### <a name="get-context-by-inserting-url-placeholder-values"></a>Obtenir le contexte en insérant des valeurs d’espace réservé d’URL

Utilisez des espaces réservés dans vos URL de configuration ou de contenu. Microsoft Teams remplace les espaces réservés par les valeurs appropriées lorsqu’il détermine l’URL de configuration ou de contenu. Les espaces réservés disponibles incluent tous les champs de l’objet [de contexte](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) . Les espaces réservés courants incluent les propriétés suivantes :

* [{page.id}](/javascript/api/@microsoft/teams-js/app.pageinfo#@microsoft-teams-js-app-pageinfo-id) : ID unique défini par le développeur pour la page définie lors [de la première configuration de la page](~/tabs/how-to/create-tab-pages/configuration-page.md). (Connu comme `{entityId}` antérieur à TeamsJS v.2.0.0).
* [{page.subPageId}](/javascript/api/@microsoft/teams-js/app.pageinfo#@microsoft-teams-js-app-pageinfo-subpageid) : ID unique défini par le développeur pour la sous-page que ce contenu pointe défini lors de la génération d’un [lien profond](~/concepts/build-and-test/deep-links.md) pour un élément spécifique dans la page. (Connu comme `{subEntityId}` antérieur à TeamsJS v.2.0.0).
* [{user.loginHint}](/javascript/api/@microsoft/teams-js/app.userinfo#@microsoft-teams-js-app-userinfo-loginhint) : valeur appropriée comme indicateur de connexion pour Azure AD. Il s’agit généralement du nom de connexion de l’utilisateur actuel dans son locataire d’origine. (Connu comme `{loginHint}` antérieur à TeamsJS v.2.0.0).
* [{user.userPrincipalName}](/javascript/api/@microsoft/teams-js/app.userinfo#@microsoft-teams-js-app-userinfo-userprincipalname) : nom d’utilisateur principal de l’utilisateur actuel dans le locataire actuel. (Connu comme `{userPrincipalName}` antérieur à TeamsJS v.2.0.0).
* [{user.id}](/javascript/api/@microsoft/teams-js/app.userinfo#@microsoft-teams-js-app-userinfo-id) : ID d’objet Azure AD de l’utilisateur actuel dans le locataire actuel. (Connu comme `{userObjectId}` antérieur à TeamsJS v.2.0.0).
* [{app.theme}](/javascript/api/@microsoft/teams-js/app.appinfo#@microsoft-teams-js-app-appinfo-theme) : thème d’interface utilisateur actuel, tel que `default`, `dark`ou `contrast`. (Connu comme `{theme}` antérieur à TeamsJS v.2.0.0).
* [{team.groupId}](/javascript/api/@microsoft/teams-js/app.teaminfo#@microsoft-teams-js-app-teaminfo-groupid) : ID du groupe Office 365 dans lequel réside l’onglet. (Connu comme `{groupId}` antérieur à TeamsJS v.2.0.0)
* [{user.tenant.id}](/javascript/api/@microsoft/teams-js/app.tenantinfo#@microsoft-teams-js-app-tenantinfo-id) : ID de locataire Azure AD de l’utilisateur actuel. (Connu comme `{tid}` antérieur à TeamsJS v.2.0.0).
* [{app.locale}](/javascript/api/@microsoft/teams-js/app.appinfo#@microsoft-teams-js-app-appinfo-locale) : paramètres régionaux actuels de l’utilisateur au format *languageId-countryId*, par exemple `en-us`. (Connu comme `{locale}` antérieur à TeamsJS v.2.0.0).

> [!NOTE]
> L’espace réservé `{upn}`précédent est désormais supprimé. Pour des raisons de compatibilité ascendante, il s'agit actuellement d'un synonyme de `{user.loginHint}`.

Par exemple, dans le manifeste de votre application, si vous définissez l’attribut *configurationUrl* tab `"https://www.contoso.com/config?name={user.loginHint}&tenant={user.tenant.id}&group={team.groupId}&theme={app.theme}"` et que l’utilisateur connecté a les attributs suivants :

* Leur nom d’utilisateur est **user@example.com**.
* Leur ID de locataire d’entreprise est **e2653c-etc**.
* Ils sont membres du groupe Office 365 avec l’ID **00209384-etc**.
* L’utilisateur a défini son thème Teams sur **sombre**.

. . . Teams appelle ensuite l’URL suivante lors de la configuration de l’onglet :

`https://www.contoso.com/config?name=user@example.com&tenant=e2653c-etc&group=00209384-etc&theme=dark`

### <a name="get-context-by-using-the-microsoft-teams-javascript-library"></a>Obtenir le contexte à l’aide de la bibliothèque JavaScript Microsoft Teams

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
    "hostClientType": "The type of host client. Possible values are android, ios, web, desktop, surfaceHub, teamsRoomsAndroid, teamsPhones, teamsDisplays rigel (deprecated, use teamsRoomsWindows instead)",
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

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

## <a name="typescript"></a>TypeScript

```TypeScript
import { app, Context } from "@microsoft/teams-js";

app.getContext().then((context: Context) => {
    /*...*/
});
```

Modèle équivalent `async/await` :

```TypeScript
import { app, Context } from "@microsoft/teams-js";

async function example() {
  const context: Context = await app.getContext();
  /*...*/
}
```

## <a name="javascript"></a>JavaScript

```js
import { app, Context } from "@microsoft/teams-js";

app.getContext().then((context) => {
    /*...*/
});
```

Modèle équivalent `async/await` :

```js
import { app, Context } from "@microsoft/teams-js";

async function example() {
  const context = await app.getContext();
  /*...*/
}
```

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

## <a name="typescript"></a>TypeScript

```TypeScript
import * as microsoftTeams from "@microsoft/teams-js";

microsoftTeams.getContext((context: microsoftTeams.Context) => {
  /* ... */
});
```

## <a name="javascript"></a>JavaScript

```js
import microsoftTeams from "@microsoft/teams-js";

microsoftTeams.getContext((context) => {
  /* ... */ 
});
```

---

Le tableau suivant répertorie les propriétés de contexte couramment utilisées de l’objet *de contexte* :

| Nom de TeamsJS v2 | Nom de TeamsJS v1 | Description |
|-----------------|-----------------|-------------|
| team.internalId | teamId | ID Microsoft Teams pour l’équipe à laquelle le contenu est associé. |
| team.displayName | teamName | Nom de l’équipe à laquelle le contenu est associé. |
| channel.id | channelId | ID Microsoft Teams pour le canal auquel le contenu est associé. |
| channel.displayName | channelName | Nom du canal auquel le contenu est associé. |
| chat.id | chatId | ID Microsoft Teams pour la conversation à laquelle le contenu est associé. |
| app.locale | local | Paramètres régionaux actuels que l’utilisateur a configurés pour l’application au format languageId-countryId (par exemple, en-us). |
| page.id | entityId | ID unique défini par le développeur pour la page vers laquelle pointe ce contenu. |
| page.subPageId | subEntityId | ID unique défini par le développeur pour la sous-page vers laquelle pointe ce contenu. Ce champ doit être utilisé pour restaurer à un état spécifique au sein d’une page, tel que le défilement vers ou l’activation d’un élément de contenu spécifique. |
| user.loginHint | loginHint | Valeur appropriée pour une utilisation en tant que login_hint lors de l’authentification auprès d’Azure AD. Étant donné qu’une partie malveillante peut exécuter votre contenu dans un navigateur, cette valeur doit être utilisée uniquement comme indicateur de l’identité de l’utilisateur et jamais comme preuve d’identité. Ce champ est disponible uniquement lorsque l’autorisation d’identité est demandée dans le manifeste. |
| user.userPrincipalName | Upn | UPN de l’utilisateur actuel. Il peut s’agir d’un UPN authentifié en externe (par exemple, des utilisateurs invités). Étant donné qu’une partie malveillante exécute votre contenu dans un navigateur, cette valeur doit être utilisée uniquement comme indicateur de l’identité de l’utilisateur et jamais comme preuve d’identité. Ce champ est disponible uniquement lorsque l’autorisation d’identité est demandée dans le manifeste. |
| user.id | userObjectId | ID d’objet Azure AD de l’utilisateur actuel. Étant donné qu’une partie malveillante exécute votre contenu dans un navigateur, cette valeur doit être utilisée uniquement comme indicateur de l’identité de l’utilisateur et jamais comme preuve d’identité. Ce champ est disponible uniquement lorsque l’autorisation d’identité est demandée dans le manifeste. |
| user.tenant.id | Tid | ID de locataire Azure AD de l’utilisateur actuel. Étant donné qu’une partie malveillante peut exécuter votre contenu dans un navigateur, cette valeur doit être utilisée uniquement comme indicateur de l’identité de l’utilisateur et jamais comme preuve d’identité. Ce champ est disponible uniquement lorsque l’autorisation d’identité est demandée dans le manifeste. |
| team.groupId | groupId | ID de groupe Office 365 pour l’équipe à laquelle le contenu est associé. Ce champ est disponible uniquement lorsque l’autorisation d’identité est demandée dans le manifeste. |
| app.theme  | thème | Le thème d’interface utilisateur actuel : par défaut, sombre, contraste |
| page.isFullScreen | IsFullScreen | Indiquez si la page est en mode plein écran. |
| team.type | teamType | Type de l’équipe. |
| sharepointSite.teamSiteUrl | teamSiteUrl | Site SharePoint racine associé à l’équipe. |
| sharepointSite.teamSiteDomain | teamSiteDomain | Domaine du site SharePoint racine associé à l’équipe. |
| sharepointSite.teamSitePath | teamSitePath | Chemin relatif du site SharePoint associé à l’équipe. |
| channel.relativeUrl | channelRelativeUrl | Chemin d’accès relatif au dossier SharePoint associé au canal. |
| app.host.sessionId | Sessionid | ID unique de la session hôte active à utiliser pour la mise en corrélation des données de télémétrie. |
| team.userRole | userTeamRole | Rôle de l’utilisateur dans l’équipe. Étant donné qu’une partie malveillante peut exécuter votre contenu dans un navigateur, cette valeur doit être utilisée uniquement comme indicateur du rôle de l’utilisateur, et jamais comme preuve de son rôle. |
| team.isArchived | isTeamArchived | Indique si l’équipe est archivée. Les applications doivent l’utiliser comme signal pour empêcher toute modification du contenu associé aux équipes archivées. |
| app.host.clientType | hostClientType | Type du client hôte. Les valeurs possibles sont : android, ios, web, desktop, rigel |
| page.frameContext | frameContext | Contexte dans lequel l’URL de page est chargée (contenu, tâche, paramètre, suppression, sidePanel) |
| sharepoint | sharepoint | Contexte SharePoint. Cette option n’est disponible qu’en cas d’hébergement dans SharePoint. |
| user.tenant.teamsSku | tenantSKU | Type de licence pour le locataire utilisateur actuel. Les valeurs possibles sont enterprise, free, edu, unknown |
| user.licenseType | userLicenseType | Type de licence pour l’utilisateur actuel. Les valeurs possibles sont les plans entreprise E1, E3 et E5 |
| app.parentMessageId | parentMessageId | ID du message parent à partir duquel ce module de tâche a été lancé. Cela n’est disponible que dans les modules de tâches lancés à partir de cartes de bot. |
| app.host.ringId | ringId | ID d’anneau actuel. |
| app.sessionId | appSessionId | ID unique de la session hôte active à utiliser pour la mise en corrélation des données de télémétrie. |
| user.isCallingAllowed | isCallingAllowed | Indique si l’appel est autorisé pour l’utilisateur connecté actuel. |
| user.isPSTNCallingAllowed | isPSTNCallingAllowed | Indique si l’appel RTC est autorisé pour l’utilisateur actuel |
| meeting.id | meetingId | ID de réunion utilisé par l’onglet lors de l’exécution dans le contexte de la réunion. |
| channel.defaultOneNoteSectionId | defaultOneNoteSectionId | ID de section OneNote lié au canal. |
| page.isMultiWindow | isMultiWindow | Indication indiquant si l’onglet se trouve dans une fenêtre contextuelle. |

Pour plus d’informations, consultez [Mises à jour à l’interface *contextuel* et à](using-teams-client-sdk.md#updates-to-the-context-interface) la référence de l’API d’interface [de contexte](/javascript/api/@microsoft/teams-js/app.context).

## <a name="retrieve-context-in-private-channels"></a>Récupérer le contexte dans des canaux privés

> [!NOTE]
> Les canaux privés sont actuellement en préversion des développeurs privés uniquement.

Lorsque votre page de contenu est chargée dans un canal privé, les données que vous recevez de l’appel `getContext` sont masquées pour protéger la confidentialité du canal.

Les champs suivants sont modifiés lorsque votre page de contenu se trouve dans un canal privé :

* `team.groupId`: Non défini pour les canaux privés
* `team.internalId`: défini sur le threadId du canal privé
* `team.displayName`: définir sur le nom du canal privé
* `sharepointSite.url`: définir sur l’URL d’un site SharePoint distinct et unique pour le canal privé
* `sharepointSite.path`: définir le chemin d’accès d’un site SharePoint distinct et unique pour le canal privé
* `sharepointSite.domain`: défini sur le domaine d’un domaine de site SharePoint distinct et unique pour le canal privé

Si votre page utilise l’une de ces valeurs, la valeur du `channel.membershipType` champ doit être `Private` de déterminer si votre page est chargée dans un canal privé et peut répondre de manière appropriée.

## <a name="retrieve-context-in-microsoft-teams-connect-shared-channels"></a>Récupérer le contexte dans Microsoft Teams Connect canaux partagés

> [!NOTE]
> Actuellement, Microsoft Teams Connect canaux partagés sont en préversion uniquement pour les développeurs.

Lorsque votre page de contenu est chargée dans un canal partagé Microsoft Teams Connect, les données que vous recevez de l’appel `getContext` sont modifiées en raison de la liste unique d’utilisateurs dans les canaux partagés.
Les champs suivants sont modifiés lorsque votre page de contenu se trouve dans un canal partagé :

* `team.groupId`: non défini pour les canaux partagés.
* `team.internalId`: défini sur l’équipe `threadId` , le canal est partagé pour l’utilisateur actuel. Si l’utilisateur a accès à plusieurs équipes, celle-ci est définie sur l’équipe qui héberge (crée) le canal partagé.
* `team.displayName`: défini sur le nom de l’équipe, le canal est partagé pour l’utilisateur actuel. Si l’utilisateur a accès à plusieurs équipes, celle-ci est définie sur l’équipe qui héberge (crée) le canal partagé.
* `sharepointSite.url`: défini sur l’URL d’un site SharePoint distinct et unique pour le canal partagé.
* `sharepointSite.path`: défini sur le chemin d’accès d’un site SharePoint distinct et unique pour le canal partagé.
* `sharepointSite.domain`: défini sur le domaine d’un domaine de site SharePoint distinct et unique pour le canal partagé.

En plus de ces modifications de champ, deux nouveaux champs sont disponibles pour les canaux partagés :

* `hostTeamGroupId`: affectez la `team.groupId` valeur associée à l’équipe d’hébergement ou à l’équipe qui a créé le canal partagé. La propriété peut permettre à Microsoft API Graph appels de récupérer l’appartenance au canal partagé.
* `hostTeamTenantId`: affectez la `channel.ownerTenantId` valeur associée à l’équipe d’hébergement ou à l’équipe qui a créé le canal partagé. La propriété peut être référencée de manière croisée avec l’ID de locataire de l’utilisateur actuel trouvé dans le `user.tenant.id` champ de l’objet *de contexte* pour déterminer si l’utilisateur est interne ou externe au locataire de l’équipe d’hébergement.

Si votre page utilise l’une de ces valeurs, la valeur du `channel.membershipType` champ doit être `Shared` de déterminer si votre page est chargée dans un canal partagé et peut répondre de manière appropriée.

> [!NOTE]
> `teamSiteUrl` fonctionne également bien pour les canaux standard.
> Si votre page utilise l’une de ces valeurs, la valeur du `channelType` champ doit être `Shared` de déterminer si votre page est chargée dans un canal partagé et peut répondre de manière appropriée.

## <a name="get-context-in-shared-channels"></a>Obtenir le contexte dans les canaux partagés

Lorsque l’expérience utilisateur de contenu est chargée dans un canal partagé, utilisez les données reçues de l’appel pour les modifications de `getContext` canal partagé. Si l’onglet utilise l’une des valeurs suivantes, vous devez remplir le `channelType` champ pour déterminer si l’onglet est chargé dans un canal partagé et répondre de manière appropriée.
Pour les canaux partagés, la `groupId` valeur est `null`, car l’ID de groupe de l’équipe hôte ne reflète pas précisément l’appartenance réelle du canal partagé. Pour résoudre ce problème, les propriétés et `hostTenantID` les `hostTeamGroupID` nouvelles propriétés sont ajoutées et utiles pour effectuer des appels Microsoft API Graph pour récupérer l’appartenance. `hostTeam` fait référence à l’équipe qui a créé le canal partagé. `currentTeam` fait référence à Team à partir de laquelle l’utilisateur actuel accède au canal partagé.

Pour plus d’informations sur ces concepts, consultez [Canaux partagés](~/concepts/build-and-test/shared-channels.md).

Utilisez les propriétés suivantes `getContext` dans les canaux partagés :

| Propriété | Description |
|----------|--------------|
|`channelId`| La propriété est définie sur l’ID de thread du canal SC.|
|`channelType`| La propriété est définie sur pour les `sharedChannel` canaux partagés.|
|`groupId`|La propriété est `null` destinée aux canaux partagés.|
|`hostTenantId`| La propriété est nouvellement ajoutée et décrit l’ID de locataire de l’hôte, utile pour la comparaison avec la propriété ID de locataire de `tid` l’utilisateur actuel. |
|`hostTeamGroupId`| La propriété vient d’être ajoutée et décrit l’ID de groupe Azure AD de l’équipe hôte, utile pour effectuer des appels Microsoft API Graph pour récupérer l’appartenance au canal partagé. |
|`teamId`|La propriété vient d’être ajoutée et définie sur l’ID de thread de l’équipe partagée actuelle. |
|`teamName`|La propriété est définie sur l’équipe `teamName`partagée actuelle. |
|`teamType`|La propriété est définie sur l’équipe `teamType`partagée actuelle.|
|`teamSiteUrl`|La propriété décrit le canal `channelSiteUrl`partagé .|
|`teamSitePath`| La propriété décrit le canal `channelSitePath`partagé .|
|`teamSiteDomain`| La propriété décrit le canal `channelSiteDomain`partagé .|
|`tenantSKU`| La propriété décrit l’équipe `tenantSKU`hôte.|
|`tid`|  La propriété décrit l’ID de locataire de l’utilisateur actuel.|
|`userObjectId`|  La propriété décrit l’ID de l’utilisateur actuel.|
|`userPrincipalName`| La propriété décrit l’UPN de l’utilisateur actuel.|

Pour plus d’informations sur les canaux partagés, consultez [Canaux partagés](~/concepts/build-and-test/shared-channels.md).

## <a name="handle-theme-change"></a>Gérer la modification du thème

Vous pouvez inscrire votre application pour être informé si le thème change en appelant `microsoftTeams.app.registerOnThemeChangeHandler(function(theme) { /* ... */ })`.

L’argument `theme` dans la fonction est une chaîne avec la valeur `default`, `dark`ou `contrast`.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créer des onglets avec les Cartes adaptatives](~/tabs/how-to/build-adaptive-card-tabs.md)

## <a name="see-also"></a>Voir aussi

* [Instructions de conception de tabulation](../../tabs/design/tabs.md)
* [Onglets Teams](~/tabs/what-are-tabs.md)
* [Créer un onglet personnel](~/tabs/how-to/create-personal-tab.md)
* [Créer un onglet de canal ou de groupe](~/tabs/how-to/create-channel-group-tab.md)
* [Utiliser des modules de tâche dans les onglets](~/task-modules-and-cards/task-modules/task-modules-tabs.md)
