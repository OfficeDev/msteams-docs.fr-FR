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
# <a name="build-tabs-with-adaptive-cards"></a><span data-ttu-id="9fbde-103">Créer des onglets avec les Cartes adaptatives</span><span class="sxs-lookup"><span data-stu-id="9fbde-103">Build tabs with Adaptive Cards</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="9fbde-104">Cette fonctionnalité est en prévisualisation [publique pour](~/resources/dev-preview/developer-preview-intro.md) les développeurs et est prise en charge sur ordinateur de bureau et mobile.</span><span class="sxs-lookup"><span data-stu-id="9fbde-104">This feature is in [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md) and is supported in desktop and mobile.</span></span> <span data-ttu-id="9fbde-105">La prise en charge dans le navigateur web sera bientôt disponible.</span><span class="sxs-lookup"><span data-stu-id="9fbde-105">Support in the web browser is coming soon.</span></span>
> * <span data-ttu-id="9fbde-106">Les onglets avec cartes adaptatives sont actuellement uniquement pris en charge en tant qu’applications personnelles.</span><span class="sxs-lookup"><span data-stu-id="9fbde-106">Tabs with Adaptive Cards are currently only supported as personal apps.</span></span>

<span data-ttu-id="9fbde-107">Utilisez des cartes adaptatives pour créer des onglets en toute simplicité.</span><span class="sxs-lookup"><span data-stu-id="9fbde-107">Use Adaptive Cards to build tabs with ease.</span></span> <span data-ttu-id="9fbde-108">Vous pouvez créer vos onglets avec des blocs d’interface utilisateur prêts à l’emploi qui semblent natifs sur ordinateur de bureau, web et mobile.</span><span class="sxs-lookup"><span data-stu-id="9fbde-108">You can build your tabs with ready-made UI Lego-blocks that look and feel native on desktop, web, and mobile.</span></span> <span data-ttu-id="9fbde-109">La création d’onglets avec des cartes adaptatives centralise toutes les fonctionnalités d’application Teams autour d’un système principal de bot et d’un frontal de carte adaptative, ce qui élimine la nécessité d’un autre système principal pour votre bot et vos onglets.</span><span class="sxs-lookup"><span data-stu-id="9fbde-109">Building tabs with Adaptive Cards centralizes all Teams app capabilities around a bot backend and Adaptive Card frontend, thus, eliminating the need for a different backend for your bot and tabs.</span></span> <span data-ttu-id="9fbde-110">Cela réduit considérablement les coûts de maintenance et de serveur de votre Teams app.</span><span class="sxs-lookup"><span data-stu-id="9fbde-110">This greatly reduces server and maintenance costs of your Teams app.</span></span> <span data-ttu-id="9fbde-111">Cet article vous aide à comprendre les modifications à apporter au manifeste de l’application, la façon dont l’activité d’appel demande et envoie des informations sous l’onglet avec des cartes adaptatives et l’impact sur le flux de travail du module de tâche.</span><span class="sxs-lookup"><span data-stu-id="9fbde-111">This article helps you understand the changes required to be made to the app manifest, how the invoke activity requests and sends information in tab with Adaptive Cards, and the impact on the task module workflow.</span></span> 

L’image suivante illustre les onglets de build avec cartes adaptatives dans les ordinateurs de bureau et mobiles : exemple de carte adaptative :::image type="content" source="../../assets/images/tabs/adaptive-cards-rendered-in-tabs.jpg" alt-text="restituer dans les onglets." border="false":::

## <a name="prerequisites"></a><span data-ttu-id="9fbde-113">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="9fbde-113">Prerequisites</span></span>

<span data-ttu-id="9fbde-114">Avant de commencer à utiliser des cartes adaptatives pour créer des onglets, vous devez :</span><span class="sxs-lookup"><span data-stu-id="9fbde-114">Before you start using Adaptive Cards to build tabs, you must:</span></span>

