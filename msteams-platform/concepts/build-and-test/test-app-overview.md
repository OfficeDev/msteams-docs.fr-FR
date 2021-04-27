---
title: Tester la vue d'ensemble de votre application
description: Décrit le processus de test de votre application personnalisée Teams dans Microsoft 365
ms.topic: how-to
localization_priority: Normal
keywords: Configurer microsoft 365 client Teams téléchargeant l'application de test
ms.openlocfilehash: 8815e73c054cb75782660ef4afb3ae583b4f40fa
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019936"
---
# <a name="test-your-app"></a><span data-ttu-id="07474-104">Tester votre application</span><span class="sxs-lookup"><span data-stu-id="07474-104">Test your app</span></span>

<span data-ttu-id="07474-105">Après avoir intégré votre application à Microsoft Teams, vous devez la tester avant de la publier.</span><span class="sxs-lookup"><span data-stu-id="07474-105">After integrating your app with Microsoft Teams, you must test your app before publishing it.</span></span> <span data-ttu-id="07474-106">L'objectif ultime est d'obtenir autant d'utilisateurs pour votre application, par conséquent, veillez à tester l'application sur plusieurs appareils que les utilisateurs peuvent utiliser.</span><span class="sxs-lookup"><span data-stu-id="07474-106">The ultimate goal is to get as many users for your app, therefore, ensure to test the app on multiple devices that users could use.</span></span> <span data-ttu-id="07474-107">Pour tester votre application :</span><span class="sxs-lookup"><span data-stu-id="07474-107">For testing your app:</span></span>

* <span data-ttu-id="07474-108">Préparer votre client Microsoft Office 365</span><span class="sxs-lookup"><span data-stu-id="07474-108">Prepare your Microsoft 365 tenant</span></span>
* <span data-ttu-id="07474-109">Choisir un espace de travail pour tester et déboguer votre application</span><span class="sxs-lookup"><span data-stu-id="07474-109">Choose a workspace to test and debug your app</span></span>
* <span data-ttu-id="07474-110">Ajouter des données de test à votre client Microsoft 365</span><span class="sxs-lookup"><span data-stu-id="07474-110">Add test data to your Microsoft 365 tenant</span></span>

## <a name="prepare-your-microsoft-365-tenant"></a><span data-ttu-id="07474-111">Préparer votre client Microsoft Office 365</span><span class="sxs-lookup"><span data-stu-id="07474-111">Prepare your Microsoft 365 tenant</span></span>

<span data-ttu-id="07474-112">Avant de commencer à tester votre application, préparez votre client de test Microsoft 365 et activez l'application Teams personnalisée pour charger votre application.</span><span class="sxs-lookup"><span data-stu-id="07474-112">Before you start testing your app, prepare your Microsoft 365 test tenant and enable custom Teams app allow you to upload your app.</span></span> <span data-ttu-id="07474-113">Vous devez vous inscrire au programme pour les développeurs Microsoft 365 et gérer les paramètres Teams de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="07474-113">You must sign-up for Microsoft 365 developer program and manage the Teams settings for your organization.</span></span> <span data-ttu-id="07474-114">Configurez votre abonnement développeur et configurez-le par le biais de la préparation de [votre client Microsoft 365.](~/concepts/build-and-test/prepare-your-o365-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="07474-114">Set up your developer subscription and configure it through [prepare your Microsoft 365 Tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>

## <a name="test-and-debug"></a><span data-ttu-id="07474-115">Test et débogage</span><span class="sxs-lookup"><span data-stu-id="07474-115">Test and debug</span></span>

<span data-ttu-id="07474-116">Pour tester et déboguer votre application, vous devez créer au moins un espace de travail.</span><span class="sxs-lookup"><span data-stu-id="07474-116">To test and debug your app, you must create at least one workspace.</span></span> <span data-ttu-id="07474-117">Vous pouvez sélectionner une configuration de test, par exemple un hôte local ou un hôte basé sur le cloud pour tester et déboguer l'application.</span><span class="sxs-lookup"><span data-stu-id="07474-117">You can select a test setup, such as local host or cloud-based host to test and debug the app.</span></span> <span data-ttu-id="07474-118">Des conseils pour déboguer votre application Teams sont fournis pour charger et exécuter votre expérience d'application.</span><span class="sxs-lookup"><span data-stu-id="07474-118">Guidance to debug your Teams app is provided to load and run your app experience.</span></span> <span data-ttu-id="07474-119">Pour plus d'informations, [voir choisir une application de mise en place et d'exécuter votre application Microsoft Teams.](~/concepts/build-and-test/debug.md)</span><span class="sxs-lookup"><span data-stu-id="07474-119">For more information, see [choose a set up and run your Microsoft Teams app](~/concepts/build-and-test/debug.md).</span></span>

