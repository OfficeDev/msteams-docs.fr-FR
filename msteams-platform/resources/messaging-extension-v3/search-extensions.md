---
title: Rechercher avec des extensions de messagerie
description: Décrit comment développer des extensions de messagerie basées sur la recherche
keywords: équipes de messagerie extensions de recherche d’extensions de messagerie
ms.topic: how-to
localization_priority: Normal
ms.date: 07/20/2019
ms.openlocfilehash: 515472838ff2ad35ef5dd295043ec27c53edb4f1
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566728"
---
# <a name="search-with-messaging-extensions"></a><span data-ttu-id="0da9b-104">Rechercher avec des extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="0da9b-104">Search with messaging extensions</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

<span data-ttu-id="0da9b-105">Les extensions de messagerie basées sur la recherche vous permettent d’interroger votre service et de publier ces informations sous la forme d’une carte, directement dans votre message.</span><span class="sxs-lookup"><span data-stu-id="0da9b-105">Search based messaging extensions allow you to query your service and post that information in the form of a card, right into your message.</span></span>

![Exemple de carte d’extension de messagerie](~/assets/images/compose-extensions/ceexample.png)

<span data-ttu-id="0da9b-107">Les sections suivantes décrivent comment le faire :</span><span class="sxs-lookup"><span data-stu-id="0da9b-107">The following sections describe how to do this:</span></span>

