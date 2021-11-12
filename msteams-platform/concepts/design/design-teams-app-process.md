---
title: Processus de conception d’application
author: heath-hamilton
description: Obtenez une idée générale de la façon dont vous pouvez utiliser les outils et les ressources Microsoft pour concevoir une application Microsoft Teams efficace.
ms.localizationpriority: medium
ms.author: surbhigupta
ms.topic: overview
ms.openlocfilehash: 95af942973b25a085662eb303077dff6cba815e5
ms.sourcegitcommit: 781f34af2a95952bf437d0b7236ae995f4e14a08
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/12/2021
ms.locfileid: "60948599"
---
# <a name="design-process-for-microsoft-teams-apps"></a>Processus de conception pour Microsoft Teams applications

Il existe plusieurs outils et ressources pour concevoir votre application Microsoft Teams web. Les étapes suivantes décrivent quand et comment vous pouvez les utiliser pendant le processus de conception. (Certaines étapes peuvent être techniquement en dehors du processus de conception, mais sont incluses pour un contexte supplémentaire.)

:::image type="content" source="~/assets/images/design-guidelines/teams-app-design-process.png" alt-text="Diagramme montrant un exemple du processus Teams conception d’application." border="false":::

## <a name="plan-your-app"></a>Planifier votre application

La conception d’une application Teams qualité nécessite de comprendre ce que vous souhaitez que l’application fait et la façon dont vous pensez que les personnes l’utiliseront. Toutefois, avant de commencer la conception, répondez aux questions suivantes :

* Qui sont vos utilisateurs ?
* Quel est leur problème ?
* Comment votre application peut-elle résoudre son problème ?
* À quelle fréquence votre application sera-t-elle utilisée ?
* Combien de personnes utiliseront votre application ?
* Quel type de retour sur investissement votre application peut-elle fournir ?

Pour plus d’informations, voir [comprendre les cas d’utilisation](~/concepts/design/understand-use-cases.md) de votre application et les ma [Teams](~/concepts/design/map-use-cases.md).

## <a name="get-teams-design-tools"></a>Obtenir les Teams de conception

Microsoft fournit des outils pour faciliter la conception de votre Teams application. Au minimum, nous vous recommandons vivement d’utiliser Microsoft Teams kit d’interface utilisateur.

### <a name="get-the-microsoft-teams-ui-kit"></a>Obtenir le kit Microsoft Teams’interface utilisateur

Le kit Microsoft Teams’interface utilisateur peut vous aider à développer une application Teams efficace dans un délai le plus court. Le kit d’interface utilisateur contient tout ce que vous voyez dans ces documents relatifs Teams conception d’application et bien plus encore, notamment des exemples complets et des variantes.

Le kit d’interface utilisateur dispose également de modèles et de composants pré-créés que vous pouvez copier et modifier selon vos besoins. Ainsi, vous pouvez passer plus de temps à concevoir la meilleure expérience utilisateur au lieu de vous soucier de l’apparence d’un bouton.

> [!TIP]
> **Le kit d’interface utilisateur est-il pour moi ?** Si vous avez une partie de la création d’une Teams, oui. Comprendre comment créer une application Teams n’est pas seulement utile aux concepteurs, mais également aux responsables de produits, aux développeurs qui utilisent des IDE et aux créateurs de création avec des outils à code faible (par exemple, Microsoft Power Platform).

