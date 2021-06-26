---
title: Conditions préalables
author: surbhigupta
description: Chaque onglet de Microsoft Teams doit respecter ces exigences.
keywords: Canal de groupe onglets teams configurable
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: b54fc7235132a9253f6eecc62417f786bf4aa45c
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140186"
---
# <a name="prerequisites"></a><span data-ttu-id="10462-104">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="10462-104">Prerequisites</span></span>

<span data-ttu-id="10462-105">Teams onglets doivent respecter les conditions préalables suivantes :</span><span class="sxs-lookup"><span data-stu-id="10462-105">Teams tabs must adhere to the following prerequisites:</span></span>

* <span data-ttu-id="10462-106">Vous devez permettre à vos pages d’onglets d’être affichées dans un iFrame, à l’aide des en-têtes de réponse HTTP X-Frame-Options et Content-Security-Policy.</span><span class="sxs-lookup"><span data-stu-id="10462-106">You must allow your tab pages to be shown in an iFrame, using X-Frame-Options and Content-Security-Policy HTTP response headers.</span></span>
  * <span data-ttu-id="10462-107">Définissez l’en-tête : `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`</span><span class="sxs-lookup"><span data-stu-id="10462-107">Set header: `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`</span></span>
  * <span data-ttu-id="10462-108">Pour la compatibilité d’Internet Explorer 11, définissez `X-Content-Security-Policy` .</span><span class="sxs-lookup"><span data-stu-id="10462-108">For Internet Explorer 11 compatibility, set `X-Content-Security-Policy`.</span></span>
  * <span data-ttu-id="10462-109">Sinon, définissez l’en-tête `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/` .</span><span class="sxs-lookup"><span data-stu-id="10462-109">Alternately, set header `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/`.</span></span> <span data-ttu-id="10462-110">Cet en-tête est supprimé, mais toujours accepté par la plupart des navigateurs.</span><span class="sxs-lookup"><span data-stu-id="10462-110">This header is deprecated but still accepted by most browsers.</span></span>

* <span data-ttu-id="10462-111">En règle générale, comme protection contre le détournement de clic, les pages de connexion ne s’restituer dans les iFrames.</span><span class="sxs-lookup"><span data-stu-id="10462-111">Typically, as a safeguard against clickjacking, login pages do not render in iFrames.</span></span> <span data-ttu-id="10462-112">Votre logique d’authentification doit utiliser une méthode autre que la redirection.</span><span class="sxs-lookup"><span data-stu-id="10462-112">Your authentication logic needs to use a method other than redirect.</span></span> <span data-ttu-id="10462-113">Par exemple, utilisez l’authentification basée sur les jetons ou sur les cookies.</span><span class="sxs-lookup"><span data-stu-id="10462-113">For example, use token-based or cookie-based authentication.</span></span>

    > [!NOTE]
    > <span data-ttu-id="10462-114">Chrome 80, dont la publication est prévue début 2020, introduit de nouvelles valeurs de cookie et impose des stratégies de cookie par défaut.</span><span class="sxs-lookup"><span data-stu-id="10462-114">Chrome 80, scheduled for release in early 2020, introduces new cookie values and imposes cookie policies by default.</span></span> <span data-ttu-id="10462-115">Il est recommandé de définir l’utilisation prévue pour vos cookies plutôt que de vous appuyer sur le comportement par défaut du navigateur.</span><span class="sxs-lookup"><span data-stu-id="10462-115">It is recommended that you set the intended use for your cookies rather than rely on default browser behavior.</span></span> <span data-ttu-id="10462-116">Pour plus d’informations, voir [l’attribut de cookie SameSite.](../../resources/samesite-cookie-update.md)</span><span class="sxs-lookup"><span data-stu-id="10462-116">For more information, see [SameSite cookie attribute](../../resources/samesite-cookie-update.md).</span></span>

* <span data-ttu-id="10462-117">Les navigateurs adhèrent à une restriction de stratégie de même origine.</span><span class="sxs-lookup"><span data-stu-id="10462-117">Browsers adhere to a same-origin policy restriction.</span></span> <span data-ttu-id="10462-118">Cela empêche les pages web d’effectuer des demandes à des domaines différents de la page web servie.</span><span class="sxs-lookup"><span data-stu-id="10462-118">It prevents webpages from making requests to different domains than the served web page.</span></span> <span data-ttu-id="10462-119">Toutefois, vous pouvez rediriger la page de configuration ou de contenu vers un autre domaine ou sous-domaine.</span><span class="sxs-lookup"><span data-stu-id="10462-119">However, you can redirect the configuration or content page to another domain or subdomain.</span></span> <span data-ttu-id="10462-120">Votre logique de navigation entre domaines doit permettre au client Teams de valider l’origine par rapport à une liste statique dans le manifeste de l’application lors du chargement ou de la communication avec `validDomains` l’onglet.</span><span class="sxs-lookup"><span data-stu-id="10462-120">Your cross-domain navigation logic must allow the Teams client to validate the origin against a static `validDomains` list in the app manifest when loading or communicating with the tab.</span></span>

