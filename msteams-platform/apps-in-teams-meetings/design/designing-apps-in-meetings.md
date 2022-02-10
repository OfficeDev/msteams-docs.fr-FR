---
title: Conception de votre extension de réunion
author: heath-hamilton
description: Découvrez comment concevoir des applications dans des réunions Teams et obtenir le kit d’interface utilisateur Microsoft Teams, l’onglet de réunion et les cas d’utilisation, le comportement réactif et la phase de réunion partagée, ainsi que le thème et la navigation.
ms.author: lajanuar
ms.localizationpriority: medium
ms.topic: conceptual
keywords: Modèle de kit d’interface utilisateur lors de la réunion - Phase de réunion partagée avec le comportement réactif
ms.openlocfilehash: e62146a4fb32f37145a818855749d68e64bee384
ms.sourcegitcommit: 60e4bbb013f0bb17a87a2e558abfcc311c73af75
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/10/2022
ms.locfileid: "62523794"
---
# <a name="designing-your-microsoft-teams-meeting-extension"></a>Conception de votre extension Microsoft Teams réunion

Vous pouvez créer des applications pour rendre les réunions plus productives. Par exemple, demandez aux personnes de répondre à une enquête au cours d’une réunion ou d’envoyer un rappel rapide qui n’interrompt pas le flux de la réunion.

## <a name="microsoft-teams-ui-kit"></a>Kit d’interface utilisateur de Microsoft Teams

Vous trouverez des instructions de conception plus complètes, y compris des éléments que vous pouvez récupérer et modifier selon vos besoins, dans Microsoft Teams kit d’interface utilisateur.

