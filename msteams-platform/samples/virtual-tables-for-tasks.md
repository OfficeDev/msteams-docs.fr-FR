---
title: Tables virtuelles pour les tâches, les réunions et les fichiers dans l’application de contrôle Collaboration
author: surbhigupta
description: Dans ce module, découvrez les tables virtuelles pour les tâches, les réunions et les fichiers dans l’application de contrôle Collaboration dans Microsoft Teams.
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: 1913b379e9f24d36948a05190a4ae1804a8ec728
ms.sourcegitcommit: 442d2c8e80a2605b6d0215c973557471f18f8121
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/11/2022
ms.locfileid: "67314594"
---
# <a name="virtual-tables-for-tasks-meetings-files"></a>Tables virtuelles pour tâches, réunions, fichiers

Une nouvelle fonctionnalité de cette version est un ensemble de tables virtuelles. Celles-ci permettent aux développeurs d’interagir avec Graph via les API OData.

La solution de base des contrôles de collaboration comprend un ensemble de [tables virtuelles](/power-apps/developer/data-platform/virtual-entities/get-started-ve), qui peuvent être utilisées pour l’accès programmatique aux données créées par les contrôles collaboration.

> [!NOTE]
> Actuellement, les contrôles collaboration sont disponibles uniquement en [préversion publique des développeurs](~/resources/dev-preview/developer-preview-intro.md).

> [!TIP]
> [Les tables virtuelles](/power-apps/developer/data-platform/virtual-entities/get-started-ve) également appelées entités virtuelles permettent l’intégration des données résidant dans des systèmes externes en représentant ces données en tant que tables dans Microsoft Dataverse, sans réplication des données et souvent sans codage personnalisé.

Le système externe utilisé par les contrôles collaboration est Microsoft Graph. Il existe des tables virtuelles pour les événements de calendrier de groupe, les rendez-vous de réservation, les plans ou les tâches du planificateur, ainsi que les lecteurs, dossiers et fichiers SharePoint.

Cet article fournit des exemples qui montrent comment accéder aux tables virtuelles à l’aide de l’API REST Dataverse pour effectuer des opérations CRUD (Créer, Lire, Mettre à jour et Supprimer).

> [!TIP]
> Pour plus d’informations sur l’API REST Dataverse, consultez [l’API web Microsoft Dataverse](/power-apps/developer/data-platform/webapi/overview).

* Les tables virtuelles utilisent l’API web Dataverse standard, ce qui facilite l’utilisation des tables virtuelles pour remplir les données dans votre application.
* Les tables virtuelles implémentent des workflows complexes nécessaires pour prendre en charge les contrôles collaboration et ceux-ci s’exécutent dans les centres de données Microsoft pour des performances optimales.  
* Les tables virtuelles utilisent les fonctionnalités standard de journalisation et de surveillance de Dataverse.

Après avoir installé les contrôles Collaboration, les tables virtuelles peuvent être traitées comme un autre service de votre application qui peut dépendre.

:::image type="content" source="~/assets/images/collaboration-control/vt-overview.png" alt-text="Vue d’ensemble des tables virtuelles":::

**Conditions préalables**

Pour suivre cet article, vous avez besoin des éléments suivants :

1. Environnement Dataverse dans lequel les contrôles collaboration ont été installés.
1. Un compte d’utilisateur dans l’environnement Dataverse, auquel le rôle **Utilisateur des contrôles de collaboration** lui est attribué.
1. Un outil tiers, par exemple : Publier un homme ou un code C# personnalisé qui vous permet de vous authentifier auprès des instances Microsoft Dataverse, de composer et d’envoyer des demandes d’API web et d’afficher des réponses.  

> [!TIP]
> Microsoft fournit des informations sur la configuration d’un environnement Postman qui se connecte à votre instance Dataverse et utilise Postman pour effectuer des opérations avec l’API web. Consultez [Utiliser Postman avec l’API web Microsoft Dataverse](/power-apps/developer/data-platform/webapi/use-postman-web-api).

## <a name="virtual-tables-sample-scenario"></a>Exemple de scénario de tables virtuelles

Le scénario décrit dans ce guide utilise les tables virtuelles Plan planificateur et Tâche. Le scénario décrit est le même que celui utilisé par le contrôle Tasks Collaboration. Du point de vue de l’utilisateur, le scénario montre comment un plan planificateur et plusieurs tâches sont créées et associées à un enregistrement métier spécifique. Le scénario explique ensuite comment récupérer les tâches associées à l’enregistrement professionnel et comment lire, mettre à jour et supprimer une tâche de planificateur spécifique.

Le diagramme de séquence suivant explique l’interaction entre le client, qui peut être le contrôle de collaboration Tâches, [l’API collaboration](/rest/api/industry/collaboration-controls/) et les tables virtuelles plan planificateur et tâche.

