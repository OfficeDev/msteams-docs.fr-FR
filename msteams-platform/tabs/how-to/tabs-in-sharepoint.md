---
title: Ajout d’un onglet Microsoft teams dans SharePoint en tant que composant WebPart SPFx
author: laujan
description: Comment déployer votre onglet teams existant vers SharePoint en tant que composant WebPart SharePoint Framework.
keywords: onglet teams développement SharePoint Framework
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 2bdc7ab578be485eee33020b3b0c1a4099fd8ade
ms.sourcegitcommit: e8dfcb167274e996395b77d65999991a18f2051a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/15/2020
ms.locfileid: "47818940"
---
# <a name="adding-a-microsoft-teams-tab-in-sharepoint-as-an-spfx-web-part"></a><span data-ttu-id="2f1a0-104">Ajout d’un onglet Microsoft teams dans SharePoint en tant que composant WebPart SPFx</span><span class="sxs-lookup"><span data-stu-id="2f1a0-104">Adding a Microsoft Teams tab in SharePoint as an SPFx web part</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2f1a0-105">Cette fonctionnalité est encore en phase préliminaire et est sujette à modifications.</span><span class="sxs-lookup"><span data-stu-id="2f1a0-105">This feature is currently in preview and is subject to change.</span></span> <span data-ttu-id="2f1a0-106">Elle n’est pas prise en charge dans les environnements de production.</span><span class="sxs-lookup"><span data-stu-id="2f1a0-106">It is not supported for use in production environments.</span></span> <span data-ttu-id="2f1a0-107">Vos commentaires et suggestions concernant cette fonctionnalité sont les bienvenus via la [liste des problèmes liés aux documents de développement SharePoint](https://github.com/SharePoint/sp-dev-docs/issues).</span><span class="sxs-lookup"><span data-stu-id="2f1a0-107">Your feedback and input around this capability is welcome using the [SharePoint Dev Docs issue list](https://github.com/SharePoint/sp-dev-docs/issues).</span></span>

## <a name="rich-integration-between-teams-and-sharepoint"></a><span data-ttu-id="2f1a0-108">Intégration enrichie entre teams et SharePoint</span><span class="sxs-lookup"><span data-stu-id="2f1a0-108">Rich integration between Teams and SharePoint</span></span>

<span data-ttu-id="2f1a0-109">Avec la version de novembre de teams et de SharePoint Framework v.</span><span class="sxs-lookup"><span data-stu-id="2f1a0-109">With the November release of Teams and SharePoint Framework v.</span></span> <span data-ttu-id="2f1a0-110">1,7, les développeurs disposent de deux fonctionnalités puissantes :</span><span class="sxs-lookup"><span data-stu-id="2f1a0-110">1.7, developers have two powerful capabilities:</span></span>

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
                        <h3><span data-ttu-id="2f1a0-111">Onglets teams dans SharePoint</span><span class="sxs-lookup"><span data-stu-id="2f1a0-111">Teams Tabs in SharePoint</span></span></h3>
                        <p><span data-ttu-id="2f1a0-112">Créez des expériences d’application enrichies dans SharePoint en plaçant votre application teams dans SharePoint (cet article).</span><span class="sxs-lookup"><span data-stu-id="2f1a0-112">Create rich app experiences in SharePoint by bringing your Teams app into Sharepoint (this article).</span></span></p>
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
                        <h3><span data-ttu-id="2f1a0-113">SharePoint Framework dans teams</span><span class="sxs-lookup"><span data-stu-id="2f1a0-113">SharePoint Framework in Teams</span></span></h3>
                        <p><span data-ttu-id="2f1a0-114">Intégrez vos composants WebPart SharePoint à teams et laissez SharePoint gérer l’hébergement pour vous.</span><span class="sxs-lookup"><span data-stu-id="2f1a0-114">Bring your SharePoint web parts to Teams and let SharePoint manage the hosting for you.</span></span></p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

### <a name="teams-tabs-in-sharepoint"></a><span data-ttu-id="2f1a0-115">Onglets teams dans SharePoint</span><span class="sxs-lookup"><span data-stu-id="2f1a0-115">Teams tabs in SharePoint</span></span>

