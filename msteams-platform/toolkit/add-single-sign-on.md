---
title: Ajouter l’authentification unique à vos applications Teams
author: zyxiaoyuer
description: Décrit l’ajout de l’authentification unique de Teams Toolkit
ms.author: surbhigupta
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/20/2022
ms.openlocfilehash: db676795e394856f6e787086cae654efad79172a
ms.sourcegitcommit: 80edf3c964bb47a2ee13f9eda4334ad19e21f331
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/24/2022
ms.locfileid: "65655114"
---
# <a name="add-single-sign-on-experience"></a>Ajouter une expérience d’authentification unique

Microsoft Teams fournit une fonction d’authentification unique pour que l’application obtienne un jeton utilisateur Teams connecté pour accéder à Microsoft Graph et à d’autres API. Teams Toolkit facilite l’interaction en faisant abstraction de certains flux et intégrations Azure AD derrière certaines API simples. Cela vous permet d’ajouter facilement des fonctionnalités d’authentification unique à votre application Teams.

Pour les applications qui interagissent avec l’utilisateur dans une conversation, une équipe ou un canal, l’authentification unique se manifeste sous la forme d’une carte adaptative avec laquelle l’utilisateur peut interagir pour appeler le flux de consentement Azure AD.

## <a name="enable-sso-support"></a>Activer la prise en charge de l’authentification unique

Teams Toolkit vous aide à ajouter l’authentification unique aux fonctionnalités Teams suivantes :

* Tab
* Bot
* Bot de notification : serveur restify
* Bot de commandes

### <a name="add-sso-using-visual-studio-code"></a>Ajouter l’authentification unique à l’aide de code Visual Studio

Les étapes suivantes vous aident à ajouter l’authentification unique à l’aide de Teams Toolkit dans Visual Studio Code

1. Ouvrez **Microsoft Visual Studio Code**.
2. Sélectionnez Teams Toolkit :::image type="content" source="../assets/images/teams-toolkit-v2/add-sso/teams-toolkit-sidebar-icon.png" alt-text="sso add sidebar"::: from left navigation bar.
3. Sélectionnez **Ajouter des fonctionnalités** sous **DÉVELOPPEMENT**.

    :::image type="content" source="../assets/images/teams-toolkit-v2/add-sso/sso-add features.png" alt-text="sso add features":::

    * Vous pouvez également ouvrir la palette de commandes et sélectionner **Teams : Ajouter des fonctionnalités**

4. Sélectionnez **Authentification unique**.

    :::image type="content" source="../assets/images/teams-toolkit-v2/add-sso/sso-select features.png" alt-text="sso select":::

### <a name="add-sso-using-teamsfx-cli"></a>Ajouter l’authentification unique à l’aide de l’interface CLI TeamsFx

Vous pouvez exécuter `teamsfx add sso`  la commande dans le **répertoire racine de votre projet**

> [!Note]
> La fonctionnalité active l’authentification unique pour toutes les fonctionnalités applicables existantes. Suivez les mêmes étapes pour activer l’authentification unique si vous ajoutez une fonctionnalité ultérieurement au projet.

## <a name="customize-your-project-using-teams-toolkit"></a>Personnaliser votre projet à l’aide de Teams Toolkit

Le tableau suivant répertorie les modifications apportées Teams Toolkit à votre projet :

   |**Type (Type)**|**Fichier**|**Objectif**|
   |--------|--------|-----------|
   |Créer|`aad.template.json` Sous `template/appPackage`|Le manifeste d’application Azure AD représente votre application Azure AD. `template/appPackage` permet d’inscrire une application Azure AD lors de l’étape de débogage ou de provisionnement local.|
   |Modifier|`manifest.template.json` Sous `template/appPackage`|Un `webApplicationInfo` objet est ajouté à votre modèle de manifeste d’application Teams. Teams nécessite ce champ pour activer l’authentification unique. La modification est en vigueur lorsque vous déclenchez un débogage ou un provisionnement local.|
   |Créer|`auth/tab`|Le code de référence, les pages de redirection d’authentification et un `README.md` fichier sont générés dans ce chemin d’accès pour un projet d’onglet.|
   |Créer|`auth/bot`|Le code de référence, les pages de redirection d’authentification et un `README.md` fichier sont générés dans ce chemin d’accès pour un projet de bot.|

