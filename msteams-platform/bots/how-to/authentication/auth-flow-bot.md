---
title: Microsoft Teams Flux d’authentification pour les bots
description: Décrit le flux Microsoft Teams’authentification dans les bots
keywords: bots de flux d’authentification Teams
localization_priority: Normal
ms.topic: overview
ms.openlocfilehash: f3bf73c105dc38e1cea515bfa7bb7d5324b02ce4
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565901"
---
# <a name="authentication-flow-for-bots-in-microsoft-teams"></a>Flux d’authentification pour les bots dans Microsoft Teams

OAuth 2.0 est une norme ouverte pour l’authentification et l’autorisation utilisée par Azure Active Directory (Azure AD) et de nombreux autres fournisseurs d’identité. Une compréhension de base d’OAuth 2.0 est une condition préalable à l’utilisation de l’authentification dans Teams; [Voici une bonne vue d’ensemble](https://aaronparecki.com/oauth-2-simplified/) plus facile à suivre que la [spécification formelle.](https://oauth.net/2/) Le flux d’authentification pour les onglets et les bots est légèrement différent : les onglets sont très similaires aux sites web afin qu’ils peuvent utiliser OAuth 2.0 directement, tandis que les bots ne le sont pas et doivent faire quelques choses différemment, mais les concepts de base sont identiques.

Consultez l’exemple GitHub [](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-auth/nodejs) d’authentification de Microsoft Teams pour obtenir un exemple de flux d’authentification pour les bots utilisant Node.js et le type d’octroi de code d’autorisation [OAuth 2.0.](https://oauth.net/2/grant-types/authorization-code/)

![Diagramme de séquence d’authentification de bot](../../../assets/images/authentication/bot_auth_sequence_diagram.png)

1. L’utilisateur envoie un message au bot.
2. Le bot détermine si l’utilisateur doit se connecter.
   Dans cet exemple, le bot stocke le jeton d’accès dans son magasin de données utilisateur. Il demande à l’utilisateur de se connecter s’il n’a pas de jeton validé pour le fournisseur d’identité sélectionné. ([Afficher le code](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/utils/AuthenticationUtils.ts#L58-L76))
3. Le bot construit l’URL vers la page de démarrage du flux d’authentification et envoie une carte à l’utilisateur avec une `signin` action. ([Afficher le code](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L160-L190))</br>
    Comme les autres flux d’authentification d’application dans Teams, la page de démarrage doit se trouver dans un domaine qui figure dans votre liste et dans le même domaine que la page de `validDomains` redirection post-connexion.
    > [!IMPORTANT] 
    > Le flux d’octroi de code d’autorisation OAuth 2.0 appelle un paramètre dans la demande d’authentification qui contient un jeton de session unique pour empêcher une attaque par falsification de demande entre `state` [sites.](https://en.wikipedia.org/wiki/Cross-site_request_forgery) L’exemple utilise un GUID généré de manière aléatoire.
4. Lorsque l’utilisateur sélectionne *le* bouton de Teams, il ouvre une fenêtre popup et navigue vers la page de démarrage.
   > [!NOTE]
   > La taille de la fenêtre pop-up peut être contrôlée par les paramètres de chaîne de requête largeur et hauteur dans l’URL. Par exemple, si vous ajoutez width=500 et height=500, la taille de la fenêtre pop-up est de 500 x 500 pixels. Teams affiche la fenêtre pop-up avec la taille de pixel donnée, jusqu’à un pourcentage maximal de la taille de la fenêtre principale.

5. La page de démarrage redirige l’utilisateur vers le point de terminaison du fournisseur `authorize` d’identité. ([Afficher le code](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/public/html/auth-start.html#L51-L56))
6. Sur le site du fournisseur, l’utilisateur se signe et accorde l’accès au bot.
7. Le fournisseur redirige l’utilisateur vers la page de redirection OAuth du bot avec un code d’autorisation.
8. Le bot échange le code d’autorisation  contre un jeton d’accès et associe provisoirement le jeton à l’utilisateur qui a initié le flux de la signature. Ci-dessous, nous appelons cela *un jeton provisoire*.
    * Dans l’exemple, le bot associe la valeur du paramètre à l’ID de l’utilisateur qui a initié le processus de signature afin qu’il puisse ultérieurement la faire correspondre à la valeur renvoyée par le fournisseur `state` `state` d’identité. ([Afficher le code](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L70-L99))
      > [!IMPORTANT] 
      > Le bot stocke le jeton qu’il reçoit du fournisseur d’identité et l’associe à un utilisateur spécifique, mais il est marqué comme « validation en attente ». 
    * Le jeton provisoire ne peut pas être utilisé sans validation supplémentaire.
      1. **Valider les informations reçues du fournisseur d’identité.** La valeur du paramètre doit être confirmée par rapport à ce `state` qui a été enregistré précédemment. 
      1. **Validez ce qui est reçu de Teams.** Une [validation](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) d’authentification en deux étapes est effectuée pour s’assurer que l’utilisateur qui a autorisé le bot auprès du fournisseur d’identité est le même utilisateur qui discute avec le bot. Cela protège contre [les attaques de l’homme au](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) milieu et les [attaques par hameçonnage.](https://en.wikipedia.org/wiki/Phishing) Le bot génère un code de vérification et le stocke, associé à l’utilisateur. Le code de vérification est envoyé automatiquement par Teams comme décrit ci-dessous. ([Afficher le code](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L100-L113))
9. Le rappel OAuth rend une page qui appelle `notifySuccess("<verification code>")` . ([Afficher le code](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/master/src/views/oauth-callback-success.hbs))
10. Teams ferme la fenêtre pop-up et renvoie le message envoyé `<verification code>` `notifySuccess()` au bot. Le bot reçoit un message [d’appel](/bot-framework/dotnet/bot-builder-dotnet-activities#invoke) avec `name = signin/verifyState` .
11. Le bot vérifie le code de vérification entrant par rapport au code de vérification stocké avec le jeton provisoire de l’utilisateur. ([Afficher le code](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L127-L140))
12. S’ils correspondent, le bot marque le jeton comme validé et prêt à être utilisé. Sinon, le flux d’th échoue et le bot supprime le jeton provisoire.

    > [!NOTE]
    > Si vous avez des problèmes avec l’authentification sur mobile, assurez-vous que votre SDK JavaScript est mis à jour vers la version 1.4.1 ou ultérieure.

## <a name="code-sample"></a>Exemple de code

Exemple de code montrant le processus d’authentification du bot :

| **Exemple de nom** | **Description** | **Node.js** | **.NET** | **Python** |
|-----------------|----------------|--------------|----------|-----------|
| Teams’authentification | Cet exemple illustre l’authentification dans Microsoft Teams applications. | [View](https://github.com/OfficeDev/microsoft-teams-sample-auth-node) | | |
| Authentification bot | Cet exemple vous apprendre à utiliser l’authentification pour un runnning de bot dans Microsoft Teams | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/46.teams-auth)

## <a name="see-also"></a>Voir aussi

[Ajouter l’authentification à Teams bot](add-authentication.md)
