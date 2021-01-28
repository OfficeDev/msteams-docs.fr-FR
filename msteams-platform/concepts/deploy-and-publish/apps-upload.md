---
title: Télécharger votre application personnalisée
description: Décrit comment télécharger votre application dans Microsoft Teams
ms.topic: how-to
keywords: Téléchargement d’applications Teams
ms.openlocfilehash: 2e7a21dc27fdfe824ecacebabbb61a3b99ae8e79
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014340"
---
# <a name="upload-an-app-package-to-microsoft-teams"></a><span data-ttu-id="800e6-104">Téléchargement d’un package d’application dans Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="800e6-104">Upload an app package to Microsoft Teams</span></span>

<span data-ttu-id="800e6-105">Pour tester votre expérience d’application dans Microsoft Teams, vous devez télécharger votre application dans Teams.</span><span class="sxs-lookup"><span data-stu-id="800e6-105">To test your app experience within Microsoft Teams, you need to upload your app to Teams.</span></span> <span data-ttu-id="800e6-106">Le téléchargement ajoute l’application à l’équipe que vous sélectionnez, et vous et les membres de votre équipe pouvez interagir avec elle comme les utilisateurs finaux.</span><span class="sxs-lookup"><span data-stu-id="800e6-106">Uploading adds the app to the team you select, and you and your team members can interact with it like end users.</span></span>

> [!NOTE]
> <span data-ttu-id="800e6-107">Le téléchargement d’un package mis à jour pour une application existante à l’aide d’un bot peut ne pas afficher les modifications apportées aux onglets lorsqu’il est vu dans la fenêtre Conversations.</span><span class="sxs-lookup"><span data-stu-id="800e6-107">Uploading an updated package for an existing app with a bot might not show tab changes when viewed through the Conversations window.</span></span> <span data-ttu-id="800e6-108">Il est préférable d’y accéder via le volant Applications ou de tester dans un environnement de test propre.</span><span class="sxs-lookup"><span data-stu-id="800e6-108">It's better to access it via the Apps fly-out, or test on a clean test environment.</span></span>

## <a name="create-your-upload-package"></a><span data-ttu-id="800e6-109">Créer votre package de chargement</span><span class="sxs-lookup"><span data-stu-id="800e6-109">Create your upload package</span></span>

<span data-ttu-id="800e6-110">Pour le développement, ainsi que pour la soumission d’AppSource (anciennement Office Store), vous devez créer un package téléchargeable qui contient les informations pour décrire votre expérience.</span><span class="sxs-lookup"><span data-stu-id="800e6-110">For development as well as AppSource (formerly Office Store) submission you must create an uploadable package that contains the information to describe your experience.</span></span> <span data-ttu-id="800e6-111">Le package, un fichier .zip, contient le manifeste de l’application et les icônes qui définissent votre expérience de manière unique.</span><span class="sxs-lookup"><span data-stu-id="800e6-111">The package, a .zip file, contains the application manifest and icons that uniquely define your experience.</span></span>

<span data-ttu-id="800e6-112">Pour créer un package de chargement, voir [Créer le package pour votre application Microsoft Teams.](../build-and-test/apps-package.md)</span><span class="sxs-lookup"><span data-stu-id="800e6-112">To create an upload package, see [Create the package for your Microsoft Teams app](../build-and-test/apps-package.md).</span></span>

<span data-ttu-id="800e6-113">Une fois votre package créé, vous pouvez désormais le télécharger dans une équipe.</span><span class="sxs-lookup"><span data-stu-id="800e6-113">With your package created, you can now upload it into a team.</span></span> <span data-ttu-id="800e6-114">Une fois téléchargé, il sera disponible pour tous les utilisateurs de l’équipe sélectionnée, et uniquement pour les utilisateurs de cette équipe.</span><span class="sxs-lookup"><span data-stu-id="800e6-114">Once uploaded it will be available for all users in the selected team, and only the users of that team.</span></span>

## <a name="load-your-package-into-teams"></a><span data-ttu-id="800e6-115">Charger votre package dans Teams</span><span class="sxs-lookup"><span data-stu-id="800e6-115">Load your package into Teams</span></span>

