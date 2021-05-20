---
title: Onglets de construction et autres expériences hébergées avec le client JavaScript SDK
author: heath-hamilton
ms.author: surbhigupta
description: Aperçu des Microsoft Teams client JavaScript SDK, qui peuvent vous aider à créer Teams expériences d’applications hébergées dans un <iframe>.
localization_priority: Normal
keywords: équipes onglets canal de groupe configurable statique SDK JavaScript personnel
ms.topic: conceptual
ms.openlocfilehash: d3dfadda7f2a56e32ecf8e5b67df3b9831c52739
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566655"
---
# <a name="building-tabs-and-other-hosted-experiences-with-the-microsoft-teams-javascript-client-sdk"></a>Création d’onglets et d’autres expériences hébergées avec Microsoft Teams client JavaScript SDK

Le Microsoft Teams client JavaScript SDK peut vous aider à créer des expériences hébergées dans Teams, ce qui signifie afficher le contenu de votre application dans un iframe.

Le SDK est utile pour développer des applications avec l’une des fonctionnalités Teams suivantes :

* [Onglets](../../tabs/what-are-tabs.md)
* [Modules de tâche](../../task-modules-and-cards/what-are-task-modules.md)

Par exemple, le SDK peut faire réagir votre [onglet aux modifications de thème apportées](../../build-your-first-app/build-personal-tab.md) par vos utilisateurs dans Teams client.

## <a name="getting-started"></a>Prise en main

Faites l’un des éléments suivants en fonction de vos préférences de développement :

* [Installez le SDK avec npm ou Yarn](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)

## <a name="common-sdk-functions"></a>Fonctions SDK courantes

Consultez les tableaux suivants pour comprendre les fonctions SDK couramment utilisées. La [documentation de référence SDK fournit](/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true) des informations plus complètes :


### <a name="basic-functions"></a>Fonctions de base

| Fonction  | Description          | Documentation|
| -----     | -----     | -----    |
| `microsoftTeams.initialize()` | Initialise le SDK. Cette fonction doit être appelée avant tout autre appel SDK.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#initialize-any-&preserve-view=true)|
|`microsoftTeams.getContext(callback: (context: Context)`| Obtient l’état actuel dans lequel la page est en cours d’exécution. Le rappel récupère **l’objet** Context.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#getcontext--context--context-----void-&preserve-view=true)<br/>[contexte obj](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true)|
| `microsoftTeams.initializeWithContext({contentUrl: string, websiteUrl: string})` | Initialise la bibliothèque Teams et définit le contexte du cadre de [l’onglet](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true) en fonction du contenuUrl et du site WebUrl. Cela garantit que la fonctionnalité go-to-website ou recharge fonctionne sur l’URL correcte.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#initializewithframecontext-framecontext--------void--string---&preserve-view=true)|
| `microsoftTeams.setFrameContext({contentUrl: string, websiteUrl: string})` | Définit le contexte du cadre [de l’onglet](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true) en fonction du contenuUrl et websiteUrl. Cela garantit que la fonctionnalité go-to-website ou recharge fonctionne sur l’URL correcte.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#setframecontext-framecontext-&preserve-view=true)|
| `microsoftTeams.registerFullScreenHandler(handler: (isFullScreen: boolean)` |Le gestionnaire qui est enregistré lorsque l’utilisateur bascule la vue plein écran ou fenêtre d’un onglet.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#registerfullscreenhandler--isfullscreen--boolean-----void-&preserve-view=true)<br/>[boolean](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#registerFullScreenHandler__isFullScreen__boolean_____void_&preserve-view=true)|
|`microsoftTeams.registerChangeSettingsHandler()` |Le gestionnaire enregistré lorsque l’utilisateur sélectionne le bouton Paramètres **activé** pour reconfigurer un onglet.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#registerchangesettingshandler-------void-&preserve-view=true)|
| `microsoftTeams.getTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters,)` |Obtient les onglets appartenant à l’application. Le rappel récupère **l’objet TabInformation.** **L’objet TabInstanceParameters** est un paramètre optionnel.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#gettabinstances--tabinfo--tabinformation-----void--tabinstanceparameters-&preserve-view=true)<br/>[obj tabInfo](/javascript/api/@microsoft/teams-js/tabinformation?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.getMruTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters)`|Obtient les onglets les plus récemment utilisés pour l’utilisateur. Le rappel récupère **l’objet TabInformation.** **L’objet TabInstanceParameters** est un paramètre optionnel.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#getmrutabinstances--tabinfo--tabinformation-----void--tabinstanceparameters-&preserve-view=true)<br/>[obj tabInfo](/javascript/api/@microsoft/teams-js/tabinformation?view=msteams-client-js-latest&preserve-view=true)<br/>[tabInstance obj](/javascript/api/@microsoft/teams-js/tabinstanceparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.shareDeepLink(deepLinkParameters: DeepLinkParameters)`|Prend **l’objet DeepLinkParameters comme** entrée et partage une boîte de dialogue de lien profond qu’un utilisateur peut utiliser pour naviguer vers le contenu *dans l’onglet*.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#sharedeeplink-deeplinkparameters-&preserve-view=true)<br/>[obj deepLink](/javascript/api/@microsoft/teams-js/deeplinkparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.executeDeepLink(deepLink: string, onComplete?: (status: boolean, reason?: string))`|Prend un **deepLink requis comme** entrée et navigue utilisateur vers une URL ou déclenche une action client, comme l’ouverture ou l’installation d’une application dans *Teams*.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#executedeeplink-string---status--boolean--reason---string-----void-&preserve-view=true)|
|`microsoftTeams.navigateToTab(tabInstance: TabInstance, onComplete?: (status: boolean, reason?: string))`|Prend **l’objet TabInstance** comme entrée et navigue vers une instance d’onglet spécifiée.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#navigatetotab-tabinstance-&preserve-view=true)<br/>[tabInstance obj](/javascript/api/@microsoft/teams-js/tabinstance?view=msteams-client-js-latest&preserve-view=true)|

