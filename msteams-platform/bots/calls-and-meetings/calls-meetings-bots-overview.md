---
title: Bots d’appels et de réunions en ligne
description: Découvrez comment vos applications Microsoft Teams peuvent interagir avec les utilisateurs à l’aide de la voix et de la vidéo à l’aide des API Microsoft Graph pour les appels et les réunions en ligne, et en savoir plus sur les flux multimédias en temps réel
ms.topic: conceptual
ms.localizationpriority: medium
keywords: appel d’appels audio vidéo IVR voix en ligne réunions en temps réel flux multimédia bot
ms.openlocfilehash: e17d0c18bfb3f751a11e43780dba9f0f85441a96
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073822"
---
# <a name="calls-and-online-meetings-bots"></a>Bots d’appels et de réunions en ligne

Les bots peuvent interagir avec Teams appels et réunions à l’aide de la voix, de la vidéo et du partage d’écran en temps réel. Avec [Les API Microsoft Graph pour les appels et les réunions en ligne](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true), Teams applications peuvent désormais interagir avec les utilisateurs à l’aide de la voix et de la vidéo pour améliorer l’expérience. Ces API vous permettent d’ajouter les nouvelles fonctionnalités suivantes :

* Réponse vocale interactive (IVR).
* Contrôle d’appel.
* Accès aux flux audio et vidéo en temps réel, y compris le partage de bureau et d’application.

Pour utiliser ces API Graph dans une application Teams, vous créez un bot et spécifiez des informations et des autorisations supplémentaires.

En outre, la plateforme multimédia en temps réel permet aux bots d’interagir avec Teams appels et réunions à l’aide de la voix, de la vidéo et du partage d’écran en temps réel. Un bot qui participe à des appels audio ou vidéo et à des réunions en ligne est un bot Microsoft Teams régulier avec peu de fonctionnalités supplémentaires utilisées pour inscrire le bot.

Le manifeste de l’application Teams avec deux paramètres `supportsCalling` supplémentaires et `supportsVideo`Graph autorisations pour l’ID d’application Microsoft de votre bot et le consentement de l’administrateur client vous permettent d’inscrire le bot. Lors de l’inscription d’un bot d’appels et de réunions pour Teams, l’URL du webhook est mentionnée, qui est le point de terminaison webhook pour tous les appels entrants à votre bot. Un bot multimédia hébergé par une application nécessite Microsoft. Graph. La bibliothèque .NET Communications.Calls.Media pour accéder aux flux multimédias audio et vidéo, et le bot doit être déployé sur une machine Windows Server ou Windows système d’exploitation invité du serveur dans Azure. Les bots sur Teams ne prennent en charge qu’un ensemble spécifique de formats multimédias pour le contenu audio et vidéo.

À présent, vous devez comprendre certains concepts, terminologie et conventions de base.

## <a name="terminologies"></a>Terminologies

Les concepts fondamentaux, la terminologie et les conventions suivants vous guident dans l’utilisation d’appels et de bots de réunion en ligne :

* Appels audio ou vidéo
* Types d’appel
* Signaux
* Appels et réunions en ligne
* Média en temps réel

### <a name="audio-or-video-calls"></a>Appels audio ou vidéo

Les appels dans Teams peuvent être purement audio ou audio et vidéo. Au lieu d’un appel audio ou vidéo, le terme appel est utilisé.

### <a name="call-types"></a>Types d’appel

Les appels sont d’égal à égal entre une personne et votre bot, ou multipartie entre votre bot et deux personnes ou plus dans un appel de groupe.

![Types d’appels](~/assets/images/calls-and-meetings/call-types.png)

Voici les différents types d’appels et autorisations requis pour l’appel :

* Un utilisateur peut lancer un appel d’égal à égal avec votre bot ou inviter votre bot dans un appel multiparte existant. L’appel multiparte n’est pas encore activé dans l’interface utilisateur Teams.

    > [!NOTE]
    > Les appels lancés par l’utilisateur à un bot ne sont actuellement pas pris en charge sur Microsoft Teams plateforme mobile.

* Graph autorisations ne sont pas nécessaires pour qu’un utilisateur lance un appel d’égal à égal avec votre bot. Des autorisations supplémentaires sont nécessaires pour que votre bot participe à un appel multiparte ou pour que votre bot lance un appel d’égal à égal avec un utilisateur.
* Un appel peut commencer en tant que pair à pair et devenir un appel multiparte. Votre bot peut lancer des appels en plusieurs parties en invitant d’autres personnes, à condition que votre bot dispose des autorisations appropriées. Si votre bot n’est pas autorisé à participer à des appels de groupe et si un participant ajoute un autre participant à l’appel, votre bot est supprimé de l’appel.

### <a name="signals"></a>Signaux

Il existe deux types de signaux: l’appel entrant et l’appel entrant. Voici les différentes fonctionnalités des signaux :

* Pour recevoir un appel entrant, vous entrez un point de terminaison dans les paramètres de votre bot. Ce point de terminaison reçoit une notification lorsqu’un appel entrant est lancé. Vous pouvez répondre à l’appel, le rejeter ou le rediriger vers quelqu’un d’autre.

    ![Gestion des appels](~/assets/images/calls-and-meetings/call-handling.png)

