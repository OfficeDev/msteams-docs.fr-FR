---
title: Créer une page de configuration
author: surbhigupta
description: Découvrez comment créer une page de configuration pour configurer un canal ou une conversation de groupe pour des paramètres tels que l’obtention de données de contexte, l’insertion d’espaces réservés et l’authentification à l’aide d’exemples de code.
keywords: Canal de groupe des onglets Teams configurable
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: dc1c5c7c8852d13ab490ae0782be0a01eef3fbea
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2022
ms.locfileid: "65103417"
---
# <a name="create-a-configuration-page"></a>Créer une page de configuration

Une page de configuration est un type spécial de [page de contenu](content-page.md). Les utilisateurs configurent certains aspects de l’application Microsoft Teams à l’aide de la page de configuration et utilisent cette configuration dans le cadre des éléments suivants :

* Onglet Canal ou conversation de groupe : collectez des informations auprès des utilisateurs et définissez la `contentUrl` page de contenu à afficher.
* Extension [de message](~/messaging-extensions/what-are-messaging-extensions.md).
* [Connecteur Office 365](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md).

## <a name="configure-a-channel-or-group-chat-tab"></a>Configurer un canal ou un onglet de conversation de groupe

L’application doit référencer le [SDK client JavaScript Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) et appeler`microsoft.initialize()`. Les URL utilisées doivent être des points de terminaison HTTPS sécurisés et disponibles à partir du cloud.

### <a name="example"></a>Exemple

L’image suivante illustre un exemple de page de configuration :

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

Sélectionnez **le bouton Sélectionner gris** ou **Sélectionner rouge** dans la page de configuration pour afficher le contenu de l’onglet avec une icône grise ou rouge.

L’image suivante affiche le contenu de l’onglet avec l’icône **Gris** sélectionnée :

<img src="~/assets/images/tab-images/configure-tab-with-gray.png" alt="Configure tab with select gray" width="400"/>

L’image suivante affiche le contenu de l’onglet avec l’icône **Rouge** sélectionnée :

<img src="~/assets/images/tab-images/configure-tab-with-red.png" alt="Configure tab with select red" width="400"/>

Le choix du bouton approprié déclenche ou `saveRed()`appelle les éléments suivants `saveGray()` :

* Défini sur `settings.setValidityState(true)` true.
* Le `microsoftTeams.settings.registerOnSaveHandler()` gestionnaire d’événements est déclenché.
* **L’enregistrement** sur la page de configuration de l’application est activé.

Le code de la page de configuration informe Teams que les exigences de configuration sont satisfaites et que l’installation peut continuer. Lorsque l’utilisateur sélectionne **Enregistrer**, les paramètres sont `settings.setSettings()` définis, comme défini par l’interface `Settings` . Pour plus d’informations, consultez [l’interface des paramètres](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true). `saveEvent.notifySuccess()` est appelé pour indiquer que l’URL de contenu a été résolue.

>[!NOTE]
>
>* Vous avez 30 secondes pour terminer l’opération d’enregistrement (le rappel à registerOnSaveHandler) avant le délai d’expiration. Après le délai d’expiration, un message d’erreur générique s’affiche.
>* Si vous inscrivez un gestionnaire d’enregistrement à l’aide `microsoftTeams.settings.registerOnSaveHandler()`, le rappel doit appeler `saveEvent.notifySuccess()` ou `saveEvent.notifyFailure()` indiquer le résultat de la configuration.
>* Si vous n’inscrivez pas de gestionnaire d’enregistrement, l’appel `saveEvent.notifySuccess()` est effectué automatiquement lorsque l’utilisateur sélectionne **Enregistrer**.

### <a name="get-context-data-for-your-tab-settings"></a>Obtenir des données de contexte pour vos paramètres d’onglet

Votre onglet nécessite des informations contextuelles pour afficher du contenu pertinent. Les informations contextuelles améliorent l’attrait de votre onglet en fournissant une expérience utilisateur plus personnalisée.

