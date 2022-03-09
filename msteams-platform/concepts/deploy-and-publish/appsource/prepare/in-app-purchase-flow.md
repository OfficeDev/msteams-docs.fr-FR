---
title: Flux d’achat dans l’application pour la monétisation des applications
description: Découvrez les tâches et concepts de base nécessaires pour implémenter des achats in-app et des fonctionnalités d’essai dans les applications Teams.
author: v-npaladugu
ms.author: surbhigupta
ms.topic: how-to
localization_priority: Normal
ms.openlocfilehash: 059322af212641988560853caf3d5a495e36f674
ms.sourcegitcommit: 2fdca6fb0ade3f6b460eb9a4dfea0a8e2ab8d3b9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/08/2022
ms.locfileid: "63356469"
---
# <a name="in-app-purchases"></a>Achats dans l'application

Microsoft Teams des API que vous pouvez utiliser pour implémenter les achats in-app afin de passer de la version gratuite à la version payante Teams applications. L’achat dans l’application vous permet de convertir des utilisateurs de plans gratuits en plans payants directement à partir de votre application.

> [!NOTE]
> Les achats in-app pour Teams applications sont actuellement disponibles uniquement en [**prévisualisation développeur**](/microsoftteams/platform/resources/dev-preview/developer-preview-intro).

## <a name="implement-in-app-purchases"></a>Implémenter des achats dans l’application

Pour proposer une expérience d’achat in-app aux utilisateurs de votre application, assurez-vous que :

* L’application repose sur [Teams bibliothèque du SDK client](https://github.com/OfficeDev/microsoft-teams-library-js).

* L’application est activée avec une offre [SaaS transactable](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md).

* L’application est activée avec [les autorisations RSC](#update-manifest).

* L’application est invoquée avec [l’API`openPurchaseExperience`](#purchase-experience-api).

L’expérience d’achat dans l’application peut être activée soit en mettant à jour le fichier  **manifest.json**, soit en activant afficher les offres d’achat dans l’application à partir de la section **Autorisations** de votre **portail du développeur**.

### <a name="update-manifest"></a>Mettre à jour le manifeste

Pour activer l’expérience d’achat dans l’application, mettez à jour Teams fichier **manifest.json** de l’application en ajoutant les autorisations RSC. Il permet aux utilisateurs de votre application de mettre à niveau vers une version payante de votre application et de commencer à utiliser de nouvelles fonctionnalités. La mise à jour du manifeste de l’application est la suivante :

```json

"authorization": {
    "permissions": {
        "resourceSpecific": [
            {
                "name": "InAppPurchase.Allow.User",
                "type": "Delegated"
            }
        ]
    }
}
```

### <a name="purchase-experience-api"></a>API Expérience d’achat

Pour déclencher l’achat in-app de l’application, invoke the `openPurchaseExperience` API from your web app.

Voici un exemple d’appel de l’API à partir de l’application :

```json
<body> 
<div> 
<div class="sectionTitle">openPurchaseExperience</div> 
<button onclick="openPurchaseExperience()">openPurchaseExperience</button> 
</div> 
</body> 
<script> 
   function openPurchaseExperience() {
      microsoftTeams.initialize();
      let callbackcalled = false;
      microsoftTeams.monetization.openPurchaseExperience((e) => {
      console.log("callback is being called");
      callbackcalled = true;  
      if (!!e && typeof e !== "string") {
            e = JSON.stringify(e);
            alert(e);
        }
        return;
      });
      console.log("after callback: ",callbackcalled);
    } 
</script> 
```

## <a name="end-user-in-app-purchasing-experience"></a>Expérience d’achat dans l’application de l’utilisateur final

L’exemple suivant montre aux utilisateurs d’acheter des plans d’abonnement pour une application Teams fictive appelée *Tâches Contoso pour Teams* :

1. Dans le Teams **Store**, recherchez et sélectionnez l’application.

1. Dans la boîte de dialogue Détails de l’application, **sélectionnez Acheter un abonnement** ou **Ajouter pour moi**.

    :::image type="content" source="~/assets/images/saas-offer/buysubscriptionplancontoso.png" alt-text="Achat de l’abonnement pour l’application sélectionnée." border="true":::

1. **Add for me** propose une version d’essai gratuite de l’application, puis la met à niveau vers une version payante.

    :::image type="content" source="~/assets/images/saas-offer/upgradeapp.png" alt-text="Mise à niveau vers l’abonnement pour l’application sélectionnée." lightbox="../../../../assets/images/saas-offer/upgradeapp.png" border="true":::

1. Dans la **boîte de dialogue Choisir un plan d’abonnement** , choisissez le plan et sélectionnez **Checkout**.

    :::image type="content" source="~/assets/images/saas-offer/choosingsubscriptionplancontoso.png" alt-text="Sélection du plan d’abonnement approprié." lightbox="../../../../assets/images/saas-offer/choosingsubscriptionplancontoso.png" border="true":::

1. Terminez la transaction et **sélectionnez Configurer maintenant** pour configurer votre abonnement.

    :::image type="content" source="~/assets/images/saas-offer/saas-offer-configure-now.png" alt-text="Configuration de l’abonnement." lightbox="../../../../assets/images/saas-offer/saas-offer-configure-now.png" border="true":::

    :::image type="content" source="~/assets/images/saas-offer/getstarted.png" alt-text="Page d’accueil de l’abonnement." lightbox="../../../../assets/images/saas-offer/getstarted.png" border="true":::

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Aperçu du test pour les applications monétisées](~/concepts/deploy-and-publish/appsource/prepare/Test-preview-for-monetized-apps.md)

## <a name="see-also"></a>Voir aussi

* [Inclure une offre SaaS avec votre application Microsoft Teams application](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md)
* [Créer une offre SaaS (Software as a Service)](include-saas-offer.md#create-your-saas-offer)
