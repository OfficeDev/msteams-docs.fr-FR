---
title: Suppression des marges d’onglet dans Microsoft Teams
author: laujan
description: Décrit comment la suppression des marges d’onglet améliorera l’expérience du développeur.
keywords: remplissage des marges de suppression de tabulation
ms.topic: reference
ms.author: lomeybur
ms.openlocfilehash: 87766a40730fdaa2da80c2e0031eab655a993c33
ms.sourcegitcommit: 9cfbc44912980a33d2d7c7c85739aeea6ccb41de
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/05/2021
ms.locfileid: "50479955"
---
# <a name="tab-margin-changes"></a>Modifications apportées aux marges de tabulation

Ce document décrit comment la suppression des marges autour de tous les onglets dans Microsoft Teams améliorera l’expérience du développeur lors de la création d’applications. Il s’agit d’une amélioration introduite dans Microsoft Teams en 2021.
La suppression des marges autour de tous les onglets permettra aux développeurs de créer des applications qui semblent plus natives à Teams. Cela s’alignera également sur nos [conceptions de kit d’interface utilisateur.](~/tabs/design/tabs.md) La plupart des applications ont déjà une meilleure apparence sans les marges qui entourent leur expérience. Toutefois, certains onglets sont visuellement affectés par cette modification, et les développeurs doivent apporter les modifications nécessaires.

:::image type="content" source="../assets/images/tabs/remove-margins-tabs.png" alt-text="Tabulation et sans marges" border="false":::

## <a name="timelines"></a>Chronologies

* 5 mars 2021 - Marges supprimées dans la prévisualisation [publique pour les développeurs.](~/resources/dev-preview/developer-preview-intro.md)
* 1er mai 2021 : les marges seront supprimées en production.

## <a name="guidelines"></a>Conseils

Les applications Microsoft Teams qui utilisent des onglets seront affectées par cette modification. Les développeurs doivent basculer vers [la](~/resources/dev-preview/developer-preview-intro.md) prévisualisation publique pour les développeurs afin de déterminer la façon dont leurs onglets sont affectés et d’apporter les modifications nécessaires.

Les développeurs d’onglets ne doivent pas compter sur Teams pour fournir des marges autour de leurs onglets. Les développeurs sont encouragés à ajouter des marges autour de leurs conceptions d’onglets lorsque cela est nécessaire. Les conceptions d’applications en production peuvent ressembler à un remplissage supplémentaire, c’est-à-dire des marges fournies par Teams et des marges fournies par l’onglet. Toutefois, le remplissage supplémentaire n’est que temporaire et va disparaître dans quelques semaines, ne laissant que le remplissage fourni par l’application.

## <a name="faq"></a>FAQ

**Est-ce que le chrome de l’application, tel que la barre d’en-tête ou la barre des tâches, est autorisé à toucher les bords de nos conceptions ?**

Oui, c’est correct et encouragé. Cela permet à l’application de se sentir native.

**Le contenu de l’application, tel que le texte, les logos et les images, est-il autorisé à toucher les bords gauche et droit de nos conceptions ?**

Non, vous devez fournir votre propre remplissage ou marges à gauche et à droite de tout le contenu de l’application pour vous assurer qu’il ne touche pas les bords de votre interface utilisateur. Vous pouvez également ajouter des marges en haut de votre onglet, si nécessaire.

**Quelle est la taille des marges précédemment appliquées par Teams ?**

* Gauche et droite : 20 px
* Haut : 16 px
* Bas : 0px

> [!IMPORTANT]
> * Les marges de tous les onglets sont supprimées : onglets personnels, onglets de conversation (groupe), onglets de réunion et onglets de canal.
> * Il n’existe aucun moyen d’opter ou de refuser cette modification. Elle s’applique à tous les onglets.
> * Cette modification peut affecter les onglets qui s’appuient sur Microsoft Teams pour fournir des marges autour de leur interface utilisateur.
