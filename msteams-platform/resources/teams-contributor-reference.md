---
title: Contribuer à la Teams documentation
description: étapes de création et de publication de Teams documentation
author: surbhigupta
ms.author: lajanuar
localization_priority: Normal
ms.topic: contributor-guide
ms.openlocfilehash: a567b0462397780650d6173df9dae1b340a06f97
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140510"
---
# <a name="contribute-to-teams-documentation"></a><span data-ttu-id="057b4-103">Contribuer à la Teams documentation</span><span class="sxs-lookup"><span data-stu-id="057b4-103">Contribute to Teams documentation</span></span>

<span data-ttu-id="057b4-104">Teams documentation technique fait partie de la bibliothèque de documentation technique **Microsoft Docs.**</span><span class="sxs-lookup"><span data-stu-id="057b4-104">Teams documentation is part of the **Microsoft Docs** technical documentation library.</span></span> <span data-ttu-id="057b4-105">Le contenu est organisé en groupes appelés jeux de documents, chacun représentant un groupe de documents associés gérés en tant qu’entité unique.</span><span class="sxs-lookup"><span data-stu-id="057b4-105">The content is organized into groups called docsets, each representing a group of related documents managed as a single entity.</span></span> <span data-ttu-id="057b4-106">Les articles du même ensemble de documents ont la même extension de chemin d’URL **docs.microsoft.com**.</span><span class="sxs-lookup"><span data-stu-id="057b4-106">Articles in the same docset have the same URL path extension after **docs.microsoft.com**.</span></span> <span data-ttu-id="057b4-107">Par exemple, `/docs.microsoft.com/microsoftteams/...` est le début du chemin d Teams fichier docset.</span><span class="sxs-lookup"><span data-stu-id="057b4-107">For example, `/docs.microsoft.com/microsoftteams/...` is the beginning of the Teams docset file path.</span></span> <span data-ttu-id="057b4-108">Teams articles sont écrits en syntaxe Markdown et hébergés sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="057b4-108">Teams articles are written in Markdown syntax and hosted on GitHub.</span></span>

