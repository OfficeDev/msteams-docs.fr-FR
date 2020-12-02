---
title: Appels et robots de réunions en ligne
description: Découvrez comment vos applications Microsoft teams peuvent interagir avec les utilisateurs à l’aide de la voix et de la vidéo à l’aide des API Microsoft Graph pour les appels et les réunions en ligne.
keywords: appel des appels vocaux audio de vidéo
ms.openlocfilehash: fa31bc55221befab1ac1b6b77e116f3fc2e1a935
ms.sourcegitcommit: bfdcd122b6b4ffc52d92320d4741f870c07f0542
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/02/2020
ms.locfileid: "49552429"
---
# <a name="calls-and-online-meetings-bots"></a>Appels et robots de réunions en ligne

> [!NOTE]
> La prise en charge des appels et des robots de réunions en ligne n’est actuellement pas prise en charge sur la plateforme Microsoft teams mobile. 

Avec l’ajout d' [API Microsoft Graph pour les appels et les réunions en ligne](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true), les applications Microsoft teams peuvent désormais interagir avec les utilisateurs de façon enrichie à l’aide de la voix et de la vidéo. Ces API vous permettent d’ajouter de nouvelles fonctionnalités telles que la réponse vocale interactive (IVR), le contrôle d’appel et l’accès à des flux audio et/ou vidéo en temps réel pour les appels et les réunions, y compris le partage de bureau et d’application.

Pour utiliser ces API Microsoft Graph dans une application Microsoft Teams, vous devez créer un bot et spécifier des informations et des autorisations supplémentaires que nous décrirons ailleurs, mais tout d’abord, il est important de comprendre certains concepts de base, terminologie et conventions :

* **Appels audio/vidéo.** Les appels dans teams peuvent être purement audio ou audio + vidéo. Par souci de concision, nous n’disons pas « appel audio/vidéo » partout ; Nous appelons simplement « Call ».
* **Types d’appels.** Les appels sont égal à égal (entre une personne et votre bot) ou à plusieurs (votre bot et deux personnes ou plus dans un appel de groupe).
  ![CallingTypes ](~/assets/images/calls-and-meetings/call-types.png) :
  * Un utilisateur peut initier un appel d’égal à égal avec votre bot ou invitez votre robot à un appel multipartie existant (bien que ce dernier n’ait pas encore été activé dans l’interface utilisateur de Microsoft Teams).
  * Les autorisations Microsoft Graph ne sont pas nécessaires pour qu’un utilisateur initie un appel P2P avec votre bot, mais des autorisations supplémentaires sont nécessaires pour que votre bot participe à un appel à plusieurs ou pour que votre bot entame un appel P2P avec un utilisateur.
  * Un appel peut commencer en tant qu’égal à égal et faire remonter à plusieurs. Votre robot peut lancer cette escalade en invitant d’autres personnes, à condition que votre robot dispose des autorisations appropriées. Si votre bot ne dispose pas des autorisations nécessaires pour participer à des appels de groupe et qu’un participant ajoute une autre partie, votre robot est abandonné de l’appel.
* **Signalisation.** Il existe deux types de signaux : les appels entrants et in-Call :
  * Pour recevoir un appel entrant, vous spécifiez un point de terminaison dans vos paramètres de robot ; ce point de terminaison reçoit une notification lorsqu’un appel entrant arrive. Vous pouvez répondre à l’appel, le refuser ou le rediriger vers un autre emplacement ou vers une autre personne.
  ![Types d’appels](~/assets/images/calls-and-meetings/call-handling.png)
  * Lorsqu’un bot est en cours d’appel, il existe des API pour activer et désactiver la fonctionnalité automatique et démarrer/arrêter le partage de contenu vidéo/de bureau avec les autres participants.
  * Le bot peut également accéder à la liste des participants, inviter de nouveaux participants et les désactiver.
