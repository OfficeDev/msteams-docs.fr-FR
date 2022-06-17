---
title: Processus de conception des applications
author: heath-hamilton
description: Découvrez comment et quand vous pouvez utiliser les outils et ressources Microsoft pour concevoir une application Microsoft Teams efficace.
ms.localizationpriority: mediums
ms.author: surbhigupta
ms.topic: overview
ms.openlocfilehash: 97ff20e0ffc6cc802c2226cc7767873cd3a25416
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2022
ms.locfileid: "66144375"
---
# <a name="design-process-for-microsoft-teams-apps"></a>Processus de conception des applications Microsoft Teams

Il existe de nombreux outils et ressources pour concevoir votre application Microsoft Teams. Les étapes suivantes décrivent quand et comment vous pouvez les utiliser au cours du processus de conception. (Certaines étapes peuvent être techniquement en dehors du processus de conception mais sont incluses pour un contexte supplémentaire).

:::image type="content" source="~/assets/images/design-guidelines/teams-app-design-process.png" alt-text="Diagramme montrant un exemple du processus de conception d'une application Teams." border="false":::

## <a name="plan-your-app"></a>Programmez votre application

Concevoir une application Teams de haute qualité nécessite de comprendre ce que vous voulez que l’application fasse et comment vous pensez que les gens l’utiliseront. Avant de commencer à concevoir, cependant, répondez aux questions suivantes :

* Qui sont vos utilisateurs ?
* Quel est leur problème ?
* Comment votre application peut-elle résoudre leur problème ?
* À quelle fréquence votre application sera-t-elle utilisée ?
* Combien de personnes utiliseront votre application ?
* Quel type de retour sur investissement votre application peut-elle fournir ?

