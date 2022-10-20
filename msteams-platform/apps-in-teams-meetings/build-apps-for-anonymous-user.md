---
title: Créer des applications pour un utilisateur anonyme
author: v-sdhakshina
description: Découvrez comment créer des applications pour les utilisateurs anonymes et tester l’expérience fournie aux utilisateurs anonymes dans les applications de réunion avec tous les paramètres d’administration.
ms.topic: conceptual
ms.author: v-sdhakshina
ms.localizationpriority: medium
ms.openlocfilehash: ff897c5135740557e12898e7e5d231557b2e2823
ms.sourcegitcommit: 40d4bde10b6820c62e49e2400b10ab3569c8c815
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/20/2022
ms.locfileid: "68615418"
---
# <a name="build-apps-for-anonymous-users"></a>Créer des applications pour les utilisateurs anonymes

Vous pouvez créer des bots, des extensions de messagerie, des cartes et des modules de tâches dans votre application pour interagir avec des participants anonymes à la réunion.

Pour tester l’expérience de votre application pour les utilisateurs anonymes, sélectionnez l’URL dans l’invitation à la réunion et rejoignez la réunion à partir d’une fenêtre de navigateur privé.

## <a name="admin-setting-for-anonymous-user-app-interaction"></a>paramètre Administration pour l’interaction avec l’application utilisateur anonyme

Les administrateurs Teams peuvent utiliser le portail d’administration pour activer ou désactiver l’interaction d’application utilisateur anonyme pour l’ensemble du locataire. Ce paramètre est activé par défaut. Pour plus d’informations, consultez [Autoriser les utilisateurs anonymes à interagir avec les applications dans les réunions](/microsoftteams/meeting-settings-in-teams).

## <a name="in-meeting-getcontext-from-teams-client-sdk"></a>In-Meeting getContext à partir du Kit de développement logiciel (SDK) client Teams

Les applications reçoivent les informations suivantes pour un utilisateur anonyme lorsqu’elles appellent l’API `getContext` à partir de la phase d’application partagée. Vous pouvez reconnaître les utilisateurs anonymes en vérifiant la `userLicenseType` valeur **Inconnu**.

```csharp
"userObjectId": "8:anon:<GUID1>",
"userLicenseType": "Unknown",
"loginHint": "8:teamsvisitor:<ID>",
"userPrincipalName": "8:teamsvisitor:<ID>",
"tid": "<meeting organizer tenant ID>"
```

| **Nom de la propriété** | **Description** |
| --- | --- |
| `userObjectId` | Valeur générée unique pour l’utilisateur anonyme. Cette valeur ne peut pas être utilisée dans les appels aux API Graph. |
| `userLicenseType` | `Unknown`, représente l’utilisateur anonyme. |
| `loginHint` | Valeur générée unique. Cette valeur ne peut pas être utilisée comme indicateur dans les flux de connexion. |
| `userPrincipalName` | Valeur générée unique. Cette valeur ne peut pas être utilisée dans les appels aux API Graph. |
| `tid` | ID de locataire de l’organisateur de la réunion. |

> [!NOTE]
> Lorsqu’un utilisateur anonyme rejoint une réunion, un nouvel ID d’utilisateur est généré. Chaque fois que l’utilisateur anonyme rejoint à nouveau une réunion, un autre ID d’utilisateur est généré.

## <a name="bot-activities-and-apis"></a>Activités et API de bot

Avec quelques différences, les activités envoyées à votre bot et les réponses qu’il reçoit des API de bot sont cohérentes entre les participants aux réunions anonymes et non anonymes. En général :

* L’ID d’utilisateur est une valeur générée qui est différente chaque fois que l’utilisateur anonyme rejoint la réunion.
* La `aadObjectId` propriété est omise.
* La `userRole` propriété est définie sur **anonyme**.
* L’ID de locataire fourni est défini sur l’ID de locataire de l’organisateur de la réunion.

### <a name="get-members-and-get-single-member-apis"></a>Obtenir des membres et obtenir des API à membre unique

