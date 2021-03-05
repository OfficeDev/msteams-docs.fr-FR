---
title: Connecteurs Office 365
description: Décrit la mise en place des connecteurs Office 365 dans Microsoft Teams
keywords: 'équipes connecteur O365 '
ms.topic: conceptual
ms.date: 04/19/2019
ms.openlocfilehash: 8f9fcc40ca0634ead0a6c5d7d0653ad4ab993860
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449254"
---
# <a name="creating-office-365-connectors-for-microsoft-teams"></a>Création de connecteurs Office 365 pour Microsoft Teams

>Avec les applications Microsoft Teams, vous pouvez ajouter votre connecteur Office 365 existant ou en créer un nouveau à inclure dans Microsoft Teams. Pour [plus d’informations, voir](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector) Créer votre propre connecteur.

## <a name="adding-a-connector-to-your-teams-app"></a>Ajout d’un connecteur à votre application Teams

Vous pouvez distribuer votre connecteur inscrit dans le cadre de votre package d’application Teams. Qu’il s’agit d’une solution autonome ou de l’une [](~/concepts/build-and-test/apps-package.md) des [](~/concepts/deploy-and-publish/apps-publish.md) nombreuses fonctionnalités que votre expérience active dans Teams, vous pouvez packager et publier votre connecteur dans le cadre de votre soumission AppSource, ou vous pouvez le fournir aux utilisateurs directement pour le chargement dans Teams. [](~/concepts/extensibility-points.md)

