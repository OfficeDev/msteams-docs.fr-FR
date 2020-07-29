---
title: Créer une page de configuration
author: laujan
description: ''
keywords: onglet teams groupe de canaux configurable
ms.topic: conceptualF
ms.author: laujan
ms.openlocfilehash: 55fe1efca4defacf10b9be34f788704b7b4491f5
ms.sourcegitcommit: 1b909fb9ccf6cdd84ed0d8f9ea0463243a802a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/28/2020
ms.locfileid: "45434481"
---
# <a name="create-a-configuration-page"></a>Créer une page de configuration

Une page de configuration est un type spécial de [page de contenu](content-page.md) qui permet à vos utilisateurs de configurer certains aspects de votre application de teams. En règle générale, ces éléments sont utilisés dans les cas suivants :

* Onglet de conversation de canal ou de groupe : la page de configuration vous permet de recueillir des informations auprès de vos utilisateurs et de définir la `contentUrl` page de contenu à afficher.
* Une [extension de messagerie](~/messaging-extensions/what-are-messaging-extensions.md)
* Un [Connecteur Office 365](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)

## <a name="configuring-a-channel-or-group-chat-tab"></a>Configuration d’un onglet de conversation de canal ou de groupe

Une page de configuration informe la page de contenu de la façon dont elle doit s’afficher. Votre application doit référencer le [Kit de développement logiciel (SDK) du client JavaScript Microsoft teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) et appeler `microsoft.initialize()` . En outre, vos URL doivent être des points de terminaison HTTPs sécurisés et disponibles dans le Cloud. Vous trouverez ci-dessous un exemple de page de configuration.

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

Ici, l’utilisateur voit apparaître deux cases d’option, **Sélectionner le gris** ou le **rouge** pour afficher le contenu de l’onglet avec une icône rouge ou grise. Le choix du bouton relatif déclenche `saveGray()` ou `saveRed()` l’appel des éléments suivants :

1. `settings.setValidityState(true)`Est défini sur true.
1. Le `microsoftTeams.settings.registerOnSaveHandler()` Gestionnaire d’événements est déclenché.
1. Le bouton **Enregistrer** de la page de configuration de l’application, chargé dans Teams, est activé.

Ce code permet aux équipes de reconnaître que les exigences de configuration ont été satisfaites et que l’installation peut être effectuée. Lors de l' **enregistrement**, les paramètres de `settings.setSettings()` sont définis, comme défini par l' `Settings` interface, pour l’instance actuelle (voir [interface des paramètres](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest) ). Enfin, `saveEvent.notifySuccess()` est appelé pour indiquer que l’URL de contenu a été résolue avec succès.

>[!NOTE]
>
>* Si un gestionnaire d’enregistrement a été inscrit à l’aide de `microsoftTeams.settings.registerOnSaveHandler()` , le rappel doit appeler `saveEvent.notifySuccess()` ou `saveEvent.notifyFailure()` pour indiquer le résultat de la configuration.
>* Si aucun gestionnaire d’enregistrement n’a été enregistré, l' `saveEvent.notifySuccess()` appel est automatiquement effectué dès que l’utilisateur sélectionne le bouton **Enregistrer** .

### <a name="get-context-data-for-your-tab-settings"></a>Obtenir les données de contexte pour les paramètres de votre onglet

Votre onglet peut nécessiter des informations contextuelles pour afficher le contenu pertinent. Les informations contextuelles peuvent améliorer davantage l’attrait de votre onglet en fournissant une expérience utilisateur plus personnalisée.

L' [interface de contexte](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest) teams définit les propriétés qui peuvent être utilisées pour votre configuration d’onglets. Vous pouvez collecter les valeurs des variables de données de contexte de deux façons :

1. Insérez des espaces réservés de chaîne de requête d’URL dans votre manifeste `configurationURL` .

1. Utilisez la méthode du [Kit de développement logiciel teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) `microsoftTeams.getContext((context) =>{}` .

#### <a name="insert-placeholders-in-the-configurationurl"></a>Insérer des espaces réservés dans le`configurationURL`

Des espaces réservés d’interface de contexte peuvent être ajoutés à votre base `configurationUrl` . Par exemple :

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

Une fois que votre page a été téléchargée, les espaces réservés de chaîne de requête sont mis à jour par teams avec les valeurs pertinentes. Vous pouvez inclure une logique dans votre page de configuration pour récupérer et utiliser ces valeurs. Pour plus d’informations sur l’utilisation des chaînes de requête d’URL, voir [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) dans notification Web docs. Voici un exemple d’extraction d’une valeur à partir de la propriété ci-dessus `configurationURL` :

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

### <a name="use-the-getcontext-function-to-retrieve-context"></a>Utiliser la `getContext()` fonction pour extraire le contexte

Lorsqu’elle est appelée, la `microsoftTeams.getContext((context) => {})` fonction récupère l' [interface de contexte](/javascript/api/@microsoft/teams-js//microsoftteams.context?view=msteams-client-js-latest). Vous pouvez ajouter cette fonction à votre page de configuration pour extraire les valeurs de contexte :

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

Vous devrez peut-être demander une authentification avant d’autoriser un utilisateur à configurer votre application ou votre contenu peut inclure des sources ayant leurs propres protocoles d’authentification. Voir [authentifier un utilisateur dans une application Microsoft teams](~/tabs/how-to/authentication/auth-flow-tab.md) les informations de contexte peuvent être utilisées pour vous aider à créer des demandes d’authentification et des URL de page d’autorisation.
Assurez-vous que tous les domaines utilisés dans vos pages d’onglets sont répertoriés dans le `manifest.json` `validDomains` tableau.

## <a name="modify-or-remove-a-tab"></a>Modifier ou supprimer un onglet

Les options de suppression prises en charge peuvent affiner l’expérience utilisateur. Vous pouvez permettre aux utilisateurs de modifier, de reconfigurer ou de renommer un onglet de groupe/canal en définissant la propriété de votre manifeste `canUpdateConfiguration` sur `true` .  En outre, vous pouvez indiquer ce qu’il advient du contenu lorsqu’un onglet est supprimé en incluant une page Options de suppression dans votre application et en définissant une valeur pour la `removeUrl` propriété dans la `setSettings()` Configuration (voir ci-dessous). Les onglets personnels ne peuvent pas être modifiés, mais peuvent être désinstallés par l’utilisateur. Pour plus d’informations, consultez [la rubrique créer une page de suppression pour votre onglet](~/tabs/how-to/create-tab-pages/removal-page.md).

## <a name="mobile-clients"></a>Clients mobiles

Si vous choisissez d’afficher l’onglet canal/groupe sur les clients mobiles Teams, la `setSettings()` configuration doit avoir une valeur pour la `websiteUrl` propriété (voir ci-dessous). La prise en charge complète des onglets sur les clients mobiles sera bientôt disponible. Pour préparer la mise à jour, suivez les [instructions pour les onglets sur les appareils mobiles](~/tabs/design/tabs-mobile.md) lors de la création des onglets.

Microsoft teams setSettings () configuration pour la page de suppression et/ou les clients mobiles :

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add unique name here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "URL REQUIRED FOR MOBILE CLIENTS",
    removeUrl: "ADD REMOVAL PAGE URL HERE"
});
```
