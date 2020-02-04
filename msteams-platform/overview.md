---
title: Plateforme pour les développeurs de Microsoft Teams
author: clearab
description: Page de présentation décrivant la plateforme de développement Microsoft teams et comment commencer à créer des applications pour Microsoft Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: cb9d91f2de29bac00f4cdcd9672adf9d7d4ee734
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674034"
---
# <a name="what-are-microsoft-teams-apps"></a>Qu’est-ce que les applications Microsoft teams ?

Microsoft teams est un espace de travail de collaboration dans Office 365 qui s’intègre aux applications et services que les personnes utilisent pour effectuer des tâches. La plateforme de développement Microsoft teams permet aux développeurs d’intégrer facilement leurs propres applications et services pour améliorer la productivité, prendre des décisions plus rapidement, fournir le focus (en réduisant le changement de contexte) et créer une collaboration sur le contenu existant et travail. Les applications créées sur la plateforme Microsoft teams sont des ponts entre le client teams et vos services et flux de travail ; les plaçant directement dans le contexte de votre plateforme de collaboration ;

## <a name="what-can-teams-apps-do"></a>Que peuvent faire les applications teams ?

Les applications créées sur la plateforme Microsoft teams se concentrent principalement sur la collaboration croissante et l’amélioration de la productivité. Votre application peut être une solution simple, par exemple, publier des notifications à partir d’autres systèmes ou des applications complexes à plusieurs facettes. N’oubliez pas que teams est une plateforme de collaboration sociale ; les meilleures applications s’emploient à aider les utilisateurs à s’exprimer et à collaborer efficacement.

* **Collaborer sur des éléments dans des systèmes externes.** L’un des principaux scénarios pour une application teams personnalisée est d’apporter des informations ou des éléments à teams à partir d’un autre endroit et de faire une conversation. Vous pouvez diffuser des informations dans Teams, permettre à vos utilisateurs de les Rechercher et de les extraire à la demande, ou de les rendre disponibles dans une vue Web incorporée.

* **Déclenchez des flux de travail à partir de conversations.** Les conversations entraînent souvent la nécessité de lancer un flux de travail ou de terminer une action ; Prenez note de ce sujet, passez en revue ma demande de tirage, convertissez-la en prospectus de ventes, etc. Votre application teams peut accéder à ce flux de travail directement à l’intérieur de teams.

* **Informer votre équipe des événements importants.** Maladie des notifications par courrier électronique ? Envoyez des notifications à teams à la place. Envoyer des notifications directement aux utilisateurs, à un canal, au flux d’activité, ou à quiconque s’y abonner.

* **Incorporer les fonctionnalités d’autres sites/services.** Parfois, il vous suffit de rendre votre application plus facile à découvrir. Incorporez votre application à page unique existante ou créez des éléments à partir de rien pour Teams.

## <a name="how-do-teams-apps-work"></a>Comment fonctionnent les applications teams ?

La première chose à savoir sur les applications personnalisées pour Microsoft Teams (autres que leur incroyable) est que teams n’est pas un service d’hébergement. Votre package d’application contient des métadonnées sur votre application (nom, icônes, etc.) et des pointeurs vers les services Web que vous hébergez qui alimentent votre application. Microsoft teams fournit le mécanisme de distribution, les structures de l’interface utilisateur/UX pour vous permettre de tirer parti de, et les API que vous pouvez utiliser pour augmenter les informations et les actions disponibles pour votre application.

Une application teams se compose de trois éléments principaux :

* **Le client Microsoft Teams (Web, de bureau ou mobile)** où les utilisateurs vont interagir avec votre application.
* **Votre package d’application de teams** qui crée l’application installée par vos utilisateurs, et contient les métadonnées et pointeurs de votre application vers vos services.
* **Votre service, flux de travail ou site Web** qui effectue la logique nécessaire, le stockage des données et les appels d’API pour alimenter votre application.

Il est important de garder à l’esprit que toute fonctionnalité que vous exposez dans une application Microsoft teams est publiquement disponible sur Internet, sauf si vous effectuez des étapes supplémentaires pour la sécuriser. Si vous fournissez un accès à des informations confidentielles ou protégées, vous devez vous assurer que vos services authentifient au minimum le point de terminaison qui se connecte à votre application ou [authentifient vos utilisateurs](~/concepts/authentication/authentication.md).

## <a name="how-can-you-share-your-teams-app"></a>Comment pouvez-vous partager votre application teams ?

Lorsque vous êtes prêt à partager vos applications Microsoft Teams, vous disposez de trois options en fonction de vos audiences ciblées.

* **[Télécharger directement votre application](~/concepts/deploy-and-publish/apps-upload.md)** Si votre application doit uniquement être partagée par votre équipe ou quelques personnes de votre organisation, vous pouvez partager votre package d’application et le charger directement.
* **[Publier dans le catalogue d’applications de votre organisation](~/concepts/deploy-and-publish/apps-publish.md)** Vous pouvez partager votre application avec l’ensemble de votre organisation via votre catalogue d’applications.
* **[Publier dans le magasin d’applications public](~/concepts/deploy-and-publish/apps-publish.md)** Si votre application est pour tout le monde, vous pouvez la publier dans notre magasin d’applications public. En fonction de vos objectifs, vous pouvez bénéficier de l’assistance marketing et commerciale.

## <a name="get-started"></a>Prise en main

* [Créer une application de robot et d’onglet dans C #](~/tutorials/get-started-dotnet-app-studio.md)
* [Créer une application bot et TAB dans JavaScript/node. js](~/tutorials/get-started-nodejs-app-studio.md)

## <a name="learn-more"></a>En savoir plus

* [Points d’extensibilité dans le client teams](~/concepts/extensibility-points.md)
* [Création d’applications pour teams](~/concepts/building-an-app.md)
