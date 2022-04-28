---
title: Sélectionneur de personnes dans les Cartes adaptatives
description: Décrit comment utiliser le contrôle Sélecteur de personnes dans les cartes adaptatives
localization_priority: Medium
keywords: Sélecteur de personnes cartes adaptatives
ms.topic: reference
author: Rajeshwari-v
ms.author: surbhigupta
ms.openlocfilehash: 3d6305895239ca2b8a0c871e53723979feb3f890
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111632"
---
# <a name="people-picker-in-adaptive-cards"></a>Sélectionneur de personnes dans les Cartes adaptatives

>[!NOTE]
> Actuellement, le sélecteur de personnes dans les cartes adaptatives est disponible en [préversion publique des développeurs](../../resources/dev-preview/developer-preview-intro.md#public-developer-preview-for-microsoft-teams) uniquement pour les appareils mobiles et en disponibilité générale (GA) pour le bureau.

Le sélecteur de personnes permet aux utilisateurs de rechercher et de sélectionner des utilisateurs dans la carte adaptative. Vous pouvez ajouter le sélecteur de personnes en tant que contrôle d’entrée à la carte adaptative, qui fonctionne entre les conversations, les canaux, les modules de tâches et les onglets. People Picker prend en charge les fonctionnalités suivantes :

* Recherche un ou plusieurs utilisateurs.
* Sélectionne un ou plusieurs utilisateurs.
* Réattribue à un ou plusieurs utilisateurs.
* Préremplit le nom des utilisateurs sélectionnés.

## <a name="popular-scenarios"></a>Scénarios courants

Le tableau suivant fournit des scénarios populaires pour le sélecteur de personnes dans les cartes adaptatives et les actions correspondantes :

|Scénarios|Actions|
|----------|-------------------------|
|Scénarios basés sur l’approbation| Pour demander, affecter et réattribuer l’approbation à l’utilisateur prévu en fonction de l’exigence.|
|Gestion des incidents| Pour suivre les incidents et notifier, affecter et réattribuer à l’utilisateur prévu pour une action immédiate.|
|Gestion de projet| Pour attribuer des tickets ou des bogues à des utilisateurs particuliers.|
|Recherche d’utilisateur| Pour rechercher des utilisateurs au sein de l’organisation.|

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

Le client web et de bureau prend en charge le sélecteur de personnes dans la carte adaptative. Lors de la recherche sur le web, le sélecteur de personnes implique une expérience de saisie inline.

### <a name="reassignment-scenario-example"></a>Exemple de scénario de réaffectation

L’utilisateur A (Robert) reçoit un ticket pour une tâche dans un canal et réalise un assignateur incorrect. L’utilisateur A réattribue la tâche qui renvoie les informations au bot.

Pour réattribuer une tâche :

1. Sélectionnez **Réaffecter** l’emplacement où le champ sélecteur de personnes est prérempli avec le nom pour réaffecter la tâche à l’utilisateur prévu.
1. Supprimez le nom de l’utilisateur incorrect.
1. Sélectionnez les utilisateurs prévus en fonction du scénario d’image, de l’utilisateur B (Mona) et de l’utilisateur C (Robin) pour la tâche.
1. Sélectionnez **Affecter**. Après l’affectation, les informations sont envoyées au bot.
   Le bot met à jour la carte adaptative et avertit les utilisateurs prévus.

L’image suivante montre le scénario de réaffectation :

![Sélecteur de personnes sur le Bureau](../../assets/images/cards/desktoppp.gif)

# <a name="mobile"></a>[Mobile](#tab/mobile)

> [!NOTE]
> Actuellement, cette fonctionnalité est disponible en [préversion publique des développeurs](../../resources/dev-preview/developer-preview-intro.md#public-developer-preview-for-microsoft-teams) uniquement.

Les clients mobiles Android et iOS prennent en charge le sélecteur de personnes dans les cartes adaptatives. Vous pouvez utiliser le sélecteur de personnes dans le mobile pour rechercher et sélectionner un utilisateur afin d’améliorer l’expérience utilisateur. L’expérience de recherche est similaire à toute autre expérience de sélection d’utilisateur dans le mobile.

### <a name="reassignment-scenario-example"></a>Exemple de scénario de réaffectation

L’utilisateur A (Robert) reçoit un ticket pour une tâche dans un canal et réalise un assignateur incorrect. L’utilisateur A réattribue la tâche qui renvoie les informations au bot.

Pour réattribuer une tâche :

1. Sélectionnez **Réaffecter** l’emplacement où le champ sélecteur de personnes est prérempli avec le nom pour réaffecter la tâche à l’utilisateur prévu.
1. Supprimez le nom de l’utilisateur incorrect.
1. Sélectionnez les utilisateurs prévus en fonction du scénario d’image, de l’utilisateur B (Mona) et de l’utilisateur C (Robin) pour la tâche.
1. Sélectionnez **Terminé**.
1. Sélectionnez **Affecter**. Après l’affectation, les informations sont envoyées au bot.
   Le bot met à jour la carte adaptative et avertit les utilisateurs prévus.

L’image suivante montre le scénario de réaffectation :

![Sélecteur de personnes sur mobile](../../assets/images/cards/mobilepp.gif)

---

## <a name="implement-people-picker"></a>Implémenter le sélecteur de personnes

Le sélecteur de personnes est implémenté en tant qu’extension du contrôle [Input.ChoiceSet](https://adaptivecards.io/explorer/Input.ChoiceSet.html) . Le contrôle d’entrée comprend les sélections suivantes :

* Liste déroulante, telle qu’une sélection développée.
* Case d’option, telle qu’une sélection unique.
* Cases à cocher, telles que plusieurs sélections.  

> [!NOTE]
> Le `Input.ChoiceSet` contrôle est basé sur les propriétés et `isMultiSelect` les `style` propriétés.  

### <a name="update-schema"></a>Mettre à jour un schéma

Les propriétés suivantes sont des ajouts au schéma pour activer l’expérience `Input.ChoiceSet` sélecteur de personnes sur la carte :  

#### <a name="inputchoiceset-control"></a>Contrôle Input.ChoiceSet

|Propriété |Type |Requis |Description |
|----|----|----|----|
|**choices.data** |**Data.Query** |Non |Active la saisie semi-automatique dynamique pour différents types d’utilisateurs, en extrayant les résultats du jeu de données spécifié. |

#### <a name="dataquery"></a>Data.Query

|Propriété |Type |Requis |Description|
|--|--|--|--|
|**Dataset** |Chaîne |Oui |Type de données qui doivent être extraites dynamiquement.|

#### <a name="dataset"></a>Dataset

Le tableau suivant fournit des valeurs prédéfinies en tant que **jeu de données** pour le sélecteur de personnes :

|Dataset|Étendue de recherche
|--|--|
|**graph.microsoft.com/users** |Recherchez tous les membres de l’organisation.|
|**graph.microsoft.com/users?scope=currentContext** |Effectuez une recherche dans les membres de la conversation en cours, comme la conversation ou le canal dans lequel la carte particulière est envoyée.|

### <a name="example"></a>Exemple

L’exemple de code permettant de créer un sélecteur de personnes avec la recherche d’organisation est le suivant :

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

L’image suivante illustre le sélecteur de personnes dans les cartes adaptatives avec la recherche dans l’organisation :

:::image type="content" source="../../assets/images/Cards/peoplepicker-org-search.png" alt-text="Recherche d’organisation du sélecteur de personnes":::

Pour activer la recherche dans une liste de membres de conversation, utilisez le jeu de données approprié défini dans la table du [jeu de données](#dataset) . `isMultiSelect` est utilisée pour activer la sélection de plusieurs utilisateurs dans le contrôle. Il est défini sur false par défaut et ce paramètre vous permet de sélectionner un seul utilisateur uniquement.

### <a name="data-submission"></a>Envoi de données

Vous pouvez utiliser `Action.Submit` ou `Action.Execute` envoyer des données sélectionnées à votre bot. La `invoke` charge utile reçue sur votre bot est une liste d’ID Microsoft Azure Active Directory (Azure AD) ou d’ID fournis dans la liste statique.
Dans le sélecteur de personnes, lorsqu’un utilisateur est sélectionné dans le contrôle, la `Azure AD ID` valeur de l’utilisateur est renvoyée. Il `Azure AD ID` s’agit d’une chaîne qui identifie de façon unique un utilisateur dans le répertoire.

Le format de la valeur soumise au bot dépend de la valeur de la `isMultiSelect` propriété :

|valeur de `isMultiSelect`|Format|
|--|--|
|false _(sélection unique)_|<selected_Azure_AD_ID>|
|true _(sélection multiple)_|<selected_Azure_AD_ID_1>,<selected_Azure_AD_ID_2>,<selected_Azure_AD_ID_3>|  

Avec le `Azure AD ID`sélecteur de personnes , présélecte l’utilisateur correspondant.

## <a name="preselection-of-user"></a>Présélection de l’utilisateur

People Picker prend en charge la présélection de l’utilisateur dans le contrôle, lors de la création et de l’envoi d’une carte adaptative. `Input.ChoiceSet` prend en charge la `value` propriété utilisée pour préélecter un utilisateur. Le format de cette `value` propriété est le même que le format de valeur soumis dans la [soumission de données](#data-submission).  
La liste suivante fournit les informations permettant de préélectionner les utilisateurs :

* Pour un utilisateur unique dans le contrôle, spécifiez l’utilisateur `Azure AD ID` en tant que `value`.
* Pour plusieurs utilisateurs, par `isMultiSelect` `true`exemple, spécifiez une chaîne séparée par des virgules.`Azure AD ID`  

L’exemple suivant décrit la présélection d’un seul utilisateur :

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

L’exemple suivant décrit la présélection de plusieurs utilisateurs :

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

Les choix statiques prennent en charge les scénarios dans lesquels des profils personnalisés doivent être insérés dans les jeux de données prédéfinis. `Input.ChoiceSet` prend en charge la `choices` spécification statique dans le json. Le choix statique est utilisé pour créer les choix que l’utilisateur peut sélectionner.

> [!NOTE]
> Les données statiques `choices` sont utilisées avec des jeux de données dynamiques.

Le choix se compose de `title` et `value`. Lorsqu’ils sont utilisés avec le sélecteur de personnes, ces choix sont traduits en profils utilisateur qui ont le `title` nom et l’identificateur `value` . Ces profils personnalisés font également partie des résultats de la recherche lorsque la requête de recherche correspond à la valeur donnée `title`.
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

L’image suivante illustre le sélecteur de personnes dans les cartes adaptatives avec des choix statiques dans la recherche d’organisation :

:::image type="content" source="../../assets/images/Cards/peoplepicker-static-choice.png" alt-text="people-picker-static-choice":::

Vous pouvez implémenter people picker pour une gestion efficace des tâches dans différents scénarios.  

## <a name="code-sample"></a>Exemple de code

| Exemple de nom           | Description | C#    | Node.js   |
|:---------------------|:--------------|:---------|:--------|
|Contrôle du sélecteur de personnes dans les cartes adaptatives| Cet exemple montre comment utiliser le contrôle sélecteur de personnes dans les cartes adaptatives.|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-people-picker-adaptive-card/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-people-picker-adaptive-card/nodejs) |

## <a name="see-also"></a>Voir aussi

[Informations de référence sur les cartes](cards-reference.md)
