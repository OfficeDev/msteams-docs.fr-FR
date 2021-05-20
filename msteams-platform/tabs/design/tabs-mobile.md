---
title: Onglets sur les appareils mobiles
description: Décrit les lignes directrices pour la conception d’onglets qui fonctionnent sur mobile.
ms.topic: conceptual
localization_priority: Normal
keywords: les équipes conçoivent des lignes directrices de référence cadre d’applications personnelles onglets mobiles
ms.openlocfilehash: 853ab2c52edd1f4faedcc92e6f0e8d0821b580c7
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566697"
---
# <a name="tabs-on-mobile"></a>Onglets sur les appareils mobiles

Vous pouvez inclure des onglets dans Teams canaux mobiles, des chats et des applications personnelles.

## <a name="accessing-personal-tabs"></a>Accéder aux onglets personnels

Vous pouvez accéder aux onglets personnels dans le tiroir de l’application.

:::image type="content" source="../../assets/images/tabs/mobile-app-drawer.png" alt-text="Illustration affichant le tiroir Teams d’application mobile." border="false":::

## <a name="accessing-channel-tabs"></a>Accéder aux onglets du canal

Vous pouvez accéder aux onglets de canal et de groupe en **sélectionnant le** bouton Plus dans le canal ou le chat dans lequel ils ont été ajoutés.

:::image type="content" source="../../assets/images/tabs/mobile-tab.png" alt-text="Illustration affichant un onglet mobile Teams de la maison." border="false":::

## <a name="design-considerations"></a>Considérations relatives à la conception

Notre plate-forme mobile permet aux applications d’être une expérience immersive avec le contenu de l’application prenant tout l’écran en dehors de la navigation Teams principale. Pour créer une expérience immersive qui s’adapte à Teams, suivez ces lignes directrices.

### <a name="responsive-design"></a>Conception réactive

