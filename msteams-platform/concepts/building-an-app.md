---
title: Création d’une application pour Microsoft teams
author: clearab
description: Comprendre le processus standard de création d’une application pour Microsoft Teams.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 748b5cf6c6bc1bf51c1f647348012057627d2679
ms.sourcegitcommit: d0ca6a4856ffd03d197d47338e633126723fa78a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2020
ms.locfileid: "45137646"
---
# <a name="building-an-app-for-microsoft-teams"></a>Création d’une application pour Microsoft teams

> [!NOTE] 
> Vous cherchez à commencer rapidement ? Vous pouvez créer des applications teams avec [Microsoft teams Toolkit et Visual Studio code](../toolkit/visual-studio-code-overview.md).

La création et la distribution d’une application basée sur la plateforme Microsoft Teams implique de choisir ce qui doit être créé, de créer vos services Web, de créer un package d’application et de distribuer ce package à vos utilisateurs finaux cibles. Il incombe aux administrateurs d’une organisation de décider qui peut accéder à votre application et l’installer, et à vos utilisateurs d’installer l’application dans n’importe quel contexte particulier.

## <a name="design-a-great-app"></a>Concevoir une application intéressante

L’étape la plus importante dans la création d’une application réussie pour Microsoft Teams consiste à choisir la combinaison appropriée de points d’extension et d’éléments de l’interface utilisateur pour en tirer parti. Parfois, il s’agit d’une décision assez simple, mais pour les applications plus complexes, vous devez consacrer beaucoup de temps à comprendre le problème que vous tentez de résoudre avec votre application et à mapper votre solution sur les différentes façons dont les utilisateurs peuvent interagir avec votre application dans le client Microsoft Teams. Ne sous-estimez pas l’importance du contexte et de la portée !. Un robot de conversation qui fonctionne très bien dans une conversation à deux peut ne pas fonctionner du tout dans le cadre d’une conversation de groupe ou d’une conversation de canal.

1. Tout d’abord, [comprenez les points d’extensibilité du client teams et les éléments d’interface utilisateur](~/concepts/extensibility-points.md) disponibles pour votre application.

2. Ensuite, assurez-vous que vous [comprenez vos cas d’utilisation](~/concepts/design/understand-use-cases.md).

3. Enfin, [Mappez vos cas d’utilisation aux fonctionnalités de la plateforme teams](~/concepts/design/map-use-cases.md).

Une fois que vous avez décidé des points et des fonctionnalités d’extensibilité de votre application, vous devez réfléchir à chacune de ces interactions. En fonction de la conception de votre application, vous pouvez consulter les éléments suivants :

* [Création d’onglets intéressants](~/tabs/design/tabs.md)
* [Conception de robots de conversation utiles](~/bots/design/bots.md)

## <a name="prepare-your-environment"></a>Préparer votre environnement

