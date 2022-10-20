---
title: Créer des applications pour la phase de réunion Teams
author: v-sdhakshina
description: Découvrez comment créer des applications pour la phase de réunion Teams, partager des API de phase en étape et générer un lien profond pour partager du contenu pour effectuer des étapes dans les réunions.
ms.topic: conceptual
ms.author: v-sdhakshina
ms.localizationpriority: medium
ms.date: 04/07/2022
ms.openlocfilehash: 440e48d370d18564f5bba869d95c63bc25b11e4e
ms.sourcegitcommit: 40d4bde10b6820c62e49e2400b10ab3569c8c815
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/20/2022
ms.locfileid: "68615396"
---
# <a name="build-apps-for-teams-meeting-stage"></a>Créer des applications pour la phase de réunion Teams

Le partage à l’étape permet aux utilisateurs de partager une application vers la phase de réunion à partir du panneau côté réunion dans une réunion en cours. Ce partage est interactif et collaboratif par rapport au partage d’écran passif.

Pour appeler le partage en phase, les utilisateurs peuvent sélectionner l’icône **Partager en étape** en haut à droite du panneau côté réunion. **L’icône Partager en phase** est native pour le client Teams et la sélection de cette icône partage l’intégralité de l’application à la phase de réunion.

## <a name="app-manifest-settings-for-apps-in-meeting-stage"></a>Paramètres de manifeste d’application pour les applications en phase de réunion

Pour partager une application à la phase de réunion, mettez à jour la `context` propriété dans le manifeste de l’application comme suit :

```json
"context":[ 
    "meetingSidePanel", 
    "meetingStage" 
     ] 
```

## <a name="advanced-share-to-stage-apis"></a>API de partage avancé à étape

Il existe de nombreux scénarios où le partage de l’application entière à la phase de réunion n’est pas aussi utile que le partage de parties spécifiques de l’application :  

1. Pour une application de brainstorming ou de tableau blanc, un utilisateur peut vouloir partager un tableau spécifique dans une réunion par rapport à l’application entière avec tous les tableaux.  

1. Pour une application médicale, un médecin peut vouloir partager uniquement le rayon X à l’écran avec le patient plutôt que de partager l’application entière avec tous les dossiers ou résultats des patients, et ainsi de suite.

1. Un utilisateur peut vouloir partager du contenu à partir d’un seul fournisseur de contenu à la fois (par exemple, YouTube) plutôt que de partager l’intégralité d’un catalogue de vidéos sur scène.

Pour aider les utilisateurs dans de tels scénarios, nous avons publié des API dans le Kit de développement logiciel (SDK) du client Teams qui vous permet d’appeler par programmation un partage en phase pour des parties spécifiques de l’application à partir d’un bouton dans le panneau côté réunion.

:::image type="content" source="../assets/images/apps-in-meetings/shared-meeting-stage-edit-review-component.png" alt-text="La capture d’écran montre l’affichage de la phase de partage vers la réunion.":::

Utilisez les API suivantes pour partager une partie spécifique de l’application :

