---
title: Développer des extensions de messagerie
description: Décrit comment se familiariser avec les extensions de messagerie dans Microsoft teams
keywords: extensions de messagerie des extensions de messagerie teams
ms.openlocfilehash: 6ba8f73d40f795a83f28707ef89c207c5d51d67c
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673565"
---
# <a name="develop-messaging-extensions-for-microsoft-teams"></a>Développer des extensions de messagerie pour Microsoft teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

Les extensions de messagerie sont un moyen efficace pour les utilisateurs de s’engager avec votre application à partir de Microsoft Teams. Grâce à cette fonctionnalité, les utilisateurs peuvent interroger ou publier des informations à partir de votre service et publier ces informations, sous la forme de cartes, directement dans un message.

![Exemple de carte d’extension de messagerie](~/assets/images/compose-extensions/ceexample.png)

Les extensions de messagerie apparaissent au bas de la zone de composition. Quelques-unes sont intégrées, telles que les emoji, les Giphy et les autocollants. Cliquez sur le bouton **autres options** (**&#8943;**) pour afficher les autres extensions de messagerie, y compris celles que vous ajoutez à partir de la Galerie d’applications ou téléchargez vous-même.

Comment utiliseriez-vous les extensions de messagerie ? Voici quelques possibilités :

* Éléments de travail et bogues
* Tickets de support client
* Graphiques et rapports d’utilisation
* Images et contenu multimédia
* Opportunités de vente et prospects

## <a name="types-of-messaging-extensions"></a>Types d’extensions de messagerie

Il existe principalement deux types d’extensions de messagerie que vous pouvez créer pour teams dès aujourd’hui. Les rubriques suivantes vous guideront tout au long du processus de création :

* [Extensions de messagerie basées sur la recherche](~/resources/messaging-extension-v3/search-extensions.md): interrogez votre service pour obtenir des informations et insérez-les dans un message. Exemple : Rechercher un élément de travail
* [Extensions de messagerie basées sur les actions](~/resources/messaging-extension-v3/create-extensions.md): collectez des informations auprès de l’utilisateur et publiez-les sur un service tiers. Exemple : créer un élément de travail
