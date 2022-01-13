---
title: Bots dans Microsoft Teams
author: surbhigupta
description: Vue d’ensemble des bots dans Microsoft Teams.
ms.topic: overview
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: a9f53654ba3240b973b77c05cd64a22c80237350
ms.sourcegitcommit: a6c39106ccc002d02a65e11627659e0c48981d8a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/13/2022
ms.locfileid: "62014562"
---
# <a name="bots-in-microsoft-teams"></a>Bots dans Microsoft Teams

Un bot est également appelé bot de conversation ou bot de conversation. Il s’agit d’une application qui exécute des tâches simples et répétitives par des utilisateurs tels que le service clientèle ou le personnel de support technique. L’utilisation quotidienne de bots inclut des bots qui fournissent des informations sur la météo, qui réservent des réservations de réservation de réservation ou qui fournissent des informations de voyage. Les interactions avec les bots peuvent répondre rapidement à des questions ou être une conversation complexe.

> [!IMPORTANT]
> Actuellement, les bots sont disponibles dans Cloud de la communauté du secteur public (Cloud de la communauté du secteur public) et non dans GCC-High et le département de la Défense (DOD).

Les bots de conversation permettent aux utilisateurs d’interagir avec votre service web à l’aide de texte, de cartes interactives et de modules de tâche.

![Appeler un bot à l’aide de texte](~/assets/images/invokebotwithtext.png)

![Appeler un bot à l’aide d’une carte](~/assets/images/invokebotwithcard.png)

<img src="~/assets/images/task-module-example.png" alt="Invoke bot using task module" width="400"/>

Les bots de conversation sont extrêmement flexibles. Les bots peuvent gérer quelques commandes de base ou des tâches complexes qui impliquent l’intelligence artificielle et le traitement du langage naturel. Les bots peuvent faire partie d’une application plus grande ou être autonomes.

Utilisez la combinaison de cartes, de texte et de modules de tâche qui vous permet de créer un bot utile. L’image suivante montre un utilisateur qui discute avec un bot dans une conversation un-à-un à l’aide de texte et de cartes interactives.

:::image type="content" source="~/assets/images/FAQPlusEndUser.gif" alt-text="Exemple de bot FAQ" border="true":::

Chaque interaction entre l’utilisateur et le bot est représentée comme une activité. Lorsqu’un bot reçoit une activité, il la transmet à ses sous-traites d’activité. Voir [les handlers d’activité du bot.](~/bots/bot-basics.md)

Les bots sont des applications qui ont une interface de conversation. Vous pouvez interagir avec un bot à l’aide de texte, de cartes interactives et de reconnaissance vocale. Un bot se comporte différemment dans une conversation de canal ou de groupe et dans une conversation un-à-un. Les conversations sont gérées via le connecteur Bot Framework. Voir [les informations de base de la conversation.](~/bots/how-to/conversations/conversation-basics.md)

Votre bot nécessite des informations contextuelles, telles que des détails de profil utilisateur pour accéder au contenu pertinent et améliorer l’expérience du bot. Voir [obtenir Teams contexte.](~/bots/how-to/get-teams-context.md)

Vous pouvez envoyer et recevoir des fichiers via le bot à l’aide Graph API ou Teams’API de bot. Consultez [les fichiers d’envoi et de réception via le bot.](~/bots/how-to/bots-filesv4.md)

La limitation des taux permet d’optimiser les bots utilisés pour Teams application. Pour protéger Microsoft Teams et ses utilisateurs, les API de bot fournissent une limite de taux pour les demandes entrantes. Voir [optimiser votre bot avec une limite de taux dans Teams](~/bots/how-to/rate-limit.md).

Avec les API Microsoft Graph pour les appels et les réunions en ligne, Microsoft Teams applications peuvent désormais interagir avec les utilisateurs à l’aide de la voix et de la vidéo. Voir [les bots d’appels et de réunions.](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)

Vous pouvez utiliser les API Teams bot pour obtenir des informations pour les membres d’une conversation ou d’une équipe. Consultez [les modifications apportées aux API Teams bot pour](~/resources/team-chat-member-api-changes.md)récupérer des membres d’équipe ou de conversation.

<!--- TBD: For quick scanning, see if the above information can be itemized as a list.
--->

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Bots et kits de développement](~/bots/bot-features.md)

## <a name="code-sample"></a>Exemple de code

|Exemple de nom | Description | C# | Node.js |
|----------------|-----------------|--------------|--------------|
| Rappel quotidien de tâche du bot| Montrez comment planifier une tâche périodique et obtenir un rappel à une heure prévue. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-daily-task-reminder/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-daily-task-reminder/nodejs) |

## <a name="see-also"></a>Voir aussi

* [Créer un robot pour Teams](~/bots/how-to/create-a-bot-for-teams.md)
* [Inscrire les appels et le bot de réunions pour Microsoft Teams](~/bots/calls-and-meetings/registering-calling-bot.md)
* [Ajouter l’authentification à Teams bot](~/bots/how-to/authentication/add-authentication.md)
* [Gestionnaire d'activité du robot](~/bots/bot-basics.md)
* [Événements de conversation dans votre robot Teams](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
