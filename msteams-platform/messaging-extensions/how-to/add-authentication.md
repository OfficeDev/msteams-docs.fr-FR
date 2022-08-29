---
title: Ajouter une authentification à votre extension de messagerie
author: surbhigupta
description: Dans cet article, vous allez apprendre à ajouter l’authentification à une extension de messagerie à l’aide d’exemples de code et d’exemples
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: c863a68f991dd62d51a534df04469eadfdb366e8
ms.sourcegitcommit: d5628e0d50c3f471abd91c3a3c2f99783b087502
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/25/2022
ms.locfileid: "67435047"
---
# <a name="add-authentication-to-your-message-extension"></a>Ajouter une authentification à votre extension de messagerie

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

> [!NOTE]
> Après avoir ajouté l’authentification à l’extension de message, l’utilisateur doit ajouter « **token.botframework.com** » à la section « **validDomains** » dans le manifeste.

## <a name="identify-the-user"></a>Identifier l’utilisateur

Chaque requête adressée à vos services inclut l’ID d’utilisateur, le nom complet de l’utilisateur et l’ID objet Azure Active Directory.

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

Les valeurs `id` et `aadObjectId` sont garanties pour l’utilisateur Teams authentifié. Elles sont utilisées comme clés pour rechercher les informations d’identification ou tout état mis en cache dans votre service. En outre, chaque requête contient l’ID de locataire Azure Active Directory, qui est utilisé pour identifier l’organisation des utilisateurs’. Le cas échéant, la requête contient également l’ID d’équipe et l’ID de canal d’où provient la demande.

## <a name="authentication"></a>Authentification

Si votre service requiert l’authentification de l’utilisateur, les utilisateurs doivent se connecter avant d’utiliser l’extension de message. Les étapes d’authentification sont similaires à celles d’un bot ou d’un onglet. La séquence est la suivante :

1. L’utilisateur émet une requête ou la requête par défaut est automatiquement envoyée à votre service.
1. Votre service vérifie si l’utilisateur est authentifié en inspectant l’ID d’utilisateur Teams.
1. Si l’utilisateur n’est pas authentifié, renvoyez une réponse `auth` avec une action suggérée `openUrl`, y compris l’URL d’authentification.
1. Le client Microsoft Teams lance une boîte de dialogue hébergeant votre page web à l’aide de l’URL d’authentification donnée.
1. Une fois que l’utilisateur s’est connecté, vous devez fermer votre fenêtre et envoyer un **code d’authentification** au client Teams.
1. Le client Teams publie ensuite la requête à sur votre service, qui inclut le code d’authentification passé à l’étape 5.

Votre service doit vérifier que le code d’authentification reçu à l’étape 6 correspond à l’étape 5. Les étapes garantissent qu’un utilisateur malveillant n’essaie pas d’usurper ou de compromettre le flux de connexion. Le flux « ferme la boucle » pour terminer la séquence d’authentification sécurisée.

### <a name="respond-with-a-sign-in-action"></a>Répondre avec une action de connexion

Pour demander à un utilisateur non authentifié de se connecter, répondez avec une action suggérée de type `openUrl` qui inclut l’URL d’authentification.

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
> * Pour que l’expérience de connexion soit hébergée dans une fenêtre contextuelle Teams, la partie domaine de l’URL doit figurer dans la liste des domaines valides de votre application. Pour plus d’informations, consultez [validDomains](~/resources/schema/manifest-schema.md#validdomains) dans le schéma du manifeste.
> * La taille de la fenêtre contextuelle d’authentification peut être définie en incluant des paramètres de chaîne de requête de largeur et de hauteur, `Value = $"{_siteUrl}/searchSettings.html?height=600&width=600"`.

### <a name="start-the-sign-in-flow"></a>Démarrer le flux de connexion

Votre expérience de connexion doit être réactive et tenir dans une fenêtre contextuelle. Il doit s’intégrer au [kit de développement logiciel (SDK) client JavaScript Microsoft Teams](/javascript/api/overview/msteams-client), qui utilise la transmission de messages.

Comme pour les autres expériences incorporées s’exécutant dans Microsoft Teams, votre code à l’intérieur de la fenêtre doit d’abord appeler `app.initialize()`. Si votre code exécute un flux OAuth, vous pouvez passer l’ID utilisateur Teams dans votre fenêtre, qui le transmet ensuite à l’URL de connexion OAuth.

### <a name="complete-the-sign-in-flow"></a>Terminer le flux de connexion

Une fois la requête de connexion terminée et redirigée vers votre page, elle doit effectuer les étapes suivantes :

1. Générez un code de sécurité, un nombre aléatoire. Vous devez mettre en cache ce code sur votre service, avec les informations d’identification obtenues via le flux de connexion, tels que les jetons OAuth 2.0.
1. Appelez `authentication.notifySuccess` et transmettez le code de sécurité.

À ce stade, la fenêtre se ferme et le contrôle est passé au client Teams. Le client publie à nouveau la requête utilisateur d’origine, ainsi que le code de sécurité dans la propriété `state` . Votre code peut utiliser le code de sécurité pour rechercher les informations d’identification stockées précédemment afin de terminer la séquence d’authentification, puis la requête de l’utilisateur.

#### <a name="reissued-request-example"></a>Exemple de nouvelle publication de requête

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

[Prise en charge de l’authentification unique pour les extensions de message](~/messaging-extensions/how-to/enable-sso-auth-me.md)
