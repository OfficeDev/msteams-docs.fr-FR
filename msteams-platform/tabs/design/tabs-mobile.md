---
title: Onglets sur les appareils mobiles
description: Décrit les instructions permettant de concevoir des onglets qui fonctionnent sur mobile.
keywords: instructions de conception teams structure de référence des applications personnelles onglets mobiles
ms.openlocfilehash: 6fe40b9cc5b6e898d0f0bce14b3dfedfd2c14032
ms.sourcegitcommit: 61c93b22490526b1de87c0b14a3c7eb6e046caf6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/31/2020
ms.locfileid: "44455519"
---
# <a name="tabs-on-mobile"></a><span data-ttu-id="05c5c-104">Onglets sur les appareils mobiles</span><span class="sxs-lookup"><span data-stu-id="05c5c-104">Tabs on mobile</span></span>

<span data-ttu-id="05c5c-105">Les onglets personnalisés peuvent faire partie d’un canal, d’une conversation de groupe ou d’une application personnelle (applications qui contiennent des onglets statiques et/ou un bot un-à-un).</span><span class="sxs-lookup"><span data-stu-id="05c5c-105">Custom tabs can be part of a channel, group chat, or personal app (apps that contain static tabs and/or a one-to-one bot).</span></span>

<span data-ttu-id="05c5c-106">Les applications personnelles sont disponibles sur les clients mobiles dans le tiroir d’application.</span><span class="sxs-lookup"><span data-stu-id="05c5c-106">Personal apps are available on mobile clients in the App Drawer.</span></span> <span data-ttu-id="05c5c-107">L’application ne peut être installée qu’à partir d’un client de bureau ou Web, et peut prendre jusqu’à 24 heures pour apparaître sur les clients mobiles.</span><span class="sxs-lookup"><span data-stu-id="05c5c-107">The app can only be installed from a desktop or web client, and can take up to 24 hours to appear on mobile clients.</span></span>

<span data-ttu-id="05c5c-108">Les onglets de groupe et de canal sont également disponibles sur les clients mobiles.</span><span class="sxs-lookup"><span data-stu-id="05c5c-108">Group and channel tabs are available on mobile clients as well.</span></span> <span data-ttu-id="05c5c-109">Le comportement par défaut consiste à utiliser votre `websiteUrl` pour lancer votre onglet dans une fenêtre de navigateur.</span><span class="sxs-lookup"><span data-stu-id="05c5c-109">The default behavior is currently to use your `websiteUrl` to launch your tab in a browser window.</span></span> <span data-ttu-id="05c5c-110">Toutefois, ils peuvent être chargés sur un client mobile en cliquant sur le `...` menu de dépassement de capacité en regard de l’onglet et en choisissant **ouvrir**, qui utilisera votre `contentUrl` pour charger l’onglet à l’intérieur du client mobile Teams.</span><span class="sxs-lookup"><span data-stu-id="05c5c-110">However, they can be loaded on a mobile client by clicking the `...` overflow menu next to the tab and choosing **Open**, which will use your `contentUrl` to load the tab inside the Teams mobile client.</span></span>

![tiroir d’application mobile](../../assets/images/personal-app-mobile.png)

## <a name="developer-considerations-for-mobile-support"></a><span data-ttu-id="05c5c-112">Considérations pour les développeurs concernant la prise en charge mobile</span><span class="sxs-lookup"><span data-stu-id="05c5c-112">Developer considerations for mobile support</span></span>

<span data-ttu-id="05c5c-113">Lorsque vous créez une application qui comprend un onglet, vous devez prendre en compte (et tester) le fonctionnement de votre onglet sur les clients Microsoft teams Android et iOS.</span><span class="sxs-lookup"><span data-stu-id="05c5c-113">When you're building an app that includes a tab, you need to consider (and test) how your tab will function on both the Android and iOS Microsoft Teams clients.</span></span> <span data-ttu-id="05c5c-114">Les sections ci-dessous décrivent certains des scénarios clés que vous devez prendre en compte.</span><span class="sxs-lookup"><span data-stu-id="05c5c-114">The sections below outline some of the key scenarios you need to consider.</span></span>

