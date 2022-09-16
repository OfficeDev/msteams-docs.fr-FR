---
title: Vue d’ensemble des actions universelles pour les cartes adaptatives
description: Découvrez les actions universelles pour les cartes adaptatives, telles que les vues spécifiques à l’utilisateur, la prise en charge des flux de travail séquentiels et bien plus encore pour les environnements de bureau et mobiles
ms.topic: overview
ms.localizationpriority: medium
ms.openlocfilehash: 9c04ed4726840bd3d1637555d1bb021f31bf2e25
ms.sourcegitcommit: 19f3e4e9088d0a07c9b567e76640d498b9d1981f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/16/2022
ms.locfileid: "67786975"
---
# <a name="universal-actions-for-adaptive-cards"></a>Actions universelles pour les cartes adaptatives

Les actions universelles pour les cartes adaptatives ont évolué à partir des commentaires des développeurs selon lesquelles même si la disposition et le rendu des cartes adaptatives étaient universels, la gestion des actions ne l’était pas. Même si un développeur voulait envoyer la même carte à différents endroits, il doit gérer les actions différemment.

Les actions universelles pour les cartes adaptatives font du bot le principal commun pour la gestion des actions et introduisent un nouveau type d’action, `Action.Execute`qui fonctionne entre les applications, telles que Teams et Outlook.

Ce document vous aide à comprendre comment utiliser le modèle Actions universelles pour améliorer l’expérience utilisateur de l’interaction avec les cartes adaptatives entre les plateformes et les applications.

> [!NOTE]
> La prise en charge des actions universelles pour les cartes adaptatives v1.4 est disponible uniquement pour les cartes envoyées par le bot. La prise en charge des cartes envoyées par le biais de la boîte de rédaction et des cartes de déploiement de liens sera bientôt disponible.

## <a name="enhance-user-experiences-with-universal-actions-for-adaptive-cards"></a>Améliorer les expériences utilisateur avec les actions universelles pour les cartes adaptatives

Les actions universelles pour les cartes adaptatives améliorent l’expérience utilisateur en activant les scénarios suivants :

