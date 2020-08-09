---
title: Utiliser Microsoft Graph pour activer l’installation et la messagerie de robots proactifs dans teams
description: Décrit la messagerie proactive dans teams et la mise en œuvre.
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: Graphique d’installation de conversation de messagerie proactive teams
ms.openlocfilehash: f1d2c51957eefbc548918210b843e408eb1107c8
ms.sourcegitcommit: 7a2da3b65246a125d441a971e7e6a6418355adbe
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/07/2020
ms.locfileid: "46587740"
---
# <a name="enable-proactive-bot-installation-and-proactive-messaging-in-teams-with-microsoft-graph-public-preview"></a><span data-ttu-id="0ddbd-104">Activation de l’installation proactive du bot et de la messagerie proactive dans teams avec Microsoft Graph (préversion publique)</span><span class="sxs-lookup"><span data-stu-id="0ddbd-104">Enable proactive bot installation and proactive messaging in Teams with Microsoft Graph (Public Preview)</span></span>

>[!IMPORTANT]
> <span data-ttu-id="0ddbd-105">Les aperçus publics de Microsoft Graph sont disponibles pour l’accès anticipé et les commentaires.</span><span class="sxs-lookup"><span data-stu-id="0ddbd-105">Microsoft Graph public previews are available for early-access and feedback.</span></span> <span data-ttu-id="0ddbd-106">Bien que cette version ait subi des tests approfondis, elle n’est pas destinée à être utilisée en production.</span><span class="sxs-lookup"><span data-stu-id="0ddbd-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

## <a name="proactive-messaging-in-teams"></a><span data-ttu-id="0ddbd-107">Messagerie proactive dans teams</span><span class="sxs-lookup"><span data-stu-id="0ddbd-107">Proactive messaging in Teams</span></span>

<span data-ttu-id="0ddbd-108">Les messages proactifs sont initiés par les robots pour démarrer des conversations avec un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0ddbd-108">Proactive messages are initiated by bots to start conversations with a user.</span></span> <span data-ttu-id="0ddbd-109">Elles répondent à de nombreux objectifs, notamment en envoyant des messages de bienvenue, en effectuant des enquêtes ou des sondages et en diffusant des notifications à l’échelle de l’organisation.</span><span class="sxs-lookup"><span data-stu-id="0ddbd-109">They serve many purposes including sending welcome messages, conducting surveys or polls, and broadcasting organization-wide notifications.</span></span>  <span data-ttu-id="0ddbd-110">Les messages proactifs dans teams peuvent être fournis sous la forme de conversations **ad hoc** ou **basées sur des boîtes de dialogue** :</span><span class="sxs-lookup"><span data-stu-id="0ddbd-110">Proactive messages in Teams can be delivered as either **ad-hoc** or **dialog-based** conversations:</span></span>

|<span data-ttu-id="0ddbd-111">Type de message</span><span class="sxs-lookup"><span data-stu-id="0ddbd-111">Message Type</span></span> | <span data-ttu-id="0ddbd-112">Description</span><span class="sxs-lookup"><span data-stu-id="0ddbd-112">Description</span></span> |
|----------------|-------------- |
|<span data-ttu-id="0ddbd-113">Message proactif ad hoc</span><span class="sxs-lookup"><span data-stu-id="0ddbd-113">Ad-hoc proactive message</span></span>| <span data-ttu-id="0ddbd-114">Le bot prorompre un message sans interrompre le flux de conversation.</span><span class="sxs-lookup"><span data-stu-id="0ddbd-114">The bot interjects a message without interrupting the conversation flow.</span></span>|
|<span data-ttu-id="0ddbd-115">Message proactif basé sur des boîtes de dialogue</span><span class="sxs-lookup"><span data-stu-id="0ddbd-115">Dialog-based proactive message</span></span> | <span data-ttu-id="0ddbd-116">Le bot crée un nouveau thread, prend le contrôle d’une conversation, remet le message proactif, se ferme et renvoie le contrôle à la boîte de dialogue précédente.</span><span class="sxs-lookup"><span data-stu-id="0ddbd-116">The bot creates a new dialog thread, takes control of a conversation, delivers the proactive message, closes, and returns control to the previous dialog.</span></span>|

