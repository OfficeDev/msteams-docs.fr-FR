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
# <a name="fields-and-flyouts"></a>Champs et lanceurs

---

## <a name="fields"></a>Champs

Les champs sont des zones dans lesquelles les utilisateurs peuvent entrer du texte.

### <a name="padding-and-size"></a>Remplissage et taille

Les champs de texte à une seule ligne représentent une hauteur fixe de des pour correspondre à la hauteur des autres composants. Certains champs de texte, tels que les champs de description, peuvent être plus hauts verticalement pour permettre davantage de texte.
[!include[Padding and size](~/includes/design/fields-image-padding.html)]

### <a name="states"></a>États

Voici les États de nos champs de texte. Les champs de texte existent dans différents États. Nous disposons de conceptions spécifiques dédiées à neuf scénarios possibles, y compris (de haut en bas) : zone de texte de repos, clavier en focus et curseur à l’intérieur du champ, clavier activé avec le texte entré, la gestion des erreurs a réussi, la gestion des erreurs a échoué, texte clair champ (y compris une icône X), champ de recherche (y compris une icône de recherche), chargement du champ et champ désactivé.
[!include[Field states](~/includes/design/fields-image-states.html)]

### <a name="formatting-help-text-and-labels"></a>Mise en forme du texte d’aide et des étiquettes

Les champs peuvent contenir un texte d’espace réservé pour donner un exemple du type d’informations requis. Ils peuvent également contenir des étiquettes qui donnent davantage de contexte à l’utilisateur. Dans un champ, votre texte doit toujours être justifié à gauche. Nous utilisons également la casse des phrases ici.

Nous utilisons l’interface utilisateur Segoe standard à 12 pt (légende) et $app-gris-02 pour les étiquettes. Pour le texte d’aide, nous utilisons une interface utilisateur Segoe standard à 14 PT (base) et $app-gris-02.
[!include[Fields typography](~/includes/design/fields-image-typography.html)]

---

## <a name="flyouts"></a>Lanceurs

Les lanceurs sont plus légers que les boîtes de dialogue et peuvent être ignorés rapidement. Ils peuvent contenir des boutons, des champs et d’autres composants.
[!include[Flyouts](~/includes/design/flyouts-image.html)]

### <a name="sizing-and-padding"></a>Dimensionnement et remplissage

Nous recommandons un remplissage 16px à gauche et à droite du contenu.
[!include[Flyouts size and padding](~/includes/design/flyouts-image-sizepadding.html)]

### <a name="placement"></a>Placement

Les lances sont contextuelles et doivent être placées au-dessus, en dessous ou à côté de l’élément qui les a déclenchés.

### <a name="scrolling"></a>Défilement

L’en-tête reste en place pour donner le contexte au contenu en cours de défilement.
[!include[Flyouts scrolling](~/includes/design/flyouts-image-scrolling.html)]

## <a name="mobile"></a>Mobile

Les champs sont des zones de saisie de texte qui acceptent les entrées des utilisateurs. Les menus volants sont des fenêtres contextuelles horizontales qui apparaissent dans le volet de la partie supérieure et peuvent être utilisées pour afficher plus de détails sur un élément.

### <a name="field-controls"></a>Contrôles de champ

[!include[Mobile fields](~/includes/design/fields-mobile-image.html)]

### <a name="flyout-menu-list-controls"></a>Contrôles de liste de menu volant

[!include[Mobile flyout menu controls](~/includes/design/flyout-menu-mobile-image.html)]
