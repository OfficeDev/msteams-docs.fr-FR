---
title: Référence des instructions de conception
description: Décrit les instructions pour la conception d’une application personnelle
keywords: instructions de conception teams structure de référence des applications personnelles
ms.openlocfilehash: f66691234149afa56a6753dd51379c9f2355318e
ms.sourcegitcommit: 61c93b22490526b1de87c0b14a3c7eb6e046caf6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/31/2020
ms.locfileid: "44455498"
---
# <a name="personal-apps"></a>Applications personnelles

> [!NOTE]
> La prise en charge complète des onglets sur les clients mobiles est prise en charge dans Teams. Vous devez suivre les [instructions pour les onglets sur mobile](../../tabs/design/tabs-mobile.md) lors de la création d’onglets pour les plateformes mobiles.

Une application personnelle est une application de teams avec une portée personnelle.  En tant que développeur d’applications, vous avez la possibilité de fournir une version de votre application qui se concentre sur les interactions avec un seul utilisateur. Il peut s’agir d’un [bot de conversation](../../bots/what-are-bots.md) pour engager des conversations un-à-un avec un utilisateur ou un [onglet personnel](../../tabs/what-are-tabs.md) qui fournit une expérience Web intégrée. Les applications personnelles permettent aux utilisateurs d’afficher leur contenu sélectionné à un seul endroit. Dans la capture d’écran suivante, contoso est une application personnelle dans le lanceur d’applications personnelles.

![image du menu de dépassement de l’application](~/assets/images/Personal-apps-App-flyout.png)

---

## <a name="guidelines"></a>Conseils

Une application personnelle contient généralement les onglets suivants :

### <a name="your-tab"></a>Votre onglet

C’est ici que vos utilisateurs verront toutes leurs choses. Il s’agit de son espace personnel. L’onglet peut être organisé sous la forme d’une liste, d’une grille, de colonnes ou d’une seule toile... tout ce qui convient le mieux à votre application. Pour plus d’informations sur la conception d’onglets effectifs, consultez la rubrique : [Tabs Design](../../tabs/design/tabs.md).

Dans la mesure où cet onglet permet d’afficher des éléments provenant de plusieurs canaux, chaque élément doit afficher sa propre équipe, le canal et l’onglet de sorte que l’utilisateur puisse voir facilement où il provient.

![Onglet tâches personnelles](~/assets/images/Personal-apps-MY-tab.png)

### <a name="recent"></a>Récents

L’onglet **récent** permet à quelqu’un de parcourir tous les utilisateurs qu’il a consultés récemment dans votre application. Elle est classée par ordre chronologique (de la plus récente à la moins récente). Si vous cliquez sur un élément de cette liste, l’utilisateur accède à son canal et à son onglet.

![Onglet récent](~/assets/images/Personal-apps-Recent-tab.png)

### <a name="all"></a>Tous

Il s’agit d’une liste de tous les onglets de l’organisation de la personne (ceux auxquels ils ont accès, quand même). En d’autres termes, il les affiche partout où l’application est utilisée. Comme avec l’onglet **récent** , si vous sélectionnez un article dans la liste, l’utilisateur est directement associé à l’onglet et au canal appropriés.

### <a name="bot"></a>Bot

Un bot n’est pas obligatoire, mais il s’agit d’un excellent moyen de communiquer directement et en privé avec vos utilisateurs. La notification est l’une des fonctions les plus importantes d’une application personnelle et quelle est la meilleure façon de les avertir qu’avec la communication directe ?

Les robots fournissent des messages sous la forme de cartes, qui peuvent fournir des informations spécifiques (par exemple, une alerte indiquant que le nouveau contenu est disponible) ou des mises à jour étendues (par exemple, une liste de tâches quotidiennes). Pour plus d’informations sur la conception de robots efficaces, consultez la rubrique : [Design bot](../../bots/design/bots.md).

![Message d’accueil bot](~/assets/images/Personal-apps-Bot.png)

### <a name="help-and-settings"></a>Aide et paramètres

Le contenu de l’aide permet aux utilisateurs de découvrir les nuances de votre application. Ajoutez un onglet **paramètres** pour leur donner la possibilité de le personnaliser.

### <a name="about"></a>À propos

Incluez un onglet à **propos** de pour fournir des informations telles que le numéro de version, les fonctionnalités, la confidentialité et les liens d’autorisations.

## <a name="best-practices"></a>Meilleures pratiques

### <a name="communicate-directly-with-your-users"></a>Communiquer directement avec vos utilisateurs

Utilisez un bot pour informer les utilisateurs des modifications et des nouvelles fonctionnalités.

### <a name="customize-your-tabs"></a>Personnaliser vos onglets...

N’hésitez pas à ajouter d’autres onglets qui aideront vos utilisateurs à accomplir des tâches spécifiques.

### <a name="and-make-them-relevant-to-every-user"></a>... et les rendre pertinentes pour chaque utilisateur

Chaque onglet que vous déclarez dans le manifeste de votre application est visible par tous les utilisateurs. Par exemple, si votre application personnelle est un outil de création de notes de frais qui est utilisé par les responsables et les employés, un onglet **approbation** doit fournir un contenu significatif pour les deux rôles.
