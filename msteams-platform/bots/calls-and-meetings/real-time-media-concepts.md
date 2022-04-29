---
title: Appels multimédias en temps réel et réunions en ligne avec Microsoft Teams
description: Comprendre les concepts clés de la création d’un bot qui peut effectuer des appels audio et vidéo en temps réel et des réunions en ligne. En savoir plus sur les sessions multimédias, la fréquence d’images, le format audio/vidéo et la référence aux ressources du développeur
ms.topic: conceptual
ms.localizationpriority: high
keywords: diffusion audio vidéo en continu audio/vidéo appelant un média en temps réel hébergé par une application multimédia hébergée par un service multimédia
ms.openlocfilehash: 0e5343567be3843c457885fcf506446b20b6dcf7
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111989"
---
# <a name="real-time-media-calls-and-meetings-with-microsoft-teams"></a>Appels et réunions multimédias en temps réel avec Microsoft Teams

La plateforme multimédia en temps réel permet aux bots d’interagir avec les appels et réunions Microsoft Teams à l’aide de la voix, de la vidéo et du partage d’écran en temps réel. La plateforme multimédia en temps réel est une fonctionnalité avancée qui permet au bot d’envoyer et de recevoir des images de contenu audio et vidéo par image. Le bot dispose d’un accès brut aux flux multimédias de partage de la voix, de la vidéo et de l’écran. Il existe des bots multimédias hébergés par un service plus simples qui s’appuient sur la plateforme multimédia en temps réel pour tout le traitement multimédia. Les bots qui traitent eux-mêmes les médias sont appelés bots multimédias hébergés par l’application.

Par exemple, dans un appel 1:1 avec un bot, au fur et à mesure que l’utilisateur parle, le bot reçoit 50 trames audio par seconde. Le bot reçoit des trames audio avec chaque trame de 20 millisecondes (ms) d’audio. Un bot multimédia hébergé par une application peut effectuer une reconnaissance vocale en temps réel à mesure que les trames audio sont reçues. Il n’est pas nécessaire d’attendre un enregistrement une fois que l’utilisateur a cessé de parler. Le bot peut également envoyer et recevoir des vidéos haute définition, y compris du contenu de partage d’écran vidéo.

La plateforme fournit une API de type socket simple permettant au bot d’envoyer et de recevoir du contenu multimédia. Il gère l’encodage et le décodage en temps réel des paquets audio ou vidéo. Il utilise des codecs tels que SILK et G.722 pour l’audio et H.264 pour la vidéo. La plateforme gère également tout chiffrement de paquet multimédia, ainsi que le déchiffrement et la transmission réseau de paquets. Le bot s’intéresse uniquement au contenu audio ou vidéo réel. Un bot multimédia en temps réel participe à des appels et réunions 1:1 avec plusieurs participants.

## <a name="media-session"></a>Session multimédia

Un bot multimédia en temps réel doit déclarer les modalités qu’il doit prendre en charge. Le bot multimédia en temps réel doit déclarer la prise en charge lorsqu’il répond à un appel entrant ou participe à une réunion Teams. Pour chaque modalité prise en charge, le bot déclare s’il peut envoyer et recevoir du contenu multimédia, recevoir uniquement ou envoyer uniquement. Par exemple, un bot conçu pour gérer les appels Teams 1:1 nécessite à la fois l’envoi et la réception d’audio. Toutefois, le bot doit envoyer uniquement la vidéo, car il n’a pas besoin de recevoir la vidéo de l’appelant. L’ensemble des modalités audio et vidéo établies entre le bot et l’appelant ou la réunion Teams est appelé session multimédia.

Deux types de modalités vidéo sont pris en charge : le partage d’écran vidéo principal et le partage d’écran vidéo. La vidéo principale est utilisée pour transporter la vidéo à partir de la webcam d’un utilisateur. Le partage d’écran vidéo permet à un utilisateur de partager l’écran. La plateforme permet à un bot d’envoyer et de recevoir les deux types de vidéos.

Lorsqu’il est joint à une réunion Teams, un bot peut recevoir simultanément plusieurs flux de vidéos principaux jusqu’à 10 par session multimédia. Le bot peut voir plusieurs participants à la réunion.

La section suivante fournit des détails sur le bot qui envoie et reçoit des médias sous la forme d’une séquence d’images.

## <a name="frames-and-frame-rate"></a>Trames et fréquence d’images

