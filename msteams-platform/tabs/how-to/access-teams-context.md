---
title: Obtenir un contexte Teams pour votre onglet
description: Dans ce module, découvrez comment obtenir le contexte utilisateur dans vos onglets, le contexte utilisateur et les informations de contexte Access
ms.localizationpriority: medium
ms.topic: how-to
ms.openlocfilehash: 63bbc9c0e5f20e293f9230000597860e3f053274
ms.sourcegitcommit: 79d525c0be309200e930cdd942bc2c753d0b718c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/19/2022
ms.locfileid: "66841721"
---
# <a name="get-context-for-your-tab"></a>Obtenir un contexte Teams pour votre onglet

Votre onglet nécessite des informations contextuelles pour afficher le contenu pertinent :

* Informations de base sur l’utilisateur, l’équipe ou l’entreprise.
* Paramètres régionaux et informations de thème.
* `page.subPageId` Qui `page.id` identifient ce qui se trouve dans cet onglet (appelé `entityId` et `subEntityId` antérieur à TeamsJS v.2.0.0).

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

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

Utilisez des espaces réservés dans vos URL de configuration ou de contenu. Microsoft Teams remplace les espaces réservés par les valeurs appropriées lorsqu’il détermine l’URL de configuration ou de contenu. Les espaces réservés disponibles incluent tous les champs de l’objet [de contexte](/javascript/api/@microsoft/teams-js/app.context) . Les espaces réservés courants incluent les listes suivantes :

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
> Actuellement, Microsoft Teams Connect canaux partagés sont en [préversion](../../resources/dev-preview/developer-preview-intro.md) développeur uniquement.

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
> Chaque fois qu’un utilisateur redémarre ou recharge le bureau ou le client web Teams, un ID de session est créé, suivi par la session Teams, tandis qu’un utilisateur quitte les applications Teams et le recharge dans la plateforme Teams, un ID de session d’application est créé, suivi par session d’application.

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
