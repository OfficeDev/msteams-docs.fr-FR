---
title: Flux d’authentification Microsoft Teams pour les bots
description: Décrit le flux d’authentification Microsoft Teams dans les bots avec un exemple de code.
keywords: bots de flux d’authentification Teams
ms.localizationpriority: high
ms.topic: overview
ms.openlocfilehash: f18d5a03ed62b55d162c7e10ba1546e4051f3744
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111849"
---
# <a name="authentication-flow-for-bots-in-microsoft-teams"></a>Flux d’authentification pour les bots dans Microsoft Teams

OAuth 2.0 est une norme ouverte pour l’authentification et l’autorisation utilisées par Azure Active Directory et de nombreux autres fournisseurs d’identité. Une compréhension de base d’OAuth 2.0 est un prérequis pour l’utilisation de l’authentification dans Teams ; [voici une bonne vue d’ensemble](https://aaronparecki.com/oauth-2-simplified/) qui est plus facile à suivre que la [spécification formelle](https://oauth.net/2/). Le flux d’authentification pour les onglets et les bots est un peu différent – des sites web. Ils peuvent donc utiliser OAuth 2.0 directement, tandis que les bots ne le peuvent pas et doivent effectuer quelques actions différemment – mais les concepts de base sont identiques.

Consultez le dépôt GitHub [Exemple d’authentification Microsoft Teams](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-auth/nodejs) pour obtenir un exemple illustrant le flux d’authentification pour les bots utilisant Node.js et le [type d’octroi de code d’autorisation OAuth 2.0](https://oauth.net/2/grant-types/authorization-code/).

![Diagramme de séquence d’authentification de bot](../../../assets/images/authentication/bot_auth_sequence_diagram.png)

1. L’utilisateur envoie un message au bot.
2. Le bot détermine si l’utilisateur doit se connecter.
   Dans cet exemple, le bot stocke le jeton d’accès dans son magasin de données utilisateur. Il demande à l’utilisateur de se connecter s’il n’a pas de jeton validé pour le fournisseur d’identité sélectionné. ([Afficher le code](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/utils/AuthenticationUtils.ts#L58-L76))
3. Le bot construit l’URL de la page de démarrage du flux d’authentification et envoie une carte à l’utilisateur avec une action de `signin`. ([Afficher le code](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L160-L190))</br>
    Comme d’autres flux d’authentification d’application dans Teams, la page de démarrage doit se trouver dans un domaine figurant dans votre liste `validDomains` et dans le même domaine que la page de redirection post-connexion.
    > [!IMPORTANT]
    > Le flux d’octroi de code d’autorisation OAuth 2.0 appelle un paramètre `state` dans la demande d’authentification, qui contient un jeton de session unique pour empêcher une [attaque de falsification de requête intersites](https://en.wikipedia.org/wiki/Cross-site_request_forgery). L’exemple utilise un GUID généré de manière aléatoire.
4. Lorsque l’utilisateur sélectionne le bouton *se connecter*, Teams ouvre une fenêtre contextuelle et accède à la page de démarrage.
   > [!NOTE]
   > La taille de la fenêtre contextuelle peut être contrôlée par le biais de paramètres de chaîne de requête de largeur et de hauteur dans l’URL. Par exemple, si vous ajoutez width=600 et height=600, la taille de la fenêtre contextuelle est de 600 x 600 pixels. La taille réelle de la fenêtre contextuelle est limitée en pourcentage par rapport à la taille de la fenêtre principale Teams. Si la fenêtre Teams est petite, la fenêtre contextuelle est plus petite que les dimensions spécifiées.

5. La page de démarrage redirige l’utilisateur vers le point de terminaison `authorize` du fournisseur d’identité. ([Afficher le code](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/public/html/auth-start.html#L51-L56))
6. Sur le site du fournisseur, l’utilisateur se connecte et accorde l’accès au bot.
7. Le fournisseur dirige l’utilisateur vers la page de redirection OAuth du bot avec un code d’autorisation.
8. Le bot utilise le code d’autorisation contre un jeton d’accès et **provisoirement** associe le jeton à l’utilisateur qui a lancé le flux de connexion. Ci-dessous, nous appelons cela un *jeton provisoire*.
    * Dans l’exemple, le bot associe la valeur du paramètre `state` à l’ID de l’utilisateur qui a lancé le processus de connexion afin qu’il puisse la mettre en correspondance ultérieurement avec la valeur `state` retournée par le fournisseur d’identité. ([Afficher le code](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L70-L99))
      > [!IMPORTANT]
      > Le bot stocke le jeton qu’il reçoit du fournisseur d’identité et l’associe à un utilisateur spécifique, mais il est marqué de « validation en attente ».
    * Le jeton provisoire ne peut pas être utilisé sans validation supplémentaire.
      1. **Validez ce qui a été reçu du fournisseur d’identité.** La valeur du paramètre `state` doit être confirmée par rapport à ce qui a été enregistré précédemment.
      1. **Valider ce qui est reçu de Teams.** Une [validation de l’authentification en deux étapes](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) est effectuée pour s’assurer que l’utilisateur qui a autorisé le bot avec le fournisseur d’identité est le même utilisateur que celui qui discute avec le bot. Cela protège contre [l’intercepteur](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) et les attaques par [hameçonnage](https://en.wikipedia.org/wiki/Phishing) . Le bot génère un code de vérification et le stocke, en l'associant à l'utilisateur. Le code de vérification est envoyé automatiquement par Teams, comme décrit ci-dessous. ([Afficher le code](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L100-L113))
9. Le rappel OAuth affiche une page qui appelle `notifySuccess("<verification code>")`. ([Afficher le code](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/master/src/views/oauth-callback-success.hbs))
10. Teams ferme la fenêtre contextuelle et renvoie le `<verification code>` envoyé à `notifySuccess()` au bot. Le bot reçoit un message [d’appel](/bot-framework/dotnet/bot-builder-dotnet-activities#invoke) avec `name = signin/verifyState`.
11. Le bot examine le code de vérification entrant par rapport au code de vérification stocké avec le jeton provisoire de l’utilisateur. ([Afficher le code](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L127-L140))
12. S’ils correspondent, le bot marque le jeton comme validé et prêt à être utilisé. Sinon, le flux d’authentification échoue et le bot supprime le jeton provisoire.

    > [!NOTE]
    > Si vous rencontrez des problèmes d’authentification sur les appareils mobiles, vérifiez que votre Kit de développement logiciel (SDK) JavaScript est mis à jour vers la version 1.4.1 ou ultérieure.

## <a name="code-sample"></a>Exemple de code

Exemple de code montrant le processus d’authentification du bot :

| **Exemple de nom** | **Description** | **Node.js** | **.NET** | **Python** |
|-----------------|----------------|--------------|----------|-----------|
| Authentification Teams | Cet exemple illustre l’authentification dans les applications Microsoft Teams. | [View](https://github.com/OfficeDev/microsoft-teams-sample-auth-node) | | |
| Authentification de bot | Cet exemple montre comment utiliser l’authentification pour un bot s’exécutant dans Microsoft Teams | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/46.teams-auth)

## <a name="see-also"></a>Voir aussi

[Ajouter l’authentification à votre bot Teams](add-authentication.md)