<span data-ttu-id="800e6-116">Vous pouvez tester votre package en le téléchargeant dans Teams.</span><span class="sxs-lookup"><span data-stu-id="800e6-116">You can test your package by uploading it into Teams.</span></span>

> [!NOTE]
> <span data-ttu-id="800e6-117">Pour que le chargement fonctionne, votre administrateur client doit d’abord [activer le téléchargement d’applications.](/microsoftteams/admin-settings)</span><span class="sxs-lookup"><span data-stu-id="800e6-117">For uploading to work, your tenant admin must first [enable uploading of apps](/microsoftteams/admin-settings).</span></span>

<span data-ttu-id="800e6-118">Il existe deux façons de télécharger votre application dans Teams :</span><span class="sxs-lookup"><span data-stu-id="800e6-118">There are two ways to upload your app to Teams:</span></span>

* <span data-ttu-id="800e6-119">Utilisation du Store</span><span class="sxs-lookup"><span data-stu-id="800e6-119">Using the Store</span></span>
* <span data-ttu-id="800e6-120">Utilisation de l’onglet Applications</span><span class="sxs-lookup"><span data-stu-id="800e6-120">Using the Apps tab</span></span>

## <a name="upload-your-package-into-a-team-or-conversation-using-the-store"></a><span data-ttu-id="800e6-121">Charger votre package dans une équipe ou une conversation à l’aide du Store</span><span class="sxs-lookup"><span data-stu-id="800e6-121">Upload your package into a team or conversation using the Store</span></span>

1. <span data-ttu-id="800e6-122">Dans le coin inférieur gauche de Teams, sélectionnez l’icône du Store.</span><span class="sxs-lookup"><span data-stu-id="800e6-122">In the lower left corner of Teams, choose the Store icon.</span></span> <span data-ttu-id="800e6-123">Dans la page Du Store, choisissez « Télécharger une application personnalisée ».</span><span class="sxs-lookup"><span data-stu-id="800e6-123">On the Store page, choose "Upload a custom app".</span></span>

  ![Afficher l’équipe](../../assets/images/store-upload-a-custom-app2.png)

2. <span data-ttu-id="800e6-125">Dans la *boîte de dialogue* Ouvrir, accédez au package que vous souhaitez télécharger et choisissez *Ouvrir.*</span><span class="sxs-lookup"><span data-stu-id="800e6-125">In the *Open* dialog, navigate to the package you want to upload and choose *Open*.</span></span>

   ![Menu Ajouter](../../assets/images/NewappAddmenudropdown.png)

<span data-ttu-id="800e6-127">Le package téléchargé doit maintenant être disponible pour une utilisation dans l’équipe ou la conversation spécifiée dans la boîte de dialogue de consentement.</span><span class="sxs-lookup"><span data-stu-id="800e6-127">The uploaded package should now be available for use in the team or conversation specified in the consent dialog.</span></span> <span data-ttu-id="800e6-128">Si votre application n’apparaît pas, la raison la plus courante est une erreur dans le manifeste, en particulier les ID de l’application, du bot et des extensions de messagerie.</span><span class="sxs-lookup"><span data-stu-id="800e6-128">If your app does not appear, the most common reason is an error in the manifest, particularly ids for the app, bot and messaging extensions.</span></span> <span data-ttu-id="800e6-129">Si l’application n’est pas limitée aux conversations, cette option n’apparaît pas.</span><span class="sxs-lookup"><span data-stu-id="800e6-129">If the app is not scoped for conversations, that option will not appear.</span></span>

>[!NOTE]
> <span data-ttu-id="800e6-130">Les applications des conversations sont actuellement en prévisualisation du développeur [et](../../resources/dev-preview/developer-preview-intro.md)l’option n’apparaît pas si Teams n’est pas en cours d’exécution dans ce mode.</span><span class="sxs-lookup"><span data-stu-id="800e6-130">Apps in conversations is currently in [Developer Preview](../../resources/dev-preview/developer-preview-intro.md), and the option will not appear if Teams is not running in that mode.</span></span>

