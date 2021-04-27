---
title: Ajouter l'onglet Teams à SharePoint
author: laujan
description: Comment déployer votre onglet Teams existant sur SharePoint en tant que partie Web De l'infrastructure SharePoint.
keywords: teams tabs sharepoint framework development
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 08a4aef329d0e5e1d063f05959f0a589581c9c03
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020329"
---
# <a name="add-teams-tab-to-sharepoint"></a>Ajouter l'onglet Teams à SharePoint 

Vous pouvez obtenir une expérience d'intégration enrichie entre Microsoft Teams et SharePoint en ajoutant un onglet Microsoft Teams dans SharePoint en tant que partie Web SPFx. Ce document vous guide sur la façon de prendre un onglet à partir d'un exemple d'application Microsoft Teams et de l'utiliser dans SharePoint. 

## <a name="rich-integration-between-teams-and-sharepoint"></a>Intégration enrichie entre Teams et SharePoint

Avec la version de novembre de Teams et SharePoint Framework v.1.7, les développeurs ont deux fonctionnalités puissantes :

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
                        <p>Créez des expériences d'application enrichies dans SharePoint en apportant votre application Teams dans SharePoint (cet article).</p>
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
                        <p>Apportez vos composants Web Parts SharePoint à Teams et laissez SharePoint gérer l'hébergement pour vous.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

### <a name="teams-tabs-in-sharepoint"></a>Onglets Teams dans SharePoint

Avec SharePoint Framework v.1.7, vous pouvez héberger vos onglets Teams dans SharePoint. Comme les onglets hébergés dans SharePoint obtiennent une expérience de **page** complète similaire, en exposant toutes les fonctionnalités des onglets Teams tout en conservant le contexte et la familiarité d'un site SharePoint.

### <a name="sharepoint-framework-in-teams"></a>SharePoint Framework dans Teams

Vous pouvez également implémenter vos onglets Microsoft Teams à l'aide de SharePoint Framework. Les composants WebPoint Framework sont hébergés dans SharePoint sans avoir besoin de services externes, tels qu'Azure. Pour les développeurs SharePoint, cela simplifie considérablement le processus de développement des onglets Teams. Pour plus d'informations sur SharePoint Framework dans Teams, voir comment utiliser [SharePoint Framework dans Teams.](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)

## <a name="introduction"></a>Introduction

L'onglet utilisé ici est déjà hébergé sur Azure, pour se concentrer sur le travail d'intégration requis.

L'exemple d'application utilisé est une application de gestion des talents. Il gère le processus d'embauche des candidats pour les postes ouverts dans une équipe. Créez un exemple d'application Teams et chargez-la dans Teams. Ne créez pas d'application de gestion des talents réelle.

### <a name="benefits-of-this-approach"></a>Avantages de cette approche

