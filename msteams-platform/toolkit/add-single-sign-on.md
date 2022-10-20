---
title: Ajouter l’authentification unique à vos applications Teams
author: zyxiaoyuer
description: Dans ce module, découvrez comment ajouter l’authentification unique (SSO) de Teams Toolkit, activer la prise en charge de l’authentification unique, mettre à jour votre application pour utiliser l’authentification unique
ms.author: surbhigupta
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/20/2022
ms.openlocfilehash: 7318ffbfe6c0fff852f493c90afe9a832a827110
ms.sourcegitcommit: e5c45071421d257d68a73406137edff5bdc5a722
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/20/2022
ms.locfileid: "68654511"
---
# <a name="add-single-sign-on-to-teams-app"></a>Ajouter l'authentification unique à l'application Teams

Microsoft Teams fournit une fonction d’authentification unique pour que l’application obtienne un jeton d’utilisateur Teams connecté pour accéder à Microsoft Graph et à d’autres API. Teams Toolkit facilite l’interaction en faisant abstraction de certains flux et intégrations Azure AD derrière certaines API simples. Cela vous permet d’ajouter facilement des fonctionnalités d’authentification unique à votre application Teams.

Pour les applications qui interagissent avec l’utilisateur dans une conversation, une équipe ou un canal, l’authentification unique se manifeste sous la forme d’une carte adaptative avec laquelle l’utilisateur peut interagir pour appeler le flux de consentement Azure AD.

## <a name="enable-sso-support"></a>Activer la prise en charge de l’authentification unique

Teams Toolkit vous aide à ajouter l’authentification unique aux fonctionnalités Teams suivantes :

* Tab
* Bot
* Bot de notification : serveur restify
* Bot de commandes
* Extension de message

### <a name="add-sso-using-visual-studio-code"></a>Ajouter l’authentification unique à l’aide de Visual Studio Code

Pour ajouter l’authentification unique à l’aide du Kit de ressources Teams dans Visual Studio Code, procédez comme suit :

1. Ouvrez **Microsoft Visual Studio Code**.
2. La capture d’écran sélectionner le Kit de ressources Teams :::image type="content" source="~/assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.png" alt-text="est un exemple de l’option Teams Toolkit dans Visual Studio Code."::: à partir de la barre de navigation gauche.
3. Sélectionnez **Ajouter des fonctionnalités** sous **DÉVELOPPEMENT**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/add-sso/sso-add features.png" alt-text="Capture d’écran montrant l’option Ajouter des fonctionnalités sous l’option Développement dans Visual Studio Code.":::

   * Vous pouvez également ouvrir la palette de commandes et sélectionner **Teams : Ajouter des fonctionnalités**.

4. Sélectionnez **Authentification unique**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/add-sso/sso-select features.png" alt-text="Capture d’écran montrant la fonctionnalité d’authentification unique mise en évidence en rouge dans Visual Studio Code.":::

### <a name="add-sso-using-teamsfx-cli"></a>Ajouter l’authentification unique à l’aide de l’interface CLI TeamsFx

Vous pouvez exécuter `teamsfx add sso` la commande dans le **répertoire racine de votre projet**.

> [!NOTE]
> La fonctionnalité active l’authentification unique pour toutes les fonctionnalités applicables existantes. Suivez les mêmes étapes pour activer l’authentification unique si vous ajoutez une fonctionnalité ultérieurement au projet.

## <a name="customize-your-project-using-teams-toolkit"></a>Personnaliser votre projet à l’aide du Kit de ressources Teams

Le tableau suivant répertorie les modifications apportées par Teams Toolkit à votre projet :

| **Type** | **Fichier**                                             | **Objectif**                                                                                                                                                                               |
| -------- | ---------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Créer   | `aad.template.json` Sous `template/appPackage`      | Le manifeste d’application Azure AD représente votre application Azure AD. `template/appPackage` permet d’inscrire une application Azure AD lors de l’étape de débogage ou de provisionnement local.                                |
| Modifier   | `manifest.template.json` Sous `template/appPackage` | Un `webApplicationInfo` objet est ajouté à votre modèle de manifeste d’application Teams. Teams requiert ce champ pour activer l’authentification unique. La modification est en vigueur lorsque vous déclenchez un débogage ou un provisionnement local. |
| Créer   | `auth/tab`                                           | Le code de référence, les pages de redirection d’authentification et `README.md` les fichiers sont générés dans ce chemin d’accès pour un projet d’onglet.                                                                                  |
| Créer   | `auth/bot`                                           | Le code de référence, les pages de redirection d’authentification et `README.md` les fichiers sont générés dans ce chemin d’accès pour un projet de bot.                                                                                  |

