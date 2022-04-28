---
title: Concevoir votre application - Comprendre la structure de l’application
description: Découvrez ce que vous pouvez et ne pouvez pas personnaliser dans Microsoft Teams lors de la conception de votre application.
author: heath-hamilton
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: surbhigupta
keywords: Filframe channel chat meeting extensions mobile desktop
ms.openlocfilehash: 8353fa74dce12642e5ca96c85c34dc06fc0da203
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2022
ms.locfileid: "65103284"
---
# <a name="understand-the-microsoft-teams-app-structure"></a>Comprendre la structure de l’application Microsoft Teams

Lors de la création de votre application, il est important de savoir ce que vous pouvez et ne pouvez pas personnaliser dans Microsoft Teams. Ces informations peuvent vous aider à mieux comprendre quelles parties de l’expérience d’application que vous contrôlez.

Les images filaires suivantes vous montrent :

* Surfaces que vous pouvez personnaliser dans chaque fonctionnalité d’application Teams (encadrée en rose).
* Étendues prises en charge par chaque fonctionnalité.

> [!TIP]
> **Que signifie l’étendue ?** Une étendue est une zone de Teams où les utilisateurs peuvent utiliser votre application. Les applications peuvent avoir une ou plusieurs étendues, notamment personnelles, canaux, conversations et réunions.

## <a name="personal-apps"></a>Applications personnelles

Les applications personnelles fournissent un grand canevas pour héberger le contenu de votre application pour les utilisateurs individuels.

***Étendues prises en charge** : Personnel*

### <a name="mobile"></a>Mobile

Le canevas est une vue web qui vous permet de personnaliser complètement l’expérience.

:::image type="content" source="../../assets/images/design-guidelines/app-structure-personal-apps-mobile.png" alt-text="Image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les applications personnelles sur mobile." border="false":::

### <a name="desktop"></a>Ordinateur de bureau

Le canevas est un iframe qui vous permet de personnaliser complètement l’expérience.

:::image type="content" source="../../assets/images/design-guidelines/app-structure-personal-apps-desktop.png" alt-text="Image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les applications personnelles sur le bureau." border="false":::

## <a name="tabs"></a>Onglets

Les onglets fournissent un canevas volumineux pour héberger le contenu de votre application pour un groupe d’utilisateurs. Vous pouvez inclure des onglets dans des espaces partagés tels que des canaux, des conversations et des invitations à des réunions.

***Étendues prises en charge** : canaux, conversations, réunions*

### <a name="mobile"></a>Mobile

Le canevas est une vue web qui vous permet de personnaliser complètement l’expérience.

:::image type="content" source="../../assets/images/design-guidelines/app-structure-tabs-mobile.png" alt-text="Image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les onglets sur mobile." border="false":::

### <a name="desktop"></a>Ordinateur de bureau

Le canevas est un iframe qui vous permet de personnaliser complètement l’expérience.

:::image type="content" source="../../assets/images/design-guidelines/app-structure-tabs-desktop.png" alt-text="Image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les onglets sur le bureau." border="false":::

## <a name="bots"></a>Bots

Les bots sont des applications conversationnelles qui s’intègrent à Teams fonctionnalités de messagerie natives, de sorte que le travail de l’interface utilisateur est géré pour vous. Du point de vue de la conception, il existe toujours des possibilités d’ajouter de la personnalité, des fonctionnalités personnalisées et des informations riches et exploitables avec notre prise en charge du traitement en langage naturel (NLP) et notre plateforme de cartes adaptatives.

***Étendues prises en charge** : Personnel, Canaux, Conversations, Réunions*

### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/design-guidelines/app-structure-bots-mobile.png" alt-text="Image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les bots sur mobile." border="false":::

### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/design-guidelines/app-structure-bots-desktop.png" alt-text="Image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les bots sur le bureau." border="false":::

## <a name="message-extensions"></a>Extensions de message

Les extensions de message sont des raccourcis permettant d’insérer du contenu d’application ou d’agir sur un message sans s’éloigner de la conversation. Les extensions de message basées sur des actions vous permettent de mieux contrôler l’expérience, tandis que Teams gère une grande partie des rendus des extensions de message basées sur la recherche.

***Étendues prises en charge** : Personnel, Canaux, Conversations, Réunions*

### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/design-guidelines/app-structure-messaging-exetensions-mobile.png" alt-text="Image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les extensions de message sur mobile." border="false":::

### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/design-guidelines/app-structure-messaging-exetensions-desktop.png" alt-text="Image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les extensions de message sur le bureau." border="false":::

## <a name="meeting-extensions"></a>Extensions de réunion

Les extensions de réunion sont des applications pour améliorer les réunions en direct. Vous pouvez héberger le contenu de votre application dans plusieurs scénarios, notamment avant, pendant et après les réunions.

***Étendues prises en charge** : Réunions, Conversations*

### <a name="mobile"></a>Mobile

La surface est une vue web, qui vous permet de personnaliser l’expérience, mais gardez à l’esprit que pendant les réunions, ces applications utilisent un thème sombre.

:::image type="content" source="../../assets/images/design-guidelines/app-structure-meeting-exetensions-mobile.png" alt-text="Image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les extensions de réunion sur mobile." border="false":::

### <a name="desktop"></a>Ordinateur de bureau

La surface est un iframe, ce qui vous permet de personnaliser l’expérience, mais gardez à l’esprit que pendant les réunions, ces applications utilisent un thème sombre et sont étroites.

:::image type="content" source="../../assets/images/design-guidelines/app-structure-meeting-exetensions-desktop.png" alt-text="Image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les extensions de réunion sur le bureau." border="false":::
