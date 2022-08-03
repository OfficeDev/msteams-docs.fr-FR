---
title: Références d’entités de table virtuelle
author: surbhigupta
description: Dans ce module, découvrez la référence d’entité de tables virtuelles et leurs attributs dans Microsoft Teams.
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: 34166c49eb61c52f8eec94b34844ef27d52715ef
ms.sourcegitcommit: 0bb822b30739e4a532a36764dad2dbf35a81ba29
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2022
ms.locfileid: "67179098"
---
# <a name="virtual-tables-entity-reference"></a>Informations de référence sur les entités de tables virtuelles

La collaboration contrôle les entités virtuelles et leurs attributs ont un mappage un-à-un avec un type de ressource Microsoft Graph spécifique. Par exemple, les entités de tâche du Planificateur Graph sont mappée au [type de ressource de tâche du Planificateur Microsoft Graph](/graph/api/resources/plannertask). L’entité virtuelle partage les mêmes attributs que le type de ressource.

> [!NOTE]
> Actuellement, les contrôles collaboration sont disponibles uniquement en [préversion publique des développeurs](~/resources/dev-preview/developer-preview-intro.md).

## <a name="collaboration-controls-virtual-entities"></a>La collaboration contrôle les entités virtuelles

| Nom | Description |
|---|---|
| Tâche du Planificateur de graphes | La table Tâches du Planificateur Graph représente une tâche planificateur dans Microsoft 365. |
| Plan du Planificateur Graph | La table Plan du Planificateur Graph représente un plan planificateur dans Microsoft 365. |
| Événement Graph | La table Des événements Graph représente un événement dans un calendrier utilisateur ou le calendrier par défaut d’un groupe Microsoft 365. |
| Rendez-vous de réservation Graph | La table De rendez-vous Graph Booking représente un rendez-vous client pour un service Booking, effectué par un ensemble de membres du personnel, provIDed par une entreprise Microsoft Bookings. |
| Lecteur Graph | La table Lecteur Graph représente l’objet de niveau supérieur qui représente oneDrive d’un utilisateur ou une bibliothèque de documents dans SharePoint. |
| Élément de lecteur Graph | La table Élément de lecteur Graph représente un fichier, un dossier ou un autre élément stocké dans un lecteur. |

## <a name="graph-planner-task"></a>Tâche du Planificateur de graphes

* Nom de l’entité : m365_graphplannertask.
* Ressource Graph : [type de ressource plannerTask](/graph/api/resources/plannertask)
* Le tri n’est pas pris en charge.
* Le filtrage n’est pas pris en charge.
* La pagination pilotée par le serveur est prise en charge, avec une taille de page maximale de 400.

### <a name="attributes-for-graph-planner-task"></a>Attributs de la tâche du Planificateur graphe

