---
title: Utiliser Microsoft Graph pour importer des messages de plateforme externe vers teams
description: Indique comment utiliser Microsoft Graph pour importer des messages à partir d’une plateforme externe vers teams
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: marge des équipes importation de messages de l’API Microsoft Migrate migration post
ms.openlocfilehash: 8e8b21c9a38570d7ede745e27b9316b7aba29956
ms.sourcegitcommit: 9fd61042e8be513c2b2bd8a33ab5e9e6498d65c5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/20/2020
ms.locfileid: "46820366"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a>Importer des messages de plateforme tierces vers teams à l’aide de Microsoft Graph

>[!IMPORTANT]
> Les aperçus publics de Microsoft Graph et Microsoft teams sont disponibles pour l’accès anticipé et les commentaires. Bien que cette version ait subi des tests approfondis, elle n’est pas destinée à être utilisée en production.

Avec Microsoft Graph, vous pouvez migrer l’historique et les données des messages existants d’un système externe vers un canal Teams. En activant la récréation d’une hiérarchie de messagerie de plateforme tierce dans Teams, les utilisateurs peuvent continuer leurs communications de manière transparente et continuer sans interruption.

## <a name="import-overview"></a>Vue d’ensemble de l’importation

À un niveau élevé, le processus d’importation se compose des éléments suivants :

