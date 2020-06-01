---
title: Prise en main d’App Studio pour Microsoft teams
description: Commencer à créer des applications intéressantes dans Microsoft teams à l’aide d’App Studio
keywords: mise en route de teams App Studio
ms.date: 03/20/2019
ms.openlocfilehash: 3d6274c204f907bdff19d1b0b9f347414423f2f5
ms.sourcegitcommit: 61c93b22490526b1de87c0b14a3c7eb6e046caf6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/31/2020
ms.locfileid: "44453860"
---
# <a name="quickly-develop-apps-with-app-studio-for-microsoft-teams"></a>Développer rapidement des applications avec App Studio pour Microsoft teams

App Studio facilite la création ou l’intégration de vos propres applications Microsoft Teams, que vous développiez des applications personnalisées pour vos applications d’entreprise ou SaaS pour teams dans le monde entier en rationalisant la création du manifeste et du package pour votre application et en fournissant des outils utiles tels que l’éditeur de carte et une bibliothèque de contrôle REACT.

## <a name="installing-app-studio"></a>Installation d’App Studio

App Studio est une application de teams qui se trouve dans le Store Teams. Suivez ce lien pour télécharger directement : [app Studio](https://aka.ms/InstallTeamsAppStudio) (vous pouvez également trouver l’application dans le magasin d’applications).

Dans le Store, recherchez App Studio.

![Entrée de magasin pour App Studio](~/assets/images/get-started/storeteamsappstudio.png)

Sélectionnez la vignette App Studio pour ouvrir la page d’installation de l’application :

![Configurer App Studio](~/assets/images/get-started/teamsappstudioconfiguration.png)

Sélectionnez *installer*.

![App Studio](~/assets/images/get-started/teamsappstudio.png)

Une fois que vous êtes dans l’application Studio, cliquez sur l’onglet *éditeur de manifeste* où vous pouvez importer une application existante ou créer une application.

## <a name="app-studio-features"></a>Fonctionnalités d’App Studio

### <a name="conversation"></a>Conversation

C’est ici que vous pouvez voir les [cartes que vous créez dans App Studio](#card-editor) dans teams lorsque vous les testez en les envoyant à vous-même.

### <a name="manifest-editor"></a>Éditeur de manifeste

Comme indiqué précédemment, la partie la plus significative d’un package d’application Microsoft teams est son fichier manifest. JSON. Ce fichier, qui doit être conforme au [schéma d’application de teams](~/resources/schema/manifest-schema.md), contient des métadonnées qui permettent à teams de présenter correctement votre application aux utilisateurs.

L’onglet Éditeur de manifeste dans App Studio simplifie la création du manifeste, ce qui vous permet de décrire l’application, de télécharger vos icônes, d’ajouter des fonctionnalités d’application et de produire un fichier. zip pouvant facilement être téléchargé dans teams à des fins de test ou distribué à d’autres personnes. Notez que l’application Studio ne produit pas de code fonctionnel pour votre application ou héberge votre application. Votre application doit déjà être hébergée et en cours d’exécution à l’URL répertoriée dans le manifeste pour que le processus de chargement d’application se traduit par une application de travail.

#### <a name="details"></a>Détails

La section Détails de l’éditeur de manifeste définit la description de haut niveau de l’application que vous effectuez. Cela inclut des éléments tels que le nom, la description et la personnalisation visuelle de l’application. Vous pouvez générer automatiquement un GUID pour votre application et fournir des URL pour votre déclaration de confidentialité et les conditions d’utilisation.

#### <a name="capabilities"></a>Fonctionnalités

La section des fonctionnalités de l’éditeur de manifeste est l’endroit où les fonctionnalités de l’application sont définies et où les détails de chacune de ces fonctionnalités sont répertoriés.

##### <a name="tabs"></a>Onglets

* **Onglets équipe.** Un onglet équipe fait partie d’un canal et permet d’accéder rapidement aux informations et aux ressources de l’équipe. Par exemple, l’onglet planificateur d’un canal contient un seul plan ; l’onglet Power BI est mappé à un rapport spécifique. Les utilisateurs peuvent accéder au contexte approprié, mais ils ne doivent pas pouvoir naviguer à l’extérieur de l’onglet. L’onglet Power BI, par exemple, ne permet pas la navigation vers d’autres rapports Power BI, mais il active le bouton *accéder au site Web* qui lance le rapport dans le site Web Power bi principal.

  Pour les onglets d’équipe, vous devez fournir une *URL de configuration* pour présenter les options et collecter des informations afin que les utilisateurs puissent personnaliser le contenu et l’expérience de votre onglet. Cette page HTML iframe est affichée lorsqu’un utilisateur ajoute l’onglet à un canal pour la première fois.

  Vous devez également fournir les domaines supplémentaires à partir desquels le chargement ou la liaison doit être lié à l’onglet.

* **Onglets personnels.** Cette section vous permet de définir un ensemble d’onglets qui sont présentés par défaut dans l’expérience de l’application personnelle (par exemple, l’expérience qu’a un utilisateur avec votre application en dehors du contexte d’une équipe ou d’un canal). Dans cette section, indiquez le nom de l’onglet, un identificateur unique, l’URL qui pointe vers l’interface utilisateur à afficher dans Teams, et éventuellement l’URL à utiliser si un utilisateur choisit d’afficher l’onglet dans un navigateur. Comme avec les onglets Teams, fournissez tous les domaines supplémentaires à partir desquels le chargement de l’onglet est prévu ou lié.

##### <a name="bots"></a>Bots

Cette section vous permet d’ajouter un [bot de conversation](~/bots/what-are-bots.md) à votre application. Si vous avez déjà un bot enregistré avec bot Framework, vous pouvez l’ajouter en cliquant sur *configurer* et en fournissant le nom du bot, l’ID de l’infrastructure bot et en définissant les étendues dans lesquelles le bot fonctionnera.

Si vous n’avez pas encore enregistré de robot avec l’infrastructure de robot, cliquez sur *Enregistrer* pour en créer un nouveau. Une fois que vous avez fini d’inscrire votre robot, revenez à cette section de l’éditeur de manifeste pour entrer son nom et son ID d’infrastructure de robot.

Une fois que vous avez fourni les informations de votre robot, vous pouvez définir éventuellement une liste de commandes que votre bot peut suggérer aux utilisateurs. Ajoutez le nom de la commande, une description de la commande qui indique sa syntaxe et ses arguments, ainsi que la ou les étendues auxquelles cette commande doit s’appliquer.

Notez que si vous avez défini votre bot de sorte qu’il ne prenne en charge qu’une seule étendue, les commandes spécifiées pour l’étendue non prise en charge seront ignorées. Vous pouvez modifier les étendues que votre robot prend en charge à tout moment.

##### <a name="connectors"></a>Connecteurs

Cette section vous permet d’ajouter un connecteur à votre application. Si vous avez déjà inscrit un connecteur Office 365, sélectionnez *configurer* , puis entrez le nom et l’ID du connecteur. Si vous souhaitez qu’un nouveau connecteur clique sur *inscrire* dans le tableau de bord du développeur connecteur dans votre navigateur.

##### <a name="messaging-extensions"></a>Extensions de messagerie

Les [extensions de messagerie](~/messaging-extensions/what-are-messaging-extensions.md) sont un moyen efficace pour les utilisateurs de s’engager avec votre application dans Microsoft Teams. Les utilisateurs peuvent demander des informations à votre service et publier ces informations sous la forme de cartes, directement dans la conversation de canal ou de conversation.

Les extensions de messagerie sont gérées par les robots de l’infrastructure bot, de sorte qu’ils nécessitent un bot configuré pour fonctionner. Si vous avez le nom et l’ID de l’infrastructure de bot du bot sur lequel vous souhaitez alimenter l’extension de messagerie, entrez-le. Dans le cas contraire, cliquez sur *Enregistrer* pour en créer un et entrez les informations par la suite. Indiquez si la configuration d’une extension de messagerie peut être mise à jour par l’utilisateur.

Une fois que le bot sous-jacent est configuré, définissez les commandes et les paramètres que l’extension de messagerie peut accepter.

Chaque commande nécessite un titre et un ID. La commande peut éventuellement contenir une description pour l’utilisateur. Chaque commande peut prendre en charge jusqu’à cinq paramètres, chacun d’entre eux nécessitant :

* Le nom du paramètre tel qu’il apparaît dans le client teams et est inclus dans la demande de l’utilisateur.
* Titre convivial
* Description facultative

#### <a name="test-and-distribute"></a>Test et distribution

Une fois que vous avez terminé la définition de votre application, la section test et distribution vous permet d’exporter la définition de votre application sous la forme d’un fichier zip, qui peut ensuite être partagé et téléchargé dans le client teams à des fins de test. Si vous cliquez sur Exporter, le fichier zip est téléchargé en tant que *appname. zip* dans le répertoire de téléchargement par défaut.

### <a name="card-editor"></a>Éditeur de carte

Une carte est un conteneur pour des informations courtes ou associées. Microsoft teams prend en charge les cartes, qui peuvent avoir plusieurs propriétés et pièces jointes. Les cartes sont une façon dont les robots et les connecteurs relaient les informations exploitables aux utilisateurs. 

Pour simplifier ce processus et réduire les risques d’erreurs, l’onglet Éditeur de carte vous permet de créer des cartes de héros ou des cartes miniatures à l’aide d’un formulaire et de vérifier et tester la carte obtenue (exactement comme un utilisateur le verrait) via un bot. Il fournit également le code JSON, C# ou node. js correspondant pour la carte que vous pouvez copier/coller dans le code source de votre application.

Si vous disposez déjà d’une carte que vous souhaitez vérifier dans Teams, vous pouvez coller le JSON de cette carte dans l’onglet JSON sous *Ajouter des informations* sur la carte et vous l’envoyer à vous-même pour voir à quoi il ressemble dans une conversation.

### <a name="react-control-library"></a>Bibliothèque de contrôle REACT

>[!Note]
> Cette bibliothèque de contrôle REACT sera déconseillée à l’avenir. Envisagez [d’utiliser les contrôles Fluent-UI REACT comme alternative](https://microsoft.github.io/fluent-ui-react/) (anciennement Stardust UI).

La création d’une application qui suit les meilleures pratiques de teams est un excellent moyen de donner à votre application un aspect adapté à l’expérience client de teams. Les contrôles de l’interface utilisateur que vous utilisez sont essentiels pour atteindre cette fin. Pour faciliter la création d’une interface utilisateur cohérente, app Studio fournit plusieurs catégories de contrôles d’interface utilisateur qui suivent les principes de conception de teams.

Des exemples de contrôles et de composants REACT correspondants sont fournis et prêts à être utilisés dans la création de votre application.

#### <a name="controls"></a>Contrôles

Les contrôles sont les suivants :

* Boutons
* Listes déroulantes
* Cases à cocher
* Cases d’option
* Inverser
* Zones de texte
* Liens
* Onglets
* Tables
* Icônes
