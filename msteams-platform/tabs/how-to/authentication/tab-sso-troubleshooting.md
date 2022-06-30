---
title: Résolution des problèmes d’authentification pour les onglets à l’aide de l’authentification unique dans Teams
description: Résolution des problèmes d’authentification unique dans Teams et comment l’utiliser dans des onglets
ms.topic: how-to
ms.localizationpriority: medium
keywords: Questions sur les erreurs d’authentification unique des onglets d’authentification teams Microsoft Azure Active Directory (Azure AD)
ms.openlocfilehash: 93365732ee284cd8cb903f7535d2770d0154d417
ms.sourcegitcommit: c398dfdae9ed96f12e1401ac7c8d0228ff9c0a2b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/30/2022
ms.locfileid: "66558421"
---
# <a name="troubleshoot-sso-authentication-in-teams"></a>Résoudre les problèmes d’authentification unique dans Teams

Voici une liste de problèmes et de questions sur l’authentification unique, et comment vous pouvez les résoudre.
<br>

## <a name="support-for-microsoft-graph"></a>Prise en charge de Microsoft Graph

<br>
<details>
<summary>1. API Graph fonctionne-t-il dans Postman ?</summary>
<br>
Vous pouvez utiliser la collection Microsoft Graph Postman avec les API Microsoft Graph.

Pour obtenir plus d’informations, consultez [Utilisation de Postman avec l’API Microsoft Graph](/graph/use-postman).
</details>
<br>
<details>
<summary>2. API Graph fonctionne-t-il dans l’Explorateur Microsoft Graph ?</summary>
<br>
Oui, API Graph fonctionne dans l’Explorateur Microsoft Graph.

