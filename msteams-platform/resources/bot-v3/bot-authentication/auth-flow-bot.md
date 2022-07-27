---
title: Flux d’authentification pour les bots
description: Décrit le flux d’authentification dans les bots
keywords: bots de flux d’authentification Teams
localization_priority: Normal
ms.topic: conceptual
ms.date: 03/01/2018
ms.openlocfilehash: e3bc5395a6a95272901076ec8bf51dc2ad57dfd2
ms.sourcegitcommit: 1cda2fd3498a76c09e31ed7fd88175414ad428f7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/27/2022
ms.locfileid: "67035330"
---
# <a name="microsoft-teams-authentication-flow-for-bots"></a>Flux d’authentification Microsoft Teams pour les bots

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

OAuth 2.0 est une norme ouverte pour l’authentification et l’autorisation utilisées par Azure AD et de nombreux autres fournisseurs d’identité. Une compréhension de base d’OAuth 2.0 est un prérequis pour l’utilisation de l’authentification dans Teams ; [voici une bonne vue d’ensemble](https://aaronparecki.com/oauth-2-simplified/) qui est plus facile à suivre que la [spécification formelle](https://oauth.net/2/). Le flux d’authentification pour les onglets et les bots est différent. Les onglets sont similaires aux sites web afin qu’ils puissent utiliser OAuth 2.0 directement, et les bots ne le sont pas et doivent faire quelques choses différemment, mais les concepts de base sont identiques.

Consultez [l’exemple d’authentification Microsoft Teams](https://github.com/OfficeDev/microsoft-teams-sample-auth-node) du référentiel GitHub pour obtenir un exemple illustrant le flux d’authentification pour les bots utilisant Node à l’aide du [type d’octroi de code d’autorisation OAuth 2.0](https://oauth.net/2/grant-types/authorization-code/).

![Diagramme de séquence d’authentification de bot](~/assets/images/authentication/bot_auth_sequence_diagram.png)

1. L’utilisateur envoie un message au bot.
2. Le bot détermine si l’utilisateur doit se connecter.
    * Dans cet exemple, le bot stocke le jeton d’accès dans son magasin de données utilisateur. Il demande à l’utilisateur de se connecter s’il n’a pas de jeton validé pour le fournisseur d’identité sélectionné. ([Afficher le code](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/utils/AuthenticationUtils.ts#L58-L76))
3. Le bot construit l’URL de la page de démarrage du flux d’authentification et envoie une carte à l’utilisateur avec une action de `signin`. ([Afficher le code](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L160-L190))
    * Comme les autres flux d’authentification d’application dans Teams, la page de démarrage doit se trouver sur un domaine figurant dans votre `validDomains` liste et sur le même domaine que la page de redirection post-connexion.
    * **IMPORTANT** : Le flux d’octroi de code d’autorisation OAuth 2.0 appelle un `state` paramètre dans la demande d’authentification qui contient un jeton de session unique pour empêcher une [attaque de falsification de demande intersite](https://en.wikipedia.org/wiki/Cross-site_request_forgery). L’exemple utilise un GUID généré de manière aléatoire.
4. Lorsque l’utilisateur *sélectionne le bouton* de connexion, Teams ouvre une fenêtre contextuelle et la navigue jusqu’à la page de démarrage.
5. La page de démarrage redirige l’utilisateur vers le point de terminaison `authorize` du fournisseur d’identité. ([Afficher le code](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/public/html/auth-start.html#L51-L56))
6. Sur le site du fournisseur, l’utilisateur se connecte et accorde l’accès au bot.
7. Le fournisseur dirige l’utilisateur vers la page de redirection OAuth du bot, avec un code d’autorisation.
8. Le bot utilise le code d’autorisation contre un jeton d’accès et **provisoirement** associe le jeton à l’utilisateur qui a lancé le flux de connexion. Ci-dessous, nous appelons cela un *jeton provisoire*.
    * Dans l’exemple, le bot associe la valeur du paramètre `state` à l’ID de l’utilisateur qui a lancé le processus de connexion afin qu’il puisse la mettre en correspondance ultérieurement avec la valeur `state` retournée par le fournisseur d’identité. ([Afficher le code](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L70-L99))
    * **IMPORTANT** : le bot stocke le jeton qu’il reçoit du fournisseur d’identité et l’associe à un utilisateur spécifique, mais il est marqué comme « en attente de validation ». Le jeton provisoire ne peut pas encore être utilisé : il doit être validé :
      1. **Validez ce qui a été reçu du fournisseur d’identité.** La valeur du paramètre `state` doit être confirmée par rapport à ce qui a été enregistré précédemment.
      1. **Valider ce qui est reçu de Teams.** Une [validation de l’authentification en deux étapes](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) est effectuée pour s’assurer que l’utilisateur qui a autorisé le bot avec le fournisseur d’identité est le même utilisateur que celui qui discute avec le bot. Cette validation protège contre [les](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) attaques par hameçonnage et les attaques par [hameçonnage](https://en.wikipedia.org/wiki/Phishing) . Le bot génère un code de vérification et le stocke, en l'associant à l'utilisateur. Le code de vérification est envoyé automatiquement par Teams, comme décrit ci-dessous aux étapes 9 et 10. ([Afficher le code](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L100-L113))
9. Le rappel OAuth affiche une page qui appelle `notifySuccess("<verification code>")`. ([Afficher le code](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/master/src/views/oauth-callback-success.hbs))
10. Teams ferme la fenêtre contextuelle et renvoie l’envoi `<verification code>` au `notifySuccess()` bot. Le bot reçoit un message [d’appel](/bot-framework/dotnet/bot-builder-dotnet-activities#invoke) avec `name = signin/verifyState`.
11. Le bot examine le code de vérification entrant par rapport au code de vérification stocké avec le jeton provisoire de l’utilisateur. ([Afficher le code](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L127-L140))
12. S’ils correspondent, le bot marque le jeton comme validé et prêt à être utilisé. Sinon, le flux d’authentification échoue et le bot supprime le jeton provisoire.

> [!Note]
> Si vous rencontrez des problèmes d’authentification sur mobile, assurez-vous que votre Kit de développement logiciel (SDK) JavaScript est mis à jour vers la version 1.4.1 ou ultérieure.

## <a name="samples"></a>Échantillons

Pour obtenir un exemple de code montrant le processus d’authentification du bot, consultez :

* [Exemple d’authentification de bot Microsoft Teams (Nœud)](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)

## <a name="more-details"></a>Plus de détails

Pour obtenir des procédures pas à pas d’implémentation détaillées pour l’authentification de bot ciblant Azure Active Directory, consultez :

* [Authentifier un utilisateur dans un bot Microsoft Teams](~/resources/bot-v3/bot-authentication/auth-bot-AAD.md)
