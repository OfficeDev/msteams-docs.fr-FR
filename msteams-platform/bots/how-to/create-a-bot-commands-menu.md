---
title: Créer un menu de commandes pour votre robot
author: clearab
description: Procédure de création d’un menu de commandes pour votre robot Microsoft teams
ms.topic: overview, command menu
ms.author: anclear
ms.openlocfilehash: ccbacc6ec6f18a38512d81dc898d0b14357d6ef7
ms.sourcegitcommit: bfdcd122b6b4ffc52d92320d4741f870c07f0542
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/02/2020
ms.locfileid: "49552485"
---
# <a name="bot-command-menus"></a>Menus de la commande bot

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

> [!Note]
> Les menus de bot n’apparaissent pas sur les clients mobiles.

Add Command menu for your bot vous permet de définir un ensemble de commandes clés auxquelles votre bot peut toujours répondre. La liste des commandes est présentée à l’utilisateur au-dessus de la zone de message de composition lorsqu’ils contournent votre robot. La sélection d’une commande dans la liste entraîne l’insertion de la chaîne de commande dans la boîte de message de composition, puis tous les utilisateurs ont besoin de l’option **Envoyer**.

![Menu de commandes bot](./conversations/media/bot-menu-sample.png)

## <a name="create-a-command-menu-for-your-bot"></a>Créer un menu de commandes pour votre robot

Les menus de commandes sont définis dans le manifeste de votre application. Vous pouvez utiliser app Studio pour vous aider à les créer ou les ajouter manuellement.

### <a name="creating-a-command-menu-for-your-bot-using-app-studio"></a>Création d’un menu de commandes pour votre bot à l’aide d’App Studio

Les instructions fournies ici supposent que vous modifiez un manifeste d’application existant. Les étapes d’ajout d’un menu de commandes sont les mêmes, que vous soyez en train de créer un nouveau manifeste ou d’en modifier un existant.

1. Ouvrez l’application Studio à partir du... menu débordement sur le rail de navigation gauche. Si vous n’avez pas disponible App Studio, vous pouvez le télécharger. Pour plus d’informations sur l’utilisation d’App Studio, voir [Installing App Studio](https://aka.ms/teams-app-studio#installing-app-studio) .

    ![App Studio](./conversations/media/AppStudio.png)

2. Une fois dans App Studio, sélectionnez l’onglet **éditeur de manifeste** .

3. Dans la colonne de gauche de la vue de l’éditeur de manifeste dans la section **fonctionnalités** , sélectionnez **bots**.

4. Dans la colonne de droite de la vue de l’éditeur de manifeste dans la section **commandes** , cliquez sur le bouton **Ajouter** .

    ![Bouton Ajouter du menu de commandes d’App Studio](./conversations/media/AppStudio-CommandMenu-Add.png)

5. L’écran **nouvelle commande** s’affiche. Entrez le **texte de commande** qui doit apparaître en tant que commande de menu, ainsi que le **texte d’aide** qui doit apparaître directement sous le texte de commande dans le menu. Cela doit être une brève explication de l’objectif de la commande.

6. Ensuite, sélectionnez la ou les étendues dans lesquelles vous souhaitez que ce menu de commandes s’affiche, puis cliquez sur le bouton **Enregistrer** .

    ![Bouton Ajouter du menu de commandes d’App Studio](./conversations/media/AppStudio-NewCommandMenu.png)

### <a name="creating-a-command-menu-for-your-bot-by-editing-manifestjson"></a>Création d’un menu de commandes pour votre bot en modifiant **Manifest.js**

Une autre approche valide pour la création d’un menu de commandes consiste à le créer directement dans le fichier manifeste lors du développement du code source de votre robot. Voici quelques éléments à garder à l’esprit lors de l’utilisation de cette approche :

1. Chaque menu prend en charge jusqu’à 10 commandes.

2. Vous pouvez créer un seul menu de commandes qui fonctionne dans toutes les étendues.

3. Vous pouvez créer un autre menu de commandes pour chaque étendue

#### <a name="manifest-example---single-menu-for-both-scopes"></a>Exemple de manifeste-menu unique pour les deux étendues

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

#### <a name="manifest-example---menu-for-each-scope"></a>Exemple de manifeste-menu pour chaque étendue

```json
{
  ...
  "bots":[
    {
      "botId":"<Microsoft app ID for your bot>",
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

## <a name="handling-menu-commands-in-your-bot-code"></a>Gestion des commandes de menu dans votre code de robot

Les robots d’un groupe ou d’un canal répondent uniquement lorsqu’ils sont mentionnés (« @botname ») dans un message. Par conséquent, chaque message reçu par un bot dans une étendue de groupe ou de canal contiendra son propre nom dans le texte du message renvoyé. Vous devez veiller à ce que les handles d’analyse de messages qui précèdent la commande renvoyée soient pris en charge.

> **Note** Pour gérer les commandes dans le code, celles-ci sont envoyées à votre bot sous la forme d’un message ordinaire. Par conséquent, vous devez les gérer comme vous le feriez pour n’importe quel autre message de la part de vos utilisateurs. Il s’agit uniquement d’un traitement de l’interface utilisateur qui insère du texte préconfiguré dans la zone de texte. L’utilisateur doit alors envoyer ce texte comme s’il s’agissait de n’importe quel autre message.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

Vous pouvez analyser la partie **\@ mention** du texte du message à l’aide d’une méthode statique fournie avec Microsoft bot Framework, une méthode de la `Activity` classe nommée `RemoveRecipientMention` .

```csharp
var modifiedText = turnContext.Activity.RemoveRecipientMention();
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

Vous pouvez analyser la partie **\@ mention** du texte du message à l’aide d’une méthode statique fournie avec Microsoft bot Framework, une méthode de la `TurnContext` classe nommée `removeMentionText` .

```javascript
const modifiedText = TurnContext.removeMentionText(turnContext.activity, turnContext.activity.recipient.id);
```

# <a name="python"></a>[Python](#tab/python)


Vous pouvez analyser la partie **@Mention** du texte du message à l’aide d’une méthode statique fournie avec Microsoft bot Framework, une méthode de la `TurnContext` classe nommée `remove_recipient_mention` .

```python
modified_text = TurnContext.remove_recipient_mention(turn_context.activity)
```

* * *

## <a name="command-menu-best-practices"></a>Meilleures pratiques du menu de commandes

* **Restez simple**: le menu robot est conçu pour présenter les fonctionnalités clés de votre bot.
* **Maintenez-le court**: les options de menu ne doivent pas être extrêmement longues et les instructions complexes en langage naturel : elles doivent être des commandes simples.
* **Conservez-le invokable**: les actions/commandes du menu bot doivent toujours être disponibles, quel que soit l’état de la conversation ou la boîte de dialogue dans laquelle se trouve le robot.

> **Note** Si vous supprimez des commandes de votre manifeste, vous devrez redéployer votre application pour que les modifications prennent effet. En règle générale, toutes les modifications apportées au manifeste le requièrent.
