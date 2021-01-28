---
title: Configurer les fournisseurs d’identité OAuth 2.0
description: Décrit comment configurer des fournisseurs d’identité axés sur Azure AD
ms.topic: how-to
keywords: Fournisseur d’identité oauth AAD d’authentification teams
ms.openlocfilehash: b5ffd6c4c1edd2c4315ea1e31474a626de53aba1
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014466"
---
# <a name="configure-identity-providers"></a>Configurer les fournisseurs d’identité

## <a name="configuring-an-application-to-use-azure-active-directory-as-an-identity-provider"></a>Configuration d’une application pour utiliser Azure Active Directory comme fournisseur d’identité

Les fournisseurs d’identité qui la prise en charge d’OAuth 2.0 n’authentifiera pas les demandes provenant d’applications inconnues ; les applications doivent être inscrites à l’avance. Pour ce faire avec Azure AD, suivez les étapes suivantes :

1. Ouvrez le [portail d’inscription des applications.](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade)

2. Sélectionnez votre application pour afficher ses propriétés ou cliquez sur le bouton « Nouvelle inscription ». Recherchez la section **URI de** redirection pour l’application.

3. Dans le menu déroulant, assurez-vous **que le site Web** est sélectionné. Mettez à jour l’URL de votre point de terminaison d’authentification. Pour les exemples d’applications TypeScript/Node.js et C# sur GitHub, les URL de redirection seront similaires à ceci :

    Rediriger les URL : `https://<hostname>/bot-auth/simple-start`

Remplacez `<hostname>` par votre hôte réel. Il peut s’agit d’un site d’hébergement dédié tel qu’Azure, Glitch ou un tunnel ngrok vers localhost sur votre ordinateur de développement tel que `abcd1234.ngrok.io` . Vous n’avez peut-être pas encore ces informations si vous n’avez pas terminé ou hébergé votre application (ou l’exemple d’application mentionné ci-dessus), mais vous pouvez toujours revenir à cette page lorsque ces informations sont connues.

## <a name="other-authentication-providers"></a>Autres fournisseurs d’authentification

* **LinkedIn** Suivez les instructions de [configuration de votre application LinkedIn](https://developer.linkedin.com/docs/oauth2)

* **Google** Obtenir les informations d’identification du client OAuth 2.0 à partir de la [console d’API Google](https://console.developers.google.com/)
