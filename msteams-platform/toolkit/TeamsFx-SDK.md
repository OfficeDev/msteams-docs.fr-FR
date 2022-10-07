---
title: Kit de développement logiciel (SDK) TeamsFx
author: surbhigupta
description: Dans ce module, découvrez le Kit de développement logiciel (SDK) TeamsFx, les concepts de base et la structure de code, la personnalisation avancée et les scénarios
ms.author: v-amprasad
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: e28e726a1915cdbc8fddf501b0352d160673516c
ms.sourcegitcommit: 637b8f93b103297b1ff9f1af181680fca6f4499d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/07/2022
ms.locfileid: "68499166"
---
# <a name="teamsfx-sdk"></a>Kit de développement logiciel (SDK) TeamsFx

TeamsFx permet de réduire vos tâches en utilisant l’authentification unique Microsoft Teams (Teams SSO) et en accédant aux ressources cloud jusqu’à des instructions sur une seule ligne sans configuration. Vous pouvez utiliser le Kit de développement logiciel (SDK) TeamsFx dans le navigateur et l’environnement Node.js. Les fonctionnalités principales de TeamsFx sont accessibles dans l’environnement client et serveur. Vous pouvez écrire du code d’authentification utilisateur de manière simplifiée pour :

* Onglet Teams
* Bot Teams
* Fonction Azure

## <a name="prerequisites"></a>Configuration requise

Vous devez installer les outils suivants et configurer votre environnement de développement :

