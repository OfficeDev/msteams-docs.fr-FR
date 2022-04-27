---
title: Kit de développement logiciel (SDK) TeamsFx
author: MuyangAmigo
description: À propos du Kit de développement logiciel (SDK) TeamsFx
ms.author: nintan
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: ade31e39d48b92cca4309b16762dc95afccf1925
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073096"
---
# <a name="teamsfx-sdk"></a>Kit de développement logiciel (SDK) TeamsFx

TeamsFx permet de réduire les tâches des développeurs en tirant parti de Teams’authentification unique et en accédant aux ressources cloud jusqu’à des instructions sur une seule ligne sans aucune configuration. Le Kit de développement logiciel (SDK) TeamsFx est conçu pour être utilisé dans le navigateur et l’environnement Node.js. Les scénarios courants sont les suivants :

* application d’onglet Teams
* Fonction Azure
* bot Teams

Vous pouvez utiliser le Kit de développement logiciel (SDK) TeamsFx pour :

* Accéder aux fonctionnalités principales dans l’environnement client et serveur 
* Écrire le code d’authentification utilisateur de manière simplifiée

## <a name="prerequisites"></a>Configuration requise

Installez les outils suivants et configurez votre environnement de développement :

* Dernière version de Node.js
* Si votre projet a installé `botbuilder` [des packages](https://github.com/Microsoft/botbuilder-js#packages) associés en tant que dépendances, vérifiez qu’ils sont de la même version. Actuellement, la version requise est 4.15.0 ou ultérieure. Pour plus d’informations, consultez [les packages du générateur de bots qui doivent être de la même version](https://github.com/BotBuilderCommunity/botbuilder-community-js/issues/57#issuecomment-508538548).

Vous devez avoir une connaissance pratique des éléments suivants :

* [Code source](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk)
* [Package (NPM)](https://www.npmjs.com/package/@microsoft/teamsfx)
* [Documentation de référence de l'API](https://aka.ms/teamsfx-sdk-help)
* [Échantillons](https://github.com/OfficeDev/TeamsFx-Samples)

## <a name="get-started"></a>Prise en main

Le Kit de développement logiciel (SDK) TeamsFx est préconfiguré dans le projet généré automatiquement à l’aide de TeamsFx Shared Computer Toolkit ou CLI.
Pour plus d’informations, consultez [Teams projet d’application](https://github.com/OfficeDev/TeamsFx/blob/main/packages/vscode-extension/README.md).

### <a name="install-the-microsoftteamsfx-package"></a>Installer le `@microsoft/teamsfx` package

Installez le Kit de développement logiciel (SDK) TeamsFx pour TypeScript ou JavaScript avec `npm`:

```bash
npm install @microsoft/teamsfx
```

### <a name="create-microsoftgraphclient-service"></a>Créer un `MicrosoftGraphClient` service

Pour créer un objet client graphe et accéder à Microsoft API Graph, vous avez besoin des informations d’identification pour vous authentifier. Le Kit de développement logiciel (SDK) fournit des API à configurer pour les développeurs.

<br>

<details>
<summary><b>Appeler API Graph au nom de Teams User (User Identity)</b></summary>

Utilisez l’extrait de code suivant :

```ts
// Equivalent to:
// const teamsfx = new TeamsFx(IdentityType.User, {
//   initiateLoginEndpoint: process.env.REACT_APP_START_LOGIN_PAGE_URL,
//   clientId: process.env.REACT_APP_CLIENT_ID,
// }
const teamsfx = new TeamsFx();
const graphClient = createMicrosoftGraphClient(teamsfx, ["User.Read"]); // Initializes MS Graph SDK using our MsGraphAuthProvider
const profile = await graphClient.api("/me").get(); // Get the profile of current user
```

</details>

<br>

<details>
<summary><b>Appeler API Graph sans utilisateur (identité de l’application)</b></summary>

Il ne nécessite pas l’interaction avec Teams utilisateur. Vous pouvez appeler Microsoft Graph en tant qu’identité d’application.

Utilisez l’extrait de code suivant :

```ts
// Equivalent to:
// const teamsfx = new TeamsFx(IdentityType.App, {
//   initiateLoginEndpoint: process.env.REACT_APP_START_LOGIN_PAGE_URL,
//   clientId: process.env.REACT_APP_CLIENT_ID,
// });
const teamsfx = new TeamsFx(IdentityType.App);
const graphClient = createMicrosoftGraphClient(teamsfx);
const profile = await graphClient.api("/users/{object_id_of_another_people}").get(); // Get the profile of certain user
```

</details>

<br>

## <a name="core-concepts-and-code-structure"></a>Concepts de base et structure de code

### <a name="teamsfx-class"></a>Classe TeamsFx

L’instance de classe TeamsFx accède par défaut à tous les paramètres TeamsFx à partir de variables d’environnement. Vous pouvez également définir des valeurs de configuration personnalisées pour remplacer les valeurs par défaut. Pour plus d’informations, consultez [la configuration de remplacement](#override-configuration) . Lors de la création d’une instance TeamsFx, vous devez également spécifier le type d’identité. Il existe deux types d’identité :

* Identité de l’utilisateur
* Identité de l’application

#### <a name="user-identity"></a>Identité de l’utilisateur

| Command | Description |
|----------------|-------------|
| `new TeamsFx(IdentityType.User)`| L’application est authentifiée en tant qu’utilisateur Teams actuel. |
| `TeamsFx:setSsoToken()`| Identité de l’utilisateur dans Node.js environnement (sans navigateur). |
| `TeamsFx:getUserInfo()` | Pour obtenir les informations de base de l’utilisateur. |
| `TeamsFx:login()` | Il est utilisé pour permettre à l’utilisateur d’effectuer un processus de consentement, si vous souhaitez utiliser l’authentification unique pour obtenir un jeton d’accès pour certaines étendues OAuth. |

> [!NOTE]
> Vous pouvez accéder aux ressources pour le compte de l’utilisateur Teams actuel.

#### <a name="application-identity"></a>Identité de l’application

| Command | Description |
|----------------|-------------|
| `new TeamsFx(IdentityType.App)`| L’application est authentifiée en tant qu’application. L’autorisation nécessite généralement l’approbation de l’administrateur.|
| `TeamsFx:getCredential()`| Il fournit des instances d’informations d’identification correspondant automatiquement au type d’identité. |

> [!NOTE]
> Vous avez besoin du consentement de l’administrateur pour les ressources.

### <a name="credential"></a>Credential

Vous devez choisir le type d’identité lors de l’initialisation de TeamsFx. Une fois que vous avez spécifié le type d’identité lors de l’initialisation de TeamsFx, le Kit de développement logiciel (SDK) utilise différents types de classe d’informations d’identification pour représenter l’identité et obtenir le jeton d’accès par le flux d’authentification correspondant.

Il existe trois classes d’informations d’identification pour simplifier l’authentification. [dossier d’informations d’identification](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/credential). Les classes d’informations d’identification implémentent `TokenCredential` l’interface, qui est largement utilisée dans les API de bibliothèque Azure, conçue pour fournir des jetons d’accès pour des étendues spécifiques. D’autres API s’appuient sur un appel d’informations d’identification `TeamsFx:getCredential()` pour obtenir une instance de `TokenCredential`.

Voici les scénarios correspondants pour chaque cible de classe d’informations d’identification.

#### <a name="user-identity-in-browser-environment"></a>Identité de l’utilisateur dans l’environnement du navigateur
`TeamsUserCredential`représente Teams l’identité de l’utilisateur actuel. L’utilisation de ces informations d’identification demande le consentement de l’utilisateur à la première fois. Il tire parti du flux Teams SSO et On-Behalf-Of pour effectuer l’échange de jetons. Le Kit de développement logiciel (SDK) utilise ces informations d’identification lorsque le développeur choisit l’identité de l’utilisateur dans l’environnement du navigateur.

Configuration requise : `initiateLoginEndpoint`, `clientId`.

#### <a name="user-identity-in-nodejs-environment"></a>Identité de l’utilisateur dans Node.js environnement
`OnBehalfOfUserCredential`utilise le flux On-Behalf-Of et nécessite Teams jeton d’authentification unique. Il est conçu pour être utilisé dans les scénarios de fonction ou de bot Azure. Le Kit de développement logiciel (SDK) utilise ces informations d’identification lorsque le développeur choisit l’identité de l’utilisateur dans Node.js environnement.

Configuration requise : `authorityHost`, `tenantId`, `clientId``clientSecret` ou `certificateContent`.

#### <a name="application-identity-in-nodejs-environment"></a>Identité d’application dans Node.js environnement
`AppCredential` représente l’identité de l’application. Il est généralement utilisé lorsque l’utilisateur n’est pas impliqué, comme le travail d’automatisation déclenché par le temps. Le Kit de développement logiciel (SDK) utilise ces informations d’identification lorsque le développeur choisit l’identité de l’application dans Node.js environnement.

Configuration requise : `tenantId`, `clientId``clientSecret` ou `certificateContent`.

### <a name="bot-sso"></a>Bot SSO

Les classes associées au bot sont stockées sous le [dossier du bot](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/bot).

`TeamsBotSsoPrompt` a une bonne intégration avec bot framework. Il simplifie le processus d’authentification lorsque vous développez une application de bot et que vous souhaitez tirer parti de l’authentification unique du bot.

Configuration requise : `initiateLoginEndpoint`, `tenantId`, `clientId`et `applicationIdUri`.

### <a name="supported-functions"></a>Fonctions prises en charge

Le Kit de développement logiciel (SDK) TeamsFx fournit plusieurs fonctions pour faciliter la configuration des bibliothèques tierces. Ils se trouvent sous le [dossier principal](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/core).

*  Service Microsoft Graph :`createMicrosoftGraphClient` et `MsGraphAuthProvider` aide à créer une instance de Graph authentifiée.
*  SQL :`getTediousConnectionConfig` retourne une configuration de connexion fastidieuse.

Configuration requise :
* `sqlServerEndpoint`, `sqlUsername``sqlPassword` si vous souhaitez utiliser l’identité de l’utilisateur
* `sqlServerEndpoint`, `sqlIdentityId` si vous souhaitez utiliser l’identité MSI

### <a name="error-handling"></a>Gestion des erreurs

La réponse d’erreur de l’API est `ErrorWithCode`, qui contient le code d’erreur et le message d’erreur. Par exemple, pour filtrer une erreur spécifique, vous pouvez utiliser l’extrait de code suivant :

```ts
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

```ts
try {
  const teamsfx = new TeamsFx();
  const graphClient = createMicrosoftGraphClient(teamsfx, ["User.Read"]); // Initializes MS Graph SDK using our MsGraphAuthProvider
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

<br>

<details>
<summary><b>Utiliser API Graph dans l’application onglet</b></summary>
 
Utiliser `TeamsFx` et `createMicrosoftGraphClient`.

```ts
const teamsfx = new TeamsFx();
const graphClient = createMicrosoftGraphClient(teamsfx, ["User.Read"]);
const profile = await graphClient.api("/me").get();
```

</details>

<br>

<details>
<summary><b>Appeler la fonction Azure dans l’application onglet</b></summary>

Utilisez `axios` la bibliothèque pour effectuer une requête HTTP à Azure Function.

```ts
const teamsfx = new TeamsFx();
const token = teamsfx.getCredential().getToken(""); // Get SSO token for the use
// Call API hosted in Azure Functions on behalf of user
const apiEndpoint = teamsfx.getConfig("apiEndpoint");
const response = await axios.default.get(apiEndpoint + "api/httptrigger1", {
  headers: {
    authorization: "Bearer " + token,
  },
});
```

</details>

<br>

<details>
<summary><b>Accéder à SQL base de données dans Azure Function</b></summary>


Utilisez `tedious` la bibliothèque pour accéder à SQL et tirer parti `DefaultTediousConnectionConfiguration` de l’authentification.
En dehors de `tedious`, vous pouvez également composer la configuration de connexion d’autres bibliothèques SQL en fonction du résultat de `sqlConnectionConfig.getConfig()`.

```ts
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
const config2 = await getTediousConnectionConfig(teamsfx "your database name");
const connection = new Connection(config);
connection.on("connect", (error) => {
  if (error) {
    console.log(error);
  }
});
```

</details>

<br>

<details>
<summary><b>Utiliser l’authentification basée sur un certificat dans Azure Function</b></summary>

```ts
const authConfig = {
  clientId: process.env.M365_CLIENT_ID,
  certificateContent: "The content of a PEM-encoded public/private key certificate",
  authorityHost: process.env.M365_AUTHORITY_HOST,
  tenantId: process.env.M365_TENANT_ID,
};
const teamsfx = new TeamsFx(IdentityType.App);
teamsfx.setCustomeConfig({
  certificateContent: "The content of a PEM-encoded public/private key certificate"
});
const token = teamsfx.getCredential().getToken();
```

</details>

<br>

<details>
<summary><b>Utiliser API Graph dans l’application bot</b></summary>

Ajouter `TeamsBotSsoPrompt` au jeu de dialogues.

```ts
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

</details>

<br>

## <a name="advanced-customization"></a>Personnalisation avancée

### <a name="configure-log"></a>Configurer le journal

Vous pouvez définir le niveau du journal client et rediriger les sorties lors de l’utilisation de cette bibliothèque. La journalisation est désactivée par défaut. Vous pouvez l’activer en définissant le niveau du journal.

#### <a name="enable-log-by-setting-log-level"></a>Activer le journal en définissant le niveau du journal

La journalisation est activée uniquement lorsque vous définissez le niveau du journal. Par défaut, il imprime les informations de journal dans la console.

Définissez le niveau du journal à l’aide de l’extrait de code suivant :

```ts
// Only need the warning and error messages.
setLogLevel(LogLevel.Warn);
```

Vous pouvez rediriger la sortie du journal en définissant une fonction d’enregistreur d’événements ou de journal personnalisée.

#### <a name="redirect-by-setting-custom-logger"></a>Rediriger en définissant l’enregistreur d’événements personnalisé

```ts
setLogLevel(LogLevel.Info);
// Set another logger if you want to redirect to Application Insights in Azure Function
setLogger(context.log);
```

#### <a name="redirect-by-setting-custom-log-function"></a>Rediriger en définissant une fonction de journal personnalisée

> [!NOTE]
> La fonction log ne prend pas effet si vous définissez un enregistreur d’événements personnalisé.

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

## <a name="override-configuration"></a>Remplacer la configuration
Vous pouvez passer une configuration personnalisée lors de la création d’une instance TeamsFx pour remplacer la configuration par défaut ou définir les champs requis lorsque des variables d’environnement sont manquantes.

- Si vous avez créé un projet d’onglet à l’aide de VS Code Shared Computer Toolkit, les valeurs de configuration suivantes sont utilisées à partir de variables d’environnement préconfigurées :
  * authorityHost (REACT_APP_AUTHORITY_HOST)
  * tenantId (REACT_APP_TENANT_ID)
  * clientId (REACT_APP_CLIENT_ID)
  * initiateLoginEndpoint (REACT_APP_START_LOGIN_PAGE_URL)
  * applicationIdUri (REACT_APP_START_LOGIN_PAGE_URL)
  * apiEndpoint (REACT_APP_FUNC_ENDPOINT)
  * apiName (REACT_APP_FUNC_NAME)

- Si vous avez créé un projet de fonction/bot Azure à l’aide de VS Code Shared Computer Toolkit, les valeurs de configuration suivantes seront utilisées à partir de variables d’environnement préconfigurées :
  * initiateLoginEndpoint (INITIATE_LOGIN_ENDPOINT)
  * authorityHost (M365_AUTHORITY_HOST)
  * tenantId (M365_TENANT_ID)
  * clientId (M365_CLIENT_ID)
  * clientSecret (M365_CLIENT_SECRET)
  * applicationIdUri (M365_APPLICATION_ID_URI)
  * apiEndpoint (API_ENDPOINT)
  * sqlServerEndpoint (SQL_ENDPOINT)
  * sqlUsername (SQL_USER_NAME)
  * sqlPassword (SQL_PASSWORD)
  * sqlDatabaseName (SQL_DATABASE_NAME)
  * sqlIdentityId (IDENTITY_ID)

## <a name="upgrade-latest-sdk-version"></a>Mettre à niveau la dernière version du Kit de développement logiciel (SDK)

Si vous utilisez la version du Kit de développement logiciel ( `loadConfiguration()`SDK), vous pouvez suivre ces étapes pour effectuer la mise à niveau vers la dernière version du SDK.
1. Supprimer `loadConfiguration()` et passer des paramètres personnalisés à l’aide de `new TeamsFx(IdentityType.User, { ...customConfig })`
2. Remplacer par `new TeamsUserCredential()``new TeamsFx()`
3. Remplacer par `new M365TenantCredential()``new TeamsFx(IdentityType.App)`
4. Remplacer par `new OnBehalfOfUserCredential(ssoToken)``new TeamsFx().setSsoToken(ssoToken)`
5. Passer l’instance des fonctions d’assistance `TeamsFx` pour remplacer l’instance d’informations d’identification

Pour plus d’informations, consultez la [classe TeamsFx](#teamsfx-class).

## <a name="next-step"></a>Étape suivante

[Exemples](https://github.com/OfficeDev/TeamsFx-Samples) de projet pour obtenir des exemples détaillés sur l’utilisation du Kit de développement logiciel (SDK) TeamsFx.

## <a name="see-also"></a>Voir aussi

[Galerie d’exemples Microsoft TeamsFx](https://github.com/OfficeDev/TeamsFx-Samples).
