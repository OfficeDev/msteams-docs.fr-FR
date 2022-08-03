---
title: API web de tables virtuelles
author: surbhigupta
description: Dans ce module, découvrez l’api web Tables virtuelles pour l’application de contrôle Collaboration, le tri de tables virtuelles et le filtrage dans Microsoft Teams.
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: 31784cfabccdfa861044e74be533c00f134ea851
ms.sourcegitcommit: 0bb822b30739e4a532a36764dad2dbf35a81ba29
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2022
ms.locfileid: "67179094"
---
# <a name="virtual-tables-web-api"></a>API web de tables virtuelles

Lorsque vous utilisez l’API Web Dataverse pour récupérer plusieurs enregistrements à partir d’une table virtuelle, des paramètres de requête supplémentaires peuvent être inclus pour prendre en charge le tri, le filtrage et la pagination. Ces fonctionnalités ne sont pas prises en charge uniformément dans les tables virtuelles de contrôles collaboration, car elles s’appuient sur la prise en charge fournie par microsoft API Graph. Pour plus d’informations sur ce que chaque table virtuelle prend en charge, consultez la référence d’entité tables virtuelles.

> [!NOTE]
> Actuellement, les contrôles collaboration sont disponibles uniquement en [préversion publique des développeurs](~/resources/dev-preview/developer-preview-intro.md).

## <a name="virtual-table-sorting"></a>Tri de tables virtuelles

Avec les tables virtuelles, vous pouvez utiliser le paramètre de requête OData $orderby pour définir des critères de tri du jeu de résultats. Utilisez le suffixe asc ou desc pour spécifier respectivement l’ordre croissant ou décroissant. La valeur par défaut est croissant si le suffixe n’est pas appliqué.  

**Tables prises en charge** : chaque table virtuelle prend en charge la même fonctionnalité de tri que sa ressource Graph respective. Les tables virtuelles qui prennent en charge le tri sont les suivantes :  

* Élément de lecteur Graph
* Événement Graph

> [!NOTE]
> Le tri n’est pas pris en charge sur tous les attributs des ressources Graph respectives. Si un utilisateur tente de trier sur une table virtuelle avec un attribut non pris en charge, ce jeu de résultats a son ordre par défaut. Il s’agit du même comportement que l’API web Dataverse sur les colonnes qui ne prennent pas en charge le tri.

Exemples :

* GET [URI de l’organisation]/api/data/v9.2/m365_graphdriveitems?$filter=m365_collaborationrootid eq '00000000-0000-0000-00 &$orderby 0000000000000000000000000=m365_name desc
* GET [URI d’organisation]/api/data/v9.2/m365_graphevents?$filter=m365_groupid eq '00000000-0000-0000-0000-00000000000000000000'$orderby=m365_subject asc

## <a name="virtual-table-filtering"></a>Filtrage de table virtuelle

Avec les tables virtuelles, vous pouvez utiliser le paramètre de requête OData $filter pour définir les critères pour lesquels les lignes seront retournées. Les tables virtuelles sont interrogées à l’aide des mêmes opérateurs OData que ceux pris en charge par l’API Web Dataverse.

* **Opérateurs de comparaison**

  |Opérateur|Description|Exemple|
  |----|----|----|
  |eq|Égal|$filter=m365_name eq 'Contoso'|
  |ne|Non égal à|$filter=m365_name ne 'Contoso'|
  |gt|Supérieur à|$filter=m365_price gt 50.0|
  |ge|Supérieur ou égal à|$filter=m365_price ge 50.0|
  |lt|Inférieur à|$filter=m365_price lt 50.0|
  |le|Inférieur ou égal à|$filter=m365_price le 50.0|

* **Opérateurs logiques**

  |Opérateur|Description|Exemple|
  |----|----|----|
  |et|AND logique |$filter=m365_name eq 'Contoso' et m365_price eq 50.0|
  |ou|OR logique |$filter=m365_name ne 'Contoso' ou m365_price eq 50.0|
  |
not|Négociation logique |$filter=not contains(m365_name,'Contoso')|

