---
title: Ajouter un menu bot
description: Décrit comment créer des menus pour les bots dans Microsoft Teams
keywords: Création de menus de bots Teams
ms.topic: how-to
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: f4190d0b21abbe00994e082000202b7bc65b917c
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019768"
---
# <a name="add-a-bot-menu-in-microsoft-teams"></a><span data-ttu-id="1161f-104">Ajouter un menu bot dans Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="1161f-104">Add a bot menu in Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="1161f-105">Pour faciliter la découverte et former les utilisateurs sur les fonctionnalités de votre bot, vous pouvez désormais ajouter des menus qui s'surfacent chaque fois que l'utilisateur interagit avec votre bot.</span><span class="sxs-lookup"><span data-stu-id="1161f-105">To aid discovery and to help educate users about your bot’s functionality, you can now add menus that surface whenever the user interacts with your bot.</span></span> <span data-ttu-id="1161f-106">Le menu affiche le texte de la commande et fournit également un texte d'aide, tel qu'un exemple d'utilisation ou une description de l'objectif de la commande.</span><span class="sxs-lookup"><span data-stu-id="1161f-106">The menu will show the command text and also provide help text, such as a usage example or description of the command’s purpose.</span></span>

![Capture d'écran du menu bot](~/assets/images/bots/bot-menus-bot-menu-sample.png)

<span data-ttu-id="1161f-108">Lorsqu'un utilisateur sélectionne un élément de menu, la chaîne de commande est insérée dans la zone de texte pour aider l'utilisateur à terminer le message du bot.</span><span class="sxs-lookup"><span data-stu-id="1161f-108">When a user selects a menu item, the command string is inserted into the text box to aid in user completion of the bot message.</span></span>

## <a name="bot-menu-support-on-teams-mobile-app"></a><span data-ttu-id="1161f-109">Prise en charge du menu bot sur l'application mobile Teams</span><span class="sxs-lookup"><span data-stu-id="1161f-109">Bot menu support on Teams mobile app</span></span>
> [!NOTE] 
> <span data-ttu-id="1161f-110">Les menus bot ne sont pas affichés sur les appareils mobiles</span><span class="sxs-lookup"><span data-stu-id="1161f-110">Bot menus are not displayed on mobile devices</span></span>

## <a name="app-manifest"></a><span data-ttu-id="1161f-111">Manifeste de l'application</span><span class="sxs-lookup"><span data-stu-id="1161f-111">App manifest</span></span>

<span data-ttu-id="1161f-112">Pour créer un menu bot, ajoutez un nouvel objet au manifeste [`commandLists`](~/resources/schema/manifest-schema.md#botscommandlists) de votre application sous la section bot.</span><span class="sxs-lookup"><span data-stu-id="1161f-112">To create a bot menu, add a new [`commandLists`](~/resources/schema/manifest-schema.md#botscommandlists) object to your app manifest under the bot section.</span></span> <span data-ttu-id="1161f-113">Vous pouvez déclarer des menus individuels avec des commandes distinctes pour chaque étendue que votre bot prend en charge ( ou ) Chaque menu prend en charge jusqu'à `personal` `groupChat` `team` 10 commandes.</span><span class="sxs-lookup"><span data-stu-id="1161f-113">You can declare individual menus with separate commands for each scope your bot supports (`personal`, `groupChat` or `team`) Each menu supports up to 10 commands.</span></span>

### <a name="manifest-excerpt---single-menu-for-both-scopes"></a><span data-ttu-id="1161f-114">Extrait de manifeste - menu unique pour les deux étendues</span><span class="sxs-lookup"><span data-stu-id="1161f-114">Manifest excerpt - single menu for both scopes</span></span>

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

### <a name="manifest-excerpt---separate-menu-per-scope"></a><span data-ttu-id="1161f-115">Extrait de manifeste - menu distinct par étendue</span><span class="sxs-lookup"><span data-stu-id="1161f-115">Manifest excerpt - separate menu per scope</span></span>

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

## <a name="best-practices"></a><span data-ttu-id="1161f-116">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="1161f-116">Best practices</span></span>

* <span data-ttu-id="1161f-117">Restez simple : le menu bot est destiné à présenter les fonctionnalités clés de votre bot.</span><span class="sxs-lookup"><span data-stu-id="1161f-117">Keep it simple: The bot menu is meant to present the key capabilities of your bot.</span></span>
* <span data-ttu-id="1161f-118">N'oubliez pas que les options de menu ne doivent pas être des instructions de langage naturel très longues et complexes, mais des commandes simples.</span><span class="sxs-lookup"><span data-stu-id="1161f-118">Keep it short: Menu options shouldn’t be extremely long and complex natural language statements - they should be simple commands.</span></span>
* <span data-ttu-id="1161f-119">Toujours disponible : les actions/commandes du menu bot doivent toujours être invocables, quel que soit l'état de la conversation ou la boîte de dialogue dans le bot.</span><span class="sxs-lookup"><span data-stu-id="1161f-119">Always available: Bot menu actions/commands should be always invokable, regardless of the state of the conversation or the dialog the bot is in.</span></span>
