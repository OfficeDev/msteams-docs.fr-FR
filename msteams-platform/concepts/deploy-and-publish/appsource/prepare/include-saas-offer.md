---
title: Inclure une offre SaaS avec votre application
description: Dans cet article, découvrez comment monétiser votre application Microsoft Teams avec un modèle de tarification basé sur un abonnement et inclure une offre SaaS avec votre application Microsoft Teams.
author: heath-hamilton
ms.author: surbhigupta
ms.topic: how-to
ms.localizationpriority: high
ms.openlocfilehash: e9182df9f6c3c5d7f84654022e658ac6d670e50d
ms.sourcegitcommit: 209b9942c02b5affdd995348902114d3b9805c61
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/09/2022
ms.locfileid: "67288184"
---
# <a name="include-a-saas-offer-with-your-teams-app"></a>Inclure une offre SaaS avec votre application Teams

:::row:::
   :::column span="3":::

Avec une offre SaaS (Software-as-a-Service) pouvant effectuer des transaction, vous pouvez monétiser votre application Teams en vendant des offres d’abonnement directement à partir de votre description dans le magasin Teams. Par exemple, supposons que vous disposez d’une application gratuite que tout le monde peut obtenir dans le Store. Vous pouvez désormais proposer des offres Premium et d’entreprise pour les utilisateurs qui souhaitent plus de fonctionnalités.

Voici une idée générale de la façon de monétiser votre application :

