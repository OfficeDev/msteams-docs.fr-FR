---
title: Fonctionnalités de la prévisualisation pour les développeurs publics
description: Détails des fonctionnalités de la prévisualisation Microsoft Teams Public Developer
ms.topic: reference
localization_priority: Normal
keywords: Teams prévisualiser les fonctionnalités de développement
ms.openlocfilehash: 84683420a5c61bb1eb493f8191bfbcbe97f6fb46
ms.sourcegitcommit: 60561c7cd189c9d6fa5e09e0f2b6c24476f2dff5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/06/2021
ms.locfileid: "52230903"
---
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a>Fonctionnalités de la prévisualisation pour les développeurs publics Microsoft Teams

> [!NOTE]
> Cette page sera dépréciée en juin 2021. Pour plus d’informations sur les fonctionnalités disponibles pour la prévisualisation pour les développeurs, voir [Nouveautés](~/whats-new.md)

La prévisualisation pour développeurs inclut les nouvelles fonctionnalités suivantes :

## <a name="app-customization"></a>Personnalisation de l’application

Vous pouvez maintenant définir un ensemble de propriétés sélectionné, qu’un administrateur Teams peut personnaliser ou renommer en fonction des besoins de son organisation. Pour plus d’informations, [voir la fonctionnalité de personnalisation de l’application.](~/concepts/design/design-teams-app-overview.md)

## <a name="tabs-single-sign-on-sso"></a>Onglets sign-on (SSO)

Vous pouvez désormais utiliser l’authentification unique [(SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) pour vous connecter et authentifier un utilisateur sur ordinateur de bureau et mobile à l’aide du SDK JavaScript Teams à partir d’une page de contenu web. L’un des avantages est qu’un utilisateur n’a jamais à se connecter ; et une fois qu’ils ont accepté l’application à l’aide de leur profil : ils sont automatiquement inscrits à leur onglet (y compris mobile).

Notre version préliminaire pour développeurs est disponible dans les versions de manifeste 1.5 et ultérieures. Notre implémentation actuelle ne peut obtenir qu’une quantité limitée d’API Graph, mais nous fournissons une solution de contournement pour obtenir des API de Graph supplémentaires à l’aide de notre API d’authentification existante.

## <a name="calls-and-online-meeting-bots"></a>Appels et bots de réunion en ligne

Avec l’ajout des API [Microsoft Graph](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)pour les appels et les réunions en ligne, les applications Microsoft Teams peuvent désormais interagir avec les utilisateurs de manière enrichie à l’aide de la voix et de la vidéo. Ces API vous permettent d’ajouter de nouvelles fonctionnalités d’application telles que la réponse vocale interactive (IVR), le contrôle d’appel et l’accès aux flux audio et/ou vidéo en temps réel pour les appels et les réunions, y compris le partage de bureau et d’application.

Nous avons ajouté une nouvelle section sur la création et le développement d’appels et de bots de réunions en ligne, en commençant par la [vue d’ensemble.](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)


## <a name="image-enlarge-support"></a>Prise en charge de l’agrandissement de l’image

Il est désormais possible pour les bots d’indiquer les images partagées dans les cartes adaptatives Teams sont autorisées à être agrandies. Cela est utile pour les scénarios tels que le partage de guides visuels détaillés pas à pas via des bots qui peuvent être difficiles à lire pour les utilisateurs dans le cas contraire. Pour rendre une image ex expandable, marquez-la `allowExpand: true` simplement comme illustré ci-dessous.

```json
    {
      "type": "Image",
      "url": "https://picsum.photos/200/200?image=110",
      "msTeams": {
        "allowExpand": true
      }
    }
```
Cela entraîne le Teams client web/de bureau à restituer un élément en pointant sur l’image pour permettre à l’utilisateur de développer l’image.
