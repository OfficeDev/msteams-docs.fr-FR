---
title: Attribut de cookie SameSite
author: laujan
description: Apprenez à connaître les types de cookies, notamment les cookies SameSite, leurs attributs, leurs implications dans les onglets, les modules de tâches et les extensions de messages de Teams, ainsi que leur authentification dans Teams.
ms.topic: reference
ms.localizationpriority: medium
ms.author: lomeybur
ms.openlocfilehash: fee4855c8dd6c8dfdb83bce8b6d4d0c5da348724
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142730"
---
# <a name="samesite-cookie-attribute"></a>Attribut de cookie SameSite

Les cookies sont des chaînes de texte envoyées par les sites web et stockées sur un ordinateur par le navigateur web. Ils sont utilisés pour l’authentification et la personnalisation. Par exemple, les cookies sont utilisés pour rappeler des informations d'état, préserver les paramètres de l'utilisateur, enregistrer l'activité de navigation et afficher des publicités pertinentes. Les cookies sont toujours liés à un domaine particulier et sont installés par différentes parties.

## <a name="types-of-cookies"></a>Types de cookies

Les types de cookies et leurs étendues correspondantes sont les suivants :

|Cookie|Portée|
| ------ | ------ |
|Cookie de première partie|Un cookie de première partie est créé par les sites web qu’un utilisateur visite. Il est utilisé pour enregistrer des données, telles que des articles de panier d’achat, des informations d’identification de connexion. Par exemple, les cookies d’authentification et d’autres analyses.|
|Cookie de seconde partie|Un cookie de seconde partie est techniquement le même qu’un cookie de première partie. La différence réside dans le fait que les données sont partagées avec une deuxième partie par le biais d’un contrat de partenariat de données. Par exemple, [Analyses et rapports Microsoft Teams](/microsoftteams/teams-analytics-and-reports/teams-reporting-reference). |
|Cookie tierce partie|Un cookie tiers est installé par un domaine autre que celui que l’utilisateur a visité explicitement et est utilisé pour le suivi. Par exemple, les boutons **J’aime** les boutons, la diffusion de messages et les conversations en direct.|

## <a name="cookies-and-http-requests"></a>Cookies et requêtes HTTP

Avant l’introduction des restrictions SameSite, les cookies étaient stockés dans le navigateur. Ils ont été attachés à chaque requête web HTTP et envoyés au serveur par l’en-tête de `Set Cookie` réponse HTTP. Cette méthode a introduit des vulnérabilités en matière de sécurité, comme les attaques CSRF (Cross Site Request Forgery). Le composant SameSite a réduit l’exposition par son implémentation et sa gestion dans l’en-tête SetCookie.

## <a name="samesite-cookie-attribute-initial-release"></a>Attribut de cookie SameSite : version initiale

