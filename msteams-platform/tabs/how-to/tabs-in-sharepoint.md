---
title: Ajouter l'onglet Teams à SharePoint
author: laujan
description: Comment déployer votre onglet Teams existant sur SharePoint en tant que partie Web De l'infrastructure SharePoint.
keywords: teams tabs sharepoint framework development
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: a2ea6c470f094a9d7b8617a210559e911f5f81c9
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058480"
---
# <a name="add-teams-tab-to-sharepoint"></a><span data-ttu-id="cff1f-104">Ajouter l'onglet Teams à SharePoint</span><span class="sxs-lookup"><span data-stu-id="cff1f-104">Add Teams tab to SharePoint</span></span> 

<span data-ttu-id="cff1f-105">Vous pouvez obtenir une expérience d'intégration enrichie entre Microsoft Teams et SharePoint en ajoutant un onglet Microsoft Teams dans SharePoint en tant que partie Web SPFx.</span><span class="sxs-lookup"><span data-stu-id="cff1f-105">You can get a rich integration experience between Microsoft Teams and SharePoint by adding a Microsoft Teams tab in SharePoint as an SPFx web part.</span></span> <span data-ttu-id="cff1f-106">Ce document vous guide sur la façon de prendre un onglet à partir d'un exemple d'application Microsoft Teams et de l'utiliser dans SharePoint.</span><span class="sxs-lookup"><span data-stu-id="cff1f-106">This document guides you on how you to take a tab from a Microsoft Teams sample app and use it in SharePoint.</span></span> 

## <a name="rich-integration-between-teams-and-sharepoint"></a><span data-ttu-id="cff1f-107">Intégration enrichie entre Teams et SharePoint</span><span class="sxs-lookup"><span data-stu-id="cff1f-107">Rich integration between Teams and SharePoint</span></span>

<span data-ttu-id="cff1f-108">Avec la version de novembre de Teams et SharePoint Framework v.1.7, les développeurs ont deux fonctionnalités puissantes :</span><span class="sxs-lookup"><span data-stu-id="cff1f-108">With the November release of Teams and SharePoint Framework v.1.7, developers have two powerful capabilities:</span></span>

<ul  class="panelContent cardsC">
<li>
    <a href="#introduction">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img src="~/assets/images/tabs/tabs-in-sharepoint/image084.png" alt="tab-in-sharepoint view"/>
                        </div>
                    </div>
                    <div class="cardText">
                        <h3><span data-ttu-id="cff1f-109">Onglets Teams dans SharePoint</span><span class="sxs-lookup"><span data-stu-id="cff1f-109">Teams Tabs in SharePoint</span></span></h3>
                        <p><span data-ttu-id="cff1f-110">Créez des expériences d'application enrichies dans SharePoint en apportant votre application Teams dans SharePoint (cet article).</span><span class="sxs-lookup"><span data-stu-id="cff1f-110">Create rich app experiences in SharePoint by bringing your Teams app into Sharepoint (this article).</span></span></p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li>
    <a href="https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img src="~/assets/images/tabs/tabs-in-sharepoint/SharePoint-web-part-exposed-as-a-Tab-in-Microsoft-Teams.png" alt="web-part-exposed-as-a-tab" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3><span data-ttu-id="cff1f-111">SharePoint Framework dans Teams</span><span class="sxs-lookup"><span data-stu-id="cff1f-111">SharePoint Framework in Teams</span></span></h3>
                        <p><span data-ttu-id="cff1f-112">Apportez vos composants Web Parts SharePoint à Teams et laissez SharePoint gérer l'hébergement pour vous.</span><span class="sxs-lookup"><span data-stu-id="cff1f-112">Bring your SharePoint web parts to Teams and let SharePoint manage the hosting for you.</span></span></p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

### <a name="teams-tabs-in-sharepoint"></a><span data-ttu-id="cff1f-113">Onglets Teams dans SharePoint</span><span class="sxs-lookup"><span data-stu-id="cff1f-113">Teams tabs in SharePoint</span></span>

