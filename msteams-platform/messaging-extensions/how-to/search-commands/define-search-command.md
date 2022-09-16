---
title: Définir des commandes de recherche d’extension de message
author: surbhigupta
description: Dans ce module, découvrez les emplacements d’appel de commande de recherche et comment créer une commande de recherche pour les extensions de messagerie.
ms.topic: conceptual
ms.author: anclear
ms.localizationpriority: medium
ms.openlocfilehash: f562763cc84979874fac612f125b536fa9e6bc36
ms.sourcegitcommit: 19f3e4e9088d0a07c9b567e76640d498b9d1981f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/16/2022
ms.locfileid: "67786961"
---
# <a name="define-message-extension-search-commands"></a>Définir des commandes de recherche d’extension de message

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Les commandes de recherche d’extension de message permettent aux utilisateurs de rechercher des systèmes externes et d’insérer les résultats de cette recherche dans un message sous la forme d’une carte. Ce document vous guide sur la façon de sélectionner la commande de recherche appeler des emplacements et d’ajouter la commande de recherche au manifeste de votre application.

> [!NOTE]
> La limite de taille de la carte de résultat est de 28 Ko. La carte n’est pas envoyée si sa taille dépasse 28 Ko.

Consultez la vidéo suivante pour découvrir comment définir des commandes de recherche d’extension de message :
<br>

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE4OIvK]
<br>

## <a name="select-search-command-invoke-locations"></a>Sélectionner des emplacements d’appel de commande de recherche

La commande de recherche est appelée à partir de n’importe quel emplacement ou des deux emplacements suivants :

* Zone de rédaction du message : boutons situés en bas de la zone de rédaction du message.
* Zone de commande : en @mentioning dans la zone de commande.

  Lorsqu’une commande de recherche est appelée à partir de la zone de message de composition, l’utilisateur envoie les résultats à la conversation. Lorsqu’il est appelé à partir de la zone de commande, l’utilisateur interagit avec la carte résultante ou la copie pour l’utiliser ailleurs.

L’image suivante affiche les emplacements d’appel de la commande de recherche :

:::image type="content" source="~/assets/images/messaging-extension/search-command-invoke-locations.png" alt-text="Capture d’écran montrant les emplacements d’appel d’une commande de recherche dans un canal Teams.":::

## <a name="add-the-search-command-to-your-app-manifest"></a>Ajouter la commande de recherche au manifeste de votre application

Pour ajouter la commande de recherche au manifeste de votre application, vous devez ajouter un nouvel `composeExtension` objet au niveau supérieur de votre manifeste d’application JSON. Vous pouvez ajouter la commande de recherche à l’aide du portail des développeurs ou manuellement.

### <a name="create-a-search-command-using-developer-portal"></a>Créer une commande de recherche à l’aide du portail des développeurs

La configuration requise pour créer une commande de recherche est que vous devez déjà avoir créé une extension de message. Pour plus d’informations sur la création d’une extension de message, consultez [créer une extension de message](~/messaging-extensions/how-to/create-messaging-extension.md).

**Pour créer une commande d’action**

1. Ouvrez **le portail des développeurs** à partir du client Microsoft Teams et sélectionnez l’onglet **Applications** . Si vous avez déjà créé votre package d’application dans le **portail des développeurs**, sélectionnez-le dans la liste. Si vous n’avez pas créé de package d’application, importez-en un existant.
1. Après avoir importé un package d’application, sélectionnez **Extensions de message sous Fonctionnalités** de **l’application**.
1. Pour créer une extension de message, vous avez besoin d’un bot inscrit par Microsoft. Vous pouvez utiliser un bot existant ou en créer un. Sélectionnez **l’option Créer un bot** , donnez un nom au nouveau bot, puis sélectionnez **Créer**.

   :::image type="content" source="../../../assets/images/tdp/bot-page.png" alt-text="Capture d’écran montrant les options de configuration d’un bot pour une application dans le portail des développeurs Teams.":::

1. Pour utiliser un bot existant, **sélectionnez Sélectionner un bot existant** et choisissez les bots existants dans la liste déroulante, ou **entrez un ID de bot** si vous avez déjà créé un ID de bot.

1. Sélectionnez l’étendue de l’extension de messagerie, puis **sélectionnez Enregistrer**.

1. Sélectionnez **Ajouter une commande** dans la section **Commande** pour inclure les commandes, qui déterminent le comportement de l’extension de message.
L’image suivante affiche l’ajout de commande pour l’extension de message :

   :::image type="content" source="../../../assets/images/tdp/add-a-command.PNG" alt-text="Capture d’écran montrant comment ajouter une commande dans le portail des développeurs Teams pour définir le comportement de l’extension de message.":::

1. Sélectionnez **Rechercher** et entrez **l’ID de commande**, **le titre de la commande** et **la description de la commande**.

1. Entrez tous les paramètres et sélectionnez le type d’entrée dans la liste déroulante.

   :::image type="content" source="../../../assets/images/tdp/add-a-command-parameter.PNG" alt-text="Capture d’écran montrant comment ajouter un paramètre pour définir votre commande dans le portail des développeurs Teams pour une extension de message.":::

