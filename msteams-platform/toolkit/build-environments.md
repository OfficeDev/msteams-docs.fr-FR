---
title: Préparer la création d’applications avec le Kit de ressources Teams
author: surbhigupta
description: Dans cet article, vous allez apprendre à créer un environnement du Kit de ressources Teams et à gérer l’application dans le portail des développeurs
ms.author: v-amprasad
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: dc3a51d393a6445c26dddd54c471ecb630580b94
ms.sourcegitcommit: dccb48902e08484692ab927415bcd3d61dc50db2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/19/2022
ms.locfileid: "67806907"
---
# <a name="prepare-to-build-apps-using-teams-toolkit"></a>Préparer la création d’applications à l’aide du Kit de ressources Teams

Teams Toolkit prend en charge les environnements pour la création d’applications. Teams Toolkit permet également d’intégrer Azure Functions fonctionnalités ainsi que des services cloud dans l’application Teams que vous avez créée.

:::image type="content" source="../assets/images/buildapps-TTK.png" alt-text="Préparer la création d’applications à l’aide du Kit de ressources Teams":::

## <a name="build-environments"></a>Créer des environnements

Le Kit de ressources Teams dans Microsoft Visual Studio Code offre un ensemble d’environnements pour créer votre application Teams. Vous pouvez choisir n’importe qui de l’environnement suivant qui convient le mieux à votre application :

* JavaScript ou TypeScript
* SharePoint Framework (SPFx)

### <a name="create-your-teams-app-using-javascript-or-typescript"></a>Créer votre application Teams à l’aide de JavaScript ou TypeScript

Les applications créées avec JavaScript présentent les avantages suivants :

* L’application est fournie avec ses propres fonctionnalités d’interface utilisateur et d’expérience utilisateur qui sont riches et conviviales.
* Fournit des mises à niveau rapides vers des applications existantes.
* Distribue des applications sur plusieurs plateformes, telles qu’Android et iOS.
* Compatible pour la création d’une application avec des API existantes.

Le Kit de ressources Teams dans Visual Studio Code prend en charge la création des applications suivantes à l’aide de JavaScript ou TypeScript :

* Application onglet : votre application onglet peut avoir du contenu web, vous pouvez avoir un onglet personnalisé pour votre contenu web dans Teams ou ajouter des fonctionnalités spécifiques à Teams à votre contenu web.
* Application bot : les bots peuvent être des bots de conversation ou des bots conversationnels qui vous permettent d’effectuer des tâches simples et répétitives telles que le service clientèle ou le personnel du support technique.
* Bot de notification : vous pouvez envoyer des messages dans un canal Teams, un groupe ou une conversation personnelle par des bots de notification avec une requête HTTP.
* Bot de commandes : vous pouvez automatiser les tâches répétitives à l’aide du bot de commandes. Les bots de commandes vous aident à répondre à des requêtes simples ou à des commandes envoyées dans des conversations.
* Extensions de message : vous pouvez interagir avec votre service web via des boutons et des formulaires. Fonctionnalité fournie par l’extension de message.

### <a name="create-your-teams-app-using-spfx"></a>Créer votre application Teams à l’aide de SPFx

Le Kit de ressources Teams dans Visual Studio Code vous permet de créer des applications d’onglet à l’aide de SPFx. Ces applications présentent les avantages suivants :

* Vous permet d’intégrer facilement les données résidant dans SharePoint à votre équipe.
* Vous pouvez intégrer votre solution SPFx à vos API métier sécurisées avec Microsoft Azure Active Directory (Azure AD).
* Vous donne accès à différents outils open source.
* Crée pour vos applications puissantes qui peuvent fournir une excellente expérience utilisateur.
* S’intègre facilement à d’autres charges de travail Microsoft (Office) 365.
* Offre la flexibilité nécessaire pour héberger des applications quand cela est nécessaire.

## <a name="support-for-azure-functions"></a>Prise en charge des Azure Functions

Vous pouvez utiliser teams toolkit pour intégrer [Azure Functions](/azure/azure-functions/functions-overview) fonctionnalités dans la création d’applications. Vous pouvez vous concentrer sur les éléments de code les plus importants et Azure Functions faire le reste.
Azure Functions vous permettent d’implémenter :

1. Logique système dans vos blocs de code facilement disponibles. Ces blocs sont appelés fonctions.
1. À mesure que les demandes augmentent, Azure Functions répond à l’exigence avec autant de demandes que nécessaire.

Azure Function s’intègre à un tableau de [services cloud](add-resource.md#types-of-cloud-resources) qui fournissent des implémentations riches en fonctionnalités. Voici quelques scénarios courants pour Azure Functions :

* Lors de la création d’une API web
* Traitement des modifications apportées à la base de données
* Traitement des flux de données iot
* Gestion des files d’attente de messages

## <a name="see-also"></a>Voir aussi

* [Extension de kit de ressources Teams pour Visual Studio](visual-studio-overview.md)
* [Gérer vos applications Teams à l’aide du portail des développeurs](../concepts/build-and-test/teams-developer-portal.md)
* [Créer une application Teams à l’aide du kit de ressources Teams](create-new-project.md)
