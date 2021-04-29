---
title: Onglets sur les appareils mobiles
description: Décrit les instructions pour la conception d'onglets qui fonctionnent sur les appareils mobiles.
ms.topic: conceptual
localization_priority: Normal
keywords: onglets mobiles des applications personnelles de l'infrastructure de référence des recommandations en matière de conception d'équipes
ms.openlocfilehash: cdcaddf5ba0fb18537e87daa4b459c7377225f76
ms.sourcegitcommit: d90c5dafea09e2893dea8da46ee49516bbaa04b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2021
ms.locfileid: "52075695"
---
# <a name="tabs-on-mobile"></a><span data-ttu-id="6677e-104">Onglets sur les appareils mobiles</span><span class="sxs-lookup"><span data-stu-id="6677e-104">Tabs on mobile</span></span>

<span data-ttu-id="6677e-105">Vous pouvez inclure des onglets dans les canaux mobiles, les conversations et les applications personnelles Teams.</span><span class="sxs-lookup"><span data-stu-id="6677e-105">You can include tabs in Teams mobile channels, chats, and personal apps.</span></span>

## <a name="accessing-personal-tabs"></a><span data-ttu-id="6677e-106">Accès aux onglets personnels</span><span class="sxs-lookup"><span data-stu-id="6677e-106">Accessing personal tabs</span></span>

<span data-ttu-id="6677e-107">Vous pouvez accéder aux onglets personnels dans le caisse de l'application.</span><span class="sxs-lookup"><span data-stu-id="6677e-107">You can access personal tabs in the app drawer.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-app-drawer.png" alt-text="Illustration montrant le caisse de l'application mobile Teams." border="false":::

## <a name="accessing-channel-tabs"></a><span data-ttu-id="6677e-109">Accès aux onglets de canal</span><span class="sxs-lookup"><span data-stu-id="6677e-109">Accessing channel tabs</span></span>

<span data-ttu-id="6677e-110">Vous pouvez accéder aux onglets de canal et de groupe en sélectionnant le bouton **Plus** dans le canal ou la conversation dans laquelle ils ont été ajoutés.</span><span class="sxs-lookup"><span data-stu-id="6677e-110">You can access channel and group tabs by selecting the **More** button in the channel or chat in which they've been added.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab.png" alt-text="Illustration montrant un onglet mobile Teams." border="false":::

## <a name="design-considerations"></a><span data-ttu-id="6677e-112">Considérations relatives à la conception</span><span class="sxs-lookup"><span data-stu-id="6677e-112">Design considerations</span></span>

<span data-ttu-id="6677e-113">Notre plateforme mobile permet aux applications d'être une expérience immersive avec le contenu de l'application prenant tout l'écran en dehors de la navigation Teams principale.</span><span class="sxs-lookup"><span data-stu-id="6677e-113">Our mobile platform allows apps to be an immersive experience with the app content taking up all of the screen apart from main Teams navigation.</span></span> <span data-ttu-id="6677e-114">Pour créer une expérience immersive adaptée à Teams, suivez ces instructions.</span><span class="sxs-lookup"><span data-stu-id="6677e-114">To create an immersive experience that fits with Teams, follow these guidelines.</span></span>

### <a name="responsive-design"></a><span data-ttu-id="6677e-115">Conception réactive</span><span class="sxs-lookup"><span data-stu-id="6677e-115">Responsive design</span></span>

<span data-ttu-id="6677e-116">Étant donné que votre onglet peut être ouvert sur des appareils avec un large éventail de tailles d'écran, il doit respecter les principes de [conception](https://www.w3schools.com/html/html_responsive.asp) réactifs.</span><span class="sxs-lookup"><span data-stu-id="6677e-116">Because your tab can be opened on devices with a wide range of screen sizes, it needs to follow [responsive design](https://www.w3schools.com/html/html_responsive.asp) principles.</span></span> <span data-ttu-id="6677e-117">Toutes les constructions clés doivent être accessibles sur les appareils mobiles et les vues ne doivent pas être déformées.</span><span class="sxs-lookup"><span data-stu-id="6677e-117">All of the key constructs should be accessible on mobile devices, and the views should not be distorted.</span></span> <span data-ttu-id="6677e-118">Assurez-vous que lorsque votre onglet est chargé sur un appareil mobile, tous les boutons et liens sont facilement accessibles à l'aide de la navigation avec les doigts.</span><span class="sxs-lookup"><span data-stu-id="6677e-118">Ensure that when your tab is loaded on a mobile device, all buttons and links are easily accessible using finger-based navigation.</span></span>