Google Chrome version 51 a introduit la `SetCookie SameSite` spécification en tant qu’attribut facultatif. À compter de la build 17672, Windows 10 introduit la prise en charge des cookies SameSite pour le [navigateur&nbsp;Microsoft Edge](https://blogs.windows.com/msedgedev/2018/05/17/samesite-cookies-microsoft-edge-internet-explorer/).

Vous pouvez refuser d’ajouter l’attribut de cookie SameSite à l’ `SetCookie` n-tête ou l’ajouter avec l’un des deux paramètres **, Lax** et **Strict**. Un attribut SameSite non implémenté a été considéré comme l’état par défaut.

## <a name="samesite-cookie-attribute-2020-release"></a>Attribut de cookie SameSite : version 2020

Chrome 80, publié en février 2020, introduit de nouvelles valeurs de cookie et impose des stratégies de cookie par défaut. Trois valeurs sont passées dans l’attribut SameSite actualisé : **Strict**, **Lax** ou **None**. L’attribut SameSite cookies prend la valeur `SameSite=Lax` par défaut s’il n’est pas spécifié.

Les attributs de cookie SameSite sont les suivants :

|Paramètre | Application | Valeur |Spécification d’attribut |
| -------- | ----------- | --------|--------|
| **Lax**  | Les cookies sont envoyés automatiquement uniquement dans un contexte **de première partie** et avec des requêtes HTTP GET. Les cookies SameSite sont retenus sur les sous-requêtes intersites, telles que les appels pour charger des images ou des iframes. Ils sont envoyés lorsqu’un utilisateur accède à l’URL à partir d’un site externe, par exemple, en suivant un lien.| **Par défaut** |`Set-Cookie: key=value; SameSite=Lax`|
| **Strict** |Le navigateur envoie uniquement des cookies pour les demandes de contexte de première partie. Il s’agit de requêtes provenant du site qui définissent le cookie. Si la requête provient d’une URL différente de celle de l’emplacement actuel, aucun des cookies marqués avec l’ `Strict`attribut n’est envoyé.| Facultatif |`Set-Cookie: key=value; SameSite=Strict`|
| **Aucune** | Les cookies sont envoyés dans le contexte de la première partie et dans les demandes d’origine croisée ; toutefois, la valeur doit être explicitement définie **`None`** et toutes les demandes de navigateur **doivent suivre le protocole HTTPS** et inclure l’attribut **`Secure`** , qui nécessite une connexion chiffrée. Les cookies qui ne respectent pas cette exigence sont **rejetés**. <br/>**Les deux attributs doivent être réunis**. S’il  **`None`** est spécifié sans **`Secure`**  ou si le protocole HTTPS n’est pas utilisé, les cookies tiers sont rejetés.| Facultatif, mais, s’il est défini, le protocole HTTPS est requis. |`Set-Cookie: key=value; SameSite=None; Secure` |

## <a name="teams-implications-and-adjustments"></a>Implications et ajustements de Teams

1. Activez le paramètre SameSite approprié pour vos cookies et vérifiez que vos applications et extensions continuent de fonctionner dans Teams.
1. Si vos applications ou extensions ne fonctionnent pas, apportez les corrections nécessaires avant la publication de Chrome 80.
1. Les partenaires internes de Microsoft peuvent rejoindre l'équipe suivante pour plus d'informations ou pour aider à résoudre ce problème : <https://teams.microsoft.com/l/team/19%3A08b594cd465e4c0491fb751e823802e2%40thread.skype/conversations?groupId=4d6d04cd-dbf0-43c8-a2ff-f80dd38be034&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47>.

> [!NOTE]
> Vous devez définir les attributs SameSite pour refléter l'utilisation prévue de vos cookies. Ne vous fiez pas au comportement par défaut du navigateur. Pour plus d'informations, [Développeurs : découvrez les nouveaux paramètres de cookies SameSite=None; Secure](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html).

### <a name="tabs-task-modules-and-message-extensions"></a>Onglets, modules de tâches et extensions de messages

* Les onglets Teams permettent `<iframes>` d'intégrer du contenu affiché à un niveau supérieur ou dans un contexte de première partie.
* Les modules de tâches vous permettent de créer des expériences de menu contextuel modal dans votre application Teams. À l’instar d’un onglet, une fenêtre modale s’ouvre à l’intérieur de la page active.
* Les extensions de message vous permettent d’insérer du contenu enrichi dans un message de conversation à partir de ressources externes.

Tous les cookies utilisés par le contenu incorporé sont considérés comme tierce partie lorsque le site est affiché dans un `<iframe>`. En outre, si des ressources distantes d’une page s’appuient sur des cookies envoyés avec une requête `<img>` et `<script>` des balises, des polices externes et du contenu personnalisé, vous devez vous assurer que celles-ci sont marquées pour une utilisation intersites, par exemple `SameSite=None; Secure` ou assurez-vous qu’une solution de secours est en place.

### <a name="authentication"></a>Authentification

Vous devez utiliser le flux d’authentification web pour les éléments suivants :

* Intégration de pages de contenu dans les onglets.
* Page de configuration, module de tâche et extension de message.
* Bot conversationnel avec un module de tâche.

Selon les restrictions SameSite mises à jour, un navigateur n’ajoute pas de cookie à un site web déjà authentifié si le lien dérive d’un site externe. Vous devez vous assurer que vos cookies d’authentification sont marqués pour une utilisation `SameSite=None; Secure` intersite ou vérifier qu’une solution de remplacement est en place.

## <a name="android-system-webview"></a>Système Android WebView

Android WebView est un composant du système Chrome qui permet aux applications Android d'afficher le contenu web. Bien que les nouvelles restrictions soient par défaut, à compter de Chrome 80, elles ne sont pas appliquées immédiatement sur webViews. Ils seront appliqués à l’avenir. Pour se préparer, Android permet aux applications natives de définir des cookies directement via [l’API CookieManager](https://developer.android.com/reference/android/webkit/CookieManager).

> [!NOTE]
>
> * Vous devez déclarer les cookies internes comme `SameSite=Lax` ou `SameSite=Strict`, le cas échéant.
> * Vous devez déclarer des cookies tierce partie en tant que `SameSite=None; Secure`.

## <a name="see-also"></a>Voir aussi

* [Exemples SameSite](https://github.com/GoogleChromeLabs/samesite-examples)
* [Recettes de cookie SameSite](https://web.dev/samesite-cookie-recipes/)
* [Clients incompatibles connus]( https://www.chromium.org/updates/same-site/incompatible-clients)
* [Développeurs : découvrez les nouveaux paramètres de cookies SameSite=None; Secure](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [Modifications à venir des cookies SameSite dans ASP.NET et ASP.NET Core](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)
* [Cookies HTTP](https://developer.mozilla.org/docs/Web/HTTP/Cookies)
