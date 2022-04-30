---
title: Création d’onglets et d’autres expériences hébergées avec le Kit de développement logiciel (SDK) client JavaScript
author: heath-hamilton
ms.author: surbhigupta
description: Vue d’ensemble du Kit de développement logiciel (SDK) client JavaScript Microsoft Teams, qui peut vous aider à créer des expériences d’application Teams hébergées dans un <iframe>. Il inclut les fonctions de base, l’espace de noms d’authentification et l’espace de noms des paramètres.
ms.localizationpriority: high
keywords: onglets teams groupe canal configurable SDK statique JavaScript personnel
ms.topic: conceptual
ms.openlocfilehash: f4204555e57c270ad03a7a01d5b231d63b72296a
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111891"
---
# <a name="building-tabs-and-other-hosted-experiences-with-the-microsoft-teams-javascript-client-sdk"></a>Création d’onglets et d’autres expériences hébergées avec le Kit de développement logiciel (SDK) client JavaScript Microsoft Teams

Le Kit de développement logiciel (SDK) client JavaScript Microsoft Teams peut vous aider à créer des expériences hébergées dans Teams, ce qui signifie l’affichage du contenu de votre application dans un iframe.

Le Kit de développement logiciel (SDK) est utile pour développer des applications avec l’une des fonctionnalités Teams suivantes :

* [Onglets](../../tabs/what-are-tabs.md)
* [Modules de tâche](../../task-modules-and-cards/what-are-task-modules.md)

Par exemple, le Kit de développement logiciel (SDK) peut faire en sorte que votre onglet [réagisse aux modifications apportées au thème](../../build-your-first-app/build-personal-tab.md#3-update-your-tab-theme) vos utilisateurs dans le client Teams.

## <a name="getting-started"></a>Prise en main

Effectuez l’une des opérations suivantes en fonction de vos préférences de développement :

* [installer le Kit de développement logiciel (SDK) avec npm ou Yarn](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)
* [Cloner le SDK (GitHub)](https://github.com/OfficeDev/microsoft-teams-library-js)

## <a name="common-sdk-functions"></a>Fonctions courantes du Kit de développement logiciel (SDK)

Consultez les tableaux suivants pour comprendre les fonctions du Kit de développement logiciel (SDK) couramment utilisées. La [documentation de référence SDK](/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true) fournit des informations plus complètes.

### <a name="basic-functions"></a>Fonctions de base

| Fonction  | Description          | Documentation|
| -----     | -----     | -----    |
| `microsoftTeams.initialize()` | Initialise le Kit de développement logiciel (SDK). Cette fonction doit être appelée avant tout autre appel du Kit de développement logiciel (SDK).|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-initialize&preserve-view=true)|
|`microsoftTeams.getContext(callback: (context: Context)`| Obtient l’état actuel dans lequel la page s’exécute. Le rappel récupère l’objet **contextuel**.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest&preserve-view=true)<br/>[obj de contexte](/javascript/api/@microsoft/teams-js/@microsoft.teams-js?view=msteams-client-js-latest&preserve-view=true)|
| `microsoftTeams.initializeWithContext({contentUrl: string, websiteUrl: string})` | Initialise la bibliothèque Teams et définit le [contexte du cadre](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true) de l'onglet en fonction du contentUrl et du websiteUrl. Cela garantit que la fonctionnalité d’accès au site web/rechargement fonctionne sur l’URL correcte.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-initializewithframecontext&preserve-view=true)|
| `microsoftTeams.setFrameContext({contentUrl: string, websiteUrl: string})` | Définit le [contexte de cadre](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true) de l’onglet en fonction de contentUrl et websiteUrl. Cela garantit que la fonctionnalité d’accès au site web/rechargement fonctionne sur l’URL correcte.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-setframecontext&preserve-view=true)|
| `microsoftTeams.registerFullScreenHandler(handler: (isFullScreen: Boolean)` |Gestionnaire inscrit lorsque l’utilisateur bascule la vue plein écran/fenêtré d’un onglet.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-registerfullscreenhandler&preserve-view=true)<br/>[Boolean](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-registerfullscreenhandler&preserve-view=true)|
|`microsoftTeams.registerChangeSettingsHandler()` |Gestionnaire inscrit lorsque l’utilisateur sélectionne le bouton **Paramètres activé** pour reconfigurer un onglet.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest&preserve-view=true)|
| `microsoftTeams.getTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters,)` |Obtient les onglets appartenant à l’application. Le rappel récupère l’objet **TabInformation**. L’objet **TabInstanceParameters** est un paramètre facultatif.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-gettabinstances&preserve-view=true)<br/>[tabInfo obj](/javascript/api/@microsoft/teams-js/microsoftteams.tabinformation?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.getMruTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters)`|Obtient les onglets les plus récemment utilisés pour l’utilisateur. Le rappel récupère l’objet **TabInformation**. L’objet **TabInstanceParameters** est un paramètre facultatif.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-getmrutabinstances&preserve-view=true)<br/>[tabInfo obj](/javascript/api/@microsoft/teams-js/microsoftteams.tabinformation?view=msteams-client-js-latest&preserve-view=true)<br/>[tabInstance obj](/javascript/api/@microsoft/teams-js/microsoftteams.tabinstanceparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.shareDeepLink(deepLinkParameters: DeepLinkParameters)`|Prend l’objet **DeepLinkParameters** comme entrée et partage une boîte de dialogue de lien profond qu’un utilisateur peut utiliser pour accéder au contenu *dans l’onglet*.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-sharedeeplink&preserve-view=true)<br/>[obj deepLink](/javascript/api/@microsoft/teams-js/microsoftteams.deeplinkparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.executeDeepLink(deepLink: string, onComplete?: (status: Boolean, reason?: string))`|Prend une **deepLink** requise en tant qu’entrée et navigue l’utilisateur vers une URL ou déclenche une action— du client en tant qu’ouverture ou installation— d’une d’application *dans Teams*.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-executedeeplink&preserve-view=true)|
|`microsoftTeams.navigateToTab(tabInstance: TabInstance, onComplete?: (status: Boolean, reason?: string))`|Prend l’objet **TabInstance** comme entrée et accède à une instance d’onglet spécifiée.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-navigatetotab&preserve-view=true)<br/>[tabInstance obj](/javascript/api/@microsoft/teams-js/microsoftteams.tabinstance?view=msteams-client-js-latest&preserve-view=true)|

### <a name="authentication-namespace"></a>Espace de noms d’authentification

| Fonction  | Description          | Documentation|
| -----     | -----     | -----    |
|`microsoftTeams.authentication.authenticate(authenticateParameters?: AuthenticateParameters)`|Lance une demande d’authentification qui ouvre une nouvelle fenêtre avec les paramètres fournis par l’appelant. Les valeurs d’entrée facultatives sont définies par l’objet **authenticateParameters**.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest&preserve-view=true)<br/>[auth obj](/javascript/api/@microsoft/teams-js/microsoftteams.authentication.authenticateparameters?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.authentication.notifySuccess(result?: string, callbackUrl?: string)`|Avertit le frame qui a lancé la demande d’authentification que la demande a réussi et ferme la fenêtre d’authentification|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.authentication.notifyFailure(reason?: string, callbackUrl?: string)`|Avertit le frame qui a lancé la demande d’authentification que la demande a échoué et ferme la fenêtre d’authentification.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.authentication.getAuthToken(authTokenRequest: AuthTokenRequest)`|Envoyez une demande pour émettre Azure AD jeton au nom de l’application. Le jeton peut être acquis à partir du cache, s’il n’a pas expiré. Sinon, une demande est envoyée à Azure AD pour obtenir un nouveau jeton.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-authentication-getauthtoken&preserve-view=true)|

