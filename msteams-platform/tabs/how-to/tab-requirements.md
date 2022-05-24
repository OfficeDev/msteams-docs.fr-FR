---
title: Conditions préalables
author: surbhigupta
description: Chaque onglet de Microsoft Teams doit respecter ces exigences.
keywords: canal de groupe des onglets Teams configurable
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: ca9b4d073a324c3cbf1d2d087bec8d366faf0830
ms.sourcegitcommit: 80edf3c964bb47a2ee13f9eda4334ad19e21f331
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/24/2022
ms.locfileid: "65654893"
---
# <a name="prerequisites"></a>Configuration requise

Veillez à respecter les conditions préalables suivantes lors de la création de votre onglet de groupe ou de canal et Teams personnel :

* Autorisez la découverte des pages de votre onglet dans un iFrame à l’aide des en-têtes de réponse HTTP X-Frame-Options et Content-Security-Policy.
  * Définir l’en-tête : `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`
  * Pour la compatibilité d’Internet Explorer 11, définissez `X-Content-Security-Policy`.
  * Vous pouvez également définir l’en-tête `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/`. Cet en-tête est déconseillé, mais il est toujours accepté par la plupart des navigateurs.

* Les pages de connexion ne s’affichent pas dans les iFrames, en tant que dispositif de protection contre le détournement de clic. Votre logique d’authentification doit utiliser une méthode autre que la redirection. Par exemple, utilisez l’authentification basée sur les jetons ou sur les cookies.

    > [!NOTE]
    > Il est recommandé de définir l’utilisation prévue pour vos cookies plutôt que de vous appuyer sur le comportement du navigateur par défaut. Pour plus d’informations, consultez [Attribut de cookie SameSite](../../resources/samesite-cookie-update.md).

* La même restriction de stratégie d’origine des navigateurs empêche les pages web d’effectuer des requêtes vers des domaines autres que ceux de la page web servie. Vous pouvez donc rediriger la page de configuration ou de contenu vers un autre domaine ou sous-domaine. Votre logique de navigation inter-domaines doit permettre au client Teams de valider l’origine par rapport à une liste statique `validDomains` dans le manifeste de l’application lors du chargement ou de la communication avec l’onglet.

* Stylisez vos onglets en fonction du thème, de la conception et de l’intention du client Teams. Les onglets fonctionnent mieux lorsqu’ils sont conçus pour répondre à un besoin spécifique et se concentrer sur un petit ensemble de tâches ou un sous-ensemble de données pertinent pour l’emplacement du canal de l’onglet.

* Dans votre page de contenu, ajoutez une référence au [Kit de développement logiciel (SDK) client JavaScript Microsoft Teams](/javascript/api/overview/msteams-client) à l’aide de balises de script. Une fois votre page chargée, appelez `microsoftTeams.initialize()`, sinon votre page ne s’affiche pas.

* Pour que l’authentification fonctionne sur des clients mobiles, vous devez effectuer une mise à niveau vers Kit de développement logiciel (SDK) JavaScript Microsoft Teams 1.4.1 et versions ultérieures.

* Si vous choisissez d’afficher l’onglet de votre canal ou de votre groupe sur un client mobile Teams, la configuration `setSettings()` doit avoir une valeur pour la propriété `websiteUrl`.

* L’onglet Microsoft Teams ne prend pas en charge la possibilité de charger des sites web intranet qui utilisent des certificats auto-signés.

## <a name="tools-to-build-tabs"></a>Outils pour créer des onglets

| &nbsp; | Installer | Pour l’utilisation... |
| --- | --- | --- |
| **Obligatoire** | &nbsp; | &nbsp; |
| &nbsp; | [Node.js](https://nodejs.org/en/download/) | Environnement runtime JavaScript principal. Utilisez la dernière version de LTS v16.|
| &nbsp; | [Microsoft Edge](https://www.microsoft.com/edge) (recommandé) ou [Google Chrome](https://www.google.com/chrome/) | Un navigateur avec des outils de développement. |
| &nbsp; | [Visual Studio Code](https://code.visualstudio.com/download) | Environnements de build JavaScript, TypeScript ou SharePoint Framework (SPFx). |
| &nbsp; | [Visual Studio 2019](https://visualstudio.com/download), **ASP.NET et le développement web** ou la charge de travail **de développement multiplateforme .NET Core** | .NET. Vous pouvez installer l’édition communauté gratuite de Visual Studio 2019. |
| &nbsp; | [Git](https://git-scm.com/downloads) | Git pour utiliser le référentiel d’exemples d’applications de GitHub. |
| &nbsp; | [Microsoft Teams](https://www.microsoft.com/en-us/microsoft-teams/download-app) | Microsoft Teams pour collaborer avec toutes les personnes avec lesquelles vous travaillez via les applications pour les conversations, les réunions, les appels, le tout au même endroit. |
| &nbsp; | [ngrok](https://ngrok.com/download) | Ngrok est un outil logiciel de proxy inverse. Ngrok crée un tunnel vers les points de terminaison HTTPS disponibles publiquement de votre serveur web local en cours d’exécution. Les points de terminaison web de votre serveur sont disponibles pendant la session active sur votre ordinateur. Lorsque l’ordinateur est arrêté ou mis en veille, le service n’est plus disponible. |
| &nbsp; | [Documentation pour les développeurs](https://dev.teams.microsoft.com/) | Portail web pour configurer, gérer et distribuer votre application Teams, y compris à votre organisation ou au magasin Teams. |

### <a name="build-your-teams-tab"></a>Créer votre onglet Teams

Nous allons maintenant créer votre onglet. Toutefois, sélectionnez d’abord votre choix d’onglet à créer :

> [!div class="nextstepaction"]
> [Créer un onglet personnel](~/tabs/how-to/create-personal-tab.md)
> [!div class="nextstepaction"]
> [Créer un onglet de canal ou de groupe](~/tabs/how-to/create-channel-group-tab.md)

## <a name="see-also"></a>Voir aussi

* [Onglets Teams](~/tabs/what-are-tabs.md)
* [Onglets sur les appareils mobiles](~/tabs/design/tabs-mobile.md)