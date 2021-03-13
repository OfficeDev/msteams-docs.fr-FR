---
title: Suppression des marges d’onglet dans Microsoft Teams
author: laujan
description: Décrit comment la suppression des marges d’onglet améliorera l’expérience du développeur.
keywords: remplissage des marges de suppression de tabulation
ms.topic: reference
ms.author: lomeybur
ms.openlocfilehash: 57e6b15999ffc41c0a3e09897ba565f9b3bf3705
ms.sourcegitcommit: 23ed7edf145df10dcfba15c43978eae9e0d451a8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/12/2021
ms.locfileid: "50753517"
---
# <a name="tab-margin-changes"></a><span data-ttu-id="26afb-104">Modifications des marges de l’onglet</span><span class="sxs-lookup"><span data-stu-id="26afb-104">Tab margin changes</span></span>

<span data-ttu-id="26afb-105">Ce document décrit comment la suppression des marges autour de tous les onglets dans Microsoft Teams améliorera l’expérience du développeur lors de la création d’applications.</span><span class="sxs-lookup"><span data-stu-id="26afb-105">This document describes how the removal of margins around all tabs in Microsoft Teams will enhance the developer's experience when building apps.</span></span> <span data-ttu-id="26afb-106">Il s’agit d’une amélioration introduite dans Microsoft Teams en 2021.</span><span class="sxs-lookup"><span data-stu-id="26afb-106">This is an enhancement introduced in Microsoft Teams in 2021.</span></span>
<span data-ttu-id="26afb-107">La suppression des marges autour de tous les onglets permettra aux développeurs de créer des applications qui semblent plus natives dans Teams.</span><span class="sxs-lookup"><span data-stu-id="26afb-107">Removing the margins around all tabs will allow developers to build apps that look more native to Teams.</span></span> <span data-ttu-id="26afb-108">Cela s’alignera également sur nos [conceptions de kit d’interface utilisateur.](~/tabs/design/tabs.md)</span><span class="sxs-lookup"><span data-stu-id="26afb-108">This will also align with our [UI kit designs](~/tabs/design/tabs.md).</span></span> <span data-ttu-id="26afb-109">La plupart des applications ont déjà une meilleure apparence sans les marges qui entourent leur expérience.</span><span class="sxs-lookup"><span data-stu-id="26afb-109">Most apps already look better without the margins surrounding their experiences.</span></span> <span data-ttu-id="26afb-110">Toutefois, certains onglets sont visuellement affectés par cette modification et les développeurs doivent apporter les modifications nécessaires.</span><span class="sxs-lookup"><span data-stu-id="26afb-110">However, some tabs are visually affected by this change, and developers must make the necessary changes.</span></span>

:::image type="content" source="../assets/images/tabs/remove-margins-tabs.png" alt-text="Tabulation et sans marges" border="false":::

## <a name="timelines"></a><span data-ttu-id="26afb-112">Chronologies</span><span class="sxs-lookup"><span data-stu-id="26afb-112">Timelines</span></span>

