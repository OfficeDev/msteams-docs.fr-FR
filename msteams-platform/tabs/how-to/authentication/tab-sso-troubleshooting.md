---
title: Résolution des problèmes d'authentification pour les onglets utilisant SSO dans Teams
description: Dépannage de l'authentification SSO dans Teams et comment l'utiliser dans les onglets
ms.topic: how-to
ms.localizationpriority: high
keywords: équipes onglets d'authentification Microsoft Azure Active Directory (Azure AD) erreurs SSO questions
ms.openlocfilehash: fa17ffef08f85124a230f76419158f4216f55416
ms.sourcegitcommit: 07f41abbeb1572a306a789485953c5588d65051e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/06/2022
ms.locfileid: "66658951"
---
# <a name="troubleshoot-sso-authentication-in-teams"></a>Résolution des problèmes d'authentification SSO dans Teams

Voici une liste de problèmes et de questions concernant le SSO, et la façon dont vous pouvez les résoudre.
<br>

## <a name="support-for-microsoft-graph"></a>Prise en charge de Microsoft Graph

<br>
<details>
<summary>1. L' API graphique fonctionne-t-elle dans Postman ?</summary>
<br>
Vous pouvez utiliser la collection Microsoft Graph Postman avec les API Microsoft Graph.

Pour obtenir plus d’informations, consultez [Utilisation de Postman avec l’API Microsoft Graph](/graph/use-postman).
</details>
<br>
<details>
<summary>2. L'API graphique fonctionne-t-elle dans l'explorateur graphique de Microsoft ?</summary>
<br>
Oui, l'API graphique fonctionne dans l'explorateur graphique de Microsoft.

Pour plus d'informations, voir [Explorateur de graphiques](https://developer.microsoft.com/graph/graph-explorer).

</details>
<br>

## <a name="error-messages-and-how-to-handle-them"></a>Messages d'erreur et comment les traiter

<br>
<details>
<summary>1. Erreur : absence de consentement.</summary>
<br>
Lorsqu' Azure AD reçoit une demande d'accès à une ressource Microsoft Graph, il vérifie si l'utilisateur (ou l'administrateur du locataire) a donné son consentement pour cette ressource. S'il n'y a pas d'enregistrement du consentement de l'utilisateur ou de l'administrateur, Azure AD envoie un message d'erreur à votre service Web.

Votre code doit indiquer au client (par exemple, dans le corps d'une réponse 403 Forbidden) comment traiter l'erreur :

- Si l'application de l'onglet nécessite des scopes Microsoft Graph pour lesquels seul un administrateur peut donner son accord, votre code devrait générer une erreur.
- Si les seules étendues requises peuvent être envoyées par l’utilisateur, votre code doit basculer vers un autre système d’authentification des utilisateurs.

</details>
<br>
<details>
<summary>2. Erreur : Portée manquante (permission).</summary>
<br>
Cette erreur n'apparaît que pendant le développement.

Pour gérer cette erreur, votre code côté serveur doit envoyer une réponse 403 Forbidden au client. Il doit consigner l'erreur dans la console ou l'enregistrer dans un journal.
</details>
<br>
<details>
<summary>3. Erreur : Audience invalide dans le jeton d'accès pour Microsoft Graph.</summary>
<br>
Le code côté serveur doit envoyer une réponse 403 Forbidden au client pour montrer un message à l'utilisateur. Il est recommandé de consigner également l'erreur dans la console, ou de l'enregistrer dans un journal.
</details>
<br>
<details>
<summary>4. Erreur : Le nom d'hôte ne doit pas être basé sur un domaine déjà possédé.</summary>
<br>
Vous pouvez obtenir cette erreur dans l'un des deux scénarios suivants :

1. Le domaine personnalisé n'est pas ajouté à Azure AD. Pour ajouter un domaine personnalisé à Azure [AD et l'enregistrer, suivez la procédure d'ajout d'un nom de domaine personnalisé à Azure AD](/azure/active-directory/fundamentals/add-custom-domain), puis suivez à nouveau les étapes de [configuration de la portée du jeton ](tab-sso-register-aad.md#configure-scope-for-access-token)d'accès.
1. Vous n'êtes pas connecté avec des informations d'identification d'administrateur dans l'hébergement Microsoft 365. Connectez-vous à Microsoft 365 en tant qu'administrateur.

</details>
<br>
<details>
<summary>5. Erreur : Le nom de l'utilisateur principal (UPN) n'a pas été reçu dans le jeton d'accès renvoyé.</summary>
<br>
Vous pouvez ajouter l' UPN comme une demande facultative dans Azure AD.

Pour plus d'informations, voir [Fournir des revendications facultatives à votre application ](/azure/active-directory/develop/active-directory-optional-claims)et[ des jetons d'accès](/azure/active-directory/develop/access-tokens).
</details>
<br>
<details>
<summary>6. Erreur : Teams SDK Erreur : resourceDisabled.</summary>
<br>
Pour éviter cette erreur, assurez-vous que l' URI de l' ID de l'application est configuré correctement dans l'enregistrement des applications Azure AD et dans votre client Teams.

