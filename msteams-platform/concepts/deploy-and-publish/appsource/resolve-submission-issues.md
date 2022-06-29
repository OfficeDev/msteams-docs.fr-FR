---
title: Résoudre les problèmes liés à l’envoi de votre magasin
description: Dans cet article, découvrez comment résoudre et corriger les problèmes liés à la soumission de votre magasin Microsoft Teams.
ms.topic: how-to
author: heath-hamilton
ms.author: surbhigupta
ms.localizationpriority: medium
ms.openlocfilehash: 5faf2d3622e88febe9522f5e2df6716ec2680cca
ms.sourcegitcommit: ffc57e128f0ae21ad2144ced93db7c78a5ae25c4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/29/2022
ms.locfileid: "66503871"
---
# <a name="resolve-issues-if-your-teams-store-submission-fails"></a>Résoudre les problèmes en cas d’échec de la soumission de votre magasin Teams

Les applications publiées dans le magasin Microsoft Teams doivent respecter les [instructions de validation du magasin Teams et les](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) [stratégies de la Place de marché commerciale](/legal/marketplace/certification-policies).

En cas d’échec de la soumission de votre magasin, Microsoft fournit un service de validation concierge pour vous aider à rendre votre application conforme et publiée.

## <a name="get-help-directly-from-microsoft"></a>Obtenir de l’aide directement auprès de Microsoft

Le service de validation concierge fourni par Microsoft aide les développeurs à publier leurs applications dans le magasin Teams. Dans le cadre de ce service, Microsoft vérifie si votre application fonctionne comme décrit, contient toutes les métadonnées appropriées et fournit de la valeur aux utilisateurs.

Si votre soumission d’application échoue, Microsoft vous envoie un rapport de révision avec des recommandations dans les 24 heures suivant la soumission.

## <a name="resolve-issues-and-resubmit-your-app"></a>Résoudre les problèmes et soumettre à nouveau votre application

Vous devez résoudre tous les problèmes signalés par l’équipe de validation microsoft concierge avant de soumettre à nouveau votre application dans l’Espace partenaires. Le rapport Microsoft contient les informations suivantes :

* Instructions de [validation correspondantes](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) pour chaque problème.
* Instructions sur la reproduction de chaque problème.
* Recommandations pour résoudre chaque problème en fonction de la documentation du développeur disponible publiquement.

Le processus de résolution des problèmes et de réinscription d’une application se présente généralement comme suit :

1. Vous corrigez tous les problèmes du rapport.
1. Vous envoyez ce qui suit à l’équipe de validation du concierge Microsoft à <a href="mailto:teamsubm@microsoft.com">teamsubm@microsoft.com</a> :
   * Un package d’application mis à jour
   * Testez les notes de votre application, si vous n’avez pas inclus ces notes dans votre soumission d’origine :
      * Informations d’identification pour au moins deux comptes (un administrateur et un non-administrateur).
      * Instructions pour configurer l’application et tester ses fonctionnalités.
      * Vidéo montrant votre application utilisée dans Teams.
1. L’équipe de validation microsoft concierge teste entièrement votre application mise à jour.
1. Vous effectuez l’une des opérations suivantes :
   * Si votre application ne présente aucun problème, renvoyez-la à l’Espace partenaires.
   * Si les problèmes ne sont pas résolus ou que Microsoft trouve de nouveaux problèmes, vous recevez un autre rapport sur ce qu’il faut résoudre. Résolvez ces problèmes et envoyez une version mise à jour de l’application à <a href="mailto:teamsubm@microsoft.com">teamsubm@microsoft.com</a>.

> [!CAUTION]
> Pour éviter les échecs de soumission multiples, ne soumettez pas votre application à l’Espace partenaires tant que l’équipe de validation du concierge Microsoft n’a pas approuvé votre application.

## <a name="faq"></a>FAQ

Obtenez des réponses à certaines questions courantes lors de la résolution des problèmes de soumission d’application.

<br>

<details>

<summary><b>Combien de temps faut-il pour publier mon application ?</b></summary>

Si votre soumission dans le Store n’a aucun problème, votre application sera publiée dans les 1 à 2 jours ouvrables. Si votre application échoue, une équipe de Microsoft vous fournit des recommandations pour résoudre les problèmes. Une fois que vous avez apporté ces correctifs et renvoyé une application mise à jour à cette équipe, vous serez averti dans les 24 heures si votre application est prête à publier ou a encore besoin de plus de travail.

<br>

</details>

<details>

<summary><b>Comment faire augmenter la probabilité que mon application passe la soumission ?</b></summary>

L’exécution des opérations suivantes peut aboutir à une soumission réussie :

1. Développez votre application en fonction [des instructions de conception teams](~/concepts/design/design-teams-app-overview.md).
1. Assurez-vous que votre application respecte les [instructions de validation du Magasin Teams et les](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) stratégies de certification de la [Place de marché commerciale Microsoft](/legal/marketplace/certification-policies).
1. Testez votre package d’application avec [l’outil de validation d’application Microsoft Teams](https://dev.teams.microsoft.com/appvalidation.html).
1. [Préparez la soumission de votre magasin Teams](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md).

<br>

</details>

<details>

<summary><b>Mon application est en bêta-test. Puis-je soumettre mon application de toute façon pour gagner du temps sur le processus de publication ?</b></summary>

Non. Microsoft valide uniquement les applications prêtes pour la production.

<br>

</details>

<details>

<summary><b>Puis-je contacter l’e-mail teamsubm@microsoft.com avant de soumettre mon application pour la première fois dans l’Espace partenaires ?</b></summary>

Non. Microsoft ne commence pas à valider votre application tant que vous n’avez pas soumis votre application pour la première fois dans l’Espace partenaires.

<br>

</details>

<details>

<summary><b>J’ai reçu un e-mail de l’Espace partenaires indiquant que mon application a été approuvée pour la publication. Pourquoi mon application n’est-elle pas dans le Magasin Teams ?</b></summary>

Une fois votre application approuvée, la publication prend généralement 1 à 2 jours ouvrables en fonction des fonctionnalités de l’application.Si votre application n’a pas été publiée après deux jours ouvrables, contactez <a href="mailto:teamsubm@microsoft.com">teamsubm@microsoft.com</a>.

<br>

</details>