* <span data-ttu-id="10462-121">Vous devez mettre en forme vos onglets en fonction Teams thème, de la conception et de l’intention du client.</span><span class="sxs-lookup"><span data-stu-id="10462-121">You must style your tabs based on the Teams client's theme, design, and intent.</span></span> <span data-ttu-id="10462-122">En règle générale, les onglets fonctionnent mieux lorsqu’ils sont conçus pour répondre à un besoin spécifique et qu’ils se concentrent sur un petit ensemble de tâches ou un sous-ensemble de données pertinents pour l’emplacement du canal de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="10462-122">Typically, tabs work best when they are built to address a specific need and focus on a small set of tasks or a subset of data that is relevant to the tab's channel location.</span></span>

* <span data-ttu-id="10462-123">Dans votre page de contenu, ajoutez une référence Microsoft Teams [SDK client JavaScript à](/javascript/api/overview/msteams-client) l’aide de balises de script.</span><span class="sxs-lookup"><span data-stu-id="10462-123">Within your content page, add a reference to [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client) using script tags.</span></span> <span data-ttu-id="10462-124">Après le chargement de votre page, appelez-la, `microsoftTeams.initialize()` sinon votre page n’est pas affichée.</span><span class="sxs-lookup"><span data-stu-id="10462-124">After your page loads, make a call to `microsoftTeams.initialize()`, otherwise your page is not displayed.</span></span>

* <span data-ttu-id="10462-125">Pour que l’authentification fonctionne sur les clients mobiles, vous devez mettre à niveau Teams SDK JavaScript vers au moins la version 1.4.1.</span><span class="sxs-lookup"><span data-stu-id="10462-125">For authentication to work on mobile clients, you must upgrade Teams JavaScript SDK to at least version 1.4.1.</span></span>

* <span data-ttu-id="10462-126">Si vous choisissez que votre onglet de canal ou de groupe s’affiche sur Teams clients mobiles, la configuration doit avoir une valeur `setSettings()` pour la `websiteUrl` propriété.</span><span class="sxs-lookup"><span data-stu-id="10462-126">If you choose to have your channel or group tab appear on Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property.</span></span>

* <span data-ttu-id="10462-127">L’onglet Teams MS ne prend pas en charge la possibilité de charger des sites web intranet qui utilisent des certificats auto-signés.</span><span class="sxs-lookup"><span data-stu-id="10462-127">MS Teams tab does not support the ability to load intranet websites that use self-signed certificates.</span></span>

## <a name="see-also"></a><span data-ttu-id="10462-128">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="10462-128">See also</span></span>

* [<span data-ttu-id="10462-129">Teams onglets</span><span class="sxs-lookup"><span data-stu-id="10462-129">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="10462-130">Créer un onglet de canal ou de groupe</span><span class="sxs-lookup"><span data-stu-id="10462-130">Create a channel or group tab</span></span>](~/tabs/how-to/create-channel-group-tab.md)
* [<span data-ttu-id="10462-131">Créer une page de contenu</span><span class="sxs-lookup"><span data-stu-id="10462-131">Create a content page</span></span>](~/tabs/how-to/create-tab-pages/content-page.md)
* [<span data-ttu-id="10462-132">Créer une page de configuration</span><span class="sxs-lookup"><span data-stu-id="10462-132">Create a configuration page</span></span>](~/tabs/how-to/create-tab-pages/configuration-page.md)
* [<span data-ttu-id="10462-133">Créer une page de suppression pour votre onglet</span><span class="sxs-lookup"><span data-stu-id="10462-133">Create a removal page for your tab</span></span>](~/tabs/how-to/create-tab-pages/removal-page.md)
* [<span data-ttu-id="10462-134">Onglets sur les appareils mobiles</span><span class="sxs-lookup"><span data-stu-id="10462-134">Tabs on mobile</span></span>](~/tabs/design/tabs-mobile.md)
* [<span data-ttu-id="10462-135">Obtenir un contexte Teams pour votre onglet</span><span class="sxs-lookup"><span data-stu-id="10462-135">Get context for your tab</span></span>](~/tabs/how-to/access-teams-context.md)
* [<span data-ttu-id="10462-136">Créer des onglets avec les Cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="10462-136">Build tabs with Adaptive Cards</span></span>](~/tabs/how-to/build-adaptive-card-tabs.md)
* [<span data-ttu-id="10462-137">Déploiement du lien des onglets et vue des étapes</span><span class="sxs-lookup"><span data-stu-id="10462-137">Tabs link unfurling and Stage View</span></span>](~/tabs/tabs-link-unfurling.md)
* [<span data-ttu-id="10462-138">Créer des onglets de conversation</span><span class="sxs-lookup"><span data-stu-id="10462-138">Create conversational tabs</span></span>](~/tabs/how-to/conversational-tabs.md)
* [<span data-ttu-id="10462-139">Modifications des marges de l’onglet</span><span class="sxs-lookup"><span data-stu-id="10462-139">Tab margin changes</span></span>](~/resources/removing-tab-margins.md)

## <a name="next-step"></a><span data-ttu-id="10462-140">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="10462-140">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="10462-141">Créer un onglet personnel</span><span class="sxs-lookup"><span data-stu-id="10462-141">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