* <span data-ttu-id="26afb-113">5 mars 2021 - Marges supprimées dans la prévisualisation [publique pour les développeurs.](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="26afb-113">March 5, 2021 - Margins removed in [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
* <span data-ttu-id="26afb-114">1er mai 2021 : les marges seront supprimées en production.</span><span class="sxs-lookup"><span data-stu-id="26afb-114">May 1, 2021 - Margins will be removed in production.</span></span>

## <a name="guidelines"></a><span data-ttu-id="26afb-115">Conseils</span><span class="sxs-lookup"><span data-stu-id="26afb-115">Guidelines</span></span>

<span data-ttu-id="26afb-116">Les applications Microsoft Teams qui utilisent des onglets seront affectées par cette modification.</span><span class="sxs-lookup"><span data-stu-id="26afb-116">Microsoft Teams apps that use tabs will be affected by this change.</span></span> <span data-ttu-id="26afb-117">Les développeurs doivent basculer vers [la](~/resources/dev-preview/developer-preview-intro.md) prévisualisation publique pour les développeurs afin de déterminer la façon dont leurs onglets sont affectés et d’apporter les modifications nécessaires.</span><span class="sxs-lookup"><span data-stu-id="26afb-117">Developers must switch to [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md) in order to determine how their tabs are affected and make the necessary changes.</span></span>

<span data-ttu-id="26afb-118">Les développeurs d’onglets ne doivent pas compter sur Teams pour fournir des marges autour de leurs onglets.</span><span class="sxs-lookup"><span data-stu-id="26afb-118">Tab developers must not rely on Teams to provide margins surrounding their tabs.</span></span> <span data-ttu-id="26afb-119">Les développeurs sont encouragés à ajouter des marges autour de leurs conceptions d’onglets lorsque cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="26afb-119">Developers are encouraged to add margins around their tab designs where it is required.</span></span> <span data-ttu-id="26afb-120">Les conceptions d’applications en production peuvent ressembler à un remplissage supplémentaire, c’est-à-dire des marges fournies par Teams et des marges fournies par l’onglet. Toutefois, le remplissage supplémentaire n’est que temporaire et va disparaître dans quelques semaines, ne laissant que le remplissage fourni par l’application.</span><span class="sxs-lookup"><span data-stu-id="26afb-120">App designs in production can look like there is extra padding, that is, margins provided by Teams and margins provided by the tab. However, the extra padding is only temporary and will go away in a few weeks, leaving only the app's provided padding.</span></span>

## <a name="faq"></a><span data-ttu-id="26afb-121">FAQ</span><span class="sxs-lookup"><span data-stu-id="26afb-121">FAQ</span></span>

<span data-ttu-id="26afb-122">**Est-ce que le chrome de l’application, tel que la barre d’en-tête ou la barre des tâches, est autorisé à toucher les bords de nos conceptions ?**</span><span class="sxs-lookup"><span data-stu-id="26afb-122">**Is it OK for app chrome, such as header bar or taskbar, to touch the edges of our designs?**</span></span>

<span data-ttu-id="26afb-123">Oui, c’est correct et encouragé.</span><span class="sxs-lookup"><span data-stu-id="26afb-123">Yes, this is fine and encouraged.</span></span> <span data-ttu-id="26afb-124">Cela permet à l’application de se sentir native.</span><span class="sxs-lookup"><span data-stu-id="26afb-124">This helps the app feel native.</span></span>

<span data-ttu-id="26afb-125">**Est-il possible pour le contenu de l’application, comme le texte, les logos et les images, d’toucher les bords gauche et droit de nos conceptions ?**</span><span class="sxs-lookup"><span data-stu-id="26afb-125">**Is it OK for app content, such as text, logos, and images, to touch the left and right edges of our designs?**</span></span>

<span data-ttu-id="26afb-126">Non, vous devez fournir votre propre remplissage ou marges à gauche et à droite de tout le contenu de l’application pour vous assurer qu’il ne touche pas les bords de votre interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="26afb-126">No, you must provide your own padding or margins to the left and right of all app content to ensure it does not touch the edges of your UI.</span></span> <span data-ttu-id="26afb-127">Vous pouvez également ajouter des marges en haut de votre onglet, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="26afb-127">You can also add margins at the top of your tab, if required.</span></span>

<span data-ttu-id="26afb-128">**Quelle est la taille des marges précédemment appliquées par Teams ?**</span><span class="sxs-lookup"><span data-stu-id="26afb-128">**What's the size of the margins Teams previously applied?**</span></span>

* <span data-ttu-id="26afb-129">Gauche et droite : 20 px</span><span class="sxs-lookup"><span data-stu-id="26afb-129">Left and right: 20px</span></span>
* <span data-ttu-id="26afb-130">Haut : 16 px</span><span class="sxs-lookup"><span data-stu-id="26afb-130">Top: 16px</span></span>
* <span data-ttu-id="26afb-131">Bas : 0px</span><span class="sxs-lookup"><span data-stu-id="26afb-131">Bottom: 0px</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="26afb-132">Les marges de tous les onglets sont supprimées : onglets personnels, onglets de conversation (groupe), onglets de réunion et onglets de canal.</span><span class="sxs-lookup"><span data-stu-id="26afb-132">All tabs have their margins removed: personal tabs, (group) chat tabs, meeting tabs, and channel tabs.</span></span>
> * <span data-ttu-id="26afb-133">Il n’existe aucun moyen d’opter ou de refuser cette modification.</span><span class="sxs-lookup"><span data-stu-id="26afb-133">There is no way to opt-in or opt-out of this change.</span></span> <span data-ttu-id="26afb-134">Elle s’applique à tous les onglets.</span><span class="sxs-lookup"><span data-stu-id="26afb-134">It will apply to all tabs.</span></span>
> * <span data-ttu-id="26afb-135">Cette modification peut affecter les onglets qui s’appuient sur Microsoft Teams pour fournir des marges autour de leur interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="26afb-135">This change can affect tabs that rely on Microsoft Teams to provide margins surrounding their UI.</span></span>
