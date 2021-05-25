---
title: Création d’onglets et d’autres expériences hébergées avec le SDK client JavaScript
author: heath-hamilton
ms.author: surbhigupta
description: Vue d’ensemble Microsoft Teams du SDK client JavaScript, qui peut vous aider à créer Teams expériences d’application hébergées dans un <iframe>.
localization_priority: Normal
keywords: onglets teams canal de groupe configurable statique SDK JavaScript personnel
ms.topic: conceptual
ms.openlocfilehash: 04c6bb9d7687a068375bce548588e6713fd57747
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630340"
---
# <a name="building-tabs-and-other-hosted-experiences-with-the-microsoft-teams-javascript-client-sdk"></a>Création d’onglets et d’autres expériences hébergées avec Microsoft Teams SDK client JavaScript

Le Microsoft Teams SDK client JavaScript peut vous aider à créer des expériences hébergées dans Teams, ce qui signifie afficher le contenu de votre application dans un iframe.

Le SDK est utile pour le développement d’applications avec l’une des fonctionnalités Teams suivantes :

* [Onglets](../../tabs/what-are-tabs.md)
* [Modules de tâche](../../task-modules-and-cards/what-are-task-modules.md)

Par exemple, le SDK peut faire réagir votre [onglet](../../build-your-first-app/build-personal-tab.md#3-update-your-tab-theme) aux modifications de thème apportées par vos utilisateurs dans Teams client.

## <a name="getting-started"></a>Prise en main

Faites l’une des choses suivantes en fonction de vos préférences de développement :

* [Installer le SDK avec npm ou NPM](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)
* [Cloner le SDK (GitHub)](https://github.com/OfficeDev/microsoft-teams-library-js)

## <a name="common-sdk-functions"></a>Fonctions SDK courantes

Consultez les tableaux suivants pour comprendre les fonctions courantes du SDK. La [documentation de référence du SDK fournit](/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true) des informations plus complètes.

### <a name="basic-functions"></a>Fonctions de base

| Fonction  | Description          | Documentation|
| -----     | -----     | -----    |
| `microsoftTeams.initialize()` | Initialise le SDK. Cette fonction doit être appelée avant tout autre appel du SDK.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#initialize-any-&preserve-view=true)|
|`microsoftTeams.getContext(callback: (context: Context)`| Obtient l’état actuel dans lequel la page est en cours d’exécution. Le rappel récupère **l’objet Context.**|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#getcontext--context--context-----void-&preserve-view=true)<br/>[context obj](/javascript/api/@microsoft/teams-js/@microsoft.teams-js?view=msteams-client-js-latest&preserve-view=true)|
| `microsoftTeams.initializeWithContext({contentUrl: string, websiteUrl: string})` | Initialise la bibliothèque Teams et définit le [](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true) contexte d’image de l’onglet en fonction de contentUrl et websiteUrl. Cela garantit que la fonctionnalité d’accès au site web/recharge fonctionne sur l’URL correcte.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#initializewithframecontext-framecontext--------void--string---&preserve-view=true)|
| `microsoftTeams.setFrameContext({contentUrl: string, websiteUrl: string})` | Définit le contexte d’image de [l’onglet](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true) en fonction de contentUrl et websiteUrl. Cela garantit que la fonctionnalité d’accès au site web/recharge fonctionne sur l’URL correcte.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#setframecontext-framecontext-&preserve-view=true)|
| `microsoftTeams.registerFullScreenHandler(handler: (isFullScreen: boolean)` |Le handler qui est enregistré lorsque l’utilisateur bascule la vue plein écran/fenêtre d’un onglet.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#registerfullscreenhandler--isfullscreen--boolean-----void-&preserve-view=true)<br/>[boolean](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#registerFullScreenHandler__isFullScreen__boolean_____void_&preserve-view=true)|
|`microsoftTeams.registerChangeSettingsHandler()` |Le handler inscrit lorsque l’utilisateur sélectionne le bouton Paramètres **pour** reconfigurer un onglet.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#registerchangesettingshandler-------void-&preserve-view=true)|
| `microsoftTeams.getTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters,)` |Obtient les onglets de l’application. Le rappel récupère l’objet **TabInformation.** **L’objet TabInstanceParameters est** un paramètre facultatif.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#gettabinstances--tabinfo--tabinformation-----void--tabinstanceparameters-&preserve-view=true)<br/>[tabInfo obj](/javascript/api/@microsoft/teams-js/microsoftteams.tabinformation?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.getMruTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters)`|Obtient les derniers onglets utilisés pour l’utilisateur. Le rappel récupère l’objet **TabInformation.** **L’objet TabInstanceParameters est** un paramètre facultatif.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#getmrutabinstances--tabinfo--tabinformation-----void--tabinstanceparameters-&preserve-view=true)<br/>[tabInfo obj](/javascript/api/@microsoft/teams-js/microsoftteams.tabinformation?view=msteams-client-js-latest&preserve-view=true)<br/>[tabInstance obj](/javascript/api/@microsoft/teams-js/microsoftteams.tabinstanceparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.shareDeepLink(deepLinkParameters: DeepLinkParameters)`|Prend **l’objet DeepLinkParameters** comme entrée et partage une boîte de dialogue de lien profond qu’un utilisateur peut utiliser pour accéder au contenu de *l’onglet.*|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#sharedeeplink-deeplinkparameters-&preserve-view=true)<br/>[deepLink obj](/javascript/api/@microsoft/teams-js/microsoftteams.deeplinkparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.executeDeepLink(deepLink: string, onComplete?: (status: boolean, reason?: string))`|Prend un **deepLink** requis en tant qu’entrée et permet à l’utilisateur d’accéder à une URL ou déclenche une action du client, telle que l’ouverture ou l’installation, d’une application dans *Teams*.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#executedeeplink-string---status--boolean--reason---string-----void-&preserve-view=true)|
|`microsoftTeams.navigateToTab(tabInstance: TabInstance, onComplete?: (status: boolean, reason?: string))`|Prend **l’objet TabInstance** comme entrée et navigue jusqu’à une instance d’onglet spécifiée.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#navigatetotab-tabinstance-&preserve-view=true)<br/>[tabInstance obj](/javascript/api/@microsoft/teams-js/microsoftteams.tabinstance?view=msteams-client-js-latest&preserve-view=true)|

### <a name="authentication-namespace"></a>Espace de noms d’authentification

| Fonction  | Description          | Documentation|
| -----     | -----     | -----    |
|`microsoftTeams.authentication.authenticate(authenticateParameters?: AuthenticateParameters)`|Lance une demande d’authentification qui ouvre une nouvelle fenêtre avec les paramètres fournis par l’appelant. Les valeurs d’entrée facultatives sont définies par **l’objet AuthenticateParameters.**|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest&preserve-view=true)<br/>[auth obj](/javascript/api/@microsoft/teams-js/microsoftteams.authentication.authenticateparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.authentication.notifySuccess(result?: string, callbackUrl?: string)`|Avertit la trame à l’origine de la demande d’authentification que la demande a réussi et ferme la fenêtre d’authentification.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.authentication.notifyFailure(reason?: string, callbackUrl?: string)`|Avertit la trame à l’origine de la demande d’authentification que la demande a échoué et ferme la fenêtre d’authentification.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest&preserve-view=true)|

### <a name="settings-namespace"></a>Paramètres de noms

| Fonction  | Description          | Documentation|
| -----     | -----     | -----    |
|`microsoftTeams.settings.setValidityState(validityState: boolean)`|La valeur initiale est false. Active le bouton **Enregistrer** ou **Supprimer** lorsque l’état de validité est true.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.getSettings(callback: (instanceSettings: Settings)`|Obtient les paramètres de l’instance actuelle. Le rappel récupère **l’Paramètres** objet.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)<br/>[settings obj](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.setSettings(instanceSettings: Settings, onComplete?: (status: boolean, reason?: string)`|Configure les paramètres de l’instance actuelle. Les paramètres valides sont définis par **l’objet Paramètres.**|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)<br/>[settings obj](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.registerOnSaveHandler(handler: (evt: SaveEvent)`|Le handler qui est enregistré lorsque l’utilisateur sélectionne le **bouton Enregistrer.** Ce handler doit être utilisé pour créer ou mettre à jour la ressource sous-jacente qui alimentera le contenu.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.registerOnRemoveHandler(handler: (evt: RemoveEvent)`|Le handler inscrit lorsque l’utilisateur sélectionne le **bouton** Supprimer. Ce handler doit être utilisé pour supprimer la ressource sous-jacente qui alimentera le contenu.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|

### <a name="task-modules-namespace"></a>Espace de noms des modules de tâche

| Fonction  | Description          | Documentation|
| -----     | -----     | -----    |
|`microsoftTeams.tasks.startTask(taskInfo: TaskInfo, submitHandler?: (err: string, result: string)`|Prend **l’objet TaskInfo** comme entrée et permet à une application d’ouvrir le module de tâche. Le **submitHandler facultatif** est inscrit lorsque le module de tâche est terminé. |[function](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest&preserve-view=true)<br/>[taskInfo obj](/javascript/api/@microsoft/teams-js/microsoftteams.taskinfo?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.tasks.submitTask(result?: string | object, appIds?: string | string[])`|Envoie le module de tâche. Le paramètre **de chaîne** de résultat facultatif est le résultat envoyé au bot ou à l’application et est généralement un objet JSON ou une sérialisation ; Le paramètre facultatif de chaîne **appIds** ou de tableau de chaînes permet de valider que l’appel provient du même appId que celui qui a appelé le module de tâche.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)|
