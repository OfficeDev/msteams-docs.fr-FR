---
title: Créer une page de configuration
author: surbhigupta
description: Comment créer une page de configuration
keywords: Canal de groupe onglets teams configurable
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: f3781cdf8be3bf39480511258616c1e5dc5dedc107910480a3b02758fa28610c
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/07/2021
ms.locfileid: "57708363"
---
# <a name="create-a-configuration-page"></a>Créer une page de configuration

Une page de configuration est un type spécial de [page de contenu.](content-page.md) Les utilisateurs configurent certains aspects de l’application Microsoft Teams à l’aide de la page de configuration et utilisent cette configuration dans le cadre des éléments suivants :

* Onglet de conversation de canal ou de groupe : recueillez des informations auprès des utilisateurs et définissez la page de contenu `contentUrl` à afficher.
* Une [extension de messagerie](~/messaging-extensions/what-are-messaging-extensions.md).
* Un [connecteur Office 365 .](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)

## <a name="configure-a-channel-or-group-chat-tab"></a>Configurer un onglet de conversation de canal ou de groupe

L’application doit référencer [Microsoft Teams SDK client JavaScript et](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) appeler `microsoft.initialize()` . Les URL utilisées doivent être sécurisées par des points de terminaison HTTPS et disponibles à partir du cloud.

### <a name="example"></a>Exemple

Un exemple de page de configuration est illustré dans l’image suivante :

<img src="~/assets/images/tab-images/configuration-page.png" alt="Configuration page" width="400"/>

Le code suivant est un exemple de code correspondant pour la page de configuration :

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

Choisissez le **bouton Sélectionner gris** ou **Rouge** dans la page de configuration pour afficher le contenu de l’onglet avec une icône grise ou rouge.

L’image suivante affiche le contenu de l’onglet avec une icône grise :

<img src="~/assets/images/tab-images/configure-tab-with-gray.png" alt="Configure tab with select gray" width="400"/>

L’image suivante affiche le contenu de l’onglet avec une icône rouge :

<img src="~/assets/images/tab-images/configure-tab-with-red.png" alt="Configure tab with select red" width="400"/>

Le choix du bouton approprié déclenche l’une `saveGray()` ou `saveRed()` l’autre des déclencheurs et appelle les éléments suivants :

* Définir `settings.setValidityState(true)` sur true. 
* Le `microsoftTeams.settings.registerOnSaveHandler()` handler d’événements est déclenché.
* **L’enregistrer** sur la page de configuration de l’application est activé.

Le code de la page de configuration Teams que les exigences de configuration sont satisfaites et que l’installation peut se poursuivre. Lorsque l’utilisateur sélectionne **Enregistrer,** les paramètres `settings.setSettings()` sont définis, comme défini par l’interface. `Settings` Pour plus d’informations, voir [l’interface des paramètres.](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true) `saveEvent.notifySuccess()` est appelée pour indiquer que l’URL de contenu a été résolue avec succès.

>[!NOTE]
>
>* Si vous inscrivez un handler d’enregistrement à l’aide de , le rappel doit appeler ou `microsoftTeams.settings.registerOnSaveHandler()` indiquer le résultat de la `saveEvent.notifySuccess()` `saveEvent.notifyFailure()` configuration.
>* Si vous n’enregistrez pas de handler d’enregistrement, l’appel est effectué automatiquement lorsque `saveEvent.notifySuccess()` l’utilisateur sélectionne **Enregistrer**.

### <a name="get-context-data-for-your-tab-settings"></a>Obtenir des données de contexte pour les paramètres de l’onglet

Votre onglet nécessite des informations contextuelles pour afficher le contenu pertinent. Les informations contextuelles améliorent davantage l’appel de votre onglet en offrant une expérience utilisateur plus personnalisée.

Pour plus d’informations sur les propriétés utilisées pour la configuration de l’onglet, voir [l’interface de contexte.](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) Collectez les valeurs des variables de données de contexte des deux manières suivantes :

