---
title: Application avec contrôles collaboration
author: surbhigupta
description: Dans ce module, découvrez comment créer une application basée sur des modèles avec des contrôles collaboration pour Teams et comment ajouter des contrôles Collaboration à l’application.
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: e712c55dd4543edda9115751be09d81d1795f02b
ms.sourcegitcommit: c1032ea4f48c4bbf5446798ff7d46d7e6e9f55d2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2022
ms.locfileid: "68027339"
---
# <a name="create-a-new-model-driven-app-with-collaboration-controls-for-teams"></a>Créer une application basée sur des modèles avec des contrôles collaboration pour Teams

Les contrôles de collaboration sont conçus pour les [applications basées sur des modèles](/power-apps/maker/model-driven-apps/model-driven-app-overview). La section suivante explique comment créer une application pilotée par modèle.

> [!NOTE]
> Actuellement, les contrôles collaboration sont disponibles uniquement en [préversion publique des développeurs](~/resources/dev-preview/developer-preview-intro.md).

## <a name="create-a-model-driven-application"></a>Créer une application pilotée par modèle

1. Ouvrez [https://make.powerapps.com.](https://make.powerapps.com/) ou [https://make.preview.powerapps.com.](https://make.preview.powerapps.com/)

1. Sélectionnez **Solutions** dans le volet gauche.

1. Sélectionnez **Nouvelle solution**, afin de pouvoir fournir une maison pour toutes vos personnalisations futures.

   :::image type="content" source="../assets/images/collaboration-control/new-solution.png" alt-text="La capture d’écran est un exemple montrant la nouvelle solution.":::

1. Indiquez le nom et l’éditeur de votre nouvelle solution. Cette solution conservera votre Gestionnaire de collaboration personnalisé.

   :::image type="content" source="../assets/images/collaboration-control/collaboration-manager.png" alt-text="La capture d’écran est un exemple montrant le gestionnaire de collaboration.":::

1. Sélectionnez **Créer**.

1. Une fois la solution créée, elle apparaît dans votre liste de solutions. Sélectionnez votre solution pour l’ouvrir.

1. Avant de créer votre application, créez une maison pour vos données. sélectionnez **Nouvelle** > **table** pour commencer.

     :::image type="content" source="../assets/images/collaboration-control/create-table.png" alt-text="La capture d’écran décrit comment créer une table.":::

1. Donnez un nom à votre table. Sous **Options avancées**, sélectionnez **Création d’une nouvelle activité**.

   :::image type="content" source="../assets/images/collaboration-control/new-activity.png" alt-text="La capture d’écran décrit comment créer une activité.":::

1. Sélectionnez **Enregistrer**.

1. Une fois que vous avez terminé de créer votre table, vous pouvez la personnaliser en ajoutant des colonnes, des relations et bien plus encore (facultatif).

1. Vous pouvez maintenant créer une application pilotée par modèle en sélectionnant **nouvelle** >  > **application pilotée par modèle d’application.**

   :::image type="content" source="../assets/images/collaboration-control/model-driven-app.png" alt-text="La capture d’écran est un exemple montrant la nouvelle application pilotée par modèle.":::

1. Choisissez le nouveau **concepteur d’applications modernes (préversion)** pour ouvrir la nouvelle application.

   :::image type="content" source="../assets/images/collaboration-control/model-driven-app-blank.png" alt-text="La capture d’écran est un exemple qui montre la nouvelle application pilotée par modèle vide.":::

1. Sélectionnez **Créer.**

1. Donnez un nom à votre application, puis **sélectionnez Créer.**

   :::image type="content" source="../assets/images/collaboration-control/collaboration-manager-for-inspection.png" alt-text="La capture d’écran est un exemple montrant le gestionnaire de collaboration à des fins d’inspection.":::

1. Sélectionnez **Ajouter une page.**

1. Sélectionnez **l’affichage et le formulaire basés sur table.**

   :::image type="content" source="../assets/images/collaboration-control/table-based.png" alt-text="La capture d’écran est un exemple montrant la vue et le formulaire basés sur une table.":::

1. Sélectionnez **Suivant.**

1. Recherchez et sélectionnez la table que vous avez créée précédemment.

   :::image type="content" source="../assets/images/collaboration-control/table-view-form-pages.png" alt-text="La capture d’écran est un exemple montrant les pages de formulaire en mode Tableau.":::

1. Sélectionnez **Ajouter.**

1. Sélectionnez **Publier** pour enregistrer et publier votre application.

1. Sélectionnez **Lire** pour tester votre nouvelle application.

Vous avez maintenant créé avec succès une application basée sur des modèles.

## <a name="add-collaboration-controls-to-your-application"></a>Ajouter des contrôles collaboration à votre application

Voici les étapes à suivre pour ajouter à l’application créée des fonctionnalités de contrôle collaboration telles que des tâches, des réunions, des fichiers et des notes :

1. Pour inclure les onglets Tâches, Réunions et Notes, vous devez modifier le formulaire Informations principales. Pour commencer, revenez à l’explorateur et sélectionnez votre solution.

1. Sélectionnez la table que vous avez créée dans [Créer une application basée sur des modèles pour Teams.](#create-a-new-model-driven-app-with-collaboration-controls-for-teams)

1. Accédez à l’onglet Formulaires de votre tableau.

     :::image type="content" source="../assets/images/collaboration-control/forms-tab.png" alt-text="La capture d’écran est un exemple montrant l’onglet Formulaires de votre tableau.":::

1. Sélectionnez le formulaire Informations de type **Main** pour l’ouvrir dans le concepteur de formulaires.

1. Une fois que vous êtes dans le concepteur de formulaires, appuyez et faites glisser un **onglet de 1 colonne** à partir de la section **Composants** .

     :::image type="content" source="../assets/images/collaboration-control/components.png" alt-text="La capture d’écran est un exemple qui montre les composants de Power Apps.":::

1. Après avoir sélectionné l’onglet, renommez l’onglet « Tâches » dans le volet de propriétés.

1. Sélectionnez le nom de l’onglet pour sélectionner la section complète, puis **sélectionnez Développer le premier composant vers l’onglet complet** dans le volet Propriétés. Cela est nécessaire, car les contrôles Collaboration sont mieux affichés dans les affichages d’onglets complets.

    :::image type="content" source="../assets/images/collaboration-control/tasks-pane.png" alt-text=" La capture d’écran décrit comment sélectionner le premier composant dans l’onglet complet.":::

     :::image type="content" source="../assets/images/collaboration-control/expand-first-component.png" alt-text=" La capture d’écran décrit comment étendre le premier composant à l’onglet complet.":::

1. Développez la catégorie Collaboration (préversion) dans le tiroir de contrôles et faites glisser le contrôle Tâches (préversion) vers la section sous forme Tâches.

     :::image type="content" source="../assets/images/collaboration-control/collab-preview.png" alt-text="Aperçu du contrôle sur la section sous forme de tâches":::

3. Définissez la table sur Activités & sélectionnez Terminé.

     :::image type="content" source="../assets/images/collaboration-control/select-table-activities.png" alt-text="Sélectionner la table pour les activités":::

5. Sélectionnez « Masquer l’étiquette » dans les propriétés.

     :::image type="content" source="../assets/images/collaboration-control/hide-label-properties.png" alt-text="Sélectionner masquer l’étiquette":::

1. Le contrôle Tâches s’affiche maintenant.

     :::image type="content" source="../assets/images/collaboration-control/new-collab-control.png" alt-text="Affichage du contrôle Tâches":::

1. Répétez les étapes tâches pour ajouter des contrôles Approbations, Fichiers, Réunions et Notes à votre application.
1. Une fois tous les contrôles ajoutés, vous verrez les contrôles affichés ci-dessous dans le Concepteur de formulaires. Si un contrôle ne s’affiche pas dans le Concepteur de formulaires, par exemple, affiche un formulaire vide, exécutez votre application dans Power Apps et la présence d’une page « configurer » ou d’un « état vide » signifie que le contrôle a été correctement ajouté.

     :::image type="content" source="../assets/images/collaboration-control/new-collab-approval.png" alt-text="Concepteur de formulaires controls":::

1. Vous pouvez maintenant exécuter votre application d’alimentation dans Power Apps en la sélectionnant.

     :::image type="content" source="../assets/images/collaboration-control/collaboration-manager-for-inspections-power-apps.png" alt-text="Gestionnaire de collaboration pour les inspections":::

1. Créez un enregistrement en sélectionnant **+ Nouveau** , puis ouvrez l’enregistrement.

     :::image type="content" source="../assets/images/collaboration-control/power-apps-open-the-record.png" alt-text="La capture d’écran est un exemple montrant les applications power qui ouvrent l’enregistrement.":::

1. Vous pouvez maintenant voir les vues de chaque onglet qui ressemblent à l’image suivante :

     :::image type="content" source="../assets/images/collaboration-control/tabs.png" alt-text="La capture d’écran est un exemple qui montre les tâches.":::

     > [!TIP]
     > Les contrôles sont visibles uniquement après l’enregistrement d’un enregistrement dans l’application. Si les onglets de contrôle n’apparaissent pas dans votre enregistrement, essayez d’actualiser votre navigateur ou de republier l’application à partir de Power Apps.

Vous avez maintenant ajouté les contrôles Collaboration à votre application. Vous pouvez maintenant exécuter votre application dans Power Apps et lancer les contrôles. Comme les paramètres n’ont pas encore été configurés, vous ne pourrez pas créer d’entités telles que Tâches ou Réunions tant que celles-ci ne seront pas ajoutées.

## <a name="define-settings-for-your-collaboration"></a>Définir les paramètres de votre collaboration

Vous pouvez définir des paramètres pour les contrôles de collaboration pour l’entité métier, comme la table créée dans [une nouvelle application pilotée par modèle](#create-a-new-model-driven-app-with-collaboration-controls-for-teams).

Les paramètres que vous pouvez appliquer sont les suivants :

|Paramètres|Utilisateur|
|---|---|
|ID de groupe|Tâches, réunions internes, approbations.|
|ID d’entreprise Bookings|Réunions externes à l’aide de Bookings |
|Site ID|fichiers SharePoint ; |
|ID de lecteur|fichiers SharePoint ;|

> [!NOTE]
> Les paramètres sont peu pratiques pour lancer votre application. Veillez donc à suivre les étapes suggérées. Si vous rencontrez des problèmes lors du lancement et de l’enregistrement des contrôles, revérifier les valeurs.

Vous pouvez obtenir l’ID de groupe en créant une équipe ou en utilisant une équipe existante dans Microsoft Teams pour héberger votre application et créer des variables de paramètres.

Pour créer une équipe, consultez [créer une équipe à partir de zéro](https://support.microsoft.com/en-us/office/create-a-team-from-scratch-174adf5f-846b-4780-b765-de1a0a737e2b).

Utilisez les instructions suivantes pour récupérer l’ID de groupe de votre équipe Teams pour les approbations, les tâches et les réunions internes :

1. Recherchez votre équipe dans votre liste d’équipes.

1. Sélectionnez l’ellipse **...** et **sélectionnez Obtenir le lien vers l’équipe**.

     :::image type="content" source="../assets/images/collaboration-control/get-link.png" alt-text="La capture d’écran décrit comment obtenir le lien avec l’équipe.":::

1. Copiez le lien et enregistrez la valeur de `groupId` l’URL. Vous utiliserez cette valeur ultérieurement lors de la définition des paramètres de votre solution.

     `https://teams.microsoft.com/l/team/19%3akk_TuKhjXu92yJvg4TZ10S6rouLSCgvHIb5NOOTfRjg1%40thread.tacv2/conversations?groupId=4310f270-1aa5-4089-99f3-47eb3b4d69ad&tenantId=b699419b-e0df-47e3-9909-24076fdcf68b`

Utilisez les instructions suivantes pour récupérer l’ID de site SharePoint et l’ID de lecteur pour les fichiers :

1. Pour utiliser le contrôle Fichiers, vous devez configurer un site SharePoint existant ou créer un nouveau site SharePoint. Pour créer un site, consultez [créer un site](/sharepoint/create-site-collection).

1. Récupérez maintenant les valeurs de paramètre de l’ID de site et de l’ID de lecteur, qui peuvent être appelées à l’aide des détails de votre site SharePoint.

     1. **ID de site** : à l’aide de [l’Explorateur Graph](https://developer.microsoft.com/graph/graph-explorer), connectez-vous et accordez des autorisations à Directory.ReadWrite.All et User.ReadWrite.All

         :::image type="content" source="../assets/images/collaboration-control/graph-permissions.png" alt-text="La capture d’écran est un exemple montrant l’Explorateur Graph.":::

     1. Veillez à remplacer le nom d’hôte par votre nom d’hôte et le chemin d’accès relatif au chemin d’accès du site, puis effectuez un appel de graphe vers `https://graph.microsoft.com/v1.0/sites/{hostname}:/{relative-path-to-site}`. Voici un exemple :
         1. Si votre URL de site = `https://myhostname.sharepoint.com/sites/MySiteName`
         1. Hostname = `myhostname.sharepoint.com`
         1. Chemin d’accès relatif au site = `sites/MySiteName`

              :::image type="content" source="../assets/images/collaboration-control/graph-call.png" alt-text="La capture d’écran est un exemple montrant l’appel Graph.":::

            L’appel de graphe serait, `https://graph.microsoft.com/v1.0/sites/myhostname.sharepoint.com:/sites/MySiteName`.

     1. La réponse reçue est un objet Json représentant le site, par exemple l’ID de site .`abcdef.sharepoint.com,0abe7394-6fce-4dcc-9884-7eaceb48cd41,8cb86762-16cd-495e-87cb-893cfdf94054`

     1. Enregistrez le paramètre de valeur d’ID de site.

     1. **ID de lecteur** : à l’aide de [l’Explorateur Graph](https://developer.microsoft.com/graph/graph-explorer), connectez-vous et effectuez l’appel de `https://graph.microsoft.com/v1.0/sites/{site-id}/drives` graphe avec la valeur de l’ID de site que vous avez enregistré précédemment.

     1. Une réponse Json est retournée avec une valeur de paramètre de tableau de type ou une liste d’objets de lecteur. Recherchez l’objet Json dont le paramètre de nom correspond au nom de votre bibliothèque de documents. Enregistrez la valeur du paramètre ID de lecteur.

Pour créer des réunions avec des utilisateurs extérieurs à votre organisation, tels que des clients, et pour utiliser des fonctionnalités de visite virtuelle dans votre application, vous devez fournir une entreprise Bookings. Pour plus d’informations, consultez [Microsoft Bookings](/microsoft-365/bookings/bookings-overview?view=o365-worldwide&preserve-view=true).

## <a name="add-settings-to-your-collaboration-manager-app"></a>Ajouter des paramètres à votre application Gestionnaire de collaboration

Pour appliquer des paramètres et explorer les fonctionnalités collaboratives de votre application dans Power Apps, ouvrez l’application que vous avez créée précédemment. Une page d’affichage s’affiche, dans laquelle vous pouvez sélectionner les enregistrements existants ou en créer un nouveau. Pour commencer par ouvrir ou créer un enregistrement.

Vous devez ajouter les ID de paramètres que vous avez enregistrés précédemment pour votre application

|Paramètres|Utilisateur|
|---|---|
|ID de groupe|Tâches, réunions internes, approbations.|
|ID d’entreprise Bookings|Réunions externes à l’aide de Bookings |
|Site ID|fichiers SharePoint ; |
|ID de lecteur|fichiers SharePoint ;|

### <a name="add-settings-for-tasks-meetings-and-files"></a>Ajouter des paramètres pour les tâches, les réunions et les fichiers

1. Lancez un contrôle et vous pouvez voir une fenêtre comme suit :

     :::image type="content" source="../assets/images/collaboration-control/launch-window.png" alt-text="La capture d’écran est un exemple montrant la fenêtre de contrôle.":::

1. Sélectionnez **Configurer** et accédez à l’onglet Général pour ajouter l’ID de groupe.

     :::image type="content" source="../assets/images/collaboration-control/groupid-general.png" alt-text="La capture d’écran décrit comment ajouter l’ID de groupe sous l’onglet Général.":::

1. Ouvrez l’onglet Fichiers pour ajouter l’ID de site et l’ID de lecteur.

     :::image type="content" source="../assets/images/collaboration-control/files-tab.png" alt-text="La capture d’écran décrit comment ajouter l’ID de site et l’ID de lecteur dans l’onglet Fichiers.":::

Le contrôle Notes ne nécessite pas de valeur de paramètre. Vous pouvez maintenant créer des entités telles que tâches et réunions dans votre application. Si vous rencontrez des problèmes lors du lancement et de l’enregistrement des contrôles, revérifier les valeurs des paramètres.

## <a name="explore-your-new-collaboration-manager-app"></a>Explorer votre nouvelle application Gestionnaire de collaboration

Les sections suivantes vous guident sur l’utilisation des contrôles Tâche, Notes, Réunions, Fichiers et Approbations.

### <a name="create-tasks"></a>Créer des tâches

Explorez la collaboration dans l’onglet Tâches en sélectionnant l’onglet Tâches, qui ouvre une page vide dans laquelle les utilisateurs peuvent ajouter toutes les tâches pertinentes qu’ils doivent effectuer.

1. Pour créer une tâche pour l’équipe, sélectionnez **Ajouter une tâche**. Il ouvre une boîte de dialogue dans laquelle vous pouvez fournir des détails sur la tâche et l’affecter aux personnes concernées de l’équipe, puis sélectionner Enregistrer.

     :::image type="content" source="../assets/images/collaboration-control/add-task.png" alt-text="La capture d’écran décrit comment ajouter une tâche.":::

1. La tâche enregistrée apparaît dans la liste des tâches.

1. Comme toutes les tâches sont sauvegardées par Planificateur Microsoft. Les utilisateurs peuvent utiliser l’application Tâches dans Microsoft Teams pour voir toutes les tâches qui sont affectées. Pour commencer, sélectionnez points de suspension **...** dans le volet gauche de Teams. Recherchez et sélectionnez Tâches par planificateur et à faire.

     :::image type="content" source="../assets/images/collaboration-control/tasks-planner.png" alt-text="La capture d’écran est un exemple des tâches par planificateur et à faire.":::

1. Après avoir ouvert l’application Tâches par planificateur et À faire, les utilisateurs peuvent voir toutes les tâches qui ont été créées dans votre application dans la section **Affecté à moi** de l’application. Les utilisateurs peuvent également afficher les détails d’une tâche, ajouter des pièces jointes et les marquer comme terminées.

### <a name="create-notes"></a>Créer des notes

Pour créer une note, sélectionnez **l’onglet Notes** de votre application, qui redirige vers un écran vide où les utilisateurs peuvent fournir des informations pertinentes. Pour ajouter une nouvelle note, sélectionnez **Nouvelle note**.
Après avoir ajouté des détails pertinents dans les notes, **sélectionnez Enregistrer**.

### <a name="create-meetings"></a>Créer des réunions

Sélectionnez l’onglet **Réunions** dans un enregistrement pour planifier des réunions internes et externes.

Pour planifier une réunion interne, sélectionnez la liste déroulante en regard du bouton **Nouvelle réunion** , puis sélectionnez **Réunion interne**.

:::image type="content" source="../assets/images/collaboration-control/new-meeting-tab.png" alt-text="La capture d’écran décrit comment planifier des réunions internes.":::

> [!NOTE]
>
> Customer Booking est activé si vous avez configuré Microsoft Booking avec un paramètre valide pour votre application.

Dans la boîte de dialogue **Nouvelle réunion** , les utilisateurs peuvent fournir des informations pertinentes sur la réunion et sélectionner **Enregistrer**. La réunion apparaît dans la liste des réunions.

:::image type="content" source="../assets/images/collaboration-control/new-meeting.png" alt-text="La capture d’écran décrit comment planifier une nouvelle réunion.":::

Pour planifier une réunion externe avec le client, sélectionnez la liste déroulante en regard du bouton **Nouvelle réunion** , puis sélectionnez **Réservation du client**. Si l’option **Réservation** de client n’est pas disponible dans la liste déroulante **Nouvelle réunion**, vérifiez si l’application est configurée pour Microsoft Bookings dans les paramètres et si l’utilisateur a le rôle Administrateur de réservations. Pour plus d’informations, consultez [ajouter du personnel à Bookings](/microsoft-365/bookings/add-staff?view=o365-worldwide&preserve-view=true). Vous pouvez ajouter des types de réservation supplémentaires en ajoutant des services supplémentaires dans votre entreprise Bookings.

:::image type="content" source="../assets/images/collaboration-control/customer-booking.png" alt-text="La capture d’écran décrit comment planifier bookings client.":::

Les utilisateurs peuvent voir les réunions internes et les réservations de clients dans leur liste de réunions. Une fois la réunion démarrée, les utilisateurs peuvent participer en sélectionnant le bouton **Rejoindre** , qui ouvre la réunion directement dans Microsoft Teams.

À mesure que les réunions sont soutenues par Outlook, les utilisateurs peuvent accéder à Bookings ou Calendrier Outlook pour voir toutes les réunions répertoriées dans un calendrier unique. Les réunions internes sont répertoriées dans le calendrier partagé.

Voici les étapes à suivre pour ajouter un calendrier partagé à votre Outlook (facultatif) :

1. Sous l’onglet Accueil du ruban, dans la section Gérer les calendriers, sélectionnez Ouvrir le calendrier > Ouvrir le calendrier partagé.

1. Dans la boîte de dialogue Ouvrir un calendrier partagé, entrez le nom de la personne. Sélectionnez la personne que vous recherchez, puis sélectionnez OK.

Dans le volet gauche, sous Calendriers partagés, vous devez maintenant voir un calendrier supplémentaire avec le nom de la personne.

:::image type="content" source="../assets/images/collaboration-control/customer-booking.png" alt-text="La capture d’écran décrit comment planifier bookings client.":::

### <a name="add-files"></a>Ajouter des fichiers

Ouvrez l’onglet **Fichiers** de votre application et **sélectionnez Charger** pour charger des fichiers à partir de OneDrive Entreprise ou de votre ordinateur. Lorsqu’un fichier est correctement chargé, l’affichage de liste principale s’actualise automatiquement pour afficher les fichiers de la liste.

:::image type="content" source="../assets/images/collaboration-control/meeting-calendar.png" alt-text="La capture d’écran décrit comment ouvrir le calendrier partagé.":::

### <a name="approvals"></a>Approbations

Les approbations permettent aux utilisateurs de demander la déconnexion d’autres utilisateurs lorsque vous travaillez dans un enregistrement. Par exemple, demandez une approbation pour terminer une tâche ou fermer un enregistrement.

1. Accédez à l’onglet **Approbations** de l’application.

1. Lorsqu’il n’y a aucune demande d’approbation, les utilisateurs voient l’écran suivant.

      :::image type="content" source="../assets/images/collaboration-control/no-approvals.png" alt-text="La capture d’écran est un exemple qui ne montre aucune demande d’approbation.":::

1. Sélectionnez la **nouvelle demande d’approbation** pour ouvrir le formulaire de demande d’approbation.

      :::image type="content" source="../assets/images/collaboration-control/approval-request-form.png" alt-text="La capture d’écran est un exemple montrant le nouveau formulaire de demande d’approbation.":::

1. Dans le formulaire de demande d’approbation, renseignez les champs requis et sélectionnez **Envoyer**, ce qui crée une demande et est ajouté à la liste.

      :::image type="content" source="../assets/images/collaboration-control/approvals-list.png" alt-text="La capture d’écran est un exemple qui montre la liste des approbations.":::

1. Sélectionnez l’approbation pour afficher les détails.

Pour plus d’informations sur les approbations, consultez [créer une approbation](https://support.microsoft.com/en-us/office/create-an-approval-6548a338-f837-4e3c-ad02-8214fc165c84).
