---
title: Résoudre les problèmes de soumission au Store
description: Comprendre comment résoudre les problèmes liés à votre soumission au Microsoft Teams store.
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
# <a name="resolve-issues-if-your-microsoft-teams-store-submission-fails"></a>Résoudre les problèmes en cas d’échec Microsoft Teams soumission au Store

Les applications publiées dans Microsoft Teams store doivent respecter les recommandations de validation Teams [store](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) et les stratégies de [marketplace commerciales.](/legal/marketplace/certification-policies)

Si votre soumission au Store échoue, Microsoft fournit un service de validation de validation pour vous aider à obtenir la conformité et la publication de votre application.

## <a name="get-help-directly-from-microsoft"></a>Obtenir de l’aide directement auprès de Microsoft

Le service de validation fourni par Microsoft permet aux développeurs d’obtenir leurs applications publiées dans Teams store. Dans le cadre de ce service, Microsoft vérifie si votre application fonctionne comme décrit, contient toutes les métadonnées appropriées et fournit une valeur ajoutée aux utilisateurs.

Si la soumission de votre application échoue, Microsoft vous envoie un rapport de révision avec des recommandations dans les 24 heures après la soumission.

## <a name="resolve-issues-and-resubmit-your-app"></a>Résoudre les problèmes et resoumettre votre application

Vous devez résoudre tous les problèmes signalés par l’équipe de validation microsoft avant de resoumettre votre application sur l’Partner Center. Le rapport Microsoft inclut les informations suivantes :

* Recommandations [de validation correspondantes](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) pour chaque problème.
* Instructions sur la façon de reproduire chaque problème.
* Recommandations résoudre chaque problème en fonction de la documentation du développeur disponible publiquement.

Le processus de résolution des problèmes et de resoumettre une application se passe généralement comme ceci :

1. Vous corrigez tous les problèmes dans le rapport.
1. Vous envoyez les informations suivantes à l’équipe de validation de Microsoft <a href="mailto:teamsubm@microsoft.com">teamsubm@microsoft.com</a>:
   * Un package d’application mis à jour
   * Notes de test pour votre application, si vous ne les avez pas inclus dans votre soumission d’origine :
      * Informations d’identification pour au moins deux comptes (un administrateur et un non administrateur).
      * Instructions pour configurer l’application et tester ses fonctionnalités.
      * Vidéo montrant votre application utilisée dans Teams.
1. L’équipe de validation microsoft teste entièrement votre application mise à jour.
1. Vous pouvez :
   * Si votre application est sans problème, resoumettre votre application sur l’Espace partenaires.
   * Si des problèmes ne sont pas résolus ou si Microsoft trouve de nouveaux problèmes, vous recevez un autre rapport sur les mesures à corriger. Résolvez ces problèmes et envoyez une version mise à jour de l’application <a href="mailto:teamsubm@microsoft.com">teamsubm@microsoft.com</a>.

> [!CAUTION]
> Pour éviter plusieurs échecs de soumission, ne resoumettez pas votre application sur l’Partner Center tant que l’équipe de validation de Microsoft n’a pas approuvé votre application.

## <a name="faq"></a>FAQ

Obtenez des réponses à certaines questions courantes lors de la résolution des problèmes de soumission d’application.

<br>

<details>

<summary><b>Combien de temps faut-il pour publier mon application ?</b></summary>

Si votre soumission au Store ne présente aucun problème, votre application publiera dans un délai de 1 à 2 jours ou moins. Si votre application échoue, une équipe microsoft vous fournit des recommandations pour résoudre les problèmes. Une fois ces correctifs corrigés et que vous renvoyez une application mise à jour à cette équipe, vous serez averti dans les 24 heures si votre application est prête à être publiée ou a encore besoin de travail.

<br>

</details>

<details>

<summary><b>Comment augmenter la probabilité que mon application réussira la soumission ?</b></summary>

Les opérations suivantes peuvent aboutir à une soumission réussie :

1. Développez votre application en fonction des recommandations [Teams conception.](~/concepts/design/design-teams-app-overview.md)
1. Assurez-vous que votre application respecte les instructions de [validation Teams store](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) et les stratégies de certification de Microsoft Commercial [Marketplace.](/legal/marketplace/certification-policies)
1. Testez votre package d’application avec [l Microsoft Teams de validation d’application.](https://dev.teams.microsoft.com/appvalidation.html)
1. [Préparez votre soumission Teams au Store.](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)

<br>

</details>

<details>

<summary><b>Mon application est en phase de test bêta. Puis-je quand même soumettre mon application pour gagner du temps lors du processus de publication ?</b></summary>

Non. Microsoft valide uniquement les applications prêtes pour la production.

<br>

</details>

<details>

<summary><b>Est-il possible de contacter teamsubm@microsoft.com de messagerie électronique avant de soumettre mon application pour la première fois sur l’Partner Center ?</b></summary>

Non. Microsoft ne commence pas à valider votre application tant que vous n’avez pas soumis votre application pour la première fois sur l’Partner Center.

<br>

</details>

<details>

<summary><b>J’ai reçu un courrier électronique de l’Partner Center pour me dire que mon application a été approuvée pour la publication. Pourquoi mon application n’est-elle pas dans Teams store ?</b></summary>

Une fois votre application approuvée, la publication prend généralement entre 1 et 2 jours ou jours, en fonction des fonctionnalités de l’application.Si votre application n’a pas été publiée après deux jours ouvr, contactez <a href="mailto:teamsubm@microsoft.com">teamsubm@microsoft.com</a>.

<br>

</details>
