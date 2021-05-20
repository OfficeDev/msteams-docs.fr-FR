---
title: Emballez votre application
description: Découvrez comment emballer votre application Microsoft Teams pour les tests, le téléchargement et l’édition en magasin.
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: 219e2d5341707ed51b7e0a3a8077f93df9eac640
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565213"
---
# <a name="create-a-microsoft-teams-app-package"></a>Créer un paquet Microsoft Teams’application

Vous avez besoin d’un package d’application mais vous prévoyez de distribuer Microsoft Teams application. Un paquet valide est un fichier ZIP qui contient les éléments suivants :

* **Manifeste d’application**: Décrit comment votre application est configurée, y compris ses capacités, les ressources requises et d’autres attributs importants.
* **Icônes d’application**: Chaque paquet nécessite une icône couleur et contour pour votre application.

## <a name="app-manifest"></a>Manifeste d'application

Votre fichier manifeste d’application doit être au niveau supérieur du paquet avec le nom `manifest.json` . 

Lors de la publication au Teams magasin, assurez-vous que votre manifeste fait référence au [dernier schéma.](~/resources/schema/manifest-schema.md)

## <a name="app-icons"></a>Icônes d’application

Votre package d’application doit inclure deux versions PNG de votre icône d’application : une version couleur et contour.

> [!Note]
> Si votre application dispose d’une extension de bot ou de messagerie, vos icônes seront également incluses dans votre Microsoft Azure’enregistrement bot service.

Pour que votre application passe l Teams magasin, ces icônes doivent répondre aux exigences de taille suivantes.

### <a name="color-icon"></a>Icône de couleur

La version couleur de votre icône s’affiche dans la plupart Teams scénarios et doit être de 192x192 pixels. Votre symbole d’icône (pixels 96x96) peut être n’importe quelle couleur, mais il doit s’asseoir sur un fond carré solide ou entièrement transparent.

Teams automatiquement votre icône pour afficher un carré avec des coins arrondis dans plusieurs scénarios et une forme hexagonale dans les scénarios bot. Pour recadrer le symbole sans perdre de détails, incluez 48 pixels de rembourrage autour de votre symbole.

:::image type="content" source="../../assets/images/icons/design-color-icon.png" alt-text="Teams couleur et des conseils de conception." border="false":::

### <a name="outline-icon"></a>Icône de contour

Une icône de contour s’affiche dans deux scénarios :

* Lorsque votre application est en cours d’utilisation et « hissé » sur la barre d’application sur le côté gauche de Teams.
* Lorsqu’un utilisateur épingle l’extension de messagerie de votre application.

L’icône doit être de 32x32 pixels. Il peut être blanc avec un fond transparent ou transparent avec un fond blanc (aucune autre couleur n’est permise). L’icône de contour ne doit pas avoir de rembourrage supplémentaire autour du symbole.

:::image type="content" source="../../assets/images/icons/design-outline-icon.png" alt-text="Teams guidage de conception d’icône." border="false":::

### <a name="best-practices"></a>Bonnes pratiques

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-do.png" alt-text="Illustration montrant comment concevoir les icônes de votre application." border="false":::

#### <a name="do-follow-the-precise-outline-icon-guidelines"></a>Faire: Suivez les lignes directrices précises icône contour

Les valeurs RVB de blanc utilisées dans votre icône doivent être rouges : 255, vert : 255, bleu : 255. Toutes les autres parties de l’icône de contour doivent être entièrement transparentes, avec le canal alpha réglé à 0.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-dont.png" alt-text="Illustration montrant comment ne pas concevoir les icônes de votre application." border="false":::

#### <a name="dont-crop-in-a-circular-or-rounded-square-shape"></a>Ne pas : Recadrer en forme carrée circulaire ou arrondie

L’icône couleur soumise dans votre paquet d’application doit être carrée. Ne faites pas le tour des coins de votre icône. Teams ajuste automatiquement le rayon d’angle.

   :::column-end:::
:::row-end:::

#### <a name="dont-copy-other-brands"></a>Ne pas : Copier d’autres marques

Vos icônes ne doivent pas imiter les produits protégés par le droit d’auteur que vous ne possédez pas. Par exemple, un design similaire à un produit ou une marque Microsoft.

### <a name="examples"></a>Exemples

Voici comment les icônes d’application apparaissent dans différentes Teams et contextes.

#### <a name="personal-app"></a>Application personnelle

:::image type="content" source="../../assets/images/icons/personal-app-icon-example.png" alt-text="Exemple montrant l’apparence d’une icône d’application dans une application personnelle." border="false":::

#### <a name="bot-channel"></a>Bot (canal)

:::image type="content" source="../../assets/images/icons/bot-icon-example.png" alt-text="Exemple montrant l’apparence d’une icône d’application sur un bot à l’intérieur du canal." border="false":::

#### <a name="messaging-extension"></a>Extension de la messagerie

:::image type="content" source="../../assets/images/icons/messaging-extension-icon-example.png" alt-text="<texte alt>" border="false":::

## <a name="next-step"></a>Étape suivante

Choisissez comment vous prévoyez distribuer votre application :

> [!div class="nextstepaction"]
> [Sideload votre application dans Teams](~/concepts/deploy-and-publish/apps-upload.md)
> [!div class="nextstepaction"]
> [Publiez votre application sur votre org](/MicrosoftTeams/tenant-apps-catalog-teams?toc=/microsoftteams/platform/toc.json&bc=/MicrosoftTeams/breadcrumb/toc.json)
> [!div class="nextstepaction"]
> [Publiez votre application sur le magasin](~/concepts/deploy-and-publish/appsource/publish.md)
