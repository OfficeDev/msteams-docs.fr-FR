---
title: Instructions de conception pour les onglets
description: Décrit les instructions pour la création d’onglets pour le contenu et la collaboration
keywords: instructions de conception teams-onglets de l’infrastructure de référence
ms.openlocfilehash: 2d4e809e3ac11a5742113bf65125848a922c0207
ms.sourcegitcommit: 50571f5c6afc86177c4fe1032fe13366a7b706dd
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/04/2020
ms.locfileid: "49576861"
---
# <a name="content-and-conversations-all-at-once-using-tabs"></a><span data-ttu-id="39bc3-104">Contenu et conversations, tous à la fois à l’aide d’onglets</span><span class="sxs-lookup"><span data-stu-id="39bc3-104">Content and conversations, all at once using tabs</span></span>

> [!Important]
> <span data-ttu-id="39bc3-105">**Onglets sur les clients mobiles**</span><span class="sxs-lookup"><span data-stu-id="39bc3-105">**Tabs on Mobile Clients**</span></span>
>
> <span data-ttu-id="39bc3-106">Suivez les [instructions pour les onglets sur mobile](./tabs-mobile.md) lors de la création de vos onglets.</span><span class="sxs-lookup"><span data-stu-id="39bc3-106">Follow the [guidance for tabs on mobile](./tabs-mobile.md) when creating your tabs.</span></span> <span data-ttu-id="39bc3-107">Si votre onglet utilise l’authentification, vous devez mettre à niveau votre SDK teams JavaScript vers la version 1.4.1 ou une version ultérieure, sinon l’authentification échouera.</span><span class="sxs-lookup"><span data-stu-id="39bc3-107">If your tab uses authentication, you must upgrade your Teams JavaScript SDK to version 1.4.1 or later, or authentication will fail.</span></span>
>
> <span data-ttu-id="39bc3-108">**Onglets canal/groupe (configurable) sur mobile :**</span><span class="sxs-lookup"><span data-stu-id="39bc3-108">**Channel/group (configurable) tabs on mobile:**</span></span>
>
> * <span data-ttu-id="39bc3-109">Les clients mobiles affichent uniquement les onglets configurables dont la valeur est `websiteUrl` .</span><span class="sxs-lookup"><span data-stu-id="39bc3-109">Mobile clients only show configurable tabs that have a value for `websiteUrl`.</span></span> <span data-ttu-id="39bc3-110">Si vous souhaitez que votre onglet apparaisse sur les clients mobiles Teams, vous devez définir la valeur de `websiteUrl` .</span><span class="sxs-lookup"><span data-stu-id="39bc3-110">If you want your tab to appear on the Teams mobile clients, you must set the value of `websiteUrl`.</span></span>
> * <span data-ttu-id="39bc3-111">Le comportement d’ouverture par défaut sur mobile consiste à ouvrir l’extérieur dans le navigateur à l’aide du `websiteUrl` .</span><span class="sxs-lookup"><span data-stu-id="39bc3-111">Default open behavior on mobile is to open outside in browser using the `websiteUrl`.</span></span> <span data-ttu-id="39bc3-112">Pour les applications publiées dans le magasin d’applications public, si vous voulez que les onglets de votre canal s’ouvrent dans teams par défaut, suivez les [instructions pour les onglets sur les appareils mobiles](~/tabs/design/tabs-mobile.md)et contactez votre représentant du support technique pour demander à être inclus dans la liste d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="39bc3-112">For apps published to the public App Store, if you want your channel tab to open inside teams by default, follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md), and reach out to your support rep to request to be whitelisted.</span></span>

<span data-ttu-id="39bc3-113">Les onglets sont des canevas que vous pouvez utiliser pour partager du contenu, organiser des conversations et héberger des services tiers dans le flux de travail Organic d’une équipe.</span><span class="sxs-lookup"><span data-stu-id="39bc3-113">Tabs are canvases that you can use to share content, hold conversations, and host third-party services, all within a team’s organic workflow.</span></span> <span data-ttu-id="39bc3-114">Lorsque vous créez un onglet dans Microsoft Teams, il place le centre et le centre de votre application Web où il est facilement accessible à partir des conversations clés.</span><span class="sxs-lookup"><span data-stu-id="39bc3-114">When you build a tab in Microsoft Teams, it puts your web app front and center where it’s easily accessible from key conversations.</span></span>

## <a name="guidelines"></a><span data-ttu-id="39bc3-115">Conseils</span><span class="sxs-lookup"><span data-stu-id="39bc3-115">Guidelines</span></span>

<span data-ttu-id="39bc3-116">Un onglet approprié doit présenter les caractéristiques suivantes :</span><span class="sxs-lookup"><span data-stu-id="39bc3-116">A good tab should display the following characteristics:</span></span>

