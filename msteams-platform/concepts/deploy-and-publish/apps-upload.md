---
title: Télécharger votre application personnalisée
description: Décrit comment télécharger votre application dans Microsoft Teams
ms.topic: how-to
keywords: Téléchargement d’applications Teams
ms.openlocfilehash: 2e7a21dc27fdfe824ecacebabbb61a3b99ae8e79
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014340"
---
# <a name="upload-an-app-package-to-microsoft-teams"></a>Téléchargement d’un package d’application dans Microsoft Teams

Pour tester votre expérience d’application dans Microsoft Teams, vous devez télécharger votre application dans Teams. Le téléchargement ajoute l’application à l’équipe que vous sélectionnez, et vous et les membres de votre équipe pouvez interagir avec elle comme les utilisateurs finaux.

> [!NOTE]
> Le téléchargement d’un package mis à jour pour une application existante à l’aide d’un bot peut ne pas afficher les modifications apportées aux onglets lorsqu’il est vu dans la fenêtre Conversations. Il est préférable d’y accéder via le volant Applications ou de tester dans un environnement de test propre.

## <a name="create-your-upload-package"></a>Créer votre package de chargement

Pour le développement, ainsi que pour la soumission d’AppSource (anciennement Office Store), vous devez créer un package téléchargeable qui contient les informations pour décrire votre expérience. Le package, un fichier .zip, contient le manifeste de l’application et les icônes qui définissent votre expérience de manière unique.

Pour créer un package de chargement, voir [Créer le package pour votre application Microsoft Teams.](../build-and-test/apps-package.md)

Une fois votre package créé, vous pouvez désormais le télécharger dans une équipe. Une fois téléchargé, il sera disponible pour tous les utilisateurs de l’équipe sélectionnée, et uniquement pour les utilisateurs de cette équipe.

## <a name="load-your-package-into-teams"></a>Charger votre package dans Teams

Vous pouvez tester votre package en le téléchargeant dans Teams.

> [!NOTE]
> Pour que le chargement fonctionne, votre administrateur client doit d’abord [activer le téléchargement d’applications.](/microsoftteams/admin-settings)

Il existe deux façons de télécharger votre application dans Teams :

* Utilisation du Store
* Utilisation de l’onglet Applications

## <a name="upload-your-package-into-a-team-or-conversation-using-the-store"></a>Charger votre package dans une équipe ou une conversation à l’aide du Store

1. Dans le coin inférieur gauche de Teams, sélectionnez l’icône du Store. Dans la page Du Store, choisissez « Télécharger une application personnalisée ».

  ![Afficher l’équipe](../../assets/images/store-upload-a-custom-app2.png)

2. Dans la *boîte de dialogue* Ouvrir, accédez au package que vous souhaitez télécharger et choisissez *Ouvrir.*

   ![Menu Ajouter](../../assets/images/NewappAddmenudropdown.png)

Le package téléchargé doit maintenant être disponible pour une utilisation dans l’équipe ou la conversation spécifiée dans la boîte de dialogue de consentement. Si votre application n’apparaît pas, la raison la plus courante est une erreur dans le manifeste, en particulier les ID de l’application, du bot et des extensions de messagerie. Si l’application n’est pas limitée aux conversations, cette option n’apparaît pas.

>[!NOTE]
> Les applications des conversations sont actuellement en prévisualisation du développeur [et](../../resources/dev-preview/developer-preview-intro.md)l’option n’apparaît pas si Teams n’est pas en cours d’exécution dans ce mode.

![Exemple de bot dans la liste des bots téléchargés](../../assets/images/botinlist.jpg)

## <a name="upload-your-package-into-a-team-using-the-apps-tab"></a>Télécharger votre package dans une équipe à l’aide de l’onglet Applications

