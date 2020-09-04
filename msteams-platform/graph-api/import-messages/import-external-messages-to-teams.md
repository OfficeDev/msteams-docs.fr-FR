---
title: Utiliser Microsoft Graph pour importer des messages de plateforme externe vers teams
description: Indique comment utiliser Microsoft Graph pour importer des messages à partir d’une plateforme externe vers teams
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: marge des équipes importation de messages de l’API Microsoft Migrate migration post
ms.openlocfilehash: 0e0aa96373d29f07893456adf54986ec23bdec3c
ms.sourcegitcommit: 02ab2cb7820dc8665bb4ec6a1a40c3b8b8f29d66
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/03/2020
ms.locfileid: "47340948"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a><span data-ttu-id="617d7-104">Importer des messages de plateforme tierces pour les équipes à l’aide de Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="617d7-104">Import third-party platform messages to Teams using Microsoft Graph</span></span>

>[!IMPORTANT]
> <span data-ttu-id="617d7-105">Les aperçus publics de Microsoft Graph et Microsoft teams sont disponibles pour l’accès anticipé et les commentaires.</span><span class="sxs-lookup"><span data-stu-id="617d7-105">Microsoft Graph and Microsoft Teams public previews are available for early-access and feedback.</span></span> <span data-ttu-id="617d7-106">Bien que cette version ait subi des tests approfondis, elle n’est pas destinée à être utilisée en production.</span><span class="sxs-lookup"><span data-stu-id="617d7-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

<span data-ttu-id="617d7-107">Avec Microsoft Graph, vous pouvez migrer l’historique et les données des messages existants d’un système externe vers un canal Teams.</span><span class="sxs-lookup"><span data-stu-id="617d7-107">With Microsoft Graph, you can migrate users' existing message history and data from an external system into a Teams channel.</span></span> <span data-ttu-id="617d7-108">En activant la récréation d’une hiérarchie de messagerie de plateforme tierce dans Teams, les utilisateurs peuvent continuer leurs communications de manière transparente et continuer sans interruption.</span><span class="sxs-lookup"><span data-stu-id="617d7-108">By enabling the recreation of a third-party platform messaging hierarchy inside Teams, users can continue their communications in a seamless manner and proceed without interruption.</span></span>

## <a name="import-overview"></a><span data-ttu-id="617d7-109">Vue d’ensemble de l’importation</span><span class="sxs-lookup"><span data-stu-id="617d7-109">Import overview</span></span>

<span data-ttu-id="617d7-110">À un niveau élevé, le processus d’importation se compose des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="617d7-110">At a high level, the import process consists of the following:</span></span>

