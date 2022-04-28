---
title: Développer des extensions de message
description: Décrit comment bien démarrer avec les extensions de message dans Microsoft Teams
ms.topic: overview
ms.localizationpriority: medium
keywords: extensions de message teams
ms.openlocfilehash: b1d219bbb8e79a99836ad20b35442e10ec537c4a
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104331"
---
# <a name="develop-message-extensions-for-microsoft-teams"></a>Développer des extensions de message pour Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

Les extensions de message sont un moyen puissant pour les utilisateurs d’interagir avec votre application à partir de Microsoft Teams. Avec cette fonctionnalité, les utilisateurs peuvent interroger ou publier des informations vers et depuis votre service et publier ces informations, sous forme de cartes, directement dans un message.

![Exemple de carte d’extension de message](~/assets/images/compose-extensions/ceexample.png)

Les extensions de message apparaissent en bas de la zone de composition. Quelques-uns sont intégrés, tels que Emoji, Giphy et Sticker. Choisissez le bouton **Plus d’options** (**&#8943;**) pour afficher d’autres extensions de message, y compris celles que vous ajoutez à partir de la galerie d’applications ou que vous chargez vous-même.

Comment utiliseriez-vous les extensions de message ? Voici quelques possibilités :

* Éléments de travail et bogues
* Tickets de support client
* Graphiques et rapports d’utilisation
* Images et contenu multimédia
* Opportunités et prospects de ventes

## <a name="types-of-message-extensions"></a>Types d’extensions de message

Il existe principalement deux types d’extensions de message que vous pouvez créer pour Teams aujourd’hui. Les rubriques suivantes vous guideront tout au long du processus de création :

* [Rechercher des extensions de message basées sur](~/resources/messaging-extension-v3/search-extensions.md) : interrogez votre service pour obtenir des informations et insérez-les dans un message. Exemple : Rechercher un élément de travail
* [Extensions de message basées sur des actions](~/resources/messaging-extension-v3/create-extensions.md) : collectez des informations de l’utilisateur et publiez-les dans un service tiers. Exemple : Créer un élément de travail
