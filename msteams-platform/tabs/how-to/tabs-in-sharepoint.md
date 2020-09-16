---
title: Ajout d’un onglet Microsoft teams dans SharePoint en tant que composant WebPart SPFx
author: laujan
description: Comment déployer votre onglet teams existant vers SharePoint en tant que composant WebPart SharePoint Framework.
keywords: onglet teams développement SharePoint Framework
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 2bdc7ab578be485eee33020b3b0c1a4099fd8ade
ms.sourcegitcommit: e8dfcb167274e996395b77d65999991a18f2051a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/15/2020
ms.locfileid: "47818940"
---
# <a name="adding-a-microsoft-teams-tab-in-sharepoint-as-an-spfx-web-part"></a>Ajout d’un onglet Microsoft teams dans SharePoint en tant que composant WebPart SPFx

> [!IMPORTANT]
> Cette fonctionnalité est encore en phase préliminaire et est sujette à modifications. Elle n’est pas prise en charge dans les environnements de production. Vos commentaires et suggestions concernant cette fonctionnalité sont les bienvenus via la [liste des problèmes liés aux documents de développement SharePoint](https://github.com/SharePoint/sp-dev-docs/issues).

## <a name="rich-integration-between-teams-and-sharepoint"></a>Intégration enrichie entre teams et SharePoint

Avec la version de novembre de teams et de SharePoint Framework v. 1,7, les développeurs disposent de deux fonctionnalités puissantes :

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
                        <h3>Onglets teams dans SharePoint</h3>
                        <p>Créez des expériences d’application enrichies dans SharePoint en plaçant votre application teams dans SharePoint (cet article).</p>
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
                        <h3>SharePoint Framework dans teams</h3>
                        <p>Intégrez vos composants WebPart SharePoint à teams et laissez SharePoint gérer l’hébergement pour vous.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

### <a name="teams-tabs-in-sharepoint"></a>Onglets teams dans SharePoint

Avec SharePoint Framework v. 1.7, nous prenons désormais en charge la possibilité pour les développeurs de prendre leurs onglets teams et de les héberger dans SharePoint. Sous forme d’onglets hébergés dans SharePoint, profitez d’une expérience de « pleine page » similaire, exposant toutes les fonctionnalités des onglets teams tout en conservant le contexte et la familiarité d’un site SharePoint.

### <a name="sharepoint-framework-in-teams"></a>SharePoint Framework dans teams

Vous pouvez également implémenter vos onglets Microsoft teams à l’aide de SharePoint Framework. Pour les développeurs SharePoint, cela simplifie considérablement le processus de développement pour les onglets Teams, car les composants WebPart de SharePoint Framework sont hébergés dans SharePoint sans qu’il soit nécessaire de recourir à des services externes comme Azure. [En savoir plus sur l’utilisation de SharePoint Framework dans Teams.](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)

## <a name="introduction"></a>Introduction

Ces instructions vous expliquent comment prendre un onglet à partir d’un exemple d’application Microsoft teams et comment l’utiliser dans SharePoint. Nous allons utiliser un onglet qui est déjà hébergé sur Azure afin de se concentrer sur le travail d’intégration requis.

L’exemple d’application que nous utilisons est une application de gestion des compétences. Il gère le processus d’embauche de candidats pour les postes ouverts dans une équipe. (L’application elle-même, même si elle semble agréable, ne fait rien. Nous souhaitons vous concentrer sur la création d’une application teams et son chargement dans Teams, et non sur la création d’une véritable application de gestion des compétences.)

### <a name="benefits-of-this-approach"></a>Avantages de cette approche

- Atteindre les utilisateurs SharePoint avec votre onglet teams existant
- Téléchargez le manifeste de votre application directement dans votre catalogue d’applications SharePoint. Les [packages d’applications teams](~/concepts/build-and-test/apps-package.md) sont désormais pris en charge par SharePoint
- Les utilisateurs finaux configurent l’onglet sur une page comme n’importe quel autre composant WebPart SharePoint
- Votre onglet peut accéder à son [contexte](~/tabs/how-to/access-teams-context.md) comme il le peut lorsqu’il est exécuté dans teams

## <a name="step-1-testing-the-sample-app"></a>Étape 1 : test de l’exemple d’application

Téléchargez l’exemple de manifeste d’application à partir de [**cet emplacement**](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip).

Dans Microsoft Teams, cliquez sur l’icône de la boutique située en bas à gauche, puis sur « Télécharger une application personnalisée » en bas à gauche. Le fichier à télécharger sera situé dans votre dossier téléchargements ; Il est appelé TalentMgmt-Azure.zip. Si tout se passe bien, vous verrez l’écran d’installation/de consentement pour l’application de gestion des compétences. Choisissez l’équipe sur laquelle vous souhaitez effectuer l’installation, puis cliquez sur le bouton installer. Vous êtes maintenant libre de tester l’application.

## <a name="step-2-using-the-teams-tab-in-sharepoint"></a>Étape 2 : utilisation de l’onglet teams dans SharePoint

Téléchargez et déployez votre package d’applications teams dans votre catalogue d’applications SharePoint en visitant `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` , par exemple `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` .

Lorsque vous y êtes invité, activez la « rendre cette solution disponible pour tous les sites de l’Organisation » :

![Onglets dans l’affichage SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image065.png)

Dans votre site, créez une page en cliquant sur le bouton engrenage dans le coin supérieur droit, puis ajoutez une page :

![Vue SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image066.png)

Vous verrez l’expérience de création de pages SharePoint. Nommez votre page « onglet My Teams ».

Ouvrez la boîte à outils du composant WebPart en appuyant sur le bouton +, puis sélectionnez l’onglet Teams (nommé « Contoso HR »). Les composants WebPart sont triés par ordre alphabétique ; s’il s’agit d’une longue liste, vous pouvez utiliser la barre de recherche pour la trouver. Cette opération crée un composant WebPart dans la zone de dessin qui contient l’onglet teams :

![Affichage onglet](~/assets/images/tabs/tabs-in-sharepoint/image071.png)

Appuyez sur le bouton « Publier » lorsque vous avez terminé les modifications.

Vous souhaiterez peut-être cliquer sur Ajouter une page à la navigation pour obtenir une référence rapide à votre page dans la barre de navigation de gauche :

![Onglet dans l’image SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image073.png)

## <a name="step-3-explore-app-pages-in-sharepoint"></a>Étape 3 : explorer les pages d’application dans SharePoint

Une fois votre page publiée, vous pouvez explorer [la transformation de votre application teams en une expérience plus complète dans SharePoint](/sharepoint/dev/spfx/web-parts/single-part-app-pages). Cette fonction convertit la page actuelle en page d’application, affichant la mise en page SharePoint normale avec une expérience pleine page pour l’onglet teams :

![Image d’onglets dans SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image085.png)

## <a name="more-information"></a>Plus d’informations

- [Création d’un onglet Microsoft Teams à l’aide de SharePoint Framework - Didacticiel](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)
- [Utilisation des pages d’application à composant unique dans SharePoint Online](/sharepoint/dev/spfx/web-parts/single-part-app-pages)