1. [Planifiez votre offre SaaS](#plan-your-saas-offer).

1. [Intégrez les API de gestion des commandes en ligne (SaaS)](#integrate-with-the-saas-fulfillment-apis).

1. [Créez une page d’accueil pour la gestion des abonnements](#build-a-landing-page-for-subscription-management).

1. [Créez votre offre SaaS](#create-your-saas-offer).

1. [Configurez votre application pour l’offre SaaS](#configure-your-app-for-the-saas-offer).

1. [Publier votre application dans le magasin Teams](#publish-your-app).

   :::column-end:::
   :::column span="1":::

:::image type="content" source="~/assets/images/saas-offer/saas-offer-diagram.png" alt-text="Diagramme montrant comment inclure une offre SaaS avec votre application Teams.":::

   :::column-end:::
:::row-end:::

## <a name="plan-your-saas-offer"></a>Planifier votre offre SaaS

Pour obtenir des conseils complets, consultez [comment planifier une offre SaaS pour la place de marché commerciale Microsoft](/azure/marketplace/plan-saas-offer).

Lors de la planification de la monétisation de votre application Teams, voici quelques éléments à prendre en compte :

* Déterminez votre modèle d’abonnement. Une offre SaaS pouvant effectuer des transactions peut inclure plusieurs offres d’abonnement. Les offres d’abonnement publics disponibles pour tout le monde sont les plus courantes, mais vous pouvez également cibler des clients spécifiques avec des offres dédiées. Pour plus d’informations, consultez [plans privés dans la place de marché commerciale Microsoft](/azure/marketplace/private-plans).
* Découvrez [*Vendre via Microsoft* comme option de référencement](/azure/marketplace/plan-saas-offer#listing-options) pour votre offre SaaS, qui est requise si vous souhaitez que les utilisateurs souscrivent à des offres d’abonnement pour votre application directement via le magasin Teams.
* Découvrez comment [l’authentification unique (SSO) Azure Active Directory](/azure/marketplace/azure-ad-saas) permet à vos clients de acheter et de gérer des abonnements. (L’authentification unique Microsoft Azure Active Directory (Azure AD) est requise pour les applications Teams avec des offres SaaS.)
* Comprenez que vous êtes responsable de la gestion et du paiement de l’infrastructure requise pour prendre en charge l’utilisation de votre offre SaaS par vos clients.
* Offres pour mobiles. Pour éviter toute violation des stratégies tierces du magasin d’applications, votre application ne peut pas inclure de liens qui permettent aux utilisateurs de souscrire à des offres d’abonnement sur les appareils mobiles. Toutefois, vous pouvez toujours indiquer si votre application comporte des fonctionnalités qui nécessitent une offre d’abonnement. Pour plus d’informations, consultez les [stratégies de certification de la place de marché commerciale](/legal/marketplace/certification-policies#114048-mobile-experience) associées.

## <a name="integrate-with-the-saas-fulfillment-apis"></a>Intégrer avec les API de traitement SaaS

L’intégration avec les API de traitement SaaS est nécessaire pour monétiser votre application Teams. Ces API vous aident à gérer le cycle de vie d’une offre d’abonnement une fois qu’elle a été souscrite par un utilisateur.

Pour obtenir des instructions complètes et des informations de référence sur les API, consultez la [documentation des API de traitement SaaS](/azure/marketplace/partner-center-portal/pc-saas-fulfillment-apis). En règle générale, vous devez implémenter les étapes suivantes à l’aide des API une fois qu’un abonnement est acheté :

1. Recevoir un [*jeton d’identification d’achat*](/azure/marketplace/partner-center-portal/pc-saas-fulfillment-life-cycle#purchased-but-not-yet-activated-pendingfulfillmentstart) via l’URL de votre page d’accueil.

1. Utilisez le jeton pour récupérer les détails de l’abonnement.

1. Informez la place de marché commerciale que l’abonnement est activé.

### <a name="best-practices-for-implementing-subscription-management"></a>Meilleures pratiques pour implémenter la gestion des abonnements

* Avec les offres SaaS pouvant effectuer des transactions pour les applications Teams, les offres d’abonnement (licences) doivent être attribuées à des utilisateurs individuels plutôt qu’à des groupes ou à une organisation entière.
* Lorsqu’une offre d’abonnement est attribuée aux utilisateurs, informez-les par le biais d’un bot Teams ou d’un e-mail. Dans la messagerie, incluez des informations sur l’ajout de l’application à Teams et la prise en main.
* Soutenir l'idée d'administrateurs multiples. En d'autres termes, plusieurs utilisateurs d'une même organisation peuvent acheter et gérer leurs propres abonnements.

## <a name="build-a-landing-page-for-subscription-management"></a>Créer une page d’accueil pour la gestion des abonnements

Une fois que quelqu’un a fini d’acheter une offre d’abonnement pour votre application dans le magasin Teams, la place de marché commerciale le redirige vers votre page d’accueil où il peut gérer l’abonnement (par exemple, attribuer une licence à un utilisateur spécifique de son organisation).

Pour obtenir des instructions complètes, consultez [créer la page d’accueil de votre offre SaaS](/azure/marketplace/azure-ad-transactable-saas-landing-page).

### <a name="best-practices-for-landing-pages"></a>Meilleures pratiques pour les pages d’accueil

Tenez compte des approches suivantes lors de la création d’une page d’accueil pour l’application Teams que vous monétiser. Consultez un exemple de page d’accueil dans l'[expérience d’achat de l’utilisateur final](#end-user-purchasing-experience).

* Les utilisateurs doivent être en mesure de se connecter à votre page d’accueil avec les mêmes informations d’identification Azure AD qu’ils ont utilisées pour acheter l’abonnement. Pour plus d’informations, consultez [Azure AD et offres SaaS pouvant faire l’objet d’une transaction dans la Place de marché commerciale](/azure/marketplace/azure-ad-saas).
* Autorisez les utilisateurs à effectuer les actions suivantes sur votre page d’accueil. N’oubliez pas de prendre en compte les éléments appropriés pour un rôle d’utilisateur et des autorisations. Par exemple, vous pouvez autoriser uniquement les administrateurs d’abonnement à rechercher des utilisateurs :
  * Rechercher des utilisateurs dans leur organisation à l’aide de la messagerie électronique ou d’une autre forme d’identité.
  * Afficher les utilisateurs auxquels ils peuvent attribuer des licences dans une liste.
  * Attribuer des licences à un ou plusieurs utilisateurs en même temps.
  * Attribuer et gérer différents types de licences (le cas échéant).
  * Vérifier si une licence est déjà attribuée à un autre utilisateur.
  * Annuler l’abonnement.
* Fournissez une introduction sur l’utilisation de votre application.
* Ajoutez des moyens d’obtenir de l’aide, telles qu’une FAQ, une base de connaissances ou un e-mail de contact.
* Fournissez un lien qui permet à l’abonné de revenir facilement à la page d’accueil. Par exemple, incluez ce lien dans l’onglet **À propos** de votre application.

## <a name="create-your-saas-offer"></a>Créer votre offre SaaS

Une fois que vous avez intégré les API de traitement SaaS et créé votre page d’accueil dans laquelle les utilisateurs peuvent gérer leurs abonnements, il est temps de créer, tester et publier officiellement votre offre SaaS pouvant effectuer des transactions.

### <a name="create-the-offer"></a>Créer l’offre

Consultez [Créer une offre SaaS](/azure/marketplace/create-new-saas-offer) pour obtenir des instructions complètes sur la procédure à suivre dans Espace partenaires. Les étapes suivantes décrivent ce qu’il faut faire à un niveau élevé.

1. Créez un compte [Espace partenaires](https://partner.microsoft.com/) si vous n’en’ avez pas.

1. Configurez les offres d’abonnement, les détails de la tarification et bien plus encore pour votre offre SaaS pouvant effectuer des transactions. En particulier, veillez à effectuer les étapes suivantes :

    * Sous **Détails du programme d’installation**, sélectionnez l’option **Oui** pour spécifier que vous vendez l’offre via Microsoft.

    * Sous **Intégration à Microsoft 365**, ajoutez le lien AppSource à la liste de votre application. Cette étape permet de s’assurer que les utilisateurs peuvent acheter vos offres d’abonnement dans AppSource en plus de Teams.

1. Enregistrez vos identifiants d'éditeur et d'offre. (Vous en aurez besoin plus tard pour lier l'offre à votre application dans le portail des développeurs).

1. Publiez votre offre sur la place de marché commerciale.

### <a name="test-the-offer"></a>Tester l’offre

Nous vous recommandons de vérifier l’expérience d’achat de bout en bout avant de publier votre offre SaaS. Vous pouvez vérifier en créant une offre distincte à des fins de test. Pour plus d’informations, consultez [vue d’ensemble de l’offre de test](/azure/marketplace/plan-saas-offer#test-offer), [créer une offre de test](/azure/marketplace/create-saas-dev-test-offer)et [prévisualiser votre offre](/azure/marketplace/test-publish-saas-offer).

> [!IMPORTANT]
> Vous pouvez tester une transaction de bout en bout dans Teams à l’aide de la [Préversion de test pour la fonctionnalité d’applications monétisées](Test-preview-for-monetized-apps.md). Pour les offres en direct, vous devez terminer le processus de validation du store de l’application.

Du point de vue de Teams, ces tests doivent vérifier que le nombre de licences et d’affectations correspond à ce qu’il se passe dans le Centre d’administration Teams lorsque les utilisateurs :

* Activent et configurent leur offre d’abonnement sur votre page d’accueil.
* Attribuent, suppriment ou réaffectent des licences à eux-mêmes ou à d’autres personnes.
* Annulent ou renouvellent leur abonnement.

### <a name="publish-the-offer"></a>Publier l’offre

Une fois le test terminé, [publiez votre offre en direct](/azure/marketplace/test-publish-saas-offer#publish-your-offer-live).

## <a name="configure-your-app-for-the-saas-offer"></a>Configurer votre application pour l’offre SaaS

Vous avez publié votre offre SaaS, mais vous devez toujours la lier à votre application Teams pour que les utilisateurs voient vos plans d’abonnement dans le magasin Teams.

1. Accédez au [Portail des développeurs](https://dev.teams.microsoft.com/) et sélectionnez **Applications**.
1. Dans la page **Applications**, sélectionnez l’application à laquelle vous liez l’offre SaaS.
1. Accédez à la page **Offres et tarification** et spécifiez vos ID d’éditeur et d’offre. (Vous pouvez trouver ces ID dans Espace partenaires si vous ne les avez pas à portée de main.)
1. Sélectionnez **Afficher** pour afficher un aperçu des offres d’abonnement de votre offre SaaS.
1. Si tout semble correct, sélectionnez **Enregistrer**.

   La propriété `subscriptionOffer` est ajoutée à votre [manifeste d’application](~/resources/schema/manifest-schema-dev-preview.md#subscriptionoffer).

   ```json
      "subscriptionOffer": {
        "offerId": "publisherId.offerId"  
        }
   ```

## <a name="publish-your-app"></a>Publier votre application

Vous avez créé votre offre SaaS et l'avez liée à votre application Teams. Il est maintenant temps de publier votre application dans le magasin Teams. Pour obtenir des instructions complètes, consultez [Publier votre application dans le magasin Teams](~/concepts/deploy-and-publish/appsource/publish.md).

> [!IMPORTANT]
>
> * Même si votre application est déjà répertoriée dans le magasin Teams, vous devez toujours passer à nouveau par le processus de validation du Store pour inclure votre offre SaaS.
> * Les offres à taux fixe créées sans l’ID d’offre et l’ID de serveur de publication dans le manifeste de l’application doivent être mises à jour et soumises à nouveau pour validation.

Une fois publiés, les utilisateurs voient une option **Acheter un abonnement** dans la boîte de dialogue détails de l’application lorsqu’ils essaient d’ajouter votre application à Teams.

## <a name="end-user-purchasing-experience"></a>Expérience d’achat de l’utilisateur final

L’exemple suivant montre comment les utilisateurs peuvent souscrire à des offres d’abonnement pour une application Teams fictive appelée *Recloud*.

1. Dans le magasin Teams, recherchez et sélectionnez l’application *Recloud* .

1. Dans la boîte de dialogue Détails de l’application, sélectionnez **Acheter un abonnement**.

    :::image type="content" source="~/assets/images/saas-offer/buysubscriptionplan.png" alt-text="Achat de l’abonnement pour l’application sélectionnée.":::

1. Sélectionnez votre pays/région pour afficher les offres d’abonnement pour votre emplacement.

1. Dans la boîte de dialogue **Choisir une offre d’abonnement** , choisissez l’offre souhaitée, puis sélectionnez **Validation de l’achat**. (Remarque : les offres privés sont visibles uniquement par les utilisateurs des organisations auxquelles vous fournissez l’offre. Ces offres sont indiquées avec une icône **Offre spéciale** :::image type="icon" source="~/assets/icons/special-icon.png":::.)

    :::image type="content" source="~/assets/images/saas-offer/choosingsubscriptionplan.png" alt-text="Sélection de l’offre d’abonnement appropriée.":::

1. Dans la boîte de dialogue **Validation de l’achat**, fournissez les informations requises et sélectionnez **Passer une commande**.

    :::image type="content" source="~/assets/images/saas-offer/placesubscriptionorder.png" alt-text="Passer la commande d’abonnement.":::

1. Lorsque vous y êtes invité, sélectionnez **Configurer maintenant** pour configurer votre abonnement.

    :::image type="content" source="~/assets/images/saas-offer/saas-offer-set-up.png" alt-text="Configuration de l’abonnement.":::

1. Gérez votre offre d’abonnement via le site web *Recloud* (également appelé [page d’accueil](#build-a-landing-page-for-subscription-management)).

    :::image type="content" source="~/assets/images/saas-offer/subscriptionlicenses.png" alt-text="Configuration des licences utilisateur.":::

## <a name="admin-purchasing-experience"></a>Expérience d’achat de l’administrateur

Les administrateurs peuvent acheter des offres d’abonnement aux applications dans le [Centre d’administration Teams](/MicrosoftTeams/purchase-third-party-apps).

## <a name="remove-a-saas-offer-from-your-app"></a>Supprimer une offre SaaS de votre application

Si vous dissociez une offre SaaS incluse dans la liste de votre magasin Teams, vous devez republier votre application pour que le changement soit visible dans le magasin.

1. Accédez au [Portail des développeurs](https://dev.teams.microsoft.com/) et sélectionnez **Applications**.
1. Dans la page **Applications**, sélectionnez l’application pour laquelle vous supprimez l’offre.
1. Accédez à la page **Offres et tarification** et sélectionnez **Rétablir**.
1. Une fois l’offre dissociée, procédez comme suit pour mettre à jour votre description dans le Store :
   1. Sélectionnez **Distribuer > Publier dans le magasin Teams**.
   1. Sélectionnez **Ouvrir Espace partenaires** pour commencer le processus de republication de votre application sans l’offre.

## <a name="see-also"></a>Voir aussi

* [Maintenance et prise en charge de votre application publiée](../post-publish/overview.md)
* [Instructions de validation pour les applications liées à l’offre SaaS](teams-store-validation-guidelines.md#apps-linked-to-saas-offer)
