---
title: Bots dans Microsoft Teams
author: surbhigupta
description: Présentation des bots dans Microsoft Teams.
ms.topic: overview
ms.localizationpriority: high
ms.author: anclear
ms.openlocfilehash: 81fa44730a26f3d7bcafdc9f37ec15b4eb7b1951
ms.sourcegitcommit: aa95313cdab4fbf0a9f62a047ebbe6a5f1fbbf5d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/20/2022
ms.locfileid: "65602291"
---
# <a name="bots-in-microsoft-teams"></a>Bots dans Microsoft Teams

Un bot est également appelé chatbot ou bot de conversation. Il s’agit d’une application qui exécute des tâches simples et répétitives effectuées par des utilisateurs tels que le service clientèle ou le personnel de support technique. L’utilisation quotidienne de bots inclut des bots qui fournissent des informations sur la météo, qui effectuent des réservations au restaurant ou qui fournissent des informations concernant les voyages. Les interactions avec les bots peuvent être des questions et réponses rapides ou des conversations complexes.

> [!IMPORTANT]
> Actuellement, les bots sont disponibles dans le Cloud de la communauté du secteur public (GCC) et GCC-High, mais pas dans le département de la Défense (DOD).
> 
> Les applications Bot dans Microsoft Teams sont disponibles dans GCC-High par le biais d’[Azure Bot Service](/azure/bot-service/channel-connect-teams).

Les bots de conversation permettent aux utilisateurs d’interagir avec votre service web à l’aide de texte, de cartes interactives et de modules de tâche.

:::image type="content" source="../assets/images/invokebotwithtext.png" alt-text="Service web utilisant du texte"lightbox="../assets/images/invokebotwithtext.png":::

:::image type="content" source="../assets/images/invokebotwithcard.png" alt-text="service web à l’aide de cartes interactives"lightbox="../assets/images/invokebotwithcard.png"border="true":::

:::image type="content" source="../assets/images/task-module-example.png" alt-text="service web à l’aide du module de tâche"lightbox="../assets/images/task-module-example.png"border="true":::

Les bots de conversation sont extrêmement flexibles. Les bots peuvent gérer quelques commandes de base ou des tâches complexes qui impliquent l’intelligence artificielle et le traitement du langage naturel. Les bots peuvent faire partie d’une application plus grande ou être autonomes.

Utilisez la bonne combinaison de cartes, de texte et de modules de tâche pour créer un bot utile. L’image suivante montre un utilisateur qui discute avec un bot dans une conversation privée à l’aide de texte et de cartes interactives.

:::image type="content" source="~/assets/images/FAQPlusEndUser.gif" alt-text="Exemple de bot FAQ" border="true":::

Chaque interaction entre l’utilisateur et le bot est représentée comme une activité. Lorsqu’un bot reçoit une activité, il la transmet à ses gestionnaires d’activité. Voir [les gestionnaires d’activité du bot](~/bots/bot-basics.md).

Les bots sont des applications qui ont une interface de conversation. Vous pouvez interagir avec un bot à l’aide de texte, de cartes interactives et de reconnaissance vocale. Un bot se comporte différemment dans une conversation de canal ou de groupe et dans une conversation privée. Les conversations sont gérées via le connecteur Bot Framework. Voir [les informations de base des conversations](~/bots/how-to/conversations/conversation-basics.md).

Votre bot nécessite des informations contextuelles, telles que les détails du profil utilisateur, pour accéder au contenu pertinent et améliorer l’expérience du bot. Consultez [obtenir le contexte Teams](~/bots/how-to/get-teams-context.md).

Vous pouvez envoyer et recevoir des fichiers via le bot à l’aide des API Graph ou des API de bot Teams. Consultez [Envoyer et recevoir des fichiers via un bot](~/bots/how-to/bots-filesv4.md).

La limitation de débit permet d’optimiser les bots utilisés pour l’application Teams. Pour protéger Microsoft Teams et ses utilisateurs, les API de bot fournissent une limite de débit pour les demandes entrantes. Voir [optimiser votre bot avec une limite de débit dans Teams](~/bots/how-to/rate-limit.md).

Avec Microsoft Graph API pour les appels et les réunions en ligne, les applications Microsoft Teams peuvent désormais interagir avec les utilisateurs à l’aide de la voix et de la vidéo. Consultez [les bots d’appels et de réunions](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).

Vous pouvez utiliser les API de bot Teams pour obtenir des informations pour les membres d’une conversation ou d’une équipe. Consultez [les modifications apportées aux API de bot Teams pour récupérer les membres de l’équipe ou de la conversation](~/resources/team-chat-member-api-changes.md).

<!--- TBD: For quick scanning, see if the above information can be itemized as a list.
--->

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Bots et kits de développement](~/bots/bot-features.md)

## <a name="code-samples"></a>Exemples de code

|Exemple de nom | Description | C# | Node.js |
|----------------|-----------------|--------------|--------------|
| Bot de rappel de tâche quotidienne| Expliquer comment planifier une tâche périodique et obtenir un rappel à une heure prévue. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-daily-task-reminder/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-daily-task-reminder/nodejs) |

## <a name="see-also"></a>Voir aussi

* [Créer un robot pour Teams](../resources/bot-v3/bots-create.md)
* [Fonctionnement des bots Microsoft Teams](/azure/bot-service/bot-builder-basics-teams)
* [Enregistrer le bot d’appels et de réunions pour Microsoft Teams](~/bots/calls-and-meetings/registering-calling-bot.md)
* [Ajouter l’authentification à votre bot Teams](~/bots/how-to/authentication/add-authentication.md)
* [Gestionnaire d'activité du robot](~/bots/bot-basics.md)
* [Événements de conversation dans votre robot Teams](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
