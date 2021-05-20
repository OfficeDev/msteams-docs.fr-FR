---
title: Qu’est-ce que les webhooks et les connecteurs ?
author: clearab
description: Comprenez comment les webhooks et les connecteurs peuvent connecter vos services Web à l’Teams client.
localization_priority: Normal
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: e36b73c0eaed5068311dae6c1ef8fdc073432334
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566802"
---
# <a name="what-are-webhooks-and-connectors"></a>Qu’est-ce que les webhooks et les connecteurs ?

Les webhooks et connecteurs constituent un moyen simple pour connecter vos services web à des canaux et équipes au sein de Microsoft Teams. 

## <a name="outgoing-webhooks"></a>Webhooks sortants

Les webhooks sortants permettent à vos utilisateurs d’envoyer des messages texte d’un canal vers vos services web. Une fois configurés, vos utilisateurs seront en mesure @mention votre webhook sortant et envoyer un message à votre service. Votre service aura cinq secondes pour envoyer une réponse au message, contenant potentiellement du texte ou une carte.

Les webhooks sortants sont configurés par équipe, ne peuvent pas être inclus dans une application Teams normale. Ils sont les mieux adaptés pour remplir des charges de travail spécifiques à l’équipe qui ne nécessitent pas de grandes quantités d’informations à recueillir ou à échanger.

Pour plus d’informations, [voir Créer un webhook sortant](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md).

## <a name="connectors"></a>Connecteurs

Les connecteurs permettent aux utilisateurs de s’abonner pour recevoir les notifications et les messages de vos services web. Ils exposent un point de terminaison HTTPS pour votre service à poster des messages à - généralement sous la forme de cartes.

### <a name="incoming-webhooks"></a>Webhooks entrants

Les webhooks entrants sont le type de connecteur le plus simple. Pour n’importe quel canal de l’équipe (s’ils sont activés pour cette équipe), vous pouvez choisir d’exposer un point de terminaison HTTPS qui acceptera JSON correctement formaté et insérera des messages dans ce canal. Ils sont un moyen rapide et facile de connecter un canal à votre service, et sont mieux utilisés pour des scénarios qui sont uniques à une équipe particulière. Par exemple, vous pouvez créer un webhook entrant dans votre canal DevOps et configurer vos services de build, de déploiement et de surveillance pour envoyer des alertes.

Pour plus d’informations, [voir Créer un webhook entrant](~/webhooks-and-connectors/how-to/add-incoming-webhook.md).

### <a name="office-365-connectors"></a>Connecteurs Office 365

Office 365 Les connecteurs vous permettent de créer une page de configuration personnalisée pour votre webhook entrant et de les emballer dans le cadre d’une application Teams’argent. Vous pouvez ensuite distribuer cette application plus largement, ou même à notre App Store. Vous envoyez des messages principalement à l Office 365 des cartes Connector, et avez la possibilité d’y ajouter un ensemble limité d’actions de carte. Un bon exemple de ceci est un connecteur météo qui permet aux utilisateurs de choisir un emplacement et l’heure de la journée pour recevoir des mises à jour sur la météo de demain. Ils sont configurés au niveau du canal, mais sont installés au niveau de l’équipe.

Pour plus d’informations, [voir Créer un connecteur Office 365'environnement](~/webhooks-and-connectors/how-to/connectors-creating.md).
