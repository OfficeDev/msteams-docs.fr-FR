---
title: Onglets sur les appareils mobiles
description: Décrit les instructions permettant de concevoir des onglets qui fonctionnent sur mobile.
keywords: instructions de conception teams structure de référence des applications personnelles onglets mobiles
ms.openlocfilehash: a1939465b04a1fe4b803efaf83402852ca536059
ms.sourcegitcommit: b51a4982842948336cfabedb63bdf8f72703585e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/25/2020
ms.locfileid: "48279765"
---
# <a name="tabs-on-mobile"></a><span data-ttu-id="4e75e-104">Onglets sur les appareils mobiles</span><span class="sxs-lookup"><span data-stu-id="4e75e-104">Tabs on mobile</span></span>

> [!NOTE]
> <span data-ttu-id="4e75e-105">Si vous choisissez d’afficher l’onglet canal/groupe sur les clients mobiles Teams, la `setSettings()` configuration doit avoir une valeur pour la `websiteUrl` propriété (voir ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="4e75e-105">If you choose to have your channel/group tab appear on Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property (see below).</span></span>

<span data-ttu-id="4e75e-106">Les onglets personnalisés peuvent faire partie d’un canal, d’une conversation de groupe ou d’une application personnelle (applications qui contiennent des onglets statiques et/ou un bot un-à-un).</span><span class="sxs-lookup"><span data-stu-id="4e75e-106">Custom tabs can be part of a channel, group chat, or personal app (apps that contain static tabs and/or a one-to-one bot).</span></span>

<span data-ttu-id="4e75e-107">Les applications personnelles sont disponibles sur les clients mobiles dans le tiroir d’application.</span><span class="sxs-lookup"><span data-stu-id="4e75e-107">Personal apps are available on mobile clients in the app drawer.</span></span> <span data-ttu-id="4e75e-108">L’application ne peut être installée qu’à partir d’un client de bureau ou Web, et peut prendre jusqu’à 24 heures pour apparaître sur les clients mobiles.</span><span class="sxs-lookup"><span data-stu-id="4e75e-108">The app can only be installed from a desktop or web client, and can take up to 24 hours to appear on mobile clients.</span></span>

<span data-ttu-id="4e75e-109">Les onglets de canal sont également disponibles sur mobile.</span><span class="sxs-lookup"><span data-stu-id="4e75e-109">Channel tabs are also available on mobile.</span></span> <span data-ttu-id="4e75e-110">Le comportement par défaut consiste à utiliser votre `websiteUrl` pour lancer votre onglet dans une fenêtre de navigateur.</span><span class="sxs-lookup"><span data-stu-id="4e75e-110">The default behavior is currently to use your `websiteUrl` to launch your tab in a browser window.</span></span> <span data-ttu-id="4e75e-111">Toutefois, ils peuvent être chargés sur un client mobile en cliquant sur le `...` menu de dépassement de capacité en regard de l’onglet et en choisissant **ouvrir**, qui utilisera votre `contentUrl` pour charger l’onglet à l’intérieur du client mobile Teams.</span><span class="sxs-lookup"><span data-stu-id="4e75e-111">However, they can be loaded on a mobile client by clicking the `...` overflow menu next to the tab and choosing **Open**, which will use your `contentUrl` to load the tab inside the Teams mobile client.</span></span>

## <a name="accessing-personal-tabs"></a><span data-ttu-id="4e75e-112">Accès aux onglets personnels</span><span class="sxs-lookup"><span data-stu-id="4e75e-112">Accessing personal tabs</span></span>

<span data-ttu-id="4e75e-113">L’illustration suivante montre comment accéder à un onglet personnel sur mobile.</span><span class="sxs-lookup"><span data-stu-id="4e75e-113">The following illustration shows how you access a personal tab on mobile.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-app-drawer.png" alt-text="Illustration illustrant le tiroir d’une application mobile Teams." border="false":::

## <a name="accessing-channel-tabs"></a><span data-ttu-id="4e75e-115">Accès aux onglets des canaux</span><span class="sxs-lookup"><span data-stu-id="4e75e-115">Accessing channel tabs</span></span>

<span data-ttu-id="4e75e-116">L’illustration suivante montre comment accéder à un onglet de canal sur mobile.</span><span class="sxs-lookup"><span data-stu-id="4e75e-116">The following illustration shows how you access a channel tab on mobile.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab.png" alt-text="Illustration illustrant un onglet teams mobile." border="false":::

## <a name="design-considerations"></a><span data-ttu-id="4e75e-118">Considérations relatives à la conception</span><span class="sxs-lookup"><span data-stu-id="4e75e-118">Design considerations</span></span>

<span data-ttu-id="4e75e-119">Notre plate-forme mobile permet aux applications d’être immersifs avec le contenu de l’application qui occupe tout l’écran, à l’exception de la navigation principale dans Teams.</span><span class="sxs-lookup"><span data-stu-id="4e75e-119">Our mobile platform allows apps to be an immersive experience with the app content taking up all of the screen apart from main Teams navigation.</span></span> <span data-ttu-id="4e75e-120">Pour créer une expérience immersive qui s’intègre à Teams, suivez ces instructions.</span><span class="sxs-lookup"><span data-stu-id="4e75e-120">To create an immersive experience that fits with Teams, follow these guidelines.</span></span>

### <a name="responsive-design"></a><span data-ttu-id="4e75e-121">Conception réactive</span><span class="sxs-lookup"><span data-stu-id="4e75e-121">Responsive design</span></span>

<span data-ttu-id="4e75e-122">Étant donné que votre onglet peut être ouvert sur des appareils avec un large éventail de tailles d’écran, il doit suivre des principes de [conception réactives](https://www.w3schools.com/html/html_responsive.asp) .</span><span class="sxs-lookup"><span data-stu-id="4e75e-122">Because your tab can be opened on devices with a wide range of screen sizes, it needs to follow [responsive design](https://www.w3schools.com/html/html_responsive.asp) principles.</span></span> <span data-ttu-id="4e75e-123">Toutes les constructions clés doivent être accessibles sur les appareils mobiles, et les vues ne doivent pas être déformées.</span><span class="sxs-lookup"><span data-stu-id="4e75e-123">All of the key constructs should be accessible on mobile devices, and the views should not be distorted.</span></span> <span data-ttu-id="4e75e-124">Assurez-vous que, lorsque votre onglet est chargé sur un appareil mobile, tous les boutons et liens sont facilement accessibles à l’aide de la navigation par doigt.</span><span class="sxs-lookup"><span data-stu-id="4e75e-124">Ensure that when your tab is loaded on a mobile device, all buttons and links are easily accessible using finger-based navigation.</span></span>

### <a name="layouts"></a><span data-ttu-id="4e75e-125">Dispositions</span><span class="sxs-lookup"><span data-stu-id="4e75e-125">Layouts</span></span>

<span data-ttu-id="4e75e-126">Le choix de la disposition appropriée pour votre onglet est important.</span><span class="sxs-lookup"><span data-stu-id="4e75e-126">Choosing the correct layout for your tab is important.</span></span> <span data-ttu-id="4e75e-127">Vous devez tenir compte du type d’informations que vous présentez et choisir une mise en page qui l’organise pour une consommation facile.</span><span class="sxs-lookup"><span data-stu-id="4e75e-127">You should consider the kind of information you're presenting, and choose a layout that organizes it for easy consumption.</span></span> <span data-ttu-id="4e75e-128">Certaines options potentielles sont présentées ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="4e75e-128">Some potential options are outlined below.</span></span>

#### <a name="single-canvas"></a><span data-ttu-id="4e75e-129">Seule zone de dessin</span><span class="sxs-lookup"><span data-stu-id="4e75e-129">Single canvas</span></span>

<span data-ttu-id="4e75e-130">Il s’agit d’une grande zone dans laquelle le travail est exécuté.</span><span class="sxs-lookup"><span data-stu-id="4e75e-130">This is one large area where work gets done.</span></span> <span data-ttu-id="4e75e-131">L’application wiki teams suit ce modèle.</span><span class="sxs-lookup"><span data-stu-id="4e75e-131">The Teams Wiki app follows this pattern.</span></span> <span data-ttu-id="4e75e-132">Si vous avez une application qui ne sépare pas le contenu en composants plus petits, il s’agit d’une solution adaptée.</span><span class="sxs-lookup"><span data-stu-id="4e75e-132">If you have an app that doesn’t separate content into smaller components this would be a good fit.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-single-canvas.png" alt-text="Illustration illustrant un onglet de canevas mobile simple Teams." border="false":::

#### <a name="list"></a><span data-ttu-id="4e75e-134">Répertorier</span><span class="sxs-lookup"><span data-stu-id="4e75e-134">List</span></span>

<span data-ttu-id="4e75e-135">Les listes sont idéales pour le tri et le filtrage de grandes quantités de données et sont idéales pour conserver les choses les plus importantes en haut.</span><span class="sxs-lookup"><span data-stu-id="4e75e-135">Lists are great for sorting and filtering large quantities of data and are great at keeping the most important things at the top.</span></span> <span data-ttu-id="4e75e-136">Il est utile d’utiliser des colonnes à trier.</span><span class="sxs-lookup"><span data-stu-id="4e75e-136">It is helpful to use sortable columns.</span></span> <span data-ttu-id="4e75e-137">Les actions peuvent être ajoutées à chaque élément de liste sous le menu points de suspension.</span><span class="sxs-lookup"><span data-stu-id="4e75e-137">Actions can be added to each list item under the ellipsis menu.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-list.png" alt-text="Illustration illustrant un onglet de liste de teams mobile." border="false":::

#### <a name="grid"></a><span data-ttu-id="4e75e-139">Treillis</span><span class="sxs-lookup"><span data-stu-id="4e75e-139">Grid</span></span>

<span data-ttu-id="4e75e-140">Les grilles sont utiles pour afficher des éléments qui sont extrêmement visuels.</span><span class="sxs-lookup"><span data-stu-id="4e75e-140">Grids are useful for showing elements which are highly visual.</span></span> <span data-ttu-id="4e75e-141">Elle permet d’inclure un filtre ou un contrôle de recherche dans la partie supérieure.</span><span class="sxs-lookup"><span data-stu-id="4e75e-141">It helps to include a filter or search control at the top.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-grid.png" alt-text="Illustration illustrant un onglet teams mobile avec une disposition grille." border="false":::

### <a name="tabs-with-bots-on-mobile"></a><span data-ttu-id="4e75e-143">Onglets avec robots sur mobile</span><span class="sxs-lookup"><span data-stu-id="4e75e-143">Tabs with bots on mobile</span></span>

<span data-ttu-id="4e75e-144">L’exemple suivant est une application personnelle qui comporte des onglets et un bot.</span><span class="sxs-lookup"><span data-stu-id="4e75e-144">The following example is a personal app that has tabs and a bot.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-with-bot.png" alt-text="Illustration illustrant la façon dont les applications mobiles teams possèdent des onglets et un bot." border="false":::

## <a name="ui-components"></a><span data-ttu-id="4e75e-146">Composants de l’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="4e75e-146">UI components</span></span>

### <a name="color-palettes"></a><span data-ttu-id="4e75e-147">Palettes de couleurs</span><span class="sxs-lookup"><span data-stu-id="4e75e-147">Color palettes</span></span>

<span data-ttu-id="4e75e-148">L’utilisation de notre palette de couleurs neutre approuvée pour les arrière-plans, les notifications, le texte et les boutons aidera votre application à se sentir plus à la maison dans Teams.</span><span class="sxs-lookup"><span data-stu-id="4e75e-148">Using our approved neutral palette for backgrounds, notifications, text, and buttons will help your app feel more at home in Teams.</span></span> <span data-ttu-id="4e75e-149">Étant donné que teams mobile comporte deux thèmes de couleur (clair et sombre), il est recommandé de s’assurer que votre application paraît belle dans les deux.</span><span class="sxs-lookup"><span data-stu-id="4e75e-149">Since Teams mobile has two colour themes (light and dark), it’s a good idea to make sure your app looks great in both.</span></span>

#### <a name="light-color"></a><span data-ttu-id="4e75e-150">Couleur claire</span><span class="sxs-lookup"><span data-stu-id="4e75e-150">Light color</span></span>

![palette de couleurs claires](../../assets/images/light-color.png)

#### <a name="dark-color"></a><span data-ttu-id="4e75e-152">Couleur foncée</span><span class="sxs-lookup"><span data-stu-id="4e75e-152">Dark color</span></span>

![palette de couleurs sombres](../../assets/images/dark-color.png)

### <a name="buttons-and-controls"></a><span data-ttu-id="4e75e-154">Boutons et contrôles</span><span class="sxs-lookup"><span data-stu-id="4e75e-154">Buttons and controls</span></span>

<span data-ttu-id="4e75e-155">Le style des boutons permet de communiquer le type d’action qu’ils déclenchent.</span><span class="sxs-lookup"><span data-stu-id="4e75e-155">The way buttons are styled helps communicate what kind of action they trigger.</span></span> <span data-ttu-id="4e75e-156">Nous mettons à jour un large éventail de boutons qui sont mis en forme pour afficher différents niveaux de mise en relief.</span><span class="sxs-lookup"><span data-stu-id="4e75e-156">We maintain a wide range of buttons that are formatted to show different levels of emphasis.</span></span> <span data-ttu-id="4e75e-157">Les boutons peuvent contenir du texte, une icône ou une combinaison de texte et d’icône.</span><span class="sxs-lookup"><span data-stu-id="4e75e-157">Buttons can have text, an icon, or a combination of text and an icon.</span></span> <span data-ttu-id="4e75e-158">Pour communiquer différents niveaux dans une hiérarchie, nous avons conçu les boutons principal et secondaire dans chaque catégorie.</span><span class="sxs-lookup"><span data-stu-id="4e75e-158">To communicate different levels in a hierarchy, we designed primary and secondary buttons within each category.</span></span>

#### <a name="buttons"></a><span data-ttu-id="4e75e-159">Boutons</span><span class="sxs-lookup"><span data-stu-id="4e75e-159">Buttons</span></span>

<span data-ttu-id="4e75e-160">Boutons principal et secondaire.</span><span class="sxs-lookup"><span data-stu-id="4e75e-160">Primary and secondary buttons.</span></span>

![image des boutons](../../assets/images/buttons.png)

#### <a name="selection-controls"></a><span data-ttu-id="4e75e-162">Contrôles de sélection</span><span class="sxs-lookup"><span data-stu-id="4e75e-162">Selection controls</span></span>

<span data-ttu-id="4e75e-163">Cases d’option, cases à cocher et basculements.</span><span class="sxs-lookup"><span data-stu-id="4e75e-163">Radio buttons, checkboxes, and toggles.</span></span>

![contrôles de sélection](../../assets/images/selection-controls.png)

#### <a name="chiclets-and-pills"></a><span data-ttu-id="4e75e-165">Chiclets et pilules</span><span class="sxs-lookup"><span data-stu-id="4e75e-165">Chiclets and pills</span></span>

![chiclets et pilules](../../assets/images/chiclets-and-pills.png)

### <a name="typography"></a><span data-ttu-id="4e75e-167">Typographie</span><span class="sxs-lookup"><span data-stu-id="4e75e-167">Typography</span></span>

<span data-ttu-id="4e75e-168">La typographie doit être claire et volontaire.</span><span class="sxs-lookup"><span data-stu-id="4e75e-168">Typography should be clear and purposeful.</span></span> <span data-ttu-id="4e75e-169">Insistez sur les informations importantes et évitez d’utiliser plusieurs polices et tailles pour réduire la confusion.</span><span class="sxs-lookup"><span data-stu-id="4e75e-169">Emphasize important information and avoid using multiple fonts and sizes to reduce confusion.</span></span> <span data-ttu-id="4e75e-170">Nous vous recommandons d’utiliser la casse des phrases et d’éviter l’utilisation de toutes les majuscules pour la localisation et la lisibilité.</span><span class="sxs-lookup"><span data-stu-id="4e75e-170">We recommend using sentence case and avoiding the usage of all caps for localization and legibility.</span></span>

![Typograph mobile](../../assets/images/mobile-typography.png)

### <a name="fields-and-flyouts"></a><span data-ttu-id="4e75e-172">Champs et lanceurs</span><span class="sxs-lookup"><span data-stu-id="4e75e-172">Fields and flyouts</span></span>

<span data-ttu-id="4e75e-173">Les champs sont des zones dans lesquelles les utilisateurs peuvent entrer du texte.</span><span class="sxs-lookup"><span data-stu-id="4e75e-173">Fields are areas where users can input text.</span></span> <span data-ttu-id="4e75e-174">Les lanceurs sont plus légers que les boîtes de dialogue et s’affichent à partir du volet supérieur.</span><span class="sxs-lookup"><span data-stu-id="4e75e-174">Flyouts are more lightweight than dialogs and appear from the top pane.</span></span>

#### <a name="list-controls"></a><span data-ttu-id="4e75e-175">Répertorier les contrôles</span><span class="sxs-lookup"><span data-stu-id="4e75e-175">List controls</span></span>

![contrôles de liste mobile](../../assets/images/mobile-list-controls.png)

#### <a name="field-controls"></a><span data-ttu-id="4e75e-177">contrôles de champs</span><span class="sxs-lookup"><span data-stu-id="4e75e-177">Field controls</span></span>

![contrôles de champ mobiles](../../assets/images/mobile-field-controls.png)

## <a name="developer-considerations"></a><span data-ttu-id="4e75e-179">Considérations pour les développeurs</span><span class="sxs-lookup"><span data-stu-id="4e75e-179">Developer considerations</span></span>

<span data-ttu-id="4e75e-180">Lorsque vous créez une application qui comprend un onglet, vous devez prendre en compte (et tester) le fonctionnement de votre onglet sur les clients Microsoft teams Android et iOS.</span><span class="sxs-lookup"><span data-stu-id="4e75e-180">When you're building an app that includes a tab, you need to consider (and test) how your tab will function on both the Android and iOS Microsoft Teams clients.</span></span> <span data-ttu-id="4e75e-181">Les sections ci-dessous décrivent certains des scénarios clés que vous devez prendre en compte.</span><span class="sxs-lookup"><span data-stu-id="4e75e-181">The sections below outline some of the key scenarios you need to consider.</span></span>

### <a name="testing-on-mobile-clients"></a><span data-ttu-id="4e75e-182">Test sur les clients mobiles</span><span class="sxs-lookup"><span data-stu-id="4e75e-182">Testing on mobile clients</span></span>

<span data-ttu-id="4e75e-183">Vous devez vérifier que votre onglet fonctionne correctement sur les appareils mobiles de différentes tailles et qualités.</span><span class="sxs-lookup"><span data-stu-id="4e75e-183">You need to validate that your tab functions properly on mobile devices of various sizes and qualities.</span></span> <span data-ttu-id="4e75e-184">Pour les appareils Android, vous pouvez utiliser le [devtools](~/tabs/how-to/developer-tools.md) pour déboguer votre onglet pendant qu’il est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="4e75e-184">For Android devices, you can use the [DevTools](~/tabs/how-to/developer-tools.md) to debug your tab while it is running.</span></span> <span data-ttu-id="4e75e-185">Nous vous recommandons de tester sur les périphériques à haute et basse performance, ainsi qu’sur une tablette.</span><span class="sxs-lookup"><span data-stu-id="4e75e-185">We recommend that you test on both high and low performing devices, as well as on a tablet.</span></span>

### <a name="authentication"></a><span data-ttu-id="4e75e-186">Authentification</span><span class="sxs-lookup"><span data-stu-id="4e75e-186">Authentication</span></span>

<span data-ttu-id="4e75e-187">Pour que l’authentification fonctionne sur les clients mobiles, vous devez mettre à niveau teams JavaScript SDK vers la version 1.4.1 au moins.</span><span class="sxs-lookup"><span data-stu-id="4e75e-187">For authentication to work on mobile clients, you must upgrade you Teams JavaScript SDK to at least version 1.4.1.</span></span>

### <a name="low-bandwidth-and-intermittent-connections"></a><span data-ttu-id="4e75e-188">Bande passante faible et connexions intermittentes</span><span class="sxs-lookup"><span data-stu-id="4e75e-188">Low bandwidth and intermittent connections</span></span>

<span data-ttu-id="4e75e-189">Les clients mobiles doivent régulièrement fonctionner avec une faible bande passante et des connexions intermittentes.</span><span class="sxs-lookup"><span data-stu-id="4e75e-189">Mobile clients regularly need to function with low bandwidth and intermittent connections.</span></span> <span data-ttu-id="4e75e-190">Votre application doit gérer les délais d’expiration appropriés en fournissant un message contextuel à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4e75e-190">Your app should handle any timeouts appropriately by providing a contextual message to the user.</span></span> <span data-ttu-id="4e75e-191">Vous devez également indiquer les indicateurs de progression de l’utilisateur pour fournir des commentaires à vos utilisateurs pour tous les processus de longue durée.</span><span class="sxs-lookup"><span data-stu-id="4e75e-191">You should also user progress indicators to provide feedback to your users for any long-running processes.</span></span>
