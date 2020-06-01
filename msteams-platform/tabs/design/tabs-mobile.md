---
title: Onglets sur les appareils mobiles
description: Décrit les instructions permettant de concevoir des onglets qui fonctionnent sur mobile.
keywords: instructions de conception teams structure de référence des applications personnelles onglets mobiles
ms.openlocfilehash: 6fe40b9cc5b6e898d0f0bce14b3dfedfd2c14032
ms.sourcegitcommit: 61c93b22490526b1de87c0b14a3c7eb6e046caf6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/31/2020
ms.locfileid: "44455519"
---
# <a name="tabs-on-mobile"></a>Onglets sur les appareils mobiles

Les onglets personnalisés peuvent faire partie d’un canal, d’une conversation de groupe ou d’une application personnelle (applications qui contiennent des onglets statiques et/ou un bot un-à-un).

Les applications personnelles sont disponibles sur les clients mobiles dans le tiroir d’application. L’application ne peut être installée qu’à partir d’un client de bureau ou Web, et peut prendre jusqu’à 24 heures pour apparaître sur les clients mobiles.

Les onglets de groupe et de canal sont également disponibles sur les clients mobiles. Le comportement par défaut consiste à utiliser votre `websiteUrl` pour lancer votre onglet dans une fenêtre de navigateur. Toutefois, ils peuvent être chargés sur un client mobile en cliquant sur le `...` menu de dépassement de capacité en regard de l’onglet et en choisissant **ouvrir**, qui utilisera votre `contentUrl` pour charger l’onglet à l’intérieur du client mobile Teams.

![tiroir d’application mobile](../../assets/images/personal-app-mobile.png)

## <a name="developer-considerations-for-mobile-support"></a>Considérations pour les développeurs concernant la prise en charge mobile

Lorsque vous créez une application qui comprend un onglet, vous devez prendre en compte (et tester) le fonctionnement de votre onglet sur les clients Microsoft teams Android et iOS. Les sections ci-dessous décrivent certains des scénarios clés que vous devez prendre en compte.

### <a name="testing-on-mobile-clients"></a>Test sur les clients mobiles

Vous devez vérifier que votre onglet fonctionne correctement sur les appareils mobiles de différentes tailles et qualités. Pour les appareils Android, vous pouvez utiliser le [devtools](~/tabs/how-to/developer-tools.md) pour déboguer votre onglet pendant qu’il est en cours d’exécution. Nous vous recommandons de tester sur les périphériques à haute et basse performance, ainsi qu’sur une tablette.

### <a name="responsive-design"></a>Conception réactive

