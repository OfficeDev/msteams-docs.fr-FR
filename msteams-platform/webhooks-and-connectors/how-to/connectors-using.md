---
title: Créer et envoyer des messages
author: laujan
description: Décrit l’utilisation des Connecteurs Office 365 dans Microsoft Teams
ms.topic: how-to
ms.localizationpriority: medium
keywords: 'équipes connecteur O365 '
ms.openlocfilehash: 49f14862870fae216de1a6d810eacd4b23c81540
ms.sourcegitcommit: 85d0584877db21e2d3e49d3ee940d22675617582
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/29/2021
ms.locfileid: "61216194"
---
# <a name="create-and-send-messages"></a>Créer et envoyer des messages

Vous pouvez créer des messages actionnables et les envoyer via le webhook entrant ou Office 365 connector.

## <a name="create-actionable-messages"></a>Créer des messages actionnables

Les messages actionnables incluent six boutons visibles sur la carte. Chaque bouton est défini dans la propriété du message à l’aide d’actions, chacune avec un type d’entrée, un champ de texte, un s sélectionneur de dates ou une liste à `potentialAction` `ActionCard` choix multiples. Chaque `ActionCard` action est associée, par `HttpPOST` exemple.

Les cartes de connecteurs prendre en charge les actions suivantes :

- `ActionCard`: présente un ou plusieurs types d’entrée et actions associées.
- `HttpPOST`: envoie une requête POST à une URL.
- `OpenUri`: ouvre l’URI dans un navigateur ou une application distinct, cible éventuellement différentes URI en fonction des systèmes d’exploitation.

L'action `ActionCard` prend en charge trois types d'entrée :

- `TextInput`: champ de texte à une seule ligne ou à plusieurs lignes avec une limite de longueur facultative.
- `DateInput`: sélecteur de dates avec un sélecteur d’heure facultatif.
- `MultichoiceInput`: Liste énumérée de choix offrant une sélection unique ou plusieurs sélections.

`MultichoiceInput` prend en charge une propriété `style` qui contrôle l’affichage initial complet de la liste. La valeur par défaut `style` dépend de la valeur suivante `isMultiSelect` :

| `isMultiSelect` | `style` par défaut |
| --- | --- |
| `false` ou non spécifié | `compact` |
| `true` | `expanded` |

Pour afficher la liste de plusieursélections dans le style compact, vous devez spécifier les deux `"isMultiSelect": true` et `"style": true` .