* <span data-ttu-id="9fbde-115">Familiarisez-vous avec le développement [de bots,](../../bots/what-are-bots.md) [les cartes adaptatives](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)et les [modules](../../task-modules-and-cards/task-modules/task-modules-bots.md) de tâche Teams.</span><span class="sxs-lookup"><span data-stu-id="9fbde-115">Be familiar with, [bot development](../../bots/what-are-bots.md), [Adaptive Cards](../../task-modules-and-cards/what-are-cards.md#adaptive-cards), and [Task Modules](../../task-modules-and-cards/task-modules/task-modules-bots.md) in Teams.</span></span>
* <span data-ttu-id="9fbde-116">Exécutez un bot Teams pour votre développement.</span><span class="sxs-lookup"><span data-stu-id="9fbde-116">Have a bot running in Teams for your development.</span></span>
* <span data-ttu-id="9fbde-117">Être en [prévisualisation pour les développeurs publics.](~/resources/dev-preview/developer-preview-intro.md)</span><span class="sxs-lookup"><span data-stu-id="9fbde-117">Be in [Public Developer Preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>

## <a name="changes-to-app-manifest"></a><span data-ttu-id="9fbde-118">Modifications apportées au manifeste de l’application</span><span class="sxs-lookup"><span data-stu-id="9fbde-118">Changes to app manifest</span></span>

<span data-ttu-id="9fbde-119">Les applications personnelles qui restituer les onglets doivent inclure un `staticTabs` tableau dans leur manifeste d’application.</span><span class="sxs-lookup"><span data-stu-id="9fbde-119">Personal apps that render tabs must include a `staticTabs` array in their app manifest.</span></span> <span data-ttu-id="9fbde-120">L’onglet Carte adaptative est restituer lorsque `contentBotId` la propriété est fournie dans la `staticTab` définition.</span><span class="sxs-lookup"><span data-stu-id="9fbde-120">Adaptive Card Tab are rendered when the `contentBotId` property is provided in the `staticTab` definition.</span></span> <span data-ttu-id="9fbde-121">Les définitions d’onglet statique doivent contenir soit un onglet de carte adaptative, soit un onglet de carte adaptative, spécifiant une expérience d’onglet de contenu web hébergé `contentBotId` `contentUrl` classique.</span><span class="sxs-lookup"><span data-stu-id="9fbde-121">Static tab definitions must contain either a `contentBotId`, specifying an Adaptive Card Tab or a `contentUrl`, specifying a typical hosted web content tab experience.</span></span>

> [!NOTE]
> <span data-ttu-id="9fbde-122">La `contentBotId` propriété est actuellement disponible version manifeste 1.9 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="9fbde-122">The `contentBotId` property is currently available manifest version 1.9 or later.</span></span> 

<span data-ttu-id="9fbde-123">Fournissez `contentBotId` la propriété avec la communication avec l’onglet Carte `botId` adaptative.</span><span class="sxs-lookup"><span data-stu-id="9fbde-123">Provide the `contentBotId` property with the `botId` that the Adaptive Card Tab must communicate with.</span></span> <span data-ttu-id="9fbde-124">Le paramètre configuré pour l’onglet Carte adaptative est envoyé dans le paramètre de chaque demande d’appel et peut être utilisé pour différencier les différents onglets de carte adaptative qui sont alimentés par le `entityId` `tabContext` même bot.</span><span class="sxs-lookup"><span data-stu-id="9fbde-124">The `entityId` configured for the Adaptive Card Tab is sent in the `tabContext` parameter of each invoke request, and can be used to differentiate different Adaptive Card Tabs that are powered by the same bot.</span></span> <span data-ttu-id="9fbde-125">Pour plus d’informations sur les autres champs de définition d’onglet statique, voir [schéma de manifeste.](../../resources/schema/manifest-schema.md#statictabs)</span><span class="sxs-lookup"><span data-stu-id="9fbde-125">For more information about other static tab definition fields, see [manifest schema](../../resources/schema/manifest-schema.md#statictabs).</span></span>

<span data-ttu-id="9fbde-126">Voici un exemple de manifeste d’onglet de carte adaptative :</span><span class="sxs-lookup"><span data-stu-id="9fbde-126">Following is a sample Adaptive Card Tab manifest:</span></span>

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

## <a name="invoke-activities"></a><span data-ttu-id="9fbde-127">Appeler des activités</span><span class="sxs-lookup"><span data-stu-id="9fbde-127">Invoke activities</span></span>

<span data-ttu-id="9fbde-128">La communication entre votre onglet de carte adaptative et votre bot s’fait par le biais `invoke` d’activités.</span><span class="sxs-lookup"><span data-stu-id="9fbde-128">Communication between your Adaptive Card Tab and your bot is done through `invoke` activities.</span></span> <span data-ttu-id="9fbde-129">Chaque `invoke` activité a un nom *correspondant.*</span><span class="sxs-lookup"><span data-stu-id="9fbde-129">Each `invoke` activity has a corresponding *name*.</span></span> <span data-ttu-id="9fbde-130">Utilisez le nom de chaque activité pour différencier chaque demande.</span><span class="sxs-lookup"><span data-stu-id="9fbde-130">Use the name of each activity to differentiate each request.</span></span> <span data-ttu-id="9fbde-131">`tab/fetch` et `tab/submit` sont les activités couvertes dans cette section.</span><span class="sxs-lookup"><span data-stu-id="9fbde-131">`tab/fetch` and `tab/submit` are the activities covered in this section.</span></span>

### <a name="fetch-adaptive-card-to-render-to-a-tab"></a><span data-ttu-id="9fbde-132">Récupérer la carte adaptative à restituer dans un onglet</span><span class="sxs-lookup"><span data-stu-id="9fbde-132">Fetch Adaptive Card to render to a tab</span></span>

<span data-ttu-id="9fbde-133">`tab/fetch` est la première demande d’appel que votre bot reçoit lorsqu’un utilisateur ouvre un onglet de carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="9fbde-133">`tab/fetch` is the first invoke request that your bot receives when a user opens an Adaptive Card Tabs.</span></span> <span data-ttu-id="9fbde-134">Lorsque votre bot reçoit la demande, il envoie une réponse de tabulation **continue** ou une réponse **d’th de tabulation.**</span><span class="sxs-lookup"><span data-stu-id="9fbde-134">When your bot receives the request, it will either send a tab **continue** response or a tab **auth** response.</span></span>
<span data-ttu-id="9fbde-135">La **réponse** continue inclut un tableau pour les **cartes,** qui est rendu verticalement sur l’onglet dans l’ordre du tableau.</span><span class="sxs-lookup"><span data-stu-id="9fbde-135">The **continue** response includes an array for **cards**, which is rendered vertically to the tab in the order of the array.</span></span>

> [!NOTE]
> <span data-ttu-id="9fbde-136">La **réponse d’authentification** est expliquée en détail dans la section [authentification.](#authentication)</span><span class="sxs-lookup"><span data-stu-id="9fbde-136">The **auth** response is explained in detail in the [authentication](#authentication) section.</span></span>

<span data-ttu-id="9fbde-137">Les extraits de code suivants sont des exemples de `tab/fetch` requête et de réponse :</span><span class="sxs-lookup"><span data-stu-id="9fbde-137">The following code snippets are examples of `tab/fetch` request and response:</span></span>

<span data-ttu-id="9fbde-138">**`tab/fetch` request**</span><span class="sxs-lookup"><span data-stu-id="9fbde-138">**`tab/fetch` request**</span></span>

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

<span data-ttu-id="9fbde-139">**`tab/fetch` réponse**</span><span class="sxs-lookup"><span data-stu-id="9fbde-139">**`tab/fetch` response**</span></span>

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

### <a name="handle-submits-from-adaptive-card"></a><span data-ttu-id="9fbde-140">Gérer les soumissions à partir de la carte adaptative</span><span class="sxs-lookup"><span data-stu-id="9fbde-140">Handle submits from Adaptive Card</span></span>

<span data-ttu-id="9fbde-141">Une fois qu’une carte adaptative est restituer dans l’onglet, elle doit être en mesure de répondre aux interactions de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9fbde-141">After an Adaptive Card is rendered in the tab, it must be able to respond to user interactions.</span></span> <span data-ttu-id="9fbde-142">Cette réponse est gérée par la demande `tab/submit` d’appel.</span><span class="sxs-lookup"><span data-stu-id="9fbde-142">This response is handled by the `tab/submit` invoke request.</span></span>

<span data-ttu-id="9fbde-143">Lorsqu’un utilisateur sélectionne un bouton dans l’onglet Carte adaptative, la demande est déclenchée à votre bot avec les données correspondantes via la fonction `tab/submit` *Action.Submit* de carte adaptative.</span><span class="sxs-lookup"><span data-stu-id="9fbde-143">When a user selects a button on the Adaptive Card Tab, the `tab/submit` request is triggered to your bot with the corresponding data through the *Action.Submit* function of Adaptive Card.</span></span> <span data-ttu-id="9fbde-144">Les données de carte adaptative sont disponibles via la propriété de données de la `tab/submit` demande.</span><span class="sxs-lookup"><span data-stu-id="9fbde-144">The Adaptive Card data is available through the data property of the `tab/submit` request.</span></span> <span data-ttu-id="9fbde-145">Vous recevrez l’une des réponses suivantes à votre demande :</span><span class="sxs-lookup"><span data-stu-id="9fbde-145">You will receive either of the following responses to your request:</span></span>

* <span data-ttu-id="9fbde-146">Réponse de code d’état http `200` sans corps.</span><span class="sxs-lookup"><span data-stu-id="9fbde-146">A http status code `200` response with no body.</span></span> <span data-ttu-id="9fbde-147">Une réponse 200 vide n’entraîne aucune action du client.</span><span class="sxs-lookup"><span data-stu-id="9fbde-147">An empty 200 response will result in no action taken by the client.</span></span>
* <span data-ttu-id="9fbde-148">L’onglet standard `200` **continue la** réponse, comme expliqué dans la section Récupérer la carte [adaptative.](#fetch-adaptive-card-to-render-to-a-tab)</span><span class="sxs-lookup"><span data-stu-id="9fbde-148">The standard `200` tab **continue** response, as explained in [Fetch Adaptive Card](#fetch-adaptive-card-to-render-to-a-tab) section.</span></span> <span data-ttu-id="9fbde-149">Une réponse **de suite** d’onglet déclenche le client pour mettre à jour l’onglet carte adaptative rendu avec les cartes adaptatives fournies dans le tableau de cartes de la **réponse continue.**</span><span class="sxs-lookup"><span data-stu-id="9fbde-149">A tab **continue** response triggers the client to update the rendered Adaptive Card Tab with the Adaptive Cards provided in the cards array of the **continue** response.</span></span>

<span data-ttu-id="9fbde-150">Les extraits de code suivants sont des exemples de `tab/submit` requête et de réponse :</span><span class="sxs-lookup"><span data-stu-id="9fbde-150">The following code snippets are examples of `tab/submit` request and response:</span></span>

<span data-ttu-id="9fbde-151">**`tab/submit` request**</span><span class="sxs-lookup"><span data-stu-id="9fbde-151">**`tab/submit` request**</span></span>

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

<span data-ttu-id="9fbde-152">**`tab/submit` réponse**</span><span class="sxs-lookup"><span data-stu-id="9fbde-152">**`tab/submit` response**</span></span>

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

## <a name="understand-task-module-workflow"></a><span data-ttu-id="9fbde-153">Comprendre le flux de travail du module de tâche</span><span class="sxs-lookup"><span data-stu-id="9fbde-153">Understand task module workflow</span></span>

<span data-ttu-id="9fbde-154">Le module de tâche utilise également la carte adaptative pour appeler `task/fetch` et les demandes et les `task/submit` réponses.</span><span class="sxs-lookup"><span data-stu-id="9fbde-154">The task module also uses Adaptive Card to invoke `task/fetch` and `task/submit` requests and responses.</span></span> <span data-ttu-id="9fbde-155">Pour plus d’informations, voir [Using Task Modules in Microsoft Teams bots](../../task-modules-and-cards/task-modules/task-modules-bots.md).</span><span class="sxs-lookup"><span data-stu-id="9fbde-155">For more information, see [Using Task Modules in Microsoft Teams bots](../../task-modules-and-cards/task-modules/task-modules-bots.md).</span></span>

<span data-ttu-id="9fbde-156">Toutefois, avec l’introduction de l’onglet Carte adaptative, il existe un changement dans la façon dont le bot répond à une `task/submit` demande.</span><span class="sxs-lookup"><span data-stu-id="9fbde-156">However, with the introduction of Adaptive Card Tab there is a change in how the bot responds to a `task/submit` request.</span></span> <span data-ttu-id="9fbde-157">Si vous utilisez un onglet de carte adaptative, le bot répond à la demande d’appel avec la réponse continue de l’onglet standard et ferme `task/submit` le module de tâche. </span><span class="sxs-lookup"><span data-stu-id="9fbde-157">If you are using an Adaptive Card Tab, the bot responds to the `task/submit` invoke request with the standard tab **continue** response, and closes the task module.</span></span> <span data-ttu-id="9fbde-158">L’onglet Carte adaptative est mis à jour en rendant la nouvelle liste de cartes fournie dans le corps de **la** réponse continue de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="9fbde-158">The Adaptive Card Tab is updated by rendering the new list of cards provided in the tab **continue** response body.</span></span>

### <a name="invoke-taskfetch"></a><span data-ttu-id="9fbde-159">Invoke `task/fetch`</span><span class="sxs-lookup"><span data-stu-id="9fbde-159">Invoke `task/fetch`</span></span>

<span data-ttu-id="9fbde-160">Les extraits de code suivants sont des exemples de `task/fetch` requête et de réponse :</span><span class="sxs-lookup"><span data-stu-id="9fbde-160">The following code snippets are examples of `task/fetch` request and response:</span></span>

<span data-ttu-id="9fbde-161">**`task/fetch` request**</span><span class="sxs-lookup"><span data-stu-id="9fbde-161">**`task/fetch` request**</span></span>
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

<span data-ttu-id="9fbde-162">**`task/fetch` réponse**</span><span class="sxs-lookup"><span data-stu-id="9fbde-162">**`task/fetch` response**</span></span>

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

### <a name="invoke-tasksubmit"></a><span data-ttu-id="9fbde-163">Invoke `task/submit`</span><span class="sxs-lookup"><span data-stu-id="9fbde-163">Invoke `task/submit`</span></span>

<span data-ttu-id="9fbde-164">Les extraits de code suivants sont des exemples de `task/submit` requête et de réponse :</span><span class="sxs-lookup"><span data-stu-id="9fbde-164">The following code snippets are examples of `task/submit` request and response:</span></span>

<span data-ttu-id="9fbde-165">**`task/submit` request**</span><span class="sxs-lookup"><span data-stu-id="9fbde-165">**`task/submit` request**</span></span>

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

<span data-ttu-id="9fbde-166">**`task/submit` Type de réponse de l’onglet**</span><span class="sxs-lookup"><span data-stu-id="9fbde-166">**`task/submit` tab response type**</span></span>

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

## <a name="authentication"></a><span data-ttu-id="9fbde-167">Authentification</span><span class="sxs-lookup"><span data-stu-id="9fbde-167">Authentication</span></span>

<span data-ttu-id="9fbde-168">Dans les sections précédentes de cet article, vous avez vu que la plupart des paradigmes de développement pouvaient être extrapolés à partir des demandes de module de tâche et des réponses dans les demandes d’onglet et les réponses.</span><span class="sxs-lookup"><span data-stu-id="9fbde-168">In the previous sections of this article, you have seen that most of the development paradigms could be extrapolated from the task module requests and responses into tab requests and responses.</span></span> <span data-ttu-id="9fbde-169">Toutefois, en matière de gestion de l’authentification, le flux de travail de l’onglet Carte adaptative suit le modèle d’authentification pour les extensions de messagerie.</span><span class="sxs-lookup"><span data-stu-id="9fbde-169">However, when it comes to handling authentication, the workflow for Adaptive Card Tab follows the authentication pattern for messaging extensions.</span></span> <span data-ttu-id="9fbde-170">Pour plus d’informations, voir [ajouter une authentification.](../../messaging-extensions/how-to/add-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="9fbde-170">For more information, see [add authentication](../../messaging-extensions/how-to/add-authentication.md).</span></span> 

<span data-ttu-id="9fbde-171">Dans la section [Appeler les activités,](#invoke-activities) vous avez été informé que les demandes peuvent avoir une réponse continue ou `tab/fetch` **auth.** </span><span class="sxs-lookup"><span data-stu-id="9fbde-171">In the [invoke activities](#invoke-activities) section, you were informed that `tab/fetch` requests can have either a **continue** or an **auth** response.</span></span> <span data-ttu-id="9fbde-172">Lorsqu’une demande est déclenchée et reçoit une réponse d' auto-th de tabulation, la page de signature `tab/fetch` s’affiche à  l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9fbde-172">When a `tab/fetch` request is triggered and receives a tab **auth** response, the sign-in page is shown to the user.</span></span> 

<span data-ttu-id="9fbde-173">**Pour obtenir un code d’authentification par le biais de `tab/fetch` l’appel**</span><span class="sxs-lookup"><span data-stu-id="9fbde-173">**To get an authentication code through `tab/fetch` invoke**</span></span>

1. <span data-ttu-id="9fbde-174">Ouvrez votre application.</span><span class="sxs-lookup"><span data-stu-id="9fbde-174">Open your app.</span></span> <span data-ttu-id="9fbde-175">La page de signature s’affiche.</span><span class="sxs-lookup"><span data-stu-id="9fbde-175">The sign in page appears.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9fbde-176">Le logo de l’application est fourni par le biais de la propriété définie dans le manifeste de l’application, et le titre qui apparaît une fois le logo défini dans la propriété renvoyée dans le corps de la réponse d’th de `icon` `title` l’onglet. </span><span class="sxs-lookup"><span data-stu-id="9fbde-176">The app logo is provided through the `icon` property defined in the app manifest, and the title appearing after the logo is defined in the `title` property returned in the tab **auth** response body.</span></span>

1. <span data-ttu-id="9fbde-177">Sélectionnez **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="9fbde-177">Select **Sign in**.</span></span> <span data-ttu-id="9fbde-178">Vous êtes redirigé vers l’URL d’authentification fournie dans `value` la propriété du corps de la réponse d’authentification. </span><span class="sxs-lookup"><span data-stu-id="9fbde-178">You are redirected to the authentication URL provided in the `value` property of the **auth** response body.</span></span> 
1. <span data-ttu-id="9fbde-179">Une fenêtre contextuelle apparaît.</span><span class="sxs-lookup"><span data-stu-id="9fbde-179">A pop-up window appears.</span></span> <span data-ttu-id="9fbde-180">Cette fenêtre pop-up héberge votre page web à l’aide de l’URL d’authentification.</span><span class="sxs-lookup"><span data-stu-id="9fbde-180">This pop-up window hosts your web page using the authentication URL.</span></span>
1. <span data-ttu-id="9fbde-181">Après vous être connectez, fermez la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="9fbde-181">After you sign in, close the window.</span></span> <span data-ttu-id="9fbde-182">Un *code d’authentification* est envoyé au client Teams client.</span><span class="sxs-lookup"><span data-stu-id="9fbde-182">An *authentication code* is sent to the Teams client.</span></span>
1. <span data-ttu-id="9fbde-183">Le Teams ressue ensuite la demande à votre service, qui inclut le code d’authentification fourni `tab/fetch` par votre page web hébergée.</span><span class="sxs-lookup"><span data-stu-id="9fbde-183">The Teams client then reissues the `tab/fetch` request to your service, which includes the authentication code provided by your hosted web page.</span></span> 

### <a name="tabfetch-authentication-data-flow"></a><span data-ttu-id="9fbde-184">`tab/fetch` flux de données d’authentification</span><span class="sxs-lookup"><span data-stu-id="9fbde-184">`tab/fetch` authentication data flow</span></span>

<span data-ttu-id="9fbde-185">L’image suivante fournit une vue d’ensemble du fonctionnement du flux de données d’authentification pour un `tab/fetch` appel.</span><span class="sxs-lookup"><span data-stu-id="9fbde-185">The following image provides an overview of how the authentication data flow works for a `tab/fetch` invoke.</span></span>

:::image type="content" source="../../assets/images/tabs/adaptive-cards-tab-auth-flow.png" alt-text="Exemple de flux d’thème d’onglet de carte adaptative." border="false":::

<span data-ttu-id="9fbde-187">**`tab/fetch` réponse d’th**</span><span class="sxs-lookup"><span data-stu-id="9fbde-187">**`tab/fetch` auth response**</span></span>

<span data-ttu-id="9fbde-188">L’extrait de code suivant est un exemple de réponse `tab/fetch` d’th :</span><span class="sxs-lookup"><span data-stu-id="9fbde-188">The following code snippet is an example of `tab/fetch` auth response:</span></span>

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

### <a name="example"></a><span data-ttu-id="9fbde-189">Exemple</span><span class="sxs-lookup"><span data-stu-id="9fbde-189">Example</span></span>

<span data-ttu-id="9fbde-190">Voici un exemple de requête rééditée :</span><span class="sxs-lookup"><span data-stu-id="9fbde-190">The following shows a reissued request example:</span></span>

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

## <a name="see-also"></a><span data-ttu-id="9fbde-191">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="9fbde-191">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9fbde-192">Carte adaptative</span><span class="sxs-lookup"><span data-stu-id="9fbde-192">Adaptive Card</span></span>](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)

