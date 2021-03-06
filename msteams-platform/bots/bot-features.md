---
title: Bots et kits de développement
author: surbhigupta
description: Vue d’ensemble des outils et des SDK pour la création Microsoft Teams bots.
ms.topic: overview
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: c346d7b7a1c720e651a847fb8a650fc549689654
ms.sourcegitcommit: f62634c59b697107e5bb3c38867b21007d328b1e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/29/2021
ms.locfileid: "53196242"
---
# <a name="bots-and-sdks"></a>Bots et kits de développement

Vous pouvez créer un bot qui fonctionne dans Microsoft Teams avec l’un des outils ou fonctionnalités suivants :

* [Microsoft Bot Framework SDK](#bots-with-the-microsoft-bot-framework)
* [Power Virtual Agents](#bots-with-power-virtual-agents)
* [Virtual Assistant](~/samples/virtual-assistant.md)
* [Webhooks et connecteurs](#bots-with-webhooks-and-connectors)

## <a name="bots-with-the-microsoft-bot-framework"></a>Bots avec le Microsoft Bot Framework

Votre bot Teams se compose des suivants :

* Un service web accessible au public hébergé par vous.
* Une inscription Bot Framework pour votre service web.
* Votre Teams d’application, qui connecte le client Teams à votre service web.

> [!TIP]
> Utilisez le portail du développeur pour inscrire votre service web auprès de Bot Framework et spécifier les configurations de votre application. Pour plus d’informations, [voir gérer vos applications avec le portail](~/concepts/build-and-test/teams-developer-portal.md)de développement pour Teams .

[Bot Framework est](https://dev.botframework.com/) un SDK enrichi utilisé pour créer des bots à l’aide de C#, Java, Python et JavaScript. Si vous avez déjà un bot basé sur Bot Framework, vous pouvez facilement le modifier pour qu’il fonctionne Teams. Utilisez les C# ou Node.js pour tirer parti de nos [SDK.](/microsoftteams/platform/#pivot=sdk-tools) Ces packages étendent les classes et méthodes de base du SDK Bot Builder comme suit :

* Utilisez des types de carte spécialisés tels que la carte Office 365 connecteur.
* Définissez Teams données de canal spécifiques sur les activités.
* Traiter les demandes d’extension de messagerie.

> [!IMPORTANT]
> Vous pouvez développer des Teams dans n’importe quelle technologie de programmation web et appeler directement les [API REST Bot Framework.](/bot-framework/rest-api/bot-framework-rest-overview) Toutefois, vous devez effectuer la gestion des jetons dans tous les cas.

## <a name="bots-with-power-virtual-agents"></a>Bots avec Power Virtual Agents

[Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) est un service chatbot construit sur la plateforme Microsoft Power et Bot Framework. Le processus de développement de Power Virtual Agent utilise une approche guidée, sans code et interface graphique qui permet aux membres de votre équipe de créer et de gérer facilement un agent virtuel intelligent. Après avoir créé votre chatbot dans le [portail Power Virtual Agents,](https://powervirtualagents.microsoft.com)vous pouvez facilement l’intégrer [à Teams](how-to/add-power-virtual-agents-bot-to-teams.md). Pour plus d’informations sur la mise en place, [voir Power Virtual Agents documentation.](/power-virtual-agents)

## <a name="bots-with-webhooks-and-connectors"></a>Bots avec webhooks et connecteurs

Les webhooks et les connecteurs connectent votre bot à vos services web. À l’aide de webhooks et de connecteurs, vous pouvez créer un bot simple pour une interaction de base, comme la création d’un flux de travail ou d’autres commandes simples. Ils sont disponibles uniquement dans l’équipe où vous les créez et sont destinés à des processus simples spécifiques au flux de travail de votre entreprise. Pour plus d’informations, [voir les webhooks et les connecteurs.](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)

## <a name="advantages-of-bots"></a>Avantages des bots

Les bots dans Microsoft Teams peuvent être intégrés dans une conversation à deux, une conversation de groupe ou un canal dans une équipe. Chaque étendue offre des opportunités et des défis uniques pour votre bot de conversation.

| Dans un canal | Dans une conversation de groupe | Dans une conversation un-à-un |
| :-- | :-- | :-- |
| Portée massive | Moins de membres | Méthode traditionnelle |
| Interactions individuelles concises | @mention bot  | Q&A bots |
| @mention bot | Similaire au canal | Bots qui indiquent à leurs personnes et prennent des notes |

### <a name="in-a-channel"></a>Dans un canal

Les canaux contiennent des conversations entre plusieurs personnes, même jusqu’à deux milliers. Cela peut donner à votre bot une portée massive, mais les interactions individuelles doivent être concises. Les interactions multi turn traditionnelles ne fonctionnent pas. Au lieu de cela, vous devez utiliser des cartes interactives ou des modules de tâche, ou déplacer la conversation vers une conversation un-à-un pour collecter de nombreuses informations. Votre bot n’a accès qu’aux messages où il se `@mentioned` trouve. Vous pouvez récupérer des messages supplémentaires à partir de la conversation à l’aide Graph microsoft et des autorisations au niveau de l’organisation.

Les bots fonctionnent mieux dans un canal dans les cas suivants :

* Notifications, dans laquelle vous fournissez une carte interactive pour que les utilisateurs prennent des informations supplémentaires.
* Scénarios de commentaires, tels que les sondages et les enquêtes.
* Un cycle de demande ou de réponse unique résout les interactions et les résultats sont utiles pour plusieurs membres de la conversation.
* Bots sociaux ou amusants, où vous obtenez une image de chat incroyable, choisissez un gagneur de manière aléatoire, etc.

### <a name="in-a-group-chat"></a>Dans une conversation de groupe

Les conversations de groupe sont des conversations non thématiques entre trois personnes au minimum. Elles impliquent généralement moins de membres qu’un canal et sont plus éphémères. Comme pour un canal, votre bot n’a accès qu’aux messages où il `@mentioned` se trouve directement.

Dans les cas où les bots fonctionnent mieux dans un canal, ils fonctionnent également mieux dans une conversation de groupe.

### <a name="in-a-one-to-one-chat"></a>Dans une conversation un-à-un

La conversation un-à-un est un moyen traditionnel pour un bot de conversation d’interagir avec un utilisateur. Voici quelques exemples de bots de conversation un-à-un : les bots Q&A, les bots qui lancent des flux de travail dans d’autres systèmes, les bots qui indiquent les conversations et les bots qui prennent des notes. Avant de créer des chatbots un-à-un, pensez à déterminer si une interface basée sur la conversation est la meilleure façon de présenter vos fonctionnalités.

## <a name="disadvantages-of-bots"></a>Inconvénients des bots

Une boîte de dialogue complète entre votre bot et l’utilisateur est un moyen lent et complexe d’accomplir une tâche. Un bot qui prend en charge un nombre excessif de commandes, notamment un large éventail de commandes, ne réussit pas ou n’est pas considéré comme positif par les utilisateurs.

### <a name="have-multi-turn-experiences-in-chat"></a>Avoir des expériences à plusieurs tour dans la conversation

Une boîte de dialogue complète nécessite que le développeur conserve l’état. Pour quitter cet état, l’utilisateur doit avoir le délai d’accès ou sélectionner **Annuler**. En outre, le processus est fastidieux. Par exemple, consultez le scénario de conversation suivant :

UTILISATEUR : planifier une réunion avec Megan.

BOT : j’ai trouvé 200 résultats, veuillez inclure un prénom et un nom.

UTILISATEUR : planifier une réunion avec Megan Bowen.

BOT : À quelle heure voulez-vous rencontrer Megan Bowen ?

UTILISATEUR : 13:00

BOT : quel jour ?

### <a name="support-too-many-commands"></a>Prise en charge d’un trop grand nombre de commandes

Comme il n’existe que six commandes visibles dans le menu bot actuel, il est peu probable que tout ce qui se trouve en plus soit utilisé avec une fréquence quelconque. Bots qui vont plus loin dans un domaine spécifique plutôt que d’essayer d’être un travail d’assistant large et mieux.

### <a name="maintain-a-large-knowledge-base"></a>Maintenir une base de connaissances importante

L’un des inconvénients des bots est qu’il est difficile de maintenir une base de connaissances de récupération importante avec des réponses nonrankées. Les bots conviennent mieux pour les interactions courtes et rapides, et ne pas passer au travers de longues listes à la recherche d’une réponse.

## <a name="code-sample"></a>Exemple de code

|Exemple de nom | Description | . NETCore | Node.js |
|----------------|-----------------|--------------|----------------|
| Bot de conversation Teams | Gestion des événements de messagerie et de conversation. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot)|

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Gestionnaire d'activité du robot](~/bots/bot-basics.md)
