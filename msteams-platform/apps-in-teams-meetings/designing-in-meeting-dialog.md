---
title: Conception d’une boîte de dialogue de réunion Microsoft teams
author: heath-hamilton
description: Conseils et meilleures pratiques pour la conception d’une boîte de dialogue de réunion pour Microsoft Teams.
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: 449e6cdf9aecefba9fe70099c961ab56955306f8
ms.sourcegitcommit: aabfd65a67e1889ec16f09476bc757dd4a46ec5b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/18/2020
ms.locfileid: "48098033"
---
# <a name="designing-an-in-meeting-dialog"></a><span data-ttu-id="047e1-103">Conception d’une boîte de dialogue de réunion</span><span class="sxs-lookup"><span data-stu-id="047e1-103">Designing an in-meeting dialog</span></span>

<span data-ttu-id="047e1-104">Les boîtes de dialogue de réunion sont affichées à l’étape de réunion Teams.</span><span class="sxs-lookup"><span data-stu-id="047e1-104">In-meeting dialogs display on the Teams meeting stage.</span></span> <span data-ttu-id="047e1-105">Elles requièrent l’attention, la confirmation ou l’interaction d’un utilisateur, mais elles sont subtiles et n’interrompent pas la réunion.</span><span class="sxs-lookup"><span data-stu-id="047e1-105">They require a user's attention, confirmation, or interaction but are subtle and don't interrupt the meeting.</span></span>

## <a name="use-cases"></a><span data-ttu-id="047e1-106">Cas d'utilisation</span><span class="sxs-lookup"><span data-stu-id="047e1-106">Use cases</span></span>

<span data-ttu-id="047e1-107">Les boîtes de dialogue de réunion sont déclenchées par un utilisateur (par exemple, l’organisateur de la réunion) qui peut souhaiter que les participants :</span><span class="sxs-lookup"><span data-stu-id="047e1-107">In-meeting dialogs are triggered by a user (such as the meeting organizer) who might want participants to:</span></span>

* <span data-ttu-id="047e1-108">Fournir des commentaires succincts</span><span class="sxs-lookup"><span data-stu-id="047e1-108">Provide brief feedback</span></span>
* <span data-ttu-id="047e1-109">Suivre une brève enquête ou sondage</span><span class="sxs-lookup"><span data-stu-id="047e1-109">Take a short survey or poll</span></span>
* <span data-ttu-id="047e1-110">Soumettre des approbations</span><span class="sxs-lookup"><span data-stu-id="047e1-110">Submit approvals</span></span>
* <span data-ttu-id="047e1-111">Obtenir les rappels</span><span class="sxs-lookup"><span data-stu-id="047e1-111">Get reminders</span></span>

## <a name="example"></a><span data-ttu-id="047e1-112">Exemple</span><span class="sxs-lookup"><span data-stu-id="047e1-112">Example</span></span>

<span data-ttu-id="047e1-113">L’exemple suivant montre à quoi la boîte de dialogue de réunion peut ressembler du point de vue d’un participant à la réunion.</span><span class="sxs-lookup"><span data-stu-id="047e1-113">The following example shows what the in-meeting dialog might look like from a meeting participant's perspective.</span></span> <span data-ttu-id="047e1-114">Comme vous pouvez le voir, le contenu et la tâche sont légers.</span><span class="sxs-lookup"><span data-stu-id="047e1-114">As you can see, the content and task are lightweight.</span></span>

:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-dialog-participant-view.png" alt-text="Cet exemple montre comment la boîte de dialogue de réunion peut ressembler du point de vue d’un participant à la réunion.":::

<span data-ttu-id="047e1-116"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Voir le scénario complet (Figma)</a></span><span class="sxs-lookup"><span data-stu-id="047e1-116"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">See the full scenario (Figma)</a></span></span>

<span data-ttu-id="047e1-117"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Voir d’autres exemples d’utilisation (Figma)</a></span><span class="sxs-lookup"><span data-stu-id="047e1-117"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">See other example use cases (Figma)</a></span></span>

## <a name="anatomy"></a><span data-ttu-id="047e1-118">Anatomie</span><span class="sxs-lookup"><span data-stu-id="047e1-118">Anatomy</span></span>

:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-dialog-anatomy.png" alt-text="Anatomie de l’interface utilisateur d’une vue de boîte de dialogue de réunion." border="false":::

1. <span data-ttu-id="047e1-120">**Icône de l’application**</span><span class="sxs-lookup"><span data-stu-id="047e1-120">**App icon**</span></span>
1. <span data-ttu-id="047e1-121">**Nom de l'application**</span><span class="sxs-lookup"><span data-stu-id="047e1-121">**App name**</span></span>
1. <span data-ttu-id="047e1-122">**Chaîne d’action**</span><span class="sxs-lookup"><span data-stu-id="047e1-122">**Action string**</span></span>
1. <span data-ttu-id="047e1-123">**Ignorer l’icône :** Ferme une seule boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="047e1-123">**Dismiss icon:** Closes a single dialog.</span></span> <span data-ttu-id="047e1-124">Toujours utiliser l’icône fermer en haut à droite au lieu d’une action dans le pied de page.</span><span class="sxs-lookup"><span data-stu-id="047e1-124">Always use the upper-right close icon instead of an action in the footer.</span></span>
1. <span data-ttu-id="047e1-125">**WebView**: affiche tous les boutons et le contenu d’application tiers (les boutons standard teams sont recommandés).</span><span class="sxs-lookup"><span data-stu-id="047e1-125">**Webview**: Displays all third-party app content and buttons (standard Teams buttons recommended).</span></span>

### <a name="sizing"></a><span data-ttu-id="047e1-126">Taille</span><span class="sxs-lookup"><span data-stu-id="047e1-126">Sizing</span></span>

<span data-ttu-id="047e1-127">Les boîtes de dialogue de réunion peuvent varier en fonction de la taille pour tenir compte de différents cas d’utilisation, mais vous devez toujours conserver les tailles de remplissage et de composant.</span><span class="sxs-lookup"><span data-stu-id="047e1-127">In-meeting dialogs can vary in size to account for different use cases, but you must always maintain padding and component sizes.</span></span>

* <span data-ttu-id="047e1-128">**Height**: la hauteur de la boîte de dialogue est déterminée par le contenu dans le WebView.</span><span class="sxs-lookup"><span data-stu-id="047e1-128">**Height**: The height of the dialog is determined by the content in the webview.</span></span> <span data-ttu-id="047e1-129">Le défilement vertical est pris en charge pour le contenu qui dépasse la hauteur maximale que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="047e1-129">Vertical scroll takes over for content that exceeds the maximum height you specify.</span></span>
* <span data-ttu-id="047e1-130">**Width**: la largeur de WebView est une valeur absolue comprise dans la plage que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="047e1-130">**Width**: The width of the webview is an absolute value within the range you specify.</span></span>

:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-dialog-sizing.png" alt-text="Illustration des dimensions possibles d’une boîte de dialogue de réunion. Height : la hauteur de la boîte de dialogue est déterminée par le contenu dans le WebView. Le défilement vertical est pris en charge pour le contenu qui dépasse la hauteur maximale (définie par vous). Min : aucun. Max : 400 pixels (320 pixels WebView). Width : la largeur de WebView est une valeur absolue comprise dans la plage que vous spécifiez. Minimum : 288 pixels (256 pixels WebView). Max : 468 pixels (436 pixels WebView)." border="false":::

## <a name="behavior"></a><span data-ttu-id="047e1-132">Comportement</span><span class="sxs-lookup"><span data-stu-id="047e1-132">Behavior</span></span>

<span data-ttu-id="047e1-133">Voir comportement général de la boîte de dialogue de réunion, tel que REST, chargement, etc., dans <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Figma</a>.</span><span class="sxs-lookup"><span data-stu-id="047e1-133">See general in-meeting dialog behavior, such as rest, loading, and more, in <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Figma</a>.</span></span>

### <a name="position"></a><span data-ttu-id="047e1-134">Position</span><span class="sxs-lookup"><span data-stu-id="047e1-134">Position</span></span>

