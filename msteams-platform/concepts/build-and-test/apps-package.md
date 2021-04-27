---
title: Package de votre application
description: Découvrez comment mettre en package votre application Microsoft Teams pour le test, le téléchargement et la publication dans le Store.
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: c8341f3d83b5e6610e44276d6732affa1d1c1e91
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020139"
---
# <a name="create-an-app-package-for-your-microsoft-teams-app"></a><span data-ttu-id="a152f-103">Créer un package d'application pour votre application Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="a152f-103">Create an app package for your Microsoft Teams app</span></span>

<span data-ttu-id="a152f-104">Les applications dans Teams sont définies par un fichier JSON manifeste d'application et regroupées dans un package d'application avec leurs icônes.</span><span class="sxs-lookup"><span data-stu-id="a152f-104">Apps in Teams are defined by an app manifest JSON file, and bundled in an app package with their icons.</span></span> <span data-ttu-id="a152f-105">Vous aurez besoin d'un package d'application pour télécharger et installer votre application dans Teams et publier dans votre catalogue d'applications métier ou dans AppSource.</span><span class="sxs-lookup"><span data-stu-id="a152f-105">You'll need an app package to upload and install your app in Teams and publish to either your Line of Business app catalog or to AppSource.</span></span>

<span data-ttu-id="a152f-106">Un package d'application Teams est un fichier .zip contenant les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="a152f-106">A Teams app package is a .zip file containing the following:</span></span>

