---
title: Package de votre application
description: Découvrez comment mettre en package votre application Microsoft Teams pour le test, le téléchargement et la publication dans le Store.
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: 219e2d5341707ed51b7e0a3a8077f93df9eac640
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565213"
---
# <a name="create-a-microsoft-teams-app-package"></a><span data-ttu-id="5fae1-103">Créer un package Microsoft Teams’application</span><span class="sxs-lookup"><span data-stu-id="5fae1-103">Create a Microsoft Teams app package</span></span>

<span data-ttu-id="5fae1-104">Vous avez besoin d’un package d’application, mais vous prévoyez de distribuer votre Microsoft Teams application.</span><span class="sxs-lookup"><span data-stu-id="5fae1-104">You need an app package however you plan to distribute your Microsoft Teams app.</span></span> <span data-ttu-id="5fae1-105">Un package valide est un fichier ZIP qui contient les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="5fae1-105">A valid package is a ZIP file that contains the following:</span></span>

* <span data-ttu-id="5fae1-106">**Manifeste de l’application**: décrit la configuration de votre application, notamment ses fonctionnalités, les ressources requises et d’autres attributs importants.</span><span class="sxs-lookup"><span data-stu-id="5fae1-106">**App manifest**: Describes how your app is configured, including its capabilities, required resources, and other important attributes.</span></span>
* <span data-ttu-id="5fae1-107">**Icônes d’application**: chaque package nécessite une icône de couleur et de plan pour votre application.</span><span class="sxs-lookup"><span data-stu-id="5fae1-107">**App icons**: Each package requires a color and outline icon for your app.</span></span>

## <a name="app-manifest"></a><span data-ttu-id="5fae1-108">Manifeste d'application</span><span class="sxs-lookup"><span data-stu-id="5fae1-108">App manifest</span></span>

<span data-ttu-id="5fae1-109">Votre fichier manifeste d’application doit se trouver au niveau supérieur du package avec le nom `manifest.json` .</span><span class="sxs-lookup"><span data-stu-id="5fae1-109">Your app manifest file must be at the top level of the package with the name `manifest.json`.</span></span> 

