---
title: Ajouter des bots à des applications Microsoft Teams
description: Décrit comment commencer à développer des bots dans Microsoft Teams
ms.topic: conceptual
keywords: développement de bots teams
ms.localizationpriority: medium
ms.date: 05/20/2018
ms.openlocfilehash: 164c8e518e38d506bbaf80f59edebfb18c07acec
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2022
ms.locfileid: "65103424"
---
# <a name="add-bots-to-microsoft-teams-apps"></a>Ajouter des bots à des applications Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Créez et connectez des bots intelligents pour interagir avec Microsoft Teams utilisateurs naturellement par le biais d’une conversation. Vous pouvez également fournir un bot simple basé sur des commandes, qui sera utilisé comme interface de « ligne de commande » pour votre expérience d’application Teams plus large. Vous pouvez créer un bot de notification uniquement, qui peut envoyer directement des informations pertinentes à vos utilisateurs dans un canal ou un message direct. Vous pouvez même apporter votre bot Bot Framework existant et ajouter Teams prise en charge spécifique pour rendre votre expérience optimale.

> [!IMPORTANT]
> Actuellement, les bots sont disponibles dans Cloud de la communauté du secteur public (Cloud de la communauté du secteur public), mais pas dans GCC-High et le ministère de la Défense (DOD).

![Exemple de bot aidant un utilisateur](~/assets/images/bot_example.png)

## <a name="what-you-need-to-know-bots"></a>Ce que vous devez savoir : Bots

Un bot apparaît comme n’importe quel autre membre de l’équipe avec lequel vous interagissez dans une conversation, sauf qu’il a une icône d’avatar hexagonale et qu’il est toujours en ligne.

Un bot se comporte différemment selon le type de conversation dans lequel il est impliqué. Les bots dans Teams prennent en charge plusieurs types de conversations appelés étendues dans le [manifeste de l’application](~/resources/schema/manifest-schema.md).

* `teams` Également appelés conversations de canal.
* `personal` Conversations entre un bot et un seul utilisateur.
* `groupChat` Conversation entre un bot et 2 utilisateurs ou plus.

Pour plus d’informations, consultez [Avoir une conversation avec un bot Microsoft Teams](~/resources/bot-v3/bot-conversations/bots-conversations.md).

Avec Microsoft Teams applications, vous pouvez faire du bot l’étoile de votre expérience, ou simplement un assistance. Les bots sont distribués dans le cadre de votre package d’application plus large, qui peut inclure d’autres [fonctionnalités telles que des onglets](~/tabs/what-are-tabs.md) ou [des extensions de message](~/messaging-extensions/what-are-messaging-extensions.md).

## <a name="bot-apis"></a>API bot

Microsoft Teams prend en charge la plupart des [Microsoft Bot Framework](https://dev.botframework.com/). (Si vous disposez déjà d’un bot basé sur Bot Framework, vous pouvez facilement l’adapter pour fonctionner dans Microsoft Teams.) Nous vous recommandons d’utiliser C# ou Node.js pour tirer parti de nos [kits SDK](/microsoftteams/platform/#pivot=sdk-tools). Ces packages étendent les classes et méthodes de base du kit de développement logiciel (SDK) Bot Builder :

* Utilisation de types de cartes spécialisés comme la carte de connecteur Office 365.
* Consommation et définition de données de canal spécifiques à Teams sur les activités.
* Traitement des demandes d’extension de message.

Les extensions du Kit de développement logiciel (SDK) installent les dépendances, y compris le Kit de développement logiciel (SDK) Bot Builder.

* **.NET** Pour utiliser les extensions Microsoft Teams pour le Kit de développement logiciel (SDK) Bot Builder pour .NET, [installez le package de NuGet Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) dans votre projet Visual Studio. Pour Node.js développement, la fonctionnalité BotBuilder pour Microsoft Teams a été incorporée dans le Kit de développement logiciel [(SDK) Bot Framework](https://github.com/microsoft/botframework-sdk) à compter de la version 4.6.

> [!IMPORTANT]
> Vous pouvez développer Teams applications dans n’importe quelle autre technologie de programmation web et appeler directement les [API REST Bot Framework](/bot-framework/rest-api/bot-framework-rest-overview), mais vous devez effectuer vous-même toute la gestion des jetons.

*Teams App Studio* vous aide à créer et à configurer votre manifeste d’application, et peut créer votre bot Bot Framework pour vous. Il contient également une bibliothèque de contrôles React et un générateur de cartes interactif.

## <a name="outgoing-webhooks"></a>Webhooks sortants

Les webhooks sortants vous permettent de créer un bot simple pour une interaction de base, comme le lancement d’un flux de travail ou d’autres commandes simples dont vous aurez peut-être besoin. Les webhooks sortants vivent uniquement dans l’équipe dans laquelle vous les créez et sont destinés à des processus simples spécifiques au flux de travail de votre entreprise. Pour plus d’informations, consultez [les webhooks sortants](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md).

## <a name="build-a-great-teams-bot"></a>Créer un bot Teams

Les rubriques suivantes vous guideront tout au long du processus de création d’un bot idéal pour Teams :

* [Créer un bot](~/resources/bot-v3/bots-create.md) : tirez parti des outils, de la documentation et de la communauté fournis par l’équipe Bot Framework.
* [Parlez à votre bot](~/resources/bot-v3/bot-conversations/bots-conversations.md) : ajoutez un flux de conversation de base et tirez parti des fonctionnalités spécifiques au canal. Si vous développez dans .NET ou Node.js, utilisez nos extensions pour le Kit de développement logiciel (SDK) Bot Builder pour simplifier votre travail.
* [Utilisation de cartes dans votre bot](~/resources/bot-v3/bots-cards.md) : concevez des cartes pour communiquer et accepter la réponse de l’utilisateur.
* [Répondre aux événements de bot](~/resources/bot-v3/bots-notifications.md)
* [Bots de notification uniquement](~/resources/bot-v3/bots-notification-only.md) : utilisation de bots pour envoyer des notifications pour votre application.
* [Obtenir le contexte](~/resources/bot-v3/bots-context.md) : obtenir des informations sur l’utilisateur.
* [Menus bot](~/resources/bot-v3/bots-menus.md) : utilisation de menus dans des bots.
* [Bots et fichiers](~/resources/bot-v3/bots-files.md) : envoi et réception de fichiers à partir de bots.
* [Utilisation d’onglets avec des bots](~/resources/bot-v3/bots-with-tabs.md) : création d’onglets et de bots fonctionnant ensemble.
* [Testez votre bot](~/resources/bot-v3/bots-test.md) : ajoutez votre bot pour les conversations personnelles ou d’équipe pour le voir en action.

## <a name="see-also"></a>Voir aussi

[Exemples Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).
