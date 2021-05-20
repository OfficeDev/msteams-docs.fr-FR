---
title: Créer des applications pour les réunions Teams
author: laujan
description: créer des applications pour les réunions d’équipes
ms.topic: conceptual
ms.author: lajanuar
localization_priority: Normal
keywords: équipes apps réunions utilisateur participant rôle api
ms.openlocfilehash: 84d0f5564d7e8e6e34dde1f3d59cc6e7a68d3332
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565913"
---
# <a name="create-apps-for-teams-meetings"></a><span data-ttu-id="57cdc-104">Créer des applications pour les réunions Teams</span><span class="sxs-lookup"><span data-stu-id="57cdc-104">Create apps for Teams meetings</span></span>

## <a name="prerequisites-and-considerations"></a><span data-ttu-id="57cdc-105">Conditions préalables et considérations</span><span class="sxs-lookup"><span data-stu-id="57cdc-105">Prerequisites and considerations</span></span>

<span data-ttu-id="57cdc-106">Avant de créer des applications pour Teams réunions, vous devez avoir une compréhension des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="57cdc-106">Before you create apps for Teams meetings, you must have an understanding of the following:</span></span>

* <span data-ttu-id="57cdc-107">Vous devez avoir une connaissance de la façon de développer Teams applications.</span><span class="sxs-lookup"><span data-stu-id="57cdc-107">You must have knowledge of how to develop Teams apps.</span></span> <span data-ttu-id="57cdc-108">Pour plus d’informations, [consultez Teams développement d’applications](../overview.md).</span><span class="sxs-lookup"><span data-stu-id="57cdc-108">For more information, see [Teams app development](../overview.md).</span></span>

