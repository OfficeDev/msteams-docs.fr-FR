---
title: Configurer des fournisseurs d’identité OAuth 2.0
description: Dans ce module, découvrez comment configurer des fournisseurs d’identité en se concentrant sur Microsoft Azure Active Directory (Azure AD)
ms.topic: how-to
ms.localizationpriority: medium
ms.openlocfilehash: 2d344fb5ffcbde35ad9e85eed9ea662d2a0ca9f6
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143444"
---
# <a name="configure-identity-providers"></a>Configurer les fournisseurs d’identité

## <a name="configuring-an-application-to-use-azure-ad-as-an-identity-provider"></a>Configuration d’une application pour utiliser Azure AD en tant que fournisseur d’identité

Les fournisseurs d’identité qui prennent en charge OAuth 2.0 n’authentifient pas les demandes provenant d’applications inconnues ; doivent être inscrites à l’avance. Pour ce faire avec Azure AD, procédez comme suit :

1. Ouvrez le [portail d’inscription d’application](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade).

2. Sélectionnez votre application pour afficher ses propriétés, ou sélectionnez le bouton « Nouvelle inscription ». Recherchez la section **URI de redirection** pour l’application.

3. Sélectionnez **Web** dans le menu déroulant. Mettez à jour l’URL vers votre point de terminaison d’authentification. Pour les exemples d’applications TypeScript/Node.js et C# sur GitHub, les URL de redirection sont similaires aux suivantes :

    URL de redirection : `https://<hostname>/bot-auth/simple-start`

Remplacez `<hostname>` par votre hôte réel, qui peut être un site d’hébergement dédié tel qu’Azure, Glitch ou un tunnel ngrok vers localhost sur votre machine de développement, par exemple `abcd1234.ngrok.io`. Vous ne disposez peut-être pas de ces informations si vous n’avez pas terminé ou hébergé votre application (ou l’exemple d’application mentionné ci-dessus), mais vous pouvez toujours revenir à cette page lorsque ces informations sont connues.

## <a name="other-authentication-providers"></a>Autres fournisseurs d’authentification

* **Linkedin :** Suivez les instructions de [configuration de votre application LinkedIn](/linkedin/talent/apply-with-linkedin)

* **Google :** Obtenir les informations d’identification du client OAuth 2.0 à partir de la [console d’API Google](https://console.developers.google.com/)

* **Fournisseurs OAuth externes à partir d’onglets :** Pour plus d’informations, consultez [Utiliser des fournisseurs OAuth externes](../../tabs/how-to/authentication/auth-oauth-provider.md)

## <a name="see-also"></a>Voir aussi

* [Authentifier un utilisateur dans un bot Microsoft Teams](../../resources/bot-v3/bot-authentication/auth-bot-AAD.md)
* [Prise en charge de l'authentification unique (SSO) pour les onglets](../../tabs/how-to/authentication/tab-sso-overview.md)
* [Authentifier un utilisateur dans un onglet Microsoft Teams](../../tabs/how-to/authentication/auth-tab-aad.md)
