---
title: Conception de votre extension de réunion
author: heath-hamilton
description: Découvrez comment concevoir des applications dans Teams réunions et obtenir le kit Microsoft Teams’interface utilisateur.
ms.author: lajanuar
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: 33b11a6dfc759fabd54ca2fe2c68978a5d5d1475
ms.sourcegitcommit: 4224c44d169b1a289cbf1d3353de6bc6de7c7ea8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/25/2021
ms.locfileid: "52644616"
---
# <a name="designing-your-microsoft-teams-meeting-extension"></a>Conception de votre extension Microsoft Teams réunion

Vous pouvez créer des applications pour rendre les réunions plus productives. Par exemple, demandez aux personnes de répondre à une enquête pendant un appel ou d’envoyer un rappel rapide qui n’interrompt pas le flux de la réunion.

## <a name="microsoft-teams-ui-kit"></a>Kit d’interface utilisateur de Microsoft Teams

Vous trouverez des instructions de conception plus complètes, y compris des éléments que vous pouvez récupérer et modifier selon vos besoins, dans le kit Microsoft Teams’interface utilisateur.

> [!div class="nextstepaction"]
> [Obtenir le Kit d’interface utilisateur de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a>Ajouter une extension de réunion

Les utilisateurs peuvent ajouter une extension de réunion avant et pendant les réunions. Ils peuvent également ajouter une application pour une réunion spécifique directement à partir du Teams store.

### <a name="add-before-a-meeting"></a>Ajouter avant une réunion

Dans les détails de la réunion, les utilisateurs peuvent sélectionner Ajouter un **onglet +** pour ouvrir le programme volant de l’application et rechercher des applications optimisées pour les réunions.

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="L’exemple montre comment ajouter une extension de réunion avant une réunion." border="false":::

### <a name="add-during-a-meeting"></a>Ajouter au cours d’une réunion

# <a name="desktop"></a>[Desktop](#tab/desktop)

Lors d’une réunion, les utilisateurs peuvent sélectionner **Plus** ajouter :::image type="icon" source="../../assets/icons/teams-client-more.png":::  >  **une application** et choisir l’application de leur choix.

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="L’exemple montre comment ajouter une extension de réunion au cours d’une réunion." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

Lors d’une réunion, les utilisateurs peuvent sélectionner **Plus** :::image type="icon" source="../../assets/icons/teams-client-more.png"::: et choisir l’application de leur choix.

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-add-during-meeting.png" alt-text="L’exemple montre comment ajouter une extension de réunion lors d’une réunion sur mobile." border="false":::

---

## <a name="before-a-meeting"></a>Avant une réunion

Avant une réunion, les utilisateurs peuvent ajouter du contenu dans l’onglet. L’exemple suivant montre un brouillon de question d’enquête à qui les personnes répondront pendant l’appel.

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="L’exemple montre comment apper le contenu des détails de la réunion avant un appel." border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a>Anatomie : onglet Réunion (avant et après les réunions)

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="L’exemple illustre l’anatomie structurelle d’un onglet de réunion avant et après une réunion." border="false":::

|Compteur|Description|
|----------|-----------|
|1|**Nom de l’onglet**: étiquette de navigation pour votre onglet.|
|2|**Dépassement de tabulation**: ouvre les actions d’onglet, telles que renommer et supprimer.|
|3|**iframe**: affiche le contenu de votre application.|

### <a name="designing-with-ui-templates"></a>Conception avec des modèles d’interface utilisateur

Utilisez l’un des modèles d Teams’interface utilisateur suivants pour vous aider à concevoir votre onglet de réunion :

* [Liste](../../concepts/design/design-teams-app-ui-templates.md#list): les listes peuvent afficher les éléments associés dans un format lisible et permettre aux utilisateurs d’agir sur une liste entière ou sur des éléments individuels.
* [Tableau des](../../concepts/design/design-teams-app-ui-templates.md#task-board)tâches : un tableau des tâches, parfois appelé « kanban board » ou « pistes de course » est une collection de cartes souvent utilisées pour suivre l’état des éléments de travail ou des tickets.
* [Tableau de](../../concepts/design/design-teams-app-ui-templates.md#dashboard)bord : un tableau de bord est un canevas contenant plusieurs cartes qui fournissent une vue d’ensemble des données ou du contenu.
* [Formulaire](../../concepts/design/design-teams-app-ui-templates.md#form): les formulaires sont conçus pour collecter, valider et envoyer des entrées utilisateur de manière structurée.
* [État vide](../../concepts/design/design-teams-app-ui-templates.md#empty-state): le modèle d’état vide peut être utilisé pour de nombreux scénarios, y compris la signature, les expériences de première utilisation, les messages d’erreur, etc.
* [Navigation gauche :](../../concepts/design/design-teams-app-advanced-ui-components.md#left-nav)le composant de navigation gauche peut vous aider si votre onglet nécessite une navigation. En règle générale, vous devez conserver la navigation au minimum.

## <a name="use-an-in-meeting-tab"></a>Utiliser un onglet de réunion

L’onglet de réunion est un canevas qui permet d’accroître la collaboration pendant les réunions. Les participants peuvent voir et interagir avec le contenu de l’application dans un espace dédié en dehors de la phase de réunion par le biais d’affichages partagés ou basés sur des rôles.

### <a name="use-cases"></a>Cas d'utilisation

Les personnes peuvent utiliser l’onglet réunion pour :

* Fournissez des commentaires détaillés. Par exemple, évaluez un candidat au poste.
* Créez un sondage, une enquête ou un élément de tâche pour les participants à la réunion.
* Afficher les notes pertinentes pour la réunion. Par exemple, des informations sur un responsable commercial.

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="L’exemple montre comment présenter le contenu d’un sondage dans un onglet de réunion." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-use-in-meeting-tab.png" alt-text="L’exemple montre comment présenter le contenu d’un sondage dans un onglet de réunion sur un appareil mobile." border="false":::

---

### <a name="anatomy-in-meeting-tab"></a>Anatomie : onglet En réunion

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-anatomy.png" alt-text="L’exemple montre l’anatomie structurelle d’un onglet en réunion." border="false":::

|Compteur|Description|
|----------|-----------|
|1|**Icône de l’application (sélectionnée)**: logo d’application transparent de 16 pixels.|
|2|**Nom de l'application**|
|3|**En-tête**: inclut le nom de votre application.|
|4 |**Bouton Fermer :** ferme l’onglet. Utilisez toujours l’icône de fermeture supérieure droite au lieu d’une action dans le pied de plan.|
|5 |**Barre de notification**: les alertes d’erreur s’affichent directement sous l’en-tête et poussent le contenu de l’iFrame vers le bas de 20 pixels.|
|6 |**iframe**: affiche le contenu de votre application.|

### <a name="spacing"></a>Espacement

Optimisez votre onglet de réunion pour qu’il s’adapte de bord à bord dans la zone iFrame de 280 pixels. Il y a 20 pixels de remplissage sur les côtés gauche et droit de l’iframe et entre l’en-tête de l’onglet. L’iframe est pleine page en bas de l’onglet.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="L’exemple montre les dimensions d’espacement des onglets dans la réunion." border="false":::

### <a name="scrolling"></a>Défilement

Le contenu de l’Iframe doit défiler verticalement. Vous pouvez uniquement voir le contenu vers qui vous avez fait défiler (rien au-dessus ou au-dessous). La barre de défilement fait partie du contenu de l’iframe.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="L’exemple montre comment défile l’onglet dans la réunion." border="false":::

### <a name="navigation"></a>Navigation

Pour les scénarios avec des couches de navigation ou un contenu lourd, nous vous recommandons de permettre aux utilisateurs d’accéder à une couche secondaire. Les utilisateurs doivent pouvoir revenir à la couche précédente.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="Exemple de navigation en réunion." border="false":::

## <a name="use-an-in-meeting-dialog"></a>Utiliser une boîte de dialogue de réunion

Les boîtes de dialogue de réunion s’affichent sur la Teams de réunion. Ils nécessitent l’attention, la confirmation ou l’interaction d’un utilisateur, mais sont discrets et n’interrompent pas la réunion. Vous devez les utiliser avec parcimonie et pour les scénarios légers et orientés vers les tâches.

### <a name="use-cases"></a>Cas d'utilisation

Les boîtes de dialogue de réunion sont déclenchées par un utilisateur (tel que l’organisateur de la réunion) qui souhaite peut-être que les participants :

* Fournir de brefs commentaires
* Prendre une courte enquête ou un sondage
* Envoyer des approbations
* Obtenir des rappels

# <a name="desktop"></a>[Desktop](#tab/desktop)

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="L’exemple montre comment utiliser une boîte de dialogue en réunion." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-use-in-meeting-dialog.png" alt-text="L’exemple montre comment utiliser une boîte de dialogue en réunion sur un appareil mobile." border="false":::

---

### <a name="anatomy-in-meeting-dialog"></a>Anatomie : boîte de dialogue en réunion

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-anatomy.png" alt-text="L’exemple illustre l’anatomie structurelle d’une boîte de dialogue en réunion." border="false":::

|Compteur|Description|
|----------|-----------|
|1|**En-tête :** inclut l’icône de l’application, le nom, la chaîne d’action et l’icône fermer.|
|2|**iframe**: affiche le contenu de votre application.|

### <a name="anatomy-in-meeting-dialog-header"></a>Anatomie : en-tête de boîte de dialogue en réunion

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="L’exemple illustre l’anatomie structurelle d’un en-tête de boîte de dialogue en réunion." border="false":::

Il existe deux variantes d’en-tête. Dans la mesure du possible, utilisez la variante avec l’avatar pour renforcer le fait que la boîte de dialogue vient d’une personne.

|Compteur|Description|
|----------|-----------|
|1|**Avatar**: personne qui lance la boîte de dialogue en réunion.|
|2|**Icône de l’application**|
|3|**Nom de l'application**|
|4 |**Bouton Fermer :** ferme la boîte de dialogue.|
|5 |**Chaîne d’action**: décrit généralement l’auteur de la boîte de dialogue.|

### <a name="responsive-behavior"></a>Comportement réactif

Les boîtes de dialogue de réunion peuvent varier en taille pour tenir compte de différents scénarios. Veillez à maintenir la taille des remplissages et des composants.

* **Largeur**: vous pouvez spécifier la largeur de l’iframe de la boîte de dialogue n’importe où dans la plage de tailles prise en charge.
* **Hauteur**: vous pouvez spécifier la hauteur de l’iframe de la boîte de dialogue n’importe où dans la plage de tailles prise en charge. Vous pouvez également autoriser les utilisateurs à faire défiler verticalement si le contenu de votre application dépasse la hauteur maximale.

Pour implémenter, spécifiez la largeur et la hauteur à l’aide de la [`externalResourceUrl`](~/apps-in-teams-meetings/create-apps-for-teams-meetings.md#notificationsignal-api) clé.

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="Exemple de boîte de dialogue en réunion. Largeur : Min--280 pixels (248 pixels iframe). Max--460 pixels (428 pixels iframe). Hauteur : 300 pixels (iframe)." border="false":::

## <a name="after-a-meeting"></a>Après une réunion

Vous pouvez revenir à une réunion une fois qu’elle s’est terminée et afficher le contenu de l’application. Dans cet exemple, l’organisateur de la réunion peut examiner les résultats des sondages dans l’onglet **Contoso.** (Remarque : du point de vue de la conception, il n’y a aucune différence entre l’expérience d’onglet avant et après la réunion.)

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

Une seule boîte de dialogue de réunion avec plusieurs interactions peut distrayer l’appel.

   :::column-end:::
:::row-end:::

### <a name="layout"></a>Disposition

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="Exemple montrant comment utiliser une mise en page de boîte de dialogue à une seule colonne." border="false":::

#### <a name="do-use-a-single-column-dialog-layout"></a>À faire : utiliser une disposition de boîte de dialogue à une seule colonne

Étant donné que les boîtes de dialogue sont au centre de la phase de réunion, l’achèvement des tâches doit être rapide et simple pour éviter toute frustration de l’utilisateur.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-dont.png" alt-text="Exemple montrant que vous ne devez pas encombrer l’espace d’une extension de réunion." border="false":::

#### <a name="dont-clutter-the-space"></a>À ne pas faire : encombrer l’espace

Le contenu épais ou trop structuré peut être gênant et gênant, en particulier au cours d’une réunion.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-do.png" alt-text="Exemple montrant une disposition d’onglet à une seule colonne." border="false":::

#### <a name="do-use-a-single-column-tab-layout"></a>À faire : utiliser une disposition d’onglet à une seule colonne

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

### <a name="scroll"></a>Faire défiler

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="Exemple de défilement vertical dans un onglet de réunion." border="false":::

#### <a name="do-scroll-vertically"></a>À faire : faire défiler verticalement

Les utilisateurs s’attendent à ce que le défilement vertical Teams (et ailleurs).

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="Exemple de défilement horizontal dans un onglet de réunion." border="false":::

#### <a name="dont-scroll-horizontally"></a>À ne pas faire : faire défiler horizontalement

Le défilement horizontal n’est pas un comportement attendu dans Teams. Les autres canevas de l’environnement de réunion défilent verticalement.

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
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-workflow-dont.png" alt-text="Exemple de scénarios complexes dans une boîte de dialogue de réunion." border="false":::

#### <a name="dont-make-in-meeting-dialogs-complex"></a>À ne pas faire : rendre les boîtes de dialogue de réunion complexes

Les boîtes de dialogue en réunion sont conçues pour de brèves interactions.

   :::column-end:::
:::row-end:::

### <a name="theming"></a>Thèmes

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="Exemple montrant une extension de réunion avec le thème foncé." border="false":::

#### <a name="do-use-teams-color-tokens"></a>À faire : utiliser Teams de couleur

Teams réunions sont optimisées pour le mode sombre afin de réduire les bruits visuels et cognitifs afin que les utilisateurs se concentrent sur la discussion et le contenu partagé. En savoir plus sur <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">l’utilisation des jetons de couleur (interface utilisateur Fluent).</a>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="Exemple montrant une extension de réunion avec un thème par défaut (clair)." border="false":::

#### <a name="dont-hard-code-hex-values"></a>À ne pas faire : valeurs hexades de code dur

Si vous n’utilisez pas Teams couleur, vos conceptions seront moins évolutives et prenons plus de temps à gérer.

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

La fourniture d’une option permettant de fermer le contenu de l’onglet de réunion peut entraîner des problèmes, car l’en-tête est déjà sur un bouton pour faire disparaître l’onglet de la réunion lui-même.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-caution.png" alt-text="Exemple montrant des modales (ou des modules de tâche) dans un onglet de réunion." border="false":::

#### <a name="caution-avoid-modals-within-the-in-meeting-tab"></a>Attention : évitez les modales dans l’onglet de la réunion

Les modales (également appelées modules de tâche) dans l’onglet déjà étroit de la réunion peuvent encapsuler et masquer le contenu.

   :::column-end:::
:::row-end:::
