---
title: Conception de votre application personnalisée
author: heath-hamilton
description: Apprenez à concevoir des applications Microsoft Teams’œil. Les ressources comprennent la trousse Microsoft Teams’assurance-chômage, les pratiques exemplaires, les exemples et plus encore.
localization_priority: Normal
ms.author: lajanuar
ms.topic: overview
ms.openlocfilehash: 2f21872bd8c37026528ff6fde282e8c433d5e052
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565115"
---
# <a name="designing-your-microsoft-teams-app"></a>Conception de votre application Microsoft Teams’argent

:::image type="content" source="../../assets/images/design-guidelines-overview.png" alt-text="Image conceptuelle introduisant les Microsoft Teams de conception.":::

Que vous vous disiez designer, chef de produit, développeur ou fabricant à l’aide d’outils à code bas, ces lignes directrices peuvent vous aider à prendre rapidement les bonnes décisions de conception pour votre application Microsoft Teams' argent.

## <a name="teams-app-design-principles"></a>Teams de conception d’applications

Teams applications aident les gens à réaliser plus ensemble. Utilisez ces principes pour guider votre conception.

:::row:::
   :::column span="":::

### <a name="collaborative"></a>collaboratif

Teams applications aident les gens à réaliser plus ensemble. Utilisez ces principes pour guider votre conception.

   :::column-end:::
   :::column span="":::

### <a name="trustworthy"></a>fiable

L’application est sécurisée et conforme. Les utilisateurs peuvent facilement trouver des informations sur la vie privée.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="globally-inclusive"></a>Inclusive à l’échelle mondiale

Les personnes de toutes origines, compétences et disciplines peuvent utiliser l’application. Il est culturellement, racialement et socialement conscient.

   :::column-end:::
   :::column span="":::

### <a name="light"></a>Light

L’application se concentre sur les scénarios de base qui se fondent Teams de travail.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="native-or-distinct"></a>Natif ou distinct

L’application utilise des Teams composants de conception ou les vôtres. Il n’y a aucun mélange de schémas de couleurs, de contrôles, et ainsi de suite.

   :::column-end:::
   :::column span="":::

### <a name="useful"></a>utile

L’application est basée sur un scénario que les gens doivent faire dans Teams.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="easy-to-use"></a>Facile à utiliser

L’interface utilisateur est facile à comprendre, agréable dans le look et le ton, et rend les gens plus productifs.

   :::column-end:::
   :::column span="":::

### <a name="responsive"></a>Réactive

L’application est agnostique de l’appareil et de l’écran.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="accessible"></a>Accessible

L’application répond Teams exigences d’accessibilité en termes de contraste de couleurs, alternatives de navigation, et plus encore.

   :::column-end:::
   :::column span="":::

### <a name="well-described"></a>Bien décrit

Le texte, les icônes et les images montrent clairement à quoi l’application est et comment l’utiliser.

   :::column-end:::
:::row-end:::

## <a name="creating-a-cohesive-experience"></a>Créer une expérience cohérente

Concevoir une Teams appe est comme concevoir une application Web conventionnelle, mais aussi un peu différent. Une conception efficace met en évidence les attributs uniques de votre application tout en s’adaptant naturellement à Teams fonctionnalités et contextes.

Ces lignes directrices et ressources peuvent vous aider à trouver cet équilibre. Vous saurez quoi faire et ce qu’il faut éviter lors de la conception de votre application Teams (comme la navigation à plusieurs niveaux dans un onglet).

## <a name="planning-your-app"></a>Planification de votre application

Pour concevoir une application de haute qualité Teams, vous devez d’abord comprendre ce que vous voulez que votre application fasse et comment vous pensez que les gens vont l’utiliser. Si vous ne l’avez pas déjà fait, prenez le temps de [bien planifier votre application.](../../concepts/extensibility-points.md)

## <a name="design-fundamentals"></a>Fondements de la conception

Apprenez les principes [fondamentaux de la conception Teams’application, y](design-teams-app-fundamentals.md)compris la mise en page, les schémas de couleurs, et plus encore.

## <a name="basic-fluent-ui-components-for-teams"></a>Composants d’interface utilisateur couramment de base pour Teams

Basé sur l’interface utilisateur fluide, ce sont les [éléments de base pour créer des interfaces Teams familiers](design-teams-app-basic-ui-components.md).

