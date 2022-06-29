---
title: Créer des connecteurs Office 365
author: laujan
description: Dans ce module, découvrez comment bien démarrer avec les connecteurs Office 365 et ajouter un connecteur à l’application Teams dans Microsoft Teams
ms.localizationpriority: medium
ms.topic: conceptual
ms.date: 06/16/2021
ms.openlocfilehash: dec9acbf7ba2f52303b04a5219de575a96a792e5
ms.sourcegitcommit: c7fbb789b9654e9b8238700460b7ae5b2a58f216
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/29/2022
ms.locfileid: "66485344"
---
# <a name="create-office-365-connectors"></a>Créer des connecteurs Office 365

Avec les applications Microsoft Teams, vous pouvez ajouter votre Connecteur Office 365 existant ou en créer un nouveau dans Teams. Pour plus d'informations, consultez la section [Construire votre propre connecteur](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector).

Consultez la vidéo suivante pour découvrir comment créer un connecteur Office 365 :
<br>

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE4OIzv]
<br>


## <a name="add-a-connector-to-teams-app"></a>Ajouter un connecteur à l’application Teams

Vous pouvez créer un [package](~/concepts/build-and-test/apps-package.md) et [publier](~/concepts/deploy-and-publish/apps-publish.md) votre connecteur dans le cadre de votre soumission AppSource. Vous pouvez distribuer votre connecteur inscrit dans le cadre de votre package d’application Teams. Pour plus d’informations sur les points d’entrée pour l’application Teams, consultez [fonctionnalités](~/concepts/extensibility-points.md). Vous pouvez également fournir le package aux utilisateurs directement pour le chargement dans Teams.

Pour distribuer votre connecteur, inscrivez-le dans le [Tableau de bord du développeur des connecteurs](https://aka.ms/connectorsdashboard).

Pour qu’un connecteur fonctionne uniquement dans Teams, suivez les instructions pour envoyer le connecteur dans [la publication de votre application dans l’article du Microsoft Teams Store](~/concepts/deploy-and-publish/appsource/publish.md) . Sinon, un connecteur inscrit fonctionne dans tous les produits Office 365 qui prennent en charge les applications, y compris les Outlook et Teams.

> [!IMPORTANT]
> Votre connecteur est inscrit après avoir sélectionné **Enregistrer** dans le tableau de bord du développeur des connecteurs. Si vous souhaitez publier votre connecteur dans AppSource, suivez les instructions dans [Publier votre application Microsoft Teams sur AppSource](~/concepts/deploy-and-publish/apps-publish.md). Si vous ne souhaitez pas publier votre application dans AppSource, distribuez-la directement à l’organisation. Après la publication des connecteurs pour votre organisation, aucune action supplémentaire n’est requise sur le tableau de bord du connecteur.

### <a name="integrate-the-configuration-experience"></a>Intégrer l’expérience de configuration

Les utilisateurs peuvent effectuer l’intégralité de l’expérience de configuration du connecteur sans avoir à quitter le client Teams. Pour obtenir l’expérience, Teams peut incorporer votre page de configuration directement dans un iframe. La séquence d’opérations est la suivante :

1. L’utilisateur sélectionne le connecteur pour commencer le processus de configuration.
1. L’utilisateur interagit avec l’expérience web pour terminer la configuration.
1. L’utilisateur sélectionne **Enregistrer**, qui déclenche un rappel dans votre code.

    > [!NOTE]
    >
    > * Le code peut traiter l’événement d’enregistrement en récupérant les paramètres du webhook. Votre code stocke le webhook pour publier des événements ultérieurement.
    > * L’expérience de configuration est chargée en ligne dans Teams.

Vous pouvez réutiliser votre expérience de configuration web existante ou créer une version distincte à héberger spécifiquement dans Teams. Votre code doit inclure le Kit de développement logiciel (SDK) JavaScript Teams. Cela permet à votre code d’accéder aux API pour effectuer des opérations courantes, telles que l’obtention du contexte utilisateur, de canal ou d’équipe actuel et l’initialisation des flux d’authentification.

Pour intégrer l’expérience de configuration :

1. Initialisez le kit de développement logiciel (SDK) en appelant `microsoftTeams.initialize()`.
1. Appeler `microsoftTeams.settings.setValidityState(true)` pour activer **Enregistrer**.

    > [!NOTE]
    > Vous devez appeler `microsoftTeams.settings.setValidityState(true)` en réponse à la sélection de l’utilisateur ou à la mise à jour du champ.

1. Inscrivez un `microsoftTeams.settings.registerOnSaveHandler()` gestionnaire d’événements, qui est appelé lorsque l’utilisateur sélectionne **Enregistrer**.
1. Appelez `microsoftTeams.settings.setSettings()` pour enregistrer les paramètres du connecteur. Les paramètres enregistrés sont également affichés dans la boîte de dialogue de configuration si l’utilisateur tente de mettre à jour une configuration existante pour votre connecteur.
1. Appeler `microsoftTeams.settings.getSettings()` pour récupérer les propriétés du webhook, y compris l’URL.

    > [!NOTE]
    > Vous devez appeler `microsoftTeams.settings.getSettings()` lorsque votre page est chargée pour la première fois en cas de reconfiguration.

1. Enregistrez le gestionnaire d’événements `microsoftTeams.settings.registerOnRemoveHandler()`, qui est appelé lorsque l’utilisateur supprime le connecteur.

Cet événement donne à votre service la possibilité d’effectuer des actions de nettoyage.

Le code suivant fournit un exemple de code HTML pour créer une page de configuration de connecteur sans le service client et le support :

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
            alert("Removed" + JSON.stringify(removeEvent));
        });

