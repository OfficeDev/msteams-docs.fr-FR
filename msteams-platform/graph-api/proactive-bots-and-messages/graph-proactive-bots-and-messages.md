---
title: Utiliser Microsoft Graph pour autoriser l'installation proactive d'un bot et la messagerie dans Teams
description: Décrit la messagerie proactive dans Teams et comment implémenter.
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: équipes d'installation de conversation de messagerie proactive Graph
ms.openlocfilehash: 62974f6f3b26e53558658f0b6cfda815dee1de8a
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101799"
---
# <a name="proactive-installation-of-apps-using-graph-api-and-send-messages"></a><span data-ttu-id="e2fff-104">Installation proactive d’applications à l’aide de l’API Graph et envoi de messages</span><span class="sxs-lookup"><span data-stu-id="e2fff-104">Proactive installation of apps using Graph API and send messages</span></span>

>[!IMPORTANT]
> <span data-ttu-id="e2fff-105">Microsoft Graph et Microsoft Teams prévisualisations publiques sont disponibles pour un accès et des commentaires en avant-première.</span><span class="sxs-lookup"><span data-stu-id="e2fff-105">Microsoft Graph and Microsoft Teams public previews are available for early access and feedback.</span></span> <span data-ttu-id="e2fff-106">Bien que cette version ait fait l'objet de tests approfondis, elle n'est pas destinée à être mise en production.</span><span class="sxs-lookup"><span data-stu-id="e2fff-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

## <a name="proactive-messaging-in-teams"></a><span data-ttu-id="e2fff-107">Messagerie proactive dans Teams</span><span class="sxs-lookup"><span data-stu-id="e2fff-107">Proactive messaging in Teams</span></span>

<span data-ttu-id="e2fff-108">Les messages proactifs sont initiés par des bots pour démarrer des conversations avec un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e2fff-108">Proactive messages are initiated by bots to start conversations with a user.</span></span> <span data-ttu-id="e2fff-109">Ils servent de nombreuses fonctions, notamment l'envoi de messages de bienvenue, la conduite d'enquêtes ou d'enquêtes et la diffusion de notifications à l'échelle de l'organisation.</span><span class="sxs-lookup"><span data-stu-id="e2fff-109">They serve many purposes including sending welcome messages, conducting surveys or polls, and broadcasting organization-wide notifications.</span></span> <span data-ttu-id="e2fff-110">Les messages proactifs Teams peuvent être remis en tant que conversations **ad hoc** ou basées **sur des** boîtes de dialogue :</span><span class="sxs-lookup"><span data-stu-id="e2fff-110">Proactive messages in Teams can be delivered as either **ad-hoc** or **dialog-based** conversations:</span></span>

|<span data-ttu-id="e2fff-111">Type de message</span><span class="sxs-lookup"><span data-stu-id="e2fff-111">Message Type</span></span> | <span data-ttu-id="e2fff-112">Description</span><span class="sxs-lookup"><span data-stu-id="e2fff-112">Description</span></span> |
|----------------|-------------- |
|<span data-ttu-id="e2fff-113">Message proactif ad hoc</span><span class="sxs-lookup"><span data-stu-id="e2fff-113">Ad-hoc proactive message</span></span>| <span data-ttu-id="e2fff-114">Le bot interjecte un message sans interrompre le flux de conversation.</span><span class="sxs-lookup"><span data-stu-id="e2fff-114">The bot interjects a message without interrupting the conversation flow.</span></span>|
|<span data-ttu-id="e2fff-115">Message proactif basé sur la boîte de dialogue</span><span class="sxs-lookup"><span data-stu-id="e2fff-115">Dialog-based proactive message</span></span> | <span data-ttu-id="e2fff-116">Le bot crée un thread de boîte de dialogue, prend le contrôle d'une conversation, remet le message proactif, ferme et renvoie le contrôle à la boîte de dialogue précédente.</span><span class="sxs-lookup"><span data-stu-id="e2fff-116">The bot creates a new dialog thread, takes control of a conversation, delivers the proactive message, closes, and returns control to the previous dialog.</span></span>|