### <a name="testing-on-mobile-clients"></a><span data-ttu-id="05c5c-115">Test sur les clients mobiles</span><span class="sxs-lookup"><span data-stu-id="05c5c-115">Testing on mobile clients</span></span>

<span data-ttu-id="05c5c-116">Vous devez vérifier que votre onglet fonctionne correctement sur les appareils mobiles de différentes tailles et qualités.</span><span class="sxs-lookup"><span data-stu-id="05c5c-116">You need to validate that your tab functions properly on mobile devices of various sizes and qualities.</span></span> <span data-ttu-id="05c5c-117">Pour les appareils Android, vous pouvez utiliser le [devtools](~/tabs/how-to/developer-tools.md) pour déboguer votre onglet pendant qu’il est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="05c5c-117">For Android devices you can use the [DevTools](~/tabs/how-to/developer-tools.md) to debug your tab while it is running.</span></span> <span data-ttu-id="05c5c-118">Nous vous recommandons de tester sur les périphériques à haute et basse performance, ainsi qu’sur une tablette.</span><span class="sxs-lookup"><span data-stu-id="05c5c-118">We recommend that you test on both high and low performing devices, as well as on a tablet.</span></span>

### <a name="responsive-design"></a><span data-ttu-id="05c5c-119">Conception réactive</span><span class="sxs-lookup"><span data-stu-id="05c5c-119">Responsive design</span></span>

