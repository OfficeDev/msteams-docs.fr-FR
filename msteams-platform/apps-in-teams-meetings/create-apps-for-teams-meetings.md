---
title: Conditions préalables et références d’API pour les applications dans les réunions Teams
author: laujan
description: Travailler avec des applications pour Teams réunions
ms.topic: conceptual
ms.author: lajanuar
localization_priority: Normal
keywords: Api de rôle d’utilisateur participant aux réunions teams apps
ms.openlocfilehash: f42e827801e21bbd039f52dbb685d4559ae5cf81
ms.sourcegitcommit: 37325179a532897fafbe827dcf9a7ca5fa5e7d0b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/09/2021
ms.locfileid: "52853507"
---
# <a name="prerequisites-and-api-references-for-apps-in-teams-meetings"></a><span data-ttu-id="6114a-104">Conditions préalables et références d’API pour les applications dans les réunions Teams</span><span class="sxs-lookup"><span data-stu-id="6114a-104">Prerequisites and API references for apps in Teams meetings</span></span>

<span data-ttu-id="6114a-105">Pour développer les fonctionnalités de vos applications tout au long du cycle de vie des réunions, Teams vous permet de travailler avec des applications pour Teams réunions.</span><span class="sxs-lookup"><span data-stu-id="6114a-105">To expand the capabilities of your apps across the meeting lifecycle, Teams enables you to work with apps for Teams meetings.</span></span> <span data-ttu-id="6114a-106">Vous devez respecter les conditions préalables et utiliser les références de l’API des applications de réunion pour améliorer l’expérience de réunion.</span><span class="sxs-lookup"><span data-stu-id="6114a-106">You must  go through the prerequisites and you can use the meeting apps API references to enhance the meeting experience.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6114a-107">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="6114a-107">Prerequisites</span></span>

<span data-ttu-id="6114a-108">Avant de travailler avec des applications pour Teams réunions, vous devez comprendre les choses suivantes :</span><span class="sxs-lookup"><span data-stu-id="6114a-108">Before you work with apps for Teams meetings, you must have an understanding of the following:</span></span>

* <span data-ttu-id="6114a-109">Vous devez savoir comment développer des Teams applications.</span><span class="sxs-lookup"><span data-stu-id="6114a-109">You must have knowledge of how to develop Teams apps.</span></span> <span data-ttu-id="6114a-110">Pour plus d’informations, [voir Teams développement d’applications.](../overview.md)</span><span class="sxs-lookup"><span data-stu-id="6114a-110">For more information, see [Teams app development](../overview.md).</span></span>

