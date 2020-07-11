---
title: Charger votre application personnalisée dans Microsoft teams
description: Décrit comment télécharger votre application dans Microsoft teams
keywords: Téléchargement d’applications teams
ms.openlocfilehash: c130ef48d3ad7476de9ca5afeb7b613197c43f18
ms.sourcegitcommit: 3ba5a5a7d9d9d906abc3ee1df9c2177de0cfd767
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2020
ms.locfileid: "45103025"
---
# <a name="upload-an-app-package-to-microsoft-teams"></a><span data-ttu-id="318ce-104">Téléchargement d’un package d’application dans Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="318ce-104">Upload an app package to Microsoft Teams</span></span>

<span data-ttu-id="318ce-105">Pour tester l’expérience de votre application dans Microsoft Teams, vous devez charger votre application dans Teams.</span><span class="sxs-lookup"><span data-stu-id="318ce-105">To test your app experience within Microsoft Teams, you need to upload your app to Teams.</span></span> <span data-ttu-id="318ce-106">Le téléchargement ajoute l’application à l’équipe que vous sélectionnez, et vous et les membres de votre équipe pouvez interagir avec elle comme les utilisateurs finaux.</span><span class="sxs-lookup"><span data-stu-id="318ce-106">Uploading adds the app to the team you select, and you and your team members can interact with it like end users.</span></span>

> [!NOTE]
> <span data-ttu-id="318ce-107">Le téléchargement d’un package mis à jour pour une application existante avec un bot peut ne pas afficher les changements d’onglet lorsqu’ils sont affichés dans la fenêtre de conversation.</span><span class="sxs-lookup"><span data-stu-id="318ce-107">Uploading an updated package for an existing app with a bot might not show tab changes when viewed through the Conversations window.</span></span> <span data-ttu-id="318ce-108">Il est préférable d’y accéder via la fonction fly-out des applications ou de tester un environnement de test propre.</span><span class="sxs-lookup"><span data-stu-id="318ce-108">It's better to access it via the Apps fly-out, or test on a clean test environment.</span></span>

## <a name="create-your-upload-package"></a><span data-ttu-id="318ce-109">Créer votre package de téléchargement</span><span class="sxs-lookup"><span data-stu-id="318ce-109">Create your upload package</span></span>

<span data-ttu-id="318ce-110">Pour le développement et l’envoi AppSource (anciennement Office Store), vous devez créer un package pouvant être chargé contenant les informations pour décrire votre expérience.</span><span class="sxs-lookup"><span data-stu-id="318ce-110">For development as well as AppSource (formerly Office Store) submission you must create an uploadable package that contains the information to describe your experience.</span></span> <span data-ttu-id="318ce-111">Le package, un fichier. zip, contient le manifeste de l’application et des icônes qui définissent votre expérience de manière unique.</span><span class="sxs-lookup"><span data-stu-id="318ce-111">The package, a .zip file, contains the application manifest and icons that uniquely define your experience.</span></span>

<span data-ttu-id="318ce-112">Pour créer un package de téléchargement, voir [créer le package pour votre application Microsoft teams](../build-and-test/apps-package.md).</span><span class="sxs-lookup"><span data-stu-id="318ce-112">To create an upload package, see [Create the package for your Microsoft Teams app](../build-and-test/apps-package.md).</span></span>

<span data-ttu-id="318ce-113">Une fois votre package créé, vous pouvez le charger dans une équipe.</span><span class="sxs-lookup"><span data-stu-id="318ce-113">With your package created, you can now upload it into a team.</span></span> <span data-ttu-id="318ce-114">Une fois téléchargée, elle est disponible pour tous les utilisateurs de l’équipe sélectionnée et uniquement les utilisateurs de cette équipe.</span><span class="sxs-lookup"><span data-stu-id="318ce-114">Once uploaded it will be available for all users in the selected team, and only the users of that team.</span></span>

## <a name="load-your-package-into-teams"></a><span data-ttu-id="318ce-115">Charger votre package dans teams</span><span class="sxs-lookup"><span data-stu-id="318ce-115">Load your package into Teams</span></span>

