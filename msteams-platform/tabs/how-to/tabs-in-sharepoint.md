---
title: Ajouter l'onglet Teams à SharePoint
author: laujan
description: Comment déployer votre onglet Teams existant SharePoint en tant que SharePoint Framework Web Part.
keywords: teams tabs sharepoint framework development
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: c6c5668c0d937e0512d8a6dba366f7fd545b8a96
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630410"
---
# <a name="add-teams-tab-to-sharepoint"></a><span data-ttu-id="be05b-104">Ajouter l'onglet Teams à SharePoint</span><span class="sxs-lookup"><span data-stu-id="be05b-104">Add Teams tab to SharePoint</span></span> 

<span data-ttu-id="be05b-105">Vous pouvez obtenir une expérience d’intégration riche entre Microsoft Teams et SharePoint en ajoutant un onglet Microsoft Teams dans SharePoint en tant que SPFx web.</span><span class="sxs-lookup"><span data-stu-id="be05b-105">You can get a rich integration experience between Microsoft Teams and SharePoint by adding a Microsoft Teams tab in SharePoint as an SPFx web part.</span></span> <span data-ttu-id="be05b-106">Ce document vous guide sur la façon dont vous pouvez prendre un onglet à partir d’un exemple d Microsoft Teams appl’application et l’utiliser dans SharePoint.</span><span class="sxs-lookup"><span data-stu-id="be05b-106">This document guides you on how you to take a tab from a Microsoft Teams sample app and use it in SharePoint.</span></span> 

## <a name="rich-integration-between-teams-and-sharepoint"></a><span data-ttu-id="be05b-107">Intégration enrichie entre Teams et SharePoint</span><span class="sxs-lookup"><span data-stu-id="be05b-107">Rich integration between Teams and SharePoint</span></span>

<span data-ttu-id="be05b-108">Avec la version de novembre Teams et SharePoint Framework version 1.7, les développeurs ont deux fonctionnalités puissantes :</span><span class="sxs-lookup"><span data-stu-id="be05b-108">With the November release of Teams and SharePoint Framework v.1.7, developers have two powerful capabilities:</span></span>

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
                        <h3><span data-ttu-id="be05b-109">Teams Onglets dans SharePoint</span><span class="sxs-lookup"><span data-stu-id="be05b-109">Teams Tabs in SharePoint</span></span></h3>
                        <p><span data-ttu-id="be05b-110">Créez des expériences d’application enrichies SharePoint en apportant votre application Teams dans SharePoint (cet article).</span><span class="sxs-lookup"><span data-stu-id="be05b-110">Create rich app experiences in SharePoint by bringing your Teams app into Sharepoint (this article).</span></span></p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li>
    <a href="/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img src="~/assets/images/tabs/tabs-in-sharepoint/SharePoint-web-part-exposed-as-a-Tab-in-Microsoft-Teams.png" alt="web-part-exposed-as-a-tab" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3><span data-ttu-id="be05b-111">SharePoint Framework dans Teams</span><span class="sxs-lookup"><span data-stu-id="be05b-111">SharePoint Framework in Teams</span></span></h3>
                        <p><span data-ttu-id="be05b-112">Faites en SharePoint vos composants Web Teams et laissez SharePoint gérer l’hébergement pour vous.</span><span class="sxs-lookup"><span data-stu-id="be05b-112">Bring your SharePoint web parts to Teams and let SharePoint manage the hosting for you.</span></span></p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

### <a name="teams-tabs-in-sharepoint"></a><span data-ttu-id="be05b-113">Teams onglets dans SharePoint</span><span class="sxs-lookup"><span data-stu-id="be05b-113">Teams tabs in SharePoint</span></span>

<span data-ttu-id="be05b-114">Avec SharePoint Framework v.1.7, vous pouvez héberger vos onglets Teams dans SharePoint.</span><span class="sxs-lookup"><span data-stu-id="be05b-114">With SharePoint Framework v.1.7, you can host your Teams tabs in SharePoint.</span></span> <span data-ttu-id="be05b-115">Comme les onglets hébergés dans SharePoint offrent une expérience de **page** complète similaire, en exposant toutes les fonctionnalités des onglets Teams tout en conservant le contexte et les caractéristiques d’un site SharePoint web.</span><span class="sxs-lookup"><span data-stu-id="be05b-115">As tabs hosted in SharePoint get a similar **full page** experience, exposing all the features of Teams tabs while retaining the context and familiarity of a SharePoint site.</span></span>

