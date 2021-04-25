---
title: Créer un menu de commandes pour votre bot
author: clearab
description: Comment créer un menu de commandes pour votre bot Microsoft Teams
ms.topic: how-to
ms.author: anclear
ms.openlocfilehash: a4d53d8287d425120d24f559b8ffffabebdbcfb4
ms.sourcegitcommit: dd2220f691029d043aaddfc7c229e332735acb1d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2021
ms.locfileid: "51995896"
---
# <a name="bot-command-menus"></a>Menus de commande du bot

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

> [!Note]
> Les menus bot n'apparaissent pas sur les clients mobiles.

Pour définir un ensemble de commandes principales à qui votre bot peut répondre, vous pouvez ajouter un menu de commandes avec une liste déroulante de commandes pour votre bot. La liste des commandes est présentée aux utilisateurs dans la zone composer un message lorsqu'ils sont en conversation avec votre bot. Sélectionnez une commande dans la liste pour insérer la chaîne de commande dans la zone composer un message et sélectionnez **Envoyer**.

![Menu de commande bot](./conversations/media/bot-menu-sample.png)

## <a name="create-a-command-menu-for-your-bot"></a>Créer un menu de commandes pour votre bot

Les menus de commande sont définis dans le manifeste de votre application. Vous pouvez utiliser **App Studio** pour les créer ou les ajouter manuellement dans le manifeste de l'application.

### <a name="create-a-command-menu-for-your-bot-using-app-studio"></a>Créer un menu de commandes pour votre bot à l'aide d'App Studio

Pour créer un menu de commandes pour votre bot, vous devez modifier un manifeste d'application existant. Les étapes d'ajout d'un menu de commandes sont les mêmes, que vous créez un nouveau manifeste ou que vous en modifiiez un existant.

**Pour créer un menu de commandes pour votre bot à l'aide d'App Studio**

