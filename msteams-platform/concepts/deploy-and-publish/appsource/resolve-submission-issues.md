---
title: Résoudre les problèmes avec la soumission de votre magasin
description: Comprendre comment résoudre les problèmes et corriger les problèmes avec votre Microsoft Teams soumission du magasin.
ms.topic: how-to
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: 23c751d7a9fec96de128521f660213a559534283
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565108"
---
# <a name="resolve-issues-if-your-microsoft-teams-store-submission-fails"></a>Résoudre les problèmes si votre soumission Microsoft Teams magasin échoue

Les applications publiées dans le magasin Microsoft Teams doivent respecter les lignes directrices [de validation Teams de magasin et](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) les politiques du marché [commercial.](/legal/marketplace/certification-policies)

En cas d’échec de votre soumission en magasin, Microsoft fournit un service de validation de conciergerie pour aider à rendre votre application conforme et publiée.

## <a name="get-help-directly-from-microsoft"></a>Obtenez de l’aide directement de Microsoft

Le service de validation de conciergerie fourni par Microsoft aide les développeurs à faire publier leurs applications Teams magasin. Dans le cadre de ce service, Microsoft vérifie si votre application fonctionne comme décrit, contient toutes les métadonnées appropriées et apporte de la valeur aux utilisateurs.

En cas d’échec de votre application, Microsoft vous envoie un rapport d’examen avec des recommandations dans les 24 heures suivant la soumission.

## <a name="resolve-issues-and-resubmit-your-app"></a>Résoudre les problèmes et soumettre à nouveau votre application

Vous devez résoudre tous les problèmes signalés par l’équipe de validation microsoft concierge avant de soumettre à nouveau votre application sur Partner Center. Le rapport Microsoft contient les informations suivantes :

* Une ligne [directrice de validation correspondante](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) pour chaque numéro.
* Instructions sur la façon de reproduire chaque numéro.
* Recommandations résoudre chaque problème en fonction de la documentation des développeurs accessible au public.

Le processus de résolution des problèmes et de soumettre à nouveau une application va généralement comme ceci:

1. Vous réparez tous les problèmes dans le rapport.
1. Vous envoyez ce qui suit à l’équipe de validation concierge Microsoft <a href="mailto:teamsubm@microsoft.com">à teamsubm@microsoft.com</a>:
   * Un package d’application mis à jour
   * Testez les notes de votre application, si vous ne les avez pas inclus dans votre soumission originale :
      * Informations d’identification pour au moins deux comptes (un administrateur et un non-administrateur).
      * Instructions pour configurer l’application et tester ses fonctionnalités.
      * Une vidéo montrant votre application utilisée dans Teams.
1. L’équipe de validation de conciergerie Microsoft teste entièrement votre application mise à jour.
1. Vous faites l’un des éléments suivants :
   * Si votre application est exempte de problèmes, soumettre à nouveau votre application sur Partner Center.
   * Si les problèmes ne sont pas résolus ou microsoft trouve de nouveaux problèmes, vous recevez un autre rapport sur ce qu’il doit corriger. Résoudre ces problèmes et envoyer une version mise à jour de l’application <a href="mailto:teamsubm@microsoft.com">à teamsubm@microsoft.com</a>.

> [!CAUTION]
> Pour éviter plusieurs échecs de soumission, ne soumettre pas à nouveau votre application sur Partner Center tant que l’équipe de validation du concierge Microsoft n’a pas approuvé votre application.

## <a name="faq"></a>FAQ

Obtenez des réponses à certaines questions courantes lorsque vous résolvez des problèmes de soumission d’applications.

<br>

<details>

<summary><b>Combien de temps faudra-t-il pour publier mon application ?</b></summary>

Si la soumission de votre magasin n’a aucun problème, votre application publiera dans les 1-2 jours ouvrables. En cas d’échec de votre application, une équipe de Microsoft vous fournit des recommandations pour résoudre les problèmes. Une fois que vous avez fait ces correctifs et renvoyer une application mise à jour à cette équipe, vous serez informé dans les 24 heures si votre application est prête à publier ou a encore besoin de plus de travail.

<br>

</details>

<details>

<summary><b>Comment puis-je augmenter la probabilité que mon application passe la soumission ?</b></summary>

Faire ce qui suit peut mener à une soumission réussie :

1. Développez votre application en fonction des lignes [directrices Teams conception de l’entreprise.](~/concepts/design/design-teams-app-overview.md)
1. Assurez-vous que votre application respecte les directives [de validation Teams magasin et les](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) politiques de certification du marché commercial [Microsoft](/legal/marketplace/certification-policies).
1. Testez votre package d’application avec [l’outil Microsoft Teams validation d’application .](https://dev.teams.microsoft.com/appvalidation.html)
1. [Préparez votre soumission Teams magasin.](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)

<br>

</details>

<details>

<summary><b>Mon application est en test bêta. Puis-je soumettre mon application de toute façon pour gagner du temps sur le processus de publication ?</b></summary>

Non. Microsoft ne valide que les applications prêtes à la production.

<br>

</details>

<details>

<summary><b>Puis-je contacter le teamsubm@microsoft.com e-mail avant de soumettre mon application pour la première fois sur Partner Center ?</b></summary>

Non. Microsoft ne commence pas à valider votre application tant que vous n’avez pas soumis votre application pour la première fois sur Partner Center.

<br>

</details>

<details>

<summary><b>J’ai reçu un e-mail de Partner Center disant que mon application a été approuvée pour publier. Pourquoi mon application n’est-elle pas dans Teams magasin ?</b></summary>

Une fois que votre application est approuvée, la publication prend généralement de 1 à 2 jours ouvrables en fonction des capacités de l’application.Si votre application n’a pas été publiée après deux jours ouvrables, <a href="mailto:teamsubm@microsoft.com">contactez teamsubm@microsoft.com</a>.

<br>

</details>