|Méthode| Description| Source|
|---|---|----|
|[**Partager le contenu de l’application à l’étape**](#share-app-content-to-stage-api)| Partagez des parties spécifiques de l’application à la phase de réunion à partir du panneau côté réunion dans une réunion. | [Kit de développement logiciel (SDK) de bibliothèque JavaScript Microsoft Teams](/javascript/api/@microsoft/teams-js/meeting) |
|[**Obtenir l’état de partage de la phase de contenu de l’application**](#get-app-content-stage-sharing-state-api)| Récupérez des informations sur l’état de partage de l’application lors de la phase de réunion. | [Kit de développement logiciel (SDK) de bibliothèque JavaScript Microsoft Teams](/javascript/api/@microsoft/teams-js/meeting.iappcontentstagesharingstate) |
|[**Obtenir les fonctionnalités de partage de phase de contenu d’application**](#get-app-content-stage-sharing-capabilities-api)| Récupérez les fonctionnalités de l’application pour le partage dans la phase de réunion. | [Kit de développement logiciel (SDK) de bibliothèque JavaScript Microsoft Teams](/javascript/api/@microsoft/teams-js/meeting.iappcontentstagesharingcapabilities) |

## <a name="share-app-content-to-stage-api"></a>Partager le contenu de l’application pour mettre en scène l’API

L’API `shareAppContentToStage` vous permet de partager des parties spécifiques de votre application à la phase de réunion. L’API est disponible via le SDK client Teams.

### <a name="prerequisite"></a>Conditions préalables

* Pour utiliser l’API `shareAppContentToStage` , vous devez obtenir les autorisations RSC. Dans le manifeste de l’application, configurez la `authorization` propriété `name`et le `type` champ`resourceSpecific`. Par exemple :

    ```json
    "authorization": {
        "permissions": { 
        "resourceSpecific": [
        { 
         "name": "MeetingStage.Write.Chat",
         "type": "Delegated"
        }
        ]
    }
    }
    ```

* `appContentUrl` doit être autorisé par `validDomains` le tableau à l’intérieur de manifest.json, sinon l’API retourne une erreur 501.

### <a name="query-parameter"></a>Paramètre de requête

Le tableau ci-dessous décrit chaque paramètre de chaîne de requête.

|Valeur|Type|Requis|Description|
|---|---|----|---|
|**callback**| Chaîne | Oui | Le rappel contient deux paramètres, l’erreur et le résultat. *L’erreur* peut contenir une erreur de type *SdkError* ou null lorsque le partage réussit. Le *résultat* peut contenir une valeur true, en cas de partage réussi, ou null en cas d’échec du partage. |
|**appContentURL**| Chaîne | Oui | URL qui sera partagée sur la scène. |

### <a name="example"></a>Exemple

```javascript
const appContentUrl = "https://www.bing.com/";

microsoftTeams.meeting.shareAppContentToStage((err, result) => {
    if (result) {
        // handle success
    }
    if (err) {
        // handle error
    }
}, appContentUrl);
```

### <a name="response-codes"></a>Codes de réponse

Le tableau suivant présente les codes de réponse :

|Code de réponse|Description|
|---|---|
| **500** | Erreur interne. |
| **501** | L’API n’est pas prise en charge dans le contexte actuel.|
| **1 000** | L’application ne dispose pas des autorisations appropriées pour autoriser le partage à être mis en scène.|

## <a name="get-app-content-stage-sharing-state-api"></a>Obtenir l’API d’état de partage de l’étape de contenu de l’API

L’API `getAppContentStageSharingState` vous permet d’extraire des informations sur le partage d’applications lors de la phase de réunion.

### <a name="query-parameter"></a>Paramètre de requête

Le tableau suivant inclut le paramètre de requête :

|Valeur|Type|Requis|Description|
|---|---|----|---|
|**callback**| Chaîne | Oui | Le rappel contient deux paramètres, l’erreur et le résultat. *L’erreur* peut contenir une erreur de type *SdkError*, en cas d’erreur, ou null lorsque le partage réussit. Le *résultat* peut contenir un `IAppContentStageSharingState` objet, lorsque le partage est réussi, ou null, en cas d’erreur.|

### <a name="example"></a>Exemple

```javascript
microsoftTeams.meeting.getAppContentStageSharingState((err, result) => {
    if (result.isAppSharing) {
        // Indicates if app is sharing content on the meeting stage.
    }
});
```

Le corps de la réponse JSON pour l’API `getAppContentStageSharingState` est le suivant :

```json
{
   "isAppSharing":true
} 
```

### <a name="response-codes"></a>Codes de réponse

Le tableau suivant présente les codes de réponse :

|Code de réponse|Description|
|---|---|
| **500** | Erreur interne. |
| **501** | L’API n’est pas prise en charge dans le contexte actuel.|
| **1 000** | L’application ne dispose pas des autorisations appropriées pour autoriser le partage à être mis en scène.|

## <a name="get-app-content-stage-sharing-capabilities-api"></a>Obtenir l'API des capacités de partage du contenu de l'application

L’API `getAppContentStageSharingCapabilities` vous permet d’extraire les fonctionnalités de l’application pour le partage dans la phase de réunion.

### <a name="query-parameter"></a>Paramètre de requête

Le tableau suivant inclut le paramètre de requête :

|Valeur|Type|Requis|Description|
|---|---|----|---|
|**callback**| Chaîne | Oui | Le rappel contient deux paramètres, l’erreur et le résultat. *L’erreur* peut contenir une erreur de type *SdkError* ou null lorsque le partage réussit. Le résultat peut contenir un `IAppContentStageSharingCapabilities` objet, lorsque le partage est réussi, ou null, en cas d’erreur.|

### <a name="example"></a>Exemple

```javascript
microsoftTeams.meeting.getAppContentStageSharingCapabilities((err, result) => {
    if (result.doesAppHaveSharePermission) {
        // Indicates app has permission to share contents to meeting stage.
    }
});
```

Le corps de la réponse JSON pour `getAppContentStageSharingCapabilities` l’API est le suivant :

```json
{
   "doesAppHaveSharePermission":true
} 
```

### <a name="response-codes"></a>Codes de réponse

Le tableau suivant présente les codes de réponse :

|Code de réponse|Description|
|---|---|
| **500** | Erreur interne. |
| **501** | L’API n’est pas prise en charge dans le contexte actuel.|
| **1 000** | L’application ne dispose pas des autorisations nécessaires pour autoriser le partage à être mis en scène.|

## <a name="generate-a-deep-link-to-share-content-to-stage-in-meetings"></a>Générer un lien profond pour partager du contenu à mettre en scène dans les réunions

Vous pouvez également générer un lien profond pour partager l’application afin de mettre en scène et de démarrer ou de participer à une réunion.

> [!NOTE]
>
> * Actuellement, le lien profond vers le partage de contenu pour effectuer des étapes dans les réunions fait l’objet d’améliorations de l’expérience utilisateur et n’est disponible qu’en [préversion publique des développeurs](~/resources/dev-preview/developer-preview-intro.md).
> * Le lien profond permettant de partager du contenu vers une phase de réunion est pris en charge uniquement dans le client de bureau Teams.

Lorsqu’un lien profond est sélectionné dans une application par un utilisateur qui fait partie d’une réunion en cours, l’application est partagée à l’étape et une fenêtre contextuelle d’autorisation s’affiche. Les utilisateurs peuvent accorder l’accès aux participants pour collaborer avec une application.

:::image type="content" source="../assets/images/intergrate-with-teams/screenshot-of-pop-up-permission.png" alt-text="La capture d’écran est un exemple montrant une fenêtre contextuelle d’autorisation.":::

Lorsqu’un utilisateur ne participe pas à une réunion, il est redirigé vers le calendrier Teams où il peut participer à une réunion ou lancer une réunion instantanée (Réunion maintenant).

:::image type="content" source="../assets/images/intergrate-with-teams/Instant-meetnow-pop-up.png" alt-text="La capture d’écran est un exemple montrant une fenêtre contextuelle lorsqu’il n’y a pas de réunion en cours.":::

Une fois que l’utilisateur a lancé une réunion instantanée (Réunion maintenant), il peut ajouter des participants et interagir avec l’application.

:::image type="content" source="../assets/images/intergrate-with-teams/Screenshot-ofmeet-now-option-pop-up.png" alt-text="La capture d’écran est un exemple qui montre une option pour ajouter des participants et comment interagir avec l’application.":::

Pour ajouter un lien profond pour partager du contenu sur scène, vous devez disposer d’un contexte d’application. Le contexte d’application permet au client Teams d’extraire le manifeste de l’application et de vérifier si le partage sur scène est possible. Voici un exemple de contexte d’application.

`{ "appSharingUrl" : "https://teams.microsoft.com/extensibility-apps/meetingapis/view", "appId": "9ec80a73-1d41-4bcb-8190-4b9eA9e29fbb" , "useMeetNow": false }`

Les paramètres de requête pour le contexte d’application sont les suivants :

* `appID`: il s’agit de l’ID qui peut être obtenu à partir du manifeste de l’application.
* `appSharingUrl`: l’URL qui doit être partagée sur scène doit être un domaine valide défini dans le manifeste de l’application. Si l’URL n’est pas un domaine valide, une boîte de dialogue d’erreur s’affiche pour fournir à l’utilisateur une description de l’erreur.
* `useMeetNow`: cela inclut un paramètre booléen qui peut être vrai ou faux.
  * **True** : lorsque la `UseMeetNow` valeur est true et s’il n’y a pas de réunion en cours, une nouvelle réunion De réunion maintenant est lancée. Quand une réunion est en cours, cette valeur est ignorée.

  * **False** : la valeur `UseMeetNow` par défaut est false, ce qui signifie que lorsqu’un lien profond est partagé vers une phase et qu’il n’y a pas de réunion en cours, une fenêtre contextuelle de calendrier s’affiche. Toutefois, vous pouvez partager directement pendant une réunion.

Vérifiez que tous les paramètres de requête sont correctement encodés en URI et que le contexte de l’application doit être encodé deux fois dans l’URL finale. Voici un exemple :

```json
var appContext= JSON.stringify({ "appSharingUrl" : "https://teams.microsoft.com/extensibility-apps/meetingapis/view", "appId": "9cc80a93-1d41-4bcb-8170-4b9ec9e29fbb", "useMeetNow":false })
var encodedContext = encodeURIComponent(appcontext).replace(/'/g,"%27").replace(/"/g,"%22")
var encodedAppContext = encodeURIComponent(encodedContext).replace(/'/g,"%27").replace(/"/g,"%22")
```

Un lien profond peut être lancé à partir du web Teams ou du client de bureau Teams.

* **Web Teams** : utilisez le format suivant pour lancer un lien profond à partir du site web Teams pour partager du contenu sur scène.

    `https://teams.microsoft.com/l/meeting-share?deeplinkId={deeplinkid}&fqdn={fqdn}}&lm=deeplink%22&appContext={encoded app context}`

    Exemple : `https://teams.microsoft.com/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`

    |Lien profond|Format|Exemple|
    |---------|---------|---------|
    |Pour partager l’application et ouvrir le calendrier Teams, lorsque UseMeeetNow a la **valeur false**, par défaut.|`https://teams.microsoft.com/l/meeting-share?deeplinkId={deeplinkid}&fqdn={fqdn}}&lm=deeplink%22&appContext={encoded app context}`|`https://teams.microsoft.com/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Afalse%257D`|
    |Pour partager l’application et lancer une réunion instantanée, lorsque UseMeeetNow a **la valeur true**.|`https://teams.microsoft.com/l/meeting-share?deeplinkId={deeplinkid}&fqdn={fqdn}}&lm=deeplink%22&appContext={encoded app context}`|`https://teams.microsoft.com/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`|

* **Client de bureau d’équipe** : utilisez le format suivant pour lancer un lien profond à partir du client de bureau Teams pour partager du contenu sur scène.

    `msteams:/l/meeting-share?   deeplinkId={deeplinkid}&fqdn={fqdn}&lm=deeplink%22&appContext={encoded app context}`

    Exemple : `msteams:/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`

    |Lien profond|Format|Exemple|
    |---------|---------|---------|
    |Pour partager l’application et ouvrir le calendrier Teams, lorsque UseMeeetNow a la **valeur false**, par défaut.|`msteams:/l/meeting-share?   deeplinkId={deeplinkid}&fqdn={fqdn}&lm=deeplink%22&appContext={encoded app context}`|`msteams:/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Afalse%257D`|
    |Pour partager l’application et lancer une réunion instantanée, lorsque UseMeeetNow a **la valeur true**.|`msteams:/l/meeting-share?   deeplinkId={deeplinkid}&fqdn={fqdn}&lm=deeplink%22&appContext={encoded app context}`|`msteams:/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`|

Les paramètres de requête sont les suivants :

* `deepLinkId`: tout identificateur utilisé pour la corrélation de télémétrie.
* `fqdn`: `fqdn` est un paramètre facultatif, qui peut être utilisé pour basculer vers un environnement approprié d’une réunion pour partager une application sur scène. Il prend en charge les scénarios dans lesquels un partage d’application spécifique se produit dans un environnement particulier. La valeur par défaut est l’URL d’entreprise `fqdn` et les valeurs possibles sont `Teams.live.com` pour Teams for Life, `teams.microsoft.com`ou `teams.microsoft.us`.

Pour partager l’intégralité de l’application à l’étape, dans le manifeste de l’application, vous devez configurer `meetingStage` et `meetingSidePanel` , en tant que contextes d’image, voir [le manifeste de l’application](../resources/schema/manifest-schema.md). Dans le cas contraire, les participants à la réunion peuvent ne pas être en mesure de voir le contenu sur scène.

> [!NOTE]
> Pour que votre application réussisse la validation, lorsque vous créez un lien profond à partir de votre site web, de votre application web ou de votre carte adaptative, utilisez **Share in meeting** comme chaîne ou copie.

## <a name="code-sample"></a>Exemple de code

|Exemple de nom | Description | C# | Node.js |
|----------------|-----------------|--------------|----------------|
|Exemple de phase de réunion | Exemple d’application pour afficher un onglet dans la phase de réunion pour la collaboration | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/nodejs) |
| Notification en réunion | Montre comment implémenter une notification en réunion à l’aide du bot. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs) |
| Signature de document en réunion | Montre comment implémenter une application Teams de signature de document. Inclut le partage de contenu d’application spécifique à l’étape, l’authentification unique Teams et la vue d’étape spécifique à l’utilisateur. | [View](https://github.com/officedev/microsoft-teams-samples/tree/main/samples/meetings-share-to-stage-signing/csharp) | N/A |

## <a name="see-also"></a>Voir aussi

* [Flux d’authentification Teams pour les onglets](../tabs/how-to/authentication/auth-flow-tab.md)
* [Applications pour les réunions Teams](teams-apps-in-meetings.md)
* [Créer des onglets pour la réunion](build-tabs-for-meeting.md)
* [Créer une conversation extensible pour la conversation de réunion](build-extensible-conversation-for-meeting-chat.md)
* [Créer des applications pour les utilisateurs anonymes](build-apps-for-anonymous-user.md)
* [API de réunion avancées](meeting-apps-apis.md)
* [Scènes personnalisées du mode ensemble](~/apps-in-teams-meetings/teams-together-mode.md)
* [FAQ sur le Kit de développement logiciel (SDK) de Live Share](teams-live-share-overview.md)
