---
title: Ajout d’un onglet Microsoft Teams dans SharePoint en tant que partie Web SPFx
author: laujan
description: Comment déployer votre onglet Teams existant sur SharePoint en tant que partie Web De l’infrastructure SharePoint.
keywords: teams tabs sharepoint framework development
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 2e5d1b01aa5f7566e25c7720d6a0539386226576
ms.sourcegitcommit: 6caf503de5544fb8b9c8c6bef8eff4ff5a46068c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/17/2021
ms.locfileid: "50270790"
---
# <a name="adding-a-microsoft-teams-tab-in-sharepoint-as-an-spfx-web-part"></a><span data-ttu-id="f381c-104">Ajout d’un onglet Microsoft Teams dans SharePoint en tant que partie Web SPFx</span><span class="sxs-lookup"><span data-stu-id="f381c-104">Adding a Microsoft Teams tab in SharePoint as an SPFx web part</span></span>

## <a name="rich-integration-between-teams-and-sharepoint"></a><span data-ttu-id="f381c-105">Intégration enrichie entre Teams et SharePoint</span><span class="sxs-lookup"><span data-stu-id="f381c-105">Rich integration between Teams and SharePoint</span></span>

<span data-ttu-id="f381c-106">Avec la version de novembre de Teams et SharePoint Framework v.</span><span class="sxs-lookup"><span data-stu-id="f381c-106">With the November release of Teams and SharePoint Framework v.</span></span> <span data-ttu-id="f381c-107">1.7, les développeurs ont deux fonctionnalités puissantes :</span><span class="sxs-lookup"><span data-stu-id="f381c-107">1.7, developers have two powerful capabilities:</span></span>

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
                        <h3><span data-ttu-id="f381c-108">Onglets Teams dans SharePoint</span><span class="sxs-lookup"><span data-stu-id="f381c-108">Teams Tabs in SharePoint</span></span></h3>
                        <p><span data-ttu-id="f381c-109">Créez des expériences d’application enrichies dans SharePoint en apportant votre application Teams dans SharePoint (cet article).</span><span class="sxs-lookup"><span data-stu-id="f381c-109">Create rich app experiences in SharePoint by bringing your Teams app into Sharepoint (this article).</span></span></p>
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
                        <h3><span data-ttu-id="f381c-110">SharePoint Framework dans Teams</span><span class="sxs-lookup"><span data-stu-id="f381c-110">SharePoint Framework in Teams</span></span></h3>
                        <p><span data-ttu-id="f381c-111">Apportez vos composants Web Parts SharePoint à Teams et laissez SharePoint gérer l’hébergement pour vous.</span><span class="sxs-lookup"><span data-stu-id="f381c-111">Bring your SharePoint web parts to Teams and let SharePoint manage the hosting for you.</span></span></p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

### <a name="teams-tabs-in-sharepoint"></a><span data-ttu-id="f381c-112">Onglets Teams dans SharePoint</span><span class="sxs-lookup"><span data-stu-id="f381c-112">Teams tabs in SharePoint</span></span>

<span data-ttu-id="f381c-113">Avec SharePoint Framework v.1.7, nous prenons désormais en charge la possibilité pour les développeurs de prendre leurs onglets Teams et de les héberger dans SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f381c-113">With SharePoint Framework v.1.7, we’re now supporting the ability for developers to take their Teams tabs and host it in SharePoint.</span></span> <span data-ttu-id="f381c-114">Comme les onglets hébergés dans SharePoint obtiennent une expérience de « page entière » similaire, en exposant toutes les fonctionnalités des onglets Teams tout en conservant le contexte et la familiarité d’un site SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f381c-114">As Tabs hosted in SharePoint get a similar "full page" experience, exposing the all the features of Teams tabs while retaining the context and familiarity of a SharePoint site.</span></span>

### <a name="sharepoint-framework-in-teams"></a><span data-ttu-id="f381c-115">SharePoint Framework dans Teams</span><span class="sxs-lookup"><span data-stu-id="f381c-115">SharePoint Framework in Teams</span></span>

