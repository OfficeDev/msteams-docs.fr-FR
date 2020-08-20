---
title: Fonctionnalités de l’aperçu public pour les développeurs
description: Décrit les fonctionnalités de la version d’évaluation pour développeurs publics de Microsoft teams
keywords: fonctionnalités de développeur d’aperçu teams
ms.openlocfilehash: e607a6c65253a5fd94f8a805f1264a567bb8fd24
ms.sourcegitcommit: 9fd61042e8be513c2b2bd8a33ab5e9e6498d65c5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/20/2020
ms.locfileid: "46819174"
---
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a>Fonctionnalités de l’aperçu public pour les développeurs pour Microsoft teams

L’aperçu des développeurs inclut les nouvelles fonctionnalités suivantes :

## <a name="adaptive-cards-v12-support"></a>Prise en charge des cartes adaptatives v 1.2

La prise en charge des [cartes adaptatives v 1.2](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0) dans teams est désormais disponible pour le grand public. Toutefois, les [éléments multimédias](https://adaptivecards.io/explorer/Media.html) ne sont actuellement pas pris en charge dans les cartes adaptative v 1.2 sur la plateforme Teams.

## <a name="tabs-single-sign-on-sso"></a>Authentification unique (SSO) des onglets

Vous pouvez désormais utiliser l’authentification [unique (SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) pour vous connecter et authentifier un utilisateur sur un ordinateur de bureau et un appareil mobile à l’aide du kit de développement logiciel (SDK) JavaScript teams à partir d’une page de contenu Web. L’un des avantages est qu’un utilisateur n’a jamais à se connecter ; et une fois qu’ils ont accepté l’application à l’aide de leur profil : ils sont automatiquement connectés à leur onglet (y compris mobile).

Notre Aperçu pour les développeurs est disponible dans les versions de manifeste 1,5 et ultérieure. Notre implémentation actuelle peut uniquement obtenir une quantité limitée d’API Graph, mais nous fournissons une solution de contournement pour obtenir des API Graph supplémentaires à l’aide de notre API d’authentification existante.

## <a name="calls-and-online-meeting-bots"></a>Appels et robots de réunion en ligne

Avec l’ajout d' [API Microsoft Graph pour les appels et les réunions en ligne](/graph/api/resources/communications-api-overview?view=graph-rest-beta), les applications Microsoft teams peuvent désormais interagir avec les utilisateurs de façon enrichie à l’aide de la voix et de la vidéo. Ces API vous permettent d’ajouter de nouvelles fonctionnalités d’application, telles que la réponse vocale interactive (IVR), le contrôle d’appel et l’accès à des flux audio et/ou vidéo en temps réel pour les appels et les réunions, y compris le partage de bureau et d’application.

Nous avons ajouté une nouvelle section sur la façon de créer et de développer des appels et des robots de réunions en ligne, en commençant par la [vue d’ensemble](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).
