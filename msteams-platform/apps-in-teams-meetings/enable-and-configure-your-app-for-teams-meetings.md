---
title: Activer et configurer vos applications pour Teams réunions
author: laujan
description: Activer et configurer vos applications pour Teams réunions
ms.topic: conceptual
ms.openlocfilehash: 3484e82f3f51a9a92da6588234744c42a86b5730
ms.sourcegitcommit: 1cc1516e71441f6f3f82b35868e21ba9933333cd
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/25/2021
ms.locfileid: "52651732"
---
# <a name="enable-and-configure-your-apps-for-teams-meetings"></a><span data-ttu-id="550a7-103">Activer et configurer vos applications pour Teams réunions</span><span class="sxs-lookup"><span data-stu-id="550a7-103">Enable and configure your apps for Teams meetings</span></span>

<span data-ttu-id="550a7-104">Chaque équipe dispose d’une façon différente de communiquer et de collaborer sur des tâches.</span><span class="sxs-lookup"><span data-stu-id="550a7-104">Every team has a different way of communicating and collaborating tasks.</span></span> <span data-ttu-id="550a7-105">Vous pouvez effectuer ces différentes tâches en personnalisant Teams avec des applications pour les réunions.</span><span class="sxs-lookup"><span data-stu-id="550a7-105">You can achieve these different tasks by customizing Teams with apps for meetings.</span></span> <span data-ttu-id="550a7-106">Pour personnaliser et effectuer différentes tâches, vous devez activer vos applications pour les réunions Teams et configurer vos applications pour qu’elles soient disponibles dans l’étendue de la réunion dans leur manifeste d’application.</span><span class="sxs-lookup"><span data-stu-id="550a7-106">To customize and to achieve different tasks, you must enable your apps for Teams meetings and configure your apps to be available in meeting scope within their app manifest.</span></span>

## <a name="enable-your-app-for-teams-meetings"></a><span data-ttu-id="550a7-107">Activer votre application pour Teams réunions</span><span class="sxs-lookup"><span data-stu-id="550a7-107">Enable your app for Teams meetings</span></span>

<span data-ttu-id="550a7-108">Pour activer votre application pour Teams réunions, vous devez mettre à jour le manifeste de votre application et utiliser les propriétés de contexte pour déterminer où votre application doit apparaître.</span><span class="sxs-lookup"><span data-stu-id="550a7-108">To enable your app for Teams meetings, you must update your app manifest and use the context properties to determine where your app must appear.</span></span>

### <a name="update-your-app-manifest"></a><span data-ttu-id="550a7-109">Mettre à jour le manifeste de votre application</span><span class="sxs-lookup"><span data-stu-id="550a7-109">Update your app manifest</span></span>

<span data-ttu-id="550a7-110">Les fonctionnalités de l’application réunions sont déclarées dans le manifeste de votre application à l’aide `configurableTabs` des `scopes` tableaux et des `context` tableaux.</span><span class="sxs-lookup"><span data-stu-id="550a7-110">The meetings app capabilities are declared in your app manifest using the `configurableTabs`, `scopes`, and `context` arrays.</span></span> <span data-ttu-id="550a7-111">L’étendue définit à qui et le contexte définit l’endroit où votre application est disponible.</span><span class="sxs-lookup"><span data-stu-id="550a7-111">Scope defines to whom and context defines where your app is available.</span></span>

> [!NOTE]
> * <span data-ttu-id="550a7-112">Essayez de mettre à jour le manifeste de votre application avec [le schéma de manifeste.](../resources/schema/manifest-schema-dev-preview.md)</span><span class="sxs-lookup"><span data-stu-id="550a7-112">Try updating your app manifest with the [manifest schema](../resources/schema/manifest-schema-dev-preview.md).</span></span>
> * <span data-ttu-id="550a7-113">Les applications dans les réunions nécessitent une étendue groupchat.</span><span class="sxs-lookup"><span data-stu-id="550a7-113">Apps in meetings require groupchat scope.</span></span> <span data-ttu-id="550a7-114">L’étendue de l’équipe fonctionne pour les onglets dans les canaux uniquement.</span><span class="sxs-lookup"><span data-stu-id="550a7-114">The team scope works for tabs in channels only.</span></span>

