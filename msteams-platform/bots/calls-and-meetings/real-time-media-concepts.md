---
title: Appels multimédias en temps réel et réunions en ligne avec Microsoft Teams
description: Comprendre les concepts clés dans la création d’un bot qui peut mener des appels audio et vidéo en temps réel et des réunions en ligne.
ms.topic: conceptual
localization_priority: Normal
keywords: audio stream video stream audio/video calling meeting real-time media application-hosted media service-hosted media-hosted media
ms.openlocfilehash: 23a4573c39968f3b5c53badc32fd80ecc4dc889087dd8d98253be9d46555919c
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/07/2021
ms.locfileid: "57709544"
---
# <a name="real-time-media-calls-and-meetings-with-microsoft-teams"></a>Appels et réunions multimédias en temps réel avec Microsoft Teams

La plateforme Real-time Media permet aux bots d’interagir avec Microsoft Teams appels et réunions à l’aide de la voix en temps réel, de la vidéo et du partage d’écran. La plateforme Real-time Media est une fonctionnalité avancée qui permet au bot d’envoyer et de recevoir du contenu vocal et vidéo image par image. Le bot dispose d’un accès brut aux flux multimédias vocaux, vidéo et de partage d’écran. Il existe des robots multimédias hébergés par un service plus simples qui s’appuient sur la plateforme multimédia en temps réel pour tout le traitement multimédia. Les bots qui traitéent les médias eux-mêmes sont appelés bots multimédias hébergés par l’application.

Par exemple, dans un appel 1:1 avec un bot, lorsque l’utilisateur parle, le bot reçoit 50 images audio par seconde. Le bot reçoit des trames audio avec chaque image de 20 millisecondes (ms) d’audio. Un bot multimédia hébergé par l’application peut faire la reconnaissance vocale en temps réel à mesure que les trames audio sont reçues. Il n’est pas nécessaire d’attendre un enregistrement une fois que l’utilisateur a cessé de parler. Le bot peut également envoyer et recevoir des vidéos haute résolution, y compris du contenu de partage d’écran vidéo.

La plateforme fournit une API simple de socket permettant au bot d’envoyer et de recevoir du média. Il gère le codage et le décodage en temps réel des paquets audio ou vidéo. Il utilise des codecs tels que LARE ET G.722 pour l’audio et H.264 pour la vidéo. La plateforme gère également le chiffrement ou le déchiffrement de tous les paquets multimédias et la transmission réseau de paquets. Le bot n’est concerné que par le contenu audio ou vidéo réel. Un bot multimédia en temps réel participe à des appels et des réunions en temps réel avec plusieurs participants.

## <a name="media-session"></a>Session multimédia

Un bot multimédia en temps réel doit déclarer les modalités qu’il doit prendre en charge. Le bot multimédia en temps réel doit déclarer la prise en charge lorsqu’il répond à un appel entrant ou rejoint une Teams réunion. Pour chaque modalité prise en charge, le bot déclare s’il peut envoyer et recevoir du média, recevoir uniquement ou envoyer uniquement. Par exemple, un bot conçu pour gérer les appels Teams 1:1 nécessite d’envoyer et de recevoir du contenu audio. Toutefois, le bot doit uniquement envoyer de la vidéo, car il n’a pas besoin de recevoir la vidéo de l’appelant. L’ensemble des modalités audio et vidéo établies entre le bot et l’appelant Teams réunion est appelé session multimédia.

Deux types de modalités vidéo sont pris en charge: le partage d’écran vidéo principal et vidéo. La vidéo principale est utilisée pour transporter la vidéo à partir de la webcam d’un utilisateur. Le partage d’écran vidéo permet à un utilisateur de partager l’écran. La plateforme permet à un bot d’envoyer et de recevoir les deux types de vidéos.

Lorsqu’il rejoint une réunion Teams, un bot peut recevoir plusieurs flux de vidéos principaux simultanément jusqu’à 10 par session multimédia. Le bot peut voir plusieurs participants à la réunion.

La section suivante fournit des détails sur l’envoi et la réception de médias par le bot sous la mesure d’une séquence d’images.

## <a name="frames-and-frame-rate"></a>Trames et fréquence d’images