<span data-ttu-id="e2fff-117">Voir, [Envoyer des notifications proactives aux utilisateurs SDK v4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="e2fff-117">See, [Send proactive notifications to users SDK v4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true).</span></span>

## <a name="proactive-app-installation-in-teams"></a><span data-ttu-id="e2fff-118">Installation proactive de l'application dans Teams</span><span class="sxs-lookup"><span data-stu-id="e2fff-118">Proactive app installation in Teams</span></span>

<span data-ttu-id="e2fff-119">Pour que votre bot puisse envoyer un message de manière proactive à un utilisateur, il doit être installé en tant qu'application personnelle ou dans une équipe dont l'utilisateur est membre.</span><span class="sxs-lookup"><span data-stu-id="e2fff-119">Before your bot can proactively message a user, it must be installed either as a personal app or in a team where the user is a member.</span></span> <span data-ttu-id="e2fff-120">Parfois, vous devez envoyer un message de manière proactive aux utilisateurs qui n'ont pas installé votre application ou qui ont déjà interagi avec celle-là.</span><span class="sxs-lookup"><span data-stu-id="e2fff-120">At times, you need to proactively message users that have not installed or previously interacted with your app.</span></span> <span data-ttu-id="e2fff-121">Par exemple, la nécessité de transmettre des informations vitales à tous les membres de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="e2fff-121">For example, the need to message vital information to everyone in your organization.</span></span> <span data-ttu-id="e2fff-122">Pour de tels scénarios, vous pouvez utiliser l'API Microsoft Graph pour installer votre bot de manière proactive pour vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="e2fff-122">For such scenarios, you can use the Microsoft Graph API to proactively install your bot for your users.</span></span>

## <a name="permissions"></a><span data-ttu-id="e2fff-123">Autorisations</span><span class="sxs-lookup"><span data-stu-id="e2fff-123">Permissions</span></span>

<span data-ttu-id="e2fff-124">Les autorisations de type de ressource Microsoft Graph [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) vous aident à gérer le cycle de vie d'installation de votre application pour toutes les étendues utilisateur (personnelle) ou d'équipe (canal) au sein de la plateforme Microsoft Teams :</span><span class="sxs-lookup"><span data-stu-id="e2fff-124">Microsoft Graph [teamsAppInstallation resource type](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) permissions helps you to manage your app's installation lifecycle for all user (personal) or team (channel) scopes within the Microsoft Teams platform:</span></span>

|<span data-ttu-id="e2fff-125">Autorisation de l’application</span><span class="sxs-lookup"><span data-stu-id="e2fff-125">Application permission</span></span> | <span data-ttu-id="e2fff-126">Description</span><span class="sxs-lookup"><span data-stu-id="e2fff-126">Description</span></span>|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|<span data-ttu-id="e2fff-127">Permet à une application Teams de lire, d'installer, de mettre à niveau et de se désinstaller elle-même pour n'importe quel **utilisateur,** sans se connecter ou utiliser préalablement.</span><span class="sxs-lookup"><span data-stu-id="e2fff-127">Allows a Teams app to read, install, upgrade, and uninstall itself for any **user**, without prior sign in or use.</span></span>|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|<span data-ttu-id="e2fff-128">Permet à une Teams de lire, d'installer, de mettre à niveau et de se désinstaller elle-même dans n'importe quelle **équipe,** sans se connecter ou utiliser préalablement.</span><span class="sxs-lookup"><span data-stu-id="e2fff-128">Allows a Teams app to read, install, upgrade, and uninstall itself in any **team**, without prior sign in or use.</span></span>|

<span data-ttu-id="e2fff-129">Pour utiliser ces autorisations, vous devez ajouter une clé [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) à votre manifeste d'application avec les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="e2fff-129">To use these permissions, you must add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>
> [!div class="checklist"]
> [!div class="checklist"]
>
> * <span data-ttu-id="e2fff-130">**id** : votre ID d'application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e2fff-130">**id** — your Azure AD app ID.</span></span>
> * <span data-ttu-id="e2fff-131">**ressource** : URL de ressource pour l'application.</span><span class="sxs-lookup"><span data-stu-id="e2fff-131">**resource** — the resource URL for the app.</span></span>
>
>[!NOTE]
>
> * <span data-ttu-id="e2fff-132">Votre bot nécessite des autorisations d'application et non des autorisations déléguées par l'utilisateur, car l'installation est pour d'autres utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="e2fff-132">Your bot requires application and not user delegated permissions because the installation is for others.</span></span>
>
> * <span data-ttu-id="e2fff-133">Un administrateur client Azure AD doit explicitement [accorder des autorisations à une application.](/graph/security-authorization#grant-permissions-to-an-application)</span><span class="sxs-lookup"><span data-stu-id="e2fff-133">An Azure AD tenant administrator must [explicitly grant permissions to an application](/graph/security-authorization#grant-permissions-to-an-application).</span></span> <span data-ttu-id="e2fff-134">Une fois qu'une application a reçu des autorisations, tous les membres du client Azure AD ont les autorisations accordées.</span><span class="sxs-lookup"><span data-stu-id="e2fff-134">After an application is granted permissions, all members of the Azure AD tenant gain the granted permissions.</span></span>

## <a name="enable-proactive-app-installation-and-messaging"></a><span data-ttu-id="e2fff-135">Activer l'installation proactive de l'application et la messagerie</span><span class="sxs-lookup"><span data-stu-id="e2fff-135">Enable proactive app installation and messaging</span></span>

> [!IMPORTANT]
><span data-ttu-id="e2fff-136">Microsoft Graph installer uniquement les applications publiées dans le magasin d'applications de votre organisation ou le Teams store.</span><span class="sxs-lookup"><span data-stu-id="e2fff-136">Microsoft Graph can only install apps published to your organization's app store or the Teams store.</span></span>

### <a name="-create-and-publish-your-proactive-messaging-bot-for-teams"></a><span data-ttu-id="e2fff-137">✔ créer et publier votre bot de messagerie proactive pour Teams</span><span class="sxs-lookup"><span data-stu-id="e2fff-137">✔ Create and publish your proactive messaging bot for Teams</span></span>

<span data-ttu-id="e2fff-138">To get started, you need a [bot for Teams](../../bots/how-to/create-a-bot-for-teams.md) with proactive [messaging](../../concepts/bots/bot-conversations/bots-conv-proactive.md) capabilities that's in your [organization's app store](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-your-org) or the Teams [store](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-the-teams-store).</span><span class="sxs-lookup"><span data-stu-id="e2fff-138">To get started, you need a [bot for Teams](../../bots/how-to/create-a-bot-for-teams.md) with [proactive messaging](../../concepts/bots/bot-conversations/bots-conv-proactive.md) capabilities that's in your [organization's app store](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-your-org) or the [Teams store](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-the-teams-store).</span></span>

