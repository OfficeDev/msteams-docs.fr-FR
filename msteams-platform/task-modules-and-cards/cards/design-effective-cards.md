---
title: Conception de cartes adaptatives pour votre application
description: Découvrez comment concevoir des cartes adaptatives Teams et obtenir le kit Microsoft Teams'interface utilisateur.
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 14ffff1264e716e04a1ffb5549b71a8b7ec5fc14
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101736"
---
# <a name="designing-adaptive-cards-for-your-microsoft-teams-app"></a>Conception de cartes adaptatives pour votre Microsoft Teams application

Une carte adaptative contient un corps libre d'éléments de carte et un ensemble facultatif d'actions. Les cartes adaptatives sont des extraits de contenu actionnables que vous pouvez ajouter à une conversation via un bot ou une extension de messagerie. À l'aide de texte, de graphiques et de boutons, ces cartes offrent une communication enrichie à votre public.

L'infrastructure de carte adaptative est utilisée dans de nombreux produits Microsoft, notamment Teams. Vous pouvez envoyer des cartes dans des messages aux utilisateurs via des bots ou des extensions de messagerie. Les utilisateurs peuvent agir sur des cartes lorsqu'ils sont présents.

:::image type="content" source="../../assets/images/adaptive-cards/adaptive-card-overview.png" alt-text="Exemple de vue d'ensemble d'une carte adaptative." border="false":::

## <a name="microsoft-teams-ui-kit"></a>Kit d’interface utilisateur de Microsoft Teams

Vous trouverez des instructions de conception plus complètes pour les cartes adaptatives dans Teams, y compris les éléments que vous pouvez récupérer et modifier selon vos besoins, dans le Kit d'interface utilisateur Microsoft Teams. Le kit d'interface utilisateur couvre également des sujets essentiels tels que les thèmes, l'accessibilité et le resserrement réactif.

