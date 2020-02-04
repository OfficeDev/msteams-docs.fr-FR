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
# <a name="add-a-bot-menu-in-microsoft-teams"></a><span data-ttu-id="3b9e2-104">Ajouter un menu bot dans Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="3b9e2-104">Add a bot menu in Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="3b9e2-105">Pour faciliter la découverte et aider les utilisateurs à se servir de la fonctionnalité de votre robot, vous pouvez désormais ajouter des menus qui se trouvent à chaque fois que l’utilisateur interagit avec votre bot.</span><span class="sxs-lookup"><span data-stu-id="3b9e2-105">To aid discovery and to help educate users about your bot’s functionality, you can now add menus that surface whenever the user interacts with your bot.</span></span> <span data-ttu-id="3b9e2-106">Le menu affiche le texte de la commande et fournit également un texte d’aide, tel qu’un exemple d’utilisation ou une description de l’objectif de la commande.</span><span class="sxs-lookup"><span data-stu-id="3b9e2-106">The menu will show the command text and also provide help text, such as a usage example or description of the command’s purpose.</span></span>

![Capture d’écran du menu du robot](~/assets/images/bots/bot-menus-bot-menu-sample.png)

<span data-ttu-id="3b9e2-108">Lorsqu’un utilisateur sélectionne un élément de menu, la chaîne de commande est insérée dans la zone de texte pour aider l’utilisateur à terminer le message bot.</span><span class="sxs-lookup"><span data-stu-id="3b9e2-108">When a user selects a menu item, the command string is inserted into the text box to aid in user completion of the bot message.</span></span>

## <a name="bot-menu-support-on-teams-mobile-app"></a><span data-ttu-id="3b9e2-109">Prise en charge du menu bot sur l’application mobile teams</span><span class="sxs-lookup"><span data-stu-id="3b9e2-109">Bot menu support on Teams mobile app</span></span>
> [!NOTE] 
> <span data-ttu-id="3b9e2-110">Les menus de bot ne s’affichent pas sur les appareils mobiles</span><span class="sxs-lookup"><span data-stu-id="3b9e2-110">Bot menus are not displayed on mobile devices</span></span>

## <a name="app-manifest"></a><span data-ttu-id="3b9e2-111">Manifeste de l’application</span><span class="sxs-lookup"><span data-stu-id="3b9e2-111">App manifest</span></span>

<span data-ttu-id="3b9e2-112">Pour créer un menu de robot, ajoutez un [`commandLists`](~/resources/schema/manifest-schema.md#botscommandlists) nouvel objet à votre manifeste d’application sous la section bot.</span><span class="sxs-lookup"><span data-stu-id="3b9e2-112">To create a bot menu, add a new [`commandLists`](~/resources/schema/manifest-schema.md#botscommandlists) object to your app manifest under the bot section.</span></span> <span data-ttu-id="3b9e2-113">Vous pouvez déclarer des menus individuels avec des commandes distinctes pour chaque étendue prise en`personal`charge `groupChat` par `team`votre bot (ou) chaque menu prend en charge jusqu’à 10 commandes.</span><span class="sxs-lookup"><span data-stu-id="3b9e2-113">You can declare individual menus with separate commands for each scope your bot supports (`personal`, `groupChat` or `team`) Each menu supports up to 10 commands.</span></span>

### <a name="manifest-excerpt---single-menu-for-both-scopes"></a><span data-ttu-id="3b9e2-114">Extrait de manifeste-menu unique pour les deux étendues</span><span class="sxs-lookup"><span data-stu-id="3b9e2-114">Manifest excerpt - single menu for both scopes</span></span>

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

### <a name="manifest-excerpt---separate-menu-per-scope"></a><span data-ttu-id="3b9e2-115">Extrait de manifeste-menu distinct par étendue</span><span class="sxs-lookup"><span data-stu-id="3b9e2-115">Manifest excerpt - separate menu per scope</span></span>

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

## <a name="best-practices"></a><span data-ttu-id="3b9e2-116">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="3b9e2-116">Best practices</span></span>

* <span data-ttu-id="3b9e2-117">Restez simple : le menu robot est conçu pour présenter les fonctionnalités clés de votre bot.</span><span class="sxs-lookup"><span data-stu-id="3b9e2-117">Keep it simple: The bot menu is meant to present the key capabilities of your bot.</span></span>
* <span data-ttu-id="3b9e2-118">Maintenez-le court : les options de menu ne doivent pas être très longues et les instructions complexes en langage naturel : elles doivent être des commandes simples.</span><span class="sxs-lookup"><span data-stu-id="3b9e2-118">Keep it short: Menu options shouldn’t be extremely long and complex natural language statements - they should be simple commands.</span></span>
* <span data-ttu-id="3b9e2-119">Toujours disponible : les actions/commandes du menu bot doivent être toujours invokable, quel que soit l’état de la conversation ou la boîte de dialogue dans laquelle se trouve le robot.</span><span class="sxs-lookup"><span data-stu-id="3b9e2-119">Always available: Bot menu actions/commands should be always invokable, regardless of the state of the conversation or the dialog the bot is in.</span></span>
