---
title: Connecteurs Office 365
description: Décrit comment se familiariser avec les connecteurs Office 365 dans Microsoft teams
keywords: 'équipes connecteur O365 '
ms.date: 04/19/2019
ms.openlocfilehash: 9c89463830d46512e622dcf4c256a867d419de83
ms.sourcegitcommit: d0ca6a4856ffd03d197d47338e633126723fa78a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2020
ms.locfileid: "45137653"
---
# <a name="creating-office-365-connectors-for-microsoft-teams"></a>Création de connecteurs Office 365 pour Microsoft teams

>Avec les applications Microsoft Teams, vous pouvez ajouter votre connecteur Office 365 existant ou en créer un nouveau à inclure dans Microsoft Teams. Pour plus d’informations, reportez-vous à [la rubrique créer votre propre connecteur](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector) .

## <a name="adding-a-connector-to-your-teams-app"></a>Ajout d’un connecteur à votre application teams

Vous pouvez distribuer votre connecteur inscrit dans le cadre de votre package d’application Teams. Qu’il s’agisse d’une solution autonome ou de l’une des [fonctionnalités](~/concepts/extensibility-points.md) que votre expérience autorise dans Teams, vous pouvez [empaqueter](~/concepts/build-and-test/apps-package.md) et [publier](~/concepts/deploy-and-publish/apps-publish.md) votre connecteur dans le cadre de votre envoi de AppSource, ou vous pouvez le fournir aux utilisateurs directement pour le téléchargement dans Teams.

