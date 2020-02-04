---
title: Instructions de conception pour les onglets
description: Décrit les instructions pour la création d’onglets pour le contenu et la collaboration
keywords: instructions de conception de l’infrastructure de référence
ms.openlocfilehash: adf86678a42e2267af00734e1ef85efced882488
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673517"
---
# <a name="content-and-conversations-all-at-once-using-tabs"></a><span data-ttu-id="2834d-104">Contenu et conversations, tous à la fois à l’aide d’onglets</span><span class="sxs-lookup"><span data-stu-id="2834d-104">Content and conversations, all at once using tabs</span></span>

> [!Important]
> <span data-ttu-id="2834d-105">**Onglets sur les clients mobiles**</span><span class="sxs-lookup"><span data-stu-id="2834d-105">**Tabs on Mobile Clients**</span></span>
>
> <span data-ttu-id="2834d-106">Suivez les [instructions pour les onglets sur mobile](~/tabs/design/tabs-mobile.md) lors de la création de vos onglets.</span><span class="sxs-lookup"><span data-stu-id="2834d-106">Follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md) when creating your tabs.</span></span> <span data-ttu-id="2834d-107">Si votre onglet utilise l’authentification, vous devez mettre à niveau votre SDK teams JavaScript vers la version 1.4.1 ou une version ultérieure, sinon l’authentification échouera.</span><span class="sxs-lookup"><span data-stu-id="2834d-107">If your tab uses authentication, you must upgrade your Teams JavaScript SDK to version 1.4.1 or later, or authentication will fail.</span></span>
>
> <span data-ttu-id="2834d-108">**Onglets personnels (statiques) sur mobile :**</span><span class="sxs-lookup"><span data-stu-id="2834d-108">**Personal (static) tabs on mobile:**</span></span>
>
> * <span data-ttu-id="2834d-109">Les onglets statiques (application personnelle) sont disponibles dans l’Aperçu pour les [développeurs](~/resources/dev-preview/developer-preview-intro.md).</span><span class="sxs-lookup"><span data-stu-id="2834d-109">Static tabs (personal app) are available in [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
> * <span data-ttu-id="2834d-110">Lors de la création de vos onglets statiques, assurez-vous de suivre les [instructions pour les onglets sur les appareils mobiles](~/tabs/design/tabs-mobile.md)</span><span class="sxs-lookup"><span data-stu-id="2834d-110">While building your static tabs, ensure to follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md)</span></span>
>
> <span data-ttu-id="2834d-111">**Onglets canal/groupe (configurable) sur mobile :**</span><span class="sxs-lookup"><span data-stu-id="2834d-111">**Channel/group (configurable) tabs on mobile:**</span></span>
>
> * <span data-ttu-id="2834d-112">Les clients mobiles affichent uniquement les onglets dont `websiteUrl`la valeur est.</span><span class="sxs-lookup"><span data-stu-id="2834d-112">Mobile clients only show tabs that have a value for `websiteUrl`.</span></span> <span data-ttu-id="2834d-113">Si vous souhaitez que votre onglet apparaisse sur les clients mobiles Teams, vous devez définir la `websiteUrl`valeur de.</span><span class="sxs-lookup"><span data-stu-id="2834d-113">If you want your tab to appear on the Teams mobile clients, you must set the value of `websiteUrl`.</span></span>
> * <span data-ttu-id="2834d-114">Le comportement d’ouverture par défaut sur mobile consiste à ouvrir l’extérieur `websiteUrl`dans le navigateur à l’aide du.</span><span class="sxs-lookup"><span data-stu-id="2834d-114">Default open behavior on mobile is to open outside in browser using the `websiteUrl`.</span></span> <span data-ttu-id="2834d-115">Pour les applications publiées dans le magasin d’applications public, si vous voulez que les onglets de votre canal s’ouvrent dans teams par défaut, suivez les [instructions pour les onglets sur les appareils mobiles](~/tabs/design/tabs-mobile.md)et contactez votre représentant du support technique pour demander à être inclus dans la liste d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="2834d-115">For apps published to the public App Store, if you want your channel tab to open inside teams by default, follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md), and reach out to your support rep to request to be whitelisted.</span></span>

<span data-ttu-id="2834d-116">Les onglets sont des canevas que vous pouvez utiliser pour partager du contenu, organiser des conversations et héberger des services tiers dans le flux de travail Organic d’une équipe.</span><span class="sxs-lookup"><span data-stu-id="2834d-116">Tabs are canvases that you can use to share content, hold conversations, and host third-party services, all within a team’s organic workflow.</span></span> <span data-ttu-id="2834d-117">Lorsque vous créez un onglet dans Microsoft Teams, il place le centre et le centre de votre application Web où il est facilement accessible à partir des conversations clés.</span><span class="sxs-lookup"><span data-stu-id="2834d-117">When you build a tab in Microsoft Teams, it puts your web app front and center where it’s easily accessible from key conversations.</span></span>