### <a name="sharepoint-framework-in-teams"></a><span data-ttu-id="be05b-116">SharePoint Framework dans Teams</span><span class="sxs-lookup"><span data-stu-id="be05b-116">SharePoint Framework in Teams</span></span>

<span data-ttu-id="be05b-117">Vous pouvez également implémenter vos onglets Microsoft Teams à l’aide SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="be05b-117">You can also implement your Microsoft Teams tabs using SharePoint Framework.</span></span> <span data-ttu-id="be05b-118">SharePoint Framework web sont hébergés dans SharePoint sans avoir besoin de services externes, tels qu’Azure.</span><span class="sxs-lookup"><span data-stu-id="be05b-118">SharePoint Framework web parts are hosted within SharePoint without any need for external services, such as Azure.</span></span> <span data-ttu-id="be05b-119">Pour SharePoint développeurs, cela simplifie considérablement le processus de développement pour Teams onglets.</span><span class="sxs-lookup"><span data-stu-id="be05b-119">For SharePoint developers, this significantly simplifies the development process for Teams tabs.</span></span> <span data-ttu-id="be05b-120">Pour plus d’informations SharePoint Framework la Teams, voir comment utiliser les SharePoint Framework [dans Teams.](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)</span><span class="sxs-lookup"><span data-stu-id="be05b-120">For more information on SharePoint Framework in Teams, see [how to use the SharePoint Framework in Teams.](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)</span></span>

## <a name="introduction"></a><span data-ttu-id="be05b-121">Introduction</span><span class="sxs-lookup"><span data-stu-id="be05b-121">Introduction</span></span>

<span data-ttu-id="be05b-122">L’onglet utilisé ici est déjà hébergé sur Azure, pour se concentrer sur le travail d’intégration requis.</span><span class="sxs-lookup"><span data-stu-id="be05b-122">The tab used here is already hosted on Azure, to focus on the required integration work.</span></span>

<span data-ttu-id="be05b-123">L’exemple d’application utilisé est une application de gestion des talents.</span><span class="sxs-lookup"><span data-stu-id="be05b-123">The sample app that is being used is a Talent Management application.</span></span> <span data-ttu-id="be05b-124">Il gère le processus d’embauche des candidats pour les postes ouverts dans une équipe.</span><span class="sxs-lookup"><span data-stu-id="be05b-124">It manages the hiring process of candidates for open positions in a team.</span></span> <span data-ttu-id="be05b-125">Créez un exemple Teams’application et chargez-la dans Teams.</span><span class="sxs-lookup"><span data-stu-id="be05b-125">Build a sample Teams app and load it into Teams.</span></span> <span data-ttu-id="be05b-126">Ne créez pas d’application de gestion des talents réelle.</span><span class="sxs-lookup"><span data-stu-id="be05b-126">Do not create a real talent management application.</span></span>

### <a name="benefits-of-this-approach"></a><span data-ttu-id="be05b-127">Avantages de cette approche</span><span class="sxs-lookup"><span data-stu-id="be05b-127">Benefits of this approach</span></span>

