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
# <a name="adding-a-microsoft-teams-tab-in-sharepoint-as-an-spfx-web-part"></a>Ajout d’un onglet Microsoft Teams dans SharePoint en tant que partie Web SPFx

## <a name="rich-integration-between-teams-and-sharepoint"></a>Intégration enrichie entre Teams et SharePoint

Avec la version de novembre de Teams et SharePoint Framework v. 1.7, les développeurs ont deux fonctionnalités puissantes :

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
                        <h3>Onglets Teams dans SharePoint</h3>
                        <p>Créez des expériences d’application enrichies dans SharePoint en apportant votre application Teams dans SharePoint (cet article).</p>
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
                        <h3>SharePoint Framework dans Teams</h3>
                        <p>Apportez vos composants Web Parts SharePoint à Teams et laissez SharePoint gérer l’hébergement pour vous.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

### <a name="teams-tabs-in-sharepoint"></a>Onglets Teams dans SharePoint

Avec SharePoint Framework v.1.7, nous prenons désormais en charge la possibilité pour les développeurs de prendre leurs onglets Teams et de les héberger dans SharePoint. Comme les onglets hébergés dans SharePoint obtiennent une expérience de « page entière » similaire, en exposant toutes les fonctionnalités des onglets Teams tout en conservant le contexte et la familiarité d’un site SharePoint.

### <a name="sharepoint-framework-in-teams"></a>SharePoint Framework dans Teams

Vous pouvez également implémenter vos onglets Microsoft Teams à l’aide de SharePoint Framework. Pour les développeurs SharePoint, cela simplifie considérablement le processus de développement pour les onglets Teams, car les composants Web Parts SharePoint Framework sont hébergés dans SharePoint sans avoir besoin de services externes tels qu’Azure. [En savoir plus sur l’utilisation de SharePoint Framework dans Teams.](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)

## <a name="introduction"></a>Introduction

Ces instructions expliquent comment vous pouvez prendre un onglet à partir d’un exemple d’application Microsoft Teams et l’utiliser dans SharePoint. Nous allons utiliser un onglet qui est déjà hébergé sur Azure afin de nous concentrer sur le travail d’intégration requis.

L’exemple d’application que nous utilisons est une application de gestion des talents. Il gère le processus d’embauche des candidats pour les postes ouverts dans une équipe. (L’application elle-même, bien qu’elle semble agréable, n’a réellement rien à faire. Nous voulons nous concentrer sur la création d’une application Teams et son chargement dans Teams, et non sur la création d’une application de gestion des talents réelle.)

### <a name="benefits-of-this-approach"></a>Avantages de cette approche

- Atteindre les utilisateurs SharePoint avec votre onglet Teams existant
- Téléchargez votre manifeste d’application directement dans votre catalogue d’applications SharePoint. [Les packages d’application Teams](~/concepts/build-and-test/apps-package.md) sont désormais pris en charge par SharePoint
- Les utilisateurs finaux configurent l’onglet d’une page comme n’importe quel autre élément Web Part SharePoint
- Votre onglet peut accéder à son [contexte](~/tabs/how-to/access-teams-context.md) comme il le peut lors de l’exécution dans Teams

## <a name="step-1-testing-the-sample-app"></a>Étape 1 : Test de l’exemple d’application

Téléchargez l’exemple de manifeste d’application [**à partir d’ici.**](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip)

Dans Microsoft Teams, cliquez sur l’icône du Store en bas à gauche, puis sur « Télécharger une application personnalisée » en bas à gauche. Le fichier à télécharger se trouve dans votre dossier Téléchargements ; Il s’appelle TalentMgmt-Azure.zip. Si tout se passe bien, l’écran d’installation/consentement s’affiche pour l’application de gestion des talents. Choisissez l’équipe dans qui vous souhaitez installer, puis cliquez sur le bouton Installer. Vous êtes désormais libre d’expérimenter l’application.

## <a name="step-2-using-the-teams-tab-in-sharepoint"></a>Étape 2 : utilisation de l’onglet Teams dans SharePoint

Téléchargez et déployez votre package d’application Teams dans votre catalogue d’applications SharePoint en visitant , par `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` exemple. `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`

Lorsque vous y sont invités, activez « Rendre cette solution disponible pour tous les sites de l’organisation » :

![Onglets en vue SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image065.png)

Dans votre site, créez une page en cliquant sur le bouton d’engrenage en haut à droite, puis sur « Ajouter une page » :

![Vue SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image066.png)

Vous verrez l’expérience de authoring des pages SharePoint. Nommez votre page « Onglet Mes équipes ».

Ouvrez la boîte à outils du volet Web En appuyant sur le bouton + et sélectionnez l’onglet Teams (nommé « Contoso HR »). Les composants Web Parts sont triés par ordre alphabétique ; S’il s’agit d’une longue liste, vous pouvez utiliser la barre de recherche pour la trouver. Cela crée un élément Web Part dans le canevas qui contient votre onglet Teams :

![Affichage Onglet](~/assets/images/tabs/tabs-in-sharepoint/image071.png)

Appuyez sur le bouton « Publier » lorsque vous avez terminé la modification.

Vous pouvez cliquer sur « Ajouter une page à la navigation » pour avoir une référence rapide à votre page dans la barre de navigation de gauche :

![Onglet dans l’image Sharepoint](~/assets/images/tabs/tabs-in-sharepoint/image073.png)

## <a name="step-3-explore-app-pages-in-sharepoint"></a>Étape 3 : Explorer les pages d’application dans SharePoint

Une fois votre page publiée, vous pouvez explorer comment transformer votre application Teams en une expérience plus [complète dans SharePoint.](/sharepoint/dev/spfx/web-parts/single-part-app-pages) Cela convertit la page actuelle en page d’application, affichant la mise en page SharePoint normale avec une expérience de page complète pour l’onglet Teams :

![Image des onglets dans SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image085.png)

## <a name="code-sample"></a>Exemple de code
| **Exemple de nom** | **Description** | **SPFx** |
|-----------------|-----------------|----------|
| Partie Web SPFx | Exemples de partie Web SPFx pour les onglets, les canaux et les groupes. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group/spfx)

## <a name="more-information"></a>Plus d’informations

- [Création d’un onglet Microsoft Teams à l’aide de SharePoint Framework - Didacticiel](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)
- [Utilisation des pages d’application à composant unique dans SharePoint Online](/sharepoint/dev/spfx/web-parts/single-part-app-pages)
