---
title: Comprendre les cas d’utilisation de votre application
author: heath-hamilton
description: Lorsque vous planifiez votre Microsoft Teams, vous devez d’abord comprendre les problèmes que votre application tente de résoudre.
ms.topic: conceptual
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 6669492c25cb3701f5c937b3f99e39d411fbc4a4
ms.sourcegitcommit: 306b6e8cb3aac8bfda10ef3999467a797d64539d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/20/2021
ms.locfileid: "58408543"
---
# <a name="understand-your-use-cases"></a>Comprendre vos cas d’utilisation

La plateforme Microsoft Teams offre une grande variété de points d’entrée et d’éléments d’interface [utilisateur](../../concepts/extensibility-points.md) dont votre application peut tirer parti.
> [!NOTE]
> Avant de commencer à créer vos cas d’utilisation, vous devez bien comprendre les fonctionnalités de Teams et ce qui est possible sur la plateforme Teams les utiliser.

Chaque méthode d’interaction avec vos utilisateurs a ses forces et ses faiblesses. Créer une application Teams consiste à trouver la combinaison idéale pour répondre aux besoins de vos utilisateurs. Si vous souhaitez répondre à ces besoins, vous devez d’abord les comprendre.

## <a name="understand-the-problem"></a>Comprendre le problème

Chaque bonne application présente un problème principal ou un besoin qu’elle tente de résoudre. Avant de commencer à créer une application, vous devez expliquer ce qu’est ce problème. Dans son cœur, Teams est une plateforme de collaboration, de sorte que les applications qui permettent de combler les lacunes dans l’obtention d’une collaboration efficace sont parfaitement adaptées. Il s’agit également d’une plateforme sociale, d’une plateforme trans-plateforme native, qui se trouve au cœur de Office 365 et qui offre une zone de dessin personnelle pour vous aider à créer des applications. Dans cette plateforme sociale, il existe un large éventail de besoins qui peuvent être résolus avec une application Teams client. Vous pouvez résoudre un large éventail de problèmes, à condition que vous compreniez celui que vous essayez de résoudre. Avant de commencer à créer une application, posez-vous des questions pertinentes, telles que :

* Quels sont les avantages et les inconvénients du système d’état actuel utilisé par vos utilisateurs ?
* Quels sont les problèmes que vos utilisateurs rencontrent aujourd’hui et que vous souhaitez résoudre ?
* Quelles fonctionnalités ou fonctionnalités vos utilisateurs aiment et aiment dans leur façon actuelle de faire le processus ?

## <a name="understand-your-user"></a>Comprendre votre utilisateur

Comprendre qui est votre utilisateur et vous pouvez identifier le bon modèle de distribution, mais plus important encore, cela vous aide à identifier la façon dont les utilisateurs utilisent Teams. Posez des questions pertinentes, telles que :

* Les utilisateurs sont-ils principalement des employés de première ligne sur des clients mobiles ?
* Prévoyez-vous qu’un grand nombre d’utilisateurs invités ont besoin d’accéder à votre application ?
* Utilisent-ils des équipes et des canaux ou principalement des conversations de groupe ?
* Quelle est la technique de vos utilisateurs principaux ?
* Avez-vous besoin d’une expérience d’intégration complète ou de quelques pointeurs ?

Parfois, la réponse est que nous voulons résoudre ce problème pour tous *Teams utilisateurs partout.* Si c’est le cas pour vous, passez du temps à comprendre ce qu’il [faut pour être publié sur AppSource](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md).

## <a name="understand-the-limitations-of-the-app"></a>Comprendre les limitations de l’application

La connaissance des limitations des applications en termes d’accessibilité des données et de résidence des données vous aidera à concevoir de meilleures applications. Ceci est important, car le fait d’avoir des informations sur les personnes qui possèdent les données et la disponibilité des API a une incidence sur l’architecture de la solution. Là encore, posez-vous des questions pertinentes, telles que :

* Quels sont les défis liés à l’intégration back end de l’application actuelle ?
* Qui possède les données du back end ? Interne ou tiers.
* Existe-t-il des pare-feu qui ont un impact sur le fonctionnement de l’application ?
* Existe-t-il des API pour accéder aux données dont vous avez besoin pour le fonctionnement de votre application ? 

