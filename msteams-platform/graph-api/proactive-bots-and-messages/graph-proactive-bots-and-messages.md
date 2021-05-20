---
title: Utilisez Microsoft Graph autoriser l’installation proactive de bots et la messagerie dans Teams
description: Décrit les messages proactifs dans les Teams la façon de mettre en œuvre.
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: équipes proactives d’installation de chat de messagerie Graph
ms.openlocfilehash: 06b50e5ab8594c257959430383bab5e355af4e06
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566151"
---
# <a name="proactive-installation-of-apps-using-graph-api-and-send-messages"></a><span data-ttu-id="53a80-104">Installation proactive d’applications à l’aide de l’API Graph et envoi de messages</span><span class="sxs-lookup"><span data-stu-id="53a80-104">Proactive installation of apps using Graph API and send messages</span></span>

>[!IMPORTANT]
> <span data-ttu-id="53a80-105">Microsoft Graph et Microsoft Teams aperçus publics sont disponibles pour un accès précoce et des commentaires.</span><span class="sxs-lookup"><span data-stu-id="53a80-105">Microsoft Graph and Microsoft Teams public previews are available for early access and feedback.</span></span> <span data-ttu-id="53a80-106">Bien que cette version ait fait l’objet d’essais approfondis, elle n’est pas destinée à être utilisé en production.</span><span class="sxs-lookup"><span data-stu-id="53a80-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

## <a name="proactive-messaging-in-teams"></a><span data-ttu-id="53a80-107">Messagerie proactive en Teams</span><span class="sxs-lookup"><span data-stu-id="53a80-107">Proactive messaging in Teams</span></span>

<span data-ttu-id="53a80-108">Les messages proactifs sont initiés par des bots pour démarrer des conversations avec un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="53a80-108">Proactive messages are initiated by bots to start conversations with a user.</span></span> <span data-ttu-id="53a80-109">Ils servent à de nombreuses fins, y compris l’envoi de messages de bienvenue, la réalisation de sondages ou de sondages, et la diffusion de notifications à l’échelle de l’organisation.</span><span class="sxs-lookup"><span data-stu-id="53a80-109">They serve many purposes including sending welcome messages, conducting surveys or polls, and broadcasting organization-wide notifications.</span></span> <span data-ttu-id="53a80-110">Les messages proactifs Teams peuvent être transmis sous forme de conversations **ad hoc** **ou dialoguées** :</span><span class="sxs-lookup"><span data-stu-id="53a80-110">Proactive messages in Teams can be delivered as either **ad-hoc** or **dialog-based** conversations:</span></span>

|<span data-ttu-id="53a80-111">Type de message</span><span class="sxs-lookup"><span data-stu-id="53a80-111">Message Type</span></span> | <span data-ttu-id="53a80-112">Description</span><span class="sxs-lookup"><span data-stu-id="53a80-112">Description</span></span> |
|----------------|-------------- |
|<span data-ttu-id="53a80-113">Message proactif ad hoc</span><span class="sxs-lookup"><span data-stu-id="53a80-113">Ad-hoc proactive message</span></span>| <span data-ttu-id="53a80-114">Le bot interjecte un message sans interrompre le flux de conversation.</span><span class="sxs-lookup"><span data-stu-id="53a80-114">The bot interjects a message without interrupting the conversation flow.</span></span>|
|<span data-ttu-id="53a80-115">Message proactif basé sur le dialogue</span><span class="sxs-lookup"><span data-stu-id="53a80-115">Dialog-based proactive message</span></span> | <span data-ttu-id="53a80-116">Le bot crée un nouveau thread de dialogue, prend le contrôle d’une conversation, délivre le message proactif, ferme et renvoie le contrôle au dialogue précédent.</span><span class="sxs-lookup"><span data-stu-id="53a80-116">The bot creates a new dialog thread, takes control of a conversation, delivers the proactive message, closes, and returns control to the previous dialog.</span></span>|

## <a name="proactive-app-installation-in-teams"></a><span data-ttu-id="53a80-117">Installation proactive d’applications dans Teams</span><span class="sxs-lookup"><span data-stu-id="53a80-117">Proactive app installation in Teams</span></span>

