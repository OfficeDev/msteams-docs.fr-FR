---
title: Connecteurs Office 365
description: Décrit comment commencer avec les connecteurs Office 365 en Microsoft Teams
keywords: 'équipes connecteur O365 '
localization_priority: Normal
ms.topic: conceptual
ms.date: 04/19/2019
ms.openlocfilehash: 9eaaedf88d907dd7a7422068ab5d20450345f0e7
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566809"
---
# <a name="creating-office-365-connectors-for-microsoft-teams"></a>Création Office 365 connecteurs pour Microsoft Teams

>Avec Microsoft Teams applications, vous pouvez ajouter votre connecteur Office 365 existant ou en créer un nouveau pour l’inclure dans Microsoft Teams. Voir [Construire votre propre connecteur pour plus](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector) d’informations.

## <a name="adding-a-connector-to-your-teams-app"></a>Ajout d’un connecteur à votre application Teams’argent

Vous pouvez distribuer votre connecteur inscrit dans le cadre de votre package d’application Teams. Que ce soit en tant que solution autonome ou l’une des [plusieurs fonctionnalités](~/concepts/extensibility-points.md) que votre expérience permet en Teams, vous [pouvez emballer et](~/concepts/build-and-test/apps-package.md) [publier](~/concepts/deploy-and-publish/apps-publish.md) votre connecteur dans le cadre de votre soumission AppSource, ou vous pouvez le fournir directement aux utilisateurs pour téléchargement dans les Teams.

