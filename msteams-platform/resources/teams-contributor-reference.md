---
title: Contribuer à la documentation Microsoft Teams’œil
description: étapes de création et de publication Teams documentation
author: laujan
ms.author: lajanuar
localization_priority: Normal
ms.topic: contributor-guide
ms.openlocfilehash: 52253bb096857e2cb883295c8ae6b58518506d9a
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566228"
---
# <a name="contributing-to-microsoft-teams-documentation"></a>Contribuer à la documentation Microsoft Teams’œil

[Teams documentation fait](/microsoftteams/platform/overview) partie de la bibliothèque de documentation technique Microsoft [Docs.](https://docs.microsoft.com/) Le contenu est organisé en groupes appelés docsets, chacun représentant un groupe de documents connexes gérés en une seule entité. Les articles dans le même docset ont la même extension de chemin URL *après docs <span></span> .microsoft.com*.  Par exemple, `/docs.microsoft.com/microsoftteams/...` c’est le début de la Teams de fichier docset. Teams articles sont écrits dans [la syntaxe MarkDown](#markdown-reference) et hébergés [sur GitHub](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform).

## <a name="set-up-your-workspace"></a>Configurez votre espace de travail

> [!div class="checklist"]
>
> * Installer [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).
> * Installez [Visual Studio Code](https://code.visualstudio.com/) (VS Code).
> * Installez [docs Authoring Pack](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) directement à partir du VS Code Marketplace.
<br>&emsp;&emsp; ou

> [!div class="checklist"]
>
> * Installez de l’intérieur VS Code :

   1. Sélectionnez **l’icône Extensions** sur la barre d’activité latérale ou utilisez **la commande Afficher => Extensions** (Ctrl+Shift+X) et recherchez le pack *d’auteur docs* (Microsoft).
   1. Sélectionnez le **bouton** Installer.
   1. Une fois l’installation terminée, **le bouton** Installer passera au bouton **Gérer les** vitesses.

## <a name="review-the-microsoft-docs-contributors-guide"></a>Publier un avis sur le Guide des contributeurs microsoft docs

Le [guide des contributeurs offre](/contribute) des orientations pour la création, la publication et la mise à jour du contenu technique sur la plate-forme Microsoft Docs.

## <a name="microsoft-writing-style-and-content-guides"></a>Guides microsoft d’écriture, de style et de contenu

* **[Guide de style d’écriture Microsoft](/style-guide/welcome)**. Envisagez d’ajouter ce guide en ligne au menu **Favoris de votre** navigateur. Il s’agit d’une ressource complète pour l’écriture technique d’aujourd’hui et reflète l’approche moderne de Microsoft à la voix et le style.

* **[Rédaction de contenu développeur](/style-guide/developer-content/)**. Teams spécifique est destiné à un public de développeurs ayant une compréhension fondamentale des concepts et des processus de programmation. Il est important que vous fournissez des informations claires et techniquement exactes d’une manière convaincante tout en maintenant le ton et le style de Microsoft.

* **[Rédaction d’instructions étape par étape](/style-guide/procedures-instructions/writing-step-by-step-instructions)**. Les expériences appliquées et interactives sont un excellent moyen pour les développeurs d’en apprendre davantage sur les produits et technologies Microsoft. Présenter des procédures complexes ou simples dans un format progressif est naturel et convivial.

## <a name="markdown-reference"></a>Référence MarkDown

 Les pages Microsoft Docs sont écrites dans la syntaxe MarkDown et paresed via [un moteur Markdig.](https://github.com/lunet-io/markdig) Veuillez *consulter la* référence [Docs Markdown pour les](/contribute/markdown-reference) balises spécifiques et les conventions de mise en forme.

## <a name="file-paths"></a>Chemins de fichiers

Définir un chemin de fichiers valide pour les hyperliens dans votre documentation peut être un défi, en particulier lorsque vous utilisez des chemins relatifs et créez des liens vers d’autres ensembles de documents.  Votre build ne réussira pas sur GitHub le chemin de fichier est incorrect ou invalide.

Pour plus d’informations sur les hyperliens et les chemins de fichiers, voir [Utilisez des liens dans la documentation](/contribute/how-to-write-links).

>[!IMPORTANT]
> Pour référencer un article qui fait *partie de la* plate-forme Teams docset:<br>
> &emsp;&#x2714; un chemin relatif sans barre oblique avant de premier plan.<br>
> &emsp;&#x2714; l’extension de fichier Markdown.<br>
>Ex :  **répertoire/annuaire des parents/chemin vers l’article.md** — > `[Building an app for Microsoft Teams](../concepts/building-an-app.md)` <br><br>
> Pour référencer un article de la bibliothèque Microsoft Docs *qui ne fait pas partie de* la Teams de la plateforme docset :<br>
> &emsp;&#x2714; un chemin relatif qui commence par une barre oblique avant.<br>
> &emsp;&#x2714; n’incluez pas l’extension de fichier. <br> Ex :  **/docset/adresse-à-file-location** —> `[Use the Microsoft Graph API to work with Microsoft Teams](/graph/api/resources/teams-api-overview)`<br><br>
> Pour référencer une page en dehors de la bibliothèque Microsoft Docs, comme GitHub, utilisez le chemin de `https` fichier complet.<br>

## <a name="code-samples-and-snippets"></a>Échantillons de code et extraits

Les échantillons de code jouent un rôle important en aidant les développeurs à utiliser avec succès les API et les SDK. Des échantillons de code bien présentés peuvent communiquer comment les choses fonctionnent plus clairement que le texte descriptif et l’information pédagogique seule. Vos échantillons de code doivent être précis, concis, bien documentés et, surtout, adaptés aux lecteurs. Le code facile à lire est également facile à comprendre, à tester, à déboger, à maintenir, à modifier et à étendre. Pour plus d’informations, [voir Comment inclure du code dans les documents](/contribute/code-in-docs).

## <a name="see-also"></a>Voir aussi

* [Docs style et la voix de démarrage rapide](/contribute/style-quick-start)
* [Tranchant : Source Code Readability Astuces](/archive/msdn-magazine/2014/october/cutting-edge-source-code-readability-tips).

> [!div class="nextstepaction"]
> [Obtenez les mises à jour microsoft docs et les dernières annonces](/teamblog)