### <a name="layouts"></a><span data-ttu-id="6677e-119">Dispositions</span><span class="sxs-lookup"><span data-stu-id="6677e-119">Layouts</span></span>

<span data-ttu-id="6677e-120">Il est important de choisir la disposition correcte pour votre onglet.</span><span class="sxs-lookup"><span data-stu-id="6677e-120">Choosing the correct layout for your tab is important.</span></span> <span data-ttu-id="6677e-121">Vous devez prendre en compte le type d'informations que vous présentez et choisir une disposition qui les organise pour faciliter la consommation.</span><span class="sxs-lookup"><span data-stu-id="6677e-121">You should consider the kind of information you're presenting, and choose a layout that organizes it for easy consumption.</span></span> <span data-ttu-id="6677e-122">Certaines options potentielles sont décrites ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="6677e-122">Some potential options are outlined below.</span></span>

#### <a name="single-canvas"></a><span data-ttu-id="6677e-123">Canevas unique</span><span class="sxs-lookup"><span data-stu-id="6677e-123">Single canvas</span></span>

<span data-ttu-id="6677e-124">Il s'agit d'un domaine important dans lequel le travail est effectué.</span><span class="sxs-lookup"><span data-stu-id="6677e-124">This is one large area where work gets done.</span></span> <span data-ttu-id="6677e-125">L'application Wiki Teams suit ce modèle.</span><span class="sxs-lookup"><span data-stu-id="6677e-125">The Teams Wiki app follows this pattern.</span></span> <span data-ttu-id="6677e-126">Si vous avez une application qui ne sépare pas le contenu en composants plus petits, cela serait adapté.</span><span class="sxs-lookup"><span data-stu-id="6677e-126">If you have an app that doesn’t separate content into smaller components this would be a good fit.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-single-canvas.png" alt-text="Illustration montrant un onglet de canevas mobile Teams." border="false":::

#### <a name="list"></a><span data-ttu-id="6677e-128">Répertorier</span><span class="sxs-lookup"><span data-stu-id="6677e-128">List</span></span>

<span data-ttu-id="6677e-129">Les listes sont excellentes pour le tri et le filtrage de grandes quantités de données et sont très bonnes pour conserver les éléments les plus importants en haut.</span><span class="sxs-lookup"><span data-stu-id="6677e-129">Lists are great for sorting and filtering large quantities of data and are great at keeping the most important things at the top.</span></span> <span data-ttu-id="6677e-130">Il est utile d'utiliser des colonnes triables.</span><span class="sxs-lookup"><span data-stu-id="6677e-130">It is helpful to use sortable columns.</span></span> <span data-ttu-id="6677e-131">Les actions peuvent être ajoutées à chaque élément de liste sous le menu des ellipses.</span><span class="sxs-lookup"><span data-stu-id="6677e-131">Actions can be added to each list item under the ellipsis menu.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-list.png" alt-text="Illustration montrant un onglet de liste mobile Teams." border="false":::

#### <a name="grid"></a><span data-ttu-id="6677e-133">Grid</span><span class="sxs-lookup"><span data-stu-id="6677e-133">Grid</span></span>

