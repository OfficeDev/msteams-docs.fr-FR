---
title: Ajouter des bots à Microsoft Teams applications
description: Décrit comment commencer à développer des bots dans Microsoft Teams
ms.topic: conceptual
keywords: développement de bots teams
localization_priority: Normal
ms.date: 05/20/2018
ms.openlocfilehash: dd32439c74daf55c89d0e34614a073a36a5ffa1e
ms.sourcegitcommit: 2c4c77dc8344f2fab8ed7a3f7155f15f0dd6a5ce
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/13/2021
ms.locfileid: "58345682"
---
# <a name="add-bots-to-microsoft-teams-apps"></a>Ajouter des bots à Microsoft Teams applications

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Créez et connectez des bots intelligents pour interagir avec Microsoft Teams utilisateurs par le biais d’une conversation. Ou fournissez un bot simple basé sur des commandes, qui sera utilisé comme interface de « ligne de commande » pour votre expérience d’application Teams étendue. Vous pouvez effectuer un bot de notification uniquement, qui peut transmettre des informations pertinentes à vos utilisateurs directement dans un canal ou un message direct. Vous pouvez même apporter votre bot bot existant basé sur Bot Framework et ajouter Teams prise en charge spécifique pour mettre en valeur votre expérience.

> [!IMPORTANT]
> Actuellement, les bots sont disponibles dans Cloud de la communauté du secteur public (Cloud de la communauté du secteur public), mais pas dans les GCC-High et le département de la Défense (DOD).

![Exemple de bot d’assistance à un utilisateur](~/assets/images/bot_example.png)

## <a name="what-you-need-to-know-bots"></a>Ce que vous devez savoir : Bots

Un bot apparaît comme n’importe quel autre membre de l’équipe avec qui vous interagissez dans une conversation, sauf qu’il a une icône d’avatar hexagonal et qu’il est toujours en ligne.

Un bot se comporte différemment selon le type de conversation dans qui il est impliqué. Les bots dans Teams plusieurs types de conversations appelées étendues dans le manifeste [de l’application.](~/resources/schema/manifest-schema.md)

* `teams` Également appelées conversations de canal.
* `personal` Conversations entre un bot et un utilisateur unique.
* `groupChat` Conversation entre un bot et 2 utilisateurs ou plus.

Pour plus d’informations, [voir Avoir une conversation avec Microsoft Teams bot.](~/resources/bot-v3/bot-conversations/bots-conversations.md)

Avec Microsoft Teams applications, vous pouvez faire du bot l’étoile de votre expérience, ou simplement un simple utilisateur d’aide. Les bots sont distribués dans le cadre de votre package d’application plus large, qui peut inclure d’autres [fonctionnalités telles](~/tabs/what-are-tabs.md) que des onglets ou [des extensions de messagerie.](~/messaging-extensions/what-are-messaging-extensions.md)

## <a name="bot-apis"></a>API de bot

Microsoft Teams prend en charge la plupart des [Microsoft Bot Framework](https://dev.botframework.com/). (Si vous avez déjà un bot basé sur Bot Framework, vous pouvez facilement l’adapter pour qu’il fonctionne Microsoft Teams.) Nous vous recommandons d’utiliser C# ou Node.js pour tirer parti de nos [SDK.](/microsoftteams/platform/#pivot=sdk-tools) Ces packages étendent les classes et méthodes de base du kit de développement logiciel (SDK) Bot Builder :

* Utilisation de types de carte spécialisés tels que la Office 365 Connector.
* Consommation et définition de Teams données de canal spécifiques sur les activités.
* Traitement des demandes d’extension de messagerie.

Les extensions du SDK installent des dépendances, y compris le SDK Bot Builder.

* **.NET** Pour utiliser les extensions Microsoft Teams pour le SDK Bot Builder pour .NET, installez le package [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet dans votre projet Visual Studio. Pour Node.js développement, la fonctionnalité BotBuilder pour Microsoft Teams a été incorporée au [SDK Bot Framework](https://github.com/microsoft/botframework-sdk) à partir de la v4.6.

> [!IMPORTANT]
> Vous pouvez développer Teams applications dans n’importe quelle autre technologie de programmation web et appeler directement les API [REST Bot Framework,](/bot-framework/rest-api/bot-framework-rest-overview) mais vous devez effectuer vous-même la gestion de tous les jetons.

*Teams App Studio* vous aide à créer et configurer votre manifeste d’application, et peut créer votre bot Bot Framework pour vous. Il contient également une bibliothèque React de contrôles et un générateur de cartes interactif.

## <a name="outgoing-webhooks"></a>Webhooks sortants

Les webhooks sortants vous permettent de créer un bot simple pour une interaction de base, par exemple en vous délant d’un flux de travail ou d’autres commandes simples dont vous pouvez avoir besoin. Les webhooks sortants ne sont créés que dans l’équipe dans laquelle vous les créez et sont conçus pour des processus simples spécifiques au flux de travail de votre entreprise. Pour plus d’informations, [voir les webhooks sortants.](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)

## <a name="build-a-great-teams-bot"></a>Créer un bot Teams de qualité

Les rubriques suivantes vous guident tout au long du processus de création d’un bot idéal pour Teams :

* [Créez un bot](~/resources/bot-v3/bots-create.md): tirez parti des excellents outils, de la documentation et de la communauté fournis par l’équipe Bot Framework.
* [Parlez à votre bot](~/resources/bot-v3/bot-conversations/bots-conversations.md): ajoutez un flux de conversation de base et tirez parti des fonctionnalités propres au canal. Si vous développez dans .NET ou Node.js, utilisez nos extensions pour le SDK Bot Builder pour simplifier votre travail.
* [Utilisation de cartes dans votre bot](~/resources/bot-v3/bots-cards.md): concevoir des cartes pour communiquer et accepter la réponse de l’utilisateur.
* [Répondre aux événements de bot](~/resources/bot-v3/bots-notifications.md)
* [Bots de notification uniquement](~/resources/bot-v3/bots-notification-only.md): utilisation de bots pour envoyer des notifications pour votre application.
* [Obtenir le contexte](~/resources/bot-v3/bots-context.md): obtenir des informations sur l’utilisateur.
* [Menus du bot](~/resources/bot-v3/bots-menus.md): utilisation de menus dans les bots.
* [Bots et fichiers :](~/resources/bot-v3/bots-files.md)envoi et réception de fichiers à partir de bots.
* [Utilisation d’onglets avec des bots :](~/resources/bot-v3/bots-with-tabs.md)faire fonctionner les onglets et les bots ensemble.
* [Testez votre bot](~/resources/bot-v3/bots-test.md): ajoutez votre bot pour les conversations personnelles ou d’équipe pour le voir en action.

## <a name="see-also"></a>Voir aussi

[Exemples Bot Framework.](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)