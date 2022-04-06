---
title: Utiliser Microsoft Graph pour importer des messages de plateforme externe dans Teams
description: Décrit comment utiliser Microsoft Graph pour importer des messages à partir d’une plateforme externe vers Teams
ms.localizationpriority: medium
author: akjo
ms.author: lajanuar
ms.topic: Overview
keywords: teams import messages api graph microsoft migrate migration post
ms.openlocfilehash: 5a33334367d0f5c229874decd5e45c5bb89ceafc
ms.sourcegitcommit: f892125106adb6731a20127f15d6e92f279127c5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/06/2022
ms.locfileid: "64685631"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a>Importer des messages de plateforme tierces pour les équipes à l’aide de Microsoft Graph

Avec Microsoft Graph, vous pouvez migrer l’historique des messages et les données existants des utilisateurs d’un système externe vers un canal Teams. En activant la recréation d’une hiérarchie de messagerie de plateforme tierce à l’intérieur de Teams, les utilisateurs peuvent poursuivre leurs communications de manière transparente et continuer sans interruption.

> [!NOTE]
> À l’avenir, Microsoft pourra exiger que vous ou vos clients payiez des frais supplémentaires en fonction du volume de données importées.

## <a name="import-overview"></a>Vue d’ensemble de l’importation

À un niveau élevé, le processus d’importation se compose des éléments suivants :