Parce que votre onglet peut être ouvert sur les appareils avec un large éventail de tailles d’écran, il doit suivre les principes [de conception](https://www.w3schools.com/html/html_responsive.asp) réactive. Toutes les constructions clés doivent être accessibles sur les appareils mobiles, et les vues ne doivent pas être déformées. Assurez-vous que lorsque votre onglet est chargé sur un appareil mobile, tous les boutons et liens sont facilement accessibles à l’aide de la navigation basée sur les doigts.

### <a name="layouts"></a>Dispositions

Il est important de choisir la bonne disposition pour votre onglet. Vous devez tenir compte du type d’information que vous présentez, et choisir une mise en page qui l’organise pour une consommation facile. Certaines options potentielles sont décrites ci-dessous.

#### <a name="single-canvas"></a>Toile unique

C’est un grand domaine où le travail est fait. L Teams appr$ Wiki suit ce modèle. Si vous avez une application qui ne sépare pas le contenu en composants plus petits, ce serait un bon ajustement.

:::image type="content" source="../../assets/images/tabs/mobile-tab-single-canvas.png" alt-text="Illustration affichant un onglet Teams simple mobile de toile." border="false":::

#### <a name="list"></a>Répertorier

Les listes sont excellentes pour le tri et le filtrage de grandes quantités de données et sont excellentes pour garder les choses les plus importantes au sommet. Il est utile d’utiliser des colonnes triables. Des actions peuvent être ajoutées à chaque élément de liste dans le menu ellipsis.

:::image type="content" source="../../assets/images/tabs/mobile-tab-list.png" alt-text="Illustration affichant un onglet Teams liste mobile." border="false":::

#### <a name="grid"></a>grille

Les grilles sont utiles pour montrer des éléments très visuels. Il aide à inclure un filtre ou un contrôle de recherche en haut.

:::image type="content" source="../../assets/images/tabs/mobile-tab-grid.png" alt-text="Illustration affichant un onglet mobile Teams avec une disposition de grille." border="false":::

### <a name="tabs-with-bots-on-mobile"></a>Onglets avec bots sur mobile

L’exemple suivant est une application personnelle qui a des onglets et un bot:

:::image type="content" source="../../assets/images/tabs/mobile-tab-with-bot.png" alt-text="Illustration montrant comment l’application Teams mobile qui a des onglets et un bot." border="false":::

## <a name="ui-components"></a>Composants d’interface utilisateur

### <a name="color-palettes"></a>Palettes de couleurs

L’utilisation de notre palette neutre approuvée pour les arrière-plans, les notifications, le texte et les boutons aidera votre application à se sentir plus à l’aise Teams. Depuis Teams mobile a deux thèmes de couleur (clair et foncé), c’est une bonne idée de s’assurer que votre application ressemble beaucoup dans les deux.

#### <a name="light-color"></a>Couleur claire

![palette de couleurs claires](../../assets/images/light-color.png)

#### <a name="dark-color"></a>Couleur foncée

![palette de couleurs foncées](../../assets/images/dark-color.png)

### <a name="buttons-and-controls"></a>Boutons et commandes

La façon dont les boutons sont sifflés aide à communiquer quel type d’action ils déclenchent. Nous maintenons un large éventail de boutons qui sont formatés pour montrer différents niveaux d’emphase. Les boutons peuvent avoir du texte, une icône ou une combinaison de texte et d’icône. Pour communiquer différents niveaux dans une hiérarchie, nous avons conçu des boutons primaires et secondaires dans chaque catégorie.

#### <a name="buttons"></a>Boutons

Boutons primaires et secondaires.

![image boutons](../../assets/images/buttons.png)

#### <a name="selection-controls"></a>Contrôles de sélection

Boutons radio, caisses à cocher et basculements.

![contrôles de sélection](../../assets/images/selection-controls.png)

#### <a name="chiclets-and-pills"></a>Chiclets et pilules

![chiclets et pilules](../../assets/images/chiclets-and-pills.png)

### <a name="typography"></a>Typographie

La typographie doit être claire et délibérée. Mettez l’accent sur des informations importantes et évitez d’utiliser plusieurs polices et tailles pour réduire la confusion. Nous vous recommandons d’utiliser le cas de phrase et d’éviter l’utilisation de tous les plafonds pour la localisation et la lisibilité.

![typographe mobile](../../assets/images/mobile-typography.png)

### <a name="fields-and-flyouts"></a>Champs et flyouts

Les champs sont des domaines où les utilisateurs peuvent entrer du texte. Les flyouts sont plus légers que les dialogues et apparaissent à partir du volet supérieur.

#### <a name="list-controls"></a>Répertorier les contrôles

![contrôles de liste mobiles](../../assets/images/mobile-list-controls.png)

#### <a name="field-controls"></a>contrôles de champs

![commandes mobiles sur le terrain](../../assets/images/mobile-field-controls.png)

## <a name="developer-considerations"></a>Considérations des développeurs

Lorsque vous construisez une application qui inclut un onglet, vous devez considérer (et tester) comment votre onglet fonctionnera à la fois sur les clients Android et iOS Microsoft Teams clients. Les sections ci-dessous décrivent certains des scénarios clés que vous devez envisager.

### <a name="authentication"></a>Authentification

Pour que l’authentification fonctionne sur les clients mobiles, vous devez Teams javascript SDK à au moins la version 1.4.1.

### <a name="low-bandwidth-and-intermittent-connections"></a>Faible bande passante et connexions intermittentes

Les clients mobiles doivent régulièrement fonctionner avec une faible bande passante et des connexions intermittentes. Votre application doit gérer les délais d’attente de manière appropriée en fournissant un message contextuel à l’utilisateur. Vous devez également utiliser des indicateurs de progression pour fournir des commentaires à vos utilisateurs pour tous les processus de longue durée.

> [!NOTE]
> Les onglets ne sont activés sur mobile qu’après l’ajout de l’application à une liste d’autorisation, en fonction de l’entrée de l’équipe d’approbation. Pour vérifier la réactivité mobile, teindez la main à teamsubm@microsoft.com.

### <a name="testing-on-mobile-clients"></a>Tests sur les clients mobiles

Vous devez valider que votre onglet fonctionne correctement sur les appareils mobiles de différentes tailles et qualités. Pour les appareils Android, vous pouvez utiliser les [DevTools pour](~/tabs/how-to/developer-tools.md) débog vos onglets pendant qu’il est en cours d’exécution. Nous vous recommandons de tester sur les appareils haute et basse performance, y compris une tablette.

### <a name="distribution"></a>Distribution

Les applications répertoriées dans Teams magasin doivent être approuvées pour une utilisation mobile qui fonctionne correctement dans Teams client mobile. La disponibilité et le comportement de l’onglet dépendent de l’approbation ou non de votre application.

#### <a name="apps-on-teams-store-approved-for-mobile"></a>Applications sur Teams web approuvées pour mobile

Le tableau suivant décrit la disponibilité et le comportement de l’onglet lorsque l’application est répertoriée sur le Teams et approuvée pour un usage mobile :

|Fonctionnalité   |Disponibilité mobile ?   |Comportement mobile|
|----------|-----------|------------|
|Canal <br /> et onglet groupe|Oui|L’onglet s’ouvre Teams client mobile en utilisant la configuration de votre `contentUrl` application.|
|Application personnelle|Oui|Chaque onglet de l’onglet application personnelle s’ouvre dans le Teams client mobile en utilisant sa `contentUrl` configuration respective.|

#### <a name="apps-on-teams-store-not-approved-for-mobile"></a>Les applications sur Teams magasin non approuvé pour mobile

Le tableau suivant décrit la disponibilité et le comportement de l’onglet lorsque l’application est répertoriée sur le Teams store mais n’est pas approuvée pour une utilisation mobile :

| Fonctionnalité | Disponibilité mobile ? | Comportement mobile |
|----------|-----------|------------|
|Onglet Canal et groupe|Oui|L’onglet s’ouvre dans le navigateur par défaut de l’appareil au lieu du client mobile Teams utilisant la configuration de `websiteUrl` votre application, qui doit également être incluse dans la fonction de votre code `setSettings()` [](/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest#functions&preserve-view=true)source. Toutefois, les utilisateurs peuvent toujours afficher l’onglet dans le client mobile Teams en **sélectionnant Plus à côté** de l’application et **en choisissant Open**, qui déclenche la configuration de votre `contentUrl` application.|
|Application personnelle|Non|Non applicable|

#### <a name="apps-not-on-teams-store"></a>Applications non sur Teams store

Si vous chargez votre application ou publiez sur le catalogue d’applications d’une organisation, le comportement de l’onglet sera le même que les applications Teams store approuvées par Microsoft pour mobile.
