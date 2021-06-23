---
title: Contribution à la Microsoft Teams documentation
description: étapes de création et de publication de Teams documentation
author: surbhigupta
ms.author: lajanuar
localization_priority: Normal
ms.topic: contributor-guide
ms.openlocfilehash: 33296219b9d42b2ca26eb3c44df5c6429f5259ce
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069162"
---
# <a name="contributing-to-microsoft-teams-documentation"></a>Contribution à la Microsoft Teams documentation

[Teams documentation technique](/microsoftteams/platform/overview) fait partie de la bibliothèque de documentation technique [Microsoft Docs.](https://docs.microsoft.com) Le contenu est organisé en groupes appelés ensembles de documents, chacun représentant un groupe de documents associés gérés en tant qu’entité unique. Les articles du même ensemble de documents ont la même extension de chemin d’URL après les *documents <span></span> .microsoft.com*.  Par exemple, `/docs.microsoft.com/microsoftteams/...` est le début du chemin d Teams fichier docset. Teams articles sont écrits en syntaxe [MarkDown](#markdown-reference) et hébergés [sur GitHub](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform).

## <a name="set-up-your-workspace"></a>Configurer votre espace de travail

> [!div class="checklist"]
>
> * Installez [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).
> * Installez [Visual Studio Code](https://code.visualstudio.com/) (VS Code).
> * Installez [docs Authoring Pack](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) directement à partir de VS Code Marketplace.
<br>&emsp;&emsp; ou

> [!div class="checklist"]
>
> * Installez à partir de VS Code :

   1. Sélectionnez l’icône **Extensions** dans la barre d’activité latéral ou utilisez la commande Afficher **=> Extensions** (Ctrl+Shift+X) et recherchez le pack de génération de documents *(Microsoft).*
   1. Sélectionnez le **bouton** Installer.
   1. Une fois l’installation terminée, le bouton **Installer** se change **en** bouton Gérer l’engrenage.

## <a name="review-the-microsoft-docs-contributors-guide"></a>Consulter le Guide des contributeurs Microsoft Docs

Le guide des collaborateurs fournit des [instructions](/contribute) pour la création, la publication et la mise à jour de contenu technique sur la plateforme Microsoft Docs.

## <a name="microsoft-writing-style-and-content-guides"></a>Guides d’écriture, de style et de contenu Microsoft

* **[Guide de style d’écriture Microsoft](/style-guide/welcome)**. Envisagez d’ajouter ce guide en ligne au menu **Favoris de votre** navigateur. Il s’agit d’une ressource complète pour la rédaction technique d’aujourd’hui et reflète l’approche moderne de Microsoft en matière de voix et de style.

* **[Écriture de contenu de développeur.](/style-guide/developer-content/)** Teams contenu spécifique est destiné à un public de développeurs ayant une compréhension fondamentale des concepts et processus de programmation. Il est important que vous fournissiez des informations claires et techniques précises de manière attrayante tout en conservant le style et le ton de Microsoft.

* **[Écriture d’instructions pas à pas.](/style-guide/procedures-instructions/writing-step-by-step-instructions)** Les expériences appliquées et interactives sont un excellent moyen pour les développeurs d’en savoir plus sur les produits et technologies Microsoft. La présentation de procédures complexes ou simples dans un format progressif est naturelle et conviviale.

## <a name="markdown-reference"></a>Référence MarkDown

 Les pages Microsoft Docs sont écrites dans la syntaxe MarkDown et sont par le biais [d’un moteur Markdig.](https://github.com/lunet-io/markdig) Veuillez *consulter la* référence [Docs Markdown](/contribute/markdown-reference) pour des balises et des conventions de mise en forme spécifiques.

## <a name="file-paths"></a>Chemins d’accès aux fichiers

La définition d’un chemin d’accès de fichier valide pour les liens hypertexte dans votre documentation peut être difficile, en particulier lorsque vous utilisez des chemins d’accès relatifs et créez des liens vers d’autres jeux de documents.  Votre build ne réussira pas GitHub si le chemin d’accès du fichier est incorrect ou non valide.

Pour plus d’informations sur les liens hypertexte et les chemins d’accès aux fichiers, voir [Utiliser des liens dans la documentation.](/contribute/how-to-write-links)

>[!IMPORTANT]
> Pour référencer un article qui fait *partie de l’ensemble* de documents Teams plateforme :<br>
> &emsp;&#x2714; utiliser un chemin d’accès relatif sans barre oblique principale.<br>
> &emsp;&#x2714; inclure l’extension de fichier Markdown.<br>
>Ex :  **répertoire parent/répertoire/chemin d’accès à article.md** —> `[Building an app for Microsoft Teams](../concepts/building-an-app.md)` <br><br>
> Pour référencer un article de la bibliothèque Microsoft Docs qui ne fait *pas* partie du jeu de documents Teams plateforme microsoft :<br>
> &emsp;&#x2714; utilisez un chemin d’accès relatif qui commence par une barre oblique.<br>
> &emsp;&#x2714; n’incluez pas l’extension de fichier. <br> Ex :  **/docset/address-to-file-location** —> `[Use the Microsoft Graph API to work with Microsoft Teams](/graph/api/resources/teams-api-overview)`<br><br>
> Pour référencer une page en dehors de la bibliothèque Microsoft Docs, telle que GitHub, utilisez le chemin `https` d’accès complet du fichier.<br>

## <a name="code-samples-and-snippets"></a>Exemples de code et extraits de code

Les exemples de code jouent un rôle important pour aider les développeurs à utiliser correctement les API et les SDK. Des exemples de code bien présentés peuvent communiquer le fonctionnement plus clairement que le texte descriptif et les informations d’instruction uniquement. Vos exemples de code doivent être précis, concis, bien documentés et, plus important encore, concis et concis. Le code facile à lire est également facile à comprendre, tester, déboguer, gérer, modifier et étendre. Pour plus d’informations, [voir Comment inclure du code dans des documents](/contribute/code-in-docs).

## <a name="see-also"></a>Voir aussi

* [Style docs et démarrage rapide de la voix](/contribute/style-quick-start)
* [Découpage : outil de lisibilité du code source Astuces](/archive/msdn-magazine/2014/october/cutting-edge-source-code-readability-tips).

> [!div class="nextstepaction"]
> [Obtenir les mises à jour de Microsoft Docs et les dernières annonces](/teamblog)
