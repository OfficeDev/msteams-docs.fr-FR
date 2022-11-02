---
title: Actions universelles pour les extensions de message basées sur la recherche
author: v-ypalikila
description: Dans cet article, découvrez les actions universelles et l’actualisation automatique des cartes adaptatives dans les extensions de message basées sur la recherche.
ms.topic: conceptual
ms.author: v-ypalikila
ms.localizationpriority: medium
ms.openlocfilehash: 18f5b783797d69144aac82e5ebd95fc30dad57a2
ms.sourcegitcommit: 9ea9a70d2591bce6b8c980d22014e160f7b45f91
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/02/2022
ms.locfileid: "68819967"
---
# <a name="universal-actions-for-search-based-message-extensions"></a>Actions universelles pour les extensions de message basées sur la recherche

Les cartes adaptatives dans les extensions de message basées sur la recherche prennent désormais en charge les actions universelles. Pour activer les actions universelles pour les extensions de message basées sur la recherche, l’application doit être conforme au [schéma des actions universelles pour les cartes adaptatives](../../../task-modules-and-cards/cards/Universal-actions-for-adaptive-cards/Work-with-Universal-Actions-for-Adaptive-Cards.md#schema-for-universal-actions-for-adaptive-cards) , ainsi qu’aux exigences suivantes :

1. L’application doit avoir un bot de conversation défini dans le manifeste de l’application.
1. Si vous avez déjà un bot conversationnel, vous devez utiliser le même bot que celui utilisé dans votre extension de message.
1. Si la carte est envoyée dans un groupe, l’application doit spécifier `team` ou `groupchat` étendue sur son bot dans le manifeste.

Exemple de schéma JSON avec les `team` valeurs et `groupchat` :

```json
{
    "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json",
    "manifestVersion": "1.11",
    "version": "1.0.0",
    "id": "%MICROSOFT-APP-ID%",
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

Activez l’actualisation automatique des cartes adaptatives dans les extensions de message basées sur la recherche afin que les utilisateurs voient toujours les dernières informations. Pour activer, définissez `userIds` le tableau au format ou `8:orgid:<AAD ID>` dans `29:<ID>` la `refresh` propriété . Pour plus d’informations, consultez [Utiliser des actions universelles pour les cartes adaptatives](../../../task-modules-and-cards/cards/Universal-actions-for-adaptive-cards/Work-with-Universal-Actions-for-Adaptive-Cards.md#user-ids-in-refresh).

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
> L’actualisation automatique est activée pour tous les utilisateurs de la conversation de groupe ou du canal avec *moins ou 60* utilisateurs. Pour les conversations (conversation de groupe ou canal) avec plus de 60 utilisateurs, les utilisateurs peuvent utiliser le bouton Actualiser dans le menu des options de message pour obtenir le résultat le plus récent.

Exemple de `Action.Execute` dans la `refresh` propriété :

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

Juste-à-temps (JIT) vous permet d’installer une extension de carte ou de message pour plusieurs utilisateurs dans une conversation de groupe ou un canal. Afin de prendre en charge les actions universelles dans les extensions de message basées sur la recherche, votre bot est ajouté à la conversation où la carte (avec `Action.Execute`) est envoyée par l’utilisateur.

Lorsqu’un utilisateur sélectionne une carte et l’envoie dans une conversation de groupe ou un canal, une invite d’installation **JIT** s’affiche. Une fois que l’utilisateur a sélectionné l’option **d’envoi** , l’application est ajoutée pour tous les utilisateurs de la conversation ou du canal en arrière-plan.

> [!NOTE]
> Pour les applications qui n’ont `Action.Execute` pas de schéma et `refresh` définis, l’invite d’installation n’est pas affichée aux utilisateurs.

Exemple de flux d’utilisateur d’installation me et JIT dynamique :

  :::image type="content" source="../../../assets/videos/dynamic-me-jit-flow.gif" alt-text="GIF affiche le flux utilisateur pour une extension de message dynamique et une installation JIT.":::

## <a name="see-also"></a>Voir aussi

* [Extensions de messages](../../what-are-messaging-extensions.md)
* [Cartes adaptatives](../../../task-modules-and-cards/what-are-cards.md#adaptive-cards)
* [Actions universelles pour les cartes adaptatives](../../../task-modules-and-cards/cards/Universal-actions-for-adaptive-cards/Overview.md)
