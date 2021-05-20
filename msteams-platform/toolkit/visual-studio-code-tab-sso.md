---
title: Authentification unique avec Teams Shared Computer Toolkit et Visual Studio Code pour onglets
description: Créez un onglet qui prend en charge les appels à guichet unique et Microsoft Graph directement dans Visual Studio Code avec le Microsoft Teams Shared Computer Toolkit
keywords: équipes visual studio code toolkit onglets sso graph authentification Azure plate-forme d’identité
localization_priority: Normal
ms.topic: how-to
ms.author: lajanuar
ms.openlocfilehash: 11e642ce335dae4344f1c730b73763e9172fd76c
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566830"
---
# <a name="single-sign-on-authentication-with-teams-toolkit-and-visual-studio-code-for-tabs"></a><span data-ttu-id="9db91-104">Authentification unique avec Teams Shared Computer Toolkit et Visual Studio Code pour onglets</span><span class="sxs-lookup"><span data-stu-id="9db91-104">Single sign-on authentication with Teams Toolkit and Visual Studio Code for tabs</span></span>

<span data-ttu-id="9db91-105">Le Microsoft Teams Shared Computer Toolkit vous permet de créer une authentification unique de connect-on (SSO) pour les applications d’onglets directement dans Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="9db91-105">The Microsoft Teams Toolkit enables you to create single sign-on (SSO) authentication  for tab apps directly within Visual Studio Code.</span></span> <span data-ttu-id="9db91-106">La boîte à outils vous guide tout au long du processus et fournit tout ce dont vous avez besoin, y compris la fourniture Plateforme d’identités Microsoft’inscription sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="9db91-106">The toolkit guides you through the process and provides everything you need including provisioning your Microsoft identity platform registration in the Azure portal.</span></span>

## <a name="get-started--create-a-project"></a><span data-ttu-id="9db91-107">Démarrer — créer un projet</span><span class="sxs-lookup"><span data-stu-id="9db91-107">Get started — create a project</span></span>

1. <span data-ttu-id="9db91-108">Créez un nouveau projet dans la boîte à outils.</span><span class="sxs-lookup"><span data-stu-id="9db91-108">Create a new project in the toolkit.</span></span>
1. <span data-ttu-id="9db91-109">Sélectionnez l’onglet comme type d’extension que vous souhaitez créer.</span><span class="sxs-lookup"><span data-stu-id="9db91-109">Select tab as the type of extension you'd like to create.</span></span>
1. <span data-ttu-id="9db91-110">Sélectionnez l’option pour prendre en charge SSO.</span><span class="sxs-lookup"><span data-stu-id="9db91-110">Select the option to support SSO.</span></span>

> [!TIP]
> <span data-ttu-id="9db91-111">Après l’installation, vous devriez voir les Teams Shared Computer Toolkit la barre d Visual Studio Code’activité.</span><span class="sxs-lookup"><span data-stu-id="9db91-111">After installation, you should see the Teams Toolkit in the Visual Studio Code activity bar.</span></span> <span data-ttu-id="9db91-112">Si ce n’est pas le cas, cliquez à droite dans la barre **d’activité et sélectionnez Microsoft Teams** épingler la boîte à outils pour un accès facile.</span><span class="sxs-lookup"><span data-stu-id="9db91-112">If not, right-click within the activity bar and select **Microsoft Teams** to pin the toolkit for easy access.</span></span>

## <a name="configure-your-project"></a><span data-ttu-id="9db91-113">Configurez votre projet</span><span class="sxs-lookup"><span data-stu-id="9db91-113">Configure your project</span></span>

1. <span data-ttu-id="9db91-114">Pour activer SSO dans Teams, votre application doit avoir une ressource d’enregistrement d’application Azure.</span><span class="sxs-lookup"><span data-stu-id="9db91-114">To enable SSO within Teams, your app must have an Azure app registration resource.</span></span> <span data-ttu-id="9db91-115">Le Teams Shared Computer Toolkit l’inscription de l’application en votre nom.</span><span class="sxs-lookup"><span data-stu-id="9db91-115">The Teams Toolkit will provision the app registration on your behalf.</span></span>
1. <span data-ttu-id="9db91-116">Entrez l’URL où votre application sera hébergée et sélectionnez **ensuite**.</span><span class="sxs-lookup"><span data-stu-id="9db91-116">Enter the URL where your app will be hosted and select **next**.</span></span> <span data-ttu-id="9db91-117">L’enregistrement de votre application sera configuré à l’aide de l’URL fournie.</span><span class="sxs-lookup"><span data-stu-id="9db91-117">Your app registration will be configured using the provided URL.</span></span>
1. <span data-ttu-id="9db91-118">Les détails de configuration de l’enregistrement de l’application seront `.env` stockés dans les fichiers dans le code source de votre projet.</span><span class="sxs-lookup"><span data-stu-id="9db91-118">The app registration's configuration details will be stored in the `.env` files in your project's source code.</span></span>

