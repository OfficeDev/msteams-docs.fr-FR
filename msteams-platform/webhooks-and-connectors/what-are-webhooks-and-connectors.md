---
title: Que sont les webhooks et les connecteurs ?
author: surbhigupta
description: Comprendre comment les webhooks et les connecteurs peuvent connecter vos services web au client Teams web.
localization_priority: Normal
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 3e8105c9f069428bf93fb9bc2533895878f5ded1
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069040"
---
# <a name="what-are-webhooks-and-connectors"></a>Que sont les webhooks et les connecteurs ?

Les webhooks et connecteurs constituent un moyen simple pour connecter vos services web à des canaux et équipes au sein de Microsoft Teams. 

## <a name="outgoing-webhooks"></a>Webhooks sortants

Les webhooks sortants permettent à vos utilisateurs d’envoyer des messages texte d’un canal vers vos services web. Une fois configuré, vos utilisateurs pourront @mention votre webhook sortant et envoyer un message à votre service. Votre service aura cinq secondes pour envoyer une réponse au message, contenant potentiellement du texte ou une carte.

Les webhooks sortants sont configurés par équipe et ne peuvent pas être inclus dans le cadre d’une application Teams normale. Ils conviennent mieux pour effectuer des charges de travail spécifiques à l’équipe qui ne nécessitent pas de grandes quantités d’informations à collecter ou à échanger.

Pour plus d’informations, [voir Créer un webhook sortant.](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)

## <a name="connectors"></a>Connecteurs

Les connecteurs permettent aux utilisateurs de s’abonner pour recevoir les notifications et les messages de vos services web. Ils exposent un point de terminaison HTTPS pour que votre service publie des messages, généralement sous forme de cartes.

### <a name="incoming-webhooks"></a>Webhooks entrants

Les webhooks entrants sont le type de connecteur le plus simple. Pour n’importe quel canal d’équipe (s’ils sont activés pour cette équipe), vous pouvez choisir d’exposer un point de terminaison HTTPS qui acceptera le format JSON correct et insérera des messages dans ce canal. Ils sont un moyen rapide et facile de connecter un canal à votre service et sont mieux utilisés pour les scénarios propres à une équipe particulière. Par exemple, vous pouvez créer un webhook entrant dans votre canal DevOps et configurer votre build, votre déploiement et vos services de surveillance pour envoyer des alertes.

Pour plus d’informations, [voir Créer un webhook entrant.](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)

### <a name="office-365-connectors"></a>Connecteurs Office 365

Office 365 Les connecteurs vous permettent de créer une page de configuration personnalisée pour votre webhook entrant et de les créer un package dans le cadre d’Teams app. Vous pouvez ensuite distribuer cette application plus largement, voire vers notre App Store. Vous envoyez des messages principalement à l’aide Office 365 cartes connecteur et vous avez la possibilité d’y ajouter un ensemble limité d’actions de carte. Un bon exemple de ce connecteur est un connecteur météo qui permet aux utilisateurs de choisir un emplacement et une heure de la journée pour recevoir des mises à jour sur la météo de demain. Ils sont configurés au niveau du canal, mais sont installés au niveau de l’équipe.

Pour plus d’informations, [voir Create an Office 365 Connector](~/webhooks-and-connectors/how-to/connectors-creating.md).
