---
title: Démarrer - Créez votre première vue d’ensemble de l’application et vos conditions préalables
author: girliemac
description: Découvrez comment commencer avec le développement Microsoft Teams’applications et configurer votre environnement.
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
# <a name="get-started-with-microsoft-teams-app-development"></a>Démarrer avec le développement Microsoft Teams apprapprateur

Créez une application simple pour apprendre les rudiments du développement Teams’application. Une fois que vous voyez « Bonjour, Monde! », essayez l’un des autres articles commencer pour plus d’informations sur les outils communs, les concepts fondamentaux, et les fonctionnalités avancées.



## <a name="what-youll-learn"></a>Ce que vous apprendrez

* Le bon fonctionnement rapide avec le Teams Shared Computer Toolkit, une extension Visual Studio Code rapide. 
* Configurez votre application avec App Studio.
* Familiarisez-vous avec Teams outils de développement et les DTS.
* Considérez les concepts Teams’applications, tels que l’authentification et la conception de meilleures pratiques.

Vous pouvez créer une application Teams en utilisant n’importe quelle technologie de votre choix, par exemple, l’interface de ligne de commande (CLI). Mais, ces articles vous aident à démarrer avec les outils et technologies recommandés suivants:

* Teams Shared Computer Toolkit, une extension Visual Studio Code
* React.js pour les onglets
* Node.js pour les bots et les extensions de messagerie


## <a name="teams-app-fundamentals"></a>Teams fondamentaux de l’application

Vous pouvez créer des applications Teams personnalisées pour vous-même, les personnes dans votre org, ou des personnes partout dans le monde. Avant de commencer, vous devez comprendre les concepts fondamentaux suivants sur le développement Teams appe :

### <a name="common-app-use-cases"></a>Cas d’utilisation d’applications courants

Voici quelques scénarios typiques qu’une application Teams personnalisée peut vous aider :

* Intégrer du contenu web, comme une application Web ou une partie d’un site Web, dans le Teams client.
* Recherchez rapidement des informations dans un autre système et ajoutez-les à une conversation Teams conversation.
* Déclenchez les flux de travail et les processus directement à partir de ce qui est dit dans une conversation.

### <a name="app-capabilities-and-tools"></a>Capacités et outils d’application

Une application est composée d’une ou plusieurs fonctionnalités Teams et de points d’interaction utilisateur. Votre outil de développement varie en fonction des capacités que vous souhaitez.

| **Capacités d’application**| **Points d’interaction** | **Outils recommandés** | **Kits de développement logiciel (SDK)** | **Piles technologiques** |
|--------|--------|--------|--------|--------|
| Onglets | Espaces où les utilisateurs peuvent interagir avec du contenu Web intégré dans des contextes personnels et partagés. | VS Code avec Teams Shared Computer Toolkit extension ou Yeoman Generator | Kit de développement logiciel client JavaScript Teams | Technologies Web générales (HTML, CSS et JavaScript) ou React.js |
| Bots | Chatbots qui interagissent avec les utilisateurs dans des contextes personnels et partagés. | VS Code avec Teams Shared Computer Toolkit extension ou Yeoman Generator | Cadre bot SDK | Node.js, C#, ou Python | 
| Extensions de messagerie | Raccourcis pour insérer du contenu d’application ou agir sur un message sans naviguer loin de la conversation. | VS Code avec Teams Shared Computer Toolkit extension ou Yeoman Generator | Cadre bot SDK | Node.js, C#, ou Python |

### <a name="teams-doesnt-host-your-app"></a>Teams n’héberge pas votre application

Lorsqu’un utilisateur installe votre application en Teams, il n’installe qu’un package d’application contenant un fichier de configuration (également connu sous le nom de manifeste d’application) et les icônes de votre application. La logique et le stockage de données de votre application sont hébergés ailleurs, tels que Azure Web Services ou localhost pendant le développement. Teams accès à ces ressources via HTTPS.

:::image type="content" source="../assets/images/build-your-first-app/app-in-cloud.png" alt-text="Illustration montrant votre application sur Teams pointant vers la logique de votre application dans le serveur cloud.":::

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créez et exécutez votre première application Teams](../build-your-first-app/build-and-run.md)