| Column  | Dataverse Type | Détails |
|---|---|---|
| `m365_collaborationrootid` | String | L’ID racine de collaboration de l’enregistrement de session de collaboration est associé à plusieurs sessions de collaboration. Cette valeur est retournée sous la forme d’une chaîne délimitée par des virgules. Notez que cet attribut ne sera pas retourné lors de la récupération de plusieurs enregistrements. |
| `m365_activechecklistitemcount` | Int32 | Nombre d’éléments de liste de vérification dont la valeur est définie sur false, représentant des éléments incomplets. |
| `m365_graphplannertaskId` | Guid | Identificateur unique de la tâche du planificateur de graphes. |
| `m365_appliedcategories` | String | Nombre d’éléments de liste de vérification dont la valeur est définie sur false, représentant des éléments incomplets. |
| `m365_appliedcategories` | String | Catégories auxquelles la tâche a été appliquée. Cet attribut est une chaîne encodée JSON, par exemple « { \"category1\" : true, \"category6\" : true, \"category9\" : true } » |
| `m365_assigneepriority` | String | Indicateur utilisé pour commander des éléments de ce type dans une vue de liste. Le format est défini comme décrit à [l’aide d’indicateurs de commande dans le Planificateur](/graph/api/resources/planner-order-hint-format). |
| `m365_assignments` | String | Ensemble d’assignés auxquels la tâche est affectée. Cet attribut est une chaîne encodée JSON par exemple « {\" 7be...\": {\"assignedBy\" : {\"user\": {\"displayName\", \"email\", \"ID\":\" 7be...\"}, \"group\": null, \"application\": null \"device\": null} » |
| `m365_bucketid` | Chaîne | ID du compartiment auquel appartient la tâche. Le compartiment doit se trouver dans le plan où se trouve la tâche. Il comporte 28 caractères et respecte la casse. [Une validation du format](/graph/api/resources/planner-identifiers-disclaimer) est effectuée sur le service. |
| `m365_checklistitemcount` | Int32 | Nombre d’éléments de liste de vérification présents sur la tâche. |
| `m365_completedby` | String | Identité de l’utilisateur qui a effectué la tâche. Cet attribut est une chaîne encodée JSON, par exemple {\"user\": {\"displayName,ID\"\"\":\"d55...\"}} |
| `m365_completeddatetime` | Date/heure | En lecture seule. Date et heure auxquelles « percentComplete » de la tâche est défini sur « 100 ». Le type d’horodatage représente les informations de date et d’heure au moyen du format ISO 8601. Il est toujours au format d’heure UTC. Par exemple, minuit UTC le 1er janvier 2014 est 2014-01-01T00:00:00Z |
| `m365_conversationthreadid` |String | ID du thread de conversation sur la tâche. Il s’agit de l’ID de l’objet de thread de conversation créé dans le groupe. |
| `m365_createdby` | String | Identité de l’utilisateur qui a créé la tâche. Cet attribut est une chaîne encodée JSON, par exemple {\"user\": {\"displayName,ID\"\"\":\"d55...\"}} |
| `m365_createddatetime` | Date/heure | En lecture seule. Date et heure auxquelles la tâche est créée. Le type d’horodatage représente les informations de date et d’heure au moyen du format ISO 8601. Il est toujours au format d’heure UTC. Par exemple, minuit UTC le 1er janvier 2014 est 2014-01-01T00:00:00Z |
| `m365_duedatetime` | Date/heure | Date et heure auxquelles la tâche doit être effectuée. Le type d’horodatage représente les informations de date et d’heure au moyen du format ISO 8601. Il est toujours au format d’heure UTC. Par exemple, minuit UTC le 1er janvier 2014 est 2014-01-01T00:00:00Z |
| `m365_hasdescription` | Boolean | En lecture seule. La valeur est true si l’objet de détails de la tâche a une description non vide et false dans le cas contraire. |
| `m365_id` | String | En lecture seule. ID de la tâche. Il comporte 28 caractères et respecte la casse. [Une validation du format](/graph/api/resources/planner-identifiers-disclaimer) est effectuée sur le service.|
| `m365_orderhint` | String | Indicateur utilisé pour commander des éléments de ce type dans une vue de liste. Le format est défini comme décrit à [l’aide d’indicateurs de commande dans le Planificateur](/graph/api/resources/planner-order-hint-format). |
| `m365_percentcomplete` | Int32 | Pourcentage d’achèvement de la tâche. Lorsque la valeur est 100, la tâche est considérée comme terminée. |
| `m365_priority` | Int32 | Priorité de la tâche. La plage de valeurs valide est comprise entre 0 et 10, la valeur croissante étant de priorité inférieure (0 a la priorité la plus élevée et 10 a la priorité la plus basse). Actuellement, le Planificateur interprète les valeurs 0 et 1 comme « urgentes », 2, 3 et 4 comme « importantes », 5, 6 et 7 comme « moyennes » et 8, 9 et 10 comme « faibles ». En outre, planner définit la valeur 1 pour « urgent », 3 pour « important », 5 pour « moyen » et 9 pour « faible ». |
| `m365_planid` | Chaîne | ID du plan auquel appartient la tâche. |
| `m365_previewtype` | String | Définit le type d’aperçu qui s’affiche sur la tâche. Les valeurs possibles sont : automatique, noPreview, checklist, description, reference. |
| `m365_referencecount` | Int32 | Nombre de références externes qui existent sur la tâche.|
| `m365_startdatetime` | Date/heure | Date et heure de début de la tâche. Le type d’horodatage représente les informations de date et d’heure au moyen du format ISO 8601. Il est toujours au format d’heure UTC. Par exemple, minuit UTC le 1er janvier 2014 est 2014-01-01T00:00:00Z |
| `m365_title` | Chaîne |Titre de la tâche. Colonne de recherche principale |

## <a name="graph-planner-plan"></a>Plan du Planificateur Graph

* Nom de l’entité : m365_graphplannerplan.
* Ressource Graph : [type de ressource plannerPlan](/graph/api/resources/plannerplan).
* Le tri n’est pas pris en charge.
* Le filtrage n’est pas pris en charge.
* La pagination pilotée par le serveur est prise en charge, avec une taille de page maximale de 400.

### <a name="attributes-for-graph-planner-plan"></a>Attributs du plan Graph Planner

| Column  | Dataverse Type | Détails |
|---|---|---|
| `m365_collaborationrootid` | String | ID racine de collaboration de la session de collaboration à laquelle l’enregistrement est associé. Si l’enregistrement est associé à plusieurs sessions de collaboration, il est retourné sous la forme d’une chaîne délimitée par des virgules. Notez que cet attribut ne sera pas retourné lors de la récupération de plusieurs enregistrements.|
| `m365_graphplannerplanid` |Guid |Identificateur unique du plan du planificateur de graphes.|
| `m365_createdby` | String | Identité de l’utilisateur qui a créé la tâche. Cet attribut est une chaîne encodée JSON, par exemple {\"user\": {\"displayName,ID\"\"\":\"d55...\"}} |
| `m365_createddatetime` | Date/heure | En lecture seule. Date et heure auxquelles la tâche est créée. Le type d’horodatage représente les informations de date et d’heure au moyen du format ISO 8601. Il est toujours au format d’heure UTC. Par exemple, minuit UTC le 1er janvier 2014 est 2014-01-01T00:00:00Z |
| `m365_id` | String | En lecture seule. ID du plan. Il comporte 28 caractères et respecte la casse. [Une validation du format](/graph/api/resources/planner-identifiers-disclaimer) est effectuée sur le service.|
| `m365_owner` | String | ID du [groupe](/graph/api/resources/group) propriétaire du plan. Une fois définie, cette propriété ne peut pas être mise à jour.|
| `m365_title` | String | Titre du plan. Colonne de recherche principale |

## <a name="graph-event"></a>Événement Graph

* Nom de l’entité : m365_graphevent
* Ressource Graph : [type de ressource d’événement](/graph/api/resources/event)
* Le tri est pris en charge sur les colonnes suivantes :
  * m365_lastmodifieddatetime
  * m365_createddatetime
  * m365_hasattachments
  * m365_importance
  * m365_responserequested
  * m365_sensitivity
  * m365_showas
  * m365_subject
* Le filtrage est pris en charge sur les colonnes suivantes :
  * m365_allownewtimeproposals
  * m365_lastmodifieddatetime
  * m365_createddatetime
  * m365_icaluID
  * m365_importance
  * m365_isallday
  * m365_iscancelled
  * m365_isdraft
  * m365_responserequested
  * m365_sensitivity
  * m365_showas
  * m365_subject
  * m365_type
* La pagination pilotée par le serveur est prise en charge.

### <a name="attributes-for-graph-event"></a>Attributs pour l’événement Graph

| Column |Dataverse Type |Détails |
|---|---|---|
|`m365_collaborationrootid` |String |Racine de collaboration de la session de collaboration à qui l’enregistrement est associé. Si l’enregistrement est associé à plusieurs sessions de collaboration, il est retourné sous la forme d’une chaîne délimitée par des virgules. Notez que cet attribut ne sera pas retourné lors de la récupération de plusieurs enregistrements. |
|`m365_allownewtimeproposals` |Boolean |True, si l’organisateur de la réunion autorise les invités à proposer une nouvelle heure lors de la réponse. Sinon, false, ce qui est facultatif. La valeur par défaut est true. |
|`m365_attendees` |String |Collection des participants à l’événement. Cet attribut est une chaîne encodée JSON d’une longueur maximale de 15 000. Par exemple, [{{\"type\":\"required,status\"\"\":{{\"response\":\"none,time\"\"\":\"0001-01-01T00:00:00Z\"}},\"emailAddress\":\"test@contoso.com\"}}] |
|`m365_body` |String |Corps du message associé à l’événement. Il peut avoir le format HTML ou texte. Cet attribut est une chaîne encodée JSON d’une longueur maximale de 15 000. Par exemple {\"contentType\":\"html,content\"\"\":\"html/html\"} |
|`m365_bodypreview` |String |Aperçu du message associé à l’événement. Valeur au format texte. |
|`m365_categories` |Chaîne |Catégories associées à l’événement. Chaque catégorie correspond à la propriétédisplayNamed’unoutlookCategorydéfini pour l’utilisateur. Par exemple [\"chaîne\"] |
|`m365_changekey` |Chaîne |Identifie la version de l’objet « event ». Chaque fois que l’événement est modifié, la propriété ChangeKey change également. Exchange peut ainsi appliquer les modifications à la version correcte de l’objet. |
|`m365_createddatetime` |Date/heure |Le type d’horodatage représente les informations de date et d’heure au moyen du format ISO 8601. Il est toujours au format d’heure UTC. Par exemple, minuit UTC le 1er janvier 2014 est 2014-01-01T00:00:00Z |
|`m365_start` |Date/heure |Date, heure et fuseau horaire de début de l’événement. Cet attribut est une chaîne encodée JSON d’une longueur maximale de 100. Par exemple {\"dateTime\":\"2022-01-19T11:00:00+00:00,timeZone\"\"\":\"UTC}\"|
|`m365_end` |Date/heure |Date, heure et fuseau horaire de fin de l’événement. Cet attribut est une chaîne encodée JSON d’une longueur maximale de 100. Par exemple {\"dateTime\":\"2022-01-19T11:00:00+00:00,timeZone\"\"\":\"UTC}\" |
|`m365_hasattachments` |Boolean |Valeur True si l’événement a des pièces jointes. |
|`m365_hideattendees` |Boolean |Lorsque la valeur est true, chaque participant se voit uniquement dans la liste des demandes de réunion et du suivi des réunions. La valeur par défaut est False. |
|`m365_icaluid` |String |Un identificateur unique pour un événement sur plusieurs calendriers. Cet ID est différent pour chaque occurrence dans une série périodique. En lecture seule. |
|`m365_isallday`|Boolean |Défini à true si l'événement dure toute la journée. Si vrai, qu’il s’agisse d’un événement d’un seul jour ou de plusieurs jours, l’heure de début et de fin doit être réglée sur minuit et se trouver dans le même fuseau horaire. |
|`m365_iscancelled` |Boolean |Valeur True si l’événement a été annulé. |
|`m365_id`| String |En lecture seule. ID de l’événement. |
|`m365_isdraft` |Boolean |Défini sur true si l’utilisateur a mis à jour la réunion dans Outlook, mais n’a pas envoyé les mises à jour aux participants. Configurez la valeur sur False si toutes les modifications ont été envoyées ou si l’événement est un rendez-vous sans participants.|
|`m365_isonlinemeeting`|Boolean|True si cet événement contient des informations de réunion en ligne (autrement dit, onlineMeeting pointe vers une ressource onlineMeetingInfo), false dans le cas contraire. La valeur par défaut est false (onlineMeeting est null). Facultatif. Une fois que vous avez défini isOnlineMeeting sur true, Microsoft Graph initialise onlineMeeting. Outlook ignore ultérieurement les autres modifications apportées à isOnlineMeeting, et la réunion reste disponible en ligne.|
|`m365_isorganizer`|Boolean|La valeur True est attribuée à cet élément si le propriétaire du calendrier (spécifié par la propriété owner du calendrier) est l’organisateur de l’événement (spécifié par la propriété organizer de l’événement). Cela s’applique également si un délégué a organisé l’événement au nom du propriétaire.|
|`m365_isremindero`n|Boolean|Valeur True si une alerte est définie pour rappeler l’événement à l’utilisateur.|
|`m365_lastmodifieddatetime`|Date/heure|Le type d’horodatage représente les informations de date et d’heure au moyen du format ISO 8601. Il est toujours au format d’heure UTC. Par exemple, minuit UTC le 1er janvier 2014 est 2014-01-01T00:00:00Z|
|`m365_location`|String|Emplacement de l’événement. Chaîne encodée JSON, longueur maximale de 4 000. Par exemple[{\"address\":null,coordinates\"\":null,displayName\"\":\"Harry\'s Bar,locationEmailAddress\"\"\":null,locationType\"\":\"default,locationUri\"\"\":null,uniqueId\"\":\"Harry\'s Bar,uniqueIdType\"\"\":\"private}\"|
|`m365_locations`|String|Emplacements où l’événement est tenu. Les propriétés location et locations se correspondent toujours mutuellement. Si vous mettez à jour la propriété location, tous les emplacements précédents dans la collection locations sont supprimés et remplacés par la nouvelle valeur location. Chaîne encodée JSON, longueur maximale 4000.par exemple[{\"address:null,coordinates\"\":null,displayName\"\":\"Harry\'s Bar,locationEmailAddress\"\"\":null,locationType\"\":\"default,locationUri\"\"\":null,uniqueId\"\":\"Harry\'s Bar,uniqueIdType\"\"\":\"private\"}]\"|
|`m365_onlinemeeting`|String|Détails pour qu’un participant rejoigne la réunion en ligne. La valeur de cette propriété est définie par défaut sur « null ». En lecture seule.Après avoir défini les propriétés isOnlineMeeting et onlineMeetingProvider pour activer une réunion en ligne, Microsoft Graph initialise onlineMeeting. Quand elle est définie, la réunion reste disponible en ligne et vous ne pouvez plus modifier les propriétés isOnlineMeeting, onlineMeetingProvider et onlneMeeting. Chaîne encodée JSON, longueur maximale 4000.par exemple{conferenceId: String,joinUrl\"\"\": \"String,phones\"\"\": [{\"@odata.type\": \"microsoft.graph.phone\"}],\"quickDial\": \"String,tollFreeNumbers\"\"\": [\"String\"],\"tollNumber\": \"String}\"\"\"\"|
|`m365_onlinemeetingprovider`|String|Détails pour qu’un participant rejoigne la réunion en ligne. La valeur de cette propriété est définie par défaut sur « null ». En lecture seule. Une fois que vous avez défini isOnlineMeeting et `onlineMeetingProvider` les propriétés pour activer une réunion en ligne, Microsoft Graph initialise onlineMeeting. Quand elle est définie, la réunion reste disponible en ligne et vous ne pouvez pas modifier à nouveau les propriétés isOnlineMeeting `onlineMeetingProvider`et onlneMeeting.|
|`m365_onlinemeetingurl`|String|Une URL pour une réunion en ligne. Cette propriété est définie uniquement lorsqu’un organisateur spécifie dans Outlook qu’un événement est une réunion en ligne telle que Skype. Lecture seule. Pour accéder à l’URL pour participer à une réunion en ligne, utilisez `joinUrl`, qui est exposée via la `onlineMeeting` propriété de l’événement. La `onlineMeetingUrl` propriété sera dépréciée à l’avenir.|
|`m365_organizer`|String|Organisateur de l’événement. Chaîne encodée JSON, longueur maximale de 4 000. {\"emailAddress\":{\"@odata.type\":\"microsoft.graph.emailAddress\"}}|
|`m365_originalendtimezone`|String|Fuseau horaire de fin défini lors de la création de l’événement. La valeur tzone://Microsoft/Custom indique qu’un fuseau horaire personnalisé hérité a été défini dans Outlook de bureau.|
|`m365_originalstart`|Date/heure|Représente l’heure de début d’un événement lorsqu’il est initialement créé en tant qu’occurrence ou exception dans une série périodique. Cette propriété n’est pas retournée pour les événements qui sont des instances uniques. Les informations de date et d’heure suivent le format ISO 8601 et sont toujours au format UTC. Par exemple, minuit UTC le 1er janvier 2014 est 2014-01-01T00:00:00Z|
|`m365_originalstarttimezone`|String|Fuseau horaire de début défini lors de la création de l’événement. La valeur tzone://Microsoft/Custom indique qu’un fuseau horaire personnalisé hérité a été défini dans Outlook de bureau.|
|`m365_recurrence`|String|Modèle de périodicité pour l’événement. Chaîne encodée JSON, longueur maximale 4000.par exemple{pattern:{\"dayOfMonth\":0,daysOfWeek\"\":[\"monday,wednesday,friday\"\"\"\"\"],\"firstDayOfWeek\":\"sunday,index\"\"\":\"first,interval\"\"\":1,month\"\":0,type\"\":\"weekly\"},\"range\":{\"startDate\":\"2017-08-14,endDate\"\"\":\"2018-08-14,\"\"\"\" numberOfOccurrences\":0,recurrenceTimeZone\"\":\"Eastern Standard Time,type\"\"\":\"endDate\"}}|
|`m365_reminderminutesbeforestart`|Int32|Nombre de minutes avant la date de début de l’événement où l’alerte de rappel a lieu.|
|`m365_responserequested`|Boolean|La valeur par défaut est true, ce qui signifie que l’organisateur souhaite qu’un invité envoie une réponse à l’événement.|
|`m365_responsestatus`|String|Indique le type de réponse envoyé en réponse à un message d’événement. Chaîne encodée JSON, longueur maximale de 4 000. {\"response\": \"String,time\"\"\": \"String (timestamp)\"}|
|`m365_sensitivity`|String|Les valeurs possibles sont : normal, personnel, privé, confidentiel.|
|`m365_seriesmasterid`|String|L’ID de la série maîtrise un élément périodique, si cet événement fait partie d’une série périodique.|
|`m365_showas`|String|État à afficher. Les valeurs possibles sont : free, tentative, busy, oof, workingElsewhere, unknown.|
|`m365_subject`|String|Texte de la ligne d’objet de l’événement. Colonne de recherche principale|
|`m365_transactionid`|String|Identificateur personnalisé spécifié par une application cliente pour le serveur afin d’éviter les opérations POST redondantes si le client tente à nouveau de créer le même événement. Ceci est utile lorsque la connectivité réseau faible entraîne l’expirer le client avant de recevoir une réponse du serveur pour la demande d’événement de création précédente du client. Une fois que vous avez défini `transactionId` lors de la création d’un événement, vous ne pouvez pas modifier transactionId dans une mise à jour ultérieure. Cette propriété est uniquement renvoyée dans une charge utile de réponse si une application l’a activée. Facultatif.|
|`m365_type`|String|Type d’événement. Les valeurs possibles sont : singleInstance, occurrence, exception, seriesMaster. Lecture seule|
|`m365_weblink`|Chaîne|URL permettant d’ouvrir l’événement dans Outlook sur le web. Outlook sur le web ouvre l’événement dans le navigateur si vous êtes connecté à votre boîte aux lettres. sinon, Outlook sur le web vous invite à vous connecter. Cette URL n’est pas accessible à partir d’un iFrame.|
|`m365_grapheventid`|Guid|Identificateur unique de l’événement de graphe.|
|`m365_groupid`|String|ID de groupe auquel appartient l’événement.|

## <a name="graph-booking-appointment"></a>Rendez-vous de réservation Graph

* Nom de l’entité : m365_graphbookingappointment
* Ressource Graph : [type de ressource bookingAppointment](/graph/api/resources/bookingappointment)
* Le tri n’est pas pris en charge.
* Le filtrage est pris en charge sur les colonnes suivantes :
  * m365_bookingbusinessID
  * m365_collaborationrootID
  * m365_customertimezone
  * m365_optoutofcustomeremail
  * m365_price
  * m365_pricetype
  * m365_serviceID
  * m365_servicename
* La pagination n’est pas prise en charge.

### <a name="attributes-for-graph-booking-appointment"></a>Attributs du rendez-vous de réservation Graph

| Column  | Dataverse Type | Détails |
|---|---|---|
| `m365_collaborationrootid`| String| ID racine de collaboration de la session de collaboration à laquelle l’enregistrement est associé. Si l’enregistrement est associé à plusieurs sessions de collaboration, il est retourné sous la forme d’une chaîne délimitée par des virgules. Notez que cet attribut ne sera pas retourné lors de la récupération de plusieurs enregistrements.|
| `m365_graphbookingappointmentid` | Guid | Identificateur unique du rendez-vous de réservation de graphe.|
| `m365_bookingbusinessid` | String | Identificateur unique de l’entreprise de réservation sous lequel le rendez-vous est planifié.|
| `m365_additionalinformation` | String | Informations supplémentaires envoyées au client lorsqu’un rendez-vous est confirmé.|
| `m365_customers` | String| Il répertorie les propriétés du client pour un rendez-vous. le rendez-vous contiendra une liste d’informations client et chaque unité indiquera les propriétés d’un client qui fait partie de ce rendez-vous. Facultatif[{\"customerID\":\"d243c77b-f1ff-4615-a01f-1660b5cb0e79,customQuestionAnswers\"\"\":[],\"emailAddress\":\"jordanm@contoso.com,location\"\"\":{address\":{\"\"city\":\"\",\"countryOrRegion\":,\"postalCode\":\"\"\"\",\"postOfficeBox,state\"\"\":\"\",\"street\":\"\",\"type\" },\"coordinates\":{\" accuracy,altitude,altitudeAccuracy,latitude,longitude\"\"\"\"\"\"\"\"\" },\"displayName\":\"\",\"locationEmailAddress,locationType,locationUri\"\"\"\"\":\"\",\"uniqueID,uniqueIDType\"\"\" },\"name\":\"Jordan Miller,notes,phone,timeZone\"\"\"\"\"\"\",\"@odata.type:\"\" #microsoft.graph.bookingCustomerInformation\"}] |
| `m365_customertimezone` | String | Fuseau horaire du client. Pour obtenir la liste des valeurs possibles, consultez le [type de ressource dateTimeTimeZone](/graph/api/resources/datetimetimezone). |
| `m365_duration` | String | Longueur du rendez-vous, indiquée au format ISO8601.|
| `m365_enddatetime` | Date/heure | Date, heure et fuseau horaire de fin du rendez-vous.|
| `m365_filledattendeescount` | Int32 | Nombre actuel de clients dans le rendez-vous.|
| `m365_id` | String | ID du bookingAppointment. En lecture seule.|
| `m365_islocationonline` | Boolean | True indique que le rendez-vous sera tenu en ligne. La valeur par défaut est false.|
| `m365_joinweburl` | String | URL de la réunion en ligne pour le rendez-vous.|
| `m365_maximumattendeescount` | Int32 | Nombre maximal de clients autorisés dans un rendez-vous.|
| `m365_optoutofcustomeremail` | Boolean | True indique que bookingCustomer pour ce rendez-vous ne souhaite pas recevoir de confirmation pour ce rendez-vous.|
| `m365_postbuffer` | String | Durée à réserver une fois le rendez-vous terminé, pour le nettoyage, par exemple. La valeur est exprimée au format ISO8601.|
| `m365_prebuffer` | String | Durée de réserve avant le début du rendez-vous, pour la préparation, par exemple. La valeur est exprimée au format ISO8601.|
| `m365_price` | DecimalType | Prix normal d’un rendez-vous pour le bookingService spécifié.|
| `m365_pricetype` | String | Paramètre permettant d’offrir de la flexibilité pour la structure tarifaire des services. Les valeurs possibles sont : undefined, fixedPrice, startingAt, hourly, free, priceVaries, callUs, notSet.|
| `m365_reminders` | String | Collection de rappels de clients envoyés pour ce rendez-vous. La valeur de cette propriété est disponible uniquement lors de la lecture de cet bookingAppointment par son ID. [{\"message\":\"Nous sommes impatients de vous voir!\",\"offset\":\"P1D,recipients\"\"\":\"customer\"},{\"message\":\"Reminder that you have a appointment!\",\"offset\":\"P1D,recipients\"\"\":\"staff\"}] |
| `m365_selfserviceappointmentid` | String | Autre ID de suivi du rendez-vous, si le rendez-vous a été créé directement par le client sur la page de planification, par opposition à un membre du personnel au nom du client.|
| `m365_serviceid` | String | ID du bookingService associé à ce rendez-vous.|
| `m365_servicelocation` | String | Emplacement où le service est fourni. {\"address\":{\"city\":\"\",\"countryOrRegion\":\"\",\"postalCode\":\"\",\"postOfficeBox,state\"\"\":\"\",\"street\":\"\",\"type\" },\"coordinates\":{\"accuracy,altitude,altitudeAccuracy,latitude,longitude\"\"\"\"\"\"\"\"\" },\"displayName\":\"Our office address,locationEmailAddress\"\" \",\"locationType,locationUri\"\"\":\"\",\"uniqueID,uniqueIDType\"\"\" } |
| `m365_servicename` | String | Nom du bookingService associé à ce rendez-vous. Cette propriété est facultative lors de la création d’un rendez-vous. S’il n’est pas spécifié, il est calculé à partir du service associé au rendez-vous par la propriété serviceID. |
| `m365_servicenotes` |String | Notes d’un bookingStaffMember. La valeur de cette propriété est disponible uniquement lors de la lecture de ce bookingAppointment par son ID.|
| `m365_smsnotificationsenabled` | Boolean | True indique que des notifications SMS seront envoyées aux clients pour le rendez-vous. La valeur par défaut est false.|
| `m365_staffmemberids` | String | ID de chaque bookingStaffMember qui est planifié dans ce rendez-vous. Stocké sous la forme d’une chaîne séparée par des virgules. [\"string\"] |
| `m365_startdatetime` | Date/heure | Date, heure et fuseau horaire de début du rendez-vous.|

## <a name="graph-drive"></a>Lecteur Graph

* Nom de l’entité : m365_graphdrive
* Ressource Graph : [type de ressource de lecteur](/graph/api/resources/drive)
* Le tri n’est pas pris en charge.
* Le filtrage n’est pas pris en charge.
* La pagination pilotée par le serveur est prise en charge.

### <a name="attributes-for-graph-drive"></a>Attributs du lecteur Graph

|Column |Dataverse Type |Détails |
|---|---|---|
|`m365_collaborationrootid` |String | ID racine de collaboration de la session de collaboration à laquelle l’enregistrement est associé. Si l’enregistrement est associé à plusieurs sessions de collaboration, il est retourné sous la forme d’une chaîne délimitée par des virgules. Notez que cet attribut ne sera pas retourné lors de la récupération de plusieurs enregistrements. |
|`m365_createdby` |String |Identité de l’utilisateur, de l’appareil ou de l’application qui a créé l’élément. En lecture seule. Cet attribut est une chaîne encodée JSON, par exemple { « user »: { « displayName »: « System Account » } } |
|`m365_createddatetime` |Date/heure |Date et heure de création de l’élément. En lecture seule. |
|`m365_description` |String |Fournit une description du lecteur visible par l’utilisateur. En lecture seule. |
|`m365_drivetype` |Chaîne |Décrit le type de lecteur représenté par cette ressource. Les lecteurs personnels OneDrive retournent des lecteurs personnels. OneDrive Entreprise retournera l’entreprise. Les bibliothèques de documents SharePoint retournent documentLibrary. En lecture seule. |
|`m365_graphdriveid` |Guid |Identificateur unique du lecteur de graphe. |
|`m365_id` |String |Identificateur unique du lecteur. En lecture seule. |
|`m365_lastmodifiedby` | String |Identité de l’utilisateur, de l’appareil et de l’application, qui a modifié l’élément pour la dernière fois. En lecture seule. Cet attribut est une chaîne encodée JSON par exemple { « user »: { « email »: « user@contoso.com », « ID »: « 61de164e-21ff-4b1c-8cbd-77ac440894f8 », « displayName »: « User Name » } } |
|`m365_lastmodifieddatetime` |Date/heure |Date et heure de la dernière modification de l’élément. En lecture seule.|
|`m365_name` |String |Nom de l'élément. En lecture seule. |
|`m365_owner` |String |Facultatif. Compte d’utilisateur qui possède le lecteur. En lecture seule. Cet attribut est une chaîne encodée JSON. Par exemple { « group »: { « ID »: « 76c7286f-8645-4ba8-bc0f-c65a16424aaa », « displayName »: « Nom du groupe » }} |
|`m365_quota` |String |Facultatif. Informations sur le quota d’espace de stockage du lecteur. En lecture seule. Cet attribut est une chaîne encodée JSON. Par exemple { « deleted »: 482586, « remaining »: 27487788645969, « state »: « normal », « total »: 27487790694400, « used »: 1565845 } |
|`m365_sharepointids` |String |Retourne des identificateurs utiles pour la compatibilité REST SharePoint. En lecture seule. Cette propriété n’est pas retournée par défaut et doit être sélectionnée à l’aide du paramètre de requête $select. Cet attribut est une chaîne encodée JSON. Par exemple , « sharePointIDs » : { « listID » : « 29d8457a-8e26-4291-9901-09718a388aaa », « siteID » : « 93618739-b3ca-4107-a77c-fba278c48aaa », « siteUrl »: « <https://contoso.sharepoint.com> », « tenantID »: « 53986071-de92-43ad-a41f-f3c4adb2beef », « webID »: « a0d0e9ec-e547-4338-92d9-4c2c62e5beef » } |
| `m365_siteid` |String |Identificateur du site qui contient la bibliothèque de documents.
|`m365_system` |String |Si la propriété est présente, elle indique qu’il s’agit d’un lecteur géré par le système. En lecture seule.
|`m365_weburl` |Chaîne |URL qui affiche la ressource dans le navigateur. En lecture seule.

### <a name="graph-drive-item"></a>Élément de lecteur Graph

* Nom de l’entité : m365_graphdriveitem
* Ressource Graph : [type de ressource driveItem](/graph/api/resources/driveitem)
* Le tri est pris en charge sur la colonne suivante :
  * m365_name
* Le filtrage est pris en charge sur la colonne suivante :
  * m365_name
* La pagination pilotée par le serveur est prise en charge.

### <a name="attributes-for-graph-drive-item"></a>Attributs de l’élément de lecteur Graph

|Column |Dataverse Type |Détails |
|---|---|---|
|`m365_audio` |String |Métadonnées audio, si l’élément est un fichier audio. En lecture seule. Uniquement sur OneDrive Personnel. Cet attribut est une chaîne encodée JSON. { « album »: « string », « albumArtist »: « string », artist »: « string », bitrate »: 128, « composers »: « string », copyright »: « string », « disc »: 0, « discCount »: 0, « duration »: 567, « genre »: « string », « hasDrm »: false, « isVariableBitrate »: false, « title »: « string », « track »: 1, « trackCount »: 16, « year »: 2014 }|
|`M365_bundle` |String |Métadonnées d’ensemble, si l’élément est un ensemble d’éléments. En lecture seule. Cet attribut est une chaîne encodée JSON. Par exemple, { « childCount »: 3, « album »: { « @odata.type »: « microsoft.graph.album » }, } |
|`m365_collaborationrootid` |String |ID racine de collaboration de la session de collaboration à laquelle l’enregistrement est associé. Si l’enregistrement est associé à plusieurs sessions de collaboration, il est retourné sous la forme d’une chaîne délimitée par des virgules. Notez que cet attribut ne sera pas retourné lors de la récupération de plusieurs enregistrements. |
|`m365_copy` |String |Si elle est présente dans la demande, une opération de copie est effectuée. |
|`m365_createdby` |String |Identité de l’utilisateur, de l’appareil et de l’application, qui a créé l’élément. En lecture seule. Cet attribut est une chaîne encodée JSON. Par exemple, {"user »:{"displayName »:"User Name »,"email »:"alias@contoso.com »,"ID »:"a298b975-3493-4d9e-b2d4-3cad78f00000"},"group »: null,"application »,"device » } |
|`m365_createddatetime` |Date/heure |Date et heure de création de l’élément. En lecture seule. |
|`m365_ctag` |String |eTag du contenu de l’élément. Ce eTag n’est pas modifié si seules les métadonnées sont modifiées. Note. Cette propriété n’est pas retournée si l’élément est un dossier. En lecture seule. |
|`m365_deleted` |String |Informations sur l’état de suppression de l’élément. En lecture seule. Cet attribut est une chaîne encodée JSON. Par exemple, { « state »: « string » } |
|`m365_description` |String |Fournit une description de l’élément visible par l’utilisateur. En lecture-écriture. Uniquement sur OneDrive Personnel |
|`m365_driveid` |String |Identificateur du lecteur qui contient l’élément de lecteur.|
|`m365_etag` |String |eTag de l’élément entier (métadonnées + contenu). En lecture seule. |
| `m365_file` |String |Métadonnées du fichier, si l’élément est un fichier. En lecture seule. Cet attribut est une chaîne encodée JSON. Par exemple, {"hashes »:{"crc32Hash »,"quickXorHash »:"Biuzvwdu+Tmu6yRefayD27hD9vD= »,"sha1Hash « ,"sha256Hash » },"mimeType »:"application/vnd.openxmlformats-officedocument.wordprocessingml.document »,"processingMetadata » } |
| `m365_filesysteminfo` |String |Informations du système de fichiers sur le client. Cet attribut est une chaîne encodée JSON. Par exemple, {"createdDateTime »:"2022-07-21T15:02:47+00:00 »,"lastAccessedDateTime »,"lastModifiedDateTime »:"2022-07-21T15:02:55+00:00"} |
|`m365_folder` |String | Métadonnées du dossier, si l’élément est un dossier. En lecture seule. Cet attribut est une chaîne encodée JSON. Par exemple, {"childCount »:0,"view » } |
|`m365_graphdriveitemid` |Guid |Identificateur unique de l’élément de lecteur de graphe. |
|`m365_id` |String |Identificateur unique de l’élément dans le lecteur. En lecture seule. |
|`m365_image` |String |Métadonnées de l’image, si l’élément est une image. En lecture seule. Cet attribut est une chaîne encodée JSON. Par exemple, {"height »,"width » } |
|`m365_lastmodifiedby` |String |Identité de l’utilisateur, de l’appareil et de l’application, qui a modifié l’élément pour la dernière fois. En lecture seule. Cet attribut est une chaîne encodée JSON. Par exemple, {"user »:{"displayName »:"User Name »,"email »:"alias@contoso.com »,"ID »:"a298b975-3493-4d9e-b2d4-3cad78f9a00e"},"group »,"application »,"device » } |
|`m365_lastmodifieddatetime` |Date/heure |Date et heure de la dernière modification de l’élément. En lecture seule. |
|`m365_location` |String |Emplacement des métadonnées, si l’élément possède des données d’emplacement. En lecture seule. Cet attribut est une chaîne encodée JSON. Par exemple, « location »: { « altitude »: 1.0, « latitude »: 1.0, « longitude »: 1.0 } |
|`m365_malware` |String |Métadonnées de programme malveillant, si l’élément a été détecté comme contenant des programmes malveillants. En lecture seule. Cet attribut est une chaîne encodée JSON. Par exemple, { « description »: « string » } |
|`m365_name` |String |Nom de l’élément (nom de fichier et extension). En lecture-écriture. |
|`m365_package` |String |Le cas échéant, indique que cet élément est un package au lieu d’un dossier ou d’un fichier. Les packages sont traités comme des fichiers dans certains contextes et comme des dossiers dans d’autres. En lecture seule. Cet attribut est une chaîne encodée JSON. Par exemple, { « type »: « oneNote » } |
|`m365_parentreference` |String |Informations de l’élément parent, si l’élément possède un parent. Cet attribut est une chaîne encodée JSON. Par exemple, {"driveID »:"b!qgK-8nOzX0qISvfGCiC2Smbv0m0RlNhDvNQDZsCMpbSnchFAhWAaQoiTLZcSo1gq »,"driveType »:"documentLibrary »,"ID »:"01EYDCV4YHV77FE3EDDFHIVD6WJ2ETT3PP »,"name »,"path »:"/drives/b!qgK-8nOzX0qISvfGCiC2Smbv0m0RlNhDvNQDZsCMpbSnchFAhWAaQoiTLZcSo1no/root: /folder name »,"shareID »,"sharepointIDs »:{"listID »:"401172a8-6085-421a-8893-12d9712a35c3c »,"listItemID »,"listItemUniqueID »:"52feaf12-836c-4e19-8a8f-d64e8939ee52 »,"siteID »: » f34e02aa-b373-4a5f-884a-f7c60a20b64a »,"siteUrl »: »https://contoso.sharepoint.com/sites/Contoso,"tenantID »,"webID »:"6dd2ef66-9411-43d8-bcd4-0366c08ccabd"},"siteID » } |
|`m365_parentreferenceid` |String |Identificateur de l’élément de lecteur qui est le parent de l’élément de lecteur. |
|`m365_pendingoperations` |String |S’il est présent, indique qu’une ou plusieurs opérations pouvant affecter l’état de la driveItem sont en attente d’achèvement. En lecture seule. Cet attribut est une chaîne encodée JSON. Par exemple, { « pendingContentUpdate »: {"@odata.type »: « microsoft.graph.pendingContentUpdate"} } |
|`m365_photo` |String |Métadonnées de la photo, si l’élément est une photo. En lecture seule. Cet attribut est une chaîne encodée JSON. Par exemple, { « cameraMake »: « Camera Make », « cameraModel »: « Camera Model », « exposureDenominator »: 1000000, « exposureNumerator »: 41671, « focalLength »: 4.38, « fNumber »: 1.73, « iso »: 70, « orientation »: 6, « takenDateTime »: « 2020-04-29T14:17:39Z » } |
|`m365_publication` |String |Indique si un élément a été publié ou extrait, à des emplacements qui prennent en charge ces actions. Cette propriété n’est pas retournée par défaut. En lecture seule. Cet attribut est une chaîne encodée JSON. Par exemple, {"level »:"published »,"versionID »:"2.0"} |
|`m365_remoteitem` |String |Données de l’élément à distance, si l’élément est partagé depuis un autre lecteur que celui auquel l’utilisateur accède actuellement. En lecture seule. Cet attribut est une chaîne encodée JSON. Par exemple, { « ID »: « string », « createdBy »: { « @odata.type »: « microsoft.graph.IdentitySet » }, « createdDateTime »: « timestamp », « file »: { « @odata.type »: « microsoft.graph.file » }, « fileSystemInfo »: { « @odata.type »: « microsoft.graph.fileSystemInfo » }, « folder »: { « @odata.type »: « microsoft.graph.folder » }, « image »: { « @odata.type »: « microsoft.graph.image » }, « lastModifiedBy »: { « @odata.type »: « microsoft.graph.IdentitySet » }, « lastModifiedDateTime »: « timestamp », « name »: « string », « package »: { » @odata.type »: « microsoft.graph.package » }, « parentReference »: { « @odata.type »: « microsoft.graph.itemReference » }, « shared »: { « @odata.type »: « microsoft.graph.shared » }, « sharepointIDs »: { « @odata.type »: « microsoft.graph.sharepointIDs » }, }, « specialFolder »: { « @odata.type »: « microsoft.graph.specialFolder » }, « size »: 1024, « video »: { « @odata.type »: « microsoft.graph.video » }, « webDavUrl »: « url », « webUrl »: « url » } |
|`m365_root` |String |Si cette propriété est non null, elle indique qu’il s’agit du driveItem le plus élevé dans le lecteur. |
|`m365_searchresult` |String |Métadonnées de la recherche, si l’élément est issu d’une recherche. En lecture seule. Cet attribut est une chaîne encodée JSON. Par exemple, { « onClickTelemetryUrl »: « url » } |
|`m365_shared` |String |Indique que l’élément a été partagé avec d’autres personnes et fournit des informations sur l’état de partage de l’élément. En lecture seule. Cet attribut est une chaîne encodée JSON. Par exemple, { « scope »: « users », « owner »: { « user »: { « displayName »: « User Name », « ID »: « bbbb6fa48aaaaa » } } } } |
|`m365_sharepointids` |String |Retourne des identificateurs utiles pour la compatibilité REST SharePoint. En lecture seule. Cet attribut est une chaîne encodée JSON. par exemple{"listID »:"401172a7-6085-421a-8893-2d9712a35aba »,"listItemID »:"338" »,"listItemUniqueID »:"0edc89e5-24ea-4c6b-a019-dc51f45eeccc »,"siteID »:"f2be02aa-b37 3-4a5f-884a-f7c60a20bddd »,"siteUrl »: »https://contoso.sharepoint.com/sites/Contoso,"tenantID »:"1c137272-0581-487f-b195-aeeb93cc4ccc »,"webID »:"6dd2ef66-9411-43d8-bcd4-0366c08caaaa"} |
|`m365_siteid` |String |Identificateur du site qui contient la bibliothèque de documents. |
|`m365_size` |IntType |Taille de l’élément en octets. En lecture seule. |
|`m365_specialfolder` |String |Si l’élément actuel est également disponible sous la forme d’un dossier spécial, cette facette est renvoyée. En lecture seule. Cet attribut est une chaîne encodée JSON. Par exemple, { « name »: « documents » } |
|`m365_thumbnail` |String |Si elle est présente dans la demande, les miniatures de l’élément de lecteur sont récupérées. |
|`m365_video` |String |Si l’élément actuel est également disponible sous la forme d’un dossier spécial, cette facette est renvoyée. En lecture seule. Cet attribut est une chaîne encodée JSON. Par exemple, {"bitrate »: 10646968, « duration »: 1050683, « height »: 720, « width »: 1280, « audioBitsPerSample »: 16, « audioChannels »: 1, « audioFormat »: « PCM », « audioSamplesPerSecond »: 32000, « fourCC »: « H264 », « frameRate »: 60} |
|`m365_webdavurl` |String | URL compatible WebDAV pour l’élément. |
|`m365_weburl` |Chaîne |URL qui affiche la ressource dans le navigateur. En lecture seule. |
