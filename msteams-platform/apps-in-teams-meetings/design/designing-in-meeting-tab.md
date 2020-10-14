---
title: Concevoir un onglet en réunion
author: heath-hamilton
description: Découvrez comment concevoir efficacement un onglet de réunion pour Microsoft Teams.
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: a5c4d0cc0d2c61f422ea9bc189f164d02b28aae0
ms.sourcegitcommit: d61f14053fc695bc1956bf50e83956613c19ccca
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/13/2020
ms.locfileid: "48452658"
---
# <a name="design-an-in-meeting-tab"></a><span data-ttu-id="1c344-103">Concevoir un onglet en réunion</span><span class="sxs-lookup"><span data-stu-id="1c344-103">Design an in-meeting tab</span></span>

<span data-ttu-id="1c344-104">L’onglet dans la réunion est un canevas permettant d’augmenter la collaboration pendant les réunions.</span><span class="sxs-lookup"><span data-stu-id="1c344-104">The in-meeting tab is a canvas for augmenting collaboration during meetings.</span></span> <span data-ttu-id="1c344-105">En fonction de l’onglet Teams, les participants peuvent voir et interagir avec le contenu de l’application dans un espace dédié en dehors de la phase de la réunion via des affichages partagés ou basés sur des rôles.</span><span class="sxs-lookup"><span data-stu-id="1c344-105">Based on the Teams tab capability, attendees can see and interact with app content in a dedicated space outside the meeting stage through shared or role-based views.</span></span>

## <a name="use-cases"></a><span data-ttu-id="1c344-106">Cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="1c344-106">Use cases</span></span>

<span data-ttu-id="1c344-107">Les utilisateurs peuvent utiliser l’onglet dans la réunion pour :</span><span class="sxs-lookup"><span data-stu-id="1c344-107">People might use the in-meeting tab to:</span></span>

* <span data-ttu-id="1c344-108">Fournir des commentaires détaillés (par exemple, évaluer un candidat de travail)</span><span class="sxs-lookup"><span data-stu-id="1c344-108">Provide detailed feedback (for example, evaluate a job candidate)</span></span>
* <span data-ttu-id="1c344-109">Créer rapidement un élément de sondage, d’enquête ou de tâche pour les participants à la réunion</span><span class="sxs-lookup"><span data-stu-id="1c344-109">Quickly create a poll, survey, or task item for the meeting participants</span></span>
* <span data-ttu-id="1c344-110">Afficher les notes relatives à la réunion (par exemple, informations sur un prospect)</span><span class="sxs-lookup"><span data-stu-id="1c344-110">Display notes relevant to the meeting (for example, information about a sales lead)</span></span>

## <a name="example"></a><span data-ttu-id="1c344-111">Exemple</span><span class="sxs-lookup"><span data-stu-id="1c344-111">Example</span></span>

<span data-ttu-id="1c344-112">L’exemple suivant montre l’onglet dans la réunion qui affiche le contenu de l’application d’enquête.</span><span class="sxs-lookup"><span data-stu-id="1c344-112">The following example shows the in-meeting tab displaying survey app content.</span></span>

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-organizer-view.png" alt-text="Exemple montre à quoi peut ressembler l’onglet réunion sous la forme d’un organisateur de réunion.":::

<span data-ttu-id="1c344-114"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Voir le scénario complet (Figma)</a></span><span class="sxs-lookup"><span data-stu-id="1c344-114"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">See the full scenario (Figma)</a></span></span>

<span data-ttu-id="1c344-115"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Voir d’autres exemples d’utilisation (Figma)</a></span><span class="sxs-lookup"><span data-stu-id="1c344-115"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">See other example use cases (Figma)</a></span></span>

## <a name="anatomy"></a><span data-ttu-id="1c344-116">Anatomie</span><span class="sxs-lookup"><span data-stu-id="1c344-116">Anatomy</span></span>

<span data-ttu-id="1c344-117">L’onglet dans la réunion affiche le contenu de votre application à l’aide des dimensions suivantes :</span><span class="sxs-lookup"><span data-stu-id="1c344-117">The in-meeting tab displays your app content using the following dimensions:</span></span>

