---
title: Authentification unique avec teams Shared Computer Toolkit et Visual Studio code d'authentification unique pour les onglets
description: Créez un onglet qui prend en charge l' sign-on unique et les appels Microsoft Graph directement dans Visual Studio Code avec le Shared Computer Toolkit Microsoft Teams
keywords: teams visual studio code toolkit tabs sso graph authentication Azure identity platform
localization_priority: Normal
ms.topic: how-to
ms.author: lajanuar
ms.openlocfilehash: daf9a1b0bb64fee9584d0f58d749cf2b1ccaa4ef
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52018424"
---
# <a name="single-sign-on-authentication-with-teams-toolkit-and-visual-studio-code-for-tabs"></a><span data-ttu-id="e5e76-104">Authentification unique avec teams Shared Computer Toolkit et Visual Studio code d'authentification unique pour les onglets</span><span class="sxs-lookup"><span data-stu-id="e5e76-104">Single sign-on authentication with Teams Toolkit and Visual Studio Code for tabs</span></span>

<span data-ttu-id="e5e76-105">L'Shared Computer Toolkit Microsoft Teams vous permet de créer une authentification unique (SSO) pour les applications d'onglet directement dans Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="e5e76-105">The Microsoft Teams Toolkit enables you to create single sign-on (SSO) authentication  for tab apps directly within Visual Studio Code.</span></span> <span data-ttu-id="e5e76-106">Le kit de ressources vous guide tout au long du processus et fournit tout ce dont vous avez besoin, y compris la mise en service de votre inscription de plateforme d'identités Microsoft dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e5e76-106">The toolkit guides you through the process and provides everything you need including provisioning your Microsoft identity platform registration in the Azure portal.</span></span>

## <a name="get-started--create-a-project"></a><span data-ttu-id="e5e76-107">Mise en place : créer un projet</span><span class="sxs-lookup"><span data-stu-id="e5e76-107">Get started — create a project</span></span>

1. <span data-ttu-id="e5e76-108">Créez un projet dans le kit de ressources.</span><span class="sxs-lookup"><span data-stu-id="e5e76-108">Create a new project in the toolkit.</span></span>
1. <span data-ttu-id="e5e76-109">Sélectionnez l'onglet comme type d'extension que vous souhaitez créer.</span><span class="sxs-lookup"><span data-stu-id="e5e76-109">Select tab as the type of extension you'd like to create.</span></span>
1. <span data-ttu-id="e5e76-110">Sélectionnez l'option de prise en charge de l' sso.</span><span class="sxs-lookup"><span data-stu-id="e5e76-110">Select the option to support SSO.</span></span>

> [!TIP]
> <span data-ttu-id="e5e76-111">Après l'installation, les équipes doivent s'Shared Computer Toolkit dans la barre Visual Studio'activité code.</span><span class="sxs-lookup"><span data-stu-id="e5e76-111">After installation, you should see the Teams Toolkit in the Visual Studio Code activity bar.</span></span> <span data-ttu-id="e5e76-112">Si ce n'est pas le cas, cliquez avec le bouton droit dans la barre d'activité et sélectionnez **Microsoft Teams** pour épingler le kit de ressources pour un accès facile.</span><span class="sxs-lookup"><span data-stu-id="e5e76-112">If not, right-click within the activity bar and select **Microsoft Teams** to pin the toolkit for easy access.</span></span>

## <a name="configure-your-project"></a><span data-ttu-id="e5e76-113">Configurer votre projet</span><span class="sxs-lookup"><span data-stu-id="e5e76-113">Configure your project</span></span>

1. <span data-ttu-id="e5e76-114">Pour activer l' utilisateur sso dans Teams, votre application doit avoir une ressource d'inscription d'application Azure.</span><span class="sxs-lookup"><span data-stu-id="e5e76-114">To enable SSO within Teams, your app must have an Azure app registration resource.</span></span> <span data-ttu-id="e5e76-115">L'Shared Computer Toolkit Teams va fournir l'inscription de l'application en votre nom.</span><span class="sxs-lookup"><span data-stu-id="e5e76-115">The Teams Toolkit will provision the app registration on your behalf.</span></span>
1. <span data-ttu-id="e5e76-116">Entrez l'URL où votre application sera hébergée et sélectionnez **ensuite.**</span><span class="sxs-lookup"><span data-stu-id="e5e76-116">Enter the URL where your app will be hosted and select **next**.</span></span> <span data-ttu-id="e5e76-117">L'inscription de votre application sera configurée à l'aide de l'URL fournie.</span><span class="sxs-lookup"><span data-stu-id="e5e76-117">Your app registration will be configured using the provided URL.</span></span>
1. <span data-ttu-id="e5e76-118">Les détails de configuration de l'inscription de l'application sont stockés dans les fichiers du `.env` code source de votre projet.</span><span class="sxs-lookup"><span data-stu-id="e5e76-118">The app registration's configuration details will be stored in the `.env` files in your project's source code.</span></span>

