---
title: Mise en place - Conditions préalables
author: adrianhall
description: Découvrez comment prendre en Microsoft Teams développement d’applications et configurer votre environnement.
ms.author: adhal
ms.date: 05/24/2021
ms.topic: quickstart
ms.openlocfilehash: 73d99f2bbbc69bf13242110a56e13e662655283c
ms.sourcegitcommit: 9cabeaed9baf96c8caeb1497f0bc37abdb787d22
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/25/2021
ms.locfileid: "52646671"
---
# <a name="prerequisites-get-started-with-microsoft-teams-app-development"></a>Conditions préalables : prendre en Microsoft Teams développement d’applications

Avant de créer votre première application Teams, vous devez installer quelques outils et configurer votre environnement de développement.

## <a name="install-required-tools"></a>Installer les outils requis

Certains des outils dont vous avez besoin dépendent de la façon dont vous préférez créer votre Teams application :

- [Node.js](https://nodejs.org/en/download/) (utilisez la dernière version de LTS v14) 
- Navigateur avec outils de développement, tels que [Microsoft Edge](https://www.microsoft.com/edge) (recommandé) ou [Google Chrome](https://www.google.com/chrome/)
- Si vous développez avec JavaScript, TypeScript ou le SharePoint Framework (SPFx), installez [Visual Studio Code](https://code.visualstudio.com/download), version 1.55 ou ultérieure.  
- Si vous développez avec .NET, installez [Visual Studio 2019.](https://visualstudio.com/download)  Veillez à installer la **charge ASP.NET développement web et** web ou la charge de travail de développement **.NET Core sur plusieurs plateformes.**

> [!WARNING]
> Il existe des problèmes connus avec `npm@7` , empaqueté avec Node v15 et ultérieur. Si vous avez des problèmes d’exécution, assurez-vous que vous utilisez `npm install` Node v14 (LTS)

## <a name="install-the-teams-toolkit"></a>Installer le Teams Shared Computer Toolkit

Le Teams Shared Computer Toolkit simplifie le processus de développement avec des outils pour mettre en service et déployer des ressources cloud pour votre application, publier dans le Teams store, etc. Vous pouvez utiliser le kit de ressources avec Visual Studio Code, Visual Studio ou en tant qu’CLI (appelé `teamsfx` ).

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Ouvrez Visual Studio Code.
1. Sélectionnez l’affichage Extensions (**Ctrl+Shift+X**  /  **⌘⇧-X** ou **Afficher > extensions**).
1. Dans la zone de recherche, entrez _Teams Shared Computer Toolkit_.
1. Sélectionnez le bouton d’installation vert en Teams Shared Computer Toolkit.

Vous pouvez également trouver le Teams Shared Computer Toolkit sur le [Visual Studio Code Marketplace.](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)

Les outils suivants sont installés par l’extension Visual Studio Code si nécessaire.  S’il est déjà installé, la version installée sera utilisée à la place.  Si vous utilisez Linux (y compris WSL), vous devez installer ces outils avant d’utiliser :

- [Outils azure Functions Core](/azure/azure-functions/functions-run-local)

    Azure Functions Core Tools permet d’exécuter localement tous les composants principaux lors d’une exécution de débogage locale, y compris les outils d’aide à l’authentification requis lors de l’exécution de vos services dans Azure.  Il est installé dans le répertoire du projet (à l’aide de npm `devDependencies` ).

- [Kit de développement logiciel .NET](/dotnet/core/install/)

    Le SDK .NET permet d’installer des liaisons personnalisées pour le débogage local et les déploiements d’applications Azure Functions.  Si vous n’avez pas installé le SDK .NET 3.1 (ou version ultérieure) globalement, la version portable sera installée.

- [ngrok](https://ngrok.com/download)

    Certaines Teams d’application (bots de conversation, extensions de messagerie et webhooks entrants) nécessitent des connexions entrantes.  Vous devez exposer votre système de développement à la Teams via un tunnel.  Un tunnel n’est pas requis pour les applications qui incluent uniquement des onglets.  Ce package est installé dans le répertoire du projet (à l’aide de npm `devDependencies` ).

# <a name="visual-studio-2019"></a>[Visual Studio 2019](#tab/vs)

Vous pouvez utiliser Visual Studio 2019 pour développer des applications Teams avec Blazor Server dans .NET.  Si vous n’avez pas l’intention de développer des applications Teams dans .NET, installez la version Visual Studio Code de Teams Shared Computer Toolkit.

Pour installer l’extension Teams Shared Computer Toolkit :

1. Ouvrez Visual Studio 2019.
1. Select **Extensions**  >  **Manage Extensions**.
1. Dans la zone de recherche, entrez _Teams Shared Computer Toolkit_.
1. Sélectionnez l’extension Teams Shared Computer Toolkit et sélectionnez **Télécharger.**

L’extension sera téléchargée.  Fermez Visual Studio 2019 pour installer l’extension.

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

Veillez à ajouter le cache global npm à votre chemin d’accès.  Cette procédure est normalement effectuée dans le cadre du programme d’installation Node.js'installation.  

Vous pouvez utiliser l’CLI avec la `teamsfx` commande.  Vérifiez que la commande fonctionne en cours `teamsfx -h` d’exécution.

> [!CAUTION]
> Avant de pouvoir exécuter TeamsFx dans les terminals PowerShell, vous devez activer la stratégie d’exécution « signé à distance » pour PowerShell.  Pour plus d’informations, reportez-vous à [la documentation PowerShell.](/powershell/module/microsoft.powershell.core/about/about_signing)

---

## <a name="install-optional-tools"></a>Installer les outils facultatifs

Installez les outils de navigateur pour le développement d’applications. Par exemple, si votre application est écrite avec des React, vous pouvez utiliser React outils de développement :

- [React Outils de développement pour Chrome](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi)

Si vous souhaitez accéder aux données stockées dans Azure ou déployer un système back-end basé sur le cloud pour votre application Teams azure, installez les outils ci-après :

- [Outils Azure pour Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-node-azure-pack)
- [Azure CLI](/cli/azure/install-azure-cli)

Si vous travaillez avec des données Graph Microsoft, vous devez en savoir plus sur l’Explorateur microsoft et lui Graph signet. Cet outil basé sur un navigateur vous permet d’interroger Microsoft Graph en dehors d’une application.

- [Afficheur Microsoft Graph](https://developer.microsoft.com/graph/graph-explorer)

Avec le Portail des développeurs pour Teams, vous pouvez configurer, gérer et distribuer votre application Teams (y compris à votre organisation ou au Teams store).

- [Documentation pour les développeurs](https://dev.teams.microsoft.com/)

## <a name="enable-sideloading"></a>Activer le chargement de version de version

Pendant le développement, vous devrez charger votre application dans Teams sans la distribuer.  C’est ce que l’on appelle le « chargement de version latérale ».

1. Si vous avez un compte Teams, vérifiez si vous pouvez télécharger une version de version de chargement de version d’application dans Teams :

    1. Dans le Teams client, sélectionnez **Applications.**
    1. Recherchez une option pour **Télécharger une application personnalisée.**

    :::image type="content" source="~/assets/images/teams-toolkit-v2/upload-custom-app-closeup.png" alt-text="Illustration montrant où dans Teams vous pouvez télécharger une application personnalisée.":::

> [!NOTE]
> Si vous ne pouvez toujours pas télécharger une version de version de chargement d’applications, parlez-en à Teams administrateur. Pour [plus d’informations, voir](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) activer Teams applications personnalisées et activer le chargement d’applications personnalisées.

## <a name="get-a-free-teams-developer-tenant-optional"></a>Obtenir un client Teams développeur gratuit (facultatif)

Si vous ne pouvez pas voir l’option chargement indépendant ou si vous n’avez pas de compte Teams, vous pouvez obtenir un compte de développeur Teams gratuit en rejoignant le programme pour les développeurs M365.  Le processus d’inscription prend environ deux minutes.

1. Go to the [Microsoft 365 developer program](https://developer.microsoft.com/microsoft-365/dev-program).
1. Sélectionnez **Rejoindre maintenant** et suivez les instructions à l’écran.
1. Lorsque vous arrivez à l’écran d’accueil, **sélectionnez Configurer l’abonnement E5.**
1. Configurer votre compte d’administrateur. Une fois que vous avez terminé, vous devriez voir un écran comme celui-ci.

    :::image type="content" source="~/assets/images/build-your-first-app/dev-program-subscription.png" alt-text="Exemple de ce que vous voyez après vous être inscrire au programme Microsoft 365 développeur.":::

1. Connectez-vous Teams à l’aide du compte d’administrateur que vous viennent de configurer.
1. Vérifiez si vous avez maintenant la Télécharger une option **d’application** personnalisée.

## <a name="get-a-free-azure-account"></a>Obtenir un compte Azure gratuit

Si vous souhaitez héberger votre application ou accéder aux ressources dans Azure, vous aurez besoin d’un abonnement Azure.  Vous pouvez [créer un compte gratuit avant](https://azure.microsoft.com/free/) de commencer.

## <a name="sign-in-to-your-microsoft-365-and-azure-accounts"></a>Connectez-vous à vos comptes Microsoft 365 azure

Vous aurez besoin d’accéder à deux comptes :

- Vos informations d Microsoft 365 compte de client. Il s’agit du compte que vous utilisez pour vous Teams. Si vous utilisez un client de programme Microsoft 365 développeur, il s’agit du compte d’administrateur que vous avez créé lorsque vous vous êtes inscrit au programme.
- - Vos informations d’identification Azure. Il s’agit du compte que vous utilisez pour accéder au portail Azure et pour mettre en service de nouvelles ressources cloud pour prendre en charge votre application.

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Ouvrez Visual Studio Code
1. Sélectionnez l Teams icône dans la barre latérale :

    :::image type="content" source="~/assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Icône Teams dans la barre latérale Visual Studio Code.":::

1. Sélectionnez **Se connectez à M365.**

    :::image type="content" source="~/assets/images/teams-toolkit-v2/account-commands.png" alt-text="Emplacement de la section Comptes utilisée pour se connecter.":::

1. Le processus de connectez-vous commence à utiliser votre navigateur web normal.  Terminez le processus de connectez-vous pour votre compte M365.  Vous serez invité à fermer le navigateur et à revenir à Visual Studio Code.
1. Revenir au Teams Shared Computer Toolkit dans Visual Studio Code.
1. Sélectionnez **Se connectez à Azure.**

    > [!TIP]
    > Si l’extension de compte Azure est installée et que vous utilisez le même compte, vous pouvez ignorer cette étape.  Vous utiliserez automatiquement le même compte que dans d’autres extensions.

1. Le processus de connectez-vous commence à utiliser votre navigateur web normal.  Terminez le processus de connectez-vous pour votre compte Azure.  Vous serez invité à fermer le navigateur et à revenir à Visual Studio Code.

Lorsque vous avez terminé, la section **ACCOUNTS** de la barre latérale affiche les deux comptes séparément, ainsi que le nombre d’abonnements Azure utilisables disponibles.  Assurez-vous que vous disposez d’au moins un abonnement Azure utilisable.  Si ce n’est pas le cas, connectez-vous et utilisez un autre compte.

# <a name="visual-studio-2019"></a>[Visual Studio 2019](#tab/vs)

Visual Studio 2019 vous invite à vous connecter à chaque service au besoin.  Vous n’avez pas besoin de vous connectez à vos comptes M365 et Azure à l’avance.

# <a name="command-line"></a>[Ligne de commande](#tab/cli)

1. Connectez-vous Microsoft 365 l’CLI TeamsFx :

    ``` bash
    teamsfx account login m365
    ```

    Le processus de connectez-vous commence à utiliser votre navigateur web normal.  Terminez le processus de connectez-vous pour votre compte M365.  Lorsque vous pourrez fermer le navigateur, vous serez invité à le faire.

2. Connectez-vous à Azure avec l’CLI TeamsFx :

    ``` bash
    teamsfx account login azure
    ```

    Le processus de connectez-vous commence à utiliser votre navigateur web normal.  Terminez le processus de connectez-vous pour votre compte Azure.  Lorsque vous pourrez fermer le navigateur, vous serez invité à le faire.

Les connexions de compte sont partagées entre Visual Studio Code et l’CLI TeamsFx.

---

## <a name="next-steps"></a>Prochaines étapes

Maintenant que votre environnement de développement est configuré, vous pouvez créer, générer et déployer votre première application Teams de développement.

- [Créer votre première application Teams l’aide React](first-app-react.md)
- [Créer votre première application Teams avec Blazor](first-app-blazor.md)
- [Créer votre première application Teams l’aide SharePoint Framework (SPFx)](first-app-spfx.md)
- [Créer une application de bot de conversation](first-app-bot.md)
- [Créer une extension de messagerie](first-message-extension.md)