* <span data-ttu-id="a152f-107">Un fichier manifeste nommé , qui spécifie les attributs de votre application et pointe vers les ressources requises pour votre expérience, telles que l'emplacement de sa page de configuration d'onglet ou l'ID de l'application Microsoft pour `manifest.json` son bot.</span><span class="sxs-lookup"><span data-stu-id="a152f-107">A manifest file named `manifest.json`, which specifies attributes of your app and points to required resources for your experience, such the location of its tab configuration page or the Microsoft app ID for its bot.</span></span>
* <span data-ttu-id="a152f-108">[Icônes de couleur et de plan pour votre application.](#app-icons)</span><span class="sxs-lookup"><span data-stu-id="a152f-108">[Color and outline icons for your app](#app-icons).</span></span>

## <a name="creating-a-manifest"></a><span data-ttu-id="a152f-109">Création d’un manifeste</span><span class="sxs-lookup"><span data-stu-id="a152f-109">Creating a manifest</span></span>

<span data-ttu-id="a152f-110">**Teams App Studio peut** vous aider à configurer votre manifeste.</span><span class="sxs-lookup"><span data-stu-id="a152f-110">**Teams App Studio** can help configure your manifest.</span></span> <span data-ttu-id="a152f-111">Elle contient également une bibliothèque de contrôle React et des exemples configurables pour les cartes.</span><span class="sxs-lookup"><span data-stu-id="a152f-111">It also contains a React control library and configurable samples for cards.</span></span> <span data-ttu-id="a152f-112">Pour plus d'informations, [voir Vue d'ensemble d'App Studio.](~/concepts/build-and-test/app-studio-overview.md)</span><span class="sxs-lookup"><span data-stu-id="a152f-112">For more information, see [App Studio Overview](~/concepts/build-and-test/app-studio-overview.md).</span></span>

<span data-ttu-id="a152f-113">Votre fichier manifeste doit être nommé « manifest.js» et se trouver au niveau supérieur du package de chargement.</span><span class="sxs-lookup"><span data-stu-id="a152f-113">Your manifest file must be named "manifest.json" and be at the top level of the upload package.</span></span> <span data-ttu-id="a152f-114">Notez que les manifestes et les packages créés précédemment peuvent prendre en charge une version antérieure du schéma.</span><span class="sxs-lookup"><span data-stu-id="a152f-114">Note that manifests and packages built previously might support an older version of the schema.</span></span> <span data-ttu-id="a152f-115">Pour les applications Teams et en particulier la soumission d'AppSource (anciennement Office Store), vous devez utiliser le schéma [de manifeste actuel.](~/resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="a152f-115">For Teams apps and especially AppSource (formerly Office Store) submission, you must use the current [manifest schema](~/resources/schema/manifest-schema.md).</span></span>

> [!TIP]
> <span data-ttu-id="a152f-116">Spécifiez le schéma au début de votre manifeste pour activer IntelliSense ou une prise en charge similaire à partir de votre éditeur de code :</span><span class="sxs-lookup"><span data-stu-id="a152f-116">Specify the schema at the beginning of your manifest to enable IntelliSense or similar support from your code editor:</span></span>
>
> `"$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.9/MicrosoftTeams.schema.json",`
 
## <a name="app-icons"></a><span data-ttu-id="a152f-117">Icônes d'application</span><span class="sxs-lookup"><span data-stu-id="a152f-117">App icons</span></span>

<span data-ttu-id="a152f-118">Votre package d'application doit inclure deux versions PNG de l'icône de votre application : une icône de couleur et une icône plan.</span><span class="sxs-lookup"><span data-stu-id="a152f-118">Your app package must include two PNG versions of your app icon—a color icon and an outline icon.</span></span> <span data-ttu-id="a152f-119">Pour que votre application passe l'avis AppSource, ces icônes doivent respecter les exigences de taille suivantes.</span><span class="sxs-lookup"><span data-stu-id="a152f-119">For your app to pass the AppSource review, these icons must meet the following size requirements.</span></span>

> [!Note]
> <span data-ttu-id="a152f-120">Si votre application dispose d'un bot ou d'une extension de messagerie, vos icônes seront également incluses dans votre inscription au service de bot Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="a152f-120">If your app has a bot or messaging extension, your icons also will be included in your Microsoft Azure Bot Service registration.</span></span>

### <a name="color-icon"></a><span data-ttu-id="a152f-121">Icône Couleur</span><span class="sxs-lookup"><span data-stu-id="a152f-121">Color icon</span></span>

<span data-ttu-id="a152f-122">La version de couleur de votre icône s'affiche dans la plupart des scénarios Teams et doit être de 192 x 192 pixels.</span><span class="sxs-lookup"><span data-stu-id="a152f-122">The color version of your icon displays in most Teams scenarios and must be 192x192 pixels.</span></span> <span data-ttu-id="a152f-123">Votre symbole d'icône (96 x 96 pixels) peut être n'importe quelle couleur ou couleur, mais il doit être sur un arrière-plan carré plein ou entièrement transparent.</span><span class="sxs-lookup"><span data-stu-id="a152f-123">Your icon symbol (96x96 pixels) can be any color or colors, but it must sit on a solid or fully transparent square background.</span></span>

<span data-ttu-id="a152f-124">Teams taille automatiquement votre icône pour afficher un carré avec des coins arrondis dans plusieurs scénarios et une forme hexagonale dans les scénarios de bot.</span><span class="sxs-lookup"><span data-stu-id="a152f-124">Teams automatically crops your icon to display a square with rounded corners in multiple scenarios and a hexagonal shape in bot scenarios.</span></span> <span data-ttu-id="a152f-125">Incluez 48 pixels de remplissage autour de votre symbole pour que ces champs soient réalisés sans perte de détails.</span><span class="sxs-lookup"><span data-stu-id="a152f-125">Include 48 pixels of padding around your symbol so these crops can be made without losing any detail.</span></span>

:::image type="content" source="../../assets/images/icons/design-color-icon.png" alt-text="Icône de couleur Teams et conseils de conception." border="false":::

### <a name="outline-icon"></a><span data-ttu-id="a152f-127">Icône Plan</span><span class="sxs-lookup"><span data-stu-id="a152f-127">Outline icon</span></span>

<span data-ttu-id="a152f-128">Une icône de plan s'affiche dans deux scénarios :</span><span class="sxs-lookup"><span data-stu-id="a152f-128">An outline icon displays in two scenarios:</span></span>

* <span data-ttu-id="a152f-129">Lorsque votre application est en cours d'utilisation et « hissée » dans la barre d'application à gauche de Teams.</span><span class="sxs-lookup"><span data-stu-id="a152f-129">When your app is in use and “hoisted” on the app bar on the left of Teams.</span></span>
* <span data-ttu-id="a152f-130">lorsqu'un utilisateur épingle l'extension de messagerie de votre application.</span><span class="sxs-lookup"><span data-stu-id="a152f-130">when a user pins your app's messaging extension.</span></span>

<span data-ttu-id="a152f-131">L'icône doit être de 32 x 32 pixels.</span><span class="sxs-lookup"><span data-stu-id="a152f-131">The icon must be 32x32 pixels.</span></span> <span data-ttu-id="a152f-132">Il peut être blanc avec un arrière-plan transparent ou transparent avec un arrière-plan blanc (aucune autre couleur n'est autorisée).</span><span class="sxs-lookup"><span data-stu-id="a152f-132">It can be white with a transparent background or transparent with a white background (no other colors are permitted).</span></span> <span data-ttu-id="a152f-133">L'icône de plan ne doit pas avoir de remplissage supplémentaire autour du symbole.</span><span class="sxs-lookup"><span data-stu-id="a152f-133">The outline icon should not have any extra padding around the symbol.</span></span>

