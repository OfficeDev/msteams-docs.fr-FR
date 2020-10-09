---
title: Empaquetage de votre application
description: Découvrez comment empaqueter votre application à des fins de test, de chargement et de publication dans Microsoft teams
keywords: empaquetage d’applications teams
ms.topic: conceptual
ms.openlocfilehash: d2d49dcc5c4ccada0a75de5df6fda29a60e809f6
ms.sourcegitcommit: 560bf433129c16888135879e2703dbdeb38ec99f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2020
ms.locfileid: "48397700"
---
# <a name="create-an-app-package-for-your-microsoft-teams-app"></a><span data-ttu-id="d765d-104">Créer un package d’application pour votre application Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="d765d-104">Create an app package for your Microsoft Teams app</span></span>

<span data-ttu-id="d765d-105">Les applications dans teams sont définies par un fichier JSON de manifeste d’application et regroupées dans un package d’application avec leurs icônes.</span><span class="sxs-lookup"><span data-stu-id="d765d-105">Apps in Teams are defined by an app manifest JSON file, and bundled in an app package with their icons.</span></span> <span data-ttu-id="d765d-106">Vous aurez besoin d’un package d’application pour télécharger et installer votre application dans Teams, et pour publier le catalogue d’applications de votre ligne de l’application métier ou vers AppSource.</span><span class="sxs-lookup"><span data-stu-id="d765d-106">You'll need an app package to upload and install your app in Teams, and to publish to either your Line of Business app catalog or to AppSource.</span></span>

<span data-ttu-id="d765d-107">Un package d’applications teams est un fichier. zip contenant les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="d765d-107">A Teams app package is a .zip file containing the following:</span></span>