<span data-ttu-id="550a7-115">Le manifeste de l’application doit inclure l’extrait de code suivant :</span><span class="sxs-lookup"><span data-stu-id="550a7-115">The app manifest must include the following code snippet:</span></span>

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
> <span data-ttu-id="550a7-116">`meetingStage` est actuellement disponible en [prévisualisation pour les](../resources/dev-preview/developer-preview-intro.md) développeurs uniquement.</span><span class="sxs-lookup"><span data-stu-id="550a7-116">`meetingStage` is currently available in [developer preview](../resources/dev-preview/developer-preview-intro.md) only.</span></span>

### <a name="context-property"></a><span data-ttu-id="550a7-117">Propriété Context</span><span class="sxs-lookup"><span data-stu-id="550a7-117">Context property</span></span>

<span data-ttu-id="550a7-118">La propriété détermine ce qui doit être affiché lorsqu’un utilisateur appelle une application dans une réunion en fonction de l’endroit où il `context` appelle l’application.</span><span class="sxs-lookup"><span data-stu-id="550a7-118">The `context` property determines what must be shown when a user invokes an app in a meeting depending on where the user invokes the app.</span></span> <span data-ttu-id="550a7-119">`context`L’onglet et `scopes` les propriétés vous permettent de déterminer où votre application doit apparaître.</span><span class="sxs-lookup"><span data-stu-id="550a7-119">The tab `context` and `scopes` properties enable you to determine where your app must appear.</span></span> <span data-ttu-id="550a7-120">Les onglets de la `team` ou `groupchat` de l’étendue peuvent avoir plusieurs contextes.</span><span class="sxs-lookup"><span data-stu-id="550a7-120">Tabs in the `team` or `groupchat` scope can have more than one context.</span></span> <span data-ttu-id="550a7-121">Voici les valeurs de la propriété à partir de laquelle vous pouvez utiliser l’ensemble ou `context` certaines des valeurs :</span><span class="sxs-lookup"><span data-stu-id="550a7-121">Following are the values for the `context` property from which you can use all or some of the values:</span></span>

|<span data-ttu-id="550a7-122">Valeur</span><span class="sxs-lookup"><span data-stu-id="550a7-122">Value</span></span>|<span data-ttu-id="550a7-123">Description</span><span class="sxs-lookup"><span data-stu-id="550a7-123">Description</span></span>|
|---|---|
| <span data-ttu-id="550a7-124">**channelTab**</span><span class="sxs-lookup"><span data-stu-id="550a7-124">**channelTab**</span></span> | <span data-ttu-id="550a7-125">Onglet dans l’en-tête d’un canal d’équipe.</span><span class="sxs-lookup"><span data-stu-id="550a7-125">A tab in the header of a team channel.</span></span> |
| <span data-ttu-id="550a7-126">**privateChatTab**</span><span class="sxs-lookup"><span data-stu-id="550a7-126">**privateChatTab**</span></span> | <span data-ttu-id="550a7-127">Onglet dans l’en-tête d’une conversation de groupe entre un ensemble d’utilisateurs, et non dans le contexte d’une équipe ou d’une réunion.</span><span class="sxs-lookup"><span data-stu-id="550a7-127">A tab in the header of a group chat between a set of users, not in the context of a team or meeting.</span></span> |
| <span data-ttu-id="550a7-128">**meetingChatTab**</span><span class="sxs-lookup"><span data-stu-id="550a7-128">**meetingChatTab**</span></span> | <span data-ttu-id="550a7-129">Onglet dans l’en-tête d’une conversation de groupe entre un ensemble d’utilisateurs dans le cadre d’une réunion programmée.</span><span class="sxs-lookup"><span data-stu-id="550a7-129">A tab in the header of a group chat between a set of users in the context of a scheduled meeting.</span></span> |
| <span data-ttu-id="550a7-130">**meetingDetailsTab**</span><span class="sxs-lookup"><span data-stu-id="550a7-130">**meetingDetailsTab**</span></span> | <span data-ttu-id="550a7-131">Onglet dans l’en-tête de l’affichage Détails de la réunion du calendrier.</span><span class="sxs-lookup"><span data-stu-id="550a7-131">A tab in the header of the meeting details view of the calendar.</span></span> |
| <span data-ttu-id="550a7-132">**meetingSidePanel**</span><span class="sxs-lookup"><span data-stu-id="550a7-132">**meetingSidePanel**</span></span> | <span data-ttu-id="550a7-133">Panneau en réunion ouvert via la barre unifiée (barre U).</span><span class="sxs-lookup"><span data-stu-id="550a7-133">An in-meeting panel opened through the unified bar (U-bar).</span></span> |
| <span data-ttu-id="550a7-134">**meetingStage**</span><span class="sxs-lookup"><span data-stu-id="550a7-134">**meetingStage**</span></span> | <span data-ttu-id="550a7-135">Une application de meetingSidePanel peut être partagée à l’étape de la réunion.</span><span class="sxs-lookup"><span data-stu-id="550a7-135">An app from the meetingSidePanel can be shared to the meeting stage.</span></span> |

