---
title: Télécharger votre application personnalisée
description: Décrit comment télécharger votre application dans Microsoft Teams
ms.topic: how-to
ms.author: lajanuar
keywords: téléchargement d’applications Teams
ms.openlocfilehash: 3ca086cf8dbb992de84b22b7499f739d7c80b9d6
ms.sourcegitcommit: 9cfbc44912980a33d2d7c7c85739aeea6ccb41de
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/05/2021
ms.locfileid: "50479880"
---
# <a name="upload-an-app-package-to-microsoft-teams"></a>Téléchargement d’un package d’application dans Microsoft Teams

Pour tester votre expérience d’application dans Microsoft Teams, vous devez télécharger votre application dans Teams. Le téléchargement ajoute l’application à l’équipe sélectionnée et tous les membres de l’équipe peuvent interagir avec elle comme les utilisateurs finaux.

> [!NOTE]
> Le téléchargement d’un package mis à jour pour une application existante avec un bot peut ne pas afficher les modifications apportées aux onglets lorsqu’il est vu dans la fenêtre de conversations. Vous pouvez accéder à l’application via le volant des applications ou tester dans un environnement propre.

## <a name="create-your-upload-package"></a>Créer votre package de chargement

Pour le développement et la soumission à AppSource, vous devez créer un package que vous pouvez télécharger. Le package doit contenir les informations pour décrire votre expérience. Le package est un fichier .zip qui contient le manifeste de l’application et les icônes qui définissent votre expérience de manière unique.

Pour créer un package de chargement, voir [Créer le package pour votre application Microsoft Teams.](../build-and-test/apps-package.md)

Après avoir créé le package, téléchargez-le dans une équipe. Le package téléchargé est uniquement disponible pour les utilisateurs de l’équipe sélectionnée.

## <a name="load-your-package-into-teams"></a>Charger votre package dans Teams

Vous pouvez tester votre package en le téléchargeant dans Teams.

> [!NOTE]
> Pour que le téléchargement fonctionne, votre administrateur client doit d’abord [activer le téléchargement d’applications.](/microsoftteams/admin-settings)

Il existe deux façons de télécharger votre application dans Teams :

* Utilisation du Store
* Utilisation de l’onglet Applications

## <a name="upload-your-package-into-a-team-or-conversation-using-the-store"></a>Charger votre package dans une équipe ou une conversation à l’aide du Store

1. Dans le coin inférieur gauche de Teams, sélectionnez **l’icône du** Store. On the Store page, choose **Upload a custom app**.

  ![Afficher l’équipe](../../assets/images/store-upload-a-custom-app2.png)

2. Dans la **boîte de dialogue** Ouvrir, accédez au package que vous souhaitez télécharger et choisissez Ouvrir.

   ![Menu Ajouter](../../assets/images/NewappAddmenudropdown.png)

Le package téléchargé doit être disponible pour être utilisé dans l’équipe ou la conversation spécifiée dans la boîte de dialogue de consentement. Si votre application n’apparaît pas, la raison la plus courante est une erreur dans le manifeste, en particulier les ID de l’application, du bot et des extensions de messagerie. Si l’application n’est pas limitée aux conversations, cette option n’apparaît pas.

>[!NOTE]
> Les applications dans les conversations sont actuellement [en](../../resources/dev-preview/developer-preview-intro.md)prévisualisation du développeur et l’option n’apparaît pas si Teams n’est pas en cours d’exécution dans ce mode.

![Exemple de bot dans la liste des bots téléchargés](../../assets/images/botinlist.jpg)

## <a name="upload-your-package-into-a-team-using-the-apps-tab"></a>Télécharger votre package dans une équipe à l’aide de l’onglet Applications

