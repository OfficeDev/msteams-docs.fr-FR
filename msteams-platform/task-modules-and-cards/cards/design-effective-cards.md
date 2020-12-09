---
title: Conception de cartes adaptatives pour votre application
description: Découvrez comment concevoir des cartes adaptatives pour teams et obtenir le kit d’interface utilisateur Microsoft Teams.
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: bd48846284620415cc8cadabc59f2ab7b61d5189
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/09/2020
ms.locfileid: "49604521"
---
# <a name="designing-adaptive-cards-for-your-microsoft-teams-app"></a>Conception de cartes adaptatives pour votre application Microsoft teams

Une carte adaptative contient un corps de forme libre des éléments de carte et un ensemble facultatif d’actions. Les cartes adaptatives sont des extraits de code actionnables, que vous pouvez ajouter à une conversation via un bot ou une extension de messagerie. À l’aide de texte, de graphiques et de boutons, ces cartes fournissent une meilleure communication à votre public.

La structure de carte adaptative est utilisée dans de nombreux produits Microsoft, y compris Teams. Vous pouvez envoyer des cartes à l’intérieur des messages à des utilisateurs via des robots ou des extensions de messagerie. Les utilisateurs peuvent effectuer des actions sur les cartes lorsqu’elles sont présentes.

:::image type="content" source="../../assets/images/adaptive-cards/adaptive-card-overview.png" alt-text="Exemple de carte adaptative." border="false":::

## <a name="microsoft-teams-ui-kit"></a>Kit d’interface utilisateur Microsoft teams

Vous trouverez des instructions de conception plus complètes pour les cartes adaptatives dans Teams, y compris les éléments que vous pouvez saisir et modifier selon vos besoins, dans le kit d’interface utilisateur Microsoft Teams. Le kit d’interface utilisateur aborde également les sujets essentiels tels que les thèmes, l’accessibilité et le dimensionnement réactif.

> [!div class="nextstepaction"]
> [Obtenir le kit d’interface utilisateur Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="adaptive-cards-designer"></a>Concepteur de cartes adaptatives

Vous pouvez également commencer à concevoir vos cartes adaptatives directement dans le navigateur.

> [!div class="nextstepaction"]
> [Essayer le concepteur de cartes adaptatives](https://adaptivecards.io/designer/)

## <a name="types-of-adaptive-cards"></a>Types de cartes adaptatives

### <a name="hero"></a>Hero

Notre plus grande carte. À utiliser pour partager des articles ou des scénarios dans lesquels une image indique la plus grande partie de l’histoire.

:::image type="content" source="../../assets/images/adaptive-cards/hero-card.png" alt-text="Exemple de carte adaptative." border="false":::

### <a name="thumbnail"></a>Thumbnail

Permet d’envoyer un message actionnable simple.

:::image type="content" source="../../assets/images/adaptive-cards/thumbnail-card.png" alt-text="Exemple de carte adaptative." border="false":::

### <a name="list"></a>Répertorier

À utiliser dans les scénarios dans lesquels vous souhaitez que l’utilisateur sélectionne un élément dans une liste, mais les éléments n’ont pas besoin de beaucoup d’explications.

:::image type="content" source="../../assets/images/adaptive-cards/list-card.png" alt-text="Exemple de carte adaptative." border="false":::

### <a name="digest"></a>Digest

À utiliser pour les résumés d’actualité et les billets d’arrondi. Remarque : nous vous recommandons d’utiliser la carte miniature pour une seule mise à jour ou un seul élément d’actualité.

:::image type="content" source="../../assets/images/adaptive-cards/digest-card.png" alt-text="Exemple de carte adaptative." border="false":::

### <a name="media"></a>Multimédia

À utiliser lorsque vous souhaitez combiner du texte et des médias, comme audio ou vidéo.

:::image type="content" source="../../assets/images/adaptive-cards/media-card.png" alt-text="Exemple de carte adaptative." border="false":::

### <a name="people"></a>Contacts

Idéal pour transmettre efficacement les personnes impliquées dans une tâche.

:::image type="content" source="../../assets/images/adaptive-cards/people-card.png" alt-text="Exemple de carte adaptative." border="false":::

### <a name="request-ticket"></a>Demander un ticket

Utilisez pour obtenir des entrées rapides d’un utilisateur afin de créer automatiquement une tâche ou un ticket.

:::image type="content" source="../../assets/images/adaptive-cards/request-ticket-card.png" alt-text="Exemple de carte adaptative." border="false":::

### <a name="imageset"></a>ImageSet

Permet d’envoyer plusieurs miniatures d’image.

:::image type="content" source="../../assets/images/adaptive-cards/image-set-card.png" alt-text="Exemple de carte adaptative." border="false":::

### <a name="actionset"></a>ActionSet

Utilisez cette option lorsque vous souhaitez que l’utilisateur sélectionne un bouton, puis recueille une entrée utilisateur supplémentaire à partir de la même carte.

:::image type="content" source="../../assets/images/adaptive-cards/action-set-card.png" alt-text="Exemple de carte adaptative." border="false":::

### <a name="choiceset"></a>ChoiceSet

Permet de collecter plusieurs entrées de l’utilisateur.

:::image type="content" source="../../assets/images/adaptive-cards/choice-set-card.png" alt-text="Exemple de carte adaptative." border="false":::

## <a name="anatomy"></a>Anatomie

:::image type="content" source="../../assets/images/adaptive-cards/anatomy.png" alt-text="Illustration illustrant l’anatomie de l’interface utilisateur d’une carte adaptative." border="false":::

Les cartes adaptatives offrent une grande flexibilité. Au minimum, nous vous suggérons vivement d’inclure les composants suivants dans chaque carte :

|Compteur|Description|
|----------|-----------|
|A|**En-tête**: rendez les en-têtes claires et concises, mais descriptives.|
|B|**Copie du corps**: permet de transmettre des détails trop longs ou pas suffisamment importants pour être inclus dans l’en-tête.|
|C|**Actions principales**: il est recommandé d’inclure les actions principales 1-3. Un maximum de six est autorisé.|

## <a name="best-practices"></a>Meilleures pratiques

### <a name="primary-and-secondary-actions"></a>Actions principales et secondaires

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-do.png" alt-text="Exemple illustrant une meilleure pratique adaptative de cartes." border="false":::

#### <a name="do-use-up-to-six-primary-actions"></a>Do : utiliser jusqu’à six actions principales

Bien que les cartes adaptatives puissent prendre en charge six actions principales, la plupart des cartes n’en ont pas besoin. Les actions doivent être claires, concises et directes. Moins est plus.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/adaptive-cards/actions-dont.png" alt-text="Exemple illustrant une meilleure pratique adaptative de cartes." border="false":::

#### <a name="dont-use-more-than-six-primary-actions"></a>Ne pas utiliser plus de six actions principales

Les cartes adaptatives doivent présenter un contenu rapide et actionnable. Trop d’actions peuvent inonder un utilisateur.

   :::column-end:::
:::row-end:::

### <a name="frequency"></a>Fréquence

:::image type="content" source="../../assets/images/adaptive-cards/frequency-do.png" alt-text="Exemple illustrant une meilleure pratique adaptative de cartes." border="false":::

#### <a name="do-be-concise"></a>Do : être concis

Il est facile d’envoyer plusieurs cartes dans une conversation, mais une fois que les cartes sortent de l’affichage, elles deviennent moins utiles. Essayez de vous limiter aux notions fondamentales. Cela est particulièrement vrai dans un canal où les utilisateurs ont moins de tolérance pour ce qu’ils perçoivent comme « bruit ».
