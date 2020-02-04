---
title: Référence des instructions de conception
description: Décrit les instructions relatives à l’utilisation des boîtes de dialogue dans vos applications
keywords: boîtes de dialogue des composants de référence des instructions de conception teams
ms.openlocfilehash: d244eedde66085d41b1f356176a7775de304aaf4
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673616"
---
# <a name="dialogs"></a><span data-ttu-id="34ff8-104">Boîtes de dialogue</span><span class="sxs-lookup"><span data-stu-id="34ff8-104">Dialogs</span></span>

<span data-ttu-id="34ff8-105">Les boîtes de dialogue doivent être utilisées avec parcimonie étant donné qu’elles peuvent être perturbatrices et doivent avoir une façon claire de quitter l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="34ff8-105">Dialogs should be used sparingly since they can be disruptive, and should have a clear way for the user to exit.</span></span>

---

## <a name="sizes"></a><span data-ttu-id="34ff8-106">Quelle</span><span class="sxs-lookup"><span data-stu-id="34ff8-106">Sizes</span></span>

<span data-ttu-id="34ff8-107">Vous pouvez choisir parmi 3 tailles de boîtes de dialogue.</span><span class="sxs-lookup"><span data-stu-id="34ff8-107">We have 3 dialog sizes to choose from.</span></span> <span data-ttu-id="34ff8-108">Choisissez la taille appropriée pour le contenu que vous avez.</span><span class="sxs-lookup"><span data-stu-id="34ff8-108">Choose the size that is appropriate for the content you have.</span></span>
[!include[Dialog sizes](~/includes/design/dialogs-image-sizes.html)]

---

## <a name="buttons"></a><span data-ttu-id="34ff8-109">Boutons</span><span class="sxs-lookup"><span data-stu-id="34ff8-109">Buttons</span></span>

<span data-ttu-id="34ff8-110">Les boutons sont alignés à droite.</span><span class="sxs-lookup"><span data-stu-id="34ff8-110">Buttons are right-justified.</span></span>
<span data-ttu-id="34ff8-111">Tous les autres éléments (cases à cocher, texte d’aide, etc.) doivent être alignés à gauche.</span><span class="sxs-lookup"><span data-stu-id="34ff8-111">All other elements (checkboxes, help text, etc.) should be left-justified.</span></span>
<span data-ttu-id="34ff8-112">Ne dupliquez pas les actions négatives (ne fournissez jamais un « X » et un bouton « Annuler » en même temps.).</span><span class="sxs-lookup"><span data-stu-id="34ff8-112">Don’t duplicate negative actions (Never provide an ‘X’ and a ‘Cancel’ button at the same time.).</span></span>
<span data-ttu-id="34ff8-113">Les boutons « appliquer » doivent être associés à des boutons « Annuler ».</span><span class="sxs-lookup"><span data-stu-id="34ff8-113">‘Apply’ buttons should be paired with ‘Cancel’ buttons.</span></span>
[!include[Dialog buttons](~/includes/design/dialogs-image-buttons.html)]

---

## <a name="scrolling"></a><span data-ttu-id="34ff8-114">Défilement</span><span class="sxs-lookup"><span data-stu-id="34ff8-114">Scrolling</span></span>

<span data-ttu-id="34ff8-115">Dans certains cas, le contenu défile.</span><span class="sxs-lookup"><span data-stu-id="34ff8-115">In some cases, content will scroll.</span></span> <span data-ttu-id="34ff8-116">Le titre de la boîte de dialogue et d’autres informations importantes restent en place.</span><span class="sxs-lookup"><span data-stu-id="34ff8-116">The dialog title and other important information remains in place.</span></span>
[!include[Dialog scrolling](~/includes/design/dialogs-image-scrolling.html)]

---

## <a name="padding"></a><span data-ttu-id="34ff8-117">Remplissage</span><span class="sxs-lookup"><span data-stu-id="34ff8-117">Padding</span></span>

<span data-ttu-id="34ff8-118">Le remplissage des quatre côtés de la boîte de dialogue doit être des.</span><span class="sxs-lookup"><span data-stu-id="34ff8-118">The padding around all four sides of the dialog should be 32px.</span></span>
[!include[Dialog padding](~/includes/design/dialogs-image-padding.html)]

---

## <a name="typography"></a><span data-ttu-id="34ff8-119">Typographie</span><span class="sxs-lookup"><span data-stu-id="34ff8-119">Typography</span></span>

<span data-ttu-id="34ff8-120">Nous utilisons Segoe UI SemiBold sur 18pt (titre 2) et $app-Black pour les titres de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="34ff8-120">We use Segoe UI SemiBold at 18pt (title2) and $app-black for dialog titles.</span></span> <span data-ttu-id="34ff8-121">Pour le corps de texte, nous utilisons l’interface utilisateur Segoe standard sur 14pt (base) et $app-Black.</span><span class="sxs-lookup"><span data-stu-id="34ff8-121">For body text, we use Segoe UI Regular at 14pt (base) and $app-black.</span></span>
[!include[Dialog typography](~/includes/design/dialogs-image-typography.html)]