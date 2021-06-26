---
title: Modules de tâche
author: surbhigupta
description: Ajouter des expériences de fenêtres popup modales pour collecter ou afficher des informations à vos utilisateurs à partir de Microsoft Teams applications
localization_priority: Normal
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 257ca54ab53d310116cc301dded01a7582c11532
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140536"
---
# <a name="task-modules"></a>Modules de tâche

Les modules de tâche vous permettent de créer des expériences de fenêtres pop-up modales dans Teams application. Dans la fenêtre pop-up, vous pouvez :

* Exécutez votre propre code HTML ou JavaScript personnalisé.
* Afficher un `<iframe>` widget basé sur une vidéo YouTube ou Microsoft Stream.
* Afficher une [carte adaptative](/adaptive-cards/).

Les modules de tâche sont utiles pour lancer et effectuer des tâches ou afficher des informations enrichies, telles que des vidéos ou des tableaux de bord Power Business Intelligence (BI). Une expérience de fenêtre pop-up est souvent plus naturelle pour les utilisateurs qui lancent et terminent des tâches par rapport à une expérience de bot basée sur un onglet ou une conversation.

Les modules de tâche s’appuient sur les bases Microsoft Teams onglets. Il s’agit essentiellement d’un onglet à l’intérieur d’une fenêtre pop-up. Ils utilisent le même SDK, donc si vous avez créé un onglet, vous êtes déjà familiarisé avec la création d’un module de tâche.

Les modules de tâche peuvent être appelés de trois façons :

* Onglets de canal ou personnels : à l’aide du SDK onglets Microsoft Teams, vous pouvez appeler des modules de tâche à partir de boutons, de liens ou de menus de votre onglet. Pour plus d’informations, voir [l’utilisation de modules de tâche dans les onglets.](~/task-modules-and-cards/task-modules/task-modules-tabs.md)
* Bots : utilisation de boutons sur [les cartes envoyées](~/task-modules-and-cards/cards/cards-reference.md) à partir de votre bot. Cela est utile lorsque vous n’exigez pas que tous les personnes d’un canal voient ce que vous faites avec un bot. Par exemple, lorsque les utilisateurs répondent à un sondage dans un canal, il n’est pas utile de voir un enregistrement de ce sondage en cours de création. Pour plus d’informations, voir [l’utilisation de modules](~/task-modules-and-cards/task-modules/task-modules-bots.md)de tâche Teams bots.
* En dehors Teams à partir d’un lien profond : vous pouvez également créer des URL pour appeler un module de tâche de n’importe où. Pour plus d’informations, voir [la syntaxe de lien profond](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-deep-link-syntax)du module de tâche.

## <a name="components-of-a-task-module"></a>Composants d’un module de tâche

Voici à quoi ressemble un module de tâche lorsqu’il est appelé à partir d’un bot :

![Exemple de module de tâche](~/assets/images/task-module/task-module-example.png)

Un module de tâche inclut les éléments suivants, comme illustré dans l’image précédente :

1. Icône de votre [ `color` application.](~/resources/schema/manifest-schema.md#icons)
2. Nom de votre [ `short` application.](~/resources/schema/manifest-schema.md#name)
3. Titre du module de tâche spécifié dans la `title` propriété de [l’objet TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object).
4. Bouton Fermer ou annuler du module de tâche. Si l’utilisateur sélectionne ce bouton, votre application reçoit un `err` événement. Pour plus d’informations, [voir l’exemple d’envoi du résultat d’un module de tâche.](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-of-submitting-the-result-of-a-task-module)

    > [!NOTE]
    > Il n’est actuellement pas possible de détecter `err` l’événement lorsqu’un module de tâche est appelé à partir d’un bot.

5. Le rectangle bleu est l’endroit où votre page web apparaît si vous chargez votre propre page web à l’aide de la `url` propriété de [l’objet TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object). Pour plus d’informations, [voir le resserrage du module de tâche.](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-sizing)
6. Si vous affichez une carte adaptative à l’aide de la propriété de l’objet `card` [TaskInfo,](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) le remplissage est ajouté pour vous. Pour plus d’informations, voir le module de tâche [CSS pour les modules de tâche HTML ou JavaScript.](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-css-for-html-or-javascript-task-modules)
7. Les boutons de carte adaptative s’affichent après la sélection **de l’inscription.** Lorsque vous utilisez votre propre page, créez vos propres boutons.

## <a name="see-also"></a>Voir aussi

[Cartes](~/task-modules-and-cards/what-are-cards.md)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Appeler et ignorer des modules de tâche](~/task-modules-and-cards/task-modules/invoking-task-modules.md)
