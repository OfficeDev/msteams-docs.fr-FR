---
title: Création d’une application pour Microsoft teams
author: clearab
description: Comprendre le processus standard de création d’une application pour Microsoft Teams.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 7c748829c481373dd7dfa011bfba4e7de3aba1bb
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673880"
---
# <a name="building-an-app-for-microsoft-teams"></a>Création d’une application pour Microsoft teams

La création et la distribution d’une application construite sur la plateforme Microsoft teams impliquent de décider ce qu’il faut créer, de créer des services Web, de créer un package d’application et de distribuer ce package à vos utilisateurs finaux cibles. Les administrateurs d’une organisation pourront décider qui peut accéder à votre application et l’installer, et il sera à vos utilisateurs d’installer votre application dans n’importe quel contexte particulier.

## <a name="design-a-great-app"></a>Concevoir une application intéressante

L’étape la plus importante dans la création d’une application réussie pour Microsoft teams consiste à choisir les points d’extension de combinaison corrects et les éléments d’interface utilisateur pour tirer parti de. Parfois, il s’agit d’une décision assez simple, mais pour les applications plus complexes, vous devriez consacrer beaucoup de temps à comprendre le problème que vous tentez de résoudre avec votre application et à mapper votre solution sur les différentes façons dont les utilisateurs peuvent interagir avec votre application dans Microsoft Client Teams. Ne sous-estimez pas l’importance du contexte et de l’étendue ! Un bot de conversation qui fonctionne très bien dans une conversation un-à-un peut ne pas fonctionner dans le cadre d’une conversation de groupe ou d’une conversation de canal.

1. Tout d’abord, [comprenez les points d’extensibilité du client teams et les éléments d’interface utilisateur](~/concepts/extensibility-points.md) disponibles pour votre application.

2. Ensuite, assurez-vous que vous [comprenez vos cas d’utilisation](~/concepts/design/understand-use-cases.md).

3. Enfin, [Mappez vos cas d’utilisation aux fonctionnalités de la plateforme teams](~/concepts/design/map-use-cases.md).

Une fois que vous avez décidé des points et des fonctionnalités d’extensibilité de votre application, vous devez réfléchir à chacune de ces interactions. En fonction de la conception de votre application, vous pouvez consulter les éléments suivants :

* [Création d’onglets intéressants](~/tabs/design/tabs.md)
* [Conception de robots de conversation utiles](~/bots/design/bots.md)

## <a name="prepare-your-environment"></a>Préparer votre environnement