>[!TIP]
> <span data-ttu-id="e2fff-139">Le modèle d'application Communicator entreprise prêt pour la production [**autorise**](../..//samples/app-templates.md#company-communicator) la diffusion de messages et constitue une bonne base pour la création de votre application de bot proactive.</span><span class="sxs-lookup"><span data-stu-id="e2fff-139">The production-ready [**Company Communicator**](../..//samples/app-templates.md#company-communicator) app template permits broadcast messaging and is a good foundation for building your proactive bot application.</span></span>

### <a name="-get-the-teamsappid-for-your-app"></a><span data-ttu-id="e2fff-140">✔ obtenir `teamsAppId` l'application</span><span class="sxs-lookup"><span data-stu-id="e2fff-140">✔ Get the `teamsAppId` for your app</span></span>

<span data-ttu-id="e2fff-141">**1. Vous** en avez besoin `teamsAppId` pour les étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="e2fff-141">**1.** You need the `teamsAppId` for the next steps.</span></span>

<span data-ttu-id="e2fff-142">Les `teamsAppId` données peuvent être récupérées à partir du catalogue d'applications de votre organisation :</span><span class="sxs-lookup"><span data-stu-id="e2fff-142">The `teamsAppId` can be retrieved from your organization's app catalog:</span></span>