| &nbsp; | Installer | Pour l’utilisation... |
   | --- | --- | --- |
   | &nbsp; | [Visual Studio Code](https://code.visualstudio.com/download) | Environnements de build JavaScript, TypeScript ou SharePoint Framework (SPFx). Utilisez la version 1.55 ou ultérieure. |
   | &nbsp; | [Toolkit Teams](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)| Extension Microsoft Visual Studio Code qui crée une structure de projet pour votre application. Utilisez la version 4.0.0. |
   | &nbsp; | [Node.js](https://nodejs.org/en/download/) | Environnement runtime JavaScript principal. Utilisez la dernière version de LTS v16.|
   | &nbsp; | [Microsoft Teams](https://www.microsoft.com/microsoft-teams/download-app) | Microsoft Teams pour collaborer avec toutes les personnes avec lesquelles vous travaillez via les applications pour les conversations, les réunions, les appels, le tout au même endroit.|
   | &nbsp; | [Microsoft&nbsp; Edge](https://www.microsoft.com/edge) (recommandé) ou [Google Chrome](https://www.google.com/chrome/) | Un navigateur avec des outils de développement. |

> [!NOTE]
> Si votre projet a installé `botbuilder` packages [associés](https://github.com/Microsoft/botbuilder-js#packages) en tant que dépendances, vérifiez qu’ils sont de la même version.

Vous devez avoir une connaissance pratique des éléments :

* [Code source](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk)
* [Package (NPM)](https://www.npmjs.com/package/@microsoft/teamsfx)
* [Documentation de référence de l'API](https://aka.ms/teamsfx-sdk-help)
* [Exemples](https://github.com/OfficeDev/TeamsFx-Samples)

## <a name="get-started"></a>Prise en main

Le Kit de développement logiciel (SDK) TeamsFx est préconfiguré dans le projet généré automatiquement à l’aide du Kit de ressources TeamsFx ou de l’interface CLI.
Pour plus d’informations, consultez [projet d’application Teams](https://github.com/OfficeDev/TeamsFx/blob/main/packages/vscode-extension/README.md).

### <a name="install-the-microsoftteamsfx-package"></a>Installer le package `@microsoft/teamsfx`

Installez le Kit de développement logiciel (SDK) TeamsFx pour TypeScript ou JavaScript avec `npm` :

```bash
npm install @microsoft/teamsfx
```

## <a name="teamsfx-core-functionalities"></a>Fonctionnalités principales de TeamsFx

### <a name="teamsfx-class"></a>Classe TeamsFx

Par défaut, l’instance de classe TeamsFx accède à tous les paramètres TeamsFx à partir de variables d’environnement. Vous pouvez également définir des valeurs de configuration personnalisées pour remplacer les valeurs par défaut. Vérifiez la [configuration de remplacement](#override-configuration) pour plus de détails.
Lors de la création d’une instance TeamsFx, vous devez également spécifier le type d’identité.
Il existe deux types d’identité :

* **Identité de l’utilisateur** : représente l’utilisateur actuel de Teams.
* **Identité de** l’application : représente l’application elle-même.

    > [!NOTE]
    > Pour ces deux types d’identité, les constructeurs et méthodes TeamsFx ne sont pas les mêmes.

Vous pouvez en savoir plus sur l’identité de l’utilisateur et l’identité de l’application dans la section suivante :

<details>
<summary><b> Identité de l’utilisateur </b></summary>

| Command | Description |
|----------------|-------------|
| `new TeamsFx(IdentityType.User)`| L’application est authentifiée en tant qu’utilisateur Teams actuel. |
| `TeamsFx:setSsoToken()`| Identité de l’utilisateur dans l’environnement Node.js (sans navigateur). |
| `TeamsFx:getUserInfo()` | Pour obtenir les informations de base de l’utilisateur. |
| `TeamsFx:login()` | Il est utilisé pour permettre à l’utilisateur d’effectuer le processus de consentement, si vous souhaitez utiliser SSO pour obtenir un jeton d’accès pour certaines étendues OAuth. |

> [!NOTE]
> Vous pouvez accéder aux ressources pour le compte de l’utilisateur Teams actuel.
</details>

<details>
<summary><b> Identité de l’application </b></summary>

| Command | Description |
|----------------|-------------|
| `new TeamsFx(IdentityType.App)`| Application  is authenticated as an application. The permission usually needs administrator's approval.|
| `TeamsFx:getCredential()`| Il fournit des instances d’informations d’identification correspondant automatiquement au type d’identité. |

> [!NOTE]
> Vous avez besoin du consentement de l’administrateur pour les ressources.
</details>

### <a name="credential"></a>Credential

Pour initialiser TeamsFx, vous devez choisir le type d’identité requis. La publication spécifiant le SDK de type d’identité utilise un type différent de classe d’informations d’identification. Ceux-ci représentent l’identité et obtiennent le jeton d’accès par le flux d’authentification correspondant. Les classes d’informations d’identification implémentent `TokenCredential` une interface largement utilisée dans les API de bibliothèque Azure conçues pour fournir des jetons d’accès pour des étendues spécifiques. D’autres API s’appuient sur l’appel d’informations d’identification `TeamsFx:getCredential()` pour obtenir une instance de `TokenCredential`. Pour plus d’informations sur les classes liées aux informations d’identification et au flux d’authentification, consultez le [dossier d’informations d’identification](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/credential).

Il existe trois classes d’informations d’identification pour simplifier l’authentification. Voici les scénarios correspondants pour chaque cible de classe d’informations d’identification.

<details>
<summary><b> Identité de l’utilisateur dans l’environnement du navigateur </b></summary>

`TeamsUserCredential` représente l’identité de l’utilisateur actuel de Teams. Pour la première fois que les informations d’identification de l’utilisateur sont authentifiées, l’authentification unique Teams effectue le flux On-Behalf-Of pour l’échange de jetons. Le Kit de développement logiciel (SDK) utilise ces informations d’identification lorsque vous choisissez l’identité de l’utilisateur dans l’environnement du navigateur.

Les configurations requises sont : `initiateLoginEndpoint` et `clientId`.
</details>

<details>
<summary><b> Identité de l’utilisateur dans Node.js environnement </b></summary>

`OnBehalfOfUserCredential` utilise le flux On-Behalf-Of et nécessite un jeton d’authentification unique Teams, dans des scénarios de bot ou de fonction Azure. Le Kit de développement logiciel (SDK) TeamsFx utilise les informations d’identification suivantes lorsque vous choisissez l’identité de l’utilisateur dans Node.js environnement.

Configuration requise : `authorityHost` `tenantId`, `clientId`, `clientSecret` ou `certificateContent`.
</details>

<details>
<summary><b> Identité d’application dans Node.js environnement </b></summary>

`AppCredential` représente l’identité de l’application. Vous pouvez utiliser l’identité de l’application lorsque l’utilisateur n’est pas impliqué, par exemple dans un travail d’automatisation déclenché dans le temps. Le Kit de développement logiciel (SDK) TeamsFx utilise les informations d’identification suivantes lorsque vous choisissez l’identité de l’application dans Node.js environnement.

Configuration requise : `tenantId` `clientId`, `clientSecret` ou `certificateContent`.
</details>

### <a name="bot-sso"></a>Authentification unique du bot

Les classes associées au bot sont stockées sous [dossier de bot](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/bot).

`TeamsBotSsoPrompt` s’intègre à bot framework. Il simplifie le processus d’authentification lorsque vous développez une application de bot et que vous souhaitez utiliser l’authentification unique du bot.

Configuration requise : `initiateLoginEndpoint` `tenantId`, `clientId` et `applicationIdUri`.

### <a name="supported-functions"></a>Fonctions prises en charge

TeamsFx SDK provides several functions to ease the configuration for third-party libraries. They're located under [core folder](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/core).

* Microsoft Graph Service:`createMicrosoftGraphClient` et `MsGraphAuthProvider` aider à créer une instance Graph authentifiée.
* SQL:`getTediousConnectionConfig` retourne une configuration de connexion fastidieuse.

    Configuration requise :

  * Si vous souhaitez utiliser l’identité de l’utilisateur, puis `sqlServerEndpoint`, `sqlUsername` et `sqlPassword` sont nécessaires.
  * Si vous souhaitez utiliser l’identité MSI, vous devez les `sqlServerEndpoint`utiliser.`sqlIdentityId`

### <a name="override-configuration"></a>Remplacer la configuration

Vous pouvez passer une configuration personnalisée lors de la création d’une `TeamsFx` instance pour remplacer la configuration par défaut ou définir les champs requis lorsqu’il `environment variables` manque.

<details>
<summary><b> Pour le projet d’onglet </b> </summary>

Si vous avez créé un projet d’onglet à l’aide de Microsoft Visual Studio Code Toolkit, les valeurs de configuration suivantes seront utilisées à partir de variables d’environnement préconfigurées :

* authorityHost (REACT_APP_AUTHORITY_HOST)
* tenantId (REACT_APP_TENANT_ID)
* clientId (REACT_APP_CLIENT_ID)
* initiateLoginEndpoint (REACT_APP_START_LOGIN_PAGE_URL)
* applicationIdUri (REACT_APP_START_LOGIN_PAGE_URL)
* apiEndpoint (REACT_APP_FUNC_ENDPOINT) // utilisé uniquement lorsqu’il existe une fonction back-end
* apiName (REACT_APP_FUNC_NAME) // utilisé uniquement lorsqu’il existe une fonction back-end

</details>

<details>
<summary><b> Pour un projet de bot ou de fonction Azure </b></summary>

Si vous avez créé une fonction Azure ou un projet de bot à l’aide de Visual Studio Code Toolkit, les valeurs de configuration suivantes seront utilisées à partir de variables d’environnement préconfigurées :

* initiateLoginEndpoint (INITIATE_LOGIN_ENDPOINT)
* authorityHost (M365_AUTHORITY_HOST)
* tenantId (M365_TENANT_ID)
* clientId (M365_CLIENT_ID)
* clientSecret (M365_CLIENT_SECRET)
* applicationIdUri (M365_APPLICATION_ID_URI)
* apiEndpoint (API_ENDPOINT)

* sqlServerEndpoint (SQL_ENDPOINT) // utilisé uniquement lorsqu’il existe une instance sql
* sqlUsername (SQL_USER_NAME) // utilisé uniquement en cas d’instance sql
* sqlPassword (SQL_PASSWORD) // utilisé uniquement lorsqu’il existe une instance sql
* sqlDatabaseName (SQL_DATABASE_NAME) // utilisé uniquement en cas d’instance sql
* sqlIdentityId (IDENTITY_ID) // utilisé uniquement en cas d’instance sql

</details>

### <a name="error-handling"></a>Gestion des erreurs

Le type de base de la réponse d’erreur d’API est `ErrorWithCode`, qui contient le code d’erreur et le message d’erreur. Par exemple, pour filtrer une erreur spécifique, vous pouvez utiliser l’extrait de code suivant :

```typescript
try {
  const teamsfx = new TeamsFx();
  await teamsfx.login("User.Read");
} catch (err: unknown) {
  if (err instanceof ErrorWithCode && err.code !== ErrorCode.ConsentFailed) {
    throw err;
  } else {
    // Silently fail because user cancels the consent dialog
    return;
  }
}
```

Si l’instance d’informations d’identification est utilisée dans d’autres bibliothèques telles que Microsoft Graph, il est possible que l’erreur soit interceptée et transformée.

## <a name="microsoft-graph-scenarios"></a>Scénarios Microsoft Graph

Cette section fournit plusieurs extraits de code pour les scénarios courants liés à Microsoft Graph. Dans de tels scénarios, l’utilisateur peut appeler des API à l’aide d’autorisations différentes à des extrémités différentes (frontend/backend).

* Autorisation de délégué utilisateur dans le serveur frontal (Utiliser TeamsUserCredential) <details>
    <summary><b>Utiliser l’API graphe dans l’application onglet</b></summary>

    Cet extrait de code vous montre comment utiliser `TeamsFx` et `createMicrosoftGraphClient` obtenir des profils utilisateur à partir de Microsoft Graph. Il vous montre également comment intercepter et résoudre un `GraphError`.

    1. Importez les classes nécessaires.

    ```typescript
    import {
      createMicrosoftGraphClient,
      TeamsFx,
    } from "@microsoft/teamsfx";
    ```

    2. Permet `TeamsFx.login()` d’obtenir le consentement de l’utilisateur.

    ```typescript
    // Put these code in a call-to-action callback function to avoid browser blocking automatically showing up pop-ups.
    await teamsfx.login(["User.Read"]); // Login with scope
    ```

    3. Vous pouvez initialiser une instance TeamsFx et un client de graphe et obtenir des informations à partir de MS Graph par ce client.

    ```typescript
    try {
      const teamsfx = new TeamsFx();
      const graphClient = createMicrosoftGraphClient(teamsfx, ["User.Read"]); // Initializes MS Graph SDK using our MsGraphAuthProvider
      const profile = await graphClient.api("/me").get();
    } catch (err: unknown) {
      // ErrorWithCode is handled by Graph client
      if (err instanceof GraphError && err.code?.includes(ErrorCode.UiRequiredError)) {
        // Need to show login button to ask for user consent.
      }
    }
    ```

    Pour plus d’informations sur l’exemple d’utilisation de API Graph dans l’application onglet, consultez [l’exemple d’onglet Hello World](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/hello-world-tab).

    </details>

    <details>
    <summary><b>Intégration à Microsoft Graph Toolkit</b></summary>

    La bibliothèque [Microsoft Graph Toolkit](https://aka.ms/mgt) est une collection de différents fournisseurs d’authentification et composants d’interface utilisateur optimisés par Microsoft Graph.

    Le `@microsoft/mgt-teamsfx-provider` package expose la classe qui utilise la `TeamsFxProvider` classe pour connecter des utilisateurs `TeamsFx` et acquérir des jetons à utiliser avec Microsoft Graph.

    1. Vous pouvez installer les packages requis suivants :

    ```bash
    npm install @microsoft/mgt-element @microsoft/mgt-teamsfx-provider @microsoft/teamsfx
    ```

    2. Initialisez le fournisseur à l’intérieur de votre composant.

    ```typescript
     // Import the providers and credential at the top of the page
    import {Providers} from '@microsoft/mgt-element';
    import {TeamsFxProvider} from '@microsoft/mgt-teamsfx-provider';
    import {TeamsUserCredential} from "@microsoft/teamsfx";

    const scope = ["User.Read"];
    const teamsfx = new TeamsFx();
    const provider = new TeamsFxProvider(teamsfx, scope);
    Providers.globalProvider = provider;   
    ```

    3. Vous pouvez utiliser la méthode pour obtenir le `teamsfx.login(scopes)` jeton d’accès requis.

    ```typescript
    // Put these code in a call-to-action callback function to avoid browser blocking automatically showing up pop-ups. 
    await teamsfx.login(this.scope);
    Providers.globalProvider.setState(ProviderState.SignedIn);
    ```

    4. Vous pouvez maintenant ajouter n’importe quel composant dans votre page HTML ou dans votre `render()` méthode avec React pour utiliser le `TeamsFx` contexte pour accéder à Microsoft Graph.

    ```html
    <mgt-person query="me" view="threeLines"></mgt-person>
    ```

    ```typescript
    public render(): void {
    return (
        <div>
            <Person personQuery="me" view={PersonViewType.threelines}></Person>
        </div>
    );
    }    
    ```

    Pour plus d’informations sur l’exemple d’initialisation du fournisseur TeamsFx, consultez [l’exemple d’exportateur de contacts](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/graph-toolkit-contact-exporter).

    </details>

* Autorisation de délégué utilisateur dans le back-end (Utiliser OnBehalfOfUserCredential) <details>
    <summary><b>Utiliser API Graph dans l’application bot</b></summary>

    Cet extrait de code vous montre comment définir `TeamsBotSsoPrompt` une boîte de dialogue, puis se connecter pour obtenir un jeton d’accès.

    1. Initialiser et ajouter `TeamsBotSsoPrompt` au jeu de dialogues.

    ```typescript
    const { ConversationState, MemoryStorage } = require("botbuilder");
    const { DialogSet, WaterfallDialog } = require("botbuilder-dialogs");
    const { TeamsBotSsoPrompt } = require("@microsoft/teamsfx");

    const convoState = new ConversationState(new MemoryStorage());
    const dialogState = convoState.createProperty("dialogState");
    const dialogs = new DialogSet(dialogState);

    const teamsfx = new TeamsFx();
    dialogs.add(
      new TeamsBotSsoPrompt(teamsfx, "TeamsBotSsoPrompt", {
        scopes: ["User.Read"],
      })
    );    
    ```

    2. Commencez la boîte de dialogue et connectez-vous.

    ```typescript
    dialogs.add(
      new WaterfallDialog("taskNeedingLogin", [
        async (step) => {
          return await step.beginDialog("TeamsBotSsoPrompt");
        },
        async (step) => {
          const token = step.result;
          if (token) {
            // ... continue with task needing access token ...
          } else {
            await step.context.sendActivity(`Sorry... We couldn't log you in. Try again later.`);
            return await step.endDialog();
          }
        },
      ])
    );    
    ```

    Pour plus d’informations sur l’exemple d’utilisation de l’API graphe dans l’application bot, consultez [l’exemple bot-sso](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/bot-sso).

    </details>

    <details>
    <summary><b>Utiliser API Graph dans l’extension de message</b></summary>

    Cet extrait de code vous montre comment remplacer `handleTeamsMessagingExtensionQuery` les extensions à partir du `TeamsActivityHandler`SDK TeamsFx et comment les utiliser `handleMessageExtensionQueryWithToken` pour vous connecter afin d’obtenir un jeton d’accès :

    ```typescript
    public async handleTeamsMessagingExtensionQuery(context: TurnContext, query: any): Promise<any> {
      return await handleMessageExtensionQueryWithToken(context, null, 'User.Read', 
        async (token: MessageExtensionTokenResponse) => {
          // ... continue to query with access token ...
        });
    }    
    ```

    Pour plus d’informations sur l’exemple d’utilisation de l’API graphe dans l’extension de message, consultez [message-extension-sso-sample](https://aka.ms/teamsfx-me-sso-sample).
    </details>

    <details>
    <summary><b>Utiliser API Graph dans le bot de commandes</b></summary>

    Cet extrait de code vous montre comment implémenter `TeamsFxBotSsoCommandHandler` le bot de commandes pour appeler l’API Microsoft.

    ```typescript
    import { Activity, TurnContext } from "botbuilder";
    import {
      CommandMessage,
      TriggerPatterns,
      TeamsFx,
      createMicrosoftGraphClient,
      TeamsFxBotSsoCommandHandler,
      TeamsBotSsoPromptTokenResponse,
    } from "@microsoft/teamsfx";

    export class ProfileSsoCommandHandler implements TeamsFxBotSsoCommandHandler {
      triggerPatterns: TriggerPatterns = "profile";

      async handleCommandReceived(
        context: TurnContext,
        message: CommandMessage,
        tokenResponse: TeamsBotSsoPromptTokenResponse,
      ): Promise<string | Partial<Activity> | void> {
        // Init TeamsFx instance with SSO token
        const teamsfx = new TeamsFx().setSsoToken(tokenResponse.ssoToken);

        // Add scope for your Azure AD app. For example: Mail.Read, etc.
        const graphClient = createMicrosoftGraphClient(teamsfx, ["User.Read"]);
      
        // Call graph api use `graph` instance to get user profile information
        const me = await graphClient.api("/me").get();

        if (me) {
          // Bot will send the user profile info to user
          return `Your command is '${message.text}' and you're logged in as ${me.displayName}`;
        } else {
          return "Could not retrieve profile information from Microsoft Graph.";
        }
      }
    }    
    ```

    Pour plus d’informations sur l’utilisation de cette classe dans le bot de commandes, consultez [Ajouter l’authentification unique à l’application Teams](add-single-sign-on.md). Il existe également un exemple de projet [command-bot-with-sso](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/command-bot-with-sso) , que vous pouvez essayer.

    </details>

    <details>
    <summary><b>Appeler la fonction Azure dans l’application onglet : flux On-Behalf-Of</b></summary>

    Cet extrait de code vous montre comment utiliser `CreateApiClient` ou `axios` bibliothèquer pour appeler Azure Function, et comment appeler API Graph dans la fonction Azure pour obtenir des profils utilisateur.

    1. Vous pouvez utiliser `CreateApiClient` le kit de développement logiciel (SDK) TeamsFx pour appeler la fonction Azure :

    ```typescript
    async function callFunction(teamsfx?: TeamsFx) {
      const teamsfx = new TeamsFx();

      // Get the credential.
      const credential = teamsfx.getCredential(); 
      // Create an API client by providing the token and endpoint.
      const apiClient = CreateApiClient(
        teamsfx.getConfig("YOUR_API_ENDPOINT"), // Create an API Client that uses SSO token to authenticate requests
        new BearerTokenAuthProvider(async () =>  (await credential.getToken(""))!.token) // Call API hosted in Azure Functions on behalf of user to inject token to request header
      );

      // Send a GET request to "RELATIVE_API_PATH", "/api/functionName" for example.
      const response = await apiClient.get("RELATIVE_API_PATH");
      return response.data;
    }    
    ```

    Vous pouvez également utiliser `axios` la bibliothèque pour appeler Azure Function.

    ```typescript
    async function callFunction(teamsfx?: TeamsFx) {
      const accessToken = await teamsfx.getCredential().getToken(""); // Get SSO token 
      // teamsfx.getConfig("apiEndpoint") will read REACT_APP_FUNC_ENDPOINT environment variable 
      const endpoint = teamsfx.getConfig("apiEndpoint");
      const response = await axios.default.get(endpoint + "/api/" + functionName, {
        headers: {
          authorization: "Bearer " + accessToken.token,
        },
      });
      return response.data;
    }    
    ```

    2. Appelez API Graph dans la fonction Azure pour le compte de l’utilisateur en réponse.

    ```typescript
    export default async function run(
      context: Context,
      req: HttpRequest,
      teamsfxContext: TeamsfxContext
    ): Promise<Response> {
      const res: Response = { status: 200, body: {},};
      // ...
      teamsfx = new TeamsFx().setSsoToken(accessToken);
      // Query user's information from the access token.
      try {
        const currentUser: UserInfo = await teamsfx.getUserInfo();
        if (currentUser && currentUser.displayName) {
          res.body.userInfoMessage = `User display name is ${currentUser.displayName}.`;
        } else {
          res.body.userInfoMessage = "No user information was found in access token.";
        }
      } catch (e) {
      }
      // Create a graph client to access user's Microsoft 365 data after user has consented.
      try {
        const graphClient: Client = createMicrosoftGraphClient(teamsfx, [".default"]);
        const profile: any = await graphClient.api("/me").get();
        res.body.graphClientMessage = profile;
      } catch (e) {
      }
      return res;
    }    
    ```

    Pour plus d’informations sur l’exemple d’utilisation de l’API graphe dans l’application bot, consultez  [l’exemple hello-world-tab-with-backend](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/hello-world-tab-with-backend).

    </details>

* Autorisation d’application dans le back-end <details>
    <summary><b>utiliser l’authentification par certificat dans Azure Function</b></summary>

    Cet extrait de code vous montre comment utiliser l’autorisation d’application basée sur un certificat pour obtenir le jeton qui peut être utilisé pour appeler API Graph.

    1. Vous pouvez initialiser le `authConfig` .`PEM-encoded key certificate`

    ```typescript
    const authConfig = {
      clientId: process.env.M365_CLIENT_ID,
      certificateContent: "The content of a PEM-encoded public/private key certificate",
      authorityHost: process.env.M365_AUTHORITY_HOST,
      tenantId: process.env.M365_TENANT_ID,
    };    
    ```

    2. Vous pouvez l’utiliser `authConfig` pour obtenir le jeton.

    ```typescript
    const teamsfx = new TeamsFx(IdentityType.App);
    teamsfx.setCustomeConfig(authConfig);
    const token = teamsfx.getCredential().getToken();    
    ```

    </details>

    <details>
    <summary><b>Utiliser l’authentification par clé secrète client dans Azure Function</b></summary>

    Cet extrait de code vous montre comment utiliser l’autorisation d’application secrète client pour obtenir le jeton qui peut être utilisé pour appeler API Graph.

    1. Vous pouvez initialiser le `authConfig` .`client secret`

    ```typescript
    const authConfig = {
      clientId: process.env.M365_CLIENT_ID,
      clientSecret: process.env.M365_CLIENT_SECRET,
      authorityHost: process.env.M365_AUTHORITY_HOST,
      tenantId: process.env.M365_TENANT_ID,
    };    
    ```

    2. Vous pouvez l’utiliser `authConfig` pour obtenir le jeton.

    ```typescript
    const teamsfx = new TeamsFx(IdentityType.App);
    teamsfx.setCustomeConfig(authConfig);
    const token = teamsfx.getCredential().getToken();    
    ```

    Pour plus d’informations sur l’exemple d’utilisation de l’API graphe dans l’application bot, consultez [l’exemple hello-world-tab-with-backend](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/hello-world-tab-with-backend).

    </details>

## <a name="other-scenarios"></a>Autres scénarios

Cette section fournit plusieurs extraits de code pour d’autres scénarios liés à Microsoft Graph. Vous pouvez créer un client d’API dans Bot ou Azure Function et accéder à la base de données SQL dans Azure Function.

  <details>
  <summary><b>Créer un client d’API pour appeler l’API existante dans Bot ou Azure Function</b></summary>

  Cet extrait de code vous montre comment appeler une API existante dans Bot par `ApiKeyProvider`.

  ```typescript
  const teamsfx = new TeamsFx();

  // Create an API Key auth provider. In addition to APiKeyProvider, following auth providers are also available:
  // BearerTokenAuthProvider, BasicAuthProvider, CertificateAuthProvider.
  const authProvider = new ApiKeyProvider("YOUR_API_KEY_NAME",
    teamsfx.getConfig("YOUR_API_KEY_VALUE"), // This reads the value of YOUR_API_KEY_VALUE environment variable.
    ApiKeyLocation.Header
  );

  // Create an API client using above auth provider.
  // You can also implement AuthProvider interface and use it here.
  const apiClient = createApiClient(
    teamsfx.getConfig("YOUR_API_ENDPOINT"), // This reads YOUR_API_ENDPOINT environment variable.
    authProvider
  );

  // Send a GET request to "RELATIVE_API_PATH", "/api/apiname" for example.
  const response = await apiClient.get("RELATIVE_API_PATH");  
  ```

  </details>

  <details>
  <summary><b>accéder à la base de données SQL dans Azure Function</b></summary>

  Utilisez `tedious` la bibliothèque pour accéder à SQL et l’utiliser `DefaultTediousConnectionConfiguration` pour gérer l’authentification. Vous pouvez également composer la configuration de connexion d’autres bibliothèques SQL en fonction du résultat de `sqlConnectionConfig.getConfig()`.

  1. Définissez la configuration de la connexion.

  ```typescript
  // Equivalent to:
  // const sqlConnectConfig = new DefaultTediousConnectionConfiguration({
  //    sqlServerEndpoint: process.env.SQL_ENDPOINT,
  //    sqlUsername: process.env.SQL_USER_NAME,
  //    sqlPassword: process.env.SQL_PASSWORD,
  // });
  const teamsfx = new TeamsFx();
  // If there's only one SQL database
  const config = await getTediousConnectionConfig(teamsfx);
  // If there are multiple SQL databases
  const config2 = await getTediousConnectionConfig(teamsfx, "your database name");  
  ```

  2. Connectez-vous à votre base de données.

  ```typescript
  const connection = new Connection(config);
  connection.on("connect", (error) => {
    if (error) {
      console.log(error);
    }
  });  
  ```

  > [!NOTE]
  > Pour plus d’informations sur l’exemple d’accès à la base de données SQL dans la fonction Azure, consultez [l’exemple share-now](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/share-now).

</details>

## <a name="advanced-customization"></a>Personnalisation avancée

### <a name="configure-log"></a>Configurer le journal

Vous pouvez définir le niveau du journal client et rediriger les sorties lors de l’utilisation de cette bibliothèque.

> [!NOTE]
> La journalisation est désactivée par défaut. Vous pouvez l’activer en définissant le niveau du journal.

#### <a name="enable-log-by-setting-log-level"></a>Activer le journal en définissant le niveau du journal

Lorsque vous définissez le niveau du journal, la journalisation est activée. Il imprime les informations du journal dans la console par défaut.

Définissez le niveau du journal à l’aide de l’extrait de code suivant :

```typescript
// Only need the warning and error messages.
setLogLevel(LogLevel.Warn);
```

> [!NOTE]
> Vous pouvez rediriger la sortie du journal en définissant une fonction d’enregistreur d’événements ou de journal personnalisée.

#### <a name="redirect-by-setting-custom-logger"></a>Rediriger en définissant un enregistreur d’événements personnalisé

```typescript
setLogLevel(LogLevel.Info);
// Set another logger if you want to redirect to Application Insights in Azure Function
setLogger(context.log);
```

#### <a name="redirect-by-setting-custom-log-function"></a>Rediriger en définissant une fonction de journal personnalisée

```typescript
setLogLevel(LogLevel.Info);
// Only log error message to Application Insights in bot application.
setLogFunction((level: LogLevel, message: string) => {
  if (level === LogLevel.Error) {
    this.telemetryClient.trackTrace({
      message: message,
      severityLevel: Severity.Error,
    });
  }
});
```

> [!NOTE]
> Les fonctions de journal ne prennent pas effet si vous définissez un enregistreur d’événements personnalisé.

## <a name="upgrade-latest-sdk-version"></a>Mettre à niveau la dernière version du Kit de développement logiciel (SDK)

Si vous utilisez la version du Kit de développement logiciel ( `loadConfiguration()`SDK), vous pouvez suivre les étapes ci-dessous pour effectuer la mise à niveau vers la dernière version du SDK :

1. Supprimez `loadConfiguration()` et transmettez les paramètres personnalisés à l’aide de `new TeamsFx(IdentityType.User, { ...customConfig })`
2. Remplacez `new TeamsUserCredential()` par `new TeamsFx()`.
3. Remplacez `new M365TenantCredential()` par `new TeamsFx(IdentityType.App)`.
4. Remplacez `new OnBehalfOfUserCredential(ssoToken)` par `new TeamsFx().setSsoToken(ssoToken)`.
5. Transmettez l’instance des fonctions d’assistance `TeamsFx` pour remplacer l’instance d’informations d’identification.

## <a name="next-step"></a>Étape suivante

Pour obtenir des exemples détaillés sur l’utilisation du projet [d’exemples](https://github.com/OfficeDev/TeamsFx-Samples) du Kit de développement logiciel (SDK) TeamsFx.

## <a name="see-also"></a>Voir aussi

[galerie d’exemples Microsoft TeamsFx](https://github.com/OfficeDev/TeamsFx-Samples).
