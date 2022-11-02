---
title: Créer une page de configuration
author: surbhigupta
description: Créer une page de configuration pour collecter des informations auprès de l’utilisateur. Obtenez également des données de contexte pour les onglets Microsoft Teams, en savoir plus sur l’authentification, modifier ou supprimer des onglets.
ms.localizationpriority: high
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 6cd9ed8572b3df2db4a727225159774156008fa6
ms.sourcegitcommit: 9ea9a70d2591bce6b8c980d22014e160f7b45f91
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/02/2022
ms.locfileid: "68820170"
---
# <a name="create-a-configuration-page"></a>Créer une page de configuration

Une page de configuration est un type particulier de [page de contenu](content-page.md). Les utilisateurs configurent certains aspects de l'application Microsoft Teams à l'aide de la page de configuration et utilisent cette configuration dans le cadre de ce qui suit :

* Un onglet de canal ou de groupe de discussion : Recueillir des informations auprès des utilisateurs et `contentUrl`définir le de la page de contenu à afficher.
* Une [extension du message](~/messaging-extensions/what-are-messaging-extensions.md).
* Un [connecteur Office 365](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md).

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

## <a name="configure-a-channel-or-group-chat-tab"></a>Configurer un onglet de canal ou de groupe de conversation

L'application doit faire référence au SDK client [JavaScript de Microsoft Teams ](/javascript/api/overview/msteams-client)et appeler`app.initialize()`. Les URL utilisées doivent être des points de terminaison HTTPS sécurisés et sont disponibles à partir du cloud.

### <a name="example"></a>Exemple

Un exemple de page de configuration est présenté dans l'image suivante :

:::image type="content" source="../../../assets/images/tab-images/configuration-page.png" alt-text="Capture d’écran montrant la page de configuration.":::

Le code suivant est un exemple de code correspondant à la page de configuration :

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

```html
<head>
    <script src="https://res.cdn.office.net/teams-js/2.2.0/js/MicrosoftTeams.min.js" 
      integrity="sha384yBjE++eHeBPzIg+IKl9OHFqMbSdrzY2S/LW3qeitc5vqXewEYRWegByWzBN/chRh" 
      crossorigin="anonymous" >
    </script>
<body>
    <button onclick="(document.getElementById('icon').src = '/images/iconGray.png'); colorClickGray()">Select Gray</button>
    <img id="icon" src="/images/teamsIcon.png" alt="icon" style="width:100px" />
    <button onclick="(document.getElementById('icon').src = '/images/iconRed.png'); colorClickRed()">Select Red</button>

    <script>
        await microsoftTeams.app.initialize();
        let saveGray = () => {
            microsoftTeams.pages.config.registerOnSaveHandler((saveEvent) => {
                const configPromise = pages.config.setConfig({
                    websiteUrl: "https://yourWebsite.com",
                    contentUrl: "https://yourWebsite.com/gray",
                    entityId: "grayIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                configPromise.
                    then((result) => {saveEvent.notifySuccess()}).
                    catch((error) => {saveEvent.notifyFailure("failure message")});
            });
        }

        let saveRed = () => {
            microsoftTeams.pages.config.registerOnSaveHandler((saveEvent) => {
                const configPromise = pages.config.setConfig({
                    websiteUrl: "https://yourWebsite.com",
                    contentUrl: "https://yourWebsite.com/red",
                    entityId: "redIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                configPromise.
                    then((result) => {saveEvent.notifySuccess();}).
                    catch((error) => {saveEvent.notifyFailure("failure message")});
            });
        }

        let gr = document.getElementById("gray").style;
        let rd = document.getElementById("red").style;

        const colorClickGray = () => {
            gr.display = "block";
            rd.display = "none";
            microsoftTeams.pages.config.setValidityState(true);
            saveGray()
        }

        const colorClickRed = () => {
            rd.display = "block";
            gr.display = "none";
            microsoftTeams.pages.config.setValidityState(true);
            saveRed();
        }
    </script>
    ...
</body>
```

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

```html
<head>
    <script src='https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js'></script>
</head>
<body>
    <button onclick="(document.getElementById('icon').src = '/images/iconGray.png'); colorClickGray()">Select Gray</button>
    <img id="icon" src="/images/teamsIcon.png" alt="icon" style="width:100px" />
    <button onclick="(document.getElementById('icon').src = '/images/iconRed.png'); colorClickRed()">Select Red</button>

    <script>
        microsoftTeams.initialize();
        let saveGray = () => {
            microsoftTeams.settings.registerOnSaveHandler((saveEvent) => {
                microsoftTeams.settings.setSettings({
                    websiteUrl: "https://yourWebsite.com",
                    contentUrl: "https://yourWebsite.com/gray",
                    entityId: "grayIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                saveEvent.notifySuccess();
            });
        }
        let saveRed = () => {
            microsoftTeams.settings.registerOnSaveHandler((saveEvent) => {
                microsoftTeams.settings.setSettings({
                    websiteUrl: "https://yourWebsite.com",
                    contentUrl: "https://yourWebsite.com/red",
                    entityId: "redIconTab",
                    suggestedDisplayName: "MyNewTab"
                });
                saveEvent.notifySuccess();
            });
        }

        let gr = document.getElementById("gray").style;
        let rd = document.getElementById("red").style;

        const colorClickGray = () => {
            gr.display = "block";
            rd.display = "none";
            microsoftTeams.settings.setValidityState(true);
            saveGray()
        }

        const colorClickRed = () => {
            rd.display = "block";
            gr.display = "none";
            microsoftTeams.settings.setValidityState(true);
            saveRed();
        }
    </script>
    ...
</body>
```

