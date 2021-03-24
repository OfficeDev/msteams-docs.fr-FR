---
title: Créer une page de configuration
author: laujan
description: Comment créer une page de configuration
keywords: Canal de groupe onglets teams configurable
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: b6da8437b6988f863288d77aedc1acb786c12d4b
ms.sourcegitcommit: 49d1ecda14042bf3f368b14c1971618fe979b914
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/23/2021
ms.locfileid: "51034677"
---
# <a name="create-a-configuration-page"></a>Créer une page de configuration

Une page de configuration est un type spécial [de page de contenu.](content-page.md) Les utilisateurs configurent certains aspects de l’application Microsoft Teams à l’aide de la page de configuration et utilisent cette configuration dans le cadre des éléments suivants :

* Onglet de conversation de canal ou de groupe : recueillez des informations auprès des utilisateurs et définissez `contentUrl` la page de contenu à afficher.
* Une [extension de messagerie](~/messaging-extensions/what-are-messaging-extensions.md)
* Un [connecteur Office 365](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)

## <a name="configuring-a-channel-or-group-chat-tab"></a>Configuration d’un onglet de conversation de canal ou de groupe

L’application doit référencer le [SDK client JavaScript Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) et appeler `microsoft.initialize()` . En outre, les URL utilisées doivent être sécurisées par des points de terminaison HTTPS et disponibles à partir du cloud. Le code suivant est un exemple de page de configuration :

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
    </body>
...
```

Choisissez le **bouton Sélectionner gris** ou **Rouge** dans la page de configuration pour afficher le contenu de l’onglet avec une icône grise ou rouge. Le choix du bouton relatif se déclenche `saveGray()` `saveRed()` soit, soit, et appelle les valeurs suivantes :

1. La `settings.setValidityState(true)` valeur true est définie.
1. Le `microsoftTeams.settings.registerOnSaveHandler()` handler d’événements est déclenché.
1. Le **bouton** Enregistrer sur la page de configuration de l’application, téléchargé dans Teams, est activé.

Le code de la page de configuration informe Teams que les exigences de configuration sont satisfaites et que l’installation peut se poursuivre. Lorsque l’utilisateur sélectionne **Enregistrer,** les paramètres `settings.setSettings()` sont définis, comme défini par l’interface. `Settings` Pour plus d’informations, voir [l’interface paramètres.](/javascript/api/@microsoft/teams-js/_settings?view=msteams-client-js-latest&preserve-view=true) Dans la dernière étape, `saveEvent.notifySuccess()` est appelée pour indiquer que l’URL de contenu a été correctement résolue.

>[!NOTE]
>
>* Si vous inscrivez un handler d’enregistrement à l’aide de , le rappel doit appeler ou `microsoftTeams.settings.registerOnSaveHandler()` indiquer le résultat de la `saveEvent.notifySuccess()` `saveEvent.notifyFailure()` configuration.
>* Si vous n’enregistrez pas de handler d’enregistrement, l’appel est effectué automatiquement lorsque l’utilisateur `saveEvent.notifySuccess()` sélectionne **Enregistrer**.

### <a name="get-context-data-for-your-tab-settings"></a>Obtenir des données de contexte pour les paramètres de l’onglet

Votre onglet peut nécessiter des informations contextuelles pour afficher le contenu pertinent. Les informations contextuelles améliorent davantage l’appel de votre onglet en offrant une expérience utilisateur plus personnalisée.

Pour plus d’informations sur les propriétés utilisées pour la configuration de l’onglet, voir [l’interface de contexte.](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) Collectez les valeurs des variables de données de contexte des deux manières suivantes :

1. Insérez des espaces de caractères de chaîne de requête d’URL dans le `configurationURL` manifeste.

1. Utilisez la [méthode du SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})` Teams.

#### <a name="insert-placeholders-in-the-configurationurl"></a>Insérer des espaces réservé dans le `configurationUrl`

Ajoutez des espaces réservé à l’interface de contexte à votre `configurationUrl` base. Par exemple :

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

Une fois votre page téléchargée, Teams met à jour les espaces réservé de chaîne de requête avec les valeurs pertinentes. Incluez la logique dans la page de configuration pour récupérer et utiliser ces valeurs. Pour plus d’informations sur l’working with URL query strings, see [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) in MDN Web Docs. L’exemple suivant décrit la façon d’extraire une valeur de la `configurationUrl` propriété :

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

La `microsoftTeams.getContext((context) => {})` fonction récupère [l’interface Context](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) lorsqu’elle est invoquée. Ajoutez cette fonction à la page de configuration pour récupérer les valeurs de contexte :

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

 Authentifier avant d’autoriser un utilisateur à configurer votre application. Dans le cas contraire, votre contenu peut inclure des sources qui ont leurs protocoles d’authentification. Pour plus d’informations, voir [Authentifier un utilisateur dans un onglet Microsoft Teams.](~/tabs/how-to/authentication/auth-flow-tab.md) Utilisez les informations de contexte pour construire les demandes d’authentification et les URL de page d’autorisation.
Assurez-vous que tous les domaines utilisés dans vos pages d’onglets sont répertoriés dans le `manifest.json` tableau et dans `validDomains` celui-ci.

## <a name="modify-or-remove-a-tab"></a>Modifier ou supprimer un onglet

Les options de suppression prise en charge améliorent davantage l’expérience utilisateur. Définissez la propriété de votre manifeste sur , qui permet aux utilisateurs de modifier, reconfigurer ou renommer un onglet de groupe `canUpdateConfiguration` `true` ou de canal. Indiquez également ce qu’il advient du contenu lorsqu’un onglet est supprimé, en incluant une page d’options de suppression dans l’application et en fixant une valeur pour la propriété `removeUrl` dans la  `setSettings()` configuration. L’utilisateur peut désinstaller les onglets Personnels, mais ne peut pas les modifier. Pour plus d’informations, [voir Créer une page de suppression pour votre onglet.](~/tabs/how-to/create-tab-pages/removal-page.md)

Configuration de Microsoft Teams setSettings() pour la page de suppression :

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

Si vous choisissez que votre onglet de canal ou de groupe apparaisse sur les clients mobiles Teams, la configuration doit avoir une valeur `setSettings()` pour la `websiteUrl` propriété. Pour plus d’informations, [voir les conseils pour les onglets sur mobile.](~/tabs/design/tabs-mobile.md)