* <span data-ttu-id="be05b-128">Touchez SharePoint utilisateurs avec votre onglet Teams existant.</span><span class="sxs-lookup"><span data-stu-id="be05b-128">Reach SharePoint users with your existing Teams tab.</span></span>
* <span data-ttu-id="be05b-129">Télécharger votre manifeste d’application directement dans SharePoint catalogue d’applications.</span><span class="sxs-lookup"><span data-stu-id="be05b-129">Upload your app manifest directly to your SharePoint app catalog.</span></span> <span data-ttu-id="be05b-130">[Teams packages d’application](~/concepts/build-and-test/apps-package.md) sont désormais pris en charge par SharePoint.</span><span class="sxs-lookup"><span data-stu-id="be05b-130">[Teams application packages](~/concepts/build-and-test/apps-package.md) are now supported by SharePoint.</span></span>
* <span data-ttu-id="be05b-131">Les utilisateurs configurent l’onglet sur une page comme n’importe quel autre SharePoint web.</span><span class="sxs-lookup"><span data-stu-id="be05b-131">The users configure the tab on a page just like any other SharePoint web part.</span></span>
* <span data-ttu-id="be05b-132">Votre onglet peut accéder à [son contexte](~/tabs/how-to/access-teams-context.md) de la même manière qu’il le peut, lors de l’exécution à l’Teams.</span><span class="sxs-lookup"><span data-stu-id="be05b-132">Your tab can access its [context](~/tabs/how-to/access-teams-context.md) sameas it can, when running inside Teams.</span></span>

<span data-ttu-id="be05b-133">**Pour ajouter Teams onglet à SharePoint**</span><span class="sxs-lookup"><span data-stu-id="be05b-133">**To add Teams tab to SharePoint**</span></span>

<span data-ttu-id="be05b-134">Effectuez les étapes suivantes pour ajouter Teams onglet à SharePoint :</span><span class="sxs-lookup"><span data-stu-id="be05b-134">Perform the following steps to add Teams tab to SharePoint:</span></span>

## <a name="1-test-the-sample-app"></a><span data-ttu-id="be05b-135">1. Tester l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="be05b-135">1. Test the sample app</span></span>

<span data-ttu-id="be05b-136">Téléchargez [l’exemple de manifeste d’application.](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip)</span><span class="sxs-lookup"><span data-stu-id="be05b-136">Download the [sample app manifest](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip).</span></span>

1. <span data-ttu-id="be05b-137">Ouvrir Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="be05b-137">Open Microsoft Teams.</span></span>
1. <span data-ttu-id="be05b-138">Sélectionnez **l’icône de l’Appstore** en bas à gauche de l’onglet latéral.</span><span class="sxs-lookup"><span data-stu-id="be05b-138">Select the **Appstore** icon at the lower left of side tab.</span></span>
1. <span data-ttu-id="be05b-139">Sélectionnez **Télécharger une application personnalisée** en bas à gauche.</span><span class="sxs-lookup"><span data-stu-id="be05b-139">Select **Upload a custom app** at the lower left.</span></span> <span data-ttu-id="be05b-140">L’image suivante affiche l’écran correspondant :</span><span class="sxs-lookup"><span data-stu-id="be05b-140">The following image displays the corresponding screen:</span></span>  

    ![télécharger une application personnalisée](~/assets/images/tabs/tabs-in-sharepoint/upload-custom-app.png)

1. <span data-ttu-id="be05b-142">Le fichier à télécharger se trouve dans votre **dossier Téléchargements.**</span><span class="sxs-lookup"><span data-stu-id="be05b-142">The file to upload is located in your **Downloads** folder.</span></span> <span data-ttu-id="be05b-143">Elle est appelée TalentMgmt-Azure.zip.</span><span class="sxs-lookup"><span data-stu-id="be05b-143">It is called TalentMgmt-Azure.zip.</span></span> <span data-ttu-id="be05b-144">L’image suivante affiche l’écran correspondant :</span><span class="sxs-lookup"><span data-stu-id="be05b-144">The following image displays the corresponding screen:</span></span>
 
    ![TalentMgmt dans Azure](~/assets/images/tabs/tabs-in-sharepoint/talentmgmt-azure.png)

1. <span data-ttu-id="be05b-146">Vous pouvez voir l’écran d’installation ou de consentement de l’application de gestion des talents.</span><span class="sxs-lookup"><span data-stu-id="be05b-146">You can see the install or consent screen for the talent management app.</span></span> <span data-ttu-id="be05b-147">Sélectionnez l’équipe que vous souhaitez installer.</span><span class="sxs-lookup"><span data-stu-id="be05b-147">Select the team you want to install.</span></span> 
1. <span data-ttu-id="be05b-148">Sélectionnez **l’installation** et commencez à tester l’application.</span><span class="sxs-lookup"><span data-stu-id="be05b-148">Select the **Install** and start experimenting with the app.</span></span>

