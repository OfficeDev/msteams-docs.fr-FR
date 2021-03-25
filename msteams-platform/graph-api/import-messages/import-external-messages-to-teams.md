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
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a><span data-ttu-id="2ff58-104">Importer des messages de plateforme tierces pour les équipes à l’aide de Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="2ff58-104">Import third-party platform messages to Teams using Microsoft Graph</span></span>

>[!IMPORTANT]
> <span data-ttu-id="2ff58-105">Les prévisualisations publiques de Microsoft Graph et Microsoft Teams sont disponibles pour un accès et des commentaires en avant-première.</span><span class="sxs-lookup"><span data-stu-id="2ff58-105">Microsoft Graph and Microsoft Teams public previews are available for early-access and feedback.</span></span> <span data-ttu-id="2ff58-106">Bien que cette version ait fait l’objet de tests approfondis, elle n’est pas destinée à être mise en production.</span><span class="sxs-lookup"><span data-stu-id="2ff58-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

<span data-ttu-id="2ff58-107">Avec Microsoft Graph, vous pouvez migrer l’historique des messages et les données des utilisateurs d’un système externe vers un canal Teams.</span><span class="sxs-lookup"><span data-stu-id="2ff58-107">With Microsoft Graph, you can migrate users' existing message history and data from an external system into a Teams channel.</span></span> <span data-ttu-id="2ff58-108">En permettant la recréation d’une hiérarchie de messagerie de plateforme tierce au sein de Teams, les utilisateurs peuvent poursuivre leurs communications de manière transparente et sans interruption.</span><span class="sxs-lookup"><span data-stu-id="2ff58-108">By enabling the recreation of a third-party platform messaging hierarchy inside Teams, users can continue their communications in a seamless manner and proceed without interruption.</span></span>

> [!NOTE] 
> <span data-ttu-id="2ff58-109">À l’avenir, Microsoft pourra exiger que vous ou vos clients payiez des frais supplémentaires en fonction du volume de données importées.</span><span class="sxs-lookup"><span data-stu-id="2ff58-109">In the future, Microsoft may require you or your customers to pay additional fees based on the amount of data imported.</span></span>

## <a name="import-overview"></a><span data-ttu-id="2ff58-110">Vue d’ensemble de l’importation</span><span class="sxs-lookup"><span data-stu-id="2ff58-110">Import overview</span></span>

<span data-ttu-id="2ff58-111">À un niveau élevé, le processus d’importation se compose des opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="2ff58-111">At a high level, the import process consists of the following:</span></span>

