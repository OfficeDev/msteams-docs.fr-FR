---
title: Onglets sur les appareils mobiles
description: Décrit les lignes directrices pour la conception d’onglets qui fonctionnent sur mobile.
ms.topic: conceptual
localization_priority: Normal
keywords: les équipes conçoivent des lignes directrices de référence cadre d’applications personnelles onglets mobiles
ms.openlocfilehash: 853ab2c52edd1f4faedcc92e6f0e8d0821b580c7
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566697"
---
# <a name="tabs-on-mobile"></a><span data-ttu-id="ee3b2-104">Onglets sur les appareils mobiles</span><span class="sxs-lookup"><span data-stu-id="ee3b2-104">Tabs on mobile</span></span>

<span data-ttu-id="ee3b2-105">Vous pouvez inclure des onglets dans Teams canaux mobiles, des chats et des applications personnelles.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-105">You can include tabs in Teams mobile channels, chats, and personal apps.</span></span>

## <a name="accessing-personal-tabs"></a><span data-ttu-id="ee3b2-106">Accéder aux onglets personnels</span><span class="sxs-lookup"><span data-stu-id="ee3b2-106">Accessing personal tabs</span></span>

<span data-ttu-id="ee3b2-107">Vous pouvez accéder aux onglets personnels dans le tiroir de l’application.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-107">You can access personal tabs in the app drawer.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-app-drawer.png" alt-text="Illustration affichant le tiroir Teams d’application mobile." border="false":::

## <a name="accessing-channel-tabs"></a><span data-ttu-id="ee3b2-109">Accéder aux onglets du canal</span><span class="sxs-lookup"><span data-stu-id="ee3b2-109">Accessing channel tabs</span></span>

<span data-ttu-id="ee3b2-110">Vous pouvez accéder aux onglets de canal et de groupe en **sélectionnant le** bouton Plus dans le canal ou le chat dans lequel ils ont été ajoutés.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-110">You can access channel and group tabs by selecting the **More** button in the channel or chat in which they've been added.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab.png" alt-text="Illustration affichant un onglet mobile Teams de la maison." border="false":::

## <a name="design-considerations"></a><span data-ttu-id="ee3b2-112">Considérations relatives à la conception</span><span class="sxs-lookup"><span data-stu-id="ee3b2-112">Design considerations</span></span>

<span data-ttu-id="ee3b2-113">Notre plate-forme mobile permet aux applications d’être une expérience immersive avec le contenu de l’application prenant tout l’écran en dehors de la navigation Teams principale.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-113">Our mobile platform allows apps to be an immersive experience with the app content taking up all of the screen apart from main Teams navigation.</span></span> <span data-ttu-id="ee3b2-114">Pour créer une expérience immersive qui s’adapte à Teams, suivez ces lignes directrices.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-114">To create an immersive experience that fits with Teams, follow these guidelines.</span></span>

### <a name="responsive-design"></a><span data-ttu-id="ee3b2-115">Conception réactive</span><span class="sxs-lookup"><span data-stu-id="ee3b2-115">Responsive design</span></span>

