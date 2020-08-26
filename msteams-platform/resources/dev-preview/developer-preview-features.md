---
title: Fonctionnalités de l’aperçu public pour les développeurs
description: Détails des fonctionnalités de Microsoft teams public developer preview
keywords: fonctionnalités de développeur d’aperçu teams
ms.openlocfilehash: 773e0334bddf45b7b86d31329b99607f3b70c534
ms.sourcegitcommit: 52732714105fac07c331cd31e370a9685f45d3e1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/25/2020
ms.locfileid: "46874841"
---
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a>Fonctionnalités de l’aperçu public pour les développeurs pour Microsoft teams

L’aperçu des développeurs inclut les nouvelles fonctionnalités suivantes :

## <a name="tabs-single-sign-on-sso"></a>Authentification unique (SSO) des onglets

Vous pouvez désormais utiliser l’authentification [unique (SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) pour vous connecter et authentifier un utilisateur sur un ordinateur de bureau et un appareil mobile à l’aide du kit de développement logiciel (SDK) JavaScript teams à partir d’une page de contenu Web. L’un des avantages est qu’un utilisateur n’a jamais à se connecter ; et une fois qu’ils ont accepté l’application à l’aide de leur profil : ils sont automatiquement connectés à leur onglet (y compris mobile).

Notre Aperçu pour les développeurs est disponible dans les versions de manifeste 1,5 et ultérieure. Notre implémentation actuelle peut uniquement obtenir une quantité limitée d’API Graph, mais nous fournissons une solution de contournement pour obtenir des API Graph supplémentaires à l’aide de notre API d’authentification existante.

## <a name="calls-and-online-meeting-bots"></a>Appels et robots de réunion en ligne

Avec l’ajout d' [API Microsoft Graph pour les appels et les réunions en ligne](/graph/api/resources/communications-api-overview?view=graph-rest-beta), les applications Microsoft teams peuvent désormais interagir avec les utilisateurs de façon enrichie à l’aide de la voix et de la vidéo. Ces API vous permettent d’ajouter de nouvelles fonctionnalités d’application, telles que la réponse vocale interactive (IVR), le contrôle d’appel et l’accès à des flux audio et/ou vidéo en temps réel pour les appels et les réunions, y compris le partage de bureau et d’application.

Nous avons ajouté une nouvelle section sur la façon de créer et de développer des appels et des robots de réunions en ligne, en commençant par la [vue d’ensemble](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).

## <a name="image-enlarge-support"></a>Prise en charge de l’image

Il est désormais possible pour les robots d’indiquer les images partagées dans les cartes adaptatives de teams qui peuvent être agrandies. Cela est utile pour des scénarios tels que le partage de guides détaillés pas à pas via des robots qui pourraient être difficiles à lire pour les utilisateurs. Pour qu’une image soit extensible, il vous suffit de la marquer `allowExpand: true` comme indiqué ci-dessous.

```json
    {
      "type": "Image",
      "url": "https://picsum.photos/200/200?image=110",
      "msTeams": {
        "allowExpand": true
      }
    }
```
Cela entraînera le rendu par le client teams Web/de bureau d’un élément sur l’image pour permettre à l’utilisateur de développer l’image.

