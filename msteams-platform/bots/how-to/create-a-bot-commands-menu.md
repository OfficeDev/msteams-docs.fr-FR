---
title: Créer un menu de commandes pour votre bot
author: surbhigupta
description: Découvrez comment créer un menu de commandes pour votre bot Microsoft Teams avec des exemples de code.
ms.topic: how-to
ms.localizationpriority: medium
ms.author: anclear
keywords: '@mention de conversation de composition de message dans le menu commande'
ms.openlocfilehash: 6d61b7566dd0dcb25fae94bf43f2f19bd219e9b0
ms.sourcegitcommit: ff31cbe4840191f004d8fc61dd4fd93d35fcaecb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/07/2022
ms.locfileid: "65938939"
---
# <a name="bot-command-menus"></a>Menus de commandes du bot

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Pour définir un ensemble de commandes principales auxquelles votre bot peut répondre, vous pouvez ajouter un menu de commandes avec une liste déroulante de commandes pour votre bot. La liste des commandes est présentée aux utilisateurs dans la zone de rédaction du message lorsqu’ils sont en conversation avec votre bot. Sélectionnez une commande dans la liste pour insérer la chaîne de commande dans la zone composer le message, puis sélectionnez **Envoyer**.

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

![Menu commande bot](./conversations/media/bot-menu-sample.png)

# <a name="mobile"></a>[Mobile](#tab/mobile)

![Menu de commande du bot mobile](./conversations/media/mobile-bot-menu-sample.png)

* * *

## <a name="create-a-command-menu-for-your-bot"></a>Créer un menu de commandes pour votre bot

Les menus de commande sont définis dans le manifeste de votre application. Vous pouvez utiliser **App Studio** pour les créer ou les ajouter manuellement dans le manifeste de l’application.

### <a name="create-a-command-menu-for-your-bot-using-app-studio"></a>Créer un menu de commandes pour votre bot à l’aide d’App Studio

Un prérequis pour créer un menu de commande pour votre bot est que vous devez modifier un manifeste d’application existant. Les étapes d’ajout d’un menu de commande sont les mêmes, que vous créiez un nouveau manifeste ou que vous modifiiez un manifeste existant.

**Pour créer un menu de commandes pour votre bot à l’aide d’App Studio**

1. Ouvrez Teams et sélectionnez **Apps** dans le volet gauche. Dans la page **applications**, recherchez **App Studio**, puis sélectionnez **Ouvrir**.
    
   > [!WARNING]
   > Si vous utilisez App Studio, nous vous recommandons d’essayer le Developer Portal pour configurer, distribuer et gérer vos applications Teams. App Studio sera déconseillé d’ici le 30 juin 2022

   :::image type="content" source="/media/AppStudio.png" alt-text="l’installation d’app studio"lightbox="media/AppStudio.png"border="true":::

2. Dans **App Studio**, sélectionnez l’onglet de **Éditeur de manifeste**. Si vous n’avez pas de package d’application existant, vous pouvez créer ou importer une application existante. Pour plus d’informations, voir [Mettre à jour un package d’application](~/get-started/deploy-csharp-app-studio.md).

3. Dans le volet gauche de **l’éditeur de manifeste** et dans la section **fonctionnalités**, sélectionnez **Bots**.

4. Dans le volet droit de **Éditeur de manifeste** et dans la section **commandes**, sélectionnez **Ajouter**. L’écran **Nouvelle commande** s’affiche.

    :::image type="content" source="/media/AppStudio-CommandMenu-Add.png" alt-text="Sélectionnez le package d’application"lightbox="/media/AppStudio-CommandMenu-Add.png"border="true":::

5. Entrez le **texte de la commande** qui doit apparaître comme menu de commande pour votre bot.

6. Entrez le **texte d’aide** qui doit apparaître sous le texte de la commande dans le menu. **texte d’aide** doit être une brève explication de l’objectif de la commande.

7. Activez les cases à cocher **Étendue** pour sélectionner l’emplacement où ce menu de commandes doit apparaître, puis sélectionnez **Enregistrer**.

:::image type="content" source="/media/AppStudio-NewCommandMenu.png" alt-text="bouton de menu Nouvelles commandes App Studio"lightbox="/media/AppStudio-NewCommandMenu.png"border="true":::

