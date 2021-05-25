---
title: Configuration de l’application dans le portail du développeur
description: Découvrez comment configurer et gérer vos applications à l’aide du portail de développement pour Microsoft Teams
keywords: mise en place des équipes du portail de développement
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: ce290bd7daa46467be279aae7c608321e75e2d57
ms.sourcegitcommit: d972953994e405c6afc42e4d4a76b48c6d4cfb5f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/24/2021
ms.locfileid: "52635114"
---
# <a name="app-configuration"></a>Configuration de l’application

La partie la plus significative d’un package Microsoft Teams’application est sa manifest.jsfichier. Ce fichier doit être conforme au [schéma Teams’application.](~/resources/schema/manifest-schema.md) Le manifest.jssur le fichier contient des métadonnées, ce qui Teams de présenter correctement votre application aux utilisateurs.

Vous pouvez effectuer les actions suivantes dans la section **Configurer** du portail du développeur :

* Créez facilement un package d’application.
* Décrivez l’application.
* Télécharger vos icônes.
* Produire un .zip pour faciliter la distribution.

> [!NOTE]
> Le portail du développeur ne produit pas de code fonctionnel pour votre application ou n’héberge pas votre application. Votre application doit déjà être hébergée et en cours d’exécution à l’URL répertoriée dans le manifeste pour que le processus de chargement de l’application aboutisse à une application fonctionnelle.

:::image type="content" source="~/assets/images/tdp/tdp_configure_1.png" alt-text="Screenshot showing the Configure page of Teams Developer Portal.":::

## <a name="basic-information-and-branding"></a>Informations de base et branding

Les **sections Informations de** base et **Branding** définissent la description de haut niveau de l’application que vous faites. Cela inclut le nom, la description et la marque visuelle de l’application. Les informations de cette section seront utilisées dans la liste du Teams de votre application et dans le dialogue d’installation de l’application.

## <a name="capabilities"></a>Fonctionnalités

Les **détails des** fonctionnalités de l’application sont répertoriés dans la section Fonctionnalités de configuration.

> [!NOTE]
> La fonctionnalité de personnalisation de l’application est actuellement disponible dans la version préliminaire du développeur uniquement.
> 
> En tant que meilleure pratique, vous devez fournir des instructions de personnalisation que les utilisateurs et les clients de l’application doivent suivre lors de la personnalisation de votre application. Pour plus d’informations, voir [personnaliser les applications dans Microsoft Teams](/MicrosoftTeams/customize-apps).

Voici les fonctionnalités :

:::image type="content" source="~/assets/images/tdp/tdp_capabilities.png" alt-text="Screenshot showing the Configure page of Teams Developer Portal.":::

* **Application personnelle** 

  Cette section vous permet de définir un ensemble d’onglets présentés par défaut dans l’expérience d’application personnelle, c’est-à-dire l’expérience qu’un utilisateur a avec votre application en dehors du contexte d’une équipe ou d’un canal. Dans cette section, fournissez les détails suivants :

  * Nom de l’onglet.
  * Identificateur unique.
  * URL qui pointe vers l’interface utilisateur à afficher dans Teams.
  * URL à utiliser si un utilisateur choisit d’afficher l’onglet dans un navigateur. Il s’agit d’une information facultative.
  * Tous les domaines supplémentaires à partir des lesquels l’onglet s’attend à charger ou à laquelle établir un lien.

* **Application de groupe et de canal**

  Un onglet Teams fait partie d’un canal et fournit un accès rapide aux informations et ressources de l’équipe. Par exemple, l’onglet Planificateur d’un canal contient un plan unique, l’onglet Power BI est mapmé à un rapport spécifique. Les utilisateurs peuvent explorer le contexte approprié, mais ils ne peuvent pas naviguer en dehors de l’onglet. Par exemple, l’onglet Power BI n’active pas la navigation vers les autres rapports Power BI, mais il active le bouton **Accéder au site web** qui lance le rapport dans le site web principal de Power BI.

    > [!NOTE]
    > Pour les onglets d’équipe, vous devez fournir une URL de configuration pour présenter les options et collecter des informations, ce qui vous aiderait à personnaliser le contenu et l’expérience de votre onglet. Cette page HTML en iframed s’affiche lorsqu’un utilisateur ajoute pour la première fois l’onglet à un canal.
    > Vous devez également fournir d'autres domaines à partir desquels l'onglet doit être chargé ou lié.

* **Bot**

  Cette section vous permet d’ajouter un [bot conversation](~/bots/what-are-bots.md) à votre application. Si vous avez déjà inscrit un bot auprès de Bot Framework, vous pouvez ajouter ce bot en cliquant sur **Configurer** et en fournissant le nom du bot, l’ID Bot Framework, et en définissant les étendues dans lesquelles le bot fonctionne.

  Si vous n’avez pas encore inscrit le bot auprès de Bot Framework, cliquez sur **Enregistrer** pour en créer un nouveau. Une fois que vous avez inscrit votre bot, revenir à cette section de l’Éditeur de manifeste pour entrer son nom et son ID Bot Framework.

  Une fois que vous avez fourni les informations de votre bot, vous pouvez éventuellement définir une liste de commandes que votre bot peut suggérer aux utilisateurs. Ajoutez le nom de la commande, une description de celle-ci qui indique sa syntaxe et ses arguments, ainsi que l’étendue à laquelle cette commande doit s’appliquer.

  Notez que si vous avez défini votre bot pour prendre en charge une seule étendue, les commandes spécifiées pour l’étendue non prise en charge seront ignorées. Vous pouvez modifier les étendues que votre bot prend en charge à tout moment.

