---
title: Actions universelles pour les extensions de message basées sur la recherche
author: v-ypalikila
description: Dans cet article, découvrez les actions universelles et l’actualisation automatique pour les cartes adaptatives dans les extensions de message basées sur la recherche.
ms.topic: conceptual
ms.author: v-ypalikila
ms.localizationpriority: medium
ms.openlocfilehash: b8515ca2a84d3c29ddfb384fde5038a68d953c33
ms.sourcegitcommit: 19f3e4e9088d0a07c9b567e76640d498b9d1981f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/16/2022
ms.locfileid: "67787197"
---
# <a name="universal-actions-for-search-based-message-extensions"></a>Actions universelles pour les extensions de message basées sur la recherche

Les cartes adaptatives dans les extensions de message basées sur la recherche prennent désormais en charge les actions universelles. Pour activer les actions universelles pour les extensions de message basées sur la recherche, l’application doit se conformer au [schéma des actions universelles pour les cartes adaptatives](../../../task-modules-and-cards/cards/Universal-actions-for-adaptive-cards/Work-with-Universal-Actions-for-Adaptive-Cards.md#schema-for-universal-actions-for-adaptive-cards) , ainsi qu’aux exigences suivantes :

1. Un bot de conversation doit être défini dans le manifeste de l’application.
1. Si vous disposez déjà d’un bot conversationnel, vous devez utiliser le même bot que celui utilisé dans votre extension de message.
1. Si la carte est envoyée dans un groupe, l’application doit spécifier ou `groupchat` étendre `team` son bot dans le manifeste.

Exemple de schéma JSON avec `team` des valeurs :`groupchat`

```json
{
    "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json",
    "manifestVersion": "1.11",
    "version": "1.0.0",
    "id": "%MICROSOFT-APP-ID%",
    "packageName": "com.example.myapp",
    "bots": [
        {
            "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
            "scopes": [
                    "team",
                    "personal",
                    "groupchat"
                ]
        }
    ],
    "composeExtensions": [
        {
            "canUpdateConfiguration": true,
            "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%", // Use the same bot as what is specified in the bots section above
        }
    ]
}
```

## <a name="automatic-refresh-for-adaptive-cards-in-search-based-message-extensions"></a>Actualisation automatique des cartes adaptatives dans les extensions de message basées sur la recherche

Activez l’actualisation automatique des cartes adaptatives dans les extensions de message basées sur la recherche pour garantir que les utilisateurs voient toujours les dernières informations. Pour l’activer, définissez `userIds` le tableau dans ou `8:orgid:<AAD ID>` au `29:<ID>` format dans la `refresh` propriété. Pour plus d’informations, consultez [travailler avec les actions universelles pour les cartes adaptatives](../../../task-modules-and-cards/cards/Universal-actions-for-adaptive-cards/Work-with-Universal-Actions-for-Adaptive-Cards.md#user-ids-in-refresh).

Exemple de `userIds` tableau dans la `refresh` propriété :

```json
    {
        "type": "AdaptiveCard",
        "refresh": {
            "userIds": [
                "8:orgid:<AADID>",
                "29:<id>"
            ],
            "action": {
                "type": "Action.Execute",
                "data": {}
            }
        },
        "body": [
            {
                "type": "TextBlock",
                "text": "Hello World!",
                "wrap": true
            }
        ],
        "actions": [
            {
                "type": "Action.Execute",
                "data": {},
                "title": "Hello"
            }
        ]
    }
```

> [!NOTE]
> L’actualisation automatique est activée pour tous les utilisateurs de la conversation de groupe ou du canal dont la taille est *inférieure ou égale à* 60 utilisateurs. Pour les conversations (conversation de groupe ou canal) avec plus de 60 utilisateurs, les utilisateurs peuvent utiliser le bouton Actualiser dans le menu des options de message pour obtenir le dernier résultat.

Exemple de `Action.Execute` la `refresh` propriété :

```json
    {
        "type": "AdaptiveCard",
        "refresh": {
            "action": {
                "type": "Action.Execute",
                "data": {}
            }
        },
        "body": [
            {
                "type": "TextBlock",
                "text": "Hello World!",
                "wrap": true
            }
        ],
        "actions": [
            {
                "type": "Action.Execute",
                "data": {},
                "title": "Hello"
            }
        ]
    }
```

## <a name="just-in-time-install"></a>Installation juste-à-temps

JIT (Juste-à-temps) vous permet d’installer une extension de carte ou de message pour plusieurs utilisateurs dans une conversation de groupe ou un canal. Pour prendre en charge les actions universelles dans les extensions de message basées sur la recherche, votre bot est ajouté à la conversation où la carte (avec `Action.Execute`) est envoyée par l’utilisateur.

Lorsqu’un utilisateur sélectionne une carte et l’envoie dans une conversation de groupe ou un canal, une invite d’installation **JIT** s’affiche. Une fois que l’utilisateur a sélectionné l’option **d’envoi** , l’application est ajoutée pour tous les utilisateurs de la conversation ou du canal en arrière-plan.

> [!NOTE]
> Pour les applications qui n’ont `Action.Execute` pas et `refresh` le schéma défini, l’invite d’installation n’est pas affichée aux utilisateurs.

Exemple de flux d’utilisateur d’installation dynamique ME et JIT :

  :::image type="content" source="../../../assets/videos/dynamic-me-jit-flow.gif" alt-text="GIF affiche le flux utilisateur pour une extension de message dynamique et une installation JIT.":::

## <a name="see-also"></a>Voir aussi

* [Extensions de messages](../../what-are-messaging-extensions.md)
* [Actions universelles pour les cartes adaptatives](../../../task-modules-and-cards/cards/Universal-actions-for-adaptive-cards/Overview.md)
