---
title: Appels et bots de réunions en ligne
description: Découvrez comment vos applications Microsoft Teams peuvent interagir avec les utilisateurs à l’aide de la voix et de la vidéo à l’aide des API Microsoft Graph pour les appels et les réunions en ligne et en savoir plus sur les flux multimédias en temps réel
ms.topic: conceptual
ms.localizationpriority: medium
keywords: appel d’appels audio vidéo de réunions vocales en ligne vocale en temps réel pour les flux multimédias
ms.openlocfilehash: 2339431e6643d9ecf986b7a327f5fb7ee764fa00
ms.sourcegitcommit: 5e5d2d3fb621bcbd9d792a5b450f95167ec8548b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/22/2022
ms.locfileid: "63727631"
---
# <a name="calls-and-online-meetings-bots"></a>Appels et bots de réunions en ligne

Les bots peuvent interagir avec Teams appels et réunions à l’aide de la voix, de la vidéo et du partage d’écran en temps réel. Avec [les API Microsoft Graph](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true) pour les appels et les réunions en ligne, Teams applications peuvent désormais interagir avec les utilisateurs à l’aide de la voix et de la vidéo pour améliorer l’expérience. Ces API vous permettent d’ajouter les nouvelles fonctionnalités suivantes :

* Réponse vocale interactive (IVR).
* Contrôle d’appel.
* Accès aux flux audio et vidéo en temps réel, y compris au partage de bureau et d’application.

Pour utiliser ces GRAPH dans une application Teams, vous créez un bot et spécifiez des informations et des autorisations supplémentaires.

En outre, la plateforme Real-time Media permet aux bots d’interagir avec Teams appels et réunions à l’aide de la voix en temps réel, de la vidéo et du partage d’écran. Un bot qui participe à des appels audio ou vidéo et à des réunions en ligne est un bot Microsoft Teams avec quelques fonctionnalités supplémentaires utilisées pour inscrire le bot.

Le manifeste Teams’application avec deux paramètres supplémentaires et les autorisations `supportsCalling` `supportsVideo`Graph pour l’ID d’application Microsoft de votre bot et le consentement de l’administrateur client vous permettent d’inscrire le bot. Lors de l’inscription d’un bot d’appels et de réunions pour Teams, l’URL de webhook est mentionnée, qui est le point de terminaison webhook pour tous les appels entrants vers votre bot. Un bot multimédia hébergé par l’application nécessite Microsoft. Graph. Bibliothèque Communications.Calls.Media .NET pour accéder aux flux multimédias audio et vidéo, et le bot doit être déployé sur un ordinateur Windows Server ou un système d’exploitation invité Windows Server dans Azure. Les bots sur Teams ne prend en charge qu’un ensemble spécifique de formats multimédias pour le contenu audio et vidéo.

Vous devez maintenant comprendre certains concepts, termes et conventions fondamentaux.

## <a name="terminologies"></a>Terminologies

Les concepts de base, la terminologie et les conventions suivants vous guident tout au long de l’utilisation des appels et des bots de réunions en ligne :

* Appels audio ou vidéo
* Types d’appel
* Signaux
* Appels et réunions en ligne
* Médias en temps réel

### <a name="audio-or-video-calls"></a>Appels audio ou vidéo

Les appels dans Teams peuvent être purement audio ou audio et vidéo. Au lieu d’un appel audio ou vidéo, le terme appel est utilisé.

### <a name="call-types"></a>Types d’appel

Les appels sont d’égal à égal entre une personne et votre bot, ou à plusieurs entre votre bot et au moins deux personnes dans un appel de groupe.

![Types d’appels](~/assets/images/calls-and-meetings/call-types.png)

Voici les différents types d’appels et autorisations requis pour l’appel :

* Un utilisateur peut lancer un appel d’égal à égal avec votre bot ou inviter votre bot à un appel à plusieurs existant. L’appel à plusieurs n’est pas encore activé dans l’interface Teams’utilisateur.

    > [!NOTE]
    > Les appels initiés par l’utilisateur vers un bot ne sont actuellement pas pris en charge Microsoft Teams plateforme mobile.

* Graph autorisations d’accès ne sont pas nécessaires pour qu’un utilisateur lance un appel d’égal à égal avec votre bot. Des autorisations supplémentaires sont nécessaires pour que votre bot participe à un appel à plusieurs ou pour qu’il lance un appel d’égal à égal avec un utilisateur.
* Un appel peut commencer comme pair à pair et finir par devenir un appel à plusieurs. Votre bot peut lancer des appels à plusieurs en invitant d’autres personnes, à condition que votre bot dispose des autorisations adéquates. Si votre bot n’est pas autorisé à participer à des appels de groupe et si un participant ajoute un autre participant à l’appel, il est supprimé de l’appel.

### <a name="signals"></a>Signaux

Il existe deux types de signaux : l’appel entrant et l’appel entrant. Voici les différentes fonctionnalités des signaux :

* Pour recevoir un appel entrant, entrez un point de terminaison dans les paramètres de votre bot. Ce point de terminaison reçoit une notification lorsqu’un appel entrant est initié. Vous pouvez répondre à l’appel, le rejeter ou le rediriger vers une autre personne.

    ![Gestion des appels](~/assets/images/calls-and-meetings/call-handling.png)

