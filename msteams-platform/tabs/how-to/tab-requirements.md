---
title: Conditions préalables
author: surbhigupta
description: Chaque onglet de Microsoft Teams doit respecter ces exigences.
keywords: Canal de groupe onglets teams configurable
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: lajanuar
---

# <a name="prerequisites"></a>Conditions préalables

Teams onglets doivent respecter les conditions préalables suivantes :

* Vous devez permettre à vos pages d’onglets d’être affichées dans un iFrame, à l’aide des en-têtes de réponse HTTP X-Frame-Options et Content-Security-Policy.
  * Définir l’en-tête : `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`
  * Pour la compatibilité d’Internet Explorer 11, définissez `X-Content-Security-Policy`.
  * Sinon, définissez l’en-tête `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/`. Cet en-tête est supprimé, mais toujours accepté par la plupart des navigateurs.

* En règle générale, comme protection contre les détournements de clics, les pages de connexion ne s’restitueraient pas dans les iFrames. Votre logique d’authentification doit utiliser une méthode autre que la redirection. Par exemple, utilisez l’authentification basée sur les jetons ou sur les cookies.

    > [!NOTE]
    > Chrome 80, dont la publication est prévue début 2020, introduit de nouvelles valeurs de cookie et impose des stratégies de cookie par défaut. Il est recommandé de définir l’utilisation prévue pour vos cookies plutôt que de vous appuyer sur le comportement par défaut du navigateur. Pour plus d’informations, voir [l’attribut de cookie SameSite](../../resources/samesite-cookie-update.md).

* Les navigateurs adhèrent à une restriction de stratégie de même origine. Cela empêche les pages web d’effectuer des demandes à des domaines différents de la page web servie. Toutefois, vous pouvez rediriger la page de configuration ou de contenu vers un autre domaine ou sous-domaine. Votre logique de navigation entre domaines doit permettre au client Teams de `validDomains` valider l’origine par rapport à une liste statique dans le manifeste de l’application lors du chargement ou de la communication avec l’onglet.

* Vous devez mettre en forme vos onglets en fonction Teams thème, de la conception et de l’intention du client. En règle générale, les onglets fonctionnent mieux lorsqu’ils sont conçus pour répondre à un besoin spécifique et qu’ils se concentrent sur un petit ensemble de tâches ou un sous-ensemble de données pertinentes pour l’emplacement du canal de l’onglet.

* Dans votre page de contenu, ajoutez une référence [Microsoft Teams SDK client JavaScript](/javascript/api/overview/msteams-client) à l’aide de balises de script. Après le chargement de votre page, appelez-la `microsoftTeams.initialize()`, sinon votre page n’est pas affichée.

* Pour que l’authentification fonctionne sur les clients mobiles, vous devez mettre à niveau Teams SDK JavaScript vers au moins la version 1.4.1.

* Si vous choisissez que votre onglet de canal ou de groupe s’affiche sur Teams clients mobiles, `setSettings()` la configuration doit avoir une valeur pour la `websiteUrl` propriété.

* L’onglet Teams MS ne prend pas en charge la possibilité de charger des sites web intranet qui utilisent des certificats auto-signés.

## <a name="tools-you-can-use-to-build-tabs"></a>Outils que vous pouvez utiliser pour créer des onglets
* [Teams Shared Computer Toolkit for Microsoft Visual Studio Code](../../toolkit/visual-studio-code-overview.md)
* [Extension de kit de ressources Teams pour Visual Studio](../../toolkit/visual-studio-overview.md)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créer un onglet personnel](~/tabs/how-to/create-personal-tab.md)

## <a name="see-also"></a>Voir aussi

* [Teams onglets](~/tabs/what-are-tabs.md)
* [Créer votre première application à l’aide de JavaScript](../../get-started/first-app-react.md)
* [Créer votre première application à l’aide de SPFx](../../get-started/first-app-spfx.md)
* [Onglets sur les appareils mobiles](~/tabs/design/tabs-mobile.md)
