---
title: Comprendre les conditions requises pour les onglets
author: laujan
description: Chaque onglet de Microsoft Teams doit respecter ces exigences.
keywords: Canal de groupe onglets teams configurable
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: f45bfc8831eb6dca660df3307bf875b7ad9fbf1e
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630403"
---
# <a name="tab-requirements"></a>Conditions requises pour l’onglet

Teams onglets doivent respecter les exigences suivantes :

* Vous devez autoriser les pages d’onglets à être servies dans un iFrame, via des en-têtes de réponse HTTP X-Frame-Options et/ou Content-Security-Policy.
  * Définissez l’en-tête : `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`
  * Pour la compatibilité d’Internet Explorer 11, `X-Content-Security-Policy` définissez également.
  * Vous pouvez également définir l’en-tête `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/` . Cet en-tête est déprécié mais toujours respecté par la plupart des navigateurs.
* En règle générale, comme protection contre le clic, les pages de connexion ne s’restitueraient pas dans les iFrames. Par conséquent, votre logique d’authentification doit utiliser une méthode autre que la redirection. Par exemple, utilisez l’authentification basée sur les jetons ou sur les cookies.

> [!NOTE]
> Chrome 80, dont la publication est prévue début 2020, introduit de nouvelles valeurs de cookie et impose des stratégies de cookie par défaut. Il est recommandé de définir l’utilisation prévue pour vos cookies plutôt que de vous appuyer sur le comportement par défaut du navigateur. Pour plus d’informations, voir Attribut de cookie SameSite (mise à jour [2020).](../../resources/samesite-cookie-update.md)

* Les navigateurs adhèrent à une restriction de stratégie de même origine qui empêche une page web d’effectuer des demandes à un domaine différent de celui qui a servi une page web. Toutefois, vous devrez peut-être rediriger la page de configuration ou de contenu vers un autre domaine ou sous-domaine. Votre logique de navigation entre domaines doit permettre au client Teams de valider l’origine par rapport à une liste validDomains statique dans le manifeste de l’application lors du chargement ou de la communication avec l’onglet.

* Pour créer une expérience transparente, vous devez donner un style à vos onglets en fonction Teams thème, de la conception et de l’intention du client. En règle générale, les onglets fonctionnent mieux lorsqu’ils sont conçus pour répondre à un besoin spécifique et qu’ils se concentrent sur un petit ensemble de tâches ou un sous-ensemble de données pertinents pour l’emplacement du canal de l’onglet.

* Dans votre page de contenu, ajoutez une référence Microsoft Teams [SDK client JavaScript à](/javascript/api/overview/msteams-client) l’aide de balises de script. Après le chargement de votre page, appelez `microsoftTeams.initialize()` . Votre page ne s’affichera pas si vous ne le faites pas.

* Pour que l’authentification fonctionne sur les clients mobiles, vous devez mettre à niveau Teams SDK JavaScript vers au moins la version 1.4.1.

* Si vous choisissez que votre onglet de canal ou de groupe s’affiche sur Teams clients mobiles, la configuration doit avoir une valeur `setSettings()` pour la `websiteUrl` propriété.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créer un onglet personnel personnalisé à l'Node.js et le générateur Yeoman pour Microsoft Teams](~/tabs/quickstarts/create-personal-tab-node-yeoman.md)