## <a name="ui-templates"></a>Modèles d’interface utilisateur

Créez rapidement des designs complexes et haute fidélité avec des [modèles pour les systèmes d’utilisation Teams les cas et les workflows.](design-teams-app-ui-templates.md)

## <a name="app-capabilities"></a>Fonctionnalités de l’application

Comprendre comment les gens ajoutent, utilisent et gèrent Teams applications pour tirer le meilleur parti de chaque fonctionnalité de votre conception.

* [Applications personnelles](../../concepts/design/personal-apps.md)
* [Onglets](../../tabs/design/tabs.md)
* [Extensions de messagerie](../../messaging-extensions/design/messaging-extension-design.md)
* [Bots](../../bots/design/bots.md)
* [Extensions de réunion](../../apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [Modules de tâche](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)
* [Cartes adaptatives](../../task-modules-and-cards/cards/design-effective-cards.md)

## <a name="app-customization"></a>Personnalisation des applications

Comprendre comment l’Teams peut personnaliser ou rebaptiser l’application en fonction des besoins de l’organisation. Cette personnalisation est activée si vous définissez `configurableProperties` le schéma manifeste. Pour plus d’informations, [consultez personnaliser les applications dans Microsoft Teams](/MicrosoftTeams/customize-apps).

> [!NOTE]
> La personnalisation des applications permet aux administrateurs de modifier l’apparence et la sensation des applications chargées par le biais de bots, d’extensions de messagerie, d’onglets et de connecteurs. Par exemple, si l’administrateur Teams personnalise le nom d’une application *de Contoso* *à Contoso Agent*, alors l’application apparaîtra avec le nouveau nom *Contoso Agent* aux utilisateurs. Toutefois, tout en ajoutant un connecteur à un chat, dans la liste les connecteurs afficheront toujours le nom de l’application comme *Contoso*.
> 
> En tant que meilleure pratique, vous devez fournir des directives de personnalisation que les utilisateurs et les clients de l’application doivent suivre lors de la personnalisation de votre application. Pour plus d’informations, [consultez les applications personnalisées dans Microsoft Teams](/MicrosoftTeams/customize-apps).

## <a name="tools-and-samples"></a>Outils et exemples

Les outils suivants peuvent aider les concepteurs et les développeurs à démarrer :

### <a name="microsoft-teams-ui-kit"></a>Kit d’interface utilisateur de Microsoft Teams

Concevez une Teams avec des composants d’interface utilisateur, des modèles et des exemples que vous pouvez faire glisser, déposer et modifier au besoin. Le kit d’interface utilisateur contient également des informations complètes sur la façon dont les applications devraient ressembler et se comporter dans Teams scénarios.

> [!div class="nextstepaction"]
> [Obtenez le kit d’interface utilisateur (Figma)](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a>Microsoft Teams Bibliothèque d’interface utilisateur

Visualisez et testez les Teams d’interface utilisateur et les composants connexes de votre navigateur.

> [!div class="nextstepaction"]
> [Essayez la bibliothèque d’interface utilisateur (aire de jeux)](https://dev-int.teams.microsoft.com/storybook/main/index.html)

Importez ces modèles et composants connexes directement dans votre projet d Teams appe.

> [!div class="nextstepaction"]
> [Obtenez la bibliothèque d’interface utilisateur (GitHub)](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a>Exemple d’application

Installez une application d’exemple pour voir à quoi ressemblent et se comportent les modèles d’interface utilisateur Teams contextes.

> [!div class="nextstepaction"]
> [Obtenez l’exemple d’application (GitHub)](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="other-resources"></a>Autres ressources

Pour en savoir plus, essayez l’une des ressources suivantes :

### <a name="fluent-ui-documentation"></a>Documentation d’interface utilisateur fluide

Obtenez des échantillons de code et des détails de mise en œuvre pour les composants fluent basés sur l’interface utilisateur utilisés pour Teams expériences.

> [!div class="nextstepaction"]
> [Essayez Teams d’interface utilisateur (Interface utilisateur fluide)](https://fluentsite.z22.web.core.windows.net/)

### <a name="adaptive-cards-designer"></a>Concepteur de cartes adaptatives

Concevez des cartes adaptatives dans notre outil web.

> [!div class="nextstepaction"]
> [Essayez le concepteur de cartes adaptatives](https://adaptivecards.io/designer/)
