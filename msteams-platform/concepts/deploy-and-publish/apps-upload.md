---
title: Télécharger votre application personnalisée
description: Décrit comment télécharger votre application dans Microsoft Teams
ms.topic: how-to
ms.author: lajanuar
keywords: téléchargement d’applications Teams
ms.openlocfilehash: 3ca086cf8dbb992de84b22b7499f739d7c80b9d6
ms.sourcegitcommit: 9cfbc44912980a33d2d7c7c85739aeea6ccb41de
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/05/2021
ms.locfileid: "50479880"
---
# <a name="upload-an-app-package-to-microsoft-teams"></a><span data-ttu-id="38b5f-104">Téléchargement d’un package d’application dans Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="38b5f-104">Upload an app package to Microsoft Teams</span></span>

<span data-ttu-id="38b5f-105">Pour tester votre expérience d’application dans Microsoft Teams, vous devez télécharger votre application dans Teams.</span><span class="sxs-lookup"><span data-stu-id="38b5f-105">To test your app experience within Microsoft Teams, you need to upload your app to Teams.</span></span> <span data-ttu-id="38b5f-106">Le téléchargement ajoute l’application à l’équipe sélectionnée et tous les membres de l’équipe peuvent interagir avec elle comme les utilisateurs finaux.</span><span class="sxs-lookup"><span data-stu-id="38b5f-106">Uploading adds the app to the selected team and all the team members can interact with it like end users.</span></span>

> [!NOTE]
> <span data-ttu-id="38b5f-107">Le téléchargement d’un package mis à jour pour une application existante avec un bot peut ne pas afficher les modifications apportées aux onglets lorsqu’il est vu dans la fenêtre de conversations.</span><span class="sxs-lookup"><span data-stu-id="38b5f-107">Uploading an updated package for an existing app with a bot might not show tab changes when viewed through the conversations window.</span></span> <span data-ttu-id="38b5f-108">Vous pouvez accéder à l’application via le volant des applications ou tester dans un environnement propre.</span><span class="sxs-lookup"><span data-stu-id="38b5f-108">You can access the app through the apps fly-out or test in a clean environment.</span></span>

## <a name="create-your-upload-package"></a><span data-ttu-id="38b5f-109">Créer votre package de chargement</span><span class="sxs-lookup"><span data-stu-id="38b5f-109">Create your upload package</span></span>

<span data-ttu-id="38b5f-110">Pour le développement et la soumission à AppSource, vous devez créer un package que vous pouvez télécharger.</span><span class="sxs-lookup"><span data-stu-id="38b5f-110">For development and AppSource submission, you must create a package that you can upload.</span></span> <span data-ttu-id="38b5f-111">Le package doit contenir les informations pour décrire votre expérience.</span><span class="sxs-lookup"><span data-stu-id="38b5f-111">The package must contain the information to describe your experience.</span></span> <span data-ttu-id="38b5f-112">Le package est un fichier .zip qui contient le manifeste de l’application et les icônes qui définissent votre expérience de manière unique.</span><span class="sxs-lookup"><span data-stu-id="38b5f-112">The package is a .zip file that contains the application manifest and icons that uniquely define your experience.</span></span>

<span data-ttu-id="38b5f-113">Pour créer un package de chargement, voir [Créer le package pour votre application Microsoft Teams.](../build-and-test/apps-package.md)</span><span class="sxs-lookup"><span data-stu-id="38b5f-113">To create an upload package, see [Create the package for your Microsoft Teams app](../build-and-test/apps-package.md).</span></span>

<span data-ttu-id="38b5f-114">Après avoir créé le package, téléchargez-le dans une équipe.</span><span class="sxs-lookup"><span data-stu-id="38b5f-114">After you create the package, upload it into a team.</span></span> <span data-ttu-id="38b5f-115">Le package téléchargé est uniquement disponible pour les utilisateurs de l’équipe sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="38b5f-115">The uploaded package is only available to the users of the selected team.</span></span>