1. [<span data-ttu-id="617d7-111">Créer une équipe avec un horodatage à l’arrière</span><span class="sxs-lookup"><span data-stu-id="617d7-111">Create a team with a back-in-time timestamp</span></span>](#step-one-create-a-team)
1. [<span data-ttu-id="617d7-112">Créer un canal avec un horodatage à la date d’expiration</span><span class="sxs-lookup"><span data-stu-id="617d7-112">Create a channel with a back-in-time timestamp</span></span>](#step-two-create-a-channel)  
1. [<span data-ttu-id="617d7-113">Importer des messages à l’arrière--</span><span class="sxs-lookup"><span data-stu-id="617d7-113">Import external back-in-time dated messages</span></span>](#step-three-import-messages)
1. [<span data-ttu-id="617d7-114">Effectuer le processus de migration d’équipe et de canal</span><span class="sxs-lookup"><span data-stu-id="617d7-114">Complete the team and channel migration process</span></span>](#step-four-complete-migration-mode)
1. [<span data-ttu-id="617d7-115">Ajouter des membres de l’équipe</span><span class="sxs-lookup"><span data-stu-id="617d7-115">Add team members</span></span>](#step-five-add-team-members)

## <a name="necessary-requirements"></a><span data-ttu-id="617d7-116">Conditions requises</span><span class="sxs-lookup"><span data-stu-id="617d7-116">Necessary requirements</span></span>

### <a name="analyze-and-prepare-message-data"></a><span data-ttu-id="617d7-117">Analyser et préparer les données de message</span><span class="sxs-lookup"><span data-stu-id="617d7-117">Analyze and prepare message data</span></span>

<span data-ttu-id="617d7-118">✔ Passer en revue les données tierces pour déterminer les éléments qui seront migrés.</span><span class="sxs-lookup"><span data-stu-id="617d7-118">✔ Review the third-party data to decide what will be migrated.</span></span>  
<span data-ttu-id="617d7-119">✔ Extraire les données sélectionnées du système de conversation tiers.</span><span class="sxs-lookup"><span data-stu-id="617d7-119">✔ Extract the selected data from the third-party chat system.</span></span>  
<span data-ttu-id="617d7-120">✔ Convertir les données d’importation au format requis pour la migration.</span><span class="sxs-lookup"><span data-stu-id="617d7-120">✔ Convert import data into format needed for migration.</span></span>  
<span data-ttu-id="617d7-121">✔ Mapper la structure de conversation tierce à la structure Teams.</span><span class="sxs-lookup"><span data-stu-id="617d7-121">✔ Map the third-party chat structure to the Teams structure.</span></span>

### <a name="set-up-your-office-365-tenant"></a><span data-ttu-id="617d7-122">Configuration de votre client Office 365</span><span class="sxs-lookup"><span data-stu-id="617d7-122">Set up your Office 365 tenant</span></span>

<span data-ttu-id="617d7-123">✔ Vous assurer qu’un client Office 365 existe pour les données d’importation.</span><span class="sxs-lookup"><span data-stu-id="617d7-123">✔ Ensure that an Office 365 tenant exists for the import data.</span></span> <span data-ttu-id="617d7-124">Pour plus d’informations sur la configuration d’une location Office 365 pour Teams, *reportez-vous*à [la rubrique prepare Your Office 365 client](../../concepts/build-and-test/prepare-your-o365-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="617d7-124">For more information on setting up an Office 365 tenancy for Teams, *see*, [Prepare your Office 365 tenant](../../concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>  
<span data-ttu-id="617d7-125">✔ Vous assurer que les membres de l’équipe sont dans Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="617d7-125">✔ Make sure that team members are in Azure Active Directory (AAD).</span></span>  <span data-ttu-id="617d7-126">Pour plus d’informations, *consultez la rubrique* [Ajouter un nouvel utilisateur](/azure/active-directory/fundamentals/add-users-azure-active-directory) à Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="617d7-126">For more information *see* [Add a new user](/azure/active-directory/fundamentals/add-users-azure-active-directory) to Azure Active Directory.</span></span>

## <a name="step-one-create-a-team"></a><span data-ttu-id="617d7-127">Étape 1 : créer une équipe</span><span class="sxs-lookup"><span data-stu-id="617d7-127">Step One: Create a team</span></span>

<span data-ttu-id="617d7-128">Étant donné que les données existantes sont migrées, il est essentiel de conserver les estampilles du message d’origine et d’empêcher l’activité de messagerie pendant le processus de migration de recréer le flux de messages existant de l’utilisateur dans Teams.</span><span class="sxs-lookup"><span data-stu-id="617d7-128">Since existing data is being migrated, maintaining the original message timestamps and preventing messaging activity during the migration process are key to recreating the user's existing message flow in Teams.</span></span> <span data-ttu-id="617d7-129">Pour ce faire, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="617d7-129">This is achieved as follows:</span></span>

1. <span data-ttu-id="617d7-130">[Créer une nouvelle équipe](/graph/api/team-post?view=graph-rest-beta&tabs=http) avec un horodatage à l’arrière-dernière à l’aide de la propriété de ressource d’équipe  `createdDateTime`  .</span><span class="sxs-lookup"><span data-stu-id="617d7-130">[Create a new team](/graph/api/team-post?view=graph-rest-beta&tabs=http) with a back-in-time timestamp using the team resource  `createdDateTime`  property.</span></span>  

1. <span data-ttu-id="617d7-131">Placez la nouvelle équipe dans `migration mode` , un état spécial qui barre les utilisateurs de la plupart des activités au sein de l’équipe jusqu’à ce que le processus de migration soit terminé.</span><span class="sxs-lookup"><span data-stu-id="617d7-131">Place the new team in `migration mode`, a special state that bars users from most activities within the team until the migration process is complete.</span></span> <span data-ttu-id="617d7-132">Incluez l' `teamCreationMode` attribut instance avec la `migration` valeur de la requête post pour identifier explicitement la nouvelle équipe comme étant créée pour la migration.</span><span class="sxs-lookup"><span data-stu-id="617d7-132">Include the `teamCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  

<!-- markdownlint-disable MD001 -->

#### <a name="permissions"></a><span data-ttu-id="617d7-133">Autorisations</span><span class="sxs-lookup"><span data-stu-id="617d7-133">Permissions</span></span>

|<span data-ttu-id="617d7-134">ScopeName</span><span class="sxs-lookup"><span data-stu-id="617d7-134">ScopeName</span></span>|<span data-ttu-id="617d7-135">DisplayName</span><span class="sxs-lookup"><span data-stu-id="617d7-135">DisplayName</span></span>|<span data-ttu-id="617d7-136">Description</span><span class="sxs-lookup"><span data-stu-id="617d7-136">Description</span></span>|<span data-ttu-id="617d7-137">Type</span><span class="sxs-lookup"><span data-stu-id="617d7-137">Type</span></span>|<span data-ttu-id="617d7-138">Consentement de l’administrateur ?</span><span class="sxs-lookup"><span data-stu-id="617d7-138">Admin Consent?</span></span>|<span data-ttu-id="617d7-139">Entités/API couvertes</span><span class="sxs-lookup"><span data-stu-id="617d7-139">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="617d7-140">Gérer la migration vers Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="617d7-140">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="617d7-141">Création, gestion de ressources pour la migration vers Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="617d7-141">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="617d7-142">**Application uniquement**</span><span class="sxs-lookup"><span data-stu-id="617d7-142">**Application-only**</span></span>|<span data-ttu-id="617d7-143">**Oui**</span><span class="sxs-lookup"><span data-stu-id="617d7-143">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a><span data-ttu-id="617d7-144">Demande (créer une équipe dans l’état de migration)</span><span class="sxs-lookup"><span data-stu-id="617d7-144">Request (create a team in migration state)</span></span>

```http
POST https://graph.microsoft.com/beta/teams

Content-Type: application/json
{
  "@microsoft.graph.teamCreationMode": "migration",
  "template@odata.bind": "https://graph.microsoft.com/beta/teamsTemplates('standard')",
  "displayName": "My Sample Team",
  "description": "My Sample Team’s Description",
  "createdDateTime": "2020-03-14T11:22:17.067Z"
}
```

#### <a name="response"></a><span data-ttu-id="617d7-145">Réponse</span><span class="sxs-lookup"><span data-stu-id="617d7-145">Response</span></span>

```http
HTTP/1.1 202 Accepted
Location: /teams/{teamId}/operations/{operationId}
Content-Location: /teams/{teamId}
```

#### <a name="error-messages"></a><span data-ttu-id="617d7-146">Messages d’erreur</span><span class="sxs-lookup"><span data-stu-id="617d7-146">Error messages</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="617d7-147">`createdDateTime`  défini pour le futur.</span><span class="sxs-lookup"><span data-stu-id="617d7-147">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="617d7-148">`createdDateTime`  correctement spécifié, mais l' `teamCreationMode`  attribut instance est manquant ou sa valeur n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="617d7-148">`createdDateTime`  correctly specified, but `teamCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-two-create-a-channel"></a><span data-ttu-id="617d7-149">Étape 2 : créer un canal</span><span class="sxs-lookup"><span data-stu-id="617d7-149">Step Two: Create a channel</span></span>

<span data-ttu-id="617d7-150">La création d’un canal pour les messages importés est similaire au scénario créer une équipe :</span><span class="sxs-lookup"><span data-stu-id="617d7-150">Creating a channel for the imported messages is similar to the create team scenario:</span></span> 

1. <span data-ttu-id="617d7-151">[Créez un canal](/graph/api/channel-post?view=graph-rest-beta&tabs=http) avec un horodatage à l’arrière-dernière à l’aide de la propriété Channel Resource `createdDateTime` .</span><span class="sxs-lookup"><span data-stu-id="617d7-151">[Create a new channel](/graph/api/channel-post?view=graph-rest-beta&tabs=http) with a back-in-time timestamp using the channel resource `createdDateTime` property.</span></span>

1. <span data-ttu-id="617d7-152">Placez le nouveau canal dans `migration mode` , un état spécial qui barre les utilisateurs de la plupart des activités de conversation au sein du canal jusqu’à ce que le processus de migration soit terminé.</span><span class="sxs-lookup"><span data-stu-id="617d7-152">Place the new channel in `migration mode`, a special state that bars users from most chat activities within the channel until the migration process is complete.</span></span>  <span data-ttu-id="617d7-153">Incluez l' `channelCreationMode` attribut instance avec la `migration` valeur de la requête post pour identifier explicitement la nouvelle équipe comme étant créée pour la migration.</span><span class="sxs-lookup"><span data-stu-id="617d7-153">Include the `channelCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  
<!-- markdownlint-disable MD024 -->
#### <a name="permissions"></a><span data-ttu-id="617d7-154">Autorisations</span><span class="sxs-lookup"><span data-stu-id="617d7-154">Permissions</span></span>

|<span data-ttu-id="617d7-155">ScopeName</span><span class="sxs-lookup"><span data-stu-id="617d7-155">ScopeName</span></span>|<span data-ttu-id="617d7-156">DisplayName</span><span class="sxs-lookup"><span data-stu-id="617d7-156">DisplayName</span></span>|<span data-ttu-id="617d7-157">Description</span><span class="sxs-lookup"><span data-stu-id="617d7-157">Description</span></span>|<span data-ttu-id="617d7-158">Type</span><span class="sxs-lookup"><span data-stu-id="617d7-158">Type</span></span>|<span data-ttu-id="617d7-159">Consentement de l’administrateur ?</span><span class="sxs-lookup"><span data-stu-id="617d7-159">Admin Consent?</span></span>|<span data-ttu-id="617d7-160">Entités/API couvertes</span><span class="sxs-lookup"><span data-stu-id="617d7-160">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="617d7-161">Gérer la migration vers Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="617d7-161">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="617d7-162">Création, gestion de ressources pour la migration vers Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="617d7-162">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="617d7-163">**Application uniquement**</span><span class="sxs-lookup"><span data-stu-id="617d7-163">**Application-only**</span></span>|<span data-ttu-id="617d7-164">**Oui**</span><span class="sxs-lookup"><span data-stu-id="617d7-164">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a><span data-ttu-id="617d7-165">Demande (créer un canal dans l’état de migration)</span><span class="sxs-lookup"><span data-stu-id="617d7-165">Request (create a channel in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="617d7-166">Réponse</span><span class="sxs-lookup"><span data-stu-id="617d7-166">Response</span></span>

```http
HTTP/1.1 202 Accepted
Location: /teams/{teamId}/channels/{channelId}/operations/{operationId}
Content-Location: /teams/{teamId}/channels/{channelId}
```

#### <a name="error-message"></a><span data-ttu-id="617d7-167">Message d’erreur</span><span class="sxs-lookup"><span data-stu-id="617d7-167">Error message</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="617d7-168">`createdDateTime`  défini pour le futur.</span><span class="sxs-lookup"><span data-stu-id="617d7-168">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="617d7-169">`createdDateTime`  correctement spécifié mais l' `channelCreationMode`  attribut instance est manquant ou sa valeur n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="617d7-169">`createdDateTime`  correctly specified but `channelCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-three-import-messages"></a><span data-ttu-id="617d7-170">Étape 3 : importer des messages</span><span class="sxs-lookup"><span data-stu-id="617d7-170">Step Three: Import messages</span></span>

<span data-ttu-id="617d7-171">Après avoir créé l’équipe et le canal, vous pouvez commencer à envoyer des messages à l’heure à l’aide des `createdDateTime` `from`  touches et dans le corps de la demande.</span><span class="sxs-lookup"><span data-stu-id="617d7-171">After the team and channel have been created, you can begin sending back-in-time messages using the `createdDateTime`  and `from`  keys in the request body.</span></span>

#### <a name="request-post-message-that-is-text-only"></a><span data-ttu-id="617d7-172">Demande (POST-message en texte seul)</span><span class="sxs-lookup"><span data-stu-id="617d7-172">Request (POST message that is text-only)</span></span>

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

#### <a name="response"></a><span data-ttu-id="617d7-173">Réponse</span><span class="sxs-lookup"><span data-stu-id="617d7-173">Response</span></span>

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

#### <a name="request-post-a-message-with-inline-image"></a><span data-ttu-id="617d7-174">Demande (publier un message avec l’image insérée)</span><span class="sxs-lookup"><span data-stu-id="617d7-174">Request (POST a message with inline \`image)</span></span>

> <span data-ttu-id="617d7-175">**Remarque**: il n’existe pas d’étendues d’autorisation spéciales dans ce scénario, car la demande fait partie de collectionchatmessage ; les étendues pour Collectionchatmessage s’appliquent également ici.</span><span class="sxs-lookup"><span data-stu-id="617d7-175">**Note**: There are no special permission scopes in this scenario since the request is part of chatMessage; scopes for chatMessage apply here as well.</span></span>

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

#### <a name="response"></a><span data-ttu-id="617d7-176">Réponse</span><span class="sxs-lookup"><span data-stu-id="617d7-176">Response</span></span>

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

## <a name="step-four-complete-migration-mode"></a><span data-ttu-id="617d7-177">Étape 4 : terminer le mode de migration</span><span class="sxs-lookup"><span data-stu-id="617d7-177">Step Four: Complete migration mode</span></span>

<span data-ttu-id="617d7-178">Une fois le processus de migration des messages terminé, l’équipe et le canal sont sortis du mode de migration à l’aide de la  `completeMigration`  méthode.</span><span class="sxs-lookup"><span data-stu-id="617d7-178">Once the message migration process has completed, both the team and channel are taken out of migration mode using the  `completeMigration`  method.</span></span> <span data-ttu-id="617d7-179">Cette étape ouvre les ressources de l’équipe et du canal pour une utilisation générale par les membres de l’équipe.</span><span class="sxs-lookup"><span data-stu-id="617d7-179">This step opens the team and channel resources for general use by team members.</span></span> <span data-ttu-id="617d7-180">L’action est liée à l' `team` instance.</span><span class="sxs-lookup"><span data-stu-id="617d7-180">The action is bound to the `team` instance.</span></span>

#### <a name="request-end-team-migration-mode"></a><span data-ttu-id="617d7-181">Demande (mode fin de migration de l’équipe)</span><span class="sxs-lookup"><span data-stu-id="617d7-181">Request (end team migration mode)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/completeMigration

```

#### <a name="response"></a><span data-ttu-id="617d7-182">Réponse</span><span class="sxs-lookup"><span data-stu-id="617d7-182">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-channel-migration-mode"></a><span data-ttu-id="617d7-183">Request (mode de migration de canal de fin)</span><span class="sxs-lookup"><span data-stu-id="617d7-183">Request (end channel migration mode)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/completeMigration

```

#### <a name="response"></a><span data-ttu-id="617d7-184">Réponse</span><span class="sxs-lookup"><span data-stu-id="617d7-184">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="error-response"></a><span data-ttu-id="617d7-185">Réponse d’erreur</span><span class="sxs-lookup"><span data-stu-id="617d7-185">Error response</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="617d7-186">Action appelée sur un `team` ou `channel` qui n’est pas dans `migrationMode` .</span><span class="sxs-lookup"><span data-stu-id="617d7-186">Action called on a `team` or `channel` that is not in `migrationMode`.</span></span>

## <a name="step-five-add-team-members"></a><span data-ttu-id="617d7-187">Étape 5 : ajouter des membres de l’équipe</span><span class="sxs-lookup"><span data-stu-id="617d7-187">Step Five: Add team members</span></span>

<span data-ttu-id="617d7-188">Vous pouvez ajouter un membre à une équipe [à l’aide de l’interface utilisateur](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) de teams ou de l’API de [membre Add](/graph/api/group-post-members?view=graph-rest-beta&tabs=http) de Microsoft Graph :</span><span class="sxs-lookup"><span data-stu-id="617d7-188">You can add a member to a team [using the Teams UI](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) or Microsoft Graph [Add member](/graph/api/group-post-members?view=graph-rest-beta&tabs=http) API:</span></span>

#### <a name="request-add-member"></a><span data-ttu-id="617d7-189">Demande (ajouter un membre)</span><span class="sxs-lookup"><span data-stu-id="617d7-189">Request (add member)</span></span>

```http
POST https://graph.microsoft.com/beta/groups/{id}/members/$ref
Content-type: application/json
Content-length: 30

{
  "@odata.id": "https://graph.microsoft.com/beta/directoryObjects/{id}"
}
```

#### <a name="response"></a><span data-ttu-id="617d7-190">Réponse</span><span class="sxs-lookup"><span data-stu-id="617d7-190">Response</span></span>

```http
HTTP/1.1 204 No Content
```

## <a name="tips-and-additional-information"></a><span data-ttu-id="617d7-191">Conseils et informations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="617d7-191">Tips and additional information</span></span>

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* <span data-ttu-id="617d7-192">Vous pouvez importer des messages à partir d’utilisateurs qui ne sont pas dans Teams.</span><span class="sxs-lookup"><span data-stu-id="617d7-192">You can import messages from users who are not in Teams.</span></span>

* <span data-ttu-id="617d7-193">Une fois la `completeMigration` demande effectuée, vous ne pouvez pas importer d’autres messages dans l’équipe.</span><span class="sxs-lookup"><span data-stu-id="617d7-193">Once the `completeMigration` request is made, you cannot import further messages into the team.</span></span>

* <span data-ttu-id="617d7-194">Les membres d’équipe ne peuvent être ajoutés à la nouvelle équipe qu’une fois que la `completeMigration` demande a renvoyé une réponse.</span><span class="sxs-lookup"><span data-stu-id="617d7-194">Team members can only be added to the new team after the `completeMigration` request has returned a successful response.</span></span>

* <span data-ttu-id="617d7-195">Limitation : importation de messages à 5 RPS par canal.</span><span class="sxs-lookup"><span data-stu-id="617d7-195">Throttling: Messages import at 5 RPS per channel.</span></span>

* <span data-ttu-id="617d7-196">Si vous devez corriger les résultats de la migration, vous devez supprimer l’équipe et répéter les étapes de création de l’équipe et du canal et de la remigration des messages.</span><span class="sxs-lookup"><span data-stu-id="617d7-196">If you need to make a correction to the migration results, you need to delete the team and repeat the steps to create the team and channel and re-migrate the messages.</span></span>

> [!NOTE]
> <span data-ttu-id="617d7-197">Actuellement, les images associées sont le seul type de média pris en charge par le schéma de l’API de message d’importation.</span><span class="sxs-lookup"><span data-stu-id="617d7-197">Currently, Inline images is the only type of media supported by the import message API schema.</span></span>

##### <a name="import-content-scope"></a><span data-ttu-id="617d7-198">Importer une étendue de contenu</span><span class="sxs-lookup"><span data-stu-id="617d7-198">Import content scope</span></span>

|<span data-ttu-id="617d7-199">Dans l’étendue</span><span class="sxs-lookup"><span data-stu-id="617d7-199">In-scope</span></span> | <span data-ttu-id="617d7-200">Hors de portée</span><span class="sxs-lookup"><span data-stu-id="617d7-200">Currently out-of-scope</span></span>|
|----------|--------------------------|
|<span data-ttu-id="617d7-201">Messages d’équipe et de canal</span><span class="sxs-lookup"><span data-stu-id="617d7-201">Team and channel messages</span></span>|<span data-ttu-id="617d7-202">1:1 et messages de conversation de groupe</span><span class="sxs-lookup"><span data-stu-id="617d7-202">1:1 and group chat messages</span></span>|
|<span data-ttu-id="617d7-203">Heure de création du message d’origine</span><span class="sxs-lookup"><span data-stu-id="617d7-203">Created time of the original message</span></span>|<span data-ttu-id="617d7-204">Canaux privés</span><span class="sxs-lookup"><span data-stu-id="617d7-204">Private channels</span></span>|
|<span data-ttu-id="617d7-205">Images incorporées dans le cadre du message</span><span class="sxs-lookup"><span data-stu-id="617d7-205">Inline images as part of the message</span></span>|<span data-ttu-id="617d7-206">Aux mentions</span><span class="sxs-lookup"><span data-stu-id="617d7-206">At mentions</span></span>|
|<span data-ttu-id="617d7-207">Liens vers des fichiers existants dans SPO/OneDrive</span><span class="sxs-lookup"><span data-stu-id="617d7-207">Links to existing files in SPO/OneDrive</span></span>|<span data-ttu-id="617d7-208">Réactions</span><span class="sxs-lookup"><span data-stu-id="617d7-208">Reactions</span></span>|
|<span data-ttu-id="617d7-209">Messages avec un texte enrichi</span><span class="sxs-lookup"><span data-stu-id="617d7-209">Messages with rich text</span></span>|<span data-ttu-id="617d7-210">Vidéos</span><span class="sxs-lookup"><span data-stu-id="617d7-210">Videos</span></span>|
|<span data-ttu-id="617d7-211">Chaîne de réponse aux messages</span><span class="sxs-lookup"><span data-stu-id="617d7-211">Message reply chain</span></span>|<span data-ttu-id="617d7-212">Annonces</span><span class="sxs-lookup"><span data-stu-id="617d7-212">Announcements</span></span>|
|<span data-ttu-id="617d7-213">Traitement à haut débit</span><span class="sxs-lookup"><span data-stu-id="617d7-213">High throughput processing</span></span>|<span data-ttu-id="617d7-214">Extraits de code</span><span class="sxs-lookup"><span data-stu-id="617d7-214">Code snippets</span></span>|
||<span data-ttu-id="617d7-215">Cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="617d7-215">Adaptive cards</span></span>|
||<span data-ttu-id="617d7-216">Auprès</span><span class="sxs-lookup"><span data-stu-id="617d7-216">Stickers</span></span>|
||<span data-ttu-id="617d7-217">Emojis</span><span class="sxs-lookup"><span data-stu-id="617d7-217">Emojis</span></span>|
||<span data-ttu-id="617d7-218">France</span><span class="sxs-lookup"><span data-stu-id="617d7-218">Quotes</span></span>|
||<span data-ttu-id="617d7-219">Billets entre les canaux</span><span class="sxs-lookup"><span data-stu-id="617d7-219">Cross posts between channels</span></span>|

> [!div class="nextstepaction"]
>[<span data-ttu-id="617d7-220">En savoir plus sur l’intégration de Microsoft Graph et Teams</span><span class="sxs-lookup"><span data-stu-id="617d7-220">Learn more about Microsoft Graph and Teams integration</span></span>](/graph/teams-concept-overview)