* **Connector**

  Cette section vous permet d’ajouter un connecteur à votre application. Si vous avez déjà inscrit un connecteur  Office 365, sélectionnez Configurer et entrez le nom et l’ID du connecteur. Si vous voulez un nouveau connecteur, cliquez sur **S'inscrire** pour accéder au tableau de bord du développeur de connecteurs dans votre navigateur.

  > [!NOTE]
  > La personnalisation d’application permet aux administrateurs de modifier l’apparence des applications chargées par le biais de bots, d’extensions de messagerie, d’onglets et de connecteurs. Par exemple, si l’administrateur Teams personnalise le nom d’une application , l’application apparaît avec le nouveau nom pour `Contoso` `Contoso Agent` les `Contoso Agent` utilisateurs. Toutefois, lors de l’ajout d’un connecteur à une conversation, dans la liste, les connecteurs afficheront toujours le nom de l’application en tant que `Contoso` .

* **Extensions de messagerie**

  [Les extensions de messagerie](~/messaging-extensions/what-are-messaging-extensions.md) sont un moyen puissant pour les utilisateurs de interagir avec votre application au sein de Microsoft Teams. Les utilisateurs peuvent interroger les informations de votre service et publier ces informations sous forme de cartes, directement dans le canal ou la conversation instantanée.

  Les extensions de messagerie sont optimisées par des bots Bot Framework. Ils ont donc besoin d’un bot configuré pour opérer. Si vous avez le nom et l’ID Bot Framework du bot dont vous voulez power l’extension de messagerie, entrez-le. Sinon, cliquez sur *S'inscrire* pour en créer un, puis entrez les informations par la suite. Choisissez si la configuration d’une extension de messagerie peut être mise à jour par l’utilisateur.

  Une fois le bot sous-jacent configuré, définissez les commandes et paramètres que l’extension de messagerie peut accepter.

  Chaque commande nécessite un titre et un ID. La commande peut éventuellement contenir une description pour l’utilisateur. Chaque commande peut prendre en charge jusqu’à cinq paramètres, chacun nécessitant les paramètres suivants :

  * Nom du paramètre tel qu’il apparaît dans Teams client et est inclus dans la demande de l’utilisateur.
  * Titre convivial.
  * Description facultative.

  > [!NOTE]
  > Pour créer une extension de messagerie à l’aide d’App Studio, voir créer une [extension de messagerie à l’aide d’app studio.](~/resources/create-messaging-extension-using-appstudio.md)

* **Extension de réunion**

  TODO : Rajesh R.

* **Scene**

  Scènes en mode Ensemble est un artefact créé par le développeur de scène à l’aide du studio de scène Microsoft qui réunit les personnes avec leur flux vidéo dans un paramètre créatif tel que le créateur de scène. Dans un paramètre de scène en cours, les participants ont des sièges désignés avec des flux vidéo restituer dans ces sièges. Pour plus d’informations, [voir Teams mode Ensemble.](~/apps-in-teams-meetings/teams-together-mode.md)

## <a name="permissions"></a>Autorisations

Vous pouvez enrichir votre application Teams avec des fonctionnalités natives d’appareil, telles que la caméra, le microphone et l’emplacement.

## <a name="languages"></a>Langages

Configurer ou modifier les langues que votre application prend en charge.

## <a name="single-sign-on"></a>Authentification unique

Configurez votre application pour authentifier les utilisateurs avec l’authentification unique (SSO).

## <a name="domains"></a>Domaines

Liste des domaines valides pour les sites web que l’application s’attend à charger dans Teams client. Les listes de domaines peuvent inclure des caractères génériques, par exemple, `*.example.com` . Cela correspond exactement à un segment du domaine ; si vous avez besoin d’une `a.b.example.com` correspondance, utilisez `*.*.example.com` . Si votre interface utilisateur de contenu ou de configuration d’onglet doit accéder à un autre domaine en plus de celui utilisé pour la configuration de l’onglet, ce domaine doit être spécifié ici.

Il n’est pas nécessaire d’inclure les domaines des fournisseurs d’identité que vous souhaitez prendre en charge dans votre application. Par exemple, pour vous authentifier à l’aide d’un ID Google, il est nécessaire de rediriger vers accounts.google.com, toutefois, vous ne devez pas inclure accounts.google.com dans `validDomains[]` .

Teams applications qui nécessitent leurs propres URL sharepoint pour fonctionner bien, inclut « {teamsitedomain} » dans leur liste de domaines valide.

> [!IMPORTANT]
> N’ajoutez pas de domaines qui sont en dehors de votre contrôle, directement ou par le biais de caractères génériques. Par exemple, `yourapp.onmicrosoft.com` est valide, toutefois, `*.onmicrosoft.com` n’est pas valide.

L’objet est un tableau avec tous les éléments du type `string` .

## <a name="advanced"></a>Avancé
Todo par Karthig

### <a name="app-content"></a>Contenu de l’application
Todo par Karthig

### <a name="first-party-settings"></a>Paramètres de première partie
Todo par Karthig

## <a name="see-also"></a>Voir aussi

* [Vue d’ensemble Teams portail du développeur](~/concepts/build-and-test/teams-developer-portal.md)
* [Distribuer Teams portail pour les développeurs](~/concepts/tdp-distribute.md)
* [Outils du portail Teams développeur](~/concepts/tdp-tools.md)