:::image type="content" source="~/assets/images/collaboration-control/vt-sequence.png" alt-text="Diagramme de séquence pour les tables virtuelles":::

## <a name="virtual-tables-basic-operations"></a>Opérations de base sur les tables virtuelles

Cette section décrit les requêtes et réponses HTTP pour chaque étape de l’exemple de scénario.

**Tâche 1 : Récupérer l’ID de groupe**

Récupérez l’ID de groupe utilisé dans [les paramètres de votre collaboration](~/samples/app-with-collaboration-controls.md#define-settings-for-your-collaboration).

> [!NOTE]
> L’utilisateur que vous utilisez pour créer le plan dans les tâches suivantes doit être membre de ce groupe. Si ce n’est pas le cas, vous obtiendrez la réponse 403 Interdit.

**Tâche 2 : Commencer une session de collaboration**

Une session de collaboration est un enregistrement de la table racine de collaboration, qui vous permet d’associer plusieurs collaborations, par exemple, des tâches, des événements, des rendez-vous à un enregistrement professionnel.

Une session de collaboration vous permet d’effectuer des opérations telles que la liste des événements de calendrier associés à un enregistrement professionnel, par exemple une application d’inspection.

# <a name="request"></a>[Demande](#tab/request)

```http
    HTTP/1.1 POST https://[Organization URI]/api/data/v9.0/m365_begincollaborationsession  
```

```json
{
    "applicationName": "{{applicationName}}", 
    "collaborationRootEntityId": "{{collaborationRootEntityId}}", 
    "collaborationRootEntityName": "{{entityName}}" 
}
```

* `applicationName`: nom unique de l’application
* `collaborationRootEntityName`: nom de l’entité d’enregistrement d’entreprise  
* `collaborationRootEntityId`: clé primaire (ID) de l’enregistrement métier spécifique

# <a name="response"></a>[Réponse](#tab/response)

```http
    HTTP/1.1 200 OK 
```

```json
{ 
    "@odata.context": "https:// [Organization URI]/api/data/v9.0/$metadata#Microsoft.Dynamics.CRM.m365_begincollaborationsessionResponse", 
    "collaborationRootId": "72fc6b52-39d5-ec11-a7b6-0022481bfe8f" 
}
```

---

Suivez les besoins dans les `collaborationRootId` demandes suivantes.

**Tâche 3 : Créer un plan planificateur**

Créez un plan planificateur et associez-le à la session de collaboration créée ci-dessus et `Group ID` `collaborationRootId`.

# <a name="request"></a>[Demande](#tab/request1)

```http
    HTTP/1.1 POST https://[Organization URI]/api/data/v9.0/m365_graphplannerplans  
```

```json

{ 
    "m365_collaborationrootid": "{{collaborationRootId}}", 
    "m365_owner": "{{groupId}}", 
    "m365_title": "{{planTitle}}" 
}

```

* `collaborationRootId`: identifie la session de collaboration à laquelle nous souhaitons associer ce plan, utiliser la valeur de la tâche 2

* `groupId`: identifie le groupe qui sera propriétaire de ce plan, utiliser la valeur de l’étape 1

* `planTitle`: Titre du plan

# <a name="response"></a>[Réponse](#tab/response1)

```http
    HTTP/1.1 201 Created 
```

```json

{ 
    "@odata.context": "https:// [Organization URI]/api/data/v9.0/$metadata#m365_graphplannerplans/$entity", 
    "@odata.etag": "W/\"JzEtUGxhbiAgQEBAQEBAQEBAQEBAQEBARCc=\"", 
    "m365_createdby": "{\"user\":{\"displayName\":null,\"email\":null,\"id\":\"be330617-0e2b-48e9-8bf7-429a09c78e65\"},\"group\":null}", 
    "m365_createddatetime": "2022-05-16T16:58:33.1833561Z", 
    "m365_owner": "03614cef-8f5b-4265-9944-080d013c55d6", 
    "m365_title": "Multi-byte plan", 
    "m365_id": "8I6fu1kNS0elsbTxd67bi2UADnJu", 
    "m365_collaborationrootid": "72fc6b52-39d5-ec11-a7b6-0022481bfe8f", 
    "m365_graphplannerplanid": "5c9c3ecf-f157-0f67-dcd9-733a77ad593e", 
    "m365_details": null 
} 

```

---

Suivez les besoins dans les`m365_id` demandes suivantes.

**Tâche 4 : Créer une tâche de planificateur**

Créer une tâche de planificateur avec `PlanId` et `collaborationRootId`. vous pouvez créer plusieurs tâches du Planificateur et les associer à la session de collaboration créée précédemment.

# <a name="request"></a>[Demande](#tab/request2)

```http
    HTTP/1.1 POST https://[Organization URI]/api/data/v9.0/m365_graphplannertasks  
```

```json
{ 
    "m365_collaborationrootid": "{{collaborationRootId}}", 
    "m365_planid": "{{planId}}", 
    "m365_title": "{{taskTitle}}", 
    "m365_duedatetime": "2022-05-04T08:00:00Z", 
    "m365_assignments": "{\"me\":{\"orderHint\":\" !\",\"@odata.type\":\"#microsoft.graph.plannerAssignment\"}}" 
} 

```

* `collaborationRootId`: identifie la session de collaboration à laquelle nous souhaitons associer ce plan, nous la valeur de la tâche 2
* `planId`: identifie le plan à laquelle cette tâche sera affectée, utilisez la valeur de l’étape précédente
* `taskTitle`: Titre de la tâche

# <a name="response"></a>[Réponse](#tab/response2)

```http
    HTTP/1.1 201 Created 
```

```json

{ 
    "@odata.context": "https://mwtmarkwallaceunmanaged.crm10.dynamics.com/api/data/v9.0/$metadata#m365_graphplannertasks/$entity", 
    "@odata.etag": "W/\"JzEtVGFzayAgQEBAQEBAQEBAQEBAQEBARCc=\"", 
    "m365_activechecklistitemcount": 0, 
    "m365_appliedcategories": "{}", 
    "m365_assigneepriority": "8585488865579062167", 
    "m365_assignments": "{\"be330617-0e2b-48e9-8bf7-429a09c78e65\":{\"assignedBy\":{\"user\":{\"displayName\":null,\"email\":null,\"id\":\"be330617-0e2b-48e9-8bf7-429a09c78e65\"},\"group\":null},\"assignedDateTime\":\"2022-05-16T16:58:47.571364+00:00\",\"orderHint\":\"8585488866179218449P`\",\"@odata.type\":\"#microsoft.graph.plannerAssignment\"}}", 
    "m365_checklistitemcount": 0, 
    "m365_createdby": "{\"user\":{\"displayName\":null,\"email\":null,\"id\":\"be330617-0e2b-48e9-8bf7-429a09c78e65\"},\"group\":null}", 
    "m365_createddatetime": "2022-05-16T16:58:47Z", 
    "m365_duedatetime": "2022-05-04T08:00:00Z", 
    "m365_hasdescription": false, 
    "m365_orderhint": "8585488865579062167", 
    "m365_percentcomplete": 0, 
    "m365_priority": 5, 
    "m365_planid": "8I6fu1kNS0elsbTxd67bi2UADnJu", 
    "m365_previewtype": "automatic", 
    "m365_referencecount": 0, 
    "m365_title": "Team-oriented discrete time-frame", 
    "m365_id": "8WSKWaEqAU-aZV4h9VUn0GUALXbH", 
    "m365_collaborationrootid": "72fc6b52-39d5-ec11-a7b6-0022481bfe8f", 
    "m365_graphplannertaskid": "0a2115b9-8b03-90ee-b450-42005d906ce8", 
    "m365_completedby": null, 
    "m365_details": null, 
    "m365_completeddatetime": null, 
    "m365_conversationthreadid": null, 
    "m365_bucketid": null, 
    "m365_startdatetime": null 
} 