<span data-ttu-id="318ce-116">Vous pouvez tester votre package en le téléchargeant dans Teams.</span><span class="sxs-lookup"><span data-stu-id="318ce-116">You can test your package by uploading it into Teams.</span></span>

> [!NOTE]
> <span data-ttu-id="318ce-117">Pour que le chargement fonctionne, votre administrateur client doit d’abord [activer le téléchargement des applications](/microsoftteams/admin-settings).</span><span class="sxs-lookup"><span data-stu-id="318ce-117">For uploading to work, your tenant admin must first [enable uploading of apps](/microsoftteams/admin-settings).</span></span>

<span data-ttu-id="318ce-118">Il existe deux façons de charger votre application dans teams :</span><span class="sxs-lookup"><span data-stu-id="318ce-118">There are two ways to upload your app to Teams:</span></span>

* <span data-ttu-id="318ce-119">Utilisation de la Banque</span><span class="sxs-lookup"><span data-stu-id="318ce-119">Using the Store</span></span>
* <span data-ttu-id="318ce-120">Utilisation de l’onglet applications</span><span class="sxs-lookup"><span data-stu-id="318ce-120">Using the Apps tab</span></span>

## <a name="upload-your-package-into-a-team-or-conversation-using-the-store"></a><span data-ttu-id="318ce-121">Charger votre package dans une équipe ou une conversation à l’aide de la Banque</span><span class="sxs-lookup"><span data-stu-id="318ce-121">Upload your package into a team or conversation using the Store</span></span>

1. <span data-ttu-id="318ce-122">Dans le coin inférieur gauche de teams, sélectionnez l’icône Store.</span><span class="sxs-lookup"><span data-stu-id="318ce-122">In the lower left corner of Teams, choose the Store icon.</span></span> <span data-ttu-id="318ce-123">Sur la page Store, choisissez « Télécharger une application personnalisée ».</span><span class="sxs-lookup"><span data-stu-id="318ce-123">On the Store page, choose "Upload a custom app".</span></span>

   ![Afficher l’équipe](../../assets/images/store-upload-a-custom-app.png)

2. <span data-ttu-id="318ce-125">Dans la boîte de dialogue *ouvrir* , accédez au package à télécharger, puis choisissez *ouvrir*.</span><span class="sxs-lookup"><span data-stu-id="318ce-125">In the *Open* dialog, navigate to the package you want to upload and choose *Open*.</span></span>

<span data-ttu-id="318ce-126">Le package téléchargé doit maintenant être disponible pour une utilisation dans l’équipe ou la conversation spécifiée dans la boîte de dialogue de consentement.</span><span class="sxs-lookup"><span data-stu-id="318ce-126">The uploaded package should now be available for use in the team or conversation specified in the consent dialog.</span></span> <span data-ttu-id="318ce-127">Si votre application ne s’affiche pas, la cause la plus fréquente est une erreur dans le manifeste, en particulier les ID pour les extensions App, bot et Messaging.</span><span class="sxs-lookup"><span data-stu-id="318ce-127">If your app does not appear, the most common reason is an error in the manifest, particularly ids for the app, bot and messaging extensions.</span></span> <span data-ttu-id="318ce-128">Si l’application n’est pas étendue pour les conversations, cette option n’apparaît pas.</span><span class="sxs-lookup"><span data-stu-id="318ce-128">If the app is not scoped for conversations, that option will not appear.</span></span>

>[!NOTE]
> <span data-ttu-id="318ce-129">Les applications dans les conversations sont actuellement en version préliminaire pour les [développeurs](../../resources/dev-preview/developer-preview-intro.md)et l’option ne s’affiche pas si teams n’est pas en cours d’exécution dans ce mode.</span><span class="sxs-lookup"><span data-stu-id="318ce-129">Apps in conversations is currently in [Developer Preview](../../resources/dev-preview/developer-preview-intro.md), and the option will not appear if Teams is not running in that mode.</span></span>

![Exemple de bot dans la liste des robots téléchargés](../../assets/images/botinlist.jpg)

