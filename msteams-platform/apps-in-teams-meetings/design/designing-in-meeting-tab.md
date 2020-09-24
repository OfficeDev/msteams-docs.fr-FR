---
title: Créer un onglet de réunion dans Microsoft teams
author: heath-hamilton
description: Conseils et meilleures pratiques pour la conception de l’onglet dans la réunion pour Microsoft Teams.
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: 4f75591468de41b5d4d3ac62a25b93412b3fccaa
ms.sourcegitcommit: f9a2f5cedc9d30ef7a9cf78a47d01cfd277e150d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2020
ms.locfileid: "48243330"
---
# <a name="design-an-in-meeting-tab"></a>Concevoir un onglet en réunion

L’onglet dans la réunion est un canevas permettant d’augmenter la collaboration pendant les réunions. En fonction de l’onglet Teams, les participants peuvent voir et interagir avec le contenu de l’application dans un espace dédié en dehors de la phase de la réunion via des affichages partagés ou basés sur des rôles.

## <a name="use-cases"></a>Cas d’utilisation

Les utilisateurs peuvent utiliser l’onglet dans la réunion pour :

* Fournir des commentaires détaillés (par exemple, évaluer un candidat de travail)
* Créer rapidement un élément de sondage, d’enquête ou de tâche pour les participants à la réunion
* Afficher les notes relatives à la réunion (par exemple, informations sur un prospect)

## <a name="example"></a>Exemple

L’exemple suivant montre l’onglet dans la réunion qui affiche le contenu de l’application d’enquête.

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-organizer-view.png" alt-text="Exemple montre à quoi peut ressembler l’onglet réunion sous la forme d’un organisateur de réunion.":::

<a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Voir le scénario complet (Figma)</a>

<a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Voir d’autres exemples d’utilisation (Figma)</a>

## <a name="anatomy"></a>Anatomie

L’onglet dans la réunion affiche le contenu de votre application à l’aide des dimensions suivantes :

* **Largeur**: 280 pixels pour la zone WebView. Il y a 20 pixels de remplissage sur les côtés gauche et droit de l’affichage WebView.
* **Hauteur**: fond perdu en bas de l’onglet. Il y a 20 pixels de remplissage entre la zone d’affichage WebView et l’en-tête d’onglet.

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-anatomy.png" alt-text="Illustration illustrant l’anatomie de l’interface utilisateur d’une extension de réunion sous-onglet réunion." border="false":::

1. **Icône**de l’application : point d’entrée de l’onglet dans la réunion.
1. **En-tête**: inclut le nom de l’onglet.
1. **Name**: nom de l’instance d’onglet.
1. **Faire disparaître : ferme**l’onglet. Toujours utiliser l’icône fermer en haut à droite au lieu d’une action dans le pied de page.
1. **WebView**: affiche le contenu de l’application tierce.

## <a name="behavior"></a>Comportement

### <a name="scale"></a>Échelle

Actuellement, la largeur de l’onglet dans la réunion est fixe.

### <a name="scrolling"></a>Défilement

Voici ce que vous devez savoir sur le défilement dans l’onglet dans la réunion :

* Vous devez uniquement pouvoir faire défiler verticalement.
* Vous ne pouvez voir que le contenu auquel vous avez fait défiler (rien au-dessus ou en dessous).
* La barre de défilement fait partie du contenu WebView.

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-scroll.png" alt-text="Illustration illustrant le mode de défilement du contenu WebView de l’onglet intégré à la réunion." border="false":::

### <a name="navigation"></a>Navigation

Pour les scénarios avec des calques de navigation ou du contenu lourd, il est recommandé d’autoriser les utilisateurs à accéder à un calque secondaire. Les utilisateurs doivent pouvoir revenir à la couche précédente.

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-nav.png" alt-text="Illustration illustrant le fonctionnement de la navigation vers un calque secondaire dans l’onglet de réunion." border="false":::

## <a name="components"></a>Composants

Les onglets de réunion sont créés principalement avec les <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">composants d’interface utilisateur suivants (Figma)</a>, qui sont basés sur le <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">système de conception Fluent</a>.

Composant | Conseils | Exemple
 - | - | -
Bouton | Les boutons principal et secondaire peuvent être de taille moyenne ou petite | Envoyer une réponse
Input | Champ pour une saisie utilisateur partielle. Le texte de l’étiquette peut inclure une icône  | Entrer des commentaires
Liste déroulante | Sélectionnez une ou plusieurs options dans une liste. Peut inclure des fonctionnalités de recherche et de sélection multiple | Choisir une langue
Contrôles de sélection | Utilisez des cases à cocher pour plusieurs choix ou cases d’option et pour basculer pour les choix uniques. Pour des sélections plus détaillées, utilisez un curseur | Vote dans un sondage
Alertes | Qu’il s’agisse d’un message urgent, d’un état d’erreur ou d’un avertissement, le message doit être court et n’interrompra pas la tâche actuelle de l’utilisateur. | Afficher un problème lors de l’envoi d’une réponse

## <a name="theming"></a>Thèmes

### <a name="colors"></a>Couleurs

Utilisez le <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">jeu de couleurs recommandé (Figma)</a> pour les arrière-plans, les avant-plans et les États de transport.

### <a name="typography"></a>Typographie

Utilisez les <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">tailles et épaisseurs de police recommandées (Figma)</a> pour les titres, le corps de texte et le texte de métadonnées.

## <a name="best-practices"></a>Meilleures pratiques

### <a name="responsiveness"></a>Réactivité

