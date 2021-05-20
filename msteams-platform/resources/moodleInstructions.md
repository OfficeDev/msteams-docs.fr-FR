---
title: Installer Moodle LMS
description: Comment installer et configurer l’application d’intégration Moodle pour Microsoft Teams
keywords: Teams Plugins d’intégration d’applications Moodle
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
author: laujan
ms.openlocfilehash: d7fddad80ca08fd4ca8dee352cdcbc46e8e97dcd
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566718"
---
# <a name="install-moodle-lms"></a><span data-ttu-id="82fa4-104">Installer Moodle LMS</span><span class="sxs-lookup"><span data-stu-id="82fa4-104">Install Moodle LMS</span></span>

<span data-ttu-id="82fa4-105">Dans cet article, vous apprendrez à installer le Moodle LMS.</span><span class="sxs-lookup"><span data-stu-id="82fa4-105">In this article you'll learn how to install the Moodle LMS.</span></span>

> [!NOTE]
> <span data-ttu-id="82fa4-106">Pour aider les administrateurs informatique à configurer facilement Moodle et l’intégration Teams, les Microsoft 365 Moodle Plugins open source sont mis à jour pour les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="82fa4-106">To help IT admins to easily set-up Moodle and Teams integration, open-source Microsoft 365 Moodle Plugins is updated for the following:</span></span>
>
> * <span data-ttu-id="82fa4-107">Enregistrement automatique de votre serveur Moodle avec [Azure Active Directory (Azure AD)](https://azure.microsoft.com/services/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="82fa4-107">Auto-registration of your Moodle server with [Azure Active Directory (Azure AD)](https://azure.microsoft.com/services/active-directory/).</span></span>
>
> * <span data-ttu-id="82fa4-108">Déploiement en un clic de votre bot Moodle Assistant sur Azure.</span><span class="sxs-lookup"><span data-stu-id="82fa4-108">One-click deployment of your Moodle Assistant bot to Azure.</span></span>
>
> * <span data-ttu-id="82fa4-109">Auto-provision des équipes et autosynchronisation des inscriptions d’équipe pour tous ou sélectionner les cours Moodle.</span><span class="sxs-lookup"><span data-stu-id="82fa4-109">Auto-provisioning of teams and auto-synchronization of team enrollments for all or select Moodle courses.</span></span>
>
> * <span data-ttu-id="82fa4-110">Auto-installation de l’onglet Moodle et du bot assistant Moodle dans chaque équipe synchronisée.</span><span class="sxs-lookup"><span data-stu-id="82fa4-110">Auto-installation of the Moodle tab and the Moodle assistant bot into each synchronized team.</span></span>
>
> <span data-ttu-id="82fa4-111">Pour en savoir plus sur les fonctionnalités de cette intégration, [consultez Microsoft Teams et Moodle](https://education.microsoft.com/resource/3dffb3a8).</span><span class="sxs-lookup"><span data-stu-id="82fa4-111">To learn more about the functionality this integration provides, see [Microsoft Teams and Moodle](https://education.microsoft.com/resource/3dffb3a8).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="82fa4-112">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="82fa4-112">Prerequisites</span></span>

<span data-ttu-id="82fa4-113">Voici les conditions préalables à l’installation de Moodle :</span><span class="sxs-lookup"><span data-stu-id="82fa4-113">Following are the prerequisites to install Moodle:</span></span>

* <span data-ttu-id="82fa4-114">Informations d’identification de l’administrateur Moodle.</span><span class="sxs-lookup"><span data-stu-id="82fa4-114">Moodle administrator credentials.</span></span>

* <span data-ttu-id="82fa4-115">Informations d’identification de l’administrateur AD Azure.</span><span class="sxs-lookup"><span data-stu-id="82fa4-115">Azure AD administrator credentials.</span></span>

* <span data-ttu-id="82fa4-116">Un abonnement Azure où vous pouvez créer de nouvelles ressources.</span><span class="sxs-lookup"><span data-stu-id="82fa4-116">An Azure subscription where you can create new resources.</span></span>

## <a name="1-install-the-microsoft-365-moodle-plugins"></a><span data-ttu-id="82fa4-117">1. Installez les plugins Microsoft 365 Moodle</span><span class="sxs-lookup"><span data-stu-id="82fa4-117">1. Install the Microsoft 365 Moodle Plugins</span></span>

<span data-ttu-id="82fa4-118">L’intégration moodle Microsoft Teams est alimentée par l’open source [Microsoft 365 ensemble de plugins Moodle.](https://github.com/Microsoft/o365-moodle)</span><span class="sxs-lookup"><span data-stu-id="82fa4-118">Moodle integration in Microsoft Teams is powered by the open source [Microsoft 365 Moodle plugins set](https://github.com/Microsoft/o365-moodle).</span></span>

### <a name="requisite-applications-and-plugins"></a><span data-ttu-id="82fa4-119">Applications et plugins requis</span><span class="sxs-lookup"><span data-stu-id="82fa4-119">Requisite applications and plugins</span></span>

<span data-ttu-id="82fa4-120">Assurez-vous d’installer et de télécharger ce qui suit avant de procéder à l Microsoft 365 installer des plugins Moodle :</span><span class="sxs-lookup"><span data-stu-id="82fa4-120">Ensure to install and download the following before proceeding with the Microsoft 365 Moodle plugins installation:</span></span>

1. <span data-ttu-id="82fa4-121">Assurez-vous [d’installer une version stable actuelle de Moodle](https://download.moodle.org/releases/latest/).</span><span class="sxs-lookup"><span data-stu-id="82fa4-121">Ensure to install a [current stable version of Moodle](https://download.moodle.org/releases/latest/).</span></span>

1. <span data-ttu-id="82fa4-122">Téléchargez et enregistrez les plugins Moodle [OpenID Connecter](https://moodle.org/plugins/auth_oidc) et [Microsoft 365'intégration](https://moodle.org/plugins/local_o365) de votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="82fa4-122">Download and save the Moodle [OpenID Connect](https://moodle.org/plugins/auth_oidc) and the [Microsoft 365 Integration](https://moodle.org/plugins/local_o365) plugins to your local computer.</span></span>

    > [!NOTE]
    > <span data-ttu-id="82fa4-123">L’installation des plugins openid Connecter et Microsoft 365'intégration sont nécessaires pour l’intégration Teams’intégration.</span><span class="sxs-lookup"><span data-stu-id="82fa4-123">Installing the OpenID Connect and Microsoft 365 Integration plugins are required for the Teams integration.</span></span>
    >
    > <span data-ttu-id="82fa4-124">En outre, les [plugins Microsoft 365 Teams thème](https://moodle.org/plugins/theme_boost_o365teams) sont fortement recommandés.</span><span class="sxs-lookup"><span data-stu-id="82fa4-124">In addition, the [Microsoft 365 Teams Theme](https://moodle.org/plugins/theme_boost_o365teams) plugins is highly recommended.</span></span>

### <a name="microsoft-365-moodle-plugins"></a><span data-ttu-id="82fa4-125">Microsoft 365 Plugins Moodle</span><span class="sxs-lookup"><span data-stu-id="82fa4-125">Microsoft 365 Moodle plugins</span></span>

1. <span data-ttu-id="82fa4-126">Connectez-vous à votre serveur Moodle en tant qu’administrateur et **sélectionnez l’administration** du site [à partir du bloc Paramètres situé](https://docs.moodle.org/22/en/Settings_block) dans le panneau de navigation gauche.</span><span class="sxs-lookup"><span data-stu-id="82fa4-126">Sign in to your Moodle server as an administrator and select **Site administration** from the [Settings block](https://docs.moodle.org/22/en/Settings_block) located in the left navigation panel.</span></span>

1. <span data-ttu-id="82fa4-127">Sélectionnez **l’onglet Plugins,** puis sélectionnez **Installer des plugins.**</span><span class="sxs-lookup"><span data-stu-id="82fa4-127">Select the **Plugins** tab, and then select **Install plugins**.</span></span>

1. <span data-ttu-id="82fa4-128">À partir **des plugins Installer de la** section fichier ZIP, **sélectionnez Choisir un fichier**.</span><span class="sxs-lookup"><span data-stu-id="82fa4-128">From the **Install plugins from ZIP file** section, select **Choose a file**.</span></span>

1. <span data-ttu-id="82fa4-129">Sélectionnez **Télécharger une** option de fichier à partir du panneau de navigation gauche, recherchez le fichier que vous avez téléchargé et **sélectionnez Télécharger ce fichier**.</span><span class="sxs-lookup"><span data-stu-id="82fa4-129">Select **Upload a file** option from the left navigation panel, browse for the file that you downloaded, and select **Upload this file**.</span></span>

1. <span data-ttu-id="82fa4-130">Sélectionnez **l’administration** du site à partir du panneau de navigation gauche pour revenir à votre tableau de bord admin.</span><span class="sxs-lookup"><span data-stu-id="82fa4-130">Select **Site administration** from the left navigation panel to return to your admin dashboard.</span></span> <span data-ttu-id="82fa4-131">Faites défiler vers le **bas pour les plugins** locaux et sélectionnez **le lien Microsoft 365'intégration.**</span><span class="sxs-lookup"><span data-stu-id="82fa4-131">Scroll down to the **Local plugins** and select the **Microsoft 365 Integration** link.</span></span>

    > [!IMPORTANT]
    >
    > * <span data-ttu-id="82fa4-132">Gardez votre page Microsoft 365 configuration Moodle Plugins ouverte dans un onglet de navigateur distinct, car vous devez revenir à cet ensemble de pages tout au long du processus.</span><span class="sxs-lookup"><span data-stu-id="82fa4-132">Keep your Microsoft 365 Moodle Plugins configuration page open in a separate browser tab as you need to return to this set of pages throughout the process.</span></span>  
    >
    > * <span data-ttu-id="82fa4-133">Si vous n’avez pas de site Moodle existant, rendez-vous sur le repo [Moodle on Azure,](https://github.com/azure/moodle) et déployez rapidement une instance Moodle et personnalisez-la à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="82fa4-133">If you do not have an existing Moodle site, go to the [Moodle on Azure](https://github.com/azure/moodle) repo, and quickly deploy a Moodle instance and customize it to your needs.</span></span>

## <a name="2-configure-the-connection-between-the-microsoft-365-plugins-and-azure-active-directory-azure-ad"></a><span data-ttu-id="82fa4-134">2. Configurer la connexion entre les plugins Microsoft 365 et Azure Active Directory (Azure AD)</span><span class="sxs-lookup"><span data-stu-id="82fa4-134">2. Configure the connection between the Microsoft 365 plugins and Azure Active Directory (Azure AD)</span></span>

<span data-ttu-id="82fa4-135">Vous devez configurer la connexion entre les plugins Microsoft 365 et Azure AD.</span><span class="sxs-lookup"><span data-stu-id="82fa4-135">You must configure the connection between the Microsoft 365 plugins and Azure AD.</span></span>

### <a name="requisites"></a><span data-ttu-id="82fa4-136">Accessoires</span><span class="sxs-lookup"><span data-stu-id="82fa4-136">Requisites</span></span>

<span data-ttu-id="82fa4-137">Inscrivez Moodle comme application dans votre annonce Azure, en utilisant le script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="82fa4-137">Register Moodle as an application in your Azure AD, using the PowerShell script.</span></span> <span data-ttu-id="82fa4-138">Le script Powershell dispositions suivantes:</span><span class="sxs-lookup"><span data-stu-id="82fa4-138">The Powershell script provisions the following:</span></span>

* <span data-ttu-id="82fa4-139">Une nouvelle application Azure AD pour votre Microsoft 365, qui est utilisée par les Microsoft 365 Moodle Plugins.</span><span class="sxs-lookup"><span data-stu-id="82fa4-139">A new Azure AD application for your Microsoft 365 tenant, which is used by the Microsoft 365 Moodle Plugins.</span></span>
* <span data-ttu-id="82fa4-140">L’application pour votre Microsoft 365, configurer les URL de réponse requises et les autorisations pour l’application provisionnée, et retourne le `AppID` et `Key` .</span><span class="sxs-lookup"><span data-stu-id="82fa4-140">The app for your Microsoft 365 tenant, set up the required reply URLs and permissions for the provisioned app, and returns the `AppID` and `Key`.</span></span>

<span data-ttu-id="82fa4-141">Utilisez la `AppID` `Key` page d’installation Microsoft 365 Moodle Plugins pour configurer votre site serveur Moodle avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="82fa4-141">Use the generated `AppID` and `Key` in your Microsoft 365 Moodle Plugins setup page to configure your Moodle server site with Azure AD.</span></span>

> [!IMPORTANT]
>
> * <span data-ttu-id="82fa4-142">Le script PowerShell n’est pas mis à jour avec les derniers éléments de configuration, par conséquent, vous devez compléter la configuration manuellement en suivant les étapes décrites dans les pages de sortie Moodle [3.8.0.4 et 3.9.1](https://docs.moodle.org/39/en/Office365#3.8.0.4_and_3.9.1_release) [et 3.8.0.5 et 3.9.2.](https://docs.moodle.org/39/en/Office365#3.8.0.5_and_3.9.2_release)</span><span class="sxs-lookup"><span data-stu-id="82fa4-142">The PowerShell script is not updated with the latest configuration items, therefore, you must complete the configuration manually following the steps outlined in the Moodle [3.8.0.4 and 3.9.1](https://docs.moodle.org/39/en/Office365#3.8.0.4_and_3.9.1_release) and [3.8.0.5 and 3.9.2](https://docs.moodle.org/39/en/Office365#3.8.0.5_and_3.9.2_release) release pages.</span></span>
>
> * <span data-ttu-id="82fa4-143">Pour plus d’informations sur l’enregistrement manuel de votre instance Moodle, [consultez l’enregistrement de votre instance Moodle en tant qu’application](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application).</span><span class="sxs-lookup"><span data-stu-id="82fa4-143">For more information on registering your Moodle instance manually, see [Register your Moodle instance as an application](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application).</span></span>

### <a name="the-moodle-tab-for-microsoft-teams-information-flow"></a><span data-ttu-id="82fa4-144">L’onglet Moodle pour le flux Microsoft Teams’information</span><span class="sxs-lookup"><span data-stu-id="82fa4-144">The Moodle tab for Microsoft Teams information flow</span></span>

<img width="530px" src="../assets/images/MoodleTabInformationFlow.png" alt="Moodle tab for Microsoft Teams information flow" />

1. <span data-ttu-id="82fa4-145">À partir de la page Microsoft 365'intégration, sélectionnez **l’onglet Configuration.**</span><span class="sxs-lookup"><span data-stu-id="82fa4-145">From the Microsoft 365 Integration plugins page, select the **Setup** tab.</span></span>

1. <span data-ttu-id="82fa4-146">Sélectionnez **le bouton Télécharger powershell** script et enregistrez-le comme un dossier ZIP sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="82fa4-146">Select the **Download PowerShell Script** button and save it as a ZIP folder to your local computer.</span></span>

1. <span data-ttu-id="82fa4-147">Préparez le script PowerShell à partir du fichier ZIP comme suit :</span><span class="sxs-lookup"><span data-stu-id="82fa4-147">Prepare the PowerShell script from the ZIP file as follows:</span></span> 

    1. <span data-ttu-id="82fa4-148">Téléchargez et extrayz `Moodle-AzureAD-Powershell.zip` le fichier.</span><span class="sxs-lookup"><span data-stu-id="82fa4-148">Download and extract the `Moodle-AzureAD-Powershell.zip` file.</span></span>
    1. <span data-ttu-id="82fa4-149">Ouvrez le dossier extrait.</span><span class="sxs-lookup"><span data-stu-id="82fa4-149">Open the extracted folder.</span></span>
    1. <span data-ttu-id="82fa4-150">Cliquez à droite sur le `Moodle-AzureAD-Script.ps1` fichier et sélectionnez **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="82fa4-150">Right-click on the `Moodle-AzureAD-Script.ps1` file and select **Properties**.</span></span>
    1. <span data-ttu-id="82fa4-151">Sous **l’onglet** Général de la fenêtre Propriétés, sélectionnez la `Unblock` case à cocher à côté de **l’attribut** Sécurité situé au bas de la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="82fa4-151">Under the **General** tab of the Properties window, select the `Unblock` checkbox next to the **Security** attribute located at the bottom of the window.</span></span>
    1. <span data-ttu-id="82fa4-152">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="82fa4-152">Select **OK**.</span></span>
    1. <span data-ttu-id="82fa4-153">Copiez le chemin d’annuaire vers le dossier extrait.</span><span class="sxs-lookup"><span data-stu-id="82fa4-153">Copy the directory path to the extracted folder.</span></span>

1. <span data-ttu-id="82fa4-154">Exécutez PowerShell en tant qu’administrateur :</span><span class="sxs-lookup"><span data-stu-id="82fa4-154">Run PowerShell as an administrator:</span></span>

    1. <span data-ttu-id="82fa4-155">Sélectionnez Démarrer.</span><span class="sxs-lookup"><span data-stu-id="82fa4-155">Select Start.</span></span>
    1. <span data-ttu-id="82fa4-156">Type PowerShell.</span><span class="sxs-lookup"><span data-stu-id="82fa4-156">Type PowerShell.</span></span>
    1. <span data-ttu-id="82fa4-157">Clic droit sur **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="82fa4-157">Right-click on **Windows PowerShell**.</span></span>
    1. <span data-ttu-id="82fa4-158">Sélectionnez **Exécuter en tant qu’administrateur**.</span><span class="sxs-lookup"><span data-stu-id="82fa4-158">Select **Run as Administrator**.</span></span>

1. <span data-ttu-id="82fa4-159">Naviguez vers le répertoire décompressé en tapant `cd .../.../Moodle-AzureAD-Powershell` `.../...` où est le chemin vers le répertoire.</span><span class="sxs-lookup"><span data-stu-id="82fa4-159">Navigate to the unzipped directory by typing `cd .../.../Moodle-AzureAD-Powershell` where `.../...` is the path to the directory.</span></span>

1. <span data-ttu-id="82fa4-160">Exécutez le script PowerShell :</span><span class="sxs-lookup"><span data-stu-id="82fa4-160">Execute the PowerShell script:</span></span>

    1. <span data-ttu-id="82fa4-161">Entrez `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser` .</span><span class="sxs-lookup"><span data-stu-id="82fa4-161">Enter `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser`.</span></span>
    1. <span data-ttu-id="82fa4-162">Entrez `./Moodle-AzureAD-Script.ps1` .</span><span class="sxs-lookup"><span data-stu-id="82fa4-162">Enter `./Moodle-AzureAD-Script.ps1`.</span></span>
    1. <span data-ttu-id="82fa4-163">Connectez-vous à votre Microsoft 365'administrateur de votre ordinateur dans la fenêtre contextée.</span><span class="sxs-lookup"><span data-stu-id="82fa4-163">Sign in to your Microsoft 365 administrator account in the pop-up window.</span></span>
    1. <span data-ttu-id="82fa4-164">Entrez le nom de l’application AD Azure, par exemple, les plugins Moodle ou Moodle.</span><span class="sxs-lookup"><span data-stu-id="82fa4-164">Enter the name of the Azure AD Application, for example, Moodle or Moodle plugins.</span></span>
    1. <span data-ttu-id="82fa4-165">Entrez l’URL de votre serveur Moodle.</span><span class="sxs-lookup"><span data-stu-id="82fa4-165">Enter the URL for your Moodle server.</span></span>
    1. <span data-ttu-id="82fa4-166">Copiez **l’ID `AppID` d’application ( )** et la clé **`Key` d’application ( )** généré par le script et enregistrez-les.</span><span class="sxs-lookup"><span data-stu-id="82fa4-166">Copy the **Application ID (`AppID`)** and **Application Key(`Key`)** generated by the script and save them.</span></span>

1. <span data-ttu-id="82fa4-167">Ensuite, vous devez ajouter `AppID` le et à la Microsoft 365 `Key` Moodle Plugins.</span><span class="sxs-lookup"><span data-stu-id="82fa4-167">Next you must add the `AppID` and `Key` to the Microsoft 365 Moodle Plugins.</span></span> <span data-ttu-id="82fa4-168">Retour à la page d’administration des plugins, administration du site > plugins > Microsoft 365 intégration.</span><span class="sxs-lookup"><span data-stu-id="82fa4-168">Return to the plugins administration page, Site administration > Plugins > Microsoft 365 Integration.</span></span>

1. <span data-ttu-id="82fa4-169">Sur **l’onglet** Configuration ajouter `AppID` le et vous copié `Key` précédemment, puis sélectionnez **Enregistrer les modifications**.</span><span class="sxs-lookup"><span data-stu-id="82fa4-169">On the **Setup** tab add the `AppID` and `Key` you copied previously, and then select **Save changes**.</span></span> <span data-ttu-id="82fa4-170">Après la mise à jour de la page, vous pouvez voir une nouvelle section **Choisir la méthode de connexion**.</span><span class="sxs-lookup"><span data-stu-id="82fa4-170">After the page refreshes, you can see a new section **Choose connection method**.</span></span>

1. <span data-ttu-id="82fa4-171">Dans la **méthode de connexion Choisir,** sélectionnez la case à cocher **étiquetée Par défaut,** puis sélectionnez **Enregistrer les modifications à** nouveau.</span><span class="sxs-lookup"><span data-stu-id="82fa4-171">In the **Choose connection method**, select the checkbox labeled **Default**, and then select **Save changes** again.</span></span>

1. <span data-ttu-id="82fa4-172">Après la page se rafraîchit, vous pouvez voir une autre nouvelle section **Consentement admin & informations supplémentaires**.</span><span class="sxs-lookup"><span data-stu-id="82fa4-172">After the page refreshes you can see another new section **Admin consent & additional information**.</span></span>
    1. <span data-ttu-id="82fa4-173">Sélectionnez **Fournir le lien consentement** administrateur, entrez vos Microsoft 365 informations d’identification de l’administrateur global, puis **acceptez** d’accorder les autorisations.</span><span class="sxs-lookup"><span data-stu-id="82fa4-173">Select **Provide Admin Consent** link, enter your Microsoft 365 Global Administrator credentials, then **Accept** to grant the permissions.</span></span>
    1. <span data-ttu-id="82fa4-174">À côté du **champ Locataire AD Azure,** sélectionnez le **bouton Détecter.**</span><span class="sxs-lookup"><span data-stu-id="82fa4-174">Next to the **Azure AD Tenant** field, select the **Detect** button.</span></span>
    1. <span data-ttu-id="82fa4-175">À côté de **l OneDrive Entreprise URL,** sélectionnez **le bouton** Détecter.</span><span class="sxs-lookup"><span data-stu-id="82fa4-175">Next to the **OneDrive for Business URL**, select the **Detect** button.</span></span>
    1. <span data-ttu-id="82fa4-176">Une fois que les champs se peuplent, sélectionnez **à nouveau le** bouton Enregistrer les modifications.</span><span class="sxs-lookup"><span data-stu-id="82fa4-176">After the fields populate, select the **Save changes** button again.</span></span>

1. <span data-ttu-id="82fa4-177">Sélectionnez le **bouton Mise** à jour pour vérifier l’installation, puis sélectionnez Enregistrer **les modifications**.</span><span class="sxs-lookup"><span data-stu-id="82fa4-177">Select the **Update** button to verify the installation, and then select **Save changes**.</span></span>

1. <span data-ttu-id="82fa4-178">Synchronisez les utilisateurs entre votre serveur Moodle et Azure AD.</span><span class="sxs-lookup"><span data-stu-id="82fa4-178">Synchronize users between your Moodle server and Azure AD.</span></span> <span data-ttu-id="82fa4-179">Pour commencer :</span><span class="sxs-lookup"><span data-stu-id="82fa4-179">To get started:</span></span>

    > [!NOTE]
    > <span data-ttu-id="82fa4-180">Selon votre environnement, vous pouvez sélectionner différentes options au cours de cette étape.</span><span class="sxs-lookup"><span data-stu-id="82fa4-180">Depending on your environment, you can select different options during this stage.</span></span>

1. <span data-ttu-id="82fa4-181">Synchronisez les utilisateurs entre votre serveur Moodle et Azure AD.</span><span class="sxs-lookup"><span data-stu-id="82fa4-181">Synchronize users between your Moodle server and Azure AD.</span></span> <span data-ttu-id="82fa4-182">Selon votre environnement, vous pouvez sélectionner différentes options au cours de cette étape.</span><span class="sxs-lookup"><span data-stu-id="82fa4-182">Depending on your environment, you can select different options during this stage.</span></span> <span data-ttu-id="82fa4-183">Pour commencer :</span><span class="sxs-lookup"><span data-stu-id="82fa4-183">To get started:</span></span>
    1. <span data-ttu-id="82fa4-184">Passez à **l’onglet Paramètres Sync**.</span><span class="sxs-lookup"><span data-stu-id="82fa4-184">Switch to the **Sync Settings tab**.</span></span>

    1. <span data-ttu-id="82fa4-185">Dans la section **Synchron utilisateurs avec Azure AD,** sélectionnez les casettes qui s’appliquent à votre environnement.</span><span class="sxs-lookup"><span data-stu-id="82fa4-185">In the **Sync users with Azure AD** section, select the checkboxes that apply to your environment.</span></span> <span data-ttu-id="82fa4-186">Vous devez sélectionner les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="82fa4-186">You must select the following:</span></span>  

        <span data-ttu-id="82fa4-187">✔ créer des comptes dans Moodle pour les utilisateurs d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="82fa4-187">✔ Create accounts in Moodle for users in Azure AD.</span></span>

        <span data-ttu-id="82fa4-188">✔ mettre à jour tous les comptes de Moodle pour les utilisateurs d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="82fa4-188">✔ Update all accounts in Moodle for users in Azure AD.</span></span>

    1. <span data-ttu-id="82fa4-189">Dans la section **Restriction de création** utilisateur, vous pouvez configurer un filtre pour limiter les utilisateurs azure ad synchronisés avec Moodle.</span><span class="sxs-lookup"><span data-stu-id="82fa4-189">In the **User Creation Restriction** section, you can setup a filter to limit the Azure AD users that is synced to Moodle.</span></span>
    1. <span data-ttu-id="82fa4-190">La section **De mappage de** champ utilisateur vous permet de personnaliser l’annonce Azure à la cartographie de champ de profil utilisateur Moodle.</span><span class="sxs-lookup"><span data-stu-id="82fa4-190">The **User Field Mapping** section allows you to customize the Azure AD to Moodle User Profile field mapping.</span></span>
    1. <span data-ttu-id="82fa4-191">Dans la **section Teams Sync,** vous pouvez sélectionner pour créer automatiquement des groupes, tels que des équipes pour certains ou pour tous vos cours Moodle existants.</span><span class="sxs-lookup"><span data-stu-id="82fa4-191">In the **Teams Sync** section, you can select to automatically create Groups, such as teams for some, or all, of your existing Moodle courses.</span></span>

13. <span data-ttu-id="82fa4-192">Pour valider [les travaux cron](https://docs.moodle.org/310/en/Cron) et les exécuter manuellement pour la première série, sélectionnez le lien **de page de gestion des tâches** planifiées dans la section Sync utilisateurs avec **Azure AD.**</span><span class="sxs-lookup"><span data-stu-id="82fa4-192">To validate [cron](https://docs.moodle.org/310/en/Cron) jobs and run them manually for the first run, select the **Scheduled tasks management page** link in the **Sync users with Azure AD** section.</span></span> <span data-ttu-id="82fa4-193">Cela vous emmène à la page **Tâches planifiées.**</span><span class="sxs-lookup"><span data-stu-id="82fa4-193">This takes you to the **Scheduled Tasks** page.</span></span>

    1. <span data-ttu-id="82fa4-194">Faites défiler vers le bas et **trouvez les utilisateurs Sync avec azure AD** travail et **sélectionnez Exécuter maintenant**.</span><span class="sxs-lookup"><span data-stu-id="82fa4-194">Scroll down and find the **Sync users with Azure AD** job and select **Run now**.</span></span>
    1. <span data-ttu-id="82fa4-195">Si vous sélectionnez pour créer des groupes en fonction des cours existants, vous pouvez également exécuter **les groupes d’utilisateurs Create Microsoft 365** travail.</span><span class="sxs-lookup"><span data-stu-id="82fa4-195">If you select to create Groups based on existing courses, you can also run the **Create user groups in Microsoft 365** job.</span></span>

    > [!NOTE]
    >
    > <span data-ttu-id="82fa4-196">Le Moodle [Cron fonctionne](https://docs.moodle.org/310/en/Cron) selon le calendrier des tâches.</span><span class="sxs-lookup"><span data-stu-id="82fa4-196">The Moodle [Cron](https://docs.moodle.org/310/en/Cron) runs according to the task schedule.</span></span> <span data-ttu-id="82fa4-197">L’horaire par défaut est une fois par jour.</span><span class="sxs-lookup"><span data-stu-id="82fa4-197">The default schedule is once a day.</span></span> <span data-ttu-id="82fa4-198">Toutefois, le cron doit fonctionner plus fréquemment pour garder tout synchronisé.</span><span class="sxs-lookup"><span data-stu-id="82fa4-198">However, the cron must run more frequently to keep everything in sync.</span></span>

1. <span data-ttu-id="82fa4-199">Revenez à la page d’administration des plugins, **à l’administration du site > à l’intégration > Microsoft 365 et** sélectionnez la page **Teams Paramètres** site.</span><span class="sxs-lookup"><span data-stu-id="82fa4-199">Return to the plugins administration page, **Site administration > Plugins > Microsoft 365 Integration**, and select the **Teams Settings** page.</span></span>

1. <span data-ttu-id="82fa4-200">Sur la page **Teams Paramètres,** configurez les paramètres requis pour activer l’intégration Teams’application.</span><span class="sxs-lookup"><span data-stu-id="82fa4-200">On the **Teams Settings** page, configure the required settings to enable the Teams app integration.</span></span>

    1. <span data-ttu-id="82fa4-201">Pour activer **OpenID Connecter**, sélectionnez le lien **d’authentification Manage** et sélectionnez l’icône **œil sur la ligne openid Connecter** si elle est grisonnée.</span><span class="sxs-lookup"><span data-stu-id="82fa4-201">To enable **OpenID Connect**, select the **Manage Authentication** link, and select the eye icon on the **OpenId Connect** line if it is greyed out.</span></span>
    1. <span data-ttu-id="82fa4-202">Pour activer l’intégration du cadre, sélectionnez le **lien HTTP Security,** puis sélectionnez la case à cocher à côté pour **autoriser l’intégration du cadre.**</span><span class="sxs-lookup"><span data-stu-id="82fa4-202">To enable frame embedding, select the **HTTP Security** link, and then select the checkbox next to **Allow frame embedding**.</span></span>
    1. <span data-ttu-id="82fa4-203">Pour activer les services Web, qui permettent les fonctionnalités de l’API Moodle, sélectionnez **le lien Fonctionnalités** avancées, puis assurez-vous que la case à cocher **à côté des services Web Enable** est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="82fa4-203">To enable web services, which enables the Moodle API features, select the **Advanced Features** link, and then ensure the checkbox next to **Enable web services** is selected.</span></span>
    1. <span data-ttu-id="82fa4-204">Pour activer les services externes pour Microsoft 365, sélectionnez le **lien services** externes, puis :</span><span class="sxs-lookup"><span data-stu-id="82fa4-204">To enable the external services for Microsoft 365, select the **External services** link, and then:</span></span>  

        <span data-ttu-id="82fa4-205">✔ **Sélectionnez Modifier** sur **la ligne Moodle Microsoft 365 Webservices.**</span><span class="sxs-lookup"><span data-stu-id="82fa4-205">✔ Select **Edit** on the **Moodle Microsoft 365 Webservices** row.</span></span>

        <span data-ttu-id="82fa4-206">✔ sélectionnez la case à cocher à côté **de Activé,** puis sélectionnez **Enregistrer les modifications**</span><span class="sxs-lookup"><span data-stu-id="82fa4-206">✔ Select the checkbox next to **Enabled**, then select **Save Changes**</span></span>

    1. <span data-ttu-id="82fa4-207">Modifiez vos autorisations utilisateur authentifiées pour leur permettre de créer des jetons de service Web.</span><span class="sxs-lookup"><span data-stu-id="82fa4-207">Edit your authenticated user permissions to allow them to create web service tokens.</span></span>

        <span data-ttu-id="82fa4-208">✔ le rôle **d’édition Lien utilisateur authentifié.**</span><span class="sxs-lookup"><span data-stu-id="82fa4-208">✔ Select the **Editing role Authenticated user** link.</span></span>

        <span data-ttu-id="82fa4-209">✔ faites défiler vers le bas et **trouvez la fonctionnalité de jetons de service Web** Create a et sélectionnez la case à cocher **Autoriser.**</span><span class="sxs-lookup"><span data-stu-id="82fa4-209">✔ Scroll down and find the **Create a web service token** capability and select the **Allow** checkbox.</span></span>

## <a name="3-deploy-the-moodle-assistant-bot-to-azure"></a><span data-ttu-id="82fa4-210">3. Déployer le Moodle Assistant Bot sur Azure</span><span class="sxs-lookup"><span data-stu-id="82fa4-210">3. Deploy the Moodle Assistant Bot to Azure</span></span>

<span data-ttu-id="82fa4-211">Le bot gratuit assistant Moodle pour les Microsoft Teams les enseignants et les étudiants à répondre aux questions sur leurs cours, devoirs, notes, et d’autres informations dans Moodle.</span><span class="sxs-lookup"><span data-stu-id="82fa4-211">The free Moodle assistant bot for Microsoft Teams helps teachers and students answer questions about their courses, assignments, grades, and other information in Moodle.</span></span> <span data-ttu-id="82fa4-212">Le bot envoie également des notifications Moodle aux élèves et aux enseignants dans Teams.</span><span class="sxs-lookup"><span data-stu-id="82fa4-212">The bot also sends Moodle notifications to students and teachers within Teams.</span></span> <span data-ttu-id="82fa4-213">Le bot est un projet open-source maintenu par Microsoft, et est disponible sur [GitHub](https://github.com/microsoft/Moodle-Teams-Bot).</span><span class="sxs-lookup"><span data-stu-id="82fa4-213">The bot is an open-source project maintained by Microsoft, and is available on [GitHub](https://github.com/microsoft/Moodle-Teams-Bot).</span></span>

> [!NOTE]
>
> * <span data-ttu-id="82fa4-214">Déployez des ressources sur votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="82fa4-214">Deploy resources to your Azure subscription.</span></span> <span data-ttu-id="82fa4-215">Toutes les ressources ont été configurées à l’aide **du** niveau gratuit.</span><span class="sxs-lookup"><span data-stu-id="82fa4-215">All resources were configured using the **free** tier.</span></span> <span data-ttu-id="82fa4-216">Selon l’utilisation de votre bot, vous devrez peut-être mettre à l’échelle ces ressources.</span><span class="sxs-lookup"><span data-stu-id="82fa4-216">Depending on the usage of your bot, you may have to scale these resources.</span></span>
>
> * <span data-ttu-id="82fa4-217">Pour utiliser l’onglet Moodle sans le bot, passer à [4](#4-deploy-your-microsoft-teams-app).</span><span class="sxs-lookup"><span data-stu-id="82fa4-217">To use the Moodle tab without the bot, skip to [4](#4-deploy-your-microsoft-teams-app).</span></span>

### <a name="moodle-bot-information-flow"></a><span data-ttu-id="82fa4-218">Flux d’information de bot moodle</span><span class="sxs-lookup"><span data-stu-id="82fa4-218">Moodle bot information flow</span></span>

<img width="530px" src="../assets/images/MoodleBotInformationFlow.png" alt="Moodle bot for Microsoft Teams information flow" />

<span data-ttu-id="82fa4-219">Pour installer le bot, vous devez l’enregistrer sur la [plate-forme d’identité Microsoft](https://identity.microsoft.com/Landing).</span><span class="sxs-lookup"><span data-stu-id="82fa4-219">To install the bot, you must register it on the [Microsoft Identity Platform](https://identity.microsoft.com/Landing).</span></span> <span data-ttu-id="82fa4-220">Cela permet à votre bot de s’authentifier par rapport à vos paramètres Microsoft.</span><span class="sxs-lookup"><span data-stu-id="82fa4-220">This allows your bot to authenticate against your Microsoft endpoints.</span></span> 

<span data-ttu-id="82fa4-221">**Pour enregistrer votre bot**</span><span class="sxs-lookup"><span data-stu-id="82fa4-221">**To register your bot**</span></span>

1. <span data-ttu-id="82fa4-222">Allez à la page d’administration plugins, puis sélectionnez **Plugins**.</span><span class="sxs-lookup"><span data-stu-id="82fa4-222">Go to the plugins administration page, and then select **Plugins**.</span></span> <span data-ttu-id="82fa4-223">Sous **Microsoft 365'intégration,** sélectionnez **l’onglet** Teams Paramètres’eau.</span><span class="sxs-lookup"><span data-stu-id="82fa4-223">Under **Microsoft 365 Integration**, select the **Teams Settings** tab.</span></span>

1. <span data-ttu-id="82fa4-224">Sélectionnez le **lien Portail d’enregistrement d’applications Microsoft** et connectez-vous avec votre identifiant Microsoft.</span><span class="sxs-lookup"><span data-stu-id="82fa4-224">Select the **Microsoft Application Registration Portal** link and sign in with your Microsoft ID.</span></span>

1. <span data-ttu-id="82fa4-225">Entrez un nom pour votre application, tel que MoodleBot et sélectionnez le **bouton Créer.**</span><span class="sxs-lookup"><span data-stu-id="82fa4-225">Enter a name for your app, such as MoodleBot and select the **Create** button.</span></span>

1. <span data-ttu-id="82fa4-226">Copiez **l’ID d’application** et passez-le dans **le champ d’identification de** l’application Bot sur la page **Paramètres’équipe.**</span><span class="sxs-lookup"><span data-stu-id="82fa4-226">Copy the **Application ID** and paste it into the **Bot Application ID** field on the **Team Settings** page.</span></span>

1. <span data-ttu-id="82fa4-227">Sélectionnez le **bouton Générer un nouveau mot** de passe.</span><span class="sxs-lookup"><span data-stu-id="82fa4-227">Select the **Generate New Password** button.</span></span> <span data-ttu-id="82fa4-228">Copiez le mot de passe généré et coller dans le champ **Mot de passe d’application Bot** sur la page **Paramètres’équipe.**</span><span class="sxs-lookup"><span data-stu-id="82fa4-228">Copy the generated password and and paste it into the **Bot Application Password** field on the **Team Settings** page.</span></span>

1. <span data-ttu-id="82fa4-229">Faites défiler vers le bas du formulaire et sélectionnez **Enregistrer les modifications**.</span><span class="sxs-lookup"><span data-stu-id="82fa4-229">Scroll to the bottom of the form and select **Save Changes**.</span></span>

<span data-ttu-id="82fa4-230">Après avoir généré votre identifiant d’application et votre mot de passe, déployez votre bot sur Azure :</span><span class="sxs-lookup"><span data-stu-id="82fa4-230">After generating your application ID and password, deploy your bot to Azure:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="82fa4-231">Sélectionnez **Déployer sur Azure** et remplissez le formulaire avec les informations nécessaires, telles que l’ID d’application Bot, le mot de passe d’application Bot et le Secret Moodle sur la page **Teams Paramètres'** utilisateur.</span><span class="sxs-lookup"><span data-stu-id="82fa4-231">Select **Deploy to Azure** and complete the form with the necessary information, such as the Bot Application ID, Bot Application Password, and the Moodle Secret on the **Teams Settings** page.</span></span> <span data-ttu-id="82fa4-232">Les informations Azure sont sur la page **Configuration.**</span><span class="sxs-lookup"><span data-stu-id="82fa4-232">The Azure information is on the **Setup** page.</span></span> 
> * <span data-ttu-id="82fa4-233">Après avoir rempli le formulaire, sélectionnez la case à cocher pour accepter les modalités.</span><span class="sxs-lookup"><span data-stu-id="82fa4-233">After completing the form, select the checkbox to agree to the terms and conditions.</span></span>
> * <span data-ttu-id="82fa4-234">Sélectionnez **Achat**.</span><span class="sxs-lookup"><span data-stu-id="82fa4-234">Select **Purchase**.</span></span> <span data-ttu-id="82fa4-235">Toutes les ressources Azure sont déployées au niveau libre.</span><span class="sxs-lookup"><span data-stu-id="82fa4-235">All Azure resources are deployed to the free tier.</span></span>

<span data-ttu-id="82fa4-236">Une fois les ressources déployées sur Azure, vous devez configurer les plugins Moodle Microsoft 365 avec un point de terminaison de messagerie.</span><span class="sxs-lookup"><span data-stu-id="82fa4-236">After the resources have completed deploying to Azure, you must configure the Microsoft 365 Moodle plugins with a messaging endpoint.</span></span> <span data-ttu-id="82fa4-237">Vous devez obtenir le point de terminaison de votre bot dans Azure :</span><span class="sxs-lookup"><span data-stu-id="82fa4-237">You must get the endpoint from your bot in Azure:</span></span>

1. <span data-ttu-id="82fa4-238">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="82fa4-238">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="82fa4-239">Dans le volet gauche, sélectionnez groupes de **ressources et** sélectionnez le groupe de ressources que vous avez utilisé ou créé, tout en déployant votre bot.</span><span class="sxs-lookup"><span data-stu-id="82fa4-239">In the left pane, select **Resource groups** and select the resource group you used or created, while deploying your bot.</span></span>

1. <span data-ttu-id="82fa4-240">Sélectionnez **la ressource WebApp Bot** à partir de la liste des ressources du groupe.</span><span class="sxs-lookup"><span data-stu-id="82fa4-240">Select the **WebApp Bot** resource from the list of resources in the group.</span></span>

1. <span data-ttu-id="82fa4-241">Copiez le **point de terminaison de** messagerie de la section Vue **d’ensemble.**</span><span class="sxs-lookup"><span data-stu-id="82fa4-241">Copy the **Messaging Endpoint** from the **Overview** section.</span></span>

1. <span data-ttu-id="82fa4-242">Dans Moodle, ouvrez la **page Paramètres’équipe** de votre Microsoft 365 Moodle Plugins.</span><span class="sxs-lookup"><span data-stu-id="82fa4-242">In Moodle, open the **Team Settings** page of your Microsoft 365 Moodle Plugins.</span></span>

1. <span data-ttu-id="82fa4-243">Dans le **champ Bot Endpoint,** coller l’URL que vous venez de copier et modifier les *messages de mot* en *webhook*.</span><span class="sxs-lookup"><span data-stu-id="82fa4-243">In the **Bot Endpoint** field paste the URL you just copied and change the word *messages* to *webhook*.</span></span> <span data-ttu-id="82fa4-244">L’URL doit apparaître comme suit : `https://botname.azurewebsites.net/api/webhook`</span><span class="sxs-lookup"><span data-stu-id="82fa4-244">The URL must appear as follows: `https://botname.azurewebsites.net/api/webhook`</span></span>

1. <span data-ttu-id="82fa4-245">Sélectionnez **Enregistrer les modifications**.</span><span class="sxs-lookup"><span data-stu-id="82fa4-245">Select **Save Changes**.</span></span>

1. <span data-ttu-id="82fa4-246">Après avoir sélectionné les modifications, retournez à **l’onglet Team Paramètres,** sélectionnez **le bouton Télécharger le fichier manifeste** et enregistrez le paquet manifeste de l’application sur votre ordinateur pour une utilisation supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="82fa4-246">After saving the changes, go back to the **Team Settings** tab, select the **Download manifest file** button, and save the app manifest package to your computer for further use.</span></span>

## <a name="4-deploy-your-microsoft-teams-app"></a><span data-ttu-id="82fa4-247">4. Déployez votre application Microsoft Teams’argent</span><span class="sxs-lookup"><span data-stu-id="82fa4-247">4. Deploy your Microsoft Teams app</span></span>

<span data-ttu-id="82fa4-248">Après le déploiement de votre bot sur Azure et configuré pour parler à votre serveur Moodle, vous devez déployer votre Microsoft Teams application.</span><span class="sxs-lookup"><span data-stu-id="82fa4-248">After your bot deployed to Azure and configured to talk to your Moodle server, you must deploy your Microsoft Teams app.</span></span> <span data-ttu-id="82fa4-249">Pour ce faire, vous devez charger le fichier manifeste de l’application que vous avez téléchargé à partir de la page Microsoft 365 Moodle Plugins Team Paramètres dans l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="82fa4-249">To do this you must load the app manifest file that you downloaded from the Microsoft 365 Moodle Plugins Team Settings page in the previous step.</span></span>

<span data-ttu-id="82fa4-250">Avant d’installer l’application, vous devez vous assurer d’activer les applications externes et le téléchargement d’applications.</span><span class="sxs-lookup"><span data-stu-id="82fa4-250">Before you install the app you must ensure to enable external apps and uploading of apps.</span></span> <span data-ttu-id="82fa4-251">Pour plus d’informations, [consultez Préparer votre Microsoft 365 locataire.](../concepts/build-and-test/prepare-your-o365-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="82fa4-251">For more information, see [Prepare your Microsoft 365 tenant](../concepts/build-and-test/prepare-your-o365-tenant.md).</span></span> 

<span data-ttu-id="82fa4-252">**Pour déployer votre application**</span><span class="sxs-lookup"><span data-stu-id="82fa4-252">**To deploy your app**</span></span> 

1. <span data-ttu-id="82fa4-253">Ouvrez **Microsoft Teams**.</span><span class="sxs-lookup"><span data-stu-id="82fa4-253">Open **Microsoft Teams**.</span></span> 

1. <span data-ttu-id="82fa4-254">Sélectionnez **l’icône** App sur la zone inférieure gauche de la barre de navigation.</span><span class="sxs-lookup"><span data-stu-id="82fa4-254">Select the **App** icon on the lower-left area of the navigation bar.</span></span>

1. <span data-ttu-id="82fa4-255">Sélectionnez le **Télécharger un lien d’application** personnalisé à partir de la liste des options.</span><span class="sxs-lookup"><span data-stu-id="82fa4-255">Select the **Upload a custom app** link from the list of options.</span></span>

   > [!NOTE]
   > <span data-ttu-id="82fa4-256">Si vous êtes connecté en tant qu’administrateur global, vous devez avoir la possibilité de télécharger l’application sur le catalogue d’applications de votre organisation, sinon vous ne pouvez charger l’application que pour une équipe dont vous êtes membre.</span><span class="sxs-lookup"><span data-stu-id="82fa4-256">If you are logged in as a global administrator, you must have the option of uploading the app to your organization's app catalog, otherwise you can only load the app for a team in which you are a member.</span></span>

4. <span data-ttu-id="82fa4-257">Sélectionnez le `manifest.zip` package que vous avez téléchargé précédemment et sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="82fa4-257">Select the `manifest.zip` package you downloaded previously and select **Save**.</span></span> <span data-ttu-id="82fa4-258">Si vous n’avez pas téléchargé le paquet manifeste de l’application, vous pouvez télécharger **à partir de l’onglet Team Paramètres** de la page de configuration des plugins dans Moodle.</span><span class="sxs-lookup"><span data-stu-id="82fa4-258">If you have not downloaded the app manifest package, you can download from the **Team Settings** tab of the plugins configuration page in Moodle.</span></span>

<span data-ttu-id="82fa4-259">Maintenant que vous avez installé l’application, vous pouvez ajouter l’onglet à n’importe quel canal à qui vous avez accès.</span><span class="sxs-lookup"><span data-stu-id="82fa4-259">Now that you have the app installed, you can add the tab to any channel that you have access to.</span></span> <span data-ttu-id="82fa4-260">Pour ce faire, accédez au canal, **sélectionnez le symbole plus** (➕) et sélectionnez votre application dans la liste.</span><span class="sxs-lookup"><span data-stu-id="82fa4-260">To do so, navigate to the channel, select the **plus** (➕) symbol and select your app from the list.</span></span> <span data-ttu-id="82fa4-261">Suivez les invites pour terminer l’ajout de votre onglet de cours Moodle à un canal.</span><span class="sxs-lookup"><span data-stu-id="82fa4-261">Follow the prompts to finish adding your Moodle course tab to a channel.</span></span>

## <a name="5-allow-automatic-creation-of-moodle-tabs-in-microsoft-teams"></a><span data-ttu-id="82fa4-262">5. Autoriser la création automatique d’onglets Moodle dans Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="82fa4-262">5. Allow automatic creation of Moodle tabs in Microsoft Teams</span></span>

<span data-ttu-id="82fa4-263">Bien que les onglets Moodle soient créés manuellement dans Microsoft Teams, vous pouvez décider de les créer automatiquement lorsque des équipes sont créées à partir de la synchronisation des cours.</span><span class="sxs-lookup"><span data-stu-id="82fa4-263">Although the Moodle tabs are created manually in Microsoft Teams, you can decide to create them automatically when teams are created from course synchronization.</span></span> <span data-ttu-id="82fa4-264">Pour ce faire, vous devez configurer l’iD de l’application Microsoft Teams téléchargée dans Moodle.</span><span class="sxs-lookup"><span data-stu-id="82fa4-264">To do this, you must configure the ID of the uploaded Microsoft Teams app in Moodle.</span></span>

<span data-ttu-id="82fa4-265">**Pour permettre la création automatique d’onglets Moodle**</span><span class="sxs-lookup"><span data-stu-id="82fa4-265">**To allow automatic creation of Moodle tabs**</span></span>

1. <span data-ttu-id="82fa4-266">Ouvrir Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="82fa4-266">Open Microsoft Teams.</span></span>

1. <span data-ttu-id="82fa4-267">Sélectionnez l’icône Apps dans la zone inférieure gauche de la barre de navigation.</span><span class="sxs-lookup"><span data-stu-id="82fa4-267">Select the Apps icon from the lower-left area of the navigation bar.</span></span>

1. <span data-ttu-id="82fa4-268">Localisez **l’application Moodle téléchargée** > l’icône **options** > sélectionner le **lien de copie**.</span><span class="sxs-lookup"><span data-stu-id="82fa4-268">Locate the uploaded **Moodle app** > select the **options** icon > select **copy link**.</span></span>

1. <span data-ttu-id="82fa4-269">Dans un éditeur de texte, coller le contenu copié.</span><span class="sxs-lookup"><span data-stu-id="82fa4-269">In a text editor, paste the copied content.</span></span> <span data-ttu-id="82fa4-270">Il doit contenir une URL telle que ht&#8203;tps://teams.microsoft.com/l/app/00112233-4455-6677-8899-aabbccddeeff.</span><span class="sxs-lookup"><span data-stu-id="82fa4-270">It must contain a URL such as ht&#8203;tps://teams.microsoft.com/l/app/00112233-4455-6677-8899-aabbccddeeff.</span></span> <span data-ttu-id="82fa4-271">Copiez la dernière partie de l’URL, par exemple `00112233-4455-6677-8899-aabbccddeeff` , qui est l’ID de l’application Microsoft Teams’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="82fa4-271">Copy the last part of the URL, such as  `00112233-4455-6677-8899-aabbccddeeff`, which is the ID of the Microsoft Teams app.</span></span>

1. <span data-ttu-id="82fa4-272">Dans Moodle, ouvrez **l’onglet Teams’application Moodle** de votre page de configuration Microsoft 365 Moodle Plugins.</span><span class="sxs-lookup"><span data-stu-id="82fa4-272">In Moodle, open the **Teams Moodle app** tab from your Microsoft 365 Moodle Plugins configuration page.</span></span>

1. <span data-ttu-id="82fa4-273">Coller l’iD de l’application Microsoft Teams dans le champ d’identification de l’application Moodle, et enregistrer les modifications.</span><span class="sxs-lookup"><span data-stu-id="82fa4-273">Paste the ID of the Microsoft Teams app into the Moodle app ID field, and save changes.</span></span>

<span data-ttu-id="82fa4-274">Lorsqu’un cours Moodle est synchronisé, Microsoft Teams installe automatiquement l’application Moodle dans l’équipe, crée un onglet Moodle dans le canal général de Teams et la configure pour contenir la page de cours du cours Moodle à partir duquel elle est synchronisée.</span><span class="sxs-lookup"><span data-stu-id="82fa4-274">When a Moodle course is synced, Microsoft Teams automatically installs the Moodle app in the team, creates a Moodle tab in the General channel of Teams, and configures it to contain the course page for the Moodle course from which it is synced.</span></span> <span data-ttu-id="82fa4-275">Vous pouvez maintenant commencer à travailler avec vos cours Moodle directement à partir de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="82fa4-275">You can now start working with your Moodle courses directly from Microsoft Teams.</span></span>

> [!NOTE]
> <span data-ttu-id="82fa4-276">Pour partager toutes les demandes de fonctionnalités ou commentaires avec nous, visitez notre [page Voix utilisateur](https://microsoftteams.uservoice.com/forums/916759-moodle).</span><span class="sxs-lookup"><span data-stu-id="82fa4-276">To share any feature requests or feedback with us, visit our [User Voice page](https://microsoftteams.uservoice.com/forums/916759-moodle).</span></span>

## <a name="see-also"></a><span data-ttu-id="82fa4-277">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="82fa4-277">See also</span></span>

- [<span data-ttu-id="82fa4-278">Intégrer les applications Web</span><span class="sxs-lookup"><span data-stu-id="82fa4-278">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)
- [<span data-ttu-id="82fa4-279">Moodle</span><span class="sxs-lookup"><span data-stu-id="82fa4-279">Moodle</span></span>](https://moodle.org/)
- <span data-ttu-id="82fa4-280">[Documentation Moodle](https://docs.moodle.org/34/en/Installing_plugins).</span><span class="sxs-lookup"><span data-stu-id="82fa4-280">[Moodle documentation](https://docs.moodle.org/34/en/Installing_plugins).</span></span>

