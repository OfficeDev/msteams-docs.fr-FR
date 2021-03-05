---
title: Ajouter l’authentification à votre extension de messagerie
author: clearab
description: Comment ajouter l’authentification à une extension de messagerie
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: d673f52e63ba845675f6631470af68d65c7297ad
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449569"
---
# <a name="add-authentication-to-your-messaging-extension"></a><span data-ttu-id="5b8de-103">Ajouter l’authentification à votre extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="5b8de-103">Add authentication to your messaging extension</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

## <a name="identify-the-user"></a><span data-ttu-id="5b8de-104">Identifier l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="5b8de-104">Identify the user</span></span>

<span data-ttu-id="5b8de-105">Chaque demande à vos services inclut l’ID obscurci de l’utilisateur qui a effectué la demande, ainsi que le nom d’affichage de l’utilisateur et l’ID d’objet Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5b8de-105">Every request to your services includes the obfuscated ID of the user that performed the request, as well as the user's display name and Azure Active Directory object ID.</span></span>

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

<span data-ttu-id="5b8de-106">Les `id` `aadObjectId` valeurs et les valeurs sont garanties pour être celle de l’utilisateur Teams authentifié.</span><span class="sxs-lookup"><span data-stu-id="5b8de-106">The `id` and `aadObjectId` values are guaranteed to be that of the authenticated Teams user.</span></span> <span data-ttu-id="5b8de-107">Ils peuvent être utilisés comme clés pour rechercher des informations d’identification ou tout état mis en cache dans votre service.</span><span class="sxs-lookup"><span data-stu-id="5b8de-107">They can be used as keys to look up credentials or any cached state in your service.</span></span> <span data-ttu-id="5b8de-108">En outre, chaque demande contient l’ID de client Azure Active Directory de l’utilisateur, qui peut être utilisé pour identifier l’organisation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5b8de-108">In addition, each request contains the Azure Active Directory tenant ID of the user, which can be used to identify the user’s organization.</span></span> <span data-ttu-id="5b8de-109">Le cas échéant, la demande contient également les ID d’équipe et de canal d’où provient la demande.</span><span class="sxs-lookup"><span data-stu-id="5b8de-109">If applicable, the request also contains the team and channel IDs from which the request originated.</span></span>

## <a name="authentication"></a><span data-ttu-id="5b8de-110">Authentification</span><span class="sxs-lookup"><span data-stu-id="5b8de-110">Authentication</span></span>

<span data-ttu-id="5b8de-111">Si votre service requiert l’authentification de l’utilisateur, vous devez le signer avant de pouvoir utiliser l’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="5b8de-111">If your service requires user authentication, you need to sign in the user before he or she can use the messaging extension.</span></span> <span data-ttu-id="5b8de-112">Si vous avez écrit un bot ou un onglet qui se signe dans l’utilisateur, cette section doit être familière.</span><span class="sxs-lookup"><span data-stu-id="5b8de-112">If you have written a bot or a tab that signs in the user, this section should be familiar.</span></span>

<span data-ttu-id="5b8de-113">La séquence est la suivante :</span><span class="sxs-lookup"><span data-stu-id="5b8de-113">The sequence is as follows:</span></span>

1. <span data-ttu-id="5b8de-114">Un utilisateur envoie une requête ou la requête par défaut est automatiquement envoyée à votre service.</span><span class="sxs-lookup"><span data-stu-id="5b8de-114">User issues a query, or the default query is automatically sent to your service.</span></span>
2. <span data-ttu-id="5b8de-115">Votre service vérifie si l’utilisateur s’est d’abord authentifié en inspectant l’ID d’utilisateur Teams.</span><span class="sxs-lookup"><span data-stu-id="5b8de-115">Your service checks whether the user has first authenticated by inspecting the Teams user ID.</span></span>
3. <span data-ttu-id="5b8de-116">Si l’utilisateur ne s’est pas authentifié, renvoyez une réponse avec une action suggérée, y compris `auth` `openUrl` l’URL d’authentification.</span><span class="sxs-lookup"><span data-stu-id="5b8de-116">If the user has not authenticated, send back an `auth` response with an `openUrl` suggested action including the authentication URL.</span></span>
4. <span data-ttu-id="5b8de-117">Le client Microsoft Teams lance une fenêtre pop-up hébergeant votre page web à l’aide de l’URL d’authentification donnée.</span><span class="sxs-lookup"><span data-stu-id="5b8de-117">The Microsoft Teams client launches a pop-up window hosting your webpage using the given authentication URL.</span></span>
5. <span data-ttu-id="5b8de-118">Une fois que l’utilisateur s’est signé, vous devez fermer votre fenêtre et envoyer un « code d’authentification » au client Teams.</span><span class="sxs-lookup"><span data-stu-id="5b8de-118">After the user signs in, you should close your window and send an "authentication code" to the Teams client.</span></span>
6. <span data-ttu-id="5b8de-119">Le client Teams ressue ensuite la requête à votre service, qui inclut le code d’authentification passé à l’étape 5.</span><span class="sxs-lookup"><span data-stu-id="5b8de-119">The Teams client then reissues the query to your service, which includes the authentication code passed in step 5.</span></span>