* Atteindre les utilisateurs SharePoint avec votre onglet Teams existant.
* Téléchargez votre manifeste d'application directement dans votre catalogue d'applications SharePoint. [Les packages d'application Teams](~/concepts/build-and-test/apps-package.md) sont désormais pris en charge par SharePoint.
* Les utilisateurs configurent l'onglet d'une page comme n'importe quel autre élément Web Part SharePoint.
* Votre onglet peut accéder à [son contexte](~/tabs/how-to/access-teams-context.md) de la même manière que lorsqu'il est en cours d'exécution dans Teams.

**Pour ajouter l'onglet Teams à SharePoint**

Pour ajouter l'onglet Teams à SharePoint, effectuez les étapes suivantes :

## <a name="1-test-the-sample-app"></a>1. Tester l'exemple d'application

Téléchargez [l'exemple de manifeste d'application.](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip)

1. Ouvrir Microsoft Teams.
1. Sélectionnez **l'icône de l'Appstore** en bas à gauche de l'onglet latéral.
1. Sélectionnez **Télécharger une application personnalisée en** bas à gauche. L'image suivante affiche l'écran correspondant :  

    ![télécharger une application personnalisée](~/assets/images/tabs/tabs-in-sharepoint/upload-custom-app.png)

1. Le fichier à télécharger se trouve dans votre **dossier Téléchargements.** Elle est appelée TalentMgmt-Azure.zip. L'image suivante affiche l'écran correspondant :
 
    ![TalentMgmt dans Azure](~/assets/images/tabs/tabs-in-sharepoint/talentmgmt-azure.png)

1. Vous pouvez voir l'écran d'installation ou de consentement de l'application de gestion des talents. Sélectionnez l'équipe que vous souhaitez installer. 
1. Sélectionnez **l'installation** et commencez à tester l'application.

## <a name="2-use-teams-tab-in-sharepoint"></a>2. Utiliser l'onglet Teams dans SharePoint

1. Téléchargez et déployez votre package d'application Teams dans votre catalogue d'applications SharePoint en visitant `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` . Par exemple, `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`.

1. Lorsque vous y sont invités, **activez Rendre cette solution disponible pour tous les sites de l'organisation.**
L'image suivante affiche l'écran correspondant :

   ![Onglets en vue SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image065.png)

1. Dans votre site, créez une page en sélectionnant le bouton d'engrenage en haut à droite, puis **sélectionnez Ajouter une page.**
L'image suivante affiche l'écran correspondant :

   ![Vue SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image066.png)

1. Vous pouvez voir l'expérience de authoring des pages SharePoint. Nommez votre page en **tant qu'onglet Mes équipes.**

1. Ouvrez la boîte à outils du volet Web En appuyant sur le bouton, puis sélectionnez l'onglet `+` Teams nommé **Contoso HR**. Les composants Web Parts sont triés par ordre alphabétique. S'il s'agit d'une longue liste, vous pouvez utiliser la barre de recherche pour la trouver. Cela crée un élément Web Part dans le canevas qui contient votre onglet Teams. L'image suivante affiche l'affichage Onglet :

   ![Affichage Onglet](~/assets/images/tabs/tabs-in-sharepoint/image071.png)

1. Appuyez sur **le** bouton Publier après avoir terminé la modification.

1. Sélectionnez **Ajouter une page à la navigation** pour avoir une référence rapide à votre page dans la barre de navigation de gauche. L'image suivante affiche l'onglet dans SharePoint : 

   ![Onglet dans l'image Sharepoint](~/assets/images/tabs/tabs-in-sharepoint/image073.png)

## <a name="3-explore-app-pages-in-sharepoint"></a>3. Explorer les pages d'application dans SharePoint

Une fois votre page publiée, vous pouvez explorer comment transformer votre application Teams en une expérience plus [complète dans SharePoint.](/sharepoint/dev/spfx/web-parts/single-part-app-pages) Cela convertit la page actuelle en page d'application, affichant la mise en page SharePoint normale avec une expérience de page complète pour l'onglet Teams. 

L'image suivante affiche l'expérience complète de l'application Teams dans Sharepoint : ![ Image des onglets dans Sharepoint](~/assets/images/tabs/tabs-in-sharepoint/image085.png)

## <a name="code-sample"></a>Exemple de code
| **Exemple de nom** | **Description** | **SPFx** |
|-----------------|-----------------|----------|
| Partie Web SPFx | Exemples de partie Web SPFx pour les onglets, les canaux et les groupes. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group/spfx)

## <a name="see-also"></a>Voir aussi

> [!div class="nextstepaction"]
> [Création d’un onglet Microsoft Teams à l’aide de SharePoint Framework - Didacticiel](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)

> [!div class="nextstepaction"]
> [Utilisation des pages d’application à composant unique dans SharePoint Online](/sharepoint/dev/spfx/web-parts/single-part-app-pages)

> [!div class="nextstepaction"]
> [Intégrer les applications Web](~/samples/integrate-web-apps-overview.md)
