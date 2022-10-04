---
title: Installer les contrôles de collaboration
author: surbhigupta
description: Dans ce module, découvrez comment installer des contrôles de collaboration avec power apps et Microsoft 365 E3 et comment installer des solutions de contrôles de collaboration.
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: 5a253c9e7373a2df9e1161e6d3fc9d9b1c8ccdaa
ms.sourcegitcommit: f2ac771cbd608e872604e9ac8ffec2d08f55ee1a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/04/2022
ms.locfileid: "68373030"
---
# <a name="install-collaboration-controls"></a>Installer les contrôles de collaboration

> [!NOTE]
> Actuellement, les contrôles de collaboration sont disponibles uniquement en [préversion publique des développeurs](~/resources/dev-preview/developer-preview-intro.md).

Dans cet article, vous allez apprendre à installer des contrôles de collaboration. Les éléments suivants sont nécessaires pour générer et déployer Gestionnaire de collaboration applications à l’aide des contrôles collaboration :

* **Applications power** : pour générer et exécuter des applications pilotées par modèle à l’aide des contrôles collaboration.
* **M365 E3 ou version ultérieure** : pour déployer des applications personnalisées dans Microsoft Teams et stocker des tâches dans le Planificateur, des fichiers dans SharePoint et des réunions dans Outlook.

Pour installer les composants dans un environnement Power Platform, les rôles suivants sont requis :

* Personnalisateur système
* Créateur d’environnement

Pour plus d’informations sur les privilèges de rôle, consultez [Configurer la sécurité des utilisateurs dans un environnement](/power-platform/admin/database-security#predefined-security-roles)

## <a name="install-the-collaboration-controls-solutions"></a>Installer les solutions de contrôles collaboration

Vous allez installer les contrôles Collaboration dans votre environnement dataverse via [Microsoft AppSource.](https://appsource.microsoft.com/en-us/product/dynamics-365/mscm.collaboration-toolkit-preview?flightCodes=collaborationcontrols&signInModalType=2&ctaType=1)

Vous ne pourrez configurer et utiliser les composants de votre propre application basée sur des modèles qu’après avoir accédé à [Microsoft AppSource](https://appsource.microsoft.com/en-us/product/dynamics-365/mscm.collaboration-toolkit-preview?flightCodes=collaborationcontrols&signInModalType=2&ctaType=1)  et installé des contrôles Collaboration dans votre environnement dataverse.

Les contrôles de collaboration incluent les solutions suivantes :

|**Solutions des paramètres** | **Objectif** |
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

Pour installer les solutions, accédez à [Microsoft AppSource](https://appsource.microsoft.com/en-us/product/dynamics-365/mscm.collaboration-toolkit-preview?flightCodes=collaborationcontrols&signInModalType=2&ctaType=1) et effectuez les étapes suivantes :

1. Sélectionnez **le bouton Obtenir maintenant** .

   :::image type="content" source="../assets/images/collaboration-control/preview-form.png" alt-text="Capture d’écran du bouton Obtenir maintenant pour afficher le contrôle Collaboration."border="true":::

1. Connectez-vous avec votre compte, remplissez le formulaire et **sélectionnez Continuer**.

   :::image type="content" source="../assets/images/collaboration-control/overview.png" alt-text="Capture d’écran du contrôle Collaboration de vue d’ensemble." border="true":::

   :::image type="content" source="../assets/images/collaboration-control/collaboration-controls-preview.png" alt-text="Capture d’écran de l’aperçu du contrôle Collaboration d’installation." border="true":::

1. Vous serez dirigé vers Power Platform Administration Center. Sélectionnez un environnement dans le menu déroulant et acceptez les termes et les instructions de stratégie.

   > [!TIP]
   > Si vous voyez une erreur d’autorisation lorsque vous sélectionnez l’environnement, essayez de sélectionner en dehors du menu déroulant de l’environnement pour voir si cela résout le problème.

   :::image type="content" source="../assets/images/collaboration-control/install-environment.png" alt-text="La capture d’écran est un exemple d’environnement de contrôle de collaboration d’installation." border="true":::

1. Sélectionnez **Installer**, l’installation peut prendre environ 15 minutes.

1. [https://make.powerapps.com/](https://make.powerapps.com/)Atteindre , [https://make.preview.powerapps.com/](https://make.preview.powerapps.com/) est également pris en charge si vous êtes inscrit à la préversion de Power Apps.

1. Vérifiez que vous êtes dans l’environnement dans lequel les contrôles sont installés, car vous pouvez afficher l’environnement et le modifier si nécessaire en haut à droite du portail Power Apps.

1. Sélectionnez l’onglet **Solutions** pour afficher toutes les solutions que vous avez installées dans l’environnement approprié.

   :::image type="content" source="../assets/images/collaboration-control/solutions.png" alt-text="Capture d’écran montrant l’onglet Solutions pour afficher tous les contrôles de collaboration de solutions." border= "true":::

> [!NOTE]
> Les contrôles collaboration sont en préversion et les éléments peuvent changer au fil du temps, ce qui peut entraîner des changements cassants. Les contrôles collaboration ne sont pas pris en charge dans les environnements de production.

Une fois l’installation réussie de toutes les solutions de collaboration dans votre environnement, vous serez en mesure de créer une nouvelle application basée sur des modèles qui peut tirer parti des fonctionnalités de contrôle collaboration.