<span data-ttu-id="9db91-119">Si vous souhaitez en savoir plus sur la façon dont l’enregistrement de votre application Azure sera provisionné, veuillez _consulter_ notre [support de connect-on unique (SSO) pour la documentation des onglets.](../tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="9db91-119">If you would like to learn more about how your Azure app registration will be provisioned, please _see_  our [single sign-on (SSO) support for tabs](../tabs/how-to/authentication/auth-aad-sso.md) documentation.</span></span>

> [!TIP]
> <span data-ttu-id="9db91-120">Vous devrez vous rendre aux **enregistrements d’applications Azure et** mettre à jour *votre API URI et* *rediriger les URL chaque fois* que vous modifiez cette URL.</span><span class="sxs-lookup"><span data-stu-id="9db91-120">You will need to go to **Azure App Registrations** and update your *API URI* and *redirect URLs* whenever you change this URL.</span></span>

## <a name="run-your-project"></a><span data-ttu-id="9db91-121">Exécutez votre projet</span><span class="sxs-lookup"><span data-stu-id="9db91-121">Run your project</span></span>

1. <span data-ttu-id="9db91-122">Sélectionnez **npm installer** à partir du `api-server` dossier.</span><span class="sxs-lookup"><span data-stu-id="9db91-122">Select **npm install** from the `api-server` folder.</span></span> <span data-ttu-id="9db91-123">Puis **npm commencer**.</span><span class="sxs-lookup"><span data-stu-id="9db91-123">Then **npm start**.</span></span>
1. <span data-ttu-id="9db91-124">Sélectionnez **npm installer** à partir du `.src` dossier.</span><span class="sxs-lookup"><span data-stu-id="9db91-124">Select **npm install** from the `.src` folder.</span></span> <span data-ttu-id="9db91-125">Puis **npm commencer**.</span><span class="sxs-lookup"><span data-stu-id="9db91-125">Then **npm start**.</span></span>
1. <span data-ttu-id="9db91-126">Si vous utilisez un service de tunnelage comme [ngrok, exécutez-le](https://ngrok.com/)et assurez-vous que l’URL correspond à ce que vous avez entré dans l’assistant de création de projet.</span><span class="sxs-lookup"><span data-stu-id="9db91-126">If you are using a tunneling service like [ngrok](https://ngrok.com/), run it and make sure the URL matches with what you entered in the project creation wizard.</span></span> <span data-ttu-id="9db91-127">Si ce n’est pas le cas, vous devrez mettre à jour _votre API URI et_ _rediriger l’URL_ dans l’enregistrement de l’application créée dans Azure.</span><span class="sxs-lookup"><span data-stu-id="9db91-127">If it doesn't, you will need to update your _API URI_ and _redirect URL_ in the app registration that was created in Azure.</span></span>
1. <span data-ttu-id="9db91-128">Accédez à la barre d’activité sur le côté gauche de la Visual Studio Code fenêtre.</span><span class="sxs-lookup"><span data-stu-id="9db91-128">Navigate to the activity bar on the left side of the Visual Studio Code window.</span></span>
1. <span data-ttu-id="9db91-129">Sélectionnez **l’icône** Exécuter pour afficher **la vue Exécuter et Debug.**</span><span class="sxs-lookup"><span data-stu-id="9db91-129">Select the **Run** icon to display the **Run and Debug** view.</span></span>
1. <span data-ttu-id="9db91-130">Vous pouvez également utiliser le raccourci clavier **Ctrl+Shift+D**.</span><span class="sxs-lookup"><span data-stu-id="9db91-130">You can also use the keyboard shortcut **Ctrl+Shift+D**.</span></span>

> [!TIP]
> <span data-ttu-id="9db91-131">Il se peut que vous ne voyiez pas l’application installer le dialogue dans le navigateur si les fenêtres contextées sont désactivées pour votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="9db91-131">You may not see the app install dialogue in the browser if pop-up windows are disabled for your browser.</span></span> <span data-ttu-id="9db91-132">Si cela se produit, activez les fenêtres contexturées et actualisez la page.</span><span class="sxs-lookup"><span data-stu-id="9db91-132">If this happens, enable pop-up windows and refresh the page.</span></span>

## <a name="see-also"></a><span data-ttu-id="9db91-133">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="9db91-133">See also</span></span>

- [<span data-ttu-id="9db91-134">Créez des applications avec les Microsoft Teams Shared Computer Toolkit et Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="9db91-134">Build apps with the Microsoft Teams Toolkit and Visual Studio Code</span></span>](visual-studio-code-overview.md)
