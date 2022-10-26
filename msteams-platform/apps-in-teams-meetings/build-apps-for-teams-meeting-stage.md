---
title: Créer des applications pour la phase de réunion Teams
author: v-sdhakshina
description: Découvrez comment créer des applications pour la phase de réunion Teams, partager à étape et générer un lien profond pour partager du contenu dans une phase de réunion.
ms.topic: conceptual
ms.author: v-sdhakshina
ms.localizationpriority: medium
ms.date: 04/07/2022
ms.openlocfilehash: 48834addceb0e7a6e4522c096cf40b117312647c
ms.sourcegitcommit: 372aade09e62ac7e5936215173a6632fbb042c9d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/26/2022
ms.locfileid: "68699137"
---
# <a name="build-apps-for-teams-meeting-stage"></a>Créer des applications pour la phase de réunion Teams

Partager à la phase permet aux utilisateurs de partager une application avec la phase de réunion à partir du panneau latéral de la réunion dans une réunion en cours. Ce partage est interactif et collaboratif par rapport au partage d’écran passif.

Pour appeler le partage à la phase, les utilisateurs peuvent sélectionner l’icône **Partager sur scène** en haut à droite du panneau latéral de la réunion. **L’icône Partager à la phase** est native du client Teams et sa sélection partage l’ensemble de l’application à la phase de réunion.

## <a name="app-manifest-settings-for-apps-in-meeting-stage"></a>Paramètres du manifeste d’application pour les applications en phase de réunion

Pour partager une application avec la phase de réunion, mettez à jour la `context` propriété dans le manifeste de l’application comme suit :

```json
"context":[ 
    "meetingSidePanel", 
    "meetingStage" 
     ] 
```

## <a name="advanced-share-to-stage-apis"></a>API avancées de partage à phase

Il existe de nombreux scénarios où le partage de l’ensemble de l’application à la phase de réunion n’est pas aussi utile que le partage de parties spécifiques de l’application :  

1. Pour une application de brainstorming ou de tableau blanc, un utilisateur peut souhaiter partager un tableau spécifique dans une réunion par rapport à l’ensemble de l’application avec tous les tableaux.  

1. Pour une application médicale, un médecin peut souhaiter partager uniquement la radiographie à l’écran avec le patient, au lieu de partager l’ensemble de l’application avec tous les dossiers ou résultats des patients, etc.

1. Un utilisateur peut souhaiter partager du contenu à partir d’un seul fournisseur de contenu à la fois (par exemple, YouTube) au lieu de partager un catalogue vidéo entier sur scène.

Pour aider les utilisateurs dans de tels scénarios, nous avons publié des API dans le Kit de développement logiciel (SDK) client Teams, qui vous permet d’appeler par programmation le partage pour des parties spécifiques de l’application à partir d’un bouton dans le panneau latéral de la réunion.

:::image type="content" source="../assets/images/apps-in-meetings/shared-meeting-stage-edit-review-component.png" alt-text="La capture d’écran montre l’affichage de la phase de partage à la réunion.":::

Utilisez les API suivantes pour partager une partie spécifique de l’application :

