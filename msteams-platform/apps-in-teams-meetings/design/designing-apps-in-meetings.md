---
title: Conception de votre extension de réunion
author: heath-hamilton
description: Découvrez comment concevoir des applications dans des réunions teams et obtenir le kit d’interface utilisateur Microsoft Teams.
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: 3d18895626d5f2846d10e7145a622834d82b2e98
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/09/2020
ms.locfileid: "49606133"
---
# <a name="designing-your-microsoft-teams-meeting-extension"></a>Conception de votre extension de réunion Microsoft teams

Vous pouvez créer des applications pour améliorer la productivité des réunions. Par exemple, demandez aux personnes de finaliser une enquête pendant un appel ou envoyez un rappel rapide qui n’interrompt pas le flux de la réunion.

## <a name="microsoft-teams-ui-kit"></a>Kit d’interface utilisateur Microsoft teams

Vous trouverez des instructions de conception plus complètes, notamment des éléments que vous pouvez saisir et modifier selon vos besoins, dans le kit d’interface utilisateur Microsoft Teams.

> [!div class="nextstepaction"]
> [Obtenir le kit d’interface utilisateur Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a>Ajouter une extension de réunion

Vous pouvez ajouter une extension de réunion avant et Pendant des réunions. Vous pouvez également une application pour une réunion spécifique directement à partir du magasin de Teams (AppSource).

### <a name="add-before-a-meeting"></a>Ajouter avant une réunion

Avant une réunion, les détails de la réunion sélectionnent **Ajouter un onglet +** pour ouvrir le menu volant d’application et Rechercher des applications optimisées pour les réunions.

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="Exemple montre comment ajouter une extension de réunion avant une réunion." border="false":::

### <a name="add-during-a-meeting"></a>Ajouter pendant une réunion

Dans une réunion, sélectionnez **plus** :::image type="icon" source="../../assets/icons/teams-client-more.png":::  >  **Ajouter une application** et choisissez l’application de votre choix.

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="Exemple montre comment ajouter une extension de réunion pendant une réunion." border="false":::

## <a name="before-a-meeting"></a>Avant une réunion

Avant la réunion, vous pouvez ajouter du contenu dans l’onglet. L’exemple suivant montre une question d’enquête préliminaire à laquelle les personnes répondront pendant l’appel.

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="Exemple montre comment afficher du contenu dans les détails de la réunion avant un appel." border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a>Anatomie : onglet réunion (avant et après les réunions)

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="Exemple illustre l’anatomie structurelle d’un onglet de réunion avant et après une réunion." border="false":::

|Compteur|Description|
|----------|-----------|
|1|**Nom** de l’onglet : étiquette de navigation pour votre onglet.|
|2 |**Débordement d’onglets**: ouvre les actions d’onglet, telles que renommer et supprimer.|
|3 |**IFRAME**: affiche le contenu de votre application.|

### <a name="designing-with-ui-templates"></a>Conception avec des modèles d’interface utilisateur

Utilisez l’un des modèles d’interface utilisateur teams suivants pour vous aider à concevoir votre onglet réunion :

* [Liste](../../concepts/design/design-teams-app-ui-templates.md#list): les listes peuvent afficher des éléments associés dans un format d’analyse et permettre aux utilisateurs d’effectuer des actions sur une liste entière ou des éléments individuels.
* [Tableau des tâches](../../concepts/design/design-teams-app-ui-templates.md#task-board): un tableau des tâches, parfois appelé tableau kanban ou couloirs de natation, est une collection de cartes souvent utilisées pour suivre l’état des éléments de travail ou des tickets.
* [Tableau](../../concepts/design/design-teams-app-ui-templates.md#dashboard)de bord : un tableau de bord est une zone de dessin contenant plusieurs cartes qui fournissent une vue d’ensemble des données ou du contenu.
* [Formulaire](../../concepts/design/design-teams-app-ui-templates.md#form): les formulaires permettent de collecter, de valider et de soumettre des entrées utilisateur de manière structurée.
* [État vide](../../concepts/design/design-teams-app-ui-templates.md#empty-state): le modèle d’état vide peut être utilisé pour de nombreux scénarios, notamment lors de la connexion, des expériences de première exécution, des messages d’erreur et bien plus encore.
* Navigation de [gauche](../../concepts/design/design-teams-app-ui-templates.md#left-nav): le modèle de navigation gauche peut vous aider si votre onglet nécessite une navigation. En règle générale, vous devez conserver la navigation par onglets au minimum.

## <a name="use-an-in-meeting-tab"></a>Utiliser un onglet de réunion

L’onglet dans la réunion est un canevas permettant d’augmenter la collaboration pendant les réunions. Les participants peuvent voir et interagir avec le contenu de l’application dans un espace dédié en dehors de la phase de réunion via des affichages partagés ou basés sur des rôles.

### <a name="use-cases"></a>Cas d'utilisation

Les utilisateurs peuvent utiliser l’onglet dans la réunion pour :

* Fournir des commentaires détaillés (par exemple, évaluer un candidat de travail)
* Créer rapidement un élément de sondage, d’enquête ou de tâche pour les participants à la réunion
* Afficher les notes relatives à la réunion (par exemple, informations sur un prospect)

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="Cet exemple montre comment vous pouvez présenter du contenu de sondage dans un onglet de réunion." border="false":::

### <a name="anatomy-in-meeting-tab"></a>Anatomie : onglet sous-réunion

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-anatomy.png" alt-text="Exemple illustre l’anatomie structurelle d’un onglet de réunion." border="false":::

|Compteur|Description|
|----------|-----------|
|1|**Icône de l’application (sélectionnée)**: logo de l’application transparente 16 pixels.|
|2 |**Nom de l'application**|
|3 |**En-tête**: inclut le nom de votre application.|
|4 |**Bouton Fermer : ferme** l’onglet. Toujours utiliser l’icône fermer en haut à droite au lieu d’une action dans le pied de page.|
|5 |**Barre de notification**: les alertes d’erreur s’affichent directement sous l’en-tête et redescendent le contenu iframe de 20 pixels.|
|6 |**IFRAME**: affiche le contenu de votre application.|

### <a name="spacing"></a>Espacement

Optimisez votre onglet de réunion pour qu’il s’ajuste au bord de la zone iframe de 280 pixels. Il y a 20 pixels de remplissage sur les côtés gauche et droit de l’IFRAME et entre l’en-tête d’onglet. L’iframe est un fond perdu en bas de l’onglet.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="Exemple affiche les dimensions d’espacement des tabulations dans la réunion." border="false":::

### <a name="scrolling"></a>Défilement

Le contenu d’un IFRAME doit faire défiler verticalement. Vous ne pouvez voir que le contenu auquel vous avez fait défiler (rien au-dessus ou en dessous). La barre de défilement fait partie du contenu IFRAME.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="Cet exemple montre comment faire défiler l’onglet de réunion." border="false":::

### <a name="navigation"></a>Navigation

Pour les scénarios avec des calques de navigation ou du contenu lourd, il est recommandé d’autoriser les utilisateurs à accéder à un calque secondaire. Les utilisateurs doivent pouvoir revenir à la couche précédente.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="Exemple illustre la navigation dans la réunion." border="false":::

## <a name="use-an-in-meeting-dialog"></a>Utiliser une boîte de dialogue de réunion

Les boîtes de dialogue de réunion sont affichées à l’étape de réunion Teams. Elles requièrent l’attention, la confirmation ou l’interaction d’un utilisateur, mais elles sont subtiles et n’interrompent pas la réunion. Vous devez les utiliser avec modération et pour les scénarios orientés sur les tâches et la lumière.

### <a name="use-cases"></a>Cas d'utilisation

Les boîtes de dialogue de réunion sont déclenchées par un utilisateur (par exemple, l’organisateur de la réunion) qui peut souhaiter que les participants :

* Fournir des commentaires succincts
* Suivre une brève enquête ou sondage
* Soumettre des approbations
* Obtenir les rappels

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="Exemple vous montre comment utiliser une boîte de dialogue de réunion." border="false":::

### <a name="anatomy-in-meeting-dialog"></a>Anatomie : boîte de dialogue de réunion

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-anatomy.png" alt-text="Exemple illustre l’anatomie structurelle d’une boîte de dialogue de réunion." border="false":::

|Compteur|Description|
|----------|-----------|
|1|**En-tête**: inclut l’icône de l’application, le nom, la chaîne d’action et l’icône fermer.|
|2 |**IFRAME**: affiche le contenu de votre application.|

### <a name="anatomy-in-meeting-dialog-header"></a>Anatomie : en-tête de boîte de dialogue de réunion

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="Exemple illustre l’anatomie structurelle d’un en-tête de boîte de dialogue de réunion." border="false":::

Il existe deux variantes d’en-tête. Dans la mesure du possible, utilisez la variante avec l’avatar pour renforcer le fait que la boîte de dialogue provient d’une personne.

|Compteur|Description|
|----------|-----------|
|1|**Avatar**: personne qui lance la boîte de dialogue de réunion.|
|2 |**Icône de l’application**|
|3 |**Nom de l'application**|
|4 |**Bouton Fermer : ferme** la boîte de dialogue.|
|5 |**Chaîne d’action**: indique généralement qui a initié la boîte de dialogue.|

### <a name="responsive-behavior"></a>Comportement réactif

Les boîtes de dialogue de réunion peuvent varier en fonction de la taille pour tenir compte de différents scénarios. Veillez à maintenir les tailles de remplissage et de composant.

* **Width**: la largeur de l’iframe est une valeur absolue comprise dans la plage que vous spécifiez.
* **Height**: la hauteur de la boîte de dialogue est déterminée par le contenu de l’IFRAME. Le défilement vertical est pris en charge pour le contenu qui dépasse la hauteur maximale.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="Exemple affiche la boîte de dialogue de réunion. Width : min--280 pixels (248 pixels IFRAME). Max--460 pixels (428 pixels IFRAME). Hauteur : 300 pixels (iframe)." border="false":::

## <a name="after-a-meeting"></a>Après une réunion

Vous pouvez revenir à une réunion une fois qu’elle a terminé et affiché le contenu de l’application. Dans cet exemple, l’organisateur de la réunion peut consulter les résultats de la recherche dans l’onglet **contoso** . (Remarque : du point de vue de la conception, il n’y a pas de différence entre les onglets pré-et post-réunion.)

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="Exemple montre un onglet post-réunion." border="false":::

## <a name="best-practices"></a>Meilleures pratiques

### <a name="interactions"></a>Leurs

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-do.png" alt-text="Exemple illustrant une meilleure pratique pour une extension de réunion." border="false":::

#### <a name="do-limit-the-number-of-interactions"></a>Do : limiter le nombre d’interactions

Pour les boîtes de dialogue de réunion, supprimez le contenu inutile qui ne permet pas aux utilisateurs d’effectuer une tâche rapidement.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-dont.png" alt-text="Exemple illustrant une meilleure pratique pour une extension de réunion." border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a>Ne pas faire : introduire des éléments inutiles

Une seule boîte de dialogue de réunion avec plusieurs interactions peut gêner l’appel.

   :::column-end:::
:::row-end:::

### <a name="layout"></a>Disposition

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="Exemple illustrant une meilleure pratique pour une extension de réunion." border="false":::

#### <a name="do-use-single-column-layouts"></a>Do : utiliser des mises en page à une seule colonne

Étant donné que les boîtes de dialogue sont au centre de l’étape de la réunion, l’exécution de la tâche doit être rapide et simple pour éviter toute frustration des utilisateurs.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-dont.png" alt-text="Exemple illustrant une meilleure pratique pour une extension de réunion." border="false":::

#### <a name="dont-clutter-the-space"></a>Ne pas : emcombrer l’espace

Le contenu dense ou très structuré peut être gênant et écrasant, en particulier lors d’une réunion.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-do.png" alt-text="Exemple illustrant une meilleure pratique pour une extension de réunion." border="false":::

#### <a name="do-use-single-columns"></a>Do : utiliser des colonnes uniques

Étant donné la nature étroite de l’onglet dans la réunion, nous vous recommandons vivement d’afficher le contenu dans une seule colonne.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-dont.png" alt-text="Exemple illustrant une meilleure pratique pour une extension de réunion." border="false":::

#### <a name="dont-use-multiple-columns"></a>Ne pas : utiliser plusieurs colonnes

En raison de l’espace limité de l’onglet dans la réunion, les mises en page comportant plusieurs colonnes ne sont pas recommandées.

   :::column-end:::
:::row-end:::

### <a name="controls"></a>Contrôles

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-do.png" alt-text="Exemple illustrant une meilleure pratique pour une extension de réunion." border="false":::

#### <a name="do-right-align-the-primary-action"></a>Do : aligner à droite l’action principale

Nous vous recommandons de positioining l’action la plus intense à l’emplacement le plus à droite.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-dont.png" alt-text="Exemple illustrant une meilleure pratique pour une extension de réunion." border="false":::

#### <a name="dont-left-or-center-align-actions"></a>Ne pas : Left ou Center align actions

Cela diffère du modèle standard teams pour le positionnement du contrôle dans une boîte de dialogue et peut entrer en conflit avec une boîte de dialogue située en arrière-plan.

   :::column-end:::
:::row-end:::

### <a name="scroll"></a>Faire défiler

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="Exemple illustrant une meilleure pratique pour une extension de réunion." border="false":::

#### <a name="do-scroll-vertically"></a>Do : faites défiler verticalement

Nous vous recommandons de placer l’action la plus intense à l’emplacement le plus à droite.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="Exemple illustrant une meilleure pratique pour une extension de réunion." border="false":::

#### <a name="dont-scroll-horizontally"></a>Ne pas faire défiler horizontalement

Le défilement horizontal n’est pas un comportement attendu dans Teams. Les autres canevas dans l’environnement de réunion sont déroulants verticalement.

   :::column-end:::
:::row-end:::

### <a name="workflows"></a>Flux de travail

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-workflow-do.png" alt-text="Exemple illustrant une meilleure pratique pour une extension de réunion." border="false":::

#### <a name="do-surface-complex-scenarios-in-the-in-meeting-tab"></a>Do : scénarios de surface complexe dans l’onglet de réunion

Si votre application inclut plusieurs tâches, nous vous recommandons vivement d’utiliser une disposition sur une seule colonne dans un onglet de réunion.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-workflow-dont.png" alt-text="Exemple illustrant une meilleure pratique pour une extension de réunion." border="false":::

#### <a name="dont-package-complex-scenarios-in-the-in-meeting-dialog"></a>Ne pas : créer un package de scénarios complexes dans la boîte de dialogue de réunion

Les boîtes de dialogue de réunion sont destinées à de brèves interactions.

   :::column-end:::
:::row-end:::

### <a name="theming"></a>Thèmes

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="Exemple illustrant une meilleure pratique pour une extension de réunion." border="false":::

#### <a name="do-use-teams-color-tokens"></a>Do : utiliser des jetons de couleur teams

Les réunions de teams sont optimisées pour le mode sombre afin de réduire le bruit visuel et cognitif afin que les utilisateurs puissent se concentrer sur la discussion et le contenu partagé. En savoir plus sur l’utilisation <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">de jetons de couleur (interface utilisateur Fluent)</a>.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="Exemple illustrant une meilleure pratique pour une extension de réunion." border="false":::

#### <a name="dont-include-another-dismiss-button"></a>Ne pas inclure un autre bouton ignorer

La fourniture d’une option permettant de fermer le contenu de l’onglet de réunion peut entraîner des problèmes, car il existe déjà un bouton dans l’en-tête pour faire disparaître l’onglet de réunion lui-même.

   :::column-end:::
:::row-end:::

### <a name="navigation"></a>Navigation

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-do.png" alt-text="Exemple illustrant une meilleure pratique pour une extension de réunion." border="false":::

#### <a name="do-have-a-back-button"></a>Do : avoir un bouton retour

Si vous avez plusieurs couches de navigation dans un onglet de réunion, les utilisateurs doivent pouvoir revenir à leurs vues précédentes.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-dont.png" alt-text="Exemple illustrant une meilleure pratique pour une extension de réunion." border="false":::

#### <a name="dont-include-another-dismiss-button"></a>Ne pas inclure un autre bouton ignorer

La fourniture d’une option permettant de fermer le contenu de l’onglet de réunion peut entraîner des problèmes, car il existe déjà un bouton dans l’en-tête pour faire disparaître l’onglet de réunion lui-même.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-caution.png" alt-text="Exemple illustrant une meilleure pratique pour une extension de réunion." border="false":::

#### <a name="caution-avoid-modals-within-the-in-meeting-tab"></a>ATTENTION : Évitez les éléments modaux au sein de l’onglet de réunion

Les modaux (également appelés modules de tâches) dans l’onglet de la réunion déjà étroite peuvent encapsuler et obscurcir le contenu.

   :::column-end:::
:::row-end:::

## <a name="validate-your-design"></a>Valider votre conception

Si vous envisagez de publier votre application dans AppSource, vous devez comprendre les problèmes de conception qui entraînent généralement l’échec des applications lors de l’envoi.

> [!div class="nextstepaction"]
> [Vérifier les instructions de validation de la conception](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
