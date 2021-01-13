---
title: Qu’est-ce que les bots de conversation ?
author: clearab
description: Vue d’ensemble des bots de conversation dans Microsoft Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 0304ae436b54db0d111eaed507beb350f1ca4632
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797868"
---
# <a name="what-are-conversational-bots-in-microsoft-teams"></a>Qu’est-ce que les bots de conversation dans Microsoft Teams ?

Les bots de conversation permettent aux utilisateurs d’interagir avec votre service web via du texte, des cartes interactives et des modules de tâches. Ils sont extrêmement flexibles : les bots de conversation peuvent être limitées à la gestion de quelques commandes simples ou d’assistants virtuels complexes, optimisés pour l’intelligence artificielle et de traitement du langage naturel. Il peut s’agit d’un aspect d’une application plus grande ou entièrement autonome.

Le gif ci-dessous montre un utilisateur qui discute avec un bot dans une conversation un-à-un à l’aide de cartes texte et interactives. La recherche de la combinaison de cartes, de texte et de modules de tâche est essentielle pour créer un bot utile. N’oubliez pas que les bots sont bien plus que du texte !

![FAQ Plus gif](~/assets/images/FAQPlusEndUser.gif)

## <a name="build--a-bot-for-teams-with-the-microsoft-bot-framework"></a>Créer un bot pour Teams avec Microsoft Bot Framework