Vous devez vous assurer que vous disposez d’un environnement dans lequel vous pouvez télécharger et tester votre application Teams. Si vous ne disposez pas déjà d’un abonnement O365 avec teams activé et de la possibilité de télécharger des applications, vous pouvez vous [inscrire au programme pour les développeurs o365](https://dev.office.com/devprogram) , qui vous donnera accès à un abonnement Office 365 gratuit à des fins de développement.

Pour plus d’informations, consultez [la rubrique prepare Your Office 365 Environment](~/concepts/build-and-test/prepare-your-o365-tenant.md) .

## <a name="build-and-test-your-app"></a>Créer et tester votre application

La création et le test de votre application pour Microsoft Teams ne sont pas très différentes de la création d’une autre application Web. La principale différence est la nécessité d’utiliser le manifeste de votre application dans votre package d’application pour connecter le client teams à vos services Web. Chaque fois que vous modifiez le manifeste de votre application, vous devez télécharger de nouveau votre package d’application, puis mettre à jour votre application dans teams en la réinstallant. Les modifications apportées à votre service Web ne nécessitent toutefois pas de réinstaller votre application dans le client Teams.

Lors de la création initiale de votre application, vous devez régulièrement mettre à jour les services Web et le package de votre application, généralement en téléchargeant et en installant l’application dans le client teams plusieurs fois (en particulier lors de la configuration initiale de votre application). Toutefois, à mesure que ce que vous créez se stabilise, la nécessité de modifier le manifeste de votre application diminue et vous devrez apporter des modifications à votre service Web.

### <a name="build-your-web-services"></a>Créer vos services Web

Une fois que vous avez décidé de la façon dont les utilisateurs vont interagir avec votre application, il est temps de créer les services Web pour les alimenter. En fonction de ce que vous créez, teams fournit différents kits de développement logiciel (SDK), modèles, exemples de code et générateurs pour vous aider à commencer, notamment :

* Kit de développement logiciel (SDK) de robot pour les [extensions de messagerie](~/messaging-extensions/what-are-messaging-extensions.md) et les [robots de conversation](~/bots/what-are-bots.md)
* Kit de développement logiciel Java client teams pour les [onglets](~/tabs/what-are-tabs.md) et autres pages de contenu
* [Générateur Yeoman](~/tutorials/get-started-yeoman.md) pour la création d’applications dans node. js
* **Aperçu** Un ensemble de contrôles Open source pour vos pages de contenu Web- [interface utilisateur Fluent](https://microsoft.github.io/fluent-ui-react/)
* [Modèles d’application](~/samples/app-templates.md) prêts pour la production
* Différents [exemples](~/samples/code-samples.md) pour vous aider à commencer

N’oubliez pas que vous devez héberger vos services Web de manière à ce qu’ils soient accessibles au public sur Internet (généralement dans un fournisseur de services Cloud comme Azure) et qui servent votre contenu via HTTPs.

### <a name="create-your-app-package"></a>Créer votre package d’application

Vous devrez également créer un package d’application qui peut être distribué et installé dans Microsoft Teams. Le package d’application contient deux icônes et un fichier manifeste JSON décrivant les métadonnées de votre application, les points d’extension que votre application utilise et des pointeurs vers les services qui alimentent ces points d’extension.

Lors de la création de votre package d’application, vous pouvez choisir de le créer manuellement ou d’utiliser app Studio, qui est une application à l’intérieur de teams qui vous aide à créer des applications Teams (connues, très Meta). App Studio vous guide tout au long de la création de votre manifeste d’application et peut vous aider à enregistrer votre robot à l’aide de l’infrastructure bot. Il contient également un concepteur de carte qui vous permet de créer visuellement des cartes et des actions de carte et d’envoyer des exemples à vous-même dans Teams.

## <a name="distributing-your-app"></a>Distribution de votre application

Vous disposez de trois options pour [distribuer votre application Microsoft teams](~/concepts/deploy-and-publish/apps-publish.md), en fonction de votre public cible.

* **Partagez directement votre package d’application.** Vous pouvez choisir de partager votre package d’application directement avec des utilisateurs. Ceci est particulièrement utile si votre application est dirigée vers un public limité (quelques équipes ou individus), et Pendant le développement et le test de votre application.
  
* **Publiez votre application sur le catalogue d’applications de votre organisation.** Si votre application est applicable à une organisation spécifique (ou si vous avez personnalisé votre application pour répondre aux besoins spécifiques d’une organisation), un administrateur de client peut charger votre application dans le catalogue d’applications de l’organisation. Cela rend votre application disponible pour tous les utilisateurs de l’Organisation pour installer (mais ne l’installe pas automatiquement).
  
* **Publiez votre application dans le magasin d’applications public.** Si votre application est destinée à tous les utilisateurs de teams, vous pouvez envoyer votre application en vue de sa publication dans le magasin d’applications public. Vous devez passer par un processus de révision rigoureux, vérifiez que vous avez pointé votre j’et franchir votre t.

Lors de la distribution de votre application, vous devez prendre en considération non seulement votre public, mais aussi les stratégies informatiques en place dans l’organisation avec laquelle vous souhaitez partager votre application. Chaque organisation dispose d’un contrôle total sur la détermination des applications à télécharger vers le catalogue d’applications de l’organisation, ainsi que sur les applications disponibles pour l’installation à partir de l’App Store.

### <a name="the-app-you-create-versus-the-app-your-users-install"></a>L’application que vous créez par rapport à l’application installée par vos utilisateurs

Votre application peut tirer parti de plusieurs points d’extensibilité dans le client teams et travailler dans diverses étendues. Le package d’application que vous distribuez aux utilisateurs définira tous ces éléments en tant qu’entité unique. Toutefois, étant donné que toutes les installations d’applications dans Microsoft teams sont *spécifiques au contexte*, l’intégralité de votre application ne peut pas toujours être installée pour tous les utilisateurs.

Par exemple, imaginez que votre application contient un bot de conversation qui fonctionne à la fois dans une conversation personnelle et une conversation d’équipe, ainsi qu’un onglet personnel et un onglet canal. Lorsque votre application est installée, elle est installée dans un contexte spécifique : si un utilisateur installe l’application dans une équipe, il n’a pas nécessairement installé la partie personnelle de votre application. Cela peut être un peu confus, n’oubliez pas de ne pas attendre que toutes les parties de votre application soient installées et configurées dans un contexte donné.

## <a name="get-started-quickly"></a>Prise en main rapide

Vous souhaitez commencer rapidement ? Consultez l’un de nos didacticiels de mise en route, ou un QuickStart pour une fonctionnalité de plateforme particulière (qui se trouve dans chaque section de fonctionnalité de la documentation).

Didacticiels de mise en route :

* [Créer une application de robot et d’onglet dans C #](~/tutorials/get-started-dotnet-app-studio.md)
* [Créer une application bot et TAB dans JavaScript/node. js](~/tutorials/get-started-nodejs-app-studio.md)
* [Créer une application avec le générateur Yeoman](~/tutorials/get-started-yeoman.md)
