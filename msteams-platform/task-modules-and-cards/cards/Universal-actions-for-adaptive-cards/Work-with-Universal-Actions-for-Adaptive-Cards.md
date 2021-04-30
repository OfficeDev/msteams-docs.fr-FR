---
title: Travailler avec des actions universelles pour les cartes adaptatives
description: Travaillez avec les actions universelles pour les cartes adaptatives.
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 8c260a4893d38ad365cbb3bdd5a7613a1b42654f
ms.sourcegitcommit: 1256639fa424e3833b44207ce847a245824d48e6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/29/2021
ms.locfileid: "52088839"
---
# <a name="work-with-universal-actions-for-adaptive-cards"></a>Travailler avec des actions universelles pour les cartes adaptatives

Les actions universelles pour les cartes adaptatives offrent un moyen d'implémenter des scénarios basés sur la carte adaptative pour les cartes Teams et Outlook. Ce document couvre les sujets suivants :

* [Schéma utilisé pour les actions universelles pour les cartes adaptatives](#schema-for-universal-actions-for-adaptive-cards)
* [Modèle d'actualisation](#refresh-model)
* [`adaptiveCard/action` activité d'appel](#adaptivecardaction-invoke-activity)
* [Compatibilité descendante](#backward-compatibility)

## <a name="quick-start-guide-to-leverage-universal-actions-for-adaptive-cards-in-teams"></a>Guide de démarrage rapide pour tirer parti des actions universelles pour les cartes adaptatives dans Teams

1. Remplacez toutes les instances `Action.Submit` de par pour mettre à jour un scénario existant sur `Action.Execute` Teams.
2. Ajoutez une clause à votre carte adaptative si vous souhaitez tirer parti du modèle d'actualisation automatique ou si votre scénario nécessite des affichages `refresh` spécifiques de l'utilisateur.

    >[!NOTE]
    > Spécifiez la `userIds` propriété à identifier et les utilisateurs qui obtiennent les mises à jour automatiques.

3. Gérer `adaptiveCard/action` les demandes d'appel dans votre bot.
4. Utilisez le contexte de la demande d'appel pour répondre à l'aide de cartes spécifiquement créées pour un utilisateur.

    > [!NOTE]
    > Chaque fois que votre bot renvoie une nouvelle carte suite au traitement d'un , la réponse doit `Action.Execute` être conforme au format de réponse.

## <a name="schema-for-universal-actions-for-adaptive-cards"></a>Schéma des actions universelles pour les cartes adaptatives

Les actions universelles pour les cartes adaptatives sont introduites dans le schéma de cartes adaptatives version 1.4. Pour utiliser efficacement la carte adaptative, la propriété de votre carte adaptative doit être définie `version` sur 1,4.

> [!NOTE]
> La définition de la propriété sur 1.4 rend votre carte adaptative incompatible avec les clients plus anciens des plateformes ou des applications, tels que Outlook et Teams, car ils ne prend pas en charge les actions universelles pour les cartes `version` adaptatives.

Si vous définissez la version de carte sur moins de 1.4 et utilisez l'une ou l'autre des deux, propriété et , les choses `refresh` `Action.Execute` suivantes se produisent :

| Client | Comportement |
| :-- | :-- |
| Teams | Votre carte cesse de fonctionner. La carte n'est pas actualisée et ne s'restituera pas en fonction de la `Action.Execute` version du client Teams client. Pour garantir la compatibilité maximale dans Teams, définissez avec un dans `Action.Execute` `Action.Submit` la propriété de fallback. |

Pour plus d'informations sur la prise en charge des clients plus anciens, voir [compatibilité ascendante.](#backward-compatibility)

### <a name="actionexecute"></a>Action.Execute

Lors de la conception de cartes adaptatives, `Action.Submit` remplacez et `Action.Http` par `Action.Execute` . Le schéma pour `Action.Execute` est similaire à celui de `Action.Submit` .

Pour plus d'informations, [voirAction.Exeschéma et propriétés cute.](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#actionexecute)

À présent, vous pouvez utiliser le modèle d'actualisation pour permettre aux cartes adaptatives de se mettre à jour automatiquement.

## <a name="refresh-model"></a>Modèle d'actualisation

Pour actualiser automatiquement votre carte adaptative, définissez sa propriété, qui incorpore une `refresh` action de type et un `Action.Execute` `userIds` tableau.

Pour plus d'informations, voir [le schéma d'actualisation et les propriétés.](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#refresh-mechanism)

## <a name="user-ids-in-refresh"></a>ID utilisateur en cours d'actualisation

Les fonctionnalités des UserIds en actualisation sont les suivantes :

* UserIds est un tableau d'utilisateurSIPL qui fait partie de la `refresh` propriété dans les cartes adaptatives.

* Si la propriété de liste est spécifiée comme dans la section Actualiser de la carte, la carte n'est `userIds` `userIds: []` pas actualisée automatiquement. Au lieu de cela, une **option** Actualiser la carte s'affiche pour l'utilisateur dans le menu à trois points du site web ou de bureau, et dans le menu contextif long sur mobile, c'est-à-dire, Android ou iOS pour actualiser manuellement la carte.

* La propriété UserIds est ajoutée, car les canaux Teams peuvent inclure un grand nombre de membres. Si tous les membres voient le canal en même temps, une actualisation automatique inconditionnelle entraîne de nombreux appels simultanés au bot. Pour éviter cela, la propriété doit toujours être incluse pour identifier les utilisateurs devant obtenir une actualisation automatique avec un maximum de `userIds` *60 MRI d'utilisateurs (en particulier).*

* Pour plus d'informations sur la façon d'extraire les MRI utilisateur d'un membre de la conversation Teams à ajouter à la liste userIds dans la section Actualiser de la carte adaptative, voir récupérer la liste ou le profil [utilisateur.](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile)

* Exemple de Teams'utilisateurSYRY est`29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk`

> [!NOTE]
> La propriété est ignorée dans Outlook, et la propriété est `userIds` `refresh` toujours activée automatiquement. Il n'existe aucun problème d'échelle Outlook car les utilisateurs visualisent la carte à différents moments.

L'étape suivante consiste à utiliser `adaptiveCard/action` l'activité d'appel pour comprendre quelle demande doit être faite après `Action.Execute` l'exécution.

## <a name="adaptivecardaction-invoke-activity"></a>`adaptiveCard/action` activité d'appel

Lorsqu'il est exécuté dans le client, un nouveau type d'activité `Action.Execute` Invoke est apporté à votre `adaptiveCard/action` bot.

Pour plus d'informations, [voir le format de requête et les propriétés d'une activité `adaptiveCard/action` d'appel classique.](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#request-format)

Pour plus d'informations, voir le format de réponse et les propriétés [d'une activité `adaptiveCard/action` d'appel classique avec les types de réponse pris en charge.](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#response-format)

Ensuite, vous pouvez appliquer la compatibilité ascendante à des clients plus anciens sur différentes plateformes et rendre votre carte adaptative compatible.

## <a name="backward-compatibility"></a>Compatibilité descendante

Les actions universelles pour les cartes adaptatives vous permettent de définir des propriétés qui permettent la compatibilité ascendante avec les anciennes versions de Outlook et Teams.

### <a name="teams"></a>Teams

Pour garantir la compatibilité ascendante de vos cartes adaptatives avec les versions antérieures de Teams, vous devez inclure la propriété et définir `fallback` sa valeur sur `Action.Submit` . En outre, votre code de bot doit traiter les deux `Action.Execute` et `Action.Submit` .

Pour plus d'informations, [voir compatibilité ascendante sur Teams](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model#teams).

## <a name="see-also"></a>Voir aussi

* [Actions de carte adaptative dans Teams](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [Comment fonctionnent les bots ?](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
