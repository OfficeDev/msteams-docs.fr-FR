---
title: Authentification unique avec Team Toolkit et Visual Studio code pour les onglets
description: Créer un onglet qui prend en charge les appels d’authentification unique et Microsoft Graph directement dans Visual Studio code avec Microsoft teams Toolkit
keywords: Visual Studio code Toolkit (onglets de la boîte à outils d’authentification par graphique SSO)
ms.topic: how-to
ms.author: lajanuar
ms.openlocfilehash: fe734143975688cd35c510cd68cd0779a2200a18
ms.sourcegitcommit: 7e47bf158249050c36d97509eea00e77089a54e6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/30/2020
ms.locfileid: "49477733"
---
# <a name="single-sign-on-authentication-with-teams-toolkit-and-visual-studio-code-for-tabs"></a><span data-ttu-id="8ee02-104">Authentification unique avec Team Toolkit et Visual Studio code pour les onglets</span><span class="sxs-lookup"><span data-stu-id="8ee02-104">Single sign-on authentication with Teams Toolkit and Visual Studio Code for tabs</span></span>

<span data-ttu-id="8ee02-105">Le kit de développement Microsoft teams vous permet de créer une authentification unique (SSO) pour les applications d’onglet directement dans Visual Studio code.</span><span class="sxs-lookup"><span data-stu-id="8ee02-105">The Microsoft Teams Toolkit enables you to create single sign-on (SSO) authentication  for tab apps directly within Visual Studio Code.</span></span> <span data-ttu-id="8ee02-106">Le kit de connaissances vous guide tout au long du processus et vous fournit tout ce dont vous avez besoin, notamment la mise en service de votre enregistrement de plateforme d’identité Microsoft dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8ee02-106">The toolkit guides you through the process and provides everything you need including provisioning your Microsoft identity platform registration in the Azure portal.</span></span>

## <a name="get-started--create-a-project"></a><span data-ttu-id="8ee02-107">Prise en main : créer un projet</span><span class="sxs-lookup"><span data-stu-id="8ee02-107">Get started — create a project</span></span>

1. <span data-ttu-id="8ee02-108">Créez un projet dans la boîte à outils.</span><span class="sxs-lookup"><span data-stu-id="8ee02-108">Create a new project in the toolkit.</span></span>
1. <span data-ttu-id="8ee02-109">Sélectionnez l’onglet comme type d’extension que vous souhaitez créer.</span><span class="sxs-lookup"><span data-stu-id="8ee02-109">Select tab as the type of extension you'd like to create.</span></span>
1. <span data-ttu-id="8ee02-110">Sélectionnez l’option permettant de prendre en charge l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="8ee02-110">Select the option to support SSO.</span></span>

> [!TIP]
> <span data-ttu-id="8ee02-111">Après l’installation, vous devriez voir la boîte à outils teams dans la barre d’activité code Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8ee02-111">After installation, you should see the Teams Toolkit in the Visual Studio Code activity bar.</span></span> <span data-ttu-id="8ee02-112">Si ce n’est pas le cas, cliquez avec le bouton droit de la barre d’activité et sélectionnez **Microsoft teams** pour épingler la boîte à outils pour un accès facile.</span><span class="sxs-lookup"><span data-stu-id="8ee02-112">If not, right-click within the activity bar and select **Microsoft Teams** to pin the toolkit for easy access.</span></span>

## <a name="configure-your-project"></a><span data-ttu-id="8ee02-113">Configurer votre projet</span><span class="sxs-lookup"><span data-stu-id="8ee02-113">Configure your project</span></span>

1. <span data-ttu-id="8ee02-114">Pour activer l’authentification unique (SSO) dans Teams, votre application doit disposer d’une ressource d’inscription Azure App.</span><span class="sxs-lookup"><span data-stu-id="8ee02-114">To enable SSO within Teams, your app must have an Azure app registration resource.</span></span> <span data-ttu-id="8ee02-115">La boîte à outils teams configurera l’inscription de l’application en votre nom.</span><span class="sxs-lookup"><span data-stu-id="8ee02-115">The Teams Toolkit will provision the app registration on your behalf.</span></span>
1. <span data-ttu-id="8ee02-116">Entrez l’URL où votre application sera hébergée et cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="8ee02-116">Enter the URL where your app will be hosted and select **next**.</span></span> <span data-ttu-id="8ee02-117">L’inscription de votre application sera configurée à l’aide de l’URL fournie.</span><span class="sxs-lookup"><span data-stu-id="8ee02-117">Your app registration will be configured using the provided URL.</span></span>
1. <span data-ttu-id="8ee02-118">Les détails de configuration de l’enregistrement de l’application seront stockés dans les `.env` fichiers dans le code source de votre projet.</span><span class="sxs-lookup"><span data-stu-id="8ee02-118">The app registration's configuration details will be stored in the `.env` files in your project's source code.</span></span>

