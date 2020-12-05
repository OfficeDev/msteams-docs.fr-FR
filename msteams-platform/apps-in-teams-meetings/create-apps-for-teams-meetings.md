---
title: Créer des applications pour les réunions Teams
author: laujan
description: créer des applications pour les réunions teams
ms.topic: conceptual
ms.author: lajanuar
keywords: applications Team Apps Meeting User Role Role API
ms.openlocfilehash: 1be9763bdd81bdff7fa2a6f5b44d936dced6755a
ms.sourcegitcommit: 50571f5c6afc86177c4fe1032fe13366a7b706dd
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/04/2020
ms.locfileid: "49576826"
---
# <a name="create-apps-for-teams-meetings"></a><span data-ttu-id="a619a-104">Créer des applications pour les réunions Teams</span><span class="sxs-lookup"><span data-stu-id="a619a-104">Create apps for Teams meetings</span></span>

## <a name="prerequisites-and-considerations"></a><span data-ttu-id="a619a-105">Conditions préalables et considérations</span><span class="sxs-lookup"><span data-stu-id="a619a-105">Prerequisites and considerations</span></span>

1. <span data-ttu-id="a619a-106">Les applications dans les réunions nécessitent des connaissances de base sur le [développement d’applications teams](../overview.md).</span><span class="sxs-lookup"><span data-stu-id="a619a-106">Apps in meetings require some basic knowledge of [Teams app development](../overview.md).</span></span> <span data-ttu-id="a619a-107">Une application dans une réunion peut comprendre des fonctionnalités d' [onglets](../tabs/what-are-tabs.md), de [robots](../bots/what-are-bots.md)et d' [extensions de messagerie](../messaging-extensions/what-are-messaging-extensions.md) , et nécessitera des mises à jour du manifeste d' [application](#update-your-app-manifest) teams pour indiquer que l’application est disponible pour les réunions.</span><span class="sxs-lookup"><span data-stu-id="a619a-107">An app in a meeting can comprise of [tabs](../tabs/what-are-tabs.md), [bots](../bots/what-are-bots.md), and [messaging extensions](../messaging-extensions/what-are-messaging-extensions.md) features and will require updates to the Teams [app manifest](#update-your-app-manifest) to indicate that the app is available for meetings</span></span>