### <a name="create-a-command-menu-for-your-bot-by-editing-manifestjson"></a>Créer un menu de commandes pour votre bot en modifiant Manifest.json

Une autre façon de créer un menu de commande consiste à le créer directement dans le fichier manifeste lors du développement de votre code source de bot. Pour utiliser cette méthode, suivez ces points :

* Chaque menu prend en charge jusqu’à dix commandes.
* Créez un menu de commandes unique qui fonctionne dans toutes les étendues.
* Créez un menu de commandes différent pour chaque étendue.

#### <a name="manifest-example-for-single-menu-for-both-scopes"></a>Exemple de manifeste pour un menu unique pour les deux étendues

L’exemple de code du manifeste pour un menu unique pour les deux étendues est le suivant :

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

L’exemple de code du manifeste pour le menu pour chaque étendue est le suivant :

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

Vous devez gérer les commandes de menu dans le code de votre bot à mesure que vous gérez les messages des utilisateurs. Vous pouvez gérer les commandes de menu dans le code de votre bot en analysant la **\@Mention** partie du texte du message.

## <a name="handle-menu-commands-in-your-bot-code"></a>Gérer les commandes de menu dans le code de votre bot

Les bots d’un groupe ou d’un canal répondent uniquement lorsqu’ils sont mentionnés `@botname` dans un message. Chaque message reçu par un bot dans une étendue de groupe ou de canal contient son nom dans le texte du message. Avant de gérer la commande retournée, votre analyse de message doit gérer le message reçu par un bot avec son nom.

> [!NOTE]
> Pour gérer les commandes dans le code, elles sont envoyées à votre bot en tant que message standard. Vous devez les gérer comme vous le feriez pour tout autre message de vos utilisateurs. Les commandes du code insèrent du texte préconfiguré dans la zone de texte. L’utilisateur doit ensuite envoyer ce texte comme il le fait pour tout autre message.

# <a name="c"></a>[C#](#tab/dotnet)

Vous pouvez analyser la **\@Mention** partie du texte du message à l’aide d’une méthode statique fournie avec le Microsoft Bot Framework. Il s’agit d’une méthode de la classe `Activity` nommée `RemoveRecipientMention`.

Le code C# permettant d’analyser la **\@Mention** partie du texte du message est la suivante :

```csharp
var modifiedText = turnContext.Activity.RemoveRecipientMention();
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

Vous pouvez analyser la **\@Mention** partie du texte du message à l’aide d’une méthode statique fournie avec le Bot Framework. Il s’agit d’une méthode de la classe `TurnContext` nommée `removeMentionText`.

Le code JavaScript permettant d’analyser la **\@mention** partie du texte du message est la suivante :

```javascript
const modifiedText = TurnContext.removeMentionText(turnContext.activity, turnContext.activity.recipient.id);
```

# <a name="python"></a>[Python](#tab/python)

Vous pouvez analyser la partie **@Mention** du texte du message à l’aide d’une méthode statique fournie avec le Bot Framework. C’est une méthode de la classe `TurnContext` appelée `remove_recipient_mention`.

Le code Python permettant d’analyser la **\@mention** partie du texte du message est la suivante :

```python
modified_text = TurnContext.remove_recipient_mention(turn_context.activity)
```

* * *

Pour permettre le bon fonctionnement de votre code de bot, vous devez suivre quelques bonnes pratiques.

## <a name="command-menu-best-practices"></a>Meilleures pratiques pour le menu commande

Voici les meilleures pratiques du menu de commandes :

* Restez simple : le menu du bot est destiné à présenter les fonctionnalités clés de votre bot.
* Restez bref : les options de menu ne doivent pas être longues et ne doivent pas être des instructions de langage naturel complexes. Elles doivent être de simples commandes.
* Gardez-le invocable : les commandes ou les actions du menu bot doivent toujours être disponibles, quel que soit l’état de la conversation ou la boîte de dialogue dans lequel se trouve le bot.

> [!NOTE]
> Si vous supprimez des commandes de votre manifeste, vous devez redéployer votre application pour implémenter les modifications. En général, toutes les modifications apportées au manifeste nécessitent le redéploiement de votre application.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Conversations de groupe et de canal](~/bots/how-to/conversations/channel-and-group-conversations.md)