[Microsoft Bot Framework est](https://dev.botframework.com/) un SDK riche pour la création de bots en C#, Java, Python et JavaScript. Si vous avez déjà un bot basé sur Bot Framework, vous pouvez facilement l’adapter pour qu’il fonctionne dans Microsoft Teams. Nous vous recommandons d’utiliser C# ou Node.js pour tirer parti de nos [SDK.](/microsoftteams/platform/#pivot=sdk-tools) Ces packages étendent les classes et méthodes de base du SDK Bot Builder comme suit :

* Utilisez des types de carte spécialisés tels que la carte connecteur Office 365.
* Consommez et définissez des données de canal spécifiques à Teams sur les activités.
* Traiter les demandes d’extension de messagerie.

Votre bot Teams se compose de trois éléments :

* un service web accessible au public que vous hébergez ;
* Inscription de votre bot avec Bot Framework.
* Votre package d’application Teams avec votre manifeste d’application. C’est ce que vos utilisateurs installent et connecte le client Teams à votre service web, acheminé via bot Service.

> [!IMPORTANT]
> Vous pouvez développer des applications Teams dans n’importe quelle technologie de programmation web et appeler directement les API [REST Bot Framework,](/bot-framework/rest-api/bot-framework-rest-overview) mais vous devez effectuer vous-même la gestion de tous les jetons.

> [!TIP]
> Teams App Studio* vous aide à créer et configurer votre manifeste d’application, et peut inscrire votre service web en tant que bot sur Bot Framework. Il contient également une bibliothèque de contrôles React et un générateur de carte interactif. *Voir* [La mise en place de Teams App Studio.](~/concepts/build-and-test/app-studio-overview.md)

## <a name="create-a-chatbot-for-teams-with-microsoft-power-virtual-agents"></a>Créer un chatbot pour Teams avec des agents virtuels Microsoft Power

[Power Virtual Agents est](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) un service chatbot, qui repose sur la plateforme Microsoft Power et Bot Framework.  Le processus de développement de Power Virtual Agent utilise une approche d’interface graphique guidée sans code pour permettre à chaque membre de votre équipe de créer et de gérer facilement un agent virtuel intelligent.  Une fois que vous avez terminé la création de votre chatbot dans le portail [Power Virtual Agents,](https://powervirtualagents.microsoft.com)vous pouvez facilement intégrer votre [chatbot d’agents virtuels Power avec Teams.](how-to/add-power-virtual-agents-bot-to-teams.md) Pour commencer à créer votre chatbot d’agents power virtual, *consultez* la [documentation des agents virtuels Power.](https://docs.microsoft.com/power-virtual-agents/)

## <a name="webhooks-and-connectors"></a>Webhooks et connecteurs

Les webhooks et les connecteurs vous permettent de créer un bot simple pour une interaction de base, par exemple en délant un flux de travail ou d’autres commandes simples. Ils sont uniquement membres de l’équipe dans laquelle vous les créez et sont destinés à des processus simples spécifiques au flux de travail de votre entreprise. *Voir* [que sont les webhooks et les connecteurs ?](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) pour plus d’informations.

## <a name="where-bots-work-best"></a>Où les bots fonctionnent le mieux

Les bots dans Microsoft Teams peuvent faire partie d’une conversation un-à-un, d’une conversation de groupe ou d’un canal dans une équipe. Chaque étendue offre des opportunités et des défis uniques à votre bot de conversation.

### <a name="in-a-channel"></a>Dans un canal

Les canaux contiennent des conversations entre plusieurs personnes, potentiellement un grand nombre de personnes (actuellement, jusqu’à deux milliers). Cela donne potentiellement une très grande portée à votre bot, mais les interactions individuelles doivent être concises. Les interactions classiques à plusieurs tours ne fonctionneront probablement pas très bien. Cherchez plutôt à utiliser des cartes interactives ou des modules de tâche, ou à transformer la conversation en conversation à deux si vous avez besoin de recueillir de nombreuses informations. Votre bot n’aura également accès qu’aux messages où il se trouve directement, bien que vous pouvez récupérer des messages supplémentaires de la conversation à l’aide de Microsoft Graph et d’autorisations élevées au niveau de `@mentioned` l’organisation.

Voici quelques scénarios dans lesquels les bots fonctionnent très bien dans un canal :

* **notifications**, notamment si vous proposez une carte interactive pour permettre aux utilisateurs de récupérer des informations supplémentaires ;
* **Scénarios de commentaires tels** que les sondages et les enquêtes.
* interactions qui peuvent être résolues dans un **seul cycle de demande/réponse**, où les résultats sont utiles à plusieurs membres de la conversation.
* **Bots sociaux/amusants** : obtenez une image de chat incroyable, sélectionnez un gagneur de manière aléatoire, etc.

### <a name="in-a-group-chat"></a>Dans une conversation de groupe

Les conversations de groupe sont des conversations non thématiques entre trois personnes au minimum. Elles ont tendance à avoir moins de membres qu’un canal et sont plus temporaires. Comme pour un canal, votre bot n’aura accès qu’aux messages où il se `@mentioned` trouve directement.

Les scénarios qui fonctionnent bien dans un canal fonctionnent généralement aussi bien dans une conversation de groupe.

### <a name="in-a-one-to-one-chat"></a>Dans une conversation un-à-un

Les bots de conversation interagissent traditionnellement de cette façon avec les utilisateurs. Ils peuvent activer des charges de travail extrêmement diverses. Le bots de questions et réponses, les bots qui initient des flux de travail dans d’autres systèmes, les bots qui font des blagues et les bots qui prennent des notes en sont quelques exemples. N’oubliez pas de déterminer si une interface basée sur la conversation est la meilleure façon de présenter vos fonctionnalités.

## <a name="bot-fails"></a>Le bot échoue

### <a name="having-multi-turn-experiences-in-chat"></a>Expériences à plusieurs tour dans la conversation

Une boîte de dialogue complète entre votre bot et l’utilisateur est un moyen lent et trop complexe d’accomplir une tâche et nécessite également au développeur de maintenir l’état. Pour quitter cet état, l’utilisateur doit avoir le délai d’accès ou taper «*Annuler*». Par-dessus tout, le processus est inutilement fastidieux :

UTILISATEUR : planifier une réunion avec Megan.

BOT : j’ai trouvé 200 résultats, veuillez inclure un prénom et un nom.

UTILISATEUR : planifier une réunion avec Megan Bowen.

BOT : À quelle heure voulez-vous rencontrer Megan Bowen ?

UTILISATEUR : 13:00

BOT : quel jour ?

### <a name="supporting-too-many-commands"></a>Prise en charge d’un trop grand nombre de commandes

Un bot qui prend en charge un nombre excessif de commandes, en particulier un large éventail de commandes, ne sera pas réussi ou n’est pas considéré comme positif par les utilisateurs. Étant donné qu’il n’y a que 6 commandes visibles dans le menu bot actuel, il est peu probable que tout ce qui se trouve en plus ne soit utilisé avec aucune fréquence. Les bots qui vont plus loin dans un domaine spécifique plutôt que d’essayer d’être un grand assistant fonctionnent mieux et s’améliorent.

### <a name="maintaining-a-large-retrieval-knowledge-base-with-unranked-responses"></a>Maintenance d’une base de connaissances de récupération importante avec des réponses nonrankées

Les bots conviennent mieux aux interactions courtes et rapides, sans passer au travers de longues listes à la recherche d’une réponse.

## <a name="get-started"></a>Prise en main

* [Bot de conversation Teams en C#/dotnet](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot)
* [Bot de conversation Teams dans JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot)

## <a name="learn-more"></a>En savoir plus

> [!div class="nextstepaction"]
> [Principes de base des bots dans Teams](~/bots/bot-basics.md)

> [!div class="nextstepaction"]
> [Créer un robot pour Teams](~/bots/how-to/create-a-bot-for-teams.md)