* **Appels et réunions en ligne.** Du point de vue d’un utilisateur Teams, il existe deux types de réunions en ligne, ad hoc et planifiées. Toutefois, du point de vue du robot, les deux sont les mêmes. Pour un bot, une réunion en ligne n’est qu’un appel à plusieurs (l’ensemble des participants) plus des « coordonnées de réunion », que vous pouvez considérer comme les métadonnées de la réunion : `botId` , `chatId` associé à la réunion,, `joinUrl` `startTime` / `endTime` , et bien plus encore.
* **Contenu multimédia en temps réel.** Lorsqu’un bot participe à un appel ou une réunion en ligne, il doit traiter les flux audio et vidéo. Lorsque les utilisateurs discutent sur un appel, s’affichent eux-mêmes sur une webcam ou présentent leurs écrans dans une réunion, un bot le « voit » comme des flux audio et/ou vidéo. Si un bot souhaite dire un ou un contenu d’écran, cela nécessite un flux audio ou vidéo. Même un peu comme le robot disant « Appuyez sur 0 pour atteindre l’opérateur » dans un scénario de réponse vocale interactive signifie lire un. Fichier WAV. Collectivement, nous faisons référence à ceci _en tant que média ou_ _multimédia en temps réel_ (lorsque vous faites référence à des scénarios dans lesquels les médias doivent être traités en temps réel, par opposition à la lecture de données audio/vidéo précédemment enregistrées). Historiquement, le traitement des flux multimédias, en particulier les flux multimédia en temps réel, a été extrêmement complexe pour les développeurs. Microsoft a créé la _plateforme multimédia en temps réel_ pour gérer ces cas d’utilisation et décharger autant que possible le traitement de média en temps réel le plus traditionnel.  Quand le bot répond à un appel entrant ou rejoint un nouvel appel ou un appel existant, il doit indiquer à la plateforme Real-time Media comment les médias seront traités. Si vous créez une application IVR, vous pouvez décharger le traitement audio onéreux à Microsoft. Par ailleurs, si votre bot nécessite un accès direct aux flux multimédias, nous en prenons le scénario. Il existe deux types de traitement multimédia :
  * **Support hébergé par le service.** Les robots se concentrent sur la gestion des flux de travail d’application (par exemple, acheminement des appels) et déchargent le traitement audio vers la plateforme multimédia en temps réel Microsoft. Avec le support hébergé par le service, vous disposez de plusieurs options pour implémenter et héberger votre robot. Un robot multimédia hébergé par un service peut être implémenté en tant que service sans État, car il ne traite pas les médias localement. Les robots multimédias hébergés par le service peuvent utiliser des API telles que la `PlayPrompt` lecture d’un clip audio, `Record` l’enregistrement de clips audio ou `SubscribeToTone` l’abonnement à des tonalités DTMF (par exemple, savoir quand un utilisateur a appuyé sur la touche 0 pour atteindre l’opérateur).
  * **Médias hébergés par l’application.** Pour qu’un bot accède directement au média, il a besoin d’une autorisation graphique spécifique, mais une fois que votre robot en dispose, la [bibliothèque multimédia en temps réel](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/) et le [Kit de développement logiciel (SDK) appelant Graph](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/articles/index.html#graph-calling-sdk-and-stateful-client-builder) vous aident à créer des médias riches et en temps réel, en appelant des bots. Un bot hébergé sur une application doit être hébergé dans un environnement Windows, comme décrit plus en détail [ici](./requirements-considerations-application-hosted-media-bots.md).

## <a name="further-reading"></a>Autres lectures

Voici plus d’informations sur la façon de créer et de tester les appels et les robots de réunions en ligne :

* [Référence de l’API Graph](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)
* [Exemple d’applications](https://github.com/microsoftgraph/microsoft-graph-comms-samples)
* [Inscription d’un bot qui prend en charge les appels et les réunions en ligne](./registering-calling-bot.md) et les [autorisations Microsoft Graph pour les appels et les robots de réunions en ligne](./registering-calling-bot.md#add-microsoft-graph-permissions)
* [Comment développer des robots d’appels et de réunions en ligne sur votre PC local](./debugging-local-testing-calling-meeting-bots.md)
* [Plus d’informations sur le traitement multimédia en temps réel](./real-time-media-concepts.md)et sur [les besoins de prise en charge des médias hébergés](./requirements-considerations-application-hosted-media-bots.md) par l’application
* [Informations techniques sur le traitement des notifications d’appel entrant](./call-notifications.md)
