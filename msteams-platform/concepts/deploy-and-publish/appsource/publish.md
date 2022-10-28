---
title: 'Vue d’ensemble : publier votre application dans le store Microsoft Teams'
description: Publiez votre application dans le Magasin Microsoft Teams ou AppSource. À quoi vous devez vous attendre après l’envoi, conseils pour l’approbation rapide et la publication d’applications liées à une offre SaaS.
ms.topic: overview
author: heath-hamilton
ms.author: surbhigupta
ms.localizationpriority: high
ms.openlocfilehash: f3981ccc9437c28b288a86912dd2b878e729c101
ms.sourcegitcommit: 0e4fcbc5efff4bfa1dbfba1e5467bbfaa6638705
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/28/2022
ms.locfileid: "68773505"
---
# <a name="publish-your-app-to-the-microsoft-teams-store"></a>Publiez votre application dans le store Microsoft Teams.

Vous pouvez distribuer votre application directement dans le Store au sein de Microsoft Teams et atteindre des millions d’utilisateurs dans le monde entier. Si votre application est également proposée dans le Store, vous pouvez atteindre instantanément les clients potentiels.

Les applications publiées dans le magasin Teams sont également automatiquement répertoriées sur la [Place de marché commerciale Microsoft](https://appsource.microsoft.com), qui est la place de marché officielle pour les applications et solutions Microsoft 365.

## <a name="understand-the-publishing-process"></a>Comprendre le processus de publication

Si votre application est prête pour la production, vous pouvez commencer le processus d’obtention de sa liste dans le magasin Teams.

> [!TIP]
> Suivre attentivement les étapes de pré-soumission peut augmenter le risque que Microsoft approuve votre application pour la publication.

:::row:::
   :::column span="":::

   :::column-end:::
   :::column span="3":::
      :::image type="content" source="../../../assets/images/submission/teams-app-store-publish-process.png" alt-text="Processus de publication de l’App Store Teams" lightbox="../../../assets/images/submission/teams-app-store-publish-process.png":::
   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

1. [Passez en revue les instructions de validation du Magasin Teams](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) pour vous assurer que votre application répond aux normes de l’application Teams et du store.

1. [Créer un compte de développeur Espace partenaires](~/concepts/deploy-and-publish/appsource/prepare/create-partner-center-dev-account.md).

1. [Préparez votre soumission au Store](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md), qui inclut l’exécution de tests automatisés, la compilation de notes de test, la création d’une liste de magasins, entre autres tâches importantes pour accélérer le processus de révision.

1. [Soumettez votre application via](/office/dev/store/add-in-submission-guide) l’Espace partenaires.

1. Si votre soumission échoue, contactez Microsoft directement pour [résoudre les problèmes et renvoyer votre application](~/concepts/deploy-and-publish/appsource/resolve-submission-issues.md).

## <a name="what-to-expect-after-you-submit-your-app"></a>À quoi vous attendre après avoir envoyé votre application ?

* **Tests fonctionnels et expérience approfondies**

  Votre application est examinée en détail par un validateur pour garantir la conformité avec les stratégies de certification de la [Place de marché commerciale Microsoft](/legal/marketplace/certification-policies).
  L’accent sera mis sur les tests fonctionnels et d’expérience utilisateur approfondis, les vérifications d’utilisation et les vérifications des métadonnées. La validation des applications est effectuée sur les clients de bureau, web et mobiles. Nous mettons tout en œuvre pour vous fournir un rapport de test détaillé dans les 24 heures de travail qui suivent l’envoi.

* **Publication d’application guidée via le service concierge**

  Si aucun problème n’est observé avec votre application, votre application est approuvée et publiée dans le Magasin Teams. En revanche, si les problèmes sont présents, vous recevrez un rapport de validation automatisé de Espace partenaires avec les détails de l’échec. Pour vous aider à publier votre application dans le Magasin Teams et à vous guider tout au long de ce processus, l’équipe de validation vous enverra un e-mail personnalisé à partir de notre service concierge [teamsubm@microsoft.com](mailto:teamsubm@microsoft.com) qui inclut les informations suivantes :

  * Résumé de tous les problèmes

  * Détails des échecs ou des problèmes liés aux liens de stratégie et à la catégorisation :

    * Correctif obligatoire : les problèmes doivent être résolus avant l’approbation de l’application.

    * Correction suggérée : les problèmes peuvent être résolus après l’approbation de l’application, car les problèmes sont des recommandations pour améliorer l’expérience de votre application.

    * Bloqueur : les problèmes empêchent l’équipe de validation de tester davantage les fonctionnalités de votre application et doivent être résolus pour que la validation continue.

    * Requête : les requêtes peuvent être partagées pour obtenir des réponses à des questions spécifiques liées à votre application.

  * Étapes pour recréer des problèmes via des instructions écrites ou un format vidéo.

  * Recommandations pour résoudre les problèmes signalés avec des liens vers des documents d’aide.

  Une fois que vous avez examiné la liste des problèmes, corrigez tous les problèmes signalés et partagez le package d’application mis à jour par e-mail pour que l’équipe de validation valide votre application à nouveau. Si vous avez des requêtes liées aux problèmes signalés, contactez l’équipe de validation à [teamsubm@microsoft.com](mailto:teamsubm@microsoft.com).

  S’il reste des problèmes ou des problèmes de régression observés dans votre application, l’équipe de validation partagera un rapport de validation mis à jour avec vous. Si votre application avait des bloqueurs, vous pouvez voir de nouveaux problèmes signalés lorsque votre application est validée une fois les blocages résolus. Parfois, l’équipe de validation a également remarqué des problèmes de régression dans les applications après le déploiement de correctifs. Il faut quelques nouvelles soumissions pour fermer tous les problèmes d’une application qui se compose de bogues et l’approuver pour qu’elle soit publiée dans le magasin Teams.

  Une fois que tous les problèmes signalés sont fermés et que la soumission finale est effectuée dans le Espace partenaires, l’équipe de validation approuve et publie votre application. Autorisez au moins un jour ouvré pour que l’application soit disponible dans le Magasin Teams.

* **Analyser l’utilisation des applications**

  Une fois votre application approuvée et publiée, vous pouvez suivre son utilisation dans le [Rapport d’utilisation de l’application Teams](/office/dev/store/teams-apps-usage) dans l’Espace partenaires. Les mesures incluent les utilisateurs actifs mensuels, quotidiens et hebdomadaires, ainsi que les graphiques de rétention et d’intensité qui vous permettent de suivre l’évolution et la fréquence de l’utilisation.

  L’affichage des données concernant les applications récemment publiées prend environ une semaine dans le rapport.

## <a name="tips-for-rapid-approval-to-publish-your-app"></a>Conseils pour une approbation rapide de la publication de votre application

* **Lors de la phase de conception**

  Passez en revue les [instructions de validation du magasin](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) au début du cycle de vie de votre application (phase de conception) pour vous assurer que vous générez votre application conformément aux exigences du Store. Si vous générez votre application conformément à ces instructions, cela empêchera tout retravail en raison d’un non-respect des stratégies de stockage.

* **Avant la soumission de l’application**

  1. [Créez votre compte Espace partenaires](prepare/create-partner-center-dev-account.md) bien à l’avance. Si vous rencontrez des difficultés avec votre compte [Espace partenaires](prepare/create-partner-center-dev-account.md), créez un [ticket de support](/azure/marketplace/partner-center-portal/support).

  1. Passez à nouveau en revue les [instructions de validation du magasin](prepare/teams-store-validation-guidelines.md) pour vous assurer que votre application est conforme aux exigences du Store. La vérification permet de réduire le nombre de problèmes observés dans votre application et, par conséquent, le temps nécessaire pour approuver votre application.

  1. Testez et retestez votre application :

     1. Validez votre package d’application à l’aide du [Developer Portal](https://dev.teams.microsoft.com/home) Teams pour identifier et corriger les erreurs de package.

        :::image type="content" source="../../../assets/images/submission/teams-validation-developer-portal.png" alt-text="Validation de l’application du Store Teams dans Developer Portal" lightbox="../../../assets/images/submission/teams-validation-developer-portal.png":::

     1. Testez automatiquement votre application soigneusement avant la soumission de l’application pour vous assurer qu’elle respecte les stratégies du Store. Chargez une version test de l’application dans Teams et testez les flux utilisateur de bout en bout pour votre application. Assurez-vous que la fonctionnalité fonctionne comme prévu, que les liens ne sont pas rompus, que l’expérience utilisateur n’est pas bloquée et que les limitations sont clairement mises en évidence.

     1. Testez votre application sur les clients de bureau, web et mobiles. Assurez-vous que l’application répond à différents facteurs de forme.
  
  1. Effectuez la[vérification de l’éditeur](/azure/active-directory/develop/publisher-verification-overview) avant de soumettre votre application. Si vous rencontrez des problèmes, vous pouvez créer un[ ticket de support](/azure/marketplace/partner-center-portal/support) pour la résolution.

  1. Lorsque vous préparez l’envoi de l’application, [suivez la liste de vérification](/microsoftteams/platform/concepts/deploy-and-publish/appsource/prepare/submission-checklist) et incluez les détails suivants dans votre package de soumission :

        1. Package d’application vérifié de manière approfondie.

        1. Informations d’identification d’administrateur et d’utilisateur non administrateur pour tester les fonctionnalités de votre application (si votre application propose un modèle d’abonnement Premium).

        1. Instructions de test détaillant les fonctionnalités de l’application et les scénarios pris en charge.

        1. Instructions de configuration si votre application nécessite davantage de configuration pour accéder aux fonctionnalités de l’application. Sinon, si votre application nécessite une configuration complexe, vous pouvez également fournir un [client de démonstration approvisionné](/office/developer-program/microsoft-365-developer-program-get-started) avec un accès administrateur afin que nos validateurs puissent ignorer les étapes de configuration.

        1. Lien vers une vidéo de démonstration qui illustre le flux utilisateur clé pour votre application. Ceci est vivement recommandé.

* **Après la soumission de l’application**

  * Après avoir examiné le rapport de validation, répondez au fil de messagerie avec toutes les requêtes relatives au rapport de validation, ou si vous avez besoin d’une assistance supplémentaire pour résoudre les problèmes signalés.

  * Assurez-vous que vous disposez d’une bande passante de développeur suffisante pour résoudre les problèmes signalés jusqu’à ce que l’application soit approuvée.

  * Vérifiez que vous avez [résolu tous les problèmes](/microsoftteams/platform/concepts/deploy-and-publish/appsource/resolve-submission-issues) signalés par le service concierge [teamsubm@microsoft.com](mailto:teamsubm@microsoft.com) avant de partager votre package d’application pour d’autres tests. Cela permet de réduire le nombre d’itérations nécessaires à la validation de votre application et, par conséquent, le temps nécessaire pour approuver votre application.
  
  * Évitez de modifier les fonctionnalités de l’application pendant le processus de validation, ce qui peut entraîner la découverte de nouveaux problèmes et augmenter le temps nécessaire à l’approbation de votre application.

## <a name="additional-tips-for-rapid-approval-to-publish-your-app-linked-to-a-saas-offer"></a>Conseils supplémentaires pour une approbation rapide de la publication de votre application liée à une offre SaaS

* **Lors de la phase de conception**

  Passez en revue [les instructions de validation du Store spécifiques aux applications publiées avec des offres SaaS liées](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#apps-linked-to-saas-offer) au début du cycle de vie de votre application (phase de conception) pour vous assurer que vous générez votre application conformément aux exigences du Store et aux stratégies de la [Place de marché commerciale Microsoft applicables aux applications Teams liées aux offres SaaS](/legal/marketplace/certification-policies#11405-teams-app-linked-to-software-as-a-service-saas-offers). Si vous générez votre application conformément à ces instructions, cela empêchera tout retravail en raison d’un non-respect des stratégies de stockage.

* **Avant la soumission de l’application**

  1. Lorsque vous préparez l’envoi de l’application, vérifiez les points suivants :

      1. Votre application est liée à une offre SaaS en direct (déjà publiée) sur AppSource avec au moins un plan avec des informations de tarification.

      1. Vous avez correctement mentionné les détails `subscriptionOffer` dans le manifeste de votre application au format `publisherId.offerId`.

      1. Vous devez vous assurer que votre offre SaaS liée est conçue pour prendre en charge les licences attribuées sur un [modèle de tarification SaaS](/azure/marketplace/create-new-saas-offer-plans).

      1. Incluez des instructions de test ou des instructions de configuration, ou créez un lien vers une vidéo de démonstration détaillant les fonctionnalités de l’application et les scénarios pris en charge, ainsi que toute information supplémentaire permettant à nos testeurs de comprendre facilement vos flux de travail du portail SaaS.

  1. Vous devez [tester](~/concepts/deploy-and-publish/appsource/prepare/test-preview-for-monetized-apps.md)de bout en bout les flux de travail de gestion des licences et des achats de bout en bout avant de soumettre votre application liée à une offre SaaS à des fins de validation. Vérifiez les points suivants :

     1. Les utilisateurs administrateurs et non-administrateurs peuvent passer une commande et confirmer l’achat de votre abonnement. Les acheteurs peuvent accéder à la page d’accueil de l’application SaaS en sélectionnant  **Configurer maintenant** dans le Centre d’administration Microsoft. Testez et assurez-vous que vos acheteurs peuvent activer et configurer leur abonnement sur votre application SaaS. La messagerie sur votre application SaaS doit fournir suffisamment d’informations claires sur la façon de transférer à un acheteur.

     1. La section **Gérer les abonnements** dans le Centre d’administration Microsoft affiche les détails corrects des abonnements proposés par vos utilisateurs de test. L’état de l’abonnement, le nombre de licences et d’autres détails doivent être exacts.

     1. L’achat et la suppression des flux de travail de licence fonctionnent comme prévu. Assurez-vous que les acheteurs peuvent augmenter le nombre de licences du Centre d’administration Microsoft. Assurez-vous que le nombre de licences et l’attribution sur votre application SaaS reflètent les licences respectives et les bonnes personnes affectées. Vérifiez également que votre application SaaS offre un moyen de retirer une licence à un utilisateur. Après la suppression d’une licence, assurez-vous que les affectations restantes et le nombre restent intacts sur votre application SaaS et que les détails corrects sont reflétés dans le Centre d’administration Microsoft.

     1. L’annulation de l’abonnement fonctionne comme prévu. Les acheteurs peuvent annuler un abonnement. Après l’annulation, vérifiez si l’état correct de l’abonnement est reflété dans le Centre d’administration Microsoft et votre application SaaS. Vérifiez que l’acheteur a perdu l’accès à l’abonnement après l’annulation réussie.

     1. Le nouvel achat d’un abonnement est transparent. Après l’annulation d’un abonnement actif, effectuez des tests approfondis pour vous assurer que les acheteurs peuvent acheter l’abonnement.

     1. Les acheteurs peuvent modifier leur offre souscrite. Une fois le plan modifié, les utilisateurs peuvent accéder aux fonctionnalités du plan mis à niveau ou rétrogradé.

     1. Votre application SaaS contient des fonctionnalités de gestion des licences. Les acheteurs doivent être en mesure d’attribuer, de modifier et de réaffecter les licences disponibles aux utilisateurs. Vérifiez si les acheteurs peuvent ajouter ou supprimer des utilisateurs pour gérer les licences.
  
  1. Vous devez tester et vérifier que les flux d’achat de licence minimum et en bloc fonctionnent comme prévu.
  
  1. Vous devez vous assurer que les utilisateurs auxquels des licences sont attribuées ont accès aux fonctionnalités précises du plan acheté décrites dans la description de votre plan.

## <a name="see-also"></a>Voir aussi

* [Publier des applications Teams dans le magasin Microsoft Teams](/training/modules/microsoft-teams-publish-app-to-store/)
* [Publication sur Microsoft 365 App Stores](/office/dev/store/)
* [Charger votre application Teams](~/concepts/deploy-and-publish/apps-upload.md)
* [Publier votre application Teams sur votre organisation](/MicrosoftTeams/tenant-apps-catalog-teams?toc=/microsoftteams/platform/toc.json&bc=/MicrosoftTeams/breadcrumb/toc.json)
* [Planifier l’expérience d’intégration pour les utilisateurs](../../design/planning-checklist.md#plan-beyond-app-building)
* [Distribution d’applications d’onglets sur des mobiles](../../../tabs/design/tabs-mobile.md#distribution)
* [Aperçu du test pour les applications monétisées](prepare/Test-preview-for-monetized-apps.md)
* [Paramètres de classement du store Microsoft Teams](post-publish/teams-store-ranking-parameters.md)
