---
title: Conception de votre application personnalisée
author: heath-hamilton
description: Découvrez comment concevoir des applications et des ressources Microsoft Teams, notamment le Kit d’interface utilisateur Microsoft Teams, les meilleures pratiques, des exemples et bien plus encore.
ms.localizationpriority: medium
ms.author: surbhigupta
ms.topic: overview
ms.openlocfilehash: 341c64b2afda7574b6d230257290220e2c97d325
ms.sourcegitcommit: 40d4bde10b6820c62e49e2400b10ab3569c8c815
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/20/2022
ms.locfileid: "68615309"
---
# <a name="designing-your-microsoft-teams-app"></a>Conception de votre application Microsoft Teams

:::image type="content" source="../../assets/images/design-guidelines-overview.png" alt-text="Image conceptuelle présentant les instructions de conception Microsoft Teams.":::

Que vous soyez concepteur, chef de produit, développeur ou créateur à l’aide d’outils à faible code, ces instructions peuvent vous aider à prendre rapidement les bonnes décisions de conception pour votre application Microsoft Teams.

## <a name="creating-a-cohesive-experience"></a>Création d’une expérience cohérente

Concevoir une application Teams revient à concevoir une application web conventionnelle, mais aussi un peu différente. Une conception efficace met en évidence les attributs uniques de votre application tout en s’ajustant naturellement avec les fonctionnalités et les contextes Teams.

Ces lignes directrices et ressources peuvent vous aider à trouver cet équilibre. Vous saurez quoi faire et ce qu’il faut éviter lors de la conception de votre application Teams (par exemple, la navigation à plusieurs niveaux dans un onglet).

## <a name="teams-app-design-principles"></a>Principes de conception des applications Teams

Les applications Teams aident les utilisateurs à aller plus loin ensemble. Utilisez ces principes pour guider votre conception.

:::row:::
   :::column span="":::

### <a name="collaborative"></a>Collaboration

L’application Teams favorise la collaboration par le biais d’activités coordonnées et partagées entre les utilisateurs.

   :::column-end:::
   :::column span="":::

### <a name="trustworthy"></a>Fiable

L’application est sécurisée et conforme. Les utilisateurs peuvent facilement trouver des informations sur la confidentialité.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="globally-inclusive"></a>Globalement inclusif

Les personnes de tous les arrière-plans, ensembles de compétences et disciplines peuvent utiliser l’application. C’est culturellement, racialement et socialement conscient.

   :::column-end:::
   :::column span="":::

### <a name="light"></a>Light

L’application se concentre sur les scénarios de base qui se fondent avec le  flux de travail Teams.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="native-or-distinct"></a>Natif ou distinct

L’application utilise des composants de conception Teams natifs ou les vôtres. Il n’existe aucun mélange de jeux de couleurs, de contrôles, et ainsi de suite.

   :::column-end:::
   :::column span="":::

### <a name="useful"></a>Utile

L’application est basée sur un scénario que les utilisateurs doivent effectuer dans Teams.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="easy-to-use"></a>Simplicité d’utilisation

L’interface utilisateur est facile à comprendre, agréable dans l’apparence et le ton, et rend les gens plus productifs.

   :::column-end:::
   :::column span="":::

### <a name="responsive"></a>Réactif

L’application est indépendante de l’appareil et de l’écran.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="accessible"></a>Accessible

L’application répond aux exigences d’accessibilité de Teams en termes de contraste des couleurs, d’alternatives de navigation, etc.

   :::column-end:::
   :::column span="":::

### <a name="well-described"></a>Bien décrit

Le texte, les icônes et les images indiquent clairement à quoi sert l’application et comment l’utiliser.

   :::column-end:::
:::row-end:::

## <a name="teams-design-system"></a>Système de conception Teams

Découvrez [les principes de base de conception d’application Teams](design-teams-app-fundamentals.md), notamment la disposition, les jeux de couleurs et bien plus encore.