## <a name="2-use-teams-tab-in-sharepoint"></a><span data-ttu-id="be05b-149">2. Utilisez l’Teams dans SharePoint</span><span class="sxs-lookup"><span data-stu-id="be05b-149">2. Use Teams tab in SharePoint</span></span>

1. <span data-ttu-id="be05b-150">Télécharger et déployez votre package Teams’application dans votre catalogue SharePoint’applications en visitant `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` .</span><span class="sxs-lookup"><span data-stu-id="be05b-150">Upload and deploy your Teams app package to your SharePoint App Catalog by visiting `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`.</span></span> <span data-ttu-id="be05b-151">Par exemple, `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`.</span><span class="sxs-lookup"><span data-stu-id="be05b-151">For example, `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`.</span></span>

1. <span data-ttu-id="be05b-152">Lorsque vous y sont invités, **activez Rendre cette solution disponible pour tous les sites de l’organisation.**</span><span class="sxs-lookup"><span data-stu-id="be05b-152">When prompted, enable **Make this solution available to all sites in the organization**.</span></span>
<span data-ttu-id="be05b-153">L’image suivante affiche l’écran correspondant :</span><span class="sxs-lookup"><span data-stu-id="be05b-153">The following image displays the corresponding screen:</span></span>

   ![Onglets en vue SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image065.png)

1. <span data-ttu-id="be05b-155">Dans votre site, créez une page en sélectionnant le bouton d’engrenage en haut à droite, puis **sélectionnez Ajouter une page.**</span><span class="sxs-lookup"><span data-stu-id="be05b-155">In your site, create a new page by selecting the gear button at the upper right and then  select **Add a page**.</span></span>
<span data-ttu-id="be05b-156">L’image suivante affiche l’écran correspondant :</span><span class="sxs-lookup"><span data-stu-id="be05b-156">The following image displays the corresponding screen:</span></span>

   ![Vue SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image066.png)

1. <span data-ttu-id="be05b-158">Vous pouvez voir l’expérience de SharePoint pages de texte.</span><span class="sxs-lookup"><span data-stu-id="be05b-158">You can see the SharePoint pages authoring experience.</span></span> <span data-ttu-id="be05b-159">Nommez votre page sous **le nom Teams Onglet .**</span><span class="sxs-lookup"><span data-stu-id="be05b-159">Name your page as **My Teams Tab**.</span></span>

1. <span data-ttu-id="be05b-160">Ouvrez la boîte à outils du service Web En appuyant sur le bouton, puis sélectionnez `+` votre onglet Teams nommé **Contoso HR**.</span><span class="sxs-lookup"><span data-stu-id="be05b-160">Open the web part toolbox by pressing the `+` button, and select your Teams Tab, named **Contoso HR**.</span></span> <span data-ttu-id="be05b-161">Les composants Web Parts sont triés par ordre alphabétique.</span><span class="sxs-lookup"><span data-stu-id="be05b-161">Web parts are sorted alphabetically.</span></span> <span data-ttu-id="be05b-162">S’il s’agit d’une longue liste, vous pouvez utiliser la barre de recherche pour la trouver.</span><span class="sxs-lookup"><span data-stu-id="be05b-162">If it is a long list, you can use the search bar to find it.</span></span> <span data-ttu-id="be05b-163">Cela crée un élément Web Part dans la zone de dessin qui contient votre Teams de dessin. L’image suivante affiche l’affichage Onglet :</span><span class="sxs-lookup"><span data-stu-id="be05b-163">This creates a web part in the canvas that contains your Teams tab. The following image displays the tab view:</span></span>

   ![Affichage Onglet](~/assets/images/tabs/tabs-in-sharepoint/image071.png)

1. <span data-ttu-id="be05b-165">Appuyez sur **le** bouton Publier après avoir terminé la modification.</span><span class="sxs-lookup"><span data-stu-id="be05b-165">Press the **Publish** button after you finish  editing.</span></span>

