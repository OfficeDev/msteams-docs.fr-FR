---
title: Authentification unique avec authentification unique Teams Shared Computer Toolkit et Visual Studio Code pour les onglets
description: Créez un onglet qui prend en charge l' sign-on unique et les appels Microsoft Graph directement dans Visual Studio Code avec le Microsoft Teams Shared Computer Toolkit
keywords: teams visual studio code toolkit tabs sso graph authentication Azure identity platform
localization_priority: Normal
ms.topic: how-to
ms.author: lajanuar
ms.openlocfilehash: b2ba9eb27d00f07ec46ddfe0c1cc13ed0864bbbc
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630991"
---
# <a name="single-sign-on-authentication-with-teams-toolkit-and-visual-studio-code-for-tabs"></a><span data-ttu-id="7846b-104">Authentification unique avec authentification unique Teams Shared Computer Toolkit et Visual Studio Code pour les onglets</span><span class="sxs-lookup"><span data-stu-id="7846b-104">Single sign-on authentication with Teams Toolkit and Visual Studio Code for tabs</span></span>

<span data-ttu-id="7846b-105">Le Microsoft Teams Shared Computer Toolkit vous permet de créer l’authentification unique (SSO) pour les applications onglet directement dans Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="7846b-105">The Microsoft Teams Toolkit enables you to create single sign-on (SSO) authentication  for tab apps directly within Visual Studio Code.</span></span> <span data-ttu-id="7846b-106">Le kit de ressources vous guide tout au long du processus et fournit tout ce dont vous avez besoin, y compris la mise en service de votre Plateforme d’identités Microsoft inscription dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7846b-106">The toolkit guides you through the process and provides everything you need including provisioning your Microsoft identity platform registration in the Azure portal.</span></span>

## <a name="get-started--create-a-project"></a><span data-ttu-id="7846b-107">Mise en place : créer un projet</span><span class="sxs-lookup"><span data-stu-id="7846b-107">Get started — create a project</span></span>

1. <span data-ttu-id="7846b-108">Créez un projet dans le kit de ressources.</span><span class="sxs-lookup"><span data-stu-id="7846b-108">Create a new project in the toolkit.</span></span>
1. <span data-ttu-id="7846b-109">Sélectionnez l’onglet comme type d’extension que vous souhaitez créer.</span><span class="sxs-lookup"><span data-stu-id="7846b-109">Select tab as the type of extension you'd like to create.</span></span>
1. <span data-ttu-id="7846b-110">Sélectionnez l’option de prise en charge de l' sso.</span><span class="sxs-lookup"><span data-stu-id="7846b-110">Select the option to support SSO.</span></span>

> [!TIP]
> <span data-ttu-id="7846b-111">Après l’installation, vous devez voir le Teams Shared Computer Toolkit dans la barre d Visual Studio Code’activité.</span><span class="sxs-lookup"><span data-stu-id="7846b-111">After installation, you should see the Teams Toolkit in the Visual Studio Code activity bar.</span></span> <span data-ttu-id="7846b-112">Si ce n’est pas le cas, cliquez avec le bouton droit dans la barre **d’activité** et sélectionnez Microsoft Teams pour épingler le kit de ressources pour faciliter l’accès.</span><span class="sxs-lookup"><span data-stu-id="7846b-112">If not, right-click within the activity bar and select **Microsoft Teams** to pin the toolkit for easy access.</span></span>

## <a name="configure-your-project"></a><span data-ttu-id="7846b-113">Configurer votre projet</span><span class="sxs-lookup"><span data-stu-id="7846b-113">Configure your project</span></span>

1. <span data-ttu-id="7846b-114">Pour activer l' utilisateur Teams, votre application doit avoir une ressource d’inscription d’application Azure.</span><span class="sxs-lookup"><span data-stu-id="7846b-114">To enable SSO within Teams, your app must have an Azure app registration resource.</span></span> <span data-ttu-id="7846b-115">L Teams Shared Computer Toolkit approvisionnement de l’inscription de l’application en votre nom.</span><span class="sxs-lookup"><span data-stu-id="7846b-115">The Teams Toolkit will provision the app registration on your behalf.</span></span>
1. <span data-ttu-id="7846b-116">Entrez l’URL où votre application sera hébergée et sélectionnez **ensuite.**</span><span class="sxs-lookup"><span data-stu-id="7846b-116">Enter the URL where your app will be hosted and select **next**.</span></span> <span data-ttu-id="7846b-117">L’inscription de votre application sera configurée à l’aide de l’URL fournie.</span><span class="sxs-lookup"><span data-stu-id="7846b-117">Your app registration will be configured using the provided URL.</span></span>
1. <span data-ttu-id="7846b-118">Les détails de configuration de l’inscription de l’application sont stockés dans les fichiers du `.env` code source de votre projet.</span><span class="sxs-lookup"><span data-stu-id="7846b-118">The app registration's configuration details will be stored in the `.env` files in your project's source code.</span></span>

