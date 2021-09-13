---
title: Créer des connecteurs Office 365
author: laujan
description: Décrit comment commencer avec les connecteurs Office 365 dans Microsoft Teams
keywords: 'équipes connecteur O365 '
ms.localizationpriority: medium
ms.topic: conceptual
ms.date: 06/16/2021
ms.openlocfilehash: 39c2533f112f5cb3c72446ad8a5638687dd3db2e
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/12/2021
ms.locfileid: "59155520"
---
# <a name="create-office-365-connectors"></a>Créer des connecteurs Office 365

Avec Microsoft Teams applications, vous pouvez ajouter votre connecteur Office 365 existant ou en créer un nouveau dans Teams. Pour plus d’informations, [voir créer votre propre connecteur.](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector)

## <a name="add-a-connector-to-teams-app"></a>Ajouter un connecteur à Teams application

Vous pouvez [packager](~/concepts/build-and-test/apps-package.md) [et publier](~/concepts/deploy-and-publish/apps-publish.md) votre connecteur dans le cadre de votre soumission AppSource. Vous pouvez distribuer votre connecteur inscrit dans le cadre de votre package Teams’application. Pour plus d’informations sur les points d’entrée Teams’application, voir [fonctionnalités.](~/concepts/extensibility-points.md) Vous pouvez également fournir le package aux utilisateurs directement pour le chargement dans Teams.

