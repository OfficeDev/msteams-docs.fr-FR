---
title: Aperçu de test pour les applications monétisées
author: v-ypalikila
description: Créez et testez des offres SaaS Preview pour Teams application avant de la mettre en direct.
ms.topic: conceptual
ms.author: v-ypalikila
ms.localizationpriority: medium
keywords: teams apps SaaS offer preview offer test preview monetized saas
ms.openlocfilehash: 849dd2ecd79a4b43d6feb6ceaca599f371df1de1
ms.sourcegitcommit: 54f6690b559beedc330b971618e574d33d69e8a8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/03/2022
ms.locfileid: "62363443"
---
# <a name="test-preview-for-monetized-apps"></a>Aperçu de test pour les applications monétisées

> [!NOTE]
> La prévisualisation des tests pour les applications monétisées est actuellement disponible uniquement en [**version préliminaire développeur**](/microsoftteams/platform/resources/dev-preview/developer-preview-intro).

Vous pouvez créer une offre SaaS (Software as a Service) et tester l’expérience d’achat de bout en bout pour vos applications monétisées dans Teams. Les utilisateurs qui sont ajoutés en tant qu’audience d’aperçu pour l’application Teams peuvent consulter votre offre SaaS avant de publier.

## <a name="create-a-preview-offer-id"></a>Créer un ID d’offre d’aperçu

Vous pouvez générer l’ID d’offre d’aperçu à partir du lien **d’aperçu d’AppSource** dans l’Partner Center. Assurez-vous que l’offre SaaS est en phase de création d’aperçu. Pour générer l’ID de l’offre d’aperçu :

1. Go to [Partner Center](https://go.microsoft.com/fwlink/?linkid=2166002) and sign in using your developer credentials.
1. Sélectionnez **les offres Marketplace**.
1. Sélectionnez l’offre SaaS que vous souhaitez prévisualiser.
1. Ajoutez une [audience d’aperçu](/azure/marketplace/create-new-saas-offer-preview) pour votre offre SaaS.
1. **Sélectionnez le lien** d’aperçu AppSource sous **Go Live** pour trouver l’ID d’offre d’aperçu dans la barre d’adresses du navigateur avec *le format publisherId.offerId-preview*.

    :::image type="content" source="../../../../assets/images/apps-in-meetings/publish-status-publisher-signoff.png" alt-text="ID de l’offre d’aperçu" border="true" :::

1. Copiez l’ID de l’offre d’aperçu à partir de la barre d’adresses du navigateur.

      :::image type="content" source="../../../../assets/images/apps-in-meetings/test-preview-monetized-apps-preview-offer-id.png" alt-text="ID de l’offre d’aperçu" border="true" :::

    > [!NOTE]
    > Contrairement à un ID d’offre publique, l’ID de l’offre d’aperçu peut être reconnu avec le suffixe *-preview* . Par exemple, **publisherId.offerId-preview**.

## <a name="configure-your-app-with-the-preview-offer-id"></a>Configurer votre application avec l’ID d’offre d’aperçu

Avant de commencer, connectez-vous  au portail du développeur à l’aide d’un compte de développeur avec une **audience** d’aperçu pour que les utilisateurs voient vos plans d’abonnement dans Teams store.

Une fois que vous avez généré votre ID d’offre d’aperçu, liez l’ID de l’offre à Teams application. Pour lier l’ID de l’offre :

1. Go to [Developer Portal](https://dev.teams.microsoft.com/) and sign in using your developer credentials.
1. **Sélectionnez Applications** dans le volet gauche.
1. Sélectionnez l’application à qui lier l’offre SaaS.
1. **Sélectionnez les plans et les tarifs**, **puis entrez l Publisher et** **l’ID d’offre**.  
  Assurez-vous que l’ID de l’offre contient le suffixe *-preview* .
1. Sélectionnez **Afficher** pour afficher un aperçu de vos plans d’abonnement.
1. Examinez les plans répertoriés sous **Abonnement aux** applications et sélectionnez **Enregistrer**.

    :::image type="content" source="../../../../assets/images/apps-in-meetings/test-preview-add-offer-id.png" alt-text="ajouter un ID d’offre" :::

La propriété subscriptionOffer est ajoutée au manifeste de votre application.

```json
"subscriptionOffer": {
     "offerId": "publisherId.offerId-preview"  
     }
```

>[!NOTE]
> Recherchez l’offre *d’aperçu d’étiquette* en regard de l’abonnement **Applications** pour confirmer si l’offre est une offre d’aperçu.

## <a name="sideload-the-app-to-teams"></a>Chargement d’une version de version Teams

Après avoir configuré votre application avec l’ID d’offre d’aperçu, créez un package d’application mis à jour et téléchargez-le sur Teams pour tester l’expérience d’achat de bout en bout. Pour plus d’informations, [voir Télécharger votre application dans Microsoft Teams](../../apps-upload.md). Vous pouvez également sélectionner **l’aperçu Teams** dans le Portail des développeurs pour Teams lancer rapidement votre application dans le client Teams client.

Si l’offre d’aperçu est spécifiée dans le manifeste de l’application et que l’audience d’aperçu est définie dans l’Centre de partenaires de l’offre, l’utilisateur peut voir le bouton Acheter **un abonnement** .

:::image type="content" source="../../../../assets/images/apps-in-meetings/test-preview-buy-subscription.png" alt-text="acheter un abonnement" border="true":::

### <a name="error-scenarios"></a>Scénarios d’erreur

* Si l’ID de l’offre est spécifié, mais que l’utilisateur ne fait pas partie de  **l’audience** d’aperçu définie dans l’Partner Center, le bouton Acheter un abonnement n’est pas activé et l’application affiche le message d’avertissement suivant à l’utilisateur :

  Aucun plan trouvé avec **-preview**. Assurez-vous que vous êtes dans l’audience d’aperçu.

  :::image type="content" source="../../../../assets/images/apps-in-meetings/test-preview-no-preview-audience.png" alt-text="pas d’audience de pré-audience" border="true" :::

* Si l’ID d’offre spécifié dans le manifeste de l’application n’est pas une offre d’aperçu, l’application affiche le message d’avertissement suivant à l’utilisateur et le chargement de version hors projet est désactivé :
  
  Il ne s’agit pas d’une offre d’aperçu. N’oubliez pas d’appender **l’aperçu** à l’ID de l’offre.

  :::image type="content" source="../../../../assets/images/apps-in-meetings/test-preview-no-preview-offer-id.png" alt-text="no -preview" border="true" :::

## <a name="see-also"></a>Voir aussi

* [Inclure une offre SaaS avec votre application Microsoft Teams application](include-saas-offer.md)
* [Créer une offre SaaS (Software as a Service)](include-saas-offer.md#create-your-saas-offer)
* [Ajouter une audience d’aperçu pour une offre SaaS](/azure/marketplace/create-new-saas-offer-preview)
* [Phase de création de l’aperçu](/azure/marketplace/review-publish-offer)
* [Examiner et publier une offre sur le marché commercial](/azure/marketplace/review-publish-offer#validation-and-publishing-steps)
