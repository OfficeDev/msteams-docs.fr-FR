---
title: Créer des applications pour les réunions Teams
author: laujan
description: créer des applications pour les réunions d’équipes
ms.topic: conceptual
ms.author: lajanuar
keywords: Api de rôle d’utilisateur participant aux réunions teams apps
ms.openlocfilehash: 78b7791deb61354ab93fa108f8bb2e134dc86080
ms.sourcegitcommit: 3727fc58e84b6f1752612884c2e0b25e207fb56e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/26/2021
ms.locfileid: "51382351"
---
# <a name="create-apps-for-teams-meetings"></a><span data-ttu-id="cf946-104">Créer des applications pour les réunions Teams</span><span class="sxs-lookup"><span data-stu-id="cf946-104">Create apps for Teams meetings</span></span>

## <a name="prerequisites-and-considerations"></a><span data-ttu-id="cf946-105">Conditions préalables et considérations</span><span class="sxs-lookup"><span data-stu-id="cf946-105">Prerequisites and considerations</span></span>

<span data-ttu-id="cf946-106">Avant de créer des applications pour les réunions Teams, vous devez comprendre les choses suivantes :</span><span class="sxs-lookup"><span data-stu-id="cf946-106">Before you create apps for Teams meetings, you must have an understanding of the following:</span></span>

* <span data-ttu-id="cf946-107">Vous devez savoir comment développer des applications Teams.</span><span class="sxs-lookup"><span data-stu-id="cf946-107">You must have knowledge of how to develop Teams apps.</span></span> <span data-ttu-id="cf946-108">Pour plus d’informations, voir [Développement d’applications Teams.](../overview.md)</span><span class="sxs-lookup"><span data-stu-id="cf946-108">For more information, see [Teams app development](../overview.md).</span></span>