* **Opérateurs de regroupement**

  |Opérateur|Description|Exemple|
  |----|----|----|
  |( )|Regroupement des priorités |$filter=(m365_name eq 'Contoso' et m365_price eq 50.0) ou contains(m365_subject,'Team Sync')|

* **Fonctions de requête**

  |Fonction |Exemple |
  |----|----|
  |contains|$filter=contains(m365_name,'Contoso')|
  |endswith|$filter=endswith(m365_name,'Contoso')|
  |startswith|$filter=startswith(m365_name,'Contoso')|

**Tables prises en charge** : chaque table virtuelle prend en charge les mêmes fonctionnalités de filtrage que sa ressource Graph respective. Les tables virtuelles qui prennent en charge le filtrage sont les suivantes :

* Rendez-vous de réservation Graph
* Élément de lecteur Graph
* Événement Graph

> [!Note]
> Le filtrage n’est pas pris en charge sur tous les attributs des ressources Graph respectives. Si un utilisateur tente de filtrer sur une table virtuelle avec un attribut non pris en charge, ce filtre est ignoré. Il s’agit du même comportement que l’API web Dataverse sur les colonnes qui ne prennent pas en charge le filtrage.

Exemples :

* GET [URI d’organisation]/api/data/v9.2/m365_graphbookingappointments?$filter=m365_bookingbusinessid eq 'ContosoBank@Contoso.onmicrosoft.com' et m365_price eq 100.0
* GET [URI d’organisation]/api/data/v9.2/m365_graphdriveitems?$filter=m365_collaborationrootid eq '00000000-0000-0000-0000-0000000000000' et m365_name eq 'Meeting Notes.docx'
* GET [URI d’organisation]/api/data/v9.2/m365_graphevents?$filter=m365_groupid eq '00000000-0000-0000-0000-0000000000000' et m365_subject eq 'Monthly Sync'

## <a name="virtual-table-pagination"></a>Pagination de table virtuelle

La pagination est une ressource utile pour extraire un grand ensemble d’enregistrements. La pagination de table virtuelle peut être obtenue de trois manières différentes.

Vous pouvez spécifier la taille de la page à l’aide de la `odata.maxpagesize` valeur de préférence dans l’en-tête de requête. Si le jeu de résultats s’étend sur plusieurs pages, la réponse inclut la `@odata.nextLink` propriété. Les exemples de demande et de réponse sont les suivants :

# <a name="request"></a>[Demande](#tab/request)

```http
  GET [Organization URI]/api/data/v9.2/m365_graphdriveitems 
  Accept: application/json 
  Prefer: odata.maxpagesize=2 
```

# <a name="response"></a>[Réponse](#tab/response)

```json
{ 

  "@odata.context": "[Organization URI]/api/data/v9.0/$metadata#m365_graphdriveitems", 
  "value": [ 
   { 
      "@odata.etag": "W/\"{FA93AF7C-1F45-4714-85A5-BB95EB86E1E5}\"", 
      "m365_name": "Review.doc", 
      "m365_graphdriveitemid": "f50aae23-6644-3d35-66d7-e3c5a979dad3", 
      …
      },
      {
      "@odata.etag": "W/\"{3938D549-1AEF-46A5-BF3C-38472AD934C2}\"", 
      "m365_name": "Review.doc", 
      "m365_graphdriveitemid": "3d59a7e2-ec83-d0b3-270e-8ad676622027", 
      … 
      } 
      ],
      "@odata.nextLink": "[Organization URI]/api/data/v9.0/m365_graphdriveitems &$skiptoken=%3Ccookie%20pagenumber=%222%22%20pagingcookie=%22UGFnZWQ9VFJVRSZwX1NvcnRCZWhhdmlvcj0xJnBfRmlsZUxlYWZSZWY9dGVzdCZwX0lEPTI5%22%20istracking=%22False%22%20/%3E" 
} 
```

---

Actuellement, les tables virtuelles suivantes prennent en charge la `odata.maxpagesize` préférence :

