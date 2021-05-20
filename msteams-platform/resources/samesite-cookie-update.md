---
title: Microsoft Teams et l’attribut de cookie SameSite (mise à jour 2020)
author: laujan
description: décrit les attributs du cookie SameSite
keywords: cookie attribue samesite
ms.topic: reference
localization_priority: Normal
ms.author: lomeybur
ms.openlocfilehash: cf28a28050d50b2b6b2601a3231cdad30211ab2c
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566711"
---
# <a name="microsoft-teams-and-the-samesite-cookie-attribute-2020-update"></a>Microsoft Teams et l’attribut de cookie SameSite (mise à jour 2020)

## <a name="cookies-in-brief"></a>Cookies en bref

 Les cookies sont des chaînes de texte, envoyées à partir de sites Web et stockées sur un ordinateur par le navigateur Web. Ils sont généralement utilisés pour l’authentification et la personnalisation, par exemple, le rappel d’informations étatiques, la préservation des paramètres utilisateur, l’enregistrement de l’activité de navigation et l’affichage des annonces pertinentes. Les cookies sont toujours liés à un domaine particulier et peuvent être installés par différentes parties. Ils sont classés comme suit :

 |Cookie|Portée|
 | ------ | ------ |
 |**Cookie de première partie**|Un cookie de première partie est créé par des sites Web qu’un utilisateur visite et est utilisé pour enregistrer des données telles que des articles de panier, des informations d’identification de connexion. Par exemple, des cookies d’authentification et d’autres analyses.|
 |**Cookie de deuxième partie**|Un cookie de deuxième partie est techniquement le même qu’un cookie de première partie. La différence est que les données sont partagées avec une deuxième partie par le biais d’un accord de partenariat de données. Par exemple, [Microsoft Teams analytique et de rapports](/microsoftteams/teams-analytics-and-reports/teams-reporting-reference). |
 |**Cookie tiers**|Un cookie tiers est installé par un domaine autre que celui que l’utilisateur a explicitement visité et est principalement utilisé pour le suivi. Par exemple, les boutons « J’aime », le service d’annonce et les conversations en direct.|

### <a name="cookies-and-http-requests"></a>Cookies et demandes HTTP