Pour plus d'informations sur l' URI de l'application, voir [Pour exposer une API ](tab-sso-register-aad.md#to-expose-an-api).

</details>
<br>

<details>
<summary>7. Erreur : Erreur générique lors de l'exécution de l'application d'onglet.</summary>
<br>
Une erreur générique peut apparaître lorsqu'une ou plusieurs des configurations d'applications effectuées dans Azure AD sont incorrectes. Pour résoudre cette erreur, vérifiez si les détails de l'application configurés dans votre code et dans le manifeste Teams correspondent aux valeurs dans Azure AD.

L'image suivante montre un exemple des détails de l'application configurés dans Azure AD.

:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/azure-app-details.png" alt-text="Valeurs de configuration des applications dans Azure AD":::

Vérifiez que les valeurs suivantes correspondent entre Azure AD, le code côté client et le manifeste de l'application Teams :

- **App ID** : L' app ID que vous avez généré dans Azure AD doit être le même dans le code et dans le fichier manifest de Teams. Vérifiez que l 'ID de l'application dans le manifeste Teams correspond à l' ID de **l'application (client)** dans Azure AD.

- **Secret d'application** : le secret d'application configuré dans le backend de votre application doit correspondre aux informations d'identification du **client dans Azure** AD.
    Vous devez également vérifier si le secret du client a expiré.

- **URI de l'application** : L'URI de l'application dans le code et dans le fichier manifeste de **l'application Teams doit correspondre à l' URI** de l'application dans Azure AD.

- **Autorisations de l'application** : Vérifiez si les autorisations que vous avez définies dans le champ d'application correspondent aux besoins de votre application. Si oui, vérifiez si elles ont été accordées à l'utilisateur dans le jeton d'accès.

- **Consentement de l'administrateur** : si un champ d'application nécessite le consentement de l'administrateur, vérifiez si le consentement a été accordé à l'utilisateur pour ce champ d'application particulier.

En outre, inspectez le jeton d'accès qui a été envoyé à l'application de l'onglet pour vérifier si les valeurs suivantes sont correctes :

- **Audience (aud)** : Vérifiez si l'identifiant de l'application dans le jeton est correct comme indiqué dans Azure AD.
- **Tenant Id(tid)** : Vérifier si le locataire mentionné dans le jeton est correct.
- **Identité de l'utilisateur (preferred_username)** : Vérifier si l'identité de l'utilisateur correspond au nom d'utilisateur dans la demande de jeton d'accès pour la portée à laquelle l'utilisateur actuel veut accéder.
- **Scopes (scp)** : Vérifier si le scope pour lequel le jeton d'accès est demandé est correct, et tel que défini dans Azure AD.
- **Azure AD version 1.0 ou 2.0 (ver)** : Vérifier si la version d' Azure AD est correcte.

Vous pouvez utiliser [JWT](https://jwt.ms) pour inspecter le jeton.

</details>
