---
title: Rechercher avec des extensions de messagerie
description: Décrit comment développer des extensions de messagerie basées sur la recherche
keywords: teams messaging extensions messaging extensions search
ms.topic: how-to
localization_priority: Normal
ms.date: 07/20/2019
ms.openlocfilehash: 89b8a42f0a9ec86d22d194d2fe5145fba5489f20
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019726"
---
# <a name="search-with-messaging-extensions"></a><span data-ttu-id="945e4-104">Rechercher avec des extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="945e4-104">Search with messaging extensions</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

<span data-ttu-id="945e4-105">Les extensions de messagerie basées sur la recherche vous permettent d'interroger votre service et de publier ces informations sous la forme d'une carte, directement dans votre message</span><span class="sxs-lookup"><span data-stu-id="945e4-105">Search based messaging extensions allow you to query your service and post that information in the form of a card, right into your message</span></span>

![Exemple de carte d'extension de messagerie](~/assets/images/compose-extensions/ceexample.png)

<span data-ttu-id="945e4-107">Les sections suivantes décrivent comment faire.</span><span class="sxs-lookup"><span data-stu-id="945e4-107">The following sections describe how to do this.</span></span>

[!include[common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

### <a name="search-type-message-extensions"></a><span data-ttu-id="945e4-108">Extensions de message de type de recherche</span><span class="sxs-lookup"><span data-stu-id="945e4-108">Search type message extensions</span></span>

<span data-ttu-id="945e4-109">Pour l'extension de messagerie basée sur la recherche, définissez `type` le paramètre sur `query` .</span><span class="sxs-lookup"><span data-stu-id="945e4-109">For search based messaging extension set the `type` parameter to `query`.</span></span> <span data-ttu-id="945e4-110">Vous trouverez ci-dessous un exemple de manifeste avec une seule commande de recherche.</span><span class="sxs-lookup"><span data-stu-id="945e4-110">Below is an example of a manifest with a single search command.</span></span> <span data-ttu-id="945e4-111">Une seule extension de messagerie peut avoir jusqu'à 10 commandes différentes associées.</span><span class="sxs-lookup"><span data-stu-id="945e4-111">A single messaging extension can have up to 10 different commands associated with it.</span></span> <span data-ttu-id="945e4-112">Cela peut inclure à la fois plusieurs commandes de recherche et plusieurs commandes basées sur l'action.</span><span class="sxs-lookup"><span data-stu-id="945e4-112">This can include both multiple search and multiple Action-based commands.</span></span>

#### <a name="complete-app-manifest-example"></a><span data-ttu-id="945e4-113">Exemple de manifeste d'application complet</span><span class="sxs-lookup"><span data-stu-id="945e4-113">Complete app manifest example</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "version": "1.0",
  "id": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
  "packageName": "com.microsoft.teams.samples.bing",
  "developer": {
    "name": "John Developer",
    "websiteUrl": "http://bingbotservice.azurewebsites.net/",
    "privacyUrl": "http://bingbotservice.azurewebsites.net/privacy",
    "termsOfUseUrl": "http://bingbotservice.azurewebsites.net/termsofuse"
  },
  "name": {
    "short": "Bing",
    "full": "Bing"
  },
  "description": {
    "short": "Find Bing search results",
    "full": "Find Bing search results and share them with your team members."
  },
  "icons": {
    "outline": "bing-outline.jpg",
    "color": "bing-color.jpg"
  },
  "accentColor": "#ff6a00",
  "composeExtensions": [
    {
      "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
      "canUpdateConfiguration": true,
      "commands": [{
          "id": "searchCmd",
          "description": "Search Bing for information on the web",
          "title": "Search",
          "initialRun": true,
          "parameters": [{
            "name": "searchKeyword",
            "description": "Enter your search keywords",
            "title": "Keywords"
          }]
        }
      ]
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "validDomains": [
    "bingbotservice.azurewebsites.net",
    "*.bingbotservice.azurewebsites.net"
  ]
}
```

### <a name="test-via-uploading"></a><span data-ttu-id="945e4-114">Test via le téléchargement</span><span class="sxs-lookup"><span data-stu-id="945e4-114">Test via uploading</span></span>

<span data-ttu-id="945e4-115">Vous pouvez tester votre extension de messagerie en chargeant votre application.</span><span class="sxs-lookup"><span data-stu-id="945e4-115">You can test your messaging extension by uploading your app.</span></span>

<span data-ttu-id="945e4-116">Pour ouvrir votre extension de messagerie, accédez à vos conversations ou canaux.</span><span class="sxs-lookup"><span data-stu-id="945e4-116">To open your messaging extension, navigate to any of your chats or channels.</span></span> <span data-ttu-id="945e4-117">Choisissez le **bouton Plus d'options** (**&#8943;**) dans la zone de composition, puis choisissez votre extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="945e4-117">Choose the **More options** (**&#8943;**) button in the compose box, and choose your messaging extension.</span></span>

## <a name="add-event-handlers"></a><span data-ttu-id="945e4-118">Ajouter des handlers d'événements</span><span class="sxs-lookup"><span data-stu-id="945e4-118">Add event handlers</span></span>

<span data-ttu-id="945e4-119">La majeure partie de votre travail implique l'événement, qui gère toutes les interactions dans la `onQuery` fenêtre d'extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="945e4-119">Most of your work involves the `onQuery` event, which handles all interactions in the messaging extension window.</span></span>

<span data-ttu-id="945e4-120">Si vous le définissez dans le manifeste, vous activez l'élément de `canUpdateConfiguration` `true` menu **Paramètres** pour votre extension de messagerie et vous devez également gérer `onQuerySettingsUrl` et `onSettingsUpdate` .</span><span class="sxs-lookup"><span data-stu-id="945e4-120">If you set `canUpdateConfiguration` to `true` in the manifest, you enable the **Settings** menu item for your messaging extension and must also handle `onQuerySettingsUrl` and `onSettingsUpdate`.</span></span>

### <a name="handle-onquery-events"></a><span data-ttu-id="945e4-121">Gérer les événements onQuery</span><span class="sxs-lookup"><span data-stu-id="945e4-121">Handle onQuery events</span></span>

<span data-ttu-id="945e4-122">Une extension de messagerie reçoit un événement lorsqu'un événement se produit dans la fenêtre d'extension de messagerie ou `onQuery` est envoyé à la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="945e4-122">A messaging extension receives an `onQuery` event when anything happens in the messaging extension window or is sent to the window.</span></span>

<span data-ttu-id="945e4-123">Si votre extension de messagerie utilise une page de configuration, votre responsable doit d'abord vérifier les informations de configuration stockées ; si l'extension de messagerie n'est pas configurée, renvoyez une réponse avec un lien vers votre page de `onQuery` `config` configuration.</span><span class="sxs-lookup"><span data-stu-id="945e4-123">If your messaging extension uses a configuration page, your handler for `onQuery` should first check for any stored configuration information; if the messaging extension isn't configured, return a `config` response with a link to your configuration page.</span></span> <span data-ttu-id="945e4-124">N'ignorez pas que la réponse de la page de configuration est également gérée par `onQuery` .</span><span class="sxs-lookup"><span data-stu-id="945e4-124">Be aware that the response from the configuration page is also handled by `onQuery`.</span></span> <span data-ttu-id="945e4-125">(La seule exception est lorsque la page de configuration est appelée par le responsable pour `onQuerySettingsUrl` ; voir la section suivante.)</span><span class="sxs-lookup"><span data-stu-id="945e4-125">(The sole exception is when the configuration page is called by the handler for `onQuerySettingsUrl`; see the following section.)</span></span>

<span data-ttu-id="945e4-126">Si votre extension de messagerie nécessite une authentification, vérifiez les informations d'état de l'utilisateur . Si l'utilisateur n'est pas signé, suivez les instructions de la section [Authentification](#authentication) plus loin dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="945e4-126">If your messaging extension requires authentication, check the user state information; if the user isn't signed in, follow the instructions in the [Authentication](#authentication) section later in this topic.</span></span>

<span data-ttu-id="945e4-127">Ensuite, vérifiez si elle est définie ; si c'est le cas, prenez les mesures appropriées, par exemple en fournissant des `initialRun` instructions ou une liste de réponses.</span><span class="sxs-lookup"><span data-stu-id="945e4-127">Next, check whether `initialRun` is set; if so, take appropriate action, such as providing instructions or a list of responses.</span></span>

<span data-ttu-id="945e4-128">Le reste de votre responsable invite l'utilisateur à fournir des informations, affiche une liste de cartes d'aperçu et renvoie la carte sélectionnée `onQuery` par l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="945e4-128">The remainder of your handler for `onQuery` prompts the user for information, displays a list of preview cards, and returns the card selected by the user.</span></span>

### <a name="handle-onquerysettingsurl-and-onsettingsupdate-events"></a><span data-ttu-id="945e4-129">Gérer les événements onQuerySettingsUrl et onSettingsUpdate</span><span class="sxs-lookup"><span data-stu-id="945e4-129">Handle onQuerySettingsUrl and onSettingsUpdate events</span></span>

<span data-ttu-id="945e4-130">Les `onQuerySettingsUrl` `onSettingsUpdate` événements et les événements fonctionnent ensemble pour activer **l'élément de menu Paramètres.**</span><span class="sxs-lookup"><span data-stu-id="945e4-130">The `onQuerySettingsUrl` and `onSettingsUpdate` events work together to enable the **Settings** menu item.</span></span>

![Captures d'écran des emplacements de l'élément de menu Paramètres](~/assets/images/compose-extensions/compose-extension-settings-menu-item.png)

<span data-ttu-id="945e4-132">Votre responsable renvoie l'URL de la page de configuration ; après la fermeture de la page de configuration, votre responsable accepte et enregistre `onQuerySettingsUrl` `onSettingsUpdate` l'état renvoyé.</span><span class="sxs-lookup"><span data-stu-id="945e4-132">Your handler for `onQuerySettingsUrl` returns the URL for the configuration page; after the configuration page closes, your handler for `onSettingsUpdate` accepts and saves the returned state.</span></span> <span data-ttu-id="945e4-133">(C'est le cas dans lequel `onQuery` *ne reçoit pas* la réponse de la page de configuration.)</span><span class="sxs-lookup"><span data-stu-id="945e4-133">(This is the one case in which `onQuery` *doesn't* receive the response from the configuration page.)</span></span>

## <a name="receive-and-respond-to-queries"></a><span data-ttu-id="945e4-134">Recevoir des requêtes et y répondre</span><span class="sxs-lookup"><span data-stu-id="945e4-134">Receive and respond to queries</span></span>

<span data-ttu-id="945e4-135">Chaque demande à votre extension de messagerie est effectuée via un objet qui `Activity` est publié sur votre URL de rappel.</span><span class="sxs-lookup"><span data-stu-id="945e4-135">Every request to your messaging extension is done via an `Activity` object that is posted to your callback URL.</span></span> <span data-ttu-id="945e4-136">La demande contient des informations sur la commande utilisateur, telles que les valeurs d'ID et de paramètre.</span><span class="sxs-lookup"><span data-stu-id="945e4-136">The request contains information about the user command, such as ID and parameter values.</span></span> <span data-ttu-id="945e4-137">La demande fournit également des métadonnées sur le contexte dans lequel votre extension a été invoquée, y compris l'ID d'utilisateur et de client, ainsi que les ID de conversation, le canal et les ID d'équipe.</span><span class="sxs-lookup"><span data-stu-id="945e4-137">The request also supplies metadata about the context in which your extension was invoked, including user and tenant ID, along with chat ID or channel and team IDs.</span></span>

### <a name="receive-user-requests"></a><span data-ttu-id="945e4-138">Recevoir des demandes des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="945e4-138">Receive user requests</span></span>

<span data-ttu-id="945e4-139">Lorsqu'un utilisateur effectue une requête, Microsoft Teams envoie à votre service un objet Bot Framework `Activity` standard.</span><span class="sxs-lookup"><span data-stu-id="945e4-139">When a user performs a query, Microsoft Teams sends your service a standard Bot Framework `Activity` object.</span></span> <span data-ttu-id="945e4-140">Votre service doit effectuer sa logique pour un type qui a été définie sur un type pris en charge, comme indiqué `Activity` `type` dans le tableau `invoke` `name` `composeExtension` suivant.</span><span class="sxs-lookup"><span data-stu-id="945e4-140">Your service should perform its logic for an `Activity` that has `type` set to `invoke` and `name` set to a supported `composeExtension` type, as shown in the following table.</span></span>

<span data-ttu-id="945e4-141">Outre les propriétés d'activité standard du bot, la charge utile contient les métadonnées de requête suivantes :</span><span class="sxs-lookup"><span data-stu-id="945e4-141">In addition to the standard bot activity properties, the payload contains the following request metadata:</span></span>

|<span data-ttu-id="945e4-142">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="945e4-142">Property name</span></span>|<span data-ttu-id="945e4-143">Objectif</span><span class="sxs-lookup"><span data-stu-id="945e4-143">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="945e4-144">Type de demande ; doit être `invoke` .</span><span class="sxs-lookup"><span data-stu-id="945e4-144">Type of request; must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="945e4-145">Type de commande qui est émis pour votre service.</span><span class="sxs-lookup"><span data-stu-id="945e4-145">Type of command that is issued to your service.</span></span> <span data-ttu-id="945e4-146">Actuellement, les types suivants sont pris en charge :</span><span class="sxs-lookup"><span data-stu-id="945e4-146">Currently the following types are supported:</span></span> <br>`composeExtension/query` <br>`composeExtension/querySettingUrl` <br>`composeExtension/setting` <br>`composeExtension/selectItem` <br>`composeExtension/queryLink` |
|`from.id`| <span data-ttu-id="945e4-147">ID de l'utilisateur qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="945e4-147">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="945e4-148">Nom de l'utilisateur qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="945e4-148">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="945e4-149">ID d'objet Azure Active Directory de l'utilisateur qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="945e4-149">Azure Active Directory object id of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="945e4-150">ID du client Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="945e4-150">Azure Active Directory tenant ID.</span></span> |
|`channelData.channel.id`| <span data-ttu-id="945e4-151">ID de canal (si la demande a été faite dans un canal).</span><span class="sxs-lookup"><span data-stu-id="945e4-151">Channel ID (if the request was made in a channel).</span></span> |
|`channelData.team.id`| <span data-ttu-id="945e4-152">ID d'équipe (si la demande a été faite dans un canal).</span><span class="sxs-lookup"><span data-stu-id="945e4-152">Team ID (if the request was made in a channel).</span></span> |
|`clientInfo`|<span data-ttu-id="945e4-153">Métadonnées facultatives sur le logiciel client utilisé pour envoyer le message d'un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="945e4-153">Optional metadata about the client software used to send a user's message.</span></span> <span data-ttu-id="945e4-154">L'entité peut contenir deux propriétés :</span><span class="sxs-lookup"><span data-stu-id="945e4-154">The entity can contain two properties:</span></span><br><span data-ttu-id="945e4-155">Le `country` champ contient l'emplacement détecté par l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="945e4-155">The `country` field contains the user's detected location.</span></span><br><span data-ttu-id="945e4-156">Le `platform` champ décrit la plateforme cliente de messagerie.</span><span class="sxs-lookup"><span data-stu-id="945e4-156">The `platform` field describes the messaging client platform.</span></span> <br><span data-ttu-id="945e4-157">Pour plus d'informations, *consultez les* [types d'entités non IRI — clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo).</span><span class="sxs-lookup"><span data-stu-id="945e4-157">For additional information, please *see* [Non-IRI entity types — clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo).</span></span>|

<span data-ttu-id="945e4-158">Les paramètres de requête se trouvent dans l'objet value, qui inclut les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="945e4-158">The request parameters itself are found in the value object, which includes the following properties:</span></span>

| <span data-ttu-id="945e4-159">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="945e4-159">Property name</span></span> | <span data-ttu-id="945e4-160">Objectif</span><span class="sxs-lookup"><span data-stu-id="945e4-160">Purpose</span></span> |
|---|---|
| `commandId` | <span data-ttu-id="945e4-161">Nom de la commande invoquée par l'utilisateur, correspondant à l'une des commandes déclarées dans le manifeste de l'application.</span><span class="sxs-lookup"><span data-stu-id="945e4-161">The name of the command invoked by the user, matching one of the commands declared in the app manifest.</span></span> |
| `parameters` | <span data-ttu-id="945e4-162">Tableau de paramètres.</span><span class="sxs-lookup"><span data-stu-id="945e4-162">Array of parameters.</span></span> <span data-ttu-id="945e4-163">Chaque objet paramètre contient le nom du paramètre, ainsi que la valeur de paramètre fournie par l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="945e4-163">Each parameter object contains the parameter name, along with the parameter value provided by the user.</span></span> |
| `queryOptions` | <span data-ttu-id="945e4-164">Paramètres de pagination :</span><span class="sxs-lookup"><span data-stu-id="945e4-164">Pagination parameters:</span></span> <br><span data-ttu-id="945e4-165">`skip`: nombre d'ignorer pour cette requête</span><span class="sxs-lookup"><span data-stu-id="945e4-165">`skip`: skip count for this query</span></span> <br><span data-ttu-id="945e4-166">`count`: nombre d'éléments à renvoyer</span><span class="sxs-lookup"><span data-stu-id="945e4-166">`count`: number of elements to return</span></span> |

#### <a name="request-example"></a><span data-ttu-id="945e4-167">Exemple de requête</span><span class="sxs-lookup"><span data-stu-id="945e4-167">Request example</span></span>

```json
{
  "name": "composeExtension/query",
  "value": {
    "commandId": "searchCmd",
    "parameters": [
      {
        "name": "searchKeywords",
        "value": "Toronto"
      }
    ],
    "queryOptions": {
      "skip": 0,
      "count": 25
    }
  },
  "type": "invoke",
  "timestamp": "2017-05-01T15:45:51.876Z",
  "localTimestamp": "2017-05-01T08:45:51.876-07:00",
  "id": "f:622749630322482883",
  "channelId": "msteams",
  "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
  "from": {
    "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
    "name": "Larry Jin",
    "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
  },
  "conversation": {
    "id": "19:skypespaces_8198cfe0dd2647ae91930f0974768a40@thread.skype"
  },
  "recipient": {
    "id": "28:b4922ea1-5315-4fd0-9b21-d941ab06e39f",
    "name": "TheComposeExtensionDev"
  },
  "entities": [
    {
    "type": "clientInfo",
      "country": "US",
      "platform": "Windows"
    }
  ]
}
```

### <a name="receive-requests-from-links-inserted-into-the-compose-message-box"></a><span data-ttu-id="945e4-168">Recevoir des demandes à partir de liens insérés dans la zone composer un message</span><span class="sxs-lookup"><span data-stu-id="945e4-168">Receive requests from links inserted into the compose message box</span></span>

<span data-ttu-id="945e4-169">Comme alternative (ou en plus) à la recherche de votre service externe, vous pouvez utiliser une URL insérée dans la zone de composition de message pour interroger votre service et renvoyer une carte.</span><span class="sxs-lookup"><span data-stu-id="945e4-169">As an alternative (or in addition) to searching your external service, you can use a URL inserted into the compose message box to query your service and return a card.</span></span> <span data-ttu-id="945e4-170">Dans la capture d'écran ci-dessous, un utilisateur a passé une URL pour un élément de travail dans Azure DevOps que l'extension de messagerie a résolue en une carte.</span><span class="sxs-lookup"><span data-stu-id="945e4-170">In the screenshot below a user has pasted in a URL for a work item in Azure DevOps which the messaging extension has resolved into a card.</span></span>

![Exemple de déploiement de lien](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

<span data-ttu-id="945e4-172">Pour permettre à votre extension de messagerie d'interagir avec les liens de cette façon, vous devez d'abord ajouter le tableau au manifeste de votre application, comme dans `messageHandlers` l'exemple ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="945e4-172">To enable your messaging extension to interact with links this way you'll first need to add the `messageHandlers` array to your app manifest as in the example below:</span></span>

```json
"composeExtensions": [
  {
    "botId": "abc123456-ab12-ab12-ab12-abcdef123456",
    "messageHandlers": [
      {
        "type": "link",
        "value": {
          "domains": [
            "*.trackeddomain.com"
          ]
        }
      }
    ]
  }
]
```

<span data-ttu-id="945e4-173">Une fois que vous avez ajouté le domaine pour écouter le manifeste de [](#respond-to-user-requests) l'application, vous devez modifier votre code de bot pour répondre à la demande d'appel ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="945e4-173">Once you've added the domain to listen on to the app manifest, you'll need to change your bot code to [respond](#respond-to-user-requests) to the below invoke request.</span></span>

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

<span data-ttu-id="945e4-174">Si votre application renvoie plusieurs éléments, seul le premier sera utilisé.</span><span class="sxs-lookup"><span data-stu-id="945e4-174">If your app returns multiple items only the first will be used.</span></span>

### <a name="respond-to-user-requests"></a><span data-ttu-id="945e4-175">Répondre aux demandes des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="945e4-175">Respond to user requests</span></span>

<span data-ttu-id="945e4-176">Lorsque l'utilisateur effectue une requête, Microsoft Teams adresse une requête HTTP synchrone à votre service.</span><span class="sxs-lookup"><span data-stu-id="945e4-176">When the user performs a query, Microsoft Teams issues a synchronous HTTP request to your service.</span></span> <span data-ttu-id="945e4-177">À ce stade, votre code dispose de 5 secondes pour fournir une réponse HTTP à la demande.</span><span class="sxs-lookup"><span data-stu-id="945e4-177">At that point, your code has 5 seconds to provide an HTTP response to the request.</span></span> <span data-ttu-id="945e4-178">Pendant ce temps, votre service peut effectuer une recherche supplémentaire ou toute autre logique métier nécessaire pour répondre à la demande.</span><span class="sxs-lookup"><span data-stu-id="945e4-178">During this time, your service can perform additional lookup, or any other business logic needed to serve the request.</span></span>

<span data-ttu-id="945e4-179">Votre service doit répondre avec les résultats correspondant à la requête de l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="945e4-179">Your service should respond with the results matching the user query.</span></span> <span data-ttu-id="945e4-180">La réponse doit indiquer un code d'état HTTP et un objet `200 OK` application/json valide avec le corps suivant :</span><span class="sxs-lookup"><span data-stu-id="945e4-180">The response must indicate an HTTP status code of `200 OK` and a valid application/json object with the following body:</span></span>

|<span data-ttu-id="945e4-181">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="945e4-181">Property name</span></span>|<span data-ttu-id="945e4-182">Objectif</span><span class="sxs-lookup"><span data-stu-id="945e4-182">Purpose</span></span>|
|---|---|
|`composeExtension`|<span data-ttu-id="945e4-183">Enveloppe de réponse de niveau supérieur.</span><span class="sxs-lookup"><span data-stu-id="945e4-183">Top-level response envelope.</span></span>|
|`composeExtension.type`|<span data-ttu-id="945e4-184">Type de réponse.</span><span class="sxs-lookup"><span data-stu-id="945e4-184">Type of response.</span></span> <span data-ttu-id="945e4-185">Les types suivants sont pris en charge :</span><span class="sxs-lookup"><span data-stu-id="945e4-185">The following types are supported:</span></span> <br><span data-ttu-id="945e4-186">`result`: affiche une liste de résultats de recherche</span><span class="sxs-lookup"><span data-stu-id="945e4-186">`result`: displays a list of search results</span></span> <br><span data-ttu-id="945e4-187">`auth`: demande à l'utilisateur de s'authentifier</span><span class="sxs-lookup"><span data-stu-id="945e4-187">`auth`: asks the user to authenticate</span></span> <br><span data-ttu-id="945e4-188">`config`: demande à l'utilisateur de configurer l'extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="945e4-188">`config`: asks the user to set up the messaging extension</span></span> <br><span data-ttu-id="945e4-189">`message` : affiche un message en texte brut.</span><span class="sxs-lookup"><span data-stu-id="945e4-189">`message`: displays a plain text message</span></span> |
|`composeExtension.attachmentLayout`|<span data-ttu-id="945e4-190">Spécifie la disposition des pièces jointes.</span><span class="sxs-lookup"><span data-stu-id="945e4-190">Specifies the layout of the attachments.</span></span> <span data-ttu-id="945e4-191">Utilisé pour les réponses de type `result` .</span><span class="sxs-lookup"><span data-stu-id="945e4-191">Used for responses of type `result`.</span></span> <br><span data-ttu-id="945e4-192">Actuellement, les types suivants sont pris en charge :</span><span class="sxs-lookup"><span data-stu-id="945e4-192">Currently the following types are supported:</span></span> <br><span data-ttu-id="945e4-193">`list`: liste d'objets de carte contenant des champs de miniature, de titre et de texte</span><span class="sxs-lookup"><span data-stu-id="945e4-193">`list`: a list of card objects containing thumbnail, title, and text fields</span></span> <br><span data-ttu-id="945e4-194">`grid`: une grille d'images miniatures</span><span class="sxs-lookup"><span data-stu-id="945e4-194">`grid`: a grid of thumbnail images</span></span> |
|`composeExtension.attachments`|<span data-ttu-id="945e4-195">Tableau d'objets pièce jointe valides.</span><span class="sxs-lookup"><span data-stu-id="945e4-195">Array of valid attachment objects.</span></span> <span data-ttu-id="945e4-196">Utilisé pour les réponses de type `result` .</span><span class="sxs-lookup"><span data-stu-id="945e4-196">Used for responses of type `result`.</span></span> <br><span data-ttu-id="945e4-197">Actuellement, les types suivants sont pris en charge :</span><span class="sxs-lookup"><span data-stu-id="945e4-197">Currently the following types are supported:</span></span> <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|<span data-ttu-id="945e4-198">Actions suggérées.</span><span class="sxs-lookup"><span data-stu-id="945e4-198">Suggested actions.</span></span> <span data-ttu-id="945e4-199">Utilisé pour les réponses de type `auth` `config` ou .</span><span class="sxs-lookup"><span data-stu-id="945e4-199">Used for responses of type `auth` or `config`.</span></span> |
|`composeExtension.text`|<span data-ttu-id="945e4-200">Message à afficher.</span><span class="sxs-lookup"><span data-stu-id="945e4-200">Message to display.</span></span> <span data-ttu-id="945e4-201">Utilisé pour les réponses de type `message` .</span><span class="sxs-lookup"><span data-stu-id="945e4-201">Used for responses of type `message`.</span></span> |

#### <a name="response-card-types-and-previews"></a><span data-ttu-id="945e4-202">Types et aperçus de cartes de réponse</span><span class="sxs-lookup"><span data-stu-id="945e4-202">Response card types and previews</span></span>

<span data-ttu-id="945e4-203">Nous prise en charge les types de pièces jointes suivants :</span><span class="sxs-lookup"><span data-stu-id="945e4-203">We support the following attachment types:</span></span>

* [<span data-ttu-id="945e4-204">Carte miniature</span><span class="sxs-lookup"><span data-stu-id="945e4-204">Thumbnail card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [<span data-ttu-id="945e4-205">Carte Hero</span><span class="sxs-lookup"><span data-stu-id="945e4-205">Hero card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [<span data-ttu-id="945e4-206">Carte connecteur Office 365</span><span class="sxs-lookup"><span data-stu-id="945e4-206">Office 365 Connector card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [<span data-ttu-id="945e4-207">Carte adaptative</span><span class="sxs-lookup"><span data-stu-id="945e4-207">Adaptive card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

<span data-ttu-id="945e4-208">Voir [Cartes](~/task-modules-and-cards/what-are-cards.md) pour une vue d'ensemble.</span><span class="sxs-lookup"><span data-stu-id="945e4-208">See [Cards](~/task-modules-and-cards/what-are-cards.md) for an overview.</span></span>

<span data-ttu-id="945e4-209">Pour découvrir comment utiliser les types de carte miniature et hero, voir Ajouter des cartes et [des actions de carte.](~/task-modules-and-cards/cards/cards-actions.md)</span><span class="sxs-lookup"><span data-stu-id="945e4-209">To learn how to use the thumbnail and hero card types, see [Add cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

<span data-ttu-id="945e4-210">Pour obtenir une documentation supplémentaire concernant la carte de connecteur Office 365, voir Utilisation de cartes de connecteur [Office 365.](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)</span><span class="sxs-lookup"><span data-stu-id="945e4-210">For additional documentation regarding the Office 365 Connector card, see [Using Office 365 Connector cards](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span></span>

<span data-ttu-id="945e4-211">La liste des résultats s'affiche dans l'interface utilisateur de Microsoft Teams avec un aperçu de chaque élément.</span><span class="sxs-lookup"><span data-stu-id="945e4-211">The result list is displayed in the Microsoft Teams UI with a preview of each item.</span></span> <span data-ttu-id="945e4-212">L'aperçu est généré de deux manières :</span><span class="sxs-lookup"><span data-stu-id="945e4-212">The preview is generated in one of two ways:</span></span>

* <span data-ttu-id="945e4-213">Utilisation de la `preview` propriété dans `attachment` l'objet.</span><span class="sxs-lookup"><span data-stu-id="945e4-213">Using the `preview` property within the `attachment` object.</span></span> <span data-ttu-id="945e4-214">La pièce jointe peut uniquement être une carte hero ou `preview` miniature.</span><span class="sxs-lookup"><span data-stu-id="945e4-214">The `preview` attachment can only be a Hero or Thumbnail card.</span></span>
* <span data-ttu-id="945e4-215">Extrait de la base `title` et `text` des `image` propriétés de la pièce jointe.</span><span class="sxs-lookup"><span data-stu-id="945e4-215">Extracted from the basic `title`, `text`, and `image` properties of the attachment.</span></span> <span data-ttu-id="945e4-216">Elles sont utilisées uniquement si la `preview` propriété n'est pas définie et que ces propriétés sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="945e4-216">These are used only if the `preview` property is not set and these properties are available.</span></span>

<span data-ttu-id="945e4-217">Vous pouvez afficher un aperçu d'une carte de connecteur Adaptatif ou Office 365 dans la liste des résultats en définition de sa propriété d'aperçu . Cela n'est pas nécessaire si les résultats sont déjà des cartes hero ou miniatures.</span><span class="sxs-lookup"><span data-stu-id="945e4-217">You can display a preview of an Adaptive or Office 365 Connector card in the result list simply by setting its preview property; this is not necessary if the results are already hero or thumbnail cards.</span></span> <span data-ttu-id="945e4-218">Si vous utilisez la pièce jointe d'aperçu, il doit s'agit d'une carte Hero ou miniature.</span><span class="sxs-lookup"><span data-stu-id="945e4-218">If you use the preview attachment, it must be either a Hero or Thumbnail card.</span></span> <span data-ttu-id="945e4-219">Si aucune propriété d'aperçu n'est spécifiée, l'aperçu de la carte échoue et rien ne s'affiche.</span><span class="sxs-lookup"><span data-stu-id="945e4-219">If no preview property is specified, the preview of the card will fail and nothing will be displayed.</span></span>

#### <a name="response-example"></a><span data-ttu-id="945e4-220">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="945e4-220">Response example</span></span>

<span data-ttu-id="945e4-221">Cet exemple montre une réponse avec deux résultats, combinant différents formats de carte : connecteur Office 365 et adaptatif.</span><span class="sxs-lookup"><span data-stu-id="945e4-221">This example shows a response with two results, mixing different card formats: Office 365 Connector and Adaptive.</span></span> <span data-ttu-id="945e4-222">Bien que vous vouliez probablement vous en tenir à un seul format de carte dans votre réponse, il montre comment la propriété de chaque élément de la collection doit définir explicitement un aperçu au format Hero ou miniature, comme décrit `preview` `attachments` ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="945e4-222">While you'll likely want to stick with one card format in your response, it shows how the `preview` property of each element in the `attachments` collection must explicitly define a preview in hero or thumbnail format as described above.</span></span>

```json
{
  "composeExtension": {
    "type": "result",
    "attachmentLayout": "list",
    "attachments": [
      {
        "contentType": "application/vnd.microsoft.teams.card.o365connector",
        "content": {
          "sections": [
            {
              "activityTitle": "[85069]: Create a cool app",
              "activityImage&quot;: &quot;https://placekitten.com/200/200"
            },
            {
              "title": "Details",
              "facts": [
                {
                  "name": "Assigned to:",
                  "value&quot;: &quot;[Larry Brown](mailto:larryb@example.com)"
                },
                {
                  "name": "State:",
                  "value": "Active"
                }
              ]
            }
          ]
        },
        "preview": {
          "contentType": "application/vnd.microsoft.card.thumbnail",
          "content": {
            "title": "85069: Create a cool app",
            "images": [
              {
                "url": "https://placekitten.com/200/200"
              }
            ]
          }
        }
      },
      {
        "contentType": "application/vnd.microsoft.card.adaptive",
        "content": {
          "type": "AdaptiveCard",
          "body": [
            {
              "type": "Container",
              "items": [
                {
                  "type": "TextBlock",
                  "text": "Microsoft Corp (NASDAQ: MSFT)",
                  "size": "medium",
                  "isSubtle": true
                },
                {
                  "type": "TextBlock",
                  "text": "September 19, 4:00 PM EST",
                  "isSubtle": true
                }
              ]
            },
            {
              "type": "Container",
              "spacing": "none",
              "items": [
                {
                  "type": "ColumnSet",
                  "columns": [
                    {
                      "type": "Column",
                      "width": "stretch",
                      "items": [
                        {
                          "type": "TextBlock",
                          "text": "75.30",
                          "size": "extraLarge"
                        },
                        {
                          "type": "TextBlock",
                          "text": "▼ 0.20 (0.32%)",
                          "size": "small",
                          "color": "attention",
                          "spacing": "none"
                        }
                      ]
                    },
                    {
                      "type": "Column",
                      "width": "auto",
                      "items": [
                        {
                          "type": "FactSet",
                          "facts": [
                            {
                              "title": "Open",
                              "value": "62.24"
                            },
                            {
                              "title": "High",
                              "value": "62.98"
                            },
                            {
                              "title": "Low",
                              "value": "62.20"
                            }
                          ]
                        }
                      ]
                    }
                  ]
                }
              ]
            }
          ],
          "version": "1.0"
        },
        "preview": {
          "contentType": "application/vnd.microsoft.card.thumbnail",
          "content": {
            "title": "Microsoft Corp (NASDAQ: MSFT)",
            "text": "75.30 ▼ 0.20 (0.32%)"
          }
        }
      }
    ]
  }
}
```

### <a name="default-query"></a><span data-ttu-id="945e4-223">Requête par défaut</span><span class="sxs-lookup"><span data-stu-id="945e4-223">Default query</span></span>

<span data-ttu-id="945e4-224">Si vous la définissez dans le manifeste, Microsoft Teams publie une requête « par défaut » lorsque l'utilisateur ouvre l'extension de messagerie pour la `initialRun` `true` première fois.</span><span class="sxs-lookup"><span data-stu-id="945e4-224">If you set `initialRun` to `true` in the manifest, Microsoft Teams issues a "default" query when the user first opens the messaging extension.</span></span> <span data-ttu-id="945e4-225">Votre service peut répondre à cette requête avec un ensemble de résultats prérepliés.</span><span class="sxs-lookup"><span data-stu-id="945e4-225">Your service can respond to this query with a set of prepopulated results.</span></span> <span data-ttu-id="945e4-226">Cela peut être utile pour afficher, par exemple, les éléments récemment affichés, les favoris ou toute autre information qui ne dépend pas de l'entrée utilisateur.</span><span class="sxs-lookup"><span data-stu-id="945e4-226">This can be useful for displaying, for instance, recently viewed items, favorites, or any other information that is not dependent on user input.</span></span>

<span data-ttu-id="945e4-227">La requête par défaut a la même structure que n'importe quelle requête utilisateur normale, sauf avec un paramètre dont la `initialRun` valeur de chaîne est `true` .</span><span class="sxs-lookup"><span data-stu-id="945e4-227">The default query has the same structure as any regular user query, except with a parameter `initialRun` whose string value is `true`.</span></span>

#### <a name="request-example-for-a-default-query"></a><span data-ttu-id="945e4-228">Exemple de requête par défaut</span><span class="sxs-lookup"><span data-stu-id="945e4-228">Request example for a default query</span></span>

```json
{
  "type": "invoke",
  "name": "composeExtension/query",
  "value": {
    "commandId": "searchCmd",
    "parameters": [
      {
        "name": "initialRun",
        "value": "true"
      }
    ],
    "queryOptions": {
      "skip": 0,
      "count": 25
    }
  },
  ⋮
}
```

## <a name="identify-the-user"></a><span data-ttu-id="945e4-229">Identifier l'utilisateur</span><span class="sxs-lookup"><span data-stu-id="945e4-229">Identify the user</span></span>

<span data-ttu-id="945e4-230">Chaque demande à vos services inclut l'ID obscurci de l'utilisateur qui a effectué la demande, ainsi que le nom d'affichage de l'utilisateur et l'ID d'objet Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="945e4-230">Every request to your services includes the obfuscated ID of the user that performed the request, as well as the user's display name and Azure Active Directory object ID.</span></span>

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

<span data-ttu-id="945e4-231">Les `id` `aadObjectId` valeurs et les valeurs sont garanties pour être celle de l'utilisateur Teams authentifié.</span><span class="sxs-lookup"><span data-stu-id="945e4-231">The `id` and `aadObjectId` values are guaranteed to be that of the authenticated Teams user.</span></span> <span data-ttu-id="945e4-232">Ils peuvent être utilisés comme clés pour rechercher des informations d'identification ou tout état mis en cache dans votre service.</span><span class="sxs-lookup"><span data-stu-id="945e4-232">They can be used as keys to look up credentials or any cached state in your service.</span></span> <span data-ttu-id="945e4-233">En outre, chaque demande contient l'ID de client Azure Active Directory de l'utilisateur, qui peut être utilisé pour identifier l'organisation de l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="945e4-233">In addition, each request contains the Azure Active Directory tenant ID of the user, which can be used to identify the user’s organization.</span></span> <span data-ttu-id="945e4-234">Le cas échéant, la demande contient également les ID d'équipe et de canal d'où provient la demande.</span><span class="sxs-lookup"><span data-stu-id="945e4-234">If applicable, the request also contains the team and channel IDs from which the request originated.</span></span>

## <a name="authentication"></a><span data-ttu-id="945e4-235">Authentification</span><span class="sxs-lookup"><span data-stu-id="945e4-235">Authentication</span></span>

<span data-ttu-id="945e4-236">Si votre service requiert l'authentification de l'utilisateur, vous devez le signer avant de pouvoir utiliser l'extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="945e4-236">If your service requires user authentication, you need to sign in the user before he or she can use the messaging extension.</span></span> <span data-ttu-id="945e4-237">Si vous avez écrit un bot ou un onglet qui se signe dans l'utilisateur, cette section doit être familière.</span><span class="sxs-lookup"><span data-stu-id="945e4-237">If you have written a bot or a tab that signs in the user, this section should be familiar.</span></span>

<span data-ttu-id="945e4-238">La séquence est la suivante :</span><span class="sxs-lookup"><span data-stu-id="945e4-238">The sequence is as follows:</span></span>

1. <span data-ttu-id="945e4-239">Un utilisateur envoie une requête ou la requête par défaut est automatiquement envoyée à votre service.</span><span class="sxs-lookup"><span data-stu-id="945e4-239">User issues a query, or the default query is automatically sent to your service.</span></span>
2. <span data-ttu-id="945e4-240">Votre service vérifie si l'utilisateur s'est d'abord authentifié en inspectant l'ID d'utilisateur Teams.</span><span class="sxs-lookup"><span data-stu-id="945e4-240">Your service checks whether the user has first authenticated by inspecting the Teams user ID.</span></span>
3. <span data-ttu-id="945e4-241">Si l'utilisateur ne s'est pas authentifié, renvoyez une réponse avec une action suggérée, y compris `auth` `openUrl` l'URL d'authentification.</span><span class="sxs-lookup"><span data-stu-id="945e4-241">If the user has not authenticated, send back an `auth` response with an `openUrl` suggested action including the authentication URL.</span></span>
4. <span data-ttu-id="945e4-242">Le client Microsoft Teams lance une fenêtre pop-up hébergeant votre page web à l'aide de l'URL d'authentification donnée.</span><span class="sxs-lookup"><span data-stu-id="945e4-242">The Microsoft Teams client launches a pop-up window hosting your webpage using the given authentication URL.</span></span>
5. <span data-ttu-id="945e4-243">Une fois que l'utilisateur s'est signé, vous devez fermer votre fenêtre et envoyer un « code d'authentification » au client Teams.</span><span class="sxs-lookup"><span data-stu-id="945e4-243">After the user signs in, you should close your window and send an "authentication code" to the Teams client.</span></span>
6. <span data-ttu-id="945e4-244">Le client Teams ressue ensuite la requête à votre service, qui inclut le code d'authentification passé à l'étape 5.</span><span class="sxs-lookup"><span data-stu-id="945e4-244">The Teams client then reissues the query to your service, which includes the authentication code passed in step 5.</span></span>

<span data-ttu-id="945e4-245">Votre service doit vérifier que le code d'authentification reçu à l'étape 6 correspond à celui de l'étape 5.</span><span class="sxs-lookup"><span data-stu-id="945e4-245">Your service should verify that the authentication code received in step 6 matches the one from step 5.</span></span> <span data-ttu-id="945e4-246">Cela garantit qu'un utilisateur malveillant ne tente pas d'usurper ou de compromettre le flux de la signature.</span><span class="sxs-lookup"><span data-stu-id="945e4-246">This ensures that a malicious user does not try to spoof or compromise the sign-in flow.</span></span> <span data-ttu-id="945e4-247">Cela permet effectivement de « fermer la boucle » pour terminer la séquence d'authentification sécurisée.</span><span class="sxs-lookup"><span data-stu-id="945e4-247">This effectively "closes the loop" to finish the secure authentication sequence.</span></span>

### <a name="respond-with-a-sign-in-action"></a><span data-ttu-id="945e4-248">Répondre avec une action de se connectez</span><span class="sxs-lookup"><span data-stu-id="945e4-248">Respond with a sign-in action</span></span>

<span data-ttu-id="945e4-249">Pour inciter un utilisateur non authentifié à se connecter, répondez avec une action suggérée de type qui inclut `openUrl` l'URL d'authentification.</span><span class="sxs-lookup"><span data-stu-id="945e4-249">To prompt an unauthenticated user to sign in, respond with a suggested action of type `openUrl` that includes the authentication URL.</span></span>

#### <a name="response-example-for-a-sign-in-action"></a><span data-ttu-id="945e4-250">Exemple de réponse pour une action de sign-in</span><span class="sxs-lookup"><span data-stu-id="945e4-250">Response example for a sign-in action</span></span>

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
> <span data-ttu-id="945e4-251">Pour que l'expérience de se connecte soit hébergée dans une fenêtre pop-up Teams, la partie domaine de l'URL doit se trouver dans la liste des domaines valides de votre application.</span><span class="sxs-lookup"><span data-stu-id="945e4-251">For the sign-in experience to be hosted in a Teams pop-up, the domain portion of the URL must be in your app’s list of valid domains.</span></span> <span data-ttu-id="945e4-252">(Voir [validDomains](~/resources/schema/manifest-schema.md#validdomains) dans le schéma de manifeste.)</span><span class="sxs-lookup"><span data-stu-id="945e4-252">(See [validDomains](~/resources/schema/manifest-schema.md#validdomains) in the manifest schema.)</span></span>

### <a name="start-the-sign-in-flow"></a><span data-ttu-id="945e4-253">Démarrer le flux de la signature</span><span class="sxs-lookup"><span data-stu-id="945e4-253">Start the sign-in flow</span></span>

<span data-ttu-id="945e4-254">Votre expérience de sign-in doit être réactive et tenir dans une fenêtre popup.</span><span class="sxs-lookup"><span data-stu-id="945e4-254">Your sign-in experience should be responsive and fit within a popup window.</span></span> <span data-ttu-id="945e4-255">Il doit s'intégrer au [SDK client JavaScript Microsoft Teams,](/javascript/api/overview/msteams-client)qui utilise la transmission de message.</span><span class="sxs-lookup"><span data-stu-id="945e4-255">It should integrate with the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client), which uses message passing.</span></span>

<span data-ttu-id="945e4-256">Comme avec d'autres expériences incorporées en cours d'exécution dans Microsoft Teams, votre code à l'intérieur de la fenêtre doit d'abord `microsoftTeams.initialize()` appeler.</span><span class="sxs-lookup"><span data-stu-id="945e4-256">As with other embedded experiences running inside Microsoft Teams, your code inside the window needs to first call `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="945e4-257">Si votre code effectue un flux OAuth, vous pouvez passer l'ID utilisateur Teams dans votre fenêtre, qui peut ensuite le transmettre à l'URL de la signature OAuth.</span><span class="sxs-lookup"><span data-stu-id="945e4-257">If your code performs an OAuth flow, you can pass the Teams user ID into your window, which then can pass it to the OAuth sign-in URL.</span></span>

### <a name="complete-the-sign-in-flow"></a><span data-ttu-id="945e4-258">Terminer le flux de la signature</span><span class="sxs-lookup"><span data-stu-id="945e4-258">Complete the sign-in flow</span></span>

<span data-ttu-id="945e4-259">Lorsque la demande de se connecte est terminée et redirige vers votre page, elle doit effectuer les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="945e4-259">When the sign-in request completes and redirects back to your page, it should perform the following steps:</span></span>

1. <span data-ttu-id="945e4-260">Générer un code de sécurité.</span><span class="sxs-lookup"><span data-stu-id="945e4-260">Generate a security code.</span></span> <span data-ttu-id="945e4-261">(Il peut s'agit d'un nombre aléatoire.) Vous devez mettre en cache ce code sur votre service, ainsi que les informations d'identification obtenues via le flux de connexion (tels que les jetons OAuth 2.0).</span><span class="sxs-lookup"><span data-stu-id="945e4-261">(This can be a random number.) You need to cache this code on your service, along with the credentials obtained through the sign-in flow (such as OAuth 2.0 tokens).</span></span>
2. <span data-ttu-id="945e4-262">Appelez `microsoftTeams.authentication.notifySuccess` et passez le code de sécurité.</span><span class="sxs-lookup"><span data-stu-id="945e4-262">Call `microsoftTeams.authentication.notifySuccess` and pass the security code.</span></span>

<span data-ttu-id="945e4-263">À ce stade, la fenêtre se ferme et le contrôle est transmis au client Teams.</span><span class="sxs-lookup"><span data-stu-id="945e4-263">At this point, the window closes and control is passed to the Teams client.</span></span> <span data-ttu-id="945e4-264">Le client peut maintenant rééditer la requête utilisateur d'origine, ainsi que le code de sécurité dans la `state` propriété.</span><span class="sxs-lookup"><span data-stu-id="945e4-264">The client now can reissue the original user query, along with the security code in the `state` property.</span></span> <span data-ttu-id="945e4-265">Votre code peut utiliser le code de sécurité pour rechercher les informations d'identification stockées précédemment pour terminer la séquence d'authentification, puis effectuer la demande de l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="945e4-265">Your code can use the security code to look up the credentials stored earlier to complete the authentication sequence and then complete the user request.</span></span>

#### <a name="reissued-request-example"></a><span data-ttu-id="945e4-266">Exemple de requête rééditée</span><span class="sxs-lookup"><span data-stu-id="945e4-266">Reissued request example</span></span>

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
        "type": "clientInfo",
        "country": "US",
        "platform": "Web",
        
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

## <a name="sdk-support"></a><span data-ttu-id="945e4-267">Prise en charge du SDK</span><span class="sxs-lookup"><span data-stu-id="945e4-267">SDK support</span></span>

### <a name="net"></a><span data-ttu-id="945e4-268">.NET</span><span class="sxs-lookup"><span data-stu-id="945e4-268">.NET</span></span>

<span data-ttu-id="945e4-269">Pour recevoir et gérer des requêtes avec le SDK Bot Builder pour .NET, vous pouvez vérifier le type d'action sur l'activité entrante, puis utiliser la méthode d'aide dans le `invoke` package NuGet [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) pour déterminer s'il s'agit d'une activité d'extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="945e4-269">To receive and handle queries with the Bot Builder SDK for .NET, you can check for the `invoke` action type on the incoming activity and then use the helper method in the NuGet package [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) to determine whether it’s a messaging extension activity.</span></span>

#### <a name="example-code-in-net"></a><span data-ttu-id="945e4-270">Exemple de code dans .NET</span><span class="sxs-lookup"><span data-stu-id="945e4-270">Example code in .NET</span></span>

```csharp
public async Task<HttpResponseMessage> Post([FromBody]Activity activity)
{
    if (activity.Type == ActivityTypes.Invoke) // Received an invoke
    {
        if (activity.IsComposeExtensionQuery())
        {
            // This is the response object that will get sent back to the messaging extension request.
            ComposeExtensionResponse invokeResponse = null;

            // This helper method gets the query as an object.
            var query = activity.GetComposeExtensionQueryData();

            if (query.CommandId != null && query.Parameters != null && query.Parameters.Count > 0)
            {
                // query.Parameters has the parameters sent by client
                var results = new ComposeExtensionResult()
                {
                    AttachmentLayout = "list",
                    Type = "result",
                    Attachments = new List<ComposeExtensionAttachment>(),
                };
                invokeResponse.ComposeExtension = results;
            }

            // Return the response
            return Request.CreateResponse<ComposeExtensionResponse>(HttpStatusCode.OK, invokeResponse);
        } else
        {
            // Handle other types of Invoke activities here.
        }
    } else {
      // Failure case catch-all.
      var response = Request.CreateResponse(HttpStatusCode.BadRequest);
      response.Content = new StringContent("Invalid request! This API supports only messaging extension requests. Check your query and try again");
      return response;
    }
}
```

### <a name="nodejs"></a><span data-ttu-id="945e4-271">Node.js</span><span class="sxs-lookup"><span data-stu-id="945e4-271">Node.js</span></span>

#### <a name="example-code-in-nodejs"></a><span data-ttu-id="945e4-272">Exemple de code dans Node.js</span><span class="sxs-lookup"><span data-stu-id="945e4-272">Example code in Node.js</span></span>

```javascript
require('dotenv').config();

import * as restify from 'restify';
import * as builder from 'botbuilder';
import * as teamBuilder from 'botbuilder-teams';

class App {
    run() {
        const server = restify.createServer();
        let teamChatConnector = new teamBuilder.TeamsChatConnector({
            appId: process.env.MICROSOFT_APP_ID,
            appPassword: process.env.MICROSOFT_APP_PASSWORD
        });

        // Command ID must match what's defined in manifest
        teamChatConnector.onQuery('<%= commandId %>',
            (event: builder.IEvent,
            query: teamBuilder.ComposeExtensionQuery,
            callback: (err: Error, result: teamBuilder.IComposeExtensionResponse, statusCode: number) => void) => {
                // Check for initialRun; i.e., when you should return default results
                // if (query.parameters[0].name === 'initialRun') {}

                // Check query.queryOptions.count and query.queryOptions.skip for paging

                // Return auth response
                // let response = teamBuilder.ComposeExtensionResponse.auth().actions([
                //     builder.CardAction.openUrl(null, 'https://authUrl', 'Please sign in')
                // ]).toResponse();

                // Return config response
                // let response = teamBuilder.ComposeExtensionResponse.config().actions([
                //     builder.CardAction.openUrl(null, 'https://configUrl', 'Please sign in')
                // ]).toResponse();

                // Return result response
                let response = teamBuilder.ComposeExtensionResponse.result('list').attachments([
                    new builder.ThumbnailCard()
                        .title('Test thumbnail card')
                        .text('This is a test thumbnail card')
                        .images([new builder.CardImage().url('https://bot-framework.azureedge.net/bot-icons-v1/bot-framework-default-9.png')])
                        .toAttachment()
                ]).toResponse();
                callback(null, response, 200);
            });
        server.post('/api/composeExtension', teamChatConnector.listen());
        server.listen(process.env.PORT, () => console.log(`listening to port:` + process.env.PORT));
    }
}

const app = new App();
app.run();
```
<span data-ttu-id="945e4-273">*Voir aussi des* [exemples Bot Framework.](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)</span><span class="sxs-lookup"><span data-stu-id="945e4-273">*See also* [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>