</script>
```

Pour authentifier l’utilisateur dans le cadre du chargement de votre page, consultez [le flux d’authentification pour les onglets](~/tabs/how-to/authentication/auth-flow-tab.md) afin d’intégrer la connexion lorsque votre page est incorporée.

> [!NOTE]
> Pour des raisons de compatibilité entre clients, votre code doit appeler `microsoftTeams.authentication.registerAuthenticationHandlers()` avec l’URL et les méthodes de rappel de réussite ou d’échec avant d’appeler `authenticate()`.

#### <a name="getsettings-response-properties"></a>Propriétés de réponse `GetSettings`

>[!NOTE]
>Les paramètres retournés par l’appel de `getSettings` sont différents lorsque vous appelez cette méthode à partir d’un onglet et diffèrent de ceux documentés dans les [paramètres js](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings).

Le tableau suivant fournit les paramètres et les détails des propriétés de réponse `GetSetting` :

| Paramètres   | Détails |
|-------------|---------|
| `entityId`       | ID d’entité, tel que défini par votre code lors de l’appel `setSettings()`. |
| `configName`  | Nom de configuration, tel que défini par votre code lors de l’appel vers `setSettings()`. |
| `contentUrl` | URL de la page de configuration, définie par votre code lors de l’appel vers `setSettings()`. |
| `webhookUrl` | URL de webhook créée pour le connecteur. Utilisez l’URL de webhook pour publier le code JSON structuré afin d’envoyer des cartes au canal. Le `webhookUrl` est retourné uniquement lorsque l’application retourne des données. |
| `appType` | Les valeurs retournées peuvent être `mail`respectivement , `groups`ou `teams` correspondre au Office 365 Mail, Office 365 Groups ou Teams. |
| `userObjectId` | ID unique correspondant à l’utilisateur Office 365 qui a lancé la configuration du connecteur. Il doit être sécurisé. Cette valeur peut être utilisée pour associer l’utilisateur dans Office 365, qui a configuré la configuration dans votre service. |

#### <a name="handle-edits"></a>Gérer les modifications

Votre code doit gérer les utilisateurs qui reviennent dans le but de modifier une configuration de connecteur existante. Pour ce faire, appelez `microsoftTeams.settings.setSettings()` pendant la configuration initiale avec les paramètres suivants :

* `entityId` est l’ID personnalisé qui représente ce que l’utilisateur a configuré et compris par votre service.
* `configName` est un nom que le code de configuration peut récupérer.
* `contentUrl` est une URL personnalisée qui est chargée lorsqu’un utilisateur modifie une configuration de connecteur existante.

Cet appel est effectué dans le cadre de votre gestionnaire d’événements d’enregistrement. Ensuite, lors du chargement de `contentUrl`, votre code doit appeler `getSettings()` pour préremplir les paramètres ou formulaires de votre interface utilisateur de configuration.

#### <a name="handle-removals"></a>Gérer les suppressions

Vous pouvez exécuter un gestionnaire d’événements lorsque l’utilisateur supprime une configuration de connecteur existante. Vous inscrivez ce gestionnaire en appelant `microsoftTeams.settings.registerOnRemoveHandler()`. Ce gestionnaire est utilisé pour effectuer des opérations de nettoyage telles que la suppression d’entrées d’une base de données.

### <a name="include-the-connector-in-your-manifest"></a>Inclure le connecteur dans votre manifeste

Télécharger le `Teams app manifest` généré automatiquement à partir du portail. Effectuez les étapes suivantes, avant de tester ou de publier l’application :

1. [Incluez deux icônes](../../concepts/build-and-test/apps-package.md#app-icons).
1. Modifiez la partie `icons` du manifeste pour inclure les noms de fichiers des icônes au lieu des URL.

Le fichier manifest.json suivant contient les éléments nécessaires pour tester et soumettre l’application :

> [!NOTE]
> Remplacez `id` et `connectorId` de l’exemple suivant par le GUID du connecteur.

#### <a name="example-of-manifestjson-with-connector"></a>Exemple de fichier manifest.json avec connecteur

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
    "full": "This is a small sample app we made for you! This app has samples of all capabilities Microsoft Teams supports.",
    "short": "This is a small sample app we made for you!"
  },
  "icons": {
    "outline": "sampleapp-outline.png",
    "color": "sampleapp-color.png"
  },
  "connectors": [
    {
      "connectorId": "e9343a03-0a5e-4c1f-95a8-263a565505a5",
      "scopes": [
        "team"
      ]
    }
  ],
  "name": {
    "short": "Sample App",
    "full": "Sample App"
  },
  "accentColor": "#FFFFFF",
  "needsIdentity": "true"
}
```

