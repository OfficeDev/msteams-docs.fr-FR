---
title: Get started - Build a channel and group tab
author: girliemac
description: Créez rapidement un onglet Microsoft Teams canal et de groupe à l’aide du Microsoft Teams Shared Computer Toolkit.
ms.author: timura
ms.date: 03/22/2020
ms.topic: tutorial
ms.openlocfilehash: ff9cfbfb7d099db52966f119add4ce8729929aa1
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566067"
---
# <a name="build-your-first-channel-and-group-tab-for-microsoft-teams"></a><span data-ttu-id="ceb95-103">Créez votre premier onglet de canal et de groupe pour Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="ceb95-103">Build your first channel and group tab for Microsoft Teams</span></span>

<span data-ttu-id="ceb95-104">Ce didacticiel vous  apprend à créer un onglet de canal de base également appelé onglet de *groupe,* qui est une page en plein écran pour un canal d’équipe ou une conversation.</span><span class="sxs-lookup"><span data-stu-id="ceb95-104">This tutorial teaches you to build a basic *channel tab* also known as a *group tab*, which is a full-screen page for a team channel or chat.</span></span> <span data-ttu-id="ceb95-105">Vous pouvez également configurer certains aspects de ce type d’onglet, par exemple renommer l’onglet afin qu’il soit significatif pour son canal, ce que vous ne pouvez pas faire dans un onglet personnel.</span><span class="sxs-lookup"><span data-stu-id="ceb95-105">You can also configure some aspects of this kind of tab, for example, rename the tab so it's meaningful to their channel, which you cannot do in a Personal Tab.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="ceb95-106">Ce que vous allez apprendre</span><span class="sxs-lookup"><span data-stu-id="ceb95-106">What you'll learn</span></span>

* <span data-ttu-id="ceb95-107">Créez un projet d’application à l’aide Microsoft Teams Shared Computer Toolkit pour Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="ceb95-107">Create an app project using the Microsoft Teams Toolkit for Visual Studio Code.</span></span>
* <span data-ttu-id="ceb95-108">Comprendre les configurations d’application et la échafaudage pertinentes pour les onglets de canal.</span><span class="sxs-lookup"><span data-stu-id="ceb95-108">Understand the app configurations and scaffolding relevant to channel tabs.</span></span>
* <span data-ttu-id="ceb95-109">Créez le contenu de l’onglet et la configuration de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="ceb95-109">Create tab content and tab configuration.</span></span>
* <span data-ttu-id="ceb95-110">Créez et exécutez votre application dans teams pour les tests.</span><span class="sxs-lookup"><span data-stu-id="ceb95-110">Build and run your app in teams for testing.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ceb95-111">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="ceb95-111">Prerequisites</span></span>

<span data-ttu-id="ceb95-112">Assurez-vous que vous comprenez comment configurer et créer une application Teams simple.</span><span class="sxs-lookup"><span data-stu-id="ceb95-112">Make sure that you understand how to set up and build a simple Teams app.</span></span> <span data-ttu-id="ceb95-113">Pour plus d’informations, [voir créer votre première Microsoft Teams application « Hello World!](../build-your-first-app/build-and-run.md)».</span><span class="sxs-lookup"><span data-stu-id="ceb95-113">For more information, see [create your first Microsoft Teams "Hello, World!" app](../build-your-first-app/build-and-run.md).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="ceb95-114">1. Créer votre projet d’application</span><span class="sxs-lookup"><span data-stu-id="ceb95-114">1. Create your app project</span></span>

<span data-ttu-id="ceb95-115">Le Microsoft Teams Shared Computer Toolkit vous permet de configurer votre application et la configuration de la échafaudage pertinente pour les onglets de canal et de groupe.</span><span class="sxs-lookup"><span data-stu-id="ceb95-115">The Microsoft Teams Toolkit helps you to configure your app and set up the scaffolding relevant to channel and group tabs.</span></span> <span data-ttu-id="ceb95-116">Il contient également une page de configuration de base et une page de contenu qui affiche un « Hello, World! »</span><span class="sxs-lookup"><span data-stu-id="ceb95-116">It also contains a basic configuration page and content page that displays a "Hello, World!"</span></span> <span data-ttu-id="ceb95-117">Message.</span><span class="sxs-lookup"><span data-stu-id="ceb95-117">message.</span></span>