Un bot multimédia en temps réel interagit directement avec les modalités audio et vidéo d’une session multimédia. Le bot envoie et reçoit du contenu multimédia sous la forme d’une séquence d’images et chaque image est une unité de contenu. Une seconde d’audio est transmise sous la forme d’une séquence de 50 images. Chaque image contient 20 ms, soit 1/50e de seconde de contenu vocal. Une seconde de vidéo est transmise sous la forme d’une séquence de 30 images fixes. Chaque image est destinée à être affichée pendant seulement 33,3 ms, soit 1/30 de seconde avant la trame vidéo suivante. Le nombre d’images transmises ou rendues par seconde est appelé fréquence d’images.

La section suivante fournit des détails sur le format audio et vidéo utilisé dans les appels et réunions multimédias en temps réel.

## <a name="audio-and-video-format"></a>Format audio et vidéo

Au format audio, chaque seconde d’audio est représentée sous la forme de 16 000 échantillons, chaque échantillon contenant 16 bits de données. Une trame audio de 20 ms contient 320 exemples qui représentent 640 octets de données.

Au format vidéo, plusieurs formats sont pris en charge. La taille du cadre et le format de couleur sont deux propriétés clés d’un format vidéo. Les tailles de trame prises en charge incluent 640 x 360 pixels, 1280 x 720 pixels et 1920 x 1080 pixels. Les formats de couleur pris en charge incluent NV12 qui est de 12 bits par pixel et RVB24 de 24 bits par pixel.

Une image vidéo de 720 p contient 921 600 pixels, soit 1280 fois 720. Dans le format de couleur RVB24, chaque pixel est représenté sous la forme de 3 octets de 24 bits, dont 1 octet chacun des composants de couleur rouge, vert et bleu. Une image vidéo RVB24 de 720p requiert 2 764 800 octets de données, soit 921 600 pixels fois 3 octets par pixel. À une fréquence d’images variable, l’envoi de trames vidéo RVB24 de 720p implique le traitement d’environ 80 mégaoctets par seconde de contenu. 80 mégaoctets sont considérablement compressés par le codec vidéo H.264 avant la transmission réseau.

Une fonctionnalité avancée de la plateforme permet à un bot d’envoyer ou de recevoir des vidéos sous forme d’images H.264 encodées. Les bots qui fournissent leur propre encodeur ou décodeur H.264 sont pris en charge, ou le flux vidéo décodé en bitmaps RVB24 ou NV12 bruts n’est pas nécessaire.

La section suivante fournit des détails sur les participants à la réunion qui parlent et qui sont des orateurs actifs et dominants.

## <a name="active-and-dominant-speakers"></a>Orateurs actifs et dominants

Lorsqu’il est joint à une réunion Teams composée de plusieurs participants, un bot peut identifier les participants à la réunion qui parlent actuellement. Les haut-parleurs actifs identifient les participants qui sont entendus dans chaque trame audio reçue. Les orateurs dominants identifient les participants les plus actifs ou les plus dominants dans la conversation de groupe, même si leur voix n’est pas entendu dans chaque trame audio. L’ensemble des orateurs dominants peut changer à mesure que différents participants prennent la parole à tour de rôle.

La section suivante fournit des détails sur les demandes d’abonnement vidéo effectuées par un bot.

## <a name="video-subscription"></a>Abonnement vidéo

Dans un appel 1:1, le bot reçoit automatiquement la vidéo de l’appelant si le bot est activé pour recevoir la vidéo. Dans une réunion Teams, le bot doit indiquer à la plateforme les participants qu’il souhaite voir. Un abonnement vidéo est une demande du bot pour recevoir le contenu vidéo ou de partage d’écran principal d’un participant. Lorsque les participants à la réunion mènent leur conversation, le bot modifie ses abonnements vidéo requis. Le bot modifie les abonnements vidéo en fonction des mises à jour du jeu d’orateurs dominants ou des notifications qui indiquent quel participant partage actuellement l’écran.

La section suivante fournit des détails sur ce que vous devez installer et la configuration requise pour développer un bot multimédia hébergé par une application.

## <a name="developer-resources"></a>Ressources du développeur

Pour développer un bot multimédia hébergé par une application, vous devez installer le paquet NuGet de la bibliothèque [Microsoft.Graph.Calls.Media .NET](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/) dans votre projet Visual Studio.

Les bots multimédias hébergés par l’application nécessitent .NET ou C# et Windows Server. Pour plus d'informations, voir [les exigences et les considérations relatives aux robots médias hébergés par des applications](requirements-considerations-application-hosted-media-bots.md#c-or-net-and-windows-server-for-development).

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Enregistrer un bot appelant](~/bots/calls-and-meetings/registering-calling-bot.md)

## <a name="see-also"></a>Voir aussi

[Formats multimédias pris en charge pour les bots](~/resources/media-formats.md)
