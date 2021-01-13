---
title: Créer des applications pour les réunions Teams
author: laujan
description: créer des applications pour les réunions d’équipes
ms.topic: conceptual
ms.author: lajanuar
keywords: Api de rôle d’utilisateur participant aux réunions teams apps
ms.openlocfilehash: 82327eca86dcdac5c47f5f4471bc91d55484d07e
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797763"
---
# <a name="create-apps-for-teams-meetings"></a><span data-ttu-id="00424-104">Créer des applications pour les réunions Teams</span><span class="sxs-lookup"><span data-stu-id="00424-104">Create apps for Teams meetings</span></span>

## <a name="prerequisites-and-considerations"></a><span data-ttu-id="00424-105">Conditions préalables et considérations</span><span class="sxs-lookup"><span data-stu-id="00424-105">Prerequisites and considerations</span></span>

* <span data-ttu-id="00424-106">Les applications dans les réunions nécessitent une connaissance de base du [développement d’applications Teams.](../overview.md)</span><span class="sxs-lookup"><span data-stu-id="00424-106">Apps in meetings require some basic knowledge of [Teams app development](../overview.md).</span></span> <span data-ttu-id="00424-107">Une application dans une réunion peut comprendre des [onglets,](../tabs/what-are-tabs.md)des [bots](../bots/what-are-bots.md)et des [fonctionnalités d’extensions](../messaging-extensions/what-are-messaging-extensions.md) de messagerie et nécessitera des mises à jour du manifeste de l’application [Teams](#update-your-app-manifest) pour indiquer que l’application est disponible pour les réunions</span><span class="sxs-lookup"><span data-stu-id="00424-107">An app in a meeting can comprise of [tabs](../tabs/what-are-tabs.md), [bots](../bots/what-are-bots.md), and [messaging extensions](../messaging-extensions/what-are-messaging-extensions.md) features and will require updates to the Teams [app manifest](#update-your-app-manifest) to indicate that the app is available for meetings</span></span>

* <span data-ttu-id="00424-108">Pour que votre application fonctionne dans le cycle de vie de la réunion sous la mesure d’un onglet, elle doit prendre en charge les onglets configurables dans l’étendue [groupchat](../resources/schema/manifest-schema.md#configurabletabs) (voir comment créer un onglet [de groupe).](../build-your-first-app/build-channel-tab.md)</span><span class="sxs-lookup"><span data-stu-id="00424-108">For your app to function in the meeting lifecycle as a tab, it must support configurable tabs in the [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs) (see how to [build a group tab](../build-your-first-app/build-channel-tab.md)).</span></span> <span data-ttu-id="00424-109">La prise en charge de l’étendue active votre application dans les `groupchat` [conversations préalables à la réunion](teams-apps-in-meetings.md#pre-meeting-app-experience) et [post-réunion.](teams-apps-in-meetings.md#post-meeting-app-experience)</span><span class="sxs-lookup"><span data-stu-id="00424-109">Supporting the `groupchat` scope will enable your app in [pre-meeting](teams-apps-in-meetings.md#pre-meeting-app-experience) and [post-meeting](teams-apps-in-meetings.md#post-meeting-app-experience) chats.</span></span>

* <span data-ttu-id="00424-110">Les paramètres d’URL de l’API de réunion peuvent nécessiter , et le tenantId, ceux-ci sont disponibles dans le cadre de l’activité du bot et du `meetingId` `userId` SDK [](/onedrive/find-your-office-365-tenant-id) client Teams.</span><span class="sxs-lookup"><span data-stu-id="00424-110">Meeting API URL parameters may require `meetingId`, `userId`, and the [tenantId](/onedrive/find-your-office-365-tenant-id) These are available as part of the Teams Client SDK and bot activity.</span></span> <span data-ttu-id="00424-111">En outre, des informations fiables pour l’ID d’utilisateur et l’ID de locataire peuvent être récupérées à l’aide de l’authentification [sso tabulation.](../tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="00424-111">Additionally, reliable information for user ID and tenant ID can be retrieved using [Tab SSO authentication](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>

* <span data-ttu-id="00424-112">Certaines API de réunion, telles que , nécessitent une inscription et un ID de bot pour générer des jetons `GetParticipant` d’th. [](../build-your-first-app/build-bot.md)</span><span class="sxs-lookup"><span data-stu-id="00424-112">Some meeting APIs, such as `GetParticipant`, require a [bot registration and ID](../build-your-first-app/build-bot.md) to generate auth tokens.</span></span>

* <span data-ttu-id="00424-113">Vous devez respecter les instructions générales de conception [de l’onglet Teams](../tabs/design/tabs.md) pour les scénarios préalables et post-réunion.</span><span class="sxs-lookup"><span data-stu-id="00424-113">You must adhere to general [Teams tab design guidelines](../tabs/design/tabs.md) for pre- and post-meeting scenarios.</span></span> <span data-ttu-id="00424-114">Pour les expériences pendant les réunions, [reportez-vous](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) aux instructions de conception de l’onglet réunion et de la boîte [de](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog) dialogue en réunion.</span><span class="sxs-lookup"><span data-stu-id="00424-114">For experiences during meetings, refer to the [in-meeting tab](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) and [in-meeting dialog](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog) design guidelines.</span></span>

* <span data-ttu-id="00424-115">Pour que votre application soit mise à jour en temps réel, elle doit être à jour en fonction des activités d’événements de la réunion.</span><span class="sxs-lookup"><span data-stu-id="00424-115">For your app to update in real time, it must be up-to-date based on event activities in the meeting.</span></span> <span data-ttu-id="00424-116">Ces événements peuvent se trouver dans la boîte de dialogue en réunion (reportez-vous au paramètre d’achèvement dans ) et d’autres surfaces tout au long du cycle `bot Id` de vie de la `Notification Signal API` réunion</span><span class="sxs-lookup"><span data-stu-id="00424-116">These events can be within the in-meeting dialog (refer to completion `bot Id` parameter in `Notification Signal API`) and other surfaces across the meeting lifecycle</span></span>

## <a name="meeting-apps-api-reference"></a><span data-ttu-id="00424-117">Référence de l’API des applications de réunion</span><span class="sxs-lookup"><span data-stu-id="00424-117">Meeting apps API reference</span></span>

|<span data-ttu-id="00424-118">API</span><span class="sxs-lookup"><span data-stu-id="00424-118">API</span></span>|<span data-ttu-id="00424-119">Description</span><span class="sxs-lookup"><span data-stu-id="00424-119">Description</span></span>|<span data-ttu-id="00424-120">Demande</span><span class="sxs-lookup"><span data-stu-id="00424-120">Request</span></span>|<span data-ttu-id="00424-121">Source</span><span class="sxs-lookup"><span data-stu-id="00424-121">Source</span></span>|
|---|---|----|---|
|<span data-ttu-id="00424-122">**GetUserContext**</span><span class="sxs-lookup"><span data-stu-id="00424-122">**GetUserContext**</span></span>| <span data-ttu-id="00424-123">Obtenez des informations contextuelles pour afficher le contenu pertinent dans un onglet Teams.</span><span class="sxs-lookup"><span data-stu-id="00424-123">Get contextual information to display relevant content in a Teams tab.</span></span> |<span data-ttu-id="00424-124">_**microsoftTeams.getContext( ( ) => { /*...\* / } )*\*_</span><span class="sxs-lookup"><span data-stu-id="00424-124">_**microsoftTeams.getContext( ( ) => {  /*...*/ } )**_</span></span>|<span data-ttu-id="00424-125">Microsoft Teams client SDK</span><span class="sxs-lookup"><span data-stu-id="00424-125">Microsoft Teams client SDK</span></span>|
|<span data-ttu-id="00424-126">**GetParticipant**</span><span class="sxs-lookup"><span data-stu-id="00424-126">**GetParticipant**</span></span>|<span data-ttu-id="00424-127">Cette API permet à un bot de récupérer les informations d’un participant par ID de réunion et ID de participant.</span><span class="sxs-lookup"><span data-stu-id="00424-127">This API allows a bot to fetch a participant information by meeting id and participant id.</span></span>|<span data-ttu-id="00424-128">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span><span class="sxs-lookup"><span data-stu-id="00424-128">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span></span> |<span data-ttu-id="00424-129">Microsoft Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="00424-129">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="00424-130">**NotificationSignal**</span><span class="sxs-lookup"><span data-stu-id="00424-130">**NotificationSignal**</span></span> |<span data-ttu-id="00424-131">Les signaux de réunion seront remis à l’aide de l’API de notification de conversation existante suivante (pour la conversation utilisateur-bot).</span><span class="sxs-lookup"><span data-stu-id="00424-131">Meeting signals will be delivered using the following existing conversation notification API (for user-bot chat).</span></span> <span data-ttu-id="00424-132">Cette API permet aux développeurs de signaler en fonction de l’action de l’utilisateur final d’afficher une bulle de boîte de dialogue en réunion.</span><span class="sxs-lookup"><span data-stu-id="00424-132">This API allows developers to signal based on end-user action to show-case an in-meeting dialog bubble.</span></span>|<span data-ttu-id="00424-133">**POST** _**/v3/conversations/{conversationId}/activities**_</span><span class="sxs-lookup"><span data-stu-id="00424-133">**POST** _**/v3/conversations/{conversationId}/activities**_</span></span>|<span data-ttu-id="00424-134">Microsoft Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="00424-134">Microsoft Bot Framework SDK</span></span>|

### <a name="getusercontext"></a><span data-ttu-id="00424-135">GetUserContext</span><span class="sxs-lookup"><span data-stu-id="00424-135">GetUserContext</span></span>

<span data-ttu-id="00424-136">Pour obtenir des instructions sur l’identification et la récupération d’informations contextuelles pour le contenu de votre onglet, reportez-vous à notre documentation de l’onglet Obtenir du contexte pour votre onglet [Teams.](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library)</span><span class="sxs-lookup"><span data-stu-id="00424-136">Please refer to our [Get context for your Teams tab](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) documentation for guidance on identifying and  retrieving contextual information for your tab content.</span></span> <span data-ttu-id="00424-137">Dans le cadre de l’extensibilité des réunions, une nouvelle valeur a été ajoutée pour la charge utile de réponse :</span><span class="sxs-lookup"><span data-stu-id="00424-137">As part of meetings extensibility, a new value has been added for the response payload:</span></span>

<span data-ttu-id="00424-138">✔ **meetingId**: utilisé par un onglet lors de l’exécution dans le contexte de la réunion.</span><span class="sxs-lookup"><span data-stu-id="00424-138">✔ **meetingId**: used by a tab when running in the meeting context.</span></span>

### <a name="getparticipant-api"></a><span data-ttu-id="00424-139">GetParticipant API</span><span class="sxs-lookup"><span data-stu-id="00424-139">GetParticipant API</span></span>

> [!NOTE]
>
> * <span data-ttu-id="00424-140">Ne met pas en cache les rôles des participants, car l’organisateur de la réunion peut modifier un rôle à tout moment.</span><span class="sxs-lookup"><span data-stu-id="00424-140">Do not cache participant roles since the meeting organizer can change a role at any point in time.</span></span>
>
> * <span data-ttu-id="00424-141">Teams ne prend actuellement pas en charge les grandes listes de distribution ou les tailles de liste de plus de 350 participants pour `GetParticipant` l’API.</span><span class="sxs-lookup"><span data-stu-id="00424-141">Teams does not currently support large distribution lists or roster sizes of more than 350 participants for the `GetParticipant` API.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="00424-142">Paramètres de requête</span><span class="sxs-lookup"><span data-stu-id="00424-142">Query parameters</span></span>

|<span data-ttu-id="00424-143">Valeur</span><span class="sxs-lookup"><span data-stu-id="00424-143">Value</span></span>|<span data-ttu-id="00424-144">Type</span><span class="sxs-lookup"><span data-stu-id="00424-144">Type</span></span>|<span data-ttu-id="00424-145">Requis</span><span class="sxs-lookup"><span data-stu-id="00424-145">Required</span></span>|<span data-ttu-id="00424-146">Description</span><span class="sxs-lookup"><span data-stu-id="00424-146">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="00424-147">**meetingId**</span><span class="sxs-lookup"><span data-stu-id="00424-147">**meetingId**</span></span>| <span data-ttu-id="00424-148">string</span><span class="sxs-lookup"><span data-stu-id="00424-148">string</span></span> | <span data-ttu-id="00424-149">Oui</span><span class="sxs-lookup"><span data-stu-id="00424-149">Yes</span></span> | <span data-ttu-id="00424-150">L’identificateur de réunion est disponible via Bot Invoke et le SDK client Teams.</span><span class="sxs-lookup"><span data-stu-id="00424-150">The meeting identifier is available through Bot Invoke and Teams Client SDK.</span></span>|
|<span data-ttu-id="00424-151">**participantId**</span><span class="sxs-lookup"><span data-stu-id="00424-151">**participantId**</span></span>| <span data-ttu-id="00424-152">string</span><span class="sxs-lookup"><span data-stu-id="00424-152">string</span></span> | <span data-ttu-id="00424-153">Oui</span><span class="sxs-lookup"><span data-stu-id="00424-153">Yes</span></span> | <span data-ttu-id="00424-154">L’ID de participant est l’ID utilisateur.</span><span class="sxs-lookup"><span data-stu-id="00424-154">The participantId is the user ID.</span></span> <span data-ttu-id="00424-155">Il est disponible dans le SSO Onglet, l’appel de bot et le SDK client Teams.</span><span class="sxs-lookup"><span data-stu-id="00424-155">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="00424-156">Il est vivement recommandé d’obtenir un participantId à partir de l' ssO Onglet.</span><span class="sxs-lookup"><span data-stu-id="00424-156">It is highly recommended to get a participantId from the Tab SSO.</span></span> |
|<span data-ttu-id="00424-157">**tenantId**</span><span class="sxs-lookup"><span data-stu-id="00424-157">**tenantId**</span></span>| <span data-ttu-id="00424-158">string</span><span class="sxs-lookup"><span data-stu-id="00424-158">string</span></span> | <span data-ttu-id="00424-159">Oui</span><span class="sxs-lookup"><span data-stu-id="00424-159">Yes</span></span> | <span data-ttu-id="00424-160">Le tenantId est requis pour les utilisateurs du client.</span><span class="sxs-lookup"><span data-stu-id="00424-160">The tenantId is required for the tenant users.</span></span> <span data-ttu-id="00424-161">Il est disponible dans le SSO Onglet, l’appel de bot et le SDK client Teams.</span><span class="sxs-lookup"><span data-stu-id="00424-161">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="00424-162">Il est vivement recommandé d’obtenir un tenantId à partir de l' ssO Onglet.</span><span class="sxs-lookup"><span data-stu-id="00424-162">It is highly recommended to get a tenantId from the Tab SSO.</span></span> |

#### <a name="example"></a><span data-ttu-id="00424-163">Exemple</span><span class="sxs-lookup"><span data-stu-id="00424-163">Example</span></span>

# <a name="cnet"></a>[<span data-ttu-id="00424-164">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="00424-164">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="00424-165">JavaScript</span><span class="sxs-lookup"><span data-stu-id="00424-165">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="00424-166">JSON</span><span class="sxs-lookup"><span data-stu-id="00424-166">JSON</span></span>](#tab/json)

```http
GET /v3/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

<span data-ttu-id="00424-167">Le corps de la réponse est :</span><span class="sxs-lookup"><span data-stu-id="00424-167">The response body is:</span></span>

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

#### <a name="response-codes"></a><span data-ttu-id="00424-168">Codes de réponse</span><span class="sxs-lookup"><span data-stu-id="00424-168">Response codes</span></span>

* <span data-ttu-id="00424-169">**403**: l’application n’est pas autorisée à obtenir des informations sur les participants.</span><span class="sxs-lookup"><span data-stu-id="00424-169">**403**: The app is not allowed to get participant information.</span></span>  <span data-ttu-id="00424-170">Il s’agit de la réponse d’erreur la plus courante et est déclenchée si l’application n’est pas installée dans la réunion.</span><span class="sxs-lookup"><span data-stu-id="00424-170">This is the most common error response and is triggered if the app is not installed in the meeting.</span></span> <span data-ttu-id="00424-171">Par exemple, si l’application est désactivée par l’administrateur client ou bloquée lors de la migration de site en direct.</span><span class="sxs-lookup"><span data-stu-id="00424-171">For example, if the app is disabled by tenant admin or blocked during live site migration.</span></span>
* <span data-ttu-id="00424-172">**200**: Informations de participant correctement récupérées.</span><span class="sxs-lookup"><span data-stu-id="00424-172">**200**: Participant information successfully retrieved.</span></span>
* <span data-ttu-id="00424-173">**401 :** jeton non valide.</span><span class="sxs-lookup"><span data-stu-id="00424-173">**401**: Invalid token.</span></span>
* <span data-ttu-id="00424-174">**404 :** Le participant est in found.</span><span class="sxs-lookup"><span data-stu-id="00424-174">**404**: Participant cannot be found.</span></span>
* <span data-ttu-id="00424-175">**500**: la réunion a expiré (plus de 60 jours depuis la fin de la réunion) ou le participant ne dispose pas d’autorisations en fonction de son rôle.</span><span class="sxs-lookup"><span data-stu-id="00424-175">**500**: The meeting has either expired (more than 60 days since the meeting ended) or the participant does not have permissions based on their role.</span></span>


<span data-ttu-id="00424-176">**Bientôt disponible**</span><span class="sxs-lookup"><span data-stu-id="00424-176">**Coming Soon**</span></span>

* <span data-ttu-id="00424-177">**404 :** la réunion a expiré ou le participant est in peut-être trouvé.</span><span class="sxs-lookup"><span data-stu-id="00424-177">**404**: The meeting has either expired or participant cannot be found.</span></span>


### <a name="notificationsignal-api"></a><span data-ttu-id="00424-178">NotificationSignal API</span><span class="sxs-lookup"><span data-stu-id="00424-178">NotificationSignal API</span></span>

> [!NOTE]
> <span data-ttu-id="00424-179">Lorsqu’une boîte de dialogue de réunion est invoquée, le même contenu est également présenté en tant que message de conversation.</span><span class="sxs-lookup"><span data-stu-id="00424-179">When an in-meeting dialog is invoked, the same content will also be presented as a chat message.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="00424-180">Paramètres de requête</span><span class="sxs-lookup"><span data-stu-id="00424-180">Query parameters</span></span>

|<span data-ttu-id="00424-181">Valeur</span><span class="sxs-lookup"><span data-stu-id="00424-181">Value</span></span>|<span data-ttu-id="00424-182">Type</span><span class="sxs-lookup"><span data-stu-id="00424-182">Type</span></span>|<span data-ttu-id="00424-183">Requis</span><span class="sxs-lookup"><span data-stu-id="00424-183">Required</span></span>|<span data-ttu-id="00424-184">Description</span><span class="sxs-lookup"><span data-stu-id="00424-184">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="00424-185">**conversationId**</span><span class="sxs-lookup"><span data-stu-id="00424-185">**conversationId**</span></span>| <span data-ttu-id="00424-186">string</span><span class="sxs-lookup"><span data-stu-id="00424-186">string</span></span> | <span data-ttu-id="00424-187">Oui</span><span class="sxs-lookup"><span data-stu-id="00424-187">Yes</span></span> | <span data-ttu-id="00424-188">L’identificateur de conversation est disponible dans le cadre de l’appel de bot</span><span class="sxs-lookup"><span data-stu-id="00424-188">The conversation identifier is available as part of bot invoke</span></span> |

#### <a name="example"></a><span data-ttu-id="00424-189">Exemple</span><span class="sxs-lookup"><span data-stu-id="00424-189">Example</span></span>

> [!NOTE]
>
<span data-ttu-id="00424-190">Le `completionBotId` paramètre est facultatif dans `externalResourceUrl` l’exemple de charge utile demandé.</span><span class="sxs-lookup"><span data-stu-id="00424-190">The `completionBotId` parameter of the `externalResourceUrl` is optional in the requested payload example.</span></span> <span data-ttu-id="00424-191">`Bot ID` est déclaré dans le manifeste et le bot reçoit un objet de résultat.</span><span class="sxs-lookup"><span data-stu-id="00424-191">`Bot ID` is declared in the manifest and the bot receives a result object.</span></span>
> * <span data-ttu-id="00424-192">Les paramètres de largeur et de hauteur externalResourceUrl doivent être en pixels.</span><span class="sxs-lookup"><span data-stu-id="00424-192">The externalResourceUrl width and height parameters must be in pixels.</span></span> <span data-ttu-id="00424-193">Reportez-vous [aux instructions de](design/designing-apps-in-meetings.md) conception pour vous assurer que les dimensions sont dans les limites autorisées.</span><span class="sxs-lookup"><span data-stu-id="00424-193">Refer to the [design guidelines](design/designing-apps-in-meetings.md) to ensure the dimensions are within the allowed limits.</span></span>
> * <span data-ttu-id="00424-194">L’URL est la page chargée en tant que `<iframe>` dans la boîte de dialogue de la réunion.</span><span class="sxs-lookup"><span data-stu-id="00424-194">The URL is the page loaded as an `<iframe>` in the in-meeting dialog.</span></span> <span data-ttu-id="00424-195">Le domaine doit se trouver dans le tableau de l’application `validDomains` dans le manifeste de votre application.</span><span class="sxs-lookup"><span data-stu-id="00424-195">The domain must be in the app's `validDomains` array in your app manifest.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="00424-196">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="00424-196">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="00424-197">JavaScript</span><span class="sxs-lookup"><span data-stu-id="00424-197">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="00424-198">JSON</span><span class="sxs-lookup"><span data-stu-id="00424-198">JSON</span></span>](#tab/json)

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

#### <a name="response-codes"></a><span data-ttu-id="00424-199">Codes de réponse</span><span class="sxs-lookup"><span data-stu-id="00424-199">Response Codes</span></span>

* <span data-ttu-id="00424-200">**201 :** l’activité avec le signal est correctement envoyée</span><span class="sxs-lookup"><span data-stu-id="00424-200">**201**: activity with signal is successfully sent</span></span>  
* <span data-ttu-id="00424-201">**401 :** jeton non valide</span><span class="sxs-lookup"><span data-stu-id="00424-201">**401**: invalid token</span></span>  
* <span data-ttu-id="00424-202">**201 : l’activité** avec le signal est correctement envoyée.</span><span class="sxs-lookup"><span data-stu-id="00424-202">**201**: Activity with signal is successfully sent.</span></span> 
* <span data-ttu-id="00424-203">**401 :** jeton non valide.</span><span class="sxs-lookup"><span data-stu-id="00424-203">**401**: Invalid token.</span></span>
* <span data-ttu-id="00424-204">**403**: l’application ne peut pas envoyer le signal.</span><span class="sxs-lookup"><span data-stu-id="00424-204">**403**: The app is unable to send the signal.</span></span> <span data-ttu-id="00424-205">Cela peut se produire pour diverses raisons, telles que la désactivation de l’application par l’administrateur client, le blocage de l’application pendant la migration du site en direct, etc.</span><span class="sxs-lookup"><span data-stu-id="00424-205">This can happen due to various reasons such as the tenant admin disables the app, the app is blocked during live site migration, and so on.</span></span> <span data-ttu-id="00424-206">Dans ce cas, la charge utile contient un message d’erreur détaillé.</span><span class="sxs-lookup"><span data-stu-id="00424-206">In this case, the payload contains a detailed error message.</span></span> 
* <span data-ttu-id="00424-207">**404 :** La conversation de réunion n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="00424-207">**404**: Meeting chat doesn't exist.</span></span>
 

## <a name="enable-your-app-for-teams-meetings"></a><span data-ttu-id="00424-208">Activer votre application pour les réunions Teams</span><span class="sxs-lookup"><span data-stu-id="00424-208">Enable your app for Teams meetings</span></span>

### <a name="update-your-app-manifest"></a><span data-ttu-id="00424-209">Mettre à jour le manifeste de votre application</span><span class="sxs-lookup"><span data-stu-id="00424-209">Update your app manifest</span></span>

<span data-ttu-id="00424-210">Les fonctionnalités de l’application réunions sont déclarées dans le manifeste de votre application via les **étendues configurableTabs** et les  ->   tableaux **de** contexte.</span><span class="sxs-lookup"><span data-stu-id="00424-210">The meetings app capabilities are declared in your app manifest via the **configurableTabs** -> **scopes** and **context** arrays.</span></span> <span data-ttu-id="00424-211">*L’étendue* définit à qui et *le contexte* définit l’endroit où votre application sera disponible.</span><span class="sxs-lookup"><span data-stu-id="00424-211">*Scope* defines to whom and *context* defines where your app will be available.</span></span>

> [!NOTE]
> <span data-ttu-id="00424-212">Utilisez le [schéma de manifeste d’aperçu du](../resources/schema/manifest-schema-dev-preview.md) développeur pour l’essayer dans le manifeste de votre application.</span><span class="sxs-lookup"><span data-stu-id="00424-212">Please use [Developer Preview manifest schema](../resources/schema/manifest-schema-dev-preview.md) to try this in your app manifest.</span></span>

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

### <a name="context-property"></a><span data-ttu-id="00424-213">Propriété Context</span><span class="sxs-lookup"><span data-stu-id="00424-213">Context property</span></span>

<span data-ttu-id="00424-214">L’onglet et les propriétés fonctionnent en harmonie pour vous permettre de déterminer où `context` `scopes` vous souhaitez que votre application apparaisse.</span><span class="sxs-lookup"><span data-stu-id="00424-214">The tab `context` and `scopes` properties work in harmony to allow you to determine where you want your app to appear.</span></span> <span data-ttu-id="00424-215">Les onglets de la `team` ou `groupchat` de l’étendue peuvent avoir plusieurs contextes.</span><span class="sxs-lookup"><span data-stu-id="00424-215">Tabs in the `team` or `groupchat` scope can have more than one context.</span></span> <span data-ttu-id="00424-216">Les valeurs possibles pour la propriété de contexte sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="00424-216">The possible values for the context property are as follows:</span></span>

* <span data-ttu-id="00424-217">**channelTab**: onglet dans l’en-tête d’un canal d’équipe.</span><span class="sxs-lookup"><span data-stu-id="00424-217">**channelTab**: a tab in the header of a team channel.</span></span>
* <span data-ttu-id="00424-218">**privateChatTab**: un onglet dans l’en-tête d’une conversation de groupe entre un ensemble d’utilisateurs non dans le contexte d’une équipe ou d’une réunion.</span><span class="sxs-lookup"><span data-stu-id="00424-218">**privateChatTab**: a tab in the header of a group chat between a set of users not in the context of a team or meeting.</span></span>
* <span data-ttu-id="00424-219">**meetingChatTab**: onglet dans l’en-tête d’une conversation de groupe entre un ensemble d’utilisateurs dans le cadre d’une réunion programmée.</span><span class="sxs-lookup"><span data-stu-id="00424-219">**meetingChatTab**: a tab in the header of a group chat between a set of users in the context of a scheduled meeting.</span></span>
* <span data-ttu-id="00424-220">**meetingDetailsTab**: onglet dans l’en-tête de l’affichage Détails de la réunion du calendrier.</span><span class="sxs-lookup"><span data-stu-id="00424-220">**meetingDetailsTab**: a tab in the header of the meeting details view of the calendar.</span></span>
* <span data-ttu-id="00424-221">**meetingSidePanel**: un panneau en réunion ouvert via la barre unifiée (u-bar).</span><span class="sxs-lookup"><span data-stu-id="00424-221">**meetingSidePanel**: an in-meeting panel opened via the unified bar (u-bar).</span></span>

> [!NOTE]
> <span data-ttu-id="00424-222">La propriété « Context » n’est actuellement pas prise en charge et sera donc ignorée sur les clients mobiles</span><span class="sxs-lookup"><span data-stu-id="00424-222">"Context" property is currently not supported and thus will be ignored on mobile clients</span></span>

## <a name="configure-your-app-for-meeting-scenarios"></a><span data-ttu-id="00424-223">Configurer votre application pour les scénarios de réunion</span><span class="sxs-lookup"><span data-stu-id="00424-223">Configure your app for meeting scenarios</span></span>

> [!NOTE]
> * <span data-ttu-id="00424-224">Pour que votre application soit visible dans la galerie d’onglets, elle doit prendre en charge les **onglets configurables** et **l’étendue de conversation de groupe.**</span><span class="sxs-lookup"><span data-stu-id="00424-224">For your app to be visible in the tab gallery it needs to **support configurable tabs** and the **group chat scope**.</span></span>
>
> * <span data-ttu-id="00424-225">Les clients mobiles ne supportent les onglets que dans les surfaces de pré et de post-réunion.</span><span class="sxs-lookup"><span data-stu-id="00424-225">Mobile clients support Tabs only in Pre and Post Meeting Surfaces.</span></span> <span data-ttu-id="00424-226">Les expériences en réunion (boîte de dialogue de réunion et onglet) sur mobile seront bientôt disponibles.</span><span class="sxs-lookup"><span data-stu-id="00424-226">The in-meeting experiences (in-meeting dialog and tab) on mobile will be available soon.</span></span> <span data-ttu-id="00424-227">Suivez les [instructions pour les onglets sur mobile](../tabs/design/tabs-mobile.md) lors de la création de vos onglets pour appareils mobiles.</span><span class="sxs-lookup"><span data-stu-id="00424-227">Follow the [guidance for tabs on mobile](../tabs/design/tabs-mobile.md) when creating your tabs for mobile.</span></span>

### <a name="before-a-meeting"></a><span data-ttu-id="00424-228">Avant une réunion</span><span class="sxs-lookup"><span data-stu-id="00424-228">Before a meeting</span></span>

<span data-ttu-id="00424-229">Les utilisateurs ayant des rôles d’organisateur et/ou de présentateur ajoutent des onglets à une réunion à l’aide du bouton ➕ plus dans les pages de **détails** et de conversation de réunion. </span><span class="sxs-lookup"><span data-stu-id="00424-229">Users with organizer and/or presenter roles add tabs to a meeting using the plus ➕ button in the meeting **Chat** and meeting **details** pages.</span></span> <span data-ttu-id="00424-230">Les extensions de messagerie sont ajoutées via le menu ellipses/overflow &#x25CF;&#x25CF;&#x25CF; située sous la zone de composition de message dans la conversation.</span><span class="sxs-lookup"><span data-stu-id="00424-230">Messaging extensions are added to via the ellipses/overflow menu &#x25CF;&#x25CF;&#x25CF; located beneath the compose message area in the chat.</span></span> <span data-ttu-id="00424-231">Les bots sont ajoutés à une conversation de réunion à l’aide de la clé « « et **@** en sélectionnant **Obtenir des bots**».</span><span class="sxs-lookup"><span data-stu-id="00424-231">Bots are added to a meeting chat using the "**@**" key and selecting **Get bots**.</span></span>

<span data-ttu-id="00424-232">✔ l’identité *de l’utilisateur* doit être confirmée via l' [ssO Onglets.](../tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="00424-232">✔ The user identity *must* be confirmed via [Tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="00424-233">Après cette authentification, l’application peut récupérer le rôle d’utilisateur via l’API GetParticipant.</span><span class="sxs-lookup"><span data-stu-id="00424-233">Following this authentication, the app can retrieve the user role via the GetParticipant API.</span></span>

 <span data-ttu-id="00424-234">✔ en fonction du rôle d’utilisateur, l’application aura désormais la possibilité de présenter des expériences spécifiques au rôle.</span><span class="sxs-lookup"><span data-stu-id="00424-234">✔ Based on the user role, the app will now have the capability to present role specific experiences.</span></span> <span data-ttu-id="00424-235">Par exemple, une application de sondage peut autoriser uniquement les organisateurs et les présentateurs à créer un sondage.</span><span class="sxs-lookup"><span data-stu-id="00424-235">For example, a polling app can allow only organizers and presenters to create a new poll.</span></span>

> <span data-ttu-id="00424-236">**REMARQUE**: les attributions de rôle peuvent être modifiées lors d’une réunion en cours.</span><span class="sxs-lookup"><span data-stu-id="00424-236">**NOTE**: Role assignments can be changed while a meeting is in progress.</span></span>  <span data-ttu-id="00424-237">*Voir rôles* [dans une réunion Teams.](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)</span><span class="sxs-lookup"><span data-stu-id="00424-237">*See* [Roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span> 

### <a name="during-a-meeting"></a><span data-ttu-id="00424-238">Pendant une réunion</span><span class="sxs-lookup"><span data-stu-id="00424-238">During a meeting</span></span>

#### <a name="sidepanel"></a><span data-ttu-id="00424-239">**sidePanel**</span><span class="sxs-lookup"><span data-stu-id="00424-239">**sidePanel**</span></span>

<span data-ttu-id="00424-240">✔ dans le manifeste de votre application, ajoutez **sidePanel** **au** tableau de contexte comme décrit ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="00424-240">✔ In your app manifest add **sidePanel** to the **context** array as described above.</span></span>

<span data-ttu-id="00424-241">✔ dans la réunion, ainsi que dans tous les scénarios, l’application s’restituera dans un onglet de réunion de 320 px de largeur.</span><span class="sxs-lookup"><span data-stu-id="00424-241">✔ In the meeting as well as in all scenarios, the app will be rendered in an in-meeting tab that is 320px in width.</span></span> <span data-ttu-id="00424-242">Votre onglet doit être optimisé pour cela.</span><span class="sxs-lookup"><span data-stu-id="00424-242">Your tab must be optimized for this.</span></span> <span data-ttu-id="00424-243">*Voir*, [Interface FrameContext](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)</span><span class="sxs-lookup"><span data-stu-id="00424-243">*See*, [FrameContext interface](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)</span></span>

<span data-ttu-id="00424-244">✔ Reportez-vous au [SDK Teams](../tabs/how-to/access-teams-context.md#user-context) pour utiliser l’API **userContext** pour router les demandes en conséquence.</span><span class="sxs-lookup"><span data-stu-id="00424-244">✔Refer to the [Teams SDK](../tabs/how-to/access-teams-context.md#user-context) to use the **userContext** API to route requests accordingly.</span></span>

<span data-ttu-id="00424-245">✔ faire référence au flux [d’authentification Teams pour les onglets.](../tabs/how-to/authentication/auth-flow-tab.md)</span><span class="sxs-lookup"><span data-stu-id="00424-245">✔ Refer to the [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span> <span data-ttu-id="00424-246">Le flux d’authentification pour les onglets est très similaire au flux d’authentification pour les sites web.</span><span class="sxs-lookup"><span data-stu-id="00424-246">Authentication flow for tabs is very similar to the auth flow for websites.</span></span> <span data-ttu-id="00424-247">Par conséquent, les onglets peuvent utiliser OAuth 2.0 directement.</span><span class="sxs-lookup"><span data-stu-id="00424-247">Thus, tabs can use OAuth 2.0 directly.</span></span> <span data-ttu-id="00424-248">*Voir aussi*, plateforme d’identité Microsoft et flux de code d’autorisation [OAuth 2.0](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span><span class="sxs-lookup"><span data-stu-id="00424-248">*See also*, [Microsoft identity platform and OAuth 2.0 authorization code flow](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span></span>

<span data-ttu-id="00424-249">✔ l’extension de message doit fonctionner comme prévu lorsqu’un utilisateur est en affichage en réunion et doit être en mesure de publier des cartes d’extension de message de composition.</span><span class="sxs-lookup"><span data-stu-id="00424-249">✔ Message extension should work as expected when a user is in an in-meeting view and should be able to post compose message extension cards.</span></span>

<span data-ttu-id="00424-250">✔ AppName en réunion : l’outil doit faire état du nom de l’application dans la barre U de la réunion.</span><span class="sxs-lookup"><span data-stu-id="00424-250">✔ AppName in-meeting - Tooltip should state the app name in-meeting U-bar.</span></span>

#### <a name="in-meeting-dialog"></a><span data-ttu-id="00424-251">**Boîtes de dialogue en réunion**</span><span class="sxs-lookup"><span data-stu-id="00424-251">**In-meeting dialog**</span></span>

<span data-ttu-id="00424-252">✔ vous devez respecter les instructions de conception de boîte de [dialogue en réunion.](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)</span><span class="sxs-lookup"><span data-stu-id="00424-252">✔ You must adhere to the [in-meeting dialog design guidelines](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog).</span></span>

<span data-ttu-id="00424-253">✔ faire référence au flux [d’authentification Teams pour les onglets.](../tabs/how-to/authentication/auth-flow-tab.md)</span><span class="sxs-lookup"><span data-stu-id="00424-253">✔ Refer to the [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span>

<span data-ttu-id="00424-254">✔ l’API [de notification](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) pour signaler qu’une notification de bulle doit être déclenchée.</span><span class="sxs-lookup"><span data-stu-id="00424-254">✔ Use the [notification](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) API to signal that a bubble notification needs to be triggered.</span></span>

<span data-ttu-id="00424-255">✔ dans le cadre de la charge utile de demande de notification, incluez l’URL où le contenu à présenter est hébergé.</span><span class="sxs-lookup"><span data-stu-id="00424-255">✔ As part of the notification request payload, include the URL where the content to be showcased is hosted.</span></span>

<span data-ttu-id="00424-256">✔ dialogue En réunion ne doit pas utiliser le module de tâche.</span><span class="sxs-lookup"><span data-stu-id="00424-256">✔ In-meeting dialog must not use task module.</span></span>

> [!NOTE]
>
> * <span data-ttu-id="00424-257">Ces notifications sont de nature persistante.</span><span class="sxs-lookup"><span data-stu-id="00424-257">These notifications are persistent in nature.</span></span> <span data-ttu-id="00424-258">Vous devez appeler la [**fonction submitTask()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) pour le faire disparaître automatiquement après qu’un utilisateur a pris une action dans l’affichage web.</span><span class="sxs-lookup"><span data-stu-id="00424-258">You must invoke the [**submitTask()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) function to auto-dismiss after a user takes an action in the web-view.</span></span> <span data-ttu-id="00424-259">Il s’agit d’une condition requise pour la soumission d’application.</span><span class="sxs-lookup"><span data-stu-id="00424-259">This is a requirement for app submission.</span></span> <span data-ttu-id="00424-260">*Voir aussi*, [SDK Teams : module de tâche](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="00424-260">*See also*, [Teams SDK: task module](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span></span>
>
> * <span data-ttu-id="00424-261">Si vous souhaitez que votre application prise en charge des utilisateurs anonymes, votre charge utile de demande d’appel initiale doit reposer sur les métadonnées de demande (ID de l’utilisateur) dans l’objet, et non sur les métadonnées de demande `from.id` `from` `from.aadObjectId` (ID Azure Active Directory de l’utilisateur).</span><span class="sxs-lookup"><span data-stu-id="00424-261">If you want your app to support anonymous users, your initial invoke request payload must rely on the `from.id`  (ID of the user) request metadata in the `from` object, not the `from.aadObjectId` (Azure Active Directory ID of the user) request metadata.</span></span> <span data-ttu-id="00424-262">*Voir* [Utilisation des modules de tâche dans les onglets](../task-modules-and-cards/task-modules/task-modules-tabs.md) et Créer et envoyer le module de [tâche.](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)</span><span class="sxs-lookup"><span data-stu-id="00424-262">*See* [Using task modules in tabs](../task-modules-and-cards/task-modules/task-modules-tabs.md) and [Create and send the task module](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).</span></span>

### <a name="after-a-meeting"></a><span data-ttu-id="00424-263">Après une réunion</span><span class="sxs-lookup"><span data-stu-id="00424-263">After a meeting</span></span>

<span data-ttu-id="00424-264">Les configurations post-réunion et préalable à la réunion sont équivalentes.</span><span class="sxs-lookup"><span data-stu-id="00424-264">The post-meeting and pre-meeting configurations are equivalent.</span></span>

## <a name="meeting-app-sample"></a><span data-ttu-id="00424-265">Exemple d’application de réunion</span><span class="sxs-lookup"><span data-stu-id="00424-265">Meeting app sample</span></span>

 > [!div class="nextstepaction"]
> [<span data-ttu-id="00424-266">Application générateur de jetons de réunion</span><span class="sxs-lookup"><span data-stu-id="00424-266">Meeting token generator app</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token)