<span data-ttu-id="cff1f-114">Avec SharePoint Framework v.1.7, vous pouvez héberger vos onglets Teams dans SharePoint.</span><span class="sxs-lookup"><span data-stu-id="cff1f-114">With SharePoint Framework v.1.7, you can host your Teams tabs in SharePoint.</span></span> <span data-ttu-id="cff1f-115">Comme les onglets hébergés dans SharePoint obtiennent une expérience de **page** complète similaire, en exposant toutes les fonctionnalités des onglets Teams tout en conservant le contexte et la familiarité d'un site SharePoint.</span><span class="sxs-lookup"><span data-stu-id="cff1f-115">As tabs hosted in SharePoint get a similar **full page** experience, exposing all the features of Teams tabs while retaining the context and familiarity of a SharePoint site.</span></span>

### <a name="sharepoint-framework-in-teams"></a><span data-ttu-id="cff1f-116">SharePoint Framework dans Teams</span><span class="sxs-lookup"><span data-stu-id="cff1f-116">SharePoint Framework in Teams</span></span>

<span data-ttu-id="cff1f-117">Vous pouvez également implémenter vos onglets Microsoft Teams à l'aide de SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="cff1f-117">You can also implement your Microsoft Teams tabs using SharePoint Framework.</span></span> <span data-ttu-id="cff1f-118">Les composants WebPoint Framework sont hébergés dans SharePoint sans avoir besoin de services externes, tels qu'Azure.</span><span class="sxs-lookup"><span data-stu-id="cff1f-118">SharePoint Framework web parts are hosted within SharePoint without any need for external services, such as Azure.</span></span> <span data-ttu-id="cff1f-119">Pour les développeurs SharePoint, cela simplifie considérablement le processus de développement des onglets Teams.</span><span class="sxs-lookup"><span data-stu-id="cff1f-119">For SharePoint developers, this significantly simplifies the development process for Teams tabs.</span></span> <span data-ttu-id="cff1f-120">Pour plus d'informations sur SharePoint Framework dans Teams, voir comment utiliser [SharePoint Framework dans Teams.](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)</span><span class="sxs-lookup"><span data-stu-id="cff1f-120">For more information on SharePoint Framework in Teams, see [how to use the SharePoint Framework in Teams.](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)</span></span>

## <a name="introduction"></a><span data-ttu-id="cff1f-121">Introduction</span><span class="sxs-lookup"><span data-stu-id="cff1f-121">Introduction</span></span>

<span data-ttu-id="cff1f-122">L'onglet utilisé ici est déjà hébergé sur Azure, pour se concentrer sur le travail d'intégration requis.</span><span class="sxs-lookup"><span data-stu-id="cff1f-122">The tab used here is already hosted on Azure, to focus on the required integration work.</span></span>

<span data-ttu-id="cff1f-123">L'exemple d'application utilisé est une application de gestion des talents.</span><span class="sxs-lookup"><span data-stu-id="cff1f-123">The sample app that is being used is a Talent Management application.</span></span> <span data-ttu-id="cff1f-124">Il gère le processus d'embauche des candidats pour les postes ouverts dans une équipe.</span><span class="sxs-lookup"><span data-stu-id="cff1f-124">It manages the hiring process of candidates for open positions in a team.</span></span> <span data-ttu-id="cff1f-125">Créez un exemple d'application Teams et chargez-la dans Teams.</span><span class="sxs-lookup"><span data-stu-id="cff1f-125">Build a sample Teams app and load it into Teams.</span></span> <span data-ttu-id="cff1f-126">Ne créez pas d'application de gestion des talents réelle.</span><span class="sxs-lookup"><span data-stu-id="cff1f-126">Do not create a real talent management application.</span></span>

### <a name="benefits-of-this-approach"></a><span data-ttu-id="cff1f-127">Avantages de cette approche</span><span class="sxs-lookup"><span data-stu-id="cff1f-127">Benefits of this approach</span></span>

