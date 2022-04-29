---
title: Version préliminaire du Kit de développement logiciel (SDK) client JavaScript Microsoft Teams v2
description: Comprendre les modifications à venir avec le Kit de développement logiciel (SDK) client JavaScript Microsoft Teams v2 (préversion)
ms.date: 11/15/2021
ms.topic: conceptual
ms.custom: m365apps
ms.localizationpriority: high
ms.openlocfilehash: 91f012821efacd0f0ff6032703d0520d5bd469e0
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111695"
---
# <a name="microsoft-teams-javascript-client-sdk-v2-preview"></a>Version préliminaire du Kit de développement logiciel (SDK) client JavaScript Microsoft Teams v2

Avec le [SDK client JavaScript Microsoft Teams v2 Preview](/javascript/api/overview/msteams-client?view=msteams-client-js-beta&preserve-view=true), le SDK Teams existant (`@microsoft/teams-js`, ou simplement `TeamsJS`) a été refactorisé pour permettre aux développeurs Teams d’[étendre les applications Teams à s’exécuter dans Outlook et Office](overview.md). Du point de vue fonctionnel, la préversion du Kit de développement logiciel (SDK) TeamsJS v2 (`@microsoft/teams-js@next`) est un sur-ensemble du Kit de développement logiciel (SDK) TeamsJS actuel. Elle prend en charge les fonctionnalités d’application Teams existantes tout en ajoutant la possibilité d’héberger des applications Teams dans Outlook et Office.

Il existe deux modifications importantes dans la préversion du Kit de développement logiciel (SDK) TeamsJS v2 dont votre code devra tenir compte pour s’exécuter dans d’autres applications Microsoft 365 :

