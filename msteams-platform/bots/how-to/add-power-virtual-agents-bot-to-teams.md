---
title: Ajouter Power Virtual Agents chatbot à Teams
author: surbhigupta
description: intégration d’un Power Virtual Agents chatbot dans la plateforme Teams web
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 85f2d91d2c5cfdb0ae746a00c7a9f3d6a0c15972
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069022"
---
# <a name="add-power-virtual-agents-chatbot"></a><span data-ttu-id="1b24c-103">Ajouter le chatbot Power Virtual Agents</span><span class="sxs-lookup"><span data-stu-id="1b24c-103">Add Power Virtual Agents chatbot</span></span> 

<span data-ttu-id="1b24c-104">Power Virtual Agents est une solution d’interface graphique guidée sans code qui permet à chaque membre de votre équipe de créer des chatbots riches et conversationnels qui s’intègrent facilement à la plateforme Teams web.</span><span class="sxs-lookup"><span data-stu-id="1b24c-104">Power Virtual Agents is a no-code, guided graphical interface solution that empowers every member of your team to create rich, conversational chatbots that easily integrate with the Teams platform.</span></span> <span data-ttu-id="1b24c-105">Tout le contenu rédigé dans Power Virtual Agents s’restituera naturellement dans Teams.</span><span class="sxs-lookup"><span data-stu-id="1b24c-105">All content authored in Power Virtual Agents renders naturally in Teams.</span></span> <span data-ttu-id="1b24c-106">Power Virtual Agents bots s’engagent avec les utilisateurs dans le Teams de conversation native.</span><span class="sxs-lookup"><span data-stu-id="1b24c-106">Power Virtual Agents bots engage with users in the Teams native chat canvas.</span></span> <span data-ttu-id="1b24c-107">Les administrateurs informatiques, les analystes d’entreprise, les spécialistes de domaines et les développeurs d’applications compétents peuvent concevoir, développer et publier des agents virtuels intelligents pour Teams sans avoir à configurer un environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="1b24c-107">The IT administrators, business analysts, domain specialists, and skilled app developers can design, develop, and publish intelligent virtual agents for Teams without having to setup a development environment.</span></span> <span data-ttu-id="1b24c-108">Ils peuvent créer un service web ou s’inscrire directement auprès de Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="1b24c-108">They can create a web service, or directly register with the Bot Framework.</span></span> 

<span data-ttu-id="1b24c-109">Ce document vous guide sur la façon de rendre votre chatbot disponible dans Teams via le portail Power Virtual Agents et d’ajouter votre bot à Teams à l’aide d’App Studio.</span><span class="sxs-lookup"><span data-stu-id="1b24c-109">This document guides you on how to make your chatbot available in Teams through the Power Virtual Agents portal, and add your bot to Teams using App Studio.</span></span> 

<span data-ttu-id="1b24c-110">Power Virtual Agents vous permet de créer des chatbots puissants qui peuvent répondre aux questions posées par vos clients, d’autres employés ou les visiteurs de votre site web ou service.</span><span class="sxs-lookup"><span data-stu-id="1b24c-110">Power Virtual Agents lets you create powerful chatbots that can answer questions posed by your customers, other employees, or visitors to your website or service.</span></span>

<span data-ttu-id="1b24c-111">Ces bots peuvent être créés facilement sans avoir besoin de développeurs ou de développeurs.</span><span class="sxs-lookup"><span data-stu-id="1b24c-111">These bots can be created easily without the need for data scientists or developers.</span></span>

> [!NOTE]
> <span data-ttu-id="1b24c-112">En ajoutant votre chatbot à Microsoft Teams, certaines données, telles que le contenu du bot et le contenu de conversation utilisateur, sont partagées avec Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="1b24c-112">By adding your chatbot to Microsoft Teams, some of the data, such as bot content and user chat content, is shared with Microsoft Teams.</span></span> <span data-ttu-id="1b24c-113">Cela signifie que vos données sont en dehors des limites de conformité et géographiques [ou régionales de votre organisation.](/power-virtual-agents/data-location)</span><span class="sxs-lookup"><span data-stu-id="1b24c-113">It means that your data flows outside of your [organization’s compliance and geographic or regional boundaries](/power-virtual-agents/data-location).</span></span> <br/>

## <a name="make-your-chatbot-available-in-teams-through-the-power-virtual-agents-portal"></a><span data-ttu-id="1b24c-114">Rendre votre chatbot disponible dans Teams via le portail Power Virtual Agents web</span><span class="sxs-lookup"><span data-stu-id="1b24c-114">Make your chatbot available in Teams through the Power Virtual Agents portal</span></span>