![Exemple de bot dans la liste des bots téléchargés](../../assets/images/botinlist.jpg)

## <a name="upload-your-package-into-a-team-using-the-apps-tab"></a><span data-ttu-id="800e6-132">Télécharger votre package dans une équipe à l’aide de l’onglet Applications</span><span class="sxs-lookup"><span data-stu-id="800e6-132">Upload your package into a team using the Apps tab</span></span>

1. <span data-ttu-id="800e6-133">Dans l’équipe cible, choisissez *Plus d’options* (**&#8943;**) et choisissez *Gérer l’équipe*.</span><span class="sxs-lookup"><span data-stu-id="800e6-133">In the target team, choose *More options* (**&#8943;**) and choose *Manage team*.</span></span>

   > [!NOTE]
   > <span data-ttu-id="800e6-134">Vous devez être le propriétaire de l’équipe ou autoriser les utilisateurs à ajouter les types d’applications appropriés pour que cette fonctionnalité apparaisse.</span><span class="sxs-lookup"><span data-stu-id="800e6-134">You must be the team owner, or the owner must allow users to add the appropriate app types for this functionality to appear.</span></span>

2. <span data-ttu-id="800e6-135">Sélectionnez l’onglet Applications, puis choisissez *Télécharger une application personnalisée* en bas à droite.</span><span class="sxs-lookup"><span data-stu-id="800e6-135">Select the Apps tab, and then choose *Upload a custom app* on the lower right.</span></span>

   ![Point d’entrée de chargement](../../assets/images/UploadACustomApp.png)

3. <span data-ttu-id="800e6-137">Accédez à votre package .zip et sélectionnez-le à partir de votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="800e6-137">Browse to and select your .zip package from your computer.</span></span>

4. <span data-ttu-id="800e6-138">Après une courte pause, vous verrez votre application téléchargée dans la liste.</span><span class="sxs-lookup"><span data-stu-id="800e6-138">After a brief pause you will see your uploaded app in the list.</span></span>

   ![Exemple de bot dans la liste des bots téléchargés](../../assets/images/botinlist.jpg)

<span data-ttu-id="800e6-140">Si votre application ne se charge pas, la raison la plus courante est une erreur dans le manifeste, en particulier les ID de l’application, du bot et des extensions de messagerie.</span><span class="sxs-lookup"><span data-stu-id="800e6-140">If your app does not load, the most common reason is an error in the manifest, particularly ids for the app, bot and messaging extensions.</span></span>

## <a name="accessing-your-uploaded-configurable-tab"></a><span data-ttu-id="800e6-141">Accès à votre onglet configurable téléchargé</span><span class="sxs-lookup"><span data-stu-id="800e6-141">Accessing your uploaded configurable tab</span></span>

<span data-ttu-id="800e6-142">Si l’application contient des onglets, les utilisateurs peuvent les épingler à n’importe quel canal de conversation ou d’équipe à l’aide du flux de galerie d’onglets standard :</span><span class="sxs-lookup"><span data-stu-id="800e6-142">If the app contains tabs, users can pin them to any conversation or team channel using the standard tab gallery flow:</span></span>

1. <span data-ttu-id="800e6-143">Go to a channel in the team.</span><span class="sxs-lookup"><span data-stu-id="800e6-143">Go to a channel in the team.</span></span> <span data-ttu-id="800e6-144">Choisissez *+* ( Ajouter un *onglet*) à droite des onglets existants.</span><span class="sxs-lookup"><span data-stu-id="800e6-144">Choose *+* (*Add a tab*) to the right of the existing tabs.</span></span>

2. <span data-ttu-id="800e6-145">Sélectionnez votre onglet dans la galerie qui s’affiche.</span><span class="sxs-lookup"><span data-stu-id="800e6-145">Select your tab from the gallery that appears.</span></span>

3. <span data-ttu-id="800e6-146">Acceptez l’invite de consentement.</span><span class="sxs-lookup"><span data-stu-id="800e6-146">Accept the consent prompt.</span></span>

4. <span data-ttu-id="800e6-147">Configurez votre onglet via sa [page de configuration](../../tabs/how-to/create-tab-pages/configuration-page.md) et choisissez *Enregistrer.*</span><span class="sxs-lookup"><span data-stu-id="800e6-147">Configure your tab via its [configuration page](../../tabs/how-to/create-tab-pages/configuration-page.md) and choose *Save*.</span></span>

  ![Boîte de dialogue Ajouter un onglet, avec une galerie d’onglets disponibles](../../assets/images/tab_gallery.png)

## <a name="accessing-your-uploaded-bot"></a><span data-ttu-id="800e6-149">Accès à votre bot téléchargé</span><span class="sxs-lookup"><span data-stu-id="800e6-149">Accessing your uploaded bot</span></span>

<span data-ttu-id="800e6-150">Lorsque vous ajoutez un bot à une équipe, il doit être utilisable par toute personne de cette équipe, à l’intérieur et à l’extérieur des canaux de l’équipe, en fonction de la définition de l’étendue du bot.</span><span class="sxs-lookup"><span data-stu-id="800e6-150">When you add a bot to a team, it should be usable by anyone on that team, inside and outside the team channels, depending on bot scope definition.</span></span> <span data-ttu-id="800e6-151">Vous et les autres membres de l’équipe verrez un billet dans le canal général indiquant que le bot a été ajouté à l’équipe.</span><span class="sxs-lookup"><span data-stu-id="800e6-151">You and other team members will see a post in the General channel indicating that the bot has been added to the team.</span></span>

<span data-ttu-id="800e6-152">Pour un bot activé pour teams, vous pouvez commencer par l’appel de votre bot en @mentioning le nom du bot, qui doit être automatiquementcomplémenté.</span><span class="sxs-lookup"><span data-stu-id="800e6-152">For a teams-enabled bot, you can start by invoking your bot by @mentioning the name of the bot, which should autocomplete.</span></span>

<span data-ttu-id="800e6-153">Pour tester les conversations directes avec votre bot, vous pouvez y accéder via la page d’accueil de l’application, l'@mention dans un canal ou la rechercher dans la **fenêtre Nouvelle** conversation.</span><span class="sxs-lookup"><span data-stu-id="800e6-153">To test direct chats with your bot, you can either access it via the App home, @mention it in a channel, or search for it in the **New Chat** window.</span></span>

<span data-ttu-id="800e6-154">Lorsque vous ajoutez votre bot à une conversation pour tester les conversations directes avec votre bot, vous pouvez le @mention dans une conversation ou le rechercher dans la **fenêtre Nouvelle** conversation.</span><span class="sxs-lookup"><span data-stu-id="800e6-154">When you add your bot to a conversation To test direct chats with your bot, you can @mention it in a conversation, or search for it in the **New Chat** window.</span></span>

## <a name="accessing-your-uploaded-connector"></a><span data-ttu-id="800e6-155">Accès à votre connecteur téléchargé</span><span class="sxs-lookup"><span data-stu-id="800e6-155">Accessing your uploaded Connector</span></span>

<span data-ttu-id="800e6-156">Une fois l’application chargée dans l’équipe ou la conversation, les utilisateurs peuvent configurer un connecteur à l’aide du flux de galerie connecteurs standard :</span><span class="sxs-lookup"><span data-stu-id="800e6-156">With the app loaded in the team or conversation, users can set up a Connector using the standard Connectors gallery flow:</span></span>

1. <span data-ttu-id="800e6-157">Go to a channel in the team.</span><span class="sxs-lookup"><span data-stu-id="800e6-157">Go to a channel in the team.</span></span> <span data-ttu-id="800e6-158">Choose *More options* (*&#8943;*) and choose *Connectors*.</span><span class="sxs-lookup"><span data-stu-id="800e6-158">Choose *More options* (*&#8943;*) and choose *Connectors*.</span></span>

2. <span data-ttu-id="800e6-159">Sélectionnez votre connecteur dans la section **Sideloaded** en bas.</span><span class="sxs-lookup"><span data-stu-id="800e6-159">Select your Connector from the **Sideloaded** section at the bottom.</span></span>

3. <span data-ttu-id="800e6-160">Configurez votre connecteur via sa [page de configuration](../../webhooks-and-connectors/how-to/connectors-creating.md) et choisissez *Enregistrer.*</span><span class="sxs-lookup"><span data-stu-id="800e6-160">Configure your Connector via its [configuration page](../../webhooks-and-connectors/how-to/connectors-creating.md) and choose *Save*.</span></span>

  ![Boîte de dialogue Ajouter un onglet, avec une galerie d’onglets disponibles.](../../assets/images/connector_gallery.png)

## <a name="accessing-your-uploaded-messaging-extension"></a><span data-ttu-id="800e6-162">Accès à votre extension de messagerie téléchargée</span><span class="sxs-lookup"><span data-stu-id="800e6-162">Accessing your uploaded messaging extension</span></span>

<span data-ttu-id="800e6-163">Une application téléchargée avec une extension de messagerie apparaît automatiquement dans le menu Plus *d’options* (*&#8943;*) dans la zone de composition.</span><span class="sxs-lookup"><span data-stu-id="800e6-163">An uploaded app with a messaging extension automatically appears in the *More options* (*&#8943;*) menu in the compose box.</span></span>

![Extensions de messagerie](../../assets/images/compose-extensions/cesampleapp.png)

## <a name="removing-or-updating-your-app"></a><span data-ttu-id="800e6-165">Suppression ou mise à jour de votre application</span><span class="sxs-lookup"><span data-stu-id="800e6-165">Removing or updating your app</span></span>

<span data-ttu-id="800e6-166">Si vous souhaitez supprimer votre application, sélectionnez l’icône de corbeille en regard du nom de l’application dans la liste Afficher les bots Teams.</span><span class="sxs-lookup"><span data-stu-id="800e6-166">If you want to remove your app, select the trash-can icon next to the app name in the View Teams bots list.</span></span>

<span data-ttu-id="800e6-167">Si vous modifiez les informations de manifeste, vous devez d’abord supprimer l’application, puis ajouter le package mis à jour (par chargement de [votre package dans une équipe).](#load-your-package-into-teams)</span><span class="sxs-lookup"><span data-stu-id="800e6-167">If you change manifest information, you must first remove the app and then add the updated package (per [Load your package into a team](#load-your-package-into-teams)).</span></span> <span data-ttu-id="800e6-168">Notez que, en règle générale, les modifications de code sur votre service ne vous obligent pas à télécharger à nouveau votre manifeste, sauf si ces modifications nécessitent des mises à jour de manifeste (telles que les modifications apportées à l’URL ou à l’ID de l’application Microsoft pour son bot).</span><span class="sxs-lookup"><span data-stu-id="800e6-168">Note that, in general, code changes on your service do not require you to re-upload your manifest, unless those changes require manifest updates (such as changes to the URL or the Microsoft app ID for its bot).</span></span>

> [!NOTE]
> <span data-ttu-id="800e6-169">Il n’existe aucun moyen de supprimer complètement un bot d’un contexte personnel.</span><span class="sxs-lookup"><span data-stu-id="800e6-169">There is no way to completely remove a bot from personal context.</span></span> <span data-ttu-id="800e6-170">Si le bot est supprimé et ré-ajouté, une communication supplémentaire avec le bot est ajoutée à la conversation précédente.</span><span class="sxs-lookup"><span data-stu-id="800e6-170">If the bot is removed and re-added, additional communication with the bot will append to the previous conversation.</span></span>

## <a name="troubleshooting-notes"></a><span data-ttu-id="800e6-171">Notes de dépannage</span><span class="sxs-lookup"><span data-stu-id="800e6-171">Troubleshooting notes</span></span>

* <span data-ttu-id="800e6-172">Si le manifeste ne se charge pas, vérifiez que vous avez suivi toutes les instructions dans Créer le [package](../../concepts/build-and-test/apps-package.md) et validé votre manifeste par rapport [au schéma.](../../resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="800e6-172">If the manifest doesn't load, please double-check that you followed all the instructions in [Create the package](../../concepts/build-and-test/apps-package.md) and validated your manifest against the [schema](../../resources/schema/manifest-schema.md).</span></span>
