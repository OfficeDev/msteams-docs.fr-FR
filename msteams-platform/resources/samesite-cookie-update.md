---
title: Attribut de cookie SameSite
author: laujan
description: décrit les attributs du cookie SameSite
keywords: samesite des attributs de cookie
ms.topic: reference
localization_priority: Normal
ms.author: lomeybur
ms.openlocfilehash: 78ac367ee550650fb9994676a8083a1b201a06086582161daba6ea4311d0aaeb
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/07/2021
ms.locfileid: "57708335"
---
# <a name="samesite-cookie-attribute"></a>Attribut de cookie SameSite 

Les cookies sont des chaînes de texte, envoyées à partir de sites web et stockées sur un ordinateur par le navigateur web. Ils sont utilisés pour l’authentification et la personnalisation. Par exemple, les cookies sont utilisés pour rappeler des informations avec état, conserver les paramètres utilisateur, enregistrer l’activité de navigation et afficher des publicités pertinentes. Les cookies sont toujours liés à un domaine particulier et sont installés par différentes parties. 

## <a name="types-of-cookies"></a>Types de cookies

Les types de cookies et leurs étendues correspondantes sont les suivants :

|Cookie|Portée|
| ------ | ------ |
|Cookie de première partie|Un cookie de première partie est créé par des sites web visités par un utilisateur. Il permet d’enregistrer des données, telles que des éléments de panier, des informations d’identification de connexion. Par exemple, les cookies d’authentification et d’autres analyses.|
|Cookie de deuxième partie|Un cookie tiers est techniquement identique à un cookie de première partie. La différence est que les données sont partagées avec une deuxième partie via un accord de partenariat de données. Par exemple, vous [Microsoft Teams analytique et de rapports.](/microsoftteams/teams-analytics-and-reports/teams-reporting-reference) |
|Cookie tiers|Un cookie tiers est installé par un domaine autre que celui que l’utilisateur a visité explicitement et est principalement utilisé pour le suivi. Par exemple, les **boutons** J’aime, la portion de la vidéo et les conversations en direct.|

## <a name="cookies-and-http-requests"></a>Cookies et requêtes HTTP

Avant l’introduction des restrictions SameSite, les cookies étaient stockés dans le navigateur. Ils ont été joints à chaque demande web HTTP et envoyés au serveur par l’en-tête `Set Cookie` de réponse HTTP. Cette méthode a introduit des vulnérabilités de sécurité, telles que la contrefaçon de demande de site croisé, appelée attaques CSRF. Le composant SameSite a réduit l’exposition via son implémentation et sa gestion dans l’en-tête SetCookie.

## <a name="samesite-cookie-attribute-initial-release"></a>Attribut de cookie SameSite : version initiale

