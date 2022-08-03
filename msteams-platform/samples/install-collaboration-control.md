---
title: Installer des contrôles collaboration
author: surbhigupta
description: Dans ce module, découvrez comment installer des contrôles de collaboration avec power apps et Microsoft 365 E3 et comment installer des solutions de contrôles de collaboration.
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: aa4259855ba0c95906d7196ffd83c093bea89ea9
ms.sourcegitcommit: 0bb822b30739e4a532a36764dad2dbf35a81ba29
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2022
ms.locfileid: "67178982"
---
# <a name="install-collaboration-controls"></a>Installer des contrôles collaboration

> [!NOTE]
> Actuellement, les contrôles collaboration sont disponibles uniquement en [préversion publique des développeurs](~/resources/dev-preview/developer-preview-intro.md).

Dans cet article, vous allez apprendre à installer des contrôles de collaboration. Les éléments suivants sont nécessaires pour générer et déployer Gestionnaire de collaboration applications à l’aide des contrôles collaboration :

* **Applications power** : pour générer et exécuter des applications pilotées par modèle à l’aide des contrôles collaboration.
* **M365 E3 ou version ultérieure** : pour déployer des applications personnalisées dans Microsoft Teams et stocker des tâches dans le Planificateur, des fichiers dans SharePoint et des réunions dans Outlook.

Pour installer les composants dans un environnement Power Platform, les rôles suivants sont requis :

* Personnalisateur système
* Créateur d’environnement

Pour plus d’informations sur les privilèges de rôle, consultez [Configurer la sécurité des utilisateurs dans un environnement](/power-platform/admin/database-security#predefined-security-roles)

## <a name="install-the-collaboration-controls-solutions"></a>Installer les solutions de contrôles collaboration

Vous allez installer les contrôles Collaboration dans votre environnement dataverse via une liaison privée. Ce lien ne doit pas être partagé avec une autre personne à l’intérieur ou à l’extérieur de votre organisation.

Vous ne pourrez configurer et utiliser les composants de votre propre application basée sur des modèles qu’après avoir reçu le lien et installé les contrôles Collaboration dans votre environnement dataverse.

Les contrôles de collaboration incluent les solutions suivantes :

|**Solutions de paramètres** | **Objectif** |
|---|---|
| Paramètres des contrôles de collaboration | Conserver l’infrastructure de paramètres qui alimente les contrôles de collaboration |
| Objets paramètres des contrôles de collaboration | Fournit des valeurs de paramètres prédéfinies utilisées par les contrôles Collaboration.|

|**Solutions de collaboration** | **Objectif** |
|---|---|
| Tâches des contrôles de collaboration  | Inclut le contrôle PCF Tasks (infrastructure du composant Power Apps). |
| Événements de contrôles de collaboration | Inclut le contrôle PCF Événements pour les réunions Outlook et Teams et les rendez-vous de réservation. |
| Notes des contrôles de collaboration | Inclut le contrôle PCF de notes, qui stocke les notes dans Dataverse. |
| Fichiers de contrôles de collaboration | Inclut le contrôle PCF Fichiers pour l’accès aux fichiers sur SharePoint. |
| Contrôles de collaboration de base |Inclut des API de collaboration personnalisées, le modèle de données de collaboration et des tables virtuelles pour les événements, les fichiers et les contrôles de tâche. |
| Approbations des contrôles de collaboration | Inclut le nouveau contrôle PCF Approbations. |
| Connecteur de contrôles de collaboration | Inclut le nouveau connecteur Power Automate collaboration |

> [!NOTE]
> Si vous disposez d’une version existante des contrôles installés dans votre environnement, vous devrez peut-être créer un nouvel environnement et effectuer une nouvelle installation pour effectuer une mise à niveau vers la dernière version.

Avant l’installation, vous devez être dans un environnement Power Platform ou un locataire administrateur. Vous aurez besoin d’un environnement dataverse avec une base de données. Si vous n’en avez pas, vous devez [en créer un pour](/power-platform/admin/create-environment) poursuivre l’installation.

Pour installer les solutions, commencez par accéder à [Microsoft AppSource], puis effectuez les étapes suivantes :

1. Sélectionnez **le bouton Obtenir maintenant** .

   :::image type="content" source="../assets/images/collaboration-control/preview-form.png" alt-text="Formulaire d’aperçu "border="true":::

1. Connectez-vous avec votre compte, remplissez le formulaire et **sélectionnez Continuer**.

   :::image type="content" source="../assets/images/collaboration-control/overview.png" alt-text="vue d’ensemble du contrôle de collaboration" border="true":::

   :::image type="content" source="../assets/images/collaboration-control/collaboration-controls-preview.png" alt-text="Aperçu du contrôle de collaboration" border="true":::

1. Vous serez dirigé vers Power Platform Administration Center. Sélectionnez un environnement dans le menu déroulant et acceptez les termes et les instructions de stratégie.

   > [!TIP]
   > Si vous voyez une erreur d’autorisation lorsque vous sélectionnez l’environnement, essayez de sélectionner en dehors du menu déroulant de l’environnement pour voir si cela résout le problème.

   :::image type="content" source="../assets/images/collaboration-control/install-environment.png" alt-text="Installer l’environnement de contrôle de collaboration" border="true":::

1. Sélectionnez **Installer**, l’installation peut prendre environ 15 minutes.

1. [https://make.powerapps.com/](https://make.powerapps.com/)Atteindre , [https://make.preview.powerapps.com/](https://make.preview.powerapps.com/) est également pris en charge si vous êtes inscrit à la préversion de Power Apps.

1. Vérifiez que vous êtes dans l’environnement dans lequel les contrôles sont installés, car vous pouvez afficher l’environnement et le modifier si nécessaire en haut à droite du portail Power Apps.

1. Sélectionnez l’onglet **Solutions** pour afficher toutes les solutions que vous avez installées dans l’environnement approprié.

   :::image type="content" source="../assets/images/collaboration-control/solutions.png" alt-text="contrôle de collaboration des solutions" border= "true":::

> [!NOTE]
> Les contrôles collaboration sont en préversion et les éléments peuvent changer au fil du temps, ce qui peut entraîner des changements cassants. Les contrôles collaboration ne sont pas pris en charge dans les environnements de production.

Une fois l’installation réussie de toutes les solutions de collaboration dans votre environnement, vous serez en mesure de créer une nouvelle application basée sur des modèles qui peut tirer parti des fonctionnalités de contrôle collaboration.
