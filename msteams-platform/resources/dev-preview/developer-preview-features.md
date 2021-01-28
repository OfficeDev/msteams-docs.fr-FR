---
title: Fonctionnalités de la prévisualisation pour les développeurs publics
description: Détails des fonctionnalités de la prévisualisation du développeur public Microsoft Teams
ms.topic: reference
keywords: Teams prévisualiser les fonctionnalités de développement
ms.openlocfilehash: 3275ef7ac0d4ba052f417f6e852f48e2fdf267f5
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014354"
---
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a>Fonctionnalités de la prévisualisation pour les développeurs publics pour Microsoft Teams

La prévisualisation pour développeurs inclut les nouvelles fonctionnalités suivantes :

## <a name="tabs-single-sign-on-sso"></a>Onglets sign-on (SSO)

Vous pouvez désormais utiliser l’authentification unique [(SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) pour vous connecter et authentifier un utilisateur sur ordinateur de bureau et mobile à l’aide du SDK JavaScript Teams à partir d’une page de contenu web. L’un des avantages est qu’un utilisateur n’a jamais à se connecter ; et une fois qu’ils ont accepté l’application à l’aide de leur profil : ils sont automatiquement inscrits à leur onglet (y compris mobile).

Notre version préliminaire pour développeurs est disponible dans les versions de manifeste 1.5 et ultérieures. Notre implémentation actuelle ne peut obtenir qu’une quantité limitée d’API Graph, mais nous fournissons une solution de contournement pour obtenir des API Graph supplémentaires à l’aide de notre API d’authentification existante.

## <a name="calls-and-online-meeting-bots"></a>Appels et bots de réunion en ligne

Avec l’ajout d’API Microsoft Graph pour les appels et les réunions en ligne, les applications Microsoft Teams peuvent désormais interagir avec les [utilisateurs](/graph/api/resources/communications-api-overview?view=graph-rest-beta)de manière enrichie à l’aide de la voix et de la vidéo. Ces API vous permettent d’ajouter de nouvelles fonctionnalités d’application telles que la réponse vocale interactive (IVR), le contrôle d’appel et l’accès aux flux audio et/ou vidéo en temps réel pour les appels et les réunions, y compris le partage de bureau et d’application.

Nous avons ajouté une nouvelle section sur la création et le développement d’appels et de bots de réunions en ligne, en commençant par la [vue d’ensemble.](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)

## <a name="image-enlarge-support"></a>Prise en charge de l’agrandissement de l’image

Il est désormais possible pour les bots d’indiquer les images partagées dans les cartes adaptatives dans Teams qui sont autorisées à être agrandies. Cela est utile pour les scénarios tels que le partage de guides visuels détaillés pas à pas via des bots qui peuvent être difficiles à lire pour les utilisateurs dans le cas contraire. Pour rendre une image ex expandable, marquez-la `allowExpand: true` simplement comme illustré ci-dessous.

```json
    {
      "type": "Image",
      "url": "https://picsum.photos/200/200?image=110",
      "msTeams": {
        "allowExpand": true
      }
    }
```
Ainsi, le client web/de bureau Teams restituera un élément sur l’image pour permettre à l’utilisateur de développer l’image.

