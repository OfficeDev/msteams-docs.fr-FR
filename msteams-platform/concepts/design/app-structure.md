---
title: Concevoir votre application - Comprendre la structure de l’application
description: Comprenez ce que vous pouvez et ne pouvez pas personnaliser Microsoft Teams lors de la conception de votre application.
author: heath-hamilton
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: surbhigupta
ms.openlocfilehash: 481ed07682767a303efed50ec06a22cbbb393408
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/12/2021
ms.locfileid: "59156802"
---
# <a name="understand-the-microsoft-teams-app-structure"></a>Comprendre la structure Microsoft Teams’application

Lors de la création de votre application, il est important de savoir ce que vous pouvez et ne pouvez pas personnaliser dans Microsoft Teams. Ces informations peuvent vous aider à mieux comprendre les parties de l’expérience d’application que vous contrôlez.

Les images filaire suivantes vous montrent :

* Surfaces que vous pouvez personnaliser dans chaque Teams d’application (en rose).
* Étendues que chaque fonctionnalité prend en charge.

> [!TIP]
> **Que signifie l’étendue ?** Une étendue est un domaine dans Teams où les personnes peuvent utiliser votre application. Les applications peuvent avoir une ou plusieurs étendues, notamment personnelles, des canaux, des conversations et des réunions.

## <a name="personal-apps"></a>Applications personnelles

Les applications personnelles fournissent une grande zone de dessin pour héberger le contenu de votre application pour des utilisateurs individuels.

***Étendues pris en charge**: Personnel*

### <a name="mobile"></a>Mobile

La zone de dessin est une vue web pour vous aider à personnaliser entièrement l’expérience.

:::image type="content" source="../../assets/images/design-guidelines/app-structure-personal-apps-mobile.png" alt-text="Image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les applications personnelles sur mobile." border="false":::

### <a name="desktop"></a>Bureau

La zone de dessin est un iframe qui vous permet de personnaliser entièrement l’expérience.

:::image type="content" source="../../assets/images/design-guidelines/app-structure-personal-apps-desktop.png" alt-text="Image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les applications personnelles sur ordinateur de bureau." border="false":::

## <a name="tabs"></a>Onglets

Les onglets fournissent une grande zone de dessin pour héberger le contenu de votre application pour un groupe d’utilisateurs. Vous pouvez inclure des onglets dans des espaces partagés tels que des canaux, des conversations et des invitations à des réunions.

***Étendues pris en charge**: Canaux, Conversations, Réunions*

### <a name="mobile"></a>Mobile

La zone de dessin est une vue web pour vous aider à personnaliser entièrement l’expérience.

:::image type="content" source="../../assets/images/design-guidelines/app-structure-tabs-mobile.png" alt-text="Image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les onglets sur appareils mobiles." border="false":::

### <a name="desktop"></a>Bureau

La zone de dessin est un iframe qui vous permet de personnaliser entièrement l’expérience.

:::image type="content" source="../../assets/images/design-guidelines/app-structure-tabs-desktop.png" alt-text="Image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les onglets de bureau." border="false":::

## <a name="bots"></a>Bots

Les bots sont des applications conversationnelles qui s’intègrent Teams fonctionnalités de messagerie native, de sorte que le travail de l’interface utilisateur est géré pour vous. Du point de vue de la conception, il est toujours possible d’ajouter de la personnalité, des fonctionnalités personnalisées et des informations riches et actionnables avec notre prise en charge du traitement du langage naturel (NLP) et la plateforme de cartes adaptatives.

***Étendues pris en charge**: Personnel, Canaux, Conversations, Réunions*

### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/design-guidelines/app-structure-bots-mobile.png" alt-text="Image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les bots sur mobile." border="false":::

### <a name="desktop"></a>Bureau

:::image type="content" source="../../assets/images/design-guidelines/app-structure-bots-desktop.png" alt-text="Image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les bots sur ordinateur de bureau." border="false":::

## <a name="messaging-extensions"></a>Extensions de messagerie

Les extensions de messagerie sont des raccourcis permettant d’insérer du contenu d’application ou agir sur un message sans quitter la conversation. Les extensions de messagerie basées sur l’action vous donnent davantage de contrôle sur l’expérience, tandis que Teams gère la plupart des rendus des extensions de messagerie basées sur la recherche.

***Étendues pris en charge**: Personnel, Canaux, Conversations, Réunions*

### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/design-guidelines/app-structure-messaging-exetensions-mobile.png" alt-text="Image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les extensions de messagerie sur mobile." border="false":::

### <a name="desktop"></a>Bureau

:::image type="content" source="../../assets/images/design-guidelines/app-structure-messaging-exetensions-desktop.png" alt-text="Image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les extensions de messagerie sur ordinateur de bureau." border="false":::

## <a name="meeting-extensions"></a>Extensions de réunion

Les extensions de réunion sont des applications pour améliorer les réunions en direct. Vous pouvez héberger le contenu de votre application dans plusieurs scénarios, notamment avant, pendant et après les réunions.

***Étendues pris en charge**: réunions, conversations*

### <a name="mobile"></a>Mobile

La surface est une vue web, qui vous permet de personnaliser l’expérience, mais gardez à l’esprit que pendant les réunions, ces applications utilisent un thème foncé.

:::image type="content" source="../../assets/images/design-guidelines/app-structure-meeting-exetensions-mobile.png" alt-text="Image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les extensions de réunion sur mobile." border="false":::

### <a name="desktop"></a>Bureau

La surface est un iframe qui vous permet de personnaliser l’expérience, mais n’oubliez pas que pendant les réunions, ces applications utilisent un thème foncé et sont étroites.

:::image type="content" source="../../assets/images/design-guidelines/app-structure-meeting-exetensions-desktop.png" alt-text="Image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les extensions de réunion sur ordinateur de bureau." border="false":::
