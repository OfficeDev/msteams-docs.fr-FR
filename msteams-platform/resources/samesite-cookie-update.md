---
title: Microsoft teams et l’attribut SameSite cookie (mise à jour 2020)
author: laujan
description: ''
keywords: attributs de cookie samesite
ms.topic: reference
ms.author: lomeybur
ms.openlocfilehash: 167266ba0b5af1c8233cffe1fef496dd94c27ae4
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673563"
---
# <a name="microsoft-teams-and-the-samesite-cookie-attribute-2020-update"></a>Microsoft teams et l’attribut SameSite cookie (mise à jour 2020)

## <a name="cookies-in-brief"></a>Cookies en bref

 Les cookies sont des chaînes de texte, envoyées à partir de sites Web et stockées sur un ordinateur par le navigateur Web. Elles sont généralement utilisées pour l’authentification et la personnalisation, par exemple, par le rappel d’informations d’État, la préservation des paramètres utilisateur, l’enregistrement de l’activité de navigation et l’affichage des publicités pertinentes. Les cookies sont toujours liés à un domaine particulier et peuvent être installés par différentes parties. Elles sont classées comme suit :

 |Cookie|Portée|
 | ------ | ------ |
 |**Cookie interne**|Un cookie tiers est créé par des sites Web visités par un utilisateur et est utilisé pour enregistrer des données telles que des éléments de panier, des informations d’identification de connexion (par exemple, des cookies d’authentification) et d’autres analyses.|
 |**Cookie de deuxième partie**|Un cookie de deuxième partie est techniquement le même que le cookie d’un destinataire. La différence réside dans le fait que les données sont partagées avec une tierce partie via un accord de partenariat de données (par exemple, l' [analyse et la création de rapports de Microsoft teams](/microsoftteams/teams-analytics-and-reports/teams-reporting-reference)). |
 |**Cookie tiers**|Un cookie tiers est installé par un domaine autre que celui que l’utilisateur a visité explicitement et est principalement utilisé pour le suivi (par exemple, les boutons « comme »), le service AD et les conversations en direct.|

### <a name="cookies-and-http-requests"></a>Cookies et requêtes HTTP

Avant l’introduction des restrictions SameSite, lorsque les cookies étaient stockés dans le navigateur, ils étaient attachés à *chaque* requête Web http et envoyés au serveur par l’en-tête de réponse HTTP set-cookie. De manière prévisible, ces performances pouvaient introduire des failles de sécurité telles que les attaques de contrefaçon de demande intersites (CSRF). *Consultez la rubrique* [http cookies](https://developer.mozilla.org/docs/Web/HTTP/Cookies). Le composant SameSite a atténué cette exposition via son implémentation et sa gestion dans l’en-tête SetCookie.

### <a name="samesite-attribute-initial-release"></a>Attribut SameSite : publication initiale

Google Chrome version 51 a introduit la spécification SetCookie SameSite en tant qu’attribut *facultatif* . À partir de la version 17672 de, Windows 10 a introduit la prise en charge des cookies SameSite pour le [navigateur Microsoft Edge](https://blogs.windows.com/msedgedev/2018/05/17/samesite-cookies-microsoft-edge-internet-explorer/).

Les développeurs peuvent choisir de ne pas ajouter l’attribut de cookie SameSite à l’en-tête SetCookie, soit les ajouter avec l’un des deux paramètres suivants : *Lax* et *strict*. Un attribut SameSite non implémenté a été considéré comme l’État par défaut.

## <a name="samesite-cookie-attribute-2020-release"></a>Attribut de cookie SameSite : version 2020

Chrome 80, planifié pour la publication en février 2020, introduit de nouvelles valeurs de cookie et impose des stratégies de cookies par défaut. Trois valeurs peuvent être passées dans l’attribut SameSite mis à jour : *strict*, *Lax*ou *None*. Les cookies qui ne spécifient pas l’attribut SameSite `SameSite=Lax`seront définis par défaut sur.

|Setting | Respect | Valeur |Spécification d’attribut |
| -------- | ----------- | --------|--------|
| **Lax**  | Les cookies ne seront envoyés automatiquement que dans un contexte *interne* et avec des demandes HTTP Get. Les cookies SameSite seront refusés sur les sous-requêtes intersites, telles que les appels pour charger des images ou des IFRAMES, mais seront envoyées lorsqu’un utilisateur navigue vers l’URL à partir d’un site externe, par exemple, en suivant un lien.| **Par défaut** |`Set-Cookie: key=value; SameSite=Lax`|
| **Empêcher** |Le navigateur enverra uniquement les cookies pour les demandes de contexte internes (demandes provenant du site qui définissent le cookie). Si la demande provient d’une URL différente de celle de l’emplacement actuel, aucun des cookies marqués avec l' `Strict` attribut n’est envoyé.| Facultatif |`Set-Cookie: key=value; SameSite=Strict`|
| **Aucune** | Les cookies sont envoyés dans le contexte interne et les demandes croisées ; Toutefois, la valeur doit être définie explicitement sur **`None`** et toutes les requêtes de navigateur **doivent suivre le protocole HTTPS** et **`Secure`** inclure l’attribut qui nécessite une connexion chiffrée. Les cookies qui n’adhèrent pas à cette exigence seront **rejetés**. <br/>**Les deux attributs sont requis ensemble**. Si seul **`None`** est spécifié sans **`Secure`** ou si le protocole HTTPS n’est pas utilisé, le cookie tiers est rejeté.| Facultatif, mais si elle est définie, le protocole HTTPs est requis. |`Set-Cookie: key=value; SameSite=None; Secure` |

## <a name="handling-incompatible-clients"></a>Gestion des clients incompatibles

> [!IMPORTANT]
> Actuellement, `SameSite=None` n’est pas pris en charge par le [**client de bureau teams**](/aspnet/core/security/samesite?view=aspnetcore-3.1#test-with-electron) ni par les versions antérieures de chrome ou Safari. *Voir* [clients incompatibles connus]( https://www.chromium.org/updates/same-site/incompatible-clients).
>Toutefois, il existe deux **solutions de contournement**:
>
>1. Vérifiez l’agent utilisateur afin de fournir la propriété SameSite correcte. Vous pouvez implémenter la vérification de l’agent utilisateur en [**C#**](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/) et [**node. js**](https://web.dev/samesite-cookie-recipes/).
>2. Définissez vos attributs de cookie en utilisant les nouveaux et les anciens modèles. *Voir* [gestion des clients incompatibles](https://web.dev/samesite-cookie-recipes/#handling-incompatible-clients)<br><br>
>**Si votre application est en cours d’exécution dans le client de bureau teams et que vous `SameSite=None` définissez l’attribut SameSite sur, votre application ne fonctionnera pas comme prévu.**

L’utilisation de l’une ou l’autre de ces méthodes garantit que votre application continue à fonctionner correctement lorsque le client de `SameSite=None` Bureau teams est mis à niveau vers une version compatible de chrome.

## <a name="teams-implications-and-adjustments"></a>Implications et ajustements des équipes

>[!WARNING]
>**Les applications qui s’exécutent dans le client de bureau Teams ne sont pas compatibles avec l' `SameSite=None` attribut et elles ne fonctionnent pas comme prévu.** Consultez les **solutions de contournement**ci-dessus.

1. Activez le paramètre SameSite approprié pour vos cookies et vérifiez que vos applications et extensions continuent de fonctionner dans Teams.
1. Si vos applications ou extensions échouent, effectuez les corrections nécessaires avant la version chrome 80.
1. Les partenaires internes de Microsoft peuvent rejoindre l’équipe suivante s’ils ont besoin d’informations supplémentaires ou de <https://teams.microsoft.com/l/team/19%3A08b594cd465e4c0491fb751e823802e2%40thread.skype/conversations?groupId=4d6d04cd-dbf0-43c8-a2ff-f80dd38be034&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47>l’aide relative à ce problème :.

> [!NOTE]
> Pour une meilleure pratique, il est recommandé de toujours définir les attributs SameSite afin de refléter l’utilisation prévue pour vos cookies, qui ne dépendent pas du comportement par défaut du navigateur. *Voir* [développeurs : Préparez-vous pour la nouvelle SameSite = aucun ; Sécuriser les paramètres des cookies](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html).

### <a name="tabs-task-modules-and-message-extensions"></a>Onglets, modules de tâches et extensions de message

* Les onglets `<iframes>` teams permettent d’incorporer du contenu affiché dans un contexte de niveau supérieur ou site.
* Les modules de tâches vous permettent de créer des expériences de menu contextuel modal dans votre application Teams. À l’instar d’un onglet, une fenêtre modale s’ouvre dans la page active.
* Les extensions de message vous permettent d’insérer du contenu enrichi dans un message de conversation à partir de ressources externes.

Les cookies utilisés par le contenu incorporé seront considérés comme des tiers lorsque le site est affiché `<iframe>`dans un. En outre, si des ressources distantes sur une page reposent sur des cookies envoyés avec une requête `<img>` ( `<script>` par exemple, des balises, des polices externes et du contenu personnalisé), vous devez vous assurer que ces derniers `SameSite=None; Secure` sont marqués pour l’utilisation intersites — ou s’assurer qu’un secours est en place.

### <a name="authentication"></a>Authentification

* Si vous avez besoin d’une authentification pour les pages de contenu incorporées dans les onglets, vous devez utiliser le flux d’authentification Web.
* Un flux d’authentification Web peut également être utilisé pour une page de configuration, un module de tâches ou une extension de messagerie.
* Vous pouvez utiliser un flux d’authentification Web pour un bot conversationnel vous devrez utiliser un module de tâches.

Conformément aux restrictions SameSite mises à jour, un navigateur n’ajoute pas de cookie à un site Web déjà authentifié si le lien dérive d’un site externe. Vous devez vous assurer que vos cookies d’authentification sont marqués pour l’utilisation intersites — `SameSite=None; Secure` ou vous assurer qu’un secours est en place.

### <a name="android-system-webview"></a>Vue d’ensemble du système Android

Android WebView est un composant système chrome qui permet aux applications Android d’afficher du contenu Web. Bien que les nouvelles restrictions deviennent la valeur par défaut, en commençant par chrome 80, elles ne seront pas appliquées immédiatement sur les WebView. Elles seront appliquées à l’avenir. Pour préparer, Android permet aux applications natives de définir des cookies directement via l' [API CookeManager](https://developer.android.com/reference/android/webkit/CookieManager):

* Pour les cookies qui sont uniquement nécessaires dans un contexte interne, vous devez les déclarer en tant `SameSite=Lax` que `SameSite=Strict`ou, le cas échéant.
* Pour les cookies nécessaires dans un contexte tiers, vous devez vous assurer qu’ils sont déclarés `SameSite=None; Secure`en tant que.

## <a name="learn-more"></a>En savoir plus

[Exemples SameSite](https://github.com/GoogleChromeLabs/samesite-examples)

[Recettes de cookie SameSite](https://web.dev/samesite-cookie-recipes/)

[Clients incompatibles connus]( https://www.chromium.org/updates/same-site/incompatible-clients)

[Développeurs : Préparez-vous pour la nouvelle SameSite = None ; Sécuriser les paramètres des cookies](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)

**Impact de la connexion OpenId**<br>
[Modifications apportées aux cookies SameSite dans ASP.NET et ASP.NET Core](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)