<span data-ttu-id="2f1a0-116">Avec SharePoint Framework v. 1.7, nous prenons désormais en charge la possibilité pour les développeurs de prendre leurs onglets teams et de les héberger dans SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2f1a0-116">With SharePoint Framework v.1.7, we’re now supporting the ability for developers to take their Teams tabs and host it in SharePoint.</span></span> <span data-ttu-id="2f1a0-117">Sous forme d’onglets hébergés dans SharePoint, profitez d’une expérience de « pleine page » similaire, exposant toutes les fonctionnalités des onglets teams tout en conservant le contexte et la familiarité d’un site SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2f1a0-117">As Tabs hosted in SharePoint get a similar "full page" experience, exposing the all the features of Teams tabs while retaining the context and familiarity of a SharePoint site.</span></span>

### <a name="sharepoint-framework-in-teams"></a><span data-ttu-id="2f1a0-118">SharePoint Framework dans teams</span><span class="sxs-lookup"><span data-stu-id="2f1a0-118">SharePoint Framework in Teams</span></span>

<span data-ttu-id="2f1a0-119">Vous pouvez également implémenter vos onglets Microsoft teams à l’aide de SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="2f1a0-119">You can also implement your Microsoft Teams tabs using SharePoint Framework.</span></span> <span data-ttu-id="2f1a0-120">Pour les développeurs SharePoint, cela simplifie considérablement le processus de développement pour les onglets Teams, car les composants WebPart de SharePoint Framework sont hébergés dans SharePoint sans qu’il soit nécessaire de recourir à des services externes comme Azure.</span><span class="sxs-lookup"><span data-stu-id="2f1a0-120">For SharePoint developers, this significantly simplifies the development process for Teams tabs because SharePoint Framework web parts are hosted within SharePoint without any need for external services such as Azure.</span></span> [<span data-ttu-id="2f1a0-121">En savoir plus sur l’utilisation de SharePoint Framework dans Teams.</span><span class="sxs-lookup"><span data-stu-id="2f1a0-121">Learn more about using the SharePoint Framework in Teams.</span></span>](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)

## <a name="introduction"></a><span data-ttu-id="2f1a0-122">Introduction</span><span class="sxs-lookup"><span data-stu-id="2f1a0-122">Introduction</span></span>

<span data-ttu-id="2f1a0-123">Ces instructions vous expliquent comment prendre un onglet à partir d’un exemple d’application Microsoft teams et comment l’utiliser dans SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2f1a0-123">These instructions will explain how you can take a tab from a Microsoft Teams sample app and use it in SharePoint.</span></span> <span data-ttu-id="2f1a0-124">Nous allons utiliser un onglet qui est déjà hébergé sur Azure afin de se concentrer sur le travail d’intégration requis.</span><span class="sxs-lookup"><span data-stu-id="2f1a0-124">We will be using a tab that's already hosted on Azure in order to focus on the required integration work.</span></span>

<span data-ttu-id="2f1a0-125">L’exemple d’application que nous utilisons est une application de gestion des compétences.</span><span class="sxs-lookup"><span data-stu-id="2f1a0-125">The sample app we're using is a Talent Management application.</span></span> <span data-ttu-id="2f1a0-126">Il gère le processus d’embauche de candidats pour les postes ouverts dans une équipe.</span><span class="sxs-lookup"><span data-stu-id="2f1a0-126">It manages the hiring process of candidates for open positions in a team.</span></span> <span data-ttu-id="2f1a0-127">(L’application elle-même, même si elle semble agréable, ne fait rien.</span><span class="sxs-lookup"><span data-stu-id="2f1a0-127">(The app itself, while it looks nice, doesn't actually do anything.</span></span> <span data-ttu-id="2f1a0-128">Nous souhaitons vous concentrer sur la création d’une application teams et son chargement dans Teams, et non sur la création d’une véritable application de gestion des compétences.)</span><span class="sxs-lookup"><span data-stu-id="2f1a0-128">We want to focus on building a Teams app and loading it into Teams, not create a real talent management application.)</span></span>

### <a name="benefits-of-this-approach"></a><span data-ttu-id="2f1a0-129">Avantages de cette approche</span><span class="sxs-lookup"><span data-stu-id="2f1a0-129">Benefits of this approach</span></span>

