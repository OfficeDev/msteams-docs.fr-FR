---
title: Conception de votre application personnalisée
author: heath-hamilton
description: Découvrez comment concevoir des Microsoft Teams applications. Les ressources incluent le kit Microsoft Teams’interface utilisateur, les meilleures pratiques, les exemples et bien plus encore.
localization_priority: Normal
ms.author: lajanuar
ms.topic: overview
ms.openlocfilehash: ab311b6b9b8494308916ef602ee98785ab6de61e
ms.sourcegitcommit: 808a203fb963eeade3a8e32db88d64677e37df7a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/10/2021
ms.locfileid: "52304025"
---
# <a name="designing-your-microsoft-teams-app"></a>Conception de votre application Microsoft Teams web

:::image type="content" source="../../assets/images/design-guidelines-overview.png" alt-text="Image conceptuelle présentant les recommandations Microsoft Teams conception.":::

Que vous êtes concepteur, chef de produit, développeur ou fabricant à l’aide d’outils à code faible, ces instructions peuvent vous aider à prendre rapidement les bonnes décisions en matière de conception pour Microsoft Teams application.

## <a name="teams-app-design-principles"></a>Teams de conception d’application

Teams applications permettent aux gens d’atteindre des objectifs plus réussis. Utilisez ces principes pour guider votre conception.

:::row:::
   :::column span="":::

### <a name="collaborative"></a>Collaboration

Teams applications permettent aux gens d’atteindre des objectifs plus réussis. Utilisez ces principes pour guider votre conception.

   :::column-end:::
   :::column span="":::

### <a name="trustworthy"></a>Fiable

L’application est sécurisée et conforme. Les utilisateurs peuvent facilement trouver des informations sur la confidentialité.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="globally-inclusive"></a>Globalement inclusive

Les personnes de tous horizons, de tous les compétences et de toutes les disciplines peuvent utiliser l’application. Il s’agit d’une approche culturelle, culturelle et sociale.

   :::column-end:::
   :::column span="":::

### <a name="light"></a>Light

L’application se concentre sur les scénarios de base qui se fondent avec Teams flux de travail.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="native-or-distinct"></a>Natif ou distinct

L’application utilise des composants Teams de conception natifs ou les vôtres. Il n’existe aucun mélange de jeux de couleurs, de contrôles, etc.

   :::column-end:::
   :::column span="":::

### <a name="useful"></a>Utile

L’application est basée sur un scénario que les personnes doivent faire dans Teams.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="easy-to-use"></a>Facile à utiliser

L’interface utilisateur est facile à comprendre, agréable en apparence et en ton, et rend les utilisateurs plus productifs.

   :::column-end:::
   :::column span="":::

### <a name="responsive"></a>Réactive

L’application est sans appareil et sans écran.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="accessible"></a>Accessible

L’application répond Teams exigences d’accessibilité en termes de contraste de couleur, d’alternatives de navigation et bien plus encore.

   :::column-end:::
   :::column span="":::

### <a name="well-described"></a>Bien décrit

Le texte, les icônes et les images montrent clairement à quoi l’application s’utilise et comment l’utiliser.

   :::column-end:::
:::row-end:::

## <a name="creating-a-cohesive-experience"></a>Création d’une expérience cohérente

Concevoir une application Teams s’approche de la conception d’une application web conventionnelle, mais également un peu différente. Une conception efficace met en évidence les attributs uniques de votre application tout en s’ajustant naturellement Teams fonctionnalités et contextes.

Ces instructions et ressources peuvent vous aider à trouver cet équilibre. Vous savez ce qu’il faut faire et ce qu’il faut éviter lors de la conception de votre application Teams (par exemple, navigation à plusieurs niveaux dans un onglet).

## <a name="planning-your-app"></a>Planification de votre application

Pour concevoir une application Teams de qualité supérieure, vous devez d’abord comprendre ce que vous voulez que votre application fait et comment vous pensez que les personnes l’utiliseront. Si ce n’est pas déjà fait, prenez le temps de [planifier correctement votre application.](../../concepts/extensibility-points.md)

## <a name="design-fundamentals"></a>Fondements de la conception

Découvrez les [principes de base de Teams conception d’application,](design-teams-app-fundamentals.md)notamment la disposition, les modèles de couleurs, etc.

## <a name="basic-fluent-ui-components-for-teams"></a>Composants d’interface utilisateur Fluent de base pour Teams