* Insérez des espaces de caractères de chaîne de requête d’URL dans le `configurationURL` manifeste.

* Utilisez la [Teams SDK.](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})`

#### <a name="insert-placeholders-in-the-configurationurl"></a>Insérer des espaces réservé dans le `configurationUrl`

Ajoutez des espaces réservé à l’interface de contexte à votre `configurationUrl` base. Par exemple :

##### <a name="base-url"></a>URL de base

```json
...
"configurationUrl": "https://yourWebsite/config",
...
```

#### <a name="base-url-with-query-strings"></a>URL de base avec chaînes de requête

```json
...
"configurationUrl": "https://yourWebsite/config?team={teamId}&channel={channelId}&{locale}"
...
```

Une fois votre page téléchargée, Teams les espaces réservé de chaîne de requête avec les valeurs pertinentes. Incluez la logique dans la page de configuration pour récupérer et utiliser ces valeurs. Pour plus d’informations sur l’working with URL query strings, see [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) in MDN Web Docs. L’exemple de code suivant permet d’extraire une valeur de la `configurationUrl` propriété :

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

### <a name="use-the-getcontext-function-to-retrieve-context"></a>Utiliser la `getContext()` fonction pour récupérer le contexte

La `microsoftTeams.getContext((context) => {})` fonction récupère [l’interface de contexte](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) lorsqu’elle est invoquée.

Le code suivant fournit un exemple d’ajout de cette fonction à la page de configuration pour récupérer des valeurs de contexte :

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

## <a name="context-and-authentication"></a>Contexte et authentification

Authentifier avant d’autoriser un utilisateur à configurer votre application. Dans le cas contraire, votre contenu peut inclure des sources qui ont leurs protocoles d’authentification. Pour plus d’informations, [voir authentifier un utilisateur dans un Microsoft Teams onglet .](~/tabs/how-to/authentication/auth-flow-tab.md) Utilisez les informations de contexte pour construire les demandes d’authentification et les URL de page d’autorisation. Assurez-vous que tous les domaines utilisés dans vos pages d’onglets sont répertoriés dans le `manifest.json` tableau et dans `validDomains` celui-ci.

## <a name="modify-or-remove-a-tab"></a>Modifier ou supprimer un onglet

Définissez la propriété de votre manifeste sur , qui permet aux utilisateurs de modifier, reconfigurer ou renommer un canal `canUpdateConfiguration` ou un onglet de `true` groupe. Indiquez également ce qu’il advient du contenu lorsqu’un onglet est supprimé, en incluant une page d’options de suppression dans l’application et en fixant une valeur pour la propriété `removeUrl` dans la  `setSettings()` configuration. L’utilisateur peut désinstaller les onglets personnels, mais ne peut pas les modifier. Pour plus d’informations, [voir créer une page de suppression pour votre onglet.](~/tabs/how-to/create-tab-pages/removal-page.md)

`setSettings()`Microsoft Teams configuration de la page de suppression :

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add unique name here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "add website URL here //Required field for configurable tabs on Mobile Clients",
    removeUrl: "add removal page URL here"
});
```

## <a name="mobile-clients"></a>Clients mobiles

Si vous choisissez que votre onglet de canal ou de groupe apparaisse sur les clients mobiles Teams, la configuration doit avoir `setSettings()` une valeur pour `websiteUrl` . Pour plus d’informations, [voir les conseils pour les onglets sur mobile.](~/tabs/design/tabs-mobile.md)

## <a name="see-also"></a>Voir aussi

* [Teams onglets](~/tabs/what-are-tabs.md)
* [Créer un onglet personnel](~/tabs/how-to/create-personal-tab.md)
* [Créer un onglet de canal ou de groupe](~/tabs/how-to/create-channel-group-tab.md)
* [Créer une page de contenu](~/tabs/how-to/create-tab-pages/content-page.md)
* [Onglets sur les appareils mobiles](~/tabs/design/tabs-mobile.md)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créer une page de suppression pour votre onglet](~/tabs/how-to/create-tab-pages/removal-page.md)