<span data-ttu-id="ceb95-118">**Pour créer votre projet d’application**</span><span class="sxs-lookup"><span data-stu-id="ceb95-118">**To create your app project**</span></span>

1. Go to Visual Studio Code and select **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: on the left Activity Bar.
1. <span data-ttu-id="ceb95-120">Connectez-vous avec votre Microsoft 365 de développement lorsque vous y être invité.</span><span class="sxs-lookup"><span data-stu-id="ceb95-120">Sign in with your Microsoft 365 development account when prompted to do so.</span></span>
1. <span data-ttu-id="ceb95-121">Dans **l’écran Sélectionner un** projet, **sélectionnez JS** (JavaScript) sous **Canal et application de groupe.**</span><span class="sxs-lookup"><span data-stu-id="ceb95-121">On the **Select project** screen, select **JS** (JavaScript) under **Channel and group app**.</span></span>
1. <span data-ttu-id="ceb95-122">Entrez un nom pour votre application Teams de messagerie.</span><span class="sxs-lookup"><span data-stu-id="ceb95-122">Enter a name for your Teams app.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="ceb95-123">Il s’agit du nom par défaut de votre application, ainsi que du nom du répertoire de projet d’application sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="ceb95-123">This is the default name for your app and also the name of the app project directory on your local machine.</span></span>

1. <span data-ttu-id="ceb95-124">Sélectionnez **l’onglet Teams canal.**</span><span class="sxs-lookup"><span data-stu-id="ceb95-124">Select **Group or Teams channel tab**.</span></span>
1. <span data-ttu-id="ceb95-125">Sélectionnez **Terminer** en bas de l’écran pour configurer votre projet et enregistrez-le sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="ceb95-125">Select **Finish** at the bottom of the screen to configure your project and save your project on your local machine.</span></span>  

## <a name="2-understand-your-app-project-components"></a><span data-ttu-id="ceb95-126">2. Comprendre les composants de votre projet d’application</span><span class="sxs-lookup"><span data-stu-id="ceb95-126">2. Understand your app project components</span></span>

<span data-ttu-id="ceb95-127">La plupart des configurations d’application et de la création de la échafaudage sont automatiquement définies lorsque vous créez votre projet avec le kit de ressources.</span><span class="sxs-lookup"><span data-stu-id="ceb95-127">Much of the app configurations and scaffolding are set up automatically when you create your project with the toolkit.</span></span> <span data-ttu-id="ceb95-128">Examinons les principaux composants de la création d’un onglet de canal.</span><span class="sxs-lookup"><span data-stu-id="ceb95-128">Let's look at the main components for building a channel tab.</span></span>