<span data-ttu-id="05c5c-120">Étant donné que votre onglet peut être ouvert sur des appareils avec un large éventail de tailles d’écran, il doit suivre des principes de [conception réactives](https://www.w3schools.com/html/html_responsive.asp) .</span><span class="sxs-lookup"><span data-stu-id="05c5c-120">Because your tab can be opened on devices with a wide range of screen sizes, it needs to follow [responsive design](https://www.w3schools.com/html/html_responsive.asp) principles.</span></span> <span data-ttu-id="05c5c-121">Toutes les constructions clés doivent être accessibles sur les appareils mobiles, et les vues ne doivent pas être déformées.</span><span class="sxs-lookup"><span data-stu-id="05c5c-121">All of the key constructs should be accessible on mobile devices, and the views should not be distorted.</span></span> <span data-ttu-id="05c5c-122">Assurez-vous que, lorsque votre onglet est chargé sur un appareil mobile, tous les boutons et liens sont facilement accessibles à l’aide de la navigation par doigt.</span><span class="sxs-lookup"><span data-stu-id="05c5c-122">Ensure that when your tab is loaded on a mobile device, all buttons and links are easily accessible using finger-based navigation.</span></span>

### <a name="authentication"></a><span data-ttu-id="05c5c-123">Authentification</span><span class="sxs-lookup"><span data-stu-id="05c5c-123">Authentication</span></span>

<span data-ttu-id="05c5c-124">Pour que l’authentification fonctionne sur les clients mobiles, vous devez mettre à niveau le kit de développement logiciel (SDK) teams JS vers la version 1.4.1 au moins.</span><span class="sxs-lookup"><span data-stu-id="05c5c-124">For authentication to work on mobile clients, you must upgrade you Teams JS SDK to at least version 1.4.1.</span></span>

### <a name="low-bandwidth--intermittent-connections"></a><span data-ttu-id="05c5c-125">Bande passante faible & les connexions intermittentes</span><span class="sxs-lookup"><span data-stu-id="05c5c-125">Low bandwidth & intermittent connections</span></span>

<span data-ttu-id="05c5c-126">Les clients mobiles doivent régulièrement fonctionner avec une faible bande passante et des connexions intermittentes.</span><span class="sxs-lookup"><span data-stu-id="05c5c-126">Mobile clients regularly need to function with low bandwidth and intermittent connections.</span></span> <span data-ttu-id="05c5c-127">Votre application doit gérer les délais d’expiration appropriés en fournissant un message contextuel à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="05c5c-127">Your app should handle any timeouts appropriately by providing a contextual message to the user.</span></span> <span data-ttu-id="05c5c-128">Vous devez également indiquer les indicateurs de progression de l’utilisateur pour fournir des commentaires à vos utilisateurs pour tous les processus de longue durée.</span><span class="sxs-lookup"><span data-stu-id="05c5c-128">You should also user progress indicators to provide feedback to your users for any long-running processes.</span></span>

## <a name="design-considerations-for-mobile"></a><span data-ttu-id="05c5c-129">Considérations relatives à la conception pour les appareils mobiles</span><span class="sxs-lookup"><span data-stu-id="05c5c-129">Design considerations for mobile</span></span>

<span data-ttu-id="05c5c-130">Notre plate-forme mobile permet aux applications d’être immersifs avec le contenu de l’application qui occupe tout l’écran, à l’exception de la navigation principale dans Teams.</span><span class="sxs-lookup"><span data-stu-id="05c5c-130">Our mobile platform allows apps to be an immersive experience with the app content taking up all of the screen apart from main Teams navigation.</span></span> <span data-ttu-id="05c5c-131">Pour créer une expérience immersive qui s’intègre en toute transparence dans le client Microsoft Teams, suivez les instructions ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="05c5c-131">To create an immersive experience that fits seamlessly within the Microsoft Teams client, follow the guidelines below.</span></span>

### <a name="layouts"></a><span data-ttu-id="05c5c-132">Dispositions</span><span class="sxs-lookup"><span data-stu-id="05c5c-132">Layouts</span></span>

<span data-ttu-id="05c5c-133">Le choix de la disposition appropriée pour votre onglet est important.</span><span class="sxs-lookup"><span data-stu-id="05c5c-133">Choosing the correct layout for your tab is important.</span></span> <span data-ttu-id="05c5c-134">Vous devez tenir compte du type d’informations que vous présentez et choisir une mise en page qui l’organise pour une consommation facile.</span><span class="sxs-lookup"><span data-stu-id="05c5c-134">You should consider the kind of information you're presenting, and choose a layout that organizes it for easy consumption.</span></span> <span data-ttu-id="05c5c-135">Certaines options potentielles sont présentées ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="05c5c-135">Some potential options are outlined below.</span></span>

#### <a name="single-canvas"></a><span data-ttu-id="05c5c-136">Seule zone de dessin</span><span class="sxs-lookup"><span data-stu-id="05c5c-136">Single canvas</span></span>

<span data-ttu-id="05c5c-137">Il s’agit d’une grande zone dans laquelle le travail est exécuté.</span><span class="sxs-lookup"><span data-stu-id="05c5c-137">This is one large area where work gets done.</span></span> <span data-ttu-id="05c5c-138">L’application wiki suit ce modèle.</span><span class="sxs-lookup"><span data-stu-id="05c5c-138">The Wiki app follows this pattern.</span></span> <span data-ttu-id="05c5c-139">Si vous avez une application qui ne sépare pas le contenu en composants plus petits, il s’agit d’une solution adaptée.</span><span class="sxs-lookup"><span data-stu-id="05c5c-139">If you have an app that doesn’t separate content into smaller components this would be a good fit.</span></span>

![disposition sur une seule zone de dessin](~/assets/images/mobile-single-canvas.png)

#### <a name="list"></a><span data-ttu-id="05c5c-141">Répertorier</span><span class="sxs-lookup"><span data-stu-id="05c5c-141">List</span></span>

<span data-ttu-id="05c5c-142">Les listes sont idéales pour le tri et le filtrage de grandes quantités de données et sont idéales pour conserver les choses les plus importantes en haut.</span><span class="sxs-lookup"><span data-stu-id="05c5c-142">Lists are great for sorting and filtering large quantities of data and are great at keeping the most important things at the top.</span></span> <span data-ttu-id="05c5c-143">Il est utile d’utiliser des colonnes à trier.</span><span class="sxs-lookup"><span data-stu-id="05c5c-143">It is helpful to use sortable columns.</span></span> <span data-ttu-id="05c5c-144">Les actions peuvent être ajoutées à chaque élément de liste sous le menu points de suspension.</span><span class="sxs-lookup"><span data-stu-id="05c5c-144">Actions can be added to each list item under the ellipsis menu.</span></span>

![disposition de liste](~/assets/images/mobile-list.png)

#### <a name="grid"></a><span data-ttu-id="05c5c-146">Treillis</span><span class="sxs-lookup"><span data-stu-id="05c5c-146">Grid</span></span>

<span data-ttu-id="05c5c-147">Les grilles sont utiles pour afficher des éléments qui sont extrêmement visuels.</span><span class="sxs-lookup"><span data-stu-id="05c5c-147">Grids are useful for showing elements which are highly visual.</span></span> <span data-ttu-id="05c5c-148">Elle permet d’inclure un filtre ou un contrôle de recherche dans la partie supérieure.</span><span class="sxs-lookup"><span data-stu-id="05c5c-148">It helps to include a filter or search control at the top.</span></span>

![disposition Grille](~/assets/images/mobile-grid.png)

### <a name="tabs-with-bots-on-mobile"></a><span data-ttu-id="05c5c-150">Onglets avec robots sur mobile</span><span class="sxs-lookup"><span data-stu-id="05c5c-150">Tabs with bots on mobile</span></span>

<span data-ttu-id="05c5c-151">Voici un exemple d’application personnelle qui contient deux onglets statiques et un bot.</span><span class="sxs-lookup"><span data-stu-id="05c5c-151">The below is an example personal app that contains two static tabs and a bot.</span></span>

![onglets et bots sur mobile](~/assets/images/mobile-tab-with-bot.png)

### <a name="ui-components"></a><span data-ttu-id="05c5c-153">Composants interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="05c5c-153">UI Components</span></span>

#### <a name="color-palettes"></a><span data-ttu-id="05c5c-154">Palettes de couleurs</span><span class="sxs-lookup"><span data-stu-id="05c5c-154">Color palettes</span></span>

<span data-ttu-id="05c5c-155">L’utilisation de notre palette de couleurs neutre approuvée pour les arrière-plans, les notifications, le texte et les boutons aidera votre application à se sentir plus à la maison dans Teams.</span><span class="sxs-lookup"><span data-stu-id="05c5c-155">Using our approved neutral palette for backgrounds, notifications, text, and buttons will help your app feel more at home in Teams.</span></span> <span data-ttu-id="05c5c-156">Étant donné que teams mobile comporte deux thèmes de couleur (clair et sombre), il est recommandé de s’assurer que votre application paraît belle dans les deux.</span><span class="sxs-lookup"><span data-stu-id="05c5c-156">Since Teams mobile has two colour themes (light and dark), it’s a good idea to make sure your app looks great in both.</span></span>

##### <a name="light-color"></a><span data-ttu-id="05c5c-157">Couleur claire</span><span class="sxs-lookup"><span data-stu-id="05c5c-157">Light color</span></span>

![palette de couleurs claires](~/assets/images/light-color.png)

##### <a name="dark-color"></a><span data-ttu-id="05c5c-159">Couleur foncée</span><span class="sxs-lookup"><span data-stu-id="05c5c-159">Dark color</span></span>

![palette de couleurs sombres](~/assets/images/dark-color.png)

#### <a name="buttons-and-controls"></a><span data-ttu-id="05c5c-161">Boutons et contrôles</span><span class="sxs-lookup"><span data-stu-id="05c5c-161">Buttons and controls</span></span>

<span data-ttu-id="05c5c-162">Le style des boutons permet de communiquer le type d’action qu’ils déclenchent.</span><span class="sxs-lookup"><span data-stu-id="05c5c-162">The way buttons are styled helps communicate what kind of action they trigger.</span></span> <span data-ttu-id="05c5c-163">Nous mettons à jour un large éventail de boutons qui sont mis en forme pour afficher différents niveaux de mise en relief.</span><span class="sxs-lookup"><span data-stu-id="05c5c-163">We maintain a wide range of buttons that are formatted to show different levels of emphasis.</span></span> <span data-ttu-id="05c5c-164">Les boutons peuvent contenir du texte, une icône ou une combinaison de texte et d’icône.</span><span class="sxs-lookup"><span data-stu-id="05c5c-164">Buttons can have text, an icon, or a combination of text and an icon.</span></span> <span data-ttu-id="05c5c-165">Pour communiquer différents niveaux dans une hiérarchie, nous avons conçu les boutons principal et secondaire dans chaque catégorie.</span><span class="sxs-lookup"><span data-stu-id="05c5c-165">To communicate different levels in a hierarchy, we designed primary and secondary buttons within each category.</span></span>

![descendre](~/assets/images/buttons.png)

![contrôles de sélection](~/assets/images/selection-controls.png)

![chiclets et pilules](~/assets/images/chiclets-and-pills.png)

#### <a name="typography"></a><span data-ttu-id="05c5c-169">Typographie</span><span class="sxs-lookup"><span data-stu-id="05c5c-169">Typography</span></span>

<span data-ttu-id="05c5c-170">La typographie doit être claire et volontaire.</span><span class="sxs-lookup"><span data-stu-id="05c5c-170">Typography should be clear and purposeful.</span></span> <span data-ttu-id="05c5c-171">Insistez sur les informations importantes et évitez d’utiliser plusieurs polices et tailles pour réduire la confusion.</span><span class="sxs-lookup"><span data-stu-id="05c5c-171">Emphasize important information and avoid using multiple fonts and sizes to reduce confusion.</span></span> <span data-ttu-id="05c5c-172">Nous vous recommandons d’utiliser la casse des phrases et d’éviter l’utilisation de toutes les majuscules pour la localisation et la lisibilité.</span><span class="sxs-lookup"><span data-stu-id="05c5c-172">We recommend using sentence case and avoiding the usage of all caps for localization and legibility.</span></span>

![Typograph mobile](~/assets/images/mobile-typography.png)

#### <a name="fields-and-flyouts"></a><span data-ttu-id="05c5c-174">Champs et menus volants</span><span class="sxs-lookup"><span data-stu-id="05c5c-174">Fields and Flyouts</span></span>

<span data-ttu-id="05c5c-175">Les champs sont des zones dans lesquelles les utilisateurs peuvent entrer du texte.</span><span class="sxs-lookup"><span data-stu-id="05c5c-175">Fields are areas where users can input text.</span></span> <span data-ttu-id="05c5c-176">Les lanceurs sont plus légers que les boîtes de dialogue et s’affichent dans le volet supérieur.</span><span class="sxs-lookup"><span data-stu-id="05c5c-176">Flyouts are more lightweight than dialogs, and appear from the top pane.</span></span>

##### <a name="list-controls"></a><span data-ttu-id="05c5c-177">Répertorier les contrôles</span><span class="sxs-lookup"><span data-stu-id="05c5c-177">List controls</span></span>

![contrôles de liste mobile](~/assets/images/mobile-list-controls.png)

##### <a name="field-controls"></a><span data-ttu-id="05c5c-179">contrôles de champs</span><span class="sxs-lookup"><span data-stu-id="05c5c-179">Field controls</span></span>

![contrôles de champ mobiles](~/assets/images/mobile-field-controls.png)
