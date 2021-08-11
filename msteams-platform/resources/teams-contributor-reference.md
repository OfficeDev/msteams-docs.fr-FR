---
title: Contribuer à la documentation Teams
description: étapes de création et de publication de Teams documentation
author: surbhigupta
ms.author: lajanuar
localization_priority: Normal
ms.topic: contributor-guide
ms.openlocfilehash: d09f946926f7377b65910c7bccce7cef8e30ef739afa31b94c83354cffbd7c27
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/07/2021
ms.locfileid: "57708055"
---
# <a name="contribute-to-teams-documentation"></a>Contribuer à la documentation Teams

Teams documentation technique fait partie de la bibliothèque de documentation technique **Microsoft Docs.** Le contenu est organisé en groupes appelés jeux de documents, chacun représentant un groupe de documents associés gérés en tant qu’entité unique. Les articles du même ensemble de documents ont la même extension de chemin d’URL **docs.microsoft.com**. Par exemple, `/docs.microsoft.com/microsoftteams/...` est le début du chemin d Teams fichier docset. Teams articles sont écrits en syntaxe Markdown et hébergés sur GitHub.

## <a name="set-up-your-workspace"></a>Configurer votre espace de travail

> [!div class="checklist"]
>
> * Installez [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).
> * Installez [Visual Studio Code](https://code.visualstudio.com/) (VS Code).
> * Installez [docs Authoring Pack](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) directement à partir de VS Code Marketplace.
<br>&emsp;&emsp; ou

> [!div class="checklist"]
>
> * Installez dans VS Code :

   1. Sélectionnez l’icône **Extensions** dans la barre d’activité latérale ou utilisez la commande **View => Extensions** ou Ctrl+Shift+X et recherchez **Microsoft Docs Authoring Pack**.
   1. Sélectionnez **Installer**.
   1. Après l’installation, **l’installation** est apportée au **bouton Gérer** l’engrenage.

## <a name="review-the-microsoft-docs-contributors-guide"></a>Consulter le Guide des contributeurs de documents Microsoft

Le guide des collaborateurs fournit des instructions pour créer, publier et mettre à jour du contenu technique sur la **plateforme Microsoft Docs.** 

## <a name="microsoft-writing-style-and-content-guides"></a>Guides d’écriture, de style et de contenu Microsoft

* **[Guide de style d’écriture Microsoft](/style-guide/welcome)**: le Guide de style d’écriture Microsoft est une ressource complète pour l’écriture technique et reflète l’approche moderne de Microsoft en matière de voix et de style. Pour faciliter la référence, ajoutez ce guide en ligne au menu **Favoris de votre** navigateur.

* **[Écriture de contenu développeur](/style-guide/developer-content/)**: Teams contenu spécifique est destiné à un public de développeurs ayant une compréhension fondamentale des concepts et processus de programmation. Il est important que vous fournissiez des informations claires et techniques précises de manière attrayante tout en conservant le style et le ton de Microsoft.

* **[Écriture d’instructions pas à pas](/style-guide/procedures-instructions/writing-step-by-step-instructions)**: les expériences appliquées et interactives sont un excellent moyen pour les développeurs d’en savoir plus sur les produits et technologies Microsoft. La présentation de procédures complexes ou simples dans un format progressif est naturelle et conviviale.

## <a name="markdown-reference"></a>Référence MarkDown

Les pages **Microsoft Docs** sont écrites dans la syntaxe **MarkDown** et sont par le biais d’un [moteur Markdig.](https://github.com/lunet-io/markdig) Pour plus d’informations sur des balises et des conventions de mise en forme spécifiques, voir [référence Docs Markdown](/contribute/markdown-reference).

## <a name="file-paths"></a>Chemins d’accès aux fichiers

Lorsque vous utilisez des chemins d’accès relatifs et que vous créez des liens vers d’autres ensembles de documents, il est important de définir un chemin d’accès au fichier valide pour les liens hypertexte dans votre documentation. Votre build réussit sur GitHub uniquement si le chemin d’accès au fichier est correct ou valide.
 
Pour plus d’informations sur les liens hypertexte et les chemins d’accès aux fichiers, voir [les liens d’utilisation dans la documentation.](/contribute/how-to-write-links)

> [!IMPORTANT]
> Pour référencer un article qui fait **partie de l’ensemble** de documents Teams plateforme :<br>
> &emsp;&#x2714; utiliser un chemin d’accès relatif sans barre oblique principale.<br>
> &emsp;&#x2714; inclure l’extension de fichier Markdown.<br>
>Ex: **parent directory/directory/path-to-article.md** —> [Building an app for Microsoft Teams](../concepts/building-an-app.md) <br><br>
> Pour référencer un article de la bibliothèque Microsoft Docs qui ne fait **pas** partie du document Teams plateforme microsoft :<br>
> &emsp;&#x2714; utilisez un chemin d’accès relatif qui commence par une barre oblique.<br>
> &emsp;&#x2714; n’incluez pas l’extension de fichier. <br> Ex : **/docset/address-to-file-location** —> [l’API Microsoft Graph pour](/graph/api/resources/teams-api-overview) travailler avec Microsoft Teams<br><br>
> Pour référencer une page en dehors de la bibliothèque Microsoft Docs, telle que GitHub, utilisez le chemin `https` d’accès complet du fichier.<br>

## <a name="code-samples-and-snippets"></a>Exemples de code et extraits de code

Les exemples de code jouent un rôle important pour utiliser efficacement les API et les SDK. Des exemples de code bien présentés peuvent communiquer plus clairement que le texte descriptif et les informations d’instruction uniquement. Vos exemples de code doivent être précis, concis, bien documentés et concis et concis. Le code facile à lire doit être facile à comprendre, tester, déboguer, gérer, modifier et étendre. Pour plus d’informations, [voir comment inclure du code dans des documents.](/contribute/code-in-docs)

## <a name="see-also"></a>Voir aussi

* [Documents Microsoft](/)
* [guide des collaborateurs](/contribute)
* [Style docs et démarrage rapide de la voix](/contribute/style-quick-start)
* [Edge : outils de lisibilité du code source Astuces](/archive/msdn-magazine/2014/october/cutting-edge-source-code-readability-tips)
* [Teams documentation](/microsoftteams/platform/overview)
* [GitHub](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform)


## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Obtenir les mises à jour de Microsoft Docs et les dernières annonces](/teamblog)
