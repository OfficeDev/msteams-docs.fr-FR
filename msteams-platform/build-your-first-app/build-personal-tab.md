---
title: Get started - Build a personal tab
author: girliemac
description: Créez rapidement un onglet personnel Microsoft Teams à l'aide de la Shared Computer Toolkit Microsoft Teams.
ms.author: timura
ms.date: 03/16/2020
ms.topic: tutorial
ms.openlocfilehash: 05ef9913e338a54c7e6ebc301825b27d4bec9705
ms.sourcegitcommit: 303fc214aa04757779a171337f31a6539f47fd03
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2021
ms.locfileid: "52068580"
---
# <a name="build-a-basic-personal-tab-for-microsoft-teams"></a><span data-ttu-id="b7ce9-103">Créer un onglet personnel de base pour Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="b7ce9-103">Build a basic personal tab for Microsoft Teams</span></span>

<span data-ttu-id="b7ce9-104">Ce didacticiel vous apprend à créer un onglet personnel de base dans Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="b7ce9-104">This tutorial teaches you to build a basic personal tab in Microsoft Teams.</span></span> <span data-ttu-id="b7ce9-105">Les onglets sont un moyen simple pour faire surface des informations dans votre application en hébergeant du contenu web dans Teams.</span><span class="sxs-lookup"><span data-stu-id="b7ce9-105">Tabs are a simple way to surface information in your app by hosting web content in Teams.</span></span> <span data-ttu-id="b7ce9-106">Les onglets sont une fonctionnalité courante des applications personnelles qui fournissent un espace de travail privé pour des utilisateurs individuels.</span><span class="sxs-lookup"><span data-stu-id="b7ce9-106">Tabs are a common feature of personal apps that provide a private workspace for individual users.</span></span> <span data-ttu-id="b7ce9-107">Les onglets personnels sont les plus proches d'une expérience web traditionnelle dans Teams.</span><span class="sxs-lookup"><span data-stu-id="b7ce9-107">Personal tabs are the closest thing to a traditional web experience in Teams.</span></span> 

## <a name="what-youll-learn"></a><span data-ttu-id="b7ce9-108">Ce que vous allez apprendre</span><span class="sxs-lookup"><span data-stu-id="b7ce9-108">What you'll learn</span></span>

* <span data-ttu-id="b7ce9-109">Comprendre les configurations d'application et la échafaudage pertinentes pour les onglets personnels.</span><span class="sxs-lookup"><span data-stu-id="b7ce9-109">Understand the app configurations and scaffolding relevant to personal tabs.</span></span>
* <span data-ttu-id="b7ce9-110">Créez un contenu d'onglet avec une liste de contacts de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="b7ce9-110">Create a tab content with a contact list of your organization.</span></span>
* <span data-ttu-id="b7ce9-111">Mettez à jour le thème de couleur d'un onglet en fonction des préférences de l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b7ce9-111">Update a tab's color theme based on user preference.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b7ce9-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b7ce9-112">Prerequisites</span></span>

<span data-ttu-id="b7ce9-113">Assurez-vous que vous comprenez comment configurer et créer une application Teams simple.</span><span class="sxs-lookup"><span data-stu-id="b7ce9-113">Make sure that you understand how to set up and build a simple Teams app.</span></span> <span data-ttu-id="b7ce9-114">Pour plus d'informations, voir [créer votre première application Microsoft Teams « Hello, World!](../build-your-first-app/build-and-run.md)».</span><span class="sxs-lookup"><span data-stu-id="b7ce9-114">For more information, see [create your first Microsoft Teams "Hello, World!" app](../build-your-first-app/build-and-run.md).</span></span>

## <a name="1-understand-your-app-project-components"></a><span data-ttu-id="b7ce9-115">1. Comprendre les composants de votre projet d'application</span><span class="sxs-lookup"><span data-stu-id="b7ce9-115">1. Understand your app project components</span></span>