- <span data-ttu-id="2f1a0-130">Atteindre les utilisateurs SharePoint avec votre onglet teams existant</span><span class="sxs-lookup"><span data-stu-id="2f1a0-130">Reach SharePoint users with your existing Teams tab</span></span>
- <span data-ttu-id="2f1a0-131">Téléchargez le manifeste de votre application directement dans votre catalogue d’applications SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2f1a0-131">Upload your app manifest directly to your SharePoint app catalog.</span></span> <span data-ttu-id="2f1a0-132">Les [packages d’applications teams](~/concepts/build-and-test/apps-package.md) sont désormais pris en charge par SharePoint</span><span class="sxs-lookup"><span data-stu-id="2f1a0-132">[Teams application packages](~/concepts/build-and-test/apps-package.md) are now supported by SharePoint</span></span>
- <span data-ttu-id="2f1a0-133">Les utilisateurs finaux configurent l’onglet sur une page comme n’importe quel autre composant WebPart SharePoint</span><span class="sxs-lookup"><span data-stu-id="2f1a0-133">End users configure the tab on a page just like any other SharePoint web part</span></span>
- <span data-ttu-id="2f1a0-134">Votre onglet peut accéder à son [contexte](~/tabs/how-to/access-teams-context.md) comme il le peut lorsqu’il est exécuté dans teams</span><span class="sxs-lookup"><span data-stu-id="2f1a0-134">Your tab can access its [context](~/tabs/how-to/access-teams-context.md) just as it can when running inside Teams</span></span>

## <a name="step-1-testing-the-sample-app"></a><span data-ttu-id="2f1a0-135">Étape 1 : test de l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="2f1a0-135">Step 1: Testing the sample app</span></span>

<span data-ttu-id="2f1a0-136">Téléchargez l’exemple de manifeste d’application à partir de [**cet emplacement**](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip).</span><span class="sxs-lookup"><span data-stu-id="2f1a0-136">Download the sample app manifest from [**here**](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip).</span></span>

<span data-ttu-id="2f1a0-137">Dans Microsoft Teams, cliquez sur l’icône de la boutique située en bas à gauche, puis sur « Télécharger une application personnalisée » en bas à gauche.</span><span class="sxs-lookup"><span data-stu-id="2f1a0-137">In Microsoft Teams, click on the Store icon at the lower left and then "Upload a custom app" at the lower left.</span></span> <span data-ttu-id="2f1a0-138">Le fichier à télécharger sera situé dans votre dossier téléchargements ; Il est appelé TalentMgmt-Azure.zip.</span><span class="sxs-lookup"><span data-stu-id="2f1a0-138">The file to upload will be located in your Downloads folder; it's called TalentMgmt-Azure.zip.</span></span> <span data-ttu-id="2f1a0-139">Si tout se passe bien, vous verrez l’écran d’installation/de consentement pour l’application de gestion des compétences.</span><span class="sxs-lookup"><span data-stu-id="2f1a0-139">If all goes well, you'll see the install/consent screen for the talent management app.</span></span> <span data-ttu-id="2f1a0-140">Choisissez l’équipe sur laquelle vous souhaitez effectuer l’installation, puis cliquez sur le bouton installer.</span><span class="sxs-lookup"><span data-stu-id="2f1a0-140">Choose the team you want to install to and click the Install button.</span></span> <span data-ttu-id="2f1a0-141">Vous êtes maintenant libre de tester l’application.</span><span class="sxs-lookup"><span data-stu-id="2f1a0-141">You're now free to experiment with the app.</span></span>

## <a name="step-2-using-the-teams-tab-in-sharepoint"></a><span data-ttu-id="2f1a0-142">Étape 2 : utilisation de l’onglet teams dans SharePoint</span><span class="sxs-lookup"><span data-stu-id="2f1a0-142">Step 2: Using the Teams tab in SharePoint</span></span>

<span data-ttu-id="2f1a0-143">Téléchargez et déployez votre package d’applications teams dans votre catalogue d’applications SharePoint en visitant `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` , par exemple `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` .</span><span class="sxs-lookup"><span data-stu-id="2f1a0-143">Upload and deploy your Teams app package to your SharePoint App Catalog by visiting `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`, e.g. `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`.</span></span>

<span data-ttu-id="2f1a0-144">Lorsque vous y êtes invité, activez la « rendre cette solution disponible pour tous les sites de l’Organisation » :</span><span class="sxs-lookup"><span data-stu-id="2f1a0-144">When prompted, enable "Make this solution available to all sites in the organization":</span></span>

![Onglets dans l’affichage SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image065.png)

