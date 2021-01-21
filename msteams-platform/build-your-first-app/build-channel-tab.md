---
title: Get started - Build a channel and group tab
author: heath-hamilton
description: Créez rapidement un onglet de groupe et de canal Microsoft Teams à l’aide de la Shared Computer Toolkit Microsoft Teams.
ms.author: lajanuar
ms.date: 10/09/2020
ms.topic: tutorial
ms.openlocfilehash: 0692d28653063c2f886db9a03e7136379edde9c3
ms.sourcegitcommit: 00c657e3bf57d3b92aca7da941cde47a2eeff4d0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/20/2021
ms.locfileid: "49911876"
---
# <a name="build-a-channel-and-group-tab-for-microsoft-teams"></a><span data-ttu-id="ec5e7-103">Créer un onglet de canal et de groupe pour Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="ec5e7-103">Build a channel and group tab for Microsoft Teams</span></span>

<span data-ttu-id="ec5e7-104">Dans ce didacticiel, vous allez créer un onglet de canal de base *(également* appelé onglet *groupe),* qui est une page en plein écran pour un canal d’équipe ou une conversation.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-104">In this tutorial, you'll build a basic *channel tab* (also known as a *group tab*), which is a full-screen page for a team channel or chat.</span></span> <span data-ttu-id="ec5e7-105">Contrairement à un onglet personnel, les utilisateurs peuvent configurer certains aspects de ce type d’onglet (par exemple, renommer l’onglet afin qu’il soit significatif pour leur canal).</span><span class="sxs-lookup"><span data-stu-id="ec5e7-105">Unlike a personal tab, users can configure some aspects of this kind of tab (for example, rename the tab so it's meaningful to their channel).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="ec5e7-106">Votre affectation</span><span class="sxs-lookup"><span data-stu-id="ec5e7-106">Your assignment</span></span>

<span data-ttu-id="ec5e7-107">Il n’y a pas longtemps, votre organisation a créé une application Teams qui utilise un onglet pour afficher des informations de contact importantes (service d’aide, RESSOURCES HUMAINES, etc.).</span><span class="sxs-lookup"><span data-stu-id="ec5e7-107">Not long ago, your organization created a Teams app that uses a tab to display important contact information (help desk, HR, etc.).</span></span> <span data-ttu-id="ec5e7-108">Toutefois, étant donné qu’il s’agit d’un onglet personnel, chaque utilisateur doit installer l’onglet pour le voir et son adoption est inférieure aux attentes.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-108">However, since it's a personal tab, each user must install the tab to see it and adoption is lower than expected.</span></span> <span data-ttu-id="ec5e7-109">En d’autres termes, trop d’employés ne savent toujours pas comment joindre le service d’aide.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-109">In other words, too many workers still don't know how to reach the help desk.</span></span>

<span data-ttu-id="ec5e7-110">Vous pouvez faciliter la recherche de ces informations en construisant un onglet de canal, ce qui permet de supprimer la charge de l’installation d’une application par tout le monde.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-110">You can make this information easier to find by building a channel tab, which will remove the burden of requiring everyone to install an app.</span></span> <span data-ttu-id="ec5e7-111">Au lieu de cela, un utilisateur peut ajouter l’onglet dans un canal ou une conversation au profit d’un groupe entier.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-111">Instead, one user can add the tab in a channel or chat for the benefit of an entire group.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="ec5e7-112">Ce que vous allez apprendre</span><span class="sxs-lookup"><span data-stu-id="ec5e7-112">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="ec5e7-113">Créer un projet d’application à l’aide du Shared Computer Toolkit Microsoft Teams pour Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="ec5e7-113">Create an app project using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="ec5e7-114">Identifier certaines configurations d’application et la échafaudage pertinentes pour les onglets de canal</span><span class="sxs-lookup"><span data-stu-id="ec5e7-114">Identify some of the app configurations and scaffolding relevant to channel tabs</span></span>
> * <span data-ttu-id="ec5e7-115">Créer du contenu d’onglet</span><span class="sxs-lookup"><span data-stu-id="ec5e7-115">Create tab content</span></span>
> * <span data-ttu-id="ec5e7-116">Créer du contenu pour la page de configuration d’un onglet</span><span class="sxs-lookup"><span data-stu-id="ec5e7-116">Create content for a tab's configuration page</span></span>
> * <span data-ttu-id="ec5e7-117">Fournir un nom d’onglet suggéré</span><span class="sxs-lookup"><span data-stu-id="ec5e7-117">Provide a suggested tab name</span></span>
> * <span data-ttu-id="ec5e7-118">Créer et exécuter votre application localement</span><span class="sxs-lookup"><span data-stu-id="ec5e7-118">Build and run your app locally</span></span>
> * <span data-ttu-id="ec5e7-119">Chargement de version test de votre application dans Teams</span><span class="sxs-lookup"><span data-stu-id="ec5e7-119">Sideload your app in Teams for testing</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ec5e7-120">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="ec5e7-120">Before you begin</span></span>

