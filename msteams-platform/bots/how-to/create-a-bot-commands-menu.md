---
title: Créer un menu de commandes pour votre bot
author: surbhigupta
description: Découvrez comment créer un menu de commandes pour votre bot Microsoft Teams avec des exemples de code.
ms.topic: how-to
ms.localizationpriority: medium
ms.author: anclear
keywords: menu commande composez la conversation de message @mention
ms.openlocfilehash: 6f4b9cdac76fc9beb42a39dde3b320036ea580b5
ms.sourcegitcommit: e40383d9081bf117030f7e6270140e6b94214e8b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2022
ms.locfileid: "65102553"
---
# <a name="bot-command-menus"></a>Menus de commande bot

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Pour définir un ensemble de commandes principales auxquelles votre bot peut répondre, vous pouvez ajouter un menu de commandes avec une liste déroulante de commandes pour votre bot. La liste des commandes est présentée aux utilisateurs dans la zone de composition du message lorsqu’ils sont en conversation avec votre bot. Sélectionnez une commande dans la liste pour insérer la chaîne de commande dans la zone de message de composition, puis sélectionnez **Envoyer**.

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

![Menu commande bot](./conversations/media/bot-menu-sample.png)

# <a name="mobile"></a>[Mobile](#tab/mobile)

![Menu de commande du bot mobile](./conversations/media/mobile-bot-menu-sample.png)

* * *

## <a name="create-a-command-menu-for-your-bot"></a>Créer un menu de commandes pour votre bot

Les menus de commande sont définis dans le manifeste de votre application. Vous pouvez utiliser **App Studio** pour les créer ou les ajouter manuellement dans le manifeste de l’application.

### <a name="create-a-command-menu-for-your-bot-using-app-studio"></a>Créer un menu de commandes pour votre bot à l’aide d’App Studio

Un prérequis pour créer un menu de commandes pour votre bot est que vous devez modifier un manifeste d’application existant. Les étapes d’ajout d’un menu de commandes sont les mêmes, que vous créiez un nouveau manifeste ou que vous en modifiiez un existant.

**Pour créer un menu de commandes pour votre bot à l’aide d’App Studio**

