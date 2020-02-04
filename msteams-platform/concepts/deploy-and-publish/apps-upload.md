---
title: Charger votre application personnalisée dans Microsoft teams
description: Décrit comment télécharger votre application dans Microsoft teams
keywords: Téléchargement d’applications teams
ms.openlocfilehash: b5807644a0c9afa26b81d07c71d5f45ab3c8ba00
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673632"
---
# <a name="upload-an-app-package-to-microsoft-teams"></a>Téléchargement d’un package d’application dans Microsoft Teams

Pour tester l’expérience de votre application dans Microsoft Teams, vous devez charger votre application dans Teams. Le téléchargement ajoute l’application à l’équipe que vous sélectionnez, et vous et les membres de votre équipe pouvez interagir avec elle comme les utilisateurs finaux.

> [!NOTE]
> Le téléchargement d’un package mis à jour pour une application existante avec un bot peut ne pas afficher les changements d’onglet lorsqu’ils sont affichés dans la fenêtre de conversation. Il est préférable d’y accéder via la fonction fly-out des applications ou de tester un environnement de test propre.

## <a name="create-your-upload-package"></a>Créer votre package de téléchargement

Pour le développement et l’envoi AppSource (anciennement Office Store), vous devez créer un package pouvant être chargé contenant les informations pour décrire votre expérience. Le package, un fichier. zip, contient le manifeste de l’application et des icônes qui définissent votre expérience de manière unique.

Pour créer un package de téléchargement, voir [créer le package pour votre application Microsoft teams](~/concepts/build-and-test/apps-package.md).

Une fois votre package créé, vous pouvez le charger dans une équipe. Une fois téléchargée, elle est disponible pour tous les utilisateurs de l’équipe sélectionnée et uniquement les utilisateurs de cette équipe.

## <a name="load-your-package-into-teams"></a>Charger votre package dans teams

Vous pouvez tester votre package en le téléchargeant dans Teams.

> [!NOTE]
> Pour que le chargement fonctionne, votre administrateur client doit d’abord [activer le téléchargement des applications](/microsoftteams/admin-settings).

Il existe deux façons de charger votre application dans teams :

* Utilisation de la Banque
* Utilisation de l’onglet applications

## <a name="upload-your-package-into-a-team-or-conversation-using-the-store"></a>Charger votre package dans une équipe ou une conversation à l’aide de la Banque

1. Dans le coin inférieur gauche de teams, sélectionnez l’icône Store. Sur la page Store, choisissez « Télécharger une application personnalisée ».

   ![Afficher l’équipe](~/assets/images/store-upload-a-custom-app.png)

2. Dans la boîte de dialogue *ouvrir* , accédez au package à télécharger, puis choisissez *ouvrir*.

Le package téléchargé doit maintenant être disponible pour une utilisation dans l’équipe ou la conversation spécifiée dans la boîte de dialogue de consentement. Si votre application ne s’affiche pas, la cause la plus fréquente est une erreur dans le manifeste, en particulier les ID pour les extensions App, bot et Messaging. Si l’application n’est pas étendue pour les conversations, cette option n’apparaît pas.

>[!NOTE]
> Les applications dans les conversations sont actuellement en version préliminaire pour les [développeurs](~/resources/dev-preview/developer-preview-intro.md)et l’option ne s’affiche pas si teams n’est pas en cours d’exécution dans ce mode.

![Exemple de bot dans la liste des robots téléchargés](~/assets/images/botinlist.jpg)

## <a name="upload-your-package-into-a-team-using-the-apps-tab"></a>Charger votre package dans une équipe à l’aide de l’onglet applications

