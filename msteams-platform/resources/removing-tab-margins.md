---
title: Modifications des marges de l’onglet
author: surbhigupta
description: Découvrez comment supprimer les marges autour des onglets dans Microsoft Teams avec le kit d’interface utilisateur. Connaître l’effet de remplissage supplémentaire, la taille de la marge pour gauche, droite, haut et bas.
ms.topic: reference
ms.localizationpriority: medium
ms.author: lomeybur
ms.openlocfilehash: ba203cd89904acde77e1d9971175afc19c47d24d
ms.sourcegitcommit: 9ea9a70d2591bce6b8c980d22014e160f7b45f91
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/02/2022
ms.locfileid: "68820072"
---
# <a name="tab-margin-changes"></a>Modifications des marges de l’onglet

Ce document décrit comment la suppression de marges autour de tous les onglets dans Microsoft Teams améliore votre expérience de création d’applications. Il s’agit d’une amélioration introduite dans Teams en 2021.
Vous pouvez créer des applications qui semblent plus natives à Teams en supprimant les marges autour de tous les onglets. Les onglets avec des marges supprimées s’alignent sur les [conceptions du kit d’interface utilisateur](~/tabs/design/tabs.md) de Microsoft Teams. La plupart des applications présentent une apparence améliorée sans marges.

:::image type="content" source="../assets/images/tabs/remove-margins-tabs.png" alt-text="Esprit tabulation et sans marges":::

> [!NOTE]
> Cette fonctionnalité n’est pas applicable aux clients mobiles, car les onglets affichés dans les clients mobiles n’ont pas de marges.

## <a name="guidelines"></a>Conseils

La suppression des marges d’onglet affecte vos applications Teams qui utilisent des onglets. Dans ce cas, vous pouvez ajouter des marges autour de vos conceptions d’onglets là où cela est nécessaire. Les conceptions d’applications en production ont un effet de remplissage supplémentaire, c’est-à-dire les marges fournies par Teams et les marges fournies par l’onglet. Toutefois, le remplissage supplémentaire n’est que temporaire et disparaît en quelques semaines, ne laissant que le remplissage fourni par l’application.

## <a name="faq"></a>Questions fréquentes (FAQ)

**Est-il acceptable que le chrome d’application, tel que la barre d’en-tête ou la barre des tâches, touche les bords de nos conceptions ?**

Oui, c’est très bien et Teams encourage une telle conception. Cela permet à l’application de se sentir native.

**Le contenu de l’application, tel que le texte, les logos et les images, peut-il toucher les bords gauche et droit de nos conceptions ?**

Non, vous devez fournir vos propres marges ou marges à gauche et à droite de tout le contenu de l’application pour vous assurer qu’il ne touche pas les bords de votre interface utilisateur. Vous pouvez également ajouter des marges en haut de votre onglet, si nécessaire.

**Quelle est la taille des marges d’onglet appliquées précédemment par Teams ?**

* Gauche et droite : 20 pixels
* Haut : 16 pixels
* Bas : 0 pixels

> [!IMPORTANT]
>
> * Tous les onglets ont leurs marges supprimées : onglets personnels, onglets de conversation (de groupe), onglets de réunion et onglets de canal.
> * La modification de la suppression de la marge d’onglet s’applique à tous les onglets. Il n’existe aucun moyen d’accepter ou de refuser la modification.
> * La modification des marges d’onglet peut affecter les onglets qui s’appuient sur Microsoft Teams pour fournir des marges autour de leur interface utilisateur.

## <a name="see-also"></a>Voir aussi

* [Créer des onglets pour Teams](../tabs/what-are-tabs.md)
* [Créer un onglet personnel](../tabs/how-to/create-personal-tab.md)
* [Créer un onglet de canal ou un onglet de groupe](../tabs/how-to/create-channel-group-tab.md)
