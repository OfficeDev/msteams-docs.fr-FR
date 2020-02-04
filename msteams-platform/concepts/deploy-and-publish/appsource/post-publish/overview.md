---
title: Publication post
description: Ce qu’il faut faire après avoir publié votre application
keywords: teams post publier le certificat de mise à jour
ms.openlocfilehash: 05e4ea47bbf81967ccf086230bf0ad8c633f6e0b
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673633"
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
* Incrémentez votre numéro de version dans votre manifeste.

### <a name="when-does-updating-your-app-trigger-the-user-consent-flow"></a>Quand la mise à jour de votre application déclenche-t-elle le flux de consentement de l’utilisateur ?

Lorsqu’un utilisateur installe votre application, il est autorisé à accorder à l’application l’autorisation d’accéder aux services et informations dont elle a besoin pour faire son travail. Lorsque vous mettez à jour votre application, vous pouvez réactiver ce comportement de consentement, en particulier si vous avez effectué une ou plusieurs des modifications suivantes :

* Ajout d’une nouvelle fonctionnalité à une application, telle que l’ajout d’un bot à une application de type onglet uniquement.
* Modification du tableau d’autorisations dans le manifeste.
* Incrémentez le numéro de version de votre application dans votre manifeste.
