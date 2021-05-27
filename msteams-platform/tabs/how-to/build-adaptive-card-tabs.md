---
title: Créer des onglets de carte adaptative
author: KirtiPereira
description: Créer des onglets à l’aide de cartes adaptatives
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: d65fc537b5282c050d891a6a73ff114c630e2c1c
ms.sourcegitcommit: c59d90ae03eae32996db49f162855965b55c52fe
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/26/2021
ms.locfileid: "52668847"
---
# <a name="build-tabs-with-adaptive-cards"></a>Créer des onglets avec des cartes adaptatives

> [!IMPORTANT]
> * Cette fonctionnalité est en prévisualisation [publique pour](~/resources/dev-preview/developer-preview-intro.md) les développeurs et est prise en charge sur ordinateur de bureau et mobile. La prise en charge dans le navigateur web sera bientôt disponible.
> * Les onglets avec cartes adaptatives sont actuellement uniquement pris en charge en tant qu’applications personnelles.

Utilisez des cartes adaptatives pour créer des onglets en toute simplicité. Vous pouvez créer vos onglets avec des blocs d’interface utilisateur prêts à l’emploi qui semblent natifs sur ordinateur de bureau, web et mobile. La création d’onglets avec des cartes adaptatives centralise toutes les fonctionnalités d’application Teams autour d’un système principal de bot et d’un frontal de carte adaptative, ce qui élimine la nécessité d’un autre système principal pour votre bot et vos onglets. Cela réduit considérablement les coûts de maintenance et de serveur de votre Teams app. Cet article vous aide à comprendre les modifications à apporter au manifeste de l’application, la façon dont l’activité d’appel demande et envoie des informations sous l’onglet avec des cartes adaptatives et l’impact sur le flux de travail du module de tâche. 

L’image suivante illustre les onglets de build avec des cartes adaptatives dans les ordinateurs de bureau et mobiles : exemple de carte adaptative :::image type="content" source="../../assets/images/tabs/adaptive-cards-rendered-in-tabs.jpg" alt-text="restituer dans les onglets." border="false":::

## <a name="prerequisites"></a>Conditions préalables

Avant de commencer à utiliser des cartes adaptatives pour créer des onglets, vous devez :

* Familiarisez-vous avec le développement [de bots,](../../bots/what-are-bots.md) [les cartes adaptatives](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)et les [modules](../../task-modules-and-cards/task-modules/task-modules-bots.md) de tâche Teams.
* Exécutez un bot Teams pour votre développement.
* Être en [prévisualisation pour les développeurs publics.](~/resources/dev-preview/developer-preview-intro.md)

## <a name="changes-to-app-manifest"></a>Modifications apportées au manifeste de l’application

Les applications personnelles qui restituer les onglets doivent inclure un `staticTabs` tableau dans leur manifeste d’application. L’onglet Carte adaptative est restituer lorsque `contentBotId` la propriété est fournie dans la `staticTab` définition. Les définitions d’onglet statique doivent contenir soit un onglet de carte adaptative, soit un onglet de carte adaptative, spécifiant une expérience d’onglet de contenu web hébergé `contentBotId` `contentUrl` classique.

> [!NOTE]
> La `contentBotId` propriété est actuellement disponible version manifeste 1.9 ou ultérieure. 