<span data-ttu-id="047e1-135">Les boîtes de dialogue de réunion sont alignées au centre de l’étape de réunion.</span><span class="sxs-lookup"><span data-stu-id="047e1-135">In-meeting dialogs are aligned in the center of the meeting stage.</span></span> <span data-ttu-id="047e1-136">Elles ne peuvent pas être déplacées et ne fonctionnent pas dans l’infrastructure des notifications au niveau du système de teams.</span><span class="sxs-lookup"><span data-stu-id="047e1-136">They can’t be dragged and work within the framework of Teams system-level notifications.</span></span>

:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-dialog-position.png" alt-text="Illustration illustrant l’anatomie de l’interface utilisateur d’une boîte de dialogue de réunion." border="false":::

### <a name="aggregation"></a><span data-ttu-id="047e1-138">Aggregat</span><span class="sxs-lookup"><span data-stu-id="047e1-138">Aggregation</span></span>

<span data-ttu-id="047e1-139">Une seule boîte de dialogue s’affiche à la fois, en empileant le classement du dernier au plus récent en bas.</span><span class="sxs-lookup"><span data-stu-id="047e1-139">Only one dialog displays at a time, stack ranking from last to most recent sent to the bottom.</span></span> <span data-ttu-id="047e1-140">Une fois qu’une boîte de dialogue est résolue ou fermée, le suivant prend sa place.</span><span class="sxs-lookup"><span data-stu-id="047e1-140">Once a dialog is resolved or dismissed, the next one take its place.</span></span>

<span data-ttu-id="047e1-141"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Voir un exemple (Figma)</a></span><span class="sxs-lookup"><span data-stu-id="047e1-141"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">See an example (Figma)</a></span></span>

### <a name="scrolling"></a><span data-ttu-id="047e1-142">Défilement</span><span class="sxs-lookup"><span data-stu-id="047e1-142">Scrolling</span></span>

<span data-ttu-id="047e1-143">Le défilement se produit dans la partie WebView d’une boîte de dialogue de réunion.</span><span class="sxs-lookup"><span data-stu-id="047e1-143">Scrolling occurs in the webview portion of an in-meeting dialog.</span></span> <span data-ttu-id="047e1-144">Souvenez-vous des éléments suivants à propos du défilement :</span><span class="sxs-lookup"><span data-stu-id="047e1-144">Remember the following about scrolling:</span></span>

* <span data-ttu-id="047e1-145">Vous devez uniquement pouvoir faire défiler verticalement.</span><span class="sxs-lookup"><span data-stu-id="047e1-145">You should only be able to scroll vertically.</span></span>
* <span data-ttu-id="047e1-146">Vous ne pouvez voir que le contenu auquel vous avez fait défiler (rien au-dessus ou en dessous).</span><span class="sxs-lookup"><span data-stu-id="047e1-146">You can only see the content you've scrolled to (nothing above or below).</span></span>

:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-dialog-scroll.png" alt-text="Illustration illustrant le mode de défilement du contenu WebView dans la boîte de dialogue de réunion." border="false":::

### <a name="buttons"></a><span data-ttu-id="047e1-148">Boutons</span><span class="sxs-lookup"><span data-stu-id="047e1-148">Buttons</span></span>

