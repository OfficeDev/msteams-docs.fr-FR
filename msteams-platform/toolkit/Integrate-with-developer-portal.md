---
title: Intégrer avec le portail des développeurs dans le Kit de ressources Teams
author: zyxiaoyuer
description: Dans ce module, découvrez comment intégrer le portail des développeurs dans Teams Toolkit
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 07/29/2022
ms.openlocfilehash: b54e833f5c8292c0b426e859e63d858102860a47
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/07/2022
ms.locfileid: "67617222"
---
# <a name="integrate-with-developer-portal"></a>Intégrer au portail des développeurs

Vous pouvez configurer et gérer votre application dans le portail des développeurs dans teams Toolkit.

## <a name="to-publish-app-using-developer-portal"></a>Pour publier une application à l’aide du portail des développeurs

Les étapes suivantes vous aident à publier votre application dans le portail des développeurs :

1. Sélectionnez **Le portail des développeurs pour Teams** sous **DÉPLOIEMENT**.

    :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/dev-portal-ttk.png" alt-text="Documentation pour les développeurs":::

   À présent, le portail des développeurs s’ouvre dans un navigateur.

1. Connectez-vous au [portail des développeurs pour Teams](https://dev.teams.microsoft.com) à l’aide du compte correspondant.
1. Importez votre package d’application dans le fichier zip, puis sélectionnez **Application** > **d’importation d’application**.
1. Sélectionnez **Publier** > **sur votre organisation**.

## <a name="to-update-manifest-file-and-app-package"></a>Pour mettre à jour le fichier manifeste et le package d’application

Si des modifications sont apportées au fichier manifeste de l’application Teams, vous pouvez mettre à jour le manifeste et publier à nouveau l’application Teams. Pour publier manuellement l’application Teams, vous pouvez tirer profit du [Portail des développeurs pour Teams](https://dev.teams.microsoft.com/home).

1. Connectez-vous au [portail des développeurs pour Teams](https://dev.teams.microsoft.com) à l’aide du compte correspondant.
1. Importez votre package d’application dans le fichier zip, puis sélectionnez **Application** > **d’importation d’application**.<br>
   Vous devez remplacer l’application que vous avez précédemment chargée sur le portail des développeurs.
1. Pour publier votre application, sélectionnez **Publier** > **sur votre organisation**.

Vous pouvez effectuer la configuration suivante dans le portail des développeurs :

* **Informations de base** : cette section affiche et vous permet de modifier le nom de l’application, l’ID d’application, les descriptions, la version, les informations de développeur, les URL d’application, l’ID d’application (client) et l’ID microsoft partner network.
* **Personnalisation** : cette page affiche les détails de l’icône de l’application.
* **Fonctionnalités de l’application** : vous pouvez ajouter les fonctionnalités suivantes à votre application :
  * Application personnelle
  * Bot
  * Connector
  * Scène
  * Application de groupe et de canal
  * Extension de la messagerie
  * Extension de réunion
  * Notification de flux d’activité
* **Autorisations** : cette section vous permet d’accorder des autorisations d’appareil, des autorisations d’équipe, des autorisations de conversation ou de réunion et des autorisations utilisateur pour votre application.
* **Authentification unique** : vous pouvez configurer votre application pour authentifier les utilisateurs avec l’authentification unique (SSO).
* **Langues** : vous pouvez configurer ou modifier la langue de votre application.
* **Domaine** : vous pouvez ajouter les domaines pour charger vos applications dans le client Teams (par exemple : *.example.com).

## <a name="see-also"></a>Voir aussi

* [Documentation pour les développeurs](../concepts/build-and-test/teams-developer-portal.md)
* [Gérez vos applications dans le portail des développeurs](../concepts/build-and-test/manage-your-apps-in-developer-portal.md)
