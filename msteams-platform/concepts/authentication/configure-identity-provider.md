---
title: Configurer les fournisseurs d’identité OAuth 2.0
description: Décrit comment configurer des fournisseurs d’identité axés sur Microsoft Azure Active Directory (Azure AD)
ms.topic: how-to
ms.localizationpriority: medium
keywords: fournisseur d’identité oauth Microsoft Azure Active Directory (Azure AD) teams
ms.openlocfilehash: 93622275a8bfc9007af751d8b9f6304a73450ec7
ms.sourcegitcommit: 90587b1ec04bf20d716ed6feb8ccca4313e87f8c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/10/2022
ms.locfileid: "62517973"
---
# <a name="configure-identity-providers"></a>Configurer les fournisseurs d’identité

## <a name="configuring-an-application-to-use-microsoft-azure-active-directory-azure-ad-as-an-identity-provider"></a>Configuration d’une application pour utiliser Microsoft Azure Active Directory (Azure AD) en tant que fournisseur d’identité

Les fournisseurs d’identité qui la prise en charge d’OAuth 2.0 n’authentifiera pas les demandes provenant d’applications inconnues ; doivent être inscrites à l’avance. Pour ce faire, Microsoft Azure Active Directory (Azure AD), suivez les étapes suivantes :

1. Ouvrez le [portail d’inscription des applications](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade).

2. Sélectionnez votre application pour afficher ses propriétés ou sélectionnez le bouton « Nouvelle inscription ». Recherchez la section **URI de** redirection pour l’application.

3. **Sélectionnez Web** dans le menu déroulant. Mettez à jour l’URL de votre point de terminaison d’authentification. Pour les exemples d’applications TypeScript/Node.js et C# sur GitHub, les URL de redirection sont similaires à ce qui suit :

    Rediriger les URL : `https://<hostname>/bot-auth/simple-start`

Remplacez `<hostname>` par votre hôte réel, qui peut être un site d’hébergement dédié tel qu’Azure, Glitch ou un tunnel ngrok vers localhost sur votre ordinateur de développement tel que `abcd1234.ngrok.io`. Vous n’avez peut-être pas ces informations si vous n’avez pas terminé ou hébergé votre application (ou l’exemple d’application mentionné ci-dessus), mais vous pouvez toujours revenir à cette page lorsque ces informations sont connues.

## <a name="other-authentication-providers"></a>Autres fournisseurs d’authentification

* **LinkedIn :** Suivez les instructions de [configuration de votre application LinkedIn](/linkedin/talent/apply-with-linkedin)

* **Google :** Obtenir les informations d’identification du client OAuth 2.0 à partir de la [console d’API Google](https://console.developers.google.com/)