1. Dans l’équipe cible, sélectionnez **Plus d’options** (**&#8943;**) et **sélectionnez Gérer l’équipe.**

   > [!NOTE]
   > Vous devez être le propriétaire de l’équipe ou le propriétaire doit donner accès aux utilisateurs pour ajouter les types d’application appropriés pour que cette fonctionnalité apparaisse.

2. Sélectionnez **l’onglet** Applications et choisissez **Télécharger une application personnalisée** en bas à droite.

   ![Point d’entrée de chargement](../../assets/images/UploadACustomApp.png)

3. Sélectionnez votre package .zip sur l’ordinateur.

4. Vous pouvez voir votre application téléchargée dans la liste.

   ![Exemple de bot dans la liste des bots téléchargés](../../assets/images/botinlist.jpg)

Si votre application ne se charge pas, la raison la plus courante est une erreur dans le manifeste, en particulier les ID de l’application, du bot et des extensions de messagerie.

## <a name="access-your-uploaded-configurable-tab"></a>Accéder à votre onglet configurable téléchargé

Si l’application contient des onglets, les utilisateurs peuvent les épingler à n’importe quel canal de conversation ou d’équipe à l’aide du flux de galerie d’onglets standard :

1. Go to a channel in the team. Choisissez **+** d’ajouter un onglet à droite des onglets existants.

2. Sélectionnez votre onglet dans la galerie qui s’affiche.

3. Acceptez l’invite de consentement.

4. Configurez votre onglet via sa [page de configuration](../../tabs/how-to/create-tab-pages/configuration-page.md) et sélectionnez **Enregistrer.**

  ![Boîte de dialogue Ajouter un onglet, avec une galerie d’onglets disponibles](../../assets/images/tab_gallery.png)

## <a name="access-your-uploaded-bot"></a>Accéder à votre bot téléchargé

Après avoir ajouté le bot à une équipe, il doit être utilisable par toute personne de cette équipe, à l’intérieur et à l’extérieur des canaux de l’équipe, en fonction de la définition de l’étendue du bot. Tous les membres de l’équipe peuvent voir un billet dans le canal général indiquant que le bot a été ajouté à l’équipe. 

Pour un bot Teams, vous pouvez commencer par l’appel de votre bot en @mentioning nom du bot.

Pour tester les conversations directes avec votre bot, vous pouvez y accéder via la page d’accueil de l’application, l'@mention dans un canal ou la rechercher dans la **fenêtre Nouvelle** conversation.

Vous pouvez @mention bot dans une conversation ou le  rechercher dans la fenêtre Nouvelle conversation pour tester les conversations directes avec votre bot.

## <a name="access-your-uploaded-connector"></a>Accéder à votre connecteur téléchargé

Une fois l’application chargée dans l’équipe ou la conversation, les utilisateurs peuvent configurer un connecteur à l’aide du flux de galerie connecteurs standard :

1. Go to a channel in the team. Choose **More options** (*&#8943;*) and choose **Connectors**.

2. Sélectionnez votre connecteur dans la section **Sideloaded** en bas.

3. Configurez votre connecteur via sa [page de configuration](../../webhooks-and-connectors/how-to/connectors-creating.md) et sélectionnez **Enregistrer.**

  ![Boîte de dialogue Ajouter un onglet, avec une galerie d’onglets disponibles.](../../assets/images/connector_gallery.png)

## <a name="access-your-uploaded-messaging-extension"></a>Accéder à votre extension de messagerie téléchargée

Une application téléchargée avec une extension de messagerie apparaît automatiquement dans le menu Plus **d’options** (*&#8943;*) dans la zone de composition.

![Extensions de messagerie](../../assets/images/compose-extensions/cesampleapp.png)

## <a name="add-a-default-install-scope-and-group-capability"></a>Ajouter une étendue d’installation et une fonctionnalité de groupe par défaut

> [!NOTE]
> L’étendue d’installation par défaut et la fonctionnalité de groupe sont actuellement disponibles en prévisualisation pour les développeurs uniquement.

Bien que l’installation d’une application dans l’étendue personnelle fonctionne pour la plupart des applications, certaines des applications du Teams Store la prise en charge des étendues personnelles et d’équipe.
Certaines de ces applications sont conçues pour fonctionner dans une équipe, des réunions ou un groupchat, avec une expérience d’application personnelle secondaire.
La sélection d’étendue d’installation par défaut vous permet de spécifier les applications `defaultInstallScope` que vous publiez. L’expérience d’installation de l’application met les options par défaut à la disposition de l’utilisateur, tandis que les autres sont déplacées sous le chevron, comme le montre l’image.

![Ajouter une application](../../assets/images/compose-extensions/addanapp.png)

La `defaultInstallScope` propriété prend en charge des valeurs, telles que personnelles, d’équipe, de conversation de groupe ou de réunions.

> [!NOTE]
>`defaultGroupCapability` fournit la fonctionnalité par défaut qui est ajoutée à l’équipe, au groupchat ou aux réunions. Choisissez un onglet, un bot ou un connecteur comme fonctionnalité par défaut pour votre application, mais vous devez vous assurer que vous avez fourni la fonctionnalité sélectionnée dans la définition de votre application.

## <a name="remove-or-update-your-app"></a>Supprimer ou mettre à jour votre application

Pour supprimer votre application, sélectionnez l’icône de suppression en regard du nom de l’application dans la liste Afficher les bots **Teams.** Si vous modifiez les informations de manifeste, supprimez d’abord l’application, puis ajoutez le package mis à jour, voir Charger votre [package dans une équipe.](#load-your-package-into-teams) Les modifications de code apportées à votre service ne vous obligent pas à charger à nouveau votre manifeste. Toutefois, si les modifications de code nécessitent des mises à jour de manifeste, telles que des modifications apportées à l’URL ou à l’ID de l’application Microsoft pour son bot, vous devez télécharger à nouveau le manifeste.

> [!NOTE]
> Vous ne pouvez pas supprimer complètement un bot d’un contexte personnel. Si le bot est supprimé et ajouté à nouveau, une communication supplémentaire avec le bot est ajoutée à la conversation précédente.

## <a name="troubleshooting-notes"></a>Notes de dépannage

Si le manifeste ne parvient pas à se charger, vérifiez si vous avez suivi toutes les instructions dans Créer le [package](../../concepts/build-and-test/apps-package.md) et validé votre manifeste par rapport [au schéma](../../resources/schema/manifest-schema.md).
