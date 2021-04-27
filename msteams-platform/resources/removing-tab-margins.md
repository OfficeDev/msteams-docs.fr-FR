---
title: Suppression des marges d'onglet dans Microsoft Teams
author: laujan
description: Décrit comment la suppression des marges d'onglet améliorera l'expérience du développeur.
keywords: remplissage des marges de suppression de tabulation
ms.topic: reference
localization_priority: Normal
ms.author: lomeybur
ms.openlocfilehash: 78d97dca73e7fce2bf4b911f5ea4588525667378
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019712"
---
# <a name="tab-margin-changes"></a><span data-ttu-id="288ba-104">Modifications des marges de l’onglet</span><span class="sxs-lookup"><span data-stu-id="288ba-104">Tab margin changes</span></span>

<span data-ttu-id="288ba-105">Ce document décrit comment la suppression des marges autour de tous les onglets dans Microsoft Teams améliorera l'expérience du développeur lors de la création d'applications.</span><span class="sxs-lookup"><span data-stu-id="288ba-105">This document describes how the removal of margins around all tabs in Microsoft Teams will enhance the developer's experience when building apps.</span></span> <span data-ttu-id="288ba-106">Il s'agit d'une amélioration introduite dans Microsoft Teams en 2021.</span><span class="sxs-lookup"><span data-stu-id="288ba-106">This is an enhancement introduced in Microsoft Teams in 2021.</span></span>
<span data-ttu-id="288ba-107">La suppression des marges autour de tous les onglets permettra aux développeurs de créer des applications qui semblent plus natives à Teams.</span><span class="sxs-lookup"><span data-stu-id="288ba-107">Removing the margins around all tabs will allow developers to build apps that look more native to Teams.</span></span> <span data-ttu-id="288ba-108">Cela s'alignera également sur nos [conceptions de kit d'interface utilisateur.](~/tabs/design/tabs.md)</span><span class="sxs-lookup"><span data-stu-id="288ba-108">This will also align with our [UI kit designs](~/tabs/design/tabs.md).</span></span> <span data-ttu-id="288ba-109">La plupart des applications ont déjà une meilleure apparence sans les marges qui entourent leur expérience.</span><span class="sxs-lookup"><span data-stu-id="288ba-109">Most apps already look better without the margins surrounding their experiences.</span></span> <span data-ttu-id="288ba-110">Toutefois, certains onglets sont visuellement affectés par cette modification, et les développeurs doivent apporter les modifications nécessaires.</span><span class="sxs-lookup"><span data-stu-id="288ba-110">However, some tabs are visually affected by this change, and developers must make the necessary changes.</span></span>

:::image type="content" source="../assets/images/tabs/remove-margins-tabs.png" alt-text="Tabulation et sans marges" border="false":::

> [!NOTE]
> <span data-ttu-id="288ba-112">Cette fonctionnalité n'est pas applicable aux clients mobiles, car les onglets des clients mobiles n'ont pas de marges.</span><span class="sxs-lookup"><span data-stu-id="288ba-112">This feature is not applicable to mobile clients, as the tabs viewed in the mobile clients do not have margins.</span></span> 

## <a name="timelines"></a><span data-ttu-id="288ba-113">Chronologies</span><span class="sxs-lookup"><span data-stu-id="288ba-113">Timelines</span></span>