## <a name="load-your-package-into-teams"></a><span data-ttu-id="38b5f-116">Charger votre package dans Teams</span><span class="sxs-lookup"><span data-stu-id="38b5f-116">Load your package into Teams</span></span>

<span data-ttu-id="38b5f-117">Vous pouvez tester votre package en le téléchargeant dans Teams.</span><span class="sxs-lookup"><span data-stu-id="38b5f-117">You can test your package by uploading it into Teams.</span></span>

> [!NOTE]
> <span data-ttu-id="38b5f-118">Pour que le téléchargement fonctionne, votre administrateur client doit d’abord [activer le téléchargement d’applications.](/microsoftteams/admin-settings)</span><span class="sxs-lookup"><span data-stu-id="38b5f-118">For uploading to work, your tenant admin must first [enable uploading of apps](/microsoftteams/admin-settings).</span></span>

<span data-ttu-id="38b5f-119">Il existe deux façons de télécharger votre application dans Teams :</span><span class="sxs-lookup"><span data-stu-id="38b5f-119">There are two ways to upload your app to Teams:</span></span>

* <span data-ttu-id="38b5f-120">Utilisation du Store</span><span class="sxs-lookup"><span data-stu-id="38b5f-120">Using the Store</span></span>
* <span data-ttu-id="38b5f-121">Utilisation de l’onglet Applications</span><span class="sxs-lookup"><span data-stu-id="38b5f-121">Using the Apps tab</span></span>

## <a name="upload-your-package-into-a-team-or-conversation-using-the-store"></a><span data-ttu-id="38b5f-122">Charger votre package dans une équipe ou une conversation à l’aide du Store</span><span class="sxs-lookup"><span data-stu-id="38b5f-122">Upload your package into a team or conversation using the Store</span></span>

1. <span data-ttu-id="38b5f-123">Dans le coin inférieur gauche de Teams, sélectionnez **l’icône du** Store.</span><span class="sxs-lookup"><span data-stu-id="38b5f-123">In the lower left corner of Teams, choose the **Store** icon.</span></span> <span data-ttu-id="38b5f-124">On the Store page, choose **Upload a custom app**.</span><span class="sxs-lookup"><span data-stu-id="38b5f-124">On the Store page, choose **Upload a custom app**.</span></span>

  ![Afficher l’équipe](../../assets/images/store-upload-a-custom-app2.png)

2. <span data-ttu-id="38b5f-126">Dans la **boîte de dialogue** Ouvrir, accédez au package que vous souhaitez télécharger et choisissez Ouvrir.</span><span class="sxs-lookup"><span data-stu-id="38b5f-126">In the **Open** dialog, navigate to the package you want to upload and choose Open.</span></span>

   ![Menu Ajouter](../../assets/images/NewappAddmenudropdown.png)

<span data-ttu-id="38b5f-128">Le package téléchargé doit être disponible pour être utilisé dans l’équipe ou la conversation spécifiée dans la boîte de dialogue de consentement.</span><span class="sxs-lookup"><span data-stu-id="38b5f-128">The uploaded package must be available for use in the team or conversation specified in the consent dialog.</span></span> <span data-ttu-id="38b5f-129">Si votre application n’apparaît pas, la raison la plus courante est une erreur dans le manifeste, en particulier les ID de l’application, du bot et des extensions de messagerie.</span><span class="sxs-lookup"><span data-stu-id="38b5f-129">If your app does not appear, the most common reason is an error in the manifest, particularly IDs for the app, bot, and messaging extensions.</span></span> <span data-ttu-id="38b5f-130">Si l’application n’est pas limitée aux conversations, cette option n’apparaît pas.</span><span class="sxs-lookup"><span data-stu-id="38b5f-130">If the app is not scoped for conversations that option does not appear.</span></span>

