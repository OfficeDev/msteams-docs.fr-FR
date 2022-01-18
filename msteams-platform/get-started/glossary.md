---
title: Microsoft Teams documentation pour les développeurs - Glossaire
description: Glossaire de la documentation Microsoft Teams développeur
ms.localizationpriority: medium
ms.topic: reference
keywords: Microsoft Teams définition de développeur
ms.openlocfilehash: 0858d0cfb246e99871c02f81c82c1eaa30bb6edf
ms.sourcegitcommit: 9e448dcdfd78f4278e9600808228e8158d830ef7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/17/2022
ms.locfileid: "62059828"
---
# <a name="glossary"></a>Glossaire

Termes et définitions courants utilisés dans Teams documentation du développeur.
<br>
<br>
<details>
<summary>A</summary>

| Terme | Définition |
| --- | --- |
| Commande d’action | Les commandes d’action sont utilisées pour présenter aux utilisateurs une fenêtre popup modale pour collecter ou afficher des informations. <br>**Voir aussi**: Extension de messagerie; Commandes de recherche |
| Carte adaptative | Une carte adaptative est un extrait de contenu actionnable que vous pouvez ajouter à une conversation via un bot ou une extension de messagerie. À l’aide de texte, de graphiques et de boutons, ces cartes fournissent une communication enrichie à votre public. |
| Catalogue d’applications | Le catalogue d’applications permet de stocker les applications pour SharePoint et office pour l’utilisation interne de notre organisation. |
| Manifeste d'application | Le Teams de l’application décrit comment l’application s’intègre au Microsoft Teams produit. Votre manifeste doit être conforme au schéma hébergé sur https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json . |
| Package de l’application | Un package Teams’application est un fichier zip qui contient le fichier manifeste de l’application et les icônes de l’application - icône de couleur et icône de plan. |
| Autorisations d’application | L’option Autorisations d’application Teams vous permet d’activer les autorisations d’appareil de l’application pour votre application. Elle est disponible uniquement lorsque le fichier manifeste de l’application déclare que l’application a besoin d’autorisations d’appareil. <br> **Voir aussi**: Autorisations d’appareil |
| Étendue de l’application | L’étendue de l’application détermine la façon dont votre application interagit avec vos utilisateurs. Une application peut avoir une étendue personnelle, une étendue de canal ou une étendue d’équipe. Une application Teams peut exister dans plusieurs étendues. |
| App Studio | App Studio est une application pour commencer à créer ou à intégrer vos propres applications Microsoft Teams applications. Il a maintenant évolué vers le Portail du développeur. <br> **Voir aussi**: Portail des développeurs |
| Ressource Azure | Service disponible via Azure que votre application Teams peut utiliser pour le déploiement Azure. Il peut s’y avoir des comptes de stockage, des applications web, des bases de données, etc. |
| Azure Active Directory | Azure Active Directory (Azure AD) est le service de gestion des identités et des accès basé sur le cloud de Microsoft. Il permet aux utilisateurs authentifiés d’accéder aux ressources Azure internes et externes. |
| Authentification | L’authentification est un processus qui permet d’autoriser l’accès des utilisateurs pour l’utilisation de votre application. Il peut être effectué à l’aide des API microsoft Graph ou de l’authentification basée sur le web. <br> **Voir aussi**: Fournisseurs d’identité |
| Flux d’authentification | Dans Teams, il existe deux flux d’authentification différents pour authentifier un utilisateur pour l’utilisation d’une application : l’authentification basée sur le web et le flux OAuthPrompt. |
|
</details>
<br>
<details>
<summary>B</summary>

| Terme | Définition |
| --- | --- |
| Blazor | Blazor est une infrastructure web libre et open source qui permet aux développeurs de créer des applications web à l’aide C# html. Il vous permet de créer des UIS web interactives à l’C# au lieu de JavaScript. Les applications de blasor sont composées de composants d’interface utilisateur web réutilisables implémentés à l’C#, HTML et CSS. Il est développé par Microsoft. |
| Bicep | Le bicep est un langage déclaratif, ce qui signifie que les éléments peuvent apparaître dans n’importe quel ordre. Contrairement aux langages impératifs, l’ordre des éléments n’affecte pas le traitement du déploiement. |
| Bot | Un bot est une application qui effectue des tâches répétitives programmées. <br> **Voir aussi**: Bot conversationnel ; Bot de conversation |
| Bot Emulator | Bot Framework Emulator est une application de bureau qui vous permet de tester et déboguer des bots, localement ou à distance. |
| Bot Framework | Bot Framework est un SDK enrichi utilisé pour créer des bots à l’aide de C#, Java, Python et JavaScript. Si vous avez déjà un bot basé sur Bot Framework, vous pouvez facilement le modifier pour qu’il fonctionne Teams. |
</details>
<br>
<details>
<summary>C</summary>

| Terme | Définition |
| --- | --- |
| Bot d’appel | Bot qui participe à des appels audio ou vidéo et à des réunions en ligne. <br> **Voir aussi**: Bot de conversation ; Bot de réunion |
| Fonctionnalité | La fonctionnalité d’une application Teams est appelée Fonctionnalité. Une application peut avoir une ou plusieurs fonctionnalités principales, telles que l’onglet, le bot, les extensions de messagerie. <br>**Voir aussi**: Fonctionnalité de l’appareil; Fonctionnalité multimédia |
| Bot de conversation | Un bot est également appelé bot de conversation ou bot de conversation. Il s’agit d’une application qui exécute des tâches simples et répétitives par des utilisateurs tels que le service clientèle ou le personnel de support technique. <br> **Voir aussi**: Bot conversationnel. |
| Canal | Un canal est un endroit unique où une équipe peut partager des messages, des outils et des fichiers. Dans Teams, le travail d’équipe et la communication se produisent dans les canaux.  |
| Secret client | La clé secrète/mot de passe client ou une paire de clés publiques ou privées certificat. N’est pas nécessaire pour les applications natives. <br> **Voir aussi**: Bot |
| Ressources cloud | Service disponible sur le cloud via Internet que votre application Teams peut utiliser. Il peut s’y avoir des comptes de stockage, des applications web, des bases de données, etc. |
| Application de collaboration |  <br> **Voir aussi**: Application autonome |
| Connecteurs |  <br> **Voir aussi**: Webhooks |
| Conversation | Une conversation est une série de messages envoyés entre votre bot Microsoft Teams et un ou plusieurs utilisateurs. Une conversation peut avoir trois étendues : canal, conversation personnelle et conversation de groupe. <br>**Voir aussi**: conversation un-à-un ; Conversation de groupe |
| Bot conversationnel |  Les bots de conversation permettent aux utilisateurs d’interagir avec votre service web à l’aide de texte, de cartes interactives et de modules de tâche. <br>**Voir aso** Bot de conversation |