```

---

Suivez les besoins dans les `m365_graphplannertaskid` demandes suivantes.

> [!NOTE]
> Il `m365_graphplannertaskid` s’agit de la clé primaire de l’enregistrement dans la table virtuelle de tâche du planificateur. Toutes les demandes suivantes à la table virtuelle pour interagir avec cet enregistrement doivent utiliser cette clé primaire. Il s’agit `plannerTaskId` des étapes suivantes de ce document.

Vous devez répéter cette étape pour créer plusieurs tâches dans le plan.

**Tâche 5 : Récupérer les tâches associées au Planificateur**

Récupérez les tâches associées au Planificateur associées `collaborationRootId` à la session de collaboration créée précédemment.

# <a name="request"></a>[Demande](#tab/request3)

```http
    HTTP/1.1 GET https://[Organization URI]/api/data/v9.0/ m365_graphplannertasks?$filter=m365_collaborationrootid eq '{{collaborationRootId}}'&$select=m365_graphplannertaskid,m365_title,m365_createddatetime  
```

* `$filter`: utilisez la requête système $filter pour demander des enregistrements associés à la session de collaboration (en spécifiant l’ID de l’enregistrement racine de collaboration).
* `$select`: utilisez l’option de requête système $select pour demander des propriétés spécifiques.

# <a name="response"></a>[Réponse](#tab/response3)

```http
    HTTP/1.1 200 OK 
```

```json

