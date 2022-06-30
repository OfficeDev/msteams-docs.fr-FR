---
title: Authentification des utilisateurs de l’application
description: Dans ce module, découvrez l’authentification dans Teams et comment l’utiliser dans les applications, le flux d’authentification web et le flux OAuthPrompt pour les bots conversationnels.
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: 5b5a083d0bd52a2c9233adaf6164821042236f85
ms.sourcegitcommit: c398dfdae9ed96f12e1401ac7c8d0228ff9c0a2b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/30/2022
ms.locfileid: "66557868"
---
# <a name="authenticate-users-in-microsoft-teams"></a>Authentifier les utilisateurs dans Microsoft Teams

L’authentification consiste à valider les utilisateurs d’applications et à sécuriser les utilisateurs de l’application et de l’application contre un accès injustifié. Vous pouvez utiliser une méthode d’authentification adaptée à votre application pour valider les utilisateurs de l’application qui souhaitent utiliser l’application Teams.

Choisissez d’ajouter l’authentification pour votre application de l’une des deux manières suivantes :

- Activer l’authentification **unique (SSO) dans une application Teams** : l’authentification unique dans Teams est une méthode d’authentification qui utilise l’identité Teams d’un utilisateur d’application pour lui fournir l’accès à votre application. Un utilisateur qui s’est connecté à Teams n’a pas besoin de se reconnecter à votre application dans l’environnement Teams. Avec seulement un consentement requis de l’utilisateur de l’application, l’application Teams récupère les détails d’accès pour eux à partir d’Azure Active Directory (AD). Une fois que l’utilisateur de l’application a donné son consentement, il peut accéder à l’application même à partir d’autres appareils sans avoir à être à nouveau validé.

- **Activer l’authentification à l’aide d’un fournisseur OAuth tiers** : vous pouvez utiliser un fournisseur d’identité OAuth tiers pour authentifier les utilisateurs de votre application. L’utilisateur de l’application est inscrit auprès du fournisseur d’identité, qui a une relation d’approbation avec votre application. Lorsque l’utilisateur tente de se connecter, le fournisseur d’identité valide l’utilisateur de l’application et lui donne accès à votre application. Azure AD est l’un de ces fournisseurs OAuth tiers. Vous pouvez utiliser d’autres fournisseurs, tels que Google, Facebook, GitHub ou tout autre fournisseur.

## <a name="select-authentication-method"></a>Sélectionner la méthode d’authentification

Activez l’authentification avec l’authentification unique ou des adresses IP OAuth tierces dans votre application onglet, application bot et application d’extension de messagerie. Sélectionnez l’une des deux méthodes permettant d’ajouter l’authentification dans votre application :

:::row:::
    :::column span="1":::
        Authentification unique
    :::column-end:::
    :::column span="1":::
        &nbsp;
    :::column-end:::
    :::column span="1":::
        OAuth
    :::column-end:::
:::row-end:::
:::row:::
    :::column span="1":::
        :::image type="content" source="../../assets/images/authentication/tab-sso-icon.png" alt-text="Authentification unique pour l’application tabulation" link="../../tabs/how-to/authentication/tab-sso-overview.md":::
    :::column-end:::
    :::column span="1":::
        <br>

        &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; **Application Tab**  
        
    :::column-end:::
    :::column span="1":::
        :::image type="content" source="../../assets/images/authentication/tab-app-idp.png" alt-text="Authentification auprès du fournisseur OAuth tiers pour l’application tabulation." link="../../tabs/how-to/authentication/auth-tab-aad.md":::
    :::column-end:::
:::row-end:::
:::row:::
    :::column span="1":::
        :::image type="content" source="../../assets/images/authentication/bot-sso-icon.png" alt-text="Authentification unique pour l’application bot" link="../../bots/how-to/authentication/auth-aad-sso-bots.md":::
    :::column-end:::
    :::column span="1":::
        <br>

        &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; **Application bot**
        
    :::column-end:::
    :::column span="1":::
        :::image type="content" source="../../assets/images/authentication/bot-app-idp.png" alt-text="Authentification auprès du fournisseur OAuth tiers pour l’application bot." link="../../bots/how-to/authentication/add-authentication.md":::
    :::column-end:::
:::row-end:::
:::row:::
    :::column span="1":::
        :::image type="content" source="../../assets/images/authentication/mex-sso-icon.png" alt-text="Authentification unique pour l’application d’extension de messagerie" link="../../messaging-extensions/how-to/enable-SSO-auth-me.md":::
    :::column-end:::
    :::column span="1":::
        <br>

        &nbsp;&nbsp; &nbsp; **Application d’extension de message**
        
    :::column-end:::
    :::column span="1":::
        :::image type="content" source="../../assets/images/authentication/mex-app-idp.png" alt-text="Authentification avec des adresses IP oAuth tierces pour l’application d’extension de messagerie." link="../../messaging-extensions/how-to/add-authentication.md":::
    :::column-end:::
:::row-end:::

> [!NOTE]
> La page d’authentification silencieuse est déplacée vers le module Ressources. Pour plus d’informations, consultez [Authentification silencieuse](../../tabs/how-to/authentication/auth-silent-aad.md).

## <a name="see-also"></a>Voir aussi

- [Activer l’authentification unique dans une application onglet](../../tabs/how-to/authentication/tab-sso-overview.md)
- [Flux d’authentification Microsoft Teams pour les onglets](~/tabs/how-to/authentication/auth-flow-tab.md)
- [Support de l'identification unique pour les robots](~/bots/how-to/authentication/auth-aad-sso-bots.md)
- [Ajouter une authentification à votre extension de messagerie](~/messaging-extensions/how-to/add-authentication.md)
