---
title: Utiliser Microsoft Graph pour autoriser l’installation proactive d’un bot et la messagerie dans Teams
description: Décrit la messagerie proactive dans Teams et comment implémenter.
localization_priority: Normal
author: akjo
ms.author: lajanuar
ms.topic: Overview
keywords: installation de conversation de messagerie proactive teams Graph
ms.openlocfilehash: 0f59a74cc24b7d80dd3afd4aa4369a47d56e4d59
ms.sourcegitcommit: a6253e89cb8c8c34d45b06e08c9668daeebc30a3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/06/2021
ms.locfileid: "53300304"
---
# <a name="proactive-installation-of-apps-using-graph-api-to-send-messages"></a><span data-ttu-id="5d5da-104">Installation proactive d’applications à l’aide de l’API Graph pour envoyer des messages</span><span class="sxs-lookup"><span data-stu-id="5d5da-104">Proactive installation of apps using Graph API to send messages</span></span>

>[!IMPORTANT]
> <span data-ttu-id="5d5da-105">Microsoft Graph et Microsoft Teams prévisualisations publiques sont disponibles pour un accès et des commentaires en avant-première.</span><span class="sxs-lookup"><span data-stu-id="5d5da-105">Microsoft Graph and Microsoft Teams public previews are available for early access and feedback.</span></span> <span data-ttu-id="5d5da-106">Bien que cette version ait fait l’objet de tests approfondis, elle n’est pas destinée à être mise en production.</span><span class="sxs-lookup"><span data-stu-id="5d5da-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

## <a name="proactive-messaging-in-teams"></a><span data-ttu-id="5d5da-107">Messagerie proactive dans Teams</span><span class="sxs-lookup"><span data-stu-id="5d5da-107">Proactive messaging in Teams</span></span>

<span data-ttu-id="5d5da-108">Les messages proactifs sont initiés par des bots pour démarrer des conversations avec un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5d5da-108">Proactive messages are initiated by bots to start conversations with a user.</span></span> <span data-ttu-id="5d5da-109">Ils servent de nombreuses fonctions, notamment l’envoi de messages de bienvenue, la conduite d’enquêtes ou d’sondages et la diffusion de notifications à l’échelle de l’organisation.</span><span class="sxs-lookup"><span data-stu-id="5d5da-109">They serve many purposes including sending welcome messages, conducting surveys or polls, and broadcasting organization-wide notifications.</span></span> <span data-ttu-id="5d5da-110">Les messages proactifs Teams peuvent être remis en tant que conversations **ad hoc** ou **basées sur des** boîtes de dialogue :</span><span class="sxs-lookup"><span data-stu-id="5d5da-110">Proactive messages in Teams can be delivered as either **ad-hoc** or **dialog-based** conversations:</span></span>

|<span data-ttu-id="5d5da-111">Type de message</span><span class="sxs-lookup"><span data-stu-id="5d5da-111">Message type</span></span> | <span data-ttu-id="5d5da-112">Description</span><span class="sxs-lookup"><span data-stu-id="5d5da-112">Description</span></span> |
|----------------|-------------- |
|<span data-ttu-id="5d5da-113">Message proactif ad hoc</span><span class="sxs-lookup"><span data-stu-id="5d5da-113">Ad-hoc proactive message</span></span>| <span data-ttu-id="5d5da-114">Le bot interjecte un message sans interrompre le flux de conversation.</span><span class="sxs-lookup"><span data-stu-id="5d5da-114">The bot interjects a message without interrupting the conversation flow.</span></span>|
|<span data-ttu-id="5d5da-115">Message proactif basé sur la boîte de dialogue</span><span class="sxs-lookup"><span data-stu-id="5d5da-115">Dialog-based proactive message</span></span> | <span data-ttu-id="5d5da-116">Le bot crée un thread de boîte de dialogue, prend le contrôle d’une conversation, remet le message proactif, ferme et renvoie le contrôle à la boîte de dialogue précédente.</span><span class="sxs-lookup"><span data-stu-id="5d5da-116">The bot creates a new dialog thread, takes control of a conversation, delivers the proactive message, closes, and returns control to the previous dialog.</span></span>|

