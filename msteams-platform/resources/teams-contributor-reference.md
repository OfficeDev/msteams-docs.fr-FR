---
title: Contribuer à la documentation Teams
description: Découvrir les étapes de création et de publication de la documentation Teams
author: surbhigupta
ms.author: lajanuar
ms.localizationpriority: medium
ms.topic: contributor-guide
ms.openlocfilehash: 4a0c522b5e9d4bcf99ee884de41b1d75846b004a
ms.sourcegitcommit: 377a4b712b50a211851aeecc1029414939945390
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2022
ms.locfileid: "68044664"
---
# <a name="contribute-to-teams-documentation"></a>Contribuer à la documentation Teams

La documentation Teams fait partie de la bibliothèque de documentation technique **Microsoft Learn** . Le contenu est organisé en groupes appelés docsets, chacun représentant un groupe de documents associés gérés en tant qu’entité unique. Les articles du même docset ont la même extension de chemin d’URL après `learn.microsoft.com`. Par exemple, `/learn.microsoft.com/microsoftteams/...` est le début du chemin du fichier docset Teams. Les articles Teams sont écrits dans la syntaxe Markdown et hébergés sur GitHub.

## <a name="set-up-your-workspace"></a>Configurer votre espace de travail

> [!div class="checklist"]
>
> * Installez [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).
> * Installez [Microsoft Visual Studio code](https://code.visualstudio.com/) (VS Code).
> * Install [Docs Authoring Pack](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) directly from the VS Code Marketplace.
<br>&emsp;&emsp; ou
> [!div class="checklist"]
>
> * Installer dans VS Code :

   1. Sélectionnez **l’icône Extensions** dans la barre d’activité latérale ou utilisez la commande **Affichage => Extensions** ou Ctrl+Maj+X, puis recherchez **docs Authoring Pack**.
   1. Sélectionnez **Installer**.
   1. Après l’installation, l'**Installer** passe au bouton d’engrenage **Gérer** .

## <a name="review-the-microsoft-docs-contributor-guide"></a>Consultez le guide du contributeur Microsoft Docs

Le guide des contributeurs fournit des instructions pour créer, publier et mettre à jour du contenu technique sur la plateforme **Microsoft Learn** .

## <a name="microsoft-writing-style-and-content-guides"></a>Guides d’écriture, de style et de contenu Microsoft

* **[guide de style d’écriture Microsoft](/style-guide/welcome)**: le Guide de style d’écriture Microsoft est une ressource complète pour l’écriture technique et reflète l’approche moderne de Microsoft en matière de voix et de style. Pour des informations de référence simples, ajoutez ce guide en ligne au menu **favoris** de votre navigateur.

* **[Écriture de contenu pour les développeurs](/style-guide/developer-content/)**: le contenu spécifique à Teams s’adresse à un public de développeurs ayant une compréhension fondamentale des concepts de programmation et des processus. Il est important que vous deviez fournir des informations claires et techniquesment précises de manière convaincante tout en conservant le ton et le style de Microsoft.

* **[écrire des instructions pas à pas](/style-guide/procedures-instructions/writing-step-by-step-instructions)**: les expériences appliquées et interactives sont un excellent moyen pour les développeurs d’en savoir plus sur les produits et technologies Microsoft. La présentation de procédures complexes ou simples dans un format progressif est naturelle et conviviale.

## <a name="markdown-reference"></a>Informations de référence sur MarkDown

Les pages **Microsoft Learn** sont écrites dans la syntaxe **MarkDown** et analysées via un moteur [Markdig](https://github.com/lunet-io/markdig). Pour plus d’informations sur des balises et des conventions de mise en forme spécifiques, consultez [référence Docs Markdown](/contribute/markdown-reference).

## <a name="file-paths"></a>Chemins d’accès

Lorsque vous utilisez des chemins relatifs et créez des liens vers d’autres docsets, il est important de définir un chemin d’accès de fichier valide pour les liens hypertexte dans votre documentation. Votre build réussit sur GitHub uniquement si le chemin d’accès au fichier est correct ou valide.

Pour plus d’informations sur les liens hypertexte et les chemins d’accès aux fichiers, consultez [utiliser des liens dans la documentation](/contribute/how-to-write-links).

> [!IMPORTANT]
> Pour référencer un article qui fait **partie de** la documentation de la plateforme Teams :<br>
> &emsp;&#x2714; Utilisez un chemin d’accès relatif sans barre oblique de début.<br>
> &emsp;&#x2714; Incluez l’extension de fichier Markdown.<br>
>Par exemple : **répertoire parent/répertoire/chemin d’accès à article.md**—> [Création d’une application pour Microsoft Teams](../concepts/building-an-app.md) <br><br>
> Pour référencer un article Microsoft Learn qui **ne fait pas partie du document de** la plateforme Teams :<br>
> &emsp;&#x2714; Utilisez un chemin relatif qui commence par une barre oblique.<br>
> &emsp;&#x2714; Do not include the file extension. <br>
> Par exemple : **/docset/address-to-file-location**> [—Utiliser l’API Microsoft Graph pour travailler avec Microsoft Teams](/graph/api/resources/teams-api-overview)<br><br>
> Pour référencer une page en dehors de Microsoft Learn, telle que GitHub, utilisez le chemin d’accès complet `https` du fichier.<br>

## <a name="code-samples-and-snippets"></a>Exemples de code et extraits de code

Les exemples de code jouent un rôle important pour utiliser efficacement les API et les Kits de développement logiciel (SDK). Des exemples de code bien présentés peuvent communiquer plus clairement le fonctionnement des éléments que le texte descriptif et les informations d’instruction seuls. Vos exemples de code doivent être précis, concis, bien documentés et conviviaux. Le code facile à lire doit être facile à comprendre, tester, déboguer, gérer, modifier et étendre. Pour plus d’informations, voir [comment inclure du code dans un article](/contribute/code-in-docs).

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Obtenir les mises à jour microsoft Learn et les dernières annonces](/teamblog)

## <a name="see-also"></a>Voir aussi

* [Microsoft Learn](/)
* [Guide du contributeur de la documentation Microsoft Learn](/contribute)
* [Démarrage rapide sur le style et la voix de Microsoft Learn](/contribute/style-quick-start)
* [À la pointe du progrès : conseils pour la lisibilité du code source ](/archive/msdn-magazine/2014/october/cutting-edge-source-code-readability-tips)
* [Documentation Teams](/microsoftteams/platform/overview)
* [GitHub](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform)
