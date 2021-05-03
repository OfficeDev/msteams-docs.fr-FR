---
title: Inscription au canal du bot Azure
description: décrit les canaux de bot Azure pour l'inscription
localization_priority: Normal
ms.topic: overview
ms.author: surbhigupta12
ms.openlocfilehash: 3cbbd204daf98f1c3528dcb6efcfde299a402912
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020948"
---
1. <span data-ttu-id="a19e6-103">Dans le [portail Azure,](https://ms.portal.azure.com/#home)sous services Azure, **sélectionnez Créer une ressource.**</span><span class="sxs-lookup"><span data-stu-id="a19e6-103">In the [Azure portal](https://ms.portal.azure.com/#home), under Azure services, select **Create a resource**.</span></span>
1. <span data-ttu-id="a19e6-104">Dans la zone de recherche, entrez « bot ».</span><span class="sxs-lookup"><span data-stu-id="a19e6-104">In the search box enter "bot".</span></span> <span data-ttu-id="a19e6-105">And in the drop-down list, select **Bot Channels Registration**.</span><span class="sxs-lookup"><span data-stu-id="a19e6-105">And in the drop-down list, select **Bot Channels Registration**.</span></span>
1. <span data-ttu-id="a19e6-106">Sélectionnez **le bouton** Créer.</span><span class="sxs-lookup"><span data-stu-id="a19e6-106">Select the **Create** button.</span></span>
1. <span data-ttu-id="a19e6-107">Dans le blade **d'inscription du** canal bot, fournissez les informations demandées sur votre bot.</span><span class="sxs-lookup"><span data-stu-id="a19e6-107">In the **Bot Channel Registration** blade, provide the requested information about your bot.</span></span>
1. <span data-ttu-id="a19e6-108">Laissez la **zone de point de terminaison** de messagerie vide pour le moment, vous entrez l'URL requise après le déploiement du bot.</span><span class="sxs-lookup"><span data-stu-id="a19e6-108">Leave the **Messaging endpoint** box empty for now, you will enter the required URL after deploying the bot.</span></span> <span data-ttu-id="a19e6-109">L'image suivante montre un exemple des paramètres d'inscription :</span><span class="sxs-lookup"><span data-stu-id="a19e6-109">The following picture shows an example of the registration settings:</span></span>

    ![inscription des canaux d'application bot](../../assets/images/authentication/auth-bot-channels-registration.png)

1. <span data-ttu-id="a19e6-111">Cliquez **sur L'ID et le mot de passe de l'application Microsoft,** **puis créez-en un.**</span><span class="sxs-lookup"><span data-stu-id="a19e6-111">Click **Microsoft App ID and password** and then **Create New**.</span></span>

    <span data-ttu-id="a19e6-112">![Créer un ID d'application ](../../assets/images/authentication/CreateMicrosoftAppID.png) ![ Microsoft : créer un ID d'application Microsoft](../../assets/images/authentication/CreateNewMicrosoftAppID.png)</span><span class="sxs-lookup"><span data-stu-id="a19e6-112">![Create Microsoft App ID](../../assets/images/authentication/CreateMicrosoftAppID.png) ![Create New Microsoft App ID](../../assets/images/authentication/CreateNewMicrosoftAppID.png)</span></span>    

1. <span data-ttu-id="a19e6-113">Cliquez **sur Créer un ID d'application dans le lien Portail d'inscription des** applications.</span><span class="sxs-lookup"><span data-stu-id="a19e6-113">Click **Create App ID in the App Registration Portal** link.</span></span>

   ![Inscriptions d'applications](../../assets/images/authentication/AppRegistration.png)
   
1. <span data-ttu-id="a19e6-115">Dans la fenêtre **d'inscription de l'application** affichée, cliquez sur l'onglet Nouvelle **inscription** dans le coin supérieur gauche.</span><span class="sxs-lookup"><span data-stu-id="a19e6-115">In the displayed **App registration** window, click the **New registration** tab in the upper left.</span></span>
1. <span data-ttu-id="a19e6-116">Entrez le nom de l'application bot que vous inscrivez, nous avons *utilisé BotTeamsAuth* (vous devez sélectionner votre propre nom unique).</span><span class="sxs-lookup"><span data-stu-id="a19e6-116">Enter the name of the bot application you are registering, we used *BotTeamsAuth* (you need to select your own unique name).</span></span>
1. <span data-ttu-id="a19e6-117">Pour les **types** de comptes pris en charge, sélectionnez Comptes dans n'importe quel répertoire d'organisation (n'importe quel annuaire *Azure AD - Multi-client)* et comptes Microsoft personnels (par exemple, Skype, Xbox).</span><span class="sxs-lookup"><span data-stu-id="a19e6-117">For the **Supported account types** select *Accounts in any organizational directory (Any Azure AD directory - Multitenant) and personal Microsoft accounts (e.g. Skype, Xbox)*.</span></span>
1. <span data-ttu-id="a19e6-118">Cliquez sur le **bouton** Enregistrer.</span><span class="sxs-lookup"><span data-stu-id="a19e6-118">Click the **Register** button.</span></span> <span data-ttu-id="a19e6-119">Une fois terminé, Azure affiche la page *Vue d'ensemble* de l'application.</span><span class="sxs-lookup"><span data-stu-id="a19e6-119">Once completed, Azure displays the *Overview* page for the application.</span></span>
1. <span data-ttu-id="a19e6-120">Copiez et enregistrez dans un fichier la valeur de l'ID de **l'application (client).**</span><span class="sxs-lookup"><span data-stu-id="a19e6-120">Copy and save to a file the **Application (client) ID** value.</span></span>
1. <span data-ttu-id="a19e6-121">Dans le panneau gauche, cliquez sur **Certificat et secrets.**</span><span class="sxs-lookup"><span data-stu-id="a19e6-121">In the left panel, click **Certificate and secrets**.</span></span>
    1. <span data-ttu-id="a19e6-122">Sous *Les secrets du client,* cliquez sur Nouvelle secret **client.**</span><span class="sxs-lookup"><span data-stu-id="a19e6-122">Under *Client secrets*, click **New client secret**.</span></span>
    1. <span data-ttu-id="a19e6-123">Ajoutez une description pour identifier ce secret auprès d'autres personnes que vous devrez peut-être créer pour cette application.</span><span class="sxs-lookup"><span data-stu-id="a19e6-123">Add a description to identify this secret from others you might need to create for this app.</span></span>
    1. <span data-ttu-id="a19e6-124">La *sélection expire.*</span><span class="sxs-lookup"><span data-stu-id="a19e6-124">Set *Expires* to your selection.</span></span>
    1. <span data-ttu-id="a19e6-125">Cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="a19e6-125">Click **Add**.</span></span>
    1. <span data-ttu-id="a19e6-126">Copiez la secret client et enregistrez-la dans un fichier.</span><span class="sxs-lookup"><span data-stu-id="a19e6-126">Copy the client secret and save it to a file.</span></span>
1. <span data-ttu-id="a19e6-127">Revenir à la fenêtre Inscription  du canal bot et copier l'ID  d'application et la secret *client* dans les zones **ID** d'application Microsoft et mot de passe, respectivement. </span><span class="sxs-lookup"><span data-stu-id="a19e6-127">Go back to the **Bot Channel Registration** window and copy the *App ID* and the *Client secret* in the **Microsoft App ID** and **Password** boxes, respectively.</span></span>
1. <span data-ttu-id="a19e6-128">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="a19e6-128">Click **OK**.</span></span>
1. <span data-ttu-id="a19e6-129">Enfin, cliquez sur **Créer.**</span><span class="sxs-lookup"><span data-stu-id="a19e6-129">Finally, click **Create**.</span></span>

<span data-ttu-id="a19e6-130">Une fois qu'Azure a créé la ressource d'inscription, elle sera incluse dans la liste des groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="a19e6-130">After Azure has created the registration resource it will be included in the resource group list.</span></span>  

![groupe d'inscription des canaux d'application bot](~/assets/images/authentication/auth-bot-channels-registration-group.PNG)

<span data-ttu-id="a19e6-132">Une fois l'inscription de vos canaux de bot créée, vous devez activer le canal Teams bot.</span><span class="sxs-lookup"><span data-stu-id="a19e6-132">Once your bot channels registration is created, you'll need to enable the Teams channel.</span></span>

1. <span data-ttu-id="a19e6-133">Dans le [portail Azure, sous](https://ms.portal.azure.com/#home)services Azure, sélectionnez l'inscription du canal bot **que** vous avez créée.</span><span class="sxs-lookup"><span data-stu-id="a19e6-133">In the [Azure portal](https://ms.portal.azure.com/#home), under Azure services, select the **Bot Channel Registration** you just created.</span></span>
1. <span data-ttu-id="a19e6-134">Dans le panneau gauche, cliquez sur **Canaux**.</span><span class="sxs-lookup"><span data-stu-id="a19e6-134">In the left panel, click **Channels**.</span></span>
1. <span data-ttu-id="a19e6-135">Cliquez sur l Microsoft Teams icône, puis sélectionnez **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="a19e6-135">Click the Microsoft Teams icon, then choose **Save**.</span></span>
