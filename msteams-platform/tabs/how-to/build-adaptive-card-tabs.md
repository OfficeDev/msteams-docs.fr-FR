---
title: Créer des onglets de carte adaptative
author: KirtiPereira
description: Créer des onglets à l’aide de cartes adaptatives
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: none
ms.openlocfilehash: 09e5a6133ac4c2b33dbf6ffae273e8107a4c67ce
ms.sourcegitcommit: 22c9e44437720d30c992a4a3626a2a9f745983c1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2021
ms.locfileid: "60720329"
---
# <a name="build-tabs-with-adaptive-cards"></a>Créer des onglets avec les Cartes adaptatives

> [!IMPORTANT]
> * Les onglets avec cartes adaptatives sont actuellement uniquement pris en charge en tant qu’applications personnelles.

Lorsque vous développez un onglet à l’aide de la méthode traditionnelle, vous pouvez être face à ces problèmes :

* Considérations html et CSS
* Temps de chargement lents
* Contraintes iFrame
* Maintenance et coûts du serveur

Les onglets de carte adaptative sont un nouveau moyen de créer des onglets dans Teams. Au lieu d’incorporer du contenu web dans un IFrame, vous pouvez restituer des cartes adaptatives dans un onglet. Lorsque le frontal est restituer avec des cartes adaptatives, le système frontal est alimenté par un bot. Le bot est responsable de l’acceptation des demandes et de la réponse appropriée avec la carte adaptative qui est rendue.

Vous pouvez créer vos onglets avec des blocs de construction d’interface utilisateur (IU) prêts à l’emploi, natifs sur ordinateur de bureau, web et mobile. Cet article vous aide à comprendre les modifications à apporter au manifeste de l’application. L’article identifie également la façon dont l’activité d’appel demande et envoie des informations sous l’onglet avec des cartes adaptatives, et son effet sur le flux de travail du module de tâche.

L’image suivante montre les onglets de build avec des cartes adaptatives sur ordinateur de bureau et mobile :

:::image type="content" source="../../assets/images/tabs/adaptive-cards-rendered-in-tabs.jpg" alt-text="Exemple de carte adaptative rendue dans les onglets." border="false":::

## <a name="prerequisites"></a>Configuration requise

Avant de commencer à utiliser des cartes adaptatives pour créer des onglets, vous devez :

