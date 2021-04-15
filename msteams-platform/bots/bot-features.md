---
title: Bots et SDK
author: clearab
description: Bots et SDK dans Microsoft Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: c76a3300229e038e0d6a93d2701b3b3c5a1286da
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/13/2021
ms.locfileid: "51697243"
---
# <a name="bots-and-sdks"></a>Bots et SDK

Pour créer un bot qui fonctionne dans Microsoft Teams, vous pouvez utiliser l'une des utilisations suivantes :
* Bot existant créé à partir du SDK Microsoft Bot Framework
* Service Chatbot des agents virtuels Power
* Webhooks et connecteurs

## <a name="bots-and-the-microsoft-bot-framework"></a>Bots et Microsoft Bot Framework

Votre bot Teams se compose des trois éléments suivants :

* un service web accessible au public que vous hébergez ;
* Inscription de votre bot avec Bot Framework.
* Votre package d'application Teams avec votre manifeste d'application. C'est ce que vos utilisateurs installent et connectent le client Teams à votre service web, acheminé via le service bot.

[Bot Framework est](https://dev.botframework.com/) un SDK enrichi utilisé pour créer des bots à l'aide de C#, Java, Python et JavaScript. Si vous avez déjà un bot basé sur Bot Framework, vous pouvez facilement le modifier pour qu'il fonctionne dans Microsoft Teams. Utilisez les C# ou Node.js pour tirer parti de nos [SDK.](/microsoftteams/platform/#pivot=sdk-tools) Ces packages étendent les classes et méthodes de base du SDK Bot Builder comme suit :

* Utilisez des types de carte spécialisés tels que la carte de connecteur Office 365.
* Définir des données de canal spécifiques à Teams sur les activités.
* Traiter les demandes d'extension de messagerie.

> [!IMPORTANT]
> Vous pouvez développer des applications Teams dans n'importe quelle technologie de programmation web et appeler directement les [API REST Bot Framework.](/bot-framework/rest-api/bot-framework-rest-overview) Toutefois, vous devez effectuer la gestion des jetons dans tous les cas.

> [!TIP]
> Teams App Studio vous aide à créer et configurer votre manifeste d'application, et à inscrire votre service web en tant que bot sur Bot Framework. Il contient également une bibliothèque de contrôles React et un générateur de carte interactif. Pour plus d'informations, voir [la mise en place de Teams App Studio.](~/concepts/build-and-test/app-studio-overview.md)

## <a name="bots-and-the-microsoft-power-virtual-agents"></a>Bots et agents virtuels Microsoft Power

[Power Virtual Agents est](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) un service chatbot construit sur la plateforme Microsoft Power et Bot Framework. Le processus de développement de Power Virtual Agent utilise une approche guidée, sans code et interface graphique qui permet aux membres de votre équipe de créer et de gérer facilement un agent virtuel intelligent. Après avoir créé votre chatbot dans le portail [Power Virtual Agents,](https://powervirtualagents.microsoft.com)vous pouvez facilement l'intégrer [à Teams.](how-to/add-power-virtual-agents-bot-to-teams.md) Pour plus d'informations sur la mise en place, voir la [documentation des agents power virtual.](https://docs.microsoft.com/power-virtual-agents/)

## <a name="bots-and-webhooks-and-connectors"></a>Bots, webhooks et connecteurs

Les webhooks et les connecteurs connectent votre bot à vos services web. À l'aide de webhooks et de connecteurs, vous pouvez créer un bot simple pour une interaction de base, comme la création d'un flux de travail ou d'autres commandes simples. Ils sont disponibles uniquement dans l'équipe où vous les créez et sont destinés à des processus simples spécifiques au flux de travail de votre entreprise. Pour plus d'informations, [voir les webhooks et les connecteurs.](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)

## <a name="advantages-of-bots"></a>Avantages des bots

Les bots dans Microsoft Teams peuvent être intégrés dans une conversation à deux, une conversation de groupe ou un canal dans une équipe. Chaque étendue offre des opportunités et des défis uniques pour votre bot de conversation.

| Dans un canal | Dans une conversation de groupe | Dans une conversation un-à-un |
| :-- | :-- | :-- |
| Portée massive | Moins de membres | Méthode traditionnelle |
| Interactions individuelles concises | @mention bot  | Q&A bots |
| @mention bot | Similaire au canal | Bots qui indiquent à leurs personnes et prennent des notes |

### <a name="in-a-channel"></a>Dans un canal

Les canaux contiennent des conversations entre plusieurs personnes, même jusqu'à deux milliers. Cela peut donner à votre bot une portée massive, mais les interactions individuelles doivent être concises. Les interactions multi turn traditionnelles ne fonctionnent pas. Au lieu de cela, vous devez utiliser des cartes interactives ou des modules de tâche, ou déplacer la conversation vers une conversation un-à-un pour collecter de nombreuses informations. Votre bot n'a accès qu'aux messages où il se `@mentioned` trouve. Vous pouvez récupérer des messages supplémentaires à partir de la conversation à l'aide de Microsoft Graph et des autorisations au niveau de l'organisation.

Les bots fonctionnent mieux dans un canal dans les cas suivants :

* Notifications, dans laquelle vous fournissez une carte interactive pour que les utilisateurs prennent des informations supplémentaires.
* Scénarios de commentaires, tels que les sondages et les enquêtes.
* Un cycle de demande ou de réponse unique résout les interactions et les résultats sont utiles pour plusieurs membres de la conversation.
* Bots sociaux ou amusants, où vous obtenez une image de chat incroyable, choisissez un gagneur de manière aléatoire, etc.

### <a name="in-a-group-chat"></a>Dans une conversation de groupe

Les conversations de groupe sont des conversations non thématiques entre trois personnes au minimum. Elles impliquent généralement moins de membres qu’un canal et sont plus éphémères. Comme pour un canal, votre bot n'a accès qu'aux messages où il `@mentioned` se trouve directement.

Dans les cas où les bots fonctionnent mieux dans un canal, ils fonctionnent également mieux dans une conversation de groupe.

### <a name="in-a-one-to-one-chat"></a>Dans une conversation un-à-un

La conversation un-à-un est un moyen traditionnel pour un bot de conversation d'interagir avec un utilisateur. Voici quelques exemples de bots de conversation un-à-un : les bots Q&A, les bots qui lancent des flux de travail dans d'autres systèmes, les bots qui indiquent les conversations et les bots qui prennent des notes. Avant de créer des chatbots un-à-un, pensez à déterminer si une interface basée sur la conversation est la meilleure façon de présenter vos fonctionnalités.

## <a name="disadvantages-of-bots"></a>Inconvénients des bots

Une boîte de dialogue complète entre votre bot et l'utilisateur est un moyen lent et complexe d'accomplir une tâche. Un bot qui prend en charge un nombre excessif de commandes, en particulier un large éventail de commandes, ne réussit pas ou n'est pas considéré comme positif par les utilisateurs.

### <a name="have-multi-turn-experiences-in-chat"></a>Avoir des expériences à plusieurs tour dans la conversation

Une boîte de dialogue complète nécessite que le développeur conserve l'état. Pour quitter cet état, l'utilisateur doit avoir le délai d'accès ou sélectionner **Annuler**. En outre, le processus est fastidieux. Par exemple, consultez le scénario de conversation suivant :

UTILISATEUR : planifier une réunion avec Megan.

BOT : j'ai trouvé 200 résultats, veuillez inclure un prénom et un nom.

UTILISATEUR : planifier une réunion avec Megan Bowen.

BOT : À quelle heure voulez-vous rencontrer Megan Bowen ?

UTILISATEUR : 13:00

BOT : quel jour ?

### <a name="support-too-many-commands"></a>Prise en charge d'un trop grand nombre de commandes

Comme il n'existe que six commandes visibles dans le menu bot actuel, il est peu probable que tout ce qui se trouve en plus soit utilisé avec une fréquence quelconque. Bots qui vont plus loin dans un domaine spécifique plutôt que d'essayer d'être un travail d'assistant large et mieux.

### <a name="maintain-a-large-knowledge-base"></a>Gérer une base de connaissances importante

L'un des inconvénients des bots est qu'il est difficile de maintenir une base de connaissances de récupération importante avec des réponses nonrankées. Les bots conviennent mieux pour les interactions courtes et rapides, et ne pas passer au travers de longues listes à la recherche d'une réponse.

## <a name="code-sample"></a>Exemple de code

|Exemple de nom | Description | . NETCore | Node.js |
|----------------|-----------------|--------------|----------------|
| Bot de conversation Teams | Gestion des événements de messagerie et de conversation. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot)|

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Bot activity handlers](~/bots/bot-basics.md)