## <a name="guidelines"></a><span data-ttu-id="2834d-118">Conseils</span><span class="sxs-lookup"><span data-stu-id="2834d-118">Guidelines</span></span>

<span data-ttu-id="2834d-119">Un onglet approprié doit présenter les caractéristiques suivantes :</span><span class="sxs-lookup"><span data-stu-id="2834d-119">A good tab should display the following characteristics:</span></span>

### <a name="focused-functionality"></a><span data-ttu-id="2834d-120">Fonctionnalités ciblées</span><span class="sxs-lookup"><span data-stu-id="2834d-120">Focused functionality</span></span>

<span data-ttu-id="2834d-121">Les onglets fonctionnent mieux lorsqu’ils sont conçus pour répondre à un besoin spécifique.</span><span class="sxs-lookup"><span data-stu-id="2834d-121">Tabs work best when they’re built to address a specific need.</span></span> <span data-ttu-id="2834d-122">Concentrez-vous sur un petit ensemble de tâches ou sur un sous-ensemble de données correspondant au canal dans lequel se trouve l’onglet.</span><span class="sxs-lookup"><span data-stu-id="2834d-122">Focus on a small set of tasks or a subset of data that’s relevant to the channel the tab is in.</span></span>

### <a name="reduced-chrome"></a><span data-ttu-id="2834d-123">Chrome réduit</span><span class="sxs-lookup"><span data-stu-id="2834d-123">Reduced chrome</span></span>

<span data-ttu-id="2834d-124">Évitez de créer plusieurs panneaux dans un onglet, d’ajouter des couches de navigation ou de demander aux utilisateurs de faire défiler verticalement et horizontalement dans un onglet. En d’autres termes, essayez de ne pas avoir d’onglets dans votre onglet.</span><span class="sxs-lookup"><span data-stu-id="2834d-124">Avoid creating multiple panels in a tab, adding layers of navigation, or requiring users to scroll both vertically and horizontally in one tab. In other words, try not to have tabs in your tab.</span></span>

> [!TIP]
> <span data-ttu-id="2834d-125">Évitez de créer plusieurs panneaux dans un onglet, d’ajouter des couches de navigation ou de demander aux utilisateurs de faire défiler verticalement et horizontalement dans un onglet.</span><span class="sxs-lookup"><span data-stu-id="2834d-125">Avoid creating multiple panels in a tab, adding layers of navigation, or requiring users to scroll both vertically and horizontally in one tab.</span></span>

### <a name="integration"></a><span data-ttu-id="2834d-126">Intégration</span><span class="sxs-lookup"><span data-stu-id="2834d-126">Integration</span></span>

<span data-ttu-id="2834d-127">Découvrez comment informer les utilisateurs de l’activité de l’onglet en publiant des cartes dans une conversation, par exemple.</span><span class="sxs-lookup"><span data-stu-id="2834d-127">Find ways to notify users about tab activity by posting cards to a conversation, for example.</span></span>

### <a name="conversational"></a><span data-ttu-id="2834d-128">Conversation</span><span class="sxs-lookup"><span data-stu-id="2834d-128">Conversational</span></span>

<span data-ttu-id="2834d-129">Trouver un moyen de faciliter la conversation sur un onglet. Cela garantit que le Centre des conversations est sur le contenu, les données ou le processus à portée de main.</span><span class="sxs-lookup"><span data-stu-id="2834d-129">Find a way to facilitate conversation around a tab. This ensures that conversations center on the content, data, or process at hand.</span></span>

### <a name="streamlined-access"></a><span data-ttu-id="2834d-130">Accès simplifié</span><span class="sxs-lookup"><span data-stu-id="2834d-130">Streamlined access</span></span>

<span data-ttu-id="2834d-131">Assurez-vous que vous accordez l’accès aux bonnes personnes au bon moment.</span><span class="sxs-lookup"><span data-stu-id="2834d-131">Make sure you’re granting access to the right people at the right time.</span></span> <span data-ttu-id="2834d-132">Le simple maintien de votre processus de connexion évite de créer des obstacles à la collaboration et à la collaboration.</span><span class="sxs-lookup"><span data-stu-id="2834d-132">Keeping your sign-in process simple will avoid creating barriers to contribution and collaboration.</span></span>

### <a name="personality"></a><span data-ttu-id="2834d-133">Caractéristique</span><span class="sxs-lookup"><span data-stu-id="2834d-133">Personality</span></span>