<span data-ttu-id="53a80-118">Avant que votre bot puisse envoyer un message proactif à un utilisateur, il doit être installé soit comme une application personnelle, soit dans une équipe où l’utilisateur est membre.</span><span class="sxs-lookup"><span data-stu-id="53a80-118">Before your bot can proactively message a user, it must be installed either as a personal app or in a team where the user is a member.</span></span> <span data-ttu-id="53a80-119">Parfois, vous devez envoyer un message proactif aux utilisateurs qui n’ont pas installé ou interagi auparavant avec votre application.</span><span class="sxs-lookup"><span data-stu-id="53a80-119">At times, you need to proactively message users that have not installed or previously interacted with your app.</span></span> <span data-ttu-id="53a80-120">Par exemple, la nécessité de transmettre des informations vitales à tous les membres de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="53a80-120">For example, the need to message vital information to everyone in your organization.</span></span> <span data-ttu-id="53a80-121">Pour de tels scénarios, vous pouvez utiliser l’API Graph Microsoft pour installer proactivement votre bot pour vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="53a80-121">For such scenarios, you can use the Microsoft Graph API to proactively install your bot for your users.</span></span>

## <a name="permissions"></a><span data-ttu-id="53a80-122">Autorisations</span><span class="sxs-lookup"><span data-stu-id="53a80-122">Permissions</span></span>

<span data-ttu-id="53a80-123">Microsoft Graph les autorisations de [type ressources d’installation](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) d’Applications vous aident à gérer le cycle de vie d’installation de votre application pour toutes les étendues utilisateur (personnel) ou d’équipe (canal) dans la plate-forme Microsoft Teams :</span><span class="sxs-lookup"><span data-stu-id="53a80-123">Microsoft Graph [teamsAppInstallation resource type](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) permissions helps you to manage your app's installation lifecycle for all user (personal) or team (channel) scopes within the Microsoft Teams platform:</span></span>

|<span data-ttu-id="53a80-124">Autorisation de l’application</span><span class="sxs-lookup"><span data-stu-id="53a80-124">Application permission</span></span> | <span data-ttu-id="53a80-125">Description</span><span class="sxs-lookup"><span data-stu-id="53a80-125">Description</span></span>|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|<span data-ttu-id="53a80-126">Permet à une Teams de lire, installer, mettre à niveau et désinstaller pour tout **utilisateur,** sans se connecter ou utiliser préalablement.</span><span class="sxs-lookup"><span data-stu-id="53a80-126">Allows a Teams app to read, install, upgrade, and uninstall itself for any **user**, without prior sign in or use.</span></span>|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|<span data-ttu-id="53a80-127">Permet à une Teams de lire, installer, mettre à niveau et se désinstaller dans n’importe **quelle** équipe, sans se connecter ou utiliser préalablement.</span><span class="sxs-lookup"><span data-stu-id="53a80-127">Allows a Teams app to read, install, upgrade, and uninstall itself in any **team**, without prior sign in or use.</span></span>|

