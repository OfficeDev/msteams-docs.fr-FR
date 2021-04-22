---
title: Package de votre application
description: Découvrez comment mettre en package votre application Microsoft Teams pour les tests, le téléchargement et la publication dans le Store.
ms.topic: conceptual
ms.openlocfilehash: 222ea5459b3496c00b1186f15a68c3288ce419f7
ms.sourcegitcommit: 35bc2a31b92f3f7c6524373108f095a870d9ad09
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/21/2021
ms.locfileid: "51922509"
---
# <a name="create-an-app-package-for-your-microsoft-teams-app"></a>Créer un package d'application pour votre application Microsoft Teams

Les applications dans Teams sont définies par un fichier JSON manifeste d'application et regroupées dans un package d'application avec leurs icônes. Vous aurez besoin d'un package d'application pour télécharger et installer votre application dans Teams et publier dans votre catalogue d'applications métier ou dans AppSource.

Un package d'application Teams est un fichier .zip contenant les informations suivantes :

* Un fichier manifeste nommé , qui spécifie les attributs de votre application et pointe vers les ressources requises pour votre expérience, telles que l'emplacement de sa page de configuration d'onglet ou l'ID de l'application Microsoft pour `manifest.json` son bot.
* [Icônes de couleur et de plan pour votre application.](#app-icons)

## <a name="creating-a-manifest"></a>Création d’un manifeste

**Teams App Studio peut** vous aider à configurer votre manifeste. Elle contient également une bibliothèque de contrôle React et des exemples configurables pour les cartes. Pour plus d'informations, [voir Vue d'ensemble d'App Studio.](~/concepts/build-and-test/app-studio-overview.md)

Votre fichier manifeste doit être nommé « manifest.js» et se trouver au niveau supérieur du package de chargement. Notez que les manifestes et les packages créés précédemment peuvent prendre en charge une version antérieure du schéma. Pour les applications Teams et en particulier la soumission d'AppSource (anciennement Office Store), vous devez utiliser le schéma [de manifeste actuel.](~/resources/schema/manifest-schema.md)

> [!TIP]
> Spécifiez le schéma au début de votre manifeste pour activer IntelliSense ou une prise en charge similaire à partir de votre éditeur de code :
>
> `"$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.9/MicrosoftTeams.schema.json",`
 
## <a name="app-icons"></a>Icônes d'application

Votre package d'application doit inclure deux versions PNG de l'icône de votre application : une icône de couleur et une icône plan. Pour que votre application passe l'avis AppSource, ces icônes doivent respecter les exigences de taille suivantes.

> [!Note]
> Si votre application dispose d'un bot ou d'une extension de messagerie, vos icônes seront également incluses dans votre inscription au service de bot Microsoft Azure.

### <a name="color-icon"></a>Icône Couleur

La version de couleur de votre icône s'affiche dans la plupart des scénarios Teams et doit être de 192 x 192 pixels. Votre symbole d'icône (96 x 96 pixels) peut être n'importe quelle couleur ou couleur, mais il doit être sur un arrière-plan carré plein ou entièrement transparent.

Teams taille automatiquement votre icône pour afficher un carré avec des coins arrondis dans plusieurs scénarios et une forme hexagonale dans les scénarios de bot. Incluez 48 pixels de remplissage autour de votre symbole pour que ces champs soient réalisés sans perte de détails.

:::image type="content" source="../../assets/images/icons/design-color-icon.png" alt-text="Conseils sur la conception des icônes de couleur Teams." border="false":::

### <a name="outline-icon"></a>Icône Plan

Une icône de plan s'affiche dans deux scénarios :

* Lorsque votre application est en cours d'utilisation et « hissée » dans la barre d'application à gauche de Teams.
* lorsqu'un utilisateur épingle l'extension de messagerie de votre application.

L'icône doit être de 32 x 32 pixels. Il peut être blanc avec un arrière-plan transparent ou transparent avec un arrière-plan blanc (aucune autre couleur n'est autorisée). L'icône de plan ne doit pas avoir de remplissage supplémentaire autour du symbole.

:::image type="content" source="../../assets/images/icons/design-outline-icon.png" alt-text="Recommandations en conception d'icônes de plan Teams." border="false":::

### <a name="best-practices"></a>Meilleures pratiques

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-do.png" alt-text="Illustration montrant comment concevoir les icônes de votre application." border="false":::

#### <a name="do-follow-the-precise-outline-icon-guidelines"></a>À faire : suivez les instructions précises sur les icônes de plan

Les valeurs RVB de blanc utilisées dans votre icône doivent être Rouge : 255, Vert : 255, Bleu : 255. Toutes les autres parties de l'icône de plan doivent être entièrement transparentes, avec le canal alpha sur 0.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-dont.png" alt-text="Illustration montrant comment ne pas concevoir les icônes de votre application." border="false":::

#### <a name="dont-crop-in-a-circular-or-rounded-square-shape"></a>À ne pas faire : rognent dans une forme carrée arrondie ou arrondie

L'icône de couleur envoyée dans votre package d'application doit être carrée. N'arrondissez pas les coins de votre icône. Teams ajuste automatiquement le rayon d'angle.

   :::column-end:::
:::row-end:::

### <a name="examples"></a>Exemples

Voici comment les icônes d'application apparaissent dans différents contextes et fonctionnalités Teams.

#### <a name="personal-app"></a>Application personnelle

:::image type="content" source="../../assets/images/icons/personal-app-icon-example.png" alt-text="Exemple montrant l'apparence d'une icône d'application dans une application personnelle." border="false":::

#### <a name="bot-channel"></a>Bot (canal)

:::image type="content" source="../../assets/images/icons/bot-icon-example.png" alt-text="Exemple montrant l'apparence d'une icône d'application sur un bot à l'intérieur d'un canal." border="false":::

#### <a name="messaging-extension"></a>Extension de la messagerie

:::image type="content" source="../../assets/images/icons/messaging-extension-icon-example.png" alt-text="<texte de>" border="false":::
