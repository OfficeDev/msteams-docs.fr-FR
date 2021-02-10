---
title: Utiliser Microsoft Graph pour activer l’installation proactive des bots et la messagerie dans Teams
description: Décrit la messagerie proactive dans Teams et la façon d’implémenter.
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: Graphe d’installation de conversation de messagerie proactive teams
ms.openlocfilehash: 4f26b4d2f4e82fcf50b7a35c46bcd07e5afecf19
ms.sourcegitcommit: b99ed616db734371e4af4594b7e895c5b05737c3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/09/2021
ms.locfileid: "50162893"
---
# <a name="enable-proactive-bot-installation-and-proactive-messaging-in-teams-with-microsoft-graph-public-preview"></a><span data-ttu-id="73386-104">Activer l’installation proactive du bot et la messagerie proactive dans Teams avec Microsoft Graph (prévisualisation publique)</span><span class="sxs-lookup"><span data-stu-id="73386-104">Enable proactive bot installation and proactive messaging in Teams with Microsoft Graph (Public Preview)</span></span>

>[!IMPORTANT]
> <span data-ttu-id="73386-105">Les prévisualisations publiques de Microsoft Graph et Microsoft Teams sont disponibles pour un accès et des commentaires en avant-première.</span><span class="sxs-lookup"><span data-stu-id="73386-105">Microsoft Graph and Microsoft Teams public previews are available for early-access and feedback.</span></span> <span data-ttu-id="73386-106">Bien que cette version ait fait l’objet de tests approfondis, elle n’est pas destinée à être mise en production.</span><span class="sxs-lookup"><span data-stu-id="73386-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

## <a name="proactive-messaging-in-teams"></a><span data-ttu-id="73386-107">Messagerie proactive dans Teams</span><span class="sxs-lookup"><span data-stu-id="73386-107">Proactive messaging in Teams</span></span>

<span data-ttu-id="73386-108">Les messages proactifs sont initiés par des bots pour démarrer des conversations avec un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="73386-108">Proactive messages are initiated by bots to start conversations with a user.</span></span> <span data-ttu-id="73386-109">Ils servent de nombreuses fonctions, notamment l’envoi de messages de bienvenue, la conduite d’enquêtes ou d’sondages et la diffusion de notifications à l’échelle de l’organisation.</span><span class="sxs-lookup"><span data-stu-id="73386-109">They serve many purposes including sending welcome messages, conducting surveys or polls, and broadcasting organization-wide notifications.</span></span>  <span data-ttu-id="73386-110">Les messages proactifs dans Teams peuvent être remis en tant que conversations **ad hoc** ou **basées sur des** boîtes de dialogue :</span><span class="sxs-lookup"><span data-stu-id="73386-110">Proactive messages in Teams can be delivered as either **ad-hoc** or **dialog-based** conversations:</span></span>

|<span data-ttu-id="73386-111">Type de message</span><span class="sxs-lookup"><span data-stu-id="73386-111">Message Type</span></span> | <span data-ttu-id="73386-112">Description</span><span class="sxs-lookup"><span data-stu-id="73386-112">Description</span></span> |
|----------------|-------------- |
|<span data-ttu-id="73386-113">Message proactif ad hoc</span><span class="sxs-lookup"><span data-stu-id="73386-113">Ad-hoc proactive message</span></span>| <span data-ttu-id="73386-114">Le bot interjecte un message sans interrompre le flux de conversation.</span><span class="sxs-lookup"><span data-stu-id="73386-114">The bot interjects a message without interrupting the conversation flow.</span></span>|
|<span data-ttu-id="73386-115">Message proactif basé sur la boîte de dialogue</span><span class="sxs-lookup"><span data-stu-id="73386-115">Dialog-based proactive message</span></span> | <span data-ttu-id="73386-116">Le bot crée un thread de boîte de dialogue, prend le contrôle d’une conversation, remet le message proactif, ferme et renvoie le contrôle à la boîte de dialogue précédente.</span><span class="sxs-lookup"><span data-stu-id="73386-116">The bot creates a new dialog thread, takes control of a conversation, delivers the proactive message, closes, and returns control to the previous dialog.</span></span>|

