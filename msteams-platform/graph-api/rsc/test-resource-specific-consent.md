---
title: Test du consentement propre à une ressource dans teams
description: Détails de test de consentement propre à une ressource dans teams à l’aide de l’affranchissement
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: How-to
keywords: autorisation teams graphique des messages RSC
ms.openlocfilehash: c1c02c2ba0051193aa459d0df26fadfc9fa55550
ms.sourcegitcommit: fdc50183f3f4bec9e4b83bcfe5e016b591402f7c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/24/2020
ms.locfileid: "44867101"
---
# <a name="test-resource-specific-consent-permissions--in-teams"></a><span data-ttu-id="df2de-104">Tester les autorisations de consentement propres aux ressources dans teams</span><span class="sxs-lookup"><span data-stu-id="df2de-104">Test resource-specific consent permissions  in Teams</span></span>

<span data-ttu-id="df2de-105">Le consentement propre à la ressource (RSC) est une intégration de Microsoft teams et Graph API qui permet à votre application d’utiliser des points de terminaison d’API pour gérer des équipes spécifiques au sein d’une organisation.</span><span class="sxs-lookup"><span data-stu-id="df2de-105">Resource-specific consent (RSC) is a Microsoft Teams and Graph API integration that enables your app to use API endpoints to manage specific teams within an organization.</span></span> <span data-ttu-id="df2de-106">*Voir*[consentement propre à la ressource (RSC) — API Microsoft teams Graph](resource-specific-consent.md).  </span><span class="sxs-lookup"><span data-stu-id="df2de-106">Please *see*  [Resource-specific consent (RSC) — Microsoft Teams Graph API](resource-specific-consent.md).</span></span>

