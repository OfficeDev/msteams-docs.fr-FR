---
title: Appels multimédia en temps réel et réunions en ligne avec Microsoft teams
description: Découvrez les concepts clés de la génération de bot qui peuvent effectuer des appels audio et vidéo en temps réel et des réunions en ligne.
keywords: flux vidéo flux vidéo d’appel audio/vidéo en temps réel hébergé par une application multimédia hébergée par un service multimédia hébergé par une application multimédia
ms.openlocfilehash: 0ec99d1caa8810d292170c7c70a1518de7301873
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673701"
---
# <a name="real-time-media-calls-and-meetings-with-microsoft-teams"></a>Réunions et appels multimédia en temps réel avec Microsoft teams

La plateforme multimédia en temps réel permet aux robots d’interagir avec les appels et les réunions Microsoft teams à l’aide de la voix, de la vidéo et du partage d’écran en temps réel. Il s’agit d’une fonctionnalité avancée qui permet au bot d’envoyer et de recevoir des images de contenu audio et vidéo *par frame*. Le bot dispose d’un accès « brut » aux flux de médias vocaux, vidéo et de partage d’écran. (Les bots qui traitent les médias eux-mêmes sont appelés robots _multimédia hébergés_ par l’application, contrairement aux robots _multimédia hébergés_ par le service, qui reposent sur la plateforme multimédia en temps réel pour tout le traitement multimédia.)

Par exemple, dans un appel 1:1 avec un bot, comme l’utilisateur parle, le bot recevra 50 images audio par seconde, chaque image contenant 20 millisecondes (MS) d’audio. Un robot multimédia hébergé par l’application peut effectuer une reconnaissance vocale en temps réel au fur et à mesure que les images audio sont reçues, au lieu de devoir attendre un enregistrement une fois que l’utilisateur a cessé de parler. Le bot peut également envoyer et recevoir de la vidéo haute définition, y compris du contenu de partage d’écran vidéo.

La plateforme fournit une API de type Socket simple pour le robot pour l’envoi et la réception de médias, et gère le codage et le décodage en temps réel des paquets audio/vidéo à l’aide de codecs tels que la soie et G. 722 pour le son et H. 264 pour la vidéo. La plateforme gère également tous les paquets de chiffrement/déchiffrement et de transmission de paquets multimédias automatiquement, de sorte que le robot doit uniquement se préoccuper du contenu audio/vidéo réel. Un bot multimédia en temps réel peut participer à des appels 1:1, ainsi qu’à des réunions avec plusieurs participants.

Cet article présente les concepts clés relatifs à la création d’un bot qui peut effectuer des appels audio/vidéo en temps réel avec Microsoft Teams.

## <a name="media-session"></a>Session multimédia

Lorsqu’un bot multimédia en temps réel répond à un appel entrant ou rejoint une réunion Microsoft Teams, il doit déclarer les modalités qu’il envisage de prendre en charge. Pour chaque modalité prise en charge, le bot déclare s’il peut envoyer et recevoir des médias, recevoir uniquement ou envoyer uniquement. Par exemple, un bot conçu pour gérer les appels de 1:1 Teams peut souhaiter envoyer et recevoir de l’audio, mais uniquement *Envoyer* de la vidéo (car il n’a pas besoin de recevoir la vidéo de l’appelant). L’ensemble des modalités audio et vidéo établies entre le bot et l’appelant ou la réunion de teams est appelé **session multimédia**.

Deux types de modalités vidéo sont pris en charge : **le partage d’écran**vidéo **principal** et vidéo. La vidéo principale est utilisée pour transporter la vidéo à partir de la webcam d’un utilisateur. Le partage d’écran vidéo permet à un utilisateur de partager son écran en tant que flux vidéo. La plateforme permet à un bot d’envoyer et/ou de recevoir *les deux* types de vidéo.

Lorsqu’elle est jointe à une réunion Teams, un bot peut recevoir simultanément plusieurs flux vidéo, jusqu’à 10 par session multimédia. Cela permet au bot de « voir » plusieurs participants à la réunion.

## <a name="frames-and-frame-rate"></a>Images et fréquence d’images

