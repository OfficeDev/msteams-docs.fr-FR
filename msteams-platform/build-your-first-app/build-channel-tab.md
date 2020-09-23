---
author: heath-hamilton
description: Découvrez comment créer un onglet de canal pour votre première application Microsoft Teams.
ms.author: lajanuar
ms.date: 09/22/2020
ms.topic: tutorial
title: Créer un onglet de canal teams
ms.openlocfilehash: d0846c3af23fd9df6013f989e9f455f711d05a5f
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "48210254"
---
# <a name="build-a-teams-channel-tab"></a><span data-ttu-id="54a63-103">Créer un onglet de canal teams</span><span class="sxs-lookup"><span data-stu-id="54a63-103">Build a Teams channel tab</span></span>

<span data-ttu-id="54a63-104">Dans ce didacticiel, vous allez créer un *onglet de canal*de base, une page de contenu plein écran pour un canal d’équipe ou une conversation.</span><span class="sxs-lookup"><span data-stu-id="54a63-104">In this tutorial, you'll build a basic *channel tab*, a full-screen content page for a team channel or chat.</span></span> <span data-ttu-id="54a63-105">Contrairement à un onglet personnel, les utilisateurs peuvent configurer certains aspects d’un onglet de canal (par exemple, renommer l’onglet de sorte qu’il soit significatif pour le canal).</span><span class="sxs-lookup"><span data-stu-id="54a63-105">Unlike a personal tab, users can configure some aspects of a channel tab (for example, rename the tab so it's meaningful to their channel).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="54a63-106">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="54a63-106">Before you begin</span></span>

<span data-ttu-id="54a63-107">Vous avez besoin d’une application de base en cours d’exécution pour commencer.</span><span class="sxs-lookup"><span data-stu-id="54a63-107">You need a basic running app to get started.</span></span> <span data-ttu-id="54a63-108">Si vous n’en avez pas, suivez les [instructions créer et exécuter les premières applications de teams](../build-your-first-app/build-and-run.md).</span><span class="sxs-lookup"><span data-stu-id="54a63-108">If you don't have one, follow the [build and run your Teams first app instructions](../build-your-first-app/build-and-run.md).</span></span> <span data-ttu-id="54a63-109">Lorsque vous créez votre projet d’application, choisissez uniquement l’option de l' **onglet canal groupe ou teams** .</span><span class="sxs-lookup"><span data-stu-id="54a63-109">When you create your app project, choose only the **Group or Teams channel tab** option.</span></span>

## <a name="your-assignment"></a><span data-ttu-id="54a63-110">Votre affectation</span><span class="sxs-lookup"><span data-stu-id="54a63-110">Your assignment</span></span>

<span data-ttu-id="54a63-111">Il n’y a pas longtemps, votre organisation a créé un onglet teams avec des informations sur la façon de contacter des fonctions importantes (support technique, RH, etc.).</span><span class="sxs-lookup"><span data-stu-id="54a63-111">Not long ago, your organization created a Teams tab with information on how to contact important functions (help desk, HR, etc.).</span></span> <span data-ttu-id="54a63-112">Toutefois, étant donné que l’onglet a été inclus uniquement à des fins personnelles, chaque utilisateur doit installer l’onglet pour l’afficher et l’adoption est inférieure à celle attendue.</span><span class="sxs-lookup"><span data-stu-id="54a63-112">However, since the tab was scoped only for personal use, each user must install the tab to see it and adoption is lower than expected.</span></span> <span data-ttu-id="54a63-113">En d’autres termes, trop de travailleurs ne sachent toujours pas comment contacter le support technique.</span><span class="sxs-lookup"><span data-stu-id="54a63-113">In other words, too many workers still don't know how to reach the help desk.</span></span>