1. Ouvrez Teams et sélectionnez **Applications** dans le volet gauche. Dans la page **Applications** , recherchez **App Studio**, puis sélectionnez **Ouvrir**.
   > [!NOTE]
   > Si vous n’avez pas **App Studio**, vous pouvez le télécharger. Pour plus [d’informations, consultez l’installation d’App Studio](~/concepts/build-and-test/app-studio-overview.md#installing-app-studio).

    :::image type="content" source="/media/AppStudio.png" alt-text="Installation d’App Studio"lightbox="media/AppStudio.png"border="true":::

2. Dans **App Studio**, sélectionnez l’onglet **Éditeur de manifeste** . Si vous n’avez pas de package d’application existant, vous pouvez créer ou importer une application existante. Pour plus d’informations, consultez [mettre à jour un package d’application](~/get-started/deploy-csharp-app-studio.md).

3. Dans le volet gauche de **l’éditeur de manifeste** et dans la section **Fonctionnalités** , sélectionnez **Bots**.

4. Dans le volet droit de **l’éditeur de manifeste** et dans la section **Commandes** , sélectionnez **Ajouter**. **L’écran Nouvelle commande** s’affiche.

    :::image type="content" source="/media/AppStudio-CommandMenu-Add.png" alt-text="Sélectionner le package d’application"lightbox="/media/AppStudio-CommandMenu-Add.png"border="true":::

5. Entrez le **texte de commande** qui doit apparaître comme menu de commande pour votre bot.

6. Entrez le **texte d’aide** qui doit apparaître sous le texte de la commande dans le menu. **Le texte d’aide** doit être une brève explication de l’objectif de la commande.

7. Activez les cases à cocher **Étendue** pour sélectionner l’endroit où ce menu de commande doit apparaître, puis **sélectionnez Enregistrer**.

:::image type="content" source="/media/AppStudio-NewCommandMenu.png" alt-text="Bouton de menu Nouvelles commandes d’App Studio"lightbox="/media/AppStudio-NewCommandMenu.png"border="true":::

### <a name="create-a-command-menu-for-your-bot-by-editing-manifestjson"></a>Créer un menu de commandes pour votre bot en modifiant Manifest.json

Une autre façon de créer un menu de commandes consiste à le créer directement dans le fichier manifeste lors du développement du code source de votre bot. Pour utiliser cette méthode, suivez les points suivants :

* Chaque menu prend en charge jusqu’à dix commandes.
* Créez un menu de commandes unique qui fonctionne dans toutes les étendues.
* Créez un menu de commandes différent pour chaque étendue.

#### <a name="manifest-example-for-single-menu-for-both-scopes"></a>Exemple de manifeste pour un menu unique pour les deux étendues

L’exemple de code du manifeste pour le menu unique pour les deux étendues est le suivant :

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

L’exemple de code du manifeste pour le menu de chaque étendue est le suivant :

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

Vous devez gérer les commandes de menu dans le code de votre bot lorsque vous gérez les messages des utilisateurs. Vous pouvez gérer les commandes de menu dans le code de votre bot en analysant la **\@partie Mention** du texte du message.

## <a name="handle-menu-commands-in-your-bot-code"></a>Gérer les commandes de menu dans le code de votre bot

Les bots d’un groupe ou d’un canal répondent uniquement lorsqu’ils sont mentionnés `@botname` dans un message. Chaque message reçu par un bot dans une étendue de groupe ou de canal contient son nom dans le texte du message. Avant de gérer la commande retournée, votre analyse de message doit gérer le message reçu par un bot portant son nom.

> [!NOTE]
> Pour gérer les commandes dans le code, elles sont envoyées à votre bot en tant que message normal. Vous devez les gérer comme vous le feriez pour tout autre message de vos utilisateurs. Les commandes du code insèrent du texte préconfiguré dans la zone de texte. L’utilisateur doit ensuite envoyer ce texte comme il le fait pour tout autre message.

# <a name="c"></a>[C#](#tab/dotnet)

Vous pouvez analyser la **\@partie Mention** du texte du message à l’aide d’une méthode statique fournie avec le Microsoft Bot Framework. Il s’agit d’une méthode de la `Activity` classe nommée `RemoveRecipientMention`.

Le code C# pour analyser la **\@partie Mention** du texte du message est le suivant :

```csharp
var modifiedText = turnContext.Activity.RemoveRecipientMention();
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

Vous pouvez analyser la **\@partie Mention** du texte du message à l’aide d’une méthode statique fournie avec Bot Framework. Il s’agit d’une méthode de la `TurnContext` classe nommée `removeMentionText`.

Le code JavaScript pour analyser la **\@partie Mention** du texte du message est le suivant :

```javascript
const modifiedText = TurnContext.removeMentionText(turnContext.activity, turnContext.activity.recipient.id);
```

# <a name="python"></a>[Python](#tab/python)

Vous pouvez analyser la **partie @Mention** du texte du message à l’aide d’une méthode statique fournie avec Bot Framework. Il s’agit d’une méthode de la `TurnContext` classe nommée `remove_recipient_mention`.

Le code Python permettant d’analyser la **\@partie Mention** du texte du message est le suivant :

```python
modified_text = TurnContext.remove_recipient_mention(turn_context.activity)
```

* * *

Pour permettre le bon fonctionnement de votre code de bot, vous devez suivre peu de bonnes pratiques.

## <a name="command-menu-best-practices"></a>Meilleures pratiques pour le menu Commandes

Voici les meilleures pratiques du menu de commandes :

* Restez simple : le menu du bot est destiné à présenter les fonctionnalités clés de votre bot.
* Restez bref : les options de menu ne doivent pas être longues et ne doivent pas être des instructions de langage naturel complexes. Il doit s’agir de commandes simples.
* Conservez l’appel : les commandes ou les actions du menu bot doivent toujours être disponibles, quel que soit l’état de la conversation ou la boîte de dialogue dans lequel se trouve le bot.

> [!NOTE]
> Si vous supprimez des commandes de votre manifeste, vous devez redéployer votre application pour implémenter les modifications. En général, toutes les modifications apportées au manifeste vous obligent à redéployer votre application.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Conversations de groupe et de canal](~/bots/how-to/conversations/channel-and-group-conversations.md)