Les mises en page d’onglets de réunion doivent pouvoir être redimensionnées en différentes tailles. Réfléchissez à la façon dont l’onglet mettra en forme et prendra en compte avant, pendant et après la réunion.

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-before-meeting.png" alt-text="Illustration montrant que le contenu de l’onglet dans la réunion ressemble à un onglet plein écran avant et après une réunion." border="false":::

#### <a name="before-the-meeting"></a>Avant la réunion

Assurez-vous que la disposition des tabulations peut s’adapter à la disposition droite ou gauche de différentes langues et que les contrôles se déplacent vers les emplacements appropriés. (Les mises en page pré-réunion peuvent également s’appliquer aux mises en page post-réunion.)

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-during-meeting.png" alt-text="Illustration illustrant la façon dont le contenu de l’onglet pre-Meeting est condensé dans l’onglet de réunion lors d’une réunion." border="false":::

#### <a name="during-the-meeting"></a>Lors de la réunion

Le contenu de la tabulation s’ajuste à la mise en page et à l’emplacement des onglets de réunion.

   :::column-end:::
:::row-end:::

### <a name="theming"></a>Thèmes

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-theming-do.png" alt-text="Illustration illustrant la conception de l’onglet pour le thème sombre utilisé dans les réunions Teams." border="false":::

#### <a name="do-design-for-a-dark-theme"></a>Do : Design pour un thème sombre

Les réunions de teams sont optimisées pour le mode sombre afin de réduire le bruit visuel et cognitif afin que les utilisateurs puissent se concentrer sur la discussion et le contenu partagé.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-theming-dont.png" alt-text="Illustration montrant que vous ne devez pas utiliser des couleurs qui ne sont pas favorables au thème sombre de teams." border="false":::

#### <a name="dont-use-unfamiliar-colors"></a>Ne pas utiliser de couleurs inhabituelles

Les couleurs qui sont en conflit avec l’environnement de la réunion peuvent être gênantes et sembler moins natives à Teams.

   :::column-end:::
:::row-end:::

### <a name="scrolling"></a>Défilement

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-scroll-do.png" alt-text="Illustration montrant que vous devez autoriser le défilement vertical uniquement dans l’onglet dans la réunion." border="false":::

#### <a name="do-scroll-vertically"></a>Do : faites défiler verticalement

Les utilisateurs anticipent le défilement vertical dans Teams (et ailleurs).

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-scroll-dont.png" alt-text="Illustration montrant que vous ne devez pas autoriser le défilement horizontal dans l’onglet de la réunion." border="false":::

#### <a name="dont-scroll-horizontally"></a>Ne pas faire défiler horizontalement

Le défilement horizontal n’est pas un comportement attendu dans Teams. Les autres canevas dans l’environnement de réunion sont déroulants verticalement.

   :::column-end:::
:::row-end:::

### <a name="layout"></a>Disposition

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-layout-do.png" alt-text="Illustration illustrant la disposition sur une seule colonne recommandée dans l’onglet dans la réunion." border="false":::

#### <a name="do-single-columns"></a>Do : colonnes uniques

Étant donné la nature étroite de l’onglet dans la réunion, nous vous recommandons vivement d’afficher le contenu dans une seule colonne.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-layout-dont.png" alt-text="Illustration illustrant la façon dont une disposition sur deux colonnes dans l’onglet de réunion n’est pas idéale." border="false":::

#### <a name="dont-multiple-columns"></a>Ne pas : plusieurs colonnes

En raison de l’espace limité de l’onglet dans la réunion, les mises en page comportant plusieurs colonnes ne sont pas recommandées.

   :::column-end:::
:::row-end:::

### <a name="navigation"></a>Navigation

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-nav-do.png" alt-text="Illustration montrant que vous devez toujours fournir un bouton précédent si votre application d’onglet de réunion dispose de plusieurs couches de navigation." border="false":::

#### <a name="do-have-a-back-button"></a>Do : avoir un bouton retour

Si vous disposez de plusieurs couches de navigation, les utilisateurs doivent pouvoir revenir à leur vue précédente.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-nav-dont.png" alt-text="Une illustration montrant que l’ajout d’un autre bouton Fermer dans l’onglet de réunion pour la navigation est redondante et peut entraîner des problèmes." border="false":::

#### <a name="dont-include-another-close-button"></a>Ne pas inclure d’autre bouton Fermer

Une option permettant de fermer le contenu de l’onglet de la réunion peut entraîner des problèmes, car il existe déjà un bouton Fermer dans l’en-tête pour faire disparaître l’onglet de réunion lui-même.

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-nav-caution.png" alt-text="Illustration montrant que vous devez être prudent lorsque vous utilisez des modaux (par exemple, des modules de tâches) dans l’onglet de la réunion en fonction de l’espace limité." border="false":::

#### <a name="caution-using-dialogs-in-a-narrow-space"></a>ATTENTION : utilisation de boîtes de dialogue dans un espace étroit

Les boîtes de dialogue, telles que les modules de tâches, dans l’onglet de la réunion déjà étroite peuvent encapsuler et obscurcir le contenu.

   :::column-end:::
:::row-end:::

## <a name="accessibility"></a>Accessibilité

Pour plus d’informations sur l’accessibilité, voir <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Figma</a>.

## <a name="resources"></a>Ressources

* <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Fichiers Figma des extensions de réunion Microsoft teams</a>
* [Instructions de conception d’onglets](../../tabs/design/tabs.md)
* [Instructions de conception d’onglets pour mobile](../../tabs/design/tabs-mobile.md)

## <a name="validate-your-design"></a>Valider votre conception

Si vous envisagez de publier votre application dans AppSource, vous devez comprendre les problèmes de conception qui entraînent généralement l’échec des applications lors de l’envoi.

> [!div class="nextstepaction"]
> [Vérifier les instructions de validation de la conception](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines)
