---
title: Flux d’achats intégrés pour la monétisation des applications
description: Apprenez les tâches et les concepts de base nécessaires pour mettre en œuvre les achats in-app et la fonctionnalité d'essai dans les applications d'équipe.
author: v-npaladugu
ms.author: surbhigupta
ms.topic: how-to
ms.localizationpriority: high
ms.openlocfilehash: 1dd557190ef6faa3afa6ab477f7e8b22c9cd0e12
ms.sourcegitcommit: 1248901a5e59db67bae091f60710aabe7562016a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/13/2022
ms.locfileid: "68560707"
---
# <a name="in-app-purchases"></a>Achats dans l'application

Microsoft Teams fournit des API que vous pouvez utiliser pour implémenter les achats in-app afin de passer de la version gratuite à la version payante Teams applications. L'achat in-app vous permet de faire passer les utilisateurs d'une formule gratuite à une formule payante directement à partir de votre application.

## <a name="implement-in-app-purchases"></a>Implémenter des achats dans l’application

Pour proposer une expérience d’achat in-app aux utilisateurs de votre application, assurez-vous que :

* L’application repose sur [Teams bibliothèque du SDK client](https://github.com/OfficeDev/microsoft-teams-library-js).

* L’application est activée avec une offre [SaaS négociable](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md).

* L’application est activée avec [les autorisations RSC](#update-manifest).

* L’application est invoquée avec [l’API`openPurchaseExperience`](#purchase-experience-api).

L’expérience d’achat dans l’application peut être activée soit en mettant à jour le fichier  `manifest.json`, soit en activant **afficher les offres d’achat** dans l’application à partir de la section **Autorisations** de votre **portail du développeur**.

### <a name="update-manifest"></a>Mise à jour du manifeste

Pour activer l’expérience d’achat dans l’application, mettez à jour Teams fichier `manifest.json` de l’application en ajoutant les autorisations RSC. Il permet aux utilisateurs de votre application de passer à une version payante de votre application et de commencer à utiliser de nouvelles fonctionnalités. La mise à jour du manifeste de l’application est la suivante :

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

Pour déclencher l'achat in-app pour l'application, invoquez `openPurchaseExperience`l'API depuis votre application web.

L’extrait de code suivant est un exemple d’appel de l’API à partir de l’application Teams générée à l’aide du Kit de développement logiciel (SDK) client JavaScript Teams :

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/jsonV11)

```json
<div> 
<div class="sectionTitle">openPurchaseExperience</div>
<button onclick="openPurchaseExperience()">openPurchaseExperience</button>
</div>
</body>
<script>
   function openPurchaseExperience()
      microsoftTeams.initialize();
      let callbackcalled = false;
      microsoftTeams.monetization.openPurchaseExperience((e) => {
            console.log("callback is being called");
            console.log(e);
            if (!!e && typeof e !== "string") {
                  alert(JSON.stringify(e));
              }
              return;
            });
      console.log("after callback: ",callbackcalled);
    }
</script>
```

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/jsonV2)

```json
<div>
<div class="sectionTitle">openPurchaseExperience</div>
<button onclick="openPurchaseExperience()">openPurchaseExperience</button>
</div>
</body>
<script>
    function openPurchaseExperience() {
      micorosftTeams.app.initialize();
      var planInfo = {
          planId: "<Plan id>", // Plan Id of the published SAAS Offer
          term: "<Plan Term>" // Term of the plan.
      }
      monetization.openPurchaseExperience(planInfo);
    }
</script>
```

---

## <a name="end-user-in-app-purchasing-experience"></a>Expérience d’achat dans l’application de l’utilisateur final

L’exemple suivant montre aux utilisateurs d’acheter des plans d’abonnement pour une application Teams fictive appelée *Tâches Contoso pour Teams* :

1. Dans le Teams **Store**, recherchez et sélectionnez l’application.

1. Dans la boîte de dialogue Détails de l’application, **sélectionnez Acheter un abonnement** ou **Ajouter pour moi**.

    :::image type="content" source="~/assets/images/saas-offer/buysubscriptionplancontoso.png" alt-text="Achat de l’abonnement pour l’application sélectionnée.":::

1. **Add for me** propose une version d’essai gratuite de l’application, puis la **met à niveau** vers une version payante.

    :::image type="content" source="~/assets/images/saas-offer/upgradeapp.png" alt-text="Mise à niveau vers l’abonnement pour l’application sélectionnée." lightbox="../../../../assets/images/saas-offer/upgradeapp.png":::

1. Dans la boîte de dialogue **Choisir un plan d’abonnement** , choisissez le plan et sélectionnez **Validation de l’achat**.

    :::image type="content" source="~/assets/images/saas-offer/choosingsubscriptionplancontoso.png" alt-text="Sélection du plan d’abonnement approprié" lightbox="../../../../assets/images/saas-offer/choosingsubscriptionplancontoso.png":::

1. Terminez la transaction et **sélectionnez Configurer maintenant** pour configurer votre abonnement.

    :::image type="content" source="~/assets/images/saas-offer/saas-offer-configure-now.png" alt-text="Configuration de l’abonnement" lightbox="../../../../assets/images/saas-offer/saas-offer-configure-now.png":::

    :::image type="content" source="~/assets/images/saas-offer/getstarted.png" alt-text="Page d’accueil de l’abonnement" lightbox="../../../../assets/images/saas-offer/getstarted.png":::

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Aperçu du test pour les applications monétisées](~/concepts/deploy-and-publish/appsource/prepare/Test-preview-for-monetized-apps.md)

## <a name="see-also"></a>Voir aussi

* [Inclure une offre SaaS avec votre application Microsoft Teams](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md)
* [Créer une offre SaaS (Software as a Service)](include-saas-offer.md#create-your-saas-offer)
