---
title: Concevoir votre application - Comprendre la structure de l’application
description: Comprenez ce que vous pouvez et ne pouvez pas personnaliser Microsoft Teams lors de la conception de votre application.
author: heath-hamilton
ms.topic: conceptual
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: bf84ad1d52cf46e9242bf4122dc5e900461ab806
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/24/2021
ms.locfileid: "52631309"
---
# <a name="understand-the-microsoft-teams-app-structure"></a>Comprendre la structure Microsoft Teams’application

Lors de la création de votre application, il est important de savoir ce que vous pouvez et ne pouvez pas personnaliser dans Microsoft Teams. Ces informations peuvent vous aider à mieux comprendre les parties de l’expérience d’application que vous contrôlez.

Les images filaire suivantes vous montrent :

* Surfaces que vous pouvez personnaliser dans chaque Teams d’application (en bleu).
* Étendues que chaque fonctionnalité prend en charge.

> [!NOTE]
> **Que signifie l’étendue ?** Une étendue est une zone de Teams où les personnes peuvent utiliser votre application. Les applications peuvent avoir une ou plusieurs étendues, notamment personnelles, des canaux, des conversations et des réunions.

## <a name="personal-apps"></a>Applications personnelles

Les applications personnelles fournissent une grande zone de dessin pour héberger le contenu de votre application pour des utilisateurs individuels. La zone de dessin est un iframe qui vous permet de personnaliser entièrement l’expérience.

***Étendues pris en charge**: Personnel*

:::image type="content" source="../../assets/images/design-guidelines/app-structure-personal-apps.png" alt-text="Image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les applications personnelles." border="false":::

## <a name="tabs"></a>Onglets

Les onglets fournissent une grande zone de dessin pour héberger le contenu de votre application pour un groupe d’utilisateurs. Vous pouvez inclure des onglets dans des espaces partagés tels que des canaux, des conversations et des invitations à des réunions. La zone de dessin est un iframe qui vous permet de personnaliser entièrement l’expérience.

***Étendues pris en charge**: Canaux, Conversations, Réunions*

:::image type="content" source="../../assets/images/design-guidelines/app-structure-tabs.png" alt-text="Image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les onglets." border="false":::

## <a name="bots"></a>Bots

Les bots sont des applications conversationnelles qui s’intègrent Teams fonctionnalités de messagerie native, de sorte que le travail de l’interface utilisateur est géré pour vous. Du point de vue de la conception, il est toujours possible d’ajouter de la personnalité, des fonctionnalités personnalisées et des informations riches et actionnables avec notre prise en charge du traitement du langage naturel (NLP) et la plateforme de cartes adaptatives.

***Étendues pris en charge**: Personnel, Canaux, Conversations, Réunions*

:::image type="content" source="../../assets/images/design-guidelines/app-structure-bots.png" alt-text="Image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les bots." border="false":::

## <a name="messaging-extensions"></a>Extensions de messagerie

Les extensions de messagerie sont des raccourcis pour insérer du contenu d’application ou agir sur un message sans sortir de la conversation. Les extensions de messagerie basées sur l’action vous donnent davantage de contrôle sur l’expérience, tandis que Teams gère la plupart des rendus des extensions de messagerie basées sur la recherche.

***Étendues pris en charge**: Personnel, Canaux, Conversations, Réunions*

:::image type="content" source="../../assets/images/design-guidelines/app-structure-messaging-exetensions.png" alt-text="Image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les extensions de messagerie." border="false":::

## <a name="meeting-extensions"></a>Extensions de réunion

Les extensions de réunion sont des applications pour améliorer les réunions en direct. Vous pouvez héberger le contenu de votre application dans plusieurs scénarios, notamment avant, pendant et après les réunions. La surface est un iframe qui vous permet de personnaliser l’expérience, mais gardez à l’esprit que ces applications sont sombres et étroites pendant les réunions.

***Étendues pris en charge**: réunions, conversations*

:::image type="content" source="../../assets/images/design-guidelines/app-structure-meeting-exetensions.png" alt-text="Image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les extensions de réunion." border="false":::
