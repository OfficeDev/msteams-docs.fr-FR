---
title: Prise en main-créer un onglet de canal et de groupe
author: heath-hamilton
description: Créez rapidement un onglet de chaîne et de groupe Microsoft teams à l’aide du kit de développement Microsoft Teams.
ms.author: lajanuar
ms.date: 10/09/2020
ms.topic: tutorial
ms.openlocfilehash: f890754cdf4ca43f39c25e3ba24fcf47b08c5a9f
ms.sourcegitcommit: d61f14053fc695bc1956bf50e83956613c19ccca
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/13/2020
ms.locfileid: "48452854"
---
# <a name="build-a-channel-and-group-tab-for-microsoft-teams"></a><span data-ttu-id="01419-103">Créer un onglet de canal et de groupe pour Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="01419-103">Build a channel and group tab for Microsoft Teams</span></span>

<span data-ttu-id="01419-104">Dans ce didacticiel, vous allez créer un *onglet de canal* de base (également appelé *onglet de groupe*), qui est une page plein écran pour un canal d’équipe ou une conversation.</span><span class="sxs-lookup"><span data-stu-id="01419-104">In this tutorial, you'll build a basic *channel tab* (also known as a *group tab*), which is a full-screen page for a team channel or chat.</span></span> <span data-ttu-id="01419-105">Contrairement à un onglet personnel, les utilisateurs peuvent configurer certains aspects de ce type d’onglet (par exemple, renommer l’onglet de sorte qu’il soit significatif pour son canal).</span><span class="sxs-lookup"><span data-stu-id="01419-105">Unlike a personal tab, users can configure some aspects of this kind of tab (for example, rename the tab so it's meaningful to their channel).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="01419-106">Votre affectation</span><span class="sxs-lookup"><span data-stu-id="01419-106">Your assignment</span></span>

<span data-ttu-id="01419-107">Il n’y a pas longtemps, votre organisation a créé un onglet teams avec des informations sur la façon de contacter des fonctions importantes (support technique, RH, etc.).</span><span class="sxs-lookup"><span data-stu-id="01419-107">Not long ago, your organization created a Teams tab with information on how to contact important functions (help desk, HR, etc.).</span></span> <span data-ttu-id="01419-108">Toutefois, étant donné que l’onglet a été inclus uniquement à des fins personnelles, chaque utilisateur doit installer l’onglet pour l’afficher et l’adoption est inférieure à celle attendue.</span><span class="sxs-lookup"><span data-stu-id="01419-108">However, since the tab was scoped only for personal use, each user must install the tab to see it and adoption is lower than expected.</span></span> <span data-ttu-id="01419-109">En d’autres termes, trop de travailleurs ne sachent toujours pas comment contacter le support technique.</span><span class="sxs-lookup"><span data-stu-id="01419-109">In other words, too many workers still don't know how to reach the help desk.</span></span>

<span data-ttu-id="01419-110">Vous pouvez faciliter la recherche de ces informations en créant un onglet de canal, ce qui vous évite de devoir installer une application.</span><span class="sxs-lookup"><span data-stu-id="01419-110">You can make this information easier to find by building a channel tab, which will remove the burden of requiring everyone to install an app.</span></span> <span data-ttu-id="01419-111">Au lieu de cela, un utilisateur peut installer l’onglet dans un canal ou une conversation pour l’ensemble du groupe.</span><span class="sxs-lookup"><span data-stu-id="01419-111">Instead, one user can install the tab in a channel or chat for the benefit of an entire group.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="01419-112">Ce que vous allez apprendre</span><span class="sxs-lookup"><span data-stu-id="01419-112">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="01419-113">Créer un projet d’application à l’aide de Microsoft teams Toolkit pour Visual Studio code</span><span class="sxs-lookup"><span data-stu-id="01419-113">Create an app project using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="01419-114">Identifier certaines des propriétés de manifeste de l’application et la génération de modèles automatique correspondant aux onglets canal et groupe</span><span class="sxs-lookup"><span data-stu-id="01419-114">Identify some of the app manifest properties and scaffolding relevant to channel and group tabs</span></span>
> * <span data-ttu-id="01419-115">Héberger une application localement</span><span class="sxs-lookup"><span data-stu-id="01419-115">Host an app locally</span></span>
> * <span data-ttu-id="01419-116">Créer un contenu de tabulation</span><span class="sxs-lookup"><span data-stu-id="01419-116">Create tab content</span></span>
> * <span data-ttu-id="01419-117">Créer du contenu pour la page de configuration d’un onglet</span><span class="sxs-lookup"><span data-stu-id="01419-117">Create content for a tab's configuration page</span></span>
> * <span data-ttu-id="01419-118">Autoriser la configuration et l’installation d’un onglet</span><span class="sxs-lookup"><span data-stu-id="01419-118">Allow a tab to be configured and installed</span></span>
> * <span data-ttu-id="01419-119">Fournir un nom d’onglet suggéré</span><span class="sxs-lookup"><span data-stu-id="01419-119">Provide a suggested tab name</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="01419-120">1. créer votre projet d’application</span><span class="sxs-lookup"><span data-stu-id="01419-120">1. Create your app project</span></span>

