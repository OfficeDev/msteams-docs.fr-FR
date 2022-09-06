---
title: Activer la personnalisation des applications et bloquer les applications jusqu’à ce que l’administrateur autorise
author: heath-hamilton
description: Dans ce module, découvrez comment les administrateurs Teams peuvent personnaliser votre application Teams pour leur organisation et masquer l’application Teams jusqu’à ce que l’administrateur approuve.
ms.localizationpriority: medium
ms.author: surbhigupta
ms.topic: overview
ms.openlocfilehash: 7d71e341bd1613e9efe6c900f29e1bd340006b49
ms.sourcegitcommit: d92e14fad6567fe91fd52ee6c213836740316683
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/06/2022
ms.locfileid: "67604953"
---
# <a name="enable-app-customization-and-block-apps-till-admin-allows"></a>Activer la personnalisation des applications et bloquer les applications jusqu’à ce que l’administrateur autorise

Microsoft Teams permet aux administrateurs de personnaliser l’application Teams pour améliorer l’expérience du Store et respecter la personnalisation de leur organisation. Un développeur d’applications peut autoriser la personnalisation de son application par un administrateur Teams. Pour plus d’informations, consultez [Personnaliser les applications dans le Centre d’administration Teams](/MicrosoftTeams/customize-apps).

## <a name="enable-customization-for-your-microsoft-teams-app"></a>Activer la personnalisation pour votre application Microsoft Teams

Vous pouvez autoriser les clients à personnaliser certains aspects de votre application Microsoft Teams dans le Centre d’administration Teams. Cette fonctionnalité est prise en charge uniquement pour les applications publiées dans le magasin Teams. Les applications et applications chargées indépendamment publiées pour une organisation ne peuvent pas être personnalisées.

Voici quelques exemples possibles de cette fonctionnalité :

* Modification de la couleur d’accentuation de l’application pour qu’elle corresponde à la marque d’une organisation.
* Mise à jour du nom de l’application de *Contoso* vers *Agent Contoso*, qui est le nom que les utilisateurs de l’organisation verront.
(Remarque : les utilisateurs qui ajoutent un connecteur à une conversation ou à un canal verront toujours le nom de l’application d’origine, *Contoso*.)

Vous pouvez activer cette fonctionnalité en définissant les propriétés d’application que vos clients peuvent personnaliser dans la [`configurableProperties` section du manifeste de l’application Teams](/microsoftteams/platform/resources/schema/manifest-schema#configurableproperties), à compter de la version 1.11. Vous pouvez le faire dans le [portail des développeurs pour Teams](https://dev.teams.microsoft.com/home) si vous avez choisi d’utiliser le portail des développeurs pour modifier le manifeste de votre application.

> [!IMPORTANT]
> Vous ne pouvez pas tester cette fonctionnalité pendant le développement. La personnalisation des applications n’est pas prise en charge lors du chargement indépendant ou de la publication dans le catalogue d’applications d’une organisation.

### <a name="user-considerations"></a>Considérations relatives aux utilisateurs

Fournissez des instructions aux clients (en particulier les administrateurs Teams) qui souhaitent personnaliser votre application. Pour plus d’informations, consultez [personnaliser des applications dans Teams](/MicrosoftTeams/customize-apps).

## <a name="block-apps-by-default-for-users-until-an-admin-approves"></a>Bloquer les applications par défaut pour les utilisateurs jusqu’à ce qu’un administrateur approuve

Pour améliorer l’expérience d’application Teams, vous pouvez masquer une application aux utilisateurs par défaut jusqu’à ce que l’administrateur autorise à afficher l’application. Par exemple, Contoso Electronics a créé une application de support technique pour Teams. Pour activer le bon fonctionnement de l’application, Contoso Electronics souhaite que les clients configurent d’abord des propriétés spécifiques de l’application. L’application est masquée par défaut et n’est disponible pour les utilisateurs qu’une fois que l’administrateur l’autorise.

Pour masquer l’application, dans le fichier manifeste de l’application, définissez la propriété `defaultBlockUntilAdminAction` sur `true`. Lorsque la propriété est définie sur `true`, dans le Centre d’administration Teams > **Gérer les applications**, **bloqué par l’éditeur** apparaît dans l’**État** de l’application :

:::image type="content" source="../../assets/images/manage-apps-status.png" alt-text="La capture d’écran est un exemple montrant une application bloquée par l’éditeur." lightbox="../../assets/images/manage-apps-status-expanded.png":::

L’administrateur obtient une demande d’action avant qu’un utilisateur puisse accéder à l’application. Sous **Gérer les applications**, les administrateurs peuvent sélectionner **Autoriser** pour autoriser l’application avec **bloqué par l’état** de l’éditeur :

:::image type="content" source="../../assets/images/manage-apps-allow.png" alt-text="La capture d’écran est un exemple qui montre l’option d’autorisation pour l’application bloquée par l’éditeur." lightbox="../../assets/images/manage-apps-allow-expanded.png":::

Si, par défaut, vous ne souhaitez pas que l’application soit masquée, vous pouvez mettre à jour la propriété `defaultBlockUntilAdminAction` sur `false`. Lorsque la nouvelle version de l’application est approuvée, par défaut, l’application est autorisée tant que l’administrateur n’a effectué aucune action explicite.

> [!NOTE]
> Pour les applications métier, `defaultBlockUntilAdminAction` n’est pas pris en charge. L’application n’est pas bloquée si vous chargez une application métier avec cette propriété.

## <a name="see-also"></a>Voir aussi

* [Schéma de manifeste d’application](/microsoftteams/platform/resources/schema/manifest-schema)
* [Personnaliser des applications dans le centre d’administration Teams](/MicrosoftTeams/customize-apps)
