---
title: Créer des applications pour les réunions Teams
author: laujan
description: créer des applications pour les réunions teams
ms.topic: conceptual
ms.author: lajanuar
keywords: applications Team Apps Meeting User Role Role API
ms.openlocfilehash: 74f04ce9420110f721d95045fccee1d455cc7ea8
ms.sourcegitcommit: b0b2f148add54ccd17fdf863c2f1973a615f8657
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/16/2020
ms.locfileid: "48487839"
---
# <a name="create-apps-for-teams-meetings-developer-preview"></a><span data-ttu-id="ade64-104">Créer des applications pour les réunions Teams (Aperçu pour les développeurs)</span><span class="sxs-lookup"><span data-stu-id="ade64-104">Create apps for Teams meetings (Developer Preview)</span></span>

>[!IMPORTANT]
> <span data-ttu-id="ade64-105">Les fonctionnalités incluses dans l’aperçu du développeur Microsoft teams sont fournies à des fins d’accès anticipé, de test et de commentaires uniquement.</span><span class="sxs-lookup"><span data-stu-id="ade64-105">Features included in Microsoft Teams Developer Preview are provided for early-access, testing, and feedback purposes only.</span></span> <span data-ttu-id="ade64-106">Ils peuvent être soumis à des modifications avant de devenir disponibles dans la publication publique et ne doivent pas être utilisés dans les applications de production.</span><span class="sxs-lookup"><span data-stu-id="ade64-106">They may undergo changes before becoming available in the public release and should not be used in production applications.</span></span>

## <a name="prerequisites-and-considerations"></a><span data-ttu-id="ade64-107">Conditions préalables et considérations</span><span class="sxs-lookup"><span data-stu-id="ade64-107">Prerequisites and considerations</span></span>

1. <span data-ttu-id="ade64-108">Les applications dans les réunions nécessitent des connaissances de base sur le [développement d’applications teams](../overview.md).</span><span class="sxs-lookup"><span data-stu-id="ade64-108">Apps in meetings require some basic knowledge of [Teams app development](../overview.md).</span></span> <span data-ttu-id="ade64-109">Une application dans une réunion peut comprendre des fonctionnalités d' [onglets](../tabs/what-are-tabs.md), de [robots](../bots/what-are-bots.md)et d' [extensions de messagerie](../messaging-extensions/what-are-messaging-extensions.md) , et nécessitera des mises à jour du manifeste d' [application](#update-your-app-manifest) teams pour indiquer que l’application est disponible pour les réunions.</span><span class="sxs-lookup"><span data-stu-id="ade64-109">An app in a meeting can comprise of [tabs](../tabs/what-are-tabs.md), [bots](../bots/what-are-bots.md), and [messaging extensions](../messaging-extensions/what-are-messaging-extensions.md) features and will require updates to the Teams [app manifest](#update-your-app-manifest) to indicate that the app is available for meetings</span></span>

