---
title: Créer et envoyer des messages
author: laujan
description: Décrit l’utilisation des Connecteurs Office 365 dans Microsoft Teams
ms.topic: how-to
localization_priority: Normal
keywords: 'équipes connecteur O365 '
ms.openlocfilehash: e396d0048831634f683b6df925853464698fb96a
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140528"
---
# <a name="create-and-send-messages"></a><span data-ttu-id="e91ac-104">Créer et envoyer des messages</span><span class="sxs-lookup"><span data-stu-id="e91ac-104">Create and send messages</span></span>

<span data-ttu-id="e91ac-105">Vous pouvez créer des messages actionnables et les envoyer via le webhook entrant ou Office 365 connector.</span><span class="sxs-lookup"><span data-stu-id="e91ac-105">You can create actionable messages and send it through Incoming Webhook or Office 365 Connector.</span></span>

## <a name="create-actionable-messages"></a><span data-ttu-id="e91ac-106">Créer des messages actionnables</span><span class="sxs-lookup"><span data-stu-id="e91ac-106">Create actionable messages</span></span>

<span data-ttu-id="e91ac-107">Les messages actionnables incluent trois boutons visibles sur la carte.</span><span class="sxs-lookup"><span data-stu-id="e91ac-107">The actionable messages include three visible buttons on the card.</span></span> <span data-ttu-id="e91ac-108">Chaque bouton est défini dans la propriété du message à l’aide d’actions, chacune avec un type d’entrée, un champ de texte, un s sélectionneur de dates ou une liste à `potentialAction` `ActionCard` choix multiples.</span><span class="sxs-lookup"><span data-stu-id="e91ac-108">Each button is defined in the `potentialAction` property of the message by using `ActionCard` actions, each with an input type, a text field, a date picker, or a multi-choice list.</span></span> <span data-ttu-id="e91ac-109">Chaque `ActionCard` action est associée, par `HttpPOST` exemple.</span><span class="sxs-lookup"><span data-stu-id="e91ac-109">Each `ActionCard` has an associated action, for example `HttpPOST`.</span></span>

<span data-ttu-id="e91ac-110">Les cartes de connecteurs prendre en charge les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="e91ac-110">The connector cards support the following actions:</span></span>

- <span data-ttu-id="e91ac-111">`ActionCard`: présente un ou plusieurs types d’entrée et actions associées.</span><span class="sxs-lookup"><span data-stu-id="e91ac-111">`ActionCard`: Presents one or more input types and associated actions.</span></span>
- <span data-ttu-id="e91ac-112">`HttpPOST`: envoie une requête POST à une URL.</span><span class="sxs-lookup"><span data-stu-id="e91ac-112">`HttpPOST`: Sends POST request to a URL.</span></span>
- <span data-ttu-id="e91ac-113">`OpenUri`: ouvre l’URI dans un navigateur ou une application distinct, cible éventuellement différents URI basés sur les systèmes d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="e91ac-113">`OpenUri`: Opens URI in a separate browser or app, optionally targets different URIs based on operating systems.</span></span>

<span data-ttu-id="e91ac-114">L'action `ActionCard` prend en charge trois types d'entrée :</span><span class="sxs-lookup"><span data-stu-id="e91ac-114">The `ActionCard` action supports three input types:</span></span>

- <span data-ttu-id="e91ac-115">`TextInput`: champ de texte à une seule ligne ou à plusieurs lignes avec une limite de longueur facultative.</span><span class="sxs-lookup"><span data-stu-id="e91ac-115">`TextInput`: A single line or multiline text field with an optional length limit.</span></span>
- <span data-ttu-id="e91ac-116">`DateInput`: sélecteur de dates avec un sélecteur d’heure facultatif.</span><span class="sxs-lookup"><span data-stu-id="e91ac-116">`DateInput`: A date selector with an optional time selector.</span></span>
- <span data-ttu-id="e91ac-117">`MultichoiceInput`: Liste énumérée de choix offrant une sélection unique ou plusieurs sélections.</span><span class="sxs-lookup"><span data-stu-id="e91ac-117">`MultichoiceInput`: An enumerated list of choices offering either a single selection or multiple selections.</span></span>

