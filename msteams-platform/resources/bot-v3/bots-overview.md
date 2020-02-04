---
title: Ajouter des robots aux applications Microsoft teams
description: Décrit comment commencer à développer des robots dans Microsoft teams
keywords: développement de robots de teams
ms.date: 05/20/2018
ms.openlocfilehash: 0ecb268c34275e958103c9905b2ed1f0858cafda
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673573"
---
# <a name="add-bots-to-microsoft-teams-apps"></a>Ajouter des robots aux applications Microsoft teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Créez et connectez des bots intelligentes pour interagir avec les utilisateurs de Microsoft teams naturellement par le biais de la conversation. Ou fournissez un robot simple basé sur des commandes, à utiliser comme interface de ligne de commande pour votre expérience d’application de teams plus large. Vous pouvez créer un robot de notification uniquement, qui peut transmettre directement les informations pertinentes à vos utilisateurs dans un canal ou un message direct. Vous pouvez même mettre votre robot basé sur une infrastructure de robot et ajouter une prise en charge spécifique aux équipes pour rendre votre expérience plus précise.

![Exemple de robot Assistant d’un utilisateur](~/assets/images/bot_example.png)

## <a name="what-you-need-to-know-bots"></a>Ce que vous devez savoir : robots

Un bot s’affiche comme n’importe quel autre membre de l’équipe avec lequel vous interagissez dans une conversation, à l’exception d’une icône avatar hexagonale qui est toujours en ligne.

Un bot se comporte différemment en fonction du type de conversation concernée. Dans Teams, les robots prennent en charge plusieurs types de conversations (appelés étendues dans le manifeste de l' [application](~/resources/schema/manifest-schema.md)).

* `teams`Également appelés conversations de canal
* `personal`Conversations entre un bot et un utilisateur unique
* `groupChat`Conversation entre un bot et 2 utilisateurs ou plus

Pour plus d’informations, consultez [la rubrique conversation avec un robot Microsoft teams](~/resources/bot-v3/bot-conversations/bots-conversations.md) .

Avec les applications Microsoft Teams, vous pouvez faire du robot l’étoile de votre expérience ou simplement une assistance. Les robots sont distribués dans le cadre de votre package d’applications plus large, qui peut inclure d’autres fonctionnalités, telles que les [onglets](~/tabs/what-are-tabs.md) ou les [extensions de messagerie](~/messaging-extensions/what-are-messaging-extensions.md).

## <a name="bot-apis"></a>API bot

Microsoft teams prend en charge la plupart de [Microsoft bot Framework](https://dev.botframework.com/). (Si vous disposez déjà d’un bot basé sur l’infrastructure de robot, vous pouvez facilement l’adapter pour fonctionner dans Microsoft Teams.) Nous vous recommandons d’utiliser C# ou node. js pour tirer parti de nos [Kits de développement](/microsoftteams/platform/#pivot=sdk-tools)logiciel (SDK). Ces packages étendent les méthodes et classes du kit de développement logiciel (SDK) de base de générateur de robots :

* Utilisation de types de carte spécialisés comme la carte connecteur Office 365
* Consommation et définition des données de canal spécifiques aux équipes sur les activités
* Traitement des demandes d’extension de messagerie

Les extensions du SDK installent des dépendances, notamment le kit de développement logiciel (SDK) du générateur.

* **.Net** Pour utiliser les extensions de Microsoft teams pour le kit de développement logiciel (SDK) du générateur de robots pour .NET, installez le package NuGet [Microsoft. Bot. Connector. teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) dans votre projet Visual Studio.
* **Node. js** pour utiliser les extensions Microsoft teams pour le kit de développement logiciel (SDK) du générateur de robots pour node. js, ajoutez le package NPM [botbuilder-teams](https://www.npmjs.com/package/botbuilder-teams) .
* **Code source** Vous pouvez trouver le code source complet des extensions dans le [BotBuilder-MicrosoftTeams](https://github.com/OfficeDev/BotBuilder-MicrosoftTeams) référentiel sur GitHub.

> [!IMPORTANT]
> Vous pouvez développer des applications teams dans n’importe quelle autre technologie de programmation Web et appeler directement les [API REST de l’infrastructure bot](/bot-framework/rest-api/bot-framework-rest-overview) , mais vous devez effectuer toutes les manipulations de jetons.

*Teams App Studio* vous permet de créer et de configurer votre manifeste d’application et peut créer votre robot d’infrastructure de robots pour vous. Il contient également une bibliothèque de contrôle REACT et un générateur de carte interactive.

## <a name="outgoing-webhooks"></a>Webhooks sortants

Les webhooks sortants vous permettent de créer un robot simple pour une interaction de base, comme le lancement d’un flux de travail ou d’autres commandes simples dont vous pouvez avoir besoin. Les webhooks sortants sont uniquement en ligne dans l’équipe dans laquelle vous les créez et sont destinés à des processus simples spécifiques au flux de travail de votre entreprise. Pour plus d’informations, consultez la rubrique [webhooks sortants](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md) .

## <a name="build-a-great-teams-bot"></a>Créer un robot teams de grande qualité

Les rubriques suivantes vous guideront tout au long du processus de création d’un robot puissant pour Teams.

* [Créer un bot](~/resources/bot-v3/bots-create.md): Tirez parti des outils, de la documentation et de la communauté intéressants fournis par l’équipe de la structure du robot.
* [Discutez avec votre robot](~/resources/bot-v3/bot-conversations/bots-conversations.md): ajoutez un flux de conversation de base et tirez parti de la fonctionnalité propre au canal. Si vous développez dans .NET ou node. js, utilisez nos extensions pour le kit de développement logiciel (SDK) du générateur de robots pour simplifier votre travail.
* [Utilisation des cartes dans votre robot](~/resources/bot-v3/bots-cards.md) Concevez des cartes pour communiquer et accepter la réponse de l’utilisateur.
* [Répondre aux événements bot](~/resources/bot-v3/bots-notifications.md).
* [Robots de notification uniquement](~/resources/bot-v3/bots-notification-only.md) Utilisation de robots pour envoyer des notifications pour votre application.
* [Obtenir un contexte](~/resources/bot-v3/bots-context.md) Obtenir des informations sur l’utilisateur.
* [Menus du robot](~/resources/bot-v3/bots-menus.md) Utilisation des menus dans les robots.
* [Robots et fichiers](~/resources/bot-v3/bots-files.md) Envoi et réception de fichiers à partir de robots.
* [Utilisation d’onglets avec des robots](~/resources/bot-v3/bots-with-tabs.md) Les onglets et les robots fonctionnent ensemble.
* [Testez votre robot](~/resources/bot-v3/bots-test.md): ajoutez votre robot pour les conversations personnelles ou d’équipe pour le voir en action.
