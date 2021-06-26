---
title: Conditions préalables
author: surbhigupta
description: Chaque onglet de Microsoft Teams doit respecter ces exigences.
keywords: Canal de groupe onglets teams configurable
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: b54fc7235132a9253f6eecc62417f786bf4aa45c
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140186"
---
# <a name="prerequisites"></a>Conditions préalables

Teams onglets doivent respecter les conditions préalables suivantes :

* Vous devez permettre à vos pages d’onglets d’être affichées dans un iFrame, à l’aide des en-têtes de réponse HTTP X-Frame-Options et Content-Security-Policy.
  * Définissez l’en-tête : `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`
  * Pour la compatibilité d’Internet Explorer 11, définissez `X-Content-Security-Policy` .
  * Sinon, définissez l’en-tête `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/` . Cet en-tête est supprimé, mais toujours accepté par la plupart des navigateurs.

* En règle générale, comme protection contre le détournement de clic, les pages de connexion ne s’restituer dans les iFrames. Votre logique d’authentification doit utiliser une méthode autre que la redirection. Par exemple, utilisez l’authentification basée sur les jetons ou sur les cookies.

    > [!NOTE]
    > Chrome 80, dont la publication est prévue début 2020, introduit de nouvelles valeurs de cookie et impose des stratégies de cookie par défaut. Il est recommandé de définir l’utilisation prévue pour vos cookies plutôt que de vous appuyer sur le comportement par défaut du navigateur. Pour plus d’informations, voir [l’attribut de cookie SameSite.](../../resources/samesite-cookie-update.md)

* Les navigateurs adhèrent à une restriction de stratégie de même origine. Cela empêche les pages web d’effectuer des demandes à des domaines différents de la page web servie. Toutefois, vous pouvez rediriger la page de configuration ou de contenu vers un autre domaine ou sous-domaine. Votre logique de navigation entre domaines doit permettre au client Teams de valider l’origine par rapport à une liste statique dans le manifeste de l’application lors du chargement ou de la communication avec `validDomains` l’onglet.

* Vous devez mettre en forme vos onglets en fonction Teams thème, de la conception et de l’intention du client. En règle générale, les onglets fonctionnent mieux lorsqu’ils sont conçus pour répondre à un besoin spécifique et qu’ils se concentrent sur un petit ensemble de tâches ou un sous-ensemble de données pertinents pour l’emplacement du canal de l’onglet.

* Dans votre page de contenu, ajoutez une référence Microsoft Teams [SDK client JavaScript à](/javascript/api/overview/msteams-client) l’aide de balises de script. Après le chargement de votre page, appelez-la, `microsoftTeams.initialize()` sinon votre page n’est pas affichée.

* Pour que l’authentification fonctionne sur les clients mobiles, vous devez mettre à niveau Teams SDK JavaScript vers au moins la version 1.4.1.

* Si vous choisissez que votre onglet de canal ou de groupe s’affiche sur Teams clients mobiles, la configuration doit avoir une valeur `setSettings()` pour la `websiteUrl` propriété.

* L’onglet Teams MS ne prend pas en charge la possibilité de charger des sites web intranet qui utilisent des certificats auto-signés.

## <a name="see-also"></a>Voir aussi

* [Teams onglets](~/tabs/what-are-tabs.md)
* [Créer un onglet de canal ou de groupe](~/tabs/how-to/create-channel-group-tab.md)
* [Créer une page de contenu](~/tabs/how-to/create-tab-pages/content-page.md)
* [Créer une page de configuration](~/tabs/how-to/create-tab-pages/configuration-page.md)
* [Créer une page de suppression pour votre onglet](~/tabs/how-to/create-tab-pages/removal-page.md)
* [Onglets sur les appareils mobiles](~/tabs/design/tabs-mobile.md)
* [Obtenir un contexte Teams pour votre onglet](~/tabs/how-to/access-teams-context.md)
* [Créer des onglets avec les Cartes adaptatives](~/tabs/how-to/build-adaptive-card-tabs.md)
* [Déploiement du lien des onglets et vue des étapes](~/tabs/tabs-link-unfurling.md)
* [Créer des onglets de conversation](~/tabs/how-to/conversational-tabs.md)
* [Modifications des marges de l’onglet](~/resources/removing-tab-margins.md)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créer un onglet personnel](~/tabs/how-to/create-personal-tab.md)