Fournissez `contentBotId` la propriété avec la communication avec l’onglet Carte `botId` adaptative. Le paramètre configuré pour l’onglet Carte adaptative est envoyé dans le paramètre de chaque demande d’appel et peut être utilisé pour différencier les différents onglets de carte adaptative qui sont alimentés par le `entityId` `tabContext` même bot. Pour plus d’informations sur les autres champs de définition d’onglet statique, voir [schéma de manifeste.](../../resources/schema/manifest-schema.md#statictabs)

Voici un exemple de manifeste d’onglet de carte adaptative :

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

La communication entre votre onglet de carte adaptative et votre bot s’fait par le biais `invoke` d’activités. Chaque `invoke` activité a un nom *correspondant.* Utilisez le nom de chaque activité pour différencier chaque demande. `tab/fetch` et `tab/submit` sont les activités couvertes dans cette section.

### <a name="fetch-adaptive-card-to-render-to-a-tab"></a>Récupérer la carte adaptative à restituer dans un onglet

`tab/fetch` est la première demande d’appel que votre bot reçoit lorsqu’un utilisateur ouvre un onglet de carte adaptative. Lorsque votre bot reçoit la demande, il envoie une réponse de tabulation **continue** ou une réponse **d’th de tabulation.**
La **réponse** continue inclut un tableau pour **les cartes,** qui est rendu verticalement sur l’onglet dans l’ordre du tableau.

> [!NOTE]
> La **réponse d’authentification** est expliquée en détail dans la section [authentification.](#authentication)

Les extraits de code suivants sont des exemples de `tab/fetch` requête et de réponse :

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

Une fois qu’une carte adaptative est restituer dans l’onglet, elle doit être en mesure de répondre aux interactions de l’utilisateur. Cette réponse est gérée par la demande `tab/submit` d’appel.

Lorsqu’un utilisateur sélectionne un bouton dans l’onglet Carte adaptative, la demande est déclenchée à votre bot avec les données correspondantes via la fonction `tab/submit` *Action.Submit* de carte adaptative. Les données de carte adaptative sont disponibles via la propriété de données de la `tab/submit` demande. Vous recevrez l’une des réponses suivantes à votre demande :

* Réponse de code d’état http `200` sans corps. Une réponse 200 vide n’entraîne aucune action du client.
* L’onglet standard `200` **continue la** réponse, comme expliqué dans la section Récupérer la carte [adaptative.](#fetch-adaptive-card-to-render-to-a-tab) Une réponse **de tabulation** continue déclenche le client pour mettre à jour l’onglet carte adaptative rendu avec les cartes adaptatives fournies dans le tableau de cartes de la **réponse continue.**

Les extraits de code suivants sont des exemples de `tab/submit` requête et de réponse :

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

Le module de tâche utilise également la carte adaptative pour appeler `task/fetch` et les demandes et les `task/submit` réponses. Pour plus d’informations, voir [Using Task Modules in Microsoft Teams bots](../../task-modules-and-cards/task-modules/task-modules-bots.md).

Toutefois, avec l’introduction de l’onglet Carte adaptative, il existe un changement dans la façon dont le bot répond à une `task/submit` demande. Si vous utilisez un onglet de carte adaptative, le bot répond à la demande d’appel avec la réponse continue de l’onglet standard et ferme `task/submit` le module de tâche.  L’onglet Carte adaptative est mis à jour en rendant la nouvelle liste de cartes fournie dans le corps de **la** réponse continue de l’onglet.

### <a name="invoke-taskfetch"></a>Invoke `task/fetch`

Les extraits de code suivants sont des exemples de `task/fetch` requête et de réponse :

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

Les extraits de code suivants sont des exemples de `task/submit` requête et de réponse :

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

Dans les sections précédentes de cet article, vous avez vu que la plupart des paradigmes de développement pouvaient être extrapolés à partir des demandes de module de tâche et des réponses en demandes et réponses d’onglet. Toutefois, en matière de gestion de l’authentification, le flux de travail de l’onglet Carte adaptative suit le modèle d’authentification pour les extensions de messagerie. Pour plus d’informations, voir [ajouter une authentification.](../../messaging-extensions/how-to/add-authentication.md) 

Dans la section [Appeler les activités,](#invoke-activities) vous avez été informé que les demandes peuvent avoir une réponse continue ou `tab/fetch` **auth.**  Lorsqu’une demande est déclenchée et reçoit une réponse d' auto-th de tabulation, la page de signature `tab/fetch` s’affiche à  l’utilisateur. 

**Pour obtenir un code d’authentification par le biais de `tab/fetch` l’appel**

1. Ouvrez votre application. La page de signature s’affiche.

    > [!NOTE]
    > Le logo de l’application est fourni par le biais de la propriété définie dans le manifeste de l’application, et le titre qui apparaît une fois le logo défini dans la propriété renvoyée dans le corps de la réponse d’th de `icon` `title` l’onglet. 

1. Sélectionnez **Se connecter**. Vous êtes redirigé vers l’URL d’authentification fournie dans `value` la propriété du corps de la réponse d’authentification.  
1. Une fenêtre contextuelle apparaît. Cette fenêtre pop-up héberge votre page web à l’aide de l’URL d’authentification.
1. Après vous être connectez, fermez la fenêtre. Un *code d’authentification* est envoyé au client Teams client.
1. Le Teams client ressue ensuite la demande à votre service, qui inclut le code d’authentification fourni `tab/fetch` par votre page web hébergée. 

### <a name="tabfetch-authentication-data-flow"></a>`tab/fetch` flux de données d’authentification

L’image suivante fournit une vue d’ensemble du fonctionnement du flux de données d’authentification pour un `tab/fetch` appel.

:::image type="content" source="../../assets/images/tabs/adaptive-cards-tab-auth-flow.png" alt-text="Exemple de flux d’thème d’onglet de carte adaptative." border="false":::

**`tab/fetch` réponse d’th**

L’extrait de code suivant est un exemple de réponse `tab/fetch` d’th :

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

Voici un exemple de requête rééditée :

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

## <a name="see-also"></a>Voir aussi

> [!div class="nextstepaction"]
> [Carte adaptative](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)

