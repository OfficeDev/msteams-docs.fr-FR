---
title: Get started - Build your first app overview and prerequisites
author: girliemac
description: Découvrez comment prendre en Microsoft Teams développement d’applications et configurer votre environnement.
ms.author: timura
ms.date: 03/18/2021
ms.topic: quickstart
ms.openlocfilehash: dae942be9383ef1e0a931d238e6148651f334ef5
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565878"
---
# <a name="get-started-with-microsoft-teams-app-development"></a>Prendre en Microsoft Teams développement d’applications

Créez une application simple pour découvrir les principes de base du Teams développement d’applications. Une fois que vous avez vu « Hello, World! », essayez l’un des autres articles de mise en ligne pour plus d’informations sur les outils courants, les concepts fondamentaux et les fonctionnalités avancées.



## <a name="what-youll-learn"></a>Ce que vous allez apprendre

* Préparez-vous rapidement avec l’extension Teams Shared Computer Toolkit, une extension Visual Studio Code’extension. 
* Configurez votre application avec App Studio.
* Familiarisez-vous Teams des outils de développement et des SDK.
* Prenez en compte Teams concepts d’application, tels que l’authentification et les meilleures pratiques en matière de conception.

Vous pouvez créer une application Teams à l’aide de n’importe quelle technologie de votre choix, par exemple, l’interface de ligne de commande (CLI). Toutefois, ces articles vous aident à commencer avec les outils et technologies recommandés suivants :

* Teams Shared Computer Toolkit, une extension Visual Studio Code
* React.js pour les onglets
* Node.js pour les bots et les extensions de messagerie


## <a name="teams-app-fundamentals"></a>Teams de base de l’application

Vous pouvez créer des applications Teams personnalisées pour vous-même, les personnes de votre organisation ou les personnes du monde entier. Avant de commencer, vous devez comprendre les concepts fondamentaux suivants concernant Teams développement d’applications :

### <a name="common-app-use-cases"></a>Cas d’utilisation d’applications courants

Voici quelques scénarios classiques qu’une application Teams personnalisée peut vous aider :

* Incorporez du contenu web, tel qu’une application web ou une partie d’un site web, dans Teams client.
* Recherchez rapidement des informations dans un autre système et ajoutez-les à une conversation Teams conversation.
* Déclencher des flux de travail et des processus directement à partir de ce qui est dit dans une conversation.

### <a name="app-capabilities-and-tools"></a>Fonctionnalités et outils de l’application

Une application est composé d’un ou de plusieurs Teams et de points d’interaction utilisateur. Votre groupe d’outils de développement varie en fonction des fonctionnalités que vous souhaitez.

| **Fonctionnalités de l’application**| **Points d’interaction** | **Outils recommandés** | **Kits de développement logiciel (SDK)** | **Piles technologiques** |
|--------|--------|--------|--------|--------|
| Onglets | Espaces dans lequel les utilisateurs peuvent interagir avec du contenu web incorporé dans des contextes personnels et partagés. | VS Code avec une extension Teams Shared Computer Toolkit ou le générateur Yeoman | Kit de développement logiciel client JavaScript Teams | Technologies web générales (HTML, CSS et JavaScript) ou React.js |
| Bots | Chatbots qui interagissent avec les utilisateurs dans des contextes personnels et partagés. | VS Code avec une extension Teams Shared Computer Toolkit ou le générateur Yeoman | Bot Framework SDK | Node.js, C# ou Python | 
| Extensions de messagerie | Raccourcis pour insérer du contenu d’application ou agir sur un message sans sortir de la conversation. | VS Code avec une extension Teams Shared Computer Toolkit ou le générateur Yeoman | Bot Framework SDK | Node.js, C# ou Python |

### <a name="teams-doesnt-host-your-app"></a>Teams n’héberge pas votre application

Lorsqu’un utilisateur installe votre application dans Teams, il installe uniquement un package d’application qui contient un fichier de configuration (également appelé manifeste d’application) et les icônes de votre application. La logique et le stockage de données de votre application sont hébergés ailleurs, tels que les services web Azure ou l’hôte local pendant le développement. Teams accède à ces ressources via HTTPS.

:::image type="content" source="../assets/images/build-your-first-app/app-in-cloud.png" alt-text="Illustration showing your app on Teams is pointing to your app logic in the cloud server.":::

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créer et exécuter votre première application Teams de messagerie](../build-your-first-app/build-and-run.md)
