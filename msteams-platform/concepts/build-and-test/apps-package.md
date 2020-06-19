---
title: Empaquetage de votre application
description: Découvrez comment empaqueter votre application à des fins de test, de chargement et de publication dans Microsoft teams
keywords: empaquetage d’applications teams
ms.topic: conceptual
ms.openlocfilehash: 66131f37f9f68c8fd54412d41068f6124da94453
ms.sourcegitcommit: 6c786434b56cc8c2765a14aa1f6149870245f309
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/06/2020
ms.locfileid: "44801366"
---
# <a name="create-an-app-package-for-your-microsoft-teams-app"></a>Créer un package d’application pour votre application Microsoft teams

Les applications dans teams sont définies par un fichier JSON de manifeste d’application et regroupées dans un package d’application avec leurs icônes. Vous aurez besoin d’un package d’application pour télécharger et installer votre application dans Teams, et pour publier le catalogue d’applications de votre ligne de l’application métier ou vers AppSource.

Un package d’applications teams est un fichier. zip contenant les éléments suivants :

* Un fichier manifeste nommé « manifest.json », qui spécifie les attributs de votre application et pointe vers les ressources requises pour votre expérience, telles que l’emplacement de sa page de configuration d’onglets ou l’ID d’application Microsoft pour son bot.
* Une icône « plan » transparente et une icône « couleur » complète. Pour plus d’informations, consultez la section [icônes](#icons) plus loin dans cette rubrique.

## <a name="creating-a-manifest"></a>Création d’un manifeste

*Teams App Studio* peut vous aider à configurer votre manifeste. Elle contient également une bibliothèque de contrôle React et des exemples configurables pour les cartes. Voir [application Studio Overview](~/concepts/build-and-test/app-studio-overview.md).

Votre fichier manifeste doit être nommé « manifest.js » et se trouver au niveau supérieur du package de téléchargement. Notez que les manifestes et les packages créés précédemment peuvent prendre en charge une version plus ancienne du schéma. Pour les applications teams et en particulier la soumission AppSource (anciennement Office Store), vous devez utiliser le [schéma de manifeste](~/resources/schema/manifest-schema.md)actuel.

> [!TIP]
> Spécifiez le schéma au début de votre manifeste pour activer IntelliSense ou une prise en charge similaire à partir de votre éditeur de code :
>
> `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",`

## <a name="icons"></a>Icônes

> [!Note]
> Si votre application contient un bot ou une extension de messagerie, les icônes utilisées seront les icônes chargées dans l’enregistrement de votre bot dans l’infrastructure de robot.

Microsoft teams nécessite deux icônes pour l’expérience de votre application, à utiliser dans le produit. Les icônes doivent être incluses dans le package et référencées via des chemins d’accès relatifs dans le manifeste. La longueur maximale de chaque chemin d’accès est de 2048 octets, et le format de l’icône est. png.

### <a name="color"></a>color

L' `color` icône est utilisée dans Microsoft Teams (dans les galeries d’applications et d’onglets, les robots, les lanceurs, etc.). Cette icône doit être 192x192 pixels. Votre icône peut être n’importe quelle couleur (ou couleurs), mais l’arrière-plan doit être votre couleur d’accentuation personnalisée. Elle doit également avoir une petite quantité de remplissage autour de l’icône pour prendre en charge le rognage hexagonal pour la version bot de l’icône.

### <a name="outline"></a>outline

L' `outline` icône est utilisée aux emplacements suivants : la barre d’application et les extensions de messagerie que l’utilisateur a marquées comme « favoris ». Cette icône doit être de 32x32 pixels. Votre icône de contour ne doit contenir que le blanc et la transparence (aucune autre couleur). L’icône peut être blanche avec un arrière-plan transparent ou transparente avec un arrière-plan blanc. L’icône de contour ne doit pas avoir de remplissage supplémentaire autour de l’icône et doit être aussi rapprochée que possible tout en maintenant les dimensions 32x32. Voici quelques exemples intéressants :

![Exemples d’icônes de plan](~/assets/images/icons/sample20x20s.png)

Imaginons, par exemple, que votre société est contoso. Vous devez envoyer deux icônes :

![Présentation des icônes](~/assets/images/framework/framework_submit_icon.png)

Voici comment les icônes apparaîtront dans l’interface utilisateur :

#### <a name="bot-and-chiclet-in-channel-view"></a>Robot et chiclet dans l’affichage des canaux

![Bot et chiclet UX](~/assets/images/icons/botandchiclet.png)

#### <a name="flyout"></a>Menu

![Exemples d’icônes contoso](~/assets/images/icons/flyout.png)

#### <a name="app-bar-and-home-screen"></a>Barre d’application et écran d’accueil

![Exemples d’icônes contoso](~/assets/images/icons/appbarhomescreen.png)