1. <span data-ttu-id="be05b-166">Sélectionnez **Ajouter une page à la navigation** pour avoir une référence rapide à votre page dans la barre de navigation de gauche.</span><span class="sxs-lookup"><span data-stu-id="be05b-166">Select **Add page to navigation** to have a quick reference to your page in the left navigation bar.</span></span> <span data-ttu-id="be05b-167">L’image suivante affiche l’onglet dans SharePoint :</span><span class="sxs-lookup"><span data-stu-id="be05b-167">The following image displays the tab in Sharepoint:</span></span> 

   ![Onglet dans l’image Sharepoint](~/assets/images/tabs/tabs-in-sharepoint/image073.png)

## <a name="3-explore-app-pages-in-sharepoint"></a><span data-ttu-id="be05b-169">3. Explorer les pages d’application dans SharePoint</span><span class="sxs-lookup"><span data-stu-id="be05b-169">3. Explore App Pages in SharePoint</span></span>

<span data-ttu-id="be05b-170">Une fois votre page publiée, vous pouvez explorer comment transformer votre application Teams en une expérience plus complète à [l’intérieur SharePoint](/sharepoint/dev/spfx/web-parts/single-part-app-pages).</span><span class="sxs-lookup"><span data-stu-id="be05b-170">After your page is published, you can explore [turning your Teams app into a more complete experience inside SharePoint](/sharepoint/dev/spfx/web-parts/single-part-app-pages).</span></span> <span data-ttu-id="be05b-171">Cela convertit la page actuelle en page d’application, affichant la mise en page normale SharePoint page avec une expérience de page complète pour l’onglet Teams page.</span><span class="sxs-lookup"><span data-stu-id="be05b-171">This converts the current page into an App Page, showing the normal SharePoint page layout with a full page experience for the Teams tab.</span></span> 

<span data-ttu-id="be05b-172">L’image suivante affiche l’expérience complète de Teams’application dans Sharepoint : ![ Image des onglets dans Sharepoint](~/assets/images/tabs/tabs-in-sharepoint/image085.png)</span><span class="sxs-lookup"><span data-stu-id="be05b-172">The following image displays the complete experience of Teams app in Sharepoint: ![Image of Tabs in Sharepoint](~/assets/images/tabs/tabs-in-sharepoint/image085.png)</span></span>

## <a name="code-sample"></a><span data-ttu-id="be05b-173">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="be05b-173">Code sample</span></span>
| <span data-ttu-id="be05b-174">**Exemple de nom**</span><span class="sxs-lookup"><span data-stu-id="be05b-174">**Sample name**</span></span> | <span data-ttu-id="be05b-175">**Description**</span><span class="sxs-lookup"><span data-stu-id="be05b-175">**Description**</span></span> | <span data-ttu-id="be05b-176">**SPFx**</span><span class="sxs-lookup"><span data-stu-id="be05b-176">**SPFx**</span></span> |
|-----------------|-----------------|----------|
| <span data-ttu-id="be05b-177">SPFx Web Part</span><span class="sxs-lookup"><span data-stu-id="be05b-177">SPFx web part</span></span> | <span data-ttu-id="be05b-178">SPFx des exemples de webs pour les onglets, les canaux et les groupes.</span><span class="sxs-lookup"><span data-stu-id="be05b-178">SPFx web part samples for tabs, channels, and groups.</span></span> | [<span data-ttu-id="be05b-179">View</span><span class="sxs-lookup"><span data-stu-id="be05b-179">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group/spfx)

## <a name="see-also"></a><span data-ttu-id="be05b-180">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="be05b-180">See also</span></span>

* [<span data-ttu-id="be05b-181">Création d’un onglet Microsoft Teams à l’aide de SharePoint Framework - Didacticiel</span><span class="sxs-lookup"><span data-stu-id="be05b-181">Building Microsoft Teams tab using SharePoint Framework - Tutorial</span></span>](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)
* [<span data-ttu-id="be05b-182">Utilisation des pages d’application à composant unique dans SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="be05b-182">Using single part app pages in SharePoint Online</span></span>](/sharepoint/dev/spfx/web-parts/single-part-app-pages)
* [<span data-ttu-id="be05b-183">Intégrer les applications Web</span><span class="sxs-lookup"><span data-stu-id="be05b-183">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)
