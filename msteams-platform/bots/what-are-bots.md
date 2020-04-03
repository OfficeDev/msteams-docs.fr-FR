---
title: Qu’est-ce que les robots de conversation ?
author: clearab
description: Vue d’ensemble des robots de conversation dans Microsoft Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 132b71a4da7462c426468c7fc2f79b26b6fbb03b
ms.sourcegitcommit: 058b7bbd817af5f513e0e018f2ef562dc3086a84
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/03/2020
ms.locfileid: "43120289"
---
# <a name="what-are-conversational-bots"></a>Qu’est-ce que les robots de conversation ?

Les bots de conversation permettent aux utilisateurs d’interagir avec votre service web via du texte, des cartes interactives et des modules de tâches. Ils sont incroyablement flexibles : les robots de conversation peuvent être délimités pour gérer quelques commandes simples ou des assistants virtuels complexes, équipés d’intelligence artificielle et de traitement naturel en langue naturelle. Il peut s’agir d’un aspect d’une application plus grande ou totalement autonome.

L’image GIF ci-dessous montre un utilisateur qui contourne un bot dans une conversation un-à-un en utilisant des cartes de texte et des cartes interactives. Trouver le bon mélange de cartes, de texte et de modules de tâches est essentiel pour créer un bot utile. N’oubliez pas que les robots sont bien plus qu’un simple texte !

![Forum aux questions et GIF](~/assets/images/FAQPlusEndUser.gif)

## <a name="how-bots-work"></a>Fonctionnement des robots

Votre bot teams se compose de trois éléments :

* Service Web accessible au public que vous hébergez.
* Enregistrement de votre bot avec l’infrastructure bot.
* Votre package d’application de teams avec votre manifeste d’application. Il s’agit de ce que vos utilisateurs installeront et connectent le client teams à votre service Web, routé via le service bot.

