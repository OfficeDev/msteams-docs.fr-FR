---
title: Conception de Cartes adaptatives pour votre application
description: Découvrez comment concevoir des Cartes adaptatives pour Teams et obtenir le Kit d’interface utilisateur de Microsoft Teams.
localization_priority: Priority
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 28a6b794b9ebae88f8895013f945cbf3b4a91e87
ms.sourcegitcommit: 306b6e8cb3aac8bfda10ef3999467a797d64539d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/20/2021
ms.locfileid: "58408656"
---
# <a name="designing-adaptive-cards-for-your-microsoft-teams-app"></a>Conception de Cartes adaptatives pour votre application Microsoft Teams

Une carte adaptative contient un corps libre d’éléments de carte et un ensemble facultatif d’actions. Les cartes adaptatives sont des extraits de contenu exploitables que vous pouvez ajouter à une conversation par le biais d'un bot ou d'une extension de messagerie. À l’aide de texte, de graphiques et de boutons, ces cartes fournissent une communication enrichie à votre public.

L’infrastructure de carte adaptative est utilisée dans de nombreux produits Microsoft, y compris Teams. Vous pouvez envoyer des cartes à l’intérieur des messages aux utilisateurs via des bots ou des extensions de messagerie. Les utilisateurs peuvent également effectuer des actions sur les cartes lorsqu’ils sont présents.

:::image type="content" source="../../assets/images/adaptive-cards/adaptive-card-overview.png" alt-text="Exemple de vue d’ensemble d’une carte adaptative." border="false":::

## <a name="microsoft-teams-ui-kit"></a>Kit d’interface utilisateur de Microsoft Teams

Vous trouverez des instructions de conception plus complètes pour Cartes adaptatives dans Teams, y compris les éléments que vous pouvez récupérer et modifier en fonction des besoins, dans le Kit d’interface utilisateur Microsoft Teams. Le kit d’interface utilisateur couvre également des sujets essentiels tels que le thème, l’accessibilité et le dimensionnement réactif.