Pour plus d’informations sur les actions de carte de connecteur, voir [Actions.](/outlook/actionable-messages/card-reference#actions)

> [!NOTE]
> * Spécifier `compact` pour la propriété `style` dans Microsoft Teams revient à spécifier `normal` pour la propriété `style` dans Microsoft Outlook.
> * Pour l’action HttpPOST, le jeton du porteur est inclus dans les demandes. Ce jeton inclut l’identité Azure AD de l’utilisateur Office 365 sujet de l’action.

## <a name="send-a-message-through-incoming-webhook-or-office-365-connector"></a>Envoyer un message via le webhook entrant ou Office 365 connector

Pour envoyer un message via votre webhook entrant ou votre connecteur Office 365, publiez une charge utile JSON sur l’URL du webhook. Cette charge utile doit prendre la forme d’une [carte Office 365 connecteur.](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)

Vous pouvez également utiliser ce JSON pour créer des cartes contenant des entrées enrichies, telles que l’entrée de texte, la sélection multiple ou la sélection de date et d’heure. Le code qui génère la carte et la publie sur l’URL de webhook peut s’exécuter sur n’importe quel service hébergé. Ces cartes sont définies dans le cadre de messages actionnables et sont également prises en charge dans les [cartes,](~/task-modules-and-cards/what-are-cards.md)utilisées dans Teams bots et extensions de messagerie.

### <a name="example-of-connector-message"></a>Exemple de message de connecteur

Voici un exemple de message de connecteur :

```json
{
    "@type": "MessageCard",
    "@context": "http://schema.org/extensions",
    "themeColor": "0076D7",
    "summary": "Larry Bryant created a new task",
    "sections": [{
        "activityTitle": "Larry Bryant created a new task",
        "activitySubtitle": "On Project Tango",
        "activityImage": "https://teamsnodesample.azurewebsites.net/static/img/image5.png",
        "facts": [{
            "name": "Assigned to",
            "value": "Unassigned"
        }, {
            "name": "Due date",
            "value": "Mon May 01 2017 17:07:18 GMT-0700 (Pacific Daylight Time)"
        }, {
            "name": "Status",
            "value": "Not started"
        }],
        "markdown": true
    }],
    "potentialAction": [{
        "@type": "ActionCard",
        "name": "Add a comment",
        "inputs": [{
            "@type": "TextInput",
            "id": "comment",
            "isMultiline": false,
            "title": "Add a comment here for this task"
        }],
        "actions": [{
            "@type": "HttpPOST",
            "name": "Add comment",
            "target": "https://docs.microsoft.com/outlook/actionable-messages"
        }]
    }, {
        "@type": "ActionCard",
        "name": "Set due date",
        "inputs": [{
            "@type": "DateInput",
            "id": "dueDate",
            "title": "Enter a due date for this task"
        }],
        "actions": [{
            "@type": "HttpPOST",
            "name": "Save",
            "target": "https://docs.microsoft.com/outlook/actionable-messages"
        }]
    }, {
        "@type": "OpenUri",
        "name": "Learn More",
        "targets": [{
            "os": "default",
            "uri": "https://docs.microsoft.com/outlook/actionable-messages"
        }]
    }, {
        "@type": "ActionCard",
        "name": "Change status",
        "inputs": [{
            "@type": "MultichoiceInput",
            "id": "list",
            "title": "Select a status",
            "isMultiSelect": "false",
            "choices": [{
                "display": "In Progress",
                "value": "1"
            }, {
                "display": "Active",
                "value": "2"
            }, {
                "display": "Closed",
                "value": "3"
            }]
        }],
        "actions": [{
            "@type": "HttpPOST",
            "name": "Save",
            "target": "https://docs.microsoft.com/outlook/actionable-messages"
        }]
    }]
}
```

Ce message fournit la carte suivante dans le canal :

![Capture d’écran d’une carte de connecteur](~/assets/images/connectorcard.png)

## <a name="send-messages-using-curl-and-powershell"></a>Envoyer des messages à l’aide de cURL et de PowerShell

# <a name="curl"></a>[cURL](#tab/cURL)

**Pour publier un message dans le webhook avec cURL**

1. Installez cURL à l’aide de https://curl.haxx.se/ : .

1. Depuis la ligne de commande , entrez la commande cURL suivante :

   ```bash
   // on macOS or Linux
   curl -H 'Content-Type: application/json' -d '{"text": "Hello World"}' <YOUR WEBHOOK URL>
   ```

   ```bash
   // on Windows
   curl.exe -H "Content-Type:application/json" -d "{'text':'Hello World'}" <YOUR WEBHOOK URL>
   ```

    > [!NOTE]
    > Si la post réussit, vous devez voir une sortie **simple de 1** `curl` par .

1. Vérifiez la Microsoft Teams client pour la nouvelle carte publiée.

# <a name="powershell"></a>[PowerShell](#tab/PowerShell)

 Conditions préalables : installation de PowerShell et familiarisation avec son utilisation de base.

**Pour publier un message sur le webhook avec PowerShell**

1. À partir de l'invite PowerShell, entrez les commandes suivantes :

   ```powershell
   Invoke-RestMethod -Method post -ContentType 'Application/Json' -Body '{"text":"Hello World!"}' -Uri <YOUR WEBHOOK URL>
   ```

    > [!NOTE]
    > Si la post réussit, vous devez voir une sortie **simple de 1** `Invoke-RestMethod` par .

1. Vérifiez le canal Microsoft Teams associé à l’URL de webhook. Vous pouvez voir la nouvelle carte publiée sur le canal. Avant d’utiliser le connecteur pour tester ou publier votre application, vous devez :

    - [Incluez deux icônes](../../concepts/build-and-test/apps-package.md#app-icons).
    - Modifiez la partie du manifeste sur les noms de fichier des icônes au lieu `icons` des URL.

---

## <a name="send-adaptive-cards-using-an-incoming-webhook"></a>Envoyer des cartes adaptatives à l’aide d’un webhook entrant

> [!NOTE]
> * Tous les éléments de schéma de carte adaptative native, à l’exception `Action.Submit` de , sont entièrement pris en charge.
> * Les actions prises en [**charge sont Action.OpenURL,**](https://adaptivecards.io/explorer/Action.OpenUrl.html) [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html)et [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html).

**Pour envoyer des cartes adaptatives via un webhook entrant**

1. [Configurer un webhook personnalisé dans](~/webhooks-and-connectors/how-to/add-incoming-webhook.md) Teams.
1. Créez un fichier JSON de carte adaptative à l’aide du code suivant :

    ```json
    {
       "type":"message",
       "attachments":[
          {
             "contentType":"application/vnd.microsoft.card.adaptive",
             "contentUrl":null,
             "content":{
                "$schema":"http://adaptivecards.io/schemas/adaptive-card.json",
                "type":"AdaptiveCard",
                "version":"1.2",
                "body":[
                    {
                    "type": "TextBlock",
                    "text": "For Samples and Templates, see [https://adaptivecards.io/samples](https://adaptivecards.io/samples)"
                    }
                ]
             }
          }
       ]
    }
    ```

    Les propriétés du fichier JSON de carte adaptative sont les suivantes :

    * Le `"type"` champ doit être`"message"`.
    * Le`"attachments"` tableau contient un ensemble d'objets carte.
    * Le `"contentType"` champ doit être de type Carte adaptative.
    * L’`"content"` objet est la carte formatée en JSON.

1. Testez votre carte adaptative avec Postman :

    * Testez la carte adaptative à [l’aide de Postman](https://www.postman.com) pour envoyer une requête POST à l’URL, créée pour configurer le webhook entrant.
    * Collez le fichier JSON dans le corps de la demande et affichez le message de carte adaptative dans Teams.

> [!TIP]
> Utilisez des [exemples de code et des modèles](https://adaptivecards.io/samples) de carte adaptative pour tester le corps de la requête POST.

## <a name="rate-limiting-for-connectors"></a>Limitation du taux pour les connecteurs

Les limites de fréquence d’application contrôlent le trafic qu’un connecteur ou un webhook entrant est autorisé à générer sur un canal. Teams les demandes à l’aide d’une fenêtre à taux fixe et d’un compteur incrémentielle mesuré en secondes. Si plus de quatre demandes sont faites en une seconde, la connexion client est limitée jusqu’à ce que la fenêtre s’actualise pendant la durée du taux fixe.

### <a name="transactions-per-second-thresholds"></a>Seuils de transaction par seconde

Le tableau suivant fournit les détails des transactions basées sur le temps :

| Durée en secondes  | Nombre maximal de demandes autorisées  |
|---|---|
| 1   | 4  |  
| 30   | 60  |  
| 3600   | 100  |
| 7200 | 150  |
| 86400  | 1800  |

Une [logique de nouvelle tentative avec](/azure/architecture/patterns/retry) un délai d’attente exponentiel peut atténuer la limitation des taux pour les cas où les demandes dépassent les limites en l’espace d’une seconde. Suivez [les meilleures pratiques pour](../../bots/how-to/rate-limit.md) éviter d’atteindre les limites de taux.

> [!NOTE]
> Une [logique de nouvelle tentative avec](/azure/architecture/patterns/retry) un délai d’attente exponentiel peut atténuer la limitation des taux pour les cas où les demandes dépassent les limites en l’espace d’une seconde. Référez-vous aux [réponses du protocole HTTP 429](../../bots/how-to/rate-limit.md#handle-http-429-responses) pour éviter de vous heurter aux limites de taux.

```csharp
// Please note that response body needs to be extracted and read 
// as Connectors do not throw 429s
try
{
    // Perform Connector POST operation     
    var httpResponseMessage = await _client.PostAsync(IncomingWebhookUrl, new StringContent(content));
    // Read response content
    var responseContent = await httpResponseMessage.Content.ReadAsStringAsync();
    if (responseContent.Contains("Microsoft Teams endpoint returned HTTP error 429")) 
    {
        // initiate retry logic
    }
}
```

Ces limites sont en place pour réduire le courrier indésirable d’un canal par un connecteur et garantissent une expérience optimale aux utilisateurs.

## <a name="see-also"></a>Voir aussi

* [Office 365 Connectors for Microsoft Teams](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [Créer un webhook entrant](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [Créer un webhook sortant](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)
* [Limite de taux pour Teams messages de bots](~/bots/how-to/rate-limit.md)
* [Créer des onglets avec les Cartes adaptatives](~/tabs/how-to/build-adaptive-card-tabs.md)
* [Mettre en forme des cartes dans Microsoft Teams](~/task-modules-and-cards/cards/cards-format.md)
