---
title: Ajouter un menu bot
description: Décrit comment créer des menus pour les bots dans Microsoft Teams
keywords: équipes bots menus création
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

Pour faciliter la découverte et aider à éduquer les utilisateurs sur les fonctionnalités de votre bot, vous pouvez maintenant ajouter des menus qui font surface chaque fois que l’utilisateur interagit avec votre bot. Le menu affichera le texte de commande et fournira également du texte d’aide, comme un exemple d’utilisation ou une description du but de la commande.

![Capture d’écran du menu bot](~/assets/images/bots/bot-menus-bot-menu-sample.png)

Lorsqu’un utilisateur sélectionne un élément de menu, la chaîne de commande est insérée dans la boîte de texte pour faciliter l’achèvement par l’utilisateur du message bot.

## <a name="bot-menu-support-on-teams-mobile-app"></a>Prise en charge du menu Bot Teams application mobile
> [!NOTE] 
> Les menus Bot ne sont pas affichés sur les appareils mobiles.

## <a name="app-manifest"></a>Manifeste d'application

Pour créer un menu bot, ajoutez un nouvel [`commandLists`](~/resources/schema/manifest-schema.md#botscommandlists) objet au manifeste de votre application sous la section bot. Vous pouvez déclarer des menus individuels avec des commandes distinctes pour chaque champ d’application de votre bot prend en charge ( `personal` , ou ) Chaque menu prend en charge `groupChat` `team` jusqu’à 10 commandes.

### <a name="manifest-excerpt---single-menu-for-both-scopes"></a>Extrait manifeste - menu unique pour les deux étendues

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

### <a name="manifest-excerpt---separate-menu-per-scope"></a>Extrait manifeste - menu séparé par portée

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

## <a name="best-practices"></a>Bonnes pratiques

* Restez simple : le menu bot est destiné à présenter les capacités clés de votre bot.
* Gardez-le court : les options de menu ne doivent pas être des instructions de langage naturel extrêmement longues et complexes - elles doivent être des commandes simples.
* Toujours disponible : les actions/commandes du menu Bot doivent toujours être invoqueables, quel que soit l’état de la conversation ou le dialogue dans le bot.
