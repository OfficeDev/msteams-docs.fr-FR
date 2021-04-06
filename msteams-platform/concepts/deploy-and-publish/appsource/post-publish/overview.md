---
title: Maintenance et prise en charge de votre application publiée
description: Que faire une fois que vous avez publié votre application
ms.topic: how-to
keywords: teams publient le manifeste de mise à jour de l’application de certification des mises à jour
ms.openlocfilehash: 8644db5e329e15d77062553eda4a41a36b2740ee
ms.sourcegitcommit: e78c9f51c4538212c53bb6c6a45a09d994896f09
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/05/2021
ms.locfileid: "51585833"
---
# <a name="maintain-and-support-your-published-app"></a>Maintenir et prendre en charge votre application publiée 

Une fois votre application approuvée et répertoriée dans le catalogue d’applications publiques, vous pouvez augmenter votre portée en complétant le programme de conformité des applications Microsoft 365 ou en ajoutant un bouton de téléchargement sur votre site web.

## <a name="microsoft-365-certified"></a>Certification Microsoft 365

Le programme de conformité des applications [Microsoft 365](./application-certification.md), est une approche à trois niveaux pour la sécurité et la conformité des applications. Chaque niveau s’appuie sur le suivant , offrant un programme en couches pour répondre aux besoins de votre client. Vous pouvez en savoir plus sur la posture de sécurité et de conformité des applications Teams en visitant la [page de conformité.](https://docs.microsoft.com/microsoft-365-app-certification/teams/teams-apps)

## <a name="add-a-download-button-to-your-product-site"></a>Ajouter un bouton de téléchargement à votre site de produit

Si votre application se trouve dans le magasin global Microsoft Teams, vous pouvez générer un lien pour votre site web qui lance Teams et affiche une boîte de dialogue de consentement et d’installation pour que les utilisateurs ajoutent l’application.
Le format est :  `https://teams.microsoft.com/l/app/<appId>` où appID est le GUID qu’ils déclarent dans le manifeste envoyé.
Exemple : `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` est le lien vers l’installation de Trello.

## <a name="updating-your-existing-teams-app"></a>Mise à jour de votre application Teams existante

* N’utilisez pas *le bouton Ajouter une nouvelle application* pour resoumettre votre application. Utilisez plutôt la vignette de votre application sous l’onglet Vue d’ensemble.
* L’appId dans le manifeste mis à jour doit être le même que dans le manifeste actuel, avec un numéro de version incrémenté.
* Incrémentez votre numéro de version dans le manifeste si vous a apporté des modifications à votre soumission, y compris le nom de l’application ou des métadonnées dans le manifeste.
* Les soumissions mises à jour sont requises pour faire l’objet d’un nouveau processus de révision et de validation.

## <a name="app-updates-and-the-user-consent-flow"></a>Mises à jour de l’application et flux de consentement de l’utilisateur

Lorsqu’un utilisateur installe votre application, l’une des premières choses qu’il fait est de donner à l’application l’autorisation d’accéder aux services et aux informations dont l’application a besoin pour faire son travail. Dans la plupart des cas, une fois que vous avez terminé la mise à jour d’une application, la nouvelle version s’affiche automatiquement pour les utilisateurs finaux. Toutefois, certaines mises à jour du manifeste de l’application [Teams](../../../../resources/schema/manifest-schema.md) nécessitent l’acceptation de l’utilisateur et peuvent déclencher de nouvelles fois ce comportement de consentement :

 >[!div class="checklist"]
>
> * Un bot est ajouté ou supprimé.
> * La valeur unique d’un bot `botId` existant est modifiée.
> * La valeur booléle d’un bot `isNotificationOnly` existant est modifiée.
> * La valeur d’un bot `supportsFiles` ou d’un `supportsCalling` booléen existant est modifiée.
> * Une extension de `composeExtensions` messagerie est ajoutée ou supprimée.
> * Un nouveau connecteur est ajouté.
> * Un nouvel onglet statique ou personnel est ajouté.
> * Un nouvel onglet de groupe ou de canal configurable est ajouté.
> * Les propriétés à `webApplicationInfo` l’intérieur sont modifiées. Pour les modifications `webApplicationInfo` apportées à , le consentement est uniquement requis dans l’étendue Teams.

### <a name="images-of-user-consent-flow"></a>Images du flux de consentement de l’utilisateur :

**Configurer un connecteur : cet** écran s’affiche uniquement pour les utilisateurs de Teams.

![Configuration du flux de consentement d’un diagramme de connecteur](../../../../assets/images/connector-teams-consentflow.png)

**Flux de consentement utilisateur** : cet écran est courant pour les étendues personnelle et de groupe. Ici, sélectionnez la case **à cocher Consentement** au nom de votre organisation et choisissez **Accepter**.

![Diagramme des autorisations](../../../../assets/images/user-consent-flow.png)