***
Choisissez le bouton **Sélectionner le gris** ou **Sélectionner le rouge** dans la page de configuration, pour afficher le contenu de l'onglet avec une icône grise ou rouge.

L'image suivante affiche le contenu de l'onglet avec l'icône **gris** sélectionné :

:::image type="content" source="../../../assets/images/tab-images/configure-tab-with-gray.png" alt-text="Capture d’écran montrant l’onglet Configurer avec la sélection grise.":::

L'image suivante affiche le contenu de l'onglet avec l'icône **rouge** sélectionnée :

:::image type="content" source="../../../assets/images/tab-images/configure-tab-with-red.png" alt-text="Capture d’écran montrant l’onglet Configurer avec la sélection rouge.":::

Le fait de choisir le bouton approprié déclenche l'une ou l'autre `saveGray()`ou `saveRed()`, et invoque ce qui suit :

* Défini `pages.config.setValidityState(true)`à vrai.
* Le `pages.config.registerOnSaveHandler()`gestionnaire d'événements est déclenché.
* **Enregistrer** sur la page de configuration de l'application, est activé.

Le code de la page de configuration informe Teams que les exigences de configuration sont remplies et que l’installation peut se poursuivre. Lorsque l’utilisateur sélectionne **Enregistrer**, les paramètres sont `pages.config.setConfig()` définis, comme défini par l’interface `Config` . Pour plus d’informations, consultez [interface de configuration](/javascript/api/@microsoft/teams-js/pages.config?). `saveEvent.notifySuccess()` est appelé pour indiquer que l'URL du contenu a été résolu avec succès.

>[!NOTE]
>
>* Vous avez 30 secondes pour terminer l’opération d’enregistrement (le rappel à `registerOnSaveHandler`) avant le délai d’expiration. Une fois le délai écoulé, un message d'erreur générique apparaît.
>* Si vous enregistrez un gestionnaire de sauvegarde à l'aide de , la fonction de `registerOnSaveHandler()`rappel doit invoquer `saveEvent.notifySuccess()`ou`saveEvent.notifyFailure()` pour indiquer le résultat de la configuration.
>* Si vous n'enregistrez pas de gestionnaire d'enregistrement, `saveEvent.notifySuccess()`l'appel est effectué automatiquement lorsque l'utilisateur sélectionne **Enregistrer**.
>* Assurez-vous d’avoir un unique `entityId`. Redirige en double `entityId` vers la première instance de l’onglet.

### <a name="get-context-data-for-your-tab-settings"></a>Obtenez des données contextuelles pour les paramètres de votre onglet

Votre onglet nécessite des informations contextuelles pour afficher un contenu pertinent. Les informations contextuelles renforcent encore l'attrait de votre onglet en offrant une expérience utilisateur plus personnalisée.

Pour plus d'informations sur les propriétés utilisées pour la configuration des onglets, voir [Interface contextuelle](/javascript/api/@microsoft/teams-js/app.context?view=msteams-client-js-latest&preserve-view=true). Recueillez les valeurs des variables de données contextuelles des deux manières suivantes :

* Insérez des chaînes de requête d'URL dans le manifeste. `configurationURL`.

