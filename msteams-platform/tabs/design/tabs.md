---
title: Instructions de conception pour les onglets
description: Décrit les instructions pour la création d’onglets pour le contenu et la collaboration
keywords: instructions de conception de l’infrastructure de référence
ms.openlocfilehash: 342e01e348c74eb143391a7d238396a2d866766a
ms.sourcegitcommit: 61edf47c9dd1dbc1df03d0d9fb83bfedca4c423b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2020
ms.locfileid: "43914552"
---
# <a name="content-and-conversations-all-at-once-using-tabs"></a><span data-ttu-id="4761d-104">Contenu et conversations, tous à la fois à l’aide d’onglets</span><span class="sxs-lookup"><span data-stu-id="4761d-104">Content and conversations, all at once using tabs</span></span>

> [!Important]
> <span data-ttu-id="4761d-105">**Onglets sur les clients mobiles**</span><span class="sxs-lookup"><span data-stu-id="4761d-105">**Tabs on Mobile Clients**</span></span>
>
> <span data-ttu-id="4761d-106">Suivez les [instructions pour les onglets sur mobile](./tabs-mobile.md) lors de la création de vos onglets.</span><span class="sxs-lookup"><span data-stu-id="4761d-106">Follow the [guidance for tabs on mobile](./tabs-mobile.md) when creating your tabs.</span></span> <span data-ttu-id="4761d-107">Si votre onglet utilise l’authentification, vous devez mettre à niveau votre SDK teams JavaScript vers la version 1.4.1 ou une version ultérieure, sinon l’authentification échouera.</span><span class="sxs-lookup"><span data-stu-id="4761d-107">If your tab uses authentication, you must upgrade your Teams JavaScript SDK to version 1.4.1 or later, or authentication will fail.</span></span>
>
> <span data-ttu-id="4761d-108">**Onglets personnels (statiques) sur mobile :**</span><span class="sxs-lookup"><span data-stu-id="4761d-108">**Personal (static) tabs on mobile:**</span></span>
>
> * <span data-ttu-id="4761d-109">Les onglets statiques (application personnelle) sont disponibles dans l’Aperçu pour les [développeurs](~/resources/dev-preview/developer-preview-intro.md).</span><span class="sxs-lookup"><span data-stu-id="4761d-109">Static tabs (personal app) are available in [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
> * <span data-ttu-id="4761d-110">Lors de la création de vos onglets statiques, assurez-vous de suivre les [instructions pour les onglets sur les appareils mobiles](~/tabs/design/tabs-mobile.md)</span><span class="sxs-lookup"><span data-stu-id="4761d-110">While building your static tabs, ensure to follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md)</span></span>
>
> <span data-ttu-id="4761d-111">**Onglets canal/groupe (configurable) sur mobile :**</span><span class="sxs-lookup"><span data-stu-id="4761d-111">**Channel/group (configurable) tabs on mobile:**</span></span>
>
> * <span data-ttu-id="4761d-112">Les clients mobiles affichent uniquement les onglets dont `websiteUrl`la valeur est.</span><span class="sxs-lookup"><span data-stu-id="4761d-112">Mobile clients only show tabs that have a value for `websiteUrl`.</span></span> <span data-ttu-id="4761d-113">Si vous souhaitez que votre onglet apparaisse sur les clients mobiles Teams, vous devez définir la `websiteUrl`valeur de.</span><span class="sxs-lookup"><span data-stu-id="4761d-113">If you want your tab to appear on the Teams mobile clients, you must set the value of `websiteUrl`.</span></span>
> * <span data-ttu-id="4761d-114">Le comportement d’ouverture par défaut sur mobile consiste à ouvrir l’extérieur `websiteUrl`dans le navigateur à l’aide du.</span><span class="sxs-lookup"><span data-stu-id="4761d-114">Default open behavior on mobile is to open outside in browser using the `websiteUrl`.</span></span> <span data-ttu-id="4761d-115">Pour les applications publiées dans le magasin d’applications public, si vous voulez que les onglets de votre canal s’ouvrent dans teams par défaut, suivez les [instructions pour les onglets sur les appareils mobiles](~/tabs/design/tabs-mobile.md)et contactez votre représentant du support technique pour demander à être inclus dans la liste d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="4761d-115">For apps published to the public App Store, if you want your channel tab to open inside teams by default, follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md), and reach out to your support rep to request to be whitelisted.</span></span>

