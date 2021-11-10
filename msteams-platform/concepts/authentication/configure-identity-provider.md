---
title: Configurer les fournisseurs d’identité OAuth 2.0
description: Décrit comment configurer des fournisseurs d’identité axés sur les Azure AD
ms.topic: how-to
ms.localizationpriority: medium
keywords: Authentification Teams AAD fournisseur d’identité oauth
ms.openlocfilehash: cae2cc3d2feba8c17ad895864fd1b5995095f71b
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/10/2021
ms.locfileid: "60887433"
---
# <a name="configure-identity-providers"></a>Configurer les fournisseurs d’identité

## <a name="configuring-an-application-to-use-azure-active-directory-as-an-identity-provider"></a>Configuration d’une application pour utiliser Azure Active Directory comme fournisseur d’identité

Les fournisseurs d’identité qui la prise en charge d’OAuth 2.0 n’authentifiera pas les demandes provenant d’applications inconnues ; doivent être inscrites à l’avance. Pour ce faire, Azure AD, suivez les étapes suivantes :

1. Ouvrez le [portail d’inscription des applications.](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade)

2. Sélectionnez votre application pour afficher ses propriétés ou sélectionnez le bouton « Nouvelle inscription ». Recherchez la section **URI de** redirection pour l’application.

3. Sélectionnez **Web** dans le menu déroulant. Mettez à jour l’URL de votre point de terminaison d’authentification. Pour les exemples d’applications TypeScript/Node.js et C# sur GitHub, les URL de redirection sont similaires à ce qui suit :

    Rediriger les URL : `https://<hostname>/bot-auth/simple-start`

Remplacez par votre hôte réel, qui peut être un site d’hébergement dédié tel qu’Azure, Glitch ou un tunnel ngrok vers localhost sur votre ordinateur de développement tel `<hostname>` que `abcd1234.ngrok.io` . Vous n’avez peut-être pas ces informations si vous n’avez pas terminé ou hébergé votre application (ou l’exemple d’application mentionné ci-dessus), mais vous pouvez toujours revenir à cette page lorsque ces informations sont connues.

## <a name="other-authentication-providers"></a>Autres fournisseurs d’authentification

* **LinkedIn :** Suivez les instructions de [configuration de votre application LinkedIn](/linkedin/talent/apply-with-linkedin)

* **Google :** Obtenir les informations d’identification du client OAuth 2.0 à partir de la [console d’API Google](https://console.developers.google.com/)
