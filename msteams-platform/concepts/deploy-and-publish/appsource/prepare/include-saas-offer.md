---
title: Inclure une offre SaaS avec votre application
description: Découvrez comment monétiser votre application Microsoft Teams en vendant des plans d’abonnement directement à partir de votre description dans le Windows Store Teams. Comprendre l’expérience d’achat de l’application de publication, de l’utilisateur final et de l’administrateur.
author: heath-hamilton
ms.author: surbhigupta
ms.topic: how-to
ms.localizationpriority: high
ms.openlocfilehash: 23327ea2765eb5496f8cfb157cdd194fcc13aaf7
ms.sourcegitcommit: edfe85e312c73e34aa795922c4b7eb0647528d48
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/30/2022
ms.locfileid: "68243254"
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
* Considérez qu’il y aura plusieurs administrateurs. En d’autres termes, plusieurs utilisateurs de la même organisation peuvent acheter et gérer leurs propres abonnements.

## <a name="manage-license-for-third-party-apps-in-teams"></a>Gérer la licence pour les applications tierces dans Teams

Teams permet aux administrateurs ou aux utilisateurs éditeurs de logiciels indépendants de gérer les licences SaaS pour les applications tierces achetées à partir de la vitrine Teams. Les administrateurs ou utilisateurs d’éditeurs de logiciels indépendants peuvent facilement attribuer, annuler l’affectation, utiliser et suivre les licences SaaS.

Pour activer la gestion des licences pour une application dans Teams, procédez comme suit :

