---
title: Ajouter Power Virtual Agents chatbot à Teams
author: laujan
description: l’intégration d Power Virtual Agents chatbot dans la plate-forme Teams
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 2a8f9c23eaa1acf2555b91cc4caf8d0f3298c114
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566116"
---
# <a name="add-power-virtual-agents-chatbot"></a><span data-ttu-id="a930f-103">Ajouter le chatbot Power Virtual Agents</span><span class="sxs-lookup"><span data-stu-id="a930f-103">Add Power Virtual Agents chatbot</span></span> 

<span data-ttu-id="a930f-104">Power Virtual Agents est une solution d’interface graphique guidée sans code qui permet à chaque membre de votre équipe de créer des chatbots riches et conversationnels qui s’intègrent facilement à la plate-forme Teams technologie.</span><span class="sxs-lookup"><span data-stu-id="a930f-104">Power Virtual Agents is a no-code, guided graphical interface solution that empowers every member of your team to create rich, conversational chatbots that easily integrate with the Teams platform.</span></span> <span data-ttu-id="a930f-105">Tout le contenu écrit dans Power Virtual Agents rend naturellement dans Teams.</span><span class="sxs-lookup"><span data-stu-id="a930f-105">All content authored in Power Virtual Agents renders naturally in Teams.</span></span> <span data-ttu-id="a930f-106">Power Virtual Agents bots s’engagent avec les utilisateurs dans Teams toile de chat natif.</span><span class="sxs-lookup"><span data-stu-id="a930f-106">Power Virtual Agents bots engage with users in the Teams native chat canvas.</span></span> <span data-ttu-id="a930f-107">Les administrateurs informatiques, les analystes d’entreprise, les spécialistes du domaine et les développeurs d’applications qualifiés peuvent concevoir, développer et publier des agents virtuels intelligents pour Teams sans avoir à configurer un environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="a930f-107">The IT administrators, business analysts, domain specialists, and skilled app developers can design, develop, and publish intelligent virtual agents for Teams without having to setup a development environment.</span></span> <span data-ttu-id="a930f-108">Ils peuvent créer un service Web ou s’inscrire directement au Cadre Bot.</span><span class="sxs-lookup"><span data-stu-id="a930f-108">They can create a web service, or directly register with the Bot Framework.</span></span> 

<span data-ttu-id="a930f-109">Ce document vous guide sur la façon de rendre votre chatbot disponible en Teams via le portail Power Virtual Agents, et d’ajouter votre bot à Teams en utilisant App Studio.</span><span class="sxs-lookup"><span data-stu-id="a930f-109">This document guides you on how to make your chatbot available in Teams through the Power Virtual Agents portal, and add your bot to Teams using App Studio.</span></span> 

<span data-ttu-id="a930f-110">Power Virtual Agents vous permet de créer de puissants chatbots qui peuvent répondre aux questions posées par vos clients, d’autres employés ou les visiteurs de votre site Web ou service.</span><span class="sxs-lookup"><span data-stu-id="a930f-110">Power Virtual Agents lets you create powerful chatbots that can answer questions posed by your customers, other employees, or visitors to your website or service.</span></span>

<span data-ttu-id="a930f-111">Ces bots peuvent être créés facilement sans avoir besoin de scientifiques ou de développeurs de données.</span><span class="sxs-lookup"><span data-stu-id="a930f-111">These bots can be created easily without the need for data scientists or developers.</span></span>

> [!NOTE]
> <span data-ttu-id="a930f-112">En ajoutant votre chatbot à Microsoft Teams, certaines données, telles que le contenu bot et le contenu du chat utilisateur, sont partagées avec Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="a930f-112">By adding your chatbot to Microsoft Teams, some of the data, such as bot content and user chat content, is shared with Microsoft Teams.</span></span> <span data-ttu-id="a930f-113">Cela signifie que vos données circulent en dehors de la conformité [de votre organisation et des frontières géographiques ou régionales.](/power-virtual-agents/data-location)</span><span class="sxs-lookup"><span data-stu-id="a930f-113">It means that your data flows outside of your [organization’s compliance and geographic or regional boundaries](/power-virtual-agents/data-location).</span></span> <br/>

## <a name="make-your-chatbot-available-in-teams-through-the-power-virtual-agents-portal"></a><span data-ttu-id="a930f-114">Rendez votre chatbot disponible en Teams le portail Power Virtual Agents vidéo</span><span class="sxs-lookup"><span data-stu-id="a930f-114">Make your chatbot available in Teams through the Power Virtual Agents portal</span></span>

<span data-ttu-id="a930f-115">Pour rendre votre chatbot disponible en Teams par le portail Power Virtual Agents, vous devez effectuer les étapes de processus suivantes :</span><span class="sxs-lookup"><span data-stu-id="a930f-115">To make your chatbot available in Teams through the Power Virtual Agents portal, you must perform the following process steps:</span></span>