<span data-ttu-id="b7ce9-116">Une fois que vous avez créé un onglet personnel de base, la modèle d'application générée fournit les composants pour le rendu de votre onglet personnel dans Teams.</span><span class="sxs-lookup"><span data-stu-id="b7ce9-116">After you have created a basic personal tab, the generated app scaffold provides the components for rendering your personal tab in Teams.</span></span> <span data-ttu-id="b7ce9-117">Vous pouvez travailler avec beaucoup de choses, mais pour l'instant, laissez-nous nous concentrer sur les questions suivantes :</span><span class="sxs-lookup"><span data-stu-id="b7ce9-117">There's a lot you can work with, but for now let us focus on the following:</span></span> 

* <span data-ttu-id="b7ce9-118">`Tab.js` dans le `src/components` répertoire de votre projet.</span><span class="sxs-lookup"><span data-stu-id="b7ce9-118">`Tab.js` file in the `src/components` directory of your project.</span></span> <span data-ttu-id="b7ce9-119">Il s'agit du rendu de la page de contenu de votre onglet.</span><span class="sxs-lookup"><span data-stu-id="b7ce9-119">This is for rendering your tab content page.</span></span>
* <span data-ttu-id="b7ce9-120">Microsoft Teams JavaScript client SDK, qui est pré-chargé dans les composants frontaux de votre projet.</span><span class="sxs-lookup"><span data-stu-id="b7ce9-120">Microsoft Teams JavaScript client SDK, which is pre-loaded in your project's front-end components.</span></span>

<span data-ttu-id="b7ce9-121">Comme vous pouvez le constater dans la section en haut du fichier, l'exemple de code utilise React , une bibliothèque JavaScript open source pour créer une `import` `Tabs.js` interface utilisateur. [](https://reactjs.org/)</span><span class="sxs-lookup"><span data-stu-id="b7ce9-121">As you may notice from the `import` section at the top of `Tabs.js` file, the sample code uses [React](https://reactjs.org/), an open-source JavaScript library for building user-interface.</span></span> 

> [!NOTE]
> <span data-ttu-id="b7ce9-122">Bien que l'utilisation de React ne _soit_ pas requise pour le développement teams, ce didacticiel vous apprend à utiliser React.</span><span class="sxs-lookup"><span data-stu-id="b7ce9-122">Although using React is _not_ required for Teams development, this tutorial teaches you with React.</span></span>

## <a name="2-customize-your-tab-content-page"></a><span data-ttu-id="b7ce9-123">2. Personnaliser la page de contenu de votre onglet</span><span class="sxs-lookup"><span data-stu-id="b7ce9-123">2. Customize your tab content page</span></span>

<span data-ttu-id="b7ce9-124">Vous pouvez personnaliser votre page de contenu d'onglet pour restituer une liste de contacts importants dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="b7ce9-124">You can customize your tab content page to render a list of important contacts in your organization.</span></span> 

<span data-ttu-id="b7ce9-125">**Pour personnaliser la page de contenu de votre onglet**</span><span class="sxs-lookup"><span data-stu-id="b7ce9-125">**To customize your tab content page**</span></span>

