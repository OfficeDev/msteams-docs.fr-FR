---
title: Configurer le consentement de l’administrateur
description: Décrit la configuration du consentement administrateur
ms.topic: how-to
ms.localizationpriority: medium
keywords: Onglets d’authentification Teams - API Graph Microsoft Azure Active Directory (Azure AD)
ms.openlocfilehash: dd954ef1ede05b6025b12512dfcee03044223642
ms.sourcegitcommit: e16b51a49756e0fe4eaf239898e28d3021f552da
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/04/2022
ms.locfileid: "65888116"
---
# <a name="configure-admin-consent"></a>Configurer le consentement de l’administrateur

Vous pouvez définir l’étendue de l’application pour une API exposée et déterminer si les utilisateurs peuvent donner leur consentement à cette étendue dans les répertoires où le consentement de l’utilisateur est activé. Vous pouvez autoriser uniquement les administrateurs à donner leur consentement pour des autorisations à privilèges plus élevés.

## <a name="to-expose-an-api"></a>Pour exposer une API

1. Sélectionnez **Gérer** > **exposer une API** dans le volet gauche.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/expose-api-menu.png" alt-text="Exposer une option de menu API." border="false":::

    La page **Exposer une API s’affiche** .

1. Sélectionnez **Définir** pour générer l’URI d’ID d’application.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/expose-an-api.png" alt-text="Définir l’URI d’ID d’application" border="false":::

    La section relative à la définition de l’URI d’ID d’application s’affiche.

1. Entrez l’URI d’ID d’application, puis **sélectionnez Enregistrer**.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/set-app-id-uri.png" alt-text="URI ID d'application" border="true":::

    Un message s’affiche sur le navigateur indiquant que l’URI de l’ID d’application a été mis à jour.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/app-id-uri-msg.png" alt-text="Message d’URI d’ID d’application" border="false":::

    L’URI d’ID d’application s’affiche sur la page.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/app-id-uri-added.png" alt-text="URI d’ID d’application mis à jour" border="false":::

## <a name="to-configure-api-scope"></a>Pour configurer l’étendue de l’API

1. Sélectionnez **+ Ajouter une étendue** dans les **étendues définies par cette section d’API** .

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/select-scope.png" alt-text="Sélectionner l’étendue" border="true":::

    La page **Ajouter une étendue** s’affiche.

1. Entrez les détails de l’application pour l’étendue de votre application.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/add-scope.png" alt-text="Ajouter des détails d’étendue" border="true":::

    1. Entrez le nom de l’étendue. Ce champ est obligatoire.
    1. Sélectionnez **Administrateurs et utilisateurs** pour configurer les utilisateurs qui peuvent donner leur consentement pour utiliser les informations d’identification de connexion de l’utilisateur. L’option par défaut est **Admins uniquement**.
    1. Entrez le **nom d’affichage du consentement administrateur**. Ce champ est obligatoire.
    1. Entrez la description du consentement de l’administrateur. Ce champ est obligatoire.
    1. Entrez le **nom d’affichage du consentement de l’utilisateur**.
    1. Entrez la description de la description du consentement de l’utilisateur.
    1. Sélectionnez l’option **Activé** pour l’état.
    1. Sélectionnez **Ajouter une étendue**.

    Un message s’affiche sur le navigateur indiquant que l’étendue a été ajoutée.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/scope-added-msg.png" alt-text="Message ajouté à l’étendue" border="false":::

    L’URI d’ID d’application s’affiche sur la page.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/scope-added.png" alt-text="Étendue ajoutée et affichée" border="false":::

## <a name="to-configure-authorized-client-application"></a>Pour configurer une application cliente autorisée

1. Parcourez la page **Exposer une API** dans la section **Application cliente autorisée** , puis sélectionnez **+ Ajouter une application cliente**.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/auth-client-apps.png" alt-text="Application cliente autorisée" border="true":::

    La page **Ajouter une application cliente** s’affiche.

1. Entrez les détails de l’ajout d’une application cliente. Pour cette section, vous allez ajouter deux applications clientes.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/add-client-app.png" alt-text="Ajouter une application cliente" border="true":::

    1. Entrez **1fec8e78-bce4-4aaf-ab1b-5451cc387264** comme ID client pour l’application mobile ou de bureau Teams.
    1. Sélectionnez l’ID d’application que vous avez créé pour votre application pour les **étendues autorisées**.
    1. Sélectionnez **Ajouter une application**.

    Un message s’affiche sur le navigateur indiquant que l’application cliente a été ajoutée.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/update-app-auth-msg.png" alt-text="Message ajouté à l’application cliente" border="false":::

    Les ID d’application cliente s’affichent sur la page.

1. Répétez l’étape précédente pour ajouter une application cliente pour l’application web Teams.

    1. Entrez **5e3ce6c0-2b1f-4285-8d4b-75ee78787346** comme ID client pour l’application web.
    1. Sélectionnez l’ID d’application que vous avez créé pour votre application pour les **étendues autorisées**.
    1. Sélectionnez **Ajouter une application**.

    Un message s’affiche sur le navigateur indiquant que l’application cliente a été ajoutée.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/update-app-auth-msg.png" alt-text="Message ajouté à l’application cliente pour l’application web" border="false":::

    Les ID d’application cliente s’affichent sur la page.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/client-app-added.png" alt-text="Application cliente ajoutée et affichée" border="true":::
