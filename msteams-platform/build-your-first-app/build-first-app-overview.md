---
title: Get started - Build your first app overview and prerequisites
author: girliemac
description: Découvrez comment commencer à développer des applications Microsoft Teams et configurer votre environnement.
ms.author: timura
ms.date: 03/18/2021
ms.topic: quickstart
ms.openlocfilehash: 3bc99c535ea659f046b65dc26d9a60de0dd49cab
ms.sourcegitcommit: 303fc214aa04757779a171337f31a6539f47fd03
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2021
ms.locfileid: "52068565"
---
# <a name="get-started-with-microsoft-teams-app-development"></a>Mise en place du développement d’applications Microsoft Teams

Créez une application simple pour découvrir les principes de base du développement d’applications Teams. Une fois que vous avez vu « Hello, World! », essayez l’un des autres articles de mise en ligne pour plus d’informations sur les outils courants, les concepts fondamentaux et les fonctionnalités avancées.



## <a name="what-youll-learn"></a>Ce que vous allez apprendre

* Rapidement opérationnel avec la Shared Computer Toolkit Teams, une extension Visual Studio Code 
* Configurer votre application avec App Studio 
* Familiarisez-vous avec les outils de développement et les SDK Teams
* Prenez en compte les concepts importants de l’application Teams, tels que l’authentification et les meilleures pratiques en matière de conception

Vous pouvez créer une application Teams à l’aide de n’importe quelle technologie de votre choix, par exemple, l’interface de ligne de commande (CLI). Toutefois, ces articles vous aident à commencer avec les outils et technologies recommandés suivants :

* Teams Shared Computer Toolkit, une extension Visual Studio code
* React.js pour les onglets
* Node.js pour les bots et les extensions de messagerie


## <a name="teams-app-fundamentals"></a>Principes de base de l’application Teams

Vous pouvez créer des applications Teams personnalisées pour vous-même, les personnes de votre organisation ou les personnes du monde entier. Avant de commencer, vous devez comprendre les concepts fondamentaux suivants concernant le développement d’applications Teams :

### <a name="common-app-use-cases"></a>Cas d’utilisation d’applications courants

Voici quelques scénarios classiques qu’une application Teams personnalisée peut vous aider :

* Incorporer du contenu web, tel qu'une application web ou une partie d'un site web, dans le client Teams
* Rechercher rapidement des informations dans un autre système et les ajouter à une conversation Teams 
* Déclencher des flux de travail et des processus directement à partir de ce qui est dit dans une conversation 

### <a name="app-capabilities-and-tools"></a>Fonctionnalités et outils de l'application

Une application est composé d'une ou de plusieurs fonctionnalités Teams et de points d'interaction utilisateur. Votre groupe d'outils de développement varie en fonction des fonctionnalités que vous souhaitez.

| **Fonctionnalités de l’application**| **Points d'interaction** | **Outils recommandés** | **Kits de développement logiciel (SDK)** | **Piles technologiques** |
|--------|--------|--------|--------|--------|
| Onglets | Espaces dans lequel les utilisateurs peuvent interagir avec du contenu web incorporé dans des contextes personnels et partagés | Vs Code avec l'extension Shared Computer Toolkit Teams ou le générateur Yeoman | Kit de développement logiciel client JavaScript Teams | Technologies web générales (HTML, CSS et JavaScript) ou React.js |
| Bots | Chatbots qui interagissent avec les utilisateurs dans des contextes personnels et partagés | Vs Code avec l'extension Shared Computer Toolkit Teams ou le générateur Yeoman | SDK Bot Botework SDK | Node.js, C# ou Python | 
| Extensions de messagerie | Raccourcis pour insérer du contenu d'application ou agir sur un message sans sortir de la conversation | Vs Code avec l'extension Shared Computer Toolkit Teams ou le générateur Yeoman | Bot Framework SDK | Node.js, C# ou Python |

### <a name="teams-doesnt-host-your-app"></a>Teams n'héberge pas votre application

Lorsqu'un utilisateur installe votre application dans Teams, il installe uniquement un package d'application qui contient un fichier de configuration (également appelé manifeste d'application) et les icônes de votre application. La logique et le stockage de données de votre application sont hébergés ailleurs, tels que les services web Azure ou l'hôte local pendant le développement. Teams accède à ces ressources via HTTPS.

:::image type="content" source="../assets/images/build-your-first-app/app-in-cloud.png" alt-text="Illustration showing your app on Teams is pointing to your app logic in the cloud server.":::

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créer et exécuter votre première application Teams](../build-your-first-app/build-and-run.md)