<span data-ttu-id="53a80-128">Pour utiliser ces autorisations, vous devez ajouter une [clé webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) à votre manifeste d’application avec les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="53a80-128">To use these permissions, you must add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>
> [!div class="checklist"]
> [!div class="checklist"]
>
> * <span data-ttu-id="53a80-129">**id** — votre identifiant d’application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="53a80-129">**id** — your Azure AD app ID.</span></span>
> * <span data-ttu-id="53a80-130">**ressource** — l’URL de ressources de l’application.</span><span class="sxs-lookup"><span data-stu-id="53a80-130">**resource** — the resource URL for the app.</span></span>
>
>[!NOTE]
>
> * <span data-ttu-id="53a80-131">Votre bot nécessite une application et non des autorisations déléguées par l’utilisateur parce que l’installation est pour d’autres.</span><span class="sxs-lookup"><span data-stu-id="53a80-131">Your bot requires application and not user delegated permissions because the installation is for others.</span></span>
>
> * <span data-ttu-id="53a80-132">Un administrateur locataire Azure AD doit [explicitement accorder des autorisations à une application](/graph/security-authorization#grant-permissions-to-an-application).</span><span class="sxs-lookup"><span data-stu-id="53a80-132">An Azure AD tenant administrator must [explicitly grant permissions to an application](/graph/security-authorization#grant-permissions-to-an-application).</span></span> <span data-ttu-id="53a80-133">Une fois qu’une demande est accordée, tous les membres du locataire Azure AD obtiennent les autorisations accordées.</span><span class="sxs-lookup"><span data-stu-id="53a80-133">After an application is granted permissions, all members of the Azure AD tenant gain the granted permissions.</span></span>

## <a name="enable-proactive-app-installation-and-messaging"></a><span data-ttu-id="53a80-134">Activer l’installation proactive d’applications et la messagerie</span><span class="sxs-lookup"><span data-stu-id="53a80-134">Enable proactive app installation and messaging</span></span>

> [!IMPORTANT]
><span data-ttu-id="53a80-135">Microsoft Graph pouvez installer uniquement des applications publiées sur l’App Store de votre organisation ou sur le Teams store.</span><span class="sxs-lookup"><span data-stu-id="53a80-135">Microsoft Graph can only install apps published to your organization's app store or the Teams store.</span></span>

### <a name="-create-and-publish-your-proactive-messaging-bot-for-teams"></a><span data-ttu-id="53a80-136">✔ créer et publier votre bot de messagerie proactif pour Teams</span><span class="sxs-lookup"><span data-stu-id="53a80-136">✔ Create and publish your proactive messaging bot for Teams</span></span>

<span data-ttu-id="53a80-137">Pour commencer, vous avez besoin [d’un bot pour Teams](../../bots/how-to/create-a-bot-for-teams.md) avec des capacités de messagerie [proactives](../../concepts/bots/bot-conversations/bots-conv-proactive.md) qui est dans [l’App Store de votre organisation](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-your-org) ou le magasin [Teams.](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-the-teams-store)</span><span class="sxs-lookup"><span data-stu-id="53a80-137">To get started, you need a [bot for Teams](../../bots/how-to/create-a-bot-for-teams.md) with [proactive messaging](../../concepts/bots/bot-conversations/bots-conv-proactive.md) capabilities that's in your [organization's app store](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-your-org) or the [Teams store](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-the-teams-store).</span></span>