* <span data-ttu-id="cf946-109">Vous devez mettre à jour le manifeste de l’application Teams pour indiquer que l’application est disponible pour les réunions.</span><span class="sxs-lookup"><span data-stu-id="cf946-109">You must update the Teams app manifest to indicate that the app is available for meetings.</span></span> <span data-ttu-id="cf946-110">Pour plus d’informations, voir [le manifeste de l’application.](#update-your-app-manifest)</span><span class="sxs-lookup"><span data-stu-id="cf946-110">For more information, see [app manifest](#update-your-app-manifest).</span></span>

* <span data-ttu-id="cf946-111">Pour que votre application fonctionne dans le cycle de vie de la réunion sous la mesure d’un onglet, elle doit prendre en charge les onglets configurables dans l’étendue groupchat.</span><span class="sxs-lookup"><span data-stu-id="cf946-111">For your app to function in the meeting lifecycle as a tab, it must support configurable tabs in the groupchat scope.</span></span> <span data-ttu-id="cf946-112">Pour plus d’informations, voir [étendue groupchat](../resources/schema/manifest-schema.md#configurabletabs) et [créer un onglet de groupe.](../build-your-first-app/build-channel-tab.md)</span><span class="sxs-lookup"><span data-stu-id="cf946-112">For more information, see [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs) and [build a group tab](../build-your-first-app/build-channel-tab.md).</span></span>

* <span data-ttu-id="cf946-113">Vous devez respecter les instructions générales de conception de l’onglet Teams pour les scénarios préalables et post-réunion.</span><span class="sxs-lookup"><span data-stu-id="cf946-113">You must adhere to general Teams tab design guidelines for pre- and post-meeting scenarios.</span></span> <span data-ttu-id="cf946-114">Pour les expériences pendant les réunions, reportez-vous aux instructions de conception de l’onglet réunion et de la boîte de dialogue en réunion.</span><span class="sxs-lookup"><span data-stu-id="cf946-114">For experiences during meetings, refer to the in-meeting tab and in-meeting dialog design guidelines.</span></span> <span data-ttu-id="cf946-115">Pour plus d’informations, voir [](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) recommandations en matière de conception [d’onglets Teams,](../tabs/design/tabs.md)recommandations en matière de conception d’onglets en réunion et recommandations en matière de conception de boîte [de dialogue en réunion.](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)</span><span class="sxs-lookup"><span data-stu-id="cf946-115">For more information, see [Teams tab design guidelines](../tabs/design/tabs.md), [in-meeting tab design guidelines](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) and [in-meeting dialog design guidelines](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog).</span></span>

* <span data-ttu-id="cf946-116">Vous devez prendre en charge l’étendue pour activer votre application dans les conversations `groupchat` préalables à la réunion et post-réunion.</span><span class="sxs-lookup"><span data-stu-id="cf946-116">You must support the `groupchat` scope to enable your app in pre-meeting and post-meeting chats.</span></span> <span data-ttu-id="cf946-117">Avec l’expérience d’application de pré-réunion, vous pouvez rechercher et ajouter des applications de réunion et effectuer des tâches préalables à la réunion.</span><span class="sxs-lookup"><span data-stu-id="cf946-117">With the pre-meeting app experience, you can find and add meeting apps and perform pre-meeting tasks.</span></span> <span data-ttu-id="cf946-118">Avec l’expérience d’application post-réunion, vous pouvez afficher les résultats de la réunion, tels que les résultats des sondages ou les commentaires.</span><span class="sxs-lookup"><span data-stu-id="cf946-118">With post-meeting app experience, you can view the results of the meeting, such as poll survey results or feedback.</span></span>

* <span data-ttu-id="cf946-119">Les paramètres d’URL de l’API de réunion doivent avoir `meetingId` `userId` , et `tenantId` .</span><span class="sxs-lookup"><span data-stu-id="cf946-119">Meeting API URL parameters must have `meetingId`, `userId`, and `tenantId`.</span></span> <span data-ttu-id="cf946-120">Ils sont disponibles dans le cadre de l’activité du bot et du SDK client Teams.</span><span class="sxs-lookup"><span data-stu-id="cf946-120">These are available as part of the Teams client SDK and bot activity.</span></span> <span data-ttu-id="cf946-121">En outre, des informations fiables pour l’ID d’utilisateur et l’ID de locataire peuvent être récupérées à l’aide de l’authentification [sso tabulation.](../tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="cf946-121">In addition, reliable information for user ID and tenant ID can be retrieved using [Tab SSO authentication](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>

* <span data-ttu-id="cf946-122">`GetParticipant`L’API doit avoir un ID et une inscription de bot pour générer des jetons d’th.</span><span class="sxs-lookup"><span data-stu-id="cf946-122">The `GetParticipant` API must have a bot registration and ID to generate auth tokens.</span></span> <span data-ttu-id="cf946-123">Pour plus d’informations, voir [l’inscription et l’ID du bot.](../build-your-first-app/build-bot.md)</span><span class="sxs-lookup"><span data-stu-id="cf946-123">For more information, see [bot registration and ID](../build-your-first-app/build-bot.md).</span></span>

* <span data-ttu-id="cf946-124">Pour que votre application soit mise à jour en temps réel, elle doit être à jour en fonction des activités d’événements de la réunion.</span><span class="sxs-lookup"><span data-stu-id="cf946-124">For your app to update in real time, it must be up-to-date based on event activities in the meeting.</span></span> <span data-ttu-id="cf946-125">Ces événements peuvent se trouver dans la boîte de dialogue de réunion et dans d’autres étapes du cycle de vie de la réunion.</span><span class="sxs-lookup"><span data-stu-id="cf946-125">These events can be within the in-meeting dialog box and other stages across the meeting lifecycle.</span></span> <span data-ttu-id="cf946-126">Pour la boîte de dialogue de réunion, voir paramètre `bot Id` d’achèvement dans `Notification Signal API` .</span><span class="sxs-lookup"><span data-stu-id="cf946-126">For the in-meeting dialog box, see completion `bot Id` parameter in `Notification Signal API`.</span></span>

## <a name="meeting-apps-api-reference"></a><span data-ttu-id="cf946-127">Référence de l’API des applications de réunion</span><span class="sxs-lookup"><span data-stu-id="cf946-127">Meeting apps API reference</span></span>

|<span data-ttu-id="cf946-128">API</span><span class="sxs-lookup"><span data-stu-id="cf946-128">API</span></span>|<span data-ttu-id="cf946-129">Description</span><span class="sxs-lookup"><span data-stu-id="cf946-129">Description</span></span>|<span data-ttu-id="cf946-130">Demande</span><span class="sxs-lookup"><span data-stu-id="cf946-130">Request</span></span>|<span data-ttu-id="cf946-131">Source</span><span class="sxs-lookup"><span data-stu-id="cf946-131">Source</span></span>|
|---|---|----|---|
|<span data-ttu-id="cf946-132">**GetUserContext**</span><span class="sxs-lookup"><span data-stu-id="cf946-132">**GetUserContext**</span></span>| <span data-ttu-id="cf946-133">Cette API vous permet d’obtenir des informations contextuelles pour afficher du contenu pertinent dans un onglet Teams.</span><span class="sxs-lookup"><span data-stu-id="cf946-133">This API enables you to get contextual information to display relevant content in a Teams tab.</span></span> |<span data-ttu-id="cf946-134">_**microsoftTeams.getContext( ( ) => { /*...\* / } )*\*_</span><span class="sxs-lookup"><span data-stu-id="cf946-134">_**microsoftTeams.getContext( ( ) => {  /*...*/ } )**_</span></span>|<span data-ttu-id="cf946-135">Microsoft Teams client SDK</span><span class="sxs-lookup"><span data-stu-id="cf946-135">Microsoft Teams client SDK</span></span>|
|<span data-ttu-id="cf946-136">**GetParticipant**</span><span class="sxs-lookup"><span data-stu-id="cf946-136">**GetParticipant**</span></span>| <span data-ttu-id="cf946-137">Cette API permet à un bot de récupérer les informations des participants par ID de réunion et ID de participant.</span><span class="sxs-lookup"><span data-stu-id="cf946-137">This API allows a bot to fetch participant information by meeting ID and participant ID.</span></span> |<span data-ttu-id="cf946-138">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span><span class="sxs-lookup"><span data-stu-id="cf946-138">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span></span> |<span data-ttu-id="cf946-139">Microsoft Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="cf946-139">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="cf946-140">**NotificationSignal**</span><span class="sxs-lookup"><span data-stu-id="cf946-140">**NotificationSignal**</span></span> | <span data-ttu-id="cf946-141">Cette API vous permet de fournir des signaux de réunion fournis à l’aide de l’API de notification de conversation existante pour la conversation utilisateur-bot.</span><span class="sxs-lookup"><span data-stu-id="cf946-141">This API enables you to provide meeting signals that are delivered using the existing conversation notification API for user-bot chat.</span></span> <span data-ttu-id="cf946-142">Il vous permet de signaler en fonction de l’action de l’utilisateur qui affiche une boîte de dialogue en réunion.</span><span class="sxs-lookup"><span data-stu-id="cf946-142">It allows you to signal based on user action that shows an in-meeting dialog box.</span></span> |<span data-ttu-id="cf946-143">**POST** _**/v3/conversations/{conversationId}/activities**_</span><span class="sxs-lookup"><span data-stu-id="cf946-143">**POST** _**/v3/conversations/{conversationId}/activities**_</span></span>|<span data-ttu-id="cf946-144">Microsoft Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="cf946-144">Microsoft Bot Framework SDK</span></span>|

### <a name="getusercontext"></a><span data-ttu-id="cf946-145">GetUserContext</span><span class="sxs-lookup"><span data-stu-id="cf946-145">GetUserContext</span></span>

<span data-ttu-id="cf946-146">Pour identifier et récupérer des informations contextuelles pour le contenu de votre onglet, voir [obtenir le contexte de votre onglet Teams.](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) est utilisé par un onglet lors de l’exécution dans le contexte de réunion et est `meetingId` ajouté pour la charge utile de réponse.</span><span class="sxs-lookup"><span data-stu-id="cf946-146">To identify and retrieve contextual information for your tab content, see [get context for your Teams tab](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library). `meetingId` is used by a tab when running in the meeting context and is added for the response payload.</span></span>

### <a name="getparticipant-api"></a><span data-ttu-id="cf946-147">GetParticipant API</span><span class="sxs-lookup"><span data-stu-id="cf946-147">GetParticipant API</span></span>

> [!NOTE]
> * <span data-ttu-id="cf946-148">Ne pas mettre en cache les rôles des participants, car l’organisateur de la réunion peut modifier un rôle à tout moment.</span><span class="sxs-lookup"><span data-stu-id="cf946-148">Do not cache participant roles since the meeting organizer can change a role any time.</span></span>
> * <span data-ttu-id="cf946-149">Teams ne prend actuellement pas en charge les grandes listes de distribution ou les tailles de liste de plus de 350 participants pour `GetParticipant` l’API.</span><span class="sxs-lookup"><span data-stu-id="cf946-149">Teams does not currently support large distribution lists or roster sizes of more than 350 participants for the `GetParticipant` API.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="cf946-150">Paramètres de requête</span><span class="sxs-lookup"><span data-stu-id="cf946-150">Query parameters</span></span>

|<span data-ttu-id="cf946-151">Valeur</span><span class="sxs-lookup"><span data-stu-id="cf946-151">Value</span></span>|<span data-ttu-id="cf946-152">Type</span><span class="sxs-lookup"><span data-stu-id="cf946-152">Type</span></span>|<span data-ttu-id="cf946-153">Requis</span><span class="sxs-lookup"><span data-stu-id="cf946-153">Required</span></span>|<span data-ttu-id="cf946-154">Description</span><span class="sxs-lookup"><span data-stu-id="cf946-154">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="cf946-155">**meetingId**</span><span class="sxs-lookup"><span data-stu-id="cf946-155">**meetingId**</span></span>| <span data-ttu-id="cf946-156">string</span><span class="sxs-lookup"><span data-stu-id="cf946-156">string</span></span> | <span data-ttu-id="cf946-157">Oui</span><span class="sxs-lookup"><span data-stu-id="cf946-157">Yes</span></span> | <span data-ttu-id="cf946-158">L’identificateur de réunion est disponible via Bot Invoke et le SDK client Teams.</span><span class="sxs-lookup"><span data-stu-id="cf946-158">The meeting identifier is available through Bot Invoke and Teams Client SDK.</span></span>|
|<span data-ttu-id="cf946-159">**participantId**</span><span class="sxs-lookup"><span data-stu-id="cf946-159">**participantId**</span></span>| <span data-ttu-id="cf946-160">string</span><span class="sxs-lookup"><span data-stu-id="cf946-160">string</span></span> | <span data-ttu-id="cf946-161">Oui</span><span class="sxs-lookup"><span data-stu-id="cf946-161">Yes</span></span> | <span data-ttu-id="cf946-162">L’ID de participant est l’ID utilisateur.</span><span class="sxs-lookup"><span data-stu-id="cf946-162">The participant ID is the user ID.</span></span> <span data-ttu-id="cf946-163">Il est disponible dans le SSO Onglet, l’appel de bot et le SDK client Teams.</span><span class="sxs-lookup"><span data-stu-id="cf946-163">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="cf946-164">Il est recommandé d’obtenir un ID de participant à partir de l' sso tabulation.</span><span class="sxs-lookup"><span data-stu-id="cf946-164">It is recommended to get a participant ID from the Tab SSO.</span></span> |
|<span data-ttu-id="cf946-165">**tenantId**</span><span class="sxs-lookup"><span data-stu-id="cf946-165">**tenantId**</span></span>| <span data-ttu-id="cf946-166">string</span><span class="sxs-lookup"><span data-stu-id="cf946-166">string</span></span> | <span data-ttu-id="cf946-167">Oui</span><span class="sxs-lookup"><span data-stu-id="cf946-167">Yes</span></span> | <span data-ttu-id="cf946-168">L’ID de client est requis pour les utilisateurs du client.</span><span class="sxs-lookup"><span data-stu-id="cf946-168">The tenant ID is required for the tenant users.</span></span> <span data-ttu-id="cf946-169">Il est disponible dans le SSO Onglet, l’appel de bot et le SDK client Teams.</span><span class="sxs-lookup"><span data-stu-id="cf946-169">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="cf946-170">Il est recommandé d’obtenir un ID de client à partir de l' sso tabulation.</span><span class="sxs-lookup"><span data-stu-id="cf946-170">It is recommended to get a tenant ID from the Tab SSO.</span></span> |

#### <a name="example"></a><span data-ttu-id="cf946-171">Exemple</span><span class="sxs-lookup"><span data-stu-id="cf946-171">Example</span></span>

# <a name="c"></a>[<span data-ttu-id="cf946-172">C#</span><span class="sxs-lookup"><span data-stu-id="cf946-172">C#</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="cf946-173">JavaScript</span><span class="sxs-lookup"><span data-stu-id="cf946-173">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="cf946-174">JSON</span><span class="sxs-lookup"><span data-stu-id="cf946-174">JSON</span></span>](#tab/json)

```http
GET /v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

* * *

<span data-ttu-id="cf946-175">Le corps de la réponse JSON pour `GetParticipant` l’API est :</span><span class="sxs-lookup"><span data-stu-id="cf946-175">The JSON response body for `GetParticipant` API is:</span></span>

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

#### <a name="response-codes"></a><span data-ttu-id="cf946-176">Codes de réponse</span><span class="sxs-lookup"><span data-stu-id="cf946-176">Response codes</span></span>

|<span data-ttu-id="cf946-177">Code de réponse</span><span class="sxs-lookup"><span data-stu-id="cf946-177">Response code</span></span>|<span data-ttu-id="cf946-178">Description</span><span class="sxs-lookup"><span data-stu-id="cf946-178">Description</span></span>|
|---|---|
| <span data-ttu-id="cf946-179">**403**</span><span class="sxs-lookup"><span data-stu-id="cf946-179">**403**</span></span> | <span data-ttu-id="cf946-180">L’application n’est pas autorisée à obtenir des informations sur les participants.</span><span class="sxs-lookup"><span data-stu-id="cf946-180">The app is not allowed to get participant information.</span></span> <span data-ttu-id="cf946-181">Il s’agit de la réponse d’erreur la plus courante et est déclenchée si l’application n’est pas installée dans la réunion.</span><span class="sxs-lookup"><span data-stu-id="cf946-181">This is the most common error response and is triggered if the app is not installed in the meeting.</span></span> <span data-ttu-id="cf946-182">Par exemple, si l’application est désactivée par l’administrateur client ou bloquée lors de la migration de site en direct.</span><span class="sxs-lookup"><span data-stu-id="cf946-182">For example, if the app is disabled by tenant admin or blocked during live site migration.</span></span>|
| <span data-ttu-id="cf946-183">**200**</span><span class="sxs-lookup"><span data-stu-id="cf946-183">**200**</span></span> | <span data-ttu-id="cf946-184">Les informations sur les participants sont récupérées avec succès.</span><span class="sxs-lookup"><span data-stu-id="cf946-184">The participant information is successfully retrieved.</span></span>|
| <span data-ttu-id="cf946-185">**401**</span><span class="sxs-lookup"><span data-stu-id="cf946-185">**401**</span></span> | <span data-ttu-id="cf946-186">L’application répond avec un jeton non valide.</span><span class="sxs-lookup"><span data-stu-id="cf946-186">The app responds with an invalid token.</span></span>|
| <span data-ttu-id="cf946-187">**404**</span><span class="sxs-lookup"><span data-stu-id="cf946-187">**404**</span></span> | <span data-ttu-id="cf946-188">La réunion a expiré ou le participant est in peut-être trouvé.</span><span class="sxs-lookup"><span data-stu-id="cf946-188">The meeting has either expired or participant cannot be found.</span></span>|
| <span data-ttu-id="cf946-189">**500**</span><span class="sxs-lookup"><span data-stu-id="cf946-189">**500**</span></span> | <span data-ttu-id="cf946-190">La réunion a expiré plus de 60 jours depuis la fin de la réunion ou le participant ne dispose pas d’autorisations en fonction de son rôle.</span><span class="sxs-lookup"><span data-stu-id="cf946-190">The meeting has either expired more than 60 days since the meeting ended or the participant does not have permissions based on their role.</span></span>|

### <a name="notificationsignal-api"></a><span data-ttu-id="cf946-191">NotificationSignal API</span><span class="sxs-lookup"><span data-stu-id="cf946-191">NotificationSignal API</span></span>

<span data-ttu-id="cf946-192">Tous les utilisateurs d’une réunion reçoivent les notifications envoyées via `NotificationSignal` l’API.</span><span class="sxs-lookup"><span data-stu-id="cf946-192">All users in a meeting receive the notifications sent through the `NotificationSignal` API.</span></span>

> [!NOTE]
> * <span data-ttu-id="cf946-193">Lorsqu’une boîte de dialogue de réunion est invoquée, le contenu est présenté comme un message de conversation.</span><span class="sxs-lookup"><span data-stu-id="cf946-193">When an in-meeting dialog box is invoked, the content is presented as a chat message.</span></span>
> * <span data-ttu-id="cf946-194">Actuellement, l’envoi de notifications ciblées n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="cf946-194">Currently, sending targeted notifications is not supported.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="cf946-195">Paramètres de requête</span><span class="sxs-lookup"><span data-stu-id="cf946-195">Query parameters</span></span>

|<span data-ttu-id="cf946-196">Valeur</span><span class="sxs-lookup"><span data-stu-id="cf946-196">Value</span></span>|<span data-ttu-id="cf946-197">Type</span><span class="sxs-lookup"><span data-stu-id="cf946-197">Type</span></span>|<span data-ttu-id="cf946-198">Requis</span><span class="sxs-lookup"><span data-stu-id="cf946-198">Required</span></span>|<span data-ttu-id="cf946-199">Description</span><span class="sxs-lookup"><span data-stu-id="cf946-199">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="cf946-200">**conversationId**</span><span class="sxs-lookup"><span data-stu-id="cf946-200">**conversationId**</span></span>| <span data-ttu-id="cf946-201">string</span><span class="sxs-lookup"><span data-stu-id="cf946-201">string</span></span> | <span data-ttu-id="cf946-202">Oui</span><span class="sxs-lookup"><span data-stu-id="cf946-202">Yes</span></span> | <span data-ttu-id="cf946-203">L’identificateur de conversation est disponible dans le cadre de l’appel de bot</span><span class="sxs-lookup"><span data-stu-id="cf946-203">The conversation identifier is available as part of bot invoke</span></span> |

#### <a name="example"></a><span data-ttu-id="cf946-204">Exemple</span><span class="sxs-lookup"><span data-stu-id="cf946-204">Example</span></span>

<span data-ttu-id="cf946-205">`Bot ID`L’objet est déclaré dans le manifeste et le bot reçoit un objet de résultat.</span><span class="sxs-lookup"><span data-stu-id="cf946-205">The `Bot ID` is declared in the manifest and the bot receives a result object.</span></span>

> [!NOTE]
> * <span data-ttu-id="cf946-206">Le `completionBotId` paramètre est facultatif dans `externalResourceUrl` l’exemple de charge utile demandé.</span><span class="sxs-lookup"><span data-stu-id="cf946-206">The `completionBotId` parameter of the `externalResourceUrl` is optional in the requested payload example.</span></span> <span data-ttu-id="cf946-207">`Bot ID` est déclaré dans le manifeste et le bot reçoit un objet de résultat.</span><span class="sxs-lookup"><span data-stu-id="cf946-207">`Bot ID` is declared in the manifest and the bot receives a result object.</span></span>
> * <span data-ttu-id="cf946-208">Les `externalResourceUrl` paramètres de largeur et de hauteur doivent être en pixels.</span><span class="sxs-lookup"><span data-stu-id="cf946-208">The `externalResourceUrl` width and height parameters must be in pixels.</span></span> <span data-ttu-id="cf946-209">Pour vous assurer que les dimensions sont dans les limites autorisées, consultez les [instructions de conception.](design/designing-apps-in-meetings.md)</span><span class="sxs-lookup"><span data-stu-id="cf946-209">To ensure the dimensions are within the allowed limits, see [design guidelines](design/designing-apps-in-meetings.md).</span></span>
> * <span data-ttu-id="cf946-210">L’URL est la page chargée en tant que dans la boîte de `<iframe>` dialogue de la réunion.</span><span class="sxs-lookup"><span data-stu-id="cf946-210">The URL is the page loaded as an `<iframe>` in the in-meeting dialog box.</span></span> <span data-ttu-id="cf946-211">Le domaine doit se trouver dans le tableau de l’application `validDomains` dans le manifeste de votre application.</span><span class="sxs-lookup"><span data-stu-id="cf946-211">The domain must be in the app's `validDomains` array in your app manifest.</span></span>

# <a name="c"></a>[<span data-ttu-id="cf946-212">C#</span><span class="sxs-lookup"><span data-stu-id="cf946-212">C#</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="cf946-213">JavaScript</span><span class="sxs-lookup"><span data-stu-id="cf946-213">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="cf946-214">JSON</span><span class="sxs-lookup"><span data-stu-id="cf946-214">JSON</span></span>](#tab/json)

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

#### <a name="response-codes"></a><span data-ttu-id="cf946-215">Codes de réponse</span><span class="sxs-lookup"><span data-stu-id="cf946-215">Response codes</span></span>

|<span data-ttu-id="cf946-216">Code de réponse</span><span class="sxs-lookup"><span data-stu-id="cf946-216">Response code</span></span>|<span data-ttu-id="cf946-217">Description</span><span class="sxs-lookup"><span data-stu-id="cf946-217">Description</span></span>|
|---|---|
| <span data-ttu-id="cf946-218">**201**</span><span class="sxs-lookup"><span data-stu-id="cf946-218">**201**</span></span> | <span data-ttu-id="cf946-219">L’activité avec signal est correctement envoyée</span><span class="sxs-lookup"><span data-stu-id="cf946-219">The activity with signal is successfully sent</span></span> |
| <span data-ttu-id="cf946-220">**401**</span><span class="sxs-lookup"><span data-stu-id="cf946-220">**401**</span></span> | <span data-ttu-id="cf946-221">L’application répond avec un jeton non valide.</span><span class="sxs-lookup"><span data-stu-id="cf946-221">The app responds with an invalid token.</span></span> |
| <span data-ttu-id="cf946-222">**403**</span><span class="sxs-lookup"><span data-stu-id="cf946-222">**403**</span></span> | <span data-ttu-id="cf946-223">L’application ne peut pas envoyer le signal.</span><span class="sxs-lookup"><span data-stu-id="cf946-223">The app is unable to send the signal.</span></span> <span data-ttu-id="cf946-224">Cela peut se produire pour diverses raisons, telles que la désactivation de l’application par l’administrateur client, le blocage de l’application pendant la migration du site en direct, etc.</span><span class="sxs-lookup"><span data-stu-id="cf946-224">This can happen due to various reasons such as the tenant admin disables the app, the app is blocked during live site migration, and so on.</span></span> <span data-ttu-id="cf946-225">Dans ce cas, la charge utile contient un message d’erreur détaillé.</span><span class="sxs-lookup"><span data-stu-id="cf946-225">In this case, the payload contains a detailed error message.</span></span> |
| <span data-ttu-id="cf946-226">**404**</span><span class="sxs-lookup"><span data-stu-id="cf946-226">**404**</span></span> | <span data-ttu-id="cf946-227">La conversation de réunion n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="cf946-227">The meeting chat does not exist.</span></span> |

## <a name="enable-your-app-for-teams-meetings"></a><span data-ttu-id="cf946-228">Activer votre application pour les réunions Teams</span><span class="sxs-lookup"><span data-stu-id="cf946-228">Enable your app for Teams meetings</span></span>

### <a name="update-your-app-manifest"></a><span data-ttu-id="cf946-229">Mettre à jour le manifeste de votre application</span><span class="sxs-lookup"><span data-stu-id="cf946-229">Update your app manifest</span></span>

<span data-ttu-id="cf946-230">Les fonctionnalités de l’application réunions sont déclarées dans le manifeste de votre application à l’aide `configurableTabs` des `scopes` tableaux et des `context` tableaux.</span><span class="sxs-lookup"><span data-stu-id="cf946-230">The meetings app capabilities are declared in your app manifest using the `configurableTabs`, `scopes`, and `context` arrays.</span></span> <span data-ttu-id="cf946-231">L’étendue définit à qui et le contexte définit l’endroit où votre application est disponible.</span><span class="sxs-lookup"><span data-stu-id="cf946-231">Scope defines to whom and context defines where your app is available.</span></span>

> [!NOTE]
> <span data-ttu-id="cf946-232">Essayez de mettre à jour le manifeste de votre application avec [le schéma de manifeste.](../resources/schema/manifest-schema-dev-preview.md)</span><span class="sxs-lookup"><span data-stu-id="cf946-232">Try updating your app manifest with the [manifest schema](../resources/schema/manifest-schema-dev-preview.md).</span></span>

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

### <a name="context-property"></a><span data-ttu-id="cf946-233">Propriété Context</span><span class="sxs-lookup"><span data-stu-id="cf946-233">Context property</span></span>

<span data-ttu-id="cf946-234">`context`L’onglet et `scopes` les propriétés vous permettent de déterminer où votre application doit apparaître.</span><span class="sxs-lookup"><span data-stu-id="cf946-234">The tab `context` and `scopes` properties enable you to determine where your app must appear.</span></span> <span data-ttu-id="cf946-235">Les onglets de la `team` ou `groupchat` de l’étendue peuvent avoir plusieurs contextes.</span><span class="sxs-lookup"><span data-stu-id="cf946-235">Tabs in the `team` or `groupchat` scope can have more than one context.</span></span> <span data-ttu-id="cf946-236">Voici les valeurs de la propriété à partir de laquelle vous pouvez utiliser l’ensemble ou `context` certaines des valeurs :</span><span class="sxs-lookup"><span data-stu-id="cf946-236">Following are the values for the `context` property from which you can use all or some of the values:</span></span>

|<span data-ttu-id="cf946-237">Valeur</span><span class="sxs-lookup"><span data-stu-id="cf946-237">Value</span></span>|<span data-ttu-id="cf946-238">Description</span><span class="sxs-lookup"><span data-stu-id="cf946-238">Description</span></span>|
|---|---|
| <span data-ttu-id="cf946-239">**channelTab**</span><span class="sxs-lookup"><span data-stu-id="cf946-239">**channelTab**</span></span> | <span data-ttu-id="cf946-240">Onglet dans l’en-tête d’un canal d’équipe.</span><span class="sxs-lookup"><span data-stu-id="cf946-240">A tab in the header of a team channel.</span></span> |
| <span data-ttu-id="cf946-241">**privateChatTab**</span><span class="sxs-lookup"><span data-stu-id="cf946-241">**privateChatTab**</span></span> | <span data-ttu-id="cf946-242">Onglet dans l’en-tête d’une conversation de groupe entre un ensemble d’utilisateurs non dans le contexte d’une équipe ou d’une réunion.</span><span class="sxs-lookup"><span data-stu-id="cf946-242">A tab in the header of a group chat between a set of users not in the context of a team or meeting.</span></span> |
| <span data-ttu-id="cf946-243">**meetingChatTab**</span><span class="sxs-lookup"><span data-stu-id="cf946-243">**meetingChatTab**</span></span> | <span data-ttu-id="cf946-244">Onglet dans l’en-tête d’une conversation de groupe entre un ensemble d’utilisateurs dans le cadre d’une réunion programmée.</span><span class="sxs-lookup"><span data-stu-id="cf946-244">A tab in the header of a group chat between a set of users in the context of a scheduled meeting.</span></span> |
| <span data-ttu-id="cf946-245">**meetingDetailsTab**</span><span class="sxs-lookup"><span data-stu-id="cf946-245">**meetingDetailsTab**</span></span> | <span data-ttu-id="cf946-246">Onglet dans l’en-tête de l’affichage Détails de la réunion du calendrier.</span><span class="sxs-lookup"><span data-stu-id="cf946-246">A tab in the header of the meeting details view of the calendar.</span></span> |
| <span data-ttu-id="cf946-247">**meetingSidePanel**</span><span class="sxs-lookup"><span data-stu-id="cf946-247">**meetingSidePanel**</span></span> | <span data-ttu-id="cf946-248">Panneau en réunion ouvert via la barre unifiée (barre U).</span><span class="sxs-lookup"><span data-stu-id="cf946-248">An in-meeting panel opened via the unified bar (U-bar).</span></span> |

> [!NOTE]
> <span data-ttu-id="cf946-249">`Context` n’est actuellement pas prise en charge sur les clients mobiles.</span><span class="sxs-lookup"><span data-stu-id="cf946-249">`Context` property is currently not supported on mobile clients.</span></span>

## <a name="configure-your-app-for-meeting-scenarios"></a><span data-ttu-id="cf946-250">Configurer votre application pour les scénarios de réunion</span><span class="sxs-lookup"><span data-stu-id="cf946-250">Configure your app for meeting scenarios</span></span>

> [!NOTE]
> * <span data-ttu-id="cf946-251">Pour que votre application soit visible dans la galerie d’onglets, elle doit prendre en charge les onglets configurables et l’étendue de conversation de groupe.</span><span class="sxs-lookup"><span data-stu-id="cf946-251">For your app to be visible in the tab gallery it must support configurable tabs and the group chat scope.</span></span>
> * <span data-ttu-id="cf946-252">Les clients mobiles ne supportent les onglets qu’aux étapes préalables et post-réunion.</span><span class="sxs-lookup"><span data-stu-id="cf946-252">Mobile clients support tabs only in pre and post meeting stages.</span></span>
> * <span data-ttu-id="cf946-253">Les expériences en réunion qui sont des boîtes de dialogue et des onglets en réunion ne sont actuellement pas pris en charge sur les clients mobiles.</span><span class="sxs-lookup"><span data-stu-id="cf946-253">The in-meeting experiences that is in-meeting dialog box and tab is currently not supported on mobile clients.</span></span> <span data-ttu-id="cf946-254">Pour plus d’informations, [consultez des conseils pour les onglets mobiles](../tabs/design/tabs-mobile.md) lors de la création de vos onglets pour appareils mobiles.</span><span class="sxs-lookup"><span data-stu-id="cf946-254">For more information, see [guidance for tabs on mobile](../tabs/design/tabs-mobile.md) when creating your tabs for mobile.</span></span>

### <a name="before-a-meeting"></a><span data-ttu-id="cf946-255">Avant une réunion</span><span class="sxs-lookup"><span data-stu-id="cf946-255">Before a meeting</span></span>

<span data-ttu-id="cf946-256">Avant une réunion, les utilisateurs peuvent ajouter des onglets, des bots et des extensions de messagerie à une réunion.</span><span class="sxs-lookup"><span data-stu-id="cf946-256">Before a meeting, users can add tabs, bots and messaging extensions to a meeting.</span></span> <span data-ttu-id="cf946-257">Les utilisateurs ayant des rôles d’organisateur et de présentateur peuvent ajouter des onglets à une réunion.</span><span class="sxs-lookup"><span data-stu-id="cf946-257">Users with organizer and presenter roles can add tabs to a meeting.</span></span>

<span data-ttu-id="cf946-258">**Pour ajouter un onglet à une réunion**</span><span class="sxs-lookup"><span data-stu-id="cf946-258">**To add a tab to a meeting**</span></span>

1. <span data-ttu-id="cf946-259">Dans votre calendrier, sélectionnez une réunion à laquelle vous souhaitez ajouter un onglet.</span><span class="sxs-lookup"><span data-stu-id="cf946-259">In your calendar, select a meeting to which you want to add a tab.</span></span>
1. <span data-ttu-id="cf946-260">Sélectionnez **l’onglet Détails** et sélectionnez plus</span><span class="sxs-lookup"><span data-stu-id="cf946-260">Select the **Details** tab and select plus</span></span> <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/><span data-ttu-id="cf946-261">.</span><span class="sxs-lookup"><span data-stu-id="cf946-261">.</span></span> <span data-ttu-id="cf946-262">La galerie d’onglets s’affiche.</span><span class="sxs-lookup"><span data-stu-id="cf946-262">The tab gallery appears.</span></span>

    ![Expérience préalable à la réunion](../assets/images/apps-in-meetings/PreMeeting.png)

1. <span data-ttu-id="cf946-264">Dans la galerie d’onglets, sélectionnez l’application à ajouter et suivez les étapes nécessaires.</span><span class="sxs-lookup"><span data-stu-id="cf946-264">In the tab gallery, select the app that you want to add and follow the steps as required.</span></span> <span data-ttu-id="cf946-265">L’application est installée en tant qu’onglet.</span><span class="sxs-lookup"><span data-stu-id="cf946-265">The app is installed as a tab.</span></span>

<span data-ttu-id="cf946-266">**Pour ajouter une extension de messagerie à une réunion**</span><span class="sxs-lookup"><span data-stu-id="cf946-266">**To add a messaging extension to a meeting**</span></span>

1. <span data-ttu-id="cf946-267">Sélectionnez les ellipses ou le menu de dépassement &#x25CF;&#x25CF;&#x25CF; dans la zone composer un message de la conversation.</span><span class="sxs-lookup"><span data-stu-id="cf946-267">Select the ellipses or overflow menu &#x25CF;&#x25CF;&#x25CF; located in the compose message area in the chat.</span></span>
1. <span data-ttu-id="cf946-268">Sélectionnez l’application à ajouter et suivez les étapes nécessaires.</span><span class="sxs-lookup"><span data-stu-id="cf946-268">Select the app that you want to add and follow the steps as required.</span></span> <span data-ttu-id="cf946-269">L’application est installée en tant qu’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="cf946-269">The app is installed as a messaging extension.</span></span>

<span data-ttu-id="cf946-270">**Pour ajouter un bot à une réunion**</span><span class="sxs-lookup"><span data-stu-id="cf946-270">**To add a bot to a meeting**</span></span>

<span data-ttu-id="cf946-271">Dans une conversation de réunion, entrez **@** la clé et **sélectionnez Obtenir des bots.**</span><span class="sxs-lookup"><span data-stu-id="cf946-271">In a meeting chat enter the **@** key and select **Get bots**.</span></span>

> [!NOTE]
> * <span data-ttu-id="cf946-272">L’identité de l’utilisateur doit être confirmée à [l’aide de l' ssO Onglets.](../tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="cf946-272">The user identity must be confirmed using [Tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="cf946-273">Après l’authentification, l’application peut récupérer le rôle d’utilisateur à l’aide de `GetParticipant` l’API.</span><span class="sxs-lookup"><span data-stu-id="cf946-273">After authentication, the app can retrieve the user role using the `GetParticipant` API.</span></span>
> * <span data-ttu-id="cf946-274">En fonction du rôle utilisateur, l’application a la possibilité de fournir des expériences spécifiques au rôle.</span><span class="sxs-lookup"><span data-stu-id="cf946-274">Based on the user role, the app has the capability to provide role specific experiences.</span></span> <span data-ttu-id="cf946-275">Par exemple, une application de sondage permet uniquement aux organisateurs et aux présentateurs de créer un sondage.</span><span class="sxs-lookup"><span data-stu-id="cf946-275">For example, a polling app allows only organizers and presenters to create a new poll.</span></span>
> * <span data-ttu-id="cf946-276">Les attributions de rôle peuvent être modifiées pendant une réunion.</span><span class="sxs-lookup"><span data-stu-id="cf946-276">Role assignments can be changed while a meeting is in progress.</span></span> <span data-ttu-id="cf946-277">Pour plus d’informations, voir [les rôles dans une réunion Teams.](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)</span><span class="sxs-lookup"><span data-stu-id="cf946-277">For more information, see [roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span>

### <a name="during-a-meeting"></a><span data-ttu-id="cf946-278">Pendant une réunion</span><span class="sxs-lookup"><span data-stu-id="cf946-278">During a meeting</span></span>

#### <a name="sidepanel"></a><span data-ttu-id="cf946-279">sidePanel</span><span class="sxs-lookup"><span data-stu-id="cf946-279">sidePanel</span></span>

<span data-ttu-id="cf946-280">Avec sidePanel, vous pouvez personnaliser les expériences d’une réunion qui permettent aux organisateurs et aux présentateurs d’avoir différents ensembles d’affichages et d’actions.</span><span class="sxs-lookup"><span data-stu-id="cf946-280">With the sidePanel, you can customize experiences in a meeting that enable organizers and presenters to have different set of views and actions.</span></span> <span data-ttu-id="cf946-281">Dans le manifeste de votre application, vous devez ajouter sidePanel au tableau de contexte.</span><span class="sxs-lookup"><span data-stu-id="cf946-281">In your app manifest, you must add sidePanel to the context array.</span></span> <span data-ttu-id="cf946-282">Dans la réunion et dans tous les scénarios, l’application est rendue dans un onglet de réunion de 320 pixels de largeur.</span><span class="sxs-lookup"><span data-stu-id="cf946-282">In the meeting and in all scenarios, the app is rendered in an in-meeting tab that is 320 pixels in width.</span></span> <span data-ttu-id="cf946-283">Pour plus d’informations, [voir l’interface FrameContext.](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)</span><span class="sxs-lookup"><span data-stu-id="cf946-283">For more information, see [FrameContext interface](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
).</span></span>

<span data-ttu-id="cf946-284">Pour utiliser `userContext` l’API pour router les demandes en conséquence, consultez [le SDK Teams.](../tabs/how-to/access-teams-context.md#user-context)</span><span class="sxs-lookup"><span data-stu-id="cf946-284">To use the `userContext` API to route requests accordingly, see [Teams SDK](../tabs/how-to/access-teams-context.md#user-context).</span></span> <span data-ttu-id="cf946-285">Voir [flux d’authentification Teams pour les onglets.](../tabs/how-to/authentication/auth-flow-tab.md)</span><span class="sxs-lookup"><span data-stu-id="cf946-285">See [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span> <span data-ttu-id="cf946-286">Le flux d’authentification pour les onglets est très similaire au flux d’authentification pour les sites web.</span><span class="sxs-lookup"><span data-stu-id="cf946-286">Authentication flow for tabs is very similar to the auth flow for websites.</span></span> <span data-ttu-id="cf946-287">Par conséquent, les onglets peuvent utiliser OAuth 2.0 directement.</span><span class="sxs-lookup"><span data-stu-id="cf946-287">So tabs can use OAuth 2.0 directly.</span></span> <span data-ttu-id="cf946-288">Voir la plateforme d’identité Microsoft et le flux de [code d’autorisation OAuth 2.0.](/azure/active-directory/develop/v2-oauth2-auth-code-flow)</span><span class="sxs-lookup"><span data-stu-id="cf946-288">See, [Microsoft identity platform and OAuth 2.0 authorization code flow](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span></span>

<span data-ttu-id="cf946-289">L’extension de messagerie fonctionne comme prévu lorsqu’un utilisateur est dans un affichage en réunion et qu’il peut publier des cartes d’extension de message de composition.</span><span class="sxs-lookup"><span data-stu-id="cf946-289">Messaging extension works as expected when a user is in an in-meeting view and the user can post compose message extension cards.</span></span> <span data-ttu-id="cf946-290">AppName en réunion est une boîte à outils qui indique le nom de l’application dans la barre U de la réunion.</span><span class="sxs-lookup"><span data-stu-id="cf946-290">AppName in-meeting is a tooltip that states the app name in-meeting U-bar.</span></span>

#### <a name="in-meeting-dialog"></a><span data-ttu-id="cf946-291">Boîtes de dialogue en réunion</span><span class="sxs-lookup"><span data-stu-id="cf946-291">In-meeting dialog</span></span>

<span data-ttu-id="cf946-292">La boîte de dialogue de réunion peut être utilisée pour impliquer les participants pendant la réunion et collecter des informations ou des commentaires pendant la réunion.</span><span class="sxs-lookup"><span data-stu-id="cf946-292">The in-meeting dialog box can be used to engage participants during the meeting and collect information or feedback during the meeting.</span></span> <span data-ttu-id="cf946-293">Utilisez [`NotificationSignal`](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) l’API pour signaler qu’une notification de bulle doit être déclenchée.</span><span class="sxs-lookup"><span data-stu-id="cf946-293">Use the [`NotificationSignal`](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) API to signal that a bubble notification must be triggered.</span></span> <span data-ttu-id="cf946-294">Dans le cadre de la charge utile de demande de notification, incluez l’URL où le contenu à afficher est hébergé.</span><span class="sxs-lookup"><span data-stu-id="cf946-294">As part of the notification request payload, include the URL where the content to be shown is hosted.</span></span>

<span data-ttu-id="cf946-295">La boîte de dialogue en réunion ne doit pas utiliser le module de tâche.</span><span class="sxs-lookup"><span data-stu-id="cf946-295">In-meeting dialog must not use task module.</span></span> <span data-ttu-id="cf946-296">Le module de tâche n’est pas appelé dans une conversation de réunion.</span><span class="sxs-lookup"><span data-stu-id="cf946-296">Task module is not invoked in a meeting chat.</span></span> <span data-ttu-id="cf946-297">Une URL de ressource externe est utilisée pour afficher une bulle de contenu dans une réunion.</span><span class="sxs-lookup"><span data-stu-id="cf946-297">An external resource URL is used to display content bubble in a meeting.</span></span> <span data-ttu-id="cf946-298">Vous pouvez utiliser la `submitTask` méthode pour envoyer des données dans une conversation de réunion.</span><span class="sxs-lookup"><span data-stu-id="cf946-298">You can use the `submitTask` method to submit data in a meeting chat.</span></span>

> [!NOTE]
> * <span data-ttu-id="cf946-299">Vous devez appeler la [fonction submitTask()](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) pour ignorer automatiquement une fois qu’un utilisateur a pris une action dans l’affichage web.</span><span class="sxs-lookup"><span data-stu-id="cf946-299">You must invoke the [submitTask()](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) function to dismiss automatically after a user takes an action in the web-view.</span></span> <span data-ttu-id="cf946-300">Il s’agit d’une condition requise pour la soumission d’application.</span><span class="sxs-lookup"><span data-stu-id="cf946-300">This is a requirement for app submission.</span></span> <span data-ttu-id="cf946-301">Pour plus d’informations, voir le module de [tâche du SDK Teams.](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="cf946-301">For more information, see [Teams SDK task module](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span></span>
> * <span data-ttu-id="cf946-302">Si vous souhaitez que votre application prise en charge des utilisateurs anonymes, votre charge utile de demande d’appel initiale doit reposer sur les métadonnées de la demande dans l’objet, et non sur `from.id` `from` les `from.aadObjectId` métadonnées de la demande.</span><span class="sxs-lookup"><span data-stu-id="cf946-302">If you want your app to support anonymous users, your initial invoke request payload must rely on the `from.id` request metadata in the `from` object, not the `from.aadObjectId` request metadata.</span></span> <span data-ttu-id="cf946-303">`from.id` est l’ID utilisateur et `from.aadObjectId` l’ID Azure Active Directory (AAD) de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="cf946-303">`from.id` is the user ID and `from.aadObjectId` is the Azure Active Directory (AAD) ID of the user.</span></span> <span data-ttu-id="cf946-304">Pour plus d’informations, voir [l’utilisation de modules de tâche](../task-modules-and-cards/task-modules/task-modules-tabs.md) dans les onglets [et créer et envoyer le module de tâche.](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)</span><span class="sxs-lookup"><span data-stu-id="cf946-304">For more information, see [using task modules in tabs](../task-modules-and-cards/task-modules/task-modules-tabs.md) and [create and send the task module](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).</span></span>

### <a name="after-a-meeting"></a><span data-ttu-id="cf946-305">Après une réunion</span><span class="sxs-lookup"><span data-stu-id="cf946-305">After a meeting</span></span>

<span data-ttu-id="cf946-306">Les configurations post-réunion et préalable à la réunion sont équivalentes.</span><span class="sxs-lookup"><span data-stu-id="cf946-306">The post-meeting and pre-meeting configurations are equivalent.</span></span>

## <a name="code-sample"></a><span data-ttu-id="cf946-307">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="cf946-307">Code sample</span></span>

|<span data-ttu-id="cf946-308">Exemple de nom</span><span class="sxs-lookup"><span data-stu-id="cf946-308">Sample name</span></span> | <span data-ttu-id="cf946-309">Description</span><span class="sxs-lookup"><span data-stu-id="cf946-309">Description</span></span> | <span data-ttu-id="cf946-310">C#</span><span class="sxs-lookup"><span data-stu-id="cf946-310">C#</span></span> |
|----------------|-----------------|--------------|
| <span data-ttu-id="cf946-311">Extensibilité des réunions</span><span class="sxs-lookup"><span data-stu-id="cf946-311">Meetings extensibility</span></span> | <span data-ttu-id="cf946-312">Exemple d’extensibilité de réunion Microsoft Teams pour transmettre des jetons.</span><span class="sxs-lookup"><span data-stu-id="cf946-312">Microsoft Teams meeting extensibility sample for passing tokens.</span></span> | [<span data-ttu-id="cf946-313">View</span><span class="sxs-lookup"><span data-stu-id="cf946-313">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) |
| <span data-ttu-id="cf946-314">Bot de bulle de contenu de réunion</span><span class="sxs-lookup"><span data-stu-id="cf946-314">Meeting content bubble bot</span></span> | <span data-ttu-id="cf946-315">Exemple d’extensibilité de réunion Microsoft Teams pour l’interaction avec le bot de bulles de contenu dans une réunion.</span><span class="sxs-lookup"><span data-stu-id="cf946-315">Microsoft Teams meeting extensibility sample for interacting with content bubble bot in a meeting.</span></span> | [<span data-ttu-id="cf946-316">View</span><span class="sxs-lookup"><span data-stu-id="cf946-316">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |

## <a name="see-also"></a><span data-ttu-id="cf946-317">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="cf946-317">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cf946-318">Recommandations en matière de conception de boîte de dialogue en réunion</span><span class="sxs-lookup"><span data-stu-id="cf946-318">In-meeting dialog design guidelines</span></span>](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
> [!div class="nextstepaction"]
> [<span data-ttu-id="cf946-319">Flux d’authentification Teams pour les onglets</span><span class="sxs-lookup"><span data-stu-id="cf946-319">Teams authentication flow for tabs</span></span>](../tabs/how-to/authentication/auth-flow-tab.md)
