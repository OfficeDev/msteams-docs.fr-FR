---
title: Empaquetage de votre application
description: Découvrez comment empaqueter votre application Microsoft teams à des fins de test, de chargement et de publication en magasin.
ms.topic: conceptual
ms.openlocfilehash: 6929375c8d6a1602f01d83d15bfa0dab7f02a664
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/09/2020
ms.locfileid: "49605273"
---
# <a name="create-an-app-package-for-your-microsoft-teams-app"></a><span data-ttu-id="5e95e-103">Créer un package d’application pour votre application Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="5e95e-103">Create an app package for your Microsoft Teams app</span></span>

<span data-ttu-id="5e95e-104">Les applications dans teams sont définies par un fichier JSON de manifeste d’application et regroupées dans un package d’application avec leurs icônes.</span><span class="sxs-lookup"><span data-stu-id="5e95e-104">Apps in Teams are defined by an app manifest JSON file, and bundled in an app package with their icons.</span></span> <span data-ttu-id="5e95e-105">Vous aurez besoin d’un package d’application pour télécharger et installer votre application dans teams et publier votre application dans votre catalogue d’applications métiers ou sur AppSource.</span><span class="sxs-lookup"><span data-stu-id="5e95e-105">You'll need an app package to upload and install your app in Teams and publish to either your Line of Business app catalog or to AppSource.</span></span>

<span data-ttu-id="5e95e-106">Un package d’applications teams est un fichier. zip contenant les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="5e95e-106">A Teams app package is a .zip file containing the following:</span></span>