>[!TIP]
> <span data-ttu-id="53a80-138">Le modèle d’application [**Communicator de l’entreprise**](../..//samples/app-templates.md#company-communicator) prêt à la production permet la diffusion de messages et est une bonne base pour la construction de votre application proactive bot.</span><span class="sxs-lookup"><span data-stu-id="53a80-138">The production-ready [**Company Communicator**](../..//samples/app-templates.md#company-communicator) app template permits broadcast messaging and is a good foundation for building your proactive bot application.</span></span>

### <a name="-get-the-teamsappid-for-your-app"></a><span data-ttu-id="53a80-139">✔ Obtenez le `teamsAppId` pour votre application</span><span class="sxs-lookup"><span data-stu-id="53a80-139">✔ Get the `teamsAppId` for your app</span></span>

<span data-ttu-id="53a80-140">**1. Vous** avez besoin `teamsAppId` de la pour les prochaines étapes.</span><span class="sxs-lookup"><span data-stu-id="53a80-140">**1.** You need the `teamsAppId` for the next steps.</span></span>

<span data-ttu-id="53a80-141">Le `teamsAppId` peut être récupéré à partir du catalogue d’applications de votre organisation :</span><span class="sxs-lookup"><span data-stu-id="53a80-141">The `teamsAppId` can be retrieved from your organization's app catalog:</span></span>

<span data-ttu-id="53a80-142">**Référence de Graph page Microsoft :** type de ressource [teamsApp](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="53a80-142">**Microsoft Graph page reference:** [teamsApp resource type](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span></span>

<span data-ttu-id="53a80-143">**HTTP GET** demande:</span><span class="sxs-lookup"><span data-stu-id="53a80-143">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
```

<span data-ttu-id="53a80-144">La demande doit retourner un `teamsApp` objet.</span><span class="sxs-lookup"><span data-stu-id="53a80-144">The request must return a `teamsApp` object.</span></span> <span data-ttu-id="53a80-145">L’objet retourné `id` est l’iD d’application généré par le catalogue de l’application et est différent de l’ID que vous avez fourni dans votre Teams manifeste de l’application :</span><span class="sxs-lookup"><span data-stu-id="53a80-145">The returned object `id` is the app's catalog generated app ID and is different from the ID that you provided in your Teams app manifest:</span></span>

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

<span data-ttu-id="53a80-146">**2.**  Si votre application a déjà été téléchargée ou déchargée latéralement pour un utilisateur dans le champ d’application personnel, vous pouvez récupérer les `teamsAppId` informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="53a80-146">**2.**  If your app has already been uploaded or sideloaded for a user in the personal scope, you can retrieve the `teamsAppId` as follows:</span></span>

<span data-ttu-id="53a80-147">**Référence de Graph page Microsoft : Liste des** applications [installées pour les utilisateurs](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="53a80-147">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="53a80-148">**HTTP GET** demande:</span><span class="sxs-lookup"><span data-stu-id="53a80-148">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

<span data-ttu-id="53a80-149">**3.** Si votre application a été téléchargée ou déchargée latéralement pour un canal dans la portée de l’équipe, vous pouvez récupérer les `teamsAppId` informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="53a80-149">**3.** If your app has been uploaded or sideloaded for a channel in the team scope, you can retrieve the `teamsAppId` as follows:</span></span>

<span data-ttu-id="53a80-150">**Référence de Graph page microsoft : Liste des** applications en [équipe](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="53a80-150">**Microsoft Graph page reference:** [List apps in team](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="53a80-151">**HTTP GET** demande:</span><span class="sxs-lookup"><span data-stu-id="53a80-151">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

>[!TIP]
> <span data-ttu-id="53a80-152">Pour affiner la liste des résultats, vous pouvez filtrer sur n’importe quel domaine de [**l’objet teamsApp.**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="53a80-152">To narrow the list of results, you can filter on any of the fields of [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true) object.</span></span>

### <a name="-determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a><span data-ttu-id="53a80-153">✔ déterminer si votre bot est actuellement installé pour un destinataire de message</span><span class="sxs-lookup"><span data-stu-id="53a80-153">✔ Determine whether your bot is currently installed for a message recipient</span></span>

<span data-ttu-id="53a80-154">**Référence de Graph page Microsoft : Liste des** applications [installées pour les utilisateurs](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="53a80-154">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="53a80-155">**HTTP GET** demande:</span><span class="sxs-lookup"><span data-stu-id="53a80-155">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="53a80-156">Cette demande renvoie un tableau vide si l’application n’est pas installée et un tableau avec un [seul objet teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) si l’application est installée.</span><span class="sxs-lookup"><span data-stu-id="53a80-156">This request returns an empty array if the app is not installed and an array with a single [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) object if the app is installed.</span></span>

### <a name="-install-your-app"></a><span data-ttu-id="53a80-157">✔ installez votre application</span><span class="sxs-lookup"><span data-stu-id="53a80-157">✔ Install your app</span></span>

<span data-ttu-id="53a80-158">**Référence de Graph page Microsoft : Installer une** application pour [l’utilisateur](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="53a80-158">**Microsoft Graph page reference:** [Install app for user](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="53a80-159">**DEMANDE HTTP POST:**</span><span class="sxs-lookup"><span data-stu-id="53a80-159">**HTTP POST** request:</span></span>

```http
POST https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps
Content-Type: application/json

{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/v1.0/appCatalogs/teamsApps/{teamsAppId}"
}
```

<span data-ttu-id="53a80-160">Si l’utilisateur a été Microsoft Teams, l’installation de l’application est vue immédiatement.</span><span class="sxs-lookup"><span data-stu-id="53a80-160">If the user has Microsoft Teams running, app installation is seen immediately.</span></span> <span data-ttu-id="53a80-161">Un redémarrage peut être nécessaire pour afficher l’application installée.</span><span class="sxs-lookup"><span data-stu-id="53a80-161">A restart may be required to view the installed app.</span></span>

### <a name="-retrieve-the-conversation-chatid"></a><span data-ttu-id="53a80-162">✔ récupérer la conversation **chatId**</span><span class="sxs-lookup"><span data-stu-id="53a80-162">✔ Retrieve the conversation **chatId**</span></span>

<span data-ttu-id="53a80-163">Lorsque votre application est installée pour l’utilisateur, le bot reçoit une `conversationUpdate` [notification d’événement](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) qui contient les informations nécessaires pour envoyer le message proactif.</span><span class="sxs-lookup"><span data-stu-id="53a80-163">When your app is installed for the user, the bot receives a `conversationUpdate` [event notification](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) that contains the necessary information to send the proactive message.</span></span>

<span data-ttu-id="53a80-164">Le `chatId` peut également être récupéré comme suit:</span><span class="sxs-lookup"><span data-stu-id="53a80-164">The `chatId` can also be retrieved as follows:</span></span>

<span data-ttu-id="53a80-165">**Référence de la page Graph Microsoft : Obtenez** le [chat](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="53a80-165">**Microsoft Graph page reference:** [Get chat](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="53a80-166">**1.** Vous devez avoir besoin de votre application `{teamsAppInstallationId}` .</span><span class="sxs-lookup"><span data-stu-id="53a80-166">**1.** You must need your app's `{teamsAppInstallationId}`.</span></span> <span data-ttu-id="53a80-167">Si vous ne l’avez pas, utilisez les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="53a80-167">If you don't have it, use the following:</span></span>

<span data-ttu-id="53a80-168">**HTTP GET** demande:</span><span class="sxs-lookup"><span data-stu-id="53a80-168">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="53a80-169">La **propriété id** de la réponse est le `teamsAppInstallationId` .</span><span class="sxs-lookup"><span data-stu-id="53a80-169">The **id** property of the response is the `teamsAppInstallationId`.</span></span>

<span data-ttu-id="53a80-170">**2.** Faites la demande suivante pour aller chercher les `chatId` :</span><span class="sxs-lookup"><span data-stu-id="53a80-170">**2.** Make the following request to fetch the `chatId`:</span></span>

<span data-ttu-id="53a80-171">**HTTP GET** demande (permission — `TeamsAppInstallation.ReadWriteSelfForUser.All` :</span><span class="sxs-lookup"><span data-stu-id="53a80-171">**HTTP GET** request (permission — `TeamsAppInstallation.ReadWriteSelfForUser.All`):</span></span>  

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
```

<span data-ttu-id="53a80-172">La **propriété id** de la réponse est le `chatId` .</span><span class="sxs-lookup"><span data-stu-id="53a80-172">The **id** property of the response is the `chatId`.</span></span>

<span data-ttu-id="53a80-173">Vous pouvez également récupérer le avec `chatId` la demande suivante, mais il nécessite l’autorisation plus `Chat.Read.All` large:</span><span class="sxs-lookup"><span data-stu-id="53a80-173">You can also retrieve the `chatId` with the following request but it requires the broader `Chat.Read.All` permission:</span></span>

<span data-ttu-id="53a80-174">**HTTP GET** demande (permission — `Chat.Read.All` :</span><span class="sxs-lookup"><span data-stu-id="53a80-174">**HTTP GET** request (permission — `Chat.Read.All`):</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
```

### <a name="-send-proactive-messages"></a><span data-ttu-id="53a80-175">✔ envoyer des messages proactifs</span><span class="sxs-lookup"><span data-stu-id="53a80-175">✔ Send proactive messages</span></span>

<span data-ttu-id="53a80-176">Votre bot peut [envoyer des messages proactifs](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) après l’ajout du bot pour un utilisateur ou une équipe et a reçu toutes les informations utilisateur.</span><span class="sxs-lookup"><span data-stu-id="53a80-176">Your bot can [send proactive messages](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) after the bot has been added for a user or a team and has received all the user information.</span></span>

## <a name="see-also"></a><span data-ttu-id="53a80-177">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="53a80-177">See also</span></span>

* [<span data-ttu-id="53a80-178">**Gérer les stratégies de mise en application dans Teams**</span><span class="sxs-lookup"><span data-stu-id="53a80-178">**Manage app setup policies in Microsoft Teams**</span></span>](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)
* [<span data-ttu-id="53a80-179">Envoyer des notifications proactives aux utilisateurs SDK v4</span><span class="sxs-lookup"><span data-stu-id="53a80-179">Send proactive notifications to users SDK v4</span></span>](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)

## <a name="view-additional-code-samples"></a><span data-ttu-id="53a80-180">Afficher des échantillons de code supplémentaires</span><span class="sxs-lookup"><span data-stu-id="53a80-180">View additional code samples</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="53a80-181">**Teams échantillons de code de messagerie proactifs**</span><span class="sxs-lookup"><span data-stu-id="53a80-181">**Teams proactive messaging code samples**</span></span>](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)