## <a name="proactive-app-installation-in-teams"></a><span data-ttu-id="5d5da-117">Installation proactive de l’application dans Teams</span><span class="sxs-lookup"><span data-stu-id="5d5da-117">Proactive app installation in Teams</span></span>

<span data-ttu-id="5d5da-118">Pour que votre bot puisse envoyer un message de manière proactive à un utilisateur, il doit être installé en tant qu’application personnelle ou dans une équipe dont l’utilisateur est membre.</span><span class="sxs-lookup"><span data-stu-id="5d5da-118">Before your bot can proactively message a user, it must be installed either as a personal app or in a team where the user is a member.</span></span> <span data-ttu-id="5d5da-119">Parfois, vous devez envoyer un message de manière proactive aux utilisateurs qui n’ont pas installé votre application ou qui ont déjà interagi avec celle-là.</span><span class="sxs-lookup"><span data-stu-id="5d5da-119">At times, you need to proactively message users that have not installed or previously interacted with your app.</span></span> <span data-ttu-id="5d5da-120">Par exemple, la nécessité de transmettre des informations importantes à tous les membres de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="5d5da-120">For example, the need to message important information to everyone in your organization.</span></span> <span data-ttu-id="5d5da-121">Pour de tels scénarios, vous pouvez utiliser l’API Microsoft Graph pour installer votre bot de manière proactive pour vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="5d5da-121">For such scenarios, you can use the Microsoft Graph API to proactively install your bot for your users.</span></span>

## <a name="permissions"></a><span data-ttu-id="5d5da-122">Autorisations</span><span class="sxs-lookup"><span data-stu-id="5d5da-122">Permissions</span></span>

<span data-ttu-id="5d5da-123">Les autorisations de type de ressource [TeamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) de Microsoft Graph vous aident à gérer le cycle de vie d’installation de votre application pour toutes les étendues utilisateur (personnel) ou d’équipe (canal) au sein de la plateforme Microsoft Teams :</span><span class="sxs-lookup"><span data-stu-id="5d5da-123">Microsoft Graph [teamsAppInstallation resource type](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) permissions help you to manage your app's installation lifecycle for all user (personal) or team (channel) scopes within the Microsoft Teams platform:</span></span>

|<span data-ttu-id="5d5da-124">Autorisation de l’application</span><span class="sxs-lookup"><span data-stu-id="5d5da-124">Application permission</span></span> | <span data-ttu-id="5d5da-125">Description</span><span class="sxs-lookup"><span data-stu-id="5d5da-125">Description</span></span>|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|<span data-ttu-id="5d5da-126">Permet à une Teams de lire, d’installer, de mettre à niveau et de se désinstaller elle-même pour n’importe quel *utilisateur,* sans se connecter ou utiliser préalablement.</span><span class="sxs-lookup"><span data-stu-id="5d5da-126">Allows a Teams app to read, install, upgrade, and uninstall itself for any *user*, without prior sign in or use.</span></span>|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|<span data-ttu-id="5d5da-127">Permet à une Teams de lire, d’installer, de mettre à niveau et de se désinstaller elle-même dans n’importe quelle *équipe,* sans se connecter ou utiliser préalablement.</span><span class="sxs-lookup"><span data-stu-id="5d5da-127">Allows a Teams app to read, install, upgrade, and uninstall itself in any *team*, without prior sign in or use.</span></span>|

<span data-ttu-id="5d5da-128">Pour utiliser ces autorisations, vous devez ajouter une clé [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) à votre manifeste d’application avec les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="5d5da-128">To use these permissions, you must add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>

* <span data-ttu-id="5d5da-129">**id**: ID de votre Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="5d5da-129">**id**: Your Azure Active Directory (AAD) app ID.</span></span>
* <span data-ttu-id="5d5da-130">**ressource**: URL de ressource pour l’application.</span><span class="sxs-lookup"><span data-stu-id="5d5da-130">**resource**: The resource URL for the app.</span></span>