* <span data-ttu-id="ceb95-129">**Configurations d’application**: **ouvrez App Studio** dans le kit de ressources pour afficher et mettre à jour les configurations de votre application.</span><span class="sxs-lookup"><span data-stu-id="ceb95-129">**App configurations**: Open **App Studio** in the toolkit to view and update your app configurations.</span></span>
* <span data-ttu-id="ceb95-130">**Échafaudage d’application**: la échafaudage de l’application fournit les composants nécessaires au rendu de l’onglet de votre canal Teams.</span><span class="sxs-lookup"><span data-stu-id="ceb95-130">**App scaffolding**: The app scaffolding provides the components needed for rendering your channel tab in Teams.</span></span> <span data-ttu-id="ceb95-131">Toutefois, pour l’instant, nous allons nous concentrer sur les questions suivantes :</span><span class="sxs-lookup"><span data-stu-id="ceb95-131">There's a lot you can work with, however, for now let's focus on the following:</span></span>
  * <span data-ttu-id="ceb95-132">Fichiers situés dans le `src/components` répertoire de votre projet :</span><span class="sxs-lookup"><span data-stu-id="ceb95-132">The files located in the `src/components` directory of your project:</span></span>
    * <span data-ttu-id="ceb95-133">`Tab.js` pour le rendu de la page de contenu de votre onglet.</span><span class="sxs-lookup"><span data-stu-id="ceb95-133">`Tab.js` for rendering your tab's content page.</span></span>
    * <span data-ttu-id="ceb95-134">`TabConfig.js` pour le rendu de la page de configuration de votre onglet.</span><span class="sxs-lookup"><span data-stu-id="ceb95-134">`TabConfig.js` for rendering your tab's configuration page.</span></span>
  * <span data-ttu-id="ceb95-135">Microsoft Teams SDK client JavaScript, qui est pré-chargé dans les composants frontaux de votre projet.</span><span class="sxs-lookup"><span data-stu-id="ceb95-135">Microsoft Teams JavaScript client SDK, which comes pre-loaded in your project's front-end components.</span></span>

## <a name="3-customize-your-tab-content-page"></a><span data-ttu-id="ceb95-136">3. Personnaliser la page de contenu de votre onglet</span><span class="sxs-lookup"><span data-stu-id="ceb95-136">3. Customize your tab content page</span></span>

1. <span data-ttu-id="ceb95-137">Copiez et modifiez l’exemple de code suivant avec des informations pertinentes pour votre organisation.</span><span class="sxs-lookup"><span data-stu-id="ceb95-137">Copy and modify the following code sample with information that's relevant to your organization.</span></span> <span data-ttu-id="ceb95-138">Vous pouvez également utiliser l’extrait de code tel qu’il est :</span><span class="sxs-lookup"><span data-stu-id="ceb95-138">You can also use the snippet as it is:</span></span>
    ```JSX
    <div>
      <h1>Important Contacts</h1>
        <ul>
          <li>Help Desk: <a href="mailto:support@company.com">support@company.com</a></li>
          <li>Human Resources: <a href="mailto:hr@company.com">hr@company.com</a></li>
          <li>Facilities: <a href="mailto:facilities@company.com">facilities@company.com</a></li>
        </ul>
    </div>
    ```
    
1. <span data-ttu-id="ceb95-139">Go to the `src/components` directory and open the `Tab.js` file.</span><span class="sxs-lookup"><span data-stu-id="ceb95-139">Go to the `src/components` directory and open the `Tab.js` file.</span></span> <span data-ttu-id="ceb95-140">Recherchez `render()` la fonction et collez votre code à l’intérieur, comme illustré dans `return()` l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="ceb95-140">Locate the `render()` function and paste your code inside `return()` as shown in the following example:</span></span>
    ```JavaScript
    render() {

        let userName = Object.keys(this.state.context).length > 0 ? this.state.context['upn'] : "";

        return (
        <div>
          <h1>Important Contacts</h1>
            <ul>
              <li>Help Desk: <a href="mailto:support@company.com">support@company.com</a></li>
              <li>Human Resources: <a href="mailto:hr@company.com">hr@company.com</a></li>
              <li>Facilities: <a href="mailto:facilities@company.com">facilities@company.com</a></li>
            </ul>
        </div>
        );
    }
    ```
    
1. <span data-ttu-id="ceb95-141">Go to the `src/components` directory and update the `App.css` file with the following code to make the email links easier to read in any theme that is used:</span><span class="sxs-lookup"><span data-stu-id="ceb95-141">Go to the `src/components` directory and update the `App.css` file with the following code to make the email links easier to read in any theme that is used:</span></span>
    ```CSS
    a {
      color: inherit;
    }
    ```

## <a name="4-customize-your-tab-configuration-page"></a><span data-ttu-id="ceb95-142">4. Personnaliser la page de configuration de votre onglet</span><span class="sxs-lookup"><span data-stu-id="ceb95-142">4. Customize your tab configuration page</span></span>

