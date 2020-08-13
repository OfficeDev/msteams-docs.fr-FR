---
title: Créer un onglet de canal pour teams
author: heath-hamilton
description: Découvrez comment créer un onglet de canal dans votre première application Microsoft Teams.
ms.topic: tutorial
ms.openlocfilehash: f0c59328219b5611efc02c9eb04db6fdc517ca08
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/12/2020
ms.locfileid: "46651986"
---
# <a name="create-a-channel-tab-for-teams"></a><span data-ttu-id="6a399-103">Créer un onglet de canal pour teams</span><span class="sxs-lookup"><span data-stu-id="6a399-103">Create a channel tab for Teams</span></span>

<span data-ttu-id="6a399-104">Dans ce didacticiel, vous allez créer un *onglet de canal*de base, une page de contenu plein écran pour un canal d’équipe ou une conversation.</span><span class="sxs-lookup"><span data-stu-id="6a399-104">In this tutorial, you'll build a basic *channel tab*, a full-screen content page for a team channel or chat.</span></span> <span data-ttu-id="6a399-105">Contrairement à un onglet personnel, les utilisateurs peuvent configurer certains aspects d’un onglet de canal (par exemple, renommer l’onglet de sorte qu’il soit significatif pour le canal).</span><span class="sxs-lookup"><span data-stu-id="6a399-105">Unlike a personal tab, users can configure some aspects of a channel tab (for example, rename the tab so it's meaningful to their channel).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6a399-106">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="6a399-106">Before you begin</span></span>

<span data-ttu-id="6a399-107">Vous avez besoin d’une application de base en cours d’exécution pour commencer.</span><span class="sxs-lookup"><span data-stu-id="6a399-107">You need a basic running app to get started.</span></span> <span data-ttu-id="6a399-108">Si vous n’en avez pas, suivez les instructions de la rubrique [créer et exécuter votre première application teams](build-and-run-with-toolkit.md).</span><span class="sxs-lookup"><span data-stu-id="6a399-108">If you don't have one, follow the instructions at [build and run your Teams first app](build-and-run-with-toolkit.md).</span></span> <span data-ttu-id="6a399-109">Lorsque vous créez votre projet d’application, choisissez uniquement l’option de l' **onglet canal groupe ou teams** .</span><span class="sxs-lookup"><span data-stu-id="6a399-109">When you create your app project, choose only the **Group or Teams channel tab** option.</span></span>

## <a name="your-assignment"></a><span data-ttu-id="6a399-110">Votre affectation</span><span class="sxs-lookup"><span data-stu-id="6a399-110">Your assignment</span></span>

<span data-ttu-id="6a399-111">Il n’y a pas longtemps, votre organisation a créé un onglet teams avec des informations sur la façon de contacter des fonctions importantes (support technique, RH, etc.).</span><span class="sxs-lookup"><span data-stu-id="6a399-111">Not long ago, your organization created a Teams tab with information on how to contact important functions (help desk, HR, etc.).</span></span> <span data-ttu-id="6a399-112">Toutefois, étant donné que l’onglet a été inclus uniquement à des fins personnelles, chaque utilisateur doit installer l’onglet pour l’afficher et l’adoption est inférieure à celle attendue.</span><span class="sxs-lookup"><span data-stu-id="6a399-112">However, since the tab was scoped only for personal use, each user must install the tab to see it and adoption is lower than expected.</span></span> <span data-ttu-id="6a399-113">En d’autres termes, trop de travailleurs ne sachent toujours pas comment contacter le support technique.</span><span class="sxs-lookup"><span data-stu-id="6a399-113">In other words, too many workers still don't know how to reach the help desk.</span></span>

<span data-ttu-id="6a399-114">Vous pouvez faciliter la recherche de ces informations en créant un onglet de canal, ce qui vous évite de devoir installer une application.</span><span class="sxs-lookup"><span data-stu-id="6a399-114">You can make this information easier to find by building a channel tab, which will remove the burden of requiring everyone to install an app.</span></span> <span data-ttu-id="6a399-115">Au lieu de cela, un utilisateur peut installer l’onglet dans un canal ou une conversation pour l’ensemble du groupe.</span><span class="sxs-lookup"><span data-stu-id="6a399-115">Instead, one user can install the tab in a channel or chat for the benefit of an entire group.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="6a399-116">Ce que vous allez apprendre</span><span class="sxs-lookup"><span data-stu-id="6a399-116">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="6a399-117">Identifier le manifeste d’application et les composants de génération de modèles automatique pertinents pour les onglets de canal</span><span class="sxs-lookup"><span data-stu-id="6a399-117">Identify the app manifest and scaffolding components relevant to channel tabs</span></span>
> * <span data-ttu-id="6a399-118">Créer du contenu pour votre onglet</span><span class="sxs-lookup"><span data-stu-id="6a399-118">Create content for your tab</span></span>
> * <span data-ttu-id="6a399-119">Créer du contenu pour la page de configuration d’un onglet</span><span class="sxs-lookup"><span data-stu-id="6a399-119">Create content for a tab's configuration page</span></span>
> * <span data-ttu-id="6a399-120">Autoriser la configuration et l’installation de l’onglet</span><span class="sxs-lookup"><span data-stu-id="6a399-120">Allow the tab to be configured and installed</span></span>
> * <span data-ttu-id="6a399-121">Fournir un nom d’onglet suggéré</span><span class="sxs-lookup"><span data-stu-id="6a399-121">Provide a suggested tab name</span></span>

