---
title: Mettre à jour le manifeste pour activer l’authentification unique pour les onglets
description: Mettez à jour le manifeste Teams pour activer l’authentification unique (SSO) pour les onglets et chargez-le dans le client Teams pour tester l’authentification unique.
ms.topic: how-to
ms.localizationpriority: high
keywords: onglets d’authentification teams Microsoft Azure Active Directory (Azure AD)
ms.openlocfilehash: bd5b7257a131a11e861b94221c533d8364b6bb54
ms.sourcegitcommit: 176bbca74ba46b7ac298899d19a2d75087fb37c1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/04/2022
ms.locfileid: "68376584"
---
# <a name="update-manifest-for-sso-and-preview-app"></a>Mettre à jour le manifeste d’application pour l’authentification unique et l’application en préversion

Avant de mettre à jour le manifeste de l’application Teams, vérifiez que vous avez configuré le code pour activer l’authentification unique dans votre application onglet.

> [!div class="nextstepaction"]
> [Configurer le code](tab-sso-code.md)

Vous avez inscrit votre application onglet dans Azure AD et obtenu un ID d’application. Vous avez également configuré votre code pour appeler `getAuthToken()` et gérer le jeton d’accès. À présent, vous devez mettre à jour le manifeste de l’application Teams pour activer l’authentification unique pour votre application onglet. Le manifeste de l’application Teams décrit comment l’application s’intègre au produit Microsoft Teams.

## <a name="webapplicationinfo-property"></a>webApplicationInfo, propriété

Configurez la `webApplicationInfo` propriété dans le fichier manifeste de l’application Teams. Cette propriété permet à l’authentification unique pour votre application d’aider les utilisateurs de l’application à accéder à votre application onglet en toute transparence.

&nbsp;&nbsp;:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/sso-manifest.png" alt-text="Configuration du manifeste de l’application Teams":::

`webApplicationInfo` a deux éléments, `id` et `resource`.

| Élément | Description |
| --- | --- |
| id | Entrez l’ID d’application (GUID) que vous avez créé dans Azure AD. |
| ressource | Entrez l’URI de sous-domaine de votre application et l’URI d’ID d’application que vous avez créé dans Azure AD lors de la création de l’étendue. Vous pouvez le copier à partir de la section **Exposer une API** **Azure AD** > . |

> [!NOTE]
> Vous devez utiliser la version 1.5 ou supérieure du manifeste pour implémenter le `webApplicationInfo` champ.

L’URI d’ID d’application que vous avez inscrit dans Azure AD est configuré avec l’étendue de l’API que vous avez exposée. Configurez l’URI `resource` de sous-domaine de votre application pour vous assurer que la demande d’authentification utilisée `getAuthToken()` est du domaine fourni dans le manifeste de l’application Teams.

Pour plus d'informations, voir [webApplicationInfo .](../../../resources/schema/manifest-schema.md#webapplicationinfo).

## <a name="to-configure-teams-app-manifest"></a>Pour configurer le manifeste de l’application Teams

1. Ouvrez le projet d’application d’onglet.
2. Ouvrez le dossier :

  > [!NOTE]
  >
  > - Le dossier de manifeste doit se trouver à la racine de votre projet. Pour plus d’informations, consultez [Créer un robot pour Microsoft Teams](../../../concepts/build-and-test/apps-package.md).
  > - Pour plus d’informations sur la création d’un manifeste.json, consultez [Référence : Schéma de manifeste pour Microsoft Teams](../../../resources/schema/manifest-schema.md).

1. Ouvrir le fichier manifest.json
1. Ajoutez l’extrait de code suivant au fichier manifeste pour ajouter la nouvelle propriété :

    ```json
    "webApplicationInfo": {
    "id": "{Azure AD AppId}",
    "resource": "api://{Subdomain}.example.com/{Azure AD AppId}"
    }
    ```

    Où
    - {Azure AD AppId} est l’ID d’application que vous avez créé lorsque vous avez inscrit votre application dans Azure AD. C’est le GUID.
    - {{Subdomain}.app ID URI} est l’URI d’ID d’application que vous avez inscrit lors de la création de l’étendue dans Azure AD.

4. Mettez à jour l’ID d’application à partir d’Azure AD dans la propriété **id** .
5. Mettez à jour l’URL du sous-domaine dans les propriétés suivantes :
   1. `contentUrl`
   2. `configurationUrl`
   3. `validDomains`
