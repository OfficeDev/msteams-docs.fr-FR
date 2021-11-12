---
title: Personnaliser votre application Teams client
author: heath-hamilton
description: Comprendre comment Teams administrateurs peuvent personnaliser votre application pour leur organisation.
ms.localizationpriority: medium
ms.author: surbhigupta
ms.topic: overview
keywords: marque de couleur d’accentuer masquer l’approbation de l’application
ms.openlocfilehash: 1487a1a44991143b93b87bf47bdb93180d97cb8c
ms.sourcegitcommit: 781f34af2a95952bf437d0b7236ae995f4e14a08
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/12/2021
ms.locfileid: "60948613"
---
# <a name="customize-your-teams-app"></a>Personnaliser votre application Teams client

## <a name="enable-your-microsoft-teams-app-to-be-customized"></a>Activer la personnalisation Microsoft Teams votre application

Vous pouvez permettre aux clients de personnaliser certains aspects de votre application Microsoft Teams dans le centre d’administration Teams client. Cette fonctionnalité est prise en charge uniquement pour les applications publiées dans Teams store. Les applications et les applications téléchargées de côté publiées pour une organisation ne peuvent pas être personnalisées.

Voici quelques exemples possibles de cette fonctionnalité :

* Modification de la couleur d’accentuage de l’application pour qu’elle corresponde à la marque d’une organisation.
* Mise à jour du nom de l’application de *Contoso* vers *l’agent Contoso,* qui est le nom que les utilisateurs de l’organisation voient. (Remarque : les utilisateurs qui ajoutent un connecteur à une conversation ou un canal voient toujours le nom de l’application d’origine, *Contoso.)*

Vous pouvez activer cette fonctionnalité dans le Portail des développeurs [pour Teams](https://dev.teams.microsoft.com/home). Cette `configurableProperties` configuration, qui n’est pas disponible dans les versions antérieures à la version 1.10 du manifeste Teams’application.

### <a name="test-your-app"></a>Tester votre application

Vous ne pouvez pas tester cette fonctionnalité pendant le développement. La personnalisation d’application n’est pas prise en charge lors du chargement de version de version ou de publication dans le catalogue d’applications d’une organisation.

### <a name="user-considerations"></a>Considérations sur les utilisateurs

Fournir des instructions pour les clients (Teams administrateurs) qui souhaitent personnaliser votre application. Pour plus d’informations, voir [personnaliser les applications dans Teams](/MicrosoftTeams/customize-apps).

## <a name="hide-teams-app-until-admin-approves"></a>Masquer Teams application jusqu’à ce que l’administrateur approuve

Pour améliorer Teams l’expérience d’application, vous pouvez masquer une application aux utilisateurs par défaut jusqu’à ce que l’administrateur autorise à la désinsidation de l’application. Par exemple, Contoso Electronics a créé une application de service d’Teams. Pour activer le fonctionnement approprié de l’application, Contoso Electronics souhaite que les clients d’abord configurer des propriétés spécifiques de l’application. L’application est masquée par défaut et n’est accessible aux utilisateurs qu’une fois que l’administrateur l’autorise.

Pour masquer l’application, dans le fichier manifeste de l’application, définissez `defaultBlockUntilAdminAction` la propriété sur `true` . Lorsque la propriété est définie sur , dans Teams centre d’administration > Gérer les applications , Bloqué par l’éditeur apparaît dans `true` l’état de l’application :  

![Gérer les applications bloquées par un éditeur](../../assets/images/apps-in-meetings/manageappsblockedapps.png)

L’administrateur reçoit une demande d’action avant qu’un utilisateur puisse accéder à l’application. Sous **Gérer les applications,** les administrateurs peuvent sélectionner **Autoriser** l’application dont l’état est Bloqué **par l’éditeur** :

![Gérer les applications](../../assets/images/apps-in-meetings/manageapp.png)

Si, par défaut, vous ne souhaitez pas que l’application soit masquée, vous pouvez mettre à jour `defaultBlockUntilAdminAction` la propriété sur `false` . Lorsque la nouvelle version de l’application est approuvée, par défaut l’application est autorisée tant que l’administrateur n’a pas pris d’action explicite.

> [!NOTE]
> `defaultBlockUntilAdminAction` n’est pas pris en charge pour les applications LOB. Si vous chargez une application LOB avec cette propriété, l’application ne sera pas bloquée.

## <a name="see-also"></a>Voir aussi

* [Schéma de manifeste d’application](/microsoftteams/platform/resources/schema/manifest-schema)
* [Personnaliser des applications dans le Centre d Teams’administration Windows](/MicrosoftTeams/customize-apps)

