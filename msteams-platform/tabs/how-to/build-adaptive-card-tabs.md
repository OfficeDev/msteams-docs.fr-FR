---
title: Construire des onglets de carte adaptatifs
author: KirtiPereira
description: Apprenez à créer des onglets à l’aide de cartes adaptatives où le serveur frontal est rendu avec des cartes adaptatives, le serveur principal est alimenté par un bot. Explorez les activités d’appel et gérez les envois.
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: high
ms.openlocfilehash: 33c9d42ff2d2d5d13676261c7197e287fcacff59
ms.sourcegitcommit: 176bbca74ba46b7ac298899d19a2d75087fb37c1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/04/2022
ms.locfileid: "68376626"
---
# <a name="build-tabs-with-adaptive-cards"></a>Créer des onglets avec les Cartes adaptatives

> [!IMPORTANT]
>
> Les onglets avec des cartes adaptatives ne sont actuellement pris en charge que comme applications personnelles.

Lorsque vous développez un onglet en utilisant la méthode traditionnelle, vous pouvez rencontrer ces problèmes :

* Considérations sur le HTML et le CSS
* Temps de chargement lent
* Contraintes iFrame
* Maintenance et coûts des serveurs

Les onglets de carte adaptative sont une nouvelle façon de construire des onglets dans Teams. Au lieu d'intégrer du contenu web dans une IFrame, vous pouvez rendre les cartes adaptatives dans un onglet. Alors que la partie frontale est rendue avec des cartes adaptatives, la partie arrière est alimentée par un robot. Le robot est chargé d'accepter les demandes et de répondre de manière appropriée avec la carte adaptative qui est rendue.

Vous pouvez créer vos onglets à l'aide de modules d'interface utilisateur prêts à l'emploi, natifs des ordinateurs de bureau, du web et des téléphones mobiles. Cet article vous aide à comprendre les modifications à apporter au manifeste de l'application. L'article explique également comment l'activité d'invocation demande et envoie des informations dans l'onglet des cartes adaptatives, et son effet sur le flux de travail du module de tâches.

L'image suivante montre des onglets de construction avec les cartes adaptatives sur le bureau et le mobile :

:::image type="content" source="../../assets/images/adaptive-cards-rendered-in-tabs.png" alt-text="Exemple de carte adaptative rendue dans les onglets.":::

## <a name="prerequisites"></a>Configuration requise

Avant de commencer à utiliser les cartes adaptatives pour construire des onglets, vous devez :

* Connaître le [développement de robots](../../bots/what-are-bots.md), [les cartes adaptatives ](https://adaptivecards.io/)et [les modules de tâches dans](../../task-modules-and-cards/task-modules/task-modules-bots.md) Teams.
* Faites fonctionner un robot dans Teams pour votre développement.

## <a name="changes-to-app-manifest"></a>Modifications du manifeste de l'application

Les applications personnelles qui rendent les onglets doivent inclure `staticTabs`un tableau dans leur manifeste d'application.. Les onglets de la carte adaptative sont rendus lorsque la `contentBotId`propriété est fournie dans`staticTab` la définition. Les définitions d'onglets statiques doivent contenir soit un , `contentBotId`spécifiant un onglet de carte adaptative`contentUrl`, soit un , spécifiant un onglet de contenu Web hébergé typique.

> [!NOTE]
> Cette `contentBotId`propriété est actuellement disponible dans la version manifeste 1.9 ou ultérieure.

Indiquez la `contentBotId`propriété avec laquelle`botId` l'onglet Carte adaptative doit communiquer. La `entityId`configuration de l'onglet de la carte adaptative est envoyée dans le `tabContext`paramètre de chaque demande d'invocation, et peut être utilisée pour différencier les onglets de la carte adaptative qui sont alimentés par le même robot. Pour plus d'informations sur les autres champs de définition des onglets statiques, voir le [schéma du manifeste](../../resources/schema/manifest-schema.md#statictabs).

Voici un exemple de manifeste de l'onglet Carte adaptative :

```json
{
  "$schema": "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
  "manifestVersion": "1.9",
  "id": "00000000-0000-0000-0000-000000000000",
  "version": "0.0.1",
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

## <a name="invoke-activities"></a>Invoquer des activités

La communication entre votre onglet de carte adaptative et votre robot se fait par le biais d'activités.`invoke`d’activités. Chaque `invoke` activité a un **nom** correspondant. Utilisez le nom de chaque activité pour différencier chaque demande. `tab/fetch` et `tab/submit` sont les activités couvertes dans cette section.

> [!NOTE]
>
> * Les robots doivent envoyer toutes les réponses à [l'URL du service](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#base-uri&preserve-view=true). L'URL du service est reçu dans le cadre des données utiles `activity`entrantes.
> * La taille de la charge utile de l'invocation a augmenté à 80kb.

### <a name="fetch-adaptive-card-to-render-to-a-tab"></a>Récupérer la carte adaptative pour la rendre dans un onglet

`tab/fetch` est la première demande d'invocation que votre robot reçoit lorsqu'un utilisateur ouvre un onglet de carte adaptative. Lorsque votre robot reçoit cette requête, il envoie soit une réponse onglet **continu** , soit une réponse onglet **authentifié** .de tabulation.
La réponse **continue** inclut un tableau pour **les cartes**, qui est affiché verticalement dans l’onglet dans l’ordre du tableau.

> [!NOTE]
> Pour plus d’informations sur la réponse **d’authentification** , consultez [l’authentification](#authentication).

Le code suivant fournit des exemples de demande et de `tab/fetch` réponse :

**`tab/fetch` demande**

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
                },
                {
                    "card": adaptiveCard3
                }  
            ]
        },
    },
    "responseType": "tab"
}
```

### <a name="handle-submits-from-adaptive-card"></a>Traiter les soumissions de la carte adaptative

Une fois qu'une carte adaptative est rendue dans l'onglet, elle peut répondre aux interactions de l'utilisateur. Cette réponse est traitée par la `tab/submit`demande d'invocation.

Lorsqu'un utilisateur sélectionne un bouton dans l'onglet Carte adaptative, la `tab/submit`demande est déclenchée vers votre robot avec les données correspondantes via la `Action.Submit`fonction de la Carte adaptative. Les données de la carte adaptative sont disponibles via la propriété data de la `tab/submit`demande. Vous recevez l'une des réponses suivantes à votre demande :

* Une réponse de `200`code d'état HTTP sans corps. Une réponse 200 vide n'entraîne aucune action de la part du client.
* La réponse de `200`l'onglet **standard continue**, comme expliqué dans la [carte adaptative de récupération](#fetch-adaptive-card-to-render-to-a-tab). Une réponse **continue** e l'onglet déclenche la mise à jour par le client de l'onglet de carte adaptative rendu avec les cartes adaptatives fournies dans le tableau de cartes de la **réponse** continue.

Le code suivant fournit des exemples de `tab/submit`demande et de réponse :

**`tab/submit` demande**

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

Le module de tâches utilise également la carte adaptative pour invoquer des demandes `task/fetch`et `task/submit`des réponses. Pour plus d'informations, voir [l'utilisation des modules de tâches dans les robots de Microsoft Teams](../../task-modules-and-cards/task-modules/task-modules-bots.md).

Avec l'introduction de l'onglet Carte adaptative, la façon dont le robot répond à une `task/submit`demande a changé. Si vous utilisez un onglet de carte adaptative, le robot répond à la demande `task/submit`d'invocation par la réponse standard de l'onglet **continue** et ferme le module de tâche. L'onglet Carte adaptative est mis à jour en rendant la nouvelle liste de cartes fournie dans le corps de réponse de l'onglet **continue**.

### <a name="invoke-taskfetch"></a>Invoquer `task/fetch`

Le code suivant fournit des exemples de`task/fetch` demande et de réponse :

**`task/fetch` demande**

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

### <a name="invoke-tasksubmit"></a>Invoquer `task/submit`

Le code suivant fournit des exemples de `task/submit`demande et de réponse :

**`task/submit` demande**

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

**`task/submit` onglet type de réponse**

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

Dans les sections précédentes, vous avez vu que la plupart des paradigmes de développement peuvent être étendus des demandes et réponses du module de tâche aux demandes et réponses de l'onglet. En ce qui concerne la gestion de l'authentification, le flux de travail pour l'onglet Carte adaptative suit le modèle d'authentification pour les extensions de message. Pour plus d'informations, voir [Ajouter l'authentification](../../messaging-extensions/how-to/add-authentication.md).