<span data-ttu-id="54a63-114">Vous pouvez faciliter la recherche de ces informations en créant un onglet de canal, ce qui vous évite de devoir installer une application.</span><span class="sxs-lookup"><span data-stu-id="54a63-114">You can make this information easier to find by building a channel tab, which will remove the burden of requiring everyone to install an app.</span></span> <span data-ttu-id="54a63-115">Au lieu de cela, un utilisateur peut installer l’onglet dans un canal ou une conversation pour l’ensemble du groupe.</span><span class="sxs-lookup"><span data-stu-id="54a63-115">Instead, one user can install the tab in a channel or chat for the benefit of an entire group.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="54a63-116">Ce que vous allez apprendre</span><span class="sxs-lookup"><span data-stu-id="54a63-116">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="54a63-117">Identifier certaines des propriétés de manifeste de l’application et la structure correspondant aux onglets de canal</span><span class="sxs-lookup"><span data-stu-id="54a63-117">Identify some of the app manifest properties and scaffolding relevant to channel tabs</span></span>
> * <span data-ttu-id="54a63-118">Créer un contenu de tabulation</span><span class="sxs-lookup"><span data-stu-id="54a63-118">Create tab content</span></span>
> * <span data-ttu-id="54a63-119">Créer du contenu pour la page de configuration d’un onglet</span><span class="sxs-lookup"><span data-stu-id="54a63-119">Create content for a tab's configuration page</span></span>
> * <span data-ttu-id="54a63-120">Autoriser la configuration et l’installation d’un onglet</span><span class="sxs-lookup"><span data-stu-id="54a63-120">Allow a tab to be configured and installed</span></span>
> * <span data-ttu-id="54a63-121">Fournir un nom d’onglet suggéré</span><span class="sxs-lookup"><span data-stu-id="54a63-121">Provide a suggested tab name</span></span>

## <a name="identify-relevant-app-project-components"></a><span data-ttu-id="54a63-122">Identifier les composants de projet d’application pertinents</span><span class="sxs-lookup"><span data-stu-id="54a63-122">Identify relevant app project components</span></span>

<span data-ttu-id="54a63-123">La plupart du manifeste de l’application et de la génération de modèles automatique sont configurés automatiquement lorsque vous créez votre projet avec le kit de outils Teams.</span><span class="sxs-lookup"><span data-stu-id="54a63-123">Much of the app manifest and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="54a63-124">Examinons les principaux composants de la création d’un onglet de canal.</span><span class="sxs-lookup"><span data-stu-id="54a63-124">Let's look at the main components for building a channel tab.</span></span>

### <a name="app-manifest"></a><span data-ttu-id="54a63-125">Manifeste de l’application</span><span class="sxs-lookup"><span data-stu-id="54a63-125">App manifest</span></span>