:::image type="content" source="../../assets/images/icons/design-outline-icon.png" alt-text="Recommandations en conception d'icônes de plan Teams." border="false":::

### <a name="best-practices"></a><span data-ttu-id="a152f-135">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="a152f-135">Best practices</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-do.png" alt-text="Illustration montrant comment concevoir les icônes de votre application." border="false":::

#### <a name="do-follow-the-precise-outline-icon-guidelines"></a><span data-ttu-id="a152f-137">À faire : suivez les instructions précises sur les icônes de plan</span><span class="sxs-lookup"><span data-stu-id="a152f-137">Do: Follow the precise outline icon guidelines</span></span>

<span data-ttu-id="a152f-138">Les valeurs RVB de blanc utilisées dans votre icône doivent être Rouge : 255, Vert : 255, Bleu : 255.</span><span class="sxs-lookup"><span data-stu-id="a152f-138">The RGB values of white used in your icon must be Red: 255, Green: 255, Blue: 255.</span></span> <span data-ttu-id="a152f-139">Toutes les autres parties de l'icône de plan doivent être entièrement transparentes, avec le canal alpha sur 0.</span><span class="sxs-lookup"><span data-stu-id="a152f-139">All other parts of the outline icon must be fully transparent, with the alpha channel set to 0.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-dont.png" alt-text="Illustration montrant comment ne pas concevoir les icônes de votre application." border="false":::

#### <a name="dont-crop-in-a-circular-or-rounded-square-shape"></a><span data-ttu-id="a152f-141">À ne pas faire : rognent dans une forme carrée arrondie ou arrondie</span><span class="sxs-lookup"><span data-stu-id="a152f-141">Don't: Crop in a circular or rounded square shape</span></span>

<span data-ttu-id="a152f-142">L'icône de couleur envoyée dans votre package d'application doit être carrée.</span><span class="sxs-lookup"><span data-stu-id="a152f-142">The color icon submitted in your app package must be square.</span></span> <span data-ttu-id="a152f-143">N'arrondissez pas les coins de votre icône.</span><span class="sxs-lookup"><span data-stu-id="a152f-143">Don’t round the corners of your icon.</span></span> <span data-ttu-id="a152f-144">Teams ajuste automatiquement le rayon d'angle.</span><span class="sxs-lookup"><span data-stu-id="a152f-144">Teams automatically adjusts the corner radius.</span></span>

   :::column-end:::
:::row-end:::

### <a name="examples"></a><span data-ttu-id="a152f-145">範例</span><span class="sxs-lookup"><span data-stu-id="a152f-145">Examples</span></span>

<span data-ttu-id="a152f-146">Voici comment les icônes d'application apparaissent dans différents contextes et fonctionnalités Teams.</span><span class="sxs-lookup"><span data-stu-id="a152f-146">Here's how app icons appear in different Teams capabilities and contexts.</span></span>

#### <a name="personal-app"></a><span data-ttu-id="a152f-147">Application personnelle</span><span class="sxs-lookup"><span data-stu-id="a152f-147">Personal app</span></span>

:::image type="content" source="../../assets/images/icons/personal-app-icon-example.png" alt-text="Exemple montrant l'apparence d'une icône d'application dans une application personnelle." border="false":::

#### <a name="bot-channel"></a><span data-ttu-id="a152f-149">Bot (canal)</span><span class="sxs-lookup"><span data-stu-id="a152f-149">Bot (channel)</span></span>

:::image type="content" source="../../assets/images/icons/bot-icon-example.png" alt-text="Exemple montrant l'apparence d'une icône d'application sur un bot à l'intérieur d'un canal." border="false":::

#### <a name="messaging-extension"></a><span data-ttu-id="a152f-151">Extension de la messagerie</span><span class="sxs-lookup"><span data-stu-id="a152f-151">Messaging extension</span></span>

:::image type="content" source="../../assets/images/icons/messaging-extension-icon-example.png" alt-text="<texte de>" border="false":::
