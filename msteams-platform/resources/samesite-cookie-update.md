---
title: Microsoft Teams et l'attribut de cookie SameSite (mise à jour 2020)
author: laujan
description: décrit les attributs du cookie SameSite
keywords: samesite des attributs de cookie
ms.topic: reference
localization_priority: Normal
ms.author: lomeybur
ms.openlocfilehash: 5713c7aae0461e577627ae7296f0a58a25ba062f
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020435"
---
# <a name="microsoft-teams-and-the-samesite-cookie-attribute-2020-update"></a>Microsoft Teams et l'attribut de cookie SameSite (mise à jour 2020)

## <a name="cookies-in-brief"></a>Cookies en bref

 Les cookies sont des chaînes de texte, envoyées à partir de sites web et stockées sur un ordinateur par le navigateur web. Ils sont généralement utilisés pour l'authentification et la personnalisation, par exemple, pour rappeler des informations avec état, préserver les paramètres utilisateur, enregistrer l'activité de navigation et afficher des publicités pertinentes. Les cookies sont toujours liés à un domaine particulier et peuvent être installés par différentes parties. Elles sont classées comme suit :

 |Cookie|Portée|
 | ------ | ------ |
 |**Cookie de première partie**|Un cookie de première partie est créé par des sites web visités par un utilisateur et utilisé pour enregistrer des données telles que des éléments de panier, des informations d'identification de connexion (par exemple, des cookies d'authentification) et d'autres analyses.|
 |**Cookie tiers**|Un cookie tiers est techniquement identique à un cookie de première partie. La différence est que les données sont partagées avec une deuxième partie via un accord de partenariat de données (par exemple, analyse et rapports [Microsoft Teams).](/microsoftteams/teams-analytics-and-reports/teams-reporting-reference) |
 |**Cookie tiers**|Un cookie tiers est installé par un domaine autre que celui que l'utilisateur a visité explicitement et est principalement utilisé pour le suivi (par exemple, boutons « J'aime », service de la vidéo et conversations en direct).|

### <a name="cookies-and-http-requests"></a>Cookies et requêtes HTTP

Avant l'introduction des restrictions SameSite, lorsque les cookies étaient stockés sur le navigateur, ils étaient joints à chaque demande web *HTTP* et envoyés au serveur par l'en-tête de réponse HTTP Set-Cookie. De manière prévisible, ces performances avaient le potentiel d'introduire des vulnérabilités de sécurité telles que les attaques de contrefaçon de demande entre sites (CSRF). *Voir* [cookies HTTP.](https://developer.mozilla.org/docs/Web/HTTP/Cookies) Le composant SameSite a atténué cette exposition par le biais de son implémentation et de sa gestion dans l'en-tête SetCookie.

### <a name="samesite-attribute-initial-release"></a>Attribut SameSite : version initiale

Google Chrome version 51 a introduit la spécification SetCookie SameSite en tant *qu'attribut facultatif.* À partir de la build 17672, Windows 10 a introduit la prise en charge des cookies SameSite pour le [navigateur Microsoft Edge.](https://blogs.windows.com/msedgedev/2018/05/17/samesite-cookies-microsoft-edge-internet-explorer/)

Les développeurs pouvaient refuser d'ajouter l'attribut de cookie SameSite à l'en-tête SetCookie ou l'ajouter avec l'un des deux paramètres, *Lax* et *Strict*. Un attribut SameSite non implémenté était considéré comme l'état par défaut.

## <a name="samesite-cookie-attribute-2020-release"></a>Attribut de cookie SameSite : version 2020

Chrome 80, dont la publication est prévue en février 2020, introduit de nouvelles valeurs de cookie et impose des stratégies de cookie par défaut. Trois valeurs peuvent être passées dans l'attribut SameSite mis à jour : *Strict,* *Lax* ou *None*. Les cookies qui ne spécifient pas l'attribut SameSite seront par `SameSite=Lax` défaut .

|Paramètre | Application | Valeur |Spécification d'attribut |
| -------- | ----------- | --------|--------|
| **Lax**  | Les cookies sont envoyés  automatiquement uniquement dans un contexte de première partie et avec des requêtes HTTP GET. Les cookies SameSite sont retenus sur les sous-demandes entre sites, telles que les appels de chargement d'images ou d'iframes, mais sont envoyés lorsqu'un utilisateur navigue vers l'URL à partir d'un site externe, par exemple, en suivant un lien.| **Par défaut** |`Set-Cookie: key=value; SameSite=Lax`|
| **Strict** |Le navigateur envoie uniquement les cookies pour les demandes de contexte de première partie (demandes provenant du site qui a définie le cookie). Si la demande provient d'une URL différente de celle de l'emplacement actuel, aucun des cookies marqués avec l'attribut `Strict` n'est envoyé.| Facultatif |`Set-Cookie: key=value; SameSite=Strict`|
| **Aucune** | Les cookies sont envoyés à la fois dans le contexte de la première partie et dans les demandes d'origine croisée . toutefois, la valeur doit être explicitement définie et toutes les demandes de navigateur doivent suivre le protocole HTTPS et inclure l'attribut qui nécessite une **`None`** connexion  **`Secure`** chiffrée. Les cookies qui ne respectent pas cette exigence seront **rejetés.** <br/>**Les deux attributs sont requis ensemble.** Si le protocole HTTPS n'est pas utilisé ou s'il est simplement spécifié, le cookie tiers **`None`** **`Secure`**  est rejeté.| Facultatif, mais, s'il est définie, le protocole HTTPS est requis. |`Set-Cookie: key=value; SameSite=None; Secure` |

## <a name="handling-incompatible-clients"></a>Gestion des clients incompatibles

