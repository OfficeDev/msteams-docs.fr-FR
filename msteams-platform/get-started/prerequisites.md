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
# <a name="prerequisites-get-started-with-microsoft-teams-app-development"></a><span data-ttu-id="e22c5-103">Conditions préalables : prendre en Microsoft Teams développement d’applications</span><span class="sxs-lookup"><span data-stu-id="e22c5-103">Prerequisites: Get started with Microsoft Teams app development</span></span>

<span data-ttu-id="e22c5-104">Avant de créer votre première application Teams, vous devez installer quelques outils et configurer votre environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="e22c5-104">Before your create your first Teams app, you must install a few tools and set up your development environment.</span></span>

## <a name="install-required-tools"></a><span data-ttu-id="e22c5-105">Installer les outils requis</span><span class="sxs-lookup"><span data-stu-id="e22c5-105">Install required tools</span></span>

<span data-ttu-id="e22c5-106">Certains des outils dont vous avez besoin dépendent de la façon dont vous préférez créer votre Teams application :</span><span class="sxs-lookup"><span data-stu-id="e22c5-106">Some of the tools you need depend on how you you prefer to build your Teams app:</span></span>

- <span data-ttu-id="e22c5-107">[Node.js](https://nodejs.org/en/download/) (utilisez la dernière version de LTS v14)</span><span class="sxs-lookup"><span data-stu-id="e22c5-107">[Node.js](https://nodejs.org/en/download/) (use the latest v14 LTS release)</span></span> 
- <span data-ttu-id="e22c5-108">Un navigateur avec des outils de développement, tels [que Microsoft Edge](https://www.microsoft.com/edge) (recommandé) ou [Google Chrome](https://www.google.com/chrome/)</span><span class="sxs-lookup"><span data-stu-id="e22c5-108">A browser with developer tools - such as [Microsoft Edge](https://www.microsoft.com/edge) (recommended) or [Google Chrome](https://www.google.com/chrome/)</span></span>
- <span data-ttu-id="e22c5-109">Si vous développez avec JavaScript, TypeScript ou le SharePoint Framework (SPFx), installez [Visual Studio Code](https://code.visualstudio.com/download), version 1.55 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="e22c5-109">If you're developing with JavaScript, TypeScript, or the SharePoint Framework (SPFx), install [Visual Studio Code](https://code.visualstudio.com/download), version 1.55 or later.</span></span>  
- <span data-ttu-id="e22c5-110">Si vous développez avec .NET, installez [Visual Studio 2019.](https://visualstudio.com/download)</span><span class="sxs-lookup"><span data-stu-id="e22c5-110">If you're developing with .NET, install [Visual Studio 2019](https://visualstudio.com/download).</span></span>  <span data-ttu-id="e22c5-111">Veillez à installer la **charge ASP.NET développement web et** web ou la charge de travail de développement **.NET Core sur plusieurs plateformes.**</span><span class="sxs-lookup"><span data-stu-id="e22c5-111">Ensure you install the **ASP.NET and web development** or **.NET Core cross-platform development** workload.</span></span>

> [!WARNING]
> <span data-ttu-id="e22c5-112">Il existe des problèmes connus avec `npm@7` , empaqueté avec Node v15 et ultérieur.</span><span class="sxs-lookup"><span data-stu-id="e22c5-112">There are known issues with `npm@7`, packaged with Node v15 and later.</span></span> <span data-ttu-id="e22c5-113">Si vous avez des problèmes d’exécution, assurez-vous que vous utilisez `npm install` Node v14 (LTS)</span><span class="sxs-lookup"><span data-stu-id="e22c5-113">If you have problems running `npm install`, ensure you're using Node v14 (LTS)</span></span>

## <a name="install-the-teams-toolkit"></a><span data-ttu-id="e22c5-114">Installer le Teams Shared Computer Toolkit</span><span class="sxs-lookup"><span data-stu-id="e22c5-114">Install the Teams Toolkit</span></span>

<span data-ttu-id="e22c5-115">Le Teams Shared Computer Toolkit simplifie le processus de développement avec des outils pour mettre en service et déployer des ressources cloud pour votre application, publier dans le Teams store, etc.</span><span class="sxs-lookup"><span data-stu-id="e22c5-115">The Teams Toolkit helps simplify the development process with tools to provision and deploy cloud resources for your app, publish to the Teams store, and more.</span></span> <span data-ttu-id="e22c5-116">Vous pouvez utiliser le kit de ressources avec Visual Studio Code, Visual Studio ou en tant qu’CLI (appelé `teamsfx` ).</span><span class="sxs-lookup"><span data-stu-id="e22c5-116">You can use the toolkit with Visual Studio Code, Visual Studio, or as a CLI (called `teamsfx`).</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="e22c5-117">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="e22c5-117">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="e22c5-118">Ouvrez Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="e22c5-118">Open Visual Studio Code.</span></span>
1. <span data-ttu-id="e22c5-119">Sélectionnez l’affichage Extensions (**Ctrl+Shift+X**  /  **⌘⇧-X** ou Afficher **> extensions**).</span><span class="sxs-lookup"><span data-stu-id="e22c5-119">Select the Extensions view (**Ctrl+Shift+X** / **⌘⇧-X** or **View > Extensions**).</span></span>
1. <span data-ttu-id="e22c5-120">Dans la zone de recherche, entrez _Teams Shared Computer Toolkit_.</span><span class="sxs-lookup"><span data-stu-id="e22c5-120">In the search box, enter _Teams Toolkit_.</span></span>
1. <span data-ttu-id="e22c5-121">Sélectionnez le bouton d’installation vert en Teams Shared Computer Toolkit.</span><span class="sxs-lookup"><span data-stu-id="e22c5-121">Select on the green install button next to the Teams Toolkit.</span></span>

<span data-ttu-id="e22c5-122">Vous pouvez également trouver le Teams Shared Computer Toolkit sur le [Visual Studio Code Marketplace.](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)</span><span class="sxs-lookup"><span data-stu-id="e22c5-122">You also can find the Teams Toolkit on the [Visual Studio Code Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).</span></span>

<span data-ttu-id="e22c5-123">Les outils suivants sont installés par l’extension Visual Studio Code si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e22c5-123">The following tools will be installed by the Visual Studio Code extension when they are needed.</span></span>  <span data-ttu-id="e22c5-124">S’il est déjà installé, la version installée sera utilisée à la place.</span><span class="sxs-lookup"><span data-stu-id="e22c5-124">If already installed, the installed version will be used instead.</span></span>  <span data-ttu-id="e22c5-125">Si vous utilisez Linux (y compris WSL), vous devez installer ces outils avant d’utiliser :</span><span class="sxs-lookup"><span data-stu-id="e22c5-125">If using Linux (including WSL), you must install these tools before use:</span></span>

- [<span data-ttu-id="e22c5-126">Outils azure Functions Core</span><span class="sxs-lookup"><span data-stu-id="e22c5-126">Azure Functions Core Tools</span></span>](/azure/azure-functions/functions-run-local)

    <span data-ttu-id="e22c5-127">Azure Functions Core Tools permet d’exécuter localement tous les composants principaux lors d’une exécution de débogage locale, y compris les outils d’aide à l’authentification requis lors de l’exécution de vos services dans Azure.</span><span class="sxs-lookup"><span data-stu-id="e22c5-127">Azure Functions Core Tools is used to run any backend components locally during a local debug run, including the authentication helpers required when running your services in Azure.</span></span>  <span data-ttu-id="e22c5-128">Il est installé dans le répertoire du projet (à l’aide de npm `devDependencies` ).</span><span class="sxs-lookup"><span data-stu-id="e22c5-128">It is installed within the project directory (using the npm `devDependencies`).</span></span>

- [<span data-ttu-id="e22c5-129">Kit de développement logiciel .NET</span><span class="sxs-lookup"><span data-stu-id="e22c5-129">.NET SDK</span></span>](/dotnet/core/install/)

    <span data-ttu-id="e22c5-130">Le SDK .NET permet d’installer des liaisons personnalisées pour le débogage local et les déploiements d’applications Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="e22c5-130">The .NET SDK is used to install customized bindings for local debugging and Azure Functions app deployments.</span></span>  <span data-ttu-id="e22c5-131">Si vous n’avez pas installé le SDK .NET 3.1 (ou version ultérieure) globalement, la version portable sera installée.</span><span class="sxs-lookup"><span data-stu-id="e22c5-131">If you have not installed the .NET 3.1 (or later) SDK globally, the portable version will be installed.</span></span>

- [<span data-ttu-id="e22c5-132">ngrok</span><span class="sxs-lookup"><span data-stu-id="e22c5-132">ngrok</span></span>](https://ngrok.com/download)

    <span data-ttu-id="e22c5-133">Certaines Teams d’application (bots de conversation, extensions de messagerie et webhooks entrants) nécessitent des connexions entrantes.</span><span class="sxs-lookup"><span data-stu-id="e22c5-133">Some Teams app features (conversational bots, messaging extensions, and incoming webhooks) require inbound connections.</span></span>  <span data-ttu-id="e22c5-134">Vous devez exposer votre système de développement à la Teams via un tunnel.</span><span class="sxs-lookup"><span data-stu-id="e22c5-134">You need to expose your development system to Teams through a tunnel.</span></span>  <span data-ttu-id="e22c5-135">Un tunnel n’est pas requis pour les applications qui incluent uniquement des onglets.</span><span class="sxs-lookup"><span data-stu-id="e22c5-135">A tunnel is not required for apps that only include tabs.</span></span>  <span data-ttu-id="e22c5-136">Ce package est installé dans le répertoire du projet (à l’aide de npm `devDependencies` ).</span><span class="sxs-lookup"><span data-stu-id="e22c5-136">This package is installed within the project directory (using npm `devDependencies`).</span></span>

# <a name="visual-studio-2019"></a>[<span data-ttu-id="e22c5-137">Visual Studio 2019</span><span class="sxs-lookup"><span data-stu-id="e22c5-137">Visual Studio 2019</span></span>](#tab/vs)

<span data-ttu-id="e22c5-138">Vous pouvez utiliser Visual Studio 2019 pour développer des applications Teams avec Blazor Server dans .NET.</span><span class="sxs-lookup"><span data-stu-id="e22c5-138">You can use Visual Studio 2019 to develop Teams apps with Blazor Server in .NET.</span></span>  <span data-ttu-id="e22c5-139">Si vous n’avez pas l’intention de développer des applications Teams dans .NET, installez la version Visual Studio Code de Teams Shared Computer Toolkit.</span><span class="sxs-lookup"><span data-stu-id="e22c5-139">If you're not intending to develop Teams apps in .NET, install the Visual Studio Code version of Teams Toolkit.</span></span>

<span data-ttu-id="e22c5-140">Pour installer l’extension Teams Shared Computer Toolkit:</span><span class="sxs-lookup"><span data-stu-id="e22c5-140">To install the Teams Toolkit extension:</span></span>

1. <span data-ttu-id="e22c5-141">Ouvrez Visual Studio 2019.</span><span class="sxs-lookup"><span data-stu-id="e22c5-141">Open Visual Studio 2019.</span></span>
1. <span data-ttu-id="e22c5-142">Select **Extensions**  >  **Manage Extensions**.</span><span class="sxs-lookup"><span data-stu-id="e22c5-142">Select **Extensions** > **Manage Extensions**.</span></span>
1. <span data-ttu-id="e22c5-143">Dans la zone de recherche, entrez _Teams Shared Computer Toolkit_.</span><span class="sxs-lookup"><span data-stu-id="e22c5-143">In the search box, enter _Teams Toolkit_.</span></span>
1. <span data-ttu-id="e22c5-144">Sélectionnez l’extension Teams Shared Computer Toolkit et sélectionnez **Télécharger.**</span><span class="sxs-lookup"><span data-stu-id="e22c5-144">Select the Teams Toolkit extension and select **Download**.</span></span>

<span data-ttu-id="e22c5-145">L’extension sera téléchargée.</span><span class="sxs-lookup"><span data-stu-id="e22c5-145">The extension will be downloaded.</span></span>  <span data-ttu-id="e22c5-146">Fermez Visual Studio 2019 pour installer l’extension.</span><span class="sxs-lookup"><span data-stu-id="e22c5-146">Close Visual Studio 2019 to install the extension.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="e22c5-147">Ligne de commande</span><span class="sxs-lookup"><span data-stu-id="e22c5-147">Command line</span></span>](#tab/cli)

<span data-ttu-id="e22c5-148">Pour installer l’CLI TeamsFx, utilisez le `npm` gestionnaire de package :</span><span class="sxs-lookup"><span data-stu-id="e22c5-148">To install the TeamsFx CLI, use the `npm` package manager:</span></span>

``` bash
npm install -g @microsoft/teamsfx-cli
```

<span data-ttu-id="e22c5-149">En fonction de votre configuration, vous devrez peut-être l’utiliser `sudo` pour installer l’CLI :</span><span class="sxs-lookup"><span data-stu-id="e22c5-149">Depending on your configuration, you may need to use `sudo` to install the CLI:</span></span>

``` bash
sudo npm install -g --unsafe-perm @microsoft/teamsfx-cli
```

<span data-ttu-id="e22c5-150">Cela est plus courant sur les systèmes Linux et macOS.</span><span class="sxs-lookup"><span data-stu-id="e22c5-150">This is more common on Linux and macOS systems.</span></span>

<span data-ttu-id="e22c5-151">Veillez à ajouter le cache global npm à votre chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="e22c5-151">Ensure you add the npm global cache to your PATH.</span></span>  <span data-ttu-id="e22c5-152">Cette procédure est normalement effectuée dans le cadre du programme d’installation Node.js'installation.</span><span class="sxs-lookup"><span data-stu-id="e22c5-152">This is normally done as part of the Node.js installer.</span></span>  

<span data-ttu-id="e22c5-153">Vous pouvez utiliser l’CLI avec la `teamsfx` commande.</span><span class="sxs-lookup"><span data-stu-id="e22c5-153">You can use the CLI with the `teamsfx` command.</span></span>  <span data-ttu-id="e22c5-154">Vérifiez que la commande fonctionne en cours `teamsfx -h` d’exécution.</span><span class="sxs-lookup"><span data-stu-id="e22c5-154">Verify that the command is working by running `teamsfx -h`.</span></span>

> [!CAUTION]
> <span data-ttu-id="e22c5-155">Avant de pouvoir exécuter TeamsFx dans les terminaux PowerShell, vous devez activer la stratégie d’exécution « signé à distance » pour PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e22c5-155">Before you can run TeamsFx in PowerShell terminals, you need to enable the "remote signed" execution policy for PowerShell.</span></span>  <span data-ttu-id="e22c5-156">Pour plus d’informations, reportez-vous à [la documentation PowerShell.](/powershell/module/microsoft.powershell.core/about/about_signing)</span><span class="sxs-lookup"><span data-stu-id="e22c5-156">For more information, refer to the [PowerShell documentation](/powershell/module/microsoft.powershell.core/about/about_signing).</span></span>

---

## <a name="install-optional-tools"></a><span data-ttu-id="e22c5-157">Installer les outils facultatifs</span><span class="sxs-lookup"><span data-stu-id="e22c5-157">Install optional tools</span></span>

<span data-ttu-id="e22c5-158">Installez les outils de navigateur pour le développement d’applications.</span><span class="sxs-lookup"><span data-stu-id="e22c5-158">Install browser tools for app development.</span></span> <span data-ttu-id="e22c5-159">Par exemple, si votre application est écrite avec des React, vous pouvez utiliser React outils de développement :</span><span class="sxs-lookup"><span data-stu-id="e22c5-159">For instance, if your app is written with React, you can use React Developer Tools:</span></span>

- [<span data-ttu-id="e22c5-160">React Outils de développement pour Chrome</span><span class="sxs-lookup"><span data-stu-id="e22c5-160">React Developer Tools for Chrome</span></span>](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi)

<span data-ttu-id="e22c5-161">Si vous souhaitez accéder aux données stockées dans Azure ou déployer un système back-end basé sur le cloud pour votre application Teams azure, installez les outils ci-après :</span><span class="sxs-lookup"><span data-stu-id="e22c5-161">If you want to access data stored in Azure or deploy a cloud-based backend for your Teams app in Azure, install these tools:</span></span>

- [<span data-ttu-id="e22c5-162">Outils Azure pour Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="e22c5-162">Azure Tools for Visual Studio Code</span></span>](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-node-azure-pack)
- [<span data-ttu-id="e22c5-163">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e22c5-163">Azure CLI</span></span>](/cli/azure/install-azure-cli)

<span data-ttu-id="e22c5-164">Si vous travaillez avec des données Graph Microsoft, vous devez en savoir plus sur l’Explorateur microsoft et lui Graph signet.</span><span class="sxs-lookup"><span data-stu-id="e22c5-164">If you work with Microsoft Graph data, you should learn about and bookmark the Microsoft Graph Explorer.</span></span> <span data-ttu-id="e22c5-165">Cet outil basé sur un navigateur vous permet d’interroger Microsoft Graph en dehors d’une application.</span><span class="sxs-lookup"><span data-stu-id="e22c5-165">This browser-based tool allows you to query Microsoft Graph outside of an app.</span></span>

- [<span data-ttu-id="e22c5-166">Afficheur Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="e22c5-166">Microsoft Graph Explorer</span></span>](https://developer.microsoft.com/graph/graph-explorer)

<span data-ttu-id="e22c5-167">Avec le Portail des développeurs pour Teams, vous pouvez configurer, gérer et distribuer votre application Teams (y compris à votre organisation ou au Teams store).</span><span class="sxs-lookup"><span data-stu-id="e22c5-167">With the Developer Portal for Teams, you can configure, manage, and distribute your Teams app (including to your org or the Teams store).</span></span>

- [<span data-ttu-id="e22c5-168">Portail des développeurs pour Teams</span><span class="sxs-lookup"><span data-stu-id="e22c5-168">Developer Portal for Teams</span></span>](https://dev.teams.microsoft.com/)

## <a name="enable-sideloading"></a><span data-ttu-id="e22c5-169">Activer le chargement de version</span><span class="sxs-lookup"><span data-stu-id="e22c5-169">Enable sideloading</span></span>

<span data-ttu-id="e22c5-170">Pendant le développement, vous devrez charger votre application dans Teams sans la distribuer.</span><span class="sxs-lookup"><span data-stu-id="e22c5-170">During development, you will need to load your app within Teams without distributing it.</span></span>  <span data-ttu-id="e22c5-171">C’est ce que l’on appelle le « chargement de version latérale ».</span><span class="sxs-lookup"><span data-stu-id="e22c5-171">This is known as "sideloading".</span></span>

1. <span data-ttu-id="e22c5-172">Si vous avez un compte Teams, vérifiez si vous pouvez télécharger une version de version de chargement de version d’application dans Teams :</span><span class="sxs-lookup"><span data-stu-id="e22c5-172">If you have a Teams account, verify if you can sideload apps in Teams:</span></span>

    1. <span data-ttu-id="e22c5-173">Dans le Teams client, sélectionnez **Applications.**</span><span class="sxs-lookup"><span data-stu-id="e22c5-173">In the Teams client, select **Apps**.</span></span>
    1. <span data-ttu-id="e22c5-174">Recherchez une option pour **Télécharger une application personnalisée.**</span><span class="sxs-lookup"><span data-stu-id="e22c5-174">Look for an option to **Upload a custom app**.</span></span>

    :::image type="content" source="~/assets/images/teams-toolkit-v2/upload-custom-app-closeup.png" alt-text="Illustration montrant où dans Teams vous pouvez télécharger une application personnalisée.":::

> [!NOTE]
> <span data-ttu-id="e22c5-176">Si vous ne pouvez toujours pas télécharger une version de version de chargement d’applications, parlez-en à Teams administrateur.</span><span class="sxs-lookup"><span data-stu-id="e22c5-176">If you still can't sideload apps, talk to your Teams administrator.</span></span> <span data-ttu-id="e22c5-177">Pour [plus d’informations, voir](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) activer Teams applications personnalisées et activer le chargement d’applications personnalisées.</span><span class="sxs-lookup"><span data-stu-id="e22c5-177">See [enable custom Teams apps and turn on custom app uploading](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) for details.</span></span>

## <a name="get-a-free-teams-developer-tenant-optional"></a><span data-ttu-id="e22c5-178">Obtenir un client Teams développeur gratuit (facultatif)</span><span class="sxs-lookup"><span data-stu-id="e22c5-178">Get a free Teams developer tenant (optional)</span></span>

<span data-ttu-id="e22c5-179">Si vous ne pouvez pas voir l’option de chargement indépendant ou si vous n’avez pas de compte Teams, vous pouvez obtenir un compte de développeur Teams gratuit en rejoignant le programme pour les développeurs M365.</span><span class="sxs-lookup"><span data-stu-id="e22c5-179">If you cannot see the sideload option, or you don't have a Teams account, you can get a free Teams developer account by joining the M365 developer program.</span></span>  <span data-ttu-id="e22c5-180">Le processus d’inscription prend environ deux minutes.</span><span class="sxs-lookup"><span data-stu-id="e22c5-180">The registration process takes approximately two minutes.</span></span>

1. <span data-ttu-id="e22c5-181">Go to the [Microsoft 365 developer program](https://developer.microsoft.com/microsoft-365/dev-program).</span><span class="sxs-lookup"><span data-stu-id="e22c5-181">Go to the [Microsoft 365 developer program](https://developer.microsoft.com/microsoft-365/dev-program).</span></span>
1. <span data-ttu-id="e22c5-182">Sélectionnez **Rejoindre maintenant** et suivez les instructions à l’écran.</span><span class="sxs-lookup"><span data-stu-id="e22c5-182">Select **Join Now** and follow the onscreen instructions.</span></span>
1. <span data-ttu-id="e22c5-183">Lorsque vous arrivez à l’écran d’accueil, **sélectionnez Configurer l’abonnement E5.**</span><span class="sxs-lookup"><span data-stu-id="e22c5-183">When you get to the welcome screen, select **Set up E5 subscription**.</span></span>
1. <span data-ttu-id="e22c5-184">Configurer votre compte d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="e22c5-184">Set up your administrator account.</span></span> <span data-ttu-id="e22c5-185">Une fois que vous avez terminé, vous devriez voir un écran comme celui-ci.</span><span class="sxs-lookup"><span data-stu-id="e22c5-185">Once you finish, you should see a screen like this.</span></span>

    :::image type="content" source="~/assets/images/build-your-first-app/dev-program-subscription.png" alt-text="Exemple de ce que vous voyez après vous être inscrire au programme Microsoft 365 développeur.":::

1. <span data-ttu-id="e22c5-187">Connectez-vous Teams à l’aide du compte d’administrateur que vous viennent de configurer.</span><span class="sxs-lookup"><span data-stu-id="e22c5-187">Log in to Teams using the administrator account you just set up.</span></span>
1. <span data-ttu-id="e22c5-188">Vérifiez si vous avez maintenant la Télécharger une option **d’application** personnalisée.</span><span class="sxs-lookup"><span data-stu-id="e22c5-188">Verify if you now have the **Upload a custom app** option.</span></span>

## <a name="get-a-free-azure-account"></a><span data-ttu-id="e22c5-189">Obtenir un compte Azure gratuit</span><span class="sxs-lookup"><span data-stu-id="e22c5-189">Get a free Azure account</span></span>

<span data-ttu-id="e22c5-190">Si vous souhaitez héberger votre application ou accéder aux ressources dans Azure, vous aurez besoin d’un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="e22c5-190">If you wish to host your app or access resources within Azure, you will need an Azure subscription.</span></span>  <span data-ttu-id="e22c5-191">Vous pouvez [créer un compte gratuit avant](https://azure.microsoft.com/free/) de commencer.</span><span class="sxs-lookup"><span data-stu-id="e22c5-191">You can [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="sign-in-to-your-microsoft-365-and-azure-accounts"></a><span data-ttu-id="e22c5-192">Connectez-vous à vos comptes Microsoft 365 azure</span><span class="sxs-lookup"><span data-stu-id="e22c5-192">Sign in to your Microsoft 365 and Azure accounts</span></span>

<span data-ttu-id="e22c5-193">Vous aurez besoin d’accéder à deux comptes :</span><span class="sxs-lookup"><span data-stu-id="e22c5-193">You will need access to two accounts:</span></span>

- <span data-ttu-id="e22c5-194">Vos informations d Microsoft 365 compte de client.</span><span class="sxs-lookup"><span data-stu-id="e22c5-194">Your Microsoft 365 account credentials.</span></span> <span data-ttu-id="e22c5-195">Il s’agit du compte que vous utilisez pour vous Teams.</span><span class="sxs-lookup"><span data-stu-id="e22c5-195">This is the account that you use to sign in to Teams.</span></span> <span data-ttu-id="e22c5-196">Si vous utilisez un client de programme Microsoft 365 développeur, il s’agit du compte d’administrateur que vous avez créé lorsque vous vous êtes inscrit au programme.</span><span class="sxs-lookup"><span data-stu-id="e22c5-196">If you're using an Microsoft 365 developer program tenant, this is the admin account you set up when you registered for the program.</span></span>
- - <span data-ttu-id="e22c5-197">Vos informations d’identification Azure.</span><span class="sxs-lookup"><span data-stu-id="e22c5-197">Your Azure credentials.</span></span> <span data-ttu-id="e22c5-198">Il s’agit du compte que vous utilisez pour accéder au portail Azure et pour mettre en service de nouvelles ressources cloud pour prendre en charge votre application.</span><span class="sxs-lookup"><span data-stu-id="e22c5-198">This is the account that you use to access the Azure Portal and for provisioning new cloud resources to support your app.</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="e22c5-199">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="e22c5-199">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="e22c5-200">Ouvrir Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="e22c5-200">Open Visual Studio Code</span></span>
1. <span data-ttu-id="e22c5-201">Sélectionnez l Teams icône dans la barre latérale :</span><span class="sxs-lookup"><span data-stu-id="e22c5-201">Select the Teams icon in the sidebar:</span></span>

    :::image type="content" source="~/assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Icône Teams de l’Visual Studio Code côté gauche.":::

1. <span data-ttu-id="e22c5-203">Sélectionnez **Se connectez à M365.**</span><span class="sxs-lookup"><span data-stu-id="e22c5-203">Select **Sign in to M365**.</span></span>

    :::image type="content" source="~/assets/images/teams-toolkit-v2/account-commands.png" alt-text="Emplacement de la section Comptes utilisée pour se connecter.":::

1. <span data-ttu-id="e22c5-205">Le processus de connectez-vous commence à utiliser votre navigateur web normal.</span><span class="sxs-lookup"><span data-stu-id="e22c5-205">The sign-in process will start using your normal web browser.</span></span>  <span data-ttu-id="e22c5-206">Terminez le processus de connectez-vous pour votre compte M365.</span><span class="sxs-lookup"><span data-stu-id="e22c5-206">Complete the sign-in process for your M365 account.</span></span>  <span data-ttu-id="e22c5-207">Vous serez invité à fermer le navigateur et à revenir à Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="e22c5-207">You will be prompted when you can close the browser and return to Visual Studio Code.</span></span>
1. <span data-ttu-id="e22c5-208">Revenir au Teams Shared Computer Toolkit dans Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="e22c5-208">Return to the Teams Toolkit within Visual Studio Code.</span></span>
1. <span data-ttu-id="e22c5-209">Sélectionnez **Se connectez à Azure.**</span><span class="sxs-lookup"><span data-stu-id="e22c5-209">Select **Sign in to Azure**.</span></span>

    > [!TIP]
    > <span data-ttu-id="e22c5-210">Si l’extension de compte Azure est installée et que vous utilisez le même compte, vous pouvez ignorer cette étape.</span><span class="sxs-lookup"><span data-stu-id="e22c5-210">If you have the Azure Account extension installed and are using the same account, you can skip this step.</span></span>  <span data-ttu-id="e22c5-211">Vous utiliserez automatiquement le même compte que dans d’autres extensions.</span><span class="sxs-lookup"><span data-stu-id="e22c5-211">You will automatically use the same account as you are using in other extensions.</span></span>

1. <span data-ttu-id="e22c5-212">Le processus de connectez-vous commence à utiliser votre navigateur web normal.</span><span class="sxs-lookup"><span data-stu-id="e22c5-212">The sign-in process will start using your normal web browser.</span></span>  <span data-ttu-id="e22c5-213">Terminez le processus de connectez-vous pour votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="e22c5-213">Complete the sign-in process for your Azure account.</span></span>  <span data-ttu-id="e22c5-214">Vous serez invité à fermer le navigateur et à revenir à Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="e22c5-214">You will be prompted when you can close the browser and return to Visual Studio Code.</span></span>

<span data-ttu-id="e22c5-215">Lorsque vous avez terminé, la section **ACCOUNTS** de la barre latérale affiche les deux comptes séparément, ainsi que le nombre d’abonnements Azure utilisables disponibles.</span><span class="sxs-lookup"><span data-stu-id="e22c5-215">When complete, the **ACCOUNTS** section of the sidebar will show the two accounts separately, together with the number of usable Azure subscriptions available to you.</span></span>  <span data-ttu-id="e22c5-216">Assurez-vous que vous disposez d’au moins un abonnement Azure utilisable.</span><span class="sxs-lookup"><span data-stu-id="e22c5-216">Ensure you have at least one usable Azure subscription available.</span></span>  <span data-ttu-id="e22c5-217">Si ce n’est pas le cas, connectez-vous et utilisez un autre compte.</span><span class="sxs-lookup"><span data-stu-id="e22c5-217">If not, sign out and use a different account.</span></span>

# <a name="visual-studio-2019"></a>[<span data-ttu-id="e22c5-218">Visual Studio 2019</span><span class="sxs-lookup"><span data-stu-id="e22c5-218">Visual Studio 2019</span></span>](#tab/vs)

<span data-ttu-id="e22c5-219">Visual Studio 2019 vous invite à vous connecter à chaque service au besoin.</span><span class="sxs-lookup"><span data-stu-id="e22c5-219">Visual Studio 2019 will prompt you to log in to each service as it is needed.</span></span>  <span data-ttu-id="e22c5-220">Vous n’avez pas besoin de vous connectez à vos comptes M365 et Azure à l’avance.</span><span class="sxs-lookup"><span data-stu-id="e22c5-220">You do not need to sign in to your M365 and Azure accounts in advance.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="e22c5-221">Ligne de commande</span><span class="sxs-lookup"><span data-stu-id="e22c5-221">Command line</span></span>](#tab/cli)

1. <span data-ttu-id="e22c5-222">Connectez-vous Microsoft 365 l’CLI TeamsFx :</span><span class="sxs-lookup"><span data-stu-id="e22c5-222">Sign in to Microsoft 365 with the TeamsFx CLI:</span></span>

    ``` bash
    teamsfx account login m365
    ```

    <span data-ttu-id="e22c5-223">Le processus de connectez-vous commence à utiliser votre navigateur web normal.</span><span class="sxs-lookup"><span data-stu-id="e22c5-223">The sign-in process will start using your normal web browser.</span></span>  <span data-ttu-id="e22c5-224">Terminez le processus de connectez-vous pour votre compte M365.</span><span class="sxs-lookup"><span data-stu-id="e22c5-224">Complete the sign-in process for your M365 account.</span></span>  <span data-ttu-id="e22c5-225">Lorsque vous pourrez fermer le navigateur, vous serez invité à le faire.</span><span class="sxs-lookup"><span data-stu-id="e22c5-225">You will be prompted when you can close the browser.</span></span>

2. <span data-ttu-id="e22c5-226">Connectez-vous à Azure avec l’CLI TeamsFx :</span><span class="sxs-lookup"><span data-stu-id="e22c5-226">Sign in to Azure with the TeamsFx CLI:</span></span>

    ``` bash
    teamsfx account login azure
    ```

    <span data-ttu-id="e22c5-227">Le processus de connectez-vous commence à utiliser votre navigateur web normal.</span><span class="sxs-lookup"><span data-stu-id="e22c5-227">The sign-in process will start using your normal web browser.</span></span>  <span data-ttu-id="e22c5-228">Terminez le processus de connectez-vous pour votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="e22c5-228">Complete the sign-in process for your Azure account.</span></span>  <span data-ttu-id="e22c5-229">Lorsque vous pourrez fermer le navigateur, vous serez invité à le faire.</span><span class="sxs-lookup"><span data-stu-id="e22c5-229">You will be prompted when you can close the browser.</span></span>

<span data-ttu-id="e22c5-230">Les connexions de compte sont partagées entre Visual Studio Code et l’CLI TeamsFx.</span><span class="sxs-lookup"><span data-stu-id="e22c5-230">The account logins are shared between Visual Studio Code and the TeamsFx CLI.</span></span>

---

## <a name="next-steps"></a><span data-ttu-id="e22c5-231">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e22c5-231">Next steps</span></span>

<span data-ttu-id="e22c5-232">Maintenant que votre environnement de développement est configuré, vous pouvez créer, générer et déployer votre première application Teams de développement.</span><span class="sxs-lookup"><span data-stu-id="e22c5-232">Now that your development environment is configured, you can create, build, and deploy your first Teams app.</span></span>

- [<span data-ttu-id="e22c5-233">Créer votre première application Teams l’aide React</span><span class="sxs-lookup"><span data-stu-id="e22c5-233">Create your first Teams app using React</span></span>](first-app-react.md)
- [<span data-ttu-id="e22c5-234">Créer votre première application Teams avec Blazor</span><span class="sxs-lookup"><span data-stu-id="e22c5-234">Create your first Teams app with Blazor</span></span>](first-app-blazor.md)
- [<span data-ttu-id="e22c5-235">Créer votre première application Teams l’aide SharePoint Framework (SPFx)</span><span class="sxs-lookup"><span data-stu-id="e22c5-235">Create your first Teams app using SharePoint Framework (SPFx)</span></span>](first-app-spfx.md)
- [<span data-ttu-id="e22c5-236">Créer une application de bot de conversation</span><span class="sxs-lookup"><span data-stu-id="e22c5-236">Create a conversational bot app</span></span>](first-app-bot.md)
- [<span data-ttu-id="e22c5-237">Créer une extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="e22c5-237">Create a messaging extension</span></span>](first-message-extension.md)
