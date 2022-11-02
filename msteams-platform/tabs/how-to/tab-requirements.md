---
title: Conditions préalables
author: surbhigupta
description: Dans cet article, découvrez les prérequis pour créer un onglet personnel, canal ou groupe Microsoft Teams. Connaître les outils nécessaires pour créer votre onglet.
ms.localizationpriority: high
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 4471d88b7f9b0fd6364c833f6b3dd910aadb300a
ms.sourcegitcommit: 9ea9a70d2591bce6b8c980d22014e160f7b45f91
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/02/2022
ms.locfileid: "68819960"
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

* Dans votre page de contenu, ajoutez une référence au [Kit de développement logiciel (SDK) client JavaScript Microsoft Teams](/javascript/api/overview/msteams-client) à l’aide de balises de script. Une fois votre page chargée, appelez `app.initialize()`, sinon votre page ne s’affichera pas.

* Pour que l’authentification fonctionne sur des clients mobiles, vous devez effectuer une mise à niveau vers Kit de développement logiciel (SDK) JavaScript Microsoft Teams 1.4.1 et versions ultérieures.

* Si vous choisissez d’afficher l’onglet de votre canal ou de votre groupe sur un client mobile Teams, la configuration `setConfig()` doit avoir une valeur pour la propriété `websiteUrl`.

* L’onglet Microsoft Teams ne prend pas en charge la possibilité de charger des sites web intranet qui utilisent des certificats auto-signés.

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

## <a name="tools-to-build-tabs"></a>Outils pour créer des onglets

| &nbsp; | Installer | Pour l’utilisation... |
| --- | --- | --- |
| **Obligatoire** | &nbsp; | &nbsp; |
| &nbsp; | [Node.js](https://nodejs.org/en/download/) | Environnement runtime JavaScript principal. Utilisez la dernière version v16 LTS.|
| &nbsp; | [Microsoft Edge](https://www.microsoft.com/edge) (recommandé) ou [Google Chrome](https://www.google.com/chrome/) | Un navigateur avec des outils de développement. |
| &nbsp; | [Visual Studio Code](https://code.visualstudio.com/download) | Environnements de build JavaScript, TypeScript ou SharePoint Framework (SPFx). |
| &nbsp; | [Visual Studio 2022](https://visualstudio.microsoft.com), **développement ASP.NET et web**, ou charge de travail développement **multiplateforme .NET Core** | .NET. Vous pouvez installer l’édition community gratuite de Visual Studio 2022. |
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

* [Créer des onglets pour Teams](../what-are-tabs.md)
* [Créer votre première application d’onglet à l’aide de JavaScript](../../sbs-gs-javascript.yml)
* [Inscrire votre application d’onglet dans Azure AD](authentication/tab-sso-register-aad.md)
* [Onglets sur les appareils mobiles](~/tabs/design/tabs-mobile.md)