## <a name="app-capabilities"></a>Fonctionnalités de l’application

Découvrez comment les utilisateurs ajoutent, utilisent et gèrent les applications Teams pour tirer le meilleur parti de chaque fonctionnalité de votre conception.

* [Applications personnelles](../../concepts/design/personal-apps.md)
* [Onglets](../../tabs/design/tabs.md)
* [Extensions de messages](../../messaging-extensions/design/messaging-extension-design.md)
* [Bots](../../bots/design/bots.md)
* [Extensions de réunion](../../apps-in-teams-meetings/design/designing-apps-in-meetings.md)

## <a name="ui-templates"></a>Modèles d’interface utilisateur

Créez rapidement des conceptions complexes et haute fidélité avec des [modèles pour les cas d’utilisation et les flux de travail courants Teams](design-teams-app-ui-templates.md).

## <a name="basic-ui-components"></a>Composants d’interface utilisateur de base

En fonction de l’interface utilisateur Fluent, il s’agit des [éléments principaux](design-teams-app-basic-ui-components.md) que vous pouvez utiliser pour créer des expériences Teams à partir de zéro.

## <a name="tools-and-samples"></a>Outils et exemples

Les outils suivants peuvent aider les concepteurs et les développeurs à démarrer :

### <a name="microsoft-teams-ui-kit"></a>Kit d’interface utilisateur de Microsoft Teams

Concevez une application Teams avec des composants d’interface utilisateur, des modèles et des exemples que vous pouvez faire glisser, déplacer et modifier selon vos besoins. Le kit d’interface utilisateur inclut également des informations complètes sur l’apparence et le comportement des applications dans différents scénarios Teams.

> [!div class="nextstepaction"]
> [Obtenir le kit d’interface utilisateur (Figma)](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a>Bibliothèque d’interface utilisateur Microsoft Teams

Affichez et testez des modèles d’interface utilisateur Teams individuels et des composants associés dans votre navigateur.

> [!div class="nextstepaction"]
> [Essayer la bibliothèque d’interface utilisateur (terrain de jeu)](https://dev-int.teams.microsoft.com/storybook/main/index.html)

Importez ces modèles et composants associés directement dans votre projet d’application Teams.

> [!div class="nextstepaction"]
> [Obtenir la bibliothèque d’interface utilisateur (GitHub)](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a>Exemple d’application

Vous pouvez charger un exemple d’application pour voir comment les applications doivent ressembler et se comporter dans le client Teams.

> [!div class="nextstepaction"]
> [Obtenir l’exemple d’application (GitHub)](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="other-resources"></a>Autres ressources

Pour en savoir plus, essayez l’une des ressources suivantes :

### <a name="fluent-ui-documentation"></a>Documentation de l’interface utilisateur Fluent

Obtenez des exemples de code et des détails d’implémentation pour les composants d’interface utilisateur Fluent de base utilisés pour créer des expériences Teams.

> [!div class="nextstepaction"]
> [Essayez Composants interface utilisateur Teams (interface utilisateur Fluent)](https://fluentsite.z22.web.core.windows.net/)

### <a name="adaptive-cards-designer"></a>Concepteur de cartes adaptatives

Concevez des cartes adaptatives dans notre outil web.

> [!div class="nextstepaction"]
> [Essayer le concepteur Cartes adaptatives](https://adaptivecards.io/designer/)

## <a name="see-also"></a>Voir aussi

* [Activer et configurer vos applications pour la phase de réunion](../../apps-in-teams-meetings/build-tabs-for-meeting.md)
* [Conception de votre bot Microsoft Teams](~/bots/design/bots.md)
* [Créer un assistant virtuel](~/samples/virtual-assistant.md)
* [Conception de modules de tâches pour votre application Microsoft Teams](~/task-modules-and-cards/task-modules/design-teams-task-modules.md)