* Rendez-vous de réservation Graph
* Graph Calendar Event
* Lecteur Graph
* Élément de lecteur Graph

Vous pouvez spécifier le nombre d’enregistrements à retourner en passant l’option `$top` dans l’URL. Si vous devez également spécifier le numéro de page, vous pouvez le faire en passant un cookie de pagination sous forme de chaîne encodée XML comme `$skiptoken` option. Pour extraire un numéro de page spécifique, vous pouvez passer le cookie de pagination au format suivant :

  `<cookie pagenumber=3 />`

# <a name="request"></a>[Demande](#tab/request1)

```http
     GET [Organization URL]/api/data/v9.2/m365_graphevents?$top=2&$skiptoken=<cookie pagenumber='3' /> 
```

# <a name="response"></a>[Réponse](#tab/response1)

```json

{
  "@odata.context": "[Organization URI]/api/data/v9.0/$metadata#m365_graphevents", 
  "value": [
   { 
      "@odata.etag": "W/\"{FA93AF7C-1F45-4714-85A5-BB95EB86E1E5}\"", 
      "m365_graphdeventid": "3d59a7e2-ec83-d0b3-270e-8ad676622027", 
      "m365_subject": "Important meeting", 
      …
    }, 
    {
      "@odata.etag": "W/\"{3938D549-1AEF-46A5-BF3C-38472AD934C2}\"", 
      "m365_graphdeventid": "f50aae23-6644-3d35-66d7-e3c5a979dad3", 
      "m365_subject": "Another important meeting", 
      …
    } 
  ] 
}

```

---

> [!Note]
> La réponse n’inclut pas la `@nextLink` propriété. Si votre cas d’utilisation nécessite le retour du lien de page suivant, vous pouvez utiliser l’en-tête de préférence odata.maxpagesize décrit à la section 1 au lieu de transmettre le paramètre d’URI $top.

Actuellement, les tables virtuelles suivantes prennent en charge l’extraction d’une page spécifique :

* Rendez-vous de réservation Graph
* Graph Calendar Event

Vous pouvez passer un code XML d’extraction en tant que chaîne encodée en XML. Avec l’option fetch XML, vous pouvez spécifier plusieurs préférences de requête. Les options spécifiques à la pagination sont page (numéro de page) et count (taille de page). Le code XML suivant spécifie le numéro de page et la taille :

  `<fetch version="1.0" mapping="logical" returntotalrecordcount="true" page="<Page Number>" count="<Page Size>"></fetch>`

# <a name="request"></a>[Demande](#tab/request2)

```http
GET [Organization URL]/api/data/v9.2/m365_graphevents?$fetchXml=<fetch version="1.0" mapping="logical" returntotalrecordcount="true" page="3" count="2"></fetch> 

```

# <a name="response"></a>[Réponse](#tab/response2)

```json
{ 

    "@odata.context": "[Organization URI]/api/data/v9.0/$metadata#m365_graphdevents", 
    "@Microsoft.Dynamics.CRM.fetchxmlpagingcookie": "<cookie pagenumber=\"3\" pagingcookie=\"\" istracking=\"False\" />", 
    "value": [ 
        { 
            "@odata.etag": "W/\"{FA93AF7C-1F45-4714-85A5-BB95EB86E1E5}\"", 
            "m365_graphdeventid": "3d59a7e2-ec83-d0b3-270e-8ad676622027", 
            "m365_subject": "Important meeting", 
            …
        }, 
        { 
            "@odata.etag": "W/\"{3938D549-1AEF-46A5-BF3C-38472AD934C2}\"", 
            "m365_graphdeventid": "f50aae23-6644-3d35-66d7-e3c5a979dad3", 
            "m365_subject": "Another important meeting", 
            …
        } 
    ] 
} 

```

---

Les tables virtuelles suivantes prennent en charge la propriété count à passer dans le cadre de l’option fetchXml :

* Lecteur Graph
* Élément de lecteur Graph

Les tables virtuelles suivantes prennent en charge la propriété de page dans le cadre de l’option fetchXml :

* Rendez-vous de réservation Graph
* Graph Calendar Event