> [!NOTE]
><span data-ttu-id="df2de-107">Pour tester les autorisations RSC, votre fichier manifeste de l’application teams doit inclure une clé **webApplicationInfo** remplie avec les champs suivants :</span><span class="sxs-lookup"><span data-stu-id="df2de-107">To test the RSC permissions, your Teams app manifest file must include a **webApplicationInfo** key populated with the following fields:</span></span>
>
> - <span data-ttu-id="df2de-108">**ID** : votre ID d’application Azure ad, *consultez la rubrique* [enregistrer votre application dans le portail Azure ad](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span><span class="sxs-lookup"><span data-stu-id="df2de-108">**id**  — your Azure AD app id, *see* [Register your app in the Azure AD portal](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
> - <span data-ttu-id="df2de-109">**ressource** : n’importe quelle chaîne, *consultez* la remarque dans [mettre à jour votre manifeste d’application teams](resource-specific-consent.md#update-your-teams-app-manifest)</span><span class="sxs-lookup"><span data-stu-id="df2de-109">**resource**  — any string, *see* the note in  [Update your Teams app manifest](resource-specific-consent.md#update-your-teams-app-manifest)</span></span>
> - <span data-ttu-id="df2de-110">**autorisations des applications** — autorisations RSC pour votre application, *voir* [autorisations spécifiques aux ressources](resource-specific-consent.md#resource-specific-permissions).</span><span class="sxs-lookup"><span data-stu-id="df2de-110">**application permissions** — RSC permissions for  your app, *see* [Resource-specific Permissions](resource-specific-consent.md#resource-specific-permissions).</span></span>

```json
"webApplicationInfo":{
      "id":"XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
      "resource":"https://AnyString",
      "applicationPermissions":[
         "TeamSettings.Read.Group",
         "ChannelMessage.Read.Group",
         "TeamSettings.Edit.Group",
         "ChannelSettings.Edit.Group",
         "Channel.Create.Group",
         "Channel.Delete.Group",
         "TeamsApp.Read.Group",
         "TeamsTab.Read.Group",
         "TeamsTab.Create.Group",
         "TeamsTab.Edit.Group",
         "TeamsTab.Delete.Group",
         "Member.Read.Group",
         "Owner.Read.Group"
      ]
   }
```

>[!IMPORTANT]
><span data-ttu-id="df2de-111">Dans le manifeste de votre application, incluez uniquement les autorisations RSC dont vous souhaitez que votre application ait besoin.</span><span class="sxs-lookup"><span data-stu-id="df2de-111">In your app manifest, only include the RSC permissions that you want your app to have.</span></span>

## <a name="test-added-rsc-permissions-using-the-postman-app"></a><span data-ttu-id="df2de-112">Tester les autorisations RSC ajoutées à l’aide de l’application postale</span><span class="sxs-lookup"><span data-stu-id="df2de-112">Test added RSC permissions using the Postman app</span></span>

<span data-ttu-id="df2de-113">Pour vérifier si les autorisations RSC sont honorées par la charge utile de la demande d’API, vous devez copier le [Code de test JSON RSC](test-rsc-json-file.md) dans votre environnement local et mettre à jour les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="df2de-113">To check whether the RSC permissions are being honored by the API request payload, you'll need to copy the [RSC JSON test code](test-rsc-json-file.md) into your local environment and update the following values:</span></span>

1. <span data-ttu-id="df2de-114">`azureADAppId`: ID de l’application Azure AD de votre application.</span><span class="sxs-lookup"><span data-stu-id="df2de-114">`azureADAppId`  — your app's Azure AD app id.</span></span>
1. <span data-ttu-id="df2de-115">`azureADAppSecret`— votre code secret d’application Azure AD (mot de passe)</span><span class="sxs-lookup"><span data-stu-id="df2de-115">`azureADAppSecret`  — your Azure AD app secret (password)</span></span>
1. <span data-ttu-id="df2de-116">`teamGroupId`— vous pouvez obtenir l’ID de groupe d’équipe à partir du client teams comme suit :</span><span class="sxs-lookup"><span data-stu-id="df2de-116">`teamGroupId` — you can get the team group id from the Teams client as follows:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="df2de-117">Dans le client Teams, sélectionnez **teams** dans la barre de navigation la plus à gauche.</span><span class="sxs-lookup"><span data-stu-id="df2de-117">In the Teams client, select **Teams** from the far left nav bar .</span></span>
> * <span data-ttu-id="df2de-118">Dans le menu déroulant, sélectionnez l’équipe où l’application est installée.</span><span class="sxs-lookup"><span data-stu-id="df2de-118">Select the team where the app is installed from the dropdown menu.</span></span>
> * <span data-ttu-id="df2de-119">Sélectionnez l’icône **autres options** (&#8943;)</span><span class="sxs-lookup"><span data-stu-id="df2de-119">Select the **More options** icon (&#8943;)</span></span>
> * <span data-ttu-id="df2de-120">Sélectionnez **obtenir un lien vers une équipe**</span><span class="sxs-lookup"><span data-stu-id="df2de-120">Select **Get link to team**</span></span> 
> * <span data-ttu-id="df2de-121">Copiez et enregistrez la valeur **GroupID** à partir de la chaîne.</span><span class="sxs-lookup"><span data-stu-id="df2de-121">Copy and save the **groupId** value from the string.</span></span>

### <a name="using-postman"></a><span data-ttu-id="df2de-122">Utilisation de l’affranchissement</span><span class="sxs-lookup"><span data-stu-id="df2de-122">Using Postman</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="df2de-123">Ouvrez l’application [post](https://www.postman.com) .</span><span class="sxs-lookup"><span data-stu-id="df2de-123">Open the [Postman](https://www.postman.com) app.</span></span>
> * <span data-ttu-id="df2de-124">Sélectionnez **File**  =>  **fichier**  =>  d'**importation** d’importation de fichier pour télécharger le fichier JSON mis à jour à partir de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="df2de-124">Select **File** => **Import** => **Import file** to upload the updated JSON file from your environment.</span></span>  
> * <span data-ttu-id="df2de-125">Sélectionnez l’onglet **Collections** .</span><span class="sxs-lookup"><span data-stu-id="df2de-125">Select the **Collections** tab.</span></span> 
> * <span data-ttu-id="df2de-126">Sélectionnez le Chevron (>) en regard du **RSC de test** pour développer la vue des détails et voir les requêtes de l’API.</span><span class="sxs-lookup"><span data-stu-id="df2de-126">Select the chevron (>) next to the **Test RSC** to expand the details view and see the API requests.</span></span>

<span data-ttu-id="df2de-127">Exécutez toute la collection d’autorisations pour chaque appel d’API.</span><span class="sxs-lookup"><span data-stu-id="df2de-127">Execute the entire permissions collection for each API call.</span></span> <span data-ttu-id="df2de-128">Les autorisations que vous avez spécifiées dans votre manifeste de l’application doivent réussir, tandis que celles qui ne sont pas spécifiées doivent échouer avec un code d’état HTTP 403.</span><span class="sxs-lookup"><span data-stu-id="df2de-128">The permissions that you specified in your app manifest should succeed, while those not specified should fail with an HTTP 403 status code.</span></span> <span data-ttu-id="df2de-129">Vérifiez tous les codes d’état de réponse pour vous assurer que le comportement des autorisations RSC dans votre application répond aux attentes.</span><span class="sxs-lookup"><span data-stu-id="df2de-129">Check all of the response status codes to confirm that the behavior of the RSC permissions in your app meet expectations.</span></span>

>[!NOTE]
><span data-ttu-id="df2de-130">Pour tester des appels d’API de suppression et de lecture spécifiques, ajoutez ces scénarios d’instance au fichier JSON.</span><span class="sxs-lookup"><span data-stu-id="df2de-130">To test specific DELETE and READ API calls, please add those instance scenarios to the JSON file.</span></span>

## <a name="test--revoked-rsc-permissions-using-postman"></a><span data-ttu-id="df2de-131">Test des autorisations RSC révoquées à l’aide du [post](https://www.postman.com/)</span><span class="sxs-lookup"><span data-stu-id="df2de-131">Test  revoked RSC permissions using [Postman](https://www.postman.com/)</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="df2de-132">Désinstallez l’application de l’équipe spécifique.</span><span class="sxs-lookup"><span data-stu-id="df2de-132">Uninstall the app from the specific team.</span></span>
> * <span data-ttu-id="df2de-133">Suivez les étapes ci-dessus pour [tester les autorisations RSC ajoutées à l’aide de l’affranchissement](#test-added-rsc-permissions-using-the-postman-app).</span><span class="sxs-lookup"><span data-stu-id="df2de-133">Follow the steps above for [Test added RSC permissions using Postman](#test-added-rsc-permissions-using-the-postman-app).</span></span>
> * <span data-ttu-id="df2de-134">Vérifiez tous les codes d’état de réponse pour confirmer que les appels d’API spécifiques ayant réussi ont échoué avec un code d’état HTTP 403.</span><span class="sxs-lookup"><span data-stu-id="df2de-134">Check all of the response status codes to confirm that the specific API calls that succeeded have failed with an HTTP 403 status code.</span></span>

> [!div class="nextstepaction"]
>
> [<span data-ttu-id="df2de-135">En savoir plus sur l’API Graph et Teams</span><span class="sxs-lookup"><span data-stu-id="df2de-135">Learn more about the Graph API and Teams</span></span>](/graph/api/resources/teams-api-overview?view=graph-rest-1.0)
