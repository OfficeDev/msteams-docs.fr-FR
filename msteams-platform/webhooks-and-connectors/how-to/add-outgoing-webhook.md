---
title: Créer un webhook sortant
author: laujan
description: explique comment créer un webhook sortant
ms.topic: conceptual
ms.localizationpriority: high
ms.author: lajanuar
keywords: 'Onglets teams : message actionnable de webhook sortant vérifiant le webhook'
ms.openlocfilehash: 8450f9411e2fa5b1e0af624f48882016951f24a7
ms.sourcegitcommit: 52af681132e496a57b18f468c5b73265a49a5f44
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2022
ms.locfileid: "64590688"
---
# <a name="create-outgoing-webhook"></a>Créer des webhooks sortants

Le webhook sortant agit comme un bot et recherche des messages dans les canaux à l’aide de **@mention**. Il envoie des notifications aux services web externes et répond avec des messages enrichis, qui incluent des cartes et des images. Cela permet d’ignorer le processus de création de bots via le [Microsoft Bot Framework](https://dev.botframework.com/).

<!--- TBD: Edit this article.
* Admonitions/alerts may be overused in this article. Check once.
* An important alert at the end of this table does not make sense. Also, it has a code snippet inside it.
* Some screenshots like teamschannel.png may be redundant. Check once.
* Some headings use title case. We use sentence case for titles.
* Check for markdownlint errors. 
* Try using &nbsp; to add spaces in codeblocks for indentation and remove the hard tabs.
* Table with just a row is not really needed. Provide the content without tabulating it.
--->

## <a name="key-features-of-outgoing-webhook"></a>Principales fonctionnalités du webhook sortant

Le tableau suivant fournit les fonctionnalités et la description des webhooks sortants :

| Fonctionnalités | Description |
| ------- | ----------- |
| Configuration délimitée| Les webhooks sont limités au niveau de l’équipe. Processus de configuration obligatoire pour chaque ajout d’un webhook sortant. |
| Messagerie réactive| Les utilisateurs doivent utiliser une @mention pour que le webhook reçoive des messages. Actuellement, les utilisateurs peuvent uniquement envoyer un webhook sortant dans les canaux publics et non dans l’étendue personnelle ou privée. |
|Échange de messages HTTP standard|Les réponses s’affichent dans la même chaîne que le message de demande initial et peuvent inclure n’importe quel contenu de message Bot Framework. Par exemple, un texte enrichi, des images, des cartes et des emojis. Bien que les webhooks sortants puissent utiliser des cartes, ils ne peuvent utiliser aucune action de carte à l’exception de `openURL`.|
| Prise en charge des méthodes de l’API Teams|Les webhooks sortants envoient une demande HTTP POST à un service web et obtiennent une réponse. Ils ne peuvent pas accéder à d’autres API, telles que la récupération de la liste de présence ou de la liste des canaux d’une équipe.|

## <a name="create-outgoing-webhooks"></a>Créer des webhooks sortants

Créez des webhooks sortants et ajoutez des bots personnalisés à Teams.

Pour créer un webhook sortant, suivez ces étapes :

1. Sélectionnez **Teams** dans le volet gauche. La page **Teams** s’affiche :

    ![Canal Teams](~/assets/images/teamschannel.png)

1. Dans la page **Teams**, sélectionnez l’équipe requise pour créer un webhook sortant et sélectionnez le &#8226;&#8226;&#8226;. Dans le menu déroulant, sélectionnez **Gérer l’équipe** :

    ![Créer des webhooks sortants](~/assets/images/outgoingwebhook1.png)

1. Sélectionnez l’onglet **Applications** sur la page de canal :

    ![Créer un webhook sortant](~/assets/images/outgoingwebhook2.png)

1. Sélectionnez **Créer un webhook sortant**:

    ![Créer des webhooks sortants](~/assets/images/outgoingwebhook3.png)

1. Tapez les détails suivants dans la page **Créer un webhook sortant** :

    * **Nom**: titre du webhook et de l’onglet @mention.
    * **URL de rappel** : point de terminaison HTTPS qui accepte les charges utiles JSON et reçoit les demandes POST de Teams.
    * **Description** : chaîne détaillée qui apparaît dans la carte de visite et le tableau de bord de l’application au niveau de l’équipe.
    * **Image de profil** : icône d’application pour votre webhook (facultative).

1. Sélectionnez **Créer**. Le webhook sortant est ajouté au canal de l’équipe actuelle :

    ![créer un webhook sortant](~/assets/images/outgoingwebhook.png)

Une boîte de dialogue [Code d’authentification de message basé sur le hachage (HMAC)](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301) s’affiche. Il s’agit d’un jeton de sécurité utilisé pour authentifier les appels entre Teams et le service extérieur désigné. Le jeton de sécurité HMAC n’expire pas et il est unique pour chaque configuration.

>[!NOTE]
> Le webhook sortant est disponible pour les utilisateurs de l’équipe, seulement si l’URL est valide et que les jetons d’authentification du serveur et du client sont égaux. Par exemple, une poignée de main HMAC.

Le scénario suivant fournit les détails pour ajouter un webhook sortant :

* Scénario : envoyez des notifications de changement d’état sur un serveur de base de données de canal Teams à votre application.
* Exemple : vous avez une application métier qui suit toutes les opérations CRUD (créer, lire, mettre à jour et supprimer). Ces opérations sont réalisées sur les enregistrements de l’employé par les utilisateurs RH du canal Teams au sein d’une location Office 365.

# <a name="url-json-payload"></a>[Charge utile JSON d’URL](#tab/urljsonpayload)

**Créer une URL sur le serveur de votre application pour accepter et traiter une demande POST avec une charge utile JSON**

Votre service reçoit des messages dans un schéma de messagerie de service de bot Azure standard. Le connecteur Bot Framework est un service RESTful qui permet de traiter l’échange de messages au format JSON via des protocoles HTTPS, comme documenté dans l’[API Azure Bot Service](/bot-framework/rest-api/bot-framework-rest-connector-api-reference). Vous pouvez également suivre le kit de développement logiciel (SDK) Microsoft Bot Framework pour traiter et analyser les messages. Pour plus d’informations, consultez [vue d’ensemble d’Azure Bot Service](/azure/bot-service/bot-service-overview-introduction).

Les webhooks sortants sont limités au niveau `team` et sont visibles par tous les membres de l’équipe. Les utilisateurs doivent **\@mentionner** le nom du webhook sortant pour l’appeler dans le canal.

# <a name="verify-hmac-token"></a>[Vérifier le jeton HMAC](#tab/verifyhmactoken)

**Créer une méthode pour vérifier le jeton HMAC du webhook sortant**

Utilisation d’un exemple de message entrant et d’ID : « contoso » de SigningKeyDictionary de {"contoso", "vqF0En+Z0ucuRTM/01o2GuhMH3hKKk/N2bOmlM31zaA=" }.

Utilisez la valeur « HMAC 03TCao0i55H1eVKUusZOTZRjtvYTs+mO41mPL+R1e1U= » dans l’autorisation de l’en-tête de demande.

Pour vous assurer que votre service reçoit uniquement les appels de clients Teams réels, Teams fournit un code HMAC dans l’en-tête d’autorisation HTTP `hmac`. Incluez toujours le code dans votre protocole d’authentification.

Votre code doit toujours valider la signature HMAC incluse dans la demande comme il suit :

* Générer le jeton HMAC à partir du corps de la demande du message. Il existe des bibliothèques standard pour le faire sur la plupart des plateformes, telles que [Crypto](https://nodejs.org/api/crypto.html#crypto_crypto) pour Node.js et [Exemple de webhook pour Teams](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) pour C\#. Microsoft Teams utilise le chiffrement HMAC SHA256 standard. Vous devez convertir le corps en un tableau d’octets en UTF8.
* Calculez le hachage à partir du tableau d’octets du jeton de sécurité fourni par Teams lorsque vous avez enregistré le webhook sortant dans le client Teams. Voir [Créer un Webhook sortant](#create-outgoing-webhook).
* Convertissez le hachage en chaîne à l’aide du codage UTF-8.
* Comparez la valeur de chaîne du hachage généré à la valeur fournie dans la requête HTTP.

# <a name="method-to-respond"></a>[Méthode de réponse](#tab/methodtorespond)

**Créer une méthode pour envoyer une réponse de réussite ou d’échec**

Les réponses de vos webhooks sortants s’affichent dans la même chaîne de réponse que le message d’origine. Lorsque l’utilisateur effectue une requête, Microsoft Teams envoie une demande HTTP synchrone à votre service et votre code obtient cinq secondes pour répondre au message avant que la connexion n’arrive à terme et ne se termine.

### <a name="example-response"></a>Exemple de réponse

```json
{
    "type": "message",
    "text": "This is a reply!"
}
```

---

> [!NOTE]
>
> * Vous pouvez envoyer une carte adaptative, une carte de bannière et des SMS en tant que pièce jointe avec un webhook sortant.
> * Les cartes prennent en charge la mise en forme. Pour plus d’informations, consultez [Mettre en forme des cartes avec Markdown](~/task-modules-and-cards/cards/cards-format.md?tabs=adaptive-md%2Cconnector-html#format-cards-with-markdown).
> * La carte adaptative dans les Webhooks sortants ne supporte que les actions de carte `openURL`.

Les codes suivants sont des exemples de réponse de carte adaptative :

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
string content = await this.Request.Content.ReadAsStringAsync();
Activity incomingActivity = JsonConvert.DeserializeObject<Activity>(content);

var Card = new AdaptiveCard(new AdaptiveSchemaVersion("1.4"))
{
    Body = new List<AdaptiveElement>()
    {
        new AdaptiveTextBlock(){Text= $"Request sent by: {incomingActivity.From.Name}"},
        new AdaptiveImage(){Url=new Uri("https://c.s-microsoft.com/en-us/CMSImages/DesktopContent-04_UPDATED.png?version=43c80870-99dd-7fb1-48c0-59aced085ab6")},
        new AdaptiveTextBlock(){Text="Sample image for Adaptive Card.."}
    }
};

var attachment = new Attachment()
{
    ContentType = AdaptiveCard.ContentType,
    Content = Card
};

var sampleResponseActivity = new Activity
{
    Attachments = new [] { attachment }
};

return sampleResponseActivity;
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
var receivedMsg = JSON.parse(payload);
var responseMsg = JSON.stringify({
    "type": "message",
    "attachments": [
        {
            "contentType": "application/vnd.microsoft.card.adaptive",
            "contentUrl": null,
            "content": {
                "type": "AdaptiveCard",
                "version": "1.4",
                "body": [
                    {
                        "type": "TextBlock",
                        "text": "Request sent by: " + receivedMsg.from.name
                    },
                    {
                        "type": "Image",
                        "url": "https://c.s-microsoft.com/en-us/CMSImages/DesktopContent-04_UPDATED.png?version=43c80870-99dd-7fb1-48c0-59aced085ab6"
                    },
                    {
                        "type": "TextBlock",
                        "text": "Sample image for Adaptive Card."
                    }
                ]
            },
            "name": null,
            "thumbnailUrl": null
        }
    ]
});
```

# <a name="json"></a>[JSON](#tab/json)

```json
{
 "type": "message",
 "attachments": [
  {
   "contentType": "application/vnd.microsoft.card.adaptive",
   "content": {
    "type": "AdaptiveCard",
    "version": "1.4",
    "body": [
     {
      "type": "TextBlock",
      "text": "Request sent by: Megan"
     },
     {
      "type": "Image",
      "url": "https://c.s-microsoft.com/en-us/CMSImages/DesktopContent-04_UPDATED.png?version=43c80870-99dd-7fb1-48c0-59aced085ab6"
     },
     {
      "type": "TextBlock",
      "text": "Sample image for Adaptive Card.."
     }
    ]
   }
  }
 ]
}
```

---

## <a name="code-sample"></a>Exemple de code

|**Exemple de nom** | **Description** | **.NET** | **Node.js** |
|----------------|------------------|--------|----------------|
| Webhooks sortants | Exemples pour créer des bots personnalisés à utiliser dans Microsoft Teams.| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/nodejs)|

## <a name="step-by-step-guide"></a>Guide pas à pas

Suivez le [guide pas à pas](../../sbs-outgoing-webhooks.yml) pour créer des webhooks sortants dans Teams.

## <a name="see-also"></a>Voir aussi

* [Créer un webhook entrant](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [Créer un connecteur Office 365](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [Créer et envoyer des messages](~/webhooks-and-connectors/how-to/connectors-using.md)
