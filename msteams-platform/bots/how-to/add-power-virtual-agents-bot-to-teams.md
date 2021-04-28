---
title: Ajouter un chatbot d'agents virtuels Power à Teams
author: laujan
description: intégration d'un chatbot d'agents virtuels Power dans la plateforme Teams
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: bd1528d06f9e9f4ca3a03f167ecb3c537977fb61
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058620"
---
# <a name="add-power-virtual-agents-chatbot"></a><span data-ttu-id="bb740-103">Ajouter un chatbot d'agents virtuels Power</span><span class="sxs-lookup"><span data-stu-id="bb740-103">Add Power Virtual Agents chatbot</span></span> 

<span data-ttu-id="bb740-104">Power Virtual Agents est une solution d'interface graphique guidée sans code qui permet à chaque membre de votre équipe de créer des chatbots riches et conversationnels qui s'intègrent facilement à la plateforme Teams.</span><span class="sxs-lookup"><span data-stu-id="bb740-104">Power Virtual Agents is a no-code, guided graphical interface solution that empowers every member of your team to create rich, conversational chatbots that easily integrate with the Teams platform.</span></span> <span data-ttu-id="bb740-105">Tout le contenu rédigé dans Power Virtual Agents s'restituera naturellement dans Teams.</span><span class="sxs-lookup"><span data-stu-id="bb740-105">All content authored in Power Virtual Agents renders naturally in Teams.</span></span> <span data-ttu-id="bb740-106">Les bots Power Virtual Agents s'engagent avec les utilisateurs dans le canevas de conversation native Teams.</span><span class="sxs-lookup"><span data-stu-id="bb740-106">Power Virtual Agents bots engage with users in the Teams native chat canvas.</span></span> <span data-ttu-id="bb740-107">Les administrateurs informatiques, les analystes d'entreprise, les spécialistes de domaines et les développeurs d'applications compétents peuvent concevoir, développer et publier des agents virtuels intelligents pour Teams sans avoir à configurer un environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="bb740-107">The IT administrators, business analysts, domain specialists, and skilled app developers can design, develop and publish intelligent virtual agents for Teams without having to setup a development environment.</span></span> <span data-ttu-id="bb740-108">Ils peuvent créer un service web ou s'inscrire directement auprès de Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="bb740-108">They can create a web service, or directly register with the Bot Framework.</span></span> 

<span data-ttu-id="bb740-109">Ce document vous guide sur la façon de rendre votre chatbot disponible dans Teams via le portail Power Virtual Agents et d'ajouter votre bot à Teams à l'aide d'App Studio.</span><span class="sxs-lookup"><span data-stu-id="bb740-109">This document guides you on how to make your chatbot available in Teams through the Power Virtual Agents portal, and add your bot to Teams using App Studio.</span></span> 

<span data-ttu-id="bb740-110">Power Virtual Agents vous permet de créer des chatbots puissants qui peuvent répondre aux questions posées par vos clients, d'autres employés ou les visiteurs de votre site web ou service.</span><span class="sxs-lookup"><span data-stu-id="bb740-110">Power Virtual Agents lets you create powerful chatbots that can answer questions posed by your customers, other employees, or visitors to your website or service.</span></span>

<span data-ttu-id="bb740-111">Ces bots peuvent être créés facilement sans avoir besoin de développeurs ou de développeurs.</span><span class="sxs-lookup"><span data-stu-id="bb740-111">These bots can be created easily without the need for data scientists or developers.</span></span>

> [!NOTE]
> <span data-ttu-id="bb740-112">En ajoutant votre chatbot à Microsoft Teams, certaines données, telles que le contenu du bot et le contenu de conversation utilisateur, sont partagées avec Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="bb740-112">By adding your chatbot to Microsoft Teams, some of the data, such as bot content and user chat content, is shared with Microsoft Teams.</span></span> <span data-ttu-id="bb740-113">Cela signifie que vos données sont en dehors des limites de conformité et géographiques [ou régionales de votre organisation.](/power-virtual-agents/data-location)</span><span class="sxs-lookup"><span data-stu-id="bb740-113">It means that your data flows outside of your [organization’s compliance and geographic or regional boundaries](/power-virtual-agents/data-location).</span></span> <br/>

