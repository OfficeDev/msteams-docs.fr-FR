---
title: Tester les autorisations de consentement propres aux ressources dans Teams
description: Détails du test du consentement spécifique aux ressources Teams postman
localization_priority: Normal
author: akjo
ms.author: lajanuar
ms.topic: tutorial
keywords: Autorisation OAuth DSO Teams AAD rsc Postman Graph
ms.openlocfilehash: 8f5b293557ef7de9e4d551c5ae2bd7216e6e3fc0
ms.sourcegitcommit: 261058171f1e3bbc822c5bcc0e9fba5a4de68000
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/24/2021
ms.locfileid: "53111127"
---
# <a name="test-resource-specific-consent-permissions-in-teams"></a><span data-ttu-id="e2b17-104">Tester les autorisations de consentement propres aux ressources dans Teams</span><span class="sxs-lookup"><span data-stu-id="e2b17-104">Test resource-specific consent permissions in Teams</span></span>

> [!NOTE]
> <span data-ttu-id="e2b17-105">Le consentement spécifique aux ressources pour l’étendue de conversation est disponible en [prévisualisation publique pour les](../../resources/dev-preview/developer-preview-intro.md) développeurs uniquement.</span><span class="sxs-lookup"><span data-stu-id="e2b17-105">Resource-specific consent for chat scope is available in [public developer preview](../../resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="e2b17-106">Le consentement spécifique aux ressources (RSC) est une intégration d’API Microsoft Teams et Graph qui permet à votre application d’utiliser des points de terminaison d’API pour gérer des ressources spécifiques (équipes ou conversations) au sein d’une organisation.</span><span class="sxs-lookup"><span data-stu-id="e2b17-106">Resource-specific consent (RSC) is a Microsoft Teams and Graph API integration that enables your app to use API endpoints to manage specific resources—either teams or chats—within an organization.</span></span> <span data-ttu-id="e2b17-107">Pour plus d’informations, voir consentement spécifique à la [ressource (RSC) — Microsoft Teams Graph API](resource-specific-consent.md).</span><span class="sxs-lookup"><span data-stu-id="e2b17-107">For more information, see [Resource-specific consent (RSC) — Microsoft Teams Graph API](resource-specific-consent.md).</span></span>

> [!NOTE]
> <span data-ttu-id="e2b17-108">Pour tester les autorisations RSC, votre fichier manifeste d’application Teams doit inclure une clé **webApplicationInfo** remplie avec les champs suivants :</span><span class="sxs-lookup"><span data-stu-id="e2b17-108">To test the RSC permissions, your Teams app manifest file must include a **webApplicationInfo** key populated with the following fields:</span></span>
>
> - <span data-ttu-id="e2b17-109">**id :** votre ID d’application Azure AD, voir [Inscrire votre application dans le portail Azure AD.](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-aad-portal)</span><span class="sxs-lookup"><span data-stu-id="e2b17-109">**id**: Your Azure AD app ID, see [Register your app in the Azure AD portal](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-aad-portal).</span></span>
> - <span data-ttu-id="e2b17-110">**ressource**: Toute chaîne, voir la remarque dans Mettre à jour [votre Teams manifeste d’application.](resource-specific-consent.md#update-your-teams-app-manifest)</span><span class="sxs-lookup"><span data-stu-id="e2b17-110">**resource**: Any string, see the note in  [Update your Teams app manifest](resource-specific-consent.md#update-your-teams-app-manifest).</span></span>
> - <span data-ttu-id="e2b17-111">**autorisations d’application**: autorisations RSC pour votre application, voir [Autorisations propres aux ressources.](resource-specific-consent.md#resource-specific-permissions)</span><span class="sxs-lookup"><span data-stu-id="e2b17-111">**application permissions**: RSC permissions for  your app, see [Resource-specific Permissions](resource-specific-consent.md#resource-specific-permissions).</span></span>

## <a name="example-for-a-team"></a><span data-ttu-id="e2b17-112">Exemple pour une équipe</span><span class="sxs-lookup"><span data-stu-id="e2b17-112">Example for a team</span></span>
```json
"webApplicationInfo":{
      "id":"XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
      "resource":"https://AnyString",
      "applicationPermissions":[
         "Channel.Create.Group",
         "Channel.Delete.Group",
         "ChannelMessage.Read.Group",
         "ChannelSettings.Read.Group",
         "ChannelSettings.Edit.Group",
         "Member.Read.Group",
         "Owner.Read.Group",
         "TeamsApp.Read.Group",
         "TeamsTab.Read.Group",
         "TeamsTab.Create.Group",
         "TeamsTab.Edit.Group",
         "TeamsTab.Delete.Group",
         "TeamSettings.Read.Group",
         "TeamSettings.Edit.Group"
      ]
   }
```

## <a name="example-for-a-chat"></a><span data-ttu-id="e2b17-113">Exemple pour une conversation</span><span class="sxs-lookup"><span data-stu-id="e2b17-113">Example for a chat</span></span>
```json
"webApplicationInfo":{
      "id":"XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
      "resource":"https://AnyString",
      "applicationPermissions":[
          "ChatSettings.Read.Chat",
          "ChatSettings.ReadWrite.Chat",
          "ChatMessage.Read.Chat",
          "ChatMember.Read.Chat",
          "Chat.Manage.Chat",
          "TeamsTab.Read.Chat",
          "TeamsTab.Create.Chat",
          "TeamsTab.Delete.Chat",
          "TeamsTab.ReadWrite.Chat",
          "TeamsAppInstallation.Read.Chat",
          "OnlineMeeting.ReadBasic.Chat"
      ]
   }
```

> [!IMPORTANT]
> <span data-ttu-id="e2b17-114">Dans le manifeste de votre application, incluez uniquement les autorisations RSC dont vous souhaitez que votre application soit propriétaire.</span><span class="sxs-lookup"><span data-stu-id="e2b17-114">In your app manifest, only include the RSC permissions that you want your app to have.</span></span>

>[!NOTE]
><span data-ttu-id="e2b17-115">Si l’application est destinée à prendre en charge l’installation dans les étendues d’équipe et de conversation, les autorisations d’équipe et de conversation peuvent être spécifiées dans le même manifeste sous `applicationPermissions` .</span><span class="sxs-lookup"><span data-stu-id="e2b17-115">If the app is meant to support installation in both team and chat scopes, then both team and chat permissions can be specified in the same manifest under `applicationPermissions`.</span></span>

## <a name="test-added-rsc-permissions-to-a-team-using-the-postman-app"></a><span data-ttu-id="e2b17-116">Test ajout d’autorisations RSC à une équipe à l’aide de l’application Postman</span><span class="sxs-lookup"><span data-stu-id="e2b17-116">Test added RSC permissions to a team using the Postman app</span></span>

<span data-ttu-id="e2b17-117">Pour vérifier si les autorisations RSC sont honorées par la charge utile de demande d’API, vous devez copier le code de [test JSON RSC](test-team-rsc-json-file.md) pour l’équipe dans votre environnement local et mettre à jour les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="e2b17-117">To check whether the RSC permissions are being honored by the API request payload, you need to copy the [RSC JSON test code for team](test-team-rsc-json-file.md) into your local environment and update the following values:</span></span>

* <span data-ttu-id="e2b17-118">`azureADAppId`: ID d’application Azure AD de votre application.</span><span class="sxs-lookup"><span data-stu-id="e2b17-118">`azureADAppId`: Your app's Azure AD app ID.</span></span>
* <span data-ttu-id="e2b17-119">`azureADAppSecret`: mot de passe de votre application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e2b17-119">`azureADAppSecret`: Your Azure AD app password.</span></span>
* <span data-ttu-id="e2b17-120">`token_scope`: l’étendue est requise pour obtenir un jeton.</span><span class="sxs-lookup"><span data-stu-id="e2b17-120">`token_scope`: The scope is required to get a token.</span></span> <span data-ttu-id="e2b17-121">définissez la valeur sur https://graph.microsoft.com/.default .</span><span class="sxs-lookup"><span data-stu-id="e2b17-121">set the value to https://graph.microsoft.com/.default.</span></span>
* <span data-ttu-id="e2b17-122">`teamGroupId`: vous pouvez obtenir l’ID de groupe d’équipe à partir du client Teams comme suit :</span><span class="sxs-lookup"><span data-stu-id="e2b17-122">`teamGroupId`: You can get the team group id from the Teams client as follows:</span></span>

    1. <span data-ttu-id="e2b17-123">Dans le Teams client, **sélectionnez Teams** dans la barre de navigation à l’extrême gauche.</span><span class="sxs-lookup"><span data-stu-id="e2b17-123">In the Teams client, select **Teams** from the far left navigation bar.</span></span>
    2. <span data-ttu-id="e2b17-124">Sélectionnez l’équipe où l’application est installée dans le menu déroulant.</span><span class="sxs-lookup"><span data-stu-id="e2b17-124">Select the team where the app is installed from the dropdown menu.</span></span>
    3. <span data-ttu-id="e2b17-125">Sélectionnez **l’icône Options** supplémentaires (&#8943;).</span><span class="sxs-lookup"><span data-stu-id="e2b17-125">Select the **More options** icon (&#8943;).</span></span>
    4. <span data-ttu-id="e2b17-126">Sélectionnez **Obtenir un lien vers l’équipe.**</span><span class="sxs-lookup"><span data-stu-id="e2b17-126">Select **Get link to team**.</span></span> 
    5. <span data-ttu-id="e2b17-127">Copiez et enregistrez la **valeur groupId** à partir de la chaîne.</span><span class="sxs-lookup"><span data-stu-id="e2b17-127">Copy and save the **groupId** value from the string.</span></span>

## <a name="test-added-rsc-permissions-to-a-chat-using-the-postman-app"></a><span data-ttu-id="e2b17-128">Test ajout d’autorisations RSC à une conversation à l’aide de l’application Postman</span><span class="sxs-lookup"><span data-stu-id="e2b17-128">Test added RSC permissions to a chat using the Postman app</span></span>

<span data-ttu-id="e2b17-129">Pour vérifier si les autorisations RSC sont honorées par la charge utile de demande d’API, vous devez copier le code de [test JSON RSC](test-chat-rsc-json-file.md) pour les conversations dans votre environnement local et mettre à jour les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="e2b17-129">To check whether the RSC permissions are being honored by the API request payload, you need to copy the [RSC JSON test code for chats](test-chat-rsc-json-file.md) into your local environment and update the following values:</span></span>

* <span data-ttu-id="e2b17-130">`azureADAppId`: ID d’application Azure AD de votre application.</span><span class="sxs-lookup"><span data-stu-id="e2b17-130">`azureADAppId`: Your app's Azure AD app ID.</span></span>
* <span data-ttu-id="e2b17-131">`azureADAppSecret`: mot de passe de votre application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e2b17-131">`azureADAppSecret`: Your Azure AD app password.</span></span>
* <span data-ttu-id="e2b17-132">`token_scope`: l’étendue est requise pour obtenir un jeton.</span><span class="sxs-lookup"><span data-stu-id="e2b17-132">`token_scope`: The scope is required to get a token.</span></span> <span data-ttu-id="e2b17-133">définissez la valeur sur https://graph.microsoft.com/.default .</span><span class="sxs-lookup"><span data-stu-id="e2b17-133">set the value to https://graph.microsoft.com/.default.</span></span>
* <span data-ttu-id="e2b17-134">`tenantId`: nom ou ID d’objet AAD de votre client.</span><span class="sxs-lookup"><span data-stu-id="e2b17-134">`tenantId`: The name or the AAD Object ID of your tenant.</span></span>
* <span data-ttu-id="e2b17-135">`chatId`: vous pouvez obtenir l’ID de thread de conversation à partir du client *web* Teams comme suit :</span><span class="sxs-lookup"><span data-stu-id="e2b17-135">`chatId`: You can get the chat thread id from the Teams *web* client as follows:</span></span>

    1. <span data-ttu-id="e2b17-136">Dans le Teams web, sélectionnez **Conversation** dans la barre de navigation de l’extrême gauche.</span><span class="sxs-lookup"><span data-stu-id="e2b17-136">In the Teams web client, select **Chat** from the far left navigation bar.</span></span>
    2. <span data-ttu-id="e2b17-137">Sélectionnez la conversation dans laquelle l’application est installée dans le menu déroulant.</span><span class="sxs-lookup"><span data-stu-id="e2b17-137">Select the chat where the app is installed from the dropdown menu.</span></span>
    3. <span data-ttu-id="e2b17-138">Copiez l’URL web et enregistrez l’ID de thread de conversation à partir de la chaîne.</span><span class="sxs-lookup"><span data-stu-id="e2b17-138">Copy the web URL and save the chat thread id from the string.</span></span>
<span data-ttu-id="e2b17-139">![ID de thread de conversation à partir de l’URL web.](../../assets/images/chat-thread-id.png)</span><span class="sxs-lookup"><span data-stu-id="e2b17-139">![Chat thread id from web URL.](../../assets/images/chat-thread-id.png)</span></span>

### <a name="use-postman"></a><span data-ttu-id="e2b17-140">Utiliser Postman</span><span class="sxs-lookup"><span data-stu-id="e2b17-140">Use Postman</span></span>

1. <span data-ttu-id="e2b17-141">Ouvrez [l’application Postman.](https://www.postman.com)</span><span class="sxs-lookup"><span data-stu-id="e2b17-141">Open the [Postman](https://www.postman.com) app.</span></span>
2. <span data-ttu-id="e2b17-142">Sélectionnez   >  **le fichier**  >  **d’importation de** fichiers pour télécharger le fichier JSON mis à jour à partir de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="e2b17-142">Select **File** > **Import** > **Import file** to upload the updated JSON file from your environment.</span></span>  
3. <span data-ttu-id="e2b17-143">Sélectionnez **l’onglet Collections.**</span><span class="sxs-lookup"><span data-stu-id="e2b17-143">Select the **Collections** tab.</span></span> 
4. <span data-ttu-id="e2b17-144">Sélectionnez le chevron en regard du test RSC pour développer l’affichage des **>** détails et afficher les demandes d’API. </span><span class="sxs-lookup"><span data-stu-id="e2b17-144">Select the chevron **>** next to the **Test RSC** to expand the details view and see the API requests.</span></span>

<span data-ttu-id="e2b17-145">Exécutez l’ensemble de la collection d’autorisations pour chaque appel d’API.</span><span class="sxs-lookup"><span data-stu-id="e2b17-145">Execute the entire permissions collection for each API call.</span></span> <span data-ttu-id="e2b17-146">Les autorisations que vous avez spécifiées dans le manifeste de votre application doivent réussir, tandis que celles qui ne sont pas spécifiées doivent échouer avec un code d’état HTTP 403.</span><span class="sxs-lookup"><span data-stu-id="e2b17-146">The permissions that you specified in your app manifest must succeed, while those not specified must fail with an HTTP 403 status code.</span></span> <span data-ttu-id="e2b17-147">Vérifiez tous les codes d’état de réponse pour vérifier que le comportement des autorisations RSC dans votre application répond aux attentes.</span><span class="sxs-lookup"><span data-stu-id="e2b17-147">Check all of the response status codes to confirm that the behavior of the RSC permissions in your app meet expectations.</span></span>

> [!NOTE]
> <span data-ttu-id="e2b17-148">Pour tester des appels d’API DELETE et READ spécifiques, ajoutez ces scénarios d’instance au fichier JSON.</span><span class="sxs-lookup"><span data-stu-id="e2b17-148">To test specific DELETE and READ API calls, add those instance scenarios to the JSON file.</span></span>

## <a name="test-revoked-rsc-permissions-using-postman"></a><span data-ttu-id="e2b17-149">Tester les autorisations RSC révoquées à l’aide [de Postman](https://www.postman.com/)</span><span class="sxs-lookup"><span data-stu-id="e2b17-149">Test revoked RSC permissions using [Postman](https://www.postman.com/)</span></span>

1. <span data-ttu-id="e2b17-150">Désinstallez l’application de la ressource spécifique.</span><span class="sxs-lookup"><span data-stu-id="e2b17-150">Uninstall the app from the specific resource.</span></span>
2. <span data-ttu-id="e2b17-151">Suivez les étapes pour la conversation ou l’équipe :</span><span class="sxs-lookup"><span data-stu-id="e2b17-151">Follow the steps for either chat or team:</span></span> 
    1. <span data-ttu-id="e2b17-152">[Test a ajouté des autorisations RSC à une équipe à l’aide de Postman](#test-added-rsc-permissions-to-a-team-using-the-postman-app).</span><span class="sxs-lookup"><span data-stu-id="e2b17-152">[Test added RSC permissions to a team using Postman](#test-added-rsc-permissions-to-a-team-using-the-postman-app).</span></span>
    2. <span data-ttu-id="e2b17-153">[Test a ajouté des autorisations RSC à une conversation à l’aide de Postman](#test-added-rsc-permissions-to-a-chat-using-the-postman-app).</span><span class="sxs-lookup"><span data-stu-id="e2b17-153">[Test added RSC permissions to a chat using Postman](#test-added-rsc-permissions-to-a-chat-using-the-postman-app).</span></span>
3. <span data-ttu-id="e2b17-154">Vérifiez tous les codes d’état de réponse pour confirmer que les appels d’API spécifiques ont échoué avec un code d’état **HTTP 403**.</span><span class="sxs-lookup"><span data-stu-id="e2b17-154">Check all the response status codes to confirm that the specific API calls **have failed with an HTTP 403 status code**.</span></span>

## <a name="see-also"></a><span data-ttu-id="e2b17-155">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="e2b17-155">See also</span></span>

[<span data-ttu-id="e2b17-156">API et Graph microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="e2b17-156">Microsoft Graph API and Teams</span></span>](/graph/api/resources/teams-api-overview?view=graph-rest-1.0&preserve-view=true)