> [!NOTE]
> <span data-ttu-id="550a7-136">`Context` n’est actuellement pas prise en charge sur les clients mobiles.</span><span class="sxs-lookup"><span data-stu-id="550a7-136">`Context` property is currently not supported on mobile clients.</span></span>

<span data-ttu-id="550a7-137">Après avoir activé votre application pour Teams réunions, vous devez configurer votre application avant une réunion, pendant une réunion et après une réunion.</span><span class="sxs-lookup"><span data-stu-id="550a7-137">After you enable your app for Teams meetings, you must configure your app before a meeting, during a meeting, and after a meeting.</span></span>

## <a name="configure-your-app-for-meeting-scenarios"></a><span data-ttu-id="550a7-138">Configurer votre application pour les scénarios de réunion</span><span class="sxs-lookup"><span data-stu-id="550a7-138">Configure your app for meeting scenarios</span></span>

> [!NOTE]
> * <span data-ttu-id="550a7-139">Pour que votre application soit visible dans la galerie d’onglets, elle doit prendre en charge les onglets configurables et l’étendue de conversation de groupe.</span><span class="sxs-lookup"><span data-stu-id="550a7-139">For your app to be visible in the tab gallery, it must support configurable tabs and the group chat scope.</span></span>
> * <span data-ttu-id="550a7-140">Les clients mobiles ne supportent les onglets qu’aux étapes préalables et post-réunion.</span><span class="sxs-lookup"><span data-stu-id="550a7-140">Mobile clients support tabs only in pre and post meeting stages.</span></span>
> * <span data-ttu-id="550a7-141">Les expériences en réunion qui sont des boîtes de dialogue et des onglets en réunion ne sont actuellement pas pris en charge sur les clients mobiles.</span><span class="sxs-lookup"><span data-stu-id="550a7-141">The in-meeting experiences that is in-meeting dialog box and tab is currently not supported on mobile clients.</span></span> <span data-ttu-id="550a7-142">Pour plus d’informations, [consultez des conseils pour les onglets mobiles](../tabs/design/tabs-mobile.md) lors de la création de vos onglets pour appareils mobiles.</span><span class="sxs-lookup"><span data-stu-id="550a7-142">For more information, see [guidance for tabs on mobile](../tabs/design/tabs-mobile.md) while creating your tabs for mobile.</span></span>