1. <span data-ttu-id="a619a-108">Pour que votre application fonctionne dans le cycle de vie de la réunion sous la forme d’un onglet, elle doit prendre en charge les onglets configurables dans l' [étendue groupchat](../resources/schema/manifest-schema.md#configurabletabs).</span><span class="sxs-lookup"><span data-stu-id="a619a-108">For your app to function in the meeting lifecycle as a tab, it must support configurable tabs in the [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs).</span></span> <span data-ttu-id="a619a-109">*Voir* [étendre votre application teams avec un onglet personnalisé](../tabs/how-to/add-tab.md). La prise en charge de l' `groupchat` étendue activera votre application dans les conversations [pré-réunion](teams-apps-in-meetings.md#pre-meeting-app-experience) et [post-réunion](teams-apps-in-meetings.md#post-meeting-app-experience) .</span><span class="sxs-lookup"><span data-stu-id="a619a-109">*See* [Extend your Teams app with a custom tab](../tabs/how-to/add-tab.md). Supporting the `groupchat` scope will enable your app in [pre-meeting](teams-apps-in-meetings.md#pre-meeting-app-experience) and [post-meeting](teams-apps-in-meetings.md#post-meeting-app-experience) chats.</span></span>

1. <span data-ttu-id="a619a-110">Les paramètres de l’URL de l’API de réunion peuvent exiger `meetingId` , `userId` et les [tenantId](/onedrive/find-your-office-365-tenant-id) disponibles dans le cadre du kit de développement logiciel client teams et de l’activité du robot.</span><span class="sxs-lookup"><span data-stu-id="a619a-110">Meeting API URL parameters may require `meetingId`, `userId`, and the [tenantId](/onedrive/find-your-office-365-tenant-id) These are available as part of the Teams Client SDK and bot activity.</span></span> <span data-ttu-id="a619a-111">En outre, des informations fiables pour l’ID d’utilisateur et l’ID de client peuvent être récupérées à l’aide de [l’authentification SSO de tabulation](../tabs/how-to/authentication/auth-aad-sso.md).</span><span class="sxs-lookup"><span data-stu-id="a619a-111">Additionally, reliable information for user ID and tenant ID can be retrieved using [Tab SSO authentication](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>

1. <span data-ttu-id="a619a-112">Certaines API de réunion, telles que `GetParticipant` nécessiteront un [ID d’enregistrement et d’application bot](../bots/how-to/create-a-bot-for-teams.md#with-an-azure-subscription) pour générer des jetons d’authentification.</span><span class="sxs-lookup"><span data-stu-id="a619a-112">Some meeting APIs, such as `GetParticipant` will require a [bot registration and bot app ID](../bots/how-to/create-a-bot-for-teams.md#with-an-azure-subscription) to generate auth tokens.</span></span>

1. <span data-ttu-id="a619a-113">En tant que développeur, vous devez respecter les [instructions de conception d’onglet teams](../tabs/design/tabs.md) générales pour les scénarios pré-et post-réunion, ainsi que les [recommandations](design/designing-in-meeting-dialog.md) pour la boîte de dialogue de réunion déclenchée lors d’une réunion Teams.</span><span class="sxs-lookup"><span data-stu-id="a619a-113">As a developer, you must adhere to general [Teams tab design guidelines](../tabs/design/tabs.md) for pre- and post-meeting scenarios as well as the [in-meeting dialog guidelines](design/designing-in-meeting-dialog.md) for in-meeting dialog triggered during a Teams meeting.</span></span>

1. <span data-ttu-id="a619a-114">Veuillez noter que pour que votre application soit mise à jour en temps réel, elle doit être à jour en fonction des activités liées aux événements dans la réunion.</span><span class="sxs-lookup"><span data-stu-id="a619a-114">Please note that in order for your app to be updated in real-time, it must be up-to-date based on event activities in the meeting.</span></span> <span data-ttu-id="a619a-115">Ces événements peuvent se situer dans la boîte de dialogue de réunion (reportez-vous à la rubrique Complete `bot Id` Parameter in `Notification Signal API` ) et d’autres surfaces dans le cycle de vie de la réunion.</span><span class="sxs-lookup"><span data-stu-id="a619a-115">These events can be within the in-meeting dialog (refer to completion `bot Id` parameter in `Notification Signal API`) and other surfaces across the meeting lifecycle</span></span>

## <a name="meeting-apps-api-reference"></a><span data-ttu-id="a619a-116">Référence de l’API des applications de réunion</span><span class="sxs-lookup"><span data-stu-id="a619a-116">Meeting apps API reference</span></span>

|<span data-ttu-id="a619a-117">API</span><span class="sxs-lookup"><span data-stu-id="a619a-117">API</span></span>|<span data-ttu-id="a619a-118">Description</span><span class="sxs-lookup"><span data-stu-id="a619a-118">Description</span></span>|<span data-ttu-id="a619a-119">Demande</span><span class="sxs-lookup"><span data-stu-id="a619a-119">Request</span></span>|<span data-ttu-id="a619a-120">Source</span><span class="sxs-lookup"><span data-stu-id="a619a-120">Source</span></span>|
|---|---|----|---|
|<span data-ttu-id="a619a-121">**GetUserContext**</span><span class="sxs-lookup"><span data-stu-id="a619a-121">**GetUserContext**</span></span>| <span data-ttu-id="a619a-122">Obtenir des informations contextuelles pour afficher le contenu pertinent dans un onglet Teams.</span><span class="sxs-lookup"><span data-stu-id="a619a-122">Get contextual information to display relevant content in a Teams tab.</span></span> |<span data-ttu-id="a619a-123">_**microsoftTeams. getContext (() => {/*...\* / } )*\*_</span><span class="sxs-lookup"><span data-stu-id="a619a-123">_**microsoftTeams.getContext( ( ) => {  /*...*/ } )**_</span></span>|<span data-ttu-id="a619a-124">Kit de développement logiciel client Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="a619a-124">Microsoft Teams client SDK</span></span>|
|<span data-ttu-id="a619a-125">**GetParticipant**</span><span class="sxs-lookup"><span data-stu-id="a619a-125">**GetParticipant**</span></span>|<span data-ttu-id="a619a-126">Cette API permet à un bot d’extraire des informations sur les participants par ID de réunion et ID de participant.</span><span class="sxs-lookup"><span data-stu-id="a619a-126">This API allows a bot to fetch a participant information by meeting id and participant id.</span></span>|<span data-ttu-id="a619a-127">**Obtenir** _**/v1/meetings/{meetingId}/participants/{participantId} ? tenantId = {tenantId}**_</span><span class="sxs-lookup"><span data-stu-id="a619a-127">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span></span> |<span data-ttu-id="a619a-128">Kit de développement logiciel (SDK) Microsoft bot Framework</span><span class="sxs-lookup"><span data-stu-id="a619a-128">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="a619a-129">**NotificationSignal**</span><span class="sxs-lookup"><span data-stu-id="a619a-129">**NotificationSignal**</span></span> |<span data-ttu-id="a619a-130">Les signaux de réunion seront remis à l’aide de l’API de notification de conversation existante suivante (pour la conversation utilisateur-bot).</span><span class="sxs-lookup"><span data-stu-id="a619a-130">Meeting signals will be delivered using the following existing conversation notification API (for user-bot chat).</span></span> <span data-ttu-id="a619a-131">Cette API permet aux développeurs de signaler en fonction de l’action de l’utilisateur final à afficher-case une bulle de dialogue de réunion.</span><span class="sxs-lookup"><span data-stu-id="a619a-131">This API allows developers to signal based on end-user action to show-case an in-meeting dialog bubble.</span></span>|<span data-ttu-id="a619a-132">**Post** _**/v3/conversations/{conversationId}/Activities**_</span><span class="sxs-lookup"><span data-stu-id="a619a-132">**POST** _**/v3/conversations/{conversationId}/activities**_</span></span>|<span data-ttu-id="a619a-133">Kit de développement logiciel (SDK) Microsoft bot Framework</span><span class="sxs-lookup"><span data-stu-id="a619a-133">Microsoft Bot Framework SDK</span></span>|

### <a name="getusercontext"></a><span data-ttu-id="a619a-134">GetUserContext</span><span class="sxs-lookup"><span data-stu-id="a619a-134">GetUserContext</span></span>

<span data-ttu-id="a619a-135">Pour obtenir des instructions sur l’identification et la récupération des informations contextuelles pour votre contenu d’onglet, consultez notre [contexte de l’onglet teams](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) .</span><span class="sxs-lookup"><span data-stu-id="a619a-135">Please refer to our [Get context for your Teams tab](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) documentation for guidance on identifying and  retrieving contextual information for your tab content.</span></span> <span data-ttu-id="a619a-136">Dans le cadre de l’extensibilité des réunions, une nouvelle valeur a été ajoutée pour la charge utile de la réponse :</span><span class="sxs-lookup"><span data-stu-id="a619a-136">As part of meetings extensibility, a new value has been added for the response payload:</span></span>

<span data-ttu-id="a619a-137">✔ **meetingId**: utilisé par un onglet lors de l’exécution dans le contexte de la réunion.</span><span class="sxs-lookup"><span data-stu-id="a619a-137">✔ **meetingId**: used by a tab when running in the meeting context.</span></span>

### <a name="getparticipant-api"></a><span data-ttu-id="a619a-138">API GetParticipant</span><span class="sxs-lookup"><span data-stu-id="a619a-138">GetParticipant API</span></span>

> [!NOTE]
>
> * <span data-ttu-id="a619a-139">Ne pas mettre en cache les rôles des participants étant donné que l’organisateur de la réunion peut modifier un rôle à tout moment.</span><span class="sxs-lookup"><span data-stu-id="a619a-139">Do not cache participant roles since the meeting organizer can change a role at any point in time.</span></span>
>
> * <span data-ttu-id="a619a-140">Teams ne prend actuellement pas en charge les listes de distribution volumineuses ni les tailles de liste de plus de 350 participants pour l' `GetParticipant` API.</span><span class="sxs-lookup"><span data-stu-id="a619a-140">Teams does not currently support large distribution lists or roster sizes of more than 350 participants for the `GetParticipant` API.</span></span>
>
> * <span data-ttu-id="a619a-141">La prise en charge du kit de développement logiciel (SDK) de robot sera bientôt disponible.</span><span class="sxs-lookup"><span data-stu-id="a619a-141">Support for the Bot Framework SDK is coming soon.</span></span>


#### <a name="request"></a><span data-ttu-id="a619a-142">Demande</span><span class="sxs-lookup"><span data-stu-id="a619a-142">Request</span></span>

```http
GET /v3/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

<span data-ttu-id="a619a-143">*Voir* la référence de l’API de l' [infrastructure bot](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="a619a-143">*See* the [Bot Framework API reference](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<!-- markdownlint-disable MD025 -->

<span data-ttu-id="a619a-144">**Exemple C#**</span><span class="sxs-lookup"><span data-stu-id="a619a-144">**C# Example**</span></span>

```csharp
   // Get role for the user who sent a message to your bot
   var senderRole = await TeamsInfo.GetMeetingParticipantAsync(turnContext);
```

* * *
<!-- markdownlint-disable MD001 -->

#### <a name="query-parameters"></a><span data-ttu-id="a619a-145">Paramètres de requête</span><span class="sxs-lookup"><span data-stu-id="a619a-145">Query parameters</span></span>

|<span data-ttu-id="a619a-146">Valeur</span><span class="sxs-lookup"><span data-stu-id="a619a-146">Value</span></span>|<span data-ttu-id="a619a-147">Type</span><span class="sxs-lookup"><span data-stu-id="a619a-147">Type</span></span>|<span data-ttu-id="a619a-148">Requis</span><span class="sxs-lookup"><span data-stu-id="a619a-148">Required</span></span>|<span data-ttu-id="a619a-149">Description</span><span class="sxs-lookup"><span data-stu-id="a619a-149">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="a619a-150">**meetingId**</span><span class="sxs-lookup"><span data-stu-id="a619a-150">**meetingId**</span></span>| <span data-ttu-id="a619a-151">string</span><span class="sxs-lookup"><span data-stu-id="a619a-151">string</span></span> | <span data-ttu-id="a619a-152">Oui</span><span class="sxs-lookup"><span data-stu-id="a619a-152">Yes</span></span> | <span data-ttu-id="a619a-153">L’identificateur de réunion est disponible via le kit de développement logiciel (SDK) et teams Client SDK.</span><span class="sxs-lookup"><span data-stu-id="a619a-153">The meeting identifier is available via Bot Invoke and Teams Client SDK.</span></span>|
|<span data-ttu-id="a619a-154">**participantId**</span><span class="sxs-lookup"><span data-stu-id="a619a-154">**participantId**</span></span>| <span data-ttu-id="a619a-155">string</span><span class="sxs-lookup"><span data-stu-id="a619a-155">string</span></span> | <span data-ttu-id="a619a-156">Oui</span><span class="sxs-lookup"><span data-stu-id="a619a-156">Yes</span></span> | <span data-ttu-id="a619a-157">Ce champ est le nom d’utilisateur et est disponible dans les onglets SSO, d’appel de bot et teams Client SDK.</span><span class="sxs-lookup"><span data-stu-id="a619a-157">This field is the User ID and it is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="a619a-158">L’authentification unique de l’onglet est fortement recommandée</span><span class="sxs-lookup"><span data-stu-id="a619a-158">Tab SSO is highly recommended</span></span>|
|<span data-ttu-id="a619a-159">**tenantId**</span><span class="sxs-lookup"><span data-stu-id="a619a-159">**tenantId**</span></span>| <span data-ttu-id="a619a-160">string</span><span class="sxs-lookup"><span data-stu-id="a619a-160">string</span></span> | <span data-ttu-id="a619a-161">Oui</span><span class="sxs-lookup"><span data-stu-id="a619a-161">Yes</span></span> | <span data-ttu-id="a619a-162">Cela est nécessaire pour les utilisateurs clients.</span><span class="sxs-lookup"><span data-stu-id="a619a-162">This required for tenant users.</span></span> <span data-ttu-id="a619a-163">Elle est disponible dans les kits de développement logiciel SSO, de robot et teams client.</span><span class="sxs-lookup"><span data-stu-id="a619a-163">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="a619a-164">L’authentification unique de l’onglet est fortement recommandée</span><span class="sxs-lookup"><span data-stu-id="a619a-164">Tab SSO is highly recommended</span></span>|

#### <a name="response-payload"></a><span data-ttu-id="a619a-165">Charge utile de réponse</span><span class="sxs-lookup"><span data-stu-id="a619a-165">Response Payload</span></span>
<!-- markdownlint-disable MD036 -->

<span data-ttu-id="a619a-166">le **rôle** sous « réunion » peut être *organisateur*, *présentateur* ou *participant*.</span><span class="sxs-lookup"><span data-stu-id="a619a-166">**role** under "meeting" can be *Organizer*, *Presenter*, or *Attendee*.</span></span>

<span data-ttu-id="a619a-167">**Exemple 1**</span><span class="sxs-lookup"><span data-stu-id="a619a-167">**Example 1**</span></span>

```json
{
   "user":{
      "id":"29:1JKiJGPAX9TTxtGxhVo0wLx_zwzo-gG8Z-X03306vBwi9p-xMTEbDXsT6KH7-0kkTS8cD-2zkrsoV6f5WJ6_aYw",
      "aadObjectId":"6aebbad0-e5a5-424a-834a-20fb051f3c1a",
      "name":"Allan Deyoung",
      "givenName":"Allan",
      "surname":"Deyoung",
      "email":"Allan.Deyoung@microsoft.com",
      "userPrincipalName":"Allan.Deyoung@microsoft.com",
      "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47",
      "userRole":"user"
   },
   "meeting":{
      "role ":"Presenter",
      "inMeeting":true
   },
   "conversation":{
      "id":"<conversation id>",
      "isGroup":true
   }
}
```
#### <a name="response-codes"></a><span data-ttu-id="a619a-168">Codes de réponse</span><span class="sxs-lookup"><span data-stu-id="a619a-168">Response Codes</span></span>

<span data-ttu-id="a619a-169">**403**: l’application n’est pas autorisée à obtenir des informations sur les participants.</span><span class="sxs-lookup"><span data-stu-id="a619a-169">**403**: The app is not allowed to get participant information.</span></span> <span data-ttu-id="a619a-170">Il s’agit de la réponse d’erreur la plus courante, qui est déclenchée lorsque l’application n’est pas installée dans la réunion, par exemple lorsqu’elle est désactivée par l’administrateur client ou bloquée lors de la migration de site réel.</span><span class="sxs-lookup"><span data-stu-id="a619a-170">This will be the most common error response and is triggered when the app is not installed in the meeting such as when it is disabled by tenant admin or blocked during live site migration.</span></span>  
<span data-ttu-id="a619a-171">**200**: les informations sur les participants ont été récupérées.</span><span class="sxs-lookup"><span data-stu-id="a619a-171">**200**: Participant information successfully retrieved.</span></span>  
<span data-ttu-id="a619a-172">**401**: jeton non valide.</span><span class="sxs-lookup"><span data-stu-id="a619a-172">**401**: Invalid token.</span></span>  
<span data-ttu-id="a619a-173">**404**: le participant est introuvable.</span><span class="sxs-lookup"><span data-stu-id="a619a-173">**404**: Participant cannot be found.</span></span> 
<span data-ttu-id="a619a-174">**500**: la réunion a expiré (plus de 60 jours après la fin de la réunion) ou le participant ne dispose pas d’autorisations en fonction de son rôle.</span><span class="sxs-lookup"><span data-stu-id="a619a-174">**500**: The meeting is either expired (more than 60 days since the meeting ended) or the participant does not have permissions based on their role.</span></span>

<span data-ttu-id="a619a-175">**Bientôt disponible**</span><span class="sxs-lookup"><span data-stu-id="a619a-175">**Coming Soon**</span></span>

<span data-ttu-id="a619a-176">**404**: la réunion a expiré ou le participant est introuvable.</span><span class="sxs-lookup"><span data-stu-id="a619a-176">**404**: the meeting has either expired or participant cannot be found.</span></span> 

<!-- markdownlint-disable MD024 -->
### <a name="notificationsignal-api"></a><span data-ttu-id="a619a-177">API NotificationSignal</span><span class="sxs-lookup"><span data-stu-id="a619a-177">NotificationSignal API</span></span>

> [!NOTE]
> <span data-ttu-id="a619a-178">Lorsqu’une boîte de dialogue de réunion est appelée, le même contenu s’affiche également sous la forme d’un message de conversation.</span><span class="sxs-lookup"><span data-stu-id="a619a-178">When an in-meeting dialog is invoked, the same content will also be presented as a chat message.</span></span>

#### <a name="request"></a><span data-ttu-id="a619a-179">Demande</span><span class="sxs-lookup"><span data-stu-id="a619a-179">Request</span></span>

```http
POST /v3/conversations/{conversationId}/activities
```

#### <a name="query-parameters"></a><span data-ttu-id="a619a-180">Paramètres de requête</span><span class="sxs-lookup"><span data-stu-id="a619a-180">Query parameters</span></span>

|<span data-ttu-id="a619a-181">Valeur</span><span class="sxs-lookup"><span data-stu-id="a619a-181">Value</span></span>|<span data-ttu-id="a619a-182">Type</span><span class="sxs-lookup"><span data-stu-id="a619a-182">Type</span></span>|<span data-ttu-id="a619a-183">Requis</span><span class="sxs-lookup"><span data-stu-id="a619a-183">Required</span></span>|<span data-ttu-id="a619a-184">Description</span><span class="sxs-lookup"><span data-stu-id="a619a-184">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="a619a-185">**conversationId**</span><span class="sxs-lookup"><span data-stu-id="a619a-185">**conversationId**</span></span>| <span data-ttu-id="a619a-186">string</span><span class="sxs-lookup"><span data-stu-id="a619a-186">string</span></span> | <span data-ttu-id="a619a-187">Oui</span><span class="sxs-lookup"><span data-stu-id="a619a-187">Yes</span></span> | <span data-ttu-id="a619a-188">L’identificateur de conversation est disponible dans le cadre de l’appel de bot.</span><span class="sxs-lookup"><span data-stu-id="a619a-188">The conversation identifier is available as part of bot invoke</span></span> |

#### <a name="request-payload"></a><span data-ttu-id="a619a-189">Charge utile de la demande</span><span class="sxs-lookup"><span data-stu-id="a619a-189">Request Payload</span></span>

> [!NOTE]
>
> *  <span data-ttu-id="a619a-190">Dans la charge demandée ci-dessous, le `completionBotId` paramètre de `externalResourceUrl` est un facultatif.</span><span class="sxs-lookup"><span data-stu-id="a619a-190">In the requested payload below, the `completionBotId` parameter of the `externalResourceUrl`is an optional.</span></span> <span data-ttu-id="a619a-191">Il s’agit de la `Bot ID` qui est déclarée dans le manifeste.</span><span class="sxs-lookup"><span data-stu-id="a619a-191">It is the `Bot ID` that is declared in the manifest.</span></span> <span data-ttu-id="a619a-192">Le bot reçoit un objet de résultat.</span><span class="sxs-lookup"><span data-stu-id="a619a-192">The bot will receive a result object.</span></span>
> * <span data-ttu-id="a619a-193">Les paramètres de largeur et de hauteur externalResourceUrl doivent être en pixels.</span><span class="sxs-lookup"><span data-stu-id="a619a-193">The externalResourceUrl width and height parameters must be in pixels.</span></span> <span data-ttu-id="a619a-194">Reportez-vous aux [instructions de conception](design/designing-in-meeting-dialog.md) pour vous assurer que les dimensions respectent les limites autorisées.</span><span class="sxs-lookup"><span data-stu-id="a619a-194">Refer to the [design guidelines](design/designing-in-meeting-dialog.md) to ensure the dimensions are within the allowed limits.</span></span>
> * <span data-ttu-id="a619a-195">L’URL est la page chargée en tant que telle dans `<iframe>` la boîte de dialogue de réunion.</span><span class="sxs-lookup"><span data-stu-id="a619a-195">The URL is the page loaded as an `<iframe>` inside the in-meeting dialog.</span></span> <span data-ttu-id="a619a-196">Le domaine de l’URL doit se trouver dans le tableau de l’application `validDomains` dans le manifeste de votre application.</span><span class="sxs-lookup"><span data-stu-id="a619a-196">The URL's domain must be in the app's `validDomains` array in your app manifest.</span></span>


# <a name="json"></a>[<span data-ttu-id="a619a-197">JSON</span><span class="sxs-lookup"><span data-stu-id="a619a-197">JSON</span></span>](#tab/json)

```json
{
    "type": "message",
    "text": "John Phillips assigned you a weekly todo",
    "summary": "Don't forget to meet with Marketing next week",
    "channelData": {
        "notification": {
            "alertInMeeting": true,
            "externalResourceUrl": "https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID"
        }
    },
    "replyToId": "1493070356924"
}
```

# <a name="cnet"></a>[<span data-ttu-id="a619a-198">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="a619a-198">C#/.NET</span></span>](#tab/dotnet)

```csharp
Activity activity = MessageFactory.Text("This is a meeting signal test");

activity.ChannelData = new TeamsChannelData
  {
    Notification = new NotificationInfo()
                    {
                        AlertInMeeting = true,
                        ExternalResourceUrl = "https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID"
                    }
  };
await turnContext.SendActivityAsync(activity).ConfigureAwait(false);
```

# <a name="javascript"></a>[<span data-ttu-id="a619a-199">JavaScript</span><span class="sxs-lookup"><span data-stu-id="a619a-199">JavaScript</span></span>](#tab/javascript)

```javascript

const replyActivity = MessageFactory.text('Hi'); // this could be an adaptive card instead
replyActivity.channelData = {
    notification: {
        alertInMeeting: true,
        externalResourceUrl: 'https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID’
    }
};
await context.sendActivity(replyActivity);
```

* * *

> [!IMPORTANT]
> <span data-ttu-id="a619a-200">L’URL dans la bulle de contenu (URL de taskInfo) doit être incluse dans la liste des [domaines valide](../resources/schema/manifest-schema.md#validdomains) incluse dans le manifeste de l’application Teams.</span><span class="sxs-lookup"><span data-stu-id="a619a-200">The URL in the content bubble (taskInfo URL) must be included in the [valid domains](../resources/schema/manifest-schema.md#validdomains) list included in the Teams app manifest.</span></span>

#### <a name="response-codes"></a><span data-ttu-id="a619a-201">Codes de réponse</span><span class="sxs-lookup"><span data-stu-id="a619a-201">Response Codes</span></span>

<span data-ttu-id="a619a-202">**201**: l’activité avec le signal est correctement envoyée</span><span class="sxs-lookup"><span data-stu-id="a619a-202">**201**: activity with signal is successfully sent</span></span>  
<span data-ttu-id="a619a-203">**401**: jeton non valide</span><span class="sxs-lookup"><span data-stu-id="a619a-203">**401**: invalid token</span></span>  
<span data-ttu-id="a619a-204">**403**: l’application n’est pas autorisée à envoyer le signal.</span><span class="sxs-lookup"><span data-stu-id="a619a-204">**403**: the app is not allowed to send the signal.</span></span> <span data-ttu-id="a619a-205">Dans ce cas, la charge utile doit contenir plus de détails sur les messages d’erreur.</span><span class="sxs-lookup"><span data-stu-id="a619a-205">In this case, the payload should contain more detail error message.</span></span> <span data-ttu-id="a619a-206">Il peut y avoir plusieurs raisons : l’application est désactivée par l’administrateur client, bloquée lors de la limitation du site actif, etc.</span><span class="sxs-lookup"><span data-stu-id="a619a-206">There can be many reasons: app disabled by tenant admin, blocked during live site mitigation, etc.</span></span>  
<span data-ttu-id="a619a-207">**404**: la conversation de réunion n’existe pas</span><span class="sxs-lookup"><span data-stu-id="a619a-207">**404**: meeting chat doesn't exist</span></span>  

## <a name="enable-your-app-for-teams-meetings"></a><span data-ttu-id="a619a-208">Activer votre application pour les réunions teams</span><span class="sxs-lookup"><span data-stu-id="a619a-208">Enable your app for Teams meetings</span></span>

### <a name="update-your-app-manifest"></a><span data-ttu-id="a619a-209">Mettre à jour le manifeste de votre application</span><span class="sxs-lookup"><span data-stu-id="a619a-209">Update your app manifest</span></span>

<span data-ttu-id="a619a-210">Les fonctionnalités des applications de réunion sont déclarées dans le manifeste **configurableTabs** de votre application via les  ->  **étendues** configurableTabs et les tableaux de **contexte** .</span><span class="sxs-lookup"><span data-stu-id="a619a-210">The meetings app capabilities are declared in your app manifest via the **configurableTabs** -> **scopes** and **context** arrays.</span></span> <span data-ttu-id="a619a-211">L' *étendue* définit la personne et le *contexte* définissant où votre application sera disponible.</span><span class="sxs-lookup"><span data-stu-id="a619a-211">*Scope* defines to whom and *context* defines where your app will be available.</span></span>

> [!NOTE]
> * <span data-ttu-id="a619a-212">Veuillez utiliser le [schéma de manifeste d’aperçu développeur](../resources/schema/manifest-schema-dev-preview.md) pour essayer cela dans le manifeste de votre application.</span><span class="sxs-lookup"><span data-stu-id="a619a-212">Please use [Developer Preview manifest schema](../resources/schema/manifest-schema-dev-preview.md) to try this in your app manifest.</span></span>

```json
"configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "canUpdateConfiguration": true,
      "scopes": [
        "team",
        "groupchat"
      ],
      "context":[
        "channelTab",
        "privateChatTab",
        "meetingChatTab",
        "meetingDetailsTab",
        "meetingSidePanel"
     ]
    }
  ]
```

### <a name="context-property"></a><span data-ttu-id="a619a-213">Context, propriété</span><span class="sxs-lookup"><span data-stu-id="a619a-213">Context property</span></span>

<span data-ttu-id="a619a-214">L’onglet `context` et les `scopes` propriétés fonctionnent en harmonie pour vous permettre de déterminer où vous souhaitez que votre application apparaisse.</span><span class="sxs-lookup"><span data-stu-id="a619a-214">The tab `context` and `scopes` properties work in harmony to allow you to determine where you want your app to appear.</span></span> <span data-ttu-id="a619a-215">Les onglets de l' `team` `groupchat` étendue ou peuvent avoir plusieurs contextes.</span><span class="sxs-lookup"><span data-stu-id="a619a-215">Tabs in the `team` or `groupchat` scope can have more than one context.</span></span> <span data-ttu-id="a619a-216">Les valeurs possibles pour la propriété Context sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="a619a-216">The possible values for the context property are as follows:</span></span>

* <span data-ttu-id="a619a-217">**channelTab**: onglet de l’en-tête d’un canal d’équipe.</span><span class="sxs-lookup"><span data-stu-id="a619a-217">**channelTab**: a tab in the header of a team channel.</span></span>
* <span data-ttu-id="a619a-218">**privateChatTab**: onglet de l’en-tête d’une conversation de groupe entre un ensemble d’utilisateurs qui n’est pas dans le contexte d’une équipe ou d’une réunion.</span><span class="sxs-lookup"><span data-stu-id="a619a-218">**privateChatTab**: a tab in the header of a group chat between a set of users not in the context of a team or meeting.</span></span>
* <span data-ttu-id="a619a-219">**meetingChatTab**: onglet de l’en-tête d’une conversation de groupe entre un ensemble d’utilisateurs dans le contexte d’une réunion planifiée.</span><span class="sxs-lookup"><span data-stu-id="a619a-219">**meetingChatTab**: a tab in the header of a group chat between a set of users in the context of a scheduled meeting.</span></span>
* <span data-ttu-id="a619a-220">**meetingDetailsTab**: onglet de l’en-tête de l’affichage Détails de la réunion du calendrier.</span><span class="sxs-lookup"><span data-stu-id="a619a-220">**meetingDetailsTab**: a tab in the header of the meeting details view of the calendar.</span></span>
* <span data-ttu-id="a619a-221">**meetingSidePanel**: un panneau de réunion ouvert par le biais de la barre unifiée (u-bar).</span><span class="sxs-lookup"><span data-stu-id="a619a-221">**meetingSidePanel**: an in-meeting panel opened via the unified bar (u-bar).</span></span>

> [!NOTE]
> <span data-ttu-id="a619a-222">La propriété « Context » n’est pas prise en charge actuellement et sera donc ignorée sur les clients mobiles</span><span class="sxs-lookup"><span data-stu-id="a619a-222">"Context" property is currently not supported and thus will be ignored on mobile clients</span></span>

## <a name="configure-your-app-for-meeting-scenarios"></a><span data-ttu-id="a619a-223">Configurer votre application pour les scénarios de réunion</span><span class="sxs-lookup"><span data-stu-id="a619a-223">Configure your app for meeting scenarios</span></span>

> [!NOTE]
> * <span data-ttu-id="a619a-224">Pour que votre application soit visible dans la Galerie d’onglets, elle doit **prendre en charge les onglets configurables** et l' **étendue de conversation de groupe**.</span><span class="sxs-lookup"><span data-stu-id="a619a-224">For your app to be visible in the tab gallery it needs to **support configurable tabs** and the **group chat scope**.</span></span>
>
> * <span data-ttu-id="a619a-225">Les clients mobiles prennent en charge les onglets uniquement dans les surfaces pre et post Meeting.</span><span class="sxs-lookup"><span data-stu-id="a619a-225">Mobile clients support Tabs only in Pre and Post Meeting Surfaces.</span></span> <span data-ttu-id="a619a-226">Les expériences de réunion (boîte de dialogue et volet de réunion) sur mobile seront bientôt disponibles.</span><span class="sxs-lookup"><span data-stu-id="a619a-226">The In-meeting experiences (in-meeting dialog and panel) on mobile will be available soon.</span></span> <span data-ttu-id="a619a-227">Suivez les [instructions pour les onglets sur mobile](../tabs/design/tabs-mobile.md) lors de la création de vos onglets pour mobile.</span><span class="sxs-lookup"><span data-stu-id="a619a-227">Follow the [guidance for tabs on mobile](../tabs/design/tabs-mobile.md) when creating your tabs for mobile.</span></span> 

### <a name="pre-meeting"></a><span data-ttu-id="a619a-228">Pré-réunion</span><span class="sxs-lookup"><span data-stu-id="a619a-228">Pre-meeting</span></span>

<span data-ttu-id="a619a-229">Les utilisateurs disposant de rôles d’organisateur et/ou de présentateur ajoutent des onglets à une réunion en utilisant le bouton plus ➕ dans les pages **conversation** de réunion et **Détails** de la réunion.</span><span class="sxs-lookup"><span data-stu-id="a619a-229">Users with organizer and/or presenter roles add tabs to a meeting using the plus ➕ button in the meeting **Chat** and meeting **details** pages.</span></span> <span data-ttu-id="a619a-230">Les extensions de messagerie sont ajoutées à via le menu ellipses/Overflow &#x25CF;&#x25CF;&#x25CF; située sous la zone de message composer dans la conversation.</span><span class="sxs-lookup"><span data-stu-id="a619a-230">Messaging extensions are added to via the ellipses/overflow menu &#x25CF;&#x25CF;&#x25CF; located beneath the compose message area in the chat.</span></span> <span data-ttu-id="a619a-231">Les robots sont ajoutés à une conversation de réunion à l’aide de la **@** touche «» et en sélectionnant **obtenir les bots**.</span><span class="sxs-lookup"><span data-stu-id="a619a-231">Bots are added to a meeting chat using the "**@**" key and selecting **Get bots**.</span></span>

<span data-ttu-id="a619a-232">✔ L’identité de l’utilisateur *doit* être confirmée via les [onglets SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span><span class="sxs-lookup"><span data-stu-id="a619a-232">✔ The user identity *must* be confirmed via [Tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="a619a-233">À la suite de cette authentification, l’application peut récupérer le rôle d’utilisateur via l’API GetParticipant.</span><span class="sxs-lookup"><span data-stu-id="a619a-233">Following this authentication, the app can retrieve the user role via the GetParticipant API.</span></span>

 <span data-ttu-id="a619a-234">✔ En fonction du rôle d’utilisateur, l’application est désormais capable de présenter des expériences spécifiques de rôle.</span><span class="sxs-lookup"><span data-stu-id="a619a-234">✔ Based on the user role, the app will now have the capability to present role specific experiences.</span></span> <span data-ttu-id="a619a-235">Par exemple, une application d’interrogation peut autoriser uniquement les organisateurs et les présentateurs à créer une nouvelle interrogation.</span><span class="sxs-lookup"><span data-stu-id="a619a-235">For example, a polling app can allow only organizers and presenters to create a new poll.</span></span>

> <span data-ttu-id="a619a-236">**Remarque**: les attributions de rôles peuvent être modifiées lorsqu’une réunion est en cours.</span><span class="sxs-lookup"><span data-stu-id="a619a-236">**NOTE**: Role assignments can be changed while a meeting is in progress.</span></span>  <span data-ttu-id="a619a-237">*Voir* [rôles dans une réunion teams](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span><span class="sxs-lookup"><span data-stu-id="a619a-237">*See* [Roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span> 

### <a name="in-meeting"></a><span data-ttu-id="a619a-238">Réunion</span><span class="sxs-lookup"><span data-stu-id="a619a-238">In-meeting</span></span>

#### <a name="sidepanel"></a><span data-ttu-id="a619a-239">**sidePanel**</span><span class="sxs-lookup"><span data-stu-id="a619a-239">**sidePanel**</span></span>

<span data-ttu-id="a619a-240">✔ Dans votre manifeste d’application, ajoutez **sidePanel** au tableau de **contexte** , comme décrit ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="a619a-240">✔ In your app manifest add **sidePanel** to the **context** array as described above.</span></span>

<span data-ttu-id="a619a-241">✔ Dans la réunion, ainsi que dans tous les scénarios, l’application sera affichée sous la forme d’un onglet dans la réunion 320 px.</span><span class="sxs-lookup"><span data-stu-id="a619a-241">✔ In the meeting as well as in all scenarios, the app will be rendered in an in-meeting tab that is 320px in width.</span></span> <span data-ttu-id="a619a-242">Pour ce faire, vous devez optimiser l’onglet.</span><span class="sxs-lookup"><span data-stu-id="a619a-242">Your tab must be optimized for this.</span></span> <span data-ttu-id="a619a-243">*Voir*, [interface FrameContext](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)</span><span class="sxs-lookup"><span data-stu-id="a619a-243">*See*, [FrameContext interface](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)</span></span>

<span data-ttu-id="a619a-244">✔ Reportez-vous au [Kit de développement logiciel teams](../tabs/how-to/access-teams-context.md#user-context) pour utiliser l’API **userContext** pour acheminer les demandes en conséquence.</span><span class="sxs-lookup"><span data-stu-id="a619a-244">✔Refer to the [Teams SDK](../tabs/how-to/access-teams-context.md#user-context) to use the **userContext** API to route requests accordingly.</span></span>

<span data-ttu-id="a619a-245">✔ Reportez-vous au [flux d’authentification teams pour les onglets](../tabs/how-to/authentication/auth-flow-tab.md).</span><span class="sxs-lookup"><span data-stu-id="a619a-245">✔ Refer to the [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span> <span data-ttu-id="a619a-246">Le flux d’authentification des onglets est très similaire au flux d’authentification pour les sites Web.</span><span class="sxs-lookup"><span data-stu-id="a619a-246">Authentication flow for tabs is very similar to the auth flow for websites.</span></span> <span data-ttu-id="a619a-247">Par conséquent, les onglets peuvent utiliser OAuth 2,0 directement.</span><span class="sxs-lookup"><span data-stu-id="a619a-247">Thus, tabs can use OAuth 2.0 directly.</span></span> <span data-ttu-id="a619a-248">*Voir aussi* la [plateforme d’identité Microsoft et le flux de code d’autorisation OAuth 2,0](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span><span class="sxs-lookup"><span data-stu-id="a619a-248">*See also*, [Microsoft identity platform and OAuth 2.0 authorization code flow](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span></span>

<span data-ttu-id="a619a-249">✔ Extension de message doit fonctionner comme prévu lorsqu’un utilisateur est dans une vue de réunion et doit être en mesure de publier des cartes d’extension de message de composition.</span><span class="sxs-lookup"><span data-stu-id="a619a-249">✔ Message extension should work as expected when a user is in an in-meeting view and should be able to post compose message extension cards.</span></span>

<span data-ttu-id="a619a-250">✔ AppName dans la réunion-ToolTip doit indiquer le nom de l’application dans la barre U de la réunion.</span><span class="sxs-lookup"><span data-stu-id="a619a-250">✔ AppName in-meeting - Tooltip should state the app name in-meeting U-bar.</span></span>

#### <a name="in-meeting-dialog"></a><span data-ttu-id="a619a-251">**boîte de dialogue de réunion**</span><span class="sxs-lookup"><span data-stu-id="a619a-251">**in-meeting dialog**</span></span>

<span data-ttu-id="a619a-252">✔ Vous devez respecter les [instructions de conception de la boîte de dialogue de réunion](design/designing-in-meeting-dialog.md).</span><span class="sxs-lookup"><span data-stu-id="a619a-252">✔ You must adhere to the [in-meeting dialog design guidelines](design/designing-in-meeting-dialog.md).</span></span>

<span data-ttu-id="a619a-253">✔ Reportez-vous au [flux d’authentification teams pour les onglets](../tabs/how-to/authentication/auth-flow-tab.md).</span><span class="sxs-lookup"><span data-stu-id="a619a-253">✔ Refer to the [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span>

<span data-ttu-id="a619a-254">✔ Utiliser l’API de [notification](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) pour signaler qu’une notification de bulle doit être déclenchée.</span><span class="sxs-lookup"><span data-stu-id="a619a-254">✔ Use the [notification](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) API to signal that a bubble notification needs to be triggered.</span></span>

<span data-ttu-id="a619a-255">✔ Dans le cadre de la charge utile de la demande de notification, incluez l’URL où le contenu à présenter est hébergé.</span><span class="sxs-lookup"><span data-stu-id="a619a-255">✔ As part of the notification request payload, include the URL where the content to be showcased is hosted.</span></span>

<span data-ttu-id="a619a-256">✔ Boîte de dialogue de réunion ne doit pas utiliser le module tâches.</span><span class="sxs-lookup"><span data-stu-id="a619a-256">✔ In-meeting dialog must not use task module.</span></span>

> [!NOTE]
>
> * <span data-ttu-id="a619a-257">Ces notifications sont permanentes.</span><span class="sxs-lookup"><span data-stu-id="a619a-257">These notifications are persistent in nature.</span></span> <span data-ttu-id="a619a-258">Vous devez appeler la fonction [**submitTask ()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) pour faire une fermeture automatique après qu’un utilisateur a effectué une action dans l’affichage Web.</span><span class="sxs-lookup"><span data-stu-id="a619a-258">You must invoke the [**submitTask()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) function to auto-dismiss after a user takes an action in the web-view.</span></span> <span data-ttu-id="a619a-259">Il s’agit d’une condition requise pour l’envoi d’une application.</span><span class="sxs-lookup"><span data-stu-id="a619a-259">This is a requirement for app submission.</span></span> <span data-ttu-id="a619a-260">*Voir aussi*, [Kit de développement logiciel (SDK) teams : module de tâches](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="a619a-260">*See also*, [Teams SDK: task module](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span></span>
>
> * <span data-ttu-id="a619a-261">Si vous souhaitez que votre application prenne en charge les utilisateurs anonymes, votre charge utile de la demande d’appel initiale doit reposer sur les métadonnées de demande `from.id`  (ID de l’utilisateur) dans l' `from` objet, et non sur l' `from.aadObjectId` ID (Azure Active Directory ID de l’utilisateur).</span><span class="sxs-lookup"><span data-stu-id="a619a-261">If you want your app to support anonymous users, your initial invoke request payload must rely on the `from.id`  (ID of the user) request metadata in the `from` object, not the `from.aadObjectId` (Azure Active Directory ID of the user) request metadata.</span></span> <span data-ttu-id="a619a-262">*Voir* [utilisation des modules de tâches dans les onglets](../task-modules-and-cards/task-modules/task-modules-tabs.md) et [créer et envoyer le module de tâches](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).</span><span class="sxs-lookup"><span data-stu-id="a619a-262">*See* [Using task modules in tabs](../task-modules-and-cards/task-modules/task-modules-tabs.md) and [Create and send the task module](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).</span></span>

### <a name="post-meeting"></a><span data-ttu-id="a619a-263">Post-réunion</span><span class="sxs-lookup"><span data-stu-id="a619a-263">Post-meeting</span></span>

<span data-ttu-id="a619a-264">Les configurations post-réunion et de réunion sont équivalentes.</span><span class="sxs-lookup"><span data-stu-id="a619a-264">The post-meeting and pre-meeting configurations are equivalent.</span></span>

## <a name="meeting-app-sample"></a><span data-ttu-id="a619a-265">Exemple d’application de réunion</span><span class="sxs-lookup"><span data-stu-id="a619a-265">Meeting app sample</span></span>

 > [!div class="nextstepaction"]
> [<span data-ttu-id="a619a-266">Application du générateur de jetons de réunion</span><span class="sxs-lookup"><span data-stu-id="a619a-266">Meeting token generator app</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token)