* <span data-ttu-id="288ba-114">5 mars 2021 - Marges supprimées dans la prévisualisation [publique pour les développeurs.](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="288ba-114">March 5, 2021 - Margins removed in [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
* <span data-ttu-id="288ba-115">15 juin 2021 - Les marges seront supprimées en production.</span><span class="sxs-lookup"><span data-stu-id="288ba-115">June 15, 2021 - Margins will be removed in production.</span></span>

## <a name="guidelines"></a><span data-ttu-id="288ba-116">Conseils</span><span class="sxs-lookup"><span data-stu-id="288ba-116">Guidelines</span></span>

<span data-ttu-id="288ba-117">Les applications Microsoft Teams qui utilisent des onglets seront affectées par cette modification.</span><span class="sxs-lookup"><span data-stu-id="288ba-117">Microsoft Teams apps that use tabs will be affected by this change.</span></span> <span data-ttu-id="288ba-118">Les développeurs doivent basculer vers [la](~/resources/dev-preview/developer-preview-intro.md) prévisualisation publique pour les développeurs afin de déterminer la façon dont leurs onglets sont affectés et d'apporter les modifications nécessaires.</span><span class="sxs-lookup"><span data-stu-id="288ba-118">Developers must switch to [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md) in order to determine how their tabs are affected and make the necessary changes.</span></span>

<span data-ttu-id="288ba-119">Les développeurs d'onglets ne doivent pas compter sur Teams pour fournir des marges autour de leurs onglets.</span><span class="sxs-lookup"><span data-stu-id="288ba-119">Tab developers must not rely on Teams to provide margins surrounding their tabs.</span></span> <span data-ttu-id="288ba-120">Les développeurs sont encouragés à ajouter des marges autour de leurs conceptions d'onglets lorsque cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="288ba-120">Developers are encouraged to add margins around their tab designs where it is required.</span></span> <span data-ttu-id="288ba-121">Les conceptions d'applications en production peuvent ressembler à un remplissage supplémentaire, c'est-à-dire des marges fournies par Teams et des marges fournies par l'onglet. Toutefois, le remplissage supplémentaire n'est que temporaire et va disparaître dans quelques semaines, ne laissant que le remplissage fourni par l'application.</span><span class="sxs-lookup"><span data-stu-id="288ba-121">App designs in production can look like there is extra padding, that is, margins provided by Teams and margins provided by the tab. However, the extra padding is only temporary and will go away in a few weeks, leaving only the app's provided padding.</span></span>

## <a name="faq"></a><span data-ttu-id="288ba-122">FAQ</span><span class="sxs-lookup"><span data-stu-id="288ba-122">FAQ</span></span>

<span data-ttu-id="288ba-123">**Est-il possible pour le chrome de l'application, comme la barre d'en-tête ou la barre des tâches, d'toucher les bords de nos conceptions ?**</span><span class="sxs-lookup"><span data-stu-id="288ba-123">**Is it OK for app chrome, such as header bar or taskbar, to touch the edges of our designs?**</span></span>

<span data-ttu-id="288ba-124">Oui, c'est correct et encouragé.</span><span class="sxs-lookup"><span data-stu-id="288ba-124">Yes, this is fine and encouraged.</span></span> <span data-ttu-id="288ba-125">Cela permet à l'application de se sentir native.</span><span class="sxs-lookup"><span data-stu-id="288ba-125">This helps the app feel native.</span></span>

<span data-ttu-id="288ba-126">**Est-il possible pour le contenu de l'application, comme le texte, les logos et les images, d'toucher les bords gauche et droit de nos conceptions ?**</span><span class="sxs-lookup"><span data-stu-id="288ba-126">**Is it OK for app content, such as text, logos, and images, to touch the left and right edges of our designs?**</span></span>

<span data-ttu-id="288ba-127">Non, vous devez fournir votre propre remplissage ou marges à gauche et à droite de tout le contenu de l'application pour vous assurer qu'il ne touche pas les bords de votre interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="288ba-127">No, you must provide your own padding or margins to the left and right of all app content to ensure it does not touch the edges of your UI.</span></span> <span data-ttu-id="288ba-128">Vous pouvez également ajouter des marges en haut de votre onglet, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="288ba-128">You can also add margins at the top of your tab, if required.</span></span>

<span data-ttu-id="288ba-129">**Quelle est la taille des marges précédemment appliquées par Teams ?**</span><span class="sxs-lookup"><span data-stu-id="288ba-129">**What's the size of the margins Teams previously applied?**</span></span>

* <span data-ttu-id="288ba-130">Gauche et droite : 20 px</span><span class="sxs-lookup"><span data-stu-id="288ba-130">Left and right: 20px</span></span>
* <span data-ttu-id="288ba-131">Haut : 16 px</span><span class="sxs-lookup"><span data-stu-id="288ba-131">Top: 16px</span></span>
* <span data-ttu-id="288ba-132">Bas : 0px</span><span class="sxs-lookup"><span data-stu-id="288ba-132">Bottom: 0px</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="288ba-133">Les marges de tous les onglets sont supprimées : onglets personnels, onglets de conversation (groupe), onglets de réunion et onglets de canal.</span><span class="sxs-lookup"><span data-stu-id="288ba-133">All tabs have their margins removed: personal tabs, (group) chat tabs, meeting tabs, and channel tabs.</span></span>
> * <span data-ttu-id="288ba-134">Il n'existe aucun moyen d'opter ou de refuser cette modification.</span><span class="sxs-lookup"><span data-stu-id="288ba-134">There is no way to opt-in or opt-out of this change.</span></span> <span data-ttu-id="288ba-135">Elle s'applique à tous les onglets.</span><span class="sxs-lookup"><span data-stu-id="288ba-135">It will apply to all tabs.</span></span>
> * <span data-ttu-id="288ba-136">Cette modification peut affecter les onglets qui s'appuient sur Microsoft Teams pour fournir des marges autour de leur interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="288ba-136">This change can affect tabs that rely on Microsoft Teams to provide margins surrounding their UI.</span></span>