* [**Les fonctions de rappel retournent désormais des objets Promise.**](#callbacks-converted-to-promises) Toutes les fonctions existantes avec un paramètre de rappel ont été modernisées pour retourner un objet [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) JavaScript pour améliorer la gestion des opérations asynchrones et la lisibilité du code.

* [**Les API sont désormais organisées en *fonctionnalités*.**](#apis-organized-into-capabilities) Vous pouvez considérer les fonctionnalités comme des regroupements logiques d’API qui fournissent des fonctionnalités similaires, telles que `authentication`, `calendar`, `mail`, `monetization`, `meeting`et `sharing`.

 Vous pouvez utiliser l’extension[Teams Toolkit](https://aka.ms/teams-toolkit) pour Microsoft Visual Studio Code afin de simplifier le processus de mise à jour de votre application Teams, comme décrit dans la section suivante.

> [!NOTE]
> L’activation d’une application Teams existante pour s’exécuter dans Outlook et Office nécessite les deux éléments suivants :
>
> 1. Dépendance sur le `@microsoft/teams-js@2.0.0-beta.1` ou version ultérieure, et
> 2. Modification du code d’application existant en fonction des modifications requises décrites dans ce document.
>
> Si vous référencez `@microsoft/teams-js@2.0.0-beta.1` (ou version ultérieure) à partir d’une application Teams existante, vous verrez des avertissements de dépréciation si votre code appelle des API qui ont changé. Une couche de traduction d’API (mappage du Kit de développement logiciel (SDK) actuel aux appels d’API du Kit de développement logiciel (SDK) en préversion) est fournie pour permettre aux applications Teams existantes de continuer à travailler dans Teams jusqu’à ce qu’elles soient en mesure de mettre à jour le code pour fonctionner avec le Kit de développement logiciel (SDK) TeamsJS v2 Preview. Une fois que vous avez mis à jour votre code avec les modifications décrites dans cet article, votre onglet personnel s’exécute également dans Outlook et Office.

## <a name="updating-to-the-teams-client-sdk-v2-preview"></a>Mise à jour vers le Kit de développement logiciel (SDK) client Teams v2 (préversion)

Le moyen le plus simple de mettre à jour votre application Teams pour utiliser le SDK TeamsJS v2 Preview consiste à utiliser l’extension [Teams Toolkit](https://aka.ms/teams-toolkit) pour Visual Studio Code. Cette section vous guide tout au long des étapes à suivre. Si vous préférez mettre à jour manuellement votre code, consultez les sections[rappels convertis en promesses](#callbacks-converted-to-promises) et [API organisées en fonctionnalités](#apis-organized-into-capabilities) pour plus d’informations sur les modifications d’API requises.

### <a name="1-install-the-latest-teams-toolkit-visual-studio-code-extension"></a>1. Installer la dernière extension Visual Studio Code du Kit de ressources Teams

Dans la *Place de marché des extensions Visual Studio Code*, recherchez **Teams Toolkit** et installez la version `2.10.0` ou une version ultérieure. Le kit de ressources fournit deux commandes pour faciliter le processus :

1. Commande pour mettre à jour votre schéma de manifeste
1. Commande permettant de mettre à jour les références de votre SDK et d’appeler des sites

Voici les deux mises à jour clés dont vous aurez besoin pour exécuter une application d’onglet personnel Teams dans d’autres applications Microsoft 365 : ``

### <a name="2-updating-the-manifest"></a>2. Mise à jour du manifeste

# <a name="teams-toolkit"></a>[Toolkit Teams](#tab/manifest-teams-toolkit)

1. Ouvrez la *Palette de commandes* : `Ctrl+Shift+P`
1. Exécutez la commande **Teams : mettez à niveau le manifeste Teams pour prendre en charge les applications Outlook et Office** et sélectionnez votre fichier manifeste d’application. Des modifications seront apportées.

# <a name="manual-steps"></a>[Étapes manuelles](#tab/manifest-manual)

Ouvrez le manifeste de votre application Teams et mettez à jour les `$schema` et `manifestVersion` valeurs suivantes :

```json
{
    "$schema" : "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
    "manifestVersion" : "m365DevPreview"
}
```

---

Si vous avez utilisé Teams Toolkit pour créer votre application personnelle, vous pouvez également l'utiliser pour valider les modifications apportées à votre fichier manifeste et identifier les éventuelles erreurs. Ouvrez la palette de commandes `Ctrl+Shift+P`et recherchez **Teams : Valider le fichier manifeste** ou sélectionnez l’option dans le menu Déploiement du Teams Toolkit (recherchez l’icône Teams sur le côté gauche de Visual Studio Code).

:::image type="content" source="images/toolkit-validate-manifest-file.png" alt-text="Option « Valider le fichier manifeste » du Kit de ressources Teams sous le menu « Déploiement »":::

### <a name="2-update-sdk-references"></a>2. Mettre à jour les références du Kit de développement logiciel (SDK)

Pour s’exécuter dans Outlook et Office, votre application doit dépendre du [package npm](https://www.npmjs.com/package/@microsoft/teams-js/v/2.0.0-beta.1)`@microsoft/teams-js@2.0.0-beta.1` (ou d’une version *bêta* ultérieure). Pour effectuer ces étapes manuellement et pour plus d’informations sur les modifications apportées à l’API, consultez les sections suivantes sur les rappels [convertis en promesses](#callbacks-converted-to-promises) et [API organisées en fonctionnalités](#apis-organized-into-capabilities).

1. Vérifiez que vous avez [Teams Toolkit](https://aka.ms/teams-toolkit) `v2.10.0` ou une version ultérieure
1. Ouvrez la *Palette de commandes* : `Ctrl+Shift+P`
1. Exécutez la commande `Teams: Upgrade Teams JS SDK references to support Outlook and Office apps`

Une fois l’opération terminée, l’utilitaire aura mis à jour votre fichier `package.json` avec la dépendance du Kit de développement logiciel (SDK) TeamsJS v2 (`@microsoft/teams-js@2.0.0-beta.1` ou version ultérieure), et vos fichiers `*.js/.ts` et `*.jsx/.tsx` seront mis à jour avec :

> [!div class="checklist"]
>
> * `package.json` Références au Kit de développement logiciel (SDK) TeamsJS v2 (préversion)
> * Importer des instructions pour le Kit de développement logiciel (SDK) TeamsJS v2 (préversion)
> * [Appels de fonction, d’énumération et d’interface](#apis-organized-into-capabilities) au Kit de développement logiciel (SDK) TeamsJS v2 (préversion)
> * `TODO`rappels de commentaires pour passer en revue les zones susceptibles d’être affectées par les modifications apportées à l’interface [de contexte](#updates-to-the-context-interface)
> * `TODO` rappels de commentaire pour garantir que la [conversion en fonctions promises à partir de fonctions de style de rappel](#callbacks-converted-to-promises) s’est bien passée à chaque site d’appel que l’outil a trouvé.

> [!IMPORTANT]
> Le code contenu dans les fichiers HTML n’est pas pris en charge par les outils de mise à niveau et nécessite des modifications manuelles.

## <a name="callbacks-converted-to-promises"></a>Rappels convertis en promesses

Les API Teams qui ont précédemment pris un paramètre de rappel ont été mises à jour pour retourner un objet [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) JavaScript. Il s’agit notamment des API suivantes :

```js
app.getContext, app.initialize, appInstallDialog.openAppInstallDialog, authentication.authenticate, authentication.getAuthToken, authentication.getUser, authentication.registerAuthenticationHandlers was removed to support using Promises, calendar.openCalendarItem, calendar.composeMeeting, call.startCall, core.executeDeepLink, location.getLocation, location.showLocation, mail.openMailItem, mail.composeMail, media.captureImage, media.getMedia, media.selectMedia, media.viewImages, media.scanBarCode, meeting.getAppContentStageSharingCapabilities, meeting.getAuthenticationTokenForAnonymousUser, meeting.getIncomingClientAudioState, meeting.getLiveStreamState, meeting.getMeetingDetails, meeting.requestStartLiveStreaming, meeting.requestStopLiveStreaming, meeting.shareAppContentToStage, meeting.stopSharingAppContentToStage, meeting.toggleIncomingClientAudio, meeting.getAppContentStageSharingState, pages.backStack.navigateBack, pages.navigateCrossDomain, pages.navigateToTab, pages.tabs.getMruTabInstances, pages.tabs.getTabInstances, pages.config.setConfig, pages.config.getConfig, people.selectPeople, ChildAppWindow.postMessage, ParentAppWindow.postMessage
```

Vous devez mettre à jour la façon dont votre code appelle l’une de ces API pour utiliser Promises. Par exemple, si votre code appelle une API Teams comme suit :

# <a name="javascript"></a>[JavaScript](#tab/javascript)

Ce code :

```js
import microsoftTeams from "@microsoft/teams-js";

microsoftTeams.getContext((context) => { /* ... */ });
```

Doit être mis à jour pour :

```js
import { app, Context } from "@microsoft/teams-js";

app.getContext().then((context) => {
    /*...*/
});
```

... ou le modèle équivalent `async/await` :

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

Doit être mis à jour pour :

```TypeScript
import { app, Context } from "@microsoft/teams-js";

app.getContext().then((context: Context) => {
    /*...*/
});
```

... ou le modèle équivalent `async/await` :

```TypeScript
import { app, Context } from "@microsoft/teams-js";

async function example() {
  const context: Context = await app.getContext();
  /*...*/
}
```

---

> [!TIP]
> Lorsque vous mettez à jour votre code pour la préversion du Kit de développement logiciel (SDK) TeamsJS v2 à l’aide du [Kit de ressources Teams](#updating-to-the-teams-client-sdk-v2-preview), les mises à jour requises sont signalées pour vous avec `TODO` commentaires dans votre code client.

## <a name="apis-organized-into-capabilities"></a>API organisées en fonctionnalités

Une *fonctionnalité* est un regroupement logique d’API qui fournissent des fonctionnalités similaires. Vous pouvez considérer Microsoft Teams, Outlook et Office comme des hôtes. Un hôte prend en charge une fonctionnalité donnée s’il prend en charge toutes les API définies dans cette fonctionnalité. Un hôte ne peut pas implémenter partiellement une fonctionnalité.  Les fonctionnalités peuvent être basées sur des fonctionnalités ou du contenu, telles que *dialogue* ou *authentification*. Il existe également des fonctionnalités pour les types d’application, telles que *onglets/pages* ou *bots* et d’autres regroupements.

Dans la préversion du Kit de développement logiciel (SDK) TeamsJS v2, les API sont définies comme des fonctions dans un espace de noms JavaScript dont le nom correspond à la fonctionnalité requise. Si une application s’exécute dans un hôte qui prend en charge la fonctionnalité de boîte de dialogue, l’application peut appeler en toute sécurité des API telles que `dialog.open` (en plus d’autres API liées au dialogue définies dans l’espace de noms). En attendant, si une application tente d’appeler une API qui n’est pas prise en charge dans cet hôte, l’API lève une exception.

### <a name="differentiate-your-app-experience"></a>Différencier votre expérience d’application

Vous pouvez vérifier la prise en charge par l’hôte d’une fonctionnalité donnée au moment de l’exécution en appelant la fonction`isSupported()` sur cette fonctionnalité (espace de noms). Elle retourne `true` si elle est prise en charge et `false` si ce n’est pas le cas, et vous pouvez ajuster le comportement de l’application en fonction des besoins. Cela permet à votre application d’activer l’interface utilisateur et les fonctionnalités des hôtes qui la prennent en charge, tout en continuant à s’exécuter pour les ordinateurs hôtes qui ne le prennent pas en charge.

Le nom de l’hôte dans lequel votre application s’exécute est exposé en tant que propriété *hostName* sur l’interface de contexte (`app.Context.app.host.name`), qui peut être interrogée au moment de l’exécution en appelant `getContext`. Il est également disponible en tant que `{hostName}`[valeur d’espace réservé d’URL](../tabs/how-to/access-teams-context.md#get-context-by-inserting-url-placeholder-values). Il est recommandé d’utiliser le mécanisme *hostName* avec parcimonie :

* **Ne partez pas** du principe que certaines fonctionnalités sont ou ne sont pas disponibles dans un hôte en fonction de la valeur de la propriété *hostName* . Au lieu de cela, recherchez la prise en charge des fonctionnalités (`isSupported`).
* **N’utilisez** pas *hostName* pour contrôler les appels d’API. Au lieu de cela, recherchez la prise en charge des fonctionnalités (`isSupported`).
* **Utilisez** *hostName* pour différencier le thème de votre application en fonction de l’hôte dans lequel elle s’exécute. Par exemple, vous pouvez utiliser Microsoft Teams violet comme couleur d’accentuation principale lors de l’exécution dans Teams, et Outlook bleu lors de l’exécution dans Outlook.
* **Utilisez** *hostName* pour différencier les messages affichés à l’utilisateur en fonction de l’hôte dans lequel il s’exécute. Par exemple, affichez *Gérer vos tâches dans Office* lors de l’exécution dans Office sur le web, et *Gérer vos tâches dans Teams* lors de l’exécution dans Microsoft Teams.

### <a name="namespaces"></a>Espaces de noms

La préversion du Kit de développement logiciel (SDK) TeamsJS v2 organise les API en *fonctionnalités* par le biais d’espaces de noms. Plusieurs nouveaux espaces de noms d’une importance particulière sont *l’application*, *les pages*, la *boîte de dialogue* et *teamsCore*.

#### <a name="app-namespace"></a>Espace de noms *d’application*

L’espace de noms`app` contient les API de niveau supérieur requises pour l’utilisation globale des applications, sur Microsoft Teams, Office et Outlook. Toutes les API de différents autres espaces de noms TeamsJS ont été déplacées vers l’espace de noms `app` dans la préversion du Kit de développement logiciel (SDK) TeamsJS v2 :

| Espace de noms d’origine `global (window)` | Nouveaux types par espaces de noms`app` |
| - | - |
| `initialize` | `app.initialize` |
| `getContext` | `app.getContext` |
| `registerOnThemeChangeHandler` | `app.registerOnThemeChangeHandler` |

| Espace de noms d’origine `appInitialization` | Nouveaux types par espaces de noms`app` |
| - | - |
| `appInitialization.notifyAppLoaded` | `app.notifyAppLoaded` |
| `appInitialization.notifySuccess` | `app.notifySuccess` |
| `appInitialization.notifyFailure` | `app.notifyFailure` |
| `appInitialization.notifyExpectedFailure` | `app.notifyExpectedFailure` |
| `appInitialization.FailedReason` enum | `app.FailedReason` |
| `appInitialization.ExpectedFailureReason` enum | `app.ExpectedFailureReason` |
| `appInitialization.IFailedRequest` enum | `app.IFailedRequest` |
| `appInitialization.IExpectedFailureRequest` enum | `app.IExpectedFailureRequest` |

#### <a name="core-namespace"></a>espace de noms *principal*

L’espace de noms `core` inclut des fonctionnalités pour les liens profonds.

| Espace de noms d’origine `publicAPIs` | Nouvel espace de noms `core` |
| - | - |
| `shareDeepLink` | `core.shareDeepLink` |
| `executeDeepLink` | `core.executeDeepLink` |

#### <a name="pages-namespace"></a>espace de noms *pages*

L’espace de noms `pages` inclut des fonctionnalités permettant d’exécuter et de parcourir des pages web au sein de différents clients Microsoft 365, notamment Teams, Office et Outlook. Il inclut également plusieurs sous-fonctionnalités, implémentées en tant que sous-espaces de noms.

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
| `navigateToTab` | `pages.tabs.navigateToTab` |

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
| interface de `settings.Settings` | `pages.config.Config` (renommé)
| interface de `settings.SaveEvent` | `pages.config.SaveEvent` (renommé)
| interface de `settings.RemoveEvent` | `pages.config.RemoveEvent` (renommé)
| interface de `settings.SaveParameters` | `pages.config.SaveParameters` (renommé)
| interface de `settings.SaveEventImpl` | `pages.config.SaveEventImpl` (renommé)

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
| interface de `FrameContext` | `pages.appButton.FrameInfo` (renommé)) |

#### <a name="dialog-namespace"></a>espace de noms de *boîte de dialogue*

Les tâches *TeamsJS* espace de noms ont été renommées en *boîte de dialogue* et les API suivantes ont été renommées :

| Espace de noms d’origine `tasks` | Nouvel espace de noms `dialog`  |
| - | - |
| `tasks.startTask` | `dialog.open` (renommé) |
| `tasks.submitTasks` | `dialog.submit` (renommé) |
| `tasks.updateTasks` | `dialog.resize` (renommé) |
| `tasks.TaskModuleDimension` enum | `dialog.DialogDimension` (renommé) |
| interface de `tasks.TaskInfo` | `dialog.DialogInfo` (renommé) |

#### <a name="teamscore-namespace"></a>espace de noms *teamsCore*

Pour généraliser le Kit de développement logiciel (SDK) TeamsJS afin d’exécuter d’autres hôtes Microsoft 365 tels qu’Office et Outlook, les fonctionnalités spécifiques à Teams (à l’origine dans l’espace de noms *global*) ont été déplacées vers un espace de noms *teamsCore* :

| Espace de noms d’origine `global (window)` | Nouvel espace de noms `teamsCore`  |
| - | - |
| `enablePrintCapability` | `teamsCore.enablePrintCapability`
| `print` | `teamsCore.print`
| `registerOnLoadHandler` | `teamsCore.registerOnLoadHandler`
| `registerBeforeUnloadHandler` | `teamsCore.registerBeforeUnloadHandler`
| `registerFocusEnterHandler` | `teamsCore.registerFocusEnterHandler`

### <a name="updates-to-the-context-interface"></a>Mises à jour de l’interface *contextuel*

L’interface `Context` a été déplacée vers l’espace de noms `app` et mise à jour pour regrouper des propriétés similaires pour une meilleure extensibilité lors de son exécution dans Outlook et Office, en plus de Teams.

Une nouvelle propriété `app.Context.app.host.name` a été ajoutée pour permettre aux onglets personnels de différencier l’expérience utilisateur en fonction de l’application hôte.

Vous pouvez également visualiser les modifications en examinant la fonction [`transformLegacyContextToAppContext`](https://github.com/OfficeDev/microsoft-teams-library-js/blob/2.0-preview/packages/teams-js/src/public/app.ts) dans la source de la préversion du Kit de développement logiciel (SDK) TeamsJS v2.

| Nom d’origine dans l’interface `Context` | Nouvel emplacement dans `app.Context` |
| - | - |
| `appIconPosition` | `app.Context.app.iconPositionVertical` |
| `appLaunchId`| *Préversion du Kit de développement logiciel (SDK) client NOT IN Teams v2* |
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
|`userClickTime`| `app.Context.app.userClickTime`|
| `userFileOpenPreference` | `app.Context.app.userFileOpenPreference` |
| `userLicenseType`| `app.Context.user.licenseType` |
| `userObjectId` | `app.Context.user.id`|
| `userTeamRole` | `app.Context.team.userRole`|
| `userDisplayName` | `app.Context.user.displayName` |
| S/O | `app.Context.app.host.name`|

## <a name="next-steps"></a>Étapes suivantes

Vous pouvez également en savoir plus sur les changements dans le journal des modifications du Kit de développement logiciel [(SDK) TeamsJS v2 (préversion](https://github.com/OfficeDev/microsoft-teams-library-js/blob/2.0-preview/packages/teams-js/CHANGELOG.md) ) et les [informations de référence sur l’API En préversion du Kit de développement logiciel (SDK) TeamsJS v2](/javascript/api/overview/msteams-client?view=msteams-client-js-beta&preserve-view=true).

Lorsque vous êtes prêt à tester vos applications Teams s’exécutant dans Outlook et Office, consultez :

> [!div class="nextstepaction"]
> [Développez votre application dans Microsoft 365](overview.md)