> [!IMPORTANT]
> Actuellement, n'est pas pris en charge par le client de bureau Teams ou les versions antérieures `SameSite=None` de Chrome ou Safari. [](/aspnet/core/security/samesite?view=aspnetcore-3.1#test-with-electron&preserve-view=true) **Voir Clients** [incompatibles connus.]( https://www.chromium.org/updates/same-site/incompatible-clients)
>Toutefois, il existe deux **solutions de contournement**:
>
>1. Vérifiez l'agent utilisateur afin de fournir la propriété SameSite correcte. Vous pouvez implémenter la vérification de l'agent utilisateur [**dans C#**](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/) et [**Node.js**](https://web.dev/samesite-cookie-recipes/).
>2. Définissez vos attributs de cookie à l'aide des modèles nouveaux et anciens. *Voir Gestion* [des clients incompatibles](https://web.dev/samesite-cookie-recipes/#handling-incompatible-clients)<br><br>
>**Si votre application s'exécute dans le client de bureau Teams et que vous définissez l'attribut SameSite sur , votre application ne fonctionne `SameSite=None` pas comme prévu.**

L'utilisation de l'une ou l'autre approche garantit que votre application continue de fonctionner correctement lorsque le client de bureau Teams est mis à niveau vers une `SameSite=None`   version compatible de Chromium.

## <a name="teams-implications-and-adjustments"></a>Implications et ajustements de Teams

>[!WARNING]
>**Les applications en cours d'exécution dans le client de bureau Teams sont incompatibles avec l'attribut et ne `SameSite=None`  fonctionneront pas comme prévu.** Voir les **solutions de contournement** ci-dessus.

1. Activez le paramètre SameSite pertinent pour vos cookies et validez que vos applications et extensions continuent de fonctionner dans Teams.
1. Si vos applications ou extensions échouent, corrigez les correctifs nécessaires avant la publication de Chrome 80.
1. Les partenaires internes de Microsoft peuvent rejoindre l'équipe suivante s'ils ont besoin d'informations supplémentaires ou d'aide sur ce problème <https://teams.microsoft.com/l/team/19%3A08b594cd465e4c0491fb751e823802e2%40thread.skype/conversations?groupId=4d6d04cd-dbf0-43c8-a2ff-f80dd38be034&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47> :

> [!NOTE]
> Il est recommandé de toujours définir des attributs SameSite pour refléter l'utilisation prévue pour vos cookies. Ne comptez pas sur le comportement par défaut du navigateur. *Voir* [Développeurs : Préparez-vous pour new SameSite=None; Sécuriser les paramètres de cookie.](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)

### <a name="tabs-task-modules-and-message-extensions"></a>Onglets, modules de tâche et extensions de message

* Les onglets Teams utilisent pour incorporer du contenu qui est vu dans un contexte de niveau supérieur ou `<iframes>` de première partie.
* Les modules de tâches vous permettent de créer des expériences de menu contextuel modal dans votre application Teams. Comme un onglet, une fenêtre modale s'ouvre à l'intérieur de la page actuelle.
* Les extensions de message vous permettent d'insérer du contenu enrichi dans un message de conversation à partir de ressources externes.

Tous les cookies utilisés par le contenu incorporé sont considérés comme tiers lorsque le site est affiché dans un `<iframe>` . En outre, si des ressources distantes d'une page s'appuient sur les cookies envoyés avec une demande (par exemple, les balises, les polices externes et le contenu personnalisé), vous devez vous assurer qu'elles sont marquées pour une utilisation sur plusieurs sites, ou vous assurer qu'un système de base est en `<img>` `<script>` `SameSite=None; Secure` place.

### <a name="authentication"></a>Authentification

* Si vous avez besoin d'une authentification pour les pages de contenu incorporées dans les onglets, vous devez utiliser le flux d'authentification basé sur le web.
* Un flux d'authentification web peut également être utilisé pour une page de configuration, un module de tâche ou une extension de messagerie.
* Vous pouvez utiliser un flux d'authentification web pour un bot de conversation dont vous aurez besoin pour utiliser un module de tâche.

En vertu des restrictions SameSite mises à jour, un navigateur n'ajoute pas de cookie à un site web déjà authentifié si le lien dérive d'un site externe. Vous devez vous assurer que vos cookies d'authentification sont marqués pour une utilisation sur plusieurs sites, ou vous assurer qu'un système de base `SameSite=None; Secure` est en place.

### <a name="android-system-webview"></a>Android System WebView

Android WebView est un composant système Chrome qui permet aux applications Android d'afficher du contenu web. Bien que les nouvelles restrictions deviennent la valeur par défaut, à partir de Chrome 80, elles ne seront pas immédiatement appliquées sur les WebViews. Elles seront appliquées à l'avenir. Pour se préparer, Android permet aux applications natives de définir des cookies directement via [l'API CookeManager](https://developer.android.com/reference/android/webkit/CookieManager):

* Pour les cookies qui ne sont nécessaires que dans un contexte de première partie, vous devez les déclarer en tant `SameSite=Lax` que `SameSite=Strict` ou, selon le cas.
* Pour les cookies nécessaires dans un contexte tiers, vous devez vous assurer qu'ils sont déclarés comme `SameSite=None; Secure` .

## <a name="learn-more"></a>En savoir plus

[Exemples sameSite](https://github.com/GoogleChromeLabs/samesite-examples)

[Recettes de cookie SameSite](https://web.dev/samesite-cookie-recipes/)

[Clients incompatibles connus]( https://www.chromium.org/updates/same-site/incompatible-clients)

[Développeurs : préparez-vous pour le nouveau samesite=aucun ; Paramètres de cookie sécurisé](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)

**Impact sur OpenId Connect**<br>
[Modifications des cookies SameSite à venir dans ASP.NET et ASP.NET core](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)
