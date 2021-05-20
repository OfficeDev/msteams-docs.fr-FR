---
title: Créer une page de configuration
author: laujan
description: comment créer une page de configuration
keywords: équipes onglets canal de groupe configurable
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: aeab1cf96d1e875db79d9143fefd0e46348f585a
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566683"
---
# <a name="create-a-configuration-page"></a>Créer une page de configuration

Une page de configuration est un type spécial de [page de contenu](content-page.md). Les utilisateurs configurent certains aspects de l’application Microsoft Teams’utilisation de la page de configuration et utilisent cette configuration dans le cadre des éléments suivants :

* Onglet de chat de canal ou de groupe : Collectez des informations auprès des utilisateurs et définissez `contentUrl` la page de contenu à afficher.
* Une [extension de messagerie](~/messaging-extensions/what-are-messaging-extensions.md).
* Un [connecteur Office 365 de travail](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md).

## <a name="configuring-a-channel-or-group-chat-tab"></a>Configuration d’un canal ou d’un onglet de chat de groupe

L’application doit faire référence [Microsoft Teams client JavaScript SDK et](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) appeler `microsoft.initialize()` . En outre, les URL utilisées doivent être sécurisées points de terminaison HTTPS et disponibles à partir du nuage. 

### <a name="example"></a>Exemple

Un exemple de page de configuration est affiché dans l’image suivante : 

<img src="~/assets/images/tab-images/configuration-page.png" alt="Configuration page" width="400"/>

Le code correspondant pour la page de configuration est affiché dans la section suivante :

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

Choisissez le **bouton Sélectionnez** gris **ou sélectionnez** rouge dans la page de configuration, pour afficher le contenu de l’onglet avec une icône grise ou rouge. 

L’image suivante affiche le contenu de l’onglet avec icône grise :

<img src="~/assets/images/tab-images/configure-tab-with-gray.png" alt="Configure tab with select gray" width="400"/>

L’image suivante affiche le contenu de l’onglet avec icône rouge :

<img src="~/assets/images/tab-images/configure-tab-with-red.png" alt="Configure tab with select red" width="400"/>

Le choix du bouton relatif déclenche ou `saveGray()` `saveRed()` , et invoque ce qui suit:

1. `settings.setValidityState(true)`L’est réglé à vrai.
1. Le `microsoftTeams.settings.registerOnSaveHandler()` gestionnaire d’événements est déclenché.
1. Le **bouton Enregistrer** sur la page de configuration de l’application, téléchargé dans Teams, est activé.

Le code de la page de configuration informe Teams que les exigences de configuration sont satisfaites et que l’installation peut se poursuivre. Lorsque l’utilisateur sélectionne **Enregistrer,** les paramètres de sont `settings.setSettings()` définis, tels que définis par `Settings` l’interface. Pour plus d’informations, [Paramètres interface](/javascript/api/@microsoft/teams-js/_settings?view=msteams-client-js-latest&preserve-view=true). Dans la dernière étape, `saveEvent.notifySuccess()` est appelé à indiquer que l’URL de contenu a résolu avec succès.

>[!NOTE]
>
>* Si vous enregistrez un gestionnaire d’enregistrement à `microsoftTeams.settings.registerOnSaveHandler()` l’aide, le rappel doit `saveEvent.notifySuccess()` `saveEvent.notifyFailure()` invoquer ou indiquer le résultat de la configuration.
>* Si vous n’enregistrez pas un gestionnaire d’enregistrement, `saveEvent.notifySuccess()` l’appel est effectué automatiquement lorsque l’utilisateur sélectionne **Enregistrer**.

### <a name="get-context-data-for-your-tab-settings"></a>Obtenez des données context contextées pour les paramètres de vos onglets

Votre onglet peut nécessiter des informations contextuelles pour afficher du contenu pertinent. Les informations contextuelles améliorent encore l’attrait de votre onglet en offrant une expérience utilisateur plus personnalisée.

Pour plus d’informations sur les propriétés utilisées pour la configuration de l’onglet, voir [interface Context](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true). Recueillir les valeurs des variables de données contextatives de deux façons suivantes :

1. Insérez les espaces réservés de chaîne de requête d’URL dans votre `configurationURL` manifeste.

1. Utilisez la [Teams SDK.](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})`

#### <a name="insert-placeholders-in-the-configurationurl"></a>Insérez les espaces réservés dans le `configurationUrl`

Ajoutez des espaces réservés à l’interface context context à votre base `configurationUrl` . Par exemple :

##### <a name="base-url"></a>URL de base

```json
...
"configurationUrl": "https://yourWebsite/config",
...
```

#### <a name="base-url-with-query-strings"></a>URL de base avec chaînes de requêtes

```json
...
"configurationUrl": "https://yourWebsite/config?team={teamId}&channel={channelId}&{locale}"
...
```

Après le téléchargement de votre page, le Teams les espaces réservés aux requêtes avec les valeurs pertinentes. Inclure la logique dans la page de configuration pour récupérer et utiliser ces valeurs. Pour plus d’informations sur le travail avec les chaînes de requêtes URL, [consultez URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) dans MDN Web Docs. L’exemple suivant décrit la façon d’extraire une valeur de la `configurationUrl` propriété :

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

### <a name="use-the-getcontext-function-to-retrieve-context"></a>Utilisez la `getContext()` fonction pour récupérer le contexte

La `microsoftTeams.getContext((context) => {})` fonction récupère [l’interface Context lorsqu’elle](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) est invoquée. Ajoutez cette fonction à la page de configuration pour récupérer les valeurs de contexte :

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

 Authentifiez avant de permettre à un utilisateur de configurer votre application. Dans le cas contraire, votre contenu peut inclure des sources qui ont leurs protocoles d’authentification. Pour plus d’informations, [voir Authentifier un utilisateur dans un onglet Microsoft Teams’utilisateur](~/tabs/how-to/authentication/auth-flow-tab.md). Utilisez les informations context contextées pour construire les urls de la page d’authentification et d’autorisation.
Assurez-vous que tous les domaines utilisés dans vos pages d’onglets sont répertoriés dans `manifest.json` le tableau et le `validDomains` tableau.

## <a name="modify-or-remove-a-tab"></a>Modifier ou supprimer un onglet

Les options de suppression prises en charge affinant davantage l’expérience utilisateur. Réglez la propriété de votre `canUpdateConfiguration` manifeste à , qui permet aux utilisateurs de `true` modifier, reconfigurer ou renommer un onglet de groupe ou de canal. Indiquez également ce qui arrive au contenu lorsqu’un onglet est supprimé, en incluant une page d’options de suppression dans l’application et en fixant une `removeUrl` valeur pour la propriété dans la  `setSettings()` configuration. L’utilisateur peut désinstaller les onglets personnels mais ne peut pas les modifier. Pour plus d’informations, [voir Créer une page de suppression pour votre onglet](~/tabs/how-to/create-tab-pages/removal-page.md).

Microsoft Teams configuration setSettings () pour la page de suppression :

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

Si vous choisissez d’avoir votre onglet canal ou groupe sur les Teams clients mobiles, la `setSettings()` configuration doit avoir une valeur pour la `websiteUrl` propriété. Pour plus d’informations, consultez [les conseils pour les onglets sur mobile](~/tabs/design/tabs-mobile.md).