<span data-ttu-id="047e1-149">Les boutons de boîte de dialogue de réunion font partie du WebView ([voir quelques exemples](#best-practices)).</span><span class="sxs-lookup"><span data-stu-id="047e1-149">In-meeting dialog buttons are part of the webview ([see some examples](#best-practices)).</span></span>

<span data-ttu-id="047e1-150">Contrairement aux composants similaires, les boîtes de dialogue de réunion sont rejetées lorsqu’un utilisateur sélectionne un bouton.</span><span class="sxs-lookup"><span data-stu-id="047e1-150">Unlike similar components, in-meeting dialogs are dismissed once a user selects a button.</span></span>

## <a name="components"></a><span data-ttu-id="047e1-151">Composants</span><span class="sxs-lookup"><span data-stu-id="047e1-151">Components</span></span>

<span data-ttu-id="047e1-152">Les boîtes de dialogue de réunion sont créées principalement avec les <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">composants d’interface utilisateur suivants (Figma)</a>, qui sont basés sur le <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">système de conception Fluent</a>.</span><span class="sxs-lookup"><span data-stu-id="047e1-152">In-meeting dialogs are built primarily with the following <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">UI components (Figma)</a>, which are based on the <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">Fluent Design System</a>.</span></span>

<span data-ttu-id="047e1-153">Composant</span><span class="sxs-lookup"><span data-stu-id="047e1-153">Component</span></span> | <span data-ttu-id="047e1-154">Conseils</span><span class="sxs-lookup"><span data-stu-id="047e1-154">Guidelines</span></span> | <span data-ttu-id="047e1-155">Exemple</span><span class="sxs-lookup"><span data-stu-id="047e1-155">Example</span></span>
 - | - | -
<span data-ttu-id="047e1-156">Bouton</span><span class="sxs-lookup"><span data-stu-id="047e1-156">Button</span></span> | <span data-ttu-id="047e1-157">Les boutons principal et secondaire peuvent être de taille moyenne ou petite</span><span class="sxs-lookup"><span data-stu-id="047e1-157">Primary and secondary buttons can be medium or small</span></span> | <span data-ttu-id="047e1-158">Envoyer une réponse</span><span class="sxs-lookup"><span data-stu-id="047e1-158">Send a response</span></span>
<span data-ttu-id="047e1-159">Input</span><span class="sxs-lookup"><span data-stu-id="047e1-159">Input</span></span> | <span data-ttu-id="047e1-160">Champ pour une saisie utilisateur partielle.</span><span class="sxs-lookup"><span data-stu-id="047e1-160">Field for brief user input.</span></span> <span data-ttu-id="047e1-161">Le texte de l’étiquette peut inclure une icône</span><span class="sxs-lookup"><span data-stu-id="047e1-161">Label text can include an icon</span></span>  | <span data-ttu-id="047e1-162">Entrer des commentaires</span><span class="sxs-lookup"><span data-stu-id="047e1-162">Enter feedback</span></span>
<span data-ttu-id="047e1-163">Liste déroulante</span><span class="sxs-lookup"><span data-stu-id="047e1-163">Dropdown</span></span> | <span data-ttu-id="047e1-164">Sélectionnez une ou plusieurs options dans une liste.</span><span class="sxs-lookup"><span data-stu-id="047e1-164">Select one or more options from a list.</span></span> <span data-ttu-id="047e1-165">Peut inclure des fonctionnalités de recherche et de sélection multiple</span><span class="sxs-lookup"><span data-stu-id="047e1-165">Can include search and multi-selection features</span></span> | <span data-ttu-id="047e1-166">Choisir une langue</span><span class="sxs-lookup"><span data-stu-id="047e1-166">Choose a language</span></span>
<span data-ttu-id="047e1-167">Contrôles de sélection</span><span class="sxs-lookup"><span data-stu-id="047e1-167">Selection controls</span></span> | <span data-ttu-id="047e1-168">Utilisez des cases à cocher pour plusieurs choix ou cases d’option et pour basculer pour les choix uniques.</span><span class="sxs-lookup"><span data-stu-id="047e1-168">Use checkboxes for multiple choices or radio buttons and toggles for single choices.</span></span> <span data-ttu-id="047e1-169">Pour des sélections plus détaillées, utilisez un curseur</span><span class="sxs-lookup"><span data-stu-id="047e1-169">For more detailed selections, use a slider</span></span> | <span data-ttu-id="047e1-170">Vote dans un sondage</span><span class="sxs-lookup"><span data-stu-id="047e1-170">Vote in a poll</span></span>
<span data-ttu-id="047e1-171">Alertes</span><span class="sxs-lookup"><span data-stu-id="047e1-171">Alerts</span></span> | <span data-ttu-id="047e1-172">Qu’il s’agisse d’un message urgent, d’un état d’erreur ou d’un avertissement, le message doit être court et n’interrompra pas la tâche actuelle de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="047e1-172">Whether displaying an urgent message, error state, or warning, the message should be short and won't interrupt the user's current task</span></span> | <span data-ttu-id="047e1-173">Afficher un problème lors de l’envoi d’une réponse</span><span class="sxs-lookup"><span data-stu-id="047e1-173">Display issue when submitting a response</span></span>

## <a name="theming"></a><span data-ttu-id="047e1-174">Thèmes</span><span class="sxs-lookup"><span data-stu-id="047e1-174">Theming</span></span>

### <a name="colors"></a><span data-ttu-id="047e1-175">Couleurs</span><span class="sxs-lookup"><span data-stu-id="047e1-175">Colors</span></span>

<span data-ttu-id="047e1-176">Utilisez le <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">jeu de couleurs recommandé (Figma)</a> pour les arrière-plans, les avant-plans et les États de transport.</span><span class="sxs-lookup"><span data-stu-id="047e1-176">Use the <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">recommended color scheme (Figma)</a> for backgrounds, foregrounds, and conveying states.</span></span>

### <a name="typography"></a><span data-ttu-id="047e1-177">Typographie</span><span class="sxs-lookup"><span data-stu-id="047e1-177">Typography</span></span>

<span data-ttu-id="047e1-178">Utilisez les <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">tailles et épaisseurs de police recommandées (Figma)</a> pour les titres, le corps de texte et le texte de métadonnées.</span><span class="sxs-lookup"><span data-stu-id="047e1-178">Use the <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">recommended font sizes and weights (Figma)</a> for titles, body text, and metadata text.</span></span>

## <a name="best-practices"></a><span data-ttu-id="047e1-179">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="047e1-179">Best practices</span></span>

<span data-ttu-id="047e1-180">Tandis que les boîtes de dialogue de réunion peuvent faire des appels plus efficaces, ils peuvent également dérailiser les appels s’ils sont trop discrets.</span><span class="sxs-lookup"><span data-stu-id="047e1-180">While in-meeting dialogs can make calls more effective, they also can derail calls if too obtrusive.</span></span> <span data-ttu-id="047e1-181">En règle générale, utilisez les boîtes de dialogue avec parcimonie et suivez ces meilleures pratiques.</span><span class="sxs-lookup"><span data-stu-id="047e1-181">In general, use the dialogs sparingly and follow these best practices.</span></span>

### <a name="navigation"></a><span data-ttu-id="047e1-182">Navigation</span><span class="sxs-lookup"><span data-stu-id="047e1-182">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-dialog-steps-do.png" alt-text="Illustration montrant comment limiter le contenu d’une boîte de dialogue dans un seul écran afin que les utilisateurs puissent se concentrer sur la réunion." border="false":::

#### <a name="do-keep-it-contained"></a><span data-ttu-id="047e1-184">Do : conservez-le</span><span class="sxs-lookup"><span data-stu-id="047e1-184">Do: Keep it contained</span></span>

<span data-ttu-id="047e1-185">Limitez le contenu de la boîte de dialogue de réunion à un seul écran pour permettre aux utilisateurs de se concentrer sur la réunion.</span><span class="sxs-lookup"><span data-stu-id="047e1-185">Limit in-meeting dialog content to a single screen so users can focus on the meeting.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-dialog-steps-dont.png" alt-text="Illustration illustrant la façon dont les boîtes de dialogue de réunion ne doivent pas obliger les utilisateurs à naviguer dans le contenu." border="false":::

#### <a name="dont-include-multiple-steps"></a><span data-ttu-id="047e1-187">Ne pas inclure plusieurs étapes</span><span class="sxs-lookup"><span data-stu-id="047e1-187">Don't: Include multiple steps</span></span>

<span data-ttu-id="047e1-188">Les boîtes de dialogue de réunion ne doivent pas obliger les utilisateurs à naviguer dans le contenu.</span><span class="sxs-lookup"><span data-stu-id="047e1-188">In-meeting dialogs shouldn't require users to navigate through content.</span></span>

   :::column-end:::
:::row-end:::

### <a name="interactions"></a><span data-ttu-id="047e1-189">Leurs</span><span class="sxs-lookup"><span data-stu-id="047e1-189">Interactions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-dialog-interactions-do.png" alt-text="Illustration montrant pourquoi vous devez supprimer le contenu inutile qui ne permet pas aux utilisateurs d’effectuer une tâche rapidement." border="false":::

   :::column-end:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-dialog-interactions-dont.png" alt-text="Une autre illustration illustrant la raison pour laquelle vous devez supprimer le contenu inutile qui ne permet pas aux utilisateurs d’effectuer des choses rapidement." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-dialog-tab-do.png" alt-text="Illustration montrant que, si vous avez besoin d’interactions complexes, il est recommandé d’utiliser à la place une seule colonne dans le volet droit de la réunion." border="false":::

#### <a name="do-limit-number-of-interactions"></a><span data-ttu-id="047e1-193">Do : limiter le nombre d’interactions</span><span class="sxs-lookup"><span data-stu-id="047e1-193">Do: Limit number of interactions</span></span>

<span data-ttu-id="047e1-194">Supprimer le contenu inutile qui ne permet pas aux utilisateurs d’effectuer une tâche rapidement.</span><span class="sxs-lookup"><span data-stu-id="047e1-194">Remove unnecessary content that doesn't help users accomplish something quickly.</span></span> <span data-ttu-id="047e1-195">Si vous avez besoin d’interactions complexes, nous vous recommandons vivement d’afficher votre contenu à l’aide d’une seule colonne sous l’onglet dans la réunion.</span><span class="sxs-lookup"><span data-stu-id="047e1-195">If you need complex interactions, we strongly recommend displaying your content using a single column on the in-meeting tab instead.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-dialog-tab-dont.png" alt-text="Illustration montrant qu’un trop grand nombre d’interactions dans la boîte de dialogue de réunion est gênant de la réunion." border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a><span data-ttu-id="047e1-197">Ne pas faire : introduire des éléments inutiles</span><span class="sxs-lookup"><span data-stu-id="047e1-197">Don't: Introduce unnecessary elements</span></span>

<span data-ttu-id="047e1-198">Il se peut que vous puissiez concevoir une seule boîte de dialogue de réunion avec plusieurs interactions, mais trop nombreuses peuvent gêner la réunion.</span><span class="sxs-lookup"><span data-stu-id="047e1-198">You may be able to design a single in-meeting dialog with multiple interactions, but too many can distract from the meeting.</span></span>

   :::column-end:::
:::row-end:::

### <a name="layout"></a><span data-ttu-id="047e1-199">Disposition</span><span class="sxs-lookup"><span data-stu-id="047e1-199">Layout</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-dialog-layout-do.png" alt-text="Illustration d’une disposition idéale pour les boîtes de dialogue de réunion." border="false":::

#### <a name="do-use-single-column-layouts"></a><span data-ttu-id="047e1-201">Do : utiliser des mises en page à une seule colonne</span><span class="sxs-lookup"><span data-stu-id="047e1-201">Do: Use single-column layouts</span></span>

<span data-ttu-id="047e1-202">Étant donné que les boîtes de dialogue sont au centre de l’étape de la réunion, l’exécution de la tâche doit être rapide et simple pour éviter toute frustration des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="047e1-202">Since the dialogs are at the center of the meeting stage, task completion should be fast and simple to avoid user frustration.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-dialog-layout-dont.png" alt-text="Illustration montrant la disposition des boîtes de dialogue de réunion qui ne sont pas recommandées." border="false":::

#### <a name="dont-clutter-the-space"></a><span data-ttu-id="047e1-204">Ne pas : emcombrer l’espace</span><span class="sxs-lookup"><span data-stu-id="047e1-204">Don't: Clutter the space</span></span>

<span data-ttu-id="047e1-205">Le contenu dense ou très structuré peut être gênant et écrasant, en particulier lors d’une réunion.</span><span class="sxs-lookup"><span data-stu-id="047e1-205">Dense or overly structured content can be distracting and overwhelming, especially during a meeting.</span></span>

   :::column-end:::
:::row-end:::

### <a name="size"></a><span data-ttu-id="047e1-206">Size</span><span class="sxs-lookup"><span data-stu-id="047e1-206">Size</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-dialog-size-do.png" alt-text="Illustration illustrant la manière dont la taille de la boîte de dialogue de réunion doit toujours être la même." border="false":::

#### <a name="do-keep-it-consistent"></a><span data-ttu-id="047e1-208">Do : conservez la cohérence</span><span class="sxs-lookup"><span data-stu-id="047e1-208">Do: Keep it consistent</span></span>

<span data-ttu-id="047e1-209">Ceci est important, car les boîtes de dialogue de réunion s’affichent toujours au même endroit.</span><span class="sxs-lookup"><span data-stu-id="047e1-209">This is important because in-meeting dialogs always display in the same location.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-dialog-size-dont.png" alt-text="Illustration montrant comment vous ne devez pas utiliser différentes tailles de boîte de dialogue." border="false":::

#### <a name="dont-always-fit-to-the-content"></a><span data-ttu-id="047e1-211">Ne pas : toujours tenir dans le contenu</span><span class="sxs-lookup"><span data-stu-id="047e1-211">Don't: Always fit to the content</span></span>

<span data-ttu-id="047e1-212">Il est possible que vous essayiez d’éviter le défilement horizontal, mais que plusieurs tailles de boîte de dialogue de réunion dans la même application constituent une expérience incohérente.</span><span class="sxs-lookup"><span data-stu-id="047e1-212">You may be trying to avoid horizontal scrolling, but multiple in-meeting dialog sizes within the same app is an inconsistent experience.</span></span>

   :::column-end:::
:::row-end:::

### <a name="controls"></a><span data-ttu-id="047e1-213">Contrôles</span><span class="sxs-lookup"><span data-stu-id="047e1-213">Controls</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-dialog-controls-do.png" alt-text="Illustration montrant où placer les boutons dans la boîte de dialogue de réunion." border="false":::

#### <a name="do-right-align-the-primary-action"></a><span data-ttu-id="047e1-215">Do : aligner à droite l’action principale</span><span class="sxs-lookup"><span data-stu-id="047e1-215">Do: Right align the primary action</span></span>

<span data-ttu-id="047e1-216">Nous vous recommandons de placer l’action la plus intense à l’emplacement le plus à droite.</span><span class="sxs-lookup"><span data-stu-id="047e1-216">We recommend positioning the most visually heavy action to the right-most location.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../assets/images/calls-and-meetings/in-meeting-dialog-controls-dont.png" alt-text="Illustration montrant où placer les boutons dans la boîte de dialogue de réunion." border="false":::

#### <a name="dont-left-or-center-align-actions"></a><span data-ttu-id="047e1-218">Ne pas : Left ou Center align actions</span><span class="sxs-lookup"><span data-stu-id="047e1-218">Don't: Left or center align actions</span></span>

<span data-ttu-id="047e1-219">Cela diffère du modèle standard teams pour le positionnement du contrôle dans une boîte de dialogue et peut entrer en conflit avec une boîte de dialogue située en arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="047e1-219">This deviates from the standard Teams pattern for control placement in a dialog and may conflict with a dialog behind the top one.</span></span>

   :::column-end:::
:::row-end:::

## <a name="accessibility"></a><span data-ttu-id="047e1-220">Accessibilité</span><span class="sxs-lookup"><span data-stu-id="047e1-220">Accessibility</span></span>

<span data-ttu-id="047e1-221">Pour plus d’informations sur l’accessibilité, voir <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Figma</a>.</span><span class="sxs-lookup"><span data-stu-id="047e1-221">For information on accessibility, see <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Figma</a>.</span></span>

## <a name="resources"></a><span data-ttu-id="047e1-222">Ressources</span><span class="sxs-lookup"><span data-stu-id="047e1-222">Resources</span></span>

* <span data-ttu-id="047e1-223"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Fichiers Figma des extensions de réunion Microsoft teams</a></span><span class="sxs-lookup"><span data-stu-id="047e1-223"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Microsoft Teams meeting extensions Figma file</a></span></span>

## <a name="validate-your-design"></a><span data-ttu-id="047e1-224">Valider votre conception</span><span class="sxs-lookup"><span data-stu-id="047e1-224">Validate your design</span></span>

<span data-ttu-id="047e1-225">Si vous envisagez de publier votre application dans AppSource, vous devez comprendre les problèmes de conception qui entraînent généralement l’échec des applications lors de l’envoi.</span><span class="sxs-lookup"><span data-stu-id="047e1-225">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="047e1-226">Vérifier les instructions de validation de la conception</span><span class="sxs-lookup"><span data-stu-id="047e1-226">Check design validation guidelines</span></span>](../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines)