>[!NOTE]
> <span data-ttu-id="38b5f-131">Les applications dans les conversations sont actuellement [en](../../resources/dev-preview/developer-preview-intro.md)prévisualisation du développeur et l’option n’apparaît pas si Teams n’est pas en cours d’exécution dans ce mode.</span><span class="sxs-lookup"><span data-stu-id="38b5f-131">Apps in conversations is currently in [Developer Preview](../../resources/dev-preview/developer-preview-intro.md), and the option does not appear if Teams is not running in that mode.</span></span>

![Exemple de bot dans la liste des bots téléchargés](../../assets/images/botinlist.jpg)

## <a name="upload-your-package-into-a-team-using-the-apps-tab"></a><span data-ttu-id="38b5f-133">Télécharger votre package dans une équipe à l’aide de l’onglet Applications</span><span class="sxs-lookup"><span data-stu-id="38b5f-133">Upload your package into a team using the Apps tab</span></span>

1. <span data-ttu-id="38b5f-134">Dans l’équipe cible, sélectionnez **Plus d’options** (**&#8943;**) et **sélectionnez Gérer l’équipe.**</span><span class="sxs-lookup"><span data-stu-id="38b5f-134">In the target team, choose **More options** (**&#8943;**) and select **Manage team**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="38b5f-135">Vous devez être le propriétaire de l’équipe ou le propriétaire doit donner accès aux utilisateurs pour ajouter les types d’application appropriés pour que cette fonctionnalité apparaisse.</span><span class="sxs-lookup"><span data-stu-id="38b5f-135">You must be the team owner or the owner must give access to users to add the appropriate app types for this functionality to appear.</span></span>

2. <span data-ttu-id="38b5f-136">Sélectionnez **l’onglet** Applications et choisissez **Télécharger une application personnalisée** en bas à droite.</span><span class="sxs-lookup"><span data-stu-id="38b5f-136">Select the **Apps** tab and choose **Upload a custom app** on the lower right.</span></span>

   ![Point d’entrée de chargement](../../assets/images/UploadACustomApp.png)

3. <span data-ttu-id="38b5f-138">Sélectionnez votre package .zip sur l’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="38b5f-138">Select your .zip package from the computer.</span></span>

4. <span data-ttu-id="38b5f-139">Vous pouvez voir votre application téléchargée dans la liste.</span><span class="sxs-lookup"><span data-stu-id="38b5f-139">You can see your uploaded app in the list.</span></span>

   ![Exemple de bot dans la liste des bots téléchargés](../../assets/images/botinlist.jpg)

<span data-ttu-id="38b5f-141">Si votre application ne se charge pas, la raison la plus courante est une erreur dans le manifeste, en particulier les ID de l’application, du bot et des extensions de messagerie.</span><span class="sxs-lookup"><span data-stu-id="38b5f-141">If your app does not load, the most common reason is an error in the manifest, particularly IDs for the app, bot, and messaging extensions.</span></span>

## <a name="access-your-uploaded-configurable-tab"></a><span data-ttu-id="38b5f-142">Accéder à votre onglet configurable téléchargé</span><span class="sxs-lookup"><span data-stu-id="38b5f-142">Access your uploaded configurable tab</span></span>

<span data-ttu-id="38b5f-143">Si l’application contient des onglets, les utilisateurs peuvent les épingler à n’importe quel canal de conversation ou d’équipe à l’aide du flux de galerie d’onglets standard :</span><span class="sxs-lookup"><span data-stu-id="38b5f-143">If the app contains tabs, users can pin them to any conversation or team channel using the standard tab gallery flow:</span></span>

1. <span data-ttu-id="38b5f-144">Go to a channel in the team.</span><span class="sxs-lookup"><span data-stu-id="38b5f-144">Go to a channel in the team.</span></span> <span data-ttu-id="38b5f-145">Choisissez **+** d’ajouter un onglet à droite des onglets existants.</span><span class="sxs-lookup"><span data-stu-id="38b5f-145">Choose **+** to add a tab to the right of the existing tabs.</span></span>

2. <span data-ttu-id="38b5f-146">Sélectionnez votre onglet dans la galerie qui s’affiche.</span><span class="sxs-lookup"><span data-stu-id="38b5f-146">Select your tab from the gallery that appears.</span></span>

3. <span data-ttu-id="38b5f-147">Acceptez l’invite de consentement.</span><span class="sxs-lookup"><span data-stu-id="38b5f-147">Accept the consent prompt.</span></span>

4. <span data-ttu-id="38b5f-148">Configurez votre onglet via sa [page de configuration](../../tabs/how-to/create-tab-pages/configuration-page.md) et sélectionnez **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="38b5f-148">Configure your tab through its [configuration page](../../tabs/how-to/create-tab-pages/configuration-page.md) and select **Save**.</span></span>

  ![Boîte de dialogue Ajouter un onglet, avec une galerie d’onglets disponibles](../../assets/images/tab_gallery.png)

## <a name="access-your-uploaded-bot"></a><span data-ttu-id="38b5f-150">Accéder à votre bot téléchargé</span><span class="sxs-lookup"><span data-stu-id="38b5f-150">Access your uploaded bot</span></span>

<span data-ttu-id="38b5f-151">Après avoir ajouté le bot à une équipe, il doit être utilisable par toute personne de cette équipe, à l’intérieur et à l’extérieur des canaux de l’équipe, en fonction de la définition de l’étendue du bot.</span><span class="sxs-lookup"><span data-stu-id="38b5f-151">After adding the bot to a team, it must be usable by anyone on that team, inside and outside the team channels, depending on bot scope definition.</span></span> <span data-ttu-id="38b5f-152">Tous les membres de l’équipe peuvent voir un billet dans le canal général indiquant que le bot a été ajouté à l’équipe. </span><span class="sxs-lookup"><span data-stu-id="38b5f-152">All team members can see a post in the **General** channel indicating that the bot has been added to the team.</span></span>

<span data-ttu-id="38b5f-153">Pour un bot Teams, vous pouvez commencer par l’appel de votre bot en @mentioning nom du bot.</span><span class="sxs-lookup"><span data-stu-id="38b5f-153">For a Teams bot, you can start by invoking your bot by @mentioning the name of the bot.</span></span>

<span data-ttu-id="38b5f-154">Pour tester les conversations directes avec votre bot, vous pouvez y accéder via la page d’accueil de l’application, l'@mention dans un canal ou la rechercher dans la **fenêtre Nouvelle** conversation.</span><span class="sxs-lookup"><span data-stu-id="38b5f-154">To test direct chats with your bot, you can either access it through the App home, @mention it in a channel, or search for it in the **New Chat** window.</span></span>

<span data-ttu-id="38b5f-155">Vous pouvez @mention bot dans une conversation ou le  rechercher dans la fenêtre Nouvelle conversation pour tester les conversations directes avec votre bot.</span><span class="sxs-lookup"><span data-stu-id="38b5f-155">You can @mention the bot in a conversation or search for it in the **New Chat** window to test direct chats with your bot.</span></span>

## <a name="access-your-uploaded-connector"></a><span data-ttu-id="38b5f-156">Accéder à votre connecteur téléchargé</span><span class="sxs-lookup"><span data-stu-id="38b5f-156">Access your uploaded Connector</span></span>

<span data-ttu-id="38b5f-157">Une fois l’application chargée dans l’équipe ou la conversation, les utilisateurs peuvent configurer un connecteur à l’aide du flux de galerie connecteurs standard :</span><span class="sxs-lookup"><span data-stu-id="38b5f-157">With the app loaded in the team or conversation, users can set up a Connector using the standard Connectors gallery flow:</span></span>

1. <span data-ttu-id="38b5f-158">Go to a channel in the team.</span><span class="sxs-lookup"><span data-stu-id="38b5f-158">Go to a channel in the team.</span></span> <span data-ttu-id="38b5f-159">Choose **More options** (*&#8943;*) and choose **Connectors**.</span><span class="sxs-lookup"><span data-stu-id="38b5f-159">Choose **More options** (*&#8943;*) and choose **Connectors**.</span></span>

2. <span data-ttu-id="38b5f-160">Sélectionnez votre connecteur dans la section **Sideloaded** en bas.</span><span class="sxs-lookup"><span data-stu-id="38b5f-160">Select your Connector from the **Sideloaded** section at the bottom.</span></span>

3. <span data-ttu-id="38b5f-161">Configurez votre connecteur via sa [page de configuration](../../webhooks-and-connectors/how-to/connectors-creating.md) et sélectionnez **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="38b5f-161">Configure your connector through its [configuration page](../../webhooks-and-connectors/how-to/connectors-creating.md) and select **Save**.</span></span>

  ![Boîte de dialogue Ajouter un onglet, avec une galerie d’onglets disponibles.](../../assets/images/connector_gallery.png)

## <a name="access-your-uploaded-messaging-extension"></a><span data-ttu-id="38b5f-163">Accéder à votre extension de messagerie téléchargée</span><span class="sxs-lookup"><span data-stu-id="38b5f-163">Access your uploaded messaging extension</span></span>

<span data-ttu-id="38b5f-164">Une application téléchargée avec une extension de messagerie apparaît automatiquement dans le menu Plus **d’options** (*&#8943;*) dans la zone de composition.</span><span class="sxs-lookup"><span data-stu-id="38b5f-164">An uploaded app with a messaging extension automatically appears in the **More options** (*&#8943;*) menu in the compose box.</span></span>

![Extensions de messagerie](../../assets/images/compose-extensions/cesampleapp.png)

## <a name="add-a-default-install-scope-and-group-capability"></a><span data-ttu-id="38b5f-166">Ajouter une étendue d’installation et une fonctionnalité de groupe par défaut</span><span class="sxs-lookup"><span data-stu-id="38b5f-166">Add a default install scope and group capability</span></span>

> [!NOTE]
> <span data-ttu-id="38b5f-167">L’étendue d’installation par défaut et la fonctionnalité de groupe sont actuellement disponibles en prévisualisation pour les développeurs uniquement.</span><span class="sxs-lookup"><span data-stu-id="38b5f-167">The default install scope and group capability is currently available in developer preview only.</span></span>

<span data-ttu-id="38b5f-168">Bien que l’installation d’une application dans l’étendue personnelle fonctionne pour la plupart des applications, certaines des applications du Teams Store la prise en charge des étendues personnelles et d’équipe.</span><span class="sxs-lookup"><span data-stu-id="38b5f-168">Although installing an app in the personal scope works for most apps, some of the apps in Teams Store support both personal and team scopes.</span></span>
<span data-ttu-id="38b5f-169">Certaines de ces applications sont conçues pour fonctionner dans une équipe, des réunions ou un groupchat, avec une expérience d’application personnelle secondaire.</span><span class="sxs-lookup"><span data-stu-id="38b5f-169">Some of these apps are intended to work in a team, meetings, or a groupchat, with personal app experience being secondary.</span></span>
<span data-ttu-id="38b5f-170">La sélection d’étendue d’installation par défaut vous permet de spécifier les applications `defaultInstallScope` que vous publiez.</span><span class="sxs-lookup"><span data-stu-id="38b5f-170">The default install scope selection helps you to specify the `defaultInstallScope` for the apps that you publish.</span></span> <span data-ttu-id="38b5f-171">L’expérience d’installation de l’application met les options par défaut à la disposition de l’utilisateur, tandis que les autres sont déplacées sous le chevron, comme le montre l’image.</span><span class="sxs-lookup"><span data-stu-id="38b5f-171">The app installation experience makes the default options available to the user, while the rest is moved under the chevron as highlighted in the image.</span></span>

![Ajouter une application](../../assets/images/compose-extensions/addanapp.png)

<span data-ttu-id="38b5f-173">La `defaultInstallScope` propriété prend en charge des valeurs, telles que personnelles, d’équipe, de conversation de groupe ou de réunions.</span><span class="sxs-lookup"><span data-stu-id="38b5f-173">The `defaultInstallScope` property supports values, such as personal, team, groupchat, or meetings.</span></span>

> [!NOTE]
><span data-ttu-id="38b5f-174">`defaultGroupCapability` fournit la fonctionnalité par défaut qui est ajoutée à l’équipe, au groupchat ou aux réunions.</span><span class="sxs-lookup"><span data-stu-id="38b5f-174">`defaultGroupCapability` provides the default capability that is added to the team, groupchat or meetings.</span></span> <span data-ttu-id="38b5f-175">Choisissez un onglet, un bot ou un connecteur comme fonctionnalité par défaut pour votre application, mais vous devez vous assurer que vous avez fourni la fonctionnalité sélectionnée dans la définition de votre application.</span><span class="sxs-lookup"><span data-stu-id="38b5f-175">Choose a tab, bot, or connector as the default capability for your app, but you must ensure that you have provided the selected capability in your app definition.</span></span>

## <a name="remove-or-update-your-app"></a><span data-ttu-id="38b5f-176">Supprimer ou mettre à jour votre application</span><span class="sxs-lookup"><span data-stu-id="38b5f-176">Remove or update your app</span></span>

<span data-ttu-id="38b5f-177">Pour supprimer votre application, sélectionnez l’icône de suppression en regard du nom de l’application dans la liste Afficher les bots **Teams.**</span><span class="sxs-lookup"><span data-stu-id="38b5f-177">To remove your app, select the delete icon next to the app name in the **View Teams** bots list.</span></span> <span data-ttu-id="38b5f-178">Si vous modifiez les informations de manifeste, supprimez d’abord l’application, puis ajoutez le package mis à jour, voir Charger votre [package dans une équipe.](#load-your-package-into-teams)</span><span class="sxs-lookup"><span data-stu-id="38b5f-178">If you change manifest information, first remove the app and then add the updated package, see [Load your package into a team](#load-your-package-into-teams).</span></span> <span data-ttu-id="38b5f-179">Les modifications de code apportées à votre service ne vous obligent pas à charger à nouveau votre manifeste.</span><span class="sxs-lookup"><span data-stu-id="38b5f-179">Code changes on your service do not require you to upload your manifest again.</span></span> <span data-ttu-id="38b5f-180">Toutefois, si les modifications de code nécessitent des mises à jour de manifeste, telles que des modifications apportées à l’URL ou à l’ID de l’application Microsoft pour son bot, vous devez télécharger à nouveau le manifeste.</span><span class="sxs-lookup"><span data-stu-id="38b5f-180">However, if the code changes require manifest updates, such as changes to the URL or the Microsoft app ID for its bot, you must upload the manifest again.</span></span>

> [!NOTE]
> <span data-ttu-id="38b5f-181">Vous ne pouvez pas supprimer complètement un bot d’un contexte personnel.</span><span class="sxs-lookup"><span data-stu-id="38b5f-181">You cannot remove a bot from a personal context entirely.</span></span> <span data-ttu-id="38b5f-182">Si le bot est supprimé et ajouté à nouveau, une communication supplémentaire avec le bot est ajoutée à la conversation précédente.</span><span class="sxs-lookup"><span data-stu-id="38b5f-182">If the bot is removed and added again, additional communication with the bot appends to the previous conversation.</span></span>

## <a name="troubleshooting-notes"></a><span data-ttu-id="38b5f-183">Notes de dépannage</span><span class="sxs-lookup"><span data-stu-id="38b5f-183">Troubleshooting notes</span></span>

<span data-ttu-id="38b5f-184">Si le manifeste ne parvient pas à se charger, vérifiez si vous avez suivi toutes les instructions dans Créer le [package](../../concepts/build-and-test/apps-package.md) et validé votre manifeste par rapport [au schéma](../../resources/schema/manifest-schema.md).</span><span class="sxs-lookup"><span data-stu-id="38b5f-184">If the manifest fails to load, check if you have followed all the instructions in [Create the package](../../concepts/build-and-test/apps-package.md) and validated your manifest against the [schema](../../resources/schema/manifest-schema.md).</span></span>
