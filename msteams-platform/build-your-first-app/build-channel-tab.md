---
title: Prise en main-créer un onglet de canal et de groupe
author: heath-hamilton
description: Créez rapidement un onglet de chaîne et de groupe Microsoft teams à l’aide du kit de développement Microsoft Teams.
ms.author: lajanuar
ms.date: 10/09/2020
ms.topic: tutorial
ms.openlocfilehash: bb87d34974469057287cf63725e7722125c57c34
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/09/2020
ms.locfileid: "49605244"
---
# <a name="build-a-channel-and-group-tab-for-microsoft-teams"></a><span data-ttu-id="9543f-103">Créer un onglet de canal et de groupe pour Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="9543f-103">Build a channel and group tab for Microsoft Teams</span></span>

<span data-ttu-id="9543f-104">Dans ce didacticiel, vous allez créer un *onglet de canal* de base (également appelé *onglet de groupe*), qui est une page plein écran pour un canal d’équipe ou une conversation.</span><span class="sxs-lookup"><span data-stu-id="9543f-104">In this tutorial, you'll build a basic *channel tab* (also known as a *group tab*), which is a full-screen page for a team channel or chat.</span></span> <span data-ttu-id="9543f-105">Contrairement à un onglet personnel, les utilisateurs peuvent configurer certains aspects de ce type d’onglet (par exemple, renommer l’onglet de sorte qu’il soit significatif pour son canal).</span><span class="sxs-lookup"><span data-stu-id="9543f-105">Unlike a personal tab, users can configure some aspects of this kind of tab (for example, rename the tab so it's meaningful to their channel).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="9543f-106">Votre affectation</span><span class="sxs-lookup"><span data-stu-id="9543f-106">Your assignment</span></span>

<span data-ttu-id="9543f-107">Il n’y a pas longtemps, votre organisation a créé une application teams qui utilise un onglet pour afficher les informations de contact importantes (support technique, RH, etc.).</span><span class="sxs-lookup"><span data-stu-id="9543f-107">Not long ago, your organization created a Teams app that uses a tab to display important contact information (help desk, HR, etc.).</span></span> <span data-ttu-id="9543f-108">Toutefois, étant donné qu’il s’agit d’un onglet personnel, chaque utilisateur doit installer l’onglet pour l’afficher et l’adoption est plus faible que prévu.</span><span class="sxs-lookup"><span data-stu-id="9543f-108">However, since it's a personal tab, each user must install the tab to see it and adoption is lower than expected.</span></span> <span data-ttu-id="9543f-109">En d’autres termes, trop de travailleurs ne sachent toujours pas comment contacter le support technique.</span><span class="sxs-lookup"><span data-stu-id="9543f-109">In other words, too many workers still don't know how to reach the help desk.</span></span>

<span data-ttu-id="9543f-110">Vous pouvez faciliter la recherche de ces informations en créant un onglet de canal, ce qui vous évite de devoir installer une application.</span><span class="sxs-lookup"><span data-stu-id="9543f-110">You can make this information easier to find by building a channel tab, which will remove the burden of requiring everyone to install an app.</span></span> <span data-ttu-id="9543f-111">Au lieu de cela, un utilisateur peut ajouter l’onglet dans un canal ou une conversation pour l’ensemble du groupe.</span><span class="sxs-lookup"><span data-stu-id="9543f-111">Instead, one user can add the tab in a channel or chat for the benefit of an entire group.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="9543f-112">Ce que vous allez apprendre</span><span class="sxs-lookup"><span data-stu-id="9543f-112">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="9543f-113">Créer un projet d’application à l’aide de Microsoft teams Toolkit pour Visual Studio code</span><span class="sxs-lookup"><span data-stu-id="9543f-113">Create an app project using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="9543f-114">Identifier certaines configurations d’application et la génération de modèles automatique concernant les onglets canal et groupe</span><span class="sxs-lookup"><span data-stu-id="9543f-114">Identify some of the app configurations and scaffolding relevant to channel and group tabs</span></span>
> * <span data-ttu-id="9543f-115">Créer un contenu de tabulation</span><span class="sxs-lookup"><span data-stu-id="9543f-115">Create tab content</span></span>
> * <span data-ttu-id="9543f-116">Créer du contenu pour la page de configuration d’un onglet</span><span class="sxs-lookup"><span data-stu-id="9543f-116">Create content for a tab's configuration page</span></span>
> * <span data-ttu-id="9543f-117">Fournir un nom d’onglet suggéré</span><span class="sxs-lookup"><span data-stu-id="9543f-117">Provide a suggested tab name</span></span>
> * <span data-ttu-id="9543f-118">Créer et exécuter votre application localement</span><span class="sxs-lookup"><span data-stu-id="9543f-118">Build and run your app locally</span></span>
> * <span data-ttu-id="9543f-119">Chargement de votre application dans teams à des fins de test</span><span class="sxs-lookup"><span data-stu-id="9543f-119">Sideload your app in Teams for testing</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9543f-120">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="9543f-120">Before you begin</span></span>