<span data-ttu-id="2f1a0-146">Dans votre site, créez une page en cliquant sur le bouton engrenage dans le coin supérieur droit, puis ajoutez une page :</span><span class="sxs-lookup"><span data-stu-id="2f1a0-146">In your site, create a new page by clicking in the gear button at the upper right and then "Add a page":</span></span>

![Vue SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image066.png)

<span data-ttu-id="2f1a0-148">Vous verrez l’expérience de création de pages SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2f1a0-148">You'll see the SharePoint Pages authoring experience.</span></span> <span data-ttu-id="2f1a0-149">Nommez votre page « onglet My Teams ».</span><span class="sxs-lookup"><span data-stu-id="2f1a0-149">Name your page "My Teams Tab".</span></span>

<span data-ttu-id="2f1a0-150">Ouvrez la boîte à outils du composant WebPart en appuyant sur le bouton +, puis sélectionnez l’onglet Teams (nommé « Contoso HR »).</span><span class="sxs-lookup"><span data-stu-id="2f1a0-150">Open the web part toolbox by pressing the + button, and select your Teams Tab (named "Contoso HR").</span></span> <span data-ttu-id="2f1a0-151">Les composants WebPart sont triés par ordre alphabétique ; s’il s’agit d’une longue liste, vous pouvez utiliser la barre de recherche pour la trouver.</span><span class="sxs-lookup"><span data-stu-id="2f1a0-151">Web parts are sorted alphabetically; if it's a long list, you can use the search bar to find it.</span></span> <span data-ttu-id="2f1a0-152">Cette opération crée un composant WebPart dans la zone de dessin qui contient l’onglet teams :</span><span class="sxs-lookup"><span data-stu-id="2f1a0-152">This will create a web part in the canvas that contains your Teams tab:</span></span>

![Affichage onglet](~/assets/images/tabs/tabs-in-sharepoint/image071.png)

<span data-ttu-id="2f1a0-154">Appuyez sur le bouton « Publier » lorsque vous avez terminé les modifications.</span><span class="sxs-lookup"><span data-stu-id="2f1a0-154">Press the "Publish" button when you are finished editing.</span></span>

<span data-ttu-id="2f1a0-155">Vous souhaiterez peut-être cliquer sur Ajouter une page à la navigation pour obtenir une référence rapide à votre page dans la barre de navigation de gauche :</span><span class="sxs-lookup"><span data-stu-id="2f1a0-155">You may want to click "Add page to navigation" to have a quick reference to your page in the left navigation bar:</span></span>

![Onglet dans l’image SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image073.png)

## <a name="step-3-explore-app-pages-in-sharepoint"></a><span data-ttu-id="2f1a0-157">Étape 3 : explorer les pages d’application dans SharePoint</span><span class="sxs-lookup"><span data-stu-id="2f1a0-157">Step 3: Explore App Pages in SharePoint</span></span>

<span data-ttu-id="2f1a0-158">Une fois votre page publiée, vous pouvez explorer [la transformation de votre application teams en une expérience plus complète dans SharePoint](/sharepoint/dev/spfx/web-parts/single-part-app-pages).</span><span class="sxs-lookup"><span data-stu-id="2f1a0-158">Once your page is published, you can explore [turning your Teams app into a more complete experience inside SharePoint](/sharepoint/dev/spfx/web-parts/single-part-app-pages).</span></span> <span data-ttu-id="2f1a0-159">Cette fonction convertit la page actuelle en page d’application, affichant la mise en page SharePoint normale avec une expérience pleine page pour l’onglet teams :</span><span class="sxs-lookup"><span data-stu-id="2f1a0-159">This converts the current page into an App Page, showing the normal SharePoint page layout with a full-page experience for the Teams tab:</span></span>

![Image d’onglets dans SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image085.png)

## <a name="more-information"></a><span data-ttu-id="2f1a0-161">Plus d’informations</span><span class="sxs-lookup"><span data-stu-id="2f1a0-161">More information</span></span>

- [<span data-ttu-id="2f1a0-162">Création d’un onglet Microsoft Teams à l’aide de SharePoint Framework - Didacticiel</span><span class="sxs-lookup"><span data-stu-id="2f1a0-162">Building Microsoft Teams tab using SharePoint Framework - Tutorial</span></span>](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)
- [<span data-ttu-id="2f1a0-163">Utilisation des pages d’application à composant unique dans SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="2f1a0-163">Using single part app pages in SharePoint Online</span></span>](/sharepoint/dev/spfx/web-parts/single-part-app-pages)