* <span data-ttu-id="1c344-118">**Largeur**: 280 pixels pour la zone WebView.</span><span class="sxs-lookup"><span data-stu-id="1c344-118">**Width**: 280 pixels for the webview area.</span></span> <span data-ttu-id="1c344-119">Il y a 20 pixels de remplissage sur les côtés gauche et droit de l’affichage WebView.</span><span class="sxs-lookup"><span data-stu-id="1c344-119">There are 20 pixels of padding on the left and right sides of the webview.</span></span>
* <span data-ttu-id="1c344-120">**Hauteur**: fond perdu en bas de l’onglet. Il y a 20 pixels de remplissage entre la zone d’affichage WebView et l’en-tête d’onglet.</span><span class="sxs-lookup"><span data-stu-id="1c344-120">**Height**: Full bleed to the bottom of the tab. There are 20 pixels of padding between the webview area and tab header.</span></span>

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-anatomy.png" alt-text="Exemple montre à quoi peut ressembler l’onglet réunion sous la forme d’un organisateur de réunion." border="false":::

1. <span data-ttu-id="1c344-122">**Icône**de l’application : point d’entrée de l’onglet dans la réunion.</span><span class="sxs-lookup"><span data-stu-id="1c344-122">**App icon**: The entry point to the in-meeting tab.</span></span>
1. <span data-ttu-id="1c344-123">**En-tête**: inclut le nom de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="1c344-123">**Header**: Includes the tab name.</span></span>
1. <span data-ttu-id="1c344-124">**Name**: nom de l’instance d’onglet.</span><span class="sxs-lookup"><span data-stu-id="1c344-124">**Name**: The name of the tab instance.</span></span>
1. <span data-ttu-id="1c344-125">**Faire disparaître : ferme**l’onglet. Toujours utiliser l’icône fermer en haut à droite au lieu d’une action dans le pied de page.</span><span class="sxs-lookup"><span data-stu-id="1c344-125">**Dismiss**: Dismisses the tab. Always use the upper-right close icon instead of an action in the footer.</span></span>
1. <span data-ttu-id="1c344-126">**WebView**: affiche le contenu de l’application tierce.</span><span class="sxs-lookup"><span data-stu-id="1c344-126">**Webview**: Displays all third-party app content.</span></span>

## <a name="behavior"></a><span data-ttu-id="1c344-127">Comportement</span><span class="sxs-lookup"><span data-stu-id="1c344-127">Behavior</span></span>

### <a name="scale"></a><span data-ttu-id="1c344-128">Échelle</span><span class="sxs-lookup"><span data-stu-id="1c344-128">Scale</span></span>

<span data-ttu-id="1c344-129">Actuellement, la largeur de l’onglet dans la réunion est fixe.</span><span class="sxs-lookup"><span data-stu-id="1c344-129">Currently, the width of the in-meeting tab is fixed.</span></span>

### <a name="scrolling"></a><span data-ttu-id="1c344-130">Défilement</span><span class="sxs-lookup"><span data-stu-id="1c344-130">Scrolling</span></span>

<span data-ttu-id="1c344-131">Voici ce que vous devez savoir sur le défilement dans l’onglet dans la réunion :</span><span class="sxs-lookup"><span data-stu-id="1c344-131">Here's what to know about scrolling in the in-meeting tab:</span></span>

* <span data-ttu-id="1c344-132">Vous devez uniquement pouvoir faire défiler verticalement.</span><span class="sxs-lookup"><span data-stu-id="1c344-132">You should only be able to scroll vertically.</span></span>
* <span data-ttu-id="1c344-133">Vous ne pouvez voir que le contenu auquel vous avez fait défiler (rien au-dessus ou en dessous).</span><span class="sxs-lookup"><span data-stu-id="1c344-133">You can only see the content you've scrolled to (nothing above or below).</span></span>
* <span data-ttu-id="1c344-134">La barre de défilement fait partie du contenu WebView.</span><span class="sxs-lookup"><span data-stu-id="1c344-134">The scrollbar is part of the webview content.</span></span>

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-scroll.png" alt-text="Exemple montre à quoi peut ressembler l’onglet réunion sous la forme d’un organisateur de réunion." border="false":::

### <a name="navigation"></a><span data-ttu-id="1c344-136">Navigation</span><span class="sxs-lookup"><span data-stu-id="1c344-136">Navigation</span></span>

<span data-ttu-id="1c344-137">Pour les scénarios avec des calques de navigation ou du contenu lourd, il est recommandé d’autoriser les utilisateurs à accéder à un calque secondaire.</span><span class="sxs-lookup"><span data-stu-id="1c344-137">For scenarios with navigation layers or heavy content, we recommend allowing users to navigate to a secondary layer.</span></span> <span data-ttu-id="1c344-138">Les utilisateurs doivent pouvoir revenir à la couche précédente.</span><span class="sxs-lookup"><span data-stu-id="1c344-138">Users must be able to go back to the previous layer.</span></span>

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-nav.png" alt-text="Exemple montre à quoi peut ressembler l’onglet réunion sous la forme d’un organisateur de réunion." border="false":::