<span data-ttu-id="9543f-121">Si vous ne l’avez pas encore fait, assurez-vous de [bien comprendre et installer les conditions préalables au développement de teams](build-first-app-overview.md#get-prerequisites).</span><span class="sxs-lookup"><span data-stu-id="9543f-121">If you haven't yet, make sure you [understand and install the Teams development prerequisites](build-first-app-overview.md#get-prerequisites).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="9543f-122">1. créer votre projet d’application</span><span class="sxs-lookup"><span data-stu-id="9543f-122">1. Create your app project</span></span>

<span data-ttu-id="9543f-123">Le kit de développement Microsoft teams vous aide à configurer votre application et à configurer la génération de modèles automatique correspondant aux onglets canal et groupe, notamment une page de configuration de base et une page de contenu qui affiche un « Hello, World ! ».</span><span class="sxs-lookup"><span data-stu-id="9543f-123">The Microsoft Teams Toolkit helps configure your app and set up scaffolding relevant to channel and group tabs, including a basic configuration page and content page that displays a "Hello, World!"</span></span> <span data-ttu-id="9543f-124">Message.</span><span class="sxs-lookup"><span data-stu-id="9543f-124">message.</span></span>

> [!TIP]
> <span data-ttu-id="9543f-125">Si vous n’avez pas encore créé de projet d’application Teams, il peut s’avérer utile de suivre [ces instructions](../build-your-first-app/build-and-run.md) pour expliquer plus en détail les projets.</span><span class="sxs-lookup"><span data-stu-id="9543f-125">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. Dans Visual Studio code, sélectionnez **Microsoft teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: dans la barre d’activité de gauche et choisissez **créer une nouvelle application teams**.
1. <span data-ttu-id="9543f-127">Lorsque vous y êtes invité, connectez-vous à l’aide de votre compte de développement Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="9543f-127">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="9543f-128">Sur l’écran **Ajouter des fonctionnalités** , sélectionnez **tabulation** puis **suivant**.</span><span class="sxs-lookup"><span data-stu-id="9543f-128">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
1. <span data-ttu-id="9543f-129">Entrez un nom pour votre application Teams.</span><span class="sxs-lookup"><span data-stu-id="9543f-129">Enter a name for your Teams app.</span></span> <span data-ttu-id="9543f-130">(Il s’agit du nom par défaut de votre application, ainsi que du nom du répertoire du projet d’application sur votre ordinateur local.)</span><span class="sxs-lookup"><span data-stu-id="9543f-130">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="9543f-131">Cochez les options de l’onglet **personnel** , des **onglets de groupe ou de canal teams** .</span><span class="sxs-lookup"><span data-stu-id="9543f-131">Check the **Personal tab** and **Group or Teams channel tab** options.</span></span> <span data-ttu-id="9543f-132">(Vous saurez bientôt pourquoi vous avez besoin des deux types d’onglets.)</span><span class="sxs-lookup"><span data-stu-id="9543f-132">(You'll soon learn why you need both types of tabs.)</span></span>
1. <span data-ttu-id="9543f-133">Sélectionnez **Terminer** en bas de l’écran pour configurer votre projet.</span><span class="sxs-lookup"><span data-stu-id="9543f-133">Select **Finish** at the bottom of the screen to configure your project.</span></span>  

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="9543f-134">2. identifier les composants de projet d’application pertinents</span><span class="sxs-lookup"><span data-stu-id="9543f-134">2. Identify relevant app project components</span></span>

<span data-ttu-id="9543f-135">La plupart des configurations et des modèles d’application sont configurés automatiquement lorsque vous créez votre projet à l’aide de Team Toolkit.</span><span class="sxs-lookup"><span data-stu-id="9543f-135">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="9543f-136">Examinons les principaux composants de création d’un onglet de canal et de groupe.</span><span class="sxs-lookup"><span data-stu-id="9543f-136">Let's look at the main components for building a channel and group tab.</span></span>

### <a name="app-configurations"></a><span data-ttu-id="9543f-137">Configurations d’application</span><span class="sxs-lookup"><span data-stu-id="9543f-137">App configurations</span></span>

<span data-ttu-id="9543f-138">Vous pouvez afficher et mettre à jour les configurations de vos applications à l’aide d’App Studio, qui est inclus dans la boîte à outils.</span><span class="sxs-lookup"><span data-stu-id="9543f-138">You can view and update your app configurations using App Studio, which is included in the toolkit.</span></span>

<span data-ttu-id="9543f-139">Lors de l’installation, le kit de fonctions a initialement configuré deux composants essentiels des onglets canal et groupe :</span><span class="sxs-lookup"><span data-stu-id="9543f-139">During setup, the toolkit initially configured two essential components of channel and group tabs:</span></span>

* <span data-ttu-id="9543f-140">**Page de configuration**: modal pour l’ajout d’un onglet à un canal ou une conversation.</span><span class="sxs-lookup"><span data-stu-id="9543f-140">**Configuration page**: The modal for adding a tab to a channel or chat.</span></span> <span data-ttu-id="9543f-141">(Dans App Studio, vous pouvez trouver cette page en accédant à onglets **> onglet équipe**.)</span><span class="sxs-lookup"><span data-stu-id="9543f-141">(In App Studio, you can find this page by going to **Tabs > Team tab**.)</span></span>
* <span data-ttu-id="9543f-142">**Page de contenu**: où vous affichez votre contenu principal.</span><span class="sxs-lookup"><span data-stu-id="9543f-142">**Content page**: Where you display your primary content.</span></span> <span data-ttu-id="9543f-143">(Dans App Studio, vous pouvez trouver cette page en accédant aux **onglets > ajouter un onglet personnel**.)</span><span class="sxs-lookup"><span data-stu-id="9543f-143">(In App Studio, you can find this page by going to **Tabs > Add a personal tab**.)</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="9543f-144">Génération de modèles automatique d’application</span><span class="sxs-lookup"><span data-stu-id="9543f-144">App scaffolding</span></span>

<span data-ttu-id="9543f-145">Le échafaudage de l’application fournit les composants pour le rendu de votre onglet personnel dans Teams.</span><span class="sxs-lookup"><span data-stu-id="9543f-145">The app scaffolding provides the components for rendering your personal tab in Teams.</span></span> <span data-ttu-id="9543f-146">Vous pouvez utiliser un grand nombre de choses, mais pour le moment, il vous suffit de vous concentrer sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="9543f-146">There's a lot you can work with, but for now you only need to focus on the following:</span></span>

* <span data-ttu-id="9543f-147">Deux fichiers situés dans le `src/components` Répertoire de votre projet :</span><span class="sxs-lookup"><span data-stu-id="9543f-147">Two files located in the `src/components` directory of your project:</span></span>
  * <span data-ttu-id="9543f-148">`Tab.js` pour afficher la page de contenu de votre onglet.</span><span class="sxs-lookup"><span data-stu-id="9543f-148">`Tab.js` for rendering your tab's content page.</span></span>
  * <span data-ttu-id="9543f-149">`TabConfig.js` pour afficher la page de configuration de votre onglet.</span><span class="sxs-lookup"><span data-stu-id="9543f-149">`TabConfig.js` for rendering your tab's configuration page.</span></span>
* <span data-ttu-id="9543f-150">Le kit de développement logiciel (SDK) JavaScript de Microsoft Teams, qui est préchargé dans les composants frontaux de votre projet.</span><span class="sxs-lookup"><span data-stu-id="9543f-150">Microsoft Teams JavaScript client SDK, which comes pre-loaded in your project's front-end components.</span></span>

## <a name="3-customize-your-tab-content-page"></a><span data-ttu-id="9543f-151">3. personnaliser votre page de contenu d’onglet</span><span class="sxs-lookup"><span data-stu-id="9543f-151">3. Customize your tab content page</span></span>

<span data-ttu-id="9543f-152">Copiez et mettez à jour l’extrait de code suivant avec des informations pertinentes pour votre organisation ou, pour des raisons de temps, utilisez le code tel quel.</span><span class="sxs-lookup"><span data-stu-id="9543f-152">Copy and update the following snippet with information that's relevant to your organization or, for the sake of time, use the code as is.</span></span>

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

<span data-ttu-id="9543f-153">Accédez au `src/components` répertoire et ouvrez `Tab.js` .</span><span class="sxs-lookup"><span data-stu-id="9543f-153">Go to the `src/components` directory and open `Tab.js`.</span></span> <span data-ttu-id="9543f-154">Recherchez la `render()` fonction et collez votre contenu dans `return()` (comme illustré).</span><span class="sxs-lookup"><span data-stu-id="9543f-154">Locate the `render()` function and paste your content inside `return()` (as shown).</span></span>

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

<span data-ttu-id="9543f-155">Ajoutez la règle suivante à `App.css` (également dans `src/components` ) de sorte que les liens électroniques soient plus faciles à lire, quel que soit le thème utilisé.</span><span class="sxs-lookup"><span data-stu-id="9543f-155">Add the following rule to `App.css` (also located in `src/components`) so the email links are easier to read no matter which theme is used.</span></span>

```CSS
a {
  color: inherit;
}
```

## <a name="4-customize-your-tab-configuration-page"></a><span data-ttu-id="9543f-156">4. personnaliser votre page de configuration d’onglet</span><span class="sxs-lookup"><span data-stu-id="9543f-156">4. Customize your tab configuration page</span></span>

<span data-ttu-id="9543f-157">Chaque onglet d’un canal ou d’une conversation comporte une page de configuration, modale avec au moins une option d’installation qui s’affiche lorsque les utilisateurs ajoutent votre application.</span><span class="sxs-lookup"><span data-stu-id="9543f-157">Every tab in a channel or chat has a configuration page, a modal with at least one setup option that displays when users add your app.</span></span> <span data-ttu-id="9543f-158">La page Configuration par défaut demande à l’utilisateur s’il souhaite avertir le canal ou la conversation lorsque l’onglet est installé.</span><span class="sxs-lookup"><span data-stu-id="9543f-158">The configuration page by default asks users if they want to notify the channel or chat when the tab is installed.</span></span>

<span data-ttu-id="9543f-159">Ajoutez du contenu personnalisé à votre page de configuration.</span><span class="sxs-lookup"><span data-stu-id="9543f-159">Add some custom content to your configuration page.</span></span> <span data-ttu-id="9543f-160">Accédez au répertoire de votre projet `src/components` , ouvrez `TabConfig.js` et mettez à jour le contenu de l’espace réservé dans `return()` (comme illustré dans l’exemple suivant).</span><span class="sxs-lookup"><span data-stu-id="9543f-160">Go to your project's `src/components` directory, open `TabConfig.js`, and update the placeholder content inside `return()` (as shown in the following example).</span></span>

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
> <span data-ttu-id="9543f-161">Au minimum, fournissez des informations succinctes sur votre application sur cette page, car il peut s’agir de la première fois que les utilisateurs en apprennent à le faire.</span><span class="sxs-lookup"><span data-stu-id="9543f-161">At minimum, provide some brief information about your app on this page since this may be the first time users are learning about it.</span></span> <span data-ttu-id="9543f-162">Vous pouvez également inclure des options de configuration personnalisées ou un [flux de travail d’authentification](../tabs/how-to/authentication/auth-aad-sso.md), qui est courant sur les pages de configuration d’onglet.</span><span class="sxs-lookup"><span data-stu-id="9543f-162">You also could include custom configuration options or an [authentication workflow](../tabs/how-to/authentication/auth-aad-sso.md), which is common on tab configuration pages.</span></span>

## <a name="5-provide-a-suggested-tab-name"></a><span data-ttu-id="9543f-163">5. fournir un nom d’onglet suggéré</span><span class="sxs-lookup"><span data-stu-id="9543f-163">5. Provide a suggested tab name</span></span>

<span data-ttu-id="9543f-164">Lorsque vous ajoutez un onglet de canal ou de groupe, le nom de l’application s’affiche par défaut (par exemple, **First-App**).</span><span class="sxs-lookup"><span data-stu-id="9543f-164">When you add a channel or group tab, by default the app name displays (for example, **first-app**).</span></span>

<span data-ttu-id="9543f-165">Cela peut être approprié en fonction de ce que vous appelez votre application, mais vous souhaiterez peut-être attribuer un nom plus évocateur dans le contexte de la collaboration de groupe (par exemple, **contacts d’équipe**).</span><span class="sxs-lookup"><span data-stu-id="9543f-165">This may be fine depending on what you call your app, but you may want to provide a name that makes more sense in the context of group collaboration (for example, **Team Contacts**).</span></span>

<span data-ttu-id="9543f-166">Dans `TabConfig.js` , accédez à `microsoftTeams.settings.setSettings` .</span><span class="sxs-lookup"><span data-stu-id="9543f-166">In `TabConfig.js`, go to `microsoftTeams.settings.setSettings`.</span></span> <span data-ttu-id="9543f-167">Ajoutez la `suggestedDisplayName` propriété avec le nom de l’onglet que vous souhaitez afficher par défaut (comme illustré).</span><span class="sxs-lookup"><span data-stu-id="9543f-167">Add the `suggestedDisplayName` property with the tab name you want to display by default (as shown).</span></span> <span data-ttu-id="9543f-168">Utilisez le nom fourni ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="9543f-168">Use the provided name or create your own.</span></span> <span data-ttu-id="9543f-169">(Par défaut, les utilisateurs peuvent modifier le nom si ils le souhaitent.)</span><span class="sxs-lookup"><span data-stu-id="9543f-169">(By default, users to change the name if they want.)</span></span>

```JavaScript
microsoftTeams.settings.setSettings({
  "contentUrl": "https://localhost:3000/tab",
  "suggestedDisplayName": "Team Contacts"
});
```

## <a name="6-build-and-run-your-app"></a><span data-ttu-id="9543f-170">6. générez et exécutez votre application</span><span class="sxs-lookup"><span data-stu-id="9543f-170">6. Build and run your app</span></span>

<span data-ttu-id="9543f-171">Pour des raisons de temps, vous allez créer et exécuter votre application localement.</span><span class="sxs-lookup"><span data-stu-id="9543f-171">In the interest of time, you'll build and run your app locally.</span></span>

<span data-ttu-id="9543f-172">(Ces informations sont également disponibles dans la boîte à outils `README` .)</span><span class="sxs-lookup"><span data-stu-id="9543f-172">(This information is also available in the toolkit `README`.)</span></span>

1. <span data-ttu-id="9543f-173">Dans un terminal, accédez au répertoire racine de votre projet d’application et exécutez `npm install` .</span><span class="sxs-lookup"><span data-stu-id="9543f-173">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="9543f-174">Exécuter `npm start` .</span><span class="sxs-lookup"><span data-stu-id="9543f-174">Run `npm start`.</span></span>

<span data-ttu-id="9543f-175">Une fois terminé, une **compilation est effectuée.**</span><span class="sxs-lookup"><span data-stu-id="9543f-175">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="9543f-176">message dans le terminal.</span><span class="sxs-lookup"><span data-stu-id="9543f-176">message in the terminal.</span></span> <span data-ttu-id="9543f-177">Votre application est en cours d’exécution sur `https://localhost:3000` .</span><span class="sxs-lookup"><span data-stu-id="9543f-177">Your app is running on `https://localhost:3000`.</span></span>

## <a name="7-sideload-your-app-in-teams"></a><span data-ttu-id="9543f-178">7. chargement de votre application dans teams</span><span class="sxs-lookup"><span data-stu-id="9543f-178">7. Sideload your app in Teams</span></span>

<span data-ttu-id="9543f-179">Votre application est prête à être testée dans Teams.</span><span class="sxs-lookup"><span data-stu-id="9543f-179">Your app is ready to test in Teams.</span></span> <span data-ttu-id="9543f-180">Pour ce faire, vous devez disposer d’un compte qui autorise l’application chargement.</span><span class="sxs-lookup"><span data-stu-id="9543f-180">To do this, you must have an account that allows app sideloading.</span></span> <span data-ttu-id="9543f-181">(Si vous n’êtes pas sûr, Découvrez comment obtenir un [compte de développement teams](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).)</span><span class="sxs-lookup"><span data-stu-id="9543f-181">(If you aren't sure you have that, learn about getting a [Teams development account](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).)</span></span>

1. <span data-ttu-id="9543f-182">Dans Visual Studio code, appuyez sur la touche **F5** pour lancer un client Web Teams.</span><span class="sxs-lookup"><span data-stu-id="9543f-182">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="9543f-183">Pour afficher le contenu de votre application dans Teams, spécifiez le lieu de fiabilité de votre application ( `localhost` ).</span><span class="sxs-lookup"><span data-stu-id="9543f-183">To display your app content in Teams, specify that where your app is running (`localhost`) is trustworthy:</span></span>
   1. <span data-ttu-id="9543f-184">Ouvrez un nouvel onglet dans la même fenêtre de navigateur (Google Chrome par défaut) qui s’est ouvert après avoir appuyé sur **F5**.</span><span class="sxs-lookup"><span data-stu-id="9543f-184">Open a new tab in the same browser window (Google Chrome by default) which opened after pressing **F5**.</span></span>
   1. <span data-ttu-id="9543f-185">Accédez à `https://localhost:3000/tab` la page et passez à la page.</span><span class="sxs-lookup"><span data-stu-id="9543f-185">Go to `https://localhost:3000/tab` and proceed to the page.</span></span>
1. <span data-ttu-id="9543f-186">Revenir à Teams.</span><span class="sxs-lookup"><span data-stu-id="9543f-186">Go back to Teams.</span></span> <span data-ttu-id="9543f-187">Dans le modal, sélectionnez **Ajouter à une équipe** ou **Ajouter à une conversation** et recherchez un canal ou une conversation que vous pouvez utiliser à des fins de test.</span><span class="sxs-lookup"><span data-stu-id="9543f-187">In the modal, select **Add to a team** or **Add to a chat** and locate a channel or chat you can use for testing.</span></span>
1. <span data-ttu-id="9543f-188">Sélectionnez **configurer un onglet**. La page de configuration s’affiche dans un modal.</span><span class="sxs-lookup"><span data-stu-id="9543f-188">Select **Set up a tab**. The configuration page displays in a modal.</span></span><br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="Capture d’écran de la page de configuration de l’onglet canal.":::
1. <span data-ttu-id="9543f-190">Sélectionnez **Enregistrer** pour configurer l’onglet. La page de contenu s’affiche.</span><span class="sxs-lookup"><span data-stu-id="9543f-190">Select **Save** to configure the tab. The content page displays.</span></span><br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="Capture d’écran d’un onglet de canal avec affichage de contenu statique.":::

## <a name="well-done"></a><span data-ttu-id="9543f-192">Bien jouer</span><span class="sxs-lookup"><span data-stu-id="9543f-192">Well done</span></span>

<span data-ttu-id="9543f-193">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="9543f-193">Congratulations!</span></span> <span data-ttu-id="9543f-194">Vous disposez d’une application teams avec un onglet qui permet d’afficher du contenu utile dans les canaux et les conversations.</span><span class="sxs-lookup"><span data-stu-id="9543f-194">You have a Teams app with a tab for displaying useful content in channels and chats.</span></span>

## <a name="learn-more"></a><span data-ttu-id="9543f-195">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="9543f-195">Learn more</span></span>

* <span data-ttu-id="9543f-196">[Authentifier les utilisateurs avec l’authentification](../tabs/how-to/authentication/auth-aad-sso.md)unique : Si vous souhaitez uniquement que les utilisateurs autorisés visualisent votre onglet, configurez l’authentification unique (SSO) via Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="9543f-196">[Authenticate tab users with SSO](../tabs/how-to/authentication/auth-aad-sso.md): If you only want authorized users viewing your tab, set up single sign-on (SSO) through Azure Active Directory (AD).</span></span>
* <span data-ttu-id="9543f-197">[Incorporer du contenu à partir d’une application Web ou d’une page Web existante](../tabs/how-to/add-tab.md#tab-requirements): nous vous avons expliqué comment créer du contenu pour un onglet personnel, mais vous pouvez également charger du contenu à partir d’une URL externe.</span><span class="sxs-lookup"><span data-stu-id="9543f-197">[Embed content from an existing web app or webpage](../tabs/how-to/add-tab.md#tab-requirements): We showed you how to create new content for a personal tab, but you can also load content from an external URL.</span></span>
* <span data-ttu-id="9543f-198">[Créez une expérience transparente pour votre onglet](../tabs/design/tabs.md): consultez les instructions recommandées pour la création d’onglets Teams.</span><span class="sxs-lookup"><span data-stu-id="9543f-198">[Create a seamless experience for your tab](../tabs/design/tabs.md): See the recommended guidelines for designing Teams tabs.</span></span>
* <span data-ttu-id="9543f-199">[Créer des onglets pour les appareils mobiles](../tabs/design/tabs-mobile.md): Découvrez comment développer des onglets pour les téléphones et les tablettes.</span><span class="sxs-lookup"><span data-stu-id="9543f-199">[Build tabs for mobile](../tabs/design/tabs-mobile.md): Understand how to develop tabs for phones and tablets.</span></span>
* [<span data-ttu-id="9543f-200">Utiliser des données de teams avec l’API Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="9543f-200">Utilize Teams data with the Microsoft Graph API</span></span>](https://docs.microsoft.com/graph/teams-concept-overview)
* [<span data-ttu-id="9543f-201">Créer un onglet sans la boîte à outils</span><span class="sxs-lookup"><span data-stu-id="9543f-201">Create a tab without the toolkit</span></span>](../tabs/how-to/add-tab.md)

## <a name="next-lesson"></a><span data-ttu-id="9543f-202">Leçon suivante</span><span class="sxs-lookup"><span data-stu-id="9543f-202">Next lesson</span></span>

<span data-ttu-id="9543f-203">Vous saurez comment créer un onglet pour la collaboration.</span><span class="sxs-lookup"><span data-stu-id="9543f-203">You know how to build a tab for collaboration.</span></span> <span data-ttu-id="9543f-204">Vous souhaitez essayer de créer un autre type d’application teams ?</span><span class="sxs-lookup"><span data-stu-id="9543f-204">Want to try building a different kind of Teams app?</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9543f-205">Créer un bot</span><span class="sxs-lookup"><span data-stu-id="9543f-205">Build a bot</span></span>](../build-your-first-app/build-bot.md)