1. <span data-ttu-id="b7ce9-126">Copiez et modifiez l'exemple de code suivant avec des informations pertinentes pour vous.</span><span class="sxs-lookup"><span data-stu-id="b7ce9-126">Copy and modify the following code sample with information that's relevant to you.</span></span> <span data-ttu-id="b7ce9-127">Vous pouvez également utiliser le code tel quelle :</span><span class="sxs-lookup"><span data-stu-id="b7ce9-127">You can also use the code as is:</span></span> 
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
1. <span data-ttu-id="b7ce9-128">Nous avons ouvert `src/components` le fichier dans le `Tab.js` répertoire.</span><span class="sxs-lookup"><span data-stu-id="b7ce9-128">Got to the `src/components` directory and open the `Tab.js` file.</span></span> 
1. <span data-ttu-id="b7ce9-129">Go to `render()` and replace the template code with the modified code inside as shown in the following `return()` example:</span><span class="sxs-lookup"><span data-stu-id="b7ce9-129">Go to `render()` and replace the template code with the modified code inside `return()` as shown in the following example:</span></span>
    ```JavaScript
    render() {
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
1. <span data-ttu-id="b7ce9-130">Go to the `src/components` directory and modify the `App.css` file with the following code to make the email links easier to read with any theme that is used:</span><span class="sxs-lookup"><span data-stu-id="b7ce9-130">Go to the `src/components` directory and modify the `App.css` file with the following code to make the email links easier to read with any theme that is used:</span></span>
    ```CSS
    a {
      color: inherit;
    }
    ```
1. <span data-ttu-id="b7ce9-131">Enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="b7ce9-131">Save your changes.</span></span> 

   <span data-ttu-id="b7ce9-132">Vous pouvez afficher le nouveau contenu dans l'onglet de votre application dans Teams.</span><span class="sxs-lookup"><span data-stu-id="b7ce9-132">You can view the new content in your app's tab in Teams.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/personal-tab-tutorial-content.png" alt-text="Capture d'écran d'un onglet personnel avec du contenu statique.":::

## <a name="3-update-your-tab-theme"></a><span data-ttu-id="b7ce9-134">3. Mettre à jour le thème de votre onglet</span><span class="sxs-lookup"><span data-stu-id="b7ce9-134">3. Update your tab theme</span></span>

<span data-ttu-id="b7ce9-135">Il est important pour votre onglet d'avoir un thème qui semble natif de Teams.</span><span class="sxs-lookup"><span data-stu-id="b7ce9-135">It is important for your tab to have a theme that feels native to Teams.</span></span> <span data-ttu-id="b7ce9-136">Vous devez mélanger votre onglet avec le thème Teams.</span><span class="sxs-lookup"><span data-stu-id="b7ce9-136">You must blend your tab with the Teams theme.</span></span> <span data-ttu-id="b7ce9-137">Vos utilisateurs préfèrent généralement les thèmes par défaut (clair), foncé ou à contraste élevé.</span><span class="sxs-lookup"><span data-stu-id="b7ce9-137">Your users generally prefer default (light), dark, or high contrast themes.</span></span> <span data-ttu-id="b7ce9-138">Comme vous l'avez peut-être remarqué dans la dernière capture d'écran, votre onglet a toujours un arrière-plan clair lorsque votre utilisateur utilise le thème foncé.</span><span class="sxs-lookup"><span data-stu-id="b7ce9-138">As you might have noticed in the last screenshot, your tab still has a light background when your user is using the dark theme.</span></span> <span data-ttu-id="b7ce9-139">Il ne s'agit pas d'une expérience utilisateur recommandée.</span><span class="sxs-lookup"><span data-stu-id="b7ce9-139">This is not a recommended user experience.</span></span>

<span data-ttu-id="b7ce9-140">Le SDK client JavaScript teams peut rendre votre application sensible aux modifications de thème dans le client et y réagir.</span><span class="sxs-lookup"><span data-stu-id="b7ce9-140">The Teams JavaScript client SDK can make your app aware of and react to theme changes in the client.</span></span> <span data-ttu-id="b7ce9-141">Pour cela, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="b7ce9-141">To do this, follow these steps:</span></span>

1. <span data-ttu-id="b7ce9-142">**Obtenir le contexte sur le thème du client Teams configuré** L'appel dans votre fichier fournit un contexte sur le thème client configuré `microsoftTeams.getContext()` `Tab.js` (tel que le thème foncé).</span><span class="sxs-lookup"><span data-stu-id="b7ce9-142">**Get context about the configured Teams client theme** The `microsoftTeams.getContext()` call in your `Tab.js` file, provides some context about the configured client theme (such as dark theme).</span></span> <span data-ttu-id="b7ce9-143">Le code suivant accède à `context` l'interface et à ses propriétés :</span><span class="sxs-lookup"><span data-stu-id="b7ce9-143">The following code accesses the `context` interface and its properties:</span></span>

    ```JavaScript
    componentDidMount(){
      // Get the user context from Teams and set it in the state
      microsoftTeams.getContext((context, error) => {
        this.setState({
          context: context,
          theme: context.theme
        });
      });
    }
    ```
1. <span data-ttu-id="b7ce9-144">**Créer un handler de modification de thème** Avec les propriétés en main, votre application a une bonne compréhension de ce qui se passe `context` autour de elle dans Teams.</span><span class="sxs-lookup"><span data-stu-id="b7ce9-144">**Create a theme change handler** With the `context` properties in hand, your app has a solid understanding of what's happening around it in Teams.</span></span> <span data-ttu-id="b7ce9-145">Toutefois, l'application n'a toujours pas d'apparence reflétant le thème lorsqu'un utilisateur le met à jour.</span><span class="sxs-lookup"><span data-stu-id="b7ce9-145">However, the app still doesn't have an appearance reflecting the theme when a user updates it.</span></span>

   <span data-ttu-id="b7ce9-146">Vous avez besoin d'un handler pour mettre à jour l'état de votre application avec le thème.</span><span class="sxs-lookup"><span data-stu-id="b7ce9-146">You need a handler to update your app's state with the theme.</span></span> <span data-ttu-id="b7ce9-147">Pour créer un handler, insérez le handler de modification de thème suivant immédiatement après `microsoftTeams.getContext()` l'appel :</span><span class="sxs-lookup"><span data-stu-id="b7ce9-147">To create a handler, insert the following theme change handler immediately after the `microsoftTeams.getContext()` call:</span></span>

    ```JavaScript
    microsoftTeams.registerOnThemeChangeHandler(theme => {
    if (theme !== this.state.context.theme) {
    this.setState({
      context: {
      ...this.state.context,
      theme
      }
      })   
      }
    });
      ```
1. <span data-ttu-id="b7ce9-148">**Correspondre aux styles de thème** Votre handler de modification de thème est en place, mais vous devez toujours répondre aux modifications et aligner les couleurs de votre onglet avec le thème actuel.</span><span class="sxs-lookup"><span data-stu-id="b7ce9-148">**Match the theme styles** Your theme change handler is in place, however, you still have to respond to changes and align your tab's colors with the current theme.</span></span>

   <span data-ttu-id="b7ce9-149">Dans la `render()` fonction, stockez l'état fourni par le handler de modification de thème dans `isTheme` :</span><span class="sxs-lookup"><span data-stu-id="b7ce9-149">In the `render()` function, store the state provided by the theme change handler in `isTheme`:</span></span>

    ```JavaScript
      const isTheme = this.state.context.theme
    ```
    
    > [!NOTE]
    > <span data-ttu-id="b7ce9-150">Cet exemple est simplement une façon d'appliquer des styles à votre onglet. Utilisez le code tel qu'il est, développez-le ou écrivez le vôtre.</span><span class="sxs-lookup"><span data-stu-id="b7ce9-150">This example is just one way you might apply styles to your tab. Use the code as is, expand on it, or write your own.</span></span>

    <span data-ttu-id="b7ce9-151">Après avoir stocké l'état fourni par le handler de modification de thème, fournissez la logique conditionnelle pour restituer les styles de votre onglet en fonction du thème actuel.</span><span class="sxs-lookup"><span data-stu-id="b7ce9-151">After storing the state provided by the theme change handler, provide the conditional logic to render your tab's styles based on the current theme.</span></span> <span data-ttu-id="b7ce9-152">L'exemple suivant montre une façon de faire de base :</span><span class="sxs-lookup"><span data-stu-id="b7ce9-152">The following example shows a basic way to do this:</span></span>

    1. <span data-ttu-id="b7ce9-153">Go to `render()` and check the current theme in `isTheme` .</span><span class="sxs-lookup"><span data-stu-id="b7ce9-153">Go to `render()` and check the current theme in `isTheme`.</span></span>
    1. <span data-ttu-id="b7ce9-154">Créez `newTheme` un objet avec des propriétés CSS pertinentes pour le thème actuel.</span><span class="sxs-lookup"><span data-stu-id="b7ce9-154">Create a `newTheme` object with CSS properties relevant to the current theme.</span></span>
    1. <span data-ttu-id="b7ce9-155">Appliquez la CSS suivante à l'élément HTML racine de votre onglet ( `<div style={newTheme}>` :</span><span class="sxs-lookup"><span data-stu-id="b7ce9-155">Apply the following CSS to your tab content's root HTML element (`<div style={newTheme}>`):</span></span>

        ```JavaScript
         let newTheme
          if (isTheme === "default") {
            newTheme = {
              backgroundColor: "#EEF1F5",
              color: "#16233A"
            };
          } else {
            newTheme = {
              backgroundColor: "#2B2B30",
              color: "#FFFFFF"
            };
          }
        ```

       <span data-ttu-id="b7ce9-156">Vérifiez votre onglet dans Teams.</span><span class="sxs-lookup"><span data-stu-id="b7ce9-156">Check your tab in Teams.</span></span> <span data-ttu-id="b7ce9-157">L'apparence correspond désormais étroitement au thème foncé.</span><span class="sxs-lookup"><span data-stu-id="b7ce9-157">The appearance now closely matches the dark theme.</span></span>

       :::image type="content" source="../assets/images/build-your-first-app/personal-tab-tutorial-updated-theme.png" alt-text="Capture d'écran d'un onglet personnel avec affichage de contenu statique.":::

## <a name="see-also"></a><span data-ttu-id="b7ce9-159">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="b7ce9-159">See also</span></span>

* [<span data-ttu-id="b7ce9-160">Kit de développement logiciel client JavaScript Teams</span><span class="sxs-lookup"><span data-stu-id="b7ce9-160">Teams JavaScript client SDK</span></span>](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* [<span data-ttu-id="b7ce9-161">Conception de votre onglet pour le bureau et le web Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="b7ce9-161">Designing your tab for Microsoft Teams desktop and web</span></span>](../tabs/design/tabs.md) 
* [<span data-ttu-id="b7ce9-162">Interface de contexte</span><span class="sxs-lookup"><span data-stu-id="b7ce9-162">Context interface</span></span>](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true)
* [<span data-ttu-id="b7ce9-163">Conception de votre application Microsoft Teams avec des modèles d'interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="b7ce9-163">Designing your Microsoft Teams app with UI templates</span></span>](../concepts/design/design-teams-app-ui-templates.md) 
* [<span data-ttu-id="b7ce9-164">Onglets sur les appareils mobiles</span><span class="sxs-lookup"><span data-stu-id="b7ce9-164">Tabs on mobile</span></span>](../tabs/design/tabs-mobile.md)
* [<span data-ttu-id="b7ce9-165">Prise en charge de l' sign-on unique (SSO) pour les onglets</span><span class="sxs-lookup"><span data-stu-id="b7ce9-165">Single sign-on (SSO) support for tabs</span></span>](../tabs/how-to/authentication/auth-aad-sso.md)
* [<span data-ttu-id="b7ce9-166">Présentation de l’API Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="b7ce9-166">Microsoft Teams API overview</span></span>](https://docs.microsoft.com/graph/teams-concept-overview)
* [<span data-ttu-id="b7ce9-167">Créer un onglet personnel personnalisé avec Node.js et le générateur Yeoman pour Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="b7ce9-167">Create a custom personal tab with Node.js and the Yeoman Generator for Microsoft Teams</span></span>](../tabs/quickstarts/create-personal-tab-node-yeoman.md)

## <a name="next-step"></a><span data-ttu-id="b7ce9-168">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="b7ce9-168">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b7ce9-169">Créer un onglet de canal</span><span class="sxs-lookup"><span data-stu-id="b7ce9-169">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)