<span data-ttu-id="550a7-143">Teams réunions fournit une expérience de collaboration unique pour votre organisation.</span><span class="sxs-lookup"><span data-stu-id="550a7-143">Teams meetings provides a unique collaborative experience for your organization.</span></span> <span data-ttu-id="550a7-144">Il permet de configurer votre application pour différents scénarios de réunion.</span><span class="sxs-lookup"><span data-stu-id="550a7-144">It provides the opportunity to configure your app for different meeting scenarios.</span></span> <span data-ttu-id="550a7-145">Vous pouvez configurer vos applications pour améliorer l’expérience de réunion en fonction du rôle de participant ou du type d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="550a7-145">You can configure your apps to enhance the meeting experience based on participant role or user type.</span></span> <span data-ttu-id="550a7-146">Vous pouvez maintenant identifier les actions qui peuvent être prises dans les scénarios de réunion suivants :</span><span class="sxs-lookup"><span data-stu-id="550a7-146">Now you can identify what actions can be taken in the following meeting scenarios:</span></span>
* [<span data-ttu-id="550a7-147">Avant la réunion</span><span class="sxs-lookup"><span data-stu-id="550a7-147">Pre-meeting</span></span>](#pre-meeting)
* [<span data-ttu-id="550a7-148">En réunion</span><span class="sxs-lookup"><span data-stu-id="550a7-148">In-meeting</span></span>](#in-meeting)
* [<span data-ttu-id="550a7-149">Après la réunion</span><span class="sxs-lookup"><span data-stu-id="550a7-149">Post-meeting</span></span>](#post-meeting)

### <a name="pre-meeting"></a><span data-ttu-id="550a7-150">Avant la réunion</span><span class="sxs-lookup"><span data-stu-id="550a7-150">Pre-meeting</span></span>

<span data-ttu-id="550a7-151">Avant une réunion, les utilisateurs peuvent ajouter des onglets, des bots et des extensions de messagerie.</span><span class="sxs-lookup"><span data-stu-id="550a7-151">Before a meeting, users can add tabs, bots, and messaging extensions.</span></span> <span data-ttu-id="550a7-152">Les utilisateurs ayant des rôles d’organisateur et de présentateur peuvent ajouter des onglets à une réunion.</span><span class="sxs-lookup"><span data-stu-id="550a7-152">Users with organizer and presenter roles can add tabs to a meeting.</span></span>

<span data-ttu-id="550a7-153">**Pour ajouter un onglet à une réunion**</span><span class="sxs-lookup"><span data-stu-id="550a7-153">**To add a tab to a meeting**</span></span>

1. <span data-ttu-id="550a7-154">Dans votre calendrier, sélectionnez une réunion à laquelle vous souhaitez ajouter un onglet.</span><span class="sxs-lookup"><span data-stu-id="550a7-154">In your calendar, select a meeting to which you want to add a tab.</span></span>
1. <span data-ttu-id="550a7-155">Sélectionnez **l’onglet Détails** et sélectionnez</span><span class="sxs-lookup"><span data-stu-id="550a7-155">Select the **Details** tab and select</span></span> <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/><span data-ttu-id="550a7-156">.</span><span class="sxs-lookup"><span data-stu-id="550a7-156">.</span></span>

    ![Expérience préalable à la réunion](../assets/images/apps-in-meetings/PreMeeting.png)

1. <span data-ttu-id="550a7-158">Dans la galerie d’onglets qui s’affiche, sélectionnez l’application à ajouter et suivez les étapes nécessaires.</span><span class="sxs-lookup"><span data-stu-id="550a7-158">In the tab gallery that appears, select the app that you want to add and follow the steps as required.</span></span> <span data-ttu-id="550a7-159">L’application est installée en tant qu’onglet.</span><span class="sxs-lookup"><span data-stu-id="550a7-159">The app is installed as a tab.</span></span>

    > [!NOTE]
    > <span data-ttu-id="550a7-160">Actuellement, dans l’onglet Réunions, l’obtention des détails de la réunion et des informations sur les participants n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="550a7-160">Currently, in meetings tab, getting meeting details and participant information is not supported.</span></span>

<span data-ttu-id="550a7-161">**Pour ajouter une extension de messagerie à une réunion**</span><span class="sxs-lookup"><span data-stu-id="550a7-161">**To add a messaging extension to a meeting**</span></span>

1. <span data-ttu-id="550a7-162">Sélectionnez les &#x25CF;&#x25CF;&#x25CF; situées dans la zone composer un message de la conversation.</span><span class="sxs-lookup"><span data-stu-id="550a7-162">Select the ellipses &#x25CF;&#x25CF;&#x25CF; located in the compose message area in the chat.</span></span>
1. <span data-ttu-id="550a7-163">Sélectionnez l’application à ajouter et suivez les étapes nécessaires.</span><span class="sxs-lookup"><span data-stu-id="550a7-163">Select the app that you want to add and follow the steps as required.</span></span> <span data-ttu-id="550a7-164">L’application est installée en tant qu’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="550a7-164">The app is installed as a messaging extension.</span></span>

<span data-ttu-id="550a7-165">**Pour ajouter un bot à une réunion**</span><span class="sxs-lookup"><span data-stu-id="550a7-165">**To add a bot to a meeting**</span></span>

<span data-ttu-id="550a7-166">Dans une conversation de réunion, entrez la **@** clé et sélectionnez **Obtenir des bots.**</span><span class="sxs-lookup"><span data-stu-id="550a7-166">In a meeting chat, enter the **@** key and select **Get bots**.</span></span>

> [!NOTE]
> * <span data-ttu-id="550a7-167">L’identité de l’utilisateur doit être confirmée à l’aide de [l' ssO Onglets.](../tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="550a7-167">The user identity must be confirmed using [Tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="550a7-168">Après l’authentification, l’application peut récupérer le rôle d’utilisateur à l’aide de `GetParticipant` l’API.</span><span class="sxs-lookup"><span data-stu-id="550a7-168">After authentication, the app can retrieve the user role using the `GetParticipant` API.</span></span>
> * <span data-ttu-id="550a7-169">En fonction du rôle utilisateur, l’application a la possibilité de fournir des expériences spécifiques au rôle.</span><span class="sxs-lookup"><span data-stu-id="550a7-169">Based on the user role, the app has the capability to provide role specific experiences.</span></span> <span data-ttu-id="550a7-170">Par exemple, une application de sondage permet uniquement aux organisateurs et aux présentateurs de créer un sondage.</span><span class="sxs-lookup"><span data-stu-id="550a7-170">For example, a polling app allows only organizers and presenters to create a new poll.</span></span>
> * <span data-ttu-id="550a7-171">Les attributions de rôle peuvent être modifiées pendant une réunion.</span><span class="sxs-lookup"><span data-stu-id="550a7-171">Role assignments can be changed while a meeting is in progress.</span></span> <span data-ttu-id="550a7-172">Pour plus d’informations, [voir les rôles dans une Teams réunion.](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)</span><span class="sxs-lookup"><span data-stu-id="550a7-172">For more information, see [roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span>

### <a name="in-meeting"></a><span data-ttu-id="550a7-173">En réunion</span><span class="sxs-lookup"><span data-stu-id="550a7-173">In-meeting</span></span>

<span data-ttu-id="550a7-174">Au cours d’une réunion, vous pouvez utiliser meetingSidePanel ou la boîte de dialogue en réunion pour créer des expériences uniques pour vos applications.</span><span class="sxs-lookup"><span data-stu-id="550a7-174">During a meeting, you can use the meetingSidePanel or the in-meeting dialog box to build unique experiences for your apps.</span></span>

#### <a name="meetingsidepanel"></a><span data-ttu-id="550a7-175">meetingSidePanel</span><span class="sxs-lookup"><span data-stu-id="550a7-175">meetingSidePanel</span></span>

<span data-ttu-id="550a7-176">Avec meetingSidePanel, vous pouvez personnaliser les expériences d’une réunion qui permettent aux organisateurs et aux présentateurs d’avoir différents ensembles d’affichages et d’actions.</span><span class="sxs-lookup"><span data-stu-id="550a7-176">With the meetingSidePanel, you can customize experiences in a meeting that enable organizers and presenters to have different set of views and actions.</span></span> <span data-ttu-id="550a7-177">Dans le manifeste de votre application, vous devez ajouter meetingSidePanel au tableau de contexte.</span><span class="sxs-lookup"><span data-stu-id="550a7-177">In your app manifest, you must add meetingSidePanel to the context array.</span></span> <span data-ttu-id="550a7-178">Dans la réunion et dans tous les scénarios, l’application est restituer dans un onglet de réunion de 320 pixels de largeur.</span><span class="sxs-lookup"><span data-stu-id="550a7-178">In the meeting and in all scenarios, the app is rendered in an in-meeting tab that is 320 pixels in width.</span></span> <span data-ttu-id="550a7-179">Pour plus d’informations, [voir l’interface FrameContext.](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="550a7-179">For more information, see [FrameContext interface](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true).</span></span>

<span data-ttu-id="550a7-180">Pour utiliser l’API pour router les demandes en `userContext` conséquence, voir Teams [SDK](../tabs/how-to/access-teams-context.md#user-context).</span><span class="sxs-lookup"><span data-stu-id="550a7-180">To use the `userContext` API to route requests accordingly, see [Teams SDK](../tabs/how-to/access-teams-context.md#user-context).</span></span> <span data-ttu-id="550a7-181">Pour plus d’informations, [Teams flux d’authentification pour les onglets.](../tabs/how-to/authentication/auth-flow-tab.md)</span><span class="sxs-lookup"><span data-stu-id="550a7-181">For more information, see [Teams authentication flow for tabs](../tabs/how-to/authentication/auth-flow-tab.md).</span></span> <span data-ttu-id="550a7-182">Le flux d’authentification pour les onglets est très similaire au flux d’authentification pour les sites web.</span><span class="sxs-lookup"><span data-stu-id="550a7-182">Authentication flow for tabs is very similar to the authentication flow for websites.</span></span> <span data-ttu-id="550a7-183">Par conséquent, les onglets peuvent utiliser OAuth 2.0 directement.</span><span class="sxs-lookup"><span data-stu-id="550a7-183">So tabs can use OAuth 2.0 directly.</span></span> <span data-ttu-id="550a7-184">Pour plus d’informations, voir Plateforme d’identités Microsoft flux de code d’autorisation [OAuth 2.0.](/azure/active-directory/develop/v2-oauth2-auth-code-flow)</span><span class="sxs-lookup"><span data-stu-id="550a7-184">For more information, see [Microsoft identity platform and OAuth 2.0 authorization code flow](/azure/active-directory/develop/v2-oauth2-auth-code-flow).</span></span>

<span data-ttu-id="550a7-185">L’extension de messagerie fonctionne comme prévu lorsqu’un utilisateur est dans un affichage en réunion et qu’il peut publier des cartes d’extension de message de composition.</span><span class="sxs-lookup"><span data-stu-id="550a7-185">Messaging extension works as expected when a user is in an in-meeting view, and the user can post compose message extension cards.</span></span> <span data-ttu-id="550a7-186">AppName en réunion est une boîte à outils qui indique le nom de l’application dans la barre U de la réunion.</span><span class="sxs-lookup"><span data-stu-id="550a7-186">AppName in-meeting is a tooltip that states the app name in-meeting U-bar.</span></span>

> [!NOTE]
> <span data-ttu-id="550a7-187">Utilisez la version 1.7.0 ou une version ultérieure du [SDK Teams,](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)car les versions antérieures ne prisent pas en charge le panneau latéral.</span><span class="sxs-lookup"><span data-stu-id="550a7-187">Use version 1.7.0 or higher of [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), as versions prior to it do not support the side panel.</span></span>

#### <a name="in-meeting-dialog-box"></a><span data-ttu-id="550a7-188">Boîte de dialogue En réunion</span><span class="sxs-lookup"><span data-stu-id="550a7-188">In-meeting dialog box</span></span>

<span data-ttu-id="550a7-189">La boîte de dialogue de réunion peut être utilisée pour impliquer les participants au cours de la réunion et collecter des informations ou des commentaires pendant la réunion.</span><span class="sxs-lookup"><span data-stu-id="550a7-189">The in-meeting dialog box can be used to engage participants during the meeting and collect information or feedback during the meeting.</span></span> <span data-ttu-id="550a7-190">Utilisez [`NotificationSignal`](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) l’API pour signaler qu’une notification de bulle doit être déclenchée.</span><span class="sxs-lookup"><span data-stu-id="550a7-190">Use the [`NotificationSignal`](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) API to signal that a bubble notification must be triggered.</span></span> <span data-ttu-id="550a7-191">Dans le cadre de la charge utile de demande de notification, incluez l’URL où le contenu à afficher est hébergé.</span><span class="sxs-lookup"><span data-stu-id="550a7-191">As part of the notification request payload, include the URL where the content to be shown is hosted.</span></span>

<span data-ttu-id="550a7-192">La boîte de dialogue en réunion ne doit pas utiliser le module de tâche.</span><span class="sxs-lookup"><span data-stu-id="550a7-192">In-meeting dialog must not use task module.</span></span> <span data-ttu-id="550a7-193">Le module de tâche n’est pas appelé dans une conversation de réunion.</span><span class="sxs-lookup"><span data-stu-id="550a7-193">Task module is not invoked in a meeting chat.</span></span> <span data-ttu-id="550a7-194">Une URL de ressource externe est utilisée pour afficher une bulle de contenu dans une réunion.</span><span class="sxs-lookup"><span data-stu-id="550a7-194">An external resource URL is used to display content bubble in a meeting.</span></span> <span data-ttu-id="550a7-195">Vous pouvez utiliser la `submitTask` méthode pour envoyer des données dans une conversation de réunion.</span><span class="sxs-lookup"><span data-stu-id="550a7-195">You can use the `submitTask` method to submit data in a meeting chat.</span></span>

> [!NOTE]
> * <span data-ttu-id="550a7-196">Vous devez appeler la [fonction submitTask()](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) pour ignorer automatiquement une fois qu’un utilisateur effectue une action dans l’affichage web.</span><span class="sxs-lookup"><span data-stu-id="550a7-196">You must invoke the [submitTask()](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) function to dismiss automatically after a user takes an action in the web view.</span></span> <span data-ttu-id="550a7-197">Il s’agit d’une condition requise pour la soumission d’application.</span><span class="sxs-lookup"><span data-stu-id="550a7-197">This is a requirement for app submission.</span></span> <span data-ttu-id="550a7-198">Pour plus d’informations, voir Teams module de [tâche du SDK.](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="550a7-198">For more information, see [Teams SDK task module](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).</span></span>
> * <span data-ttu-id="550a7-199">Si vous souhaitez que votre application prise en charge des utilisateurs anonymes, votre charge utile de demande d’appel initiale doit reposer sur les métadonnées de la demande dans l’objet, et non sur `from.id` `from` les `from.aadObjectId` métadonnées de la demande.</span><span class="sxs-lookup"><span data-stu-id="550a7-199">If you want your app to support anonymous users, your initial invoke request payload must rely on the `from.id` request metadata in the `from` object, not the `from.aadObjectId` request metadata.</span></span> <span data-ttu-id="550a7-200">`from.id`est l’ID d’utilisateur `from.aadObjectId` Azure Active Directory (AAD) de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="550a7-200">`from.id` is the user ID and `from.aadObjectId` is the Azure Active Directory (AAD) ID of the user.</span></span> <span data-ttu-id="550a7-201">Pour plus d’informations, voir [l’utilisation de modules de tâche](../task-modules-and-cards/task-modules/task-modules-tabs.md) dans les onglets [et créer et envoyer le module de tâche.](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)</span><span class="sxs-lookup"><span data-stu-id="550a7-201">For more information, see [using task modules in tabs](../task-modules-and-cards/task-modules/task-modules-tabs.md) and [create and send the task module](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).</span></span>

#### <a name="share-to-stage"></a><span data-ttu-id="550a7-202">Partager pour mettre en scène</span><span class="sxs-lookup"><span data-stu-id="550a7-202">Share to stage</span></span>

> [!NOTE]
> * <span data-ttu-id="550a7-203">Cette fonctionnalité est actuellement disponible en [prévisualisation pour les](../resources/dev-preview/developer-preview-intro.md) développeurs uniquement.</span><span class="sxs-lookup"><span data-stu-id="550a7-203">This capability is currently available in [developer preview](../resources/dev-preview/developer-preview-intro.md) only.</span></span>
> * <span data-ttu-id="550a7-204">Pour utiliser cette fonctionnalité, l’application doit prendre en charge un meetingSidePanel en réunion.</span><span class="sxs-lookup"><span data-stu-id="550a7-204">To use this feature, the app must support an in-meeting meetingSidePanel.</span></span>

<span data-ttu-id="550a7-205">Cette fonctionnalité permet aux développeurs de partager une application au stade de la réunion.</span><span class="sxs-lookup"><span data-stu-id="550a7-205">This capability gives developers the ability to share an app to the meeting stage.</span></span> <span data-ttu-id="550a7-206">En activant le partage à l’étape de la réunion, les participants à la réunion peuvent collaborer en temps réel.</span><span class="sxs-lookup"><span data-stu-id="550a7-206">By enabling share to the meeting stage, meeting participants can collaborate in real-time.</span></span>

<span data-ttu-id="550a7-207">Le contexte requis se trouve `meetingStage` dans le manifeste de l’application.</span><span class="sxs-lookup"><span data-stu-id="550a7-207">The required context is `meetingStage` in the app manifest.</span></span> <span data-ttu-id="550a7-208">Une condition préalable consiste à avoir le `meetingSidePanel` contexte.</span><span class="sxs-lookup"><span data-stu-id="550a7-208">A prerequisite for this is to have the `meetingSidePanel` context.</span></span> <span data-ttu-id="550a7-209">Cela active le **partage** dans meetingSidePanel.</span><span class="sxs-lookup"><span data-stu-id="550a7-209">This enables **Share** in the meetingSidePanel.</span></span>

![Partager des étapes pendant l’expérience de réunion](~/assets/images/apps-in-meetings/share_to_stage_during_meeting.png)

<span data-ttu-id="550a7-211">La modification de manifeste nécessaire pour activer cette fonctionnalité est la suivante :</span><span class="sxs-lookup"><span data-stu-id="550a7-211">The manifest change that is needed to enable this capability is as follows:</span></span>

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

### <a name="post-meeting"></a><span data-ttu-id="550a7-212">Après la réunion</span><span class="sxs-lookup"><span data-stu-id="550a7-212">Post-meeting</span></span>

<span data-ttu-id="550a7-213">Les configurations de post-réunion et de [pré-réunion](#pre-meeting) sont les mêmes.</span><span class="sxs-lookup"><span data-stu-id="550a7-213">The post-meeting and [pre-meeting](#pre-meeting) configurations are the same.</span></span>

## <a name="code-sample"></a><span data-ttu-id="550a7-214">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="550a7-214">Code sample</span></span>

|<span data-ttu-id="550a7-215">Exemple de nom</span><span class="sxs-lookup"><span data-stu-id="550a7-215">Sample name</span></span> | <span data-ttu-id="550a7-216">Description</span><span class="sxs-lookup"><span data-stu-id="550a7-216">Description</span></span> | <span data-ttu-id="550a7-217">Échantillon</span><span class="sxs-lookup"><span data-stu-id="550a7-217">Sample</span></span> |
|----------------|-----------------|--------------|----------------|-----------|
| <span data-ttu-id="550a7-218">Application de réunion</span><span class="sxs-lookup"><span data-stu-id="550a7-218">Meeting app</span></span> | <span data-ttu-id="550a7-219">Montre comment utiliser l’application Générateur de jetons de réunion pour demander un jeton, qui est généré séquentiellement afin que chaque participant ait une bonne opportunité d’interagir.</span><span class="sxs-lookup"><span data-stu-id="550a7-219">Demonstrates how to use the Meeting Token Generator app to request a token, which is generated sequentially so that each participant has a fair opportunity to interact.</span></span> <span data-ttu-id="550a7-220">Cela peut être utile dans des situations telles que les réunions scrum, les&sessions A, etc.</span><span class="sxs-lookup"><span data-stu-id="550a7-220">This can be useful in situations like scrum meetings, Q&A sessions, and so on.</span></span> | [<span data-ttu-id="550a7-221">View</span><span class="sxs-lookup"><span data-stu-id="550a7-221">View</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token) |

## <a name="see-also"></a><span data-ttu-id="550a7-222">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="550a7-222">See also</span></span>

* [<span data-ttu-id="550a7-223">Recommandations en matière de conception de boîte de dialogue en réunion</span><span class="sxs-lookup"><span data-stu-id="550a7-223">In-meeting dialog design guidelines</span></span>](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [<span data-ttu-id="550a7-224">Teams d’authentification pour les onglets</span><span class="sxs-lookup"><span data-stu-id="550a7-224">Teams authentication flow for tabs</span></span>](../tabs/how-to/authentication/auth-flow-tab.md)