{ 

    "@odata.context": "https://mwtmarkwallaceunmanaged.crm10.dynamics.com/api/data/v9.0/$metadata#m365_graphplannertasks(m365_graphplannertaskid,m365_title,m365_createddatetime)", 
    "value": [ 
        { 
            "@odata.etag": "W/\"JzEtVGFzayAgQEBAQEBAQEBAQEBAQEBARCc=\"", 
            "m365_graphplannertaskid": "8537731e-9414-1091-8d7d-ce5b74fc2477", 
            "m365_title": "Diverse executive core", 
            "m365_createddatetime": "2022-05-16T16:58:45Z", 
            "m365_id": "N_A2qmo3j0uvZZY1yd6V_GUADDEg", 
            "m365_collaborationrootid": "72fc6b52-39d5-ec11-a7b6-0022481bfe8f" 
        }, 
        { 
            "@odata.etag": "W/\"JzEtVGFzayAgQEBAQEBAQEBAQEBAQEBARCc=\"", 
            "m365_graphplannertaskid": "4a89895a-050e-9165-a6e4-19c3850f22ec", 
            "m365_title": "Cloned didactic open architecture", 
            "m365_createddatetime": "2022-05-16T16:58:41Z", 
            "m365_id": "--U0zbgsO0us084C0yCyEWUALbWw", 
            "m365_collaborationrootid": "72fc6b52-39d5-ec11-a7b6-0022481bfe8f" 
        }, 
        { 
            "@odata.etag": "W/\"JzEtVGFzayAgQEBAQEBAQEBAQEBAQEBARCc=\"", 
            "m365_graphplannertaskid": "20a08b8c-394b-b3fb-f9d1-47496df7a67b", 
            "m365_title": "Synergized zero defect interface", 
            "m365_createddatetime": "2022-05-16T16:58:43Z", 
            "m365_id": "AMn3RtbmV0m6cvkp5HKDCWUAKI0_", 
            "m365_collaborationrootid": "72fc6b52-39d5-ec11-a7b6-0022481bfe8f" 
        } 
    ] 
} 

```

---

Suivez les `m365_id‘s` ID en tant que nécessaires dans les demandes suivantes.

**Tâche 6 : Récupérer une tâche du planificateur**

Récupérez une tâche de planificateur avec `PlannerTaskID` laquelle effectuer une opération de lecture sur l’une des tâches de planificateur créées précédemment.

# <a name="request"></a>[Demande](#tab/request4)

```http
    HTTP/1.1 GET https://[Organization URI]/api/data/v9.0/m365_graphplannertasks({{plannerTaskId}})  
```

* `plannerTaskId`: la clé primaire de l’enregistrement de tâche du planificateur est la `m365_graphplannertaskid` propriété.

# <a name="response"></a>[Réponse](#tab/response4)

```http
    HTTP/1.1 200 OK 
```

```json
{ 
    "@odata.context": "https://mwtmarkwallaceunmanaged.crm10.dynamics.com/api/data/v9.0/$metadata#m365_graphplannertasks/$entity", 
    "@odata.etag": "W/\"JzEtVGFzayAgQEBAQEBAQEBAQEBAQEBARCc=\"", 
    "m365_activechecklistitemcount": 0, 
    "m365_appliedcategories": "{}", 
    "m365_assigneepriority": "8585488204334528131", 
    "m365_assignments": "{\"be330617-0e2b-48e9-8bf7-429a09c78e65\":{\"assignedBy\":{\"user\":{\"displayName\":null,\"email\":null,\"id\":\"be330617-0e2b-48e9-8bf7-429a09c78e65\"},\"group\":null},\"assignedDateTime\":\"2022-05-17T11:20:52.0247676+00:00\",\"orderHint\":\"8585488204934840644P2\",\"@odata.type\":\"#microsoft.graph.plannerAssignment\"}}", 
    "m365_checklistitemcount": 0, 
    "m365_createdby": "{\"user\":{\"displayName\":null,\"email\":null,\"id\":\"be330617-0e2b-48e9-8bf7-429a09c78e65\"},\"group\":null}", 
    "m365_createddatetime": "2022-05-17T11:20:52Z", 
    "m365_duedatetime": "2022-05-04T08:00:00Z", 
    "m365_orderhint": "8585488204334528131", 
    "m365_percentcomplete": 0, 
    "m365_priority": 5, 
    "m365_planid": "8I6fu1kNS0elsbTxd67bi2UADnJu", 
    "m365_previewtype": "automatic", 
    "m365_referencecount": 0, 
    "m365_title": "Secured content-based customer loyalty", 
    "m365_id": "SXmz1hxiOk-E3MKJUyhj0mUABvix", 
    "m365_details": "{\"@odata.context\":\"https://graph.microsoft.com/beta/$metadata#planner/tasks('SXmz1hxiOk-E3MKJUyhj0mUABvix')/details/$entity\",\"@odata.etag\":\"W/\\\"JzEtVGFza0RldGFpbHMgQEBAQEBAQEBAQEBAQEBARCc=\\\"\",\"description\":null,\"previewType\":\"automatic\",\"id\":\"SXmz1hxiOk-E3MKJUyhj0mUABvix\",\"references\":{},\"checklist\":{}}", 
    "m365_graphplannertaskid": "1b326015-bb43-945c-85bc-9b2a4ed16c73", 
    "m365_completedby": null, 
    "m365_hasdescription": null, 
    "m365_collaborationrootid": null, 
    "m365_completeddatetime": null, 
    "m365_conversationthreadid": null, 
    "m365_bucketid": null, 
    "m365_startdatetime": null 
}

