---
title: Référence des instructions de conception
description: Décrit les instructions relatives à l’utilisation des champs et des lanceurs dans vos applications
keywords: instructions de conception des équipes références à des champs et des lanceurs
ms.openlocfilehash: 0f62d38bf961ae79b05c599638cefb3c76f46ed4
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673968"
---
# <a name="fields-and-flyouts"></a><span data-ttu-id="30088-104">Champs et lanceurs</span><span class="sxs-lookup"><span data-stu-id="30088-104">Fields and flyouts</span></span>

---

## <a name="fields"></a><span data-ttu-id="30088-105">Champs</span><span class="sxs-lookup"><span data-stu-id="30088-105">Fields</span></span>

<span data-ttu-id="30088-106">Les champs sont des zones dans lesquelles les utilisateurs peuvent entrer du texte.</span><span class="sxs-lookup"><span data-stu-id="30088-106">Fields are areas where users can input text.</span></span>

### <a name="padding-and-size"></a><span data-ttu-id="30088-107">Remplissage et taille</span><span class="sxs-lookup"><span data-stu-id="30088-107">Padding and size</span></span>

<span data-ttu-id="30088-108">Les champs de texte à une seule ligne représentent une hauteur fixe de des pour correspondre à la hauteur des autres composants.</span><span class="sxs-lookup"><span data-stu-id="30088-108">Single-line text fields are a fixed height of 32px to match the height of other components.</span></span> <span data-ttu-id="30088-109">Certains champs de texte, tels que les champs de description, peuvent être plus hauts verticalement pour permettre davantage de texte.</span><span class="sxs-lookup"><span data-stu-id="30088-109">Some text fields such as description fields may be taller vertically to allow more text.</span></span>
[!include[Padding and size](~/includes/design/fields-image-padding.html)]

### <a name="states"></a><span data-ttu-id="30088-110">États</span><span class="sxs-lookup"><span data-stu-id="30088-110">States</span></span>

<span data-ttu-id="30088-111">Voici les États de nos champs de texte.</span><span class="sxs-lookup"><span data-stu-id="30088-111">These are the states of our text fields.</span></span> <span data-ttu-id="30088-112">Les champs de texte existent dans différents États.</span><span class="sxs-lookup"><span data-stu-id="30088-112">Text fields exist in different states.</span></span> <span data-ttu-id="30088-113">Nous disposons de conceptions spécifiques dédiées à neuf scénarios possibles, y compris (de haut en bas) : zone de texte de repos, clavier en focus et curseur à l’intérieur du champ, clavier activé avec le texte entré, la gestion des erreurs a réussi, la gestion des erreurs a échoué, texte clair champ (y compris une icône X), champ de recherche (y compris une icône de recherche), chargement du champ et champ désactivé.</span><span class="sxs-lookup"><span data-stu-id="30088-113">We have specific designs dedicated to nine possible scenarios, including (top to bottom): Resting text field, Keyboard in focus and cursor inside the field, Keyboard in focus with text entered, Error handling has succeeded, Error handling has failed, Clear text field (including an X icon), Search field (including a Search icon), Loading field, and a Disabled field.</span></span>
[!include[Field states](~/includes/design/fields-image-states.html)]

### <a name="formatting-help-text-and-labels"></a><span data-ttu-id="30088-114">Mise en forme du texte d’aide et des étiquettes</span><span class="sxs-lookup"><span data-stu-id="30088-114">Formatting help text and labels</span></span>

<span data-ttu-id="30088-115">Les champs peuvent contenir un texte d’espace réservé pour donner un exemple du type d’informations requis.</span><span class="sxs-lookup"><span data-stu-id="30088-115">Fields can contain placeholder text to give an example of the kind of information that is required.</span></span> <span data-ttu-id="30088-116">Ils peuvent également contenir des étiquettes qui donnent davantage de contexte à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="30088-116">They can also hold labels that give the user more context.</span></span> <span data-ttu-id="30088-117">Dans un champ, votre texte doit toujours être justifié à gauche.</span><span class="sxs-lookup"><span data-stu-id="30088-117">Within a field, your text should always be justified left.</span></span> <span data-ttu-id="30088-118">Nous utilisons également la casse des phrases ici.</span><span class="sxs-lookup"><span data-stu-id="30088-118">We use sentence casing throughout here, as well.</span></span>