Vous devez vous assurer que vous disposez d’un environnement dans lequel vous pouvez télécharger et tester votre application Teams. Si vous ne disposez pas déjà d’un abonnement O365 avec teams activé et de la possibilité de télécharger des applications, vous pouvez vous [inscrire au programme pour les développeurs o365](https://developer.microsoft.com/microsoft-365/dev-program) , qui vous donnera accès à un abonnement Office 365 gratuit à des fins de développement.

Pour plus d’informations, consultez [la rubrique prepare Your Office 365 Environment](~/concepts/build-and-test/prepare-your-o365-tenant.md) .

## <a name="build-and-test-your-app"></a>Concevoir et tester votre application

La création et le test de votre application pour Microsoft Teams ne sont pas très différentes de la création d’une autre application Web. La principale différence est la nécessité d’utiliser le manifeste de votre application dans votre package d’application pour connecter le client teams à vos services Web. Chaque fois que vous modifiez le manifeste de votre application, vous devez télécharger de nouveau votre package d’application, puis mettre à jour votre application dans teams en la réinstallant. Les modifications apportées à votre service Web ne nécessitent toutefois pas de réinstaller votre application dans le client Teams.

Lors de la création initiale de votre application, vous devez régulièrement mettre à jour les services Web et le package de votre application, généralement en téléchargeant et en installant l’application dans le client teams plusieurs fois (en particulier lors de la configuration initiale de votre application). Toutefois, à mesure que ce que vous créez se stabilise, la nécessité de modifier le manifeste de votre application diminue et vous devrez apporter des modifications à votre service Web.

### <a name="build-your-web-services"></a>Créer vos services Web

Une fois que vous avez décidé de la façon dont les utilisateurs vont interagir avec votre application, il est temps de créer les services Web pour la mettre en place. En fonction de ce que vous créez, Teams fournit divers kits de développement logiciel (SDK), modèles, exemples de code et générateurs pour vous aider à démarrer, notamment :

* Kit de développement logiciel (SDK) de robot pour les [extensions de messagerie](~/messaging-extensions/what-are-messaging-extensions.md) et les [robots de conversation](~/bots/what-are-bots.md)
* Kit de développement logiciel Java client teams pour les [onglets](~/tabs/what-are-tabs.md) et autres pages de contenu
* [Générateur Yeoman](~/tutorials/get-started-yeoman.md) pour la création d’applications dans Node.js
* **Aperçu** Un ensemble de contrôles Open source pour vos pages de contenu Web- [interface utilisateur Fluent](https://microsoft.github.io/fluent-ui-react/)
* [Modèles d’application](~/samples/app-templates.md) prêts pour la production
* Différents [exemples](~/samples/code-samples.md) pour vous aider à commencer

N’oubliez pas que vous devez héberger vos services Web de façon à ce qu’ils soient accessibles au public sur Internet (généralement chez un fournisseur de services Cloud tel qu’Azure) et diffuser votre contenu via HTTPs.

### <a name="create-your-app-package"></a>Créer votre package d’application

Vous devrez également créer un package d’application qui peut être distribué et installé dans Microsoft Teams. Le package d’application contient deux icônes et un fichier manifeste JSON qui décrit les métadonnées de votre application, les points d’extension utilisés par votre application et les pointeurs vers les services qui redirigent ces points d’extension.

Lors de la création de votre package d’application, vous pouvez choisir de le créer manuellement ou d’utiliser App Studio qui vous permet de créer des applications Teams (très Meta). App Studio vous guide tout au long de la création de votre manifeste d’application et peut vous aider à enregistrer votre robot à l’aide de Bot Framework. Il contient également un concepteur de cartes qui vous aide à créer visuellement des cartes et des actions de carte et vous envoie des exemples dans Teams.

## <a name="distributing-your-app"></a>Distribution de votre application

Vous disposez de trois options pour [distribuer votre application Microsoft teams](~/concepts/deploy-and-publish/apps-publish.md), en fonction de votre public cible.

* **Partager directement votre package d’application.** Vous pouvez choisir de partager votre package d’application directement avec les utilisateurs. Ceci est particulièrement utile si votre application est dirigée vers un public limité (quelques équipes ou individus), et Pendant le développement et le test de votre application.
  
* **Publiez votre application dans le catalogue d’applications d’organisation.** Si votre application est applicable à une organisation spécifique (ou si vous avez personnalisé votre application pour répondre aux besoins spécifiques d’une organisation), un administrateur de client peut charger votre application dans le catalogue d’applications de l’organisation. Cette option permet à tous les utilisateurs de l’organisation d’installer (mais ne les installe pas automatiquement).
  
* **Publier votre application sur l’App Store public.** Si votre application est destinée à tous les utilisateurs Teams où que vous soyez, vous pouvez envoyer votre application pour publication dans l’App Store public. Vous devez passer par un processus de révision rigoureux. vous devez donc vous assurer d'avoir mis les points sur les i et les croix sur les t.

Lorsque vous distribuez votre application, vous devez prendre en considération non seulement l’audience souhaitée, mais les stratégies informatiques de l’organisation avec lesquelles vous voulez partager votre application. Chaque organisation dispose d’un contrôle total sur la détermination des applications qui seront téléchargées dans leur catalogue d’applications d’organisation et des applications disponibles pour installation à partir de l’App Store.

### <a name="the-app-you-create-versus-the-app-your-users-install"></a>L’application que vous créez par rapport à l’application installée par vos utilisateurs

Votre application peut tirer parti de plusieurs points d’extensibilité dans le client teams et travailler dans diverses étendues. Le package d’application que vous distribuez aux utilisateurs définira tous ces éléments en tant qu’entité unique. Toutefois, étant donné que toutes les installations d’applications dans Microsoft teams sont *spécifiques au contexte*, l’intégralité de votre application ne peut pas toujours être installée pour tous les utilisateurs.

Par exemple, imaginez que votre application contient un bot de conversation qui fonctionne à la fois dans une conversation personnelle et une conversation d’équipe, ainsi qu’un onglet personnel et un onglet canal. Lorsque votre application est installée, elle est installée dans un contexte spécifique : si un utilisateur installe l’application dans une équipe, il n’a pas nécessairement installé la partie personnelle de votre application. Cela peut être un peu confus, n’oubliez pas de ne pas attendre que toutes les parties de votre application soient installées et configurées dans un contexte donné.

## <a name="getting-started-tutorials"></a>Didacticiels de mise en route

* [Créer une application de robot et d’onglet dans C #](~/tutorials/get-started-dotnet-app-studio.md)
* [Créer une application de robot et d’onglet en JavaScript/Node.js](~/tutorials/get-started-nodejs-app-studio.md)
* [Créer une application avec le générateur Yeoman](~/tutorials/get-started-yeoman.md)