### <a name="settings-namespace"></a>Espace de noms paramètres

| Fonction  | Description          | Documentation|
| -----     | -----     | -----    |
|`microsoftTeams.settings.setValidityState(validityState: Boolean)`|La valeur initiale est false. Active le bouton **Enregistrer** ou **Supprimer** lorsque l’état de validité est true.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.getSettings(callback: (instanceSettings: Settings)`|Obtient les paramètres de l’instance actuelle. Le rappel récupère l’objet **paramètres**.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)<br/>[paramètres obj](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.setSettings(instanceSettings: Settings, onComplete?: (status: Boolean, reason?: string)`|Configure les paramètres de l’instance actuelle. Les paramètres valides sont définis par l’objet **paramètres**.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)<br/>[paramètres obj](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.registerOnSaveHandler(handler: (evt: SaveEvent)`|Gestionnaire inscrit lorsque l’utilisateur sélectionne le bouton **Enregistrer** . Ce gestionnaire doit être utilisé pour créer ou mettre à jour la ressource sous-jacente qui alimente le contenu.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.settings.registerOnRemoveHandler(handler: (evt: RemoveEvent)`|Gestionnaire inscrit lorsque l’utilisateur sélectionne le bouton **Supprimer** . Ce gestionnaire doit être utilisé pour supprimer la ressource sous-jacente qui alimente le contenu.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)|

### <a name="task-modules-namespace"></a>Espace de noms des modules de tâches

| Fonction  | Description          | Documentation|
| -----     | -----     | -----    |
|`microsoftTeams.tasks.startTask(taskInfo: TaskInfo, submitHandler?: (err: string, result: string)`|Prend l’objet **TaskInfo** en entrée et permet à une application d’ouvrir le module de tâche. Le **submitHandler** facultatif est inscrit lorsque le module de tâche est terminé. |[function](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest&preserve-view=true)<br/>[taskInfo obj](/javascript/api/@microsoft/teams-js/microsoftteams.taskinfo?view=msteams-client-js-latest&preserve-view=true)|
|`microsoftTeams.tasks.submitTask(result?: string | object, appIds?: string | string[])`|Envoie le module de tâche. Le **résultat** facultatif  paramètre de chaîne est le résultat envoyé au bot ou à l’application et est généralement un objet JSON ou une sérialisation ; Le paramètre facultatif **appIds** paramètre de chaîne ou de tableau de chaînes permet de valider que l’appel provient du même appId que celui qui a appelé le module de tâche.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-tasks-submittask&preserve-view=true)|