Avant l’introduction des restrictions SameSite, lorsque les cookies étaient stockés sur le navigateur, ils étaient attachés *à* chaque demande web HTTP et envoyés au serveur par l’en-tête de réponse Set-Cookie HTTP. Comme on pouvait s’y rendre, cette performance avait le potentiel d’introduire des failles de sécurité telles que les attaques de contrefaçon de demande de site cross-site (CSRF). *Voir* [les cookies HTTP](https://developer.mozilla.org/docs/Web/HTTP/Cookies). Le composant SameSite a atténué cette exposition grâce à sa mise en œuvre et à sa gestion dans l’en-tête SetCookie.

### <a name="samesite-attribute-initial-release"></a>Attribut SameSite : libération initiale

Google Chrome version 51 a introduit la spécification SetCookie SameSite comme un *attribut optionnel.* À partir de Build 17672, Windows 10 introduit la prise en charge des cookies SameSite [pour Microsoft Edge navigateur](https://blogs.windows.com/msedgedev/2018/05/17/samesite-cookies-microsoft-edge-internet-explorer/).

Les développeurs peuvent refuser d’ajouter l’attribut de cookie SameSite à l’en-tête SetCookie ou ils pourraient l’ajouter avec l’un des deux paramètres, *Lax* et *Strict*. Un attribut SameSite non implémenté a été considéré comme l’état par défaut.

## <a name="samesite-cookie-attribute-2020-release"></a>Attribut de cookie SameSite : version 2020

Chrome 80, dont la sortie est prévue en février 2020, introduit de nouvelles valeurs de cookies et impose des stratégies de cookies par défaut. Trois valeurs peuvent être transmises dans l’attribut SameSite mis à *jour : Strict,* *Lax,* ou *None*. Les cookies qui ne spécifient pas l’attribut SameSite seront par défaut `SameSite=Lax` à .

|Paramètre | application | Valeur |Spécification des attributs |
| -------- | ----------- | --------|--------|
| **laxiste**  | Les cookies ne seront envoyés automatiquement que dans *un contexte de première* partie et avec les demandes HTTP GET. Les cookies SameSite seront retenus sur les sous-demandes inter-sites, telles que les appels pour charger des images ou des iframes, mais seront envoyés lorsqu’un utilisateur navigue vers l’URL à partir d’un site externe, par exemple, en suivant un lien.| **Par défaut** |`Set-Cookie: key=value; SameSite=Lax`|
| **strict** |Le navigateur n’enverra des cookies que pour les demandes de contexte de première partie (demandes provenant du site qui a défini le cookie). Si la demande provient d’une URL différente de celle de l’emplacement actuel, aucun des cookies marqués avec `Strict` l’attribut ne sera envoyé.| Facultatif |`Set-Cookie: key=value; SameSite=Strict`|
| **Aucune** | Les cookies seront envoyés dans le contexte de la première partie et dans les demandes d’origine croisée; toutefois, la valeur doit être définie explicitement et toutes **`None`** les demandes du navigateur doivent suivre le protocole **HTTPS et** inclure **`Secure`** l’attribut qui nécessite une connexion cryptée. Les cookies qui n’adhèrent pas à cette exigence seront **rejetés.** <br/>**Les deux attributs sont requis ensemble**. Si le protocole HTTPS n’est pas utilisé ou si le protocole **`None`** **`Secure`**  HTTPS n’est pas utilisé, le cookie tiers sera rejeté.| Facultatif, mais, s’il est défini, le protocole HTTPS est nécessaire. |`Set-Cookie: key=value; SameSite=None; Secure` |

## <a name="teams-implications-and-adjustments"></a>Teams implications et ajustements

1. Activez le paramètre SameSite pertinent pour vos cookies et validez que vos applications et extensions continuent de fonctionner dans Teams.
1. Si vos applications ou extensions échouent, faites les correctifs nécessaires avant la version Chrome 80.
1. Les partenaires internes de Microsoft peuvent rejoindre l’équipe suivante s’ils ont besoin de plus d’informations ou d’aide pour ce problème : <https://teams.microsoft.com/l/team/19%3A08b594cd465e4c0491fb751e823802e2%40thread.skype/conversations?groupId=4d6d04cd-dbf0-43c8-a2ff-f80dd38be034&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47> .

> [!NOTE]
> Pour les meilleures pratiques, il est recommandé de toujours définir des attributs SameSite pour refléter l’utilisation prévue pour vos cookies. Ne vous fiez pas au comportement par défaut du navigateur. Pour plus d’informations, [voir Développeurs: Préparez-vous pour new SameSite=None; Sécurisez les cookies Paramètres](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html).

### <a name="tabs-task-modules-and-message-extensions"></a>Onglets, modules de tâches et extensions de messages

* Teams onglets utilisés `<iframes>` pour intégrer du contenu qui est visualisé dans un contexte de haut niveau ou de première partie.
* Les modules de tâches vous permettent de créer des expériences de menu contextuel modal dans votre application Teams. Semblable à un onglet, une fenêtre modale s’ouvre à l’intérieur de la page actuelle.
* Les extensions de messages vous permettent d’insérer du contenu enrichi dans le message de chat à partir de ressources externes.

Tous les cookies utilisés par le contenu intégré seront considérés comme tiers lorsque le site est affiché dans un `<iframe>` . En outre, si des ressources distantes sur une page s’appuient sur l’envoi de cookies avec une demande et des balises, des polices externes et du contenu personnalisé, vous devez vous assurer `<img>` `<script>` qu’ils sont marqués pour une utilisation inter-sites, par exemple ou pour vous `SameSite=None; Secure` assurer qu’un repli est en place.

### <a name="authentication"></a>Authentification

* Si vous avez besoin d’authentification pour les pages de contenu intégrées dans les onglets, vous devrez utiliser le flux d’authentification basé sur le Web.
* Un flux d’authentification basé sur le Web peut également être utilisé pour une page de configuration, un module de tâches ou une extension de messagerie.
* Vous pouvez utiliser un flux d’authentification basé sur le Web pour un bot conversationnel dont vous aurez besoin pour utiliser un module de tâches.

Conformément aux restrictions mises à jour de SameSite, un navigateur n’ajoutera pas de cookie à un site Web déjà authentifié si le lien provient d’un site externe. Vous devrez vous assurer que vos cookies d’authentification sont marqués pour une utilisation inter-sites `SameSite=None; Secure` ou s’assurer qu’un repli est en place.

### <a name="android-system-webview"></a>WebView système Android

Android WebView est un composant du système Chrome qui permet aux applications Android d’afficher du contenu Web. Bien que les nouvelles restrictions deviennent par défaut, à commencer par Chrome 80, elles ne seront pas immédiatement appliquées sur WebViews. Ils seront appliqués à l’avenir. Pour se préparer, Android permet aux applications natives de définir des cookies directement via [l’API CookeManager](https://developer.android.com/reference/android/webkit/CookieManager):

* Pour les cookies qui ne sont nécessaires que dans un contexte de première partie, vous devez les déclarer `SameSite=Lax` au `SameSite=Strict` besoin.
* Pour les cookies nécessaires dans un contexte tiers, vous devez vous assurer qu’ils sont déclarés comme `SameSite=None; Secure` .

## <a name="see-also"></a>Voir aussi

* [Mêmes exemples de site](https://github.com/GoogleChromeLabs/samesite-examples)

* [Recettes de biscuits SameSite](https://web.dev/samesite-cookie-recipes/)

* [Clients incompatibles connus]( https://www.chromium.org/updates/same-site/incompatible-clients)

* [Développeurs: Préparez-vous pour samesite=none nouveau; Sécurisez les cookies Paramètres](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)

**OpenId Connecter impact**<br>
[Changements à venir de cookies SameSite dans ASP.NET et ASP.NET Core](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)