> [!NOTE]
> En ajoutant l’authentification unique, Teams Toolkit ne change rien dans le cloud tant que vous n’avez pas déclenché le débogage local. Mettez à jour votre code pour vous assurer que l’authentification unique fonctionne dans le projet.

## <a name="update-your-application-to-use-sso"></a>Mettre à jour votre application pour utiliser l’authentification unique

Pour activer l’authentification unique dans votre application, procédez comme suit :

> [!NOTE]
> Ces modifications sont basées sur les modèles que nous échafaudons.

---

<br>
<br><details>
<summary><b>Projet d’onglet </b></summary>

1. Copier `auth-start.html` et `auth-end.htm`\*\* dans le `auth/public` dossier vers .`tabs/public/` Teams Toolkit inscrit ces deux points de terminaison dans Azure AD pour le flux de redirection d’Azure AD.

2. Copier le `sso` dossier sous `auth/tab` .`tabs/src/sso/`

   * `InitTeamsFx`: le fichier implémente une fonction qui initialise le Kit de développement logiciel (SDK) TeamsFx et ouvre `GetUserProfile` le composant après l’initialisation du SDK.

   * `GetUserProfile`: le fichier implémente une fonction qui appelle Microsoft API Graph pour obtenir des informations utilisateur.

3. Exécutez `npm install @microsoft/teamsfx-react` sous `tabs/`.

4. Ajoutez les lignes suivantes pour `tabs/src/components/sample/Welcome.tsx` importer `InitTeamsFx`:

   ```Bash

   import { InitTeamsFx } from "../../sso/InitTeamsFx";

   ```

5. Remplacez la ligne suivante :

   `<AddSSO />`pour `<InitTeamsFx />` remplacer le composant `InitTeamsFx` par le `AddSso` composant.

</details>
<details>
<summary><b>Projet de bot </b></summary>

#### <a name="set-up-the-azure-ad-redirects"></a>Configurer les redirections Azure AD

1. Déplacer le `auth/bot/public` dossier vers `bot/src`. Ce dossier contient des pages HTML que l’application bot héberge. Lorsque le flux d’authentification unique est lancé avec Azure AD, il redirige l’utilisateur vers les pages HTML.
1. Modifiez le vôtre `bot/src/index` pour ajouter les itinéraires appropriés `restify` aux pages HTML.

   ```ts
   const path = require("path");

   server.get(
     "/auth-*.html",
     restify.plugins.serveStatic({
       directory: path.join(__dirname, "public"),
     })
   );
   ```

#### <a name="update-your-app"></a>Mettre à jour votre application

Le gestionnaire `ProfileSsoCommandHandler` de commandes SSO utilise un jeton Azure AD pour appeler Microsoft Graph. Ce jeton est obtenu à l’aide du jeton d’utilisateur Teams connecté. Le flux est regroupé dans une boîte de dialogue qui affiche une boîte de dialogue de consentement si nécessaire.

1. Déplacer le `profileSsoCommandHandler` fichier sous le `auth/bot/sso` dossier vers `bot/src`. `ProfileSsoCommandHandler` la classe est un gestionnaire de commandes SSO pour obtenir des informations utilisateur avec le jeton SSO, suivre cette méthode et créer votre propre gestionnaire de commandes SSO.
1. Ouvrez `package.json` le fichier et vérifiez que la version du Kit de développement logiciel (SDK) teamsfx >= 1.2.0.
1. Exécutez la `npm install isomorphic-fetch --save` commande dans le `bot` dossier.
1. Pour le script ts, exécutez la `npm install copyfiles --save-dev` commande dans le `bot` dossier et remplacez les lignes suivantes dans `package.json`:

   ```json
   "build": "tsc --build && shx cp -r ./src/adaptiveCards ./lib/src",
   ```

    avec le 

   ```json
   "build": "tsc --build && shx cp -r ./src/adaptiveCards ./lib/src && copyfiles src/public/*.html lib/",
   ```

   Cette opération copie les pages HTML utilisées pour la redirection d’authentification lors de la génération du projet de bot.

