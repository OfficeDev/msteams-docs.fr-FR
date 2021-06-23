---
title: Ajouter des bots personnalisés à Microsoft Teams avec des webhooks sortants
description: explique comment ajouter un webhook sortant
ms.topic: conceptual
ms.author: lajanuar
localization_priority: Normal
keywords: 'onglets teams : message actionnable de webhook sortant vérifiant le webhook'
ms.openlocfilehash: 2fac6f42e27a4c8cb3d079ea281d458a4dfe41ed
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069181"
---
# <a name="add-custom-bots-to-teams-with-outgoing-webhooks"></a><span data-ttu-id="4fa98-104">Ajouter des bots personnalisés à Teams avec des webhooks sortants</span><span class="sxs-lookup"><span data-stu-id="4fa98-104">Add custom bots to Teams with outgoing webhooks</span></span>

## <a name="outgoing-webhooks-in-teams"></a><span data-ttu-id="4fa98-105">Webhooks sortants dans Teams</span><span class="sxs-lookup"><span data-stu-id="4fa98-105">Outgoing webhooks in Teams</span></span>

<span data-ttu-id="4fa98-106">Les webhooks sont un moyen Teams pour s’intégrer à des applications externes.</span><span class="sxs-lookup"><span data-stu-id="4fa98-106">Webhooks are an eminent way for Teams to integrate with external apps.</span></span> <span data-ttu-id="4fa98-107">Un webhook est essentiellement une demande POST envoyée à une URL de rappel.</span><span class="sxs-lookup"><span data-stu-id="4fa98-107">A webhook is essentially a POST request sent to a callback URL.</span></span> <span data-ttu-id="4fa98-108">Les webhooks sortants permettent aux utilisateurs d’envoyer des messages à votre service web sans passer par le processus complet de création de bots via le [Microsoft Bot Framework](https://dev.botframework.com/).</span><span class="sxs-lookup"><span data-stu-id="4fa98-108">Outgoing webhooks allow users to send messages to your web service without going through the full process of creating bots via the [Microsoft Bot Framework](https://dev.botframework.com/).</span></span>

<span data-ttu-id="4fa98-109">Le webhook sortant envoie des données de Teams service choisi capable d’accepter une charge utile JSON.</span><span class="sxs-lookup"><span data-stu-id="4fa98-109">Outgoing webhook sends data from Teams to any chosen service capable of accepting a JSON payload.</span></span> <span data-ttu-id="4fa98-110">Après avoir ajouté les webhooks sortants à une équipe, il agit comme un bot et recherche des messages dans les canaux à l’aide de **\@ la mention**.</span><span class="sxs-lookup"><span data-stu-id="4fa98-110">After adding the outgoing webhooks to a team, it acts as a bot and looks for messages in channels using **\@mention**.</span></span> <span data-ttu-id="4fa98-111">Il envoie des notifications aux services web externes et répond par des messages enrichis, qui incluent des cartes et des images.</span><span class="sxs-lookup"><span data-stu-id="4fa98-111">It sends notifications to external web services and responds with rich messages, which include cards and images.</span></span>

## <a name="outgoing-webhook-key-features"></a><span data-ttu-id="4fa98-112">Fonctionnalités de clé de webhook sortant</span><span class="sxs-lookup"><span data-stu-id="4fa98-112">Outgoing webhook key features</span></span>

| <span data-ttu-id="4fa98-113">Fonctionnalité</span><span class="sxs-lookup"><span data-stu-id="4fa98-113">Feature</span></span> | <span data-ttu-id="4fa98-114">Description</span><span class="sxs-lookup"><span data-stu-id="4fa98-114">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="4fa98-115">Configuration limitée</span><span class="sxs-lookup"><span data-stu-id="4fa98-115">Scoped configuration</span></span>| <span data-ttu-id="4fa98-116">Les webhooks sont limitées au niveau de l’équipe.</span><span class="sxs-lookup"><span data-stu-id="4fa98-116">Webhooks are scoped at the team level.</span></span> <span data-ttu-id="4fa98-117">Vous devez passer par le processus de configuration de chaque équipe dans laquelle vous souhaitez ajouter votre webhook sortant.</span><span class="sxs-lookup"><span data-stu-id="4fa98-117">You must go through the setup process for each team where you want to add your outgoing webhook.</span></span> |
| <span data-ttu-id="4fa98-118">Messagerie réactive</span><span class="sxs-lookup"><span data-stu-id="4fa98-118">Reactive messaging</span></span>| <span data-ttu-id="4fa98-119">Les utilisateurs doivent utiliser @mention pour que le webhook reçoit des messages.</span><span class="sxs-lookup"><span data-stu-id="4fa98-119">Users must use @mention for the webhook to receive messages.</span></span> <span data-ttu-id="4fa98-120">Actuellement, les utilisateurs peuvent uniquement envoyer des messages à un webhook sortant dans les canaux publics et non dans l’étendue personnelle ou privée.</span><span class="sxs-lookup"><span data-stu-id="4fa98-120">Currently, users can only message an outgoing webhook in public channels and not within the personal or private scope.</span></span> |
|<span data-ttu-id="4fa98-121">Échange de messages HTTP standard</span><span class="sxs-lookup"><span data-stu-id="4fa98-121">Standard HTTP message exchange</span></span>|<span data-ttu-id="4fa98-122">Les réponses apparaissent dans la même chaîne que le message de demande d’origine et peuvent inclure n’importe quel contenu de message d’infrastructure de bot, par exemple du texte enrichi, des images, des cartes et des emojis.</span><span class="sxs-lookup"><span data-stu-id="4fa98-122">Responses appear in the same chain as the original request message and can include any bot framework message content, for example, rich text, images, cards, and emojis.</span></span> <span data-ttu-id="4fa98-123">Bien que les webhooks sortants peuvent utiliser des cartes, ils ne peuvent pas utiliser d’actions de carte à l’exception de `openURL` .</span><span class="sxs-lookup"><span data-stu-id="4fa98-123">Although outgoing webhooks can use cards, they cannot use any card actions except for `openURL`.</span></span>|
| <span data-ttu-id="4fa98-124">Teams Prise en charge des méthodes d’API</span><span class="sxs-lookup"><span data-stu-id="4fa98-124">Teams API method support</span></span>|<span data-ttu-id="4fa98-125">Le webhook sortant envoie une demande HTTP POST à un service web et renvoie une réponse.</span><span class="sxs-lookup"><span data-stu-id="4fa98-125">Outgoing webhook sends an HTTP POST to a web service and process a response back.</span></span> <span data-ttu-id="4fa98-126">Ils ne peuvent pas accéder à d’autres API telles que la récupération de la liste de la liste ou de la liste des canaux d’une équipe.</span><span class="sxs-lookup"><span data-stu-id="4fa98-126">They cannot access any other APIs like retrieve the roster or list of channels in a team.</span></span>|

## <a name="creating-actionable-messages"></a><span data-ttu-id="4fa98-127">Créations des messages intégrant des actions</span><span class="sxs-lookup"><span data-stu-id="4fa98-127">Creating actionable messages</span></span>

<span data-ttu-id="4fa98-128">Les cartes de connecteur incluent trois boutons visibles sur la carte.</span><span class="sxs-lookup"><span data-stu-id="4fa98-128">The connector cards include three visible buttons on the card.</span></span> <span data-ttu-id="4fa98-129">Chaque bouton est défini dans la propriété du message à `potentialAction` l’aide `ActionCard` d’actions.</span><span class="sxs-lookup"><span data-stu-id="4fa98-129">Each button is defined in the `potentialAction` property of the message by using `ActionCard` actions.</span></span> <span data-ttu-id="4fa98-130">Chacune `ActionCard` contient un type d’entrée, un champ de texte, un s sélectionneur de dates ou une liste à choix multiples.</span><span class="sxs-lookup"><span data-stu-id="4fa98-130">Each `ActionCard` contains an input type; a text field, a date picker, or a multi-choice list.</span></span> <span data-ttu-id="4fa98-131">Chaque `ActionCard` action est associée à une action, par exemple. `HttpPOST`</span><span class="sxs-lookup"><span data-stu-id="4fa98-131">Each `ActionCard` action has an associated action, for example, `HttpPOST`.</span></span>

<span data-ttu-id="4fa98-132">Les cartes de connecteur prennent en charge trois types d’actions :</span><span class="sxs-lookup"><span data-stu-id="4fa98-132">Connector cards support three types of actions:</span></span>

| <span data-ttu-id="4fa98-133">Opération</span><span class="sxs-lookup"><span data-stu-id="4fa98-133">Action</span></span> | <span data-ttu-id="4fa98-134">Description</span><span class="sxs-lookup"><span data-stu-id="4fa98-134">Description</span></span> |
| ------- | ----------- |
| `ActionCard` |<span data-ttu-id="4fa98-135">Présente un ou plusieurs types d’entrée et actions associées.</span><span class="sxs-lookup"><span data-stu-id="4fa98-135">Presents one or more input types and associated actions.</span></span>|
| `HttpPOST` | <span data-ttu-id="4fa98-136">Envoie une demande POST à une URL.</span><span class="sxs-lookup"><span data-stu-id="4fa98-136">Sends a POST request to a URL.</span></span> |
| `OpenUri` |  <span data-ttu-id="4fa98-137">Ouvre un URI dans un navigateur ou une application distinct, cible éventuellement différentes URI en fonction des systèmes d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="4fa98-137">Opens a URI in a separate browser or app, optionally targets different URIs based on operating systems.</span></span>|

<span data-ttu-id="4fa98-138">L'action `ActionCard` prend en charge trois types d'entrée :</span><span class="sxs-lookup"><span data-stu-id="4fa98-138">The `ActionCard` action supports three input types:</span></span>

| <span data-ttu-id="4fa98-139">Type d’entrée</span><span class="sxs-lookup"><span data-stu-id="4fa98-139">Input type</span></span> | <span data-ttu-id="4fa98-140">Description</span><span class="sxs-lookup"><span data-stu-id="4fa98-140">Description</span></span> |
| ------- | ----------- |
| `TextInput` | <span data-ttu-id="4fa98-141">Champ de texte à ligne unique ou multiligne avec une limite de longueur facultative.</span><span class="sxs-lookup"><span data-stu-id="4fa98-141">A single-line or multiline text field with an optional length limit.</span></span> |
| `DateInput` | <span data-ttu-id="4fa98-142">Sélecteur de dates avec un sélecteur d’heure facultatif.</span><span class="sxs-lookup"><span data-stu-id="4fa98-142">A date selector with an optional time selector.</span></span> |
| `MultichoiceInput` | <span data-ttu-id="4fa98-143">Liste de choix spécifiée, offrant soit une sélection unique, soit plusieurs sélections.</span><span class="sxs-lookup"><span data-stu-id="4fa98-143">A specified list of choices, offering either a single selection or multiple selections.</span></span>|

<span data-ttu-id="4fa98-144">`MultichoiceInput` prend en `style` charge une propriété qui contrôle l’affichage d’une liste entièrement étendue.</span><span class="sxs-lookup"><span data-stu-id="4fa98-144">`MultichoiceInput` supports a `style` property that controls the display of a fully expanded list.</span></span> <span data-ttu-id="4fa98-145">La valeur par défaut `style` dépend de la `isMultiSelect` valeur.</span><span class="sxs-lookup"><span data-stu-id="4fa98-145">The default value of `style` depends on the `isMultiSelect` value.</span></span>

| <span data-ttu-id="4fa98-146">`isMultiSelect` value</span><span class="sxs-lookup"><span data-stu-id="4fa98-146">`isMultiSelect` value</span></span>  | <span data-ttu-id="4fa98-147">`style` valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="4fa98-147">`style` default value</span></span>  |
| --- | --- |
| <span data-ttu-id="4fa98-148">`false` ou non spécifié</span><span class="sxs-lookup"><span data-stu-id="4fa98-148">`false` or not specified</span></span> | <span data-ttu-id="4fa98-149">Le style par défaut est `compact`</span><span class="sxs-lookup"><span data-stu-id="4fa98-149">The default style is `compact`</span></span>|
| `true` | <span data-ttu-id="4fa98-150">Le style par défaut est `expanded`</span><span class="sxs-lookup"><span data-stu-id="4fa98-150">The default style is `expanded`</span></span> |

> [!NOTE]
> * <span data-ttu-id="4fa98-151">Entrez les `"isMultiSelect": true` deux et, si vous souhaitez que la liste à sélections multiples soit affichée `"style": true` dans un style compact.</span><span class="sxs-lookup"><span data-stu-id="4fa98-151">Enter both `"isMultiSelect": true` and `"style": true`, if you want the multi-select list to be displayed in a compact style.</span></span>
> * <span data-ttu-id="4fa98-152">La sélection de la propriété dans Teams est la même que la sélection de la propriété `compact` `style` dans Microsoft `normal` `style` Outlook.</span><span class="sxs-lookup"><span data-stu-id="4fa98-152">Selecting `compact` for the `style` property in Teams is the same as selecting `normal` for the `style` property in Microsoft Outlook.</span></span>
> * <span data-ttu-id="4fa98-153">Les webhooks ne peuvent Office 365 les cartes de retour de message et les cartes adaptatives.</span><span class="sxs-lookup"><span data-stu-id="4fa98-153">Webhooks support only Office 365 message back cards and adaptive cards.</span></span>

<span data-ttu-id="4fa98-154">Pour plus d’informations sur les actions de carte de connecteur, voir **[Actions](/outlook/actionable-messages/card-reference#actions)** dans la référence de carte de message actionnable.</span><span class="sxs-lookup"><span data-stu-id="4fa98-154">For all other details about connector card actions, see **[Actions](/outlook/actionable-messages/card-reference#actions)** in the actionable message card reference.</span></span>

## <a name="adding-outgoing-webhooks-to-your-app"></a><span data-ttu-id="4fa98-155">Ajout de webhooks sortants à votre application</span><span class="sxs-lookup"><span data-stu-id="4fa98-155">Adding outgoing webhooks to your app</span></span>

<span data-ttu-id="4fa98-156">**Scénario**: envoyer des notifications d’état de modification sur Teams de base de données de canal vers votre application.</span><span class="sxs-lookup"><span data-stu-id="4fa98-156">**Scenario**: Push change status notifications on a Teams channel database server to your app.</span></span>  
<span data-ttu-id="4fa98-157">**Exemple**: vous avez une application métier qui suit toutes les opérations CRUD réalisées sur les enregistrements des employés par Teams utilisateurs RH de canal au sein d’Office 365 clients.</span><span class="sxs-lookup"><span data-stu-id="4fa98-157">**Example**: You have a line-of-business app that tracks all CRUD operations made to employee records by Teams channel HR users across an Office 365 tenancy.</span></span>

### <a name="1-create-a-url-on-your-apps-server-to-accept-and-process-a-post-request-with-a-json-payload"></a><span data-ttu-id="4fa98-158">1. Créez une URL sur le serveur de votre application pour accepter et traiter une demande POST avec une charge utile JSON</span><span class="sxs-lookup"><span data-stu-id="4fa98-158">1. Create a URL on your app's server to accept and process a POST request with a JSON payload</span></span>

<span data-ttu-id="4fa98-159">Votre service reçoit des messages dans un schéma de messagerie de service de bot Azure standard.</span><span class="sxs-lookup"><span data-stu-id="4fa98-159">Your service receives messages in a standard Azure bot service messaging schema.</span></span> <span data-ttu-id="4fa98-160">Le connecteur d’infrastructure du bot est un service RESTful qui permet à votre service de traiter l’échange de messages au format JSON via des protocoles HTTPS, comme documenté dans [l’API Azure Bot Service.](/bot-framework/rest-api/bot-framework-rest-connector-api-reference)</span><span class="sxs-lookup"><span data-stu-id="4fa98-160">The bot framework connector is a RESTful service that empowers your service to process the interchange of JSON formatted messages via HTTPS protocols as documented in the [Azure Bot Service API](/bot-framework/rest-api/bot-framework-rest-connector-api-reference).</span></span> <span data-ttu-id="4fa98-161">Vous pouvez également suivre le [Microsoft Bot Framework SDK] pour traiter et passer des messages.</span><span class="sxs-lookup"><span data-stu-id="4fa98-161">Alternatively, you can follow the [Microsoft Bot Framework SDK] to process and parse messages.</span></span> <span data-ttu-id="4fa98-162">Voir aussi [à propos d’Azure Bot Service](/azure/bot-service/bot-service-overview-introduction).</span><span class="sxs-lookup"><span data-stu-id="4fa98-162">See also [About Azure Bot Service](/azure/bot-service/bot-service-overview-introduction).</span></span>


<span data-ttu-id="4fa98-163">Les webhooks sortants sont limitées au niveau et `team` sont visibles par tous les membres de l’équipe.</span><span class="sxs-lookup"><span data-stu-id="4fa98-163">Outgoing webhooks are scoped to the `team` level and are visible to all the team members.</span></span> <span data-ttu-id="4fa98-164">Tout comme un bot, les utilisateurs doivent **\@ mentionner** le nom du webhook sortant pour l’appeler dans le canal.</span><span class="sxs-lookup"><span data-stu-id="4fa98-164">Just like a bot, users need to **\@mention** the name of the outgoing webhook to invoke it in the channel.</span></span>

### <a name="2-create-a-method-to-verify-the-outgoing-webhook-hmac-token"></a><span data-ttu-id="4fa98-165">2. Créer une méthode pour vérifier le jeton HMAC du webhook sortant</span><span class="sxs-lookup"><span data-stu-id="4fa98-165">2. Create a method to verify the outgoing webhook HMAC token</span></span>

#### <a name="hmac-signature-for-testing-with-code-example"></a><span data-ttu-id="4fa98-166">Exemple de signature HMAC à tester avec du code</span><span class="sxs-lookup"><span data-stu-id="4fa98-166">HMAC signature for testing with code example</span></span>

<span data-ttu-id="4fa98-167">Utilisation de l’exemple de message entrant et d’ID : « contoso » de SigningKeyDictionary de {"contoso », « vqF0En+Z0ucuRTM/01o2GuhMH3hKKk/N2bOmlM31zaA= » }.</span><span class="sxs-lookup"><span data-stu-id="4fa98-167">Using example of inbound message and id: "contoso" of SigningKeyDictionary of {"contoso", "vqF0En+Z0ucuRTM/01o2GuhMH3hKKk/N2bOmlM31zaA=" }.</span></span>

<span data-ttu-id="4fa98-168">Utilisez la valeur « HMAC 03TCao0i55H1eVKUusZOTZRjtvYTs+mO41mPL+R1e1U= » dans l’autorisation de l’en-tête de demande.</span><span class="sxs-lookup"><span data-stu-id="4fa98-168">Use the value "HMAC 03TCao0i55H1eVKUusZOTZRjtvYTs+mO41mPL+R1e1U=" in the authorization of request header.</span></span>

<span data-ttu-id="4fa98-169">Pour vous assurer que votre service reçoit uniquement des appels provenant de clients Teams réels, Teams fournit un code HMAC dans l’en-tête `hmac` HTTP.</span><span class="sxs-lookup"><span data-stu-id="4fa98-169">To ensure that your service is receiving calls only from actual Teams clients, Teams provides an HMAC code in the HTTP `hmac` header.</span></span> <span data-ttu-id="4fa98-170">Toujours inclus le code dans votre protocole d’authentification.</span><span class="sxs-lookup"><span data-stu-id="4fa98-170">Always included the code in your authentication protocol.</span></span>

<span data-ttu-id="4fa98-171">Votre code doit toujours valider la signature HMAC incluse dans la demande :</span><span class="sxs-lookup"><span data-stu-id="4fa98-171">Your code must always validate the HMAC signature included in the request:</span></span>

* <span data-ttu-id="4fa98-172">Générer le jeton HMAC à partir du corps de la demande du message.</span><span class="sxs-lookup"><span data-stu-id="4fa98-172">Generate the HMAC token from the request body of the message.</span></span> <span data-ttu-id="4fa98-173">Il existe des bibliothèques standard pour le faire sur la plupart des plateformes (voir [Crypto](https://nodejs.org/api/crypto.html#crypto_crypto) for Node.js or see [Teams Webhook Sample](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) for C \# ).</span><span class="sxs-lookup"><span data-stu-id="4fa98-173">There are standard libraries to do this on most platforms (see [Crypto](https://nodejs.org/api/crypto.html#crypto_crypto) for Node.js or see [Teams Webhook Sample](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) for C\#).</span></span> <span data-ttu-id="4fa98-174">Microsoft Teams utilise le chiffrement HMAC SHA256 standard.</span><span class="sxs-lookup"><span data-stu-id="4fa98-174">Microsoft Teams uses standard SHA256 HMAC cryptography.</span></span> <span data-ttu-id="4fa98-175">Vous devez convertir le corps en tableau d’byte en UTF8.</span><span class="sxs-lookup"><span data-stu-id="4fa98-175">You need to convert the body to a byte array in UTF8.</span></span>
* <span data-ttu-id="4fa98-176">Calculez le hachage à partir du tableau d’byte du jeton de sécurité fourni par **Teams** lorsque vous avez inscrit le webhook sortant dans le client Teams].</span><span class="sxs-lookup"><span data-stu-id="4fa98-176">Compute the hash from the byte array of the security token **provided by Teams** when you registered the outgoing webhook in the Teams client].</span></span> <span data-ttu-id="4fa98-177">Voir [Créer un webhook sortant.](#create-an-outgoing-webhook)</span><span class="sxs-lookup"><span data-stu-id="4fa98-177">See [Create an outgoing webhook](#create-an-outgoing-webhook).</span></span>
* <span data-ttu-id="4fa98-178">Convertissez le hachage en chaîne à l’aide du codage UTF-8.</span><span class="sxs-lookup"><span data-stu-id="4fa98-178">Convert the hash to a string using UTF-8 encoding.</span></span>
* <span data-ttu-id="4fa98-179">Comparez la valeur de chaîne du hachage généré à la valeur fournie dans la requête HTTP.</span><span class="sxs-lookup"><span data-stu-id="4fa98-179">Compare the string value of the generated hash with the value provided in the HTTP request.</span></span>

### <a name="3-create-a-method-to-send-a-success-or-failure-response"></a><span data-ttu-id="4fa98-180">3. Créer une méthode pour envoyer une réponse de réussite ou d’échec</span><span class="sxs-lookup"><span data-stu-id="4fa98-180">3. Create a method to send a success or failure response</span></span>

<span data-ttu-id="4fa98-181">Les réponses de vos webhooks sortants apparaissent dans la même chaîne de réponse que le message d’origine.</span><span class="sxs-lookup"><span data-stu-id="4fa98-181">Responses from your outgoing webhooks appear in the same reply chain as the original message.</span></span> <span data-ttu-id="4fa98-182">Lorsque l’utilisateur effectue une requête, Microsoft Teams envoie une demande HTTP synchrone à votre service et votre code obtient cinq secondes pour répondre au message avant que la connexion n’arrive à terme et ne se termine.</span><span class="sxs-lookup"><span data-stu-id="4fa98-182">When the user performs a query, Microsoft Teams issues a synchronous HTTP request to your service and your code gets five seconds to respond to the message before the connection times out and terminates.</span></span>

### <a name="example-response"></a><span data-ttu-id="4fa98-183">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="4fa98-183">Example response</span></span>

```json
{
    "type": "message",
    "text": "This is a reply!"
}
```

> [!NOTE]
> * <span data-ttu-id="4fa98-184">Vous pouvez envoyer des messages de carte adaptative, de carte Hero et de texte en pièce jointe avec un webhook sortant.</span><span class="sxs-lookup"><span data-stu-id="4fa98-184">You can send Adaptive Card, Hero card, and text messages as attachment with outgoing webhook.</span></span>
> * <span data-ttu-id="4fa98-185">Les cartes sont en charge de la mise en forme.</span><span class="sxs-lookup"><span data-stu-id="4fa98-185">Cards support formatting.</span></span> <span data-ttu-id="4fa98-186">Pour plus d’informations, voir [les cartes de mise en forme avec markdown](~/task-modules-and-cards/cards/cards-format.md?tabs=adaptive-md%2Cconnector-html#formatting-cards-with-markdown).</span><span class="sxs-lookup"><span data-stu-id="4fa98-186">For more information, see [format cards with markdown](~/task-modules-and-cards/cards/cards-format.md?tabs=adaptive-md%2Cconnector-html#formatting-cards-with-markdown).</span></span>

<span data-ttu-id="4fa98-187">Les codes suivants sont des exemples de réponse de carte adaptative :</span><span class="sxs-lookup"><span data-stu-id="4fa98-187">Following codes are examples of an Adaptive Card response:</span></span>

# <a name="cnet"></a>[<span data-ttu-id="4fa98-188">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="4fa98-188">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="4fa98-189">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="4fa98-189">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="4fa98-190">JSON</span><span class="sxs-lookup"><span data-stu-id="4fa98-190">JSON</span></span>](#tab/json)

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

## <a name="create-an-outgoing-webhook"></a><span data-ttu-id="4fa98-191">Créer un webhook sortant</span><span class="sxs-lookup"><span data-stu-id="4fa98-191">Create an outgoing webhook</span></span>

1. <span data-ttu-id="4fa98-192">Sélectionnez l’équipe appropriée et choisissez **Gérer** l’équipe dans le menu déroulant (&#8226;&#8226;&#8226;).</span><span class="sxs-lookup"><span data-stu-id="4fa98-192">Select the appropriate team and choose **Manage team** from the (&#8226;&#8226;&#8226;) drop-down menu.</span></span>
1. <span data-ttu-id="4fa98-193">Choisissez **l’onglet Applications** dans la barre de navigation.</span><span class="sxs-lookup"><span data-stu-id="4fa98-193">Choose the **Apps** tab from the navigation bar.</span></span>
1. <span data-ttu-id="4fa98-194">Dans le coin inférieur droit de la fenêtre, **sélectionnez Créer un webhook sortant.**</span><span class="sxs-lookup"><span data-stu-id="4fa98-194">From the window's lower right corner select **Create an outgoing webhook**.</span></span>
1. <span data-ttu-id="4fa98-195">Dans la fenêtre popup qui en résulte, remplissez les champs requis :</span><span class="sxs-lookup"><span data-stu-id="4fa98-195">In the resulting popup window complete the required fields:</span></span>

>* <span data-ttu-id="4fa98-196">**Nom**: titre du webhook et @mention’appuyer</span><span class="sxs-lookup"><span data-stu-id="4fa98-196">**Name**: The webhook title and @mention tap</span></span>
>* <span data-ttu-id="4fa98-197">**URL de rappel**: point de terminaison HTTPS qui accepte les charges utiles JSON et reçoit les demandes POST de Teams</span><span class="sxs-lookup"><span data-stu-id="4fa98-197">**Callback URL**: The HTTPS endpoint that accepts JSON payloads and receives POST requests from Teams</span></span>
>* <span data-ttu-id="4fa98-198">**Description**: chaîne détaillée qui apparaît dans la carte de visite et le tableau de bord de l’application au niveau de l’équipe</span><span class="sxs-lookup"><span data-stu-id="4fa98-198">**Description**: A detailed string that appear in the profile card and the team-level App dashboard</span></span>
>* <span data-ttu-id="4fa98-199">**Image de profil**: icône d’application facultative pour votre webhook</span><span class="sxs-lookup"><span data-stu-id="4fa98-199">**Profile Picture**: An optional app icon for your webhook</span></span>
>* <span data-ttu-id="4fa98-200">Sélectionnez **le bouton** Créer dans le coin inférieur droit de la fenêtre pop-up et le webhook sortant est ajouté aux canaux de l’équipe actuelle.</span><span class="sxs-lookup"><span data-stu-id="4fa98-200">Select the **Create** button from the lower right corner of the pop-up window and the outgoing webhook are added to the current team's channels.</span></span>
>* <span data-ttu-id="4fa98-201">La fenêtre de boîte de dialogue suivante affiche un jeton de sécurité [HMAC (Message Authentication Code)](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301) basé sur le hachage utilisé pour authentifier les appels entre Teams et le service externe désigné.</span><span class="sxs-lookup"><span data-stu-id="4fa98-201">The next dialog window displays an [Hash-based Message Authentication Code (HMAC)](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301) security token that is used to authenticate calls between Teams and the designated outside service.</span></span>
>* <span data-ttu-id="4fa98-202">Le webhook sortant est disponible pour les utilisateurs de l’équipe, uniquement si l’URL est valide et que les jetons d’authentification du serveur et du client sont égaux, par exemple, une négociation HMAC.</span><span class="sxs-lookup"><span data-stu-id="4fa98-202">The outgoing webhook is available to the team's users, only if the URL is valid and the server and client authentication tokens are equal for example, an HMAC handshake.</span></span>

## <a name="code-sample"></a><span data-ttu-id="4fa98-203">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="4fa98-203">Code sample</span></span>
|<span data-ttu-id="4fa98-204">**Exemple de nom**</span><span class="sxs-lookup"><span data-stu-id="4fa98-204">**Sample name**</span></span> | <span data-ttu-id="4fa98-205">**Description**</span><span class="sxs-lookup"><span data-stu-id="4fa98-205">**Description**</span></span> | <span data-ttu-id="4fa98-206">**.NET**</span><span class="sxs-lookup"><span data-stu-id="4fa98-206">**.NET**</span></span> | <span data-ttu-id="4fa98-207">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="4fa98-207">**Node.js**</span></span> |
|----------------|------------------|--------|----------------|
| <span data-ttu-id="4fa98-208">Webhooks sortants</span><span class="sxs-lookup"><span data-stu-id="4fa98-208">Outgoing webhooks</span></span> | <span data-ttu-id="4fa98-209">Exemples de création **de bots personnalisés** à utiliser dans Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="4fa98-209">Samples to create **Custom Bots** to be used in Microsoft Teams.</span></span>| [<span data-ttu-id="4fa98-210">View</span><span class="sxs-lookup"><span data-stu-id="4fa98-210">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/csharp) | [<span data-ttu-id="4fa98-211">View</span><span class="sxs-lookup"><span data-stu-id="4fa98-211">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/nodejs)|