## <a name="components"></a><span data-ttu-id="1c344-140">Composants</span><span class="sxs-lookup"><span data-stu-id="1c344-140">Components</span></span>

<span data-ttu-id="1c344-141">Les onglets de réunion sont créés principalement avec les <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">composants d’interface utilisateur suivants (Figma)</a>, qui sont basés sur le <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">système de conception Fluent</a>.</span><span class="sxs-lookup"><span data-stu-id="1c344-141">In-meeting tabs are built primarily with the following <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">UI components (Figma)</a>, which are based on the <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">Fluent Design System</a>.</span></span>

<span data-ttu-id="1c344-142">Composant</span><span class="sxs-lookup"><span data-stu-id="1c344-142">Component</span></span> | <span data-ttu-id="1c344-143">Conseils</span><span class="sxs-lookup"><span data-stu-id="1c344-143">Guidelines</span></span> | <span data-ttu-id="1c344-144">Exemple</span><span class="sxs-lookup"><span data-stu-id="1c344-144">Example</span></span>
 - | - | -
<span data-ttu-id="1c344-145">Bouton</span><span class="sxs-lookup"><span data-stu-id="1c344-145">Button</span></span> | <span data-ttu-id="1c344-146">Les boutons principal et secondaire peuvent être de taille moyenne ou petite</span><span class="sxs-lookup"><span data-stu-id="1c344-146">Primary and secondary buttons can be medium or small</span></span> | <span data-ttu-id="1c344-147">Envoyer une réponse</span><span class="sxs-lookup"><span data-stu-id="1c344-147">Send a response</span></span>
<span data-ttu-id="1c344-148">Input</span><span class="sxs-lookup"><span data-stu-id="1c344-148">Input</span></span> | <span data-ttu-id="1c344-149">Champ pour une saisie utilisateur partielle.</span><span class="sxs-lookup"><span data-stu-id="1c344-149">Field for brief user input.</span></span> <span data-ttu-id="1c344-150">Le texte de l’étiquette peut inclure une icône</span><span class="sxs-lookup"><span data-stu-id="1c344-150">Label text can include an icon</span></span>  | <span data-ttu-id="1c344-151">Entrer des commentaires</span><span class="sxs-lookup"><span data-stu-id="1c344-151">Enter feedback</span></span>
<span data-ttu-id="1c344-152">Liste déroulante</span><span class="sxs-lookup"><span data-stu-id="1c344-152">Dropdown</span></span> | <span data-ttu-id="1c344-153">Sélectionnez une ou plusieurs options dans une liste.</span><span class="sxs-lookup"><span data-stu-id="1c344-153">Select one or more options from a list.</span></span> <span data-ttu-id="1c344-154">Peut inclure des fonctionnalités de recherche et de sélection multiple</span><span class="sxs-lookup"><span data-stu-id="1c344-154">Can include search and multi-selection features</span></span> | <span data-ttu-id="1c344-155">Choisir une langue</span><span class="sxs-lookup"><span data-stu-id="1c344-155">Choose a language</span></span>
<span data-ttu-id="1c344-156">Contrôles de sélection</span><span class="sxs-lookup"><span data-stu-id="1c344-156">Selection controls</span></span> | <span data-ttu-id="1c344-157">Utilisez des cases à cocher pour plusieurs choix ou cases d’option et pour basculer pour les choix uniques.</span><span class="sxs-lookup"><span data-stu-id="1c344-157">Use checkboxes for multiple choices or radio buttons and toggles for single choices.</span></span> <span data-ttu-id="1c344-158">Pour des sélections plus détaillées, utilisez un curseur</span><span class="sxs-lookup"><span data-stu-id="1c344-158">For more detailed selections, use a slider</span></span> | <span data-ttu-id="1c344-159">Vote dans un sondage</span><span class="sxs-lookup"><span data-stu-id="1c344-159">Vote in a poll</span></span>
<span data-ttu-id="1c344-160">Alertes</span><span class="sxs-lookup"><span data-stu-id="1c344-160">Alerts</span></span> | <span data-ttu-id="1c344-161">Qu’il s’agisse d’un message urgent, d’un état d’erreur ou d’un avertissement, le message doit être court et n’interrompra pas la tâche actuelle de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1c344-161">Whether displaying an urgent message, error state, or warning, the message should be short and won't interrupt the user's current task</span></span> | <span data-ttu-id="1c344-162">Afficher un problème lors de l’envoi d’une réponse</span><span class="sxs-lookup"><span data-stu-id="1c344-162">Display issue when submitting a response</span></span>