1. <span data-ttu-id="ade64-110">Pour que votre application fonctionne dans le cycle de vie de la réunion sous la forme d’un onglet, elle doit prendre en charge les onglets configurables dans l' [étendue groupchat](../resources/schema/manifest-schema.md#configurabletabs).</span><span class="sxs-lookup"><span data-stu-id="ade64-110">For your app to function in the meeting lifecycle as a tab, it must support configurable tabs in the [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs).</span></span> <span data-ttu-id="ade64-111">*Voir* [étendre votre application teams avec un onglet personnalisé](../tabs/how-to/add-tab.md). La prise en charge de l' `groupchat` étendue activera votre application dans les conversations [pré-réunion](teams-apps-in-meetings.md#pre-meeting-app-experience) et [post-réunion](teams-apps-in-meetings.md#post-meeting-app-experience) .</span><span class="sxs-lookup"><span data-stu-id="ade64-111">*See* [Extend your Teams app with a custom tab](../tabs/how-to/add-tab.md). Supporting the `groupchat` scope will enable your app in [pre-meeting](teams-apps-in-meetings.md#pre-meeting-app-experience) and [post-meeting](teams-apps-in-meetings.md#post-meeting-app-experience) chats.</span></span>

1. <span data-ttu-id="ade64-112">Les paramètres de l’URL de l’API de réunion peuvent exiger `meetingId` , `userId` et les [tenantId](/onedrive/find-your-office-365-tenant-id) disponibles dans le cadre du kit de développement logiciel client teams et de l’activité du robot.</span><span class="sxs-lookup"><span data-stu-id="ade64-112">Meeting API URL parameters may require `meetingId`, `userId`, and the [tenantId](/onedrive/find-your-office-365-tenant-id) These are available as part of the Teams Client SDK and bot activity.</span></span> <span data-ttu-id="ade64-113">En outre, des informations fiables pour l’ID d’utilisateur et l’ID de client peuvent être récupérées à l’aide de [l’authentification SSO de tabulation](../tabs/how-to/authentication/auth-aad-sso.md).</span><span class="sxs-lookup"><span data-stu-id="ade64-113">Additionally, reliable information for user ID and tenant ID can be retrieved using [Tab SSO authentication](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>

1. <span data-ttu-id="ade64-114">Certaines API de réunion, telles que `GetParticipant` nécessiteront un [ID d’enregistrement et d’application bot](../bots/how-to/create-a-bot-for-teams.md#with-an-azure-subscription) pour générer des jetons d’authentification.</span><span class="sxs-lookup"><span data-stu-id="ade64-114">Some meeting APIs, such as `GetParticipant` will require a [bot registration and bot app ID](../bots/how-to/create-a-bot-for-teams.md#with-an-azure-subscription) to generate auth tokens.</span></span>

1. <span data-ttu-id="ade64-115">Les développeurs doivent respecter les [conseils généraux de conception des onglets teams](../tabs/design/tabs.md) pour les scénarios antérieurs et postérieurs à la réunion, ainsi que les [recommandations](design/designing-in-meeting-dialog.md) pour la boîte de dialogue de réunion déclenchée lors d’une réunion Teams.</span><span class="sxs-lookup"><span data-stu-id="ade64-115">Developers must adhere to general [Teams tab design guidelines](../tabs/design/tabs.md) for pre- and post-meeting scenarios as well as the [in-meeting dialog guidelines](design/designing-in-meeting-dialog.md) for in-meeting dialog triggered during a Teams meeting.</span></span>

## <a name="meeting-apps-api-reference"></a><span data-ttu-id="ade64-116">Référence de l’API des applications de réunion</span><span class="sxs-lookup"><span data-stu-id="ade64-116">Meeting apps API reference</span></span>

|<span data-ttu-id="ade64-117">API</span><span class="sxs-lookup"><span data-stu-id="ade64-117">API</span></span>|<span data-ttu-id="ade64-118">Description</span><span class="sxs-lookup"><span data-stu-id="ade64-118">Description</span></span>|<span data-ttu-id="ade64-119">Demande</span><span class="sxs-lookup"><span data-stu-id="ade64-119">Request</span></span>|<span data-ttu-id="ade64-120">Source</span><span class="sxs-lookup"><span data-stu-id="ade64-120">Source</span></span>|
|---|---|----|---|
|<span data-ttu-id="ade64-121">**GetUserContext**</span><span class="sxs-lookup"><span data-stu-id="ade64-121">**GetUserContext**</span></span>| <span data-ttu-id="ade64-122">Obtenir des informations contextuelles pour afficher le contenu pertinent dans un onglet Teams.</span><span class="sxs-lookup"><span data-stu-id="ade64-122">Get contextual information to display relevant content in a Teams tab.</span></span> |<span data-ttu-id="ade64-123">_**microsoftTeams. getContext (() => {/*...\* / } )*\*_</span><span class="sxs-lookup"><span data-stu-id="ade64-123">_**microsoftTeams.getContext( ( ) => {  /*...*/ } )**_</span></span>|<span data-ttu-id="ade64-124">Kit de développement logiciel client Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="ade64-124">Microsoft Teams client SDK</span></span>|
|<span data-ttu-id="ade64-125">**GetParticipant**</span><span class="sxs-lookup"><span data-stu-id="ade64-125">**GetParticipant**</span></span>|<span data-ttu-id="ade64-126">Cette API permet à un bot d’extraire des informations sur les participants par ID de réunion et ID de participant.</span><span class="sxs-lookup"><span data-stu-id="ade64-126">This API allows a bot to fetch a participant information by meeting id and participant id.</span></span>|<span data-ttu-id="ade64-127">**Obtenir** _ **/v1/meetings/{meetingId}/participants/{participantId} ? tenantId = {tenantId}**_</span><span class="sxs-lookup"><span data-stu-id="ade64-127">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span></span> |<span data-ttu-id="ade64-128">Kit de développement logiciel (SDK) Microsoft bot Framework</span><span class="sxs-lookup"><span data-stu-id="ade64-128">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="ade64-129">**NotificationSignal**</span><span class="sxs-lookup"><span data-stu-id="ade64-129">**NotificationSignal**</span></span> |<span data-ttu-id="ade64-130">Les signaux de réunion seront remis à l’aide de l’API de notification de conversation existante suivante (pour la conversation utilisateur-bot).</span><span class="sxs-lookup"><span data-stu-id="ade64-130">Meeting signals will be delivered using the following existing conversation notification API (for user-bot chat).</span></span> <span data-ttu-id="ade64-131">Cette API permet aux développeurs de signaler en fonction de l’action de l’utilisateur final à afficher-case une bulle de dialogue de réunion.</span><span class="sxs-lookup"><span data-stu-id="ade64-131">This API allows developers to signal based on end-user action to show-case an in-meeting dialog bubble.</span></span>|<span data-ttu-id="ade64-132">**Post** _ **/v3/conversations/{conversationId}/Activities**_</span><span class="sxs-lookup"><span data-stu-id="ade64-132">**POST** _**/v3/conversations/{conversationId}/activities**_</span></span>|<span data-ttu-id="ade64-133">Kit de développement logiciel (SDK) Microsoft bot Framework</span><span class="sxs-lookup"><span data-stu-id="ade64-133">Microsoft Bot Framework SDK</span></span>|

### <a name="getusercontext"></a><span data-ttu-id="ade64-134">GetUserContext</span><span class="sxs-lookup"><span data-stu-id="ade64-134">GetUserContext</span></span>

<span data-ttu-id="ade64-135">Pour obtenir des instructions sur l’identification et la récupération des informations contextuelles pour votre contenu d’onglet, consultez notre [contexte de l’onglet teams](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) .</span><span class="sxs-lookup"><span data-stu-id="ade64-135">Please refer to our [Get context for your Teams tab](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) documentation for guidance on identifying and  retrieving contextual information for your tab content.</span></span> <span data-ttu-id="ade64-136">Dans le cadre de l’extensibilité des réunions, une nouvelle valeur a été ajoutée pour la charge utile de la réponse :</span><span class="sxs-lookup"><span data-stu-id="ade64-136">As part of meetings extensibility, a new value has been added for the response payload:</span></span>

<span data-ttu-id="ade64-137">✔ **meetingId**: utilisé par un onglet lors de l’exécution dans le contexte de la réunion.</span><span class="sxs-lookup"><span data-stu-id="ade64-137">✔ **meetingId**: used by a tab when running in the meeting context.</span></span>

### <a name="getparticipant-api"></a><span data-ttu-id="ade64-138">API GetParticipant</span><span class="sxs-lookup"><span data-stu-id="ade64-138">GetParticipant API</span></span>

> [!NOTE]
>
> * <span data-ttu-id="ade64-139">Ne pas mettre en cache les rôles des participants étant donné que l’organisateur de la réunion peut modifier un rôle à tout moment.</span><span class="sxs-lookup"><span data-stu-id="ade64-139">Do not cache participant roles since the meeting organizer can change a role at any point in time.</span></span>
>
> * <span data-ttu-id="ade64-140">Teams ne prend actuellement pas en charge les listes de distribution volumineuses ni les tailles de liste de plus de 350 participants pour l' `GetParticipant` API.</span><span class="sxs-lookup"><span data-stu-id="ade64-140">Teams does not currently support large distribution lists or roster sizes of more than 350 participants for the `GetParticipant` API.</span></span>
>
> * <span data-ttu-id="ade64-141">La prise en charge du kit de développement logiciel (SDK) de robot sera bientôt disponible.</span><span class="sxs-lookup"><span data-stu-id="ade64-141">Support for the Bot Framework SDK is coming soon.</span></span>

#### <a name="request"></a><span data-ttu-id="ade64-142">Demande</span><span class="sxs-lookup"><span data-stu-id="ade64-142">Request</span></span>

```http
GET /v3/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

<span data-ttu-id="ade64-143">*Voir* la référence de l’API de l' [infrastructure bot](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="ade64-143">*See* the [Bot Framework API reference](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<!-- markdownlint-disable MD025 -->

<span data-ttu-id="ade64-144">**Exemple C#**</span><span class="sxs-lookup"><span data-stu-id="ade64-144">**C# Example**</span></span>

```csharp
string meetingId = "meetingid?";
string participantId = "participantidhere";
var connectorClient = turnContext.TurnState.Get<IConnectorClient>();
var creds = connectorClient.Credentials as AppCredentials;
var bearerToken = await creds.GetTokenAsync().ConfigureAwait(false);
var request = new HttpRequestMessage();
request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", bearerToken);
request.Method = new HttpMethod("GET");
request.RequestUri = new System.Uri(Path.Combine(connectorClient.BaseUri.OriginalString, $"/meetings/{meetingId}/participants/{participantId}"));
HttpResponseMessage response = await (connectorClient as ServiceClient<ConnectorClient>).HttpClient.SendAsync(request, cancellationToken).ConfigureAwait(false);
if (response.StatusCode == System.Net.HttpStatusCode.OK)
{
    var content = await response.Content.ReadAsStringAsync().ConfigureAwait(false);
    var theObject = Rest.Serialization.SafeJsonConvert.DeserializeObject<WhateverObjectIsReturned>(content, connectorClient.DeserializationSettings);
}
```

* * *
<!-- markdownlint-disable MD001 -->

#### <a name="query-parameters"></a><span data-ttu-id="ade64-145">Paramètres de requête</span><span class="sxs-lookup"><span data-stu-id="ade64-145">Query parameters</span></span>

|<span data-ttu-id="ade64-146">Valeur</span><span class="sxs-lookup"><span data-stu-id="ade64-146">Value</span></span>|<span data-ttu-id="ade64-147">Type</span><span class="sxs-lookup"><span data-stu-id="ade64-147">Type</span></span>|<span data-ttu-id="ade64-148">Requis</span><span class="sxs-lookup"><span data-stu-id="ade64-148">Required</span></span>|<span data-ttu-id="ade64-149">Description</span><span class="sxs-lookup"><span data-stu-id="ade64-149">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="ade64-150">**meetingId**</span><span class="sxs-lookup"><span data-stu-id="ade64-150">**meetingId**</span></span>| <span data-ttu-id="ade64-151">string</span><span class="sxs-lookup"><span data-stu-id="ade64-151">string</span></span> | <span data-ttu-id="ade64-152">Oui</span><span class="sxs-lookup"><span data-stu-id="ade64-152">Yes</span></span> | <span data-ttu-id="ade64-153">L’identificateur de réunion est disponible via le kit de développement logiciel (SDK) et teams Client SDK.</span><span class="sxs-lookup"><span data-stu-id="ade64-153">The meeting identifier is available via Bot Invoke and Teams Client SDK.</span></span>|
|<span data-ttu-id="ade64-154">**participantId**</span><span class="sxs-lookup"><span data-stu-id="ade64-154">**participantId**</span></span>| <span data-ttu-id="ade64-155">string</span><span class="sxs-lookup"><span data-stu-id="ade64-155">string</span></span> | <span data-ttu-id="ade64-156">Oui</span><span class="sxs-lookup"><span data-stu-id="ade64-156">Yes</span></span> | <span data-ttu-id="ade64-157">Ce champ est le nom d’utilisateur et est disponible dans les onglets SSO, d’appel de bot et teams Client SDK.</span><span class="sxs-lookup"><span data-stu-id="ade64-157">This field is the User ID and it is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="ade64-158">L’authentification unique de l’onglet est fortement recommandée</span><span class="sxs-lookup"><span data-stu-id="ade64-158">Tab SSO is highly recommended</span></span>|
|<span data-ttu-id="ade64-159">**tenantId**</span><span class="sxs-lookup"><span data-stu-id="ade64-159">**tenantId**</span></span>| <span data-ttu-id="ade64-160">string</span><span class="sxs-lookup"><span data-stu-id="ade64-160">string</span></span> | <span data-ttu-id="ade64-161">Oui</span><span class="sxs-lookup"><span data-stu-id="ade64-161">Yes</span></span> | <span data-ttu-id="ade64-162">Cela est nécessaire pour les utilisateurs clients.</span><span class="sxs-lookup"><span data-stu-id="ade64-162">This required for tenant users.</span></span> <span data-ttu-id="ade64-163">Elle est disponible dans les kits de développement logiciel SSO, de robot et teams client.</span><span class="sxs-lookup"><span data-stu-id="ade64-163">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="ade64-164">L’authentification unique de l’onglet est fortement recommandée</span><span class="sxs-lookup"><span data-stu-id="ade64-164">Tab SSO is highly recommended</span></span>|

#### <a name="response-payload"></a><span data-ttu-id="ade64-165">Charge utile de réponse</span><span class="sxs-lookup"><span data-stu-id="ade64-165">Response Payload</span></span>
<!-- markdownlint-disable MD036 -->

<span data-ttu-id="ade64-166">**meetingRole** peut être *organisateur*, *présentateur*ou *participant*.</span><span class="sxs-lookup"><span data-stu-id="ade64-166">**meetingRole** can be *Organizer*, *Presenter*, or *Attendee*.</span></span>

<span data-ttu-id="ade64-167">**Exemple 1**</span><span class="sxs-lookup"><span data-stu-id="ade64-167">**Example 1**</span></span>

```json
{
  "user":
  {
      "id": "29:1JKiJGPAX9TTxtGxhVo0wLx_zwzo-gG8Z-X03306vBwi9p-xMTEbDXsT6KH7-0kkTS8cD-2zkrsoV6f5WJ6_aYw",
      "aadObjectId": "6aebbad0-e5a5-424a-834a-20fb051f3c1a",
      "name": "Allan Deyoung",
      "givenName": "Allan",
      "surname": "Deyoung",
      "email": "Allan.Deyoung@microsoft.com",
      "userPrincipalName": "Allan.Deyoung@microsoft.com",
      "tenantId": "72f988bf-86f1-41af-91ab-2d7cd011db47",
  },
  "meeting":
  {
      "role ": "Presenter",
      "inMeeting":true
  },
  "conversation":
  {
      "id": "<conversation id>"
  }
}
```
#### <a name="response-codes"></a><span data-ttu-id="ade64-168">Codes de réponse</span><span class="sxs-lookup"><span data-stu-id="ade64-168">Response Codes</span></span>

<span data-ttu-id="ade64-169">**403**: l’application n’est pas autorisée à obtenir des informations sur les participants.</span><span class="sxs-lookup"><span data-stu-id="ade64-169">**403**: the app is not allowed to get participant information.</span></span> <span data-ttu-id="ade64-170">Il s’agit de la réponse d’erreur la plus courante, qui est déclenchée lorsque l’application n’est pas installée dans la réunion, par exemple lorsque l’application est désactivée par l’administrateur client ou bloquée lors de l’atténuation du site actif.</span><span class="sxs-lookup"><span data-stu-id="ade64-170">This will be the most common error response and is triggered when the app is not installed in the meeting such as when the app is disabled by tenant admin or blocked during live site mitigation.</span></span>  
<span data-ttu-id="ade64-171">**200**: informations sur les participants récupérées avec succès</span><span class="sxs-lookup"><span data-stu-id="ade64-171">**200**: participant information successfully retrieved</span></span>  
<span data-ttu-id="ade64-172">**401**: jeton non valide</span><span class="sxs-lookup"><span data-stu-id="ade64-172">**401**: invalid token</span></span>  
<span data-ttu-id="ade64-173">**404**: la réunion n’existe pas ou le participant est introuvable.</span><span class="sxs-lookup"><span data-stu-id="ade64-173">**404**: the meeting doesn't exist or participant can’t be found.</span></span>

<!-- markdownlint-disable MD024 -->
### <a name="notificationsignal-api"></a><span data-ttu-id="ade64-174">API NotificationSignal</span><span class="sxs-lookup"><span data-stu-id="ade64-174">NotificationSignal API</span></span>

> [!NOTE]
> <span data-ttu-id="ade64-175">Lorsqu’une boîte de dialogue de réunion est appelée, le même contenu s’affiche également sous la forme d’un message de conversation.</span><span class="sxs-lookup"><span data-stu-id="ade64-175">When an in-meeting dialog is invoked, the same content will also be presented as a chat message.</span></span>

#### <a name="request"></a><span data-ttu-id="ade64-176">Demande</span><span class="sxs-lookup"><span data-stu-id="ade64-176">Request</span></span>

```http
POST /v3/conversations/{conversationId}/activities
```

#### <a name="query-parameters"></a><span data-ttu-id="ade64-177">Paramètres de requête</span><span class="sxs-lookup"><span data-stu-id="ade64-177">Query parameters</span></span>

|<span data-ttu-id="ade64-178">Valeur</span><span class="sxs-lookup"><span data-stu-id="ade64-178">Value</span></span>|<span data-ttu-id="ade64-179">Type</span><span class="sxs-lookup"><span data-stu-id="ade64-179">Type</span></span>|<span data-ttu-id="ade64-180">Requis</span><span class="sxs-lookup"><span data-stu-id="ade64-180">Required</span></span>|<span data-ttu-id="ade64-181">Description</span><span class="sxs-lookup"><span data-stu-id="ade64-181">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="ade64-182">**conversationId**</span><span class="sxs-lookup"><span data-stu-id="ade64-182">**conversationId**</span></span>| <span data-ttu-id="ade64-183">string</span><span class="sxs-lookup"><span data-stu-id="ade64-183">string</span></span> | <span data-ttu-id="ade64-184">Oui</span><span class="sxs-lookup"><span data-stu-id="ade64-184">Yes</span></span> | <span data-ttu-id="ade64-185">L’identificateur convdersation est disponible dans le cadre de l’appel de bot.</span><span class="sxs-lookup"><span data-stu-id="ade64-185">The convdersation identifier is available as part of bot invoke</span></span> |
|<span data-ttu-id="ade64-186">**completionBotId**</span><span class="sxs-lookup"><span data-stu-id="ade64-186">**completionBotId**</span></span>| <span data-ttu-id="ade64-187">string</span><span class="sxs-lookup"><span data-stu-id="ade64-187">string</span></span> | <span data-ttu-id="ade64-188">Non</span><span class="sxs-lookup"><span data-stu-id="ade64-188">No</span></span> | <span data-ttu-id="ade64-189">Ce champ est l’ID du bot déclaré dans le manifeste.</span><span class="sxs-lookup"><span data-stu-id="ade64-189">This field is the Bot ID that is declared in the manifest.</span></span> <span data-ttu-id="ade64-190">Le bot reçoit un objet de résultat.</span><span class="sxs-lookup"><span data-stu-id="ade64-190">The bot will receive a result object</span></span> |

#### <a name="request-payload"></a><span data-ttu-id="ade64-191">Charge utile de la demande</span><span class="sxs-lookup"><span data-stu-id="ade64-191">Request Payload</span></span>

# <a name="json"></a>[<span data-ttu-id="ade64-192">JSON</span><span class="sxs-lookup"><span data-stu-id="ade64-192">JSON</span></span>](#tab/json)

```json
{
    "type": "message",
    "text": "John Phillips assigned you a weekly todo",
    "summary": "Don't forget to meet with Marketing next week",
    "channelData": {
        "notification": {
            "alertInMeeting": true,
            "externalResourceUrl": "https://teams.microsoft.com/l/bubble/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID"
        }
    },
    "replyToId": "1493070356924"
}
```

# <a name="cnet"></a>[<span data-ttu-id="ade64-193">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="ade64-193">C#/.NET</span></span>](#tab/dotnet)

```csharp
Activity activity = MessageFactory.Text("This is a meeting signal test");
MeetingNotification notification = new MeetingNotification
  {
    AlertInMeeting = true,
    ExternalResourceUrl = "https://teams.microsoft.com/l/bubble/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID"
  };
activity.ChannelData = new TeamsChannelData
  {
    Notification = notification
  };
await turnContext.SendActivityAsync(activity).ConfigureAwait(false);
```

# <a name="javascript"></a>[<span data-ttu-id="ade64-194">JavaScript</span><span class="sxs-lookup"><span data-stu-id="ade64-194">JavaScript</span></span>](#tab/javascript)

```javascript

const replyActivity = MessageFactory.text('Hi'); // this could be an adaptive card instead
replyActivity.channelData = {
    notification: {
        alertInMeeting: true,
        externalResourceUrl: 'https://teams.microsoft.com/l/bubble/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID’
    }
};
await context.sendActivity(replyActivity);
```

* * *

> [!IMPORTANT]
> <span data-ttu-id="ade64-195">L’URL dans la bulle de contenu (URL de taskInfo) doit être incluse dans la liste des [domaines valide](../resources/schema/manifest-schema.md#validdomains) incluse dans le manifeste de l’application Teams.</span><span class="sxs-lookup"><span data-stu-id="ade64-195">The URL in the content bubble (taskInfo URL) must be included in the [valid domains](../resources/schema/manifest-schema.md#validdomains) list included in the Teams app manifest.</span></span>

#### <a name="response-codes"></a><span data-ttu-id="ade64-196">Codes de réponse</span><span class="sxs-lookup"><span data-stu-id="ade64-196">Response Codes</span></span>

<span data-ttu-id="ade64-197">**201**: l’activité avec le signal est correctement envoyée</span><span class="sxs-lookup"><span data-stu-id="ade64-197">**201**: activity with signal is successfully sent</span></span>  
<span data-ttu-id="ade64-198">**401**: jeton non valide</span><span class="sxs-lookup"><span data-stu-id="ade64-198">**401**: invalid token</span></span>  
<span data-ttu-id="ade64-199">**403**: l’application n’est pas autorisée à envoyer le signal.</span><span class="sxs-lookup"><span data-stu-id="ade64-199">**403**: the app is not allowed to send the signal.</span></span> <span data-ttu-id="ade64-200">Dans ce cas, la charge utile doit contenir plus de détails sur les messages d’erreur.</span><span class="sxs-lookup"><span data-stu-id="ade64-200">In this case, the payload should contain more detail error message.</span></span> <span data-ttu-id="ade64-201">Il peut y avoir plusieurs raisons : l’application est désactivée par l’administrateur client, bloquée lors de la limitation du site actif, etc.</span><span class="sxs-lookup"><span data-stu-id="ade64-201">There can be many reasons: app disabled by tenant admin, blocked during live site mitigation, etc.</span></span>  
<span data-ttu-id="ade64-202">**404**: la conversation de réunion n’existe pas</span><span class="sxs-lookup"><span data-stu-id="ade64-202">**404**: meeting chat doesn't exist</span></span>  

## <a name="enable-your-app-for-teams-meetings"></a><span data-ttu-id="ade64-203">Activer votre application pour les réunions teams</span><span class="sxs-lookup"><span data-stu-id="ade64-203">Enable your app for Teams meetings</span></span>

### <a name="update-your-app-manifest"></a><span data-ttu-id="ade64-204">Mettre à jour le manifeste de votre application</span><span class="sxs-lookup"><span data-stu-id="ade64-204">Update your app manifest</span></span>

<span data-ttu-id="ade64-205">Les fonctionnalités des applications de réunion sont déclarées dans le manifeste **configurableTabs**de votre application via les  ->  **étendues** configurableTabs et les tableaux de **contexte** .</span><span class="sxs-lookup"><span data-stu-id="ade64-205">The meetings app capabilities are declared in your app manifest via the **configurableTabs** -> **scopes** and **context** arrays.</span></span> <span data-ttu-id="ade64-206">L' *étendue* définit la personne et le *contexte* définissant où votre application sera disponible.</span><span class="sxs-lookup"><span data-stu-id="ade64-206">*Scope* defines to whom and *context* defines where your app will be available.</span></span>

> [!NOTE]
> * <span data-ttu-id="ade64-207">Veuillez utiliser le [schéma de manifeste d’aperçu développeur](../resources/schema/manifest-schema-dev-preview.md) pour essayer cela dans le manifeste de votre application.</span><span class="sxs-lookup"><span data-stu-id="ade64-207">Please use [Developer Preview manifest schema](../resources/schema/manifest-schema-dev-preview.md) to try this in your app manifest.</span></span>
> * <span data-ttu-id="ade64-208">La plateforme mobile ne prend actuellement en charge que le schéma de manifeste 1,6</span><span class="sxs-lookup"><span data-stu-id="ade64-208">Mobile Platform currently only support Manifest Schema 1.6</span></span>
> * <span data-ttu-id="ade64-209">La plateforme mobile prend en charge les onglets uniquement dans les surfaces pre et post Meeting.</span><span class="sxs-lookup"><span data-stu-id="ade64-209">Mobile Platform supports Tabs only in Pre and Post Meeting Surfaces.</span></span> <span data-ttu-id="ade64-210">Les expériences de réunion (boîte de dialogue et onglet de réunion) sur mobile seront bientôt disponibles.</span><span class="sxs-lookup"><span data-stu-id="ade64-210">The In-meeting experiences (in-meeting dialog and tab) on mobile will be available soon</span></span>

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

### <a name="context-property"></a><span data-ttu-id="ade64-211">Context, propriété</span><span class="sxs-lookup"><span data-stu-id="ade64-211">Context property</span></span>

<span data-ttu-id="ade64-212">L’onglet `context` et les `scopes` propriétés fonctionnent en harmonie pour vous permettre de déterminer où vous souhaitez que votre application apparaisse.</span><span class="sxs-lookup"><span data-stu-id="ade64-212">The tab `context` and `scopes` properties work in harmony to allow you to determine where you want your app to appear.</span></span> <span data-ttu-id="ade64-213">Les onglets de l' `team` `groupchat` étendue ou peuvent avoir plusieurs contextes.</span><span class="sxs-lookup"><span data-stu-id="ade64-213">Tabs in the `team` or `groupchat` scope can have more than one context.</span></span> <span data-ttu-id="ade64-214">Les valeurs possibles pour la propriété Context sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="ade64-214">The possible values for the context property are as follows:</span></span>

* <span data-ttu-id="ade64-215">**channelTab**: onglet de l’en-tête d’un canal d’équipe.</span><span class="sxs-lookup"><span data-stu-id="ade64-215">**channelTab**: a tab in the header of a team channel.</span></span>
* <span data-ttu-id="ade64-216">**privateChatTab**: onglet de l’en-tête d’une conversation de groupe entre un ensemble d’utilisateurs qui n’est pas dans le contexte d’une équipe ou d’une réunion.</span><span class="sxs-lookup"><span data-stu-id="ade64-216">**privateChatTab**: a tab in the header of a group chat between a set of users not in the context of a team or meeting.</span></span>
* <span data-ttu-id="ade64-217">**meetingChatTab**: onglet de l’en-tête d’une conversation de groupe entre un ensemble d’utilisateurs dans le contexte d’une réunion planifiée.</span><span class="sxs-lookup"><span data-stu-id="ade64-217">**meetingChatTab**: a tab in the header of a group chat between a set of users in the context of a scheduled meeting.</span></span>
* <span data-ttu-id="ade64-218">**meetingDetailsTab**: onglet de l’en-tête de l’affichage Détails de la réunion du calendrier.</span><span class="sxs-lookup"><span data-stu-id="ade64-218">**meetingDetailsTab**: a tab in the header of the meeting details view of the calendar.</span></span>
* <span data-ttu-id="ade64-219">**meetingSidePanel**: un panneau de réunion ouvert par le biais de la barre unifiée (u-bar).</span><span class="sxs-lookup"><span data-stu-id="ade64-219">**meetingSidePanel**: an in-meeting panel opened via the unified bar (u-bar).</span></span>

## <a name="configure-your-app-for-meeting-scenarios"></a><span data-ttu-id="ade64-220">Configurer votre application pour les scénarios de réunion</span><span class="sxs-lookup"><span data-stu-id="ade64-220">Configure your app for meeting scenarios</span></span>

> [!NOTE]
> <span data-ttu-id="ade64-221">Pour que votre application soit visible dans la Galerie d’onglets, elle doit **prendre en charge les onglets configurables** et l' **étendue de conversation de groupe**.</span><span class="sxs-lookup"><span data-stu-id="ade64-221">For your app to be visible in the tab gallery it needs to **support configurable tabs** and the **group chat scope**.</span></span>

### <a name="pre-meeting"></a><span data-ttu-id="ade64-222">Pré-réunion</span><span class="sxs-lookup"><span data-stu-id="ade64-222">Pre-meeting</span></span>

<span data-ttu-id="ade64-223">Les utilisateurs disposant de rôles d’organisateur et/ou de présentateur ajoutent des onglets à une réunion en utilisant le bouton plus ➕ dans les pages **conversation** de réunion et **Détails** de la réunion.</span><span class="sxs-lookup"><span data-stu-id="ade64-223">Users with organizer and/or presenter roles add tabs to a meeting using the plus ➕ button in the meeting **Chat** and meeting **details** pages.</span></span> <span data-ttu-id="ade64-224">Les extensions de messagerie sont ajoutées à via le menu ellipses/Overflow &#x25CF;&#x25CF;&#x25CF; située sous la zone de message composer dans la conversation.</span><span class="sxs-lookup"><span data-stu-id="ade64-224">Messaging extensions are added to via the ellipses/overflow menu &#x25CF;&#x25CF;&#x25CF; located beneath the compose message area in the chat.</span></span> <span data-ttu-id="ade64-225">Les robots sont ajoutés à une conversation de réunion à l’aide de la **@** touche «» et en sélectionnant **obtenir les bots**.</span><span class="sxs-lookup"><span data-stu-id="ade64-225">Bots are added to a meeting chat using the "**@**" key and selecting **Get bots**.</span></span>

<span data-ttu-id="ade64-226">✔ L’identité de l’utilisateur *doit* être confirmée via les [onglets SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span><span class="sxs-lookup"><span data-stu-id="ade64-226">✔ The user identity *must* be confirmed via [Tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="ade64-227">À la suite de cette authentification, l’application peut récupérer le rôle d’utilisateur via l’API GetParticipant.</span><span class="sxs-lookup"><span data-stu-id="ade64-227">Following this authentication, the app can retrieve the user role via the GetParticipant API.</span></span>

 <span data-ttu-id="ade64-228">✔ En fonction du rôle d’utilisateur, l’application est désormais capable de présenter des expériences spécifiques de rôle.</span><span class="sxs-lookup"><span data-stu-id="ade64-228">✔ Based on the user role, the app will now have the capability to present role specific experiences.</span></span> <span data-ttu-id="ade64-229">Par exemple, une application d’interrogation peut autoriser uniquement les organisateurs et les présentateurs à créer une nouvelle interrogation.</span><span class="sxs-lookup"><span data-stu-id="ade64-229">For example, a polling app can allow only organizers and presenters to create a new poll.</span></span>

> <span data-ttu-id="ade64-230">**Remarque**: les attributions de rôles peuvent être modifiées lorsqu’une réunion est en cours.</span><span class="sxs-lookup"><span data-stu-id="ade64-230">**NOTE**: Role assignments can be changed while a meeting is in progress.</span></span>  <span data-ttu-id="ade64-231">*Voir* [rôles dans une réunion teams](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span><span class="sxs-lookup"><span data-stu-id="ade64-231">*See* [Roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span> 

### <a name="in-meeting"></a><span data-ttu-id="ade64-232">Réunion</span><span class="sxs-lookup"><span data-stu-id="ade64-232">In-meeting</span></span>

#### <a name="sidepanel"></a><span data-ttu-id="ade64-233">**sidePanel**</span><span class="sxs-lookup"><span data-stu-id="ade64-233">**sidePanel**</span></span>

<span data-ttu-id="ade64-234">✔ Dans votre manifeste d’application, ajoutez **sidePanel** au tableau de **contexte** , comme décrit ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="ade64-234">✔ In your app manifest add **sidePanel** to the **context** array as described above.</span></span>

<span data-ttu-id="ade64-235">✔ Dans la réunion, ainsi que dans tous les scénarios, l’application sera affichée sous la forme d’un onglet dans la réunion 320 px.</span><span class="sxs-lookup"><span data-stu-id="ade64-235">✔ In the meeting as well as in all scenarios, the app will be rendered in an in-meeting tab that is 320px in width.</span></span> <span data-ttu-id="ade64-236">Pour ce faire, vous devez optimiser l’onglet.</span><span class="sxs-lookup"><span data-stu-id="ade64-236">Your tab must be optimized for this.</span></span> <span data-ttu-id="ade64-237">*Voir*, [interface FrameContext](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="ade64-237">*See*, [FrameContext interface](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true)</span></span>

<span data-ttu-id="ade64-238">✔ Reportez-vous au [Kit de développement logiciel teams](../tabs/how-to/access-teams-context.md#user-context) pour utiliser l’API **userContext** pour acheminer les demandes en conséquence.</span><span class="sxs-lookup"><span data-stu-id="ade64-238">✔Refer to the [Teams SDK](../tabs/how-to/access-teams-context.md#user-context) to use the **userContext** API to route requests accordingly.</span></span>

<span data-ttu-id="ade64-239">✔ Reportez-vous au [flux d’authentification teams pour les onglets](../tabs/how-to/authentication/auth-flow-tab.md).</span><span class="sxs-lookup"><span data-stu-id="ade64-239">✔ Refer to the [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span> <span data-ttu-id="ade64-240">Le flux d’authentification des onglets est très similaire au flux d’authentification pour les sites Web.</span><span class="sxs-lookup"><span data-stu-id="ade64-240">Authentication flow for tabs is very similar to the auth flow for websites.</span></span> <span data-ttu-id="ade64-241">Par conséquent, les onglets peuvent utiliser OAuth 2,0 directement.</span><span class="sxs-lookup"><span data-stu-id="ade64-241">Thus, tabs can use OAuth 2.0 directly.</span></span> <span data-ttu-id="ade64-242">*Voir aussi*la [plateforme d’identité Microsoft et le flux de code d’autorisation OAuth 2,0](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span><span class="sxs-lookup"><span data-stu-id="ade64-242">*See also*, [Microsoft identity platform and OAuth 2.0 authorization code flow](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span></span>

#### <a name="in-meeting-dialog"></a><span data-ttu-id="ade64-243">**boîte de dialogue de réunion**</span><span class="sxs-lookup"><span data-stu-id="ade64-243">**in-meeting dialog**</span></span>

<span data-ttu-id="ade64-244">✔ Vous devez respecter les [instructions de conception de la boîte de dialogue de réunion](design/designing-in-meeting-dialog.md).</span><span class="sxs-lookup"><span data-stu-id="ade64-244">✔ You must adhere to the [in-meeting dialog design guidelines](design/designing-in-meeting-dialog.md).</span></span>

<span data-ttu-id="ade64-245">✔ Reportez-vous au [flux d’authentification teams pour les onglets](../tabs/how-to/authentication/auth-flow-tab.md).</span><span class="sxs-lookup"><span data-stu-id="ade64-245">✔ Refer to the [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span>

<span data-ttu-id="ade64-246">✔ Utiliser l’API de [notification](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) pour signaler qu’une notification de bulle doit être déclenchée.</span><span class="sxs-lookup"><span data-stu-id="ade64-246">✔ Use the [notification](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) API to signal that a bubble notification needs to be triggered.</span></span>

<span data-ttu-id="ade64-247">✔ Dans le cadre de la charge utile de la demande de notification, incluez l’URL où le contenu à présenter est hébergé.</span><span class="sxs-lookup"><span data-stu-id="ade64-247">✔ As part of the notification request payload, include the URL where the content to be showcased is hosted.</span></span>

> [!NOTE]
>
> * <span data-ttu-id="ade64-248">Ces notifications sont permanentes.</span><span class="sxs-lookup"><span data-stu-id="ade64-248">These notifications are persistent in nature.</span></span> <span data-ttu-id="ade64-249">Vous devez appeler la fonction [**submitTask ()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) pour faire une fermeture automatique après qu’un utilisateur a effectué une action dans l’affichage Web.</span><span class="sxs-lookup"><span data-stu-id="ade64-249">You must invoke the [**submitTask()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) function to auto-dismiss after a user takes an action in the web-view.</span></span> <span data-ttu-id="ade64-250">Il s’agit d’une condition requise pour l’envoi d’une application.</span><span class="sxs-lookup"><span data-stu-id="ade64-250">This is a requirement for app submission.</span></span> <span data-ttu-id="ade64-251">*Voir aussi*, [Kit de développement logiciel (SDK) teams : module de tâches](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="ade64-251">*See also*, [Teams SDK: task module](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span></span>
>
> * <span data-ttu-id="ade64-252">Si vous souhaitez que votre application prenne en charge les utilisateurs anonymes, votre charge utile de la demande d’appel initiale doit reposer sur les métadonnées de demande `from.id`  (ID de l’utilisateur) dans l' `from` objet, et non sur l' `from.aadObjectId` ID (Azure Active Directory ID de l’utilisateur).</span><span class="sxs-lookup"><span data-stu-id="ade64-252">If you want your app to support anonymous users, your initial invoke request payload must rely on the `from.id`  (ID of the user) request metadata in the `from` object, not the `from.aadObjectId` (Azure Active Directory ID of the user) request metadata.</span></span> <span data-ttu-id="ade64-253">*Voir* [utilisation des modules de tâches dans les onglets](../task-modules-and-cards/task-modules/task-modules-tabs.md) et [créer et envoyer le module de tâches](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).</span><span class="sxs-lookup"><span data-stu-id="ade64-253">*See* [Using task modules in tabs](../task-modules-and-cards/task-modules/task-modules-tabs.md) and [Create and send the task module](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).</span></span>

### <a name="post-meeting"></a><span data-ttu-id="ade64-254">Post-réunion</span><span class="sxs-lookup"><span data-stu-id="ade64-254">Post-meeting</span></span>

<span data-ttu-id="ade64-255">Les configurations post-réunion et de réunion sont équivalentes.</span><span class="sxs-lookup"><span data-stu-id="ade64-255">The post-meeting and pre-meeting configurations are equivalent.</span></span>

## <a name="meeting-app-sample"></a><span data-ttu-id="ade64-256">Exemple d’application de réunion</span><span class="sxs-lookup"><span data-stu-id="ade64-256">Meeting app sample</span></span>

 > [!div class="nextstepaction"]
> [<span data-ttu-id="ade64-257">Application du générateur de jetons de réunion</span><span class="sxs-lookup"><span data-stu-id="ade64-257">Meeting token generator app</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token)
