---
title: Modifications des marges de l’onglet
author: surbhigupta
description: Décrit comment la suppression des marges d’onglet améliore l’expérience de création d’applications.
keywords: remplissage des marges de suppression de tabulation
ms.topic: reference
ms.localizationpriority: medium
ms.author: lomeybur
ms.openlocfilehash: 79c4d887a028d9da722325985f9bbd62740e3781
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/12/2021
ms.locfileid: "59157006"
---
# <a name="tab-margin-changes"></a>Modifications des marges de l’onglet

Ce document décrit comment la suppression des marges autour de tous les onglets Microsoft Teams améliore l’expérience de création de votre application. Il s’agit d’une amélioration introduite dans Microsoft Teams 2021.
Vous pouvez créer des applications qui semblent plus natives Teams en supprimant les marges autour de tous les onglets. Les onglets avec marges supprimées s’alignent Microsoft Teams conceptions du [kit d’interface utilisateur de Microsoft Teams'](~/tabs/design/tabs.md). La plupart des applications offrent une apparence améliorée sans marges.

:::image type="content" source="../assets/images/tabs/remove-margins-tabs.png" alt-text="Tabulation et sans marges" border="false":::

> [!NOTE]
> Cette fonctionnalité n’est pas applicable aux clients mobiles, car les onglets des clients mobiles n’ont pas de marges. 

## <a name="guidelines"></a>Conseils

La suppression des marges de tabulation affecte Teams applications qui utilisent des onglets. Dans ce cas, vous pouvez ajouter des marges autour de vos conceptions d’onglets lorsque cela est nécessaire. Les conceptions d’applications en production ont un effet de remplissage supplémentaire, c’est-à-dire les marges fournies par les Teams et les marges fournies par l’onglet. Toutefois, l’espacement supplémentaire n’est que temporaire et disparaît dans quelques semaines, ne laissant que le remplissage fourni par l’application.

## <a name="faq"></a>FAQ

**Est-il possible pour le chrome de l’application, comme la barre d’en-tête ou la barre des tâches, d’toucher les bords de nos conceptions ?**

Oui, cela est correct et Teams encourage une telle conception. Cela permet à l’application de se sentir native.

**Est-il possible pour le contenu de l’application, comme le texte, les logos et les images, d’toucher les bords gauche et droit de nos conceptions ?**

Non, vous devez fournir votre propre remplissage ou marges à gauche et à droite de tout le contenu de l’application pour vous assurer qu’il ne touche pas les bords de votre interface utilisateur. Vous pouvez également ajouter des marges en haut de votre onglet, si nécessaire.

**Quelle est la taille des marges de tabulation appliquées Teams précédemment ?**

* Gauche et droite : 20 px
* Haut : 16 px
* Bas : 0px

> [!IMPORTANT]
> * Les marges de tous les onglets sont supprimées : onglets personnels, onglets de conversation (groupe), onglets de réunion et onglets de canal.
> * La modification de suppression de la marge de tabulation s’applique à tous les onglets. Il n’existe aucun moyen d’opter ou de refuser la modification. 
> * La modification des marges de tabulation peut affecter les onglets qui s’appuient sur Microsoft Teams pour fournir des marges autour de leur interface utilisateur.

## <a name="see-also"></a>Voir aussi

* [Teams onglets](~/tabs/what-are-tabs.md)
* [Créer un onglet personnel](~/tabs/how-to/create-personal-tab.md)
* [Créer un onglet de canal ou de groupe](~/tabs/how-to/create-channel-group-tab.md)
* [Onglets sur les appareils mobiles](~/tabs/design/tabs-mobile.md)
