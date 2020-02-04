---
title: Configuration des fournisseurs d’identité OAuth 2,0
description: Décrit comment configurer des fournisseurs d’identité avec un focus sur Azure AD
keywords: authentification par teams fournisseur d’identité OAuth AAD
ms.openlocfilehash: 799b0c20cda64456a4610acbdbedf758989bee55
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673920"
---
# <a name="configuring-identity-providers"></a>Configuration des fournisseurs d’identité

## <a name="configuring-an-application-to-use-azure-active-directory-as-an-identity-provider"></a>Configuration d’une application pour utiliser Azure Active Directory en tant que fournisseur d’identité

Les fournisseurs d’identité prenant en charge OAuth 2,0 n’authentifient pas les demandes provenant d’applications inconnues ; les applications doivent être enregistrées à l’avance. Pour effectuer cette opération avec Azure AD, procédez comme suit :

1. Ouvrez le [portail d’inscription des applications](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade).

2. Sélectionnez votre application pour afficher ses propriétés, ou cliquez sur le bouton « nouvelle inscription ». Recherchez la section **URI de redirection** pour l’application.

3. Dans le menu déroulant, vérifiez que l’option **Web** est sélectionnée. Mettez à jour l’URL vers votre point de terminaison d’authentification. Pour les exemples d’applications de type machine à écrire/node. js et C# sur GitHub, les URL de redirection ressemblent à ceci :

    URL de redirection :`https://<hostname>/bot-auth/simple-start`

Remplacez `<hostname>` par votre hôte réel. Il peut s’agir d’un site d’hébergement dédié, tel que Azure, un problème ou un tunnel ngrok vers localhost sur votre `abcd1234.ngrok.io`ordinateur de développement, comme. Vous ne disposez peut-être pas encore de ces informations si vous n’avez pas terminé ou hébergé votre application (ou l’exemple d’application mentionné ci-dessus), mais vous pouvez toujours revenir à cette page lorsque ces informations sont connues.

## <a name="other-authentication-providers"></a>Autres fournisseurs d’authentification

* **LinkedIn** Suivez les instructions de la procédure de [configuration de votre application LinkedIn](https://developer.linkedin.com/docs/oauth2)

* **Google** Obtenir des informations d’identification de client 2,0 OAuth à partir de la [console d’API Google](https://console.developers.google.com/)
