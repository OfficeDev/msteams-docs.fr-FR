---
title: Ajouter l’authentification à votre extension de message
author: surbhigupta
description: Découvrez comment ajouter l’authentification à une extension de message à l’aide d’exemples de code et d’exemples
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: e3f799214a5007f90c03b2a7f9ac280c8e8760e1
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104412"
---
# <a name="add-authentication-to-your-message-extension"></a>Ajouter l’authentification à votre extension de message

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

## <a name="identify-the-user"></a>Identifier l’utilisateur

Chaque demande adressée à vos services inclut l’ID d’utilisateur, le nom complet de l’utilisateur et Azure Active Directory ID d’objet.

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

Les `id` valeurs et `aadObjectId` les valeurs sont garanties pour l’utilisateur Teams authentifié. Elles sont utilisées comme clés pour rechercher les informations d’identification ou tout état mis en cache dans votre service. En outre, chaque requête contient l’ID de locataire Azure Active Directory, qui est utilisé pour identifier l’organisation de l’utilisateur. Le cas échéant, la demande contient également l’ID d’équipe et l’ID de canal d’où provient la demande.

## <a name="authentication"></a>Authentification

Si votre service nécessite une authentification utilisateur, les utilisateurs doivent se connecter avant d’utiliser l’extension de message. Les étapes d’authentification sont similaires à celles d’un bot ou d’un onglet. La séquence est la suivante :

1. L’utilisateur émet une requête ou la requête par défaut est automatiquement envoyée à votre service.
1. Votre service vérifie si l’utilisateur est authentifié en inspectant l’ID d’utilisateur Teams.
1. Si l’utilisateur n’est pas authentifié, renvoyez une `auth` réponse avec une `openUrl` action suggérée, y compris l’URL d’authentification.
1. Le client Microsoft Teams lance une boîte de dialogue hébergeant votre page web à l’aide de l’URL d’authentification donnée.
1. Une fois que l’utilisateur s’est connecté, vous devez fermer votre fenêtre et envoyer un **code d’authentification** au client Teams.
1. Le client Teams réexécutera ensuite la requête à votre service, ce qui inclut le code d’authentification passé à l’étape 5.

Votre service doit vérifier que le code d’authentification reçu à l’étape 6 correspond à celui de l’étape 5. Cela garantit qu’un utilisateur malveillant n’essaie pas d’usurper ou de compromettre le flux de connexion. Cela « ferme la boucle » pour terminer la séquence d’authentification sécurisée.

### <a name="respond-with-a-sign-in-action"></a>Répondre avec une action de connexion

Pour inviter un utilisateur non authentifié à se connecter, répondez avec une action suggérée de type `openUrl` qui inclut l’URL d’authentification.

#### <a name="response-example-for-a-sign-in-action"></a>Exemple de réponse pour une action de connexion

```json
{
  "composeExtension":{
    "type":"auth",
    "suggestedActions":{
      "actions":[
        {
          "type": "openUrl",
          "value": "https://example.com/auth",
          "title": "Sign in to this app"
        }
      ]
    }
  }
}
```

> [!NOTE]
>
> * Pour que l’expérience de connexion soit hébergée dans une fenêtre contextuelle Teams, la partie domaine de l’URL doit figurer dans la liste des domaines valides de votre application. Pour plus d’informations, consultez [validDomains](~/resources/schema/manifest-schema.md#validdomains) dans le schéma de manifeste.
> * La taille de la fenêtre contextuelle d’authentification peut être définie en incluant les paramètres de chaîne de requête de largeur et de hauteur. `Value = $"{_siteUrl}/searchSettings.html?settings={escapedSettings}",`

### <a name="start-the-sign-in-flow"></a>Démarrer le flux de connexion

Votre expérience de connexion doit être réactive et tenir dans une fenêtre contextuelle. Il doit s’intégrer au [SDK client JavaScript Microsoft Teams](/javascript/api/overview/msteams-client), qui utilise la transmission de messages.

Comme avec d’autres expériences incorporées s’exécutant dans Microsoft Teams, votre code à l’intérieur de la fenêtre doit d’abord appeler `microsoftTeams.initialize()`. Si votre code exécute un flux OAuth, vous pouvez passer l’ID d’utilisateur Teams dans votre fenêtre, qui le transmet ensuite à l’URL de connexion OAuth.

### <a name="complete-the-sign-in-flow"></a>Terminer le flux de connexion

Une fois la demande de connexion terminée et redirigée vers votre page, elle doit effectuer les étapes suivantes :

1. Générez un code de sécurité, un nombre aléatoire. Vous devez mettre en cache ce code sur votre service, ainsi que les informations d’identification obtenues via le flux de connexion, comme les jetons OAuth 2.0.
1. Appelez `microsoftTeams.authentication.notifySuccess` et transmettez le code de sécurité.

À ce stade, la fenêtre se ferme et le contrôle est passé au client Teams. Le client réissue maintenant la requête utilisateur d’origine, ainsi que le code de sécurité dans la `state` propriété. Votre code peut utiliser le code de sécurité pour rechercher les informations d’identification stockées précédemment pour terminer la séquence d’authentification, puis terminer la demande de l’utilisateur.

#### <a name="reissued-request-example"></a>Exemple de demande rééditée

```json
{
    "name": "composeExtension/query",
    "value": {
        "commandId": "insertWiki",
        "parameters": [{
            "name": "searchKeyword",
            "value": "lakers"
        }],
        "state": "12345",
        "queryOptions": {
            "skip": 0,
            "count": 25
        }
    },
    "type": "invoke",
    "timestamp": "2017-04-26T05:18:25.629Z",
    "localTimestamp": "2017-04-25T22:18:25.629-07:00",
    "entities": [{
        "locale": "en-US",
        "country": "US",
        "platform": "Web",
        "type": "clientInfo"
    }],
    "text": "",
    "attachments": [],
    "address": {
        "id": "f:7638210432489287768",
        "channelId": "msteams",
        "user": {
            "id": "29:1A5TJWHkbOwSyu_L9Ktk9QFI1d_kBOEPeNEeO1INscpKHzHTvWfiau5AX_6y3SuiOby-r73dzHJ17HipUWqGPgw",
            "aadObjectId": "fc8ca1c0-d043-4af6-b09f-141536207403"
        },
        "conversation": {
            "id": "19:7705841b240044b297123ad7f9c99217@thread.skype"
        },
        "bot": {
            "id": "28:c073afa8-7e77-4f92-b3e7-aa589e952a3e",
            "name": "maotestbot2"
        },
        "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
        "useAuth": true
    },
    "source": "msteams"
}
```

## <a name="code-sample"></a>Exemple de code

|**Exemple de nom** | **Description** |**.NET** | **Node.js**|
|----------------|-----------------|--------------|----------------|
|Extensions de message - authentification et configuration | Extension de message qui a une page de configuration, accepte les demandes de recherche et retourne les résultats une fois que l’utilisateur s’est connecté. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config)|[View](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/javascript_nodejs/52.teams-messaging-extensions-search-auth-config)|

## <a name="see-also"></a>Voir aussi

[Prise en charge de l’authentification unique (SSO) pour les extensions de message](~/messaging-extensions/how-to/enable-sso-auth-me.md)
