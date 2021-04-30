---
title: Vue d'ensemble des actions universelles pour les cartes adaptatives
description: Vue d'ensemble rapide des actions universelles pour les cartes adaptatives.
ms.topic: overview
localization_priority: Normal
ms.openlocfilehash: f0adf3d1a01262ff9cbdf14128c9ffe088ae8072
ms.sourcegitcommit: 1256639fa424e3833b44207ce847a245824d48e6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/29/2021
ms.locfileid: "52088856"
---
# <a name="universal-actions-for-adaptive-cards"></a>Actions universelles pour les cartes adaptatives

Les actions universelles pour les cartes adaptatives ont évolué à partir des commentaires du développeur qui, même si la disposition et le rendu des cartes adaptatives étaient universels, la gestion des actions n'était pas. Même si un développeur souhaitait envoyer la même carte à différents endroits, il doit gérer les actions différemment.

Universal Actions for Adaptive Cards brings the bot as the common backend for handling actions and introduces a new action type, `Action.Execute` which works across apps, such as Teams and Outlook.

Ce document vous aide à comprendre comment utiliser le modèle Actions universelles pour améliorer l'expérience utilisateur lors de l'interaction avec les cartes adaptatives sur les plateformes et les applications.

> [!NOTE]
> La prise en charge des actions universelles pour les cartes adaptatives est disponible uniquement pour les cartes envoyées par le bot. La prise en charge des cartes envoyées par le biais de la zone de composition et des cartes de déploiement de liens sera bientôt disponible.

## <a name="enhance-user-experiences-with-universal-actions-for-adaptive-cards"></a>Améliorer les expériences utilisateur avec les actions universelles pour les cartes adaptatives

Les actions universelles pour les cartes adaptatives améliorent l'expérience utilisateur en activant les scénarios suivants :

