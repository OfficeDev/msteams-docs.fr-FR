---
title: Utiliser Microsoft Graph pour importer des messages de plateforme externe Teams
description: Décrit comment utiliser Microsoft Graph pour importer des messages à partir d’une plateforme externe vers Teams
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: teams import messages api graph microsoft migrate migration post
ms.openlocfilehash: 5ea06e8b490bae0595abb31086848d0b050bded0
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566158"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a><span data-ttu-id="d4335-104">Importer des messages de plateforme tierces pour les équipes à l’aide de Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="d4335-104">Import third-party platform messages to Teams using Microsoft Graph</span></span>

<span data-ttu-id="d4335-105">Avec Microsoft Graph, vous pouvez migrer l’historique des messages et les données des utilisateurs d’un système externe vers un canal Teams de données.</span><span class="sxs-lookup"><span data-stu-id="d4335-105">With Microsoft Graph, you can migrate users' existing message history and data from an external system into a Teams channel.</span></span> <span data-ttu-id="d4335-106">En activant la recréation d’une hiérarchie de messagerie de plateforme tierce à l’intérieur de Teams, les utilisateurs peuvent poursuivre leurs communications de manière transparente et sans interruption.</span><span class="sxs-lookup"><span data-stu-id="d4335-106">By enabling the recreation of a third-party platform messaging hierarchy inside Teams, users can continue their communications in a seamless manner and proceed without interruption.</span></span>

> [!NOTE] 
> <span data-ttu-id="d4335-107">À l’avenir, Microsoft pourra exiger que vous ou vos clients payiez des frais supplémentaires en fonction du volume de données importées.</span><span class="sxs-lookup"><span data-stu-id="d4335-107">In the future, Microsoft may require you or your customers to pay additional fees based on the amount of data imported.</span></span>

## <a name="import-overview"></a><span data-ttu-id="d4335-108">Vue d’ensemble de l’importation</span><span class="sxs-lookup"><span data-stu-id="d4335-108">Import overview</span></span>

<span data-ttu-id="d4335-109">À un niveau élevé, le processus d’importation se compose des opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="d4335-109">At a high level, the import process consists of the following:</span></span>

