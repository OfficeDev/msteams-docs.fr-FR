---
title: Utiliser Microsoft Graph pour importer des messages de plateforme externe dans Teams
description: Décrit comment utiliser Microsoft Graph pour importer des messages à partir d’une plateforme externe vers Teams
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: teams import messages api graph microsoft migrate migration post
ms.openlocfilehash: 8cf4f964aba7ce9375b1b259ae88a7fbcb620631
ms.sourcegitcommit: f6e4a303828224a702138753a8e5e27c8a094c82
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/24/2021
ms.locfileid: "51176955"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a>Importer des messages de plateforme tierces pour les équipes à l’aide de Microsoft Graph

>[!IMPORTANT]
> Les prévisualisations publiques de Microsoft Graph et Microsoft Teams sont disponibles pour un accès et des commentaires en avant-première. Bien que cette version ait fait l’objet de tests approfondis, elle n’est pas destinée à être mise en production.

Avec Microsoft Graph, vous pouvez migrer l’historique des messages et les données des utilisateurs d’un système externe vers un canal Teams. En permettant la recréation d’une hiérarchie de messagerie de plateforme tierce au sein de Teams, les utilisateurs peuvent poursuivre leurs communications de manière transparente et sans interruption.

> [!NOTE] 
> À l’avenir, Microsoft pourra exiger que vous ou vos clients payiez des frais supplémentaires en fonction du volume de données importées.

## <a name="import-overview"></a>Vue d’ensemble de l’importation

À un niveau élevé, le processus d’importation se compose des opérations suivantes :

