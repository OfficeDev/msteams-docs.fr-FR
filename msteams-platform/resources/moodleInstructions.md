---
title: Installer Moodle LMS
description: Comment installer et configurer l’application d’intégration Dentele pour Microsoft Teams
keywords: Teams Plug-ins d’intégration d’application Dente
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
author: surbhigupta
ms.openlocfilehash: 54f4fec4e240f866c686ed715bd5093a319a2a48
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069170"
---
# <a name="install-moodle-lms"></a><span data-ttu-id="f9e0f-104">Installer Moodle LMS</span><span class="sxs-lookup"><span data-stu-id="f9e0f-104">Install Moodle LMS</span></span>

<span data-ttu-id="f9e0f-105">Dans cet article, vous allez apprendre à installer le LMS DeNte.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-105">In this article you'll learn how to install the Moodle LMS.</span></span>

> [!NOTE]
> <span data-ttu-id="f9e0f-106">Pour aider les administrateurs informatiques à configurer facilement l’intégration de Teams et De Latuale, open source Microsoft 365 Plug-ins Enfichables Est mis à jour pour les raisons suivantes :</span><span class="sxs-lookup"><span data-stu-id="f9e0f-106">To help IT admins to easily set-up Moodle and Teams integration, open-source Microsoft 365 Moodle Plugins is updated for the following:</span></span>
>
> * <span data-ttu-id="f9e0f-107">Inscription automatique de votre serveur Dente avec [Azure Active Directory (Azure AD).](https://azure.microsoft.com/services/active-directory/)</span><span class="sxs-lookup"><span data-stu-id="f9e0f-107">Auto-registration of your Moodle server with [Azure Active Directory (Azure AD)](https://azure.microsoft.com/services/active-directory/).</span></span>
>
> * <span data-ttu-id="f9e0f-108">Déploiement en un seul clic de votre bot Assistant d’accès à Azure.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-108">One-click deployment of your Moodle Assistant bot to Azure.</span></span>
>
> * <span data-ttu-id="f9e0f-109">Mise en service automatique des équipes et synchronisation automatique des inscriptions d’équipes pour toutes les équipes ou sélectionnez Des cours De commercialisation.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-109">Auto-provisioning of teams and auto-synchronization of team enrollments for all or select Moodle courses.</span></span>
>
> * <span data-ttu-id="f9e0f-110">Installation automatique de l’onglet Dente et du bot assistant Dentier dans chaque équipe synchronisée.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-110">Auto-installation of the Moodle tab and the Moodle assistant bot into each synchronized team.</span></span>
>
> <span data-ttu-id="f9e0f-111">Pour en savoir plus sur les fonctionnalités que fournit cette intégration, [voir Microsoft Teams et Lassy.](https://education.microsoft.com/resource/3dffb3a8)</span><span class="sxs-lookup"><span data-stu-id="f9e0f-111">To learn more about the functionality this integration provides, see [Microsoft Teams and Moodle](https://education.microsoft.com/resource/3dffb3a8).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f9e0f-112">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="f9e0f-112">Prerequisites</span></span>

<span data-ttu-id="f9e0f-113">Voici les conditions préalables à l’installation de Sondèle :</span><span class="sxs-lookup"><span data-stu-id="f9e0f-113">Following are the prerequisites to install Moodle:</span></span>

* <span data-ttu-id="f9e0f-114">Informations d’identification de l’administrateur en cas de mauvaises choses.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-114">Moodle administrator credentials.</span></span>

* <span data-ttu-id="f9e0f-115">Informations d’identification de l’administrateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-115">Azure AD administrator credentials.</span></span>

* <span data-ttu-id="f9e0f-116">Un abonnement Azure dans lequel vous pouvez créer de nouvelles ressources.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-116">An Azure subscription where you can create new resources.</span></span>

## <a name="1-install-the-microsoft-365-moodle-plugins"></a><span data-ttu-id="f9e0f-117">1. Installer les plug-Microsoft 365 Plug-ins Enfichables</span><span class="sxs-lookup"><span data-stu-id="f9e0f-117">1. Install the Microsoft 365 Moodle Plugins</span></span>

<span data-ttu-id="f9e0f-118">L’intégration de La Microsoft Teams est optimisée par l’open source [Microsoft 365 plug-ins Le jeu de plug-ins Enfichables.](https://github.com/Microsoft/o365-moodle)</span><span class="sxs-lookup"><span data-stu-id="f9e0f-118">Moodle integration in Microsoft Teams is powered by the open source [Microsoft 365 Moodle plugins set](https://github.com/Microsoft/o365-moodle).</span></span>

### <a name="requisite-applications-and-plugins"></a><span data-ttu-id="f9e0f-119">Applications et plug-ins requis</span><span class="sxs-lookup"><span data-stu-id="f9e0f-119">Requisite applications and plugins</span></span>

<span data-ttu-id="f9e0f-120">Assurez-vous d’installer et de télécharger les données suivantes avant de poursuivre l’installation Microsoft 365 plug-ins Enfichables Enfichables :</span><span class="sxs-lookup"><span data-stu-id="f9e0f-120">Ensure to install and download the following before proceeding with the Microsoft 365 Moodle plugins installation:</span></span>

1. <span data-ttu-id="f9e0f-121">Assurez-vous d’installer [une version stable actuelle de Lasa.](https://download.moodle.org/releases/latest/)</span><span class="sxs-lookup"><span data-stu-id="f9e0f-121">Ensure to install a [current stable version of Moodle](https://download.moodle.org/releases/latest/).</span></span>

1. <span data-ttu-id="f9e0f-122">Téléchargez et enregistrez les [plug-ins](https://moodle.org/plugins/auth_oidc) d’Connecter Et d’intégration [Microsoft 365](https://moodle.org/plugins/local_o365) à votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-122">Download and save the Moodle [OpenID Connect](https://moodle.org/plugins/auth_oidc) and the [Microsoft 365 Integration](https://moodle.org/plugins/local_o365) plugins to your local computer.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f9e0f-123">L’installation des plug-ins OpenID Connecter et Microsoft 365'intégration est requise pour l’intégration Teams’installation.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-123">Installing the OpenID Connect and Microsoft 365 Integration plugins are required for the Teams integration.</span></span>
    >
    > <span data-ttu-id="f9e0f-124">En outre, les [plug-ins Microsoft 365 Teams Thème](https://moodle.org/plugins/theme_boost_o365teams) sont vivement recommandés.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-124">In addition, the [Microsoft 365 Teams Theme](https://moodle.org/plugins/theme_boost_o365teams) plugins is highly recommended.</span></span>

### <a name="microsoft-365-moodle-plugins"></a><span data-ttu-id="f9e0f-125">Microsoft 365 Plug-ins Dentelé</span><span class="sxs-lookup"><span data-stu-id="f9e0f-125">Microsoft 365 Moodle plugins</span></span>

1. <span data-ttu-id="f9e0f-126">Connectez-vous à votre serveur En tant qu’administrateur, puis sélectionnez Administration du **site** dans le bloc [Paramètres](https://docs.moodle.org/22/en/Settings_block) situé dans le panneau de navigation de gauche.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-126">Sign in to your Moodle server as an administrator and select **Site administration** from the [Settings block](https://docs.moodle.org/22/en/Settings_block) located in the left navigation panel.</span></span>

1. <span data-ttu-id="f9e0f-127">Sélectionnez **l’onglet Plug-ins,** puis installez **les plug-ins.**</span><span class="sxs-lookup"><span data-stu-id="f9e0f-127">Select the **Plugins** tab, and then select **Install plugins**.</span></span>

1. <span data-ttu-id="f9e0f-128">Dans la section **Installer les plug-ins à** partir du fichier ZIP, **sélectionnez Choisir un fichier.**</span><span class="sxs-lookup"><span data-stu-id="f9e0f-128">From the **Install plugins from ZIP file** section, select **Choose a file**.</span></span>

1. <span data-ttu-id="f9e0f-129">Sélectionnez **Télécharger une** option de fichier dans le panneau de navigation de gauche, recherchez le fichier que vous avez téléchargé, puis sélectionnez Télécharger **ce fichier.**</span><span class="sxs-lookup"><span data-stu-id="f9e0f-129">Select **Upload a file** option from the left navigation panel, browse for the file that you downloaded, and select **Upload this file**.</span></span>

1. <span data-ttu-id="f9e0f-130">Sélectionnez **Administration du site** dans le panneau de navigation de gauche pour revenir à votre tableau de bord d’administration.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-130">Select **Site administration** from the left navigation panel to return to your admin dashboard.</span></span> <span data-ttu-id="f9e0f-131">Faites défiler vers le bas **jusqu’aux plug-ins locaux** et sélectionnez **le lien Microsoft 365'intégration** locale.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-131">Scroll down to the **Local plugins** and select the **Microsoft 365 Integration** link.</span></span>

    > [!IMPORTANT]
    >
    > * <span data-ttu-id="f9e0f-132">Gardez votre page Microsoft 365 configuration des plug-ins En forme de jeu ouverte dans un onglet de navigateur distinct, car vous devez revenir à cet ensemble de pages tout au long du processus.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-132">Keep your Microsoft 365 Moodle Plugins configuration page open in a separate browser tab as you need to return to this set of pages throughout the process.</span></span>  
    >
    > * <span data-ttu-id="f9e0f-133">Si vous n’avez pas de site Vous pouvez le faire, rendez-vous dans le repo [D’Azure,](https://github.com/azure/moodle) puis déployez rapidement une instance De son côté et personnalisez-la en fonction de vos besoins.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-133">If you do not have an existing Moodle site, go to the [Moodle on Azure](https://github.com/azure/moodle) repo, and quickly deploy a Moodle instance and customize it to your needs.</span></span>

## <a name="2-configure-the-connection-between-the-microsoft-365-plugins-and-azure-active-directory-azure-ad"></a><span data-ttu-id="f9e0f-134">2. Configurer la connexion entre les plug-ins Microsoft 365 et Azure Active Directory (Azure AD)</span><span class="sxs-lookup"><span data-stu-id="f9e0f-134">2. Configure the connection between the Microsoft 365 plugins and Azure Active Directory (Azure AD)</span></span>

<span data-ttu-id="f9e0f-135">Vous devez configurer la connexion entre les plug-ins Microsoft 365 et Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-135">You must configure the connection between the Microsoft 365 plugins and Azure AD.</span></span>

### <a name="requisites"></a><span data-ttu-id="f9e0f-136">Conditions requises</span><span class="sxs-lookup"><span data-stu-id="f9e0f-136">Requisites</span></span>

<span data-ttu-id="f9e0f-137">Enregistrez Le jeu En tant qu’application dans Azure AD, à l’aide du script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-137">Register Moodle as an application in your Azure AD, using the PowerShell script.</span></span> <span data-ttu-id="f9e0f-138">Le script Powershell a les dispositions suivantes :</span><span class="sxs-lookup"><span data-stu-id="f9e0f-138">The Powershell script provisions the following:</span></span>

* <span data-ttu-id="f9e0f-139">Une nouvelle application Azure AD pour votre client Microsoft 365, qui est utilisée par les plug-ins Microsoft 365 Leindent.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-139">A new Azure AD application for your Microsoft 365 tenant, which is used by the Microsoft 365 Moodle Plugins.</span></span>
* <span data-ttu-id="f9e0f-140">L’application pour votre client Microsoft 365, configurer les URL de réponse requises et les autorisations pour l’application mise en service, et renvoie le `AppID` et `Key` .</span><span class="sxs-lookup"><span data-stu-id="f9e0f-140">The app for your Microsoft 365 tenant, set up the required reply URLs and permissions for the provisioned app, and returns the `AppID` and `Key`.</span></span>

<span data-ttu-id="f9e0f-141">Utilisez la page d’installation générée et dans votre Microsoft 365 Plug-ins En forme Pour configurer votre `AppID` site serveur `Key` Dentele avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-141">Use the generated `AppID` and `Key` in your Microsoft 365 Moodle Plugins setup page to configure your Moodle server site with Azure AD.</span></span>

> [!IMPORTANT]
>
> * <span data-ttu-id="f9e0f-142">Le script PowerShell n’est pas mis à jour avec les éléments de configuration les plus récents. Par conséquent, vous devez effectuer la configuration manuellement en suivant les étapes décrites dans les pages de publication De la version [3.8.0.4 et 3.9.1](https://docs.moodle.org/39/en/Office365#3.8.0.4_and_3.9.1_release) et [3.8.0.5 et 3.9.2.](https://docs.moodle.org/39/en/Office365#3.8.0.5_and_3.9.2_release)</span><span class="sxs-lookup"><span data-stu-id="f9e0f-142">The PowerShell script is not updated with the latest configuration items, therefore, you must complete the configuration manually following the steps outlined in the Moodle [3.8.0.4 and 3.9.1](https://docs.moodle.org/39/en/Office365#3.8.0.4_and_3.9.1_release) and [3.8.0.5 and 3.9.2](https://docs.moodle.org/39/en/Office365#3.8.0.5_and_3.9.2_release) release pages.</span></span>
>
> * <span data-ttu-id="f9e0f-143">Pour plus d’informations sur l’inscription manuelle de votre instance Dente, voir Enregistrer votre [instance Dente en tant qu’application.](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application)</span><span class="sxs-lookup"><span data-stu-id="f9e0f-143">For more information on registering your Moodle instance manually, see [Register your Moodle instance as an application](https://docs.moodle.org/34/en/Office365#Register_your_Moodle_instance_as_an_Application).</span></span>

### <a name="the-moodle-tab-for-microsoft-teams-information-flow"></a><span data-ttu-id="f9e0f-144">Onglet Dentelé pour le flux Microsoft Teams’informations</span><span class="sxs-lookup"><span data-stu-id="f9e0f-144">The Moodle tab for Microsoft Teams information flow</span></span>

<img width="530px" src="../assets/images/MoodleTabInformationFlow.png" alt="Moodle tab for Microsoft Teams information flow" />

1. <span data-ttu-id="f9e0f-145">Dans la page Microsoft 365 plug-ins Intégration, sélectionnez **l’onglet** Installation.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-145">From the Microsoft 365 Integration plugins page, select the **Setup** tab.</span></span>

1. <span data-ttu-id="f9e0f-146">Sélectionnez **le bouton Télécharger le script PowerShell** et enregistrez-le en tant que dossier ZIP sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-146">Select the **Download PowerShell Script** button and save it as a ZIP folder to your local computer.</span></span>

1. <span data-ttu-id="f9e0f-147">Préparez le script PowerShell à partir du fichier ZIP comme suit :</span><span class="sxs-lookup"><span data-stu-id="f9e0f-147">Prepare the PowerShell script from the ZIP file as follows:</span></span> 

    1. <span data-ttu-id="f9e0f-148">Téléchargez et extrayz le `Moodle-AzureAD-Powershell.zip` fichier.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-148">Download and extract the `Moodle-AzureAD-Powershell.zip` file.</span></span>
    1. <span data-ttu-id="f9e0f-149">Ouvrez le dossier extrait.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-149">Open the extracted folder.</span></span>
    1. <span data-ttu-id="f9e0f-150">Cliquez avec le bouton droit sur `Moodle-AzureAD-Script.ps1` le fichier et sélectionnez **Propriétés.**</span><span class="sxs-lookup"><span data-stu-id="f9e0f-150">Right-click on the `Moodle-AzureAD-Script.ps1` file and select **Properties**.</span></span>
    1. <span data-ttu-id="f9e0f-151">Sous **l’onglet Général** de la fenêtre Propriétés, cochez la case en regard de l’attribut Security situé en `Unblock` bas de la fenêtre. </span><span class="sxs-lookup"><span data-stu-id="f9e0f-151">Under the **General** tab of the Properties window, select the `Unblock` checkbox next to the **Security** attribute located at the bottom of the window.</span></span>
    1. <span data-ttu-id="f9e0f-152">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-152">Select **OK**.</span></span>
    1. <span data-ttu-id="f9e0f-153">Copiez le chemin d’accès au répertoire dans le dossier extrait.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-153">Copy the directory path to the extracted folder.</span></span>

1. <span data-ttu-id="f9e0f-154">Exécutez PowerShell en tant qu’administrateur :</span><span class="sxs-lookup"><span data-stu-id="f9e0f-154">Run PowerShell as an administrator:</span></span>

    1. <span data-ttu-id="f9e0f-155">Sélectionnez Démarrer.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-155">Select Start.</span></span>
    1. <span data-ttu-id="f9e0f-156">Tapez PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-156">Type PowerShell.</span></span>
    1. <span data-ttu-id="f9e0f-157">Cliquez avec le bouton **droit sur Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-157">Right-click on **Windows PowerShell**.</span></span>
    1. <span data-ttu-id="f9e0f-158">Sélectionnez **Exécuter en tant qu’administrateur.**</span><span class="sxs-lookup"><span data-stu-id="f9e0f-158">Select **Run as Administrator**.</span></span>

1. <span data-ttu-id="f9e0f-159">Accédez au répertoire décompressé en tapant où se trouve `cd .../.../Moodle-AzureAD-Powershell` `.../...` le chemin d’accès au répertoire.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-159">Navigate to the unzipped directory by typing `cd .../.../Moodle-AzureAD-Powershell` where `.../...` is the path to the directory.</span></span>

1. <span data-ttu-id="f9e0f-160">Exécutez le script PowerShell :</span><span class="sxs-lookup"><span data-stu-id="f9e0f-160">Execute the PowerShell script:</span></span>

    1. <span data-ttu-id="f9e0f-161">Entrez `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser` .</span><span class="sxs-lookup"><span data-stu-id="f9e0f-161">Enter `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser`.</span></span>
    1. <span data-ttu-id="f9e0f-162">Entrez `./Moodle-AzureAD-Script.ps1` .</span><span class="sxs-lookup"><span data-stu-id="f9e0f-162">Enter `./Moodle-AzureAD-Script.ps1`.</span></span>
    1. <span data-ttu-id="f9e0f-163">Connectez-vous à Microsoft 365 compte d’administrateur dans la fenêtre pop-up.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-163">Sign in to your Microsoft 365 administrator account in the pop-up window.</span></span>
    1. <span data-ttu-id="f9e0f-164">Entrez le nom de l’application Azure AD, par exemple, les plug-ins Il s’agit des plug-ins Il est vrai ou Non.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-164">Enter the name of the Azure AD Application, for example, Moodle or Moodle plugins.</span></span>
    1. <span data-ttu-id="f9e0f-165">Entrez l’URL de votre serveur Dentelé.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-165">Enter the URL for your Moodle server.</span></span>
    1. <span data-ttu-id="f9e0f-166">Copiez **l’ID d’application ( `AppID` ) et** la clé **d’application ( `Key` )** générés par le script et enregistrez-les.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-166">Copy the **Application ID (`AppID`)** and **Application Key(`Key`)** generated by the script and save them.</span></span>

1. <span data-ttu-id="f9e0f-167">Ensuite, vous devez ajouter les `AppID` `Key` plug-ins Microsoft 365 Et à l’autre.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-167">Next you must add the `AppID` and `Key` to the Microsoft 365 Moodle Plugins.</span></span> <span data-ttu-id="f9e0f-168">Revenir à la page d’administration des plug-ins, Administration du site > plug-ins > Microsoft 365'intégration.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-168">Return to the plugins administration page, Site administration > Plugins > Microsoft 365 Integration.</span></span>

1. <span data-ttu-id="f9e0f-169">Sous **l’onglet Installation,** ajoutez et `AppID` `Key` copiez-le précédemment, puis sélectionnez **Enregistrer les modifications.**</span><span class="sxs-lookup"><span data-stu-id="f9e0f-169">On the **Setup** tab add the `AppID` and `Key` you copied previously, and then select **Save changes**.</span></span> <span data-ttu-id="f9e0f-170">Une fois la page actualisée, vous pouvez voir une nouvelle section **Choisir la méthode de connexion.**</span><span class="sxs-lookup"><span data-stu-id="f9e0f-170">After the page refreshes, you can see a new section **Choose connection method**.</span></span>

1. <span data-ttu-id="f9e0f-171">Dans la **méthode Choisir une connexion,** cochez la case par **défaut,** puis sélectionnez **Enregistrer les modifications** à nouveau.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-171">In the **Choose connection method**, select the checkbox labeled **Default**, and then select **Save changes** again.</span></span>

1. <span data-ttu-id="f9e0f-172">Une fois la page actualisée, vous pouvez voir une autre nouvelle section consentement de **l’administrateur & informations supplémentaires.**</span><span class="sxs-lookup"><span data-stu-id="f9e0f-172">After the page refreshes you can see another new section **Admin consent & additional information**.</span></span>
    1. <span data-ttu-id="f9e0f-173">Sélectionnez **Fournir le lien Consentement de** l’administrateur, entrez Microsoft 365 informations d’identification de l’administrateur général, puis acceptez d’accorder les autorisations. </span><span class="sxs-lookup"><span data-stu-id="f9e0f-173">Select **Provide Admin Consent** link, enter your Microsoft 365 Global Administrator credentials, then **Accept** to grant the permissions.</span></span>
    1. <span data-ttu-id="f9e0f-174">En regard du **champ Client Azure AD,** sélectionnez **le bouton** Détecter.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-174">Next to the **Azure AD Tenant** field, select the **Detect** button.</span></span>
    1. <span data-ttu-id="f9e0f-175">En plus de **l OneDrive Entreprise URL,** sélectionnez **le bouton** Détecter.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-175">Next to the **OneDrive for Business URL**, select the **Detect** button.</span></span>
    1. <span data-ttu-id="f9e0f-176">Une fois les champs remplis, sélectionnez de nouveau le bouton Enregistrer **les modifications.**</span><span class="sxs-lookup"><span data-stu-id="f9e0f-176">After the fields populate, select the **Save changes** button again.</span></span>

1. <span data-ttu-id="f9e0f-177">Sélectionnez le **bouton** Mettre à jour pour vérifier l’installation, puis sélectionnez **Enregistrer les modifications.**</span><span class="sxs-lookup"><span data-stu-id="f9e0f-177">Select the **Update** button to verify the installation, and then select **Save changes**.</span></span>

1. <span data-ttu-id="f9e0f-178">Synchronisez les utilisateurs entre votre serveur Et Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-178">Synchronize users between your Moodle server and Azure AD.</span></span> <span data-ttu-id="f9e0f-179">Pour commencer :</span><span class="sxs-lookup"><span data-stu-id="f9e0f-179">To get started:</span></span>

    > [!NOTE]
    > <span data-ttu-id="f9e0f-180">En fonction de votre environnement, vous pouvez sélectionner différentes options au cours de cette étape.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-180">Depending on your environment, you can select different options during this stage.</span></span>

1. <span data-ttu-id="f9e0f-181">Synchronisez les utilisateurs entre votre serveur Et Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-181">Synchronize users between your Moodle server and Azure AD.</span></span> <span data-ttu-id="f9e0f-182">En fonction de votre environnement, vous pouvez sélectionner différentes options au cours de cette étape.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-182">Depending on your environment, you can select different options during this stage.</span></span> <span data-ttu-id="f9e0f-183">Pour commencer :</span><span class="sxs-lookup"><span data-stu-id="f9e0f-183">To get started:</span></span>
    1. <span data-ttu-id="f9e0f-184">Basculez vers **l’onglet Paramètres synchronisation.**</span><span class="sxs-lookup"><span data-stu-id="f9e0f-184">Switch to the **Sync Settings tab**.</span></span>

    1. <span data-ttu-id="f9e0f-185">Dans la section **Synchroniser les utilisateurs avec Azure AD,** cochez les case qui s’appliquent à votre environnement.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-185">In the **Sync users with Azure AD** section, select the checkboxes that apply to your environment.</span></span> <span data-ttu-id="f9e0f-186">Vous devez sélectionner ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="f9e0f-186">You must select the following:</span></span>  

        <span data-ttu-id="f9e0f-187">✔ créer des comptes dans Le Chatin pour les utilisateurs dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-187">✔ Create accounts in Moodle for users in Azure AD.</span></span>

        <span data-ttu-id="f9e0f-188">✔ tous les comptes dans Le Chatin pour les utilisateurs dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-188">✔ Update all accounts in Moodle for users in Azure AD.</span></span>

    1. <span data-ttu-id="f9e0f-189">Dans la section Restriction de création d’utilisateurs, vous pouvez configurer un filtre pour limiter les utilisateurs Azure AD synchronisés avec Lele. </span><span class="sxs-lookup"><span data-stu-id="f9e0f-189">In the **User Creation Restriction** section, you can setup a filter to limit the Azure AD users that is synced to Moodle.</span></span>
    1. <span data-ttu-id="f9e0f-190">La section **Mappage des champs** utilisateur vous permet de personnaliser Azure AD en mappage de champ De profil utilisateur en toute convivialisation.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-190">The **User Field Mapping** section allows you to customize the Azure AD to Moodle User Profile field mapping.</span></span>
    1. <span data-ttu-id="f9e0f-191">Dans la section **Teams** sync, vous pouvez choisir de créer automatiquement des groupes, tels que des équipes pour une partie ou l’ensemble, de vos cours Ententaux existants.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-191">In the **Teams Sync** section, you can select to automatically create Groups, such as teams for some, or all, of your existing Moodle courses.</span></span>

13. <span data-ttu-id="f9e0f-192">Pour valider [les travaux cron](https://docs.moodle.org/310/en/Cron) et les exécuter manuellement pour la première utilisation, sélectionnez le lien de **la page** Gestion des tâches programmées dans la section Synchroniser les utilisateurs avec **Azure AD.**</span><span class="sxs-lookup"><span data-stu-id="f9e0f-192">To validate [cron](https://docs.moodle.org/310/en/Cron) jobs and run them manually for the first run, select the **Scheduled tasks management page** link in the **Sync users with Azure AD** section.</span></span> <span data-ttu-id="f9e0f-193">Vous êtes alors sur la page **Tâches programmées.**</span><span class="sxs-lookup"><span data-stu-id="f9e0f-193">This takes you to the **Scheduled Tasks** page.</span></span>

    1. <span data-ttu-id="f9e0f-194">Faites défiler vers le bas et recherchez les utilisateurs de synchronisation avec le travail **Azure AD,** puis **sélectionnez Exécuter maintenant.**</span><span class="sxs-lookup"><span data-stu-id="f9e0f-194">Scroll down and find the **Sync users with Azure AD** job and select **Run now**.</span></span>
    1. <span data-ttu-id="f9e0f-195">Si vous choisissez de créer des groupes en fonction des cours existants, vous pouvez également exécuter le travail Créer des groupes d’utilisateurs **Microsoft 365** travail.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-195">If you select to create Groups based on existing courses, you can also run the **Create user groups in Microsoft 365** job.</span></span>

    > [!NOTE]
    >
    > <span data-ttu-id="f9e0f-196">Le [Cron](https://docs.moodle.org/310/en/Cron) DeNte s’exécute en fonction de la planification des tâches.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-196">The Moodle [Cron](https://docs.moodle.org/310/en/Cron) runs according to the task schedule.</span></span> <span data-ttu-id="f9e0f-197">La planification par défaut est une fois par jour.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-197">The default schedule is once a day.</span></span> <span data-ttu-id="f9e0f-198">Toutefois, le cron doit s’exécuter plus fréquemment pour que tout reste synchronisé.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-198">However, the cron must run more frequently to keep everything in sync.</span></span>

1. <span data-ttu-id="f9e0f-199">Revenir à la page d’administration des plug-ins, administration > **sites > Microsoft 365'intégration,** puis sélectionnez la page **Teams Paramètres** page.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-199">Return to the plugins administration page, **Site administration > Plugins > Microsoft 365 Integration**, and select the **Teams Settings** page.</span></span>

1. <span data-ttu-id="f9e0f-200">Sur la **Teams Paramètres** page, configurez les paramètres requis pour activer l’intégration Teams’application.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-200">On the **Teams Settings** page, configure the required settings to enable the Teams app integration.</span></span>

    1. <span data-ttu-id="f9e0f-201">Pour activer **OpenID Connecter,** sélectionnez le lien Gérer l’authentification, puis sélectionnez l’icône d’œil sur la ligne  **OpenId Connecter** si elle est grisée.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-201">To enable **OpenID Connect**, select the **Manage Authentication** link, and select the eye icon on the **OpenId Connect** line if it is greyed out.</span></span>
    1. <span data-ttu-id="f9e0f-202">Pour activer l’incorporation d’images, sélectionnez le lien **sécurité HTTP,** puis cochez la case en regard de l’incorporation **d’une image .**</span><span class="sxs-lookup"><span data-stu-id="f9e0f-202">To enable frame embedding, select the **HTTP Security** link, and then select the checkbox next to **Allow frame embedding**.</span></span>
    1. <span data-ttu-id="f9e0f-203">Pour activer les services web, qui activent  les fonctionnalités de l’API Contrôle d’accès, sélectionnez le lien Fonctionnalités avancées, puis assurez-vous que la case à cocher en regard de Activer les **services web** est activée.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-203">To enable web services, which enables the Moodle API features, select the **Advanced Features** link, and then ensure the checkbox next to **Enable web services** is selected.</span></span>
    1. <span data-ttu-id="f9e0f-204">Pour activer les services externes pour Microsoft 365, sélectionnez le lien **Services** externes, puis :</span><span class="sxs-lookup"><span data-stu-id="f9e0f-204">To enable the external services for Microsoft 365, select the **External services** link, and then:</span></span>  

        <span data-ttu-id="f9e0f-205">✔ **sélectionnez Modifier** sur la ligne **Microsoft 365 WebServices.**</span><span class="sxs-lookup"><span data-stu-id="f9e0f-205">✔ Select **Edit** on the **Moodle Microsoft 365 Webservices** row.</span></span>

        <span data-ttu-id="f9e0f-206">✔ cochez la case en regard de **Activé,** puis **sélectionnez Enregistrer les modifications**</span><span class="sxs-lookup"><span data-stu-id="f9e0f-206">✔ Select the checkbox next to **Enabled**, then select **Save Changes**</span></span>

    1. <span data-ttu-id="f9e0f-207">Modifiez vos autorisations utilisateur authentifiées pour leur permettre de créer des jetons de service web.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-207">Edit your authenticated user permissions to allow them to create web service tokens.</span></span>

        <span data-ttu-id="f9e0f-208">✔ sélectionnez le lien utilisateur authentifié du rôle **d’édition.**</span><span class="sxs-lookup"><span data-stu-id="f9e0f-208">✔ Select the **Editing role Authenticated user** link.</span></span>

        <span data-ttu-id="f9e0f-209">✔ faites défiler vers le bas et recherchez la fonctionnalité Créer un jeton **de service web** et cochez la **case** Autoriser.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-209">✔ Scroll down and find the **Create a web service token** capability and select the **Allow** checkbox.</span></span>

## <a name="3-deploy-the-moodle-assistant-bot-to-azure"></a><span data-ttu-id="f9e0f-210">3. Déployer le bot Assistant Dentelé sur Azure</span><span class="sxs-lookup"><span data-stu-id="f9e0f-210">3. Deploy the Moodle Assistant Bot to Azure</span></span>

<span data-ttu-id="f9e0f-211">Le bot d’assistant Free Moodle pour Microsoft Teams aide les enseignants et les étudiants à répondre à des questions sur leurs cours, devoirs, notes et autres informations dans Le jeu.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-211">The free Moodle assistant bot for Microsoft Teams helps teachers and students answer questions about their courses, assignments, grades, and other information in Moodle.</span></span> <span data-ttu-id="f9e0f-212">Le bot envoie également des notifications à l’adresse d’étudiants et d’enseignants Teams.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-212">The bot also sends Moodle notifications to students and teachers within Teams.</span></span> <span data-ttu-id="f9e0f-213">Le bot est un projet open source tenu à jour par Microsoft et est disponible [sur GitHub](https://github.com/microsoft/Moodle-Teams-Bot).</span><span class="sxs-lookup"><span data-stu-id="f9e0f-213">The bot is an open-source project maintained by Microsoft, and is available on [GitHub](https://github.com/microsoft/Moodle-Teams-Bot).</span></span>

> [!NOTE]
>
> * <span data-ttu-id="f9e0f-214">Déployez des ressources dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-214">Deploy resources to your Azure subscription.</span></span> <span data-ttu-id="f9e0f-215">Toutes les ressources ont été configurées à l’aide **du niveau** libre.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-215">All resources were configured using the **free** tier.</span></span> <span data-ttu-id="f9e0f-216">Selon l’utilisation de votre bot, vous de devez peut-être mettre à l’échelle ces ressources.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-216">Depending on the usage of your bot, you may have to scale these resources.</span></span>
>
> * <span data-ttu-id="f9e0f-217">Pour utiliser l’ongletUlation sans le bot, passez à [4](#4-deploy-your-microsoft-teams-app).</span><span class="sxs-lookup"><span data-stu-id="f9e0f-217">To use the Moodle tab without the bot, skip to [4](#4-deploy-your-microsoft-teams-app).</span></span>

### <a name="moodle-bot-information-flow"></a><span data-ttu-id="f9e0f-218">Flux d’informations sur le bot de chatouillement</span><span class="sxs-lookup"><span data-stu-id="f9e0f-218">Moodle bot information flow</span></span>

<img width="530px" src="../assets/images/MoodleBotInformationFlow.png" alt="Moodle bot for Microsoft Teams information flow" />

<span data-ttu-id="f9e0f-219">Pour installer le bot, vous devez l’inscrire sur la [plateforme d’identités Microsoft.](https://identity.microsoft.com/Landing)</span><span class="sxs-lookup"><span data-stu-id="f9e0f-219">To install the bot, you must register it on the [Microsoft Identity Platform](https://identity.microsoft.com/Landing).</span></span> <span data-ttu-id="f9e0f-220">Cela permet à votre bot de s’authentifier sur vos points de terminaison Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-220">This allows your bot to authenticate against your Microsoft endpoints.</span></span> 

<span data-ttu-id="f9e0f-221">**Pour inscrire votre bot**</span><span class="sxs-lookup"><span data-stu-id="f9e0f-221">**To register your bot**</span></span>

1. <span data-ttu-id="f9e0f-222">Go to the plugins administration page, and then select **Plugins**.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-222">Go to the plugins administration page, and then select **Plugins**.</span></span> <span data-ttu-id="f9e0f-223">Sous **Microsoft 365'intégration,** sélectionnez **Teams Paramètres’onglet.**</span><span class="sxs-lookup"><span data-stu-id="f9e0f-223">Under **Microsoft 365 Integration**, select the **Teams Settings** tab.</span></span>

1. <span data-ttu-id="f9e0f-224">Sélectionnez le **lien Portail d’inscription des** applications Microsoft et connectez-vous avec votre ID Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-224">Select the **Microsoft Application Registration Portal** link and sign in with your Microsoft ID.</span></span>

1. <span data-ttu-id="f9e0f-225">Entrez un nom pour votre application, tel que SondentleBot, puis sélectionnez **le bouton** Créer.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-225">Enter a name for your app, such as MoodleBot and select the **Create** button.</span></span>

1. <span data-ttu-id="f9e0f-226">Copiez **l’ID d’application** et collez-le dans le champ **ID de l’application** bot sur la page **Paramètres** équipe.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-226">Copy the **Application ID** and paste it into the **Bot Application ID** field on the **Team Settings** page.</span></span>

1. <span data-ttu-id="f9e0f-227">Sélectionnez le **bouton Générer un nouveau mot de** passe.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-227">Select the **Generate New Password** button.</span></span> <span data-ttu-id="f9e0f-228">Copiez le mot de passe généré et collez-le dans le champ Mot de passe de **l’application** bot sur la page **Paramètres** équipe.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-228">Copy the generated password and and paste it into the **Bot Application Password** field on the **Team Settings** page.</span></span>

1. <span data-ttu-id="f9e0f-229">Faites défiler jusqu’au bas du formulaire et sélectionnez **Enregistrer les modifications.**</span><span class="sxs-lookup"><span data-stu-id="f9e0f-229">Scroll to the bottom of the form and select **Save Changes**.</span></span>

<span data-ttu-id="f9e0f-230">Après avoir généré votre ID d’application et votre mot de passe, déployez votre bot sur Azure :</span><span class="sxs-lookup"><span data-stu-id="f9e0f-230">After generating your application ID and password, deploy your bot to Azure:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f9e0f-231">Sélectionnez Déployer sur **Azure** et complétez le formulaire avec les informations nécessaires, telles que l’ID de l’application bot, le mot de passe de l’application bot et le secret de l’Teams Paramètres **page.**</span><span class="sxs-lookup"><span data-stu-id="f9e0f-231">Select **Deploy to Azure** and complete the form with the necessary information, such as the Bot Application ID, Bot Application Password, and the Moodle Secret on the **Teams Settings** page.</span></span> <span data-ttu-id="f9e0f-232">Les informations Azure se trouve sur la page **d’installation.**</span><span class="sxs-lookup"><span data-stu-id="f9e0f-232">The Azure information is on the **Setup** page.</span></span> 
> * <span data-ttu-id="f9e0f-233">Une fois le formulaire terminé, cochez la case pour accepter les conditions générales.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-233">After completing the form, select the checkbox to agree to the terms and conditions.</span></span>
> * <span data-ttu-id="f9e0f-234">Sélectionnez **Acheter.**</span><span class="sxs-lookup"><span data-stu-id="f9e0f-234">Select **Purchase**.</span></span> <span data-ttu-id="f9e0f-235">Toutes les ressources Azure sont déployées sur le niveau gratuit.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-235">All Azure resources are deployed to the free tier.</span></span>

<span data-ttu-id="f9e0f-236">Une fois le déploiement des ressources terminé sur Azure, vous devez configurer les plug-ins Microsoft 365 Leindent avec un point de terminaison de messagerie.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-236">After the resources have completed deploying to Azure, you must configure the Microsoft 365 Moodle plugins with a messaging endpoint.</span></span> <span data-ttu-id="f9e0f-237">Vous devez obtenir le point de terminaison à partir de votre bot dans Azure :</span><span class="sxs-lookup"><span data-stu-id="f9e0f-237">You must get the endpoint from your bot in Azure:</span></span>

1. <span data-ttu-id="f9e0f-238">Connectez-vous au [Portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f9e0f-238">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="f9e0f-239">Dans le volet gauche, sélectionnez les groupes de ressources et sélectionnez le groupe de ressources que vous avez utilisé ou créé lors du déploiement de votre bot. </span><span class="sxs-lookup"><span data-stu-id="f9e0f-239">In the left pane, select **Resource groups** and select the resource group you used or created, while deploying your bot.</span></span>

1. <span data-ttu-id="f9e0f-240">Sélectionnez **la ressource WebApp Bot** dans la liste des ressources du groupe.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-240">Select the **WebApp Bot** resource from the list of resources in the group.</span></span>

1. <span data-ttu-id="f9e0f-241">Copiez **le point de terminaison de messagerie à** partir de la section Vue **d’ensemble.**</span><span class="sxs-lookup"><span data-stu-id="f9e0f-241">Copy the **Messaging Endpoint** from the **Overview** section.</span></span>

1. <span data-ttu-id="f9e0f-242">Dans Le chat, ouvrez la page **d Paramètres** de votre Microsoft 365 Plug-ins De l’équipe.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-242">In Moodle, open the **Team Settings** page of your Microsoft 365 Moodle Plugins.</span></span>

1. <span data-ttu-id="f9e0f-243">Dans le **champ Point de terminaison du bot,** collez l’URL que vous avez copiée et modifiez le *mot messages* en *webhook.*</span><span class="sxs-lookup"><span data-stu-id="f9e0f-243">In the **Bot Endpoint** field paste the URL you just copied and change the word *messages* to *webhook*.</span></span> <span data-ttu-id="f9e0f-244">L’URL doit apparaître comme suit : `https://botname.azurewebsites.net/api/webhook`</span><span class="sxs-lookup"><span data-stu-id="f9e0f-244">The URL must appear as follows: `https://botname.azurewebsites.net/api/webhook`</span></span>

1. <span data-ttu-id="f9e0f-245">Sélectionnez **Enregistrer les modifications.**</span><span class="sxs-lookup"><span data-stu-id="f9e0f-245">Select **Save Changes**.</span></span>

1. <span data-ttu-id="f9e0f-246">Après avoir enregistrer les modifications, revenir à l’onglet **Paramètres** d’équipe, sélectionnez le bouton Télécharger le fichier manifeste, puis enregistrez le package de manifeste de l’application sur votre ordinateur pour une utilisation supplémentaire. </span><span class="sxs-lookup"><span data-stu-id="f9e0f-246">After saving the changes, go back to the **Team Settings** tab, select the **Download manifest file** button, and save the app manifest package to your computer for further use.</span></span>

## <a name="4-deploy-your-microsoft-teams-app"></a><span data-ttu-id="f9e0f-247">4. Déployer votre application Microsoft Teams de messagerie</span><span class="sxs-lookup"><span data-stu-id="f9e0f-247">4. Deploy your Microsoft Teams app</span></span>

<span data-ttu-id="f9e0f-248">Une fois que votre bot a été déployé sur Azure et configuré pour parler à votre serveur Dente, vous devez déployer votre application Microsoft Teams web.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-248">After your bot deployed to Azure and configured to talk to your Moodle server, you must deploy your Microsoft Teams app.</span></span> <span data-ttu-id="f9e0f-249">Pour ce faire, vous devez charger le fichier manifeste de l’application que vous avez téléchargé à partir de la page Microsoft 365 La page d’équipe Plug-ins De l’Paramètres à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-249">To do this you must load the app manifest file that you downloaded from the Microsoft 365 Moodle Plugins Team Settings page in the previous step.</span></span>

<span data-ttu-id="f9e0f-250">Avant d’installer l’application, vous devez veiller à activer les applications externes et à télécharger des applications.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-250">Before you install the app you must ensure to enable external apps and uploading of apps.</span></span> <span data-ttu-id="f9e0f-251">Pour plus d’informations, [voir Préparer Microsoft 365 client.](../concepts/build-and-test/prepare-your-o365-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="f9e0f-251">For more information, see [Prepare your Microsoft 365 tenant](../concepts/build-and-test/prepare-your-o365-tenant.md).</span></span> 

<span data-ttu-id="f9e0f-252">**Pour déployer votre application**</span><span class="sxs-lookup"><span data-stu-id="f9e0f-252">**To deploy your app**</span></span> 

1. <span data-ttu-id="f9e0f-253">Ouvrez **Microsoft Teams**.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-253">Open **Microsoft Teams**.</span></span> 

1. <span data-ttu-id="f9e0f-254">Sélectionnez **l’icône** Application dans la zone inférieure gauche de la barre de navigation.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-254">Select the **App** icon on the lower-left area of the navigation bar.</span></span>

1. <span data-ttu-id="f9e0f-255">Sélectionnez le **Télécharger un lien d’application** personnalisé dans la liste des options.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-255">Select the **Upload a custom app** link from the list of options.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f9e0f-256">Si vous êtes connecté en tant qu’administrateur général, vous devez avoir la possibilité de télécharger l’application dans le catalogue d’applications de votre organisation, sinon vous ne pouvez charger l’application que pour une équipe dont vous êtes membre.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-256">If you are logged in as a global administrator, you must have the option of uploading the app to your organization's app catalog, otherwise you can only load the app for a team in which you are a member.</span></span>

4. <span data-ttu-id="f9e0f-257">Sélectionnez `manifest.zip` le package que vous avez téléchargé précédemment et sélectionnez **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="f9e0f-257">Select the `manifest.zip` package you downloaded previously and select **Save**.</span></span> <span data-ttu-id="f9e0f-258">Si vous n’avez pas téléchargé le package de manifeste de l’application, vous pouvez le télécharger à partir de l’onglet **Paramètres** d’équipe de la page de configuration des plug-ins dans Lele.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-258">If you have not downloaded the app manifest package, you can download from the **Team Settings** tab of the plugins configuration page in Moodle.</span></span>

<span data-ttu-id="f9e0f-259">Maintenant que l’application est installée, vous pouvez ajouter l’onglet à n’importe quel canal à qui vous avez accès.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-259">Now that you have the app installed, you can add the tab to any channel that you have access to.</span></span> <span data-ttu-id="f9e0f-260">Pour ce faire, accédez au canal, sélectionnez le **symbole plus** (➕) et sélectionnez votre application dans la liste.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-260">To do so, navigate to the channel, select the **plus** (➕) symbol and select your app from the list.</span></span> <span data-ttu-id="f9e0f-261">Suivez les invites pour terminer l’ajout de l’onglet de cours DeNte à un canal.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-261">Follow the prompts to finish adding your Moodle course tab to a channel.</span></span>

## <a name="5-allow-automatic-creation-of-moodle-tabs-in-microsoft-teams"></a><span data-ttu-id="f9e0f-262">5. Autoriser la création automatique d’onglets Dentelé dans Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="f9e0f-262">5. Allow automatic creation of Moodle tabs in Microsoft Teams</span></span>

<span data-ttu-id="f9e0f-263">Bien que les onglets Dentelé soient créés manuellement dans Microsoft Teams, vous pouvez décider de les créer automatiquement lorsque des équipes sont créées à partir de la synchronisation de cours.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-263">Although the Moodle tabs are created manually in Microsoft Teams, you can decide to create them automatically when teams are created from course synchronization.</span></span> <span data-ttu-id="f9e0f-264">Pour ce faire, vous devez configurer l’ID de l’application Microsoft Teams téléchargée dans Sondèle.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-264">To do this, you must configure the ID of the uploaded Microsoft Teams app in Moodle.</span></span>

<span data-ttu-id="f9e0f-265">**Pour autoriser la création automatique d’onglets Dentelé**</span><span class="sxs-lookup"><span data-stu-id="f9e0f-265">**To allow automatic creation of Moodle tabs**</span></span>

1. <span data-ttu-id="f9e0f-266">Ouvrir Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-266">Open Microsoft Teams.</span></span>

1. <span data-ttu-id="f9e0f-267">Sélectionnez l’icône Applications dans la zone inférieure gauche de la barre de navigation.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-267">Select the Apps icon from the lower-left area of the navigation bar.</span></span>

1. <span data-ttu-id="f9e0f-268">Recherchez l’application **Dentier** téléchargée > sélectionnez **l’icône d’options** > sélectionner le lien **copier.**</span><span class="sxs-lookup"><span data-stu-id="f9e0f-268">Locate the uploaded **Moodle app** > select the **options** icon > select **copy link**.</span></span>

1. <span data-ttu-id="f9e0f-269">Dans un éditeur de texte, collez le contenu copié.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-269">In a text editor, paste the copied content.</span></span> <span data-ttu-id="f9e0f-270">Il doit contenir une URL telle que ht&#8203;tps://teams.microsoft.com/l/app/00112233-4455-6677-8899-aabbccddeeff.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-270">It must contain a URL such as ht&#8203;tps://teams.microsoft.com/l/app/00112233-4455-6677-8899-aabbccddeeff.</span></span> <span data-ttu-id="f9e0f-271">Copiez la dernière partie de l’URL, par exemple, qui est l’ID de `00112233-4455-6677-8899-aabbccddeeff` l’Microsoft Teams’application.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-271">Copy the last part of the URL, such as  `00112233-4455-6677-8899-aabbccddeeff`, which is the ID of the Microsoft Teams app.</span></span>

1. <span data-ttu-id="f9e0f-272">Dans L’espace de commentaires, ouvrez **l Teams a tabulation de l’application Enfichables à** partir de Microsoft 365 page de configuration des plug-ins Enfichables Enfichables.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-272">In Moodle, open the **Teams Moodle app** tab from your Microsoft 365 Moodle Plugins configuration page.</span></span>

1. <span data-ttu-id="f9e0f-273">Collez l’ID de l’application Microsoft Teams dans le champ D’ID de l’application Et enregistrez les modifications.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-273">Paste the ID of the Microsoft Teams app into the Moodle app ID field, and save changes.</span></span>

<span data-ttu-id="f9e0f-274">Lors de la synchronisation d’un cours DNS, Microsoft Teams installe automatiquement l’application Dente dans l’équipe, crée un onglet Dentelé dans le canal Général de Teams et le configure pour qu’il contienne la page de cours pour le cours À partir duquel il est synchronisé.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-274">When a Moodle course is synced, Microsoft Teams automatically installs the Moodle app in the team, creates a Moodle tab in the General channel of Teams, and configures it to contain the course page for the Moodle course from which it is synced.</span></span> <span data-ttu-id="f9e0f-275">Vous pouvez maintenant commencer à utiliser vos cours De la part de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-275">You can now start working with your Moodle courses directly from Microsoft Teams.</span></span>

> [!NOTE]
> <span data-ttu-id="f9e0f-276">Pour partager des demandes de fonctionnalités ou des commentaires avec nous, visitez notre [page User Voice.](https://microsoftteams.uservoice.com/forums/916759-moodle)</span><span class="sxs-lookup"><span data-stu-id="f9e0f-276">To share any feature requests or feedback with us, visit our [User Voice page](https://microsoftteams.uservoice.com/forums/916759-moodle).</span></span>

## <a name="see-also"></a><span data-ttu-id="f9e0f-277">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="f9e0f-277">See also</span></span>

- [<span data-ttu-id="f9e0f-278">Intégrer les applications Web</span><span class="sxs-lookup"><span data-stu-id="f9e0f-278">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)
- [<span data-ttu-id="f9e0f-279">Moodle</span><span class="sxs-lookup"><span data-stu-id="f9e0f-279">Moodle</span></span>](https://moodle.org/)
- <span data-ttu-id="f9e0f-280">[Documentation en toute fin](https://docs.moodle.org/34/en/Installing_plugins)de vie.</span><span class="sxs-lookup"><span data-stu-id="f9e0f-280">[Moodle documentation](https://docs.moodle.org/34/en/Installing_plugins).</span></span>