Google Chrome version 51 a introduit la `SetCookie SameSite` spécification en tant qu’attribut facultatif. À partir de la build 17672, Windows 10 introduit la prise en charge des cookies SameSite [pour Microsoft Edge navigateur.](https://blogs.windows.com/msedgedev/2018/05/17/samesite-cookies-microsoft-edge-internet-explorer/)

Vous pouvez choisir de ne pas ajouter l’attribut de cookie SameSite à l’en-tête ou de l’ajouter avec l’un des deux `SetCookie` **paramètres, Lax** et **Strict**. Un attribut SameSite non implémenté était considéré comme l’état par défaut.

## <a name="samesite-cookie-attribute-2020-release"></a>Attribut de cookie SameSite : version 2020

Chrome 80, publié en février 2020, introduit de nouvelles valeurs de cookie et impose des stratégies de cookie par défaut. Trois valeurs sont passées dans l’attribut SameSite mis à jour : **Strict,** **Lax** ou **None**. S’il n’est pas spécifié, l’attribut SameSite des cookies prend la valeur `SameSite=Lax` par défaut.    
 
Les attributs de cookie SameSite sont les suivants :

|Paramètre | Application | Valeur |Spécification d’attribut |
| -------- | ----------- | --------|--------|
| **Lax**  | Les cookies sont envoyés automatiquement uniquement dans un contexte de première **partie** et avec des requêtes HTTP GET. Les cookies SameSite sont retenus sur les demandes de sous-sites, telles que les appels de chargement d’images ou d’iframes. Ils sont envoyés lorsqu’un utilisateur navigue vers l’URL à partir d’un site externe, par exemple, en suivant un lien.| **Par défaut** |`Set-Cookie: key=value; SameSite=Lax`|
| **Strict** |Le navigateur envoie uniquement des cookies pour les demandes de contexte de première partie. Ce sont des demandes provenant du site qui définissent le cookie. Si la demande provient d’une URL différente de celle de l’emplacement actuel, aucun des cookies marqués avec `Strict` l’attribut n’est envoyé.| Facultatif |`Set-Cookie: key=value; SameSite=Strict`|
| **Aucune** | Les cookies sont envoyés dans le contexte de première partie et les demandes d’origine croisée ; toutefois, la valeur doit être explicitement définie et toutes les demandes de navigateur doivent suivre le protocole HTTPS et inclure l’attribut qui nécessite une **`None`** connexion  **`Secure`** chiffrée. Les cookies qui ne respectent pas cette exigence sont **rejetés.** <br/>**Les deux attributs sont requis ensemble.** Si ce protocole est spécifié sans ou si le protocole HTTPS n’est pas utilisé, les cookies tiers  **`None`** **`Secure`**  sont rejetés.| Facultatif, mais, s’il est définie, le protocole HTTPS est requis. |`Set-Cookie: key=value; SameSite=None; Secure` |

## <a name="teams-implications-and-adjustments"></a>Teams et ajustements

1. Activez le paramètre SameSite pertinent pour vos cookies et validez que vos applications et extensions continuent de fonctionner Teams.
1. Si vos applications ou extensions échouent, corrigez les correctifs nécessaires avant la publication de Chrome 80.
1. Les partenaires internes de Microsoft peuvent rejoindre l’équipe suivante pour plus d’informations ou de l’aide sur ce <https://teams.microsoft.com/l/team/19%3A08b594cd465e4c0491fb751e823802e2%40thread.skype/conversations?groupId=4d6d04cd-dbf0-43c8-a2ff-f80dd38be034&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47> problème :

> [!NOTE]
> Vous devez définir des attributs SameSite pour refléter l’utilisation prévue pour vos cookies. Ne comptez pas sur le comportement par défaut du navigateur. Pour plus d’informations, [voir Développeurs : Se préparer pour new SameSite=None; Secure Cookie Paramètres](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html).

### <a name="tabs-task-modules-and-messaging-extensions"></a>Onglets, modules de tâche et extensions de messagerie

* Teams les onglets utilisés pour incorporer du contenu qui est vu dans un contexte `<iframes>` de niveau supérieur ou de première partie.
* Les modules de tâche vous permettent de créer des expériences de menu contextuel modal dans votre application Teams. Comme un onglet, une fenêtre modale s’ouvre à l’intérieur de la page actuelle.
* Les extensions de messagerie vous permettent d’insérer du contenu enrichi dans un message de conversation à partir de ressources externes.

Tous les cookies utilisés par le contenu incorporé sont considérés comme tiers lorsque le site est affiché dans un `<iframe>` . En outre, si des ressources distantes sur une page s’appuient sur les cookies envoyés avec une demande et des `<img>` balises, des polices externes et du contenu personnalisé, vous devez vous assurer qu’elles sont marquées pour une utilisation sur plusieurs sites, par exemple, ou vous assurer qu’un système de base est en `<script>` `SameSite=None; Secure` place.

### <a name="authentication"></a>Authentification

Vous devez utiliser le flux d’authentification basé sur le web pour les raisons suivantes :

* Pages de contenu incorporées dans les onglets.
* Page de configuration, module de tâche et extension de messagerie.
* Bot conversationnel avec un module de tâche.

En fonction des restrictions SameSite mises à jour, un navigateur n’ajoute pas de cookie à un site web déjà authentifié si le lien dérive d’un site externe. Vous devez vous assurer que vos cookies d’authentification sont marqués pour une utilisation sur plusieurs sites ou s’assurer qu’un système de `SameSite=None; Secure` base est en place.

## <a name="android-system-webview"></a>Android System WebView

Android WebView est un composant système Chrome qui permet aux applications Android d’afficher le contenu web. Bien que les nouvelles restrictions soient par défaut, à partir de Chrome 80, elles ne sont pas immédiatement appliquées sur les webViews. Elles seront appliquées à l’avenir. Pour se préparer, Android permet aux applications natives de définir des cookies directement via [l’API CookieManager.](https://developer.android.com/reference/android/webkit/CookieManager)

> [!NOTE]     
> * Vous devez déclarer les cookies de première partie `SameSite=Lax` en tant `SameSite=Strict` que ou, selon le cas.      
> * Vous devez déclarer des cookies tiers comme `SameSite=None; Secure` .   

## <a name="see-also"></a>Voir aussi

* [Exemples sameSite](https://github.com/GoogleChromeLabs/samesite-examples)
* [Recettes de cookie SameSite](https://web.dev/samesite-cookie-recipes/)
* [Clients incompatibles connus]( https://www.chromium.org/updates/same-site/incompatible-clients)
* [Développeurs : découvrez les nouveaux paramètres de cookies SameSite=None; Secure](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [Modifications à venir des cookies SameSite dans ASP.NET et ASP.NET Core](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)
* [Cookies HTTP](https://developer.mozilla.org/docs/Web/HTTP/Cookies)