Un bot multimédia en temps réel interagit directement avec les modalités audio et vidéo d’une session multimédia. Cela signifie que le bot envoie et/ou reçoit des médias sous la forme d’une séquence de **trames**, dans laquelle chaque image représente une unité de contenu. Une seconde de l’audio peut être transmise sous la forme d’une séquence de 50 trames, chaque image contenant 20 millisecondes (MS) (1/50e de seconde) de contenu de synthèse vocale. Une seconde partie de la vidéo peut être découpée en une séquence de 30 images fixes, chacune étant destinée à être affichée uniquement 33.3 ms (1/30 de seconde) avant l’affichage de l’image vidéo suivante. Le nombre de trames émises ou rendues par seconde est appelé la **fréquence d’images**. « 30fps » indique 30 images par seconde.

## <a name="audio-format"></a>Format audio

Chaque seconde de l’audio est représentée par des **exemples**16 000, chaque exemple contenant 16 bits de données. Une trame audio 20 ms contient 320 exemples (640 octets de données).

## <a name="video-format"></a>Format vidéo

Il existe plusieurs formats pris en charge pour la vidéo. Deux propriétés clés d’un format vidéo sont sa **taille d’image** et son **format de couleur**. Les tailles de cadre prises en charge sont 640x360 (« 360p »), 1280x720 (« 720p ») et 1920x1080 (« 1080p »). Les formats de couleurs pris en charge incluent NV12 (12 bits par pixel) et RGB24 (24 bits par pixel).

Une image vidéo « 720p » contient 921 600 pixels (1280 fois 720). Dans le format de couleur RGB24, chaque pixel est représenté par 3 octets (24 bits) constitués d’un octet, chacun des composants de couleur rouge, vert et bleu. Par conséquent, une image vidéo 720p RGB24 nécessite 2 764 800 octets de données (921 600 pixels à 3 octets/pixel). À une fréquence d’images de 30fps, l’envoi de trames vidéo 720p RGB24 signifie un traitement approximatif de 80 Mo/s de contenu (qui est largement compressé par le codec vidéo H. 264 avant la transmission réseau).

Une fonctionnalité avancée de la plateforme permet à un bot d’envoyer/recevoir des vidéos en tant que trames H. 264 **codées** . Cela prend en charge les robots qui fournissent leur propre codeur/décodeur H. 264, ou qui n’ont pas besoin du flux vidéo décodé dans des RGB24 brutes ou des bitmaps NV12.

## <a name="active-and-dominant-speakers"></a>Haut-parleurs actifs et dominant

Lorsqu’elle est jointe à une réunion teams composée de plusieurs participants, un bot peut identifier les participants à la réunion en cours de conversation. Les **haut-parleurs actifs** identifient les participants qui sont entendus dans chaque trame audio reçue. Les **haut-parleurs dominants** identifient les participants les plus actifs (ou « dominant ») dans la conversation de groupe, même si leur voix n’est pas audible dans chaque cadre audio. Le jeu de haut-parleurs dominant peut varier à mesure que les différents participants prennent la parole.

## <a name="video-subscription"></a>Abonnement vidéo

Dans un appel 1:1, le bot reçoit automatiquement la vidéo de l’appelant si le bot est activé pour recevoir la vidéo. Dans une réunion Teams, le bot doit indiquer à la plateforme que les participants qu’il souhaite voir. Un **abonnement vidéo** est une demande de la part du bot pour recevoir le contenu vidéo principal d’un participant ou un partage d’écran. Lorsque les participants à la réunion conduisent leur conversation, le bot peut modifier les abonnements vidéo souhaités en fonction des mises à jour du jeu de haut-parleurs dominant ou des notifications indiquant quel participant est en train de partager des écrans.

## <a name="developer-resources"></a>Ressources pour les développeurs

Pour développer un robot multimédia hébergé par une application, vous devez installer le package NuGet suivant dans votre projet Visual Studio :

- [Bibliothèque Microsoft. Graph. Calls. Media .NET](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/)

Les robots multimédias hébergés par l’application requièrent .NET/C# et Windows Server, comme décrit en détail dans [Requirements and Considerations for application-Hosted Media bots](requirements-considerations-application-hosted-media-bots.md#application-hosted-media-bot-development-requires-cnet-and-windows-server).