<span data-ttu-id="e5e76-119">Si vous souhaitez en savoir plus sur la façon  dont l'inscription de votre application Azure sera mise en service, consultez notre prise en charge de l' [sign-on unique (SSO)](../tabs/how-to/authentication/auth-aad-sso.md) pour la documentation sur les onglets.</span><span class="sxs-lookup"><span data-stu-id="e5e76-119">If you would like to learn more about how your Azure app registration will be provisioned, please _see_  our [single sign-on (SSO) support for tabs](../tabs/how-to/authentication/auth-aad-sso.md) documentation.</span></span>

> [!TIP]
> <span data-ttu-id="e5e76-120">Vous devrez accéder à **Azure App Registrations** et  mettre à jour votre *URI d'API* et rediriger les URL chaque fois que vous modifiez cette URL.</span><span class="sxs-lookup"><span data-stu-id="e5e76-120">You will need to go to **Azure App Registrations** and update your *API URI* and *redirect URLs* whenever you change this URL.</span></span>

## <a name="run-your-project"></a><span data-ttu-id="e5e76-121">Exécuter votre projet</span><span class="sxs-lookup"><span data-stu-id="e5e76-121">Run your project</span></span>

1. <span data-ttu-id="e5e76-122">Sélectionnez **npm installer** dans le `api-server` dossier.</span><span class="sxs-lookup"><span data-stu-id="e5e76-122">Select **npm install** from the `api-server` folder.</span></span> <span data-ttu-id="e5e76-123">Puis **npm start**.</span><span class="sxs-lookup"><span data-stu-id="e5e76-123">Then **npm start**.</span></span>
1. <span data-ttu-id="e5e76-124">Sélectionnez **l'installation npm** dans le `.src` dossier.</span><span class="sxs-lookup"><span data-stu-id="e5e76-124">Select **npm install** from the `.src` folder.</span></span> <span data-ttu-id="e5e76-125">Puis **npm start**.</span><span class="sxs-lookup"><span data-stu-id="e5e76-125">Then **npm start**.</span></span>
1. <span data-ttu-id="e5e76-126">Si vous utilisez un service de tunneling comme [ngrok,](https://ngrok.com/)exécutez-le et assurez-vous que l'URL correspond à ce que vous avez entré dans l'Assistant création de projet.</span><span class="sxs-lookup"><span data-stu-id="e5e76-126">If you are using a tunneling service like [ngrok](https://ngrok.com/), run it and make sure the URL matches with what you entered in the project creation wizard.</span></span> <span data-ttu-id="e5e76-127">Si ce n'est pas le cas, vous devrez mettre à jour votre _URI d'API_ et _rediriger l'URL_ dans l'inscription de l'application qui a été créée dans Azure.</span><span class="sxs-lookup"><span data-stu-id="e5e76-127">If it doesn't, you will need to update your _API URI_ and _redirect URL_ in the app registration that was created in Azure.</span></span>
1. <span data-ttu-id="e5e76-128">Accédez à la barre d'activité sur le côté gauche de la Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="e5e76-128">Navigate to the activity bar on the left side of the Visual Studio Code window.</span></span>
1. <span data-ttu-id="e5e76-129">Sélectionnez **l'icône** Exécuter pour afficher **l'affichage Exécuter et déboguer.**</span><span class="sxs-lookup"><span data-stu-id="e5e76-129">Select the **Run** icon to display the **Run and Debug** view.</span></span>
1. <span data-ttu-id="e5e76-130">Vous pouvez également utiliser le raccourci clavier **Ctrl+Shift+D**.</span><span class="sxs-lookup"><span data-stu-id="e5e76-130">You can also use the keyboard shortcut **Ctrl+Shift+D**.</span></span>

> [!TIP]
> <span data-ttu-id="e5e76-131">Vous ne verrez peut-être pas le dialogue d'installation de l'application dans le navigateur si les fenêtres pop-up sont désactivées pour votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="e5e76-131">You may not see the app install dialogue in the browser if pop-up windows are disabled for your browser.</span></span> <span data-ttu-id="e5e76-132">Si cela se produit, activez les fenêtres pop-up et actualisez la page.</span><span class="sxs-lookup"><span data-stu-id="e5e76-132">If this happens, enable pop-up windows and refresh the page.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e5e76-133">En savoir plus : créer des applications avec le code Shared Computer Toolkit et Visual Studio Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="e5e76-133">Learn more: Build apps with the Microsoft Teams Toolkit and Visual Studio Code</span></span>](visual-studio-code-overview.md)