## <a name="test-your-connector"></a>Tester votre connecteur

Pour tester votre connecteur, téléchargez-le dans une équipe avec n'importe quelle autre application. Vous pouvez créer un package .zip à l’aide du fichier manifeste à partir des deux fichiers d’icône et du tableau de bord du développeur des connecteurs, modifié comme indiqué dans [Inclure le connecteur dans votre manifeste](#include-the-connector-in-your-manifest).

Une fois que vous avez téléchargé l’application, ouvrez la liste des connecteurs à partir de n’importe quel canal. Faites défiler la page vers le bas pour afficher votre application dans la section **Téléchargé** :

![Capture d’écran d’une section chargée dans la boîte de dialogue du connecteur](~/assets/images/connectors/connector_dialog_uploaded.png)

> [!NOTE]
> Le flux se produit entièrement dans Teams en tant qu’expérience hébergée.

Pour vérifier que l’`HttpPOST`action fonctionne correctement, [envoyez des messages à votre connecteur](~/webhooks-and-connectors/how-to/connectors-using.md).

Suivez le [guide pas à pas](../../sbs-teams-connectors.yml) pour créer et tester les connecteurs dans teams.

## <a name="distribute-webhook-and-connector"></a>Distribuer le webhook et le connecteur

1. [Configurez un webhook entrant](~/webhooks-and-connectors/how-to/add-incoming-webhook.md#create-an-incoming-webhook) directement pour votre équipe.

1. Ajoutez une [page de configuration](~/webhooks-and-connectors/how-to/connectors-creating.md?#integrate-the-configuration-experience) et publiez votre webhook entrant dans un connecteur Office 365.

1. Empaquetez et publiez votre connecteur dans le cadre de votre soumission [AppSource](~/concepts/deploy-and-publish/office-store-guidance.md) .

## <a name="code-sample"></a>Exemple de code

Le tableau suivant fournit l’exemple de nom et sa description :

|**Exemple de nom** | **Description** | **.NET** | **Node.js** |
|----------------|------------------|--------|----------------|
| Connecteurs | Exemple de connecteur Office 365 générant des notifications sur le canal Teams.| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-todo-notification/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-github-notification/nodejs)|
| Exemple de connecteurs génériques |Exemple de code pour un connecteur générique facile à personnaliser pour tout système qui prend en charge les webhooks.| | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-generic/nodejs)|

## <a name="step-by-step-guide"></a>Guide pas à pas

Suivez le [guide pas à pas](../../sbs-teams-connectors.yml) pour créer et tester un connecteur dans Teams.

## <a name="see-also"></a>Voir aussi

* [Créer et envoyer des messages](~/webhooks-and-connectors/how-to/connectors-using.md)
* [Créer un webhook entrant](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [Créer un connecteur Office 365](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [ Comment les administrateurs peuvent-ils activer ou désactiver les connecteurs ?](/MicrosoftTeams/office-365-custom-connectors#enable-or-disable-connectors-in-teams)
* [Comment les administrateurs peuvent publier des connecteurs personnalisés au sein de leur organisation ?](/MicrosoftTeams/office-365-custom-connectors)
