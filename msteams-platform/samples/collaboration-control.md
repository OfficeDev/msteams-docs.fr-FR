---
title: Contrôles de collaboration
author: surbhigupta
description: Dans ce module, découvrez comment les contrôles de collaboration permettent aux créateurs de créer des applications qui s’intègrent aux services Microsoft 365 tels que Planner, Bookings et Outlook.
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: fa0cb45921820a61fbfd7112a50f28eb9230fb4b
ms.sourcegitcommit: f2ac771cbd608e872604e9ac8ffec2d08f55ee1a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/04/2022
ms.locfileid: "68373023"
---
# <a name="collaboration-controls"></a>Contrôles de collaboration

Les contrôles de collaboration permettent d’appliquer Microsoft 365 et Microsoft Teams pour les approbations, les fichiers, les réunions, les notes et les tâches afin d’activer la collaboration contextuelle autour des processus métier. Ces contrôles vous permettent de créer des expériences collaboratives personnalisées qui peuvent être exposées directement dans Teams. Les solutions qui composent les contrôles de collaboration permettent aux créateurs de créer des applications qui s’intègrent aux services Microsoft 365 tels que Planner, Bookings, Outlook et SharePoint de manière à faible code.

Ces contrôles vous permettent de simplifier la collaboration de flux de travail des utilisateurs en créant des applications métier et en fonctionnant sans passer du contexte de l’application à l’application avec les éléments suivants :

* Approbations
* Fichiers
* Réunions
* Remarques
* Tâches

> [!NOTE]
> Actuellement, les contrôles collaboration sont disponibles uniquement en [préversion publique des développeurs](~/resources/dev-preview/developer-preview-intro.md).

Voici quelques-unes des fonctionnalités clés des contrôles collaboration :

* **Planificateur Microsoft tâches :** créez des tâches et attribuez-les aux membres d’un enregistrement afin qu’ils puissent afficher une liste consolidée des tâches dans l’application basée sur le modèle et l’application tâches dans Microsoft Teams.

* **Tâches Dataverse :** Créez des tâches qui peuvent être affectées à des utilisateurs externes à votre organisation.

* **Notes dataverse :** Créez des notes qui sont affectées à un enregistrement dans votre application.

* **Réunions Outlook :** Planifiez des réunions avec les clients et les employés internes et connectez-vous en toute transparence avec Microsoft Teams avec une sélection d’un bouton.

* **Fichiers SharePoint :** Partagez des fichiers avec des membres d’un enregistrement afin de pouvoir rechercher, référencer et modifier des artefacts pertinents dans un emplacement centralisé soutenu par SharePoint.

* **Approbations:** Simplifiez les demandes au sein de votre équipe.

> [!NOTE]
> En configurant et en utilisant les différentes fonctionnalités Microsoft 365 des contrôles de collaboration mentionnés précédemment, vous accordez l’autorisation aux données utilisateur de passer par le API Graph et acceptez [les conditions d’utilisation de l’API Microsoft](/legal/microsoft-apis/terms-of-use?context=graph%2Fcontext). Pour plus d’informations, consultez [Microsoft Graph](/graph/overview).

## <a name="how-collaboration-controls-works"></a>Fonctionnement des contrôles de collaboration

Les contrôles s’exécutent dans une application MDA (Model Driven Application) Power Apps qui peut être déployée sur Microsoft Teams. MDA s’exécute sur Microsoft Dataverse et peut être intégré à un modèle de données personnalisé. Les contrôles s’intègrent aux tâches Microsoft Graph for Planner, aux calendriers Outlook et Teams et aux fichiers SharePoint. Les contrôles collaboration ne s’intègrent pas directement à des sources externes, telles qu’un système d’enregistrement ou un portail.

* Les données peuvent être ajoutées à Dataverse à partir de sources externes via des API OData standard.

* Les données peuvent être lues à partir de Dataverse via des API OData standard et envoyées à des sources externes telles qu’un système d’enregistrement ou un portail.

:::image type="content" source="~/assets/images/collaboration-control/consumption-mda.png" alt-text="Cycle de vie de collaboration":::
