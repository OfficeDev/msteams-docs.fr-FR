---
title: Emballez votre application
description: Découvrez comment emballer votre application Microsoft Teams pour les tests, le téléchargement et l’édition en magasin.
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: 219e2d5341707ed51b7e0a3a8077f93df9eac640
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565213"
---
# <a name="create-a-microsoft-teams-app-package"></a><span data-ttu-id="22f38-103">Créer un paquet Microsoft Teams’application</span><span class="sxs-lookup"><span data-stu-id="22f38-103">Create a Microsoft Teams app package</span></span>

<span data-ttu-id="22f38-104">Vous avez besoin d’un package d’application mais vous prévoyez de distribuer Microsoft Teams application.</span><span class="sxs-lookup"><span data-stu-id="22f38-104">You need an app package however you plan to distribute your Microsoft Teams app.</span></span> <span data-ttu-id="22f38-105">Un paquet valide est un fichier ZIP qui contient les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="22f38-105">A valid package is a ZIP file that contains the following:</span></span>

* <span data-ttu-id="22f38-106">**Manifeste d’application**: Décrit comment votre application est configurée, y compris ses capacités, les ressources requises et d’autres attributs importants.</span><span class="sxs-lookup"><span data-stu-id="22f38-106">**App manifest**: Describes how your app is configured, including its capabilities, required resources, and other important attributes.</span></span>
* <span data-ttu-id="22f38-107">**Icônes d’application**: Chaque paquet nécessite une icône couleur et contour pour votre application.</span><span class="sxs-lookup"><span data-stu-id="22f38-107">**App icons**: Each package requires a color and outline icon for your app.</span></span>

## <a name="app-manifest"></a><span data-ttu-id="22f38-108">Manifeste d'application</span><span class="sxs-lookup"><span data-stu-id="22f38-108">App manifest</span></span>

<span data-ttu-id="22f38-109">Votre fichier manifeste d’application doit être au niveau supérieur du paquet avec le nom `manifest.json` .</span><span class="sxs-lookup"><span data-stu-id="22f38-109">Your app manifest file must be at the top level of the package with the name `manifest.json`.</span></span> 

