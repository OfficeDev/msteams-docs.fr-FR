---
title: Ajouter un menu robot
description: Décrit comment créer des menus pour les robots dans Microsoft teams
keywords: création de menus robots teams
ms.date: 05/20/2019
ms.openlocfilehash: 36a224dc21cccc5fcd1047e45e3d749e7ca19ea7
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673576"
---
# <a name="add-a-bot-menu-in-microsoft-teams"></a>Ajouter un menu bot dans Microsoft teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Pour faciliter la découverte et aider les utilisateurs à se servir de la fonctionnalité de votre robot, vous pouvez désormais ajouter des menus qui se trouvent à chaque fois que l’utilisateur interagit avec votre bot. Le menu affiche le texte de la commande et fournit également un texte d’aide, tel qu’un exemple d’utilisation ou une description de l’objectif de la commande.

![Capture d’écran du menu du robot](~/assets/images/bots/bot-menus-bot-menu-sample.png)

Lorsqu’un utilisateur sélectionne un élément de menu, la chaîne de commande est insérée dans la zone de texte pour aider l’utilisateur à terminer le message bot.

## <a name="bot-menu-support-on-teams-mobile-app"></a>Prise en charge du menu bot sur l’application mobile teams
> [!NOTE] 
> Les menus de bot ne s’affichent pas sur les appareils mobiles

## <a name="app-manifest"></a>Manifeste de l’application

Pour créer un menu de robot, ajoutez un [`commandLists`](~/resources/schema/manifest-schema.md#botscommandlists) nouvel objet à votre manifeste d’application sous la section bot. Vous pouvez déclarer des menus individuels avec des commandes distinctes pour chaque étendue prise en`personal`charge `groupChat` par `team`votre bot (ou) chaque menu prend en charge jusqu’à 10 commandes.

### <a name="manifest-excerpt---single-menu-for-both-scopes"></a>Extrait de manifeste-menu unique pour les deux étendues

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

### <a name="manifest-excerpt---separate-menu-per-scope"></a>Extrait de manifeste-menu distinct par étendue

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

* Restez simple : le menu robot est conçu pour présenter les fonctionnalités clés de votre bot.
* Maintenez-le court : les options de menu ne doivent pas être très longues et les instructions complexes en langage naturel : elles doivent être des commandes simples.
* Toujours disponible : les actions/commandes du menu bot doivent être toujours invokable, quel que soit l’état de la conversation ou la boîte de dialogue dans laquelle se trouve le robot.