<span data-ttu-id="5b8de-120">Votre service doit vérifier que le code d’authentification reçu à l’étape 6 correspond à celui de l’étape 5.</span><span class="sxs-lookup"><span data-stu-id="5b8de-120">Your service should verify that the authentication code received in step 6 matches the one from step 5.</span></span> <span data-ttu-id="5b8de-121">Cela garantit qu’un utilisateur malveillant ne tente pas d’usurper ou de compromettre le flux de la signature.</span><span class="sxs-lookup"><span data-stu-id="5b8de-121">This ensures that a malicious user does not try to spoof or compromise the sign-in flow.</span></span> <span data-ttu-id="5b8de-122">Cela permet effectivement de « fermer la boucle » pour terminer la séquence d’authentification sécurisée.</span><span class="sxs-lookup"><span data-stu-id="5b8de-122">This effectively "closes the loop" to finish the secure authentication sequence.</span></span>

### <a name="respond-with-a-sign-in-action"></a><span data-ttu-id="5b8de-123">Répondre avec une action de se connectez</span><span class="sxs-lookup"><span data-stu-id="5b8de-123">Respond with a sign-in action</span></span>

<span data-ttu-id="5b8de-124">Pour inciter un utilisateur non authentifié à se connecter, répondez avec une action suggérée de type qui inclut `openUrl` l’URL d’authentification.</span><span class="sxs-lookup"><span data-stu-id="5b8de-124">To prompt an unauthenticated user to sign in, respond with a suggested action of type `openUrl` that includes the authentication URL.</span></span>

#### <a name="response-example-for-a-sign-in-action"></a><span data-ttu-id="5b8de-125">Exemple de réponse pour une action de sign-in</span><span class="sxs-lookup"><span data-stu-id="5b8de-125">Response example for a sign-in action</span></span>

```json
{
  "composeExtension":{
    "type":"auth",
    "suggestedActions":{
      "actions":[
        {
          "type": "openUrl",
          "value": "https://example.com/auth",
          "title": "Sign in to this app"
        }
      ]
    }
  }
}
```