<span data-ttu-id="22f38-110">Lors de la publication au Teams magasin, assurez-vous que votre manifeste fait référence au [dernier schéma.](~/resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="22f38-110">When publishing to the Teams store, make sure your manifest references the latest [schema](~/resources/schema/manifest-schema.md).</span></span>

## <a name="app-icons"></a><span data-ttu-id="22f38-111">Icônes d’application</span><span class="sxs-lookup"><span data-stu-id="22f38-111">App icons</span></span>

<span data-ttu-id="22f38-112">Votre package d’application doit inclure deux versions PNG de votre icône d’application : une version couleur et contour.</span><span class="sxs-lookup"><span data-stu-id="22f38-112">Your app package must include two PNG versions of your app icon: A color and outline version.</span></span>

> [!Note]
> <span data-ttu-id="22f38-113">Si votre application dispose d’une extension de bot ou de messagerie, vos icônes seront également incluses dans votre Microsoft Azure’enregistrement bot service.</span><span class="sxs-lookup"><span data-stu-id="22f38-113">If your app has a bot or messaging extension, your icons also will be included in your Microsoft Azure Bot Service registration.</span></span>

<span data-ttu-id="22f38-114">Pour que votre application passe l Teams magasin, ces icônes doivent répondre aux exigences de taille suivantes.</span><span class="sxs-lookup"><span data-stu-id="22f38-114">For your app to pass Teams store review, these icons must meet the following size requirements.</span></span>

### <a name="color-icon"></a><span data-ttu-id="22f38-115">Icône de couleur</span><span class="sxs-lookup"><span data-stu-id="22f38-115">Color icon</span></span>

<span data-ttu-id="22f38-116">La version couleur de votre icône s’affiche dans la plupart Teams scénarios et doit être de 192x192 pixels.</span><span class="sxs-lookup"><span data-stu-id="22f38-116">The color version of your icon displays in most Teams scenarios and must be 192x192 pixels.</span></span> <span data-ttu-id="22f38-117">Votre symbole d’icône (pixels 96x96) peut être n’importe quelle couleur, mais il doit s’asseoir sur un fond carré solide ou entièrement transparent.</span><span class="sxs-lookup"><span data-stu-id="22f38-117">Your icon symbol (96x96 pixels) can be any color, but it must sit on a solid or fully transparent square background.</span></span>

<span data-ttu-id="22f38-118">Teams automatiquement votre icône pour afficher un carré avec des coins arrondis dans plusieurs scénarios et une forme hexagonale dans les scénarios bot.</span><span class="sxs-lookup"><span data-stu-id="22f38-118">Teams automatically crops your icon to display a square with rounded corners in multiple scenarios and a hexagonal shape in bot scenarios.</span></span> <span data-ttu-id="22f38-119">Pour recadrer le symbole sans perdre de détails, incluez 48 pixels de rembourrage autour de votre symbole.</span><span class="sxs-lookup"><span data-stu-id="22f38-119">To crop the symbol without losing any detail, include 48 pixels of padding around your symbol.</span></span>

:::image type="content" source="../../assets/images/icons/design-color-icon.png" alt-text="Teams couleur et des conseils de conception." border="false":::

### <a name="outline-icon"></a><span data-ttu-id="22f38-121">Icône de contour</span><span class="sxs-lookup"><span data-stu-id="22f38-121">Outline icon</span></span>

<span data-ttu-id="22f38-122">Une icône de contour s’affiche dans deux scénarios :</span><span class="sxs-lookup"><span data-stu-id="22f38-122">An outline icon displays in two scenarios:</span></span>

* <span data-ttu-id="22f38-123">Lorsque votre application est en cours d’utilisation et « hissé » sur la barre d’application sur le côté gauche de Teams.</span><span class="sxs-lookup"><span data-stu-id="22f38-123">When your app is in use and “hoisted” on the app bar on the left side of Teams.</span></span>
* <span data-ttu-id="22f38-124">Lorsqu’un utilisateur épingle l’extension de messagerie de votre application.</span><span class="sxs-lookup"><span data-stu-id="22f38-124">When a user pins your app's messaging extension.</span></span>

<span data-ttu-id="22f38-125">L’icône doit être de 32x32 pixels.</span><span class="sxs-lookup"><span data-stu-id="22f38-125">The icon must be 32x32 pixels.</span></span> <span data-ttu-id="22f38-126">Il peut être blanc avec un fond transparent ou transparent avec un fond blanc (aucune autre couleur n’est permise).</span><span class="sxs-lookup"><span data-stu-id="22f38-126">It can be white with a transparent background or transparent with a white background (no other colors are permitted).</span></span> <span data-ttu-id="22f38-127">L’icône de contour ne doit pas avoir de rembourrage supplémentaire autour du symbole.</span><span class="sxs-lookup"><span data-stu-id="22f38-127">The outline icon should not have any extra padding around the symbol.</span></span>

:::image type="content" source="../../assets/images/icons/design-outline-icon.png" alt-text="Teams guidage de conception d’icône." border="false":::

### <a name="best-practices"></a><span data-ttu-id="22f38-129">Bonnes pratiques</span><span class="sxs-lookup"><span data-stu-id="22f38-129">Best practices</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-do.png" alt-text="Illustration montrant comment concevoir les icônes de votre application." border="false":::

#### <a name="do-follow-the-precise-outline-icon-guidelines"></a><span data-ttu-id="22f38-131">Faire: Suivez les lignes directrices précises icône contour</span><span class="sxs-lookup"><span data-stu-id="22f38-131">Do: Follow the precise outline icon guidelines</span></span>

<span data-ttu-id="22f38-132">Les valeurs RVB de blanc utilisées dans votre icône doivent être rouges : 255, vert : 255, bleu : 255.</span><span class="sxs-lookup"><span data-stu-id="22f38-132">The RGB values of white used in your icon must be Red: 255, Green: 255, Blue: 255.</span></span> <span data-ttu-id="22f38-133">Toutes les autres parties de l’icône de contour doivent être entièrement transparentes, avec le canal alpha réglé à 0.</span><span class="sxs-lookup"><span data-stu-id="22f38-133">All other parts of the outline icon must be fully transparent, with the alpha channel set to 0.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-dont.png" alt-text="Illustration montrant comment ne pas concevoir les icônes de votre application." border="false":::

#### <a name="dont-crop-in-a-circular-or-rounded-square-shape"></a><span data-ttu-id="22f38-135">Ne pas : Recadrer en forme carrée circulaire ou arrondie</span><span class="sxs-lookup"><span data-stu-id="22f38-135">Don't: Crop in a circular or rounded square shape</span></span>

<span data-ttu-id="22f38-136">L’icône couleur soumise dans votre paquet d’application doit être carrée.</span><span class="sxs-lookup"><span data-stu-id="22f38-136">The color icon submitted in your app package must be square.</span></span> <span data-ttu-id="22f38-137">Ne faites pas le tour des coins de votre icône.</span><span class="sxs-lookup"><span data-stu-id="22f38-137">Don’t round the corners of your icon.</span></span> <span data-ttu-id="22f38-138">Teams ajuste automatiquement le rayon d’angle.</span><span class="sxs-lookup"><span data-stu-id="22f38-138">Teams automatically adjusts the corner radius.</span></span>

   :::column-end:::
:::row-end:::

#### <a name="dont-copy-other-brands"></a><span data-ttu-id="22f38-139">Ne pas : Copier d’autres marques</span><span class="sxs-lookup"><span data-stu-id="22f38-139">Don't: Copy other brands</span></span>

<span data-ttu-id="22f38-140">Vos icônes ne doivent pas imiter les produits protégés par le droit d’auteur que vous ne possédez pas.</span><span class="sxs-lookup"><span data-stu-id="22f38-140">Your icons must not mimic any copyrighted products that you don't own.</span></span> <span data-ttu-id="22f38-141">Par exemple, un design similaire à un produit ou une marque Microsoft.</span><span class="sxs-lookup"><span data-stu-id="22f38-141">For example, a design similar to a Microsoft product or brand.</span></span>

### <a name="examples"></a><span data-ttu-id="22f38-142">Exemples</span><span class="sxs-lookup"><span data-stu-id="22f38-142">Examples</span></span>

<span data-ttu-id="22f38-143">Voici comment les icônes d’application apparaissent dans différentes Teams et contextes.</span><span class="sxs-lookup"><span data-stu-id="22f38-143">Here's how app icons appear in different Teams capabilities and contexts.</span></span>

#### <a name="personal-app"></a><span data-ttu-id="22f38-144">Application personnelle</span><span class="sxs-lookup"><span data-stu-id="22f38-144">Personal app</span></span>

:::image type="content" source="../../assets/images/icons/personal-app-icon-example.png" alt-text="Exemple montrant l’apparence d’une icône d’application dans une application personnelle." border="false":::

#### <a name="bot-channel"></a><span data-ttu-id="22f38-146">Bot (canal)</span><span class="sxs-lookup"><span data-stu-id="22f38-146">Bot (channel)</span></span>

:::image type="content" source="../../assets/images/icons/bot-icon-example.png" alt-text="Exemple montrant l’apparence d’une icône d’application sur un bot à l’intérieur du canal." border="false":::

#### <a name="messaging-extension"></a><span data-ttu-id="22f38-148">Extension de la messagerie</span><span class="sxs-lookup"><span data-stu-id="22f38-148">Messaging extension</span></span>

:::image type="content" source="../../assets/images/icons/messaging-extension-icon-example.png" alt-text="<texte alt>" border="false":::

## <a name="next-step"></a><span data-ttu-id="22f38-150">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="22f38-150">Next step</span></span>

<span data-ttu-id="22f38-151">Choisissez comment vous prévoyez distribuer votre application :</span><span class="sxs-lookup"><span data-stu-id="22f38-151">Choose how you plan to distribute your app:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="22f38-152">Sideload votre application dans Teams</span><span class="sxs-lookup"><span data-stu-id="22f38-152">Sideload your app in Teams</span></span>](~/concepts/deploy-and-publish/apps-upload.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="22f38-153">Publiez votre application sur votre org</span><span class="sxs-lookup"><span data-stu-id="22f38-153">Publish your app to your org</span></span>](/MicrosoftTeams/tenant-apps-catalog-teams?toc=/microsoftteams/platform/toc.json&bc=/MicrosoftTeams/breadcrumb/toc.json)
> [!div class="nextstepaction"]
> [<span data-ttu-id="22f38-154">Publiez votre application sur le magasin</span><span class="sxs-lookup"><span data-stu-id="22f38-154">Publish your app to the store</span></span>](~/concepts/deploy-and-publish/appsource/publish.md)
