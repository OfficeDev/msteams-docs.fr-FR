---
title: Créer des onglets de carte adaptative
author: KirtiPereira
description: Découvrez comment créer des onglets à l’aide de cartes adaptatives avec des exemples de code, notamment l’appel d’activités, la compréhension du flux de travail du module de tâches et l’authentification.
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: none
keywords: flux de données d’authentification d’application personnelle de carte adaptative
ms.openlocfilehash: 95507373671f9044bec788e981f66931b4588705
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104524"
---
# <a name="build-tabs-with-adaptive-cards"></a>Créer des onglets avec les Cartes adaptatives

> [!IMPORTANT]
>
> * Les onglets avec cartes adaptatives sont actuellement pris en charge uniquement en tant qu’applications personnelles.

Lorsque vous développez un onglet à l’aide de la méthode traditionnelle, vous pouvez rencontrer les problèmes suivants :

* Considérations html et CSS
* Temps de chargement lents
* Contraintes iFrame
* Maintenance et coûts du serveur

Les onglets de carte adaptative constituent un nouveau moyen de créer des onglets dans Teams. Au lieu d’incorporer du contenu web dans un IFrame, vous pouvez afficher des cartes adaptatives dans un onglet. Tandis que le serveur frontal est rendu avec des cartes adaptatives, le back-end est alimenté par un bot. Le bot est responsable de l’acceptation des demandes et de la réponse appropriée avec la carte adaptative qui est rendue.

Vous pouvez créer vos onglets avec des blocs de construction d’interface utilisateur prêts à l’utilisation natifs sur les ordinateurs de bureau, le web et les appareils mobiles. Cet article vous aide à comprendre les modifications à apporter au manifeste de l’application. L’article identifie également la façon dont l’activité d’appel demande et envoie des informations dans l’onglet avec cartes adaptatives, et son effet sur le flux de travail du module de tâches.

L’image suivante montre des onglets de build avec des cartes adaptatives dans le bureau et le mobile :

:::image type="content" source="../../assets/images/adaptive-cards-rendered-in-tabs.png" alt-text="Exemple de carte adaptative rendue dans des onglets." border="false":::

## <a name="prerequisites"></a>Conditions préalables

Avant de commencer à utiliser des cartes adaptatives pour générer des onglets, vous devez :

