---
title: Qu’est-ce que les robots de conversation ?
author: clearab
description: Vue d’ensemble des robots de conversation dans Microsoft Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: a88d516c57faa96e29de3e786910a13c4d65ac84
ms.sourcegitcommit: 61c93b22490526b1de87c0b14a3c7eb6e046caf6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/31/2020
ms.locfileid: "44453867"
---
# <a name="what-are-conversational-bots"></a>Qu’est-ce que les robots de conversation ?

Les bots de conversation permettent aux utilisateurs d’interagir avec votre service web via du texte, des cartes interactives et des modules de tâches. Ils sont incroyablement flexibles : les robots de conversation peuvent être délimités pour gérer quelques commandes simples ou des assistants virtuels complexes, équipés d’intelligence artificielle et de traitement naturel en langue naturelle. Il peut s’agir d’un aspect d’une application plus grande ou totalement autonome.

L’image GIF ci-dessous montre un utilisateur qui contourne un bot dans une conversation un-à-un en utilisant des cartes de texte et des cartes interactives. Trouver le bon mélange de cartes, de texte et de modules de tâches est essentiel pour créer un bot utile. N’oubliez pas que les robots sont bien plus qu’un simple texte !

![Forum aux questions et GIF](~/assets/images/FAQPlusEndUser.gif)

## <a name="build--a-bot-for-teams-with-the-microsoft-bot-framework"></a>Créer un bot pour teams avec Microsoft bot Framework

Microsoft bot Framework] ( https://dev.botframework.com/) Kit de développement logiciel (SDK) enrichi pour la création de robots à l’aide de C#, Java, Python et JavaScript. Si vous disposez déjà d’un bot basé sur l’infrastructure de robot, vous pouvez facilement l’adapter pour qu’elle fonctionne dans Microsoft Teams. Nous vous recommandons d’utiliser C# ou node. js pour tirer parti de nos [Kits de développement](/microsoftteams/platform/#pivot=sdk-tools)logiciel (SDK). Ces packages étendent les classes et méthodes de base du kit de développement logiciel (SDK) de base, comme suit :

* Utilisez des types de carte spéciaux comme la carte connecteur Office 365.
* Utiliser et définir des données de canal spécifiques aux équipes sur les activités.
* Traiter les demandes d’extension de messagerie.

Votre bot teams se compose de trois éléments :

* un service web accessible au public que vous hébergez ;
* Enregistrement de votre bot avec l’infrastructure bot.
* Votre package d’application de teams avec votre manifeste d’application. Il s’agit de ce que vos utilisateurs installeront et connectent le client teams à votre service Web, routé via le service bot.

> [!IMPORTANT]
> Vous pouvez développer des applications teams dans n’importe quelle technologie de programmation Web et appeler directement les [API REST de l’infrastructure bot](/bot-framework/rest-api/bot-framework-rest-overview) , mais vous devez effectuer toutes les manipulations de jetons.

> [!TIP]
> Teams App Studio * vous permet de créer et de configurer votre manifeste d’application et peut enregistrer votre service Web en tant que bot sur l’infrastructure bot. Il contient également une bibliothèque de contrôle REACT et un générateur de carte interactive. *Consultez la rubrique* [prise en main de Team App Studio](~/concepts/build-and-test/app-studio-overview.md).

## <a name="create-a-chatbot-for-teams-with-microsoft-power-virtual-agents"></a>Créer un chatbot pour teams avec Microsoft Power Virtual agents

Les [agents Virtual Power](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) sont un service chatbot, basé sur Microsoft Power Platform and bot Framework.  Le processus de développement de l’agent virtuel d’alimentation utilise une approche d’interface graphique guidée, sans code pour permettre à chaque membre de votre équipe de créer et de gérer facilement un agent virtuel intelligent.  Une fois que vous avez terminé la création de votre chatbot dans le [portail Power Virtual agents](https://powervirtualagents.microsoft.com), vous pouvez facilement [intégrer vos agents virtuels de puissance chatbot à teams](how-to/add-power-virtual-agents-bot-to-teams.md). Pour commencer à créer vos agents de gestion de l’alimentation chatbot, *consultez* la [documentation des agents Virtual Power](https://docs.microsoft.com/power-virtual-agents/).

## <a name="webhooks-and-connectors"></a>Webhooks et connecteurs

Les connecteurs et les webhooks vous permettent de créer un robot simple pour une interaction de base, comme le lancement d’un flux de travail ou d’autres commandes simples. Ils vivent uniquement dans l’équipe dans laquelle vous les créez et sont destinés à des processus simples spécifiques au flux de travail de votre entreprise. *Voir* [qu’est-ce qu’un webhooks et un connecteur ?](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) pour plus d’informations.

## <a name="where-bots-work-best"></a>Fonctionnement optimal des robots

Les robots de Microsoft teams peuvent faire partie d’une conversation un-à-un, d’une conversation de groupe ou d’un canal dans une équipe. Chaque étendue fournit des opportunités et des défis uniques pour votre robot de conversation.

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

### <a name="in-a-one-to-one-chat"></a>Dans une conversation un-à-un

Les bots de conversation interagissent traditionnellement de cette façon avec les utilisateurs. Ils peuvent activer des charges de travail incroyablement diverses. Le bots de questions et réponses, les bots qui initient des flux de travail dans d’autres systèmes, les bots qui font des blagues et les bots qui prennent des notes en sont quelques exemples. N’oubliez pas de déterminer si une interface basée sur une conversation est la meilleure façon de présenter vos fonctionnalités.

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

> [!div class="nextstepaction"]
> [Notions de base sur les robots dans teams](~/bots/bot-basics.md)

> [!div class="nextstepaction"]
> [Créer un robot pour Teams](~/bots/how-to/create-a-bot-for-teams.md)
