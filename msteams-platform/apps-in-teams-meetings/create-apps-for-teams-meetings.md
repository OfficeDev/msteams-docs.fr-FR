---
title: Conditions préalables et références d’API pour les applications dans les réunions Teams
author: surbhigupta
description: Travailler avec des applications pour Teams réunions
ms.topic: conceptual
ms.author: lajanuar
localization_priority: Normal
keywords: Api de rôle d’utilisateur participant aux réunions teams apps
ms.openlocfilehash: 38a7a5fdf9794fb95b4141f2c73e8282a9bf8601
ms.sourcegitcommit: 059d22c436ee9b07a61561ff71e03e1c23ff40b8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/30/2021
ms.locfileid: "53211589"
---
# <a name="prerequisites-and-api-references-for-apps-in-teams-meetings"></a><span data-ttu-id="92d1c-104">Conditions préalables et références d’API pour les applications dans les réunions Teams</span><span class="sxs-lookup"><span data-stu-id="92d1c-104">Prerequisites and API references for apps in Teams meetings</span></span>

<span data-ttu-id="92d1c-105">Pour développer les fonctionnalités de vos applications tout au long du cycle de vie des réunions, Teams vous permet de travailler avec des applications pour Teams réunions.</span><span class="sxs-lookup"><span data-stu-id="92d1c-105">To expand the capabilities of your apps across the meeting lifecycle, Teams enables you to work with apps for Teams meetings.</span></span> <span data-ttu-id="92d1c-106">Vous devez respecter les conditions préalables et utiliser les références de l’API des applications de réunion pour améliorer l’expérience de réunion.</span><span class="sxs-lookup"><span data-stu-id="92d1c-106">You must  go through the prerequisites and you can use the meeting apps API references to enhance the meeting experience.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="92d1c-107">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="92d1c-107">Prerequisites</span></span>

<span data-ttu-id="92d1c-108">Avant de travailler avec des applications pour Teams réunions, vous devez comprendre les choses suivantes :</span><span class="sxs-lookup"><span data-stu-id="92d1c-108">Before you work with apps for Teams meetings, you must have an understanding of the following:</span></span>

* <span data-ttu-id="92d1c-109">Vous devez savoir comment développer des Teams applications.</span><span class="sxs-lookup"><span data-stu-id="92d1c-109">You must have knowledge of how to develop Teams apps.</span></span> <span data-ttu-id="92d1c-110">Pour plus d’informations, [voir Teams développement d’applications.](../overview.md)</span><span class="sxs-lookup"><span data-stu-id="92d1c-110">For more information, see [Teams app development](../overview.md).</span></span>

