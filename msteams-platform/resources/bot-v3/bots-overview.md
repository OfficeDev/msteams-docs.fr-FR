---
title: Ajouter des bots aux applications Microsoft Teams
description: Dans ce module, découvrez comment commencer à développer des bots dans Microsoft Teams et quelles sont les conditions requises pour ajouter un bot dans Teams
ms.topic: conceptual
ms.localizationpriority: medium
ms.date: 05/20/2018
ms.openlocfilehash: a1563d72ada21810393d7a0118b5a2b94463a27b
ms.sourcegitcommit: 69a45722c5c09477bbff3ba1520e6c81d2d2d997
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/11/2022
ms.locfileid: "67312211"
---
# <a name="add-bots-to-microsoft-teams-apps"></a>Ajouter des bots aux applications Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Créez et connectez des bots intelligents pour interagir naturellement avec les utilisateurs de Microsoft Teams par le biais d’une conversation. Ou fournissez un bot simple basé sur des commandes, à utiliser comme votre « ligne de commande » pour votre expérience d’application Teams plus large. Vous pouvez créer un bot de notification uniquement, qui peut envoyer (push) des informations pertinentes à vos utilisateurs directement dans un canal ou un message direct. Vous pouvez même apporter votre bot basé sur Bot Framework existant et ajouter une prise en charge spécifique à Teams pour améliorer votre expérience.

> [!IMPORTANT]
> Actuellement, les bots sont disponibles dans government community cloud (GCC) et GCC-High, mais pas dans le ministère de la Défense (DOD).

:::image type="content" source="../../assets/images/bot_example.png" alt-text="Exemple de bot aidant un utilisateur":::

## <a name="what-you-need-to-know-bots"></a>Ce que vous devez savoir : bots

Un bot apparaît comme n’importe quel autre membre de l’équipe avec lequel vous interagissez dans une conversation, à ceci près qu’il a une icône d’avatar hexagonal et qu’il est toujours en ligne.

Un bot se comporte différemment en fonction du type de conversation dans lequel il est impliqué. Les bots dans Teams prennent en charge plusieurs types de conversations appelées étendues dans le [manifeste d’application](~/resources/schema/manifest-schema.md).

* `teams` Également appelé conversations de canal.
* `personal` conversations entre un bot et un seul utilisateur.
* `groupChat` Conversation entre un bot et au moins deux utilisateurs.

Pour plus d’informations, consultez [Avoir une conversation avec un bot Microsoft Teams](~/resources/bot-v3/bot-conversations/bots-conversations.md).

Avec les applications Teams, vous pouvez faire du bot l’étoile de votre expérience, ou simplement un assistance. Les bots sont distribués dans le cadre de votre package d’application plus large, qui peut inclure d’autres fonctionnalités telles que les [onglets](~/tabs/what-are-tabs.md) ou les [extensions de message](~/messaging-extensions/what-are-messaging-extensions.md).

## <a name="bot-apis"></a>API de bot

Teams prend en charge la plupart des [Microsoft Bot Framework](https://dev.botframework.com/). (Si vous disposez déjà d’un bot basé sur Bot Framework, vous pouvez facilement l’adapter pour fonctionner dans Teams.) Nous vous recommandons d’utiliser C# ou Node.js pour tirer parti de nos [kits SDK](/microsoftteams/platform/#pivot=sdk-tools). Ces packages étendent les classes et méthodes de base du kit de développement logiciel (SDK) Bot Builder :

* Utilisation de types de cartes spécialisés tels que la carte connecteur Office 365.
* Utilisation et définition de données de canal spécifiques à Teams sur les activités.
* Traitement des demandes d’extension de message.

Les extensions du Kit de développement logiciel (SDK) installent des dépendances, notamment le SDK Bot Builder.

* **.NET** Pour utiliser les extensions Microsoft Teams pour le Bot Builder SDK pour .NET, installez le paquet [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet dans votre projet Visual Studio. Pour le développement Node.js, la fonctionnalité BotBuilder pour Microsoft Teams a été incorporée dans le kit de développement logiciel (SDK) [Bot Framework](https://github.com/microsoft/botframework-sdk) à compter de la version 4.6.

> [!IMPORTANT]
> Vous pouvez développer des applications Teams dans n’importe quelle autre technologie de programmation web et appeler directement les API REST [Bot Framework](/bot-framework/rest-api/bot-framework-rest-overview) , mais vous devez gérer vous-même tous les jetons.

*Le portail des développeurs pour Teams* vous aide à créer et à configurer votre manifeste d’application, et peut créer votre bot Bot Framework pour vous. Il contient également une bibliothèque de contrôles React et un générateur de cartes interactif.

## <a name="outgoing-webhooks"></a>Webhooks sortants

Les webhooks sortants vous permettent de créer un bot simple pour une interaction de base, comme le lancement d’un flux de travail ou d’autres commandes simples dont vous pouvez avoir besoin. Les webhooks sortants résident uniquement dans l’équipe dans laquelle vous les créez et sont destinés à des processus simples spécifiques au flux de travail de votre entreprise. Pour plus d’informations, consultez [webhooks sortants](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md).

## <a name="build-a-great-teams-bot"></a>Créer un bot Teams idéal

Les articles suivants vous guideront tout au long du processus de création d’un bot idéal pour Teams :

* [Créer un bot](~/resources/bot-v3/bots-create.md): tirez parti des outils, de la documentation et de la communauté fournis par l’équipe Bot Framework.
* [parlez à votre bot](~/resources/bot-v3/bot-conversations/bots-conversations.md): ajoutez un flux de conversation de base et tirez parti des fonctionnalités spécifiques au canal. Si vous développez dans .NET ou Node.js, utilisez nos extensions pour le SDK Bot Builder afin de simplifier votre travail.
* [Utilisation de cartes dans votre bot](~/resources/bot-v3/bots-cards.md): concevez des cartes pour communiquer et accepter la réponse de l’utilisateur.
* [répondre aux événements de bot](~/resources/bot-v3/bots-notifications.md)
* [bots de notification uniquement](~/resources/bot-v3/bots-notification-only.md): utilisation de bots pour envoyer des notifications pour votre application.
* [Obtenir le contexte](~/resources/bot-v3/bots-context.md): obtenir des informations sur l’utilisateur.
* [menus bot](~/resources/bot-v3/bots-menus.md): utilisation de menus dans les bots.
* [bots et fichiers](~/resources/bot-v3/bots-files.md): envoi et réception de fichiers à partir de bots.
* [l’utilisation d’onglets avec des bots](~/resources/bot-v3/bots-with-tabs.md): la collaboration des onglets et des bots.
* [tester votre bot](~/resources/bot-v3/bots-test.md): ajoutez votre bot pour les conversations personnelles ou d’équipe pour le voir en action.

## <a name="see-also"></a>Voir aussi

[Exemples Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)