1. [Créer une offre dans l’Espace partenaires](#create-an-offer-in-partner-center)
1. [Mettre à jour votre application Teams](#update-your-teams-app)
1. [Après l’achat](#post-purchase)
1. [Intégrer à l’API de droite d’utilisation de Graph](#integrate-with-graph-usage-right-api)

### <a name="create-an-offer-in-partner-center"></a>Créer une offre dans l’Espace partenaires

1. Connectez-vous à [l’Espace partenaires](https://partner.microsoft.com/) et sélectionnez **Espace partenaires**.

   :::image type="content" source="~/assets/images/first-party-license-mgt/partner-center-home-page.png" alt-text="Les captures d’écran montrent comment se connecter au compte Espace partenaires.":::

1. Dans la page **d’accueil** , sélectionnez l’onglet Offres de la **Place de marché** pour définir les offres de la Place de marché commerciale.

   :::image type="content" source="~/assets/images/first-party-license-mgt/home-page.png" alt-text="Les captures d’écran montrent la page d’accueil et l’onglet Offre de la Place de marché dans l’Espace partenaires.":::

1. Sélectionnez **Vue d’ensemble** dans le volet gauche.

1. Sélectionnez **Nouveau logiciel d’offre** > **en tant que service**.

   :::image type="content" source="~/assets/images/first-party-license-mgt/commercial-marketplace.png" alt-text="Les captures d’écran montrent la page de l’offre de la Place de marché dans laquelle vous pouvez sélectionner une nouvelle offre.":::

1. Entrez **l’ID d’offre** et **l’alias d’offre** , puis **sélectionnez Créer**.

   > [!NOTE]
   > Si vous créez une offre à des fins de test, ajoutez le texte **-ISVPILOT** à la fin de votre alias d’offre. Cela indique à l’équipe de certification que l’offre est à des fins de test. Microsoft supprime régulièrement des offres avec **-ISVPILOT** . Par conséquent, n’utilisez pas cette balise pour d’autres raisons que le test de la fonctionnalité de gestion des licences.

   :::image type="content" source="~/assets/images/first-party-license-mgt/saas.png" alt-text="Les captures d’écran montrent comment entrer l’ID d’offre et l’alias d’offre dans l’Espace partenaires.":::

1. Dans la page d’installation de l’offre, sous détails de l’installation, cochez la case **Oui, je souhaite que Microsoft gère les licences client en mon nom**.

   :::image type="content" source="~/assets/images/first-party-license-mgt/saas-isvpilot.png" alt-text="Les captures d’écran montrent la page d’installation de l’offre pour configurer la licence à gérer pour votre application dans Teams.":::

   > [!NOTE]
   >
   > * Il s’agit d’un paramètre unique que vous ne pouvez pas modifier une fois votre offre publiée. Cela permet au client de gérer les licences de votre application dans Teams.
   > * Le manifeste d’application ne prend en charge qu’une seule offre pour une application. Choisissez une solution de gestion des licences appropriée pour tous les plans disponibles dans votre offre et vous ne pouvez pas modifier cette option une fois l’offre mise en ligne.

1. Sélectionnez **Enregistrer le brouillon**.

1. Sélectionnez **Vue d’ensemble du plan** dans le volet gauche, puis **sélectionnez Créer un plan**.

   > [!NOTE]
   > Vous devez ajouter au moins un plan.

   :::image type="content" source="~/assets/images/first-party-license-mgt/plan-overview.png" alt-text="Les captures d’écran montrent une vue d’ensemble du plan pour créer un plan pour vos applications dans l’Espace partenaires.":::

1. Entrez l’ID de plan et le nom du plan, puis sélectionnez **Créer**.

1. Entrez le **nom du plan** et la **description du plan**.

   > [!NOTE]
   > Les informations de plan s’affichent sur la Place de marché Teams et [Appsource](https://appsource.microsoft.com/) sous la liste des offres (section plans).

   :::image type="content" source="~/assets/images/first-party-license-mgt/plan-listing.png" alt-text="Les captures d’écran affichent la page du plan pour ajouter le nom du plan et la description du plan pour votre application.":::

1. Sélectionnez **Enregistrer le brouillon**.

1. Sélectionnez **Tarification et disponibilité** dans le volet gauche.

1. Ajoutez des détails sur la tarification et la disponibilité.

   :::image type="content" source="~/assets/images/first-party-license-mgt/pricing-availability.png" alt-text="Les captures d’écran montrent la page de tarification et de disponibilité pour ajouter une offre SaaS pour votre application.":::

1. Sélectionnez **Enregistrer le brouillon**.

1. Sélectionnez **Vue d’ensemble du plan** en haut de la page pour accéder à la page de liste qui affiche tous les plans que vous avez créés pour cette offre.

   :::image type="content" source="~/assets/images/first-party-license-mgt/list-of-plans-created.png" alt-text="Les captures d’écran montrent la page de liste des plans avec l’ID de service, le modèle tarifaire, la disponibilité, l’état et l’action.":::

1. Copiez l’ID de service du plan que vous avez créé pour l’intégrer à l’API Microsoft Graph Usage Rights.

### <a name="update-your-teams-app"></a>Mettre à jour votre application Teams

Mettez à jour votre application Teams pour la mapper aux fonctionnalités payantes et [mapper votre application Teams](https://aka.ms/TMTG) à votre offre et publier.

### <a name="post-purchase"></a>Après l’achat

1. Après l’activation, le client est redirigé de la page d’accueil vers la gestion des licences Teams.

1. Une fois l’achat de l’abonnement terminé, le client est redirigé vers la page d’accueil de l’application pour l’activation de l’abonnement. Il s’agit de l’expérience existante pour l’achat [d’applications monétisées par](https://aka.ms/TMTG) l’utilisateur dans Teams.

1. Une fois que le client a activé l’achat d’abonnement sur la page d’accueil, le client est redirigé vers la page abonnements dans Teams via un lien [d’URL de redirection](https://teams.microsoft.com/_#/subscriptionManagement) ou un bouton que le client sélectionne sur la page d’accueil de l’éditeur.

### <a name="integrate-with-graph-usage-right-api"></a>Intégrer à l’API de droite d’utilisation de Graph

Intégrer à l’API Graph Usage Right pour gérer les autorisations utilisateur au moment du lancement de l’application par un client disposant d’une licence d’achat. Vous devez déterminer les autorisations de l’utilisateur pour l’application avec un appel Graph à l’API Droits d’utilisation.

Vous pouvez appeler les API Graph pour déterminer si l’utilisateur actuellement connecté avec un abonnement valide du plan a accès à votre application. Pour appeler l’API Graph UsageRight pour vérifier les autorisations utilisateur, procédez comme suit :

1. Obtenir un jeton OBO utilisateur : [obtenir l’accès pour le compte d’un utilisateur - Microsoft Graph | Microsoft Docs](/graph/auth-v2-user).

1. Appeler Graph pour obtenir l’ID d’objet de l’utilisateur : [utiliser microsoft API Graph - Microsoft Graph | Microsoft Docs](/graph/use-the-api).

1. Appeler l’API UsageRights pour déterminer que l’utilisateur dispose d’une licence pour le plan [List user usageRights - Microsoft Graph beta | Microsoft Docs](/graph/api/user-list-usagerights?view=graph-rest-beta&tabs=http&preserve-view=true).

   > [!NOTE]
   > Vous devez disposer des autorisations minimales `User.Read` pour appeler UsageRights.
   > L’API UsageRights est actuellement en version bêta. Une fois la version mise à jour vers V1, les utilisateurs de l’éditeur de logiciels indépendants doivent passer de la version bêta à la version V1.

### <a name="check-license-usage-in-partner-center-analytics"></a>Vérifier l’utilisation des licences dans l’analytique de l’Espace partenaires

1. Connectez-vous à l’[Espace partenaires](https://partner.microsoft.com/).
1. Dans le volet gauche, accédez à **La Place de marché commerciale > Analyser les licences >**.
1. Sélectionnez **Plan et Locataire** dans le widget de création de rapports pour voir l’utilisation du mois.

## <a name="build-a-landing-page-for-subscription-management"></a>Créer une page d’accueil pour la gestion des abonnements

Une fois que quelqu’un a fini d’acheter une offre d’abonnement pour votre application dans le magasin Teams, la place de marché commerciale le redirige vers votre page d’accueil où il peut gérer l’abonnement (par exemple, attribuer une licence à un utilisateur spécifique de son organisation).

Sélectionnez **Non, je préfère gérer moi-même les licences client** dans de tels cas.

Pour obtenir des instructions complètes, consultez [créer la page d’accueil de votre offre SaaS](/azure/marketplace/azure-ad-transactable-saas-landing-page).

Une fois que quelqu’un a fini d’acheter un plan d’abonnement pour votre application et souhaite rester dans Teams, sans le diriger vers votre page d’accueil, sélectionnez **Oui, j’aimerais que Microsoft gère les licences client en mon nom**.

Pour plus d’informations, consultez [la gestion des licences](/platform/concepts/deploy-and-publish/appsource/prepare/first-party-license-management) internes.

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

1. Stockez vos ID d’éditeur et d’offre. (Vous en aurez besoin plus tard pour lier l’offre à votre application dans le Portail des développeurs.)

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