1. [<span data-ttu-id="d4335-110">Créer une équipe avec un timestamp de retour dans le temps</span><span class="sxs-lookup"><span data-stu-id="d4335-110">Create a team with a back-in-time timestamp</span></span>](#step-one-create-a-team)
1. [<span data-ttu-id="d4335-111">Créer un canal avec un timestamp de retour dans le temps</span><span class="sxs-lookup"><span data-stu-id="d4335-111">Create a channel with a back-in-time timestamp</span></span>](#step-two-create-a-channel) 
1. [<span data-ttu-id="d4335-112">Importer des messages obsolètes dans le temps externes</span><span class="sxs-lookup"><span data-stu-id="d4335-112">Import external back-in-time dated messages</span></span>](#step-three-import-messages)
1. [<span data-ttu-id="d4335-113">Terminer le processus de migration des équipes et des canaux</span><span class="sxs-lookup"><span data-stu-id="d4335-113">Complete the team and channel migration process</span></span>](#step-four-complete-migration-mode)
1. [<span data-ttu-id="d4335-114">Ajouter des membres d’équipe</span><span class="sxs-lookup"><span data-stu-id="d4335-114">Add team members</span></span>](#step-five-add-team-members)

## <a name="necessary-requirements"></a><span data-ttu-id="d4335-115">Conditions requises</span><span class="sxs-lookup"><span data-stu-id="d4335-115">Necessary requirements</span></span>

### <a name="analyze-and-prepare-message-data"></a><span data-ttu-id="d4335-116">Analyser et préparer les données des messages</span><span class="sxs-lookup"><span data-stu-id="d4335-116">Analyze and prepare message data</span></span>

<span data-ttu-id="d4335-117">✔ examiner les données tierces pour déterminer ce qui sera migré.</span><span class="sxs-lookup"><span data-stu-id="d4335-117">✔ Review the third-party data to decide what will be migrated.</span></span>  
<span data-ttu-id="d4335-118">✔ extraire les données sélectionnées du système de conversation tiers.</span><span class="sxs-lookup"><span data-stu-id="d4335-118">✔ Extract the selected data from the third-party chat system.</span></span>  
<span data-ttu-id="d4335-119">✔ la structure de conversation tierce à la structure Teams de conversation.</span><span class="sxs-lookup"><span data-stu-id="d4335-119">✔ Map the third-party chat structure to the Teams structure.</span></span>  
<span data-ttu-id="d4335-120">✔ convertir les données d’importation au format nécessaire pour la migration.</span><span class="sxs-lookup"><span data-stu-id="d4335-120">✔ Convert import data into format needed for migration.</span></span>  

### <a name="set-up-your-office-365-tenant"></a><span data-ttu-id="d4335-121">Configuration de votre client Office 365</span><span class="sxs-lookup"><span data-stu-id="d4335-121">Set up your Office 365 tenant</span></span>

<span data-ttu-id="d4335-122">✔ s’assurer qu’Office 365 client existant pour les données d’importation.</span><span class="sxs-lookup"><span data-stu-id="d4335-122">✔ Ensure that an Office 365 tenant exists for the import data.</span></span> <span data-ttu-id="d4335-123">Pour plus d’informations sur la configuration d’Office 365 client pour Teams, voir [Préparer votre client Office 365 client.](../../concepts/build-and-test/prepare-your-o365-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="d4335-123">For more information on setting up an Office 365 tenancy for Teams, see [Prepare your Office 365 tenant](../../concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>  
<span data-ttu-id="d4335-124">✔ assurez-vous que les membres de l’équipe sont Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="d4335-124">✔ Make sure that team members are in Azure Active Directory (AAD).</span></span>  <span data-ttu-id="d4335-125">Pour plus d’informations, [voir Ajouter un nouvel](/azure/active-directory/fundamentals/add-users-azure-active-directory) utilisateur à Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d4335-125">For more information, see [Add a new user](/azure/active-directory/fundamentals/add-users-azure-active-directory) to Azure Active Directory.</span></span>

## <a name="step-one-create-a-team"></a><span data-ttu-id="d4335-126">Étape 1 : Créer une équipe</span><span class="sxs-lookup"><span data-stu-id="d4335-126">Step One: Create a team</span></span>

<span data-ttu-id="d4335-127">Étant donné que les données existantes sont migrées, il est essentiel de maintenir les timestamps des messages d’origine et d’empêcher l’activité de messagerie pendant le processus de migration pour recréer le flux de messages existant de l’utilisateur dans Teams.</span><span class="sxs-lookup"><span data-stu-id="d4335-127">Since existing data is being migrated, maintaining the original message timestamps and preventing messaging activity during the migration process are key to recreating the user's existing message flow in Teams.</span></span> <span data-ttu-id="d4335-128">Pour ce faire, les résultats sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="d4335-128">This is achieved as follows:</span></span>

> <span data-ttu-id="d4335-129">[Créez une équipe avec](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) un timestamp de retour dans le temps à l’aide de la propriété de ressource  `createdDateTime`  d’équipe.</span><span class="sxs-lookup"><span data-stu-id="d4335-129">[Create a new team](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) with a back-in-time timestamp using the team resource  `createdDateTime`  property.</span></span> <span data-ttu-id="d4335-130">Placez la nouvelle équipe dans un état spécial qui interdit aux utilisateurs la plupart des activités au sein de l’équipe jusqu’à ce que le processus `migration mode` de migration soit terminé.</span><span class="sxs-lookup"><span data-stu-id="d4335-130">Place the new team in `migration mode`, a special state that bars users from most activities within the team until the migration process is complete.</span></span> <span data-ttu-id="d4335-131">Incluez `teamCreationMode` l’attribut d’instance avec la valeur dans la requête POST pour identifier explicitement la nouvelle équipe comme `migration` étant créée pour la migration.</span><span class="sxs-lookup"><span data-stu-id="d4335-131">Include the `teamCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  

> [!Note]
> <span data-ttu-id="d4335-132">Le champ sera rempli uniquement pour les instances d’une équipe ou d’un canal `createdDateTime` qui ont été migrées.</span><span class="sxs-lookup"><span data-stu-id="d4335-132">The `createdDateTime` field will only be populated for instances of a team or channel that have been migrated.</span></span>

<!-- markdownlint-disable MD001 -->

#### <a name="permissions"></a><span data-ttu-id="d4335-133">Autorisations</span><span class="sxs-lookup"><span data-stu-id="d4335-133">Permissions</span></span>

|<span data-ttu-id="d4335-134">ScopeName</span><span class="sxs-lookup"><span data-stu-id="d4335-134">ScopeName</span></span>|<span data-ttu-id="d4335-135">DisplayName</span><span class="sxs-lookup"><span data-stu-id="d4335-135">DisplayName</span></span>|<span data-ttu-id="d4335-136">Description</span><span class="sxs-lookup"><span data-stu-id="d4335-136">Description</span></span>|<span data-ttu-id="d4335-137">Type</span><span class="sxs-lookup"><span data-stu-id="d4335-137">Type</span></span>|<span data-ttu-id="d4335-138">Consentement de l’administrateur ?</span><span class="sxs-lookup"><span data-stu-id="d4335-138">Admin Consent?</span></span>|<span data-ttu-id="d4335-139">Entités/API couvertes</span><span class="sxs-lookup"><span data-stu-id="d4335-139">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="d4335-140">Gérer la migration vers Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="d4335-140">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="d4335-141">Création, gestion des ressources pour la migration vers Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="d4335-141">Creating, managing resources for migration to Microsoft Teams.</span></span>|<span data-ttu-id="d4335-142">**Application uniquement**</span><span class="sxs-lookup"><span data-stu-id="d4335-142">**Application-only**</span></span>|<span data-ttu-id="d4335-143">**Oui**</span><span class="sxs-lookup"><span data-stu-id="d4335-143">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a><span data-ttu-id="d4335-144">Demander (créer une équipe en état de migration)</span><span class="sxs-lookup"><span data-stu-id="d4335-144">Request (create a team in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="d4335-145">Réponse</span><span class="sxs-lookup"><span data-stu-id="d4335-145">Response</span></span>

```http
HTTP/1.1 202 Accepted
Location: /teams/{team-id}/operations/{operation-id}
Content-Location: /teams/{team-id}
```

#### <a name="error-messages"></a><span data-ttu-id="d4335-146">Messages d’erreur</span><span class="sxs-lookup"><span data-stu-id="d4335-146">Error messages</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="d4335-147">`createdDateTime`  définie pour l’avenir.</span><span class="sxs-lookup"><span data-stu-id="d4335-147">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="d4335-148">`createdDateTime`  correctement spécifié, mais `teamCreationMode`  l’attribut d’instance est manquant ou a une valeur non valide.</span><span class="sxs-lookup"><span data-stu-id="d4335-148">`createdDateTime`  correctly specified, but `teamCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-two-create-a-channel"></a><span data-ttu-id="d4335-149">Étape 2 : Créer un canal</span><span class="sxs-lookup"><span data-stu-id="d4335-149">Step Two: Create a channel</span></span>

<span data-ttu-id="d4335-150">La création d’un canal pour les messages importés est similaire au scénario de création d’équipe :</span><span class="sxs-lookup"><span data-stu-id="d4335-150">Creating a channel for the imported messages is similar to the create team scenario:</span></span>

> <span data-ttu-id="d4335-151">[Créez un canal avec](/graph/api/channel-post?view=graph-rest-v1.0&tabs=http&preserve-view=true) un timestamp de retour dans le temps à l’aide de la propriété de ressource `createdDateTime` de canal.</span><span class="sxs-lookup"><span data-stu-id="d4335-151">[Create a new channel](/graph/api/channel-post?view=graph-rest-v1.0&tabs=http&preserve-view=true) with a back-in-time timestamp using the channel resource `createdDateTime` property.</span></span> <span data-ttu-id="d4335-152">Placez le nouveau canal dans , un état spécial qui interdit aux utilisateurs de la plupart des activités de conversation au sein du canal jusqu’à ce que le processus `migration mode` de migration soit terminé.</span><span class="sxs-lookup"><span data-stu-id="d4335-152">Place the new channel in `migration mode`, a special state that bars users from most chat activities within the channel until the migration process is complete.</span></span>  <span data-ttu-id="d4335-153">Incluez `channelCreationMode` l’attribut d’instance avec la valeur dans la requête POST pour identifier explicitement la nouvelle équipe comme `migration` étant créée pour la migration.</span><span class="sxs-lookup"><span data-stu-id="d4335-153">Include the `channelCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  
<!-- markdownlint-disable MD024 -->
#### <a name="permissions"></a><span data-ttu-id="d4335-154">Autorisations</span><span class="sxs-lookup"><span data-stu-id="d4335-154">Permissions</span></span>

|<span data-ttu-id="d4335-155">ScopeName</span><span class="sxs-lookup"><span data-stu-id="d4335-155">ScopeName</span></span>|<span data-ttu-id="d4335-156">DisplayName</span><span class="sxs-lookup"><span data-stu-id="d4335-156">DisplayName</span></span>|<span data-ttu-id="d4335-157">Description</span><span class="sxs-lookup"><span data-stu-id="d4335-157">Description</span></span>|<span data-ttu-id="d4335-158">Type</span><span class="sxs-lookup"><span data-stu-id="d4335-158">Type</span></span>|<span data-ttu-id="d4335-159">Consentement de l’administrateur ?</span><span class="sxs-lookup"><span data-stu-id="d4335-159">Admin Consent?</span></span>|<span data-ttu-id="d4335-160">Entités/API couvertes</span><span class="sxs-lookup"><span data-stu-id="d4335-160">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="d4335-161">Gérer la migration vers Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="d4335-161">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="d4335-162">Création, gestion des ressources pour la migration vers Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="d4335-162">Creating, managing resources for migration to Microsoft Teams.</span></span>|<span data-ttu-id="d4335-163">**Application uniquement**</span><span class="sxs-lookup"><span data-stu-id="d4335-163">**Application-only**</span></span>|<span data-ttu-id="d4335-164">**Oui**</span><span class="sxs-lookup"><span data-stu-id="d4335-164">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a><span data-ttu-id="d4335-165">Demande (créer un canal dans l’état de migration)</span><span class="sxs-lookup"><span data-stu-id="d4335-165">Request (create a channel in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="d4335-166">Réponse</span><span class="sxs-lookup"><span data-stu-id="d4335-166">Response</span></span>

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

#### <a name="error-message"></a><span data-ttu-id="d4335-167">Message d’erreur</span><span class="sxs-lookup"><span data-stu-id="d4335-167">Error message</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="d4335-168">`createdDateTime`  définie pour l’avenir.</span><span class="sxs-lookup"><span data-stu-id="d4335-168">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="d4335-169">`createdDateTime`  correctement spécifié, mais `channelCreationMode`  l’attribut d’instance est manquant ou a une valeur non valide.</span><span class="sxs-lookup"><span data-stu-id="d4335-169">`createdDateTime`  correctly specified but `channelCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-three-import-messages"></a><span data-ttu-id="d4335-170">Étape 3 : Importer des messages</span><span class="sxs-lookup"><span data-stu-id="d4335-170">Step Three: Import messages</span></span>

<span data-ttu-id="d4335-171">Une fois l’équipe et le canal créés, vous pouvez commencer à envoyer des messages dans le temps à l’aide des clés dans `createdDateTime`  le corps de la `from`  demande.</span><span class="sxs-lookup"><span data-stu-id="d4335-171">After the team and channel have been created, you can begin sending back-in-time messages using the `createdDateTime`  and `from`  keys in the request body.</span></span> <span data-ttu-id="d4335-172">**REMARQUE**: les messages importés avec des threads de messages antérieures ne `createdDateTime` sont pas pris en `createdDateTime` charge.</span><span class="sxs-lookup"><span data-stu-id="d4335-172">**NOTE**: messages imported with `createdDateTime` earlier than the message thread `createdDateTime` is not supported.</span></span>

> [!NOTE]
> * <span data-ttu-id="d4335-173">`createdDateTime` doit être unique entre les messages dans le même thread.</span><span class="sxs-lookup"><span data-stu-id="d4335-173">`createdDateTime` must be unique across messages in the same thread.</span></span>
> * <span data-ttu-id="d4335-174">`createdDateTime` prend en charge les timestamps avec une précision en millisecondes.</span><span class="sxs-lookup"><span data-stu-id="d4335-174">`createdDateTime` supports timestamps with milliseconds precision.</span></span> <span data-ttu-id="d4335-175">Par exemple, si la valeur du message de demande entrante est définie sur `createdDateTime` *2020-09-16T05:50:31.0025302Z,* il est converti en *2020-09-16T05:50:31.002Z* lorsque le message est saturé.</span><span class="sxs-lookup"><span data-stu-id="d4335-175">For example, if the incoming request message has the value of `createdDateTime` set as *2020-09-16T05:50:31.0025302Z*, then it would be converted to *2020-09-16T05:50:31.002Z* when the message is ingested.</span></span>

#### <a name="request-post-message-that-is-text-only"></a><span data-ttu-id="d4335-176">Demande (message POST en texte uniquement)</span><span class="sxs-lookup"><span data-stu-id="d4335-176">Request (POST message that is text-only)</span></span>

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

#### <a name="response"></a><span data-ttu-id="d4335-177">Réponse</span><span class="sxs-lookup"><span data-stu-id="d4335-177">Response</span></span>

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

#### <a name="error-messages"></a><span data-ttu-id="d4335-178">Messages d’erreur</span><span class="sxs-lookup"><span data-stu-id="d4335-178">Error messages</span></span>

```http
400 Bad Request
```

#### <a name="request-post-a-message-with-inline-image"></a><span data-ttu-id="d4335-179">Demander (PUBLIER un message avec une image en ligne)</span><span class="sxs-lookup"><span data-stu-id="d4335-179">Request (POST a message with inline image)</span></span>

> [!Note]
> <span data-ttu-id="d4335-180">Il n’existe aucune étendue d’autorisation spéciale dans ce scénario, car la demande fait partie de chatMessage ; Les étendues de chatMessage s’appliquent également ici.</span><span class="sxs-lookup"><span data-stu-id="d4335-180">There are no special permission scopes in this scenario since the request is part of chatMessage; scopes for chatMessage apply here as well.</span></span>

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

#### <a name="response"></a><span data-ttu-id="d4335-181">Réponse</span><span class="sxs-lookup"><span data-stu-id="d4335-181">Response</span></span>

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

## <a name="step-four-complete-migration-mode"></a><span data-ttu-id="d4335-182">Étape 4 : Terminer le mode de migration</span><span class="sxs-lookup"><span data-stu-id="d4335-182">Step Four: Complete migration mode</span></span>

<span data-ttu-id="d4335-183">Une fois le processus de migration des messages terminé, l’équipe et le canal sont sortis du mode de migration à l’aide de la  `completeMigration`  méthode.</span><span class="sxs-lookup"><span data-stu-id="d4335-183">Once the message migration process has completed, both the team and channel are taken out of migration mode using the  `completeMigration`  method.</span></span> <span data-ttu-id="d4335-184">Cette étape ouvre les ressources d’équipe et de canal pour une utilisation générale par les membres de l’équipe.</span><span class="sxs-lookup"><span data-stu-id="d4335-184">This step opens the team and channel resources for general use by team members.</span></span> <span data-ttu-id="d4335-185">L’action est liée à `team` l’instance.</span><span class="sxs-lookup"><span data-stu-id="d4335-185">The action is bound to the `team` instance.</span></span> <span data-ttu-id="d4335-186">Tous les canaux doivent être terminés hors du mode de migration pour que l’équipe puisse être terminée.</span><span class="sxs-lookup"><span data-stu-id="d4335-186">All channels must be completed out of migration mode before the team can be completed.</span></span>

#### <a name="request-end-channel-migration-mode"></a><span data-ttu-id="d4335-187">Demande (mode de migration du canal final)</span><span class="sxs-lookup"><span data-stu-id="d4335-187">Request (end channel migration mode)</span></span>

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/channels/channel-id/completeMigration

```

#### <a name="response"></a><span data-ttu-id="d4335-188">Réponse</span><span class="sxs-lookup"><span data-stu-id="d4335-188">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-team-migration-mode"></a><span data-ttu-id="d4335-189">Demande (mode de migration d’équipe de fin)</span><span class="sxs-lookup"><span data-stu-id="d4335-189">Request (end team migration mode)</span></span>

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/completeMigration
```

#### <a name="response"></a><span data-ttu-id="d4335-190">Réponse</span><span class="sxs-lookup"><span data-stu-id="d4335-190">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

* <span data-ttu-id="d4335-191">Action appelée sur un `team` `channel` ou qui n’est pas dans `migrationMode` .</span><span class="sxs-lookup"><span data-stu-id="d4335-191">Action called on a `team` or `channel` that is not in `migrationMode`.</span></span>

## <a name="step-five-add-team-members"></a><span data-ttu-id="d4335-192">Étape 5 : Ajouter des membres d’équipe</span><span class="sxs-lookup"><span data-stu-id="d4335-192">Step Five: Add team members</span></span>

<span data-ttu-id="d4335-193">Vous pouvez ajouter un membre à une équipe à l’aide de l Teams’interface utilisateur ou de Microsoft Graph API [Ajouter un](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) membre : [](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9)</span><span class="sxs-lookup"><span data-stu-id="d4335-193">You can add a member to a team [using the Teams UI](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) or Microsoft Graph [Add member](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) API:</span></span>

#### <a name="request-add-member"></a><span data-ttu-id="d4335-194">Demande (ajouter un membre)</span><span class="sxs-lookup"><span data-stu-id="d4335-194">Request (add member)</span></span>

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

#### <a name="response"></a><span data-ttu-id="d4335-195">Réponse</span><span class="sxs-lookup"><span data-stu-id="d4335-195">Response</span></span>

```http
HTTP/1.1 204 No Content
```

## <a name="tips-and-additional-information"></a><span data-ttu-id="d4335-196">Astuces et des informations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="d4335-196">Tips and additional information</span></span>

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* <span data-ttu-id="d4335-197">Une fois `completeMigration` la demande faite, vous ne pouvez pas importer d’autres messages dans l’équipe.</span><span class="sxs-lookup"><span data-stu-id="d4335-197">Once the `completeMigration` request is made, you cannot import further messages into the team.</span></span>

* <span data-ttu-id="d4335-198">Les membres de l’équipe peuvent uniquement être ajoutés à la nouvelle équipe une fois `completeMigration` que la demande a renvoyé une réponse réussie.</span><span class="sxs-lookup"><span data-stu-id="d4335-198">Team members can only be added to the new team after the `completeMigration` request has returned a successful response.</span></span>

* <span data-ttu-id="d4335-199">Limitation : les messages sont importés à 5 rps par canal.</span><span class="sxs-lookup"><span data-stu-id="d4335-199">Throttling: Messages import at 5 RPS per channel.</span></span>

* <span data-ttu-id="d4335-200">Si vous devez apporter une correction aux résultats de la migration, vous devez supprimer l’équipe et répéter les étapes pour créer l’équipe et le canal et migrer à nouveau les messages.</span><span class="sxs-lookup"><span data-stu-id="d4335-200">If you need to make a correction to the migration results, you need to delete the team and repeat the steps to create the team and channel and re-migrate the messages.</span></span>

> [!NOTE]
> <span data-ttu-id="d4335-201">Actuellement, les images inline sont le seul type de média pris en charge par le schéma d’API d’importation de message.</span><span class="sxs-lookup"><span data-stu-id="d4335-201">Currently, inline images are the only type of media supported by the import message API schema.</span></span>

##### <a name="import-content-scope"></a><span data-ttu-id="d4335-202">Importer l’étendue du contenu</span><span class="sxs-lookup"><span data-stu-id="d4335-202">Import content scope</span></span>

|<span data-ttu-id="d4335-203">Dans l’étendue</span><span class="sxs-lookup"><span data-stu-id="d4335-203">In-scope</span></span> | <span data-ttu-id="d4335-204">Actuellement hors de portée</span><span class="sxs-lookup"><span data-stu-id="d4335-204">Currently out-of-scope</span></span>|
|----------|--------------------------|
|<span data-ttu-id="d4335-205">Messages d’équipe et de canal</span><span class="sxs-lookup"><span data-stu-id="d4335-205">Team and channel messages</span></span>|<span data-ttu-id="d4335-206">1:1 et messages de conversation de groupe</span><span class="sxs-lookup"><span data-stu-id="d4335-206">1:1 and group chat messages</span></span>|
|<span data-ttu-id="d4335-207">Heure de création du message d’origine</span><span class="sxs-lookup"><span data-stu-id="d4335-207">Created time of the original message</span></span>|<span data-ttu-id="d4335-208">Canaux privés</span><span class="sxs-lookup"><span data-stu-id="d4335-208">Private channels</span></span>|
|<span data-ttu-id="d4335-209">Images inline dans le cadre du message</span><span class="sxs-lookup"><span data-stu-id="d4335-209">Inline images as part of the message</span></span>|<span data-ttu-id="d4335-210">À mentions</span><span class="sxs-lookup"><span data-stu-id="d4335-210">At mentions</span></span>|
|<span data-ttu-id="d4335-211">Liens vers des fichiers existants dans SPO/OneDrive</span><span class="sxs-lookup"><span data-stu-id="d4335-211">Links to existing files in SPO/OneDrive</span></span>|<span data-ttu-id="d4335-212">Réactions</span><span class="sxs-lookup"><span data-stu-id="d4335-212">Reactions</span></span>|
|<span data-ttu-id="d4335-213">Messages avec texte enrichi</span><span class="sxs-lookup"><span data-stu-id="d4335-213">Messages with rich text</span></span>|<span data-ttu-id="d4335-214">Vidéos</span><span class="sxs-lookup"><span data-stu-id="d4335-214">Videos</span></span>|
|<span data-ttu-id="d4335-215">Chaîne de réponse de message</span><span class="sxs-lookup"><span data-stu-id="d4335-215">Message reply chain</span></span>|<span data-ttu-id="d4335-216">Annonces</span><span class="sxs-lookup"><span data-stu-id="d4335-216">Announcements</span></span>|
|<span data-ttu-id="d4335-217">Traitement à haut débit</span><span class="sxs-lookup"><span data-stu-id="d4335-217">High throughput processing</span></span>|<span data-ttu-id="d4335-218">Extraits de code</span><span class="sxs-lookup"><span data-stu-id="d4335-218">Code snippets</span></span>|
||<span data-ttu-id="d4335-219">Autocollants</span><span class="sxs-lookup"><span data-stu-id="d4335-219">Stickers</span></span>|
||<span data-ttu-id="d4335-220">Emojis</span><span class="sxs-lookup"><span data-stu-id="d4335-220">Emojis</span></span>|
||<span data-ttu-id="d4335-221">Devis</span><span class="sxs-lookup"><span data-stu-id="d4335-221">Quotes</span></span>|
||<span data-ttu-id="d4335-222">Billets croisés entre les canaux</span><span class="sxs-lookup"><span data-stu-id="d4335-222">Cross posts between channels</span></span>|


## <a name="see-also"></a><span data-ttu-id="d4335-223">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="d4335-223">See also</span></span>

[<span data-ttu-id="d4335-224">En savoir plus sur l’intégration de Microsoft Graph et Teams microsoft</span><span class="sxs-lookup"><span data-stu-id="d4335-224">Learn more about Microsoft Graph and Teams integration</span></span>](/graph/teams-concept-overview)