6. Enregistrez le fichier manifeste de l’application Teams.

<br>
<details>
<summary>Voici un exemple de manifeste d’application après sa mise à jour</summary>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json",
  "manifestVersion": "1.11",
  "version": "1.0.0",
  "id": "bccfbe67-e08b-4ec1-a7fd-e0aaf41a097c",
  "developer": {
    "name": "Microsoft",
    "websiteUrl": "https://www.microsoft.com",
    "privacyUrl": "https://www.microsoft.com/privacy",
    "termsOfUseUrl": "https://www.microsoft.com/termsofuse"
  },
  "name": {
    "short": "Teams Auth SSO",
    "full": "Teams Auth SSO"
  },
  "description": {
    "short": "Teams Auth SSO app",
    "full": "The Teams Auth SSO app"
  },
  "icons": {
    "outline": "outline.png",
    "color": "color.png"
  },
  "accentColor": "#60A18E",
  "staticTabs": [
    {
      "entityId": "auth",
      "name": "Auth",
      "contentUrl": "https://contoso.com/Home/Index",
      "scopes": [ "personal" ]
    }
  ],
  "configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/Home/Configure",
      "canUpdateConfiguration": true,
      "scopes": [
        "team"
      ]
    }
  ],
  "permissions": [ "identity", "messageTeamMembers" ],
  "validDomains": [
    "contoso.com"
  ],
  "webApplicationInfo": {
    "id": "bccfbe67-e08b-4ec1-a7fd-e0aaf41a097c",
    "resource": "api://contoso.com/bccfbe67-e08b-4ec1-a7fd-e0aaf41a097c"
  }
}
```

</details>

> [!NOTE]
> Pendant le débogage, vous pouvez utiliser ngrok pour tester votre application dans Azure AD. Dans ce cas, vous devez remplacer le sous-domaine par `api://subdomain.example.com/00000000-0000-0000-0000-000000000000` l’URL ngrok. Vous devez mettre à jour l’URL chaque fois que votre sous-domaine ngrok change. Par exemple, api://23c3-103-50-148-128.ngrok.io/bccfbe67-e08b-4ec1-a7fd-e0aaf41a097c.

## <a name="sideload-and-preview-in-teams"></a>Chargement indépendant et préversion dans Teams

Vous avez configuré l’application onglet pour activer l’authentification unique dans Azure AD, dans le code de l’application et dans le fichier manifeste Teams. Vous pouvez maintenant charger une version test de votre application onglet dans Teams et la prévisualiser dans l’environnement Teams.

:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/sso-flow.png" alt-text="Application SSO":::

Pour afficher un aperçu de votre application onglet dans Teams :

1. Créer un package d’application Teams

   Un package d’application est un fichier zip qui contient un manifeste d’application et des icônes d’application.

1. Ouvrir Teams.

1. Sélectionnez **Applications** > **gérer vos applications** > **Charger une application**.

    Les options de chargement d’une application s’affichent.

1. Sélectionnez **Charger une application personnalisée** pour charger l’application onglet dans Teams.

1. Sélectionnez votre fichier zip de package d’application, puis sélectionnez **Ajouter**.

    L’application onglet est chargée de manière indépendante et la boîte de dialogue s’affiche pour vous informer des autorisations supplémentaires qui peuvent être requises.

1. Cliquez sur **Continuer**.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/teams-sso-consent.png" alt-text="Boîte de dialogue Teams indiquant les autorisations supplémentaires requises":::

    La boîte de dialogue de consentement Azure AD s’affiche.

1. Sélectionnez **Accepter** pour donner son consentement pour les étendues open-id.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/aad-sso-consent.png" alt-text="Capture d’écran de la boîte de dialogue de consentement Azure AD":::

    Teams ouvre l’application onglet et vous pouvez l’utiliser.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/teams-sso-app.png" alt-text="Exemple d’application onglet Teams avec l’authentification unique activée":::

    Félicitations ! Vous avez activé l’authentification unique pour votre application onglet.

## <a name="see-also"></a>Voir aussi

- [Référence : schéma de manifeste pour Microsoft Teams](../../../resources/schema/manifest-schema.md)
- [Format du schéma de manifeste](https://developer.microsoft.com/json-schemas/teams/v1.12/MicrosoftTeams.schema.json)
- [Créer un package de l’application Microsoft Teams](../../../concepts/build-and-test/apps-package.md)
