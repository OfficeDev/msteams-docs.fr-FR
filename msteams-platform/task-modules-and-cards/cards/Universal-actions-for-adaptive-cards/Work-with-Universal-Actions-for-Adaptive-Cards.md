---
title: Travailler avec les actions universelles pour les cartes adaptatives
description: Apprenez à utiliser les actions universelles pour les cartes adaptatives, notamment le schéma pour universalactions pour les cartes adaptatives, le modèle d’actualisation et la compatibilité descendante
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: 17dd7fd611c593c3f5de0237e0aa61885ac630c0
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143878"
---
# <a name="work-with-universal-actions-for-adaptive-cards"></a>Travailler avec les actions universelles pour les cartes adaptatives

Les actions universelles pour Cartes adaptatives permettent d’implémenter des scénarios basés sur des cartes adaptatives pour Teams et Outlook. Ce document traite des rubriques suivantes :

* [Schéma utilisé pour les actions universelles pour Cartes adaptatives](#schema-for-universal-actions-for-adaptive-cards)
* [Actualiser un modèle](#refresh-model)
* [`adaptiveCard/action` invoquer une activité](#adaptivecardaction-invoke-activity)
* [Compatibilité descendante](#backward-compatibility)

## <a name="quick-start-guide-to-use-universal-actions-for-adaptive-cards-in-teams"></a>Guide de démarrage rapide pour utiliser les actions universelles pour Cartes adaptatives dans Teams

1. Remplacez toutes les instances de `Action.Submit` par `Action.Execute` pour mettre à jour un scénario existant sur Teams.
2. Ajoutez une clause `refresh` à votre carte adaptative, si vous souhaitez utiliser le modèle d’actualisation automatique ou si votre scénario nécessite des vues spécifiques à l’utilisateur.

    >[!NOTE]
    > Spécifiez la `userIds` propriété pour identifier les utilisateurs qui reçoivent des mises à jour automatiques.

3. Gérez `adaptiveCard/action` appeler des requêtes dans votre bot.
4. Utilisez le contexte de la demande d’appel pour répondre avec des cartes créées pour un utilisateur.

    > [!NOTE]
    > Chaque fois que votre bot retourne une nouvelle carte suite au traitement d’un `Action.Execute`, la réponse doit être conforme au format de réponse.

## <a name="schema-for-universal-actions-for-adaptive-cards"></a>Schéma des actions universelles pour Cartes adaptatives

Les actions universelles pour Cartes adaptatives sont introduites dans le schéma Cartes adaptatives version 1.4. Pour utiliser efficacement la carte adaptative, la propriété `version` de votre carte adaptative doit être définie sur 1,4.

> [!NOTE]
> La définition de la propriété `version` sur 1.4 rend votre carte adaptative incompatible avec les clients plus anciens des plateformes ou des applications, telles qu’Outlook et Teams, car elles ne prennent pas en charge les actions universelles pour Cartes adaptatives.

Si vous définissez la version de la carte sur une version inférieure à 1.4 et que vous utilisez une ou les deux, la propriété `refresh` et `Action.Execute`, les événements suivants se produisent :

| Client | Comportement |
| :-- | :-- |
| Équipes | Votre carte cesse de fonctionner. La carte n’est pas actualisée et `Action.Execute` ne s’affiche pas en fonction de la version du client Teams. Pour garantir une compatibilité maximale dans Teams, définissez `Action.Execute` avec une classe `Action.Submit` dans la propriété de secours. |

Pour plus d’informations sur la prise en charge des clients plus anciens, consultez [compatibilité descendante](#backward-compatibility).

### <a name="actionexecute"></a>Exécution d’action

Lors de la création de Cartes adaptatives, remplacez `Action.Submit` et `Action.Http` par `Action.Execute`. Le schéma de `Action.Execute` est similaire à celui de `Action.Submit`.

Pour plus d’informations, consultez [Schéma d’exécution et propriétés](/adaptive-cards/authoring-cards/universal-action-model#actionexecute).

À présent, vous pouvez utiliser le modèle d’actualisation pour permettre à Cartes adaptatives de se mettre à jour automatiquement.

## <a name="refresh-model"></a>Actualiser le modèle

Pour actualiser automatiquement votre carte adaptative, définissez sa propriété `refresh`, qui incorpore une action de type `Action.Execute` et un tableau `userIds`.

Pour plus d’informations, consultez [actualiser le schéma et les propriétés](/adaptive-cards/authoring-cards/universal-action-model#refresh-mechanism).

## <a name="user-ids-in-refresh"></a>ID d’utilisateur en cours d’actualisation

Voici les fonctionnalités des UserIds en cours d’actualisation :

* UserIds est un tableau de MRIS utilisateur, qui fait partie de la propriété `refresh` dans Cartes adaptatives.

* Si la propriété de liste `userIds` est spécifiée comme `userIds: []` dans la section Actualiser de la carte, la carte n’est pas automatiquement actualisée. Au lieu de cela, une option **Actualiser la carte** s’affiche pour l’utilisateur dans le menu à points triples de Teams client web ou de bureau et dans le menu contextuel longue pression dans Teams mobile, c’est-à-dire Android ou iOS pour actualiser manuellement la carte. Vous pouvez également choisir d’ignorer `userIds` complètement la propriété d’actualisation au cas où le scénario impliquerait <=60 membres dans Teams conversations ou canaux de groupe. Le client Teams appelle automatiquement les appels d’actualisation pour tous les utilisateurs si le groupe ou le canal a <=60 utilisateurs.

* La propriété UserIds est ajoutée, car les canaux dans Teams peuvent inclure un grand nombre de membres. Si tous les membres consultent le canal en même temps, une actualisation automatique inconditionnelle entraîne de nombreux appels simultanés au bot. La propriété `userIds` doit toujours être incluse pour identifier les utilisateurs qui doivent recevoir une actualisation automatique avec un maximum de *60 (soixante) MRI utilisateur*.

* Vous pouvez récupérer les MRIS utilisateur du membre de conversation Teams. Pour plus d’informations sur l’ajout de la liste userIds dans la section Actualiser de la carte adaptative, consultez [récupérer la liste ou le profil utilisateur](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile).

 Vous pouvez obtenir le MRI utilisateur pour le canal, la conversation de groupe ou la conversation privée à l’aide de l’exemple suivant :

 1. Utilisation de TurnContext  

     `userMRI= turnContext.Activity.From.Id`

 1. Utilisation de la méthode GetMemberAsync
  
     `var member = await TeamsInfo.GetMemberAsync(turnContext, turnContext.Activity.From.Id, cancellationToken);var userMRI = member.Id;`

* L’exemple d’utilisateur Teams EST `29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk`

> [!NOTE]
> La propriété `userIds` est ignorée dans Outlook, et la propriété `refresh` est toujours activée automatiquement. Il n’existe aucun problème de mise à l’échelle dans Outlook, car les utilisateurs consultent la carte à des moments différents.

L’étape suivante consiste à utiliser l’activité `adaptiveCard/action` appeler pour comprendre quelle demande doit être effectuée après l’exécution de `Action.Execute`.

## <a name="adaptivecardaction-invoke-activity"></a>`adaptiveCard/action` appeler l’activité

Quand `Action.Execute` est exécuté dans le client, un nouveau type d’activité Invoke `adaptiveCard/action` est créé pour votre bot.

Pour plus d’informations, consultez [format de requête et propriétés d’une activité d’invocation classique `adaptiveCard/action` ](/adaptive-cards/authoring-cards/universal-action-model#request-format).

Pour plus d’informations, consultez [format de réponse et propriétés d’une activité d’invocation classique`adaptiveCard/action` avec des types de réponse pris en charge](/adaptive-cards/authoring-cards/universal-action-model#response-format).

Ensuite, vous pouvez appliquer la compatibilité descendante aux clients plus anciens sur différentes plateformes et rendre votre carte adaptative compatible.

## <a name="backward-compatibility"></a>Compatibilité descendante

Les actions universelles pour Cartes adaptatives vous permettent de définir des propriétés qui permettent la compatibilité descendante avec les versions antérieures d’Outlook et teams.

### <a name="teams"></a>Teams

Pour garantir la compatibilité descendante de votre Cartes adaptatives avec les versions antérieures de Teams, vous devez inclure la propriété `fallback` et définir sa valeur sur `Action.Submit`. En outre, votre code de bot doit traiter `Action.Execute` et `Action.Submit`.

Pour plus d’informations, voir [Considérations relatives à la compatibilité descendante](/adaptive-cards/authoring-cards/universal-action-model#teams).

## <a name="code-samples"></a>Exemples de code

|Exemple de nom | Description | . NETCore | Node.js |
|----------------|-----------------|--------------|--------------|
| Bot de traiteur Teams | Créez un bot qui accepte la commande de nourriture à l’aide de Cartes adaptatives. |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-teams-catering/csharp)| N’est pas encore disponible. |
| Flux de travail séquentiels Cartes adaptatives | Montrez comment implémenter des flux de travail séquentiels, des vues spécifiques à l’utilisateur et des Cartes adaptatives à jour dans les bots. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/csharp) | [Affichage](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/nodejs) .|

## <a name="see-also"></a>Voir aussi

* [Actions de carte adaptative dans Teams](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [Comment fonctionnent les bots ?](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
* [Flux de travail séquentiels](~/task-modules-and-cards/cards/universal-actions-for-adaptive-cards/sequential-workflows.md)
* [Cartes actualisées](~/task-modules-and-cards/cards/universal-actions-for-adaptive-cards/up-to-date-views.md)
* [Commentaires sur l’achèvement du formulaire](~/bots/how-to/conversations/conversation-messages.md#form-completion-feedback)