1. Pour que le flux de consentement de l’authentification unique fonctionne, remplacez le code suivant dans le `bot/src/index` fichier :

   ```ts
   server.post("/api/messages", async (req, res) => {
     await commandBot.requestHandler(req, res);
   });
   ```

    avec le 

   ```ts
   server.post("/api/messages", async (req, res) => {
     await commandBot.requestHandler(req, res).catch((err) => {
       // Error message including "412" means it is waiting for user's consent, which is a normal process of SSO, sholdn't throw this error.
       if (!err.message.includes("412")) {
         throw err;
       }
     });
   });
   ```

1. Remplacez les options par exemple `ConversationBot` pour `bot/src/internal/initialize` ajouter la configuration de l’authentification unique et le gestionnaire de commandes SSO :

   ```ts
   export const commandBot = new ConversationBot({
       ...
       command: {
           enabled: true,
           commands: [new HelloWorldCommandHandler()],
       },
   });
   ```

    avec le 

   ```ts
   import { ProfileSsoCommandHandler } from "../profileSsoCommandHandler";

   export const commandBot = new ConversationBot({
       ...
       // To learn more about ssoConfig, please refer teamsfx sdk document: https://docs.microsoft.com/microsoftteams/platform/toolkit/teamsfx-sdk
       ssoConfig: {
           aad :{
               scopes:["User.Read"],
           },
       },
       command: {
           enabled: true,
           commands: [new HelloWorldCommandHandler() ],
           ssoCommands: [new ProfileSsoCommandHandler()],
       },
   });
   ```

1. Inscrivez votre commande dans le manifeste de l’application Teams. Ouvrez `templates/appPackage/manifest.template.json`et ajoutez les lignes suivantes sous `commands` `commandLists` votre bot :

   ```json
   {
     "title": "profile",
     "description": "Show user profile using Single Sign On feature"
   }
   ```

#### <a name="add-a-new-sso-command-to-the-bot-optional"></a>Ajouter une nouvelle commande SSO au bot (facultatif)

Après avoir ajouté l’authentification unique dans votre projet, vous pouvez ajouter une nouvelle commande d’authentification unique.

1. Créez un fichier tel que `photoSsoCommandHandler.ts` ou `photoSsoCommandHandler.js` in `bot/src/` et ajoutez votre propre gestionnaire de commandes SSO pour appeler API Graph :

   ```TypeScript
   // for TypeScript:
   import { Activity, TurnContext, ActivityTypes } from "botbuilder";
   import "isomorphic-fetch";
   import {
       CommandMessage,
       TriggerPatterns,
       TeamsFx,
       createMicrosoftGraphClient,
       TeamsFxBotSsoCommandHandler,
       TeamsBotSsoPromptTokenResponse,
   } from "@microsoft/teamsfx";

   export class PhotoSsoCommandHandler implements TeamsFxBotSsoCommandHandler {
       triggerPatterns: TriggerPatterns = "photo";

       async handleCommandReceived(
           context: TurnContext,
           message: CommandMessage,
           tokenResponse: TeamsBotSsoPromptTokenResponse,
       ): Promise<string | Partial<Activity> | void> {
           await context.sendActivity("Retrieving user information from Microsoft Graph ...");

           const teamsfx = new TeamsFx().setSsoToken(tokenResponse.ssoToken);

           const graphClient = createMicrosoftGraphClient(teamsfx, ["User.Read"]);

           let photoUrl = "";
           try {
               const photo = await graphClient.api("/me/photo/$value").get();
               const arrayBuffer = await photo.arrayBuffer();
               const buffer=Buffer.from(arrayBuffer, 'binary');
               photoUrl = "data:image/png;base64," + buffer.toString("base64");
           } catch {
               // Could not fetch photo from user's profile, return empty string as placeholder.
           }
           if (photoUrl) {
               const photoMessage: Partial<Activity> = {
                   type: ActivityTypes.Message,
                   text: 'This is your photo:',
                   attachments: [
                       {
                           name: 'photo.png',
                           contentType: 'image/png',
                           contentUrl: photoUrl
                       }
                   ]
               };
               return photoMessage;
           } else {
               return "Could not retrieve your photo from Microsoft Graph. Please make sure you have uploaded your photo.";
           }
       }
   }
   ```

   ```javascript
   // for JavaScript:
   const { ActivityTypes } = require("botbuilder");
   require("isomorphic-fetch");
   const {
     createMicrosoftGraphClient,
     TeamsFx,
   } = require("@microsoft/teamsfx");

   class PhotoSsoCommandHandler {
     triggerPatterns = "photo";

     async handleCommandReceived(context, message, tokenResponse) {
       await context.sendActivity(
         "Retrieving user information from Microsoft Graph ..."
       );

       const teamsfx = new TeamsFx().setSsoToken(tokenResponse.ssoToken);

       const graphClient = createMicrosoftGraphClient(teamsfx, ["User.Read"]);

       let photoUrl = "";
       try {
         const photo = await graphClient.api("/me/photo/$value").get();
         const arrayBuffer = await photo.arrayBuffer();
         const buffer = Buffer.from(arrayBuffer, "binary");
         photoUrl = "data:image/png;base64," + buffer.toString("base64");
       } catch {
         // Could not fetch photo from user's profile, return empty string as placeholder.
       }
       if (photoUrl) {
         const photoMessage = {
           type: ActivityTypes.Message,
           text: "This is your photo:",
           attachments: [
             {
               name: "photo.png",
               contentType: "image/png",
               contentUrl: photoUrl,
             },
           ],
         };
         return photoMessage;
       } else {
         return "Could not retrieve your photo from Microsoft Graph. Please make sure you have uploaded your photo.";
       }
     }
   }

   module.exports = {
     PhotoSsoCommandHandler,
   };
   ```

