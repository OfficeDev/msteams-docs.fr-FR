---
title: Instructions de conception pour les onglets
description: Décrit les instructions pour la création d’onglets pour le contenu et la collaboration
keywords: instructions de conception teams-onglets de l’infrastructure de référence
ms.openlocfilehash: 2d4e809e3ac11a5742113bf65125848a922c0207
ms.sourcegitcommit: 50571f5c6afc86177c4fe1032fe13366a7b706dd
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/04/2020
ms.locfileid: "49576861"
---
# <a name="content-and-conversations-all-at-once-using-tabs"></a>Contenu et conversations, tous à la fois à l’aide d’onglets

> [!Important]
> **Onglets sur les clients mobiles**
>
> Suivez les [instructions pour les onglets sur mobile](./tabs-mobile.md) lors de la création de vos onglets. Si votre onglet utilise l’authentification, vous devez mettre à niveau votre SDK teams JavaScript vers la version 1.4.1 ou une version ultérieure, sinon l’authentification échouera.
>
> **Onglets canal/groupe (configurable) sur mobile :**
>
> * Les clients mobiles affichent uniquement les onglets configurables dont la valeur est `websiteUrl` . Si vous souhaitez que votre onglet apparaisse sur les clients mobiles Teams, vous devez définir la valeur de `websiteUrl` .
> * Le comportement d’ouverture par défaut sur mobile consiste à ouvrir l’extérieur dans le navigateur à l’aide du `websiteUrl` . Pour les applications publiées dans le magasin d’applications public, si vous voulez que les onglets de votre canal s’ouvrent dans teams par défaut, suivez les [instructions pour les onglets sur les appareils mobiles](~/tabs/design/tabs-mobile.md)et contactez votre représentant du support technique pour demander à être inclus dans la liste d’autorisation.

Les onglets sont des canevas que vous pouvez utiliser pour partager du contenu, organiser des conversations et héberger des services tiers dans le flux de travail Organic d’une équipe. Lorsque vous créez un onglet dans Microsoft Teams, il place le centre et le centre de votre application Web où il est facilement accessible à partir des conversations clés.

## <a name="guidelines"></a>Conseils

Un onglet approprié doit présenter les caractéristiques suivantes :

### <a name="focused-functionality"></a>Fonctionnalités ciblées

Les onglets fonctionnent mieux lorsqu’ils sont conçus pour répondre à un besoin spécifique. Concentrez-vous sur un petit ensemble de tâches ou sur un sous-ensemble de données correspondant au canal dans lequel se trouve l’onglet.

### <a name="reduced-chrome"></a>Chrome réduit

Évitez de créer plusieurs panneaux au sein d’un même onglet, d’y ajouter des couches de navigation ou d’obliger les utilisateurs à faire défiler son contenu verticalement et horizontalement. En d’autres termes, essayez de ne pas avoir d’onglets dans votre onglet.

### <a name="integration"></a>Intégration

