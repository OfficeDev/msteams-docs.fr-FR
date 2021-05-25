---
title: Tester la vue d’ensemble de votre application
description: Décrit le processus de test de votre application Teams personnalisée dans Microsoft 365
ms.topic: how-to
localization_priority: Normal
keywords: Configurer Microsoft 365 client Teams l’application de test
ms.openlocfilehash: 37f917727aba1a0f9828434b1519b4bb787df7aa
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/24/2021
ms.locfileid: "52631005"
---
# <a name="test-your-app"></a><span data-ttu-id="d11f7-104">Tester votre application</span><span class="sxs-lookup"><span data-stu-id="d11f7-104">Test your app</span></span>

<span data-ttu-id="d11f7-105">Après avoir intégré votre application à Microsoft Teams, vous devez la tester avant de la publier.</span><span class="sxs-lookup"><span data-stu-id="d11f7-105">After integrating your app with Microsoft Teams, you must test your app before publishing it.</span></span> <span data-ttu-id="d11f7-106">L’objectif ultime est d’obtenir autant d’utilisateurs pour votre application, par conséquent, veillez à tester l’application sur plusieurs appareils que les utilisateurs peuvent utiliser.</span><span class="sxs-lookup"><span data-stu-id="d11f7-106">The ultimate goal is to get as many users for your app, therefore, ensure to test the app on multiple devices that users could use.</span></span> <span data-ttu-id="d11f7-107">Pour tester votre application :</span><span class="sxs-lookup"><span data-stu-id="d11f7-107">For testing your app:</span></span>

* <span data-ttu-id="d11f7-108">Préparez votre Microsoft 365 client.</span><span class="sxs-lookup"><span data-stu-id="d11f7-108">Prepare your Microsoft 365 tenant.</span></span>
* <span data-ttu-id="d11f7-109">Choisissez un espace de travail pour tester et déboguer votre application.</span><span class="sxs-lookup"><span data-stu-id="d11f7-109">Choose a workspace to test and debug your app.</span></span>
* <span data-ttu-id="d11f7-110">Ajoutez des données de test à Microsoft 365 client.</span><span class="sxs-lookup"><span data-stu-id="d11f7-110">Add test data to your Microsoft 365 tenant.</span></span>

## <a name="prepare-your-microsoft-365-tenant"></a><span data-ttu-id="d11f7-111">Préparer votre client Microsoft Office 365</span><span class="sxs-lookup"><span data-stu-id="d11f7-111">Prepare your Microsoft 365 tenant</span></span>

