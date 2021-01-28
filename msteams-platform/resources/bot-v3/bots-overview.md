---
title: Ajouter des bots aux applications Microsoft Teams
description: Décrit comment commencer à développer des bots dans Microsoft Teams
ms.topic: conceptual
keywords: développement de bots teams
ms.date: 05/20/2018
ms.openlocfilehash: 226340500f59754d603f21b7868eecab38f942af
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014403"
---
# <a name="add-bots-to-microsoft-teams-apps"></a>Ajouter des bots aux applications Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Créez et connectez des bots intelligents pour interagir naturellement avec les utilisateurs de Microsoft Teams par le biais de la conversation. Ou fournissez un bot simple basé sur des commandes, qui sera utilisé comme interface de « ligne de commande » pour votre expérience d’application Teams plus large. Vous pouvez effectuer un bot de notification uniquement, qui peut transmettre des informations pertinentes à vos utilisateurs directement dans un canal ou un message direct. Vous pouvez même apporter votre bot existant basé sur Bot Framework et ajouter une prise en charge spécifique à Teams pour mettre en valeur votre expérience.

![Exemple de bot d’assistance à un utilisateur](~/assets/images/bot_example.png)

## <a name="what-you-need-to-know-bots"></a>Ce que vous devez savoir : Bots

Un bot apparaît comme n’importe quel autre membre de l’équipe avec qui vous interagissez dans une conversation, sauf qu’il possède une icône d’avatar hexagonal et qu’il est toujours en ligne.

Un bot se comporte différemment selon le type de conversation dans qui il est impliqué. Les bots dans Teams supportent plusieurs types de conversations (appelées étendues dans le manifeste [de l’application).](~/resources/schema/manifest-schema.md)

* `teams` Également appelées conversations de canal
* `personal` Conversations entre un bot et un utilisateur unique
* `groupChat` Conversation entre un bot et 2 utilisateurs ou plus

Pour [plus d’informations, voir](~/resources/bot-v3/bot-conversations/bots-conversations.md) Avoir une conversation avec un bot Microsoft Teams.

Avec les applications Microsoft Teams, vous pouvez faire du bot l’étoile de votre expérience, ou simplement un utilisateur d’aide. Les bots sont distribués dans le cadre de votre package d’application plus large, qui peut inclure d’autres [fonctionnalités telles](~/tabs/what-are-tabs.md) que des onglets ou [des extensions de messagerie.](~/messaging-extensions/what-are-messaging-extensions.md)

## <a name="bot-apis"></a>API de bot

Microsoft Teams prend en charge la plupart [de Microsoft Bot Framework.](https://dev.botframework.com/) (Si vous avez déjà un bot basé sur Bot Framework, vous pouvez facilement l’adapter pour qu’il fonctionne dans Microsoft Teams.) Nous vous recommandons d’utiliser C# ou Node.js pour tirer parti de nos [SDK.](/microsoftteams/platform/#pivot=sdk-tools) Ces packages étendent les classes et méthodes de base du kit de développement logiciel (SDK) Bot Builder :

* Utilisation de types de cartes spécialisés tels que la carte connecteur Office 365
* Consommation et définition de données de canal spécifiques à Teams sur les activités
* Traitement des demandes d’extension de messagerie

Les extensions du SDK installent les dépendances, y compris le SDK Bot Builder.

* **.NET** Pour utiliser les extensions Microsoft Teams pour le SDK Bot Builder pour .NET, installez le package NuGet [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) dans Visual Studio projet. Pour Node.js développement, la fonctionnalité BotBuilder pour Microsoft Teams a été intégrée au [SDK Bot Framework](https://github.com/microsoft/botframework-sdk) à partir de la v4.6.

*Voir aussi des* [exemples Bot Framework.](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)

> [!IMPORTANT]
> Vous pouvez développer des applications Teams dans n’importe quelle autre technologie de programmation web et appeler directement les API [REST Bot Framework,](/bot-framework/rest-api/bot-framework-rest-overview) mais vous devez effectuer vous-même la gestion de tous les jetons.

*Teams App Studio vous* aide à créer et configurer votre manifeste d’application, et peut créer votre bot Bot Framework pour vous. Il contient également une bibliothèque de contrôles React et un générateur de carte interactif.

## <a name="outgoing-webhooks"></a>Webhooks sortants

Les webhooks sortants vous permettent de créer un bot simple pour une interaction de base, par exemple en vous délant d’un flux de travail ou d’autres commandes simples dont vous pouvez avoir besoin. Les webhooks sortants ne sont créés que dans l’équipe dans laquelle vous les créez et sont conçus pour des processus simples spécifiques au flux de travail de votre entreprise. Pour [plus d’informations, voir les webhooks](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md) sortants.

## <a name="build-a-great-teams-bot"></a>Créer un bot Teams de qualité

Les rubriques suivantes vous guident tout au long du processus de création d’un bot idéal pour Teams.

* [Créez un bot](~/resources/bot-v3/bots-create.md): tirez parti des excellents outils, de la documentation et de la communauté fournis par l’équipe Bot Framework.
* [Parlez à votre bot](~/resources/bot-v3/bot-conversations/bots-conversations.md): ajoutez un flux de conversation de base et tirez parti des fonctionnalités propres au canal. Si vous développez dans .NET ou Node.js, utilisez nos extensions pour le SDK Bot Builder pour simplifier votre travail.
* [Utilisation de cartes dans votre bot](~/resources/bot-v3/bots-cards.md) Concevez des cartes pour communiquer et accepter la réponse de l’utilisateur.
* [Répondre aux événements du bot.](~/resources/bot-v3/bots-notifications.md)
* [Bots de notification uniquement](~/resources/bot-v3/bots-notification-only.md) Utilisation de bots pour envoyer des notifications pour votre application.
* [Obtenir le contexte](~/resources/bot-v3/bots-context.md) Obtenir des informations sur l’utilisateur.
* [Menus bot](~/resources/bot-v3/bots-menus.md) Utilisation de menus dans les bots.
* [Bots et fichiers](~/resources/bot-v3/bots-files.md) Envoi et réception de fichiers à partir de bots.
* [Utilisation d’onglets avec des bots](~/resources/bot-v3/bots-with-tabs.md) Faire fonctionner les onglets et les bots ensemble.
* [Testez votre bot](~/resources/bot-v3/bots-test.md): ajoutez votre bot pour les conversations personnelles ou d’équipe pour le voir en action.