<span data-ttu-id="a930f-116">**Pour rendre le chatbot disponible en Teams**</span><span class="sxs-lookup"><span data-stu-id="a930f-116">**To make the chatbot available in Teams**</span></span>

1. <span data-ttu-id="a930f-117">**Publier le dernier contenu bot**</span><span class="sxs-lookup"><span data-stu-id="a930f-117">**Publish the latest bot content**</span></span>  
<span data-ttu-id="a930f-118">Après avoir créé un chatbot dans le Power Virtual Agents, vous devez publier votre bot avant que Teams utilisateurs puissent interagir avec lui.</span><span class="sxs-lookup"><span data-stu-id="a930f-118">After creating a chatbot in the Power Virtual Agents portal, you must publish your bot before Teams users can interact with it.</span></span> <span data-ttu-id="a930f-119">Pour plus d’informations, [voir Publier le dernier contenu bot](/power-virtual-agents/publication-fundamentals-publish-channels#publish-the-latest-bot-content).</span><span class="sxs-lookup"><span data-stu-id="a930f-119">For more information, see [Publish the latest bot content](/power-virtual-agents/publication-fundamentals-publish-channels#publish-the-latest-bot-content).</span></span>

   ![publier dans le portail des agents virtuels de puissance](../../assets/images/pva-publish.png)

1. <span data-ttu-id="a930f-121">**Configurer le canal Teams’œil**</span><span class="sxs-lookup"><span data-stu-id="a930f-121">**Configure the Teams channel**</span></span>  
<span data-ttu-id="a930f-122">Après avoir publié votre bot, ajoutez le canal Teams pour mettre le bot à la disposition des Teams utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="a930f-122">After publishing your bot, add the Teams channel to make the bot available to Teams users.</span></span>

   ![canaux dans le portail des agents virtuels de puissance](../../assets/images/pva-channels.png)

1. <span data-ttu-id="a930f-124">**Générer un ID app pour votre chatbot**</span><span class="sxs-lookup"><span data-stu-id="a930f-124">**Generate an App ID for your chatbot**</span></span>  
<span data-ttu-id="a930f-125">Après avoir ajouté le Teams à votre chatbot, un identifiant **d’application est** généré dans la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="a930f-125">After adding the Teams channel to your chatbot, an **App ID** is generated in the dialog box.</span></span> <span data-ttu-id="a930f-126">L’ID app est un identifiant microsoft unique généré pour votre bot.</span><span class="sxs-lookup"><span data-stu-id="a930f-126">The App ID is a unique Microsoft generated identifier for your bot.</span></span> <span data-ttu-id="a930f-127">Enregistrez l’ID de l’application pour créer un package d’application pour Teams.</span><span class="sxs-lookup"><span data-stu-id="a930f-127">Save the App ID to create an app package for Teams.</span></span>

## <a name="add-your-bot-to-teams-using-app-studio"></a><span data-ttu-id="a930f-128">Ajoutez votre bot à votre Teams’utilisation d’App Studio</span><span class="sxs-lookup"><span data-stu-id="a930f-128">Add your bot to Teams using App Studio</span></span>

<span data-ttu-id="a930f-129">Si [le téléchargement d’applications personnalisées est](/microsoftteams/admin-settings) activé dans votre instance Teams, vous pouvez utiliser Teams App Studio pour télécharger directement votre chatbot et commencer à l’utiliser immédiatement.</span><span class="sxs-lookup"><span data-stu-id="a930f-129">If [uploading custom apps is enabled](/microsoftteams/admin-settings) in your Teams instance, you can use Teams App Studio to directly upload your chatbot and start using it immediately.</span></span> <span data-ttu-id="a930f-130">Pour partager votre chatbot, vous pouvez demander à votre administrateur de rendre votre bot disponible dans le catalogue d’applications locataires ou vous pouvez envoyer votre paquet d’applications à d’autres et leur demander de le télécharger indépendamment.</span><span class="sxs-lookup"><span data-stu-id="a930f-130">To share your chatbot, you can request your admin to make your bot available in the tenant app catalog or you can send your app package to others and ask them to upload it independently.</span></span>

1. <span data-ttu-id="a930f-131">**Installer App Studio dans Teams**</span><span class="sxs-lookup"><span data-stu-id="a930f-131">**Install App Studio in Teams**</span></span>  
<span data-ttu-id="a930f-132">App Studio est une application Teams gratuite.</span><span class="sxs-lookup"><span data-stu-id="a930f-132">App Studio is a Teams app.</span></span> <span data-ttu-id="a930f-133">Installez App Studio depuis le Teams qui simplifie le processus de création et d’enregistrement de bots en Teams :</span><span class="sxs-lookup"><span data-stu-id="a930f-133">Install App Studio from the Teams store that simplifies the process of bot creation and registration in Teams:</span></span> 

   1. <span data-ttu-id="a930f-134">Sélectionnez l’icône de l’App Store Teams’instance et recherchez **App Studio**.</span><span class="sxs-lookup"><span data-stu-id="a930f-134">Select the app store icon from Teams instance, and search for **App Studio**.</span></span>

      &emsp;&emsp; <img  width="450px" alt="Finding App Studio in the Store" src="../../assets/images/get-started/app-studio-store.png"/>   

   1. <span data-ttu-id="a930f-135">Sélectionnez **la vignette App Studio** et sélectionnez **Installer** dans la boîte de dialogue pop-up.</span><span class="sxs-lookup"><span data-stu-id="a930f-135">Select the **App Studio** tile and select **Install** in the pop-up dialog box.</span></span>

      &emsp;&emsp; <img  width="450px" alt="Installing App Studio" src="../../assets/images/get-started/app-studio-install.png"/>

1. <span data-ttu-id="a930f-136">**Créez le manifeste Teams’application dans App Studio**</span><span class="sxs-lookup"><span data-stu-id="a930f-136">**Create the Teams app manifest in App Studio**</span></span>  
<span data-ttu-id="a930f-137">Les bots en Teams sont définis par un fichier JSON manifeste d’application qui fournit les informations de base sur votre bot et ses capacités.</span><span class="sxs-lookup"><span data-stu-id="a930f-137">Bots in Teams are defined by an app manifest JSON file that provides the basic information about your bot and its capabilities.</span></span> <span data-ttu-id="a930f-138">Dans **App Studio**, sélectionnez Manifest **editor**, et **sélectionnez Créer une nouvelle application**.</span><span class="sxs-lookup"><span data-stu-id="a930f-138">In **App Studio**, select **Manifest editor**, and select **Create a new app**.</span></span>

    ![créer une nouvelle application](../../assets/images/get-started/create-new-app.png)

1. <span data-ttu-id="a930f-140">**Ajoutez les détails de votre bot**</span><span class="sxs-lookup"><span data-stu-id="a930f-140">**Add your bot details**</span></span>  
<span data-ttu-id="a930f-141">Complétez tous les champs requis.</span><span class="sxs-lookup"><span data-stu-id="a930f-141">Complete all the required fields.</span></span> <span data-ttu-id="a930f-142">Pour une description complète de chaque champ voir la [définition manifeste schéma](../../resources/schema/manifest-schema.md).</span><span class="sxs-lookup"><span data-stu-id="a930f-142">For a full description of each field see [manifest schema definition](../../resources/schema/manifest-schema.md).</span></span>

    ![ajouter les détails de l’application](../../assets/images/get-started/add-app-details.png)

1. <span data-ttu-id="a930f-144">**Configurer votre bot** Pour configurer le bot, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="a930f-144">**Set up your bot** To set-up the bot, perform the following steps:</span></span> 
     1. <span data-ttu-id="a930f-145">Ouvrez **l’onglet Bots.**</span><span class="sxs-lookup"><span data-stu-id="a930f-145">Open the **Bots** tab.</span></span> 
     1. <span data-ttu-id="a930f-146">Sélectionnez **Setup**  >  **Bot existant** et entrez le nom de votre bot.</span><span class="sxs-lookup"><span data-stu-id="a930f-146">Select **Setup** > **Existing bot** and enter the name of your bot.</span></span>

   ![Mise en place de bots](../../assets/images/get-started/bot-set-up.png) 

   <span data-ttu-id="a930f-148">L’image suivante montre comment configurer un bot existant :</span><span class="sxs-lookup"><span data-stu-id="a930f-148">The following image depicts how to set-up an existing bot:</span></span>      

   ![mise en place de bots existants](../../assets/images/get-started/existing-bot-set-up.png)
       
1. <span data-ttu-id="a930f-150">**Ajouter votre identifiant d’application**</span><span class="sxs-lookup"><span data-stu-id="a930f-150">**Add your App ID**</span></span>  
<span data-ttu-id="a930f-151">Pour ajouter votre identifiant d’application, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="a930f-151">To add your App ID, perform the following steps:</span></span>  
    1. <span data-ttu-id="a930f-152">Sélectionnez **Connecter un id bot différent et coller l’id** app que **vous** avez copié plus tôt.</span><span class="sxs-lookup"><span data-stu-id="a930f-152">Select **Connect to a different bot id** and paste the **App Id** you copied earlier.</span></span> 
    1. <span data-ttu-id="a930f-153">Sélectionnez **Scope**  >  **Personal**  >  **Save**.</span><span class="sxs-lookup"><span data-stu-id="a930f-153">Select **Scope** > **Personal** > **Save**.</span></span>

    ![ajouter l’id de l’application](../../assets/images/get-started/add-app-id.png)

1. <span data-ttu-id="a930f-155">**Ajouter des domaines valides pour votre bot**</span><span class="sxs-lookup"><span data-stu-id="a930f-155">**Add valid domains for your bot**</span></span>  
<span data-ttu-id="a930f-156">Cette étape n’est requise que si votre bot exige que l’utilisateur se connecte.</span><span class="sxs-lookup"><span data-stu-id="a930f-156">This step is only required if your bot requires the user to sign in.</span></span> <span data-ttu-id="a930f-157">Sélectionnez **domaines et autorisations** et dans le **domaine des domaines valides,** fournissez l’entrée suivante :</span><span class="sxs-lookup"><span data-stu-id="a930f-157">Select **Domains and permissions** and in the **Valid Domains** field, provide the following input:</span></span>

    ```bash
       token.botframework.com
    ```

1. <span data-ttu-id="a930f-158">**Testez et distribuez votre bot**</span><span class="sxs-lookup"><span data-stu-id="a930f-158">**Test and distribute your bot**</span></span>  
<span data-ttu-id="a930f-159">Ouvrez **test et distribuez** l’onglet **et** sélectionnez Installer pour ajouter votre bot directement à votre Teams instance.</span><span class="sxs-lookup"><span data-stu-id="a930f-159">Open **Test and distribute** tab and select **Install** to add your bot directly to your Teams instance.</span></span> <span data-ttu-id="a930f-160">Alternativement, vous pouvez télécharger le package d’application complété à partager avec les utilisateurs de Teams ou le fournir à votre administrateur pour rendre votre bot disponible dans le catalogue d’applications locataires.</span><span class="sxs-lookup"><span data-stu-id="a930f-160">Alternately, you can download the completed app package to share with Teams users or provide it to your admin to make your bot available in the tenant app catalog.</span></span>

1. <span data-ttu-id="a930f-161">**Démarrer un chat** </span><span class="sxs-lookup"><span data-stu-id="a930f-161">**Start a chat** </span></span>  
<span data-ttu-id="a930f-162">Le processus de mise en place pour l’ajout de votre Power Virtual Agents bot de chat à Teams est complet.</span><span class="sxs-lookup"><span data-stu-id="a930f-162">The set-up process for adding your Power Virtual Agents chat bot to Teams is complete.</span></span> <span data-ttu-id="a930f-163">Vous pouvez maintenant commencer une conversation avec votre bot dans un chat personnel.</span><span class="sxs-lookup"><span data-stu-id="a930f-163">You can now start a conversation with your bot in a personal chat.</span></span>

## <a name="see-also"></a><span data-ttu-id="a930f-164">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="a930f-164">See also</span></span>

- [<span data-ttu-id="a930f-165">Power Virtual Agents</span><span class="sxs-lookup"><span data-stu-id="a930f-165">Power Virtual Agents</span></span>](/power-virtual-agents/fundamentals-what-is-power-virtual-agents)  

- <span data-ttu-id="a930f-166">[Créez un chatbot pour Teams avec Microsoft Power Virtual Agents](../bot-features.md#bots-and-the-microsoft-power-virtual-agents).</span><span class="sxs-lookup"><span data-stu-id="a930f-166">[Create a chatbot for Teams with Microsoft Power Virtual Agents](../bot-features.md#bots-and-the-microsoft-power-virtual-agents).</span></span>  

- [<span data-ttu-id="a930f-167">portail Power Virtual Agents’information</span><span class="sxs-lookup"><span data-stu-id="a930f-167">Power Virtual Agents portal</span></span>](https://powervirtualagents.microsoft.com)

- [<span data-ttu-id="a930f-168">Publiez votre bot Power Virtual Agents</span><span class="sxs-lookup"><span data-stu-id="a930f-168">Publish your Power Virtual Agents bot</span></span>](/power-virtual-agents/publication-fundamentals-publish-channels)

- <span data-ttu-id="a930f-169">[Sécurité et conformité dans Microsoft Teams](/MicrosoftTeams/security-compliance-overview).</span><span class="sxs-lookup"><span data-stu-id="a930f-169">[Security and compliance in Microsoft Teams](/MicrosoftTeams/security-compliance-overview).</span></span>

## <a name="next-step"></a><span data-ttu-id="a930f-170">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="a930f-170">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a930f-171">Créer un assistant virtuel</span><span class="sxs-lookup"><span data-stu-id="a930f-171">Create virtual assistant</span></span>](~/samples/virtual-assistant.md)

