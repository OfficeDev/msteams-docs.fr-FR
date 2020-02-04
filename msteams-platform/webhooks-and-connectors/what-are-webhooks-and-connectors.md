---
title: Qu’est-ce qu’un webhooks et un connecteur ?
author: clearab
description: Découvrez comment les webhooks et les connecteurs peuvent connecter vos services Web au client Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 2be6f82bba0efe05a22a8da9da0acc1e0ad6fa00
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673528"
---
# <a name="what-are-webhooks-and-connectors"></a>Qu’est-ce qu’un webhooks et un connecteur ?

Les webhooks et les connecteurs sont un moyen simple de connecter vos services Web à des canaux et à des équipes internes à Microsoft Teams. 

## <a name="outgoing-webhooks"></a>Webhooks sortants

Les webhooks sortants permettent à vos utilisateurs d’envoyer des messages texte à partir d’un canal vers vos services Web. Une fois configurés, vos utilisateurs pourront @mention votre webhook sortant et envoyer un message à votre service. Votre service disposera de cinq secondes pour envoyer une réponse au message, contenant éventuellement du texte ou une carte.

Les webhooks sortants sont configurés au niveau de chaque équipe, et ne peuvent pas être inclus dans une application teams normale. Elles conviennent mieux à la réalisation de charges de travail spécifiques à l’équipe qui ne nécessitent pas de grandes quantités d’informations à collecter ou à échanger.

Consultez la rubrique [créer un webhook sortant](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md).

## <a name="connectors"></a>Connecteurs

Les connecteurs permettent aux utilisateurs de s’abonner pour recevoir des notifications et des messages de vos services Web. Ils exposent un point de terminaison HTTPs pour votre service pour publier des messages, généralement sous la forme de cartes.

### <a name="incoming-webhooks"></a>Webhooks entrants

Les webhooks entrants constituent le type de connecteur le plus simple. Pour n’importe quel canal dans l’équipe (s’ils sont activés pour cette équipe), vous pouvez choisir d’exposer un point de terminaison HTTPs qui accepte le format JSON correctement mis en forme et d’insérer des messages dans ce canal. Il s’agit d’un moyen simple et rapide de connecter un canal à votre service, et est recommandé pour les scénarios propres à une équipe particulière. Par exemple, vous pouvez créer un webhook entrant dans votre canal DevOps et configurer vos services de génération, de déploiement et de surveillance pour envoyer des alertes.

Consultez la rubrique [créer un webhook entrant](~/webhooks-and-connectors/how-to/add-incoming-webhook.md).

### <a name="office-365-connectors"></a>Connecteurs Office 365

Les connecteurs Office 365 vous permettent de créer une page de configuration personnalisée pour votre webhook entrant et de les empaqueter dans le cadre d’une application Teams. Vous pouvez ensuite distribuer cette application plus globalement ou même dans notre magasin d’applications. Vous envoyez des messages principalement à l’aide de cartes de connecteur Office 365 et vous avez également la possibilité d’y ajouter un ensemble limité d’actions de carte. Un connecteur météorologique qui permet aux utilisateurs de choisir un emplacement et une heure de réception des mises à jour pour la météo de demain est un parfait exemple. Ils sont configurés au niveau du canal, mais sont installés au niveau de l’équipe.

Voir [Create an Office 365 Connector](~/webhooks-and-connectors/how-to/connectors-creating.md).