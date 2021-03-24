---
title: Appels et bots de réunions en ligne
description: Découvrez comment vos applications Microsoft Teams peuvent interagir avec les utilisateurs à l’aide de la voix et de la vidéo à l’aide des API Microsoft Graph pour les appels et les réunions en ligne.
keywords: appel d’appels de réunions vocales (IVR) audio en ligne
ms.openlocfilehash: 0fcf420ba8d698404d00bb2cab3d61cab2245f40
ms.sourcegitcommit: 49d1ecda14042bf3f368b14c1971618fe979b914
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/23/2021
ms.locfileid: "51034641"
---
# <a name="calls-and-online-meetings-bots"></a>Appels et bots de réunions en ligne

Avec l’ajout d’API Microsoft Graph pour les appels et les réunions en ligne, les applications Microsoft Teams peuvent désormais interagir avec les [utilisateurs](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)de manière enrichie à l’aide de la voix et de la vidéo. Ces API vous permettent d’ajouter de nouvelles fonctionnalités telles que la réponse vocale interactive (IVR), le contrôle d’appel et l’accès aux flux audio et/ou vidéo en temps réel pour les appels et les réunions, y compris le partage de bureau et d’application.

Pour utiliser ces API Microsoft Graph dans une application Microsoft Teams, vous créez un bot et spécifiez des informations et autorisations supplémentaires que nous allons décrire ailleurs, mais tout d’abord, il est important de comprendre certains concepts de base, terminologie et conventions :

* **Appels audio/vidéo.** Les appels dans Teams peuvent être purement audio ou audio+vidéo. Par souci de concision, nous ne dites pas « appel audio/vidéo » partout ; nous venons de dire « appel ».
* **Types d’appel.** Les appels sont pair à pair (entre une personne et votre bot) ou à plusieurs (votre bot et plusieurs personnes dans un appel de groupe).
  ![CallingTypes ](~/assets/images/calls-and-meetings/call-types.png) :
  * Un utilisateur peut lancer un appel d’égal à égal avec votre bot ou inviter votre bot à un appel à plusieurs existant (bien que ce dernier ne soit pas encore activé dans l’interface utilisateur de Microsoft Teams).
  
  > [!NOTE]
  > Les appels initiés par l’utilisateur à un bot ne sont actuellement pas pris en charge sur la plateforme mobile Microsoft Teams. 
  
  * Les autorisations Microsoft Graph ne sont pas nécessaires pour qu’un utilisateur lance un appel d’égal à égal avec votre bot, mais des autorisations supplémentaires sont nécessaires pour que votre bot participe à un appel à plusieurs ou pour que votre bot lance un appel d’égal à égal avec un utilisateur.
  * Un appel peut commencer comme pair à pair et s’escalader à plusieurs. Votre bot peut initier cette escalade en invitant d’autres personnes, à condition que votre bot dispose des autorisations adéquates. Si votre bot n’est pas autorisé à participer à des appels de groupe et qu’un participant ajoute une autre personne, votre bot est supprimé de l’appel.
* **Signalisation.** Il existe deux types de signaux : l’appel entrant et l’appel entrant :
  * Pour recevoir un appel entrant, vous spécifiez un point de terminaison dans les paramètres de votre bot . ce point de terminaison reçoit une notification lorsqu’un appel entrant arrive. Vous pouvez répondre à l’appel, le rejeter ou le rediriger vers un endroit ou une autre personne.
  ![Types d’appel](~/assets/images/calls-and-meetings/call-handling.png)
  * Lorsqu’un bot est dans un appel, il existe des API pour activer et désactiver lui-même le son et pour démarrer/arrêter le partage de contenu vidéo/de bureau avec les autres participants.
  * Le bot peut également accéder à la liste des participants, inviter de nouveaux participants et les désactiver.
