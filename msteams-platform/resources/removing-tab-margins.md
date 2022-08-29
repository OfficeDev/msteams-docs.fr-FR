---
title: Modifications des marges de l’onglet
author: surbhigupta
description: Découvrez comment supprimer des marges autour des onglets dans Microsoft Teams avec le kit d’interface utilisateur. Connaître l’effet de remplissage supplémentaire, la taille de la marge pour la gauche, la droite, le haut et le bas.
ms.topic: reference
ms.localizationpriority: medium
ms.author: lomeybur
ms.openlocfilehash: 715c6b735323e442490de8634384054be565e7a8
ms.sourcegitcommit: 87bba925d005eb331d876a0b9b75154f8100e911
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2022
ms.locfileid: "67450442"
---
# <a name="tab-margin-changes"></a>Modifications des marges de l’onglet

Ce document décrit comment la suppression des marges autour de tous les onglets dans Microsoft Teams améliore l’expérience de création d’applications. Il s’agit d’une amélioration introduite dans Teams en 2021.
Vous pouvez créer des applications qui semblent plus natives pour Teams en supprimant les marges autour de tous les onglets. Les onglets avec les marges supprimées s’alignent sur les [conceptions du kit d’interface utilisateur](~/tabs/design/tabs.md) de Microsoft Teams. La plupart des applications présentent une apparence améliorée sans marges.

:::image type="content" source="../assets/images/tabs/remove-margins-tabs.png" alt-text="Esprit tabulation et sans marges":::

> [!NOTE]
> Cette fonctionnalité n’est pas applicable aux clients mobiles, car les onglets affichés dans les clients mobiles n’ont pas de marges.

## <a name="guidelines"></a>Conseils

La suppression des marges de tabulation affecte vos applications Teams qui utilisent des onglets. Dans ce cas, vous pouvez ajouter des marges autour de vos conceptions d’onglet là où cela est nécessaire. Les conceptions d’applications en production ont un effet de remplissage supplémentaire, c’est-à-dire des marges fournies par Teams et des marges fournies par l’onglet. Toutefois, le remplissage supplémentaire n’est que temporaire et disparaît dans quelques semaines, ne laissant que le remplissage fourni par l’application.

## <a name="faq"></a>FAQ

**Est-il possible que le chrome d’application, tel que la barre d’en-tête ou la barre des tâches, touche les bords de nos conceptions ?**

Oui, c’est correct et Teams encourage ce type de conception. Cela permet à l’application de se sentir native.

**Est-il possible que le contenu de l’application, tel que le texte, les logos et les images, touche les bords gauche et droit de nos conceptions ?**

Non, vous devez fournir votre propre remplissage ou marges à gauche et à droite de tout le contenu de l’application pour vous assurer qu’il ne touche pas les bords de votre interface utilisateur. Vous pouvez également ajouter des marges en haut de votre onglet, si nécessaire.

**Quelle est la taille des marges d’onglet que Teams a appliquées précédemment ?**

* Gauche et droite : 20 pixels
* Haut : 16 pixels
* Bas : 0 pixels

> [!IMPORTANT]
>
> * Les marges de tous les onglets sont supprimées : onglets personnels, onglets de conversation (groupe), onglets de réunion et onglets de canal.
> * La modification de suppression de la marge de tabulation s’applique à tous les onglets. Il n’existe aucun moyen d’accepter ou de refuser la modification.
> * La modification des marges de tabulation peut affecter les onglets qui s’appuient sur Microsoft Teams pour fournir des marges entourant leur interface utilisateur.

## <a name="see-also"></a>Voir aussi

* [Onglets Teams](~/tabs/what-are-tabs.md)
* [Créer un onglet personnel](~/tabs/how-to/create-personal-tab.md)
* [Créer un onglet de canal ou de groupe](~/tabs/how-to/create-channel-group-tab.md)
* [Onglets sur les appareils mobiles](~/tabs/design/tabs-mobile.md)
