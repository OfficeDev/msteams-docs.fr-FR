---
title: Utilisez microsoft Graph pour importer des messages de plate-forme externes à Teams
description: Décrit comment utiliser Microsoft pour importer des messages Graph une plate-forme externe pour Teams
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: les équipes importent des messages api graphique microsoft migrer la migration post
ms.openlocfilehash: 5ea06e8b490bae0595abb31086848d0b050bded0
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566158"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a>Importer des messages de plateforme tierces pour les équipes à l’aide de Microsoft Graph

Avec Microsoft Graph, vous pouvez migrer l’historique des messages et les données existants des utilisateurs à partir d’un système externe dans Teams canal. En permettant la reconstitution d’une hiérarchie de messagerie de plate-forme tierce à l’intérieur de Teams, les utilisateurs peuvent poursuivre leurs communications de manière transparente et procéder sans interruption.

> [!NOTE] 
> À l’avenir, Microsoft pourra exiger que vous ou vos clients payiez des frais supplémentaires en fonction du volume de données importées.

## <a name="import-overview"></a>Vue d’ensemble des importations

À un niveau élevé, le processus d’importation se compose des éléments suivants :

1. [Créer une équipe avec une lampe de temps de retour dans le temps](#step-one-create-a-team)
1. [Créer un canal avec une lampe de temps de retour dans le temps](#step-two-create-a-channel) 
1. [Importer des messages externes datés de retour dans le temps](#step-three-import-messages)
1. [Terminer le processus de migration de l’équipe et du canal](#step-four-complete-migration-mode)
1. [Ajouter les membres de l’équipe](#step-five-add-team-members)

## <a name="necessary-requirements"></a>Exigences nécessaires

### <a name="analyze-and-prepare-message-data"></a>Analyser et préparer les données des messages

✔ examiner les données de tiers pour décider ce qui sera migré.  
✔ extraire les données sélectionnées à partir du système de chat tiers.  
✔ la structure de chat tierce à la structure Teams tiers.  
✔ convertir les données d’importation en format nécessaire à la migration.  

### <a name="set-up-your-office-365-tenant"></a>Configuration de votre client Office 365

✔'assurer qu’un Office 365 existe pour les données d’importation. Pour plus d’informations sur la mise en place d Office 365 une location de Teams, [consultez Préparer votre Office 365 locataire.](../../concepts/build-and-test/prepare-your-o365-tenant.md)  
✔ assurez-vous que les membres de l’équipe sont Azure Active Directory (AAD).  Pour plus d’informations, [voir Ajouter un nouvel](/azure/active-directory/fundamentals/add-users-azure-active-directory) utilisateur à Azure Active Directory.

## <a name="step-one-create-a-team"></a>Première étape : Créer une équipe

Étant donné que les données existantes sont migrées, la maintenance des délais de message d’origine et la prévention de l’activité de messagerie pendant le processus de migration sont essentielles pour recréer le flux de messages existant de l’utilisateur dans Teams. Ceci est réalisé comme suit:

> [Créez une nouvelle équipe avec](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) une lampe de temps de retour à temps en utilisant la propriété des ressources de l’équipe. `createdDateTime` Placez la nouvelle équipe dans `migration mode` un état spécial qui interdit aux utilisateurs de la plupart des activités au sein de l’équipe jusqu’à ce que le processus de migration soit terminé. Inclure `teamCreationMode` l’attribut d’instance `migration` avec la valeur dans la demande POST pour identifier explicitement la nouvelle équipe comme étant créée pour la migration.  

> [!Note]
> Le `createdDateTime` champ ne sera peuplé que pour les cas d’une équipe ou d’un canal qui ont été migrés.

<!-- markdownlint-disable MD001 -->

#### <a name="permissions"></a>Autorisations

|ScopeName (scopename)|DisplayName|Description|Type|Consentement admin?|Entités/API couvertes|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|Gérer la migration vers Microsoft Teams|Créer, gérer des ressources pour la migration vers Microsoft Teams.|**Application uniquement**|**Oui**|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a>Demande (créer une équipe dans l’état de migration)

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

#### <a name="error-messages"></a>Messages d’erreur

```http
400 Bad Request
```

* `createdDateTime`  pour l’avenir.
* `createdDateTime`  correctement spécifié, mais `teamCreationMode`  l’attribut d’instance est manquant ou défini sur une valeur non valide.

## <a name="step-two-create-a-channel"></a>Deuxième étape : Créer un canal

La création d’un canal pour les messages importés est similaire au scénario d’équipe de création :

> [Créez un nouveau canal avec](/graph/api/channel-post?view=graph-rest-v1.0&tabs=http&preserve-view=true) une lampe de temps de retour dans le temps en utilisant la propriété ressource du `createdDateTime` canal. Placez le nouveau canal dans `migration mode` , un état spécial qui interdit aux utilisateurs de la plupart des activités de chat dans le canal jusqu’à ce que le processus de migration est terminé.  Inclure `channelCreationMode` l’attribut d’instance `migration` avec la valeur dans la demande POST pour identifier explicitement la nouvelle équipe comme étant créée pour la migration.  
<!-- markdownlint-disable MD024 -->
#### <a name="permissions"></a>Autorisations

|ScopeName (scopename)|DisplayName|Description|Type|Consentement admin?|Entités/API couvertes|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|Gérer la migration vers Microsoft Teams|Créer, gérer des ressources pour la migration vers Microsoft Teams.|**Application uniquement**|**Oui**|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a>Demande (créer un canal dans l’état de migration)

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

* `createdDateTime`  pour l’avenir.
* `createdDateTime`  correctement spécifié, mais `channelCreationMode`  l’attribut d’instance est manquant ou défini à la valeur invalide.

## <a name="step-three-import-messages"></a>Troisième étape : Importer des messages

Une fois que l’équipe et le canal ont été créés, vous pouvez commencer à envoyer des messages de retour dans le temps en utilisant `createdDateTime`  les clés et les clés de `from`  l’organisme de demande. **REMARQUE**: les messages importés plus `createdDateTime` tôt que le thread de message ne sont pas pris en `createdDateTime` charge.

> [!NOTE]
> * `createdDateTime` doit être unique à travers les messages dans le même thread.
> * `createdDateTime` prend en charge les tempstamps avec une précision milliseconde. Par exemple, si le message de demande entrant a la valeur `createdDateTime` de *définir comme 2020-09-16T05:50:31.0025302Z*, alors il serait converti *en 2020-09-16T05:50:31.002Z* lorsque le message est ingéré.

#### <a name="request-post-message-that-is-text-only"></a>Demande (MESSAGE POST uniquement textuel)

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

#### <a name="error-messages"></a>Messages d’erreur

```http
400 Bad Request
```

#### <a name="request-post-a-message-with-inline-image"></a>Demande (POSTEz un message avec l’image en ligne)

> [!Note]
> Il n’y a pas de portées d’autorisation spéciales dans ce scénario puisque la demande fait partie de chatMessage; les possibilités de chatMessage s’appliquent ici aussi.

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

## <a name="step-four-complete-migration-mode"></a>Quatrième étape : Mode de migration complet

Une fois le processus de migration des messages terminé, l’équipe et le canal sont retirés du mode migration en utilisant la  `completeMigration`  méthode. Cette étape ouvre l’équipe et canalise les ressources pour une utilisation générale par les membres de l’équipe. L’action est liée à `team` l’instance. Tous les canaux doivent être complétés hors mode migration avant que l’équipe puisse être terminée.

#### <a name="request-end-channel-migration-mode"></a>Demande (mode de migration de canal final)

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/channels/channel-id/completeMigration

```

#### <a name="response"></a>Réponse

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-team-migration-mode"></a>Demande (mode de migration d’équipe de fin)

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/completeMigration
```

#### <a name="response"></a>Réponse

```http
HTTP/1.1 204 NoContent
```

* Action appelée sur un `team` ou qui `channel` n’est pas en `migrationMode` .

## <a name="step-five-add-team-members"></a>Cinquième étape : Ajouter les membres de l’équipe

Vous pouvez ajouter un membre à une équipe en utilisant [l’interface utilisateur Teams’interface](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) utilisateur ou microsoft Graph [ajouter api](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) membre :

#### <a name="request-add-member"></a>Demande (ajouter un membre)

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

## <a name="tips-and-additional-information"></a>Astuces informations complémentaires

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* Une fois la `completeMigration` demande faite, vous ne pouvez pas importer d’autres messages dans l’équipe.

* Les membres de l’équipe ne peuvent être ajoutés à la nouvelle équipe `completeMigration` qu’une fois que la demande a répondu avec succès.

* Limitation : Les messages importent à 5 RPS par canal.

* Si vous devez apporter une correction aux résultats de migration, vous devez supprimer l’équipe et répéter les étapes pour créer l’équipe et le canal et re-migrer les messages.

> [!NOTE]
> Actuellement, les images en ligne sont le seul type de support pris en charge par le schéma api de message d’importation.

##### <a name="import-content-scope"></a>Portée du contenu d’importation

|Dans le champ d’application | Actuellement hors de portée|
|----------|--------------------------|
|Messages d’équipe et de chaîne|1:1 et messages de chat de groupe|
|Temps créé du message original|Canaux privés|
|Images en ligne dans le cadre du message|Aux mentions|
|Liens vers des fichiers existants dans SPO/OneDrive|Réactions|
|Messages avec texte riche|Vidéos|
|Chaîne de réponse de message|Annonces|
|Traitement à haut débit|Extraits de code|
||Autocollants|
||Emojis|
||guillemets|
||Postes croisés entre les canaux|


## <a name="see-also"></a>Voir aussi

[En savoir plus sur l’intégration Graph microsoft Teams’intégration](/graph/teams-concept-overview)