* <span data-ttu-id="6114a-111">Vous devez mettre à jour Teams manifeste de l’application pour indiquer que l’application est disponible pour les réunions.</span><span class="sxs-lookup"><span data-stu-id="6114a-111">You must update the Teams app manifest to indicate that the app is available for meetings.</span></span> <span data-ttu-id="6114a-112">Pour plus d’informations, voir [le manifeste de l’application.](enable-and-configure-your-app-for-teams-meetings.md#update-your-app-manifest)</span><span class="sxs-lookup"><span data-stu-id="6114a-112">For more information, see [app manifest](enable-and-configure-your-app-for-teams-meetings.md#update-your-app-manifest).</span></span>

* <span data-ttu-id="6114a-113">Votre application doit prendre en charge les onglets configurables dans l’étendue groupchat, pour que votre application fonctionne dans le cycle de vie de la réunion sous la mesure d’un onglet. Pour plus d’informations, voir [étendue groupchat](../resources/schema/manifest-schema.md#configurabletabs) et [créer un onglet de groupe.](../build-your-first-app/build-channel-tab.md)</span><span class="sxs-lookup"><span data-stu-id="6114a-113">Your app must support configurable tabs in the groupchat scope, for your app to function in the meeting lifecycle as a tab. For more information, see [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs) and [build a group tab](../build-your-first-app/build-channel-tab.md).</span></span>

* <span data-ttu-id="6114a-114">Vous devez respecter les recommandations générales Teams la conception d’onglets pour les scénarios préalables et post-réunion.</span><span class="sxs-lookup"><span data-stu-id="6114a-114">You must adhere to general Teams tab design guidelines for pre and post-meeting scenarios.</span></span> <span data-ttu-id="6114a-115">Pour les expériences pendant les réunions, reportez-vous aux recommandations en matière de conception de l’onglet réunion et de la boîte de dialogue en réunion.</span><span class="sxs-lookup"><span data-stu-id="6114a-115">For experiences during meetings, refer to the in-meeting tab and in-meeting dialog design guidelines.</span></span> <span data-ttu-id="6114a-116">Pour plus d’informations, [voir Teams recommandations](../tabs/design/tabs.md)en matière de conception d’onglets, [](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab)de recommandations en matière de conception d’onglets en réunion et de conception de boîte de dialogue en [réunion.](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)</span><span class="sxs-lookup"><span data-stu-id="6114a-116">For more information, see [Teams tab design guidelines](../tabs/design/tabs.md), [in-meeting tab design guidelines](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab), and [in-meeting dialog design guidelines](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog).</span></span>

* <span data-ttu-id="6114a-117">Vous devez prendre en charge l’étendue pour activer votre application dans les conversations `groupchat` préalables à la réunion et post-réunion.</span><span class="sxs-lookup"><span data-stu-id="6114a-117">You must support the `groupchat` scope to enable your app in pre-meeting and post-meeting chats.</span></span> <span data-ttu-id="6114a-118">Avec l’expérience d’application de pré-réunion, vous pouvez rechercher et ajouter des applications de réunion et effectuer des tâches préalables à la réunion.</span><span class="sxs-lookup"><span data-stu-id="6114a-118">With the pre-meeting app experience, you can find and add meeting apps and perform pre-meeting tasks.</span></span> <span data-ttu-id="6114a-119">Avec l’expérience d’application post-réunion, vous pouvez afficher les résultats de la réunion, tels que les résultats des sondages ou les commentaires.</span><span class="sxs-lookup"><span data-stu-id="6114a-119">With post-meeting app experience, you can view the results of the meeting, such as poll survey results or feedback.</span></span>

* <span data-ttu-id="6114a-120">Les paramètres d’URL de l’API de réunion doivent avoir `meetingId` `userId` , et `tenantId` .</span><span class="sxs-lookup"><span data-stu-id="6114a-120">Meeting API URL parameters must have `meetingId`, `userId`, and `tenantId`.</span></span> <span data-ttu-id="6114a-121">Ceux-ci sont disponibles dans le cadre de l Teams du SDK client et du bot.</span><span class="sxs-lookup"><span data-stu-id="6114a-121">These are available as part of the Teams Client SDK and bot activity.</span></span> <span data-ttu-id="6114a-122">En outre, vous pouvez récupérer des informations fiables pour l’ID d’utilisateur et l’ID de locataire à l’aide de l’authentification [SSO onglet](../tabs/how-to/authentication/auth-aad-sso.md).</span><span class="sxs-lookup"><span data-stu-id="6114a-122">In addition, you can retrieve reliable information for user ID and tenant ID using [tab SSO authentication](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>

* <span data-ttu-id="6114a-123">`GetParticipant`L’API doit avoir un ID et une inscription de bot pour générer des jetons d’th.</span><span class="sxs-lookup"><span data-stu-id="6114a-123">The `GetParticipant` API must have a bot registration and ID to generate auth tokens.</span></span> <span data-ttu-id="6114a-124">Pour plus d’informations, voir [l’inscription et l’ID du bot.](../build-your-first-app/build-bot.md)</span><span class="sxs-lookup"><span data-stu-id="6114a-124">For more information, see [bot registration and ID](../build-your-first-app/build-bot.md).</span></span>

* <span data-ttu-id="6114a-125">Pour que votre application soit mise à jour en temps réel, elle doit être à jour en fonction des activités d’événements de la réunion.</span><span class="sxs-lookup"><span data-stu-id="6114a-125">For your app to update in real time, it must be up-to-date based on event activities in the meeting.</span></span> <span data-ttu-id="6114a-126">Ces événements peuvent se trouver dans la boîte de dialogue de réunion et dans d’autres étapes du cycle de vie de la réunion.</span><span class="sxs-lookup"><span data-stu-id="6114a-126">These events can be within the in-meeting dialog box and other stages across the meeting lifecycle.</span></span> <span data-ttu-id="6114a-127">Pour la boîte de dialogue de réunion, voir paramètre `bot Id` d’achèvement dans `NotificationSignal` l’API.</span><span class="sxs-lookup"><span data-stu-id="6114a-127">For the in-meeting dialog box, see completion `bot Id` parameter in `NotificationSignal` API.</span></span>

<span data-ttu-id="6114a-128">Une fois que vous avez satisfait aux conditions préalables, vous pouvez utiliser les références de l’API des applications de réunion, qui vous permettent d’accéder aux informations à l’aide d’attributs et d’afficher `GetUserContext` `GetParticipant` du contenu `NotificationSignal` pertinent.</span><span class="sxs-lookup"><span data-stu-id="6114a-128">After you have gone through the prerequisites, you can use the meeting apps API references `GetUserContext`, `GetParticipant`, and `NotificationSignal` that enable you to access information using attributes and display relevant content.</span></span>

## <a name="meeting-apps-api-references"></a><span data-ttu-id="6114a-129">Références de l’API des applications de réunion</span><span class="sxs-lookup"><span data-stu-id="6114a-129">Meeting apps API references</span></span>

<span data-ttu-id="6114a-130">Les nouvelles fonctionnalités de réunion vous fournissent des API qui transforment l’expérience de réunion.</span><span class="sxs-lookup"><span data-stu-id="6114a-130">The new meeting extensibilities provide you with APIs that transform the meeting experience.</span></span> <span data-ttu-id="6114a-131">Avec cette nouvelle fonctionnalité, vous pouvez créer des applications ou intégrer des applications existantes dans le cycle de vie de la réunion.</span><span class="sxs-lookup"><span data-stu-id="6114a-131">With this new capability, you can build apps or integrate existing apps within the meeting lifecycle.</span></span> <span data-ttu-id="6114a-132">Vous pouvez utiliser les API pour que votre application soit au courant de la réunion.</span><span class="sxs-lookup"><span data-stu-id="6114a-132">You can use the APIs to make your app aware of the meeting.</span></span> <span data-ttu-id="6114a-133">Vous pouvez choisir les API que vous souhaitez utiliser pour améliorer l’expérience de réunion.</span><span class="sxs-lookup"><span data-stu-id="6114a-133">You can choose which APIs you want to use to enhance the meeting experience.</span></span>

<span data-ttu-id="6114a-134">Le tableau suivant fournit la liste de ces API :</span><span class="sxs-lookup"><span data-stu-id="6114a-134">The following table provides a list of these APIs:</span></span>

|<span data-ttu-id="6114a-135">API</span><span class="sxs-lookup"><span data-stu-id="6114a-135">API</span></span>|<span data-ttu-id="6114a-136">Description</span><span class="sxs-lookup"><span data-stu-id="6114a-136">Description</span></span>|<span data-ttu-id="6114a-137">Demande</span><span class="sxs-lookup"><span data-stu-id="6114a-137">Request</span></span>|<span data-ttu-id="6114a-138">Source</span><span class="sxs-lookup"><span data-stu-id="6114a-138">Source</span></span>|
|---|---|----|---|
|<span data-ttu-id="6114a-139">**GetUserContext**</span><span class="sxs-lookup"><span data-stu-id="6114a-139">**GetUserContext**</span></span>| <span data-ttu-id="6114a-140">Cette API vous permet d’obtenir des informations contextuelles pour afficher du contenu pertinent dans Teams onglet.</span><span class="sxs-lookup"><span data-stu-id="6114a-140">This API enables you to get contextual information to display relevant content in a Teams tab.</span></span> |<span data-ttu-id="6114a-141">_**microsoftTeams.getContext( ( ) => { /*...\* / } )*\*_</span><span class="sxs-lookup"><span data-stu-id="6114a-141">_**microsoftTeams.getContext( ( ) => {  /*...*/ } )**_</span></span>|<span data-ttu-id="6114a-142">Microsoft Teams Client SDK</span><span class="sxs-lookup"><span data-stu-id="6114a-142">Microsoft Teams Client SDK</span></span>|
|<span data-ttu-id="6114a-143">**GetParticipant**</span><span class="sxs-lookup"><span data-stu-id="6114a-143">**GetParticipant**</span></span>| <span data-ttu-id="6114a-144">Cette API permet à un bot de récupérer les informations des participants par ID de réunion et ID de participant.</span><span class="sxs-lookup"><span data-stu-id="6114a-144">This API allows a bot to fetch participant information by meeting ID and participant ID.</span></span> |<span data-ttu-id="6114a-145">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span><span class="sxs-lookup"><span data-stu-id="6114a-145">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span></span> |<span data-ttu-id="6114a-146">Microsoft Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="6114a-146">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="6114a-147">**NotificationSignal**</span><span class="sxs-lookup"><span data-stu-id="6114a-147">**NotificationSignal**</span></span> | <span data-ttu-id="6114a-148">Cette API vous permet de fournir des signaux de réunion fournis à l’aide de l’API de notification de conversation existante pour la conversation utilisateur-bot.</span><span class="sxs-lookup"><span data-stu-id="6114a-148">This API enables you to provide meeting signals that are delivered using the existing conversation notification API for user-bot chat.</span></span> <span data-ttu-id="6114a-149">Il vous permet de signaler en fonction de l’action de l’utilisateur qui affiche une boîte de dialogue en réunion.</span><span class="sxs-lookup"><span data-stu-id="6114a-149">It allows you to signal based on user action that shows an in-meeting dialog box.</span></span> |<span data-ttu-id="6114a-150">**POST** _**/v3/conversations/{conversationId}/activities**_</span><span class="sxs-lookup"><span data-stu-id="6114a-150">**POST** _**/v3/conversations/{conversationId}/activities**_</span></span>|<span data-ttu-id="6114a-151">Microsoft Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="6114a-151">Microsoft Bot Framework SDK</span></span>|

### <a name="getusercontext-api"></a><span data-ttu-id="6114a-152">GetUserContext API</span><span class="sxs-lookup"><span data-stu-id="6114a-152">GetUserContext API</span></span>

<span data-ttu-id="6114a-153">Pour identifier et récupérer des informations contextuelles pour le contenu de votre onglet, voir obtenir le [contexte de Teams onglet .](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) est utilisé par un onglet lors de l’exécution dans le contexte de réunion et est `meetingId` ajouté pour la charge utile de réponse.</span><span class="sxs-lookup"><span data-stu-id="6114a-153">To identify and retrieve contextual information for your tab content, see [get context for your Teams tab](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library). `meetingId` is used by a tab when running in the meeting context and is added for the response payload.</span></span>

### <a name="getparticipant-api"></a><span data-ttu-id="6114a-154">GetParticipant API</span><span class="sxs-lookup"><span data-stu-id="6114a-154">GetParticipant API</span></span>

> [!NOTE]
> * <span data-ttu-id="6114a-155">Ne pas mettre en cache les rôles des participants, car l’organisateur de la réunion peut modifier les rôles à tout moment.</span><span class="sxs-lookup"><span data-stu-id="6114a-155">Do not cache participant roles since the meeting organizer can change the roles any time.</span></span>
> * <span data-ttu-id="6114a-156">Teams ne prend actuellement pas en charge les grandes listes de distribution ou les tailles de liste de plus de 350 participants pour `GetParticipant` l’API.</span><span class="sxs-lookup"><span data-stu-id="6114a-156">Teams does not currently support large distribution lists or roster sizes of more than 350 participants for the `GetParticipant` API.</span></span>

<span data-ttu-id="6114a-157">L’API permet à un bot de récupérer les informations des participants par ID de réunion et `GetParticipant` ID de participant.</span><span class="sxs-lookup"><span data-stu-id="6114a-157">The `GetParticipant` API allows a bot to fetch participant information by meeting ID and participant ID.</span></span> <span data-ttu-id="6114a-158">L’API inclut des paramètres de requête, des exemples et des codes de réponse.</span><span class="sxs-lookup"><span data-stu-id="6114a-158">The API includes query parameters, examples, and response codes.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="6114a-159">Paramètres de requête</span><span class="sxs-lookup"><span data-stu-id="6114a-159">Query parameters</span></span>

<span data-ttu-id="6114a-160">`GetParticipant`L’API inclut les paramètres de requête suivants :</span><span class="sxs-lookup"><span data-stu-id="6114a-160">The `GetParticipant` API includes the following query parameters:</span></span>

|<span data-ttu-id="6114a-161">Valeur</span><span class="sxs-lookup"><span data-stu-id="6114a-161">Value</span></span>|<span data-ttu-id="6114a-162">Type</span><span class="sxs-lookup"><span data-stu-id="6114a-162">Type</span></span>|<span data-ttu-id="6114a-163">Requis</span><span class="sxs-lookup"><span data-stu-id="6114a-163">Required</span></span>|<span data-ttu-id="6114a-164">Description</span><span class="sxs-lookup"><span data-stu-id="6114a-164">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="6114a-165">**meetingId**</span><span class="sxs-lookup"><span data-stu-id="6114a-165">**meetingId**</span></span>| <span data-ttu-id="6114a-166">String</span><span class="sxs-lookup"><span data-stu-id="6114a-166">String</span></span> | <span data-ttu-id="6114a-167">Oui</span><span class="sxs-lookup"><span data-stu-id="6114a-167">Yes</span></span> | <span data-ttu-id="6114a-168">L’identificateur de réunion est disponible via Bot Invoke et Teams Client SDK.</span><span class="sxs-lookup"><span data-stu-id="6114a-168">The meeting identifier is available through Bot Invoke and Teams Client SDK.</span></span>|
|<span data-ttu-id="6114a-169">**participantId**</span><span class="sxs-lookup"><span data-stu-id="6114a-169">**participantId**</span></span>| <span data-ttu-id="6114a-170">String</span><span class="sxs-lookup"><span data-stu-id="6114a-170">String</span></span> | <span data-ttu-id="6114a-171">Oui</span><span class="sxs-lookup"><span data-stu-id="6114a-171">Yes</span></span> | <span data-ttu-id="6114a-172">L’ID de participant est l’ID utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6114a-172">The participant ID is the user ID.</span></span> <span data-ttu-id="6114a-173">Il est disponible dans tabulation SSO, Bot Invoke et Teams Client SDK.</span><span class="sxs-lookup"><span data-stu-id="6114a-173">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="6114a-174">Il est recommandé d’obtenir un ID de participant à partir de l' sso tabulation.</span><span class="sxs-lookup"><span data-stu-id="6114a-174">It is recommended to get a participant ID from the Tab SSO.</span></span> |
|<span data-ttu-id="6114a-175">**tenantId**</span><span class="sxs-lookup"><span data-stu-id="6114a-175">**tenantId**</span></span>| <span data-ttu-id="6114a-176">String</span><span class="sxs-lookup"><span data-stu-id="6114a-176">String</span></span> | <span data-ttu-id="6114a-177">Oui</span><span class="sxs-lookup"><span data-stu-id="6114a-177">Yes</span></span> | <span data-ttu-id="6114a-178">L’ID de client est requis pour les utilisateurs du client.</span><span class="sxs-lookup"><span data-stu-id="6114a-178">The tenant ID is required for the tenant users.</span></span> <span data-ttu-id="6114a-179">Il est disponible dans tabulation SSO, Bot Invoke et Teams Client SDK.</span><span class="sxs-lookup"><span data-stu-id="6114a-179">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="6114a-180">Il est recommandé d’obtenir un ID de client à partir de l' sso tabulation.</span><span class="sxs-lookup"><span data-stu-id="6114a-180">It is recommended to get a tenant ID from the Tab SSO.</span></span> |

#### <a name="example"></a><span data-ttu-id="6114a-181">Exemple</span><span class="sxs-lookup"><span data-stu-id="6114a-181">Example</span></span>

<span data-ttu-id="6114a-182">`GetParticipant`L’API inclut les exemples suivants :</span><span class="sxs-lookup"><span data-stu-id="6114a-182">The `GetParticipant` API includes the following examples:</span></span>

# <a name="c"></a>[<span data-ttu-id="6114a-183">C#</span><span class="sxs-lookup"><span data-stu-id="6114a-183">C#</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="6114a-184">JavaScript</span><span class="sxs-lookup"><span data-stu-id="6114a-184">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="6114a-185">JSON</span><span class="sxs-lookup"><span data-stu-id="6114a-185">JSON</span></span>](#tab/json)

```http
GET /v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

* * *

<span data-ttu-id="6114a-186">Le corps de la réponse JSON pour `GetParticipant` l’API est :</span><span class="sxs-lookup"><span data-stu-id="6114a-186">The JSON response body for `GetParticipant` API is:</span></span>

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

#### <a name="response-codes"></a><span data-ttu-id="6114a-187">Codes de réponse</span><span class="sxs-lookup"><span data-stu-id="6114a-187">Response codes</span></span>

<span data-ttu-id="6114a-188">`GetParticipant`L’API inclut les codes de réponse suivants :</span><span class="sxs-lookup"><span data-stu-id="6114a-188">The `GetParticipant` API includes the following response codes:</span></span>

|<span data-ttu-id="6114a-189">Code de réponse</span><span class="sxs-lookup"><span data-stu-id="6114a-189">Response code</span></span>|<span data-ttu-id="6114a-190">Description</span><span class="sxs-lookup"><span data-stu-id="6114a-190">Description</span></span>|
|---|---|
| <span data-ttu-id="6114a-191">**403**</span><span class="sxs-lookup"><span data-stu-id="6114a-191">**403**</span></span> | <span data-ttu-id="6114a-192">L’application n’est pas autorisée à obtenir des informations sur les participants.</span><span class="sxs-lookup"><span data-stu-id="6114a-192">The app is not allowed to get participant information.</span></span> <span data-ttu-id="6114a-193">Il s’agit de la réponse d’erreur la plus courante et est déclenchée si l’application n’est pas installée dans la réunion.</span><span class="sxs-lookup"><span data-stu-id="6114a-193">This is the most common error response and is triggered if the app is not installed in the meeting.</span></span> <span data-ttu-id="6114a-194">Par exemple, si l’application est désactivée par l’administrateur client ou bloquée pendant la migration du site en direct.</span><span class="sxs-lookup"><span data-stu-id="6114a-194">For example, if the app is disabled by tenant admin or blocked during live site migration.</span></span>|
| <span data-ttu-id="6114a-195">**200**</span><span class="sxs-lookup"><span data-stu-id="6114a-195">**200**</span></span> | <span data-ttu-id="6114a-196">Les informations sur les participants sont récupérées avec succès.</span><span class="sxs-lookup"><span data-stu-id="6114a-196">The participant information is successfully retrieved.</span></span>|
| <span data-ttu-id="6114a-197">**401**</span><span class="sxs-lookup"><span data-stu-id="6114a-197">**401**</span></span> | <span data-ttu-id="6114a-198">L’application répond avec un jeton non valide.</span><span class="sxs-lookup"><span data-stu-id="6114a-198">The app responds with an invalid token.</span></span>|
| <span data-ttu-id="6114a-199">**404**</span><span class="sxs-lookup"><span data-stu-id="6114a-199">**404**</span></span> | <span data-ttu-id="6114a-200">La réunion a expiré ou le participant est in peut-être trouvé.</span><span class="sxs-lookup"><span data-stu-id="6114a-200">The meeting has either expired or participant cannot be found.</span></span>|
| <span data-ttu-id="6114a-201">**500**</span><span class="sxs-lookup"><span data-stu-id="6114a-201">**500**</span></span> | <span data-ttu-id="6114a-202">La réunion a expiré (plus de 60 jours) depuis la fin de la réunion ou les participants ne disposent pas d’autorisations en fonction de leur rôle.</span><span class="sxs-lookup"><span data-stu-id="6114a-202">The meeting has either expired (more than 60 days) since the meeting ended or the participants do not have permissions based on their role.</span></span>|

### <a name="notificationsignal-api"></a><span data-ttu-id="6114a-203">NotificationSignal API</span><span class="sxs-lookup"><span data-stu-id="6114a-203">NotificationSignal API</span></span>

<span data-ttu-id="6114a-204">Tous les utilisateurs d’une réunion reçoivent les notifications envoyées via `NotificationSignal` l’API.</span><span class="sxs-lookup"><span data-stu-id="6114a-204">All users in a meeting receive the notifications sent through the `NotificationSignal` API.</span></span>

> [!NOTE]
> * <span data-ttu-id="6114a-205">Lorsqu’une boîte de dialogue de réunion est invoquée, le contenu est présenté comme un message de conversation.</span><span class="sxs-lookup"><span data-stu-id="6114a-205">When an in-meeting dialog box is invoked, the content is presented as a chat message.</span></span>
> * <span data-ttu-id="6114a-206">Actuellement, l’envoi de notifications ciblées n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="6114a-206">Currently, sending targeted notifications is not supported.</span></span>

<span data-ttu-id="6114a-207">`NotificationSignal` L’API vous permet de fournir des signaux de réunion fournis à l’aide de l’API de notification de conversation existante pour la conversation utilisateur-bot.</span><span class="sxs-lookup"><span data-stu-id="6114a-207">`NotificationSignal` API enables you to provide meeting signals that are delivered using the existing conversation notification API for user-bot chat.</span></span> <span data-ttu-id="6114a-208">Cette API vous permet de signaler en fonction de l’action de l’utilisateur qui affiche une boîte de dialogue en réunion.</span><span class="sxs-lookup"><span data-stu-id="6114a-208">This API allows you to signal based on user action that shows an in-meeting dialog box.</span></span> <span data-ttu-id="6114a-209">L’API inclut le paramètre de requête, des exemples et des codes de réponse.</span><span class="sxs-lookup"><span data-stu-id="6114a-209">The API includes query parameter, examples, and response codes.</span></span>

#### <a name="query-parameter"></a><span data-ttu-id="6114a-210">Paramètre de requête</span><span class="sxs-lookup"><span data-stu-id="6114a-210">Query parameter</span></span>

<span data-ttu-id="6114a-211">`NotificationSignal`L’API inclut le paramètre de requête suivant :</span><span class="sxs-lookup"><span data-stu-id="6114a-211">The `NotificationSignal` API includes the following query parameter:</span></span>

|<span data-ttu-id="6114a-212">Valeur</span><span class="sxs-lookup"><span data-stu-id="6114a-212">Value</span></span>|<span data-ttu-id="6114a-213">Type</span><span class="sxs-lookup"><span data-stu-id="6114a-213">Type</span></span>|<span data-ttu-id="6114a-214">Requis</span><span class="sxs-lookup"><span data-stu-id="6114a-214">Required</span></span>|<span data-ttu-id="6114a-215">Description</span><span class="sxs-lookup"><span data-stu-id="6114a-215">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="6114a-216">**conversationId**</span><span class="sxs-lookup"><span data-stu-id="6114a-216">**conversationId**</span></span>| <span data-ttu-id="6114a-217">String</span><span class="sxs-lookup"><span data-stu-id="6114a-217">String</span></span> | <span data-ttu-id="6114a-218">Oui</span><span class="sxs-lookup"><span data-stu-id="6114a-218">Yes</span></span> | <span data-ttu-id="6114a-219">L’identificateur de conversation est disponible dans le cadre de Bot Invoke.</span><span class="sxs-lookup"><span data-stu-id="6114a-219">The conversation identifier is available as part of Bot Invoke.</span></span> |

#### <a name="examples"></a><span data-ttu-id="6114a-220">Exemples</span><span class="sxs-lookup"><span data-stu-id="6114a-220">Examples</span></span>

<span data-ttu-id="6114a-221">`Bot ID`L’objet est déclaré dans le manifeste et le bot reçoit un objet de résultat.</span><span class="sxs-lookup"><span data-stu-id="6114a-221">The `Bot ID` is declared in the manifest and the bot receives a result object.</span></span>

> [!NOTE]
> * <span data-ttu-id="6114a-222">Le `completionBotId` paramètre est facultatif dans `externalResourceUrl` l’exemple de charge utile demandé.</span><span class="sxs-lookup"><span data-stu-id="6114a-222">The `completionBotId` parameter of the `externalResourceUrl` is optional in the requested payload example.</span></span> <span data-ttu-id="6114a-223">`Bot ID` est déclaré dans le manifeste et le bot reçoit un objet de résultat.</span><span class="sxs-lookup"><span data-stu-id="6114a-223">`Bot ID` is declared in the manifest and the bot receives a result object.</span></span>
> * <span data-ttu-id="6114a-224">Les `externalResourceUrl` paramètres de largeur et de hauteur doivent être en pixels.</span><span class="sxs-lookup"><span data-stu-id="6114a-224">The `externalResourceUrl` width and height parameters must be in pixels.</span></span> <span data-ttu-id="6114a-225">Pour vous assurer que les dimensions sont dans les limites autorisées, consultez les [instructions de conception.](design/designing-apps-in-meetings.md)</span><span class="sxs-lookup"><span data-stu-id="6114a-225">To ensure the dimensions are within the allowed limits, see [design guidelines](design/designing-apps-in-meetings.md).</span></span>
> * <span data-ttu-id="6114a-226">L’URL est la page chargée en tant que dans la boîte de `<iframe>` dialogue de la réunion.</span><span class="sxs-lookup"><span data-stu-id="6114a-226">The URL is the page loaded as an `<iframe>` in the in-meeting dialog box.</span></span> <span data-ttu-id="6114a-227">Le domaine doit se trouver dans le tableau de l’application `validDomains` dans le manifeste de votre application.</span><span class="sxs-lookup"><span data-stu-id="6114a-227">The domain must be in the app's `validDomains` array in your app manifest.</span></span>

<span data-ttu-id="6114a-228">`NotificationSignal`L’API inclut les exemples suivants :</span><span class="sxs-lookup"><span data-stu-id="6114a-228">The `NotificationSignal` API includes the following examples:</span></span>

# <a name="c"></a>[<span data-ttu-id="6114a-229">C#</span><span class="sxs-lookup"><span data-stu-id="6114a-229">C#</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="6114a-230">JavaScript</span><span class="sxs-lookup"><span data-stu-id="6114a-230">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="6114a-231">JSON</span><span class="sxs-lookup"><span data-stu-id="6114a-231">JSON</span></span>](#tab/json)

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

---

#### <a name="response-codes"></a><span data-ttu-id="6114a-232">Codes de réponse</span><span class="sxs-lookup"><span data-stu-id="6114a-232">Response codes</span></span>

<span data-ttu-id="6114a-233">`NotificationSignal`L’API inclut les codes de réponse suivants :</span><span class="sxs-lookup"><span data-stu-id="6114a-233">The `NotificationSignal` API includes the following response codes:</span></span>

|<span data-ttu-id="6114a-234">Code de réponse</span><span class="sxs-lookup"><span data-stu-id="6114a-234">Response code</span></span>|<span data-ttu-id="6114a-235">Description</span><span class="sxs-lookup"><span data-stu-id="6114a-235">Description</span></span>|
|---|---|
| <span data-ttu-id="6114a-236">**201**</span><span class="sxs-lookup"><span data-stu-id="6114a-236">**201**</span></span> | <span data-ttu-id="6114a-237">L’activité avec le signal est envoyée avec succès.</span><span class="sxs-lookup"><span data-stu-id="6114a-237">The activity with signal is successfully sent.</span></span> |
| <span data-ttu-id="6114a-238">**401**</span><span class="sxs-lookup"><span data-stu-id="6114a-238">**401**</span></span> | <span data-ttu-id="6114a-239">L’application répond avec un jeton non valide.</span><span class="sxs-lookup"><span data-stu-id="6114a-239">The app responds with an invalid token.</span></span> |
| <span data-ttu-id="6114a-240">**403**</span><span class="sxs-lookup"><span data-stu-id="6114a-240">**403**</span></span> | <span data-ttu-id="6114a-241">L’application ne peut pas envoyer le signal.</span><span class="sxs-lookup"><span data-stu-id="6114a-241">The app is unable to send the signal.</span></span> <span data-ttu-id="6114a-242">Cela peut se produire pour diverses raisons, telles que la désactivation de l’application par l’administrateur client, le blocage de l’application pendant la migration du site en direct, etc.</span><span class="sxs-lookup"><span data-stu-id="6114a-242">This can happen due to various reasons such as the tenant admin disables the app, the app is blocked during live site migration, and so on.</span></span> <span data-ttu-id="6114a-243">Dans ce cas, la charge utile contient un message d’erreur détaillé.</span><span class="sxs-lookup"><span data-stu-id="6114a-243">In this case, the payload contains a detailed error message.</span></span> |
| <span data-ttu-id="6114a-244">**404**</span><span class="sxs-lookup"><span data-stu-id="6114a-244">**404**</span></span> | <span data-ttu-id="6114a-245">La conversation de réunion n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="6114a-245">The meeting chat does not exist.</span></span> |

## <a name="code-sample"></a><span data-ttu-id="6114a-246">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="6114a-246">Code sample</span></span>

|<span data-ttu-id="6114a-247">Exemple de nom</span><span class="sxs-lookup"><span data-stu-id="6114a-247">Sample name</span></span> | <span data-ttu-id="6114a-248">Description</span><span class="sxs-lookup"><span data-stu-id="6114a-248">Description</span></span> | <span data-ttu-id="6114a-249">.NET</span><span class="sxs-lookup"><span data-stu-id="6114a-249">.NET</span></span> | <span data-ttu-id="6114a-250">Node.js</span><span class="sxs-lookup"><span data-stu-id="6114a-250">Node.js</span></span> |
|----------------|-----------------|--------------|--------------|
| <span data-ttu-id="6114a-251">Extensibilité des réunions</span><span class="sxs-lookup"><span data-stu-id="6114a-251">Meetings extensibility</span></span> | <span data-ttu-id="6114a-252">Microsoft Teams’extensibilité de réunion pour transmettre des jetons.</span><span class="sxs-lookup"><span data-stu-id="6114a-252">Microsoft Teams meeting extensibility sample for passing tokens.</span></span> | [<span data-ttu-id="6114a-253">View</span><span class="sxs-lookup"><span data-stu-id="6114a-253">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [<span data-ttu-id="6114a-254">View</span><span class="sxs-lookup"><span data-stu-id="6114a-254">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
| <span data-ttu-id="6114a-255">Bot de bulle de contenu de réunion</span><span class="sxs-lookup"><span data-stu-id="6114a-255">Meeting content bubble bot</span></span> | <span data-ttu-id="6114a-256">Microsoft Teams exemple d’extensibilité de réunion pour l’interaction avec le bot de bulles de contenu dans une réunion.</span><span class="sxs-lookup"><span data-stu-id="6114a-256">Microsoft Teams meeting extensibility sample for interacting with content bubble bot in a meeting.</span></span> | [<span data-ttu-id="6114a-257">View</span><span class="sxs-lookup"><span data-stu-id="6114a-257">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |  [<span data-ttu-id="6114a-258">View</span><span class="sxs-lookup"><span data-stu-id="6114a-258">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs)|
| <span data-ttu-id="6114a-259">MeetingSidePanel</span><span class="sxs-lookup"><span data-stu-id="6114a-259">Meeting meetingSidePanel</span></span> | <span data-ttu-id="6114a-260">Microsoft Teams exemple d’extensibilité de réunion pour interagir avec le panneau latéral en réunion.</span><span class="sxs-lookup"><span data-stu-id="6114a-260">Microsoft Teams meeting extensibility sample for interacting with the side panel in-meeting.</span></span> | [<span data-ttu-id="6114a-261">View</span><span class="sxs-lookup"><span data-stu-id="6114a-261">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) | [<span data-ttu-id="6114a-262">View</span><span class="sxs-lookup"><span data-stu-id="6114a-262">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/nodejs)|

## <a name="see-also"></a><span data-ttu-id="6114a-263">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="6114a-263">See also</span></span>

* [<span data-ttu-id="6114a-264">Recommandations en matière de conception de boîte de dialogue en réunion</span><span class="sxs-lookup"><span data-stu-id="6114a-264">In-meeting dialog design guidelines</span></span>](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [<span data-ttu-id="6114a-265">Teams d’authentification pour les onglets</span><span class="sxs-lookup"><span data-stu-id="6114a-265">Teams authentication flow for tabs</span></span>](../tabs/how-to/authentication/auth-flow-tab.md)
* [<span data-ttu-id="6114a-266">Applications pour Teams réunions</span><span class="sxs-lookup"><span data-stu-id="6114a-266">Apps for Teams meetings</span></span>](teams-apps-in-meetings.md)

## <a name="next-step"></a><span data-ttu-id="6114a-267">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="6114a-267">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6114a-268">Activer et configurer vos applications pour Teams réunions</span><span class="sxs-lookup"><span data-stu-id="6114a-268">Enable and configure your apps for Teams meetings</span></span>](enable-and-configure-your-app-for-teams-meetings.md)