### <a name="focused-functionality"></a><span data-ttu-id="39bc3-117">Fonctionnalités ciblées</span><span class="sxs-lookup"><span data-stu-id="39bc3-117">Focused functionality</span></span>

<span data-ttu-id="39bc3-118">Les onglets fonctionnent mieux lorsqu’ils sont conçus pour répondre à un besoin spécifique.</span><span class="sxs-lookup"><span data-stu-id="39bc3-118">Tabs work best when they’re built to address a specific need.</span></span> <span data-ttu-id="39bc3-119">Concentrez-vous sur un petit ensemble de tâches ou sur un sous-ensemble de données correspondant au canal dans lequel se trouve l’onglet.</span><span class="sxs-lookup"><span data-stu-id="39bc3-119">Focus on a small set of tasks or a subset of data that’s relevant to the channel the tab is in.</span></span>

### <a name="reduced-chrome"></a><span data-ttu-id="39bc3-120">Chrome réduit</span><span class="sxs-lookup"><span data-stu-id="39bc3-120">Reduced chrome</span></span>

<span data-ttu-id="39bc3-121">Évitez de créer plusieurs panneaux au sein d’un même onglet, d’y ajouter des couches de navigation ou d’obliger les utilisateurs à faire défiler son contenu verticalement et horizontalement. En d’autres termes, essayez de ne pas avoir d’onglets dans votre onglet.</span><span class="sxs-lookup"><span data-stu-id="39bc3-121">Avoid creating multiple panels in a tab, adding layers of navigation, or requiring users to scroll both vertically and horizontally in one tab. In other words, try not to have tabs in your tab.</span></span>

### <a name="integration"></a><span data-ttu-id="39bc3-122">Intégration</span><span class="sxs-lookup"><span data-stu-id="39bc3-122">Integration</span></span>

