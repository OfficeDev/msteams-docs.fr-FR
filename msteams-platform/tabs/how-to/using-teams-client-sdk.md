---
title: Création d’onglets et d’autres expériences hébergées avec le Kit de développement logiciel (SDK) client JavaScript Microsoft Teams
author: heath-hamilton
ms.author: surbhigupta
description: Vue d’ensemble du Kit de développement logiciel (SDK) client JavaScript Microsoft Teams, qui peut vous aider à créer des expériences d’application hébergées dans un <iframe> dans Teams, Office et Outlook.
ms.localizationpriority: high
keywords: onglets teams , canal de groupe configurable SDK statique JavaScript personnel m365
ms.topic: conceptual
ms.openlocfilehash: 2a1c827913759d49ba721251d4a6f5382d8eb3a4
ms.sourcegitcommit: 264d3cc84d6eec4ab025cf86a7a6f4865f1aed07
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/24/2022
ms.locfileid: "65653286"
---
# <a name="building-tabs-and-other-hosted-experiences-with-the-microsoft-teams-javascript-client-sdk"></a>Création d’onglets et d’autres expériences hébergées avec le Kit de développement logiciel (SDK) client JavaScript Microsoft Teams

Le Kit de développement logiciel (SDK) client JavaScript Microsoft Teams peut vous aider à créer des expériences hébergées dans Teams, Office et Outlook, où le contenu de votre application est hébergé dans un [iframe](https://developer.mozilla.org/docs/Web/HTML/Element/iframe). Le Kit de développement logiciel (SDK) est utile pour développer des applications avec les fonctionnalités Teams suivantes :

* [Onglets](../../tabs/what-are-tabs.md)
* [Boîtes de dialogue (modules de tâche)](../../task-modules-and-cards/what-are-task-modules.md)

À compter de la version `2.0.0`, le Kit de développement logiciel (SDK) client Teams existant (`@microsoft/teams-js`, ou simplement `TeamsJS`) a été refactorisé pour permettre [aux applications Teams de s’exécuter dans Outlook et Office](/m365-apps/overview.md), en plus de Microsoft Teams. Du point de vue fonctionnel, la dernière version de TeamsJS prend en charge toutes les fonctionnalités d’application Teams existantes (v.1.x.x), tout en ajoutant la possibilité facultative d’héberger des applications Teams dans Outlook et Office.

Voici les conseils de contrôle de version actuels pour différents scénarios d’application :

|                  |[Version de TeamsJS](/javascript/api/overview/msteams-client) | [Version du manifeste de l’application](../../resources/schema/manifest-schema.md)| Étapes suivantes|
|------------------|---------|--------|---|
|**Applications Teams étendues à Office/Outlook**| TeamsJS v.2.0 ou version ultérieure  | **1.13** ou version ultérieure | [Étendre une application Teams pour l’exécuter sur Microsoft 365](../../m365-apps/extend-m365-teams-personal-tab.md) ou [Créer une application Microsoft 365](../../m365-apps/extend-m365-teams-personal-tab.md#quickstart) |
|**Applications Teams uniquement existantes**| Mettre à jour vers TeamsJS v.2.0 si possible (v.1.12 est toujours pris en charge*)  | 1.12 | [Comprendre la compatibilité descendante de TeamsJS](#backwards-compatibility) et [Mise à jour vers TeamsJS v.2.0](#updating-to-the-teams-client-sdk-v200) |
|**Nouvelles applications Teams uniquement**| TeamsJS v.2.0 ou version ultérieure | 1.12 | [Créer une application Teams à l’aide du kit de ressources Teams](../../toolkit/create-new-project.md) |

**La meilleure pratique consiste à utiliser la dernière version de TeamsJS (v.2.0 ou ultérieure) dans la mesure du possible, afin de bénéficier des dernières améliorations et de la prise en charge des nouvelles fonctionnalités (même pour les applications Teams uniquement). TeamsJS v.1.12 continuera d’être pris en charge, mais aucune nouvelle fonctionnalité ou amélioration ne sera ajoutée.*

Le reste de cet article vous guide tout au long de la structure et des dernières mises à jour du Kit de développement logiciel (SDK) du client JavaScript Teams.

### <a name="microsoft-365-support-running-teams-apps-in-office-and-outlook"></a>prise en charge Microsoft 365 (exécution d’applications Teams dans Office et Outlook)

TeamsJS v.2.0 introduit la possibilité pour certains types d’applications Teams de s’exécuter dans l’écosystème Microsoft 365. Actuellement, d’autres hôtes d’applications Microsoft 365 (y compris Office et Outlook) pour les applications Teams prennent en charge un sous-ensemble des types d’applications et des fonctionnalités que vous pouvez créer pour la plateforme Teams. Cette prise en charge s’étendra au fil du temps. Pour obtenir un résumé de la prise en charge des hôtes pour les applications Teams, consultez [Étendre les applications Teams sur Microsoft 365](../../m365-apps/overview.md).

Le tableau suivant répertorie les onglets et boîtes de dialogue Teams (modules de tâches) fonctionnalités (espaces de noms publics) avec une prise en charge étendue pour s’exécuter dans d’autres hôtes Microsoft 365.

> [!TIP]
> Vérifiez la prise en charge par l’hôte d’une fonctionnalité donnée au moment de l’exécution en appelant la fonction `isSupported()` sur cette fonctionnalité (espace de noms).

|Fonctionnalité | Prise en charge de l’hôte | Remarques |
|-----------|--------------|-------|
| application | Teams, Outlook, Office | Espace de noms représentant l’initialisation et le cycle de vie des applications. |
| appInitialization| | Déconseillé. Remplacé par `app` un espace de noms. |
| appInstallDialog | Équipes||
| authentification | Teams, Outlook, Office | |
| calendrier | Teams, Outlook ||
| appeler | Équipes||
| conversation |Équipes||
| fenêtre de dialogue | Teams, Outlook, Office | Espace de noms représentant des dialogues (anciennement *nommés modules de tâches*. Consultez les notes sur [les boîtes de dialogue](#dialogs). |
| emplacement |Équipes| Consultez les notes sur [les autorisations d’application](#app-permissions).|
| messagerie | Outlook (bureau Windows uniquement)||
| média |Équipes| Consultez les notes sur [les autorisations d’application](#app-permissions).|
| pages | Teams, Outlook, Office | Espace de noms représentant la navigation de page. Consultez les notes sur la [liaison approfondie](#deep-linking). |
| contacts |Équipes||
| paramètres || Déconseillé. Remplacé par `pages.config`.|
| partage | Équipes||
| tasks | | Déconseillé. Remplacé par la fonctionnalité `dialog`. Consultez les notes sur [les boîtes de dialogue](#dialogs).|
| teamsCore | Équipes | Espace de noms contenant des fonctionnalités spécifiques à Teams.|
| video | Équipes||

#### <a name="app-permissions"></a>Autorisations d’application

Les fonctionnalités d’application qui exigent que l’utilisateur accorde [des autorisations d’appareil](../../concepts/device-capabilities/device-capabilities-overview.md) (telles que l’*emplacement*) ne sont pas encore prises en charge pour les applications s’exécutant en dehors de Teams. Il n’existe actuellement aucun moyen de vérifier les autorisations d’application dans Paramètres ou l’en-tête de votre application lors de l’exécution dans Outlook ou Office. Si une application Teams s’exécutant dans Office ou Outlook appelle une API TeamsJS (ou HTML5) qui déclenche des autorisations d’appareil, cette API génère une erreur et ne parvient pas à afficher une boîte de dialogue système demandant le consentement de l’utilisateur.

L’aide actuelle pour l’instant consiste à modifier votre code pour intercepter l’échec :

* Vérifiez [isSupported()](#differentiate-your-app-experience) sur une fonctionnalité avant de l’utiliser. `media`, `meeting`et `files` ne prennent pas encore en charge les appels *isSupported* et ne fonctionnent pas encore en dehors de Teams.
* Interceptez et gérez les erreurs lors de l’appel des API TeamsJS et HTML5.

Lorsqu’une API n’est pas prise en charge ou génère une erreur, ajoutez une logique pour échouer correctement ou fournissez une solution de contournement. Par exemple :

* Dirigez l’utilisateur vers le site web de votre application.
* Indiquez à l’utilisateur d’utiliser l’application dans Teams pour terminer le flux.
* Informez l’utilisateur que la fonctionnalité n’est pas encore disponible.

En outre, il est recommandé de s’assurer que le manifeste de votre application spécifie uniquement les autorisations d’appareil qu’il utilise.

#### <a name="deep-linking"></a>Liaisons profondes

Avant TeamsJS version 2.0, tous les scénarios de liaison approfondie étaient gérés à l’aide de `shareDeepLink` (pour générer un lien *vers* une partie spécifique de votre application) et `executeDeepLink` (pour accéder à un lien profond *à partir* de votre application ou *au sein* de celui-ci). TeamsJS v.2.0 introduit une nouvelle API, `navigateToApp`, pour accéder aux pages (et sous-pages) d’une application de manière cohérente entre les hôtes d’application (Office et Outlook, en plus de Teams). Voici les instructions mises à jour pour les scénarios de liaison approfondie :

##### <a name="deep-links-into-your-app"></a>Liens profonds dans votre application

Utilisez `pages.shareDeepLink` (appelé *shareDeepLink* avant TeamsJS v.2.0) pour générer et afficher un lien pouvant être copié que l’utilisateur doit partager. Lorsque vous cliquez dessus, un utilisateur est invité à installer l’application si elle n’est pas déjà installée pour l’hôte d’application (spécifié dans le chemin d’accès du lien).

##### <a name="navigation-within-your-app"></a>Navigation dans votre application

Utilisez la nouvelle API `pages.navigateToApp` pour naviguer dans votre application au sein de l’application d’hébergement.

Cette API fournit l’équivalent de la navigation vers un lien profond (car le *executeDeepLink* désormais déconseillé a été utilisé une fois) sans que votre application doive construire une URL ou gérer différents formats de liens profonds pour différents hôtes d’application.

##### <a name="deep-links-out-of-your-app"></a>Liens profonds hors de votre application

Pour des liens profonds entre votre application et différentes zones de son hôte actuel, utilisez les API fortement typées fournies par le Kit de développement logiciel (SDK) TeamsJS. Par exemple, utilisez la fonctionnalité *Calendrier* pour ouvrir une boîte de dialogue de planification ou un élément de calendrier à partir de votre application.

Pour les liens profonds de votre application vers d’autres applications s’exécutant sur le même hôte, utilisez `pages.navigateToApp`.

Pour tout autre scénario de liaison approfondie externe, vous pouvez utiliser `app.openLink`, qui fournit des fonctionnalités similaires à l’API *executeDeepLink* désormais déconseillée (à partir de TeamsJS v.2.0).

#### <a name="dialogs"></a>Boîtes de dialogue

À compter de la version 2.0 de TeamsJS, le concept de plateforme Teams du [module de tâche](../../task-modules-and-cards/what-are-task-modules.md) a été renommé en *boîte de dialogue* pour une meilleure cohérence avec les concepts existants dans l’écosystème de développeurs Microsoft 365. Par conséquent, l’espace de noms `tasks` a été déprécié en faveur du nouvel espace de noms `dialog` .

Cette nouvelle fonctionnalité de dialogue est divisée en une fonctionnalité principale (`dialog`) pour la prise en charge des dialogues HTML et une sous-capabilité, `dialog.bot`, pour le développement de dialogues basés sur un bot.

La fonctionnalité de dialogue ne prend pas encore en charge [les dialogues de carte adaptative](../../task-modules-and-cards/task-modules/design-teams-task-modules.md). Les dialogues adaptatifs basés sur une carte doivent toujours être appelés à l’aide de `tasks.startTask()`.

La fonction `dialog.open` ne fonctionne actuellement que pour l’ouverture de boîtes de dialogue HTMl, et elle retourne une fonction de rappel (`PostMessageChannel`) que vous pouvez utiliser pour passer des messages (`ChildAppWindow.postMessage`) à la boîte de dialogue nouvellement ouverte.  `dialog.open` retourne un rappel (plutôt qu’une promesse), car il ne nécessite pas la suspension de l’exécution de l’application en attendant la fermeture de la boîte de dialogue (offrant ainsi plus de flexibilité pour différents modèles d’interaction utilisateur).

## <a name="whats-new-in-teamsjs-version-20"></a>Nouveautés de TeamsJS version 2.0

Il existe deux changements significatifs entre les versions TeamsJS 1.x.x et v.2.0.0 et ultérieures :

* [**Les fonctions de rappel retournent désormais des objets Promise.**](#callbacks-converted-to-promises) La plupart des fonctions avec des paramètres de rappel dans TeamsJS v.1.12 ont été modernisées pour retourner un objet JavaScript [Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise) pour améliorer la gestion des opérations asynchrones et la lisibilité du code.

* [**Les API sont désormais organisées en *fonctionnalités*.**](#apis-organized-into-capabilities) Vous pouvez considérer les fonctionnalités comme des regroupements logiques d’API qui fournissent des fonctionnalités similaires, telles que `authentication`, `dialog`, `chat`et `calendar`. Chaque espace de noms représente une fonctionnalité distincte.

> [!TIP]
> Vous pouvez utiliser [l’extension Teams Toolkit](https://aka.ms/teams-toolkit) pour Microsoft Visual Studio Code afin de simplifier le [processus de mise à jour TeamsJS v.2.0](#updating-to-the-teams-client-sdk-v200) pour une application Teams existante.

### <a name="backwards-compatibility"></a>Compatibilité descendante

Une fois que vous commencez à référencer `@microsoft/teams-js@2.0.0` (ou version ultérieure) à partir d’une application Teams existante, vous verrez des avertissements de dépréciation pour tout code appelant des API qui ont changé.

Une couche de traduction d’API (mappage du Kit de développement logiciel (SDK) v.1 aux appels d’API du Kit de développement logiciel (SDK) v.2) est fournie pour permettre aux applications Teams existantes de continuer à travailler dans Teams jusqu’à ce qu’elles soient en mesure de mettre à jour le code d’application pour utiliser les modèles d’API TeamsJS v.2.

#### <a name="teams-only-apps"></a>Applications Teams uniquement

Même si vous envisagez que votre application s’exécute uniquement dans Teams (et non dans Office et Outlook), il est recommandé de commencer à référencer la dernière version de TeamsJS (*v.2.0* ou ultérieure) dès que possible, afin de tirer parti des dernières améliorations, des nouvelles fonctionnalités et du support (même pour les applications Teams uniquement). TeamsJS v.1.12 continuera d’être pris en charge, mais aucune nouvelle fonctionnalité ou amélioration ne sera ajoutée.

Une fois que vous êtes en mesure de le faire, l’étape suivante consiste à [mettre à jour le code d’application existant](#2-update-sdk-references) avec les modifications décrites dans cet article. En attendant, la couche de traduction de l’API v.1 vers v.2 offre une compatibilité descendante, ce qui garantit que votre application Teams existante continue de fonctionner dans TeamsJS version 2.0.

#### <a name="teams-apps-running-across-microsoft-365"></a>Applications Teams s’exécutant sur Microsoft 365

L’activation d’une application Teams existante pour s’exécuter dans Outlook et Office nécessite les éléments suivants :

1. Dépendance vis-à-vis de TeamsJS version 2.0 ( `@microsoft/teams-js@2.0`) ou ultérieure,

2. [Modification du code d’application existant](#2-update-sdk-references) en fonction des modifications requises décrites dans cet article, et

3. [Mise à jour du manifeste de votre application](#3-update-the-manifest-optional) vers la version 1.13 ou ultérieure.

Pour plus d’informations, consultez [Étendre les applications Teams sur Microsoft 365](../../m365-apps/overview.md).

### <a name="callbacks-converted-to-promises"></a>Rappels convertis en promesses

Les API Teams qui ont précédemment pris un paramètre de rappel ont été mises à jour pour retourner un objet JavaScript [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) . Il s’agit notamment des API suivantes :

```js
app.getContext, app.initialize, appInstallDialog.openAppInstallDialog, app.openLink, authentication.authenticate, authentication.getAuthToken, authentication.getUser, authentication.registerAuthenticationHandlers was removed to support using Promises, calendar.openCalendarItem, calendar.composeMeeting, call.startCall, chat.getChatMembers, conversations.openConversation, location.getLocation, location.showLocation, mail.openMailItem, mail.composeMail, pages.backStack.navigateBack, pages.navigateCrossDomain, pages.navigateToTab, pages.tabs.getMruTabInstances, pages.tabs.getTabInstances, pages.getConfig, pages.config.setConfig, pages.backStack.navigateBack, people.selectPeople, teams.fullTrust.getConfigSetting, teams.fullTrust.joinedTeams.getUserJoinedTeams
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
> Lorsque vous utilisez [Teams toolkit pour effectuer une mise à jour vers TeamsJS v.2.0](#updating-to-the-teams-client-sdk-v200), les mises à jour requises sont signalées pour vous avec `TODO` commentaires dans votre code client.

### <a name="apis-organized-into-capabilities"></a>API organisées en fonctionnalités

Une *fonctionnalité* est un regroupement logique (via un espace de noms) d’API qui fournissent des fonctionnalités similaires. Vous pouvez considérer Microsoft Teams, Outlook et Office comme des hôtes de votre application d’onglet. Un hôte prend en charge une fonctionnalité donnée s’il prend en charge toutes les API définies dans cette fonctionnalité. Un hôte ne peut pas implémenter partiellement une fonctionnalité. Les fonctionnalités peuvent être basées sur des fonctionnalités ou du contenu, telles que *l’authentification* ou *la boîte de dialogue*. Il existe également des fonctionnalités pour les types d’application tels que les *pages* et d’autres regroupements.

À compter de TeamsJS v.2.0, les API sont définies en tant que fonctions dans un espace de noms JavaScript dont le nom correspond à la fonctionnalité requise. Par exemple, si une application s’exécute dans un hôte qui prend en charge la fonctionnalité de *boîte de dialogue* , l’application peut appeler en toute sécurité des API telles que `dialog.open` (en plus d’autres API liées au dialogue définies dans l’espace de noms). Si une application tente d’appeler une API qui n’est pas prise en charge dans cet hôte, l’API lève une exception. Pour vérifier si l’hôte actuel exécutant votre application prend en charge une fonctionnalité donnée, appelez la fonction [isSupported()](#differentiate-your-app-experience) de son espace de noms.

#### <a name="differentiate-your-app-experience"></a>Différencier votre expérience d’application

Vous pouvez vérifier la prise en charge par l’hôte d’une fonctionnalité donnée au moment de l’exécution en appelant la fonction`isSupported()` sur cette fonctionnalité (espace de noms). Elle retourne `true` si elle est prise en charge et `false` si ce n’est pas le cas, et vous pouvez ajuster le comportement de l’application en fonction des besoins. Cela permet à votre application d’activer l’interface utilisateur et les fonctionnalités des hôtes qui la prennent en charge, tout en continuant à s’exécuter pour les ordinateurs hôtes qui ne le prennent pas en charge.

Le nom de l’hôte dans lequel votre application s’exécute est exposé en tant que propriété *hostName* sur l’interface de contexte (`app.Context.app.host.name`), qui peut être interrogée au moment de l’exécution en appelant `getContext`. Il est également disponible en tant que `{hostName}`[valeur d’espace réservé d’URL](./access-teams-context.md#get-context-by-inserting-url-placeholder-values). Il est recommandé d’utiliser le mécanisme *hostName* avec parcimonie :

* **Ne partez pas** du principe que certaines fonctionnalités sont ou ne sont pas disponibles dans un hôte en fonction de la valeur de la propriété *hostName*. Au lieu de cela, recherchez la prise en charge des fonctionnalités (`isSupported`).
* **N’utilisez** pas *hostName* pour contrôler les appels d’API. Au lieu de cela, recherchez la prise en charge des fonctionnalités (`isSupported`).
* **Utilisez***hostName* pour différencier le thème de votre application en fonction de l’hôte dans lequel elle s’exécute. Par exemple, vous pouvez utiliser Microsoft Teams violet comme couleur d’accentuation principale lors de l’exécution dans Teams, et Outlook bleu lors de l’exécution dans Outlook.
* **Utilisez** *hostName* pour différencier les messages affichés à l’utilisateur en fonction de l’hôte dans lequel il s’exécute. Par exemple, affichez *Gérer vos tâches dans Office* lors de l’exécution dans Office sur le web, et *Gérer vos tâches dans Teams* lors de l’exécution dans Microsoft Teams.

#### <a name="namespaces"></a>Espaces de noms

À compter de TeamsJS v.2.0, les API sont organisées en *fonctionnalités* par le biais d’espaces de noms. Plusieurs nouveaux espaces de noms d’une importance particulière sont *l’application*, *les pages*, la *boîte de dialogue* et *teamsCore*.

##### <a name="app-namespace"></a>Espace de noms *d’application*

L’espace de noms`app` contient les API de niveau supérieur requises pour l’utilisation globale des applications, sur Microsoft Teams, Office et Outlook. Toutes les API de différents autres espaces de noms TeamsJS ont été déplacées vers l’espace de noms `app` à partir de TeamsJS v.2.0 :

| Espace de noms d’origine `global (window)` | Nouvel espace de noms `app` |
| - | - |
| `executeDeepLink` | `app.openLink` (renommé) |
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

##### <a name="pages-namespace"></a>espace de noms *pages*

L’espace de noms `pages` inclut des fonctionnalités permettant d’exécuter et de parcourir des pages web dans différents hôtes Microsoft 365, notamment Teams, Office et Outlook. Il inclut également plusieurs sous-éléments, implémentés en tant que sous-espaces.

| Espace de noms d’origine `global (window)` | Nouvel espace de noms `pages` |
| - | - |
| `setFrameContext` | `pages.setCurrentFrame` (renommé) |
| `initializeWithFrameContext` | `pages.initializeWithFrameContext` |
| `registerFocusEnterHandler` | `pages.registerFocusEnterHandler`
| `registerFullScreenHandler` | `pages.registerFullScreenHandler` |
| `navigateCrossDomain` | `pages.navigateCrossDomain` |
| `returnFocus` | `pages.returnFocus` |
| `shareDeepLink` | `pages.shareDeepLink` |

| Espace de noms d’origine `settings` | Nouvel espace de noms `pages`  |
| - | - |
| `settings.getSettings` | `pages.getConfig` (renommé)

###### <a name="pagestabs"></a>*pages.tabs*

| Espace de noms d’origine `global (window)` | Nouvel espace de noms `pages.tabs` |
| - | - |
| `getTabInstances` |  `pages.tabs.getTabInstances` |
| `getMruTabInstances` | `pages.tabs.getMruTabInstances` |

| Espace de noms d’origine `navigation` | Nouvel espace de noms `pages.tabs` |
| - | - |
| `navigation.navigateToTab` | `pages.tabs.navigateToTab` |

###### <a name="pagesconfig"></a>*pages.config*

| Espace de noms d’origine `settings` | Nouvel espace de noms `pages.config`  |
| - | - |
| `settings.setSettings` | `pages.config.setConfig` (renommé)
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
| `registerChangeConfigHandler` | `pages.config.registerChangeConfigHandler` (renommé)

###### <a name="pagesbackstack"></a>*pages.backStack*

| Espace de noms d’origine `navigation` | Nouvel espace de noms `pages.backStack`  |
| - | - |
| `navigation.navigateBack` | `pages.backStack.navigateBack`

| Espace de noms d’origine `global (window)` | Nouvel espace de noms `pages.backStack`  |
| - | - |
| `registerBackButtonHandler` | `pages.backStack.registerBackButtonHandler`

###### <a name="pagesappbutton"></a>*pages.appButton*

| Espace de noms d’origine `global (window)` | Nouvel espace de noms `pages.appButton`  |
| - | - |
| `registerAppButtonClickHandler` | `pages.appButton.onClick` (renommé)
| `registerAppButtonHoverEnterHandler` | `pages.appButton.onHoverEnter` (renommé)
| `registerAppButtonHoverLeaveEnter` | `pages.appButton.onHoverLeave` (renommé)
| interface de `FrameContext` | `pages.appButton.FrameInfo` (renommé)) |

##### <a name="dialog-namespace"></a>espace de noms de *boîte de dialogue*

Les tâches *TeamsJS* espace de noms ont été renommées en *boîte de dialogue* et les API suivantes ont été renommées :

| Espace de noms d’origine `tasks` | Nouvel espace de noms `dialog`  |
| - | - |
| `tasks.startTask` | `dialog.open` (renommé) |
| `tasks.submitTasks` | `dialog.submit` (renommé) |
| `tasks.updateTasks` | `dialog.update.resize` (renommé) |
| `tasks.TaskModuleDimension` enum | `dialog.DialogDimension` (renommé) |
| interface de `tasks.TaskInfo` | `dialog.DialogInfo` (renommé) |

En outre, cette fonctionnalité a été divisée en une fonctionnalité principale (`dialog`) pour la prise en charge des dialogues HTML, et une sous-capacité pour les dialogues basés sur un bot, `dialog.bot`.

##### <a name="teamscore-namespace"></a>espace de noms *teamsCore*

Pour généraliser le Kit de développement logiciel (SDK) TeamsJS afin d’exécuter d’autres hôtes Microsoft 365 tels qu’Office et Outlook, les fonctionnalités spécifiques à Teams (à l’origine dans l’espace de noms *global*) ont été déplacées vers un espace de noms *teamsCore* :

| Espace de noms d’origine `global (window)` | Nouvel espace de noms `teamsCore`  |
| - | - |
| `enablePrintCapability` | `teamsCore.enablePrintCapability`
| `print` | `teamsCore.print`
| `registerOnLoadHandler` | `teamsCore.registerOnLoadHandler`
| `registerBeforeUnloadHandler` | `teamsCore.registerBeforeUnloadHandler`

#### <a name="updates-to-the-context-interface"></a>Mises à jour de l’interface *contextuel*

L’interface `Context` a été déplacée vers l’espace de noms `app` et mise à jour pour regrouper des propriétés similaires pour une meilleure extensibilité lors de son exécution dans Outlook et Office, en plus de Teams.

Une nouvelle propriété `app.Context.app.host.name` a été ajoutée pour permettre aux onglets de différencier l’expérience utilisateur en fonction de l’application hôte.

Vous pouvez également visualiser les modifications en examinant la fonction `transformLegacyContextToAppContext` dans la [source TeamsJS v.2.0](https://github.com/OfficeDev/microsoft-teams-library-js/blob/main/packages/teams-js/src/public/app.ts)  (*fichier app.ts* ).

| Nom d’origine dans l’interface `Context` | Nouvel emplacement dans `app.Context` |
| - | - |
| `appIconPosition` | `app.Context.app.iconPositionVertical` |
| `appLaunchId`| *NON INCLUS DANS TeamsJS v.2.0* |
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

## <a name="updating-to-the-teams-client-sdk-v200"></a>Mise à jour vers le Kit de développement logiciel (SDK) client Teams v.2.0.0

Le moyen le plus simple de mettre à jour votre application Teams pour utiliser TeamsJS v.2.0 consiste à utiliser [l’extension Teams Toolkit](https://aka.ms/teams-toolkit) pour Visual Studio Code. Cette section vous guide tout au long des étapes à suivre. Si vous préférez mettre à jour manuellement votre code, consultez les sections[rappels convertis en promesses](#callbacks-converted-to-promises) et [API organisées en fonctionnalités](#apis-organized-into-capabilities) pour plus d’informations sur les modifications d’API requises.

### <a name="1-install-the-latest-teams-toolkit-visual-studio-code-extension"></a>1. Installer la dernière extension Visual Studio Code du Kit de ressources Teams

Dans la *Place de marché des extensions Visual Studio Code*, recherchez **Teams Toolkit** et installez la version `2.10.0` ou une version ultérieure.

### <a name="2-update-sdk-references"></a>2. Mettre à jour les références du Kit de développement logiciel (SDK)

Pour s’exécuter dans Outlook et Office, votre application doit dépendre du [package npm](https://www.npmjs.com/package/@microsoft/teams-js/v/2.0.0)`@microsoft/teams-js@2.0.0` (ou version ultérieure). Pour effectuer ces étapes manuellement et pour plus d’informations sur les modifications apportées à l’API, consultez les sections suivantes sur les rappels [convertis en promesses](#callbacks-converted-to-promises) et [API organisées en fonctionnalités](#apis-organized-into-capabilities).

1. Vérifiez que vous avez [Teams Toolkit](https://aka.ms/teams-toolkit) `v.2.10.0` ou une version ultérieure
1. Ouvrez la *Palette de commandes* : `Ctrl+Shift+P`
1. Exécutez la commande `Teams: Upgrade Teams JS SDK references to support Outlook and Office apps`

Une fois l’opération terminée, l’utilitaire aura mis à jour votre fichier `package.json` avec la dépendance TeamsJS v.2.0 (`@microsoft/teams-js@2.0.0` ou version ultérieure), et vos fichiers `*.js/.ts` et `*.jsx/.tsx` seront mis à jour avec :

> [!div class="checklist"]
>
> * `package.json` références à TeamsJS v.2.0
> * Importer des instructions pour TeamsJS v.2.0
> * [Appels de fonction, d’énumération et d’interface](#apis-organized-into-capabilities) à TeamsJS v.2.0
> * `TODO`rappels de commentaires pour passer en revue les zones susceptibles d’être affectées par les modifications apportées à l’interface [de contexte](#updates-to-the-context-interface)
> * `TODO` rappels de commentaire pour [convertir des fonctions de rappel en promesses](#callbacks-converted-to-promises)

> [!IMPORTANT]
> Le code contenu dans les fichiers HTML n’est pas pris en charge par les outils de mise à niveau et nécessite des modifications manuelles.

### <a name="3-update-the-manifest-optional"></a>3. Mettre à jour le manifeste (facultatif)

Si vous mettez à jour une application Teams pour qu’elle s’exécute dans Office et Outlook, vous devez également mettre à jour le manifeste de l’application vers la version 1.13 ou ultérieure. Vous pouvez le faire facilement avec le Kit de ressources Teams ou manuellement.

# <a name="teams-toolkit"></a>[Toolkit Teams](#tab/manifest-teams-toolkit)

1. Ouvrez la *palette de commandes* : `Ctrl+Shift+P`
1. Exécuter **Teams : mettez à niveau le manifeste Teams pour prendre en charge la commande Applications Outlook et Office** et sélectionnez votre fichier manifeste d’application. Des modifications seront apportées en place.

# <a name="manual-steps"></a>[Étapes manuelles](#tab/manifest-manual)

Ouvrez le manifeste de votre application Teams et mettez à jour les `$schema` et `manifestVersion` valeurs suivantes :

```json
{
    "$schema" : "https://developer.microsoft.com/json-schemas/teams/v1.13/MicrosoftTeams.schema.json",
    "manifestVersion" : "1.13"
}
```

---

Si vous avez utilisé Teams Toolkit pour créer votre application personnelle, vous pouvez également l'utiliser pour valider les modifications apportées à votre fichier manifeste et identifier les éventuelles erreurs. Ouvrez la palette de commandes `Ctrl+Shift+P`et recherchez **Teams : Valider le fichier manifeste** ou sélectionnez l’option dans le menu Déploiement du Teams Toolkit (recherchez l’icône Teams sur le côté gauche de Visual Studio Code).

:::image type="content" source="../../m365-apps/images/toolkit-validate-manifest-file.png" alt-text="Option « Valider le fichier manifeste » du Kit de ressources Teams sous le menu « Déploiement »":::

## <a name="next-steps"></a>Étapes suivantes

* Utilisez la [référence TeamsJS](/javascript/api/overview/msteams-client) pour bien démarrer avec le Kit de développement logiciel (SDK) client JavaScript Microsoft Teams.
* Consultez le [journal des modifications](https://github.com/OfficeDev/microsoft-teams-library-js/blob/main/packages/teams-js/CHANGELOG.md) pour connaître les dernières mises à jour de TeamsJS.