1. Dans l’équipe cible, choisissez *Plus d’options* (**&#8943;**) et choisissez *Gérer l’équipe*.

   > [!NOTE]
   > Vous devez être le propriétaire de l’équipe ou autoriser les utilisateurs à ajouter les types d’applications appropriés pour que cette fonctionnalité apparaisse.

2. Sélectionnez l’onglet Applications, puis choisissez *Télécharger une application personnalisée* en bas à droite.

   ![Point d’entrée de chargement](../../assets/images/UploadACustomApp.png)

3. Accédez à votre package .zip et sélectionnez-le à partir de votre ordinateur.

4. Après une courte pause, vous verrez votre application téléchargée dans la liste.

   ![Exemple de bot dans la liste des bots téléchargés](../../assets/images/botinlist.jpg)

Si votre application ne se charge pas, la raison la plus courante est une erreur dans le manifeste, en particulier les ID de l’application, du bot et des extensions de messagerie.

## <a name="accessing-your-uploaded-configurable-tab"></a>Accès à votre onglet configurable téléchargé

Si l’application contient des onglets, les utilisateurs peuvent les épingler à n’importe quel canal de conversation ou d’équipe à l’aide du flux de galerie d’onglets standard :

1. Go to a channel in the team. Choisissez *+* ( Ajouter un *onglet*) à droite des onglets existants.

2. Sélectionnez votre onglet dans la galerie qui s’affiche.

3. Acceptez l’invite de consentement.

4. Configurez votre onglet via sa [page de configuration](../../tabs/how-to/create-tab-pages/configuration-page.md) et choisissez *Enregistrer.*

  ![Boîte de dialogue Ajouter un onglet, avec une galerie d’onglets disponibles](../../assets/images/tab_gallery.png)

## <a name="accessing-your-uploaded-bot"></a>Accès à votre bot téléchargé

Lorsque vous ajoutez un bot à une équipe, il doit être utilisable par toute personne de cette équipe, à l’intérieur et à l’extérieur des canaux de l’équipe, en fonction de la définition de l’étendue du bot. Vous et les autres membres de l’équipe verrez un billet dans le canal général indiquant que le bot a été ajouté à l’équipe.

Pour un bot activé pour teams, vous pouvez commencer par l’appel de votre bot en @mentioning le nom du bot, qui doit être automatiquementcomplémenté.

Pour tester les conversations directes avec votre bot, vous pouvez y accéder via la page d’accueil de l’application, l'@mention dans un canal ou la rechercher dans la **fenêtre Nouvelle** conversation.

Lorsque vous ajoutez votre bot à une conversation pour tester les conversations directes avec votre bot, vous pouvez le @mention dans une conversation ou le rechercher dans la **fenêtre Nouvelle** conversation.

## <a name="accessing-your-uploaded-connector"></a>Accès à votre connecteur téléchargé

Une fois l’application chargée dans l’équipe ou la conversation, les utilisateurs peuvent configurer un connecteur à l’aide du flux de galerie connecteurs standard :

1. Go to a channel in the team. Choose *More options* (*&#8943;*) and choose *Connectors*.

2. Sélectionnez votre connecteur dans la section **Sideloaded** en bas.

3. Configurez votre connecteur via sa [page de configuration](../../webhooks-and-connectors/how-to/connectors-creating.md) et choisissez *Enregistrer.*

  ![Boîte de dialogue Ajouter un onglet, avec une galerie d’onglets disponibles.](../../assets/images/connector_gallery.png)

## <a name="accessing-your-uploaded-messaging-extension"></a>Accès à votre extension de messagerie téléchargée

Une application téléchargée avec une extension de messagerie apparaît automatiquement dans le menu Plus *d’options* (*&#8943;*) dans la zone de composition.

![Extensions de messagerie](../../assets/images/compose-extensions/cesampleapp.png)

## <a name="removing-or-updating-your-app"></a>Suppression ou mise à jour de votre application

Si vous souhaitez supprimer votre application, sélectionnez l’icône de corbeille en regard du nom de l’application dans la liste Afficher les bots Teams.

Si vous modifiez les informations de manifeste, vous devez d’abord supprimer l’application, puis ajouter le package mis à jour (par chargement de [votre package dans une équipe).](#load-your-package-into-teams) Notez que, en règle générale, les modifications de code sur votre service ne vous obligent pas à télécharger à nouveau votre manifeste, sauf si ces modifications nécessitent des mises à jour de manifeste (telles que les modifications apportées à l’URL ou à l’ID de l’application Microsoft pour son bot).

> [!NOTE]
> Il n’existe aucun moyen de supprimer complètement un bot d’un contexte personnel. Si le bot est supprimé et ré-ajouté, une communication supplémentaire avec le bot est ajoutée à la conversation précédente.

## <a name="troubleshooting-notes"></a>Notes de dépannage

* Si le manifeste ne se charge pas, vérifiez que vous avez suivi toutes les instructions dans Créer le [package](../../concepts/build-and-test/apps-package.md) et validé votre manifeste par rapport [au schéma.](../../resources/schema/manifest-schema.md)