<span data-ttu-id="54a63-126">L’extrait de code suivant du manifeste de l’application indique [`configurableTabs`](../resources/schema/manifest-schema.md#configurabletabs) , qui inclut les propriétés et les valeurs par défaut pertinentes pour les onglets de canal.</span><span class="sxs-lookup"><span data-stu-id="54a63-126">The following snippet from the app manifest shows [`configurableTabs`](../resources/schema/manifest-schema.md#configurabletabs), which includes the properties and default values relevant to channel tabs.</span></span>

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

* <span data-ttu-id="54a63-127">`configurationUrl`: URL hôte de votre page de configuration d’onglet (doit être HTTPs).</span><span class="sxs-lookup"><span data-stu-id="54a63-127">`configurationUrl`: The host URL for your tab configuration page (must be HTTPS).</span></span>
* <span data-ttu-id="54a63-128">`canUpdateConfiguration`: Si ce paramètre `true` est défini sur, les utilisateurs peuvent modifier les paramètres de tabulation, renommer l’onglet ou le supprimer d’un canal ou d’une conversation.</span><span class="sxs-lookup"><span data-stu-id="54a63-128">`canUpdateConfiguration`: If set to `true`, users can change tab settings, rename the tab, or remove it from a channel or chat.</span></span>
* <span data-ttu-id="54a63-129">`scopes`: Spécifie si les utilisateurs peuvent installer l’application dans Channels ( `team` ) et les conversations ( `groupchat` ).</span><span class="sxs-lookup"><span data-stu-id="54a63-129">`scopes`: Specifies if users can install the app in channels (`team`) and chats (`groupchat`).</span></span> <span data-ttu-id="54a63-130">Au moins une valeur est requise.</span><span class="sxs-lookup"><span data-stu-id="54a63-130">At least one value is required.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="54a63-131">Génération de modèles automatique d’application</span><span class="sxs-lookup"><span data-stu-id="54a63-131">App scaffolding</span></span>

<span data-ttu-id="54a63-132">Le échafaudage de l’application fournit un `TabConfig.js` fichier, situé dans le `src/components` Répertoire de votre projet, pour afficher la page de configuration de votre onglet (en savoir plus sur cela prochainement).</span><span class="sxs-lookup"><span data-stu-id="54a63-132">The app scaffolding provides a `TabConfig.js` file, located in the `src/components` directory of your project, for rendering your tab's configuration page (more on this soon).</span></span>

## <a name="create-your-tab-content"></a><span data-ttu-id="54a63-133">Créer le contenu de votre onglet</span><span class="sxs-lookup"><span data-stu-id="54a63-133">Create your tab content</span></span>

<span data-ttu-id="54a63-134">Ouvrez le manifeste de l’application ( `manifest.json` ) dans le `.publish` répertoire et définissez les propriétés suivantes dans [`staticTabs`](../resources/schema/manifest-schema.md#statictabs) , qui définit la page de contenu de votre onglet.</span><span class="sxs-lookup"><span data-stu-id="54a63-134">Open the app manifest (`manifest.json`) in the `.publish` directory and set the following properties in [`staticTabs`](../resources/schema/manifest-schema.md#statictabs), which defines your tab's content page.</span></span>

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

<span data-ttu-id="54a63-135">Copiez et mettez à jour l’extrait de code suivant avec des informations pertinentes pour votre organisation ou, pour des raisons de temps, utilisez le code tel quel.</span><span class="sxs-lookup"><span data-stu-id="54a63-135">Copy and update the following snippet with information that's relevant to your organization or, for the sake of time, use the code as is.</span></span>

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

<span data-ttu-id="54a63-136">Accédez au `src/components` répertoire et ouvrez `Tab.js` .</span><span class="sxs-lookup"><span data-stu-id="54a63-136">Go to the `src/components` directory and open `Tab.js`.</span></span> <span data-ttu-id="54a63-137">Recherchez la `render()` fonction et collez votre contenu dans `return()` (comme illustré).</span><span class="sxs-lookup"><span data-stu-id="54a63-137">Locate the `render()` function and paste your content inside `return()` (as shown).</span></span>

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

<span data-ttu-id="54a63-138">Ajoutez la règle suivante pour `App.css` que les liens électroniques soient plus faciles à lire quel que soit le thème utilisé.</span><span class="sxs-lookup"><span data-stu-id="54a63-138">Add the following rule to `App.css` so the email links are easier to read no matter which theme is used.</span></span>

```CSS
a {
  color: inherit;
}
```

## <a name="create-your-tab-configuration-page"></a><span data-ttu-id="54a63-139">Créer votre page de configuration d’onglet</span><span class="sxs-lookup"><span data-stu-id="54a63-139">Create your tab configuration page</span></span>

<span data-ttu-id="54a63-140">Chaque onglet de canal comporte une page de configuration, modale avec au moins une option d’installation qui s’affiche lors de l’installation de l’application.</span><span class="sxs-lookup"><span data-stu-id="54a63-140">Every channel tab has a configuration page, a modal with at least one setup option that displays when installing the app.</span></span> <span data-ttu-id="54a63-141">La page Configuration par défaut demande à l’utilisateur s’il souhaite avertir le canal ou la conversation lorsque l’onglet est installé.</span><span class="sxs-lookup"><span data-stu-id="54a63-141">The configuration page by default asks users if they want to notify the channel or chat when the tab is installed.</span></span>

<span data-ttu-id="54a63-142">Ajoutez du contenu à votre page de configuration.</span><span class="sxs-lookup"><span data-stu-id="54a63-142">Add some content to your configuration page.</span></span> <span data-ttu-id="54a63-143">Accédez au répertoire de votre projet `src/components` , ouvrez-le `TabConfig.js` et insérez du contenu dans `return()` (comme illustré).</span><span class="sxs-lookup"><span data-stu-id="54a63-143">Go to your project's `src/components` directory, open `TabConfig.js`, and insert some content inside `return()` (as shown).</span></span>

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
> <span data-ttu-id="54a63-144">Au minimum, fournissez des informations succinctes sur votre application sur cette page, car il peut s’agir de la première fois que les utilisateurs en apprennent à le faire.</span><span class="sxs-lookup"><span data-stu-id="54a63-144">At minimum, provide some brief information about your app on this page since this may be the first time users are learning about it.</span></span> <span data-ttu-id="54a63-145">Vous pouvez également inclure des options de configuration personnalisées ou un [flux de travail d’authentification](../tabs/how-to/authentication/auth-aad-sso.md), qui est courant sur les pages de configuration d’onglet.</span><span class="sxs-lookup"><span data-stu-id="54a63-145">You also could include custom configuration options or an [authentication workflow](../tabs/how-to/authentication/auth-aad-sso.md), which is common on tab configuration pages.</span></span>

## <a name="allow-the-tab-to-be-configured-and-installed"></a><span data-ttu-id="54a63-146">Autoriser la configuration et l’installation de l’onglet</span><span class="sxs-lookup"><span data-stu-id="54a63-146">Allow the tab to be configured and installed</span></span>

<span data-ttu-id="54a63-147">Pour que les utilisateurs puissent configurer et installer correctement l’onglet canal, vous devez ajouter l’URL d’hôte que vous avez configurée lors de la [création et de l’exécution de votre première application](../build-your-first-app/build-and-run.md) sur le composant de page de configuration.</span><span class="sxs-lookup"><span data-stu-id="54a63-147">For users to successfully configure and install the channel tab, you must add the host URL you set up when [creating and running your first app](../build-your-first-app/build-and-run.md) to the configuration page component.</span></span>

<span data-ttu-id="54a63-148">Accédez à `TabConfig.js` et recherchez `microsoftTeams.settings.setSettings` .</span><span class="sxs-lookup"><span data-stu-id="54a63-148">Go to `TabConfig.js` and locate `microsoftTeams.settings.setSettings`.</span></span> <span data-ttu-id="54a63-149">Pour `"contentUrl"` , remplacez la `localhost:3000` partie de l’URL par le domaine dans lequel vous hébergez le contenu de l’onglet (comme illustré ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="54a63-149">For `"contentUrl"`, replace the `localhost:3000` part of the URL with the domain where you're hosting the tab content (as shown).</span></span>

```JavaScript
microsoftTeams.settings.setSettings({
  "contentUrl": "https://<MY_HOST_DOMAIN>/tab"
});
```

<span data-ttu-id="54a63-150">Assurez-vous également que `microsoftTeams.settings.setValidityState(true);` .</span><span class="sxs-lookup"><span data-stu-id="54a63-150">Also, make sure that `microsoftTeams.settings.setValidityState(true);`.</span></span> <span data-ttu-id="54a63-151">C’est par défaut, mais si ce paramètre est défini sur `false` , le bouton **Enregistrer** est désactivé sur la page de configuration.</span><span class="sxs-lookup"><span data-stu-id="54a63-151">It is by default, but if set to `false`, the **Save** button is disabled on the configuration page.</span></span>

## <a name="provide-a-suggested-tab-name"></a><span data-ttu-id="54a63-152">Fournir un nom d’onglet suggéré</span><span class="sxs-lookup"><span data-stu-id="54a63-152">Provide a suggested tab name</span></span>

<span data-ttu-id="54a63-153">Lorsque vous installez un onglet pour une utilisation personnelle, le nom d’affichage est la `name` propriété dans la `staticTabs` partie du manifeste de l’application (par exemple, **mes contacts**).</span><span class="sxs-lookup"><span data-stu-id="54a63-153">When you install a tab for personal use, the display name is the `name` property in the `staticTabs` portion of of the app manifest (for example, **My Contacts**).</span></span> <span data-ttu-id="54a63-154">Lorsque vous installez un onglet canal, le nom de l’application s’affiche par défaut (par exemple, **First-App**).</span><span class="sxs-lookup"><span data-stu-id="54a63-154">When you install a channel tab, by default the app name displays (for example, **first-app**).</span></span>

<span data-ttu-id="54a63-155">Cela peut être approprié en fonction de ce que vous appelez votre application, mais vous souhaiterez peut-être attribuer un nom plus évocateur dans le contexte de la collaboration de groupe (par exemple, **contacts d’équipe**).</span><span class="sxs-lookup"><span data-stu-id="54a63-155">This may be fine depending on what you call your app, but you may want to provide a name that makes more sense in the context of group collaboration (for example, **Team Contacts**).</span></span>

<span data-ttu-id="54a63-156">Dans `TabConfig.js` , revenez à `microsoftTeams.settings.setSettings` .</span><span class="sxs-lookup"><span data-stu-id="54a63-156">In `TabConfig.js`, go back to `microsoftTeams.settings.setSettings`.</span></span> <span data-ttu-id="54a63-157">Ajoutez la `suggestedDisplayName` propriété avec le nom de l’onglet que vous souhaitez afficher par défaut (comme illustré).</span><span class="sxs-lookup"><span data-stu-id="54a63-157">Add the `suggestedDisplayName` property with the tab name you want to display by default (as shown).</span></span> <span data-ttu-id="54a63-158">Utilisez le nom fourni ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="54a63-158">Use the provided name or create your own.</span></span> <span data-ttu-id="54a63-159">N’oubliez pas que dans le manifeste, vous autorisez les utilisateurs à modifier le nom s’ils le souhaitent.</span><span class="sxs-lookup"><span data-stu-id="54a63-159">Remember, in the manifest you're allowing users to change the name if they want.</span></span>

```JavaScript
microsoftTeams.settings.setSettings({
  "contentUrl": "https://<MY_HOST_DOMAIN>/tab",
  "suggestedDisplayName": "Team Contacts"
});
```

## <a name="view-the-channel-tab"></a><span data-ttu-id="54a63-160">Affichage de l’onglet canal</span><span class="sxs-lookup"><span data-stu-id="54a63-160">View the channel tab</span></span>

<span data-ttu-id="54a63-161">Pour afficher les pages de configuration et de contenu de l’onglet canal, vous devez l’installer dans un canal ou une conversation.</span><span class="sxs-lookup"><span data-stu-id="54a63-161">To see your channel tab's configuration and content pages, you must install it in a channel or chat.</span></span>

1. <span data-ttu-id="54a63-162">Dans le client Teams, sélectionnez **applications**.</span><span class="sxs-lookup"><span data-stu-id="54a63-162">In the Teams client, select **Apps**.</span></span>
1. <span data-ttu-id="54a63-163">Sélectionnez **Télécharger une application personnalisée** et choisissez l’application `Development.zip` .</span><span class="sxs-lookup"><span data-stu-id="54a63-163">Select **Upload a custom app** and choose your app's `Development.zip`.</span></span>
1. <span data-ttu-id="54a63-164">Sélectionnez **Ajouter à une équipe** ou **Ajouter à une conversation** , puis recherchez un canal ou une conversation que vous pouvez utiliser à des fins de test.</span><span class="sxs-lookup"><span data-stu-id="54a63-164">Choose **Add to a team** or **Add to a chat** and locate a channel or chat you can use for testing.</span></span>
1. <span data-ttu-id="54a63-165">Sélectionnez **configurer un onglet**. La page Configuration s’affiche.</span><span class="sxs-lookup"><span data-stu-id="54a63-165">Select **Set up a tab**. The configuration page displays.</span></span><br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="Capture d’écran de la page de configuration de l’onglet canal.":::
1. <span data-ttu-id="54a63-167">Sélectionnez **Enregistrer** pour configurer l’onglet. Le contenu s’affiche.</span><span class="sxs-lookup"><span data-stu-id="54a63-167">Select **Save** to configure the tab. The content displays.</span></span><br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="Capture d’écran d’un onglet de canal avec affichage de contenu statique.":::

## <a name="well-done"></a><span data-ttu-id="54a63-169">Bien jouer</span><span class="sxs-lookup"><span data-stu-id="54a63-169">Well done</span></span>

<span data-ttu-id="54a63-170">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="54a63-170">Congratulations!</span></span> <span data-ttu-id="54a63-171">Vous disposez d’une application teams avec un onglet Channel pour afficher du contenu utile dans des canaux et des conversations.</span><span class="sxs-lookup"><span data-stu-id="54a63-171">You have a Teams app with a channel tab for displaying useful content in channels and chats.</span></span>

## <a name="learn-more"></a><span data-ttu-id="54a63-172">Si vous souhaitez en savoir plus</span><span class="sxs-lookup"><span data-stu-id="54a63-172">Learn more</span></span>

* <span data-ttu-id="54a63-173">[Authentifier les utilisateurs avec l’authentification](../tabs/how-to/authentication/auth-aad-sso.md)unique : Si vous souhaitez uniquement que les utilisateurs autorisés visualisent votre onglet, configurez l’authentification unique (SSO) via Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="54a63-173">[Authenticate tab users with SSO](../tabs/how-to/authentication/auth-aad-sso.md): If you only want authorized users viewing your tab, set up single sign-on (SSO) through Azure Active Directory (AD).</span></span>
* <span data-ttu-id="54a63-174">[Incorporer du contenu à partir d’une application Web ou d’une page Web existante](../tabs/how-to/add-tab.md#tab-requirements): nous vous avons expliqué comment créer du contenu pour un onglet personnel, mais vous pouvez également charger du contenu à partir d’une URL externe.</span><span class="sxs-lookup"><span data-stu-id="54a63-174">[Embed content from an existing web app or webpage](../tabs/how-to/add-tab.md#tab-requirements): We showed you how to create new content for a personal tab, but you can also load content from an external URL.</span></span>
* <span data-ttu-id="54a63-175">[Créez une expérience transparente pour votre onglet](../tabs/design/tabs.md): consultez les instructions recommandées pour la création d’onglets Teams.</span><span class="sxs-lookup"><span data-stu-id="54a63-175">[Create a seamless experience for your tab](../tabs/design/tabs.md): See the recommended guidelines for designing Teams tabs.</span></span>
* <span data-ttu-id="54a63-176">[Créer des onglets pour les appareils mobiles](../tabs/design/tabs-mobile.md): Découvrez comment développer des onglets pour les téléphones et les tablettes.</span><span class="sxs-lookup"><span data-stu-id="54a63-176">[Build tabs for mobile](../tabs/design/tabs-mobile.md): Understand how to develop tabs for phones and tablets.</span></span>
* [<span data-ttu-id="54a63-177">Créer un onglet sans la boîte à outils</span><span class="sxs-lookup"><span data-stu-id="54a63-177">Create a tab without the toolkit</span></span>](../tabs/how-to/add-tab.md)

## <a name="next-lesson"></a><span data-ttu-id="54a63-178">Leçon suivante</span><span class="sxs-lookup"><span data-stu-id="54a63-178">Next lesson</span></span>

<span data-ttu-id="54a63-179">Vous saurez comment créer un onglet pour la collaboration.</span><span class="sxs-lookup"><span data-stu-id="54a63-179">You know how to build a tab for collaboration.</span></span> <span data-ttu-id="54a63-180">Vous souhaitez essayer de créer un autre type d’application teams ?</span><span class="sxs-lookup"><span data-stu-id="54a63-180">Want to try building a different kind of Teams app?</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="54a63-181">Créer un bot</span><span class="sxs-lookup"><span data-stu-id="54a63-181">Build a bot</span></span>](../build-your-first-app/build-bot.md)