<span data-ttu-id="f381c-116">Vous pouvez également implémenter vos onglets Microsoft Teams à l’aide de SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="f381c-116">You can also implement your Microsoft Teams tabs using SharePoint Framework.</span></span> <span data-ttu-id="f381c-117">Pour les développeurs SharePoint, cela simplifie considérablement le processus de développement pour les onglets Teams, car les composants Web Parts SharePoint Framework sont hébergés dans SharePoint sans avoir besoin de services externes tels qu’Azure.</span><span class="sxs-lookup"><span data-stu-id="f381c-117">For SharePoint developers, this significantly simplifies the development process for Teams tabs because SharePoint Framework web parts are hosted within SharePoint without any need for external services such as Azure.</span></span> [<span data-ttu-id="f381c-118">En savoir plus sur l’utilisation de SharePoint Framework dans Teams.</span><span class="sxs-lookup"><span data-stu-id="f381c-118">Learn more about using the SharePoint Framework in Teams.</span></span>](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)

## <a name="introduction"></a><span data-ttu-id="f381c-119">Introduction</span><span class="sxs-lookup"><span data-stu-id="f381c-119">Introduction</span></span>

<span data-ttu-id="f381c-120">Ces instructions expliquent comment vous pouvez prendre un onglet à partir d’un exemple d’application Microsoft Teams et l’utiliser dans SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f381c-120">These instructions will explain how you can take a tab from a Microsoft Teams sample app and use it in SharePoint.</span></span> <span data-ttu-id="f381c-121">Nous allons utiliser un onglet qui est déjà hébergé sur Azure afin de nous concentrer sur le travail d’intégration requis.</span><span class="sxs-lookup"><span data-stu-id="f381c-121">We will be using a tab that's already hosted on Azure in order to focus on the required integration work.</span></span>

<span data-ttu-id="f381c-122">L’exemple d’application que nous utilisons est une application de gestion des talents.</span><span class="sxs-lookup"><span data-stu-id="f381c-122">The sample app we're using is a Talent Management application.</span></span> <span data-ttu-id="f381c-123">Il gère le processus d’embauche des candidats pour les postes ouverts dans une équipe.</span><span class="sxs-lookup"><span data-stu-id="f381c-123">It manages the hiring process of candidates for open positions in a team.</span></span> <span data-ttu-id="f381c-124">(L’application elle-même, bien qu’elle semble agréable, n’a réellement rien à faire.</span><span class="sxs-lookup"><span data-stu-id="f381c-124">(The app itself, while it looks nice, doesn't actually do anything.</span></span> <span data-ttu-id="f381c-125">Nous voulons nous concentrer sur la création d’une application Teams et son chargement dans Teams, et non sur la création d’une application de gestion des talents réelle.)</span><span class="sxs-lookup"><span data-stu-id="f381c-125">We want to focus on building a Teams app and loading it into Teams, not create a real talent management application.)</span></span>

### <a name="benefits-of-this-approach"></a><span data-ttu-id="f381c-126">Avantages de cette approche</span><span class="sxs-lookup"><span data-stu-id="f381c-126">Benefits of this approach</span></span>

- <span data-ttu-id="f381c-127">Atteindre les utilisateurs SharePoint avec votre onglet Teams existant</span><span class="sxs-lookup"><span data-stu-id="f381c-127">Reach SharePoint users with your existing Teams tab</span></span>
- <span data-ttu-id="f381c-128">Téléchargez votre manifeste d’application directement dans votre catalogue d’applications SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f381c-128">Upload your app manifest directly to your SharePoint app catalog.</span></span> <span data-ttu-id="f381c-129">[Les packages d’application Teams](~/concepts/build-and-test/apps-package.md) sont désormais pris en charge par SharePoint</span><span class="sxs-lookup"><span data-stu-id="f381c-129">[Teams application packages](~/concepts/build-and-test/apps-package.md) are now supported by SharePoint</span></span>
- <span data-ttu-id="f381c-130">Les utilisateurs finaux configurent l’onglet d’une page comme n’importe quel autre élément Web Part SharePoint</span><span class="sxs-lookup"><span data-stu-id="f381c-130">End users configure the tab on a page just like any other SharePoint web part</span></span>
- <span data-ttu-id="f381c-131">Votre onglet peut accéder à son [contexte](~/tabs/how-to/access-teams-context.md) comme il le peut lors de l’exécution dans Teams</span><span class="sxs-lookup"><span data-stu-id="f381c-131">Your tab can access its [context](~/tabs/how-to/access-teams-context.md) just as it can when running inside Teams</span></span>

