---
title: Bots d’appels et de réunions en ligne
description: Découvrez comment vos applications Microsoft Teams peuvent interagir avec les utilisateurs à l’aide de la voix et de la vidéo à l’aide d’API Microsoft Graph pour les appels et les réunions en ligne, et en savoir plus sur les flux multimédias en temps réel
ms.topic: conceptual
ms.localizationpriority: medium
keywords: appel d’appels audio vidéo IVR voice online réunions en temps réel flux multimédia bot
ms.openlocfilehash: 98dd4e329abec3e1b84ae9230d299a2e9d50fd8b
ms.sourcegitcommit: 430bf416bb8d1b74f926c8b5d5ffd3dbb0782286
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/10/2022
ms.locfileid: "65297169"
---
# <a name="calls-and-online-meetings-bots"></a>Bots d’appels et de réunions en ligne

Les bots peuvent interagir avec les appels et réunions Teams à l’aide de la voix, de la vidéo et du partage d’écran en temps réel. Avec [Microsoft Graph API pour les appels et les réunions en ligne](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true), les applications Teams peuvent désormais interagir avec les utilisateurs à l’aide de la voix et de la vidéo pour améliorer l’expérience. Ces API vous permettent d’ajouter les nouvelles fonctionnalités suivantes :

* Réponse vocale interactive (IVR).
* Contrôle d’appel.
* Accès aux flux audio et vidéo en temps réel, y compris le partage de bureau et d’application.

Pour utiliser ces API Graph dans une application Teams, vous créez un bot et spécifiez des informations et des autorisations supplémentaires.

En outre, la plateforme multimédia en temps réel permet aux bots d’interagir avec les appels et réunions Teams à l’aide de la voix, de la vidéo et du partage d’écran en temps réel. Un bot qui participe à des appels audio ou vidéo et à des réunions en ligne est un bot Microsoft Teams standard avec quelques fonctionnalités supplémentaires utilisées pour inscrire le bot.

Le manifeste de l’application Teams avec deux paramètres supplémentaires `supportsCalling` et `supportsVideo`, les autorisations Graph pour l’ID d’application Microsoft de votre bot et le consentement de l’administrateur client vous permettent d’inscrire le bot. Lors de l’inscription d’un bot d’appels et de réunions pour Teams, l’URL du webhook est mentionnée, qui est le point de terminaison webhook pour tous les appels entrants à votre bot. Un bot multimédia hébergé par une application nécessite la bibliothèque Microsoft.Graph.Communications.Calls.Media .NET pour accéder aux flux multimédias audio et vidéo, et le bot doit être déployé sur une machine Windows Server ou un système d’exploitation invité Windows Server dans Azure. Bots sur Teams prend uniquement en charge un ensemble spécifique de formats multimédias pour le contenu audio et vidéo.

À présent, vous devez comprendre certains concepts fondamentaux, la terminologie et les conventions.

## <a name="terminologies"></a>Terminologies

Les concepts, la terminologie et les conventions de base suivants vous guident dans l’utilisation des appels et des bots de réunion en ligne :

* Appels audio ou vidéo
* Types d’appel
* Signaux
* Appels et réunions en ligne
* Média en temps réel

### <a name="audio-or-video-calls"></a>Appels audio ou vidéo

Les appels dans Teams peuvent être purement audio ou audio et vidéo. Au lieu d’un appel audio ou vidéo, le terme appel est utilisé.

### <a name="call-types"></a>Types d’appel

Les appels sont d’égal à égal entre une personne et votre bot, ou multipartie entre votre bot et deux personnes ou plus dans un appel de groupe.

:::image type="content" source="~/assets/images/calls-and-meetings/call-types.png" alt-text="Types d’appels"border="true":::

Voici les différents types d’appels et autorisations requis pour l’appel :

* Un utilisateur peut lancer un appel pair à pair avec votre bot ou inviter votre bot dans un appel multipartie existant. L’appel multipartie n’est pas encore activé dans l’interface utilisateur Teams.

    > [!NOTE]
    > Les appels lancés par l’utilisateur à un bot ne sont actuellement pas pris en charge sur la plateforme mobile Microsoft Teams.

* Les autorisations Graph ne sont pas nécessaires pour qu’un utilisateur lance un appel d’égal à égal avec votre bot. Des autorisations supplémentaires sont nécessaires pour que votre bot participe à un appel en plusieurs parties ou pour que votre bot lance un appel pair à pair avec un utilisateur.
* Un appel peut commencer comme pair à pair et devenir un appel multipartie. Votre bot peut lancer des appels en plusieurs parties en invitant d’autres personnes, à condition que votre bot dispose des autorisations appropriées. Si votre bot ne dispose pas des autorisations nécessaires pour participer aux appels de groupe et si un participant ajoute un autre participant à l’appel, votre bot est supprimé de l’appel.

### <a name="signals"></a>Signaux

Il existe deux types de signaux : l’appel entrant et l’appel. Voici les différentes fonctionnalités des signaux :

* Pour recevoir un appel entrant, entrez un point de terminaison dans les paramètres de votre bot. Ce point de terminaison reçoit une notification lorsqu’un appel entrant est lancé. Vous pouvez répondre à l’appel, le rejeter ou le rediriger vers une autre personne.

     :::image type="content" source="~/assets/images/calls-and-meetings/call-handling.png" alt-text="Gestion des appels"border="true":::