<span data-ttu-id="07474-120">Testez votre bot localement.</span><span class="sxs-lookup"><span data-stu-id="07474-120">Test your bot locally.</span></span> <span data-ttu-id="07474-121">Pour plus d'informations, voir [déboguer votre bot localement avec un IDE.](~/bots/how-to/debug/locally-with-an-ide.md)</span><span class="sxs-lookup"><span data-stu-id="07474-121">For more information, see [debug your bot locally with an IDE](~/bots/how-to/debug/locally-with-an-ide.md).</span></span> <span data-ttu-id="07474-122">Vous pouvez également déboguer votre bot avec des logiciels [intermédiaires d'inspection](/azure/bot-service/bot-service-debug-inspection-middleware?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) et des [outils adaptatifs.](/azure/bot-service/bot-service-debug-adaptive-tools?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="07474-122">You can also debug your bot with [inspection middleware](/azure/bot-service/bot-service-debug-inspection-middleware?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) and [adaptive tools](/azure/bot-service/bot-service-debug-adaptive-tools?view=azure-bot-service-4.0&preserve-view=true).</span></span> 

<span data-ttu-id="07474-123">Pour afficher les journaux de la console, afficher ou modifier des requêtes html, css et réseau pendant l'runtime, ajoutez des points d'arrêt à votre code JavaScript et effectuez un débogage interactif pour accéder aux DevTools.</span><span class="sxs-lookup"><span data-stu-id="07474-123">To view the console logs, view or modify html, css, and network requests during runtime, add breakpoints to your JavaScript code, and perform interactive debugging access the DevTools.</span></span> <span data-ttu-id="07474-124">Pour plus d'informations, [voir Accéder aux onglets DevTools pour Teams.](~/tabs/how-to/developer-tools.md)</span><span class="sxs-lookup"><span data-stu-id="07474-124">For more information, see [Access the DevTools for Teams tabs](~/tabs/how-to/developer-tools.md).</span></span> 

## <a name="add-test-data-to-your-microsoft-365-tenant"></a><span data-ttu-id="07474-125">Ajouter des données de test à votre client Microsoft 365</span><span class="sxs-lookup"><span data-stu-id="07474-125">Add test data to your Microsoft 365 tenant</span></span>

<span data-ttu-id="07474-126">Ajoutez les données de test au client de test Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="07474-126">Add the test data to Microsoft 365 test tenant.</span></span> <span data-ttu-id="07474-127">Pour plus d'informations, voir ajouter des données de test à votre client [test Office 365](~/concepts/build-and-test/test-data.md)et remplir toutes les conditions préalables avant de commencer à télécharger vos données de test.</span><span class="sxs-lookup"><span data-stu-id="07474-127">For more information, see [add test data to your Office 365 test tenant](~/concepts/build-and-test/test-data.md), and complete all the prerequisites before you start uploading your test data.</span></span>

## <a name="see-also"></a><span data-ttu-id="07474-128">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="07474-128">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="07474-129">Déboguer votre onglet</span><span class="sxs-lookup"><span data-stu-id="07474-129">Debug your tab</span></span>](~/tabs/how-to/developer-tools.md)
 
> [!div class="nextstepaction"]
> [<span data-ttu-id="07474-130">Déboguer vos bots</span><span class="sxs-lookup"><span data-stu-id="07474-130">Debug your bots</span></span>](~/bots/how-to/debug/locally-with-an-ide.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="07474-131">Tester les autorisations RSC</span><span class="sxs-lookup"><span data-stu-id="07474-131">Test RSC permissions</span></span>](~/graph-api/rsc/test-resource-specific-consent.md)

## <a name="next-step"></a><span data-ttu-id="07474-132">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="07474-132">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="07474-133">Préparer votre client Microsoft Office 365</span><span class="sxs-lookup"><span data-stu-id="07474-133">Prepare your Microsoft 365 tenant</span></span>](~/concepts/build-and-test/prepare-your-o365-tenant.md)