### <a name="authentication-namespace"></a>Espace nominatif d’authentification

| Fonction  | Description          | Documentation|
| -----     | -----     | -----    |
|`microsoftTeams.authentication.authenticate(authenticateParameters?: AuthenticateParameters)`|Lance une demande d’authentification qui ouvre une nouvelle fenêtre avec les paramètres fournis par l’appelant. Les valeurs d’entrée optionnelles sont définies **par l’objet AuthenticateParameters.**|[function](/javascript/api/@microsoft/teams-js/authentication?view=msteams-client-js-latest&preserve-view=true)<br/>[auth obj](/javascript/api/@microsoft/teams-js/authenticateparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.authentication.notifySuccess(result?: string, callbackUrl?: string)`|Informe le cadre à l’origine de la demande d’authentification que la demande a été réussie et ferme la fenêtre d’authentification|[function](/javascript/api/@microsoft/teams-js/authentication?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.authentication.notifyFailure(reason?: string, callbackUrl?: string)`|Informe le cadre à l’origine de la demande d’authentification que la demande a échoué et ferme la fenêtre d’authentification.|[function](/javascript/api/@microsoft/teams-js/authentication?view=msteams-client-js-latest&preserve-view=true)|

### <a name="settings-namespace"></a>Paramètres’espace nominatif

| Fonction  | Description          | Documentation|
| -----     | -----     | -----    |
|`microsoftTeams.settings.setValidityState(validityState: boolean)`|La valeur initiale est fausse. Active le bouton **Enregistrer** ou **supprimer lorsque** l’état de validité est vrai.|[function](/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.getSettings(callback: (instanceSettings: Settings)`|Obtient les paramètres pour l’instance en cours. Le rappel récupère **l’objet** Paramètres’objet.|[function](/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest&preserve-view=true)<br/>[paramètres obj](/javascript/api/@microsoft/teams-js/_settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.setSettings(instanceSettings: Settings, onComplete?: (status: boolean, reason?: string)`|Configure les paramètres de l’instance actuelle. Les paramètres valides sont définis par **Paramètres objet.**|[function](/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest&preserve-view=true)<br/>[paramètres obj](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.registerOnSaveHandler(handler: (evt: SaveEvent)`|Le gestionnaire enregistré lorsque l’utilisateur sélectionne le bouton **Enregistrer.** Ce gestionnaire doit être utilisé pour créer ou mettre à jour la ressource sous-jacente qui alimenter le contenu.|[function](/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.registerOnRemoveHandler(handler: (evt: RemoveEvent)`|Le gestionnaire qui est enregistré lorsque l’utilisateur sélectionne le **bouton Supprimer.** Ce gestionnaire doit être utilisé pour supprimer la ressource sous-jacente qui alimenter le contenu.|[function](/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest&preserve-view=true)|

### <a name="task-modules-namespace"></a>Modules de tâches espace de nom

| Fonction  | Description          | Documentation|
| -----     | -----     | -----    |
|`microsoftTeams.tasks.startTask(taskInfo: TaskInfo, submitHandler?: (err: string, result: string)`|Prend **l’objet TaskInfo** comme entrée et permet à une application d’ouvrir le module de tâches. Le **submitHandler optionnel** est enregistré lorsque le module de tâche est terminé. |[function](/javascript/api/@microsoft/teams-js/tasks?view=msteams-client-js-latest&preserve-view=true)<br/>[taskInfo obj](/javascript/api/@microsoft/teams-js/taskinfo?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.tasks.submitTask(result?: string | object, appIds?: string | string[])`|Soumet le module de tâches. Le paramètre **de** chaîne de résultat optionnel est le résultat envoyé au bot ou à l’application et est généralement un objet JSON ou une sérialisation; Le paramètre **appIds** en option ou le paramètre du réseau de chaînes permet de valider que l’appel provient de la même appId que celle qui invoquait le module de tâche.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)|
