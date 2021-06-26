---
title: Créer un webhook sortant
author: laujan
description: explique comment créer un webhook sortant
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
keywords: 'onglets teams : message actionnable de webhook sortant vérifiant le webhook'
ms.openlocfilehash: c02ff5388e47ba40056afcc1fcf5e8d7ad4437e8
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140326"
---
# <a name="create-outgoing-webhook"></a>Créer un webhook sortant

Le webhook sortant agit comme un bot et recherche des messages dans les canaux à **l’aide de @mention**. Il envoie des notifications aux services web externes et répond par des messages enrichis, qui incluent des cartes et des images. Cela permet d’ignorer le processus de création de bots via [le Microsoft Bot Framework](https://dev.botframework.com/).

## <a name="key-features-of-outgoing-webhook"></a>Fonctionnalités clés du webhook sortant

Le tableau suivant fournit les fonctionnalités et la description des webhooks sortants :

| Fonctionnalités | Description |
| ------- | ----------- |
| Configuration limitée| Les webhooks sont limitées au niveau de l’équipe. Le processus de mise en place obligatoire pour chaque application ajoute un webhook sortant. |
| Messagerie réactive| Les utilisateurs doivent utiliser @mention pour que le webhook reçoit des messages. Actuellement, les utilisateurs peuvent uniquement envoyer un webhook sortant dans les canaux publics et non dans l’étendue personnelle ou privée. |
|Échange de messages HTTP standard|Les réponses apparaissent dans la même chaîne que le message de demande d’origine et peuvent inclure n’importe quel contenu de message Bot Framework, par exemple du texte enrichi, des images, des cartes et des emojis. Bien que les webhooks sortants peuvent utiliser des cartes, ils ne peuvent pas utiliser d’actions de carte à l’exception de `openURL` .|
| Teams Prise en charge des méthodes d’API|Les webhooks sortants envoient une demande HTTP POST à un service web et renvoient une réponse. Ils ne peuvent pas accéder à d’autres API, telles que la récupération de la liste de la liste ou de la liste des canaux d’une équipe.|

## <a name="create-outgoing-webhooks"></a>Créer des webhooks sortants

Créez des webhooks sortants et ajoutez des bots personnalisés à Teams.

**Pour créer un webhook sortant**

1. Sélectionnez **Teams** dans le volet gauche. La **page Teams’affiche** :

    ![Canal Teams](~/assets/images/teamschannel.png)

1. Dans la page **Teams,** sélectionnez l’équipe requise pour créer un webhook sortant et sélectionnez le &#8226;&#8226;&#8226;. Dans le menu déroulant, sélectionnez **Gérer l’équipe**:

    ![Créer un webhook sortant](~/assets/images/outgoingwebhook1.png)

1. Sélectionnez **l’onglet** Applications sur la page de canal :

    ![Créer un webhook sortant](~/assets/images/outgoingwebhook2.png)

1. Sélectionnez **Créer un webhook sortant**:

    ![Créer des webhooks sortants](~/assets/images/outgoingwebhook3.png)

1. Tapez les détails suivants dans la page **Créer un webhook sortant** :

    * **Nom**: titre du webhook et onglet @mention webhook.
    * **URL de rappel**: point de terminaison HTTPS qui accepte les charges utiles JSON et reçoit les demandes POST de Teams.
    * **Description**: chaîne détaillée qui apparaît dans la carte de visite et le tableau de bord de l’application au niveau de l’équipe.
    * **Image de** profil : icône d’application pour votre webhook, qui est facultative.

1. Sélectionnez **Créer**. Le webhook sortant est ajouté au canal de l’équipe actuelle :

    ![créer un webhook sortant](~/assets/images/outgoingwebhook.png)

Une boîte de dialogue [HMAC (Message Authentication Code)](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301) basée sur le hachage s’affiche. Il s’agit d’un jeton de sécurité utilisé pour authentifier les appels entre Teams et le service extérieur désigné.

>[!NOTE]
> Le webhook sortant est disponible pour les utilisateurs de l’équipe, uniquement si l’URL est valide et que les jetons d’authentification du serveur et du client sont égaux. Par exemple, une poignée de main HMAC.

Le scénario suivant fournit les détails pour ajouter un webhook sortant :

* Scénario : envoyer des notifications d’état de modification sur Teams serveur de base de données de canal vers votre application.
* Exemple : vous avez une application métier qui suit toutes les opérations CRUD, telles que créer, lire, mettre à jour et supprimer. Ces opérations sont réalisées sur les enregistrements des employés par Teams utilisateurs RH de canal au sein d’Office 365 location.

# <a name="url-json-payload"></a>[Charge utile JSON d’URL](#tab/urljsonpayload)
**Créer une URL sur le serveur de votre application pour accepter et traiter une demande POST avec une charge utile JSON**

Votre service reçoit des messages dans un schéma de messagerie de service de bot Azure standard. Le connecteur Bot Framework est un service RESTful qui permet de traiter l’échange de messages au format JSON via des protocoles HTTPS, comme documenté dans [l’API Azure Bot Service.](/bot-framework/rest-api/bot-framework-rest-connector-api-reference) Vous pouvez également suivre le SDK Microsoft Bot Framework pour traiter et parer les messages. Pour plus d’informations, voir [vue d’ensemble d’Azure Bot Service.](/azure/bot-service/bot-service-overview-introduction)

Les webhooks sortants sont limitées au niveau et `team` sont visibles par tous les membres de l’équipe. Les utilisateurs **\@ doivent mentionner** le nom du webhook sortant pour l’appeler dans le canal.

# <a name="verify-hmac-token"></a>[Vérifier le jeton HMAC](#tab/verifyhmactoken)
**Créer une méthode pour vérifier le jeton HMAC du webhook sortant**

Utilisation d’un exemple de message entrant et d’ID : « contoso » de SigningKeyDictionary de {"contoso », « vqF0En+Z0ucuRTM/01o2GuhMH3hKKk/N2bOmlM31zaA= » }.

Utilisez la valeur « HMAC 03TCao0i55H1eVKUusZOTZRjtvYTs+mO41mPL+R1e1U= » dans l’autorisation de l’en-tête de demande.

Pour vous assurer que votre service ne reçoit des appels que de clients Teams réels, Teams fournit un code HMAC dans l’en-tête d’autorisation `hmac` HTTP. Incluez toujours le code dans votre protocole d’authentification.

Votre code doit toujours valider la signature HMAC incluse dans la demande comme suit :

* Générer le jeton HMAC à partir du corps de la demande du message. Il existe des bibliothèques standard pour le faire sur la plupart des plateformes, telles que [Crypto](https://nodejs.org/api/crypto.html#crypto_crypto) for Node.js et [Teams webhook pour](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) C \# ). Microsoft Teams utilise le chiffrement HMAC SHA256 standard. Vous devez convertir le corps en tableau d’entiers en UTF8.
* Calculez le hachage à partir du tableau d’Teams du jeton de sécurité lorsque vous avez inscrit le webhook sortant dans le client Teams. Voir [créer un webhook sortant.](#create-outgoing-webhook)
* Convertissez le hachage en chaîne à l’aide du codage UTF-8.
* Comparez la valeur de chaîne du hachage généré à la valeur fournie dans la requête HTTP.

# <a name="method-to-respond"></a>[Méthode de réponse](#tab/methodtorespond)
**Créer une méthode pour envoyer une réponse de réussite ou d’échec**

Les réponses de vos webhooks sortants apparaissent dans la même chaîne de réponse que le message d’origine. Lorsque l’utilisateur effectue une requête, Microsoft Teams envoie une demande HTTP synchrone à votre service et votre code obtient cinq secondes pour répondre au message avant que la connexion n’arrive à terme et ne se termine.

### <a name="example-response"></a>Exemple de réponse

```json
{
    "type": "message",
    "text": "This is a reply!"
}
```
---

> [!NOTE]
> * Vous pouvez envoyer des messages de carte adaptative, de carte Hero et de texte en pièce jointe avec le webhook sortant.
> * Les cartes sont en charge de la mise en forme. Pour plus d’informations, voir [les cartes de mise en forme avec markdown](~/task-modules-and-cards/cards/cards-format.md?tabs=adaptive-md%2Cconnector-html#format-cards-with-markdown).

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

* * *

## <a name="code-sample"></a>Exemple de code

|**Exemple de nom** | **Description** | **.NET** | **Node.js** |
|----------------|------------------|--------|----------------|
| Webhooks sortants | Exemples de création de bots personnalisés à utiliser dans Microsoft Teams.| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/nodejs)|

## <a name="see-also"></a>Voir aussi
* [Créer un webhook entrant](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [Créer un connecteur Office 365](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [Créer et envoyer des messages](~/webhooks-and-connectors/how-to/connectors-using.md)
