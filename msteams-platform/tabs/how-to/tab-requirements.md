---
title: Conditions préalables
author: surbhigupta
description: Chaque onglet de Microsoft Teams doit respecter ces exigences.
keywords: Canal de groupe onglets teams configurable
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: fe72691465ca785cefb6a96c8eb4005a64601a17
ms.sourcegitcommit: 3dc9b539c6f7fbfb844c47a78e3b4d2200dabdad
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2022
ms.locfileid: "64571515"
---
# <a name="prerequisites"></a>Configuration requise

Veillez à respecter les conditions préalables suivantes lors de la création Teams onglet personnel et de canal ou de groupe :

* Autorisez la découverte de pages d’onglets dans un iFrame, à l’aide des en-têtes de réponse HTTP X-Frame-Options et Content-Security-Policy.
  * Définir l’en-tête : `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`
  * Pour la compatibilité d’Internet Explorer 11, définissez `X-Content-Security-Policy`.
  * Sinon, définissez l’en-tête `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/`. Cet en-tête est supprimé, mais toujours accepté par la plupart des navigateurs.

* Les pages de connexion ne s’restitueraient pas dans les iFrames, par mesure de protection contre les détournements de clics. Votre logique d’authentification doit utiliser une méthode autre que la redirection. Par exemple, utilisez l’authentification basée sur les jetons ou sur les cookies.

    > [!NOTE]
    > Il est recommandé de définir l’utilisation prévue pour vos cookies plutôt que de vous appuyer sur le comportement par défaut du navigateur. Pour plus d’informations, voir [l’attribut de cookie SameSite](../../resources/samesite-cookie-update.md).

* Les restrictions de stratégie de même origine des navigateurs empêchent les pages web d’effectuer des demandes vers des domaines différents de la page web servie. Ainsi, vous pouvez rediriger la page de configuration ou de contenu vers un autre domaine ou sous-domaine. Votre logique de navigation entre domaines doit permettre au client `validDomains` Teams de valider l’origine par rapport à une liste statique dans le manifeste de l’application lors du chargement ou de la communication avec l’onglet.

* Stylez vos onglets en fonction Teams thème, de la conception et de l’intention du client. Les onglets fonctionnent mieux lorsqu’ils sont créés pour répondre à un besoin spécifique et qu’ils se concentrent sur un petit ensemble de tâches ou un sous-ensemble de données pertinentes pour l’emplacement du canal de l’onglet.

* Dans votre page de contenu, ajoutez une référence Microsoft Teams [SDK client JavaScript](/javascript/api/overview/msteams-client) à l’aide de balises de script. Après le chargement de votre page, appelez-la `microsoftTeams.initialize()`, sinon votre page n’est pas affichée.

* Pour que l’authentification fonctionne sur les clients mobiles, vous devez mettre à niveau Teams JavaScript SDK 1.4.1 et version ultérieure.

* Si vous choisissez que votre onglet de canal ou de groupe s’affiche sur Teams client mobile, `setSettings()` la configuration doit avoir une valeur pour la `websiteUrl` propriété.

* Microsoft Teams’onglet ne prend pas en charge la possibilité de charger des sites web intranet qui utilisent des certificats auto-signés.

## <a name="tools-to-build-tabs"></a>Outils pour créer des onglets

| &nbsp; | Installer | Pour utiliser... |
| --- | --- | --- |
| **Obligatoire** | &nbsp; | &nbsp; |
| &nbsp; | [Node.js](https://nodejs.org/en/download/) | Environnement d’runtime JavaScript back-end. Utilisez la dernière version de LTS v14.|
| &nbsp; | [Microsoft Edge](https://www.microsoft.com/edge) (recommandé) ou [Google Chrome](https://www.google.com/chrome/) | Navigateur avec outils de développement. |
| &nbsp; | [Visual Studio Code](https://code.visualstudio.com/download) | JavaScript, TypeScript ou SharePoint Framework (SPFx) build. |
| &nbsp; | [Visual Studio 2019](https://visualstudio.com/download), **ASP.NET développement web**, ou charge de travail de **développement .NET Core sur plusieurs plateformes** | .NET. Vous pouvez installer l’édition communautaire gratuite de Visual Studio 2019. |
| &nbsp; | [Git](https://git-scm.com/downloads) | Git pour utiliser le référentiel d’exemples d’applications GitHub. |
| &nbsp; | [Microsoft Teams](https://www.microsoft.com/en-us/microsoft-teams/download-app) | Microsoft Teams collaborer avec tous les personnes avec qui vous travaillez via des applications de conversation, de réunions, d’appels, le tout au même endroit. |
| &nbsp; | [ngrok](https://ngrok.com/download) | Ngrok est un outil logiciel de proxy inverse. Ngrok crée un tunnel vers les points de terminaison HTTPS disponibles publiquement de votre serveur web exécutant localement. Les points de terminaison web de votre serveur sont disponibles pendant la session en cours sur votre ordinateur. Lorsque l’ordinateur est arrêté ou en veille, le service n’est plus disponible. |
| &nbsp; | [Documentation pour les développeurs](https://dev.teams.microsoft.com/) | Portail web pour configurer, gérer et distribuer votre application Teams y compris à votre organisation ou au Teams store. |

### <a name="build-your-teams-tab"></a>Créer votre onglet Teams de projet

Maintenant, nous allons créer votre onglet. Tout d’abord, sélectionnez votre choix d’onglet à créer :

> [!div class="nextstepaction"]
> [Créer un onglet personnel](~/tabs/how-to/create-personal-tab.md)
> [!div class="nextstepaction"]
> [Créer un onglet de canal ou de groupe](~/tabs/how-to/create-channel-group-tab.md)

## <a name="see-also"></a>Voir aussi

* [Teams onglets](~/tabs/what-are-tabs.md)
* [Onglets sur les appareils mobiles](~/tabs/design/tabs-mobile.md)