<span data-ttu-id="6677e-134">Les grilles sont utiles pour l'affichage d'éléments hautement visuels.</span><span class="sxs-lookup"><span data-stu-id="6677e-134">Grids are useful for showing elements which are highly visual.</span></span> <span data-ttu-id="6677e-135">Il est utile d'inclure un contrôle de filtre ou de recherche en haut.</span><span class="sxs-lookup"><span data-stu-id="6677e-135">It helps to include a filter or search control at the top.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-grid.png" alt-text="Illustration montrant un onglet mobile Teams avec une disposition de grille." border="false":::

### <a name="tabs-with-bots-on-mobile"></a><span data-ttu-id="6677e-137">Onglets avec bots sur mobile</span><span class="sxs-lookup"><span data-stu-id="6677e-137">Tabs with bots on mobile</span></span>

<span data-ttu-id="6677e-138">L'exemple suivant est une application personnelle qui possède des onglets et un bot.</span><span class="sxs-lookup"><span data-stu-id="6677e-138">The following example is a personal app that has tabs and a bot.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-with-bot.png" alt-text="Illustration montrant comment une application Teams mobile avec des onglets et un bot." border="false":::

## <a name="ui-components"></a><span data-ttu-id="6677e-140">Composants de l'interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="6677e-140">UI components</span></span>

### <a name="color-palettes"></a><span data-ttu-id="6677e-141">Palettes de couleurs</span><span class="sxs-lookup"><span data-stu-id="6677e-141">Color palettes</span></span>

<span data-ttu-id="6677e-142">L'utilisation de notre palette neutre approuvée pour les arrière-plans, les notifications, le texte et les boutons permettra à votre application de se sentir plus à l'accueil dans Teams.</span><span class="sxs-lookup"><span data-stu-id="6677e-142">Using our approved neutral palette for backgrounds, notifications, text, and buttons will help your app feel more at home in Teams.</span></span> <span data-ttu-id="6677e-143">Étant donné que Teams mobile a deux thèmes à thèmes (clair et foncé), il est bon de s'assurer que votre application s'annonce bien dans les deux cas.</span><span class="sxs-lookup"><span data-stu-id="6677e-143">Since Teams mobile has two colour themes (light and dark), it’s a good idea to make sure your app looks great in both.</span></span>

#### <a name="light-color"></a><span data-ttu-id="6677e-144">Couleur claire</span><span class="sxs-lookup"><span data-stu-id="6677e-144">Light color</span></span>

![palette de couleurs claires](../../assets/images/light-color.png)

#### <a name="dark-color"></a><span data-ttu-id="6677e-146">Couleur foncée</span><span class="sxs-lookup"><span data-stu-id="6677e-146">Dark color</span></span>

![palette de couleurs foncées](../../assets/images/dark-color.png)

### <a name="buttons-and-controls"></a><span data-ttu-id="6677e-148">Boutons et contrôles</span><span class="sxs-lookup"><span data-stu-id="6677e-148">Buttons and controls</span></span>

<span data-ttu-id="6677e-149">Le style des boutons permet de communiquer le type d’action qu’ils déclenchent.</span><span class="sxs-lookup"><span data-stu-id="6677e-149">The way buttons are styled helps communicate what kind of action they trigger.</span></span> <span data-ttu-id="6677e-150">Nous tenez à jour un large éventail de boutons mis en forme pour afficher différents niveaux d’accentuation.</span><span class="sxs-lookup"><span data-stu-id="6677e-150">We maintain a wide range of buttons that are formatted to show different levels of emphasis.</span></span> <span data-ttu-id="6677e-151">Les boutons peuvent avoir du texte, une icône ou une combinaison de texte et d’icône.</span><span class="sxs-lookup"><span data-stu-id="6677e-151">Buttons can have text, an icon, or a combination of text and an icon.</span></span> <span data-ttu-id="6677e-152">Pour communiquer différents niveaux dans une hiérarchie, nous avons conçu des boutons principaux et secondaires dans chaque catégorie.</span><span class="sxs-lookup"><span data-stu-id="6677e-152">To communicate different levels in a hierarchy, we designed primary and secondary buttons within each category.</span></span>

#### <a name="buttons"></a><span data-ttu-id="6677e-153">Boutons</span><span class="sxs-lookup"><span data-stu-id="6677e-153">Buttons</span></span>