Pour plus d’informations, consultez [l’Explorateur Graph](https://developer.microsoft.com/graph/graph-explorer).

</details>
<br>

## <a name="error-messages-and-how-to-handle-them"></a>Messages d’erreur et comment les gérer

<br>
<details>
<summary>1. Erreur : consentement manquant.</summary>
<br>
Quand Azure AD reçoit une demande d’accès à une ressource Microsoft Graph, il vérifie si l’utilisateur (ou l’administrateur du locataire) a donné son consentement pour cette ressource. S’il n’existe aucun enregistrement de consentement de la part de l’utilisateur ou de l’administrateur, Azure AD envoie un message d’erreur à votre service web.

Votre code doit indiquer au client (par exemple, dans le corps d’une réponse 403 Interdit) comment gérer l’erreur :

- Si l’application onglet a besoin d’étendues Microsoft Graph pour lesquelles seul un administrateur peut donner son consentement, votre code doit générer une erreur.
- Si les seules étendues requises peuvent être envoyées par l’utilisateur, votre code doit basculer vers un autre système d’authentification des utilisateurs.

</details>
<br>
<details>
<summary>2. Erreur : Étendue manquante (autorisation).</summary>
<br>
Cette erreur est visible uniquement pendant le développement.

Pour gérer cette erreur, votre code côté serveur doit envoyer une réponse 403 Interdit au client. Il doit consigner l’erreur dans la console ou l’enregistrer dans un journal.
</details>
<br>
<details>
<summary>3. Erreur : Audience non valide dans le jeton d’accès pour Microsoft Graph.</summary>
<br>
Le code côté serveur doit envoyer une réponse 403 Interdit au client pour afficher un message à l’utilisateur. Il est recommandé de consigner également l’erreur dans la console ou de l’enregistrer dans un journal.
</details>
<br>
<details>
<summary>4. Erreur : le nom d’hôte ne doit pas être basé sur un domaine déjà détenu.</summary>
<br>
Vous pouvez obtenir cette erreur dans l’un des deux scénarios suivants :

1. Le domaine personnalisé n’est pas ajouté à Azure AD. Pour ajouter un domaine personnalisé à Azure AD et l’inscrire, suivez la procédure [d’ajout d’un nom de domaine personnalisé à la procédure Azure AD](/azure/active-directory/fundamentals/add-custom-domain) , puis suivez les étapes pour configurer à nouveau [l’étendue du jeton d’accès](tab-sso-register-aad.md#configure-scope-for-access-token) .
1. Vous n’êtes pas connecté avec les informations d’identification d’administrateur dans le client Microsoft 365. Connectez-vous à Microsoft 365 en tant qu’administrateur.

</details>
<br>
<details>
<summary>5. Erreur : Nom d’utilisateur principal (UPN) non reçu dans le jeton d’accès retourné.</summary>
<br>
Vous pouvez ajouter UPN en tant que revendication facultative dans Azure AD.

Pour plus d’informations, consultez [Fournir des revendications facultatives à votre application](/azure/active-directory/develop/active-directory-optional-claims) et [des jetons d’accès](/azure/active-directory/develop/access-tokens).
</details>
<br>
<details>
<summary>6. Erreur : Erreur du Kit de développement logiciel (SDK) Teams : resourceDisabled.</summary>
<br>
Pour éviter cette erreur, assurez-vous que l’URI d’ID d’application est correctement configuré dans l’inscription d’application Azure AD et dans votre client Teams.

Pour plus d’informations sur l’URI d’ID d’application, consultez [Pour exposer une API](tab-sso-register-aad.md#to-expose-an-api).

</details>
<br>

<details>
<summary>7. Erreur : Erreur générique lors de l’exécution de l’application onglet.</summary>
<br>
Une erreur générique peut apparaître quand une ou plusieurs configurations d’application effectuées dans Azure AD sont incorrectes. Pour résoudre cette erreur, vérifiez si les détails de l’application configurés dans votre code et le manifeste Teams correspondent aux valeurs dans Azure AD.

L’image suivante montre un exemple des détails de l’application configurés dans Azure AD.

:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/azure-app-details.png" alt-text="Valeurs de configuration d’application dans Azure AD":::

Vérifiez que les valeurs suivantes correspondent entre Azure AD, le code côté client et le manifeste de l’application Teams :

- **ID d’application** : l’ID d’application que vous avez généré dans Azure AD doit être le même dans le code et dans le fichier manifeste Teams. Vérifiez que l’ID d’application dans le manifeste Teams correspond à **l’ID d’application (client)** dans Azure AD.

- **Secret d’application** : le secret d’application configuré dans le backend de votre application doit correspondre aux **informations d’identification du client** dans Azure AD.
    Vous devez également vérifier si la clé secrète client a expiré.

- **URI d’ID** d’application : l’URI d’ID d’application dans le code et dans le fichier manifeste de l’application Teams doit correspondre à **l’URI iD** d’application dans Azure AD.

- **Autorisations d’application** : vérifiez si les autorisations que vous avez définies dans l’étendue sont en fonction des besoins de votre application. Si c’est le cas, vérifiez s’ils ont été accordés à l’utilisateur dans le jeton d’accès.

- **Administration consentement** : si une étendue requiert le consentement de l’administrateur, vérifiez si le consentement a été accordé pour l’étendue particulière à l’utilisateur.

En outre, examinez le jeton d’accès qui a été envoyé à l’application onglet pour vérifier si les valeurs suivantes sont correctes :

- **Audience (aud)** : vérifiez si l’ID d’application dans le jeton est correct comme indiqué dans Azure AD.
- **ID de locataire (tid)** : vérifiez si le locataire mentionné dans le jeton est correct.
- Identité de l’utilisateur **(preferred_username)** : vérifiez si l’identité de l’utilisateur correspond au nom d’utilisateur dans la demande de jeton d’accès pour l’étendue à laquelle l’utilisateur actuel souhaite accéder.
- **Étendues (scp)** : vérifiez si l’étendue pour laquelle le jeton d’accès est demandé est correcte et telle qu’elle est définie dans Azure AD.
- **Azure AD version 1.0 ou 2.0 (ver)** : vérifiez si la version d’Azure AD est correcte.

Vous pouvez utiliser [JWT](https://jwt.ms) pour inspecter le jeton.

</details>