* Familiarisez-vous avec [le développement de bots](../../bots/what-are-bots.md), [les cartes adaptatives](https://adaptivecards.io/) et [les modules de tâches](../../task-modules-and-cards/task-modules/task-modules-bots.md) dans Teams.
* Disposez d’un bot en cours d’exécution dans Teams pour votre développement.

## <a name="changes-to-app-manifest"></a>Modifications apportées au manifeste de l’application

Les applications personnelles qui affichent des onglets doivent inclure un `staticTabs` tableau dans leur manifeste d’application. Les onglets de carte adaptative sont rendus lorsque la `contentBotId` propriété est fournie dans la `staticTab` définition. Les définitions d’onglet statique doivent contenir un `contentBotId`onglet , spécifiant un onglet Carte adaptative ou un `contentUrl`, spécifiant une expérience d’onglet de contenu web hébergée classique.

> [!NOTE]
> La `contentBotId` propriété est actuellement disponible dans le manifeste version 1.9 ou ultérieure.

Indiquez la `contentBotId` propriété avec laquelle l’onglet `botId` Carte adaptative doit communiquer. L’onglet `entityId` Carte adaptative configuré est envoyé dans le `tabContext` paramètre de chaque demande d’appel et peut être utilisé pour différencier les onglets de carte adaptative qui sont alimentés par le même bot. Pour plus d’informations sur les autres champs de définition d’onglet statique, consultez [le schéma de manifeste](../../resources/schema/manifest-schema.md#statictabs).

Voici un exemple de manifeste de l’onglet Carte adaptative :

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

La communication entre votre onglet Carte adaptative et votre bot s’effectue par le biais `invoke` d’activités. Chaque `invoke` activité a un **nom** correspondant. Utilisez le nom de chaque activité pour différencier chaque requête. `tab/fetch` et `tab/submit` sont les activités décrites dans cette section.

> [!NOTE]
>
> * Les bots doivent envoyer toutes les réponses à [l’URL du service](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#base-uri&preserve-view=true). L’URL du service est reçue dans le cadre de la charge utile entrante `activity` .
> * La taille de la charge utile d’appel est passée à 80 Ko.

### <a name="fetch-adaptive-card-to-render-to-a-tab"></a>Récupérer la carte adaptative pour effectuer un rendu dans un onglet

`tab/fetch` est la première demande d’appel que votre bot reçoit lorsqu’un utilisateur ouvre un onglet Carte adaptative. Lorsque votre bot reçoit la demande, il envoie une réponse **continue** d’onglet ou une réponse **d’authentification** de tabulation.
La réponse **continue** inclut un tableau pour **les cartes**, qui est affiché verticalement dans l’onglet dans l’ordre du tableau.

> [!NOTE]
> Pour plus d’informations sur la réponse **d’authentification** , consultez [l’authentification](#authentication).

Le code suivant fournit des exemples de demande et de `tab/fetch` réponse :

**`tab/fetch` Demande**

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

**`tab/fetch` Réponse**

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

### <a name="handle-submits-from-adaptive-card"></a>Gérer les envois à partir d’une carte adaptative

Une fois qu’une carte adaptative est affichée dans l’onglet, elle peut répondre aux interactions utilisateur. Cette réponse est gérée par la requête d’appel `tab/submit` .

Lorsqu’un utilisateur sélectionne un bouton sous l’onglet Carte adaptative, la `tab/submit` demande est déclenchée sur votre bot avec les données correspondantes via la `Action.Submit` fonction carte adaptative. Les données de la carte adaptative sont disponibles via la propriété de données de la `tab/submit` demande. Vous recevez l’une des réponses suivantes à votre demande :

* Réponse de code `200` d’état HTTP sans corps. Une réponse vide de 200 n’entraîne aucune action du client.
* L’onglet standard `200` **continue** la réponse, comme expliqué dans [la récupération de la carte adaptative](#fetch-adaptive-card-to-render-to-a-tab). Une réponse **continue** d’onglet déclenche la mise à jour de l’onglet Carte adaptative rendue par le client avec les cartes adaptatives fournies dans le tableau de cartes de la réponse **continue** .

Le code suivant fournit des exemples de demande et de `tab/submit` réponse :

**`tab/submit` Demande**

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

**`tab/submit` Réponse**

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

## <a name="understand-task-module-workflow"></a>Comprendre le flux de travail du module de tâches

Le module de tâche utilise également la carte adaptative pour appeler `task/fetch` et `task/submit` demander et répondre. Pour plus d’informations, consultez [l’utilisation de modules de tâches dans Microsoft Teams bots](../../task-modules-and-cards/task-modules/task-modules-bots.md).

Avec l’introduction de l’onglet Carte adaptative, la façon dont le bot répond à une `task/submit` demande change. Si vous utilisez un onglet Carte adaptative, le bot répond à la `task/submit` demande d’appel avec l’onglet standard **continuer** la réponse et ferme le module de tâche. L’onglet Carte adaptative est mis à jour en affichant la nouvelle liste de cartes fournie dans le corps de la réponse **continue** de l’onglet.

### <a name="invoke-taskfetch"></a>Invoquer `task/fetch`

Le code suivant fournit des exemples de demande et de `task/fetch` réponse :

**`task/fetch` Demande**

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

**`task/fetch` Réponse**

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

Le code suivant fournit des exemples de demande et de `task/submit` réponse :

**`task/submit` Demande**

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

**`task/submit` type de réponse d’onglet**

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

Dans les sections précédentes, vous avez vu que la plupart des paradigmes de développement peuvent être étendus des demandes et réponses du module de tâche aux demandes et réponses d’onglet. Lorsqu’il s’agit de gérer l’authentification, l’onglet Flux de travail de la carte adaptative suit le modèle d’authentification pour les extensions de message. Pour plus d’informations, consultez [ajouter l’authentification](../../messaging-extensions/how-to/add-authentication.md).

`tab/fetch` les demandes peuvent avoir une **réponse continue** ou une réponse **d’authentification** . Lorsqu’une `tab/fetch` requête est déclenchée et reçoit une réponse **d’authentification** par onglet, la page de connexion s’affiche à l’utilisateur.

**Pour obtenir un code d’authentification via l’appel `tab/fetch`**

1. Ouvrez votre application. La page de connexion s’affiche.

    > [!NOTE]
    > Le logo de l’application est fourni par le biais de la `icon` propriété définie dans le manifeste de l’application. Titre apparaissant après la définition du logo dans la `title` propriété retournée dans le corps de la réponse **d’authentification** de l’onglet.

1. Sélectionnez **Connexion**. Vous êtes redirigé vers l’URL d’authentification fournie dans la `value` propriété du corps de la réponse **d’authentification** .
1. Une fenêtre contextuelle apparaît. Cette fenêtre contextuelle héberge votre page web à l’aide de l’URL d’authentification.
1. Après vous être connecté, fermez la fenêtre. Un **code d’authentification** est envoyé au client Teams.
1. Le client Teams réexécutera ensuite la `tab/fetch` demande à votre service, qui inclut le code d’authentification fourni par votre page web hébergée.

### <a name="tabfetch-authentication-data-flow"></a>`tab/fetch` flux de données d’authentification

L’image suivante fournit une vue d’ensemble du fonctionnement du flux de données d’authentification pour un `tab/fetch` appel.

:::image type="content" source="../../assets/images/tabs/adaptive-cards-tab-auth-flow.png" alt-text="Exemple de flux d’authentification onglet carte adaptative." border="false":::

**`tab/fetch` réponse d’authentification**

Le code suivant fournit un exemple de réponse d’authentification `tab/fetch` :

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

Le code suivant montre un exemple de requête rééditée :

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
| Afficher les cartes adaptatives sous l’onglet Teams | Microsoft Teams exemple de code de l’onglet, qui montre comment afficher les cartes adaptatives dans Teams. |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-adaptive-cards/csharp)| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-adaptive-cards/nodejs) |

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Déploiement de liens d’onglets et mode Étape](~/tabs/tabs-link-unfurling.md)

## <a name="see-also"></a>Voir aussi

* [Carte adaptative](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)
* [onglets Teams](~/tabs/what-are-tabs.md)
* [Créer un onglet personnel](~/tabs/how-to/create-personal-tab.md)
* [Créer un canal ou un onglet de groupe](~/tabs/how-to/create-channel-group-tab.md)
* [Onglets sur les appareils mobiles](~/tabs/design/tabs-mobile.md)
* [Commentaires sur l’achèvement du formulaire](~/bots/how-to/conversations/conversation-messages.md#form-completion-feedback)
