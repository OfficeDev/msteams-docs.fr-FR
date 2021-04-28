---
title: Tester les autorisations de consentement spécifiques aux ressources dans Teams
description: Détails du test du consentement spécifique aux ressources dans Teams à l'aide de Postman
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: tutorial
keywords: Teams Authorization OAuth SSO AAD rsc Postman Graph
ms.openlocfilehash: 7f67df35954cd29810c387d05215eeec476a4ed4
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058326"
---
# <a name="test-resource-specific-consent-permissions-in-teams"></a><span data-ttu-id="eab81-104">Tester les autorisations de consentement spécifiques aux ressources dans Teams</span><span class="sxs-lookup"><span data-stu-id="eab81-104">Test resource-specific consent permissions in Teams</span></span>

<span data-ttu-id="eab81-105">Le consentement spécifique aux ressources (RSC) est une intégration d'API Microsoft Teams et Graph qui permet à votre application d'utiliser des points de terminaison d'API pour gérer des équipes spécifiques au sein d'une organisation.</span><span class="sxs-lookup"><span data-stu-id="eab81-105">Resource-specific consent (RSC) is a Microsoft Teams and Graph API integration that enables your app to use API endpoints to manage specific teams within an organization.</span></span> <span data-ttu-id="eab81-106">Pour plus d'informations, voir consentement spécifique aux [ressources (RSC) — API Microsoft Teams Graph](resource-specific-consent.md).</span><span class="sxs-lookup"><span data-stu-id="eab81-106">For more information, see [Resource-specific consent (RSC) — Microsoft Teams Graph API](resource-specific-consent.md).</span></span>

> [!NOTE]
> <span data-ttu-id="eab81-107">Pour tester les autorisations RSC, votre fichier manifeste d'application Teams doit inclure une clé **webApplicationInfo** remplie avec les champs suivants :</span><span class="sxs-lookup"><span data-stu-id="eab81-107">To test the RSC permissions, your Teams app manifest file must include a **webApplicationInfo** key populated with the following fields:</span></span>
>
> - <span data-ttu-id="eab81-108">**id :** votre ID d'application Azure AD, voir [Inscrire votre application dans le portail Azure AD.](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)</span><span class="sxs-lookup"><span data-stu-id="eab81-108">**id**: Your Azure AD app ID, see [Register your app in the Azure AD portal](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
> - <span data-ttu-id="eab81-109">**ressource**: n'importe quelle chaîne, voir la note dans [mettre à jour le manifeste de votre application Teams.](resource-specific-consent.md#update-your-teams-app-manifest)</span><span class="sxs-lookup"><span data-stu-id="eab81-109">**resource**: Any string, see the note in  [Update your Teams app manifest](resource-specific-consent.md#update-your-teams-app-manifest).</span></span>
> - <span data-ttu-id="eab81-110">**autorisations d'application**: autorisations RSC pour votre application, voir [Autorisations propres aux ressources.](resource-specific-consent.md#resource-specific-permissions)</span><span class="sxs-lookup"><span data-stu-id="eab81-110">**application permissions**: RSC permissions for  your app, see [Resource-specific Permissions](resource-specific-consent.md#resource-specific-permissions).</span></span>

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

> [!IMPORTANT]
> <span data-ttu-id="eab81-111">Dans le manifeste de votre application, incluez uniquement les autorisations RSC dont vous souhaitez que votre application soit propriétaire.</span><span class="sxs-lookup"><span data-stu-id="eab81-111">In your app manifest, only include the RSC permissions that you want your app to have.</span></span>

## <a name="test-added-rsc-permissions-using-the-postman-app"></a><span data-ttu-id="eab81-112">Test des autorisations RSC ajoutées à l'aide de l'application Postman</span><span class="sxs-lookup"><span data-stu-id="eab81-112">Test added RSC permissions using the Postman app</span></span>

<span data-ttu-id="eab81-113">Pour vérifier si les autorisations RSC sont honorées par la charge utile de demande d'API, vous devez copier le code de [test JSON RSC](test-rsc-json-file.md) dans votre environnement local et mettre à jour les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="eab81-113">To check whether the RSC permissions are being honored by the API request payload, you need to copy the [RSC JSON test code](test-rsc-json-file.md) into your local environment and update the following values:</span></span>

* <span data-ttu-id="eab81-114">`azureADAppId`: ID d'application Azure AD de votre application.</span><span class="sxs-lookup"><span data-stu-id="eab81-114">`azureADAppId`: Your app's Azure AD app ID.</span></span>
* <span data-ttu-id="eab81-115">`azureADAppSecret`: mot de passe de votre application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eab81-115">`azureADAppSecret`: Your Azure AD app password.</span></span>
* <span data-ttu-id="eab81-116">`token_scope`: l'étendue est requise pour obtenir un jeton.</span><span class="sxs-lookup"><span data-stu-id="eab81-116">`token_scope`: The scope is required to get a token.</span></span> <span data-ttu-id="eab81-117">définissez la valeur sur https://graph.microsoft.com/.default .</span><span class="sxs-lookup"><span data-stu-id="eab81-117">set the value to https://graph.microsoft.com/.default.</span></span>
* <span data-ttu-id="eab81-118">`teamGroupId`: vous pouvez obtenir l'ID de groupe d'équipe à partir du client Teams comme suit :</span><span class="sxs-lookup"><span data-stu-id="eab81-118">`teamGroupId`: You can get the team group id from the Teams client as follows:</span></span>

    1. <span data-ttu-id="eab81-119">Dans le client Teams, sélectionnez **Teams** dans la barre de navigation à l'extrême gauche.</span><span class="sxs-lookup"><span data-stu-id="eab81-119">In the Teams client, select **Teams** from the far left navigation bar.</span></span>
    2. <span data-ttu-id="eab81-120">Sélectionnez l'équipe où l'application est installée dans le menu déroulant.</span><span class="sxs-lookup"><span data-stu-id="eab81-120">Select the team where the app is installed from the dropdown menu.</span></span>
    3. <span data-ttu-id="eab81-121">Sélectionnez **l'icône Options** supplémentaires (&#8943;).</span><span class="sxs-lookup"><span data-stu-id="eab81-121">Select the **More options** icon (&#8943;).</span></span>
    4. <span data-ttu-id="eab81-122">Sélectionnez **Obtenir un lien vers l'équipe.**</span><span class="sxs-lookup"><span data-stu-id="eab81-122">Select **Get link to team**.</span></span> 
    5. <span data-ttu-id="eab81-123">Copiez et enregistrez **la valeur groupId** à partir de la chaîne.</span><span class="sxs-lookup"><span data-stu-id="eab81-123">Copy and save the **groupId** value from the string.</span></span>