## <a name="theming"></a><span data-ttu-id="1c344-163">Thèmes</span><span class="sxs-lookup"><span data-stu-id="1c344-163">Theming</span></span>

### <a name="colors"></a><span data-ttu-id="1c344-164">Couleurs</span><span class="sxs-lookup"><span data-stu-id="1c344-164">Colors</span></span>

<span data-ttu-id="1c344-165">Utilisez le <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">jeu de couleurs recommandé (Figma)</a> pour les arrière-plans, les avant-plans et les États de transport.</span><span class="sxs-lookup"><span data-stu-id="1c344-165">Use the <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">recommended color scheme (Figma)</a> for backgrounds, foregrounds, and conveying states.</span></span>

### <a name="typography"></a><span data-ttu-id="1c344-166">Typographie</span><span class="sxs-lookup"><span data-stu-id="1c344-166">Typography</span></span>

<span data-ttu-id="1c344-167">Utilisez les <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">tailles et épaisseurs de police recommandées (Figma)</a> pour les titres, le corps de texte et le texte de métadonnées.</span><span class="sxs-lookup"><span data-stu-id="1c344-167">Use the <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">recommended font sizes and weights (Figma)</a> for titles, body text, and metadata text.</span></span>

## <a name="best-practices"></a><span data-ttu-id="1c344-168">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="1c344-168">Best practices</span></span>

### <a name="responsiveness"></a><span data-ttu-id="1c344-169">Réactivité</span><span class="sxs-lookup"><span data-stu-id="1c344-169">Responsiveness</span></span>

<span data-ttu-id="1c344-170">Les mises en page d’onglets de réunion doivent pouvoir être redimensionnées en différentes tailles.</span><span class="sxs-lookup"><span data-stu-id="1c344-170">In-meeting tab layouts should be able to scale to various sizes.</span></span> <span data-ttu-id="1c344-171">Réfléchissez à la façon dont l’onglet mettra en forme et prendra en compte avant, pendant et après la réunion.</span><span class="sxs-lookup"><span data-stu-id="1c344-171">Consider how the tab will scale and take shape before, during, and after the meeting.</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-before-meeting.png" alt-text="Exemple montre à quoi peut ressembler l’onglet réunion sous la forme d’un organisateur de réunion." border="false":::

#### <a name="before-the-meeting"></a><span data-ttu-id="1c344-173">Avant la réunion</span><span class="sxs-lookup"><span data-stu-id="1c344-173">Before the meeting</span></span>

<span data-ttu-id="1c344-174">Assurez-vous que la disposition des tabulations peut s’adapter à la disposition droite ou gauche de différentes langues et que les contrôles se déplacent vers les emplacements appropriés.</span><span class="sxs-lookup"><span data-stu-id="1c344-174">Make sure your tab layout can adapt to a right or left layout for different languages and that controls move to the correct locations.</span></span> <span data-ttu-id="1c344-175">(Les mises en page pré-réunion peuvent également s’appliquer aux mises en page post-réunion.)</span><span class="sxs-lookup"><span data-stu-id="1c344-175">(Pre-meeting layouts can also apply to post-meeting layouts.)</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-during-meeting.png" alt-text="Exemple montre à quoi peut ressembler l’onglet réunion sous la forme d’un organisateur de réunion." border="false":::

#### <a name="during-the-meeting"></a><span data-ttu-id="1c344-177">Lors de la réunion</span><span class="sxs-lookup"><span data-stu-id="1c344-177">During the meeting</span></span>

<span data-ttu-id="1c344-178">Le contenu de la tabulation s’ajuste à la mise en page et à l’emplacement des onglets de réunion.</span><span class="sxs-lookup"><span data-stu-id="1c344-178">Tab content adjusts to the in-meeting tab layout and location.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="1c344-179">Thèmes</span><span class="sxs-lookup"><span data-stu-id="1c344-179">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-theming-do.png" alt-text="Exemple montre à quoi peut ressembler l’onglet réunion sous la forme d’un organisateur de réunion." border="false":::

#### <a name="do-design-for-a-dark-theme"></a><span data-ttu-id="1c344-181">Do : Design pour un thème sombre</span><span class="sxs-lookup"><span data-stu-id="1c344-181">Do: Design for a dark theme</span></span>

