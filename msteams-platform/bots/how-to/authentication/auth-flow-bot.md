---
title: Flux d’authentification pour les robots
description: Décrit le flux d’authentification dans les robots
keywords: robots de flux d’authentification des équipes
ms.date: 03/01/2018
ms.openlocfilehash: 40f34a3b51349cc1d11f819a92b479a92ebac149
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673947"
---
# <a name="microsoft-teams-authentication-flow-for-bots"></a>Flux d’authentification de Microsoft teams pour les robots

OAuth 2,0 est une norme ouverte pour l’authentification et l’autorisation utilisées par Azure Active Directory (Azure AD) et de nombreux autres fournisseurs d’identité. Une compréhension de base de OAuth 2,0 est une condition préalable à l’utilisation de l’authentification dans teams ; [Voici une bonne présentation](https://aaronparecki.com/oauth-2-simplified/) qui est plus facile à suivre que les [spécifications formelles](https://oauth.net/2/). Le flux d’authentification pour les onglets et les robots est un peu différent : les onglets sont très similaires aux sites Web afin qu’ils puissent utiliser OAuth 2,0 directement, tandis que les robots ne sont pas et doivent effectuer quelques opérations différemment, mais les concepts de base sont identiques.

Voir l’exemple [d’authentification Microsoft teams](https://github.com/OfficeDev/microsoft-teams-sample-auth-node) GitHub référentiel pour obtenir un exemple illustrant le flux d’authentification pour les robots utilisant node. js et le [type d’octroi de code d’autorisation OAuth 2,0](https://oauth.net/2/grant-types/authorization-code/).

![Diagramme de séquence d’authentification de robot](../../../assets/images/authentication/bot_auth_sequence_diagram.png)

1. L’utilisateur envoie un message au bot.
2. Le bot détermine si l’utilisateur doit se connecter.
    * Dans cet exemple, le bot stocke le jeton d’accès dans son magasin de données utilisateur. Il demande à l’utilisateur de se connecter s’il ne dispose pas d’un jeton validé pour le fournisseur d’identité sélectionné. ([Afficher le code](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/utils/AuthenticationUtils.ts#L58-L76))
3. Le bot construit l’URL sur la page de démarrage du flux d’authentification et envoie une carte à l’utilisateur avec une `signin` action. ([Afficher le code](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L160-L190))
    * Comme les autres flux d’authentification d’application dans Teams, la page de démarrage doit se trouver dans `validDomains` un domaine de votre liste et dans le même domaine que la page de redirection post-connexion.
    * **Important**: les appels de flux d’octroi de code d’autorisation `state` OAuth 2,0 pour un paramètre dans la demande d’authentification contenant un jeton de session unique pour empêcher une [attaque de contrefaçon de demande intersite](https://en.wikipedia.org/wiki/Cross-site_request_forgery). L’exemple utilise un GUID généré de manière aléatoire.
4. Lorsque l’utilisateur sélectionne le bouton de *connexion* , teams ouvre une fenêtre contextuelle et accède à la page de démarrage.
5. La page de démarrage redirige l’utilisateur vers le point de terminaison `authorize` du fournisseur d’identité. ([Afficher le code](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/public/html/auth-start.html#L51-L56))
6. Sur le site du fournisseur, l’utilisateur se connecte et autorise l’accès au bot.
7. Le fournisseur dirige l’utilisateur vers la page de redirection OAuth du bot avec un code d’autorisation.
8. Le bot Echange le code d’autorisation pour un jeton d’accès et, de façon **provisoire** , associe le jeton à l’utilisateur qui a initié le flux de connexion. Ci-dessous, nous appelons ce *jeton provisoire*.
    * Dans l’exemple, le bot associe la valeur du `state` paramètre à l’ID de l’utilisateur qui a initié le processus de connexion afin qu’il puisse le faire correspondre ultérieurement `state` à la valeur renvoyée par le fournisseur d’identité. ([Afficher le code](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L70-L99))
    * **Important**: le robot stocke le jeton qu’il reçoit du fournisseur d’identité et l’associe à un utilisateur spécifique, mais il est marqué comme « validation en attente ». Le jeton provisoire ne peut pas être utilisé pour le moment ; elle doit être encore validée :
      1. **Validez le contenu reçu du fournisseur d’identité.** La valeur du `state` paramètre doit être confirmée par rapport à ce qui a été enregistré précédemment. 
      1. **Valider les éléments reçus par Teams.** Une validation de l' [authentification en deux étapes](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) est effectuée afin de s’assurer que l’utilisateur qui a autorisé le robot avec le fournisseur d’identité est le même utilisateur en conversation avec le bot. Cela empêche [les attaques de l’intercepteur et de l'](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) [hameçonnage](https://en.wikipedia.org/wiki/Phishing) . Le bot génère un code de vérification et le stocke associé à l’utilisateur. Le code de vérification est envoyé automatiquement par Teams, comme décrit ci-dessous. ([Afficher le code](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L100-L113))
9. Le rappel OAuth affiche une page qui appelle `notifySuccess("<verification code>")`. ([Afficher le code](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/master/src/views/oauth-callback-success.hbs))
10. Teams ferme la fenêtre contextuelle et envoie le `<verification code>` message envoyé à `notifySuccess()` nouveau au bot. Le bot reçoit un [](/bot-framework/dotnet/bot-builder-dotnet-activities#invoke) message d’appel `name = signin/verifyState`avec.
11. Le bot compare le code de vérification entrant au code de vérification stocké avec le jeton provisoire de l’utilisateur. ([Afficher le code](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L127-L140))
12. Si elles correspondent, le robot marque le jeton comme validé et prêt à être utilisé. Dans le cas contraire, le flux d’authentification échoue et le bot supprime le jeton provisoire.

> [!NOTE]
> Si vous rencontrez des problèmes avec l’authentification sur mobile, vérifiez que votre SDK JavaScript est mis à jour vers la version 1.4.1 ou ultérieure.

## <a name="samples"></a>Exemples

Pour obtenir un exemple de code illustrant le processus d’authentification du bot, voir :

* [Exemple d’authentification Microsoft teams bot (node. js)](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)

## <a name="more-details"></a>Plus de détails

Pour obtenir des procédures pas à pas d’implémentation détaillées pour l’authentification de bot ciblant Azure AD, voir :

* [Ajouter l’authentification à votre robot teams](add-authentication.md)
