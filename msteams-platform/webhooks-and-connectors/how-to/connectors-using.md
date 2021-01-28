---
title: Envoi de messages à des connecteurs et Webhooks
description: Décrit l’utilisation des Connecteurs Office 365 dans Microsoft Teams
ms.topic: how-to
localization_priority: Priority
keywords: 'équipes connecteur O365 '
ms.openlocfilehash: 36d30c0be3d562c7a71989355249f0cfa76e797d
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014081"
---
# <a name="sending-messages-to-connectors-and-webhooks"></a><span data-ttu-id="79761-104">Envoi de messages à des connecteurs et Webhooks</span><span class="sxs-lookup"><span data-stu-id="79761-104">Sending messages to connectors and webhooks</span></span>

<span data-ttu-id="79761-105">Pour envoyer un message par le biais de votre connecteur Office 365 ou de webhook entrant, vous publiez une charge utile JSON dans l’URL webhook.</span><span class="sxs-lookup"><span data-stu-id="79761-105">To send a message through your Office 365 Connector or incoming webhook, you post a JSON payload to the webhook URL.</span></span> <span data-ttu-id="79761-106">En règle générale, cette charge utile se présente sous la forme d’une [carte de connecteur Office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span><span class="sxs-lookup"><span data-stu-id="79761-106">Typically this payload will be in the form of an [Office 365 Connector Card](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span></span>

<span data-ttu-id="79761-107">Vous pouvez également utiliser ce JSON pour créer des cartes contenant des entrées enrichies, telles que l’entrée de texte, la sélection multiple ou la sélection d’une date et d’une heure.</span><span class="sxs-lookup"><span data-stu-id="79761-107">You can also use this JSON to create cards containing rich inputs, such as text entry, multi-select, or picking a date and time.</span></span> <span data-ttu-id="79761-108">Le code qui génère la carte et publie sur l’URL webhook peut être exécuté sur un service hébergé.</span><span class="sxs-lookup"><span data-stu-id="79761-108">The code that generates the card and posts to the webhook URL can be running on any hosted service.</span></span> <span data-ttu-id="79761-109">Ces cartes sont définies dans le cadre de messages intégrant des actions et sont également prises en charge dans les [cartes](~/task-modules-and-cards/what-are-cards.md) utilisées dans les bots Teams et les extensions de messagerie.</span><span class="sxs-lookup"><span data-stu-id="79761-109">These cards are defined as part of actionable messages, and are also supported in [cards](~/task-modules-and-cards/what-are-cards.md) used in Teams bots and Messaging extensions.</span></span>

### <a name="example-connector-message"></a><span data-ttu-id="79761-110">Exemple de message de connecteur</span><span class="sxs-lookup"><span data-stu-id="79761-110">Example connector message</span></span>

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

<span data-ttu-id="79761-111">Ce message génère la carte suivante dans le canal.</span><span class="sxs-lookup"><span data-stu-id="79761-111">This message produces the following card in the channel.</span></span>

![Capture d’écran d’une carte de connecteur](~/assets/images/connectors/connector_message.png)

## <a name="creating-actionable-messages"></a><span data-ttu-id="79761-113">Créations des messages intégrant des actions</span><span class="sxs-lookup"><span data-stu-id="79761-113">Creating actionable messages</span></span>

<span data-ttu-id="79761-114">L’exemple de la section précédente inclut trois boutons visibles sur la carte.</span><span class="sxs-lookup"><span data-stu-id="79761-114">The example in the preceding section includes three visible buttons on the card.</span></span> <span data-ttu-id="79761-115">Chaque bouton est défini dans la propriété `potentialAction` du message à l’aide d'actions `ActionCard`, contenant chacune un type d’entrée : un champ de texte, un sélecteur de dates ou une liste à choix multiple.</span><span class="sxs-lookup"><span data-stu-id="79761-115">Each button is defined in the `potentialAction` property of the message by using `ActionCard` actions, each containing an input type: a text field, a date picker, or a multi-choice list.</span></span> <span data-ttu-id="79761-116">Chaque action `ActionCard` est associée à une action (par exemple, `HttpPOST`).</span><span class="sxs-lookup"><span data-stu-id="79761-116">Each `ActionCard` action has an associated action, for example `HttpPOST`.</span></span>

<span data-ttu-id="79761-117">Les cartes de connecteur prennent en charge trois types d’actions :</span><span class="sxs-lookup"><span data-stu-id="79761-117">Connector cards support three types of actions:</span></span>

- <span data-ttu-id="79761-118">`ActionCard` Affiche un ou plusieurs types d’entrées et actions associées</span><span class="sxs-lookup"><span data-stu-id="79761-118">`ActionCard` Presents one or more input types and associated actions</span></span>
- <span data-ttu-id="79761-119">`HttpPOST` Envoie une demande de publication à une URL.</span><span class="sxs-lookup"><span data-stu-id="79761-119">`HttpPOST` Sends a POST request to a URL</span></span>
- <span data-ttu-id="79761-120">`OpenUri` Ouvre un URI dans un navigateur ou une application distincte, cible de façon facultative différents URI basés sur des systèmes d’exploitation</span><span class="sxs-lookup"><span data-stu-id="79761-120">`OpenUri` Opens a URI in a separate browser or app; optionally targets different URIs based on operating systems</span></span>

<span data-ttu-id="79761-121">L'action `ActionCard` prend en charge trois types d'entrée :</span><span class="sxs-lookup"><span data-stu-id="79761-121">The `ActionCard` action supports three input types:</span></span>

- <span data-ttu-id="79761-122">`TextInput` Zone de texte d'une ou plusieurs lignes avec une limite de longueur facultative</span><span class="sxs-lookup"><span data-stu-id="79761-122">`TextInput` A single-line or multiline text field with an optional length limit</span></span>
- <span data-ttu-id="79761-123">`DateInput` Sélecteur de date avec un sélecteur d’heures facultatif</span><span class="sxs-lookup"><span data-stu-id="79761-123">`DateInput` A date selector with an optional time selector</span></span>
- <span data-ttu-id="79761-124">`MultichoiceInput` Liste énumérée de choix proposant une sélection unique ou plusieurs sélections</span><span class="sxs-lookup"><span data-stu-id="79761-124">`MultichoiceInput` A enumerated list of choices offering either a single selection or multiple selections</span></span>

<span data-ttu-id="79761-125">`MultichoiceInput` prend en charge une propriété `style` qui contrôle l’affichage initial complet de la liste.</span><span class="sxs-lookup"><span data-stu-id="79761-125">`MultichoiceInput` supports a `style` property that controls whether the list initially appears fully expanded.</span></span> <span data-ttu-id="79761-126">La valeur par défaut de `style` dépend de la valeur de `isMultiSelect`.</span><span class="sxs-lookup"><span data-stu-id="79761-126">The default value of `style` depends on the value of `isMultiSelect`.</span></span>

| `isMultiSelect` | <span data-ttu-id="79761-127">`style` par défaut</span><span class="sxs-lookup"><span data-stu-id="79761-127">`style` default</span></span> |
| --- | --- |
| <span data-ttu-id="79761-128">`false` ou non spécifié</span><span class="sxs-lookup"><span data-stu-id="79761-128">`false` or not specified</span></span> | `compact` |
| `true` | `expanded` |

<span data-ttu-id="79761-129">Si vous souhaitez afficher une liste de sélections à l’origine dans le style compact, vous devez spécifier `"isMultiSelect": true` et `"style": true`.</span><span class="sxs-lookup"><span data-stu-id="79761-129">If you want a multiselect list initially displayed in the compact style, you must specify both `"isMultiSelect": true` and `"style": true`.</span></span>

> [!NOTE]
> <span data-ttu-id="79761-130">Spécifier `compact` pour la propriété `style` dans Microsoft Teams revient à spécifier `normal` pour la propriété `style` dans Microsoft Outlook.</span><span class="sxs-lookup"><span data-stu-id="79761-130">Specifying `compact` for the `style` property in Microsoft Teams is the same as specifying `normal` for the `style` property in Microsoft Outlook.</span></span>

<span data-ttu-id="79761-131">Pour accéder à d’autres informations sur les actions de la carte de connecteur, consultez **[Actions](/outlook/actionable-messages/card-reference#actions)** dans la référence de carte de message intégrant des actions.</span><span class="sxs-lookup"><span data-stu-id="79761-131">For all other details about Connector card actions, see **[Actions](/outlook/actionable-messages/card-reference#actions)** in the actionable message card reference.</span></span>

## <a name="setting-up-a-custom-incoming-webhook"></a><span data-ttu-id="79761-132">Configuration d’un webhook entrant personnalisé</span><span class="sxs-lookup"><span data-stu-id="79761-132">Setting up a custom incoming webhook</span></span>

<span data-ttu-id="79761-133">Pour découvrir comment envoyer une carte simple à un connecteur, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="79761-133">Follow these steps to see how to send a simple card to a Connector.</span></span>

1. <span data-ttu-id="79761-134">Dans Microsoft Teams, choisissez **Autres options** (**&#8943;**) à côté du nom de la chaîne, puis choisissez **Connecteurs**.</span><span class="sxs-lookup"><span data-stu-id="79761-134">In Microsoft Teams, choose **More options** (**&#8943;**) next to the channel name and then choose **Connectors**.</span></span>
2. <span data-ttu-id="79761-135">Faites défiler la liste des Connecteurs à **Webhook entrant**, puis choisissez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="79761-135">Scroll through the list of Connectors to **Incoming Webhook**, and choose **Add**.</span></span>
3. <span data-ttu-id="79761-136">Entrez un nom pour le webhook, téléchargez une image à associer aux données du webhook, puis choisissez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="79761-136">Enter a name for the webhook, upload an image to associate with data from the webhook, and choose **Create**.</span></span>
4. <span data-ttu-id="79761-137">Copiez le webhook dans le presse-papiers et enregistrez-le.</span><span class="sxs-lookup"><span data-stu-id="79761-137">Copy the webhook to the clipboard and save it.</span></span> <span data-ttu-id="79761-138">Vous aurez besoin de l’URL de webhook pour envoyer des informations à Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="79761-138">You'll need the webhook URL for sending information to Microsoft Teams.</span></span>
5. <span data-ttu-id="79761-139">Choisissez **OK**.</span><span class="sxs-lookup"><span data-stu-id="79761-139">Choose **Done**.</span></span>

### <a name="post-a-message-to-the-webhook-using-curl"></a><span data-ttu-id="79761-140">Publier un message sur le webhook à l’aide de cURL</span><span class="sxs-lookup"><span data-stu-id="79761-140">Post a message to the webhook using cURL</span></span>

<span data-ttu-id="79761-141">Les étapes suivantes utilisent [cURL](https://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="79761-141">The following steps use [cURL](https://curl.haxx.se/).</span></span> <span data-ttu-id="79761-142">Nous partons du principe que vous avez installé cette application et que vous êtes familiarisé avec son utilisation de base.</span><span class="sxs-lookup"><span data-stu-id="79761-142">We assume that you have this installed and are familiar with its basic usage.</span></span>

1. <span data-ttu-id="79761-143">Depuis la ligne de commande , entrez la commande cURL suivante :</span><span class="sxs-lookup"><span data-stu-id="79761-143">From the command line, enter the following cURL command:</span></span>

   ```bash
   // on macOS or Linux
   curl -H 'Content-Type: application/json' -d '{"text": "Hello World"}' <YOUR WEBHOOK URL>
   ```

   ```bash
   // on Windows
   curl.exe -H "Content-Type:application/json" -d "{'text':'Hello World'}" <YOUR WEBHOOK URL>
   ```

2. <span data-ttu-id="79761-144">Si la publication réussit, un simple résultat **1** est affiché par `curl`.</span><span class="sxs-lookup"><span data-stu-id="79761-144">If the POST succeeds, you should see a simple **1** output by `curl`.</span></span>
3. <span data-ttu-id="79761-145">Consultez le client Microsoft Team.</span><span class="sxs-lookup"><span data-stu-id="79761-145">Check the Microsoft Team client.</span></span> <span data-ttu-id="79761-146">Vous devriez voir la nouvelle carte publiée dans l’équipe.</span><span class="sxs-lookup"><span data-stu-id="79761-146">You should see the new card posted to the team.</span></span>

### <a name="post-a-message-to-the-webhook-using-powershell"></a><span data-ttu-id="79761-147">Publier un message sur le webhook à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="79761-147">Post a message to the webhook using PowerShell</span></span>

<span data-ttu-id="79761-148">Les étapes suivantes utilisent PowerShell.</span><span class="sxs-lookup"><span data-stu-id="79761-148">The following steps use PowerShell.</span></span> <span data-ttu-id="79761-149">Nous partons du principe que vous avez installé cette application et que vous êtes familiarisé avec son utilisation de base.</span><span class="sxs-lookup"><span data-stu-id="79761-149">We assume that you have this installed and are familiar with its basic usage.</span></span>

1. <span data-ttu-id="79761-150">À partir de l'invite PowerShell, entrez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="79761-150">From the PowerShell prompt, enter the following command:</span></span>

   ```powershell
   Invoke-RestMethod -Method post -ContentType 'Application/Json' -Body '{"text":"Hello World!"}' -Uri <YOUR WEBHOOK URL>
   ```

2. <span data-ttu-id="79761-151">Si la publication réussit, un simple résultat **1** est affichée par `Invoke-RestMethod`.</span><span class="sxs-lookup"><span data-stu-id="79761-151">If the POST succeeds, you should see a simple **1** output by `Invoke-RestMethod`.</span></span>
3. <span data-ttu-id="79761-152">Vérifiez le canal Microsoft Teams associé à l’URL de webhook.</span><span class="sxs-lookup"><span data-stu-id="79761-152">Check the Microsoft Teams channel associated with the webhook URL.</span></span> <span data-ttu-id="79761-153">Vous devriez voir la nouvelle carte publiée sur le canal.</span><span class="sxs-lookup"><span data-stu-id="79761-153">You should see the new card posted to the channel.</span></span>

- <span data-ttu-id="79761-154">[Incluez deux icônes](../../concepts/build-and-test/apps-package.md#app-icons).</span><span class="sxs-lookup"><span data-stu-id="79761-154">[Include two icons](../../concepts/build-and-test/apps-package.md#app-icons).</span></span>
- <span data-ttu-id="79761-155">Modifiez la partie `icons` du manifeste pour faire référence aux noms de fichier des icônes au lieu des URL.</span><span class="sxs-lookup"><span data-stu-id="79761-155">Modify the `icons` portion of the manifest to refer to the file names of the icons instead of URLs.</span></span>

<span data-ttu-id="79761-156">Le fichier manifest.json suivant contient les éléments de base nécessaires pour tester et envoyer votre application.</span><span class="sxs-lookup"><span data-stu-id="79761-156">The following manifest.json file contains the basic elements needed to test and submit your app.</span></span>

> [!NOTE]
> <span data-ttu-id="79761-157">Remplacez `id` et `connectorId` de l’exemple suivant par le GUID de votre connecteur.</span><span class="sxs-lookup"><span data-stu-id="79761-157">Replace `id` and `connectorId` in the following example with the GUID of your Connector.</span></span>

#### <a name="example-manifestjson-with-connector"></a><span data-ttu-id="79761-158">Exemple de fichier manifest.json avec Connecteur</span><span class="sxs-lookup"><span data-stu-id="79761-158">Example manifest.json with connector</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
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

## <a name="send-adaptive-cards-using-an-incoming-webhook"></a><span data-ttu-id="79761-159">Envoyer des cartes adaptatives à l'aide d'un webhook entrant</span><span class="sxs-lookup"><span data-stu-id="79761-159">Send adaptive cards using an incoming webhook</span></span>

> [!NOTE]
>
> <span data-ttu-id="79761-160">✔ Tous les éléments du schéma de la carte adaptative native, à l'exception`Action.Submit`, sont entièrement pris en charge.</span><span class="sxs-lookup"><span data-stu-id="79761-160">✔ All native adaptive card schema elements, except `Action.Submit`, are fully supported.</span></span>
>
> <span data-ttu-id="79761-161">✔ Les actions soutenues sont [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html),et [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html).</span><span class="sxs-lookup"><span data-stu-id="79761-161">✔ The supported Actions are [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html), and [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html).</span></span>

### <a name="the-flow-for-sending-adaptive-cards-via-an-incoming-webhook-is-as-follows"></a><span data-ttu-id="79761-162">Le flux pour l'envoi[de cartes adaptatives](../../task-modules-and-cards/cards/cards-reference.md#adaptive-card) via un webhook entrant est le suivant :</span><span class="sxs-lookup"><span data-stu-id="79761-162">The flow for sending [adaptive cards](../../task-modules-and-cards/cards/cards-reference.md#adaptive-card) via an incoming webhook is as follows:</span></span>

<span data-ttu-id="79761-163">**1.** [Configurer un webhook personnalisé](#setting-up-a-custom-incoming-webhook) dans Teams.</span><span class="sxs-lookup"><span data-stu-id="79761-163">**1.** [Setup a custom webhook](#setting-up-a-custom-incoming-webhook) in Teams.</span></span></br></br>
<span data-ttu-id="79761-164">**2.** Créez votre fichier JSON de carte adaptative :</span><span class="sxs-lookup"><span data-stu-id="79761-164">**2.** Create your adaptive card JSON file:</span></span>

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
                "text": "For Samples and Templates, see [https://adaptivecards.io/samples](https://adaptivecards.io/samples)",
                }
            ]
         }
      }
   ]
}
```

> [!div class="checklist"]
>
> - <span data-ttu-id="79761-165">Le `"type"` champ doit être`"message"`.</span><span class="sxs-lookup"><span data-stu-id="79761-165">The `"type"` field must be `"message"`.</span></span>
> - <span data-ttu-id="79761-166">Le`"attachments"` tableau contient un ensemble d'objets carte.</span><span class="sxs-lookup"><span data-stu-id="79761-166">The `"attachments"` array contains a set of card objects.</span></span>
> - <span data-ttu-id="79761-167">Le`"contentType"` champ doit être réglé sur le type de carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="79761-167">The `"contentType"` field must be set to adaptive card type.</span></span>
> - <span data-ttu-id="79761-168">L’`"content"` objet est la carte formatée en JSON.</span><span class="sxs-lookup"><span data-stu-id="79761-168">The `"content"` object is the card formatted in JSON.</span></span>

<span data-ttu-id="79761-169">**3.** Testez votre carte adaptative avec le facteur</span><span class="sxs-lookup"><span data-stu-id="79761-169">**3.** Test your adaptive card with Postman</span></span>

<span data-ttu-id="79761-170">Vous pouvez tester votre carte adaptative en utilisant [le facteur](https://www.postman.com) pour envoyer une demande POST à l'URL que vous avez créée lors de la configuration de votre webhook entrant.</span><span class="sxs-lookup"><span data-stu-id="79761-170">You can test your adaptive card using [Postman](https://www.postman.com) to send a POST request to the URL that you created when you setup your incoming webhook.</span></span> <span data-ttu-id="79761-171">Collez votre fichier JSON dans le corps de la demande et visualisez le message de votre carte adaptative dans Teams.</span><span class="sxs-lookup"><span data-stu-id="79761-171">Paste your JSON file in the body of the request and view your adaptive card message in Teams.</span></span>

>[!TIP]
> <span data-ttu-id="79761-172">Vous pouvez utiliser des échantillons et des modèles de codes [de carte adaptative](https://adaptivecards.io/samples) pour le corps de votre demande de test Post.</span><span class="sxs-lookup"><span data-stu-id="79761-172">You can use adaptive card code [Samples and Templates](https://adaptivecards.io/samples) for the body of your test Post request.</span></span>

## <a name="testing-your-connector"></a><span data-ttu-id="79761-173">Test du connecteur</span><span class="sxs-lookup"><span data-stu-id="79761-173">Testing your connector</span></span>

<span data-ttu-id="79761-174">Pour tester le connecteur, téléchargez-le dans une équipe comme vous le feriez avec une autre application.</span><span class="sxs-lookup"><span data-stu-id="79761-174">To test your Connector, upload it to a team as you would with any other app.</span></span> <span data-ttu-id="79761-175">Vous pouvez créer un package .zip à l’aide du fichier manifeste à partir du tableau de bord du développeur de connecteurs (modifié comme indiqué dans la section précédente) et des deux fichiers d’icône.</span><span class="sxs-lookup"><span data-stu-id="79761-175">You can create a .zip package using the manifest file from the Connectors Developer Dashboard (modified as directed in the preceding section) and the two icon files.</span></span>

<span data-ttu-id="79761-176">Une fois que vous avez téléchargé l’application, ouvrez la liste des connecteurs à partir de n’importe quel canal.</span><span class="sxs-lookup"><span data-stu-id="79761-176">After you upload the app, open the Connectors list from any channel.</span></span> <span data-ttu-id="79761-177">Faites défiler la page vers le bas pour afficher votre application dans la section **Téléchargé**.</span><span class="sxs-lookup"><span data-stu-id="79761-177">Scroll to the bottom to see your app in the **Uploaded** section.</span></span>

![Capture d’écran de la section téléchargée dans la boîte de dialogue connecteur](~/assets/images/connectors/connector_dialog_uploaded.png)

<span data-ttu-id="79761-179">Vous pouvez à présent lancer l’expérience de configuration.</span><span class="sxs-lookup"><span data-stu-id="79761-179">You can now launch the configuration experience.</span></span> <span data-ttu-id="79761-180">N’oubliez pas que ce flux se produit entièrement au sein de Microsoft Teams via une fenêtre indépendante.</span><span class="sxs-lookup"><span data-stu-id="79761-180">Be aware that this flow occurs entirely within Microsoft Teams through a pop-up window.</span></span> <span data-ttu-id="79761-181">Pour l’instant, ce comportement diffère de l’expérience de configuration dans les connecteurs que vous avez créés. Nous travaillons à l’unification de l’expérience.</span><span class="sxs-lookup"><span data-stu-id="79761-181">Currently, this behavior differs from the configuration experience in Connectors that we created; we are working on unifying the experiences.</span></span>

<span data-ttu-id="79761-182">Pour vérifier qu’une action `HttpPOST` fonctionne correctement, utilisez votre [webhook entrant personnalisé](#setting-up-a-custom-incoming-webhook).</span><span class="sxs-lookup"><span data-stu-id="79761-182">To verify that an `HttpPOST` action is working correctly, use your [custom incoming webhook](#setting-up-a-custom-incoming-webhook).</span></span>

## <a name="rate-limiting-for-connectors"></a><span data-ttu-id="79761-183">Limitation du taux pour les connecteurs</span><span class="sxs-lookup"><span data-stu-id="79761-183">Rate limiting for connectors</span></span>

<span data-ttu-id="79761-184">Les limites de débit d'application contrôlent le trafic qu'un connecteur ou un webhook entrant est autorisé à générer sur un canal.</span><span class="sxs-lookup"><span data-stu-id="79761-184">Application rate limits control the traffic that a connector or an incoming webhook is allowed to generate on a channel.</span></span> <span data-ttu-id="79761-185">Les équipes effectuent le suivi des demandes via une fenêtre à débit fixe et un compteur incrémentiel mesuré en secondes.</span><span class="sxs-lookup"><span data-stu-id="79761-185">Teams tracks requests via a fixed-rate window and incremental counter measured in seconds.</span></span>  <span data-ttu-id="79761-186">Si le nombre de demandes est trop élevé, la connexion client sera limitée jusqu’à l’actualisation de la fenêtre, c’est-à-dire, pour la durée du débit fixe.</span><span class="sxs-lookup"><span data-stu-id="79761-186">If too many requests are made, the client connection will be throttled until the window refreshes, i.e., for the duration of the fixed rate.</span></span>

### <a name="transactions-per-second-thresholds"></a><span data-ttu-id="79761-187">**Seuils de transaction par seconde**</span><span class="sxs-lookup"><span data-stu-id="79761-187">**Transactions per second thresholds**</span></span>

| <span data-ttu-id="79761-188">Durée (secondes)</span><span class="sxs-lookup"><span data-stu-id="79761-188">Time (seconds)</span></span>  | <span data-ttu-id="79761-189">Nombre maximal de demandes autorisées</span><span class="sxs-lookup"><span data-stu-id="79761-189">Maximum allowed requests</span></span>  |
|---|---|
| <span data-ttu-id="79761-190">1</span><span class="sxs-lookup"><span data-stu-id="79761-190">1</span></span>   | <span data-ttu-id="79761-191">4</span><span class="sxs-lookup"><span data-stu-id="79761-191">4</span></span>  |  
| <span data-ttu-id="79761-192">30</span><span class="sxs-lookup"><span data-stu-id="79761-192">30</span></span>   | <span data-ttu-id="79761-193">60</span><span class="sxs-lookup"><span data-stu-id="79761-193">60</span></span>  |  
| <span data-ttu-id="79761-194">3600</span><span class="sxs-lookup"><span data-stu-id="79761-194">3600</span></span>   | <span data-ttu-id="79761-195">100</span><span class="sxs-lookup"><span data-stu-id="79761-195">100</span></span>  |
| <span data-ttu-id="79761-196">7200</span><span class="sxs-lookup"><span data-stu-id="79761-196">7200</span></span> | <span data-ttu-id="79761-197">150</span><span class="sxs-lookup"><span data-stu-id="79761-197">150</span></span>  |
| <span data-ttu-id="79761-198">86400</span><span class="sxs-lookup"><span data-stu-id="79761-198">86400</span></span>  | <span data-ttu-id="79761-199">1800</span><span class="sxs-lookup"><span data-stu-id="79761-199">1800</span></span>  |

<span data-ttu-id="79761-200">*Voir aussi* [Connecteurs Office 365 — Microsoft Teams](https://docs.microsoft.com/connectors/teams/)</span><span class="sxs-lookup"><span data-stu-id="79761-200">*See also* [Office 365 Connectors — Microsoft Teams](https://docs.microsoft.com/connectors/teams/)</span></span>

<span data-ttu-id="79761-201">Une [logique des nouvelles tentatives avec une sauvegarde exponentielle](/azure/architecture/patterns/retry) comme ci-dessous permet de limiter les débits pour les cas où les demandes dépassent les limites en une seconde.</span><span class="sxs-lookup"><span data-stu-id="79761-201">A [retry logic with exponential back-off](/azure/architecture/patterns/retry) like below would mitigate rate limiting for cases where requests are exceeding the limits within a second.</span></span> <span data-ttu-id="79761-202">Veuillez suivre les [meilleures pratiques](../../bots/how-to/rate-limit.md#best-practices) pour éviter d’atteindre les limites de débit.</span><span class="sxs-lookup"><span data-stu-id="79761-202">Please follow [best practices](../../bots/how-to/rate-limit.md#best-practices) to avoid hitting the rate limits.</span></span>

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
 
<span data-ttu-id="79761-203">Ces limites sont en place pour réduire le courrier indésirable d’un canal par un connecteur et de garantir une expérience optimale pour vos utilisateurs finaux.</span><span class="sxs-lookup"><span data-stu-id="79761-203">These limits are in place to reduce spamming a channel by a connector and ensures an optimal experience to your end users.</span></span>