<span data-ttu-id="8ee02-119">Si vous souhaitez en savoir plus sur le mode d’inscription de votre application Azure, _reportez-vous_  à notre [prise en charge de l’authentification unique (SSO) pour les onglets](../tabs/how-to/authentication/auth-aad-sso.md) documentation.</span><span class="sxs-lookup"><span data-stu-id="8ee02-119">If you would like to learn more about how your Azure app registration will be provisioned, please _see_  our [single sign-on (SSO) support for tabs](../tabs/how-to/authentication/auth-aad-sso.md) documentation.</span></span>

> [!TIP]
> <span data-ttu-id="8ee02-120">Vous devrez accéder aux **inscriptions d’applications Azure** et mettre à jour votre *URI d’API* et *Rediriger les URL* chaque fois que vous modifiez cette URL.</span><span class="sxs-lookup"><span data-stu-id="8ee02-120">You will need to go to **Azure App Registrations** and update your *API URI* and *redirect URLs* whenever you change this URL.</span></span>

## <a name="run-your-project"></a><span data-ttu-id="8ee02-121">Exécuter votre projet</span><span class="sxs-lookup"><span data-stu-id="8ee02-121">Run your project</span></span>

1. <span data-ttu-id="8ee02-122">Sélectionnez **NPM installer** dans le `api-server` dossier.</span><span class="sxs-lookup"><span data-stu-id="8ee02-122">Select **npm install** from the `api-server` folder.</span></span> <span data-ttu-id="8ee02-123">Ensuite **NPM Start**.</span><span class="sxs-lookup"><span data-stu-id="8ee02-123">Then **npm start**.</span></span>
1. <span data-ttu-id="8ee02-124">Sélectionnez **NPM installer** dans le `.src` dossier.</span><span class="sxs-lookup"><span data-stu-id="8ee02-124">Select **npm install** from the `.src` folder.</span></span> <span data-ttu-id="8ee02-125">Ensuite **NPM Start**.</span><span class="sxs-lookup"><span data-stu-id="8ee02-125">Then **npm start**.</span></span>
1. <span data-ttu-id="8ee02-126">Si vous utilisez un service de tunneling comme [ngrok](https://ngrok.com/), exécutez-le et assurez-vous que l’URL correspond à ce que vous avez entré dans l’Assistant Création de projet.</span><span class="sxs-lookup"><span data-stu-id="8ee02-126">If you are using a tunneling service like [ngrok](https://ngrok.com/), run it and make sure the URL matches with what you entered in the project creation wizard.</span></span> <span data-ttu-id="8ee02-127">Si ce n’est pas le cas, vous devez mettre à jour l’URI de votre _API_ et l' _URL de redirection_ dans l’inscription de l’application qui a été créée dans Azure.</span><span class="sxs-lookup"><span data-stu-id="8ee02-127">If it doesn't, you will need to update your _API URI_ and _redirect URL_ in the app registration that was created in Azure.</span></span>
1. <span data-ttu-id="8ee02-128">Accédez à la barre d’activité sur le côté gauche de la fenêtre de code Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8ee02-128">Navigate to the activity bar on the left side of the Visual Studio Code window.</span></span>
1. <span data-ttu-id="8ee02-129">Sélectionnez l’icône **exécuter** pour afficher l’affichage **exécuter et déboguer** .</span><span class="sxs-lookup"><span data-stu-id="8ee02-129">Select the **Run** icon to display the **Run and Debug** view.</span></span>
1. <span data-ttu-id="8ee02-130">Vous pouvez également utiliser le raccourci clavier **Ctrl + Maj + D**.</span><span class="sxs-lookup"><span data-stu-id="8ee02-130">You can also use the keyboard shortcut **Ctrl+Shift+D**.</span></span>

> [!TIP]
> <span data-ttu-id="8ee02-131">Il se peut que la boîte de dialogue d’installation de l’application ne s’affiche pas dans le navigateur si les fenêtres contextuelles sont désactivées pour votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="8ee02-131">You may not see the app install dialogue in the browser if pop-up windows are disabled for your browser.</span></span> <span data-ttu-id="8ee02-132">Dans ce cas, activez les fenêtres contextuelles et actualisez la page.</span><span class="sxs-lookup"><span data-stu-id="8ee02-132">If this happens, enable pop-up windows and refresh the page.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8ee02-133">En savoir plus : créer des applications avec Microsoft teams Toolkit et Visual Studio code</span><span class="sxs-lookup"><span data-stu-id="8ee02-133">Learn more: Build apps with the Microsoft Teams Toolkit and Visual Studio Code</span></span>](visual-studio-code-overview.md)
