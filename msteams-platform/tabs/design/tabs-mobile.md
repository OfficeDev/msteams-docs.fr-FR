---
title: Onglets sur les appareils mobiles
description: Décrit les instructions pour la conception d'onglets qui fonctionnent sur mobile.
ms.topic: conceptual
localization_priority: Normal
keywords: onglets mobiles des applications personnelles de l'infrastructure de référence des recommandations en matière de conception d'équipes
ms.openlocfilehash: 6459d6af7899859f25b28587021e26ce6440fbef
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020407"
---
# <a name="tabs-on-mobile"></a>Onglets sur les appareils mobiles

> [!NOTE]
> Si vous choisissez que votre onglet canal/groupe apparaisse sur les clients mobiles Teams, la configuration doit avoir une valeur pour la propriété `setSettings()` `websiteUrl` (voir ci-dessous).

Les onglets personnalisés peuvent faire partie d'un canal, d'une conversation de groupe ou d'une application personnelle (applications qui contiennent des onglets statiques et/ou un bot un-à-un).

Les applications personnelles sont disponibles sur les clients mobiles dans le caisse de l'application. L'application ne peut être installée qu'à partir d'un ordinateur de bureau ou d'un client web et son apparition sur les clients mobiles peut prendre jusqu'à 24 heures. Vous pouvez également appliquer un rechargement sur le client mobile en vous dé signant et en vous délant. Cela devrait rendre l'application mobile disponible immédiatement.

Les onglets de canal sont également disponibles sur les appareils mobiles. Le comportement par défaut consiste actuellement à utiliser votre `websiteUrl` onglet pour lancer votre onglet dans une fenêtre de navigateur. Toutefois, ils peuvent être chargés sur un client mobile en cliquant sur le menu de dépassement en haut de l'onglet et en choisissant Ouvrir, qui vous permet de charger l'onglet à l'intérieur du `...` client mobile  `contentUrl` Teams.

## <a name="accessing-personal-tabs"></a>Accès aux onglets personnels

L'illustration suivante montre comment accéder à un onglet personnel sur un appareil mobile.

:::image type="content" source="../../assets/images/tabs/mobile-app-drawer.png" alt-text="Illustration montrant le caisse d'application mobile Teams." border="false":::

## <a name="accessing-channel-tabs"></a>Accès aux onglets de canal

L'illustration suivante montre comment accéder à un onglet de canal sur mobile.

:::image type="content" source="../../assets/images/tabs/mobile-tab.png" alt-text="Illustration montrant un onglet mobile Teams." border="false":::

## <a name="design-considerations"></a>Considérations relatives à la conception

Notre plateforme mobile permet aux applications d'être une expérience immersive avec le contenu de l'application prenant tout l'écran en dehors de la navigation Teams principale. Pour créer une expérience immersive adaptée à Teams, suivez ces instructions.

### <a name="responsive-design"></a>Conception réactive

Étant donné que votre onglet peut être ouvert sur des appareils avec un large éventail de tailles d'écran, il doit respecter les principes de [conception](https://www.w3schools.com/html/html_responsive.asp) réactifs. Toutes les constructions clés doivent être accessibles sur les appareils mobiles et les vues ne doivent pas être déformées. Assurez-vous que lorsque votre onglet est chargé sur un appareil mobile, tous les boutons et liens sont facilement accessibles à l'aide de la navigation avec les doigts.

### <a name="layouts"></a>Dispositions

Il est important de choisir la disposition correcte pour votre onglet. Vous devez prendre en compte le type d'informations que vous présentez et choisir une disposition qui les organise pour faciliter la consommation. Certaines options potentielles sont décrites ci-dessous.

#### <a name="single-canvas"></a>Canevas unique

Il s'agit d'un domaine important dans lequel le travail est effectué. L'application Wiki Teams suit ce modèle. Si vous avez une application qui ne sépare pas le contenu en composants plus petits, cela serait adapté.

:::image type="content" source="../../assets/images/tabs/mobile-tab-single-canvas.png" alt-text="Illustration montrant un onglet de canevas mobile Teams." border="false":::

#### <a name="list"></a>Répertorier

Les listes sont excellentes pour le tri et le filtrage de grandes quantités de données et sont très bonnes pour conserver les éléments les plus importants en haut. Il est utile d'utiliser des colonnes triables. Les actions peuvent être ajoutées à chaque élément de liste sous le menu des ellipses.

:::image type="content" source="../../assets/images/tabs/mobile-tab-list.png" alt-text="Illustration montrant un onglet de liste mobile Teams." border="false":::

#### <a name="grid"></a>Grid

Les grilles sont utiles pour afficher des éléments hautement visuels. Il est utile d'inclure un contrôle de filtre ou de recherche en haut.