<span data-ttu-id="4761d-116">Les onglets sont des canevas que vous pouvez utiliser pour partager du contenu, organiser des conversations et héberger des services tiers dans le flux de travail Organic d’une équipe.</span><span class="sxs-lookup"><span data-stu-id="4761d-116">Tabs are canvases that you can use to share content, hold conversations, and host third-party services, all within a team’s organic workflow.</span></span> <span data-ttu-id="4761d-117">Lorsque vous créez un onglet dans Microsoft Teams, il place le centre et le centre de votre application Web où il est facilement accessible à partir des conversations clés.</span><span class="sxs-lookup"><span data-stu-id="4761d-117">When you build a tab in Microsoft Teams, it puts your web app front and center where it’s easily accessible from key conversations.</span></span>

## <a name="guidelines"></a><span data-ttu-id="4761d-118">Conseils</span><span class="sxs-lookup"><span data-stu-id="4761d-118">Guidelines</span></span>

<span data-ttu-id="4761d-119">Un onglet approprié doit présenter les caractéristiques suivantes :</span><span class="sxs-lookup"><span data-stu-id="4761d-119">A good tab should display the following characteristics:</span></span>

### <a name="focused-functionality"></a><span data-ttu-id="4761d-120">Fonctionnalités ciblées</span><span class="sxs-lookup"><span data-stu-id="4761d-120">Focused functionality</span></span>

<span data-ttu-id="4761d-121">Les onglets fonctionnent mieux lorsqu’ils sont conçus pour répondre à un besoin spécifique.</span><span class="sxs-lookup"><span data-stu-id="4761d-121">Tabs work best when they’re built to address a specific need.</span></span> <span data-ttu-id="4761d-122">Concentrez-vous sur un petit ensemble de tâches ou sur un sous-ensemble de données correspondant au canal dans lequel se trouve l’onglet.</span><span class="sxs-lookup"><span data-stu-id="4761d-122">Focus on a small set of tasks or a subset of data that’s relevant to the channel the tab is in.</span></span>

### <a name="reduced-chrome"></a><span data-ttu-id="4761d-123">Chrome réduit</span><span class="sxs-lookup"><span data-stu-id="4761d-123">Reduced chrome</span></span>

<span data-ttu-id="4761d-124">Évitez de créer plusieurs panneaux au sein d’un même onglet, d’y ajouter des couches de navigation ou d’obliger les utilisateurs à faire défiler son contenu verticalement et horizontalement. En d’autres termes, essayez de ne pas avoir d’onglets dans votre onglet.</span><span class="sxs-lookup"><span data-stu-id="4761d-124">Avoid creating multiple panels in a tab, adding layers of navigation, or requiring users to scroll both vertically and horizontally in one tab. In other words, try not to have tabs in your tab.</span></span>

### <a name="integration"></a><span data-ttu-id="4761d-125">Intégration</span><span class="sxs-lookup"><span data-stu-id="4761d-125">Integration</span></span>

