---
title: Développer des extensions de messagerie
description: Décrit la mise en place des extensions de messagerie dans Microsoft Teams
ms.topic: overview
keywords: extensions de messagerie teams
ms.openlocfilehash: 1eb75371b1a8adbeadbcbdbc0d06c7d88f2f1ccc
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696548"
---
# <a name="develop-messaging-extensions-for-microsoft-teams"></a>Développer des extensions de messagerie pour Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

Les extensions de messagerie sont un moyen puissant pour les utilisateurs d'interagir avec votre application à partir de Microsoft Teams. Avec cette fonctionnalité, les utilisateurs peuvent interroger ou publier des informations à partir de votre service et publier ces informations, sous forme de cartes, directement dans un message.

![Exemple de carte d'extension de messagerie](~/assets/images/compose-extensions/ceexample.png)

Les extensions de messagerie apparaissent en bas de la zone de composition. Quelques-uns sont intégrés, tels que Emoji, Giphy et Autocollant. Choisissez le **bouton Plus d'options** **(&#8943;)** pour voir d'autres extensions de messagerie, y compris celles que vous ajoutez à partir de la galerie d'applications ou que vous téléchargez vous-même.

Comment utiliser les extensions de messagerie ? Voici quelques possibilités :

* Éléments de travail et bogues
* Tickets de support client
* Graphiques et rapports d'utilisation
* Images et contenu multimédia
* Opportunités de vente et prospects

## <a name="types-of-messaging-extensions"></a>Types d'extensions de messagerie

Il existe principalement deux types d'extensions de messagerie que vous pouvez créer pour Teams aujourd'hui. Les rubriques suivantes vous guident tout au long du processus de création :

* [Extensions de messagerie basées sur la recherche](~/resources/messaging-extension-v3/search-extensions.md): interrogez votre service pour obtenir des informations et insérez-les dans un message. Exemple : Rechercher un élément de travail
* [Extensions de messagerie basées sur l'action](~/resources/messaging-extension-v3/create-extensions.md): collecter des informations auprès de l'utilisateur et publier dans un service tiers. Exemple : Créer un élément de travail