## <a name="make-your-chatbot-available-in-teams-through-the-power-virtual-agents-portal"></a><span data-ttu-id="bb740-114">Rendre votre chatbot disponible dans Teams via le portail Power Virtual Agents</span><span class="sxs-lookup"><span data-stu-id="bb740-114">Make your chatbot available in Teams through the Power Virtual Agents portal</span></span>

<span data-ttu-id="bb740-115">Pour rendre votre chatbot disponible dans Teams via le portail Power Virtual Agents, vous devez effectuer les étapes de processus suivantes :</span><span class="sxs-lookup"><span data-stu-id="bb740-115">To make your chatbot available in Teams through the Power Virtual Agents portal, you must perform the following process steps:</span></span>

<span data-ttu-id="bb740-116">**Pour rendre le chatbot disponible dans Teams**</span><span class="sxs-lookup"><span data-stu-id="bb740-116">**To make the chatbot available in Teams**</span></span>

1. <span data-ttu-id="bb740-117">**Publier le contenu du bot le plus récent**</span><span class="sxs-lookup"><span data-stu-id="bb740-117">**Publish the latest bot content**</span></span>  
<span data-ttu-id="bb740-118">Après avoir créé un chatbot dans le portail Power Virtual Agents, vous devez publier votre bot pour que les utilisateurs de Teams peuvent interagir avec celui-ci.</span><span class="sxs-lookup"><span data-stu-id="bb740-118">After creating a chatbot in the Power Virtual Agents portal, you must publish your bot before Teams users can interact with it.</span></span> <span data-ttu-id="bb740-119">Pour plus d'informations, [voir Publier le contenu du bot le plus récent.](/power-virtual-agents/publication-fundamentals-publish-channels#publish-the-latest-bot-content)</span><span class="sxs-lookup"><span data-stu-id="bb740-119">For more information, see [Publish the latest bot content](/power-virtual-agents/publication-fundamentals-publish-channels#publish-the-latest-bot-content).</span></span>

   ![publier dans le portail des agents virtuels d'alimentation](../../assets/images/pva-publish.png)

1. <span data-ttu-id="bb740-121">**Configurer le canal Teams**</span><span class="sxs-lookup"><span data-stu-id="bb740-121">**Configure the Teams channel**</span></span>  
<span data-ttu-id="bb740-122">Après avoir publié votre bot, ajoutez le canal Teams pour le rendre accessible aux utilisateurs de Teams.</span><span class="sxs-lookup"><span data-stu-id="bb740-122">After publishing your bot, add the Teams channel to make the bot available to Teams users.</span></span>

   ![canaux dans le portail des agents virtuels d'alimentation](../../assets/images/pva-channels.png)

1. <span data-ttu-id="bb740-124">**Générer un ID d'application pour votre chatbot**</span><span class="sxs-lookup"><span data-stu-id="bb740-124">**Generate an App ID for your chatbot**</span></span>  
<span data-ttu-id="bb740-125">Après avoir ajouté le canal Teams à votre chatbot, un **ID** d'application est généré dans la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="bb740-125">After adding the Teams channel to your chatbot, an **App ID** is generated in the dialog box.</span></span> <span data-ttu-id="bb740-126">L'ID d'application est un identificateur Microsoft unique généré pour votre bot.</span><span class="sxs-lookup"><span data-stu-id="bb740-126">The App ID is a unique Microsoft generated identifier for your bot.</span></span> <span data-ttu-id="bb740-127">Enregistrez l'ID d'application pour créer un package d'application pour Teams.</span><span class="sxs-lookup"><span data-stu-id="bb740-127">Save the App ID to create an app package for Teams.</span></span>

## <a name="add-your-bot-to-teams-using-app-studio"></a><span data-ttu-id="bb740-128">Ajouter votre bot à Teams à l'aide d'App Studio</span><span class="sxs-lookup"><span data-stu-id="bb740-128">Add your bot to Teams using App Studio</span></span>

<span data-ttu-id="bb740-129">Si [le téléchargement d'applications](/microsoftteams/admin-settings) personnalisées est activé dans votre instance Teams, vous pouvez utiliser Teams App Studio pour télécharger directement votre chatbot et commencer à l'utiliser immédiatement.</span><span class="sxs-lookup"><span data-stu-id="bb740-129">If [uploading custom apps is enabled](/microsoftteams/admin-settings) in your Teams instance, you can use Teams App Studio to directly upload your chatbot and start using it immediately.</span></span> <span data-ttu-id="bb740-130">Pour partager votre chatbot, vous pouvez demander à votre administrateur de rendre votre bot disponible dans le catalogue d'applications client ou vous pouvez envoyer votre package d'application à d'autres utilisateurs et leur demander de le télécharger indépendamment.</span><span class="sxs-lookup"><span data-stu-id="bb740-130">To share your chatbot, you can request your admin to make your bot available in the tenant app catalog or you can send your app package to others and ask them to upload it independently.</span></span>

1. <span data-ttu-id="bb740-131">**Installer App Studio dans Teams**</span><span class="sxs-lookup"><span data-stu-id="bb740-131">**Install App Studio in Teams**</span></span>  
<span data-ttu-id="bb740-132">App Studio est une application Teams.</span><span class="sxs-lookup"><span data-stu-id="bb740-132">App Studio is a Teams app.</span></span> <span data-ttu-id="bb740-133">Installez App Studio à partir du magasin Teams qui simplifie le processus de création et d'inscription du bot dans Teams :</span><span class="sxs-lookup"><span data-stu-id="bb740-133">Install App Studio from the Teams store that simplifies the process of bot creation and registration in Teams:</span></span> 

   1. <span data-ttu-id="bb740-134">Sélectionnez l'icône du Magasin d'applications à partir de l'instance Teams, puis **recherchez App Studio.**</span><span class="sxs-lookup"><span data-stu-id="bb740-134">Select the app store icon from Teams instance, and search for **App Studio**.</span></span>

      &emsp;&emsp; <img  width="450px" alt="Finding App Studio in the Store" src="../../assets/images/get-started/app-studio-store.png"/>   

   1. <span data-ttu-id="bb740-135">Sélectionnez **la vignette App Studio** et **sélectionnez Installer** dans la boîte de dialogue qui s'affiche.</span><span class="sxs-lookup"><span data-stu-id="bb740-135">Select the **App Studio** tile and select **Install** in the pop-up dialog box.</span></span>

      &emsp;&emsp; <img  width="450px" alt="Installing App Studio" src="../../assets/images/get-started/app-studio-install.png"/>

1. <span data-ttu-id="bb740-136">**Créer le manifeste de l'application Teams dans App Studio**</span><span class="sxs-lookup"><span data-stu-id="bb740-136">**Create the Teams app manifest in App Studio**</span></span>  
<span data-ttu-id="bb740-137">Les bots dans Teams sont définis par un fichier JSON de manifeste d'application qui fournit les informations de base sur votre bot et ses fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="bb740-137">Bots in Teams are defined by an app manifest JSON file that provides the basic information about your bot and its capabilities.</span></span> <span data-ttu-id="bb740-138">Dans **App Studio,** sélectionnez **l'éditeur de** manifeste, puis **sélectionnez Créer une application.**</span><span class="sxs-lookup"><span data-stu-id="bb740-138">In **App Studio**, select **Manifest editor**, and select **Create a new app**.</span></span>  
<span data-ttu-id="bb740-139">L'image suivante vous guide pour créer une application dans App Studio :</span><span class="sxs-lookup"><span data-stu-id="bb740-139">The following image guides you to create a new app in App Studio:</span></span>  

   ![créer une application](../../assets/images/get-started/create-new-app.png)

1. <span data-ttu-id="bb740-141">**Ajouter les détails de votre bot**</span><span class="sxs-lookup"><span data-stu-id="bb740-141">**Add your bot details**</span></span>  
<span data-ttu-id="bb740-142">Remplissez tous les champs requis.</span><span class="sxs-lookup"><span data-stu-id="bb740-142">Complete all the required fields.</span></span> <span data-ttu-id="bb740-143">Pour obtenir une description complète de chaque champ, voir [la définition du schéma de manifeste.](../../resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="bb740-143">For a full description of each field see [manifest schema definition](../../resources/schema/manifest-schema.md).</span></span>   
<span data-ttu-id="bb740-144">L'image suivante vous guide pour ajouter les détails de l'application :</span><span class="sxs-lookup"><span data-stu-id="bb740-144">The following image guides you to add the app details:</span></span>  

   ![ajouter des détails sur l'application](../../assets/images/get-started/add-app-details.png)

1. <span data-ttu-id="bb740-146">**Configurer votre bot** Pour configurer le bot, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="bb740-146">**Set up your bot** To set-up the bot, perform the following steps:</span></span> 
     1. <span data-ttu-id="bb740-147">Ouvrez **l'onglet Bots.**</span><span class="sxs-lookup"><span data-stu-id="bb740-147">Open the **Bots** tab.</span></span> 
     1. <span data-ttu-id="bb740-148">Sélectionnez   >  **Installer le bot existant** et entrez le nom de votre bot.</span><span class="sxs-lookup"><span data-stu-id="bb740-148">Select **Setup** > **Existing bot** and enter the name of your bot.</span></span>

   <span data-ttu-id="bb740-149">L'image suivante vous guide pour configurer un bot :</span><span class="sxs-lookup"><span data-stu-id="bb740-149">The following image guides you to set-up a bot:</span></span>    

   ![Mise en place d'un bot](../../assets/images/get-started/bot-set-up.png) 

   <span data-ttu-id="bb740-151">L'image suivante vous guide pour configurer un bot existant :</span><span class="sxs-lookup"><span data-stu-id="bb740-151">The following image guides you to set-up an existing bot:</span></span>      

   ![mise en place d'un bot existant](../../assets/images/get-started/existing-bot-set-up.png)    
1. <span data-ttu-id="bb740-153">**Ajouter votre ID d'application**</span><span class="sxs-lookup"><span data-stu-id="bb740-153">**Add your App ID**</span></span>  
<span data-ttu-id="bb740-154">Pour ajouter votre ID d'application, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="bb740-154">To add your App ID, perform the following steps:</span></span>  
    1. <span data-ttu-id="bb740-155">Sélectionnez **Se connecter à un autre ID de bot** et collez l'ID d'application que vous avez copié précédemment. </span><span class="sxs-lookup"><span data-stu-id="bb740-155">Select **Connect to a different bot id** and paste the **App Id** you copied earlier.</span></span> 
    1. <span data-ttu-id="bb740-156">Sélectionnez   >  **l'étendue d'enregistrer**  >  **personnel**.</span><span class="sxs-lookup"><span data-stu-id="bb740-156">Select **Scope** > **Personal** > **Save**.</span></span>      
<span data-ttu-id="bb740-157">L'image suivante vous guide pour configurer un bot existant :</span><span class="sxs-lookup"><span data-stu-id="bb740-157">The following image guides you to set-up an existing bot:</span></span>    

   ![ajouter un ID d'application](../../assets/images/get-started/add-app-id.png)

1. <span data-ttu-id="bb740-159">**Ajouter des domaines valides pour votre bot**</span><span class="sxs-lookup"><span data-stu-id="bb740-159">**Add valid domains for your bot**</span></span>  
<span data-ttu-id="bb740-160">Cette étape est requise uniquement si votre bot nécessite que l'utilisateur se connecte.</span><span class="sxs-lookup"><span data-stu-id="bb740-160">This step is only required if your bot requires the user to sign in.</span></span> <span data-ttu-id="bb740-161">Sélectionnez **Domaines et autorisations et,** dans le **champ Domaines valides,** fournissez l'entrée suivante :</span><span class="sxs-lookup"><span data-stu-id="bb740-161">Select **Domains and permissions** and in the **Valid Domains** field, provide the following input:</span></span>

    ```bash
       token.botframework.com
    ```

7.  <span data-ttu-id="bb740-162">**Tester et distribuer votre bot**</span><span class="sxs-lookup"><span data-stu-id="bb740-162">**Test and distribute your bot**</span></span>  
<span data-ttu-id="bb740-163">Ouvrez **Test et distribuez** l'onglet, puis **sélectionnez Installer** pour ajouter votre bot directement à votre instance Teams.</span><span class="sxs-lookup"><span data-stu-id="bb740-163">Open **Test and distribute** tab and select **Install** to add your bot directly to your Teams instance.</span></span> <span data-ttu-id="bb740-164">Vous pouvez également télécharger le package d'application terminé pour le partager avec les utilisateurs de Teams ou le fournir à votre administrateur pour que votre bot soit disponible dans le catalogue d'applications client.</span><span class="sxs-lookup"><span data-stu-id="bb740-164">Alternately, you can download the completed app package to share with Teams users or provide it to your admin to make your bot available in the tenant app catalog.</span></span>

8. <span data-ttu-id="bb740-165">**Démarrer une conversation** </span><span class="sxs-lookup"><span data-stu-id="bb740-165">**Start a chat** </span></span>  
<span data-ttu-id="bb740-166">Le processus de mise en place de l'ajout de votre bot de conversation Power Virtual Agents à Teams est terminé.</span><span class="sxs-lookup"><span data-stu-id="bb740-166">The set-up process for adding your Power Virtual Agents chat bot to Teams is complete.</span></span> <span data-ttu-id="bb740-167">Vous pouvez maintenant démarrer une conversation avec votre bot dans une conversation personnelle.</span><span class="sxs-lookup"><span data-stu-id="bb740-167">You can now start a conversation with your bot in a personal chat.</span></span>

## <a name="see-also"></a><span data-ttu-id="bb740-168">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="bb740-168">See also</span></span>

- [<span data-ttu-id="bb740-169">Power Virtual Agents</span><span class="sxs-lookup"><span data-stu-id="bb740-169">Power Virtual Agents</span></span>](/power-virtual-agents/fundamentals-what-is-power-virtual-agents)  

- <span data-ttu-id="bb740-170">[Créez un chatbot pour Teams avec les agents virtuels Microsoft Power.](../bot-features.md#bots-and-the-microsoft-power-virtual-agents)</span><span class="sxs-lookup"><span data-stu-id="bb740-170">[Create a chatbot for Teams with Microsoft Power Virtual Agents](../bot-features.md#bots-and-the-microsoft-power-virtual-agents).</span></span>  

- [<span data-ttu-id="bb740-171">Portail Power Virtual Agents</span><span class="sxs-lookup"><span data-stu-id="bb740-171">Power Virtual Agents portal</span></span>](https://powervirtualagents.microsoft.com)

- [<span data-ttu-id="bb740-172">Publier votre bot d'agents virtuels Power</span><span class="sxs-lookup"><span data-stu-id="bb740-172">Publish your Power Virtual Agents bot</span></span>](/power-virtual-agents/publication-fundamentals-publish-channels)

- <span data-ttu-id="bb740-173">[Sécurité et conformité dans Microsoft Teams.](/MicrosoftTeams/security-compliance-overview)</span><span class="sxs-lookup"><span data-stu-id="bb740-173">[Security and compliance in Microsoft Teams](/MicrosoftTeams/security-compliance-overview).</span></span>

## <a name="next-step"></a><span data-ttu-id="bb740-174">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="bb740-174">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bb740-175">Créer un assistant virtuel</span><span class="sxs-lookup"><span data-stu-id="bb740-175">Create virtual assistant</span></span>](~/samples/virtual-assistant.md)