<span data-ttu-id="01419-121">La boîte à outils Microsoft teams vous permet de configurer le manifeste de l’application et les onglets de canal et de groupe, notamment une page de configuration de base et une page de contenu qui affiche un « Hello, World ! ».</span><span class="sxs-lookup"><span data-stu-id="01419-121">The Microsoft Teams Toolkit helps you set up the app manifest and scaffolding relevant to channel and group tabs, including a basic configuration page and content page that displays a "Hello, World!"</span></span> <span data-ttu-id="01419-122">Message.</span><span class="sxs-lookup"><span data-stu-id="01419-122">message.</span></span>

> [!TIP]
> <span data-ttu-id="01419-123">Si vous n’avez pas encore créé de projet d’application Teams, il peut s’avérer utile de suivre [ces instructions](../build-your-first-app/build-and-run.md) pour expliquer plus en détail les projets.</span><span class="sxs-lookup"><span data-stu-id="01419-123">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. Dans Visual Studio code, sélectionnez **Microsoft teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: dans la barre d’activité de gauche et choisissez **créer une nouvelle application teams**.
1. <span data-ttu-id="01419-125">Entrez un nom pour votre application Teams.</span><span class="sxs-lookup"><span data-stu-id="01419-125">Enter a name for your Teams app.</span></span> <span data-ttu-id="01419-126">(Il s’agit du nom par défaut de votre application, ainsi que du nom du répertoire du projet d’application sur votre ordinateur local.)</span><span class="sxs-lookup"><span data-stu-id="01419-126">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="01419-127">Dans l’écran **Ajouter des fonctionnalités** , **Sélectionnez l’onglet** Groupe, puis **groupe ou Team Channel**.</span><span class="sxs-lookup"><span data-stu-id="01419-127">On the **Add capabilities** screen, select **Tab** then **Group or Teams channel tab**.</span></span>
1. <span data-ttu-id="01419-128">Sélectionnez **Terminer** en bas de l’écran pour configurer votre projet.</span><span class="sxs-lookup"><span data-stu-id="01419-128">Select **Finish** at the bottom of the screen to configure your project.</span></span>  

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="01419-129">2. identifier les composants de projet d’application pertinents</span><span class="sxs-lookup"><span data-stu-id="01419-129">2. Identify relevant app project components</span></span>

<span data-ttu-id="01419-130">La plupart du manifeste de l’application et de la génération de modèles automatique sont configurés automatiquement lorsque vous créez votre projet avec le kit de outils Teams.</span><span class="sxs-lookup"><span data-stu-id="01419-130">Much of the app manifest and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="01419-131">Examinons les principaux composants de création d’un onglet de canal et de groupe.</span><span class="sxs-lookup"><span data-stu-id="01419-131">Let's look at the main components for building a channel and group tab.</span></span>

### <a name="app-manifest"></a><span data-ttu-id="01419-132">Manifeste de l’application</span><span class="sxs-lookup"><span data-stu-id="01419-132">App manifest</span></span>