<span data-ttu-id="39bc3-123">Découvrez comment informer les utilisateurs de l’activité des onglets en publiant des [cartes adaptatives](../../task-modules-and-cards/what-are-cards.md#adaptive-cards) sur une conversation.</span><span class="sxs-lookup"><span data-stu-id="39bc3-123">Find ways to notify users about tab activity by posting [adaptive cards](../../task-modules-and-cards/what-are-cards.md#adaptive-cards) to a conversation.</span></span>

### <a name="conversational"></a><span data-ttu-id="39bc3-124">Conversationnel</span><span class="sxs-lookup"><span data-stu-id="39bc3-124">Conversational</span></span>

<span data-ttu-id="39bc3-125">Trouver un moyen de faciliter la conversation sur un onglet. Cela garantit que le Centre des conversations est sur le contenu, les données ou le processus à portée de main.</span><span class="sxs-lookup"><span data-stu-id="39bc3-125">Find a way to facilitate conversation around a tab. This ensures that conversations center on the content, data, or process at hand.</span></span>

### <a name="streamlined-access"></a><span data-ttu-id="39bc3-126">Accès simplifié</span><span class="sxs-lookup"><span data-stu-id="39bc3-126">Streamlined access</span></span>

<span data-ttu-id="39bc3-127">Assurez-vous que vous accordez l’accès aux bonnes personnes au bon moment.</span><span class="sxs-lookup"><span data-stu-id="39bc3-127">Make sure you’re granting access to the right people at the right time.</span></span> <span data-ttu-id="39bc3-128">Le simple maintien de votre processus de connexion évite de créer des obstacles à la collaboration et à la collaboration.</span><span class="sxs-lookup"><span data-stu-id="39bc3-128">Keeping your sign-in process simple will avoid creating barriers to contribution and collaboration.</span></span>

### <a name="responsiveness-to-window-sizing"></a><span data-ttu-id="39bc3-129">Réactivité au dimensionnement de la fenêtre</span><span class="sxs-lookup"><span data-stu-id="39bc3-129">Responsiveness to window sizing</span></span>

<span data-ttu-id="39bc3-130">Les équipes peuvent être utilisées dans des tailles de fenêtre aussi petites que 720px, de sorte que l’utilisation d’un onglet dans une petite fenêtre est aussi importante que celle des résolutions très élevées.</span><span class="sxs-lookup"><span data-stu-id="39bc3-130">Teams can be used in window sizes as small as 720px, so making sure that a tab is usable in a small window is just as important as usability at very high resolutions.</span></span>

### <a name="flat-navigation"></a><span data-ttu-id="39bc3-131">Navigation plate</span><span class="sxs-lookup"><span data-stu-id="39bc3-131">Flat navigation</span></span>

<span data-ttu-id="39bc3-132">Nous demandons aux développeurs de ne pas ajouter leur portail entier à un onglet. Le maintien de la navigation relativement plat permet de conserver un modèle de conversation plus simple.</span><span class="sxs-lookup"><span data-stu-id="39bc3-132">We ask developers not to add their entire portal to a tab. Keeping the navigation relatively flat helps maintain a simpler conversational model.</span></span> <span data-ttu-id="39bc3-133">En d’autres termes, la conversation concerne une liste d’éléments, tels que les éléments de travail triage, ou une seule chose, comme une spécification.</span><span class="sxs-lookup"><span data-stu-id="39bc3-133">In other words, the conversation is about a list of things, such as triaged work items, or a single thing, like a spec.</span></span>

<span data-ttu-id="39bc3-134">Il existe des défis de navigation inhérents à la hiérarchie de navigation profonde, dans les conversations thématiques.</span><span class="sxs-lookup"><span data-stu-id="39bc3-134">There are inherent navigational challenges with deep navigation hierarchy, within threaded conversations.</span></span> <span data-ttu-id="39bc3-135">Pour une expérience utilisateur optimale, votre navigation par onglet doit être réduite à un minimum et être conçue comme suit :</span><span class="sxs-lookup"><span data-stu-id="39bc3-135">For the best user experience, your tab navigation should be kept to a minimum and be designed as follows:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="39bc3-136">**Ouvre un module de tâche, tel qu’un élément de travail ou une entité spécifique**.</span><span class="sxs-lookup"><span data-stu-id="39bc3-136">**Opens a task module such as an individual work item or entity**.</span></span> <span data-ttu-id="39bc3-137">Cela exclut la conversation et est la meilleure option pour conserver la conversation en particulier sur l’onglet et non sur les sous-entités ou les expériences de modification.</span><span class="sxs-lookup"><span data-stu-id="39bc3-137">This precludes chat entirely and is the best option to keep chat specifically about the tab and not the sub-entities or editing experiences.</span></span>
>* <span data-ttu-id="39bc3-138">**Ouvre une Pseudo boîte de dialogue dans un IFRAME**.</span><span class="sxs-lookup"><span data-stu-id="39bc3-138">**Opens a pseudo dialog in an iframe**.</span></span> <span data-ttu-id="39bc3-139">Si elle est utilisée avec un arrière-plan filtré, nous vous recommandons d’utiliser la couleur la plus claire plutôt que l’obscurité.</span><span class="sxs-lookup"><span data-stu-id="39bc3-139">If used with a screened background we recommend using the lighter color rather than the dark.</span></span> <span data-ttu-id="39bc3-140">La `app-gray-10 at 30%` transparence fonctionne bien.</span><span class="sxs-lookup"><span data-stu-id="39bc3-140">The `app-gray-10 at 30%` transparency works well.</span></span>
>* <span data-ttu-id="39bc3-141">**Ouvre une page de navigateur**.</span><span class="sxs-lookup"><span data-stu-id="39bc3-141">**Opens a browser page**.</span></span>

### <a name="personality"></a><span data-ttu-id="39bc3-142">Caractéristique</span><span class="sxs-lookup"><span data-stu-id="39bc3-142">Personality</span></span>

<span data-ttu-id="39bc3-143">Votre zone de dessin de tabulation constitue une excellente occasion de personnaliser votre expérience.</span><span class="sxs-lookup"><span data-stu-id="39bc3-143">Your tab canvas presents a great opportunity to brand your experience.</span></span> <span data-ttu-id="39bc3-144">Votre logo est une partie importante de votre identité et de votre connexion avec vos utilisateurs., assurez-vous de l’inclure :</span><span class="sxs-lookup"><span data-stu-id="39bc3-144">Your logo is an important part of your identity and connection with your users., so be sure to include it:</span></span>

> [!div class="checklist"]
>
>* <span data-ttu-id="39bc3-145">Placer votre logo dans le coin gauche ou droit ou le long du bord inférieur</span><span class="sxs-lookup"><span data-stu-id="39bc3-145">Place your logo in the left or right corner or along the bottom edge</span></span>
> * <span data-ttu-id="39bc3-146">Garder votre logo petit et discret</span><span class="sxs-lookup"><span data-stu-id="39bc3-146">Keep your logo small and unobtrusive</span></span>

<span data-ttu-id="39bc3-147">L’incorporation de vos propres couleurs et dispositions twill facilite également la communication de la personnalité.</span><span class="sxs-lookup"><span data-stu-id="39bc3-147">Incorporating your own colors and layouts twill also aid in communicating personality.</span></span>

> [!TIP]
> <span data-ttu-id="39bc3-148">Utilisez notre style visuel pour que votre service ressemble à une partie de teams.</span><span class="sxs-lookup"><span data-stu-id="39bc3-148">Please work with our visual style so your service feels like a part of Teams.</span></span> <span data-ttu-id="39bc3-149">*Voir*, par exemple, les [couleurs de teams](../../concepts/design/components/color.md)</span><span class="sxs-lookup"><span data-stu-id="39bc3-149">*See*, for example [Teams Colors](../../concepts/design/components/color.md)</span></span>

---

## <a name="tab-layouts"></a><span data-ttu-id="39bc3-150">Mises en page d’onglets</span><span class="sxs-lookup"><span data-stu-id="39bc3-150">Tab layouts</span></span>

[!INCLUDE [Tab layouts](../../includes/design/tab-layouts.html)]

---

## <a name="types-of-tabs"></a><span data-ttu-id="39bc3-151">Types d’onglets</span><span class="sxs-lookup"><span data-stu-id="39bc3-151">Types of tabs</span></span>

[!INCLUDE [Tab types](../../includes/design/tab-types.html)]

---

## <a name="configuration-page-height"></a><span data-ttu-id="39bc3-152">Hauteur de la page de configuration</span><span class="sxs-lookup"><span data-stu-id="39bc3-152">Configuration page height</span></span>

>[!IMPORTANT]
><span data-ttu-id="39bc3-153">En septembre 2018, la hauteur de la [page de configuration](~/tabs/how-to/create-tab-pages/configuration-page.md) des onglets a été augmentée, tandis que la largeur est restée inchangée.</span><span class="sxs-lookup"><span data-stu-id="39bc3-153">In September 2018, the height for the tab [configuration page](~/tabs/how-to/create-tab-pages/configuration-page.md) was increased while the width remained unchanged.</span></span> <span data-ttu-id="39bc3-154">Si votre application est conçue pour une taille plus ancienne, votre page de configuration d’onglet aura une grande quantité d’espacement vertical.</span><span class="sxs-lookup"><span data-stu-id="39bc3-154">If your app is designed for the older size your tab configuration page will have a great deal of vertical whitespace.</span></span> <span data-ttu-id="39bc3-155">Les applications de magasin héritées exemptées de cette modification devront contacter Microsoft après la mise à jour pour prendre en compte les nouvelles dimensions.</span><span class="sxs-lookup"><span data-stu-id="39bc3-155">Legacy store apps exempted from this change will need to contact Microsoft after updating to accommodate the new dimensions.</span></span>

<span data-ttu-id="39bc3-156">Les dimensions de la page de configuration de l’onglet :</span><span class="sxs-lookup"><span data-stu-id="39bc3-156">The dimensions of the tab configuration page:</span></span>


<img width="450px" title="Tailles des onglets de configuration" src="~/assets/images/tabs/config-dialog-Contoso2.png" alt="sizes for config tabs" />


### <a name="guidelines-for-tab-configuration-page-format"></a><span data-ttu-id="39bc3-158">Instructions pour le format de page de configuration d’onglet</span><span class="sxs-lookup"><span data-stu-id="39bc3-158">Guidelines for tab configuration page format</span></span>

* <span data-ttu-id="39bc3-159">Basez la hauteur minimale de votre zone de contenu sur la page de configuration de votre onglet sur les éléments graphiques de hauteur fixe.</span><span class="sxs-lookup"><span data-stu-id="39bc3-159">Base the minimum height of your content area of your tab configuration page on fixed-height graphic elements.</span></span>
* <span data-ttu-id="39bc3-160">Calculer l’espacement vertical disponible (hauteur de la zone de contenu dans la page de configuration) à l’aide de `window.innerHeight` .</span><span class="sxs-lookup"><span data-stu-id="39bc3-160">Calculate available vertical space (the height of the content area in the configuration page) using `window.innerHeight`.</span></span> <span data-ttu-id="39bc3-161">Cette valeur renvoie la taille du `<iframe>` dans lequel votre page de configuration se trouve, ce qui peut changer dans les versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="39bc3-161">This returns the size of the `<iframe>` in which your configuration page resides, which may change in future releases.</span></span> <span data-ttu-id="39bc3-162">À l’aide de cette valeur, votre contenu s’ajuste automatiquement aux modifications ultérieures.</span><span class="sxs-lookup"><span data-stu-id="39bc3-162">By using this value your content will adjust automatically to future changes.</span></span>
* <span data-ttu-id="39bc3-163">Allouer de l’espace vertical aux éléments de hauteur variable moins ce qui est nécessaire pour les éléments de hauteur fixe.</span><span class="sxs-lookup"><span data-stu-id="39bc3-163">Allocate vertical space to the variable-height elements minus what's needed for the fixed-height elements.</span></span>
* <span data-ttu-id="39bc3-164">Pour l’état de *connexion* , centrez verticalement et horizontalement le contenu.</span><span class="sxs-lookup"><span data-stu-id="39bc3-164">For the *login* state, vertically and horizontally center the content.</span></span>
* <span data-ttu-id="39bc3-165">Si vous souhaitez une image d’arrière-plan, vous avez besoin d’une nouvelle image ajustée pour s’adapter à la zone (par défaut) ou vous pouvez conserver la même image et choisir entre :</span><span class="sxs-lookup"><span data-stu-id="39bc3-165">If you want a background image, you need either a new image, sized to fit the area (preferred), or you can keep the same image and choose between:</span></span>
  * <span data-ttu-id="39bc3-166">alignement sur le coin supérieur gauche.</span><span class="sxs-lookup"><span data-stu-id="39bc3-166">aligning to the upper left hand corner.</span></span>
  * <span data-ttu-id="39bc3-167">mise à l’échelle de l’image pour l’ajuster.</span><span class="sxs-lookup"><span data-stu-id="39bc3-167">scaling the image to fit.</span></span>

<span data-ttu-id="39bc3-168">Lorsque la taille est correcte, votre page de configuration d’onglet doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="39bc3-168">When properly sized, your tab configuration page should look similar to this:</span></span>

<img width="450px" title="Onglet nouvelle configuration" src="~/assets/images/tabs/config-dialog-Contoso.png" alt="new config tab"/>

## <a name="best-practices"></a><span data-ttu-id="39bc3-170">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="39bc3-170">Best practices</span></span>

### <a name="always-include-a-default-state"></a><span data-ttu-id="39bc3-171">Toujours inclure un État par défaut</span><span class="sxs-lookup"><span data-stu-id="39bc3-171">Always include a default state</span></span>

<span data-ttu-id="39bc3-172">Incluez un État par défaut pour faciliter la configuration des onglets, même si votre onglet est configurable.</span><span class="sxs-lookup"><span data-stu-id="39bc3-172">Include a default state to make tabs easy to set up even if your tab is configurable.</span></span>

### <a name="deep-linking"></a><span data-ttu-id="39bc3-173">Liaison profonde</span><span class="sxs-lookup"><span data-stu-id="39bc3-173">Deep linking</span></span>

<span data-ttu-id="39bc3-174">Chaque fois que possible, les cartes et les robots doivent créer des liens approfondis vers des données plus riches dans un onglet hébergé. Par exemple, une carte peut afficher un résumé des données de bogue, mais vous pouvez cliquer dessus pour afficher l’intégralité du bogue dans un onglet.</span><span class="sxs-lookup"><span data-stu-id="39bc3-174">Whenever possible, cards and bots should deep link to richer data in a hosted tab. For example, a card may show a summary of bug data, but clicking it can shows the entire bug in a tab.</span></span>

### <a name="naming"></a><span data-ttu-id="39bc3-175">Donnant</span><span class="sxs-lookup"><span data-stu-id="39bc3-175">Naming</span></span>

<span data-ttu-id="39bc3-176">Dans de nombreux cas, le nom de votre application fera un excellent nom d’onglet.</span><span class="sxs-lookup"><span data-stu-id="39bc3-176">In many cases, the name of your app will make a great tab name.</span></span> <span data-ttu-id="39bc3-177">Toutefois, vous pouvez également nommer vos onglets en fonction de la fonctionnalité qu’ils fournissent.</span><span class="sxs-lookup"><span data-stu-id="39bc3-177">But, also consider naming your tabs according to the functionality they provide.</span></span>

### <a name="multi-window"></a><span data-ttu-id="39bc3-178">Multi-fenêtre</span><span class="sxs-lookup"><span data-stu-id="39bc3-178">Multi-window</span></span>

<span data-ttu-id="39bc3-179">Les onglets de canal dotés de fonctionnalités d’édition complexes doivent ouvrir le mode éditeur dans plusieurs fenêtres plutôt qu’un onglet.</span><span class="sxs-lookup"><span data-stu-id="39bc3-179">Channel tabs that have complex editing capabilities must open the editor view in multi-window rather than a tab.</span></span>

### <a name="no-horizontal-scrolling"></a><span data-ttu-id="39bc3-180">Pas de défilement horizontal</span><span class="sxs-lookup"><span data-stu-id="39bc3-180">No horizontal scrolling</span></span>

<span data-ttu-id="39bc3-181">La tabulation ne doit pas avoir de défilement horizontal.</span><span class="sxs-lookup"><span data-stu-id="39bc3-181">Tab should not have horizontal scrolling.</span></span>

### <a name="easy-navigation"></a><span data-ttu-id="39bc3-182">Navigation facile</span><span class="sxs-lookup"><span data-stu-id="39bc3-182">Easy navigation</span></span>

<span data-ttu-id="39bc3-183">La navigation à l’intérieur d’une application d’onglets doit être facile à suivre, c’est-à-dire, lorsque cela est nécessaire/applicable, les pages suivantes :</span><span class="sxs-lookup"><span data-stu-id="39bc3-183">Navigation inside a tab app must be easy to follow i.e. pages have the following where necessary/applicable:</span></span>
* <span data-ttu-id="39bc3-184">Boutons précédent</span><span class="sxs-lookup"><span data-stu-id="39bc3-184">Back buttons</span></span>
* <span data-ttu-id="39bc3-185">En-têtes de page</span><span class="sxs-lookup"><span data-stu-id="39bc3-185">Page headers</span></span>
* <span data-ttu-id="39bc3-186">Barres</span><span class="sxs-lookup"><span data-stu-id="39bc3-186">Breadcrumbs</span></span>
* <span data-ttu-id="39bc3-187">Menus de hamburger</span><span class="sxs-lookup"><span data-stu-id="39bc3-187">Hamburger menus</span></span>

### <a name="undo-last-action"></a><span data-ttu-id="39bc3-188">Annuler la dernière action</span><span class="sxs-lookup"><span data-stu-id="39bc3-188">Undo last action</span></span>

<span data-ttu-id="39bc3-189">L’utilisateur doit pouvoir annuler sa dernière action dans l’application.</span><span class="sxs-lookup"><span data-stu-id="39bc3-189">User must be able to undo their last action in the app.</span></span>

### <a name="share-content"></a><span data-ttu-id="39bc3-190">Partager du contenu</span><span class="sxs-lookup"><span data-stu-id="39bc3-190">Share content</span></span>

<span data-ttu-id="39bc3-191">Les applications personnelles doivent permettre aux utilisateurs de partager du contenu d’une expérience d’application personnelle avec d’autres membres de l’équipe.</span><span class="sxs-lookup"><span data-stu-id="39bc3-191">Personal apps should enable users to share content from a personal app experience with other team members.</span></span> <span data-ttu-id="39bc3-192">L’onglet canal doit fournir une navigation qui complète la navigation principale dans Teams, au lieu d’entrer en conflit avec elle (par exemple, les barres de navigation du rail gauche).</span><span class="sxs-lookup"><span data-stu-id="39bc3-192">Channel tab must provide navigation that complements the main Teams navigation, rather than conflicting with it (such as left rail nav-bars).</span></span>

### <a name="single-view"></a><span data-ttu-id="39bc3-193">Vue unique</span><span class="sxs-lookup"><span data-stu-id="39bc3-193">Single view</span></span>

<span data-ttu-id="39bc3-194">Les applications personnelles doivent présenter du contenu provenant d’instances ou d’instances d’étendue de conversation de groupe de cette application dans une seule vue, par exemple, un utilisateur Trello doit être en mesure d’afficher toutes les instances des cartes Trello auxquelles elles participent au niveau de l’équipe dans leur application personnelle.</span><span class="sxs-lookup"><span data-stu-id="39bc3-194">Personal apps should present content from team or group chat scoped instances of that app in a single view, e.g., a Trello user should be able to see all instances of Trello boards they participate in at a team level in their personal app.</span></span>

### <a name="no-app-bar"></a><span data-ttu-id="39bc3-195">Aucune barre d’application</span><span class="sxs-lookup"><span data-stu-id="39bc3-195">No app bar</span></span>

<span data-ttu-id="39bc3-196">Les onglets ne doivent pas fournir de barre d’application avec des icônes dans le rail gauche qui entrent en conflit avec la navigation principale de teams.</span><span class="sxs-lookup"><span data-stu-id="39bc3-196">Tabs should not provide an app bar with icons in the left rail that conflicts with the main Teams navigation.</span></span>

### <a name="navigation"></a><span data-ttu-id="39bc3-197">Navigation</span><span class="sxs-lookup"><span data-stu-id="39bc3-197">Navigation</span></span>

<span data-ttu-id="39bc3-198">Les onglets ne doivent pas comporter plus de 3 niveaux de navigation au sein de l’application.</span><span class="sxs-lookup"><span data-stu-id="39bc3-198">Tabs should not have more than 3 levels of navigation within the app.</span></span>

### <a name="l2l3-view"></a><span data-ttu-id="39bc3-199">Vue L2/L3</span><span class="sxs-lookup"><span data-stu-id="39bc3-199">L2/L3 view</span></span>

<span data-ttu-id="39bc3-200">Les pages secondaires et tertiaires d’un onglet doivent être ouvertes dans une vue L2/L3 dans la zone d’onglet principale qui est parcourue via le plan de navigation.</span><span class="sxs-lookup"><span data-stu-id="39bc3-200">Secondary and tertiary pages in a tab should be opened in an L2/L3 view in the main tab area that is navigated via the breadcrumb.</span></span>

### <a name="no-link-to-external-browser"></a><span data-ttu-id="39bc3-201">Aucun lien vers le navigateur externe</span><span class="sxs-lookup"><span data-stu-id="39bc3-201">No link to external browser</span></span>

<span data-ttu-id="39bc3-202">Les cibles de liens dans les onglets ne doivent pas être liées à un navigateur externe, mais doivent être liées à des éléments div contenus dans Teams.</span><span class="sxs-lookup"><span data-stu-id="39bc3-202">Link targets in tabs should not link to an external browser but should link to div elements contained within Teams.</span></span> <span data-ttu-id="39bc3-203">Par exemple, à l’intérieur des modules de tâches, des onglets, etc.</span><span class="sxs-lookup"><span data-stu-id="39bc3-203">For example, inside task Modules, tabs, etc.</span></span>

## <a name="notifications-for-tabs"></a><span data-ttu-id="39bc3-204">Notifications pour les onglets</span><span class="sxs-lookup"><span data-stu-id="39bc3-204">Notifications for tabs</span></span>

<span data-ttu-id="39bc3-205">Il existe deux modes de notification pour les modifications apportées au contenu des onglets :</span><span class="sxs-lookup"><span data-stu-id="39bc3-205">There are two modes of notification for tab content changes:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="39bc3-206">**Utiliser l’API de l’application pour avertir les utilisateurs des modifications**.</span><span class="sxs-lookup"><span data-stu-id="39bc3-206">**Use the app API to notify users of changes**.</span></span> <span data-ttu-id="39bc3-207">Ce message s’affichera dans le flux d’activités de l’utilisateur et le lien profond vers l’onglet. *voir*  [créer des liens détaillés vers du contenu et des fonctionnalités dans Microsoft teams](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true )</span><span class="sxs-lookup"><span data-stu-id="39bc3-207">This message will show up in the user’s activity feed and deep link to the tab. *See*  [Create deep links to content and features in Microsoft Teams](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true )</span></span>

> * <span data-ttu-id="39bc3-208">**Utiliser un bot**.</span><span class="sxs-lookup"><span data-stu-id="39bc3-208">**Use a bot**.</span></span> <span data-ttu-id="39bc3-209">Cette méthode est préférée en particulier si le thread de tabulation est ciblé.</span><span class="sxs-lookup"><span data-stu-id="39bc3-209">This method is preferred especially if the Tab thread is targeted.</span></span> <span data-ttu-id="39bc3-210">Le résultat est que la conversation de thème de l’onglet est déplacée vers le mode récemment actif.</span><span class="sxs-lookup"><span data-stu-id="39bc3-210">The result will be that the tab’s threaded conversation will be moved into view as recently active.</span></span> <span data-ttu-id="39bc3-211">Cette méthode permet également une sophistication du mode d’envoi de la notification.</span><span class="sxs-lookup"><span data-stu-id="39bc3-211">This method also allows for some sophistication in how the notification is sent.</span></span>

<span data-ttu-id="39bc3-212">L’envoi d’un message à un fil d’onglet augmente la sensibilisation de l’activité à tous les utilisateurs sans en informer explicitement tout le monde.</span><span class="sxs-lookup"><span data-stu-id="39bc3-212">Sending a message to a tab thread increases the awareness of activity to all users without explicitly notifying everyone.</span></span> <span data-ttu-id="39bc3-213">Il s’agit d’une sensibilisation sans bruit.</span><span class="sxs-lookup"><span data-stu-id="39bc3-213">This is awareness without noise.</span></span> <span data-ttu-id="39bc3-214">En outre, lorsque vous avez `@mention`  des utilisateurs spécifiques, la même notification est placée dans le flux, en les liant directement au fil d’onglets.</span><span class="sxs-lookup"><span data-stu-id="39bc3-214">In addition, when you `@mention`  specific users the same notification will be placed in their feed, deep linking them to the tab thread directly.</span></span>

### <a name="tab-design-best-practices"></a><span data-ttu-id="39bc3-215">Meilleures pratiques pour la création d’onglets</span><span class="sxs-lookup"><span data-stu-id="39bc3-215">Tab design best practices</span></span>

* <span data-ttu-id="39bc3-216">Les onglets personnel/statique doivent permettre aux utilisateurs de partager le contenu d’une expérience d’application personnelle avec d’autres membres de l’équipe.</span><span class="sxs-lookup"><span data-stu-id="39bc3-216">Personal/Static tabs should enable users to share content from a personal app experience with another team members.</span></span>
* <span data-ttu-id="39bc3-217">Les onglets personnels/statiques peuvent présenter du contenu provenant d’instances ou d’instances d’étendues de conversation de groupe de cette application dans une seule vue.</span><span class="sxs-lookup"><span data-stu-id="39bc3-217">Personal/Static tabs may present content from team or group chat scoped instances of that app in a single view.</span></span>
* <span data-ttu-id="39bc3-218">Les cibles de liens dans les onglets ne doivent pas être liées à un navigateur externe, mais doivent être liées à des éléments div contenus dans Teams (par exemple, à l’intérieur, des modules de tâches, des onglets, etc.).</span><span class="sxs-lookup"><span data-stu-id="39bc3-218">Link targets in tabs should not link to an external browser but should link to div elements contained within Teams (example-inside, task modules, tabs, etc).</span></span>
* <span data-ttu-id="39bc3-219">Les onglets doivent répondre aux thèmes de l’équipe.</span><span class="sxs-lookup"><span data-stu-id="39bc3-219">Tabs should be responsive to Team’s themes.</span></span> <span data-ttu-id="39bc3-220">Lorsque le thème teams est modifié, le thème au sein de l’application doit également être modifié pour refléter ce thème.</span><span class="sxs-lookup"><span data-stu-id="39bc3-220">When the Teams theme is changed, the theme within the app should also change to reflect that theme.</span></span>
* <span data-ttu-id="39bc3-221">Les onglets doivent utiliser des composants de style teams dans la mesure du possible.</span><span class="sxs-lookup"><span data-stu-id="39bc3-221">Tabs should use Teams-styled components where possible.</span></span> <span data-ttu-id="39bc3-222">Cela signifie adopter des polices Teams, des rampes, des palettes de couleurs, un système de grille, un mouvement, un ton de voix, etc.</span><span class="sxs-lookup"><span data-stu-id="39bc3-222">It means adopting Teams fonts, type ramps, color palettes, grid system, motion, tone of voice, etc.</span></span>
* <span data-ttu-id="39bc3-223">Les onglets doivent utiliser les comportements d’interaction de teams pour la navigation dans la page, la position et l’utilisation des boîtes de dialogue, des hiérarchies d’informations, etc.</span><span class="sxs-lookup"><span data-stu-id="39bc3-223">Tabs should use Teams interaction behaviors for in-page navigation, position, and use of dialogs, information hierarchies, etc.</span></span>
* <span data-ttu-id="39bc3-224">Les onglets doivent utiliser le menu hamburger teams standard et/ou la barre de navigation pour la navigation dans l’application.</span><span class="sxs-lookup"><span data-stu-id="39bc3-224">Tabs should use the standard Teams hamburger menu and/or breadcrumb for in-app navigation.</span></span> <span data-ttu-id="39bc3-225">Les onglets ne doivent pas fournir de barre d’application avec des icônes dans le rail gauche qui entrent en conflit avec la navigation principale de teams.</span><span class="sxs-lookup"><span data-stu-id="39bc3-225">Tabs should not provide an app bar with icons in the left rail that conflicts with the main Teams navigation.</span></span>
* <span data-ttu-id="39bc3-226">Les onglets ne doivent pas avoir plus de trois niveaux de navigation dans l’application.</span><span class="sxs-lookup"><span data-stu-id="39bc3-226">Tabs should not have more than three levels of navigation within the app.</span></span>
* <span data-ttu-id="39bc3-227">Les pages secondaires et tertiaires d’un onglet doivent être ouvertes dans une vue L2/L3 dans la zone d’onglet principale qui est parcourue via le plan de navigation.</span><span class="sxs-lookup"><span data-stu-id="39bc3-227">Secondary and tertiary pages in a tab should be opened in an L2/L3 view in the main tab area that is navigated via the breadcrumb.</span></span>
* <span data-ttu-id="39bc3-228">Les onglets disposant de fonctionnalités d’édition complexes dans l’application doivent ouvrir le mode éditeur dans plusieurs fenêtres plutôt qu’un onglet (pour le bureau et le Web).</span><span class="sxs-lookup"><span data-stu-id="39bc3-228">Tabs that have complex editing capabilities within the app should open the editor view in multi-window rather than a tab (for desktop and web).</span></span>
* <span data-ttu-id="39bc3-229">Pour une expérience utilisateur améliorée, citons un bot personnel qui envoie un message de bienvenue à l’utilisateur lors de la première exécution et répond aux commandes **Hi**, **Help** et **Hello** .</span><span class="sxs-lookup"><span data-stu-id="39bc3-229">For improved user experience include a personal bot that sends a welcome message to the user on the first run and responds to the **hi**, **help**, and **hello** commands.</span></span> <span data-ttu-id="39bc3-230">Vous pouvez vous reporter à la documentation sur les [bots conversation](../../bots/what-are-bots.md#in-a-one-to-one-chat) pour obtenir de l’aide.</span><span class="sxs-lookup"><span data-stu-id="39bc3-230">You can refer to the documentation on [conversational bots](../../bots/what-are-bots.md#in-a-one-to-one-chat) for further assistance.</span></span>
