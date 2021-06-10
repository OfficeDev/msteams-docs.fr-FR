---
title: Ajouter une authentification à votre extension de messagerie
author: clearab
description: Comment ajouter l’authentification à une extension de messagerie
localization_priority: Normal
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 1670bcd68def5470f2a590b11f7c25a00ccd06b7
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020708"
---
# <a name="add-authentication-to-your-messaging-extension"></a><span data-ttu-id="f2af5-103">Ajouter une authentification à votre extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="f2af5-103">Add authentication to your messaging extension</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

## <a name="identify-the-user"></a><span data-ttu-id="f2af5-104">Identifier l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="f2af5-104">Identify the user</span></span>

<span data-ttu-id="f2af5-105">Chaque demande à vos services inclut l’ID utilisateur, le nom d’affichage de l’utilisateur et Azure Active Directory’objet.</span><span class="sxs-lookup"><span data-stu-id="f2af5-105">Every request to your services includes the user  ID, the user's display name and Azure Active Directory object ID.</span></span>

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

<span data-ttu-id="f2af5-106">Les `id` `aadObjectId` valeurs et les valeurs sont garanties pour l’utilisateur Teams authentifié.</span><span class="sxs-lookup"><span data-stu-id="f2af5-106">The `id` and `aadObjectId` values are guaranteed for the authenticated Teams user.</span></span> <span data-ttu-id="f2af5-107">Ils sont utilisés comme clés pour rechercher les informations d’identification ou tout état mis en cache dans votre service.</span><span class="sxs-lookup"><span data-stu-id="f2af5-107">They are used as keys to look up the credentials or any cached state in your service.</span></span> <span data-ttu-id="f2af5-108">En outre, chaque demande contient l’ID Azure Active Directory client de l’utilisateur, qui est utilisé pour identifier l’organisation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f2af5-108">In addition, each request contains the Azure Active Directory tenant ID of the user, which is used to identify the user’s organization.</span></span> <span data-ttu-id="f2af5-109">Le cas échéant, la demande contient également l’ID d’équipe et l’ID de canal d’où provient la demande.</span><span class="sxs-lookup"><span data-stu-id="f2af5-109">If applicable, the request also contains the team Id and channel ID from which the request is originated.</span></span>

## <a name="authentication"></a><span data-ttu-id="f2af5-110">Authentification</span><span class="sxs-lookup"><span data-stu-id="f2af5-110">Authentication</span></span>

<span data-ttu-id="f2af5-111">Si votre service nécessite une authentification utilisateur, les utilisateurs doivent se connecter avant d’utiliser l’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="f2af5-111">If your service requires user authentication, the users must sign in before they use the messaging extension.</span></span> <span data-ttu-id="f2af5-112">Les étapes d’authentification sont similaires à celle d’un bot ou d’un onglet. La séquence est la suivante :</span><span class="sxs-lookup"><span data-stu-id="f2af5-112">The authentication steps are similar to that of a bot or tab. The sequence is as follows:</span></span>

1. <span data-ttu-id="f2af5-113">Un utilisateur envoie une requête ou la requête par défaut est automatiquement envoyée à votre service.</span><span class="sxs-lookup"><span data-stu-id="f2af5-113">User issues a query, or the default query is automatically sent to your service.</span></span>
1. <span data-ttu-id="f2af5-114">Votre service vérifie si l’utilisateur est authentifié en inspectant l’Teams’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f2af5-114">Your service checks whether the user is authenticated by inspecting the Teams user ID.</span></span>
1. <span data-ttu-id="f2af5-115">Si l’utilisateur n’est pas authentifié, renvoyez une réponse avec une action suggérée, y compris `auth` `openUrl` l’URL d’authentification.</span><span class="sxs-lookup"><span data-stu-id="f2af5-115">If the user is not authenticated, send back an `auth` response with an `openUrl` suggested action including the authentication URL.</span></span>
1. <span data-ttu-id="f2af5-116">Le client Microsoft Teams lance une boîte de dialogue hébergeant votre page web à l’aide de l’URL d’authentification donnée.</span><span class="sxs-lookup"><span data-stu-id="f2af5-116">The Microsoft Teams client launches a dialog box hosting your webpage using the given authentication URL.</span></span>
1. <span data-ttu-id="f2af5-117">Une fois que l’utilisateur se signe, vous devez fermer votre fenêtre et envoyer un **code d’authentification** au client Teams client.</span><span class="sxs-lookup"><span data-stu-id="f2af5-117">After the user signs in, you should close your window and send an **authentication code** to the Teams client.</span></span>
1. <span data-ttu-id="f2af5-118">Le Teams client ressue ensuite la requête à votre service, qui inclut le code d’authentification passé à l’étape 5.</span><span class="sxs-lookup"><span data-stu-id="f2af5-118">The Teams client then reissues the query to your service, which includes the authentication code passed in Step 5.</span></span>