<span data-ttu-id="01419-133">L’extrait de code suivant du manifeste de l’application indique [`configurableTabs`](../resources/schema/manifest-schema.md#configurabletabs) , qui inclut les propriétés et les valeurs par défaut pertinentes pour les onglets canal et groupe.</span><span class="sxs-lookup"><span data-stu-id="01419-133">The following snippet from the app manifest shows [`configurableTabs`](../resources/schema/manifest-schema.md#configurabletabs), which includes the properties and default values relevant to channel and group tabs.</span></span>

```JSON
"configurableTabs": [
    {
        "configurationUrl": "{baseUrl0}/config",
        "canUpdateConfiguration": true,
        "scopes": [
            "team",
            "groupchat"
        ]
    }
],
```

* <span data-ttu-id="01419-134">`configurationUrl`: URL hôte de votre page de configuration d’onglet (doit être HTTPs).</span><span class="sxs-lookup"><span data-stu-id="01419-134">`configurationUrl`: The host URL for your tab configuration page (must be HTTPS).</span></span>
* <span data-ttu-id="01419-135">`canUpdateConfiguration`: Si ce paramètre `true` est défini sur, les utilisateurs peuvent modifier les paramètres de tabulation, renommer l’onglet ou le supprimer d’un canal ou d’une conversation.</span><span class="sxs-lookup"><span data-stu-id="01419-135">`canUpdateConfiguration`: If set to `true`, users can change tab settings, rename the tab, or remove it from a channel or chat.</span></span>
* <span data-ttu-id="01419-136">`scopes`: Spécifie si les utilisateurs peuvent installer l’application dans Channels ( `team` ) et les conversations ( `groupchat` ).</span><span class="sxs-lookup"><span data-stu-id="01419-136">`scopes`: Specifies if users can install the app in channels (`team`) and chats (`groupchat`).</span></span> <span data-ttu-id="01419-137">Au moins une valeur est requise.</span><span class="sxs-lookup"><span data-stu-id="01419-137">At least one value is required.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="01419-138">Génération de modèles automatique d’application</span><span class="sxs-lookup"><span data-stu-id="01419-138">App scaffolding</span></span>

<span data-ttu-id="01419-139">Le échafaudage de l’application fournit un `TabConfig.js` fichier, situé dans le `src/components` Répertoire de votre projet, pour afficher la page de configuration de votre onglet (en savoir plus sur cela prochainement).</span><span class="sxs-lookup"><span data-stu-id="01419-139">The app scaffolding provides a `TabConfig.js` file, located in the `src/components` directory of your project, for rendering your tab's configuration page (more on this soon).</span></span>

## <a name="3-run-your-app"></a><span data-ttu-id="01419-140">3. exécuter votre application</span><span class="sxs-lookup"><span data-stu-id="01419-140">3. Run your app</span></span>

<span data-ttu-id="01419-141">Pour des raisons de temps, vous allez créer et exécuter votre application localement.</span><span class="sxs-lookup"><span data-stu-id="01419-141">In the interest of time, you'll build and run your app locally.</span></span>

1. <span data-ttu-id="01419-142">Dans un terminal, accédez au répertoire racine de votre projet d’application et exécutez `npm install` .</span><span class="sxs-lookup"><span data-stu-id="01419-142">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="01419-143">Exécuter `npm start` .</span><span class="sxs-lookup"><span data-stu-id="01419-143">Run `npm start`.</span></span>

<span data-ttu-id="01419-144">Une fois terminé, une **compilation est effectuée.**</span><span class="sxs-lookup"><span data-stu-id="01419-144">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="01419-145">message dans le terminal.</span><span class="sxs-lookup"><span data-stu-id="01419-145">message in the terminal.</span></span>

## <a name="4-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="01419-146">4. configurer un tunnel sécurisé pour votre application</span><span class="sxs-lookup"><span data-stu-id="01419-146">4. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="01419-147">À des fins de test, nous allons héberger votre onglet sur un serveur Web local (port 3000).</span><span class="sxs-lookup"><span data-stu-id="01419-147">For testing purposes, let's host your tab on a local web server (port 3000).</span></span>

1. <span data-ttu-id="01419-148">Dans un terminal, exécutez `ngrok http 3000` .</span><span class="sxs-lookup"><span data-stu-id="01419-148">In a terminal, run `ngrok http 3000`.</span></span>
1. <span data-ttu-id="01419-149">Copiez l’URL HTTPs que vous avez fournie.</span><span class="sxs-lookup"><span data-stu-id="01419-149">Copy the HTTPS URL you're provided.</span></span>
1. <span data-ttu-id="01419-150">Dans votre `.publish` répertoire, ouvrez `Development.env` .</span><span class="sxs-lookup"><span data-stu-id="01419-150">In your `.publish` directory, open `Development.env`.</span></span>
1. <span data-ttu-id="01419-151">Remplacez la `baseUrl0` valeur par l’URL copiée.</span><span class="sxs-lookup"><span data-stu-id="01419-151">Replace the `baseUrl0` value with the copied URL.</span></span> <span data-ttu-id="01419-152">(Par exemple, remplacez `baseUrl0=http://localhost:3000` par `baseUrl0=https://85528b2b3ca5.ngrok.io` .)</span><span class="sxs-lookup"><span data-stu-id="01419-152">(For example, change `baseUrl0=http://localhost:3000` to `baseUrl0=https://85528b2b3ca5.ngrok.io`.)</span></span>

<span data-ttu-id="01419-153">Le manifeste de votre application pointe vers l’emplacement où vous hébergez l’onglet.</span><span class="sxs-lookup"><span data-stu-id="01419-153">Your app manifest is pointing to where you're hosting the tab.</span></span>

## <a name="5-customize-your-tab-content-page"></a><span data-ttu-id="01419-154">5. personnaliser votre page de contenu d’onglet</span><span class="sxs-lookup"><span data-stu-id="01419-154">5. Customize your tab content page</span></span>

<span data-ttu-id="01419-155">Ouvrez le manifeste de l’application ( `manifest.json` ) dans le `.publish` répertoire et définissez les propriétés suivantes dans [`staticTabs`](../resources/schema/manifest-schema.md#statictabs) , qui définit la page de contenu de votre onglet.</span><span class="sxs-lookup"><span data-stu-id="01419-155">Open the app manifest (`manifest.json`) in the `.publish` directory and set the following properties in [`staticTabs`](../resources/schema/manifest-schema.md#statictabs), which defines your tab's content page.</span></span>

```JSON
"staticTabs": [
    {
        "entityId": "index",
        "name": "My Contacts",
        "contentUrl": "{baseUrl0}/tab",
        "scopes": [ "personal" ]
    }
],
```

<span data-ttu-id="01419-156">Copiez et mettez à jour l’extrait de code suivant avec des informations pertinentes pour votre organisation ou, pour des raisons de temps, utilisez le code tel quel.</span><span class="sxs-lookup"><span data-stu-id="01419-156">Copy and update the following snippet with information that's relevant to your organization or, for the sake of time, use the code as is.</span></span>

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

<span data-ttu-id="01419-157">Accédez au `src/components` répertoire et ouvrez `Tab.js` .</span><span class="sxs-lookup"><span data-stu-id="01419-157">Go to the `src/components` directory and open `Tab.js`.</span></span> <span data-ttu-id="01419-158">Recherchez la `render()` fonction et collez votre contenu dans `return()` (comme illustré).</span><span class="sxs-lookup"><span data-stu-id="01419-158">Locate the `render()` function and paste your content inside `return()` (as shown).</span></span>

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

<span data-ttu-id="01419-159">Ajoutez la règle suivante pour `App.css` que les liens électroniques soient plus faciles à lire quel que soit le thème utilisé.</span><span class="sxs-lookup"><span data-stu-id="01419-159">Add the following rule to `App.css` so the email links are easier to read no matter which theme is used.</span></span>

```CSS
a {
  color: inherit;
}
```

## <a name="6-create-your-tab-configuration-page"></a><span data-ttu-id="01419-160">6. créer votre page de configuration d’onglet</span><span class="sxs-lookup"><span data-stu-id="01419-160">6. Create your tab configuration page</span></span>

<span data-ttu-id="01419-161">Chaque onglet d’un canal ou d’une conversation comporte une page de configuration, modale avec au moins une option d’installation qui s’affiche lorsque les utilisateurs installent votre application.</span><span class="sxs-lookup"><span data-stu-id="01419-161">Every tab in a channel or chat has a configuration page, a modal with at least one setup option that displays when users install your app.</span></span> <span data-ttu-id="01419-162">La page Configuration par défaut demande à l’utilisateur s’il souhaite avertir le canal ou la conversation lorsque l’onglet est installé.</span><span class="sxs-lookup"><span data-stu-id="01419-162">The configuration page by default asks users if they want to notify the channel or chat when the tab is installed.</span></span>

<span data-ttu-id="01419-163">Ajoutez du contenu à votre page de configuration.</span><span class="sxs-lookup"><span data-stu-id="01419-163">Add some content to your configuration page.</span></span> <span data-ttu-id="01419-164">Accédez au répertoire de votre projet `src/components` , ouvrez-le `TabConfig.js` et insérez du contenu dans `return()` (comme illustré).</span><span class="sxs-lookup"><span data-stu-id="01419-164">Go to your project's `src/components` directory, open `TabConfig.js`, and insert some content inside `return()` (as shown).</span></span>

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
> <span data-ttu-id="01419-165">Au minimum, fournissez des informations succinctes sur votre application sur cette page, car il peut s’agir de la première fois que les utilisateurs en apprennent à le faire.</span><span class="sxs-lookup"><span data-stu-id="01419-165">At minimum, provide some brief information about your app on this page since this may be the first time users are learning about it.</span></span> <span data-ttu-id="01419-166">Vous pouvez également inclure des options de configuration personnalisées ou un [flux de travail d’authentification](../tabs/how-to/authentication/auth-aad-sso.md), qui est courant sur les pages de configuration d’onglet.</span><span class="sxs-lookup"><span data-stu-id="01419-166">You also could include custom configuration options or an [authentication workflow](../tabs/how-to/authentication/auth-aad-sso.md), which is common on tab configuration pages.</span></span>

## <a name="7-allow-the-tab-to-be-configured-and-installed"></a><span data-ttu-id="01419-167">7. autoriser la configuration et l’installation de l’onglet</span><span class="sxs-lookup"><span data-stu-id="01419-167">7. Allow the tab to be configured and installed</span></span>

<span data-ttu-id="01419-168">Pour que les utilisateurs puissent configurer et installer correctement l’onglet, vous devez ajouter l' [URL d’hôte sécurisé que vous avez définie](#4-set-up-a-secure-tunnel-to-your-app) au composant de page de configuration.</span><span class="sxs-lookup"><span data-stu-id="01419-168">For users to successfully configure and install the tab, you must add the [secure host URL you set up](#4-set-up-a-secure-tunnel-to-your-app) to the configuration page component.</span></span>

<span data-ttu-id="01419-169">Accédez à `TabConfig.js` et recherchez `microsoftTeams.settings.setSettings` .</span><span class="sxs-lookup"><span data-stu-id="01419-169">Go to `TabConfig.js` and locate `microsoftTeams.settings.setSettings`.</span></span> <span data-ttu-id="01419-170">Pour `"contentUrl"` , remplacez la `localhost:3000` partie de l’URL par le domaine dans lequel vous hébergez le contenu de l’onglet (comme illustré ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="01419-170">For `"contentUrl"`, replace the `localhost:3000` part of the URL with the domain where you're hosting the tab content (as shown).</span></span>

```JavaScript
microsoftTeams.settings.setSettings({
  "contentUrl": "https://<MY_HOST_DOMAIN>/tab"
});
```

<span data-ttu-id="01419-171">Assurez-vous également que `microsoftTeams.settings.setValidityState(true);` .</span><span class="sxs-lookup"><span data-stu-id="01419-171">Also, make sure that `microsoftTeams.settings.setValidityState(true);`.</span></span> <span data-ttu-id="01419-172">C’est par défaut, mais si ce paramètre est défini sur `false` , le bouton **Enregistrer** est désactivé sur la page de configuration.</span><span class="sxs-lookup"><span data-stu-id="01419-172">It is by default, but if set to `false`, the **Save** button is disabled on the configuration page.</span></span>

## <a name="8-provide-a-suggested-tab-name"></a><span data-ttu-id="01419-173">8. fournir un nom d’onglet suggéré</span><span class="sxs-lookup"><span data-stu-id="01419-173">8. Provide a suggested tab name</span></span>

<span data-ttu-id="01419-174">Lorsque vous installez un onglet pour une utilisation personnelle, le nom complet est la `name` propriété dans la `staticTabs` partie du manifeste de l’application (par exemple, **mes contacts**).</span><span class="sxs-lookup"><span data-stu-id="01419-174">When you install a tab for personal use, the display name is the `name` property in the `staticTabs` portion of the app manifest (for example, **My Contacts**).</span></span> <span data-ttu-id="01419-175">Lorsque vous installez un onglet canal, le nom de l’application s’affiche par défaut (par exemple, **First-App**).</span><span class="sxs-lookup"><span data-stu-id="01419-175">When you install a channel tab, by default the app name displays (for example, **first-app**).</span></span>

<span data-ttu-id="01419-176">Cela peut être approprié en fonction de ce que vous appelez votre application, mais vous souhaiterez peut-être attribuer un nom plus évocateur dans le contexte de la collaboration de groupe (par exemple, **contacts d’équipe**).</span><span class="sxs-lookup"><span data-stu-id="01419-176">This may be fine depending on what you call your app, but you may want to provide a name that makes more sense in the context of group collaboration (for example, **Team Contacts**).</span></span>

<span data-ttu-id="01419-177">Dans `TabConfig.js` , revenez à `microsoftTeams.settings.setSettings` .</span><span class="sxs-lookup"><span data-stu-id="01419-177">In `TabConfig.js`, go back to `microsoftTeams.settings.setSettings`.</span></span> <span data-ttu-id="01419-178">Ajoutez la `suggestedDisplayName` propriété avec le nom de l’onglet que vous souhaitez afficher par défaut (comme illustré).</span><span class="sxs-lookup"><span data-stu-id="01419-178">Add the `suggestedDisplayName` property with the tab name you want to display by default (as shown).</span></span> <span data-ttu-id="01419-179">Utilisez le nom fourni ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="01419-179">Use the provided name or create your own.</span></span> <span data-ttu-id="01419-180">N’oubliez pas que dans le manifeste, vous autorisez les utilisateurs à modifier le nom s’ils le souhaitent.</span><span class="sxs-lookup"><span data-stu-id="01419-180">Remember, in the manifest you're allowing users to change the name if they want.</span></span>

```JavaScript
microsoftTeams.settings.setSettings({
  "contentUrl": "https://<MY_HOST_DOMAIN>/tab",
  "suggestedDisplayName": "Team Contacts"
});
```

## <a name="9-view-the-tab"></a><span data-ttu-id="01419-181">9. afficher l’onglet</span><span class="sxs-lookup"><span data-stu-id="01419-181">9. View the tab</span></span>

<span data-ttu-id="01419-182">Pour afficher les pages de configuration et de contenu de votre onglet, vous devez l’installer dans un canal ou une conversation.</span><span class="sxs-lookup"><span data-stu-id="01419-182">To see your tab's configuration and content pages, you must install it in a channel or chat.</span></span>

1. <span data-ttu-id="01419-183">Dans le client Teams, sélectionnez **applications**.</span><span class="sxs-lookup"><span data-stu-id="01419-183">In the Teams client, select **Apps**.</span></span>
1. <span data-ttu-id="01419-184">Sélectionnez **Télécharger une application personnalisée** et choisissez l’application `Development.zip` .</span><span class="sxs-lookup"><span data-stu-id="01419-184">Select **Upload a custom app** and choose your app's `Development.zip`.</span></span>
1. <span data-ttu-id="01419-185">Sélectionnez **Ajouter à une équipe** ou **Ajouter à une conversation** , puis recherchez un canal ou une conversation que vous pouvez utiliser à des fins de test.</span><span class="sxs-lookup"><span data-stu-id="01419-185">Choose **Add to a team** or **Add to a chat** and locate a channel or chat you can use for testing.</span></span>
1. <span data-ttu-id="01419-186">Sélectionnez **configurer un onglet**. La page Configuration s’affiche.</span><span class="sxs-lookup"><span data-stu-id="01419-186">Select **Set up a tab**. The configuration page displays.</span></span><br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="Capture d’écran de la page de configuration de l’onglet canal.":::
1. <span data-ttu-id="01419-188">Sélectionnez **Enregistrer** pour configurer l’onglet. Le contenu s’affiche.</span><span class="sxs-lookup"><span data-stu-id="01419-188">Select **Save** to configure the tab. The content displays.</span></span><br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="Capture d’écran de la page de configuration de l’onglet canal.":::

## <a name="well-done"></a><span data-ttu-id="01419-190">Bien jouer</span><span class="sxs-lookup"><span data-stu-id="01419-190">Well done</span></span>

<span data-ttu-id="01419-191">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="01419-191">Congratulations!</span></span> <span data-ttu-id="01419-192">Vous disposez d’une application teams avec un onglet qui permet d’afficher du contenu utile dans les canaux et les conversations.</span><span class="sxs-lookup"><span data-stu-id="01419-192">You have a Teams app with a tab for displaying useful content in channels and chats.</span></span>

## <a name="learn-more"></a><span data-ttu-id="01419-193">Si vous souhaitez en savoir plus</span><span class="sxs-lookup"><span data-stu-id="01419-193">Learn more</span></span>

* <span data-ttu-id="01419-194">[Authentifier les utilisateurs avec l’authentification](../tabs/how-to/authentication/auth-aad-sso.md)unique : Si vous souhaitez uniquement que les utilisateurs autorisés visualisent votre onglet, configurez l’authentification unique (SSO) via Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="01419-194">[Authenticate tab users with SSO](../tabs/how-to/authentication/auth-aad-sso.md): If you only want authorized users viewing your tab, set up single sign-on (SSO) through Azure Active Directory (AD).</span></span>
* <span data-ttu-id="01419-195">[Incorporer du contenu à partir d’une application Web ou d’une page Web existante](../tabs/how-to/add-tab.md#tab-requirements): nous vous avons expliqué comment créer du contenu pour un onglet personnel, mais vous pouvez également charger du contenu à partir d’une URL externe.</span><span class="sxs-lookup"><span data-stu-id="01419-195">[Embed content from an existing web app or webpage](../tabs/how-to/add-tab.md#tab-requirements): We showed you how to create new content for a personal tab, but you can also load content from an external URL.</span></span>
* <span data-ttu-id="01419-196">[Créez une expérience transparente pour votre onglet](../tabs/design/tabs.md): consultez les instructions recommandées pour la création d’onglets Teams.</span><span class="sxs-lookup"><span data-stu-id="01419-196">[Create a seamless experience for your tab](../tabs/design/tabs.md): See the recommended guidelines for designing Teams tabs.</span></span>
* <span data-ttu-id="01419-197">[Créer des onglets pour les appareils mobiles](../tabs/design/tabs-mobile.md): Découvrez comment développer des onglets pour les téléphones et les tablettes.</span><span class="sxs-lookup"><span data-stu-id="01419-197">[Build tabs for mobile](../tabs/design/tabs-mobile.md): Understand how to develop tabs for phones and tablets.</span></span>
* [<span data-ttu-id="01419-198">Créer un onglet sans la boîte à outils</span><span class="sxs-lookup"><span data-stu-id="01419-198">Create a tab without the toolkit</span></span>](../tabs/how-to/add-tab.md)

## <a name="next-lesson"></a><span data-ttu-id="01419-199">Leçon suivante</span><span class="sxs-lookup"><span data-stu-id="01419-199">Next lesson</span></span>

<span data-ttu-id="01419-200">Vous saurez comment créer un onglet pour la collaboration.</span><span class="sxs-lookup"><span data-stu-id="01419-200">You know how to build a tab for collaboration.</span></span> <span data-ttu-id="01419-201">Vous souhaitez essayer de créer un autre type d’application teams ?</span><span class="sxs-lookup"><span data-stu-id="01419-201">Want to try building a different kind of Teams app?</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="01419-202">Créer un bot</span><span class="sxs-lookup"><span data-stu-id="01419-202">Build a bot</span></span>](../build-your-first-app/build-bot.md)