```

---

Effectuez le suivi de la `@odata.etag` propriété et de la`m365_graphplannertaskid` propriété, car celles-ci seront nécessaires pour effectuer des opérations de mise à jour ou de suppression.

**Tâche 7 : Mettre à jour une tâche du planificateur**

Mettez à jour une tâche de planificateur pour `PlannerTask ID` effectuer une opération de mise à jour sur l’une des tâches de planificateur créées à l’étape précédente. Pour mettre à jour une tâche de planificateur, exécutez la requête suivante :

# <a name="request"></a>[Demande](#tab/request5)

```http
    HTTP/1.1 PATCH https://[Organization URI]/api/data/v9.0/m365_graphplannertasks({{plannerTaskId}})
```

* En-tête : If-Match : {{@odata.etag}}

```json

{
    "m365_title": "{{$planTitle}}" 
}   

```

* `@odata.etag`: Etag pour la tâche, vous devez effectuer une lecture pour récupérer la version la plus à jour.

* `planTitle`: titre mis à jour pour la tâche

# <a name="response"></a>[Réponse](#tab/response5)

```http
    HTTP/1.1 204 No Content 
```

---

**Tâche 8 : Supprimer une tâche du planificateur**

Supprimez une tâche de planificateur avec `PlannerTask ID` laquelle effectuer une opération de suppression sur l’une des tâches de planificateur créées à l’étape précédente. Pour supprimer une tâche de planificateur, exécutez la requête suivante :

# <a name="request"></a>[Demande](#tab/request6)

```http
    HTTP/1.1 DELETE https://[Organization URI]/api/data/v9.0/m365_graphplannertasks({{plannerTaskId}})
```

* `@odata.etag`: Etag pour la tâche, vous devez effectuer une lecture pour récupérer la version la plus à jour.

# <a name="response"></a>[Réponse](#tab/response6)

```http
    HTTP/1.1 204 No Content
```

---

**Tâche 9 : Mettre à jour les détails d’une tâche du planificateur**

Mettez à jour une tâche de planificateur pour `PlannerTask ID` effectuer une opération de mise à jour sur l’une des tâches du planificateur créées à l’étape précédente.

# <a name="request"></a>[Demande](#tab/request7)

```http
    HTTP/1.1 PATCH https://[Organization URI]/api/data/v9.0/m365_graphplannertasks({{plannerTaskId}})
```

En-tête : If-Match : {{@odata.etag}}

```json

