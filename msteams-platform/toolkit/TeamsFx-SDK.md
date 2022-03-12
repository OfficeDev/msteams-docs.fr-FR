---
title: Kit de développement logiciel (SDK) TeamsFx
author: MuyangAmigo
description: À propos du SDK TeamsFx
ms.author: nintan
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 1e78827d4105eefb112bef40d059804a94050f2d
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453620"
---
# <a name="teamsfx-sdk-for-typescript-or-javascript"></a>SDK TeamsFx pour TypeScript ou JavaScript

TeamsFx vise à réduire les tâches d’implémentation de l’identité et l’accès aux ressources cloud aux instructions à ligne unique avec une configuration nulle.

Utilisez la bibliothèque pour :

* Accédez aux fonctionnalités principales dans l’environnement client et serveur de la même manière.
* Écrivez du code d’authentification utilisateur de manière simplifiée.

## <a name="get-started"></a>Prise en main

Le Kit de développement logiciel (SDK) TeamsFx est préconfiguré dans un projet généré automatiquement à l’aide du Kit de ressources TeamsFx ou de l’interface CLI.
Pour plus d’informations, [voir Teams projet d’application](https://github.com/OfficeDev/TeamsFx/blob/main/packages/vscode-extension/README.md).

### <a name="prerequisites"></a>Configuration requise

* Node.js version ultérieure `10.x.x` .
* Si votre projet a installé des `botbuilder` [packages associés](https://github.com/Microsoft/botbuilder-js#packages) en tant que dépendances, assurez-vous qu’ils sont de la même version et que la version est .`>= 4.9.3` ([Problème : tous les packages BOTBUILDER doivent être de la même version](https://github.com/BotBuilderCommunity/botbuilder-community-js/issues/57#issuecomment-508538548))

Pour plus d’informations, reportez-vous aux rubriques suivantes :

* [Code source](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk)
* [Package (NPM)](https://www.npmjs.com/package/@microsoft/teamsfx)
* [Documentation de référence de l'API](https://aka.ms/teamsfx-sdk-help)
* [Échantillons](https://github.com/OfficeDev/TeamsFx-Samples)

### <a name="install-the-microsoftteamsfx-package"></a>Installer le `@microsoft/teamsfx` package

Installez le SDK TeamsFx pour TypeScript ou JavaScript avec `npm`:

```bash
npm install @microsoft/teamsfx
```

### <a name="create-and-authenticate-microsoftgraphclient"></a>Créer et s’authentifier `MicrosoftGraphClient`

Pour créer un objet client graph pour accéder à l’API microsoft Graph, vous aurez besoin des informations d’identification pour vous authentifier. Le SDK fournit plusieurs classes d’informations d’identification qui répondent à différentes exigences. Vous devez charger la configuration avant d’utiliser des informations d’identification.

* Dans l’environnement de navigateur, vous devez passer explicitement les paramètres de configuration. La React projet a fourni des variables d’environnement à utiliser.

```ts
loadConfiguration({
  authentication: {
    initiateLoginEndpoint: process.env.REACT_APP_START_LOGIN_PAGE_URL,
    clientId: process.env.REACT_APP_CLIENT_ID,
  },
});
```

* Dans un environnement NodeJS tel qu’Azure Function, vous pouvez simplement appeler `loadConfiguration`. Il se charge à partir des variables d’environnement par défaut.

```ts
loadConfiguration();
```

#### <a name="using-teams-app-user-credential"></a>Utilisation des informations Teams’utilisateur de l’application

Utilisez l’extrait de code suivant :

```ts
loadConfiguration({
  authentication: {
    initiateLoginEndpoint: process.env.REACT_APP_START_LOGIN_PAGE_URL,
    clientId: process.env.REACT_APP_CLIENT_ID,
  },
});
const credential = new TeamsUserCredential();
const graphClient = createMicrosoftGraphClient(credential, ["User.Read"]); // Initializes MS Graph SDK using our MsGraphAuthProvider
const profile = await graphClient.api("/me").get();
```

> [!NOTE]
> Vous pouvez utiliser cette classe d’informations d’identification dans l’application de navigateur, Teams Tab App.

#### <a name="using-microsoft-365-tenant-credential"></a>Utilisation des informations Microsoft 365 client

Microsoft 365 d’identification du client n’a pas besoin d’interagir Teams utilisateur de l’application. Vous pouvez appeler Microsoft Graph en tant qu’application.

Utilisez l’extrait de code suivant :

```ts
loadConfiguration();
const credential = new M365TenantCredential();
const graphClient = createMicrosoftGraphClient(credential);
const profile = await graphClient.api("/users/{object_id_of_another_people}").get();
```

## <a name="core-concepts-and-code-structure"></a>Concepts de base et structure du code

### <a name="credentials"></a>Identifiants

Il existe 3 classes d’informations d’identification situées sous le dossier [d’informations](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/credential) d’identification pour simplifier l’authentification.

Les classes d’informations `TokenCredential` d’identification implémentent une interface largement utilisée dans les API de bibliothèque Azure. Ils sont conçus pour fournir des jetons d’accès pour des étendues spécifiques. Les classes d’informations d’identification suivantes représentent différentes identités dans certains scénarios :

* `TeamsUserCredential`représente Teams’identité de l’utilisateur actuel. L’utilisation de ces informations d’identification demande le consentement de l’utilisateur pour la première fois.
* `M365TenantCredential`représente Microsoft 365 client. Elle est généralement utilisée lorsque l’utilisateur n’est pas impliqué comme un travail d’automatisation déclenché dans le temps.
* `OnBehalfOfUserCredential` utilise le flux « de la part de ». Il a besoin d’un jeton d’accès et vous pouvez obtenir un nouveau jeton pour une étendue différente. Il est conçu pour être utilisé dans les scénarios azure function ou bot.

### <a name="bots"></a>Bots

Les classes associées au bot sont stockées sous le [dossier bot](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/bot).

`TeamsBotSsoPrompt` peut s’intégrer à Bot Framework. Il simplifie le processus d’authentification pour le développement d’une application bot.

### <a name="helper-functions"></a>Fonctions d’aide

Le SDK TeamsFx fournit des fonctions d’aide pour faciliter la configuration des bibliothèques tierces. Ils se trouvent sous le [dossier principal](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/core).

### <a name="error-handling"></a>Gestion des erreurs

La réponse d’erreur de l’API `ErrorWithCode`est , qui contient le code d’erreur et le message d’erreur.

Par exemple, pour filtrer une erreur spécifique, vous pouvez utiliser l’extrait de code suivant :

```ts
try {
  const credential = new TeamsUserCredential();
  await credential.login("User.Read");
} catch (err: unknown) {
  if (err instanceof ErrorWithCode && err.code !== ErrorCode.ConsentFailed) {
    throw err;
  } else {
    // Silently fail because user cancels the consent dialog
    return;
  }
}
```

Et si l’instance d’informations d’identification est utilisée dans une autre bibliothèque telle que Microsoft Graph, il est possible que l’erreur soit capturée et transformée.

```ts
try {
  const credential = new TeamsUserCredential();
  const graphClient = createMicrosoftGraphClient(credential, ["User.Read"]); // Initializes MS Graph SDK using our MsGraphAuthProvider
  const profile = await graphClient.api("/me").get();
} catch (err: unknown) {
  // ErrorWithCode is handled by Graph client
  if (err instanceof GraphError && err.code?.includes(ErrorCode.UiRequiredError)) {
    this.setState({
      showLoginBtn: true,
    });
  }
}
```

## <a name="scenarios"></a>Scénarios

La section suivante fournit plusieurs extraits de code pour les scénarios courants :

### <a name="use-graph-api-in-tab-app"></a>Utiliser l’API Graph’onglet dans l’application Onglet

Utilisez `TeamsUserCredential` et `createMicrosoftGraphClient`.

```ts
loadConfiguration({
  authentication: {
    initiateLoginEndpoint: process.env.REACT_APP_START_LOGIN_PAGE_URL,
    clientId: process.env.REACT_APP_CLIENT_ID,
  },
});
const credential: any = new TeamsUserCredential();
const graphClient = createMicrosoftGraphClient(credential, ["User.Read"]);
const profile = await graphClient.api("/me").get();
```

### <a name="call-azure-function-in-tab-app"></a>Appeler la fonction Azure dans l’application Onglet

Utilisez la `axios` bibliothèque pour effectuer une requête HTTP à azure Function.

```ts
loadConfiguration({
  authentication: {
    initiateLoginEndpoint: process.env.REACT_APP_START_LOGIN_PAGE_URL,
    clientId: process.env.REACT_APP_CLIENT_ID,
  },
});
const credential: any = new TeamsUserCredential();
const token = credential.getToken(""); // Get SSO token for the user
// Call API hosted in Azure Functions on behalf of user
const apiConfig = getResourceConfiguration(ResourceType.API);
const response = await axios.default.get(apiConfig.endpoint + "api/httptrigger1", {
  headers: {
    authorization: "Bearer " + token,
  },
});
```

### <a name="access-sql-database-in-azure-function"></a>Accéder à SQL base de données dans Azure Function

Utilisez la `tedious` bibliothèque pour accéder à SQL qui `DefaultTediousConnectionConfiguration` gère l’authentification.
En dehors `tedious`de , vous pouvez également composer la config de connexion d’SQL bibliothèques basées sur le résultat de `sqlConnectionConfig.getConfig()`.

```ts
loadConfiguration();
const sqlConnectConfig = new DefaultTediousConnectionConfiguration();
// If there's only one SQL database
const config = await sqlConnectConfig.getConfig();
// If there are multiple SQL databases
const config2 = await sqlConnectConfig.getConfig("your database name");
const connection = new Connection(config);
connection.on("connect", (error) => {
  if (error) {
    console.log(error);
  }
});
```

### <a name="use-certificate-based-authentication-in-azure-function"></a>Utiliser l’authentification basée sur les certificats dans azure Function

```ts
loadConfiguration({
  authentication: {
    clientId: process.env.M365_CLIENT_ID,
    certificateContent: "The content of a PEM-encoded public/private key certificate",
    authorityHost: process.env.M365_AUTHORITY_HOST,
    tenantId: process.env.M365_TENANT_ID,
  },
});
```

### <a name="use-graph-api-in-bot-application"></a>Utiliser l’API Graph dans l’application Bot

Ajouter au `TeamsBotSsoPrompt` jeu de boîtes de dialogue.

```ts
const { ConversationState, MemoryStorage } = require("botbuilder");
const { DialogSet, WaterfallDialog } = require("botbuilder-dialogs");
const { TeamsBotSsoPrompt } = require("@microsoft/teamsfx");

const convoState = new ConversationState(new MemoryStorage());
const dialogState = convoState.createProperty("dialogState");
const dialogs = new DialogSet(dialogState);

loadConfiguration();
dialogs.add(
  new TeamsBotSsoPrompt("TeamsBotSsoPrompt", {
    scopes: ["User.Read"],
  })
);

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

## <a name="troubleshooting"></a>Résolution des problèmes

### <a name="configure-log"></a>Configurer le journal

Vous pouvez définir le niveau de journal client et rediriger les sorties lors de l’utilisation de cette bibliothèque. La journalisation est désactivée par défaut, vous pouvez l’activer en fixant le niveau du journal.

#### <a name="enable-log-by-setting-log-level"></a>Activer le journal en setting log level

La journalisation est activée uniquement lorsque vous définissez le niveau du journal. Par défaut, il imprime les informations du journal sur la console.

Définissez le niveau de journal à l’aide de l’extrait de code suivant :

```ts
// Only need the warning and error messages.
setLogLevel(LogLevel.Warn);
```

Vous pouvez rediriger la sortie du journal en setting custom logger or log function.

##### <a name="redirect-by-setting-custom-logger"></a>Rediriger en setting custom logger

```ts
setLogLevel(LogLevel.Info);
// Set another logger if you want to redirect to Application Insights in Azure Function
setLogger(context.log);
```

##### <a name="redirect-by-setting-custom-log-function"></a>Rediriger en setting custom log function

> [!NOTE]
> La fonction Log ne prend pas effet si vous définissez un enregistreur personnalisé.

```ts
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

## <a name="see-also"></a>Voir aussi

[Galerie d’exemples Microsoft TeamsFx](https://github.com/OfficeDev/TeamsFx-Samples)