1. [Créer une équipe avec un timestamp de retour dans le temps](#step-one-create-a-team)
1. [Créer un canal avec un timestamp de retour dans le temps](#step-two-create-a-channel)  
1. [Importer des messages obsolètes dans le temps externes](#step-three-import-messages)
1. [Terminer le processus de migration des équipes et des canaux](#step-four-complete-migration-mode)
1. [Ajouter des membres d’équipe](#step-five-add-team-members)

## <a name="necessary-requirements"></a>Conditions requises

### <a name="analyze-and-prepare-message-data"></a>Analyser et préparer les données des messages

✔ examiner les données tierces pour déterminer ce qui sera migré.  
✔ extraire les données sélectionnées du système de conversation tiers.  
✔ la structure de conversation tierce à la structure Teams.  
✔ convertir les données d’importation au format nécessaire pour la migration.  

### <a name="set-up-your-office-365-tenant"></a>Configuration de votre client Office 365

✔ s’assurer qu’un client Office 365 existe pour les données d’importation. Pour plus d’informations sur la configuration d’une location Office 365 pour *Teams,* voir , Préparer votre client [Office 365.](../../concepts/build-and-test/prepare-your-o365-tenant.md)  
✔ assurez-vous que les membres de l’équipe sont dans Azure Active Directory (AAD).  Pour plus *d’informations,* [voir Ajouter un nouvel](/azure/active-directory/fundamentals/add-users-azure-active-directory) utilisateur à Azure Active Directory.

## <a name="step-one-create-a-team"></a>Étape 1 : Créer une équipe

Étant donné que les données existantes sont migrées, il est essentiel de maintenir les timestamps des messages d’origine et d’empêcher l’activité de messagerie pendant le processus de migration pour recréer le flux de messages existant de l’utilisateur dans Teams. Pour ce faire, les résultats sont les suivants :

> [Créez une équipe avec](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) un timestamp de retour dans le temps à l’aide de la propriété de ressource  `createdDateTime`  d’équipe. Placez la nouvelle équipe dans un état spécial qui interdit aux utilisateurs la plupart des activités au sein de l’équipe jusqu’à ce que le processus `migration mode` de migration soit terminé. Incluez `teamCreationMode` l’attribut d’instance avec la valeur dans la requête POST pour identifier explicitement la nouvelle équipe comme étant `migration` créée pour la migration.  

> **REMARQUE**: le champ sera rempli uniquement pour les instances d’une équipe ou d’un canal `createdDateTime` qui ont été migrées.

<!-- markdownlint-disable MD001 -->

#### <a name="permissions"></a>Autorisations

|ScopeName|DisplayName|Description|Type|Consentement de l’administrateur ?|Entités/API couvertes|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|Gérer la migration vers Microsoft Teams|Création, gestion des ressources pour la migration vers Microsoft Teams|**Application uniquement**|**Oui**|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a>Demander (créer une équipe en état de migration)

```http
POST https://graph.microsoft.com/beta/teams

Content-Type: application/json
{
  "@microsoft.graph.teamCreationMode": "migration",
  "template@odata.bind": "https://graph.microsoft.com/beta/teamsTemplates('standard')",
  "displayName": "My Sample Team",
  "description": "My Sample Team’s Description",
  "createdDateTime": "2020-03-14T11:22:17.043Z"
}
```

#### <a name="response"></a>Réponse

```http
HTTP/1.1 202 Accepted
Location: /teams/{teamId}/operations/{operationId}
Content-Location: /teams/{teamId}
```

#### <a name="error-messages"></a>Messages d’erreur

```http
400 Bad Request
```

* `createdDateTime`  définie pour l’avenir.
* `createdDateTime`  correctement spécifié, mais `teamCreationMode`  l’attribut d’instance est manquant ou a une valeur non valide.

## <a name="step-two-create-a-channel"></a>Étape 2 : Créer un canal

La création d’un canal pour les messages importés est similaire au scénario de création d’équipe :

> [Créez un canal avec](/graph/api/channel-post?view=graph-rest-beta&tabs=http&preserve-view=true) un timestamp de retour dans le temps à l’aide de la propriété de ressource `createdDateTime` de canal. Placez le nouveau canal dans , un état spécial qui interdit aux utilisateurs de la plupart des activités de conversation au sein du canal jusqu’à ce que le processus `migration mode` de migration soit terminé.  Incluez `channelCreationMode` l’attribut d’instance avec la valeur dans la requête POST pour identifier explicitement la nouvelle équipe comme `migration` étant créée pour la migration.  
<!-- markdownlint-disable MD024 -->
#### <a name="permissions"></a>Autorisations

|ScopeName|DisplayName|Description|Type|Consentement de l’administrateur ?|Entités/API couvertes|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|Gérer la migration vers Microsoft Teams|Création, gestion des ressources pour la migration vers Microsoft Teams|**Application uniquement**|**Oui**|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a>Demande (créer un canal dans l’état de migration)

```http
POST https://graph.microsoft.com/beta/teams/{id}/channels

Content-Type: application/json
{
  "@microsoft.graph.channelCreationMode": "migration",
  "displayName": "Architecture Discussion",
  "description": "This channel is where we debate all future architecture plans",
  "membershipType": "standard",
  "createdDateTime": "2020-03-14T11:22:17.047Z"
}
```

#### <a name="response"></a>Réponse

```http
HTTP/1.1 202 Accepted

{
   "@odata.context":"https://canary.graph.microsoft.com/testprodbetateamsgraphsvcncus/$metadata#teams('9cc6d6ab-07d8-4d14-bc2b-7db8995d6d23')/channels/$entity",
   "id":"19:e90f6814ce674072a4126206e7de485e@thread.tacv2",
   "createdDateTime":null,
   "displayName":"Architecture Discussion",
   "description":"This channel is where we debate all future architecture plans",
   "isFavoriteByDefault":null,
   "email":null,
   "webUrl":null,
   "membershipType":null,
   "moderationSettings":null
}
```

#### <a name="error-message"></a>Message d’erreur

```http
400 Bad Request
```

* `createdDateTime`  définie pour l’avenir.
* `createdDateTime`  correctement spécifié, mais `channelCreationMode`  l’attribut d’instance est manquant ou a une valeur non valide.

## <a name="step-three-import-messages"></a>Étape 3 : Importer des messages

Une fois l’équipe et le canal créés, vous pouvez commencer à envoyer des messages dans le temps à l’aide des clés dans `createdDateTime`  le corps de la `from`  demande. **REMARQUE**: les messages importés avec des threads de messages antérieures ne `createdDateTime` sont pas pris en `createdDateTime` charge.

> [!NOTE]
> * `createdDateTime` doit être unique entre les messages dans le même thread.
> * `createdDateTime` prend en charge les timestamps avec une précision en millisecondes. Par exemple, si la valeur du message de demande entrante est définie sur `createdDateTime` *2020-09-16T05:50:31.0025302Z,* il est converti en *2020-09-16T05:50:31.002Z* lorsque le message est saturé.

#### <a name="request-post-message-that-is-text-only"></a>Demande (message POST en texte uniquement)

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/messages

{
   "createdDateTime":"2019-02-04T19:58:15.511Z",
   "from":{
      "user":{
         "id":"id-value",
         "displayName":"Joh Doe",
         "userIdentityType":"aadUser"
      }
   },
   "body":{
      "contentType":"html",
      "content":"Hello World"
   }
}
```

#### <a name="response"></a>Réponse

```http
HTTP/1.1 200 OK

{
   "@odata.context":"https://graph.microsoft.com/beta/$metadata#teams('teamId')/channels('channelId')/messages/$entity",
   "id":"id-value",
   "replyToId":null,
   "etag":"id-value",
   "messageType":"message",
   "createdDateTime":"2019-02-04T19:58:15.58Z",
   "lastModifiedDateTime":null,
   "deleted":false,
   "subject":null,
   "summary":null,
   "importance":"normal",
   "locale":"en-us",
   "policyViolation":null,
   "from":{
      "application":null,
      "device":null,
      "conversation":null,
      "user":{
         "id":"id-value",
         "displayName":"Joh Doe",
         "userIdentityType":"aadUser"
      }
   },
   "body":{
      "contentType":"html",
      "content":"Hello World"
   },
   "attachments":[
   ],
   "mentions":[
   ],
   "reactions":[
   ]
}
```

#### <a name="error-messages"></a>Messages d’erreur

```http
400 Bad Request
```

#### <a name="request-post-a-message-with-inline-image"></a>Demander (PUBLIER un message avec une image fixe)

> **Remarque**: il n’existe aucune étendue d’autorisation spéciale dans ce scénario, car la demande fait partie de chatMessage ; Les étendues de chatMessage s’appliquent également ici.

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/messages

{
  "body": {
        "contentType": "html",
        "content": "<div><div>\n<div><span><img height=\"250\" src=\"../hostedContents/1/$value\" width=\"176.2295081967213\" style=\"vertical-align:bottom; width:176px; height:250px\"></span>\n\n</div>\n\n\n</div>\n</div>"
    },
    "hostedContents":[
        {
            "@microsoft.graph.temporaryId": "1",
            "contentBytes": "iVBORw0KGgoAAAANSUhEUgAAANcAAAExCAYAAADvFzeeAAAXjklEQVR4Ae2d/XNU1RnH+9e0FFrA0RCIyaS8hRA0HV5KbS1gHRgVpjMClY4GHJ3yYm1HCmXaWttaaZUZtIIFKYi8lFAkvOQ9u5vN225IARVBbX9/Os9NbrLZbMjmhCfJPX5+2Lmb3T25y3O+n/M599x7w9f+++UXwoMakIF7n4GvUdR7X1RqSk01A8CFuZm5GGUAuIwKi72wF3ABF+YyygBwGRUWc2Eu4AIuzGWUAeAyKizmwlzABVyYyygDwGVUWMyFuYALuDCXUQaAy6iwmAtzARdwfWXMdeuzT+TGxz3Sfb1LunrapL07IW3pePDQ5/qavqef0c+OdYAELuAac4jGGkLL9rdvfyo9N9ODQAqBGmmrwGlb/R0u3xG4gMspOC5hG882CoRaaCSA8n1ff9doIQMu4PIOrus3u+8ZVNnw6e/Od5AALuDKOyz5hmqiPnfnzi1J9bSbgRWCpvvQfY307wQu4BoxJCOFaDK8rwsQmQsUIQhWW93XSIsewAVckYdLQ24F0Ui/926AARdwRRounZ6Np7GyYdN9DzdFBC7gijRc43GMlQ1U9s/6HXJNjYELuHI<<-----Removed----->>>>",
            "contentType": "image/png"
        }
    ]
}
```

#### <a name="response"></a>Réponse

```http
HTTP/1.1 200 OK

{
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#teams('teamId')/channels('channelId')/messages/$entity",
    "id": "id-value",
    "replyToId": null,
    "etag": "id-value",
    "messageType": "message",
    "createdDateTime": "2019-02-04T19:58:15.511Z",
    "lastModifiedDateTime": null,
    "deleted": false,
    "subject": null,
    "summary": null,
    "importance": "normal",
    "locale": "en-us",
    "policyViolation": null,
    "from": {
        "application": null,
        "device": null,
        "conversation": null,
        "user": {
            "id": "id-value",
            "displayName": "Joh Doe",
            "userIdentityType": "aadUser"
        }
    },
      "body": {
        "contentType": "html",
        "content": "<div><div>\n<div><span><img height=\"250\" src=\"https://graph.microsoft.com/teams/teamId/channels/channelId/messages/id-value/hostedContents/hostedContentId/$value\" width=\"176.2295081967213\" style=\"vertical-align:bottom; width:176px; height:250px\"></span>\n\n</div>\n\n\n</div>\n</div>"
    },
    "attachments": [],
    "mentions": [],
    "reactions": []
}
```

## <a name="step-four-complete-migration-mode"></a>Étape 4 : Terminer le mode de migration

Une fois le processus de migration des messages terminé, l’équipe et le canal sont sortis du mode de migration à l’aide de la  `completeMigration`  méthode. Cette étape ouvre les ressources d’équipe et de canal pour une utilisation générale par les membres de l’équipe. L’action est liée à `team` l’instance.

#### <a name="request-end-team-migration-mode"></a>Demande (mode de migration d’équipe de fin)

```http
POST https://graph.microsoft.com/beta/teams/teamId/completeMigration

```

#### <a name="response"></a>Réponse

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-channel-migration-mode"></a>Demande (mode de migration du canal final)

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/completeMigration

```

#### <a name="response"></a>Réponse

```http
HTTP/1.1 204 NoContent
```

#### <a name="error-response"></a>Réponse d’erreur

```http
400 Bad Request
```

* Action appelée sur un `team` `channel` ou qui n’est pas dans `migrationMode` .

## <a name="step-five-add-team-members"></a>Étape 5 : Ajouter des membres d’équipe

Vous pouvez ajouter un membre à une équipe à [l’aide](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) de l’interface utilisateur Teams ou de l’API Ajouter [un membre](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) Microsoft Graph :

#### <a name="request-add-member"></a>Demande (ajouter un membre)

```http
POST https://graph.microsoft.com/beta/teams/{id}/members
Content-type: application/json
Content-length: 30
{
"@odata.type": "#microsoft.graph.aadUserConversationMember",
"roles": [],
"user@odata.bind": "https://graph.microsoft.com/beta/users/{user-id}"
}
```

#### <a name="response"></a>Réponse

```http
HTTP/1.1 204 No Content
```

## <a name="tips-and-additional-information"></a>Conseils et informations supplémentaires

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* Vous pouvez importer des messages provenant d’utilisateurs qui ne sont pas dans Teams. **REMARQUE**: les messages importés pour les utilisateurs non présents dans le client ne seront pas accessibles dans le client Teams ou les portails de conformité lors de la prévisualisation publique.

* Une fois `completeMigration` la demande faite, vous ne pouvez pas importer d’autres messages dans l’équipe.

* Les membres de l’équipe peuvent uniquement être ajoutés à la nouvelle équipe une fois `completeMigration` que la demande a renvoyé une réponse réussie.

* Limitation : les messages sont importés à 5 rps par canal.

* Si vous devez apporter une correction aux résultats de la migration, vous devez supprimer l’équipe et répéter les étapes pour créer l’équipe et le canal et migrer à nouveau les messages.

> [!NOTE]
> Actuellement, les images inline sont le seul type de média pris en charge par le schéma d’API d’importation de message.

##### <a name="import-content-scope"></a>Importer l’étendue du contenu

|Dans l’étendue | Actuellement hors de portée|
|----------|--------------------------|
|Messages d’équipe et de canal|1:1 et messages de conversation de groupe|
|Heure de création du message d’origine|Canaux privés|
|Images inline dans le cadre du message|À mentions|
|Liens vers des fichiers existants dans SPO/OneDrive|Réactions|
|Messages avec texte enrichi|Vidéos|
|Chaîne de réponse de message|Annonces|
|Traitement à haut débit|Extraits de code|
||Cartes adaptatives|
||Autocollants|
||Emojis|
||Guillemets|
||Billets croisés entre les canaux|


## <a name="see-also"></a>Voir aussi
> [!div class="nextstepaction"]
>[En savoir plus sur l’intégration de Microsoft Graph et Teams](/graph/teams-concept-overview)