Pour distribuer votre connecteur, vous devez vous inscrire à l’aide du [tableau de bord du développeur de connecteurs](https://outlook.office.com/connectors/home/login/#/publish). Par défaut, une fois qu’un connecteur est inscrit, il est supposé que votre connecteur fonctionnera sur tous les produits Office 365 qui le prennent en charge, y compris Outlook et Teams. Si ce n’est _pas_ le cas et que vous devez créer un connecteur qui fonctionne uniquement dans Microsoft Teams, contactez-nous directement à l' [application Microsoft teams envois](mailto:teamsubm@microsoft.com).

> [!IMPORTANT]
> Une fois que vous avez cliqué sur **Enregistrer** dans le tableau de bord du développeur de connecteurs, votre connecteur est enregistré. Si vous souhaitez publier votre connecteur dans AppSource, suivez les instructions de la [publication de votre application Microsoft teams vers AppSource](~/concepts/deploy-and-publish/apps-publish.md). Si vous ne souhaitez pas publier votre application dans AppSource, et plutôt simplement la distribuer directement à votre organisation, vous pouvez le faire en [publiant dans votre organisation](#publish-connectors-for-your-organization). Si vous souhaitez uniquement publier dans votre organisation, aucune autre action n’est nécessaire sur le tableau de bord du connecteur.

### <a name="integrating-the-configuration-experience"></a>Intégration de l’expérience de configuration

Vos utilisateurs termineront l’expérience de configuration du connecteur tout entier sans avoir à quitter le client Teams. Pour réaliser cette expérience, teams incorpore votre page de configuration directement dans un IFRAME. La séquence d’opérations se présente comme suit :

1. L’utilisateur clique sur votre connecteur pour commencer le processus de configuration.
2. Teams chargera votre expérience de configuration en ligne.
3. L’utilisateur interagit avec votre expérience Web pour terminer la configuration.
4. L’utilisateur appuie sur « enregistrer », qui déclenche un rappel dans votre code.
5. Votre code traitera l’événement Save en récupérant les paramètres du webhook (répertoriés ci-dessous). Votre code doit ensuite stocker le webhook pour publier des événements ultérieurement.

Vous pouvez réutiliser votre expérience de configuration Web existante ou créer une version distincte à héberger spécifiquement dans Teams. Votre code doit :

1. Incluez le kit de développement logiciel (SDK) Microsoft teams JavaScript. Votre code accède ainsi aux API pour effectuer des opérations courantes telles que l’obtention du contexte d’utilisateur/canal/équipe actuel et l’initiation de flux d’authentification. Initialisez le kit de développement logiciel (SDK) en appelant `microsoftTeams.initialize()`.
2. Appelez `microsoftTeams.settings.setValidityState(true)` lorsque vous souhaitez activer le bouton enregistrer. Vous devez effectuer cette action en réponse à une entrée utilisateur valide, telle qu’une sélection ou une mise à jour de champ.
3. Enregistrer un `microsoftTeams.settings.registerOnSaveHandler()` Gestionnaire d’événements, qui est appelé lorsque l’utilisateur clique sur Enregistrer.
4. Appel `microsoftTeams.settings.setSettings()` pour enregistrer les paramètres du connecteur. Ce qui est enregistré ici est également ce qui s’affichera dans la boîte de dialogue de configuration si l’utilisateur tente de mettre à jour une configuration existante pour votre connecteur.
5. Appeler `microsoftTeams.settings.getSettings()` les propriétés webhook, y compris l’URL elle-même. Vous devez également l’appeler en plus de lors de l’événement Save, vous devez également l’appeler lorsque votre page est chargée pour la première fois en cas de reconfiguration.
6. Module Enregistrer un `microsoftTeams.settings.registerOnRemoveHandler()` Gestionnaire d’événements, qui est appelé lorsque l’utilisateur supprime votre connecteur. Cet événement permet à votre service d’effectuer des actions de nettoyage.

#### <a name="getsettings-response-properties"></a>`GetSettings()`Propriétés de la réponse

>[!Note]
>Les paramètres renvoyés par l' `getSettings` appel ici sont différents de ceux de l’appel de cette méthode à partir d’un onglet et diffèrent de ceux décrits [ici](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest).

| Paramètre   | Détails |
|-------------|---------|
| `entityId`       | ID d’entité, tel que défini par votre code lors de l’appel `setSettings()` . |
| `configName`  | Nom de la configuration, tel que défini par votre code lors de l’appel `setSettings()` . |
| `contentUrl` | L’URL de la page de configuration, telle que définie par votre code lors de l’appel`setSettings()` |
| `webhookUrl` | URL de webhook créée pour ce connecteur. Conservez l’URL de webhook et utilisez-la pour publier un JSON structuré afin d’envoyer des cartes vers le canal. L’élément `webhookUrl` est renvoyé uniquement lorsque l’application effectue un renvoi. |
| `appType` | Les valeurs renvoyées peuvent être `mail`, `groups` ou `teams` correspondant à la messagerie Office 365, aux groupes Office 365 ou à Microsoft Teams. |
| `userObjectId` | Il s’agit de l’ID unique correspondant à l’utilisateur Office 365 qui a initié le programme d’installation du connecteur. Il doit être sécurisé. Cette valeur peut être utilisée pour associer l’utilisateur dans Office 365 qui a défini la configuration à l’utilisateur dans votre service. |

Si vous devez authentifier l’utilisateur dans le cadre du chargement de votre page à l’étape 2 ci-dessus, reportez-vous à [ce lien](~/tabs/how-to/authentication/auth-flow-tab.md) pour obtenir des informations sur l’intégration de la connexion lorsque votre page est incorporée.

> [!NOTE]
> En raison de raisons de compatibilité entre les clients, votre code doit appeler `microsoftTeams.authentication.registerAuthenticationHandlers()` avec les méthodes de rappel URL et réussite/échec avant d’appeler `authenticate()` .

#### <a name="handling-edits"></a>Gestion des modifications

Votre code doit gérer les utilisateurs qui reviennent dans le but de modifier une configuration de connecteur existante. Pour ce faire, appelez `microsoftTeams.settings.setSettings()` lors de la configuration initiale avec les paramètres suivants :

- `entityId`est l’ID personnalisé compris par votre service et représente ce que l’utilisateur a configuré.
- `configName`est un nom convivial que votre code de configuration peut récupérer
- `contentUrl`est une URL personnalisée qui est chargée lorsqu’un utilisateur modifie une configuration de connecteur existante. Vous pouvez utiliser cette URL pour permettre à votre code de gérer plus facilement le cas de modification.

En règle générale, cet appel est effectué dans le cadre de votre gestionnaire d’événements Save. Ensuite, lorsque le `contentUrl` code ci-dessus est chargé, votre code doit appeler `getSettings()` pour préremplir les paramètres ou les formulaires dans votre interface utilisateur de configuration.

#### <a name="handling-removals"></a>Gestion des suppressions

Vous pouvez éventuellement exécuter un gestionnaire d’événements lorsque l’utilisateur supprime une configuration de connecteur existante. Vous enregistrez ce gestionnaire en appelant `microsoftTeams.settings.registerOnRemoveHandler()` . Ce gestionnaire peut être utilisé pour effectuer des opérations de nettoyage, telles que la suppression d’entrées d’une base de données.

### <a name="including-the-connector-in-your-manifest"></a>Inclusion du connecteur dans votre manifeste

Vous pouvez télécharger le manifeste d’application teams généré automatiquement à partir du portail. Avant de pouvoir l’utiliser pour tester ou publier votre application, vous devez procéder comme suit :

- Vous avez le choix entre deux icônes, en suivant les instructions figurant dans [Icônes](~/concepts/build-and-test/apps-package.md#icons).
- Modifiez la partie `icons` du manifeste pour faire référence aux noms de fichier des icônes au lieu des URL.

Le fichier manifest.json suivant contient les éléments de base nécessaires pour tester et envoyer votre application.

> [!NOTE]
> Remplacez `id` et `connectorId` de l’exemple suivant par le GUID de votre connecteur.

#### <a name="example-manifestjson-with-connector"></a>Exemple de fichier manifest.json avec Connecteur

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "id": "e9343a03-0a5e-4c1f-95a8-263a565505a5",
  "version": "1.0",
  "packageName": "com.sampleapp",
  "developer": {
    "name": "Publisher",
    "websiteUrl": "https://www.microsoft.com",
    "privacyUrl": "https://www.microsoft.com",
    "termsOfUseUrl": "https://www.microsoft.com"
  },
  "description": {
    "full": "This is a sample manifest for an app with a connector with an inline configuration experience.",
    "short": "This is a sample manifest for an app with a connector."
  },
  "icons": {
    "outline": "sampleapp-outline.png",
    "color": "sampleapp-color.png"
  },
  "connectors": [
    {
      "connectorId": "e9343a03-0a5e-4c1f-95a8-263a565505a5",
      "configurationUrl": "https://teamstodoappconnectorwithinlineconfig.azurewebsites.net/Connector/Setup",
      "scopes": [
        "team"
      ]
    }
  ],
  "name": {
    "short": "Sample App",
    "full": "Sample App Long Name"
  },
  "accentColor": "#FFFFFF"
}
```

## <a name="testing-your-connector"></a>Test du connecteur

Pour tester le connecteur, téléchargez-le dans une équipe comme vous le feriez avec une autre application. Vous pouvez créer un package .zip à l’aide du fichier manifeste à partir du tableau de bord du développeur de connecteurs (modifié comme indiqué dans la section précédente) et des deux fichiers d’icône.

Une fois que vous avez téléchargé l’application, ouvrez la liste des connecteurs à partir de n’importe quel canal. Faites défiler la page vers le bas pour afficher votre application dans la section **Téléchargé**.

![Capture d’écran de la section téléchargée dans la boîte de dialogue connecteur](~/assets/images/connectors/connector_dialog_uploaded.png)

Vous pouvez à présent lancer l’expérience de configuration. N’oubliez pas que ce flux se fait entièrement au sein de Microsoft teams en tant qu’expérience hébergée.

Pour vérifier qu’une `HttpPOST` action fonctionne correctement, [envoyez des messages à votre connecteur](~/webhooks-and-connectors/how-to/connectors-using.md).

## <a name="publish-connectors-for-your-organization"></a>Publier des connecteurs pour votre organisation

Parfois, il se peut que vous ne vouliez pas publier votre application connecteur vers le AppSource/magasin public, mais que celle-ci soit disponible uniquement pour les utilisateurs de votre organisation. Dans ce cas, vous pouvez charger votre application de connecteur personnalisé dans le [catalogue d’applications de votre organisation](~/concepts/deploy-and-publish/apps-publish.md). De cette manière, votre application de connecteur sera disponible uniquement pour cette organisation, et vous n’aurez pas besoin de publier votre connecteur dans la Banque publique.

Une fois que vous avez téléchargé votre package d’application, pour configurer et utiliser le connecteur dans une équipe, vous pouvez l’installer à partir du catalogue d’applications de l’organisation en procédant comme suit :

1. Sélectionnez l’icône applications dans la barre de navigation extrême gauche.
1. Dans la fenêtre **applications** , sélectionnez **connecteurs**.
1. Sélectionnez le connecteur que vous souhaitez ajouter et une fenêtre de boîte de dialogue contextuelle s’affichera.
1. Sélectionnez l’option **Ajouter à une barre d’équipe** .
1. Dans la fenêtre de boîte de dialogue suivante, tapez le nom d’une équipe ou d’un canal.
1. Sélectionnez l’option **configurer une** barre de liens dans le coin inférieur droit de la fenêtre de la boîte de dialogue.
1. Le connecteur sera disponible dans la section &#9679;&#9679;&#9679; => *plusieurs options*  =>  *connecteurs*  =>  de*tous les*  =>  *connecteurs de votre équipe* pour cette équipe. Vous pouvez naviguer en faisant défiler vers cette section ou Rechercher l’application connecteur.
1. Pour configurer ou modifier le connecteur, sélectionnez la barre **configurer** .