1. Ajoutez `PhotoSsoCommandHandler` une instance au `ssoCommands` tableau dans `bot/src/internal/initialize.ts`:

   ```ts
   // for TypeScript:
   import { PhotoSsoCommandHandler } from "../photoSsoCommandHandler";

   export const commandBot = new ConversationBot({
       ...
       command: {
           ...
           ssoCommands: [new ProfileSsoCommandHandler(), new PhotoSsoCommandHandler()],
       },
   });
   ```

   ```javascript
   // for JavaScript:
   ...
   const { PhotoSsoCommandHandler } = require("../photoSsoCommandHandler");

   const commandBot = new ConversationBot({
       ...
       command: {
           ...
           ssoCommands: [new ProfileSsoCommandHandler(), new PhotoSsoCommandHandler()]
       },
   });
   ...

   ```

1. Inscrivez votre commande dans le manifeste de l’application Teams. Ouvrez `templates/appPackage/manifest.template.json`et ajoutez les lignes suivantes sous `commands` `commandLists` votre bot :

   ```JSON

   {
       "title": "photo",
       "description": "Show user photo using Single Sign On feature"
   }

   ```

</details>

<details>
<summary><b>Projet d’extension de message </b></summary>

L’exemple de logique métier fournit un gestionnaire `TeamsBot` qui étend TeamsActivityHandler et le remplace `handleTeamsMessagingExtensionQuery`.

Vous pouvez mettre à jour la logique de requête dans le `handleMessageExtensionQueryWithToken` jeton with, qui est obtenu à l’aide du jeton d’utilisateur Teams connecté.

Pour que cela fonctionne dans votre application :

1. Déplacer le `auth/bot/public` dossier vers `bot`. Ce dossier contient des pages HTML que l’application bot héberge. Quand des flux d’authentification unique sont lancés avec Azure AD, Azure AD redirige l’utilisateur vers ces pages.

1. Modifiez votre `bot/index` page pour ajouter les itinéraires appropriés `restify` à ces pages.

    ```ts
    const path = require("path");

    server.get(
        "/auth-*.html",
        restify.plugins.serveStatic({
            directory: path.join(__dirname, "public"),
        })
    );
    ```

1. `handleTeamsMessagingExtensionQuery` Remplacer l’interface sous `bot/teamsBot`. Vous pouvez suivre l’exemple de code dans la `handleMessageExtensionQueryWithToken` logique de votre propre requête.

1. Ouvrez `bot/package.json`, vérifiez que `@microsoft/teamsfx` la version >= 1.2.0

1. Installez `isomorphic-fetch` les packages npm dans votre projet de bot.

1. (Pour ts uniquement) Installez `copyfiles` les packages npm dans votre projet de bot, ajoutez ou mettez à jour le `build` script comme `bot/package.json` suit :

    ```json
    "build": "tsc --build && copyfiles ./public/*.html lib/",
    ```

    Ainsi, les pages HTML utilisées pour la redirection d’authentification sont copiées lors de la création de ce projet de bot.