<span data-ttu-id="e2fff-143">**Référence de la page Graph Microsoft :** type de ressource [teamsApp](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="e2fff-143">**Microsoft Graph page reference:** [teamsApp resource type](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span></span>

<span data-ttu-id="e2fff-144">**Requête HTTP GET** :</span><span class="sxs-lookup"><span data-stu-id="e2fff-144">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
```

<span data-ttu-id="e2fff-145">La demande doit renvoyer un `teamsApp` objet.</span><span class="sxs-lookup"><span data-stu-id="e2fff-145">The request must return a `teamsApp` object.</span></span> <span data-ttu-id="e2fff-146">L'objet renvoyé est l'ID d'application généré par le catalogue de l'application et est différent de l'ID que vous avez fourni dans `id` votre manifeste Teams'application :</span><span class="sxs-lookup"><span data-stu-id="e2fff-146">The returned object `id` is the app's catalog generated app ID and is different from the ID that you provided in your Teams app manifest:</span></span>

```json
{
  "value": [
    {
      "id": "b1c5353a-7aca-41b3-830f-27d5218fe0e5",
      "externalId": "f31b1263-ba99-435a-a679-911d24850d7c",
      "name": "Test App",
      "version": "1.0.1",
      "distributionMethod": "Organization"
    }
  ]
}
```

<span data-ttu-id="e2fff-147">**2.**  Si votre application a déjà été téléchargée ou téléchargée de manière secondaire pour un utilisateur dans l'étendue personnelle, vous pouvez récupérer les données `teamsAppId` suivantes :</span><span class="sxs-lookup"><span data-stu-id="e2fff-147">**2.**  If your app has already been uploaded or sideloaded for a user in the personal scope, you can retrieve the `teamsAppId` as follows:</span></span>

<span data-ttu-id="e2fff-148">**Référence Graph page** microsoft : [liste des applications installées pour l'utilisateur](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="e2fff-148">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="e2fff-149">**Requête HTTP GET** :</span><span class="sxs-lookup"><span data-stu-id="e2fff-149">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

<span data-ttu-id="e2fff-150">**3.** Si votre application a été téléchargée ou téléchargée de manière secondaire pour un canal dans l'étendue de l'équipe, vous pouvez récupérer les informations `teamsAppId` suivantes :</span><span class="sxs-lookup"><span data-stu-id="e2fff-150">**3.** If your app has been uploaded or sideloaded for a channel in the team scope, you can retrieve the `teamsAppId` as follows:</span></span>

<span data-ttu-id="e2fff-151">**Référence de page Graph Microsoft : lister** [les applications en équipe](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="e2fff-151">**Microsoft Graph page reference:** [List apps in team](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="e2fff-152">**Requête HTTP GET** :</span><span class="sxs-lookup"><span data-stu-id="e2fff-152">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

>[!TIP]
> <span data-ttu-id="e2fff-153">Pour affiner la liste des résultats, vous pouvez filtrer sur n'importe quel champ de [**l'objet teamsApp.**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="e2fff-153">To narrow the list of results, you can filter on any of the fields of [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true) object.</span></span>

### <a name="-determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a><span data-ttu-id="e2fff-154">✔ déterminer si votre bot est actuellement installé pour un destinataire de message</span><span class="sxs-lookup"><span data-stu-id="e2fff-154">✔ Determine whether your bot is currently installed for a message recipient</span></span>

<span data-ttu-id="e2fff-155">**Référence Graph page** microsoft : [liste des applications installées pour l'utilisateur](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="e2fff-155">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="e2fff-156">**Requête HTTP GET** :</span><span class="sxs-lookup"><span data-stu-id="e2fff-156">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="e2fff-157">Cette demande renvoie un tableau vide si l'application n'est pas installée et un tableau avec un seul objet [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) si l'application est installée.</span><span class="sxs-lookup"><span data-stu-id="e2fff-157">This request returns an empty array if the app is not installed and an array with a single [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) object if the app is installed.</span></span>

### <a name="-install-your-app"></a><span data-ttu-id="e2fff-158">✔ installer votre application</span><span class="sxs-lookup"><span data-stu-id="e2fff-158">✔ Install your app</span></span>

<span data-ttu-id="e2fff-159">**Référence de la page Graph Microsoft : installer** [l'application pour l'utilisateur](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="e2fff-159">**Microsoft Graph page reference:** [Install app for user](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="e2fff-160">**Requête HTTP POST** :</span><span class="sxs-lookup"><span data-stu-id="e2fff-160">**HTTP POST** request:</span></span>

```http
POST https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps
Content-Type: application/json

{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/v1.0/appCatalogs/teamsApps/{teamsAppId}"
}
```

<span data-ttu-id="e2fff-161">Si l'utilisateur a Microsoft Teams en cours d'exécution, l'installation de l'application s'exécute immédiatement.</span><span class="sxs-lookup"><span data-stu-id="e2fff-161">If the user has Microsoft Teams running, app installation is seen immediately.</span></span> <span data-ttu-id="e2fff-162">Un redémarrage peut être nécessaire pour afficher l'application installée.</span><span class="sxs-lookup"><span data-stu-id="e2fff-162">A restart may be required to view the installed app.</span></span>

### <a name="-retrieve-the-conversation-chatid"></a><span data-ttu-id="e2fff-163">✔ récupérer la conversation **chatId**</span><span class="sxs-lookup"><span data-stu-id="e2fff-163">✔ Retrieve the conversation **chatId**</span></span>

<span data-ttu-id="e2fff-164">Lorsque votre application est installée pour l'utilisateur, le bot reçoit une notification d'événement qui contient les informations nécessaires `conversationUpdate` [](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) pour envoyer le message proactif.</span><span class="sxs-lookup"><span data-stu-id="e2fff-164">When your app is installed for the user, the bot receives a `conversationUpdate` [event notification](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) that contains the necessary information to send the proactive message.</span></span>

<span data-ttu-id="e2fff-165">Les `chatId` données peuvent également être récupérées comme suit :</span><span class="sxs-lookup"><span data-stu-id="e2fff-165">The `chatId` can also be retrieved as follows:</span></span>

<span data-ttu-id="e2fff-166">**Référence de la page Graph Microsoft : obtenir** une [conversation](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="e2fff-166">**Microsoft Graph page reference:** [Get chat](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="e2fff-167">**1.** Vous devez avoir besoin de votre `{teamsAppInstallationId}` application.</span><span class="sxs-lookup"><span data-stu-id="e2fff-167">**1.** You must need your app's `{teamsAppInstallationId}`.</span></span> <span data-ttu-id="e2fff-168">Si vous ne l'avez pas, utilisez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="e2fff-168">If you don't have it, use the following:</span></span>

<span data-ttu-id="e2fff-169">**Requête HTTP GET** :</span><span class="sxs-lookup"><span data-stu-id="e2fff-169">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="e2fff-170">La **propriété id** de la réponse est le `teamsAppInstallationId` .</span><span class="sxs-lookup"><span data-stu-id="e2fff-170">The **id** property of the response is the `teamsAppInstallationId`.</span></span>

<span data-ttu-id="e2fff-171">**2. Faites** la demande suivante pour récupérer le `chatId` :</span><span class="sxs-lookup"><span data-stu-id="e2fff-171">**2.** Make the following request to fetch the `chatId`:</span></span>

<span data-ttu-id="e2fff-172">**Requête HTTP GET** (autorisation — `TeamsAppInstallation.ReadWriteSelfForUser.All` ) :</span><span class="sxs-lookup"><span data-stu-id="e2fff-172">**HTTP GET** request (permission — `TeamsAppInstallation.ReadWriteSelfForUser.All`):</span></span>  

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
```

<span data-ttu-id="e2fff-173">La **propriété id** de la réponse est le `chatId` .</span><span class="sxs-lookup"><span data-stu-id="e2fff-173">The **id** property of the response is the `chatId`.</span></span>

<span data-ttu-id="e2fff-174">Vous pouvez également récupérer la `chatId` requête avec la requête suivante, mais elle requiert l'autorisation plus large `Chat.Read.All` :</span><span class="sxs-lookup"><span data-stu-id="e2fff-174">You can also retrieve the `chatId` with the following request but it requires the broader `Chat.Read.All` permission:</span></span>

<span data-ttu-id="e2fff-175">**Requête HTTP GET** (autorisation — `Chat.Read.All` ) :</span><span class="sxs-lookup"><span data-stu-id="e2fff-175">**HTTP GET** request (permission — `Chat.Read.All`):</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
```

### <a name="-send-proactive-messages"></a><span data-ttu-id="e2fff-176">✔ messages proactifs</span><span class="sxs-lookup"><span data-stu-id="e2fff-176">✔ Send proactive messages</span></span>

<span data-ttu-id="e2fff-177">Votre bot peut [envoyer des messages proactifs](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) une fois qu'il a été ajouté pour un utilisateur ou une équipe et qu'il a reçu toutes les informations utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e2fff-177">Your bot can [send proactive messages](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) after the bot has been added for a user or a team and has received all the user information.</span></span>

## <a name="related-topic-for-teams-administrators"></a><span data-ttu-id="e2fff-178">Rubrique connexe pour les Teams administrateurs</span><span class="sxs-lookup"><span data-stu-id="e2fff-178">Related topic for Teams administrators</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="e2fff-179">**Gérer les stratégies de mise en application dans Teams**</span><span class="sxs-lookup"><span data-stu-id="e2fff-179">**Manage app setup policies in Microsoft Teams**</span></span>](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)

## <a name="view-additional-code-samples"></a><span data-ttu-id="e2fff-180">Afficher des exemples de code supplémentaires</span><span class="sxs-lookup"><span data-stu-id="e2fff-180">View additional code samples</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="e2fff-181">**Teams exemples de code de messagerie proactifs**</span><span class="sxs-lookup"><span data-stu-id="e2fff-181">**Teams proactive messaging code samples**</span></span>](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>