<span data-ttu-id="1c344-182">Les réunions de teams sont optimisées pour le mode sombre afin de réduire le bruit visuel et cognitif afin que les utilisateurs puissent se concentrer sur la discussion et le contenu partagé.</span><span class="sxs-lookup"><span data-stu-id="1c344-182">Teams meetings are optimized for dark mode to help reduce visual and cognitive noise so users can focus on the discussion and shared content.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-theming-dont.png" alt-text="Exemple montre à quoi peut ressembler l’onglet réunion sous la forme d’un organisateur de réunion." border="false":::

#### <a name="dont-use-unfamiliar-colors"></a><span data-ttu-id="1c344-184">Ne pas utiliser de couleurs inhabituelles</span><span class="sxs-lookup"><span data-stu-id="1c344-184">Don't: Use unfamiliar colors</span></span>

<span data-ttu-id="1c344-185">Les couleurs qui sont en conflit avec l’environnement de la réunion peuvent être gênantes et sembler moins natives à Teams.</span><span class="sxs-lookup"><span data-stu-id="1c344-185">Colors that clash with the meeting environment may be distracting and appear less native to Teams.</span></span>

   :::column-end:::
:::row-end:::

### <a name="scrolling"></a><span data-ttu-id="1c344-186">Défilement</span><span class="sxs-lookup"><span data-stu-id="1c344-186">Scrolling</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-scroll-do.png" alt-text="Exemple montre à quoi peut ressembler l’onglet réunion sous la forme d’un organisateur de réunion." border="false":::

#### <a name="do-scroll-vertically"></a><span data-ttu-id="1c344-188">Do : faites défiler verticalement</span><span class="sxs-lookup"><span data-stu-id="1c344-188">Do: Scroll vertically</span></span>

<span data-ttu-id="1c344-189">Les utilisateurs anticipent le défilement vertical dans Teams (et ailleurs).</span><span class="sxs-lookup"><span data-stu-id="1c344-189">Users anticipate vertical scrolling in Teams (and elsewhere).</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-scroll-dont.png" alt-text="Exemple montre à quoi peut ressembler l’onglet réunion sous la forme d’un organisateur de réunion." border="false":::

#### <a name="dont-scroll-horizontally"></a><span data-ttu-id="1c344-191">Ne pas faire défiler horizontalement</span><span class="sxs-lookup"><span data-stu-id="1c344-191">Don't: Scroll horizontally</span></span>

<span data-ttu-id="1c344-192">Le défilement horizontal n’est pas un comportement attendu dans Teams.</span><span class="sxs-lookup"><span data-stu-id="1c344-192">Horizontal scrolling isn’t an expected behavior in Teams.</span></span> <span data-ttu-id="1c344-193">Les autres canevas dans l’environnement de réunion sont déroulants verticalement.</span><span class="sxs-lookup"><span data-stu-id="1c344-193">Other canvases in the meeting environment scroll vertically.</span></span>

   :::column-end:::
:::row-end:::

### <a name="layout"></a><span data-ttu-id="1c344-194">Disposition</span><span class="sxs-lookup"><span data-stu-id="1c344-194">Layout</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-layout-do.png" alt-text="Exemple montre à quoi peut ressembler l’onglet réunion sous la forme d’un organisateur de réunion." border="false":::

#### <a name="do-single-columns"></a><span data-ttu-id="1c344-196">Do : colonnes uniques</span><span class="sxs-lookup"><span data-stu-id="1c344-196">Do: Single columns</span></span>

<span data-ttu-id="1c344-197">Étant donné la nature étroite de l’onglet dans la réunion, nous vous recommandons vivement d’afficher le contenu dans une seule colonne.</span><span class="sxs-lookup"><span data-stu-id="1c344-197">Given the in-meeting tab’s narrow nature, we strongly recommend displaying the contents in a single column.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-layout-dont.png" alt-text="Exemple montre à quoi peut ressembler l’onglet réunion sous la forme d’un organisateur de réunion." border="false":::

#### <a name="dont-multiple-columns"></a><span data-ttu-id="1c344-199">Ne pas : plusieurs colonnes</span><span class="sxs-lookup"><span data-stu-id="1c344-199">Don't: Multiple columns</span></span>