1. Mettez à jour `templates/appPackage/aad.template.json` vos étendues utilisées dans `handleMessageExtensionQueryWithToken`.

    ```json
    "requiredResourceAccess": [
        {
            "resourceAppId": "Microsoft Graph",
            "resourceAccess": [
                {
                    "id": "User.Read",
                    "type": "Scope"
                }
            ]
        }
    ]
    ```

</details>

<br>

## <a name="debug-your-application"></a>Déboguer votre application

Appuyez sur F5 pour déboguer votre application. Teams Toolkit utilise le fichier manifeste Azure AD pour inscrire une application Azure AD pour l’authentification unique. Pour les fonctionnalités de débogage local du Kit de ressources Teams, consultez [Déboguer votre application Teams localement](debug-local.md).

## <a name="customize-azure-ad-application-registration"></a>Personnaliser l’inscription d’application Azure AD

Le [manifeste de l’application Azure AD](/azure/active-directory/develop/reference-app-manifest) vous permet de personnaliser différents aspects de l’inscription d’application. Vous pouvez mettre à jour le manifeste en fonction des besoins. Si vous devez inclure davantage d’autorisations d’API pour accéder aux API souhaitées, consultez [les autorisations d’API pour accéder aux API souhaitées](https://github.com/OfficeDev/TeamsFx/wiki/#customize-aad-manifest-template).
Pour afficher votre application Azure AD dans Portail Azure, consultez [Afficher l’application Azure AD dans Portail Azure](https://github.com/OfficeDev/TeamsFx/wiki/Manage-AAD-application-in-Teams-Toolkit#How-to-view-the-AAD-app-on-the-Azure-portal).

## <a name="sso-authentication-concepts"></a>Concepts d’authentification unique

Les concepts suivants vous aident à utiliser l’authentification unique :

### <a name="working-of-sso-in-teams"></a>Fonctionnement de l’authentification unique dans Teams

L’authentification unique dans Microsoft Azure Active Directory (Azure AD) actualise silencieusement le jeton d’authentification pour réduire le nombre de fois où les utilisateurs doivent entrer leurs informations d’identification de connexion. Si les utilisateurs acceptent d'utiliser votre application, ils n'ont pas besoin de donner à nouveau leur consentement sur un autre appareil car ils sont automatiquement connectés.

Les onglets et les bots Teams ont un flux similaire pour la prise en charge de l’authentification unique. Pour plus d’informations, consultez l’article suivant :

1. [Authentification unique (SSO) dans Tabs](../tabs/how-to/authentication/tab-sso-overview.md)
1. [Authentification unique (SSO) dans Bots](../bots/how-to/authentication/auth-aad-sso-bots.md)

### <a name="simplified-sso-with-teamsfx"></a>Authentification unique simplifiée avec TeamsFx

TeamsFx permet de réduire les tâches des développeurs en utilisant l’authentification unique et en accédant aux ressources cloud jusqu’à des instructions sur une seule ligne sans aucune configuration.

Avec le Kit de développement logiciel (SDK) TeamsFx, vous pouvez écrire du code d’authentification utilisateur de manière simplifiée à l’aide des informations d’identification :

1. Identité de l’utilisateur dans l’environnement du navigateur : `TeamsUserCredential` représente l’identité de l’utilisateur actuel de Teams.
1. Identité de l’utilisateur dans Node.js environnement : `OnBehalfOfUserCredential` utilise le flux On-Behalf-Of et le jeton d’authentification unique.
1. Identité d’application dans Node.js environnement : `AppCredential` représente l’identité de l’application.

Pour plus d’informations sur le Kit de développement logiciel (SDK) TeamsFx, consultez :

* Informations de référence sur le SDK ou [l’API](/javascript/api/@microsoft/teamsfx/?view=msteams-client-js-latest&preserve-view=true) [TeamsFx](TeamsFx-SDK.md)
* [Galerie d’exemples Microsoft Teams Framework (TeamsFx)](https://github.com/OfficeDev/TeamsFx-Samples/tree/v2)

## <a name="see-also"></a>Voir aussi

[Conditions préalables à la création de votre application Teams](tools-prerequisites.md)
