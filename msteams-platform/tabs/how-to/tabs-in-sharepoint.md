---
title: Ajouter l'onglet Teams à SharePoint
author: surbhigupta
description: Comment déployer votre onglet Teams existant SharePoint en tant que SharePoint Framework Web Part.
keywords: teams tabs sharepoint framework development
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 6720cf3fdc8a02d325bf775f4bf319b9d07ec17c
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/22/2021
ms.locfileid: "53068651"
---
# <a name="add-teams-tab-to-sharepoint"></a>Ajouter l'onglet Teams à SharePoint 

Vous pouvez obtenir une expérience d’intégration riche entre Microsoft Teams et SharePoint en ajoutant un onglet Microsoft Teams dans SharePoint en tant que SPFx web. Ce document vous guide sur la façon dont vous pouvez prendre un onglet à partir d’un exemple d Microsoft Teams appl’application et l’utiliser dans SharePoint. 

## <a name="rich-integration-between-teams-and-sharepoint"></a>Intégration enrichie entre Teams et SharePoint

Avec la version de novembre Teams et SharePoint Framework version 1.7, les développeurs ont deux fonctionnalités puissantes :

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
                        <h3>Teams Onglets dans SharePoint</h3>
                        <p>Créez des expériences d’application enrichies SharePoint en apportant votre application Teams dans SharePoint (cet article).</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li>
    <a href="/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab">
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
                        <p>Faites en SharePoint vos composants Web Teams et laissez SharePoint gérer l’hébergement pour vous.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

### <a name="teams-tabs-in-sharepoint"></a>Teams onglets dans SharePoint

Avec SharePoint Framework v.1.7, vous pouvez héberger vos onglets Teams dans SharePoint. Comme les onglets hébergés dans SharePoint offrent une expérience de **page** complète similaire, en exposant toutes les fonctionnalités des onglets Teams tout en conservant le contexte et la familiarité d’un site SharePoint.

### <a name="sharepoint-framework-in-teams"></a>SharePoint Framework dans Teams

Vous pouvez également implémenter vos onglets Microsoft Teams à l’aide SharePoint Framework. SharePoint Framework web sont hébergés dans SharePoint sans avoir besoin de services externes, tels qu’Azure. Pour SharePoint développeurs, cela simplifie considérablement le processus de développement pour Teams onglets. Pour plus d’informations SharePoint Framework la Teams, voir comment utiliser les SharePoint Framework [dans Teams.](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)

## <a name="introduction"></a>Introduction

L’onglet utilisé ici est déjà hébergé sur Azure, pour se concentrer sur le travail d’intégration requis.

L’exemple d’application utilisé est une application de gestion des talents. Il gère le processus d’embauche des candidats pour les postes ouverts dans une équipe. Créez un exemple Teams application et chargez-la dans Teams. Ne créez pas d’application de gestion des talents réelle.

### <a name="benefits-of-this-approach"></a>Avantages de cette approche

* Touchez SharePoint utilisateurs avec votre onglet Teams existant.
* Télécharger votre manifeste d’application directement dans SharePoint catalogue d’applications. [Teams packages d’application](~/concepts/build-and-test/apps-package.md) sont désormais pris en charge par SharePoint.
* Les utilisateurs configurent l’onglet sur une page comme n’importe quel autre SharePoint web.
* Votre onglet peut accéder à [son contexte](~/tabs/how-to/access-teams-context.md) de la même manière qu’il le peut, lors de l’exécution à l’Teams.

**Pour ajouter Teams onglet à SharePoint**

Effectuez les étapes suivantes pour ajouter Teams onglet à SharePoint :

## <a name="1-test-the-sample-app"></a>1. Tester l’exemple d’application

Téléchargez [l’exemple de manifeste d’application.](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip)

1. Ouvrir Microsoft Teams.
1. Sélectionnez **l’icône de l’Appstore** en bas à gauche de l’onglet latéral.
1. Sélectionnez **Télécharger une application personnalisée** en bas à gauche. L’image suivante affiche l’écran correspondant :  

    ![télécharger une application personnalisée](~/assets/images/tabs/tabs-in-sharepoint/upload-custom-app.png)

1. Le fichier à télécharger se trouve dans votre **dossier Téléchargements.** Elle est appelée TalentMgmt-Azure.zip. L’image suivante affiche l’écran correspondant :
 
    ![TalentMgmt dans Azure](~/assets/images/tabs/tabs-in-sharepoint/talentmgmt-azure.png)

1. Vous pouvez voir l’écran d’installation ou de consentement de l’application de gestion des talents. Sélectionnez l’équipe que vous souhaitez installer. 
1. Sélectionnez **l’installation** et commencez à tester l’application.

## <a name="2-use-teams-tab-in-sharepoint"></a>2. Utilisez l’Teams dans SharePoint

1. Télécharger et déployez votre package Teams’application dans votre catalogue SharePoint’applications en visitant `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` . Par exemple, `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`.

1. Lorsque vous y sont invités, **activez Rendre cette solution disponible pour tous les sites de l’organisation.**
L’image suivante affiche l’écran correspondant :

   ![Onglets en vue SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image065.png)

1. Dans votre site, créez une page en sélectionnant le bouton d’engrenage en haut à droite, puis **sélectionnez Ajouter une page.**
L’image suivante affiche l’écran correspondant :

   ![Vue SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image066.png)

1. Vous pouvez voir l’expérience de SharePoint pages de texte. Nommez votre page sous **le nom Mon Teams onglet**.

1. Ouvrez la boîte à outils du service Web En appuyant sur le bouton, puis sélectionnez `+` votre onglet Teams nommé **Contoso HR**. Les composants Web Parts sont triés par ordre alphabétique. S’il s’agit d’une longue liste, vous pouvez utiliser la barre de recherche pour la trouver. Cela crée un élément Web Part dans la zone de dessin qui contient votre Teams onglet. L’image suivante affiche l’affichage Onglet :

   ![Affichage Onglet](~/assets/images/tabs/tabs-in-sharepoint/image071.png)

1. Appuyez sur **le** bouton Publier après avoir terminé la modification.

1. Sélectionnez **Ajouter une page à la navigation** pour avoir une référence rapide à votre page dans la barre de navigation de gauche. L’image suivante affiche l’onglet dans SharePoint : 

   ![Onglet dans l’image Sharepoint](~/assets/images/tabs/tabs-in-sharepoint/image073.png)

## <a name="3-explore-app-pages-in-sharepoint"></a>3. Explorer les pages d’application dans SharePoint

Une fois votre page publiée, vous pouvez explorer comment transformer votre application Teams en une expérience plus complète à [l’intérieur SharePoint](/sharepoint/dev/spfx/web-parts/single-part-app-pages). Cela convertit la page actuelle en page d’application, affichant la mise en page normale SharePoint page avec une expérience de page complète pour l’onglet Teams page. 

L’image suivante affiche l’expérience complète Teams’application dans SharePoint : ![ Image des onglets dans SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image085.png)

## <a name="code-sample"></a>Exemple de code
| **Exemple de nom** | **Description** | **SPFx** |
|-----------------|-----------------|----------|
| SPFx Web Part | SPFx des exemples de webs pour les onglets, les canaux et les groupes. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group/spfx)

## <a name="see-also"></a>Voir aussi

* [Création d’un onglet Microsoft Teams à l’aide de SharePoint Framework - Didacticiel](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)
* [Utilisation des pages d’application à composant unique dans SharePoint Online](/sharepoint/dev/spfx/web-parts/single-part-app-pages)
* [Intégrer les applications Web](~/samples/integrate-web-apps-overview.md)
