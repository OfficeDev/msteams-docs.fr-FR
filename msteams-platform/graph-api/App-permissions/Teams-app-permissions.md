---
title: Gérer les autorisations des applications Teams
author: surbhigupta
description: Dans ce module, découvrez comment les applications Teams sont gérées à différents endroits en fonction de la fonctionnalité.
ms.topic: reference
ms.localizationpriority: medium
ms.author: lomeybur
ms.openlocfilehash: 2bc501444e52f31061312c325ddf7dd80370240a
ms.sourcegitcommit: 84747a9e3c561c2ca046eda0b52ada18da04521d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2022
ms.locfileid: "68791847"
---
# <a name="permissions-in-teams-app"></a>Autorisations dans l’application Teams

L’autorisation pour l’application Teams est gérée à deux endroits, en fonction de la fonctionnalité de l’application :

* [Consentement spécifique à la ressource (RSC)](#resource-specific-consent)
* [Azure Active Directory Domain Services (Azure AD)](#azure-active-directory)

:::image type="content" source="../../assets/images/teams-app-permissions.png" alt-text="La capture d’écran décrit les différentes autorisations d’application Teams.":::

## <a name="resource-specific-consent"></a>Consentement spécifique à la ressource

RSC est une intégration Microsoft Teams et Microsoft API Graph qui permet à votre application d’utiliser des points de terminaison d’API pour gérer des ressources spécifiques, que ce soit des équipes ou des conversations, au sein d’une organisation. Pour plus d’informations, consultez [Activer le consentement spécifique à la ressource dans Teams](../rsc/resource-specific-consent.md).

Les autorisations RSC sont uniquement disponibles pour les applications Teams installées sur le client Teams et ne font actuellement pas partie du portail Azure AD et sont déclarées dans le fichier manifeste d’application Teams (JSON).

## <a name="azure-active-directory"></a>Azure Active Directory

Azure AD est un service cloud de gestion des identités et des accès. Ce service permet à vos employés d’accéder à des ressources externes, telles que Microsoft 365, le Portail Azure et des milliers d’autres applications SaaS. Pour plus d'informations, voir [Azure Active Directory](/azure/active-directory/fundamentals/active-directory-whatis).

### <a name="microsoft-graph-api-permission"></a>Autorisation Microsoft API Graph

API Graph autorisations sont gérées dans Azure AD. Pour que votre application puisse accéder aux données dans Microsoft Graph, l’utilisateur ou l’administrateur doivent lui accorder les autorisations appropriées via un processus de consentement. Si vous souhaitez en savoir plus, veuillez consulter la page [Référence des autorisations de Microsoft Graph](/graph/permissions-reference).

## <a name="capability-wise-management"></a>Gestion judicieuse des capacités

### <a name="bot-and-messaging-extension"></a>Bot et extension de messagerie

L’ID d’extension de bot ou de messagerie est généré en fonction de la plateforme d’inscription suivante. Cet ID est requis pour ajouter un bot ou une extension de messagerie à une application Teams.

* Portail Azure AD
* Portail développeur ou Bot Framework

#### <a name="azure-ad-portal"></a>Portail Azure AD

Lorsqu’un bot ou une extension de messagerie est inscrit sur le portail Azure AD, un ID d’application Azure AD lui est associé, qui se trouve dans le portail **Azure AD** > **Inscriptions d’applications**. Les points de terminaison et autres configurations de bot sont gérés dans le Portail Azure.

#### <a name="developer-or-bot-framework-portal"></a>Portail développeur ou Bot Framework

Lorsqu’un bot ou une extension de messagerie est inscrit dans le portail Développeur ou Bot Framework, elle n’a pas d’ID d’application Azure AD. Toutefois, l’ID d’extension de bot ou de messagerie se trouve sur le portail Bot Framework. Les points de terminaison et autres configurations de bot sont gérés dans le portail Bot Framework.

D’autres configurations teams spécifiques au bot peuvent être gérées dans la section Portail des développeurs de l’application.

### <a name="connectors"></a>Connecteurs

Les connecteurs ont un ID de connecteur et sont inscrits et gérés via le tableau de bord du développeur de connecteurs. Cet ID est nécessaire pour introduire un connecteur à l’application Teams. D’autres configurations spécifiques à Teams pour les connecteurs peuvent être gérées dans la section portail des développeurs de l’application.
