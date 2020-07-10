---
title: Utilisation du kit de développement logiciel client Teams
author: laujan
description: Comment utiliser le kit de développement logiciel (SDK) Team client pour ajouter une fonctionnalité de teams à vos onglets personnalisés
keywords: onglets teams groupe de kit de développement logiciel (SDK) statique Java personnel
ms.topic: conceptual
ms.openlocfilehash: 07903d766ac67f2dbc9fc09268618ac5c2ae33c2
ms.sourcegitcommit: 1525db0515ab310a91939d85dbbfb7e887537849
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/09/2020
ms.locfileid: "45091297"
---
# <a name="using-the-teams-client-sdk"></a>Utilisation du kit de développement logiciel client Teams

Le **Kit de développement logiciel (SDK) JavaScript de teams** et la **bibliothèque JavaScript teams** font partie de la [plateforme de développement Microsoft teams](/microsoftteams/platform/) et fournissent des outils et des processus pour faciliter la création d’applications Teams. Le kit de développement logiciel (SDK) Team client est distribué sous la forme d’un package NPM. La dernière version est disponible ici : <https://www.npmjs.com/package/@microsoft/teams-js> . La bibliothèque teams se trouve à l’adresse <https://github.com/OfficeDev/microsoft-teams-library-js> .

Le tableau suivant présente les fonctions de la bibliothèque teams généralement utilisées dans le développement d’onglets :

## <a name="teams-sdk-public-api"></a>API publique du kit de développement logiciel teams 