<span data-ttu-id="f2af5-119">Votre service doit vérifier que le code d’authentification reçu à l’étape 6 correspond à celui de l’étape 5.</span><span class="sxs-lookup"><span data-stu-id="f2af5-119">Your service should verify that the authentication code received in step 6 matches the one from step 5.</span></span> <span data-ttu-id="f2af5-120">Cela garantit qu’un utilisateur malveillant ne tente pas d’usurper ou de compromettre le flux de la signature.</span><span class="sxs-lookup"><span data-stu-id="f2af5-120">This ensures that a malicious user does not try to spoof or compromise the sign in flow.</span></span> <span data-ttu-id="f2af5-121">Cela permet effectivement de « fermer la boucle » pour terminer la séquence d’authentification sécurisée.</span><span class="sxs-lookup"><span data-stu-id="f2af5-121">This effectively "closes the loop" to finish the secure authentication sequence.</span></span>

### <a name="respond-with-a-sign-in-action"></a><span data-ttu-id="f2af5-122">Répondre avec une action de se connectez</span><span class="sxs-lookup"><span data-stu-id="f2af5-122">Respond with a sign-in action</span></span>

<span data-ttu-id="f2af5-123">Pour inviter un utilisateur non authentifié à se connecter, répondez avec une action suggérée de type qui inclut `openUrl` l’URL d’authentification.</span><span class="sxs-lookup"><span data-stu-id="f2af5-123">To prompt an unauthenticated user to sign in, respond with a suggested action of type `openUrl` that includes the authentication URL.</span></span>

#### <a name="response-example-for-a-sign-in-action"></a><span data-ttu-id="f2af5-124">Exemple de réponse pour une action de sign-in</span><span class="sxs-lookup"><span data-stu-id="f2af5-124">Response example for a sign-in action</span></span>

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
> <span data-ttu-id="f2af5-125">Pour que l’expérience de se connecte soit hébergée dans une fenêtre Teams, la partie domaine de l’URL doit se trouver dans la liste des domaines valides de votre application.</span><span class="sxs-lookup"><span data-stu-id="f2af5-125">For the sign in experience to be hosted in a Teams pop-up window, the domain portion of the URL must be in your app’s list of valid domains.</span></span> <span data-ttu-id="f2af5-126">Pour plus d’informations, [voir validDomains](~/resources/schema/manifest-schema.md#validdomains) dans le schéma de manifeste.</span><span class="sxs-lookup"><span data-stu-id="f2af5-126">For more information, see [validDomains](~/resources/schema/manifest-schema.md#validdomains) in the manifest schema.</span></span>

### <a name="start-the-sign-in-flow"></a><span data-ttu-id="f2af5-127">Démarrer le flux de la signature</span><span class="sxs-lookup"><span data-stu-id="f2af5-127">Start the sign in flow</span></span>

<span data-ttu-id="f2af5-128">Votre expérience de se connecte doit être réactive et tenir dans une fenêtre pop-up.</span><span class="sxs-lookup"><span data-stu-id="f2af5-128">Your sign in experience must be responsive and fit within a pop-up window.</span></span> <span data-ttu-id="f2af5-129">Il doit s’intégrer au [SDK Microsoft Teams client JavaScript,](/javascript/api/overview/msteams-client)qui utilise la transmission de message.</span><span class="sxs-lookup"><span data-stu-id="f2af5-129">It should integrate with the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client), which uses message passing.</span></span>