<span data-ttu-id="e91ac-118">`MultichoiceInput` prend en charge une propriété `style` qui contrôle l’affichage initial complet de la liste.</span><span class="sxs-lookup"><span data-stu-id="e91ac-118">`MultichoiceInput` supports a `style` property that controls whether the list initially appears fully expanded.</span></span> <span data-ttu-id="e91ac-119">La valeur par défaut `style` dépend de la valeur suivante `isMultiSelect` :</span><span class="sxs-lookup"><span data-stu-id="e91ac-119">The default value of `style` depends on the value of `isMultiSelect` as follows:</span></span>

| `isMultiSelect` | <span data-ttu-id="e91ac-120">`style` par défaut</span><span class="sxs-lookup"><span data-stu-id="e91ac-120">`style` default</span></span> |
| --- | --- |
| <span data-ttu-id="e91ac-121">`false` ou non spécifié</span><span class="sxs-lookup"><span data-stu-id="e91ac-121">`false` or not specified</span></span> | `compact` |
| `true` | `expanded` |

<span data-ttu-id="e91ac-122">Pour afficher la liste de plusieursélections dans le style compact, vous devez spécifier les deux `"isMultiSelect": true` et `"style": true` .</span><span class="sxs-lookup"><span data-stu-id="e91ac-122">To display the multiselect list in the compact style, you must specify both `"isMultiSelect": true` and `"style": true`.</span></span>

