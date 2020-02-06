---
title: Liste de vérification du manifeste de l’application
description: Liste de vérification de votre manifeste d’application pour la publication de votre application Microsoft teams sur AppSource
keywords: Microsoft teams publier la liste de vérification de la publication Office
ms.openlocfilehash: 6186daf264f04e04d6037ddfb7d9208994cc3c57
ms.sourcegitcommit: 44ac886c0ca34a16222d3991a61606f8483b8481
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/05/2020
ms.locfileid: "41783877"
---
# <a name="app-manifest-checklist"></a>Liste de vérification du manifeste de l’application

>[!IMPORTANT]
>Nous effectuons la migration de la gestion des solutions Office du Tableau de bord vendeur à l’Espace partenaires. Pour plus d’informations, voir [Déplacement du Tableau de bord vendeur vers l’Espace partenaires](https://developer.microsoft.com/office/blogs/moving-management-of-solutions-from-seller-dashboard-to-partner-center/) et [FAQ](https://docs.microsoft.com/office/dev/store/partner-center-faq).

Le manifeste de votre application doit être conforme aux instructions décrites ci-dessous.

>[!Tip]
> Utilisez App Studio pour vous aider à créer votre manifeste d’application. Il validera la plupart des conditions requises ci-dessous, et affichera les erreurs ou les avertissements sur l’onglet **test et distribution** .

## <a name="tips"></a>Conseils

* N’utilisez pas « Teams », « Microsoft » ou « app » dans le nom de votre application.
* Le developerName dans votre manifeste doit être le même que le nom du fournisseur défini dans le centre de partenaires.
* Assurez-vous que la description de l’application, les captures d’écran, le texte et les images promotionnelles décrivent uniquement l’application et qu’elles ne contiennent aucune publicité, promotion ou nom de marque protégé supplémentaire.
* Si votre produit nécessite un compte sur votre service ou un autre service, répertoriez-le dans la description et vérifiez qu’il existe des liens pour vous inscrire, connectez-vous et déconnectez-vous.
* Si votre produit nécessite des achats supplémentaires pour fonctionner correctement, répertoriez-le dans la description.
* Fournissez les conditions requises et les liens de politique de confidentialité dans le manifeste et le Centre des partenaires ou le tableau de bord. Vérifiez que les liens correspondent correctement à la documentation appropriée, à l’idéal pour les équipes spécifiques. Pour les robots, vous devez fournir ces mêmes informations dans la section envoi de la page d’inscription de l’infrastructure bot.
* Assurez-vous que les métadonnées dans le manifeste correspondent exactement aux métadonnées du centre de partenaires (et, pour les robots, dans l’inscription de l’infrastructure de robot). Notez que votre entrée du centre partenaires peut contenir une description plus détaillée et mise en forme pour l’utiliser dans la page du produit AppSource.
* Assurez-vous que le titre de l’application utilisé dans votre manifeste est une **correspondance exacte** avec le titre de l’application entré dans l’envoi du centre partenaire. *Consultez la rubrique* [créer des listes efficaces dans Microsoft AppSource et dans Office, utilisez un nom de complément cohérent ](https://docs.microsoft.com/office/dev/store/create-effective-office-store-listings#use-a-consistent-add-in-name).

## <a name="metadata-requirement"></a>Exigences de métadonnées

Les métadonnées suivantes sont requises pour votre application.

|Données|Type|Taille|Manifeste|Espace partenaires|Description|
|---|---|---|---|---|---|
|Package d’application|.zip|||✔|Package d’application réel pour le téléchargement ou l’envoi AppSource.|
|Logo couleur|.png|192&times;192 pixels|`icon.color`||Icône à afficher dans la liste de la page du produit dans la Galerie Teams. Il s’agit du logo de votre produit pleine couleur.|
|Contour du logo|.png|32&times;32 pixels|`icon.outline`||Icône à afficher dans Teams, dans le canal de conversation de teams et dans d’autres emplacements. Il s’agit de votre logo affiché sous la forme d’un contour blanc avec arrière-plan transparent.|
|Logo de l’application|. png,. jpg,. jpeg,. gif|300&times;300 pixels||✔|Icône à afficher dans AppSource. Il s’agit du logo de produit pleine couleur, qui est un fichier différent de celui utilisé dans le manifeste pour `icon.color`. elle doit être inférieure à 512 Ko.|
|Lien de support|URL|||✔|Lien permettant de prendre en charge les informations pour les utilisateurs finaux qui n’ont peut-être pas installé votre application. Lien accessible au public accessible sans connexion (HTTPs).|
|Lien de confidentialité|URL||`developer.privacyUrl`|✔|Un lien vers votre politique de confidentialité (HTTPs).|
|Lien de la vidéo|URL|||Facultatif|Lien vers une vidéo sur votre application.|
|ACCORD|. doc,. pdf, etc.|||Facultatif|AppSource nécessite un contrat de licence utilisateur final (CLUF), que vous pouvez fournir en tant que pièce jointe. Si vous choisissez de ne pas soumettre de contrat de licence, un seul sera fourni à votre place.|
|Conditions de service|URL||`developer.termsOfServiceUrl`||Un lien vers vos conditions de service (HTTPs).|
|Notes de test|Insérer un remplissage incorporé ou un lien vers une URL publique|||Notes de test détaillées sur la façon de tester votre application étape par étape. Veuillez inclure deux informations d’identification pour le test des scénarios d’administrateur et non d’administrateur.|

## <a name="localized-content"></a>Contenu localisé

> [!NOTE]
> AppSource prévoit de prendre en charge le contenu localisé pour les métadonnées suivantes. Actuellement, le Listing de votre application s’affichera uniquement en anglais dans AppSource, mais sera affiché correctement dans le client Teams. Pour plus d’informations, consultez [la rubrique Localizing Your App](~/concepts/build-and-test/apps-localization.md) .

|Données|Type|Taille|Manifeste|Espace partenaires|Description|
|---|---|---|---|---|---|
|Nom de l'application|Chaîne|0,30|`name.short`|✔|Nom de votre application tel qu’il doit apparaître dans la boutique et dans le produit.|
|Nom de l’application longue|Chaîne|0,30|`name.full`|✔|Nom de votre application tel qu’il doit apparaître dans la boutique et dans le produit.|
|Description brève|Chaîne|80|`description.short`|✔|Brève description de votre application.|
|Description longue|Chaîne|4000|`description.full`|✔|Description plus détaillée de votre application. Dans le fichier manifeste, un résumé précis est approprié. Dans le centre de partenaires, vous pouvez utiliser une description enrichie et mise en forme pour la page du produit AppSource.|
|Captures d’écran (1-5)|. png,. jpg ou. gif|1366w x 768h et inférieur à 1024 Ko||✔|Au moins une capture d’écran illustrant votre expérience d’application. Utilise sur la page des détails de l’application.|

## <a name="submission-extras-for-bots"></a>Soumission de compléments pour les robots

Les robots de Microsoft teams doivent être créés à l’aide de bot Framework. Pour obtenir des instructions, consultez [la rubrique Create a bot](~/bots/how-to/create-a-bot-for-teams.md) . Utiliser une icône de couleur 96 x 96 pour l’icône de votre robot dans l’infrastructure de robot.
