---
title: conversations 1-sur-1 avec des robots
description: Décrit le scénario de bout en bout de la conversation 1-on-1 avec un bot dans Microsoft teams
keywords: scénarios teams 1on1 1to1 de conversation
ms.date: 05/20/2019
ms.openlocfilehash: e23bb98160125d7fdbb4521467e2f522d6b6ce40
ms.sourcegitcommit: fdcd91b270d4c2e98ab2b2c1029c76c49bb807fa
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/13/2020
ms.locfileid: "44801081"
---
# <a name="have-a-personal-one-on-one-conversation-with-a-microsoft-teams-bot"></a>Disposer d’une conversation personnelle (individuelle) avec un robot Microsoft teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft teams permet aux utilisateurs de participer à des conversations directes avec des robots créés sur [Microsoft bot Framework](/azure/bot-service/?view=azure-bot-service-3.0). Les utilisateurs peuvent trouver des robots dans la Galerie découvrir les applications et les ajouter à leur expérience de teams pour les conversations personnelles. Les propriétaires d’équipe et les utilisateurs disposant des autorisations appropriées peuvent également ajouter des bots en tant que membres de l’équipe (voir [interagir dans un canal d’équipe](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)), ce qui les rend non seulement disponibles dans les canaux de l’équipe, mais également pour la conversation personnelle de tous ces utilisateurs.

La conversation personnelle diffère de celle des canaux en ce que l’utilisateur n’a pas besoin de @mention le bot. Si un bot est utilisé dans plusieurs contextes (personnel, groupChat ou canal), vous devrez détecter si le robot se trouve dans une conversation ou un canal de groupe et traiter les messages un peu différemment. Pour plus d’informations, consultez [la rubrique interagir dans un canal d’équipe ou une conversation de groupe](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) .

## <a name="designing-a-great-personal-bot"></a>Conception d’un robot personnel

Un robot puissant dans Microsoft teams permet aux utilisateurs d’obtenir les informations dont ils ont besoin, tout cela dans le cadre de l’expérience de teams. Les conversations personnelles avec un bot sont des échanges privés entre un bot et son utilisateur ; ils constituent un excellent moyen de fournir des informations spécifiques et pertinentes pour cet utilisateur dans le contexte personnel. Un bot dans la conversation personnelle est une boîte de dialogue entre votre service et l’individu, où un bot d’une conversation ou d’un canal de groupe diffuse tout vers un groupe de personnes.

En fonction de l’expérience que vous souhaitez créer, il se peut que le robot doive travailler sur plusieurs étendues-personnel, groupChat et/ou équipe. Le travail de prise en charge de plusieurs étendues est minime. Il n’y a pas d’attentes dans teams que votre bot fonctionne dans toutes les étendues, mais vous devez vous assurer que votre robot est pertinent et qu’il fournit la valeur de l’utilisateur dans n’importe quelle étendue que vous choisissez de prendre en charge.

## <a name="best-practice-welcome-messages-in-personal-conversations"></a>Meilleure pratique : messages de bienvenue dans les conversations personnelles

Votre robot doit [Envoyer de manière proactive](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) un message de bienvenue à une conversation personnelle la première fois (et uniquement la première fois) un utilisateur lance une conversation personnelle avec votre robot. (Cette recommandation ne s’applique pas aux contacts pour la première fois dans un canal.)