<span data-ttu-id="1c344-200">En raison de l’espace limité de l’onglet dans la réunion, les mises en page comportant plusieurs colonnes ne sont pas recommandées.</span><span class="sxs-lookup"><span data-stu-id="1c344-200">Due to the limited space of the in-meeting tab, layouts with more than one column aren’t recommended.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="1c344-201">Navigation</span><span class="sxs-lookup"><span data-stu-id="1c344-201">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-nav-do.png" alt-text="Exemple montre à quoi peut ressembler l’onglet réunion sous la forme d’un organisateur de réunion." border="false":::

#### <a name="do-have-a-back-button"></a><span data-ttu-id="1c344-203">Do : avoir un bouton retour</span><span class="sxs-lookup"><span data-stu-id="1c344-203">Do: Have a back button</span></span>

<span data-ttu-id="1c344-204">Si vous disposez de plusieurs couches de navigation, les utilisateurs doivent pouvoir revenir à leur vue précédente.</span><span class="sxs-lookup"><span data-stu-id="1c344-204">If you have more than one layer of navigation, users must be able to go back to their previous view.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-nav-dont.png" alt-text="Exemple montre à quoi peut ressembler l’onglet réunion sous la forme d’un organisateur de réunion." border="false":::

#### <a name="dont-include-another-close-button"></a><span data-ttu-id="1c344-206">Ne pas inclure d’autre bouton Fermer</span><span class="sxs-lookup"><span data-stu-id="1c344-206">Don't: Include another close button</span></span>

<span data-ttu-id="1c344-207">Une option permettant de fermer le contenu de l’onglet de la réunion peut entraîner des problèmes, car il existe déjà un bouton Fermer dans l’en-tête pour faire disparaître l’onglet de réunion lui-même.</span><span class="sxs-lookup"><span data-stu-id="1c344-207">Providing an option to close in-meeting tab content may cause issues since there’s already a close button in the header to dismiss the in-meeting tab itself.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-nav-caution.png" alt-text="Exemple montre à quoi peut ressembler l’onglet réunion sous la forme d’un organisateur de réunion." border="false":::

#### <a name="caution-using-dialogs-in-a-narrow-space"></a><span data-ttu-id="1c344-209">ATTENTION : utilisation de boîtes de dialogue dans un espace étroit</span><span class="sxs-lookup"><span data-stu-id="1c344-209">Caution: Using dialogs in a narrow space</span></span>

<span data-ttu-id="1c344-210">Les boîtes de dialogue, telles que les modules de tâches, dans l’onglet de la réunion déjà étroite peuvent encapsuler et obscurcir le contenu.</span><span class="sxs-lookup"><span data-stu-id="1c344-210">Dialogs, such as task modules, in the already narrow in-meeting tab might wrap and obscure the content.</span></span>

   :::column-end:::
:::row-end:::

## <a name="accessibility"></a><span data-ttu-id="1c344-211">Accessibilité</span><span class="sxs-lookup"><span data-stu-id="1c344-211">Accessibility</span></span>

<span data-ttu-id="1c344-212">Pour plus d’informations sur l’accessibilité, voir <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Figma</a>.</span><span class="sxs-lookup"><span data-stu-id="1c344-212">For information on accessibility, see <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Figma</a>.</span></span>

## <a name="resources"></a><span data-ttu-id="1c344-213">Ressources</span><span class="sxs-lookup"><span data-stu-id="1c344-213">Resources</span></span>

* <span data-ttu-id="1c344-214"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Fichiers Figma des extensions de réunion Microsoft teams</a></span><span class="sxs-lookup"><span data-stu-id="1c344-214"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Microsoft Teams meeting extensions Figma file</a></span></span>
* [<span data-ttu-id="1c344-215">Instructions de conception d’onglets</span><span class="sxs-lookup"><span data-stu-id="1c344-215">Tabs design guidelines</span></span>](../../tabs/design/tabs.md)
* [<span data-ttu-id="1c344-216">Instructions de conception d’onglets pour mobile</span><span class="sxs-lookup"><span data-stu-id="1c344-216">Tabs design guidelines for mobile</span></span>](../../tabs/design/tabs-mobile.md)

## <a name="validate-your-design"></a><span data-ttu-id="1c344-217">Valider votre conception</span><span class="sxs-lookup"><span data-stu-id="1c344-217">Validate your design</span></span>

<span data-ttu-id="1c344-218">Si vous envisagez de publier votre application dans AppSource, vous devez comprendre les problèmes de conception qui entraînent généralement l’échec des applications lors de l’envoi.</span><span class="sxs-lookup"><span data-stu-id="1c344-218">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1c344-219">Vérifier les instructions de validation de la conception</span><span class="sxs-lookup"><span data-stu-id="1c344-219">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines)