<span data-ttu-id="0ddbd-117">*Voir*, [Envoyer des notifications proactives au kit de développement logiciel (SDK) v4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp)</span><span class="sxs-lookup"><span data-stu-id="0ddbd-117">*See*, [Send proactive notifications to users SDK v4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp)</span></span>

## <a name="proactive-app-installation-in-teams"></a><span data-ttu-id="0ddbd-118">Installation de l’application proactive dans teams</span><span class="sxs-lookup"><span data-stu-id="0ddbd-118">Proactive app installation in Teams</span></span>

<span data-ttu-id="0ddbd-119">Pour que votre robot puisse messageer de manière proactive un utilisateur, il doit être installé en tant qu’application personnelle ou dans une équipe où l’utilisateur est membre.</span><span class="sxs-lookup"><span data-stu-id="0ddbd-119">Before your bot can proactively message a user, it needs to be installed either as a personal app, or in a team where the user is a member.</span></span> <span data-ttu-id="0ddbd-120">Parfois, vous devrez peut-être communiquer de manière proactive les utilisateurs qui _n’ont pas_ installé ou précédemment interagi avec votre application.</span><span class="sxs-lookup"><span data-stu-id="0ddbd-120">At times,  you may need to proactively message users that have _not_ installed or previously interacted with your app.</span></span> <span data-ttu-id="0ddbd-121">Par exemple, la nécessité de messageer des informations vitales à tous les membres de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="0ddbd-121">For instance, the need to message vital information to everyone in your organization.</span></span> <span data-ttu-id="0ddbd-122">Pour ces scénarios, vous pouvez utiliser l’API Microsoft Graph pour installer votre robot de manière proactive pour vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="0ddbd-122">For such scenarios, you can use the Microsoft Graph API to proactively install your bot for your users.</span></span>

## <a name="permissions"></a><span data-ttu-id="0ddbd-123">Autorisations</span><span class="sxs-lookup"><span data-stu-id="0ddbd-123">Permissions</span></span>

<span data-ttu-id="0ddbd-124">Les autorisations de [type de ressource](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0) Microsoft Graph teamsAppInstallation vous permettent de gérer le cycle de vie de l’installation de votre application pour toutes les étendues utilisateur (personnelles) ou d’équipe (canal) au sein de la plateforme Microsoft teams :</span><span class="sxs-lookup"><span data-stu-id="0ddbd-124">Microsoft Graph [teamsAppInstallation resource type](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0) permissions allow you to manage your app's installation lifecycle for all user (personal) or team (channel) scopes within the Microsoft Teams platform:</span></span>

|<span data-ttu-id="0ddbd-125">Autorisation de l’application</span><span class="sxs-lookup"><span data-stu-id="0ddbd-125">Application permission</span></span> | <span data-ttu-id="0ddbd-126">Description</span><span class="sxs-lookup"><span data-stu-id="0ddbd-126">Description</span></span>|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|<span data-ttu-id="0ddbd-127">Permet à une application de teams de lire, d’installer, de mettre à niveau et de désinstaller lui-même pour tout **utilisateur**, sans connexion ni utilisation préalable.</span><span class="sxs-lookup"><span data-stu-id="0ddbd-127">Allows a Teams app to read, install, upgrade, and uninstall itself for any **user**, without prior sign in or use.</span></span>|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|<span data-ttu-id="0ddbd-128">Permet à une application de teams de lire, d’installer, de mettre à niveau et de désinstaller elle-même dans n’importe quelle **équipe**, sans connexion ni utilisation préalable.</span><span class="sxs-lookup"><span data-stu-id="0ddbd-128">Allows a Teams app to read, install, upgrade, and uninstall itself in any **team**, without prior sign in or use.</span></span>|

<span data-ttu-id="0ddbd-129">Pour utiliser ces autorisations, vous devez ajouter une clé [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) à votre manifeste d’application avec les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="0ddbd-129">To use these permissions, you must add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>
> [!div class="checklist"]
> [!div class="checklist"]
>
> * <span data-ttu-id="0ddbd-130">**ID** : votre ID d’application Azure ad.</span><span class="sxs-lookup"><span data-stu-id="0ddbd-130">**id**  — your Azure AD app id.</span></span>
> * <span data-ttu-id="0ddbd-131">**ressource** — l’URL de la ressource pour l’application.</span><span class="sxs-lookup"><span data-stu-id="0ddbd-131">**resource** — the resource URL for the app.</span></span>
>

