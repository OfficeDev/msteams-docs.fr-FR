---
title: Ajouter l’authentification à votre extension de messagerie
author: clearab
description: Procédure d’ajout d’une authentification à une extension de messagerie
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: f7ebbcd99b1ec35900de7ec2f54f93263918e945
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673602"
---
# <a name="add-authentication-to-your-messaging-extension"></a>Ajouter l’authentification à votre extension de messagerie

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

## <a name="identify-the-user"></a>Identifier l’utilisateur

Chaque demande adressée à vos services comprend l’ID brouillé de l’utilisateur qui a exécuté la demande, ainsi que le nom d’affichage et l’ID d’objet Azure Active Directory de l’utilisateur.

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

Les `id` valeurs `aadObjectId` et sont garanties comme celles de l’utilisateur de teams authentifié. Elles peuvent être utilisées en tant que clés pour rechercher des informations d’identification ou un État mis en cache dans votre service. En outre, chaque requête contient l’ID de client Azure Active Directory de l’utilisateur, qui peut être utilisé pour identifier l’organisation de l’utilisateur. Le cas échéant, la demande contient également les ID d’équipe et de canal à l’origine de la demande.

## <a name="authentication"></a>Authentification

Si votre service requiert l’authentification de l’utilisateur, vous devez vous connecter à l’utilisateur avant de pouvoir utiliser l’extension de messagerie. Si vous avez écrit un bot ou un onglet qui se connecte à l’utilisateur, cette section doit être familière.

La séquence est la suivante :

1. Un utilisateur émet une requête ou la requête par défaut est automatiquement envoyée à votre service.
2. Votre service vérifie si l’utilisateur a d’abord été authentifié en inspectant l’ID utilisateur Teams.
3. Si l’utilisateur n’est pas authentifié, renvoyez une `auth` réponse avec une `openUrl` action suggérée, y compris l’URL d’authentification.
4. Le client Microsoft teams lance une fenêtre contextuelle hébergeant votre page Web à l’aide de l’URL d’authentification donnée.
5. Une fois que l’utilisateur se connecte, vous devez fermer votre fenêtre et envoyer un « code d’authentification » au client Teams.
6. Le client teams réémet ensuite la requête à votre service, ce qui inclut le code d’authentification passé à l’étape 5.

Votre service doit vérifier que le code d’authentification reçu à l’étape 6 correspond à celui de l’étape 5. Cela permet de s’assurer qu’un utilisateur malveillant n’essaie pas d’usurper ou de compromettre le flux de connexion. Cela « ferme la boucle » de manière efficace pour terminer la séquence d’authentification sécurisée.

### <a name="respond-with-a-sign-in-action"></a>Répondre à l’aide d’une action de connexion

Pour inviter un utilisateur non authentifié à se connecter, répondez avec une action suggérée de `openUrl` type qui inclut l’URL d’authentification.

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
> Pour que l’expérience de connexion soit hébergée dans une fenêtre contextuelle Teams, la partie domaine de l’URL doit figurer dans la liste des domaines valides de votre application. (Voir [validDomains](~/resources/schema/manifest-schema.md#validdomains) dans le schéma de manifeste.)

### <a name="start-the-sign-in-flow"></a>Démarrer le flux de connexion

Votre expérience de connexion doit être réactive et s’ajuster dans une fenêtre contextuelle. Il doit s’intégrer avec le [Kit de développement logiciel (SDK) JavaScript de Microsoft teams](/javascript/api/overview/msteams-client), qui utilise le passage des messages.

Comme pour les autres expériences incorporées s’exécutant dans Microsoft Teams, votre code à l’intérieur `microsoftTeams.initialize()`de la fenêtre doit commencer par appeler. Si votre code effectue un flux OAuth, vous pouvez transmettre l’ID d’utilisateur teams dans votre fenêtre, qui peut ensuite la transmettre à l’URL de connexion OAuth.

### <a name="complete-the-sign-in-flow"></a>Terminer le flux de connexion

Lorsque la demande de connexion se termine et redirige vers votre page, elle doit effectuer les étapes suivantes :

1. Générez un code de sécurité. (Il peut s’agir d’un nombre aléatoire.) Vous devez mettre en cache ce code sur votre service, ainsi que les informations d’identification obtenues via le flux de connexion (par exemple, les jetons OAuth 2,0).
2. Appelez `microsoftTeams.authentication.notifySuccess` et transférez le code de sécurité.

À ce stade, la fenêtre se ferme et le contrôle est transmis au client Teams. Le client peut désormais réexécuter la requête de l’utilisateur d’origine, ainsi que le code `state` de sécurité dans la propriété. Votre code peut utiliser le code de sécurité pour rechercher les informations d’identification stockées précédemment pour terminer la séquence d’authentification, puis terminer la demande de l’utilisateur.

#### <a name="reissued-request-example"></a>Exemple de requête reémise

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

