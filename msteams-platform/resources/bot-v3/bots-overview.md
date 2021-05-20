---
title: Ajouter des bots aux Microsoft Teams applications
description: Décrit comment commencer à développer des bots dans Microsoft Teams
ms.topic: conceptual
keywords: équipes de développement bots
localization_priority: Normal
ms.date: 05/20/2018
ms.openlocfilehash: 674576efccb2916b8a82ae27310d8fe49909a782
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566753"
---
# <a name="add-bots-to-microsoft-teams-apps"></a>Ajouter des bots aux Microsoft Teams applications

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Créez et connectez des bots intelligents pour interagir avec Microsoft Teams utilisateurs naturellement par le chat. Ou fournissez un bot simple basé sur les commandes, qui sera utilisé comme interface de « ligne de commande » pour votre expérience plus large Teams’application. Vous pouvez faire un bot de notification uniquement, qui peut pousser les informations pertinentes pour vos utilisateurs directement à eux dans un canal ou un message direct. Vous pouvez même apporter votre bot bot existant basé sur bot framework et ajouter un support Teams spécifique pour faire briller votre expérience.

![Exemple d’un bot aidant un utilisateur](~/assets/images/bot_example.png)

## <a name="what-you-need-to-know-bots"></a>Ce que vous devez savoir: Bots

Un bot apparaît comme n’importe quel autre membre de l’équipe avec qui vous interagissez dans une conversation, sauf qu’il a une icône d’avatar hexagonal et est toujours en ligne.

Un bot se comporte différemment selon le type de conversation dans qui il est impliqué. Bots dans Teams plusieurs types de conversations appelées étendues dans le manifeste [de l’application](~/resources/schema/manifest-schema.md).

* `teams` Aussi appelé conversations canal.
* `personal` Conversations entre un bot et un seul utilisateur.
* `groupChat` Une conversation entre un bot et 2 utilisateurs ou plus.

Pour plus d’informations, [voir Avoir une conversation avec un bot Microsoft Teams.](~/resources/bot-v3/bot-conversations/bots-conversations.md)

Avec Microsoft Teams applications, vous pouvez faire du bot la star de votre expérience, ou tout simplement un aide. Les bots sont distribués dans le cadre de votre paquet d’applications plus large qui peut inclure d’autres fonctionnalités telles que [des onglets ou](~/tabs/what-are-tabs.md) des [extensions de messagerie.](~/messaging-extensions/what-are-messaging-extensions.md)

## <a name="bot-apis"></a>API Bot

Microsoft Teams soutient la plupart des [Microsoft Bot Framework](https://dev.botframework.com/). (Si vous avez déjà un bot basé sur le cadre Bot, vous pouvez facilement l’adapter pour travailler en Microsoft Teams.) Nous vous recommandons d’utiliser C# ou Node.js pour profiter de [nos SDK.](/microsoftteams/platform/#pivot=sdk-tools) Ces packages étendent les classes et méthodes de base du kit de développement logiciel (SDK) Bot Builder :

* Utilisation de types de cartes spécialisés comme la Office 365 carte Connector.
* Consommer et définir Teams de canaux spécifiques aux activités.
* Traitement des demandes d’extension de messagerie.

Les extensions SDK installent des dépendances, y compris le Bot Builder SDK.

* **.NET (en)** Pour utiliser les extensions Microsoft Teams pour le Bot Builder SDK pour .NET, installez le package [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet dans votre projet Visual Studio. Pour Node.js développement, le BotBuilder pour Microsoft Teams fonctionnalité a été incorporé dans [le Bot Framework SDK](https://github.com/microsoft/botframework-sdk) à partir de v4.6.

> [!IMPORTANT]
> Vous pouvez développer Teams applications dans n’importe quelle autre technologie de programmation Web et appeler [directement les API Bot Framework REST,](/bot-framework/rest-api/bot-framework-rest-overview) mais vous devez effectuer toutes les manipulations de jetons vous-même.

*Teams App Studio vous* aide à créer et configurer votre manifeste d’application, et peut créer votre bot Bot Framework pour vous. Il contient également une bibliothèque React contrôle des cartes et un constructeur de cartes interactif.

## <a name="outgoing-webhooks"></a>Webhooks sortants

Les webhooks sortants vous permettent de créer un bot simple pour l’interaction de base, comme le coup d’envoi d’un workflow ou d’autres commandes simples dont vous pourriez avoir besoin. Les webhooks sortants ne vivent que dans l’équipe dans laquelle vous les créez et sont destinés à des processus simples spécifiques au flux de travail de votre entreprise. Pour plus d’informations, [consultez les webhooks sortants](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md).

## <a name="build-a-great-teams-bot"></a>Construire un grand bot Teams

Les sujets suivants vous guideront à travers le processus de création d’un grand bot pour Teams:

* [Créer un bot](~/resources/bot-v3/bots-create.md): Profitez des excellents outils, de la documentation et de la communauté fournis par l’équipe bot framework.
* [Parlez à votre bot : Ajoutez](~/resources/bot-v3/bot-conversations/bots-conversations.md)le flux de conversation de base et tirez parti des fonctionnalités spécifiques au canal. Si vous développez dans .NET ou Node.js, utilisez nos extensions pour le Bot Builder SDK pour simplifier votre travail.
* [Utilisation de cartes dans votre bot :](~/resources/bot-v3/bots-cards.md)Concevoir des cartes pour communiquer et accepter la réponse de l’utilisateur.
* [Répondre aux événements bot](~/resources/bot-v3/bots-notifications.md)
* [Bots de notification uniquement :](~/resources/bot-v3/bots-notification-only.md)Utiliser des bots pour envoyer des notifications pour votre application.
* [Obtenez le contexte](~/resources/bot-v3/bots-context.md): Obtenez des informations sur l’utilisateur.
* [Menus bot :](~/resources/bot-v3/bots-menus.md)Utilisation de menus en bots.
* [Bots et fichiers :](~/resources/bot-v3/bots-files.md)Envoi et réception de fichiers de bots.
* [Utilisation d’onglets avec des bots](~/resources/bot-v3/bots-with-tabs.md): Faire travailler ensemble les onglets et les bots.
* [Testez votre bot](~/resources/bot-v3/bots-test.md): Ajoutez votre bot pour des conversations personnelles ou d’équipe pour le voir en action.

## <a name="see-also"></a>Voir aussi

[Échantillons bot framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).