## <a name="step-1-testing-the-sample-app"></a><span data-ttu-id="f381c-132">Étape 1 : Test de l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="f381c-132">Step 1: Testing the sample app</span></span>

<span data-ttu-id="f381c-133">Téléchargez l’exemple de manifeste d’application [**à partir d’ici.**](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip)</span><span class="sxs-lookup"><span data-stu-id="f381c-133">Download the sample app manifest from [**here**](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip).</span></span>

<span data-ttu-id="f381c-134">Dans Microsoft Teams, cliquez sur l’icône du Store en bas à gauche, puis sur « Télécharger une application personnalisée » en bas à gauche.</span><span class="sxs-lookup"><span data-stu-id="f381c-134">In Microsoft Teams, click on the Store icon at the lower left and then "Upload a custom app" at the lower left.</span></span> <span data-ttu-id="f381c-135">Le fichier à télécharger se trouve dans votre dossier Téléchargements ; Il s’appelle TalentMgmt-Azure.zip.</span><span class="sxs-lookup"><span data-stu-id="f381c-135">The file to upload will be located in your Downloads folder; it's called TalentMgmt-Azure.zip.</span></span> <span data-ttu-id="f381c-136">Si tout se passe bien, l’écran d’installation/consentement s’affiche pour l’application de gestion des talents.</span><span class="sxs-lookup"><span data-stu-id="f381c-136">If all goes well, you'll see the install/consent screen for the talent management app.</span></span> <span data-ttu-id="f381c-137">Choisissez l’équipe dans qui vous souhaitez installer, puis cliquez sur le bouton Installer.</span><span class="sxs-lookup"><span data-stu-id="f381c-137">Choose the team you want to install to and click the Install button.</span></span> <span data-ttu-id="f381c-138">Vous êtes désormais libre d’expérimenter l’application.</span><span class="sxs-lookup"><span data-stu-id="f381c-138">You're now free to experiment with the app.</span></span>

## <a name="step-2-using-the-teams-tab-in-sharepoint"></a><span data-ttu-id="f381c-139">Étape 2 : utilisation de l’onglet Teams dans SharePoint</span><span class="sxs-lookup"><span data-stu-id="f381c-139">Step 2: Using the Teams tab in SharePoint</span></span>

<span data-ttu-id="f381c-140">Téléchargez et déployez votre package d’application Teams dans votre catalogue d’applications SharePoint en visitant , par `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` exemple. `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`</span><span class="sxs-lookup"><span data-stu-id="f381c-140">Upload and deploy your Teams app package to your SharePoint App Catalog by visiting `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`, e.g. `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`.</span></span>

<span data-ttu-id="f381c-141">Lorsque vous y sont invités, activez « Rendre cette solution disponible pour tous les sites de l’organisation » :</span><span class="sxs-lookup"><span data-stu-id="f381c-141">When prompted, enable "Make this solution available to all sites in the organization":</span></span>

![Onglets en vue SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image065.png)

<span data-ttu-id="f381c-143">Dans votre site, créez une page en cliquant sur le bouton d’engrenage en haut à droite, puis sur « Ajouter une page » :</span><span class="sxs-lookup"><span data-stu-id="f381c-143">In your site, create a new page by clicking in the gear button at the upper right and then "Add a page":</span></span>

![Vue SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image066.png)

<span data-ttu-id="f381c-145">Vous verrez l’expérience de authoring des pages SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f381c-145">You'll see the SharePoint Pages authoring experience.</span></span> <span data-ttu-id="f381c-146">Nommez votre page « Onglet Mes équipes ».</span><span class="sxs-lookup"><span data-stu-id="f381c-146">Name your page "My Teams Tab".</span></span>

<span data-ttu-id="f381c-147">Ouvrez la boîte à outils du volet Web En appuyant sur le bouton + et sélectionnez l’onglet Teams (nommé « Contoso HR »).</span><span class="sxs-lookup"><span data-stu-id="f381c-147">Open the web part toolbox by pressing the + button, and select your Teams Tab (named "Contoso HR").</span></span> <span data-ttu-id="f381c-148">Les composants Web Parts sont triés par ordre alphabétique ; S’il s’agit d’une longue liste, vous pouvez utiliser la barre de recherche pour la trouver.</span><span class="sxs-lookup"><span data-stu-id="f381c-148">Web parts are sorted alphabetically; if it's a long list, you can use the search bar to find it.</span></span> <span data-ttu-id="f381c-149">Cela crée un élément Web Part dans le canevas qui contient votre onglet Teams :</span><span class="sxs-lookup"><span data-stu-id="f381c-149">This will create a web part in the canvas that contains your Teams tab:</span></span>

