---
title: Qu’est-ce que les robots ?
author: clearab
description: Vue d’ensemble des robots dans Microsoft Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 1e07d56769cbb303f9af98f84c8ae6064325c1a7
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/12/2020
ms.locfileid: "46651941"
---
# <a name="what-are-bots"></a>Qu’est-ce que les robots ?

Les robots permettent aux utilisateurs d’interagir avec votre service Web par le biais de textes, de cartes interactives et de modules de tâches. Ils sont incroyablement flexibles : vous pouvez étendre les robots de façon à gérer quelques commandes simples ou des assistants virtuels équipés d’une intelligence artificielle et d’un traitement en langage naturel. Il peut s’agir d’un aspect d’une application plus grande ou totalement autonome.

Trouver le bon mélange de cartes, de texte et de modules de tâches est essentiel pour créer un bot utile. N’oubliez pas que les robots sont bien plus qu’un simple texte !

![Forum aux questions et GIF](~/assets/images/FAQPlusEndUser.gif)

## <a name="user-scenarios"></a>Scénarios utilisateur

Les robots de Microsoft teams peuvent faire partie d’un canal, d’une conversation de groupe ou d’une conversation en un seul. Chaque étendue fournit des opportunités et des défis uniques pour votre robot de conversation.

### <a name="in-a-channel"></a>Dans un canal

Les canaux contiennent des conversations thématiques entre plusieurs personnes, potentiellement de nombreuses personnes (actuellement, jusqu’à 2000). Cela donne potentiellement une très grande portée à votre bot, mais les interactions individuelles doivent être concises. Les interactions classiques à plusieurs tours ne fonctionneront probablement pas très bien. Cherchez plutôt à utiliser des cartes interactives ou des modules de tâche, ou à transformer la conversation en conversation à deux si vous avez besoin de recueillir de nombreuses informations. Votre robot n’aura également accès qu’aux messages qui s’y trouvent `@mentioned` directement, même si vous pouvez récupérer des messages supplémentaires à partir de la conversation à l’aide de Microsoft Graph et des autorisations de niveau organisation élevées.

Voici quelques scénarios dans lesquels les bots fonctionnent très bien dans un canal :

* **notifications**, notamment si vous proposez une carte interactive pour permettre aux utilisateurs de récupérer des informations supplémentaires ;
* **Scénarios de commentaires** , tels que les sondages et les enquêtes.
* interactions qui peuvent être résolues dans un **seul cycle de demande/réponse**, où les résultats sont utiles à plusieurs membres de la conversation.
* **Robots sociaux/loisirs** : obtenez une image de chat attrayante, sélectionnez un gagnant, etc.

### <a name="in-a-group-chat"></a>Dans une conversation de groupe

Les conversations de groupe sont des conversations non thématiques entre trois personnes au minimum. Ils ont tendance à avoir moins de membres qu’un canal et sont plus transitoires. À l’instar d’un canal, votre robot n’a accès qu’aux messages pour lesquels il est `@mentioned` directement.

Les scénarios qui fonctionnent correctement dans un canal fonctionnent généralement également dans une conversation de groupe.

### <a name="in-a-one-on-one-chat"></a>Dans une conversation en un seul

Les bots de conversation interagissent traditionnellement de cette façon avec les utilisateurs. Ils peuvent activer des charges de travail incroyablement diverses. Le bots de questions et réponses, les bots qui initient des flux de travail dans d’autres systèmes, les bots qui font des blagues et les bots qui prennent des notes en sont quelques exemples. N’oubliez pas de déterminer si une interface basée sur une conversation est la meilleure façon de présenter vos fonctionnalités.

## <a name="building-a-teams-bot-with-the-microsoft-bot-framework"></a>Création d’un robot teams avec Microsoft bot Framework

[Microsoft bot Framework](https://dev.botframework.com/) est un kit de développement logiciel (SDK) enrichi pour la création de robots à l’aide de C#, Java, Python ou JavaScript. Si vous disposez déjà d’un bot basé sur l’infrastructure de robot, vous pouvez facilement l’adapter pour qu’elle fonctionne dans Microsoft Teams. Nous vous recommandons d’utiliser C# ou Node.js pour tirer parti de nos [Kits de développement](/microsoftteams/platform/#pivot=sdk-tools)logiciel (SDK). Ces packages étendent les classes et méthodes de base du kit de développement logiciel (SDK) de base, comme suit :

* Utilisez des types de carte spéciaux comme la carte connecteur Office 365.
* Utiliser et définir des données de canal spécifiques aux équipes sur les activités.
* Traiter les demandes d’extension de messagerie.

> [!IMPORTANT]
> Vous pouvez développer des applications teams dans n’importe quelle technologie de programmation Web et appeler directement les [API REST de l’infrastructure bot](/bot-framework/rest-api/bot-framework-rest-overview) , mais vous devez effectuer toutes les manipulations de jetons.

Votre bot teams se compose de trois éléments :

* un service web accessible au public que vous hébergez ;
* Enregistrement de votre bot avec l’infrastructure bot.
* Votre package d’application de teams avec votre manifeste d’application. Il s’agit de ce que vos utilisateurs installeront et connectent le client teams à votre service Web, routé via le service bot.

> [!TIP]
> Teams App Studio * vous permet de créer et de configurer votre manifeste d’application et peut enregistrer votre service Web en tant que bot sur l’infrastructure bot. Il contient également une bibliothèque de contrôle REACT et un générateur de carte interactive. *Consultez la rubrique* [prise en main de Team App Studio](~/concepts/build-and-test/app-studio-overview.md).

## <a name="building-a-teams-bot-with-microsoft-power-virtual-agents"></a>Création d’un bot teams avec les agents virtuels de gestion de l’alimentation Microsoft

[Power Virtual agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) est un service basé sur Microsoft Power Platform and bot Framework. Le processus de développement de l’agent virtuel d’alimentation utilise une approche d’interface graphique guidée, sans code pour permettre à chaque membre de votre équipe de créer et de gérer facilement un agent virtuel intelligent. Une fois que vous avez terminé la création de votre chatbot dans le [portail Power Virtual agents](https://powervirtualagents.microsoft.com), vous pouvez facilement [intégrer vos agents virtuels de puissance chatbot à teams](../../bots/how-to/add-power-virtual-agents-bot-to-teams.md). Pour commencer à créer vos agents de gestion de l’alimentation chatbot, *consultez* la [documentation des agents Virtual Power](https://docs.microsoft.com/power-virtual-agents/).

## <a name="connectors-and-bots"></a>Connecteurs et robots

Les connecteurs vous permettent de créer un robot simple pour une interaction de base, comme le lancement d’un flux de travail ou d’autres commandes simples. Ils vivent uniquement dans l’équipe dans laquelle vous les créez et sont destinés à des processus simples spécifiques au flux de travail de votre entreprise. *Voir* [qu’est-ce qu’un webhooks et un connecteur ?](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) pour plus d’informations.

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
* [Bot de conversation Teams dans JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot)

## <a name="learn-more"></a>En savoir plus

* [Notions de base sur les robots dans teams](~/bots/bot-basics.md)
* [Créer un robot pour Teams](~/bots/how-to/create-a-bot-for-teams.md)
* [Planification de votre application](../../concepts/extensibility-points.md)
* [Conception de votre application].. /(.. /designing-your-app/designing-overview.md)
* [Création de votre application](../../concepts/building-an-app.md)
* [Publication de votre application](../../concepts/deploy-and-publish/overview.md)