Pour distribuer votre connecteur, vous devez vous inscrire à l’aide du tableau de bord du [développeur de connecteurs.](https://outlook.office.com/connectors/home/login/#/publish) Par défaut, une fois qu’un connecteur est inscrit, il est supposé que votre connecteur fonctionne dans tous les produits Office 365 qui les prend en charge, y compris Outlook et Teams. Si ce _n’est_ pas le cas et que vous devez créer un connecteur qui fonctionne uniquement dans Microsoft Teams, contactez-nous directement auprès des [soumissions d’applications Microsoft Teams.](mailto:teamsubm@microsoft.com)

> [!IMPORTANT]
> Une fois que **vous avez choisi Enregistrer** dans le tableau de bord du développeur de connecteurs, votre connecteur est enregistré. Si vous souhaitez publier votre connecteur dans AppSource, suivez les instructions de la publication de votre application [Microsoft Teams dans AppSource.](~/concepts/deploy-and-publish/apps-publish.md) Si vous ne souhaitez pas publier votre application dans AppSource et simplement la distribuer directement à votre organisation uniquement, vous pouvez le faire en publiant dans [votre organisation.](#publish-connectors-for-your-organization) Si vous souhaitez uniquement publier dans votre organisation, aucune action supplémentaire n’est nécessaire sur le tableau de bord du connecteur.

### <a name="integrating-the-configuration-experience"></a>Intégration de l’expérience de configuration

Vos utilisateurs termineront toute l’expérience de configuration du connecteur sans avoir à quitter le client Teams. Pour obtenir cette expérience, Teams incorpore votre page de configuration directement dans un iframe. La séquence d’opérations est la suivante :

1. L’utilisateur clique sur votre connecteur pour commencer le processus de configuration.
2. Teams charge votre expérience de configuration en ligne.
3. L’utilisateur interagit avec votre expérience web pour terminer la configuration.
4. L’utilisateur appuie sur « Enregistrer », ce qui déclenche un rappel dans votre code.
5. Votre code traitera l’événement d’enregistrer en récupérant les paramètres de webhook (documentés ci-dessous). Votre code doit ensuite stocker le webhook pour publier des événements ultérieurement.

Vous pouvez réutiliser votre expérience de configuration web existante ou créer une version distincte à héberger spécifiquement dans Teams. Votre code doit :

1. Incluez le SDK JavaScript Microsoft Teams. Cela permet à votre code d’accéder aux API pour effectuer des opérations courantes telles que l’obtention du contexte utilisateur/canal/équipe actuel et l’initiateur des flux d’authentification. Initialisez le kit de développement logiciel (SDK) en appelant `microsoftTeams.initialize()`.
2. Appelez `microsoftTeams.settings.setValidityState(true)` lorsque vous souhaitez activer le bouton Enregistrer. Vous devez le faire en réponse à une entrée utilisateur valide, telle qu’une sélection ou une mise à jour de champ.
3. Inscrivez un `microsoftTeams.settings.registerOnSaveHandler()` handler d’événements, qui est appelé lorsque l’utilisateur clique sur Enregistrer.
4. Appelez `microsoftTeams.settings.setSettings()` pour enregistrer les paramètres du connecteur. Les informations enregistrées ici sont également affichées dans la boîte de dialogue de configuration si l’utilisateur tente de mettre à jour une configuration existante pour votre connecteur.
5. Appelez `microsoftTeams.settings.getSettings()` pour récupérer les propriétés de webhook, y compris l’URL proprement dite. Vous devez l’appeler en plus de l’événement d’enregistrer, vous devez également l’appeler lorsque votre page est chargée pour la première fois dans le cas d’une nouvelle configuration.
6. (Facultatif) Inscrivez un `microsoftTeams.settings.registerOnRemoveHandler()` handler d’événements, qui est appelé lorsque l’utilisateur supprime votre connecteur. Cet événement permet à votre service d’effectuer des actions de nettoyage.

Voici un exemple de code HTML pour créer une page de configuration de connecteur sans CSS :

```html
<h2>Send notifications when tasks are:</h2>
<div class="col-md-8">
    <section id="configSection">
        <form id="configForm">
            <input type="radio" name="notificationType" value="Create" onclick="onClick()"> Created
            <br>
            <br>
            <input type="radio" name="notificationType" value="Update" onclick="onClick()"> Updated
        </form>
    </section>
</div>

<script src="https://statics.teams.microsoft.com/sdk/v1.5.2/js/MicrosoftTeams.min.js" crossorigin="anonymous"></script>
<script src="/Scripts/jquery-1.10.2.js"></script>

<script type="text/javascript">

        function onClick() {
            microsoftTeams.settings.setValidityState(true);
        }

        microsoftTeams.initialize();
        microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
            var radios = document.getElementsByName('notificationType');

            var eventType = '';
            if (radios[0].checked) {
                eventType = radios[0].value;
            } else {
                eventType = radios[1].value;
            }

            microsoftTeams.settings.setSettings({
                 entityId: eventType,
                contentUrl: "https://YourSite/Connector/Setup",
                removeUrl:"https://YourSite/Connector/Setup",
                 configName: eventType
                });

            microsoftTeams.settings.getSettings(function (settings) {
                // We get the Webhook URL in settings.webhookUrl which needs to be saved. 
                // This can be used later to send notification.
            });

            saveEvent.notifySuccess();
        });

        microsoftTeams.settings.registerOnRemoveHandler(function (removeEvent) {
            var removeCalled = true;
            alert("Removed" + JSON.stringify(removeEvent));
        });

</script>
```

#### <a name="getsettings-response-properties"></a>`GetSettings()` propriétés de réponse

>[!Note]
>Les paramètres renvoyés par l’appel ici sont différents de ceux que vous avez appelés à partir d’un onglet et diffèrent de ceux documentés `getSettings` [ici.](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest&preserve-view=true)

| Paramètre   | Détails |
|-------------|---------|
| `entityId`       | ID d’entité, tel que définie par votre code lors de `setSettings()` l’appel. |
| `configName`  | Nom de la configuration, tel que définie par votre code lors de `setSettings()` l’appel. |
| `contentUrl` | URL de la page de configuration, définie par votre code lors de l’appel `setSettings()` |
| `webhookUrl` | URL de webhook créée pour ce connecteur. Persistez l’URL de webhook et utilisez-la pour post JSON structuré pour envoyer des cartes au canal. L’élément `webhookUrl` est renvoyé uniquement lorsque l’application effectue un renvoi. |
| `appType` | Les valeurs renvoyées peuvent être `mail`, `groups` ou `teams` correspondant à la messagerie Office 365, aux groupes Office 365 ou à Microsoft Teams. |
| `userObjectId` | Il s’agit de l’ID unique correspondant à l’utilisateur Office 365 qui a initié la configuration du connecteur. Il doit être sécurisé. Cette valeur peut être utilisée pour associer l’utilisateur dans Office 365 qui a défini la configuration à l’utilisateur dans votre service. |

Si vous devez authentifier l’utilisateur dans le cadre du [](~/tabs/how-to/authentication/auth-flow-tab.md) chargement de votre page à l’étape 2 ci-dessus, reportez-vous à ce lien pour plus d’informations sur la façon d’intégrer la connexion lorsque votre page est incorporée.

> [!NOTE]
> Pour des raisons de compatibilité entre clients, votre code devra appeler avec l’URL et les méthodes de rappel de `microsoftTeams.authentication.registerAuthenticationHandlers()` réussite/échec avant d’appeler. `authenticate()`

#### <a name="handling-edits"></a>Gestion des modifications

Votre code doit gérer les utilisateurs qui reviennent dans le but de modifier une configuration de connecteur existante. Pour ce faire, appelez `microsoftTeams.settings.setSettings()` pendant la configuration initiale avec les paramètres suivants :

- `entityId` est l’ID personnalisé compris par votre service et qui représente ce que l’utilisateur a configuré.
- `configName` est un nom convivial que votre code de configuration peut récupérer
- `contentUrl` est une URL personnalisée qui est chargée lorsqu’un utilisateur modifie une configuration de connecteur existante. Vous pouvez utiliser cette URL pour faciliter la tâche de modification de votre code.

En règle générale, cet appel est effectué dans le cadre de votre économiseur d’événements. Ensuite, lorsque le code ci-dessus est chargé, votre code doit appeler pour prére remplir les paramètres ou formulaires de votre `contentUrl` interface utilisateur de `getSettings()` configuration.

#### <a name="handling-removals"></a>Gestion des suppressions

Vous pouvez éventuellement exécuter un programme de gestion d’événements lorsque l’utilisateur supprime une configuration de connecteur existante. Vous inscrivez ce handler en appelant `microsoftTeams.settings.registerOnRemoveHandler()` . Ce handler peut être utilisé pour effectuer des opérations de nettoyage telles que la suppression d’entrées d’une base de données.

### <a name="including-the-connector-in-your-manifest"></a>Inclure le connecteur dans votre manifeste

Vous pouvez télécharger le manifeste d’application Teams généré automatiquement à partir du portail. Toutefois, avant de pouvoir l’utiliser pour tester ou publier votre application, vous devez :

- [Incluez deux icônes](../../concepts/build-and-test/apps-package.md#app-icons).
- Modifiez la partie `icons` du manifeste pour faire référence aux noms de fichier des icônes au lieu des URL.

Le fichier manifest.json suivant contient les éléments de base nécessaires pour tester et envoyer votre application.

> [!NOTE]
> Remplacez `id` et `connectorId` de l’exemple suivant par le GUID de votre connecteur.

#### <a name="example-manifestjson-with-connector"></a>Exemple de fichier manifest.json avec Connecteur

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
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

Vous pouvez à présent lancer l’expérience de configuration. N’ignorez pas que ce flux se produit entièrement dans Microsoft Teams en tant qu’expérience hébergée.

Pour vérifier `HttpPOST` qu’une action fonctionne correctement, [envoyez des messages à votre connecteur.](~/webhooks-and-connectors/how-to/connectors-using.md)

## <a name="publish-connectors-for-your-organization"></a>Publier des connecteurs pour votre organisation

Parfois, vous ne souhaitez peut-être pas publier votre application de connecteur dans l’AppSource/Store public, mais vous souhaitez qu’elle soit disponible uniquement pour les utilisateurs de votre organisation. Dans ce cas, vous pouvez charger votre application de connecteur personnalisé vers le catalogue [d’applications de votre organisation.](~/concepts/deploy-and-publish/apps-publish.md) Ainsi, votre application de connecteur sera disponible uniquement pour cette organisation et vous n’aurez pas besoin de publier votre connecteur dans le magasin public.

Une fois que vous avez chargé votre package d’application, pour configurer et utiliser le connecteur dans une équipe, il peut être installé à partir du catalogue d’applications de l’organisation en suivant les étapes suivantes :

1. Sélectionnez l’icône des applications dans la barre de navigation verticale à l’extrême gauche.
1. Dans la **fenêtre Applications,** **sélectionnez Connecteurs.**
1. Sélectionnez le connecteur que vous souhaitez ajouter et une fenêtre de boîte de dialogue s’affiche.
1. Sélectionnez **Ajouter à une barre d’équipe.**
1. Dans la fenêtre de boîte de dialogue suivante, tapez un nom d’équipe ou de canal.
1. Sélectionnez **la barre Configurer un connecteur** dans le coin inférieur droit de la fenêtre de boîte de dialogue.
1. Le connecteur sera disponible dans la section &#9679;&#9679;&#9679; => *Plus d’options* Connecteurs Tous les connecteurs pour votre équipe pour cette  =>    =>    =>   équipe. Vous pouvez naviguer en accédant à cette section ou rechercher l’application connecteur.
1. Pour configurer ou modifier le connecteur, sélectionnez **la barre Configurer.**

## <a name="code-sample"></a>Exemple de code
|**Exemple de nom** | **Description** | **.NET** | **Node.js** |
|----------------|------------------|--------|----------------|
| Connecteurs    | Exemple de connecteur Office 365 générant des notifications au canal Teams.|   [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-todo-notification/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-github-notification/nodejs)|
| Exemple de connecteurs génériques |Exemple de code pour un connecteur générique facile à personnaliser pour n’importe quel système qui prend en charge les webhooks.|  | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-generic/nodejs)|