| Fonction  | Description          | Documentation|
| -----     | -----     | -----    | -----        |
| `microsoftTeams.initialize()` | Initialise la bibliothèque Teams. Cette fonction doit être appelée avant tout autre appel SDK.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#initialize-any-)|
|`microsoftTeams.getContext(callback: (context: Context)`| Obtient l’état actuel dans lequel la page est en cours d’exécution. Le rappel récupère l’objet de **contexte** .|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#getcontext--context--context-----void-)<br/>[obj de contexte](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest)|
| `microsoftTeams.initializeWithContext({contentUrl: string, websiteUrl: string})` | Initialise la bibliothèque teams et définit le contexte d' [image](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest) de l’onglet en fonction des ContentUrl et websiteUrl. Cela garantit que la fonctionnalité d’accès au site Web/de chargement fonctionne sur l’URL correcte.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#initializewithframecontext-framecontext--------void--string---)|
| `microsoftTeams.setFrameContext({contentUrl: string, websiteUrl: string})` | Définit le contexte d' [image](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest) de l’onglet en fonction des ContentUrl et websiteUrl. Cela garantit que la fonctionnalité d’accès au site Web/de chargement fonctionne sur l’URL correcte.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#setframecontext-framecontext-)|
| `microsoftTeams.registerFullScreenHandler(handler: (isFullScreen: boolean)` |Gestionnaire inscrit lorsque l’utilisateur active ou désactive l’affichage plein écran d’un onglet.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#registerfullscreenhandler--isfullscreen--boolean-----void-)<br/>[boolean](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest#isfullscreen)|
|`microsoftTeams.registerChangeSettingsHandler()` |Gestionnaire enregistré lorsque l’utilisateur sélectionne le bouton **paramètres** activés pour reconfigurer un onglet.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#registerchangesettingshandler-------void-)|
| `microsoftTeams.getTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters,)` |Obtient les onglets appartenant à l’application. Le rappel récupère l’objet **TabInformation** . L’objet **TabInstanceParameters** est un paramètre facultatif.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#gettabinstances--tabinfo--tabinformation-----void--tabinstanceparameters-)<br/>[tabInfo obj](/javascript/api/@microsoft/teams-js/microsoftteams.tabinformation?view=msteams-client-js-latest)|
|`microsoftTeams.getMruTabInstances(callback: (tabInfo: TabInformation),tabInstanceParameters?: TabInstanceParameters)`|Obtient les onglets les plus récemment utilisés pour l’utilisateur. Le rappel récupère l’objet **TabInformation** . L’objet **TabInstanceParameters** est un paramètre facultatif.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#getmrutabinstances--tabinfo--tabinformation-----void--tabinstanceparameters-)<br/>[tabInfo obj](/javascript/api/@microsoft/teams-js/microsoftteams.teaminformation?view=msteams-client-js-latest)<br/>[tabInstance obj](/javascript/api/@microsoft/teams-js/microsoftteams.tabinstanceparameters?view=msteams-client-js-latest)|
|`microsoftTeams.shareDeepLink(deepLinkParameters: DeepLinkParameters)`|Prend l’objet **DeepLinkParameters** comme entrée et partage une boîte de dialogue de lien profond qu’un utilisateur peut utiliser pour accéder au contenu *au sein de l’onglet*.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#sharedeeplink-deeplinkparameters-)<br/>[deepLink obj](/javascript/api/@microsoft/teams-js/microsoftteams.deeplinkparameters?view=msteams-client-js-latest)|
|`microsoftTeams.executeDeepLink(deepLink: string, onComplete?: (status: boolean, reason?: string))`|Prend un **deepLink** obligatoire comme entrée et parcourt l’utilisateur vers une URL ou déclenche une action client, telle que l’ouverture ou l’installation, une application *dans teams*.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#executedeeplink-string---status--boolean--reason---string-----void-)|
|`microsoftTeams.navigateToTab(tabInstance: TabInstance, onComplete?: (status: boolean, reason?: string))`|Prend l’objet **TabInstance** comme entrée et accède à une instance d’onglet spécifiée.|[function](/javascript/api/@microsoft/teams-js/microsoftteams?view=msteams-client-js-latest#navigatetotab-tabinstance-)<br/>[tabInstance obj](/javascript/api/@microsoft/teams-js/microsoftteams.tabinstance?view=msteams-client-js-latest)|

## <a name="authentication-namespace"></a>Espace de noms d’authentification

| Fonction  | Description          | Documentation|
| -----     | -----     | -----    | -----        |
|`microsoftTeams.authentication.authenticate(authenticateParameters?: AuthenticateParameters)`|Lance une demande d’authentification qui ouvre une nouvelle fenêtre avec les paramètres fournis par l’appelant. Les valeurs d’entrée facultatives sont définies par l’objet **AuthenticateParameters** .|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest#authenticate-authenticateparameters-)<br/>[obj d’authentification](/javascript/api/@microsoft/teams-js/microsoftteams.authentication.authenticateparameters?view=msteams-client-js-latest)|
|`microsoftTeams.authentication.notifySuccess(result?: string, callbackUrl?: string)`|Avertit le cadre qui a initié la demande d’authentification que la demande a réussi et qui ferme la fenêtre d’authentification.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest#notifysuccess-string--string-)|
|`microsoftTeams.authentication.notifyFailure(reason?: string, callbackUrl?: string)`|Indique au cadre qui a initié la demande d’authentification que la demande a échoué et ferme la fenêtre d’authentification.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest#notifyfailure-string--string-)|

## <a name="settings-namespace"></a>Espace de noms paramètres

| Fonction  | Description          | Documentation|
| -----     | -----     | -----    | -----        |
|`microsoftTeams.settings.setValidityState(validityState: boolean)`|La valeur initiale est false. Active le bouton **Enregistrer** ou **supprimer** lorsque l’état de validité est true.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings?view=msteams-client-js-latest#setvaliditystate-boolean-)|
|`microsoftTeams.settings.getSettings(callback: (instanceSettings: Settings)`|Obtient les paramètres de l’instance actuelle. Le rappel récupère l’objet **Settings** .|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings?view=msteams-client-js-latest#getsettings--instancesettings--settings-----void-)<br/>[paramètres obj](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest)|
|`microsoftTeams.settings.setSettings(instanceSettings: Settings, onComplete?: (status: boolean, reason?: string)`|Configure les paramètres de l’instance actuelle. Les paramètres valides sont définis par l’objet **Settings** .|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings?view=msteams-client-js-latest#setsettings-settings-)<br/>[paramètres obj](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest)|
|`microsoftTeams.settings.registerOnSaveHandler(handler: (evt: SaveEvent)`|Gestionnaire inscrit lorsque l’utilisateur sélectionne le bouton **Enregistrer** . Ce gestionnaire doit être utilisé pour créer ou mettre à jour la ressource sous-jacente qui alimente le contenu.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings?view=msteams-client-js-latest#registeronsavehandler--evt--saveevent-----void-)|
|`microsoftTeams.settings.registerOnRemoveHandler(handler: (evt: RemoveEvent)`|Gestionnaire inscrit lorsque l’utilisateur sélectionne le bouton **supprimer** . Ce gestionnaire doit être utilisé pour supprimer la ressource sous-jacente qui alimente le contenu.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.settings?view=msteams-client-js-latest#registeronremovehandler--evt--removeevent-----void-)|

## <a name="tasks-namespace"></a>Espace de noms tâches

| Fonction  | Description          | Documentation|
| -----     | -----     | -----    | -----        |
|`microsoftTeams.tasks.startTask(taskInfo: TaskInfo, submitHandler?: (err: string, result: string)`|Prend l’objet **TaskInfo** comme entrée et permet à une application d’ouvrir le module de tâches. L' **submitHandler** facultatif est inscrit lorsque le module de tâche est terminé. |[function](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#starttask-taskinfo---err--string--result--string-----void-)<br/>[taskInfo obj](/javascript/api/@microsoft/teams-js/microsoftteams.taskinfo?view=msteams-client-js-latest)|
|`microsoftTeams.tasks.submitTask(result?: string | object, appIds?: string | string[])`|Soumet le module de tâche. Le paramètre de chaîne de **résultats** facultatif est le résultat envoyé au bot ou à l’application ; il s’agit généralement d’un objet ou d’une sérialisation JSON ; La chaîne ou le paramètre de tableau de chaînes des **AppID** facultatifs facilite la validation de l’origine de l’appel du même AppID que celui qui a appelé le module de tâche.|[function](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---)|
