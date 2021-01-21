---
title: Ajouter l’authentification à votre extension de messagerie
author: clearab
description: Comment ajouter l’authentification à une extension de messagerie
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 4ebe65af06240d13ceb99fe3b7640ab402d716c5
ms.sourcegitcommit: 00c657e3bf57d3b92aca7da941cde47a2eeff4d0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/20/2021
ms.locfileid: "49911869"
---
# <a name="add-authentication-to-your-messaging-extension"></a>Ajouter l’authentification à votre extension de messagerie

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

## <a name="identify-the-user"></a>Identifier l’utilisateur

Chaque demande à vos services inclut l’ID obscurci de l’utilisateur qui a effectué la demande, ainsi que le nom d’affichage de l’utilisateur et l’ID d’objet Azure Active Directory.

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

Les `id` `aadObjectId` valeurs et les valeurs sont garanties pour être celle de l’utilisateur Teams authentifié. Elles peuvent être utilisées comme clés pour rechercher des informations d’identification ou tout état mis en cache dans votre service. En outre, chaque demande contient l’ID de client Azure Active Directory de l’utilisateur, qui peut être utilisé pour identifier l’organisation de l’utilisateur. Le cas échéant, la demande contient également les ID d’équipe et de canal d’où provient la demande.

## <a name="authentication"></a>Authentification

Si votre service requiert l’authentification de l’utilisateur, vous devez le signer avant de pouvoir utiliser l’extension de messagerie. Si vous avez écrit un bot ou un onglet qui se signe dans l’utilisateur, cette section doit être familière.

La séquence est la suivante :

1. Un utilisateur envoie une requête ou la requête par défaut est automatiquement envoyée à votre service.
2. Votre service vérifie si l’utilisateur s’est d’abord authentifié en inspectant l’ID d’utilisateur Teams.
3. Si l’utilisateur ne s’est pas authentifié, renvoyez une réponse avec une action suggérée, y compris `auth` `openUrl` l’URL d’authentification.
4. Le client Microsoft Teams lance une fenêtre pop-up hébergeant votre page web à l’aide de l’URL d’authentification donnée.
5. Une fois que l’utilisateur s’est signé, vous devez fermer votre fenêtre et envoyer un « code d’authentification » au client Teams.
6. Le client Teams ressue ensuite la requête à votre service, qui inclut le code d’authentification passé à l’étape 5.

Votre service doit vérifier que le code d’authentification reçu à l’étape 6 correspond à celui de l’étape 5. Cela garantit qu’un utilisateur malveillant ne tente pas d’usurper ou de compromettre le flux de la signature. Cela permet effectivement de « fermer la boucle » pour terminer la séquence d’authentification sécurisée.

### <a name="respond-with-a-sign-in-action"></a>Répondre avec une action de se connectez

Pour inviter un utilisateur non authentifié à se connecter, répondez avec une action suggérée de type qui inclut `openUrl` l’URL d’authentification.

#### <a name="response-example-for-a-sign-in-action"></a>Exemple de réponse pour une action de sign-in

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
> Pour que l’expérience de se connecte soit hébergée dans une fenêtre pop-up Teams, la partie domaine de l’URL doit se trouver dans la liste des domaines valides de votre application. (Voir [validDomains](~/resources/schema/manifest-schema.md#validdomains) dans le schéma de manifeste.)

### <a name="start-the-sign-in-flow"></a>Démarrer le flux de la signature

Votre expérience de sign-in doit être réactive et tenir dans une fenêtre popup. Il doit s’intégrer au [SDK client JavaScript Microsoft Teams,](/javascript/api/overview/msteams-client)qui utilise la transmission de message.

Comme avec d’autres expériences incorporées en cours d’exécution dans Microsoft Teams, votre code à l’intérieur de la fenêtre doit d’abord `microsoftTeams.initialize()` appeler. Si votre code effectue un flux OAuth, vous pouvez passer l’ID utilisateur Teams dans votre fenêtre, qui peut ensuite le transmettre à l’URL de la signature OAuth.

### <a name="complete-the-sign-in-flow"></a>Terminer le flux de la signature

Lorsque la demande de se connecte est terminée et redirige vers votre page, elle doit effectuer les étapes suivantes :

1. Générer un code de sécurité. (Il peut s’agit d’un nombre aléatoire.) Vous devez mettre en cache ce code sur votre service, ainsi que les informations d’identification obtenues via le flux de connexion (tels que les jetons OAuth 2.0).
2. Appelez `microsoftTeams.authentication.notifySuccess` et passez le code de sécurité.

À ce stade, la fenêtre se ferme et le contrôle est transmis au client Teams. Le client peut maintenant rééditer la requête utilisateur d’origine, ainsi que le code de sécurité dans la `state` propriété. Votre code peut utiliser le code de sécurité pour rechercher les informations d’identification stockées précédemment pour terminer la séquence d’authentification, puis effectuer la demande de l’utilisateur.

#### <a name="reissued-request-example"></a>Exemple de requête rééditée

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

## <a name="samples"></a>Exemples
Pour obtenir un exemple de code montrant le processus d’authentification des extensions de messagerie, voir :

[Exemple d’authentification des extensions de messagerie Microsoft Teams](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config)

 
