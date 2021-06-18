---
title: Mise en place - Conditions préalables
author: adrianhall
description: Découvrez comment commencer à développer des applications Microsoft Teams et configurer votre environnement.
ms.author: adhal
ms.date: 05/24/2021
ms.topic: quickstart
ms.openlocfilehash: 6496d238b3858c1df974732fa57c28eed7c54eb2
ms.sourcegitcommit: 14409950307b135265c8582408be5277b35131dd
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2021
ms.locfileid: "52994188"
---
# <a name="prerequisites-get-started-with-microsoft-teams-app-development"></a>Conditions préalables : mise en place du développement d’applications Microsoft Teams

Avant de créer votre première application Teams, vous devez installer quelques outils et configurer votre environnement de développement.

## <a name="install-required-tools"></a>Installer les outils requis

Certains des outils dont vous avez besoin dépendent de la façon dont vous préférez créer votre application Teams :

- [Node.js](https://nodejs.org/en/download/) (utilisez la dernière version de LTS v14)
- Un navigateur avec des outils de développement, tels [que Microsoft Edge](https://www.microsoft.com/edge) (recommandé) ou Google [Chrome](https://www.google.com/chrome/)
- Si vous développez avec JavaScript, TypeScript ou SharePoint Framework (SPFx), installez [Visual Studio Code](https://code.visualstudio.com/download), version 1.55 ou ultérieure.  
- Si vous développez avec .NET, installez [Visual Studio 2019.](https://visualstudio.com/download) Veillez à installer la **charge ASP.NET développement web et** web ou la charge de travail de développement **.NET Core sur plusieurs plateformes.**

> [!WARNING]
> Il existe des problèmes connus avec `npm@7` , empaqueté avec Node v15 et ultérieur. Si vous avez des problèmes d’exécution, assurez-vous que vous utilisez `npm install` Node v14 (LTS)

## <a name="install-the-teams-toolkit"></a>Installer la Shared Computer Toolkit Teams

La Shared Computer Toolkit Teams simplifie le processus de développement avec des outils pour mettre en service et déployer des ressources cloud pour votre application, publier dans le magasin Teams, etc. Vous pouvez utiliser la boîte à outils avec Visual Studio Code, Visual Studio ou en tant qu’CLI (appelé `teamsfx` ).

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Ouvrez Visual Studio Code.
1. Sélectionnez l’affichage Extensions (**Ctrl+Shift+X**  /  **⌘⇧-X** ou Afficher **> extensions**).
1. Dans la zone de recherche, entrez **Teams Shared Computer Toolkit**.
1. Sélectionnez le bouton d’installation vert en Shared Computer Toolkit Teams.

Vous pouvez également trouver l’Shared Computer Toolkit Teams sur [le Visual Studio Marketplace de code.](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)

Les outils suivants peuvent être installés par l’extension Visual Studio code lorsque cela est nécessaire. S’il est déjà installé, la version installée peut être utilisée à la place. Si vous utilisez Linux, y compris WSL, vous devez installer ces outils avant d’utiliser :

- [Outils azure Functions Core](/azure/azure-functions/functions-run-local)

    Azure Functions Core Tools permet d’exécuter localement tous les composants principaux lors d’une exécution de débogage locale, y compris les outils d’aide à l’authentification requis lors de l’exécution de vos services dans Azure. Il est installé dans le répertoire du projet (à l’aide de npm `devDependencies` ).

- [Kit de développement logiciel .NET](/dotnet/core/install/)

    Le SDK .NET permet d’installer des liaisons personnalisées pour le débogage local et les déploiements d’applications Azure Functions. Si vous n’avez pas installé le SDK .NET 3.1 (ou version ultérieure) globalement, la version portable peut être installée.

- [ngrok](https://ngrok.com/download)

    Certaines fonctionnalités d’application Teams (bots de conversation, extensions de messagerie et webhooks entrants) nécessitent des connexions entrantes. Vous devez exposer votre système de développement à Teams via un tunnel. Un tunnel n’est pas requis pour les applications qui incluent uniquement des onglets. Ce package est installé dans le répertoire du projet (à l’aide de npm `devDependencies` ).

# <a name="visual-studio-2019"></a>[Visual Studio 2019](#tab/vs)

Vous pouvez utiliser Visual Studio 2019 pour développer des applications Teams avec Blazor Server dans .NET. Si vous n’avez pas l’intention de développer des applications Teams dans .NET, installez la version Visual Studio Code de Teams Shared Computer Toolkit.

Pour installer l’extension Shared Computer Toolkit Teams :

1. Ouvrez Visual Studio 2019.
1. Select **Extensions**  >  **Manage Extensions**.
1. Dans la zone de recherche, entrez **Teams Shared Computer Toolkit**.
1. Sélectionnez l’extension Shared Computer Toolkit teams, puis sélectionnez **Télécharger.**

L’extension peut être téléchargée. Fermez Visual Studio 2019 pour installer l’extension.

# <a name="command-line"></a>[Ligne de commande](#tab/cli)

Pour installer l’CLI TeamsFx, utilisez le `npm` gestionnaire de package :

``` bash
npm install -g @microsoft/teamsfx-cli
```

En fonction de votre configuration, vous devrez peut-être l’utiliser `sudo` pour installer l’CLI :

``` bash
sudo npm install -g --unsafe-perm @microsoft/teamsfx-cli
```

Cela est plus courant sur les systèmes Linux et macOS.

Veillez à ajouter le cache global npm à votre chemin d’accès. Cette procédure est normalement effectuée dans le cadre du programme d’installation Node.js'installation.  

Vous pouvez utiliser l’CLI avec la `teamsfx` commande. Vérifiez que la commande fonctionne en cours `teamsfx -h` d’exécution.

> [!CAUTION]
> Avant de pouvoir exécuter TeamsFx dans les terminals PowerShell, vous devez activer la stratégie d’exécution « signé à distance » pour PowerShell. Pour plus d’informations, reportez-vous à [la documentation PowerShell.](/powershell/module/microsoft.powershell.core/about/about_signing)

---

## <a name="install-optional-tools"></a>Installer les outils facultatifs

Installez les outils de navigateur pour le développement d’applications. Par exemple, si votre application est écrite avec React, vous pouvez utiliser les outils de développement React :

- [React Developer Tools for Chrome](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi)

Si vous souhaitez accéder aux données stockées dans Azure ou déployer un système back-end basé sur le cloud pour votre application Teams dans Azure, installez les outils ci-après :

- [Outils Azure pour Visual Studio code](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-node-azure-pack)
- [Azure CLI](/cli/azure/install-azure-cli)

Si vous travaillez avec des données Microsoft Graph, vous devez en savoir plus sur l’Explorateur Microsoft Graph et en faire un signet. Cet outil basé sur un navigateur vous permet d’interroger Microsoft Graph en dehors d’une application.

- [Afficheur Microsoft Graph](https://developer.microsoft.com/graph/graph-explorer)

Avec le portail du développeur pour Teams, vous pouvez configurer, gérer et distribuer votre application Teams, y compris à votre organisation ou au magasin Teams.

- [Documentation pour les développeurs](https://dev.teams.microsoft.com/)

## <a name="enable-sideloading"></a>Activer le chargement de version de version

Pendant le développement, vous devez charger votre application dans Teams sans la distribuer. C’est ce que l’on appelle le « chargement de version latérale ».

1. Si vous avez un compte Teams, vérifiez si vous pouvez télécharger une version de version de chargement d’applications dans Teams :

    1. Dans le client Teams, sélectionnez **Applications.**
    1. Recherchez une option pour **télécharger une application personnalisée.**

    :::image type="content" source="~/assets/images/teams-toolkit-v2/upload-custom-app-closeup.png" alt-text="Illustration montrant où dans Teams vous pouvez télécharger une application personnalisée.":::

> [!NOTE]
> Si vous ne pouvez toujours pas télécharger une version de version de chargement d’applications, parlez-en à votre administrateur Teams. Pour plus [d’informations, voir](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) activer les applications Teams personnalisées et activer le chargement d’applications personnalisées.

## <a name="get-a-free-teams-developer-tenant-optional"></a>Obtenir un client de développeur Teams gratuit (facultatif)

Si vous ne pouvez pas voir l’option de chargement indépendant ou si vous n’avez pas de compte Teams, vous pouvez obtenir un compte de développeur Teams gratuit en rejoignant le programme pour les développeurs M365.  Le processus d’inscription prend environ deux minutes.

1. Go to the [Microsoft 365 developer program](https://developer.microsoft.com/microsoft-365/dev-program).
1. Sélectionnez **Rejoindre maintenant** et suivez les instructions à l’écran.
1. Lorsque vous arrivez à l’écran d’accueil, **sélectionnez Configurer l’abonnement E5.**
1. Configurer votre compte d’administrateur. Une fois que vous avez terminé, vous devriez voir un écran comme celui-ci.

    :::image type="content" source="~/assets/images/build-your-first-app/dev-program-subscription.png" alt-text="Exemple de ce que vous voyez après vous être inscrire au programme pour les développeurs Microsoft 365.":::

1. Connectez-vous à Teams à l’aide du compte d’administrateur que vous viennent de configurer.
1. Vérifiez si vous avez désormais l’option **Télécharger une application personnalisée.**

## <a name="get-a-free-azure-account"></a>Obtenir un compte Azure gratuit

Si vous souhaitez héberger votre application ou accéder aux ressources dans Azure, vous devez avoir un abonnement Azure.  Vous pouvez [créer un compte gratuit avant](https://azure.microsoft.com/free/) de commencer.

## <a name="sign-in-to-your-microsoft-365-and-azure-accounts"></a>Connectez-vous à vos comptes Microsoft 365 et Azure

Vous devez avoir accès à deux comptes :

- Informations d’identification de votre compte Microsoft 365. Il s’agit du compte que vous utilisez pour vous inscrire à Teams. Si vous utilisez un client de programme pour les développeurs Microsoft 365, il s’agit du compte d’administrateur que vous avez créé lorsque vous vous êtes inscrit au programme.
- - Vos informations d’identification Azure. Il s’agit du compte que vous utilisez pour accéder au portail Azure et pour mettre en service de nouvelles ressources cloud pour prendre en charge votre application.

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Open Visual Studio Code
1. Sélectionnez l Teams icône dans la barre latérale :

    :::image type="content" source="~/assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Icône Teams dans la barre latérale Visual Studio Code.":::

1. Sélectionnez **Se connectez à M365.**

    :::image type="content" source="~/assets/images/teams-toolkit-v2/account-commands.png" alt-text="Emplacement de la section Comptes utilisée pour se connecter.":::

1. Le processus de connectez-vous commence à utiliser votre navigateur web normal. Terminez le processus de connectez-vous pour votre compte M365. Vous êtes invité à fermer le navigateur et à revenir à Visual Studio Code.
1. Revenir au Teams Shared Computer Toolkit dans Visual Studio Code.
1. Sélectionnez **Se connectez à Azure.**

    > [!TIP]
    > Si l’extension de compte Azure est installée et que vous utilisez le même compte, vous pouvez ignorer cette étape. Utilisez le même compte que celui que vous utilisez dans d’autres extensions.

1. Le processus de connectez-vous commence à utiliser votre navigateur web normal.  Terminez le processus de connectez-vous pour votre compte Azure. Vous êtes invité à fermer le navigateur et à revenir à Visual Studio Code.

Lorsque vous avez terminé, la section **ACCOUNTS** de la barre latérale affiche les deux comptes séparément, ainsi que le nombre d’abonnements Azure utilisables disponibles. Assurez-vous que vous disposez d’au moins un abonnement Azure utilisable. Si ce n’est pas le cas, connectez-vous et utilisez un autre compte.

# <a name="visual-studio-2019"></a>[Visual Studio 2019](#tab/vs)

Visual Studio 2019 vous invite à vous connecter à chaque service si nécessaire. Vous n’avez pas besoin de vous connectez à vos comptes M365 et Azure à l’avance.

# <a name="command-line"></a>[Ligne de commande](#tab/cli)

1. Connectez-vous Microsoft 365 l’CLI TeamsFx :

    ``` bash
    teamsfx account login m365
    ```

    Le processus de connectez-vous commence à utiliser votre navigateur web normal. Terminez le processus de connectez-vous pour votre compte M365. Lorsque vous pouvez fermer le navigateur, vous êtes invité à le faire.

2. Connectez-vous à Azure avec l’CLI TeamsFx :

    ``` bash
    teamsfx account login azure
    ```

    Le processus de connectez-vous commence à utiliser votre navigateur web normal. Terminez le processus de connectez-vous pour votre compte Azure. Lorsque vous pouvez fermer le navigateur, vous êtes invité à le faire.

Les connexions de compte sont partagées entre Visual Studio Code et l’CLI TeamsFx.

---

Maintenant que votre environnement de développement est configuré, vous pouvez créer, générer et déployer votre première application Teams de développement.

## <a name="see-also"></a>Voir aussi

- [Créer votre première application Teams avec Blazor](first-app-blazor.md)
- [Créer votre première application Teams l’aide SharePoint Framework (SPFx)](first-app-spfx.md)
- [Créer une application de bot de conversation](first-app-bot.md)
- [Créer une extension de messagerie](first-message-extension.md)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créer votre première application Teams l’aide React](first-app-react.md)
