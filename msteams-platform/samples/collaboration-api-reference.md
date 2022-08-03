---
title: Références de l’API REST contrôle et paramètres de collaboration
author: surbhigupta
description: Dans ce module, découvrez la référence de l’API REST de contrôle et de paramètres de collaboration pour gérer les paramètres, démarrer, mapper et récupérer des activités de collaboration.
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: bc0a5e6834077e199c1dff26568ef2acfeb72745
ms.sourcegitcommit: 0bb822b30739e4a532a36764dad2dbf35a81ba29
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2022
ms.locfileid: "67178979"
---
# <a name="collaboration-control-and-settings-rest-api-reference"></a>Informations de référence sur le contrôle de collaboration et les paramètres de l’API REST

Les développeurs peuvent utiliser le contrôle collaboration et l’API REST Paramètres pour gérer les paramètres, démarrer, mapper et récupérer des activités de collaboration avec leurs propres entités de modèle d’entreprise.

> [!NOTE]
> Actuellement, les contrôles collaboration sont disponibles uniquement en [préversion publique des développeurs](~/resources/dev-preview/developer-preview-intro.md).

Cet article fournit des informations de référence sur l’API REST de la solution de contrôle collaboration.

## <a name="rest-operations-collaboration---custom-api"></a>Opérations REST : Collaboration - API personnalisée

|Opération|Description|
|---------|-----------|
|[Associer une carte de collaboration](/rest/api/industry/collaboration-toolkit/collaboration-custom-ap-is/associate-collaboration-map)|Associe une entité collaborative à une session de collaboration.|
|[Commencer la session de collaboration](/rest/api/industry/collaboration-toolkit/collaboration-custom-ap-is/begin-collaboration-session)|Crée un enregistrement de session de collaboration lié à une entité métier, au contexte d’application et aux métadonnées facultatives.|
|[Dissocier la carte de collaboration](/rest/api/industry/collaboration-toolkit/collaboration-custom-ap-is/disassociate-collaboration-map-custom-api)|Dissocie une entité mappée de la session de collaboration donnée.|
|[Récupérer des cartes de collaboration](/rest/api/industry/collaboration-toolkit/collaboration-custom-ap-is/retrieve-collaboration-maps-custom-api)|Obtient la liste des mappages de collaboration pour une session d’un type d’entité spécifique.|
|[Récupérer une session de collaboration](/rest/api/industry/collaboration-toolkit/collaboration-custom-ap-is/retrieve-collaboration-session-custom-api)|Obtient un enregistrement de session de collaboration en fonction des paramètres fournis.|
|[Mettre à jour la carte de collaboration](/rest/api/industry/collaboration-toolkit/collaboration-custom-ap-is/update-collaboration-map-custom-api)|Mises à jour un enregistrement de carte de collaboration et ses métadonnées s’ils sont fournis.|
|[Mettre à jour la session de collaboration](/rest/api/industry/collaboration-toolkit/collaboration-custom-ap-is/update-collaboration-session)|Mises à jour un enregistrement de session de collaboration et éventuellement ses métadonnées.|

## <a name="rest-operations-collaboration---standard-odata-apis"></a>Opérations REST : Collaboration - API OData standard

|Opération|Description|
|---------|-----------|
|[Obtenir la carte de collaboration par ID](/rest/api/industry/collaboration-toolkit/collaboration-standard-o-data-ap-is/get-collaboration-map-by-id)|Obtient les détails d’un enregistrement de carte de collaboration.|
|[Obtenir les métadonnées de collaboration](/rest/api/industry/collaboration-toolkit/collaboration-standard-o-data-ap-is/get-collaboration-metadata)|Obtient la liste des enregistrements de métadonnées de collaboration pour une carte de collaboration donnée ou un nom d’entité racine de collaboration.|
|[Obtenir la racine de la collaboration](/rest/api/industry/collaboration-toolkit/collaboration-standard-o-data-ap-is/get-collaboration-root)|Répertorie toutes les sessions de collaboration créées.|

## <a name="rest-operations-settings---custom-apis"></a>Opérations REST : Paramètres - API personnalisées

|Opération|Description|
|---------|-----------|
|[Créer et mettre à jour les paramètres](/rest/api/industry/collaboration-toolkit/settings-custom-ap-is/create-update-setting-custom-api)|Crée ou met à jour un paramètre qui correspond à la fois au chemin d’accès du groupe et au nom de définition des paramètres.|
|[Récupérer les paramètres Null](/rest/api/industry/collaboration-toolkit/settings-custom-ap-is/retrieve-null-settings-custom-api)|Retourne une liste de définitions de paramètres qui n’ont pas de valeur.|
|[Récupérer les paramètres](/rest/api/industry/collaboration-toolkit/settings-custom-ap-is/retrieve-settings-custom-api)|Retourne une liste de paramètres ou de paramètres spécifiques dans des groupes.|

## <a name="rest-operations-settings---standard-odata-apis"></a>Opérations REST : paramètres - API OData standard

|Opération|Description|
|---------|-----------|
|[Supprimer la définition des paramètres](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/delete-settings-definition)|Supprime une définition de paramètres.|
|[Supprimer un groupe de paramètres](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/delete-settings-group)|Supprime un groupe de paramètres.|
|[Supprimer le type de paramètres](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/delete-settings-type)|Supprimez un type de paramètres.|
|[Supprimer la valeur des paramètres](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/delete-settings-value)|Supprime une valeur de paramètres.|
|[Obtenir les définitions de paramètres](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/get-settings-definitions)|Répertorie les définitions de paramètres.|
|[Obtenir les groupes de paramètres](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/get-settings-groups)|Répertorie les groupes de paramètres.|
|[Obtenir les types de paramètres](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/get-settings-types)|Répertorie les types de paramètres.|
|[Obtenir la valeur des paramètres](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/get-settings-value)|Répertorie les valeurs des paramètres.|
|[Définition des paramètres de correctif](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/patch-settings-definition)|Mises à jour une définition de paramètres.|
|[Groupe Paramètres des correctifs](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/patch-settings-group)|Mises à jour un groupe de paramètres.|
|[Type de paramètres de correctif](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/patch-settings-type)|Mises à jour un type de paramètres.|
|[Valeur des paramètres du correctif](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/patch-settings-value)|Mises à jour une valeur de paramètre.|
|[Définition des paramètres post](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/post-settings-definition)|Crée une définition de paramètres.|
|[Publier un groupe de paramètres](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/post-settings-group)|Crée un groupe de paramètres.|
|[Type de paramètres post](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/post-settings-type)|Crée un nouveau type de paramètres.|
|[Post Settings Value](/rest/api/industry/collaboration-toolkit/settings-standard-o-data-ap-is/post-settings-value)|Crée une valeur de paramètre.|