Pour plus d’informations sur les propriétés utilisées pour la configuration des onglets, consultez [l’interface de contexte](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true). Collectez les valeurs des variables de données de contexte des deux manières suivantes :

* Insérez des espaces réservés de chaîne de requête URL dans celui de `configurationURL`votre manifeste.

* Utilisez la méthode [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)`microsoftTeams.getContext((context) =>{})`.

#### <a name="insert-placeholders-in-the-configurationurl"></a>Insérer des espaces réservés dans le `configurationUrl`

Ajoutez des espaces réservés d’interface de contexte à votre base `configurationUrl`. Par exemple :

##### <a name="base-url"></a>URL de base

```json
...
"configurationUrl": "https://yourWebsite/config",
...
```

#### <a name="base-url-with-query-strings"></a>URL de base avec des chaînes de requête

```json
...
"configurationUrl": "https://yourWebsite/config?team={teamId}&channel={channelId}&{locale}"
...
```

Une fois votre page chargée, Teams met à jour les espaces réservés de chaîne de requête avec les valeurs appropriées. Incluez la logique dans la page de configuration pour récupérer et utiliser ces valeurs. Pour plus d’informations sur l’utilisation des chaînes de requête URL, consultez [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) dans MDN Web Docs. L’exemple de code suivant permet d’extraire une valeur de la `configurationUrl` propriété :

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

### <a name="use-the-getcontext-function-to-retrieve-context"></a>Utiliser la fonction pour récupérer le `getContext()` contexte

La `microsoftTeams.getContext((context) => {})` fonction récupère [l’interface de contexte](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) lorsqu’elle est appelée.

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

S’authentifier avant d’autoriser un utilisateur à configurer votre application. Sinon, votre contenu peut inclure des sources qui ont leurs protocoles d’authentification. Pour plus d’informations, consultez [l’authentification d’un utilisateur dans un onglet Microsoft Teams](~/tabs/how-to/authentication/auth-flow-tab.md). Utilisez les informations de contexte pour construire les requêtes d’authentification et les URL de page d’autorisation. Assurez-vous que tous les domaines utilisés dans vos pages d’onglets sont répertoriés dans le tableau et `validDomains` dans le `manifest.json` tableau.

## <a name="modify-or-remove-a-tab"></a>Modifier ou supprimer un onglet

Définissez la propriété `true`de `canUpdateConfiguration` votre manifeste sur , ce qui permet aux utilisateurs de modifier, reconfigurer ou renommer un canal ou un onglet de groupe. Indiquez également ce qui arrive au contenu lorsqu’un onglet est supprimé, en incluant une page d’options de suppression dans l’application et en définissant une valeur pour la `removeUrl` propriété dans la `setSettings()` configuration. L’utilisateur peut désinstaller les onglets personnels, mais ne peut pas les modifier. Pour plus d’informations, consultez [créer une page de suppression pour votre onglet](~/tabs/how-to/create-tab-pages/removal-page.md).

`setSettings()` Microsoft Teams configuration de la page de suppression :

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add a unique identifier here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "add website URL here //Required field for configurable tabs on Mobile Clients",
    removeUrl: "add removal page URL here"
});
```

## <a name="mobile-clients"></a>Clients mobiles

Si vous choisissez d’afficher l’onglet de votre canal ou groupe sur le Teams clients mobiles, la `setSettings()` configuration doit avoir une valeur pour `websiteUrl`. Pour plus d’informations, consultez [les conseils relatifs aux onglets sur les appareils mobiles](~/tabs/design/tabs-mobile.md).

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créer une page de suppression pour votre onglet](~/tabs/how-to/create-tab-pages/removal-page.md)

## <a name="see-also"></a>Voir aussi

* [onglets Teams](~/tabs/what-are-tabs.md)
* [Créer un onglet personnel](~/tabs/how-to/create-personal-tab.md)
* [Créer un canal ou un onglet de groupe](~/tabs/how-to/create-channel-group-tab.md)
* [Créer une page de contenu](~/tabs/how-to/create-tab-pages/content-page.md)
* [Onglets sur les appareils mobiles](~/tabs/design/tabs-mobile.md)