## <a name="identify-relevant-app-manifest-and-scaffolding-components"></a><span data-ttu-id="6a399-122">Identifier le manifeste d’application et les composants d’échafaudage pertinents</span><span class="sxs-lookup"><span data-stu-id="6a399-122">Identify relevant app manifest and scaffolding components</span></span>

<span data-ttu-id="6a399-123">La plupart des onglets de canal de génération d’applications et de manifeste sont configurés automatiquement lorsque vous créez votre projet avec Team Toolkit.</span><span class="sxs-lookup"><span data-stu-id="6a399-123">Much of the channel tab app scaffolding and manifest is set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="6a399-124">Examinons les principaux composants de la création d’un onglet de canal.</span><span class="sxs-lookup"><span data-stu-id="6a399-124">Let's look at the main components for building a channel tab.</span></span>

### <a name="app-manifest"></a><span data-ttu-id="6a399-125">Manifeste de l’application</span><span class="sxs-lookup"><span data-stu-id="6a399-125">App manifest</span></span>

<span data-ttu-id="6a399-126">L’extrait de code suivant du manifeste de l’application indique [`configurableTabs`](../../resources/schema/manifest-schema.md#configurabletabs) , qui inclut les propriétés et les valeurs par défaut pertinentes pour les onglets de canal.</span><span class="sxs-lookup"><span data-stu-id="6a399-126">The following snippet from the app manifest shows [`configurableTabs`](../../resources/schema/manifest-schema.md#configurabletabs), which includes the properties and default values relevant to channel tabs.</span></span>

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

* <span data-ttu-id="6a399-127">`configurationUrl`: URL hôte de votre page de configuration d’onglet (doit être HTTPs).</span><span class="sxs-lookup"><span data-stu-id="6a399-127">`configurationUrl`: The host URL for your tab configuration page (must be HTTPS).</span></span>
* <span data-ttu-id="6a399-128">`canUpdateConfiguration`: Si ce paramètre `true` est défini sur, les utilisateurs peuvent modifier les paramètres de tabulation, renommer l’onglet ou le supprimer d’un canal ou d’une conversation.</span><span class="sxs-lookup"><span data-stu-id="6a399-128">`canUpdateConfiguration`: If set to `true`, users can change tab settings, rename the tab, or remove it from a channel or chat.</span></span>
* <span data-ttu-id="6a399-129">`scopes`: Spécifie si les utilisateurs peuvent installer l’application dans Channels ( `team` ) et les conversations ( `groupchat` ).</span><span class="sxs-lookup"><span data-stu-id="6a399-129">`scopes`: Specifies if users can install the app in channels (`team`) and chats (`groupchat`).</span></span> <span data-ttu-id="6a399-130">Au moins une valeur est requise.</span><span class="sxs-lookup"><span data-stu-id="6a399-130">At least one value is required.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="6a399-131">Génération de modèles automatique d’application</span><span class="sxs-lookup"><span data-stu-id="6a399-131">App scaffolding</span></span>

<span data-ttu-id="6a399-132">Le échafaudage de l’application fournit un `TabConfig.js` fichier, situé dans le `src/components` Répertoire de votre projet, pour afficher la page de configuration de votre onglet (en savoir plus sur cela prochainement).</span><span class="sxs-lookup"><span data-stu-id="6a399-132">The app scaffolding provides a `TabConfig.js` file, located in the `src/components` directory of your project, for rendering your tab's configuration page (more on this soon).</span></span>

## <a name="create-your-tab-content"></a><span data-ttu-id="6a399-133">Créer le contenu de votre onglet</span><span class="sxs-lookup"><span data-stu-id="6a399-133">Create your tab content</span></span>

<span data-ttu-id="6a399-134">Ouvrez le manifeste de votre application ( `manifest.json` ) et définissez les propriétés suivantes dans [`staticTabs`](../../resources/schema/manifest-schema.md#statictabs) , qui définit la page de contenu de votre onglet.</span><span class="sxs-lookup"><span data-stu-id="6a399-134">Open your app manifest (`manifest.json`) and set the following properties in [`staticTabs`](../../resources/schema/manifest-schema.md#statictabs), which defines your tab's content page.</span></span>

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

<span data-ttu-id="6a399-135">Copiez et mettez à jour l’extrait de code suivant avec des informations pertinentes pour votre organisation ou, pour des raisons de temps, utilisez le code tel quel.</span><span class="sxs-lookup"><span data-stu-id="6a399-135">Copy and update the following snippet with information that's relevant to your organization or, for the sake of time, use the code as is.</span></span>

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

<span data-ttu-id="6a399-136">Accédez au `src/components` répertoire et ouvrez `Tab.js` .</span><span class="sxs-lookup"><span data-stu-id="6a399-136">Go to the `src/components` directory and open `Tab.js`.</span></span> <span data-ttu-id="6a399-137">Recherchez la `render()` fonction et collez votre contenu dans `return()` (comme illustré).</span><span class="sxs-lookup"><span data-stu-id="6a399-137">Locate the `render()` function and paste your content inside `return()` (as shown).</span></span>

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

<span data-ttu-id="6a399-138">Ajoutez la règle suivante pour `App.css` que les liens électroniques soient plus faciles à lire quel que soit le thème utilisé.</span><span class="sxs-lookup"><span data-stu-id="6a399-138">Add the following rule to `App.css` so the email links are easier to read no matter which theme is used.</span></span>

```CSS
  a {
    color: inherit;
  }
```

## <a name="create-your-tab-configuration-page"></a><span data-ttu-id="6a399-139">Créer votre page de configuration d’onglet</span><span class="sxs-lookup"><span data-stu-id="6a399-139">Create your tab configuration page</span></span>

<span data-ttu-id="6a399-140">Chaque onglet de canal comporte une page de configuration, modale avec au moins une option d’installation qui s’affiche lors de l’installation de l’application.</span><span class="sxs-lookup"><span data-stu-id="6a399-140">Every channel tab has a configuration page, a modal with at least one setup option that displays when installing the app.</span></span> <span data-ttu-id="6a399-141">La page Configuration par défaut demande à l’utilisateur s’il souhaite avertir le canal ou la conversation lorsque l’onglet est installé.</span><span class="sxs-lookup"><span data-stu-id="6a399-141">The configuration page by default asks users if they want to notify the channel or chat when the tab is installed.</span></span>

<span data-ttu-id="6a399-142">Ajoutez du contenu à votre page de configuration.</span><span class="sxs-lookup"><span data-stu-id="6a399-142">Add some content to your configuration page.</span></span> <span data-ttu-id="6a399-143">Accédez au répertoire de votre projet `src/components` , ouvrez-le `TabConfig.js` et insérez du contenu dans `return()` (comme illustré).</span><span class="sxs-lookup"><span data-stu-id="6a399-143">Go to your project's `src/components` directory, open `TabConfig.js`, and insert some content inside `return()` (as shown).</span></span>

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
> <span data-ttu-id="6a399-144">Au minimum, fournissez des informations succinctes sur votre application sur cette page, car il peut s’agir de la première fois que les utilisateurs en apprennent à le faire.</span><span class="sxs-lookup"><span data-stu-id="6a399-144">At minimum, provide some brief information about your app on this page since this may be the first time users are learning about it.</span></span> <span data-ttu-id="6a399-145">Vous pouvez également inclure des options de configuration personnalisées ou un [flux de travail d’authentification](../../tabs/how-to/authentication/auth-aad-sso.md), qui est courant sur les pages de configuration d’onglet.</span><span class="sxs-lookup"><span data-stu-id="6a399-145">You also could include custom configuration options or an [authentication workflow](../../tabs/how-to/authentication/auth-aad-sso.md), which is common on tab configuration pages.</span></span>

## <a name="allow-the-tab-to-be-configured-and-installed"></a><span data-ttu-id="6a399-146">Autoriser la configuration et l’installation de l’onglet</span><span class="sxs-lookup"><span data-stu-id="6a399-146">Allow the tab to be configured and installed</span></span>

<span data-ttu-id="6a399-147">Pour que les utilisateurs puissent configurer et installer correctement l’onglet canal, vous devez ajouter l’URL d’hôte que vous avez configurée lors de la [création et de l’exécution de votre première application](build-and-run-with-toolkit.md) sur le composant de page de configuration.</span><span class="sxs-lookup"><span data-stu-id="6a399-147">For users to successfully configure and install the channel tab, you must add the host URL you set up when [creating and running your first app](build-and-run-with-toolkit.md) to the configuration page component.</span></span>

<span data-ttu-id="6a399-148">Accédez à `TabConfig.js` et recherchez `microsoftTeams.settings.setSettings` .</span><span class="sxs-lookup"><span data-stu-id="6a399-148">Go to `TabConfig.js` and locate `microsoftTeams.settings.setSettings`.</span></span> <span data-ttu-id="6a399-149">Pour `"contentUrl"` , remplacez la `localhost:3000` partie de l’URL par le domaine dans lequel vous hébergez le contenu de l’onglet (comme illustré ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="6a399-149">For `"contentUrl"`, replace the `localhost:3000` part of the URL with the domain where you're hosting the tab content (as shown).</span></span>

```JavaScript
    microsoftTeams.settings.setSettings({
      "contentUrl": "https://<MY_HOST_DOMAIN>/tab"
    });
```

<span data-ttu-id="6a399-150">Assurez-vous également que `microsoftTeams.settings.setValidityState(true);` .</span><span class="sxs-lookup"><span data-stu-id="6a399-150">Also, make sure that `microsoftTeams.settings.setValidityState(true);`.</span></span> <span data-ttu-id="6a399-151">C’est par défaut, mais si ce paramètre est défini sur `false` , le bouton **Enregistrer** est désactivé sur la page de configuration.</span><span class="sxs-lookup"><span data-stu-id="6a399-151">It is by default, but if set to `false`, the **Save** button is disabled on the configuration page.</span></span>

## <a name="provide-a-suggested-tab-name"></a><span data-ttu-id="6a399-152">Fournir un nom d’onglet suggéré</span><span class="sxs-lookup"><span data-stu-id="6a399-152">Provide a suggested tab name</span></span>

<span data-ttu-id="6a399-153">Lorsque vous installez un onglet pour une utilisation personnelle, le nom d’affichage est la `name` propriété dans la `staticTabs` partie du manifeste de l’application (par exemple, **mes contacts**).</span><span class="sxs-lookup"><span data-stu-id="6a399-153">When you install a tab for personal use, the display name is the `name` property in the `staticTabs` portion of of the app manifest (for example, **My Contacts**).</span></span> <span data-ttu-id="6a399-154">Lorsque vous installez un onglet canal, le nom de l’application s’affiche par défaut (par exemple, **First-App**).</span><span class="sxs-lookup"><span data-stu-id="6a399-154">When you install a channel tab, by default the app name displays (for example, **first-app**).</span></span>

<span data-ttu-id="6a399-155">Cela peut être approprié en fonction de ce que vous appelez votre application, mais vous souhaiterez peut-être attribuer un nom plus évocateur dans le contexte de la collaboration de groupe (par exemple, **contacts d’équipe**).</span><span class="sxs-lookup"><span data-stu-id="6a399-155">This may be fine depending on what you call your app, but you may want to provide a name that makes more sense in the context of group collaboration (for example, **Team Contacts**).</span></span>

<span data-ttu-id="6a399-156">Dans `TabConfig.js` , revenez à `microsoftTeams.settings.setSettings` .</span><span class="sxs-lookup"><span data-stu-id="6a399-156">In `TabConfig.js`, go back to `microsoftTeams.settings.setSettings`.</span></span> <span data-ttu-id="6a399-157">Ajoutez la `suggestedDisplayName` propriété avec le nom de l’onglet que vous souhaitez afficher par défaut (comme illustré).</span><span class="sxs-lookup"><span data-stu-id="6a399-157">Add the `suggestedDisplayName` property with the tab name you want to display by default (as shown).</span></span> <span data-ttu-id="6a399-158">Utilisez le nom fourni ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="6a399-158">Use the provided name or create your own.</span></span> <span data-ttu-id="6a399-159">N’oubliez pas que dans le manifeste, vous autorisez les utilisateurs à modifier le nom s’ils le souhaitent.</span><span class="sxs-lookup"><span data-stu-id="6a399-159">Remember, in the manifest you're allowing users to change the name if they want.</span></span>

```JavaScript
    microsoftTeams.settings.setSettings({
      "contentUrl": "https://<MY_HOST_DOMAIN>/tab",
      "suggestedDisplayName": "Team Contacts"
    });
```

## <a name="view-the-channel-tab"></a><span data-ttu-id="6a399-160">Affichage de l’onglet canal</span><span class="sxs-lookup"><span data-stu-id="6a399-160">View the channel tab</span></span>

<span data-ttu-id="6a399-161">Pour afficher les pages de configuration et de contenu de l’onglet canal, vous devez l’installer dans un canal ou une conversation.</span><span class="sxs-lookup"><span data-stu-id="6a399-161">To see your channel tab's configuration and content pages, you must install it in a channel or chat.</span></span>

1. <span data-ttu-id="6a399-162">Dans le client Teams, sélectionnez **applications**.</span><span class="sxs-lookup"><span data-stu-id="6a399-162">In the Teams client, select **Apps**.</span></span>
1. <span data-ttu-id="6a399-163">Sélectionnez **Télécharger une application personnalisée** et choisissez l’application `Development.zip` .</span><span class="sxs-lookup"><span data-stu-id="6a399-163">Select **Upload a custom app** and choose your app's `Development.zip`.</span></span>
1. <span data-ttu-id="6a399-164">Sélectionnez **Ajouter à une équipe** ou **Ajouter à une conversation** , puis recherchez un canal ou une conversation que vous pouvez utiliser à des fins de test.</span><span class="sxs-lookup"><span data-stu-id="6a399-164">Choose **Add to a team** or **Add to a chat** and locate a channel or chat you can use for testing.</span></span>
1. <span data-ttu-id="6a399-165">Sélectionnez **configurer un onglet**. La page Configuration s’affiche.</span><span class="sxs-lookup"><span data-stu-id="6a399-165">Select **Set up a tab**. The configuration page displays.</span></span>

:::image type="content" source="../doc-links/images/channel-tab-tutorial-content.png" alt-text="Exemple de capture d’écran de la page de configuration de l’onglet canal":::

<span data-ttu-id="6a399-167">Une fois que vous sélectionnez **Enregistrer** pour configurer l’onglet, le contenu s’affiche.</span><span class="sxs-lookup"><span data-stu-id="6a399-167">Once you select **Save** to configure the tab, the content displays.</span></span>

![Exemple de capture d’écran d’un onglet de canal avec contenu statique](../doc-links/images/channel-tab-tutorial-content-installed.png)

## <a name="well-done"></a><span data-ttu-id="6a399-169">Bien jouer</span><span class="sxs-lookup"><span data-stu-id="6a399-169">Well done</span></span>

<span data-ttu-id="6a399-170">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="6a399-170">Congratulations!</span></span> <span data-ttu-id="6a399-171">Vous disposez d’une application teams avec un onglet Channel pour afficher du contenu utile dans des canaux et des conversations.</span><span class="sxs-lookup"><span data-stu-id="6a399-171">You have a Teams app with a channel tab for displaying useful content in channels and chats.</span></span>

## <a name="learn-more"></a><span data-ttu-id="6a399-172">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="6a399-172">Learn more</span></span>

* <span data-ttu-id="6a399-173">[Authentifier les utilisateurs avec l’authentification](../../tabs/how-to/authentication/auth-aad-sso.md)unique : Si vous souhaitez uniquement que les utilisateurs autorisés visualisent votre onglet, configurez l’authentification unique (SSO) via Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="6a399-173">[Authenticate tab users with SSO](../../tabs/how-to/authentication/auth-aad-sso.md): If you only want authorized users viewing your tab, set up single sign-on (SSO) through Azure Active Directory (AD).</span></span>
* <span data-ttu-id="6a399-174">[Incorporer du contenu à partir d’une application Web ou d’une page Web existante](../../tabs/how-to/add-tab.md#tab-requirements): nous vous avons expliqué comment créer du contenu pour un onglet personnel, mais vous pouvez également charger du contenu à partir d’une URL externe.</span><span class="sxs-lookup"><span data-stu-id="6a399-174">[Embed content from an existing web app or webpage](../../tabs/how-to/add-tab.md#tab-requirements): We showed you how to create new content for a personal tab, but you can also load content from an external URL.</span></span>
* <span data-ttu-id="6a399-175">[Créez une expérience transparente pour votre onglet](../../tabs/design/tabs.md): consultez les instructions recommandées pour la création d’onglets Teams.</span><span class="sxs-lookup"><span data-stu-id="6a399-175">[Create a seamless experience for your tab](../../tabs/design/tabs.md): See the recommended guidelines for designing Teams tabs.</span></span>
* <span data-ttu-id="6a399-176">[Onglets de génération pour les appareils mobiles](../../tabs/design/tabs-mobile.md): Découvrez comment développer des onglets pour smartphones et tablettes.</span><span class="sxs-lookup"><span data-stu-id="6a399-176">[Build tabs for mobile](../../tabs/design/tabs-mobile.md): Understand how to develop tabs for smartphones and tablets.</span></span>