<span data-ttu-id="2834d-134">Votre zone de dessin de tabulation constitue une excellente occasion de personnaliser votre expérience.</span><span class="sxs-lookup"><span data-stu-id="2834d-134">Your tab canvas presents a good opportunity to brand your experience.</span></span> <span data-ttu-id="2834d-135">Incorporez vos propres logos, couleurs et dispositions pour communiquer la personnalité.</span><span class="sxs-lookup"><span data-stu-id="2834d-135">Incorporate your own logos, colors, and layouts to communicate personality.</span></span>

<span data-ttu-id="2834d-136">Votre logo est une partie importante de votre identité et une connexion avec vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="2834d-136">Your logo is an important part of your identity and a connection with your users.</span></span> <span data-ttu-id="2834d-137">Veillez donc à l’inclure.</span><span class="sxs-lookup"><span data-stu-id="2834d-137">So be sure to include it.</span></span>

* <span data-ttu-id="2834d-138">Placer votre logo dans le coin gauche ou droit ou le long du bord inférieur</span><span class="sxs-lookup"><span data-stu-id="2834d-138">Place your logo in the left or right corner or along the bottom edge</span></span>
* <span data-ttu-id="2834d-139">Garder votre logo petit et discret</span><span class="sxs-lookup"><span data-stu-id="2834d-139">Keep your logo small and unobtrusive</span></span>

> [!TIP]
> <span data-ttu-id="2834d-140">Utilisez notre style visuel pour que votre service ressemble à une partie de teams.</span><span class="sxs-lookup"><span data-stu-id="2834d-140">Please work with our visual style so your service feels like a part of Teams.</span></span>

---

## <a name="tab-layouts"></a><span data-ttu-id="2834d-141">Mises en page d’onglets</span><span class="sxs-lookup"><span data-stu-id="2834d-141">Tab layouts</span></span>

[!include[Tab layouts](~/includes/design/tab-layouts.html)]

---

## <a name="types-of-tabs"></a><span data-ttu-id="2834d-142">Types d’onglets</span><span class="sxs-lookup"><span data-stu-id="2834d-142">Types of tabs</span></span>

[!include[Tab types](~/includes/design/tab-types.html)]

---

## <a name="configuration-page-height"></a><span data-ttu-id="2834d-143">Hauteur de la page de configuration</span><span class="sxs-lookup"><span data-stu-id="2834d-143">Configuration page height</span></span>

>[!NOTE]
><span data-ttu-id="2834d-144">En septembre 2018, la hauteur de la [page de configuration](~/tabs/how-to/create-tab-pages/configuration-page.md) des onglets a été augmentée, tandis que la largeur est restée inchangée.</span><span class="sxs-lookup"><span data-stu-id="2834d-144">In September 2018, the height for the tab [configuration page](~/tabs/how-to/create-tab-pages/configuration-page.md) was increased while the width remained unchanged.</span></span> <span data-ttu-id="2834d-145">Si votre application est conçue pour une taille plus ancienne, votre page de configuration d’onglet aura une grande quantité d’espacement vertical.</span><span class="sxs-lookup"><span data-stu-id="2834d-145">If your app is designed for the older size your tab configuration page will have a great deal of vertical whitespace.</span></span> <span data-ttu-id="2834d-146">Les applications de magasin héritées exemptées de cette modification devront contacter Microsoft après la mise à jour pour prendre en compte les nouvelles dimensions.</span><span class="sxs-lookup"><span data-stu-id="2834d-146">Legacy store apps exempted from this change will need to contact Microsoft after updating to accommodate the new dimensions.</span></span>

<span data-ttu-id="2834d-147">Les dimensions de la page de configuration de l’onglet :</span><span class="sxs-lookup"><span data-stu-id="2834d-147">The dimensions of the tab configuration page:</span></span>

<img width="450px" title="Tailles des onglets de configuration" src="~/assets/images/tabs/config-dialog-Contoso2.png" />

### <a name="guidelines-for-tab-configuration-page-format"></a><span data-ttu-id="2834d-149">Instructions pour le format de page de configuration d’onglet</span><span class="sxs-lookup"><span data-stu-id="2834d-149">Guidelines for tab configuration page format</span></span>