Étant donné que votre onglet peut être ouvert sur des appareils avec un large éventail de tailles d’écran, il doit suivre des principes de [conception réactives](https://www.w3schools.com/html/html_responsive.asp) . Toutes les constructions clés doivent être accessibles sur les appareils mobiles, et les vues ne doivent pas être déformées. Assurez-vous que, lorsque votre onglet est chargé sur un appareil mobile, tous les boutons et liens sont facilement accessibles à l’aide de la navigation par doigt.

### <a name="authentication"></a>Authentification

Pour que l’authentification fonctionne sur les clients mobiles, vous devez mettre à niveau le kit de développement logiciel (SDK) teams JS vers la version 1.4.1 au moins.

### <a name="low-bandwidth--intermittent-connections"></a>Bande passante faible & les connexions intermittentes

Les clients mobiles doivent régulièrement fonctionner avec une faible bande passante et des connexions intermittentes. Votre application doit gérer les délais d’expiration appropriés en fournissant un message contextuel à l’utilisateur. Vous devez également indiquer les indicateurs de progression de l’utilisateur pour fournir des commentaires à vos utilisateurs pour tous les processus de longue durée.

## <a name="design-considerations-for-mobile"></a>Considérations relatives à la conception pour les appareils mobiles

Notre plate-forme mobile permet aux applications d’être immersifs avec le contenu de l’application qui occupe tout l’écran, à l’exception de la navigation principale dans Teams. Pour créer une expérience immersive qui s’intègre en toute transparence dans le client Microsoft Teams, suivez les instructions ci-dessous.

### <a name="layouts"></a>Dispositions

Le choix de la disposition appropriée pour votre onglet est important. Vous devez tenir compte du type d’informations que vous présentez et choisir une mise en page qui l’organise pour une consommation facile. Certaines options potentielles sont présentées ci-dessous.

#### <a name="single-canvas"></a>Seule zone de dessin

Il s’agit d’une grande zone dans laquelle le travail est exécuté. L’application wiki suit ce modèle. Si vous avez une application qui ne sépare pas le contenu en composants plus petits, il s’agit d’une solution adaptée.

![disposition sur une seule zone de dessin](~/assets/images/mobile-single-canvas.png)

#### <a name="list"></a>Répertorier

Les listes sont idéales pour le tri et le filtrage de grandes quantités de données et sont idéales pour conserver les choses les plus importantes en haut. Il est utile d’utiliser des colonnes à trier. Les actions peuvent être ajoutées à chaque élément de liste sous le menu points de suspension.

![disposition de liste](~/assets/images/mobile-list.png)

#### <a name="grid"></a>Treillis

Les grilles sont utiles pour afficher des éléments qui sont extrêmement visuels. Elle permet d’inclure un filtre ou un contrôle de recherche dans la partie supérieure.

![disposition Grille](~/assets/images/mobile-grid.png)

### <a name="tabs-with-bots-on-mobile"></a>Onglets avec robots sur mobile

Voici un exemple d’application personnelle qui contient deux onglets statiques et un bot.

![onglets et bots sur mobile](~/assets/images/mobile-tab-with-bot.png)

### <a name="ui-components"></a>Composants interface utilisateur

#### <a name="color-palettes"></a>Palettes de couleurs

L’utilisation de notre palette de couleurs neutre approuvée pour les arrière-plans, les notifications, le texte et les boutons aidera votre application à se sentir plus à la maison dans Teams. Étant donné que teams mobile comporte deux thèmes de couleur (clair et sombre), il est recommandé de s’assurer que votre application paraît belle dans les deux.

##### <a name="light-color"></a>Couleur claire

![palette de couleurs claires](~/assets/images/light-color.png)

##### <a name="dark-color"></a>Couleur foncée

![palette de couleurs sombres](~/assets/images/dark-color.png)

#### <a name="buttons-and-controls"></a>Boutons et contrôles

Le style des boutons permet de communiquer le type d’action qu’ils déclenchent. Nous mettons à jour un large éventail de boutons qui sont mis en forme pour afficher différents niveaux de mise en relief. Les boutons peuvent contenir du texte, une icône ou une combinaison de texte et d’icône. Pour communiquer différents niveaux dans une hiérarchie, nous avons conçu les boutons principal et secondaire dans chaque catégorie.

![descendre](~/assets/images/buttons.png)

![contrôles de sélection](~/assets/images/selection-controls.png)

![chiclets et pilules](~/assets/images/chiclets-and-pills.png)

#### <a name="typography"></a>Typographie

La typographie doit être claire et volontaire. Insistez sur les informations importantes et évitez d’utiliser plusieurs polices et tailles pour réduire la confusion. Nous vous recommandons d’utiliser la casse des phrases et d’éviter l’utilisation de toutes les majuscules pour la localisation et la lisibilité.

![Typograph mobile](~/assets/images/mobile-typography.png)

#### <a name="fields-and-flyouts"></a>Champs et menus volants

Les champs sont des zones dans lesquelles les utilisateurs peuvent entrer du texte. Les lanceurs sont plus légers que les boîtes de dialogue et s’affichent dans le volet supérieur.

##### <a name="list-controls"></a>Répertorier les contrôles

![contrôles de liste mobile](~/assets/images/mobile-list-controls.png)

##### <a name="field-controls"></a>contrôles de champs

![contrôles de champ mobiles](~/assets/images/mobile-field-controls.png)