* <span data-ttu-id="92d1c-111">Vous devez mettre à jour Teams manifeste de l’application pour indiquer que l’application est disponible pour les réunions.</span><span class="sxs-lookup"><span data-stu-id="92d1c-111">You must update the Teams app manifest to indicate that the app is available for meetings.</span></span> <span data-ttu-id="92d1c-112">Pour plus d’informations, voir [le manifeste de l’application.](enable-and-configure-your-app-for-teams-meetings.md#update-your-app-manifest)</span><span class="sxs-lookup"><span data-stu-id="92d1c-112">For more information, see [app manifest](enable-and-configure-your-app-for-teams-meetings.md#update-your-app-manifest).</span></span>

* <span data-ttu-id="92d1c-113">Votre application doit prendre en charge les onglets configurables dans l’étendue groupchat, pour que votre application fonctionne dans le cycle de vie de la réunion sous la mesure d’un onglet. Pour plus d’informations, voir [étendue groupchat](../resources/schema/manifest-schema.md#configurabletabs) et [créer un onglet de groupe.](../build-your-first-app/build-channel-tab.md)</span><span class="sxs-lookup"><span data-stu-id="92d1c-113">Your app must support configurable tabs in the groupchat scope, for your app to function in the meeting lifecycle as a tab. For more information, see [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs) and [build a group tab](../build-your-first-app/build-channel-tab.md).</span></span>

* <span data-ttu-id="92d1c-114">Vous devez respecter les recommandations générales Teams la conception d’onglets pour les scénarios préalables et post-réunion.</span><span class="sxs-lookup"><span data-stu-id="92d1c-114">You must adhere to general Teams tab design guidelines for pre and post-meeting scenarios.</span></span> <span data-ttu-id="92d1c-115">Pour les expériences pendant les réunions, reportez-vous aux instructions de conception de l’onglet réunion et de la boîte de dialogue en réunion.</span><span class="sxs-lookup"><span data-stu-id="92d1c-115">For experiences during meetings, refer to the in-meeting tab and in-meeting dialog design guidelines.</span></span> <span data-ttu-id="92d1c-116">Pour plus d’informations, [voir Teams recommandations](../tabs/design/tabs.md)en matière de conception d’onglets, [](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab)de recommandations en matière de conception d’onglets en réunion et de conception de boîte de dialogue en [réunion.](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)</span><span class="sxs-lookup"><span data-stu-id="92d1c-116">For more information, see [Teams tab design guidelines](../tabs/design/tabs.md), [in-meeting tab design guidelines](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab), and [in-meeting dialog design guidelines](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog).</span></span>

* <span data-ttu-id="92d1c-117">Vous devez prendre en charge l’étendue pour activer votre application dans les conversations `groupchat` préalables à la réunion et post-réunion.</span><span class="sxs-lookup"><span data-stu-id="92d1c-117">You must support the `groupchat` scope to enable your app in pre-meeting and post-meeting chats.</span></span> <span data-ttu-id="92d1c-118">Avec l’expérience d’application de pré-réunion, vous pouvez rechercher et ajouter des applications de réunion et effectuer des tâches préalables à la réunion.</span><span class="sxs-lookup"><span data-stu-id="92d1c-118">With the pre-meeting app experience, you can find and add meeting apps and perform pre-meeting tasks.</span></span> <span data-ttu-id="92d1c-119">Avec l’expérience d’application post-réunion, vous pouvez afficher les résultats de la réunion, tels que les résultats des sondages ou les commentaires.</span><span class="sxs-lookup"><span data-stu-id="92d1c-119">With post-meeting app experience, you can view the results of the meeting, such as poll survey results or feedback.</span></span>

* <span data-ttu-id="92d1c-120">Les paramètres d’URL de l’API de réunion doivent avoir `meetingId` `userId` , et `tenantId` .</span><span class="sxs-lookup"><span data-stu-id="92d1c-120">Meeting API URL parameters must have `meetingId`, `userId`, and `tenantId`.</span></span> <span data-ttu-id="92d1c-121">Ceux-ci sont disponibles dans le cadre de l Teams du SDK client et du bot.</span><span class="sxs-lookup"><span data-stu-id="92d1c-121">These are available as part of the Teams Client SDK and bot activity.</span></span> <span data-ttu-id="92d1c-122">En outre, vous pouvez récupérer des informations fiables pour l’ID utilisateur et l’ID client à l’aide de l’authentification [sso tab.](../tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="92d1c-122">In addition, you can retrieve reliable information for user ID and tenant ID using [tab SSO authentication](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>

* <span data-ttu-id="92d1c-123">`GetParticipant`L’API doit avoir un ID et une inscription de bot pour générer des jetons d’th.</span><span class="sxs-lookup"><span data-stu-id="92d1c-123">The `GetParticipant` API must have a bot registration and ID to generate auth tokens.</span></span> <span data-ttu-id="92d1c-124">Pour plus d’informations, voir [l’inscription et l’ID du bot.](../build-your-first-app/build-bot.md)</span><span class="sxs-lookup"><span data-stu-id="92d1c-124">For more information, see [bot registration and ID](../build-your-first-app/build-bot.md).</span></span>

* <span data-ttu-id="92d1c-125">Pour que votre application soit mise à jour en temps réel, elle doit être à jour en fonction des activités d’événements de la réunion.</span><span class="sxs-lookup"><span data-stu-id="92d1c-125">For your app to update in real time, it must be up-to-date based on event activities in the meeting.</span></span> <span data-ttu-id="92d1c-126">Ces événements peuvent se trouver dans la boîte de dialogue de réunion et dans d’autres étapes du cycle de vie de la réunion.</span><span class="sxs-lookup"><span data-stu-id="92d1c-126">These events can be within the in-meeting dialog box and other stages across the meeting lifecycle.</span></span> <span data-ttu-id="92d1c-127">Pour la boîte de dialogue de réunion, voir paramètre `bot Id` d’achèvement dans `NotificationSignal` l’API.</span><span class="sxs-lookup"><span data-stu-id="92d1c-127">For the in-meeting dialog box, see completion `bot Id` parameter in `NotificationSignal` API.</span></span>

* <span data-ttu-id="92d1c-128">L’API Détails de la réunion doit avoir un ID de bot et d’inscription de bot.</span><span class="sxs-lookup"><span data-stu-id="92d1c-128">Meeting Details API must have a bot registration and bot ID.</span></span> <span data-ttu-id="92d1c-129">Il nécessite le SDK bot pour obtenir `TurnContext` .</span><span class="sxs-lookup"><span data-stu-id="92d1c-129">It requires Bot SDK to get `TurnContext`.</span></span>

* <span data-ttu-id="92d1c-130">Pour les événements de réunion en temps réel, vous devez connaître `TurnContext` l’objet disponible via le Bot SDK.</span><span class="sxs-lookup"><span data-stu-id="92d1c-130">For real-time meeting events, you must be familiar with the `TurnContext` object available through the Bot SDK.</span></span> <span data-ttu-id="92d1c-131">`Activity`L’objet dans contient la charge utile avec `TurnContext` l’heure de début et de fin réelle.</span><span class="sxs-lookup"><span data-stu-id="92d1c-131">The `Activity` object in `TurnContext` contains the payload with the actual start and end time.</span></span> <span data-ttu-id="92d1c-132">Les événements de réunion en temps réel nécessitent un ID de bot inscrit à partir de la Teams web.</span><span class="sxs-lookup"><span data-stu-id="92d1c-132">Real-time meeting events require a registered bot ID from the Teams platform.</span></span>

<span data-ttu-id="92d1c-133">Une fois que vous avez satisfait aux conditions préalables, vous pouvez utiliser les références de l’API des applications de réunion , et l’API Détails de la réunion qui vous permettent d’accéder aux informations à l’aide d’attributs et d’afficher le contenu `GetUserContext` `GetParticipant` `NotificationSignal` pertinent.</span><span class="sxs-lookup"><span data-stu-id="92d1c-133">After you have gone through the prerequisites, you can use the meeting apps API references `GetUserContext`, `GetParticipant`, `NotificationSignal`, and Meeting Details API that enable you to access information using attributes and display relevant content.</span></span>

## <a name="meeting-apps-api-references"></a><span data-ttu-id="92d1c-134">Références de l’API des applications de réunion</span><span class="sxs-lookup"><span data-stu-id="92d1c-134">Meeting apps API references</span></span>

<span data-ttu-id="92d1c-135">Les nouvelles fonctionnalités de réunion vous fournissent des API qui transforment l’expérience de réunion.</span><span class="sxs-lookup"><span data-stu-id="92d1c-135">The new meeting extensibilities provide you with APIs that transform the meeting experience.</span></span> <span data-ttu-id="92d1c-136">Avec cette nouvelle fonctionnalité, vous pouvez créer des applications ou intégrer des applications existantes dans le cycle de vie de la réunion.</span><span class="sxs-lookup"><span data-stu-id="92d1c-136">With this new capability, you can build apps or integrate existing apps within the meeting lifecycle.</span></span> <span data-ttu-id="92d1c-137">Vous pouvez utiliser les API pour que votre application soit au courant de la réunion.</span><span class="sxs-lookup"><span data-stu-id="92d1c-137">You can use the APIs to make your app aware of the meeting.</span></span> <span data-ttu-id="92d1c-138">Vous pouvez choisir les API que vous souhaitez utiliser pour améliorer l’expérience de réunion.</span><span class="sxs-lookup"><span data-stu-id="92d1c-138">You can choose which APIs you want to use to enhance the meeting experience.</span></span>

<span data-ttu-id="92d1c-139">Le tableau suivant fournit la liste de ces API :</span><span class="sxs-lookup"><span data-stu-id="92d1c-139">The following table provides a list of these APIs:</span></span>

|<span data-ttu-id="92d1c-140">API</span><span class="sxs-lookup"><span data-stu-id="92d1c-140">API</span></span>|<span data-ttu-id="92d1c-141">Description</span><span class="sxs-lookup"><span data-stu-id="92d1c-141">Description</span></span>|<span data-ttu-id="92d1c-142">Demande</span><span class="sxs-lookup"><span data-stu-id="92d1c-142">Request</span></span>|<span data-ttu-id="92d1c-143">Source</span><span class="sxs-lookup"><span data-stu-id="92d1c-143">Source</span></span>|
|---|---|----|---|
|<span data-ttu-id="92d1c-144">**GetUserContext**</span><span class="sxs-lookup"><span data-stu-id="92d1c-144">**GetUserContext**</span></span>| <span data-ttu-id="92d1c-145">Cette API vous permet d’obtenir des informations contextuelles pour afficher du contenu pertinent dans Teams onglet.</span><span class="sxs-lookup"><span data-stu-id="92d1c-145">This API enables you to get contextual information to display relevant content in a Teams tab.</span></span> |<span data-ttu-id="92d1c-146">_**microsoftTeams.getContext( ( ) => { /*...\* / } )*\*_</span><span class="sxs-lookup"><span data-stu-id="92d1c-146">_**microsoftTeams.getContext( ( ) => {  /*...*/ } )**_</span></span>|<span data-ttu-id="92d1c-147">Microsoft Teams Client SDK</span><span class="sxs-lookup"><span data-stu-id="92d1c-147">Microsoft Teams Client SDK</span></span>|
|<span data-ttu-id="92d1c-148">**GetParticipant**</span><span class="sxs-lookup"><span data-stu-id="92d1c-148">**GetParticipant**</span></span>| <span data-ttu-id="92d1c-149">Cette API permet à un bot de récupérer les informations des participants par ID de réunion et ID de participant.</span><span class="sxs-lookup"><span data-stu-id="92d1c-149">This API allows a bot to fetch participant information by meeting ID and participant ID.</span></span> |<span data-ttu-id="92d1c-150">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span><span class="sxs-lookup"><span data-stu-id="92d1c-150">**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_</span></span> |<span data-ttu-id="92d1c-151">Microsoft Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="92d1c-151">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="92d1c-152">**NotificationSignal**</span><span class="sxs-lookup"><span data-stu-id="92d1c-152">**NotificationSignal**</span></span> | <span data-ttu-id="92d1c-153">Cette API vous permet de fournir des signaux de réunion fournis à l’aide de l’API de notification de conversation existante pour la conversation utilisateur-bot.</span><span class="sxs-lookup"><span data-stu-id="92d1c-153">This API enables you to provide meeting signals that are delivered using the existing conversation notification API for user-bot chat.</span></span> <span data-ttu-id="92d1c-154">Il vous permet de signaler en fonction de l’action de l’utilisateur qui affiche une boîte de dialogue en réunion.</span><span class="sxs-lookup"><span data-stu-id="92d1c-154">It allows you to signal based on user action that shows an in-meeting dialog box.</span></span> |<span data-ttu-id="92d1c-155">**POST** _**/v3/conversations/{conversationId}/activities**_</span><span class="sxs-lookup"><span data-stu-id="92d1c-155">**POST** _**/v3/conversations/{conversationId}/activities**_</span></span>|<span data-ttu-id="92d1c-156">Microsoft Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="92d1c-156">Microsoft Bot Framework SDK</span></span>|
|<span data-ttu-id="92d1c-157">**Détails de la réunion**</span><span class="sxs-lookup"><span data-stu-id="92d1c-157">**Meeting Details**</span></span> | <span data-ttu-id="92d1c-158">Cette API vous permet d’obtenir des métadonnées de réunion statiques.</span><span class="sxs-lookup"><span data-stu-id="92d1c-158">This API enables you to get static meeting metadata.</span></span> |<span data-ttu-id="92d1c-159">**GET** _**/v1/meetings/{meetingId}**_</span><span class="sxs-lookup"><span data-stu-id="92d1c-159">**GET** _**/v1/meetings/{meetingId}**_</span></span>| <span data-ttu-id="92d1c-160">Bot SDK</span><span class="sxs-lookup"><span data-stu-id="92d1c-160">Bot SDK</span></span> |

### <a name="getusercontext-api"></a><span data-ttu-id="92d1c-161">GetUserContext API</span><span class="sxs-lookup"><span data-stu-id="92d1c-161">GetUserContext API</span></span>

<span data-ttu-id="92d1c-162">Pour identifier et récupérer des informations contextuelles pour le contenu de votre onglet, voir obtenir le [contexte de Teams onglet .](../tabs/how-to/access-teams-context.md#get-context-by-using-the-microsoft-teams-javascript-library) est utilisé par un onglet lors de l’exécution dans le contexte de réunion et est `meetingId` ajouté pour la charge utile de réponse.</span><span class="sxs-lookup"><span data-stu-id="92d1c-162">To identify and retrieve contextual information for your tab content, see [get context for your Teams tab](../tabs/how-to/access-teams-context.md#get-context-by-using-the-microsoft-teams-javascript-library). `meetingId` is used by a tab when running in the meeting context and is added for the response payload.</span></span>

### <a name="getparticipant-api"></a><span data-ttu-id="92d1c-163">GetParticipant API</span><span class="sxs-lookup"><span data-stu-id="92d1c-163">GetParticipant API</span></span>

> [!NOTE]
> * <span data-ttu-id="92d1c-164">Ne pas mettre en cache les rôles des participants, car l’organisateur de la réunion peut modifier les rôles à tout moment.</span><span class="sxs-lookup"><span data-stu-id="92d1c-164">Do not cache participant roles since the meeting organizer can change the roles any time.</span></span>
> * <span data-ttu-id="92d1c-165">Teams ne prend actuellement pas en charge les grandes listes de distribution ou les tailles de liste de plus de 350 participants pour `GetParticipant` l’API.</span><span class="sxs-lookup"><span data-stu-id="92d1c-165">Teams does not currently support large distribution lists or roster sizes of more than 350 participants for the `GetParticipant` API.</span></span>

<span data-ttu-id="92d1c-166">L’API permet à un bot de récupérer les informations des participants par ID de réunion et `GetParticipant` ID de participant.</span><span class="sxs-lookup"><span data-stu-id="92d1c-166">The `GetParticipant` API allows a bot to fetch participant information by meeting ID and participant ID.</span></span> <span data-ttu-id="92d1c-167">L’API inclut des paramètres de requête, des exemples et des codes de réponse.</span><span class="sxs-lookup"><span data-stu-id="92d1c-167">The API includes query parameters, examples, and response codes.</span></span>

#### <a name="query-parameters"></a><span data-ttu-id="92d1c-168">Paramètres de requête</span><span class="sxs-lookup"><span data-stu-id="92d1c-168">Query parameters</span></span>

<span data-ttu-id="92d1c-169">`GetParticipant`L’API inclut les paramètres de requête suivants :</span><span class="sxs-lookup"><span data-stu-id="92d1c-169">The `GetParticipant` API includes the following query parameters:</span></span>

|<span data-ttu-id="92d1c-170">Valeur</span><span class="sxs-lookup"><span data-stu-id="92d1c-170">Value</span></span>|<span data-ttu-id="92d1c-171">Type</span><span class="sxs-lookup"><span data-stu-id="92d1c-171">Type</span></span>|<span data-ttu-id="92d1c-172">Requis</span><span class="sxs-lookup"><span data-stu-id="92d1c-172">Required</span></span>|<span data-ttu-id="92d1c-173">Description</span><span class="sxs-lookup"><span data-stu-id="92d1c-173">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="92d1c-174">**meetingId**</span><span class="sxs-lookup"><span data-stu-id="92d1c-174">**meetingId**</span></span>| <span data-ttu-id="92d1c-175">String</span><span class="sxs-lookup"><span data-stu-id="92d1c-175">String</span></span> | <span data-ttu-id="92d1c-176">Oui</span><span class="sxs-lookup"><span data-stu-id="92d1c-176">Yes</span></span> | <span data-ttu-id="92d1c-177">L’identificateur de réunion est disponible via Bot Invoke et Teams Client SDK.</span><span class="sxs-lookup"><span data-stu-id="92d1c-177">The meeting identifier is available through Bot Invoke and Teams Client SDK.</span></span>|
|<span data-ttu-id="92d1c-178">**participantId**</span><span class="sxs-lookup"><span data-stu-id="92d1c-178">**participantId**</span></span>| <span data-ttu-id="92d1c-179">String</span><span class="sxs-lookup"><span data-stu-id="92d1c-179">String</span></span> | <span data-ttu-id="92d1c-180">Oui</span><span class="sxs-lookup"><span data-stu-id="92d1c-180">Yes</span></span> | <span data-ttu-id="92d1c-181">L’ID de participant est l’ID utilisateur.</span><span class="sxs-lookup"><span data-stu-id="92d1c-181">The participant ID is the user ID.</span></span> <span data-ttu-id="92d1c-182">Il est disponible dans tabulation SSO, Bot Invoke et Teams Client SDK.</span><span class="sxs-lookup"><span data-stu-id="92d1c-182">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="92d1c-183">Il est recommandé d’obtenir un ID de participant à partir de l' sso tabulation.</span><span class="sxs-lookup"><span data-stu-id="92d1c-183">It is recommended to get a participant ID from the Tab SSO.</span></span> |
|<span data-ttu-id="92d1c-184">**tenantId**</span><span class="sxs-lookup"><span data-stu-id="92d1c-184">**tenantId**</span></span>| <span data-ttu-id="92d1c-185">String</span><span class="sxs-lookup"><span data-stu-id="92d1c-185">String</span></span> | <span data-ttu-id="92d1c-186">Oui</span><span class="sxs-lookup"><span data-stu-id="92d1c-186">Yes</span></span> | <span data-ttu-id="92d1c-187">L’ID de client est requis pour les utilisateurs du client.</span><span class="sxs-lookup"><span data-stu-id="92d1c-187">The tenant ID is required for the tenant users.</span></span> <span data-ttu-id="92d1c-188">Il est disponible dans tabulation SSO, Bot Invoke et Teams Client SDK.</span><span class="sxs-lookup"><span data-stu-id="92d1c-188">It is available in Tab SSO, Bot Invoke, and Teams Client SDK.</span></span> <span data-ttu-id="92d1c-189">Il est recommandé d’obtenir un ID de client à partir de l' sso tabulation.</span><span class="sxs-lookup"><span data-stu-id="92d1c-189">It is recommended to get a tenant ID from the Tab SSO.</span></span> |

#### <a name="example"></a><span data-ttu-id="92d1c-190">Exemple</span><span class="sxs-lookup"><span data-stu-id="92d1c-190">Example</span></span>

<span data-ttu-id="92d1c-191">`GetParticipant`L’API inclut les exemples suivants :</span><span class="sxs-lookup"><span data-stu-id="92d1c-191">The `GetParticipant` API includes the following examples:</span></span>

# <a name="c"></a>[<span data-ttu-id="92d1c-192">C#</span><span class="sxs-lookup"><span data-stu-id="92d1c-192">C#</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="92d1c-193">JavaScript</span><span class="sxs-lookup"><span data-stu-id="92d1c-193">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="92d1c-194">JSON</span><span class="sxs-lookup"><span data-stu-id="92d1c-194">JSON</span></span>](#tab/json)

```http
GET /v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

---

<span data-ttu-id="92d1c-195">Le corps de la réponse JSON pour `GetParticipant` l’API est :</span><span class="sxs-lookup"><span data-stu-id="92d1c-195">The JSON response body for `GetParticipant` API is:</span></span>

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

#### <a name="response-codes"></a><span data-ttu-id="92d1c-196">Codes de réponse</span><span class="sxs-lookup"><span data-stu-id="92d1c-196">Response codes</span></span>

<span data-ttu-id="92d1c-197">`GetParticipant`L’API inclut les codes de réponse suivants :</span><span class="sxs-lookup"><span data-stu-id="92d1c-197">The `GetParticipant` API includes the following response codes:</span></span>

|<span data-ttu-id="92d1c-198">Code de réponse</span><span class="sxs-lookup"><span data-stu-id="92d1c-198">Response code</span></span>|<span data-ttu-id="92d1c-199">Description</span><span class="sxs-lookup"><span data-stu-id="92d1c-199">Description</span></span>|
|---|---|
| <span data-ttu-id="92d1c-200">**403**</span><span class="sxs-lookup"><span data-stu-id="92d1c-200">**403**</span></span> | <span data-ttu-id="92d1c-201">L’application n’est pas autorisée à obtenir des informations sur les participants.</span><span class="sxs-lookup"><span data-stu-id="92d1c-201">The app is not allowed to get participant information.</span></span> <span data-ttu-id="92d1c-202">Il s’agit de la réponse d’erreur la plus courante et est déclenchée si l’application n’est pas installée dans la réunion.</span><span class="sxs-lookup"><span data-stu-id="92d1c-202">This is the most common error response and is triggered if the app is not installed in the meeting.</span></span> <span data-ttu-id="92d1c-203">Par exemple, si l’application est désactivée par l’administrateur client ou bloquée lors de la migration de site en direct.</span><span class="sxs-lookup"><span data-stu-id="92d1c-203">For example, if the app is disabled by tenant admin or blocked during live site migration.</span></span>|
| <span data-ttu-id="92d1c-204">**200**</span><span class="sxs-lookup"><span data-stu-id="92d1c-204">**200**</span></span> | <span data-ttu-id="92d1c-205">Les informations sur les participants sont récupérées avec succès.</span><span class="sxs-lookup"><span data-stu-id="92d1c-205">The participant information is successfully retrieved.</span></span>|
| <span data-ttu-id="92d1c-206">**401**</span><span class="sxs-lookup"><span data-stu-id="92d1c-206">**401**</span></span> | <span data-ttu-id="92d1c-207">L’application répond avec un jeton non valide.</span><span class="sxs-lookup"><span data-stu-id="92d1c-207">The app responds with an invalid token.</span></span>|
| <span data-ttu-id="92d1c-208">**404**</span><span class="sxs-lookup"><span data-stu-id="92d1c-208">**404**</span></span> | <span data-ttu-id="92d1c-209">La réunion a expiré ou le participant est in peut-être trouvé.</span><span class="sxs-lookup"><span data-stu-id="92d1c-209">The meeting has either expired or participant cannot be found.</span></span>|
| <span data-ttu-id="92d1c-210">**500**</span><span class="sxs-lookup"><span data-stu-id="92d1c-210">**500**</span></span> | <span data-ttu-id="92d1c-211">La réunion a expiré (plus de 60 jours) depuis la fin de la réunion ou les participants ne disposent pas d’autorisations en fonction de leur rôle.</span><span class="sxs-lookup"><span data-stu-id="92d1c-211">The meeting has either expired (more than 60 days) since the meeting ended or the participants do not have permissions based on their role.</span></span>|

### <a name="notificationsignal-api"></a><span data-ttu-id="92d1c-212">NotificationSignal API</span><span class="sxs-lookup"><span data-stu-id="92d1c-212">NotificationSignal API</span></span>

<span data-ttu-id="92d1c-213">Tous les utilisateurs d’une réunion reçoivent les notifications envoyées via `NotificationSignal` l’API.</span><span class="sxs-lookup"><span data-stu-id="92d1c-213">All users in a meeting receive the notifications sent through the `NotificationSignal` API.</span></span>

> [!NOTE]
> * <span data-ttu-id="92d1c-214">Lorsqu’une boîte de dialogue de réunion est invoquée, le contenu est présenté comme un message de conversation.</span><span class="sxs-lookup"><span data-stu-id="92d1c-214">When an in-meeting dialog box is invoked, the content is presented as a chat message.</span></span>
> * <span data-ttu-id="92d1c-215">Actuellement, l’envoi de notifications ciblées n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="92d1c-215">Currently, sending targeted notifications is not supported.</span></span>

<span data-ttu-id="92d1c-216">`NotificationSignal` L’API vous permet de fournir des signaux de réunion fournis à l’aide de l’API de notification de conversation existante pour la conversation utilisateur-bot.</span><span class="sxs-lookup"><span data-stu-id="92d1c-216">`NotificationSignal` API enables you to provide meeting signals that are delivered using the existing conversation notification API for user-bot chat.</span></span> <span data-ttu-id="92d1c-217">Cette API vous permet de signaler en fonction de l’action de l’utilisateur qui affiche une boîte de dialogue en réunion.</span><span class="sxs-lookup"><span data-stu-id="92d1c-217">This API allows you to signal based on user action that shows an in-meeting dialog box.</span></span> <span data-ttu-id="92d1c-218">L’API inclut le paramètre de requête, des exemples et des codes de réponse.</span><span class="sxs-lookup"><span data-stu-id="92d1c-218">The API includes query parameter, examples, and response codes.</span></span>

#### <a name="query-parameter"></a><span data-ttu-id="92d1c-219">Paramètre de requête</span><span class="sxs-lookup"><span data-stu-id="92d1c-219">Query parameter</span></span>

<span data-ttu-id="92d1c-220">`NotificationSignal`L’API inclut le paramètre de requête suivant :</span><span class="sxs-lookup"><span data-stu-id="92d1c-220">The `NotificationSignal` API includes the following query parameter:</span></span>

|<span data-ttu-id="92d1c-221">Valeur</span><span class="sxs-lookup"><span data-stu-id="92d1c-221">Value</span></span>|<span data-ttu-id="92d1c-222">Type</span><span class="sxs-lookup"><span data-stu-id="92d1c-222">Type</span></span>|<span data-ttu-id="92d1c-223">Requis</span><span class="sxs-lookup"><span data-stu-id="92d1c-223">Required</span></span>|<span data-ttu-id="92d1c-224">Description</span><span class="sxs-lookup"><span data-stu-id="92d1c-224">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="92d1c-225">**conversationId**</span><span class="sxs-lookup"><span data-stu-id="92d1c-225">**conversationId**</span></span>| <span data-ttu-id="92d1c-226">String</span><span class="sxs-lookup"><span data-stu-id="92d1c-226">String</span></span> | <span data-ttu-id="92d1c-227">Oui</span><span class="sxs-lookup"><span data-stu-id="92d1c-227">Yes</span></span> | <span data-ttu-id="92d1c-228">L’identificateur de conversation est disponible dans le cadre de Bot Invoke.</span><span class="sxs-lookup"><span data-stu-id="92d1c-228">The conversation identifier is available as part of Bot Invoke.</span></span> |

#### <a name="examples"></a><span data-ttu-id="92d1c-229">Exemples</span><span class="sxs-lookup"><span data-stu-id="92d1c-229">Examples</span></span>

<span data-ttu-id="92d1c-230">`Bot ID`L’objet est déclaré dans le manifeste et le bot reçoit un objet de résultat.</span><span class="sxs-lookup"><span data-stu-id="92d1c-230">The `Bot ID` is declared in the manifest and the bot receives a result object.</span></span>

> [!NOTE]
> * <span data-ttu-id="92d1c-231">Le `completionBotId` paramètre est facultatif dans `externalResourceUrl` l’exemple de charge utile demandé.</span><span class="sxs-lookup"><span data-stu-id="92d1c-231">The `completionBotId` parameter of the `externalResourceUrl` is optional in the requested payload example.</span></span> <span data-ttu-id="92d1c-232">`Bot ID` est déclaré dans le manifeste et le bot reçoit un objet de résultat.</span><span class="sxs-lookup"><span data-stu-id="92d1c-232">`Bot ID` is declared in the manifest and the bot receives a result object.</span></span>
> * <span data-ttu-id="92d1c-233">Les `externalResourceUrl` paramètres de largeur et de hauteur doivent être en pixels.</span><span class="sxs-lookup"><span data-stu-id="92d1c-233">The `externalResourceUrl` width and height parameters must be in pixels.</span></span> <span data-ttu-id="92d1c-234">Pour vous assurer que les dimensions sont dans les limites autorisées, consultez les [instructions de conception.](design/designing-apps-in-meetings.md)</span><span class="sxs-lookup"><span data-stu-id="92d1c-234">To ensure the dimensions are within the allowed limits, see [design guidelines](design/designing-apps-in-meetings.md).</span></span>
> * <span data-ttu-id="92d1c-235">L’URL est la page chargée en tant que dans la boîte de `<iframe>` dialogue de la réunion.</span><span class="sxs-lookup"><span data-stu-id="92d1c-235">The URL is the page loaded as an `<iframe>` in the in-meeting dialog box.</span></span> <span data-ttu-id="92d1c-236">Le domaine doit se trouver dans le tableau de l’application `validDomains` dans le manifeste de votre application.</span><span class="sxs-lookup"><span data-stu-id="92d1c-236">The domain must be in the app's `validDomains` array in your app manifest.</span></span>

<span data-ttu-id="92d1c-237">`NotificationSignal`L’API inclut les exemples suivants :</span><span class="sxs-lookup"><span data-stu-id="92d1c-237">The `NotificationSignal` API includes the following examples:</span></span>

# <a name="c"></a>[<span data-ttu-id="92d1c-238">C#</span><span class="sxs-lookup"><span data-stu-id="92d1c-238">C#</span></span>](#tab/dotnet)

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

# <a name="javascript"></a>[<span data-ttu-id="92d1c-239">JavaScript</span><span class="sxs-lookup"><span data-stu-id="92d1c-239">JavaScript</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="92d1c-240">JSON</span><span class="sxs-lookup"><span data-stu-id="92d1c-240">JSON</span></span>](#tab/json)

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

#### <a name="response-codes"></a><span data-ttu-id="92d1c-241">Codes de réponse</span><span class="sxs-lookup"><span data-stu-id="92d1c-241">Response codes</span></span>

<span data-ttu-id="92d1c-242">`NotificationSignal`L’API inclut les codes de réponse suivants :</span><span class="sxs-lookup"><span data-stu-id="92d1c-242">The `NotificationSignal` API includes the following response codes:</span></span>

|<span data-ttu-id="92d1c-243">Code de réponse</span><span class="sxs-lookup"><span data-stu-id="92d1c-243">Response code</span></span>|<span data-ttu-id="92d1c-244">Description</span><span class="sxs-lookup"><span data-stu-id="92d1c-244">Description</span></span>|
|---|---|
| <span data-ttu-id="92d1c-245">**201**</span><span class="sxs-lookup"><span data-stu-id="92d1c-245">**201**</span></span> | <span data-ttu-id="92d1c-246">L’activité avec le signal est envoyée avec succès.</span><span class="sxs-lookup"><span data-stu-id="92d1c-246">The activity with signal is successfully sent.</span></span> |
| <span data-ttu-id="92d1c-247">**401**</span><span class="sxs-lookup"><span data-stu-id="92d1c-247">**401**</span></span> | <span data-ttu-id="92d1c-248">L’application répond avec un jeton non valide.</span><span class="sxs-lookup"><span data-stu-id="92d1c-248">The app responds with an invalid token.</span></span> |
| <span data-ttu-id="92d1c-249">**403**</span><span class="sxs-lookup"><span data-stu-id="92d1c-249">**403**</span></span> | <span data-ttu-id="92d1c-250">L’application ne peut pas envoyer le signal.</span><span class="sxs-lookup"><span data-stu-id="92d1c-250">The app is unable to send the signal.</span></span> <span data-ttu-id="92d1c-251">Cela peut se produire pour diverses raisons, telles que la désactivation de l’application par l’administrateur client, le blocage de l’application pendant la migration du site en direct, etc.</span><span class="sxs-lookup"><span data-stu-id="92d1c-251">This can happen due to various reasons such as the tenant admin disables the app, the app is blocked during live site migration, and so on.</span></span> <span data-ttu-id="92d1c-252">Dans ce cas, la charge utile contient un message d’erreur détaillé.</span><span class="sxs-lookup"><span data-stu-id="92d1c-252">In this case, the payload contains a detailed error message.</span></span> |
| <span data-ttu-id="92d1c-253">**404**</span><span class="sxs-lookup"><span data-stu-id="92d1c-253">**404**</span></span> | <span data-ttu-id="92d1c-254">La conversation de réunion n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="92d1c-254">The meeting chat does not exist.</span></span> |

### <a name="meeting-details-api"></a><span data-ttu-id="92d1c-255">API Détails de la réunion</span><span class="sxs-lookup"><span data-stu-id="92d1c-255">Meeting Details API</span></span>

> [!NOTE]
> <span data-ttu-id="92d1c-256">Cette fonctionnalité est actuellement disponible en prévisualisation [pour les](../resources/dev-preview/developer-preview-intro.md) développeurs publics uniquement.</span><span class="sxs-lookup"><span data-stu-id="92d1c-256">This feature is currently available in [public developer preview](../resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="92d1c-257">L’API Détails de la réunion permet à votre application d’obtenir des métadonnées de réunion statiques.</span><span class="sxs-lookup"><span data-stu-id="92d1c-257">The Meeting Details API enables your app to get static meeting metadata.</span></span> <span data-ttu-id="92d1c-258">Il s’agit de points de données qui ne changent pas dynamiquement.</span><span class="sxs-lookup"><span data-stu-id="92d1c-258">These are data points that do not change dynamically.</span></span>
<span data-ttu-id="92d1c-259">L’API est disponible via Bot Services.</span><span class="sxs-lookup"><span data-stu-id="92d1c-259">The API is available through Bot Services.</span></span>

#### <a name="prerequisite"></a><span data-ttu-id="92d1c-260">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="92d1c-260">Prerequisite</span></span>

<span data-ttu-id="92d1c-261">Pour utiliser l’API Détails de la réunion, vous devez obtenir les autorisations RSC.</span><span class="sxs-lookup"><span data-stu-id="92d1c-261">To use the Meeting Details API, you must obtain RSC permissions.</span></span> <span data-ttu-id="92d1c-262">Utilisez l’exemple suivant pour configurer la propriété du manifeste de votre `webApplicationInfo` application :</span><span class="sxs-lookup"><span data-stu-id="92d1c-262">Use the following example to configure your app manifest's `webApplicationInfo` property:</span></span>

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    "applicationPermissions": [
      "OnlineMeeting.ReadBasic.Chat"
    ]
}
 ```
 
#### <a name="query-parameter"></a><span data-ttu-id="92d1c-263">Paramètre de requête</span><span class="sxs-lookup"><span data-stu-id="92d1c-263">Query parameter</span></span>

<span data-ttu-id="92d1c-264">L’API Détails de la réunion inclut le paramètre de requête suivant :</span><span class="sxs-lookup"><span data-stu-id="92d1c-264">The Meeting Details API includes the following query parameter:</span></span>

|<span data-ttu-id="92d1c-265">Valeur</span><span class="sxs-lookup"><span data-stu-id="92d1c-265">Value</span></span>|<span data-ttu-id="92d1c-266">Type</span><span class="sxs-lookup"><span data-stu-id="92d1c-266">Type</span></span>|<span data-ttu-id="92d1c-267">Requis</span><span class="sxs-lookup"><span data-stu-id="92d1c-267">Required</span></span>|<span data-ttu-id="92d1c-268">Description</span><span class="sxs-lookup"><span data-stu-id="92d1c-268">Description</span></span>|
|---|---|----|---|
|<span data-ttu-id="92d1c-269">**meetingId**</span><span class="sxs-lookup"><span data-stu-id="92d1c-269">**meetingId**</span></span>| <span data-ttu-id="92d1c-270">String</span><span class="sxs-lookup"><span data-stu-id="92d1c-270">String</span></span> | <span data-ttu-id="92d1c-271">Oui</span><span class="sxs-lookup"><span data-stu-id="92d1c-271">Yes</span></span> | <span data-ttu-id="92d1c-272">L’identificateur de réunion est disponible via Bot Invoke et Teams Client SDK.</span><span class="sxs-lookup"><span data-stu-id="92d1c-272">The meeting identifier is available through Bot Invoke and Teams Client SDK.</span></span> |

#### <a name="example"></a><span data-ttu-id="92d1c-273">Exemple</span><span class="sxs-lookup"><span data-stu-id="92d1c-273">Example</span></span>

<span data-ttu-id="92d1c-274">L’API Détails de la réunion inclut les exemples suivants :</span><span class="sxs-lookup"><span data-stu-id="92d1c-274">The Meeting Details API includes the following examples:</span></span>

# <a name="c"></a>[<span data-ttu-id="92d1c-275">C#</span><span class="sxs-lookup"><span data-stu-id="92d1c-275">C#</span></span>](#tab/dotnet)

```csharp
var connectorClient = parameters.TurnContext.TurnState.Get<IConnectorClient>();
var creds = connectorClient.Credentials as AppCredentials;
var bearerToken = await creds.GetTokenAsync().ConfigureAwait(false);
var request = new HttpRequestMessage(HttpMethod.Get, new Uri(new Uri(connectorClient.BaseUri.OriginalString), $"v1/meetings/{meetingId}"));
request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", bearerToken);
HttpResponseMessage response = await (connectorClient as ServiceClient<ConnectorClient>).HttpClient.SendAsync(request, CancellationToken.None).ConfigureAwait(false);
string content;
if (response.Content != null)
{
    content = await response.Content.ReadAsStringAsync().ConfigureAwait(false);
}
```

# <a name="javascript"></a>[<span data-ttu-id="92d1c-276">JavaScript</span><span class="sxs-lookup"><span data-stu-id="92d1c-276">JavaScript</span></span>](#tab/javascript)

<span data-ttu-id="92d1c-277">Non disponible</span><span class="sxs-lookup"><span data-stu-id="92d1c-277">Not available</span></span>

# <a name="json"></a>[<span data-ttu-id="92d1c-278">JSON</span><span class="sxs-lookup"><span data-stu-id="92d1c-278">JSON</span></span>](#tab/json)

```http
GET /v1/meetings/{meetingId}
```

---

<span data-ttu-id="92d1c-279">Le corps de la réponse JSON pour l’API Détails de la réunion est le suivant :</span><span class="sxs-lookup"><span data-stu-id="92d1c-279">The JSON response body for Meeting Details API is as follows:</span></span>

```json
{ 
   "details": { 
        "id": "meeting ID", 
        "msGraphResourceId": "", 
        "scheduledStartTime": "2020-08-21T02:30:00+00:00", 
        "scheduledEndTime": "2020-08-21T03:00:00+00:00", 
        "joinUrl": "https://teams.microsoft.com/l/xx", 
        "title": "All Hands", 
        "type": "Scheduled" 
    }, 
    "conversation": { 
            "isGroup": true, 
            “conversationType”: “groupchat”, 
            "id": "meeting chat ID" 
    }, 
    "organizer": { 
        "id": "<organizer user ID>", 
        "aadObjectId": "<AAD ID>", 
        "tenantId": "<Tenant ID>" 
    }
} 
```

## <a name="real-time-teams-meeting-events"></a><span data-ttu-id="92d1c-280">Événements de réunion Teams en temps réel</span><span class="sxs-lookup"><span data-stu-id="92d1c-280">Real-time Teams meeting events</span></span>

> [!NOTE]
> <span data-ttu-id="92d1c-281">Cette fonctionnalité est actuellement disponible en prévisualisation [pour les](../resources/dev-preview/developer-preview-intro.md) développeurs publics uniquement.</span><span class="sxs-lookup"><span data-stu-id="92d1c-281">This feature is currently available in [public developer preview](../resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="92d1c-282">L’utilisateur peut recevoir des événements de réunion en temps réel.</span><span class="sxs-lookup"><span data-stu-id="92d1c-282">The user can receive real-time meeting events.</span></span> <span data-ttu-id="92d1c-283">Dès qu’une application est associée à une réunion, les heures de début et de fin de réunion réelles sont partagées avec le bot.</span><span class="sxs-lookup"><span data-stu-id="92d1c-283">As soon as any app is associated with a meeting, the actual meeting start and meeting end time are shared with the bot.</span></span>

<span data-ttu-id="92d1c-284">Les heures de début et de fin réelles d’une réunion sont différentes des heures de début et de fin prévues.</span><span class="sxs-lookup"><span data-stu-id="92d1c-284">Actual start and end time of a meeting are different from the scheduled start and end time.</span></span> <span data-ttu-id="92d1c-285">L’API des détails de la réunion fournit l’heure de début et de fin prévues, tandis que l’événement fournit l’heure de début et de fin réelle.</span><span class="sxs-lookup"><span data-stu-id="92d1c-285">The meeting details API provides the scheduled start and end time while the event provides the actual start and end time.</span></span>

### <a name="prerequisite"></a><span data-ttu-id="92d1c-286">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="92d1c-286">Prerequisite</span></span>

<span data-ttu-id="92d1c-287">Le manifeste de votre application doit avoir la propriété pour recevoir les événements de `webApplicationInfo` début et de fin de réunion.</span><span class="sxs-lookup"><span data-stu-id="92d1c-287">Your app manifest must have the `webApplicationInfo` property to receive the meeting start and end events.</span></span> <span data-ttu-id="92d1c-288">Utilisez l’exemple suivant pour configurer votre manifeste :</span><span class="sxs-lookup"><span data-stu-id="92d1c-288">Use the following example to configure your manifest:</span></span>

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    "applicationPermissions": [
      "OnlineMeeting.ReadBasic.Chat"
    ]
}
 ```

### <a name="example-of-meeting-start-event-payload"></a><span data-ttu-id="92d1c-289">Exemple de charge utile d’événement de début de réunion</span><span class="sxs-lookup"><span data-stu-id="92d1c-289">Example of meeting start event payload</span></span>

<span data-ttu-id="92d1c-290">Le code suivant fournit un exemple de charge utile d’événement de début de réunion :</span><span class="sxs-lookup"><span data-stu-id="92d1c-290">The following code provides an example of meeting start event payload:</span></span>

```json
{ 
    "name": "application/vnd.microsoft.meetingStart", 
    "type": "event", 
    "timestamp": "2021-04-29T16:10:41.1252256Z", 
    "id": "123", 
    "channelId": "msteams", 
    "serviceUrl": "https://microsoft.com", 
    "from": { 
        "id": "userID", 
        "aadObjectId": "aadOnjectId" 
    }, 
    "conversation": { 
        "isGroup": true, 
        "tenantId": "tenantId", 
        "id": "thread id" 
    }, 
    "recipient": { 
        "id": "user Id", 
        "name": "user name" 
    }, 
    "entities": [ 
        { 
            "locale": "en-US", 
            "country": "US", 
            "type": "clientInfo" 
        } 
    ], 
    "channelData": { 
        "tenant": { 
            "id": "channel id" 
        }, 
        "source": null, 
        "meeting": { 
            "id": "meeting id" 
        } 
    }, 
    "value": { 
        "MeetingType": "Scheduled", 
        "Title": "Meeting Start/End Event", 
        "Id":"meeting id", 
        "JoinUrl": "url" 
        "StartTime": "2021-04-29T16:17:17.4388966Z" 
    }, 
    "locale": "en-US" 
}
```

### <a name="example-of-meeting-end-event-payload"></a><span data-ttu-id="92d1c-291">Exemple de charge utile d’événement de fin de réunion</span><span class="sxs-lookup"><span data-stu-id="92d1c-291">Example of meeting end event payload</span></span>

<span data-ttu-id="92d1c-292">Le code suivant fournit un exemple de charge utile d’événement de fin de réunion :</span><span class="sxs-lookup"><span data-stu-id="92d1c-292">The following code provides an example of meeting end event payload:</span></span>

```json
{ 
    "name": "application/vnd.microsoft.meetingEnd", 
    "type": "event", 
    "timestamp": "2021-04-29T16:17:17.4388966Z", 
    "id": "123", 
    "channelId": "msteams", 
    "serviceUrl": "https://microsoft.com", 
    "from": { 
        "id": "user id", 
        "aadObjectId": "aadObjectId" 
    }, 
    "conversation": { 
        "isGroup": true, 
        "tenantId": "tenantId", 
        "id": "thread id" 
    }, 
    "recipient": { 
        "id": "user id", 
        "name": "user name" 
    }, 
    "entities": [ 
        { 
            "locale": "en-US", 
            "country": "US", 
            "type": "clientInfo" 
        } 
    ], 
    "channelData": { 
        "tenant": { 
            "id": "channel id" 
        }, 
        "source": null, 
        "meeting": { 
            "id": "meeting Id" 
        } 
    }, 
    "value": { 
        "MeetingType": "Scheduled", 
        "Title": "Meeting Start/End Event in Canary", 
        "Id": "19:meeting_NTM3ZDJjOTUtZGRhOS00MzYxLTk5NDAtMzY4M2IzZWFjZGE1@thread.v2", 
        "JoinUrl": "url", 
        "EndTime": "2021-04-29T16:17:17.4388966Z" 
    }, 
    "locale": "en-US" 
}
```

### <a name="example-of-getting-metadata-of-a-meeting"></a><span data-ttu-id="92d1c-293">Exemple d’obtention des métadonnées d’une réunion</span><span class="sxs-lookup"><span data-stu-id="92d1c-293">Example of getting metadata of a meeting</span></span>

<span data-ttu-id="92d1c-294">Votre bot reçoit l’événement via `OnEventActivityAsync` le handler.</span><span class="sxs-lookup"><span data-stu-id="92d1c-294">Your bot receives the event through the `OnEventActivityAsync` handler.</span></span>

<span data-ttu-id="92d1c-295">Pour désérialiser la charge utile json, un objet modèle est introduit pour obtenir les métadonnées d’une réunion.</span><span class="sxs-lookup"><span data-stu-id="92d1c-295">To deserialize the json payload, a model object is introduced to get the metadata of a meeting.</span></span> <span data-ttu-id="92d1c-296">Les métadonnées d’une réunion résident dans la `value` propriété dans la charge utile de l’événement.</span><span class="sxs-lookup"><span data-stu-id="92d1c-296">The metadata of a meeting resides in the `value` property in the event payload.</span></span> <span data-ttu-id="92d1c-297">L’objet modèle est créé, dont les variables membres correspondent aux clés sous `MeetingStartEndEventvalue` la propriété dans la charge utile de `value` l’événement.</span><span class="sxs-lookup"><span data-stu-id="92d1c-297">The `MeetingStartEndEventvalue` model object is created, whose member variables correspond to the keys under the `value` property in the event payload.</span></span>

<span data-ttu-id="92d1c-298">Le code suivant montre comment capturer les métadonnées d’une réunion qui est , , , , et à partir d’un événement de début `MeetingType` et de fin de réunion `Title` `Id` `JoinUrl` `StartTime` `EndTime` :</span><span class="sxs-lookup"><span data-stu-id="92d1c-298">The following code shows how to capture the metadata of a meeting that is `MeetingType`, `Title`, `Id`, `JoinUrl`, `StartTime`, and `EndTime` from a meeting start and end event:</span></span>

```csharp
protected override async Task OnEventActivityAsync(
ITurnContext<IEventActivity> turnContext, CancellationToken cancellationToken)
{
    // Event Name is either 'application/vnd.microsoft.meetingStart' or 'application/vnd.microsoft.meetingEnd'
    var meetingEventName = turnContext.Activity.Name;
    // Value contains meeting information (ex: meeting type, start time, etc).
    var meetingEventInfo = turnContext.Activity.Value as JObject; 
    var meetingEventInfoObject =
meetingEventInfo.ToObject<MeetingStartEndEventValue>();
    // Create a very simple adaptive card with meeting information
var attachmentCard = createMeetingStartOrEndEventAttachment(meetingEventName,
meetingEventInfoObject);
    await turnContext.SendActivityAsync(MessageFactory.Attachment(attachmentCard));
}
```

<span data-ttu-id="92d1c-299">MeetingStartEndEventvalue.cs inclut le code suivant :</span><span class="sxs-lookup"><span data-stu-id="92d1c-299">The MeetingStartEndEventvalue.cs includes the following code:</span></span>

```csharp
public class MeetingStartEndEventValue
{
    public string Id { get; set; }
    public string Title { get; set; }
    public string MeetingType { get; set; }
    public string JoinUrl { get; set; }
    public string StartTime { get; set; }
    public string EndTime { get; set; }
}
```

## <a name="code-sample"></a><span data-ttu-id="92d1c-300">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="92d1c-300">Code sample</span></span>

|<span data-ttu-id="92d1c-301">Exemple de nom</span><span class="sxs-lookup"><span data-stu-id="92d1c-301">Sample name</span></span> | <span data-ttu-id="92d1c-302">Description</span><span class="sxs-lookup"><span data-stu-id="92d1c-302">Description</span></span> | <span data-ttu-id="92d1c-303">.NET</span><span class="sxs-lookup"><span data-stu-id="92d1c-303">.NET</span></span> | <span data-ttu-id="92d1c-304">Node.js</span><span class="sxs-lookup"><span data-stu-id="92d1c-304">Node.js</span></span> |
|----------------|-----------------|--------------|--------------|
| <span data-ttu-id="92d1c-305">Extensibilité des réunions</span><span class="sxs-lookup"><span data-stu-id="92d1c-305">Meetings extensibility</span></span> | <span data-ttu-id="92d1c-306">Microsoft Teams’extensibilité de réunion pour transmettre des jetons.</span><span class="sxs-lookup"><span data-stu-id="92d1c-306">Microsoft Teams meeting extensibility sample for passing tokens.</span></span> | [<span data-ttu-id="92d1c-307">View</span><span class="sxs-lookup"><span data-stu-id="92d1c-307">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [<span data-ttu-id="92d1c-308">View</span><span class="sxs-lookup"><span data-stu-id="92d1c-308">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
| <span data-ttu-id="92d1c-309">Bot de bulle de contenu de réunion</span><span class="sxs-lookup"><span data-stu-id="92d1c-309">Meeting content bubble bot</span></span> | <span data-ttu-id="92d1c-310">Microsoft Teams d’extensibilité de réunion pour interagir avec le bot de bulles de contenu dans une réunion.</span><span class="sxs-lookup"><span data-stu-id="92d1c-310">Microsoft Teams meeting extensibility sample for interacting with content bubble bot in a meeting.</span></span> | [<span data-ttu-id="92d1c-311">View</span><span class="sxs-lookup"><span data-stu-id="92d1c-311">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |  [<span data-ttu-id="92d1c-312">View</span><span class="sxs-lookup"><span data-stu-id="92d1c-312">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs)|
| <span data-ttu-id="92d1c-313">MeetingSidePanel</span><span class="sxs-lookup"><span data-stu-id="92d1c-313">Meeting meetingSidePanel</span></span> | <span data-ttu-id="92d1c-314">Microsoft Teams d’extensibilité de réunion pour interagir avec le panneau latéral en réunion.</span><span class="sxs-lookup"><span data-stu-id="92d1c-314">Microsoft Teams meeting extensibility sample for interacting with the side panel in-meeting.</span></span> | [<span data-ttu-id="92d1c-315">View</span><span class="sxs-lookup"><span data-stu-id="92d1c-315">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) | [<span data-ttu-id="92d1c-316">View</span><span class="sxs-lookup"><span data-stu-id="92d1c-316">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/nodejs)|
| <span data-ttu-id="92d1c-317">Onglet Détails de la réunion</span><span class="sxs-lookup"><span data-stu-id="92d1c-317">Details Tab in Meeting</span></span> | <span data-ttu-id="92d1c-318">Microsoft Teams’extensibilité de réunion pour l’itère avec l’onglet Détails en réunion.</span><span class="sxs-lookup"><span data-stu-id="92d1c-318">Microsoft Teams meeting extensibility sample for iteracting with Details Tab in-meeting.</span></span> | [<span data-ttu-id="92d1c-319">View</span><span class="sxs-lookup"><span data-stu-id="92d1c-319">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-details-tab/csharp) | [<span data-ttu-id="92d1c-320">View</span><span class="sxs-lookup"><span data-stu-id="92d1c-320">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-details-tab/nodejs)|

## <a name="see-also"></a><span data-ttu-id="92d1c-321">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="92d1c-321">See also</span></span>

* [<span data-ttu-id="92d1c-322">Recommandations en matière de conception de boîte de dialogue en réunion</span><span class="sxs-lookup"><span data-stu-id="92d1c-322">In-meeting dialog design guidelines</span></span>](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [<span data-ttu-id="92d1c-323">Teams d’authentification pour les onglets</span><span class="sxs-lookup"><span data-stu-id="92d1c-323">Teams authentication flow for tabs</span></span>](../tabs/how-to/authentication/auth-flow-tab.md)
* [<span data-ttu-id="92d1c-324">Applications pour Teams réunions</span><span class="sxs-lookup"><span data-stu-id="92d1c-324">Apps for Teams meetings</span></span>](teams-apps-in-meetings.md)

## <a name="next-step"></a><span data-ttu-id="92d1c-325">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="92d1c-325">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="92d1c-326">Activer et configurer vos applications pour Teams réunions</span><span class="sxs-lookup"><span data-stu-id="92d1c-326">Enable and configure your apps for Teams meetings</span></span>](enable-and-configure-your-app-for-teams-meetings.md)