* <span data-ttu-id="2834d-150">Basez la hauteur minimale de votre zone de contenu sur la page de configuration de votre onglet sur les éléments graphiques de hauteur fixe.</span><span class="sxs-lookup"><span data-stu-id="2834d-150">Base the minimum height of your content area of your tab configuration page on fixed-height graphic elements.</span></span>
* <span data-ttu-id="2834d-151">Calculer l’espacement vertical disponible (hauteur de la zone de contenu dans la page de `window.innerHeight`Configuration) à l’aide de.</span><span class="sxs-lookup"><span data-stu-id="2834d-151">Calculate available vertical space (the height of the content area in the configuration page) using `window.innerHeight`.</span></span> <span data-ttu-id="2834d-152">Cette valeur renvoie la taille du `<iframe>` dans lequel votre page de configuration se trouve, ce qui peut changer dans les versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="2834d-152">This returns the size of the `<iframe>` in which your configuration page resides, which may change in future releases.</span></span> <span data-ttu-id="2834d-153">À l’aide de cette valeur, votre contenu s’ajuste automatiquement aux modifications ultérieures.</span><span class="sxs-lookup"><span data-stu-id="2834d-153">By using this value your content will adjust automatically to future changes.</span></span>
* <span data-ttu-id="2834d-154">Allouer de l’espace vertical aux éléments de hauteur variable moins ce qui est nécessaire pour les éléments de hauteur fixe.</span><span class="sxs-lookup"><span data-stu-id="2834d-154">Allocate vertical space to the variable-height elements minus what's needed for the fixed-height elements.</span></span>
* <span data-ttu-id="2834d-155">Pour l’état de *connexion* , centrez verticalement et horizontalement le contenu.</span><span class="sxs-lookup"><span data-stu-id="2834d-155">For the *login* state, vertically and horizontally center the content.</span></span>
* <span data-ttu-id="2834d-156">Si vous souhaitez une image d’arrière-plan, vous avez besoin d’une nouvelle image ajustée pour s’adapter à la zone (par défaut) ou vous pouvez conserver la même image et choisir entre :</span><span class="sxs-lookup"><span data-stu-id="2834d-156">If you want a background image, you need either a new image, sized to fit the area (preferred), or you can keep the same image and choose between:</span></span>
  * <span data-ttu-id="2834d-157">alignement sur le coin supérieur gauche.</span><span class="sxs-lookup"><span data-stu-id="2834d-157">aligning to the upper left hand corner.</span></span>
  * <span data-ttu-id="2834d-158">mise à l’échelle de l’image pour l’ajuster.</span><span class="sxs-lookup"><span data-stu-id="2834d-158">scaling the image to fit.</span></span>

<span data-ttu-id="2834d-159">Lorsque la taille est correcte, votre page de configuration d’onglet doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="2834d-159">When properly sized, your tab configuration page should look similar to this:</span></span>

<img width="450px" title="Onglet nouvelle configuration" src="~/assets/images/tabs/config-dialog-Contoso.png" />

## <a name="best-practices"></a><span data-ttu-id="2834d-161">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="2834d-161">Best practices</span></span>

### <a name="always-include-a-default-state"></a><span data-ttu-id="2834d-162">Toujours inclure un État par défaut</span><span class="sxs-lookup"><span data-stu-id="2834d-162">Always include a default state</span></span>

<span data-ttu-id="2834d-163">Incluez un État par défaut pour faciliter la configuration des onglets, même si votre onglet est configurable.</span><span class="sxs-lookup"><span data-stu-id="2834d-163">Include a default state to make tabs easy to set up even if your tab is configurable.</span></span>

### <a name="deep-linking"></a><span data-ttu-id="2834d-164">Liaison profonde</span><span class="sxs-lookup"><span data-stu-id="2834d-164">Deep linking</span></span>

<span data-ttu-id="2834d-165">Chaque fois que possible, les cartes et les robots doivent créer des liens approfondis vers des données plus riches dans un onglet hébergé. Par exemple, une carte peut afficher un résumé des données de bogue, mais vous pouvez cliquer dessus pour afficher l’intégralité du bogue dans un onglet.</span><span class="sxs-lookup"><span data-stu-id="2834d-165">Whenever possible, cards and bots should deep link to richer data in a hosted tab. For example, a card may show a summary of bug data, but clicking it can shows the entire bug in a tab.</span></span>

### <a name="naming"></a><span data-ttu-id="2834d-166">Donnant</span><span class="sxs-lookup"><span data-stu-id="2834d-166">Naming</span></span>

<span data-ttu-id="2834d-167">Dans de nombreux cas, le nom de votre application peut donner un excellent nom d’onglet.</span><span class="sxs-lookup"><span data-stu-id="2834d-167">In many cases, the name of your app may make a great tab name.</span></span> <span data-ttu-id="2834d-168">Vous pouvez également nommer vos onglets en fonction de la fonctionnalité qu’ils fournissent.</span><span class="sxs-lookup"><span data-stu-id="2834d-168">But consider naming your tabs according to the functionality they provide.</span></span>