* Lorsqu’un bot est en cours d’appel, il existe des API pour activer et désactiver le son du bot et pour démarrer ou arrêter le partage de contenu vidéo ou de bureau avec d’autres participants.
* Le bot peut également accéder à la liste des participants, inviter de nouveaux participants et les désactiver.

### <a name="calls-and-online-meetings"></a>Appels et réunions en ligne

Du point Teams du point de vue de l’utilisateur, il existe deux types de réunions en ligne, ad hoc et programmées. Du point de vue d’un bot, les deux réunions en ligne sont identiques. Pour un bot, une réunion en ligne est un appel à plusieurs entre un ensemble de participants et inclut les coordonnées de la réunion. Les coordonnées de réunion sont les métadonnées de la réunion`botId`, y compris , `chatId` associées à la réunion, `joinUrl``startTime` `endTime`ou, etc.

### <a name="real-time-media"></a>Médias en temps réel

Lorsqu’un bot participe à un appel ou à une réunion en ligne, il doit gérer les flux audio et vidéo. Lorsque les utilisateurs parlent lors d’un appel, s’affichent sur une webcam ou présentent leurs écrans dans une réunion, un bot l’affiche sous forme de flux audio et vidéo. Si un bot souhaite dire quelque chose d’aussi simple que, appuyez sur **0** pour atteindre l’opérateur dans un scénario de réponse vocale interactive (IVR), il nécessite la lecture d’un . Fichier WAV. Collectivement, il s’agit d’un média ou d’un média en temps réel.

Les médias en temps réel font référence à des scénarios où les médias doivent être traitées en temps réel, par opposition à la lecture d’audio ou de vidéos précédemment enregistrées. La gestion des flux multimédias, en particulier des flux multimédias en temps réel, est extrêmement complexe. Microsoft a créé la plateforme Multimédia en temps réel pour gérer ces scénarios et décharger autant que possible la lourde charge traditionnelle du traitement multimédia en temps réel. Lorsque le bot répond à un appel entrant ou rejoint un appel nouveau ou existant, il doit indiquer à la plateforme Multimédia en temps réel comment le média est géré. Si vous construisez une application de réponse vocale vocale vocale, vous pouvez décharger le traitement audio coûteux à Microsoft. Sinon, si votre bot nécessite un accès direct aux flux multimédias, ce scénario est également pris en charge. Il existe deux types de traitement multimédia :

* **Média hébergé par** le service : les bots se concentrent sur la gestion des flux de travail d’application, tels que le routage des appels et le déchargement du traitement audio vers la plateforme Microsoft Real-time Media. Avec les médias hébergés par le service, vous avez plusieurs options pour implémenter et héberger votre bot. Un bot média hébergé par le service peut être implémenté en tant que service sans état, car il ne traite pas les médias localement. Les robots multimédias hébergés par le service peuvent utiliser les API suivantes :

  * `PlayPrompt` pour la lecture d’un clip audio.
  * `Record` pour l’enregistrement des clips audio.
  * `SubscribeToTone` pour s’abonner à des tonalités DTMF (dual tone multiple frequency).

    Par exemple, savoir quand un utilisateur a appuyer **sur 0** pour atteindre l’opérateur.

* **Support hébergé par l’application** : pour qu’un bot obtienne un accès direct aux médias, il a besoin d’une autorisation Graph spécifique. Une fois que votre bot dispose de l’autorisation, la bibliothèque multimédia en temps réel et le [SDK d’appel Graph](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/articles/index.html#graph-calling-sdk-and-stateful-client-builder) vous aident à créer des médias enrichis en temps réel et des bots d’appel.[](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/) Un bot hébergé par l’application doit être hébergé dans un environnement Windows. Pour plus d’informations, voir [bots multimédias hébergés par l’application](./requirements-considerations-application-hosted-media-bots.md).

## <a name="code-sample"></a>Exemple de code

| **Exemple de nom** | **Description** | **Graph** |
|---------------|----------|--------|
| Graph communication | Graph communications pour interagir avec la plateforme de communication de Microsoft. | [View](https://github.com/microsoftgraph/microsoft-graph-comms-samples) |

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Appels et réunions avec les médias en temps réel](~/bots/calls-and-meetings/real-time-media-concepts.md)

## <a name="see-also"></a>Voir aussi

* [Graph API de référence](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)
* [Exemple d’applications](https://github.com/microsoftgraph/microsoft-graph-comms-samples)
* [Inscription d’un bot qui prend en charge les appels et les réunions en ligne](./registering-calling-bot.md)
* [Graph pour les appels et les bots de réunion en ligne](./registering-calling-bot.md#add-graph-permissions)
* [Comment développer des bots d’appels et de réunions en ligne sur votre ordinateur](./debugging-local-testing-calling-meeting-bots.md)
* [Conditions requises et considérations pour les robots multimédias hébergés par l’application](./requirements-considerations-application-hosted-media-bots.md)
* [Informations techniques sur la gestion des notifications d’appels entrants](./call-notifications.md)
