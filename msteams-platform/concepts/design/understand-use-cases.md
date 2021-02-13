---
title: Comprendre vos cas d’utilisation
author: clearab
description: Comprendre vos cas d’utilisation
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 270771ecc47bbfc03a33d1603f680bc3424989ad
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231616"
---
# <a name="understand-your-use-cases"></a>Comprendre vos cas d’utilisation

La plateforme Microsoft Teams offre une grande variété de [points d’extensibilité](~/concepts/extensibility-points.md) et d’éléments d’interface utilisateur dont votre application peut tirer parti. Si vous ne savez pas déjà ce qui est possible sur la plateforme Teams, vous devez d’abord lire cet article.

Chaque méthode d’interaction avec vos utilisateurs possède ses propres forces et faiblesses. La création d’une application Teams formidable consiste à trouver la combinaison qui répond aux besoins de vos utilisateurs. Si vous souhaitez répondre à ces besoins, vous devez d’abord les comprendre.

## <a name="what-problem-are-you-trying-to-solve"></a>Quel problème essayez-vous de résoudre ?

Chaque bonne application présente un problème principal (ou un besoin) qu’elle tente de résoudre . Avant de commencer à créer, vous devez expliquer ce qu’est ce problème. Teams est une plateforme de collaboration, de sorte que les applications qui cherchent à résoudre les problèmes de collaboration sont parfaitement adaptées. Il s’agit également d’une plateforme sociale, d’une plateforme trans-plateforme native, qui se trouve au cœur d’Office 365 et qui offre un canevas personnel dans le but de créer des applications. Il existe un très grand nombre de besoins qui peuvent être résolus avec une application Teams, assurez-vous simplement de bien comprendre celui que vous essayez de résoudre.

## <a name="who-are-you-solving-it-for"></a>Pour qui la résoudre ?

Parfois, cela peut être évident : « Le système de surveillance de mon équipe doit envoyer des alertes quelque part, nous devons être en mesure d’en parler très rapidement, et aucun d’entre nous ne souhaite consulter notre courrier électronique. » Parfois, votre public cible peut s’accroître au fil du temps : « Notre équipe de l’équipe est vraiment enthousiaste de notre système d’alertes, et maintenant, elle veut agir. » Comprendre qui sont vos utilisateurs vous aidera à identifier le bon modèle de distribution, mais plus important encore vous aidera à identifier la façon dont *ils utilisent Teams.* S’agit-il principalement de travailleurs de première ligne sur des clients mobiles ? Prévoyez-vous qu’un grand nombre d’utilisateurs invités ont besoin d’accéder à votre application ? Utilisent-ils des équipes et des canaux, ou principalement des conversations de groupe ? Comment sont-elles techniquement sophistiquées ? Aurez-vous besoin d’une expérience complète d’embarquement ou de quelques pointeurs ?

Parfois, la réponse est « Nous voulons résoudre ce problème pour tous les utilisateurs de l’équipe partout ». Si c’est le cas pour vous, vous souhaiterez passer du temps à comprendre ce qu’il faut pour être [publié sur AppSource.](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)

## <a name="do-you-need-authentication"></a>Avez-vous besoin d’une authentification ?

Vous devez déterminer dès le début si vous devez protéger les services que vous exposez et à quel niveau. N’oubliez pas que les services web que vous allez exposer dans votre application Teams sont disponibles publiquement sur Internet, donc si vous devez les sécuriser, commencez à réfléchir à l’heure actuelle.

## <a name="should-the-entire-app-be-in-teams"></a>L’ensemble de l’application doit-il être dans Teams ?

Que vous construisiez un élément entièrement nouveau ou que vous insérait une solution existante dans Teams, il est important de décider si l’ensemble de l’application va se trouver dans le client Teams ou s’il est logique de n’apporter qu’une partie de l’expérience. Avec une combinaison d’onglets, d’extensions de messagerie, de modules de tâche, de cartes interactives et de bots conversationnels, vous pouvez créer des applications complexes entièrement à l’intérieur de Teams. Toutefois, cela n’a pas toujours de sens. N’oubliez pas qui sont vos utilisateurs et le problème que vous essayez de résoudre. Ont-ils déjà un système pour résoudre la plupart du problème et vous devez simplement étendre un sous-ensemble de fonctionnalités dans Teams ? En règle générale, si vous comptez uniquement apporter une partie de votre solution, vous devez vous concentrer sur le partage, la collaboration et l’initiateur et la surveillance des flux de travail.

## <a name="what-will-the-onboarding-experience-be-like"></a>À quoi ressemblera l’expérience d’intégration ?

Votre expérience d’intégration peut être la différence entre la réussite ou l’échec de votre application. Pour chaque fonctionnalité de votre application et pour chaque contexte dans lequel cette fonctionnalité peut être installée, vous devez avoir un plan pour vous présenter. La façon dont vous introduisez votre bot de conversation lorsqu’il est installé dans un canal avec un millier de personnes sera probablement différente de celle d’une conversation un-à-un. Que se passe-t-il lorsqu’un utilisateur configure votre onglet pour la première fois dans un canal ? Si vous partagez des cartes avec une extension de messagerie, est-il logique d’ajouter un petit lien vers une page « En savoir plus » pour présenter aux utilisateurs ce que votre application peut faire d’autre ?

Le fait de connaître vos utilisateurs vous aidera à créer la bonne expérience. Pensez-vous que la plupart des personnes ont déjà un contexte sur l’objectif de votre application ou qu’ils ont déjà utilisé vos services dans un autre contexte ? Ou sont-ils en cours d’accès à votre application sans connaissances préalables ? Concevoir votre expérience d’intégration avec vos utilisateurs clés à l’esprit.

N’oubliez pas également que les utilisateurs peuvent découvrir votre application de différentes manières : il peut s’agit de ceux qui l’installent, ou ils peuvent être introduits dans votre application lorsqu’un autre membre de l’équipe l’utilise pour partager du contenu. Si vous souhaitez que votre application se propage, vous devez rechercher des moyens de vous présenter à tout le monde.

Par-dessus tout, n’oubliez pas que personne n’aime le courrier indésirable. L’explosion de messages personnels et de canaux est un bon moyen de ne pas être installé rapidement !

## <a name="next-steps"></a>Étapes suivantes

* [Ma cartographier vos cas d’utilisation avec des fonctionnalités](~/concepts/design/map-use-cases.md)
* [Choisir comment distribuer votre application](../deploy-and-publish/overview.md)

## <a name="learn-more"></a>En savoir plus

* [Concevoir des onglets efficaces](~/tabs/design/tabs.md)
* [Créer des bots incroyables](~/bots/design/bots.md)

