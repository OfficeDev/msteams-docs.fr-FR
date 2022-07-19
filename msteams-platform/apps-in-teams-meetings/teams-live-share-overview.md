---
title: Vue d’ensemble Live Share
author: surbhigupta
description: Dans ce module, découvrez ce qu’est le Kit de développement logiciel (SDK) Microsoft Live Share et ses scénarios utilisateur.
ms.topic: overview
ms.localizationpriority: high
ms.author: v-ypalikila
ms.date: 04/07/2022
ms.openlocfilehash: 80d28acd5616fea371f3cd84354412504815ff87
ms.sourcegitcommit: 79d525c0be309200e930cdd942bc2c753d0b718c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/19/2022
ms.locfileid: "66841861"
---
---

# <a name="live-share-sdk"></a>FAQ sur le Kit de développement logiciel (SDK) de Live Share

> [!Note]
> Le SDK de Live Share est actuellement disponible uniquement en [préversion publique du développeur](../resources/dev-preview/developer-preview-intro.md). Vous devez faire partie de la préversion publique du développeur pour Microsoft Teams utiliser le kit de développement logiciel (SDK) de Live Share.

Live Share est un Kit de développement logiciel (SDK) conçu pour transformer Teams applications en expériences multi-utilisateurs collaboratives sans écrire de code principal dédié. Le Kit de développement logiciel (SDK) Live Share intègre en toute transparence les réunions à [Infrastructure Fluid](https://fluidframework.com/). Infrastructure Fluid est une collection de bibliothèques clientes permettant de distribuer et de synchroniser l’état partagé. Live Share fournit un relais [Azure Fluid](/azure/azure-fluid-relay/) gratuit, entièrement managé et prêt à l’emploi, soutenu par la sécurité et l’échelle mondiale de Teams.

> [!div class="nextstepaction"]
> [Prise en main](teams-live-share-quick-start.md)

Le SDK Live Share fournit une `TeamsFluidClient` classe pour la connexion à un conteneur Fluid spécial associé à chaque réunion en quelques lignes de code. Outre les structures de données fournies par Infrastructure Fluid, Live Share prend également en charge un nouvel ensemble de classes de structures de données distribuées (DDS) afin de simplifier la création d'applications pour les scénarios de réunion courants, tels que la lecture de médias partagés.

:::image type="content" source="../assets/images/teams-live-share/teams-live-share-contoso-video.gif" alt-text="Expérience de partage de vidéos Live Share":::

## <a name="why-build-apps-using-the-live-share-sdk"></a>Pourquoi créer des applications à l’aide du SDK Live Share?

La création d’applications collaboratives peut être difficile, fastidieuse, coûteuse et comprend des exigences de conformité complexes à grande échelle. Les utilisateurs de Teams passent beaucoup de temps à revoir leur travail avec leurs coéquipiers, à regarder des vidéos ensemble et à réfléchir à de nouvelles idées grâce au partage d'écran. Le SDK Live Share vous permet de transformer votre application en quelque chose de plus collaboratif avec un investissement minimal.

Voici quelques-uns des principaux avantages du SDK Live Share :

* Gestion et sécurité des sessions sans souci.
* Structures de données distribuées avec état et sans état.
* Extensions multimédias pour synchroniser facilement la vidéo et l’audio.
* Respecter les privilèges de réunion à l’aide de la vérification de rôle.
* Service gratuit et entièrement managé avec une faible latence.
* Injection intelligente de l'audio.

:::image type="content" source="../assets/images/teams-live-share/Teams-live-share-schematics.png" alt-text="Live Share Teams":::

## <a name="user-scenarios"></a>Scénarios utilisateur

|Scénario|Exemple|
| :------- | :--------------------- |
| Les utilisateurs et leurs collègues ont prévu une réunion pour présenter un premier montage d'une vidéo de marketing lors d'une prochaine revue de direction et veulent mettre en évidence des sections spécifiques pour obtenir des commentaires. | Les utilisateurs partagent la vidéo vers la phase de réunion et démarrent la vidéo. Si nécessaire, l’utilisateur suspend la vidéo pour discuter de la scène. Les utilisateurs peuvent dessiner à tour de rôle des parties de l’écran pour mettre en évidence les points clés.|
| Vous êtes responsable de projet pour une équipe agile qui joue à Agile Poker avec votre équipe afin d’estimer la quantité de travail nécessaire pour un sprint à venir.| Vous partagez une application de planification Agile Poker à la phase de réunion qui utilise le SDK Live Share et jouez au jeu de planification jusqu’à ce que l’équipe atteigne un consensus.|

> [!IMPORTANT]
> Toutes les données envoyées ou stockées via le service Azure Fluid Relay hébergé du SDK Live Share sont accessibles pendant 24 heures. Si vous souhaitez en savoir plus, veuillez consulter la rubrique [FAQ sur Live Share](teams-live-share-faq.md).

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Prise en main](teams-live-share-quick-start.md)

## <a name="see-also"></a>Voir aussi

* [Référentiel GitHub](https://github.com/microsoft/live-share-sdk)
* [ Documents de référence du kit SDK Live Share](/javascript/api/@microsoft/live-share/)
* [Documents de référence du Kit de développement logiciel (SDK) Live Share Media](/javascript/api/@microsoft/live-share-media/)
* [Fonctionnalités de Live Share](teams-live-share-capabilities.md)
* [Fonctionnalités média de Live Share](teams-live-share-media-capabilities.md)
* [FAQ sur Live Share](teams-live-share-faq.md)
* [Applications Teams dans les réunions](teams-apps-in-meetings.md)
