---
title: Contribuer à la documentation Teams
description: étapes de création et de publication de la documentation Teams
author: surbhigupta
ms.author: lajanuar
ms.localizationpriority: high
ms.topic: contributor-guide
ms.openlocfilehash: 480b8bc1692672023171f3b6e67e0ee526cbe509
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111898"
---
# <a name="contribute-to-teams-documentation"></a>Contribuer à la documentation Teams

La documentation Teams fait partie de la bibliothèque de documentation technique **Microsoft Docs** . Le contenu est organisé en groupes appelés docsets, chacun représentant un groupe de documents associés gérés en tant qu’entité unique. Les articles du même docset ont la même extension de chemin d’URL après **docs.microsoft.com**. Par exemple, `/docs.microsoft.com/microsoftteams/...` est le début du chemin du fichier docset Teams. Les articles Teams sont écrits dans la syntaxe Markdown et hébergés sur GitHub.

## <a name="set-up-your-workspace"></a>Configurer votre espace de travail

> [!div class="checklist"]
>
> * Installez [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).
> * Installez [Microsoft Visual Studio code](https://code.visualstudio.com/) (VS Code).
> * Installez [docs Authoring Pack](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) directement à partir de la place de marché VS Code.
<br>&emsp;&emsp; ou
> [!div class="checklist"]
>
> * Installer dans VS Code :

   1. Sélectionnez l’icône **Extensions** dans la barre d’activité latérale ou utilisez la commande **View => Extensions** ou Ctrl+Maj+X et recherchez **Microsoft Docs** de pack de création.
   1. Sélectionnez **Installer**.
   1. Après l’installation, l'**Installer** passe au bouton d’engrenage **Gérer** .

## <a name="review-the-microsoft-docs-contributors-guide"></a>Consulter le Guide des contributeurs Microsoft Docs

Le guide des contributeurs fournit des instructions pour créer, publier et mettre à jour du contenu technique sur la plateforme **Microsoft Docs** .

## <a name="microsoft-writing-style-and-content-guides"></a>Guides d’écriture, de style et de contenu Microsoft

* **[guide de style d’écriture Microsoft](/style-guide/welcome)**: le Guide de style d’écriture Microsoft est une ressource complète pour l’écriture technique et reflète l’approche moderne de Microsoft en matière de voix et de style. Pour des informations de référence simples, ajoutez ce guide en ligne au menu **favoris** de votre navigateur.

* **[Écriture de contenu pour les développeurs](/style-guide/developer-content/)**: le contenu spécifique à Teams s’adresse à un public de développeurs ayant une compréhension fondamentale des concepts de programmation et des processus. Il est important de fournir des informations claires et techniques précises de manière attrayante tout en conservant le ton et le style de Microsoft.

* **[écrire des instructions pas à pas](/style-guide/procedures-instructions/writing-step-by-step-instructions)**: les expériences appliquées et interactives sont un excellent moyen pour les développeurs d’en savoir plus sur les produits et technologies Microsoft. La présentation de procédures complexes ou simples dans un format progressif est naturelle et conviviale.

## <a name="markdown-reference"></a>Informations de référence sur MarkDown

**Microsoft Docs** pages sont écrites dans **syntaxe** MarkDown et analysées à l’aide d’un moteur de [Markdig](https://github.com/lunet-io/markdig). Pour plus d’informations sur des balises et des conventions de mise en forme spécifiques, consultez [référence Docs Markdown](/contribute/markdown-reference).

## <a name="file-paths"></a>Chemins d’accès

Lorsque vous utilisez des chemins relatifs et créez des liens vers d’autres documents, il est important de définir un chemin d’accès de fichier valide pour les liens hypertexte dans votre documentation. Votre build réussit sur GitHub uniquement si le chemin d’accès au fichier est correct ou valide.

Pour plus d’informations sur les liens hypertexte et les chemins d’accès aux fichiers, consultez [utiliser des liens dans la documentation](/contribute/how-to-write-links).

> [!IMPORTANT]
> Pour référencer un article qui fait **partie de** la documentation de la plateforme Teams :<br>
> &emsp;&#x2714; Utilisez un chemin d’accès relatif sans barre oblique de début.<br>
> &emsp;&#x2714; Incluez l’extension de fichier Markdown.<br>
>Par exemple : **répertoire parent/répertoire/chemin d’accès à article.md**—> [Création d’une application pour Microsoft Teams](../concepts/building-an-app.md) <br><br>
> Pour référencer un article de bibliothèque Microsoft Docs qui **ne fait pas partie de** la documentation de la plateforme Teams :<br>
> &emsp;&#x2714; Utilisez un chemin relatif qui commence par une barre oblique.<br>
> &emsp;&#x2714; N’incluez pas l’extension de fichier. <br>
> Par exemple : **/docset/address-to-file-location**> [—Utiliser l’API Microsoft Graph pour travailler avec Microsoft Teams](/graph/api/resources/teams-api-overview)<br><br>
> Pour référencer une page en dehors de la bibliothèque Microsoft Docs, telle que GitHub, utilisez le chemin d’accès complet `https` fichier.<br>

## <a name="code-samples-and-snippets"></a>Exemples de code et extraits de code

Les exemples de code jouent un rôle important pour utiliser efficacement les API et les Kits de développement logiciel (SDK). Des exemples de code bien présentés peuvent communiquer plus clairement le fonctionnement des éléments que le texte descriptif et les informations d’instruction seuls. Vos exemples de code doivent être précis, concis, bien documentés et conviviaux. Le code facile à lire doit être facile à comprendre, tester, déboguer, gérer, modifier et étendre. Pour plus d’informations, consultez [comment inclure du code dans la documentation](/contribute/code-in-docs).

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [obtenir Microsoft Docs mises à jour et les dernières annonces](/teamblog)

## <a name="see-also"></a>Voir aussi

* [Microsoft Docs](/)
* [Guide des contributeurs](/contribute)
* [style docs et de démarrage rapide de la voix](/contribute/style-quick-start)
* [À la pointe du progrès : conseils pour la lisibilité du code source ](/archive/msdn-magazine/2014/october/cutting-edge-source-code-readability-tips)
* [Documentation Teams](/microsoftteams/platform/overview)
* [GitHub](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform)