> [!Note]
> En ajoutant l’authentification unique, Teams Toolkit ne change rien dans le cloud tant que vous n’avez pas déclenché le débogage local. Mettez à jour votre code pour vous assurer que l’authentification unique fonctionne dans le projet.

## <a name="update-your-application-to-use-sso"></a>Mettre à jour votre application pour utiliser l’authentification unique

Les étapes suivantes vous aident à activer l’authentification unique dans votre application.

> [!NOTE]
> Ces modifications sont basées sur les modèles que nous échafaudons.

---
<br>
<br><details>
<summary><b>Projet d’onglet </b></summary>

1. Copier `auth-start.html` et `auth-end.htm`** dans le `auth/public` dossier vers `tabs/public/`. Teams Toolkit inscrit ces deux points de terminaison dans Azure AD pour le flux de redirection d’Azure AD.

2. Copier le `sso` dossier sous `auth/tab` .`tabs/src/sso/`

    * `InitTeamsFx`: le fichier implémente une fonction qui initialise le Kit de développement logiciel (SDK) TeamsFx et ouvre `GetUserProfile` le composant après l’initialisation du SDK

    * `GetUserProfile`: le fichier implémente une fonction qui appelle Microsoft API Graph pour obtenir des informations utilisateur

3. Exécutez `npm install @microsoft/teamsfx-react` sous `tabs/`.

4. Ajoutez les lignes suivantes pour `tabs/src/components/sample/Welcome.tsx` importer `InitTeamsFx`:

    ```Bash

    import { InitTeamsFx } from "../../sso/InitTeamsFx";

    ```

5. Remplacez la ligne suivante : `<AddSSO />` `<InitTeamsFx />` pour remplacer le composant par `InitTeamsFx` le `AddSso` composant.

</details>
<details>
<summary><b>Projet de bot </b></summary>

1. Copier `auth/bot/public` le dossier vers `bot/src`. Les deux dossiers contiennent des pages HTML utilisées pour la redirection d’authentification. Vous devez modifier `bot/src/index` le fichier pour ajouter le routage à ces pages.

2. Copier `auth/bot/sso` le dossier vers `bot/src`. Les deux dossiers contiennent trois fichiers comme référence pour l’implémentation de l’authentification unique :

    * `showUserInfo`: il implémente une fonction pour obtenir des informations utilisateur avec un jeton d’authentification unique. Vous pouvez suivre cette procédure pour créer votre propre méthode qui nécessite un jeton d’authentification unique.

    * `ssoDialog`: il crée un [ComponentDialog](/javascript/api/botbuilder-dialogs/componentdialog?view=botbuilder-ts-latest&preserve-view=true) utilisé pour l’authentification unique.

    * `teamsSsoBot`: il crée un [TeamsActivityHandler](/javascript/api/botbuilder/teamsactivityhandler?view=botbuilder-ts-latest&preserve-view=true) avec `ssoDialog` et l’ajoute `showUserInfo` en tant que commande qui peut être déclenchée.

3. Suivez l’exemple de code et inscrivez votre propre commande `addCommand` dans ce fichier (facultatif).

4. Exécutez `npm install isomorphic-fetch` sous `bot/`.

5. Exécutez `npm install copyfiles` sous `bot/` et remplacez la ligne suivante dans package.json :
  
   ```JSON

   "build": "tsc --build",

    ```

    avec le 

   ```JSON

   "build": "tsc --build && copyfiles public/*.html lib/",

   ```

   Les pages HTML utilisées pour la redirection d’authentification sont copiées lors de la génération de ce projet de bot.

6. Après avoir ajouté les fichiers suivants, vous devez créer une instance `teamsSsoBot` dans le `bot/src/index` fichier. Remplacez le code suivant :

   ```Bash
  
   // Process Teams activity with Bot Framework.
   server.post("/api/messages", async (req, res) => {
   await commandBot.requestHandler(req, res);
   });  

   ```

    avec le 

   ```Bash

   const handler = new TeamsSsoBot();
   // Process Teams activity with Bot Framework.
   server.post("/api/messages", async (req, res) => {
       await commandBot.requestHandler(req, res, async (context)=> {
           await handler.run(context);
       });
   });

   ```

