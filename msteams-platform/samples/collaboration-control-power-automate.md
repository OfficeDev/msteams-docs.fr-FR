---
title: Application de contrôle Power Automate dans Collaboration
author: surbhigupta
description: Dans ce module, découvrez Power Automate dans l’application de contrôle Collaboration dans Microsoft Teams et comment créer une application Azure.
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: 975d5fdd923d96ae1daa649795259a05904b6921
ms.sourcegitcommit: f2ac771cbd608e872604e9ac8ffec2d08f55ee1a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/04/2022
ms.locfileid: "68373051"
---
# <a name="power-automate"></a>Power Automate

Power Automate peut être utilisé pour automatiser les flux de travail autour de votre application Gestionnaire de collaboration. Par exemple, créez automatiquement des tâches lorsqu’un nouvel enregistrement est créé.

Le connecteur de contrôle de collaboration permet aux développeurs d’accéder aux API de contrôle collaboration par des déclencheurs ou des actions dans des workflows automatisés dans Microsoft Power Automate, Microsoft Power Apps et Azure Logic Apps.

> [!NOTE]
> Actuellement, les contrôles de collaboration sont disponibles uniquement en [préversion publique des développeurs](~/resources/dev-preview/developer-preview-intro.md).

Dans cette version, le connecteur permet aux créateurs de configurer des déclencheurs :

1. Lors de la création d’une session de collaboration.
1. Lorsqu’une tâche de planificateur est créée ou modifiée.

Il inclut également un ensemble d’API de contrôles de collaboration et de tâches qui peuvent être appelées avec un flux. Les actions du connecteur se trouvent dans les sélections d’étapes de flux de travail. Le connecteur lui-même se trouve sur les connecteurs personnalisés avec des options configurables. Pour utiliser le connecteur dans votre solution, il est nécessaire de créer un Azure App approuvé par votre environnement pour exécuter les flux.

## <a name="create-an-azure-app"></a>Créer un Azure App

