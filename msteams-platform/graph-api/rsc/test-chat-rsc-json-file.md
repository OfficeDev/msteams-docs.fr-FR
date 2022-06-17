---
title: Tester le consentement spécifique à une ressource pour une conversation dans Teams
description: Dans ce module, découvrez comment tester le consentement spécifique à une ressource pour une conversation dans Teams à l’aide de Postman avec un exemple de fichier JSON.
ms.localizationpriority: medium
author: jecha
ms.author: jecha
ms.topic: how-to
ms.openlocfilehash: 2155ab68bc95dd643c9796102e2c0ebf7088baa4
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142863"
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