* [Actions universelles](#universal-actions)
* [Affichages spécifiques à l'utilisateur](#user-specific-views)
* [Prise en charge séquentielle du flux de travail](#sequential-workflow-support)
* [Affichages à jour](#up-to-date-views)

### <a name="universal-actions"></a>Actions universelles

Avant les actions universelles pour les cartes adaptatives, différents hôtes fournissaient différents modèles d'action comme suit :

* Teams ou bots utilisés, une approche qui reporte le modèle de communication réel `Action.Submit` au canal sous-jacent.
* Outlook utilisé pour communiquer avec le service backend spécifié explicitement dans la charge utile de `Action.Http` carte adaptative.

L'image suivante illustre le modèle d'action incohérent actuel :

:::image type="content" source="~/assets/images/adaptive-cards/current-teams-outlook-action-model.png" alt-text="Modèle d'action incohérent":::

Avec les actions universelles pour les cartes adaptatives, vous pouvez utiliser la gestion des `Action.Execute` actions sur différentes plateformes. `Action.Execute`fonctionne sur les hubs, notamment Teams et Outlook. En outre, une carte adaptative peut être renvoyée en réponse à une demande `Action.Execute` d'appel déclenchée.

L'image suivante montre le nouveau modèle d'action universelle :

:::image type="content" source="~/assets/images/adaptive-cards/universal-action-model.png" alt-text="Nouvelles actions universelles pour les cartes adaptatives":::

Vous pouvez désormais envoyer la même carte aux deux Teams et Outlook et les synchroniser les unes avec les autres à l'aide du bot sous-jacent. Toute action entreprise sur l'une ou l'autre plateforme est reflétée dans l'autre avec cette build une seule *fois,* déployer n'importe où (Actions universelles pour les cartes adaptatives).

L'image suivante illustre les actions universelles pour les cartes adaptatives pour Teams et Outlook :

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-teams-outlook.png" alt-text="Même carte pour Teams et Outlook":::

### <a name="user-specific-views"></a>Affichages spécifiques à l'utilisateur

Aujourd'hui, tous les utilisateurs Teams chat ou canal voient exactement les mêmes actions d'affichage et de bouton sur la carte adaptative. Toutefois, dans certains scénarios, certains utilisateurs doivent agir différemment et avoir accès à différentes informations au sein de la même conversation ou canal.

Par exemple, si vous envoyez une carte de rapport d'incident dans une conversation ou un canal, seul l'utilisateur affecté à l'incident doit voir un **bouton Résoudre.** En revanche, le créateur de  l'incident doit voir un bouton Modifier et tous les autres utilisateurs doivent uniquement être en mesure d'afficher les détails de l'incident. Cela est rendu possible par les affichages spécifiques de l'utilisateur qui sont activés par la `refresh` propriété.

L'image suivante montre un exemple d'extension de messagerie de ticket dans laquelle différents utilisateurs de la conversation sont affichés différentes actions en fonction de l'exigence :

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-incident-management.png" alt-text="Affichages spécifiques à l'utilisateur":::

Pour plus d'informations, voir [l'exemple pour les affichages spécifiques de l'utilisateur.](User-Specific-Views.md)

### <a name="sequential-workflow-support"></a>Prise en charge séquentielle du flux de travail

Avec la prise en charge séquentielle du flux de travail, les utilisateurs peuvent avancer dans une série de flux de travail sans envoyer différentes cartes séparément. Cela est rendu possible par la possibilité de renvoyer une `Action.Execute` carte adaptative en réponse à une action. En outre, tous les utilisateurs de la conversation ou du canal peuvent avancer dans leur flux de travail sans modifier la carte pour les autres utilisateurs de la conversation.

L'image suivante illustre un exemple de robot de commande de produits : <br/>

<img src="~/assets/images/bots/sequentialWorkflow.gif" alt="Sequential Workflow" width="400"/>

L'image suivante montre les différents états pour les différents utilisateurs dans la conversation ou le canal :

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-catering-bot.png" alt-text="États du bot de restauration":::

Pour plus d'informations, voir [l'exemple de flux de travail séquentiel.](Sequential-Workflows.md)

### <a name="up-to-date-views"></a>Affichages à jour

Vous pouvez créer des cartes adaptatives qui se met à jour automatiquement. Par exemple, il peut s'agit d'une demande d'approbation envoyée par un utilisateur. Après approbation, la carte doit afficher automatiquement les détails sur l'heure d'approbation de la demande et sur les personnes qui ont approuvé la demande. Le modèle d'actualisation vous permet de fournir ces affichages à jour. L'image suivante illustre un flux d'approbation en plusieurs étapes et la façon dont les vues de différents utilisateurs sont affichées.

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views.png" alt-text="Affichages utilisateur spécifiques à jour":::

Pour plus d'informations, voir [l'exemple d'affichages à jour.](Up-To-Date-Views.md)

À présent, vous pouvez comprendre comment les cartes adaptatives peuvent être transformées avec le nouveau modèle Actions universelles pour fournir une expérience utilisateur unique et améliorée.

## <a name="adaptive-cards-and-the-new-universal-actions-model"></a>Cartes adaptatives et nouveau modèle Actions universelles

Les cartes adaptatives sont une combinaison de contenu, tel que du texte et des graphiques, et d'actions qui peuvent être effectuées par un utilisateur. Pour plus d'informations, voir [Cartes adaptatives.](http://adaptivecards.io/) Les nouvelles actions universelles pour les cartes adaptatives permettent une gestion courante des actions de carte adaptative sur les plateformes et les applications. Pour plus d'informations, voir [Modèle d'action universelle.](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model)

Le document [Actions universelles pour cartes adaptatives](Work-with-universal-actions-for-adaptive-cards.md) vous permet d'utiliser les fonctionnalités des actions universelles pour les cartes adaptatives pour votre solution.

## <a name="see-also"></a>Voir aussi

* [Qu'est-ce que les bots ?](~/bots/what-are-bots.md)
* [Vue d’ensemble des cartes adaptatives](~/task-modules-and-cards/what-are-cards.md)
* [Cartes adaptatives @ Microsoft Build 2020](https://youtu.be/hEBhwB72Qn4?t=1393)
* [Cartes adaptatives @ Ignite 2020](https://techcommunity.microsoft.com/t5/video-hub/elevate-user-experiences-with-teams-and-adaptive-cards/m-p/1689460)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Travailler avec des actions universelles pour les cartes adaptatives](Work-with-universal-actions-for-adaptive-cards.md)