* <span data-ttu-id="57cdc-109">Vous devez mettre à jour le Teams’application pour indiquer que l’application est disponible pour les réunions.</span><span class="sxs-lookup"><span data-stu-id="57cdc-109">You must update the Teams app manifest to indicate that the app is available for meetings.</span></span> <span data-ttu-id="57cdc-110">Pour plus d’informations, voir [manifeste de l’application](#update-your-app-manifest).</span><span class="sxs-lookup"><span data-stu-id="57cdc-110">For more information, see [app manifest](#update-your-app-manifest).</span></span>

* <span data-ttu-id="57cdc-111">Pour que votre application fonctionne dans le cycle de vie de la réunion sous forme d’onglet, elle doit prendre en charge les onglets configurables dans la portée groupchat.</span><span class="sxs-lookup"><span data-stu-id="57cdc-111">For your app to function in the meeting lifecycle as a tab, it must support configurable tabs in the groupchat scope.</span></span> <span data-ttu-id="57cdc-112">Pour plus d’informations, consultez [la portée groupchat](../resources/schema/manifest-schema.md#configurabletabs) et [créez un onglet groupe](../build-your-first-app/build-channel-tab.md).</span><span class="sxs-lookup"><span data-stu-id="57cdc-112">For more information, see [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs) and [build a group tab](../build-your-first-app/build-channel-tab.md).</span></span>

* <span data-ttu-id="57cdc-113">Vous devez respecter les lignes directrices générales Teams conception des onglets pour les scénarios avant et après la réunion.</span><span class="sxs-lookup"><span data-stu-id="57cdc-113">You must adhere to general Teams tab design guidelines for pre- and post-meeting scenarios.</span></span> <span data-ttu-id="57cdc-114">Pour les expériences pendant les réunions, consultez l’onglet en réunion et les lignes directrices de conception de dialogue en réunion.</span><span class="sxs-lookup"><span data-stu-id="57cdc-114">For experiences during meetings, refer to the in-meeting tab and in-meeting dialog design guidelines.</span></span> <span data-ttu-id="57cdc-115">Pour plus d’informations, consultez [les Teams de conception d’onglets,](../tabs/design/tabs.md)les lignes [directrices de conception d’onglets en](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) réunion et les lignes [directrices de conception de dialogue en réunion.](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)</span><span class="sxs-lookup"><span data-stu-id="57cdc-115">For more information, see [Teams tab design guidelines](../tabs/design/tabs.md), [in-meeting tab design guidelines](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) and [in-meeting dialog design guidelines](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog).</span></span>

* <span data-ttu-id="57cdc-116">Vous devez prendre en charge `groupchat` la portée pour activer votre application dans les conversations de pré-réunion et post-réunion.</span><span class="sxs-lookup"><span data-stu-id="57cdc-116">You must support the `groupchat` scope to enable your app in pre-meeting and post-meeting chats.</span></span> <span data-ttu-id="57cdc-117">Grâce à l’expérience de l’application pré-réunion, vous pouvez trouver et ajouter des applications de réunion et effectuer des tâches de pré-réunion.</span><span class="sxs-lookup"><span data-stu-id="57cdc-117">With the pre-meeting app experience, you can find and add meeting apps and perform pre-meeting tasks.</span></span> <span data-ttu-id="57cdc-118">Grâce à l’expérience de l’application après la réunion, vous pouvez consulter les résultats de la réunion, tels que les résultats du sondage ou les commentaires.</span><span class="sxs-lookup"><span data-stu-id="57cdc-118">With post-meeting app experience, you can view the results of the meeting, such as poll survey results or feedback.</span></span>

* <span data-ttu-id="57cdc-119">La réunion des paramètres d’URL de l’API `meetingId` doit avoir , et `userId` `tenantId` .</span><span class="sxs-lookup"><span data-stu-id="57cdc-119">Meeting API URL parameters must have `meetingId`, `userId`, and `tenantId`.</span></span> <span data-ttu-id="57cdc-120">Ceux-ci sont disponibles dans le cadre de l Teams client SDK et l’activité bot.</span><span class="sxs-lookup"><span data-stu-id="57cdc-120">These are available as part of the Teams client SDK and bot activity.</span></span> <span data-ttu-id="57cdc-121">En outre, des informations fiables pour l’identification de l’utilisateur et l’ID locataire peuvent être récupérées à l’aide [de l’authentification Tab SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span><span class="sxs-lookup"><span data-stu-id="57cdc-121">In addition, reliable information for user ID and tenant ID can be retrieved using [Tab SSO authentication](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>

* <span data-ttu-id="57cdc-122">`GetParticipant`L’API doit avoir un enregistrement de bot et un ID pour générer des jetons auth.</span><span class="sxs-lookup"><span data-stu-id="57cdc-122">The `GetParticipant` API must have a bot registration and ID to generate auth tokens.</span></span> <span data-ttu-id="57cdc-123">Pour plus d’informations, voir [inscription bot et ID](../build-your-first-app/build-bot.md).</span><span class="sxs-lookup"><span data-stu-id="57cdc-123">For more information, see [bot registration and ID](../build-your-first-app/build-bot.md).</span></span>

* <span data-ttu-id="57cdc-124">Pour que votre application soit mise à jour en temps réel, elle doit être à jour en fonction des activités de l’événement lors de la réunion.</span><span class="sxs-lookup"><span data-stu-id="57cdc-124">For your app to update in real time, it must be up-to-date based on event activities in the meeting.</span></span> <span data-ttu-id="57cdc-125">Ces événements peuvent se trouver dans la boîte de dialogue en réunion et dans d’autres étapes du cycle de vie de la réunion.</span><span class="sxs-lookup"><span data-stu-id="57cdc-125">These events can be within the in-meeting dialog box and other stages across the meeting lifecycle.</span></span> <span data-ttu-id="57cdc-126">Pour la boîte de dialogue en réunion, voir le paramètre `bot Id` d’achèvement dans `Notification Signal API` .</span><span class="sxs-lookup"><span data-stu-id="57cdc-126">For the in-meeting dialog box, see completion `bot Id` parameter in `Notification Signal API`.</span></span>

## <a name="meeting-apps-api-reference"></a><span data-ttu-id="57cdc-127">Référence API des applications de réunion</span><span class="sxs-lookup"><span data-stu-id="57cdc-127">Meeting apps API reference</span></span>

|<span data-ttu-id="57cdc-128">API</span><span class="sxs-lookup"><span data-stu-id="57cdc-128">API</span></span>|<span data-ttu-id="57cdc-129">Description</span><span class="sxs-lookup"><span data-stu-id="57cdc-129">Description</span></span>|<span data-ttu-id="57cdc-130">Demande</span><span class="sxs-lookup"><span data-stu-id="57cdc-130">Request</span></span>|<span data-ttu-id="57cdc-131">Source</span><span class="sxs-lookup"><span data-stu-id="57cdc-131">Source</span></span>|
|---|---|----|---|
|<span data-ttu-id="57cdc-132">**GetUserContexte GetUserContext GetUserContext GetUs**</span><span class="sxs-lookup"><span data-stu-id="57cdc-132">**GetUserContext**</span></span>| <span data-ttu-id="57cdc-133">Cette API vous permet d’obtenir des informations contextuelles pour afficher le contenu pertinent dans un onglet Teams’écran.</span><span class="sxs-lookup"><span data-stu-id="57cdc-133">This API enables you to get contextual information to display relevant content in a Teams tab.</span></span> |<span data-ttu-id="57cdc-134">_**microsoftTeams.getContext ( ) => { /*...\* / } )*\*_</span><span class="sxs-lookup"><span data-stu-id="57cdc-134">_**microsoftTeams.getContext( ( ) => {  /*...*/ } )**_</span></span>|<span data-ttu-id="57cdc-135">Microsoft Teams client SDK</span><span class="sxs-lookup"><span data-stu-id="57cdc-135">Microsoft Teams client SDK</span></span>|
|<span data-ttu-id="57cdc-136">**GetParticipant**</span><span class="sxs-lookup"><span data-stu-id="57cdc-136">**GetParticipant**</span></span>| <span data-ttu-id="57cdc-137">Cette API permet à un bot d’aller chercher des informations sur les participants en rencontrant l’ID et l’ID du participant.</span><span class="sxs-lookup"><span data-stu-id="57cdc-137">This API allows a bot to fetch participant information by meeting ID and participant ID.</span></span> |<span data-ttu-id="57cdc-138">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span><span class="sxs-lookup"><span data-stu-id="57cdc-138">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span></span> |<span data-ttu-id="57cdc-139">Microsoft Bot Framework SDK (en)</span><span class="sxs-lookup"><span data-stu-id="57cdc-139">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="57cdc-140">**NotificationSignal (notifications)**</span><span class="sxs-lookup"><span data-stu-id="57cdc-140">**NotificationSignal**</span></span> | <span data-ttu-id="57cdc-141">Cette API vous permet de fournir des signaux de réunion qui sont livrés à l’aide de l’API de notification de conversation existante pour le chat utilisateur-bot.</span><span class="sxs-lookup"><span data-stu-id="57cdc-141">This API enables you to provide meeting signals that are delivered using the existing conversation notification API for user-bot chat.</span></span> <span data-ttu-id="57cdc-142">Il vous permet de signaler en fonction de l’action de l’utilisateur qui affiche une boîte de dialogue en réunion.</span><span class="sxs-lookup"><span data-stu-id="57cdc-142">It allows you to signal based on user action that shows an in-meeting dialog box.</span></span> |<span data-ttu-id="57cdc-143">**POST** _**/v3/conversations/{conversationId}/activités**_</span><span class="sxs-lookup"><span data-stu-id="57cdc-143">**POST** _**/v3/conversations/{conversationId}/activities**_</span></span>|<span data-ttu-id="57cdc-144">Microsoft Bot Framework SDK (en)</span><span class="sxs-lookup"><span data-stu-id="57cdc-144">Microsoft Bot Framework SDK</span></span>|

### <a name="getusercontext"></a><span data-ttu-id="57cdc-145">GetUserContexte GetUserContext GetUserContext GetUs</span><span class="sxs-lookup"><span data-stu-id="57cdc-145">GetUserContext</span></span>

<span data-ttu-id="57cdc-146">Pour identifier et récupérer les informations contextuelles pour le contenu de votre onglet, [consultez le contexte de votre onglet Teams’onglet](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library). `meetingId`est utilisé par un onglet lors de l’exécution dans le contexte de la réunion et est ajouté pour la charge utile de réponse.</span><span class="sxs-lookup"><span data-stu-id="57cdc-146">To identify and retrieve contextual information for your tab content, see [get context for your Teams tab](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library). `meetingId` is used by a tab when running in the meeting context and is added for the response payload.</span></span>

### <a name="getparticipant-api"></a><span data-ttu-id="57cdc-147">GetPi GetParticipant</span><span class="sxs-lookup"><span data-stu-id="57cdc-147">GetParticipant API</span></span>

> [!NOTE]
> * <span data-ttu-id="57cdc-148">Ne cachez pas les rôles des participants puisque l’organisateur de la réunion peut changer de rôle à tout moment.</span><span class="sxs-lookup"><span data-stu-id="57cdc-148">Do not cache participant roles since the meeting organizer can change a role any time.</span></span>
> * <span data-ttu-id="57cdc-149">Teams’appuie pas actuellement les grandes listes de distribution ou la taille des listes de plus de 350 participants pour `GetParticipant` l’API.</span><span class="sxs-lookup"><span data-stu-id="57cdc-149">Teams does not currently support large distribution lists or roster sizes of more than 350 participants for the `GetParticipant` API.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="57cdc-150">Paramètres de requête</span><span class="sxs-lookup"><span data-stu-id="57cdc-150">Query parameters</span></span>

|<span data-ttu-id="57cdc-151">Valeur</span><span class="sxs-lookup"><span data-stu-id="57cdc-151">Value</span></span>|<span data-ttu-id="57cdc-152">Type</span><span class="sxs-lookup"><span data-stu-id="57cdc-152">Type</span></span>|<span data-ttu-id="57cdc-153">Requis</span><span class="sxs-lookup"><span data-stu-id="57cdc-153">Required</span></span>|<span data-ttu-id="57cdc-154">Description</span><span class="sxs-lookup"><span data-stu-id="57cdc-154">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="57cdc-155">**meetingId**</span><span class="sxs-lookup"><span data-stu-id="57cdc-155">**meetingId**</span></span>| <span data-ttu-id="57cdc-156">string</span><span class="sxs-lookup"><span data-stu-id="57cdc-156">string</span></span> | <span data-ttu-id="57cdc-157">Oui</span><span class="sxs-lookup"><span data-stu-id="57cdc-157">Yes</span></span> | <span data-ttu-id="57cdc-158">L’identificateur de réunion est disponible via Bot Invoke Teams client SDK.</span><span class="sxs-lookup"><span data-stu-id="57cdc-158">The meeting identifier is available through Bot Invoke and Teams Client SDK.</span></span>|
|<span data-ttu-id="57cdc-159">**participantId**</span><span class="sxs-lookup"><span data-stu-id="57cdc-159">**participantId**</span></span>| <span data-ttu-id="57cdc-160">string</span><span class="sxs-lookup"><span data-stu-id="57cdc-160">string</span></span> | <span data-ttu-id="57cdc-161">Oui</span><span class="sxs-lookup"><span data-stu-id="57cdc-161">Yes</span></span> | <span data-ttu-id="57cdc-162">L’iD participant est l’identifiant de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="57cdc-162">The participant ID is the user ID.</span></span> <span data-ttu-id="57cdc-163">Il est disponible dans Tab SSO, Bot Invoke et Teams Client SDK.</span><span class="sxs-lookup"><span data-stu-id="57cdc-163">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="57cdc-164">Il est recommandé d’obtenir un iD participant de l’onglet SSO.</span><span class="sxs-lookup"><span data-stu-id="57cdc-164">It is recommended to get a participant ID from the Tab SSO.</span></span> |
|<span data-ttu-id="57cdc-165">**tenantId**</span><span class="sxs-lookup"><span data-stu-id="57cdc-165">**tenantId**</span></span>| <span data-ttu-id="57cdc-166">string</span><span class="sxs-lookup"><span data-stu-id="57cdc-166">string</span></span> | <span data-ttu-id="57cdc-167">Oui</span><span class="sxs-lookup"><span data-stu-id="57cdc-167">Yes</span></span> | <span data-ttu-id="57cdc-168">L’identification du locataire est requise pour les utilisateurs locataires.</span><span class="sxs-lookup"><span data-stu-id="57cdc-168">The tenant ID is required for the tenant users.</span></span> <span data-ttu-id="57cdc-169">Il est disponible dans Tab SSO, Bot Invoke et Teams Client SDK.</span><span class="sxs-lookup"><span data-stu-id="57cdc-169">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="57cdc-170">Il est recommandé d’obtenir une pièce d’identité du locataire de l’onglet SSO.</span><span class="sxs-lookup"><span data-stu-id="57cdc-170">It is recommended to get a tenant ID from the Tab SSO.</span></span> |

#### <a name="example"></a><span data-ttu-id="57cdc-171">Exemple</span><span class="sxs-lookup"><span data-stu-id="57cdc-171">Example</span></span>

# <a name="c"></a>[<span data-ttu-id="57cdc-172">C#</span><span class="sxs-lookup"><span data-stu-id="57cdc-172">C#</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="57cdc-173">JavaScript</span><span class="sxs-lookup"><span data-stu-id="57cdc-173">JavaScript</span></span>](#tab/javascript)

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onMessage(async (context, next) => {
            TeamsMeetingParticipant participant = getMeetingParticipant(turnContext, "yourMeetingId", "yourParticipantId", "yourTenantId");
            let member = participant.user;
            let meetingInfo = participant.meeting;
            let conversation = participant.conversation;
            
            await context.sendActivity(`The participant role is: '${meetingInfo.role}'`);
            await next();
        });
    }
}

```

# <a name="json"></a>[<span data-ttu-id="57cdc-174">JSON</span><span class="sxs-lookup"><span data-stu-id="57cdc-174">JSON</span></span>](#tab/json)

```http
GET /v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

* * *

<span data-ttu-id="57cdc-175">L’organe de réponse JSON pour `GetParticipant` l’API est :</span><span class="sxs-lookup"><span data-stu-id="57cdc-175">The JSON response body for `GetParticipant` API is:</span></span>

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

#### <a name="response-codes"></a><span data-ttu-id="57cdc-176">Codes de réponse</span><span class="sxs-lookup"><span data-stu-id="57cdc-176">Response codes</span></span>

|<span data-ttu-id="57cdc-177">Code de réponse</span><span class="sxs-lookup"><span data-stu-id="57cdc-177">Response code</span></span>|<span data-ttu-id="57cdc-178">Description</span><span class="sxs-lookup"><span data-stu-id="57cdc-178">Description</span></span>|
|---|---|
| <span data-ttu-id="57cdc-179">**403**</span><span class="sxs-lookup"><span data-stu-id="57cdc-179">**403**</span></span> | <span data-ttu-id="57cdc-180">L’application n’est pas autorisée à obtenir des informations sur les participants.</span><span class="sxs-lookup"><span data-stu-id="57cdc-180">The app is not allowed to get participant information.</span></span> <span data-ttu-id="57cdc-181">Il s’agit de la réponse d’erreur la plus courante et est déclenchée si l’application n’est pas installée dans la réunion.</span><span class="sxs-lookup"><span data-stu-id="57cdc-181">This is the most common error response and is triggered if the app is not installed in the meeting.</span></span> <span data-ttu-id="57cdc-182">Par exemple, si l’application est désactivée par l’administrateur locataire ou bloquée pendant la migration du site en direct.</span><span class="sxs-lookup"><span data-stu-id="57cdc-182">For example, if the app is disabled by tenant admin or blocked during live site migration.</span></span>|
| <span data-ttu-id="57cdc-183">**200**</span><span class="sxs-lookup"><span data-stu-id="57cdc-183">**200**</span></span> | <span data-ttu-id="57cdc-184">Les informations des participants sont récupérées avec succès.</span><span class="sxs-lookup"><span data-stu-id="57cdc-184">The participant information is successfully retrieved.</span></span>|
| <span data-ttu-id="57cdc-185">**401**</span><span class="sxs-lookup"><span data-stu-id="57cdc-185">**401**</span></span> | <span data-ttu-id="57cdc-186">L’application répond par un jeton invalide.</span><span class="sxs-lookup"><span data-stu-id="57cdc-186">The app responds with an invalid token.</span></span>|
| <span data-ttu-id="57cdc-187">**404**</span><span class="sxs-lookup"><span data-stu-id="57cdc-187">**404**</span></span> | <span data-ttu-id="57cdc-188">La réunion est expirée ou le participant ne peut pas être trouvé.</span><span class="sxs-lookup"><span data-stu-id="57cdc-188">The meeting has either expired or participant cannot be found.</span></span>|
| <span data-ttu-id="57cdc-189">**500**</span><span class="sxs-lookup"><span data-stu-id="57cdc-189">**500**</span></span> | <span data-ttu-id="57cdc-190">La réunion a expiré plus de 60 jours depuis la fin de la réunion ou le participant n’a pas d’autorisations en fonction de son rôle.</span><span class="sxs-lookup"><span data-stu-id="57cdc-190">The meeting has either expired more than 60 days since the meeting ended or the participant does not have permissions based on their role.</span></span>|

### <a name="notificationsignal-api"></a><span data-ttu-id="57cdc-191">NotificationSignal API</span><span class="sxs-lookup"><span data-stu-id="57cdc-191">NotificationSignal API</span></span>

<span data-ttu-id="57cdc-192">Tous les utilisateurs d’une réunion reçoivent les notifications envoyées via `NotificationSignal` l’API.</span><span class="sxs-lookup"><span data-stu-id="57cdc-192">All users in a meeting receive the notifications sent through the `NotificationSignal` API.</span></span>

> [!NOTE]
> * <span data-ttu-id="57cdc-193">Lorsqu’une boîte de dialogue en réunion est invoquée, le contenu est présenté comme un message de chat.</span><span class="sxs-lookup"><span data-stu-id="57cdc-193">When an in-meeting dialog box is invoked, the content is presented as a chat message.</span></span>
> * <span data-ttu-id="57cdc-194">Actuellement, l’envoi de notifications ciblées n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="57cdc-194">Currently, sending targeted notifications is not supported.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="57cdc-195">Paramètres de requête</span><span class="sxs-lookup"><span data-stu-id="57cdc-195">Query parameters</span></span>

|<span data-ttu-id="57cdc-196">Valeur</span><span class="sxs-lookup"><span data-stu-id="57cdc-196">Value</span></span>|<span data-ttu-id="57cdc-197">Type</span><span class="sxs-lookup"><span data-stu-id="57cdc-197">Type</span></span>|<span data-ttu-id="57cdc-198">Requis</span><span class="sxs-lookup"><span data-stu-id="57cdc-198">Required</span></span>|<span data-ttu-id="57cdc-199">Description</span><span class="sxs-lookup"><span data-stu-id="57cdc-199">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="57cdc-200">**conversationId**</span><span class="sxs-lookup"><span data-stu-id="57cdc-200">**conversationId**</span></span>| <span data-ttu-id="57cdc-201">string</span><span class="sxs-lookup"><span data-stu-id="57cdc-201">string</span></span> | <span data-ttu-id="57cdc-202">Oui</span><span class="sxs-lookup"><span data-stu-id="57cdc-202">Yes</span></span> | <span data-ttu-id="57cdc-203">L’identificateur de conversation est disponible dans le cadre de bot invoquer.</span><span class="sxs-lookup"><span data-stu-id="57cdc-203">The conversation identifier is available as part of bot invoke.</span></span> |

#### <a name="example"></a><span data-ttu-id="57cdc-204">Exemple</span><span class="sxs-lookup"><span data-stu-id="57cdc-204">Example</span></span>

<span data-ttu-id="57cdc-205">Le `Bot ID` est déclaré dans le manifeste et le bot reçoit un objet de résultat.</span><span class="sxs-lookup"><span data-stu-id="57cdc-205">The `Bot ID` is declared in the manifest and the bot receives a result object.</span></span>

> [!NOTE]
> * <span data-ttu-id="57cdc-206">Le `completionBotId` paramètre de la `externalResourceUrl` est facultative dans l’exemple de charge utile demandé.</span><span class="sxs-lookup"><span data-stu-id="57cdc-206">The `completionBotId` parameter of the `externalResourceUrl` is optional in the requested payload example.</span></span> <span data-ttu-id="57cdc-207">`Bot ID` est déclaré dans le manifeste et le bot reçoit un objet de résultat.</span><span class="sxs-lookup"><span data-stu-id="57cdc-207">`Bot ID` is declared in the manifest and the bot receives a result object.</span></span>
> * <span data-ttu-id="57cdc-208">Les `externalResourceUrl` paramètres de largeur et de hauteur doivent être en pixels.</span><span class="sxs-lookup"><span data-stu-id="57cdc-208">The `externalResourceUrl` width and height parameters must be in pixels.</span></span> <span data-ttu-id="57cdc-209">Pour vous assurer que les dimensions sont dans les limites autorisées, consultez les lignes [directrices de conception.](design/designing-apps-in-meetings.md)</span><span class="sxs-lookup"><span data-stu-id="57cdc-209">To ensure the dimensions are within the allowed limits, see [design guidelines](design/designing-apps-in-meetings.md).</span></span>
> * <span data-ttu-id="57cdc-210">L’URL est la page chargée comme `<iframe>` un dans la boîte de dialogue en réunion.</span><span class="sxs-lookup"><span data-stu-id="57cdc-210">The URL is the page loaded as an `<iframe>` in the in-meeting dialog box.</span></span> <span data-ttu-id="57cdc-211">Le domaine doit être dans le tableau de `validDomains` l’application dans votre manifeste d’application.</span><span class="sxs-lookup"><span data-stu-id="57cdc-211">The domain must be in the app's `validDomains` array in your app manifest.</span></span>

# <a name="c"></a>[<span data-ttu-id="57cdc-212">C#</span><span class="sxs-lookup"><span data-stu-id="57cdc-212">C#</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="57cdc-213">JavaScript</span><span class="sxs-lookup"><span data-stu-id="57cdc-213">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="57cdc-214">JSON</span><span class="sxs-lookup"><span data-stu-id="57cdc-214">JSON</span></span>](#tab/json)

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

#### <a name="response-codes"></a><span data-ttu-id="57cdc-215">Codes de réponse</span><span class="sxs-lookup"><span data-stu-id="57cdc-215">Response codes</span></span>

|<span data-ttu-id="57cdc-216">Code de réponse</span><span class="sxs-lookup"><span data-stu-id="57cdc-216">Response code</span></span>|<span data-ttu-id="57cdc-217">Description</span><span class="sxs-lookup"><span data-stu-id="57cdc-217">Description</span></span>|
|---|---|
| <span data-ttu-id="57cdc-218">**201**</span><span class="sxs-lookup"><span data-stu-id="57cdc-218">**201**</span></span> | <span data-ttu-id="57cdc-219">L’activité avec signal est envoyée avec succès.</span><span class="sxs-lookup"><span data-stu-id="57cdc-219">The activity with signal is successfully sent.</span></span> |
| <span data-ttu-id="57cdc-220">**401**</span><span class="sxs-lookup"><span data-stu-id="57cdc-220">**401**</span></span> | <span data-ttu-id="57cdc-221">L’application répond par un jeton invalide.</span><span class="sxs-lookup"><span data-stu-id="57cdc-221">The app responds with an invalid token.</span></span> |
| <span data-ttu-id="57cdc-222">**403**</span><span class="sxs-lookup"><span data-stu-id="57cdc-222">**403**</span></span> | <span data-ttu-id="57cdc-223">L’application n’est pas en mesure d’envoyer le signal.</span><span class="sxs-lookup"><span data-stu-id="57cdc-223">The app is unable to send the signal.</span></span> <span data-ttu-id="57cdc-224">Cela peut se produire pour diverses raisons telles que l’administrateur locataire désactive l’application, l’application est bloquée pendant la migration du site en direct, et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="57cdc-224">This can happen due to various reasons such as the tenant admin disables the app, the app is blocked during live site migration, and so on.</span></span> <span data-ttu-id="57cdc-225">Dans ce cas, la charge utile contient un message d’erreur détaillé.</span><span class="sxs-lookup"><span data-stu-id="57cdc-225">In this case, the payload contains a detailed error message.</span></span> |
| <span data-ttu-id="57cdc-226">**404**</span><span class="sxs-lookup"><span data-stu-id="57cdc-226">**404**</span></span> | <span data-ttu-id="57cdc-227">Le chat de réunion n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="57cdc-227">The meeting chat does not exist.</span></span> |

## <a name="enable-your-app-for-teams-meetings"></a><span data-ttu-id="57cdc-228">Activez votre application pour Teams réunions</span><span class="sxs-lookup"><span data-stu-id="57cdc-228">Enable your app for Teams meetings</span></span>

### <a name="update-your-app-manifest"></a><span data-ttu-id="57cdc-229">Mettez à jour le manifeste de votre application</span><span class="sxs-lookup"><span data-stu-id="57cdc-229">Update your app manifest</span></span>

<span data-ttu-id="57cdc-230">Les fonctionnalités de l’application de réunions sont déclarées dans le manifeste de votre application à `configurableTabs` l’aide de la , et les `scopes` `context` tableaux.</span><span class="sxs-lookup"><span data-stu-id="57cdc-230">The meetings app capabilities are declared in your app manifest using the `configurableTabs`, `scopes`, and `context` arrays.</span></span> <span data-ttu-id="57cdc-231">Scope définit à qui et le contexte définit l’endroit où votre application est disponible.</span><span class="sxs-lookup"><span data-stu-id="57cdc-231">Scope defines to whom and context defines where your app is available.</span></span>

> [!NOTE]
> <span data-ttu-id="57cdc-232">Essayez de mettre à jour votre manifeste d’application [avec le schéma manifeste](../resources/schema/manifest-schema-dev-preview.md).</span><span class="sxs-lookup"><span data-stu-id="57cdc-232">Try updating your app manifest with the [manifest schema](../resources/schema/manifest-schema-dev-preview.md).</span></span>
> <span data-ttu-id="57cdc-233">Les applications dans les réunions ont besoin *d’une portée groupchat.*</span><span class="sxs-lookup"><span data-stu-id="57cdc-233">Apps in meetings need *groupchat* scope.</span></span> <span data-ttu-id="57cdc-234">La *portée de* l’équipe fonctionne uniquement pour les onglets dans les canaux.</span><span class="sxs-lookup"><span data-stu-id="57cdc-234">The *team* scope works for tabs in channels only.</span></span>

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
        "meetingSidePanel",
        "meetingStage"
     ]
    }
  ]
