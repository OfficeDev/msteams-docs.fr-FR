---
title: Concevoir votre application - Comprendre la structure de l’application
description: Découvrez ce que vous pouvez et ne pouvez pas personnaliser dans Microsoft Teams lors de la conception de votre application.
author: heath-hamilton
ms.topic: conceptual
ms.localizationpriority: high
ms.author: surbhigupta
keywords: extensions de message de conversation de canal filaire bureau mobile
ms.openlocfilehash: 5bda408a015c646f993fe2c70efa0b7904b64842
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111380"
---
# <a name="understand-the-microsoft-teams-app-structure"></a>Comprendre la structure de l’application Microsoft Teams

Lors de la création de votre application, il est important de savoir ce que vous pouvez et ne pouvez pas personnaliser dans Microsoft Teams. Ces informations peuvent vous aider à mieux comprendre les parties de l’expérience d’application que vous contrôlez.

Les images filaires suivantes vous montrent :

* Surfaces que vous pouvez personnaliser dans chaque fonctionnalité d’application Teams (encadrée en rose).
* Étendues prises en charge par chaque fonctionnalité.

> [!TIP]
> **Que signifie l’étendue ?** Une étendue est une zone dans Teams où les utilisateurs peuvent utiliser votre application. Les applications peuvent avoir une ou plusieurs étendues, notamment personnelles, canaux, conversations et réunions.

## <a name="personal-apps"></a>Applications personnelles

Les applications personnelles fournissent un canevas volumineux pour héberger le contenu de votre application pour des utilisateurs individuels.

***étendues prises en charge**: Personnel*

### <a name="mobile"></a>Mobile

Le canevas est une vue web qui vous permet de personnaliser complètement l’expérience.

:::image type="content" source="../../assets/images/design-guidelines/app-structure-personal-apps-mobile.png" alt-text="image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les applications personnelles sur mobile." border="false":::

### <a name="desktop"></a>Ordinateur de bureau

Le canevas est un iframe qui vous permet de personnaliser complètement l’expérience.

:::image type="content" source="../../assets/images/design-guidelines/app-structure-personal-apps-desktop.png" alt-text="image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les applications personnelles sur le bureau." border="false":::

## <a name="tabs"></a>Onglets

Les onglets fournissent un canevas volumineux pour héberger le contenu de votre application pour un groupe d’utilisateurs. Vous pouvez inclure des onglets dans des espaces partagés tels que des canaux, des conversations et des invitations à des réunions.

***étendues prises en charge**: canaux, conversations, réunions*

### <a name="mobile"></a>Mobile

Le canevas est une vue web qui vous permet de personnaliser complètement l’expérience.

:::image type="content" source="../../assets/images/design-guidelines/app-structure-tabs-mobile.png" alt-text="image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les onglets sur les appareils mobiles." border="false":::

### <a name="desktop"></a>Ordinateur de bureau

Le canevas est un iframe qui vous permet de personnaliser complètement l’expérience.

:::image type="content" source="../../assets/images/design-guidelines/app-structure-tabs-desktop.png" alt-text="image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les onglets sur le bureau." border="false":::

## <a name="bots"></a>Bots

Les bots sont des applications conversationnelles qui s’intègrent aux fonctionnalités de messagerie natives de Teams, de sorte que le travail de l’interface utilisateur est géré pour vous. Du point de vue de la conception, il existe toujours des opportunités d’ajouter de la personnalité, des fonctionnalités personnalisées et des informations riches et exploitables avec notre prise en charge du traitement en langage naturel (NLP) et notre plateforme Cartes adaptatives.

***étendues prises en charge**: personnel, canaux, conversations, réunions*

### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/design-guidelines/app-structure-bots-mobile.png" alt-text="image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les bots sur mobile." border="false":::

### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/design-guidelines/app-structure-bots-desktop.png" alt-text="image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les bots sur le bureau." border="false":::

## <a name="message-extensions"></a>Extensions de messages

Les extensions de message sont des raccourcis permettant d’insérer du contenu d’application ou d’agir sur un message sans quitter la conversation. Les extensions de message basées sur des actions vous permettent de mieux contrôler l’expérience, tandis que Teams gère une grande partie des rendus des extensions de message basées sur la recherche.

***étendues prises en charge**: personnel, canaux, conversations, réunions*

### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/design-guidelines/app-structure-messaging-exetensions-mobile.png" alt-text="image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les extensions de message sur mobile." border="false":::

### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/design-guidelines/app-structure-messaging-exetensions-desktop.png" alt-text="image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les extensions de message sur le bureau." border="false":::

## <a name="meeting-extensions"></a>Extensions de réunion

Les extensions de réunion sont des applications permettant d’améliorer les réunions en direct. Vous pouvez héberger le contenu de votre application dans plusieurs scénarios, notamment avant, pendant et après les réunions.

***étendues prises en charge**: réunions, conversations*

### <a name="mobile"></a>Mobile

La surface est une vue web qui vous permet de personnaliser l’expérience, mais gardez à l’esprit que pendant les réunions, ces applications utilisent un thème sombre.

:::image type="content" source="../../assets/images/design-guidelines/app-structure-meeting-exetensions-mobile.png" alt-text="image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les extensions de réunion sur mobile." border="false":::

### <a name="desktop"></a>Ordinateur de bureau

La surface est un iframe, ce qui vous permet de personnaliser l’expérience, mais gardez à l’esprit que pendant les réunions, ces applications utilisent un thème sombre et sont étroite.

:::image type="content" source="../../assets/images/design-guidelines/app-structure-meeting-exetensions-desktop.png" alt-text="image conceptuelle montrant les zones frontales dans Teams que les développeurs peuvent personnaliser pour les extensions de réunion sur le bureau." border="false":::