* Utilisez la [méthode du SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `app.getContext()`Teams.

#### <a name="insert-placeholders-in-the-configurationurl"></a>Insérer des espaces réservés dans le `configurationUrl`

Ajouter des espaces réservés à l'interface contextuelle à votre base `configurationUrl`. Par exemple :

##### <a name="base-url"></a>URL de base

```json
...
"configurationUrl": "https://yourWebsite/config",
...
```

#### <a name="base-url-with-query-strings"></a>URL de base avec chaînes d'interrogation

```json
...
"configurationUrl": "https://yourWebsite/config?team={teamId}&channel={channelId}&{locale}"
...
```

Une fois votre page téléchargée, Teams met à jour les espaces réservés aux chaînes de requête avec les valeurs pertinentes. Incluez une logique dans la page de configuration pour récupérer et utiliser ces valeurs. Pour plus d'informations sur l'utilisation des chaînes de requête d'URL, voir [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) dans MDN Web Docs. L'exemple de code suivant permet d'extraire une valeur de la `configurationUrl`propriété :

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

```html
<script>
   await microsoftTeams.app.initialize();
   const getId = () => {
        let urlParams = new URLSearchParams(document.location.search.substring(1));
        let blueTeamId = urlParams.get('team');
        return blueTeamId
    }
//For testing, you can invoke the following to view the pertinent value:
document.write(getId());
</script>
```

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

```html
<script>
   microsoftTeams.initialize();
   const getId = () => {
        let urlParams = new URLSearchParams(document.location.search.substring(1));
        let blueTeamId = urlParams.get('team');
        return blueTeamId
    }
//For testing, you can invoke the following to view the pertinent value:
document.write(getId());
</script>
```

***

### <a name="use-the-getcontext-function-to-retrieve-context"></a>Utilisez `getContext()`la fonction pour récupérer le contexte

La `app.getContext()` fonction retourne une promesse qui se résout avec l’objet [d’interface de contexte](/javascript/api/@microsoft/teams-js/pages?view=msteams-client-js-latest&preserve-view=true) .

Le code suivant fournit un exemple d'ajout de cette fonction à la page de configuration pour récupérer les valeurs du contexte :

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

```html
<!-- `userPrincipalName` will render in the span with the id "user". -->

<span id="user"></span>
...
<script type="module">
    import {app} from 'https://res.cdn.office.net/teams-js/2.0.0/js/MicrosoftTeams.min.js';
    const contextPromise = app.getContext();
    contextPromise.
        then((context) => {
            let userId = document.getElementById('user');
            userId.innerHTML = context.user.userPrincipalName;
        }).
        catch((error) => {/*Unsuccessful operation*/});
</script>
...
```

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

```html
<!-- `userPrincipalName` will render in the span with the id "user". -->

<span id="user"></span>
...
<script>
    microsoftTeams.getContext((context) =>{
        let userId = document.getElementById('user');
        userId.innerHTML = context.userPrincipalName;
    });
</script>
...
```

***

## <a name="context-and-authentication"></a>Contexte et authentification

Authentifiez-vous avant de permettre à un utilisateur de configurer votre application. Sinon, votre contenu pourrait inclure des sources qui ont leurs protocoles d'authentification. Pour plus d'informations, voir [authentifier un utilisateur dans un onglet Microsoft Teams](~/tabs/how-to/authentication/auth-flow-tab.md) . Utilisez les informations contextuelles pour construire les demandes d'authentification et les URL des pages d'autorisation. Assurez-vous que tous les domaines utilisés dans vos pages d'onglet sont répertoriés dans le `manifest.json`tableau`validDomains` et.

## <a name="modify-or-remove-a-tab"></a>Modifier ou supprimer un onglet

Définissez la propriété de `canUpdateConfiguration` votre manifeste sur `true`. Il permet aux utilisateurs de modifier ou de reconfigurer un onglet de canal ou de groupe. Vous pouvez renommer votre onglet uniquement via l’interface utilisateur de Teams. Informez l’utilisateur de l’impact sur le contenu lorsqu’un onglet est supprimé. Pour ce faire, incluez une page d’options de suppression dans l’application et définissez une valeur pour la `removeUrl` propriété dans la `setConfig()` configuration (anciennement `setSettings()`). L’utilisateur peut désinstaller les onglets personnels, mais ne peut pas les modifier. Pour plus d’informations, consultez [créer une page de suppression pour votre onglet](~/tabs/how-to/create-tab-pages/removal-page.md).

Page de configuration de Microsoft Teams `setConfig()` (anciennement `setSettings()`) pour la suppression :

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

```javascript
import { pages } from "@microsoft/teams-js";
const configPromise = pages.config.setConfig({
    contentUrl: "add content page URL here",
    entityId: "add a unique identifier here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "add website URL here //Required field for configurable tabs on Mobile Clients",
    removeUrl: "add removal page URL here"
});
configPromise.
    then((result) => {/*Successful operation*/).
    catch((error) => {/*Unsuccessful operation*/});
```

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add a unique identifier here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "add website URL here //Required field for configurable tabs on Mobile Clients",
    removeUrl: "add removal page URL here"
});
```

***

## <a name="mobile-clients"></a>Clients mobiles

Si vous choisissez de faire apparaître votre onglet de canal ou de groupe sur les clients mobiles Teams, la `setConfig()`configuration doit avoir une valeur pour `websiteUrl`. Pour plus d'informations, voir [les conseils pour les onglets sur les téléphones portables.](~/tabs/design/tabs-mobile.md)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créer une page de retrait pour votre onglet](~/tabs/how-to/create-tab-pages/removal-page.md)

## <a name="see-also"></a>Voir aussi

* [Créer des onglets pour Teams](../../what-are-tabs.md)
* [Mettre à jour le manifeste d’application pour l’authentification unique et l’application en préversion](../authentication/tab-sso-manifest.md)
* [Configurer l’authentification d’un fournisseur d’identité OAuth tiers](../authentication/auth-tab-aad.md)
* [Créer des connecteurs Office 365](../../../webhooks-and-connectors/how-to/connectors-creating.md)
* [Obtenir un contexte Teams pour votre onglet](../access-teams-context.md)
* [Onglets sur les appareils mobiles](../../design/tabs-mobile.md)