|Méthode| Description| Source|
|---|---|----|
|[**Partager le contenu de l’application à l’étape**](#share-app-content-to-stage-api)| Partagez des parties spécifiques de l’application à la phase de réunion à partir du panneau latéral de la réunion dans une réunion. | [Kit de développement logiciel (SDK) de la bibliothèque JavaScript Microsoft Teams](/javascript/api/@microsoft/teams-js/meeting) |
|[**Obtenir l’état de partage de la phase de contenu de l’application**](#get-app-content-stage-sharing-state-api)| Récupérez des informations sur l’état de partage de l’application lors de la phase de réunion. | [Kit de développement logiciel (SDK) de la bibliothèque JavaScript Microsoft Teams](/javascript/api/@microsoft/teams-js/meeting.iappcontentstagesharingstate) |
|[**Obtenir les fonctionnalités de partage de phase de contenu d’application**](#get-app-content-stage-sharing-capabilities-api)| Récupérez les fonctionnalités de l’application pour le partage dans la phase de réunion. | [Kit de développement logiciel (SDK) de la bibliothèque JavaScript Microsoft Teams](/javascript/api/@microsoft/teams-js/meeting.iappcontentstagesharingcapabilities) |

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

* `appContentUrl` doit être autorisé par `validDomains` array dans manifest.json, sinon l’API retourne une erreur 501.

### <a name="query-parameter"></a>Paramètre de requête

Le tableau ci-dessous décrit chaque paramètre de chaîne de requête.

|Valeur|Type|Requis|Description|
|---|---|----|---|
|**callback**| Chaîne | Oui | Le rappel contient deux paramètres, l’erreur et le résultat. *L’erreur* peut contenir une erreur de type *SdkError* ou null lorsque le partage réussit. Le *résultat* peut contenir une valeur true, si un partage a réussi, ou null en cas d’échec du partage. |
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
| **1 000** | L’application ne dispose pas des autorisations appropriées pour autoriser le partage à mettre en scène.|

## <a name="get-app-content-stage-sharing-state-api"></a>Obtenir l’API d’état de partage de l’étape de contenu de l’API

L’API `getAppContentStageSharingState` vous permet d’extraire des informations sur le partage d’applications sur la phase de réunion.

### <a name="query-parameter"></a>Paramètre de requête

Le tableau suivant inclut le paramètre de requête :

|Valeur|Type|Requis|Description|
|---|---|----|---|
|**callback**| Chaîne | Oui | Le rappel contient deux paramètres, erreur et résultat. *L’erreur* peut contenir une erreur de type *SdkError*, en cas d’erreur, ou null lorsque le partage réussit. Le *résultat* peut contenir un `IAppContentStageSharingState` objet, lorsque le partage réussit, ou null, en cas d’erreur.|

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
| **1 000** | L’application ne dispose pas des autorisations appropriées pour autoriser le partage à mettre en scène.|

## <a name="get-app-content-stage-sharing-capabilities-api"></a>Obtenir l'API des capacités de partage du contenu de l'application

L’API `getAppContentStageSharingCapabilities` vous permet d’extraire les fonctionnalités de l’application pour le partage dans la phase de réunion.

### <a name="query-parameter"></a>Paramètre de requête

Le tableau suivant inclut le paramètre de requête :

|Valeur|Type|Requis|Description|
|---|---|----|---|
|**callback**| Chaîne | Oui | Le rappel contient deux paramètres, erreur et résultat. *L’erreur* peut contenir une erreur de type *SdkError* ou null lorsque le partage réussit. Le résultat peut contenir un `IAppContentStageSharingCapabilities` objet, lorsque le partage réussit, ou null, en cas d’erreur.|

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
| **1 000** | L’application ne dispose pas des autorisations nécessaires pour autoriser le partage à mettre en scène.|

## <a name="generate-a-deep-link-to-share-content-to-stage-in-meetings"></a>Générer un lien profond pour partager du contenu à l’étape des réunions

Vous pouvez également générer un lien profond pour partager l’application pour mettre en scène et démarrer ou rejoindre une réunion.

> [!NOTE]
>
> * Actuellement, le lien profond permettant de partager du contenu dans les réunions fait l’objet d’améliorations de l’expérience utilisateur et n’est disponible que dans la [préversion publique pour les développeurs](~/resources/dev-preview/developer-preview-intro.md).
> * Le lien profond permettant de partager du contenu en phase de réunion est pris en charge uniquement dans le client de bureau Teams.

Lorsqu’un lien profond est sélectionné dans une application par un utilisateur qui fait partie d’une réunion en cours, l’application est partagée sur la scène et une fenêtre contextuelle d’autorisation s’affiche. Les utilisateurs peuvent accorder l’accès aux participants pour collaborer avec une application.

:::image type="content" source="../assets/images/intergrate-with-teams/screenshot-of-pop-up-permission.png" alt-text="La capture d’écran est un exemple montrant une fenêtre contextuelle d’autorisation.":::

Lorsqu’un utilisateur ne participe pas à une réunion, l’utilisateur est redirigé vers le calendrier Teams où il peut rejoindre une réunion ou lancer une réunion instantanée (Réunion maintenant).

:::image type="content" source="../assets/images/intergrate-with-teams/Instant-meetnow-pop-up.png" alt-text="La capture d’écran est un exemple qui montre une fenêtre contextuelle lorsqu’il n’y a pas de réunion en cours.":::

Une fois que l’utilisateur lance une réunion instantanée (Réunion maintenant), il peut ajouter des participants et interagir avec l’application.

:::image type="content" source="../assets/images/intergrate-with-teams/Screenshot-ofmeet-now-option-pop-up.png" alt-text="La capture d’écran est un exemple qui montre une option permettant d’ajouter des participants et comment interagir avec l’application.":::

Pour ajouter un lien profond afin de partager du contenu sur scène, vous devez disposer d’un contexte d’application. Le contexte de l’application permet au client Teams d’extraire le manifeste de l’application et de vérifier si le partage sur scène est possible. Voici un exemple de contexte d’application.

`{ "appSharingUrl" : "https://teams.microsoft.com/extensibility-apps/meetingapis/view", "appId": "9ec80a73-1d41-4bcb-8190-4b9eA9e29fbb" , "useMeetNow": false }`

Les paramètres de requête pour le contexte de l’application sont les suivants :

* `appID`: il s’agit de l’ID qui peut être obtenu à partir du manifeste de l’application.
* `appSharingUrl`: l’URL qui doit être partagée sur scène doit être un domaine valide défini dans le manifeste de l’application. Si l’URL n’est pas un domaine valide, une boîte de dialogue d’erreur s’affiche pour fournir à l’utilisateur une description de l’erreur.
* `useMeetNow`: cela inclut un paramètre booléen qui peut être true ou false.
  * **True** : lorsque la `UseMeetNow` valeur est true et s’il n’y a pas de réunion en cours, une nouvelle réunion Meet now est lancée. En cas de réunion en cours, cette valeur est ignorée.

  * **False** : la valeur par défaut de `UseMeetNow` est false, ce qui signifie que lorsqu’un lien profond est partagé vers la phase et qu’il n’y a pas de réunion en cours, une fenêtre contextuelle de calendrier s’affiche. Toutefois, vous pouvez partager directement au cours d’une réunion.

Vérifiez que tous les paramètres de requête sont correctement encodés dans l’URI et que le contexte de l’application doit être codé deux fois dans l’URL finale. Voici un exemple :

```json
var appContext= JSON.stringify({ "appSharingUrl" : "https://teams.microsoft.com/extensibility-apps/meetingapis/view", "appId": "9cc80a93-1d41-4bcb-8170-4b9ec9e29fbb", "useMeetNow":false })
var encodedContext = encodeURIComponent(appcontext).replace(/'/g,"%27").replace(/"/g,"%22")
var encodedAppContext = encodeURIComponent(encodedContext).replace(/'/g,"%27").replace(/"/g,"%22")
```

Un lien profond peut être lancé à partir du web Teams ou du client de bureau Teams.

* **Web Teams** : utilisez le format suivant pour lancer un lien profond à partir du web Teams afin de partager du contenu sur scène.

    `https://teams.microsoft.com/l/meeting-share?deeplinkId={deeplinkid}&fqdn={fqdn}}&lm=deeplink%22&appContext={encoded app context}`

    Exemple : `https://teams.microsoft.com/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`

    |Lien profond|Format|Exemple|
    |---------|---------|---------|
    |Pour partager l’application et ouvrir le calendrier Teams, lorsque UseMeeetNow a la valeur **false**, valeur par défaut.|`https://teams.microsoft.com/l/meeting-share?deeplinkId={deeplinkid}&fqdn={fqdn}}&lm=deeplink%22&appContext={encoded app context}`|`https://teams.microsoft.com/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Afalse%257D`|
    |Pour partager l’application et lancer une réunion instantanée, lorsque UseMeeetNow a la **valeur true**.|`https://teams.microsoft.com/l/meeting-share?deeplinkId={deeplinkid}&fqdn={fqdn}}&lm=deeplink%22&appContext={encoded app context}`|`https://teams.microsoft.com/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`|

* **Client de bureau d’équipe** : utilisez le format suivant pour lancer un lien profond à partir du client de bureau Teams afin de partager du contenu sur scène.

    `msteams:/l/meeting-share?   deeplinkId={deeplinkid}&fqdn={fqdn}&lm=deeplink%22&appContext={encoded app context}`

    Exemple : `msteams:/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`

    |Lien profond|Format|Exemple|
    |---------|---------|---------|
    |Pour partager l’application et ouvrir le calendrier Teams, lorsque UseMeeetNow a la valeur **false**, valeur par défaut.|`msteams:/l/meeting-share?   deeplinkId={deeplinkid}&fqdn={fqdn}&lm=deeplink%22&appContext={encoded app context}`|`msteams:/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Afalse%257D`|
    |Pour partager l’application et lancer une réunion instantanée, lorsque UseMeeetNow a la **valeur true**.|`msteams:/l/meeting-share?   deeplinkId={deeplinkid}&fqdn={fqdn}&lm=deeplink%22&appContext={encoded app context}`|`msteams:/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`|

Les paramètres de requête sont les suivants :

* `deepLinkId`: identificateur utilisé pour la corrélation de télémétrie.
* `fqdn`: `fqdn` est un paramètre facultatif, qui peut être utilisé pour basculer vers un environnement approprié d’une réunion pour partager une application sur scène. Il prend en charge les scénarios où un partage d’application spécifique se produit dans un environnement particulier. La valeur par défaut de est l’URL d’entreprise `fqdn` et les valeurs possibles sont `Teams.live.com` pour Teams for Life, `teams.microsoft.com`ou `teams.microsoft.us`.

Pour partager l’ensemble de l’application à l’étape, dans le manifeste de l’application, vous devez configurer `meetingStage` et `meetingSidePanel` en tant que contextes de trame, consultez [manifeste de l’application](../resources/schema/manifest-schema.md). Dans le cas contraire, les participants à la réunion risquent de ne pas être en mesure de voir le contenu sur scène.

> [!NOTE]
> Pour que votre application réussisse la validation, lorsque vous créez un lien profond à partir de votre site web, application web ou carte adaptative, utilisez **Partager en réunion** comme chaîne ou copie.

## <a name="build-an-in-meeting-document-signing-app"></a>Créer une application de signature de document en réunion

Vous pouvez créer une application en réunion pour permettre aux participants à la réunion de connecter des documents en temps réel. Il facilite l’examen et la signature de documents en une seule session. Les participants peuvent signer les documents à l’aide de leur identité de locataire actuelle.

Vous pouvez utiliser une application de signature en réunion pour :

- Ajouter des documents à réviser pendant une réunion
- Partager des documents à réviser à l’étape principale
- Signer des documents à l’aide de l’identité du signataire

Les participants peuvent consulter et signer des documents, tels que des contrats d’achat et des bons de commande.

![Application de signature de document en réunion](~/assets//images/sbs-inmeeting-doc-signing/signing-clip.gif)

Les rôles de participants suivants peuvent être impliqués pendant la réunion :

- **Créateur de** documents : ce rôle peut ajouter ses propres documents à réviser et à signer.
- **Signataire** : ce rôle peut signer des documents révisés.
- **Lecteur** : ce rôle peut afficher les documents ajoutés à la réunion.

## <a name="code-sample"></a>Exemple de code

|Exemple de nom | Description | C# | Node.js |
|----------------|-----------------|--------------|----------------|
|Exemple de phase de réunion | Exemple d’application pour afficher un onglet dans la phase de réunion pour la collaboration | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/nodejs) |
| Notification en réunion | Montre comment implémenter la notification en réunion à l’aide d’un bot. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs) |
| Signature de documents en réunion | Montre comment implémenter une application Teams de signature de document. Inclut le partage de contenu d’application spécifique à la phase, l’authentification unique Teams et la vue de phase spécifique à l’utilisateur. | [View](https://github.com/officedev/microsoft-teams-samples/tree/main/samples/meetings-share-to-stage-signing/csharp) | N/A |

## <a name="step-by-step-guide"></a>Guide pas à pas

Suivez le [guide pas à pas](../sbs-inmeeting-document-signing.yml) pour créer une application de signature de document en réunion.

## <a name="see-also"></a>Voir aussi

* [Flux d’authentification Teams pour les onglets](../tabs/how-to/authentication/auth-flow-tab.md)
* [Applications pour les réunions Teams](teams-apps-in-meetings.md)
* [Onglets générer pour la réunion](build-tabs-for-meeting.md)
* [Créer une conversation extensible pour la conversation de réunion](build-extensible-conversation-for-meeting-chat.md)
* [Créer des applications pour les utilisateurs anonymes](build-apps-for-anonymous-user.md)
* [API de réunion avancées](meeting-apps-apis.md)
* [Scènes personnalisées du mode ensemble](~/apps-in-teams-meetings/teams-together-mode.md)
* [FAQ sur le Kit de développement logiciel (SDK) de Live Share](teams-live-share-overview.md)
* [Guide pas à pas pour créer une application de signature de document en réunion](../sbs-inmeeting-document-signing.yml)