<span data-ttu-id="ceb95-143">Chaque onglet d’un canal ou d’une conversation possède une page de configuration, une page modale avec au moins une option de configuration qui s’affiche lorsque les utilisateurs ajoutent votre application.</span><span class="sxs-lookup"><span data-stu-id="ceb95-143">Every tab in a channel or chat has a configuration page, a modal with at least one setup option that displays when users add your app.</span></span> <span data-ttu-id="ceb95-144">La page de configuration demande par défaut aux utilisateurs s’ils souhaitent avertir le canal ou la conversation lors de l’installation de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="ceb95-144">The configuration page by default asks users if they want to notify the channel or chat when the tab is installed.</span></span> <span data-ttu-id="ceb95-145">Vous pouvez personnaliser la page de configuration en ajoutant du contenu personnalisé.</span><span class="sxs-lookup"><span data-stu-id="ceb95-145">You can customize the configuration page by adding custom content.</span></span>

<span data-ttu-id="ceb95-146">Pour ajouter du contenu personnalisé, ouvrez le fichier à partir du répertoire et mettez à jour le contenu de l’espace réservé à l’intérieur, comme `TabConfig.js` `src/components` illustré dans `return()` l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="ceb95-146">To add custom content, open `TabConfig.js` file from the `src/components` directory and update the placeholder content inside `return()` as shown in the following example:</span></span>

  ```JavaScript
  return (
      <div>
        <h1>Add My Contoso Contacts</h1>
        <div>
          Select <b>Save</b> to add our organization's important contacts to this workspace.
        </div>
      </div>
  );
  ```
 
> [!TIP]
> <span data-ttu-id="ceb95-147">Donnez de brèves informations sur votre application sur cette page, car c’est la première fois que les utilisateurs lisent des informations à ce sujet.</span><span class="sxs-lookup"><span data-stu-id="ceb95-147">Give a brief information about your app on this page since this would be the first time users are reading about it.</span></span> <span data-ttu-id="ceb95-148">Vous pouvez également inclure des options de configuration personnalisées ou [un](../tabs/how-to/authentication/auth-aad-sso.md)flux de travail d’authentification, ce qui est courant dans les pages de configuration d’onglets.</span><span class="sxs-lookup"><span data-stu-id="ceb95-148">You can also include custom configuration options or an [authentication workflow](../tabs/how-to/authentication/auth-aad-sso.md), which is common on tab configuration pages.</span></span>

## <a name="5-customize-your-tab-name"></a><span data-ttu-id="ceb95-149">5. Personnaliser le nom de votre onglet</span><span class="sxs-lookup"><span data-stu-id="ceb95-149">5. Customize your tab name</span></span>

<span data-ttu-id="ceb95-150">Lorsque vous ajoutez un onglet de canal, le nom de l’application s’affiche par défaut, par exemple, **première application.**</span><span class="sxs-lookup"><span data-stu-id="ceb95-150">When you add a channel tab, the app name displays by default, for example, **first-app**.</span></span> <span data-ttu-id="ceb95-151">Vous pouvez également fournir un nom plus logique dans le contexte de la collaboration de groupe, par exemple, **Contacts d’équipe**:</span><span class="sxs-lookup"><span data-stu-id="ceb95-151">You can also provide a name that makes more sense in the context of group collaboration, for example, **Team Contacts**:</span></span>

1. <span data-ttu-id="ceb95-152">Go to the `src/components` directory and open the `TabConfig.js` file.</span><span class="sxs-lookup"><span data-stu-id="ceb95-152">Go to the `src/components` directory and open the `TabConfig.js` file.</span></span>
1. <span data-ttu-id="ceb95-153">Ajoutez la propriété avec le nom d’onglet que vous souhaitez afficher par défaut, comme `suggestedDisplayName` `microsoftTeams.settings.setSettings` illustré dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="ceb95-153">Add the `suggestedDisplayName` property with the tab name you want to display by default under `microsoftTeams.settings.setSettings` as shown in the following example:</span></span>

    ```JavaScript
        microsoftTeams.settings.setSettings({
        "contentUrl": "https://localhost:3000/tab",
        "suggestedDisplayName": "Team Contacts"
      });
      ```

