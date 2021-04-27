---
title: Comprendre les conditions requises pour les onglets
author: laujan
description: Chaque onglet de Microsoft Teams doit respecter ces exigences.
keywords: Canal de groupe onglets teams configurable
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 8013c10050ae81ada0f2a27576cd43077eafe1e0
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019579"
---
# <a name="tab-requirements"></a>Conditions requises pour l’onglet

Les onglets Teams doivent respecter les exigences suivantes :

* Vous devez autoriser les pages d'onglets à être servies dans un iFrame, via des en-têtes de réponse HTTP X-Frame-Options et/ou Content-Security-Policy.
  * Définissez l'en-tête : `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`
  * Pour la compatibilité d'Internet Explorer 11, `X-Content-Security-Policy` définissez également.
  * Vous pouvez également définir l'en-tête `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/` . Cet en-tête est déprécié mais toujours respecté par la plupart des navigateurs.
* En règle générale, comme protection contre la prise de clic, les pages de connexion ne s'restitueraient pas dans les iFrames. Par conséquent, votre logique d'authentification doit utiliser une méthode autre que la redirection (par exemple, utiliser l'authentification basée sur les jetons ou l'authentification basée sur les cookies).

> [!NOTE]
> Chrome 80, dont la publication est prévue début 2020, introduit de nouvelles valeurs de cookie et impose des stratégies de cookie par défaut. Il est recommandé de définir l'utilisation prévue pour vos cookies plutôt que de vous appuyer sur le comportement par défaut du navigateur. *Voir* [l'attribut de cookie SameSite (mise à jour 2020).](../../resources/samesite-cookie-update.md)

* Les navigateurs adhèrent à une restriction de stratégie de même origine qui empêche une page web d'effectuer des demandes vers un domaine différent de celui qui a servi une page web. Toutefois, vous devrez peut-être rediriger la page de configuration ou de contenu vers un autre domaine ou sous-domaine. Votre logique de navigation entre domaines doit permettre au client Teams de valider l'origine par rapport à une liste validDomains statique dans le manifeste de l'application lors du chargement ou de la communication avec l'onglet.

* Pour créer une expérience transparente, vous devez donner un style à vos onglets en fonction du thème, de la conception et de l'intention du client Teams. En règle générale, les onglets fonctionnent mieux lorsqu'ils sont conçus pour répondre à un besoin spécifique et qu'ils se concentrent sur un petit ensemble de tâches ou un sous-ensemble de données pertinents pour l'emplacement du canal de l'onglet.

* Dans votre page de contenu, ajoutez une référence au [SDK client JavaScript Microsoft Teams](/javascript/api/overview/msteams-client) à l'aide de balises de script. Après le chargement de votre page, appelez `microsoftTeams.initialize()` . Votre page ne s'affichera pas si vous ne le faites pas.

* Pour que l'authentification fonctionne sur les clients mobiles, vous devez mettre à niveau le SDK JavaScript teams vers la version 1.4.1 au minimum.

* Si vous choisissez que votre onglet de canal ou de groupe apparaisse sur les clients mobiles Teams, la configuration doit avoir une valeur `setSettings()` pour la `websiteUrl` propriété.