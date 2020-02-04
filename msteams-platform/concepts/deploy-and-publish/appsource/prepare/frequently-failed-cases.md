---
title: Conseils et incidents fréquemment ayant échoué
description: Décrit des conseils pour l’envoi et la plupart des stratégies ayant échoué
keywords: Forum aux questions sur la publication de teams
ms.openlocfilehash: ffb472c918a205bdcf921b967269a80fcaa93338
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673876"
---
# <a name="tips-and-frequently-failed-cases"></a>Conseils et incidents fréquemment ayant échoué 

Cet article décrit certaines des raisons les plus courantes de validation d’échec d’applications. Il n’est pas destiné à être une liste exhaustive de tous les problèmes potentiels liés à votre application. Toutefois, si vous suivez ce guide, la probabilité d’une première passe est grandement améliorée. Consultez la liste complète des stratégies ici : [stratégies de validation AppSource](https://dev.office.com/officestore/docs/validation-policies). Les stratégies de la section 14 des stratégies de validation AppSource globales sont propres aux applications Microsoft Teams.

## <a name="tips-for-successful-app-submission"></a>Conseils pour la soumission d’une application réussie

* Vérifiez que vous utilisez la version 1.4.1 ou une version ultérieure du kit de développement logiciel (SDK) JavaScript Teams.
* N’effectuez pas de modifications dans votre application lorsque la validation est en cours. Cela nécessite une nouvelle validation complète de votre application.
* Votre application ne doit pas cesser de répondre, se terminer de manière inopinée ou contenir des erreurs de programmation. Si un problème survient, il doit être correctement restauré avec un message de transfert valide à l’utilisateur.
* Votre application ne doit pas télécharger, installer ou lancer automatiquement un code exécutable sur l’environnement de l’utilisateur. Tout téléchargement doit rechercher une autorisation explicite de l’utilisateur.
* Tous les éléments que vous associez à votre expérience, tels que les descriptions et la documentation de support, doivent être précis. Utilisez correctement l'orthographe, les majuscules, la ponctuation et la grammaire.
* Aide et support : il est fortement recommandé d’avoir un lien Aide/FAQ pour votre application teams et de fournir ce lien lors de la première utilisation de l’expérience utilisateur. Pour toutes les applications personnelles, nous vous recommandons de fournir votre page d’aide sous la forme d’un onglet personnel pour une meilleure expérience utilisateur.

## <a name="policy-112-sign-up-sign-in-and-sign-out"></a>Stratégie 11,2 : s’inscrire, se connecter et se déconnecter

Description : les applications doivent fournir une expérience d’inscription claire et simple et (le cas échéant). L’expérience doit être accessible sur toutes les fonctionnalités de votre application.

* S’il existe une option de connexion explicite fournie à l’utilisateur, il doit y avoir une option de déconnexion (même si l’application utilise l’authentification unique/authentification silencieuse).
* L’option de déconnexion doit signer l’utilisateur uniquement sur la fonctionnalité de votre application, et non sur le client Teams.
* Toutes les étendues disposant d’une connexion doivent également être déconnectées. Au minimum, l’option de déconnexion doit signer l’utilisateur à partir des mêmes fonctionnalités que l’option de connexion. Par exemple, si l’option de connexion connecte l’utilisateur à la fois à une extension de messagerie et à une tabulation, l’option de déconnexion doit signer l’utilisateur à partir de l’extension de message et de l’onglet.

* Assurez-vous qu’il existe toujours un moyen d’inverser les comportements suivants (ou similaires) :
  * Connexion => déconnexion
  * Lier un compte/service => annuler la liaison d’un compte/service
  * Connecter un compte/service => déconnecter le compte/service
  * Autoriser un compte/service => de/désactiver le compte/service
  * Inscrire un compte/service => annuler l’inscription du compte/service
* Si votre application nécessite un compte ou un service, vous devez permettre à l’utilisateur de s’inscrire ou de demander une inscription. Une exception peut être recherchée pour un processus d’inscription si votre application s’ajuste à la catégorie d’application « entreprise ».
* La fonctionnalité de connexion/déconnexion doit fonctionner sur les clients mobiles. Vérifiez que vous avez mis à niveau votre SDK JavaScript teams vers la version 1.4.1 ou une version ultérieure.

Pour plus d’informations sur l’authentification, consultez la rubrique suivante :

* [Documentation de l’authentification](~/concepts/authentication/authentication.md)
* [Exemple d’authentification bot dans le nœud](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
* [Exemple d’authentification d’onglet dans le nœud](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)
* [Authentification Tab/bot dans C#/.NET](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp)

## <a name="policy-145-microsoft-teams-apps-must-respond-in-a-reasonable-timeframe"></a>Stratégie 14,5 : les applications Microsoft teams doivent répondre dans un délai raisonnable.

* 14.5.1 : pour les onglets, si une réponse à une action prend plus de trois secondes, vous devez fournir un message de chargement ou un avertissement.
* 14.5.2 : pour les robots, une réponse à une commande utilisateur doit se produire dans les deux secondes. Si un traitement plus long est requis, vous devez utiliser un indicateur de saisie.
* 14.5.3 : pour les extensions de composition, une réponse à une commande utilisateur doit être exécutée dans les cinq secondes.

> [!TIP]
> Assurez-vous d’inclure l’indicateur de chargement lorsque l’application prend trop de temps.

## <a name="policy-14153-content-in-a-tab-should-not-have-superfluousunnecessary-ui-aka-ui-chrome-or-layered-navigation"></a>Stratégie 14.15.3 : le contenu d’un onglet ne doit pas avoir d’interface utilisateur superflue/inutile (alias : UI chrome) ou de navigation en couches

Les onglets doivent fournir du contenu ciblé et éviter les éléments d’interface utilisateur qui ne sont pas liés à ce contenu. En règle générale, cela fait référence à une navigation imbriquée/superposée inutile, à une interface utilisateur non liée ou inappropriée en regard du contenu ou à tous les liens permettant à l’utilisateur d’accéder au contenu qui n’est pas lié au contenu de l’onglet. Par exemple, SharePoint a supprimé les menus de navigation et n’a présenté que le contenu principal dans l’onglet.

![Vue SharePoint du](~/assets/images/faq/web-sp.png)
![mode Web SharePoint](~/assets/images/faq/tab-sp.png)

S’il existe plusieurs options d’affichage, vous pouvez choisir d’utiliser un menu de configuration d’onglet pour l’utilisateur. Par exemple, au lieu d’incorporer un menu à l’intérieur de l’onglet, les idées larges déplacent le menu sur la page de configuration de sorte que l’affichage de l’onglet réel soit propre et centré.

![Page de configuration de l’idée large](~/assets/images/faq/wideidea.png)

## <a name="policy-14157-bots-must-respond-to-any-command-and-must-not-dead-end-the-user"></a>Stratégie 14.15.7 : les robots doivent répondre à n’importe quelle commande et ne doivent pas être bloqués par l’utilisateur.

Votre robot doit toujours être réactif. Voici quelques conseils pour aider votre robot à répondre plus intelligemment aux utilisateurs.

**Utilisez la liste de commandes :** L’analyse de l’entrée de l’utilisateur ou prédiction de l’utilisateur est difficile. Au lieu de laisser l’utilisateur deviner ce que votre robot peut faire, fournissez aux utilisateurs une liste de commandes que votre robot peut comprendre.

![Liste de commandes de flux](~/assets/images/faq/flow-bot.png)

**Inclure une commande d’aide :** Les utilisateurs sont susceptibles de taper « aide » lorsqu’ils sont perdus ou lorsque le bot n’a pas répondu à ce qu’ils attendent. Incluez une commande d’aide qui fournit votre proposition de valeur, ainsi que toutes vos commandes valides.

![Commande d’aide au flux](~/assets/images/faq/flow-help.png)

**Inclure le contenu de l’aide ou des conseils en cas de perte de votre robot :** Lorsque vous n’êtes pas en mesure de comprendre l’entrée de l’utilisateur, fournissez un autre résultat à l’utilisateur. Par exemple, «je suis désolée, je ne comprends pas. Tapez « aide » pour plus d’informations. Ne répondez pas avec un message d’erreur ou simplement « je ne comprends pas ». Utilisez cette chance pour enseigner vos utilisateurs.

**Considérez les deux étendues :** Assurez-vous que votre robot fournit les réponses appropriées lorsqu’il est mentionné (@*botname*) dans un canal et dans les conversations personnelles, le cas échéant. Si votre bot ne fournit pas de contexte explicite au sein de l’étendue personnelle ou Teams, désactivez cette étendue via le manifeste. (Consultez le `bots` bloc dans la [Référence du schéma de manifeste de Microsoft teams](~/resources/schema/manifest-schema.md#bots).)

## <a name="policy-14159-bot-must-send-welcome-messages-on-the-first-launch"></a>Stratégie 14.15.9 : le bot doit envoyer des messages de bienvenue au premier lancement

Les messages de bienvenue sont le meilleur moyen de définir le ton. Il s’agit du premier utilisateur d’interaction avec le bot. Un bon message d’accueil peut inciter l’utilisateur à continuer à explorer l’application alors qu’un mauvais risque de confondre l’utilisation et les utilisateurs peuvent perdre des intérêts s’ils ne peuvent pas voir immédiatement la valeur de l’application.

### <a name="personal-scope"></a>Étendue personnelle

Lors du premier lancement du bot, l’utilisateur doit obtenir un message de bienvenue auprès du bot, même avant de se connecter. Couplez des conseils pour vous intéresser lors de la conception de votre message de bienvenue :

**Rendez le message concis et instructif :** Il se peut que les utilisateurs aient des expériences et des connaissances très différentes sur votre application. Ils ont peut-être utilisé votre application sur une autre plateforme ou ne connaissent rien sur votre application. Vous souhaitez personnaliser votre message pour l’ensemble de l’audience et, dans quelques phrases, expliquer ce que fait votre robot et comment interagir avec lui. Vous devez également expliquer la valeur de l’application et la façon dont les utilisateurs peuvent l’utiliser.
![Café et robot dinning](~/assets/images/faq/cafe-bot.png)

**Rendez votre message exploitable :** Réfléchissez à la première chose que les utilisateurs doivent faire après l’installation de votre application. Faut-il effectuer une commande sympa ? Existe-t-il une autre expérience d’intégration ? Doivent-ils se connecter ? Vous pouvez ajouter des actions sur une carte adaptative ou fournir des exemples spécifiques tels que « essayez de vous demander.... », « voici ce que je peux faire... ».

### <a name="team-scope"></a>Étendue de l’équipe

Les choses sont un peu différentes lorsque le bot est d’abord ajouté à un canal. Normalement, vous ne devez pas envoyer un message 1:1 à tous les membres de l’équipe, mais le bot peut envoyer un message de bienvenue dans le canal.

## <a name="policy-141510-tab-configuration-ui-should-not-dead-end-the-experience-and-always-provide-a-way-for-a-user-to-continue"></a>Stratégie 14.15.10 : l’interface utilisateur de configuration d’onglets ne doit pas interrompre l’expérience et offrir toujours un moyen à un utilisateur de continuer.

Un utilisateur doit toujours pouvoir terminer l’expérience de configuration, même s’il ne parvient pas à trouver immédiatement le contenu qu’il recherche. L’expérience de configuration doit fournir aux utilisateurs des options permettant de trouver leur contenu ou d’épingler une URL ou de créer du contenu s’il n’existe pas. L’utilisateur ne doit pas laisser l’expérience de configuration pour créer du contenu, puis revenir à teams pour l’épingler.

![OneNote permet aux utilisateurs de coller un lien OneNote dans les notes de cas est introuvable](~/assets/images/faq/tab-onenote-config.png)

![Les utilisateurs peuvent toujours créer un plan sur le planificateur pour les cas où il n’en existe pas.](~/assets/images/faq/tab-planner-config.png)

![SharePoint permet également à l’utilisateur de coller directement une liaison SharePoint](~/assets/images/faq/tab-sp-config.png)