---
title: Instructions de conception pour les onglets
description: Décrit les instructions pour la création d’onglets pour le contenu et la collaboration
keywords: instructions de conception de l’infrastructure de référence
ms.openlocfilehash: 342e01e348c74eb143391a7d238396a2d866766a
ms.sourcegitcommit: 61edf47c9dd1dbc1df03d0d9fb83bfedca4c423b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2020
ms.locfileid: "43914552"
---
# <a name="content-and-conversations-all-at-once-using-tabs"></a>Contenu et conversations, tous à la fois à l’aide d’onglets

> [!Important]
> **Onglets sur les clients mobiles**
>
> Suivez les [instructions pour les onglets sur mobile](./tabs-mobile.md) lors de la création de vos onglets. Si votre onglet utilise l’authentification, vous devez mettre à niveau votre SDK teams JavaScript vers la version 1.4.1 ou une version ultérieure, sinon l’authentification échouera.
>
> **Onglets personnels (statiques) sur mobile :**
>
> * Les onglets statiques (application personnelle) sont disponibles dans l’Aperçu pour les [développeurs](~/resources/dev-preview/developer-preview-intro.md).
> * Lors de la création de vos onglets statiques, assurez-vous de suivre les [instructions pour les onglets sur les appareils mobiles](~/tabs/design/tabs-mobile.md)
>
> **Onglets canal/groupe (configurable) sur mobile :**
>
> * Les clients mobiles affichent uniquement les onglets dont `websiteUrl`la valeur est. Si vous souhaitez que votre onglet apparaisse sur les clients mobiles Teams, vous devez définir la `websiteUrl`valeur de.
> * Le comportement d’ouverture par défaut sur mobile consiste à ouvrir l’extérieur `websiteUrl`dans le navigateur à l’aide du. Pour les applications publiées dans le magasin d’applications public, si vous voulez que les onglets de votre canal s’ouvrent dans teams par défaut, suivez les [instructions pour les onglets sur les appareils mobiles](~/tabs/design/tabs-mobile.md)et contactez votre représentant du support technique pour demander à être inclus dans la liste d’autorisation.

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

Nous demandons aux développeurs de ne pas ajouter l’intégralité de leur portail à un onglet. le maintien de la navigation relativement plat contribue à maintenir un modèle de conversation plus simple. En d’autres termes, la conversation concerne une liste d’éléments, tels que les éléments de travail triage, ou une seule chose, comme une spécification.

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
> Utilisez notre style visuel pour que votre service ressemble à une partie de teams. *Voir*, par exemple, [couleurs teams] (/concepts/design/Components/Typography.MD

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

<img width="450px" title="Tailles des onglets de configuration" src="~/assets/images/tabs/config-dialog-Contoso2.png" />

### <a name="guidelines-for-tab-configuration-page-format"></a>Instructions pour le format de page de configuration d’onglet

* Basez la hauteur minimale de votre zone de contenu sur la page de configuration de votre onglet sur les éléments graphiques de hauteur fixe.
* Calculer l’espacement vertical disponible (hauteur de la zone de contenu dans la page de `window.innerHeight`Configuration) à l’aide de. Cette valeur renvoie la taille du `<iframe>` dans lequel votre page de configuration se trouve, ce qui peut changer dans les versions ultérieures. À l’aide de cette valeur, votre contenu s’ajuste automatiquement aux modifications ultérieures.
* Allouer de l’espace vertical aux éléments de hauteur variable moins ce qui est nécessaire pour les éléments de hauteur fixe.
* Pour l’état de *connexion* , centrez verticalement et horizontalement le contenu.
* Si vous souhaitez une image d’arrière-plan, vous avez besoin d’une nouvelle image ajustée pour s’adapter à la zone (par défaut) ou vous pouvez conserver la même image et choisir entre :
  * alignement sur le coin supérieur gauche.
  * mise à l’échelle de l’image pour l’ajuster.

Lorsque la taille est correcte, votre page de configuration d’onglet doit ressembler à ceci :

<img width="450px" title="Onglet nouvelle configuration" src="~/assets/images/tabs/config-dialog-Contoso.png" />

## <a name="best-practices"></a>Meilleures pratiques

### <a name="always-include-a-default-state"></a>Toujours inclure un État par défaut

Incluez un État par défaut pour faciliter la configuration des onglets, même si votre onglet est configurable.

### <a name="deep-linking"></a>Liaison profonde

Chaque fois que possible, les cartes et les robots doivent créer des liens approfondis vers des données plus riches dans un onglet hébergé. Par exemple, une carte peut afficher un résumé des données de bogue, mais vous pouvez cliquer dessus pour afficher l’intégralité du bogue dans un onglet.

### <a name="naming"></a>Donnant

Dans de nombreux cas, le nom de votre application fera un excellent nom d’onglet. Toutefois, vous pouvez également nommer vos onglets en fonction de la fonctionnalité qu’ils fournissent.

## <a name="notifications-for-tabs"></a>Notifications pour les onglets

Il existe deux modes de notification pour les modifications apportées au contenu des onglets :

> [!div class="checklist"]
>
> * **Utiliser l’API de l’application pour avertir les utilisateurs des modifications**. Ce message s’affichera dans le flux d’activités de l’utilisateur et le lien profond vers l’onglet. *voir*  [créer des liens détaillés vers du contenu et des fonctionnalités dans Microsoft teams](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest)
> * **Utiliser un bot**. Cette méthode est préférée en particulier si le thread de tabulation est ciblé. Le résultat est que la conversation de thème de l’onglet est déplacée vers le mode récemment actif. Cette méthode permet également une sophistication du mode d’envoi de la notification.

  L’envoi d’un message à un fil d’onglet augmente la sensibilisation de l’activité à tous les utilisateurs sans en informer explicitement tout le monde. Il s’agit d’une sensibilisation sans bruit. En outre, lorsque vous `@mention` avez des utilisateurs spécifiques, la même notification est placée dans le flux, en les liant directement au fil d’onglets.