1. Dans l’équipe cible, sélectionnez *plus d’options* (**&#8943;**) et sélectionnez *gérer l’équipe*.

   > [!NOTE]
   > Vous devez être le propriétaire de l’équipe, ou le propriétaire doit autoriser les utilisateurs à ajouter les types d’application appropriés pour que cette fonctionnalité apparaisse.

2. Sélectionnez l’onglet applications, puis *Télécharger une application personnalisée* dans la partie inférieure droite.

   ![Télécharger le point d’entrée](~/assets/images/uploadACustomApp.png)

3. Naviguez jusqu’à votre package. zip et sélectionnez-le sur votre ordinateur.

4. Après une brève pause, vous verrez votre application téléchargée dans la liste.

   ![Exemple de bot dans la liste des robots téléchargés](~/assets/images/botinlist.jpg)

Si votre application ne se charge pas, la cause la plus fréquente est une erreur dans le manifeste, en particulier les ID pour les extensions App, bot et Messaging.

## <a name="accessing-your-uploaded-configurable-tab"></a>Accès à votre onglet configurable chargé

Si l’application contient des onglets, les utilisateurs peuvent les épingler à n’importe quelle conversation ou canal d’équipe à l’aide du flux de Galerie d’onglets standard :

1. Accéder à un canal dans l’équipe. Choisissez *+* (*Ajouter un onglet*) à droite des onglets existants.

2. Sélectionnez votre onglet dans la galerie qui s’affiche.

3. Acceptez l’invite de consentement.

4. Configurez votre onglet par le biais de sa [page de configuration](~/tabs/how-to/create-tab-pages/configuration-page.md) , puis choisissez *Enregistrer*.

  ![Boîte de dialogue Ajouter un onglet, comprenant une galerie des onglets disponibles](~/assets/images/tab_gallery.png)

## <a name="accessing-your-uploaded-bot"></a>Accès à votre bot chargé

Lorsque vous ajoutez un bot à une équipe, il doit pouvoir être utilisé par tous les utilisateurs de cette équipe, à l’intérieur et à l’extérieur des canaux de l’équipe, en fonction de la définition de l’étendue du bot. Vous et les autres membres de l’équipe verrez un billet dans le canal général indiquant que le bot a été ajouté à l’équipe.

Pour un robot compatible Teams, vous pouvez commencer par appeler votre bot en @mentioning le nom du bot, qui doit se terminer de manière automatique.

Pour tester les conversations directes avec votre robot, vous pouvez y accéder via la page d’accueil de l’application, le @mention dans un canal ou le Rechercher dans la nouvelle fenêtre de **conversation** .

Lorsque vous ajoutez votre bot à une conversation pour tester les conversations directes avec votre robot, vous pouvez le @mention dans une conversation ou le Rechercher dans la nouvelle fenêtre de **conversation** .

## <a name="accessing-your-uploaded-connector"></a>Accès à votre connecteur téléchargé

Une fois l’application chargée dans l’équipe ou la conversation, les utilisateurs peuvent configurer un connecteur à l’aide du flux de Galerie de connecteurs standard :

1. Accéder à un canal dans l’équipe. Sélectionnez *plus d’options* (*&#8943;*) et choisissez *connecteurs*.

2. Sélectionnez votre connecteur dans la section **chargé** en bas.

3. Configurez votre connecteur via sa [page de configuration](~/webhooks-and-connectors/how-to/connectors-creating.md) et sélectionnez *Enregistrer*.

  ![La boîte de dialogue Ajouter un onglet, qui propose une galerie des onglets disponibles.](~/assets/images/connector_gallery.png)

## <a name="accessing-your-uploaded-messaging-extension"></a>Accès à votre extension de messagerie chargée

Une application téléchargée avec une extension de messagerie apparaît automatiquement dans le menu *plus d’options* (*&#8943;*) de la zone de composition.

![Extensions de messagerie](~/assets/images/compose-extensions/cesampleapp.png)

## <a name="removing-or-updating-your-app"></a>Suppression ou mise à jour de votre application

Si vous souhaitez supprimer votre application, sélectionnez l’icône de la Corbeille en regard du nom de l’application dans la liste afficher les bots de teams.

Si vous modifiez les informations de manifeste, vous devez d’abord supprimer l’application, puis ajouter le package mis à jour (par [chargez votre package dans une équipe](#load-your-package-into-teams)). Notez que, en règle générale, les modifications apportées au code de votre service ne nécessitent pas le chargement de votre manifeste, sauf si ces modifications nécessitent des mises à jour du manifeste (telles que les modifications apportées à l’URL ou l’ID de l’application Microsoft pour son bot).

> [!NOTE]
> Il n’existe aucun moyen de supprimer complètement un bot du contexte personnel. Si le bot est supprimé et ajouté de nouveau, une communication supplémentaire avec le bot est ajoutée à la conversation précédente.

## <a name="troubleshooting-notes"></a>Remarques sur la résolution des problèmes

* Si le manifeste ne se charge pas, vérifiez que vous avez suivi toutes les instructions de [Create the package](~/concepts/build-and-test/apps-package.md) et validé votre manifeste par rapport au [schéma](~/resources/schema/manifest-schema.md).