> [!div class="nextstepaction"]
> [Obtenir le Kit d’interface utilisateur de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="adaptive-cards-designer"></a>Concepteur de cartes adaptatives

Vous pouvez également commencer à concevoir vos Cartes adaptatives directement dans le navigateur.

> [!div class="nextstepaction"]
> [Essayer le concepteur Cartes adaptatives](https://adaptivecards.io/designer/)

## <a name="types-of-adaptive-cards"></a>Types de Cartes adaptatives

### <a name="hero"></a>Bannière

Notre carte la plus grande. À utiliser pour partager des articles ou des scénarios où une image indique la plupart de l’histoire.

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/adaptive-cards/mobile-hero-card.png" alt-text="Exemple montrant une carte de bannière de Carte adaptative sur un mobile." border="false":::

#### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/adaptive-cards/hero-card.png" alt-text="Exemple montrant une carte de bannière de Carte adaptative." border="false":::

### <a name="thumbnail"></a>Miniature

Permet d’envoyer un message actionnable simple.

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/adaptive-cards/mobile-thumbnail-card.png" alt-text="Exemple montrant une carte miniature de Carte adaptative sur un mobile." border="false":::

#### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/adaptive-cards/thumbnail-card.png" alt-text="Exemple montrant une carte miniature de Carte adaptative." border="false":::

### <a name="list"></a>Répertorier

Utilisez-le dans les scénarios où vous souhaitez que l’utilisateur choisisse un élément dans une liste, mais que les éléments n’ont pas besoin de beaucoup d’explications.

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/adaptive-cards/mobile-list-card.png" alt-text="Exemple montrant une carte de liste de Carte adaptative sur un mobile." border="false":::

#### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/adaptive-cards/list-card.png" alt-text="Exemple montrant une carte de liste de Carte adaptative." border="false":::

### <a name="digest"></a>Digérer

À utiliser pour les résumés d'actualités et les articles de synthèse. Remarque : nous vous recommandons la carte miniature pour une simple mise à jour ou un élément d’actualités.

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/adaptive-cards/mobile-digest-card.png" alt-text="L’exemple montre une carte de condensé de Carte adaptative sur mobile." border="false":::

#### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/adaptive-cards/digest-card.png" alt-text="L’exemple montre une carte de condensé de Carte adaptative." border="false":::

### <a name="media"></a>Médias

À utiliser lorsque vous souhaitez combiner du texte et des médias, tels que l'audio ou la vidéo.

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/adaptive-cards/mobile-media-card.png" alt-text="Exemple montrant une carte média de Carte adaptative sur mobile." border="false":::

#### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/adaptive-cards/media-card.png" alt-text="Exemple montrant une carte média de Carte adaptative." border="false":::

### <a name="people"></a>Personnes

Meilleure utilisation lorsque vous communiquez efficacement les personnes impliquées dans une tâche.

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/adaptive-cards/mobile-people-card.png" alt-text="Exemple montrant une carte de contacts de Carte adaptative sur mobile." border="false":::

#### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/adaptive-cards/people-card.png" alt-text="Exemple montrant une carte de personnes de Carte adaptative." border="false":::

### <a name="request-ticket"></a>Ticket de demande

Permet d’obtenir des entrées rapides d’un utilisateur pour créer automatiquement une tâche ou un ticket.

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/adaptive-cards/mobile-request-ticket-card.png" alt-text="Exemple montrant une carte de ticket de demande de Carte adaptative sur un mobile." border="false":::

#### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/adaptive-cards/request-ticket-card.png" alt-text="Exemple montrant une carte de ticket de demande de Carte adaptative." border="false":::

### <a name="image-set"></a>Jeu d’images

Permet d’envoyer plusieurs miniatures d’image.

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/adaptive-cards/mobile-image-set-card.png" alt-text="Exemple montrant une carte de jeu d’image de Carte adaptative sur un mobile." border="false":::

#### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/adaptive-cards/image-set-card.png" alt-text="Exemple montrant une carte de jeu d’image de Carte adaptative." border="false":::

### <a name="action-set"></a>Jeu d’actions

Utilisez cette option lorsque vous souhaitez que l’utilisateur sélectionne un bouton, puis recueille d'autres entrées utilisateur sur la même carte.

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/adaptive-cards/mobile-action-set-card.png" alt-text="Exemple montrant une carte de jeu d’action de Carte adaptative sur un appareil mobile." border="false":::

#### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/adaptive-cards/action-set-card.png" alt-text="Exemple montrant une carte de jeu d’action de Carte adaptative." border="false":::

### <a name="choice-set"></a>Ensemble de choix

Permet de collecter plusieurs entrées de l’utilisateur.

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/adaptive-cards/mobile-choice-set-card.png" alt-text="Exemple montrant une carte d’ensemble de choix de Carte adaptative sur un appareil mobile." border="false":::

#### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/adaptive-cards/choice-set-card.png" alt-text="Exemple montrant une carte d’ensemble de choix de Carte adaptative." border="false":::

## <a name="anatomy"></a>Anatomie

Les cartes adaptatives ont une grande flexibilité. Mais au minimum, nous vous suggérons vivement d’inclure les composants suivants dans chaque carte.

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/adaptive-cards/mobile-anatomy.png" alt-text="Exemple illustrant l'anatomie de la Carte adaptative sur un appareil mobile." border="false":::

|Compteur|Description|
|----------|-----------|
|A|**En-tête** : rendez vos en-têtes clairs et concis.|
|B|**Copie du corps** : transmettez des détails trop longs ou pas assez importants pour être inclus dans l’en-tête.|
|C|**Actions principales** : il est recommandé d’inclure entre 1 et 3 actions principales. Un groupe peut comporter jusqu’à six.|

#### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/adaptive-cards/anatomy.png" alt-text="Exemple illustrant l'anatomie de la Carte adaptative." border="false":::

|Compteur|Description|
|----------|-----------|
|A|**En-tête** : rendez vos en-têtes clairs et concis.|
|B|**Copie du corps** : transmettez des détails trop longs ou pas assez importants pour être inclus dans l’en-tête.|
|C|**Actions principales** : il est recommandé d’inclure entre 1 et 3 actions principales. Un groupe peut comporter jusqu’à six.|

## <a name="best-practices"></a>Meilleures pratiques

Utilisez ces recommandations pour créer une expérience d’application de qualité.

### <a name="primary-and-secondary-actions"></a>Actions principales et secondaires

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-do.png" alt-text="Meilleure pratique concernant la façon dont vous ne devez inclure qu’un petit jeu d’actions sur une carte adaptative." border="false":::

#### <a name="do-use-up-to-six-primary-actions"></a>À faire : utiliser jusqu’à six actions principales

Bien que Cartes adaptatives puisse prendre en charge six actions principales, la plupart des cartes n’en ont pas besoin. Les actions doivent être claires, concises et directes. Moins, c’est plus.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-dont.png" alt-text="Meilleure pratique pour ne pas surcharger les utilisateurs avec un trop grand nombre d’actions sur une carte adaptative." border="false":::

#### <a name="dont-use-more-than-six-primary-actions"></a>À ne pas faire : utiliser plus de six actions principales

Les cartes adaptatives doivent présenter un contenu rapide et exploitable. Un trop grand nombre d’actions peut surcharger un utilisateur.

   :::column-end:::
:::row-end:::

### <a name="frequency"></a>Fréquence

:::image type="content" source="../../assets/images/adaptive-cards/frequency-do.png" alt-text="Meilleure pratique concernant la fréquence des cartes adaptatives." border="false":::

#### <a name="do-be-concise"></a>À faire : être concis

Il est facile d’envoyer plusieurs cartes dans une conversation, mais une fois que les cartes défilent hors de l’affichage, elles deviennent moins utiles. Essayez de vous limiter à l’essentiel. Cela est particulièrement vrai dans un canal où les utilisateurs ont moins de tolérance pour ce qu’ils considèrent comme du « bruit ».
