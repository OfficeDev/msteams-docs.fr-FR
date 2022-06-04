---
title: Authentification des utilisateurs de l’application
description: Décrit l’authentification dans Teams et comment l’utiliser dans les applications
ms.topic: conceptual
ms.localizationpriority: medium
keywords: Microsoft Azure Active Directory DSO OAuth d’authentification teams (Azure AD)
ms.openlocfilehash: db1a16959755668ec9aa298ed355ef657503ca03
ms.sourcegitcommit: e16b51a49756e0fe4eaf239898e28d3021f552da
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/04/2022
ms.locfileid: "65887733"
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
        :::image type="content" source="../../assets/images/authentication/tab-sso-icon.png" alt-text="Authentification unique pour l’application tabulation" link="../../tabs/how-to/authentication/tab-sso-overview.md" border="false":::
    :::column-end:::
    :::column span="1":::
        <br>

        &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; **Application Tab**  
        
    :::column-end:::
    :::column span="1":::
        :::image type="content" source="../../assets/images/authentication/tab-app-idp.png" alt-text="Authentification auprès du fournisseur OAuth tiers pour l’application tabulation." link="../../tabs/how-to/authentication/auth-tab-aad.md" border="false":::
    :::column-end:::
:::row-end:::
:::row:::
    :::column span="1":::
        :::image type="content" source="../../assets/images/authentication/bot-sso-icon.png" alt-text="Authentification unique pour l’application bot" link="../../bots/how-to/authentication/auth-aad-sso-bots.md" border="false":::
    :::column-end:::
    :::column span="1":::
        <br>

        &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; **Application bot**
        
    :::column-end:::
    :::column span="1":::
        :::image type="content" source="../../assets/images/authentication/bot-app-idp.png" alt-text="Authentification auprès du fournisseur OAuth tiers pour l’application bot." link="../../bots/how-to/authentication/add-authentication.md" border="false":::
    :::column-end:::
:::row-end:::
:::row:::
    :::column span="1":::
        :::image type="content" source="../../assets/images/authentication/mex-sso-icon.png" alt-text="Authentification unique pour l’application d’extension de messagerie" link="../../messaging-extensions/how-to/enable-SSO-auth-me.md" border="false":::
    :::column-end:::
    :::column span="1":::
        <br>

        &nbsp;&nbsp; &nbsp; **Application d’extension de message**
        
    :::column-end:::
    :::column span="1":::
        :::image type="content" source="../../assets/images/authentication/mex-app-idp.png" alt-text="Authentification avec des adresses IP oAuth tierces pour l’application d’extension de messagerie." link="../../messaging-extensions/how-to/add-authentication.md" border="false":::
    :::column-end:::
:::row-end:::

> [!NOTE]
> La page d’authentification silencieuse est déplacée vers le module Ressources. Pour plus d’informations, consultez [Authentification silencieuse](../../tabs/how-to/authentication/auth-silent-aad.md).

## <a name="see-also"></a>Voir aussi

- [Activer l’authentification unique dans une application onglet](../../tabs/how-to/authentication/tab-sso-overview.md)
- [Flux d’authentification Microsoft Teams pour les onglets](~/tabs/how-to/authentication/auth-flow-tab.md)
- [Support de l'identification unique pour les robots](~/bots/how-to/authentication/auth-aad-sso-bots.md)
- [Ajouter une authentification à votre extension de messagerie](~/messaging-extensions/how-to/add-authentication.md)
