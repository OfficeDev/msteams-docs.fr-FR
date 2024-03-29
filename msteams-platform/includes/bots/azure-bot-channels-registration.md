---
title: Inscription au canal du bot Azure
description: décrit les canaux du bot Azure pour l’inscription
localization_priority: Normal
ms.topic: overview
ms.author: surbhigupta12
ms.openlocfilehash: 96d7ed857074547d0c3da5b412b8065d063f3a3100da6a7431fd65879bfa91ff
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/07/2021
ms.locfileid: "57703789"
---
1. Dans le [portail Azure,](https://ms.portal.azure.com/#home)sous services Azure, **sélectionnez Créer une ressource.**
1. Dans la zone de recherche, entrez « bot ». And in the drop-down list, select **Bot Channels Registration**.
1. Sélectionnez **le bouton** Créer.
1. Dans le blade **d’inscription du** canal bot, fournissez les informations demandées sur votre bot.
1. Laissez la **zone de point de terminaison** de messagerie vide pour le moment, vous entrez l’URL requise après le déploiement du bot. L’image suivante montre un exemple des paramètres d’inscription :

    ![inscription des canaux d’application bot](../../assets/images/authentication/auth-bot-channels-registration.png)

1. Cliquez **sur L’ID et le mot de passe de l’application Microsoft,** **puis créez-en un.**

    ![Créer un ID d’application ](../../assets/images/authentication/CreateMicrosoftAppID.png) ![ Microsoft : créer un ID d’application Microsoft](../../assets/images/authentication/CreateNewMicrosoftAppID.png)    

1. Cliquez **sur Créer un ID d’application dans le lien Portail d’inscription des** applications.

   ![Inscriptions des applications](../../assets/images/authentication/AppRegistration.png)
   
1. Dans la fenêtre **d’inscription de l’application** affichée, cliquez sur l’onglet Nouvelle **inscription** dans le coin supérieur gauche.
1. Entrez le nom de l’application bot que vous inscrivez, nous avons *utilisé BotTeamsAuth* (vous devez sélectionner votre propre nom unique).
1. Pour les **types** de comptes pris en charge, sélectionnez Comptes dans n’importe quel répertoire d’organisation (n’importe quel annuaire *Azure AD - Multi-client)* et comptes Microsoft personnels (par exemple, Skype, Xbox).
1. Cliquez sur **le bouton** Enregistrer. Une fois terminé, Azure affiche la page *Vue d’ensemble* de l’application.
1. Copiez et enregistrez dans un fichier la valeur de **l’ID** de l’application (client).
1. Dans le panneau gauche, cliquez sur **Certificat et secrets.**
    1. Sous *Les secrets client,* cliquez **sur Nouvelle secret client.**
    1. Ajoutez une description pour identifier ce secret auprès d’autres personnes que vous devrez peut-être créer pour cette application.
    1. La *sélection expire.*
    1. Cliquez sur **Ajouter**.
    1. Copiez la secret client et enregistrez-la dans un fichier.
1. Revenir à la fenêtre Inscription du canal bot  et copiez respectivement  *l’ID* d’application et la secret client dans les zones  **ID** de l’application Microsoft et Mot de passe.
1. Cliquez sur **OK**.
1. Enfin, cliquez sur **Créer.**

Une fois qu’Azure a créé la ressource d’inscription, elle sera incluse dans la liste des groupes de ressources.  

![groupe d’inscription des canaux d’application bot](~/assets/images/authentication/auth-bot-channels-registration-group.PNG)

Une fois l’inscription de vos canaux de bot créée, vous devez activer le canal Teams bot.

1. Dans le [portail Azure, sous](https://ms.portal.azure.com/#home)services Azure, sélectionnez l’inscription du canal bot **que** vous avez créée.
1. Dans le panneau gauche, cliquez sur **Canaux**.
1. Cliquez sur l Microsoft Teams icône, puis sélectionnez **Enregistrer.**