Basés sur l’interface utilisateur Fluent, ce sont les éléments de base pour créer des [interfaces Teams familières.](design-teams-app-basic-ui-components.md)

## <a name="ui-templates"></a>Modèles d’interface utilisateur

Créez rapidement des conceptions complexes et haute fidélité avec des modèles pour les Teams et les flux [de travail.](design-teams-app-ui-templates.md)

## <a name="app-capabilities"></a>Fonctionnalités de l’application

Comprendre comment les personnes ajoutent, utilisent et gèrent Teams applications pour utiliser au mieux chaque fonctionnalité de votre conception.

* [Applications personnelles](../../concepts/design/personal-apps.md)
* [Onglets](../../tabs/design/tabs.md)
* [Extensions de messagerie](../../messaging-extensions/design/messaging-extension-design.md)
* [Bots](../../bots/design/bots.md)
* [Extensions de réunion](../../apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [Modules de tâche](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)
* [Cartes adaptatives](../../task-modules-and-cards/cards/design-effective-cards.md)

## <a name="app-customization"></a>Personnalisation de l’application

Comprendre comment l’administrateur Teams peut personnaliser ou renommer l’application en fonction des besoins de l’organisation. Cette personnalisation est activée si vous définissez le `configurableProperties` schéma de manifeste. Pour plus d’informations, voir [Personnaliser les applications dans Microsoft Teams](/MicrosoftTeams/customize-apps).

> [!NOTE]
> La personnalisation d’application permet aux administrateurs de modifier l’apparence des applications chargées par le biais de bots, d’extensions de messagerie, d’onglets et de connecteurs. Par exemple, si l’administrateur Teams personnalise le nom d’une application de *Contoso* à *Agent Contoso,* l’application apparaît sous le nouveau nom *Agent Contoso* pour les utilisateurs. Toutefois, lors de l’ajout d’un connecteur à une conversation, dans la liste, les connecteurs afficheront toujours le nom de l’application en tant *que Contoso*.
> 
> En tant que meilleure pratique, vous devez fournir des instructions de personnalisation que les utilisateurs et les clients de l’application doivent suivre lors de la personnalisation de votre application. Pour plus d’informations, voir [personnaliser les applications dans Microsoft Teams](/MicrosoftTeams/customize-apps).

## <a name="tools-and-samples"></a>Outils et exemples

Les outils suivants peuvent aider les concepteurs et les développeurs à démarrer :

### <a name="microsoft-teams-ui-kit"></a>Kit d’interface utilisateur de Microsoft Teams

Concevez une Teams avec des composants d’interface utilisateur, des modèles et des exemples que vous pouvez faire glisser, déposer et modifier selon vos besoins. Le kit d’interface utilisateur inclut également des informations complètes sur l’apparence et le comportement des applications dans Teams différents scénarios.

> [!div class="nextstepaction"]
> [Obtenir le kit d’interface utilisateur (Figma)](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a>Microsoft Teams Bibliothèque d’interface utilisateur

Affichez et testez les Teams d’interface utilisateur et les composants associés dans votre navigateur.

> [!div class="nextstepaction"]
> [Essayer la bibliothèque d’interface utilisateur (aire de jeu)](https://dev-int.teams.microsoft.com/storybook/main/index.html)

Importez ces modèles et composants associés directement dans Teams projet d’application.

> [!div class="nextstepaction"]
> [Obtenir la bibliothèque d’interface utilisateur (GitHub)](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a>Exemple d’application

Installez un exemple d’application pour voir l’apparence et le comportement des modèles d’interface utilisateur Teams contextes.

> [!div class="nextstepaction"]
> [Obtenir l’exemple d’application (GitHub)](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="other-resources"></a>Autres ressources

Pour en savoir plus, essayez l’une des ressources suivantes.

### <a name="fluent-ui-documentation"></a>Documentation de l’interface utilisateur Fluent

Obtenez des exemples de code et des détails d’implémentation pour les composants Fluent UI utilisés pour créer des expériences Teams utilisateur.

> [!div class="nextstepaction"]
> [Essayer Teams composants d’interface utilisateur (interface utilisateur Fluent)](https://fluentsite.z22.web.core.windows.net/)

### <a name="adaptive-cards-designer"></a>Concepteur de cartes adaptatives

Concevez des cartes adaptatives dans notre outil web.

> [!div class="nextstepaction"]
> [Essayer le concepteur de cartes adaptatives](https://adaptivecards.io/designer/)