<span data-ttu-id="e91ac-123">Pour plus d’informations sur les actions de carte de connecteur, voir [Actions.](/outlook/actionable-messages/card-reference#actions)</span><span class="sxs-lookup"><span data-stu-id="e91ac-123">For more information on connector card actions, see [Actions](/outlook/actionable-messages/card-reference#actions).</span></span>

> [!NOTE]
> * <span data-ttu-id="e91ac-124">Spécifier `compact` pour la propriété `style` dans Microsoft Teams revient à spécifier `normal` pour la propriété `style` dans Microsoft Outlook.</span><span class="sxs-lookup"><span data-stu-id="e91ac-124">Specifying `compact` for the `style` property in Microsoft Teams is the same as specifying `normal` for the `style` property in Microsoft Outlook.</span></span>
> * <span data-ttu-id="e91ac-125">Pour l’action HttpPOST, le jeton du porteur est inclus dans les demandes.</span><span class="sxs-lookup"><span data-stu-id="e91ac-125">For the HttpPOST action, the bearer token is included with the requests.</span></span> <span data-ttu-id="e91ac-126">Ce jeton inclut l’identité Azure AD de l’utilisateur Office 365 sujet de l’action.</span><span class="sxs-lookup"><span data-stu-id="e91ac-126">This token includes the Azure AD identity of the Office 365 user who took the action.</span></span>

## <a name="send-a-message-through-incoming-webhook-or-office-365-connector"></a><span data-ttu-id="e91ac-127">Envoyer un message via le webhook entrant ou Office 365 connector</span><span class="sxs-lookup"><span data-stu-id="e91ac-127">Send a message through Incoming Webhook or Office 365 Connector</span></span>

<span data-ttu-id="e91ac-128">Pour envoyer un message via votre webhook entrant ou votre connecteur Office 365, publiez une charge utile JSON sur l’URL du webhook.</span><span class="sxs-lookup"><span data-stu-id="e91ac-128">To send a message through your Incoming Webhook or Office 365 Connector, post a JSON payload to the webhook URL.</span></span> <span data-ttu-id="e91ac-129">Cette charge utile doit prendre la forme d’une [carte Office 365 connecteur.](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)</span><span class="sxs-lookup"><span data-stu-id="e91ac-129">This payload must be in the form of an [Office 365 connector card](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span></span>

<span data-ttu-id="e91ac-130">Vous pouvez également utiliser ce JSON pour créer des cartes contenant des entrées enrichies, telles que l’entrée de texte, la sélection multiple ou la sélection de date et d’heure.</span><span class="sxs-lookup"><span data-stu-id="e91ac-130">You can also use this JSON to create cards containing rich inputs, such as text entry, multiselect, or selecting date and time.</span></span> <span data-ttu-id="e91ac-131">Le code qui génère la carte et la publie sur l’URL de webhook peut s’exécuter sur n’importe quel service hébergé.</span><span class="sxs-lookup"><span data-stu-id="e91ac-131">The code that generates the card and posts it to the webhook URL can run on any hosted service.</span></span> <span data-ttu-id="e91ac-132">Ces cartes sont définies dans le cadre de messages actionnables et sont également prises en charge dans les [cartes,](~/task-modules-and-cards/what-are-cards.md)utilisées dans Teams bots et extensions de messagerie.</span><span class="sxs-lookup"><span data-stu-id="e91ac-132">These cards are defined as part of actionable messages and are also supported in [cards](~/task-modules-and-cards/what-are-cards.md), used in Teams bots and messaging extensions.</span></span>

### <a name="example-of-connector-message"></a><span data-ttu-id="e91ac-133">Exemple de message de connecteur</span><span class="sxs-lookup"><span data-stu-id="e91ac-133">Example of connector message</span></span>

<span data-ttu-id="e91ac-134">Voici un exemple de message de connecteur :</span><span class="sxs-lookup"><span data-stu-id="e91ac-134">An example of connector message is as follows:</span></span>

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

<span data-ttu-id="e91ac-135">Ce message fournit la carte suivante dans le canal :</span><span class="sxs-lookup"><span data-stu-id="e91ac-135">This message provides the following card in the channel:</span></span>

![Capture d’écran d’une carte de connecteur](~/assets/images/connectorcard.png)

## <a name="send-messages-using-curl-and-powershell"></a><span data-ttu-id="e91ac-137">Envoyer des messages à l’aide de cURL et de PowerShell</span><span class="sxs-lookup"><span data-stu-id="e91ac-137">Send messages using cURL and PowerShell</span></span>

# <a name="curl"></a>[<span data-ttu-id="e91ac-138">cURL</span><span class="sxs-lookup"><span data-stu-id="e91ac-138">cURL</span></span>](#tab/cURL)

<span data-ttu-id="e91ac-139">**Pour publier un message dans le webhook avec cURL**</span><span class="sxs-lookup"><span data-stu-id="e91ac-139">**To post a message in the webhook with cURL**</span></span>

1. <span data-ttu-id="e91ac-140">Installez cURL à l’aide de https://curl.haxx.se/ : .</span><span class="sxs-lookup"><span data-stu-id="e91ac-140">Install cURL using: https://curl.haxx.se/.</span></span>

1. <span data-ttu-id="e91ac-141">Depuis la ligne de commande , entrez la commande cURL suivante :</span><span class="sxs-lookup"><span data-stu-id="e91ac-141">From the command line, enter the following cURL command:</span></span>

   ```bash
   // on macOS or Linux
   curl -H 'Content-Type: application/json' -d '{"text": "Hello World"}' <YOUR WEBHOOK URL>
   ```

   ```bash
   // on Windows
   curl.exe -H "Content-Type:application/json" -d "{'text':'Hello World'}" <YOUR WEBHOOK URL>
   ```

    > [!NOTE]
    > <span data-ttu-id="e91ac-142">Si la publication réussit, vous devez voir une sortie **simple de 1** `curl` par .</span><span class="sxs-lookup"><span data-stu-id="e91ac-142">If the POST succeeds, you must see a simple **1** output by `curl`.</span></span>

1. <span data-ttu-id="e91ac-143">Vérifiez la Microsoft Teams client pour la nouvelle carte publiée.</span><span class="sxs-lookup"><span data-stu-id="e91ac-143">Check the Microsoft Teams client for the new card posted.</span></span>

# <a name="powershell"></a>[<span data-ttu-id="e91ac-144">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e91ac-144">PowerShell</span></span>](#tab/PowerShell)

 <span data-ttu-id="e91ac-145">Conditions préalables : installation de PowerShell et familiarisation avec son utilisation de base.</span><span class="sxs-lookup"><span data-stu-id="e91ac-145">Prerequisite: Installation of PowerShell and familiarization with its basic usage.</span></span>

<span data-ttu-id="e91ac-146">**Pour publier un message sur le webhook avec PowerShell**</span><span class="sxs-lookup"><span data-stu-id="e91ac-146">**To post a message to the webhook with PowerShell**</span></span>

1. <span data-ttu-id="e91ac-147">À partir de l'invite PowerShell, entrez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="e91ac-147">From the PowerShell prompt, enter the following command:</span></span>

   ```powershell
   Invoke-RestMethod -Method post -ContentType 'Application/Json' -Body '{"text":"Hello World!"}' -Uri <YOUR WEBHOOK URL>
   ```

    > [!NOTE]
    > <span data-ttu-id="e91ac-148">Si la publication réussit, vous devez voir une sortie **simple de 1** `Invoke-RestMethod` par .</span><span class="sxs-lookup"><span data-stu-id="e91ac-148">If the POST succeeds, you must see a simple **1** output by `Invoke-RestMethod`.</span></span>

1. <span data-ttu-id="e91ac-149">Vérifiez le canal Microsoft Teams associé à l’URL de webhook.</span><span class="sxs-lookup"><span data-stu-id="e91ac-149">Check the Microsoft Teams channel associated with the webhook URL.</span></span> <span data-ttu-id="e91ac-150">Vous pouvez voir la nouvelle carte publiée sur le canal.</span><span class="sxs-lookup"><span data-stu-id="e91ac-150">You can see the new card posted to the channel.</span></span> <span data-ttu-id="e91ac-151">Avant d’utiliser le connecteur pour tester ou publier votre application, vous devez :</span><span class="sxs-lookup"><span data-stu-id="e91ac-151">Before you use the connector to test or publish your app, you must do the following:</span></span>

    - <span data-ttu-id="e91ac-152">[Incluez deux icônes](../../concepts/build-and-test/apps-package.md#app-icons).</span><span class="sxs-lookup"><span data-stu-id="e91ac-152">[Include two icons](../../concepts/build-and-test/apps-package.md#app-icons).</span></span>
    - <span data-ttu-id="e91ac-153">Modifiez la partie du manifeste sur les noms de fichiers des icônes au lieu `icons` des URL.</span><span class="sxs-lookup"><span data-stu-id="e91ac-153">Modify the `icons` portion of the manifest to the file names of the icons instead of URLs.</span></span>

---

## <a name="send-adaptive-cards-using-an-incoming-webhook"></a><span data-ttu-id="e91ac-154">Envoyer des cartes adaptatives à l’aide d’un webhook entrant</span><span class="sxs-lookup"><span data-stu-id="e91ac-154">Send Adaptive Cards using an Incoming Webhook</span></span>

> [!NOTE]
> * <span data-ttu-id="e91ac-155">Tous les éléments de schéma de carte adaptative native, à l’exception `Action.Submit` de , sont entièrement pris en charge.</span><span class="sxs-lookup"><span data-stu-id="e91ac-155">All native Adaptive Card schema elements, except `Action.Submit`, are fully supported.</span></span>
> * <span data-ttu-id="e91ac-156">Les actions prises en [**charge sont Action.OpenURL,**](https://adaptivecards.io/explorer/Action.OpenUrl.html) [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html)et [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html).</span><span class="sxs-lookup"><span data-stu-id="e91ac-156">The supported actions are [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html), and [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html).</span></span>

<span data-ttu-id="e91ac-157">**Pour envoyer des cartes adaptatives via un webhook entrant**</span><span class="sxs-lookup"><span data-stu-id="e91ac-157">**To send Adaptive Cards through an Incoming Webhook**</span></span>

1. <span data-ttu-id="e91ac-158">[Configurer un webhook personnalisé dans](/add-incoming-webhook.md) Teams.</span><span class="sxs-lookup"><span data-stu-id="e91ac-158">[Setup a custom webhook](/add-incoming-webhook.md) in Teams.</span></span>
1. <span data-ttu-id="e91ac-159">Créez un fichier JSON de carte adaptative à l’aide du code suivant :</span><span class="sxs-lookup"><span data-stu-id="e91ac-159">Create Adaptive Card JSON file using the following code:</span></span>

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

    <span data-ttu-id="e91ac-160">Les propriétés du fichier JSON de carte adaptative sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="e91ac-160">The properties for Adaptive Card JSON file are as follows:</span></span>

    * <span data-ttu-id="e91ac-161">Le `"type"` champ doit être`"message"`.</span><span class="sxs-lookup"><span data-stu-id="e91ac-161">The `"type"` field must be `"message"`.</span></span>
    * <span data-ttu-id="e91ac-162">Le`"attachments"` tableau contient un ensemble d'objets carte.</span><span class="sxs-lookup"><span data-stu-id="e91ac-162">The `"attachments"` array contains a set of card objects.</span></span>
    * <span data-ttu-id="e91ac-163">Le `"contentType"` champ doit être de type Carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="e91ac-163">The `"contentType"` field must be set to Adaptive Card type.</span></span>
    * <span data-ttu-id="e91ac-164">L’`"content"` objet est la carte formatée en JSON.</span><span class="sxs-lookup"><span data-stu-id="e91ac-164">The `"content"` object is the card formatted in JSON.</span></span>

1. <span data-ttu-id="e91ac-165">Testez votre carte adaptative avec Postman :</span><span class="sxs-lookup"><span data-stu-id="e91ac-165">Test your Adaptive Card with Postman:</span></span>

    * <span data-ttu-id="e91ac-166">Testez la carte adaptative à l’aide [de Postman](https://www.postman.com) pour envoyer une requête POST à l’URL, créée pour configurer le webhook entrant.</span><span class="sxs-lookup"><span data-stu-id="e91ac-166">Test the Adaptive Card using [Postman](https://www.postman.com) to send a POST request to the URL, created to set up Incoming Webhook.</span></span>
    * <span data-ttu-id="e91ac-167">Collez le fichier JSON dans le corps de la demande et affichez le message de carte adaptative dans Teams.</span><span class="sxs-lookup"><span data-stu-id="e91ac-167">Paste the JSON file in the body of the request and view the Adaptive Card message in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="e91ac-168">Utilisez des [exemples de code et des modèles](https://adaptivecards.io/samples) de carte adaptative pour tester le corps de la requête POST.</span><span class="sxs-lookup"><span data-stu-id="e91ac-168">Use Adaptive Card [code samples and templates](https://adaptivecards.io/samples) to test the body of POST request.</span></span>

## <a name="rate-limiting-for-connectors"></a><span data-ttu-id="e91ac-169">Limitation du taux pour les connecteurs</span><span class="sxs-lookup"><span data-stu-id="e91ac-169">Rate limiting for connectors</span></span>

<span data-ttu-id="e91ac-170">Les limites de fréquence d’application contrôlent le trafic qu’un connecteur ou un webhook entrant est autorisé à générer sur un canal.</span><span class="sxs-lookup"><span data-stu-id="e91ac-170">Application rate limits control the traffic that a connector or an Incoming Webhook is permitted to generate on a channel.</span></span> <span data-ttu-id="e91ac-171">Teams les demandes à l’aide d’une fenêtre à taux fixe et d’un compteur incrémentielle mesuré en secondes.</span><span class="sxs-lookup"><span data-stu-id="e91ac-171">Teams track requests using a fixed rate window and incremental counter measured in seconds.</span></span> <span data-ttu-id="e91ac-172">Si plus de quatre demandes sont faites en une seconde, la connexion client est limitée jusqu’à ce que la fenêtre s’actualise pendant la durée du taux fixe.</span><span class="sxs-lookup"><span data-stu-id="e91ac-172">If more than four requests are made in a second, the client connection is throttled until the window refreshes for the duration of the fixed rate.</span></span>

### <a name="transactions-per-second-thresholds"></a><span data-ttu-id="e91ac-173">Seuils de transaction par seconde</span><span class="sxs-lookup"><span data-stu-id="e91ac-173">Transactions per second thresholds</span></span>

<span data-ttu-id="e91ac-174">Le tableau suivant fournit les détails des transactions basées sur le temps :</span><span class="sxs-lookup"><span data-stu-id="e91ac-174">The following table provides the time based transaction details:</span></span>

| <span data-ttu-id="e91ac-175">Durée en secondes</span><span class="sxs-lookup"><span data-stu-id="e91ac-175">Time in seconds</span></span>  | <span data-ttu-id="e91ac-176">Nombre maximal de demandes autorisées</span><span class="sxs-lookup"><span data-stu-id="e91ac-176">Maximum allowed requests</span></span>  |
|---|---|
| <span data-ttu-id="e91ac-177">1 </span><span class="sxs-lookup"><span data-stu-id="e91ac-177">1</span></span>   | <span data-ttu-id="e91ac-178">4 </span><span class="sxs-lookup"><span data-stu-id="e91ac-178">4</span></span>  |  
| <span data-ttu-id="e91ac-179">30</span><span class="sxs-lookup"><span data-stu-id="e91ac-179">30</span></span>   | <span data-ttu-id="e91ac-180">60</span><span class="sxs-lookup"><span data-stu-id="e91ac-180">60</span></span>  |  
| <span data-ttu-id="e91ac-181">3600</span><span class="sxs-lookup"><span data-stu-id="e91ac-181">3600</span></span>   | <span data-ttu-id="e91ac-182">100</span><span class="sxs-lookup"><span data-stu-id="e91ac-182">100</span></span>  |
| <span data-ttu-id="e91ac-183">7200</span><span class="sxs-lookup"><span data-stu-id="e91ac-183">7200</span></span> | <span data-ttu-id="e91ac-184">150</span><span class="sxs-lookup"><span data-stu-id="e91ac-184">150</span></span>  |
| <span data-ttu-id="e91ac-185">86400</span><span class="sxs-lookup"><span data-stu-id="e91ac-185">86400</span></span>  | <span data-ttu-id="e91ac-186">1800</span><span class="sxs-lookup"><span data-stu-id="e91ac-186">1800</span></span>  |

<span data-ttu-id="e91ac-187">Une [logique de nouvelle tentative avec](/azure/architecture/patterns/retry) un délai d’attente exponentiel peut atténuer la limitation des taux pour les cas où les demandes dépassent les limites en l’espace d’une seconde.</span><span class="sxs-lookup"><span data-stu-id="e91ac-187">A [retry logic with exponential back-off](/azure/architecture/patterns/retry) can mitigate rate limiting for cases where requests are exceeding the limits within a second.</span></span> <span data-ttu-id="e91ac-188">Suivez [les meilleures pratiques](../../bots/how-to/rate-limit.md) pour éviter d’atteindre les limites de taux.</span><span class="sxs-lookup"><span data-stu-id="e91ac-188">Follow [best practices](../../bots/how-to/rate-limit.md) to avoid hitting the rate limits.</span></span>

> [!NOTE]
> <span data-ttu-id="e91ac-189">Une [logique de nouvelle tentative avec](/azure/architecture/patterns/retry) un délai d’attente exponentiel peut atténuer la limitation des taux pour les cas où les demandes dépassent les limites en l’espace d’une seconde.</span><span class="sxs-lookup"><span data-stu-id="e91ac-189">A [retry logic with exponential back-off](/azure/architecture/patterns/retry) can mitigate rate limiting for cases where requests are exceeding the limits within a second.</span></span> <span data-ttu-id="e91ac-190">Référez-vous aux [réponses du protocole HTTP 429](../../bots/how-to/rate-limit.md#handle-http-429-responses) pour éviter de vous heurter aux limites de taux.</span><span class="sxs-lookup"><span data-stu-id="e91ac-190">Refer [HTTP 429 responses](../../bots/how-to/rate-limit.md#handle-http-429-responses) to avoid hitting the rate limits.</span></span>

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

<span data-ttu-id="e91ac-191">Ces limites sont en place pour réduire le courrier indésirable d’un canal par un connecteur et garantissent une expérience optimale aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="e91ac-191">These limits are in place to reduce spamming a channel by a connector and ensures an optimal experience to users.</span></span>

## <a name="see-also"></a><span data-ttu-id="e91ac-192">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="e91ac-192">See also</span></span>

* [<span data-ttu-id="e91ac-193">Office 365 Connecteurs pour Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="e91ac-193">Office 365 Connectors for Microsoft Teams</span></span>](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [<span data-ttu-id="e91ac-194">Créer un webhook entrant</span><span class="sxs-lookup"><span data-stu-id="e91ac-194">Create an Incoming Webhook</span></span>](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [<span data-ttu-id="e91ac-195">Créer un webhook sortant</span><span class="sxs-lookup"><span data-stu-id="e91ac-195">Create an Outgoing Webhook</span></span>](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)
