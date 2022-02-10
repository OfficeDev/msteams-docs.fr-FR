---
title: Intégrer Sélecteur de personnes
author: Rajeshwari-v
description: Utilisation du SDK Teams client JavaScript pour intégrer le contrôle S picker de personnes
keywords: contrôle du s picker de personnes
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: surbhigupta
ms.openlocfilehash: 7a7a229bdeab7d83f71f8dbe3b24da8b44b3db32
ms.sourcegitcommit: 90587b1ec04bf20d716ed6feb8ccca4313e87f8c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/10/2022
ms.locfileid: "62518141"
---
# <a name="integrate-people-picker"></a>Intégrer Sélecteur de personnes  

Le sélecateur de personnes est un contrôle pour rechercher et sélectionner des personnes. Il s’agit d’une fonctionnalité native disponible sur Teams plateforme. Vous pouvez intégrer Teams contrôle d’entrée natif du s picker de personnes à vos applications web. Vous pouvez choisir entre une sélection unique ou une sélection multiple, et des configurations, telles que la limitation de la recherche au sein d’une conversation, de canaux ou de l’ensemble de l’organisation.

Vous pouvez utiliser [Microsoft Teams SDK client JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), `selectPeople` qui fournit l’API pour intégrer le s picker de personnes dans votre application web. 

## <a name="advantages-of-integrating-the-native-people-picker"></a>Avantages de l’intégration du s picker de personnes natif 

* Le contrôle S picker de personnes fonctionne sur toutes les surfaces Teams, telles que le module de tâche, une conversation, un canal, un onglet de réunion et une application personnelle.
* Ce contrôle vous permet de rechercher et de sélectionner des utilisateurs au sein d’une conversation, d’un canal ou de l’ensemble de l’organisation.
* Le sélecteur de personnes vous aide dans les scénarios impliquant l’affectation de tâches, le marquage et l’informer d’un utilisateur. 
* Vous pouvez utiliser ce contrôle facilement disponible dans votre application web. Cela permet d’économiser considérablement l’effort et le temps nécessaires pour créer un tel contrôle vous-même.

Vous devez appeler l’API `selectPeople` pour intégrer le contrôle S picker de personnes dans Teams application. Pour une intégration efficace, vous devez comprendre l’extrait de [code](#code-snippet) pour appeler l’API. Il est important de vous familiariser avec les erreurs de [réponse d’API](#error-handling) pour gérer les erreurs dans votre application web.

> [!NOTE] 
> Actuellement, Microsoft Teams prise en charge du s picker de personnes est disponible uniquement pour les clients mobiles.

## <a name="selectpeople-api"></a>`selectPeople` API 

`selectPeople`L’API vous permet d’ajouter Teams natifs `People Picker input control` à vos applications web.  
La description de l’API est la suivante :

| API      | Description  |
| --- | --- |
|**selectPeople**|Lance un sélecateur de personnes et permet à l’utilisateur de rechercher et de sélectionner une ou plusieurs personnes dans la liste.<br/><br/>Cette API renvoie l’ID, le nom et l’adresse e-mail des utilisateurs sélectionnés à l’application web d’appel.<br/><br/>Dans le cas d’une application personnelle, le contrôle recherche dans l’organisation. Si l’application est ajoutée à une conversation ou un canal, le contexte de recherche est configuré en fonction du scénario. La recherche est limitée au sein des membres de cette conversation, canal ou mis à disposition au sein de l’organisation.|

L’API `selectPeople` est livré avec les configurations d’entrée suivantes :

|Paramètre de configuration|Type|Description| Valeur par défaut|
|-----|------|--------------|------|
|`title`| Chaîne| Il s’agit d’un paramètre facultatif. Il définit le titre du contrôle S sélectionneur de personnes. | Sélectionner des personnes|
|`setSelected`|Chaîne| Il s’agit d’un paramètre facultatif. Vous devez transmettre Microsoft Azure Active Directory (Azure AD) des personnes à pré-sélectionné. Ce paramètre présélectionne les personnes lors du lancement du contrôle Sélectionneur de personnes. En cas de sélection unique, seul le premier utilisateur valide est pré-préruplé en ignorant les autres. |Null| 
|`openOrgWideSearchInChatOrChannel`|Boolean | Il s’agit d’un paramètre facultatif. Lorsqu’elle est définie sur True, elle lance le sérial de personnes dans l’étendue de l’organisation, même si l’application est ajoutée à une conversation ou un canal. |Faux|
|`singleSelect`|Boolean|Il s’agit d’un paramètre facultatif. Lorsqu’elle est définie sur True, elle lance le s sélectionneur de personnes en limitant la sélection à un seul utilisateur. |Faux|

L’image suivante illustre l’expérience du s picker de personnes dans un exemple d’application web :

![Expérience d’application web du s picker de personnes](../../assets/images/tabs/people-picker-control-capability.png)

### <a name="code-snippet"></a>Extrait de code

**Appel `selectPeople` API permettant** de sélectionner des personnes dans une liste :

```javascript
 microsoftTeams.people.selectPeople((error: microsoftTeams.SdkError, people: microsoftTeams.people.PeoplePickerResult[]) => 
 {
    if (error) 
    {
        if (error.message) 
           {
             alert(" ErrorCode: " + error.errorCode + error.message);
           }
            else 
            {
              alert(" ErrorCode: " + error.errorCode);
            }
      }
    if (people)
     {
            output(" People length: " + people.length + " " + JSON.stringify(people));
      }
  });
```

## <a name="error-handling"></a>Gestion des erreurs

Vous devez veiller à gérer correctement les erreurs dans votre application web. Le tableau suivant répertorie les codes d’erreur et les conditions dans lesquelles les erreurs sont générées : 

|Code d'erreur |  Nom de l’erreur     | Condition|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | L’API n’est pas prise en charge sur la plateforme actuelle.|
| **500** | INTERNAL_ERROR | Une erreur interne s’est produite lors du lancement du s picker de personnes.|
| **4000** | INVALID_ARGUMENTS | L’API est invoquée avec des arguments obligatoires erronés ou insuffisants.|
| **8000** | USER_ABORT |L’utilisateur a annulé l’opération.|
| **9000** | OLD_PLATFORM | L’utilisateur se trouve sur une ancienne build de plateforme où l’implémentation de l’API n’est pas présente.  La mise à niveau de la build résout le problème.|

## <a name="see-also"></a>Voir aussi

* [Intégrer des fonctionnalités multimédias dans Teams](mobile-camera-image-permissions.md)
* [Intégrer le code QR ou la fonctionnalité de scanneur de code-barres dans Teams](qr-barcode-scanner-capability.md)
* [Intégrer des fonctionnalités d’emplacement dans Teams](location-capability.md)