* [Actions universelles](#universal-actions)
* [Affichages spécifiques à l’utilisateur](#user-specific-views)
* [Prise en charge du flux de travail séquentiel](#sequential-workflow-support)
* [Affichages à jour](#up-to-date-views)

### <a name="universal-actions"></a>Actions universelles

Avant les actions universelles pour les cartes adaptatives, différents hôtes fournissaient différents modèles d’action comme suit :

* Teams ou bots utilisés `Action.Submit`, une approche qui reporte le modèle de communication réel au canal sous-jacent.
* Outlook utilisé `Action.Http` pour communiquer avec le service principal spécifié explicitement dans la charge utile de carte adaptative.

L’image suivante montre le modèle d’action incohérent actuel :

:::image type="content" source="~/assets/images/adaptive-cards/current-teams-outlook-action-model.png" alt-text="Modèle d’action incohérent":::

Avec les actions universelles pour les cartes adaptatives, vous pouvez utiliser `Action.Execute` pour la gestion des actions sur différentes plateformes. `Action.Execute` fonctionne sur plusieurs hubs, notamment Teams et Outlook. En outre, une carte adaptative peut être retournée comme réponse pour une `Action.Execute` demande d’appel déclenchée.

L’image suivante montre le nouveau modèle Action universelle :

:::image type="content" source="~/assets/images/adaptive-cards/universal-action-model.png" alt-text="Nouvelles actions universelles pour les cartes adaptatives":::

Vous pouvez maintenant envoyer la même carte à Teams et Outlook et les synchroniser les unes avec les autres à l’aide du bot sous-jacent. Toute action effectuée sur l’une ou l’autre plateforme est reflétée à l’autre avec cette *build une fois, déployer n’importe où* (actions universelles pour les cartes adaptatives) modèle.

L’image suivante illustre les actions universelles pour les cartes adaptatives pour Teams et Outlook :

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="~/assets/images/mobile-universal-bots-teams-outlook.png" alt-text="Même carte mobile pour Teams et Outlook":::

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-teams-outlook.png" alt-text="Même carte pour Teams et Outlook" lightbox="../../../assets/images/adaptive-cards/universal-bots-teams-outlook.png":::

* * *

### <a name="user-specific-views"></a>Affichages spécifiques à l’utilisateur

Aujourd’hui, chaque utilisateur de la conversation ou du canal Teams voit exactement les mêmes actions d’affichage et de bouton sur la carte adaptative. Toutefois, dans certains scénarios, certains utilisateurs doivent agir différemment et avoir accès à des informations différentes au sein du même canal ou conversation.

Par exemple, si vous envoyez une carte de rapport d’incident dans une conversation ou un canal, seul l’utilisateur auquel l’incident est affecté doit voir un bouton **Résoudre** . En revanche, le créateur de l’incident doit voir un bouton **Modifier** et tous les autres utilisateurs doivent uniquement être en mesure d’afficher les détails de l’incident. Cela est rendu possible par les vues spécifiques à l’utilisateur activées par la `refresh` propriété.

L’image suivante montre un exemple d’extension de message de ticketing (ME) dans laquelle différents utilisateurs de la conversation reçoivent différentes actions en fonction de l’exigence :

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="~/assets/images/adaptive-cards/mobile-universal-bots-incident-management.jpg" alt-text="Vues spécifiques à l’utilisateur mobile" lightbox="../../../assets/images/adaptive-cards/mobile-universal-bots-incident-management.jpg":::

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-incident-management.png" alt-text="Affichages spécifiques à l’utilisateur" lightbox="../../../assets/images/adaptive-cards/universal-bots-incident-management.png":::

* * *

Pour plus d’informations, consultez [l’exemple de vues spécifiques à l’utilisateur](User-Specific-Views.md).

### <a name="sequential-workflow-support"></a>Prise en charge du flux de travail séquentiel

Avec la prise en charge des flux de travail séquentiels, les utilisateurs peuvent parcourir une série de flux de travail sans envoyer de cartes différentes séparément. Cela est rendu possible par la possibilité de `Action.Execute` retourner une carte adaptative en réponse à une action. En outre, tout utilisateur de la conversation ou du canal peut progresser dans son flux de travail sans modifier la carte pour d’autres utilisateurs dans la conversation.

L’image suivante illustre un exemple de robot de commande d’aliments : <br/>

<img src="~/assets/images/bots/sequentialWorkflow.gif" alt="Sequential Workflow" width="400"/>

L’image suivante montre les différents états pour différents utilisateurs dans la conversation ou le canal :

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-catering-bot.png" alt-text="États du bot de restauration" lightbox="../../../assets/images/adaptive-cards/universal-bots-catering-bot.png":::

Pour plus d’informations, consultez [l’exemple de flux de travail séquentiel](Sequential-Workflows.md).

### <a name="up-to-date-views"></a>Affichages à jour

Vous pouvez créer des cartes adaptatives qui se mettent à jour automatiquement. Par exemple, il peut s’agir d’une demande d’approbation envoyée par un utilisateur. Après approbation, la carte doit afficher automatiquement des détails sur l’heure d’approbation de la demande et sur la personne qui a approuvé la demande. Le modèle d’actualisation vous permet de fournir ces vues à jour. L’image suivante montre un flux d’approbation en plusieurs étapes et comment les vues des différents utilisateurs sont affichées.

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views.png" alt-text="Affichages spécifiques à l’utilisateur à jour" lightbox="../../../assets/images/adaptive-cards/universal-bots-up-to-date-views.png":::

Pour plus d’informations, consultez [l’exemple de vues à jour](Up-To-Date-Views.md).

Vous pouvez maintenant comprendre comment les cartes adaptatives peuvent être transformées avec le nouveau modèle Actions universelles pour offrir une expérience utilisateur unique et améliorée.

## <a name="adaptive-cards-and-the-new-universal-actions-model"></a>Cartes adaptatives et nouveau modèle Actions universelles

Les cartes adaptatives sont une combinaison de contenus, tels que du texte et des graphiques, ainsi que des actions qui peuvent être effectuées par un utilisateur. Pour plus d’informations, voir [Cartes adaptatives](http://adaptivecards.io/). Les nouvelles actions universelles pour les cartes adaptatives permettent une gestion commune des actions de carte adaptative entre les plateformes et les applications. Pour plus d’informations, consultez [Le modèle d’action universelle](/adaptive-cards/authoring-cards/universal-action-model).

Vous pouvez commencer par mettre à jour des scénarios à l’aide du [guide de démarrage rapide]. (Work-with-universal-actions-for-adaptive-cards.md) et tirer parti des actions universelles.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Travailler avec les actions universelles pour les cartes adaptatives](Work-with-universal-actions-for-adaptive-cards.md)

## <a name="see-also"></a>Voir aussi

* [Qu’est-ce que les bots ?](~/bots/what-are-bots.md)
* [Vue d’ensemble des cartes adaptatives](~/task-modules-and-cards/what-are-cards.md)
* [Cartes adaptatives @ Microsoft Build 2020](https://youtu.be/hEBhwB72Qn4?t=1393)
* [Cartes adaptatives @ Ignite 2020](https://techcommunity.microsoft.com/t5/video-hub/elevate-user-experiences-with-teams-and-adaptive-cards/m-p/1689460).
* [Actions universelles pour les extensions de messagerie basées sur la recherche](../../../messaging-extensions/how-to/search-commands/universal-actions-for-search-based-message-extensions.md)
