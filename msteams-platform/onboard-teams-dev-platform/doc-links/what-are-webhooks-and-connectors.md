---
title: Qu’est-ce qu’un webhooks et un connecteur ?
author: clearab
description: Découvrez comment les webhooks et les connecteurs peuvent connecter vos services Web au client Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 740806e43af94d5a5da876affec2070a5a461b11
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/12/2020
ms.locfileid: "46651937"
---
# <a name="what-are-webhooks-and-connectors"></a>Qu’est-ce qu’un webhooks et un connecteur ?

Les webhooks et les connecteurs sont des méthodes simples pour connecter des systèmes et des services externes avec des canaux et des conversations Microsoft Teams.

Les utilisateurs peuvent, par exemple, s’abonner à des notifications à partir d’une autre application (généralement sous la forme de cartes).

## <a name="incoming-webhooks"></a>Webhooks entrants

Les webhooks entrants constituent le type de connecteur le plus simple, ainsi qu’un moyen rapide et simple de connecter le canal d’une équipe à un service externe. Pour n’importe quel canal (s’il est activé pour cette équipe), vous pouvez exposer un point de terminaison HTTPs qui accepte le format JSON correctement mis en forme et insérer des messages dans le canal.

Consultez la rubrique [créer un webhook entrant](~/webhooks-and-connectors/how-to/add-incoming-webhook.md).

### <a name="user-scenarios"></a>Scénarios utilisateur

Les webhooks entrants conviennent mieux aux scénarios spécifiques à une équipe particulière. Par exemple, vous pouvez créer un webhook entrant dans votre canal DevOps et configurer vos services de génération, de déploiement et de surveillance pour envoyer des alertes.

## <a name="office-365-connectors"></a>Connecteurs Office 365

Un connecteur Office 365 vous permet de créer une page de configuration personnalisée pour le webhook entrant et de l’empaqueter dans le cadre d’une application Teams. Vous pouvez ensuite distribuer cette application plus largement ou même dans notre magasin d’applications. Vous envoyez des messages principalement à l’aide de cartes de connecteur Office 365 qui peuvent également disposer d’un ensemble limité d’actions de carte. Ils sont configurés au niveau du canal mais installés au niveau de l’équipe.

Voir [Create an Office 365 Connector](~/webhooks-and-connectors/how-to/connectors-creating.md).

### <a name="user-scenarios"></a>Scénarios utilisateur

Un connecteur météo qui vous permet de choisir un emplacement et une heure de réception des mises à jour de la prévision de demain.

## <a name="outgoing-webhooks"></a>Webhooks sortants

Les webhooks sortants permettent à vos utilisateurs d’envoyer des messages texte d’un canal vers vos services web. Une fois configurés, les utilisateurs peuvent @mention votre application et envoyer un message à votre service externe. Votre service dispose de cinq secondes pour envoyer une réponse au message, contenant potentiellement du texte ou une carte.

Les webhooks sortants sont configurés en fonction de chaque équipe et ne peuvent pas être inclus dans une application teams normale.

Consultez la rubrique [créer un webhook sortant](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md).

### <a name="user-scenarios"></a>Scénarios utilisateur

Les webhooks sortants conviennent mieux à la réalisation de flux de travail spécifiques à une équipe qui ne nécessitent pas de collecter ou d’échanger de grandes quantités d’informations.

## <a name="learn-more"></a>En savoir plus

* [Planification de votre application](../../concepts/extensibility-points.md)
* [Création de votre application](../../concepts/building-an-app.md)
* [Publication de votre application](../../concepts/deploy-and-publish/overview.md)