<span data-ttu-id="1b24c-115">Pour rendre votre chatbot disponible dans Teams via le portail Power Virtual Agents, vous devez effectuer les étapes de processus suivantes :</span><span class="sxs-lookup"><span data-stu-id="1b24c-115">To make your chatbot available in Teams through the Power Virtual Agents portal, you must perform the following process steps:</span></span>

<span data-ttu-id="1b24c-116">**Pour rendre le chatbot disponible dans Teams**</span><span class="sxs-lookup"><span data-stu-id="1b24c-116">**To make the chatbot available in Teams**</span></span>

1. <span data-ttu-id="1b24c-117">**Publier le contenu du bot le plus récent**</span><span class="sxs-lookup"><span data-stu-id="1b24c-117">**Publish the latest bot content**</span></span>  
<span data-ttu-id="1b24c-118">Après avoir créé un chatbot dans le portail Power Virtual Agents, vous devez publier votre bot pour que Teams utilisateurs puisse interagir avec celui-ci.</span><span class="sxs-lookup"><span data-stu-id="1b24c-118">After creating a chatbot in the Power Virtual Agents portal, you must publish your bot before Teams users can interact with it.</span></span> <span data-ttu-id="1b24c-119">Pour plus d’informations, voir [Publier le contenu du bot le plus récent.](/power-virtual-agents/publication-fundamentals-publish-channels#publish-the-latest-bot-content)</span><span class="sxs-lookup"><span data-stu-id="1b24c-119">For more information, see [Publish the latest bot content](/power-virtual-agents/publication-fundamentals-publish-channels#publish-the-latest-bot-content).</span></span>

   ![publier dans le portail des agents virtuels avec alimentation](../../assets/images/pva-publish.png)

1. <span data-ttu-id="1b24c-121">**Configurer le canal Teams canal**</span><span class="sxs-lookup"><span data-stu-id="1b24c-121">**Configure the Teams channel**</span></span>  
<span data-ttu-id="1b24c-122">Après avoir publié votre bot, ajoutez le canal Teams pour le mettre à la disposition Teams utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="1b24c-122">After publishing your bot, add the Teams channel to make the bot available to Teams users.</span></span>

   ![canaux dans le portail des agents virtuels d’alimentation](../../assets/images/pva-channels.png)

1. <span data-ttu-id="1b24c-124">**Générer un ID d’application pour votre chatbot**</span><span class="sxs-lookup"><span data-stu-id="1b24c-124">**Generate an App ID for your chatbot**</span></span>  
<span data-ttu-id="1b24c-125">Après avoir ajouté le Teams à votre chatbot, un **ID** d’application est généré dans la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1b24c-125">After adding the Teams channel to your chatbot, an **App ID** is generated in the dialog box.</span></span> <span data-ttu-id="1b24c-126">L’ID d’application est un identificateur Microsoft unique généré pour votre bot.</span><span class="sxs-lookup"><span data-stu-id="1b24c-126">The App ID is a unique Microsoft generated identifier for your bot.</span></span> <span data-ttu-id="1b24c-127">Enregistrez l’ID d’application pour créer un package d’application Teams.</span><span class="sxs-lookup"><span data-stu-id="1b24c-127">Save the App ID to create an app package for Teams.</span></span>

## <a name="add-your-bot-to-teams-using-app-studio"></a><span data-ttu-id="1b24c-128">Ajouter votre bot à Teams à l’aide d’App Studio</span><span class="sxs-lookup"><span data-stu-id="1b24c-128">Add your bot to Teams using App Studio</span></span>

<span data-ttu-id="1b24c-129">Si [le](/microsoftteams/admin-settings) téléchargement d’applications personnalisées est activé dans votre instance Teams, vous pouvez utiliser Teams App Studio pour télécharger directement votre chatbot et commencer à l’utiliser immédiatement.</span><span class="sxs-lookup"><span data-stu-id="1b24c-129">If [uploading custom apps is enabled](/microsoftteams/admin-settings) in your Teams instance, you can use Teams App Studio to directly upload your chatbot and start using it immediately.</span></span> <span data-ttu-id="1b24c-130">Pour partager votre chatbot, vous pouvez demander à votre administrateur de rendre votre bot disponible dans le catalogue d’applications client ou vous pouvez envoyer votre package d’application à d’autres utilisateurs et leur demander de le télécharger indépendamment.</span><span class="sxs-lookup"><span data-stu-id="1b24c-130">To share your chatbot, you can request your admin to make your bot available in the tenant app catalog or you can send your app package to others and ask them to upload it independently.</span></span>

1. <span data-ttu-id="1b24c-131">**Installer App Studio dans Teams**</span><span class="sxs-lookup"><span data-stu-id="1b24c-131">**Install App Studio in Teams**</span></span>  
<span data-ttu-id="1b24c-132">App Studio est une application Teams application.</span><span class="sxs-lookup"><span data-stu-id="1b24c-132">App Studio is a Teams app.</span></span> <span data-ttu-id="1b24c-133">Installez App Studio à partir du magasin Teams qui simplifie le processus de création et d’inscription du bot dans Teams :</span><span class="sxs-lookup"><span data-stu-id="1b24c-133">Install App Studio from the Teams store that simplifies the process of bot creation and registration in Teams:</span></span> 

   1. <span data-ttu-id="1b24c-134">Sélectionnez l’icône du Magasin d’applications Teams instance, puis recherchez **App Studio.**</span><span class="sxs-lookup"><span data-stu-id="1b24c-134">Select the app store icon from Teams instance, and search for **App Studio**.</span></span>

      &emsp;&emsp; <img  width="450px" alt="Finding App Studio in the Store" src="../../assets/images/get-started/app-studio-store.png"/>   

   1. <span data-ttu-id="1b24c-135">Sélectionnez **la vignette App Studio** et **sélectionnez Installer** dans la boîte de dialogue qui s’affiche.</span><span class="sxs-lookup"><span data-stu-id="1b24c-135">Select the **App Studio** tile and select **Install** in the pop-up dialog box.</span></span>

      &emsp;&emsp; <img  width="450px" alt="Installing App Studio" src="../../assets/images/get-started/app-studio-install.png"/>

1. <span data-ttu-id="1b24c-136">**Créer le manifeste Teams’application dans App Studio**</span><span class="sxs-lookup"><span data-stu-id="1b24c-136">**Create the Teams app manifest in App Studio**</span></span>  
<span data-ttu-id="1b24c-137">Les bots dans Teams sont définis par un fichier JSON manifeste d’application qui fournit les informations de base sur votre bot et ses fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="1b24c-137">Bots in Teams are defined by an app manifest JSON file that provides the basic information about your bot and its capabilities.</span></span> <span data-ttu-id="1b24c-138">Dans **App Studio,** sélectionnez **l’éditeur de** manifeste, puis **sélectionnez Créer une application.**</span><span class="sxs-lookup"><span data-stu-id="1b24c-138">In **App Studio**, select **Manifest editor**, and select **Create a new app**.</span></span>

    ![créer une application](../../assets/images/get-started/create-new-app.png)

1. <span data-ttu-id="1b24c-140">**Ajouter les détails de votre bot**</span><span class="sxs-lookup"><span data-stu-id="1b24c-140">**Add your bot details**</span></span>  
<span data-ttu-id="1b24c-141">Remplissez tous les champs requis.</span><span class="sxs-lookup"><span data-stu-id="1b24c-141">Complete all the required fields.</span></span> <span data-ttu-id="1b24c-142">Pour obtenir une description complète de chaque champ, voir [la définition du schéma de manifeste.](../../resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="1b24c-142">For a full description of each field see [manifest schema definition](../../resources/schema/manifest-schema.md).</span></span>

    ![ajouter des détails sur l’application](../../assets/images/get-started/add-app-details.png)

1. <span data-ttu-id="1b24c-144">**Configurer votre bot** Pour configurer le bot, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="1b24c-144">**Set up your bot** To set-up the bot, perform the following steps:</span></span> 
     1. <span data-ttu-id="1b24c-145">Ouvrez **l’onglet Bots.**</span><span class="sxs-lookup"><span data-stu-id="1b24c-145">Open the **Bots** tab.</span></span> 
     1. <span data-ttu-id="1b24c-146">Sélectionnez   >  **Installer le bot existant** et entrez le nom de votre bot.</span><span class="sxs-lookup"><span data-stu-id="1b24c-146">Select **Setup** > **Existing bot** and enter the name of your bot.</span></span>

   ![Mise en place d’un bot](../../assets/images/get-started/bot-set-up.png) 

   <span data-ttu-id="1b24c-148">L’image suivante décrit comment configurer un bot existant :</span><span class="sxs-lookup"><span data-stu-id="1b24c-148">The following image depicts how to set-up an existing bot:</span></span>      

   ![mise en place d’un bot existant](../../assets/images/get-started/existing-bot-set-up.png)
       
1. <span data-ttu-id="1b24c-150">**Ajouter votre ID d’application**</span><span class="sxs-lookup"><span data-stu-id="1b24c-150">**Add your App ID**</span></span>  
<span data-ttu-id="1b24c-151">Pour ajouter votre ID d’application, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="1b24c-151">To add your App ID, perform the following steps:</span></span>  
    1. <span data-ttu-id="1b24c-152">Sélectionnez **Connecter vers un autre ID de bot** et collez l’ID **d’application** que vous avez copié précédemment.</span><span class="sxs-lookup"><span data-stu-id="1b24c-152">Select **Connect to a different bot id** and paste the **App Id** you copied earlier.</span></span> 
    1. <span data-ttu-id="1b24c-153">Sélectionnez   >  **l’étendue d’enregistrer**  >  **personnel**.</span><span class="sxs-lookup"><span data-stu-id="1b24c-153">Select **Scope** > **Personal** > **Save**.</span></span>

    ![ajouter un ID d’application](../../assets/images/get-started/add-app-id.png)

1. <span data-ttu-id="1b24c-155">**Ajouter des domaines valides pour votre bot**</span><span class="sxs-lookup"><span data-stu-id="1b24c-155">**Add valid domains for your bot**</span></span>  
<span data-ttu-id="1b24c-156">Cette étape est requise uniquement si votre bot nécessite que l’utilisateur se connecte.</span><span class="sxs-lookup"><span data-stu-id="1b24c-156">This step is only required if your bot requires the user to sign in.</span></span> <span data-ttu-id="1b24c-157">Sélectionnez **Domaines et autorisations et,** dans le **champ Domaines valides,** fournissez l’entrée suivante :</span><span class="sxs-lookup"><span data-stu-id="1b24c-157">Select **Domains and permissions** and in the **Valid Domains** field, provide the following input:</span></span>

    ```bash
       token.botframework.com
    ```

1. <span data-ttu-id="1b24c-158">**Tester et distribuer votre bot**</span><span class="sxs-lookup"><span data-stu-id="1b24c-158">**Test and distribute your bot**</span></span>  
<span data-ttu-id="1b24c-159">Ouvrez **Test et distribuez** l’onglet, puis sélectionnez **Installer** pour ajouter votre bot directement à Teams instance.</span><span class="sxs-lookup"><span data-stu-id="1b24c-159">Open **Test and distribute** tab and select **Install** to add your bot directly to your Teams instance.</span></span> <span data-ttu-id="1b24c-160">Vous pouvez également télécharger le package d’application terminé pour le partager avec des utilisateurs Teams ou le fournir à votre administrateur pour que votre bot soit disponible dans le catalogue d’applications client.</span><span class="sxs-lookup"><span data-stu-id="1b24c-160">Alternately, you can download the completed app package to share with Teams users or provide it to your admin to make your bot available in the tenant app catalog.</span></span>

1. <span data-ttu-id="1b24c-161">**Démarrer une conversation** </span><span class="sxs-lookup"><span data-stu-id="1b24c-161">**Start a chat** </span></span>  
<span data-ttu-id="1b24c-162">Le processus de mise en place de l’ajout Power Virtual Agents bot de conversation à Teams est terminé.</span><span class="sxs-lookup"><span data-stu-id="1b24c-162">The set-up process for adding your Power Virtual Agents chat bot to Teams is complete.</span></span> <span data-ttu-id="1b24c-163">Vous pouvez maintenant démarrer une conversation avec votre bot dans une conversation personnelle.</span><span class="sxs-lookup"><span data-stu-id="1b24c-163">You can now start a conversation with your bot in a personal chat.</span></span>

## <a name="see-also"></a><span data-ttu-id="1b24c-164">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="1b24c-164">See also</span></span>

* [<span data-ttu-id="1b24c-165">Power Virtual Agents</span><span class="sxs-lookup"><span data-stu-id="1b24c-165">Power Virtual Agents</span></span>](/power-virtual-agents/fundamentals-what-is-power-virtual-agents)  
* <span data-ttu-id="1b24c-166">[Créez un chatbot pour Teams avec Microsoft Power Virtual Agents](../bot-features.md#bots-and-the-microsoft-power-virtual-agents).</span><span class="sxs-lookup"><span data-stu-id="1b24c-166">[Create a chatbot for Teams with Microsoft Power Virtual Agents](../bot-features.md#bots-and-the-microsoft-power-virtual-agents).</span></span>  
* [<span data-ttu-id="1b24c-167">Power Virtual Agents portail</span><span class="sxs-lookup"><span data-stu-id="1b24c-167">Power Virtual Agents portal</span></span>](https://powervirtualagents.microsoft.com)
* [<span data-ttu-id="1b24c-168">Publier votre bot Power Virtual Agents de publication</span><span class="sxs-lookup"><span data-stu-id="1b24c-168">Publish your Power Virtual Agents bot</span></span>](/power-virtual-agents/publication-fundamentals-publish-channels)
* <span data-ttu-id="1b24c-169">[Sécurité et conformité dans Microsoft Teams](/MicrosoftTeams/security-compliance-overview).</span><span class="sxs-lookup"><span data-stu-id="1b24c-169">[Security and compliance in Microsoft Teams](/MicrosoftTeams/security-compliance-overview).</span></span>

## <a name="next-step"></a><span data-ttu-id="1b24c-170">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="1b24c-170">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1b24c-171">Créer un assistant virtuel</span><span class="sxs-lookup"><span data-stu-id="1b24c-171">Create virtual assistant</span></span>](~/samples/virtual-assistant.md)