<span data-ttu-id="d11f7-112">Avant de commencer à tester votre application, préparez votre client de test Microsoft 365 et activez l’application Teams personnalisée vous permet de télécharger votre application.</span><span class="sxs-lookup"><span data-stu-id="d11f7-112">Before you start testing your app, prepare your Microsoft 365 test tenant and enable custom Teams app allow you to upload your app.</span></span> <span data-ttu-id="d11f7-113">Vous devez vous inscrire au programme Microsoft 365 développeur et gérer les paramètres Teams de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="d11f7-113">You must sign-up for Microsoft 365 developer program and manage the Teams settings for your organization.</span></span> <span data-ttu-id="d11f7-114">Configurez votre abonnement développeur et configurez-le par le biais de [la préparation Microsoft 365 client.](~/concepts/build-and-test/prepare-your-o365-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="d11f7-114">Set up your developer subscription and configure it through [prepare your Microsoft 365 Tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

## <a name="test-and-debug"></a><span data-ttu-id="d11f7-115">Test et débogage</span><span class="sxs-lookup"><span data-stu-id="d11f7-115">Test and debug</span></span>

<span data-ttu-id="d11f7-116">Pour tester et déboguer votre application, vous devez créer au moins un espace de travail.</span><span class="sxs-lookup"><span data-stu-id="d11f7-116">To test and debug your app, you must create at least one workspace.</span></span> <span data-ttu-id="d11f7-117">Vous pouvez sélectionner une configuration de test, par exemple un hôte local ou un hôte basé sur le cloud pour tester et déboguer l’application.</span><span class="sxs-lookup"><span data-stu-id="d11f7-117">You can select a test setup, such as local host or cloud-based host to test and debug the app.</span></span> <span data-ttu-id="d11f7-118">Des conseils pour déboguer votre Teams application sont fournis pour charger et exécuter votre expérience d’application.</span><span class="sxs-lookup"><span data-stu-id="d11f7-118">Guidance to debug your Teams app is provided to load and run your app experience.</span></span> <span data-ttu-id="d11f7-119">Pour plus d’informations, [voir choisir une application de Microsoft Teams.](~/concepts/build-and-test/debug.md)</span><span class="sxs-lookup"><span data-stu-id="d11f7-119">For more information, see [choose a set up and run your Microsoft Teams app](~/concepts/build-and-test/debug.md).</span></span>

<span data-ttu-id="d11f7-120">Testez votre bot localement.</span><span class="sxs-lookup"><span data-stu-id="d11f7-120">Test your bot locally.</span></span> <span data-ttu-id="d11f7-121">Pour plus d’informations, voir [déboguer votre bot localement avec un IDE.](~/bots/how-to/debug/locally-with-an-ide.md)</span><span class="sxs-lookup"><span data-stu-id="d11f7-121">For more information, see [debug your bot locally with an IDE](~/bots/how-to/debug/locally-with-an-ide.md).</span></span> <span data-ttu-id="d11f7-122">Vous pouvez également déboguer votre bot avec des logiciels [intermédiaires d’inspection](/azure/bot-service/bot-service-debug-inspection-middleware?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) et des [outils adaptatifs.](/azure/bot-service/bot-service-debug-adaptive-tools?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="d11f7-122">You can also debug your bot with [inspection middleware](/azure/bot-service/bot-service-debug-inspection-middleware?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) and [adaptive tools](/azure/bot-service/bot-service-debug-adaptive-tools?view=azure-bot-service-4.0&preserve-view=true).</span></span> 

<span data-ttu-id="d11f7-123">Pour afficher les journaux de la console, afficher ou modifier des requêtes html, css et réseau pendant l’runtime, ajoutez des points d’arrêt à votre code JavaScript et effectuez un débogage interactif pour accéder aux DevTools.</span><span class="sxs-lookup"><span data-stu-id="d11f7-123">To view the console logs, view or modify html, css, and network requests during runtime, add breakpoints to your JavaScript code, and perform interactive debugging access the DevTools.</span></span> <span data-ttu-id="d11f7-124">Pour plus d’informations, [voir Access the DevTools for Teams tabs](~/tabs/how-to/developer-tools.md).</span><span class="sxs-lookup"><span data-stu-id="d11f7-124">For more information, see [Access the DevTools for Teams tabs](~/tabs/how-to/developer-tools.md).</span></span> 

## <a name="add-test-data-to-your-microsoft-365-tenant"></a><span data-ttu-id="d11f7-125">Ajouter des données de test à votre client Microsoft 365 client</span><span class="sxs-lookup"><span data-stu-id="d11f7-125">Add test data to your Microsoft 365 tenant</span></span>

<span data-ttu-id="d11f7-126">Ajoutez les données de test Microsoft 365 client test.</span><span class="sxs-lookup"><span data-stu-id="d11f7-126">Add the test data to Microsoft 365 test tenant.</span></span> <span data-ttu-id="d11f7-127">Pour plus d’informations, voir ajouter des données de test à [votre client de test Office 365](~/concepts/build-and-test/test-data.md)et remplir toutes les conditions préalables avant de commencer à télécharger vos données de test.</span><span class="sxs-lookup"><span data-stu-id="d11f7-127">For more information, see [add test data to your Office 365 test tenant](~/concepts/build-and-test/test-data.md), and complete all the prerequisites before you start uploading your test data.</span></span>

## <a name="see-also"></a><span data-ttu-id="d11f7-128">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="d11f7-128">See also</span></span>

* [<span data-ttu-id="d11f7-129">Déboguer votre onglet</span><span class="sxs-lookup"><span data-stu-id="d11f7-129">Debug your tab</span></span>](~/tabs/how-to/developer-tools.md)
* [<span data-ttu-id="d11f7-130">Déboguer vos bots</span><span class="sxs-lookup"><span data-stu-id="d11f7-130">Debug your bots</span></span>](~/bots/how-to/debug/locally-with-an-ide.md)
* [<span data-ttu-id="d11f7-131">Tester les autorisations RSC</span><span class="sxs-lookup"><span data-stu-id="d11f7-131">Test RSC permissions</span></span>](~/graph-api/rsc/test-resource-specific-consent.md)

## <a name="next-step"></a><span data-ttu-id="d11f7-132">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="d11f7-132">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d11f7-133">Préparer votre client Microsoft Office 365</span><span class="sxs-lookup"><span data-stu-id="d11f7-133">Prepare your Microsoft 365 tenant</span></span>](~/concepts/build-and-test/prepare-your-o365-tenant.md)
