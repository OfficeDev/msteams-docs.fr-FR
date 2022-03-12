---
title: Travailler avec les actions universelles pour les cartes adaptatives
description: Apprenez à utiliser les actions universelles pour les cartes adaptatives, notamment le schéma pour UniversalActions pour les cartes adaptatives, le modèle d’actualisation et la compatibilité ascendante à l’aide d’exemples de code.
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: c0893f5aaa9e454ab8a4091ce5b08c132c110746
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/12/2022
ms.locfileid: "63452577"
---
# <a name="work-with-universal-actions-for-adaptive-cards"></a>Travailler avec les actions universelles pour les cartes adaptatives

Les actions universelles pour les cartes adaptatives permettent d’implémenter des scénarios basés sur la carte adaptative pour les cartes Teams et Outlook. Ce document traite des sujets suivants :

* [Schéma utilisé pour les actions universelles pour les cartes adaptatives](#schema-for-universal-actions-for-adaptive-cards)
* [Modèle d’actualisation](#refresh-model)
* [`adaptiveCard/action` activité d’appel](#adaptivecardaction-invoke-activity)
* [Compatibilité descendante](#backward-compatibility)

## <a name="quick-start-guide-to-use-universal-actions-for-adaptive-cards-in-teams"></a>Guide de démarrage rapide pour utiliser les actions universelles pour les cartes adaptatives dans Teams

1. Remplacez toutes les instances de `Action.Submit` par `Action.Execute` pour mettre à jour un scénario existant sur Teams.
2. Ajoutez une `refresh` clause à votre carte adaptative si vous souhaitez utiliser le modèle d’actualisation automatique ou si votre scénario nécessite des affichages spécifiques de l’utilisateur.

    >[!NOTE]
    > Spécifiez la `userIds` propriété à identifier et les utilisateurs qui obtiennent les mises à jour automatiques.

3. Gérer les `adaptiveCard/action` demandes d’appel dans votre bot.
4. Utilisez le contexte de la demande d’appel pour répondre à l’aide de cartes créées pour un utilisateur.

    > [!NOTE]
    > Chaque fois que votre bot renvoie une nouvelle carte suite `Action.Execute`au traitement d’un , la réponse doit être conforme au format de réponse.

## <a name="schema-for-universal-actions-for-adaptive-cards"></a>Schéma des actions universelles pour les cartes adaptatives

Les actions universelles pour les cartes adaptatives sont introduites dans le schéma de cartes adaptatives version 1.4. Pour utiliser efficacement la carte adaptative, `version` la propriété de votre carte adaptative doit être définie sur 1,4.

> [!NOTE]
> `version` La définition de la propriété sur 1.4 rend votre carte adaptative incompatible avec les clients plus anciens des plateformes ou des applications, tels que Outlook et Teams, car ils ne prend pas en charge les actions universelles pour les cartes adaptatives.

Si vous définissez la version de carte sur moins de 1.4 et utilisez l’une ou l’autre des deux, `refresh` propriété `Action.Execute`et , les choses suivantes se produisent :

| Client | Comportement |
| :-- | :-- |
| Teams | Votre carte cesse de fonctionner. La carte n’est pas actualisée et `Action.Execute` ne s’restituera pas en fonction de la version du client Teams client. Pour garantir la compatibilité maximale dans Teams, `Action.Execute` définissez avec un `Action.Submit` dans la propriété de fallback. |

Pour plus d’informations sur la prise en charge des clients plus anciens, voir [compatibilité ascendante](#backward-compatibility).

### <a name="actionexecute"></a>Action.Execute

Lors de la conception de cartes adaptatives, remplacez `Action.Submit` et `Action.Http` par `Action.Execute`. Le schéma pour est `Action.Execute` similaire à celui de `Action.Submit`.

Pour plus d’informations, [voir schéma et propriétés Action.Execute](/adaptive-cards/authoring-cards/universal-action-model#actionexecute).

À présent, vous pouvez utiliser le modèle d’actualisation pour permettre aux cartes adaptatives de se mettre à jour automatiquement.

## <a name="refresh-model"></a>Modèle d’actualisation

Pour actualiser automatiquement votre carte adaptative, définissez sa `refresh` propriété, qui incorpore une action de type `Action.Execute` et un `userIds` tableau.

Pour plus d’informations, voir [le schéma d’actualisation et les propriétés](/adaptive-cards/authoring-cards/universal-action-model#refresh-mechanism).

## <a name="user-ids-in-refresh"></a>ID utilisateur en cours d’actualisation

Les fonctionnalités des UserIds en actualisation sont les suivantes :

* UserIds est un tableau de MRIS utilisateur, qui fait partie de `refresh` la propriété dans les cartes adaptatives.

* Si la `userIds` propriété de liste est spécifiée comme `userIds: []` dans la section Actualiser de la carte, la carte n’est pas actualisée automatiquement. Au lieu de cela, **une option Actualiser** la carte s’affiche pour l’utilisateur dans le menu à trois points du site web ou du bureau, et dans le menu contextif long sur mobile, c’est-à-dire, Android ou iOS pour actualiser manuellement la carte.

* La propriété UserIds est ajoutée, car les canaux Teams peuvent inclure un grand nombre de membres. Si tous les membres voient le canal en même temps, une actualisation automatique inconditionnelle entraîne de nombreux appels simultanés au bot. La `userIds` propriété doit toujours être incluse pour identifier les utilisateurs devant obtenir une actualisation automatique avec un maximum de *60 MRI d’utilisateur (en particulier*).

* Vous pouvez récupérer les TEAMS utilisateur du membre de la conversation. Pour plus d’informations sur l’ajout de la liste userIds dans la section Actualiser de la carte adaptative, voir récupérer la liste ou [le profil utilisateur](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile).

 Vous pouvez obtenir l’utilisateur IRM pour le canal, la conversation de groupe ou la conversation 1:1 à l’aide de l’exemple suivant :

 1. Utilisation de TurnContext  

     `userMRI= turnContext.Activity.From.Id`

 1. Utilisation de la méthode GetMemberAsync
  
     `var member = await TeamsInfo.GetMemberAsync(turnContext, turnContext.Activity.From.Id, cancellationToken);var userMRI = member.Id;`

* Exemple de Teams’utilisateurSYRY est`29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk`

> [!NOTE]
> La `userIds` propriété est ignorée dans Outlook, et la `refresh` propriété est toujours activée automatiquement. Il n’existe aucun problème d’échelle Outlook car les utilisateurs visualisent la carte à différents moments.

L’étape suivante consiste à utiliser l’activité `adaptiveCard/action` d’appel pour comprendre quelle demande doit être faite après `Action.Execute` l’exécution.

## <a name="adaptivecardaction-invoke-activity"></a>`adaptiveCard/action` activité d’appel

Lorsqu’il `Action.Execute` est exécuté dans le client, un nouveau type d’activité Invoke `adaptiveCard/action` est apporté à votre bot.

Pour plus d’informations, [voir le format de requête et les propriétés d’une activité d’appel `adaptiveCard/action` classique](/adaptive-cards/authoring-cards/universal-action-model#request-format).

Pour plus d’informations, voir [le format de réponse et les propriétés d’une `adaptiveCard/action` activité d’appel classique avec les types de réponse pris en charge](/adaptive-cards/authoring-cards/universal-action-model#response-format).

Ensuite, vous pouvez appliquer la compatibilité ascendante à des clients plus anciens sur différentes plateformes et rendre votre carte adaptative compatible.

## <a name="backward-compatibility"></a>Compatibilité descendante

Les actions universelles pour les cartes adaptatives vous permettent de définir des propriétés qui permettent la compatibilité ascendante avec les anciennes versions de Outlook et Teams.

### <a name="teams"></a>Teams

Pour garantir la compatibilité ascendante de vos cartes adaptatives avec des versions antérieures de Teams, `fallback` vous devez inclure la propriété et définir sa valeur sur `Action.Submit`. En outre, votre code de bot doit traiter les deux `Action.Execute` et `Action.Submit`.

Pour plus d’informations, [voir compatibilité avec les Teams](/adaptive-cards/authoring-cards/universal-action-model#teams).

## <a name="code-samples"></a>Exemples de code

|Exemple de nom | Description | . NETCore | Node.js |
|----------------|-----------------|--------------|--------------|
| Teams bot de restauration | Créez un bot qui accepte l’ordre des produits à l’aide de cartes adaptatives. |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-teams-catering/csharp)| N’est pas encore disponible. |
| Cartes adaptatives de flux de travail séquentiels | Montrer comment implémenter des flux de travail séquentiels, des affichages spécifiques à l’utilisateur et des cartes adaptatives à jour dans les bots. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/nodejs) |

## <a name="see-also"></a>Voir aussi

* [Actions de carte adaptative dans Teams](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [Comment fonctionnent les bots ?](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
* [Flux de travail séquentiels](~/task-modules-and-cards/cards/universal-actions-for-adaptive-cards/sequential-workflows.md)
* [Cartes actualisées](~/task-modules-and-cards/cards/universal-actions-for-adaptive-cards/up-to-date-views.md)
* [Commentaires sur l’achèvement du formulaire](~/bots/how-to/conversations/conversation-messages.md#form-completion-feedback)
