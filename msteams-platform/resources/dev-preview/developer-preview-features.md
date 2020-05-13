---
title: Fonctionnalités de l’aperçu public pour les développeurs
description: Décrit les fonctionnalités de la version d’évaluation pour développeurs publics de Microsoft teams
keywords: fonctionnalités de développeur d’aperçu teams
ms.openlocfilehash: 7ed442072779917dcc5db3ebcb4afaac9db0407f
ms.sourcegitcommit: b9e8839858ea8e9e33fe5e20e14bbe86c75fd510
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/12/2020
ms.locfileid: "44210700"
---
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a>Fonctionnalités de l’aperçu public pour les développeurs pour Microsoft teams

L’aperçu des développeurs inclut les nouvelles fonctionnalités suivantes :

## <a name="adaptive-cards-v12-support"></a>Prise en charge des cartes adaptatives v 1.2

La prise en charge des [cartes adaptatives v 1.2](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0) dans teams est désormais disponible pour le grand public. Toutefois, les [éléments multimédias](https://adaptivecards.io/explorer/Media.html) ne sont actuellement pas pris en charge dans les cartes adaptative v 1.2 sur la plateforme Teams.

## <a name="tabs-single-sign-on-sso"></a>Authentification unique (SSO) des onglets

Vous pouvez désormais utiliser l’authentification [unique (SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) pour vous connecter et authentifier un utilisateur sur un ordinateur de bureau et un appareil mobile à l’aide du kit de développement logiciel (SDK) JavaScript teams à partir d’une page de contenu Web. L’un des avantages est qu’un utilisateur n’a jamais à se connecter ; et une fois qu’ils ont accepté l’application à l’aide de leur profil : ils sont automatiquement connectés à leur onglet (y compris mobile).

Notre Aperçu pour les développeurs est disponible dans les versions de manifeste 1,5 et ultérieure. Notre implémentation actuelle peut uniquement obtenir une quantité limitée d’API Graph, mais nous fournissons une solution de contournement pour obtenir des API Graph supplémentaires à l’aide de notre API d’authentification existante.

## <a name="personal-apps-static-tabs-and-1-1-bots-enabled-on-mobile"></a>Applications personnelles (onglets statiques et robots 1-1) activés sur mobile

Les applications personnelles installées (onglets statiques et robots 1-1) sont désormais disponibles dans le bac d’applications sur les appareils mobiles. Pour plus d’informations, consultez la rubrique [Design Guidelines for mobile](~/tabs/design/tabs-mobile.md) for Design Guidance. Les applications ne peuvent être installées qu’à partir d’un client de bureau ou Web, et peuvent prendre jusqu’à 4 heures pour être disponibles sur mobile après l’installation.

Cela inclut la capacité d’un administrateur système à précoder une application via des [stratégies de configuration d’application](/microsoftteams/teams-app-setup-policies). Les applications qui ont été épinglées seront affichées dans le tiroir d’application.

## <a name="calls-and-online-meeting-bots"></a>Appels et robots de réunion en ligne

Avec l’ajout d' [API Microsoft Graph pour les appels et les réunions en ligne](/graph/api/resources/communications-api-overview?view=graph-rest-beta), les applications Microsoft teams peuvent désormais interagir avec les utilisateurs de façon enrichie à l’aide de la voix et de la vidéo. Ces API vous permettent d’ajouter de nouvelles fonctionnalités d’application, telles que la réponse vocale interactive (IVR), le contrôle d’appel et l’accès à des flux audio et/ou vidéo en temps réel pour les appels et les réunions, y compris le partage de bureau et d’application.

Nous avons ajouté une nouvelle section sur la façon de créer et de développer des appels et des robots de réunions en ligne, en commençant par la [vue d’ensemble](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).
