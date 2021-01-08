---
title: Créer des applications pour les réunions Teams
author: laujan
description: créer des applications pour les réunions teams
ms.topic: conceptual
ms.author: lajanuar
keywords: applications Team Apps Meeting User Role Role API
ms.openlocfilehash: e768c2dc6722d006c89927adfe60e03243a076d0
ms.sourcegitcommit: f0dfae429385ef02f61896ad49172c4803ef6622
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/31/2020
ms.locfileid: "49740870"
---
# <a name="create-apps-for-teams-meetings"></a><span data-ttu-id="f787e-104">Créer des applications pour les réunions Teams</span><span class="sxs-lookup"><span data-stu-id="f787e-104">Create apps for Teams meetings</span></span>

## <a name="prerequisites-and-considerations"></a><span data-ttu-id="f787e-105">Conditions préalables et considérations</span><span class="sxs-lookup"><span data-stu-id="f787e-105">Prerequisites and considerations</span></span>

1. <span data-ttu-id="f787e-106">Les applications dans les réunions nécessitent des connaissances de base sur le [développement d’applications teams](../overview.md).</span><span class="sxs-lookup"><span data-stu-id="f787e-106">Apps in meetings require some basic knowledge of [Teams app development](../overview.md).</span></span> <span data-ttu-id="f787e-107">Une application dans une réunion peut comprendre des fonctionnalités d' [onglets](../tabs/what-are-tabs.md), de [robots](../bots/what-are-bots.md)et d' [extensions de messagerie](../messaging-extensions/what-are-messaging-extensions.md) , et nécessitera des mises à jour du manifeste d' [application](#update-your-app-manifest) teams pour indiquer que l’application est disponible pour les réunions.</span><span class="sxs-lookup"><span data-stu-id="f787e-107">An app in a meeting can comprise of [tabs](../tabs/what-are-tabs.md), [bots](../bots/what-are-bots.md), and [messaging extensions](../messaging-extensions/what-are-messaging-extensions.md) features and will require updates to the Teams [app manifest](#update-your-app-manifest) to indicate that the app is available for meetings</span></span>