Pour plus d'informations, consultez [la section Comprendre les cas](~/concepts/design/understand-use-cases.md) d'utilisation[ de votre application et faire correspondre les cas d'utilisation à Teams](~/concepts/design/map-use-cases.md).

## <a name="get-teams-design-tools"></a>Obtenir des outils de conception pour les équipes

Microsoft fournit des outils pour faciliter la conception de votre application Teams. Au minimum, nous vous recommandons vivement d'utiliser le kit d'interface utilisateur de Microsoft Teams.

### <a name="get-the-microsoft-teams-ui-kit"></a>Obtenez le kit d'interface utilisateur de Microsoft Teams

Le kit d'interface utilisateur de Microsoft Teams peut vous aider à développer une application Teams efficace en un minimum de temps. Le kit d'interface utilisateur contient tout ce que vous voyez dans ces documents concernant la conception de l'application Teams et bien plus encore, y compris des exemples et des variantes détaillés.

Le kit d'interface utilisateur comporte également des modèles et des composants préétablis que vous pouvez copier et modifier selon vos besoins. Vous pouvez ainsi consacrer plus de temps à la conception de la meilleure expérience utilisateur au lieu de vous préoccuper de l'aspect d'un bouton.

> [!TIP]
> **Le kit d'interface utilisateur est-il pour moi ?** Si vous avez participé à la création d'une application Teams, oui. Comprendre comment créer une application Teams n'est pas seulement utile aux concepteurs, mais aussi aux chefs de produit, aux développeurs qui utilisent des IDE et aux créateurs qui construisent avec des outils à code réduit (tels que Microsoft Power Plat).

1. Allez [sur la page Figma du kit d'interface utilisateur](https://www.figma.com/community/file/916836509871353159) de Microsoft Teams .
1. Sélectionnez **Duplicate** pour ouvrir le kit d'interface utilisateur. (Vous devrez peut-être d'abord créer un compte Figma).

### <a name="try-the-sample-app"></a>Essayez l'application d'exemple

Vous pouvez télécharger un exemple d'application pour voir comment les applications doivent se présenter et se comporter dans le client Teams.

> [!div class="nextstepaction"]
> [Obtenir l'application d'exemple (GitHub)](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="learn-teams-design-system"></a>Apprendre le système de conception des équipes

Lisez en profondeur ou familiarisez-vous au moins avec les principes fondamentaux de la conception des [applications Teams, notamment la mise en page, les schémas](design-teams-app-fundamentals.md) de couleurs, et plus.

## <a name="choose-app-capabilities"></a>Choisissez les capacités de l'application

Après la phase de planification, vous pouvez déterminer quelles capacités de Teams correspondent aux cas d'utilisation de votre application. Par exemple, si vous souhaitez informer les gens de manière proactive, un robot pourrait être la bonne solution.

Le kit d'interface utilisateur comporte des modèles préétablis qui montrent comment les gens ajoutent, configurent, utilisent et gèrent généralement chaque fonctionnalité. Pour une référence rapide, ces informations se trouvent également dans ces documents, mais avec le kit d'interface utilisateur, vous pouvez copier et coller n'importe lequel de ces modèles dans la conception de votre application.

1. Dans le menu de gauche du kit d'interface, allez dans **Capacités de l'application** et sélectionnez la capacité que vous souhaitez pour votre application.
1. Copiez ce dont vous avez besoin sur cette page pour concevoir votre application.<br />
   Par exemple, si votre application prend en charge l'authentification par signature unique, copiez et collez la conception permettant de gérer ce scénario précis.

## <a name="design-your-ux-flow"></a>Concevoir votre flux UX

Une fois que vous avez conçu une application de base, vous pouvez la modifier et l'affiner autant que vous le souhaitez en copiant les modèles d'interface utilisateur d'équipes et les modèles de base.

### <a name="design-with-ui-templates"></a>Conception avec des modèles d'interface utilisateur

Les modèles d'interface utilisateur sont des conceptions complexes et de haute fidélité pour les cas d'utilisation et les flux de travail courants de Teams. Au lieu de commencer par le bas avec des composants de base, nous vous recommandons d'utiliser ces modèles pour simplifier et accélérer le processus de conception.

1. Dans le menu de gauche du kit d'interface utilisateur, allez dans Modèles **d'interface utilisateur**.
1. Copiez les modèles qui conviennent à la conception de votre application.<br />
   Par exemple, si vous concevez une application personnelle, vous pouvez utiliser un modèle de tableau de bord.

### <a name="design-with-basic-ui-components"></a>Conception avec les composants de base de l'interface utilisateur

Basés sur Fluent UI, ce sont les éléments de base pour créer des interfaces familières pour les équipes. Utilisez ces composants si un modèle d'interface utilisateur manque d'un élément dont vous avez besoin ou si vous souhaitez simplement concevoir votre application à partir de zéro.

1. Dans le menu de gauche du kit d'interface utilisateur, allez dans Composants de **base de l'interface utilisateur**.
1. Copiez les composants dont vous avez besoin pour la conception de votre application (par exemple, un bouton ou une bascule).

## <a name="implement-your-design"></a>Mettez en œuvre votre conception

La conception est terminée et vous êtes prêt à commencer à construire. Les outils suivants peuvent vous aider à simplifier le développement frontal de votre application.

### <a name="build-with-ui-templates"></a>Construire avec des modèles d'interface utilisateur

Si vous avez utilisé des modèles d'interface utilisateur dans votre conception, vous pouvez mettre en œuvre ces modèles avec la bibliothèque d'interface utilisateur de Microsoft Teams (une bibliothèque de composant reposant sur Fluent UI).

Actuellement, tous les modèles figurant dans le kit d'interface utilisateur ne sont pas disponibles dans la bibliothèque.

> [!div class="nextstepaction"]
> [Obtenir la bibliothèque (GitHub)](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="build-with-basic-ui-components"></a>Construire avec des composants d'interface utilisateur de base

Tout comme la phase de conception, vous pouvez utiliser ces composants d'interface utilisateur Fluent dans votre projet d'application si un modèle d'interface utilisateur manque d'un élément dont vous avez besoin, ou si vous voulez simplement construire l'application à partir de zéro. 

(Remarque : si vous remarquez qu'il manque quelque chose ou si vous avez une idée de modèle, pensez à contribuer à la bibliothèque de l'interface utilisateur de Teams).

> [!div class="nextstepaction"]
> [Obtenir la bibliothèque (Fluent UI)](https://fluentsite.z22.web.core.windows.net/)

## <a name="review-design-resources"></a>Examiner les ressources de conception

Que vous commenciez à travailler sur votre application ou que vous soyez sur le point d'avoir une application prête à être mise en production, nous vous recommandons de consulter régulièrement les ressources suivantes :

* **Directives de validation du magasin Microsoft Teams** : Fournit des normes que toutes les applications Teams doivent respecter, et pas seulement les applications répertoriées dans le magasin. Pour plus d’informations, consultez les [consignes](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md).
* **Meilleures pratiques de conception** : Ces documents et le kit d'interface utilisateur fournissent les meilleures pratiques pour concevoir des applications de haute qualité. Par exemple, consultez les [meilleures pratiques pour la conception de robots](~/bots/design/bots.md#best-practices).

## <a name="see-also"></a>Voir aussi

[Conception des notifications du flux d'activités](~/concepts/design/activity-feed-notifications.md)
