---
title: Documentation de Microsoft teams
description: étapes de création et de publication de la documentation des équipes
author: laujan
ms.author: lajanuar
ms.topic: contributor-guide
ms.openlocfilehash: 80aaf7795a226c0437140fe72e1d74b07fa66775
ms.sourcegitcommit: f6029c8ff0c5315613a3efcd86777aa4cede39e6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/11/2020
ms.locfileid: "48995015"
---
# <a name="contributing-to-microsoft-teams-documentation"></a>Documentation de Microsoft teams

La [documentation de teams](/microsoftteams/platform/overview) fait partie de la bibliothèque de documentation technique [Microsoft docs](https://docs.microsoft.com/) . Le contenu est organisé en groupes appelés docsets, chacun représentant un groupe de documents connexes gérés en tant qu’entité unique. Les articles du même docset ont la même extension de chemin d’URL après *docs <span></span> . Microsoft.com*.  Par exemple,  `/docs.microsoft.com/microsoftteams/...`   est le début du chemin d’accès au fichier docset Teams. Les Articles de teams sont écrits dans la syntaxe de  [démarque](#markdown-reference) et hébergés sur [GitHub](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform).

## <a name="set-up-your-workspace"></a>Configurer votre espace de travail

> [!div class="checklist"]
>
> * Installez [git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).
> * Installez [Visual Studio code](https://code.visualstudio.com/) (vs code).
> * Installer le [Pack de création de docs](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) directement à partir du vs code Marketplace
<br>&emsp;&emsp; des

> [!div class="checklist"]
>
> * Installez à partir du code VS :

   1. Sélectionnez l' **icône extensions** sur la barre d’activité latérale ou utilisez la commande **Afficher => les extensions** (Ctrl + Maj + X) et recherchez le *Pack de création docs* (Microsoft).
   1. Sélectionnez le bouton **installer** .
   1. Une fois l’installation terminée, le bouton **installer** prend la forme du bouton **gérer** les engrenages.

## <a name="review-the-microsoft-docs-contributors-guide"></a>Consulter le guide des contributeurs Microsoft docs

Le [Guide sur les contributeurs](/contribute) offre une direction pour la création, la publication et la mise à jour de contenu technique sur Microsoft/docs. *Voir aussi* , [style docs et démarrage rapide de la voix](/contribute/style-quick-start) .

## <a name="microsoft-writing-style-and-content-guides"></a>Guides de rédaction, de style et de contenu Microsoft

* **[Guide de style d’écriture Microsoft](/style-guide/welcome)**. Envisagez d’ajouter ce guide en ligne au menu **favoris** de votre navigateur. Il s’agit d’une ressource complète pour la rédaction technique d’aujourd’hui et reflète l’approche moderne de Microsoft en matière de voix et de style.

* **[Rédaction de contenu de développeur](/style-guide/developer-content/)**. Le contenu spécifique à teams est destiné aux développeurs, avec une compréhension fondamentale des concepts et des processus de programmation. Il est important de fournir des informations claires et précises de façon attrayante tout en maintenant la tonalité et le style de Microsoft.

* **[Écriture d’instructions pas à pas](/style-guide/procedures-instructions/writing-step-by-step-instructions)**. Les expériences appliquées et interactives permettent aux développeurs d’en savoir plus sur les produits et technologies Microsoft. La présentation de procédures complexes ou simples dans un format progressif est naturelle et conviviale.

## <a name="markdown-reference"></a>Référence de la démarque

 Les pages Microsoft docs sont écrites dans la syntaxe de démarque et sont analysées via un moteur [Markdig](https://github.com/lunet-io/markdig) . *Consultez la rubrique* [docs de référence](/contribute/markdown-reference) pour les balises et les conventions de mise en forme spécifiques.

## <a name="file-paths"></a>Chemins d’accès aux fichiers

La définition d’un chemin d’accès de fichier valide pour les liens hypertexte dans votre documentation peut être un problème, en particulier lorsque vous utilisez des chemins d’accès relatifs et que vous créez des liens vers d’autres docsets.  Votre génération ne réussit pas sur GitHub si le chemin d’accès au fichier est incorrect ou non valide.

Pour plus d’informations sur les liens hypertexte et les chemins d’accès aux fichiers, *reportez-vous* [à la rubrique utiliser des liens dans la documentation](/contribute/how-to-write-links).

>[!IMPORTANT]
> Pour référencer un article qui fait *partie de* la plateforme teams docset :<br>
> &emsp;&#x2714; utiliser un chemin d’accès relatif sans barre oblique de début.<br>
> &emsp;&#x2714; inclure l’extension du fichier de démarques.<br>
>Ex :  **répertoire parent/répertoire/chemin d’accès-à-article. MD** — > `[Building an app for Microsoft Teams](../concepts/building-an-app.md)` <br><br>
> Pour référencer un article de bibliothèque Microsoft docs ( <https://docs.microsoft.com/> ) qui *ne fait pas partie de* la plateforme teams docset, procédez comme suit :<br>
> &emsp;&#x2714; utiliser un chemin d’accès relatif qui commence par une barre oblique.<br>
> &emsp;&#x2714; n’incluez pas l’extension de fichier. <br> Ex :  **/docset/Address-to-file-location** — > `[Use the Microsoft Graph API to work with Microsoft Teams](/graph/api/resources/teams-api-overview)`
>

## <a name="code-samples-and-snippets"></a>Exemples de code et extraits de code

Les exemples de code jouent un rôle important dans la façon d’aider les développeurs à utiliser correctement les API et les SDK. Les exemples de code bien présentés peuvent communiquer de façon plus claire que le texte descriptif et des informations pédagogiques. Vos exemples de code doivent être précis, concis, bien documentés et, plus important encore, compatibles avec les lecteurs. Le code facile à lire est également facile à comprendre, de tester, de déboguer, de tenir à jour, de modifier et d’étendre. *Consultez la rubrique* [How to include code in docs](/contribute/code-in-docs). Pour obtenir des conseils de lisibilité, *reportez-vous également à la section* [Cutting Edge : conseils de lisibilité de code source](/archive/msdn-magazine/2014/october/cutting-edge-source-code-readability-tips).

> [!div class="nextstepaction"]
> [Obtenir les mises à jour de Microsoft Docs et les dernières annonces](/teamblog)