{ 

    "m365_title": "{{$planTitle}}", 
    "m365_details": "{\"@odata.etag\":\"{{details.etag}}\",\"description\":\"Updated Task Description\"}" 

}   
```

* `@odata.etag`: Etag pour la tâche, vous devez effectuer une lecture pour récupérer la version la plus à jour.
* `planTitle`: titre mis à jour pour la tâche.
* `@details.etag`: Etag pour les détails de la tâche, vous devez effectuer une lecture à l’aide du paramètre de requête $select pour inclure la `m365_details` colonne afin de récupérer la version la plus récente. Cette valeur sera incluse dans la `m365_details` colonne de la réponse. Cette valeur n’est pas la même que celle du `@odata.etag` serveur principal du Planificateur, car la tâche et ses détails sont stockés séparément.

# <a name="response"></a>[Réponse](#tab/response7)

```http
HTTP/1.1 204 No Content 
```

---

> [!NOTE]
> Vous pouvez définir l’en-tête `If-Match` sur « * » et vous n’aurez pas besoin de fournir de valeurs etag, mais vos modifications remplaceront toujours la tâche et ses détails.

## <a name="virtual-tables-authorization"></a>Autorisation des tables virtuelles

Voici les étapes d’autorisation requises pour effectuer des requêtes HTTP à l’aide des tables virtuelles dans la solution de contrôles collaboration.

### <a name="azure-app-registration"></a>Inscription d’application Azure

Pour acquérir le jeton de porteur approprié, une inscription d’application dans Azure est requise. Pour plus d’informations sur les inscriptions d’applications, consultez [inscrire une application](/azure/active-directory/develop/quickstart-register-app).

1. Créez une inscription d’application dans le Portail Azure pour vous authentifier.
1. Accédez aux **certificats & secrets**.
1. Créez une clé secrète client.

     > [!IMPORTANT]
     > Veillez à copier la valeur du secret et à la stocker pour une utilisation ultérieure. Vous ne pourrez plus y accéder après avoir quitté la page active.

1. Accédez aux **autorisations d’API**.
1. Ajoutez **l’user_impersonation** autorisation déléguée à partir de Dynamics CRM.
1. Accordez le consentement de l’administrateur pour cette autorisation.

     :::image type="content" source="../assets/images/collaboration-control/power-automate-api-permission.png" alt-text="La capture d’écran est un exemple montrant l’autorisation de l’API Power Automate":::

1. Accédez au **manifeste**.
1. Définissez la valeur des attributs suivants sur true :

   * oauth2AllowIdTokenImplicitFlow
   * oauth2AllowImplicitFlow

1. Sélectionnez Enregistrer.

     :::image type="content" source="../assets/images/collaboration-control/power-automate-manifest.png" alt-text="La capture d’écran est un exemple montrant le manifeste Power Automate":::

### <a name="powerapps-environment-permissions"></a>Autorisations d’environnement PowerApps

Une fois l’inscription de l’application configurée, vous devez configurer un utilisateur d’application dans l’environnement PowerApps. Cela vous permet de vous authentifier avec les étendues Dynamics correctes qui ont été configurées précédemment.

1. Ouvrez le [Centre de Administration Power Platform](https://admin.powerplatform.microsoft.com/).
1. Accédez aux **environnements** > **Your_Environment** > **liste utilisateurs de l’application Utilisateurs** > .
1. Sélectionnez **Nouvel utilisateur d’application** , puis sélectionnez votre inscription d’application Azure.
1. Sélectionnez **Modifier les rôles de sécurité** et attribuez le rôle **Administrateur système** à l’utilisateur de l’application.

   1. Le rôle **Administrateur système** est appliqué pour autoriser l’authentification pour tous les utilisateurs ayant un rôle de sécurité inférieur. Par exemple, **Collaboration contrôle l’utilisateur**.
   1. Cela peut être restreint en appliquant un rôle inférieur à l’application. Par exemple, **La collaboration contrôle l’administrateur**.

     :::image type="content" source="../assets/images/collaboration-control/power-automate-admin-center.png" alt-text="La capture d’écran est un exemple montrant le Centre d’administration Power Automate":::

### <a name="getting-the-bearer-token"></a>Obtention du jeton du porteur

Une fois les autorisations d’inscription d’application Azure et d’environnement PowerApps terminées, envoyez la requête HTTP suivante pour obtenir le jeton du porteur.

```http
POST https://login.microsoftonline.com/<AZURE_APP_TENANT_ID>/oauth2/token
```

* **Content-Type**: application/x-www-form-urlencoded
* **client_id** : <AZURE_APP_CLIENT_ID>
* **&client_secret** : <AZURE_APP_CLIENT_ID>
* **ressource&** : https://\<RESOURCEURL\>/
* **nom d’utilisateur&** : \<USERNAME\>
* **mot de passe&** : \<PASSWORD\>
* **&grant_type** : Mot de passe

> [!IMPORTANT]
> Veillez à inclure la barre oblique de fin sur le paramètre de ressource. Si ce n’est pas le cas, vous obtiendrez une erreur liée aux étendues Graph lors de l’appel de la table virtuelle.

À partir de la charge utile de réponse, copiez la valeur de la propriété **access_token** . Vous pouvez ensuite passer ce jeton du porteur dans le cadre de l’en-tête d’autorisation lors de l’établissement de demandes aux tables virtuelles.

:::image type="content" source="../assets/images/collaboration-control/power-automate-authorization.png" alt-text="La capture d’écran est un exemple montrant l’autorisation Power Automate":::

## <a name="virtual-tables-error-handling"></a>Gestion des erreurs des tables virtuelles

La gestion des erreurs des tables virtuelles décrit les scénarios d’erreur courants et la façon dont les tables virtuelles répondront.

### <a name="attempt-to-create-a-virtual-record-without-a-collaboration-session"></a>Tentative de création d’un enregistrement virtuel sans session de collaboration

Une session de collaboration valide est requise pour chaque demande de création d’un enregistrement virtuel.  Lorsqu’un enregistrement virtuel est créé, la table virtuelle crée un enregistrement de carte de collaboration, qui inclut la clé primaire de l’enregistrement virtuel, le nom de l’entité et l’ID externe, c’est-à-dire l’ID de ressource Graph. Cette carte de collaboration est associée à une session de collaboration, et c’est ainsi que les contrôles collaboration effectueront le suivi des collaborations associées à un enregistrement d’entreprise.

# <a name="request"></a>[Demande](#tab/request8)

```http
    HTTP/1.1 POST https://[Organization URI]/api/data/v9.0/m365_graphplannertasks  