* <span data-ttu-id="5e95e-107">Un fichier manifeste nommé `manifest.json` , qui spécifie les attributs de votre application et pointe vers les ressources requises pour votre expérience, telles que l’emplacement de sa page de configuration d’onglets ou l’ID d’application Microsoft pour son bot.</span><span class="sxs-lookup"><span data-stu-id="5e95e-107">A manifest file named `manifest.json`, which specifies attributes of your app and points to required resources for your experience, such the location of its tab configuration page or the Microsoft app ID for its bot.</span></span>
* <span data-ttu-id="5e95e-108">[Icônes de couleur et de plan de votre application](#app-icons).</span><span class="sxs-lookup"><span data-stu-id="5e95e-108">[Color and outline icons for your app](#app-icons).</span></span>

## <a name="creating-a-manifest"></a><span data-ttu-id="5e95e-109">Création d’un manifeste</span><span class="sxs-lookup"><span data-stu-id="5e95e-109">Creating a manifest</span></span>

<span data-ttu-id="5e95e-110">*Teams App Studio* peut vous aider à configurer votre manifeste.</span><span class="sxs-lookup"><span data-stu-id="5e95e-110">*Teams App Studio* can help configure your manifest.</span></span> <span data-ttu-id="5e95e-111">Elle contient également une bibliothèque de contrôle React et des exemples configurables pour les cartes.</span><span class="sxs-lookup"><span data-stu-id="5e95e-111">It also contains a React control library and configurable samples for cards.</span></span> <span data-ttu-id="5e95e-112">Voir [application Studio Overview](~/concepts/build-and-test/app-studio-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5e95e-112">See [App Studio Overview](~/concepts/build-and-test/app-studio-overview.md).</span></span>

<span data-ttu-id="5e95e-113">Votre fichier manifeste doit être nommé « manifest.js » et se trouver au niveau supérieur du package de téléchargement.</span><span class="sxs-lookup"><span data-stu-id="5e95e-113">Your manifest file must be named "manifest.json" and be at the top level of the upload package.</span></span> <span data-ttu-id="5e95e-114">Notez que les manifestes et les packages créés précédemment peuvent prendre en charge une version plus ancienne du schéma.</span><span class="sxs-lookup"><span data-stu-id="5e95e-114">Note that manifests and packages built previously might support an older version of the schema.</span></span> <span data-ttu-id="5e95e-115">Pour les applications teams et en particulier la soumission AppSource (anciennement Office Store), vous devez utiliser le [schéma de manifeste](~/resources/schema/manifest-schema.md)actuel.</span><span class="sxs-lookup"><span data-stu-id="5e95e-115">For Teams apps and especially AppSource (formerly Office Store) submission, you must use the current [manifest schema](~/resources/schema/manifest-schema.md).</span></span>

> [!TIP]
> <span data-ttu-id="5e95e-116">Spécifiez le schéma au début de votre manifeste pour activer IntelliSense ou une prise en charge similaire à partir de votre éditeur de code :</span><span class="sxs-lookup"><span data-stu-id="5e95e-116">Specify the schema at the beginning of your manifest to enable IntelliSense or similar support from your code editor:</span></span>
>
> `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`

## <a name="app-icons"></a><span data-ttu-id="5e95e-117">Icônes de l’application</span><span class="sxs-lookup"><span data-stu-id="5e95e-117">App icons</span></span>

<span data-ttu-id="5e95e-118">Votre package d’application doit inclure deux versions PNG de votre icône d’application, une icône de couleur et une icône en mode plan.</span><span class="sxs-lookup"><span data-stu-id="5e95e-118">Your app package must include two PNG versions of your app icon—a color icon and an outline icon.</span></span> <span data-ttu-id="5e95e-119">Pour que votre application réussisse la révision AppSource, ces icônes doivent respecter les exigences de taille suivantes.</span><span class="sxs-lookup"><span data-stu-id="5e95e-119">For your app to pass the AppSource review, these icons must meet the following size requirements.</span></span>

> [!Note]
> <span data-ttu-id="5e95e-120">Si votre application dispose d’un bot ou d’une extension de messagerie, vos icônes seront également incluses dans votre inscription au service Microsoft Azure bot.</span><span class="sxs-lookup"><span data-stu-id="5e95e-120">If your app has a bot or messaging extension, your icons also will be included in your Microsoft Azure Bot Service registration.</span></span>

### <a name="color-icon"></a><span data-ttu-id="5e95e-121">Icône couleur</span><span class="sxs-lookup"><span data-stu-id="5e95e-121">Color icon</span></span>

<span data-ttu-id="5e95e-122">La version couleur de votre icône s’affiche dans la plupart des scénarios de teams et doit être 192x192 pixels.</span><span class="sxs-lookup"><span data-stu-id="5e95e-122">The color version of your icon displays in most Teams scenarios and must be 192x192 pixels.</span></span> <span data-ttu-id="5e95e-123">Le symbole de votre icône (96 x 96 pixels) peut être une couleur ou des couleurs, mais il doit être placé sur un arrière-plan Uni ou entièrement transparent.</span><span class="sxs-lookup"><span data-stu-id="5e95e-123">Your icon symbol (96x96 pixels) can be any color or colors, but it must sit on a solid or fully transparent square background.</span></span>

<span data-ttu-id="5e95e-124">Teams rogne automatiquement votre icône pour afficher un carré avec des angles arrondis dans plusieurs scénarios et une forme hexagonale dans les scénarios de robot.</span><span class="sxs-lookup"><span data-stu-id="5e95e-124">Teams automatically crops your icon to display a square with rounded corners in multiple scenarios and a hexagonal shape in bot scenarios.</span></span> <span data-ttu-id="5e95e-125">Incluez 48 pixels de remplissage pour que ces cultures puissent être effectuées sans perte de détail.</span><span class="sxs-lookup"><span data-stu-id="5e95e-125">Include 48 pixels of padding around your symbol so these crops can be made without losing any detail.</span></span>

:::image type="content" source="../../assets/images/icons/design-color-icon.png" alt-text="Conseils de conception de l’icône couleur des équipes." border="false":::

### <a name="outline-icon"></a><span data-ttu-id="5e95e-127">Icône de plan</span><span class="sxs-lookup"><span data-stu-id="5e95e-127">Outline icon</span></span>

<span data-ttu-id="5e95e-128">Une icône en mode plan s’affiche dans deux scénarios :</span><span class="sxs-lookup"><span data-stu-id="5e95e-128">An outline icon displays in two scenarios:</span></span>

* <span data-ttu-id="5e95e-129">Lorsque votre application est en cours d’utilisation et « levée » dans la barre de l’application située à gauche de teams.</span><span class="sxs-lookup"><span data-stu-id="5e95e-129">When your app is in use and “hoisted” on the app bar on the left of Teams.</span></span>
* <span data-ttu-id="5e95e-130">Lorsqu’un utilisateur épingle l’extension de messagerie de votre application.</span><span class="sxs-lookup"><span data-stu-id="5e95e-130">when a user pins your app's messaging extension.</span></span>

<span data-ttu-id="5e95e-131">L’icône doit être de 32x32 pixels.</span><span class="sxs-lookup"><span data-stu-id="5e95e-131">The icon must be 32x32 pixels.</span></span> <span data-ttu-id="5e95e-132">Il peut être blanc avec un arrière-plan transparent ou transparent avec un arrière-plan blanc (aucune autre couleur n’est autorisée).</span><span class="sxs-lookup"><span data-stu-id="5e95e-132">It can be white with a transparent background or transparent with a white background (no other colors are permitted).</span></span> <span data-ttu-id="5e95e-133">L’icône de contour ne doit pas comporter de remplissage supplémentaire pour le symbole.</span><span class="sxs-lookup"><span data-stu-id="5e95e-133">The outline icon should not have any extra padding around the symbol.</span></span>

:::image type="content" source="../../assets/images/icons/design-outline-icon.png" alt-text="Conseils de conception de l’icône couleur des équipes." border="false":::

### <a name="best-practices"></a><span data-ttu-id="5e95e-135">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="5e95e-135">Best practices</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-do.png" alt-text="Illustration illustrant la conception de vos icônes d’application." border="false":::

#### <a name="do-follow-the-precise-outline-icon-guidelines"></a><span data-ttu-id="5e95e-137">Do : suivre les instructions d’icône de contour précises</span><span class="sxs-lookup"><span data-stu-id="5e95e-137">Do: Follow the precise outline icon guidelines</span></span>

<span data-ttu-id="5e95e-138">Les valeurs RVB du blanc utilisé dans votre icône doivent être rouges : 255, vert : 255, bleu : 255.</span><span class="sxs-lookup"><span data-stu-id="5e95e-138">The RGB values of white used in your icon must be Red: 255, Green: 255, Blue: 255.</span></span> <span data-ttu-id="5e95e-139">Toutes les autres parties de l’icône de contour doivent être entièrement transparentes, avec la couche alpha définie sur 0.</span><span class="sxs-lookup"><span data-stu-id="5e95e-139">All other parts of the outline icon must be fully transparent, with the alpha channel set to 0.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-dont.png" alt-text="Illustration montrant comment ne pas concevoir vos icônes d’application." border="false":::

#### <a name="dont-crop-in-a-circular-or-rounded-square-shape"></a><span data-ttu-id="5e95e-141">Ne pas : Rogner dans une forme circulaire ou en carré arrondi</span><span class="sxs-lookup"><span data-stu-id="5e95e-141">Don't: Crop in a circular or rounded square shape</span></span>

<span data-ttu-id="5e95e-142">L’icône de couleur soumise dans votre package d’application doit être carrée.</span><span class="sxs-lookup"><span data-stu-id="5e95e-142">The color icon submitted in your app package must be square.</span></span> <span data-ttu-id="5e95e-143">N’arrondissez pas les coins de votre icône.</span><span class="sxs-lookup"><span data-stu-id="5e95e-143">Don’t round the corners of your icon.</span></span> <span data-ttu-id="5e95e-144">Teams ajuste automatiquement le rayon d’arrondi.</span><span class="sxs-lookup"><span data-stu-id="5e95e-144">Teams automatically adjusts the corner radius.</span></span>

   :::column-end:::
:::row-end:::

### <a name="examples"></a><span data-ttu-id="5e95e-145">Exemples</span><span class="sxs-lookup"><span data-stu-id="5e95e-145">Examples</span></span>

<span data-ttu-id="5e95e-146">Voici comment les icônes d’application apparaissent dans les différents contextes et fonctionnalités de teams.</span><span class="sxs-lookup"><span data-stu-id="5e95e-146">Here's how app icons appear in different Teams capabilities and contexts.</span></span>

#### <a name="personal-app"></a><span data-ttu-id="5e95e-147">Application personnelle</span><span class="sxs-lookup"><span data-stu-id="5e95e-147">Personal app</span></span>

:::image type="content" source="../../assets/images/icons/personal-app-icon-example.png" alt-text="Exemple illustrant l’apparence d’une icône d’application dans une application personnelle." border="false":::

#### <a name="bot-channel"></a><span data-ttu-id="5e95e-149">Bot (canal)</span><span class="sxs-lookup"><span data-stu-id="5e95e-149">Bot (channel)</span></span>

:::image type="content" source="../../assets/images/icons/bot-icon-example.png" alt-text="Exemple illustrant l’apparence d’une icône d’application sur un robot au sein d’un canal." border="false":::

#### <a name="messaging-extension"></a><span data-ttu-id="5e95e-151">Extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="5e95e-151">Messaging extension</span></span>

:::image type="content" source="../../assets/images/icons/messaging-extension-icon-example.png" alt-text="<>texte de remplacement " border="false":::