## <a name="6-build-and-run-your-app"></a><span data-ttu-id="ceb95-154">6. Créer et exécuter votre application</span><span class="sxs-lookup"><span data-stu-id="ceb95-154">6. Build and run your app</span></span>

<span data-ttu-id="ceb95-155">Ce didacticiel vous apprend à créer et exécuter votre application localement.</span><span class="sxs-lookup"><span data-stu-id="ceb95-155">This tutorial teaches you to build and run your app locally.</span></span> 

1. <span data-ttu-id="ceb95-156">Go to the root directory of your app project in Terminal.</span><span class="sxs-lookup"><span data-stu-id="ceb95-156">Go to the root directory of your app project in Terminal.</span></span>
1. <span data-ttu-id="ceb95-157">Exécutez `npm install`.</span><span class="sxs-lookup"><span data-stu-id="ceb95-157">Run `npm install`.</span></span>
1. <span data-ttu-id="ceb95-158">Exécutez `npm start`.</span><span class="sxs-lookup"><span data-stu-id="ceb95-158">Run `npm start`.</span></span>

<span data-ttu-id="ceb95-159">Ces informations sont également présentes dans la `README` section du kit de ressources.</span><span class="sxs-lookup"><span data-stu-id="ceb95-159">This information is also present in the `README` section of the toolkit.</span></span>
<span data-ttu-id="ceb95-160">Votre application est en cours `https://localhost:3000` d’exécution après la compilation **!**</span><span class="sxs-lookup"><span data-stu-id="ceb95-160">Your app is running on `https://localhost:3000` after the **Compiled successfully!**</span></span> <span data-ttu-id="ceb95-161">s’affiche dans le terminal.</span><span class="sxs-lookup"><span data-stu-id="ceb95-161">message appears in the terminal.</span></span> 

## <a name="7-sideload-your-app-in-teams"></a><span data-ttu-id="ceb95-162">7. Chargement d’une version de version Teams</span><span class="sxs-lookup"><span data-stu-id="ceb95-162">7. Sideload your app in Teams</span></span>

<span data-ttu-id="ceb95-163">Votre application est prête à être testée dans Teams.</span><span class="sxs-lookup"><span data-stu-id="ceb95-163">Your app is ready to test in Teams.</span></span> <span data-ttu-id="ceb95-164">Pour ce faire, vous devez avoir un compte qui autorise le chargement de version d’application.</span><span class="sxs-lookup"><span data-stu-id="ceb95-164">To do this, you must have an account that allows app sideloading.</span></span> 

1. <span data-ttu-id="ceb95-165">Ouvrez un client web Teams dans Visual Studio Code avec la **touche F5.**</span><span class="sxs-lookup"><span data-stu-id="ceb95-165">Open a Teams web client in Visual Studio Code with the **F5** key.</span></span>
1. <span data-ttu-id="ceb95-166">Ajoutez ( ) comme digne de confiance en suivant les étapes suivantes pour permettre l’affichage du contenu de `localhost` votre application dans Teams :</span><span class="sxs-lookup"><span data-stu-id="ceb95-166">Add (`localhost`) as trustworthy by following these steps to enable your app content to display in Teams:</span></span>

   1. <span data-ttu-id="ceb95-167">Ouvrez un nouvel onglet dans la même fenêtre de navigateur (Google Chrome par défaut) qui s’est ouverte avec la **touche F5.**</span><span class="sxs-lookup"><span data-stu-id="ceb95-167">Open a new tab in the same browser window (Google Chrome by default) which opened with the **F5** key.</span></span>
   1. <span data-ttu-id="ceb95-168">Ouvrez `https://localhost:3000/tab` et continuez jusqu’à la page.</span><span class="sxs-lookup"><span data-stu-id="ceb95-168">Open `https://localhost:3000/tab` and proceed to the page.</span></span>