1. <span data-ttu-id="f787e-108">Pour que votre application fonctionne dans le cycle de vie de la réunion sous la forme d’un onglet, elle doit prendre en charge les onglets configurables dans l' [étendue groupchat](../resources/schema/manifest-schema.md#configurabletabs).</span><span class="sxs-lookup"><span data-stu-id="f787e-108">For your app to function in the meeting lifecycle as a tab, it must support configurable tabs in the [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs).</span></span> <span data-ttu-id="f787e-109">*Voir* [étendre votre application teams avec un onglet personnalisé](../tabs/how-to/add-tab.md). La prise en charge de l' `groupchat` étendue activera votre application dans les conversations [pré-réunion](teams-apps-in-meetings.md#pre-meeting-app-experience) et [post-réunion](teams-apps-in-meetings.md#post-meeting-app-experience) .</span><span class="sxs-lookup"><span data-stu-id="f787e-109">*See* [Extend your Teams app with a custom tab](../tabs/how-to/add-tab.md). Supporting the `groupchat` scope will enable your app in [pre-meeting](teams-apps-in-meetings.md#pre-meeting-app-experience) and [post-meeting](teams-apps-in-meetings.md#post-meeting-app-experience) chats.</span></span>

1. <span data-ttu-id="f787e-110">Les paramètres de l’URL de l’API de réunion peuvent exiger `meetingId` , `userId` et les [tenantId](/onedrive/find-your-office-365-tenant-id) disponibles dans le cadre du kit de développement logiciel client teams et de l’activité du robot.</span><span class="sxs-lookup"><span data-stu-id="f787e-110">Meeting API URL parameters may require `meetingId`, `userId`, and the [tenantId](/onedrive/find-your-office-365-tenant-id) These are available as part of the Teams Client SDK and bot activity.</span></span> <span data-ttu-id="f787e-111">En outre, des informations fiables pour l’ID d’utilisateur et l’ID de client peuvent être récupérées à l’aide de [l’authentification SSO de tabulation](../tabs/how-to/authentication/auth-aad-sso.md).</span><span class="sxs-lookup"><span data-stu-id="f787e-111">Additionally, reliable information for user ID and tenant ID can be retrieved using [Tab SSO authentication](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>

1. <span data-ttu-id="f787e-112">Certaines API de réunion, telles que `GetParticipant` nécessiteront un [ID d’enregistrement et d’application bot](../bots/how-to/create-a-bot-for-teams.md#with-an-azure-subscription) pour générer des jetons d’authentification.</span><span class="sxs-lookup"><span data-stu-id="f787e-112">Some meeting APIs, such as `GetParticipant` will require a [bot registration and bot app ID](../bots/how-to/create-a-bot-for-teams.md#with-an-azure-subscription) to generate auth tokens.</span></span>

1. <span data-ttu-id="f787e-113">En tant que développeur, vous devez respecter les [instructions de conception d’onglet teams](../tabs/design/tabs.md) générales pour les scénarios pré-et post-réunion, ainsi que les [recommandations](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog) pour la boîte de dialogue de réunion déclenchée lors d’une réunion Teams.</span><span class="sxs-lookup"><span data-stu-id="f787e-113">As a developer, you must adhere to general [Teams tab design guidelines](../tabs/design/tabs.md) for pre- and post-meeting scenarios as well as the [in-meeting dialog guidelines](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog) for in-meeting dialog triggered during a Teams meeting.</span></span>

1. <span data-ttu-id="f787e-114">Veuillez noter que pour que votre application soit mise à jour en temps réel, elle doit être à jour en fonction des activités liées aux événements dans la réunion.</span><span class="sxs-lookup"><span data-stu-id="f787e-114">Please note that in order for your app to be updated in real-time, it must be up-to-date based on event activities in the meeting.</span></span> <span data-ttu-id="f787e-115">Ces événements peuvent se situer dans la boîte de dialogue de réunion (reportez-vous à la rubrique Complete `bot Id` Parameter in `Notification Signal API` ) et d’autres surfaces dans le cycle de vie de la réunion.</span><span class="sxs-lookup"><span data-stu-id="f787e-115">These events can be within the in-meeting dialog (refer to completion `bot Id` parameter in `Notification Signal API`) and other surfaces across the meeting lifecycle</span></span>

## <a name="meeting-apps-api-reference"></a><span data-ttu-id="f787e-116">Référence de l’API des applications de réunion</span><span class="sxs-lookup"><span data-stu-id="f787e-116">Meeting apps API reference</span></span>

|<span data-ttu-id="f787e-117">API</span><span class="sxs-lookup"><span data-stu-id="f787e-117">API</span></span>|<span data-ttu-id="f787e-118">Description</span><span class="sxs-lookup"><span data-stu-id="f787e-118">Description</span></span>|<span data-ttu-id="f787e-119">Demande</span><span class="sxs-lookup"><span data-stu-id="f787e-119">Request</span></span>|<span data-ttu-id="f787e-120">Source</span><span class="sxs-lookup"><span data-stu-id="f787e-120">Source</span></span>|
|---|---|----|---|
|<span data-ttu-id="f787e-121">**GetUserContext**</span><span class="sxs-lookup"><span data-stu-id="f787e-121">**GetUserContext**</span></span>| <span data-ttu-id="f787e-122">Obtenir des informations contextuelles pour afficher le contenu pertinent dans un onglet Teams.</span><span class="sxs-lookup"><span data-stu-id="f787e-122">Get contextual information to display relevant content in a Teams tab.</span></span> |<span data-ttu-id="f787e-123">_**microsoftTeams. getContext (() => {/*...\* / } )*\*_</span><span class="sxs-lookup"><span data-stu-id="f787e-123">_**microsoftTeams.getContext( ( ) => {  /*...*/ } )**_</span></span>|<span data-ttu-id="f787e-124">Kit de développement logiciel client Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="f787e-124">Microsoft Teams client SDK</span></span>|
|<span data-ttu-id="f787e-125">**GetParticipant**</span><span class="sxs-lookup"><span data-stu-id="f787e-125">**GetParticipant**</span></span>|<span data-ttu-id="f787e-126">Cette API permet à un bot d’extraire des informations sur les participants par ID de réunion et ID de participant.</span><span class="sxs-lookup"><span data-stu-id="f787e-126">This API allows a bot to fetch a participant information by meeting id and participant id.</span></span>|<span data-ttu-id="f787e-127">**Obtenir** _**/v1/meetings/{meetingId}/participants/{participantId} ? tenantId = {tenantId}**_</span><span class="sxs-lookup"><span data-stu-id="f787e-127">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span></span> |<span data-ttu-id="f787e-128">Kit de développement logiciel (SDK) Microsoft bot Framework</span><span class="sxs-lookup"><span data-stu-id="f787e-128">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="f787e-129">**NotificationSignal**</span><span class="sxs-lookup"><span data-stu-id="f787e-129">**NotificationSignal**</span></span> |<span data-ttu-id="f787e-130">Les signaux de réunion seront remis à l’aide de l’API de notification de conversation existante suivante (pour la conversation utilisateur-bot).</span><span class="sxs-lookup"><span data-stu-id="f787e-130">Meeting signals will be delivered using the following existing conversation notification API (for user-bot chat).</span></span> <span data-ttu-id="f787e-131">Cette API permet aux développeurs de signaler en fonction de l’action de l’utilisateur final à afficher-case une bulle de dialogue de réunion.</span><span class="sxs-lookup"><span data-stu-id="f787e-131">This API allows developers to signal based on end-user action to show-case an in-meeting dialog bubble.</span></span>|<span data-ttu-id="f787e-132">**Post** _**/v3/conversations/{conversationId}/Activities**_</span><span class="sxs-lookup"><span data-stu-id="f787e-132">**POST** _**/v3/conversations/{conversationId}/activities**_</span></span>|<span data-ttu-id="f787e-133">Kit de développement logiciel (SDK) Microsoft bot Framework</span><span class="sxs-lookup"><span data-stu-id="f787e-133">Microsoft Bot Framework SDK</span></span>|

### <a name="getusercontext"></a><span data-ttu-id="f787e-134">GetUserContext</span><span class="sxs-lookup"><span data-stu-id="f787e-134">GetUserContext</span></span>

<span data-ttu-id="f787e-135">Pour obtenir des instructions sur l’identification et la récupération des informations contextuelles pour votre contenu d’onglet, consultez notre [contexte de l’onglet teams](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) .</span><span class="sxs-lookup"><span data-stu-id="f787e-135">Please refer to our [Get context for your Teams tab](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) documentation for guidance on identifying and  retrieving contextual information for your tab content.</span></span> <span data-ttu-id="f787e-136">Dans le cadre de l’extensibilité des réunions, une nouvelle valeur a été ajoutée pour la charge utile de la réponse :</span><span class="sxs-lookup"><span data-stu-id="f787e-136">As part of meetings extensibility, a new value has been added for the response payload:</span></span>

<span data-ttu-id="f787e-137">✔ **meetingId**: utilisé par un onglet lors de l’exécution dans le contexte de la réunion.</span><span class="sxs-lookup"><span data-stu-id="f787e-137">✔ **meetingId**: used by a tab when running in the meeting context.</span></span>

### <a name="getparticipant-api"></a><span data-ttu-id="f787e-138">API GetParticipant</span><span class="sxs-lookup"><span data-stu-id="f787e-138">GetParticipant API</span></span>

> [!NOTE]
>
> * <span data-ttu-id="f787e-139">Ne pas mettre en cache les rôles des participants étant donné que l’organisateur de la réunion peut modifier un rôle à tout moment.</span><span class="sxs-lookup"><span data-stu-id="f787e-139">Do not cache participant roles since the meeting organizer can change a role at any point in time.</span></span>
>
> * <span data-ttu-id="f787e-140">Teams ne prend actuellement pas en charge les listes de distribution volumineuses ni les tailles de liste de plus de 350 participants pour l' `GetParticipant` API.</span><span class="sxs-lookup"><span data-stu-id="f787e-140">Teams does not currently support large distribution lists or roster sizes of more than 350 participants for the `GetParticipant` API.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="f787e-141">Paramètres de requête</span><span class="sxs-lookup"><span data-stu-id="f787e-141">Query parameters</span></span>

|<span data-ttu-id="f787e-142">Valeur</span><span class="sxs-lookup"><span data-stu-id="f787e-142">Value</span></span>|<span data-ttu-id="f787e-143">Type</span><span class="sxs-lookup"><span data-stu-id="f787e-143">Type</span></span>|<span data-ttu-id="f787e-144">Requis</span><span class="sxs-lookup"><span data-stu-id="f787e-144">Required</span></span>|<span data-ttu-id="f787e-145">Description</span><span class="sxs-lookup"><span data-stu-id="f787e-145">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="f787e-146">**meetingId**</span><span class="sxs-lookup"><span data-stu-id="f787e-146">**meetingId**</span></span>| <span data-ttu-id="f787e-147">string</span><span class="sxs-lookup"><span data-stu-id="f787e-147">string</span></span> | <span data-ttu-id="f787e-148">Oui</span><span class="sxs-lookup"><span data-stu-id="f787e-148">Yes</span></span> | <span data-ttu-id="f787e-149">L’identificateur de réunion est disponible via le kit de développement logiciel (SDK) et teams Client SDK.</span><span class="sxs-lookup"><span data-stu-id="f787e-149">The meeting identifier is available through Bot Invoke and Teams Client SDK.</span></span>|
|<span data-ttu-id="f787e-150">**participantId**</span><span class="sxs-lookup"><span data-stu-id="f787e-150">**participantId**</span></span>| <span data-ttu-id="f787e-151">string</span><span class="sxs-lookup"><span data-stu-id="f787e-151">string</span></span> | <span data-ttu-id="f787e-152">Oui</span><span class="sxs-lookup"><span data-stu-id="f787e-152">Yes</span></span> | <span data-ttu-id="f787e-153">Le participantId est l’ID d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f787e-153">The participantId is the user ID.</span></span> <span data-ttu-id="f787e-154">Elle est disponible dans les kits de développement logiciel SSO, de robot et teams client.</span><span class="sxs-lookup"><span data-stu-id="f787e-154">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="f787e-155">Il est vivement recommandé d’obtenir un participantId à partir de l’authentification unique de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="f787e-155">It is highly recommended to get a participantId from the Tab SSO.</span></span> |
|<span data-ttu-id="f787e-156">**tenantId**</span><span class="sxs-lookup"><span data-stu-id="f787e-156">**tenantId**</span></span>| <span data-ttu-id="f787e-157">string</span><span class="sxs-lookup"><span data-stu-id="f787e-157">string</span></span> | <span data-ttu-id="f787e-158">Oui</span><span class="sxs-lookup"><span data-stu-id="f787e-158">Yes</span></span> | <span data-ttu-id="f787e-159">Le tenantId est requis pour les utilisateurs du client.</span><span class="sxs-lookup"><span data-stu-id="f787e-159">The tenantId is required for the tenant users.</span></span> <span data-ttu-id="f787e-160">Elle est disponible dans les kits de développement logiciel SSO, de robot et teams client.</span><span class="sxs-lookup"><span data-stu-id="f787e-160">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="f787e-161">Il est vivement recommandé d’obtenir un tenantId à partir de l’authentification unique de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="f787e-161">It is highly recommended to get a tenantId from the Tab SSO.</span></span> |

#### <a name="example"></a><span data-ttu-id="f787e-162">Exemple</span><span class="sxs-lookup"><span data-stu-id="f787e-162">Example</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f787e-163">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f787e-163">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  TeamsMeetingParticipant participant = GetMeetingParticipantAsync(turnContext, "yourMeetingId", "yourParticipantId", "yourTenantId");
  TeamsChannelAccount member = participant.User;
  MeetingParticipantInfo meetingInfo = participant.Meeting;
  ConversationAccount conversation = participant.Conversation;

  await turnContext.SendActivityAsync(MessageFactory.Text($"The participant role is: {meetingInfo.Role}"), cancellationToken);
}

```

# <a name="javascript"></a>[<span data-ttu-id="f787e-164">JavaScript</span><span class="sxs-lookup"><span data-stu-id="f787e-164">JavaScript</span></span>](#tab/javascript)

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onMessage(async (context, next) => {
            TeamsMeetingParticipant participant = GetMeetingParticipantAsync(turnContext, "yourMeetingId", "yourParticipantId", "yourTenantId");
            let member = participant.user;
            let meetingInfo = participant.meeting;
            let conversation = participant.conversation;
            
            await context.sendActivity(`The participant role is: '${meetingInfo.role}'`);
            await next();
        });
    }
}

```

# <a name="json"></a>[<span data-ttu-id="f787e-165">JSON</span><span class="sxs-lookup"><span data-stu-id="f787e-165">JSON</span></span>](#tab/json)

```http
GET /v3/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

<span data-ttu-id="f787e-166">Le corps de la réponse est :</span><span class="sxs-lookup"><span data-stu-id="f787e-166">The response body is:</span></span>

```json
{
   "user":{
      "id":"29:1JKiJGPAX9TTxtGxhVo0wLx_zwzo-gG8Z-X03306vBwi9p-xMTEbDXsT6KH7-0kkTS8cD-2zkrsoV6f5WJ6_aYw",
      "aadObjectId":"e236c4bf-88b1-4f3a-b1d7-8891dfc332b5",
      "name":"Bob Young",
      "givenName":"Bob",
      "surname":"Young",
      "email":"Bob.young@microsoft.com",
      "userPrincipalName":"Bob.young@microsoft.com",
      "tenantId":"2fe477ab-0efc-4dfd-bde2-484374e2c373",
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

* * *

#### <a name="response-codes"></a><span data-ttu-id="f787e-167">Codes de réponse</span><span class="sxs-lookup"><span data-stu-id="f787e-167">Response codes</span></span>

* <span data-ttu-id="f787e-168">**403**: l’application n’est pas autorisée à obtenir des informations sur les participants.</span><span class="sxs-lookup"><span data-stu-id="f787e-168">**403**: The app is not allowed to get participant information.</span></span>  <span data-ttu-id="f787e-169">Il s’agit de la réponse d’erreur la plus courante, qui est déclenchée si l’application n’est pas installée dans la réunion.</span><span class="sxs-lookup"><span data-stu-id="f787e-169">This is the most common error response and is triggered if the app is not installed in the meeting.</span></span> <span data-ttu-id="f787e-170">Par exemple, si l’application est désactivée par l’administrateur client ou bloquée lors de la migration de site en direct.</span><span class="sxs-lookup"><span data-stu-id="f787e-170">For example, if the app is disabled by tenant admin or blocked during live site migration.</span></span>
* <span data-ttu-id="f787e-171">**200**: les informations sur les participants ont été récupérées.</span><span class="sxs-lookup"><span data-stu-id="f787e-171">**200**: Participant information successfully retrieved.</span></span>
* <span data-ttu-id="f787e-172">**401**: jeton non valide.</span><span class="sxs-lookup"><span data-stu-id="f787e-172">**401**: Invalid token.</span></span>
* <span data-ttu-id="f787e-173">**404**: le participant est introuvable.</span><span class="sxs-lookup"><span data-stu-id="f787e-173">**404**: Participant cannot be found.</span></span>
* <span data-ttu-id="f787e-174">**500**: la réunion a expiré (plus de 60 jours après la fin de la réunion) ou le participant ne dispose pas d’autorisations en fonction de son rôle.</span><span class="sxs-lookup"><span data-stu-id="f787e-174">**500**: The meeting has either expired (more than 60 days since the meeting ended) or the participant does not have permissions based on their role.</span></span>


<span data-ttu-id="f787e-175">**Bientôt disponible**</span><span class="sxs-lookup"><span data-stu-id="f787e-175">**Coming Soon**</span></span>

* <span data-ttu-id="f787e-176">**404**: la réunion a expiré ou le participant est introuvable.</span><span class="sxs-lookup"><span data-stu-id="f787e-176">**404**: The meeting has either expired or participant cannot be found.</span></span>


### <a name="notificationsignal-api"></a><span data-ttu-id="f787e-177">API NotificationSignal</span><span class="sxs-lookup"><span data-stu-id="f787e-177">NotificationSignal API</span></span>

> [!NOTE]
> <span data-ttu-id="f787e-178">Lorsqu’une boîte de dialogue de réunion est appelée, le même contenu s’affiche également sous la forme d’un message de conversation.</span><span class="sxs-lookup"><span data-stu-id="f787e-178">When an in-meeting dialog is invoked, the same content will also be presented as a chat message.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="f787e-179">Paramètres de requête</span><span class="sxs-lookup"><span data-stu-id="f787e-179">Query parameters</span></span>

|<span data-ttu-id="f787e-180">Valeur</span><span class="sxs-lookup"><span data-stu-id="f787e-180">Value</span></span>|<span data-ttu-id="f787e-181">Type</span><span class="sxs-lookup"><span data-stu-id="f787e-181">Type</span></span>|<span data-ttu-id="f787e-182">Requis</span><span class="sxs-lookup"><span data-stu-id="f787e-182">Required</span></span>|<span data-ttu-id="f787e-183">Description</span><span class="sxs-lookup"><span data-stu-id="f787e-183">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="f787e-184">**conversationId**</span><span class="sxs-lookup"><span data-stu-id="f787e-184">**conversationId**</span></span>| <span data-ttu-id="f787e-185">string</span><span class="sxs-lookup"><span data-stu-id="f787e-185">string</span></span> | <span data-ttu-id="f787e-186">Oui</span><span class="sxs-lookup"><span data-stu-id="f787e-186">Yes</span></span> | <span data-ttu-id="f787e-187">L’identificateur de conversation est disponible dans le cadre de l’appel de bot.</span><span class="sxs-lookup"><span data-stu-id="f787e-187">The conversation identifier is available as part of bot invoke</span></span> |

#### <a name="example"></a><span data-ttu-id="f787e-188">Exemple</span><span class="sxs-lookup"><span data-stu-id="f787e-188">Example</span></span>

> [!NOTE]
>
<span data-ttu-id="f787e-189">Le `completionBotId` paramètre de l' `externalResourceUrl` est facultatif dans l’exemple de charge utile demandé.</span><span class="sxs-lookup"><span data-stu-id="f787e-189">The `completionBotId` parameter of the `externalResourceUrl` is optional in the requested payload example.</span></span> <span data-ttu-id="f787e-190">`Bot ID` est déclaré dans le manifeste et le bot reçoit un objet de résultat.</span><span class="sxs-lookup"><span data-stu-id="f787e-190">`Bot ID` is declared in the manifest and the bot receives a result object.</span></span>
> * <span data-ttu-id="f787e-191">Les paramètres de largeur et de hauteur externalResourceUrl doivent être en pixels.</span><span class="sxs-lookup"><span data-stu-id="f787e-191">The externalResourceUrl width and height parameters must be in pixels.</span></span> <span data-ttu-id="f787e-192">Reportez-vous aux [instructions de conception](design/designing-apps-in-meetings.md) pour vous assurer que les dimensions respectent les limites autorisées.</span><span class="sxs-lookup"><span data-stu-id="f787e-192">Refer to the [design guidelines](design/designing-apps-in-meetings.md) to ensure the dimensions are within the allowed limits.</span></span>
> * <span data-ttu-id="f787e-193">L’URL est la page chargée en tant que `<iframe>` dans la boîte de dialogue de réunion.</span><span class="sxs-lookup"><span data-stu-id="f787e-193">The URL is the page loaded as an `<iframe>` in the in-meeting dialog.</span></span> <span data-ttu-id="f787e-194">Le domaine doit se trouver dans le tableau de l’application `validDomains` dans le manifeste de votre application.</span><span class="sxs-lookup"><span data-stu-id="f787e-194">The domain must be in the app's `validDomains` array in your app manifest.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f787e-195">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f787e-195">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="f787e-196">JavaScript</span><span class="sxs-lookup"><span data-stu-id="f787e-196">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="f787e-197">JSON</span><span class="sxs-lookup"><span data-stu-id="f787e-197">JSON</span></span>](#tab/json)

```http
POST /v3/conversations/{conversationId}/activities

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

* * *

#### <a name="response-codes"></a><span data-ttu-id="f787e-198">Codes de réponse</span><span class="sxs-lookup"><span data-stu-id="f787e-198">Response Codes</span></span>

* <span data-ttu-id="f787e-199">**201**: l’activité avec le signal est correctement envoyée</span><span class="sxs-lookup"><span data-stu-id="f787e-199">**201**: activity with signal is successfully sent</span></span>  
* <span data-ttu-id="f787e-200">**401**: jeton non valide</span><span class="sxs-lookup"><span data-stu-id="f787e-200">**401**: invalid token</span></span>  
* <span data-ttu-id="f787e-201">**201**: l’activité avec le signal est correctement envoyée.</span><span class="sxs-lookup"><span data-stu-id="f787e-201">**201**: Activity with signal is successfully sent.</span></span> 
* <span data-ttu-id="f787e-202">**401**: jeton non valide.</span><span class="sxs-lookup"><span data-stu-id="f787e-202">**401**: Invalid token.</span></span>
* <span data-ttu-id="f787e-203">**403**: l’application ne parvient pas à envoyer le signal.</span><span class="sxs-lookup"><span data-stu-id="f787e-203">**403**: The app is unable to send the signal.</span></span> <span data-ttu-id="f787e-204">Cela peut se produire pour diverses raisons, telles que l’administrateur client désactive l’application, que l’application est bloquée lors de la migration de site réel, et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="f787e-204">This can happen due to various reasons such as the tenant admin disables the app, the app is blocked during live site migration, and so on.</span></span> <span data-ttu-id="f787e-205">Dans ce cas, la charge utile contient un message d’erreur détaillé.</span><span class="sxs-lookup"><span data-stu-id="f787e-205">In this case, the payload contains a detailed error message.</span></span> 
* <span data-ttu-id="f787e-206">**404**: la conversation de réunion n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="f787e-206">**404**: Meeting chat doesn't exist.</span></span>
 

## <a name="enable-your-app-for-teams-meetings"></a><span data-ttu-id="f787e-207">Activer votre application pour les réunions teams</span><span class="sxs-lookup"><span data-stu-id="f787e-207">Enable your app for Teams meetings</span></span>

### <a name="update-your-app-manifest"></a><span data-ttu-id="f787e-208">Mettre à jour le manifeste de votre application</span><span class="sxs-lookup"><span data-stu-id="f787e-208">Update your app manifest</span></span>

<span data-ttu-id="f787e-209">Les fonctionnalités des applications de réunion sont déclarées dans le manifeste de votre application via les  ->  **étendues** configurableTabs et les tableaux de **contexte** .</span><span class="sxs-lookup"><span data-stu-id="f787e-209">The meetings app capabilities are declared in your app manifest via the **configurableTabs** -> **scopes** and **context** arrays.</span></span> <span data-ttu-id="f787e-210">L' *étendue* définit la personne et le *contexte* définissant où votre application sera disponible.</span><span class="sxs-lookup"><span data-stu-id="f787e-210">*Scope* defines to whom and *context* defines where your app will be available.</span></span>

> [!NOTE]
> <span data-ttu-id="f787e-211">Veuillez utiliser le [schéma de manifeste d’aperçu développeur](../resources/schema/manifest-schema-dev-preview.md) pour essayer cela dans le manifeste de votre application.</span><span class="sxs-lookup"><span data-stu-id="f787e-211">Please use [Developer Preview manifest schema](../resources/schema/manifest-schema-dev-preview.md) to try this in your app manifest.</span></span>

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

### <a name="context-property"></a><span data-ttu-id="f787e-212">Context, propriété</span><span class="sxs-lookup"><span data-stu-id="f787e-212">Context property</span></span>

<span data-ttu-id="f787e-213">L’onglet `context` et les `scopes` propriétés fonctionnent en harmonie pour vous permettre de déterminer où vous souhaitez que votre application apparaisse.</span><span class="sxs-lookup"><span data-stu-id="f787e-213">The tab `context` and `scopes` properties work in harmony to allow you to determine where you want your app to appear.</span></span> <span data-ttu-id="f787e-214">Les onglets de l' `team` `groupchat` étendue ou peuvent avoir plusieurs contextes.</span><span class="sxs-lookup"><span data-stu-id="f787e-214">Tabs in the `team` or `groupchat` scope can have more than one context.</span></span> <span data-ttu-id="f787e-215">Les valeurs possibles pour la propriété Context sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="f787e-215">The possible values for the context property are as follows:</span></span>

* <span data-ttu-id="f787e-216">**channelTab**: onglet de l’en-tête d’un canal d’équipe.</span><span class="sxs-lookup"><span data-stu-id="f787e-216">**channelTab**: a tab in the header of a team channel.</span></span>
* <span data-ttu-id="f787e-217">**privateChatTab**: onglet de l’en-tête d’une conversation de groupe entre un ensemble d’utilisateurs qui n’est pas dans le contexte d’une équipe ou d’une réunion.</span><span class="sxs-lookup"><span data-stu-id="f787e-217">**privateChatTab**: a tab in the header of a group chat between a set of users not in the context of a team or meeting.</span></span>
* <span data-ttu-id="f787e-218">**meetingChatTab**: onglet de l’en-tête d’une conversation de groupe entre un ensemble d’utilisateurs dans le contexte d’une réunion planifiée.</span><span class="sxs-lookup"><span data-stu-id="f787e-218">**meetingChatTab**: a tab in the header of a group chat between a set of users in the context of a scheduled meeting.</span></span>
* <span data-ttu-id="f787e-219">**meetingDetailsTab**: onglet de l’en-tête de l’affichage Détails de la réunion du calendrier.</span><span class="sxs-lookup"><span data-stu-id="f787e-219">**meetingDetailsTab**: a tab in the header of the meeting details view of the calendar.</span></span>
* <span data-ttu-id="f787e-220">**meetingSidePanel**: un panneau de réunion ouvert par le biais de la barre unifiée (u-bar).</span><span class="sxs-lookup"><span data-stu-id="f787e-220">**meetingSidePanel**: an in-meeting panel opened via the unified bar (u-bar).</span></span>

> [!NOTE]
> <span data-ttu-id="f787e-221">La propriété « Context » n’est pas prise en charge actuellement et sera donc ignorée sur les clients mobiles</span><span class="sxs-lookup"><span data-stu-id="f787e-221">"Context" property is currently not supported and thus will be ignored on mobile clients</span></span>

## <a name="configure-your-app-for-meeting-scenarios"></a><span data-ttu-id="f787e-222">Configurer votre application pour les scénarios de réunion</span><span class="sxs-lookup"><span data-stu-id="f787e-222">Configure your app for meeting scenarios</span></span>

> [!NOTE]
> * <span data-ttu-id="f787e-223">Pour que votre application soit visible dans la Galerie d’onglets, elle doit **prendre en charge les onglets configurables** et l' **étendue de conversation de groupe**.</span><span class="sxs-lookup"><span data-stu-id="f787e-223">For your app to be visible in the tab gallery it needs to **support configurable tabs** and the **group chat scope**.</span></span>
>
> * <span data-ttu-id="f787e-224">Les clients mobiles prennent en charge les onglets uniquement dans les surfaces pre et post Meeting.</span><span class="sxs-lookup"><span data-stu-id="f787e-224">Mobile clients support Tabs only in Pre and Post Meeting Surfaces.</span></span> <span data-ttu-id="f787e-225">Les expériences de réunion (boîte de dialogue et onglet de réunion) sur mobile seront disponibles prochainement.</span><span class="sxs-lookup"><span data-stu-id="f787e-225">The in-meeting experiences (in-meeting dialog and tab) on mobile will be available soon.</span></span> <span data-ttu-id="f787e-226">Suivez les [instructions pour les onglets sur mobile](../tabs/design/tabs-mobile.md) lors de la création de vos onglets pour mobile.</span><span class="sxs-lookup"><span data-stu-id="f787e-226">Follow the [guidance for tabs on mobile](../tabs/design/tabs-mobile.md) when creating your tabs for mobile.</span></span>

### <a name="before-a-meeting"></a><span data-ttu-id="f787e-227">Avant une réunion</span><span class="sxs-lookup"><span data-stu-id="f787e-227">Before a meeting</span></span>

<span data-ttu-id="f787e-228">Les utilisateurs disposant de rôles d’organisateur et/ou de présentateur ajoutent des onglets à une réunion en utilisant le bouton plus ➕ dans les pages **conversation** de réunion et **Détails** de la réunion.</span><span class="sxs-lookup"><span data-stu-id="f787e-228">Users with organizer and/or presenter roles add tabs to a meeting using the plus ➕ button in the meeting **Chat** and meeting **details** pages.</span></span> <span data-ttu-id="f787e-229">Les extensions de messagerie sont ajoutées à via le menu ellipses/Overflow &#x25CF;&#x25CF;&#x25CF; située sous la zone de message composer dans la conversation.</span><span class="sxs-lookup"><span data-stu-id="f787e-229">Messaging extensions are added to via the ellipses/overflow menu &#x25CF;&#x25CF;&#x25CF; located beneath the compose message area in the chat.</span></span> <span data-ttu-id="f787e-230">Les robots sont ajoutés à une conversation de réunion à l’aide de la **@** touche «» et en sélectionnant **obtenir les bots**.</span><span class="sxs-lookup"><span data-stu-id="f787e-230">Bots are added to a meeting chat using the "**@**" key and selecting **Get bots**.</span></span>

<span data-ttu-id="f787e-231">✔ L’identité de l’utilisateur *doit* être confirmée via les [onglets SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span><span class="sxs-lookup"><span data-stu-id="f787e-231">✔ The user identity *must* be confirmed via [Tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="f787e-232">À la suite de cette authentification, l’application peut récupérer le rôle d’utilisateur via l’API GetParticipant.</span><span class="sxs-lookup"><span data-stu-id="f787e-232">Following this authentication, the app can retrieve the user role via the GetParticipant API.</span></span>

 <span data-ttu-id="f787e-233">✔ En fonction du rôle d’utilisateur, l’application est désormais capable de présenter des expériences spécifiques de rôle.</span><span class="sxs-lookup"><span data-stu-id="f787e-233">✔ Based on the user role, the app will now have the capability to present role specific experiences.</span></span> <span data-ttu-id="f787e-234">Par exemple, une application d’interrogation peut autoriser uniquement les organisateurs et les présentateurs à créer une nouvelle interrogation.</span><span class="sxs-lookup"><span data-stu-id="f787e-234">For example, a polling app can allow only organizers and presenters to create a new poll.</span></span>

> <span data-ttu-id="f787e-235">**Remarque**: les attributions de rôles peuvent être modifiées lorsqu’une réunion est en cours.</span><span class="sxs-lookup"><span data-stu-id="f787e-235">**NOTE**: Role assignments can be changed while a meeting is in progress.</span></span>  <span data-ttu-id="f787e-236">*Voir* [rôles dans une réunion teams](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span><span class="sxs-lookup"><span data-stu-id="f787e-236">*See* [Roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span> 

### <a name="during-a-meeting"></a><span data-ttu-id="f787e-237">Lors d’une réunion</span><span class="sxs-lookup"><span data-stu-id="f787e-237">During a meeting</span></span>

#### <a name="sidepanel"></a><span data-ttu-id="f787e-238">**sidePanel**</span><span class="sxs-lookup"><span data-stu-id="f787e-238">**sidePanel**</span></span>

<span data-ttu-id="f787e-239">✔ Dans votre manifeste d’application, ajoutez **sidePanel** au tableau de **contexte** , comme décrit ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="f787e-239">✔ In your app manifest add **sidePanel** to the **context** array as described above.</span></span>

<span data-ttu-id="f787e-240">✔ Dans la réunion, ainsi que dans tous les scénarios, l’application sera affichée sous la forme d’un onglet dans la réunion 320 px.</span><span class="sxs-lookup"><span data-stu-id="f787e-240">✔ In the meeting as well as in all scenarios, the app will be rendered in an in-meeting tab that is 320px in width.</span></span> <span data-ttu-id="f787e-241">Pour ce faire, vous devez optimiser l’onglet.</span><span class="sxs-lookup"><span data-stu-id="f787e-241">Your tab must be optimized for this.</span></span> <span data-ttu-id="f787e-242">*Voir*, [interface FrameContext](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)</span><span class="sxs-lookup"><span data-stu-id="f787e-242">*See*, [FrameContext interface](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)</span></span>

<span data-ttu-id="f787e-243">✔ Reportez-vous au [Kit de développement logiciel teams](../tabs/how-to/access-teams-context.md#user-context) pour utiliser l’API **userContext** pour acheminer les demandes en conséquence.</span><span class="sxs-lookup"><span data-stu-id="f787e-243">✔Refer to the [Teams SDK](../tabs/how-to/access-teams-context.md#user-context) to use the **userContext** API to route requests accordingly.</span></span>

<span data-ttu-id="f787e-244">✔ Reportez-vous au [flux d’authentification teams pour les onglets](../tabs/how-to/authentication/auth-flow-tab.md).</span><span class="sxs-lookup"><span data-stu-id="f787e-244">✔ Refer to the [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span> <span data-ttu-id="f787e-245">Le flux d’authentification des onglets est très similaire au flux d’authentification pour les sites Web.</span><span class="sxs-lookup"><span data-stu-id="f787e-245">Authentication flow for tabs is very similar to the auth flow for websites.</span></span> <span data-ttu-id="f787e-246">Par conséquent, les onglets peuvent utiliser OAuth 2,0 directement.</span><span class="sxs-lookup"><span data-stu-id="f787e-246">Thus, tabs can use OAuth 2.0 directly.</span></span> <span data-ttu-id="f787e-247">*Voir aussi* la [plateforme d’identité Microsoft et le flux de code d’autorisation OAuth 2,0](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span><span class="sxs-lookup"><span data-stu-id="f787e-247">*See also*, [Microsoft identity platform and OAuth 2.0 authorization code flow](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span></span>

<span data-ttu-id="f787e-248">✔ Extension de message doit fonctionner comme prévu lorsqu’un utilisateur est dans une vue de réunion et doit être en mesure de publier des cartes d’extension de message de composition.</span><span class="sxs-lookup"><span data-stu-id="f787e-248">✔ Message extension should work as expected when a user is in an in-meeting view and should be able to post compose message extension cards.</span></span>

<span data-ttu-id="f787e-249">✔ AppName dans la réunion-ToolTip doit indiquer le nom de l’application dans la barre U de la réunion.</span><span class="sxs-lookup"><span data-stu-id="f787e-249">✔ AppName in-meeting - Tooltip should state the app name in-meeting U-bar.</span></span>

#### <a name="in-meeting-dialog"></a><span data-ttu-id="f787e-250">**Boîtes de dialogue en réunion**</span><span class="sxs-lookup"><span data-stu-id="f787e-250">**In-meeting dialog**</span></span>

<span data-ttu-id="f787e-251">✔ Vous devez respecter les [instructions de conception de la boîte de dialogue de réunion](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog).</span><span class="sxs-lookup"><span data-stu-id="f787e-251">✔ You must adhere to the [in-meeting dialog design guidelines](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog).</span></span>

<span data-ttu-id="f787e-252">✔ Reportez-vous au [flux d’authentification teams pour les onglets](../tabs/how-to/authentication/auth-flow-tab.md).</span><span class="sxs-lookup"><span data-stu-id="f787e-252">✔ Refer to the [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span>

<span data-ttu-id="f787e-253">✔ Utiliser l’API de [notification](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) pour signaler qu’une notification de bulle doit être déclenchée.</span><span class="sxs-lookup"><span data-stu-id="f787e-253">✔ Use the [notification](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) API to signal that a bubble notification needs to be triggered.</span></span>

<span data-ttu-id="f787e-254">✔ Dans le cadre de la charge utile de la demande de notification, incluez l’URL où le contenu à présenter est hébergé.</span><span class="sxs-lookup"><span data-stu-id="f787e-254">✔ As part of the notification request payload, include the URL where the content to be showcased is hosted.</span></span>

<span data-ttu-id="f787e-255">✔ Boîte de dialogue de réunion ne doit pas utiliser le module tâches.</span><span class="sxs-lookup"><span data-stu-id="f787e-255">✔ In-meeting dialog must not use task module.</span></span>

> [!NOTE]
>
> * <span data-ttu-id="f787e-256">Ces notifications sont permanentes.</span><span class="sxs-lookup"><span data-stu-id="f787e-256">These notifications are persistent in nature.</span></span> <span data-ttu-id="f787e-257">Vous devez appeler la fonction [**submitTask ()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) pour faire une fermeture automatique après qu’un utilisateur a effectué une action dans l’affichage Web.</span><span class="sxs-lookup"><span data-stu-id="f787e-257">You must invoke the [**submitTask()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) function to auto-dismiss after a user takes an action in the web-view.</span></span> <span data-ttu-id="f787e-258">Il s’agit d’une condition requise pour l’envoi d’une application.</span><span class="sxs-lookup"><span data-stu-id="f787e-258">This is a requirement for app submission.</span></span> <span data-ttu-id="f787e-259">*Voir aussi*, [Kit de développement logiciel (SDK) teams : module de tâches](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="f787e-259">*See also*, [Teams SDK: task module](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span></span>
>
> * <span data-ttu-id="f787e-260">Si vous souhaitez que votre application prenne en charge les utilisateurs anonymes, votre charge utile de la demande d’appel initiale doit reposer sur les métadonnées de demande `from.id`  (ID de l’utilisateur) dans l' `from` objet, et non sur l' `from.aadObjectId` ID (Azure Active Directory ID de l’utilisateur).</span><span class="sxs-lookup"><span data-stu-id="f787e-260">If you want your app to support anonymous users, your initial invoke request payload must rely on the `from.id`  (ID of the user) request metadata in the `from` object, not the `from.aadObjectId` (Azure Active Directory ID of the user) request metadata.</span></span> <span data-ttu-id="f787e-261">*Voir* [utilisation des modules de tâches dans les onglets](../task-modules-and-cards/task-modules/task-modules-tabs.md) et [créer et envoyer le module de tâches](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).</span><span class="sxs-lookup"><span data-stu-id="f787e-261">*See* [Using task modules in tabs](../task-modules-and-cards/task-modules/task-modules-tabs.md) and [Create and send the task module](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).</span></span>

### <a name="after-a-meeting"></a><span data-ttu-id="f787e-262">Après une réunion</span><span class="sxs-lookup"><span data-stu-id="f787e-262">After a meeting</span></span>

<span data-ttu-id="f787e-263">Les configurations post-réunion et de réunion sont équivalentes.</span><span class="sxs-lookup"><span data-stu-id="f787e-263">The post-meeting and pre-meeting configurations are equivalent.</span></span>

## <a name="meeting-app-sample"></a><span data-ttu-id="f787e-264">Exemple d’application de réunion</span><span class="sxs-lookup"><span data-stu-id="f787e-264">Meeting app sample</span></span>

 > [!div class="nextstepaction"]
> [<span data-ttu-id="f787e-265">Application du générateur de jetons de réunion</span><span class="sxs-lookup"><span data-stu-id="f787e-265">Meeting token generator app</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token)