`tab/fetch` les demandes peuvent avoir une **réponse continue** ou une réponse **d’authentification** . Lorsqu'une `tab/fetch`requête est déclenchée et qu'elle reçoit une réponse **d'authentification par onglet,** la page de connexion est affichée à l'utilisateur..

**Pour obtenir un code d'authentification en invoquant `tab/fetch`**

1. Ouvrez votre application. La page de connexion apparaît.

    > [!NOTE]
    > Le logo de l'application est fourni par la `icon`propriété définie dans le manifeste de l'application. Le titre apparaissant après le logo est défini dans la `title`propriété retournée dans le corps de la réponse de l'onglet **d'authentification**.

1. Sélectionnez **Connexion**. Vous êtes redirigé vers l'URL d'authentification fournie dans la `value`propriété du corps de la réponse **d'authentification**.
1. Une fenêtre contextuelle apparaît. Cette fenêtre pop-up héberge votre page web en utilisant l'URL d'authentification.
1. Après vous être connecté, fermez la fenêtre. Un code **d'authentification est envoyé** au client Teams.
1. Le client Teams réitère ensuite la `tab/fetch`demande à votre service, qui inclut le code d'authentification fourni par votre page Web hébergée.

### <a name="tabfetch-authentication-data-flow"></a>`tab/fetch` flux de données d’authentification

L'image suivante donne une vue d'ensemble du fonctionnement du flux de données d'authentification pour une `tab/fetch`invocation.

:::image type="content" source="../../assets/images/tabs/adaptive-cards-tab-auth-flow.png" alt-text="Exemple de flux d'authentification de l'onglet Carte adaptative.":::

**`tab/fetch`Exemple de flux d'authentification de l'onglet Carte adaptative.**

Le code suivant fournit un exemple de réponse `tab/fetch`d'authentification :

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

Le code suivant montre un exemple de demande rééditée :

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
| Afficher les cartes adaptatives dans l'onglet Équipes | L'exemple de code de l'onglet Microsoft Teams, qui montre comment afficher les cartes adaptatives dans Teams. |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-adaptive-cards/csharp)| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-adaptive-cards/nodejs) |

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Déploiement du lien des onglets et vue de scène](~/tabs/tabs-link-unfurling.md)

## <a name="see-also"></a>Voir aussi

* [Carte adaptative](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)
* [onglets Teams](~/tabs/what-are-tabs.md)
* [Créer un onglet personnel](~/tabs/how-to/create-personal-tab.md)
* [Créer un onglet de canal ou de groupe](~/tabs/how-to/create-channel-group-tab.md)
* [Onglets sur les appareils mobiles](~/tabs/design/tabs-mobile.md)
* [Commentaires sur l’achèvement du formulaire](~/bots/how-to/conversations/conversation-messages.md#form-completion-feedback)
