---
title: Prise en main de App Studio dans Microsoft Teams
description: Dans cet article, vous allez apprendre à créer et gérer vos applications avec App Studio pour Microsoft Teams et l’installation d’App Studio.
ms.localizationpriority: medium
ms.topic: overview
ms.openlocfilehash: cf9f4a144886c67b2c2c667683d62a65fc4ee9c4
ms.sourcegitcommit: e429131d01df7103a467df2c42cdfe41ab822b10
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/20/2022
ms.locfileid: "66164268"
---
# <a name="manage-your-apps-with-app-studio-for-microsoft-teams"></a>Gérer vos applications avec App Studio pour Microsoft Teams

> [!WARNING]
> **Essayez le portail des développeurs** : App Studio a évolué. Configurez, distribuez et gérez vos applications Teams avec la nouvelle [Developer Portal](https://dev.teams.microsoft.com/). <br> App Studio sera déconseillé d’ici le 30 juin 2022.

App Studio vous permet de créer et d’intégrer facilement vos propres applications Microsoft Teams, que vous développiez des applications personnalisées pour votre entreprise ou des applications SaaS pour des équipes du monde entier, en rationalisant la création du manifeste et du package pour votre application et en fournissant des outils utiles comme l'éditeur de cartes et une bibliothèque de contrôle React.

> [!IMPORTANT]
> App Studio n’est actuellement pas disponible dans les types d’organisations Teams suivants :
>
> * Government Community Cloud (GCC)
> * GCC High
> * DoD

## <a name="installing-app-studio"></a>Installation de App Studio

App Studio est une application Teams, qui se trouve dans le magasin Teams. Suivez ce lien pour télécharger directement [App Studio](https://aka.ms/InstallTeamsAppStudio). Vous pouvez également trouver l’application dans l’App Store.

Dans le Store, recherchez App Studio.

:::image type="content" source="../../assets/images/get-started/StoreTeamsAppStudio.png" alt-text="Entrée du Store pour App Studio":::

Sélectionnez la vignette App Studio pour ouvrir la page d’installation de l’application :

:::image type="content" source="../../assets/images/get-started/teamsAppStudioConfiguration.png" alt-text="Configurer de app studio":::

Sélectionnez **Installer**.

:::image type="content" source="../../assets/images/get-started/TeamsAppStudio.png" alt-text="app studio":::

Une fois que vous êtes dans App Studio, sélectionnez l’onglet **Éditeur de manifeste** dans lequel vous pouvez importer une application existante ou créer une application.

## <a name="app-studio-features"></a>Fonctionnalités d’App Studio

Cette section couvre les fonctionnalités, telles que la conversation, l’éditeur de manifeste, les détails et les fonctionnalités. Vous pouvez personnaliser vos fonctionnalités à l’aide de la personnalisation de l’application.

### <a name="conversation"></a>Conversation

C’est l’endroit où vous pouvez voir à quoi ressemblent les [cartes de visite que vous créez dans App Studio](#card-editor) dans Teams lorsque vous les testez en les envoyant vous-même.

### <a name="manifest-editor"></a>Éditeur de manifeste

Comme mentionné précédemment, la partie la plus importante d’un package d’application Teams est son fichier manifest.json. Ce fichier, qui doit être conforme au [schéma d’application Teams](~/resources/schema/manifest-schema.md), contient des métadonnées, ce qui permet à Teams de présenter correctement votre application aux utilisateurs.

L’onglet Éditeur de manifeste d’App Studio simplifie la création du manifeste, ce qui vous permet de décrire l’application, de charger vos icônes, d’ajouter des fonctionnalités d’application et de produire un fichier .zip, qui peut facilement être chargé dans Teams à des fins de test ou distribué à d’autres utilisateurs. App Studio ne produit pas de code fonctionnel pour votre application, ni n’héberge votre application. Votre application doit déjà être hébergée et en cours d’exécution à l’URL répertoriée dans le manifeste pour que le processus de chargement de l’application aboutisse à une application fonctionnelle.

#### <a name="details"></a>Détails

La section Détails de l’Éditeur de manifeste définit la description générale de l’application que vous créez. Notamment le nom, la description et l’image de marque de l’application. Vous pouvez générer automatiquement un GUID pour votre application et fournir des URL pour votre déclaration de confidentialité et vos conditions d’utilisation.

#### <a name="capabilities"></a>Fonctionnalités

La section Fonctionnalités de l'Éditeur de manifeste est l'endroit où les fonctionnalités de l'application sont définies et où les détails de chacune de ces fonctionnalités sont énumérés.

> [!NOTE]
> En guise de bonne pratique, vous devez fournir des instructions de personnalisation aux utilisateurs et aux clients de l’application à suivre lors de la personnalisation de votre application. Pour plus d’informations, consultez [personnaliser les applications dans Microsoft Teams](/MicrosoftTeams/customize-apps).

##### <a name="tabs"></a>Onglets

* **Onglets d’équipe.** Un onglet d’équipe devient un canal et permet d’accéder rapidement aux informations et ressources de l’équipe. Par exemple, l’onglet Planificateur d’un canal contient un seul plan. L’onglet Power BI correspond à un rapport spécifique. Les utilisateurs peuvent accéder au contexte approprié, mais ils ne doivent pas pouvoir naviguer en dehors de l’onglet. L’onglet Power BI, par exemple, n’active pas la navigation vers d’autres rapports Power BI, mais il active le bouton *Accéder au site web* qui lance le rapport dans le site web principal Power BI.

  Pour les onglets d’équipe, vous devez fournir une *URL de configuration* pour présenter les options et collecter les informations nécessaires pour que les utilisateurs personnalisent le contenu et l’expérience de votre onglet. Cette page HTML iframée s’affiche lorsqu’un utilisateur ajoute l’onglet pour la première fois à un canal.

  Vous devez également fournir d'autres domaines à partir desquels l'onglet doit être chargé ou lié.

* **Onglets personnels.** Vous pouvez définir un ensemble d’onglets qui sont présentés par défaut dans l’expérience d’application personnelle (expérience qu’un utilisateur a avec votre application en dehors du contexte d’une équipe ou d’un canal). Dans cette section, indiquez le nom de l’onglet, un identificateur unique, l’URL qui pointe vers l’interface utilisateur à afficher dans Teams et éventuellement l’URL à utiliser si un utilisateur choisit d’afficher l’onglet dans un navigateur. Avec Teams onglets, fournissez tous les domaines supplémentaires à partir desquels l’onglet s’attend à être chargé ou vers lesquels établir un lien.

##### <a name="bots"></a>Bots

Cette section vous permet d’ajouter un [bot conversation](~/bots/what-are-bots.md) à votre application. Si vous *disposez* déjà d’un bot inscrit auprès de Bot Framework, vous pouvez l’ajouter en cliquant sur Configurer et en fournissant le nom du bot, l’ID Bot Framework, et en définissant les étendues dans lesquelles le bot fonctionne.

Si vous n’avez pas encore inscrit de bot auprès de Bot Framework, **sélectionnez Inscrire** pour en créer un. Une fois que vous avez inscrit votre bot, revenez à cette section de l’Éditeur manifeste pour entrer son nom et l’ID Bot Framework.

Une fois que vous avez fourni les informations de votre bot, vous pouvez maintenant éventuellement définir une liste de commandes que votre bot peut suggérer aux utilisateurs. Ajoutez le nom de la commande, une description de la commande, qui indique sa syntaxe et ses arguments, ainsi que l’étendue à laquelle cette commande doit s’appliquer.

> [!NOTE]
> Si vous avez défini votre bot pour prendre en charge une seule étendue, les commandes spécifiées pour l’étendue non prise en charge sont ignorées. Vous pouvez modifier les étendues que votre bot prend en charge à tout moment.

##### <a name="connectors"></a>Connecteurs

Cette section vous permet d’ajouter un connecteur à votre application. Si vous avez déjà inscrit un connecteur Office 365, sélectionnez **Configurer** puis entrez le nom et l’ID du connecteur. Si vous souhaitez qu’un nouveau connecteur **sélectionnez Inscrire** pour qu’il soit pris dans le tableau de bord du développeur du connecteur dans votre navigateur.

##### <a name="message-extensions"></a>Message Extensions

[Les extensions de message](~/messaging-extensions/what-are-messaging-extensions.md) sont un moyen puissant pour les utilisateurs d’interagir avec votre application dans Teams. Les utilisateurs peuvent interroger les informations de votre service et publier ces informations sous forme de cartes, directement dans le canal ou la conversation instantanée.

Les extensions de message sont alimentées par des bots Bot Framework. Elles nécessitent donc un bot configuré pour fonctionner. Si vous avez le nom et l’ID Bot Framework du bot que vous souhaitez activer l’extension de message, entrez-le. Sinon, **sélectionnez Inscrire** pour en créer un et entrez les informations par la suite. Indiquez si la configuration d’une extension de message peut être mise à jour par l’utilisateur.

Une fois le bot sous-jacent configuré, définissez les commandes et les paramètres que l’extension de message peut accepter.

Chaque commande nécessite un titre et un ID. La commande peut éventuellement contenir une description pour l’utilisateur. Chaque commande peut prendre en charge jusqu’à cinq paramètres, chacun d’eux nécessitant :

* Nom du paramètre tel qu’il apparaît dans le client Teams et inclus dans la demande de l’utilisateur.
* Titre convivial.
* Description facultative.

> [!NOTE]
> Pour créer une extension de message à l’aide d’App Studio, consultez [créer une extension de message à l’aide d’App Studio](~/resources/create-messaging-extension-using-appstudio.md).

#### <a name="test-and-distribute"></a>Tester et distribuer

Une fois que vous avez terminé de définir votre application, la section Test et distribution vous permet d’exporter la définition de votre application en tant que fichier zip, qui peut ensuite être partagée et chargée dans le client Teams à des fins de test. Cliquer sur Exporter télécharge le fichier zip sous *appname.zip* dans votre répertoire de téléchargement par défaut.

##### <a name="publish-your-app-to-teams"></a>Publier votre application sur Teams

Sur la page d’accueil de votre projet, vous pouvez télécharger votre application dans une équipe, l’envoyer sur le magasin d’applications personnalisé de votre entreprise pour les utilisateurs de votre organisation ou envoyer votre application à la source de l’application pour tous les utilisateurs Teams. Votre administrateur informatique examine ces soumissions. Vous pouvez revenir à la page *Publier* pour vérifier l’état de votre envoi et savoir si votre application a été approuvée ou refusée par votre administrateur informatique. C’est également ici que vous pouvez envoyer des mises à jour à votre application ou annuler les envois en cours.

### <a name="card-editor"></a>Éditeur de carte

Une carte est un conteneur pour des éléments d’informations courts ou associés. Teams prend en charge les cartes, qui peuvent avoir plusieurs propriétés et pièces jointes. Les cartes sont un moyen clé pour les bots et les connecteurs de relayer des informations utilisables pour les utilisateurs.

Pour faciliter et rendre ce processus moins sujet aux erreurs, l’onglet Éditeur de carte vous permet de créer des cartes héros ou des cartes miniatures à l’aide d’un formulaire et de vérifier et de tester la carte obtenue (exactement comme un utilisateur le voit) par le biais d’un bot. Elle fournit également le code JSON, C# ou Node.js correspondant pour la carte que vous pouvez copier/coller dans le code source de votre application.

Si vous avez déjà une carte que vous voulez vérifier dans Teams, vous pouvez coller le JSON de cette carte dans l’onglet JSON sous *Ajouter des informations de carte* et vous les envoyer pour voir à quoi celle-ci ressemble dans une conversation.

### <a name="react-control-library"></a>Bibliothèque de contrôles React

>[!Note]
> Cette bibliothèque de contrôles React est déconseillée à l’avenir. Envisagez d’utiliser les [contrôles react Fluent-UI comme alternative](https://microsoft.github.io/fluent-ui-react/) précédemment Stardust UI.

La création d’une application qui suit les meilleures pratiques de Teams est un excellent moyen de donner à votre application une apparence qui s’adapte parfaitement à l’expérience cliente de Teams. Les contrôles d’interface utilisateur sont essentiels pour atteindre cet objectif. Pour faciliter la création d’une interface utilisateur cohérente, App Studio fournit plusieurs catégories de contrôles d’interface utilisateur, qui suivent Teams principes de conception.

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

## <a name="app-studio-to-developer-portal"></a>App Studio vers le portail des développeurs

App Studio sera déconseillé. Vous pouvez utiliser le portail des développeurs. Le tableau suivant fournit les informations détaillées sur les fonctionnalités prises en charge dans le portail des développeurs :

| Fonctionnalités | App Studio | Portail des développeurs |
| --- | --- | --- |
| Analyse des applications* | ❌ | ✔️ |
| Fonctionnalités de l’application - Bots | ✔️ | ✔️ |
| Fonctionnalités de l’application - Connecteurs | ✔️ | ✔️ |
| Fonctionnalités de l’application - Extension de messagerie | ✔️ | ✔️ |
| Fonctionnalités de l’application - Extension réunion | ❌ | ✔️ |
| Fonctionnalités de l’application - Applications personnelles | ✔️ | ✔️ |
| Fonctionnalités de l’application - Onglets | ✔️ | ✔️ |
| Environnements d’application | ❌ | ✔️ |
| Langues de l’application | ✔️ | ✔️ |
| Aperçu et téléchargement du manifeste d’application | ✔️ | ✔️ |
| Plans d’application et tarification | ❌ | ✔️ |
| Publication d’applications | ✔️ | ✔️ |
| Autorisations d’application | ❌ | ✔️ |
| Partage d’applications avec les co-développeurs | ❌ | ✔️ |
| Validation d’application | ✔️ | ✔️ |
| Créer une application | ✔️ | ✔️ |
| Transmettre un package zip | ✔️ | ✔️ |

\**L’analytique des applications sera bientôt disponible en disponibilité générale.*

## <a name="see-also"></a>Voir aussi

[Gérer vos applications avec le Portail des développeurs pour Microsoft Teams](~/concepts/build-and-test/teams-developer-portal.md)