<span data-ttu-id="6677e-154">Boutons principal et secondaire.</span><span class="sxs-lookup"><span data-stu-id="6677e-154">Primary and secondary buttons.</span></span>

![image de boutons](../../assets/images/buttons.png)

#### <a name="selection-controls"></a><span data-ttu-id="6677e-156">Contrôles de sélection</span><span class="sxs-lookup"><span data-stu-id="6677e-156">Selection controls</span></span>

<span data-ttu-id="6677e-157">Boutons d’radio, case à cocher et boutons bascule.</span><span class="sxs-lookup"><span data-stu-id="6677e-157">Radio buttons, checkboxes, and toggles.</span></span>

![contrôles de sélection](../../assets/images/selection-controls.png)

#### <a name="chiclets-and-pills"></a><span data-ttu-id="6677e-159">Yézélettes et insérables</span><span class="sxs-lookup"><span data-stu-id="6677e-159">Chiclets and pills</span></span>

![tlets et l’errég](../../assets/images/chiclets-and-pills.png)

### <a name="typography"></a><span data-ttu-id="6677e-161">Typographie</span><span class="sxs-lookup"><span data-stu-id="6677e-161">Typography</span></span>

<span data-ttu-id="6677e-162">La typographie doit être claire et précise.</span><span class="sxs-lookup"><span data-stu-id="6677e-162">Typography should be clear and purposeful.</span></span> <span data-ttu-id="6677e-163">Mettre en avant des informations importantes et éviter d’utiliser plusieurs polices et tailles pour réduire la confusion.</span><span class="sxs-lookup"><span data-stu-id="6677e-163">Emphasize important information and avoid using multiple fonts and sizes to reduce confusion.</span></span> <span data-ttu-id="6677e-164">Nous vous recommandons d’utiliser un cas de phrase et d’éviter l’utilisation de toutes les limites pour la localisation et la lisibilité.</span><span class="sxs-lookup"><span data-stu-id="6677e-164">We recommend using sentence case and avoiding the usage of all caps for localization and legibility.</span></span>

![typograph mobile](../../assets/images/mobile-typography.png)

### <a name="fields-and-flyouts"></a><span data-ttu-id="6677e-166">Champs et volants</span><span class="sxs-lookup"><span data-stu-id="6677e-166">Fields and flyouts</span></span>

<span data-ttu-id="6677e-167">Les champs sont des zones où les utilisateurs peuvent entrer du texte.</span><span class="sxs-lookup"><span data-stu-id="6677e-167">Fields are areas where users can input text.</span></span> <span data-ttu-id="6677e-168">Les volants sont plus légers que les boîtes de dialogue et apparaissent dans le volet supérieur.</span><span class="sxs-lookup"><span data-stu-id="6677e-168">Flyouts are more lightweight than dialogs and appear from the top pane.</span></span>

#### <a name="list-controls"></a><span data-ttu-id="6677e-169">Répertorier les contrôles</span><span class="sxs-lookup"><span data-stu-id="6677e-169">List controls</span></span>

![contrôles de liste mobile](../../assets/images/mobile-list-controls.png)

#### <a name="field-controls"></a><span data-ttu-id="6677e-171">contrôles de champs</span><span class="sxs-lookup"><span data-stu-id="6677e-171">Field controls</span></span>

![contrôles de champ mobile](../../assets/images/mobile-field-controls.png)

## <a name="developer-considerations"></a><span data-ttu-id="6677e-173">Considérations pour les développeurs</span><span class="sxs-lookup"><span data-stu-id="6677e-173">Developer considerations</span></span>

<span data-ttu-id="6677e-174">Lorsque vous construisez une application qui inclut un onglet, vous devez prendre en compte (et tester) le fonctionnement de votre onglet sur les clients Microsoft Teams Android et iOS.</span><span class="sxs-lookup"><span data-stu-id="6677e-174">When you're building an app that includes a tab, you need to consider (and test) how your tab will function on both the Android and iOS Microsoft Teams clients.</span></span> <span data-ttu-id="6677e-175">Les sections ci-dessous décrivent certains des scénarios clés que vous devez prendre en considération.</span><span class="sxs-lookup"><span data-stu-id="6677e-175">The sections below outline some of the key scenarios you need to consider.</span></span>

