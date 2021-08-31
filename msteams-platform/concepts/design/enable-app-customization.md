---
title: Activer la personnalisation de votre application
author: heath-hamilton
description: Comprendre comment Teams administrateurs peuvent personnaliser votre application pour leur organisation.
localization_priority: Normal
ms.author: surbhigupta
ms.topic: overview
ms.openlocfilehash: ffc429d3dee0ab05e65951233b60ec17ae659b0e
ms.sourcegitcommit: 306b6e8cb3aac8bfda10ef3999467a797d64539d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/20/2021
ms.locfileid: "58408663"
---
# <a name="enable-your-microsoft-teams-app-to-be-customized"></a>Activer la personnalisation Microsoft Teams votre application

Vous pouvez permettre aux clients de personnaliser certains aspects de votre application Microsoft Teams dans le centre d’administration Teams client. Cette fonctionnalité est prise en charge uniquement pour les applications publiées dans Teams store. Les applications et les applications téléchargées de côté publiées pour une organisation ne peuvent pas être personnalisées.

Voici quelques exemples possibles de cette fonctionnalité :

* Modification de la couleur d’accentuage de l’application pour qu’elle corresponde à la marque d’une organisation.
* Mise à jour du nom de l’application de *Contoso* vers *l’agent Contoso*, qui est le nom que les utilisateurs de l’organisation voient. (Remarque : les utilisateurs qui ajoutent un connecteur à une conversation ou un canal voient toujours le nom de l’application d’origine, *Contoso.)*

Vous pouvez activer cette fonctionnalité dans le Portail des développeurs [pour Teams](https://dev.teams.microsoft.com/home). Cette configuration, qui n’est pas disponible dans les versions antérieures à `configurableProperties` la version 1.10 du manifeste Teams’application.

## <a name="test-your-app"></a>Tester votre application

Vous ne pouvez pas tester cette fonctionnalité pendant le développement. La personnalisation d’application n’est pas prise en charge lors du chargement de version de version ou de publication dans le catalogue d’applications d’une organisation.

## <a name="user-considerations"></a>Considérations sur les utilisateurs

Fournir des instructions pour les clients (Teams administrateurs) qui souhaitent personnaliser votre application. Pour plus d’informations, voir [personnaliser les applications dans Teams](/MicrosoftTeams/customize-apps).

## <a name="see-also"></a>Voir aussi

* [Personnaliser des applications dans le Centre d Teams’administration Windows](/MicrosoftTeams/customize-apps)