```

```json

{ 
    "m365_planid": "{{planId}}", 
    "m365_title": "{{taskTitle}}", 
    "m365_duedatetime": "2022-05-04T08:00:00Z", 
    "m365_assignments": "{\"me\":{\"orderHint\":\" !\",\"@odata.type\":\"#microsoft.graph.plannerAssignment\"}}" 
}

```

La `collaborationRootId` propriété est manquante dans la demande.

# <a name="response"></a>[Réponse](#tab/response8)

```http
    HTTP/1.1 400 Bad Request 
```

```json

{ 
    "error": { 
        "code": "0x80048d0b", 
        "message": "Parameter 'm365_collaborationrootid' is null, empty, or white-space." 
    } 
} 

```

---

Pour résoudre ce problème, vous devez toujours fournir une propriété valide `collaborationRootId` lors de la création d’un enregistrement virtuel.

### <a name="attempt-to-read-a-virtual-record-without-a-collaboration-map"></a>Tentative de lecture d’un enregistrement virtuel sans carte de collaboration

Les tables virtuelles vous permettent d’exécuter des demandes, qui retournent des collections d’enregistrements virtuels. Nous l’avons vu précédemment dans ce document, où nous avons demandé toutes les tâches du planificateur associées à une session de collaboration spécifique. Il est également possible de demander toutes les tâches de planificateur associées à un plan planificateur spécifique à l’aide d’une requête système $filter comme celle-ci : $filter=m365_planid eq`{{planId}}`. Un problème qui se produit si vous utilisez une telle requête est que les enregistrements sont retournés pour les tâches du planificateur, qui ne sont pas associées à une session de collaboration, c’est-à-dire des tâches de planificateur créées par un autre moyen que l’utilisation d’un contrôle Collaboration. Si vous tentez de lire, mettre à jour ou supprimer un tel enregistrement, la demande échoue, car la table virtuelle ne trouve pas la carte de collaboration associée.  

# <a name="request"></a>[Demande](#tab/request9)

```http
    HTTP/1.1 GET https://[Organization URI]/api/data/v9.0/m365_graphplannertasks({{plannerTaskId}})
```

La `plannerTaskId` propriété est associée à une tâche de planificateur, qui a été créée à l’aide de l’interface web du planificateur et n’a donc pas d’enregistrement de carte de collaboration.

# <a name="response"></a>[Réponse](#tab/response9)

```http
    HTTP/1.1 404 Not Found 
```

```json
{ 
    "error": { 
        "code": "0x80048d02", 
        "message": "A record with the specified key values does not exist in m365_collaborationmap entity" 
    }
} 
```

---

Pour résoudre ce problème, vous devez vérifier le message d’erreur dans la réponse et s’il est défini sur le message indiqué ci-dessus, cela signifie que l’enregistrement virtuel n’est pas associé. Pour créer une association pour cet enregistrement, vous devez appeler [Associate Collaboration Map - API REST](/rest/api/industry/collaboration-controls/collaboration-custom-ap-is/associate-collaboration-map).

### <a name="attempt-to-read-a-virtual-record-and-the-graph-resource-has-been-deleted"></a>Tentative de lecture d’un enregistrement virtuel et suppression de la ressource Graph

En lien avec l’erreur précédente, vous devez gérer le cas où une ressource Graph a été supprimée, mais le client a toujours une référence à l’enregistrement virtuel supprimé. Cela peut se produire si un autre utilisateur a supprimé l’enregistrement. Si vous tentez de lire, mettre à jour ou supprimer un tel enregistrement, la demande échoue, car la table virtuelle ne peut pas récupérer la ressource à partir de Graph.

# <a name="request"></a>[Demande](#tab/request10)

```http
    HTTP/1.1 GET https://[Organization URI]/api/data/v9.0/m365_graphplannertasks({{plannerTaskId}})
```

La `plannerTaskId` propriété est associée à une tâche de planificateur, qui a été supprimée.

# <a name="response"></a>[Réponse](#tab/response10)

```http
    HTTP/1.1 404 Not Found 
