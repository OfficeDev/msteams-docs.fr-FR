---
title: Publication post
description: Ce qu’il faut faire après avoir publié votre application
keywords: teams post publier le certificat de mise à jour
ms.openlocfilehash: 77b74d77546de0ae93b0ae39aec925d2e3dec2cf
ms.sourcegitcommit: fdc50183f3f4bec9e4b83bcfe5e016b591402f7c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/24/2020
ms.locfileid: "44867092"
---
# <a name="maintain-and-support-your-published-app"></a>Gérer et prendre en charge votre application publiée 

Une fois que votre application est approuvée et inscrite dans le catalogue d’applications public, vous pouvez augmenter votre portée en obtenant la certification de l’application ou en ajoutant un bouton de téléchargement de votre site Web.

## <a name="application-certificate"></a>Certificat d’application

Microsoft fournit un [programme de certification d’application](./application-certification.md) qui compile vos informations d’application et les présente sur la [page de sécurité et de conformité des applications Microsoft teams](https://aka.ms/AppCertification). Ces informations visent à aider les administrateurs à choisir les applications qui sont sûres pour leur organisation.

## <a name="add-a-download-button-to-your-product-site"></a>Ajouter un bouton de téléchargement à votre site de produit

Si votre application se trouve dans le magasin Microsoft Teams, vous pouvez générer un lien vers votre site Web qui lance teams et affiche une boîte de dialogue de consentement et d’installation pour permettre aux utilisateurs d’ajouter l’application.
Le format est : `https://teams.microsoft.com/l/app/<appId>` où AppID est le GUID qu’il déclare dans le manifeste soumis.
Exemple : `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` est le lien pour installer Trello.

## <a name="updating-your-existing-teams-app"></a>Mise à jour de votre application teams existante

* N’utilisez pas le bouton *Ajouter une nouvelle application* pour renvoyer votre application. Utilisez plutôt la mosaïque de votre application sous l’onglet vue d’ensemble.
* L’appId dans le manifeste mis à jour doit être le même que dans le manifeste actuel, avec un numéro de version incrémentiel.
* Incrémentez votre numéro de version dans le manifeste si vous effectuez des modifications de manifeste dans votre envoi.
* Les soumissions mises à jour doivent être soumises à un nouveau processus de révision et de validation.

## <a name="app-updates-and-the-user-consent-flow"></a>Mises à jour de l’application et flux de consentement de l’utilisateur

Lorsqu’un utilisateur installe votre application, il est autorisé à accorder à l’application l’autorisation d’accéder aux services et informations dont elle a besoin pour faire son travail. Dans la plupart des cas, une fois que vous avez terminé une mise à jour de l’application, la nouvelle version s’affiche automatiquement pour les utilisateurs finaux. Toutefois, certaines mises à jour du manifeste de l' [application teams](../../../../resources/schema/manifest-schema.md) nécessitent l’acceptation de l’utilisateur et peuvent déclencher à nouveau ce comportement de consentement :

 >[!div class="checklist"]
>
> * Un bot a été ajouté ou supprimé.
> * La valeur unique d’un bot existant `botId` a changé.
> * La valeur booléenne d’un bot existant `isNotificationOnly` a changé.
> * La valeur booléenne d’un bot existant `supportsFiles` a changé.
> * Une extension de messagerie ( `composeExtensions` ) a été ajoutée ou supprimée.
> * Un nouveau connecteur a été ajouté.
> * Un nouvel onglet statique/personnel a été ajouté.
> * Un nouvel onglet de groupe/canal configurable a été ajouté.
> * Les `webApplicationInfo` valeurs ont changé.
>