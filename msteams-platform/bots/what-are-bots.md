---
title: Bots dans Microsoft Teams
author: surbhigupta
description: Dans cet article, utilisez des bots conversationnels dans Microsoft Teams pour partager des fichiers, envoyer des notifications proactives, des cartes interactives, passer des appels, appeler une commande de bot, IVR.
ms.topic: overview
ms.localizationpriority: high
ms.author: anclear
ms.openlocfilehash: 90176b63c64d23ae76a8c98515e37455ab0742c0
ms.sourcegitcommit: 217025a61ed9c3b76b507fe95563142abc6d0318
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/17/2022
ms.locfileid: "67363511"
---
# <a name="build-bots-for-teams"></a>Créer des bots pour Teams

> [!NOTE]
> Il est recommandé de créer votre première application bot ou application de bot de notification à l’aide de l’outil de développement de nouvelle génération pour Teams. Pour plus d’informations, consultez [Teams Toolkit pour Visual Studio Code](../toolkit/teams-toolkit-fundamentals.md) et [Teams Toolkit pour Visual Studio](../toolkit/teams-toolkit-overview-visual-studio.md).

Un bot est également appelé chatbot ou bot de conversation. Il s’agit d’une application qui exécute des tâches simples et répétitives effectuées par des utilisateurs tels que le service clientèle ou le personnel de support technique. L’utilisation quotidienne de bots inclut des bots qui fournissent des informations sur la météo, qui effectuent des réservations au restaurant ou qui fournissent des informations concernant les voyages. Les interactions avec les bots peuvent être des questions et réponses rapides ou des conversations complexes.

> [!IMPORTANT]
>
> * Actuellement, les bots sont disponibles dans le Cloud de la communauté du secteur public (GCC) et GCC-High, mais pas dans le département de la Défense (DOD).
>
> * Les applications bot au sein de Microsoft Teams sont disponibles dans le Cloud de la communauté du secteur public supérieur via le [Service de bot d’Azure](/azure/bot-service/how-to-deploy-gov-cloud-high) et l’inscription du canal de bot doit être effectuée dans le portail Azure Government.
>
> * Les applications dans le Cloud de la communauté du secteur public supérieur prennent uniquement en charge jusqu’à la version de manifeste v1.10. Les URL d’image dans Cartes adaptatives ne sont pas prises en charge dans l’environnement du Cloud de la communauté du secteur public supérieur. Vous pouvez remplacer une URL d’image par un DataUri encodé en Base64.

Les bots de conversation permettent aux utilisateurs d’interagir avec votre service web à l’aide de texte, de cartes interactives et de modules de tâche.

:::image type="content" source="../assets/images/invokebotwithtext.png" alt-text="La capture d’écran est un exemple montrant un service web utilisant du texte."lightbox="../assets/images/invokebotwithtext.png":::

:::image type="content" source="../assets/images/invokebotwithcard.png" alt-text="La capture d’écran est un exemple montrant un service web utilisant des cartes interactives."lightbox="../assets/images/invokebotwithcard.png"border="true":::

:::image type="content" source="../assets/images/task-module-example.png" alt-text="La capture d’écran est un exemple montrant un service web à l’aide d’un module de tâche." lightbox="../assets/images/task-module-example-expanded.png":::

Les bots de conversation sont extrêmement flexibles. Les bots peuvent gérer quelques commandes de base ou des tâches complexes qui impliquent l’intelligence artificielle et le traitement du langage naturel. Les bots peuvent faire partie d’une application plus grande ou être autonomes.

Utilisez la bonne combinaison de cartes, de texte et de modules de tâche pour créer un bot utile. L’image suivante montre un utilisateur qui discute avec un bot dans une conversation privée à l’aide de texte et de cartes interactives.

:::image type="content" source="~/assets/images/FAQPlusEndUser.gif" alt-text="La capture d’écran est un exemple montrant un exemple de bot FAQ.":::

Chaque interaction entre l’utilisateur et le bot est représentée comme une activité. Lorsqu’un bot reçoit une activité, il la transmet à ses gestionnaires d’activité. Voir [les gestionnaires d’activité du bot](~/bots/bot-basics.md).

Les bots sont des applications qui ont une interface de conversation. Vous pouvez interagir avec un bot à l’aide de texte, de cartes interactives et de reconnaissance vocale. Un bot se comporte différemment dans une conversation de canal ou de groupe et dans une conversation privée. Les conversations sont gérées via le connecteur Bot Framework. Voir [les informations de base des conversations](~/bots/how-to/conversations/conversation-basics.md).

Votre bot a besoin d’informations contextuelles, telles que les détails du profil utilisateur, pour accéder au contenu pertinent et améliorer l’expérience du bot. Voir [obtenir le contexte Teams](~/bots/how-to/get-teams-context.md).

Vous pouvez envoyer et recevoir des fichiers via le bot à l’aide des API Graph ou des API de bot Teams. Consultez [Envoyer et recevoir des fichiers via un bot](~/bots/how-to/bots-filesv4.md).

La limitation de débit permet d’optimiser les bots utilisés pour l’application Teams. Pour protéger Teams et ses utilisateurs, les API de bot fournissent une limite de débit pour les demandes entrantes. Voir [optimiser votre bot avec une limite de débit dans Teams](~/bots/how-to/rate-limit.md).

Avec les API Microsoft Graph pour les appels et les réunions en ligne, les applications Teams peuvent désormais interagir avec les utilisateurs à l’aide de la voix et de la vidéo. Voir [les bots d’appels et de réunions.](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)

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
| bot Hello World | Il s’agit d’une application Hello World simple avec les fonctionnalités d’extension Bot et Message. |  | [View](https://github.com/OfficeDev/TeamsFx-Samples/tree/v1.0.0/hello-world-bot) |
| Notification de carte adaptative | Il s’agit d’un exemple qui montre comment envoyer des notifications avec différentes cartes adaptatives à l’aide de Bots. |  | [View](https://github.com/OfficeDev/TeamsFx-Samples/tree/v1.0.0/adaptive-card-notification) |
| Notification de webhook entrant | Il s’agit d’un exemple qui montre comment envoyer des notifications via le webhook entrant dans les canaux Microsoft Teams. |  | [View](https://github.com/OfficeDev/TeamsFx-Samples/tree/v1.0.0/incoming-webhook-notification) |

## <a name="see-also"></a>Voir aussi

* [Créer un robot pour Teams](../resources/bot-v3/bots-create.md)
* [Fonctionnement des bots Microsoft Teams](/azure/bot-service/bot-builder-basics-teams)
* [Enregistrer le bot d’appels et de réunions pour Microsoft Teams](~/bots/calls-and-meetings/registering-calling-bot.md)
* [Ajouter l’authentification à votre bot Teams](~/bots/how-to/authentication/add-authentication.md)
* [Gestionnaire d'activité du robot](~/bots/bot-basics.md)
* [Événements de conversation dans votre robot Teams](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
* [Créer votre première application de bot à l’aide de JavaScript](../sbs-gs-bot.yml)
* [Générer un bot de notification avec JavaScript](../sbs-gs-notificationbot.yml)
