---
title: Envoi de messages à des connecteurs et Webhooks
description: Décrit l’utilisation des Connecteurs Office 365 dans Microsoft Teams
localization_priority: Priority
keywords: 'équipes connecteur O365 '
ms.openlocfilehash: df91dfc68dbafb5e32d8c0e5732eb820c21a51b0
ms.sourcegitcommit: a08f1c7eb9fca11f44842773ab669c69d4af40db
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/10/2020
ms.locfileid: "43225776"
---
# <a name="sending-messages-to-connectors-and-webhooks"></a>Envoi de messages à des connecteurs et Webhooks

Pour envoyer un message par le biais de votre connecteur Office 365 ou de webhook entrant, vous publiez une charge utile JSON dans l’URL webhook. En règle générale, cette charge utile se présente sous la forme d’une [carte de connecteur Office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).

Vous pouvez également utiliser ce JSON pour créer des cartes contenant des entrées enrichies, telles que l’entrée de texte, la sélection multiple ou la sélection d’une date et d’une heure. Le code qui génère la carte et publie sur l’URL webhook peut être exécuté sur un service hébergé. Ces cartes sont définies dans le cadre de messages intégrant des actions et sont également prises en charge dans les [cartes](~/task-modules-and-cards/what-are-cards.md) utilisées dans les bots Teams et les extensions de messagerie.

### <a name="example-connector-message"></a>Exemple de message de connecteur

```json
{
    "@type": "MessageCard",
    "@context": "http://schema.org/extensions",
    "themeColor": "0076D7",
    "summary": "Larry Bryant created a new task",
    "sections": [{
        "activityTitle": "![TestImage](https://47a92947.ngrok.io/Content/Images/default.png)Larry Bryant created a new task",
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
            "target": "http://..."
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
            "target": "http://..."
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
            "target": "http://..."
        }]
    }]
}
```

Ce message génère la carte suivante dans le canal.

![Capture d’écran d’une carte de connecteur](~/assets/images/connectors/connector_message.png)

## <a name="creating-actionable-messages"></a>Créations des messages intégrant des actions

L’exemple de la section précédente inclut trois boutons visibles sur la carte. Chaque bouton est défini dans la propriété `potentialAction` du message à l’aide d'actions `ActionCard`, contenant chacune un type d’entrée : un champ de texte, un sélecteur de dates ou une liste à choix multiple. Chaque action `ActionCard` est associée à une action (par exemple, `HttpPOST`).

Les cartes de connecteur prennent en charge trois types d’actions :

- `ActionCard` Affiche un ou plusieurs types d’entrées et actions associées
- `HttpPOST` Envoie une demande de publication à une URL.
- `OpenUri` Ouvre un URI dans un navigateur ou une application distincte, cible de façon facultative différents URI basés sur des systèmes d’exploitation

(Une quatrième action, `ViewAction`, n’est pas encore prise en charge, mais n’est plus nécessaire. Utilisez `OpenUri` à la place.)

L'action `ActionCard` prend en charge trois types d'entrée :

- `TextInput` Zone de texte d'une ou plusieurs lignes avec une limite de longueur facultative
- `DateInput` Sélecteur de date avec un sélecteur d’heures facultatif
- `MultichoiceInput` Liste énumérée de choix proposant une sélection unique ou plusieurs sélections

`MultichoiceInput` prend en charge une propriété `style` qui contrôle l’affichage initial complet de la liste. La valeur par défaut de `style` dépend de la valeur de `isMultiSelect`.

| `isMultiSelect` | `style` par défaut |
| --- | --- |
| `false` ou non spécifié | `compact` |
| `true` | `expanded` |

Si vous souhaitez afficher une liste de sélections à l’origine dans le style compact, vous devez spécifier `"isMultiSelect": true` et `"style": true`.

> [!NOTE]
> Spécifier `compact` pour la propriété `style` dans Microsoft Teams revient à spécifier `normal` pour la propriété `style` dans Microsoft Outlook.