:::image type="content" source="../../assets/images/tabs/mobile-tab-grid.png" alt-text="Illustration montrant un onglet mobile Teams avec une disposition de grille." border="false":::

### <a name="tabs-with-bots-on-mobile"></a>Onglets avec bots sur mobile

L'exemple suivant est une application personnelle qui possède des onglets et un bot.

:::image type="content" source="../../assets/images/tabs/mobile-tab-with-bot.png" alt-text="Illustration montrant comment une application Teams mobile avec des onglets et un bot." border="false":::

## <a name="ui-components"></a>Composants de l'interface utilisateur

### <a name="color-palettes"></a>Palettes de couleurs

L'utilisation de notre palette neutre approuvée pour les arrière-plans, les notifications, le texte et les boutons permettra à votre application de se sentir plus à l'accueil dans Teams. Étant donné que Teams mobile a deux thèmes à thèmes (clair et foncé), il est bon de s'assurer que votre application s'annonce bien dans les deux cas.

#### <a name="light-color"></a>Couleur claire

![palette de couleurs claires](../../assets/images/light-color.png)

#### <a name="dark-color"></a>Couleur foncée

![palette de couleurs foncées](../../assets/images/dark-color.png)

### <a name="buttons-and-controls"></a>Boutons et contrôles

Le style des boutons permet de communiquer le type d'action qu'ils déclenchent. Nous tenez à jour un large éventail de boutons mis en forme pour afficher différents niveaux d'accentuation. Les boutons peuvent avoir du texte, une icône ou une combinaison de texte et d'icône. Pour communiquer différents niveaux dans une hiérarchie, nous avons conçu des boutons principaux et secondaires dans chaque catégorie.

#### <a name="buttons"></a>Boutons

Boutons principal et secondaire.

![image de boutons](../../assets/images/buttons.png)

#### <a name="selection-controls"></a>Contrôles de sélection

Boutons d'radio, case à cocher et boutons bascule.

![contrôles de sélection](../../assets/images/selection-controls.png)

#### <a name="chiclets-and-pills"></a>Îles et err.

![cachets et err.](../../assets/images/chiclets-and-pills.png)

### <a name="typography"></a>Typographie

La typographie doit être claire et précise. Mettre en avant des informations importantes et éviter d'utiliser plusieurs polices et tailles pour réduire la confusion. Nous vous recommandons d'utiliser un cas de phrase et d'éviter l'utilisation de toutes les limites pour la localisation et la lisibilité.

![typograph mobile](../../assets/images/mobile-typography.png)

### <a name="fields-and-flyouts"></a>Champs et volants

Les champs sont des zones où les utilisateurs peuvent entrer du texte. Les volants sont plus légers que les boîtes de dialogue et apparaissent dans le volet supérieur.

#### <a name="list-controls"></a>Répertorier les contrôles

![contrôles de liste mobile](../../assets/images/mobile-list-controls.png)

#### <a name="field-controls"></a>contrôles de champs

![contrôles de champ mobile](../../assets/images/mobile-field-controls.png)

## <a name="developer-considerations"></a>Considérations pour les développeurs

Lorsque vous construisez une application qui inclut un onglet, vous devez prendre en compte (et tester) le fonctionnement de votre onglet sur les clients Microsoft Teams Android et iOS. Les sections ci-dessous décrivent certains des scénarios clés que vous devez prendre en considération.

### <a name="testing-on-mobile-clients"></a>Test sur les clients mobiles

Vous devez vérifier que votre onglet fonctionne correctement sur des appareils mobiles de différentes tailles et qualités. Pour les appareils Android, vous pouvez utiliser [DevTools](~/tabs/how-to/developer-tools.md) pour déboguer votre onglet pendant son exécution. Nous vous recommandons de tester sur les appareils à haut et à faible niveau de performance, ainsi que sur une tablette.

### <a name="authentication"></a>Authentification

Pour que l'authentification fonctionne sur les clients mobiles, vous devez mettre à niveau le SDK JavaScript teams vers la version 1.4.1 au minimum.

### <a name="low-bandwidth-and-intermittent-connections"></a>Bande passante faible et connexions intermittentes

Les clients mobiles doivent régulièrement fonctionner avec une bande passante faible et des connexions intermittentes. Votre application doit gérer les délai d'accès de manière appropriée en fournissant un message contextuel à l'utilisateur. Vous devez également fournir des indicateurs de progression des utilisateurs pour fournir des commentaires à vos utilisateurs pour tout processus de longue durée.

> [!NOTE]
> Les onglets sont activés sur les appareils mobiles uniquement après l’ajout de l’application à une liste d’autorisation, en fonction de l’entrée de l’équipe d’approbation. Pour vérifier la réactivité de l’appareil mobile, teamsubm@microsoft.com. 
