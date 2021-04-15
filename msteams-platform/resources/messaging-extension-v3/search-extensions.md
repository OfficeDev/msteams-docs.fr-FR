---
title: Rechercher avec des extensions de messagerie
description: Décrit comment développer des extensions de messagerie basées sur la recherche
keywords: teams messaging extensions messaging extensions search
ms.topic: how-to
ms.date: 07/20/2019
ms.openlocfilehash: 7a4074fe4f3a15621729f4c549d31dc90d98e714
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696103"
---
# <a name="search-with-messaging-extensions"></a>Rechercher avec des extensions de messagerie

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

Les extensions de messagerie basées sur la recherche vous permettent d'interroger votre service et de publier ces informations sous la forme d'une carte, directement dans votre message

![Exemple de carte d'extension de messagerie](~/assets/images/compose-extensions/ceexample.png)

Les sections suivantes décrivent comment faire.

[!include[common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

### <a name="search-type-message-extensions"></a>Extensions de message de type de recherche

Pour l'extension de messagerie basée sur la recherche, définissez `type` le paramètre sur `query` . Vous trouverez ci-dessous un exemple de manifeste avec une seule commande de recherche. Une seule extension de messagerie peut être associée à jusqu'à 10 commandes différentes. Cela peut inclure à la fois plusieurs commandes de recherche et plusieurs commandes basées sur l'action.

#### <a name="complete-app-manifest-example"></a>Exemple de manifeste d'application complet

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

### <a name="test-via-uploading"></a>Test via le chargement

Vous pouvez tester votre extension de messagerie en chargeant votre application.

Pour ouvrir votre extension de messagerie, accédez à vos conversations ou canaux. Choisissez le **bouton Plus d'options** (**&#8943;**) dans la zone de composition, puis choisissez votre extension de messagerie.

## <a name="add-event-handlers"></a>Ajouter des handlers d'événements

La majeure partie de votre travail implique l'événement, qui gère toutes les interactions dans la `onQuery` fenêtre d'extension de messagerie.

Si vous le définissez dans le manifeste, vous activez l'élément de `canUpdateConfiguration` `true` menu **Paramètres** pour votre extension de messagerie et vous devez également gérer `onQuerySettingsUrl` et `onSettingsUpdate` .

### <a name="handle-onquery-events"></a>Gérer les événements onQuery

Une extension de messagerie reçoit un événement lorsqu'un événement se produit dans la fenêtre d'extension de messagerie ou `onQuery` est envoyé à la fenêtre.

Si votre extension de messagerie utilise une page de configuration, votre responsable doit d'abord vérifier les informations de configuration stockées ; si l'extension de messagerie n'est pas configurée, renvoyez une réponse avec un lien vers votre page de `onQuery` `config` configuration. N'ignorez pas que la réponse de la page de configuration est également gérée par `onQuery` . (La seule exception est lorsque la page de configuration est appelée par le responsable pour `onQuerySettingsUrl` ; voir la section suivante.)

Si votre extension de messagerie nécessite une authentification, vérifiez les informations d'état de l'utilisateur . Si l'utilisateur n'est pas inscrit, suivez les instructions de la section [Authentification](#authentication) plus loin dans cette rubrique.

Ensuite, vérifiez si elle est définie ; si c'est le cas, prenez les mesures appropriées, par exemple en fournissant des `initialRun` instructions ou une liste de réponses.

Le reste de votre responsable invite l'utilisateur à fournir des informations, affiche une liste de cartes d'aperçu et renvoie la carte sélectionnée `onQuery` par l'utilisateur.

### <a name="handle-onquerysettingsurl-and-onsettingsupdate-events"></a>Gérer les événements onQuerySettingsUrl et onSettingsUpdate

Les `onQuerySettingsUrl` `onSettingsUpdate` événements et les événements fonctionnent ensemble pour activer **l'élément de menu Paramètres.**

![Captures d'écran des emplacements de l'élément de menu Paramètres](~/assets/images/compose-extensions/compose-extension-settings-menu-item.png)

Votre responsable renvoie l'URL de la page de configuration ; une fois que la page de configuration se ferme, votre responsable accepte et enregistre `onQuerySettingsUrl` `onSettingsUpdate` l'état renvoyé. (C'est le cas dans lequel `onQuery` *ne reçoit pas* la réponse de la page de configuration.)

## <a name="receive-and-respond-to-queries"></a>Recevoir des requêtes et y répondre

Chaque demande à votre extension de messagerie est effectuée via un objet qui `Activity` est publié sur votre URL de rappel. La demande contient des informations sur la commande utilisateur, telles que les valeurs d'ID et de paramètre. La demande fournit également des métadonnées sur le contexte dans lequel votre extension a été invoquée, y compris l'ID d'utilisateur et de client, ainsi que les ID de conversation, le canal et les ID d'équipe.

### <a name="receive-user-requests"></a>Recevoir des demandes des utilisateurs

Lorsqu'un utilisateur effectue une requête, Microsoft Teams envoie à votre service un objet Bot Framework `Activity` standard. Votre service doit effectuer sa logique pour un type qui a été définie sur un type pris en charge, comme indiqué `Activity` `type` dans le tableau `invoke` `name` `composeExtension` suivant.

Outre les propriétés d'activité standard du bot, la charge utile contient les métadonnées de requête suivantes :

|Nom de la propriété|Objectif|
|---|---|
|`type`| Type de demande ; doit être `invoke` . |
|`name`| Type de commande qui est émis pour votre service. Actuellement, les types suivants sont pris en charge : <br>`composeExtension/query` <br>`composeExtension/querySettingUrl` <br>`composeExtension/setting` <br>`composeExtension/selectItem` <br>`composeExtension/queryLink` |
|`from.id`| ID de l'utilisateur qui a envoyé la demande. |
|`from.name`| Nom de l'utilisateur qui a envoyé la demande. |
|`from.aadObjectId`| ID d'objet Azure Active Directory de l'utilisateur qui a envoyé la demande. |
|`channelData.tenant.id`| ID du client Azure Active Directory. |
|`channelData.channel.id`| ID de canal (si la demande a été faite dans un canal). |
|`channelData.team.id`| ID d'équipe (si la demande a été faite dans un canal). |
|`clientInfo`|Métadonnées facultatives sur le logiciel client utilisé pour envoyer le message d'un utilisateur. L'entité peut contenir deux propriétés :<br>Le `country` champ contient l'emplacement détecté par l'utilisateur.<br>Le `platform` champ décrit la plateforme cliente de messagerie. <br>Pour plus d'informations, *consultez les* [types d'entités non IRI — clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo).|

Les paramètres de demande proprement dits se trouvent dans l'objet value, qui inclut les propriétés suivantes :

| Nom de la propriété | Objectif |
|---|---|
| `commandId` | Nom de la commande invoquée par l'utilisateur, correspondant à l'une des commandes déclarées dans le manifeste de l'application. |
| `parameters` | Tableau de paramètres. Chaque objet paramètre contient le nom du paramètre, ainsi que la valeur de paramètre fournie par l'utilisateur. |
| `queryOptions` | Paramètres de pagination : <br>`skip`: nombre d'ignorer pour cette requête <br>`count`: nombre d'éléments à renvoyer |

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

### <a name="receive-requests-from-links-inserted-into-the-compose-message-box"></a>Recevoir des demandes à partir de liens insérés dans la zone composer un message

Comme alternative (ou en plus) à la recherche de votre service externe, vous pouvez utiliser une URL insérée dans la zone de composition de message pour interroger votre service et renvoyer une carte. Dans la capture d'écran ci-dessous, un utilisateur a passé une URL pour un élément de travail dans Azure DevOps que l'extension de messagerie a résolue en une carte.

![Exemple de déploiement de lien](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

Pour permettre à votre extension de messagerie d'interagir avec les liens de cette façon, vous devez d'abord ajouter le tableau au manifeste de votre application, comme dans `messageHandlers` l'exemple ci-dessous :

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

Une fois que vous avez ajouté le domaine pour écouter le manifeste de [](#respond-to-user-requests) l'application, vous devez modifier votre code de bot pour répondre à la demande d'appel ci-dessous.

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

Si votre application renvoie plusieurs éléments, seul le premier sera utilisé.

### <a name="respond-to-user-requests"></a>Répondre aux demandes des utilisateurs

Lorsque l'utilisateur effectue une requête, Microsoft Teams adresse une requête HTTP synchrone à votre service. À ce stade, votre code dispose de 5 secondes pour fournir une réponse HTTP à la demande. Pendant ce temps, votre service peut effectuer une recherche supplémentaire ou toute autre logique métier nécessaire pour répondre à la demande.

Votre service doit répondre avec les résultats correspondant à la requête de l'utilisateur. La réponse doit indiquer un code d'état HTTP et un objet `200 OK` application/json valide avec le corps suivant :

|Nom de la propriété|Objectif|
|---|---|
|`composeExtension`|Enveloppe de réponse de niveau supérieur.|
|`composeExtension.type`|Type de réponse. Les types suivants sont pris en charge : <br>`result`: affiche une liste de résultats de recherche <br>`auth`: demande à l'utilisateur de s'authentifier <br>`config`: demande à l'utilisateur de configurer l'extension de messagerie <br>`message` : affiche un message en texte brut. |
|`composeExtension.attachmentLayout`|Spécifie la disposition des pièces jointes. Utilisé pour les réponses de type `result` . <br>Actuellement, les types suivants sont pris en charge : <br>`list`: liste d'objets de carte contenant des champs de miniature, de titre et de texte <br>`grid`: une grille d'images miniatures |
|`composeExtension.attachments`|Tableau d'objets pièce jointe valides. Utilisé pour les réponses de type `result` . <br>Actuellement, les types suivants sont pris en charge : <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|Actions suggérées. Utilisé pour les réponses de type `auth` `config` ou . |
|`composeExtension.text`|Message à afficher. Utilisé pour les réponses de type `message` . |

#### <a name="response-card-types-and-previews"></a>Types et aperçus de cartes de réponse

Nous prise en charge les types de pièces jointes suivants :

* [Carte miniature](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [Carte Hero](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Carte connecteur Office 365](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [Carte adaptative](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

Voir [Cartes](~/task-modules-and-cards/what-are-cards.md) pour une vue d'ensemble.

Pour découvrir comment utiliser les types de carte miniature et hero, voir Ajouter des cartes et [des actions de carte.](~/task-modules-and-cards/cards/cards-actions.md)

Pour obtenir une documentation supplémentaire concernant la carte de connecteur Office 365, voir Utilisation de cartes de connecteur [Office 365.](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)

La liste des résultats s'affiche dans l'interface utilisateur de Microsoft Teams avec un aperçu de chaque élément. L'aperçu est généré de deux manières :

* Utilisation de la `preview` propriété dans `attachment` l'objet. La `preview` pièce jointe ne peut être qu'une carte hero ou miniature.
* Extrait de la base `title` et `text` des `image` propriétés de la pièce jointe. Elles sont utilisées uniquement si la `preview` propriété n'est pas définie et que ces propriétés sont disponibles.

Vous pouvez afficher un aperçu d'une carte de connecteur Adaptatif ou Office 365 dans la liste des résultats simplement en définition de sa propriété d'aperçu . Cela n'est pas nécessaire si les résultats sont déjà des cartes hero ou miniatures. Si vous utilisez la pièce jointe d'aperçu, il doit s'agit d'une carte Hero ou miniature. Si aucune propriété d'aperçu n'est spécifiée, l'aperçu de la carte échoue et rien ne s'affiche.

#### <a name="response-example"></a>Exemple de réponse

Cet exemple montre une réponse avec deux résultats, combinant différents formats de carte : connecteur Office 365 et adaptatif. Bien que vous vouliez probablement vous en tenir à un seul format de carte dans votre réponse, il montre comment la propriété de chaque élément de la collection doit définir explicitement un aperçu au format Hero ou miniature, comme décrit `preview` `attachments` ci-dessus.

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

Si vous la définissez dans le manifeste, Microsoft Teams publie une requête « par défaut » lorsque l'utilisateur ouvre l'extension de messagerie pour la `initialRun` `true` première fois. Votre service peut répondre à cette requête avec un ensemble de résultats prérepliés. Cela peut être utile pour afficher, par exemple, les éléments récemment affichés, les favoris ou toute autre information qui ne dépend pas de l'entrée utilisateur.

La requête par défaut a la même structure que n'importe quelle requête utilisateur normale, sauf avec un paramètre dont la `initialRun` valeur de chaîne est `true` .

#### <a name="request-example-for-a-default-query"></a>Exemple de requête par défaut

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

## <a name="identify-the-user"></a>Identifier l'utilisateur

Chaque demande à vos services inclut l'ID obscurci de l'utilisateur qui a effectué la demande, ainsi que le nom d'affichage de l'utilisateur et l'ID d'objet Azure Active Directory.

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

Les `id` `aadObjectId` valeurs et les valeurs sont garanties pour être celle de l'utilisateur Teams authentifié. Elles peuvent être utilisées comme clés pour rechercher des informations d'identification ou tout état mis en cache dans votre service. En outre, chaque demande contient l'ID de client Azure Active Directory de l'utilisateur, qui peut être utilisé pour identifier l'organisation de l'utilisateur. Le cas échéant, la demande contient également les ID d'équipe et de canal d'où provient la demande.

## <a name="authentication"></a>Authentification

Si votre service requiert l'authentification de l'utilisateur, vous devez le signer avant de pouvoir utiliser l'extension de messagerie. Si vous avez écrit un bot ou un onglet qui se signe dans l'utilisateur, cette section doit être familière.

La séquence est la suivante :

1. Un utilisateur envoie une requête ou la requête par défaut est automatiquement envoyée à votre service.
2. Votre service vérifie si l'utilisateur s'est d'abord authentifié en inspectant l'ID d'utilisateur Teams.
3. Si l'utilisateur ne s'est pas authentifié, renvoyez une réponse avec une action suggérée, y compris `auth` `openUrl` l'URL d'authentification.
4. Le client Microsoft Teams lance une fenêtre pop-up hébergeant votre page web à l'aide de l'URL d'authentification donnée.
5. Une fois que l'utilisateur s'est signé, vous devez fermer votre fenêtre et envoyer un « code d'authentification » au client Teams.
6. Le client Teams ressue ensuite la requête à votre service, qui inclut le code d'authentification passé à l'étape 5.

Votre service doit vérifier que le code d'authentification reçu à l'étape 6 correspond à celui de l'étape 5. Cela garantit qu'un utilisateur malveillant ne tente pas d'usurper ou de compromettre le flux de la signature. Cela permet effectivement de « fermer la boucle » pour terminer la séquence d'authentification sécurisée.

### <a name="respond-with-a-sign-in-action"></a>Répondre avec une action de connect

Pour inciter un utilisateur non authentifié à se connecter, répondez avec une action suggérée de type qui inclut `openUrl` l'URL d'authentification.

#### <a name="response-example-for-a-sign-in-action"></a>Exemple de réponse pour une action de sign-in

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
> Pour que l'expérience de se connecte soit hébergée dans une fenêtre pop-up Teams, la partie domaine de l'URL doit se trouver dans la liste des domaines valides de votre application. (Voir [validDomains](~/resources/schema/manifest-schema.md#validdomains) dans le schéma de manifeste.)

### <a name="start-the-sign-in-flow"></a>Démarrer le flux de la signature

Votre expérience de sign-in doit être réactive et tenir dans une fenêtre popup. Il doit s'intégrer au [SDK client JavaScript Microsoft Teams,](/javascript/api/overview/msteams-client)qui utilise la transmission de message.

Comme avec d'autres expériences incorporées en cours d'exécution dans Microsoft Teams, votre code à l'intérieur de la fenêtre doit d'abord `microsoftTeams.initialize()` appeler. Si votre code effectue un flux OAuth, vous pouvez transmettre l'ID utilisateur Teams dans votre fenêtre, qui peut ensuite le transmettre à l'URL de la signature OAuth.

### <a name="complete-the-sign-in-flow"></a>Terminer le flux de la signature

Lorsque la demande de se connecte est terminée et redirige vers votre page, elle doit effectuer les étapes suivantes :

1. Générer un code de sécurité. (Il peut s'agit d'un nombre aléatoire.) Vous devez mettre en cache ce code sur votre service, ainsi que les informations d'identification obtenues via le flux de connexion (tels que les jetons OAuth 2.0).
2. Appelez `microsoftTeams.authentication.notifySuccess` et passez le code de sécurité.

À ce stade, la fenêtre se ferme et le contrôle est transmis au client Teams. Le client peut maintenant rééditer la requête utilisateur d'origine, ainsi que le code de sécurité dans la `state` propriété. Votre code peut utiliser le code de sécurité pour rechercher les informations d'identification stockées précédemment pour terminer la séquence d'authentification, puis effectuer la demande de l'utilisateur.

#### <a name="reissued-request-example"></a>Exemple de requête rééditée

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

## <a name="sdk-support"></a>Prise en charge du SDK

### <a name="net"></a>.NET

Pour recevoir et gérer des requêtes avec le SDK Bot Builder pour .NET, vous pouvez vérifier le type d'action sur l'activité entrante, puis utiliser la méthode d'aide dans le `invoke` package NuGet [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) pour déterminer s'il s'agit d'une activité d'extension de messagerie.

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
*Voir aussi des* [exemples Bot Framework.](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)
