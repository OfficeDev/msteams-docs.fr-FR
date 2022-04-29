---
title: Recevoir tous les messages de canal avec RSC
author: surbhigupta12
description: Recevoir tous les messages de canal avec RSC
ms.topic: conceptual
ms.localizationpriority: high
ms.openlocfilehash: 6b4c2add73c54aadd068c16171a0d340a0c79075
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111205"
---
# <a name="receive-all-channel-messages-with-rsc"></a>Recevoir tous les messages de canal avec RSC

Le modèle d’autorisations de consentement spécifique à la ressource (RSC), initialement développé pour les API Graph Teams, est étendu aux scénarios de bot.

À l’aide de RSC, vous pouvez désormais demander aux propriétaires d’équipe de donner leur consentement pour qu’un bot reçoive des messages utilisateur sur les canaux standard d’une équipe sans être @mentionné. Cette fonctionnalité est activée en spécifiant l’autorisation `ChannelMessage.Read.Group` dans le manifeste d’une application Teams compatible RSC. Après la configuration, les propriétaires d’équipe peuvent accorder leur consentement pendant le processus d’installation de l’application.

Pour plus d’informations sur l’activation de RSC pour votre application, consultez [consentement spécifique à la ressource dans Teams](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#update-your-teams-app-manifest).

## <a name="enable-bots-to-receive-all-channel-messages"></a>Autoriser les bots à recevoir tous les messages de canal

L’autorisation `ChannelMessage.Read.Group` RSC est étendue aux bots. Avec le consentement de l’utilisateur, cette autorisation permet aux applications graphes d’obtenir tous les messages d’une conversation et aux bots de recevoir tous les messages de canal sans être @mentionné.

> [!NOTE]
>
> * Les services qui ont besoin d’accéder à toutes les données de message Teams doivent utiliser les API Graph qui fournissent également l’accès aux données archivées dans les canaux et les conversations.
> * Les bots doivent utiliser l’autorisation `ChannelMessage.Read.Group` RSC de manière appropriée pour créer et améliorer l’expérience attrayante pour les utilisateurs de l’équipe, sinon ils ne recevront pas l’approbation du magasin. La description de l’application doit inclure la façon dont le bot utilise les données qu’il lit.
> * L’autorisation `ChannelMessage.Read.Group` RSC ne peut pas être utilisée par les bots pour extraire de grandes quantités de données client.

## <a name="update-app-manifest"></a>Mettre à jour le manifeste de l’application

Pour que votre bot reçoive tous les messages de canal, RSC doit être configuré dans le manifeste de l’application Teams avec l’autorisation `ChannelMessage.Read.Group` spécifiée dans la propriété `webApplicationInfo`.

![Mettre à jour le manifeste de l’application](~/bots/how-to/conversations/Media/appmanifest.png)


Voici un exemple de l’objet `webApplicationInfo` :

* **id** : ID de votre application Microsoft Azure Active Directory (Azure AD). Cela peut être identique à l’ID de votre bot.
* **ressource** : n’importe quelle chaîne. Ce champ n’a aucune opération dans RSC, mais doit être ajouté et avoir une valeur pour éviter une réponse d’erreur.
* **applicationPermissions** : les autorisations RSC pour votre application avec `ChannelMessage.Read.Group` doivent être spécifiées. Pour plus d’informations, consultez [autorisations spécifiques à la ressource](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#resource-specific-permissions).

Le code suivant fournit un exemple de manifeste d’application :

```json
"webApplicationInfo": {
"id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
"resource": "https://AnyString",
"applicationPermissions": [
"ChannelMessage.Read.Group"
    ]
  }
```

## <a name="sideload-in-a-team"></a>Chargement indépendant dans une équipe

Pour charger une version test dans une équipe, indiquez si tous les messages de canal d’une équipe avec RSC sont reçus sans être @mentionné :

1. Sélectionnez ou créez une équipe.
1. Sélectionnez les points de suspension &#x25CF;&#x25CF;&#x25CF; à partir du volet gauche. Le menu déroulant s’affiche.
1. Sélectionnez **Gérer une équipe** dans le menu déroulant. Les détails s’affichent.

   ![Gestion des applications en équipe](~/bots/how-to/conversations/Media/managingteam.png)

      :::image type="content" source="Media/managingteam.png" alt-text="gestion d’une équipe"border="true":::

1. Sélectionner **les applications**. Plusieurs applications s’affichent.
1. Sélectionnez **Charger une application personnalisée** dans le coin inférieur droit.

      :::image type="content" source="Media/uploadingcustomapp.png" alt-text="chargement d’une application personnalisée":::
  
1. Sélectionnez le package d’application dans la boîte de dialogue **Ouvrir** .
1. Sélectionnez **Ouvrir**.

      :::image type="content" source="Media/selectapppackage.png" alt-text="Sélectionnez le package d’application"lightbox="Media/selectapppackage.png"border="true":::

1. Sélectionnez **Ajouter** dans la fenêtre contextuelle des détails de l’application pour ajouter le bot à l’équipe sélectionnée.

      :::image type="content" source="Media/addingbot.png" alt-text="Ajout d’un bot"lightbox="Media/addingbot.png"border="true":::

1. Sélectionnez un canal et entrez un message dans le canal de votre bot.

    Le bot reçoit le message sans être @mentionné.

      :::image type="content" source="Media/botreceivingmessage.png" alt-text="Bot recevant un message"lightbox="Media/botreceivingmessage.png"border="true":::

## <a name="code-snippets"></a>Extraits de code

Le code suivant fournit un exemple d’autorisations RSC :

# <a name="c"></a>[C#](#tab/dotnet)

```csharp

// Handle when a message is addressed to the bot. 
// When rsc is enabled the method will be called even when bot is addressed without being @mentioned
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text("Using RSC the bot can recieve messages across channels in team without being @mentioned."));
}
```

# <a name="nodejs"></a>[Node.js](#tab/nodejs)

```javascript

// Handle when a message is addressed to the bot. 
// When rsc is enabled the method will be called even when bot is addressed without being @mentioned
this.onMessage(async (context, next) => {
   await context.sendActivity(MessageFactory.text("Using RSC the bot can recieve messages across channles in team without being @mentioned."))
   await next();
});
```

---

## <a name="code-sample"></a>Exemple de code

| Exemple de nom | Description | C# |Node.js|
|-------------|-------------|------|----|
|Messages de canal avec autorisations RSC| Exemple d’application Microsoft Teams montrant comment un bot peut recevoir tous les messages de canal avec RSC sans être @mentionné.| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-receive-channel-messages-withRSC/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-receive-channel-messages-withRSC/nodejs) |

## <a name="see-also"></a>Voir aussi

* [Conversations de robots](/microsoftteams/platform/bots/how-to/conversations/conversation-basics)
* [Consentement spécifique à la ressource](/microsoftteams/resource-specific-consent)
* [Tester le consentement spécifique à la ressource](/microsoftteams/platform/graph-api/rsc/test-resource-specific-consent)
* [Charger une application personnalisée dans Teams](~/concepts/deploy-and-publish/apps-upload.md)
