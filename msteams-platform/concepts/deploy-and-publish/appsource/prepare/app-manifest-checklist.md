---
title: Liste de contrôle des manifestes de l’application
description: Liste de vérification pour le manifeste de votre application pour la publication de votre application Microsoft Teams dans AppSource
ms.topic: reference
localization_priority: Normal
keywords: teams publish store office publishing checklist
ms.openlocfilehash: a8fd57d8050530856fa635f59c0a6ce4f8c2a5cf
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019901"
---
# <a name="app-manifest-checklist"></a>Liste de contrôle des manifestes de l’application

>[!IMPORTANT]
>Nous effectuons la migration de la gestion des solutions Office du Tableau de bord vendeur à l’Espace partenaires. Pour plus d’informations, voir [Déplacement du Tableau de bord vendeur vers l’Espace partenaires](https://developer.microsoft.com/office/blogs/moving-management-of-solutions-from-seller-dashboard-to-partner-center/) et [FAQ](https://docs.microsoft.com/office/dev/store/partner-center-faq).

Votre manifeste d'application doit être conforme aux instructions décrites ci-dessous.

>[!Tip]
> Utilisez App Studio pour vous aider à créer votre manifeste d'application. Il validera la plupart des conditions requises ci-dessous pour vous et affichera les erreurs ou avertissements sous l'onglet **Test et** Distribution.

## <a name="tips"></a>Conseils

* N'utilisez pas « Teams », « Microsoft » ou « app » dans le nom de votre application.
* Le developerName dans votre manifeste doit être identique au nom du fournisseur défini dans l'Partner Center.
* Assurez-vous que la description, les captures d'écran, le texte et les images promotionnelles de l'application décrivent uniquement l'application et qu'elles ne contiennent pas de publicités, de promotions ou de noms de marque protégés par copyright.
* Si votre produit nécessite un compte sur votre service ou un autre service, affichez cette liste dans la description et assurez-vous qu'il existe des liens pour s'inscrire, vous inscrire et vous en servir.
* Si votre produit nécessite des achats supplémentaires pour fonctionner correctement, listez-le dans la description.
* Fournissez les liens requis concernant les conditions et la politique de confidentialité dans le manifeste et dans l'Partner Center ou le Tableau de bord. Vérifiez que les liens sont correctement résolus vers la documentation appropriée, dans l'idéal, spécifique à Teams. Pour les bots, vous devez fournir ces informations dans la section Soumission de la page d'inscription bot Framework.
* Assurez-vous que les métadonnées dans le manifeste correspond exactement aux métadonnées dans l'Partner Center (et, pour les bots, dans l'inscription Bot Framework). Notez que votre entrée de l'Centre partenaires peut contenir une description plus détaillée et mise en forme à utiliser dans la page du produit AppSource.
* Assurez-vous que le titre de l'application utilisé dans votre manifeste correspond **exactement** au titre de l'application entré dans la soumission de l'Partner Center. *Voir* Créer des listes efficaces dans Microsoft AppSource et dans Office — Utilisez un nom [de add-in cohérent.](https://docs.microsoft.com/office/dev/store/create-effective-office-store-listings#use-a-consistent-add-in-name)

## <a name="metadata-requirement"></a>Conditions requises pour les métadonnées

Les métadonnées suivantes sont requises pour votre application.

|Données|Type|Size|Manifeste|Espace partenaires|Description|
|---|---|---|---|---|---|
|Package d'application|.zip|||✔|Package d'application réel pour le chargement ou la soumission d'AppSource.|
|Logo couleur|.png|192 &times; 192 pixels|`icon.color`||Icône à afficher dans la liste des pages de produits dans la galerie Teams. Il s'agit de votre logo de produit en couleur.|
|Plan du logo|.png|32 &times; 32 pixels|`icon.outline`||Icône à afficher dans Teams, dans le canal de conversation Teams et dans d'autres emplacements. Il s'agit de votre logo rendu sous la forme d'un plan blanc avec un arrière-plan transparent.|
|Logo de l'application|.png, .jpg, .jpeg, .gif|300 &times; 300 pixels||✔|Icône à afficher dans AppSource. Il s'agit du logo de produit en couleur complète et d'un fichier différent de celui utilisé dans le manifeste pour `icon.color` . Elle doit être plus petite que 512 Ko.|
|Lien de support|URL|||✔|Lien vers le support technique pour les utilisateurs finaux qui n'ont peut-être pas installé votre application. Lien accessible publiquement sans connexion (HTTPS).|
|Lien confidentialité|URL||`developer.privacyUrl`|✔|Lien vers votre politique de confidentialité (HTTPS).|
|Lien de la vidéo|URL|||Facultatif|Lien vers une vidéo sur votre application.|
|EULA|.doc, .pdf, etc.|||Facultatif|AppSource nécessite un contrat de licence utilisateur final que vous pouvez fournir en pièce jointe. Si vous choisissez de ne pas soumettre un accord de niveau de service, un autre sera fourni en votre nom.|
|Conditions d'utilisation|URL||`developer.termsOfServiceUrl`||Lien vers vos conditions d'utilisation (HTTPS).|
|Test Notes|Remplissage en ligne ou lien vers une URL publique|||Notes de test détaillées sur la façon de tester pas à pas votre application. Veuillez inclure deux informations d'identification de connexion pour tester les scénarios d'administration et de non-administrateur.|

## <a name="localized-content"></a>Contenu localisée

> [!NOTE]
> AppSource prévoit de prendre en charge le contenu localisée pour les métadonnées suivantes. Actuellement, la liste de votre application s'affiche uniquement en anglais dans AppSource, mais elle s'affiche correctement dans le client Teams. Pour [plus d'informations, voir](~/concepts/build-and-test/apps-localization.md) la recherche de votre application.

|Données|Type|Size|Manifeste|Espace partenaires|Description|
|---|---|---|---|---|---|
|Nom de l'application|String|30|`name.short`|✔|Nom de votre application tel qu'il doit apparaître dans la boutique et dans le produit.|
|Nom de l'application longue|String|30|`name.full`|✔|Nom de votre application tel qu'il doit apparaître dans la boutique et dans le produit.|
|Description brève|String|80|`description.short`|✔|Brève description de votre application.|
|Description longue|String|4000|`description.full`|✔|Description plus détaillée de votre application. Dans le fichier manifeste, un résumé précis est approprié. Dans l'Centre partenaires, vous pouvez utiliser une description plus riche et mise en forme pour la page du produit AppSource.|
|Captures d'écran (1-5)|.png, .jpg ou .gif|1 366 x 768 h et moins de 1 024 Ko||✔|Au moins une capture d'écran qui illustre l'expérience de votre application. Utilise sur la page de détails de l'application.|

## <a name="submission-extras-for-bots"></a>Soumission de figurants pour les bots

Les bots dans Microsoft Teams doivent être créés à l'aide de Bot Framework. Voir [Créer un bot pour](~/bots/how-to/create-a-bot-for-teams.md) obtenir des instructions. Utilisez une icône de couleur 96 x 96 pour l'icône de votre bot dans Bot Framework.
