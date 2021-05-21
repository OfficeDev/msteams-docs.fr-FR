---
title: Ajouter un menu bot
description: Décrit comment créer des menus pour des bots dans Microsoft Teams
keywords: Création de menus de bots Teams
ms.topic: how-to
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: da6f36e1b7071b92f6411ab7d2afdccb795946b7
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566767"
---
# <a name="add-a-bot-menu-in-microsoft-teams"></a>Ajouter un menu bot dans Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Pour faciliter la découverte et former les utilisateurs sur les fonctionnalités de votre bot, vous pouvez désormais ajouter des menus qui s’surfacent chaque fois que l’utilisateur interagit avec votre bot. Le menu affiche le texte de la commande et fournit également un texte d’aide, tel qu’un exemple d’utilisation ou une description de l’objectif de la commande.

![Capture d’écran du menu bot](~/assets/images/bots/bot-menus-bot-menu-sample.png)

Lorsqu’un utilisateur sélectionne un élément de menu, la chaîne de commande est insérée dans la zone de texte pour aider l’utilisateur à terminer le message du bot.

## <a name="bot-menu-support-on-teams-mobile-app"></a>Prise en charge du menu bot sur Teams application mobile
> [!NOTE] 
> Les menus bot ne sont pas affichés sur les appareils mobiles.

## <a name="app-manifest"></a>Manifeste d'application

Pour créer un menu bot, ajoutez un nouvel objet au manifeste [`commandLists`](~/resources/schema/manifest-schema.md#botscommandlists) de votre application sous la section bot. Vous pouvez déclarer des menus individuels avec des commandes distinctes pour chaque étendue que votre bot prend en charge ( ou ) Chaque menu prend en charge jusqu’à `personal` `groupChat` `team` 10 commandes.

### <a name="manifest-excerpt---single-menu-for-both-scopes"></a>Extrait de manifeste - menu unique pour les deux étendues

```json
{
  ⋮
  "bots":[
    {
      "botId":"[Microsoft App ID for your bot]",
      "scopes": [
        "personal",
        "team"
      ],
      "commandLists":[
        {
          "scopes":[
            "team",
            "personal"
          ],
          "commands":[
            {
              "title":"Help",
              "description":"Displays this help message"
            },
            {
              "title":"Search Flights",
              "description":"Search flights from Seattle to Phoenix May 2-5 departing after 3pm"
            },
            {
              "title":"Search Hotels",
              "description":"Search hotels in Portland tonight"
            },
            {
              "title":"Best Time to Fly",
              "description":"Best time to fly to London for a 5 day trip this summer"
            }
          ]
        }
      ]
    }
  ],
  ...
}
```

### <a name="manifest-excerpt---separate-menu-per-scope"></a>Extrait de manifeste - menu distinct par étendue

```json
{
  ...
  "bots":[
    {
      "botId":"[Microsoft app ID for your bot]",
      "scopes": [
        "groupChat",
        "team"
      ],
      "commandLists":[
        {
          "scopes":[
            "team"
          ],
          "commands":[
            {
            "title":"help",
            "description":"Displays this help message for channels"
            }
          ]
        },
        {
          "scopes":[
            "groupChat"
          ],
          "commands":[
            {
            "title":"help",
            "description":"Displays this help message for group chat"
            }
          ]
        }
      ]
    }
  ],
  ...
}
```

## <a name="best-practices"></a>Meilleures pratiques

* Restez simple : le menu bot est destiné à présenter les fonctionnalités clés de votre bot.
* N’oubliez pas que les options de menu ne doivent pas être des instructions de langage naturel très longues et complexes, mais des commandes simples.
* Toujours disponible : les actions/commandes du menu bot doivent toujours être invocables, quel que soit l’état de la conversation ou la boîte de dialogue dans le bot.
