---
title: Utiliser Microsoft Graph pour importer des messages de plateformes externes dans Teams
description: Décrit comment utiliser Microsoft Graph pour importer des messages d'une plateforme externe dans Teams.
ms.localizationpriority: high
author: akjo
ms.author: lajanuar
ms.topic: Overview
ms.openlocfilehash: 759fe9af0178af47c5f14b849269ab9ab444c35f
ms.sourcegitcommit: d92e14fad6567fe91fd52ee6c213836740316683
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/06/2022
ms.locfileid: "67605032"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a>Importer des messages de plateforme tierces pour les équipes à l’aide de Microsoft Graph

Avec le graphique Microsoft, vous pouvez migrer l'historique des messages et les données des utilisateurs d'un système externe vers un canal Teams. En permettant la recréation d'une hiérarchie de messagerie d'une plateforme tierce au sein de Teams, les utilisateurs peuvent poursuivre leurs communications de manière transparente et sans interruption.

> [!NOTE]
> À l’avenir, Microsoft pourra exiger que vous ou vos clients payiez des frais supplémentaires en fonction du volume de données importées.

## <a name="import-overview"></a>Aperçu des importations

À un niveau élevé, le processus d'importation se compose des éléments suivants :

1. [Créer une équipe avec un horodatage de retour dans le temps](#step-1-create-a-team).
1. [Créer un canal avec un horodatage de retour dans le temps](#step-2-create-a-channel).
1. [Importation de messages externes datés dans le temps](#step-3-import-messages).
1. [Compléter le processus de migration des équipes et des canaux](#step-4-complete-migration-mode).
1. [Ajouter des membres de l'équipe](#step-five-add-team-members).

## <a name="prerequisites"></a>Configuration requise

### <a name="analyze-and-prepare-message-data"></a>Analyser et préparer les données des messages

* Examinez les données des tiers pour décider de ce qui sera migré.  
* Extraire les données sélectionnées du système de conversation tiers.  
* Mettez en correspondance la structure de conversation de la tierce partie avec la structure de Teams.  
* Convertissez les données d'importation dans le format nécessaire à la migration.  

### <a name="set-up-your-office-365-tenant"></a>Configuration de votre client Office 365

* Assurez-vous qu'un locataire Office 365 existe pour les données d'importation. Pour plus d'informations sur la configuration d'un locataire Office 365 pour Teams, consultez la section [préparer votre locataire Office 365](../../concepts/build-and-test/prepare-your-o365-tenant.md).
* Assurez-vous que les membres de l'équipe sont dans Azure Active Directory. Pour plus d’informations, consultez [ajouter un nouvel utilisateur](/azure/active-directory/fundamentals/add-users-azure-active-directory) à Azure AD.

## <a name="step-1-create-a-team"></a>Étape 1 : Créer une équipe

Puisque vous migrez des données existantes, le maintien des horodatages originaux des messages et la prévention de l'activité de messagerie pendant le processus de migration sont essentiels pour recréer le flux de messages existant de l'utilisateur dans Teams. Cet objectif est atteint de la manière suivante :

> [Créez une nouvelle équipe](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) avec un horodatage rétroactif en utilisant la `createdDateTime`propriété de ressource de l'équipe. Placez la nouvelle équipe en`migration mode` , un état spécial qui restreint les utilisateurs de la plupart des activités au sein de l'équipe jusqu'à ce que le processus de migration soit terminé. Incluez l'attribut `teamCreationMode`instance avec la valeur dans`migration` la requête POST pour identifier explicitement la nouvelle équipe comme étant créée pour la migration.  

> [!NOTE]
> Ce`createdDateTime` champ ne sera rempli que pour les instances d'une équipe ou d'un canal qui ont été migrées.

<!-- markdownlint-disable MD001 -->

#### <a name="permission"></a>Autorisation

|ScopeName|DisplayName|Description|Type|Consentement de l'administration ?|Entités/API couvertes|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|Gérer la migration vers Microsoft Teams|Création et gestion des ressources pour la migration vers Teams.|**Application uniquement**|**Oui**|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a>Demande (créer une équipe dans l'état de migration)

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

Vous pouvez recevoir le message d'erreur dans les scénarios suivants :

* Si `createdDateTime` est défini pour l’avenir.
* Si `createdDateTime`est correctement spécifié`teamCreationMode`, mais l'attribut d'instance est manquant ou a une valeur invalide.

## <a name="step-2-create-a-channel"></a>Étape 2 : Créer un canal

La création d'un canal pour les messages importés est similaire à la création d'un canal d'équipe :

> [Créer un nouveau canal](/graph/api/channel-post?view=graph-rest-v1.0&tabs=http&preserve-view=true) avec un horodatage rétroactif en utilisant la `createdDateTime`propriété de ressource du canal. Placez le nouveau canal en`migration mode` , un état spécial qui restreint les utilisateurs de la plupart des activités de conversation dans le canal jusqu'à ce que le processus de migration soit terminé. Incluez l'attribut `channelCreationMode`instance avec la valeur dans`migration` la requête POST pour identifier explicitement la nouvelle équipe comme étant créée pour la migration.  
<!-- markdownlint-disable MD024 -->
#### <a name="permission"></a>Autorisation

|ScopeName|DisplayName|Description|Type|Consentement de l'administration ?|Entités/API couvertes|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|Gérer la migration vers Microsoft Teams|Création et gestion des ressources pour la migration vers Teams.|**Application uniquement**|**Oui**|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a>Demande (créer un canal en état de migration)

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

Vous pouvez recevoir le message d'erreur dans les scénarios suivants :

* Si `createdDateTime` est défini pour l’avenir.
* Si `createdDateTime`le produit est correctement `channelCreationMode`spécifié mais que l'attribut d'instance est absent ou a une valeur non valide.

## <a name="step-3-import-messages"></a>Étape 3 : Importer des messages

Une fois l'équipe et le canal créés, vous pouvez commencer à envoyer des messages rétroactifs en utilisant les clés `createdDateTime`  et `from`dans le corps de la requête.

> [!NOTE]
>
> * Les messages importés avec `createdDateTime`une date antérieure à celle du fil de messages ne sont pas `createdDateTime`pris en charge.
> * `createdDateTime` doit être unique pour tous les messages d'un même fil.
> * `createdDateTime`prend en charge les horodatages avec une précision de l'ordre de la milliseconde. Par exemple, si la valeur du message de demande entrant est `createdDateTime`fixée *à 2020-09-16T05:50:31.0025302Z*, elle sera convertie en *2020-09-16T05:50:31.002Z* lorsque le message sera ingéré.

#### <a name="request-post-message-that-is-text-only"></a>Demande (message POST en texte seul)

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

#### <a name="request-post-a-message-with-inline-image"></a>Demande (POST un message avec une image en ligne)

> [!NOTE]
>
> * Il n'y a pas d'autorisations spéciales dans ce scénario, car la demande fait partie de l'application `chatMessage`.
> * Les champs d'application `chatMessage`s'appliquent ici.

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

Une fois le processus de migration des messages terminé, l'équipe et le canal sont sortis du mode de migration en utilisant la `completeMigration`méthode suivante. Cette étape ouvre les ressources de l'équipe et du canal pour une utilisation générale par les membres de l'équipe. L'action est liée à `team`l'instance. Avant que l'équipe ne termine, tous les canaux doivent être sortis du mode de migration.

#### <a name="request-end-channel-migration-mode"></a>Demande (mode de migration de fin de canal)

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/channels/channel-id/completeMigration
```

#### <a name="response"></a>Réponse

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-team-migration-mode"></a>Demande (fin du mode de migration des équipes)

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/completeMigration
```

#### <a name="response"></a>Réponse

```http
HTTP/1.1 204 NoContent
```

Action appelée sur un `team` ou `channel` qui n’est pas dans `migrationMode`.

## <a name="step-five-add-team-members"></a>Étape 5 : Ajouter des membres d’équipe

Vous pouvez ajouter un membre à une [équipe en utilisant l'interface utilisateur Teams](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) ou l'API [d'ajout de membre](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) du graphique Microsoft :

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

## <a name="tips-and-additional-information"></a>Conseils et informations supplémentaires

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* Une fois la demande `completeMigration` effectuée, vous ne pouvez pas importer d’autres messages dans l’équipe.

* Vous ne pouvez ajouter des membres de l'équipe à la nouvelle équipe qu'après que la `completeMigration`demande a renvoyé une réponse positive.

* Limitation : Importation des messages à cinq RPS par canal.

* Si vous devez apporter une correction aux résultats de la migration, vous devez supprimer l'équipe et répéter les étapes pour créer l'équipe et le canal et migrer à nouveau les messages.

> [!NOTE]
> Actuellement, les images en ligne sont le seul type de média pris en charge par le schéma de l'API des messages d'importation.

##### <a name="import-content-scope"></a>Importation de la portée du contenu

Le tableau suivant présente l'étendue du contenu :

|Dans l’étendue | Actuellement hors l’étendue|
|----------|--------------------------|
|Messages de l'équipe et du canal|Messages de conversation 1:1 et de groupe|
|Heure de création du message original|Canaux privés|
|Images en ligne faisant partie du message|Aux mentions|
|Liens vers des fichiers existants dans SPO ou OneDrive|Réactions|
|Messages avec du texte enrichi|Vidéos|
|Chaîne de réponse aux messages|Annonces|
|Traitement à haut débit|Extraits de code|
||Autocollants|
||Emojis|
||Devis|
||Postes croisés entre les canaux|
||Canaux partagés|

## <a name="see-also"></a>Voir aussi

* [Intégration de Graphique et Teams de Microsoft](/graph/teams-concept-overview)
* [Exporter du contenu avec les API d’exportation Microsoft Teams](/microsoftteams/export-teams-content)
* [Limites du service Microsoft Teams](/graph/throttling-limits#microsoft-teams-service-limits)
* [Licences et exigences de paiement pour l’API Microsoft Teams](/graph/teams-licenses)
