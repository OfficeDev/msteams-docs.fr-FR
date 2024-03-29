---
title: Intégrer Sélecteur de personnes
description: Dans cet article, découvrez comment utiliser le Kit de développement logiciel (SDK) du client JavaScript Teams pour intégrer le contrôle Sélecteur de personnes et les avantages de l’utilisation du sélecteur de personnes.
ms.topic: conceptual
ms.localizationpriority: high
ms.author: surbhigupta
ms.openlocfilehash: 0b70dcc6aaa95b1a21b8b11081aa39b235cab296
ms.sourcegitcommit: 53818e55dfe0dbdf874d578a40982f7db444f89b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/01/2022
ms.locfileid: "68319943"
---
# <a name="integrate-people-picker"></a>Intégrer Sélecteur de personnes

People Picker est un contrôle de saisie dans Teams qui permet aux utilisateurs de rechercher et de sélectionner des personnes. Vous pouvez intégrer le contrôle de saisie People Picker dans une application Web, ce qui permet aux utilisateurs finaux d'exécuter différentes fonctions telles que la recherche et la sélection de personnes dans un chat, un canal ou dans toute l'organisation au sein de Teams. Le contrôle People Picker est disponible sur tous les clients Teams, tels que le web, le bureau et le mobile.

Vous pouvez utiliser le [SDK client JavaScript de Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), qui fournit l'API `selectPeople` pour intégrer le contrôle de saisie People Picker dans votre application Web.

## <a name="advantages-of-using-people-picker"></a>Avantages de l’utilisation de Sélecteur de personnes

* Fonctionne sur toutes les fonctionnalités teams, telles que le module de tâche, la conversation, le canal, l’onglet réunion et l’application personnelle.
* Permet à l’utilisateur de rechercher et de sélectionner des personnes dans une conversation, un canal ou toute l’organisation au sein de Teams.
* Aide dans les scénarios impliquant l’affectation de tâches, le marquage et la notification de l’utilisateur.
* Économise beaucoup de temps et d’efforts par rapport à la création d’un contrôle similaire.

Pour intégrer le contrôle de saisie People Picker dans votre application Teams, utilisez l'API [`selectPeople`](#selectpeople-api). Pour intégrer et appeler l'API, vous devez avoir une bonne compréhension de l'extrait de [code suivant](#code-snippet). Vous devez également connaître les [erreurs de réponse d’API](#error-handling).

## <a name="selectpeople-api"></a>API `selectPeople`

L'API `selectPeople` vous permet d'ajouter le contrôle d'entrée Teams People Picker aux applications Web et vous aide également dans les domaines suivants :

* Permet à l’utilisateur de rechercher et de sélectionner une ou plusieurs personnes dans la liste.
* Retourne l’ID, le nom et l’adresse e-mail des utilisateurs sélectionnés à l’application web.

Dans une application personnelle, le contrôle recherche le nom ou l'identifiant de messagerie dans toute l'organisation au sein de Teams. Si l’application est ajoutée à une conversation ou à un canal, le contexte de recherche est configuré en fonction du scénario. La recherche est limitée dans les membres de cette conversation ou canal.

L’API `selectPeople` est livré avec les configurations d’entrée suivantes :

|Paramètre de configuration|Type|Description| Valeur par défaut|
|-----|------|--------------|------|
|`title`|Chaîne| Il s’agit d’un paramètre facultatif qui définit le titre du contrôle S sélectionneur de personnes.|`selectPeople`|
|`setSelected`|Chaîne| Il s’agit d’un paramètre facultatif. Vous devez transmettre Microsoft Azure Active Directory (Azure AD) des personnes à pré-sélectionné. Ce paramètre présélectionne les personnes lors du lancement du contrôle d’entrée du sélectionneur de personnes. Dans une sélection unique, seul le premier utilisateur valide est pré-rempli en ignorant le reste.|**Null**|
|`openOrgWideSearchInChatOrChannel`|Boolean| Il s'agit d'un paramètre facultatif qui, lorsqu'il est défini sur true, lance le People Picker dans l'ensemble de l'organisation, même si l'application est ajoutée à un chat ou à un canal.|**False**|
|`singleSelect`|Boolean|Il s'agit d'un paramètre facultatif qui, lorsqu'il est défini sur true, lance le People Picker et limite la sélection à un seul utilisateur.|**False**|

L’image suivante affiche l’expérience de Sélecteur de personnes sur les appareils mobiles et de bureau :

# <a name="mobile"></a>[Mobile](#tab/Samplemobileapp)

Le contrôle d’entrée Sélecteur de personnes permet à l’utilisateur de rechercher et d’ajouter des personnes en procédant comme suit :

1. Tapez le nom de la personne que vous voulez inviter. La liste s’affiche avec des suggestions de nom.
1. Sélectionnez le nom de la personne requise dans la liste.

   :::image type="content" source="../../assets/images/tabs/people-picker-control-capability-mobile-updated.png" alt-text="S’il s’est s’il est mobile":::

# <a name="desktop"></a>[Imprimante de bureau](#tab/Sampledesktop)

Le contrôle People Picker sur le web ou le bureau est lancé dans une fenêtre modale en haut de votre application web et pour ajouter des personnes, suivez les étapes suivantes :

1. Tapez le nom de la personne que vous voulez inviter. La liste s’affiche avec des suggestions de nom.
1. Sélectionnez le nom de la personne requise dans la liste.

   :::image type="content" source="../../assets/images/tabs/select-people-picker-byname.png" alt-text="Sélecteur de personnes par nom bureau":::

---

## <a name="code-snippet"></a>Extrait de code

L’extrait de code suivant affiche l’utilisation des personnes `selectPeople` de l’API à partir d’une liste :

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

```javascript
people.selectPeople({ setSelected: ["aad id"], openOrgWideSearchInChatOrChannel: true, singleSelect: false, title: true}).then(people) => 
 {
    output(" People length: " + people.length + " " + JSON.stringify(people));
 }).catch((error) => { /*Unsuccessful operation*/ });
```

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

```javascript
people.selectPeople((error: microsoftTeams.SdkError, people: microsoftTeams.people.PeoplePickerResult[]) => 
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
  },{ setSelected: ["aad id"], openOrgWideSearchInChatOrChannel: true, singleSelect: false, title: true});
```

***

## <a name="error-handling"></a>Gestion des erreurs

Le tableau suivant répertorie les codes d’erreur et leurs descriptions :

|Code d’erreur |  Nom de l’erreur     | Description|
| --------- | --------------- | --------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | L’API n’est pas prise en charge sur la plateforme actuelle.|
| **500** | INTERNAL_ERROR | Erreur interne rencontrée lors du lancement de Sélecteur de personnes.|
| **4000** | ARGUMENTS NON VALIDES | L’API est appelée avec des arguments obligatoires incorrects ou insuffisants.|
| **8000** | USER_ABORT |L’utilisateur a annulé l’opération.|
| **9000** | OLD_PLATFORM | L’utilisateur se trouve sur une ancienne build de plateforme où l’implémentation de l’API n’est pas disponible. Mettre à niveau vers la dernière version de la build pour résoudre le problème.|

## <a name="see-also"></a>Voir aussi

* [Intégrer les fonctionnalités médias](~/concepts/device-capabilities/media-capabilities.md)
* [Intégrer le code QR ou la fonctionnalité de scanneur de code-barres dans Teams](qr-barcode-scanner-capability.md)
* [Intégrer les fonctionnalités d’emplacement sur Teams](location-capability.md)
* [composant de sélecteur Personnes dans le Kit de ressources Microsoft Graph](/graph/toolkit/components/people-picker)
