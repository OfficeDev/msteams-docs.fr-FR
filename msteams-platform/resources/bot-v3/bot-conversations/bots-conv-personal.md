---
title: Conversations 1-sur-1 avec des bots
description: Décrit le scénario de bout en bout d’une conversation 1-on-1 avec un bot dans Microsoft Teams
keywords: scénarios teams 1on1 1to1 bot de conversation
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
# <a name="have-a-personal-one-on-one-conversation-with-a-microsoft-teams-bot"></a>Avoir une conversation personnelle (un-à-un) avec un Microsoft Teams bot

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Teams permet aux utilisateurs de s’engager dans des conversations directes avec des bots intégrés au [Microsoft Bot Framework](/azure/bot-service/?view=azure-bot-service-3.0&preserve-view=true). Les utilisateurs peuvent trouver des bots dans la galerie Découvrir les applications et les ajouter à leur expérience Teams pour les conversations personnelles. Les propriétaires d’équipe et les utilisateurs ayant les autorisations appropriées peuvent également ajouter des bots en tant que membres de l’équipe. Pour plus d’informations, voir [Interagir](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)dans un canal d’équipe ), qui les rend non seulement disponibles dans les canaux de cette équipe, mais également pour la conversation personnelle pour tous ces utilisateurs.

La conversation personnelle diffère de la conversation dans les canaux en ce que l’utilisateur n’a pas besoin @mention le bot. Si un bot est utilisé dans plusieurs contextes tels que personnel, groupChat ou canal, vous devez détecter si le bot se trouve dans une conversation ou un canal de groupe, et traiter les messages un peu différemment. Pour plus d’informations, voir [Interagir dans un canal d’équipe ou une conversation de groupe.](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)

## <a name="designing-a-great-personal-bot"></a>Conception d’un bot personnel idéal

Un bot de qualité dans Microsoft Teams permet aux utilisateurs d’obtenir les informations dont ils ont besoin, dans le contexte de l Teams expérience utilisateur. Les conversations personnelles avec un bot sont des échanges privés entre un bot et son utilisateur . Ils sont un excellent moyen de fournir des informations spécifiques et pertinentes pour cet utilisateur dans le contexte personnel. Un bot dans une conversation personnelle est vraiment une boîte de dialogue entre votre service et l’individu, où un bot dans une conversation de groupe ou un canal diffuse tout à un groupe de personnes.

Selon l’expérience que vous souhaitez créer, le bot peut avoir besoin de travailler dans plusieurs étendues : personnel, groupchat et équipe. Le travail pour prendre en charge plusieurs étendues est minimal. Il n’est pas attendu dans Teams que votre bot fonctionne dans toutes les étendues, mais vous devez vous assurer que votre bot est logique et fournit une valeur utilisateur dans les étendues que vous choisissez de prendre en charge.

## <a name="best-practice-welcome-messages-in-personal-conversations"></a>Meilleure pratique : messages de bienvenue dans les conversations personnelles

Votre bot doit envoyer de manière [proactive](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) un message de bienvenue à une conversation personnelle la première fois (et uniquement la première fois) qu’un utilisateur lance une conversation personnelle avec votre bot. Cette recommandation ne s’applique pas aux contacts pour la première fois dans un canal.
