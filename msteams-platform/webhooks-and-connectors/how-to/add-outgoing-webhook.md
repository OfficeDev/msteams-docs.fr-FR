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
# <a name="create-outgoing-webhook"></a><span data-ttu-id="0f4c6-104">Créer un webhook sortant</span><span class="sxs-lookup"><span data-stu-id="0f4c6-104">Create Outgoing Webhook</span></span>

<span data-ttu-id="0f4c6-105">Le webhook sortant agit comme un bot et recherche des messages dans les canaux à **l’aide de @mention**.</span><span class="sxs-lookup"><span data-stu-id="0f4c6-105">The Outgoing Webhook acts as a bot and search for messages in channels using **@mention**.</span></span> <span data-ttu-id="0f4c6-106">Il envoie des notifications aux services web externes et répond par des messages enrichis, qui incluent des cartes et des images.</span><span class="sxs-lookup"><span data-stu-id="0f4c6-106">It sends notifications to external web services and responds with rich messages, which include cards and images.</span></span> <span data-ttu-id="0f4c6-107">Cela permet d’ignorer le processus de création de bots via [le Microsoft Bot Framework](https://dev.botframework.com/).</span><span class="sxs-lookup"><span data-stu-id="0f4c6-107">It helps to skip the process of creating bots through the [Microsoft Bot Framework](https://dev.botframework.com/).</span></span>

## <a name="key-features-of-outgoing-webhook"></a><span data-ttu-id="0f4c6-108">Fonctionnalités clés du webhook sortant</span><span class="sxs-lookup"><span data-stu-id="0f4c6-108">Key features of Outgoing Webhook</span></span>

<span data-ttu-id="0f4c6-109">Le tableau suivant fournit les fonctionnalités et la description des webhooks sortants :</span><span class="sxs-lookup"><span data-stu-id="0f4c6-109">The following table provides the features and description of Outgoing Webhooks:</span></span>

| <span data-ttu-id="0f4c6-110">Fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="0f4c6-110">Features</span></span> | <span data-ttu-id="0f4c6-111">Description</span><span class="sxs-lookup"><span data-stu-id="0f4c6-111">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="0f4c6-112">Configuration limitée</span><span class="sxs-lookup"><span data-stu-id="0f4c6-112">Scoped configuration</span></span>| <span data-ttu-id="0f4c6-113">Les webhooks sont limitées au niveau de l’équipe.</span><span class="sxs-lookup"><span data-stu-id="0f4c6-113">Webhooks are scoped at the team level.</span></span> <span data-ttu-id="0f4c6-114">Le processus de mise en place obligatoire pour chaque application ajoute un webhook sortant.</span><span class="sxs-lookup"><span data-stu-id="0f4c6-114">Mandatory set up process for each adds an Outgoing Webhook.</span></span> |
| <span data-ttu-id="0f4c6-115">Messagerie réactive</span><span class="sxs-lookup"><span data-stu-id="0f4c6-115">Reactive messaging</span></span>| <span data-ttu-id="0f4c6-116">Les utilisateurs doivent utiliser @mention pour que le webhook reçoit des messages.</span><span class="sxs-lookup"><span data-stu-id="0f4c6-116">Users must use @mention for the webhook to receive messages.</span></span> <span data-ttu-id="0f4c6-117">Actuellement, les utilisateurs peuvent uniquement envoyer un webhook sortant dans les canaux publics et non dans l’étendue personnelle ou privée.</span><span class="sxs-lookup"><span data-stu-id="0f4c6-117">Currently, users can only message an Outgoing Webhook in public channels and not within the personal or private scope.</span></span> |
|<span data-ttu-id="0f4c6-118">Échange de messages HTTP standard</span><span class="sxs-lookup"><span data-stu-id="0f4c6-118">Standard HTTP message exchange</span></span>|<span data-ttu-id="0f4c6-119">Les réponses apparaissent dans la même chaîne que le message de demande d’origine et peuvent inclure n’importe quel contenu de message Bot Framework, par exemple du texte enrichi, des images, des cartes et des emojis.</span><span class="sxs-lookup"><span data-stu-id="0f4c6-119">Responses appear in the same chain as the original request message and can include any Bot Framework message content, for example, rich text, images, cards, and emojis.</span></span> <span data-ttu-id="0f4c6-120">Bien que les webhooks sortants peuvent utiliser des cartes, ils ne peuvent pas utiliser d’actions de carte à l’exception de `openURL` .</span><span class="sxs-lookup"><span data-stu-id="0f4c6-120">Although Outgoing Webhooks can use cards, they cannot use any card actions except for `openURL`.</span></span>|
| <span data-ttu-id="0f4c6-121">Teams Prise en charge des méthodes d’API</span><span class="sxs-lookup"><span data-stu-id="0f4c6-121">Teams API method support</span></span>|<span data-ttu-id="0f4c6-122">Les webhooks sortants envoient une demande HTTP POST à un service web et renvoient une réponse.</span><span class="sxs-lookup"><span data-stu-id="0f4c6-122">Outgoing Webhooks sends an HTTP POST to a web service and gets a response.</span></span> <span data-ttu-id="0f4c6-123">Ils ne peuvent pas accéder à d’autres API, telles que la récupération de la liste de la liste ou de la liste des canaux d’une équipe.</span><span class="sxs-lookup"><span data-stu-id="0f4c6-123">They cannot access any other APIs, such as retrieve the roster or list of channels in a team.</span></span>|

## <a name="create-outgoing-webhooks"></a><span data-ttu-id="0f4c6-124">Créer des webhooks sortants</span><span class="sxs-lookup"><span data-stu-id="0f4c6-124">Create Outgoing Webhooks</span></span>

<span data-ttu-id="0f4c6-125">Créez des webhooks sortants et ajoutez des bots personnalisés à Teams.</span><span class="sxs-lookup"><span data-stu-id="0f4c6-125">Create Outgoing Webhooks and add custom bots to Teams.</span></span>

<span data-ttu-id="0f4c6-126">**Pour créer un webhook sortant**</span><span class="sxs-lookup"><span data-stu-id="0f4c6-126">**To create an Outgoing Webhook**</span></span>

1. <span data-ttu-id="0f4c6-127">Sélectionnez **Teams** dans le volet gauche.</span><span class="sxs-lookup"><span data-stu-id="0f4c6-127">Select **Teams** from the left pane.</span></span> <span data-ttu-id="0f4c6-128">La **page Teams’affiche** :</span><span class="sxs-lookup"><span data-stu-id="0f4c6-128">The **Teams** page appears:</span></span>

    ![Canal Teams](~/assets/images/teamschannel.png)

1. <span data-ttu-id="0f4c6-130">Dans la page **Teams,** sélectionnez l’équipe requise pour créer un webhook sortant et sélectionnez le &#8226;&#8226;&#8226;.</span><span class="sxs-lookup"><span data-stu-id="0f4c6-130">In the **Teams** page, select the required team to create an Outgoing Webhook and select the &#8226;&#8226;&#8226;.</span></span> <span data-ttu-id="0f4c6-131">Dans le menu déroulant, sélectionnez **Gérer l’équipe**:</span><span class="sxs-lookup"><span data-stu-id="0f4c6-131">In the dropdown menu, select **Manage team**:</span></span>

    ![Créer un webhook sortant](~/assets/images/outgoingwebhook1.png)

1. <span data-ttu-id="0f4c6-133">Sélectionnez **l’onglet** Applications sur la page de canal :</span><span class="sxs-lookup"><span data-stu-id="0f4c6-133">Select the **Apps** tab on the channel page:</span></span>

    ![Créer un webhook sortant](~/assets/images/outgoingwebhook2.png)

1. <span data-ttu-id="0f4c6-135">Sélectionnez **Créer un webhook sortant**:</span><span class="sxs-lookup"><span data-stu-id="0f4c6-135">Select **Create an Outgoing Webhook**:</span></span>

    ![Créer des webhooks sortants](~/assets/images/outgoingwebhook3.png)

1. <span data-ttu-id="0f4c6-137">Tapez les détails suivants dans la page **Créer un webhook sortant** :</span><span class="sxs-lookup"><span data-stu-id="0f4c6-137">Type the following details in the **Create an Outgoing Webhook** page:</span></span>

    * <span data-ttu-id="0f4c6-138">**Nom**: titre du webhook et onglet @mention webhook.</span><span class="sxs-lookup"><span data-stu-id="0f4c6-138">**Name**: The webhook title and @mention tab.</span></span>
    * <span data-ttu-id="0f4c6-139">**URL de rappel**: point de terminaison HTTPS qui accepte les charges utiles JSON et reçoit les demandes POST de Teams.</span><span class="sxs-lookup"><span data-stu-id="0f4c6-139">**Callback URL**: The HTTPS endpoint that accepts JSON payloads and receives POST requests from Teams.</span></span>
    * <span data-ttu-id="0f4c6-140">**Description**: chaîne détaillée qui apparaît dans la carte de visite et le tableau de bord de l’application au niveau de l’équipe.</span><span class="sxs-lookup"><span data-stu-id="0f4c6-140">**Description**: A detailed string that appears in the profile card and the team-level App dashboard.</span></span>
    * <span data-ttu-id="0f4c6-141">**Image de** profil : icône d’application pour votre webhook, qui est facultative.</span><span class="sxs-lookup"><span data-stu-id="0f4c6-141">**Profile Picture**: An app icon for your webhook, which is optional.</span></span>

1. <span data-ttu-id="0f4c6-142">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="0f4c6-142">Select **Create**.</span></span> <span data-ttu-id="0f4c6-143">Le webhook sortant est ajouté au canal de l’équipe actuelle :</span><span class="sxs-lookup"><span data-stu-id="0f4c6-143">The Outgoing Webhook is added to the current team's channel:</span></span>

    ![créer un webhook sortant](~/assets/images/outgoingwebhook.png)

<span data-ttu-id="0f4c6-145">Une boîte de dialogue [HMAC (Message Authentication Code)](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301) basée sur le hachage s’affiche.</span><span class="sxs-lookup"><span data-stu-id="0f4c6-145">A [Hash-based Message Authentication Code (HMAC)](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301) dialogue box appears.</span></span> <span data-ttu-id="0f4c6-146">Il s’agit d’un jeton de sécurité utilisé pour authentifier les appels entre Teams et le service extérieur désigné.</span><span class="sxs-lookup"><span data-stu-id="0f4c6-146">It is a security token used to authenticate calls between Teams and the designated outside service.</span></span>

>[!NOTE]
> <span data-ttu-id="0f4c6-147">Le webhook sortant est disponible pour les utilisateurs de l’équipe, uniquement si l’URL est valide et que les jetons d’authentification du serveur et du client sont égaux.</span><span class="sxs-lookup"><span data-stu-id="0f4c6-147">The Outgoing Webhook is available to the team's users, only if the URL is valid and the server and client authentication tokens are equal.</span></span> <span data-ttu-id="0f4c6-148">Par exemple, une poignée de main HMAC.</span><span class="sxs-lookup"><span data-stu-id="0f4c6-148">For example, an HMAC handshake.</span></span>

<span data-ttu-id="0f4c6-149">Le scénario suivant fournit les détails pour ajouter un webhook sortant :</span><span class="sxs-lookup"><span data-stu-id="0f4c6-149">The following scenario provides the details to add an Outgoing Webhook:</span></span>

* <span data-ttu-id="0f4c6-150">Scénario : envoyer des notifications d’état de modification sur Teams serveur de base de données de canal vers votre application.</span><span class="sxs-lookup"><span data-stu-id="0f4c6-150">Scenario: Push change status notifications on a Teams channel database server to your app.</span></span>
* <span data-ttu-id="0f4c6-151">Exemple : vous avez une application métier qui suit toutes les opérations CRUD, telles que créer, lire, mettre à jour et supprimer.</span><span class="sxs-lookup"><span data-stu-id="0f4c6-151">Example: You have a line of business app that tracks all CRUD operations, such as create, read, update, and delete.</span></span> <span data-ttu-id="0f4c6-152">Ces opérations sont réalisées sur les enregistrements des employés par Teams utilisateurs RH de canal au sein d’Office 365 location.</span><span class="sxs-lookup"><span data-stu-id="0f4c6-152">These operations are made to the employee records by Teams channel HR users across an Office 365 tenancy.</span></span>

# <a name="url-json-payload"></a>[<span data-ttu-id="0f4c6-153">Charge utile JSON d’URL</span><span class="sxs-lookup"><span data-stu-id="0f4c6-153">URL JSON payload</span></span>](#tab/urljsonpayload)
<span data-ttu-id="0f4c6-154">**Créer une URL sur le serveur de votre application pour accepter et traiter une demande POST avec une charge utile JSON**</span><span class="sxs-lookup"><span data-stu-id="0f4c6-154">**Create a URL on your app's server to accept and process a POST request with a JSON payload**</span></span>

<span data-ttu-id="0f4c6-155">Votre service reçoit des messages dans un schéma de messagerie de service de bot Azure standard.</span><span class="sxs-lookup"><span data-stu-id="0f4c6-155">Your service receives messages in a standard Azure bot service messaging schema.</span></span> <span data-ttu-id="0f4c6-156">Le connecteur Bot Framework est un service RESTful qui permet de traiter l’échange de messages au format JSON via des protocoles HTTPS, comme documenté dans [l’API Azure Bot Service.](/bot-framework/rest-api/bot-framework-rest-connector-api-reference)</span><span class="sxs-lookup"><span data-stu-id="0f4c6-156">The Bot Framework connector is a RESTful service that empowers to process the interchange of JSON formatted messages through HTTPS protocols as documented in the [Azure Bot Service API](/bot-framework/rest-api/bot-framework-rest-connector-api-reference).</span></span> <span data-ttu-id="0f4c6-157">Vous pouvez également suivre le SDK Microsoft Bot Framework pour traiter et parer les messages.</span><span class="sxs-lookup"><span data-stu-id="0f4c6-157">Alternatively, you can follow the Microsoft Bot Framework SDK to process and parse messages.</span></span> <span data-ttu-id="0f4c6-158">Pour plus d’informations, voir [vue d’ensemble d’Azure Bot Service.](/azure/bot-service/bot-service-overview-introduction)</span><span class="sxs-lookup"><span data-stu-id="0f4c6-158">For more information, see [overview of Azure Bot Service](/azure/bot-service/bot-service-overview-introduction).</span></span>

<span data-ttu-id="0f4c6-159">Les webhooks sortants sont limitées au niveau et `team` sont visibles par tous les membres de l’équipe.</span><span class="sxs-lookup"><span data-stu-id="0f4c6-159">Outgoing Webhooks are scoped to the `team` level and are visible to all the team members.</span></span> <span data-ttu-id="0f4c6-160">Les utilisateurs **\@ doivent mentionner** le nom du webhook sortant pour l’appeler dans le canal.</span><span class="sxs-lookup"><span data-stu-id="0f4c6-160">Users need to **\@mention** the name of the Outgoing Webhook to invoke it in the channel.</span></span>

# <a name="verify-hmac-token"></a>[<span data-ttu-id="0f4c6-161">Vérifier le jeton HMAC</span><span class="sxs-lookup"><span data-stu-id="0f4c6-161">Verify HMAC token</span></span>](#tab/verifyhmactoken)
<span data-ttu-id="0f4c6-162">**Créer une méthode pour vérifier le jeton HMAC du webhook sortant**</span><span class="sxs-lookup"><span data-stu-id="0f4c6-162">**Create a method to verify the Outgoing Webhook HMAC token**</span></span>

<span data-ttu-id="0f4c6-163">Utilisation d’un exemple de message entrant et d’ID : « contoso » de SigningKeyDictionary de {"contoso », « vqF0En+Z0ucuRTM/01o2GuhMH3hKKk/N2bOmlM31zaA= » }.</span><span class="sxs-lookup"><span data-stu-id="0f4c6-163">Using example of inbound message and ID: "contoso" of SigningKeyDictionary of {"contoso", "vqF0En+Z0ucuRTM/01o2GuhMH3hKKk/N2bOmlM31zaA=" }.</span></span>

<span data-ttu-id="0f4c6-164">Utilisez la valeur « HMAC 03TCao0i55H1eVKUusZOTZRjtvYTs+mO41mPL+R1e1U= » dans l’autorisation de l’en-tête de demande.</span><span class="sxs-lookup"><span data-stu-id="0f4c6-164">Use the value "HMAC 03TCao0i55H1eVKUusZOTZRjtvYTs+mO41mPL+R1e1U=" in the authorization of request header.</span></span>

<span data-ttu-id="0f4c6-165">Pour vous assurer que votre service ne reçoit des appels que de clients Teams réels, Teams fournit un code HMAC dans l’en-tête d’autorisation `hmac` HTTP.</span><span class="sxs-lookup"><span data-stu-id="0f4c6-165">To ensure that your service is receiving calls only from actual Teams clients, Teams provides an HMAC code in the HTTP `hmac` authorization header.</span></span> <span data-ttu-id="0f4c6-166">Incluez toujours le code dans votre protocole d’authentification.</span><span class="sxs-lookup"><span data-stu-id="0f4c6-166">Always include the code in your authentication protocol.</span></span>

<span data-ttu-id="0f4c6-167">Votre code doit toujours valider la signature HMAC incluse dans la demande comme suit :</span><span class="sxs-lookup"><span data-stu-id="0f4c6-167">Your code must always validate the HMAC signature included in the request as follows:</span></span>

* <span data-ttu-id="0f4c6-168">Générer le jeton HMAC à partir du corps de la demande du message.</span><span class="sxs-lookup"><span data-stu-id="0f4c6-168">Generate the HMAC token from the request body of the message.</span></span> <span data-ttu-id="0f4c6-169">Il existe des bibliothèques standard pour le faire sur la plupart des plateformes, telles que [Crypto](https://nodejs.org/api/crypto.html#crypto_crypto) for Node.js et [Teams webhook pour](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) C \# ).</span><span class="sxs-lookup"><span data-stu-id="0f4c6-169">There are standard libraries to do this on most platform, such as [Crypto](https://nodejs.org/api/crypto.html#crypto_crypto) for Node.js and [Teams webhook sample](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) for C\#).</span></span> <span data-ttu-id="0f4c6-170">Microsoft Teams utilise le chiffrement HMAC SHA256 standard.</span><span class="sxs-lookup"><span data-stu-id="0f4c6-170">Microsoft Teams uses standard SHA256 HMAC cryptography.</span></span> <span data-ttu-id="0f4c6-171">Vous devez convertir le corps en tableau d’entiers en UTF8.</span><span class="sxs-lookup"><span data-stu-id="0f4c6-171">You must convert the body to a byte array in UTF8.</span></span>
* <span data-ttu-id="0f4c6-172">Calculez le hachage à partir du tableau d’Teams du jeton de sécurité lorsque vous avez inscrit le webhook sortant dans le client Teams.</span><span class="sxs-lookup"><span data-stu-id="0f4c6-172">Compute the hash from the byte array of the security token provided by Teams when you registered the Outgoing Webhook in the Teams client.</span></span> <span data-ttu-id="0f4c6-173">Voir [créer un webhook sortant.](#create-outgoing-webhook)</span><span class="sxs-lookup"><span data-stu-id="0f4c6-173">See [create an Outgoing Webhook](#create-outgoing-webhook).</span></span>
* <span data-ttu-id="0f4c6-174">Convertissez le hachage en chaîne à l’aide du codage UTF-8.</span><span class="sxs-lookup"><span data-stu-id="0f4c6-174">Convert the hash to a string using UTF-8 encoding.</span></span>
* <span data-ttu-id="0f4c6-175">Comparez la valeur de chaîne du hachage généré à la valeur fournie dans la requête HTTP.</span><span class="sxs-lookup"><span data-stu-id="0f4c6-175">Compare the string value of the generated hash with the value provided in the HTTP request.</span></span>

# <a name="method-to-respond"></a>[<span data-ttu-id="0f4c6-176">Méthode de réponse</span><span class="sxs-lookup"><span data-stu-id="0f4c6-176">Method to respond</span></span>](#tab/methodtorespond)
<span data-ttu-id="0f4c6-177">**Créer une méthode pour envoyer une réponse de réussite ou d’échec**</span><span class="sxs-lookup"><span data-stu-id="0f4c6-177">**Create a method to send a success or failure response**</span></span>

<span data-ttu-id="0f4c6-178">Les réponses de vos webhooks sortants apparaissent dans la même chaîne de réponse que le message d’origine.</span><span class="sxs-lookup"><span data-stu-id="0f4c6-178">Responses from your Outgoing Webhooks appear in the same reply chain as the original message.</span></span> <span data-ttu-id="0f4c6-179">Lorsque l’utilisateur effectue une requête, Microsoft Teams envoie une demande HTTP synchrone à votre service et votre code obtient cinq secondes pour répondre au message avant que la connexion n’arrive à terme et ne se termine.</span><span class="sxs-lookup"><span data-stu-id="0f4c6-179">When the user performs a query, Microsoft Teams issues a synchronous HTTP request to your service and your code gets five seconds to respond to the message before the connection times out and terminates.</span></span>

### <a name="example-response"></a><span data-ttu-id="0f4c6-180">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="0f4c6-180">Example response</span></span>

```json
{
    "type": "message",
    "text": "This is a reply!"
}
```
---

> [!NOTE]
> * <span data-ttu-id="0f4c6-181">Vous pouvez envoyer des messages de carte adaptative, de carte Hero et de texte en pièce jointe avec le webhook sortant.</span><span class="sxs-lookup"><span data-stu-id="0f4c6-181">You can send Adaptive Card, Hero card, and text messages as attachment with Outgoing Webhook.</span></span>
> * <span data-ttu-id="0f4c6-182">Les cartes sont en charge de la mise en forme.</span><span class="sxs-lookup"><span data-stu-id="0f4c6-182">Cards support formatting.</span></span> <span data-ttu-id="0f4c6-183">Pour plus d’informations, voir [les cartes de mise en forme avec markdown](~/task-modules-and-cards/cards/cards-format.md?tabs=adaptive-md%2Cconnector-html#format-cards-with-markdown).</span><span class="sxs-lookup"><span data-stu-id="0f4c6-183">For more information, see [format cards with markdown](~/task-modules-and-cards/cards/cards-format.md?tabs=adaptive-md%2Cconnector-html#format-cards-with-markdown).</span></span>

<span data-ttu-id="0f4c6-184">Les codes suivants sont des exemples de réponse de carte adaptative :</span><span class="sxs-lookup"><span data-stu-id="0f4c6-184">Following codes are examples of an Adaptive Card response:</span></span>

# <a name="cnet"></a>[<span data-ttu-id="0f4c6-185">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="0f4c6-185">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="0f4c6-186">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="0f4c6-186">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="0f4c6-187">JSON</span><span class="sxs-lookup"><span data-stu-id="0f4c6-187">JSON</span></span>](#tab/json)

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

## <a name="code-sample"></a><span data-ttu-id="0f4c6-188">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="0f4c6-188">Code sample</span></span>

|<span data-ttu-id="0f4c6-189">**Exemple de nom**</span><span class="sxs-lookup"><span data-stu-id="0f4c6-189">**Sample name**</span></span> | <span data-ttu-id="0f4c6-190">**Description**</span><span class="sxs-lookup"><span data-stu-id="0f4c6-190">**Description**</span></span> | <span data-ttu-id="0f4c6-191">**.NET**</span><span class="sxs-lookup"><span data-stu-id="0f4c6-191">**.NET**</span></span> | <span data-ttu-id="0f4c6-192">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="0f4c6-192">**Node.js**</span></span> |
|----------------|------------------|--------|----------------|
| <span data-ttu-id="0f4c6-193">Webhooks sortants</span><span class="sxs-lookup"><span data-stu-id="0f4c6-193">Outgoing Webhooks</span></span> | <span data-ttu-id="0f4c6-194">Exemples de création de bots personnalisés à utiliser dans Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="0f4c6-194">Samples to create custom bots to be used in Microsoft Teams.</span></span>| [<span data-ttu-id="0f4c6-195">View</span><span class="sxs-lookup"><span data-stu-id="0f4c6-195">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/csharp) | [<span data-ttu-id="0f4c6-196">View</span><span class="sxs-lookup"><span data-stu-id="0f4c6-196">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/nodejs)|

## <a name="see-also"></a><span data-ttu-id="0f4c6-197">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="0f4c6-197">See also</span></span>
* [<span data-ttu-id="0f4c6-198">Créer un webhook entrant</span><span class="sxs-lookup"><span data-stu-id="0f4c6-198">Create an Incoming Webhook</span></span>](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [<span data-ttu-id="0f4c6-199">Créer un connecteur Office 365</span><span class="sxs-lookup"><span data-stu-id="0f4c6-199">Create an Office 365 Connector</span></span>](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [<span data-ttu-id="0f4c6-200">Créer et envoyer des messages</span><span class="sxs-lookup"><span data-stu-id="0f4c6-200">Create and send messages</span></span>](~/webhooks-and-connectors/how-to/connectors-using.md)