<span data-ttu-id="30088-119">Nous utilisons l’interface utilisateur Segoe standard à 12 pt (légende) et $app-gris-02 pour les étiquettes.</span><span class="sxs-lookup"><span data-stu-id="30088-119">We use Segoe UI Regular at 12 pt (caption) and $app-gray-02 for labels.</span></span> <span data-ttu-id="30088-120">Pour le texte d’aide, nous utilisons une interface utilisateur Segoe standard à 14 PT (base) et $app-gris-02.</span><span class="sxs-lookup"><span data-stu-id="30088-120">For help text, we use Segoe UI Regular at 14 pt (base) and $app-gray-02.</span></span>
[!include[Fields typography](~/includes/design/fields-image-typography.html)]

---

## <a name="flyouts"></a><span data-ttu-id="30088-121">Lanceurs</span><span class="sxs-lookup"><span data-stu-id="30088-121">Flyouts</span></span>

<span data-ttu-id="30088-122">Les lanceurs sont plus légers que les boîtes de dialogue et peuvent être ignorés rapidement.</span><span class="sxs-lookup"><span data-stu-id="30088-122">Flyouts are more lightweight than dialogs and can be dismissed quickly.</span></span> <span data-ttu-id="30088-123">Ils peuvent contenir des boutons, des champs et d’autres composants.</span><span class="sxs-lookup"><span data-stu-id="30088-123">They can contain buttons, fields, and other components.</span></span>
[!include[Flyouts](~/includes/design/flyouts-image.html)]

### <a name="sizing-and-padding"></a><span data-ttu-id="30088-124">Dimensionnement et remplissage</span><span class="sxs-lookup"><span data-stu-id="30088-124">Sizing and padding</span></span>

<span data-ttu-id="30088-125">Nous recommandons un remplissage 16px à gauche et à droite du contenu.</span><span class="sxs-lookup"><span data-stu-id="30088-125">We recommend a 16px padding to the left and right of the content.</span></span>
[!include[Flyouts size and padding](~/includes/design/flyouts-image-sizepadding.html)]

### <a name="placement"></a><span data-ttu-id="30088-126">Placement</span><span class="sxs-lookup"><span data-stu-id="30088-126">Placement</span></span>

<span data-ttu-id="30088-127">Les lances sont contextuelles et doivent être placées au-dessus, en dessous ou à côté de l’élément qui les a déclenchés.</span><span class="sxs-lookup"><span data-stu-id="30088-127">Flyouts are contextual and should be placed above, below, or beside the element that triggered it.</span></span>

### <a name="scrolling"></a><span data-ttu-id="30088-128">Défilement</span><span class="sxs-lookup"><span data-stu-id="30088-128">Scrolling</span></span>

<span data-ttu-id="30088-129">L’en-tête reste en place pour donner le contexte au contenu en cours de défilement.</span><span class="sxs-lookup"><span data-stu-id="30088-129">The header remains in place to give context to the content being scrolled.</span></span>
[!include[Flyouts scrolling](~/includes/design/flyouts-image-scrolling.html)]

## <a name="mobile"></a><span data-ttu-id="30088-130">Mobile</span><span class="sxs-lookup"><span data-stu-id="30088-130">Mobile</span></span>

<span data-ttu-id="30088-131">Les champs sont des zones de saisie de texte qui acceptent les entrées des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="30088-131">Fields are text-entry boxes that accept input from users.</span></span> <span data-ttu-id="30088-132">Les menus volants sont des fenêtres contextuelles horizontales qui apparaissent dans le volet de la partie supérieure et peuvent être utilisées pour afficher plus de détails sur un élément.</span><span class="sxs-lookup"><span data-stu-id="30088-132">Flyout menus are horizontal pop-up windows that appear from the top pane and can be used to show more detail about an item.</span></span>

### <a name="field-controls"></a><span data-ttu-id="30088-133">Contrôles de champ</span><span class="sxs-lookup"><span data-stu-id="30088-133">Field Controls</span></span>

[!include[Mobile fields](~/includes/design/fields-mobile-image.html)]

### <a name="flyout-menu-list-controls"></a><span data-ttu-id="30088-134">Contrôles de liste de menu volant</span><span class="sxs-lookup"><span data-stu-id="30088-134">Flyout menu list controls</span></span>

[!include[Mobile flyout menu controls](~/includes/design/flyout-menu-mobile-image.html)]