* Lorsqu’un bot est dans un appel, il existe des API pour désactiver et désactiver le bot et pour démarrer ou arrêter le partage de contenu vidéo ou de bureau avec d’autres participants.
* Le bot peut également accéder à la liste des participants, inviter de nouveaux participants et les désactiver.

### <a name="calls-and-online-meetings"></a>Appels et réunions en ligne

Du point de vue de l’utilisateur Teams, il existe deux types de réunions en ligne, ad hoc et planifiées. Du point de vue d’un bot, les deux réunions en ligne sont identiques. Pour un bot, une réunion en ligne est un appel multiparte entre un ensemble de participants et inclut des coordonnées de réunion. Les coordonnées de réunion sont les métadonnées de la réunion, y compris `botId`, `chatId` associées à la réunion, `joinUrl``startTime` ou `endTime`, et ainsi de suite.

### <a name="real-time-media"></a>Média en temps réel

Lorsqu’un bot participe à un appel ou à une réunion en ligne, il doit gérer les flux audio et vidéo. Lorsque les utilisateurs parlent lors d’un appel, s’affichent sur une webcam, ou présentent leurs écrans dans une réunion, à un bot, il est affiché sous forme de flux audio et vidéo. Si un bot veut dire quelque chose d’aussi simple que, **appuyez sur 0 pour atteindre l’opérateur** dans un scénario de réponse vocale interactive (IVR), il faut lire un . Fichier WAV. Collectivement, il s’agit de médias ou de médias en temps réel.

Les médias en temps réel font référence à des scénarios dans lesquels les supports doivent être traités en temps réel, par opposition à la lecture d’audio ou de vidéo précédemment enregistrés. La gestion des flux multimédias, en particulier des flux multimédias en temps réel, est extrêmement complexe. Microsoft a créé la plateforme multimédia en temps réel pour gérer ces scénarios et décharger autant que possible la charge lourde traditionnelle du traitement multimédia en temps réel. Lorsque le bot répond à un appel entrant ou rejoint un appel nouveau ou existant, il doit indiquer à la plateforme multimédia en temps réel comment le média est géré. Si vous créez une application IVR, vous pouvez décharger le traitement audio coûteux vers Microsoft. Sinon, si votre bot nécessite un accès direct aux flux multimédias, ce scénario est également pris en charge. Il existe deux types de traitement multimédia :

* **Média hébergé par le service** : les bots se concentrent sur la gestion du flux de travail d’application, comme le routage des appels et le déchargement du traitement audio vers la plateforme multimédia en temps réel Microsoft. Avec les médias hébergés par le service, vous avez plusieurs options pour implémenter et héberger votre bot. Un bot média hébergé par le service peut être implémenté en tant que service sans état, car il ne traite pas les médias localement. Les bots multimédias hébergés par le service peuvent utiliser les API suivantes :

  * `PlayPrompt` pour lire un clip audio.
  * `Record` pour l’enregistrement de clips audio.
  * `SubscribeToTone` pour s’abonner à des tonalités d’une fréquence multiple à deux tonalités (DTMF).

    Par exemple, savoir quand un utilisateur a appuyé sur **0** pour atteindre l’opérateur.

* **Média hébergé par** l’application : pour qu’un bot obtienne un accès direct au média, il a besoin d’une autorisation de Graph spécifique. Une fois que votre bot a l’autorisation, la [bibliothèque multimédia en temps réel](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/) et le [kit de développement logiciel (SDK) d’appel Graph](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/articles/index.html#graph-calling-sdk-and-stateful-client-builder) vous aident à créer des médias riches en temps réel et à appeler des bots. Un bot hébergé par l’application doit être hébergé dans un environnement Windows. Pour plus d’informations, consultez les [bots multimédias hébergés par l’application](./requirements-considerations-application-hosted-media-bots.md).

## <a name="code-sample"></a>Exemple de code

| **Exemple de nom** | **Description** | **Graph** |
|---------------|----------|--------|
| communication Graph | Graph les communications pour interagir avec la plateforme de communications de Microsoft. | [View](https://github.com/microsoftgraph/microsoft-graph-comms-samples) |

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Appels et réunions avec les médias en temps réel](~/bots/calls-and-meetings/real-time-media-concepts.md)

## <a name="see-also"></a>Voir aussi

* [API Graph référence](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)
* [Exemple d’applications](https://github.com/microsoftgraph/microsoft-graph-comms-samples)
* [Inscription d’un bot qui prend en charge les appels et les réunions en ligne](./registering-calling-bot.md)
* [Graph autorisations pour les bots d’appels et de réunions en ligne](./registering-calling-bot.md#add-graph-permissions)
* [Comment développer des bots d’appel et de réunion en ligne sur votre ordinateur](./debugging-local-testing-calling-meeting-bots.md)
* [Exigences et considérations relatives aux bots multimédias hébergés par l’application](./requirements-considerations-application-hosted-media-bots.md)
* [Informations techniques sur la gestion des notifications d’appel entrant](./call-notifications.md)
* [Configurer un standard automatique](/microsoftteams/create-a-phone-system-auto-attendant)
* [Configurer la réponse automatique pour Salles Microsoft Teams sur les appareils Android et Teams les téléphones vidéo](/microsoftteams/set-up-auto-answer-on-teams-android)
* [Teams stratégie d’enregistrement](/MicrosoftTeams/teams-recording-policy)