1. Sélectionnez **Ajouter un domaine** sous **Liens d’aperçu**.

1. Entrez un domaine valide, puis **sélectionnez Ajouter**.

   :::image type="content" source="../../../assets/images/tdp/add-domain.PNG" alt-text="Capture d’écran montrant comment ajouter un domaine valide à votre extension de messagerie pour le déploiement de liens.":::

1. Sélectionnez **Enregistrer**.

   :::image type="content" source="../../../assets/images/tdp/add-a-command-save.PNG" alt-text="Capture d’écran montrant comment enregistrer tous vos paramètres et paramètres pour votre extension de message.":::

**Pour ajouter des paramètres supplémentaires**

1. Sélectionnez ellipse sous la section de commande, puis **sélectionnez Modifier le paramètre**.

   :::image type="content" source="../../../assets/images/tdp/edit-parameters.PNG" alt-text="Les captures d’écran montrent comment modifier les paramètres de votre extension de message.":::

1. Sélectionnez **Ajouter un paramètre** et entrez tous les paramètres.

   :::image type="content" source="../../../assets/images/tdp/add-parameter.PNG" alt-text="Capture d’écran montrant comment ajouter des paramètres supplémentaires pour votre extension de message."lightbox="../../../assets/images/tdp/add-a-parameters.PNG":::

### <a name="create-a-search-command-manually"></a>Créer une commande de recherche manuellement

Pour ajouter manuellement votre commande de recherche d’extension de message au manifeste de votre application, vous devez ajouter les paramètres suivants à votre `composeExtension.commands` tableau d’objets :

| Nom de la propriété | Objectif | Obligatoire ? | Version minimale du manifeste |
|---|---|---|---|
| `id` | Cette propriété est un ID unique que vous affectez à la commande de recherche. La demande de l’utilisateur inclut cet ID. | Oui | 1.0 |
| `title` | Cette propriété est un nom de commande. Cette valeur apparaît dans l’interface utilisateur. | Oui | 1.0 |
| `description` | Cette propriété est un texte d’aide indiquant ce que fait cette commande. Cette valeur apparaît dans l’interface utilisateur. | Oui | 1.0 |
| `type` | Cette propriété doit être un `query`. | Non | 1.4 |
|`initialRun` | Si cette propriété a la valeur **true**, elle indique que cette commande doit être exécutée dès que l’utilisateur sélectionne cette commande dans l’interface utilisateur. | Non | 1.0 |
| `context` | Cette propriété est un tableau facultatif de valeurs qui définit le contexte dans lequel l’action de recherche est disponible. Les valeurs possibles sont `message`, `compose` ou `commandBox`. La valeur par défaut est `["compose", "commandBox"]`. | Non | 1,5 |

Vous devez ajouter les détails du paramètre de recherche qui définit le texte visible par votre utilisateur dans le client Teams.

| Nom de la propriété | Objectif | Est-ce obligatoire ? | Version minimale du manifeste |
|---|---|---|---|
| `parameters` | Cette propriété définit une liste statique de paramètres pour la commande. | Non | 1.0 |
| `parameter.name` | Cette propriété décrit le nom du paramètre. L’objet `parameter.name` est envoyé à votre service dans la demande de l’utilisateur. | Oui | 1.0 |
| `parameter.description` | Cette propriété décrit les objectifs du paramètre ou l’exemple de la valeur qui doit être fournie. Cette valeur apparaît dans l’interface utilisateur. | Oui | 1.0 |
| `parameter.title` | Cette propriété est un titre ou une étiquette de paramètre convivial court. | Oui | 1.0 |
| `parameter.inputType` | Cette propriété est définie sur le type de l’entrée requise. Les valeurs possibles sont : `text`, `textarea`, `number``date`, `toggle``time`. La valeur par défaut est `text`. | Non | 1.4 |
| `parameters.value` | Valeur initiale du paramètre. Actuellement, la valeur n’est pas prise en charge | Non | 1,5 |

#### <a name="example"></a>Exemple

La section suivante est un exemple de manifeste d’application simple de l’objet `composeExtensions` définissant une commande de recherche :

```json
{
...
  "composeExtensions": [
    {
      "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
      "canUpdateConfiguration": true,
      "commands": [{
          "id": "searchCmd",
          "description": "Search Bing for information on the web",
          "title": "Search",
          "initialRun": true,
          "parameters": [{
            "name": "searchKeyword",
            "description": "Enter your search keywords",
            "title": "Keywords"
          }]
        }
      ]
    }
  ],
...
}

```

Pour obtenir le manifeste complet de l’application, consultez [le schéma de manifeste de l’application](~/resources/schema/manifest-schema.md).

## <a name="code-sample"></a>Exemple de code

| Exemple de nom           | Description | .NET    | Node.js   |
|:---------------------|:--------------|:---------|:--------|
|Recherche d'extension des messages Teams   |  Décrit comment définir les commandes de recherche et répondre aux recherches.        |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="step-by-step-guide"></a>Guide pas à pas

Suivez le [guide pas à pas](../../../sbs-messagingextension-searchcommand.yml) pour créer une extension de message basée sur la recherche.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Répondez aux commandes de recherche](~/messaging-extensions/how-to/search-commands/respond-to-search.md).
