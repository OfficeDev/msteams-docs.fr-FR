---
title: Microsoft Teams version préliminaire du SDK client JavaScript v2
description: Comprendre les modifications apportées avec Microsoft Teams javaScript client SDK v2 Preview
ms.date: 11/15/2021
ms.topic: conceptual
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: 4214cc4a738b979a7fa95b2bd9c5110ea0360c68
ms.sourcegitcommit: c65a868744e4108b5d786de2350981e3f1f05718
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2022
ms.locfileid: "62081092"
---
# <a name="microsoft-teams-javascript-client-sdk-v2-preview"></a>Microsoft Teams version préliminaire du SDK client JavaScript v2

Avec le [SDK client JavaScript v2 Preview Microsoft Teams, le SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-beta&preserve-view=true)Teams existant ( ou simplement ) a été `@microsoft/teams-js` refactorisation pour permettre aux développeurs Teams d’étendre les applications Teams pour qu’elles s’exécutent en `TeamsJS` [Outlook et Office](overview.md). Du point de vue fonctionnel, le SDK TeamsJS v2 Preview ( ) est un sur-ensemble du `@microsoft/teams-js@next` SDK TeamsJS actuel, il prend en charge les fonctionnalités d’application Teams existantes tout en ajoutant la possibilité d’héberger des applications Teams dans Outlook et Office.

Il existe deux modifications importantes dans l’aperçu du SDK TeamsJS v2 dont votre code devra tenir compte pour pouvoir s’exécuter dans d’Microsoft 365 applications :