> [!NOTE]
>
> * <span data-ttu-id="5d5da-131">Votre bot nécessite des autorisations d’application et non des autorisations déléguées par l’utilisateur, car l’installation est pour d’autres utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="5d5da-131">Your bot requires application and not user delegated permissions because the installation is for others.</span></span>
>
> * <span data-ttu-id="5d5da-132">Un administrateur client AAD doit [explicitement accorder des autorisations à une application.](/graph/security-authorization#grant-permissions-to-an-application)</span><span class="sxs-lookup"><span data-stu-id="5d5da-132">An AAD tenant administrator must [explicitly grant permissions to an application](/graph/security-authorization#grant-permissions-to-an-application).</span></span> <span data-ttu-id="5d5da-133">Une fois les autorisations accordées à l’application, tous les membres du client AAD obtiennent les autorisations accordées.</span><span class="sxs-lookup"><span data-stu-id="5d5da-133">After the application is granted permissions, all members of the AAD tenant get the granted permissions.</span></span>

## <a name="enable-proactive-app-installation-and-messaging"></a><span data-ttu-id="5d5da-134">Activer l’installation proactive de l’application et la messagerie</span><span class="sxs-lookup"><span data-stu-id="5d5da-134">Enable proactive app installation and messaging</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5d5da-135">Microsoft Graph installer uniquement les applications publiées dans le magasin d’applications de votre organisation ou dans Teams store.</span><span class="sxs-lookup"><span data-stu-id="5d5da-135">Microsoft Graph can only install apps published to your organization's app store or the Teams store.</span></span>

### <a name="create-and-publish-your-proactive-messaging-bot-for-teams"></a><span data-ttu-id="5d5da-136">Créer et publier votre bot de messagerie proactive pour Teams</span><span class="sxs-lookup"><span data-stu-id="5d5da-136">Create and publish your proactive messaging bot for Teams</span></span>

<span data-ttu-id="5d5da-137">To get started, you need a [bot for Teams](../../bots/how-to/create-a-bot-for-teams.md) with proactive [messaging](../../concepts/bots/bot-conversations/bots-conv-proactive.md) capabilities that is in your [organization’s app store](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-your-org) or the Teams [store](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-the-teams-store).</span><span class="sxs-lookup"><span data-stu-id="5d5da-137">To get started, you need a [bot for Teams](../../bots/how-to/create-a-bot-for-teams.md) with [proactive messaging](../../concepts/bots/bot-conversations/bots-conv-proactive.md) capabilities that is in your [organization's app store](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-your-org) or the [Teams store](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-the-teams-store).</span></span>

> [!TIP]
> <span data-ttu-id="5d5da-138">Le modèle d’application [*Communicator*](../..//samples/app-templates.md#company-communicator) entreprise prêt pour la production autorise la diffusion de messagerie et constitue un bon début pour créer votre application de bot proactive.</span><span class="sxs-lookup"><span data-stu-id="5d5da-138">The production-ready [*Company Communicator*](../..//samples/app-templates.md#company-communicator) app template permits broadcast messaging and is a good start to build your proactive bot application.</span></span>

### <a name="get-the-teamsappid-for-your-app"></a><span data-ttu-id="5d5da-139">Obtenir les `teamsAppId` applications pour votre application</span><span class="sxs-lookup"><span data-stu-id="5d5da-139">Get the `teamsAppId` for your app</span></span>

<span data-ttu-id="5d5da-140">Vous pouvez récupérer les `teamsAppId` informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="5d5da-140">You can retrieve the `teamsAppId` in the following ways:</span></span>

* <span data-ttu-id="5d5da-141">À partir du catalogue d’applications de votre organisation :</span><span class="sxs-lookup"><span data-stu-id="5d5da-141">From your organization's app catalog:</span></span>

    <span data-ttu-id="5d5da-142">**Référence de la page Graph Microsoft :** type de ressource [teamsApp](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="5d5da-142">**Microsoft Graph page reference:** [teamsApp resource type](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span></span>

    <span data-ttu-id="5d5da-143">**Requête HTTP GET** :</span><span class="sxs-lookup"><span data-stu-id="5d5da-143">**HTTP GET** request:</span></span>

    ```http
        GET https://graph.microsoft.com/v1.0/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
    ```

    <span data-ttu-id="5d5da-144">La demande doit renvoyer un objet, qui est `teamsApp` l’ID d’application généré par le catalogue de `id` l’application.</span><span class="sxs-lookup"><span data-stu-id="5d5da-144">The request must return a `teamsApp` object `id`, which is the app's catalog generated app ID.</span></span> <span data-ttu-id="5d5da-145">Ceci est différent de l’ID que vous avez fourni dans votre manifeste Teams application :</span><span class="sxs-lookup"><span data-stu-id="5d5da-145">This is different from the ID that you provided in your Teams app manifest:</span></span>

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

* <span data-ttu-id="5d5da-146">Si votre application a déjà été téléchargée ou téléchargée de nouveau pour un utilisateur dans une étendue personnelle :</span><span class="sxs-lookup"><span data-stu-id="5d5da-146">If your app has already been uploaded or sideloaded for a user in personal scope:</span></span>

    <span data-ttu-id="5d5da-147">**Référence Graph page** microsoft : [liste des applications installées pour l’utilisateur](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="5d5da-147">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

    <span data-ttu-id="5d5da-148">**Requête HTTP GET** :</span><span class="sxs-lookup"><span data-stu-id="5d5da-148">**HTTP GET** request:</span></span>

    ```http
    GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
    ```

* <span data-ttu-id="5d5da-149">Si votre application a déjà été téléchargée ou téléchargée de nouveau pour un canal dans l’étendue de l’équipe :</span><span class="sxs-lookup"><span data-stu-id="5d5da-149">If your app has already been uploaded or sideloaded for a channel in team scope:</span></span>

    <span data-ttu-id="5d5da-150">**Référence de page Graph Microsoft : lister** [les applications en équipe](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="5d5da-150">**Microsoft Graph page reference:** [List apps in team](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

    <span data-ttu-id="5d5da-151">**Requête HTTP GET** :</span><span class="sxs-lookup"><span data-stu-id="5d5da-151">**HTTP GET** request:</span></span>

    ```http
    GET https://graph.microsoft.com/v1.0/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
    ```

    > [!TIP]
    > <span data-ttu-id="5d5da-152">Pour affiner la liste des résultats, vous pouvez filtrer n’importe quel champ de [**l’objet teamsApp.**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="5d5da-152">To narrow the list of results, you can filter any of the fields of the [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true) object.</span></span>

### <a name="determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a><span data-ttu-id="5d5da-153">Déterminer si votre bot est actuellement installé pour un destinataire de message</span><span class="sxs-lookup"><span data-stu-id="5d5da-153">Determine whether your bot is currently installed for a message recipient</span></span>

<span data-ttu-id="5d5da-154">Vous pouvez déterminer si votre bot est actuellement installé pour un destinataire de message comme suit :</span><span class="sxs-lookup"><span data-stu-id="5d5da-154">You can determine whether your bot is currently installed for a message recipient as follows:</span></span>

<span data-ttu-id="5d5da-155">**Référence Graph page** microsoft : [liste des applications installées pour l’utilisateur](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="5d5da-155">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="5d5da-156">**Requête HTTP GET** :</span><span class="sxs-lookup"><span data-stu-id="5d5da-156">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="5d5da-157">La requête renvoie :</span><span class="sxs-lookup"><span data-stu-id="5d5da-157">The request returns:</span></span>

* <span data-ttu-id="5d5da-158">Tableau vide si l’application n’est pas installée.</span><span class="sxs-lookup"><span data-stu-id="5d5da-158">An empty array if the app is not installed.</span></span>
* <span data-ttu-id="5d5da-159">Tableau avec un seul [objet teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) si l’application est installée.</span><span class="sxs-lookup"><span data-stu-id="5d5da-159">An array with a single [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) object if the app is installed.</span></span>

### <a name="install-your-app"></a><span data-ttu-id="5d5da-160">Installer votre application</span><span class="sxs-lookup"><span data-stu-id="5d5da-160">Install your app</span></span>

<span data-ttu-id="5d5da-161">Vous pouvez installer votre application comme suit :</span><span class="sxs-lookup"><span data-stu-id="5d5da-161">You can install your app as follows:</span></span>

<span data-ttu-id="5d5da-162">**Référence de page Graph Microsoft : installer** [l’application pour l’utilisateur](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="5d5da-162">**Microsoft Graph page reference:** [Install app for user](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="5d5da-163">**Requête HTTP POST** :</span><span class="sxs-lookup"><span data-stu-id="5d5da-163">**HTTP POST** request:</span></span>

```http
POST https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps
Content-Type: application/json

{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/v1.0/appCatalogs/teamsApps/{teamsAppId}"
}
```

<span data-ttu-id="5d5da-164">Si l’utilisateur a Microsoft Teams en cours d’exécution, l’installation de l’application se produit immédiatement.</span><span class="sxs-lookup"><span data-stu-id="5d5da-164">If the user has Microsoft Teams running, app installation occurs immediately.</span></span> <span data-ttu-id="5d5da-165">Un redémarrage peut être nécessaire pour afficher l’application installée.</span><span class="sxs-lookup"><span data-stu-id="5d5da-165">A restart may be required to view the installed app.</span></span>

### <a name="retrieve-the-conversation-chatid"></a><span data-ttu-id="5d5da-166">Récupérer la conversation `chatId`</span><span class="sxs-lookup"><span data-stu-id="5d5da-166">Retrieve the conversation `chatId`</span></span>

<span data-ttu-id="5d5da-167">Lorsque votre application est installée pour l’utilisateur, le bot reçoit une notification d’événement qui contient les informations nécessaires `conversationUpdate` [](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) pour envoyer le message proactif.</span><span class="sxs-lookup"><span data-stu-id="5d5da-167">When your app is installed for the user, the bot receives a `conversationUpdate` [event notification](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) that contains the necessary information to send the proactive message.</span></span>

<span data-ttu-id="5d5da-168">**Référence de la page Graph Microsoft : obtenir** une [conversation](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="5d5da-168">**Microsoft Graph page reference:** [Get chat](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)</span></span>

1. <span data-ttu-id="5d5da-169">Vous devez avoir votre `{teamsAppInstallationId}` application.</span><span class="sxs-lookup"><span data-stu-id="5d5da-169">You must have your app's `{teamsAppInstallationId}`.</span></span> <span data-ttu-id="5d5da-170">Si vous ne l’avez pas, utilisez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="5d5da-170">If you do not have it, use the following:</span></span>

    <span data-ttu-id="5d5da-171">**Requête HTTP GET** :</span><span class="sxs-lookup"><span data-stu-id="5d5da-171">**HTTP GET** request:</span></span>

    ```http
    GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
    ```

    <span data-ttu-id="5d5da-172">La **propriété id** de la réponse est le `teamsAppInstallationId` .</span><span class="sxs-lookup"><span data-stu-id="5d5da-172">The **id** property of the response is the `teamsAppInstallationId`.</span></span>

1. <span data-ttu-id="5d5da-173">Faites la demande suivante pour extraire le `chatId` :</span><span class="sxs-lookup"><span data-stu-id="5d5da-173">Make the following request to fetch the `chatId`:</span></span>

    <span data-ttu-id="5d5da-174">**Requête HTTP GET** (autorisation — `TeamsAppInstallation.ReadWriteSelfForUser.All` ) :</span><span class="sxs-lookup"><span data-stu-id="5d5da-174">**HTTP GET** request (permission — `TeamsAppInstallation.ReadWriteSelfForUser.All`):</span></span>  

    ```http
    GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
    ```

    <span data-ttu-id="5d5da-175">La **propriété id** de la réponse est le `chatId` .</span><span class="sxs-lookup"><span data-stu-id="5d5da-175">The **id** property of the response is the `chatId`.</span></span>

    <span data-ttu-id="5d5da-176">Vous pouvez également récupérer la `chatId` requête avec la requête suivante, mais elle requiert l’autorisation plus large `Chat.Read.All` :</span><span class="sxs-lookup"><span data-stu-id="5d5da-176">You can also retrieve the `chatId` with the following request but it requires the broader `Chat.Read.All` permission:</span></span>

    <span data-ttu-id="5d5da-177">**Requête HTTP GET** (autorisation — `Chat.Read.All` ) :</span><span class="sxs-lookup"><span data-stu-id="5d5da-177">**HTTP GET** request (permission — `Chat.Read.All`):</span></span>

    ```http
    GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
    ```

### <a name="send-proactive-messages"></a><span data-ttu-id="5d5da-178">Envoyer des messages proactifs</span><span class="sxs-lookup"><span data-stu-id="5d5da-178">Send proactive messages</span></span>

<span data-ttu-id="5d5da-179">Votre bot peut [envoyer des messages proactifs](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) une fois qu’il a été ajouté pour un utilisateur ou une équipe et qu’il a reçu toutes les informations utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5d5da-179">Your bot can [send proactive messages](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) after the bot has been added for a user or a team, and has received all the user information.</span></span>

## <a name="code-sample"></a><span data-ttu-id="5d5da-180">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="5d5da-180">Code sample</span></span>

| <span data-ttu-id="5d5da-181">**Exemple de nom**</span><span class="sxs-lookup"><span data-stu-id="5d5da-181">**Sample Name**</span></span> | <span data-ttu-id="5d5da-182">**Description**</span><span class="sxs-lookup"><span data-stu-id="5d5da-182">**Description**</span></span> | <span data-ttu-id="5d5da-183">**.NET**</span><span class="sxs-lookup"><span data-stu-id="5d5da-183">**.NET**</span></span> | <span data-ttu-id="5d5da-184">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="5d5da-184">**Node.js**</span></span> |
|---------------|--------------|--------|-------------|--------|
| <span data-ttu-id="5d5da-185">Installation proactive de l’application et envoi de notifications proactives</span><span class="sxs-lookup"><span data-stu-id="5d5da-185">Proactive installation of app and sending proactive notifications</span></span> | <span data-ttu-id="5d5da-186">Cet exemple montre comment utiliser l’installation proactive de l’application pour les utilisateurs et envoyer des notifications proactives en appelant les API Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="5d5da-186">This sample shows how you can use proactive installation of app for users and send proactive notifications by calling Microsoft Graph APIs.</span></span> | [<span data-ttu-id="5d5da-187">View</span><span class="sxs-lookup"><span data-stu-id="5d5da-187">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-proactive-installation/csharp) | [<span data-ttu-id="5d5da-188">View</span><span class="sxs-lookup"><span data-stu-id="5d5da-188">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-proactive-installation/nodejs) |

## <a name="see-also"></a><span data-ttu-id="5d5da-189">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="5d5da-189">See also</span></span>

* [<span data-ttu-id="5d5da-190">**Gérer les stratégies de configuration d’application dans Microsoft Teams**</span><span class="sxs-lookup"><span data-stu-id="5d5da-190">**Manage app setup policies in Microsoft Teams**</span></span>](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)
* [<span data-ttu-id="5d5da-191">Envoyer des notifications proactives aux utilisateurs SDK v4</span><span class="sxs-lookup"><span data-stu-id="5d5da-191">Send proactive notifications to users SDK v4</span></span>](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)

## <a name="additional-code-samples"></a><span data-ttu-id="5d5da-192">Exemples de code supplémentaires</span><span class="sxs-lookup"><span data-stu-id="5d5da-192">Additional code samples</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="5d5da-193">**Teams exemples de code de messagerie proactifs**</span><span class="sxs-lookup"><span data-stu-id="5d5da-193">**Teams proactive messaging code samples**</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-proactive-messaging/csharp)