Les robots pour Microsoft teams sont basés sur [Microsoft bot Framework](https://dev.botframework.com/). Si vous disposez déjà d’un bot basé sur l’infrastructure de robot, vous pouvez facilement l’adapter pour qu’elle fonctionne dans Microsoft Teams. Nous vous recommandons d’utiliser C# ou node. js pour tirer parti de nos [Kits de développement](/microsoftteams/platform/#pivot=sdk-tools)logiciel (SDK). Ces packages étendent les classes et méthodes de base du kit de développement logiciel (SDK) de base, comme suit :

* Utilisez des types de carte spéciaux comme la carte connecteur Office 365.
* Utiliser et définir des données de canal spécifiques aux équipes sur les activités.
* Traiter les demandes d’extension de messagerie.

> [!IMPORTANT]
> Vous pouvez développer des applications teams dans n’importe quelle technologie de programmation Web et appeler directement les [API REST de l’infrastructure bot](/bot-framework/rest-api/bot-framework-rest-overview) , mais vous devez effectuer toutes les manipulations de jetons.

> [!TIP]
> Teams App Studio * vous permet de créer et de configurer votre manifeste d’application et peut enregistrer votre service Web en tant que bot sur l’infrastructure bot. Il contient également une bibliothèque de contrôle REACT et un générateur de carte interactive. *Consultez la rubrique* [prise en main de Team App Studio](~/concepts/build-and-test/app-studio-overview.md).

## <a name="webhooks-and-connectors"></a>Webhooks et connecteurs

Les connecteurs et les webhooks vous permettent de créer un robot simple pour une interaction de base, comme le lancement d’un flux de travail ou d’autres commandes simples. Ils vivent uniquement dans l’équipe dans laquelle vous les créez et sont destinés à des processus simples spécifiques au flux de travail de votre entreprise. *Voir* [qu’est-ce qu’un webhooks et un connecteur ?](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) pour plus d’informations.

## <a name="where-bots-work-best"></a>Fonctionnement optimal des robots

Les robots de Microsoft teams peuvent faire partie d’une conversation un-à-un, d’une conversation de groupe ou d’un canal dans une équipe. Chaque étendue fournit des opportunités et des défis uniques pour votre robot de conversation.

### <a name="in-a-channel"></a>Dans un canal

Les canaux contiennent des conversations thématiques entre plusieurs personnes, potentiellement de nombreuses personnes (actuellement, jusqu’à 2000). Cela peut entraîner l’énorme potentiel de votre robot, mais les différentes interactions doivent être concises. Les interactions de multi-tour classiques ne fonctionneront probablement pas correctement. À la place, regardez utiliser des cartes interactives ou des modules de tâches, ou déplacez éventuellement la conversation vers une conversation un-à-un si vous avez besoin de collecter beaucoup d’informations. Votre bot n’aura également accès qu’aux messages qui s’y `@mentioned` trouvent directement, vous ne pouvez pas récupérer des messages supplémentaires à l’aide de Microsoft Graph et des autorisations de niveau organisation élevées.

Voici quelques scénarios dans lesquels les robots Excel dans un canal sont les suivants :

* Les **notifications**, en particulier si vous fournissez une carte interactive pour que les utilisateurs puissent prendre des informations supplémentaires.
* **Scénarios de commentaires** , tels que les sondages et les enquêtes.
* Interactions pouvant être résolues en un **seul cycle de demande/réponse**, où les résultats sont utiles pour plusieurs membres de la conversation.
* **Robots sociaux/loisirs** : obtenez une image de chat attrayante, sélectionnez un gagnant, etc.

### <a name="in-a-group-chat"></a>Dans une conversation de groupe

Les conversations de groupe sont des conversations non thématiques entre trois personnes ou plus. Ils ont tendance à avoir moins de membres qu’un canal et sont plus transitoires. À l’instar d’un canal, votre robot n’a accès qu’aux messages `@mentioned` pour lesquels il est directement.

Les scénarios qui fonctionnent correctement dans un canal fonctionnent généralement également dans une conversation de groupe.

### <a name="in-a-one-to-one-chat"></a>Dans une conversation un-à-un

Il s’agit de la manière la plus classique pour un bot de conversation d’interagir avec un utilisateur. Ils peuvent activer des charges de travail incroyablement diverses. Q&les robots, les robots qui lancent des flux de travail dans d’autres systèmes, les robots qui indiquent des blagues et les robots qui prennent des notes, sont simplement quelques exemples. N’oubliez pas de déterminer si une interface basée sur une conversation est la meilleure façon de présenter vos fonctionnalités.

## <a name="bot-fails"></a>Échec du bot

### <a name="having-multi-turn-experiences-in-chat"></a>Utilisation de plusieurs expériences dans la conversation

Une boîte de dialogue complète entre votre robot et l’utilisateur est une façon lente et excessivement complexe de faire en sorte qu’une tâche soit terminée et nécessite également que le développeur conserve son état. Pour quitter cet État, un utilisateur doit avoir dépassé le délai d’attente ou taper «*Annuler*». Au-dessus de tout, le processus est inutilement fastidieux :

UTILISATEUR : planifier une réunion avec Megan.

BOT : J’ai trouvé 200 résultats, veuillez inclure un prénom et un nom de famille.

UTILISATEUR : planifier une réunion avec Megan Bowen.

BOT : OK, quelle heure souhaitez-vous rencontrer avec Megan Bowen ?

UTILISATEUR : 1:00 pm.

ROBOT : le jour où ?

### <a name="supporting-too-many-commands"></a>Prise en charge d’un trop grand nombre de commandes

Un bot qui prend en charge des commandes excessives, en particulier un large éventail de commandes, ne réussit pas ou ne s’affiche pas positivement par les utilisateurs. Étant donné qu’il y a seulement 6 commandes visibles dans le menu robot actuel, il est peu probable qu’il n’y ait aucune fréquence. Les robots qui s’approfondient à une zone spécifique plutôt que d’essayer d’être un Assistant plus large fonctionneront et seront mieux adaptés.

### <a name="maintaining-a-large-retrieval-knowledge-base-with-unranked-responses"></a>Maintenance d’une base de connaissances de récupération volumineuse avec des réponses sans classement

Les robots sont les plus adaptés aux interactions courtes et rapides, sans passer par les longues listes cherchant une réponse.

## <a name="get-started"></a>Prise en main

* [Robots de conversation teams en C#/dotnet](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot)
* [Robots de conversation teams en JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot)

## <a name="learn-more"></a>En savoir plus

> [!div class="nextstepaction"]
> [Notions de base sur les robots dans teams](~/bots/bot-basics.md)

> [!div class="nextstepaction"]
> [Créer un bot pour teams](~/bots/how-to/create-a-bot-for-teams.md)
