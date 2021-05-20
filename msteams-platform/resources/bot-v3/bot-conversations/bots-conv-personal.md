---
title: Conversations 1 contre 1 avec des bots
description: Décrit le scénario de bout en bout d’avoir une conversation en 1 contre 1 avec un bot dans Microsoft Teams
keywords: scénarios équipes 1on1 1to1 conversation bot
localization_priority: Normal
ms.topic: conceptual
ms.date: 05/20/2019
ms.openlocfilehash: dff65e919485eff0443032995b934b7ae93c64eb
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566501"
---
# <a name="have-a-personal-one-on-one-conversation-with-a-microsoft-teams-bot"></a>Avoir une conversation personnelle (en face-à-face) avec un bot Microsoft Teams vie

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Teams permet aux utilisateurs de s’engager dans des conversations directes avec des bots construits [sur Microsoft Bot Framework](/azure/bot-service/?view=azure-bot-service-3.0&preserve-view=true). Les utilisateurs peuvent trouver des bots dans la galerie Discover Apps et les ajouter à leur expérience Teams pour des conversations personnelles. Les propriétaires d’équipe et les utilisateurs avec les autorisations appropriées peuvent également ajouter des bots en tant que membres de l’équipe. Pour plus d’informations, [voir Interact dans un canal d’équipe),](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)qui non seulement les rend disponibles dans les canaux de cette équipe, mais aussi pour le chat personnel pour tous ces utilisateurs.

Chat personnel diffère de chat dans les canaux en ce que l’utilisateur n’a pas besoin @mention le bot. Si un bot est utilisé dans plusieurs contextes tels que personnel, groupChat ou canal, vous devez détecter si le bot est dans un chat de groupe ou un canal, et traiter les messages un peu différemment. Pour plus d’informations, voir [Interact dans un canal d’équipe ou un chat de groupe](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).

## <a name="designing-a-great-personal-bot"></a>Concevoir un grand bot personnel

Un grand bot dans la Microsoft Teams les utilisateurs à obtenir les informations dont ils ont besoin, le tout dans le contexte de l’expérience Teams’utilisateur. Les conversations personnelles avec un bot sont des échanges privés entre un bot et son utilisateur; ils sont un excellent moyen de fournir des informations spécifiques et pertinentes pour cet utilisateur dans le contexte personnel. Un bot dans le chat personnel est vraiment un dialogue entre votre service et l’individu, où un bot dans un chat de groupe ou une chaîne diffuse tout à un groupe de personnes.

Selon l’expérience que vous souhaitez créer, le bot peut avoir besoin de travailler dans plusieurs étendues - personnel, groupchat, et l’équipe. Le travail de soutien à plus d’une portée est minime. Il n’y a aucune attente en Teams que votre fonction bot dans toutes les étendues, mais vous devez vous assurer que votre bot a du sens et fournit la valeur de l’utilisateur dans n’importe quelle portée (s) que vous choisissez de prendre en charge.

## <a name="best-practice-welcome-messages-in-personal-conversations"></a>Meilleures pratiques : Messages de bienvenue dans les conversations personnelles

Votre bot doit [envoyer un](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) message de bienvenue à un chat personnel la première fois (et seulement la première fois) un utilisateur lance une conversation personnelle avec votre bot. Cette recommandation ne s’applique pas aux contacts pour la première fois dans un canal.