> [!div class="nextstepaction"]
> [Obtenir le Kit d’interface utilisateur de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a>Ajouter une extension de réunion

Les utilisateurs peuvent ajouter une extension de réunion avant et pendant les réunions. Ils peuvent également ajouter une application pour une réunion spécifique directement à partir du Teams store.

### <a name="add-before-a-meeting"></a>Ajouter avant une réunion

Dans les détails de la réunion, les utilisateurs peuvent sélectionner Ajouter un **onglet +** pour ouvrir le programme volant de l’application et rechercher des applications optimisées pour les réunions.

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="L’exemple montre comment ajouter une extension de réunion avant une réunion." border="false":::

### <a name="add-during-a-meeting"></a>Ajouter au cours d’une réunion

#### <a name="mobile"></a>Mobile

Une fois que l’application a été ajoutée (par exemple, sur le bureau), les utilisateurs peuvent accéder à l’application dans une réunion en sélectionnant **Plus** :::image type="icon" source="../../assets/icons/teams-client-more.png":::.

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-add-during-meeting.png" alt-text="L’exemple montre comment ajouter une extension de réunion lors d’une réunion sur mobile." border="false":::

#### <a name="desktop"></a>Ordinateur de bureau

Lors d’une réunion, les utilisateurs **peuvent sélectionner** :::image type="icon" source="../../assets/icons/teams-client-more.png"::: >  Ajouter une **application** et l’application de leur choix.

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="L’exemple montre comment ajouter une extension de réunion au cours d’une réunion." border="false":::

## <a name="before-a-meeting"></a>Avant une réunion

Avant une réunion, votre application est accessible aux utilisateurs sous un onglet. L’exemple suivant montre un brouillon de question d’enquête à qui les personnes répondront au cours de la réunion.

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="L’exemple montre comment apper le contenu des détails de la réunion avant un appel." border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a>Anatomie : onglet Réunion (avant et après les réunions)

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="L’exemple montre l’anatomie structurelle d’un onglet de réunion avant et après une réunion." border="false":::

|Compteur|Description|
|----------|-----------|
|1|**Nom de l’onglet** : étiquette de navigation pour votre onglet.|
|2|**Dépassement d’onglet** : ouvre les actions d’onglet, telles que renommer et supprimer.|
|3|**IFrame** : affiche le contenu de votre application.|

### <a name="design-with-ui-templates"></a>Conception avec des modèles d’interface utilisateur

Utilisez l’un des modèles d Teams’interface utilisateur suivants pour vous aider à concevoir votre onglet de réunion :

* [Liste](../../concepts/design/design-teams-app-ui-templates.md#list) : les listes peuvent afficher des éléments associés dans un format lisible et permettre aux utilisateurs d’agir sur une liste entière ou sur des éléments individuels.
* [Tableau des tâches](../../concepts/design/design-teams-app-ui-templates.md#task-board) : un tableau des tâches, parfois appelé « tableau kanban » ou « pistes de course » est une collection de cartes souvent utilisées pour suivre l’état des éléments de travail ou des tickets.
* [Tableau de bord](../../concepts/design/design-teams-app-ui-templates.md#dashboard) : un tableau de bord est un espace contenant plusieurs cartes qui fournissent une vue d’ensemble de données ou de contenu.
* [Formulaire](../../concepts/design/design-teams-app-ui-templates.md#form) : les formulaires sont conçus pour collecter, valider et envoyer des entrées utilisateur de manière structurée.
* [État vide](../../concepts/design/design-teams-app-ui-templates.md#empty-state) : le modèle d’état vide peut être utilisé pour de nombreux scénarios, y compris la connexion, les expériences de première exécution, les messages d’erreur et bien plus encore.
* [Navigation gauche](../../concepts/design/design-teams-app-advanced-ui-components.md#left-nav) : le composant de navigation gauche peut vous aider si votre onglet nécessite une navigation. En règle générale, vous devez conserver la navigation au minimum.

## <a name="use-an-in-meeting-tab"></a>Utiliser un onglet de réunion

L’onglet de réunion est un canevas qui permet d’accroître la collaboration pendant les réunions. Les participants peuvent voir et interagir avec le contenu de l’application dans un espace dédié en dehors de la phase de réunion par le biais d’affichages partagés ou basés sur des rôles.

### <a name="use-cases"></a>Cas d’utilisation

Les personnes peuvent utiliser l’onglet réunion pour :

* Fournissez des commentaires détaillés. Par exemple, évaluez un candidat au poste.
* Créez un sondage, une enquête ou un élément de tâche pour les participants à la réunion.
* Afficher les notes pertinentes pour la réunion. Par exemple, des informations sur un responsable commercial.

#### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-use-in-meeting-tab.png" alt-text="L’exemple montre comment présenter le contenu d’un sondage dans un onglet de réunion sur un appareil mobile." border="false":::

#### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="L’exemple montre comment présenter le contenu d’un sondage dans un onglet de réunion." border="false":::

### <a name="anatomy-in-meeting-tab"></a>Anatomie : onglet En réunion

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-anatomy.png" alt-text="L’exemple montre l’anatomie structurelle d’un onglet en réunion." border="false":::

|Compteur|Description|
|----------|-----------|
|1|**Icône de l’application (sélectionnée)** : logo d’application transparent de 16 pixels.|
|2|**Nom de l’application**|
|3|**En-tête :** inclut le nom de votre application.|
|4|**Bouton Fermer :** ferme l’onglet. Utilisez toujours l’icône de fermeture supérieure droite au lieu d’une action dans le pied de plan.|
|5|**Barre de notification** : les alertes d’erreur s’affichent directement sous l’en-tête et poussent le reste du contenu de votre iframe vers le bas de 20 pixels.|
|6 |**IFrame** : affiche le contenu de votre application.|

### <a name="spacing"></a>Espacement

Optimisez votre onglet de réunion pour qu’il s’adapte de bord à bord dans la zone iFrame de 280 pixels. Il y a 20 pixels de remplissage sur les côtés gauche et droit de l’iframe et entre l’en-tête de l’onglet. L’iframe est pleine page en bas de l’onglet.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="L’exemple montre les dimensions d’espacement des onglets dans la réunion." border="false":::

### <a name="scrolling"></a>Défilement

N’oubliez pas les choses suivantes si vous autorisez le défilement :

* Le contenu du contenu de l’iframe doit uniquement défiler verticalement.
* Les utilisateurs doivent voir uniquement le contenu vers qui ils ont fait défiler (rien au-dessus ou au-dessous). 
* La barre de défilement fait partie du contenu de l’iframe.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="L’exemple montre comment défile l’onglet dans la réunion." border="false":::

### <a name="navigation"></a>Navigation

Pour les scénarios avec des couches de navigation ou un contenu épais, nous vous recommandons de permettre aux utilisateurs d’accéder à une couche secondaire. Les utilisateurs doivent pouvoir revenir à la couche précédente.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="Exemple de navigation en réunion." border="false":::

## <a name="use-an-in-meeting-dialog"></a>Utiliser une boîte de dialogue de réunion

Les boîtes de dialogue de réunion s’affichent sur la Teams de réunion. Ils nécessitent l’attention, la confirmation ou l’interaction d’un utilisateur, mais sont discrets et n’interrompent pas la réunion. Vous devez les utiliser avec parcimonie et pour les scénarios légers et orientés vers les tâches.

### <a name="use-cases"></a>Cas d’utilisation

Les boîtes de dialogue de réunion sont déclenchées par un utilisateur (tel que l’organisateur de la réunion) qui souhaite peut-être que les participants :

* Fournir de brefs commentaires
* Prendre une courte enquête ou un sondage
* Envoyer des approbations
* Obtenir des rappels

### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-use-in-meeting-dialog.png" alt-text="L’exemple montre comment utiliser une boîte de dialogue en réunion sur un appareil mobile." border="false":::

### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="L’exemple montre comment utiliser une boîte de dialogue en réunion." border="false":::

### <a name="anatomy-in-meeting-dialog"></a>Anatomie : boîte de dialogue en réunion

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-anatomy.png" alt-text="L’exemple montre l’anatomie structurelle d’une boîte de dialogue en réunion." border="false":::

|Compteur|Description|
|----------|-----------|
|1|**En-tête :** inclut l’icône de l’application, le nom, la chaîne d’action et l’icône fermer.|
|2|**IFrame** : affiche le contenu de votre application.|

### <a name="anatomy-in-meeting-dialog-header"></a>Anatomie : en-tête de boîte de dialogue en réunion

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="L’exemple montre l’anatomie structurelle d’un en-tête de boîte de dialogue en réunion." border="false":::

Il existe deux variantes d’en-tête. Dans la mesure du possible, utilisez la variante avec l’avatar pour renforcer le fait que la boîte de dialogue vient d’une personne.

|Compteur|Description|
|----------|-----------|
|1|**Avatar** : personne qui initie la boîte de dialogue en réunion.|
|2|**Icône de l’application**|
|3|**Nom de l’application**|
|4|**Bouton Fermer :** ferme la boîte de dialogue.|
|5|**Chaîne d’action** : décrit généralement l’auteur de la boîte de dialogue.|

### <a name="responsive-behavior-in-meeting-dialogs"></a>Comportement réactif : boîtes de dialogue en réunion

Les boîtes de dialogue de réunion peuvent varier en taille pour tenir compte de différents scénarios. Veillez à maintenir le remplissage et les tailles de composants.

* **Largeur** : vous pouvez spécifier la largeur de l’iframe de la boîte de dialogue n’importe où dans la plage de tailles prise en charge.
* **Hauteur** : vous pouvez spécifier la hauteur de l’iframe de la boîte de dialogue n’importe où dans la plage de tailles prise en charge. Vous pouvez également autoriser les utilisateurs à faire défiler verticalement si le contenu de votre application dépasse la hauteur maximale.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="Exemple de boîte de dialogue en réunion. Largeur : Min--280 pixels (248 pixels iframe). Max--460 pixels (428 pixels iframe). Hauteur : 300 pixels (iframe)." border="false":::

## <a name="use-the-shared-meeting-stage"></a>Utiliser l’étape de réunion partagée

Vous pouvez permettre aux utilisateurs de partager et d’interagir avec tout ou partie du contenu de votre application lors de la phase de réunion. Voici quelques exemples d’utilisation possible de cette fonctionnalité lors d’une réunion :

* Modification d’un document
* Tableau blanc
* Examen d’un tableau de bord
* Regarder une vidéo
* Lecture d’un jeu

Les applications partagées à l’étape de la réunion occupent le même espace qu’un écran partagé. L’étape se réoriente également pour tous les participants à la réunion de la même manière.

> [!NOTE]
> Actuellement, les utilisateurs mobiles ne peuvent pas partager de contenu d’application à l’étape de la réunion. Cependant, ils peuvent voir le contenu partagé à partir du bureau.

### <a name="use-cases"></a>Cas d’utilisation

L’étape de la réunion partagée est une question de collaboration et de participation. Voici quelques exemples de scénarios pour vous aider à commencer.

:::row:::
   :::column span="1":::

**Modification et révision :** examinez les tableaux de bord et la planification avec tous les utilisateurs de la réunion.

   :::column-end:::
   :::column span="3":::

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-edit-review.png" alt-text="L’exemple montre un tableau de bord en cours de révision lors de la phase de réunion partagée." border="false":::

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-edit-review-component.png" alt-text="L’exemple montre un composant de tableau de bord en cours de révision lors de la phase de réunion partagée." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="1":::

**Tableau blanc :** dessin et idée ensemble sur une zone de dessin partagée.

   :::column-end:::
   :::column span="3":::

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-whiteboard.png" alt-text="L’exemple montre un tableau blanc sur la phase de réunion partagée." border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="1":::

**Questionnaire :** Tester les connaissances et obtenir des informations avec des supports interactifs.

   :::column-end:::
   :::column span="3":::

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-quiz.png" alt-text="Un exemple montre un questionnaire sur la phase de réunion partagée." border="false":::

   :::column-end:::
:::row-end:::

### <a name="anatomy-share-all-app-content-to-a-meeting"></a>Anatomie : partager tout le contenu de l’application à une réunion

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-anatomy.png" alt-text="L’image illustre l’anatomie de conception de la phase de réunion partagée lorsque tout le contenu de l’application est partagé." border="false":::

|Compteur|Description|
|----------|-----------|
|1|**Icône de l’application** : l’icône en surbrillant indique que l’onglet De réunion de l’application est ouvert.|
|2|**Bouton Partager avec la réunion** : point d’entrée pour partager l’application avec la réunion. S’affiche si vous configurez votre application pour utiliser la phase de réunion partagée.|
|3|**Attribution du présentateur** : affiche le nom du participant qui a partagé l’application.|
|4|**IFrame** : affiche le contenu de votre application.|
|5|**Bouton Arrêter le partage :** arrête le partage de l’application à la phase de réunion. S’affiche uniquement pour le participant qui a démarré le partage.|

### <a name="anatomy-share-specific-app-content-to-a-meeting"></a>Anatomie : partager du contenu d’application spécifique à une réunion

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-anatomy-component.png" alt-text="L’image illustre l’anatomie de conception de la phase de réunion partagée lorsque seul le contenu d’application spécifique est partagé." border="false":::

|Compteur|Description|
|----------|-----------|
|1|**Icône de l’application** : l’icône en surbrillant indique que l’onglet De réunion de l’application est ouvert.|
|2|**Bouton Partager avec la réunion** : point d’entrée pour partager l’application avec la réunion. Pour une expérience cohérente, utilisez toujours l’icône Teams partage standard. **Partager avec une réunion** est le texte par défaut recommandé, mais vous pouvez également le personnaliser pour vos cas d’utilisation. Par exemple, **lire ensemble pour** une application de jeu ou **Regarder ensemble** pour une application vidéo. Dans les deux cas, assurez-vous que l’action créera une expérience partagée et interactive avec tous les utilisateurs de la réunion.|
|3|**Attribution du présentateur** : affiche le nom du participant qui a partagé l’application.|
|4|**IFrame** : affiche le contenu de votre application.|
|5|**Bouton Arrêter le partage :** arrête le partage de l’application à la phase de réunion. S’affiche uniquement pour le participant qui a démarré le partage.|

### <a name="responsive-behavior-shared-meeting-stage"></a>Comportement réactif : étape de réunion partagée

Les applications partagées au stade de la réunion varient en taille en fonction de l’état de la réunion et de la façon dont l’utilisateur re dimensionne la fenêtre. Maintenez le remplissage et la disposition réactive de la navigation et des contrôles comme vous le feriez dans un navigateur.

* **Panneau** latéral : un utilisateur peut ouvrir le panneau latéral à tout moment au cours d’une réunion pour discuter, afficher la liste de membres ou utiliser une application (c’est-à-dire, l’onglet de la réunion). L’étape est réorganiser dynamiquement lorsque le panneau est ouvert.
* **Grille vidéo et audio :** la grille vidéo et audio est toujours visible pour afficher les participants à la réunion. Lorsqu’un utilisateur met à la une ou épingle une personne dans la réunion, cela augmente la hauteur ou la largeur de la grille des participants en fonction de l’orientation.

#### <a name="meeting-stage-without-side-panel"></a>Étape de la réunion (sans panneau latéral)

Lorsque le panneau latéral n’est pas ouvert, l’étape de la réunion est de 994 x 678 pixels par défaut et peut être d’au moins 792 x 382 pixels.

:::image type="content" source="~/assets/images/apps-in-meetings/meeting-stage-no-side-panel.png" alt-text="Image montrant la réactivité de la phase de réunion partagée avec le panneau latéral fermé." border="false":::

#### <a name="meeting-stage-with-side-panel"></a>Étape de la réunion (avec panneau latéral)

Lorsque le panneau latéral est ouvert, l’étape de la réunion est de 918 x 540 pixels par défaut et peut être d’au moins 472 x 382 pixels.

:::image type="content" source="~/assets/images/apps-in-meetings/meeting-stage-with-side-panel.png" alt-text="Image montrant la réactivité de la phase de réunion partagée avec le panneau latéral ouvert." border="false":::

## <a name="after-a-meeting"></a>Après une réunion

Vous pouvez revenir à une réunion une fois qu’elle s’est terminée et afficher le contenu de l’application. Dans cet exemple, l’organisateur de la réunion peut examiner les résultats des sondages dans l’onglet **Contoso** . (Remarque : du point de vue de la conception, il n’y a aucune différence entre l’expérience de l’onglet avant et après la réunion.)

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="L’exemple d’illustration montre un onglet après la réunion." border="false":::

## <a name="best-practices"></a>Meilleures pratiques

Utilisez ces recommandations pour créer une expérience d’application de qualité.

### <a name="interactions"></a>Interactions

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-do.png" alt-text="Exemple montrant comment limiter le nombre d’interactions." border="false":::

#### <a name="do-limit-the-number-of-interactions"></a>À faire : limiter le nombre d’interactions

Pour les boîtes de dialogue de réunion, supprimez le contenu inutile qui n’aide pas les utilisateurs à accomplir une tâche rapidement.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-dont.png" alt-text="Exemple montrant comment ne pas introduire d’éléments inutiles." border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a>À ne pas faire : introduire des éléments inutiles

Une seule boîte de dialogue de réunion avec plusieurs interactions peut distrayer la réunion.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-shared-stage-do.png" alt-text="Exemple montrant comment créer un environnement centré." border="false":::

#### <a name="do-create-a-focused-environment"></a>À faire : créer un environnement axé sur le travail

Nous vous recommandons de conserver l’étendue de l’expérience de votre application uniquement à la phase de réunion. Vous pouvez utiliser un onglet de réunion dans le panneau latéral en tant qu’affichage privé secondaire pour certains scénarios.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-shared-stage-dont.png" alt-text="Exemple montrant comment ne pas inclure de surfaces concurrentes pendant les réunions." border="false":::

#### <a name="dont-include-competing-surfaces"></a>À ne pas faire : inclure des surfaces concurrentes

Votre application doit uniquement demander aux utilisateurs de se concentrer sur une seule surface à la fois, qu’elle collabore sur la scène ou qu’elle réponde à une boîte de dialogue en réunion. (Remarque : vous ne pouvez pas conserver les boîtes de dialogue déclenchées par d’autres applications pendant que votre application est sur le terrain.) 

   :::column-end:::
:::row-end:::

### <a name="layout"></a>Disposition

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="Exemple montrant comment utiliser une mise en page de boîte de dialogue à une seule colonne." border="false":::

#### <a name="do-use-a-one-column-dialog"></a>À faire : utiliser une boîte de dialogue d’une colonne

Étant donné que les boîtes de dialogue sont au centre de la phase de réunion, l’achèvement des tâches doit être rapide et simple pour éviter toute frustration de l’utilisateur.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-dont.png" alt-text="Exemple montrant que vous ne devez pas encombrer l’espace d’une extension de réunion." border="false":::

#### <a name="dont-clutter-the-space"></a>À ne pas faire : encombrer l’espace

Le contenu épais ou trop structuré peut être gênant et gênant, en particulier lors d’une réunion.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-do.png" alt-text="Exemple montrant une disposition d’onglet à une seule colonne." border="false":::

#### <a name="do-use-a-one-column-tab"></a>À faire : utiliser un onglet d’une colonne

Étant donné la nature étroite de l’onglet en réunion, nous vous recommandons vivement d’afficher le contenu dans une seule colonne.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-dont.png" alt-text="Exemple montrant un onglet avec plusieurs colonnes." border="false":::

#### <a name="dont-use-multiple-columns"></a>À ne pas faire : utiliser plusieurs colonnes

En raison de l’espace limité de l’onglet en réunion, les dispositions avec plusieurs colonnes ne sont pas recommandées.

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
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-dont.png" alt-text="Exemple montrant comment ne pas aligner à gauche les contrôles principaux." border="false":::

#### <a name="dont-left-or-center-align-actions"></a>À ne pas faire : aligner les actions à gauche ou au centre

Cela s’écarte du modèle Teams standard pour l’emplacement des contrôles dans une boîte de dialogue et peut être en conflit avec une boîte de dialogue derrière la partie supérieure.

   :::column-end:::
:::row-end:::

### <a name="scrolling"></a>Défilement

:::row:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="Exemple de défilement vertical dans un onglet de réunion." border="false":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-scroll-do.png" alt-text="Exemple de défilement vertical dans l’étape de réunion partagée." border="false":::

#### <a name="do-scroll-vertically"></a>À faire : faire défiler verticalement

Les utilisateurs s’attendent à ce que le défilement vertical Teams (et ailleurs). Cela peut ne pas s’appliquer si vous avez un canevas créatif, tel qu’un tableau blanc, que les utilisateurs peuvent faire panoramique sur les axes x et y.

   :::column-end:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="Exemple de défilement horizontal dans un onglet de réunion." border="false":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-scroll-dont.png" alt-text="Exemple de défilement horizontal dans l’étape de réunion partagée." border="false":::

#### <a name="dont-scroll-horizontally"></a>À ne pas faire : faire défiler horizontalement

Le défilement horizontal n’est pas un comportement attendu dans Teams (y compris l’environnement de réunion).

   :::column-end:::
:::row-end:::

### <a name="workflows"></a>Flux de travail

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-workflow-do.png" alt-text="Exemple montrant un scénario complexe dans un onglet de réunion." border="false":::

#### <a name="do-surface-complex-scenarios-in-the-in-meeting-tab"></a>À faire : surfacer des scénarios complexes dans l’onglet réunion

Si votre application comprend plusieurs tâches, nous vous recommandons vivement d’utiliser un onglet de réunion avec une disposition sur une seule colonne.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-workflow-dont.png" alt-text="Exemple de scénarios complexes dans une boîte de dialogue en réunion." border="false":::

#### <a name="dont-make-in-meeting-dialogs-complex"></a>À ne pas faire : rendre les boîtes de dialogue de réunion complexes

Les boîtes de dialogue en réunion sont conçues pour de brèves interactions.

   :::column-end:::
:::row-end:::

### <a name="theming"></a>Thèmes

:::row:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="Exemple montrant une extension de réunion avec le thème foncé." border="false":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-theming-do.png" alt-text="Autre exemple montrant l’extension de réunion avec le thème foncé." border="false":::

#### <a name="do-focus-on-dark-theme"></a>À faire : concentrez-vous sur le thème foncé

Teams réunions sont optimisées pour le thème foncé afin de réduire les bruits visuels et cognitifs afin que les utilisateurs peuvent se concentrer sur la discussion et le contenu partagé. Gardez à l’esprit que certains types d’applications (par exemple, tableau blanc et modification de documents) n’ont pas besoin d’une zone de dessin sombre.

   :::column-end:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="Exemple montrant une extension de réunion avec des couleurs qui ne correspondent pas au thème de réunion." border="false":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-theming-dont.png" alt-text="Autre exemple montrant une extension de réunion avec des couleurs qui ne correspondent pas au thème de la réunion." border="false":::

#### <a name="dont-use-unfamiliar-colors"></a>À ne pas faire : utiliser des couleurs inconnues

Les couleurs qui entrent en conflit avec l’environnement de réunion peuvent être gênantes et apparaître moins natives Teams. Découvrez la palette de couleurs Teams[,](https://developer.microsoft.com/fluentui#/styles/web/colors/products) y compris les neutres du thème d’appel.

   :::column-end:::
:::row-end:::

### <a name="navigation"></a>Navigation

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-do.png" alt-text="Exemple montrant une extension de réunion avec un bouton Retour." border="false":::

#### <a name="do-have-a-back-button"></a>À faire : avoir un bouton Retour

Si vous avez plusieurs couches de navigation dans un onglet de réunion, les utilisateurs doivent pouvoir revenir à leurs vues précédentes.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-dont.png" alt-text="Exemple montrant une extension de réunion avec deux boutons d’mascmit." border="false":::

#### <a name="dont-include-another-dismiss-button"></a>À ne pas faire : inclure un autre bouton d’arrêt

La fourniture d’une option pour fermer le contenu de l’onglet en réunion peut entraîner des problèmes, car l’en-tête ne doit pas être fermé par un bouton.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-caution.png" alt-text="Exemple montrant des modales (ou des modules de tâche) dans un onglet de réunion." border="false":::

#### <a name="caution-avoid-modals-within-the-in-meeting-tab"></a>Attention : évitez les modales dans l’onglet de la réunion

Les modaux (également appelés modules de tâche) dans l’onglet déjà étroit de la réunion peuvent encapsuler et masquer le contenu.

   :::column-end:::
:::row-end:::

### <a name="responsive-behavior"></a>Comportement réactif

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-responsiveness-do.png" alt-text="Exemple montrant comment re tailler correctement une extension de réunion." border="false":::

#### <a name="do-resize-and-scale-your-app-responsively"></a>À faire : resize and scale your app responsively

Le contenu de l’application doit être resserre et condensé dynamiquement dans des fenêtres plus petites. Conservez la navigation principale de votre application et tous les contrôles flottants visibles.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-responsiveness-dont.png" alt-text="Exemple montrant comment ne pas re tailler correctement une extension de réunion." border="false":::

#### <a name="dont-crop-or-clip-primary-ui-components"></a>À ne pas faire : rognez ou clipez les composants principaux de l’interface utilisateur

La navigation flottante et les contrôles hors écran et la nécessité d’un défilement à rechercher peuvent prêter à confusion pour les utilisateurs. Le contenu de votre application ne doit pas défiler horizontalement lorsqu’il ne peut pas tenir dans l’iframe.

   :::column-end:::
:::row-end:::

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Configurer votre application pour les réunions](~/apps-in-teams-meetings/enable-and-configure-your-app-for-teams-meetings.md)
