---
title: Configuration de l’application dans le portail du développeur
description: Découvrez comment configurer et gérer vos applications à l’aide du portail de développement pour Microsoft Teams
keywords: mise en place des équipes du portail de développement
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: ce290bd7daa46467be279aae7c608321e75e2d57
ms.sourcegitcommit: d972953994e405c6afc42e4d4a76b48c6d4cfb5f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/24/2021
ms.locfileid: "52635114"
---
# <a name="app-configuration"></a><span data-ttu-id="12b07-104">Configuration de l’application</span><span class="sxs-lookup"><span data-stu-id="12b07-104">App configuration</span></span>

<span data-ttu-id="12b07-105">La partie la plus significative d’un package Microsoft Teams’application est sa manifest.jsfichier.</span><span class="sxs-lookup"><span data-stu-id="12b07-105">The most significant part of a Microsoft Teams app package is its manifest.json file.</span></span> <span data-ttu-id="12b07-106">Ce fichier doit être conforme au [schéma Teams’application.](~/resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="12b07-106">This file must conform to the [Teams App schema](~/resources/schema/manifest-schema.md).</span></span> <span data-ttu-id="12b07-107">Le manifest.jssur le fichier contient des métadonnées, ce qui Teams de présenter correctement votre application aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="12b07-107">The manifest.json file contains metadata, which allows Teams to correctly present your app to users.</span></span>

<span data-ttu-id="12b07-108">Vous pouvez effectuer les actions suivantes dans la section **Configurer** du portail du développeur :</span><span class="sxs-lookup"><span data-stu-id="12b07-108">You can perform the following actions in the **Configure** section of the Developer Portal:</span></span>

* <span data-ttu-id="12b07-109">Créez facilement un package d’application.</span><span class="sxs-lookup"><span data-stu-id="12b07-109">Create an app package easily.</span></span>
* <span data-ttu-id="12b07-110">Décrivez l’application.</span><span class="sxs-lookup"><span data-stu-id="12b07-110">Describe the app.</span></span>
* <span data-ttu-id="12b07-111">Télécharger vos icônes.</span><span class="sxs-lookup"><span data-stu-id="12b07-111">Upload your icons.</span></span>
* <span data-ttu-id="12b07-112">Produire un .zip pour faciliter la distribution.</span><span class="sxs-lookup"><span data-stu-id="12b07-112">Produce a .zip file for easy distribution.</span></span>

> [!NOTE]
> <span data-ttu-id="12b07-113">Le portail du développeur ne produit pas de code fonctionnel pour votre application ou n’héberge pas votre application.</span><span class="sxs-lookup"><span data-stu-id="12b07-113">Developer Portal does not produce functional code for your app, or host your app.</span></span> <span data-ttu-id="12b07-114">Votre application doit déjà être hébergée et en cours d’exécution à l’URL répertoriée dans le manifeste pour que le processus de chargement de l’application aboutisse à une application fonctionnelle.</span><span class="sxs-lookup"><span data-stu-id="12b07-114">Your app must already be hosted and running at the URL listed in the manifest for the app upload process to result in a working app.</span></span>

:::image type="content" source="~/assets/images/tdp/tdp_configure_1.png" alt-text="Screenshot showing the Configure page of Teams Developer Portal.":::

## <a name="basic-information-and-branding"></a><span data-ttu-id="12b07-116">Informations de base et branding</span><span class="sxs-lookup"><span data-stu-id="12b07-116">Basic information and Branding</span></span>

<span data-ttu-id="12b07-117">Les **sections Informations de** base et **Branding** définissent la description de haut niveau de l’application que vous faites.</span><span class="sxs-lookup"><span data-stu-id="12b07-117">The **Basic information** and **Branding** sections define the high-level description of the app you are making.</span></span> <span data-ttu-id="12b07-118">Cela inclut le nom, la description et la marque visuelle de l’application.</span><span class="sxs-lookup"><span data-stu-id="12b07-118">This includes the app’s name, description, and visual branding.</span></span> <span data-ttu-id="12b07-119">Les informations de cette section seront utilisées dans la liste du Teams de votre application et dans le dialogue d’installation de l’application.</span><span class="sxs-lookup"><span data-stu-id="12b07-119">The information in this section will be used in your app's Teams store listing and app installation dialogue.</span></span>

## <a name="capabilities"></a><span data-ttu-id="12b07-120">Fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="12b07-120">Capabilities</span></span>

<span data-ttu-id="12b07-121">Les **détails des** fonctionnalités de l’application sont répertoriés dans la section Fonctionnalités de configuration.</span><span class="sxs-lookup"><span data-stu-id="12b07-121">The **Capabilities** section of Configuration has the app's capabilities details listed.</span></span>

> [!NOTE]
> <span data-ttu-id="12b07-122">La fonctionnalité de personnalisation de l’application est actuellement disponible dans la version préliminaire du développeur uniquement.</span><span class="sxs-lookup"><span data-stu-id="12b07-122">The app customization feature is currently available in the developer preview only.</span></span>
> 
> <span data-ttu-id="12b07-123">En tant que meilleure pratique, vous devez fournir des instructions de personnalisation que les utilisateurs et les clients de l’application doivent suivre lors de la personnalisation de votre application.</span><span class="sxs-lookup"><span data-stu-id="12b07-123">As a best practice, you must provide customization guidelines for app users and customers to follow when customizing your app.</span></span> <span data-ttu-id="12b07-124">Pour plus d’informations, voir [personnaliser les applications dans Microsoft Teams](/MicrosoftTeams/customize-apps).</span><span class="sxs-lookup"><span data-stu-id="12b07-124">For more information, see [customize apps in Microsoft Teams](/MicrosoftTeams/customize-apps).</span></span>

<span data-ttu-id="12b07-125">Voici les fonctionnalités :</span><span class="sxs-lookup"><span data-stu-id="12b07-125">Following are the capabilities:</span></span>

:::image type="content" source="~/assets/images/tdp/tdp_capabilities.png" alt-text="Screenshot showing the Configure page of Teams Developer Portal.":::

* <span data-ttu-id="12b07-127">**Application personnelle**</span><span class="sxs-lookup"><span data-stu-id="12b07-127">**Personal app**</span></span> 

  <span data-ttu-id="12b07-128">Cette section vous permet de définir un ensemble d’onglets présentés par défaut dans l’expérience d’application personnelle, c’est-à-dire l’expérience qu’un utilisateur a avec votre application en dehors du contexte d’une équipe ou d’un canal.</span><span class="sxs-lookup"><span data-stu-id="12b07-128">This section lets you define a set of tabs that are presented by default in the personal app experience, that is, the experience a user has with your app outside the context of a team or channel.</span></span> <span data-ttu-id="12b07-129">Dans cette section, fournissez les détails suivants :</span><span class="sxs-lookup"><span data-stu-id="12b07-129">In this section, provide the following details:</span></span>

  * <span data-ttu-id="12b07-130">Nom de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="12b07-130">The tab name.</span></span>
  * <span data-ttu-id="12b07-131">Identificateur unique.</span><span class="sxs-lookup"><span data-stu-id="12b07-131">A unique identifier.</span></span>
  * <span data-ttu-id="12b07-132">URL qui pointe vers l’interface utilisateur à afficher dans Teams.</span><span class="sxs-lookup"><span data-stu-id="12b07-132">The URL that points to the UI to be displayed in Teams.</span></span>
  * <span data-ttu-id="12b07-133">URL à utiliser si un utilisateur choisit d’afficher l’onglet dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="12b07-133">The URL to use if a user opts to view the tab in a browser.</span></span> <span data-ttu-id="12b07-134">Il s’agit d’une information facultative.</span><span class="sxs-lookup"><span data-stu-id="12b07-134">This is an optional information.</span></span>
  * <span data-ttu-id="12b07-135">Tous les domaines supplémentaires à partir des lesquels l’onglet s’attend à charger ou à laquelle établir un lien.</span><span class="sxs-lookup"><span data-stu-id="12b07-135">Any additional domains from which the tab expects to load from or link to.</span></span>

* <span data-ttu-id="12b07-136">**Application de groupe et de canal**</span><span class="sxs-lookup"><span data-stu-id="12b07-136">**Group and channel app**</span></span>

  <span data-ttu-id="12b07-137">Un onglet Teams fait partie d’un canal et fournit un accès rapide aux informations et ressources de l’équipe.</span><span class="sxs-lookup"><span data-stu-id="12b07-137">A Teams tab becomes part of a channel and provides quick access to team information and resources.</span></span> <span data-ttu-id="12b07-138">Par exemple, l’onglet Planificateur d’un canal contient un plan unique, l’onglet Power BI est mapmé à un rapport spécifique.</span><span class="sxs-lookup"><span data-stu-id="12b07-138">For example, the Planner tab for a channel contains a single plan, the Power BI tab maps to a specific report.</span></span> <span data-ttu-id="12b07-139">Les utilisateurs peuvent explorer le contexte approprié, mais ils ne peuvent pas naviguer en dehors de l’onglet. Par exemple, l’onglet Power BI n’active pas la navigation vers les autres rapports Power BI, mais il active le bouton **Accéder au site web** qui lance le rapport dans le site web principal de Power BI.</span><span class="sxs-lookup"><span data-stu-id="12b07-139">Users can drill down to the relevant context, but they should not be able to navigate outside the tab. The Power BI tab, for instance, doesn't enable navigation to other Power BI reports, but it does enable the **Go to website** button that launches the report in the main Power BI website.</span></span>

    > [!NOTE]
    > <span data-ttu-id="12b07-140">Pour les onglets d’équipe, vous devez fournir une URL de configuration pour présenter les options et collecter des informations, ce qui vous aiderait à personnaliser le contenu et l’expérience de votre onglet. Cette page HTML en iframed s’affiche lorsqu’un utilisateur ajoute pour la première fois l’onglet à un canal.</span><span class="sxs-lookup"><span data-stu-id="12b07-140">For team tabs, you must provide a Configuration URL to present options and gather information, that would help you to customize the content and experience of your tab. This iframed HTML page is displayed when a user first adds the tab to a channel.</span></span>
    > <span data-ttu-id="12b07-141">Vous devez également fournir d'autres domaines à partir desquels l'onglet doit être chargé ou lié.</span><span class="sxs-lookup"><span data-stu-id="12b07-141">You must also provide any additional domains that the tab expects to load from or link to.</span></span>

* <span data-ttu-id="12b07-142">**Bot**</span><span class="sxs-lookup"><span data-stu-id="12b07-142">**Bot**</span></span>

  <span data-ttu-id="12b07-143">Cette section vous permet d’ajouter un [bot conversation](~/bots/what-are-bots.md) à votre application.</span><span class="sxs-lookup"><span data-stu-id="12b07-143">This section allows you to add a [conversational bot](~/bots/what-are-bots.md) to your app.</span></span> <span data-ttu-id="12b07-144">Si vous avez déjà inscrit un bot auprès de Bot Framework, vous pouvez ajouter ce bot en cliquant sur **Configurer** et en fournissant le nom du bot, l’ID Bot Framework, et en définissant les étendues dans lesquelles le bot fonctionne.</span><span class="sxs-lookup"><span data-stu-id="12b07-144">If you already have a bot registered with Bot Framework, you can add that bot by clicking **Set Up** and supplying the bot's name, Bot Framework ID, and defining the scopes in which the bot will work.</span></span>

  <span data-ttu-id="12b07-145">Si vous n’avez pas encore inscrit le bot auprès de Bot Framework, cliquez sur **Enregistrer** pour en créer un nouveau.</span><span class="sxs-lookup"><span data-stu-id="12b07-145">If you have not registered the bot with the Bot Framework yet, click **Register** to create a new one.</span></span> <span data-ttu-id="12b07-146">Une fois que vous avez inscrit votre bot, revenir à cette section de l’Éditeur de manifeste pour entrer son nom et son ID Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="12b07-146">After you have registered your bot, come back to this section of the Manifest Editor to enter its name and Bot Framework ID.</span></span>

  <span data-ttu-id="12b07-147">Une fois que vous avez fourni les informations de votre bot, vous pouvez éventuellement définir une liste de commandes que votre bot peut suggérer aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="12b07-147">After you have supplied your bot's information, you can now optionally define a list of commands that your bot can suggest to users.</span></span> <span data-ttu-id="12b07-148">Ajoutez le nom de la commande, une description de celle-ci qui indique sa syntaxe et ses arguments, ainsi que l’étendue à laquelle cette commande doit s’appliquer.</span><span class="sxs-lookup"><span data-stu-id="12b07-148">Add the name of the command, a description of the command which indicates its syntax and arguments, and the scope(s) to which this command should apply.</span></span>

  <span data-ttu-id="12b07-149">Notez que si vous avez défini votre bot pour prendre en charge une seule étendue, les commandes spécifiées pour l’étendue non prise en charge seront ignorées.</span><span class="sxs-lookup"><span data-stu-id="12b07-149">Note that if you have defined your bot to only support one scope, commands specified for the unsupported scope will be ignored.</span></span> <span data-ttu-id="12b07-150">Vous pouvez modifier les étendues que votre bot prend en charge à tout moment.</span><span class="sxs-lookup"><span data-stu-id="12b07-150">You can edit the scopes your bot supports at any time.</span></span>

* <span data-ttu-id="12b07-151">**Connector**</span><span class="sxs-lookup"><span data-stu-id="12b07-151">**Connector**</span></span>

  <span data-ttu-id="12b07-152">Cette section vous permet d’ajouter un connecteur à votre application.</span><span class="sxs-lookup"><span data-stu-id="12b07-152">This section allows you to add a connector to your app.</span></span> <span data-ttu-id="12b07-153">Si vous avez déjà inscrit un connecteur  Office 365, sélectionnez Configurer et entrez le nom et l’ID du connecteur.</span><span class="sxs-lookup"><span data-stu-id="12b07-153">If you already have registered an Office 365 connector, select **Set up** and enter the name and ID of the connector.</span></span> <span data-ttu-id="12b07-154">Si vous voulez un nouveau connecteur, cliquez sur **S'inscrire** pour accéder au tableau de bord du développeur de connecteurs dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="12b07-154">If you want a new connector click **Register** to be taken to the Connector Developer Dashboard in your browser.</span></span>

  > [!NOTE]
  > <span data-ttu-id="12b07-155">La personnalisation d’application permet aux administrateurs de modifier l’apparence des applications chargées par le biais de bots, d’extensions de messagerie, d’onglets et de connecteurs.</span><span class="sxs-lookup"><span data-stu-id="12b07-155">App customization enables admins to change the look-and-feel of the apps loaded through bots, messaging extensions, tabs, and connectors.</span></span> <span data-ttu-id="12b07-156">Par exemple, si l’administrateur Teams personnalise le nom d’une application , l’application apparaît avec le nouveau nom pour `Contoso` `Contoso Agent` les `Contoso Agent` utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="12b07-156">For example, if the Teams admin customizes the name of an app from `Contoso` to `Contoso Agent`, then the app will appear with the new name `Contoso Agent` to the users.</span></span> <span data-ttu-id="12b07-157">Toutefois, lors de l’ajout d’un connecteur à une conversation, dans la liste, les connecteurs afficheront toujours le nom de l’application en tant que `Contoso` .</span><span class="sxs-lookup"><span data-stu-id="12b07-157">However, while adding a connector to a chat, in the list, the connectors will still show the name of the app as `Contoso`.</span></span>

* <span data-ttu-id="12b07-158">**Extensions de messagerie**</span><span class="sxs-lookup"><span data-stu-id="12b07-158">**Messaging Extensions**</span></span>

  <span data-ttu-id="12b07-159">[Les extensions de messagerie](~/messaging-extensions/what-are-messaging-extensions.md) sont un moyen puissant pour les utilisateurs de interagir avec votre application au sein de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="12b07-159">[Messaging extensions](~/messaging-extensions/what-are-messaging-extensions.md) are a powerful way for users to engage with your app within Microsoft Teams.</span></span> <span data-ttu-id="12b07-160">Les utilisateurs peuvent interroger les informations de votre service et publier ces informations sous forme de cartes, directement dans le canal ou la conversation instantanée.</span><span class="sxs-lookup"><span data-stu-id="12b07-160">Users can query for information from your service and post that information in the form of cards, right into the channel or chat conversation.</span></span>

  <span data-ttu-id="12b07-161">Les extensions de messagerie sont optimisées par des bots Bot Framework. Ils ont donc besoin d’un bot configuré pour opérer.</span><span class="sxs-lookup"><span data-stu-id="12b07-161">Messaging extensions are powered by Bot Framework bots, so they require a configured bot to operate.</span></span> <span data-ttu-id="12b07-162">Si vous avez le nom et l’ID Bot Framework du bot dont vous voulez power l’extension de messagerie, entrez-le.</span><span class="sxs-lookup"><span data-stu-id="12b07-162">If you have the name and Bot Framework ID of the bot you would like to power the messaging extension, enter it.</span></span> <span data-ttu-id="12b07-163">Sinon, cliquez sur *S'inscrire* pour en créer un, puis entrez les informations par la suite.</span><span class="sxs-lookup"><span data-stu-id="12b07-163">Otherwise, click *Register* to create one and enter the information afterward.</span></span> <span data-ttu-id="12b07-164">Choisissez si la configuration d’une extension de messagerie peut être mise à jour par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="12b07-164">Select whether the configuration of a messaging extension can be updated by the user.</span></span>

  <span data-ttu-id="12b07-165">Une fois le bot sous-jacent configuré, définissez les commandes et paramètres que l’extension de messagerie peut accepter.</span><span class="sxs-lookup"><span data-stu-id="12b07-165">After you have the underlying bot configured, define the commands and parameters which the messaging extension can accept.</span></span>

  <span data-ttu-id="12b07-166">Chaque commande nécessite un titre et un ID.</span><span class="sxs-lookup"><span data-stu-id="12b07-166">Each command requires a title and an ID.</span></span> <span data-ttu-id="12b07-167">La commande peut éventuellement contenir une description pour l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="12b07-167">The command can optionally contain a description for the user.</span></span> <span data-ttu-id="12b07-168">Chaque commande peut prendre en charge jusqu’à cinq paramètres, chacun nécessitant les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="12b07-168">Each command can support up to five parameters, each of which requires the following:</span></span>

  * <span data-ttu-id="12b07-169">Nom du paramètre tel qu’il apparaît dans Teams client et est inclus dans la demande de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="12b07-169">The name of the parameter as it appears in the Teams client and is included in the user request.</span></span>
  * <span data-ttu-id="12b07-170">Titre convivial.</span><span class="sxs-lookup"><span data-stu-id="12b07-170">A user-friendly title.</span></span>
  * <span data-ttu-id="12b07-171">Description facultative.</span><span class="sxs-lookup"><span data-stu-id="12b07-171">An optional description.</span></span>

  > [!NOTE]
  > <span data-ttu-id="12b07-172">Pour créer une extension de messagerie à l’aide d’App Studio, voir créer une [extension de messagerie à l’aide d’app studio.](~/resources/create-messaging-extension-using-appstudio.md)</span><span class="sxs-lookup"><span data-stu-id="12b07-172">To create messaging extension using app studio, see [create messaging extension using app studio](~/resources/create-messaging-extension-using-appstudio.md).</span></span>

* <span data-ttu-id="12b07-173">**Extension de réunion**</span><span class="sxs-lookup"><span data-stu-id="12b07-173">**Meeting extension**</span></span>

  <span data-ttu-id="12b07-174">TODO : Rajesh R.</span><span class="sxs-lookup"><span data-stu-id="12b07-174">//TODO: Rajesh R.</span></span>

* <span data-ttu-id="12b07-175">**Scene**</span><span class="sxs-lookup"><span data-stu-id="12b07-175">**Scene**</span></span>

  <span data-ttu-id="12b07-176">Scènes en mode Ensemble est un artefact créé par le développeur de scène à l’aide du studio de scène Microsoft qui réunit les personnes avec leur flux vidéo dans un paramètre créatif tel que le créateur de scène.</span><span class="sxs-lookup"><span data-stu-id="12b07-176">Scenes in Together Mode is an artifact created by the scene developer using the Microsoft Scene studio that brings people together along with their video stream in a creative setting as conceived by the scene creator.</span></span> <span data-ttu-id="12b07-177">Dans un paramètre de scène en cours, les participants ont des sièges désignés avec des flux vidéo restituer dans ces sièges.</span><span class="sxs-lookup"><span data-stu-id="12b07-177">In a conceived scene setting, participants have designated seats with video streams rendered in those seats.</span></span> <span data-ttu-id="12b07-178">Pour plus d’informations, [voir Teams mode Ensemble.](~/apps-in-teams-meetings/teams-together-mode.md)</span><span class="sxs-lookup"><span data-stu-id="12b07-178">For more information, see [Teams Together Mode](~/apps-in-teams-meetings/teams-together-mode.md).</span></span>

## <a name="permissions"></a><span data-ttu-id="12b07-179">Autorisations</span><span class="sxs-lookup"><span data-stu-id="12b07-179">Permissions</span></span>

<span data-ttu-id="12b07-180">Vous pouvez enrichir votre application Teams avec des fonctionnalités natives d’appareil, telles que la caméra, le microphone et l’emplacement.</span><span class="sxs-lookup"><span data-stu-id="12b07-180">You can enrich your Teams app with native device capabilities, such as camera, microphone, and location.</span></span>

## <a name="languages"></a><span data-ttu-id="12b07-181">Langages</span><span class="sxs-lookup"><span data-stu-id="12b07-181">Languages</span></span>

<span data-ttu-id="12b07-182">Configurer ou modifier les langues que votre application prend en charge.</span><span class="sxs-lookup"><span data-stu-id="12b07-182">Set up or change the languages that your app supports.</span></span>

## <a name="single-sign-on"></a><span data-ttu-id="12b07-183">Authentification unique</span><span class="sxs-lookup"><span data-stu-id="12b07-183">Single Sign-On</span></span>

<span data-ttu-id="12b07-184">Configurez votre application pour authentifier les utilisateurs avec l’authentification unique (SSO).</span><span class="sxs-lookup"><span data-stu-id="12b07-184">Configure your app to authenticate users with single sign-on (SSO).</span></span>

## <a name="domains"></a><span data-ttu-id="12b07-185">Domaines</span><span class="sxs-lookup"><span data-stu-id="12b07-185">Domains</span></span>

<span data-ttu-id="12b07-186">Liste des domaines valides pour les sites web que l’application s’attend à charger dans Teams client.</span><span class="sxs-lookup"><span data-stu-id="12b07-186">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="12b07-187">Les listes de domaines peuvent inclure des caractères génériques, par exemple, `*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="12b07-187">Domain listings can include wildcards, for example, `*.example.com`.</span></span> <span data-ttu-id="12b07-188">Cela correspond exactement à un segment du domaine ; si vous avez besoin d’une `a.b.example.com` correspondance, utilisez `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="12b07-188">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="12b07-189">Si votre interface utilisateur de contenu ou de configuration d’onglet doit accéder à un autre domaine en plus de celui utilisé pour la configuration de l’onglet, ce domaine doit être spécifié ici.</span><span class="sxs-lookup"><span data-stu-id="12b07-189">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="12b07-190">Il n’est pas nécessaire d’inclure les domaines des fournisseurs d’identité que vous souhaitez prendre en charge dans votre application.</span><span class="sxs-lookup"><span data-stu-id="12b07-190">It is not necessary to include the domains of the identity providers you want to support in your app.</span></span> <span data-ttu-id="12b07-191">Par exemple, pour vous authentifier à l’aide d’un ID Google, il est nécessaire de rediriger vers accounts.google.com, toutefois, vous ne devez pas inclure accounts.google.com dans `validDomains[]` .</span><span class="sxs-lookup"><span data-stu-id="12b07-191">For example, to authenticate using a Google ID, it is required to redirect to accounts.google.com, however, you must not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="12b07-192">Teams applications qui nécessitent leurs propres URL sharepoint pour fonctionner bien, inclut « {teamsitedomain} » dans leur liste de domaines valide.</span><span class="sxs-lookup"><span data-stu-id="12b07-192">Teams apps that require their own sharepoint URLs to function well, includes "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="12b07-193">N’ajoutez pas de domaines qui sont en dehors de votre contrôle, directement ou par le biais de caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="12b07-193">Do not add domains that are outside your control, either directly or through wildcards.</span></span> <span data-ttu-id="12b07-194">Par exemple, `yourapp.onmicrosoft.com` est valide, toutefois, `*.onmicrosoft.com` n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="12b07-194">For example, `yourapp.onmicrosoft.com` is valid, however, `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="12b07-195">L’objet est un tableau avec tous les éléments du type `string` .</span><span class="sxs-lookup"><span data-stu-id="12b07-195">The object is an array with all elements of the type `string`.</span></span>

## <a name="advanced"></a><span data-ttu-id="12b07-196">Avancé</span><span class="sxs-lookup"><span data-stu-id="12b07-196">Advanced</span></span>
<span data-ttu-id="12b07-197">Todo par Karthig</span><span class="sxs-lookup"><span data-stu-id="12b07-197">//Todo by Karthig</span></span>

### <a name="app-content"></a><span data-ttu-id="12b07-198">Contenu de l’application</span><span class="sxs-lookup"><span data-stu-id="12b07-198">App content</span></span>
<span data-ttu-id="12b07-199">Todo par Karthig</span><span class="sxs-lookup"><span data-stu-id="12b07-199">//Todo by Karthig</span></span>

### <a name="first-party-settings"></a><span data-ttu-id="12b07-200">Paramètres de première partie</span><span class="sxs-lookup"><span data-stu-id="12b07-200">First party settings</span></span>
<span data-ttu-id="12b07-201">Todo par Karthig</span><span class="sxs-lookup"><span data-stu-id="12b07-201">//Todo by Karthig</span></span>

## <a name="see-also"></a><span data-ttu-id="12b07-202">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="12b07-202">See also</span></span>

* [<span data-ttu-id="12b07-203">Vue d’ensemble Teams portail du développeur</span><span class="sxs-lookup"><span data-stu-id="12b07-203">Overview of Teams Developer Portal</span></span>](~/concepts/build-and-test/teams-developer-portal.md)
* [<span data-ttu-id="12b07-204">Distribuer Teams portail pour les développeurs</span><span class="sxs-lookup"><span data-stu-id="12b07-204">Distribute Teams Developer Portal</span></span>](~/concepts/tdp-distribute.md)
* [<span data-ttu-id="12b07-205">Outils du portail Teams développeur</span><span class="sxs-lookup"><span data-stu-id="12b07-205">Tools in Teams Developer Portal</span></span>](~/concepts/tdp-tools.md)