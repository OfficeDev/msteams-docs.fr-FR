---
title: Prise en main de App Studio dans Microsoft Teams
description: Prise en main de la création de superbes applications dans Microsoft Teams à l’aide d’App Studio
keywords: mise en place d’app studio teams
ms.localizationpriority: medium
ms.topic: overview
ms.openlocfilehash: 92f24fbb7d4a41a192178ead1e2cb40dd7446b25
ms.sourcegitcommit: 781f34af2a95952bf437d0b7236ae995f4e14a08
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/12/2021
ms.locfileid: "60948634"
---
# <a name="manage-your-apps-with-app-studio-for-microsoft-teams"></a>Gérer vos applications avec App Studio pour Microsoft Teams

> [!TIP]
> **Essayez le portail du développeur**: App Studio a évolué. Configurez, distribuez et gérez vos applications Teams avec le nouveau [portail du développeur.](https://dev.teams.microsoft.com/)

App Studio vous permet de créer et d’intégrer facilement vos propres applications Microsoft Teams, que vous développiez des applications personnalisées pour votre entreprise ou des applications SaaS pour des équipes du monde entier, en rationalisant la création du manifeste et du package pour votre application et en fournissant des outils utiles comme l'éditeur de cartes et une bibliothèque de contrôle React.

> [!IMPORTANT]
> App Studio n’est actuellement pas disponible dans les types d’organisation Teams suivantes :
>
> * Government Community Cloud (GCC)
> * GCC High
> * DoD

## <a name="installing-app-studio"></a>Installation de App Studio

App Studio est une application Teams disponible dans la boutique Teams. Suivez ce lien pour télécharger directement [App Studio.](https://aka.ms/InstallTeamsAppStudio) Vous pouvez également trouver l’application dans l’App Store.

Dans le Store, recherchez App Studio.

![Entrée du Store pour App Studio](~/assets/images/get-started/storeteamsappstudio.png)

Sélectionnez la vignette App Studio pour ouvrir la page d’installation de l’application :

![Configurer de app studio](~/assets/images/get-started/teamsappstudioconfiguration.png)

Sélectionnez **Installer**.

![app studio](~/assets/images/get-started/teamsappstudio.png)

Une fois dans App Studio, cliquez sur l’onglet **Éditeur de manifeste** dans lequel vous pouvez importer une application existante ou créer une nouvelle application.

## <a name="app-studio-features"></a>Fonctionnalités d’App Studio

Cette section traite des fonctionnalités, telles que la conversation, l’éditeur de manifeste, les détails et les fonctionnalités. Vous pouvez personnaliser vos fonctionnalités à l’aide de la personnalisation de l’application.

### <a name="conversation"></a>Conversation

C’est l’endroit où vous pouvez voir à quoi ressemblent les [cartes de visite que vous créez dans App Studio](#card-editor) dans Teams lorsque vous les testez en les envoyant vous-même.

### <a name="manifest-editor"></a>Éditeur de manifeste

Comme indiqué précédemment, la partie la plus importante d’un package d’application Microsoft Teams est son fichier manifest.json. Ce fichier, qui doit être conforme au [schéma de l’application Teams](~/resources/schema/manifest-schema.md), contient des métadonnées qui permettent à Teams de présenter correctement votre application aux utilisateurs.

L’onglet Éditeur de manifeste dans App Studio simplifie la création du manifeste, ce qui vous permet de décrire l’application, de télécharger vos icônes, d’ajouter des fonctionnalités d’application et de créer un fichier .zip qui peut être facilement téléchargé dans Teams à des utilisateurs à des buts de test ou de distribution. Notez que App Studio ne produit pas de code fonctionnel pour votre application ou n’héberge pas votre application. Votre application doit déjà être hébergée et en cours d’exécution à l’URL répertoriée dans le manifeste pour que le processus de chargement de l’application aboutisse à une application fonctionnelle.

#### <a name="details"></a>Détails

La section détails de l’Éditeur de manifeste définit la description générale de l’application que vous êtes en train de réaliser. Notamment le nom, la description et l’image de marque de l’application. Vous pouvez générer automatiquement un GUID pour votre application et fournir des URL pour votre déclaration de confidentialité et vos conditions d’utilisation.

#### <a name="capabilities"></a>Fonctionnalités

La section Fonctionnalités de l'Éditeur de manifeste est l'endroit où les fonctionnalités de l'application sont définies et où les détails de chacune de ces fonctionnalités sont énumérés.

> [!NOTE]
> En tant que meilleure pratique, vous devez fournir des instructions de personnalisation que les utilisateurs et les clients de l’application doivent suivre lors de la personnalisation de votre application. Pour plus d’informations, voir [personnaliser les applications dans Microsoft Teams](/MicrosoftTeams/customize-apps).

##### <a name="tabs"></a>Onglets

* **Onglets d’équipe.** Un onglet d’équipe devient un canal et permet d’accéder rapidement aux informations et ressources de l’équipe. Par exemple, l’onglet Planificateur d’un canal contient un seul plan. L’onglet Power BI correspond à un rapport spécifique. Les utilisateurs peuvent explorer le contexte approprié, mais ils ne peuvent pas naviguer en dehors de l’onglet. Par exemple, l’onglet Power BI n’active pas la navigation vers les autres rapports Power BI, mais il active le bouton *Accéder au site web* qui lance le rapport dans le site web principal de Power BI.

  Pour les onglets d’équipe, vous devez fournir une *URL de configuration* pour présenter les options et collecter les informations nécessaires pour que les utilisateurs personnalisent le contenu et l’expérience de votre onglet. Cette page HTML iframée s’affiche lorsqu’un utilisateur ajoute l’onglet pour la première fois à un canal.

  Vous devez également fournir d'autres domaines à partir desquels l'onglet doit être chargé ou lié.

* **Onglets personnels.** Cette section vous permet de définir un ensemble d’onglets présentés par défaut dans l’expérience d’application personnelle (expérience dont dispose un utilisateur avec votre application en dehors du contexte d’une équipe ou d’un canal). Dans cette section, indiquez le nom de l’onglet, un identificateur unique, l’URL qui pointe vers l’interface utilisateur à afficher dans Teams et éventuellement l’URL à utiliser si un utilisateur choisit d’afficher l’onglet dans un navigateur. Avec Teams onglets, fournissez tous les domaines supplémentaires à partir des lesquels l’onglet s’attend à se charger ou à lier.

##### <a name="bots"></a>Bots

Cette section vous permet d’ajouter un [bot conversation](~/bots/what-are-bots.md) à votre application. Si vous avez déjà inscrit un bot auprès de Bot Framework, vous pouvez ajouter ce bot en cliquant sur *Configurer* et en fournissant le nom du bot, l’ID Bot Framework, et en définissant les étendues dans lesquelles le bot fonctionne.

Si vous n’avez pas encore inscrit un bot auprès de Bot Framework, cliquez sur **s'inscrire** pour en créer un autre. Une fois que vous avez inscrit votre bot, revenez à cette section de l’Éditeur manifeste pour entrer son nom et l’ID Bot Framework.

Une fois que vous avez fourni les informations de votre bot, vous pouvez éventuellement définir une liste de commandes que votre bot peut suggérer aux utilisateurs. Ajoutez le nom de la commande, une description de celle-ci qui indique sa syntaxe et ses arguments, ainsi que l’étendue à laquelle cette commande doit s’appliquer.

> [!NOTE]
> Si vous avez défini votre bot pour prendre en charge une seule étendue, les commandes spécifiées pour l’étendue non prise en charge sont ignorées. Vous pouvez modifier les étendues que votre bot prend en charge à tout moment.

##### <a name="connectors"></a>Connecteurs

Cette section vous permet d’ajouter un connecteur à votre application. Si vous avez déjà inscrit un connecteur Office 365, sélectionnez **Configurer** puis entrez le nom et l’ID du connecteur. Si vous voulez un nouveau connecteur, cliquez sur **S'inscrire** pour accéder au tableau de bord du développeur de connecteurs dans votre navigateur.

##### <a name="messaging-extensions"></a>Extensions de messagerie

[Les extensions de messagerie](~/messaging-extensions/what-are-messaging-extensions.md) sont un moyen puissant pour les utilisateurs de interagir avec votre application au sein de Microsoft Teams. Les utilisateurs peuvent interroger les informations de votre service et publier ces informations sous forme de cartes, directement dans le canal ou la conversation instantanée.

Les extensions de messagerie sont optimisées par des bots Bot Framework. Ils ont donc besoin d’un bot configuré pour opérer. Si vous avez le nom et l’ID Bot Framework du bot dont vous voulez power l’extension de messagerie, entrez-le. Sinon, cliquez sur **S'inscrire** pour en créer un, puis entrez les informations par la suite. Choisissez si la configuration d’une extension de messagerie peut être mise à jour par l’utilisateur.

Une fois le bot sous-jacent configuré, définissez les commandes et paramètres que l’extension de messagerie peut accepter.

Chaque commande nécessite un titre et un ID. La commande peut éventuellement contenir une description pour l’utilisateur. Chaque commande peut prendre en charge jusqu’à cinq paramètres, chacun d’eux nécessitant :

* Nom du paramètre tel qu’il apparaît dans Teams client et est inclus dans la demande de l’utilisateur.
* Titre convivial.
* Description facultative.

> [!NOTE]
> Pour créer une extension de messagerie à l’aide d’App Studio, voir créer une [extension de messagerie à l’aide d’app studio.](~/resources/create-messaging-extension-using-appstudio.md)

#### <a name="test-and-distribute"></a>Tester et distribuer

Une fois que vous avez fini de définir votre application, la section Tester et distribuer vous permet d’exporter la définition de votre application en tant que fichier zip, qui peut ensuite être partagé et téléchargé dans le client Teams à des moments de test. Cliquer sur Exporter télécharge le fichier zip sous *appname.zip* dans votre répertoire de téléchargement par défaut.

##### <a name="publish-your-app-to-teams"></a>Publier votre application sur Teams
Sur la page d’accueil de votre projet, vous pouvez télécharger votre application dans une équipe, l’envoyer sur le magasin d’applications personnalisé de votre entreprise pour les utilisateurs de votre organisation ou envoyer votre application à la source de l’application pour tous les utilisateurs Teams. Votre administrateur informatique examine ces envois. Vous pouvez revenir à la page *Publier* pour vérifier l’état de votre envoi et savoir si votre application a été approuvée ou refusée par votre administrateur informatique. C’est également ici que vous pouvez envoyer des mises à jour à votre application ou annuler les envois en cours.

### <a name="card-editor"></a>Éditeur de carte

Une carte est un conteneur pour des éléments d’informations courts ou associés. Microsoft Teams prend en charge les cartes, qui peuvent avoir plusieurs propriétés et pièces jointes. Les cartes sont un moyen clé pour les bots et les connecteurs de relayer des informations utilisables pour les utilisateurs. 

Pour faciliter ce processus et réduire les risques d’erreur, l’onglet Éditeur de cartes vous permet de créer des cartes Hero ou des cartes miniatures à l’aide d’un formulaire, ainsi que de vérifier et de tester la carte résultante (exactement comme l’aurait vu un utilisateur) via un bot. Elle fournit également le code JSON, C# ou Node.js correspondant pour la carte que vous pouvez copier/coller dans le code source de votre application.

Si vous avez déjà une carte que vous voulez vérifier dans Teams, vous pouvez coller le JSON de cette carte dans l’onglet JSON sous *Ajouter des informations de carte* et vous les envoyer pour voir à quoi celle-ci ressemble dans une conversation.

### <a name="react-control-library"></a>Bibliothèque de contrôles React

>[!Note]
> Cet React bibliothèque de contrôles est bientôt supprimé. Envisagez [d’utiliser Fluent des](https://microsoft.github.io/fluent-ui-react/) contrôles react de l’interface utilisateur utilisateur en tant qu’autre interface utilisateur Stardust précédemment.

La création d’une application qui suit les meilleures pratiques de Teams est un excellent moyen de donner à votre application une apparence qui s’adapte parfaitement à l’expérience cliente de Teams. Les contrôles d’interface utilisateur sont essentiels pour atteindre cet objectif. Pour simplifier la création d’une interface utilisateur cohérente, App Studio fournit plusieurs catégories de contrôles d’interface utilisateur qui suivent les principes de conception de Teams.

Des exemples de contrôles et de composants React correspondants sont fournis et prêts à être utilisés pour la création de votre application.

#### <a name="controls"></a>Contrôles

Les contrôles incluent :

* Boutons
* Listes déroulantes
* Cases à cocher
* Cases d’option
* Bascule
* Zones de texte
* Liens
* Onglets
* Tables
* Icônes

## <a name="see-also"></a>Voir aussi

[Gérer vos applications avec le Portail des développeurs pour Microsoft Teams](~/concepts/build-and-test/teams-developer-portal.md)