[!include[common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

### <a name="search-type-message-extensions"></a><span data-ttu-id="0da9b-108">Extensions de message de type recherche</span><span class="sxs-lookup"><span data-stu-id="0da9b-108">Search type message extensions</span></span>

<span data-ttu-id="0da9b-109">Pour l’extension de messagerie basée sur la recherche définir `type` le paramètre à `query` .</span><span class="sxs-lookup"><span data-stu-id="0da9b-109">For search based messaging extension set the `type` parameter to `query`.</span></span> <span data-ttu-id="0da9b-110">Voici un exemple d’un manifeste avec une seule commande de recherche.</span><span class="sxs-lookup"><span data-stu-id="0da9b-110">Below is an example of a manifest with a single search command.</span></span> <span data-ttu-id="0da9b-111">Une seule extension de messagerie peut avoir jusqu’à 10 commandes différentes qui lui sont associées.</span><span class="sxs-lookup"><span data-stu-id="0da9b-111">A single messaging extension can have up to 10 different commands associated with it.</span></span> <span data-ttu-id="0da9b-112">Cela peut inclure à la fois plusieurs recherches et plusieurs commandes basées sur l’action.</span><span class="sxs-lookup"><span data-stu-id="0da9b-112">This can include both multiple search and multiple Action-based commands.</span></span>

#### <a name="complete-app-manifest-example"></a><span data-ttu-id="0da9b-113">Exemple complet de manifeste d’application</span><span class="sxs-lookup"><span data-stu-id="0da9b-113">Complete app manifest example</span></span>

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

### <a name="test-via-uploading"></a><span data-ttu-id="0da9b-114">Test via le téléchargement</span><span class="sxs-lookup"><span data-stu-id="0da9b-114">Test via uploading</span></span>

<span data-ttu-id="0da9b-115">Vous pouvez tester votre extension de messagerie en téléchargeant votre application.</span><span class="sxs-lookup"><span data-stu-id="0da9b-115">You can test your messaging extension by uploading your app.</span></span>

<span data-ttu-id="0da9b-116">Pour ouvrir votre extension de messagerie, accédez à l’un de vos chats ou canaux.</span><span class="sxs-lookup"><span data-stu-id="0da9b-116">To open your messaging extension, navigate to any of your chats or channels.</span></span> <span data-ttu-id="0da9b-117">Choisissez le **bouton Plus d’options** **(&#8943;)** dans la boîte de composition, et choisissez votre extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="0da9b-117">Choose the **More options** (**&#8943;**) button in the compose box, and choose your messaging extension.</span></span>

## <a name="add-event-handlers"></a><span data-ttu-id="0da9b-118">Ajouter des gestionnaires d’événements</span><span class="sxs-lookup"><span data-stu-id="0da9b-118">Add event handlers</span></span>

<span data-ttu-id="0da9b-119">La plupart de votre travail implique `onQuery` l’événement, qui gère toutes les interactions dans la fenêtre d’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="0da9b-119">Most of your work involves the `onQuery` event, which handles all interactions in the messaging extension window.</span></span>

<span data-ttu-id="0da9b-120">Si vous `canUpdateConfiguration` définissez `true` dans le manifeste, vous activez **l’élément de** menu Paramètres pour votre extension de messagerie et devez également gérer et `onQuerySettingsUrl` `onSettingsUpdate` .</span><span class="sxs-lookup"><span data-stu-id="0da9b-120">If you set `canUpdateConfiguration` to `true` in the manifest, you enable the **Settings** menu item for your messaging extension and must also handle `onQuerySettingsUrl` and `onSettingsUpdate`.</span></span>

### <a name="handle-onquery-events"></a><span data-ttu-id="0da9b-121">Gérer les événements deQuery</span><span class="sxs-lookup"><span data-stu-id="0da9b-121">Handle onQuery events</span></span>

<span data-ttu-id="0da9b-122">Une extension de messagerie reçoit un `onQuery` événement lorsque quelque chose se passe dans la fenêtre d’extension de messagerie ou est envoyé à la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="0da9b-122">A messaging extension receives an `onQuery` event when anything happens in the messaging extension window or is sent to the window.</span></span>

<span data-ttu-id="0da9b-123">Si votre extension de messagerie utilise une page de configuration, votre gestionnaire doit `onQuery` d’abord vérifier les informations de configuration stockées; si l’extension de messagerie n’est pas configurée, retournez `config` une réponse avec un lien vers votre page de configuration.</span><span class="sxs-lookup"><span data-stu-id="0da9b-123">If your messaging extension uses a configuration page, your handler for `onQuery` should first check for any stored configuration information; if the messaging extension isn't configured, return a `config` response with a link to your configuration page.</span></span> <span data-ttu-id="0da9b-124">Sachez que la réponse de la page de configuration est également gérée par `onQuery` .</span><span class="sxs-lookup"><span data-stu-id="0da9b-124">Be aware that the response from the configuration page is also handled by `onQuery`.</span></span> <span data-ttu-id="0da9b-125">La seule exception est lorsque la page de configuration est appelée par le gestionnaire pour `onQuerySettingsUrl` ; voir la section suivante:</span><span class="sxs-lookup"><span data-stu-id="0da9b-125">The sole exception is when the configuration page is called by the handler for `onQuerySettingsUrl`; see the following section:</span></span>

<span data-ttu-id="0da9b-126">Si votre extension de messagerie nécessite une authentification, vérifiez les informations de l’état de l’utilisateur; si l’utilisateur n’est pas connecté, suivez les instructions dans la section [Authentification](#authentication) plus tard dans ce sujet.</span><span class="sxs-lookup"><span data-stu-id="0da9b-126">If your messaging extension requires authentication, check the user state information; if the user isn't signed in, follow the instructions in the [Authentication](#authentication) section later in this topic.</span></span>

<span data-ttu-id="0da9b-127">Ensuite, vérifiez si `initialRun` c’est défini; le cas échéant, prenez les mesures appropriées, comme fournir des instructions ou une liste de réponses.</span><span class="sxs-lookup"><span data-stu-id="0da9b-127">Next, check whether `initialRun` is set; if so, take appropriate action, such as providing instructions or a list of responses.</span></span>

<span data-ttu-id="0da9b-128">Le reste de votre gestionnaire pour les invite `onQuery` à l’utilisateur pour des informations, affiche une liste de cartes de prévisualisation, et renvoie la carte sélectionnée par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0da9b-128">The remainder of your handler for `onQuery` prompts the user for information, displays a list of preview cards, and returns the card selected by the user.</span></span>

### <a name="handle-onquerysettingsurl-and-onsettingsupdate-events"></a><span data-ttu-id="0da9b-129">Gérer les événementsQuerySettingsUrl et onSettingsUpdate</span><span class="sxs-lookup"><span data-stu-id="0da9b-129">Handle onQuerySettingsUrl and onSettingsUpdate events</span></span>

<span data-ttu-id="0da9b-130">Les `onQuerySettingsUrl` événements et les événements travaillent ensemble pour permettre à `onSettingsUpdate` **l’Paramètres de** menu.</span><span class="sxs-lookup"><span data-stu-id="0da9b-130">The `onQuerySettingsUrl` and `onSettingsUpdate` events work together to enable the **Settings** menu item.</span></span>

![Captures d’écran des emplacements Paramètres menu de l’article](~/assets/images/compose-extensions/compose-extension-settings-menu-item.png)

<span data-ttu-id="0da9b-132">Votre gestionnaire pour `onQuerySettingsUrl` renvoie l’URL de la page de configuration; après la fermeture de la page de configuration, votre gestionnaire `onSettingsUpdate` accepte et enregistre l’état retourné.</span><span class="sxs-lookup"><span data-stu-id="0da9b-132">Your handler for `onQuerySettingsUrl` returns the URL for the configuration page; after the configuration page closes, your handler for `onSettingsUpdate` accepts and saves the returned state.</span></span> <span data-ttu-id="0da9b-133">C’est le seul cas dans `onQuery` *lequel ne reçoit pas* la réponse de la page de configuration.</span><span class="sxs-lookup"><span data-stu-id="0da9b-133">This is the one case in which `onQuery` *doesn't* receive the response from the configuration page.</span></span>

## <a name="receive-and-respond-to-queries"></a><span data-ttu-id="0da9b-134">Recevoir et répondre aux requêtes</span><span class="sxs-lookup"><span data-stu-id="0da9b-134">Receive and respond to queries</span></span>

<span data-ttu-id="0da9b-135">Chaque demande à votre extension de messagerie se fait via `Activity` un objet qui est affiché sur votre URL de rappel.</span><span class="sxs-lookup"><span data-stu-id="0da9b-135">Every request to your messaging extension is done via an `Activity` object that is posted to your callback URL.</span></span> <span data-ttu-id="0da9b-136">La demande contient des informations sur la commande utilisateur, telles que les valeurs d’identification et de paramètres.</span><span class="sxs-lookup"><span data-stu-id="0da9b-136">The request contains information about the user command, such as ID and parameter values.</span></span> <span data-ttu-id="0da9b-137">La demande fournit également des métadonnées sur le contexte dans lequel votre extension a été invoquée, y compris l’identification de l’utilisateur et du locataire, ainsi que l’id de chat ou les identifiants de chaîne et d’équipe.</span><span class="sxs-lookup"><span data-stu-id="0da9b-137">The request also supplies metadata about the context in which your extension was invoked, including user and tenant ID, along with chat ID or channel and team IDs.</span></span>

### <a name="receive-user-requests"></a><span data-ttu-id="0da9b-138">Recevoir les demandes des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="0da9b-138">Receive user requests</span></span>

<span data-ttu-id="0da9b-139">Lorsqu’un utilisateur effectue une requête, Microsoft Teams envoie à votre service un objet Bot Framework `Activity` standard.</span><span class="sxs-lookup"><span data-stu-id="0da9b-139">When a user performs a query, Microsoft Teams sends your service a standard Bot Framework `Activity` object.</span></span> <span data-ttu-id="0da9b-140">Votre service doit exécuter sa logique pour un qui a `Activity` défini et mis à un type pris en `type` `invoke` `name` `composeExtension` charge, comme indiqué dans le tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="0da9b-140">Your service should perform its logic for an `Activity` that has `type` set to `invoke` and `name` set to a supported `composeExtension` type, as shown in the following table.</span></span>

<span data-ttu-id="0da9b-141">En plus des propriétés d’activité bot standard, la charge utile contient les métadonnées de demande suivantes :</span><span class="sxs-lookup"><span data-stu-id="0da9b-141">In addition to the standard bot activity properties, the payload contains the following request metadata:</span></span>

|<span data-ttu-id="0da9b-142">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="0da9b-142">Property name</span></span>|<span data-ttu-id="0da9b-143">Objectif</span><span class="sxs-lookup"><span data-stu-id="0da9b-143">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="0da9b-144">Type de demande; doit être `invoke` .</span><span class="sxs-lookup"><span data-stu-id="0da9b-144">Type of request; must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="0da9b-145">Type de commande qui est délivré à votre service.</span><span class="sxs-lookup"><span data-stu-id="0da9b-145">Type of command that is issued to your service.</span></span> <span data-ttu-id="0da9b-146">Actuellement, les types suivants sont pris en charge :</span><span class="sxs-lookup"><span data-stu-id="0da9b-146">Currently the following types are supported:</span></span> <br>`composeExtension/query` <br>`composeExtension/querySettingUrl` <br>`composeExtension/setting` <br>`composeExtension/selectItem` <br>`composeExtension/queryLink` |
|`from.id`| <span data-ttu-id="0da9b-147">ID de l’utilisateur qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="0da9b-147">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="0da9b-148">Nom de l’utilisateur qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="0da9b-148">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="0da9b-149">Azure Active Directory id objet de l’utilisateur qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="0da9b-149">Azure Active Directory object id of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="0da9b-150">ID du client Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0da9b-150">Azure Active Directory tenant ID.</span></span> |
|`channelData.channel.id`| <span data-ttu-id="0da9b-151">ID de canal (si la demande a été faite dans un canal).</span><span class="sxs-lookup"><span data-stu-id="0da9b-151">Channel ID (if the request was made in a channel).</span></span> |
|`channelData.team.id`| <span data-ttu-id="0da9b-152">ID d’équipe (si la demande a été faite dans un canal).</span><span class="sxs-lookup"><span data-stu-id="0da9b-152">Team ID (if the request was made in a channel).</span></span> |
|`clientInfo`|<span data-ttu-id="0da9b-153">Métadonnées optionnelles sur le logiciel client utilisé pour envoyer le message d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0da9b-153">Optional metadata about the client software used to send a user's message.</span></span> <span data-ttu-id="0da9b-154">L’entité peut contenir deux propriétés :</span><span class="sxs-lookup"><span data-stu-id="0da9b-154">The entity can contain two properties:</span></span><br><span data-ttu-id="0da9b-155">Le `country` champ contient l’emplacement détecté par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0da9b-155">The `country` field contains the user's detected location.</span></span><br><span data-ttu-id="0da9b-156">Le `platform` champ décrit la plate-forme client de messagerie.</span><span class="sxs-lookup"><span data-stu-id="0da9b-156">The `platform` field describes the messaging client platform.</span></span> <br><span data-ttu-id="0da9b-157">Pour plus d’informations, *veuillez consulter* [les types d’entités non IRI — clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo).</span><span class="sxs-lookup"><span data-stu-id="0da9b-157">For additional information, please *see* [Non-IRI entity types — clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo).</span></span>|

<span data-ttu-id="0da9b-158">Les paramètres de demande eux-mêmes se trouvent dans l’objet de valeur, qui comprend les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="0da9b-158">The request parameters itself are found in the value object, which includes the following properties:</span></span>

| <span data-ttu-id="0da9b-159">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="0da9b-159">Property name</span></span> | <span data-ttu-id="0da9b-160">Objectif</span><span class="sxs-lookup"><span data-stu-id="0da9b-160">Purpose</span></span> |
|---|---|
| `commandId` | <span data-ttu-id="0da9b-161">Le nom de la commande invoquée par l’utilisateur, correspondant à l’une des commandes déclarées dans le manifeste de l’application.</span><span class="sxs-lookup"><span data-stu-id="0da9b-161">The name of the command invoked by the user, matching one of the commands declared in the app manifest.</span></span> |
| `parameters` | <span data-ttu-id="0da9b-162">Tableau des paramètres : Chaque objet paramètre contient le nom du paramètre, ainsi que la valeur de paramètre fournie par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0da9b-162">Array of parameters: Each parameter object contains the parameter name, along with the parameter value provided by the user.</span></span> |
| `queryOptions` | <span data-ttu-id="0da9b-163">Paramètres de pagination :</span><span class="sxs-lookup"><span data-stu-id="0da9b-163">Pagination parameters:</span></span> <br><span data-ttu-id="0da9b-164">`skip`: ignorer le nombre de requêtes</span><span class="sxs-lookup"><span data-stu-id="0da9b-164">`skip`: skip count for this query</span></span> <br><span data-ttu-id="0da9b-165">`count`: nombre d’éléments à retourner</span><span class="sxs-lookup"><span data-stu-id="0da9b-165">`count`: number of elements to return</span></span> |

#### <a name="request-example"></a><span data-ttu-id="0da9b-166">Exemple de requête</span><span class="sxs-lookup"><span data-stu-id="0da9b-166">Request example</span></span>

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

### <a name="receive-requests-from-links-inserted-into-the-compose-message-box"></a><span data-ttu-id="0da9b-167">Recevoir les demandes des liens insérés dans la boîte à messages de composition</span><span class="sxs-lookup"><span data-stu-id="0da9b-167">Receive requests from links inserted into the compose message box</span></span>

<span data-ttu-id="0da9b-168">Comme alternative (ou en outre) à la recherche de votre service externe, vous pouvez utiliser une URL insérée dans la boîte de messages de composition pour interroger votre service et retourner une carte.</span><span class="sxs-lookup"><span data-stu-id="0da9b-168">As an alternative (or in addition) to searching your external service, you can use a URL inserted into the compose message box to query your service and return a card.</span></span> <span data-ttu-id="0da9b-169">Dans la capture d’écran ci-dessous, un utilisateur a passé dans une URL pour un élément de travail en Azure DevOps que l’extension de messagerie a résolu dans une carte.</span><span class="sxs-lookup"><span data-stu-id="0da9b-169">In the screenshot below a user has pasted in a URL for a work item in Azure DevOps which the messaging extension has resolved into a card.</span></span>

![Exemple de déploiement de liens](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

<span data-ttu-id="0da9b-171">Pour permettre à votre extension de messagerie d’interagir avec les liens de cette façon, vous devrez d’abord ajouter `messageHandlers` le tableau à votre manifeste d’application comme dans l’exemple ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="0da9b-171">To enable your messaging extension to interact with links this way you'll first need to add the `messageHandlers` array to your app manifest as in the example below:</span></span>

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

<span data-ttu-id="0da9b-172">Une fois que vous avez ajouté le domaine pour écouter le manifeste de [](#respond-to-user-requests) l’application, vous devrez modifier votre code bot pour répondre à la demande d’invocateur ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="0da9b-172">Once you've added the domain to listen on to the app manifest, you'll need to change your bot code to [respond](#respond-to-user-requests) to the below invoke request.</span></span>

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

<span data-ttu-id="0da9b-173">Si votre application renvoie plusieurs éléments, seul le premier sera utilisé.</span><span class="sxs-lookup"><span data-stu-id="0da9b-173">If your app returns multiple items only the first will be used.</span></span>

### <a name="respond-to-user-requests"></a><span data-ttu-id="0da9b-174">Répondre aux demandes des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="0da9b-174">Respond to user requests</span></span>

<span data-ttu-id="0da9b-175">Lorsque l’utilisateur effectue une requête, Microsoft Teams émet une demande HTTP synchrone à votre service.</span><span class="sxs-lookup"><span data-stu-id="0da9b-175">When the user performs a query, Microsoft Teams issues a synchronous HTTP request to your service.</span></span> <span data-ttu-id="0da9b-176">À ce stade, votre code dispose de 5 secondes pour fournir une réponse HTTP à la demande.</span><span class="sxs-lookup"><span data-stu-id="0da9b-176">At that point, your code has 5 seconds to provide an HTTP response to the request.</span></span> <span data-ttu-id="0da9b-177">Pendant ce temps, votre service peut effectuer des recherchez supplémentaires, ou toute autre logique d’entreprise nécessaire pour répondre à la demande.</span><span class="sxs-lookup"><span data-stu-id="0da9b-177">During this time, your service can perform additional lookup, or any other business logic needed to serve the request.</span></span>

<span data-ttu-id="0da9b-178">Votre service doit répondre avec les résultats correspondant à la requête utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0da9b-178">Your service should respond with the results matching the user query.</span></span> <span data-ttu-id="0da9b-179">La réponse doit indiquer un code d’état HTTP `200 OK` et un objet d’application/json valide avec l’organisme suivant :</span><span class="sxs-lookup"><span data-stu-id="0da9b-179">The response must indicate an HTTP status code of `200 OK` and a valid application/json object with the following body:</span></span>

|<span data-ttu-id="0da9b-180">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="0da9b-180">Property name</span></span>|<span data-ttu-id="0da9b-181">Objectif</span><span class="sxs-lookup"><span data-stu-id="0da9b-181">Purpose</span></span>|
|---|---|
|`composeExtension`|<span data-ttu-id="0da9b-182">Enveloppe de réponse de haut niveau.</span><span class="sxs-lookup"><span data-stu-id="0da9b-182">Top-level response envelope.</span></span>|
|`composeExtension.type`|<span data-ttu-id="0da9b-183">Type de réponse.</span><span class="sxs-lookup"><span data-stu-id="0da9b-183">Type of response.</span></span> <span data-ttu-id="0da9b-184">Les types suivants sont pris en charge :</span><span class="sxs-lookup"><span data-stu-id="0da9b-184">The following types are supported:</span></span> <br><span data-ttu-id="0da9b-185">`result`: affiche une liste de résultats de recherche</span><span class="sxs-lookup"><span data-stu-id="0da9b-185">`result`: displays a list of search results</span></span> <br><span data-ttu-id="0da9b-186">`auth`: demande à l’utilisateur de s’authentifier</span><span class="sxs-lookup"><span data-stu-id="0da9b-186">`auth`: asks the user to authenticate</span></span> <br><span data-ttu-id="0da9b-187">`config`: demande à l’utilisateur de configurer l’extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="0da9b-187">`config`: asks the user to set up the messaging extension</span></span> <br><span data-ttu-id="0da9b-188">`message` : affiche un message en texte brut.</span><span class="sxs-lookup"><span data-stu-id="0da9b-188">`message`: displays a plain text message</span></span> |
|`composeExtension.attachmentLayout`|<span data-ttu-id="0da9b-189">Spécifie la disposition des pièces jointes.</span><span class="sxs-lookup"><span data-stu-id="0da9b-189">Specifies the layout of the attachments.</span></span> <span data-ttu-id="0da9b-190">Utilisé pour les réponses de type `result` .</span><span class="sxs-lookup"><span data-stu-id="0da9b-190">Used for responses of type `result`.</span></span> <br><span data-ttu-id="0da9b-191">Actuellement, les types suivants sont pris en charge :</span><span class="sxs-lookup"><span data-stu-id="0da9b-191">Currently the following types are supported:</span></span> <br><span data-ttu-id="0da9b-192">`list`: une liste d’objets de cartes contenant des champs de vignette, de titre et de texte</span><span class="sxs-lookup"><span data-stu-id="0da9b-192">`list`: a list of card objects containing thumbnail, title, and text fields</span></span> <br><span data-ttu-id="0da9b-193">`grid`: une grille d’images miniatures</span><span class="sxs-lookup"><span data-stu-id="0da9b-193">`grid`: a grid of thumbnail images</span></span> |
|`composeExtension.attachments`|<span data-ttu-id="0da9b-194">Tableau d’objets de pièce jointe valides.</span><span class="sxs-lookup"><span data-stu-id="0da9b-194">Array of valid attachment objects.</span></span> <span data-ttu-id="0da9b-195">Utilisé pour les réponses de type `result` .</span><span class="sxs-lookup"><span data-stu-id="0da9b-195">Used for responses of type `result`.</span></span> <br><span data-ttu-id="0da9b-196">Actuellement, les types suivants sont pris en charge :</span><span class="sxs-lookup"><span data-stu-id="0da9b-196">Currently the following types are supported:</span></span> <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|<span data-ttu-id="0da9b-197">Actions suggérées.</span><span class="sxs-lookup"><span data-stu-id="0da9b-197">Suggested actions.</span></span> <span data-ttu-id="0da9b-198">Utilisé pour les réponses de type `auth` ou `config` .</span><span class="sxs-lookup"><span data-stu-id="0da9b-198">Used for responses of type `auth` or `config`.</span></span> |
|`composeExtension.text`|<span data-ttu-id="0da9b-199">Message à afficher.</span><span class="sxs-lookup"><span data-stu-id="0da9b-199">Message to display.</span></span> <span data-ttu-id="0da9b-200">Utilisé pour les réponses de type `message` .</span><span class="sxs-lookup"><span data-stu-id="0da9b-200">Used for responses of type `message`.</span></span> |

#### <a name="response-card-types-and-previews"></a><span data-ttu-id="0da9b-201">Types de cartes de réponse et aperçus</span><span class="sxs-lookup"><span data-stu-id="0da9b-201">Response card types and previews</span></span>

<span data-ttu-id="0da9b-202">Nous prenons en charge les types de pièces jointes suivants :</span><span class="sxs-lookup"><span data-stu-id="0da9b-202">We support the following attachment types:</span></span>

* [<span data-ttu-id="0da9b-203">Carte miniature</span><span class="sxs-lookup"><span data-stu-id="0da9b-203">Thumbnail card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [<span data-ttu-id="0da9b-204">Carte de héros</span><span class="sxs-lookup"><span data-stu-id="0da9b-204">Hero card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [<span data-ttu-id="0da9b-205">Office 365 Carte connecteur</span><span class="sxs-lookup"><span data-stu-id="0da9b-205">Office 365 Connector card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [<span data-ttu-id="0da9b-206">Carte adaptative</span><span class="sxs-lookup"><span data-stu-id="0da9b-206">Adaptive card</span></span>](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

<span data-ttu-id="0da9b-207">Pour plus d’informations, consultez [Cartes pour](~/task-modules-and-cards/what-are-cards.md) un aperçu.</span><span class="sxs-lookup"><span data-stu-id="0da9b-207">For more information, see [Cards](~/task-modules-and-cards/what-are-cards.md) for an overview.</span></span>

<span data-ttu-id="0da9b-208">Pour apprendre à utiliser les types de vignettes et de cartes héros, voir Ajouter [des cartes et des actions de carte](~/task-modules-and-cards/cards/cards-actions.md).</span><span class="sxs-lookup"><span data-stu-id="0da9b-208">To learn how to use the thumbnail and hero card types, see [Add cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

<span data-ttu-id="0da9b-209">Pour plus de documentation concernant la carte connecteur Office 365, voir Utilisation [Office 365 cartes Connecteur](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span><span class="sxs-lookup"><span data-stu-id="0da9b-209">For additional documentation regarding the Office 365 Connector card, see [Using Office 365 Connector cards](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).</span></span>

<span data-ttu-id="0da9b-210">La liste des résultats est affichée dans l’interface Microsoft Teams’interface utilisateur avec un aperçu de chaque élément.</span><span class="sxs-lookup"><span data-stu-id="0da9b-210">The result list is displayed in the Microsoft Teams UI with a preview of each item.</span></span> <span data-ttu-id="0da9b-211">L’aperçu est généré de deux façons :</span><span class="sxs-lookup"><span data-stu-id="0da9b-211">The preview is generated in one of two ways:</span></span>

* <span data-ttu-id="0da9b-212">Utilisation de la `preview` propriété dans `attachment` l’objet.</span><span class="sxs-lookup"><span data-stu-id="0da9b-212">Using the `preview` property within the `attachment` object.</span></span> <span data-ttu-id="0da9b-213">La `preview` pièce jointe ne peut être qu’une carte Héros ou Vignette.</span><span class="sxs-lookup"><span data-stu-id="0da9b-213">The `preview` attachment can only be a Hero or Thumbnail card.</span></span>
* <span data-ttu-id="0da9b-214">Extrait de la base `title` , et les propriétés de la pièce `text` `image` jointe.</span><span class="sxs-lookup"><span data-stu-id="0da9b-214">Extracted from the basic `title`, `text`, and `image` properties of the attachment.</span></span> <span data-ttu-id="0da9b-215">Ceux-ci ne sont utilisés que si `preview` la propriété n’est pas définie et que ces propriétés sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="0da9b-215">These are used only if the `preview` property is not set and these properties are available.</span></span>

<span data-ttu-id="0da9b-216">Vous pouvez afficher un aperçu d’une carte Connecteur adaptative ou Office 365 dans la liste des résultats simplement en paramètre sa propriété d’aperçu; ce n’est pas nécessaire si les résultats sont déjà des cartes héros ou miniatures.</span><span class="sxs-lookup"><span data-stu-id="0da9b-216">You can display a preview of an Adaptive or Office 365 Connector card in the result list simply by setting its preview property; this is not necessary if the results are already hero or thumbnail cards.</span></span> <span data-ttu-id="0da9b-217">Si vous utilisez la pièce jointe d’aperçu, il doit s’agir d’une carte Héros ou Vignette.</span><span class="sxs-lookup"><span data-stu-id="0da9b-217">If you use the preview attachment, it must be either a Hero or Thumbnail card.</span></span> <span data-ttu-id="0da9b-218">Si aucune propriété d’aperçu n’est spécifiée, l’aperçu de la carte échouera et rien ne sera affiché.</span><span class="sxs-lookup"><span data-stu-id="0da9b-218">If no preview property is specified, the preview of the card will fail and nothing will be displayed.</span></span>

#### <a name="response-example"></a><span data-ttu-id="0da9b-219">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="0da9b-219">Response example</span></span>

<span data-ttu-id="0da9b-220">Cet exemple montre une réponse avec deux résultats, mélangeant différents formats de cartes : Office 365 Connecteur et Adaptatif.</span><span class="sxs-lookup"><span data-stu-id="0da9b-220">This example shows a response with two results, mixing different card formats: Office 365 Connector and Adaptive.</span></span> <span data-ttu-id="0da9b-221">Bien que vous voudrez probablement rester avec un format de carte dans votre réponse, il montre comment la `preview` propriété de chaque élément de la collection doit définir explicitement un aperçu en format héros ou vignette comme `attachments` décrit ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="0da9b-221">While you'll likely want to stick with one card format in your response, it shows how the `preview` property of each element in the `attachments` collection must explicitly define a preview in hero or thumbnail format as described above.</span></span>

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

### <a name="default-query"></a><span data-ttu-id="0da9b-222">Requête par défaut</span><span class="sxs-lookup"><span data-stu-id="0da9b-222">Default query</span></span>

<span data-ttu-id="0da9b-223">Si vous définissez `initialRun` `true` dans le manifeste, vous Microsoft Teams une requête « par défaut » lorsque l’utilisateur ouvre pour la première fois l’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="0da9b-223">If you set `initialRun` to `true` in the manifest, Microsoft Teams issues a "default" query when the user first opens the messaging extension.</span></span> <span data-ttu-id="0da9b-224">Votre service peut répondre à cette requête avec un ensemble de résultats prépeuplés.</span><span class="sxs-lookup"><span data-stu-id="0da9b-224">Your service can respond to this query with a set of prepopulated results.</span></span> <span data-ttu-id="0da9b-225">Cela peut être utile pour afficher, par exemple, des éléments, des favoris ou toute autre information qui ne dépend pas de l’entrée de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0da9b-225">This can be useful for displaying, for instance, recently viewed items, favorites, or any other information that is not dependent on user input.</span></span>

<span data-ttu-id="0da9b-226">La requête par défaut a la même structure que n’importe quelle requête utilisateur régulière, sauf avec un paramètre dont `initialRun` la valeur de chaîne est `true` .</span><span class="sxs-lookup"><span data-stu-id="0da9b-226">The default query has the same structure as any regular user query, except with a parameter `initialRun` whose string value is `true`.</span></span>

#### <a name="request-example-for-a-default-query"></a><span data-ttu-id="0da9b-227">Exemple de demande pour une requête par défaut</span><span class="sxs-lookup"><span data-stu-id="0da9b-227">Request example for a default query</span></span>

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

## <a name="identify-the-user"></a><span data-ttu-id="0da9b-228">Identifier l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="0da9b-228">Identify the user</span></span>

<span data-ttu-id="0da9b-229">Chaque demande à vos services inclut l’iD masqué de l’utilisateur qui a effectué la demande, ainsi que le nom d’affichage de l’utilisateur et l’Azure Active Directory’objet.</span><span class="sxs-lookup"><span data-stu-id="0da9b-229">Every request to your services includes the obfuscated ID of the user that performed the request, as well as the user's display name and Azure Active Directory object ID.</span></span>

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

<span data-ttu-id="0da9b-230">Les `id` valeurs et les valeurs sont `aadObjectId` garanties d’être celle de l’utilisateur Teams authentifié.</span><span class="sxs-lookup"><span data-stu-id="0da9b-230">The `id` and `aadObjectId` values are guaranteed to be that of the authenticated Teams user.</span></span> <span data-ttu-id="0da9b-231">Ils peuvent être utilisés comme clés pour rechercher des informations d’identification ou tout état mis en cache dans votre service.</span><span class="sxs-lookup"><span data-stu-id="0da9b-231">They can be used as keys to look up credentials or any cached state in your service.</span></span> <span data-ttu-id="0da9b-232">En outre, chaque demande contient l’Azure Active Directory locataire de l’utilisateur, qui peut être utilisé pour identifier l’organisation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0da9b-232">In addition, each request contains the Azure Active Directory tenant ID of the user, which can be used to identify the user’s organization.</span></span> <span data-ttu-id="0da9b-233">Le cas échéant, la demande contient également les iD de l’équipe et du canal à partir de laquelle la demande provient.</span><span class="sxs-lookup"><span data-stu-id="0da9b-233">If applicable, the request also contains the team and channel IDs from which the request originated.</span></span>

## <a name="authentication"></a><span data-ttu-id="0da9b-234">Authentification</span><span class="sxs-lookup"><span data-stu-id="0da9b-234">Authentication</span></span>

<span data-ttu-id="0da9b-235">Si votre service nécessite l’authentification de l’utilisateur, vous devez vous connecter à l’utilisateur avant qu’il ne puisse utiliser l’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="0da9b-235">If your service requires user authentication, you need to sign in the user before he or she can use the messaging extension.</span></span> <span data-ttu-id="0da9b-236">Si vous avez écrit un bot ou un onglet qui signe dans l’utilisateur, cette section doit être familier.</span><span class="sxs-lookup"><span data-stu-id="0da9b-236">If you have written a bot or a tab that signs in the user, this section should be familiar.</span></span>

<span data-ttu-id="0da9b-237">La séquence est la suivante:</span><span class="sxs-lookup"><span data-stu-id="0da9b-237">The sequence is as follows:</span></span>

1. <span data-ttu-id="0da9b-238">L’utilisateur émet une requête, ou la requête par défaut est automatiquement envoyée à votre service.</span><span class="sxs-lookup"><span data-stu-id="0da9b-238">User issues a query, or the default query is automatically sent to your service.</span></span>
2. <span data-ttu-id="0da9b-239">Votre service vérifie si l’utilisateur s’est d’abord authentifié en inspectant l’Teams’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0da9b-239">Your service checks whether the user has first authenticated by inspecting the Teams user ID.</span></span>
3. <span data-ttu-id="0da9b-240">Si l’utilisateur ne s’est pas authentifié, renvoyez une `auth` réponse avec une action `openUrl` suggérée incluant l’URL d’authentification.</span><span class="sxs-lookup"><span data-stu-id="0da9b-240">If the user has not authenticated, send back an `auth` response with an `openUrl` suggested action including the authentication URL.</span></span>
4. <span data-ttu-id="0da9b-241">Le Microsoft Teams client lance une fenêtre contextée hébergeant votre page Web à l’aide de l’URL d’authentification donnée.</span><span class="sxs-lookup"><span data-stu-id="0da9b-241">The Microsoft Teams client launches a pop-up window hosting your webpage using the given authentication URL.</span></span>
5. <span data-ttu-id="0da9b-242">Une fois que l’utilisateur s’est dédité, vous devez fermer votre fenêtre et envoyer un « code d’authentification » Teams client.</span><span class="sxs-lookup"><span data-stu-id="0da9b-242">After the user signs in, you should close your window and send an "authentication code" to the Teams client.</span></span>
6. <span data-ttu-id="0da9b-243">Le Teams client réédite ensuite la requête à votre service, qui inclut le code d’authentification passé à l’étape 5.</span><span class="sxs-lookup"><span data-stu-id="0da9b-243">The Teams client then reissues the query to your service, which includes the authentication code passed in step 5.</span></span>

<span data-ttu-id="0da9b-244">Votre service doit vérifier que le code d’authentification reçu à l’étape 6 correspond à celui de l’étape 5.</span><span class="sxs-lookup"><span data-stu-id="0da9b-244">Your service should verify that the authentication code received in step 6 matches the one from step 5.</span></span> <span data-ttu-id="0da9b-245">Cela garantit qu’un utilisateur malveillant n’essaie pas d’usurper ou de compromettre le flux de connecte.</span><span class="sxs-lookup"><span data-stu-id="0da9b-245">This ensures that a malicious user does not try to spoof or compromise the sign-in flow.</span></span> <span data-ttu-id="0da9b-246">Cela « ferme efficacement la boucle » pour terminer la séquence d’authentification sécurisée.</span><span class="sxs-lookup"><span data-stu-id="0da9b-246">This effectively "closes the loop" to finish the secure authentication sequence.</span></span>

### <a name="respond-with-a-sign-in-action"></a><span data-ttu-id="0da9b-247">Réagissez par une action de dédant</span><span class="sxs-lookup"><span data-stu-id="0da9b-247">Respond with a sign-in action</span></span>

<span data-ttu-id="0da9b-248">Pour inciter un utilisateur non autorisé à se connecter, répondez par une action suggérée de type qui inclut `openUrl` l’URL d’authentification.</span><span class="sxs-lookup"><span data-stu-id="0da9b-248">To prompt an unauthenticated user to sign in, respond with a suggested action of type `openUrl` that includes the authentication URL.</span></span>

#### <a name="response-example-for-a-sign-in-action"></a><span data-ttu-id="0da9b-249">Exemple de réponse pour une action de dédant</span><span class="sxs-lookup"><span data-stu-id="0da9b-249">Response example for a sign-in action</span></span>

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
> <span data-ttu-id="0da9b-250">Pour que l’expérience de connexion soit hébergée dans un pop-up Teams, la partie domaine de l’URL doit être dans la liste des domaines valides de votre application.</span><span class="sxs-lookup"><span data-stu-id="0da9b-250">For the sign-in experience to be hosted in a Teams pop-up, the domain portion of the URL must be in your app’s list of valid domains.</span></span> <span data-ttu-id="0da9b-251">Pour plus d’informations, [voir validDomains](~/resources/schema/manifest-schema.md#validdomains) dans le schéma manifeste.</span><span class="sxs-lookup"><span data-stu-id="0da9b-251">For more information, see [validDomains](~/resources/schema/manifest-schema.md#validdomains) in the manifest schema.</span></span>

### <a name="start-the-sign-in-flow"></a><span data-ttu-id="0da9b-252">Démarrer le flux de connecte</span><span class="sxs-lookup"><span data-stu-id="0da9b-252">Start the sign-in flow</span></span>

<span data-ttu-id="0da9b-253">Votre expérience de connectement doit être réactive et s’insérer dans une fenêtre contextée.</span><span class="sxs-lookup"><span data-stu-id="0da9b-253">Your sign-in experience should be responsive and fit within a popup window.</span></span> <span data-ttu-id="0da9b-254">Il doit s’intégrer à [Microsoft Teams client JavaScript SDK](/javascript/api/overview/msteams-client), qui utilise le passage de messages.</span><span class="sxs-lookup"><span data-stu-id="0da9b-254">It should integrate with the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client), which uses message passing.</span></span>

<span data-ttu-id="0da9b-255">Comme avec d’autres expériences intégrées en cours d’exécution à l Microsoft Teams, votre code à l’intérieur de la fenêtre doit d’abord appeler `microsoftTeams.initialize()` .</span><span class="sxs-lookup"><span data-stu-id="0da9b-255">As with other embedded experiences running inside Microsoft Teams, your code inside the window needs to first call `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="0da9b-256">Si votre code effectue un flux OAuth, vous pouvez passer l’identifiant utilisateur Teams dans votre fenêtre, qui peut ensuite le transmettre à l’URL de connexion OAuth.</span><span class="sxs-lookup"><span data-stu-id="0da9b-256">If your code performs an OAuth flow, you can pass the Teams user ID into your window, which then can pass it to the OAuth sign-in URL.</span></span>

### <a name="complete-the-sign-in-flow"></a><span data-ttu-id="0da9b-257">Compléter le flux de signalisation</span><span class="sxs-lookup"><span data-stu-id="0da9b-257">Complete the sign-in flow</span></span>

<span data-ttu-id="0da9b-258">Lorsque la demande de inscription se termine et redirige vers votre page, elle doit effectuer les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="0da9b-258">When the sign-in request completes and redirects back to your page, it should perform the following steps:</span></span>

1. <span data-ttu-id="0da9b-259">Générer un code de sécurité.</span><span class="sxs-lookup"><span data-stu-id="0da9b-259">Generate a security code.</span></span> <span data-ttu-id="0da9b-260">(Cela peut être un nombre aléatoire.) Vous devez mettre en cache ce code sur votre service, ainsi que les informations d’identification obtenues par le flux de connexion tels que, OAuth 2.0 jetons.</span><span class="sxs-lookup"><span data-stu-id="0da9b-260">(This can be a random number.) You need to cache this code on your service, along with the credentials obtained through the sign-in flow such as, OAuth 2.0 tokens.</span></span>
2. <span data-ttu-id="0da9b-261">Appelez `microsoftTeams.authentication.notifySuccess` et passez le code de sécurité.</span><span class="sxs-lookup"><span data-stu-id="0da9b-261">Call `microsoftTeams.authentication.notifySuccess` and pass the security code.</span></span>

<span data-ttu-id="0da9b-262">À ce stade, la fenêtre se ferme et le contrôle est transmis à l’Teams client.</span><span class="sxs-lookup"><span data-stu-id="0da9b-262">At this point, the window closes and control is passed to the Teams client.</span></span> <span data-ttu-id="0da9b-263">Le client peut désormais rééditer la requête utilisateur d’origine, ainsi que le code de sécurité de la `state` propriété.</span><span class="sxs-lookup"><span data-stu-id="0da9b-263">The client now can reissue the original user query, along with the security code in the `state` property.</span></span> <span data-ttu-id="0da9b-264">Votre code peut utiliser le code de sécurité pour rechercher les informations d’identification stockées plus tôt pour compléter la séquence d’authentification, puis remplir la demande de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0da9b-264">Your code can use the security code to look up the credentials stored earlier to complete the authentication sequence and then complete the user request.</span></span>

#### <a name="reissued-request-example"></a><span data-ttu-id="0da9b-265">Exemple de demande réédité</span><span class="sxs-lookup"><span data-stu-id="0da9b-265">Reissued request example</span></span>

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

## <a name="sdk-support"></a><span data-ttu-id="0da9b-266">Prise en charge de la SDK</span><span class="sxs-lookup"><span data-stu-id="0da9b-266">SDK support</span></span>

### <a name="net"></a><span data-ttu-id="0da9b-267">.NET</span><span class="sxs-lookup"><span data-stu-id="0da9b-267">.NET</span></span>

<span data-ttu-id="0da9b-268">Pour recevoir et gérer les requêtes avec le Bot Builder SDK pour .NET, vous pouvez vérifier le `invoke` type d’action sur l’activité entrante, puis utiliser la méthode d’aide dans le paquet NuGet [Microsoft.Bot.Connector.Teams pour déterminer s’il](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) s’agit d’une activité d’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="0da9b-268">To receive and handle queries with the Bot Builder SDK for .NET, you can check for the `invoke` action type on the incoming activity and then use the helper method in the NuGet package [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) to determine whether it’s a messaging extension activity.</span></span>

#### <a name="example-code-in-net"></a><span data-ttu-id="0da9b-269">Exemple de code dans .NET</span><span class="sxs-lookup"><span data-stu-id="0da9b-269">Example code in .NET</span></span>

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

### <a name="nodejs"></a><span data-ttu-id="0da9b-270">Node.js</span><span class="sxs-lookup"><span data-stu-id="0da9b-270">Node.js</span></span>

#### <a name="example-code-in-nodejs"></a><span data-ttu-id="0da9b-271">Exemple de code dans Node.js</span><span class="sxs-lookup"><span data-stu-id="0da9b-271">Example code in Node.js</span></span>

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

## <a name="see-also"></a><span data-ttu-id="0da9b-272">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="0da9b-272">See also</span></span>

<span data-ttu-id="0da9b-273">[Échantillons bot framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="0da9b-273">[Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>