> [!div class="nextstepaction"]
> [Obtenir le Kit d’interface utilisateur de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="adaptive-cards-designer"></a>Concepteur de cartes adaptatives

Vous pouvez également commencer à concevoir vos cartes adaptatives directement dans le navigateur.

> [!div class="nextstepaction"]
> [Essayer le concepteur de cartes adaptatives](https://adaptivecards.io/designer/)

## <a name="types-of-adaptive-cards"></a>Types de cartes adaptatives

### <a name="hero"></a>Hero

Notre carte la plus grande. Permet de partager des articles ou des scénarios où une image indique la majeure partie de l'article.

:::image type="content" source="../../assets/images/adaptive-cards/hero-card.png" alt-text="L'exemple montre une carte hero de carte adaptative." border="false":::

### <a name="thumbnail"></a>Miniature

À utiliser pour envoyer un message actionnable simple.

:::image type="content" source="../../assets/images/adaptive-cards/thumbnail-card.png" alt-text="Exemple de carte miniature carte adaptative." border="false":::

### <a name="list"></a>Répertorier

À utiliser dans les scénarios où vous souhaitez que l'utilisateur sélectionne un élément dans une liste, mais où les éléments n'ont pas besoin d'une grande explication.

:::image type="content" source="../../assets/images/adaptive-cards/list-card.png" alt-text="Exemple de carte de liste carte adaptative." border="false":::

### <a name="digest"></a>Digest

À utiliser pour les résumés d'actualités et les publications d'arrondi. Remarque : nous vous recommandons la carte miniature pour une seule mise à jour ou un élément d'actualités.

:::image type="content" source="../../assets/images/adaptive-cards/digest-card.png" alt-text="L'exemple montre une carte de condensé de carte adaptative." border="false":::

### <a name="media"></a>Support

À utiliser lorsque vous souhaitez combiner du texte et du contenu multimédia, comme l'audio ou la vidéo.

:::image type="content" source="../../assets/images/adaptive-cards/media-card.png" alt-text="Exemple de carte multimédia carte adaptative." border="false":::

### <a name="people"></a>Personnes

Il est préférable de les utiliser pour communiquer efficacement les personnes impliquées dans une tâche.

:::image type="content" source="../../assets/images/adaptive-cards/people-card.png" alt-text="L'exemple montre une carte de visite de carte adaptative." border="false":::

### <a name="request-ticket"></a>Ticket de demande

Permet d'obtenir des entrées rapides d'un utilisateur pour créer automatiquement une tâche ou un ticket.

:::image type="content" source="../../assets/images/adaptive-cards/request-ticket-card.png" alt-text="Exemple de carte de ticket de demande de carte adaptative." border="false":::

### <a name="imageset"></a>ImageSet

Permet d'envoyer plusieurs miniatures d'image.

:::image type="content" source="../../assets/images/adaptive-cards/image-set-card.png" alt-text="L'exemple montre une carte de jeu d'images de carte adaptative." border="false":::

### <a name="actionset"></a>ActionSet

À utiliser lorsque vous souhaitez que l'utilisateur sélectionne un bouton, puis rassemblez des entrées utilisateur à partir de la même carte.

:::image type="content" source="../../assets/images/adaptive-cards/action-set-card.png" alt-text="Exemple de carte de jeu d'actions carte adaptative." border="false":::

### <a name="choiceset"></a>ChoiceSet

Permet de collecter plusieurs entrées de l'utilisateur.

:::image type="content" source="../../assets/images/adaptive-cards/choice-set-card.png" alt-text="Un exemple illustre une carte de choix de carte adaptative." border="false":::

## <a name="anatomy"></a>Anatomie

:::image type="content" source="../../assets/images/adaptive-cards/anatomy.png" alt-text="Exemple de carte d'anatomie de carte adaptative." border="false":::

Les cartes adaptatives offrent beaucoup de flexibilité. Toutefois, nous vous suggérons vivement d'inclure les composants suivants dans chaque carte :

|Compteur|Description|
|----------|-----------|
|A|**En-tête :** rendre les en-têtes clairs et concis, mais descriptifs.|
|B|**Copie du** corps : utilisez cette copie pour transmettre des détails trop longs ou pas assez importants à inclure dans l'en-tête.|
|C|**Actions principales**: en tant que meilleure pratique, incluez 1 à 3 actions principales. Un maximum de six est autorisé.|

## <a name="best-practices"></a>Meilleures pratiques

Utilisez ces recommandations pour créer une expérience d'application de qualité.

### <a name="primary-and-secondary-actions"></a>Actions principales et secondaires

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-do.png" alt-text="Meilleure pratique concernant la façon dont vous devez inclure uniquement un petit ensemble d'actions sur une carte adaptative." border="false":::

#### <a name="do-use-up-to-six-primary-actions"></a>À faire : utiliser jusqu'à six actions principales

Bien que les cartes adaptatives peuvent prendre en charge six actions principales, la plupart des cartes n'en ont pas besoin. Les actions doivent être claires, concises et simples. Moins, c'est plus.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-dont.png" alt-text="Meilleure pratique pour ne pas submerger les utilisateurs d'un trop grand nombre d'actions sur une carte adaptative." border="false":::

#### <a name="dont-use-more-than-six-primary-actions"></a>À ne pas faire : utiliser plus de six actions principales

Les cartes adaptatives doivent présenter un contenu rapide et actionnable. Un trop grand nombre d'actions peut submerger un utilisateur.

   :::column-end:::
:::row-end:::

### <a name="frequency"></a>Fréquence

:::image type="content" source="../../assets/images/adaptive-cards/frequency-do.png" alt-text="Meilleure pratique concernant la fréquence des cartes adaptatives." border="false":::

#### <a name="do-be-concise"></a>À faire : soyez concis

Il est facile d'envoyer plusieurs cartes dans une conversation, mais une fois que les cartes défilent en dehors de la vue, elles deviennent moins utiles. Essayez de vous limiter aux éléments essentiels. Cela est particulièrement vrai dans un canal où les utilisateurs ont moins de tolérance pour ce qu'ils considèrent comme du « bruit ».