1. Ouvrez Teams et **sélectionnez Applications** dans le volet gauche. Dans la page **Applications,** recherchez **App Studio** et sélectionnez **Ouvrir.** 
   > [!NOTE]
   > Si vous n'avez **pas App Studio,** vous pouvez le télécharger. Pour plus d'informations, [voir l'installation d'App Studio.](~/concepts/build-and-test/app-studio-overview.md#installing-app-studio)

    ![App Studio](./conversations/media/AppStudio.png)

2. Dans **App Studio,** sélectionnez **l'onglet Éditeur de** manifeste. Si vous n'avez pas de package d'application existant, vous pouvez créer ou importer une application existante. Pour plus d'informations, voir [mettre à jour un package d'application.](~/tutorials/get-started-dotnet-app-studio.md#use-app-studio-to-update-the-app-package)

3. Dans le volet gauche de l'éditeur **de manifeste** et dans la **section** **Fonctionnalités,** sélectionnez Bots .

4. Dans le volet droit de l'éditeur **de manifeste** et dans la section **Commandes,** sélectionnez **Ajouter**. **L'écran Nouvelle commande** s'affiche.

    ![Bouton Ajouter du menu commandes App Studio](./conversations/media/AppStudio-CommandMenu-Add.png)

5. Entrez le **texte de commande** qui doit apparaître comme menu de commande pour votre bot.

6. Entrez le **texte d'aide** qui doit apparaître sous le texte de commande dans le menu. **Le texte d'aide** doit être une brève explication de l'objectif de la commande.

7. Cochez **les cases** d'étendue pour sélectionner l'endroit où ce menu de commande doit apparaître, puis sélectionnez **Enregistrer.**

    ![Bouton de menu Nouvelles commandes App Studio](./conversations/media/AppStudio-NewCommandMenu.png)

### <a name="create-a-command-menu-for-your-bot-by-editing-manifestjson"></a>Créer un menu de commandes pour votre bot en le Manifest.jssur

Une autre façon de créer un menu de commandes consiste à le créer directement dans le fichier manifeste lors du développement de votre code source de bot. Pour utiliser cette méthode, suivez les points ci-après :

* Chaque menu prend en charge jusqu'à dix commandes.
* Créez un menu de commande unique qui fonctionne dans toutes les étendues.
* Créez un menu de commandes différent pour chaque étendue.

#### <a name="manifest-example-for-single-menu-for-both-scopes"></a>Exemple de manifeste pour un menu unique pour les deux étendues

L'exemple de code de manifeste pour un menu unique pour les deux étendues est le suivant :

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

#### <a name="manifest-example-for-the-menu-for-each-scope"></a>Exemple de manifeste pour le menu pour chaque étendue

L'exemple de code de manifeste pour le menu pour chaque étendue est le suivant :

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

Vous devez gérer les commandes de menu dans le code de votre bot lorsque vous traitez les messages des utilisateurs. Vous pouvez gérer les commandes de menu dans le code de votre bot en parant la **\@ partie Mention** du texte du message.

## <a name="handle-menu-commands-in-your-bot-code"></a>Gérer les commandes de menu dans le code de votre bot

Les bots d'un groupe ou d'un canal répondent uniquement lorsqu'ils sont mentionnés `@botname` dans un message. Chaque message reçu par un bot dans une étendue de groupe ou de canal contient son nom dans le texte du message renvoyé. Avant de gérer la commande renvoyée, l'utilisation de votre message doit gérer le message reçu par un bot avec son nom.

> [!NOTE]
> Pour gérer les commandes dans le code, elles sont envoyées à votre bot en tant que message normal. Vous devez les gérer comme vous le feriez pour tout autre message de vos utilisateurs. Les commandes du code insèrent du texte pré-configuré dans la zone de texte. L'utilisateur doit ensuite envoyer ce texte comme il le fait pour tout autre message.

# <a name="c"></a>[C#](#tab/dotnet)

Vous pouvez analyser la partie **\@ Mention** du texte du message à l'aide d'une méthode statique fournie avec Microsoft Bot Framework. Il s'agit d'une méthode de `Activity` la classe nommée `RemoveRecipientMention` .

Le C# code pour l'utilisation de la partie **\@ Mention** du texte du message est le suivant :

```csharp
var modifiedText = turnContext.Activity.RemoveRecipientMention();
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

Vous pouvez analyser la **\@ partie Mention** du texte du message à l'aide d'une méthode statique fournie avec Bot Framework. Il s'agit d'une méthode de `TurnContext` la classe nommée `removeMentionText` .

Le code JavaScript pour l'utilisation de la **\@ partie Mention** du texte du message est le suivant :

```javascript
const modifiedText = TurnContext.removeMentionText(turnContext.activity, turnContext.activity.recipient.id);
```

# <a name="python"></a>[Python](#tab/python)

Vous pouvez l'@Mention **partie** du texte du message à l'aide d'une méthode statique fournie avec Bot Framework. Il s'agit d'une méthode de `TurnContext` la classe nommée `remove_recipient_mention` .

Le code Python pour l'extrait de la **\@ partie Mention** du texte du message est le suivant :

```python
modified_text = TurnContext.remove_recipient_mention(turn_context.activity)
```

* * *

Pour activer le bon fonctionnement de votre code bot, vous devez suivre quelques meilleures pratiques.

## <a name="command-menu-best-practices"></a>Meilleures pratiques en matière de menu de commandes

Voici les meilleures pratiques en matière de menu de commandes :

* Restez simple : le menu bot est destiné à présenter les fonctionnalités clés de votre bot.
* Restez bref : les options de menu ne doivent pas être longues et ne doivent pas être des instructions de langage naturel complexes. Ce doivent être des commandes simples.
* Restez invocable : les commandes ou les actions de menu bot doivent toujours être disponibles, quel que soit l’état de la conversation ou la boîte de dialogue dans le bot.

> [!NOTE]
> Si vous supprimez des commandes de votre manifeste, vous devez redéployer votre application pour implémenter les modifications. En règle générale, les modifications apportées au manifeste vous obligent à redéployer votre application.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Conversations de groupe et de canal](~/bots/how-to/conversations/channel-and-group-conversations.md)
