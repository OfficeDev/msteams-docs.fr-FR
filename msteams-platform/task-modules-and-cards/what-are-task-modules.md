---
title: Modules de tâche
author: surbhigupta
description: Dans ce module, découvrez comment ajouter des expériences contextuelles modales pour collecter ou afficher des informations à vos utilisateurs à partir de vos applications Microsoft Teams
ms.localizationpriority: medium
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 23d6a0f1645fefe66544c755ddb617eba9ea8f3e
ms.sourcegitcommit: 1cda2fd3498a76c09e31ed7fd88175414ad428f7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/27/2022
ms.locfileid: "67035295"
---
# <a name="task-modules"></a>Modules de tâche

Les modules de tâche vous permettent de créer des expériences contextuelles modales dans votre application Teams. Dans la fenêtre contextuelle, vous pouvez :

* Exécutez votre propre code HTML ou JavaScript personnalisé.
* Affichez un `<iframe>`widget basé sur youTube ou Microsoft Stream vidéo.
* Afficher une [carte adaptative](/adaptive-cards/).

Les modules de tâches sont utiles pour lancer et terminer des tâches ou afficher des informations enrichies, telles que des vidéos ou des tableaux de bord Power Business Intelligence (BI). Une expérience contextuelle est souvent plus naturelle pour les utilisateurs qui lancent et effectuent des tâches par rapport à une expérience de bot basée sur un onglet ou une conversation.

Les modules de tâche s’appuient sur les bases des onglets Microsoft Teams. Il s’agit essentiellement d’un onglet à l’intérieur d’une fenêtre contextuelle. Ils utilisent le même Kit de développement logiciel (SDK), donc si vous avez créé un onglet, vous êtes déjà familiarisé avec la création d’un module de tâche.

Les modules de tâche peuvent être appelés de trois façons :

* Onglets de canal ou personnels : à l’aide du Kit de développement logiciel (SDK) Onglets Microsoft Teams, vous pouvez appeler des modules de tâches à partir de boutons, de liens ou de menus de votre onglet. Pour plus d’informations, consultez [l’utilisation de modules de tâches dans des onglets](~/task-modules-and-cards/task-modules/task-modules-tabs.md).
* Bots : Utilisation de boutons sur les [cartes](~/task-modules-and-cards/cards/cards-reference.md) envoyées à partir de votre bot. Cela est utile lorsque vous n’avez pas besoin que tous les utilisateurs d’un canal voient ce que vous faites avec un bot. Par exemple, lorsque les utilisateurs répondent à un sondage dans un canal, il n’est pas utile de voir un enregistrement de ce sondage en cours de création. Pour plus d’informations, consultez [l’utilisation de modules de tâches à partir de bots Teams](~/task-modules-and-cards/task-modules/task-modules-bots.md).
* En dehors de Teams à partir d’un lien profond : vous pouvez également créer des URL pour appeler un module de tâche à partir de n’importe où. Pour plus d’informations, consultez [la syntaxe de lien profond du module de tâches](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-deep-link-syntax).

## <a name="components-of-a-task-module"></a>Composants d’un module de tâche

Voici à quoi ressemble un module de tâche lorsqu’il est appelé à partir d’un bot :

:::image type="content" source="../assets/images/task-module/task-module-example.png" alt-text="exemple de module de tâche":::

Un module de tâche inclut les éléments suivants, comme illustré dans l’image précédente :

1. Icône de [`color`](~/resources/schema/manifest-schema.md#icons)votre application.
2. Nom de [`short`](~/resources/schema/manifest-schema.md#name)votre application.
3. Titre du module de tâche spécifié dans la `title` propriété de [l’objet TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object).
4. Bouton Fermer ou annuler du module de tâche. Si l’utilisateur sélectionne ce bouton, votre application reçoit un `err` événement. Pour plus d’informations, consultez [l’exemple d’envoi du résultat d’un module de tâche](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-of-submitting-the-result-of-a-task-module).

    > [!NOTE]
    > Il n’est actuellement pas possible de détecter l’événement `err` lorsqu’un module de tâche est appelé à partir d’un bot.

5. Le rectangle bleu est l’endroit où votre page web s’affiche si vous chargez votre propre page web à l’aide de la `url` propriété de [l’objet TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object). Pour plus d'informations, consultez [Dimensionnement du module de tâches](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-sizing).
6. Si vous affichez une carte adaptative à l’aide de la `card` propriété de [l’objet TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) , le remplissage est ajouté pour vous. Pour plus d’informations, consultez le [module de tâche CSS pour les modules de tâche HTML ou JavaScript](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-css-for-html-or-javascript-task-modules).
7. Les boutons de carte adaptative s’affichent après avoir sélectionné **S’inscrire**. Lorsque vous utilisez votre propre page, créez vos propres boutons.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Appeler et ignorer des modules de tâche](~/task-modules-and-cards/task-modules/invoking-task-modules.md)

## <a name="see-also"></a>Voir aussi

[Cartes](~/task-modules-and-cards/what-are-cards.md)