Un bot multimédia en temps réel interagit directement avec les modalités audio et vidéo d’une session multimédia. Le bot envoie et reçoit du contenu multimédia sous la mesure d’une séquence d’images et chaque image est une unité de contenu. Une seconde de l’audio est transmise sous la mesure d’une séquence de 50 images. Chaque image contient 20 ms qui est 1/50e de seconde de contenu de reconnaissance vocale. Une seconde de vidéo est transmise en tant que séquence de 30 images fixes. Chaque image est destinée à être vue pendant 33,3 ms, soit 1/30e de seconde avant la trame vidéo suivante. Le nombre d’images transmises ou rendues par seconde est appelé fréquence d’images.

La section suivante fournit des détails sur le format audio et vidéo utilisé dans les appels et réunions multimédias en temps réel.

## <a name="audio-and-video-format"></a>Format audio et vidéo

Au format audio, chaque seconde de l’audio est représentée sous forme de 16 000 échantillons, chaque échantillon contenant 16 bits de données. Un cadre audio de 20 ms contient 320 échantillons de 640 octets de données.

Dans le format vidéo, plusieurs formats sont pris en charge. Deux propriétés clés d’un format vidéo sont sa taille d’image et son format de couleur. Les tailles d’images pris en charge incluent 640 x 360 pixels, 1280 x 720 pixels et 1920 x 1080 pixels. Les formats de couleur pris en charge incluent NV12 qui est de 12 bits par pixel et RVB24 qui est de 24 bits par pixel.

Une image vidéo de 720 p contient 921 600 pixels, soit 1 280 fois 720. Au format de couleur RVB24, chaque pixel est représenté sous la forme de 3 octets de 24 bits, dont 1 octet chacun des composants de couleur rouge, vert et bleu. Une seule image vidéo RVB24 de 720 p nécessite 2 764 800 octets de données, soit 921 600 pixels et 3 octets par pixel. À une fréquence d’images variable, l’envoi de trames vidéo RVB24 de 720 p implique le traitement d’environ 80 mégaoctets par seconde de contenu. 80 mégaoctets sont considérablement compressés par le codec vidéo H.264 avant la transmission réseau.

Une fonctionnalité avancée de la plateforme permet à un bot d’envoyer ou de recevoir des vidéos sous forme d’images H.264 codées. Les bots qui fournissent leur propre encodeur ou décodeur H.264 sont pris en charge, ou le flux vidéo décodé en bitmaps RGB24 ou NV12 brutes n’est pas requis.

La section suivante fournit des détails sur les participants à la réunion qui sont des haut-parleurs actifs et dominants.

## <a name="active-and-dominant-speakers"></a>Haut-parleurs actifs et dominants

Lorsqu’il est Teams à une réunion composée de plusieurs participants, un bot peut identifier les participants à la réunion qui parlent actuellement. Les haut-parleurs actifs identifient les participants qui sont entendus dans chaque trame audio reçue. Les haut-parleurs dominants identifient les participants les plus actifs ou les plus dominants dans la conversation de groupe, bien que leur voix ne soit pas entendu dans chaque trame audio. L’ensemble des haut-parleurs dominants peut changer à mesure que différents participants parlent à tour de rôle.

La section suivante fournit des détails sur les demandes d’abonnement vidéo réalisées par un bot.

## <a name="video-subscription"></a>Abonnement vidéo

Dans un appel 1:1, le bot reçoit automatiquement la vidéo de l’appelant si le bot est activé pour recevoir la vidéo. Dans une Teams, le bot doit indiquer à la plateforme les participants qu’il souhaite voir. Un abonnement vidéo est une demande du bot pour recevoir le contenu vidéo ou de partage d’écran principal d’un participant. Lorsque les participants à la réunion effectuent leur conversation, le bot modifie ses abonnements vidéo requis. Le bot modifie les abonnements vidéo en fonction des mises à jour du jeu de haut-parleurs dominants ou des notifications qui indiquent quel participant partage actuellement l’écran.

La section suivante fournit des détails sur ce que vous devez installer et les conditions requises pour développer un bot multimédia hébergé par l’application.

## <a name="developer-resources"></a>Ressources pour les développeurs

Pour développer un bot multimédia hébergé par l’application, vous devez installer [Microsoft.Graph. La bibliothèque Calls.Media .NET NuGet](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/) package dans votre Visual Studio projet.

Les bots multimédias hébergés par l’application nécessitent .NET ou C# et Windows Server. Pour plus d’informations, voir [les exigences et les considérations relatives aux bots multimédias hébergés par l’application.](requirements-considerations-application-hosted-media-bots.md#c-or-net-and-windows-server-for-development)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Enregistrer un bot appelant](~/bots/calls-and-meetings/registering-calling-bot.md)
