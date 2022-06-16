---
title: Conception de votre extension de réunion
author: heath-hamilton
description: Découvrez comment concevoir des applications dans Teams réunions et obtenir le kit d’interface utilisateur Microsoft Teams, l’onglet en réunion, les cas d’usage, le comportement réactif, la phase de réunion partagée, le thème et la navigation.
ms.author: lajanuar
ms.localizationpriority: medium
ms.topic: conceptual
keywords: Étape de réunion partagée du modèle de kit d’interface utilisateur dans la réunion
ms.openlocfilehash: 5688e858fda4aa90fb4bfa75ca70c145308d97ca
ms.sourcegitcommit: 5070746e736edb4ae77cd3efcb2ab8bb2e5819a0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/16/2022
ms.locfileid: "66122998"
---
# <a name="designing-your-microsoft-teams-meeting-extension"></a>Conception de votre extension de réunion Microsoft Teams

Vous pouvez créer des applications pour rendre les réunions plus productives. Par exemple, demandez aux personnes de répondre à une enquête pendant une réunion ou d’envoyer un rappel rapide qui n’interrompt pas le flux de la réunion.

## <a name="microsoft-teams-ui-kit"></a>Kit d’interface utilisateur de Microsoft Teams

Vous trouverez des instructions de conception plus complètes, notamment des éléments que vous pouvez récupérer et modifier en fonction des besoins, dans le kit d’interface utilisateur Microsoft Teams.