## <a name="provide-authentication"></a>Fournir l’authentification

Vous devez déterminer dès le début si vous devez protéger les services que vous exposez et à quel niveau. N’oubliez pas que les services web exposés dans votre application Teams sont disponibles publiquement sur Internet. Par contre, si vous devez les sécuriser, commencez à y penser maintenant. Si vous avez besoin d’une solution qui nécessite que vous fournissiez l’accès invité pour les utilisateurs en dehors du client, des restrictions et des autorisations d’accès doivent être placées pour protéger les informations confidentielles. Vous devrez concevoir des applications en raison des limitations qui s’appliquent à l’accès des utilisateurs invités. Par conséquent, posez-vous des questions, telles que : 

* Les utilisateurs accèderont-ils à différentes vues des données en fonction de leurs rôles ?
* Y a-t-il des pii impliquées ?
* Les interactions seront-ils également basées sur les rôles d’utilisateur ?
* Les utilisateurs externes accèderont-ils à l’application ?

## <a name="decide-what-goes-in-teams"></a>Décider de ce qui se passe Teams

Que vous construisiez quelque chose de nouveau ou que vous insérait une solution existante dans Teams, il est important de décider si l’ensemble de l’application sera à l’intérieur du client Teams client. Vérifiez s’il est logique de n’apporter qu’une partie de l’expérience. Avec une combinaison d’onglets, d’extensions de messagerie, de modules de tâche, de cartes adaptatives et de bots conversationnels, vous pouvez créer des applications complexes entièrement Teams.
N’oubliez pas qui sont vos utilisateurs et le problème que vous essayez de résoudre. Ont-ils déjà un système pour résoudre la plupart du problème ou vous devez simplement étendre un sous-ensemble de fonctionnalités dans Teams ? En règle générale, si vous comptez apporter une partie de votre solution, vous devez vous concentrer sur le partage, la collaboration, l’initiative et la surveillance des flux de travail.

## <a name="plan-the-onboarding-experience"></a>Planifier l’expérience d’intégration

Votre expérience d’intégration peut être la différence entre la réussite ou l’échec de votre application. Pour chaque fonctionnalité de votre application et chaque contexte dans lequel cette fonctionnalité peut être installée, vous devez avoir un plan pour vous présenter. La façon dont vous introduisez votre bot de conversation lorsqu’il est installé dans un canal avec un millier de personnes est différente lorsqu’il est installé dans une conversation un-à-un. Que se passe-t-il lorsqu’un utilisateur configure votre onglet pour la première fois dans un canal ? Si vous partagez des cartes avec une extension de messagerie, est-il logique d’ajouter un petit lien vers une **page** En savoir plus pour présenter aux utilisateurs ce que votre application peut faire d’autre ?

Le fait de savoir qui sont vos utilisateurs vous aide à créer l’expérience la plus agréable. Pensez-vous que la plupart des personnes ont déjà un contexte sur l’objectif de votre application ou qu’ils ont déjà utilisé vos services dans un autre contexte ? Est-ce qu’ils arrivent dans votre application sans connaissances préalables ? Concevoir votre expérience d’intégration avec vos utilisateurs clés à l’esprit.

N’oubliez pas que les utilisateurs peuvent découvrir votre application de différentes manières. Ils peuvent être ceux qui l’installent ou ils peuvent être introduits dans votre application lorsqu’un autre utilisateur l’utilise pour partager du contenu. Si vous souhaitez que davantage d’utilisateurs utilisent votre application, vous devez rechercher des moyens de vous présenter à tout le monde.

Par-dessus tout, n’oubliez pas que personne n’aime le courrier indésirable. L’explosion de messages personnels et de canaux est un bon moyen de ne pas être installé rapidement !

## <a name="plan-for-the-future"></a>Planifier l’avenir

Identifiez les nouvelles fonctionnalités que l’utilisateur préférera dans la solution actuelle. Si vous disposez d’une feuille de route pour l’ajout de nouvelles fonctionnalités à l’application, la conception et l’architecture seront impactées.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Ma cartographier vos cas d’utilisation](../../concepts/design/map-use-cases.md)