```
> [!NOTE]
> <span data-ttu-id="57cdc-235">`meetingStage` est actuellement disponible en aperçu développeur seulement.</span><span class="sxs-lookup"><span data-stu-id="57cdc-235">`meetingStage` is currently available in developer preview only.</span></span>

### <a name="context-property"></a><span data-ttu-id="57cdc-236">Propriété context</span><span class="sxs-lookup"><span data-stu-id="57cdc-236">Context property</span></span>

<span data-ttu-id="57cdc-237">L’onglet `context` et les propriétés vous permettent de déterminer `scopes` où votre application doit apparaître.</span><span class="sxs-lookup"><span data-stu-id="57cdc-237">The tab `context` and `scopes` properties enable you to determine where your app must appear.</span></span> <span data-ttu-id="57cdc-238">Les onglets dans la `team` portée ou la portée peuvent avoir plus `groupchat` d’un contexte.</span><span class="sxs-lookup"><span data-stu-id="57cdc-238">Tabs in the `team` or `groupchat` scope can have more than one context.</span></span> <span data-ttu-id="57cdc-239">Voici les valeurs de la propriété `context` à partir de laquelle vous pouvez utiliser la plupart ou certaines des valeurs:</span><span class="sxs-lookup"><span data-stu-id="57cdc-239">Following are the values for the `context` property from which you can use all or some of the values:</span></span>

|<span data-ttu-id="57cdc-240">Valeur</span><span class="sxs-lookup"><span data-stu-id="57cdc-240">Value</span></span>|<span data-ttu-id="57cdc-241">Description</span><span class="sxs-lookup"><span data-stu-id="57cdc-241">Description</span></span>|
|---|---|
| <span data-ttu-id="57cdc-242">**channelTab (en)**</span><span class="sxs-lookup"><span data-stu-id="57cdc-242">**channelTab**</span></span> | <span data-ttu-id="57cdc-243">Un onglet dans l’en-tête d’un canal d’équipe.</span><span class="sxs-lookup"><span data-stu-id="57cdc-243">A tab in the header of a team channel.</span></span> |
| <span data-ttu-id="57cdc-244">**privateChatTab (en)**</span><span class="sxs-lookup"><span data-stu-id="57cdc-244">**privateChatTab**</span></span> | <span data-ttu-id="57cdc-245">Un onglet dans l’en-tête d’un chat de groupe entre un ensemble d’utilisateurs non dans le cadre d’une équipe ou d’une réunion.</span><span class="sxs-lookup"><span data-stu-id="57cdc-245">A tab in the header of a group chat between a set of users not in the context of a team or meeting.</span></span> |
| <span data-ttu-id="57cdc-246">**réunionChatTab**</span><span class="sxs-lookup"><span data-stu-id="57cdc-246">**meetingChatTab**</span></span> | <span data-ttu-id="57cdc-247">Un onglet dans l’en-tête d’un chat de groupe entre un ensemble d’utilisateurs dans le cadre d’une réunion planifiée.</span><span class="sxs-lookup"><span data-stu-id="57cdc-247">A tab in the header of a group chat between a set of users in the context of a scheduled meeting.</span></span> |
| <span data-ttu-id="57cdc-248">**réunionDetailsTab**</span><span class="sxs-lookup"><span data-stu-id="57cdc-248">**meetingDetailsTab**</span></span> | <span data-ttu-id="57cdc-249">Un onglet dans l’en-tête de la réunion détaille la vue du calendrier.</span><span class="sxs-lookup"><span data-stu-id="57cdc-249">A tab in the header of the meeting details view of the calendar.</span></span> |
| <span data-ttu-id="57cdc-250">**réunionSidePanel**</span><span class="sxs-lookup"><span data-stu-id="57cdc-250">**meetingSidePanel**</span></span> | <span data-ttu-id="57cdc-251">Un panel en réunion s’est ouvert via la barre unifiée (U-bar).</span><span class="sxs-lookup"><span data-stu-id="57cdc-251">An in-meeting panel opened via the unified bar (U-bar).</span></span> |
| <span data-ttu-id="57cdc-252">**réunionStage**</span><span class="sxs-lookup"><span data-stu-id="57cdc-252">**meetingStage**</span></span> | <span data-ttu-id="57cdc-253">Une application du sidepanel peut être partagée jusqu’à l’étape de la réunion.</span><span class="sxs-lookup"><span data-stu-id="57cdc-253">An app from the sidepanel can be shared to the meeting stage.</span></span> |

> [!NOTE]
> <span data-ttu-id="57cdc-254">`Context` propriété n’est actuellement pas prise en charge sur les clients mobiles.</span><span class="sxs-lookup"><span data-stu-id="57cdc-254">`Context` property is currently not supported on mobile clients.</span></span>

## <a name="configure-your-app-for-meeting-scenarios"></a><span data-ttu-id="57cdc-255">Configurez votre application pour des scénarios de réunion</span><span class="sxs-lookup"><span data-stu-id="57cdc-255">Configure your app for meeting scenarios</span></span>

> [!NOTE]
> * <span data-ttu-id="57cdc-256">Pour que votre application soit visible dans la galerie d’onglets, elle doit prendre en charge les onglets configurables et la portée de chat de groupe.</span><span class="sxs-lookup"><span data-stu-id="57cdc-256">For your app to be visible in the tab gallery it must support configurable tabs and the group chat scope.</span></span>
> * <span data-ttu-id="57cdc-257">Les clients mobiles ne supporte les onglets qu’aux étapes avant et après la réunion.</span><span class="sxs-lookup"><span data-stu-id="57cdc-257">Mobile clients support tabs only in pre and post meeting stages.</span></span>
> * <span data-ttu-id="57cdc-258">Les expériences en réunion qui sont en réunion boîte de dialogue et onglet n’est actuellement pas pris en charge sur les clients mobiles.</span><span class="sxs-lookup"><span data-stu-id="57cdc-258">The in-meeting experiences that is in-meeting dialog box and tab is currently not supported on mobile clients.</span></span> <span data-ttu-id="57cdc-259">Pour plus d’informations, consultez [les conseils pour les onglets sur mobile](../tabs/design/tabs-mobile.md) lors de la création de vos onglets pour mobile.</span><span class="sxs-lookup"><span data-stu-id="57cdc-259">For more information, see [guidance for tabs on mobile](../tabs/design/tabs-mobile.md) when creating your tabs for mobile.</span></span>

### <a name="before-a-meeting"></a><span data-ttu-id="57cdc-260">Avant une réunion</span><span class="sxs-lookup"><span data-stu-id="57cdc-260">Before a meeting</span></span>

<span data-ttu-id="57cdc-261">Avant une réunion, les utilisateurs peuvent ajouter des onglets, des bots et des extensions de messagerie à une réunion.</span><span class="sxs-lookup"><span data-stu-id="57cdc-261">Before a meeting, users can add tabs, bots and messaging extensions to a meeting.</span></span> <span data-ttu-id="57cdc-262">Les utilisateurs ayant des rôles d’organisateur et de présentateur peuvent ajouter des onglets à une réunion.</span><span class="sxs-lookup"><span data-stu-id="57cdc-262">Users with organizer and presenter roles can add tabs to a meeting.</span></span>

<span data-ttu-id="57cdc-263">**Pour ajouter un onglet à une réunion**</span><span class="sxs-lookup"><span data-stu-id="57cdc-263">**To add a tab to a meeting**</span></span>

1. <span data-ttu-id="57cdc-264">Dans votre calendrier, sélectionnez une réunion à laquelle vous souhaitez ajouter un onglet.</span><span class="sxs-lookup"><span data-stu-id="57cdc-264">In your calendar, select a meeting to which you want to add a tab.</span></span>
1. <span data-ttu-id="57cdc-265">Sélectionnez **l’onglet Détails** et sélectionnez plus</span><span class="sxs-lookup"><span data-stu-id="57cdc-265">Select the **Details** tab and select plus</span></span> <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/><span data-ttu-id="57cdc-266">.</span><span class="sxs-lookup"><span data-stu-id="57cdc-266">.</span></span> <span data-ttu-id="57cdc-267">La galerie d’onglets apparaît.</span><span class="sxs-lookup"><span data-stu-id="57cdc-267">The tab gallery appears.</span></span>

    ![Expérience de pré-réunion](../assets/images/apps-in-meetings/PreMeeting.png)

1. <span data-ttu-id="57cdc-269">Dans la galerie d’onglets, sélectionnez l’application que vous souhaitez ajouter et suivez les étapes au besoin.</span><span class="sxs-lookup"><span data-stu-id="57cdc-269">In the tab gallery, select the app that you want to add and follow the steps as required.</span></span> <span data-ttu-id="57cdc-270">L’application est installée sous forme d’onglet.</span><span class="sxs-lookup"><span data-stu-id="57cdc-270">The app is installed as a tab.</span></span>
    > [!NOTE] 
    > <span data-ttu-id="57cdc-271">À l’heure actuelle, dans l’onglet réunions, il n’est pas pris en charge l’obtention des détails de la réunion et de l’information sur les participants.</span><span class="sxs-lookup"><span data-stu-id="57cdc-271">Currently, in meetings tab, getting meeting details and participant information is not supported.</span></span>

<span data-ttu-id="57cdc-272">**Pour ajouter une extension de messagerie à une réunion**</span><span class="sxs-lookup"><span data-stu-id="57cdc-272">**To add a messaging extension to a meeting**</span></span>

1. <span data-ttu-id="57cdc-273">Sélectionnez les ellipses ou le menu de débordement &#x25CF;&#x25CF;&#x25CF; dans la zone de message de composition dans le chat.</span><span class="sxs-lookup"><span data-stu-id="57cdc-273">Select the ellipses or overflow menu &#x25CF;&#x25CF;&#x25CF; located in the compose message area in the chat.</span></span>
1. <span data-ttu-id="57cdc-274">Sélectionnez l’application que vous souhaitez ajouter et suivez les étapes au besoin.</span><span class="sxs-lookup"><span data-stu-id="57cdc-274">Select the app that you want to add and follow the steps as required.</span></span> <span data-ttu-id="57cdc-275">L’application est installée comme une extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="57cdc-275">The app is installed as a messaging extension.</span></span>

<span data-ttu-id="57cdc-276">**Pour ajouter un bot à une réunion**</span><span class="sxs-lookup"><span data-stu-id="57cdc-276">**To add a bot to a meeting**</span></span>

<span data-ttu-id="57cdc-277">Dans un chat de réunion entrez **@** la clé et **sélectionnez Get bots**.</span><span class="sxs-lookup"><span data-stu-id="57cdc-277">In a meeting chat enter the **@** key and select **Get bots**.</span></span>

> [!NOTE]
> * <span data-ttu-id="57cdc-278">L’identité de l’utilisateur doit être confirmée à [l’aide de Tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span><span class="sxs-lookup"><span data-stu-id="57cdc-278">The user identity must be confirmed using [Tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="57cdc-279">Après authentification, l’application peut récupérer le rôle de l’utilisateur à l’aide de `GetParticipant` l’API.</span><span class="sxs-lookup"><span data-stu-id="57cdc-279">After authentication, the app can retrieve the user role using the `GetParticipant` API.</span></span>
> * <span data-ttu-id="57cdc-280">En fonction du rôle de l’utilisateur, l’application a la capacité de fournir des expériences spécifiques au rôle.</span><span class="sxs-lookup"><span data-stu-id="57cdc-280">Based on the user role, the app has the capability to provide role specific experiences.</span></span> <span data-ttu-id="57cdc-281">Par exemple, une application de sondage permet uniquement aux organisateurs et aux présentateurs de créer un nouveau sondage.</span><span class="sxs-lookup"><span data-stu-id="57cdc-281">For example, a polling app allows only organizers and presenters to create a new poll.</span></span>
> * <span data-ttu-id="57cdc-282">Les affectations de rôle peuvent être modifiées pendant qu’une réunion est en cours.</span><span class="sxs-lookup"><span data-stu-id="57cdc-282">Role assignments can be changed while a meeting is in progress.</span></span> <span data-ttu-id="57cdc-283">Pour plus d’informations, [voir les rôles dans une Teams réunion](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span><span class="sxs-lookup"><span data-stu-id="57cdc-283">For more information, see [roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span>

### <a name="during-a-meeting"></a><span data-ttu-id="57cdc-284">Au cours d’une réunion</span><span class="sxs-lookup"><span data-stu-id="57cdc-284">During a meeting</span></span>

#### <a name="sidepanel"></a><span data-ttu-id="57cdc-285">sidePanel (sidePanel)</span><span class="sxs-lookup"><span data-stu-id="57cdc-285">sidePanel</span></span>

<span data-ttu-id="57cdc-286">Avec sidePanel, vous pouvez personnaliser les expériences d’une réunion qui permet aux organisateurs et aux présentateurs d’avoir différents ensembles de points de vue et d’actions.</span><span class="sxs-lookup"><span data-stu-id="57cdc-286">With the sidePanel, you can customize experiences in a meeting that enable organizers and presenters to have different set of views and actions.</span></span> <span data-ttu-id="57cdc-287">Dans votre manifeste d’application, vous devez ajouter sidePanel au tableau contextnel.</span><span class="sxs-lookup"><span data-stu-id="57cdc-287">In your app manifest, you must add sidePanel to the context array.</span></span> <span data-ttu-id="57cdc-288">Dans la réunion et dans tous les scénarios, l’application est rendue dans un onglet en réunion de 320 pixels de largeur.</span><span class="sxs-lookup"><span data-stu-id="57cdc-288">In the meeting and in all scenarios, the app is rendered in an in-meeting tab that is 320 pixels in width.</span></span> <span data-ttu-id="57cdc-289">Pour plus d’informations, [voir interface FrameContext](/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
).</span><span class="sxs-lookup"><span data-stu-id="57cdc-289">For more information, see [FrameContext interface](/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
).</span></span>

<span data-ttu-id="57cdc-290">Pour utiliser `userContext` l’API pour acheminer les demandes en conséquence, [Teams SDK](../tabs/how-to/access-teams-context.md#user-context).</span><span class="sxs-lookup"><span data-stu-id="57cdc-290">To use the `userContext` API to route requests accordingly, see [Teams SDK](../tabs/how-to/access-teams-context.md#user-context).</span></span> <span data-ttu-id="57cdc-291">Voir [le Teams’authentification pour les onglets](../tabs/how-to/authentication/auth-flow-tab.md).</span><span class="sxs-lookup"><span data-stu-id="57cdc-291">See [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span> <span data-ttu-id="57cdc-292">Le flux d’authentification pour les onglets est très similaire au flux auth pour les sites Web.</span><span class="sxs-lookup"><span data-stu-id="57cdc-292">Authentication flow for tabs is very similar to the auth flow for websites.</span></span> <span data-ttu-id="57cdc-293">Ainsi, les onglets peuvent utiliser OAuth 2.0 directement.</span><span class="sxs-lookup"><span data-stu-id="57cdc-293">So tabs can use OAuth 2.0 directly.</span></span> <span data-ttu-id="57cdc-294">Voir, [Plateforme d’identités Microsoft et OAuth 2.0 flux de code d’autorisation](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span><span class="sxs-lookup"><span data-stu-id="57cdc-294">See, [Microsoft identity platform and OAuth 2.0 authorization code flow](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span></span>

<span data-ttu-id="57cdc-295">L’extension de messagerie fonctionne comme prévu lorsqu’un utilisateur est dans une vue en réunion et que l’utilisateur peut poster des cartes d’extension de message.</span><span class="sxs-lookup"><span data-stu-id="57cdc-295">Messaging extension works as expected when a user is in an in-meeting view and the user can post compose message extension cards.</span></span> <span data-ttu-id="57cdc-296">AppName en réunion est un tooltip qui indique le nom de l’application en réunion U-bar.</span><span class="sxs-lookup"><span data-stu-id="57cdc-296">AppName in-meeting is a tooltip that states the app name in-meeting U-bar.</span></span>

> [!NOTE]
> <span data-ttu-id="57cdc-297">Utilisez la version 1.7.0 ou plus [de Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), car les versions antérieures ne supportent pas le panneau latéral.</span><span class="sxs-lookup"><span data-stu-id="57cdc-297">Use version 1.7.0 or higher of [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), as versions prior to it do not support the side panel.</span></span>

#### <a name="in-meeting-dialog"></a><span data-ttu-id="57cdc-298">Boîtes de dialogue en réunion</span><span class="sxs-lookup"><span data-stu-id="57cdc-298">In-meeting dialog</span></span>

<span data-ttu-id="57cdc-299">La boîte de dialogue en réunion peut être utilisée pour engager les participants pendant la réunion et recueillir des informations ou des commentaires pendant la réunion.</span><span class="sxs-lookup"><span data-stu-id="57cdc-299">The in-meeting dialog box can be used to engage participants during the meeting and collect information or feedback during the meeting.</span></span> <span data-ttu-id="57cdc-300">Utilisez [`NotificationSignal`](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) l’API pour signaler qu’une notification de bulle doit être déclenchée.</span><span class="sxs-lookup"><span data-stu-id="57cdc-300">Use the [`NotificationSignal`](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) API to signal that a bubble notification must be triggered.</span></span> <span data-ttu-id="57cdc-301">Dans le cadre de la charge utile de la demande de notification, inclure l’URL où le contenu à montrer est hébergé.</span><span class="sxs-lookup"><span data-stu-id="57cdc-301">As part of the notification request payload, include the URL where the content to be shown is hosted.</span></span>

<span data-ttu-id="57cdc-302">Le dialogue en réunion ne doit pas utiliser de module de tâches.</span><span class="sxs-lookup"><span data-stu-id="57cdc-302">In-meeting dialog must not use task module.</span></span> <span data-ttu-id="57cdc-303">Le module de tâche n’est pas invoqué dans un chat de réunion.</span><span class="sxs-lookup"><span data-stu-id="57cdc-303">Task module is not invoked in a meeting chat.</span></span> <span data-ttu-id="57cdc-304">Une URL de ressource externe est utilisée pour afficher la bulle de contenu dans une réunion.</span><span class="sxs-lookup"><span data-stu-id="57cdc-304">An external resource URL is used to display content bubble in a meeting.</span></span> <span data-ttu-id="57cdc-305">Vous pouvez utiliser la méthode `submitTask` pour soumettre des données dans un chat de réunion.</span><span class="sxs-lookup"><span data-stu-id="57cdc-305">You can use the `submitTask` method to submit data in a meeting chat.</span></span>

> [!NOTE]
> * <span data-ttu-id="57cdc-306">Vous devez [invoquer la fonction submitTask()](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) pour rejeter automatiquement après qu’un utilisateur prend une action dans la vue Web.</span><span class="sxs-lookup"><span data-stu-id="57cdc-306">You must invoke the [submitTask()](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) function to dismiss automatically after a user takes an action in the web-view.</span></span> <span data-ttu-id="57cdc-307">Il s’agit d’une exigence pour la soumission de l’application.</span><span class="sxs-lookup"><span data-stu-id="57cdc-307">This is a requirement for app submission.</span></span> <span data-ttu-id="57cdc-308">Pour plus d’informations, [Teams module de tâches SDK](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="57cdc-308">For more information, see [Teams SDK task module](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span></span>
> * <span data-ttu-id="57cdc-309">Si vous souhaitez que votre application prend en charge les utilisateurs anonymes, votre charge utile de demande d’invocateur initial doit s’appuyer `from.id` sur les métadonnées de demande dans `from` l’objet, et non `from.aadObjectId` sur les métadonnées de la demande.</span><span class="sxs-lookup"><span data-stu-id="57cdc-309">If you want your app to support anonymous users, your initial invoke request payload must rely on the `from.id` request metadata in the `from` object, not the `from.aadObjectId` request metadata.</span></span> <span data-ttu-id="57cdc-310">`from.id`est l’identifiant de `from.aadObjectId` l’utilisateur et est Azure Active Directory ID (AAD) de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="57cdc-310">`from.id` is the user ID and `from.aadObjectId` is the Azure Active Directory (AAD) ID of the user.</span></span> <span data-ttu-id="57cdc-311">Pour plus d’informations, voir [l’utilisation de modules de tâches dans les onglets](../task-modules-and-cards/task-modules/task-modules-tabs.md) [et créer et envoyer le module de tâches](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).</span><span class="sxs-lookup"><span data-stu-id="57cdc-311">For more information, see [using task modules in tabs](../task-modules-and-cards/task-modules/task-modules-tabs.md) and [create and send the task module](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).</span></span>

#### <a name="share-to-stage"></a><span data-ttu-id="57cdc-312">Partager sur scène</span><span class="sxs-lookup"><span data-stu-id="57cdc-312">Share to stage</span></span> 

> [!NOTE]
> * <span data-ttu-id="57cdc-313">Cette fonctionnalité est actuellement disponible en aperçu développeur uniquement.</span><span class="sxs-lookup"><span data-stu-id="57cdc-313">This capability is currently available in developer preview only.</span></span>
> * <span data-ttu-id="57cdc-314">Pour utiliser cette fonctionnalité, l’application doit prendre en charge un sidepanel en réunion.</span><span class="sxs-lookup"><span data-stu-id="57cdc-314">To use this feature, the app must support an in-meeting sidepanel.</span></span>


<span data-ttu-id="57cdc-315">Cette fonctionnalité permet aux développeurs de partager une application à l’étape de la réunion.</span><span class="sxs-lookup"><span data-stu-id="57cdc-315">This capability gives developers the ability to share an app to the meeting stage.</span></span> <span data-ttu-id="57cdc-316">En permettant de partager à l’étape de la réunion, les participants à la réunion peuvent collaborer en temps réel.</span><span class="sxs-lookup"><span data-stu-id="57cdc-316">By enabling share to the meeting stage, meeting participants can collaborate in real-time.</span></span> 

<span data-ttu-id="57cdc-317">Le contexte requis se trouve `meetingStage` dans le manifeste de l’application.</span><span class="sxs-lookup"><span data-stu-id="57cdc-317">The required context is `meetingStage` in the app manifest.</span></span> <span data-ttu-id="57cdc-318">Une condition préalable à cela est d’avoir le `meetingSidePanel` contexte.</span><span class="sxs-lookup"><span data-stu-id="57cdc-318">A prerequisite for this is to have the `meetingSidePanel` context.</span></span> <span data-ttu-id="57cdc-319">Cela permet le **bouton Partager** dans le sidepanel tel que spécifié dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="57cdc-319">This enables the **Share** button in the sidepanel as depecited in the following image:</span></span>

  ![share_to_stage_during_meeting expérience](~/assets/images/apps-in-meetings/share_to_stage_during_meeting.png)

<span data-ttu-id="57cdc-321">Le changement manifeste nécessaire pour activer cette capacité est le suivant :</span><span class="sxs-lookup"><span data-stu-id="57cdc-321">The manifest change that is needed to enable this capability is as follows:</span></span> 

```json

"configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "canUpdateConfiguration": true,
      "scopes": [
        "groupchat"
      ],
      "context":[
        
        "meetingSidePanel",
        "meetingStage"
     ]
    }
  ]
```



### <a name="after-a-meeting"></a><span data-ttu-id="57cdc-322">Après une réunion</span><span class="sxs-lookup"><span data-stu-id="57cdc-322">After a meeting</span></span>

<span data-ttu-id="57cdc-323">Les configurations post-réunion et pré-réunion sont équivalentes.</span><span class="sxs-lookup"><span data-stu-id="57cdc-323">The post-meeting and pre-meeting configurations are equivalent.</span></span>

## <a name="code-sample"></a><span data-ttu-id="57cdc-324">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="57cdc-324">Code sample</span></span>

|<span data-ttu-id="57cdc-325">Nom de l’échantillon</span><span class="sxs-lookup"><span data-stu-id="57cdc-325">Sample name</span></span> | <span data-ttu-id="57cdc-326">Description</span><span class="sxs-lookup"><span data-stu-id="57cdc-326">Description</span></span> | <span data-ttu-id="57cdc-327">.NET</span><span class="sxs-lookup"><span data-stu-id="57cdc-327">.NET</span></span> | <span data-ttu-id="57cdc-328">Node.js</span><span class="sxs-lookup"><span data-stu-id="57cdc-328">Node.js</span></span> |
|----------------|-----------------|--------------|--------------|
| <span data-ttu-id="57cdc-329">Extensibilité des réunions</span><span class="sxs-lookup"><span data-stu-id="57cdc-329">Meetings extensibility</span></span> | <span data-ttu-id="57cdc-330">Microsoft Teams’exemple d’extensibilité de réunion pour passer des jetons.</span><span class="sxs-lookup"><span data-stu-id="57cdc-330">Microsoft Teams meeting extensibility sample for passing tokens.</span></span> | [<span data-ttu-id="57cdc-331">View</span><span class="sxs-lookup"><span data-stu-id="57cdc-331">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [<span data-ttu-id="57cdc-332">View</span><span class="sxs-lookup"><span data-stu-id="57cdc-332">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
| <span data-ttu-id="57cdc-333">Bot de bulle de contenu de réunion</span><span class="sxs-lookup"><span data-stu-id="57cdc-333">Meeting content bubble bot</span></span> | <span data-ttu-id="57cdc-334">Microsoft Teams’exemple d’extensibilité de réunion pour interagir avec le bot bulle de contenu dans une réunion.</span><span class="sxs-lookup"><span data-stu-id="57cdc-334">Microsoft Teams meeting extensibility sample for interacting with content bubble bot in a meeting.</span></span> | [<span data-ttu-id="57cdc-335">View</span><span class="sxs-lookup"><span data-stu-id="57cdc-335">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |  [<span data-ttu-id="57cdc-336">View</span><span class="sxs-lookup"><span data-stu-id="57cdc-336">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs)|
| <span data-ttu-id="57cdc-337">Réunion SidePanel</span><span class="sxs-lookup"><span data-stu-id="57cdc-337">Meeting SidePanel</span></span> | <span data-ttu-id="57cdc-338">Microsoft Teams’exemple d’extensibilité de la réunion pour iteracting avec le panneau latéral en réunion.</span><span class="sxs-lookup"><span data-stu-id="57cdc-338">Microsoft Teams meeting extensibility sample for iteracting with the side panel in-meeting.</span></span> | [<span data-ttu-id="57cdc-339">View</span><span class="sxs-lookup"><span data-stu-id="57cdc-339">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) |

## <a name="see-also"></a><span data-ttu-id="57cdc-340">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="57cdc-340">See also</span></span>

* [<span data-ttu-id="57cdc-341">Lignes directrices en réunion sur la conception du dialogue</span><span class="sxs-lookup"><span data-stu-id="57cdc-341">In-meeting dialog design guidelines</span></span>](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [<span data-ttu-id="57cdc-342">Teams d’authentification pour les onglets</span><span class="sxs-lookup"><span data-stu-id="57cdc-342">Teams authentication flow for tabs</span></span>](../tabs/how-to/authentication/auth-flow-tab.md)