<span data-ttu-id="ee3b2-116">Parce que votre onglet peut être ouvert sur les appareils avec un large éventail de tailles d’écran, il doit suivre les principes [de conception](https://www.w3schools.com/html/html_responsive.asp) réactive.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-116">Because your tab can be opened on devices with a wide range of screen sizes, it needs to follow [responsive design](https://www.w3schools.com/html/html_responsive.asp) principles.</span></span> <span data-ttu-id="ee3b2-117">Toutes les constructions clés doivent être accessibles sur les appareils mobiles, et les vues ne doivent pas être déformées.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-117">All of the key constructs should be accessible on mobile devices, and the views should not be distorted.</span></span> <span data-ttu-id="ee3b2-118">Assurez-vous que lorsque votre onglet est chargé sur un appareil mobile, tous les boutons et liens sont facilement accessibles à l’aide de la navigation basée sur les doigts.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-118">Ensure that when your tab is loaded on a mobile device, all buttons and links are easily accessible using finger-based navigation.</span></span>

### <a name="layouts"></a><span data-ttu-id="ee3b2-119">Dispositions</span><span class="sxs-lookup"><span data-stu-id="ee3b2-119">Layouts</span></span>

<span data-ttu-id="ee3b2-120">Il est important de choisir la bonne disposition pour votre onglet.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-120">Choosing the correct layout for your tab is important.</span></span> <span data-ttu-id="ee3b2-121">Vous devez tenir compte du type d’information que vous présentez, et choisir une mise en page qui l’organise pour une consommation facile.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-121">You should consider the kind of information you're presenting, and choose a layout that organizes it for easy consumption.</span></span> <span data-ttu-id="ee3b2-122">Certaines options potentielles sont décrites ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-122">Some potential options are outlined below.</span></span>

#### <a name="single-canvas"></a><span data-ttu-id="ee3b2-123">Toile unique</span><span class="sxs-lookup"><span data-stu-id="ee3b2-123">Single canvas</span></span>

<span data-ttu-id="ee3b2-124">C’est un grand domaine où le travail est fait.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-124">This is one large area where work gets done.</span></span> <span data-ttu-id="ee3b2-125">L Teams appr$ Wiki suit ce modèle.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-125">The Teams Wiki app follows this pattern.</span></span> <span data-ttu-id="ee3b2-126">Si vous avez une application qui ne sépare pas le contenu en composants plus petits, ce serait un bon ajustement.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-126">If you have an app that doesn’t separate content into smaller components this would be a good fit.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-single-canvas.png" alt-text="Illustration affichant un onglet Teams simple mobile de toile." border="false":::

#### <a name="list"></a><span data-ttu-id="ee3b2-128">Répertorier</span><span class="sxs-lookup"><span data-stu-id="ee3b2-128">List</span></span>

<span data-ttu-id="ee3b2-129">Les listes sont excellentes pour le tri et le filtrage de grandes quantités de données et sont excellentes pour garder les choses les plus importantes au sommet.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-129">Lists are great for sorting and filtering large quantities of data and are great at keeping the most important things at the top.</span></span> <span data-ttu-id="ee3b2-130">Il est utile d’utiliser des colonnes triables.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-130">It is helpful to use sortable columns.</span></span> <span data-ttu-id="ee3b2-131">Des actions peuvent être ajoutées à chaque élément de liste dans le menu ellipsis.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-131">Actions can be added to each list item under the ellipsis menu.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-list.png" alt-text="Illustration affichant un onglet Teams liste mobile." border="false":::

#### <a name="grid"></a><span data-ttu-id="ee3b2-133">grille</span><span class="sxs-lookup"><span data-stu-id="ee3b2-133">Grid</span></span>

<span data-ttu-id="ee3b2-134">Les grilles sont utiles pour montrer des éléments très visuels.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-134">Grids are useful for showing elements which are highly visual.</span></span> <span data-ttu-id="ee3b2-135">Il aide à inclure un filtre ou un contrôle de recherche en haut.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-135">It helps to include a filter or search control at the top.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-grid.png" alt-text="Illustration affichant un onglet mobile Teams avec une disposition de grille." border="false":::

### <a name="tabs-with-bots-on-mobile"></a><span data-ttu-id="ee3b2-137">Onglets avec bots sur mobile</span><span class="sxs-lookup"><span data-stu-id="ee3b2-137">Tabs with bots on mobile</span></span>

<span data-ttu-id="ee3b2-138">L’exemple suivant est une application personnelle qui a des onglets et un bot:</span><span class="sxs-lookup"><span data-stu-id="ee3b2-138">The following example is a personal app that has tabs and a bot:</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-with-bot.png" alt-text="Illustration montrant comment l’application Teams mobile qui a des onglets et un bot." border="false":::

## <a name="ui-components"></a><span data-ttu-id="ee3b2-140">Composants d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="ee3b2-140">UI components</span></span>

### <a name="color-palettes"></a><span data-ttu-id="ee3b2-141">Palettes de couleurs</span><span class="sxs-lookup"><span data-stu-id="ee3b2-141">Color palettes</span></span>

<span data-ttu-id="ee3b2-142">L’utilisation de notre palette neutre approuvée pour les arrière-plans, les notifications, le texte et les boutons aidera votre application à se sentir plus à l’aise Teams.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-142">Using our approved neutral palette for backgrounds, notifications, text, and buttons will help your app feel more at home in Teams.</span></span> <span data-ttu-id="ee3b2-143">Depuis Teams mobile a deux thèmes de couleur (clair et foncé), c’est une bonne idée de s’assurer que votre application ressemble beaucoup dans les deux.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-143">Since Teams mobile has two colour themes (light and dark), it’s a good idea to make sure your app looks great in both.</span></span>

#### <a name="light-color"></a><span data-ttu-id="ee3b2-144">Couleur claire</span><span class="sxs-lookup"><span data-stu-id="ee3b2-144">Light color</span></span>

![palette de couleurs claires](../../assets/images/light-color.png)

#### <a name="dark-color"></a><span data-ttu-id="ee3b2-146">Couleur foncée</span><span class="sxs-lookup"><span data-stu-id="ee3b2-146">Dark color</span></span>

![palette de couleurs foncées](../../assets/images/dark-color.png)

### <a name="buttons-and-controls"></a><span data-ttu-id="ee3b2-148">Boutons et commandes</span><span class="sxs-lookup"><span data-stu-id="ee3b2-148">Buttons and controls</span></span>

<span data-ttu-id="ee3b2-149">La façon dont les boutons sont sifflés aide à communiquer quel type d’action ils déclenchent.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-149">The way buttons are styled helps communicate what kind of action they trigger.</span></span> <span data-ttu-id="ee3b2-150">Nous maintenons un large éventail de boutons qui sont formatés pour montrer différents niveaux d’emphase.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-150">We maintain a wide range of buttons that are formatted to show different levels of emphasis.</span></span> <span data-ttu-id="ee3b2-151">Les boutons peuvent avoir du texte, une icône ou une combinaison de texte et d’icône.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-151">Buttons can have text, an icon, or a combination of text and an icon.</span></span> <span data-ttu-id="ee3b2-152">Pour communiquer différents niveaux dans une hiérarchie, nous avons conçu des boutons primaires et secondaires dans chaque catégorie.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-152">To communicate different levels in a hierarchy, we designed primary and secondary buttons within each category.</span></span>

#### <a name="buttons"></a><span data-ttu-id="ee3b2-153">Boutons</span><span class="sxs-lookup"><span data-stu-id="ee3b2-153">Buttons</span></span>

<span data-ttu-id="ee3b2-154">Boutons primaires et secondaires.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-154">Primary and secondary buttons.</span></span>

![image boutons](../../assets/images/buttons.png)

#### <a name="selection-controls"></a><span data-ttu-id="ee3b2-156">Contrôles de sélection</span><span class="sxs-lookup"><span data-stu-id="ee3b2-156">Selection controls</span></span>

<span data-ttu-id="ee3b2-157">Boutons radio, caisses à cocher et basculements.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-157">Radio buttons, checkboxes, and toggles.</span></span>

![contrôles de sélection](../../assets/images/selection-controls.png)

#### <a name="chiclets-and-pills"></a><span data-ttu-id="ee3b2-159">Chiclets et pilules</span><span class="sxs-lookup"><span data-stu-id="ee3b2-159">Chiclets and pills</span></span>

![chiclets et pilules](../../assets/images/chiclets-and-pills.png)

### <a name="typography"></a><span data-ttu-id="ee3b2-161">Typographie</span><span class="sxs-lookup"><span data-stu-id="ee3b2-161">Typography</span></span>

<span data-ttu-id="ee3b2-162">La typographie doit être claire et délibérée.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-162">Typography should be clear and purposeful.</span></span> <span data-ttu-id="ee3b2-163">Mettez l’accent sur des informations importantes et évitez d’utiliser plusieurs polices et tailles pour réduire la confusion.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-163">Emphasize important information and avoid using multiple fonts and sizes to reduce confusion.</span></span> <span data-ttu-id="ee3b2-164">Nous vous recommandons d’utiliser le cas de phrase et d’éviter l’utilisation de tous les plafonds pour la localisation et la lisibilité.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-164">We recommend using sentence case and avoiding the usage of all caps for localization and legibility.</span></span>

![typographe mobile](../../assets/images/mobile-typography.png)

### <a name="fields-and-flyouts"></a><span data-ttu-id="ee3b2-166">Champs et flyouts</span><span class="sxs-lookup"><span data-stu-id="ee3b2-166">Fields and flyouts</span></span>

<span data-ttu-id="ee3b2-167">Les champs sont des domaines où les utilisateurs peuvent entrer du texte.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-167">Fields are areas where users can input text.</span></span> <span data-ttu-id="ee3b2-168">Les flyouts sont plus légers que les dialogues et apparaissent à partir du volet supérieur.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-168">Flyouts are more lightweight than dialogs and appear from the top pane.</span></span>

#### <a name="list-controls"></a><span data-ttu-id="ee3b2-169">Répertorier les contrôles</span><span class="sxs-lookup"><span data-stu-id="ee3b2-169">List controls</span></span>

![contrôles de liste mobiles](../../assets/images/mobile-list-controls.png)

#### <a name="field-controls"></a><span data-ttu-id="ee3b2-171">contrôles de champs</span><span class="sxs-lookup"><span data-stu-id="ee3b2-171">Field controls</span></span>

![commandes mobiles sur le terrain](../../assets/images/mobile-field-controls.png)

## <a name="developer-considerations"></a><span data-ttu-id="ee3b2-173">Considérations des développeurs</span><span class="sxs-lookup"><span data-stu-id="ee3b2-173">Developer considerations</span></span>

<span data-ttu-id="ee3b2-174">Lorsque vous construisez une application qui inclut un onglet, vous devez considérer (et tester) comment votre onglet fonctionnera à la fois sur les clients Android et iOS Microsoft Teams clients.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-174">When you're building an app that includes a tab, you need to consider (and test) how your tab will function on both the Android and iOS Microsoft Teams clients.</span></span> <span data-ttu-id="ee3b2-175">Les sections ci-dessous décrivent certains des scénarios clés que vous devez envisager.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-175">The sections below outline some of the key scenarios you need to consider.</span></span>

### <a name="authentication"></a><span data-ttu-id="ee3b2-176">Authentification</span><span class="sxs-lookup"><span data-stu-id="ee3b2-176">Authentication</span></span>

<span data-ttu-id="ee3b2-177">Pour que l’authentification fonctionne sur les clients mobiles, vous devez Teams javascript SDK à au moins la version 1.4.1.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-177">For authentication to work on mobile clients, you must upgrade you Teams JavaScript SDK to at least version 1.4.1.</span></span>

### <a name="low-bandwidth-and-intermittent-connections"></a><span data-ttu-id="ee3b2-178">Faible bande passante et connexions intermittentes</span><span class="sxs-lookup"><span data-stu-id="ee3b2-178">Low bandwidth and intermittent connections</span></span>

<span data-ttu-id="ee3b2-179">Les clients mobiles doivent régulièrement fonctionner avec une faible bande passante et des connexions intermittentes.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-179">Mobile clients regularly need to function with low bandwidth and intermittent connections.</span></span> <span data-ttu-id="ee3b2-180">Votre application doit gérer les délais d’attente de manière appropriée en fournissant un message contextuel à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-180">Your app should handle any timeouts appropriately by providing a contextual message to the user.</span></span> <span data-ttu-id="ee3b2-181">Vous devez également utiliser des indicateurs de progression pour fournir des commentaires à vos utilisateurs pour tous les processus de longue durée.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-181">You should also user progress indicators to provide feedback to your users for any long-running processes.</span></span>

> [!NOTE]
> <span data-ttu-id="ee3b2-182">Les onglets ne sont activés sur mobile qu’après l’ajout de l’application à une liste d’autorisation, en fonction de l’entrée de l’équipe d’approbation.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-182">Tabs are enabled on mobile only after the application is added to an allow list, based on the input of the approval team.</span></span> <span data-ttu-id="ee3b2-183">Pour vérifier la réactivité mobile, teindez la main à teamsubm@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-183">To check mobile responsiveness, reach out to teamsubm@microsoft.com.</span></span>

### <a name="testing-on-mobile-clients"></a><span data-ttu-id="ee3b2-184">Tests sur les clients mobiles</span><span class="sxs-lookup"><span data-stu-id="ee3b2-184">Testing on mobile clients</span></span>

<span data-ttu-id="ee3b2-185">Vous devez valider que votre onglet fonctionne correctement sur les appareils mobiles de différentes tailles et qualités.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-185">You need to validate that your tab functions properly on mobile devices of various sizes and qualities.</span></span> <span data-ttu-id="ee3b2-186">Pour les appareils Android, vous pouvez utiliser les [DevTools pour](~/tabs/how-to/developer-tools.md) débog vos onglets pendant qu’il est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-186">For Android devices, you can use the [DevTools](~/tabs/how-to/developer-tools.md) to debug your tab while it is running.</span></span> <span data-ttu-id="ee3b2-187">Nous vous recommandons de tester sur les appareils haute et basse performance, y compris une tablette.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-187">We recommend that you test on both high- and low-performance devices, including a tablet.</span></span>

### <a name="distribution"></a><span data-ttu-id="ee3b2-188">Distribution</span><span class="sxs-lookup"><span data-stu-id="ee3b2-188">Distribution</span></span>

<span data-ttu-id="ee3b2-189">Les applications répertoriées dans Teams magasin doivent être approuvées pour une utilisation mobile qui fonctionne correctement dans Teams client mobile.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-189">Apps listed on the Teams store must be approved for mobile use to function properly in the Teams mobile client.</span></span> <span data-ttu-id="ee3b2-190">La disponibilité et le comportement de l’onglet dépendent de l’approbation ou non de votre application.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-190">Tab availability and behavior depends on whether your app is approved.</span></span>

#### <a name="apps-on-teams-store-approved-for-mobile"></a><span data-ttu-id="ee3b2-191">Applications sur Teams web approuvées pour mobile</span><span class="sxs-lookup"><span data-stu-id="ee3b2-191">Apps on Teams store approved for mobile</span></span>

<span data-ttu-id="ee3b2-192">Le tableau suivant décrit la disponibilité et le comportement de l’onglet lorsque l’application est répertoriée sur le Teams et approuvée pour un usage mobile :</span><span class="sxs-lookup"><span data-stu-id="ee3b2-192">The following table describes tab availability and behavior when the app is listed on the Teams store and approved for mobile use:</span></span>

|<span data-ttu-id="ee3b2-193">Fonctionnalité</span><span class="sxs-lookup"><span data-stu-id="ee3b2-193">Capability</span></span>   |<span data-ttu-id="ee3b2-194">Disponibilité mobile ?</span><span class="sxs-lookup"><span data-stu-id="ee3b2-194">Mobile availability?</span></span>   |<span data-ttu-id="ee3b2-195">Comportement mobile</span><span class="sxs-lookup"><span data-stu-id="ee3b2-195">Mobile behavior</span></span>|
|----------|-----------|------------|
|<span data-ttu-id="ee3b2-196">Canal</span><span class="sxs-lookup"><span data-stu-id="ee3b2-196">Channel</span></span> <br /> <span data-ttu-id="ee3b2-197">et onglet groupe</span><span class="sxs-lookup"><span data-stu-id="ee3b2-197">and group tab</span></span>|<span data-ttu-id="ee3b2-198">Oui</span><span class="sxs-lookup"><span data-stu-id="ee3b2-198">Yes</span></span>|<span data-ttu-id="ee3b2-199">L’onglet s’ouvre Teams client mobile en utilisant la configuration de votre `contentUrl` application.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-199">Tab opens in the Teams mobile client using your app's `contentUrl` configuration.</span></span>|
|<span data-ttu-id="ee3b2-200">Application personnelle</span><span class="sxs-lookup"><span data-stu-id="ee3b2-200">Personal app</span></span>|<span data-ttu-id="ee3b2-201">Oui</span><span class="sxs-lookup"><span data-stu-id="ee3b2-201">Yes</span></span>|<span data-ttu-id="ee3b2-202">Chaque onglet de l’onglet application personnelle s’ouvre dans le Teams client mobile en utilisant sa `contentUrl` configuration respective.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-202">Each tab in the personal app tab opens in the Teams mobile client using its respective `contentUrl` configuration.</span></span>|

#### <a name="apps-on-teams-store-not-approved-for-mobile"></a><span data-ttu-id="ee3b2-203">Les applications sur Teams magasin non approuvé pour mobile</span><span class="sxs-lookup"><span data-stu-id="ee3b2-203">Apps on Teams store not approved for mobile</span></span>

<span data-ttu-id="ee3b2-204">Le tableau suivant décrit la disponibilité et le comportement de l’onglet lorsque l’application est répertoriée sur le Teams store mais n’est pas approuvée pour une utilisation mobile :</span><span class="sxs-lookup"><span data-stu-id="ee3b2-204">The following table describes tab availability and behavior when the app is listed on the Teams store but not approved for mobile use:</span></span>

| <span data-ttu-id="ee3b2-205">Fonctionnalité</span><span class="sxs-lookup"><span data-stu-id="ee3b2-205">Capability</span></span> | <span data-ttu-id="ee3b2-206">Disponibilité mobile ?</span><span class="sxs-lookup"><span data-stu-id="ee3b2-206">Mobile availability?</span></span> | <span data-ttu-id="ee3b2-207">Comportement mobile</span><span class="sxs-lookup"><span data-stu-id="ee3b2-207">Mobile behavior</span></span> |
|----------|-----------|------------|
|<span data-ttu-id="ee3b2-208">Onglet Canal et groupe</span><span class="sxs-lookup"><span data-stu-id="ee3b2-208">Channel and group tab</span></span>|<span data-ttu-id="ee3b2-209">Oui</span><span class="sxs-lookup"><span data-stu-id="ee3b2-209">Yes</span></span>|<span data-ttu-id="ee3b2-210">L’onglet s’ouvre dans le navigateur par défaut de l’appareil au lieu du client mobile Teams utilisant la configuration de `websiteUrl` votre application, qui doit également être incluse dans la fonction de votre code `setSettings()` [](/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest#functions&preserve-view=true)source.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-210">Tab opens in the device's default browser instead of the Teams mobile client using your app's `websiteUrl` configuration, which also must be included in your source code's `setSettings()` [function](/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest#functions&preserve-view=true).</span></span> <span data-ttu-id="ee3b2-211">Toutefois, les utilisateurs peuvent toujours afficher l’onglet dans le client mobile Teams en **sélectionnant Plus à côté** de l’application et **en choisissant Open**, qui déclenche la configuration de votre `contentUrl` application.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-211">However, users can still view the tab in the Teams mobile client by selecting **More** next to the app and choosing **Open**, which triggers your app’s `contentUrl` configuration.</span></span>|
|<span data-ttu-id="ee3b2-212">Application personnelle</span><span class="sxs-lookup"><span data-stu-id="ee3b2-212">Personal app</span></span>|<span data-ttu-id="ee3b2-213">Non</span><span class="sxs-lookup"><span data-stu-id="ee3b2-213">No</span></span>|<span data-ttu-id="ee3b2-214">Non applicable</span><span class="sxs-lookup"><span data-stu-id="ee3b2-214">Not applicable</span></span>|

#### <a name="apps-not-on-teams-store"></a><span data-ttu-id="ee3b2-215">Applications non sur Teams store</span><span class="sxs-lookup"><span data-stu-id="ee3b2-215">Apps not on Teams store</span></span>

<span data-ttu-id="ee3b2-216">Si vous chargez votre application ou publiez sur le catalogue d’applications d’une organisation, le comportement de l’onglet sera le même que les applications Teams store approuvées par Microsoft pour mobile.</span><span class="sxs-lookup"><span data-stu-id="ee3b2-216">If you're sideloading your app or publishing to an org's app catalog, tab behavior will be the same as Teams store apps approved by Microsoft for mobile.</span></span>
