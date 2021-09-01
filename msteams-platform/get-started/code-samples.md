---
title: Exemples de code d’application
description: Liens et descriptions d’exemples d’applications pour la plateforme Microsoft Teams développeur
localization_priority: Normal
ms.topic: reference
keywords: Microsoft Teams exemples de développeur
ms.openlocfilehash: c261aebc327d09265db8831c2b7a8549f30a34fe
ms.sourcegitcommit: 68f5411f5989ac706b6a4a7b2884296e145fe7c4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/01/2021
ms.locfileid: "58849425"
---
# <a name="overview"></a>Aperçu

Dans ce didacticiel, vous allez apprendre à créer une application à l’aide de React, Blazor, SPFx, C# ou .NET, Node.js et le générateur Yeoman. Vous allez également apprendre à créer votre premier bot et votre première extension de messagerie. Ce didacticiel vous guidera dans plusieurs exemples de code pour les onglets, les bots, les extensions de messagerie, les webhooks et les connecteurs et les API Graph qui vous aideront à personnaliser et configurer vos applications. En outre, vous pouvez également consulter les sections Microsoft Learn dans laquelle vous pouvez étendre les fonctionnalités de la plateforme Teams développeur en créant des applications personnalisées.  

## <a name="getting-started-with-microsoft-learn"></a>Mise en place de Microsoft Learn

| **Fonctionnalité**| **Module Learn**|
|--------|-------------|
| Onglets : expériences web incorporées  |  [Créez des expériences web incorporées avec les onglets pour Microsoft Teams](/learn/modules/embedded-web-experiences/) |
| Webhooks et connecteurs  |  [Connecter des services web à Microsoft Teams à l’aide de webhooks et de connecteurs Office 365](/learn/modules/msteams-webhooks-connectors/) |
|Extensions de messagerie  | [Interactions orientées sur des tâches dans Microsoft Teams avec les extensions de messagerie](/learn/modules/msteams-messaging-extensions/)  |
| Modules de tâche |  [Collecter des entrées dans Microsoft Teams modules de tâche](/learn/modules/msteams-task-modules/) |
| Bots conversationnels  | [Créer des bots conversationnels interactifs pour Microsoft Teams](/learn/modules/msteams-conversation-bots/)  |

## <a name="build-your-first-microsoft-teams-app-overview"></a>Créer votre première vue d’Microsoft Teams application

Dans les **leçons de mise** en ligne, vous allez apprendre à créer des applications Teams de base. Chaque didacticiel montre comment créer une application Teams simple et réelle tout en vous présentant des outils courants, des concepts fondamentaux et des fonctionnalités plus avancées.

### <a name="teams-app-fundamentals"></a>Teams de base de l’application

La [plateforme Teams développeur vous](../overview.md) permet de créer des applications personnalisées. Voici quelques scénarios courants pour lesquelles une application Microsoft Teams personnalisée peut être utile :

* Incorporez votre site web ou votre application web directement dans le client Teams.
* Aidez les utilisateurs à rechercher rapidement des informations dans un autre système et à ajouter les résultats à une conversation dans Teams.
* Déclenchez des flux de travail et des processus sur la base d’une conversation dans Teams, en conservant le contexte de la conversation.

Avant de commencer les didacticiels, vous devez connaître les informations suivantes sur la création d’applications pour Teams.

### <a name="app-capabilities"></a>Fonctionnalités de l’application

Une Teams’application est composé d’une ou de plusieurs fonctionnalités de [plateforme](../concepts/capabilities-overview.md) et de [points d’interaction utilisateur.](../concepts/extensibility-points.md)

Selon les fonctionnalités que vous souhaitez pour votre application, vous aurez besoin d’un groupe d’outils de développement approprié.

| Fonctionnalités de l’application | Interactions avec l’utilisateur | Outils recommandés | Kits de développement logiciel (SDK) | Piles technologiques |
|--------|-------------|--------|--------|--------|
| Onglets | Une expérience web incorporée en plein écran. | VS Code avec une extension Teams Shared Computer Toolkit, ou YoTeams (générateur Yeoman) | [Teams SDK client](/javascript/api/overview/msteams-client) | Technologie web en général, HTML, CSS et JavaScript |
| Bots | Bot de conversation qui converse avec les membres. | VS Code avec une extension Teams Shared Computer Toolkit, ou YoTeams (générateur Yeoman) | [Bot Framework SDK](https://dev.botframework.com/) | Node.js, C# ou Python |
| Extensions de messagerie | Raccourcis pour insérer du contenu externe dans une conversation ou prendre des mesures sur les messages. | VS Code avec une extension Teams Shared Computer Toolkit, ou YoTeams (générateur Yeoman) | [Bot Framework SDK](https://dev.botframework.com/) | Node.js, C# ou Python |

La section Commencer vous présente les ensembles d’outils recommandés et les technologies couramment utilisées, telles que les Visual Studio Code avec extension Teams, les React.js pour les onglets et les Node.js pour les bots et les extensions de messagerie, même si vous n’êtes pas limité à l’utilisation de ces piles *particulières.*

Si vous préférez utiliser une interface de ligne de commande (CLI), voir créer votre première application [Microsoft Teams’aide du générateur Yeoman.](../get-started/get-started-yeoman.md)

### <a name="teams-does-not-host-your-app"></a>Teams n’héberge pas votre application

Vous installerez uniquement un package d’application qui contient un fichier de configuration, appelé manifeste et icônes d’application Teams client. Le reste des logiques d’application et du stockage de données sont hébergés ailleurs, tels que les services web Azure. Votre application dans le cloud ou localhost pendant vos accès de développement Teams via HTTPS.

:::image type="content" source="../assets/images/build-your-first-app/app-in-cloud.png" alt-text="Illustration showing your app on Teams is pointing to your app logic in the cloud server.":::

## <a name="see-also"></a>Voir aussi

* [Créer une application à l’aide React](first-app-react.md)
* [Créer une application à l’aide de Blazor](first-app-blazor.md)
* [Créer une application à l’aide SPFx](first-app-spfx.md)
* [Créer une application en utilisant C# ou .NET](get-started-dotnet-app-studio.md)
* [Créer une application en utilisant Node.js](get-started-nodejs-app-studio.md)
* [Créer une application à l’aide du générateur Yeoman](get-started-yeoman.md)
* [Créer une application de bot de conversation](first-app-bot.md)
* [Créer une extension de messagerie](first-message-extension.md)
* [Exemples de code](https://github.com/OfficeDev/Microsoft-Teams-Samples)