>[!NOTE]
>
> * <span data-ttu-id="0ddbd-132">Votre bot requiert des autorisations _déléguées_ de l' _application_ , car l’installation n’est pas pour vous, mais pour d’autres.</span><span class="sxs-lookup"><span data-stu-id="0ddbd-132">Your bot requires _application_ not _user delegated_ permissions because the installation is not for yourself but for others.</span></span>
>
> * <span data-ttu-id="0ddbd-133">Un administrateur client Azure AD doit [accorder explicitement des autorisations à une application](/graph/security-authorization#grant-permissions-to-an-application).</span><span class="sxs-lookup"><span data-stu-id="0ddbd-133">An Azure AD tenant administrator must [explicitly grant permissions to an application](/graph/security-authorization#grant-permissions-to-an-application).</span></span> <span data-ttu-id="0ddbd-134">Une fois qu’une application reçoit des autorisations, _tous_ les membres du client Azure ad bénéficient des autorisations accordées.</span><span class="sxs-lookup"><span data-stu-id="0ddbd-134">After an application is granted permissions, _all_ members of the Azure AD tenant will gain the granted permissions.</span></span>

## <a name="enable-proactive-app-installation-and-messaging"></a><span data-ttu-id="0ddbd-135">Activation de la messagerie et de l’installation de l’application proactive</span><span class="sxs-lookup"><span data-stu-id="0ddbd-135">Enable proactive app installation and messaging</span></span>

 > [!IMPORTANT]
><span data-ttu-id="0ddbd-136">Microsoft Graph installe uniquement les applications publiées dans le [catalogue d’applications](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) de votre organisation ou dans [AppSource](https://appsource.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="0ddbd-136">Microsoft Graph will only install apps published within your organization's [app catalog](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) or in [AppSource](https://appsource.microsoft.com/).</span></span>

### <a name="-create-and-publish-your-proactive-messaging-bot-for-teams"></a><span data-ttu-id="0ddbd-137">✔ Créer et publier votre robot de messagerie proactive pour teams</span><span class="sxs-lookup"><span data-stu-id="0ddbd-137">✔ Create and publish your proactive messaging bot for Teams</span></span>

<span data-ttu-id="0ddbd-138">Pour commencer, vous aurez besoin d’un [bot pour teams](../../bots/how-to/create-a-bot-for-teams.md) avec des fonctionnalités de [messagerie proactive](../../concepts/bots/bot-conversations/bots-conv-proactive.md) et [publié](../../concepts/deploy-and-publish/overview.md) dans le [catalogue d’applications](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) de votre organisation ou dans [AppSource](https://appsource.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="0ddbd-138">To get started, you will need a [bot for Teams](../../bots/how-to/create-a-bot-for-teams.md) with [proactive messaging](../../concepts/bots/bot-conversations/bots-conv-proactive.md) capabilities and  [published](../../concepts/deploy-and-publish/overview.md) in your organization's [app catalog](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) or in [AppSource](https://appsource.microsoft.com/).</span></span>

>[!TIP]
> <span data-ttu-id="0ddbd-139">Le modèle d’application [**Communicator**](../..//samples/app-templates.md#company-communicator) de l’entreprise prête pour la production permet la messagerie de diffusion et constitue une base intéressante pour la création de votre application bot proactive.</span><span class="sxs-lookup"><span data-stu-id="0ddbd-139">The production-ready [**Company Communicator**](../..//samples/app-templates.md#company-communicator) app template enables broadcast messaging and is a good foundation for building your proactive bot application.</span></span>

### <a name="-get-the-teamsappid-for-your-app"></a><span data-ttu-id="0ddbd-140">✔ Obtenir le `teamsAppId` pour votre application</span><span class="sxs-lookup"><span data-stu-id="0ddbd-140">✔ Get the `teamsAppId` for your app</span></span>

<span data-ttu-id="0ddbd-141">**1.** vous en aurez besoin `teamsAppId` pour les étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="0ddbd-141">**1.** You will need the `teamsAppId`  for the next steps.</span></span>

<span data-ttu-id="0ddbd-142">Le `teamsAppId` peut être récupéré à partir du catalogue d’applications de votre organisation :</span><span class="sxs-lookup"><span data-stu-id="0ddbd-142">The `teamsAppId` can be retrieved from your organization's app catalog:</span></span>

<span data-ttu-id="0ddbd-143">**Référence de la page Microsoft Graph :** [type de ressource teamsApp](/graph/api/resources/teamsapp?view=graph-rest-1.0)</span><span class="sxs-lookup"><span data-stu-id="0ddbd-143">**Microsoft Graph page reference:** [teamsApp resource type](/graph/api/resources/teamsapp?view=graph-rest-1.0)</span></span>

<span data-ttu-id="0ddbd-144">Requête **Get http** :</span><span class="sxs-lookup"><span data-stu-id="0ddbd-144">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
```

<span data-ttu-id="0ddbd-145">La demande renverra un `teamsApp` objet.</span><span class="sxs-lookup"><span data-stu-id="0ddbd-145">The request will return a `teamsApp`  object.</span></span> <span data-ttu-id="0ddbd-146">L’objet renvoyé `id` est l’ID de l’application générée par le catalogue de l’application et est différent du « ID : » que vous avez fourni dans le manifeste de votre application teams :</span><span class="sxs-lookup"><span data-stu-id="0ddbd-146">The returned object's `id`  is the app's catalog generated app id and is different from the "id:" that you provided in your Teams app manifest:</span></span>

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

<span data-ttu-id="0ddbd-147">**2.** si votre application a déjà été téléchargée/versions test chargées pour un utilisateur dans l’étendue personnelle, vous pouvez récupérer les `teamsAppId` éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="0ddbd-147">**2.**  If your app has already been uploaded/sideloaded for a user in the personal scope, you can retrieve the `teamsAppId` as follows:</span></span>

<span data-ttu-id="0ddbd-148">**Référence de la page Microsoft Graph :** [répertorier les applications installées pour l’utilisateur](/graph/api/user-list-teamsappinstallation?view=graph-rest-beta&tabs=http)</span><span class="sxs-lookup"><span data-stu-id="0ddbd-148">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/user-list-teamsappinstallation?view=graph-rest-beta&tabs=http)</span></span>

<span data-ttu-id="0ddbd-149">Requête **Get http** :</span><span class="sxs-lookup"><span data-stu-id="0ddbd-149">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="0ddbd-150">**3.** si votre application a déjà été téléchargée/versions test chargées pour un canal dans l’étendue de l’équipe, vous pouvez récupérer les `teamsAppId` éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="0ddbd-150">**3.** If your app has already been uploaded/sideloaded for a channel in the team scope, you can retrieve the `teamsAppId` as follows:</span></span>

<span data-ttu-id="0ddbd-151">**Référence de la page Microsoft Graph :** [répertorier les applications dans Team](/graph/api/teamsappinstallation-list?view=graph-rest-beta&tabs=http)</span><span class="sxs-lookup"><span data-stu-id="0ddbd-151">**Microsoft Graph page reference:** [List apps in team](/graph/api/teamsappinstallation-list?view=graph-rest-beta&tabs=http)</span></span>

<span data-ttu-id="0ddbd-152">Requête **Get http** :</span><span class="sxs-lookup"><span data-stu-id="0ddbd-152">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{manifestId}'
```

>[!TIP]
> <span data-ttu-id="0ddbd-153">Vous pouvez filtrer les champs de l’objet [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0) pour affiner la liste des résultats.</span><span class="sxs-lookup"><span data-stu-id="0ddbd-153">You can filter on any of the fields of the [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0) object to narrow the list of results.</span></span>

### <a name="-determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a><span data-ttu-id="0ddbd-154">✔ Déterminer si votre bot est actuellement installé pour un destinataire de message</span><span class="sxs-lookup"><span data-stu-id="0ddbd-154">✔ Determine whether your bot is currently installed for a message recipient</span></span>

<span data-ttu-id="0ddbd-155">**Référence de la page Microsoft Graph :** [répertorier les applications installées pour l’utilisateur](/graph/api/user-list-teamsappinstallation?view=graph-rest-beta&tabs=http)</span><span class="sxs-lookup"><span data-stu-id="0ddbd-155">**Microsoft Graph page reference:** [List apps installed for user](/graph/api/user-list-teamsappinstallation?view=graph-rest-beta&tabs=http)</span></span>

<span data-ttu-id="0ddbd-156">Requête **Get http** :</span><span class="sxs-lookup"><span data-stu-id="0ddbd-156">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="0ddbd-157">Cette requête renverra un tableau vide si l’application n’est pas installée ou une baie avec un seul objet [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-beta) , si elle a été installée.</span><span class="sxs-lookup"><span data-stu-id="0ddbd-157">This request will return an empty array if the app is not installed, or an array with a single [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-beta) object if it has been installed.</span></span>

### <a name="-install-your-app"></a><span data-ttu-id="0ddbd-158">✔ Installer votre application</span><span class="sxs-lookup"><span data-stu-id="0ddbd-158">✔ Install your app</span></span>

<span data-ttu-id="0ddbd-159">**Référence Microsoft Graph :** [installer l’application pour l’utilisateur](/graph/api/user-add-teamsappinstallation?view=graph-rest-beta&tabs=http)</span><span class="sxs-lookup"><span data-stu-id="0ddbd-159">**Microsoft Graph reference:** [Install app for user](/graph/api/user-add-teamsappinstallation?view=graph-rest-beta&tabs=http)</span></span>

<span data-ttu-id="0ddbd-160">Demande **http post** :</span><span class="sxs-lookup"><span data-stu-id="0ddbd-160">**HTTP POST** request:</span></span>

```http
POST https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps
{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/beta/appCatalogs/teamsApps/{teamsAppId}"
}
```

<span data-ttu-id="0ddbd-161">Si Microsoft teams est en cours d’exécution pour l’utilisateur, l’installation de l’application peut s’afficher immédiatement.</span><span class="sxs-lookup"><span data-stu-id="0ddbd-161">If the user has Microsoft Teams running, they may see the app install immediately.</span></span> <span data-ttu-id="0ddbd-162">Un redémarrage peut également être nécessaire pour afficher l’application installée.</span><span class="sxs-lookup"><span data-stu-id="0ddbd-162">Alternatively,  a  restart may be necessary to see the installed app.</span></span>

### <a name="-retrieve-the-conversation-chatid"></a><span data-ttu-id="0ddbd-163">✔ Récupérer le **chatId** de conversation</span><span class="sxs-lookup"><span data-stu-id="0ddbd-163">✔ Retrieve the conversation **chatId**</span></span>

<span data-ttu-id="0ddbd-164">Lorsque votre application est installée pour l’utilisateur, le bot reçoit une `conversationUpdate` [notification d’événement](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) qui contiendra les informations nécessaires pour envoyer le message proactif.</span><span class="sxs-lookup"><span data-stu-id="0ddbd-164">When your app is installed for the user, the bot will receive a `conversationUpdate` [event notification](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) that will contain the necessary information to send the proactive message.</span></span>

<span data-ttu-id="0ddbd-165">Le `chatId` peut également être récupéré comme suit :</span><span class="sxs-lookup"><span data-stu-id="0ddbd-165">The `chatId` can also be retrieved as follows:</span></span>

<span data-ttu-id="0ddbd-166">**Référence Microsoft Graph :** [obtenir une conversation](/graph/api/chat-get?view=graph-rest-beta&tabs=http)</span><span class="sxs-lookup"><span data-stu-id="0ddbd-166">**Microsoft Graph reference:** [Get chat](/graph/api/chat-get?view=graph-rest-beta&tabs=http)</span></span>

<span data-ttu-id="0ddbd-167">**1.** vous aurez besoin de votre application `{teamsAppInstallationId}` .</span><span class="sxs-lookup"><span data-stu-id="0ddbd-167">**1.** You will need your app's `{teamsAppInstallationId}`.</span></span> <span data-ttu-id="0ddbd-168">Si vous ne l’avez pas, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0ddbd-168">If you don't have it, use the following:</span></span>

<span data-ttu-id="0ddbd-169">Requête **Get http** :</span><span class="sxs-lookup"><span data-stu-id="0ddbd-169">**HTTP GET** request:</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

<span data-ttu-id="0ddbd-170">La propriété **ID** de la réponse est l' `teamsAppInstallationId` .</span><span class="sxs-lookup"><span data-stu-id="0ddbd-170">The **id** property of the response is the `teamsAppInstallationId`.</span></span>

<span data-ttu-id="0ddbd-171">**2.** effectuez la requête suivante pour extraire les `chatId` éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="0ddbd-171">**2.** Make the following request to fetch the `chatId`:</span></span>

<span data-ttu-id="0ddbd-172">Requête **http Get** (autorisation `TeamsAppInstallation.ReadWriteSelfForUser.All` ) :</span><span class="sxs-lookup"><span data-stu-id="0ddbd-172">**HTTP GET** request (permission — `TeamsAppInstallation.ReadWriteSelfForUser.All`):</span></span>  

```http
 GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
```

<span data-ttu-id="0ddbd-173">La propriété **ID** de la réponse est l' `chatId` .</span><span class="sxs-lookup"><span data-stu-id="0ddbd-173">The **id** property of the response is the `chatId`.</span></span>

<span data-ttu-id="0ddbd-174">Vous pouvez également récupérer les `chatId` avec la demande ci-dessous, mais cela nécessite une autorisation plus large `Chat.Read.All` :</span><span class="sxs-lookup"><span data-stu-id="0ddbd-174">Alternately, you can retrieve the `chatId`  with the request below, but it will require the broader `Chat.Read.All` permission:</span></span>

<span data-ttu-id="0ddbd-175">Requête **http Get** (autorisation `Chat.Read.All` ) :</span><span class="sxs-lookup"><span data-stu-id="0ddbd-175">**HTTP GET** request (permission — `Chat.Read.All`):</span></span>

```http
GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
```

### <a name="-send-proactive-messages"></a><span data-ttu-id="0ddbd-176">✔ Envoyer des messages proactifs</span><span class="sxs-lookup"><span data-stu-id="0ddbd-176">✔ Send proactive messages</span></span>

<span data-ttu-id="0ddbd-177">Une fois que votre robot a été ajouté pour un utilisateur ou une équipe et qu’il a acquis les informations d’utilisateur nécessaires, il peut commencer à [Envoyer des messages proactifs](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp).</span><span class="sxs-lookup"><span data-stu-id="0ddbd-177">Once your bot has been added for a user or team and has acquired the necessary user  information, it can begin to [send proactive messages](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp).</span></span>

# <a name="c--net"></a>[<span data-ttu-id="0ddbd-178">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="0ddbd-178">C# / .NET</span></span>](#tab/csharp)

<span data-ttu-id="0ddbd-179">L’extrait de code suivant provient des [exemples de l’infrastructure Microsoft bot pour C#.](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/16.proactive-messages)</span><span class="sxs-lookup"><span data-stu-id="0ddbd-179">The following code snippet is from the [Microsoft Bot Framework Samples for C#.](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/16.proactive-messages)</span></span>

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

# <a name="javascript"></a>[<span data-ttu-id="0ddbd-180">JavaScript</span><span class="sxs-lookup"><span data-stu-id="0ddbd-180">JavaScript</span></span>](#tab/javascript)

<span data-ttu-id="0ddbd-181">L’extrait de code suivant provient des [exemples de Microsoft bot Framework pour JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/16.proactive-messages).</span><span class="sxs-lookup"><span data-stu-id="0ddbd-181">The following code snippet is from the [Microsoft Bot Framework Samples for JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/16.proactive-messages).</span></span>

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

## <a name="related-topic-for-teams-administrators"></a><span data-ttu-id="0ddbd-182">Rubrique connexe pour les administrateurs teams</span><span class="sxs-lookup"><span data-stu-id="0ddbd-182">Related topic for Teams administrators</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="0ddbd-183">**Gérer les stratégies de configuration d’application dans Microsoft teams**</span><span class="sxs-lookup"><span data-stu-id="0ddbd-183">**Manage app setup policies in Microsoft Teams**</span></span>](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)

## <a name="view-additional-code-samples"></a><span data-ttu-id="0ddbd-184">Afficher des exemples de code supplémentaires</span><span class="sxs-lookup"><span data-stu-id="0ddbd-184">View additional code samples</span></span>
>
> [!div class="nextstepaction"]
> [<span data-ttu-id="0ddbd-185">**Exemples de code de messagerie proactive teams**</span><span class="sxs-lookup"><span data-stu-id="0ddbd-185">**Teams proactive messaging code samples**</span></span>](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>