7. Ajoutez les itinéraires HTML dans le `bot/src/index` fichier :

   ```Bash

   server.get(
       "/auth-*.html",
       restify.plugins.serveStatic({
           directory: path.join(__dirname, "public"),
       })
   );

   ```

8. Ajoutez les lignes suivantes à `bot/src/index` importer `teamsSsoBot` et `path`:

   ```Bash

   // For ts:
   import { TeamsSsoBot } from "./sso/teamsSsoBot";
   const path = require("path");

   // For js:
   const { TeamsSsoBot } = require("./sso/teamsSsoBot");
   const path = require("path");

   ```

9. Inscrivez votre commande dans le manifeste de l’application Teams. Ouvrez `templates/appPackage/manifest.template.json`et ajoutez les lignes suivantes sous `command` `commandLists` votre bot :

   ```JSON

   {
       "title": "show",
       "description": "Show user profile using Single Sign On feature"
   }

   ```
</details>
<details>
<summary><b>Ajouter une nouvelle commande au bot </b></summary>

> [!NOTE]
> Actuellement, ces instructions s’appliquent à `command bot`. Si vous commencez par un `bot`exemple [bot-sso](https://github.com/OfficeDev/TeamsFx-Samples/tree/v2/bot-sso).

Les étapes suivantes vous aident à ajouter une nouvelle commande, après avoir ajouté l’authentification unique dans votre projet :

1. Créez un fichier (`todo.ts`ou`todo.js`) sous `bot/src/` et ajoutez votre propre logique métier pour appeler API Graph :

# <a name="typescript"></a>[TypeScript](#tab/typescript)

   ```typescript
   // for TypeScript:
export async function showUserImage(
    context: TurnContext,
    ssoToken: string,
    param: any[]
): Promise<DialogTurnResult> {
    await context.sendActivity("Retrieving user photo from Microsoft Graph ...");

    // Init TeamsFx instance with SSO token
    const teamsfx = new TeamsFx().setSsoToken(ssoToken);

    // Update scope here. For example: Mail.Read, etc.
    const graphClient = createMicrosoftGraphClient(teamsfx, param[0]);
    
    // You can add following code to get your photo:
    // let photoUrl = "";
    // try {
    //   const photo = await graphClient.api("/me/photo/$value").get();
    //   photoUrl = URL.createObjectURL(photo);
    // } catch {
    //   // Could not fetch photo from user's profile, return empty string as placeholder.
    // }
    // if (photoUrl) {
    //   await context.sendActivity(
    //     `You can find your photo here: ${photoUrl}`
    //   );
    // } else {
    //   await context.sendActivity("Could not retrieve your photo from Microsoft Graph. Please make sure you have uploaded your photo.");
    // }

    return;
}  
   ```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

   ```javaScript
   // for JavaScript:
export async function showUserImage(context, ssoToken, param) {
    await context.sendActivity("Retrieving user photo from Microsoft Graph ...");

    // Init TeamsFx instance with SSO token
    const teamsfx = new TeamsFx().setSsoToken(ssoToken);

    // Update scope here. For example: Mail.Read, etc.
    const graphClient = createMicrosoftGraphClient(teamsfx, param[0]);
    
    // You can add following code to get your photo:
    // let photoUrl = "";
    // try {
    //   const photo = await graphClient.api("/me/photo/$value").get();
    //   photoUrl = URL.createObjectURL(photo);
    // } catch {
    //   // Could not fetch photo from user's profile, return empty string as placeholder.
    // }
    // if (photoUrl) {
    //   await context.sendActivity(
    //     `You can find your photo here: ${photoUrl}`
    //   );
    // } else {
    //   await context.sendActivity("Could not retrieve your photo from Microsoft Graph. Please make sure you have uploaded your photo.");
    // }

    return;
}
   ```

---

2. Inscrire une nouvelle commande

   * Ajoutez la ligne suivante pour la nouvelle inscription de commande à l’aide `addCommand` de `teamsSsoBot`:

   ```bash

   this.dialog.addCommand("ShowUserProfile", "show", showUserInfo);

   ```

   * Ajoutez les lignes suivantes après la ligne ci-dessus pour inscrire une nouvelle commande `photo` et hook avec la méthode `showUserImage` ajoutée ci-dessus :

   ```bash

   // As shown here, you can add your own parameter into the `showUserImage` method
   // You can also use regular expression for the command here
   const scope = ["User.Read"];
   this.dialog.addCommand("ShowUserPhoto", new RegExp("photo\s*.*"), showUserImage, scope);

   ```

3. Inscrivez votre commande dans le manifeste de l’application Teams. Ouvrez `templates/appPackage/manifest.template.json`et ajoutez les lignes suivantes sous `command` `commandLists` votre bot :

   ```JSON

   {
       "title": "photo",
       "description": "Show user photo using Single Sign On feature"
   }

   ```
</details>
<br>

## <a name="debug-your-application"></a>Déboguer votre application

Appuyez sur F5 pour déboguer votre application. Teams Toolkit utilise le fichier manifeste Azure AD pour inscrire une application Azure AD pour l’authentification unique. Pour Teams fonctionnalités de débogage local du Kit de ressources, consultez [Déboguer votre application Teams localement](debug-local.md).

## <a name="customize-azure-ad-application-registration"></a>Personnaliser l’inscription d’application Azure AD

Le [manifeste de l’application Azure AD](/azure/active-directory/develop/reference-app-manifest) vous permet de personnaliser différents aspects de l’inscription d’application. Vous pouvez mettre à jour le manifeste en fonction des besoins. Si vous devez inclure des autorisations d’API supplémentaires pour accéder aux API souhaitées, consultez [les autorisations d’API pour accéder aux API souhaitées](https://github.com/OfficeDev/TeamsFx/wiki/#customize-aad-manifest-template).
Pour afficher votre application Azure AD dans le portail Azure, consultez [Afficher l’application Azure AD dans Portail Azure](https://github.com/OfficeDev/TeamsFx/wiki/Manage-AAD-application-in-Teams-Toolkit#How-to-view-the-AAD-app-on-the-Azure-portal). 

## <a name="sso-authentication-concepts"></a>Concepts d’authentification unique

Les concepts suivants vous aident à effectuer l’authentification unique :

### <a name="working-of-sso-in-teams"></a>Fonctionnement de l’authentification unique dans Teams

L’authentification unique dans Microsoft Azure Active Directory (Azure AD) actualise silencieusement le jeton d’authentification pour réduire le nombre de fois où les utilisateurs doivent entrer leurs informations d’identification de connexion. Si les utilisateurs acceptent d'utiliser votre application, ils n'ont pas besoin de donner à nouveau leur consentement sur un autre appareil car ils sont automatiquement connectés.

Teams onglets et bots ont un flux similaire pour la prise en charge de l’authentification unique. Pour plus d’informations, consultez :

1. [Authentification unique (SSO) dans Tabs](../tabs/how-to/authentication/auth-aad-sso.md)
2. [Authentification unique (SSO) dans Bots](../bots/how-to/authentication/auth-aad-sso-bots.md)

### <a name="simplified-sso-with-teamsfx"></a>Authentification unique simplifiée avec TeamsFx

TeamsFx aide à réduire les tâches des développeurs en utilisant Teams SSO et en accédant aux ressources cloud jusqu’à des instructions sur une seule ligne sans aucune configuration.

Avec le Kit de développement logiciel (SDK) TeamsFx, vous pouvez écrire du code d’authentification utilisateur de manière simplifiée à l’aide des informations d’identification :

1. Identité de l’utilisateur dans l’environnement du navigateur : `TeamsUserCredential` représente Teams’identité de l’utilisateur actuel.
2. Identité de l’utilisateur dans Node.js environnement : `OnBehalfOfUserCredentail` utilise le flux On-Behalf-Of et Teams jeton d’authentification unique.
3. Identité d’application dans Node.js environnement : `AppCredential` représente l’identité de l’application.

Pour plus d’informations sur le Kit de développement logiciel (SDK) TeamsFx, consultez :

* Informations de référence sur le SDK ou [l’API](/javascript/api/@microsoft/teamsfx/?view=msteams-client-js-latest&preserve-view=true) [TeamsFx](TeamsFx-SDK.md)
* [Galerie d’exemples Microsoft Teams Framework (TeamsFx)](https://github.com/OfficeDev/TeamsFx-Samples/tree/v2)

## <a name="see-also"></a>Voir aussi

* [Préparer des comptes pour créer des applications Teams](accounts.md)