### <a name="authentication"></a><span data-ttu-id="6677e-176">Authentification</span><span class="sxs-lookup"><span data-stu-id="6677e-176">Authentication</span></span>

<span data-ttu-id="6677e-177">Pour que l'authentification fonctionne sur les clients mobiles, vous devez mettre à niveau le SDK JavaScript teams vers la version 1.4.1 au minimum.</span><span class="sxs-lookup"><span data-stu-id="6677e-177">For authentication to work on mobile clients, you must upgrade you Teams JavaScript SDK to at least version 1.4.1.</span></span>

### <a name="low-bandwidth-and-intermittent-connections"></a><span data-ttu-id="6677e-178">Bande passante faible et connexions intermittentes</span><span class="sxs-lookup"><span data-stu-id="6677e-178">Low bandwidth and intermittent connections</span></span>

<span data-ttu-id="6677e-179">Les clients mobiles doivent régulièrement fonctionner avec une bande passante faible et des connexions intermittentes.</span><span class="sxs-lookup"><span data-stu-id="6677e-179">Mobile clients regularly need to function with low bandwidth and intermittent connections.</span></span> <span data-ttu-id="6677e-180">Votre application doit gérer les délai d'accès de manière appropriée en fournissant un message contextuel à l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6677e-180">Your app should handle any timeouts appropriately by providing a contextual message to the user.</span></span> <span data-ttu-id="6677e-181">Vous devez également fournir des indicateurs de progression des utilisateurs pour fournir des commentaires à vos utilisateurs pour tout processus de longue durée.</span><span class="sxs-lookup"><span data-stu-id="6677e-181">You should also user progress indicators to provide feedback to your users for any long-running processes.</span></span>

> [!NOTE]
> <span data-ttu-id="6677e-182">Les onglets sont activés sur les appareils mobiles uniquement après l'ajout de l'application à une liste d'autorisation, en fonction de l'entrée de l'équipe d'approbation.</span><span class="sxs-lookup"><span data-stu-id="6677e-182">Tabs are enabled on mobile only after the application is added to an allow list, based on the input of the approval team.</span></span> <span data-ttu-id="6677e-183">Pour vérifier la réactivité de l'appareil mobile, teamsubm@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="6677e-183">To check mobile responsiveness, reach out to teamsubm@microsoft.com.</span></span>

### <a name="testing-on-mobile-clients"></a><span data-ttu-id="6677e-184">Test sur les clients mobiles</span><span class="sxs-lookup"><span data-stu-id="6677e-184">Testing on mobile clients</span></span>

<span data-ttu-id="6677e-185">Vous devez vérifier que votre onglet fonctionne correctement sur des appareils mobiles de différentes tailles et qualités.</span><span class="sxs-lookup"><span data-stu-id="6677e-185">You need to validate that your tab functions properly on mobile devices of various sizes and qualities.</span></span> <span data-ttu-id="6677e-186">Pour les appareils Android, vous pouvez utiliser [DevTools](~/tabs/how-to/developer-tools.md) pour déboguer votre onglet pendant son exécution.</span><span class="sxs-lookup"><span data-stu-id="6677e-186">For Android devices, you can use the [DevTools](~/tabs/how-to/developer-tools.md) to debug your tab while it is running.</span></span> <span data-ttu-id="6677e-187">Nous vous recommandons de tester sur les appareils à haut et à faible niveau de performance, ainsi que sur une tablette.</span><span class="sxs-lookup"><span data-stu-id="6677e-187">We recommend that you test on both high and low performing devices, as well as on a tablet.</span></span>

### <a name="distribution"></a><span data-ttu-id="6677e-188">Distribution</span><span class="sxs-lookup"><span data-stu-id="6677e-188">Distribution</span></span>

