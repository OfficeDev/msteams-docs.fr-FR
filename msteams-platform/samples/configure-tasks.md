---
title: Configurer des tâches pour des clients externes dans l’application de contrôle Collaboration
author: surbhigupta
description: Dans ce module, découvrez comment configurer tasks pour les clients externes dans l’application de contrôle Collaboration dans Microsoft Teams.
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: bb98ab632b335717a61499600aef01e652fd0dee
ms.sourcegitcommit: 0bb822b30739e4a532a36764dad2dbf35a81ba29
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2022
ms.locfileid: "67179043"
---
# <a name="configure-tasks-for-external-clients"></a>Configurer des tâches pour des clients externes

Tâches externes qui peuvent être affectées à des utilisateurs qui ne font pas partie de votre organisation ou qui n’ont pas accès à votre application, comme l’affectation d’une tâche à un client.

Pour l’activer, vous aurez besoin d’une étape supplémentaire de passage d’une chaîne XML à chaque instance du contrôle PCF Tasks attaché au composant de sous-grille sur le formulaire MDA souhaité. La chaîne XML est une requête paramétrée qui permet au contrôle d’extraire les données requises d’une table qui contient des informations client.

> [!NOTE]
> Actuellement, les contrôles collaboration sont disponibles uniquement en [préversion publique des développeurs](~/resources/dev-preview/developer-preview-intro.md).

Voici les étapes à suivre pour créer des tâches externes :

1. Créez une entité personnalisée telle que Customer ou réutilisez une entité client existante telle que Contacts.

1. Créez des champs qui contiendront les informations suivantes :
    1. Nom
    1. E-mail
    1. Parent (recherche dans la table parente telle que Inspections)
    > [!NOTE]
    > L’entité client créée ci-dessus est l’endroit où le contrôle de tâche extrait les informations client lors de l’affectation d’une tâche externe. Le champ Parent garantit que l’entité client est liée à un enregistrement d’inspection.

1. Générez un fichier Fetch XML pour permettre au contrôle PCF d’extraire les informations client appropriées.

    **Configurer le schéma XML**

    Voici la définition de schéma pour la configuration des tâches Fetch XML. Toute extraction XML doit être conçue pour répondre aux exigences suivantes :

    * Le résultat de la requête doit retourner les propriétés suivantes pour chaque objet utilisateur :
      * ID
      * displayname
      * e-mail, utilisez l’alias si nécessaire.
    * La requête doit contenir le paramètre **@top** pour permettre à l’appelant de limiter le nombre de résultats.
    * La requête doit avoir **@rootEntityId** paramètre pour filtrer les résultats par des enregistrements associés uniquement, si nécessaire.
    * La requête doit avoir **@useName** paramètre pour autoriser le filtrage des résultats par nom
    * La requête doit avoir **@useIdentifier** paramètre pour autoriser l’extraction uniquement des utilisateurs sélectionnés.

    **Schéma XML de configuration et exemple**

    La configuration du schéma XML extrait les données de la table client. Vous pouvez ajuster le `<fetch/>` nœud pour spécifier votre propre requête afin d’afficher les utilisateurs de n’importe quelle autre table personnalisée.

    > [!NOTE]
    > L’entité ci-dessus, le nom d’attribut et l’attribut d’ordre dans le code XML sont au format **PublisherPrefix_TableColumn** .

    ```xml
    
    <custom-tasks> 
    <custom-task id="external" name="External" for="guest"> 
    <fetch top="@top"> 
    <entity name="[Name of table, e.g. Crb2891_customer]"> 
    <attribute name="[Name of ID column, e.g. Crb2891_customerid]" alias="id" /> 
    <attribute name="[Name of primary name column, e.g. Crb2891_name]" alias="displayname" /> 
    <attribute name="[Name of email column, e.g. Crb2891_email]" alias="email" /> 
    <order attribute ="[Name of primary name column, e.g. Crb2891_name]" descending="false" /> 
    <filter type="and"> 
    <condition attribute="[Name of parent lookup column, e.g. Crb2891_parent]" operator="eq" value="@rootEntityId" /> 
    <condition attribute="[Name of primary name column, e.g. Crb2891_name]" operator="like" value="@userName" /> 
    <condition attribute="[Name of email column, e.g. Crb2891_email]" operator="like" value="@userIdentifier" /> 
    </filter> 
    </link-entity> 
    </entity> 
    </fetch> 
    </custom-task> 
    </custom-tasks> 
    
    ```

1. Liez les contrôles Task au sous-menu dans le concepteur de formulaires classique. Sélectionnez **Enregistrer** , puis **sélectionnez Basculer vers la version classique**.

1. Parcourez le concepteur de formulaires classique jusqu’à ce que vous trouviez l’onglet **Tâches** . Double-cliquez sur le sous-menu pour ouvrir sa boîte de dialogue de propriétés.

    :::image type="content" source="~/assets/images/collaboration-control/subgrid-property.png" alt-text="Boîte de dialogue Propriétés des tâches":::

1. Dans la boîte de dialogue de propriétés, définissez les propriétés comme indiqué dans l’image suivante :

    :::image type="content" source="~/assets/images/collaboration-control/tasks-property.png" alt-text="Paramètres de propriété Tasks":::

1. Accédez à l’onglet Contrôles et sélectionnez :::image type="icon" source="~/assets/images/collaboration-control/edit-icon.png" alt-text="Modifier les tâches"::: sur la propriété Tâches personnalisées pour ajouter le code XML fetch généré ci-dessus.

1. Coller le code XML fetch

    :::image type="content" source="~/assets/images/collaboration-control/set-fetchproperties.png" alt-text="Récupérer les paramètres de propriété XML":::

    :::image type="content" source="~/assets/images/collaboration-control/custom-tasksproperty.png" alt-text="Récupérer les paramètres de propriété personnalisée XML":::

1. Sélectionnez **OK** dans Configurer la propriété « Tâches personnalisées » et définir les fenêtres Propriétés.

1. Enregistrer et publier.
