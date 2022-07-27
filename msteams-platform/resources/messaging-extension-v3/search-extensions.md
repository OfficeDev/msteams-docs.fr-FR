---
title: Rechercher avec des extensions de message
description: Dans cet article, vous allez apprendre à développer des extensions de message basées sur la recherche
ms.topic: how-to
ms.localizationpriority: medium
ms.date: 07/20/2019
ms.openlocfilehash: aece6f0984e1a6979f5a591fb271010e508b51a1
ms.sourcegitcommit: 1cda2fd3498a76c09e31ed7fd88175414ad428f7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/27/2022
ms.locfileid: "67035225"
---
# <a name="search-with-message-extensions"></a>Rechercher avec des extensions de message

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

Les extensions de message basées sur la recherche vous permettent d’interroger votre service et de publier ces informations sous la forme d’une carte, directement dans votre message.

![Exemple de carte d’extension de message](~/assets/images/compose-extensions/ceexample.png)

Les sections suivantes décrivent comment procéder :

[!include[common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

## <a name="search-type-message-extensions"></a>Extensions de message de type de recherche

Pour l’extension de message basée sur la recherche, définissez le `type` paramètre `query`sur . Voici un exemple de manifeste avec une seule commande de recherche. Une extension de message unique peut avoir jusqu’à 10 commandes différentes qui lui sont associées. Cela peut inclure plusieurs commandes de recherche et plusieurs commandes basées sur des actions.

### <a name="complete-app-manifest-example"></a>Exemple de manifeste d’application complet

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

## <a name="test-via-uploading"></a>Tester via le chargement

Vous pouvez tester votre extension de message en chargeant votre application.

Pour ouvrir votre extension de message, accédez à l’une de vos conversations ou canaux. Choisissez le bouton **Plus d’options** (**&#8943;**) dans la zone de composition, puis choisissez votre extension de message.

## <a name="add-event-handlers"></a>Ajouter des gestionnaires d’événements

La plupart de votre travail implique l’événement `onQuery` , qui gère toutes les interactions dans la fenêtre d’extension de message.

Si vous définissez la `true` valeur `canUpdateConfiguration` sur dans le manifeste, vous activez l’élément de menu Paramètres pour votre extension de message, et devez également gérer `onQuerySettingsUrl` et `onSettingsUpdate`.

## <a name="handle-onquery-events"></a>Gérer les événements onQuery

Une extension de message reçoit un événement lorsqu’un `onQuery` événement se produit dans la fenêtre d’extension de message ou est envoyé à la fenêtre.

Si votre extension de message utilise une page de configuration, votre gestionnaire `onQuery` doit d’abord rechercher les informations de configuration stockées. Si l’extension de message n’est pas configurée, retournez une `config` réponse avec un lien vers votre page de configuration. La réponse de la page de configuration est également gérée par `onQuery`. La seule exception est lorsque la page de configuration est appelée par le gestionnaire pour `onQuerySettingsUrl`; consultez la section suivante :

Si votre extension de message nécessite une authentification, vérifiez les informations d’état de l’utilisateur. Si l’utilisateur n’est pas connecté, suivez les instructions de la section [Authentification](#authentication) plus loin dans cette rubrique.

Ensuite, vérifiez si `initialRun` elle est définie ; si c’est le cas, prenez les mesures appropriées, par exemple en fournissant des instructions ou une liste de réponses.

Le reste de votre gestionnaire `onQuery` invite l’utilisateur à fournir des informations, affiche une liste de cartes d’aperçu et retourne la carte sélectionnée par l’utilisateur.

## <a name="handle-onquerysettingsurl-and-onsettingsupdate-events"></a>Gérer les événements onQuerySettingsUrl et onSettingsUpdate

Les `onQuerySettingsUrl` événements et `onSettingsUpdate` les événements fonctionnent ensemble pour activer l’élément de menu **Paramètres** .

![Captures d’écran des emplacements de l’élément de menu Paramètres](~/assets/images/compose-extensions/compose-extension-settings-menu-item.png)

Votre gestionnaire pour `onQuerySettingsUrl` renvoie l’URL de la page de configuration ; une fois la page de configuration fermée, votre gestionnaire accepte `onSettingsUpdate` et enregistre l’état retourné. Il s’agit du seul cas dans lequel `onQuery` la page de configuration ne reçoit *pas* la réponse.

## <a name="receive-and-respond-to-queries"></a>Recevoir et répondre aux requêtes

Chaque demande adressée à votre extension de message est effectuée via un `Activity` objet publié sur votre URL de rappel. La requête contient des informations sur la commande utilisateur, telles que l’ID et les valeurs de paramètre. La demande fournit également des métadonnées sur le contexte dans lequel votre extension a été appelée, y compris l’ID d’utilisateur et de locataire, ainsi que l’ID de conversation ou de canal et les ID d’équipe.

### <a name="receive-user-requests"></a>Recevoir des demandes de l’utilisateur

Lorsqu’un utilisateur exécute une requête, Microsoft Teams envoie à votre service un objet Bot Framework `Activity` standard. Votre service doit exécuter sa logique pour un `Activity` type qui a `type` été défini `invoke` sur et `name` défini sur un type pris `composeExtension` en charge, comme indiqué dans le tableau suivant.

En plus des propriétés standard de l’activité du bot, la charge utile contient les métadonnées de requête suivantes :

|Nom de la propriété|Objectif|
|---|---|
|`type`| Type de requête ; doit être `invoke`. |
|`name`| Type de commande qui est émise à votre service. Actuellement, les types suivants sont pris en charge : <br>`composeExtension/query` <br>`composeExtension/querySettingUrl` <br>`composeExtension/setting` <br>`composeExtension/selectItem` <br>`composeExtension/queryLink` |
|`from.id`| Identification de l'utilisateur qui a envoyé la demande. |
|`from.name`| Nom de l'utilisateur qui a envoyé la demande. |
|`from.aadObjectId`| Microsoft Azure Active Directory ID d’objet (Azure AD) de l’utilisateur qui a envoyé la demande. |
|`channelData.tenant.id`| ID de locataire Microsoft Azure Active Directory (Azure AD). |
|`channelData.channel.id`| Identification du canal (si la demande a été faite dans un canal). |
|`channelData.team.id`| Identification de l'équipe (si la demande a été faite dans un canal). |
|`clientInfo`|Métadonnées facultatives sur le logiciel client utilisé pour envoyer le message d’un utilisateur. L’entité peut contenir deux propriétés :<br>Le `country` champ contient l’emplacement détecté par l’utilisateur.<br>Le `platform` champ décrit la plateforme cliente de messagerie. <br>Pour plus d’informations, *consultez* [Les types d’entités non IRI ( clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo)).|

Les paramètres de requête se trouvent dans l’objet value, qui inclut les propriétés suivantes :

| Nom de la propriété | Objectif |
|---|---|
| `commandId` | Nom de la commande appelée par l’utilisateur, correspondant à l’une des commandes déclarées dans le manifeste de l’application. |
| `parameters` | Tableau de paramètres : chaque objet de paramètre contient le nom du paramètre, ainsi que la valeur de paramètre fournie par l’utilisateur. |
| `queryOptions` | Paramètres de pagination : <br>`skip`: nombre d’skips pour cette requête <br>`count`: nombre d’éléments à retourner |

#### <a name="request-example"></a>Exemple de requête

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

### <a name="receive-requests-from-links-inserted-into-the-compose-message-box"></a>Recevoir des demandes à partir de liens insérés dans la zone de composition du message

En guise d’alternative (ou en plus) à la recherche de votre service externe, vous pouvez utiliser une URL insérée dans la boîte de message de composition pour interroger votre service et retourner une carte. Dans la capture d’écran ci-dessous, un utilisateur a collé une URL pour un élément de travail dans Azure DevOps, que l’extension de message a résolue dans une carte.

![Exemple de déploiement de lien](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

Pour permettre à votre extension de message d’interagir avec les liens de cette façon, vous devez d’abord ajouter le `messageHandlers` tableau au manifeste de votre application, comme dans l’exemple ci-dessous :

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

Une fois que vous avez ajouté le domaine pour écouter le manifeste de l’application, vous devez modifier le code de votre bot pour [répondre](#respond-to-user-requests) à la demande d’appel ci-dessous.

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

Si votre application retourne plusieurs éléments, seul le premier sera utilisé.

### <a name="respond-to-user-requests"></a>Répondre aux demandes des utilisateurs

Lorsque l’utilisateur exécute une requête, Teams émet une requête HTTP synchrone à votre service. Pendant ce temps, votre code dispose de 5 secondes pour fournir une réponse HTTP à la requête. Pendant ce temps, votre service peut effectuer une recherche supplémentaire ou toute autre logique métier nécessaire pour traiter la demande.

Votre service doit répondre avec les résultats correspondant à la requête utilisateur. La réponse doit indiquer un code d’état HTTP et `200 OK` un objet application/json valide avec le corps suivant :

|Nom de la propriété|Objectif|
|---|---|
|`composeExtension`|Enveloppe de réponse de niveau supérieur.|
|`composeExtension.type`|Type de réponse. Les types suivants sont pris en charge : <br>`result`: affiche la liste des résultats de la recherche <br>`auth`: invite l’utilisateur à s’authentifier <br>`config`: invite l’utilisateur à configurer l’extension de message <br>`message` : affiche un message en texte brut. |
|`composeExtension.attachmentLayout`|Spécifie la disposition des pièces jointes. Utilisé pour les réponses de type `result`. <br>Actuellement, les types suivants sont pris en charge : <br>`list`: liste d’objets de carte contenant des champs miniature, titre et texte <br>`grid`: grille d’images miniatures |
|`composeExtension.attachments`|Tableau d’objets pièce jointe valides. Utilisé pour les réponses de type `result`. <br>Actuellement, les types suivants sont pris en charge : <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|Actions suggérées. Utilisé pour les réponses de type `auth` ou `config`. |
|`composeExtension.text`|Message à afficher. Utilisé pour les réponses de type `message`. |

#### <a name="response-card-types-and-previews"></a>Types de cartes de réponse et aperçus

Nous prenons en charge les types de pièces jointes suivants :

* [Carte miniature](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [Carte de bannière](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Carte Connecteur Office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [Carte adaptative](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

Pour plus d’informations, consultez [Cartes](~/task-modules-and-cards/what-are-cards.md) pour obtenir une vue d’ensemble.

Pour savoir comment utiliser les types de miniatures et de cartes de héros, consultez [Ajouter des cartes et des actions de carte](~/task-modules-and-cards/cards/cards-actions.md).

Pour obtenir de la documentation supplémentaire sur la carte de connecteur Office 365, consultez [Utilisation des cartes de connecteur Office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).

La liste des résultats s’affiche dans l’interface utilisateur de Microsoft Teams avec un aperçu de chaque élément. La préversion est générée de deux manières :

* Utilisation de la `preview` propriété dans l’objet `attachment` . La `preview` pièce jointe ne peut être qu’un héros ou une carte miniature.
* Extrait des propriétés de base `title``text`et `image` de la pièce jointe. Elles sont utilisées uniquement si la `preview` propriété n’est pas définie et que ces propriétés sont disponibles.

Vous pouvez afficher un aperçu d’une carte de connecteur adaptative ou Office 365 dans la liste des résultats en définissant simplement sa propriété d’aperçu. Cela n’est pas nécessaire si les résultats sont déjà des cartes de héros ou de miniatures. Si vous utilisez la pièce jointe en préversion, il doit s’agir d’une carte Hero ou Thumbnail. Si aucune propriété d’aperçu n’est spécifiée, l’aperçu de la carte échoue et rien ne s’affiche.

#### <a name="response-example"></a>Exemple de réponse

Cet exemple montre une réponse avec deux résultats, combinant différents formats de carte : Office 365 Connecteur et Adaptatif. Bien que vous souhaitiez probablement utiliser un format de carte dans votre réponse, elle montre comment la `preview` propriété de chaque élément de la `attachments` collection doit définir explicitement un aperçu au format héros ou miniature, comme décrit ci-dessus.

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

### <a name="default-query"></a>Requête par défaut

Si vous avez la valeur définie `initialRun` `true` dans le manifeste, Microsoft Teams émet une requête « par défaut » lorsque l’utilisateur ouvre l’extension de message pour la première fois. Votre service peut répondre à cette requête avec un ensemble de résultats préremplis. Cela peut être utile pour afficher, par exemple, les éléments récemment consultés, les favoris ou toute autre information qui ne dépend pas de l’entrée de l’utilisateur.

La requête par défaut a la même structure que n’importe quelle requête utilisateur standard, sauf avec un paramètre `initialRun` dont la valeur de chaîne est `true`.

#### <a name="request-example-for-a-default-query"></a>Exemple de requête pour une requête par défaut

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

## <a name="identify-the-user"></a>Identifier l’utilisateur

Chaque demande adressée à vos services inclut l’ID masqué de l’utilisateur qui a effectué la requête, ainsi que le nom d’affichage et l’ID d’objet Microsoft Azure Active Directory (Azure AD) de l’utilisateur.

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

Les `id` valeurs et `aadObjectId` les valeurs sont garanties comme celles de l’utilisateur Teams authentifié. Elles peuvent être utilisées comme clés pour rechercher des informations d’identification ou n’importe quel état mis en cache dans votre service. En outre, chaque requête contient l’ID de locataire Microsoft Azure Active Directory (Azure AD) de l’utilisateur, qui peut être utilisé pour identifier l’organisation de l’utilisateur. Le cas échéant, la demande contient également les ID d’équipe et de canal d’où provient la demande.

## <a name="authentication"></a>Authentification

Si votre service requiert l’authentification de l’utilisateur, vous devez connecter l’utilisateur avant que l’utilisateur puisse utiliser l’extension de message. Si vous avez écrit un bot ou un onglet qui connecte l’utilisateur, cette section doit être familière.

La séquence est la suivante :

1. L’utilisateur émet une requête ou la requête par défaut est automatiquement envoyée à votre service.
2. Votre service vérifie si l’utilisateur s’est d’abord authentifié en inspectant l’ID d’utilisateur Teams.
3. Si l’utilisateur ne s’est pas authentifié, renvoyez une `auth` réponse avec une `openUrl` action suggérée, y compris l’URL d’authentification.
4. Le client Microsoft Teams lance une fenêtre contextuelle hébergeant votre page web à l’aide de l’URL d’authentification donnée.
5. Une fois que l’utilisateur s’est connecté, vous devez fermer votre fenêtre et envoyer un « code d’authentification » au client Teams.
6. Le client Teams réissue ensuite la requête à votre service, qui inclut le code d’authentification passé à l’étape 5.

Votre service doit vérifier que le code d’authentification reçu à l’étape 6 correspond à celui de l’étape 5, ce qui garantit qu’un utilisateur malveillant n’essaie pas d’usurper ou de compromettre le flux de connexion. Cela « ferme la boucle » pour terminer la séquence d’authentification sécurisée.

### <a name="respond-with-a-sign-in-action"></a>Répondre avec une action de connexion

Pour inviter un utilisateur non authentifié à se connecter, répondez avec une action suggérée de type `openUrl` qui inclut l’URL d’authentification.

#### <a name="response-example-for-a-sign-in-action"></a>Exemple de réponse pour une action de connexion

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
> Pour que l’expérience de connexion soit hébergée dans une fenêtre contextuelle Teams, la partie domaine de l’URL doit figurer dans la liste des domaines valides de votre application. Pour plus d’informations, consultez [validDomains](~/resources/schema/manifest-schema.md#validdomains) dans le schéma du manifeste.

### <a name="start-the-sign-in-flow"></a>Démarrer le flux de connexion

Votre expérience de connexion doit être réactive et tenir dans une fenêtre contextuelle. Il doit s’intégrer au [kit de développement logiciel (SDK) client JavaScript Microsoft Teams](/javascript/api/overview/msteams-client), qui utilise la transmission de messages.

Comme avec d’autres expériences incorporées s’exécutant dans Teams, votre code à l’intérieur de la fenêtre doit d’abord appeler `microsoftTeams.initialize()`. Si votre code exécute un flux OAuth, vous pouvez passer l’ID d’utilisateur Teams dans votre fenêtre, qui peut ensuite le transmettre à l’URL de connexion OAuth.

### <a name="complete-the-sign-in-flow"></a>Terminer le flux de connexion

Une fois la demande de connexion terminée et redirigée vers votre page, elle doit effectuer les étapes suivantes :

1. Générez un code de sécurité. (Il peut s’agir d’un nombre aléatoire.) Vous devez mettre en cache ce code sur votre service, ainsi que les informations d’identification obtenues via le flux de connexion, tels que les jetons OAuth 2.0.
2. Appelez `microsoftTeams.authentication.notifySuccess` et transmettez le code de sécurité.

À ce stade, la fenêtre se ferme et le contrôle est passé au client Teams. Le client peut maintenant réexécuter la requête utilisateur d’origine, ainsi que le code de sécurité dans la `state` propriété. Votre code peut utiliser le code de sécurité pour rechercher les informations d’identification stockées précédemment afin de terminer la séquence d’authentification, puis la requête de l’utilisateur.

#### <a name="reissued-request-example"></a>Exemple de nouvelle publication de requête

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

## <a name="sdk-support"></a>Prise en charge du Kit de développement logiciel (SDK)

### <a name="net"></a>.NET

Pour recevoir et gérer des requêtes avec le Kit de développement logiciel (SDK) Bot Builder pour .NET, vous pouvez rechercher le `invoke` type d’action sur l’activité entrante, puis utiliser la méthode d’assistance dans le package NuGet [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) pour déterminer s’il s’agit d’une activité d’extension de message.

#### <a name="example-code-in-net"></a>Exemple de code dans .NET

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

### <a name="nodejs"></a>Node.js

#### <a name="example-code-in-nodejs"></a>Exemple de code dans Node.js

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

## <a name="see-also"></a>Voir aussi

[Exemples Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)
