---
title: Onglets sur les appareils mobiles
description: Décrit les instructions permettant de concevoir des onglets qui fonctionnent sur mobile.
keywords: instructions de conception teams structure de référence des applications personnelles onglets mobiles
ms.openlocfilehash: a1939465b04a1fe4b803efaf83402852ca536059
ms.sourcegitcommit: b51a4982842948336cfabedb63bdf8f72703585e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/25/2020
ms.locfileid: "48279765"
---
# <a name="tabs-on-mobile"></a>Onglets sur les appareils mobiles

> [!NOTE]
> Si vous choisissez d’afficher l’onglet canal/groupe sur les clients mobiles Teams, la `setSettings()` configuration doit avoir une valeur pour la `websiteUrl` propriété (voir ci-dessous).

Les onglets personnalisés peuvent faire partie d’un canal, d’une conversation de groupe ou d’une application personnelle (applications qui contiennent des onglets statiques et/ou un bot un-à-un).

Les applications personnelles sont disponibles sur les clients mobiles dans le tiroir d’application. L’application ne peut être installée qu’à partir d’un client de bureau ou Web, et peut prendre jusqu’à 24 heures pour apparaître sur les clients mobiles.

Les onglets de canal sont également disponibles sur mobile. Le comportement par défaut consiste à utiliser votre `websiteUrl` pour lancer votre onglet dans une fenêtre de navigateur. Toutefois, ils peuvent être chargés sur un client mobile en cliquant sur le `...` menu de dépassement de capacité en regard de l’onglet et en choisissant **ouvrir**, qui utilisera votre `contentUrl` pour charger l’onglet à l’intérieur du client mobile Teams.

## <a name="accessing-personal-tabs"></a>Accès aux onglets personnels

L’illustration suivante montre comment accéder à un onglet personnel sur mobile.

:::image type="content" source="../../assets/images/tabs/mobile-app-drawer.png" alt-text="Illustration illustrant le tiroir d’une application mobile Teams." border="false":::

## <a name="accessing-channel-tabs"></a>Accès aux onglets des canaux

L’illustration suivante montre comment accéder à un onglet de canal sur mobile.

:::image type="content" source="../../assets/images/tabs/mobile-tab.png" alt-text="Illustration illustrant un onglet teams mobile." border="false":::

## <a name="design-considerations"></a>Considérations relatives à la conception

Notre plate-forme mobile permet aux applications d’être immersifs avec le contenu de l’application qui occupe tout l’écran, à l’exception de la navigation principale dans Teams. Pour créer une expérience immersive qui s’intègre à Teams, suivez ces instructions.

### <a name="responsive-design"></a>Conception réactive

