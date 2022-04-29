---
title: Personnaliser votre application Teams
author: heath-hamilton
description: Découvrez comment les administrateurs Teams peuvent personnaliser votre application pour leur organisation.
ms.localizationpriority: high
ms.author: surbhigupta
ms.topic: overview
keywords: marque de couleur d’accentuation masquer l’approbation de l’application
ms.openlocfilehash: 4728e6f34680d51983558d1ad96c47ffe3650234
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111198"
---
# <a name="customize-your-teams-app"></a>Personnaliser votre application Teams

## <a name="enable-your-microsoft-teams-app-to-be-customized"></a>Activer la personnalisation de votre application Microsoft Teams

Vous pouvez autoriser les clients à personnaliser certains aspects de votre application Microsoft Teams dans le Centre d’administration Teams. Cette fonctionnalité est prise en charge uniquement pour les applications publiées dans le magasin Teams. Les applications et applications chargées indépendamment publiées pour une organisation ne peuvent pas être personnalisées.

Voici quelques exemples possibles de cette fonctionnalité :

* Modification de la couleur d’accentuation de l’application pour qu’elle corresponde à la marque d’une organisation.
* Mise à jour du nom de l’application de *Contoso* vers *Agent Contoso*, qui est le nom que les utilisateurs de l’organisation verront. (Remarque : les utilisateurs qui ajoutent un connecteur à une conversation ou à un canal verront toujours le nom de l’application d’origine, *Contoso*.)

Vous pouvez activer cette fonctionnalité dans le [Portail des développeurs pour Teams](https://dev.teams.microsoft.com/home). Cela configure `configurableProperties`, qui n’est pas disponible dans les versions antérieures à la version 1.10 du manifeste de l’application Teams.

### <a name="test-your-app"></a>Tester votre application

Vous ne pouvez pas tester cette fonctionnalité pendant le développement. La personnalisation des applications n’est pas prise en charge lors du chargement indépendant ou de la publication dans le catalogue d’applications d’une organisation.

### <a name="user-considerations"></a>Considérations relatives aux utilisateurs

Fournissez des instructions aux clients (en particulier les administrateurs Teams) qui souhaitent personnaliser votre application. Pour plus d’informations, consultez [personnaliser des applications dans Teams](/MicrosoftTeams/customize-apps).

## <a name="hide-teams-app-until-admin-approves"></a>Masquer l’application Teams jusqu’à ce que l’administrateur approuve

Pour améliorer l’expérience d’application Teams, vous pouvez masquer une application aux utilisateurs par défaut jusqu’à ce que l’administrateur autorise à afficher l’application. Par exemple, Contoso Electronics a créé une application de support technique pour Teams. Pour activer le bon fonctionnement de l’application, Contoso Electronics souhaite que les clients configurent d’abord des propriétés spécifiques de l’application. L’application est masquée par défaut et n’est disponible pour les utilisateurs qu’une fois que l’administrateur l’autorise.

> [!NOTE]
> Le magasin Teams a évolué :
> 
> Auparavant, les applications métier étaient mises à jour en sélectionnant les points de suspension sur la vignette. Avec l’expérience mise à jour du Magasin Teams, vous pouvez maintenant mettre à jour les applications métier en vous connectant au [centre d’administration Teams](https://admin.teams.microsoft.com).

Pour masquer l’application, dans le fichier manifeste de l’application, définissez la propriété `defaultBlockUntilAdminAction` sur `true`. Lorsque la propriété est définie sur `true`, dans le Centre d’administration Teams > **Gérer les applications**, **bloqué par l’éditeur** apparaît dans l’**État** de l’application :

![Gérer les applications bloquées par l’éditeur](../../assets/images/apps-in-meetings/manageappsblockedapps.png)

L’administrateur obtient une demande d’action avant qu’un utilisateur puisse accéder à l’application. Sous **Gérer les applications**, les administrateurs peuvent sélectionner **Autoriser** pour autoriser l’application avec **bloqué par l’état** de l’éditeur :

![Gérer les applications](../../assets/images/apps-in-meetings/manageapp.png)

Si, par défaut, vous ne souhaitez pas que l’application soit masquée, vous pouvez mettre à jour la propriété `defaultBlockUntilAdminAction` sur `false`. Lorsque la nouvelle version de l’application est approuvée, par défaut, l’application est autorisée tant que l’administrateur n’a effectué aucune action explicite.

> [!NOTE]
> `defaultBlockUntilAdminAction` n’est pas pris en charge pour les applications métier. Si vous chargez une application métier avec cette propriété, l’application ne sera pas bloquée.

## <a name="see-also"></a>Voir aussi

* [Schéma de manifeste d’application](/microsoftteams/platform/resources/schema/manifest-schema)
* [Personnaliser des applications dans le centre d’administration Teams](/MicrosoftTeams/customize-apps)