[L’obtention de membres](/microsoftteams/platform/bots/how-to/get-teams-context#fetch-the-roster-or-user-profile) et l’obtention d’API [à membre unique](/microsoftteams/platform/bots/how-to/get-teams-context#get-single-member-details) retournent des informations limitées pour les utilisateurs anonymes :

```json
{ 
  "id": "<GUID1>", 
  "name": "<AnonTest (Guest)>",  
  "tenantId": "<GUID2>", 
  "userRole": "anonymous" 
} 
```

| **Nom de la propriété** | **Description** |
| --- | --- |
| `id` | Valeur générée unique pour l’utilisateur anonyme. |
| `name` | Nom fourni par l’utilisateur anonyme lors de la participation à la réunion. |
| `tenantId` | ID de locataire de l’organisateur de la réunion. |
| `userRole` | `anonymous`, représente l’utilisateur anonyme. |

> [!NOTE]
> L’ID reçu des API de bot et de l’API du Kit de développement logiciel (SDK) client Teams n’est pas le même.

### <a name="conversationupdate-activity-membersadded-and-membersremoved"></a>Activité ConversationUpdate MembersAdded et MembersRemoved

```csharp
{ 
  "membersAdded": [ 
    { 
      "id": "<GUID1>" 
    } 
  ], 
  "type": "conversationUpdate", 
  "timestamp": "<timestamp>", 
  "id": "<event unique identifier>", 
  "channelId": "msteams", 
  "serviceUrl": "<serviceURL>", 
  "from": { 
    "id": "<GUID2>" 
  }, 
  "conversation": { 
    "isGroup": true, 
    "tenantId": "<tenant id>", 
    "id": "<conversation id>" 
  }, 
  "recipient": { 
    "id": "<bot id>", 
    "name": "<bot name>" 
  }, 
  "channelData": { 
    "tenant": { 
      "id": "<tenant id>" 
    }, 
    "source": null, 
    "meeting": { 
      "id": "<meeting id>" 
    } 
  } 
} 
```

| **Nom de la propriété** | **Description** |
| --- | --- |
| `membersAdded.id` | ID d’utilisateur anonyme. |
| `from.id` | ID de l’organisateur de la réunion. |
| `conversation.tenantId` | ID de locataire de l’organisateur de la réunion. |
| `conversation.id` | ID de conversation de la conversation de réunion. |
| `tenant.id` | ID de locataire de l’organisateur de la réunion. |

Des modifications similaires s’appliquent à la charge utile d’activité `membersRemoved` .

> [!NOTE]
>
> Lorsqu’un utilisateur anonyme rejoint ou quitte une réunion, l’objet `from` de la charge utile a toujours l’ID de l’organisateur de la réunion, même si l’action a été effectuée par une autre personne.

### <a name="create-conversation-api"></a>Créer une API conversationnelle

Les bots ne sont pas autorisés à lancer une conversation un-à-un avec un utilisateur anonyme. Si un bot appelle l’API Créer une conversation avec l’ID d’utilisateur d’un utilisateur anonyme, il reçoit un code d’état `400` de demande incorrecte et la réponse d’erreur suivante :

```csharp
{ 
  "error": {
    "code": "BadArgument",
    "message": "Bot cannot create a conversation with an anonymous user"
  }
} 
```

### <a name="adaptive-cards"></a>Cartes adaptatives

Les utilisateurs anonymes peuvent afficher et interagir avec les cartes adaptatives dans la conversation de réunion. Les actions de carte adaptative se comportent de la même façon pour les utilisateurs anonymes et non anonymes. Pour plus d’informations, consultez [Actions de carte](/microsoftteams/platform/task-modules-and-cards/cards/cards-actions?tabs=json).

## <a name="known-issues-and-limitations"></a>Problèmes connus et conseils

* Les onglets de panneau latéral et les bulles de contenu ne sont pas disponibles pour les utilisateurs anonymes. Les utilisateurs anonymes peuvent toujours voir le contenu de l’application partagé à la phase de réunion.

* Pour un utilisateur anonyme, l’ID d’utilisateur `getContext` et l’ID d’utilisateur reçus par le bot sont différents. Il n’est pas possible de mettre en corrélation les deux directement. Si vous devez suivre l’identité de l’utilisateur entre votre onglet et votre bot, vous devez inviter l’utilisateur à s’authentifier auprès d’un fournisseur d’identité externe.

* Les utilisateurs anonymes verront une icône d’application générique sur les messages et les cartes du bot, au lieu de l’icône réelle de l’application. Par exemple :

    :::image type="content" source="../assets/images/apps-in-meetings/app-icon.png" alt-text="Cette capture d’écran montre comment l’icône d’application s’affiche pour un utilisateur anonyme.":::

## <a name="see-also"></a>Voir aussi

* [Créer des applications pour la phase de réunion Teams](build-apps-for-teams-meeting-stage.md)
* [API d’applications de réunion](meeting-apps-apis.md)
* [Fonctionnement des bots Microsoft Teams](/azure/bot-service/bot-builder-basics-teams)