<span data-ttu-id="4761d-126">Découvrez comment informer les utilisateurs de l’activité des onglets en publiant des [cartes adaptatives](../../task-modules-and-cards/what-are-cards.md#adaptive-cards) sur une conversation.</span><span class="sxs-lookup"><span data-stu-id="4761d-126">Find ways to notify users about tab activity by posting [adaptive cards](../../task-modules-and-cards/what-are-cards.md#adaptive-cards) to a conversation.</span></span>

### <a name="conversational"></a><span data-ttu-id="4761d-127">Conversationnel</span><span class="sxs-lookup"><span data-stu-id="4761d-127">Conversational</span></span>

<span data-ttu-id="4761d-128">Trouver un moyen de faciliter la conversation sur un onglet. Cela garantit que le Centre des conversations est sur le contenu, les données ou le processus à portée de main.</span><span class="sxs-lookup"><span data-stu-id="4761d-128">Find a way to facilitate conversation around a tab. This ensures that conversations center on the content, data, or process at hand.</span></span>

### <a name="streamlined-access"></a><span data-ttu-id="4761d-129">Accès simplifié</span><span class="sxs-lookup"><span data-stu-id="4761d-129">Streamlined access</span></span>

<span data-ttu-id="4761d-130">Assurez-vous que vous accordez l’accès aux bonnes personnes au bon moment.</span><span class="sxs-lookup"><span data-stu-id="4761d-130">Make sure you’re granting access to the right people at the right time.</span></span> <span data-ttu-id="4761d-131">Le simple maintien de votre processus de connexion évite de créer des obstacles à la collaboration et à la collaboration.</span><span class="sxs-lookup"><span data-stu-id="4761d-131">Keeping your sign-in process simple will avoid creating barriers to contribution and collaboration.</span></span>

### <a name="responsiveness-to-window-sizing"></a><span data-ttu-id="4761d-132">Réactivité au dimensionnement de la fenêtre</span><span class="sxs-lookup"><span data-stu-id="4761d-132">Responsiveness to window sizing</span></span>

<span data-ttu-id="4761d-133">Les équipes peuvent être utilisées dans des tailles de fenêtre aussi petites que 720px, de sorte que l’utilisation d’un onglet dans une petite fenêtre est aussi importante que celle des résolutions très élevées.</span><span class="sxs-lookup"><span data-stu-id="4761d-133">Teams can be used in window sizes as small as 720px, so making sure that a tab is usable in a small window is just as important as usability at very high resolutions.</span></span>

### <a name="flat-navigation"></a><span data-ttu-id="4761d-134">Navigation plate</span><span class="sxs-lookup"><span data-stu-id="4761d-134">Flat navigation</span></span>

<span data-ttu-id="4761d-135">Nous demandons aux développeurs de ne pas ajouter l’intégralité de leur portail à un onglet. le maintien de la navigation relativement plat contribue à maintenir un modèle de conversation plus simple.</span><span class="sxs-lookup"><span data-stu-id="4761d-135">We ask developers not to add their entire portal to a tab. Keeping the navigation relatively flat helps maintain a simpler conversational model.</span></span> <span data-ttu-id="4761d-136">En d’autres termes, la conversation concerne une liste d’éléments, tels que les éléments de travail triage, ou une seule chose, comme une spécification.</span><span class="sxs-lookup"><span data-stu-id="4761d-136">In other words, the conversation is about a list of things, such as triaged work items, or a single thing, like a spec.</span></span>

<span data-ttu-id="4761d-137">Il existe des défis de navigation inhérents à la hiérarchie de navigation profonde, dans les conversations thématiques.</span><span class="sxs-lookup"><span data-stu-id="4761d-137">There are inherent navigational challenges with deep navigation hierarchy, within threaded conversations.</span></span> <span data-ttu-id="4761d-138">Pour une expérience utilisateur optimale, votre navigation par onglet doit être réduite à un minimum et être conçue comme suit :</span><span class="sxs-lookup"><span data-stu-id="4761d-138">For the best user experience, your tab navigation should be kept to a minimum and be designed as follows:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="4761d-139">**Ouvre un module de tâche, tel qu’un élément de travail ou une entité spécifique**.</span><span class="sxs-lookup"><span data-stu-id="4761d-139">**Opens a task module such as an individual work item or entity**.</span></span> <span data-ttu-id="4761d-140">Cela exclut la conversation et est la meilleure option pour conserver la conversation en particulier sur l’onglet et non sur les sous-entités ou les expériences de modification.</span><span class="sxs-lookup"><span data-stu-id="4761d-140">This precludes chat entirely and is the best option to keep chat specifically about the tab and not the sub-entities or editing experiences.</span></span>
>* <span data-ttu-id="4761d-141">**Ouvre une Pseudo boîte de dialogue dans un IFRAME**.</span><span class="sxs-lookup"><span data-stu-id="4761d-141">**Opens a pseudo dialog in an iframe**.</span></span> <span data-ttu-id="4761d-142">Si elle est utilisée avec un arrière-plan filtré, nous vous recommandons d’utiliser la couleur la plus claire plutôt que l’obscurité.</span><span class="sxs-lookup"><span data-stu-id="4761d-142">If used with a screened background we recommend using the lighter color rather than the dark.</span></span> <span data-ttu-id="4761d-143">La `app-gray-10 at 30%` transparence fonctionne bien.</span><span class="sxs-lookup"><span data-stu-id="4761d-143">The `app-gray-10 at 30%` transparency works well.</span></span>
>* <span data-ttu-id="4761d-144">**Ouvre une page de navigateur**.</span><span class="sxs-lookup"><span data-stu-id="4761d-144">**Opens a browser page**.</span></span>

### <a name="personality"></a><span data-ttu-id="4761d-145">Caractéristique</span><span class="sxs-lookup"><span data-stu-id="4761d-145">Personality</span></span>

<span data-ttu-id="4761d-146">Votre zone de dessin de tabulation constitue une excellente occasion de personnaliser votre expérience.</span><span class="sxs-lookup"><span data-stu-id="4761d-146">Your tab canvas presents a great opportunity to brand your experience.</span></span> <span data-ttu-id="4761d-147">Votre logo est une partie importante de votre identité et de votre connexion avec vos utilisateurs., assurez-vous de l’inclure :</span><span class="sxs-lookup"><span data-stu-id="4761d-147">Your logo is an important part of your identity and connection with your users., so be sure to include it:</span></span>

> [!div class="checklist"]
>
>* <span data-ttu-id="4761d-148">Placer votre logo dans le coin gauche ou droit ou le long du bord inférieur</span><span class="sxs-lookup"><span data-stu-id="4761d-148">Place your logo in the left or right corner or along the bottom edge</span></span>
> * <span data-ttu-id="4761d-149">Garder votre logo petit et discret</span><span class="sxs-lookup"><span data-stu-id="4761d-149">Keep your logo small and unobtrusive</span></span>

<span data-ttu-id="4761d-150">L’incorporation de vos propres couleurs et dispositions twill facilite également la communication de la personnalité.</span><span class="sxs-lookup"><span data-stu-id="4761d-150">Incorporating your own colors and layouts twill also aid in communicating personality.</span></span>

> [!TIP]
> <span data-ttu-id="4761d-151">Utilisez notre style visuel pour que votre service ressemble à une partie de teams.</span><span class="sxs-lookup"><span data-stu-id="4761d-151">Please work with our visual style so your service feels like a part of Teams.</span></span> <span data-ttu-id="4761d-152">*Voir*, par exemple, [couleurs teams] (/concepts/design/Components/Typography.MD</span><span class="sxs-lookup"><span data-stu-id="4761d-152">*See*, for example [Teams Colors](/concepts/design/components/typography.md</span></span>

---

## <a name="tab-layouts"></a><span data-ttu-id="4761d-153">Mises en page d’onglets</span><span class="sxs-lookup"><span data-stu-id="4761d-153">Tab layouts</span></span>

[!INCLUDE [Tab layouts](../../includes/design/tab-layouts.html)]

---

## <a name="types-of-tabs"></a><span data-ttu-id="4761d-154">Types d’onglets</span><span class="sxs-lookup"><span data-stu-id="4761d-154">Types of tabs</span></span>

[!INCLUDE [Tab types](../../includes/design/tab-types.html)]

---

## <a name="configuration-page-height"></a><span data-ttu-id="4761d-155">Hauteur de la page de configuration</span><span class="sxs-lookup"><span data-stu-id="4761d-155">Configuration page height</span></span>

>[!IMPORTANT]
><span data-ttu-id="4761d-156">En septembre 2018, la hauteur de la [page de configuration](~/tabs/how-to/create-tab-pages/configuration-page.md) des onglets a été augmentée, tandis que la largeur est restée inchangée.</span><span class="sxs-lookup"><span data-stu-id="4761d-156">In September 2018, the height for the tab [configuration page](~/tabs/how-to/create-tab-pages/configuration-page.md) was increased while the width remained unchanged.</span></span> <span data-ttu-id="4761d-157">Si votre application est conçue pour une taille plus ancienne, votre page de configuration d’onglet aura une grande quantité d’espacement vertical.</span><span class="sxs-lookup"><span data-stu-id="4761d-157">If your app is designed for the older size your tab configuration page will have a great deal of vertical whitespace.</span></span> <span data-ttu-id="4761d-158">Les applications de magasin héritées exemptées de cette modification devront contacter Microsoft après la mise à jour pour prendre en compte les nouvelles dimensions.</span><span class="sxs-lookup"><span data-stu-id="4761d-158">Legacy store apps exempted from this change will need to contact Microsoft after updating to accommodate the new dimensions.</span></span>

<span data-ttu-id="4761d-159">Les dimensions de la page de configuration de l’onglet :</span><span class="sxs-lookup"><span data-stu-id="4761d-159">The dimensions of the tab configuration page:</span></span>

<img width="450px" title="Tailles des onglets de configuration" src="~/assets/images/tabs/config-dialog-Contoso2.png" />

### <a name="guidelines-for-tab-configuration-page-format"></a><span data-ttu-id="4761d-161">Instructions pour le format de page de configuration d’onglet</span><span class="sxs-lookup"><span data-stu-id="4761d-161">Guidelines for tab configuration page format</span></span>

* <span data-ttu-id="4761d-162">Basez la hauteur minimale de votre zone de contenu sur la page de configuration de votre onglet sur les éléments graphiques de hauteur fixe.</span><span class="sxs-lookup"><span data-stu-id="4761d-162">Base the minimum height of your content area of your tab configuration page on fixed-height graphic elements.</span></span>
* <span data-ttu-id="4761d-163">Calculer l’espacement vertical disponible (hauteur de la zone de contenu dans la page de `window.innerHeight`Configuration) à l’aide de.</span><span class="sxs-lookup"><span data-stu-id="4761d-163">Calculate available vertical space (the height of the content area in the configuration page) using `window.innerHeight`.</span></span> <span data-ttu-id="4761d-164">Cette valeur renvoie la taille du `<iframe>` dans lequel votre page de configuration se trouve, ce qui peut changer dans les versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="4761d-164">This returns the size of the `<iframe>` in which your configuration page resides, which may change in future releases.</span></span> <span data-ttu-id="4761d-165">À l’aide de cette valeur, votre contenu s’ajuste automatiquement aux modifications ultérieures.</span><span class="sxs-lookup"><span data-stu-id="4761d-165">By using this value your content will adjust automatically to future changes.</span></span>
* <span data-ttu-id="4761d-166">Allouer de l’espace vertical aux éléments de hauteur variable moins ce qui est nécessaire pour les éléments de hauteur fixe.</span><span class="sxs-lookup"><span data-stu-id="4761d-166">Allocate vertical space to the variable-height elements minus what's needed for the fixed-height elements.</span></span>
* <span data-ttu-id="4761d-167">Pour l’état de *connexion* , centrez verticalement et horizontalement le contenu.</span><span class="sxs-lookup"><span data-stu-id="4761d-167">For the *login* state, vertically and horizontally center the content.</span></span>
* <span data-ttu-id="4761d-168">Si vous souhaitez une image d’arrière-plan, vous avez besoin d’une nouvelle image ajustée pour s’adapter à la zone (par défaut) ou vous pouvez conserver la même image et choisir entre :</span><span class="sxs-lookup"><span data-stu-id="4761d-168">If you want a background image, you need either a new image, sized to fit the area (preferred), or you can keep the same image and choose between:</span></span>
  * <span data-ttu-id="4761d-169">alignement sur le coin supérieur gauche.</span><span class="sxs-lookup"><span data-stu-id="4761d-169">aligning to the upper left hand corner.</span></span>
  * <span data-ttu-id="4761d-170">mise à l’échelle de l’image pour l’ajuster.</span><span class="sxs-lookup"><span data-stu-id="4761d-170">scaling the image to fit.</span></span>

<span data-ttu-id="4761d-171">Lorsque la taille est correcte, votre page de configuration d’onglet doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="4761d-171">When properly sized, your tab configuration page should look similar to this:</span></span>

<img width="450px" title="Onglet nouvelle configuration" src="~/assets/images/tabs/config-dialog-Contoso.png" />

## <a name="best-practices"></a><span data-ttu-id="4761d-173">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="4761d-173">Best practices</span></span>

### <a name="always-include-a-default-state"></a><span data-ttu-id="4761d-174">Toujours inclure un État par défaut</span><span class="sxs-lookup"><span data-stu-id="4761d-174">Always include a default state</span></span>

<span data-ttu-id="4761d-175">Incluez un État par défaut pour faciliter la configuration des onglets, même si votre onglet est configurable.</span><span class="sxs-lookup"><span data-stu-id="4761d-175">Include a default state to make tabs easy to set up even if your tab is configurable.</span></span>

### <a name="deep-linking"></a><span data-ttu-id="4761d-176">Liaison profonde</span><span class="sxs-lookup"><span data-stu-id="4761d-176">Deep linking</span></span>

<span data-ttu-id="4761d-177">Chaque fois que possible, les cartes et les robots doivent créer des liens approfondis vers des données plus riches dans un onglet hébergé. Par exemple, une carte peut afficher un résumé des données de bogue, mais vous pouvez cliquer dessus pour afficher l’intégralité du bogue dans un onglet.</span><span class="sxs-lookup"><span data-stu-id="4761d-177">Whenever possible, cards and bots should deep link to richer data in a hosted tab. For example, a card may show a summary of bug data, but clicking it can shows the entire bug in a tab.</span></span>

### <a name="naming"></a><span data-ttu-id="4761d-178">Donnant</span><span class="sxs-lookup"><span data-stu-id="4761d-178">Naming</span></span>

<span data-ttu-id="4761d-179">Dans de nombreux cas, le nom de votre application fera un excellent nom d’onglet.</span><span class="sxs-lookup"><span data-stu-id="4761d-179">In many cases, the name of your app will make a great tab name.</span></span> <span data-ttu-id="4761d-180">Toutefois, vous pouvez également nommer vos onglets en fonction de la fonctionnalité qu’ils fournissent.</span><span class="sxs-lookup"><span data-stu-id="4761d-180">But, also consider naming your tabs according to the functionality they provide.</span></span>

## <a name="notifications-for-tabs"></a><span data-ttu-id="4761d-181">Notifications pour les onglets</span><span class="sxs-lookup"><span data-stu-id="4761d-181">Notifications for tabs</span></span>

<span data-ttu-id="4761d-182">Il existe deux modes de notification pour les modifications apportées au contenu des onglets :</span><span class="sxs-lookup"><span data-stu-id="4761d-182">There are two modes of notification for tab content changes:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="4761d-183">**Utiliser l’API de l’application pour avertir les utilisateurs des modifications**.</span><span class="sxs-lookup"><span data-stu-id="4761d-183">**Use the app api to notify users of changes**.</span></span> <span data-ttu-id="4761d-184">Ce message s’affichera dans le flux d’activités de l’utilisateur et le lien profond vers l’onglet. *voir*  [créer des liens détaillés vers du contenu et des fonctionnalités dans Microsoft teams](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest)</span><span class="sxs-lookup"><span data-stu-id="4761d-184">This message will show up in the user’s activity feed and deep link to the tab. *See*  [Create deep links to content and features in Microsoft Teams](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest)</span></span>
> * <span data-ttu-id="4761d-185">**Utiliser un bot**.</span><span class="sxs-lookup"><span data-stu-id="4761d-185">**Use a bot**.</span></span> <span data-ttu-id="4761d-186">Cette méthode est préférée en particulier si le thread de tabulation est ciblé.</span><span class="sxs-lookup"><span data-stu-id="4761d-186">This method is preferred especially if the Tab thread is targeted.</span></span> <span data-ttu-id="4761d-187">Le résultat est que la conversation de thème de l’onglet est déplacée vers le mode récemment actif.</span><span class="sxs-lookup"><span data-stu-id="4761d-187">The result will be that the tab’s threaded conversation will be moved into view as recently active.</span></span> <span data-ttu-id="4761d-188">Cette méthode permet également une sophistication du mode d’envoi de la notification.</span><span class="sxs-lookup"><span data-stu-id="4761d-188">This method also allows for some sophistication in how the notification is sent.</span></span>

  <span data-ttu-id="4761d-189">L’envoi d’un message à un fil d’onglet augmente la sensibilisation de l’activité à tous les utilisateurs sans en informer explicitement tout le monde.</span><span class="sxs-lookup"><span data-stu-id="4761d-189">Sending a message to a tab thread increases the awareness of activity to all users without explicitly notifying everyone.</span></span> <span data-ttu-id="4761d-190">Il s’agit d’une sensibilisation sans bruit.</span><span class="sxs-lookup"><span data-stu-id="4761d-190">This is awareness without noise.</span></span> <span data-ttu-id="4761d-191">En outre, lorsque vous `@mention` avez des utilisateurs spécifiques, la même notification est placée dans le flux, en les liant directement au fil d’onglets.</span><span class="sxs-lookup"><span data-stu-id="4761d-191">In addition, when you `@mention`  specific users the same notification will be placed in their feed, deep linking them to the tab thread directly.</span></span>