![Affichage Onglet](~/assets/images/tabs/tabs-in-sharepoint/image071.png)

<span data-ttu-id="f381c-151">Appuyez sur le bouton « Publier » lorsque vous avez terminé la modification.</span><span class="sxs-lookup"><span data-stu-id="f381c-151">Press the "Publish" button when you are finished editing.</span></span>

<span data-ttu-id="f381c-152">Vous pouvez cliquer sur « Ajouter une page à la navigation » pour avoir une référence rapide à votre page dans la barre de navigation de gauche :</span><span class="sxs-lookup"><span data-stu-id="f381c-152">You may want to click "Add page to navigation" to have a quick reference to your page in the left navigation bar:</span></span>

![Onglet dans l’image Sharepoint](~/assets/images/tabs/tabs-in-sharepoint/image073.png)

## <a name="step-3-explore-app-pages-in-sharepoint"></a><span data-ttu-id="f381c-154">Étape 3 : Explorer les pages d’application dans SharePoint</span><span class="sxs-lookup"><span data-stu-id="f381c-154">Step 3: Explore App Pages in SharePoint</span></span>

<span data-ttu-id="f381c-155">Une fois votre page publiée, vous pouvez explorer comment transformer votre application Teams en une expérience plus [complète dans SharePoint.](/sharepoint/dev/spfx/web-parts/single-part-app-pages)</span><span class="sxs-lookup"><span data-stu-id="f381c-155">Once your page is published, you can explore [turning your Teams app into a more complete experience inside SharePoint](/sharepoint/dev/spfx/web-parts/single-part-app-pages).</span></span> <span data-ttu-id="f381c-156">Cela convertit la page actuelle en page d’application, affichant la mise en page SharePoint normale avec une expérience de page complète pour l’onglet Teams :</span><span class="sxs-lookup"><span data-stu-id="f381c-156">This converts the current page into an App Page, showing the normal SharePoint page layout with a full-page experience for the Teams tab:</span></span>

![Image des onglets dans SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image085.png)

## <a name="code-sample"></a><span data-ttu-id="f381c-158">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="f381c-158">Code sample</span></span>
| <span data-ttu-id="f381c-159">**Exemple de nom**</span><span class="sxs-lookup"><span data-stu-id="f381c-159">**Sample name**</span></span> | <span data-ttu-id="f381c-160">**Description**</span><span class="sxs-lookup"><span data-stu-id="f381c-160">**Description**</span></span> | <span data-ttu-id="f381c-161">**SPFx**</span><span class="sxs-lookup"><span data-stu-id="f381c-161">**SPFx**</span></span> |
|-----------------|-----------------|----------|
| <span data-ttu-id="f381c-162">Partie Web SPFx</span><span class="sxs-lookup"><span data-stu-id="f381c-162">SPFx web part</span></span> | <span data-ttu-id="f381c-163">Exemples de partie Web SPFx pour les onglets, les canaux et les groupes.</span><span class="sxs-lookup"><span data-stu-id="f381c-163">SPFx web part samples for tabs, channels, and groups.</span></span> | [<span data-ttu-id="f381c-164">View</span><span class="sxs-lookup"><span data-stu-id="f381c-164">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group/spfx)

## <a name="more-information"></a><span data-ttu-id="f381c-165">Plus d’informations</span><span class="sxs-lookup"><span data-stu-id="f381c-165">More information</span></span>

- [<span data-ttu-id="f381c-166">Création d’un onglet Microsoft Teams à l’aide de SharePoint Framework - Didacticiel</span><span class="sxs-lookup"><span data-stu-id="f381c-166">Building Microsoft Teams tab using SharePoint Framework - Tutorial</span></span>](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)
- [<span data-ttu-id="f381c-167">Utilisation des pages d’application à composant unique dans SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="f381c-167">Using single part app pages in SharePoint Online</span></span>](/sharepoint/dev/spfx/web-parts/single-part-app-pages)