<span data-ttu-id="5fae1-110">Lors de la publication dans Teams store, assurez-vous que votre manifeste fait référence au [schéma le plus récent.](~/resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="5fae1-110">When publishing to the Teams store, make sure your manifest references the latest [schema](~/resources/schema/manifest-schema.md).</span></span>

## <a name="app-icons"></a><span data-ttu-id="5fae1-111">Icônes d’application</span><span class="sxs-lookup"><span data-stu-id="5fae1-111">App icons</span></span>

<span data-ttu-id="5fae1-112">Votre package d’application doit inclure deux versions PNG de l’icône de votre application : une version de couleur et une version plan.</span><span class="sxs-lookup"><span data-stu-id="5fae1-112">Your app package must include two PNG versions of your app icon: A color and outline version.</span></span>

> [!Note]
> <span data-ttu-id="5fae1-113">Si votre application dispose d’un bot ou d’une extension de messagerie, vos icônes seront également incluses dans votre inscription Microsoft Azure Bot Service.</span><span class="sxs-lookup"><span data-stu-id="5fae1-113">If your app has a bot or messaging extension, your icons also will be included in your Microsoft Azure Bot Service registration.</span></span>

<span data-ttu-id="5fae1-114">Pour que votre application soit Teams’avis dans le Store, ces icônes doivent respecter les exigences de taille suivantes.</span><span class="sxs-lookup"><span data-stu-id="5fae1-114">For your app to pass Teams store review, these icons must meet the following size requirements.</span></span>

### <a name="color-icon"></a><span data-ttu-id="5fae1-115">Icône Couleur</span><span class="sxs-lookup"><span data-stu-id="5fae1-115">Color icon</span></span>

<span data-ttu-id="5fae1-116">La version de couleur de votre icône s’affiche dans la plupart Teams scénarios et doit être de 192 x 192 pixels.</span><span class="sxs-lookup"><span data-stu-id="5fae1-116">The color version of your icon displays in most Teams scenarios and must be 192x192 pixels.</span></span> <span data-ttu-id="5fae1-117">Votre symbole d’icône (96 x 96 pixels) peut être n’importe quelle couleur, mais il doit être sur un arrière-plan carré plein ou entièrement transparent.</span><span class="sxs-lookup"><span data-stu-id="5fae1-117">Your icon symbol (96x96 pixels) can be any color, but it must sit on a solid or fully transparent square background.</span></span>

<span data-ttu-id="5fae1-118">Teams votre icône pour afficher automatiquement un carré avec des coins arrondis dans plusieurs scénarios et une forme hexagonale dans les scénarios de bot.</span><span class="sxs-lookup"><span data-stu-id="5fae1-118">Teams automatically crops your icon to display a square with rounded corners in multiple scenarios and a hexagonal shape in bot scenarios.</span></span> <span data-ttu-id="5fae1-119">Pour roger le symbole sans perdre de détail, incluez 48 pixels de remplissage autour de votre symbole.</span><span class="sxs-lookup"><span data-stu-id="5fae1-119">To crop the symbol without losing any detail, include 48 pixels of padding around your symbol.</span></span>

:::image type="content" source="../../assets/images/icons/design-color-icon.png" alt-text="Teams icône de couleur et des conseils de conception." border="false":::

### <a name="outline-icon"></a><span data-ttu-id="5fae1-121">Icône Plan</span><span class="sxs-lookup"><span data-stu-id="5fae1-121">Outline icon</span></span>

<span data-ttu-id="5fae1-122">Une icône de plan s’affiche dans deux scénarios :</span><span class="sxs-lookup"><span data-stu-id="5fae1-122">An outline icon displays in two scenarios:</span></span>

* <span data-ttu-id="5fae1-123">Lorsque votre application est en cours d’utilisation et « hissée » dans la barre de l’application sur le côté gauche de la Teams.</span><span class="sxs-lookup"><span data-stu-id="5fae1-123">When your app is in use and “hoisted” on the app bar on the left side of Teams.</span></span>
* <span data-ttu-id="5fae1-124">Lorsqu’un utilisateur épingle l’extension de messagerie de votre application.</span><span class="sxs-lookup"><span data-stu-id="5fae1-124">When a user pins your app's messaging extension.</span></span>

<span data-ttu-id="5fae1-125">L’icône doit être de 32 x 32 pixels.</span><span class="sxs-lookup"><span data-stu-id="5fae1-125">The icon must be 32x32 pixels.</span></span> <span data-ttu-id="5fae1-126">Il peut être blanc avec un arrière-plan transparent ou transparent avec un arrière-plan blanc (aucune autre couleur n’est autorisée).</span><span class="sxs-lookup"><span data-stu-id="5fae1-126">It can be white with a transparent background or transparent with a white background (no other colors are permitted).</span></span> <span data-ttu-id="5fae1-127">L’icône de plan ne doit pas avoir de remplissage supplémentaire autour du symbole.</span><span class="sxs-lookup"><span data-stu-id="5fae1-127">The outline icon should not have any extra padding around the symbol.</span></span>

:::image type="content" source="../../assets/images/icons/design-outline-icon.png" alt-text="Teams de conception d’icônes de plan." border="false":::

### <a name="best-practices"></a><span data-ttu-id="5fae1-129">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="5fae1-129">Best practices</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-do.png" alt-text="Illustration montrant comment concevoir les icônes de votre application." border="false":::

#### <a name="do-follow-the-precise-outline-icon-guidelines"></a><span data-ttu-id="5fae1-131">À faire : suivez les instructions précises sur les icônes de plan</span><span class="sxs-lookup"><span data-stu-id="5fae1-131">Do: Follow the precise outline icon guidelines</span></span>

<span data-ttu-id="5fae1-132">Les valeurs RVB de blanc utilisées dans votre icône doivent être Rouge : 255, Vert : 255, Bleu : 255.</span><span class="sxs-lookup"><span data-stu-id="5fae1-132">The RGB values of white used in your icon must be Red: 255, Green: 255, Blue: 255.</span></span> <span data-ttu-id="5fae1-133">Toutes les autres parties de l’icône de plan doivent être entièrement transparentes, avec le canal alpha sur 0.</span><span class="sxs-lookup"><span data-stu-id="5fae1-133">All other parts of the outline icon must be fully transparent, with the alpha channel set to 0.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-dont.png" alt-text="Illustration montrant comment ne pas concevoir les icônes de votre application." border="false":::

#### <a name="dont-crop-in-a-circular-or-rounded-square-shape"></a><span data-ttu-id="5fae1-135">À ne pas faire : rognent dans une forme carrée arrondie ou arrondie</span><span class="sxs-lookup"><span data-stu-id="5fae1-135">Don't: Crop in a circular or rounded square shape</span></span>

<span data-ttu-id="5fae1-136">L’icône de couleur envoyée dans votre package d’application doit être carrée.</span><span class="sxs-lookup"><span data-stu-id="5fae1-136">The color icon submitted in your app package must be square.</span></span> <span data-ttu-id="5fae1-137">N’arrondissez pas les coins de votre icône.</span><span class="sxs-lookup"><span data-stu-id="5fae1-137">Don’t round the corners of your icon.</span></span> <span data-ttu-id="5fae1-138">Teams ajuste automatiquement le rayon d’angle.</span><span class="sxs-lookup"><span data-stu-id="5fae1-138">Teams automatically adjusts the corner radius.</span></span>

   :::column-end:::
:::row-end:::

#### <a name="dont-copy-other-brands"></a><span data-ttu-id="5fae1-139">À ne pas faire : copier d’autres marques</span><span class="sxs-lookup"><span data-stu-id="5fae1-139">Don't: Copy other brands</span></span>

<span data-ttu-id="5fae1-140">Vos icônes ne doivent pas imiter les produits protégés par des droits d’auteur que vous ne possédez pas.</span><span class="sxs-lookup"><span data-stu-id="5fae1-140">Your icons must not mimic any copyrighted products that you don't own.</span></span> <span data-ttu-id="5fae1-141">Par exemple, une conception similaire à un produit ou une marque Microsoft.</span><span class="sxs-lookup"><span data-stu-id="5fae1-141">For example, a design similar to a Microsoft product or brand.</span></span>

### <a name="examples"></a><span data-ttu-id="5fae1-142">Exemples</span><span class="sxs-lookup"><span data-stu-id="5fae1-142">Examples</span></span>

<span data-ttu-id="5fae1-143">Voici comment les icônes d’application s’affichent dans Teams fonctionnalités et contextes différents.</span><span class="sxs-lookup"><span data-stu-id="5fae1-143">Here's how app icons appear in different Teams capabilities and contexts.</span></span>

#### <a name="personal-app"></a><span data-ttu-id="5fae1-144">Application personnelle</span><span class="sxs-lookup"><span data-stu-id="5fae1-144">Personal app</span></span>

:::image type="content" source="../../assets/images/icons/personal-app-icon-example.png" alt-text="Exemple montrant l’apparence d’une icône d’application dans une application personnelle." border="false":::

#### <a name="bot-channel"></a><span data-ttu-id="5fae1-146">Bot (canal)</span><span class="sxs-lookup"><span data-stu-id="5fae1-146">Bot (channel)</span></span>

:::image type="content" source="../../assets/images/icons/bot-icon-example.png" alt-text="Exemple montrant l’apparence d’une icône d’application sur un bot à l’intérieur d’un canal." border="false":::

#### <a name="messaging-extension"></a><span data-ttu-id="5fae1-148">Extension de la messagerie</span><span class="sxs-lookup"><span data-stu-id="5fae1-148">Messaging extension</span></span>

:::image type="content" source="../../assets/images/icons/messaging-extension-icon-example.png" alt-text="<texte de>" border="false":::

## <a name="next-step"></a><span data-ttu-id="5fae1-150">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="5fae1-150">Next step</span></span>

<span data-ttu-id="5fae1-151">Choisissez la façon dont vous prévoyez de distribuer votre application :</span><span class="sxs-lookup"><span data-stu-id="5fae1-151">Choose how you plan to distribute your app:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5fae1-152">Chargez une version de version de votre application dans Teams</span><span class="sxs-lookup"><span data-stu-id="5fae1-152">Sideload your app in Teams</span></span>](~/concepts/deploy-and-publish/apps-upload.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="5fae1-153">Publier votre application dans votre organisation</span><span class="sxs-lookup"><span data-stu-id="5fae1-153">Publish your app to your org</span></span>](/MicrosoftTeams/tenant-apps-catalog-teams?toc=/microsoftteams/platform/toc.json&bc=/MicrosoftTeams/breadcrumb/toc.json)
> [!div class="nextstepaction"]
> [<span data-ttu-id="5fae1-154">Publier votre application dans le Store</span><span class="sxs-lookup"><span data-stu-id="5fae1-154">Publish your app to the store</span></span>](~/concepts/deploy-and-publish/appsource/publish.md)