### <a name="use-postman"></a><span data-ttu-id="eab81-124">Utiliser Postman</span><span class="sxs-lookup"><span data-stu-id="eab81-124">Use Postman</span></span>

1. <span data-ttu-id="eab81-125">Ouvrez [l'application Postman.](https://www.postman.com)</span><span class="sxs-lookup"><span data-stu-id="eab81-125">Open the [Postman](https://www.postman.com) app.</span></span>
2. <span data-ttu-id="eab81-126">Sélectionnez   >  **le fichier**  >  **d'importation de** fichiers pour télécharger le fichier JSON mis à jour à partir de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="eab81-126">Select **File** > **Import** > **Import file** to upload the updated JSON file from your environment.</span></span>  
3. <span data-ttu-id="eab81-127">Sélectionnez **l'onglet Collections.**</span><span class="sxs-lookup"><span data-stu-id="eab81-127">Select the **Collections** tab.</span></span> 
4. <span data-ttu-id="eab81-128">Sélectionnez le chevron en regard du test RSC pour développer l'affichage des **>** détails et afficher les demandes d'API. </span><span class="sxs-lookup"><span data-stu-id="eab81-128">Select the chevron **>** next to the **Test RSC** to expand the details view and see the API requests.</span></span>

<span data-ttu-id="eab81-129">Exécutez l'ensemble de la collection d'autorisations pour chaque appel d'API.</span><span class="sxs-lookup"><span data-stu-id="eab81-129">Execute the entire permissions collection for each API call.</span></span> <span data-ttu-id="eab81-130">Les autorisations que vous avez spécifiées dans le manifeste de votre application doivent réussir, tandis que celles qui ne sont pas spécifiées doivent échouer avec un code d'état HTTP 403.</span><span class="sxs-lookup"><span data-stu-id="eab81-130">The permissions that you specified in your app manifest must succeed, while those not specified must fail with an HTTP 403 status code.</span></span> <span data-ttu-id="eab81-131">Vérifiez tous les codes d'état de réponse pour vérifier que le comportement des autorisations RSC dans votre application répond aux attentes.</span><span class="sxs-lookup"><span data-stu-id="eab81-131">Check all of the response status codes to confirm that the behavior of the RSC permissions in your app meet expectations.</span></span>

> [!NOTE]
> <span data-ttu-id="eab81-132">Pour tester des appels d'API DELETE et READ spécifiques, ajoutez ces scénarios d'instance au fichier JSON.</span><span class="sxs-lookup"><span data-stu-id="eab81-132">To test specific DELETE and READ API calls, add those instance scenarios to the JSON file.</span></span>

## <a name="test-revoked-rsc-permissions-using-postman"></a><span data-ttu-id="eab81-133">Tester les autorisations RSC révoquées à l'aide [de Postman](https://www.postman.com/)</span><span class="sxs-lookup"><span data-stu-id="eab81-133">Test revoked RSC permissions using [Postman](https://www.postman.com/)</span></span>

1. <span data-ttu-id="eab81-134">Désinstallez l'application de l'équipe spécifique.</span><span class="sxs-lookup"><span data-stu-id="eab81-134">Uninstall the app from the specific team.</span></span>
2. <span data-ttu-id="eab81-135">Suivez les étapes pour [tester les autorisations RSC ajoutées à l'aide de Postman](#test-added-rsc-permissions-using-the-postman-app).</span><span class="sxs-lookup"><span data-stu-id="eab81-135">Follow the steps for [Test added RSC permissions using Postman](#test-added-rsc-permissions-using-the-postman-app).</span></span>
3. <span data-ttu-id="eab81-136">Vérifiez tous les codes d'état de réponse pour confirmer que les appels d'API spécifiques, qui ont réussi, ont échoué avec un code d'état **HTTP 403**.</span><span class="sxs-lookup"><span data-stu-id="eab81-136">Check all the response status codes to confirm that the specific API calls, **succeeded, have failed with an HTTP 403 status code**.</span></span>

## <a name="see-also"></a><span data-ttu-id="eab81-137">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="eab81-137">See also</span></span>

- [<span data-ttu-id="eab81-138">API Microsoft Graph et Teams</span><span class="sxs-lookup"><span data-stu-id="eab81-138">Microsoft Graph API and Teams</span></span>](/graph/api/resources/teams-api-overview?view=graph-rest-1.0&preserve-view=true)

