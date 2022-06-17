---
title: Conversations en tête-à-tête avec des bots
description: Dans ce module, découvrez le scénario de bout en bout d’une conversation en face à face avec un bot dans Microsoft Teams
ms.localizationpriority: medium
ms.topic: conceptual
ms.date: 05/20/2019
ms.openlocfilehash: e973e335558a54187a11d5146b52c5774d3cf758
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2022
ms.locfileid: "66144326"
---
# <a name="have-a-personal-one-on-one-conversation-with-a-microsoft-teams-bot"></a>Avoir une conversation personnelle (en tête-à-tête) avec un bot Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Teams permet aux utilisateurs d’engager des conversations directes avec des bots basés sur [Microsoft Bot Framework](/azure/bot-service/?view=azure-bot-service-3.0&preserve-view=true). Les utilisateurs peuvent trouver des bots dans la galerie Discover Apps et les ajouter à leur expérience Teams pour des conversations personnelles. Les propriétaires d’équipe et les utilisateurs disposant des autorisations appropriées peuvent également ajouter des bots en tant que membres de l’équipe. Pour plus d’informations, consultez [Interagir dans un canal d’équipe](~/resources/bot-v3/bot-conversations/bots-conv-channel.md), qui les rend non seulement disponibles dans les canaux de cette équipe, mais également pour les utilisateurs de conversation personnelle.

La conversation personnelle diffère de la conversation dans les canaux en ce que l’utilisateur n’a pas besoin de @mentionner le bot. Si un bot est utilisé dans plusieurs contextes, comme dans les étendues suivantes :
* Personnel
* Conversation de groupe.
* Canal

Vous devez détecter si le bot se trouve dans une conversation de groupe ou un canal, et traiter les messages un peu différemment. Pour plus d’informations, consultez [Interagir dans un canal d’équipe ou une conversation de groupe](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).

## <a name="designing-a-great-personal-bot"></a>Conception d’un bot personnel de qualité

Un excellent bot dans Microsoft Teams permet aux utilisateurs d’obtenir les informations dont ils ont besoin, le tout dans le contexte de l’expérience Teams. Les conversations personnelles avec un bot sont des échanges privés entre un bot et son utilisateur ; ils constituent un excellent moyen de fournir des informations spécifiques et pertinentes à cet utilisateur dans le contexte personnel. Un bot dans une conversation personnelle est une boîte de dialogue entre votre service et l’individu, où un bot dans une conversation de groupe ou un canal diffuse tout à un groupe de personnes.

Selon l’expérience que vous souhaitez créer, le bot peut avoir besoin de travailler dans plusieurs étendues : personnel, conversation de groupe et équipe. Le travail de prise en charge de plusieurs étendues est minimal. Dans Teams, rien ne requiert que votre bot fonctionne dans toutes les étendues, mais vous devez vous assurer que votre bot est cohérent et qu’il apporte une valeur ajoutée aux utilisateurs dans les étendues que vous choisissez de prendre en charge.

## <a name="best-practice-welcome-messages-in-personal-conversations"></a>Bonne pratique : messages d’accueil dans les conversations personnelles

Votre bot doit [envoyer de manière proactive](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) un message de bienvenue à une conversation personnelle la première fois (et seulement la première fois) qu’un utilisateur lance une conversation personnelle avec votre bot. Cette recommandation ne s'applique pas aux premiers contacts dans un canal.