1. [Créez une équipe avec un horodatage de retour dans le temps](#step-1-create-a-team).
1. [Créez un canal avec un horodatage de retour dans le temps](#step-2-create-a-channel).
1. [Importer des messages datant du retour dans le temps externes](#step-3-import-messages).
1. [Terminez le processus de migration de l’équipe et du canal](#step-4-complete-migration-mode).
1. [Ajoutez des membres de l’équipe](#step-five-add-team-members).

## <a name="prerequisites"></a>Configuration requise

### <a name="analyze-and-prepare-message-data"></a>Analyser et préparer les données de message

* Passez en revue les données tierces pour déterminer ce qui sera migré.  
* Extrayez les données sélectionnées à partir du système de conversation tiers.  
* Mappez la structure de conversation tierce à la structure Teams.  
* Convertissez les données d’importation au format nécessaire à la migration.  

### <a name="set-up-your-office-365-tenant"></a>Configuration de votre client Office 365

* Vérifiez qu’il existe un locataire Office 365 pour les données d’importation. Pour plus d’informations sur la configuration d’une location Office 365 pour Teams, consultez [préparer votre locataire Office 365](../../concepts/build-and-test/prepare-your-o365-tenant.md).
* Assurez-vous que les membres de l’équipe sont en Azure Active Directory. Pour plus d’informations, consultez [ajouter un nouvel utilisateur](/azure/active-directory/fundamentals/add-users-azure-active-directory) à Azure AD.

## <a name="step-1-create-a-team"></a>Étape 1 : Créer une équipe

Étant donné que vous migrez des données existantes, la gestion des horodatages de message d’origine et la prévention de l’activité de messagerie pendant le processus de migration sont essentielles pour recréer le flux de messages existant de l’utilisateur dans Teams. Pour ce faire, procédez comme suit :

> [Créez une équipe](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) avec un horodatage de retour dans le temps à l’aide de la propriété de ressource `createdDateTime` d’équipe. Placez la nouvelle équipe dans `migration mode`un état spécial qui empêche les utilisateurs de la plupart des activités au sein de l’équipe jusqu’à ce que le processus de migration soit terminé. Incluez l’attribut `teamCreationMode` d’instance avec la `migration` valeur dans la requête POST pour identifier explicitement la nouvelle équipe comme étant créée pour la migration.  

> [!NOTE]
> Le `createdDateTime` champ est rempli uniquement pour les instances d’une équipe ou d’un canal qui ont été migrés.

<!-- markdownlint-disable MD001 -->

#### <a name="permission"></a>Autorisation

|ScopeName|DisplayName|Description|Type|Consentement de l’administrateur ?|Entités/API couvertes|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|Gérer la migration vers Microsoft Teams|Création et gestion des ressources pour la migration vers Microsoft Teams.|**Application uniquement**|**Oui**|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a>Requête (créer une équipe dans l’état de migration)

```http
POST https://graph.microsoft.com/v1.0/teams

Content-Type: application/json
{
  "@microsoft.graph.teamCreationMode": "migration",
  "template@odata.bind": "https://graph.microsoft.com/v1.0/teamsTemplates('standard')",
  "displayName": "My Sample Team",
  "description": "My Sample Team’s Description",
  "createdDateTime": "2020-03-14T11:22:17.043Z"
}
```

#### <a name="response"></a>Réponse

```http
HTTP/1.1 202 Accepted
Location: /teams/{team-id}/operations/{operation-id}
Content-Location: /teams/{team-id}
```

#### <a name="error-message"></a>Message d’erreur

```http
400 Bad Request
```

Vous pouvez recevoir le message d’erreur dans les scénarios suivants :

* Si `createdDateTime` est défini pour l’avenir.
* S’il `createdDateTime` est correctement spécifié, mais `teamCreationMode` que l’attribut d’instance est manquant ou défini sur une valeur non valide.

## <a name="step-2-create-a-channel"></a>Étape 2 : Créer un canal

La création d’un canal pour les messages importés est similaire au scénario de création d’équipe :

> [Créez un canal](/graph/api/channel-post?view=graph-rest-v1.0&tabs=http&preserve-view=true) avec un horodatage de retour dans le temps à l’aide de la propriété de ressource `createdDateTime` de canal. Placez le nouveau canal dans `migration mode`un état spécial qui empêche les utilisateurs de la plupart des activités de conversation au sein du canal jusqu’à ce que le processus de migration soit terminé. Incluez l’attribut `channelCreationMode` d’instance avec la `migration` valeur dans la requête POST pour identifier explicitement la nouvelle équipe comme étant créée pour la migration.  
<!-- markdownlint-disable MD024 -->
#### <a name="permission"></a>Autorisation

|ScopeName|DisplayName|Description|Type|Consentement de l’administrateur ?|Entités/API couvertes|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|Gérer la migration vers Microsoft Teams|Création et gestion des ressources pour la migration vers Microsoft Teams.|**Application uniquement**|**Oui**|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a>Requête (créer un canal dans l’état de migration)

```http
POST https://graph.microsoft.com/v1.0/teams/{team-id}/channels

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
   "@odata.context":"https://graph.microsoft.com/v1.0/$metadata#teams('team-id')/channels/$entity",
   "id":"id-value",
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

Vous pouvez recevoir le message d’erreur dans les scénarios suivants :

* Si `createdDateTime` est défini pour l’avenir.
* Si `createdDateTime` elle est correctement spécifiée, mais que `channelCreationMode` l’attribut d’instance est manquant ou défini sur une valeur non valide.

## <a name="step-3-import-messages"></a>Étape 3 : Importer des messages

Une fois l’équipe et le canal créés, vous pouvez commencer à envoyer des messages de retour dans le temps à l’aide des clés et `from` des `createdDateTime` clés dans le corps de la requête.

> [!NOTE]
>
> * Les messages importés avec `createdDateTime` des valeurs antérieures au thread `createdDateTime` de message ne sont pas pris en charge.
> * `createdDateTime` doit être unique entre les messages du même thread.
> * `createdDateTime` prend en charge les horodatages avec une précision en millisecondes. Par exemple, si la valeur du message de `createdDateTime` demande entrante est *définie sur 2020-09-16T05:50:31.0025302Z*, il est converti en *2020-09-16T05:50:31.002Z* lorsque le message est ingéré.

#### <a name="request-post-message-that-is-text-only"></a>Requête (message POST en texte uniquement)

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/channels/channel-id/messages

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
   "@odata.context":"https://graph.microsoft.com/v1.0/$metadata#teams('team-id')/channels('channel-id')/messages/$entity",
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

#### <a name="error-message"></a>Message d’erreur

```http
400 Bad Request
```

#### <a name="request-post-a-message-with-inline-image"></a>Request (POST a message with inline image)

> [!NOTE]
>
> * Il n’existe aucune étendue d’autorisation spéciale dans ce scénario, car la demande fait partie de `chatMessage`.
> * Les étendues à `chatMessage` appliquer ici.

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/channels/channel-id/messages

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
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#teams('team-id')/channels('channel-id')/messages/$entity",
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

## <a name="step-4-complete-migration-mode"></a>Étape 4 : Terminer le mode de migration

Une fois le processus de migration des messages terminé, l’équipe et le canal sont retirés du mode de migration à l’aide de la  `completeMigration` méthode. Cette étape ouvre les ressources d’équipe et de canal pour une utilisation générale par les membres de l’équipe. L’action est liée à l’instance `team` . Avant la fin de l’équipe, tous les canaux doivent être terminés hors du mode de migration.

#### <a name="request-end-channel-migration-mode"></a>Demande (mode de migration de canal final)

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/channels/channel-id/completeMigration

```

#### <a name="response"></a>Réponse

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-team-migration-mode"></a>Demande (mode de migration de l’équipe de fin)

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/completeMigration
```

#### <a name="response"></a>Réponse

```http
HTTP/1.1 204 NoContent
```

Action appelée sur un `team` ou `channel` qui n’est pas dans `migrationMode`.

## <a name="step-five-add-team-members"></a>Étape 5 : Ajouter des membres d’équipe

Vous pouvez ajouter un membre à une équipe à [l’aide de l’interface utilisateur Teams](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) ou de Microsoft Graph [ajouter](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) une API membre :

#### <a name="request-add-member"></a>Requête (ajouter un membre)

```http
POST https://graph.microsoft.com/beta/teams/{team-id}/members
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

## <a name="tips-and-additional-information"></a>Astuces et des informations supplémentaires

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* Une fois la `completeMigration` demande effectuée, vous ne pouvez pas importer d’autres messages dans l’équipe.

* Vous ne pouvez ajouter des membres d’équipe à la nouvelle équipe qu’une fois que la `completeMigration` demande a renvoyé une réponse correcte.

* Limitation : les messages sont importés à cinq RPS par canal.

* Si vous devez apporter une correction aux résultats de la migration, vous devez supprimer l’équipe et répéter les étapes pour créer l’équipe et le canal, puis migrer à nouveau les messages.

> [!NOTE]
> Actuellement, les images incluses sont le seul type de média pris en charge par le schéma d’API de message d’importation.

##### <a name="import-content-scope"></a>Importer l’étendue du contenu

Le tableau suivant fournit l’étendue de contenu :

|Dans l’étendue | Actuellement hors de portée|
|----------|--------------------------|
|Messages d’équipe et de canal|1:1 et messages de conversation de groupe|
|Heure de création du message d’origine|Canaux privés|
|Images incluses dans le message|Aux mentions|
|Liens vers des fichiers existants dans SPO ou OneDrive|Réactions|
|Messages avec du texte enrichi|Vidéos|
|Chaîne de réponse de message|Annonces|
|Traitement à débit élevé|Extraits de code|
||Autocollants|
||Emojis|
||Devis|
||Messages croisés entre canaux|
||Canaux partagés|

## <a name="see-also"></a>Voir aussi

[Intégration de Microsoft Graph et Teams](/graph/teams-concept-overview)