1. <span data-ttu-id="ceb95-169">Sélectionnez **Ajouter à une équipe ou** Ajouter à une **conversation** et recherchez un canal ou une conversation que vous pouvez utiliser pour le test à partir de la modale dans Teams.</span><span class="sxs-lookup"><span data-stu-id="ceb95-169">Select **Add to a team** or **Add to a chat** and locate a channel or chat you can use for testing from the modal in Teams.</span></span>
1. <span data-ttu-id="ceb95-170">Sélectionnez **Configurer un onglet.** La page de configuration s’affiche dans une forme modale.</span><span class="sxs-lookup"><span data-stu-id="ceb95-170">Select **Set up a tab**. The configuration page displays in a modal.</span></span>

   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="Capture d’écran d’une page de configuration d’onglet de canal.":::

1. <span data-ttu-id="ceb95-172">Sélectionnez **Enregistrer** pour configurer l’onglet. La page de contenu suivante s’affiche :</span><span class="sxs-lookup"><span data-stu-id="ceb95-172">Select **Save** to configure the tab. The following content page appears:</span></span>

   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="Capture d’écran d’un onglet de canal avec affichage de contenu statique.":::

## <a name="see-also"></a><span data-ttu-id="ceb95-174">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="ceb95-174">See also</span></span>

* [<span data-ttu-id="ceb95-175">Créer et exécuter votre première application Microsoft Teams application</span><span class="sxs-lookup"><span data-stu-id="ceb95-175">Build and run your first Microsoft Teams app</span></span>](../build-your-first-app/build-and-run.md) 
* [<span data-ttu-id="ceb95-176">Kit de développement logiciel client JavaScript Teams</span><span class="sxs-lookup"><span data-stu-id="ceb95-176">Teams JavaScript client SDK</span></span>](/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* [<span data-ttu-id="ceb95-177">Conception de votre onglet pour Microsoft Teams bureau et web</span><span class="sxs-lookup"><span data-stu-id="ceb95-177">Designing your tab for Microsoft Teams desktop and web</span></span>](../tabs/design/tabs.md) 
* [<span data-ttu-id="ceb95-178">Conception de votre application Microsoft Teams avec des modèles d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="ceb95-178">Designing your Microsoft Teams app with UI templates</span></span>](../concepts/design/design-teams-app-ui-templates.md) 
* [<span data-ttu-id="ceb95-179">Onglets sur les appareils mobiles</span><span class="sxs-lookup"><span data-stu-id="ceb95-179">Tabs on mobile</span></span>](../tabs/design/tabs-mobile.md)
* [<span data-ttu-id="ceb95-180">Prise en charge de l' sign-on unique (SSO) pour les onglets</span><span class="sxs-lookup"><span data-stu-id="ceb95-180">Single sign-on (SSO) support for tabs</span></span>](../tabs/how-to/authentication/auth-aad-sso.md)
* [<span data-ttu-id="ceb95-181">Présentation de l’API Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="ceb95-181">Microsoft Teams API overview</span></span>](/graph/teams-concept-overview)
* [<span data-ttu-id="ceb95-182">Créez un onglet personnel personnalisé avec Node.js et le générateur Yeoman pour Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="ceb95-182">Create a custom personal tab with Node.js and the Yeoman Generator for Microsoft Teams</span></span>](../tabs/quickstarts/create-personal-tab-node-yeoman.md)

## <a name="next-step"></a><span data-ttu-id="ceb95-183">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="ceb95-183">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ceb95-184">Créer un bot</span><span class="sxs-lookup"><span data-stu-id="ceb95-184">Build a bot</span></span>](../build-your-first-app/build-bot.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="ceb95-185">Créer une extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="ceb95-185">Build a messaging extension</span></span>](../build-your-first-app/build-messaging-extension.md)
