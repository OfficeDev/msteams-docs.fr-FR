---
title: Créer des onglets de carte adaptative
author: KirtiPereira
description: Créer des onglets à l’aide de cartes adaptatives
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: 4359b20d5839b86955082b7a5da8db262e13600c
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179901"
---
# <a name="build-tabs-with-adaptive-cards"></a><span data-ttu-id="d5ef1-103">Créer des onglets avec les Cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="d5ef1-103">Build tabs with Adaptive Cards</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="d5ef1-104">Cette fonctionnalité est en prévisualisation [publique pour](~/resources/dev-preview/developer-preview-intro.md) les développeurs et est prise en charge sur ordinateur de bureau et mobile.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-104">This feature is in [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md) and is supported in desktop and mobile.</span></span> <span data-ttu-id="d5ef1-105">La prise en charge dans le navigateur web sera bientôt disponible.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-105">Support in the web browser is coming soon.</span></span>
> * <span data-ttu-id="d5ef1-106">Les onglets avec cartes adaptatives sont actuellement uniquement pris en charge en tant qu’applications personnelles.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-106">Tabs with Adaptive Cards are currently only supported as personal apps.</span></span>

<span data-ttu-id="d5ef1-107">Lorsque vous développez un onglet à l’aide de la méthode traditionnelle, vous pouvez être face à ces problèmes, tels que les considérations html et CSS, les temps de chargement lents, les contraintes iFrame, ainsi que la maintenance et les coûts du serveur.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-107">When developing a tab using the traditional method, you might run into these issues, such as HTML and CSS considerations, slow load times, iFrame constraints, and server maintenance and costs.</span></span> <span data-ttu-id="d5ef1-108">Les onglets de carte adaptative sont une nouvelle façon de créer des onglets dans Teams.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-108">Adaptive Card tabs is a new way to build tabs in Teams.</span></span> <span data-ttu-id="d5ef1-109">Au lieu d’incorporer du contenu web dans un IFrame, vous pouvez restituer des cartes adaptatives dans un onglet. Lorsque le frontal est restituer avec des cartes adaptatives, le système frontal est alimenté par un bot.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-109">Instead of embedding web content in an IFrame, you can render Adaptive Cards to a tab. While the front-end is rendered with Adaptive Cards, the backend is powered by a bot.</span></span> <span data-ttu-id="d5ef1-110">Le bot est responsable de l’acceptation des demandes et de la réponse appropriée avec la carte adaptative qui est rendue.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-110">The bot is responsible for accepting requests and responding appropriately with the Adaptive Card that is rendered.</span></span>

<span data-ttu-id="d5ef1-111">Vous pouvez créer vos onglets avec des blocs d’interface utilisateur prêts à l’emploi qui semblent natifs sur ordinateur de bureau, web et mobile.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-111">You can build your tabs with ready-made user interface (UI) Lego-blocks that look and feel native on desktop, web, and mobile.</span></span> <span data-ttu-id="d5ef1-112">Cet article vous aide à comprendre les modifications à apporter au manifeste de l’application, la façon dont l’activité d’appel demande et envoie des informations sous l’onglet avec des cartes adaptatives, ainsi que l’impact sur le flux de travail du module de tâche.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-112">This article helps you understand the changes required to be made to the app manifest, how the invoke activity requests and sends information in tab with Adaptive Cards, and the impact on the task module workflow.</span></span>

<span data-ttu-id="d5ef1-113">L’image suivante illustre les onglets de build avec des cartes adaptatives sur ordinateur de bureau et mobile :</span><span class="sxs-lookup"><span data-stu-id="d5ef1-113">The following image depicts build tabs with Adaptive Cards in desktop and mobile:</span></span>

:::image type="content" source="../../assets/images/tabs/adaptive-cards-rendered-in-tabs.jpg" alt-text="Exemple de carte adaptative rendue dans les onglets." border="false":::

## <a name="prerequisites"></a><span data-ttu-id="d5ef1-115">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="d5ef1-115">Prerequisites</span></span>

<span data-ttu-id="d5ef1-116">Avant de commencer à utiliser des cartes adaptatives pour créer des onglets, vous devez :</span><span class="sxs-lookup"><span data-stu-id="d5ef1-116">Before you start using Adaptive Cards to build tabs, you must:</span></span>