1. [<span data-ttu-id="2ff58-112">Créer une équipe avec un timestamp de retour dans le temps</span><span class="sxs-lookup"><span data-stu-id="2ff58-112">Create a team with a back-in-time timestamp</span></span>](#step-one-create-a-team)
1. [<span data-ttu-id="2ff58-113">Créer un canal avec un timestamp de retour dans le temps</span><span class="sxs-lookup"><span data-stu-id="2ff58-113">Create a channel with a back-in-time timestamp</span></span>](#step-two-create-a-channel)  
1. [<span data-ttu-id="2ff58-114">Importer des messages obsolètes dans le temps externes</span><span class="sxs-lookup"><span data-stu-id="2ff58-114">Import external back-in-time dated messages</span></span>](#step-three-import-messages)
1. [<span data-ttu-id="2ff58-115">Terminer le processus de migration des équipes et des canaux</span><span class="sxs-lookup"><span data-stu-id="2ff58-115">Complete the team and channel migration process</span></span>](#step-four-complete-migration-mode)
1. [<span data-ttu-id="2ff58-116">Ajouter des membres d’équipe</span><span class="sxs-lookup"><span data-stu-id="2ff58-116">Add team members</span></span>](#step-five-add-team-members)

## <a name="necessary-requirements"></a><span data-ttu-id="2ff58-117">Conditions requises</span><span class="sxs-lookup"><span data-stu-id="2ff58-117">Necessary requirements</span></span>

### <a name="analyze-and-prepare-message-data"></a><span data-ttu-id="2ff58-118">Analyser et préparer les données des messages</span><span class="sxs-lookup"><span data-stu-id="2ff58-118">Analyze and prepare message data</span></span>

<span data-ttu-id="2ff58-119">✔ examiner les données tierces pour déterminer ce qui sera migré.</span><span class="sxs-lookup"><span data-stu-id="2ff58-119">✔ Review the third-party data to decide what will be migrated.</span></span>  
<span data-ttu-id="2ff58-120">✔ extraire les données sélectionnées du système de conversation tiers.</span><span class="sxs-lookup"><span data-stu-id="2ff58-120">✔ Extract the selected data from the third-party chat system.</span></span>  
<span data-ttu-id="2ff58-121">✔ la structure de conversation tierce à la structure Teams.</span><span class="sxs-lookup"><span data-stu-id="2ff58-121">✔ Map the third-party chat structure to the Teams structure.</span></span>  
<span data-ttu-id="2ff58-122">✔ convertir les données d’importation au format nécessaire pour la migration.</span><span class="sxs-lookup"><span data-stu-id="2ff58-122">✔ Convert import data into format needed for migration.</span></span>  

### <a name="set-up-your-office-365-tenant"></a><span data-ttu-id="2ff58-123">Configuration de votre client Office 365</span><span class="sxs-lookup"><span data-stu-id="2ff58-123">Set up your Office 365 tenant</span></span>

<span data-ttu-id="2ff58-124">✔ s’assurer qu’un client Office 365 existe pour les données d’importation.</span><span class="sxs-lookup"><span data-stu-id="2ff58-124">✔ Ensure that an Office 365 tenant exists for the import data.</span></span> <span data-ttu-id="2ff58-125">Pour plus d’informations sur la configuration d’une location Office 365 pour *Teams,* voir , Préparer votre client [Office 365.](../../concepts/build-and-test/prepare-your-o365-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="2ff58-125">For more information on setting up an Office 365 tenancy for Teams, *see*, [Prepare your Office 365 tenant](../../concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>  
<span data-ttu-id="2ff58-126">✔ assurez-vous que les membres de l’équipe sont dans Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="2ff58-126">✔ Make sure that team members are in Azure Active Directory (AAD).</span></span>  <span data-ttu-id="2ff58-127">Pour plus *d’informations,* [voir Ajouter un nouvel](/azure/active-directory/fundamentals/add-users-azure-active-directory) utilisateur à Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2ff58-127">For more information *see* [Add a new user](/azure/active-directory/fundamentals/add-users-azure-active-directory) to Azure Active Directory.</span></span>

## <a name="step-one-create-a-team"></a><span data-ttu-id="2ff58-128">Étape 1 : Créer une équipe</span><span class="sxs-lookup"><span data-stu-id="2ff58-128">Step One: Create a team</span></span>

<span data-ttu-id="2ff58-129">Étant donné que les données existantes sont migrées, il est essentiel de maintenir les timestamps des messages d’origine et d’empêcher l’activité de messagerie pendant le processus de migration pour recréer le flux de messages existant de l’utilisateur dans Teams.</span><span class="sxs-lookup"><span data-stu-id="2ff58-129">Since existing data is being migrated, maintaining the original message timestamps and preventing messaging activity during the migration process are key to recreating the user's existing message flow in Teams.</span></span> <span data-ttu-id="2ff58-130">Pour ce faire, les résultats sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="2ff58-130">This is achieved as follows:</span></span>

> <span data-ttu-id="2ff58-131">[Créez une équipe avec](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) un timestamp de retour dans le temps à l’aide de la propriété de ressource  `createdDateTime`  d’équipe.</span><span class="sxs-lookup"><span data-stu-id="2ff58-131">[Create a new team](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) with a back-in-time timestamp using the team resource  `createdDateTime`  property.</span></span> <span data-ttu-id="2ff58-132">Placez la nouvelle équipe dans un état spécial qui interdit aux utilisateurs la plupart des activités au sein de l’équipe jusqu’à ce que le processus `migration mode` de migration soit terminé.</span><span class="sxs-lookup"><span data-stu-id="2ff58-132">Place the new team in `migration mode`, a special state that bars users from most activities within the team until the migration process is complete.</span></span> <span data-ttu-id="2ff58-133">Incluez `teamCreationMode` l’attribut d’instance avec la valeur dans la requête POST pour identifier explicitement la nouvelle équipe comme étant `migration` créée pour la migration.</span><span class="sxs-lookup"><span data-stu-id="2ff58-133">Include the `teamCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  

> <span data-ttu-id="2ff58-134">**REMARQUE**: le champ sera rempli uniquement pour les instances d’une équipe ou d’un canal `createdDateTime` qui ont été migrées.</span><span class="sxs-lookup"><span data-stu-id="2ff58-134">**NOTE**:  The `createdDateTime` field will only be populated for instances of a team or channel that have been migrated.</span></span>

<!-- markdownlint-disable MD001 -->

#### <a name="permissions"></a><span data-ttu-id="2ff58-135">Autorisations</span><span class="sxs-lookup"><span data-stu-id="2ff58-135">Permissions</span></span>

|<span data-ttu-id="2ff58-136">ScopeName</span><span class="sxs-lookup"><span data-stu-id="2ff58-136">ScopeName</span></span>|<span data-ttu-id="2ff58-137">DisplayName</span><span class="sxs-lookup"><span data-stu-id="2ff58-137">DisplayName</span></span>|<span data-ttu-id="2ff58-138">Description</span><span class="sxs-lookup"><span data-stu-id="2ff58-138">Description</span></span>|<span data-ttu-id="2ff58-139">Type</span><span class="sxs-lookup"><span data-stu-id="2ff58-139">Type</span></span>|<span data-ttu-id="2ff58-140">Consentement de l’administrateur ?</span><span class="sxs-lookup"><span data-stu-id="2ff58-140">Admin Consent?</span></span>|<span data-ttu-id="2ff58-141">Entités/API couvertes</span><span class="sxs-lookup"><span data-stu-id="2ff58-141">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="2ff58-142">Gérer la migration vers Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="2ff58-142">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="2ff58-143">Création, gestion des ressources pour la migration vers Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="2ff58-143">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="2ff58-144">**Application uniquement**</span><span class="sxs-lookup"><span data-stu-id="2ff58-144">**Application-only**</span></span>|<span data-ttu-id="2ff58-145">**Oui**</span><span class="sxs-lookup"><span data-stu-id="2ff58-145">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a><span data-ttu-id="2ff58-146">Demander (créer une équipe en état de migration)</span><span class="sxs-lookup"><span data-stu-id="2ff58-146">Request (create a team in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="2ff58-147">Réponse</span><span class="sxs-lookup"><span data-stu-id="2ff58-147">Response</span></span>

```http
HTTP/1.1 202 Accepted
Location: /teams/{teamId}/operations/{operationId}
Content-Location: /teams/{teamId}
```

#### <a name="error-messages"></a><span data-ttu-id="2ff58-148">Messages d’erreur</span><span class="sxs-lookup"><span data-stu-id="2ff58-148">Error messages</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="2ff58-149">`createdDateTime`  définie pour l’avenir.</span><span class="sxs-lookup"><span data-stu-id="2ff58-149">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="2ff58-150">`createdDateTime`  correctement spécifié, mais `teamCreationMode`  l’attribut d’instance est manquant ou a une valeur non valide.</span><span class="sxs-lookup"><span data-stu-id="2ff58-150">`createdDateTime`  correctly specified, but `teamCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-two-create-a-channel"></a><span data-ttu-id="2ff58-151">Étape 2 : Créer un canal</span><span class="sxs-lookup"><span data-stu-id="2ff58-151">Step Two: Create a channel</span></span>

<span data-ttu-id="2ff58-152">La création d’un canal pour les messages importés est similaire au scénario de création d’équipe :</span><span class="sxs-lookup"><span data-stu-id="2ff58-152">Creating a channel for the imported messages is similar to the create team scenario:</span></span>

> <span data-ttu-id="2ff58-153">[Créez un canal avec](/graph/api/channel-post?view=graph-rest-beta&tabs=http&preserve-view=true) un timestamp de retour dans le temps à l’aide de la propriété de ressource `createdDateTime` de canal.</span><span class="sxs-lookup"><span data-stu-id="2ff58-153">[Create a new channel](/graph/api/channel-post?view=graph-rest-beta&tabs=http&preserve-view=true) with a back-in-time timestamp using the channel resource `createdDateTime` property.</span></span> <span data-ttu-id="2ff58-154">Placez le nouveau canal dans , un état spécial qui interdit aux utilisateurs de la plupart des activités de conversation au sein du canal jusqu’à ce que le processus `migration mode` de migration soit terminé.</span><span class="sxs-lookup"><span data-stu-id="2ff58-154">Place the new channel in `migration mode`, a special state that bars users from most chat activities within the channel until the migration process is complete.</span></span>  <span data-ttu-id="2ff58-155">Incluez `channelCreationMode` l’attribut d’instance avec la valeur dans la requête POST pour identifier explicitement la nouvelle équipe comme `migration` étant créée pour la migration.</span><span class="sxs-lookup"><span data-stu-id="2ff58-155">Include the `channelCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  
<!-- markdownlint-disable MD024 -->
#### <a name="permissions"></a><span data-ttu-id="2ff58-156">Autorisations</span><span class="sxs-lookup"><span data-stu-id="2ff58-156">Permissions</span></span>

|<span data-ttu-id="2ff58-157">ScopeName</span><span class="sxs-lookup"><span data-stu-id="2ff58-157">ScopeName</span></span>|<span data-ttu-id="2ff58-158">DisplayName</span><span class="sxs-lookup"><span data-stu-id="2ff58-158">DisplayName</span></span>|<span data-ttu-id="2ff58-159">Description</span><span class="sxs-lookup"><span data-stu-id="2ff58-159">Description</span></span>|<span data-ttu-id="2ff58-160">Type</span><span class="sxs-lookup"><span data-stu-id="2ff58-160">Type</span></span>|<span data-ttu-id="2ff58-161">Consentement de l’administrateur ?</span><span class="sxs-lookup"><span data-stu-id="2ff58-161">Admin Consent?</span></span>|<span data-ttu-id="2ff58-162">Entités/API couvertes</span><span class="sxs-lookup"><span data-stu-id="2ff58-162">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="2ff58-163">Gérer la migration vers Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="2ff58-163">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="2ff58-164">Création, gestion des ressources pour la migration vers Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="2ff58-164">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="2ff58-165">**Application uniquement**</span><span class="sxs-lookup"><span data-stu-id="2ff58-165">**Application-only**</span></span>|<span data-ttu-id="2ff58-166">**Oui**</span><span class="sxs-lookup"><span data-stu-id="2ff58-166">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a><span data-ttu-id="2ff58-167">Demande (créer un canal dans l’état de migration)</span><span class="sxs-lookup"><span data-stu-id="2ff58-167">Request (create a channel in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="2ff58-168">Réponse</span><span class="sxs-lookup"><span data-stu-id="2ff58-168">Response</span></span>

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

#### <a name="error-message"></a><span data-ttu-id="2ff58-169">Message d’erreur</span><span class="sxs-lookup"><span data-stu-id="2ff58-169">Error message</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="2ff58-170">`createdDateTime`  définie pour l’avenir.</span><span class="sxs-lookup"><span data-stu-id="2ff58-170">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="2ff58-171">`createdDateTime`  correctement spécifié, mais `channelCreationMode`  l’attribut d’instance est manquant ou a une valeur non valide.</span><span class="sxs-lookup"><span data-stu-id="2ff58-171">`createdDateTime`  correctly specified but `channelCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-three-import-messages"></a><span data-ttu-id="2ff58-172">Étape 3 : Importer des messages</span><span class="sxs-lookup"><span data-stu-id="2ff58-172">Step Three: Import messages</span></span>

<span data-ttu-id="2ff58-173">Une fois l’équipe et le canal créés, vous pouvez commencer à envoyer des messages dans le temps à l’aide des clés dans `createdDateTime`  le corps de la `from`  demande.</span><span class="sxs-lookup"><span data-stu-id="2ff58-173">After the team and channel have been created, you can begin sending back-in-time messages using the `createdDateTime`  and `from`  keys in the request body.</span></span> <span data-ttu-id="2ff58-174">**REMARQUE**: les messages importés avec des threads de messages antérieures ne `createdDateTime` sont pas pris en `createdDateTime` charge.</span><span class="sxs-lookup"><span data-stu-id="2ff58-174">**NOTE**: messages imported with `createdDateTime` earlier than the message thread `createdDateTime` is not supported.</span></span>

> [!NOTE]
> * <span data-ttu-id="2ff58-175">`createdDateTime` doit être unique entre les messages dans le même thread.</span><span class="sxs-lookup"><span data-stu-id="2ff58-175">`createdDateTime` must be unique across messages in the same thread.</span></span>
> * <span data-ttu-id="2ff58-176">`createdDateTime` prend en charge les timestamps avec une précision en millisecondes.</span><span class="sxs-lookup"><span data-stu-id="2ff58-176">`createdDateTime` supports timestamps with milliseconds precision.</span></span> <span data-ttu-id="2ff58-177">Par exemple, si la valeur du message de demande entrante est définie sur `createdDateTime` *2020-09-16T05:50:31.0025302Z,* il est converti en *2020-09-16T05:50:31.002Z* lorsque le message est saturé.</span><span class="sxs-lookup"><span data-stu-id="2ff58-177">For example, if the incoming request message has the value of `createdDateTime` set as *2020-09-16T05:50:31.0025302Z*, then it would be converted to *2020-09-16T05:50:31.002Z* when the message is ingested.</span></span>

#### <a name="request-post-message-that-is-text-only"></a><span data-ttu-id="2ff58-178">Demande (message POST en texte uniquement)</span><span class="sxs-lookup"><span data-stu-id="2ff58-178">Request (POST message that is text-only)</span></span>

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

#### <a name="response"></a><span data-ttu-id="2ff58-179">Réponse</span><span class="sxs-lookup"><span data-stu-id="2ff58-179">Response</span></span>

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

#### <a name="error-messages"></a><span data-ttu-id="2ff58-180">Messages d’erreur</span><span class="sxs-lookup"><span data-stu-id="2ff58-180">Error messages</span></span>

```http
400 Bad Request
```

#### <a name="request-post-a-message-with-inline-image"></a><span data-ttu-id="2ff58-181">Demander (PUBLIER un message avec une image fixe)</span><span class="sxs-lookup"><span data-stu-id="2ff58-181">Request (POST a message with inline image)</span></span>

> <span data-ttu-id="2ff58-182">**Remarque**: il n’existe aucune étendue d’autorisation spéciale dans ce scénario, car la demande fait partie de chatMessage ; Les étendues de chatMessage s’appliquent également ici.</span><span class="sxs-lookup"><span data-stu-id="2ff58-182">**Note**: There are no special permission scopes in this scenario since the request is part of chatMessage; scopes for chatMessage apply here as well.</span></span>

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

#### <a name="response"></a><span data-ttu-id="2ff58-183">Réponse</span><span class="sxs-lookup"><span data-stu-id="2ff58-183">Response</span></span>

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

## <a name="step-four-complete-migration-mode"></a><span data-ttu-id="2ff58-184">Étape 4 : Terminer le mode de migration</span><span class="sxs-lookup"><span data-stu-id="2ff58-184">Step Four: Complete migration mode</span></span>

<span data-ttu-id="2ff58-185">Une fois le processus de migration des messages terminé, l’équipe et le canal sont sortis du mode de migration à l’aide de la  `completeMigration`  méthode.</span><span class="sxs-lookup"><span data-stu-id="2ff58-185">Once the message migration process has completed, both the team and channel are taken out of migration mode using the  `completeMigration`  method.</span></span> <span data-ttu-id="2ff58-186">Cette étape ouvre les ressources d’équipe et de canal pour une utilisation générale par les membres de l’équipe.</span><span class="sxs-lookup"><span data-stu-id="2ff58-186">This step opens the team and channel resources for general use by team members.</span></span> <span data-ttu-id="2ff58-187">L’action est liée à `team` l’instance.</span><span class="sxs-lookup"><span data-stu-id="2ff58-187">The action is bound to the `team` instance.</span></span>

#### <a name="request-end-team-migration-mode"></a><span data-ttu-id="2ff58-188">Demande (mode de migration d’équipe de fin)</span><span class="sxs-lookup"><span data-stu-id="2ff58-188">Request (end team migration mode)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/completeMigration

```

#### <a name="response"></a><span data-ttu-id="2ff58-189">Réponse</span><span class="sxs-lookup"><span data-stu-id="2ff58-189">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-channel-migration-mode"></a><span data-ttu-id="2ff58-190">Demande (mode de migration du canal final)</span><span class="sxs-lookup"><span data-stu-id="2ff58-190">Request (end channel migration mode)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/completeMigration

```

#### <a name="response"></a><span data-ttu-id="2ff58-191">Réponse</span><span class="sxs-lookup"><span data-stu-id="2ff58-191">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="error-response"></a><span data-ttu-id="2ff58-192">Réponse d’erreur</span><span class="sxs-lookup"><span data-stu-id="2ff58-192">Error response</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="2ff58-193">Action appelée sur un `team` `channel` ou qui n’est pas dans `migrationMode` .</span><span class="sxs-lookup"><span data-stu-id="2ff58-193">Action called on a `team` or `channel` that is not in `migrationMode`.</span></span>

## <a name="step-five-add-team-members"></a><span data-ttu-id="2ff58-194">Étape 5 : Ajouter des membres d’équipe</span><span class="sxs-lookup"><span data-stu-id="2ff58-194">Step Five: Add team members</span></span>

<span data-ttu-id="2ff58-195">Vous pouvez ajouter un membre à une équipe à [l’aide](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) de l’interface utilisateur Teams ou de l’API Ajouter [un membre](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) Microsoft Graph :</span><span class="sxs-lookup"><span data-stu-id="2ff58-195">You can add a member to a team [using the Teams UI](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) or Microsoft Graph [Add member](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) API:</span></span>

#### <a name="request-add-member"></a><span data-ttu-id="2ff58-196">Demande (ajouter un membre)</span><span class="sxs-lookup"><span data-stu-id="2ff58-196">Request (add member)</span></span>

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

#### <a name="response"></a><span data-ttu-id="2ff58-197">Réponse</span><span class="sxs-lookup"><span data-stu-id="2ff58-197">Response</span></span>

```http
HTTP/1.1 204 No Content
```

## <a name="tips-and-additional-information"></a><span data-ttu-id="2ff58-198">Conseils et informations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="2ff58-198">Tips and additional information</span></span>

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* <span data-ttu-id="2ff58-199">Vous pouvez importer des messages provenant d’utilisateurs qui ne sont pas dans Teams.</span><span class="sxs-lookup"><span data-stu-id="2ff58-199">You can import messages from users who are not in Teams.</span></span> <span data-ttu-id="2ff58-200">**REMARQUE**: les messages importés pour les utilisateurs non présents dans le client ne seront pas accessibles dans le client Teams ou les portails de conformité lors de la prévisualisation publique.</span><span class="sxs-lookup"><span data-stu-id="2ff58-200">**NOTE**: Messages imported for users not present in the tenant will not be searchable in the Teams client or compliance portals during Public Preview.</span></span>

* <span data-ttu-id="2ff58-201">Une fois `completeMigration` la demande faite, vous ne pouvez pas importer d’autres messages dans l’équipe.</span><span class="sxs-lookup"><span data-stu-id="2ff58-201">Once the `completeMigration` request is made, you cannot import further messages into the team.</span></span>

* <span data-ttu-id="2ff58-202">Les membres de l’équipe peuvent uniquement être ajoutés à la nouvelle équipe une fois `completeMigration` que la demande a renvoyé une réponse réussie.</span><span class="sxs-lookup"><span data-stu-id="2ff58-202">Team members can only be added to the new team after the `completeMigration` request has returned a successful response.</span></span>

* <span data-ttu-id="2ff58-203">Limitation : les messages sont importés à 5 rps par canal.</span><span class="sxs-lookup"><span data-stu-id="2ff58-203">Throttling: Messages import at 5 RPS per channel.</span></span>

* <span data-ttu-id="2ff58-204">Si vous devez apporter une correction aux résultats de la migration, vous devez supprimer l’équipe et répéter les étapes pour créer l’équipe et le canal et migrer à nouveau les messages.</span><span class="sxs-lookup"><span data-stu-id="2ff58-204">If you need to make a correction to the migration results, you need to delete the team and repeat the steps to create the team and channel and re-migrate the messages.</span></span>

> [!NOTE]
> <span data-ttu-id="2ff58-205">Actuellement, les images inline sont le seul type de média pris en charge par le schéma d’API d’importation de message.</span><span class="sxs-lookup"><span data-stu-id="2ff58-205">Currently, inline images are the only type of media supported by the import message API schema.</span></span>

##### <a name="import-content-scope"></a><span data-ttu-id="2ff58-206">Importer l’étendue du contenu</span><span class="sxs-lookup"><span data-stu-id="2ff58-206">Import content scope</span></span>

|<span data-ttu-id="2ff58-207">Dans l’étendue</span><span class="sxs-lookup"><span data-stu-id="2ff58-207">In-scope</span></span> | <span data-ttu-id="2ff58-208">Actuellement hors de portée</span><span class="sxs-lookup"><span data-stu-id="2ff58-208">Currently out-of-scope</span></span>|
|----------|--------------------------|
|<span data-ttu-id="2ff58-209">Messages d’équipe et de canal</span><span class="sxs-lookup"><span data-stu-id="2ff58-209">Team and channel messages</span></span>|<span data-ttu-id="2ff58-210">1:1 et messages de conversation de groupe</span><span class="sxs-lookup"><span data-stu-id="2ff58-210">1:1 and group chat messages</span></span>|
|<span data-ttu-id="2ff58-211">Heure de création du message d’origine</span><span class="sxs-lookup"><span data-stu-id="2ff58-211">Created time of the original message</span></span>|<span data-ttu-id="2ff58-212">Canaux privés</span><span class="sxs-lookup"><span data-stu-id="2ff58-212">Private channels</span></span>|
|<span data-ttu-id="2ff58-213">Images inline dans le cadre du message</span><span class="sxs-lookup"><span data-stu-id="2ff58-213">Inline images as part of the message</span></span>|<span data-ttu-id="2ff58-214">À mentions</span><span class="sxs-lookup"><span data-stu-id="2ff58-214">At mentions</span></span>|
|<span data-ttu-id="2ff58-215">Liens vers des fichiers existants dans SPO/OneDrive</span><span class="sxs-lookup"><span data-stu-id="2ff58-215">Links to existing files in SPO/OneDrive</span></span>|<span data-ttu-id="2ff58-216">Réactions</span><span class="sxs-lookup"><span data-stu-id="2ff58-216">Reactions</span></span>|
|<span data-ttu-id="2ff58-217">Messages avec texte enrichi</span><span class="sxs-lookup"><span data-stu-id="2ff58-217">Messages with rich text</span></span>|<span data-ttu-id="2ff58-218">Vidéos</span><span class="sxs-lookup"><span data-stu-id="2ff58-218">Videos</span></span>|
|<span data-ttu-id="2ff58-219">Chaîne de réponse de message</span><span class="sxs-lookup"><span data-stu-id="2ff58-219">Message reply chain</span></span>|<span data-ttu-id="2ff58-220">Annonces</span><span class="sxs-lookup"><span data-stu-id="2ff58-220">Announcements</span></span>|
|<span data-ttu-id="2ff58-221">Traitement à haut débit</span><span class="sxs-lookup"><span data-stu-id="2ff58-221">High throughput processing</span></span>|<span data-ttu-id="2ff58-222">Extraits de code</span><span class="sxs-lookup"><span data-stu-id="2ff58-222">Code snippets</span></span>|
||<span data-ttu-id="2ff58-223">Cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="2ff58-223">Adaptive cards</span></span>|
||<span data-ttu-id="2ff58-224">Autocollants</span><span class="sxs-lookup"><span data-stu-id="2ff58-224">Stickers</span></span>|
||<span data-ttu-id="2ff58-225">Emojis</span><span class="sxs-lookup"><span data-stu-id="2ff58-225">Emojis</span></span>|
||<span data-ttu-id="2ff58-226">Guillemets</span><span class="sxs-lookup"><span data-stu-id="2ff58-226">Quotes</span></span>|
||<span data-ttu-id="2ff58-227">Billets croisés entre les canaux</span><span class="sxs-lookup"><span data-stu-id="2ff58-227">Cross posts between channels</span></span>|


## <a name="see-also"></a><span data-ttu-id="2ff58-228">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="2ff58-228">See also</span></span>
> [!div class="nextstepaction"]
>[<span data-ttu-id="2ff58-229">En savoir plus sur l’intégration de Microsoft Graph et Teams</span><span class="sxs-lookup"><span data-stu-id="2ff58-229">Learn more about Microsoft Graph and Teams integration</span></span>](/graph/teams-concept-overview)