Pour distribuer votre connecteur, vous devez vous inscrire en utilisant le tableau de bord [des développeurs de connecteurs.](https://outlook.office.com/connectors/home/login/#/publish) Par défaut, une fois qu’un connecteur est enregistré, il est supposé que votre connecteur fonctionnera dans tous les produits Office 365 qui les soutiennent, y compris les Outlook et Teams. Si ce _n’est_ pas le cas et que vous devez créer un connecteur qui ne fonctionne qu’en Microsoft Teams, contactez-nous [directement à Microsoft Teams d’applications](mailto:teamsubm@microsoft.com).

> [!IMPORTANT]
> Une fois que vous **avez choisi Enregistrer** dans le tableau de bord des développeurs de connecteurs, votre connecteur est enregistré. Si vous souhaitez publier votre connecteur dans AppSource, suivez les instructions de [Publier votre application Microsoft Teams à AppSource](~/concepts/deploy-and-publish/apps-publish.md). Si vous ne souhaitez pas publier votre application dans AppSource, et plutôt simplement la distribuer directement à votre organisation uniquement, vous pouvez le faire en [publiant à votre organisation](#publish-connectors-for-your-organization). Si vous souhaitez uniquement publier sur votre organisation, aucune autre action n’est nécessaire sur le tableau de bord Connector.

### <a name="integrating-the-configuration-experience"></a>Intégration de l’expérience de configuration

Vos utilisateurs compléteront toute l’expérience de configuration connecteur sans avoir à quitter le Teams client. Pour réaliser cette expérience, Teams intégrera votre page de configuration directement dans un iframe. La séquence des opérations est la suivante :

1. L’utilisateur clique sur votre connecteur pour commencer le processus de configuration.
2. Teams chargera votre expérience de configuration en ligne.
3. L’utilisateur interagit avec votre expérience Web pour compléter la configuration.
4. L’utilisateur appuie sur « Enregistrer », ce qui déclenche un rappel dans votre code.
5. Votre code traitera l’événement d’sauvegarde en récupérant les paramètres webhook (documentés ci-dessous). Votre code doit ensuite stocker le webhook pour afficher des événements plus tard.

Vous pouvez réutiliser votre expérience de configuration Web existante ou créer une version distincte qui sera hébergée spécifiquement dans Teams. Votre code doit :

1. Incluez le Microsoft Teams JavaScript SDK. Cela donne à votre code l’accès aux API pour effectuer des opérations courantes comme obtenir le contexte utilisateur/canal/équipe actuel et initier des flux d’authentification. Initialisez le kit de développement logiciel (SDK) en appelant `microsoftTeams.initialize()`.
2. Appelez `microsoftTeams.settings.setValidityState(true)` lorsque vous souhaitez activer le bouton Enregistrer. Vous devez le faire en réponse à l’entrée utilisateur valide, comme une sélection ou une mise à jour sur le terrain.
3. Enregistrez `microsoftTeams.settings.registerOnSaveHandler()` un gestionnaire d’événements, qui est appelé lorsque l’utilisateur clique enregistrer.
4. Appelez `microsoftTeams.settings.setSettings()` pour enregistrer les paramètres du connecteur. Ce qui est enregistré ici est également ce qui sera affiché dans le dialogue de configuration si l’utilisateur tente de mettre à jour une configuration existante pour votre connecteur.
5. Appelez `microsoftTeams.settings.getSettings()` pour récupérer les propriétés webhook, y compris l’URL elle-même. Vous devez appeler cela En plus de l’événement enregistrer, vous devez également appeler cela lorsque votre page est chargée pour la première fois dans le cas d’une re-configuration.
6. (Facultatif) Enregistrez `microsoftTeams.settings.registerOnRemoveHandler()` un gestionnaire d’événements, qui est appelé lorsque l’utilisateur supprime votre connecteur. Cet événement donne à votre service l’occasion d’effectuer toutes les actions de nettoyage.

Voici un exemple HTML pour créer une page de configuration Connector sans le CSS :

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

#### <a name="getsettings-response-properties"></a>`GetSettings()` propriétés de réponse

>[!Note]
>Les paramètres retournés par `getSettings` l’appel ici sont différents que si vous deuriez invoquer cette méthode à partir d’un onglet, et diffèrent de ceux documentés [ici](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest&preserve-view=true).

| Paramètre   | Détails |
|-------------|---------|
| `entityId`       | L’ID de l’entité, tel qu’il est défini par votre code lors de l’appel `setSettings()` . |
| `configName`  | Le nom de configuration, tel que défini par votre code lors de l’appel `setSettings()` . |
| `contentUrl` | L’URL de la page de configuration, tel que défini par votre code lors de l’appel `setSettings()` . |
| `webhookUrl` | L’URL webhook créée pour ce connecteur. Persistez l’URL webhook et utilisez-la pour POSTER JSON structuré pour envoyer des cartes au canal. L’élément `webhookUrl` est renvoyé uniquement lorsque l’application effectue un renvoi. |
| `appType` | Les valeurs renvoyées peuvent être `mail`, `groups` ou `teams` correspondant à la messagerie Office 365, aux groupes Office 365 ou à Microsoft Teams. |
| `userObjectId` | Il s’agit de l’id unique correspondant Office 365 utilisateur qui a initié la configuration du connecteur. Il doit être sécurisé. Cette valeur peut être utilisée pour associer l’utilisateur dans Office 365 qui a défini la configuration à l’utilisateur dans votre service. |

Si vous devez authentifier l’utilisateur dans le cadre du chargement de votre page à l’étape 2 ci-dessus, consultez ce [lien pour](~/tabs/how-to/authentication/auth-flow-tab.md) plus de détails sur la façon dont vous pouvez intégrer la connexion lorsque votre page est intégrée.

> [!NOTE]
> Pour des raisons de compatibilité inter-clients, votre code devra appeler avec `microsoftTeams.authentication.registerAuthenticationHandlers()` l’URL et les méthodes de rappel de succès/échec avant d’appeler `authenticate()` .

#### <a name="handling-edits"></a>Manipulation des modifications

Votre code doit gérer les utilisateurs qui reviennent dans le but de modifier une configuration de connecteur existante. Pour ce faire, appelez `microsoftTeams.settings.setSettings()` lors de la configuration initiale avec les paramètres suivants :

- `entityId` est l’iD personnalisé qui est compris par votre service et représente ce que l’utilisateur a configuré.
- `configName` est un nom amical que votre code de configuration peut récupérer
- `contentUrl` est une URL personnalisée qui est chargée lorsqu’un utilisateur modifie une configuration de connecteur existante. Vous pouvez utiliser cette URL pour faciliter le gestion de l’étui de modification par votre code.

En règle générale, cet appel est effectué dans le cadre de votre gestionnaire d’événements d’enregistrer. Ensuite, lorsque ce qui `contentUrl` précède est chargé, votre code doit appeler `getSettings()` pour prépeupler tous les paramètres ou formulaires de votre interface utilisateur de configuration.

#### <a name="handling-removals"></a>Traitement des déménagements

Vous pouvez exécuter un gestionnaire d’événements en option lorsque l’utilisateur supprime une configuration de connecteur existante. Vous enregistrez ce gestionnaire en appelant `microsoftTeams.settings.registerOnRemoveHandler()` . Ce gestionnaire peut être utilisé pour effectuer des opérations de nettoyage telles que la suppression des entrées d’une base de données.

### <a name="including-the-connector-in-your-manifest"></a>Inclure le connecteur dans votre manifeste

Vous pouvez télécharger le manifeste d’application Teams généré automatiquement à partir du portail. Avant de pouvoir l’utiliser pour tester ou publier votre application, cependant, vous devez faire ce qui suit:

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

Vous pouvez à présent lancer l’expérience de configuration. Sachez que ce flux se produit entièrement dans Microsoft Teams comme une expérience hébergée.

Pour vérifier `HttpPOST` qu’une action fonctionne correctement, envoyez [des messages à votre connecteur](~/webhooks-and-connectors/how-to/connectors-using.md).

## <a name="publish-connectors-for-your-organization"></a>Publiez connecteurs pour votre organisation

Parfois, vous ne souhaitez peut-être pas publier votre application connecteur sur l’AppSource/Store public, mais vous souhaitez qu’elle ne soit disponible que pour les utilisateurs de votre organisation. Dans de tels cas, vous pouvez télécharger votre application de connecteur personnalisée sur le [catalogue d’applications de votre organisation.](~/concepts/deploy-and-publish/apps-publish.md) De cette façon, votre application de connecteur ne sera disponible que pour cette organisation, et vous n’aurez pas besoin de publier votre connecteur au magasin public.

Une fois que vous avez téléchargé votre paquet d’applications, pour configurer et utiliser le connecteur dans une équipe, il peut être installé à partir du catalogue d’applications de l’organisation en suivant ces étapes :

1. Sélectionnez l’icône apps à partir de la barre de navigation verticale d’extrême gauche.
1. Dans la **fenêtre Apps** sélectionnez **Connecteurs**.
1. Sélectionnez le connecteur que vous souhaitez ajouter et une fenêtre de dialogue contexturée s’affichera.
1. Sélectionnez **l’ajout à une barre** d’équipe.
1. Dans la fenêtre de dialogue suivante, tapez une équipe ou un nom de canal.
1. Sélectionnez la **barre de connecteur de** l’angle inférieur droit de la fenêtre de dialogue.
1. Le connecteur sera disponible dans la section &#9679;&#9679;&#9679; => *options*  =>  *Connecteurs*  =>  *Tous*  =>  *connecteurs pour votre équipe* pour cette équipe. Vous pouvez naviguer en faisant défiler vers cette section ou rechercher l’application connecteur.
1. Pour configurer ou modifier le connecteur, sélectionnez **la barre Configure.**

## <a name="code-sample"></a>Exemple de code
|**Nom de l’échantillon** | **Description** | **.NET (en)** | **Node.js** |
|----------------|------------------|--------|----------------|
| Connecteurs    | Exemple Office 365 connecteur générant des notifications au canal des équipes.|   [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-todo-notification/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-github-notification/nodejs)|
| Échantillon générique de connecteurs |Exemple de code pour un connecteur générique facile à personnaliser pour n’importe quel système qui prend en charge les webhooks.|  | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-generic/nodejs)|