Pour accéder à d’autres informations sur les actions de la carte de connecteur, consultez **[Actions ](/outlook/actionable-messages/card-reference#actions)** dans la référence de carte de message intégrant des actions.

## <a name="setting-up-a-custom-incoming-webhook"></a>Configuration d’un webhook entrant personnalisé

Pour découvrir comment envoyer une carte simple à un connecteur, procédez comme suit.

1. Dans Microsoft Teams, choisissez **Autres options** (**&#8943;**) à côté du nom de la chaîne, puis choisissez **Connecteurs**.
2. Faites défiler la liste des Connecteurs à **Webhook entrant**, puis choisissez **Ajouter**.
3. Entrez un nom pour le webhook, téléchargez une image à associer aux données du webhook, puis choisissez**Créer**.
4. Copiez le webhook dans le presse-papiers et enregistrez-le. Vous aurez besoin de l’URL de webhook pour envoyer des informations à Microsoft Teams.
5. Choisissez **OK**.

### <a name="post-a-message-to-the-webhook-using-curl"></a>Publier un message sur le webhook à l’aide de cURL

Les étapes suivantes utilisent [cURL](https://curl.haxx.se/). Nous partons du principe que vous avez installé cette application et que vous êtes familiarisé avec son utilisation de base.

1. Depuis la ligne de commande , entrez la commande cURL suivante :

   ```bash
   // on macOS or Linux
   curl -H 'Content-Type: application/json' -d '{\"text\": \"Hello World\"}' <YOUR WEBHOOK URL>
   ```

   ```bash
   // on Windows
   curl.exe -H 'Content-Type: application/json' -d '{\"text\": \"Hello World\"}' <YOUR WEBHOOK URL>
   ```

2. Si la publication réussit, un simple résultat **1** est affiché par `curl`.
3. Consultez le client Microsoft Team. Vous devriez voir la nouvelle carte publiée dans l’équipe.

### <a name="post-a-message-to-the-webhook-using-powershell"></a>Publier un message sur le webhook à l’aide de PowerShell

Les étapes suivantes utilisent PowerShell. Nous partons du principe que vous avez installé cette application et que vous êtes familiarisé avec son utilisation de base.

1. À partir de l'invite PowerShell, entrez les commandes suivantes :

   ```powershell
   Invoke-RestMethod -Method post -ContentType 'Application/Json' -Body '{"text":"Hello World!"}' -Uri <YOUR WEBHOOK URL>
   ```

2. Si la publication réussit, un simple résultat **1** est affichée par `Invoke-RestMethod`.
3. Vérifiez le canal Microsoft Teams associé à l’URL de webhook. Vous devriez voir la nouvelle carte publiée sur le canal.

- Vous avez le choix entre deux icônes, en suivant les instructions figurant dans [Icônes](~/concepts/build-and-test/apps-package.md#icons).
- Modifiez la partie `icons` du manifeste pour faire référence aux noms de fichier des icônes au lieu des URL.

Le fichier manifest.json suivant contient les éléments de base nécessaires pour tester et envoyer votre application.

> [!NOTE]
> Remplacez `id` et `connectorId` de l’exemple suivant par le GUID de votre connecteur.

#### <a name="example-manifestjson-with-connector"></a>Exemple de fichier manifest.json avec Connecteur

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "id": "e9343a03-0a5e-4c1f-95a8-263a565505a5",
  "version": "1.0",
  "packageName": "com.sampleapp",
  "developer": {
    "name": "Publisher",
    "websiteUrl": "https://www.microsoft.com",
    "privacyUrl": "https://www.microsoft.com",
    "termsOfUseUrl": "https://www.microsoft.com"
  },
  "description": {
    "full": "This is a small sample app we made for you! This app has samples of all capabilities Microsoft Teams supports.",
    "short": "This is a small sample app we made for you!"
  },
  "icons": {
    "outline": "sampleapp-outline.png",
    "color": "sampleapp-color.png"
  },
  "connectors": [
    {
      "connectorId": "e9343a03-0a5e-4c1f-95a8-263a565505a5",
      "scopes": [
        "team"
      ]
    }
  ],
  "name": {
    "short": "Sample App",
    "full": "Sample App"
  },
  "accentColor": "#FFFFFF",
  "needsIdentity": "true"
}
```

## <a name="testing-your-connector"></a>Test du connecteur

Pour tester le connecteur, téléchargez-le dans une équipe comme vous le feriez avec une autre application. Vous pouvez créer un package .zip à l’aide du fichier manifeste à partir du tableau de bord du développeur de connecteurs (modifié comme indiqué dans la section précédente) et des deux fichiers d’icône.

Une fois que vous avez téléchargé l’application, ouvrez la liste des connecteurs à partir de n’importe quel canal. Faites défiler la page vers le bas pour afficher votre application dans la section **Téléchargé**.

![Capture d’écran de la section téléchargée dans la boîte de dialogue connecteur](~/assets/images/connectors/connector_dialog_uploaded.png)

Vous pouvez à présent lancer l’expérience de configuration. N’oubliez pas que ce flux se produit entièrement au sein de Microsoft Teams via une fenêtre indépendante. Pour l’instant, ce comportement diffère de l’expérience de configuration dans les connecteurs que vous avez créés. Nous travaillons à l’unification de l’expérience.

Pour vérifier qu’une action `HttpPOST` fonctionne correctement, utilisez votre [webhook entrant personnalisé](#setting-up-a-custom-incoming-webhook).

## <a name="rate-limiting-for-connectors"></a>Limitation du taux pour les connecteurs

Les limites de débit d'application contrôlent le trafic qu'un connecteur ou un webhook entrant est autorisé à générer sur un canal. Les équipes effectuent le suivi des demandes via une fenêtre à débit fixe et un compteur incrémentiel mesuré en secondes.  Si le nombre de demandes est trop élevé, la connexion client sera limitée jusqu’à l’actualisation de la fenêtre, c’est-à-dire, pour la durée du débit fixe.

### <a name="transactions-per-second-thresholds"></a>**Seuils de transaction par seconde**

| Durée (secondes)  | Nombre maximal de demandes autorisées  |
|---|---|
| 1   | 4  |  
| 30   | 60  |  
| 3600   | 100  |
| 7200 | 150  |
| 86400  | 1800  |

*Voir aussi* [Connecteurs Office 365 — Microsoft Teams](https://docs.microsoft.com/connectors/teams/)

Une [logique des nouvelles tentatives avec une sauvegarde exponentielle](/azure/architecture/patterns/retry) comme ci-dessous permet de limiter les débits pour les cas où les demandes dépassent les limites en une seconde. Veuillez suivre les [meilleures pratiques](../../bots/how-to/rate-limit.md#best-practices) pour éviter d’atteindre les limites de débit.

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
 
Ces limites sont en place pour réduire le courrier indésirable d’un canal par un connecteur et de garantir une expérience optimale pour vos utilisateurs finaux.