> [!div class="nextstepaction"]
> [Obtenir le Kit d’interface utilisateur de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a>Ajouter une extension de réunion

Les utilisateurs peuvent ajouter une extension de réunion avant et pendant les réunions. Ils peuvent également ajouter une application pour une réunion spécifique directement à partir du magasin Teams.

### <a name="add-before-a-meeting"></a>Ajouter avant une réunion

Dans les détails de la réunion, les utilisateurs peuvent sélectionner **Ajouter un onglet +** pour ouvrir le menu volant de l’application et rechercher les applications optimisées pour les réunions.

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="Exemple montrant comment ajouter une extension de réunion avant une réunion." border="false":::

### <a name="add-during-a-meeting"></a>Ajouter pendant une réunion

#### <a name="mobile"></a>Mobile

Une fois l’application ajoutée (par exemple, sur le bureau), les utilisateurs peuvent accéder à l’application dans une réunion en sélectionnant **Plus**:::image type="icon" source="../../assets/icons/teams-client-more.png":::.

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-add-during-meeting.png" alt-text="Exemple montrant comment ajouter une extension de réunion pendant une réunion sur un appareil mobile." border="false":::

#### <a name="desktop"></a>Ordinateur de bureau

Dans une réunion, les utilisateurs peuvent sélectionner **Plus** :::image type="icon" source="../../assets/icons/teams-client-more.png"::: > **d’ajouter une application** et sélectionner l’application souhaitée.

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="Exemple montrant comment ajouter une extension de réunion pendant une réunion." border="false":::

## <a name="before-a-meeting"></a>Avant une réunion

Avant une réunion, votre application est disponible pour les utilisateurs sous un onglet. L’exemple suivant montre un brouillon de question d’enquête auquel les personnes répondront pendant la réunion.

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="L’exemple montre comment ajouter du contenu dans les détails de la réunion avant un appel." border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a>Anatomie : onglet Réunion (avant et après les réunions)

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="L’exemple montre l’anatomie structurelle d’un onglet de réunion avant et après une réunion." border="false":::

|Compteur|Description|
|----------|-----------|
|1|**Nom de l’onglet** : étiquette de navigation pour votre onglet.|
|2|**Dépassement d’onglet** : ouvre les actions d’onglet, telles que renommer et supprimer.|
|3|**IFrame** : affiche le contenu de votre application.|

### <a name="design-with-ui-templates"></a>Conception avec des modèles d'interface utilisateur

Utilisez l’un des modèles d’interface utilisateur Teams suivants pour vous aider à concevoir votre onglet de réunion :

* [Liste](../../concepts/design/design-teams-app-ui-templates.md#list) : les listes peuvent afficher des éléments associés dans un format lisible et permettre aux utilisateurs d’agir sur une liste entière ou sur des éléments individuels.
* [Tableau des tâches](../../concepts/design/design-teams-app-ui-templates.md#task-board) : un tableau des tâches, parfois appelé « tableau kanban » ou « pistes de course » est une collection de cartes souvent utilisées pour suivre l’état des éléments de travail ou des tickets.
* [Tableau de bord](../../concepts/design/design-teams-app-ui-templates.md#dashboard) : un tableau de bord est un espace contenant plusieurs cartes qui fournissent une vue d’ensemble de données ou de contenu.
* [Formulaire](../../concepts/design/design-teams-app-ui-templates.md#form) : les formulaires sont conçus pour collecter, valider et envoyer des entrées utilisateur de manière structurée.
* [État vide](../../concepts/design/design-teams-app-ui-templates.md#empty-state) : le modèle d’état vide peut être utilisé pour de nombreux scénarios, y compris la connexion, les expériences de première exécution, les messages d’erreur et bien plus encore.
* [Navigation gauche](../../concepts/design/design-teams-app-advanced-ui-components.md#left-nav) : le composant de navigation gauche peut vous aider si votre onglet nécessite une navigation. En général, vous devez conserver la navigation au minimum.

## <a name="use-an-in-meeting-tab"></a>Utiliser un onglet de réunion

L’onglet in-meeting est un canevas permettant d’accroître la collaboration pendant les réunions. Les participants peuvent voir et interagir avec le contenu de l’application dans un espace dédié en dehors de la phase de réunion via des vues partagées ou basées sur des rôles.

### <a name="use-cases"></a>Cas d’utilisation

Les personnes peuvent utiliser l’onglet in-meeting pour :

* Fournissez des commentaires détaillés. Par exemple, évaluez un candidat au poste.
* Créez un sondage, une enquête ou un élément de tâche pour les participants à la réunion.
* Affichez les notes relatives à la réunion. Par exemple, des informations sur un prospect.

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-use-in-meeting-tab.png" alt-text="L’exemple montre comment présenter le contenu d’un sondage dans un onglet de réunion sur mobile." border="false":::

#### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="L’exemple montre comment présenter le contenu d’un sondage dans un onglet de réunion." border="false":::

### <a name="anatomy-in-meeting-tab"></a>Anatomie : onglet Réunion

:::image type="content" source="../../assets/in-meeting-tab-anatomy.png" alt-text="L’exemple montre l’anatomie structurelle d’un onglet en réunion." border="false":::

|Compteur|Description|
|----------|-----------|
|1|**Icône d’application (sélectionnée)** : logo d’application transparent de 16 pixels.|
|2|**Nom de l'application**|
|3|**En-tête** : inclut le nom de votre application.|
|4|**Bouton Fermer** : ignore l’onglet. Utilisez toujours l’icône de fermeture supérieure droite au lieu d’une action dans le pied de page.|
|5|**Barre de notification** : les alertes d’erreur s’affichent directement sous l’en-tête et poussent le reste de votre contenu iframe vers le bas de 20 pixels.|
|6 |**IFrame** : affiche le contenu de votre application.|

### <a name="spacing"></a>Espacement

Optimisez votre onglet de réunion pour qu’il s’adapte de bord en périphérie dans la zone iframe de 280 pixels de large. Il y a 20 pixels de remplissage sur les côtés gauche et droit de l’iframe et entre l’en-tête d’onglet. L’iframe est entièrement saigné en bas de l’onglet.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="L’exemple montre les dimensions d’espacement des onglets dans la réunion." border="false":::

### <a name="scrolling"></a>Défilement

N’oubliez pas les éléments suivants si vous autorisez le défilement :

* Le contenu du contenu de l’iframe ne doit faire l’objet d’un défilement vertical que.
* Les utilisateurs doivent uniquement voir le contenu vers lequel ils ont fait défiler (rien au-dessus ou en dessous).
* La barre de défilement fait partie du contenu de l’iframe.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="Exemple montrant le défilement de l’onglet dans la réunion." border="false":::

### <a name="navigation"></a>Navigation

Pour les scénarios avec des couches de navigation ou un contenu lourd, nous vous recommandons d’autoriser les utilisateurs à accéder à une couche secondaire. Les utilisateurs doivent pouvoir revenir à la couche précédente.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="L’exemple montre la navigation dans la réunion." border="false":::

## <a name="use-an-in-meeting-dialog"></a>Utiliser une boîte de dialogue en réunion

Les dialogues en réunion s’affichent sur la Teams phase de réunion. Ils nécessitent l’attention, la confirmation ou l’interaction d’un utilisateur, mais sont subtils et n’interrompent pas la réunion. Vous devez les utiliser avec parcimonie et pour les scénarios légers et orientés tâches.

### <a name="use-cases"></a>Cas d’utilisation

Les dialogues en réunion sont déclenchés par un utilisateur (tel que l’organisateur de la réunion) qui peut souhaiter que les participants :

* Fournir de brefs commentaires
* Effectuer une courte enquête ou sondage
* Envoyer des approbations
* Obtenir des rappels

### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-use-in-meeting-dialog.png" alt-text="L’exemple montre comment utiliser une boîte de dialogue en réunion sur un appareil mobile." border="false":::

### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="Exemple montrant comment utiliser une boîte de dialogue en réunion." border="false":::

### <a name="anatomy-in-meeting-dialog"></a>Anatomie : boîte de dialogue en réunion

:::image type="content" source="../../assets/in-meeting-dialog-anatomy.png" alt-text="Exemple montrant l’anatomie structurelle d’une boîte de dialogue en réunion." border="false":::

|Compteur|Description|
|----------|-----------|
|1|**En-tête** : inclut l’icône d’application, le nom, la chaîne d’action et l’icône fermer.|
|2|**IFrame** : affiche le contenu de votre application.|

### <a name="anatomy-in-meeting-dialog-header"></a>Anatomie : en-tête de boîte de dialogue en réunion

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="Exemple montrant l’anatomie structurelle d’un en-tête de boîte de dialogue en réunion." border="false":::

Il existe deux variantes d’en-tête. Si possible, utilisez la variante avec l’avatar pour confirmer que la boîte de dialogue provient d’une personne.

|Compteur|Description|
|----------|-----------|
|1|**Avatar** : personne qui lance la boîte de dialogue en réunion.|
|2|**Icône de l’application**|
|3|**Nom de l'application**|
|4|**Bouton Fermer** : ignore la boîte de dialogue.|
|5|**Chaîne d’action** : décrit généralement qui a initié la boîte de dialogue.|

### <a name="responsive-behavior-in-meeting-dialogs"></a>Comportement réactif : boîtes de dialogue en réunion

La taille des boîtes de dialogue en réunion peut varier pour tenir compte de différents scénarios. Veillez à maintenir le remplissage et les tailles de composants.

* **Largeur** : vous pouvez spécifier la largeur de l’iframe de la boîte de dialogue n’importe où dans la plage de tailles prise en charge.
* **Hauteur** : vous pouvez spécifier la hauteur de l’iframe de la boîte de dialogue n’importe où dans la plage de taille prise en charge. Vous pouvez également autoriser les utilisateurs à faire défiler verticalement si le contenu de votre application dépasse la hauteur maximale.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="L’exemple montre la boîte de dialogue en réunion. Largeur : Min--280 pixels (iframe de 248 pixels). Max--460 pixels (428 pixels iframe). Hauteur : 300 pixels (iframe)." border="false":::

## <a name="use-the-shared-meeting-stage"></a>Utiliser la phase de réunion partagée

Vous pouvez autoriser les utilisateurs à partager et à interagir avec tout ou partie du contenu de votre application pendant la phase de réunion. Voici des exemples de la façon dont les utilisateurs peuvent utiliser cette fonctionnalité lors d’une réunion :

* Modification d’un document
* Tableau blanc
* Examen d’un tableau de bord
* Regarder une vidéo
* Jouer à un jeu

Les applications partagées dans la phase de réunion occupent le même espace qu’un écran partagé. La scène se réoriente également pour tous les participants à la réunion.

> [!NOTE]
> Actuellement, les utilisateurs mobiles ne peuvent pas partager le contenu de l’application à la phase de réunion. Toutefois, ils peuvent voir le contenu partagé à partir du bureau.

### <a name="use-cases"></a>Cas d’utilisation

La phase de réunion partagée est consacrée à la collaboration et à la participation. Voici quelques exemples de scénarios pour vous aider à commencer.

:::row:::
   :::column span="1":::

**Modifier et passer en revue** : explorez les tableaux de bord et la planification avec tous les participants à la réunion.

   :::column-end:::
   :::column span="3":::

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-edit-review.png" alt-text="L’exemple montre un tableau de bord en cours de révision lors de la phase de réunion partagée." border="false":::

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-edit-review-component.png" alt-text="L’exemple montre un composant de tableau de bord en cours de révision lors de la phase de réunion partagée." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="1":::

**Tableau blanc** : Dessinez et imbriquez ensemble sur un canevas partagé.

   :::column-end:::
   :::column span="3":::

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-whiteboard.png" alt-text="L’exemple montre un tableau blanc sur la phase de réunion partagée." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="1":::

**Questionnaire** : Testez les connaissances et obtenez des insights avec des matériaux interactifs.

   :::column-end:::
   :::column span="3":::

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-quiz.png" alt-text="L’exemple montre un questionnaire sur la phase de réunion partagée." border="false":::

   :::column-end:::
:::row-end:::

### <a name="anatomy-share-all-app-content-to-a-meeting"></a>Anatomie : Partager tout le contenu de l’application à une réunion

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-anatomy.png" alt-text="L’image montre l’anatomie de conception de la phase de réunion partagée lorsque tout le contenu de l’application est partagé." border="false":::

|Compteur|Description|
|----------|-----------|
|1|**Icône d’application** : l’icône en surbrillance indique que l’onglet in-meeting de l’application est ouvert.|
|2|**Bouton Partager vers la réunion** : point d’entrée pour partager l’application avec la réunion. S’affiche si vous configurez votre application pour utiliser la phase de réunion partagée.|
|3|**Attribution du présentateur** : affiche le nom du participant qui a partagé l’application.|
|4|**IFrame** : affiche le contenu de votre application.|
|5|**Bouton Arrêter le partage** : arrête le partage de l’application dans la phase de réunion. S’affiche uniquement pour le participant qui a démarré le partage.|

### <a name="anatomy-share-specific-app-content-to-a-meeting"></a>Anatomie : partager du contenu d’application spécifique à une réunion

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-anatomy-component.png" alt-text="L’image montre l’anatomie de conception de la phase de réunion partagée lorsque seul le contenu spécifique de l’application est partagé." border="false":::

|Compteur|Description|
|----------|-----------|
|1|**Icône d’application** : l’icône en surbrillance indique que l’onglet in-meeting de l’application est ouvert.|
|2|**Bouton Partager vers la réunion** : point d’entrée pour partager l’application avec la réunion. Pour une expérience cohérente, utilisez toujours l’icône de partage Teams standard. **Partager vers la réunion** est le texte par défaut recommandé, mais vous pouvez également le personnaliser pour vos cas d’usage. Par exemple, **jouez ensemble** pour une application de jeu ou **regardez ensemble** pour une application vidéo. Dans les deux cas, indiquez clairement que l’action créera une expérience interactive partagée avec tous les participants à la réunion.|
|3|**Attribution du présentateur** : affiche le nom du participant qui a partagé l’application.|
|4|**IFrame** : affiche le contenu de votre application.|
|5|**Bouton Arrêter le partage** : arrête le partage de l’application dans la phase de réunion. S’affiche uniquement pour le participant qui a démarré le partage.|

### <a name="responsive-behavior-shared-meeting-stage"></a>Comportement réactif : étape de réunion partagée

La taille des applications partagées dans la phase de réunion varie en fonction de l’état de la réunion et de la façon dont l’utilisateur redimensionne la fenêtre. Conservez le remplissage et la disposition réactive de la navigation et des contrôles comme vous le feriez dans un navigateur.

* **Panneau latéral** : un utilisateur peut avoir le panneau latéral ouvert à tout moment pendant une réunion pour discuter, afficher la liste de présence ou utiliser une application (c’est-à-dire, l’onglet réunion). L’étape se réorganise dynamiquement lorsque le panneau est ouvert.
* **Grille vidéo et audio** : la grille vidéo et audio est toujours visible pour afficher les participants à la réunion. Lorsqu’un utilisateur met en évidence ou épingle une personne dans la réunion, cela augmente la hauteur ou la largeur de la grille des participants en fonction de l’orientation.

#### <a name="meeting-stage-without-side-panel"></a>Étape de réunion (sans panneau latéral)

Lorsque le panneau latéral n’est pas ouvert, la phase de réunion est de 994 x 678 pixels par défaut et peut être d’au moins 792 x 382 pixels.

:::image type="content" source="~/assets/images/apps-in-meetings/meeting-stage-no-side-panel.png" alt-text="Image montrant la réactivité de la phase de réunion partagée avec le panneau latéral fermé." border="false":::

#### <a name="meeting-stage-with-side-panel"></a>Étape de réunion (avec panneau latéral)

Lorsque le panneau latéral est ouvert, la phase de réunion est de 918 x 540 pixels par défaut et peut être d’au moins 472 x 382 pixels.

:::image type="content" source="~/assets/images/apps-in-meetings/meeting-stage-with-side-panel.png" alt-text="Image montrant la réactivité de la phase de réunion partagée avec le panneau latéral ouvert." border="false":::

## <a name="after-a-meeting"></a>Après une réunion

Vous pouvez revenir à une réunion une fois celle-ci terminée et afficher le contenu de l’application. Dans cet exemple, l’organisateur de la réunion peut examiner les résultats du sondage sous l’onglet **Contoso** . (Remarque : Du point de vue de la conception, il n’existe aucune différence entre l’expérience de l’onglet avant et après la réunion.)

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="L’exemple d’illustration montre un onglet post-réunion." border="false":::

## <a name="best-practices"></a>Meilleures pratiques

Utilisez ces recommandations pour créer une expérience d’application de qualité.

### <a name="interactions"></a>Interactions

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-do.png" alt-text="Exemple montrant comment limiter le nombre d’interactions." border="false":::

#### <a name="do-limit-the-number-of-interactions"></a>À faire : limiter le nombre d’interactions

Pour les dialogues en réunion, supprimez le contenu inutile qui n’aide pas les utilisateurs à accomplir rapidement quelque chose.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-dont.png" alt-text="Exemple montrant comment ne pas introduire d’éléments inutiles." border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a>Ne pas : introduire des éléments inutiles

Une seule boîte de dialogue en réunion avec plusieurs interactions peut distraire la réunion.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-shared-stage-do.png" alt-text="Exemple montrant comment créer un environnement ciblé." border="false":::

#### <a name="do-create-a-focused-environment"></a>À faire : créer un environnement ciblé

Nous vous recommandons de limiter l’expérience de votre application à la phase de réunion. Vous pouvez utiliser un onglet en réunion dans le panneau latéral comme vue secondaire privée pour certains scénarios.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-shared-stage-dont.png" alt-text="Exemple montrant comment ne pas inclure de surfaces concurrentes pendant les réunions." border="false":::

#### <a name="dont-include-competing-surfaces"></a>Ne pas : inclure des surfaces concurrentes

Votre application ne doit demander aux utilisateurs de se concentrer que sur une seule surface à la fois, qu’il s’agisse de collaborer sur la scène ou de répondre à une boîte de dialogue en réunion. (Remarque : vous ne pouvez pas conserver les dialogues déclenchés par d’autres applications pendant que votre application est sur scène.)

   :::column-end:::
:::row-end:::

### <a name="layout"></a>Disposition

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="Exemple montrant comment utiliser une disposition de boîte de dialogue à une seule colonne." border="false":::

#### <a name="do-use-a-one-column-dialog"></a>À faire : utiliser une boîte de dialogue à une colonne

Étant donné que les dialogues sont au centre de la phase de réunion, l’achèvement des tâches doit être rapide et simple pour éviter la frustration de l’utilisateur.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-dont.png" alt-text="Exemple montrant que vous ne devez pas encombrer l’espace d’une extension de réunion." border="false":::

#### <a name="dont-clutter-the-space"></a>Ne pas : encombrer l’espace

Le contenu dense ou trop structuré peut être distrayant et écrasant, en particulier lors d’une réunion.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-do.png" alt-text="Exemple montrant une disposition d’onglet à une seule colonne." border="false":::

#### <a name="do-use-a-one-column-tab"></a>À faire : utiliser un onglet à une colonne

Étant donné la nature étroite de l’onglet en réunion, nous vous recommandons vivement d’afficher le contenu dans une seule colonne.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-dont.png" alt-text="Exemple montrant un onglet avec plusieurs colonnes." border="false":::

#### <a name="dont-use-multiple-columns"></a>Ne pas : utiliser plusieurs colonnes

En raison de l’espace limité de l’onglet in-meeting, les dispositions avec plusieurs colonnes ne sont pas recommandées.

   :::column-end:::
:::row-end:::

### <a name="controls"></a>Contrôles

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-do.png" alt-text="Exemple montrant comment aligner à droite les contrôles principaux." border="false":::

#### <a name="do-right-align-the-primary-action"></a>À faire : aligner à droite l’action principale

Nous vous recommandons de positionner l’action la plus lourde visuellement à l’emplacement le plus à droite.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-dont.png" alt-text="Exemple montrant comment vous ne devez pas aligner les contrôles principaux à gauche." border="false":::

#### <a name="dont-left-or-center-align-actions"></a>Ne pas : actions d’alignement à gauche ou au centre

Cela s’écarte du modèle de Teams standard pour le placement du contrôle dans une boîte de dialogue et peut entrer en conflit avec un dialogue situé derrière le premier.

   :::column-end:::
:::row-end:::

### <a name="scrolling"></a>Défilement

:::row:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="Exemple montrant le défilement vertical dans un onglet de réunion." border="false":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-scroll-do.png" alt-text="Exemple montrant le défilement vertical dans la phase de réunion partagée." border="false":::

#### <a name="do-scroll-vertically"></a>À faire : faire défiler verticalement

Les utilisateurs s’attendent à un défilement vertical dans Teams (et ailleurs). Cela peut ne pas s’appliquer si vous disposez d’un canevas créatif, tel qu’un tableau blanc, que les utilisateurs peuvent panoramiquer sur les axes x et y.

   :::column-end:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="Exemple montrant le défilement horizontal dans un onglet in-meeting." border="false":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-scroll-dont.png" alt-text="Exemple montrant le défilement horizontal dans la phase de réunion partagée." border="false":::

#### <a name="dont-scroll-horizontally"></a>Ne pas faire défiler horizontalement

Le défilement horizontal n’est pas un comportement attendu dans Teams (y compris l’environnement de réunion).

   :::column-end:::
:::row-end:::

### <a name="workflows"></a>Flux de travail

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-workflow-do.png" alt-text="Exemple montrant un scénario complexe dans un onglet en réunion." border="false":::

#### <a name="do-surface-complex-scenarios-in-the-in-meeting-tab"></a>À faire : Scénarios complexes de surface dans l’onglet in-meeting

Si votre application inclut plusieurs tâches, nous vous recommandons vivement d’utiliser un onglet en réunion avec une disposition à une seule colonne.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-workflow-dont.png" alt-text="Exemple montrant des scénarios complexes dans une boîte de dialogue en réunion." border="false":::

#### <a name="dont-make-in-meeting-dialogs-complex"></a>Ne pas : rendre les dialogues en réunion complexes

Les dialogues en réunion sont destinés à de brèves interactions.

   :::column-end:::
:::row-end:::

### <a name="theming"></a>Thèmes

:::row:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="Exemple montrant une extension de réunion avec le thème sombre." border="false":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-theming-do.png" alt-text="Autre exemple montrant l’extension de réunion avec le thème sombre." border="false":::

#### <a name="do-focus-on-dark-theme"></a>À faire : Concentrez-vous sur le thème sombre

Teams réunions sont optimisées pour le thème sombre afin de réduire le bruit visuel et cognitif afin que les utilisateurs puissent se concentrer sur la discussion et le contenu partagé. Gardez à l’esprit que certains types d’applications (par exemple, le tableau blanc et la modification de documents) n’ont pas besoin d’un canevas foncé.

   :::column-end:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="Exemple montrant une extension de réunion avec des couleurs qui ne correspondent pas au thème de la réunion." border="false":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-theming-dont.png" alt-text="Autre exemple montrant une extension de réunion avec des couleurs qui ne correspondent pas au thème de la réunion." border="false":::

#### <a name="dont-use-unfamiliar-colors"></a>Ne pas : utiliser des couleurs inconnues

Les couleurs qui entrent en conflit avec l’environnement de réunion peuvent être distrayantes et paraître moins natives pour Teams. Découvrez la rampe de [couleurs](https://developer.microsoft.com/fluentui#/styles/web/colors/products) Teams, y compris les neutres de thème d’appel.

   :::column-end:::
:::row-end:::

### <a name="navigation"></a>Navigation

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-do.png" alt-text="Exemple montrant une extension de réunion avec un bouton Précédent." border="false":::

#### <a name="do-have-a-back-button"></a>À faire : avoir un bouton Précédent

Si vous avez plusieurs couches de navigation dans un onglet de réunion, les utilisateurs doivent être en mesure de revenir à leurs vues précédentes.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-dont.png" alt-text="Exemple montrant une extension de réunion avec deux boutons ignorer." border="false":::

#### <a name="dont-include-another-dismiss-button"></a>Ne pas : inclure un autre bouton Ignorer

La possibilité de fermer le contenu de l’onglet de réunion peut entraîner des problèmes, car il existe déjà un bouton dans l’en-tête pour ignorer l’onglet dans la réunion lui-même.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-caution.png" alt-text="Exemple montrant des modaux (ou des modules de tâche) dans un onglet de réunion." border="false":::

#### <a name="caution-avoid-modals-within-the-in-meeting-tab"></a>Attention : Évitez les modales dans l’onglet in-meeting

Les modaux (également appelés modules de tâche) dans l’onglet déjà étroit de la réunion peuvent encapsuler et masquer le contenu.

   :::column-end:::
:::row-end:::

### <a name="responsive-behavior"></a>Comportement réactif

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-responsiveness-do.png" alt-text="Exemple montrant comment redimensionner correctement une extension de réunion." border="false":::

#### <a name="do-resize-and-scale-your-app-responsively"></a>À faire : redimensionner et mettre à l’échelle votre application de manière réactive

Le contenu de l’application doit se redimensionner et se condenser dynamiquement dans des fenêtres plus petites. Gardez la navigation principale de votre application et tous les contrôles flottants visibles.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-responsiveness-dont.png" alt-text="Exemple montrant comment ne pas redimensionner correctement une extension de réunion." border="false":::

#### <a name="dont-crop-or-clip-primary-ui-components"></a>Ne pas : rogner ou découper les composants principaux de l’interface utilisateur

La navigation flottante et les contrôles hors écran et nécessitant un défilement pour trouver peuvent prêter à confusion pour les utilisateurs. Le contenu de votre application ne doit pas défiler horizontalement lorsqu’il ne peut pas tenir dans l’iframe.

   :::column-end:::
:::row-end:::

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Configurer votre application pour les réunions](~/apps-in-teams-meetings/enable-and-configure-your-app-for-teams-meetings.md)
