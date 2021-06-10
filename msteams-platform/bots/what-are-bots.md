---
title: Bots dans Microsoft Teams
author: clearab
description: Vue d’ensemble des bots Microsoft Teams.
ms.topic: overview
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: e91211d7237384b1d39f877cf217dcddfc66cc1e
ms.sourcegitcommit: d90c5dafea09e2893dea8da46ee49516bbaa04b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2021
ms.locfileid: "52075660"
---
# <a name="bots-in-microsoft-teams"></a>Bots dans Microsoft Teams

Un bot également appelé bot de conversation est une application qui exécute des tâches automatisées simples et répétitives effectuées par les utilisateurs, telles que le service clientèle ou le personnel de support technique. Parmi les exemples de bots utilisés quotidiennement, citons les bots qui fournissent des informations sur la météo, qui réservent des réservations de réservations ou qui fournissent des informations de voyage. Une interaction de bot peut être une question et une réponse rapides, ou il peut s’agit d’une conversation complexe qui permet d’accéder aux services.

> [!VIDEO https://www.youtube-nocookie.com/embed/zSIysk0yL0Q]

Les bots de conversation permettent aux utilisateurs d’interagir avec votre service web via du texte, des cartes interactives et des modules de tâches.

![Appeler un bot à l’aide de texte](~/assets/images/invokebotwithtext.png)

![Appeler un bot à l’aide d’une carte](~/assets/images/invokebotwithcard.png)

<img src="~/assets/images/task-module-example.png" alt="Invoke bot using task module" width="400"/>

Les bots de conversation sont extrêmement flexibles et peuvent être étendues pour gérer quelques commandes simples ou des tâches complexes, optimisées pour l’intelligence artificielle et de traitement du langage naturel. Ils peuvent être un aspect d’une application plus grande ou être entièrement autonomes.

La recherche de la combinaison de cartes, de texte et de modules de tâche est essentielle pour créer un bot utile. L’image suivante montre un utilisateur qui discute avec un bot dans une conversation un-à-un à l’aide de cartes texte et interactives :

:::image type="content" source="~/assets/images/FAQPlusEndUser.gif" alt-text="Exemple de bot FAQ" border="true":::

Chaque interaction entre l’utilisateur et le bot est représentée comme une activité. Lorsqu’un bot reçoit une activité, il la transmet à ses handlers d’activité. Pour plus d’informations, voir [les handlers d’activité des bots.](~/bots/bot-basics.md) 

En outre, les bots sont des applications qui ont une interface de conversation. Vous pouvez interagir avec un bot à l’aide de texte, de cartes interactives et de reconnaissance vocale. Un bot se comporte différemment selon qu’il s’agit d’une conversation de canal ou de groupe, ou d’une conversation un-à-un. Les conversations sont gérées via le connecteur Bot Framework. Pour plus d’informations, voir [les informations de base de la conversation.](~/bots/how-to/conversations/conversation-basics.md)

Votre bot nécessite des informations contextuelles, telles que des détails de profil utilisateur pour accéder au contenu pertinent et améliorer l’expérience du bot. Pour plus d’informations, [voir obtenir Teams contexte.](~/bots/how-to/get-teams-context.md) 

Vous pouvez également envoyer et recevoir des fichiers via le bot à l’aide Graph API ou Teams’API de bot. Pour plus d’informations, voir [envoyer et recevoir des fichiers via le bot.](~/bots/how-to/bots-filesv4.md)

En outre, la limitation des taux est utilisée pour optimiser les bots utilisés pour Teams application. Pour protéger Microsoft Teams et ses utilisateurs, les API de bot fournissent une limite de taux pour les demandes entrantes. Pour plus d’informations, voir [optimiser votre bot avec une limite](~/bots/how-to/rate-limit.md)de taux Teams .

Avec les API Microsoft Graph pour les appels et les réunions en ligne, Microsoft Teams applications peuvent désormais interagir avec les utilisateurs à l’aide de la voix et de la vidéo. Pour plus d’informations, voir [les bots d’appels et de réunions.](~/bots/calls-and-meetings/calls-meetings-bots-overview.md) 

Vous pouvez utiliser les API Teams bot pour obtenir des informations pour un ou plusieurs membres d’une conversation ou d’une équipe. Pour plus d’informations, voir [les modifications apportées aux API Teams bot pour](~/resources/team-chat-member-api-changes.md)récupérer des membres d’équipe ou de conversation.

## <a name="see-also"></a>Voir aussi

[Créer un robot pour Teams](~/bots/how-to/create-a-bot-for-teams.md)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Bots et kits de développement](~/bots/bot-features.md)