* Familiarisez-vous [avec le développement de bots,](../../bots/what-are-bots.md)les cartes [adaptatives](https://adaptivecards.io/)et les [modules](../../task-modules-and-cards/task-modules/task-modules-bots.md) de tâche Teams.
* Exécutez un bot Teams pour votre développement.

## <a name="changes-to-app-manifest"></a>Modifications apportées au manifeste de l’application

Les applications personnelles qui restituer les onglets doivent inclure un `staticTabs` tableau dans leur manifeste d’application. Les onglets carte adaptative sont rendus lorsque `contentBotId` la propriété est fournie dans la `staticTab` définition. Les définitions d’onglet statique doivent contenir soit un onglet de carte adaptative, soit un onglet de carte adaptative, spécifiant une expérience d’onglet de contenu web hébergé `contentBotId` `contentUrl` classique.

> [!NOTE]
> La `contentBotId` propriété est actuellement disponible dans le manifeste version 1.9 ou ultérieure.

Fournissez `contentBotId` la propriété avec `botId` l’onglet Carte adaptative avec qui doit communiquer. Le paramètre configuré pour l’onglet Carte adaptative est envoyé dans le paramètre de chaque demande d’appel et peut être utilisé pour différencier les onglets de carte adaptative qui sont alimentés par le `entityId` `tabContext` même bot. Pour plus d’informations sur les autres champs de définition d’onglet statique, voir [schéma de manifeste.](../../resources/schema/manifest-schema.md#statictabs)

Voici un exemple de manifeste d’onglet carte adaptative :

```json
{
  "$schema": "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
  "manifestVersion": "1.9",
  "id": "00000000-0000-0000-0000-000000000000",
  "version": "0.0.1",
  "packageName": "acprototype",
  "developer": {
    "name": "Contoso",
    "websiteUrl": "https://contoso.yourwebsite.com",
    "privacyUrl": "https://contoso.yourwebsite.com/privacy.html",
    "termsOfUseUrl": "https://contoso.yourwebsite.com/terms.html"
  },
  "name": {
    "short": "Contoso",
    "full": "Contoso Home"
  },
  "description": {
    "short": "Add short description here",
    "full": "Add full description here"
  },
  "icons": {
    "outline": "icon-outline.png",
    "color": "icon-color.png"
  },
  "accentColor": "#D85028",
  "configurableTabs": [],
  "staticTabs": [
    {
      "entityId": "homeTab",
      "name": "Home",
      "contentBotId": "00000000-0000-0000-0000-000000000000",
      "scopes": ["personal"]
    },
    {
      "entityId": "moreTab",
      "name": "More",
      "contentBotId": "00000000-0000-0000-0000-000000000000",
      "scopes": ["personal"]
    }
  ],
  "connectors": [],
  "composeExtensions": [],
  "permissions": ["identity", "messageTeamMembers"],
  "validDomains": [
    "contoso.yourwebsite.com",
    "token.botframework.com"
  ]
}
```

## <a name="invoke-activities"></a>Appeler des activités

La communication entre l’onglet Carte adaptative et votre bot s’fait par le biais `invoke` d’activités. Chaque `invoke` activité a un nom **correspondant.** Utilisez le nom de chaque activité pour différencier chaque demande. `tab/fetch` et `tab/submit` sont les activités couvertes dans cette section.

> [!NOTE]
> * Les bots doivent envoyer toutes les réponses à [l’URL du service.](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#base-uri&preserve-view=true) L’URL du service est reçue dans le cadre de la charge `activity` utile entrante.
> * La taille de la charge utile d’appel a augmenté jusqu’à 80 000b.

### <a name="fetch-adaptive-card-to-render-to-a-tab"></a>Récupérer la carte adaptative pour le rendu dans un onglet

`tab/fetch`est la première demande d’appel que votre bot reçoit lorsqu’un utilisateur ouvre un onglet Carte adaptative. Lorsque votre bot reçoit la demande, il envoie une réponse de tabulation **continue** ou une réponse **d’th de tabulation.**
La **réponse** continue inclut un tableau pour les **cartes,** qui est rendu verticalement sur l’onglet dans l’ordre du tableau.

> [!NOTE]
> Pour plus d’informations sur la réponse **d’authentification,** voir [l’authentification.](#authentication)

Le code suivant fournit des exemples de `tab/fetch` requête et de réponse :

**`tab/fetch` request**

```json
// tab/fetch POST request: agents/{botId}/invoke
{
    "name": "tab/fetch",
    "value: {
        "tabContext": {
            "tabEntityId": "{tab_entity_id}"
        },
        "context": {
            "theme": "default"
            }
    },
    "conversation": {
        "id": "{generated_conversation_id}"
    },
    "imdisplayname": "{user_display_name}"
}
```

**`tab/fetch` réponse**

```json
// tab/fetch **continue** POST response:
{
    "tab": {
        "type": "continue",
        "value": {
            "cards": [
                {
                    "card": adaptiveCard1,
                },
                {
                    "card": adaptiveCard2,
                }
                {
                    "card": adaptiveCard3
                }  
            ]
        },
    },
    "responseType": "tab"
}
```

### <a name="handle-submits-from-adaptive-card"></a>Gérer les soumissions à partir de la carte adaptative

Une fois qu’une carte adaptative est restituer dans l’onglet, elle peut répondre aux interactions de l’utilisateur. Cette réponse est gérée par la demande `tab/submit` d’appel.

Lorsqu’un utilisateur sélectionne un bouton sous l’onglet Carte adaptative, la demande est déclenchée à votre bot avec les données correspondantes par le biais de la `tab/submit` `Action.Submit` fonction de carte adaptative. Les données de carte adaptative sont disponibles via la propriété de données de la `tab/submit` demande. Vous recevez l’une des réponses suivantes à votre demande :

* Réponse de code d’état HTTP `200` sans corps. Une réponse 200 vide n’entraîne aucune action du client.
* L’onglet standard `200` **continue la** réponse, comme expliqué dans fetch Adaptive [Card](#fetch-adaptive-card-to-render-to-a-tab). Une réponse **de tabulation continue** déclenche la mise à jour de l’onglet Carte adaptative rendue par le client avec les cartes adaptatives fournies dans le tableau de cartes de la **réponse continue.**

Le code suivant fournit des exemples de `tab/submit` requête et de réponse :

**`tab/submit` request**

```json
// tab/submit POST request: agents/{botId}/invoke:
{
    "name": "tab/submit",
    "value": {
        "data": {
            "type": "tab/submit",
            //...<data properties>
            },
        "context": {
            "theme": "default"
            },
        "tabContext": {
            "tabEntityId": "{tab_entity_id}"
            },
        },
    "conversation": {
           "id": "{generated_conversation_id}" 
        },
    "imdisplayname": "{user_display_name}"
}
```

**`tab/submit` réponse**

```json
//tab/fetch **continue** POST response:
{
    "tab": {
        "type": "continue",
        "value": {
            "cards": [
              {
                "card": adaptiveCard1,
                },
              {
                "card": adaptiveCard2,
                } 
            ]
        },
    },
    "responseType": "tab"
}
```

## <a name="understand-task-module-workflow"></a>Comprendre le flux de travail du module de tâche

Le module de tâche utilise également la carte adaptative pour appeler `task/fetch` et les demandes et les `task/submit` réponses. Pour plus d’informations, [voir l’utilisation des modules de tâche Microsoft Teams bots.](../../task-modules-and-cards/task-modules/task-modules-bots.md)

Avec l’introduction de l’onglet Carte adaptative, il existe un changement dans la façon dont le bot répond à une `task/submit` demande. Si vous utilisez un onglet Carte adaptative, le bot répond à la demande d’appel avec la réponse continue de l’onglet standard et ferme `task/submit` le module de tâche.  L’onglet Carte adaptative est mis à jour en rendant la nouvelle liste de cartes fournie dans le corps de **la** réponse continue de l’onglet.

### <a name="invoke-taskfetch"></a>Invoke `task/fetch`

Le code suivant fournit des exemples de `task/fetch` requête et de réponse :

**`task/fetch` request**
```json
// task/fetch POST request: agents/{botId}/invoke
{
    "name": "task/fetch",
    "value": {
        "data": {
            "type": "task/fetch"
        },
        "context": {
            "theme": "default",
        },
        "tabContext": {
            "tabEntityId": "{tab_entity_id}"
        }
    },
    "imdisplayname": "{user_display_name}",
    "conversation": {
        "id": "{generated_conversation_id}"
    } 
}
```

**`task/fetch` réponse**

```json
// task/fetch POST response: agents/{botId}/invoke
{
    "task": {
        "value": {
            "title": "Ninja Cat",
            "height": "small",
            "width": "small",
            "card": {
                "contentType": "application/vnd.microsoft.card.adaptive",
                "content": adaptiveCard,
            }
        },
    "type": "continue"
    },
    "responseType": "task"
}
```

### <a name="invoke-tasksubmit"></a>Invoke `task/submit`

Le code suivant fournit des exemples de `task/submit` requête et de réponse :

**`task/submit` request**

```json
// task/submit POST request: agent/{botId}/invoke:
{
    "name": "task/submit",
    "value": {
        "data": {serialized_data_object},
        "context": {
            "theme": "default"
        },
    "tabContext": {
        "tabEntityId": "{tab_entity_id}"
        },
    },
    "conversation": {
        "id": "{generated_conversation_id}"
    },
    "imdisplayname": "{user_display_name}",
}
```

**`task/submit` Type de réponse de l’onglet**

```json
// tab/fetch **continue** POST response: 
{
    "task":{
        "value": {
            "tab": {
                "type": "continue",
                "value": {
                    "cards": [
                        {
                            "card": adaptiveCard1
                        },
                        {
                            "card": adaptiveCard2
                        }
                    ]
                }
            }
        },
        "type": "continue"
    },
    "responseType": "task"
}
```

## <a name="authentication"></a>Authentification

Dans les sections précédentes, vous avez vu que la plupart des paradigmes de développement peuvent être étendus des demandes et réponses du module de tâche en demandes d’onglet et en réponses. En ce qui concerne la gestion de l’authentification, le flux de travail de l’onglet Carte adaptative suit le modèle d’authentification pour les extensions de messagerie. Pour plus d’informations, voir [ajouter une authentification.](../../messaging-extensions/how-to/add-authentication.md)

`tab/fetch`les demandes peuvent avoir une **réponse continue** ou **auth.** Lorsqu’une demande est déclenchée et reçoit une réponse d’th d’onglet, la page de signature `tab/fetch` s’affiche à  l’utilisateur.

**Pour obtenir un code d’authentification par le biais de `tab/fetch` l’appel**

1. Ouvrez votre application. La page de signature s’affiche.

    > [!NOTE]
    > Le logo de l’application est fourni par le biais `icon` de la propriété définie dans le manifeste de l’application. Titre qui s’affiche une fois que le logo est défini dans la propriété renvoyée dans le corps de la réponse `title` **d’th** de l’onglet.

1. Sélectionnez **Connexion**. Vous êtes redirigé vers l’URL d’authentification fournie dans la propriété du corps de la `value` réponse d’authentification. 
1. Une fenêtre contextuelle apparaît. Cette fenêtre pop-up héberge votre page web à l’aide de l’URL d’authentification.
1. Après vous être connectez, fermez la fenêtre. Un **code d’authentification** est envoyé au client Teams client.
1. Le Teams ressue ensuite la demande à votre service, qui inclut le code d’authentification fourni `tab/fetch` par votre page web hébergée.

### <a name="tabfetch-authentication-data-flow"></a>`tab/fetch` flux de données d’authentification

L’image suivante fournit une vue d’ensemble du fonctionnement du flux de données d’authentification pour un `tab/fetch` appel.

:::image type="content" source="../../assets/images/tabs/adaptive-cards-tab-auth-flow.png" alt-text="Exemple de flux d’thème d’onglet de carte adaptative." border="false":::

**`tab/fetch` réponse d’th**

Le code suivant fournit un exemple de réponse `tab/fetch` d’th :

```json
// tab/auth POST response (openURL)
{
    "tab": {
        "type": "auth",
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

### <a name="example"></a>Exemple

Le code suivant illustre un exemple de requête rééditée :

```json
{
    "name": "tab/fetch",
    "type": "invoke",
    "timestamp": "2021-01-15T00:10:12.253Z",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer/",
    "from": {
        "id": "{id}",
        "name": "John Smith",
        "aadObjectId": "00000000-0000-0000-0000-000000000000"
    },
    "conversation": {
        "tenantId": "{tenantId}",
        "id": "tab:{guid}"
    },
    "recipients": {
        "id": "28:00000000-0000-0000-0000-000000000000",
        "name": "ContosoApp"
    },
    "entities": [
        {
            "locale": "en-us",
            "country": "US",
            "platform": "Windows",
            "timezone": "America/Los_Angeles",
            "type": "clientInfo"
        }
    ],
    "channelData": {
        "tenant": { "id": "00000000-0000-0000-0000-000000000000" },
        "source": { "name": "message" }
    },
    "value": {
        "tabContext": { "tabEntityId": "homeTab" },
        "state": "0.43195668034524815"
    },
    "locale": "en-US",
    "localTimeZone": "America/Los_Angeles"
}
```

## <a name="code-sample"></a>Exemple de code

|**Exemple de nom** | **Description** |**.NET** | **Node.js** |
|----------------|-----------------|--------------|--------------|
| Afficher les cartes adaptatives dans Teams onglet | Microsoft Teams exemple de code d’onglet, qui montre comment afficher des cartes adaptatives dans Teams. |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-adaptive-cards/csharp)| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-adaptive-cards/nodejs) |

## <a name="see-also"></a>Voir aussi

* [Carte adaptative](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)
* [Teams onglets](~/tabs/what-are-tabs.md)
* [Créer un onglet personnel](~/tabs/how-to/create-personal-tab.md)
* [Créer un onglet de canal ou de groupe](~/tabs/how-to/create-channel-group-tab.md)
* [Onglets sur les appareils mobiles](~/tabs/design/tabs-mobile.md)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Déploiement du lien des onglets et vue des étapes](~/tabs/tabs-link-unfurling.md)