<span data-ttu-id="6677e-189">Les applications répertoriées dans le magasin Teams doivent être approuvées pour une utilisation mobile afin de fonctionner correctement dans le client mobile Teams.</span><span class="sxs-lookup"><span data-stu-id="6677e-189">Apps listed on the Teams store must be approved for mobile use to function properly in the Teams mobile client.</span></span> <span data-ttu-id="6677e-190">Le comportement des onglets dépend de l'approbation ou non de votre application.</span><span class="sxs-lookup"><span data-stu-id="6677e-190">How tabs behave depends on whether your app is approved.</span></span>

#### <a name="channel-and-group-tab-behavior"></a><span data-ttu-id="6677e-191">Comportement des onglets de canal et de groupe</span><span class="sxs-lookup"><span data-stu-id="6677e-191">Channel and group tab behavior</span></span>

* <span data-ttu-id="6677e-192">**Comportement lorsqu'il est** approuvé : s'ouvre dans le client mobile Teams à l'aide de la configuration de votre `contentUrl` application.</span><span class="sxs-lookup"><span data-stu-id="6677e-192">**Behavior when approved**: Opens in the Teams mobile client using your app's `contentUrl` configuration.</span></span>
* <span data-ttu-id="6677e-193">**Comportement lorsqu'il n'est** pas approuvé : s'ouvre dans le navigateur par défaut de l'appareil à l'aide de la configuration de votre application (qui doit également être incluse dans la fonction de `websiteUrl` votre code `setSettings()` source).</span><span class="sxs-lookup"><span data-stu-id="6677e-193">**Behavior when not approved**: Opens in the device’s default browser using your app's `websiteUrl` configuration (which also must be included in your source code's `setSettings()` function).</span></span> <span data-ttu-id="6677e-194">Toutefois, les utilisateurs peuvent toujours charger l'onglet dans le client mobile Teams en sélectionnant Plus à côté de l'application et en choisissant **Ouvrir,** ce qui déclenche la configuration de votre  `contentUrl` application.</span><span class="sxs-lookup"><span data-stu-id="6677e-194">However, users can still load the tab in the Teams mobile client by selecting **More** next to the app and choosing **Open**, which triggers your app’s `contentUrl` configuration.</span></span>

#### <a name="personal-app-behavior"></a><span data-ttu-id="6677e-195">Comportement des applications personnelles</span><span class="sxs-lookup"><span data-stu-id="6677e-195">Personal app behavior</span></span>

* <span data-ttu-id="6677e-196">**Comportement lorsqu'il est** approuvé : chaque onglet de l'application personnelle s'affiche dans le client mobile Teams en utilisant leur `contentUrl` configuration respective.</span><span class="sxs-lookup"><span data-stu-id="6677e-196">**Behavior when approved**: Each tab in the personal app displays in the Teams mobile client using their respective `contentUrl` configuration.</span></span>
* <span data-ttu-id="6677e-197">**Comportement lorsqu'il n'est pas** approuvé : l'application personnelle n'est pas disponible dans le client mobile Teams.</span><span class="sxs-lookup"><span data-stu-id="6677e-197">**Behavior when not approved**: The personal app is unavailable in the Teams mobile client.</span></span>

#### <a name="non-teams-store-app-behavior"></a><span data-ttu-id="6677e-198">Comportement des applications du Store autres que Teams</span><span class="sxs-lookup"><span data-stu-id="6677e-198">Non-Teams store app behavior</span></span>

<span data-ttu-id="6677e-199">Si vous chargez une version de votre application ou que vous publiez dans le catalogue d'applications d'une organisation, le comportement de l'onglet sera le même que celui des applications du magasin Teams approuvées par Microsoft pour appareils mobiles.</span><span class="sxs-lookup"><span data-stu-id="6677e-199">If you're sideloading your app or publishing to an org's app catalog, tab behavior will be the same as Teams store apps approved by Microsoft for mobile.</span></span>
