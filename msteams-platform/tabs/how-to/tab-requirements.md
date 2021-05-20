---
title: Comprendre les exigences de l’onglet
author: laujan
description: Chaque onglet dans Microsoft Teams doit respecter ces exigences.
keywords: équipes onglets canal de groupe configurable
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: a46a80401b29b5436807c9a5b94580beca3786f0
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566662"
---
# <a name="tab-requirements"></a>Conditions requises pour l’onglet

Teams onglets doivent respecter les exigences suivantes :

* Vous devez autoriser le service de vos pages d’onglets dans un iFrame, via des options X-Frame et/ou des en-têtes de réponse HTTP content-security-policy.
  * En-tête de jeu : `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`
  * Pour la compatibilité Internet Explorer 11, `X-Content-Security-Policy` ensemble ainsi.
  * Alternativement, réglez l’en-tête. `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/` Cet en-tête est déprécié mais toujours respecté par la plupart des navigateurs.
* En règle générale, en tant que protection contre le clic-jacking, les pages de connexion ne s’rendront pas dans iFrames. Par conséquent, votre logique d’authentification doit utiliser une méthode autre que la redirection. Par exemple, utilisez l’authentification basée sur les jetons ou les cookies.

> [!NOTE]
> Chrome 80, dont la sortie est prévue début 2020, introduit de nouvelles valeurs de cookies et impose des stratégies de cookies par défaut. Il est recommandé de définir l’utilisation prévue pour vos cookies plutôt que de compter sur le comportement par défaut du navigateur. Pour plus d’informations, voir [l’attribut cookie SameSite (mise à jour 2020).](../../resources/samesite-cookie-update.md)

* Les navigateurs adhèrent à une restriction de stratégie de même origine qui empêche une page Web de faire des demandes à un domaine différent de celui qui a servi une page Web. Toutefois, vous devrez peut-être rediriger la configuration ou la page de contenu vers un autre domaine ou sous-domaine. Votre logique de navigation inter-domaines doit permettre au client Teams de valider l’origine par rapport à une liste validDomains statique dans le manifeste de l’application lors du chargement ou de la communication avec l’onglet.

* Pour créer une expérience transparente, vous devez coiffer vos onglets en fonction du thème, de la conception et de l’intention du client Teams’utiliser. En règle générale, les onglets fonctionnent mieux lorsqu’ils sont conçus pour répondre à un besoin spécifique et se concentrer sur un petit ensemble de tâches ou un sous-ensemble de données qui est pertinent à l’emplacement du canal de l’onglet.

* Dans votre page de contenu, ajoutez une référence à [Microsoft Teams client JavaScript SDK à l’aide de](/javascript/api/overview/msteams-client) balises de script. Suite à la charge de votre page, faites un appel à `microsoftTeams.initialize()` . Votre page ne sera pas affichée si vous ne le faites pas.

* Pour que l’authentification fonctionne sur les clients mobiles, vous devez Teams javascript SDK à au moins la version 1.4.1.

* Si vous choisissez d’avoir votre onglet canal ou groupe sur Teams clients mobiles, `setSettings()` la configuration doit avoir une valeur pour la `websiteUrl` propriété.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créez un onglet personnel personnalisé à l’aide Node.js et du générateur Yeoman pour Microsoft Teams](~/tabs/quickstarts/create-personal-tab-node-yeoman.md)