Découvrez comment informer les utilisateurs de l’activité des onglets en publiant des [cartes adaptatives](../../task-modules-and-cards/what-are-cards.md#adaptive-cards) sur une conversation.

### <a name="conversational"></a>Conversationnel

Trouver un moyen de faciliter la conversation sur un onglet. Cela garantit que le Centre des conversations est sur le contenu, les données ou le processus à portée de main.

### <a name="streamlined-access"></a>Accès simplifié

Assurez-vous que vous accordez l’accès aux bonnes personnes au bon moment. Le simple maintien de votre processus de connexion évite de créer des obstacles à la collaboration et à la collaboration.

### <a name="responsiveness-to-window-sizing"></a>Réactivité au dimensionnement de la fenêtre

Les équipes peuvent être utilisées dans des tailles de fenêtre aussi petites que 720px, de sorte que l’utilisation d’un onglet dans une petite fenêtre est aussi importante que celle des résolutions très élevées.

### <a name="flat-navigation"></a>Navigation plate

Nous demandons aux développeurs de ne pas ajouter leur portail entier à un onglet. Le maintien de la navigation relativement plat permet de conserver un modèle de conversation plus simple. En d’autres termes, la conversation concerne une liste d’éléments, tels que les éléments de travail triage, ou une seule chose, comme une spécification.

Il existe des défis de navigation inhérents à la hiérarchie de navigation profonde, dans les conversations thématiques. Pour une expérience utilisateur optimale, votre navigation par onglet doit être réduite à un minimum et être conçue comme suit :

> [!div class="checklist"]
>
> * **Ouvre un module de tâche, tel qu’un élément de travail ou une entité spécifique**. Cela exclut la conversation et est la meilleure option pour conserver la conversation en particulier sur l’onglet et non sur les sous-entités ou les expériences de modification.
>* **Ouvre une Pseudo boîte de dialogue dans un IFRAME**. Si elle est utilisée avec un arrière-plan filtré, nous vous recommandons d’utiliser la couleur la plus claire plutôt que l’obscurité. La `app-gray-10 at 30%` transparence fonctionne bien.
>* **Ouvre une page de navigateur**.

### <a name="personality"></a>Caractéristique

Votre zone de dessin de tabulation constitue une excellente occasion de personnaliser votre expérience. Votre logo est une partie importante de votre identité et de votre connexion avec vos utilisateurs., assurez-vous de l’inclure :

> [!div class="checklist"]
>
>* Placer votre logo dans le coin gauche ou droit ou le long du bord inférieur
> * Garder votre logo petit et discret

L’incorporation de vos propres couleurs et dispositions twill facilite également la communication de la personnalité.

> [!TIP]
> Utilisez notre style visuel pour que votre service ressemble à une partie de teams. *Voir*, par exemple, les [couleurs de teams](../../concepts/design/components/color.md)

---

## <a name="tab-layouts"></a>Mises en page d’onglets

[!INCLUDE [Tab layouts](../../includes/design/tab-layouts.html)]

---

## <a name="types-of-tabs"></a>Types d’onglets

[!INCLUDE [Tab types](../../includes/design/tab-types.html)]

---

## <a name="configuration-page-height"></a>Hauteur de la page de configuration

>[!IMPORTANT]
>En septembre 2018, la hauteur de la [page de configuration](~/tabs/how-to/create-tab-pages/configuration-page.md) des onglets a été augmentée, tandis que la largeur est restée inchangée. Si votre application est conçue pour une taille plus ancienne, votre page de configuration d’onglet aura une grande quantité d’espacement vertical. Les applications de magasin héritées exemptées de cette modification devront contacter Microsoft après la mise à jour pour prendre en compte les nouvelles dimensions.

Les dimensions de la page de configuration de l’onglet :


<img width="450px" title="Tailles des onglets de configuration" src="~/assets/images/tabs/config-dialog-Contoso2.png" alt="sizes for config tabs" />


### <a name="guidelines-for-tab-configuration-page-format"></a>Instructions pour le format de page de configuration d’onglet

* Basez la hauteur minimale de votre zone de contenu sur la page de configuration de votre onglet sur les éléments graphiques de hauteur fixe.
* Calculer l’espacement vertical disponible (hauteur de la zone de contenu dans la page de configuration) à l’aide de `window.innerHeight` . Cette valeur renvoie la taille du `<iframe>` dans lequel votre page de configuration se trouve, ce qui peut changer dans les versions ultérieures. À l’aide de cette valeur, votre contenu s’ajuste automatiquement aux modifications ultérieures.
* Allouer de l’espace vertical aux éléments de hauteur variable moins ce qui est nécessaire pour les éléments de hauteur fixe.
* Pour l’état de *connexion* , centrez verticalement et horizontalement le contenu.
* Si vous souhaitez une image d’arrière-plan, vous avez besoin d’une nouvelle image ajustée pour s’adapter à la zone (par défaut) ou vous pouvez conserver la même image et choisir entre :
  * alignement sur le coin supérieur gauche.
  * mise à l’échelle de l’image pour l’ajuster.

Lorsque la taille est correcte, votre page de configuration d’onglet doit ressembler à ceci :

<img width="450px" title="Onglet nouvelle configuration" src="~/assets/images/tabs/config-dialog-Contoso.png" alt="new config tab"/>

## <a name="best-practices"></a>Meilleures pratiques

### <a name="always-include-a-default-state"></a>Toujours inclure un État par défaut

Incluez un État par défaut pour faciliter la configuration des onglets, même si votre onglet est configurable.

### <a name="deep-linking"></a>Liaison profonde

Chaque fois que possible, les cartes et les robots doivent créer des liens approfondis vers des données plus riches dans un onglet hébergé. Par exemple, une carte peut afficher un résumé des données de bogue, mais vous pouvez cliquer dessus pour afficher l’intégralité du bogue dans un onglet.

### <a name="naming"></a>Donnant

Dans de nombreux cas, le nom de votre application fera un excellent nom d’onglet. Toutefois, vous pouvez également nommer vos onglets en fonction de la fonctionnalité qu’ils fournissent.

### <a name="multi-window"></a>Multi-fenêtre

Les onglets de canal dotés de fonctionnalités d’édition complexes doivent ouvrir le mode éditeur dans plusieurs fenêtres plutôt qu’un onglet.

### <a name="no-horizontal-scrolling"></a>Pas de défilement horizontal

La tabulation ne doit pas avoir de défilement horizontal.

### <a name="easy-navigation"></a>Navigation facile

La navigation à l’intérieur d’une application d’onglets doit être facile à suivre, c’est-à-dire, lorsque cela est nécessaire/applicable, les pages suivantes :
* Boutons précédent
* En-têtes de page
* Barres
* Menus de hamburger

### <a name="undo-last-action"></a>Annuler la dernière action

L’utilisateur doit pouvoir annuler sa dernière action dans l’application.

### <a name="share-content"></a>Partager du contenu

Les applications personnelles doivent permettre aux utilisateurs de partager du contenu d’une expérience d’application personnelle avec d’autres membres de l’équipe. L’onglet canal doit fournir une navigation qui complète la navigation principale dans Teams, au lieu d’entrer en conflit avec elle (par exemple, les barres de navigation du rail gauche).

### <a name="single-view"></a>Vue unique

Les applications personnelles doivent présenter du contenu provenant d’instances ou d’instances d’étendue de conversation de groupe de cette application dans une seule vue, par exemple, un utilisateur Trello doit être en mesure d’afficher toutes les instances des cartes Trello auxquelles elles participent au niveau de l’équipe dans leur application personnelle.

### <a name="no-app-bar"></a>Aucune barre d’application

Les onglets ne doivent pas fournir de barre d’application avec des icônes dans le rail gauche qui entrent en conflit avec la navigation principale de teams.

### <a name="navigation"></a>Navigation

Les onglets ne doivent pas comporter plus de 3 niveaux de navigation au sein de l’application.

### <a name="l2l3-view"></a>Vue L2/L3

Les pages secondaires et tertiaires d’un onglet doivent être ouvertes dans une vue L2/L3 dans la zone d’onglet principale qui est parcourue via le plan de navigation.

### <a name="no-link-to-external-browser"></a>Aucun lien vers le navigateur externe

Les cibles de liens dans les onglets ne doivent pas être liées à un navigateur externe, mais doivent être liées à des éléments div contenus dans Teams. Par exemple, à l’intérieur des modules de tâches, des onglets, etc.

## <a name="notifications-for-tabs"></a>Notifications pour les onglets

Il existe deux modes de notification pour les modifications apportées au contenu des onglets :

> [!div class="checklist"]
>
> * **Utiliser l’API de l’application pour avertir les utilisateurs des modifications**. Ce message s’affichera dans le flux d’activités de l’utilisateur et le lien profond vers l’onglet. *voir*  [créer des liens détaillés vers du contenu et des fonctionnalités dans Microsoft teams](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true )

> * **Utiliser un bot**. Cette méthode est préférée en particulier si le thread de tabulation est ciblé. Le résultat est que la conversation de thème de l’onglet est déplacée vers le mode récemment actif. Cette méthode permet également une sophistication du mode d’envoi de la notification.

L’envoi d’un message à un fil d’onglet augmente la sensibilisation de l’activité à tous les utilisateurs sans en informer explicitement tout le monde. Il s’agit d’une sensibilisation sans bruit. En outre, lorsque vous avez `@mention`  des utilisateurs spécifiques, la même notification est placée dans le flux, en les liant directement au fil d’onglets.

### <a name="tab-design-best-practices"></a>Meilleures pratiques pour la création d’onglets

* Les onglets personnel/statique doivent permettre aux utilisateurs de partager le contenu d’une expérience d’application personnelle avec d’autres membres de l’équipe.
* Les onglets personnels/statiques peuvent présenter du contenu provenant d’instances ou d’instances d’étendues de conversation de groupe de cette application dans une seule vue.
* Les cibles de liens dans les onglets ne doivent pas être liées à un navigateur externe, mais doivent être liées à des éléments div contenus dans Teams (par exemple, à l’intérieur, des modules de tâches, des onglets, etc.).
* Les onglets doivent répondre aux thèmes de l’équipe. Lorsque le thème teams est modifié, le thème au sein de l’application doit également être modifié pour refléter ce thème.
* Les onglets doivent utiliser des composants de style teams dans la mesure du possible. Cela signifie adopter des polices Teams, des rampes, des palettes de couleurs, un système de grille, un mouvement, un ton de voix, etc.
* Les onglets doivent utiliser les comportements d’interaction de teams pour la navigation dans la page, la position et l’utilisation des boîtes de dialogue, des hiérarchies d’informations, etc.
* Les onglets doivent utiliser le menu hamburger teams standard et/ou la barre de navigation pour la navigation dans l’application. Les onglets ne doivent pas fournir de barre d’application avec des icônes dans le rail gauche qui entrent en conflit avec la navigation principale de teams.
* Les onglets ne doivent pas avoir plus de trois niveaux de navigation dans l’application.
* Les pages secondaires et tertiaires d’un onglet doivent être ouvertes dans une vue L2/L3 dans la zone d’onglet principale qui est parcourue via le plan de navigation.
* Les onglets disposant de fonctionnalités d’édition complexes dans l’application doivent ouvrir le mode éditeur dans plusieurs fenêtres plutôt qu’un onglet (pour le bureau et le Web).
* Pour une expérience utilisateur améliorée, citons un bot personnel qui envoie un message de bienvenue à l’utilisateur lors de la première exécution et répond aux commandes **Hi**, **Help** et **Hello** . Vous pouvez vous reporter à la documentation sur les [bots conversation](../../bots/what-are-bots.md#in-a-one-to-one-chat) pour obtenir de l’aide.
