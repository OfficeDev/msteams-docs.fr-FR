---
title: Comprendre vos cas d’utilisation
author: clearab
description: Décider de la façon de distribuer votre application
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: ef1007c21e79cd69155b64f02d2980bcf6a708b9
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673863"
---
# <a name="understand-your-use-cases"></a>Comprendre vos cas d’utilisation

La plateforme Microsoft teams offre un grand nombre de [points d’extensibilité et d’éléments d’interface](~/concepts/extensibility-points.md) dont votre application peut tirer parti. Si vous n’avez pas déjà une bonne compréhension de ce qui est possible sur la plateforme Teams, vous devez tout d’abord lire cet article.

Chaque méthode d’interaction avec vos utilisateurs a ses propres points forts et faiblesses. La création d’une application Isard teams consiste à trouver la bonne combinaison pour répondre aux besoins de vos utilisateurs. Si vous envisagez de répondre à ces besoins, vous devez d’abord les comprendre.

## <a name="what-problem-are-you-trying-to-solve"></a>Quel problème essayez-vous de résoudre ?

Chaque application correcte a un problème principal (ou besoin) qu’elle tente de résoudre avant de commencer à créer vous devez expliquer ce qu’est le problème. En fait, teams est une plateforme de collaboration qui permet aux applications de résoudre les problèmes de collaboration. Il s’agit également d’une plateforme de mise en réseau, qui est en mode natif, se trouve au cœur d’Office 365 et offre une toile personnelle pour vous permettant de créer des applications. Il existe de nombreux besoins pouvant être résolus à l’aide d’une application Teams, mais assurez-vous que vous comprenez celui que vous tentez de résoudre.

## <a name="who-are-you-solving-it-for"></a>Qui vous le résolvez ?

Parfois, ceci peut être évident : « le système de surveillance de mon équipe a besoin d’envoyer des alertes quelque part, nous devons pouvoir les discuter vraiment rapidement, et aucun d’entre nous ne souhaitera consulter notre courrier électronique ». Parfois, votre public cible peut croître au fil du temps : « notre équipe sœur est en réalité Jealous de notre système d’alerte, et cela veut qu’elle se trouve sur l’action. » La compréhension des personnes qui vous aideront à identifier le modèle de distribution correct, mais plus important, vous aidera à identifier la *façon dont ils utilisent teams*. Sont-ils principalement des travailleurs frontaux sur des clients mobiles ? Prévoyez-vous que de nombreux utilisateurs invités ont besoin d’accéder à votre application ? Utilisent-ils des équipes et des canaux, ou principalement des conversations de groupe ? Quels sont les techniques sophistiquées techniquement élaborées ? Aurez-vous besoin d’une expérience d’intégration complète ou d’un petit nombre de pointeurs ?

Parfois, la réponse est « nous voulons résoudre ce problème pour tous les utilisateurs de l’équipe ». Si c’est le cas, vous voudrez consacrer un certain temps à comprendre [ce qu’il faut faire pour publier sur AppSource](~/concepts/deploy-and-publish/appsource/prepare/overview.md).

## <a name="do-you-need-authentication"></a>Avez-vous besoin d’une authentification ?

Vous devez identifier à l’avance si vous devez protéger les services que vous exposez, et à quel niveau. Rappelez-vous que les services Web que vous exposez dans votre application de teams sont accessibles au public sur Internet, de sorte que si vous avez besoin de les sécuriser pour commencer à réfléchir à la mise à disposition.

## <a name="should-the-entire-app-be-in-teams"></a>L’application entière doit-elle être dans teams ?

Qu’il s’agisse de créer un élément entièrement nouveau ou d’intégrer une solution existante dans Teams, il est important de déterminer si l’application entière doit être à l’intérieur du client teams ou s’il est logique de n’apporter qu’une partie de l’expérience. Avec une combinaison d’onglets, d’extensions de messagerie, de modules de tâches, de cartes interactives et de robots de conversation, vous pouvez créer des applications complexes entièrement à l’intérieur de teams. Toutefois, cela n’est pas toujours judicieux. Rappelez-vous des utilisateurs et le problème que vous tentez de résoudre. Dispose-t-elle déjà d’un système pour résoudre la plus grande partie du problème, et vous avez simplement besoin d’étendre un sous-ensemble de la fonctionnalité à teams ? En règle générale, si vous envisagez de mettre en place une partie de votre solution, vous devez vous concentrer sur les flux de travail de partage, de collaboration et de démarrage et de surveillance.

## <a name="what-will-the-onboarding-experience-be-like"></a>Qu’est-ce que l’expérience d’intégration ?

Votre expérience d’intégration peut être la différence entre la réussite ou l’échec de votre application. Pour chaque fonctionnalité de votre application, et pour chaque contexte dans lequel cette fonctionnalité peut être installée, vous devez planifier la façon dont vous allez vous présenter. La manière dont vous présentez votre robot de conversation lorsqu’il est installé dans un canal avec un millier de personnes sera probablement différente de celle dans le cadre d’une conversation un-à-un. Que se passe-t-il lorsqu’un utilisateur configure d’abord votre onglet dans un canal ? Si vous partagez des cartes avec une extension de messagerie, est-il logique de pouvoir ajouter un petit lien vers une page « en savoir plus » afin de présenter aux utilisateurs les autres possibilités de votre application ?

Connaître les personnes qui vous aideront à concevoir la bonne expérience. Prévoyez-vous que la plupart des utilisateurs ont déjà un contexte de ce à quoi votre application est destinée, ou si vous avez déjà utilisé vos services dans un autre contexte ? Ou est-ce qu’ils accèdent à votre application sans connaissances préalables ? Élaborez votre expérience d’intégration avec vos utilisateurs clés.

Rappelez-vous également que les utilisateurs peuvent découvrir votre application de différentes manières : ils peuvent être ceux qui l’installent, ou ils peuvent être introduits dans votre application lorsqu’un autre membre de l’équipe l’utilise pour partager du contenu. Si vous souhaitez que votre application se propage, vous devez rechercher les moyens de vous présenter à tout le monde.

Au-dessus de tout le monde, n’oubliez pas que personne n’aime le courrier indésirable L’annulation avec les messages personnels et de canal constitue un moyen efficace de s’installer rapidement.

## <a name="next-steps"></a>Étapes suivantes

* [Mapper vos cas d’utilisation sur la fonctionnalité](~/concepts/design/map-use-cases.md)
* [Choisir le mode de distribution de votre application](~/concepts/deploy-and-publish/apps-publish.md)

## <a name="learn-more"></a>En savoir plus

* [Concevoir des onglets efficaces](~/tabs/design/tabs.md)
* [Créer des robots étonnants](~/bots/design/bots.md)