<span data-ttu-id="73386-117">*Voir*, [Envoyer des notifications proactives aux utilisateurs SDK v4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="73386-117">*See*, [Send proactive notifications to users SDK v4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)</span></span>

## <a name="proactive-app-installation-in-teams"></a><span data-ttu-id="73386-118">Installation proactive de l’application dans Teams</span><span class="sxs-lookup"><span data-stu-id="73386-118">Proactive app installation in Teams</span></span>

<span data-ttu-id="73386-119">Avant que votre bot puisse envoyer un message de manière proactive à un utilisateur, il doit être installé en tant qu’application personnelle ou dans une équipe dont l’utilisateur est membre.</span><span class="sxs-lookup"><span data-stu-id="73386-119">Before your bot can proactively message a user, it needs to be installed either as a personal app, or in a team where the user is a member.</span></span> <span data-ttu-id="73386-120">Parfois, vous devrez peut-être envoyer  un message de manière proactive aux utilisateurs qui n’ont pas installé votre application ou qui ont déjà interagi avec celle-là.</span><span class="sxs-lookup"><span data-stu-id="73386-120">At times,  you may need to proactively message users that have _not_ installed or previously interacted with your app.</span></span> <span data-ttu-id="73386-121">Par exemple, la nécessité de transmettre des informations vitales à tous les membres de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="73386-121">For instance, the need to message vital information to everyone in your organization.</span></span> <span data-ttu-id="73386-122">Pour de tels scénarios, vous pouvez utiliser l’API Microsoft Graph pour installer votre bot de manière proactive pour vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="73386-122">For such scenarios, you can use the Microsoft Graph API to proactively install your bot for your users.</span></span>

## <a name="permissions"></a><span data-ttu-id="73386-123">Autorisations</span><span class="sxs-lookup"><span data-stu-id="73386-123">Permissions</span></span>

<span data-ttu-id="73386-124">Les autorisations de type de ressource [TeamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) de Microsoft Graph vous permettent de gérer le cycle de vie d’installation de votre application pour toutes les étendues utilisateur (personnelles) ou d’équipe (canal) au sein de la plateforme Microsoft Teams :</span><span class="sxs-lookup"><span data-stu-id="73386-124">Microsoft Graph [teamsAppInstallation resource type](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) permissions allow you to manage your app's installation lifecycle for all user (personal) or team (channel) scopes within the Microsoft Teams platform:</span></span>

|<span data-ttu-id="73386-125">Autorisation de l’application</span><span class="sxs-lookup"><span data-stu-id="73386-125">Application permission</span></span> | <span data-ttu-id="73386-126">Description</span><span class="sxs-lookup"><span data-stu-id="73386-126">Description</span></span>|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|<span data-ttu-id="73386-127">Permet à une application Teams de lire, d’installer, de mettre à niveau et de se désinstaller elle-même pour n’importe quel **utilisateur,** sans se connecter ou utiliser préalablement.</span><span class="sxs-lookup"><span data-stu-id="73386-127">Allows a Teams app to read, install, upgrade, and uninstall itself for any **user**, without prior sign in or use.</span></span>|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|<span data-ttu-id="73386-128">Permet à une application Teams de lire, d’installer, de mettre à niveau et de se désinstaller elle-même dans n’importe quelle **équipe,** sans se connecter ou utiliser préalablement.</span><span class="sxs-lookup"><span data-stu-id="73386-128">Allows a Teams app to read, install, upgrade, and uninstall itself in any **team**, without prior sign in or use.</span></span>|

<span data-ttu-id="73386-129">Pour utiliser ces autorisations, vous devez ajouter une clé [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) à votre manifeste d’application avec les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="73386-129">To use these permissions, you must add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>
> [!div class="checklist"]
> [!div class="checklist"]
>
> * <span data-ttu-id="73386-130">**id**  : id de votre application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="73386-130">**id**  — your Azure AD app id.</span></span>
> * <span data-ttu-id="73386-131">**ressource** : URL de ressource pour l’application.</span><span class="sxs-lookup"><span data-stu-id="73386-131">**resource** — the resource URL for the app.</span></span>
>

>[!NOTE]
>
> * <span data-ttu-id="73386-132">Votre bot nécessite  des _autorisations déléguées_ par l’utilisateur, car l’installation n’est pas pour vous-même, mais pour d’autres utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="73386-132">Your bot requires _application_ not _user delegated_ permissions because the installation is not for yourself but for others.</span></span>
>
> * <span data-ttu-id="73386-133">Un administrateur client Azure AD doit explicitement [accorder des autorisations à une application.](/graph/security-authorization#grant-permissions-to-an-application)</span><span class="sxs-lookup"><span data-stu-id="73386-133">An Azure AD tenant administrator must [explicitly grant permissions to an application](/graph/security-authorization#grant-permissions-to-an-application).</span></span> <span data-ttu-id="73386-134">Une fois qu’une application  a reçu des autorisations, tous les membres du client Azure AD en auront les autorisations accordées.</span><span class="sxs-lookup"><span data-stu-id="73386-134">After an application is granted permissions, _all_ members of the Azure AD tenant will gain the granted permissions.</span></span>

## <a name="enable-proactive-app-installation-and-messaging"></a><span data-ttu-id="73386-135">Activer l’installation proactive de l’application et la messagerie</span><span class="sxs-lookup"><span data-stu-id="73386-135">Enable proactive app installation and messaging</span></span>

 > [!IMPORTANT]
><span data-ttu-id="73386-136">Microsoft Graph installe uniquement les applications publiées dans le catalogue d’applications de votre organisation [ou](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) dans [AppSource.](https://appsource.microsoft.com/)</span><span class="sxs-lookup"><span data-stu-id="73386-136">Microsoft Graph will only install apps published within your organization's [app catalog](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) or in [AppSource](https://appsource.microsoft.com/).</span></span>

### <a name="-create-and-publish-your-proactive-messaging-bot-for-teams"></a><span data-ttu-id="73386-137">✔ créer et publier votre bot de messagerie proactive pour Teams</span><span class="sxs-lookup"><span data-stu-id="73386-137">✔ Create and publish your proactive messaging bot for Teams</span></span>

<span data-ttu-id="73386-138">Pour commencer, vous aurez besoin d’un bot pour [](../../concepts/deploy-and-publish/overview.md) [Teams](../../bots/how-to/create-a-bot-for-teams.md) avec des [](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) fonctionnalités de messagerie [proactives](../../concepts/bots/bot-conversations/bots-conv-proactive.md) et publié dans le catalogue d’applications de votre organisation ou [dans AppSource.](https://appsource.microsoft.com/)</span><span class="sxs-lookup"><span data-stu-id="73386-138">To get started, you will need a [bot for Teams](../../bots/how-to/create-a-bot-for-teams.md) with [proactive messaging](../../concepts/bots/bot-conversations/bots-conv-proactive.md) capabilities and  [published](../../concepts/deploy-and-publish/overview.md) in your organization's [app catalog](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) or in [AppSource](https://appsource.microsoft.com/).</span></span>

>[!TIP]
> <span data-ttu-id="73386-139">Le modèle d’application Communicator entreprise prêt pour la production [**active**](../..//samples/app-templates.md#company-communicator) la messagerie de diffusion et constitue une bonne base pour la création de votre application de bot proactive.</span><span class="sxs-lookup"><span data-stu-id="73386-139">The production-ready [**Company Communicator**](../..//samples/app-templates.md#company-communicator) app template enables broadcast messaging and is a good foundation for building your proactive bot application.</span></span>

### <a name="-get-the-teamsappid-for-your-app"></a><span data-ttu-id="73386-140">✔ obtenir `teamsAppId` l’application</span><span class="sxs-lookup"><span data-stu-id="73386-140">✔ Get the `teamsAppId` for your app</span></span>

<span data-ttu-id="73386-141">**1.** Vous en aurez besoin `teamsAppId`  pour les étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="73386-141">**1.** You will need the `teamsAppId`  for the next steps.</span></span>

<span data-ttu-id="73386-142">Les `teamsAppId` données peuvent être récupérées à partir du catalogue d’applications de votre organisation :</span><span class="sxs-lookup"><span data-stu-id="73386-142">The `teamsAppId` can be retrieved from your organization's app catalog:</span></span>

<span data-ttu-id="73386-143">**Référence de page Microsoft Graph : type** de ressource [teamsApp](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="73386-143">**Microsoft Graph page reference:** [teamsApp resource type](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)</span></span>

<span data-ttu-id="73386-144">**Requête HTTP GET** :</span><span class="sxs-lookup"><span data-stu-id="73386-144">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
```

<span data-ttu-id="73386-145">La demande retourne un `teamsApp`  objet.</span><span class="sxs-lookup"><span data-stu-id="73386-145">The request will return a `teamsApp`  object.</span></span> <span data-ttu-id="73386-146">L’objet renvoyé est l’ID d’application généré par le catalogue de l’application et est différent de l'« id: » que vous avez fourni dans le manifeste de votre `id`  application Teams :</span><span class="sxs-lookup"><span data-stu-id="73386-146">The returned object's `id`  is the app's catalog generated app id and is different from the "id:" that you provided in your Teams app manifest:</span></span>

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

<span data-ttu-id="73386-147">**2.**  Si votre application a déjà été téléchargée ou téléchargée de manière secondaire pour un utilisateur dans l’étendue personnelle, vous pouvez récupérer les données `teamsAppId` suivantes :</span><span class="sxs-lookup"><span data-stu-id="73386-147">**2.**  If your app has already been uploaded or sideloaded for a user in the personal scope, you can retrieve the `teamsAppId` as follows:</span></span>

<span data-ttu-id="73386-148">**Référence de page Microsoft Graph : Liste** des applications [installées pour l’utilisateur](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="73386-148">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="73386-149">**Requête HTTP GET** :</span><span class="sxs-lookup"><span data-stu-id="73386-149">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

<span data-ttu-id="73386-150">**3.** Si votre application a déjà été téléchargée/téléchargée de manière secondaire pour un canal dans l’étendue de l’équipe, vous pouvez récupérer les données `teamsAppId` suivantes :</span><span class="sxs-lookup"><span data-stu-id="73386-150">**3.** If your app has already been uploaded/sideloaded for a channel in the team scope, you can retrieve the `teamsAppId` as follows:</span></span>

<span data-ttu-id="73386-151">**Référence de page Microsoft Graph : lister** [les applications en équipe](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="73386-151">**Microsoft Graph page reference:** [List apps in team](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="73386-152">**Requête HTTP GET** :</span><span class="sxs-lookup"><span data-stu-id="73386-152">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

>[!TIP]
> <span data-ttu-id="73386-153">Vous pouvez filtrer n’importe quel champ de l’objet [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true) pour affiner la liste des résultats.</span><span class="sxs-lookup"><span data-stu-id="73386-153">You can filter on any of the fields of the [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true) object to narrow the list of results.</span></span>

### <a name="-determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a><span data-ttu-id="73386-154">✔ déterminer si votre bot est actuellement installé pour un destinataire de message</span><span class="sxs-lookup"><span data-stu-id="73386-154">✔ Determine whether your bot is currently installed for a message recipient</span></span>

<span data-ttu-id="73386-155">**Référence de page Microsoft Graph : Liste** des applications [installées pour l’utilisateur](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="73386-155">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="73386-156">**Requête HTTP GET** :</span><span class="sxs-lookup"><span data-stu-id="73386-156">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="73386-157">Cette demande retourne un tableau vide si l’application n’est pas installée ou un tableau avec un seul objet [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) s’il a été installé.</span><span class="sxs-lookup"><span data-stu-id="73386-157">This request will return an empty array if the app is not installed, or an array with a single [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) object if it has been installed.</span></span>

### <a name="-install-your-app"></a><span data-ttu-id="73386-158">✔ installer votre application</span><span class="sxs-lookup"><span data-stu-id="73386-158">✔ Install your app</span></span>

<span data-ttu-id="73386-159">**Référence de page Microsoft Graph : installer** [l’application pour l’utilisateur](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="73386-159">**Microsoft Graph page reference:** [Install app for user](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="73386-160">**Requête HTTP POST** :</span><span class="sxs-lookup"><span data-stu-id="73386-160">**HTTP POST** request:</span></span>

```http
POST https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps
{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/v1.0/appCatalogs/teamsApps/{teamsAppId}"
}
```

<span data-ttu-id="73386-161">Si Microsoft Teams est en cours d’exécution pour l’utilisateur, il peut voir l’application s’installer immédiatement.</span><span class="sxs-lookup"><span data-stu-id="73386-161">If the user has Microsoft Teams running, they may see the app install immediately.</span></span> <span data-ttu-id="73386-162">Sinon, un redémarrage peut être nécessaire pour voir l’application installée.</span><span class="sxs-lookup"><span data-stu-id="73386-162">Alternatively, a restart may be necessary to see the installed app.</span></span>

### <a name="-retrieve-the-conversation-chatid"></a><span data-ttu-id="73386-163">✔ récupérer la conversation **chatId**</span><span class="sxs-lookup"><span data-stu-id="73386-163">✔ Retrieve the conversation **chatId**</span></span>

<span data-ttu-id="73386-164">Lorsque votre application est installée pour l’utilisateur, le bot reçoit une notification d’événement qui contient les informations nécessaires pour envoyer `conversationUpdate` [](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) le message proactif.</span><span class="sxs-lookup"><span data-stu-id="73386-164">When your app is installed for the user, the bot will receive a `conversationUpdate` [event notification](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) that will contain the necessary information to send the proactive message.</span></span>

<span data-ttu-id="73386-165">Les `chatId` données peuvent également être récupérées comme suit :</span><span class="sxs-lookup"><span data-stu-id="73386-165">The `chatId` can also be retrieved as follows:</span></span>

<span data-ttu-id="73386-166">**Référence de page Microsoft Graph : obtenir** une [conversation](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="73386-166">**Microsoft Graph page reference:** [Get chat](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)</span></span>

<span data-ttu-id="73386-167">**1.** Vous aurez besoin de votre `{teamsAppInstallationId}` application.</span><span class="sxs-lookup"><span data-stu-id="73386-167">**1.** You will need your app's `{teamsAppInstallationId}`.</span></span> <span data-ttu-id="73386-168">Si vous ne l’avez pas, utilisez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="73386-168">If you don't have it, use the following:</span></span>

<span data-ttu-id="73386-169">**Requête HTTP GET** :</span><span class="sxs-lookup"><span data-stu-id="73386-169">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="73386-170">La **propriété id** de la réponse est le `teamsAppInstallationId` .</span><span class="sxs-lookup"><span data-stu-id="73386-170">The **id** property of the response is the `teamsAppInstallationId`.</span></span>

<span data-ttu-id="73386-171">**2. Faites** la demande suivante pour récupérer le `chatId` :</span><span class="sxs-lookup"><span data-stu-id="73386-171">**2.** Make the following request to fetch the `chatId`:</span></span>

<span data-ttu-id="73386-172">**Requête HTTP GET** (autorisation — `TeamsAppInstallation.ReadWriteSelfForUser.All` ) :</span><span class="sxs-lookup"><span data-stu-id="73386-172">**HTTP GET** request (permission — `TeamsAppInstallation.ReadWriteSelfForUser.All`):</span></span>  

```http
 GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
```

<span data-ttu-id="73386-173">La **propriété id** de la réponse est le `chatId` .</span><span class="sxs-lookup"><span data-stu-id="73386-173">The **id** property of the response is the `chatId`.</span></span>

<span data-ttu-id="73386-174">Vous pouvez également récupérer la demande avec la demande ci-dessous, mais elle `chatId`  nécessitera l’autorisation plus `Chat.Read.All` large :</span><span class="sxs-lookup"><span data-stu-id="73386-174">Alternately, you can retrieve the `chatId`  with the request below, but it will require the broader `Chat.Read.All` permission:</span></span>

<span data-ttu-id="73386-175">**Requête HTTP GET** (autorisation — `Chat.Read.All` ) :</span><span class="sxs-lookup"><span data-stu-id="73386-175">**HTTP GET** request (permission — `Chat.Read.All`):</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
```

### <a name="-send-proactive-messages"></a><span data-ttu-id="73386-176">✔ messages proactifs</span><span class="sxs-lookup"><span data-stu-id="73386-176">✔ Send proactive messages</span></span>

<span data-ttu-id="73386-177">Une fois que votre bot a été ajouté pour un utilisateur ou une équipe et qu’il a acquis les informations utilisateur nécessaires, il peut commencer à [envoyer des messages proactifs.](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="73386-177">Once your bot has been added for a user or team and has acquired the necessary user  information, it can begin to [send proactive messages](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true).</span></span>

# <a name="c--net"></a>[<span data-ttu-id="73386-178">C# / .NET</span><span class="sxs-lookup"><span data-stu-id="73386-178">C# / .NET</span></span>](#tab/csharp)

<span data-ttu-id="73386-179">L’extrait de code suivant est issu des [exemples Microsoft Bot Framework pour C#.](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/16.proactive-messages)</span><span class="sxs-lookup"><span data-stu-id="73386-179">The following code snippet is from the [Microsoft Bot Framework Samples for C#.](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/16.proactive-messages)</span></span>

```csharp
using System.Collections.Concurrent;
using System.Collections.Generic;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.Bot.Builder;
using Microsoft.Bot.Schema;

namespace Microsoft.BotBuilderSamples
{
    public class ProactiveBot : ActivityHandler
    {
        // Message to send to users when the bot receives a Conversation Update event
        private const string WelcomeMessage = "Welcome to the Proactive Bot sample.  Navigate to http://localhost:3978/api/notify to proactively message everyone who has previously messaged this bot.";

        // Dependency injected dictionary for storing ConversationReference objects used in NotifyController to proactively message users
        private readonly ConcurrentDictionary<string, ConversationReference> _conversationReferences;

        public ProactiveBot(ConcurrentDictionary<string, ConversationReference> conversationReferences)
        {
            _conversationReferences = conversationReferences;
        }

        private void AddConversationReference(Activity activity)
        {
            var conversationReference = activity.GetConversationReference();
            _conversationReferences.AddOrUpdate(conversationReference.User.Id, conversationReference, (key, newValue) => conversationReference);
        }

        protected override Task OnConversationUpdateActivityAsync(ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
        {
            AddConversationReference(turnContext.Activity as Activity);

            return base.OnConversationUpdateActivityAsync(turnContext, cancellationToken);
        }

        protected override async Task OnMembersAddedAsync(IList<ChannelAccount> membersAdded, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
        {
            foreach (var member in membersAdded)
            {
                // Greet anyone that was not the target (recipient) of this message.
                if (member.Id != turnContext.Activity.Recipient.Id)
                {
                    await turnContext.SendActivityAsync(MessageFactory.Text(WelcomeMessage), cancellationToken);
                }
            }
        }

        protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
        {
            AddConversationReference(turnContext.Activity as Activity);

            // Echo back what the user said
            await turnContext.SendActivityAsync(MessageFactory.Text($"You sent '{turnContext.Activity.Text}'"), cancellationToken);
        }
    }
}
```

# <a name="javascript"></a>[<span data-ttu-id="73386-180">JavaScript</span><span class="sxs-lookup"><span data-stu-id="73386-180">JavaScript</span></span>](#tab/javascript)

<span data-ttu-id="73386-181">L’extrait de code suivant est issu des [exemples Microsoft Bot Framework pour JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/16.proactive-messages).</span><span class="sxs-lookup"><span data-stu-id="73386-181">The following code snippet is from the [Microsoft Bot Framework Samples for JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/16.proactive-messages).</span></span>

```javascript
const { ActivityHandler, TurnContext } = require('botbuilder');

class ProactiveBot extends ActivityHandler {
    constructor(conversationReferences) {
        super();

        // Dependency injected dictionary for storing ConversationReference objects used in NotifyController to proactively message users
        this.conversationReferences = conversationReferences;

        this.onConversationUpdate(async (context, next) => {
            this.addConversationReference(context.activity);

            await next();
        });

        this.onMembersAdded(async (context, next) => {
            const membersAdded = context.activity.membersAdded;
            for (let cnt = 0; cnt < membersAdded.length; cnt++) {
                if (membersAdded[cnt].id !== context.activity.recipient.id) {
                    const welcomeMessage = 'Welcome to the Proactive Bot sample.  Navigate to http://localhost:3978/api/notify to proactively message everyone who has previously messaged this bot.';
                    await context.sendActivity(welcomeMessage);
                }
            }

            // By calling next() you ensure that the next BotHandler is run.
            await next();
        });

        this.onMessage(async (context, next) => {
            this.addConversationReference(context.activity);

            // Echo back what the user said
            await context.sendActivity(`You sent '${ context.activity.text }'`);
            await next();
        });
    }

    addConversationReference(activity) {
        const conversationReference = TurnContext.getConversationReference(activity);
        this.conversationReferences[conversationReference.conversation.id] = conversationReference;
    }
}

module.exports.ProactiveBot = ProactiveBot;

```
---

## <a name="related-topic-for-teams-administrators"></a><span data-ttu-id="73386-182">Rubrique connexe pour les administrateurs Teams</span><span class="sxs-lookup"><span data-stu-id="73386-182">Related topic for Teams administrators</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="73386-183">**Gérer les stratégies de mise en application dans Teams**</span><span class="sxs-lookup"><span data-stu-id="73386-183">**Manage app setup policies in Microsoft Teams**</span></span>](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)

## <a name="view-additional-code-samples"></a><span data-ttu-id="73386-184">Afficher des exemples de code supplémentaires</span><span class="sxs-lookup"><span data-stu-id="73386-184">View additional code samples</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="73386-185">**Exemples de code de messagerie proactive Teams**</span><span class="sxs-lookup"><span data-stu-id="73386-185">**Teams proactive messaging code samples**</span></span>](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>