```

```json
{ 
    "error": { 
        "code": "0x80048d02", 
        "message": "REST call failed because: Reason - NotFound, Full error - {\"error\":{\"code\":\"\",\"message\":\"The requested item is not found.\",\"innerError\":{\"date\":\"2022-05-17T16:30:51\",\"request-id\":\"b692a31a-312d-490c-8dce-d258459a0211\",\"client-request-id\":\"b692a31a-312d-490c-8dce-d258459a0211\"}}}." 
    } 
} 
```

---

Ce cas doit être géré par n’importe quel code client, qui récupère les enregistrements virtuels, car un autre utilisateur peut supprimer la ressource Graph associée à tout moment.

### <a name="attempt-to-update-a-virtual-record-with-an-invalid-odataetag"></a>Tentative de mise à jour d’un enregistrement virtuel avec un @odata.etag non valide

La `@odata.etag` propriété est utilisée pour la concurrence des données et pour empêcher la surécriture du même enregistrement s’il a été mis à jour par un autre utilisateur. Quand un enregistrement est lu, l’etag actuel est retourné et reste valide jusqu’à ce que l’enregistrement soit modifié. L’etag doit être inclus dans toute demande de mise à jour et sera vérifié avant la fin de l’opération. Si l’enregistrement a été modifié par un autre utilisateur depuis que l’utilisateur actuel l’a lu, la demande de mise à jour des utilisateurs actuels échoue.

Si vous effectuez deux demandes de mises à jour à l’aide du même @odata.etag, la deuxième demande échoue :

# <a name="request"></a>[Demande](#tab/request11)

```http
    HTTP/1.1 PATCH https://[Organization URI]/api/data/v9.0/m365_graphplannertasks({{plannerTaskId}})
```

En-tête : If-Match : {{@odata.etag}}

```json
{
    "m365_title": "{{$planTitle}}" 
}

```

# <a name="response"></a>[Réponse](#tab/response11)

```http
    HTTP/1.1 409 Conflict 
```

```json
{ 
    "error": { 
        "code": "0x80048d08", 
        "message": "REST call failed because: Reason - Conflict, Full error - {\"error\":{\"code\":\"\",\"message\":\"The attempted changes conflicted with already accepted changes. Read the latest state and resolve differences.\",\"innerError\":{\"date\":\"2022-05-18T06:54:55\",\"request-id\":\"dc6cd2b7-1509-4e81-91ff-22cf35b86e18\",\"client-request-id\":\"dc6cd2b7-1509-4e81-91ff-22cf35b86e18\"}}}." 
    }
} 
```

---

### <a name="querying-for-associated-virtual-records"></a>Interrogation des enregistrements virtuels associés

Dans la tâche 5 ci-dessus, décrit comment récupérer les tâches associées au Planificateur. Cette opération est prise en charge pour toutes les tables virtuelles. Lors de l’exécution de cette requête, vous devez inclure une `$filter` requête, qui spécifie l’ID racine de collaboration comme indiqué ci-dessous :

# <a name="request"></a>[Demande](#tab/request12)

```http
    HTTP/1.1 GET https://[Organization URI]/api/data/v9.0/ m365_graphplannertasks?$filter=m365_collaborationrootid eq '{{collaborationRootId}}'&$select=m365_graphplannertaskid,m365_title,m365_createddatetime  
```

---

* Les autres options de filtrage ne peuvent pas être combinées avec cette `$filter` requête et, le cas échéant, elles seront ignorées.
* Un autre filtrage doit être effectué directement sur la réponse de la demande.

### <a name="querying-for-virtual-records-with-required-key-attributes"></a>Interrogation d’enregistrements virtuels avec les attributs de clé requis

Quand, l’API web Dataverse est appelée pour récupérer plusieurs enregistrements à partir des tables virtuelles suivantes, un attribut de clé obligatoire est requis. Les rendez-vous de réservation Graph nécessitent qu’un rendez-vous valide `m365_bookingbusinessid` soit inclus dans la requête. Si l’attribut de clé n’est pas fourni, la demande échoue comme suit :

# <a name="response"></a>[Réponse](#tab/response13)

```http
    HTTP/1.1 400 Bad Request 
```

```json

{ 
  "error": { 
    "code": "0x80048d0b", 
    "message": "Key attribute is missing: 'm365_bookingbusinessid'.", 
    ….
  } 
} 

```

---

Pour résoudre ce problème, remplacez la demande par ce format :

# <a name="request"></a>[Demande](#tab/request14)

```http
    HTTP/1.1 GET https://[Organization URI]/api/data/v9.0/ m365_graphbookingappointments?$filter=m365_bookingbusinessid eq '{{bookingBusinessId}}'
```

---

### <a name="creating-virtual-records-and-graph-access-control"></a>Création d’enregistrements virtuels et de contrôle d’accès Graph

Les tables virtuelles respectent le contrôle d’accès spécifié pour Microsoft Graph. Les tables virtuelles n’autorisent pas les opérations que l’utilisateur n’a pas pu effectuer à l’aide de Microsoft API Graph. Par exemple, si l’utilisateur que vous utilisez pour créer le plan est la tâche 3 et qu’il n’est pas membre du groupe que vous utilisez, vous obtenez 403 réponses Interdites.