* Lorsqu’un bot est dans un appel, il existe des API permettant de désactiver ou de désactiver le son du bot, ainsi que de démarrer ou d’arrêter le partage de contenu vidéo ou de bureau avec d’autres participants.
* Le bot peut également accéder à la liste des participants, inviter de nouveaux participants et les désactiver.

### <a name="calls-and-online-meetings"></a>Appels et réunions en ligne

Du point de vue d’un utilisateur Teams, il existe deux types de réunions en ligne, ad hoc et planifiées. Du point de vue d’un bot, les deux réunions en ligne sont les mêmes. Pour un bot, une réunion en ligne est un appel multipartie entre un ensemble de participants et inclut des coordonnées de réunion. Les coordonnées de réunion sont les métadonnées de la réunion, notamment `botId`, `chatId` associées à la réunion, `joinUrl`, `startTime` ou `endTime`, etc.

### <a name="real-time-media"></a>Média en temps réel

Lorsqu’un bot participe à un appel ou à une réunion en ligne, il doit gérer les flux audio et vidéo. Lorsque les utilisateurs parlent lors d’un appel, s’affichent sur une webcam ou présentent leurs écrans dans une réunion, un bot s’affiche sous forme de flux audio et vidéo. Si un bot souhaite dire quelque chose d’aussi simple que, **appuyez sur 0 pour atteindre l’opérateur** dans un scénario de réponse vocale interactive (IVR), il nécessite de lire un . Fichier WAV. Collectivement, il s’agit d’un média ou d’un média en temps réel.

Le média en temps réel fait référence à des scénarios dans lesquels le média doit être traité en temps réel, par opposition à la lecture de contenu audio ou vidéo enregistré précédemment. La gestion des flux multimédias, en particulier les flux multimédias en temps réel, est extrêmement complexe. Microsoft a créé la plateforme multimédia en temps réel pour gérer ces scénarios et décharger autant que possible le traitement multimédia en temps réel. Lorsque le bot répond à un appel entrant ou rejoint un appel nouveau ou existant, il doit indiquer à la plateforme multimédia en temps réel comment les médias sont gérés. Si vous créez une application IVR, vous pouvez décharger le traitement audio coûteux vers Microsoft. Sinon, si votre bot nécessite un accès direct aux flux multimédias, ce scénario est également pris en charge. Il existe deux types de traitement multimédia :

* **Média hébergé par le service** : les bots se concentrent sur la gestion du flux de travail d’application, comme le routage des appels et le déchargement du traitement audio vers la plateforme multimédia en temps réel Microsoft. Avec les médias hébergés par le service, vous disposez de plusieurs options pour implémenter et héberger votre bot. Un bot média hébergé par le service peut être implémenté en tant que service sans état, car il ne traite pas les médias localement. Les bots multimédias hébergés par le service peuvent utiliser les API suivantes :

  * `PlayPrompt` pour lire un clip audio.
  * `Record` pour l’enregistrement de clips audio.
  * `SubscribeToTone` pour s’abonner à des tonalités d’une fréquence multiple à deux tonalités (DTMF).

    Par exemple, savoir quand un utilisateur a appuyé sur **0** pour atteindre l’opérateur.

* **Média hébergé par l’application**: pour qu’un bot obtienne un accès direct au média, il a besoin d’une autorisation de Graph spécifique. Une fois que votre bot a l’autorisation, la [bibliothèque multimédia en temps réel](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/) et le [kit de développement logiciel (SDK) d’appel Graph](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/articles/index.html#graph-calling-sdk-and-stateful-client-builder) vous aident à créer des médias riches en temps réel et à appeler des bots. Un bot hébergé par l’application doit être hébergé dans un environnement Windows. Pour plus d’informations, consultez [bots multimédias hébergés par l’application](./requirements-considerations-application-hosted-media-bots.md).

## <a name="code-sample"></a>Exemple de code

| **Exemple de nom** | **Description** | **Graph** |
|---------------|----------|--------|
| Communication graphique | Affichez les communications pour interagir avec la plateforme de communication de Microsoft. | [View](https://github.com/microsoftgraph/microsoft-graph-comms-samples) |

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Appels et réunions avec les médias en temps réel](~/bots/calls-and-meetings/real-time-media-concepts.md)

## <a name="see-also"></a>Voir aussi

* [Référence de l’API Microsoft Graph](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)
* [Exemple d’applications](https://github.com/microsoftgraph/microsoft-graph-comms-samples)
* [Inscription d’un bot qui prend en charge les appels et les réunions en ligne](./registering-calling-bot.md)
* [Autorisations Graph pour les bots d’appels et de réunions en ligne](./registering-calling-bot.md#add-graph-permissions)
* [Comment développer des bots d’appel et de réunion en ligne sur votre ordinateur](./debugging-local-testing-calling-meeting-bots.md)
* [Exigences et considérations relatives aux bots multimédias hébergés par l’application](./requirements-considerations-application-hosted-media-bots.md)
* [Informations techniques sur la gestion des notifications d’appel entrant](./call-notifications.md)
* [Configurer un standard automatique](/microsoftteams/create-a-phone-system-auto-attendant)
* [Configurer la réponse automatique pour les salles Microsoft Teams sur les appareils mobiles vidéo Android et Teams](/microsoftteams/set-up-auto-answer-on-teams-android)
* [Stratégie d’enregistrement Teams](/MicrosoftTeams/teams-recording-policy)
* [Utilisation de l’API de communication dans Microsoft Graph](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)