## <a name="upload-your-package-into-a-team-using-the-apps-tab"></a><span data-ttu-id="318ce-131">Charger votre package dans une équipe à l’aide de l’onglet applications</span><span class="sxs-lookup"><span data-stu-id="318ce-131">Upload your package into a team using the Apps tab</span></span>

1. <span data-ttu-id="318ce-132">Dans l’équipe cible, sélectionnez *plus d’options* (**&#8943;**) et sélectionnez *gérer l’équipe*.</span><span class="sxs-lookup"><span data-stu-id="318ce-132">In the target team, choose *More options* (**&#8943;**) and choose *Manage team*.</span></span>

   > [!NOTE]
   > <span data-ttu-id="318ce-133">Vous devez être le propriétaire de l’équipe, ou le propriétaire doit autoriser les utilisateurs à ajouter les types d’application appropriés pour que cette fonctionnalité apparaisse.</span><span class="sxs-lookup"><span data-stu-id="318ce-133">You must be the team owner, or the owner must allow users to add the appropriate app types for this functionality to appear.</span></span>

2. <span data-ttu-id="318ce-134">Sélectionnez l’onglet applications, puis *Télécharger une application personnalisée* dans la partie inférieure droite.</span><span class="sxs-lookup"><span data-stu-id="318ce-134">Select the Apps tab, and then choose *Upload a custom app* on the lower right.</span></span>

   ![Télécharger le point d’entrée](../../assets/images/UploadACustomApp.png)

3. <span data-ttu-id="318ce-136">Naviguez jusqu’à votre package. zip et sélectionnez-le sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="318ce-136">Browse to and select your .zip package from your computer.</span></span>

4. <span data-ttu-id="318ce-137">Après une brève pause, vous verrez votre application téléchargée dans la liste.</span><span class="sxs-lookup"><span data-stu-id="318ce-137">After a brief pause you will see your uploaded app in the list.</span></span>

   ![Exemple de bot dans la liste des robots téléchargés](../../assets/images/botinlist.jpg)

<span data-ttu-id="318ce-139">Si votre application ne se charge pas, la cause la plus fréquente est une erreur dans le manifeste, en particulier les ID pour les extensions App, bot et Messaging.</span><span class="sxs-lookup"><span data-stu-id="318ce-139">If your app does not load, the most common reason is an error in the manifest, particularly ids for the app, bot and messaging extensions.</span></span>

## <a name="accessing-your-uploaded-configurable-tab"></a><span data-ttu-id="318ce-140">Accès à votre onglet configurable chargé</span><span class="sxs-lookup"><span data-stu-id="318ce-140">Accessing your uploaded configurable tab</span></span>

<span data-ttu-id="318ce-141">Si l’application contient des onglets, les utilisateurs peuvent les épingler à n’importe quelle conversation ou canal d’équipe à l’aide du flux de Galerie d’onglets standard :</span><span class="sxs-lookup"><span data-stu-id="318ce-141">If the app contains tabs, users can pin them to any conversation or team channel using the standard tab gallery flow:</span></span>

1. <span data-ttu-id="318ce-142">Accéder à un canal dans l’équipe.</span><span class="sxs-lookup"><span data-stu-id="318ce-142">Go to a channel in the team.</span></span> <span data-ttu-id="318ce-143">Choisissez *+* (*Ajouter un onglet*) à droite des onglets existants.</span><span class="sxs-lookup"><span data-stu-id="318ce-143">Choose *+* (*Add a tab*) to the right of the existing tabs.</span></span>

2. <span data-ttu-id="318ce-144">Sélectionnez votre onglet dans la galerie qui s’affiche.</span><span class="sxs-lookup"><span data-stu-id="318ce-144">Select your tab from the gallery that appears.</span></span>

3. <span data-ttu-id="318ce-145">Acceptez l’invite de consentement.</span><span class="sxs-lookup"><span data-stu-id="318ce-145">Accept the consent prompt.</span></span>

4. <span data-ttu-id="318ce-146">Configurez votre onglet par le biais de sa [page de configuration](../../tabs/how-to/create-tab-pages/configuration-page.md) , puis choisissez *Enregistrer*.</span><span class="sxs-lookup"><span data-stu-id="318ce-146">Configure your tab via its [configuration page](../../tabs/how-to/create-tab-pages/configuration-page.md) and choose *Save*.</span></span>

  ![Boîte de dialogue Ajouter un onglet, comprenant une galerie des onglets disponibles](../../assets/images/tab_gallery.png)

## <a name="accessing-your-uploaded-bot"></a><span data-ttu-id="318ce-148">Accès à votre bot chargé</span><span class="sxs-lookup"><span data-stu-id="318ce-148">Accessing your uploaded bot</span></span>

<span data-ttu-id="318ce-149">Lorsque vous ajoutez un bot à une équipe, il doit pouvoir être utilisé par tous les utilisateurs de cette équipe, à l’intérieur et à l’extérieur des canaux de l’équipe, en fonction de la définition de l’étendue du bot.</span><span class="sxs-lookup"><span data-stu-id="318ce-149">When you add a bot to a team, it should be usable by anyone on that team, inside and outside the team channels, depending on bot scope definition.</span></span> <span data-ttu-id="318ce-150">Vous et les autres membres de l’équipe verrez un billet dans le canal général indiquant que le bot a été ajouté à l’équipe.</span><span class="sxs-lookup"><span data-stu-id="318ce-150">You and other team members will see a post in the General channel indicating that the bot has been added to the team.</span></span>

<span data-ttu-id="318ce-151">Pour un robot compatible Teams, vous pouvez commencer par appeler votre bot en @mentioning le nom du bot, qui doit se terminer de manière automatique.</span><span class="sxs-lookup"><span data-stu-id="318ce-151">For a teams-enabled bot, you can start by invoking your bot by @mentioning the name of the bot, which should autocomplete.</span></span>

<span data-ttu-id="318ce-152">Pour tester les conversations directes avec votre robot, vous pouvez y accéder via la page d’accueil de l’application, le @mention dans un canal ou le Rechercher dans la nouvelle fenêtre de **conversation** .</span><span class="sxs-lookup"><span data-stu-id="318ce-152">To test direct chats with your bot, you can either access it via the App home, @mention it in a channel, or search for it in the **New Chat** window.</span></span>

<span data-ttu-id="318ce-153">Lorsque vous ajoutez votre bot à une conversation pour tester les conversations directes avec votre robot, vous pouvez le @mention dans une conversation ou le Rechercher dans la nouvelle fenêtre de **conversation** .</span><span class="sxs-lookup"><span data-stu-id="318ce-153">When you add your bot to a conversation To test direct chats with your bot, you can @mention it in a conversation, or search for it in the **New Chat** window.</span></span>

## <a name="accessing-your-uploaded-connector"></a><span data-ttu-id="318ce-154">Accès à votre connecteur téléchargé</span><span class="sxs-lookup"><span data-stu-id="318ce-154">Accessing your uploaded Connector</span></span>

<span data-ttu-id="318ce-155">Une fois l’application chargée dans l’équipe ou la conversation, les utilisateurs peuvent configurer un connecteur à l’aide du flux de Galerie de connecteurs standard :</span><span class="sxs-lookup"><span data-stu-id="318ce-155">With the app loaded in the team or conversation, users can set up a Connector using the standard Connectors gallery flow:</span></span>

1. <span data-ttu-id="318ce-156">Accéder à un canal dans l’équipe.</span><span class="sxs-lookup"><span data-stu-id="318ce-156">Go to a channel in the team.</span></span> <span data-ttu-id="318ce-157">Sélectionnez *plus d’options* (*&#8943;*) et choisissez *connecteurs*.</span><span class="sxs-lookup"><span data-stu-id="318ce-157">Choose *More options* (*&#8943;*) and choose *Connectors*.</span></span>

2. <span data-ttu-id="318ce-158">Sélectionnez votre connecteur dans la section **versions test chargées** en bas.</span><span class="sxs-lookup"><span data-stu-id="318ce-158">Select your Connector from the **Sideloaded** section at the bottom.</span></span>

3. <span data-ttu-id="318ce-159">Configurez votre connecteur via sa [page de configuration](../../webhooks-and-connectors/how-to/connectors-creating.md) et sélectionnez *Enregistrer*.</span><span class="sxs-lookup"><span data-stu-id="318ce-159">Configure your Connector via its [configuration page](../../webhooks-and-connectors/how-to/connectors-creating.md) and choose *Save*.</span></span>

  ![La boîte de dialogue Ajouter un onglet, qui propose une galerie des onglets disponibles.](../../assets/images/connector_gallery.png)

## <a name="accessing-your-uploaded-messaging-extension"></a><span data-ttu-id="318ce-161">Accès à votre extension de messagerie chargée</span><span class="sxs-lookup"><span data-stu-id="318ce-161">Accessing your uploaded messaging extension</span></span>

<span data-ttu-id="318ce-162">Une application téléchargée avec une extension de messagerie apparaît automatiquement dans le menu *plus d’options* (*&#8943;*) de la zone de composition.</span><span class="sxs-lookup"><span data-stu-id="318ce-162">An uploaded app with a messaging extension automatically appears in the *More options* (*&#8943;*) menu in the compose box.</span></span>

![Extensions de messagerie](../../assets/images/compose-extensions/cesampleapp.png)

## <a name="removing-or-updating-your-app"></a><span data-ttu-id="318ce-164">Suppression ou mise à jour de votre application</span><span class="sxs-lookup"><span data-stu-id="318ce-164">Removing or updating your app</span></span>

<span data-ttu-id="318ce-165">Si vous souhaitez supprimer votre application, sélectionnez l’icône de la Corbeille en regard du nom de l’application dans la liste afficher les bots de teams.</span><span class="sxs-lookup"><span data-stu-id="318ce-165">If you want to remove your app, select the trash-can icon next to the app name in the View Teams bots list.</span></span>

<span data-ttu-id="318ce-166">Si vous modifiez les informations de manifeste, vous devez d’abord supprimer l’application, puis ajouter le package mis à jour (par [chargez votre package dans une équipe](#load-your-package-into-teams)).</span><span class="sxs-lookup"><span data-stu-id="318ce-166">If you change manifest information, you must first remove the app and then add the updated package (per [Load your package into a team](#load-your-package-into-teams)).</span></span> <span data-ttu-id="318ce-167">Notez que, en règle générale, les modifications apportées au code de votre service ne nécessitent pas le chargement de votre manifeste, sauf si ces modifications nécessitent des mises à jour du manifeste (telles que les modifications apportées à l’URL ou l’ID de l’application Microsoft pour son bot).</span><span class="sxs-lookup"><span data-stu-id="318ce-167">Note that, in general, code changes on your service do not require you to re-upload your manifest, unless those changes require manifest updates (such as changes to the URL or the Microsoft app ID for its bot).</span></span>

> [!NOTE]
> <span data-ttu-id="318ce-168">Il n’existe aucun moyen de supprimer complètement un bot du contexte personnel.</span><span class="sxs-lookup"><span data-stu-id="318ce-168">There is no way to completely remove a bot from personal context.</span></span> <span data-ttu-id="318ce-169">Si le bot est supprimé et ajouté de nouveau, une communication supplémentaire avec le bot est ajoutée à la conversation précédente.</span><span class="sxs-lookup"><span data-stu-id="318ce-169">If the bot is removed and re-added, additional communication with the bot will append to the previous conversation.</span></span>

## <a name="troubleshooting-notes"></a><span data-ttu-id="318ce-170">Remarques sur la résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="318ce-170">Troubleshooting notes</span></span>

* <span data-ttu-id="318ce-171">Si le manifeste ne se charge pas, vérifiez que vous avez suivi toutes les instructions de [Create the package](../../concepts/build-and-test/apps-package.md) et validé votre manifeste par rapport au [schéma](../../resources/schema/manifest-schema.md).</span><span class="sxs-lookup"><span data-stu-id="318ce-171">If the manifest doesn't load, please double-check that you followed all the instructions in [Create the package](../../concepts/build-and-test/apps-package.md) and validated your manifest against the [schema](../../resources/schema/manifest-schema.md).</span></span>

