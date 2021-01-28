---
title: Onglets sur les appareils mobiles
description: Décrit les instructions pour la conception d’onglets qui fonctionnent sur mobile.
ms.topic: conceptual
keywords: onglets mobiles des applications personnelles de l’infrastructure de référence des recommandations en matière de conception d’équipes
ms.openlocfilehash: 462228daa2179482110e2deb42f0f16ab2f5d5ec
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014172"
---
# <a name="tabs-on-mobile"></a><span data-ttu-id="1030f-104">Onglets sur les appareils mobiles</span><span class="sxs-lookup"><span data-stu-id="1030f-104">Tabs on mobile</span></span>

> [!NOTE]
> <span data-ttu-id="1030f-105">Si vous choisissez que votre onglet canal/groupe apparaisse sur les clients mobiles Teams, la configuration doit avoir une valeur pour la propriété `setSettings()` `websiteUrl` (voir ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="1030f-105">If you choose to have your channel/group tab appear on Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property (see below).</span></span>

<span data-ttu-id="1030f-106">Les onglets personnalisés peuvent faire partie d’un canal, d’une conversation de groupe ou d’une application personnelle (applications qui contiennent des onglets statiques et/ou un bot un-à-un).</span><span class="sxs-lookup"><span data-stu-id="1030f-106">Custom tabs can be part of a channel, group chat, or personal app (apps that contain static tabs and/or a one-to-one bot).</span></span>

<span data-ttu-id="1030f-107">Les applications personnelles sont disponibles sur les clients mobiles dans le caisse de l’application.</span><span class="sxs-lookup"><span data-stu-id="1030f-107">Personal apps are available on mobile clients in the app drawer.</span></span> <span data-ttu-id="1030f-108">L’application ne peut être installée qu’à partir d’un ordinateur de bureau ou d’un client web et son apparition sur les clients mobiles peut prendre jusqu’à 24 heures.</span><span class="sxs-lookup"><span data-stu-id="1030f-108">The app can only be installed from a desktop or web client, and can take up to 24 hours to appear on mobile clients.</span></span>

<span data-ttu-id="1030f-109">Les onglets de canal sont également disponibles sur les appareils mobiles.</span><span class="sxs-lookup"><span data-stu-id="1030f-109">Channel tabs are also available on mobile.</span></span> <span data-ttu-id="1030f-110">Le comportement par défaut consiste actuellement à utiliser votre `websiteUrl` onglet pour lancer votre onglet dans une fenêtre de navigateur.</span><span class="sxs-lookup"><span data-stu-id="1030f-110">The default behavior is currently to use your `websiteUrl` to launch your tab in a browser window.</span></span> <span data-ttu-id="1030f-111">Toutefois, ils peuvent être chargés sur un client mobile en cliquant sur le menu de dépassement en haut de l’onglet et en choisissant Ouvrir, qui vous permet de charger l’onglet à l’intérieur du `...` client mobile  `contentUrl` Teams.</span><span class="sxs-lookup"><span data-stu-id="1030f-111">However, they can be loaded on a mobile client by clicking the `...` overflow menu next to the tab and choosing **Open**, which will use your `contentUrl` to load the tab inside the Teams mobile client.</span></span>

## <a name="accessing-personal-tabs"></a><span data-ttu-id="1030f-112">Accès aux onglets personnels</span><span class="sxs-lookup"><span data-stu-id="1030f-112">Accessing personal tabs</span></span>

<span data-ttu-id="1030f-113">L’illustration suivante montre comment accéder à un onglet personnel sur un appareil mobile.</span><span class="sxs-lookup"><span data-stu-id="1030f-113">The following illustration shows how you access a personal tab on mobile.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-app-drawer.png" alt-text="Illustration montrant le caisse de l’application mobile Teams." border="false":::

## <a name="accessing-channel-tabs"></a><span data-ttu-id="1030f-115">Accès aux onglets de canal</span><span class="sxs-lookup"><span data-stu-id="1030f-115">Accessing channel tabs</span></span>

<span data-ttu-id="1030f-116">L’illustration suivante montre comment accéder à un onglet de canal sur mobile.</span><span class="sxs-lookup"><span data-stu-id="1030f-116">The following illustration shows how you access a channel tab on mobile.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab.png" alt-text="Illustration montrant un onglet mobile Teams." border="false":::

## <a name="design-considerations"></a><span data-ttu-id="1030f-118">Considérations relatives à la conception</span><span class="sxs-lookup"><span data-stu-id="1030f-118">Design considerations</span></span>

<span data-ttu-id="1030f-119">Notre plateforme mobile permet aux applications d’être une expérience immersive avec le contenu de l’application prenant tout l’écran en dehors de la navigation Teams principale.</span><span class="sxs-lookup"><span data-stu-id="1030f-119">Our mobile platform allows apps to be an immersive experience with the app content taking up all of the screen apart from main Teams navigation.</span></span> <span data-ttu-id="1030f-120">Pour créer une expérience immersive adaptée à Teams, suivez ces instructions.</span><span class="sxs-lookup"><span data-stu-id="1030f-120">To create an immersive experience that fits with Teams, follow these guidelines.</span></span>

### <a name="responsive-design"></a><span data-ttu-id="1030f-121">Conception réactive</span><span class="sxs-lookup"><span data-stu-id="1030f-121">Responsive design</span></span>

<span data-ttu-id="1030f-122">Étant donné que votre onglet peut être ouvert sur des appareils avec un large éventail de tailles d’écran, il doit respecter les principes de [conception](https://www.w3schools.com/html/html_responsive.asp) réactifs.</span><span class="sxs-lookup"><span data-stu-id="1030f-122">Because your tab can be opened on devices with a wide range of screen sizes, it needs to follow [responsive design](https://www.w3schools.com/html/html_responsive.asp) principles.</span></span> <span data-ttu-id="1030f-123">Toutes les constructions clés doivent être accessibles sur les appareils mobiles et les vues ne doivent pas être déformées.</span><span class="sxs-lookup"><span data-stu-id="1030f-123">All of the key constructs should be accessible on mobile devices, and the views should not be distorted.</span></span> <span data-ttu-id="1030f-124">Assurez-vous que lorsque votre onglet est chargé sur un appareil mobile, tous les boutons et liens sont facilement accessibles à l’aide de la navigation avec les doigts.</span><span class="sxs-lookup"><span data-stu-id="1030f-124">Ensure that when your tab is loaded on a mobile device, all buttons and links are easily accessible using finger-based navigation.</span></span>

### <a name="layouts"></a><span data-ttu-id="1030f-125">Dispositions</span><span class="sxs-lookup"><span data-stu-id="1030f-125">Layouts</span></span>

<span data-ttu-id="1030f-126">Il est important de choisir la disposition correcte pour votre onglet.</span><span class="sxs-lookup"><span data-stu-id="1030f-126">Choosing the correct layout for your tab is important.</span></span> <span data-ttu-id="1030f-127">Vous devez prendre en compte le type d’informations que vous présentez et choisir une disposition qui les organise pour faciliter la consommation.</span><span class="sxs-lookup"><span data-stu-id="1030f-127">You should consider the kind of information you're presenting, and choose a layout that organizes it for easy consumption.</span></span> <span data-ttu-id="1030f-128">Certaines options potentielles sont décrites ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="1030f-128">Some potential options are outlined below.</span></span>

#### <a name="single-canvas"></a><span data-ttu-id="1030f-129">Canevas unique</span><span class="sxs-lookup"><span data-stu-id="1030f-129">Single canvas</span></span>

<span data-ttu-id="1030f-130">Il s’agit d’un domaine important dans lequel le travail est effectué.</span><span class="sxs-lookup"><span data-stu-id="1030f-130">This is one large area where work gets done.</span></span> <span data-ttu-id="1030f-131">L’application Wiki Teams suit ce modèle.</span><span class="sxs-lookup"><span data-stu-id="1030f-131">The Teams Wiki app follows this pattern.</span></span> <span data-ttu-id="1030f-132">Si vous avez une application qui ne sépare pas le contenu en composants plus petits, cela serait adapté.</span><span class="sxs-lookup"><span data-stu-id="1030f-132">If you have an app that doesn’t separate content into smaller components this would be a good fit.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-single-canvas.png" alt-text="Illustration montrant un onglet de canevas mobile Teams." border="false":::

#### <a name="list"></a><span data-ttu-id="1030f-134">Répertorier</span><span class="sxs-lookup"><span data-stu-id="1030f-134">List</span></span>

<span data-ttu-id="1030f-135">Les listes sont excellentes pour le tri et le filtrage de grandes quantités de données et sont très bonnes pour conserver les éléments les plus importants en haut.</span><span class="sxs-lookup"><span data-stu-id="1030f-135">Lists are great for sorting and filtering large quantities of data and are great at keeping the most important things at the top.</span></span> <span data-ttu-id="1030f-136">Il est utile d’utiliser des colonnes triables.</span><span class="sxs-lookup"><span data-stu-id="1030f-136">It is helpful to use sortable columns.</span></span> <span data-ttu-id="1030f-137">Les actions peuvent être ajoutées à chaque élément de liste sous le menu des ellipses.</span><span class="sxs-lookup"><span data-stu-id="1030f-137">Actions can be added to each list item under the ellipsis menu.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-list.png" alt-text="Illustration montrant un onglet de liste mobile Teams." border="false":::

#### <a name="grid"></a><span data-ttu-id="1030f-139">Grid</span><span class="sxs-lookup"><span data-stu-id="1030f-139">Grid</span></span>

<span data-ttu-id="1030f-140">Les grilles sont utiles pour l’affichage d’éléments hautement visuels.</span><span class="sxs-lookup"><span data-stu-id="1030f-140">Grids are useful for showing elements which are highly visual.</span></span> <span data-ttu-id="1030f-141">Il est utile d’inclure un contrôle de filtre ou de recherche en haut.</span><span class="sxs-lookup"><span data-stu-id="1030f-141">It helps to include a filter or search control at the top.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-grid.png" alt-text="Illustration montrant un onglet mobile Teams avec une disposition de grille." border="false":::

### <a name="tabs-with-bots-on-mobile"></a><span data-ttu-id="1030f-143">Onglets avec bots sur mobile</span><span class="sxs-lookup"><span data-stu-id="1030f-143">Tabs with bots on mobile</span></span>

<span data-ttu-id="1030f-144">L’exemple suivant est une application personnelle qui possède des onglets et un bot.</span><span class="sxs-lookup"><span data-stu-id="1030f-144">The following example is a personal app that has tabs and a bot.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-with-bot.png" alt-text="Illustration montrant comment une application Teams mobile avec des onglets et un bot." border="false":::

## <a name="ui-components"></a><span data-ttu-id="1030f-146">Composants de l’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="1030f-146">UI components</span></span>

### <a name="color-palettes"></a><span data-ttu-id="1030f-147">Palettes de couleurs</span><span class="sxs-lookup"><span data-stu-id="1030f-147">Color palettes</span></span>

<span data-ttu-id="1030f-148">L’utilisation de notre palette neutre approuvée pour les arrière-plans, les notifications, le texte et les boutons permettra à votre application de se sentir plus à l’accueil dans Teams.</span><span class="sxs-lookup"><span data-stu-id="1030f-148">Using our approved neutral palette for backgrounds, notifications, text, and buttons will help your app feel more at home in Teams.</span></span> <span data-ttu-id="1030f-149">Étant donné que Teams mobile a deux thèmes à thèmes (clair et foncé), il est bon de s’assurer que votre application s’annonce bien dans les deux cas.</span><span class="sxs-lookup"><span data-stu-id="1030f-149">Since Teams mobile has two colour themes (light and dark), it’s a good idea to make sure your app looks great in both.</span></span>

#### <a name="light-color"></a><span data-ttu-id="1030f-150">Couleur claire</span><span class="sxs-lookup"><span data-stu-id="1030f-150">Light color</span></span>

![palette de couleurs claires](../../assets/images/light-color.png)

#### <a name="dark-color"></a><span data-ttu-id="1030f-152">Couleur foncée</span><span class="sxs-lookup"><span data-stu-id="1030f-152">Dark color</span></span>

![palette de couleurs foncées](../../assets/images/dark-color.png)

### <a name="buttons-and-controls"></a><span data-ttu-id="1030f-154">Boutons et contrôles</span><span class="sxs-lookup"><span data-stu-id="1030f-154">Buttons and controls</span></span>

<span data-ttu-id="1030f-155">Le style des boutons permet de communiquer le type d’action qu’ils déclenchent.</span><span class="sxs-lookup"><span data-stu-id="1030f-155">The way buttons are styled helps communicate what kind of action they trigger.</span></span> <span data-ttu-id="1030f-156">Nous tenez à jour un large éventail de boutons mis en forme pour afficher différents niveaux d’accentuation.</span><span class="sxs-lookup"><span data-stu-id="1030f-156">We maintain a wide range of buttons that are formatted to show different levels of emphasis.</span></span> <span data-ttu-id="1030f-157">Les boutons peuvent avoir du texte, une icône ou une combinaison de texte et d’icône.</span><span class="sxs-lookup"><span data-stu-id="1030f-157">Buttons can have text, an icon, or a combination of text and an icon.</span></span> <span data-ttu-id="1030f-158">Pour communiquer différents niveaux dans une hiérarchie, nous avons conçu des boutons principaux et secondaires dans chaque catégorie.</span><span class="sxs-lookup"><span data-stu-id="1030f-158">To communicate different levels in a hierarchy, we designed primary and secondary buttons within each category.</span></span>

#### <a name="buttons"></a><span data-ttu-id="1030f-159">Boutons</span><span class="sxs-lookup"><span data-stu-id="1030f-159">Buttons</span></span>

<span data-ttu-id="1030f-160">Boutons principal et secondaire.</span><span class="sxs-lookup"><span data-stu-id="1030f-160">Primary and secondary buttons.</span></span>

![image de boutons](../../assets/images/buttons.png)

#### <a name="selection-controls"></a><span data-ttu-id="1030f-162">Contrôles de sélection</span><span class="sxs-lookup"><span data-stu-id="1030f-162">Selection controls</span></span>

<span data-ttu-id="1030f-163">Boutons d’radio, case à cocher et boutons bascule.</span><span class="sxs-lookup"><span data-stu-id="1030f-163">Radio buttons, checkboxes, and toggles.</span></span>

![contrôles de sélection](../../assets/images/selection-controls.png)

#### <a name="chiclets-and-pills"></a><span data-ttu-id="1030f-165">Îles et err.</span><span class="sxs-lookup"><span data-stu-id="1030f-165">Chiclets and pills</span></span>

![tlets et l’errég](../../assets/images/chiclets-and-pills.png)

### <a name="typography"></a><span data-ttu-id="1030f-167">Typographie</span><span class="sxs-lookup"><span data-stu-id="1030f-167">Typography</span></span>

<span data-ttu-id="1030f-168">La typographie doit être claire et précise.</span><span class="sxs-lookup"><span data-stu-id="1030f-168">Typography should be clear and purposeful.</span></span> <span data-ttu-id="1030f-169">Mettre en avant des informations importantes et éviter d’utiliser plusieurs polices et tailles pour réduire la confusion.</span><span class="sxs-lookup"><span data-stu-id="1030f-169">Emphasize important information and avoid using multiple fonts and sizes to reduce confusion.</span></span> <span data-ttu-id="1030f-170">Nous vous recommandons d’utiliser un cas de phrase et d’éviter l’utilisation de toutes les limites pour la localisation et la lisibilité.</span><span class="sxs-lookup"><span data-stu-id="1030f-170">We recommend using sentence case and avoiding the usage of all caps for localization and legibility.</span></span>

![typograph mobile](../../assets/images/mobile-typography.png)

### <a name="fields-and-flyouts"></a><span data-ttu-id="1030f-172">Champs et volants</span><span class="sxs-lookup"><span data-stu-id="1030f-172">Fields and flyouts</span></span>

<span data-ttu-id="1030f-173">Les champs sont des zones où les utilisateurs peuvent entrer du texte.</span><span class="sxs-lookup"><span data-stu-id="1030f-173">Fields are areas where users can input text.</span></span> <span data-ttu-id="1030f-174">Les volants sont plus légers que les boîtes de dialogue et apparaissent dans le volet supérieur.</span><span class="sxs-lookup"><span data-stu-id="1030f-174">Flyouts are more lightweight than dialogs and appear from the top pane.</span></span>

#### <a name="list-controls"></a><span data-ttu-id="1030f-175">Répertorier les contrôles</span><span class="sxs-lookup"><span data-stu-id="1030f-175">List controls</span></span>

![contrôles de liste mobile](../../assets/images/mobile-list-controls.png)

#### <a name="field-controls"></a><span data-ttu-id="1030f-177">contrôles de champs</span><span class="sxs-lookup"><span data-stu-id="1030f-177">Field controls</span></span>

![contrôles de champ mobile](../../assets/images/mobile-field-controls.png)

## <a name="developer-considerations"></a><span data-ttu-id="1030f-179">Considérations sur les développeurs</span><span class="sxs-lookup"><span data-stu-id="1030f-179">Developer considerations</span></span>

<span data-ttu-id="1030f-180">Lorsque vous construisez une application qui inclut un onglet, vous devez prendre en compte (et tester) le fonctionnement de votre onglet sur les clients Microsoft Teams Android et iOS.</span><span class="sxs-lookup"><span data-stu-id="1030f-180">When you're building an app that includes a tab, you need to consider (and test) how your tab will function on both the Android and iOS Microsoft Teams clients.</span></span> <span data-ttu-id="1030f-181">Les sections ci-dessous décrivent certains des scénarios clés que vous devez prendre en considération.</span><span class="sxs-lookup"><span data-stu-id="1030f-181">The sections below outline some of the key scenarios you need to consider.</span></span>

### <a name="testing-on-mobile-clients"></a><span data-ttu-id="1030f-182">Test sur les clients mobiles</span><span class="sxs-lookup"><span data-stu-id="1030f-182">Testing on mobile clients</span></span>

<span data-ttu-id="1030f-183">Vous devez vérifier que votre onglet fonctionne correctement sur des appareils mobiles de différentes tailles et qualités.</span><span class="sxs-lookup"><span data-stu-id="1030f-183">You need to validate that your tab functions properly on mobile devices of various sizes and qualities.</span></span> <span data-ttu-id="1030f-184">Pour les appareils Android, vous pouvez utiliser [DevTools](~/tabs/how-to/developer-tools.md) pour déboguer votre onglet pendant son exécution.</span><span class="sxs-lookup"><span data-stu-id="1030f-184">For Android devices, you can use the [DevTools](~/tabs/how-to/developer-tools.md) to debug your tab while it is running.</span></span> <span data-ttu-id="1030f-185">Nous vous recommandons de tester les appareils à haut et faible niveau de performance, ainsi que sur une tablette.</span><span class="sxs-lookup"><span data-stu-id="1030f-185">We recommend that you test on both high and low performing devices, as well as on a tablet.</span></span>

### <a name="authentication"></a><span data-ttu-id="1030f-186">Authentification</span><span class="sxs-lookup"><span data-stu-id="1030f-186">Authentication</span></span>

<span data-ttu-id="1030f-187">Pour que l’authentification fonctionne sur les clients mobiles, vous devez mettre à niveau le SDK JavaScript teams vers la version 1.4.1 au minimum.</span><span class="sxs-lookup"><span data-stu-id="1030f-187">For authentication to work on mobile clients, you must upgrade you Teams JavaScript SDK to at least version 1.4.1.</span></span>

### <a name="low-bandwidth-and-intermittent-connections"></a><span data-ttu-id="1030f-188">Bande passante faible et connexions intermittentes</span><span class="sxs-lookup"><span data-stu-id="1030f-188">Low bandwidth and intermittent connections</span></span>

<span data-ttu-id="1030f-189">Les clients mobiles doivent régulièrement fonctionner avec une bande passante faible et des connexions intermittentes.</span><span class="sxs-lookup"><span data-stu-id="1030f-189">Mobile clients regularly need to function with low bandwidth and intermittent connections.</span></span> <span data-ttu-id="1030f-190">Votre application doit gérer les délai d’accès de manière appropriée en fournissant un message contextuel à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1030f-190">Your app should handle any timeouts appropriately by providing a contextual message to the user.</span></span> <span data-ttu-id="1030f-191">Vous devez également fournir des indicateurs de progression des utilisateurs pour fournir des commentaires à vos utilisateurs pour tout processus de longue durée.</span><span class="sxs-lookup"><span data-stu-id="1030f-191">You should also user progress indicators to provide feedback to your users for any long-running processes.</span></span>