> [!NOTE]
> <span data-ttu-id="5b8de-126">Pour que l’expérience de se connecte soit hébergée dans une fenêtre pop-up Teams, la partie domaine de l’URL doit se trouver dans la liste des domaines valides de votre application.</span><span class="sxs-lookup"><span data-stu-id="5b8de-126">For the sign-in experience to be hosted in a Teams pop-up, the domain portion of the URL must be in your app’s list of valid domains.</span></span> <span data-ttu-id="5b8de-127">(Voir [validDomains](~/resources/schema/manifest-schema.md#validdomains) dans le schéma de manifeste.)</span><span class="sxs-lookup"><span data-stu-id="5b8de-127">(See [validDomains](~/resources/schema/manifest-schema.md#validdomains) in the manifest schema.)</span></span>

### <a name="start-the-sign-in-flow"></a><span data-ttu-id="5b8de-128">Démarrer le flux de la signature</span><span class="sxs-lookup"><span data-stu-id="5b8de-128">Start the sign-in flow</span></span>

<span data-ttu-id="5b8de-129">Votre expérience de sign-in doit être réactive et tenir dans une fenêtre popup.</span><span class="sxs-lookup"><span data-stu-id="5b8de-129">Your sign-in experience should be responsive and fit within a popup window.</span></span> <span data-ttu-id="5b8de-130">Il doit s’intégrer au [SDK client JavaScript Microsoft Teams,](/javascript/api/overview/msteams-client)qui utilise la transmission de message.</span><span class="sxs-lookup"><span data-stu-id="5b8de-130">It should integrate with the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client), which uses message passing.</span></span>

<span data-ttu-id="5b8de-131">Comme avec d’autres expériences incorporées en cours d’exécution dans Microsoft Teams, votre code à l’intérieur de la fenêtre doit d’abord `microsoftTeams.initialize()` appeler.</span><span class="sxs-lookup"><span data-stu-id="5b8de-131">As with other embedded experiences running inside Microsoft Teams, your code inside the window needs to first call `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="5b8de-132">Si votre code effectue un flux OAuth, vous pouvez transmettre l’ID utilisateur Teams dans votre fenêtre, qui peut ensuite le transmettre à l’URL de la signature OAuth.</span><span class="sxs-lookup"><span data-stu-id="5b8de-132">If your code performs an OAuth flow, you can pass the Teams user ID into your window, which then can pass it to the OAuth sign-in URL.</span></span>

### <a name="complete-the-sign-in-flow"></a><span data-ttu-id="5b8de-133">Terminer le flux de la signature</span><span class="sxs-lookup"><span data-stu-id="5b8de-133">Complete the sign-in flow</span></span>

<span data-ttu-id="5b8de-134">Lorsque la demande de se connecte est terminée et redirige vers votre page, elle doit effectuer les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="5b8de-134">When the sign-in request completes and redirects back to your page, it should perform the following steps:</span></span>

1. <span data-ttu-id="5b8de-135">Générer un code de sécurité.</span><span class="sxs-lookup"><span data-stu-id="5b8de-135">Generate a security code.</span></span> <span data-ttu-id="5b8de-136">(Il peut s’agit d’un nombre aléatoire.) Vous devez mettre en cache ce code sur votre service, ainsi que les informations d’identification obtenues via le flux de connexion (tels que les jetons OAuth 2.0).</span><span class="sxs-lookup"><span data-stu-id="5b8de-136">(This can be a random number.) You need to cache this code on your service, along with the credentials obtained through the sign-in flow (such as OAuth 2.0 tokens).</span></span>
2. <span data-ttu-id="5b8de-137">Appelez `microsoftTeams.authentication.notifySuccess` et passez le code de sécurité.</span><span class="sxs-lookup"><span data-stu-id="5b8de-137">Call `microsoftTeams.authentication.notifySuccess` and pass the security code.</span></span>

<span data-ttu-id="5b8de-138">À ce stade, la fenêtre se ferme et le contrôle est transmis au client Teams.</span><span class="sxs-lookup"><span data-stu-id="5b8de-138">At this point, the window closes and control is passed to the Teams client.</span></span> <span data-ttu-id="5b8de-139">Le client peut maintenant rééditer la requête utilisateur d’origine, ainsi que le code de sécurité dans la `state` propriété.</span><span class="sxs-lookup"><span data-stu-id="5b8de-139">The client now can reissue the original user query, along with the security code in the `state` property.</span></span> <span data-ttu-id="5b8de-140">Votre code peut utiliser le code de sécurité pour rechercher les informations d’identification stockées précédemment pour terminer la séquence d’authentification, puis effectuer la demande de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5b8de-140">Your code can use the security code to look up the credentials stored earlier to complete the authentication sequence and then complete the user request.</span></span>

#### <a name="reissued-request-example"></a><span data-ttu-id="5b8de-141">Exemple de requête rééditée</span><span class="sxs-lookup"><span data-stu-id="5b8de-141">Reissued request example</span></span>

```json
{
    "name": "composeExtension/query",
    "value": {
        "commandId": "insertWiki",
        "parameters": [{
            "name": "searchKeyword",
            "value": "lakers"
        }],
        "state": "12345",
        "queryOptions": {
            "skip": 0,
            "count": 25
        }
    },
    "type": "invoke",
    "timestamp": "2017-04-26T05:18:25.629Z",
    "localTimestamp": "2017-04-25T22:18:25.629-07:00",
    "entities": [{
        "locale": "en-US",
        "country": "US",
        "platform": "Web",
        "type": "clientInfo"
    }],
    "text": "",
    "attachments": [],
    "address": {
        "id": "f:7638210432489287768",
        "channelId": "msteams",
        "user": {
            "id": "29:1A5TJWHkbOwSyu_L9Ktk9QFI1d_kBOEPeNEeO1INscpKHzHTvWfiau5AX_6y3SuiOby-r73dzHJ17HipUWqGPgw",
            "aadObjectId": "fc8ca1c0-d043-4af6-b09f-141536207403"
        },
        "conversation": {
            "id": "19:7705841b240044b297123ad7f9c99217@thread.skype"
        },
        "bot": {
            "id": "28:c073afa8-7e77-4f92-b3e7-aa589e952a3e",
            "name": "maotestbot2"
        },
        "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
        "useAuth": true
    },
    "source": "msteams"
}
```

## <a name="code-sample"></a><span data-ttu-id="5b8de-142">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="5b8de-142">Code sample</span></span>
|<span data-ttu-id="5b8de-143">**Exemple de nom**</span><span class="sxs-lookup"><span data-stu-id="5b8de-143">**Sample name**</span></span> | <span data-ttu-id="5b8de-144">**Description**</span><span class="sxs-lookup"><span data-stu-id="5b8de-144">**Description**</span></span> |<span data-ttu-id="5b8de-145">**.NET**</span><span class="sxs-lookup"><span data-stu-id="5b8de-145">**.NET**</span></span> | <span data-ttu-id="5b8de-146">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="5b8de-146">**Node.js**</span></span>|
|----------------|-----------------|--------------|----------------|
|<span data-ttu-id="5b8de-147">Extensions de messagerie : th et config</span><span class="sxs-lookup"><span data-stu-id="5b8de-147">Messaging extensions - auth and config</span></span> | <span data-ttu-id="5b8de-148">Extension de messagerie qui possède une page de configuration, accepte les demandes de recherche et renvoie les résultats une fois que l’utilisateur s’est inscrit.</span><span class="sxs-lookup"><span data-stu-id="5b8de-148">A Messaging Extension that has a configuration page, accepts search requests, and returns results after the user has signed in.</span></span> |[<span data-ttu-id="5b8de-149">View</span><span class="sxs-lookup"><span data-stu-id="5b8de-149">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config)|[<span data-ttu-id="5b8de-150">View</span><span class="sxs-lookup"><span data-stu-id="5b8de-150">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/javascript_nodejs/52.teams-messaging-extensions-search-auth-config)| 

 
