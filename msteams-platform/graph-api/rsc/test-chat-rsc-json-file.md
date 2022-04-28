---
title: Tester le consentement spécifique à une ressource pour une conversation dans Teams
description: Apprenez à tester le consentement spécifique aux ressources pour une conversation dans Teams en utilisant Postman avec un exemple de fichier JSON.
ms.localizationpriority: high
author: jecha
ms.author: jecha
ms.topic: how-to
keywords: équipes autorisation OAuth SSO Azure AD rsc graphique Postman
ms.openlocfilehash: 7419316efbebf4f59c81432f7cd37db7a4a29e4a
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111177"
---
# <a name="test-chat-rsc-postman-collection-for-json"></a>Test de discussion RSC Postman collection pour JSON

```json
{
 "info": {
  "_postman_id": "36d695ea-3ce2-4b2d-a1ac-b1721d2d46f1",
  "name": "Test-ChatRSC",
  "description": "Collection to test RSC.",
  "schema": "https://schema.getpostman.com/json/collection/v2.1.0/collection.json"
 },
 "item": [
  {
   "name": "Teams client app installation flow",
   "item": [
    {
     "name": "Chat - Create App Context Token",
     "event": [
      {
       "listen": "test",
       "script": {
        "exec": [
         "console.log(\"responseHeaders: \" + JSON.stringify(pm.response.headers));\r",
         "console.log(\"responseBody: \" + JSON.stringify(pm.response.text()));\r",
         "\r",
         "pm.test(\"Status Code 200\", () => {\r",
         "    // Need to validate the request succeeded. \r",
         "    pm.response.to.have.status(200);\r",
         "\r",
         "    // Set the app_context access token\r",
         "    const { access_token } = pm.response.json();\r",
         "    pm.environment.set(\"appContextToken\", access_token);\r",
         "});"
        ],
        "type": "text/javascript"
       }
      }
     ],
     "request": {
      "method": "POST",
      "header": [
       {
        "key": "Content-Type",
        "type": "text",
        "value": "application/x-www-form-urlencoded",
        "disabled": true
       }
      ],
      "body": {
       "mode": "urlencoded",
       "urlencoded": [
        {
         "key": "grant_type",
         "value": "client_credentials",
         "type": "text"
        },
        {
         "key": "client_id",
         "value": "{{azureADAppId}}",
         "type": "text"
        },
        {
         "key": "client_secret",
         "value": "{{azureADAppSecret}}",
         "type": "text"
        },
        {
         "key": "scope",
         "value": "{{token_scope}}",
         "type": "text"
        }
       ]
      },
      "url": {
       "raw": "https://login.microsoftonline.com/{{tenantId}}/oauth2/v2.0/token",
       "protocol": "https",
       "host": [
        "login",
        "microsoftonline",
        "com"
       ],
       "path": [
        "{{tenantId}}",
        "oauth2",
        "v2.0",
        "token"
       ]
      }
     },
     "response": []
    },
    {
     "name": "Get Chat",
     "event": [
      {
       "listen": "test",
       "script": {
        "exec": [
         "console.log(\"responseHeaders: \" + JSON.stringify(pm.response.headers));\r",
         "console.log(\"responseBody: \" + JSON.stringify(pm.response.text()));\r",
         "\r",
         "pm.test(\"Status Code 200\", () => {\r",
         "    // Need to validate the request succeeded. \r",
         "    pm.response.to.have.status(200)\r",
         "});"
        ],
        "type": "text/javascript"
       }
      }
     ],
     "request": {
      "method": "GET",
      "header": [
       {
        "key": "Authorization",
        "value": "Bearer {{appContextToken}}",
        "type": "text"
       }
      ],
      "url": {
       "raw": "https://graph.microsoft.com/beta/chats/{{chatId}}",
       "protocol": "https",
       "host": [
        "graph",
        "microsoft",
        "com"
       ],
       "path": [
        "beta",
        "chats",
        "{{chatId}}"
       ]
      }
     },
     "response": []
    },
    {
     "name": "Get Chat Members",
     "event": [
      {
       "listen": "test",
       "script": {
        "exec": [
         "console.log(\"responseHeaders: \" + JSON.stringify(pm.response.headers));\r",
         "console.log(\"responseBody: \" + JSON.stringify(pm.response.text()));\r",
         "\r",
         "pm.test(\"Status Code 200\", () => {\r",
         "    // Need to validate the request succeeded. \r",
         "    pm.response.to.have.status(200)\r",
         "});"
        ],
        "type": "text/javascript"
       }
      }
     ],
     "request": {
      "method": "GET",
      "header": [
       {
        "key": "Authorization",
        "value": "Bearer {{appContextToken}}",
        "type": "text"
       }
      ],
      "url": {
       "raw": "https://graph.microsoft.com/beta/chats/{{chatId}}/members",
       "protocol": "https",
       "host": [
        "graph",
        "microsoft",
        "com"
       ],
       "path": [
        "beta",
        "chats",
        "{{chatId}}",
        "members"
       ]
      }
     },
     "response": []
    },
    {
     "name": "Get Chat Messages",
     "event": [
      {
       "listen": "test",
       "script": {
        "exec": [
         "console.log(\"responseHeaders: \" + JSON.stringify(pm.response.headers));\r",
         "console.log(\"responseBody: \" + JSON.stringify(pm.response.text()));\r",
         "\r",
         "pm.test(\"Status Code 200\", () => {\r",
         "    // Need to validate the request succeeded. \r",
         "    pm.response.to.have.status(200)\r",
         "});"
        ],
        "type": "text/javascript"
       }
      }
     ],
     "request": {
      "method": "GET",
      "header": [
       {
        "key": "Authorization",
        "value": "Bearer {{appContextToken}}",
        "type": "text"
       }
      ],
      "url": {
       "raw": "https://graph.microsoft.com/beta/chats/{{chatId}}/messages",
       "protocol": "https",
       "host": [
        "graph",
        "microsoft",
        "com"
       ],
       "path": [
        "beta",
        "chats",
        "{{chatId}}",
        "messages"
       ]
      }
     },
     "response": []
    },
    {
     "name": "Get Tabs",
     "event": [
      {
       "listen": "test",
       "script": {
        "exec": [
         "console.log(\"responseHeaders: \" + JSON.stringify(pm.response.headers));\r",
         "console.log(\"responseBody: \" + JSON.stringify(pm.response.text()));\r",
         "\r",
         "pm.test(\"Status Code 200\", () => {\r",
         "    // Need to validate the request succeeded. \r",
         "    pm.response.to.have.status(200);\r",
         "\r",
         "    const { internalId } = pm.response.json();\r",
         "    pm.environment.set(\"generalChannelId\", internalId);\r",
         "});"
        ],
        "type": "text/javascript"
       }
      }
     ],
     "request": {
      "method": "GET",
      "header": [
       {
        "key": "Authorization",
        "value": "Bearer {{appContextToken}}",
        "type": "text"
       }
      ],
      "url": {
       "raw": "https://graph.microsoft.com/beta/chats/{{chatId}}/tabs",
       "protocol": "https",
       "host": [
        "graph",
        "microsoft",
        "com"
       ],
       "path": [
        "beta",
        "chats",
        "{{chatId}}",
        "tabs"
       ]
      }
     },
     "response": []
    },
    {
     "name": "Get PermissionGrants",
     "event": [
      {
       "listen": "test",
       "script": {
        "exec": [
         "console.log(\"responseHeaders: \" + JSON.stringify(pm.response.headers));\r",
         "console.log(\"responseBody: \" + JSON.stringify(pm.response.text()));\r",
         "\r",
         "pm.test(\"Status Code 200\", () => {\r",
         "    // Need to validate the request succeeded. \r",
         "    pm.response.to.have.status(200)\r",
         "});"
        ],
        "type": "text/javascript"
       }
      }
     ],
     "request": {
      "method": "GET",
      "header": [
       {
        "key": "Authorization",
        "value": "Bearer {{appContextToken}}",
        "type": "text"
       }
      ],
      "url": {
       "raw": "https://graph.microsoft.com/beta/chats/{{chatId}}/permissionGrants",
       "protocol": "https",
       "host": [
        "graph",
        "microsoft",
        "com"
       ],
       "path": [
        "beta",
        "chats",
        "{{chatId}}",
        "permissionGrants"
       ]
      }
     },
     "response": []
    },
    {
     "name": "Get InstalledApps",
     "event": [
      {
       "listen": "test",
       "script": {
        "exec": [
         "console.log(\"responseHeaders: \" + JSON.stringify(pm.response.headers));\r",
         "console.log(\"responseBody: \" + JSON.stringify(pm.response.text()));\r",
         "\r",
         "pm.test(\"Status Code 200\", () => {\r",
         "    // Need to validate the request succeeded. \r",
         "    pm.response.to.have.status(200);\r",
         "\r",
         "    const { internalId } = pm.response.json();\r",
         "});"
        ],
        "type": "text/javascript"
       }
      }
     ],
     "request": {
      "method": "GET",
      "header": [
       {
        "key": "Authorization",
        "value": "Bearer {{appContextToken}}",
        "type": "text"
       }
      ],
      "url": {
       "raw": "https://graph.microsoft.com/beta/chats/{{chatId}}/installedApps?$expand=teamsApp",
       "protocol": "https",
       "host": [
        "graph",
        "microsoft",
        "com"
       ],
       "path": [
        "beta",
        "chats",
        "{{chatId}}",
        "installedApps"
       ],
       "query": [
        {
         "key": "$expand",
         "value": "teamsApp"
        }
       ]
      }
     },
     "response": []
    }
   ]
  }
 ]
}
```
