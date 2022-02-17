---
title: 'Vue d’ensemble : Teams publication de l’App Store'
description: Décrit le processus de soumission de votre application à l’Partner Center et de sa publication dans Microsoft Teams store (et AppSource).
ms.topic: overview
author: heath-hamilton
ms.author: surbhigupta
ms.localizationpriority: none
ms.openlocfilehash: eaebde76a3d1f387ba16c9fdc77670144d22fa61
ms.sourcegitcommit: 40aade608ee21f5d7d813bd145bef5736dc647f1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/17/2022
ms.locfileid: "62881650"
---
# <a name="publish-your-app-to-the-microsoft-teams-store"></a>Publier votre application dans le Microsoft Teams store

Vous pouvez distribuer votre application directement dans le Store Microsoft Teams et atteindre des millions d’utilisateurs dans le monde entier. Si votre application est également présente dans le Store, vous pouvez immédiatement atteindre des clients potentiels.

Les applications publiées dans Teams store sont également automatiquement répertoriées sur [Microsoft AppSource](https://appsource.microsoft.com), qui est la place de marché officielle pour Microsoft 365 applications et solutions.

## <a name="understand-the-publishing-process"></a>Comprendre le processus de publication

Lorsque vous pensez que votre application est prête pour la production, vous pouvez commencer le processus d’obtention de sa liste dans Teams store.

> [!TIP]
> Le fait de suivre attentivement les étapes préalables à la soumission peut augmenter le risque que Microsoft approuve votre application pour publication.

:::row:::
   :::column span="":::
      
   :::column-end:::
   :::column span="3":::
      :::image type="content" source="../../../assets/images/submission/teams-app-store-publish-process.png" alt-text="Teams publication de l’App Store" lightbox="../../../assets/images/submission/teams-app-store-publish-process.png":::
   :::column-end:::
   :::column span="":::
      
   :::column-end:::
:::row-end:::

1. [Examinez les recommandations Teams validation du Store](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) pour vous assurer que votre application répond Teams et aux normes du Store.

1. [Créez un compte de développeur de l’Espace partenaires](~/concepts/deploy-and-publish/appsource/prepare/create-partner-center-dev-account.md).

1. [Préparez votre soumission au Store](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md), qui inclut l’exécution de tests automatisés, la compilation de notes de test, la création d’une liste de magasins, entre autres tâches importantes pour accélérer le processus de révision.

1. [Soumettez votre application via](/office/dev/store/add-in-submission-guide) l’Partner Center.

1. Si votre soumission échoue, travaillez directement avec Microsoft pour résoudre les problèmes et soumettre à nouveau [votre application](~/concepts/deploy-and-publish/appsource/resolve-submission-issues.md).

## <a name="what-to-expect-after-you-submit-your-app"></a>À quoi s’attendre après avoir soumis votre application ?

* **Tests fonctionnels et d’expérience approfondies**

  Votre application est minutieusement examinée par un validateur pour s’assurer de la conformité avec les stratégies de [certification De Microsoft Commercial Marketplace](/legal/marketplace/certification-policies) en se concentre sur les tests approfondis fonctionnels et d’expérience utilisateur, les vérifications d’utilisation et les contrôles de métadonnées. La validation de l’application est effectuée sur les clients de bureau, web et mobiles.

* **Publication d’application guidée par le biais du service d’accueil**

  Si aucun problème n’est observé avec votre application, elle sera approuvée et publiée dans le Teams store. En cas de problème, vous recevrez un rapport de validation automatisé de l’Partner Center avec les détails de l’échec. Pour vous aider à publier correctement votre application dans le magasin Teams et vous guider tout au long de ce processus, l’équipe de validation vous enverra un courrier électronique personnalisé à partir de notre [teamsubm@microsoft.com](mailto:teamsubm@microsoft.com) de service qui inclut les informations suivantes :

   * Résumé de tous les problèmes

   * Détails des échecs ou des problèmes avec les liens de stratégie et la catégorisation : 

     * Correctif obligatoire : ces problèmes doivent être résolus avant l’approbation de l’application.

     * Solution suggérée : ces problèmes peuvent être résolus après l’approbation de l’application, car il s’agit de recommandations pour améliorer l’expérience de votre application.

     * Bloqueur : ces problèmes empêchent l’équipe de validation de tester davantage les fonctionnalités de votre application et doivent être résolus pour que la validation continue.

     * Requête : ces requêtes peuvent être partagées pour obtenir des réponses à des questions spécifiques relatives à votre application.

   * Étapes pour recréer les problèmes par le biais d’instructions écrites ou d’un format vidéo.

   * Recommandations résoudre les problèmes signalés avec des liens vers des documents d’aide.
 
  Une fois que vous avez examiné la liste des problèmes, corrigez tous les problèmes signalés et partagez le package d’application mis à jour par courrier électronique, pour que l’équipe de validation valide votre application de manière approfondie. Si vous avez des requêtes liées aux problèmes signalés, contactez l’équipe de validation [teamsubm@microsoft.com](mailto:teamsubm@microsoft.com).

  Si des problèmes restants ou de régression sont observés dans votre application, l’équipe de validation partagera avec vous un rapport de validation mis à jour. Si votre application avait des bloqueurs, vous pouvez voir de nouveaux problèmes signalés lorsque votre application est validée une fois les bloqueurs résolus. Parfois, l’équipe de validation a également remarqué des problèmes de régression dans les applications après le déploiement de correctifs. Il faut quelques ré-envois pour fermer tous les problèmes d’une application qui se compose de bogues et l’obtenir approuvée pour publier dans le Teams store.

  Une fois tous les problèmes signalés fermés et la soumission finale dans l’Centre partenaires, l’équipe de validation approuve et publie votre application. Autorisez au moins un jour ouvr pour que l’application soit disponible dans Teams store.

## <a name="tips-for-rapid-approval-to-publish-your-app"></a>Astuces pour une approbation rapide de la publication de votre application

* **Lors de la phase de conception**

  Examinez les instructions [de validation du Store](prepare/teams-store-validation-guidelines.md) au début du cycle de vie de votre application (phase de conception) pour vous assurer que vous créez votre application en adéquation avec les exigences du Store. Si vous créez votre application en respectant ces instructions, cela empêchera toute nouvelle mise à jour en raison de l’absence d’adhésion aux stratégies du Store.

* **Avant la soumission de l’application**

  1. [Créez votre compte Espace partenaires](prepare/create-partner-center-dev-account.md) bien à l’avance. Si vous êtes confronté à des difficultés avec votre [compte Espace](prepare/create-partner-center-dev-account.md) partenaires, créez un [ticket de support](/azure/marketplace/partner-center-portal/support).

  1. Examinez [à nouveau les instructions de validation](prepare/teams-store-validation-guidelines.md) du Store pour vous assurer que votre application est en adéquation avec les exigences du Store. Cela permet de réduire le nombre de problèmes observés dans votre application et, par conséquent, le temps pris pour approuver votre application.

  1. Testez et retentez votre application :

     1. Validez votre package d’application à l’aide Teams [portail](https://dev.teams.microsoft.com/home) du développeur pour identifier et corriger les erreurs de package.

        :::image type="content" source="../../../assets/images/submission/teams-validation-developer-portal.png" alt-text="validation de la boutique":::
 
     1. Testez automatiquement votre application minutieusement avant sa soumission pour vous assurer qu’elle respecte les stratégies du Store. Chargez une version test de l Teams et testez les flux d’utilisateurs de bout en bout pour votre application. Assurez-vous que la fonctionnalité fonctionne comme prévu, que les liens ne sont pas rompus, que l’expérience utilisateur n’est pas bloquée et que les limitations sont clairement mises en évidence.

     1. Testez votre application sur les clients de bureau, web et mobiles. Assurez-vous que l’application répond à différents facteurs de forme.

  1. Terminez [la vérification de l’éditeur](/azure/active-directory/develop/publisher-verification-overview) avant de soumettre votre application. Si vous avez des problèmes, vous pouvez créer un ticket de [support pour](/azure/marketplace/partner-center-portal/support) la résolution.

  1. Lors de la préparation de la soumission d’application, suivez [la liste de contrôle](/microsoftteams/platform/concepts/deploy-and-publish/appsource/prepare/submission-checklist) et incluez les détails suivants dans votre package de soumission :

      1. Package d’application minutieusement vérifié.

      1. Informations d’identification d’administrateur et d’utilisateur non administrateur pour tester les fonctionnalités de votre application (si votre application propose un modèle d’abonnement premium).

      1. Instructions de test détaillant les fonctionnalités de l’application et les scénarios pris en charge.

      1. Instructions de configuration si votre application nécessite une configuration supplémentaire pour accéder aux fonctionnalités de l’application. Par ailleurs, si votre application nécessite une configuration complexe, vous pouvez également fournir [](/office/developer-program/microsoft-365-developer-program-get-started) un client de démonstration fourni avec un accès administrateur afin que nos validateurs peuvent ignorer les étapes de configuration.

      1. Lien vers un flux d’utilisateur de clé d’enregistrement vidéo de démonstration pour votre application. Cette recommandation est vivement recommandée.

* **Soumission post-application**

  * Une fois que vous avez examiné le rapport de validation, répondez au thread de messagerie avec toutes les requêtes liées au rapport de validation ou si vous avez besoin d’une prise en charge supplémentaire pour résoudre les problèmes signalés.

  * Assurez-vous que vous avez suffisamment de bande passante développeur pour résoudre les problèmes signalés jusqu’à ce que l’application soit approuvée.

  * Assurez-vous que vous avez résolu tous les problèmes [signalés](/microsoftteams/platform/concepts/deploy-and-publish/appsource/resolve-submission-issues) par [le service teamsubm@microsoft.com](mailto:teamsubm@microsoft.com) avant de partager votre package d’application pour d’autres tests. Cela permet de réduire le nombre d’itérations requises pour valider votre application et, par conséquent, le temps nécessaire pour approuver votre application.
  
  * Évitez de modifier les fonctionnalités de l’application pendant le processus de validation. Cela peut entraîner la découverte de nouveaux problèmes et augmenter le temps d’approbation de votre application.

## <a name="see-also"></a>Voir aussi

* [Publication dans Microsoft 365 App Store](/office/dev/store/)
* [Télécharger votre application Teams de messagerie](~/concepts/deploy-and-publish/apps-upload.md)
* [Publier votre application Teams sur votre organisation](/MicrosoftTeams/tenant-apps-catalog-teams?toc=/microsoftteams/platform/toc.json&bc=/MicrosoftTeams/breadcrumb/toc.json)
* [Planifier l’expérience d’intégration pour les utilisateurs](../../design/understand-use-cases.md#plan-the-onboarding-experience)
* [Distribution d’applications d’onglets sur un appareil mobile](../../../tabs/design/tabs-mobile.md#distribution)
* [Aperçu du test pour les applications monétisées](prepare/Test-preview-for-monetized-apps.md)