Étant donné que votre onglet peut être ouvert sur des appareils avec un large éventail de tailles d’écran, il doit suivre des principes de [conception réactives](https://www.w3schools.com/html/html_responsive.asp) . Toutes les constructions clés doivent être accessibles sur les appareils mobiles, et les vues ne doivent pas être déformées. Assurez-vous que, lorsque votre onglet est chargé sur un appareil mobile, tous les boutons et liens sont facilement accessibles à l’aide de la navigation par doigt.

### <a name="layouts"></a>Dispositions

Le choix de la disposition appropriée pour votre onglet est important. Vous devez tenir compte du type d’informations que vous présentez et choisir une mise en page qui l’organise pour une consommation facile. Certaines options potentielles sont présentées ci-dessous.

#### <a name="single-canvas"></a>Seule zone de dessin

Il s’agit d’une grande zone dans laquelle le travail est exécuté. L’application wiki teams suit ce modèle. Si vous avez une application qui ne sépare pas le contenu en composants plus petits, il s’agit d’une solution adaptée.

:::image type="content" source="../../assets/images/tabs/mobile-tab-single-canvas.png" alt-text="Illustration illustrant un onglet de canevas mobile simple Teams." border="false":::

#### <a name="list"></a>Répertorier

Les listes sont idéales pour le tri et le filtrage de grandes quantités de données et sont idéales pour conserver les choses les plus importantes en haut. Il est utile d’utiliser des colonnes à trier. Les actions peuvent être ajoutées à chaque élément de liste sous le menu points de suspension.

:::image type="content" source="../../assets/images/tabs/mobile-tab-list.png" alt-text="Illustration illustrant un onglet de liste de teams mobile." border="false":::

#### <a name="grid"></a>Treillis

Les grilles sont utiles pour afficher des éléments qui sont extrêmement visuels. Elle permet d’inclure un filtre ou un contrôle de recherche dans la partie supérieure.

:::image type="content" source="../../assets/images/tabs/mobile-tab-grid.png" alt-text="Illustration illustrant un onglet teams mobile avec une disposition grille." border="false":::

### <a name="tabs-with-bots-on-mobile"></a>Onglets avec robots sur mobile

L’exemple suivant est une application personnelle qui comporte des onglets et un bot.

:::image type="content" source="../../assets/images/tabs/mobile-tab-with-bot.png" alt-text="Illustration illustrant la façon dont les applications mobiles teams possèdent des onglets et un bot." border="false":::

## <a name="ui-components"></a>Composants de l’interface utilisateur

### <a name="color-palettes"></a>Palettes de couleurs

L’utilisation de notre palette de couleurs neutre approuvée pour les arrière-plans, les notifications, le texte et les boutons aidera votre application à se sentir plus à la maison dans Teams. Étant donné que teams mobile comporte deux thèmes de couleur (clair et sombre), il est recommandé de s’assurer que votre application paraît belle dans les deux.

#### <a name="light-color"></a>Couleur claire

![palette de couleurs claires](../../assets/images/light-color.png)

#### <a name="dark-color"></a>Couleur foncée

![palette de couleurs sombres](../../assets/images/dark-color.png)

### <a name="buttons-and-controls"></a>Boutons et contrôles

Le style des boutons permet de communiquer le type d’action qu’ils déclenchent. Nous mettons à jour un large éventail de boutons qui sont mis en forme pour afficher différents niveaux de mise en relief. Les boutons peuvent contenir du texte, une icône ou une combinaison de texte et d’icône. Pour communiquer différents niveaux dans une hiérarchie, nous avons conçu les boutons principal et secondaire dans chaque catégorie.

#### <a name="buttons"></a>Boutons

Boutons principal et secondaire.

![image des boutons](../../assets/images/buttons.png)

#### <a name="selection-controls"></a>Contrôles de sélection

Cases d’option, cases à cocher et basculements.

![contrôles de sélection](../../assets/images/selection-controls.png)

#### <a name="chiclets-and-pills"></a>Chiclets et pilules

![chiclets et pilules](../../assets/images/chiclets-and-pills.png)

### <a name="typography"></a>Typographie

La typographie doit être claire et volontaire. Insistez sur les informations importantes et évitez d’utiliser plusieurs polices et tailles pour réduire la confusion. Nous vous recommandons d’utiliser la casse des phrases et d’éviter l’utilisation de toutes les majuscules pour la localisation et la lisibilité.

![Typograph mobile](../../assets/images/mobile-typography.png)

### <a name="fields-and-flyouts"></a>Champs et lanceurs

Les champs sont des zones dans lesquelles les utilisateurs peuvent entrer du texte. Les lanceurs sont plus légers que les boîtes de dialogue et s’affichent à partir du volet supérieur.

#### <a name="list-controls"></a>Répertorier les contrôles

![contrôles de liste mobile](../../assets/images/mobile-list-controls.png)

#### <a name="field-controls"></a>contrôles de champs

![contrôles de champ mobiles](../../assets/images/mobile-field-controls.png)

## <a name="developer-considerations"></a>Considérations pour les développeurs

Lorsque vous créez une application qui comprend un onglet, vous devez prendre en compte (et tester) le fonctionnement de votre onglet sur les clients Microsoft teams Android et iOS. Les sections ci-dessous décrivent certains des scénarios clés que vous devez prendre en compte.

### <a name="testing-on-mobile-clients"></a>Test sur les clients mobiles

Vous devez vérifier que votre onglet fonctionne correctement sur les appareils mobiles de différentes tailles et qualités. Pour les appareils Android, vous pouvez utiliser le [devtools](~/tabs/how-to/developer-tools.md) pour déboguer votre onglet pendant qu’il est en cours d’exécution. Nous vous recommandons de tester sur les périphériques à haute et basse performance, ainsi qu’sur une tablette.

### <a name="authentication"></a>Authentification

Pour que l’authentification fonctionne sur les clients mobiles, vous devez mettre à niveau teams JavaScript SDK vers la version 1.4.1 au moins.

### <a name="low-bandwidth-and-intermittent-connections"></a>Bande passante faible et connexions intermittentes

Les clients mobiles doivent régulièrement fonctionner avec une faible bande passante et des connexions intermittentes. Votre application doit gérer les délais d’expiration appropriés en fournissant un message contextuel à l’utilisateur. Vous devez également indiquer les indicateurs de progression de l’utilisateur pour fournir des commentaires à vos utilisateurs pour tous les processus de longue durée.