<span data-ttu-id="7846b-119">Si vous souhaitez en savoir plus sur la façon  dont votre inscription d’application Azure sera mise en service, consultez notre prise en charge de l' [sign-on unique (SSO)](../tabs/how-to/authentication/auth-aad-sso.md) pour la documentation sur les onglets.</span><span class="sxs-lookup"><span data-stu-id="7846b-119">If you would like to learn more about how your Azure app registration will be provisioned, please _see_  our [single sign-on (SSO) support for tabs](../tabs/how-to/authentication/auth-aad-sso.md) documentation.</span></span>

> [!TIP]
> <span data-ttu-id="7846b-120">Vous devez accéder à **Azure App Registrations** et  mettre à jour votre *URI d’API* et rediriger les URL chaque fois que vous modifiez cette URL.</span><span class="sxs-lookup"><span data-stu-id="7846b-120">You will need to go to **Azure App Registrations** and update your *API URI* and *redirect URLs* whenever you change this URL.</span></span>

## <a name="run-your-project"></a><span data-ttu-id="7846b-121">Exécuter votre projet</span><span class="sxs-lookup"><span data-stu-id="7846b-121">Run your project</span></span>

1. <span data-ttu-id="7846b-122">Sélectionnez **npm installer** dans le `api-server` dossier.</span><span class="sxs-lookup"><span data-stu-id="7846b-122">Select **npm install** from the `api-server` folder.</span></span> <span data-ttu-id="7846b-123">Puis **npm start**.</span><span class="sxs-lookup"><span data-stu-id="7846b-123">Then **npm start**.</span></span>
1. <span data-ttu-id="7846b-124">Sélectionnez **npm installer** dans le `.src` dossier.</span><span class="sxs-lookup"><span data-stu-id="7846b-124">Select **npm install** from the `.src` folder.</span></span> <span data-ttu-id="7846b-125">Puis **npm start**.</span><span class="sxs-lookup"><span data-stu-id="7846b-125">Then **npm start**.</span></span>
1. <span data-ttu-id="7846b-126">Si vous utilisez un service de tunneling comme [ngrok,](https://ngrok.com/)exécutez-le et assurez-vous que l’URL correspond à ce que vous avez entré dans l’Assistant création de projet.</span><span class="sxs-lookup"><span data-stu-id="7846b-126">If you are using a tunneling service like [ngrok](https://ngrok.com/), run it and make sure the URL matches with what you entered in the project creation wizard.</span></span> <span data-ttu-id="7846b-127">Si ce n’est pas le cas, vous devrez mettre à jour votre _URI d’API_ et rediriger l’URL dans l’inscription de l’application qui a été créée dans Azure. </span><span class="sxs-lookup"><span data-stu-id="7846b-127">If it doesn't, you will need to update your _API URI_ and _redirect URL_ in the app registration that was created in Azure.</span></span>
1. <span data-ttu-id="7846b-128">Accédez à la barre d’activité sur le côté gauche de Visual Studio Code fenêtre.</span><span class="sxs-lookup"><span data-stu-id="7846b-128">Navigate to the activity bar on the left side of the Visual Studio Code window.</span></span>
1. <span data-ttu-id="7846b-129">Sélectionnez **l’icône** Exécuter pour afficher **l’affichage Exécuter et déboguer.**</span><span class="sxs-lookup"><span data-stu-id="7846b-129">Select the **Run** icon to display the **Run and Debug** view.</span></span>
1. <span data-ttu-id="7846b-130">Vous pouvez également utiliser le raccourci clavier **Ctrl+Shift+D**.</span><span class="sxs-lookup"><span data-stu-id="7846b-130">You can also use the keyboard shortcut **Ctrl+Shift+D**.</span></span>

> [!TIP]
> <span data-ttu-id="7846b-131">Vous ne verrez peut-être pas le dialogue d’installation de l’application dans le navigateur si les fenêtres pop-up sont désactivées pour votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="7846b-131">You may not see the app install dialogue in the browser if pop-up windows are disabled for your browser.</span></span> <span data-ttu-id="7846b-132">Si cela se produit, activez les fenêtres pop-up et actualisez la page.</span><span class="sxs-lookup"><span data-stu-id="7846b-132">If this happens, enable pop-up windows and refresh the page.</span></span>

## <a name="see-also"></a><span data-ttu-id="7846b-133">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="7846b-133">See also</span></span>

[<span data-ttu-id="7846b-134">Créer des applications avec les Microsoft Teams Shared Computer Toolkit et Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="7846b-134">Build apps with the Microsoft Teams Toolkit and Visual Studio Code</span></span>](visual-studio-code-overview.md)
