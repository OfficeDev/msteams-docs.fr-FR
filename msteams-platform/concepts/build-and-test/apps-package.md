---
title: Empaquetage de votre application
description: Découvrez comment empaqueter votre application Microsoft teams à des fins de test, de chargement et de publication en magasin.
ms.topic: conceptual
ms.openlocfilehash: 6929375c8d6a1602f01d83d15bfa0dab7f02a664
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/09/2020
ms.locfileid: "49605273"
---
# <a name="create-an-app-package-for-your-microsoft-teams-app"></a>Créer un package d’application pour votre application Microsoft teams

Les applications dans teams sont définies par un fichier JSON de manifeste d’application et regroupées dans un package d’application avec leurs icônes. Vous aurez besoin d’un package d’application pour télécharger et installer votre application dans teams et publier votre application dans votre catalogue d’applications métiers ou sur AppSource.

Un package d’applications teams est un fichier. zip contenant les éléments suivants :

* Un fichier manifeste nommé `manifest.json` , qui spécifie les attributs de votre application et pointe vers les ressources requises pour votre expérience, telles que l’emplacement de sa page de configuration d’onglets ou l’ID d’application Microsoft pour son bot.
* [Icônes de couleur et de plan de votre application](#app-icons).

## <a name="creating-a-manifest"></a>Création d’un manifeste

*Teams App Studio* peut vous aider à configurer votre manifeste. Elle contient également une bibliothèque de contrôle React et des exemples configurables pour les cartes. Voir [application Studio Overview](~/concepts/build-and-test/app-studio-overview.md).

Votre fichier manifeste doit être nommé « manifest.js » et se trouver au niveau supérieur du package de téléchargement. Notez que les manifestes et les packages créés précédemment peuvent prendre en charge une version plus ancienne du schéma. Pour les applications teams et en particulier la soumission AppSource (anciennement Office Store), vous devez utiliser le [schéma de manifeste](~/resources/schema/manifest-schema.md)actuel.

> [!TIP]
> Spécifiez le schéma au début de votre manifeste pour activer IntelliSense ou une prise en charge similaire à partir de votre éditeur de code :
>
> `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`

## <a name="app-icons"></a>Icônes de l’application

Votre package d’application doit inclure deux versions PNG de votre icône d’application, une icône de couleur et une icône en mode plan. Pour que votre application réussisse la révision AppSource, ces icônes doivent respecter les exigences de taille suivantes.

> [!Note]
> Si votre application dispose d’un bot ou d’une extension de messagerie, vos icônes seront également incluses dans votre inscription au service Microsoft Azure bot.

### <a name="color-icon"></a>Icône couleur

La version couleur de votre icône s’affiche dans la plupart des scénarios de teams et doit être 192x192 pixels. Le symbole de votre icône (96 x 96 pixels) peut être une couleur ou des couleurs, mais il doit être placé sur un arrière-plan Uni ou entièrement transparent.

Teams rogne automatiquement votre icône pour afficher un carré avec des angles arrondis dans plusieurs scénarios et une forme hexagonale dans les scénarios de robot. Incluez 48 pixels de remplissage pour que ces cultures puissent être effectuées sans perte de détail.

:::image type="content" source="../../assets/images/icons/design-color-icon.png" alt-text="Conseils de conception de l’icône couleur des équipes." border="false":::

### <a name="outline-icon"></a>Icône de plan

Une icône en mode plan s’affiche dans deux scénarios :

* Lorsque votre application est en cours d’utilisation et « levée » dans la barre de l’application située à gauche de teams.
* Lorsqu’un utilisateur épingle l’extension de messagerie de votre application.

L’icône doit être de 32x32 pixels. Il peut être blanc avec un arrière-plan transparent ou transparent avec un arrière-plan blanc (aucune autre couleur n’est autorisée). L’icône de contour ne doit pas comporter de remplissage supplémentaire pour le symbole.

:::image type="content" source="../../assets/images/icons/design-outline-icon.png" alt-text="Conseils de conception de l’icône couleur des équipes." border="false":::

### <a name="best-practices"></a>Meilleures pratiques

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-do.png" alt-text="Illustration illustrant la conception de vos icônes d’application." border="false":::

#### <a name="do-follow-the-precise-outline-icon-guidelines"></a>Do : suivre les instructions d’icône de contour précises

Les valeurs RVB du blanc utilisé dans votre icône doivent être rouges : 255, vert : 255, bleu : 255. Toutes les autres parties de l’icône de contour doivent être entièrement transparentes, avec la couche alpha définie sur 0.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-dont.png" alt-text="Illustration montrant comment ne pas concevoir vos icônes d’application." border="false":::

#### <a name="dont-crop-in-a-circular-or-rounded-square-shape"></a>Ne pas : Rogner dans une forme circulaire ou en carré arrondi

L’icône de couleur soumise dans votre package d’application doit être carrée. N’arrondissez pas les coins de votre icône. Teams ajuste automatiquement le rayon d’arrondi.

   :::column-end:::
:::row-end:::

### <a name="examples"></a>Exemples

Voici comment les icônes d’application apparaissent dans les différents contextes et fonctionnalités de teams.

#### <a name="personal-app"></a>Application personnelle

:::image type="content" source="../../assets/images/icons/personal-app-icon-example.png" alt-text="Exemple illustrant l’apparence d’une icône d’application dans une application personnelle." border="false":::

#### <a name="bot-channel"></a>Bot (canal)

:::image type="content" source="../../assets/images/icons/bot-icon-example.png" alt-text="Exemple illustrant l’apparence d’une icône d’application sur un robot au sein d’un canal." border="false":::

#### <a name="messaging-extension"></a>Extension de messagerie

:::image type="content" source="../../assets/images/icons/messaging-extension-icon-example.png" alt-text="<>texte de remplacement " border="false":::
