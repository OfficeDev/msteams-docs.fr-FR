---
title: Package de votre application
description: Découvrez comment mettre en package votre application Microsoft Teams pour le test, le téléchargement et la publication dans le Store.
ms.localizationpriority: medium
ms.topic: conceptual
ms.openlocfilehash: 926d6051024ae6e9a5f3d857bdb97fa02f56e8db
ms.sourcegitcommit: c04a1a792773a9d5c61169c5702d94a8c478ad1c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2021
ms.locfileid: "60260672"
---
# <a name="create-a-microsoft-teams-app-package"></a>Créer un package Microsoft Teams’application

Vous avez besoin d’un package d’application, mais vous prévoyez de distribuer votre Microsoft Teams application. Un package valide est un fichier ZIP qui contient les éléments suivants :

* **Manifeste de l’application**: décrit la configuration de votre application, notamment ses fonctionnalités, les ressources requises et d’autres attributs importants.
* **Icônes d’application**: chaque package nécessite une icône de couleur et de plan pour votre application.

## <a name="app-manifest"></a>Manifeste d'application

Votre fichier manifeste d’application doit se trouver au niveau supérieur du package avec le nom `manifest.json` . 

Lors de la publication dans Teams store, assurez-vous que votre manifeste fait référence au [schéma le plus récent.](~/resources/schema/manifest-schema.md)

## <a name="app-icons"></a>Icônes d’application

Votre package d’application doit inclure deux versions PNG de l’icône de votre application : une version de couleur et une version plan.

> [!Note]
> Si votre application dispose d’un bot ou d’une extension de messagerie, vos icônes seront également incluses dans votre inscription Microsoft Azure Bot Service.

Pour que votre application soit Teams’avis dans le Store, ces icônes doivent respecter les exigences de taille suivantes.

### <a name="color-icon"></a>Icône Couleur

La version de couleur de votre icône s’affiche dans la plupart des scénarios Teams et doit être de 192x192 pixels. Votre symbole d’icône (96 x 96 pixels) peut être n’importe quelle couleur, mais il doit être sur un arrière-plan carré plein ou entièrement transparent.

Teams votre icône pour afficher automatiquement un carré avec des coins arrondis dans plusieurs scénarios et une forme hexagonale dans les scénarios de bot. Pour roger le symbole sans perdre de détail, incluez 48 pixels de remplissage autour de votre symbole.

:::image type="content" source="../../assets/images/icons/design-color-icon.png" alt-text="Teams icône de couleur et des conseils de conception." border="false":::

### <a name="outline-icon"></a>Icône Plan

Une icône de plan s’affiche dans deux scénarios :

* Lorsque votre application est en cours d’utilisation et « hissée » dans la barre de l’application sur le côté gauche de la Teams.
* Lorsqu’un utilisateur épingle l’extension de messagerie de votre application.

L’icône doit être de 32 x 32 pixels. Il peut être blanc avec un arrière-plan transparent ou transparent avec un arrière-plan blanc (aucune autre couleur n’est autorisée). L’icône de plan ne doit pas avoir de remplissage supplémentaire autour du symbole.

:::image type="content" source="../../assets/images/icons/design-outline-icon.png" alt-text="Teams de conception d’icônes de plan." border="false":::

### <a name="best-practices"></a>Meilleures pratiques

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-do.png" alt-text="Illustration montrant comment concevoir les icônes de votre application." border="false":::

#### <a name="do-follow-the-precise-outline-icon-guidelines"></a>À faire : suivez les instructions précises sur les icônes de plan

Les valeurs RVB de blanc utilisées dans votre icône doivent être Rouge : 255, Vert : 255, Bleu : 255. Toutes les autres parties de l’icône de plan doivent être entièrement transparentes, avec le canal alpha sur 0.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-dont.png" alt-text="Illustration montrant comment ne pas concevoir les icônes de votre application." border="false":::

#### <a name="dont-crop-in-a-circular-or-rounded-square-shape"></a>À ne pas faire : rognent dans une forme carrée arrondie ou arrondie

L’icône de couleur envoyée dans votre package d’application doit être carrée. N’arrondissez pas les coins de votre icône. Teams ajuste automatiquement le rayon d’angle.

   :::column-end:::
:::row-end:::

#### <a name="dont-copy-other-brands"></a>À ne pas faire : copier d’autres marques

Vos icônes ne doivent pas imiter les produits protégés par des droits d’auteur que vous ne possédez pas. Par exemple, une conception similaire à un produit ou une marque Microsoft.

### <a name="examples"></a>範例

Voici comment les icônes d’application s’affichent dans Teams fonctionnalités et contextes différents.

#### <a name="personal-app"></a>Application personnelle

:::image type="content" source="../../assets/images/icons/personal-app-icon-example.png" alt-text="Exemple montrant l’apparence d’une icône d’application dans une application personnelle." border="false":::

#### <a name="bot-channel"></a>Bot (canal)

:::image type="content" source="../../assets/images/icons/bot-icon-example.png" alt-text="Exemple montrant l’apparence d’une icône d’application sur un bot à l’intérieur d’un canal." border="false":::

#### <a name="messaging-extension"></a>Extension de la messagerie

:::image type="content" source="../../assets/images/icons/messaging-extension-icon-example.png" alt-text="<texte de>" border="false":::

## <a name="next-step"></a>Étape suivante

Choisissez la façon dont vous prévoyez de distribuer votre application :

> [!div class="nextstepaction"]
> [Chargez une version de version de votre application dans Teams](~/concepts/deploy-and-publish/apps-upload.md)
> [!div class="nextstepaction"]
> [Publier votre application dans votre organisation](/MicrosoftTeams/tenant-apps-catalog-teams?toc=/microsoftteams/platform/toc.json&bc=/MicrosoftTeams/breadcrumb/toc.json)
> [!div class="nextstepaction"]
> [Publier votre application dans le Store](~/concepts/deploy-and-publish/appsource/publish.md)
