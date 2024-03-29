---
title: Empaqueter votre application
description: Découvrez comment empaqueter votre application Microsoft Teams et la charger dans Teams. Créez un package d’application, activez le chargement personnalisé, assurez-vous que votre application est en cours d’exécution et accessible à l’aide de HTTPs.
ms.localizationpriority: high
ms.topic: conceptual
ms.openlocfilehash: cd2bb1c2f0ff97a28f467334148c283142b2d535
ms.sourcegitcommit: 84747a9e3c561c2ca046eda0b52ada18da04521d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2022
ms.locfileid: "68791453"
---
# <a name="create-teams-app-package"></a>Créer un package d’application Teams

Vous avez besoin d’un package d’application. Toutefois, vous prévoyez de distribuer votre application Microsoft Teams. Un package valide est un fichier ZIP qui contient les éléments suivants :

* **Manifeste de l’application** : décrit la configuration de votre application, notamment ses fonctionnalités, les ressources requises et d’autres attributs importants.
* **Icônes d’application** : chaque package nécessite une icône de couleur et de contour pour votre application.

## <a name="teams-doesnt-host-your-app"></a>Teams n’héberge pas votre application

Lorsqu’un utilisateur installe votre application dans Teams, il installe un package d’application qui contient un seul fichier de configuration (également appelé manifeste d’application) et les icônes de votre application. La logique de l’application et le stockage des données sont hébergés ailleurs, par exemple sur localhost pendant le développement et sur Azure Web Services. Teams accède à ces ressources via HTTPS.

:::image type="content" source="../../assets/images/teams-app-host.png" alt-text="Illustration montrant l’hébergement d’applications pour Application Teams":::

## <a name="app-manifest"></a>Manifeste d'application

Votre fichier manifeste de l’application doit se trouver au niveau supérieur du package avec le nom `manifest.json`.

Lors de la publication dans le store Teams, assurez-vous que votre manifeste fait référence au [schéma](~/resources/schema/manifest-schema.md) le plus récent.

## <a name="app-icons"></a>Icônes d’application

Votre package de l’application doit inclure deux versions de format PNG de l’icône de votre application : une version de couleur et une version de contour.

> [!Note]
> Si votre application dispose d’un bot ou d’une extension de message, vos icônes seront également incluses dans votre inscription Microsoft Azure Bot Service.

Pour que votre application soit approuvé par le store Teams, ces icônes doivent respecter les exigences de taille suivantes.

### <a name="color-icon"></a>Icône de couleur

La version de couleur de votre icône s’affiche dans la plupart des scénarios Teams et doit être de 192x192 pixels. Le symbole de votre icône (96 x 96 pixels) peut être de n’importe quelle couleur, mais il doit se trouver sur un arrière-plan carré plein ou entièrement transparent.

Teams rogne automatiquement votre icône pour afficher un carré avec des coins arrondis dans plusieurs scénarios et une forme hexagonale dans les scénarios de bot. Pour rogner le symbole sans perdre de détail, incluez 48 pixels de remplissage autour de votre symbole.

:::image type="content" source="../../assets/images/icons/design-color-icon.png" alt-text="Aide concernant les icônes de couleur et leur conception.":::

### <a name="outline-icon"></a>Icône de contour

Une icône de contour s’affiche dans deux scénarios :

* Lorsque votre application est en cours d’utilisation et « hissée » dans la barre de l’application sur le côté gauche de Teams.
* Lorsqu’un utilisateur épingle l’extension de message de votre application.

L’icône doit être de 32 x 32 pixels. Il peut être blanc avec un arrière-plan transparent ou transparent avec un arrière-plan blanc (aucune autre couleur n’est autorisée). L’icône de contour ne doit pas avoir de remplissage supplémentaire autour du symbole.

:::image type="content" source="../../assets/images/icons/design-outline-icon.png" alt-text="Aide concernant les icônes de contour et leur conception.":::

### <a name="best-practices"></a>Bonnes pratiques

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-do.png" alt-text="Illustration montrant comment concevoir les icônes de votre application.":::

#### <a name="do-follow-the-precise-outline-icon-guidelines"></a>À faire : suivez les instructions précises sur les icônes de contour

Les valeurs RVB de blanc utilisées dans votre icône doivent être Rouge : 255, Vert : 255, Bleu : 255. Toutes les autres parties de l’icône de contour doivent être entièrement transparentes, avec le canal alpha sur 0.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-dont.png" alt-text="Illustration montrant ce qu’il ne faut pas faire avec les icônes de votre application.":::

#### <a name="dont-crop-in-a-circular-or-rounded-square-shape"></a>À ne pas faire : rogner dans une forme circulaire ou carrée arrondie

L’icône de couleur envoyée dans votre package de l’application doit être carrée. N’arrondissez pas les coins de votre icône. Teams ajuste automatiquement le rayon de l’angle.

   :::column-end:::
:::row-end:::

#### <a name="dont-copy-other-brands"></a>À ne pas faire : copier d’autres marques

Vos icônes ne doivent pas imiter les produits protégés par des droits d’auteur que vous ne possédez pas. Par exemple, une conception similaire à un produit ou une marque Microsoft.

### <a name="examples"></a>Exemples

Voici comment les icônes d’application apparaissent dans différentes fonctionnalités et contextes Teams.

#### <a name="personal-app"></a>Application personnelle

:::image type="content" source="../../assets/images/icons/personal-app-icon-example.png" alt-text="Exemple montrant l’apparence d’une icône d’application dans une application personnelle.":::

#### <a name="bot-channel"></a>Bot (canal)

:::image type="content" source="../../assets/images/icons/bot-icon-example.png" alt-text="Exemple montrant l’apparence d’une icône d’application sur un bot à l’intérieur d’un canal.":::

#### <a name="message-extension"></a>Extension de message

:::image type="content" source="../../assets/images/icons/messaging-extension-icon-example.png" alt-text="<texte de remplacement>":::

## <a name="next-step"></a>Étape suivante

Choisissez la façon dont vous prévoyez de distribuer votre application :

> [!div class="nextstepaction"]
> [Charger une version test de votre application dans Teams](~/concepts/deploy-and-publish/apps-upload.md)
> [!div class="nextstepaction"]
> [Publier votre application dans votre organisation](/MicrosoftTeams/tenant-apps-catalog-teams?toc=/microsoftteams/platform/toc.json&bc=/MicrosoftTeams/breadcrumb/toc.json)
> [!div class="nextstepaction"]
> [Publier votre application dans le Store](~/concepts/deploy-and-publish/appsource/publish.md)

## <a name="see-also"></a>Voir aussi

[Gérer vos applications avec le Portail des développeurs pour Microsoft Teams](~/concepts/build-and-test/teams-developer-portal.md)