* <span data-ttu-id="cff1f-128">Atteindre les utilisateurs SharePoint avec votre onglet Teams existant.</span><span class="sxs-lookup"><span data-stu-id="cff1f-128">Reach SharePoint users with your existing Teams tab.</span></span>
* <span data-ttu-id="cff1f-129">Téléchargez votre manifeste d'application directement dans votre catalogue d'applications SharePoint.</span><span class="sxs-lookup"><span data-stu-id="cff1f-129">Upload your app manifest directly to your SharePoint app catalog.</span></span> <span data-ttu-id="cff1f-130">[Les packages d'application Teams](~/concepts/build-and-test/apps-package.md) sont désormais pris en charge par SharePoint.</span><span class="sxs-lookup"><span data-stu-id="cff1f-130">[Teams application packages](~/concepts/build-and-test/apps-package.md) are now supported by SharePoint.</span></span>
* <span data-ttu-id="cff1f-131">Les utilisateurs configurent l'onglet d'une page comme n'importe quel autre élément Web Part SharePoint.</span><span class="sxs-lookup"><span data-stu-id="cff1f-131">The users configure the tab on a page just like any other SharePoint web part.</span></span>
* <span data-ttu-id="cff1f-132">Votre onglet peut accéder à [son contexte](~/tabs/how-to/access-teams-context.md) de la même manière que lors de son exécution dans Teams.</span><span class="sxs-lookup"><span data-stu-id="cff1f-132">Your tab can access its [context](~/tabs/how-to/access-teams-context.md) sameas it can, when running inside Teams.</span></span>

<span data-ttu-id="cff1f-133">**Pour ajouter l'onglet Teams à SharePoint**</span><span class="sxs-lookup"><span data-stu-id="cff1f-133">**To add Teams tab to SharePoint**</span></span>

<span data-ttu-id="cff1f-134">Pour ajouter l'onglet Teams à SharePoint, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="cff1f-134">Perform the following steps to add Teams tab to SharePoint:</span></span>

## <a name="1-test-the-sample-app"></a><span data-ttu-id="cff1f-135">1. Tester l'exemple d'application</span><span class="sxs-lookup"><span data-stu-id="cff1f-135">1. Test the sample app</span></span>

<span data-ttu-id="cff1f-136">Téléchargez [l'exemple de manifeste d'application.](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip)</span><span class="sxs-lookup"><span data-stu-id="cff1f-136">Download the [sample app manifest](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip).</span></span>

1. <span data-ttu-id="cff1f-137">Ouvrir Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="cff1f-137">Open Microsoft Teams.</span></span>
1. <span data-ttu-id="cff1f-138">Sélectionnez **l'icône de l'Appstore** en bas à gauche de l'onglet latéral.</span><span class="sxs-lookup"><span data-stu-id="cff1f-138">Select the **Appstore** icon at the lower left of side tab.</span></span>
1. <span data-ttu-id="cff1f-139">Sélectionnez **Télécharger une application personnalisée en** bas à gauche.</span><span class="sxs-lookup"><span data-stu-id="cff1f-139">Select **Upload a custom app** at the lower left.</span></span> <span data-ttu-id="cff1f-140">L'image suivante affiche l'écran correspondant :</span><span class="sxs-lookup"><span data-stu-id="cff1f-140">The following image displays the corresponding screen:</span></span>  

    ![télécharger une application personnalisée](~/assets/images/tabs/tabs-in-sharepoint/upload-custom-app.png)

1. <span data-ttu-id="cff1f-142">Le fichier à télécharger se trouve dans votre **dossier Téléchargements.**</span><span class="sxs-lookup"><span data-stu-id="cff1f-142">The file to upload is located in your **Downloads** folder.</span></span> <span data-ttu-id="cff1f-143">Elle est appelée TalentMgmt-Azure.zip.</span><span class="sxs-lookup"><span data-stu-id="cff1f-143">It is called TalentMgmt-Azure.zip.</span></span> <span data-ttu-id="cff1f-144">L'image suivante affiche l'écran correspondant :</span><span class="sxs-lookup"><span data-stu-id="cff1f-144">The following image displays the corresponding screen:</span></span>
 
    ![TalentMgmt dans Azure](~/assets/images/tabs/tabs-in-sharepoint/talentmgmt-azure.png)

1. <span data-ttu-id="cff1f-146">Vous pouvez voir l'écran d'installation ou de consentement de l'application de gestion des talents.</span><span class="sxs-lookup"><span data-stu-id="cff1f-146">You can see the install or consent screen for the talent management app.</span></span> <span data-ttu-id="cff1f-147">Sélectionnez l'équipe que vous souhaitez installer.</span><span class="sxs-lookup"><span data-stu-id="cff1f-147">Select the team you want to install.</span></span> 
1. <span data-ttu-id="cff1f-148">Sélectionnez **l'installation** et commencez à tester l'application.</span><span class="sxs-lookup"><span data-stu-id="cff1f-148">Select the **Install** and start experimenting with the app.</span></span>

## <a name="2-use-teams-tab-in-sharepoint"></a><span data-ttu-id="cff1f-149">2. Utiliser l'onglet Teams dans SharePoint</span><span class="sxs-lookup"><span data-stu-id="cff1f-149">2. Use Teams tab in SharePoint</span></span>

1. <span data-ttu-id="cff1f-150">Téléchargez et déployez votre package d'application Teams dans votre catalogue d'applications SharePoint en visitant `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` .</span><span class="sxs-lookup"><span data-stu-id="cff1f-150">Upload and deploy your Teams app package to your SharePoint App Catalog by visiting `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`.</span></span> <span data-ttu-id="cff1f-151">Par exemple, `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`.</span><span class="sxs-lookup"><span data-stu-id="cff1f-151">For example, `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`.</span></span>

1. <span data-ttu-id="cff1f-152">Lorsque vous y sont invités, **activez Rendre cette solution disponible pour tous les sites de l'organisation.**</span><span class="sxs-lookup"><span data-stu-id="cff1f-152">When prompted, enable **Make this solution available to all sites in the organization**.</span></span>
<span data-ttu-id="cff1f-153">L'image suivante affiche l'écran correspondant :</span><span class="sxs-lookup"><span data-stu-id="cff1f-153">The following image displays the corresponding screen:</span></span>

   ![Onglets en vue SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image065.png)

1. <span data-ttu-id="cff1f-155">Dans votre site, créez une page en sélectionnant le bouton d'engrenage en haut à droite, puis **sélectionnez Ajouter une page.**</span><span class="sxs-lookup"><span data-stu-id="cff1f-155">In your site, create a new page by selecting the gear button at the upper right and then  select **Add a page**.</span></span>
<span data-ttu-id="cff1f-156">L'image suivante affiche l'écran correspondant :</span><span class="sxs-lookup"><span data-stu-id="cff1f-156">The following image displays the corresponding screen:</span></span>

   ![Vue SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image066.png)

1. <span data-ttu-id="cff1f-158">Vous pouvez voir l'expérience de authoring des pages SharePoint.</span><span class="sxs-lookup"><span data-stu-id="cff1f-158">You can see the SharePoint pages authoring experience.</span></span> <span data-ttu-id="cff1f-159">Nommez votre page en **tant qu'onglet Mes équipes.**</span><span class="sxs-lookup"><span data-stu-id="cff1f-159">Name your page as **My Teams Tab**.</span></span>

1. <span data-ttu-id="cff1f-160">Ouvrez la boîte à outils du volet Web En appuyant sur le bouton, puis sélectionnez l'onglet `+` Teams nommé **Contoso HR**.</span><span class="sxs-lookup"><span data-stu-id="cff1f-160">Open the web part toolbox by pressing the `+` button, and select your Teams Tab, named **Contoso HR**.</span></span> <span data-ttu-id="cff1f-161">Les composants Web Parts sont triés par ordre alphabétique.</span><span class="sxs-lookup"><span data-stu-id="cff1f-161">Web parts are sorted alphabetically.</span></span> <span data-ttu-id="cff1f-162">S'il s'agit d'une longue liste, vous pouvez utiliser la barre de recherche pour la trouver.</span><span class="sxs-lookup"><span data-stu-id="cff1f-162">If it is a long list, you can use the search bar to find it.</span></span> <span data-ttu-id="cff1f-163">Cela crée un élément Web Part dans le canevas qui contient votre onglet Teams. L'image suivante affiche l'affichage Onglet :</span><span class="sxs-lookup"><span data-stu-id="cff1f-163">This creates a web part in the canvas that contains your Teams tab. The following image displays the tab view:</span></span>

   ![Affichage Onglet](~/assets/images/tabs/tabs-in-sharepoint/image071.png)

1. <span data-ttu-id="cff1f-165">Appuyez sur **le** bouton Publier après avoir terminé la modification.</span><span class="sxs-lookup"><span data-stu-id="cff1f-165">Press the **Publish** button after you finish  editing.</span></span>

1. <span data-ttu-id="cff1f-166">Sélectionnez **Ajouter une page à la navigation** pour avoir une référence rapide à votre page dans la barre de navigation de gauche.</span><span class="sxs-lookup"><span data-stu-id="cff1f-166">Select **Add page to navigation** to have a quick reference to your page in the left navigation bar.</span></span> <span data-ttu-id="cff1f-167">L'image suivante affiche l'onglet dans SharePoint :</span><span class="sxs-lookup"><span data-stu-id="cff1f-167">The following image displays the tab in Sharepoint:</span></span> 

   ![Onglet dans l'image Sharepoint](~/assets/images/tabs/tabs-in-sharepoint/image073.png)

## <a name="3-explore-app-pages-in-sharepoint"></a><span data-ttu-id="cff1f-169">3. Explorer les pages d'application dans SharePoint</span><span class="sxs-lookup"><span data-stu-id="cff1f-169">3. Explore App Pages in SharePoint</span></span>

<span data-ttu-id="cff1f-170">Une fois votre page publiée, vous pouvez explorer comment transformer votre application Teams en une expérience plus [complète dans SharePoint.](/sharepoint/dev/spfx/web-parts/single-part-app-pages)</span><span class="sxs-lookup"><span data-stu-id="cff1f-170">After your page is published, you can explore [turning your Teams app into a more complete experience inside SharePoint](/sharepoint/dev/spfx/web-parts/single-part-app-pages).</span></span> <span data-ttu-id="cff1f-171">Cela convertit la page actuelle en page d'application, affichant la mise en page SharePoint normale avec une expérience de page complète pour l'onglet Teams.</span><span class="sxs-lookup"><span data-stu-id="cff1f-171">This converts the current page into an App Page, showing the normal SharePoint page layout with a full page experience for the Teams tab.</span></span> 

<span data-ttu-id="cff1f-172">L'image suivante affiche l'expérience complète de l'application Teams dans Sharepoint : ![ Image des onglets dans Sharepoint](~/assets/images/tabs/tabs-in-sharepoint/image085.png)</span><span class="sxs-lookup"><span data-stu-id="cff1f-172">The following image displays the complete experience of Teams app in Sharepoint: ![Image of Tabs in Sharepoint](~/assets/images/tabs/tabs-in-sharepoint/image085.png)</span></span>

## <a name="code-sample"></a><span data-ttu-id="cff1f-173">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="cff1f-173">Code sample</span></span>
| <span data-ttu-id="cff1f-174">**Exemple de nom**</span><span class="sxs-lookup"><span data-stu-id="cff1f-174">**Sample name**</span></span> | <span data-ttu-id="cff1f-175">**Description**</span><span class="sxs-lookup"><span data-stu-id="cff1f-175">**Description**</span></span> | <span data-ttu-id="cff1f-176">**SPFx**</span><span class="sxs-lookup"><span data-stu-id="cff1f-176">**SPFx**</span></span> |
|-----------------|-----------------|----------|
| <span data-ttu-id="cff1f-177">Partie Web SPFx</span><span class="sxs-lookup"><span data-stu-id="cff1f-177">SPFx web part</span></span> | <span data-ttu-id="cff1f-178">Exemples de partie Web SPFx pour les onglets, les canaux et les groupes.</span><span class="sxs-lookup"><span data-stu-id="cff1f-178">SPFx web part samples for tabs, channels, and groups.</span></span> | [<span data-ttu-id="cff1f-179">View</span><span class="sxs-lookup"><span data-stu-id="cff1f-179">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group/spfx)

## <a name="see-also"></a><span data-ttu-id="cff1f-180">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="cff1f-180">See also</span></span>

- [<span data-ttu-id="cff1f-181">Création d’un onglet Microsoft Teams à l’aide de SharePoint Framework - Didacticiel</span><span class="sxs-lookup"><span data-stu-id="cff1f-181">Building Microsoft Teams tab using SharePoint Framework - Tutorial</span></span>](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)

- [<span data-ttu-id="cff1f-182">Utilisation des pages d’application à composant unique dans SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="cff1f-182">Using single part app pages in SharePoint Online</span></span>](/sharepoint/dev/spfx/web-parts/single-part-app-pages)

- [<span data-ttu-id="cff1f-183">Intégrer les applications Web</span><span class="sxs-lookup"><span data-stu-id="cff1f-183">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)
