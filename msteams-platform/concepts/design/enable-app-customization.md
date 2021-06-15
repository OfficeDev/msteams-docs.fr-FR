---
title: Activer la personnalisation de votre application
author: heath-hamilton
description: Comprendre comment Teams administrateurs peuvent personnaliser votre application pour leur organisation.
localization_priority: Normal
ms.author: surbhigupta
ms.topic: overview
ms.openlocfilehash: bf1b43629c87dd4123520c634772e5dea14e0bb5
ms.sourcegitcommit: 64c1cf2a268ef101a519bc31d171618d0f6cd12a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/13/2021
ms.locfileid: "52915082"
---
# <a name="enable-your-microsoft-teams-app-to-be-customized"></a>Activer la personnalisation Microsoft Teams votre application

Vous pouvez permettre aux clients de personnaliser certains aspects de votre application Microsoft Teams dans le centre d’administration Teams client. Cette fonctionnalité est prise en charge uniquement pour les applications publiées dans Teams store. Les applications et les applications téléchargées de côté publiées pour une organisation ne peuvent pas être personnalisées.

Voici quelques exemples possibles de cette fonctionnalité :

* Modification de la couleur d’accentuage de l’application pour qu’elle corresponde à la marque d’une organisation.
* Mise à jour du nom de l’application de *Contoso* vers *l’agent Contoso*, qui est le nom que les utilisateurs de l’organisation voient. (Remarque : les utilisateurs qui ajoutent un connecteur à une conversation ou un canal voient toujours le nom de l’application d’origine, *Contoso.)*

Vous pouvez activer cette fonctionnalité dans le Portail des développeurs [pour Teams](https://dev.teams.microsoft.com/home). Cette configuration, qui ne sont pas disponibles dans les versions antérieures à `configurableProperties` la version 1.10 du manifeste Teams’application.

## <a name="test-your-app"></a>Tester votre application

Vous ne pouvez pas tester cette fonctionnalité pendant le développement. La personnalisation d’application n’est pas prise en charge pour le chargement de version de version ou la publication dans le catalogue d’applications d’une organisation.

## <a name="user-considerations"></a>Considérations sur les utilisateurs

En tant qu’éditeur d’application, fournissez les informations suivantes aux clients Teams administrateurs :
* Incluez une note recommandant de tester les modifications de personnalisation dans un client Teams test avant d’apporter des modifications dans son environnement de production. 
* Fournissez les meilleures pratiques pour personnaliser votre application.

## <a name="see-also"></a>Voir aussi

* [Personnaliser des applications dans le Centre d Teams’administration Windows](/MicrosoftTeams/customize-apps)
