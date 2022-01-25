---
title: Inclure une offre SaaS avec votre application
description: Découvrez comment monétiser votre application Microsoft Teams avec des plans d’abonnement.
author: heath-hamilton
ms.author: surbhigupta
ms.topic: how-to
ms.localizationpriority: medium
ms.openlocfilehash: 597896d79408fa596e9949166fceda97ef440d07
ms.sourcegitcommit: 7209e5af27e1ebe34f7e26ca1e6b17cb7290bc06
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/25/2022
ms.locfileid: "62212004"
---
# <a name="include-a-saas-offer-with-your-microsoft-teams-app"></a>Inclure une offre SaaS avec votre application Microsoft Teams application

:::row:::
   :::column span="3":::

Avec une offre SaaS (Software-as-a-Service) transactable, vous pouvez monétiser votre application Teams en vendant des plans d’abonnement directement à partir de votre Teams store. Par exemple, dites que vous avez une application gratuite que tout le monde peut obtenir dans le Store. Vous pouvez désormais proposer des offres Premium et Entreprise aux utilisateurs qui souhaitent davantage de fonctionnalités.

Voici une idée générale de la monétisation de votre application :

1.  [Planifiez votre offre SaaS.](#plan-your-saas-offer)

1.  [Intégration avec les API SaaS Fulfillment](#integrate-with-the-saas-fulfillment-apis).

1.  [Créez une page d’accueil pour la gestion des abonnements.](#build-a-landing-page-for-subscription-management)

1.  [Créez votre offre SaaS.](#create-your-saas-offer)

1.  [Configurez votre application pour l’offre SaaS.](#configure-your-app-for-the-saas-offer)

1.  [Publiez votre application dans le Teams store.](#publish-your-app)

   :::column-end:::
   :::column span="1":::
   
:::image type="content" source="~/assets/images/saas-offer/saas-offer-diagram.png" alt-text="Diagramme montrant le processus d’inclure une offre SaaS avec votre Teams application." border="false":::

   :::column-end:::
:::row-end:::

## <a name="plan-your-saas-offer"></a>Planifier votre offre SaaS

Pour obtenir des instructions complètes, voir comment planifier une offre [SaaS pour la place de marché commerciale Microsoft.](/azure/marketplace/plan-saas-offer)

Lorsque vous planifiez la monétisation de Teams’application, voici quelques éléments à prendre en compte :

* Déterminez votre modèle d’abonnement. Une offre SaaS transactable peut inclure plusieurs plans d’abonnement. Les plans d’abonnement public disponibles pour tout le monde sont les plus courants, mais vous pouvez également cibler des clients spécifiques avec des offres uniquement pour eux. Pour plus d’informations, [consultez les offres privées sur le marketplace commercial Microsoft.](/azure/marketplace/private-offers)
* En savoir plus sur l’option de vente par le biais [ *de La*](/azure/marketplace/plan-saas-offer#listing-options) liste Microsoft pour votre offre SaaS, qui est requise si vous souhaitez que les utilisateurs achètent des plans d’abonnement pour votre application directement via le Teams store.
* Découvrez comment [Azure Active Directory l' sign-on unique (SSO)](/azure/marketplace/azure-ad-saas) permet à vos clients d’acheter et de gérer des abonnements. (Azure AD' sso est requise pour Teams applications avec des offres SaaS.)
* Comprenez que vous êtes responsable de la gestion et du paiement de l’infrastructure requise pour prendre en charge l’utilisation de votre offre SaaS par vos clients.
* Planifiez l’utilisation des appareils mobiles. Pour éviter de violer les stratégies du Magasin d’applications tiers, votre application ne peut pas inclure de liens qui permettent aux utilisateurs d’acheter des plans d’abonnement sur un appareil mobile. Toutefois, vous pouvez toujours indiquer si votre application comporte des fonctionnalités qui nécessitent un plan d’abonnement. Pour plus d’informations, voir les [stratégies de certification de marketplace commerciales associées.](/legal/marketplace/certification-policies#114048-mobile-experience)

## <a name="integrate-with-the-saas-fulfillment-apis"></a>Intégration avec les API SaaS Fulfillment

L’intégration aux API SaaS Fulfillment est nécessaire pour monétiser votre Teams application. Ces API vous aident à gérer le cycle de vie d’un plan d’abonnement une fois qu’il est acheté par un utilisateur.

Pour obtenir des instructions complètes et des références d’API, consultez la documentation des [API SaaS Fulfillment.](/azure/marketplace/partner-center-portal/pc-saas-fulfillment-apis) En règle générale, vous devez implémenter les étapes suivantes à l’aide des API une fois qu’un abonnement est acheté :

1. Recevoir un [*jeton d’identification d’achat*](/azure/marketplace/partner-center-portal/pc-saas-fulfillment-life-cycle#purchased-but-not-yet-activated-pendingfulfillmentstart) via l’URL de votre page d’accueil.

1. Utilisez le jeton pour récupérer les détails de l’abonnement.

1. Informez la place de marché commerciale que l’abonnement est activé.

### <a name="best-practices-for-implementing-subscription-management"></a>Meilleures pratiques pour l’implémentation de la gestion des abonnements

* Avec les offres SaaS transactables pour les applications Teams, les plans d’abonnement (licences) doivent être attribués à des utilisateurs individuels plutôt qu’à des groupes ou à une organisation entière.
* Lorsque des utilisateurs se voit attribuer un plan d’abonnement, informez-les par Teams robot ou par courrier électronique. Dans la messagerie, incluez des informations sur la façon d’ajouter l’application à Teams et de commencer.
* Prise en charge de l’idée de plusieurs administrateurs. En d’autres termes, plusieurs utilisateurs de la même organisation peuvent acheter et gérer leurs propres abonnements.

## <a name="build-a-landing-page-for-subscription-management"></a>Créer une page d’accueil pour la gestion des abonnements 

Lorsqu’une personne a terminé d’acheter un plan d’abonnement pour votre application dans le magasin Teams, la place de marché commerciale l’dirige vers votre page d’accueil où elle peut gérer l’abonnement (par exemple, attribuer une licence à un utilisateur spécifique dans son organisation).

Pour obtenir des instructions complètes, [voir créer la page d’accueil de votre offre SaaS.](/azure/marketplace/azure-ad-transactable-saas-landing-page)

### <a name="best-practices-for-landing-pages"></a>Meilleures pratiques pour les pages d’arrivée

Envisagez les approches suivantes lors de la création d’une page d’accueil Teams’application que vous monétisez. Consultez un exemple de page d’accueil dans [l’expérience d’achat de l’utilisateur final.](#end-user-purchasing-experience)

* Les utilisateurs doivent être en mesure de se connecter à votre page d’accueil avec les mêmes informations d’Azure AD qu’ils ont utilisées pour acheter l’abonnement. Pour plus d’informations, [voir Azure AD et les offres SaaS transactables sur le marché commercial.](/azure/marketplace/azure-ad-saas)
* Autorisez les utilisateurs à prendre les mesures suivantes sur votre page d’accueil. N’oubliez pas de considérer ce qui est approprié pour le rôle et les autorisations d’un utilisateur (par exemple, vous pouvez autoriser uniquement les administrateurs d’abonnement à rechercher des utilisateurs) :
  * Recherchez des utilisateurs dans leur organisation à l’aide de la messagerie électronique ou d’une autre forme d’identité.
  * Consultez les utilisateurs à qui ils peuvent attribuer des licences dans une liste.
  * Attribuer des licences à un ou plusieurs utilisateurs en même temps.
  * Attribuer et gérer différents types de licences (si disponible).
  * Vérifier si une licence est déjà attribuée à un autre utilisateur.
  * Annulez leur abonnement.
* Présentation de l’utilisation de votre application.
* Ajoutez des façons d’obtenir de l’aide, telles qu’un FORUM AUX QUESTIONS, une base de connaissances ou un message électronique de contact.
* Fournissez un lien qui permet à l’abonné de revenir facilement à la page d’accueil. Par exemple, incluez ce lien dans l’onglet À propos **de votre** application.

## <a name="create-your-saas-offer"></a>Créer votre offre SaaS

Une fois que vous avez intégré les API SaaS Fulfillment et créé votre page d’accueil dans laquelle les utilisateurs peuvent gérer leurs abonnements, il est temps de créer, tester et publier officiellement votre offre SaaS gérable.

> [!IMPORTANT]
> Teams ne prend actuellement en **charge** que le modèle de tarification Par utilisateur (utilisateur/mois et utilisateur/année) pour les offres SaaS. Pour plus d’informations, voir [les modèles de tarification SaaS.](/azure/marketplace/plan-saas-offer#saas-pricing-models)

### <a name="create-the-offer"></a>Créer l’offre

Voir [créer une offre SaaS pour](/azure/marketplace/create-new-saas-offer) obtenir des instructions complètes sur la façon de le faire dans l’Espace partenaires. Les étapes suivantes décrivent ce qu’il faut faire à un niveau élevé.

1.  Créez [un compte Espace](https://partner.microsoft.com/) partenaires si vous n’en avez pas.

1.  Configurez les plans d’abonnement, les détails des tarifs et bien plus encore pour votre offre SaaS transactable. En particulier, veillez à effectuer les étapes suivantes :

    * Sous **Détails du programme** d’installation, sélectionnez l’option **Oui** pour spécifier que vous vendez l’offre via Microsoft.
     
    * Sous **Microsoft 365'intégration,** ajoutez le lien AppSource à la liste de votre application. Cette étape garantit que les personnes peuvent acheter vos plans d’abonnement dans AppSource en plus de Teams.

1. Stockez votre éditeur et proposez des ID. (Vous en aurez besoin ultérieurement pour lier l’offre à votre application dans le portail du développeur.)

1. Publiez votre offre sur le marché commercial.

### <a name="test-the-offer"></a>Tester l’offre

Nous vous recommandons vivement de vérifier l’expérience d’achat de bout en bout avant de publier votre offre SaaS. Pour ce faire, créez une offre distincte uniquement pour le test. Pour plus d’informations, consultez [la vue d’ensemble de l’offre](/azure/marketplace/plan-saas-offer#test-offer) [de test, créez une](/azure/marketplace/create-saas-dev-test-offer)offre de test et [prévisualiser votre offre.](/azure/marketplace/test-publish-saas-offer)

> [!IMPORTANT]
> Vous devez tester votre offre SaaS transactable dans AppSource. Actuellement, vous ne pouvez pas tester une transaction de bout en bout dans Teams tant que votre application n’a pas terminé la validation du Store.

Du point de Teams, ces tests doivent vérifier que le nombre de licences et d’affectations correspond à ce qui se passe dans le Centre d’administration Teams lorsque les utilisateurs :

* Activez et configurez leur plan d’abonnement sur votre page d’accueil.
* Attribuer, supprimer ou réaffecter des licences à eux-mêmes ou à d’autres personnes.
* Annuler ou renouveler son abonnement.

### <a name="publish-the-offer"></a>Publier l’offre

Une fois que vous avez terminé le test, [publiez votre offre en direct.](/azure/marketplace/test-publish-saas-offer#publish-your-offer-live)

## <a name="configure-your-app-for-the-saas-offer"></a>Configurer votre application pour l’offre SaaS

Vous avez publié votre offre SaaS, mais vous devez toujours la lier à votre application Teams pour que les utilisateurs voient vos plans d’abonnement dans le Teams store.

1. Go to the [Developer Portal](https://dev.teams.microsoft.com/) and select **Apps**.
1. Dans la page **Applications,** sélectionnez l’application à qui vous liez l’offre SaaS.
1. Go to the **Plans and pricing** page and specify your publisher and offer IDs. (Vous pouvez trouver ces ID dans l’Partner Center si vous ne les avez pas disponibles.)
1. Sélectionnez **Afficher** pour afficher un aperçu des plans d’abonnement de votre offre SaaS.
1. Si tout semble bien, sélectionnez **Enregistrer.**

   La `subscriptionOffer` propriété est ajoutée au manifeste de votre [application.](~/resources/schema/manifest-schema-dev-preview.md#subscriptionoffer)

   ```json
      "subscriptionOffer": {
        "offerId": "publisherId.offerId"  
        }
   ```

## <a name="publish-your-app"></a>Publier votre application

Vous avez créé votre offre SaaS et l’avez liée à votre application Teams. Il est maintenant temps de publier votre application dans le Teams store. Pour obtenir des instructions complètes, voir [publier votre application dans le Teams store.](~/concepts/deploy-and-publish/appsource/publish.md)

> [!IMPORTANT]
> Même si votre application est déjà répertoriée dans le magasin Teams, vous devez toujours passer par le processus de validation du Store pour inclure votre offre SaaS.

Une fois publié, les utilisateurs voient une **option** Acheter un abonnement dans la boîte de dialogue détails de l’application lorsqu’ils essaient d’ajouter votre application à Teams.

## <a name="end-user-purchasing-experience"></a>Expérience d’achat de l’utilisateur final

L’exemple suivant montre comment les utilisateurs peuvent acheter des plans d’abonnement pour une application Teams fictive appelée *Recloud*.

1. Dans le Teams, recherchez et sélectionnez *l’application Recloud.*

1. Dans la boîte de dialogue Détails de l’application, **sélectionnez Acheter un abonnement.**

    :::image type="content" source="~/assets/images/saas-offer/buysubscriptionplan.png" alt-text="Achat de l’abonnement pour l’application sélectionnée.":::

1. Sélectionnez votre pays pour consulter les plans d’abonnement pour votre emplacement.

1. Dans la **boîte de dialogue Choisir un plan d’abonnement,** choisissez l’offre de votre choix et sélectionnez **Checkout**. (Remarque : les plans privés sont visibles uniquement pour les utilisateurs des organisation à qui vous proposez l’offre. Ces offres sont indiquées avec une **icône d’offre** :::image type="icon" source="~/assets/icons/special-icon.png"::: spéciale.)

    :::image type="content" source="~/assets/images/saas-offer/choosingsubscriptionplan.png" alt-text="Sélection du plan d’abonnement approprié.":::

1. Dans la **boîte de dialogue d’checkout,** fournissez toutes les informations requises et sélectionnez **Commande .**

    :::image type="content" source="~/assets/images/saas-offer/placesubscriptionorder.png" alt-text="Passer la commande d’abonnement.":::

1. Lorsque vous y est invité, **sélectionnez Configurer maintenant** pour configurer votre abonnement.

    :::image type="content" source="~/assets/images/saas-offer/saas-offer-set-up.png" alt-text="Configuration de l’abonnement.":::

1. Gérez votre plan d’abonnement via le site web *Recloud* (également appelé [page d’accueil).](#build-a-landing-page-for-subscription-management)

    :::image type="content" source="~/assets/images/saas-offer/subscriptionlicenses.png" alt-text="Configuration des licences utilisateur.":::

## <a name="admin-purchasing-experience"></a>Expérience d’achat de l’administrateur

Les administrateurs peuvent acheter des plans d’abonnement d’application [dans Teams centre d’administration.](/MicrosoftTeams/purchase-third-party-apps)

## <a name="remove-a-saas-offer-from-your-app"></a>Supprimer une offre SaaS de votre application

Si vous dissociez une offre SaaS incluse dans votre Teams store, vous devez republier votre application pour voir la modification dans le Store.

1. Go to the [Developer Portal](https://dev.teams.microsoft.com/) and select **Apps**.
1. Dans la page **Applications,** sélectionnez l’application dont vous supprimez l’offre.
1. Go to the **Plans and pricing** page and select **Revert**.
1. Une fois que l’offre n’est pas liée, faites les choses suivantes pour mettre à jour votre liste dans le Store :
   1. Sélectionnez **Distribuer > publier dans le Teams store.**
   1. Sélectionnez **Ouvrir l’Espace** partenaires pour commencer le processus de republier votre application sans l’offre.

## <a name="see-also"></a>Voir aussi

[Maintenance et prise en charge de votre application publiée](../post-publish/overview.md)