* <span data-ttu-id="d765d-108">Un fichier manifeste nommé « manifest.json », qui spécifie les attributs de votre application et pointe vers les ressources requises pour votre expérience, telles que l’emplacement de sa page de configuration d’onglets ou l’ID d’application Microsoft pour son bot.</span><span class="sxs-lookup"><span data-stu-id="d765d-108">A manifest file named "manifest.json", which specifies attributes of your app and points to required resources for your experience, such the location of its tab configuration page or the Microsoft app ID for its bot.</span></span>
* <span data-ttu-id="d765d-109">Une icône « plan » transparente et une icône « couleur » complète.</span><span class="sxs-lookup"><span data-stu-id="d765d-109">A transparent "outline" icon and a full "color" icon.</span></span> <span data-ttu-id="d765d-110">Pour plus d’informations, consultez la section [icônes](#icons) plus loin dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="d765d-110">See [Icons](#icons) later in this topic for more information.</span></span>

## <a name="creating-a-manifest"></a><span data-ttu-id="d765d-111">Création d’un manifeste</span><span class="sxs-lookup"><span data-stu-id="d765d-111">Creating a manifest</span></span>

<span data-ttu-id="d765d-112">*Teams App Studio* peut vous aider à configurer votre manifeste.</span><span class="sxs-lookup"><span data-stu-id="d765d-112">*Teams App Studio* can help configure your manifest.</span></span> <span data-ttu-id="d765d-113">Elle contient également une bibliothèque de contrôle React et des exemples configurables pour les cartes.</span><span class="sxs-lookup"><span data-stu-id="d765d-113">It also contains a React control library and configurable samples for cards.</span></span> <span data-ttu-id="d765d-114">Voir [application Studio Overview](~/concepts/build-and-test/app-studio-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d765d-114">See [App Studio Overview](~/concepts/build-and-test/app-studio-overview.md).</span></span>

<span data-ttu-id="d765d-115">Votre fichier manifeste doit être nommé « manifest.js » et se trouver au niveau supérieur du package de téléchargement.</span><span class="sxs-lookup"><span data-stu-id="d765d-115">Your manifest file must be named "manifest.json" and be at the top level of the upload package.</span></span> <span data-ttu-id="d765d-116">Notez que les manifestes et les packages créés précédemment peuvent prendre en charge une version plus ancienne du schéma.</span><span class="sxs-lookup"><span data-stu-id="d765d-116">Note that manifests and packages built previously might support an older version of the schema.</span></span> <span data-ttu-id="d765d-117">Pour les applications teams et en particulier la soumission AppSource (anciennement Office Store), vous devez utiliser le [schéma de manifeste](~/resources/schema/manifest-schema.md)actuel.</span><span class="sxs-lookup"><span data-stu-id="d765d-117">For Teams apps and especially AppSource (formerly Office Store) submission, you must use the current [manifest schema](~/resources/schema/manifest-schema.md).</span></span>

> [!TIP]
> <span data-ttu-id="d765d-118">Spécifiez le schéma au début de votre manifeste pour activer IntelliSense ou une prise en charge similaire à partir de votre éditeur de code :</span><span class="sxs-lookup"><span data-stu-id="d765d-118">Specify the schema at the beginning of your manifest to enable IntelliSense or similar support from your code editor:</span></span>
>
> `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",`

## <a name="icons"></a><span data-ttu-id="d765d-119">Icônes</span><span class="sxs-lookup"><span data-stu-id="d765d-119">Icons</span></span>

> [!Note]
> <span data-ttu-id="d765d-120">Si votre application contient un bot ou une extension de messagerie, les icônes utilisées seront les icônes chargées dans l’enregistrement de votre bot dans l’infrastructure de robot.</span><span class="sxs-lookup"><span data-stu-id="d765d-120">If your app contains a bot or messaging extension, the icons used will be the icons uploaded to your bot registration in the Bot Framework.</span></span>

<span data-ttu-id="d765d-121">Microsoft teams nécessite deux icônes pour l’expérience de votre application, à utiliser dans le produit.</span><span class="sxs-lookup"><span data-stu-id="d765d-121">Microsoft Teams requires two icons for your app experience, to be used within the product.</span></span> <span data-ttu-id="d765d-122">Les icônes doivent être incluses dans le package et référencées via des chemins d’accès relatifs dans le manifeste.</span><span class="sxs-lookup"><span data-stu-id="d765d-122">Icons must be included in the package and referenced via relative paths in the manifest.</span></span> <span data-ttu-id="d765d-123">La longueur maximale de chaque chemin d’accès est de 2048 octets, et le format de l’icône est. png.</span><span class="sxs-lookup"><span data-stu-id="d765d-123">The maximum length of each path is 2048 bytes, and the format of the icon is .png.</span></span>

### <a name="color"></a><span data-ttu-id="d765d-124">color</span><span class="sxs-lookup"><span data-stu-id="d765d-124">color</span></span>

<span data-ttu-id="d765d-125">L' `color` icône est utilisée dans Microsoft Teams (dans les galeries d’applications et d’onglets, les robots, les lanceurs, etc.).</span><span class="sxs-lookup"><span data-stu-id="d765d-125">The `color` icon is used throughout Microsoft Teams (in app and tab galleries, bots, flyouts, and so on).</span></span> <span data-ttu-id="d765d-126">Cette icône doit être 192x192 pixels.</span><span class="sxs-lookup"><span data-stu-id="d765d-126">This icon should be 192x192 pixels.</span></span> <span data-ttu-id="d765d-127">Votre icône peut être n’importe quelle couleur (ou couleurs), mais l’arrière-plan doit être votre couleur d’accentuation personnalisée.</span><span class="sxs-lookup"><span data-stu-id="d765d-127">Your icon can be any color (or colors), but the background should be your branded accent color.</span></span> <span data-ttu-id="d765d-128">Elle doit également avoir une petite quantité de remplissage autour de l’icône pour prendre en charge le rognage hexagonal pour la version bot de l’icône.</span><span class="sxs-lookup"><span data-stu-id="d765d-128">It should also have a small amount of padding surrounding the icon to accommodate the hexagonal cropping for the bot version of the icon.</span></span>

### <a name="outline"></a><span data-ttu-id="d765d-129">outline</span><span class="sxs-lookup"><span data-stu-id="d765d-129">outline</span></span>

<span data-ttu-id="d765d-130">L' `outline` icône est utilisée aux emplacements suivants : la barre d’application et les extensions de messagerie que l’utilisateur a marquées comme « favoris ».</span><span class="sxs-lookup"><span data-stu-id="d765d-130">The `outline` icon is used in these places: the app bar and messaging extensions the user has marked as a "favorite."</span></span> <span data-ttu-id="d765d-131">Cette icône doit être de 32x32 pixels.</span><span class="sxs-lookup"><span data-stu-id="d765d-131">This icon must be 32x32 pixels.</span></span> <span data-ttu-id="d765d-132">Votre icône de contour ne doit contenir que le blanc et la transparence (aucune autre couleur).</span><span class="sxs-lookup"><span data-stu-id="d765d-132">Your outline icon must contain only white and transparency (no other colors).</span></span> <span data-ttu-id="d765d-133">L’icône peut être blanche avec un arrière-plan transparent ou transparente avec un arrière-plan blanc.</span><span class="sxs-lookup"><span data-stu-id="d765d-133">The icon can be white with transparent background or transparent with a white background.</span></span> <span data-ttu-id="d765d-134">L’icône de contour ne doit pas avoir de remplissage supplémentaire autour de l’icône et doit être aussi rapprochée que possible tout en maintenant les dimensions 32x32.</span><span class="sxs-lookup"><span data-stu-id="d765d-134">The outline icon should not have extra padding surrounding the icon and should be as tightly cropped as possible while still maintaining the 32x32 dimensions.</span></span> <span data-ttu-id="d765d-135">Voici quelques exemples intéressants :</span><span class="sxs-lookup"><span data-stu-id="d765d-135">Here are a few good examples:</span></span>

> [!TIP]
>  * <span data-ttu-id="d765d-136">La couleur doit être « blanc » en RVB, (rouge : 255, vert : 255, bleu : 255).</span><span class="sxs-lookup"><span data-stu-id="d765d-136">Color must be "White" in RGB, (Red: 255, Green: 255, Blue: 255).</span></span>
>  * <span data-ttu-id="d765d-137">Toute autre partie de l’icône doit être transparente.</span><span class="sxs-lookup"><span data-stu-id="d765d-137">All other part of icon should be transparent.</span></span>
>  * <span data-ttu-id="d765d-138">Pour le passage, la petite icône doit être pleine transparence, canal alpha égal à 0 et toute autre valeur est échec.</span><span class="sxs-lookup"><span data-stu-id="d765d-138">For passing, small icon must be full transparent, Alpha channel to be 0 and any other value is a fail.</span></span>

![Exemples d’icônes de plan](~/assets/images/icons/sample20x20s.png)

<span data-ttu-id="d765d-140">Imaginons, par exemple, que votre société est contoso.</span><span class="sxs-lookup"><span data-stu-id="d765d-140">For example, say your company is Contoso.</span></span> <span data-ttu-id="d765d-141">Vous devez envoyer deux icônes :</span><span class="sxs-lookup"><span data-stu-id="d765d-141">You'd submit two icons:</span></span>

![Présentation des icônes](~/assets/images/framework/framework_submit_icon.png)

<span data-ttu-id="d765d-143">Voici comment les icônes apparaîtront dans l’interface utilisateur :</span><span class="sxs-lookup"><span data-stu-id="d765d-143">Here's how the icons would appear in the UI:</span></span>

#### <a name="bot-and-chiclet-in-channel-view"></a><span data-ttu-id="d765d-144">Robot et chiclet dans l’affichage des canaux</span><span class="sxs-lookup"><span data-stu-id="d765d-144">Bot and chiclet in Channel view</span></span>

![Bot et chiclet UX](~/assets/images/icons/botandchiclet.png)

#### <a name="flyout"></a><span data-ttu-id="d765d-146">Menu</span><span class="sxs-lookup"><span data-stu-id="d765d-146">Flyout</span></span>

![Exemple de menu volant contoso](~/assets/images/icons/flyout.png)

#### <a name="app-bar-and-home-screen"></a><span data-ttu-id="d765d-148">Barre d’application et écran d’accueil</span><span class="sxs-lookup"><span data-stu-id="d765d-148">App bar and home screen</span></span>

![Exemple de barre d’application Contoso homescreen](~/assets/images/icons/appbarhomescreen.png)