* [**Les fonctions de rappel retournent désormais des objets Promise.**](#callbacks-converted-to-promises) Toutes les fonctions existantes avec un paramètre de rappel ont été modernisers pour renvoyer un objet JavaScript [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) afin d’améliorer la gestion des opérations asynchrones et la lisibilité du code.

 - [**Les API sont désormais organisées en *fonctionnalités.***](#apis-organized-into-capabilities) Vous pouvez voir les fonctionnalités comme des regroupements logiques d’API qui fournissent des fonctionnalités similaires, telles que `authentication` , , , et `calendar` `mail` `monetization` `meeting` `sharing` .

 Vous pouvez utiliser [l’extension Teams Shared Computer Toolkit pour](https://aka.ms/teams-toolkit) Visual Studio Code pour simplifier le processus de mise à jour de votre application Teams, comme décrit dans la section suivante.

> [!NOTE]
> Pour qu’une application Teams existante s’exécute en Outlook et Office nécessite les deux :
> 1. Dépendance sur le `@microsoft/teams-js@2.0.0-beta.1` ou les ultérieures, et
> 2. Modification du code d’application existant en fonction des modifications requises décrites dans ce document.
>
>  Si vous référencez (ou une ultérieure) à partir d’une application Teams existante, vous verrez des avertissements d’annulation si votre code appelle des API qui `@microsoft/teams-js@2.0.0-beta.1` ont été modifiées. Une couche de traduction d’API (mappage du SDK actuel pour prévisualiser les appels d’API du SDK) est fournie pour permettre aux applications Teams existantes de continuer à fonctionner dans Teams jusqu’à ce qu’elles soient en mesure de mettre à jour le code pour fonctionner avec l’aperçu du SDK TeamsJS v2. Une fois que vous avez mis à jour votre code avec les modifications décrites dans cet article, votre onglet personnel s’exécute également Outlook et Office.

## <a name="updating-to-the-teams-client-sdk-v2-preview"></a>Mise à jour vers le Teams client SDK v2 Preview

Le moyen le plus simple de mettre à jour votre application Teams pour utiliser l’aperçu du SDK TeamsJS v2 consiste à utiliser [l’extension Teams Shared Computer Toolkit](https://aka.ms/teams-toolkit) pour Visual Studio Code. Cette section vous présente les étapes à suivre pour ce faire. Si vous préférez mettre à jour manuellement votre code, consultez les [rappels convertis](#callbacks-converted-to-promises) en promesses et LES API organisées en [sections](#apis-organized-into-capabilities) de fonctionnalités pour plus d’informations sur les modifications d’API requises.

### <a name="1-install-the-latest-teams-toolkit-vs-code-extension"></a>1. Installer la dernière extension de Teams Shared Computer Toolkit VS Code

Dans la *Visual Studio Code Extensions Marketplace,* recherchez Teams Shared Computer Toolkit **et** installez la version ou version `2.10.0` ultérieure. Le kit de ressources fournit deux commandes pour aider le processus :

1. Commande de mise à jour de votre schéma de manifeste
1. Commande pour mettre à jour vos références et sites d’appel du SDK

Voici les deux mises à jour clés dont vous aurez besoin pour exécuter une application Teams onglet personnel dans d’autres applications Microsoft 365 suivantes : « »

### <a name="2-updating-the-manifest"></a>2. Mise à jour du manifeste

# <a name="teams-toolkit"></a>[Toolkit Teams](#tab/manifest-teams-toolkit)

1. Ouvrez *la palette de commandes*: `Ctrl+Shift+P`
1. Exécutez **Teams : mettre à** niveau Teams manifeste pour prendre en charge Outlook commande Office applications et sélectionnez votre fichier manifeste d’application. Les modifications seront apportées en place.

# <a name="manual-steps"></a>[Étapes manuelles](#tab/manifest-manual)

Ouvrez votre Teams de l’application et mettez à jour les `$schema` `manifestVersion` valeurs suivantes :

```json
{
    "$schema" : "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
    "manifestVersion" : "m365DevPreview"
}
```
---

Si vous avez utilisé Teams Shared Computer Toolkit pour créer votre application personnelle, vous pouvez également l’utiliser pour valider les modifications apportées à votre fichier manifeste et identifier les erreurs éventuelles. Ouvrez la palette de commandes et recherchez Teams : Valider le fichier manifeste ou sélectionnez l’option dans le menu Déploiement de l’Teams Shared Computer Toolkit (recherchez l’icône Teams sur le côté gauche de `Ctrl+Shift+P` Visual Studio Code). 

:::image type="content" source="images/toolkit-validate-manifest-file.png" alt-text="Teams Shared Computer Toolkit’option « Valider le fichier manifeste » sous le menu « Déploiement »":::

### <a name="2-update-sdk-references"></a>2. Mettre à jour les références du SDK

Pour s’exécuter Outlook et Office, votre application doit dépendre du [package npm](https://www.npmjs.com/package/@microsoft/teams-js/v/2.0.0-beta.1) (ou d’une `@microsoft/teams-js@2.0.0-beta.1` version *bêta* ultérieure). Pour effectuer ces étapes manuellement et pour plus d’informations sur les modifications apportées aux API, consultez les sections suivantes sur les [rappels convertis](#callbacks-converted-to-promises) en promesses et api organisées en [fonctionnalités.](#apis-organized-into-capabilities)

1. Assurez-vous que vous [avez Teams Shared Computer Toolkit](https://aka.ms/teams-toolkit) `v2.10.0` ou ultérieure
1. Ouvrez *la palette de commandes*: `Ctrl+Shift+P`
1. Exécuter la commande `Teams: Upgrade Teams JS SDK references to support Outlook and Office apps`

Une fois l’exécution terminée, l’utilitaire aura mis à jour votre fichier avec la dépendance du `package.json` SDK TeamsJS v2 Preview (ou version ultérieure), et vos fichiers et vos fichiers seront mis à jour avec `@microsoft/teams-js@2.0.0-beta.1` `*.js/.ts` `*.jsx/.tsx` :

> [!div class="checklist"]
> * `package.json` références au SDK TeamsJS v2 Preview
> * Instructions Import pour le SDK TeamsJS v2 Preview
> * [Appels de fonction, d’enum et d’interface](#apis-organized-into-capabilities) au SDK TeamsJS v2 Preview
> * `TODO` rappels de commentaires pour passer en revue les zones qui peuvent être touchées par les modifications [de l’interface](#updates-to-the-context-interface) context
> * `TODO` commenter les rappels pour s’assurer que la conversion en fonctions [de promesses](#callbacks-converted-to-promises) à partir de fonctions de style de rappel s’est bien passé sur chaque site d’appel trouvé par l’outil

> [!IMPORTANT]
> Le code à l’intérieur de fichiers html n’est pas pris en charge par les outils de mise à niveau et nécessite des modifications manuelles.

## <a name="callbacks-converted-to-promises"></a>Rappels convertis en promesses

Teams API qui ont précédemment pris un paramètre de rappel ont été mises à jour pour renvoyer un objet De [promesse](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) JavaScript. Il s’agit des API suivantes :

```js
app.getContext, app.initialize, appInstallDialog.openAppInstallDialog, authentication.authenticate, authentication.getAuthToken, authentication.getUser, authentication.registerAuthenticationHandlers was removed to support using Promises, calendar.openCalendarItem, calendar.composeMeeting, call.startCall, core.executeDeepLink, location.getLocation, location.showLocation, mail.openMailItem, mail.composeMail, media.captureImage, media.getMedia, media.selectMedia, media.viewImages, media.scanBarCode, meeting.getAppContentStageSharingCapabilities, meeting.getAuthenticationTokenForAnonymousUser, meeting.getIncomingClientAudioState, meeting.getLiveStreamState, meeting.getMeetingDetails, meeting.requestStartLiveStreaming, meeting.requestStopLiveStreaming, meeting.shareAppContentToStage, meeting.stopSharingAppContentToStage, meeting.toggleIncomingClientAudio, meeting.getAppContentStageSharingState, pages.backStack.navigateBack, pages.navigateCrossDomain, pages.navigateToTab, pages.tabs.getMruTabInstances, pages.tabs.getTabInstances, pages.config.setConfig, pages.config.getConfig, people.selectPeople, ChildAppWindow.postMessage, ParentAppWindow.postMessage
```

Vous devez mettre à jour la façon dont votre code appelle l’une de ces API pour utiliser les promesses. Par exemple, si votre code appelle une API Teams comme celle-ci :

# <a name="javascript"></a>[JavaScript](#tab/javascript)

Ce code :

```js
import microsoftTeams from "@microsoft/teams-js";

microsoftTeams.getContext((context) => { /* ... */ });
```

Doit être mis à jour comme indiqué dans :

```js
import { app, Context } from "@microsoft/teams-js";

app.getContext().then((context) => {
    /*...*/
});
```

... ou le modèle `async/await` équivalent :

```js
import { app, Context } from "@microsoft/teams-js";

async function example() {
  const context = await app.getContext();
  /*...*/
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

Ce code :

```TypeScript
import * as microsoftTeams from "@microsoft/teams-js";

microsoftTeams.getContext((context: microsoftTeams.Context) => {
  /* ... */
});
```

Doit être mis à jour comme indiqué dans :

```TypeScript
import { app, Context } from "@microsoft/teams-js";

app.getContext().then((context: Context) => {
    /*...*/
});
```

... ou le modèle `async/await` équivalent :

```TypeScript
import { app, Context } from "@microsoft/teams-js";

async function example() {
  const context: Context = await app.getContext();
  /*...*/
}
```

---

> [!TIP]
> Lorsque vous mettez à jour votre code pour l’aperçu du SDK TeamsJS v2 à l’aide de [Teams Shared Computer Toolkit,](#updating-to-the-teams-client-sdk-v2-preview)les mises à jour requises sont signalées pour vous avec des commentaires dans votre `TODO` code client.

## <a name="apis-organized-into-capabilities"></a>API organisées en fonctionnalités

Une *fonctionnalité* est un regroupement logique d’API qui fournissent des fonctionnalités similaires. Vous pouvez penser Microsoft Teams, Outlook et Office, en tant qu’hôtes. Un hôte prend en charge une fonctionnalité donnée s’il prend en charge toutes les API définies dans cette fonctionnalité. Un hôte ne peut pas implémenter partiellement une fonctionnalité.  Les fonctionnalités peuvent être basées sur des fonctionnalités ou du contenu, telles que la *boîte de dialogue ou* l’authentification.  Il existe également des fonctionnalités pour les types d’applications, telles que *les onglets/pages* ou *les bots,* et d’autres regroupements.

Dans le SDK TeamsJS v2 Preview, les API sont définies en tant que fonctions dans un espace de noms JavaScript dont le nom correspond à la fonctionnalité requise. Si une application est en cours d’exécution dans un hôte qui prend en charge la fonctionnalité de boîte de dialogue, l’application peut appeler en toute sécurité des API telles que (en plus d’autres API liées à la boîte de dialogue définies dans l’espace de `dialog.open` noms). En attendant, si une application tente d’appeler une API qui n’est pas prise en charge dans cet hôte, l’API va lancer une exception.

### <a name="differentiate-your-app-experience"></a>Différencier l’expérience de votre application

Vous pouvez vérifier la prise en charge par l’hôte d’une fonctionnalité donnée au moment de l’utilisation en appelant la `isSupported()` fonction sur cette fonctionnalité (espace de noms). Elle sera de retour si elle est prise en charge et si ce n’est pas le cas, et vous pouvez ajuster le comportement de `true` `false` l’application selon le cas. Cela permet à votre application d’allumer l’interface utilisateur et les fonctionnalités dans les hôtes qui la prisent en charge, tout en continuant à s’exécuter pour les hôtes qui ne le sont pas.

Le nom de l’hôte dans lequel votre application s’exécute est exposé en tant que propriété *hostName* sur l’interface de contexte ( ), qui peut être interrogé lors de l’exécution en appelant `app.Context.app.host.name` `getContext` . Il est également disponible en tant que valeur `{hostName}` [d’espace réservé d’URL.](../tabs/how-to/access-teams-context.md#get-context-by-inserting-url-placeholder-values) La meilleure pratique consiste à utiliser le *mécanisme hostName* avec parcimonie :

* **Ne supposez pas** que certaines fonctionnalités sont ou ne sont pas disponibles dans un hôte en fonction de la valeur de la propriété *hostName.* Au lieu de cela, vérifiez la prise en charge des fonctionnalités ( `isSupported` ).
* **N’utilisez pas** *hostName pour* appeler les API. Au lieu de cela, vérifiez la prise en charge des fonctionnalités ( `isSupported` ).
* **Utilisez** *hostName pour* différencier le thème de votre application en fonction de l’hôte dans qui il s’exécute. Par exemple, vous pouvez utiliser Microsoft Teams violet comme couleur d’accentuant principale lors de l’exécution en Teams, et Outlook bleu lors de l’exécution en Outlook.
* **Utilisez** *hostName pour* différencier les messages affichés à l’utilisateur en fonction de l’hôte dans lequel il s’exécute. Par exemple, affichez Gérer vos tâches dans *Office* lors de  l’exécution dans Office sur le Web et Gérer vos tâches dans Teams lors de l’exécution dans Microsoft Teams.

### <a name="namespaces"></a>Espaces de noms

L’aperçu du SDK TeamsJS v2 organise les API en fonctionnalités *par* le moyen d’espaces de noms. Plusieurs nouveaux espaces de noms d’importance particulière sont *application,* *pages,* boîte de *dialogue* et *teamsCore*.

#### <a name="app-namespace"></a>*espace de* noms d’application

L’espace de noms contient les API de niveau supérieur requises pour l’utilisation globale de l’application, `app` Microsoft Teams, Office et Outlook. Toutes les API de différents autres espaces de noms TeamsJS ont été déplacées vers l’espace de noms dans `app` teamsJS SDK v2 Preview :

| Espace de noms d’origine `global (window)` | Nouvel espace de noms `app` |
| - | - |
| `initialize` | `app.initialize` |
| `getContext` | `app.getContext` |
| `registerOnThemeChangeHandler` | `app.registerOnThemeChangeHandler` |

| Espace de noms d’origine `appInitialization` | Nouvel espace de noms `app` |
| - | - |
| `appInitialization.notifyAppLoaded` | `app.notifyAppLoaded` |
| `appInitialization.notifySuccess` | `app.notifySuccess` |
| `appInitialization.notifyFailure` | `app.notifyFailure` |
| `appInitialization.notifyExpectedFailure` | `app.notifyExpectedFailure` |
| `appInitialization.FailedReason` enum | `app.FailedReason` |
| `appInitialization.ExpectedFailureReason` enum | `app.ExpectedFailureReason` |
| `appInitialization.IFailedRequest` enum | `app.IFailedRequest` |
| `appInitialization.IExpectedFailureRequest` enum | `app.IExpectedFailureRequest` |

#### <a name="core-namespace"></a>*espace de* noms principal

`core`L’espace de noms inclut des fonctionnalités pour les liens profonds.

| Espace de noms d’origine `publicAPIs` | Nouvel espace de noms `core` |
| - | - |
| `shareDeepLink` | `core.shareDeepLink` |
| `executeDeepLink` | `core.executeDeepLink` |

#### <a name="pages-namespace"></a>*espace* de noms pages

L’espace de noms inclut des fonctionnalités pour l’exécution et la navigation de pages web au sein de différents clients Microsoft 365, notamment Teams, Office et `pages` Outlook. Il inclut également plusieurs sous-fonctionnalités, implémentées en tant que sous-espaces de noms.

| Espace de noms d’origine `global (window)` | Nouvel espace de noms `pages` |
| - | - |
| `setFrameContext` | `pages.setCurrentFrame` (renommé) |
| `initializeWithFrameContext` | `pages.initializeWithFrameContext` |
| `registerFullScreenHandler` | `pages.registerFullScreenHandler` |
| `navigateCrossDomain` | `pages.navigateCrossDomain` |
| `returnFocus` | `pages.returnFocus` |

##### <a name="pagestabs"></a>*pages.tabs*

| Espace de noms d’origine `global (window)` | Nouvel espace de noms `pages.tabs` |
| - | - |
| `getTabInstances` |  `pages.tabs.getTabInstances` |
| `getMruTabInstances` | `pages.tabs.getMruTabInstances` |
| ` navigateToTab` | `pages.tabs.navigateToTab` |

| Espace de noms d’origine `navigation` | Nouvel espace de noms `pages.tabs` |
| - | - |
| `navigation.navigateToTab` | `pages.tabs.navigateToTab` |

##### <a name="pagesconfig"></a>*pages.config*

| Espace de noms d’origine `settings` | Nouvel espace de noms `pages.config`  |
| - | - |
| `settings.setSettings` | `pages.config.setConfig` (renommé)
| `settings.getSettings` | `pages.config.getConfig` (renommé)
| `settings.setValidityState`| `pages.config.setValidityState`
| `settings.initialize` | `pages.config.initialize`
| `settings.registerOnSaveHandler`| `pages.config.registerOnSaveHandler`
| `settings.registerOnRemoveHandler` | `pages.config.registerOnRemoveHandler`
| `settings.Settings` interface | `pages.config.Config` (renommé)
| `settings.SaveEvent` interface | `pages.config.SaveEvent` (renommé)
| `settings.RemoveEvent` interface | `pages.config.RemoveEvent` (renommé)
| `settings.SaveParameters` interface | `pages.config.SaveParameters` (renommé)
| `settings.SaveEventImpl` interface | `pages.config.SaveEventImpl` (renommé)

| Espace de noms d’origine `global (window)` | Nouvel espace de noms `pages.config` |
| - | - |
| `registerEnterSettingsHandler` | `pages.config.registerChangeConfigHandler` (renommé)

##### <a name="pagesbackstack"></a>*pages.backStack*

| Espace de noms d’origine `navigation` | Nouvel espace de noms `pages.backStack`  |
| - | - |
| `navigation.navigateBack` | `pages.backStack.navigateBack`

| Espace de noms d’origine `global (window)` | Nouvel espace de noms `pages.backStack`  |
| - | - |
| `registerBackButtonHandler` | `pages.backStack.registerBackButtonHandler`

##### <a name="pagesappbutton"></a>*pages.appButton*

| Espace de noms d’origine `global (window)` | Nouvel espace de noms `pages.appButton`  |
| - | - |
| `registerAppButtonClickHandler` | `pages.appButton.onClick` (renommé)
| `registerAppButtonHoverEnterHandler` | `pages.appButton.onHoverEnter` (renommé)
| `registerAppButtonHoverLeaveEnter` | `pages.appButton.onHoverLeave` (renommé)
| `FrameContext` interface | `pages.appButton.FrameInfo` (renommé)) |

#### <a name="dialog-namespace"></a>*espace* de noms de boîte de dialogue

L’espace de noms *des* tâches TeamsJS a été renommé en boîte de dialogue *et* les API suivantes ont été renommées :

| Espace de noms d’origine `tasks` | Nouvel espace de noms `dialog`  |
| - | - |
| `tasks.startTask` | `dialog.open` (renommé) |
| `tasks.submitTasks` | `dialog.submit` (renommé) |
| `tasks.updateTasks` | `dialog.resize` (renommé) |
| `tasks.TaskModuleDimension` enum | `dialog.DialogDimension` (renommé) |
| `tasks.TaskInfo` interface | `dialog.DialogInfo` (renommé) |

#### <a name="teamscore-namespace"></a>*espace de noms teamsCore*

Pour généraliser le SDK TeamsJS afin d’exécuter d’autres hôtes Microsoft 365 tels que Office et Outlook, les fonctionnalités propres à Teams (à l’origine dans l’espace de noms *global)* ont été déplacées vers un espace de noms *teamsCore* :

| Espace de noms d’origine `global (window)` | Nouvel espace de noms `teamsCore`  |
| - | - |
| `enablePrintCapability` | `teamsCore.enablePrintCapability`
| `print` | `teamsCore.print`
| `registerOnLoadHandler` | `teamsCore.registerOnLoadHandler`
| `registerBeforeUnloadHandler` | `teamsCore.registerBeforeUnloadHandler`
| `registerFocusEnterHandler` | `teamsCore.registerFocusEnterHandler`

### <a name="updates-to-the-context-interface"></a>Mises à jour de l’interface *de* contexte

L’interface a été déplacée vers l’espace de noms et mise à jour pour grouper des propriétés similaires pour une meilleure évolutivité, car elle s’exécute dans Outlook et Office, en plus des `Context` `app` Teams.

Une nouvelle propriété a été ajoutée pour permettre aux onglets personnels de différencier l’expérience utilisateur `app.Context.app.host.name` en fonction de l’application hôte.

Vous pouvez également visualiser les modifications en révisant la fonction dans la source d’aperçu du  [`transformLegacyContextToAppContext`](https://github.com/OfficeDev/microsoft-teams-library-js/blob/2.0-preview/packages/teams-js/src/public/app.ts) SDK TeamsJS v2.

| Nom d’origine dans `Context` l’interface | Nouvel emplacement dans `app.Context` |
| - | - |
| `appIconPosition` | `app.Context.app.iconPositionVertical` |
| `appLaunchId`| *N’EST PAS TEAMS version préliminaire du SDK client v2* |
| `appSessionId` | `app.Context.app.sessionId`|
| `channelId`| `app.Context.channel.id` |
| `channelName`| `app.Context.channel.displayName`|
| `channelRelativeUrl` | `app.Context.channel.relativeUrl`|
| `channelType`| `app.Context.channel.membershipType` |
| `chatId` | `app.Context.chat.id`|
| `defaultOneNoteSectionId`| `app.Context.channel.defaultOneNoteSectionId`|
| `entityId` | `app.Context.page.id`|
| `frameContext` | `app.Context.page.frameContext`|
| `groupId`| `app.Context.team.groupId` |
| `hostClientType` | `app.Context.app.host.clientType`|
| `hostTeamGroupId`| `app.Context.channel.ownerGroupId` |
| `hostTeamTenantId` | `app.Context.channel.ownerTenantId`|
| `isCallingAllowed` | `app.Context.user.isCallingAllowed`|
| `isFullScreen` | `app.Context.page.isFullScreen`|
| `isMultiWindow`| `app.Context.page.isMultiWindow` |
| `isPSTNCallingAllowed` | `app.Context.user.isPSTNCallingAllowed`|
| `isTeamArchived` | `app.Context.team.isArchived`|
| `locale` | `app.Context.app.locale` |
| `loginHint`| `app.Context.user.loginHint` |
| `meetingId`| `app.Context.meeting.id` |
| `osLocaleInfo` | `app.Context.app.osLocaleInfo` |
| `parentMessageId`| `app.Context.app.parentMessageId`|
| `ringId` | `app.Context.app.host.ringId`|
| `sessionId`| `app.Context.app.host.sessionId` |
| `sourceOrigin` | `app.Context.page.sourceOrigin`|
| `subEntityId`| `app.Context.page.subPageId` |
| `teamId` | `app.Context.team.internalId`|
| `teamSiteDomain` | `app.Context.sharepointSite.domain`|
| `teamSitePath` | `app.Context.sharepointSite.path`|
| `teamSiteUrl`| `app.Context.sharepointSite.url` |
| `teamTemplateId` | `app.Context.team.templateId`|
| `teamType` | `app.Context.team.type`|
| `tenantSKU`| `app.Context.user.tenant.teamsSku` |
| `tid`| `app.Context.user.tenant.id` |
| `upn` | `app.Context.user.userPrincipalName` |
|` userClickTime`| `app.Context.app.userClickTime`|
| `userFileOpenPreference` | `app.Context.app.userFileOpenPreference` |
| `userLicenseType`| `app.Context.user.licenseType` |
| `userObjectId` | `app.Context.user.id`|
| ` userTeamRole` | `app.Context.team.userRole`|
| `userDisplayName` | `app.Context.user.displayName` |
| N/A | `app.Context.app.host.name`|

## <a name="next-steps"></a>Prochaines étapes

Vous pouvez également en savoir plus sur les modifications importantes dans lelog des modifications du [SDK TeamsJS v2 Preview](https://github.com/OfficeDev/microsoft-teams-library-js/blob/2.0-preview/CHANGELOG.md) et dans la référence de [l’API du SDK TeamsJS v2 Preview.](/javascript/api/overview/msteams-client?view=msteams-client-js-beta&preserve-view=true)

Lorsque vous êtes prêt à tester vos applications Teams en cours d’exécution Outlook et Office, voir :

> [!div class="nextstepaction"]
> [Étendre votre application Teams sur plusieurs Microsoft 365](overview.md)