Pour distribuer votre connecteur, vous devez vous inscrire via [le Tableau de bord du développeur de connecteurs.](https://outlook.office.com/connectors/home/login/#/publish) Lorsqu’un connecteur est inscrit, il est supposé qu’il fonctionne dans tous les produits Office 365 qui prend en charge les applications, y compris Outlook et Teams. Si ce n’est pas le cas et que vous devez créer un connecteur qui fonctionne uniquement dans Microsoft Teams, contactez : Microsoft Teams [e-mail soumissions d’applications](mailto:teamsubm@microsoft.com).

> [!IMPORTANT]
> Votre connecteur est enregistré après avoir sélectionné **Enregistrer** dans le tableau de bord du développeur de connecteurs. Si vous souhaitez publier votre connecteur dans AppSource, suivez les instructions de publication de votre [application Microsoft Teams dans AppSource.](~/concepts/deploy-and-publish/apps-publish.md) Si vous ne souhaitez pas publier votre application dans AppSource, distribuez-la directement à l’organisation. Après [la publication des connecteurs pour votre organisation,](#publish-connectors-for-the-organization)aucune action supplémentaire n’est requise sur le tableau de bord du connecteur.

### <a name="integrate-the-configuration-experience"></a>Intégrer l’expérience de configuration

Les utilisateurs peuvent terminer toute l’expérience de configuration du connecteur sans avoir à quitter Teams client. Pour obtenir l’expérience, Teams pouvez incorporer votre page de configuration directement dans un iframe. La séquence d’opérations est la suivante :

1. L’utilisateur sélectionne le connecteur pour commencer le processus de configuration.
1. L’utilisateur interagit avec l’expérience web pour terminer la configuration.
1. L’utilisateur sélectionne **Enregistrer,** ce qui déclenche un rappel dans le code.

    > [!NOTE]
    > * Le code peut traiter l’événement d’enregistrer en récupérant les paramètres de webhook. Votre code stocke le webhook pour publier des événements ultérieurement.
    > * L’expérience de configuration est chargée en ligne dans Teams.

Vous pouvez réutiliser votre expérience de configuration web existante ou créer une version distincte à héberger spécifiquement dans Teams. Votre code doit inclure le Microsoft Teams SDK JavaScript. Cela permet à votre code d’accéder aux API pour effectuer des opérations courantes, telles que l’obtention du contexte de l’utilisateur, du canal ou de l’équipe actuel et lancer des flux d’authentification.

**Pour intégrer l’expérience de configuration**

1. Initialisez le kit de développement logiciel (SDK) en appelant `microsoftTeams.initialize()`.
1. Appel `microsoftTeams.settings.setValidityState(true)` pour activer **Enregistrer**.

    > [!NOTE]
    > Vous devez appeler `microsoftTeams.settings.setValidityState(true)` en réponse à la sélection de l’utilisateur ou à la mise à jour du champ.

1. Enregistrez  `microsoftTeams.settings.registerOnSaveHandler()` le handler d’événements, qui est appelé lorsque l’utilisateur sélectionne **Enregistrer**.
1. Appelez `microsoftTeams.settings.setSettings()` pour enregistrer les paramètres du connecteur. Les paramètres enregistrés sont également affichés dans la boîte de dialogue de configuration si l’utilisateur tente de mettre à jour une configuration existante pour votre connecteur.
1. Appelez `microsoftTeams.settings.getSettings()` pour récupérer les propriétés du webhook, y compris l’URL.

    > [!NOTE]
    > Vous devez appeler lorsque votre page est chargée pour la première fois `microsoftTeams.settings.getSettings()` en cas de reconfiguration.

1. Enregistrez `microsoftTeams.settings.registerOnRemoveHandler()` le handler d’événements, qui est appelé lorsque l’utilisateur supprime le connecteur.

Cet événement permet à votre service d’effectuer des actions de nettoyage.

Le code suivant fournit un exemple de code HTML pour créer une page de configuration de connecteur sans le support technique et le service clientèle :

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

Pour authentifier l’utilisateur dans le cadre du chargement de votre page, consultez flux d’authentification pour les [onglets](~/tabs/how-to/authentication/auth-flow-tab.md) pour intégrer la signature lorsque votre page est incorporée.

> [!NOTE]
> Pour des raisons de compatibilité entre clients, votre code doit appeler avec l’URL et les méthodes de rappel de réussite ou `microsoftTeams.authentication.registerAuthenticationHandlers()` d’échec avant d’appeler. `authenticate()`

#### <a name="getsettings-response-properties"></a>`GetSettings` propriétés de réponse

>[!NOTE]
>Les paramètres renvoyés par l’appel sont différents lorsque vous appelez cette méthode à partir d’un onglet et diffèrent de ceux `getSettings` documentés dans [les paramètres js](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest&preserve-view=true).

Le tableau suivant fournit les paramètres et les détails des propriétés `GetSetting` de réponse :

| Paramètres   | Détails |
|-------------|---------|
| `entityId`       | L’ID d’entité, tel que définie par votre code lors de `setSettings()` l’appel. |
| `configName`  | Nom de la configuration, tel que définie par votre code lors de `setSettings()` l’appel. |
| `contentUrl` | URL de la page de configuration, définie par votre code lors de `setSettings()` l’appel. |
| `webhookUrl` | URL de webhook créée pour le connecteur. Utilisez l’URL de webhook pour post JSON structuré pour envoyer des cartes au canal. Elle `webhookUrl` est renvoyée uniquement lorsque l’application renvoie des données avec succès. |
| `appType` | Les valeurs renvoyées peuvent être `mail` `groups` respectivement Office 365 `teams` mail, Office 365 ou Microsoft Teams. |
| `userObjectId` | ID unique correspondant à l’Office 365 qui a initié la mise en place du connecteur. Elle doit être sécurisée. Cette valeur peut être utilisée pour associer l’utilisateur Office 365, qui a installé la configuration dans votre service. |

#### <a name="handle-edits"></a>Gérer les modifications

Votre code doit gérer les utilisateurs qui reviennent pour modifier une configuration de connecteur existante. Pour ce faire, appelez `microsoftTeams.settings.setSettings()` pendant la configuration initiale avec les paramètres suivants :

- `entityId` est l’ID personnalisé qui représente ce que l’utilisateur a configuré et compris par votre service.
- `configName` est un nom que le code de configuration peut récupérer.
- `contentUrl` est une URL personnalisée qui est chargée lorsqu’un utilisateur modifie une configuration de connecteur existante.

Cet appel est effectué dans le cadre de votre économiseur d’événements. Ensuite, lorsque le code est chargé, votre code doit appeler pour pré-remplir les paramètres ou `contentUrl` `getSettings()` formulaires de votre interface utilisateur de configuration.

#### <a name="handle-removals"></a>Gérer les suppressions

Vous pouvez exécuter un programme de gestion d’événements lorsque l’utilisateur supprime une configuration de connecteur existante. Vous inscrivez ce handler en appelant `microsoftTeams.settings.registerOnRemoveHandler()` . Ce handler est utilisé pour effectuer des opérations de nettoyage, telles que la suppression d’entrées d’une base de données.

### <a name="include-the-connector-in-your-manifest"></a>Inclure le connecteur dans votre manifeste

Téléchargez la version automatique générée `Teams app manifest` à partir du portail. Avant de tester ou de publier l’application, effectuez les étapes suivantes :

1. [Incluez deux icônes](../../concepts/build-and-test/apps-package.md#app-icons).
1. Modifiez la partie du manifeste pour inclure les noms de fichier des icônes au lieu `icons` des URL.

Le fichier manifest.jssuivant contient les éléments nécessaires pour tester et soumettre l’application :

> [!NOTE]
> Remplacez `id` `connectorId` et dans l’exemple suivant par le GUID du connecteur.

#### <a name="example-of-manifestjson-with-connector"></a>Exemple d'manifest.jsavec connecteur

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

## <a name="enable-or-disable-connectors-in-teams"></a>Activer ou désactiver des connecteurs dans Teams

Le module Exchange Online PowerShell V2 utilise l’authentification moderne et fonctionne avec l’authentification multifacteur, appelée authentification multifacteur, pour la connexion à tous les environnements PowerShell Exchange dans Microsoft 365. Les administrateurs peuvent utiliser Exchange Online PowerShell pour désactiver les connecteurs pour un client entier ou une boîte aux lettres de groupe spécifique, affectant tous les utilisateurs de ce client ou de cette boîte aux lettres. Il n’est pas possible de désactiver pour certains et non pour d’autres. En outre, les connecteurs sont désactivés par défaut pour Cloud de la communauté du secteur public, appelés Cloud de la communauté du secteur public client.

Le paramètre au niveau du client remplace le paramètre au niveau du groupe. Par exemple, si un administrateur active les connecteurs pour le groupe et les désactive sur le client, les connecteurs pour le groupe sont désactivés. Pour activer un connecteur dans Teams, connectez-vous à [Exchange Online PowerShell](/powershell/exchange/connect-to-exchange-online-powershell?view=exchange-ps#connect-to-exchange-online-powershell-using-modern-authentication-with-or-without-mfa&preserve-view=true) à l’aide de l’authentification moderne avec ou sans authentification multifacteur.

### <a name="commands-to-enable-or-disable-connectors"></a>Commandes permettant d’activer ou de désactiver des connecteurs

Dans Exchange Online PowerShell, exécutez les commandes suivantes :

* Pour désactiver les connecteurs pour le client : `Set-OrganizationConfig -ConnectorsEnabled:$false` .
* Pour désactiver les messages actionnables pour le client : `Set-OrganizationConfig -ConnectorsActionableMessagesEnabled:$false` .
* Pour activer les connecteurs pour Teams, exécutez les commandes suivantes :
  * `Set-OrganizationConfig -ConnectorsEnabled:$true `
  * `Set-OrganizationConfig -ConnectorsEnabledForTeams:$true`
  * `Set-OrganizationConfig -ConnectorsActionableMessagesEnabled:$true`

Pour plus d’informations sur l’échange de module PowerShell, voir [Set-OrganizationConfig](/powershell/module/exchange/Set-OrganizationConfig?view=exchange-ps&preserve-view=true). Pour activer ou désactiver les connecteurs Outlook, [connectez](https://support.microsoft.com/topic/connect-apps-to-your-groups-in-outlook-ed0ce547-038f-4902-b9b3-9e518ae6fbab?ui=en-us&rs=en-us&ad=us)des applications à vos groupes dans Outlook .

## <a name="test-your-connector"></a>Tester votre connecteur

Pour tester votre connecteur, téléchargez-le vers une équipe avec n’importe quelle autre application. Vous pouvez créer un package .zip à l’aide du fichier manifeste à partir des deux fichiers d’icône et connecteurs du Tableau de bord du développeur, modifié comme indiqué dans Inclure le connecteur dans [votre manifeste.](#include-the-connector-in-your-manifest)

Après avoir téléchargé l’application, ouvrez la liste des connecteurs à partir de n’importe quel canal. Faites défiler vers le bas pour voir votre application dans la section **Téléchargée** :

![Capture d’écran d’une section téléchargée dans la boîte de dialogue connecteur](~/assets/images/connectors/connector_dialog_uploaded.png)

> [!NOTE]
> Le flux se produit entièrement au sein Microsoft Teams en tant qu’expérience hébergée.

Pour vérifier que `HttpPOST` l’action fonctionne correctement, [envoyez des messages à votre connecteur.](~/webhooks-and-connectors/how-to/connectors-using.md)

## <a name="publish-connectors-for-the-organization"></a>Publier des connecteurs pour l’organisation

Si vous souhaitez que le connecteur soit disponible uniquement pour les utilisateurs de votre organisation, vous pouvez télécharger votre application de connecteur personnalisée dans le catalogue [d’applications de votre organisation.](~/concepts/deploy-and-publish/apps-publish.md)

Après avoir téléchargé le package d’application pour configurer et utiliser le connecteur dans une équipe, installez le connecteur à partir du catalogue d’applications de l’organisation.

**Pour configurer un connecteur**

1. Sélectionnez **Applications** dans la barre de navigation de gauche.
1. Dans la section **Applications,** sélectionnez **Connecteurs.**
1. Sélectionnez le connecteur que vous souhaitez ajouter. Une fenêtre de boîte de dialogue s’affiche.
1. Dans le menu déroulant, **sélectionnez Ajouter à une équipe.**
1. Dans la zone de recherche, tapez un nom d’équipe ou de canal.
1. Sélectionnez **Configurer un connecteur dans** le menu déroulant dans le coin inférieur droit de la fenêtre de dialogue.

> [!IMPORTANT]
> Actuellement, les connecteurs personnalisés ne sont pas disponibles dans Cloud de la communauté du secteur public (Cloud de la communauté du secteur public), Cloud de la communauté du secteur public-High et le Département de la Défense (DOD).

Le connecteur est disponible dans la section &#9679;&#9679;&#9679; > **Plus d’options** Connecteurs Tous les connecteurs pour  >    >    >  **votre** équipe pour cette équipe. Vous pouvez naviguer en accédant à cette section ou rechercher l’application connecteur. Pour configurer ou modifier le connecteur, sélectionnez **Configurer**.

## <a name="distribute-webhook-and-connector"></a>Distribuer le webhook et le connecteur

1. [Configurer un webhook entrant](~/webhooks-and-connectors/how-to/add-incoming-webhook.md?branch=pr-en-us-3076#create-incoming-webhook) directement pour votre équipe.
1. Ajoutez [une page de configuration](~/webhooks-and-connectors/how-to/connectors-creating.md?branch=pr-en-us-3076#integrate-the-configuration-experience) et [publiez votre webhook entrant](~/webhooks-and-connectors/how-to/connectors-creating.md?branch=pr-en-us-3076#publish-connectors-for-the-organization) dans un connecteur O365.
1. Packagez et publiez votre connecteur dans le cadre de [votre soumission AppSource.](~/concepts/deploy-and-publish/office-store-guidance.md)

## <a name="code-sample"></a>Exemple de code

Le tableau suivant fournit le nom de l’exemple et sa description :

|**Exemple de nom** | **Description** | **.NET** | **Node.js** |
|----------------|------------------|--------|----------------|
| Connecteurs    | Exemple Office 365 connecteur générant des notifications vers Teams canal.|   [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-todo-notification/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-github-notification/nodejs)|
| Exemple de connecteurs génériques |Exemple de code pour un connecteur générique facile à personnaliser pour tout système qui prend en charge les webhooks.|  | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-generic/nodejs)|

## <a name="see-also"></a>Voir aussi

* [Créer et envoyer des messages](~/webhooks-and-connectors/how-to/connectors-using.md)
* [Créer un webhook entrant](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [Créer un connecteur Office 365](~/webhooks-and-connectors/how-to/connectors-creating.md)