* <span data-ttu-id="d5ef1-117">Familiarisez-vous avec le développement [de bots,](../../bots/what-are-bots.md) [les cartes adaptatives](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)et les [modules de tâche](../../task-modules-and-cards/task-modules/task-modules-bots.md) Teams.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-117">Be familiar with, [bot development](../../bots/what-are-bots.md), [Adaptive Cards](../../task-modules-and-cards/what-are-cards.md#adaptive-cards), and [task modules](../../task-modules-and-cards/task-modules/task-modules-bots.md) in Teams.</span></span>
* <span data-ttu-id="d5ef1-118">Exécutez un bot Teams pour votre développement.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-118">Have a bot running in Teams for your development.</span></span>
* <span data-ttu-id="d5ef1-119">Être en [prévisualisation pour les développeurs publics.](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="d5ef1-119">Be in [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>

## <a name="changes-to-app-manifest"></a><span data-ttu-id="d5ef1-120">Modifications apportées au manifeste de l’application</span><span class="sxs-lookup"><span data-stu-id="d5ef1-120">Changes to app manifest</span></span>

<span data-ttu-id="d5ef1-121">Les applications personnelles qui restituer les onglets doivent inclure un `staticTabs` tableau dans leur manifeste d’application.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-121">Personal apps that render tabs must include a `staticTabs` array in their app manifest.</span></span> <span data-ttu-id="d5ef1-122">Les onglets carte adaptative sont rendus lorsque `contentBotId` la propriété est fournie dans la `staticTab` définition.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-122">Adaptive Card tabs are rendered when the `contentBotId` property is provided in the `staticTab` definition.</span></span> <span data-ttu-id="d5ef1-123">Les définitions d’onglet statique doivent contenir soit un onglet de carte adaptative, soit un onglet de carte adaptative, spécifiant une expérience d’onglet de contenu web hébergé `contentBotId` `contentUrl` classique.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-123">Static tab definitions must contain either a `contentBotId`, specifying an Adaptive Card tab or a `contentUrl`, specifying a typical hosted web content tab experience.</span></span>

> [!NOTE]
> <span data-ttu-id="d5ef1-124">La `contentBotId` propriété est actuellement disponible dans le manifeste version 1.9 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-124">The `contentBotId` property is currently available in manifest version 1.9 or later.</span></span>

<span data-ttu-id="d5ef1-125">Fournissez `contentBotId` la propriété avec `botId` l’onglet Carte adaptative avec qui doit communiquer.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-125">Provide the `contentBotId` property with the `botId` that the Adaptive Card tab must communicate with.</span></span> <span data-ttu-id="d5ef1-126">Le paramètre configuré pour l’onglet Carte adaptative est envoyé dans le paramètre de chaque demande d’appel et peut être utilisé pour différencier les onglets de carte adaptative qui sont alimentés par le `entityId` `tabContext` même bot.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-126">The `entityId` configured for the Adaptive Card tab is sent in the `tabContext` parameter of each invoke request, and can be used to differentiate Adaptive Card Tabs that are powered by the same bot.</span></span> <span data-ttu-id="d5ef1-127">Pour plus d’informations sur les autres champs de définition d’onglet statique, voir [schéma de manifeste.](../../resources/schema/manifest-schema.md#statictabs)</span><span class="sxs-lookup"><span data-stu-id="d5ef1-127">For more information about other static tab definition fields, see [manifest schema](../../resources/schema/manifest-schema.md#statictabs).</span></span>

<span data-ttu-id="d5ef1-128">Voici un exemple de manifeste d’onglet carte adaptative :</span><span class="sxs-lookup"><span data-stu-id="d5ef1-128">Following is a sample Adaptive Card tab manifest:</span></span>

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

## <a name="invoke-activities"></a><span data-ttu-id="d5ef1-129">Appeler des activités</span><span class="sxs-lookup"><span data-stu-id="d5ef1-129">Invoke activities</span></span>

<span data-ttu-id="d5ef1-130">La communication entre l’onglet Carte adaptative et votre bot s’fait par le biais `invoke` d’activités.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-130">Communication between your Adaptive Card tab and your bot is done through `invoke` activities.</span></span> <span data-ttu-id="d5ef1-131">Chaque `invoke` activité a un nom **correspondant.**</span><span class="sxs-lookup"><span data-stu-id="d5ef1-131">Each `invoke` activity has a corresponding **name**.</span></span> <span data-ttu-id="d5ef1-132">Utilisez le nom de chaque activité pour différencier chaque demande.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-132">Use the name of each activity to differentiate each request.</span></span> <span data-ttu-id="d5ef1-133">`tab/fetch` et `tab/submit` sont les activités couvertes dans cette section.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-133">`tab/fetch` and `tab/submit` are the activities covered in this section.</span></span>

### <a name="fetch-adaptive-card-to-render-to-a-tab"></a><span data-ttu-id="d5ef1-134">Récupérer la carte adaptative à restituer dans un onglet</span><span class="sxs-lookup"><span data-stu-id="d5ef1-134">Fetch Adaptive Card to render to a tab</span></span>

<span data-ttu-id="d5ef1-135">`tab/fetch`est la première demande d’appel que votre bot reçoit lorsqu’un utilisateur ouvre un onglet Carte adaptative. Lorsque votre bot reçoit la demande, il envoie une réponse de tabulation **continue** ou une réponse **d’th de tabulation.**</span><span class="sxs-lookup"><span data-stu-id="d5ef1-135">`tab/fetch` is the first invoke request that your bot receives when a user opens an Adaptive Card tab. When your bot receives the request, it either sends a tab **continue** response or a tab **auth** response.</span></span>
<span data-ttu-id="d5ef1-136">La **réponse** continue inclut un tableau pour les **cartes,** qui est rendu verticalement sur l’onglet dans l’ordre du tableau.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-136">The **continue** response includes an array for **cards**, which is rendered vertically to the tab in the order of the array.</span></span>

> [!NOTE]
> <span data-ttu-id="d5ef1-137">Pour plus d’informations sur la réponse **d’authentification,** voir [l’authentification.](#authentication)</span><span class="sxs-lookup"><span data-stu-id="d5ef1-137">For more information on **auth** response, see [authentication](#authentication).</span></span>

<span data-ttu-id="d5ef1-138">Le code suivant fournit des exemples de `tab/fetch` requête et de réponse :</span><span class="sxs-lookup"><span data-stu-id="d5ef1-138">The following code provides examples of `tab/fetch` request and response:</span></span>

<span data-ttu-id="d5ef1-139">**`tab/fetch` request**</span><span class="sxs-lookup"><span data-stu-id="d5ef1-139">**`tab/fetch` request**</span></span>

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

<span data-ttu-id="d5ef1-140">**`tab/fetch` réponse**</span><span class="sxs-lookup"><span data-stu-id="d5ef1-140">**`tab/fetch` response**</span></span>

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

### <a name="handle-submits-from-adaptive-card"></a><span data-ttu-id="d5ef1-141">Gérer les soumissions à partir de la carte adaptative</span><span class="sxs-lookup"><span data-stu-id="d5ef1-141">Handle submits from Adaptive Card</span></span>

<span data-ttu-id="d5ef1-142">Une fois qu’une carte adaptative est restituer dans l’onglet, elle doit être en mesure de répondre aux interactions de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-142">After an Adaptive Card is rendered in the tab, it must be able to respond to user interactions.</span></span> <span data-ttu-id="d5ef1-143">Cette réponse est gérée par la demande `tab/submit` d’appel.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-143">This response is handled by the `tab/submit` invoke request.</span></span>

<span data-ttu-id="d5ef1-144">Lorsqu’un utilisateur sélectionne un bouton sous l’onglet Carte adaptative, la demande est déclenchée à votre bot avec les données correspondantes par le biais de la `tab/submit` `Action.Submit` fonction de carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-144">When a user selects a button on the Adaptive Card tab, the `tab/submit` request is triggered to your bot with the corresponding data through the `Action.Submit` function of Adaptive Card.</span></span> <span data-ttu-id="d5ef1-145">Les données de carte adaptative sont disponibles via la propriété de données de la `tab/submit` demande.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-145">The Adaptive Card data is available through the data property of the `tab/submit` request.</span></span> <span data-ttu-id="d5ef1-146">Vous recevez l’une des réponses suivantes à votre demande :</span><span class="sxs-lookup"><span data-stu-id="d5ef1-146">You receive either of the following responses to your request:</span></span>

* <span data-ttu-id="d5ef1-147">Réponse de code d’état HTTP `200` sans corps.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-147">An HTTP status code `200` response with no body.</span></span> <span data-ttu-id="d5ef1-148">Une réponse 200 vide n’entraîne aucune action du client.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-148">An empty 200 response results in no action taken by the client.</span></span>
* <span data-ttu-id="d5ef1-149">L’onglet standard `200` **continue la** réponse, comme expliqué dans récupérer la [carte adaptative](#fetch-adaptive-card-to-render-to-a-tab).</span><span class="sxs-lookup"><span data-stu-id="d5ef1-149">The standard `200` tab **continue** response, as explained in [fetch Adaptive Card](#fetch-adaptive-card-to-render-to-a-tab).</span></span> <span data-ttu-id="d5ef1-150">Une réponse **de tabulation continue** déclenche la mise à jour de l’onglet Carte adaptative rendue par le client avec les cartes adaptatives fournies dans le tableau de cartes de la **réponse continue.**</span><span class="sxs-lookup"><span data-stu-id="d5ef1-150">A tab **continue** response triggers the client to update the rendered Adaptive Card tab with the Adaptive Cards provided in the cards array of the **continue** response.</span></span>

<span data-ttu-id="d5ef1-151">Le code suivant fournit des exemples de `tab/submit` requête et de réponse :</span><span class="sxs-lookup"><span data-stu-id="d5ef1-151">The following code provides examples of `tab/submit` request and response:</span></span>

<span data-ttu-id="d5ef1-152">**`tab/submit` request**</span><span class="sxs-lookup"><span data-stu-id="d5ef1-152">**`tab/submit` request**</span></span>

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

<span data-ttu-id="d5ef1-153">**`tab/submit` réponse**</span><span class="sxs-lookup"><span data-stu-id="d5ef1-153">**`tab/submit` response**</span></span>

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

## <a name="understand-task-module-workflow"></a><span data-ttu-id="d5ef1-154">Comprendre le flux de travail du module de tâche</span><span class="sxs-lookup"><span data-stu-id="d5ef1-154">Understand task module workflow</span></span>

<span data-ttu-id="d5ef1-155">Le module de tâche utilise également la carte adaptative pour appeler `task/fetch` et les demandes et les `task/submit` réponses.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-155">The task module also uses Adaptive Card to invoke `task/fetch` and `task/submit` requests and responses.</span></span> <span data-ttu-id="d5ef1-156">Pour plus d’informations, [voir l’utilisation des modules de tâche Microsoft Teams bots.](../../task-modules-and-cards/task-modules/task-modules-bots.md)</span><span class="sxs-lookup"><span data-stu-id="d5ef1-156">For more information, see [using Task Modules in Microsoft Teams bots](../../task-modules-and-cards/task-modules/task-modules-bots.md).</span></span>

<span data-ttu-id="d5ef1-157">Avec l’introduction de l’onglet Carte adaptative, il existe un changement dans la façon dont le bot répond à une `task/submit` demande.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-157">With the introduction of Adaptive Card tab, there is a change in how the bot responds to a `task/submit` request.</span></span> <span data-ttu-id="d5ef1-158">Si vous utilisez un onglet Carte adaptative, le bot répond à la demande d’appel avec la réponse continue de l’onglet standard et ferme `task/submit` le module de tâche. </span><span class="sxs-lookup"><span data-stu-id="d5ef1-158">If you are using an Adaptive Card tab, the bot responds to the `task/submit` invoke request with the standard tab **continue** response, and closes the task module.</span></span> <span data-ttu-id="d5ef1-159">L’onglet Carte adaptative est mis à jour en rendant la nouvelle liste de cartes fournie dans le corps de **la** réponse continue de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-159">The Adaptive Card tab is updated by rendering the new list of cards provided in the tab **continue** response body.</span></span>

### <a name="invoke-taskfetch"></a><span data-ttu-id="d5ef1-160">Invoke `task/fetch`</span><span class="sxs-lookup"><span data-stu-id="d5ef1-160">Invoke `task/fetch`</span></span>

<span data-ttu-id="d5ef1-161">Le code suivant fournit des exemples de `task/fetch` requête et de réponse :</span><span class="sxs-lookup"><span data-stu-id="d5ef1-161">The following code provides examples of `task/fetch` request and response:</span></span>

<span data-ttu-id="d5ef1-162">**`task/fetch` request**</span><span class="sxs-lookup"><span data-stu-id="d5ef1-162">**`task/fetch` request**</span></span>
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

<span data-ttu-id="d5ef1-163">**`task/fetch` réponse**</span><span class="sxs-lookup"><span data-stu-id="d5ef1-163">**`task/fetch` response**</span></span>

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

### <a name="invoke-tasksubmit"></a><span data-ttu-id="d5ef1-164">Invoke `task/submit`</span><span class="sxs-lookup"><span data-stu-id="d5ef1-164">Invoke `task/submit`</span></span>

<span data-ttu-id="d5ef1-165">Le code suivant fournit des exemples de `task/submit` requête et de réponse :</span><span class="sxs-lookup"><span data-stu-id="d5ef1-165">The following code provides examples of `task/submit` request and response:</span></span>

<span data-ttu-id="d5ef1-166">**`task/submit` request**</span><span class="sxs-lookup"><span data-stu-id="d5ef1-166">**`task/submit` request**</span></span>

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

<span data-ttu-id="d5ef1-167">**`task/submit` Type de réponse de l’onglet**</span><span class="sxs-lookup"><span data-stu-id="d5ef1-167">**`task/submit` tab response type**</span></span>

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

## <a name="authentication"></a><span data-ttu-id="d5ef1-168">Authentification</span><span class="sxs-lookup"><span data-stu-id="d5ef1-168">Authentication</span></span>

<span data-ttu-id="d5ef1-169">Dans les sections précédentes de cet article, vous avez vu que la plupart des paradigmes de développement peuvent être étendus des demandes de module de tâche et des réponses en demandes et réponses d’onglet.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-169">In the previous sections of this article, you have seen that most of the development paradigms can be extended from the task module requests and responses into tab requests and responses.</span></span> <span data-ttu-id="d5ef1-170">En ce qui concerne la gestion de l’authentification, le flux de travail de l’onglet Carte adaptative suit le modèle d’authentification pour les extensions de messagerie.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-170">When it comes to handling authentication, the workflow for Adaptive Card tab follows the authentication pattern for messaging extensions.</span></span> <span data-ttu-id="d5ef1-171">Pour plus d’informations, voir [ajouter une authentification.](../../messaging-extensions/how-to/add-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="d5ef1-171">For more information, see [add authentication](../../messaging-extensions/how-to/add-authentication.md).</span></span>

<span data-ttu-id="d5ef1-172">`tab/fetch`les demandes peuvent avoir une **réponse continue** ou **auth.**</span><span class="sxs-lookup"><span data-stu-id="d5ef1-172">`tab/fetch` requests can have either a **continue** or an **auth** response.</span></span> <span data-ttu-id="d5ef1-173">Lorsqu’une demande est déclenchée et reçoit une réponse d' auto-th de tabulation, la page de signature `tab/fetch` s’affiche à  l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-173">When a `tab/fetch` request is triggered and receives a tab **auth** response, the sign-in page is shown to the user.</span></span>

<span data-ttu-id="d5ef1-174">**Pour obtenir un code d’authentification par le biais de `tab/fetch` l’appel**</span><span class="sxs-lookup"><span data-stu-id="d5ef1-174">**To get an authentication code through `tab/fetch` invoke**</span></span>

1. <span data-ttu-id="d5ef1-175">Ouvrez votre application.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-175">Open your app.</span></span> <span data-ttu-id="d5ef1-176">La page de signature s’affiche.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-176">The sign in page appears.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d5ef1-177">Le logo de l’application est fourni par le biais `icon` de la propriété définie dans le manifeste de l’application.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-177">The app logo is provided through the `icon` property defined in the app manifest.</span></span> <span data-ttu-id="d5ef1-178">Titre qui s’affiche une fois que le logo est défini dans la propriété renvoyée dans le corps de la réponse `title` **d’th** de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-178">The title appearing after the logo is defined in the `title` property returned in the tab **auth** response body.</span></span>

1. <span data-ttu-id="d5ef1-179">Sélectionnez **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-179">Select **Sign in**.</span></span> <span data-ttu-id="d5ef1-180">Vous êtes redirigé vers l’URL d’authentification fournie dans `value` la propriété du corps de la réponse d’authentification. </span><span class="sxs-lookup"><span data-stu-id="d5ef1-180">You are redirected to the authentication URL provided in the `value` property of the **auth** response body.</span></span>
1. <span data-ttu-id="d5ef1-181">Une fenêtre contextuelle apparaît.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-181">A pop-up window appears.</span></span> <span data-ttu-id="d5ef1-182">Cette fenêtre pop-up héberge votre page web à l’aide de l’URL d’authentification.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-182">This pop-up window hosts your web page using the authentication URL.</span></span>
1. <span data-ttu-id="d5ef1-183">Après vous être connectez, fermez la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-183">After you sign in, close the window.</span></span> <span data-ttu-id="d5ef1-184">Un **code d’authentification** est envoyé au client Teams client.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-184">An **authentication code** is sent to the Teams client.</span></span>
1. <span data-ttu-id="d5ef1-185">Le Teams client ressue ensuite la demande à votre service, qui inclut le code d’authentification fourni `tab/fetch` par votre page web hébergée.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-185">The Teams client then reissues the `tab/fetch` request to your service, which includes the authentication code provided by your hosted web page.</span></span>

### <a name="tabfetch-authentication-data-flow"></a><span data-ttu-id="d5ef1-186">`tab/fetch` flux de données d’authentification</span><span class="sxs-lookup"><span data-stu-id="d5ef1-186">`tab/fetch` authentication data flow</span></span>

<span data-ttu-id="d5ef1-187">L’image suivante fournit une vue d’ensemble du fonctionnement du flux de données d’authentification pour un `tab/fetch` appel.</span><span class="sxs-lookup"><span data-stu-id="d5ef1-187">The following image provides an overview of how the authentication data flow works for a `tab/fetch` invoke.</span></span>

:::image type="content" source="../../assets/images/tabs/adaptive-cards-tab-auth-flow.png" alt-text="Exemple de flux d’thème d’onglet de carte adaptative." border="false":::

<span data-ttu-id="d5ef1-189">**`tab/fetch` réponse d’th**</span><span class="sxs-lookup"><span data-stu-id="d5ef1-189">**`tab/fetch` auth response**</span></span>

<span data-ttu-id="d5ef1-190">Le code suivant fournit un exemple de réponse `tab/fetch` d’th :</span><span class="sxs-lookup"><span data-stu-id="d5ef1-190">The following code provides an example of `tab/fetch` auth response:</span></span>

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

### <a name="example"></a><span data-ttu-id="d5ef1-191">Exemple</span><span class="sxs-lookup"><span data-stu-id="d5ef1-191">Example</span></span>

<span data-ttu-id="d5ef1-192">Le code suivant illustre un exemple de requête rééditée :</span><span class="sxs-lookup"><span data-stu-id="d5ef1-192">The following code shows a reissued request example:</span></span>

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

## <a name="see-also"></a><span data-ttu-id="d5ef1-193">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="d5ef1-193">See also</span></span>

* [<span data-ttu-id="d5ef1-194">Carte adaptative</span><span class="sxs-lookup"><span data-stu-id="d5ef1-194">Adaptive Card</span></span>](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)
* [<span data-ttu-id="d5ef1-195">Teams onglets</span><span class="sxs-lookup"><span data-stu-id="d5ef1-195">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="d5ef1-196">Créer un onglet personnel</span><span class="sxs-lookup"><span data-stu-id="d5ef1-196">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
* [<span data-ttu-id="d5ef1-197">Créer un onglet de canal ou de groupe</span><span class="sxs-lookup"><span data-stu-id="d5ef1-197">Create a channel or group tab</span></span>](~/tabs/how-to/create-channel-group-tab.md)
* [<span data-ttu-id="d5ef1-198">Onglets sur les appareils mobiles</span><span class="sxs-lookup"><span data-stu-id="d5ef1-198">Tabs on mobile</span></span>](~/tabs/design/tabs-mobile.md)

## <a name="next-step"></a><span data-ttu-id="d5ef1-199">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="d5ef1-199">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d5ef1-200">Déploiement du lien des onglets et vue des étapes</span><span class="sxs-lookup"><span data-stu-id="d5ef1-200">Tabs link unfurling and Stage View</span></span>](~/tabs/tabs-link-unfurling.md)