Dans le [Portail Azure](https://ms.portal.azure.com/#home) de gestion Azure Active Directory, connectez-vous à votre compte avec les autorisations appropriées pour ajouter une application utilisateur à votre environnement en procédant comme suit :

1. Dans la page d’accueil de Portail Azure, sélectionnez **Azure Active Directory**. Dans Azure Active Directory, sélectionnez la liste déroulante pour **Ajouter** , puis sélectionnez **Inscription d’application**.

   :::image type="content" source="../assets/images/collaboration-control/azure-active-directory-home-portal.png" alt-text="Capture d’écran d’un exemple montrant comment ajouter une nouvelle inscription d’application.":::

   :::image type="content" source="../assets/images/collaboration-control/new-app-registration.png" alt-text="Capture d’écran d’un exemple montrant comment ajouter une nouvelle inscription d’application.":::

1. Dans l’inscription de l’application, définissez le nom de votre application et ajoutez l’URI de redirection web sur `https://global.consent.azure-apim.net/redirect`.

   :::image type="content" source="../assets/images/collaboration-control/register-an-application.png" alt-text="Capture d’écran d’un exemple montrant comment inscrire une application.":::

1. Dans la section Octroi implicite et flux hybrides, sélectionnez les jetons d’accès et les jetons d’ID.

   :::image type="content" source="../assets/images/collaboration-control/authorisation-endpoint-tokens.png" alt-text="Capture d’écran d’un exemple montrant les jetons et les jetons d’ID.":::

1. Sélectionnez Autorisation d’API dans le volet gauche, **sélectionnez Ajouter une autorisation**, puis recherchez l’autorisation **CRM dynamique** .

   :::image type="content" source="../assets/images/collaboration-control/dynamic-crm.png" alt-text="La capture d’écran est un exemple qui montre comment ajouter une autorisation.":::

1. Veillez à sélectionner **user_impersonation** dans Autorisations après avoir sélectionné Dynamics CRM.

   :::image type="content" source="../assets/images/collaboration-control/admin-consent-required.png" alt-text="Capture d’écran d’un exemple montrant comment activer la case à cocher user_impersonation.":::

1. Dans la page Certificats & Secrets, ajoutez une **nouvelle clé secrète client** et enregistrez la valeur pour une utilisation ultérieure lors de la configuration de la sécurité du connecteur.

   :::image type="content" source="../assets/images/collaboration-control/copy-new-secret-value.png" alt-text="Capture d’écran d’un exemple montrant comment copier une nouvelle valeur secrète.":::

1. Dans la page Vue d’ensemble de l’application, copiez **l’ID d’application (client)** et enregistrez-le pour une utilisation ultérieure lors de la configuration de la sécurité du connecteur.

   :::image type="content" source="../assets/images/collaboration-control/application-client-ID.png" alt-text="Capture d’écran d’un exemple montrant comment enregistrer l’ID client":::

Votre application Azure est maintenant définie et vous devez l’ajouter en tant qu’application utilisateur dans votre environnement.

## <a name="add-azure-app-to-power-automate-environment"></a>Ajouter une application Azure à l’environnement Power Automate

1. Ouvrez le portail Power Apps, dans le coin supérieur droit, sélectionnez **les paramètres** et ouvrez **Administration centre**.

   :::image type="content" source="../assets/images/collaboration-control/power-apps-interface.png" alt-text="Capture d’écran d’un exemple montrant l’interface Power Apps.":::

1. Dans le Centre d’administration, sélectionnez **Environnement** dans le volet gauche, puis sélectionnez votre environnement dans la liste que vous souhaitez ajouter à l’application connecteur.

   :::image type="content" source="../assets/images/collaboration-control/power-platform-admin-center.png" alt-text="Capture d’écran d’un exemple montrant comment ajouter une application de connecteur.":::

1. Dans la page des détails de l’environnement, sélectionnez **Paramètres**.

   :::image type="content" source="../assets/images/collaboration-control/settings-environment.png" alt-text="Capture d’écran d’un exemple montrant comment sélectionner des paramètres.":::

1. Dans la page détails des paramètres, sélectionnez **La section Utilisateurs + autorisations** , puis **les utilisateurs de l’application**.

   :::image type="content" source="../assets/images/collaboration-control/users-link.png" alt-text="La capture d’écran est un exemple montrant le lien utilisateur de l’application.":::

1. Dans la page Utilisateurs de l’application, sélectionnez **l’utilisateur + Nouvel utilisateur d’application**. **La fenêtre Créer un utilisateur d’application** s’affiche.

   :::image type="content" source="../assets/images/collaboration-control/new-app-user.png" alt-text="La capture d’écran est un exemple montrant le nouvel utilisateur d’application.":::

1. Sélectionnez **+ Ajouter une application**.

   :::image type="content" source="../assets/images/collaboration-control/create-new-app-user.png" alt-text="Capture d’écran d’un exemple montrant comment créer un utilisateur d’application.":::

1. Sélectionnez votre application dans la zone de recherche, puis sélectionnez Ajouter à nouveau.

   :::image type="content" source="../assets/images/collaboration-control/add-app-aad.png" alt-text="Capture d’écran d’un exemple montrant comment ajouter une application à partir d’Azure Active Directory.":::

Une fois l’application ajoutée, **définissez l’unité métier** et les **rôles de sécurité** sur votre application de connecteur. Sélectionnez **Créer** et votre application figure dans la liste. Avec l’utilisateur d’application défini dans l’environnement, nous pouvons passer à la configuration du connecteur personnalisé.

## <a name="custom-connector-configuration"></a>Configuration du connecteur personnalisé

1. Ouvrez PowerApps ou Power Automate, puis sélectionnez le menu **Connecteurs personnalisés** . Sélectionnez **Modifier** pour le connecteur Collaboration.

   :::image type="content" source="../assets/images/collaboration-control/collaboration-connector.png" alt-text="Capture d’écran montrant comment sélectionner modifier le menu du connecteur personnalisé.":::
1. Sous l’onglet Informations générales, entrez l’hôte avec l’adresse du domaine d’instance Dynamique 365 (sans le https://).

   :::image type="content" source="../assets/images/collaboration-control/general-information.png" alt-text="La capture d’écran est un exemple qui montre les informations générales.":::

1. Sous l’onglet Sécurité, entrez les entrées suivantes :

   * Clé secrète client : utilisez votre valeur de secret d’application enregistrée dans l’entrée.
   * ID client : votre application Azure (ID client).
   * URL de la ressource : URL de votre instance Dynamic 365 (`https://org.crm.dynamics.com/`).
   * Étendue : identique à celle ci-dessus. Suffixe par défaut (`https://org.crm.dynamics.com/.default`).

   :::image type="content" source="../assets/images/collaboration-control/dynamic-365-instance.png" alt-text="Capture d’écran d’un exemple montrant l’instance Dynamic 365.":::

1. Sélectionnez **Mettre à jour le connecteur** pour enregistrer les modifications et autoriser votre flux à établir des connexions.

   :::image type="content" source="../assets/images/collaboration-control/custom-connector.png" alt-text="Capture d’écran d’un exemple montrant le connecteur personnalisé.":::

## <a name="how-to-invoke-the-connector"></a>Comment appeler le connecteur  

Les déclencheurs et les actions sont prédéfinis avec une entrée et une sortie configurables en tant qu’étape de flux de travail. Ajout de l’étape de flux de travail à la position de flux de travail appropriée avec une configuration d’entrée et de sortie correcte pour définir quand le déclencheur ou l’action doit être appelé.

  :::image type="content" source="../assets/images/collaboration-control/invoke-the-connector.png" alt-text="La capture d’écran est un exemple qui montre comment appeler le connecteur.":::

### <a name="triggers-and-actions-supported-with-connector"></a>Déclencheurs et actions pris en charge avec le connecteur

Les déclencheurs et actions suivants sont pris en charge dans un flux :

* **Déclenche**

  1. Lors de la création d’une session de collaboration.

      :::image type="content" source="../assets/images/collaboration-control/colab-session-created-preview.png" alt-text="Capture d’écran montrant la session collaboration créée.":::

      **Portée:** Étendue à limiter, quelles lignes peuvent déclencher le flux.

      **Exécutez comme suit :** Utilisateur en cours d’exécution pour les étapes dans lesquelles les connexions d’appelant sont utilisées.

  1. Lorsqu’une tâche est créée ou modifiée

      :::image type="content" source="../assets/images/collaboration-control/task-created.png" alt-text="Capture d’écran d’un exemple montrant que la tâche est créée ou modifiée.":::

      Par défaut, la tâche du planificateur de déclencheur est désactivée et ne se déclenche pas. Pour l’activer, l’administrateur du locataire doit suivre les étapes suivantes :

      1. Créez un ticket de support sous le chemin d’accès Contrôles/Paramètres Power Apps/Collaboration.
      1. Demandez que votre environnement soit activé pour le connecteur Collaboration et qu’il fournisse votre URL d’environnement (par défaut) ou votre ID d’organisation.  
      1. Vous pouvez ajouter l’exemple de texte suivant à votre demande de support : « Activer l’URL de l’environnement : `url` pour le connecteur de collaboration ».
      1. Pour ouvrir un ticket de support, consultez [Obtenir de l’aide et du support](/power-platform/admin/get-help-support)

* **Actions**

  1. Commencer la session de collaboration

      :::image type="content" source="../assets/images/collaboration-control/begin-collab-session.png" alt-text="Capture d’écran d’un exemple montrant comment commencer une session de collaboration.":::

     Cette action d’étape crée une session de collaboration pour votre entité métier dataverse :

      * **Nom de l’application :** Le nom de l’application associée, par exemple, peut être « Gestionnaire de collaboration for Loans » ou « Gestionnaire de collaboration for Closed Loan Auditing ».
      * **Nom de l’entité racine de collaboration :** Le type d’enregistrement d’application (nom de la table), par exemple, peut être « msfi_loanapplication » pour une Gestionnaire de collaboration pour l’application Loans.
      * **ID d’entité racine de collaboration :** ID de l’enregistrement d’application associé, par exemple, peut être l’ID d’un enregistrement d’application de prêt.  

      ***Options avancées***

      **Métadonnées (avancées) :** Ajoute des métadonnées pour une session de collaboration.

        * **Type OData :** Ce champ doit être fourni si l’autre clé/valeur est définie et doit correspondre exactement à #Microsoft.Dynamics.CRM.m365_collaborationmetadata.
        * **Clé:** Clé associée à l’attribut de métadonnées.
        * **Valeur:** Valeur associée à l’attribut de métadonnées.

  1. Récupérer une session de collaboration

      ::image type="content » source= ».. /assets/images/collaboration-control/retrieve-collab-session.png » alt-text="Capture d’écran est un exemple montrant comment récupérer une session de collaboration. »:::

     Cette action d’étape retourne la session de collaboration qui correspond aux entrées fournies :

     * **Nom de l’application :** Contexte de nom d’application pour la session de collaboration.
     * **ID d’entité racine de collaboration :** ID d’entité métier pour la session de collaboration.  
     * **Nom de l’entité racine de collaboration :** Type d’entité métier pour la session de collaboration.

  1. Mettre à jour la session collaboration

      :::image type="content" source="../assets/images/collaboration-control/update-collab-session.png" alt-text="Capture d’écran d’un exemple montrant comment mettre à jour la session de collaboration.":::

     Cette action d’étape met à jour une session de collaboration existante :

     * **ID racine de collaboration :** GUID pour l’enregistrement racine/session de collaboration cible.
     * **ID d’entité racine de collaboration :** ID d’entité métier auquel la session de collaboration fait référence.
     * **Nom de l’entité racine de collaboration :** Nom du type d’entité métier auquel la session de collaboration fait référence.

     ***Options avancées :***

      **Créer des métadonnées (avancé) :** Ajoute d’autres métadonnées à un enregistrement de session de collaboration.

      * **Type OData :** Ce champ doit être fourni si l’autre clé/valeur est définie et doit correspondre exactement à #Microsoft.Dynamics.CRM.m365_collaborationmetadata.
      * **Clé:** Clé associée à l’attribut de métadonnées.
      * **Valeur:** Valeur associée à l’attribut de métadonnées.

      **Mettre à jour les métadonnées (avancé) :** Mises à jour métadonnées existantes sur un enregistrement de session de collaboration.

      * **Type OData :** Ce champ doit être fourni si l’autre clé/valeur est définie et doit correspondre exactement à #Microsoft.Dynamics.CRM.m365_collaborationmetadata.
      * **Clé:** Clé associée à l’attribut de métadonnées à mettre à jour.
      * **Valeur:** Valeur associée à l’attribut de métadonnées.

      **Supprimer les métadonnées (avancé) :** Supprime toutes les métadonnées existantes sur un enregistrement de session de collaboration.

      * **Type OData :** Ce champ doit être fourni si l’autre clé/valeur est définie et doit correspondre exactement à #Microsoft.Dynamics.CRM.m365_collaborationmetadata.
      * **Clé:** Clé associée à l’attribut de métadonnées à supprimer.

  1. Associer une carte de collaboration (externe)

      :::image type="content" source="../assets/images/collaboration-control/associate-collab-map.png" alt-text="Capture d’écran d’un exemple montrant comment associer une carte de collaboration.":::

     Cette action d’étape crée un mappage d’une entité de collaboration externe (hors dataverse) avec votre session de collaboration :

     * **ID racine de collaboration :** Identificateur unique de session de collaboration à mapper à une entité collaborative.
     * **ID externe de la carte de collaboration :** ID de ressource collaborative externe à mapper.
     * **Nom de l’entité de carte de collaboration :** Nom du type d’entité collaborative externe à mapper.

     ***Options avancées :***

     **Métadonnées:** Ajoutez des métadonnées pour une carte de collaboration.
     * **Type OData :** Ce champ doit être fourni si l’autre clé/valeur est définie et doit correspondre exactement à #Microsoft.Dynamics.CRM.m365_collaborationmetadata.
     * **Clé:** Clé associée à l’attribut de métadonnées.
     * **Valeur:** Valeur associée à l’attribut de métadonnées.

  1. Associer une carte de collaboration (interne)

      :::image type="content" source="../assets/images/collaboration-control/associate-collab-map-internal.png" alt-text="Capture d’écran d’un exemple montrant comment associer une carte de collaboration interne.":::

     Cette action d’étape crée un mappage d’une entité de collaboration (table dataverse) avec votre session de collaboration. Les paramètres internes sont destinés à créer des mappages entre des entités/tables Dataverse internes uniquement.

     * **ID racine de collaboration :** Identificateur unique de session de collaboration à mapper à une entité collaborative.
     * **ID d’entité de carte de collaboration :** ID d’entité collaborative Dataverse à mapper.
     * **Nom de l’entité de carte de collaboration :** Nom du type d’entité collaborative Dataverse à mapper.

     ***Options avancées :***

     **Métadonnées (avancé)** Ajoutez des métadonnées pour une carte de collaboration.

     * **Type OData :** Ce champ doit être fourni si l’autre clé/valeur est définie et doit correspondre exactement à #Microsoft.Dynamics.CRM.m365_collaborationmetadata
     * **Clé:** Clé associée à l’attribut de métadonnées
     * **Valeur:** Valeur associée à l’attribut de métadonnées

  1. Mettre à jour la carte de collaboration

      :::image type="content" source="../assets/images/collaboration-control/update-collab-map.png" alt-text="Capture d’écran d’un exemple montrant comment mettre à jour la carte de collaboration.":::

     Cette étape met à jour une carte de collaboration existante :

     * **ID de carte de collaboration :** Identificateur unique de la carte de collaboration à mettre à jour.
     * **ID d’entité de carte de collaboration :** ID d’entité collaborative à mapper. Cette valeur doit être vide si l’ID externe est fourni
     * **Nom de l’entité carte de collaboration**
     * **ID externe de la carte de collaboration :** ID de ressource collaborative externe à mapper. Cette valeur doit être vide si l’ID d’entité est fourni.  

     ***Options avancées :***

     **Créer des métadonnées :** Ajoute d’autres métadonnées à un enregistrement de carte de collaboration.

     * **Type OData :** Ce champ doit être fourni si l’autre clé/valeur est définie et doit correspondre exactement à #Microsoft.Dynamics.CRM.m365_collaborationmetadata.
     * **Clé:** Clé associée à l’attribut de métadonnées.
     * **Valeur:** Valeur associée à l’attribut de métadonnées.

     **Mettre à jour les métadonnées :** Mises à jour métadonnées existantes sur un enregistrement de carte de collaboration.

     * **Type OData :** Ce champ doit être fourni si l’autre clé/valeur est définie et doit correspondre exactement à #Microsoft.Dynamics.CRM.m365_collaborationmetadata
     * **Clé:** Clé associée à l’attribut de métadonnées à mettre à jour
     * **Valeur:** Valeur associée à l’attribut de métadonnées

     **Supprimer les métadonnées :** Supprime toutes les métadonnées existantes sur un enregistrement de carte de collaboration.

     * **Type OData :** Ce champ doit être fourni si l’autre clé/valeur est définie et doit correspondre exactement à #Microsoft.Dynamics.CRM.m365_collaborationmetadata.
     * **Clé:** Clé associée à l’attribut de métadonnées à supprimer.

  1. Obtenir les métadonnées de collaboration

      :::image type="content" source="../assets/images/collaboration-control/get-collab-metadata.png" alt-text="La capture d’écran est un exemple montrant comment obtenir des métadonnées de collaboration.":::

     Cette action d’étape répertorie toutes les métadonnées correspondant au filtre spécifié.

     **Filtre:** Filtre à appliquer à la requête de métadonnées.
     Exemple de récupération de toutes les métadonnées liées à un ID d’entité de carte de collaboration  
     m365_entityname eq 'm365_collaborationmap' et m365_entityid eq 'GUID'

  1. Créer une tâche de planificateur

      :::image type="content" source="../assets/images/collaboration-control/create-planner-task.png" alt-text="Capture d’écran d’un exemple montrant comment créer une tâche de planificateur.":::

     Cette action d’étape crée une tâche du Planificateur graphe à l’aide d’une table virtuelle de tâche du Planificateur de contrôles de collaboration :

     * **ID racine de collaboration (obligatoire) :** Identificateur unique de session de collaboration
     * **ID de plan (obligatoire) :** ID de plan auquel appartient la tâche
     * **Titre (obligatoire) :** Titre de la tâche
     * **Affectations:** Objet au format json qui représente toutes les affectations d’une tâche. Voir, [type de ressource plannerAssignments](/graph/api/resources/plannerassignments)
     * **ID de compartiment :** ID de compartiment auquel les tâches appartiennent.
     * **Priorité:** Priorité de la tâche. La valeur croissante 0 et 10 (inclusive) est inférieure à la priorité.

     ***Options avancées :***

     * **Nombre d’éléments de liste de vérification actifs** (avancé) : nombre d’éléments de liste de vérification dont la valeur est définie sur false représentant des éléments incomplets.
     * **Catégories appliquées :** Objet de formateur json qui représente toutes les catégories à appliquer pour la tâche. Consultez le [type de ressource plannerAppliedCategories](/graph/api/resources/plannerappliedcategories).
     * **Priorité de l’assignateur :** Indicateurs de valeur de chaîne utilisés pour commander des éléments de ce type dans une vue de liste. Voir, [à l’aide d’indicateurs de commande dans le Planificateur](/graph/api/resources/planner-order-hint-format)
     * **Nombre d’éléments de liste de vérification :** Nombre d’éléments de liste de vérification présents sur la tâche.
     * **Terminé par :** Objet au format json qui représente l’identité de l’utilisateur qui a terminé la tâche. Voir, [type de ressource identitySet](/graph/api/resources/identityset)
     * **ID de thread de conversation :** ID de thread de la conversation sur la tâche. Il s’agit de l’ID de l’objet de thread de conversation créé dans le groupe.
     * **Créé par :** Objet au format json qui représente l’identité de l’utilisateur qui a créé la tâche. Voir, [type de ressource identitySet](/graph/api/resources/identityset)
     * **Date d’échéance :** Date et heure d’échéance de la tâche. Le type d’horodatage représente les informations de date et d’heure au moyen du format ISO 8601. Il est toujours au format d’heure UTC. Par exemple, minuit UTC le 1er janvier 2014 est 2014-01-01T00:00:00Z.
     * **Indicateur de commande :** Indicateur utilisé pour commander des éléments de ce type dans une vue de liste. Le format est défini comme décrit à [l’aide d’indicateurs de commande dans le Planificateur](/graph/api/resources/planner-order-hint-format).
     * **Pourcentage terminé :** Pourcentage d’achèvement des tâches (0-100)
     * **Type d’aperçu :** Cela définit le type de préversion qui s’affiche sur la tâche. Les valeurs possibles sont : automatique, noPreview, checklist, description, reference.
     * **Nombre de références :** Nombre de références externes qui existent sur la tâche.
     * **Date de début :** Date et heure de début de la tâche. Le type d’horodatage représente les informations de date et d’heure au moyen du format ISO 8601. Il est toujours au format d’heure UTC. Par exemple, minuit UTC le 1er janvier 2014 est 2014-01-01T00:00:00Z.

  1. Tâche Obtenir le planificateur

      :::image type="content" source="../assets/images/collaboration-control/get-planner-task.png" alt-text="Capture d’écran d’un exemple montrant la tâche get planner.":::

     Cette action d’étape retourne les données d’une tâche du planificateur à l’aide de la table virtuelle des tâches du Planificateur de contrôles de collaboration :

     **ID de tâche (obligatoire) :** Identificateur unique de tâche

  1. Tâche du Planificateur de mise à jour

      :::image type="content" source="../assets/images/collaboration-control/update-planner-task-preview.png" alt-text="Capture d’écran montrant la tâche Du planificateur de mise à jour.":::

     Cette action d’étape met à jour un enregistrement de tâche du planificateur à l’aide d’une table virtuelle de tâches du Planificateur de contrôles de collaboration.

     * **ID de tâche (obligatoire) :** Identificateur unique de tâche.
     * **Affectations:** Objet au format json qui représente toutes les affectations d’une tâche. Voir le type de ressource plannerAssignments - Microsoft Graph v1.0 | Microsoft Docs.  
     * **ID de compartiment :** ID de compartiment à l’emplacement auquel la tâche appartient.  
     * **Détails de la tâche du Planificateur :** Représente les informations supplémentaires sur une tâche.
     * **Date d’échéance :** Date et heure d’échéance de la tâche. Le type d’horodatage représente les informations de date et d’heure au moyen du format ISO 8601. Il est toujours au format d’heure UTC. Par exemple, minuit UTC le 1er janvier 2014 est 2014-01-01T00:00:00Z.
     * **Priorité:** Priorité de la tâche. La valeur croissante 0 et 10 (inclusive) est inférieure à la priorité.  
     * **Pourcentage terminé :** Pourcentage d’achèvement des tâches (0-100).
     * **Titre:** Titre de la tâche.

     ***Options avancées :***

     * **Catégories appliquées :** Objet au format json qui représente toutes les catégories à appliquer pour la tâche. Consultez le [type de ressource plannerAppliedCategories](/graph/api/resources/plannerappliedcategories).
     * **Priorité de l’assignateur :** Indicateurs de valeur de chaîne utilisés pour commander des éléments de ce type dans une vue de liste. Consultez, [à l’aide d’indicateurs de commande dans le Planificateur](/graph/api/resources/planner-order-hint-format).
     * **ID de thread de conversation :** ID de thread de la conversation sur la tâche. Il s’agit de l’ID de l’objet de thread de conversation créé dans le groupe.
     * **ID racine de collaboration :** Identificateur unique de session de collaboration.
     * **Indicateur de commande :** Indicateur utilisé pour commander des éléments de ce type dans une vue de liste. Le format est défini comme plan ici.
     * **Date de début :** Date et heure de début de la tâche. Le type d’horodatage représente les informations de date et d’heure au moyen du format ISO 8601. Il est toujours au format d’heure UTC. Par exemple, minuit UTC le 1er janvier 2014 est 2014-01-01T00:00:00Z.

**Exemple de scénario de flux**

Voici des exemples de flux :

1. Obtention d’une réponse à partir de Formulaires Microsoft, création d’une session de collaboration et d’une tâche associée.

   :::image type="content" source="../assets/images/collaboration-control/response-submitted.png" alt-text="La capture d’écran est un exemple montrant comment envoyer une nouvelle réponse.":::

1. Chaque fois qu’une session de collaboration est créée, capturez les détails et envoyez une notification par e-mail.

   :::image type="content" source="../assets/images/collaboration-control/colab-session-created-preview.png" alt-text="Capture d’écran d’un exemple montrant la session collaboration créée.":::

> [!NOTE]
> Plusieurs flux peuvent être déclenchés de cette façon pour effectuer différentes actions, à l’aide des données de la réponse de la création de session collaboration.
