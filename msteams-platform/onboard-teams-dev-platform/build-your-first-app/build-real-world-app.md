---
title: Création de votre première application teams
author: heath-hamilton
description: Didacticiel pour la création d’une application Microsoft teams réelle
ms.openlocfilehash: 4915dde4ef5a852f4fc5d1e4c83e3349db2eaf6b
ms.sourcegitcommit: 80bf79a952bb14cbc38c0bd1e3cf8a346158e28e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/13/2020
ms.locfileid: "46655673"
---
# <a name="learn-how-to-build-your-first-teams-app"></a>Découvrez comment créer votre première application teams

Dans **créer votre première application**, vous découvrez comment créer une application teams de base par le biais de didacticiels. Les leçons sont générées les unes sur les autres, tout au long de chaque étape de la création d’une application de teams simple et réelle. Nous vous présenterons des outils courants, des concepts fondamentaux et des liens utiles.

Vous commencerez par créer et exécuter un « Hello, World ! ». application d’onglets. Vous allez ensuite créer une interface utilisateur simple et découvrir comment obtenir un contexte utile avec le kit de développement logiciel (SDK) JavaScript de Microsoft Teams.

## <a name="what-youll-learn"></a>Ce que vous allez apprendre

> [!div class="checklist"]
  >
  > - **Soyez rapidement opérationnel avec Team Toolkit**: Microsoft teams Toolkit for Visual Studio code s’occupe de la création de votre projet d’application et de votre génération de modèles automatique afin que vous puissiez utiliser une application en cours d’exécution en quelques minutes.
  > - **Définissez votre application avec le manifeste**: le manifeste est un plan qui vous permet de spécifier les capacités et les services utilisés par votre application Teams.
  > - **Portée de votre audience**: vous pouvez créer une application de teams pour une collaboration ou une utilisation personnelle. Dans les didacticiels, vous apprendrez à créer un onglet pour des utilisateurs individuels ou un groupe de personnes dans un canal ou une conversation.
  > - **Utiliser le kit de développement logiciel teams pour obtenir le contexte**: Découvrez comment utiliser le kit de développement logiciel (SDK) Microsoft teams JavaScript pour effectuer des modifications de thème ou configurer l’expérience de configuration  
  > - **Développez votre application**: tout au long des didacticiels, nous allons nous attacher à des rubriques connexes susceptibles de vous intéresser (certaines incluent des instructions relatives à l’authentification et à la conception).

## <a name="teams-app-fundamentals"></a>Principes fondamentaux des applications teams

Avant de commencer les didacticiels, vous devez connaître les points suivants relatifs à la création d’applications pour Teams.

### <a name="apps-can-have-multiple-capabilities"></a>Les applications peuvent avoir plusieurs fonctionnalités

Les applications teams se composent d’une ou de plusieurs [fonctionnalités de plateforme](../capabilities-overview.md), notamment des [onglets](../doc-links/what-are-tabs.md), des [robots](../doc-links/what-are-bots.md ), des [extensions de messagerie](../doc-links/what-are-messaging-extensions.md), des [webhooks et des connecteurs](../doc-links/what-are-webhooks-and-connectors.md). Les applications teams ont également de nombreuses [conventions et éléments d’interface utilisateur](../doc-links/teams-ui-conventions.md), tels que des cartes, des modules de tâches et des liens détaillés, que vous pouvez utiliser pour créer la meilleure expérience utilisateur possible.

Pour ces didacticiels, vous allez créer uniquement des onglets, mais vous pouvez ajouter un bot ou d’autres fonctionnalités à votre application comme vous le souhaitez.

### <a name="teams-doesnt-host-your-app"></a>Teams n’héberge pas votre application  

Une application teams se compose de trois éléments principaux :

1. Le client Microsoft Teams (Web, de bureau ou mobile) où les utilisateurs interagissent avec votre application.
1. Votre application, service, flux de travail ou site Web qui effectue la logique, le stockage des données et les appels d’API nécessaires pour alimenter votre application.
1. Votre package d’application, que vous utilisez pour installer l’application dans Teams. Il contient des métadonnées d’application (nom, icônes, etc.) et des pointeurs vers vos services.

## <a name="next-step"></a>Étape suivante

C’est tout pour l’instant, commençons !

> [!div class="nextstepaction"]
> [Créer et exécuter votre première application](build-and-run-with-toolkit.md)
