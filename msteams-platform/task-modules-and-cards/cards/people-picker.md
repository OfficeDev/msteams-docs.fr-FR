---
title: Sélectionneur de personnes dans les Cartes adaptatives
description: Décrit comment utiliser le contrôle S sélectionneur de personnes dans les cartes adaptatives
localization_priority: Normal
keywords: Socheur de personnes de cartes adaptatives
ms.topic: reference
author: Rajeshwari-v
ms.author: surbhigupta
ms.openlocfilehash: 449c3d764cf3e4db68207560890e954bef14c7b4
ms.sourcegitcommit: 90587b1ec04bf20d716ed6feb8ccca4313e87f8c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/10/2022
ms.locfileid: "62518302"
---
# <a name="people-picker-in-adaptive-cards"></a>Sélectionneur de personnes dans les Cartes adaptatives

>[!NOTE]
> Actuellement, le s picker de personnes dans les cartes [](../../resources/dev-preview/developer-preview-intro.md#public-developer-preview-for-microsoft-teams) adaptatives est disponible en prévisualisation publique pour les développeurs uniquement pour les appareils mobiles et généralement disponible (GA) pour les ordinateurs de bureau.

Le sélecateur de personnes permet aux utilisateurs de rechercher et de sélectionner des utilisateurs dans la carte adaptative. Vous pouvez ajouter le s sélectionneur de personnes en tant que contrôle d’entrée à la carte adaptative, qui fonctionne sur les conversations, les canaux, les modules de tâche et les onglets. Le s picker de personnes prend en charge les fonctionnalités suivantes :        

* Recherche un ou plusieurs utilisateurs.
* Sélectionne un ou plusieurs utilisateurs. 
* Réaffecte à un ou plusieurs utilisateurs. 
* Pré-prérupule le nom des utilisateurs sélectionnés.

## <a name="popular-scenarios"></a>Scénarios populaires 

Le tableau suivant fournit les scénarios les plus populaires pour le s picker de personnes dans les cartes adaptatives et les actions correspondantes :

|Scénarios|Actions|
|----------|-------------------------|
|Scénarios basés sur l’approbation| Pour demander, affecter et réaffecter l’approbation à l’utilisateur prévu en fonction de l’exigence.|
|Gestion des incidents| Pour suivre les incidents et avertir, affecter et réaffecter à l’utilisateur prévu pour une action immédiate.| 
|Gestion de projet| Pour attribuer des tickets ou des bogues à des utilisateurs particuliers.|
|Recherche d’utilisateur| Pour rechercher des utilisateurs au sein de l’organisation.|

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

Le client web et de bureau prend en charge le s sélectionneur de personnes dans la carte adaptative. Lors de la recherche sur le web, le sériateur de personnes implique une expérience de saisie inline.

### <a name="reassignment-scenario-example"></a>Exemple de scénario de réaffectation

L’utilisateur A (Robert) reçoit un ticket pour une tâche dans un canal et réalise une affectation incorrecte. L’utilisateur A réaffecte la tâche qui renvoie les informations au bot. 

**Pour réaffecter une tâche**

1. **Sélectionnez Réaffecter l’endroit** où le champ du sélecateur de personnes est préresigné avec le nom pour réaffecter la tâche à l’utilisateur prévu.
1. Supprimez le nom de l’utilisateur incorrect. 
1. Sélectionnez les utilisateurs prévus selon le scénario d’image, l’utilisateur B (Mona) et l’utilisateur C (Robin) pour la tâche. 
1. Sélectionnez **Affecter**. Après l’affectation, les informations sont envoyées au bot. 
   Le bot met à jour la carte adaptative et avertit les utilisateurs prévus. 
 
L’image suivante illustre le scénario de réaffectation :    

![S sélectionneur de personnes sur le Bureau](../../assets/images/cards/desktoppp.gif)

# <a name="mobile"></a>[Mobile](#tab/mobile)

> [!NOTE]
> Actuellement, cette fonctionnalité est disponible en prévisualisation [pour les développeurs publics](../../resources/dev-preview/developer-preview-intro.md#public-developer-preview-for-microsoft-teams) uniquement.

Les clients mobiles Android et iOS prend en charge le s picker de personnes dans les cartes adaptatives. Vous pouvez utiliser le sélecateur de personnes dans un appareil mobile pour rechercher et sélectionner un utilisateur afin d’améliorer l’expérience utilisateur. L’expérience de recherche est similaire à toute autre expérience de sélection d’utilisateur sur mobile.

### <a name="reassignment-scenario-example"></a>Exemple de scénario de réaffectation

L’utilisateur A (Robert) reçoit un ticket pour une tâche dans un canal et réalise une affectation incorrecte. L’utilisateur A réaffecte la tâche qui renvoie les informations au bot. 

**Pour réaffecter une tâche**

1. **Sélectionnez Réaffecter l’endroit** où le champ du sélecateur de personnes est préresigné avec le nom pour réaffecter la tâche à l’utilisateur prévu.
1. Supprimez le nom de l’utilisateur incorrect.
1. Sélectionnez les utilisateurs prévus selon le scénario d’image, l’utilisateur B (Mona) et l’utilisateur C (Robin) pour la tâche.
1. Sélectionnez **Terminé**.
1. Sélectionnez **Affecter**. Après l’affectation, les informations sont envoyées au bot. 
   Le bot met à jour la carte adaptative et avertit les utilisateurs prévus. 

L’image suivante illustre le scénario de réaffectation : 

![S picker de personnes sur mobile](../../assets/images/cards/mobilepp.gif)

---

## <a name="implement-people-picker"></a>Implémenter le s picker de personnes

Le s picker de personnes est implémenté en tant qu’extension du [contrôle Input.ChoiceSet](https://adaptivecards.io/explorer/Input.ChoiceSet.html) . Le contrôle d’entrée inclut les sélections suivantes :   

* Dropdown, par exemple une sélection étendue.
* Bouton d’radio, tel qu’une sélection unique.
* Cases à cocher, telles que plusieurs sélections.  

> [!NOTE]
> Le `Input.ChoiceSet` contrôle est basé sur les propriétés `style` et les `isMultiSelect` propriétés.  

### <a name="update-schema"></a>Mettre à jour un schéma

Les propriétés suivantes sont des ajouts au `Input.ChoiceSet` schéma afin d’activer l’expérience du s picker de personnes sur la carte :  

#### <a name="inputchoiceset-control"></a>Contrôle Input.ChoiceSet

|Propriété |Type |Requis |Description |
|----|----|----|----|
|**choices.data** |**Data.Query** |Non |Active la mise à niveau automatique dynamique pour différents types d’utilisateurs, en extraire les résultats à partir du jeu de données spécifié. |

#### <a name="dataquery"></a>Data.Query

|Propriété |Type |Requis |Description|
|--|--|--|--|
|**dataset** |String |Oui |Type de données à extraire dynamiquement.|   

#### <a name="dataset"></a>dataset
Le tableau suivant fournit des valeurs prédéfines en tant que **jeu de données** pour le s picker de personnes :   

|dataset|Étendue de recherche
|--|--|
|**graph.microsoft.com/users** |Effectuer une recherche dans tous les membres de l’organisation.|
|**graph.microsoft.com/users?scope=currentContext** |Recherchez dans les membres de la conversation en cours, par exemple la conversation ou le canal dans lequel la carte particulière est envoyée.|        

### <a name="example"></a>Exemple
L’exemple de code pour la création du s picker de personnes avec la recherche dans l’organisation est le suivant :

```json 
{
    "type": "AdaptiveCard",
    "body": [
        {
            "type": "TextBlock",
            "size": "Medium",
            "weight": "Bolder",
            "text": "People Picker with Org search enabled"
        },
        {
            "type": "Input.ChoiceSet",
            "choices": [],
            "choices.data": {
                "type": "Data.Query",
                "dataset": "graph.microsoft.com/users"
            },
            "id": "people-picker",
            "isMultiSelect": true
        }
    ],
    "actions": [
        {
            "type": "Action.Submit",
            "title": "Submit"
        }
    ],
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.2"
}
```  

L’image suivante illustre le s sélectionneur de personnes dans les cartes adaptatives avec la recherche de l’organisation :

![Recherche dans l’organisation du s picker de personnes](../../assets/images/cards/peoplepicker-org-search.png)

Pour activer la recherche dans une liste de membres de conversation, utilisez le jeu de données approprié défini dans la table [de jeux de](#dataset) données. `isMultiSelect` permet d’activer la sélection de plusieurs utilisateurs dans le contrôle. Elle est définie sur False par défaut et ce paramètre vous permet de sélectionner un seul utilisateur.

### <a name="data-submission"></a>Soumission de données

Vous pouvez utiliser ou `Action.Submit` envoyer `Action.Execute` des données sélectionnées à votre bot. La `invoke` charge utile reçue sur votre bot est une liste d’ID Microsoft Azure Active Directory (Azure AD) ou des ID fournis dans la liste statique.
Dans le sélecateur de personnes, lorsqu’un utilisateur est sélectionné dans le contrôle, `Microsoft Azure Active Directory (Azure AD) ID` il s’agit de la valeur renvoyée. Il `Microsoft Azure Active Directory (Azure AD) ID` s’agit d’une chaîne qui identifie de manière unique un utilisateur dans l’annuaire.

Le format de la valeur envoyée au bot dépend de la valeur de la `isMultiSelect` propriété :

|valeur de `isMultiSelect`|Format|
|--|--|
|false _(sélection unique)_|<selected_Azure_AD_ID>|
|true _(sélection multiple)_|<selected_Azure_AD_ID_1>,<selected_Azure_AD_ID_2>,<selected_Azure_AD_ID_3>|  

Avec le `Azure AD ID`sélectionneur de personnes, l’utilisateur correspondant est sélectionné au préalable. 

## <a name="preselection-of-user"></a>Préselection de l’utilisateur

Le sélecateur de personnes prend en charge la pré-sélection de l’utilisateur dans le contrôle, lors de la création et de l’envoi d’une carte adaptative. `Input.ChoiceSet` prend en charge `value` la propriété utilisée pour présélectionner un utilisateur. Le format de cette propriété `value` est identique au format de valeur soumise dans [l’envoi de données](#data-submission).  
La liste suivante fournit les informations pour présélectionner les utilisateurs :

* Pour un utilisateur unique dans le contrôle, spécifiez l’utilisateur `Microsoft Azure Active Directory (Azure AD) ID` en tant que `value`. 
* Pour plusieurs utilisateurs, par exemple `isMultiSelect` `true`, spécifiez une chaîne de s séparées par des virgules `Microsoft Azure Active Directory (Azure AD) ID`.  

L’exemple suivant décrit la pré-sélection d’un utilisateur unique :

```json
{
    "type": "AdaptiveCard",
    "body": [
        {
            "type": "TextBlock",
            "size": "Medium",
            "weight": "Bolder",
            "text": "People Picker with Org search enabled"
        },
        {
            "type": "Input.ChoiceSet",
            "choices": [],
            "choices.data": {
                "type": "Data.Query",
                "dataset": "graph.microsoft.com/users"
            },
            "id": "people-picker",
            "value": "<Azure AD ID 1>"
        }
    ],
    "actions": [
        {
            "type": "Action.Submit",
            "title": "Submit"
        }
    ],
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.2"
}
```  

L’exemple suivant décrit la pré-sélection de plusieurs utilisateurs :

```json
{
    "type": "AdaptiveCard",
    "body": [
        {
            "type": "TextBlock",
            "size": "Medium",
            "weight": "Bolder",
            "text": "People Picker with Org search enabled"
        },
        {
            "type": "Input.ChoiceSet",
            "choices": [],
            "choices.data": {
                "type": "Data.Query",
                "dataset": "graph.microsoft.com/users"
            },
            "id": "people-picker",
            "isMultiSelect": true,
            "value": "<Azure AD ID 1>,<Azure AD ID 2>,<Azure AD ID 3>"
        }
    ],
    "actions": [
        {
            "type": "Action.Submit",
            "title": "Submit"
        }
    ],
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.2"
}
```
 
## <a name="static-choices"></a>Choix statiques

Les choix statiques sont pris en charge dans les scénarios où les profils personnalisés doivent être insérés dans les jeux de données prédéfinits. `Input.ChoiceSet` prend en charge la `choices` spécification statique dans le json. Le choix statique est utilisé pour créer les choix que l’utilisateur peut sélectionner.

> [!NOTE]
> Les `choices` données statiques sont utilisées avec des jeux de données dynamiques. 

Le choix se compose de `title` et `value`. Lorsqu’ils sont utilisés avec le s sélectionneur de personnes, ces choix `title` sont convertis en profils utilisateur qui ont le nom et l’identificateur `value` . Ces profils personnalisés font également partie des résultats de recherche lorsque la requête de recherche correspond à ce qui est donné `title`.    
L’exemple suivant décrit les choix statiques : 

```json
{
    "type": "AdaptiveCard",
    "body": [
        {
            "type": "TextBlock",
            "size": "Medium",
            "weight": "Bolder",
            "text": "People Picker with Org search enabled"
        },
        {
            "type": "Input.ChoiceSet",
            "choices": [
                {
                    "title": "Custom Profile 1",
                    "value": "Profile1"
                },
                {
                    "title": "Custom Profile 2",
                    "value": "Profile2"
                }
            ],
            "choices.data": {
                "type": "Data.Query",
                "dataset": "graph.microsoft.com/users"
            },
            "id": "people-picker",
            "isMultiSelect": true
        }
    ],
    "actions": [
        {
            "type": "Action.Submit",
            "title": "Submit"
        }
    ],
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.2"
}
```

L’image suivante illustre le s sélectionneur de personnes dans les cartes adaptatives avec des choix statiques dans la recherche de l’organisation :

![Choix statique du s picker de personnes](../../assets/images/cards/peoplepicker-static-choice.png)


Vous pouvez implémenter le s sélectionneur de personnes pour une gestion efficace des tâches dans différents scénarios.  

## <a name="see-also"></a>Voir aussi

[Référence des cartes](cards-reference.md)

