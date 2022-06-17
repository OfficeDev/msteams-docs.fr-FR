---
title: Ajouter un menu bot
description: Dans ce module, découvrez comment ajouter un menu bot dans Microsoft Teams et créer des menus pour les bots dans Microsoft Teams
ms.topic: how-to
ms.localizationpriority: medium
ms.date: 05/20/2019
ms.openlocfilehash: ed65699b930d3e5334dd7fbb03da18a1482d6e5d
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143381"
---
# <a name="add-a-bot-menu-in-microsoft-teams"></a>Ajouter un menu bot dans Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Pour faciliter la découverte et aider à informer les utilisateurs sur les fonctionnalités de votre bot, vous pouvez maintenant ajouter des menus qui apparaissent chaque fois que l’utilisateur interagit avec votre bot. Le menu affiche le texte de la commande et fournit également du texte d’aide, tel qu’un exemple d’utilisation ou une description de l’objectif de la commande.

![Capture d’écran du menu bot](~/assets/images/bots/bot-menus-bot-menu-sample.png)

Lorsqu’un utilisateur sélectionne un élément de menu, la chaîne de commande est insérée dans la zone de texte pour faciliter la saisie semi-automatique du message du bot par l’utilisateur.

## <a name="bot-menu-support-on-teams-mobile-app"></a>Prise en charge du menu Bot sur Teams application mobile

> [!NOTE]
> Les menus bot ne sont pas affichés sur les appareils mobiles.

## <a name="app-manifest"></a>Manifeste d'application

Pour créer un menu bot, ajoutez un nouvel [`commandLists`](~/resources/schema/manifest-schema.md#botscommandlists) objet au manifeste de votre application sous la section bot. Vous pouvez déclarer des menus individuels avec des commandes distinctes pour chaque étendue prise en charge par votre bot (`personal`, `groupChat`ou `team`) Chaque menu prend en charge jusqu’à 10 commandes.

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

### <a name="manifest-excerpt---separate-menu-per-scope"></a>Extrait de manifeste : menu distinct par étendue

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

* Restez simple : le menu du bot est destiné à présenter les fonctionnalités clés de votre bot.
* Restez bref : les options de menu ne doivent pas être des instructions en langage naturel extrêmement longues et complexes . Il doit s’agir de commandes simples.
* Toujours disponible : les actions/commandes du menu bot doivent toujours être appelées, quel que soit l’état de la conversation ou la boîte de dialogue dans lequel se trouve le bot.