## <a name="set-up-your-workspace"></a><span data-ttu-id="057b4-109">Configurer votre espace de travail</span><span class="sxs-lookup"><span data-stu-id="057b4-109">Set up your workspace</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="057b4-110">Installez [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).</span><span class="sxs-lookup"><span data-stu-id="057b4-110">Install [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).</span></span>
> * <span data-ttu-id="057b4-111">Installez [Visual Studio Code](https://code.visualstudio.com/) (VS Code).</span><span class="sxs-lookup"><span data-stu-id="057b4-111">Install [Visual Studio Code](https://code.visualstudio.com/) (VS Code).</span></span>
> * <span data-ttu-id="057b4-112">Installez [docs Authoring Pack](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) directement à partir de VS Code Marketplace.</span><span class="sxs-lookup"><span data-stu-id="057b4-112">Install [Docs Authoring Pack](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) directly from the VS Code Marketplace.</span></span>
<br><span data-ttu-id="057b4-113">&emsp;&emsp; ou</span><span class="sxs-lookup"><span data-stu-id="057b4-113">&emsp;&emsp; or</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="057b4-114">Installez dans VS Code :</span><span class="sxs-lookup"><span data-stu-id="057b4-114">Install within VS Code:</span></span>

   1. <span data-ttu-id="057b4-115">Sélectionnez l’icône **Extensions** dans la barre d’activité latérale ou utilisez la commande **View => Extensions** ou Ctrl+Shift+X et recherchez **Microsoft Docs Authoring Pack**.</span><span class="sxs-lookup"><span data-stu-id="057b4-115">Select the **Extensions icon** on the side activity bar or use the **View => Extensions** command or Ctrl+Shift+X and, search for **Microsoft Docs Authoring Pack**.</span></span>
   1. <span data-ttu-id="057b4-116">Sélectionnez **Installer**.</span><span class="sxs-lookup"><span data-stu-id="057b4-116">Select **Install**.</span></span>
   1. <span data-ttu-id="057b4-117">Après l’installation, **l’installation** est apportée au **bouton Gérer** l’engrenage.</span><span class="sxs-lookup"><span data-stu-id="057b4-117">After installation, the **Install** changes to the **Manage** gear button.</span></span>

## <a name="review-the-microsoft-docs-contributors-guide"></a><span data-ttu-id="057b4-118">Consulter le Guide des contributeurs de documents Microsoft</span><span class="sxs-lookup"><span data-stu-id="057b4-118">Review the Microsoft Docs Contributors Guide</span></span>

<span data-ttu-id="057b4-119">Le guide des collaborateurs fournit des instructions pour créer, publier et mettre à jour du contenu technique sur la **plateforme Microsoft Docs.**</span><span class="sxs-lookup"><span data-stu-id="057b4-119">The contributors guide provides direction to create, publish, and update technical content on the **Microsoft Docs** platform.</span></span> 

## <a name="microsoft-writing-style-and-content-guides"></a><span data-ttu-id="057b4-120">Guides d’écriture, de style et de contenu Microsoft</span><span class="sxs-lookup"><span data-stu-id="057b4-120">Microsoft Writing, Style, and Content Guides</span></span>

* <span data-ttu-id="057b4-121">**[Guide de style d’écriture Microsoft](/style-guide/welcome)**: le Guide de style d’écriture Microsoft est une ressource complète pour l’écriture technique et reflète l’approche moderne de Microsoft en matière de voix et de style.</span><span class="sxs-lookup"><span data-stu-id="057b4-121">**[Microsoft Writing Style Guide](/style-guide/welcome)**: Microsoft Writing Style Guide is a comprehensive resource for technical writing and reflects Microsoft's modern approach to voice and style.</span></span> <span data-ttu-id="057b4-122">Pour faciliter la référence, ajoutez ce guide en ligne au menu **Favoris de votre** navigateur.</span><span class="sxs-lookup"><span data-stu-id="057b4-122">For easy reference, add this online guide to your browser's **Favorites** menu.</span></span>

* <span data-ttu-id="057b4-123">**[Écriture de contenu développeur](/style-guide/developer-content/)**: Teams contenu spécifique est destiné à un public de développeurs ayant une compréhension fondamentale des concepts et processus de programmation.</span><span class="sxs-lookup"><span data-stu-id="057b4-123">**[Writing developer content](/style-guide/developer-content/)**: Teams specific content is aimed at a developer audience with a fundamental understanding of programming concepts and processes.</span></span> <span data-ttu-id="057b4-124">Il est important que vous fournissiez des informations claires et techniquement précises de manière attrayante tout en conservant le style et le ton de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="057b4-124">It is important that you must provide clear, technically accurate information in a compelling manner while maintaining Microsoft's tone and style.</span></span>

* <span data-ttu-id="057b4-125">**[Écriture d’instructions pas à pas](/style-guide/procedures-instructions/writing-step-by-step-instructions)**: les expériences appliquées et interactives sont un excellent moyen pour les développeurs d’en savoir plus sur les produits et technologies Microsoft.</span><span class="sxs-lookup"><span data-stu-id="057b4-125">**[Writing step-by-step instructions](/style-guide/procedures-instructions/writing-step-by-step-instructions)**: Applied and interactive experiences are a great way for developers to learn about Microsoft products and technologies.</span></span> <span data-ttu-id="057b4-126">La présentation de procédures complexes ou simples dans un format progressif est naturelle et conviviale.</span><span class="sxs-lookup"><span data-stu-id="057b4-126">Presenting complex or simple procedures in a progressive format is natural and user friendly.</span></span>

## <a name="markdown-reference"></a><span data-ttu-id="057b4-127">Référence MarkDown</span><span class="sxs-lookup"><span data-stu-id="057b4-127">MarkDown reference</span></span>

<span data-ttu-id="057b4-128">Les pages **Microsoft Docs** sont écrites dans la syntaxe **MarkDown** et sont par le biais d’un [moteur Markdig.](https://github.com/lunet-io/markdig)</span><span class="sxs-lookup"><span data-stu-id="057b4-128">**Microsoft Docs** pages are written in **MarkDown** syntax and parsed through a [Markdig](https://github.com/lunet-io/markdig) engine.</span></span> <span data-ttu-id="057b4-129">Pour plus d’informations sur des balises et des conventions de mise en forme spécifiques, voir [référence Docs Markdown](/contribute/markdown-reference).</span><span class="sxs-lookup"><span data-stu-id="057b4-129">For more information on specific tags and formatting conventions, see [Docs Markdown reference](/contribute/markdown-reference).</span></span>

## <a name="file-paths"></a><span data-ttu-id="057b4-130">Chemins d’accès aux fichiers</span><span class="sxs-lookup"><span data-stu-id="057b4-130">File Paths</span></span>

<span data-ttu-id="057b4-131">Lorsque vous utilisez des chemins d’accès relatifs et que vous créez des liens vers d’autres ensembles de documents, il est important de définir un chemin d’accès au fichier valide pour les liens hypertexte dans votre documentation.</span><span class="sxs-lookup"><span data-stu-id="057b4-131">When using relative paths and creating links to other docsets, it is important to set a valid file path for hyperlinks in your documentation.</span></span> <span data-ttu-id="057b4-132">Votre build réussit sur GitHub uniquement si le chemin d’accès au fichier est correct ou valide.</span><span class="sxs-lookup"><span data-stu-id="057b4-132">Your build succeeds on GitHub only if the file path is correct or valid.</span></span>
 
<span data-ttu-id="057b4-133">Pour plus d’informations sur les liens hypertexte et les chemins d’accès aux fichiers, voir [les liens d’utilisation dans la documentation.](/contribute/how-to-write-links)</span><span class="sxs-lookup"><span data-stu-id="057b4-133">For more information on hyperlinks and file paths, see [use links in documentation](/contribute/how-to-write-links).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="057b4-134">Pour référencer un article qui fait **partie de l’ensemble** de documents Teams plateforme :</span><span class="sxs-lookup"><span data-stu-id="057b4-134">To reference an article that is **part of** the Teams platform docset:</span></span><br>
> <span data-ttu-id="057b4-135">&emsp;&#x2714; utiliser un chemin d’accès relatif sans barre oblique principale.</span><span class="sxs-lookup"><span data-stu-id="057b4-135">&emsp;&#x2714; Use a relative path without a leading forward slash.</span></span><br>
> <span data-ttu-id="057b4-136">&emsp;&#x2714; inclure l’extension de fichier Markdown.</span><span class="sxs-lookup"><span data-stu-id="057b4-136">&emsp;&#x2714; Include the Markdown file extension.</span></span><br>
><span data-ttu-id="057b4-137">Ex: **parent directory/directory/path-to-article.md** —> [Building an app for Microsoft Teams](../concepts/building-an-app.md)</span><span class="sxs-lookup"><span data-stu-id="057b4-137">Ex:  **parent directory/directory/path-to-article.md** —> [Building an app for Microsoft Teams](../concepts/building-an-app.md)</span></span> <br><br>
> <span data-ttu-id="057b4-138">Pour référencer un article de la bibliothèque Microsoft Docs qui ne fait **pas** partie du jeu de documents Teams plateforme microsoft :</span><span class="sxs-lookup"><span data-stu-id="057b4-138">To reference a Microsoft Docs library article that **is not part of** the Teams platform docset:</span></span><br>
> <span data-ttu-id="057b4-139">&emsp;&#x2714; utilisez un chemin d’accès relatif qui commence par une barre oblique.</span><span class="sxs-lookup"><span data-stu-id="057b4-139">&emsp;&#x2714; Use a relative path that begins with a forward slash.</span></span><br>
> <span data-ttu-id="057b4-140">&emsp;&#x2714; n’incluez pas l’extension de fichier.</span><span class="sxs-lookup"><span data-stu-id="057b4-140">&emsp;&#x2714; Do not include the file extension.</span></span> <br> <span data-ttu-id="057b4-141">Ex : **/docset/address-to-file-location** —> [l’API Microsoft Graph pour](/graph/api/resources/teams-api-overview) travailler avec Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="057b4-141">Ex:  **/docset/address-to-file-location** —> [Use the Microsoft Graph API to work with Microsoft Teams](/graph/api/resources/teams-api-overview)</span></span><br><br>
> <span data-ttu-id="057b4-142">Pour référencer une page en dehors de la bibliothèque Microsoft Docs, telle que GitHub, utilisez le chemin `https` d’accès complet du fichier.</span><span class="sxs-lookup"><span data-stu-id="057b4-142">To reference a page outside of the Microsoft Docs library, such as GitHub, use the full `https` file path.</span></span><br>

## <a name="code-samples-and-snippets"></a><span data-ttu-id="057b4-143">Exemples de code et extraits de code</span><span class="sxs-lookup"><span data-stu-id="057b4-143">Code Samples and Snippets</span></span>

<span data-ttu-id="057b4-144">Les exemples de code jouent un rôle important pour utiliser efficacement les API et les SDK.</span><span class="sxs-lookup"><span data-stu-id="057b4-144">Code samples play an important role to use APIs and SDKs effectively.</span></span> <span data-ttu-id="057b4-145">Des exemples de code bien présentés peuvent communiquer plus clairement que le texte descriptif et les informations d’instruction uniquement.</span><span class="sxs-lookup"><span data-stu-id="057b4-145">Well presented code samples can communicate how things work more clearly than descriptive text and instructional information alone.</span></span> <span data-ttu-id="057b4-146">Vos exemples de code doivent être précis, concis, bien documentés et concis et concis.</span><span class="sxs-lookup"><span data-stu-id="057b4-146">Your code samples must be accurate, concise, well documented, and reader friendly.</span></span> <span data-ttu-id="057b4-147">Le code facile à lire doit être facile à comprendre, tester, déboguer, gérer, modifier et étendre.</span><span class="sxs-lookup"><span data-stu-id="057b4-147">Code that is easy to read must be easy to understand, test, debug, maintain, modify, and extend.</span></span> <span data-ttu-id="057b4-148">Pour plus d’informations, [voir comment inclure du code dans des documents.](/contribute/code-in-docs)</span><span class="sxs-lookup"><span data-stu-id="057b4-148">For more information, see [how to include code in docs](/contribute/code-in-docs).</span></span>

## <a name="see-also"></a><span data-ttu-id="057b4-149">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="057b4-149">See also</span></span>

* [<span data-ttu-id="057b4-150">Documents Microsoft</span><span class="sxs-lookup"><span data-stu-id="057b4-150">Microsoft Docs</span></span>](/)
* [<span data-ttu-id="057b4-151">guide des collaborateurs</span><span class="sxs-lookup"><span data-stu-id="057b4-151">contributors guide</span></span>](/contribute)
* [<span data-ttu-id="057b4-152">Style docs et démarrage rapide de la voix</span><span class="sxs-lookup"><span data-stu-id="057b4-152">Docs style and voice quick start</span></span>](/contribute/style-quick-start)
* [<span data-ttu-id="057b4-153">Edge : outils de lisibilité du code source Astuces</span><span class="sxs-lookup"><span data-stu-id="057b4-153">Cutting Edge : Source Code Readability Tips</span></span>](/archive/msdn-magazine/2014/october/cutting-edge-source-code-readability-tips)
* [<span data-ttu-id="057b4-154">Teams documentation</span><span class="sxs-lookup"><span data-stu-id="057b4-154">Teams documentation</span></span>](/microsoftteams/platform/overview)
* [<span data-ttu-id="057b4-155">GitHub</span><span class="sxs-lookup"><span data-stu-id="057b4-155">GitHub</span></span>](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform)


## <a name="next-step"></a><span data-ttu-id="057b4-156">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="057b4-156">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="057b4-157">Obtenir les mises à jour de Microsoft Docs et les dernières annonces</span><span class="sxs-lookup"><span data-stu-id="057b4-157">Get Microsoft Docs updates and the latest announcements</span></span>](/teamblog)