<span data-ttu-id="f2af5-130">Comme avec d’autres expériences incorporées en cours d Microsoft Teams, votre code à l’intérieur de la fenêtre doit d’abord `microsoftTeams.initialize()` appeler.</span><span class="sxs-lookup"><span data-stu-id="f2af5-130">As with other embedded experiences running inside Microsoft Teams, your code inside the window needs to first call `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="f2af5-131">Si votre code effectue un flux OAuth, vous pouvez transmettre l’ID d’utilisateur Teams dans votre fenêtre, qui le transmet ensuite à l’URL de la signature OAuth.</span><span class="sxs-lookup"><span data-stu-id="f2af5-131">If your code performs an OAuth flow, you can pass the Teams user ID into your window, which then passes it to the OAuth sign-in URL.</span></span>

### <a name="complete-the-sign-in-flow"></a><span data-ttu-id="f2af5-132">Terminer le flux de la signature</span><span class="sxs-lookup"><span data-stu-id="f2af5-132">Complete the sign in flow</span></span>

<span data-ttu-id="f2af5-133">Lorsque la demande de se connecte est terminée et redirige vers votre page, elle doit effectuer les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="f2af5-133">When the sign in request completes and redirects back to your page, it must perform the following steps:</span></span>

1. <span data-ttu-id="f2af5-134">Générer un code de sécurité.</span><span class="sxs-lookup"><span data-stu-id="f2af5-134">Generate a security code.</span></span> <span data-ttu-id="f2af5-135">Il s’agit d’un nombre aléatoire.</span><span class="sxs-lookup"><span data-stu-id="f2af5-135">This is a random number.</span></span> <span data-ttu-id="f2af5-136">Vous devez mettre en cache ce code sur votre service, ainsi que les informations d’identification obtenues via le flux de connexion, telles que les jetons OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="f2af5-136">You must cache this code on your service, along with the credentials obtained through the sign in flow, such as OAuth 2.0 tokens.</span></span>
1. <span data-ttu-id="f2af5-137">Appelez `microsoftTeams.authentication.notifySuccess` et passez le code de sécurité.</span><span class="sxs-lookup"><span data-stu-id="f2af5-137">Call `microsoftTeams.authentication.notifySuccess` and pass the security code.</span></span>

<span data-ttu-id="f2af5-138">À ce stade, la fenêtre se ferme et le contrôle est transmis au client Teams client.</span><span class="sxs-lookup"><span data-stu-id="f2af5-138">At this point, the window closes and control is passed to the Teams client.</span></span> <span data-ttu-id="f2af5-139">Le client ressue désormais la requête utilisateur d’origine, ainsi que le code de sécurité dans la `state` propriété.</span><span class="sxs-lookup"><span data-stu-id="f2af5-139">The client now reissues the original user query, along with the security code in the `state` property.</span></span> <span data-ttu-id="f2af5-140">Votre code peut utiliser le code de sécurité pour rechercher les informations d’identification stockées précédemment pour terminer la séquence d’authentification, puis effectuer la demande de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f2af5-140">Your code can use the security code to look up the credentials stored earlier to complete the authentication sequence and then complete the user request.</span></span>

#### <a name="reissued-request-example"></a><span data-ttu-id="f2af5-141">Exemple de requête rééditée</span><span class="sxs-lookup"><span data-stu-id="f2af5-141">Reissued request example</span></span>

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

## <a name="code-sample"></a><span data-ttu-id="f2af5-142">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="f2af5-142">Code sample</span></span>
|<span data-ttu-id="f2af5-143">**Exemple de nom**</span><span class="sxs-lookup"><span data-stu-id="f2af5-143">**Sample name**</span></span> | <span data-ttu-id="f2af5-144">**Description**</span><span class="sxs-lookup"><span data-stu-id="f2af5-144">**Description**</span></span> |<span data-ttu-id="f2af5-145">**.NET**</span><span class="sxs-lookup"><span data-stu-id="f2af5-145">**.NET**</span></span> | <span data-ttu-id="f2af5-146">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="f2af5-146">**Node.js**</span></span>|
|----------------|-----------------|--------------|----------------|
|<span data-ttu-id="f2af5-147">Extensions de messagerie : th et config</span><span class="sxs-lookup"><span data-stu-id="f2af5-147">Messaging extensions - auth and config</span></span> | <span data-ttu-id="f2af5-148">Extension de messagerie qui possède une page de configuration, accepte les demandes de recherche et renvoie les résultats une fois que l’utilisateur s’est inscrit.</span><span class="sxs-lookup"><span data-stu-id="f2af5-148">A Messaging Extension that has a configuration page, accepts search requests, and returns results after the user has signed in.</span></span> |[<span data-ttu-id="f2af5-149">View</span><span class="sxs-lookup"><span data-stu-id="f2af5-149">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config)|[<span data-ttu-id="f2af5-150">View</span><span class="sxs-lookup"><span data-stu-id="f2af5-150">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/javascript_nodejs/52.teams-messaging-extensions-search-auth-config)| 

 