* **Appels et réunions en ligne.** Du point de vue d’un utilisateur Teams, il existe deux types de réunions en ligne : ad hoc et programmées. Toutefois, du point de vue d’un bot, les deux sont identiques. Pour un bot, une réunion en ligne est simplement un appel à plusieurs (ensemble de participants) plus « coordonnées de réunion », que vous pouvez voir comme les métadonnées de la réunion : , associées à la réunion, et bien plus `botId` `chatId` `joinUrl` `startTime` / `endTime` encore.
* **Médias en temps réel.** Lorsqu’un bot participe à un appel ou à une réunion en ligne, il doit gérer les flux audio et vidéo. Lorsque les utilisateurs parlent lors d’un appel, s’affichent sur une webcam ou présentent leurs écrans lors d’une réunion, un bot « voit » cela comme des flux audio et/ou vidéo. Si un bot souhaite dire quelque chose ou présenter du contenu d’écran, cela nécessite un flux audio ou vidéo. Même quelque chose d’aussi simple que le bot qui dit « appuyer sur 0 pour atteindre l’opérateur » dans un scénario de réponse vocale interactive (IVR) implique la lecture d’un . Fichier WAV. Collectivement, il s’agit de médias ou de médias en temps réel (lorsqu’il s’agit de scénarios où les médias doivent être traitées en temps réel, par opposition à la lecture d’audio/vidéo précédemment enregistrées).   Historiquement, la gestion des flux multimédias, en particulier des flux multimédias en temps réel, était extrêmement complexe pour les développeurs. Microsoft a créé la _plateforme Multimédia_ en temps réel pour gérer ces cas d’utilisation et pour décharger autant que possible les « charges importantes » traditionnelles du traitement multimédia en temps réel.  Quand le bot répond à un appel entrant ou rejoint un nouvel appel ou un appel existant, il doit indiquer à la plateforme Real-time Media comment les médias seront traités. Si vous construisez une application de réponse vocale, vous pouvez décharger le traitement audio coûteux à Microsoft. Par contre, si votre bot nécessite un accès direct aux flux multimédias, nous 2016 000 000 000. Il existe les deux types de traitement multimédia :
  * **Média hébergé par le service.** Les bots se concentrent sur la gestion du flux de travail d’application (par exemple, les appels de routage) et déchargent le traitement audio sur la plateforme Microsoft Real-time Media. Avec les médias hébergés par le service, vous avez plusieurs options pour implémenter et héberger votre bot. Un bot multimédia hébergé par le service peut être implémenté en tant que service sans état, car il ne traitera pas les médias localement. Les robots multimédias hébergés par le service peuvent utiliser des API telles que la lecture d’un clip audio, l’enregistrement de clips audio ou l’abonnement à des `PlayPrompt` `Record` `SubscribeToTone` tonalités DTMF (par exemple, savoir quand un utilisateur a appuyer sur 0 pour atteindre l’opérateur).
  * **Support hébergé par l’application.** Pour qu’un bot obtienne un accès direct aux médias, il a besoin [](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/) d’une autorisation Graph spécifique, mais une fois que votre bot l’a, la bibliothèque de médias en temps réel et le [SDK Graph Calling](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/articles/index.html#graph-calling-sdk-and-stateful-client-builder) vous aident à créer des médias enrichis en temps réel, appelant des bots. Un bot hébergé par l’application doit être hébergé dans un environnement Windows, comme décrit plus en détail [ici.](./requirements-considerations-application-hosted-media-bots.md)

## <a name="further-reading"></a>Lecture supplémentaire

Voici plus d’informations sur la création et le test d’appels et de bots de réunions en ligne :

* [Référence de l’API Graph](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)
* [Exemple d’applications](https://github.com/microsoftgraph/microsoft-graph-comms-samples)
* [Inscription d’un bot qui prend en charge les appels](./registering-calling-bot.md) et les réunions en ligne et les autorisations Microsoft Graph pour les appels et les [bots de réunions en ligne](./registering-calling-bot.md#add-microsoft-graph-permissions)
* [Comment développer des bots d’appels et de réunions en ligne sur votre PC local](./debugging-local-testing-calling-meeting-bots.md)
* [Plus d’informations sur le traitement multimédia](./real-time-media-concepts.md)en temps réel et les informations nécessaires pour prendre en charge les médias [hébergés par l’application](./requirements-considerations-application-hosted-media-bots.md)
* [Informations techniques sur la gestion des notifications d’appels entrants](./call-notifications.md)