1. Go to the [Microsoft Teams UI Kit Figma page](https://www.figma.com/community/file/916836509871353159).
1. Sélectionnez **Dupliquer** pour ouvrir le kit d’interface utilisateur. (Vous de devez d’abord créer un compte Figma.)

### <a name="try-the-sample-app"></a>Essayer l’exemple d’application

Vous pouvez télécharger un exemple d’application pour voir l’apparence et le comportement des applications dans Teams client.

> [!div class="nextstepaction"]
> [Obtenir l’exemple d’application (GitHub)](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="learn-teams-design-system"></a>En savoir Teams du système de conception

Lisez en détail ou familiarisez-vous au moins avec les principes de base de Teams [conception](design-teams-app-fundamentals.md)d’application, notamment la disposition, les modèles de couleurs, etc.

## <a name="choose-app-capabilities"></a>Choisir les fonctionnalités de l’application

Après la phase de planification, vous pouvez déterminer les fonctionnalités Teams adaptées aux cas d’utilisation de votre application. Par exemple, si vous souhaitez avertir les personnes de manière proactive, un bot peut être la bonne fonctionnalité.

Le kit d’interface utilisateur comprend des conceptions pré-conçues qui vous montrent comment les utilisateurs ajoutent, définissent, utilisent et gèrent généralement chaque fonctionnalité. Pour référence rapide, ces informations se trouve également dans ces documents, mais avec le kit d’interface utilisateur, vous pouvez copier et coller l’une de ces conceptions dans la conception de votre application.

1. Dans le navigation gauche du kit  d’interface utilisateur, sélectionnez les fonctionnalités de l’application et sélectionnez la fonctionnalité que vous souhaitez pour votre application.
1. Copiez ce dont vous avez besoin à partir de cette page pour concevoir votre application.<br />
   Par exemple, si votre application prend en charge l’authentification à l’aide de l’authentification unique, copiez et collez la conception pour gérer ce scénario exact.

## <a name="design-your-ux-flow"></a>Concevoir votre flux d’UX

Une fois que vous avez une conception d’application de base Teams, vous pouvez la modifier et l’affiner autant que vous le souhaitez en copiant des modèles d’interface utilisateur et des composants de base à partir du kit d’interface utilisateur.

### <a name="design-with-ui-templates"></a>Conception avec des modèles d’interface utilisateur

Les modèles d’interface utilisateur sont des conceptions complexes et haute fidélité pour les Teams et les flux de travail. Au lieu de commencer de bas en bas avec des composants de base, nous vous recommandons d’utiliser ces modèles pour simplifier et accélérer le processus de conception.

1. Dans le navigation gauche du kit d’interface utilisateur, allez aux **modèles d’interface utilisateur.**
1. Copiez des modèles qui sont logiques pour la conception de votre application.<br />
   Par exemple, si vous concevez une application personnelle, vous pouvez utiliser un modèle de tableau de bord.

### <a name="design-with-basic-ui-components"></a>Conception avec des composants d’interface utilisateur de base

En fonction Fluent’interface utilisateur, il s’Teams éléments de base pour créer des interfaces utilisateur familières. Utilisez ces composants si un modèle d’interface utilisateur manque un élément dont vous avez besoin ou si vous souhaitez simplement concevoir votre application à partir de zéro.

1. Dans le volet de navigation gauche du kit d’interface utilisateur, allez aux **composants de l’interface utilisateur de base.**
1. Copiez les composants dont vous avez besoin pour la conception de votre application (par exemple, un bouton ou un bouton bascule).

## <a name="implement-your-design"></a>Implémenter votre conception

La conception est effectuée et vous êtes prêt à commencer la création. Les outils suivants peuvent vous aider à simplifier le développement frontal de votre application.

### <a name="build-with-ui-templates"></a>Créer avec des modèles d’interface utilisateur

Si vous avez utilisé des modèles d’interface utilisateur dans votre conception, vous pouvez implémenter ces modèles avec la bibliothèque d’interface utilisateur Microsoft Teams (bibliothèque de composants React basée sur Fluent’interface utilisateur).

Actuellement, tous les modèles répertoriés dans le kit d’interface utilisateur ne sont pas disponibles dans la bibliothèque.

> [!div class="nextstepaction"]
> [Obtenir la bibliothèque (GitHub)](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="build-with-basic-ui-components"></a>Créer avec des composants d’interface utilisateur de base

À la différence de la phase de conception, vous pouvez utiliser ces composants d’interface utilisateur Fluent dans votre projet d’application si un modèle d’interface utilisateur manque un élément dont vous avez besoin ou si vous souhaitez simplement créer l’application à partir de zéro. 

(Remarque : si vous remarquez un manque de quelque chose ou si vous avez une idée pour un modèle, envisagez de contribuer au Teams bibliothèque d’interface utilisateur.)

> [!div class="nextstepaction"]
> [Obtenir la bibliothèque (Fluent’interface utilisateur)](https://fluentsite.z22.web.core.windows.net/)

## <a name="review-design-resources"></a>Examiner les ressources de conception

Que vous débutiez sur votre application ou que vous soyez proche d’une application prête pour la production, nous vous recommandons de consulter régulièrement les ressources suivantes :

* **Microsoft Teams de validation** du Store : fournit des normes que toutes les applications Teams doivent suivre, et pas seulement les applications répertoriées dans le Windows Store. Pour plus d’informations, voir les [instructions.](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)
* **Meilleures pratiques en matière** de conception : ces documents et le kit d’interface utilisateur fournissent les meilleures pratiques pour concevoir des applications de haute qualité. Par exemple, consultez les [meilleures pratiques en matière de conception de bots.](~/bots/design/bots.md#best-practices)

## <a name="see-also"></a>Voir aussi

[Conception de notifications de flux d’activités](~/concepts/design/activity-feed-notifications.md)
