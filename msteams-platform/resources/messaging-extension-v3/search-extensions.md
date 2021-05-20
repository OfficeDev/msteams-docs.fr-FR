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
# <a name="search-with-messaging-extensions"></a>Rechercher avec des extensions de messagerie

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

Les extensions de messagerie basées sur la recherche vous permettent d’interroger votre service et de publier ces informations sous la forme d’une carte, directement dans votre message.

![Exemple de carte d’extension de messagerie](~/assets/images/compose-extensions/ceexample.png)

Les sections suivantes décrivent comment le faire :

[!include[common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

### <a name="search-type-message-extensions"></a>Extensions de message de type recherche

Pour l’extension de messagerie basée sur la recherche définir `type` le paramètre à `query` . Voici un exemple d’un manifeste avec une seule commande de recherche. Une seule extension de messagerie peut avoir jusqu’à 10 commandes différentes qui lui sont associées. Cela peut inclure à la fois plusieurs recherches et plusieurs commandes basées sur l’action.

#### <a name="complete-app-manifest-example"></a>Exemple complet de manifeste d’application

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

### <a name="test-via-uploading"></a>Test via le téléchargement

Vous pouvez tester votre extension de messagerie en téléchargeant votre application.

Pour ouvrir votre extension de messagerie, accédez à l’un de vos chats ou canaux. Choisissez le **bouton Plus d’options** **(&#8943;)** dans la boîte de composition, et choisissez votre extension de messagerie.

## <a name="add-event-handlers"></a>Ajouter des gestionnaires d’événements

La plupart de votre travail implique `onQuery` l’événement, qui gère toutes les interactions dans la fenêtre d’extension de messagerie.

Si vous `canUpdateConfiguration` définissez `true` dans le manifeste, vous activez **l’élément de** menu Paramètres pour votre extension de messagerie et devez également gérer et `onQuerySettingsUrl` `onSettingsUpdate` .

### <a name="handle-onquery-events"></a>Gérer les événements deQuery

Une extension de messagerie reçoit un `onQuery` événement lorsque quelque chose se passe dans la fenêtre d’extension de messagerie ou est envoyé à la fenêtre.

Si votre extension de messagerie utilise une page de configuration, votre gestionnaire doit `onQuery` d’abord vérifier les informations de configuration stockées; si l’extension de messagerie n’est pas configurée, retournez `config` une réponse avec un lien vers votre page de configuration. Sachez que la réponse de la page de configuration est également gérée par `onQuery` . La seule exception est lorsque la page de configuration est appelée par le gestionnaire pour `onQuerySettingsUrl` ; voir la section suivante:

Si votre extension de messagerie nécessite une authentification, vérifiez les informations de l’état de l’utilisateur; si l’utilisateur n’est pas connecté, suivez les instructions dans la section [Authentification](#authentication) plus tard dans ce sujet.

Ensuite, vérifiez si `initialRun` c’est défini; le cas échéant, prenez les mesures appropriées, comme fournir des instructions ou une liste de réponses.

Le reste de votre gestionnaire pour les invite `onQuery` à l’utilisateur pour des informations, affiche une liste de cartes de prévisualisation, et renvoie la carte sélectionnée par l’utilisateur.

### <a name="handle-onquerysettingsurl-and-onsettingsupdate-events"></a>Gérer les événementsQuerySettingsUrl et onSettingsUpdate

Les `onQuerySettingsUrl` événements et les événements travaillent ensemble pour permettre à `onSettingsUpdate` **l’Paramètres de** menu.

![Captures d’écran des emplacements Paramètres menu de l’article](~/assets/images/compose-extensions/compose-extension-settings-menu-item.png)

Votre gestionnaire pour `onQuerySettingsUrl` renvoie l’URL de la page de configuration; après la fermeture de la page de configuration, votre gestionnaire `onSettingsUpdate` accepte et enregistre l’état retourné. C’est le seul cas dans `onQuery` *lequel ne reçoit pas* la réponse de la page de configuration.

## <a name="receive-and-respond-to-queries"></a>Recevoir et répondre aux requêtes

Chaque demande à votre extension de messagerie se fait via `Activity` un objet qui est affiché sur votre URL de rappel. La demande contient des informations sur la commande utilisateur, telles que les valeurs d’identification et de paramètres. La demande fournit également des métadonnées sur le contexte dans lequel votre extension a été invoquée, y compris l’identification de l’utilisateur et du locataire, ainsi que l’id de chat ou les identifiants de chaîne et d’équipe.

### <a name="receive-user-requests"></a>Recevoir les demandes des utilisateurs

Lorsqu’un utilisateur effectue une requête, Microsoft Teams envoie à votre service un objet Bot Framework `Activity` standard. Votre service doit exécuter sa logique pour un qui a `Activity` défini et mis à un type pris en `type` `invoke` `name` `composeExtension` charge, comme indiqué dans le tableau suivant.

En plus des propriétés d’activité bot standard, la charge utile contient les métadonnées de demande suivantes :

|Nom de la propriété|Objectif|
|---|---|
|`type`| Type de demande; doit être `invoke` . |
|`name`| Type de commande qui est délivré à votre service. Actuellement, les types suivants sont pris en charge : <br>`composeExtension/query` <br>`composeExtension/querySettingUrl` <br>`composeExtension/setting` <br>`composeExtension/selectItem` <br>`composeExtension/queryLink` |
|`from.id`| ID de l’utilisateur qui a envoyé la demande. |
|`from.name`| Nom de l’utilisateur qui a envoyé la demande. |
|`from.aadObjectId`| Azure Active Directory id objet de l’utilisateur qui a envoyé la demande. |
|`channelData.tenant.id`| ID du client Azure Active Directory. |
|`channelData.channel.id`| ID de canal (si la demande a été faite dans un canal). |
|`channelData.team.id`| ID d’équipe (si la demande a été faite dans un canal). |
|`clientInfo`|Métadonnées optionnelles sur le logiciel client utilisé pour envoyer le message d’un utilisateur. L’entité peut contenir deux propriétés :<br>Le `country` champ contient l’emplacement détecté par l’utilisateur.<br>Le `platform` champ décrit la plate-forme client de messagerie. <br>Pour plus d’informations, *veuillez consulter* [les types d’entités non IRI — clientInfo](https://github.com/microsoft/botframework-sdk/blob/master/specs/botframework-activity/botframework-activity.md#clientinfo).|

Les paramètres de demande eux-mêmes se trouvent dans l’objet de valeur, qui comprend les propriétés suivantes :

| Nom de la propriété | Objectif |
|---|---|
| `commandId` | Le nom de la commande invoquée par l’utilisateur, correspondant à l’une des commandes déclarées dans le manifeste de l’application. |
| `parameters` | Tableau des paramètres : Chaque objet paramètre contient le nom du paramètre, ainsi que la valeur de paramètre fournie par l’utilisateur. |
| `queryOptions` | Paramètres de pagination : <br>`skip`: ignorer le nombre de requêtes <br>`count`: nombre d’éléments à retourner |

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

### <a name="receive-requests-from-links-inserted-into-the-compose-message-box"></a>Recevoir les demandes des liens insérés dans la boîte à messages de composition

Comme alternative (ou en outre) à la recherche de votre service externe, vous pouvez utiliser une URL insérée dans la boîte de messages de composition pour interroger votre service et retourner une carte. Dans la capture d’écran ci-dessous, un utilisateur a passé dans une URL pour un élément de travail en Azure DevOps que l’extension de messagerie a résolu dans une carte.

![Exemple de déploiement de liens](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

Pour permettre à votre extension de messagerie d’interagir avec les liens de cette façon, vous devrez d’abord ajouter `messageHandlers` le tableau à votre manifeste d’application comme dans l’exemple ci-dessous :

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

Une fois que vous avez ajouté le domaine pour écouter le manifeste de [](#respond-to-user-requests) l’application, vous devrez modifier votre code bot pour répondre à la demande d’invocateur ci-dessous.

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

Lorsque l’utilisateur effectue une requête, Microsoft Teams émet une demande HTTP synchrone à votre service. À ce stade, votre code dispose de 5 secondes pour fournir une réponse HTTP à la demande. Pendant ce temps, votre service peut effectuer des recherchez supplémentaires, ou toute autre logique d’entreprise nécessaire pour répondre à la demande.

Votre service doit répondre avec les résultats correspondant à la requête utilisateur. La réponse doit indiquer un code d’état HTTP `200 OK` et un objet d’application/json valide avec l’organisme suivant :

|Nom de la propriété|Objectif|
|---|---|
|`composeExtension`|Enveloppe de réponse de haut niveau.|
|`composeExtension.type`|Type de réponse. Les types suivants sont pris en charge : <br>`result`: affiche une liste de résultats de recherche <br>`auth`: demande à l’utilisateur de s’authentifier <br>`config`: demande à l’utilisateur de configurer l’extension de messagerie <br>`message` : affiche un message en texte brut. |
|`composeExtension.attachmentLayout`|Spécifie la disposition des pièces jointes. Utilisé pour les réponses de type `result` . <br>Actuellement, les types suivants sont pris en charge : <br>`list`: une liste d’objets de cartes contenant des champs de vignette, de titre et de texte <br>`grid`: une grille d’images miniatures |
|`composeExtension.attachments`|Tableau d’objets de pièce jointe valides. Utilisé pour les réponses de type `result` . <br>Actuellement, les types suivants sont pris en charge : <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|Actions suggérées. Utilisé pour les réponses de type `auth` ou `config` . |
|`composeExtension.text`|Message à afficher. Utilisé pour les réponses de type `message` . |

#### <a name="response-card-types-and-previews"></a>Types de cartes de réponse et aperçus

Nous prenons en charge les types de pièces jointes suivants :

* [Carte miniature](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [Carte de héros](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Office 365 Carte connecteur](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [Carte adaptative](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

Pour plus d’informations, consultez [Cartes pour](~/task-modules-and-cards/what-are-cards.md) un aperçu.

Pour apprendre à utiliser les types de vignettes et de cartes héros, voir Ajouter [des cartes et des actions de carte](~/task-modules-and-cards/cards/cards-actions.md).

Pour plus de documentation concernant la carte connecteur Office 365, voir Utilisation [Office 365 cartes Connecteur](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card).

La liste des résultats est affichée dans l’interface Microsoft Teams’interface utilisateur avec un aperçu de chaque élément. L’aperçu est généré de deux façons :

* Utilisation de la `preview` propriété dans `attachment` l’objet. La `preview` pièce jointe ne peut être qu’une carte Héros ou Vignette.
* Extrait de la base `title` , et les propriétés de la pièce `text` `image` jointe. Ceux-ci ne sont utilisés que si `preview` la propriété n’est pas définie et que ces propriétés sont disponibles.

Vous pouvez afficher un aperçu d’une carte Connecteur adaptative ou Office 365 dans la liste des résultats simplement en paramètre sa propriété d’aperçu; ce n’est pas nécessaire si les résultats sont déjà des cartes héros ou miniatures. Si vous utilisez la pièce jointe d’aperçu, il doit s’agir d’une carte Héros ou Vignette. Si aucune propriété d’aperçu n’est spécifiée, l’aperçu de la carte échouera et rien ne sera affiché.

#### <a name="response-example"></a>Exemple de réponse

Cet exemple montre une réponse avec deux résultats, mélangeant différents formats de cartes : Office 365 Connecteur et Adaptatif. Bien que vous voudrez probablement rester avec un format de carte dans votre réponse, il montre comment la `preview` propriété de chaque élément de la collection doit définir explicitement un aperçu en format héros ou vignette comme `attachments` décrit ci-dessus.

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

Si vous définissez `initialRun` `true` dans le manifeste, vous Microsoft Teams une requête « par défaut » lorsque l’utilisateur ouvre pour la première fois l’extension de messagerie. Votre service peut répondre à cette requête avec un ensemble de résultats prépeuplés. Cela peut être utile pour afficher, par exemple, des éléments, des favoris ou toute autre information qui ne dépend pas de l’entrée de l’utilisateur.

La requête par défaut a la même structure que n’importe quelle requête utilisateur régulière, sauf avec un paramètre dont `initialRun` la valeur de chaîne est `true` .

#### <a name="request-example-for-a-default-query"></a>Exemple de demande pour une requête par défaut

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

Chaque demande à vos services inclut l’iD masqué de l’utilisateur qui a effectué la demande, ainsi que le nom d’affichage de l’utilisateur et l’Azure Active Directory’objet.

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

Les `id` valeurs et les valeurs sont `aadObjectId` garanties d’être celle de l’utilisateur Teams authentifié. Ils peuvent être utilisés comme clés pour rechercher des informations d’identification ou tout état mis en cache dans votre service. En outre, chaque demande contient l’Azure Active Directory locataire de l’utilisateur, qui peut être utilisé pour identifier l’organisation de l’utilisateur. Le cas échéant, la demande contient également les iD de l’équipe et du canal à partir de laquelle la demande provient.

## <a name="authentication"></a>Authentification

Si votre service nécessite l’authentification de l’utilisateur, vous devez vous connecter à l’utilisateur avant qu’il ne puisse utiliser l’extension de messagerie. Si vous avez écrit un bot ou un onglet qui signe dans l’utilisateur, cette section doit être familier.

La séquence est la suivante:

1. L’utilisateur émet une requête, ou la requête par défaut est automatiquement envoyée à votre service.
2. Votre service vérifie si l’utilisateur s’est d’abord authentifié en inspectant l’Teams’utilisateur.
3. Si l’utilisateur ne s’est pas authentifié, renvoyez une `auth` réponse avec une action `openUrl` suggérée incluant l’URL d’authentification.
4. Le Microsoft Teams client lance une fenêtre contextée hébergeant votre page Web à l’aide de l’URL d’authentification donnée.
5. Une fois que l’utilisateur s’est dédité, vous devez fermer votre fenêtre et envoyer un « code d’authentification » Teams client.
6. Le Teams client réédite ensuite la requête à votre service, qui inclut le code d’authentification passé à l’étape 5.

Votre service doit vérifier que le code d’authentification reçu à l’étape 6 correspond à celui de l’étape 5. Cela garantit qu’un utilisateur malveillant n’essaie pas d’usurper ou de compromettre le flux de connecte. Cela « ferme efficacement la boucle » pour terminer la séquence d’authentification sécurisée.

### <a name="respond-with-a-sign-in-action"></a>Réagissez par une action de dédant

Pour inciter un utilisateur non autorisé à se connecter, répondez par une action suggérée de type qui inclut `openUrl` l’URL d’authentification.

#### <a name="response-example-for-a-sign-in-action"></a>Exemple de réponse pour une action de dédant

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
> Pour que l’expérience de connexion soit hébergée dans un pop-up Teams, la partie domaine de l’URL doit être dans la liste des domaines valides de votre application. Pour plus d’informations, [voir validDomains](~/resources/schema/manifest-schema.md#validdomains) dans le schéma manifeste.

### <a name="start-the-sign-in-flow"></a>Démarrer le flux de connecte

Votre expérience de connectement doit être réactive et s’insérer dans une fenêtre contextée. Il doit s’intégrer à [Microsoft Teams client JavaScript SDK](/javascript/api/overview/msteams-client), qui utilise le passage de messages.

Comme avec d’autres expériences intégrées en cours d’exécution à l Microsoft Teams, votre code à l’intérieur de la fenêtre doit d’abord appeler `microsoftTeams.initialize()` . Si votre code effectue un flux OAuth, vous pouvez passer l’identifiant utilisateur Teams dans votre fenêtre, qui peut ensuite le transmettre à l’URL de connexion OAuth.

### <a name="complete-the-sign-in-flow"></a>Compléter le flux de signalisation

Lorsque la demande de inscription se termine et redirige vers votre page, elle doit effectuer les étapes suivantes :

1. Générer un code de sécurité. (Cela peut être un nombre aléatoire.) Vous devez mettre en cache ce code sur votre service, ainsi que les informations d’identification obtenues par le flux de connexion tels que, OAuth 2.0 jetons.
2. Appelez `microsoftTeams.authentication.notifySuccess` et passez le code de sécurité.

À ce stade, la fenêtre se ferme et le contrôle est transmis à l’Teams client. Le client peut désormais rééditer la requête utilisateur d’origine, ainsi que le code de sécurité de la `state` propriété. Votre code peut utiliser le code de sécurité pour rechercher les informations d’identification stockées plus tôt pour compléter la séquence d’authentification, puis remplir la demande de l’utilisateur.

#### <a name="reissued-request-example"></a>Exemple de demande réédité

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

## <a name="sdk-support"></a>Prise en charge de la SDK

### <a name="net"></a>.NET

Pour recevoir et gérer les requêtes avec le Bot Builder SDK pour .NET, vous pouvez vérifier le `invoke` type d’action sur l’activité entrante, puis utiliser la méthode d’aide dans le paquet NuGet [Microsoft.Bot.Connector.Teams pour déterminer s’il](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) s’agit d’une activité d’extension de messagerie.

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

[Échantillons bot framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).