1. [Créer une équipe avec un horodatage à l’arrière](#step-one-create-a-team)
1. [Créer un canal avec un horodatage à la date d’expiration](#step-two-create-a-channel)  
1. [Importer des messages à l’arrière--](#step-three-import-messages)
1. [Effectuer le processus de migration d’équipe et de canal](#step-four-complete-migration-mode)
1. [Ajouter des membres de l’équipe](#step-five-add-team-members)

## <a name="necessary-requirements"></a>Conditions requises

### <a name="analyze-and-prepare-message-data"></a>Analyser et préparer les données de message

✔ Passer en revue les données tierces pour déterminer les éléments qui seront migrés.  
✔ Extraire les données sélectionnées du système de conversation tiers.  
✔ Convertir les données d’importation au format requis pour la migration.  
✔ Mapper la structure de conversation tierce à la structure Teams.

### <a name="set-up-your-office-365-tenant"></a>Configuration de votre client Office 365

✔ Vous assurer qu’un client Office 365 existe pour les données d’importation. Pour plus d’informations sur la configuration d’une location Office 365 pour Teams, *reportez-vous*à [la rubrique prepare Your Office 365 client](../../concepts/build-and-test/prepare-your-o365-tenant.md).  
✔ Vous assurer que les membres de l’équipe sont dans Azure Active Directory (AAD).  Pour plus d’informations, *consultez la rubrique* [Ajouter un nouvel utilisateur](/azure/active-directory/fundamentals/add-users-azure-active-directory) à Azure Active Directory.

## <a name="step-one-create-a-team"></a>Étape 1 : créer une équipe

Étant donné que les données existantes sont migrées, il est essentiel de conserver les estampilles du message d’origine et d’empêcher l’activité de messagerie pendant le processus de migration de recréer le flux de messages existant de l’utilisateur dans Teams. Pour ce faire, procédez comme suit :

1. [Créer une nouvelle équipe](/graph/api/team-post?view=graph-rest-beta&tabs=http) avec un horodatage à l’arrière-dernière à l’aide de la propriété de ressource d’équipe  `createdDateTime`  .  

1. Placez la nouvelle équipe dans `migration mode` , un état spécial qui barre les utilisateurs de la plupart des activités au sein de l’équipe jusqu’à ce que le processus de migration soit terminé. Incluez l' `teamCreationMode` attribut instance avec la `migration` valeur de la requête post pour identifier explicitement la nouvelle équipe comme étant créée pour la migration.  

<!-- markdownlint-disable MD001 -->

#### <a name="permissions"></a>Autorisations

|ScopeName|DisplayName|Description|Type|Consentement de l’administrateur ?|Entités/API couvertes|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|Gérer la migration vers Microsoft teams|Création, gestion de ressources pour la migration vers Microsoft teams|**Application uniquement**|**Oui**|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a>Demande (créer une équipe dans l’état de migration)

```http
POST https://graph.microsoft.com/beta/teams

Content-Type: application/json
{
  "@microsoft.graph.teamCreationMode": "migration",
  "template@odata.bind": "https://graph.microsoft.com/beta/teamsTemplates('standard')",
  "displayName": "My Sample Team",
  "description": "My Sample Team’s Description"
  "createdDateTime": "2020-03-14T11:22:17.067Z"
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

* `createdDateTime`  défini pour le futur.
* `createdDateTime`  correctement spécifié, mais l' `teamCreationMode`  attribut instance est manquant ou sa valeur n’est pas valide.

## <a name="step-two-create-a-channel"></a>Étape 2 : créer un canal

La création d’un canal pour les messages importés est similaire au scénario créer une équipe : 

1. [Créez un canal](/graph/api/channel-post?view=graph-rest-beta&tabs=http) avec un horodatage à l’arrière-dernière à l’aide de la propriété Channel Resource `createdDateTime` .

1. Placez le nouveau canal dans `migration mode` , un état spécial qui barre les utilisateurs de la plupart des activités de conversation au sein du canal jusqu’à ce que le processus de migration soit terminé.  Incluez l' `channelCreationMode` attribut instance avec la `migration` valeur de la requête post pour identifier explicitement la nouvelle équipe comme étant créée pour la migration.  
<!-- markdownlint-disable MD024 -->
#### <a name="permissions"></a>Autorisations

|ScopeName|DisplayName|Description|Type|Consentement de l’administrateur ?|Entités/API couvertes|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|Gérer la migration vers Microsoft teams|Création, gestion de ressources pour la migration vers Microsoft teams|**Application uniquement**|**Oui**|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a>Demande (créer un canal dans l’état de migration)

```http
POST https://graph.microsoft.com/beta/teams/{id}/channels

Content-Type: application/json
{
  "@microsoft.graph.channelCreationMode": "migration",
  "displayName": "Architecture Discussion",
  "description": "This channel is where we debate all future architecture plans",
  "membershipType": "standard",
  "createdDateTime": "2020-03-14T11:22:17.067Z"
}
```

#### <a name="response"></a>Réponse

```http
HTTP/1.1 202 Accepted
Location: /teams/{teamId}/channels/{channelId}/operations/{operationId}
Content-Location: /teams/{teamId}/channels/{channelId}
```

#### <a name="error-message"></a>Message d’erreur

```http
400 Bad Request
```

* `createdDateTime`  défini pour le futur.
* `createdDateTime`  correctement spécifié mais l' `channelCreationMode`  attribut instance est manquant ou sa valeur n’est pas valide.

## <a name="step-three-import-messages"></a>Étape 3 : importer des messages

Après avoir créé l’équipe et le canal, vous pouvez commencer à envoyer des messages à l’heure à l’aide des `createdDateTime` `from`  touches et dans le corps de la demande.

#### <a name="request-post-message-that-is-text-only"></a>Demande (POST-message en texte seul)

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/messages

{
    "replyToId": null,
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
        "content": "Hello World"
    },
    "attachments": [],
    "mentions": [],
    "reactions": []
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
        "content": "Hello World"
    },
    "attachments": [],
    "mentions": [],
    "reactions": []
}
```

#### <a name="request-post-a-message-with-inline-image"></a>Demande (publier un message avec l’image insérée)

> **Remarque**: il n’existe pas d’étendues d’autorisation spéciales dans ce scénario, car la demande fait partie de collectionchatmessage ; les étendues pour Collectionchatmessage s’appliquent également ici.

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
    {
      "body": {
        "contentType": "html",
        "content": "<div><div>\n<div><span><img height=\"250\" src=\"https://graph.microsoft.com/teams/teamId/channels/channelId/messages/id-value/hostedContents/hostedContentId/$value\" width=\"176.2295081967213\" style=\"vertical-align:bottom; width:176px; height:250px\"></span>\n\n</div>\n\n\n</div>\n</div>"
    },
    "attachments": [],
    "mentions": [],
    "reactions": []
}
```

## <a name="step-four-complete-migration-mode"></a>Étape 4 : terminer le mode de migration

Une fois le processus de migration des messages terminé, l’équipe et le canal sont sortis du mode de migration à l’aide de la  `completeMigration`  méthode. Cette étape ouvre les ressources de l’équipe et du canal pour une utilisation générale par les membres de l’équipe. L’action est liée à l' `team` instance.

#### <a name="request-end-team-migration-mode"></a>Demande (mode fin de migration de l’équipe)

```http
POST https://graph.microsoft.com/beta/teams/teamId/completeMigration

```

#### <a name="response"></a>Réponse

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-channel-migration-mode"></a>Request (mode de migration de canal de fin)

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

* Action appelée sur un `team` ou `channel` qui n’est pas dans `migrationMode` .

## <a name="step-five-add-team-members"></a>Étape 5 : ajouter des membres de l’équipe

Vous pouvez ajouter un membre à une équipe [à l’aide de l’interface utilisateur](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) de teams ou de l’API de [membre Add](/graph/api/group-post-members?view=graph-rest-beta&tabs=http) de Microsoft Graph :

#### <a name="request-add-member"></a>Demande (ajouter un membre)

```http
POST https://graph.microsoft.com/beta/groups/{id}/members/$ref
Content-type: application/json
Content-length: 30

{
  "@odata.id": "https://graph.microsoft.com/beta/directoryObjects/{id}"
}
```

#### <a name="response"></a>Réponse

```http
HTTP/1.1 204 No Content
```

## <a name="tips-and-additional-information"></a>Conseils et informations supplémentaires

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* Vous pouvez importer des messages à partir d’utilisateurs qui ne sont pas dans Teams.

* Une fois la `completeMigration` demande effectuée, vous ne pouvez pas importer d’autres messages dans l’équipe.

* Les membres d’équipe ne peuvent être ajoutés à la nouvelle équipe qu’une fois que la `completeMigration` demande a renvoyé une réponse.

* Limitation : importation de messages à 5 RPS par canal.

* Si vous devez corriger les résultats de la migration, vous devez supprimer l’équipe et répéter les étapes de création de l’équipe et du canal et de la remigration des messages.

> [!NOTE]
> Actuellement, les images associées sont le seul type de média pris en charge par le schéma de l’API de message d’importation.

##### <a name="import-content-scope"></a>Importer une étendue de contenu

|Dans l’étendue | Hors de portée|
|----------|--------------------------|
|Messages d’équipe et de canal|1:1 et messages de conversation de groupe|
|Heure de création du message d’origine|Canaux privés|
|Images incorporées dans le cadre du message|Aux mentions|
|Liens vers des fichiers existants dans SPO/OneDrive|Réactions|
|Messages avec un texte enrichi|Vidéos|
|Chaîne de réponse aux messages|Annonces|
|Traitement à haut débit|Extraits de code|
||Cartes adaptatives|
||Auprès|
||Emojis|
||France|
||Billets entre les canaux|

> [!div class="nextstepaction"]
>[En savoir plus sur l’intégration de Microsoft Graph et Teams](/graph/teams-concept-overview)