<span data-ttu-id="ec5e7-121">Si vous ne l’avez pas encore fait, assurez-vous de bien comprendre et [d’installer les conditions préalables de développement teams.](build-first-app-overview.md#get-prerequisites)</span><span class="sxs-lookup"><span data-stu-id="ec5e7-121">If you haven't yet, make sure you [understand and install the Teams development prerequisites](build-first-app-overview.md#get-prerequisites).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="ec5e7-122">1. Créer votre projet d’application</span><span class="sxs-lookup"><span data-stu-id="ec5e7-122">1. Create your app project</span></span>

<span data-ttu-id="ec5e7-123">Le Shared Computer Toolkit Microsoft Teams vous aide à configurer votre application et à configurer la modèle pour les onglets de canal et de groupe, y compris une page de configuration de base et une page de contenu qui affiche « Hello, World! ».</span><span class="sxs-lookup"><span data-stu-id="ec5e7-123">The Microsoft Teams Toolkit helps configure your app and set up scaffolding relevant to channel and group tabs, including a basic configuration page and content page that displays a "Hello, World!"</span></span> <span data-ttu-id="ec5e7-124">Message.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-124">message.</span></span>

> [!TIP]
> <span data-ttu-id="ec5e7-125">Si vous n’avez pas encore créé de projet d’application Teams, il peut vous être utile de suivre ces [instructions](../build-your-first-app/build-and-run.md) qui expliquent les projets plus en détail.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-125">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. In Visual Studio Code, select **Microsoft Teams** on the left Activity Bar and choose Create a new Teams :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **app**.
1. <span data-ttu-id="ec5e7-127">Lorsque vous y invitez, connectez-vous avec votre compte de développement Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-127">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="ec5e7-128">Dans **l’écran Ajouter des fonctionnalités,** **sélectionnez Onglet,** puis **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-128">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
1. <span data-ttu-id="ec5e7-129">Entrez un nom pour votre application Teams.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-129">Enter a name for your Teams app.</span></span> <span data-ttu-id="ec5e7-130">(Il s’agit du nom par défaut de votre application, ainsi que du nom du répertoire de projet d’application sur votre ordinateur local.) Sélectionnez **l’onglet de canal Groupe ou Teams.**</span><span class="sxs-lookup"><span data-stu-id="ec5e7-130">(This is the default name for your app and also the name of the app project directory on your local machine.) Select **Group or Teams channel tab**.</span></span>
1. <span data-ttu-id="ec5e7-131">Sélectionnez **Terminer** en bas de l’écran pour configurer votre projet.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-131">Select **Finish** at the bottom of the screen to configure your project.</span></span>  

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="ec5e7-132">2. Identifier les composants de projet d’application pertinents</span><span class="sxs-lookup"><span data-stu-id="ec5e7-132">2. Identify relevant app project components</span></span>

<span data-ttu-id="ec5e7-133">La plupart des configurations d’application et de la création de la échafaudage sont automatiquement définies lorsque vous créez votre projet avec le kit de ressources.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-133">Much of the app configurations and scaffolding are set up automatically when you create your project with the toolkit.</span></span> <span data-ttu-id="ec5e7-134">Examinons les principaux composants de la création d’un onglet de canal.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-134">Let's look at the main components for building a channel tab.</span></span>

### <a name="app-configurations"></a><span data-ttu-id="ec5e7-135">Configurations d’application</span><span class="sxs-lookup"><span data-stu-id="ec5e7-135">App configurations</span></span>

<span data-ttu-id="ec5e7-136">Dans le kit de ressources, allez dans **App Studio** pour afficher et mettre à jour les configurations de votre application.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-136">In the toolkit, go to **App Studio** to view and update your app configurations.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="ec5e7-137">Échafaudage d’application</span><span class="sxs-lookup"><span data-stu-id="ec5e7-137">App scaffolding</span></span>

<span data-ttu-id="ec5e7-138">La échafaudage de l’application fournit les composants pour le rendu de l’onglet de votre canal dans Teams.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-138">The app scaffolding provides the components for rendering your channel tab in Teams.</span></span> <span data-ttu-id="ec5e7-139">Il y a beaucoup de choses que vous pouvez utiliser, mais pour l’instant, vous ne devez vous concentrer que sur les questions suivantes :</span><span class="sxs-lookup"><span data-stu-id="ec5e7-139">There's a lot you can work with, but for now you only need to focus on the following:</span></span>

* <span data-ttu-id="ec5e7-140">Deux fichiers se trouvent dans `src/components` le répertoire de votre projet :</span><span class="sxs-lookup"><span data-stu-id="ec5e7-140">Two files located in the `src/components` directory of your project:</span></span>
  * <span data-ttu-id="ec5e7-141">`Tab.js` pour le rendu de la page de contenu de votre onglet.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-141">`Tab.js` for rendering your tab's content page.</span></span>
  * <span data-ttu-id="ec5e7-142">`TabConfig.js` pour le rendu de la page de configuration de votre onglet.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-142">`TabConfig.js` for rendering your tab's configuration page.</span></span>
* <span data-ttu-id="ec5e7-143">SDK client JavaScript Microsoft Teams, qui est pré-chargé dans les composants frontaux de votre projet.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-143">Microsoft Teams JavaScript client SDK, which comes pre-loaded in your project's front-end components.</span></span>

## <a name="3-customize-your-tab-content-page"></a><span data-ttu-id="ec5e7-144">3. Personnaliser la page de contenu de votre onglet</span><span class="sxs-lookup"><span data-stu-id="ec5e7-144">3. Customize your tab content page</span></span>

<span data-ttu-id="ec5e7-145">Copiez et mettez à jour l’extrait de code suivant avec des informations pertinentes pour votre organisation ou, par souci de temps, utilisez le code tel qu’il est.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-145">Copy and update the following snippet with information that's relevant to your organization or, for the sake of time, use the code as is.</span></span>

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

<span data-ttu-id="ec5e7-146">Go to the `src/components` directory and open `Tab.js` .</span><span class="sxs-lookup"><span data-stu-id="ec5e7-146">Go to the `src/components` directory and open `Tab.js`.</span></span> <span data-ttu-id="ec5e7-147">Recherchez `render()` la fonction et collez votre contenu à l’intérieur `return()` (comme illustré).</span><span class="sxs-lookup"><span data-stu-id="ec5e7-147">Locate the `render()` function and paste your content inside `return()` (as shown).</span></span>

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

<span data-ttu-id="ec5e7-148">Ajoutez la règle suivante (également située dans ) afin que les liens de messagerie soient plus faciles à lire, quel que `App.css` soit le thème `src/components` utilisé.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-148">Add the following rule to `App.css` (also located in `src/components`) so the email links are easier to read no matter which theme is used.</span></span>

```CSS
a {
  color: inherit;
}
```

## <a name="4-customize-your-tab-configuration-page"></a><span data-ttu-id="ec5e7-149">4. Personnaliser la page de configuration de votre onglet</span><span class="sxs-lookup"><span data-stu-id="ec5e7-149">4. Customize your tab configuration page</span></span>

<span data-ttu-id="ec5e7-150">Chaque onglet d’un canal ou d’une conversation possède une page de configuration, une page modale avec au moins une option de configuration qui s’affiche lorsque les utilisateurs ajoutent votre application.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-150">Every tab in a channel or chat has a configuration page, a modal with at least one setup option that displays when users add your app.</span></span> <span data-ttu-id="ec5e7-151">La page de configuration demande par défaut aux utilisateurs s’ils souhaitent avertir le canal ou la conversation lors de l’installation de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-151">The configuration page by default asks users if they want to notify the channel or chat when the tab is installed.</span></span>

<span data-ttu-id="ec5e7-152">Ajoutez du contenu personnalisé à votre page de configuration.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-152">Add some custom content to your configuration page.</span></span> <span data-ttu-id="ec5e7-153">Go to your project’s `src/components` directory, open `TabConfig.js` , and update the placeholder content inside `return()` (as shown in the following example).</span><span class="sxs-lookup"><span data-stu-id="ec5e7-153">Go to your project's `src/components` directory, open `TabConfig.js`, and update the placeholder content inside `return()` (as shown in the following example).</span></span>

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
> <span data-ttu-id="ec5e7-154">Fournissez au moins quelques informations brèves sur votre application sur cette page, car il peut s’agit de la première fois que les utilisateurs en font l’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-154">At minimum, provide some brief information about your app on this page since this may be the first time users are learning about it.</span></span> <span data-ttu-id="ec5e7-155">Vous pouvez également inclure des options de configuration personnalisées ou [un](../tabs/how-to/authentication/auth-aad-sso.md)flux de travail d’authentification, ce qui est courant dans les pages de configuration d’onglets.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-155">You also could include custom configuration options or an [authentication workflow](../tabs/how-to/authentication/auth-aad-sso.md), which is common on tab configuration pages.</span></span>

## <a name="5-provide-a-suggested-tab-name"></a><span data-ttu-id="ec5e7-156">5. Fournir un nom d’onglet suggéré</span><span class="sxs-lookup"><span data-stu-id="ec5e7-156">5. Provide a suggested tab name</span></span>

<span data-ttu-id="ec5e7-157">Lorsque vous ajoutez un onglet de canal, le nom de l’application s’affiche par défaut (par exemple, **première application).**</span><span class="sxs-lookup"><span data-stu-id="ec5e7-157">When you add a channel tab, by default the app name displays (for example, **first-app**).</span></span>

<span data-ttu-id="ec5e7-158">Cela peut être correct en fonction de ce que vous appelez votre application, mais vous souhaitez peut-être fournir un nom plus logique dans le contexte de la collaboration de groupe (par exemple, Contacts **d’équipe).**</span><span class="sxs-lookup"><span data-stu-id="ec5e7-158">This may be fine depending on what you call your app, but you may want to provide a name that makes more sense in the context of group collaboration (for example, **Team Contacts**).</span></span>

1. <span data-ttu-id="ec5e7-159">Dans `TabConfig.js` , allez à `microsoftTeams.settings.setSettings` .</span><span class="sxs-lookup"><span data-stu-id="ec5e7-159">In `TabConfig.js`, go to `microsoftTeams.settings.setSettings`.</span></span>
2. <span data-ttu-id="ec5e7-160">Ajoutez `suggestedDisplayName` la propriété avec le nom d’onglet que vous souhaitez afficher par défaut.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-160">Add the `suggestedDisplayName` property with the tab name you want to display by default.</span></span> 
3. <span data-ttu-id="ec5e7-161">Utilisez le nom fourni dans l’exemple suivant ou tapez votre nom.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-161">Use the name provided in the following example or type your name.</span></span> <span data-ttu-id="ec5e7-162">(Par défaut, les utilisateurs peuvent modifier le nom.)</span><span class="sxs-lookup"><span data-stu-id="ec5e7-162">(By default, users can change the name.)</span></span>

```JavaScript
microsoftTeams.settings.setSettings({
  "contentUrl": "https://localhost:3000/tab",
  "suggestedDisplayName": "Team Contacts"
});
```

## <a name="6-build-and-run-your-app"></a><span data-ttu-id="ec5e7-163">6. Créer et exécuter votre application</span><span class="sxs-lookup"><span data-stu-id="ec5e7-163">6. Build and run your app</span></span>

<span data-ttu-id="ec5e7-164">Dans l’intérêt du temps, vous allez créer et exécuter votre application localement.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-164">In the interest of time, you'll build and run your app locally.</span></span>

<span data-ttu-id="ec5e7-165">(Ces informations sont également disponibles dans le kit de `README` ressources.)</span><span class="sxs-lookup"><span data-stu-id="ec5e7-165">(This information is also available in the toolkit `README`.)</span></span>

1. <span data-ttu-id="ec5e7-166">Dans un terminal, allez dans le répertoire racine de votre projet d’application et exécutez `npm install` .</span><span class="sxs-lookup"><span data-stu-id="ec5e7-166">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="ec5e7-167">Exécutez `npm start` .</span><span class="sxs-lookup"><span data-stu-id="ec5e7-167">Run `npm start`.</span></span>

<span data-ttu-id="ec5e7-168">Une fois terminé, une compilation a **réussi !**</span><span class="sxs-lookup"><span data-stu-id="ec5e7-168">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="ec5e7-169">dans le terminal.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-169">message in the terminal.</span></span> <span data-ttu-id="ec5e7-170">Votre application est en cours d’exécution sur `https://localhost:3000` .</span><span class="sxs-lookup"><span data-stu-id="ec5e7-170">Your app is running on `https://localhost:3000`.</span></span>

## <a name="7-sideload-your-app-in-teams"></a><span data-ttu-id="ec5e7-171">7. Chargement de version de version de votre application dans Teams</span><span class="sxs-lookup"><span data-stu-id="ec5e7-171">7. Sideload your app in Teams</span></span>

<span data-ttu-id="ec5e7-172">Votre application est prête à être testée dans Teams.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-172">Your app is ready to test in Teams.</span></span> <span data-ttu-id="ec5e7-173">Pour ce faire, vous devez avoir un compte qui autorise le chargement de version de version d’application.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-173">To do this, you must have an account that allows app sideloading.</span></span> <span data-ttu-id="ec5e7-174">(Si vous n’êtes pas sûr de l’avoir, découvrez comment obtenir un compte [de développement Teams.)](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account)</span><span class="sxs-lookup"><span data-stu-id="ec5e7-174">(If you aren't sure you have that, learn about getting a [Teams development account](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).)</span></span>

1. <span data-ttu-id="ec5e7-175">Dans Visual Studio Code, appuyez sur la **touche F5** pour lancer un client web Teams.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-175">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="ec5e7-176">Pour afficher le contenu de votre application dans Teams, spécifiez que l’endroit où votre application est en cours d’exécution ( `localhost` ) est digne de confiance :</span><span class="sxs-lookup"><span data-stu-id="ec5e7-176">To display your app content in Teams, specify that where your app is running (`localhost`) is trustworthy:</span></span>
   1. <span data-ttu-id="ec5e7-177">Ouvrez un nouvel onglet dans la même fenêtre de navigateur (Google Chrome par défaut) qui s’est ouvert après avoir appuyez sur **F5**.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-177">Open a new tab in the same browser window (Google Chrome by default) which opened after pressing **F5**.</span></span>
   1. <span data-ttu-id="ec5e7-178">Go to `https://localhost:3000/tab` and proceed to the page.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-178">Go to `https://localhost:3000/tab` and proceed to the page.</span></span>
1. <span data-ttu-id="ec5e7-179">Revenir à Teams.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-179">Go back to Teams.</span></span> <span data-ttu-id="ec5e7-180">Dans la modale, sélectionnez Ajouter à une équipe ou Ajouter à une **conversation** et recherchez un canal ou une conversation que vous pouvez utiliser pour le test. </span><span class="sxs-lookup"><span data-stu-id="ec5e7-180">In the modal, select **Add to a team** or **Add to a chat** and locate a channel or chat you can use for testing.</span></span>
1. <span data-ttu-id="ec5e7-181">Sélectionnez **Configurer un onglet.** La page de configuration s’affiche dans une forme modale.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-181">Select **Set up a tab**. The configuration page displays in a modal.</span></span><br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="Capture d’écran d’une page de configuration d’onglet de canal.":::
1. <span data-ttu-id="ec5e7-183">Sélectionnez **Enregistrer** pour configurer l’onglet. La page de contenu s’affiche.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-183">Select **Save** to configure the tab. The content page displays.</span></span><br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="Capture d’écran d’un onglet de canal avec affichage de contenu statique.":::

## <a name="well-done"></a><span data-ttu-id="ec5e7-185">Bien jouer</span><span class="sxs-lookup"><span data-stu-id="ec5e7-185">Well done</span></span>

<span data-ttu-id="ec5e7-186">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="ec5e7-186">Congratulations!</span></span> <span data-ttu-id="ec5e7-187">Vous avez une application Teams avec un onglet pour afficher du contenu utile dans les canaux et les conversations.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-187">You have a Teams app with a tab for displaying useful content in channels and chats.</span></span>

## <a name="learn-more"></a><span data-ttu-id="ec5e7-188">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="ec5e7-188">Learn more</span></span>

* <span data-ttu-id="ec5e7-189">Suivez nos [instructions de conception](../tabs/design/tabs.md) et créez avec des [modèles d’interface utilisateur](../concepts/design/design-teams-app-ui-templates.md) prêts pour la production pour créer une expérience transparente.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-189">Follow our [design guidelines](../tabs/design/tabs.md) and build with [production-ready UI templates](../concepts/design/design-teams-app-ui-templates.md) to create a seamless experience.</span></span>
* <span data-ttu-id="ec5e7-190">Comprendre [les considérations mobiles pour](../tabs/design/tabs-mobile.md) les onglets.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-190">Understand [mobile considerations](../tabs/design/tabs-mobile.md) for tabs.</span></span>
* <span data-ttu-id="ec5e7-191">[Ajoutez l’authentification sso à votre onglet.](../tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="ec5e7-191">[Add SSO authentication to your tab](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>
* <span data-ttu-id="ec5e7-192">Utiliser les données Teams avec [Microsoft Graph.](https://docs.microsoft.com/graph/teams-concept-overview)</span><span class="sxs-lookup"><span data-stu-id="ec5e7-192">Utilize Teams data with [Microsoft Graph](https://docs.microsoft.com/graph/teams-concept-overview).</span></span>
* [<span data-ttu-id="ec5e7-193">Créer un onglet sans le kit de ressources</span><span class="sxs-lookup"><span data-stu-id="ec5e7-193">Create a tab without the toolkit</span></span>](../tabs/quickstarts/create-channel-group-tab-node-yeoman.md)

## <a name="next-lesson"></a><span data-ttu-id="ec5e7-194">Leçon suivante</span><span class="sxs-lookup"><span data-stu-id="ec5e7-194">Next lesson</span></span>

<span data-ttu-id="ec5e7-195">Vous savez comment créer un onglet pour la collaboration.</span><span class="sxs-lookup"><span data-stu-id="ec5e7-195">You know how to build a tab for collaboration.</span></span> <span data-ttu-id="ec5e7-196">Vous souhaitez essayer de créer un autre type d’application Teams ?</span><span class="sxs-lookup"><span data-stu-id="ec5e7-196">Want to try building a different kind of Teams app?</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ec5e7-197">Créer un bot</span><span class="sxs-lookup"><span data-stu-id="ec5e7-197">Build a bot</span></span>](../build-your-first-app/build-bot.md)
