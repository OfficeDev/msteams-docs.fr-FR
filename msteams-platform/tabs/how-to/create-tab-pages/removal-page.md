---
title: Créer une page de suppression d’onglets
author: surbhigupta
description: Comment créer une page de suppression d’onglet
keywords: onglets teams , canal de groupe configurable Supprimer la suppression
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: fe0445099958af7cd9eccc831fe22fa2e94cbcc5
ms.sourcegitcommit: 929391b6c04d53ea84a93145e2f29d6b96a64d37
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/25/2022
ms.locfileid: "65672935"
---
# <a name="create-a-removal-page"></a>Créer une page de suppression

Vous pouvez étendre et améliorer l’expérience utilisateur en prenant en charge les options de suppression et de modification dans votre application. Teams permet aux utilisateurs de renommer ou de supprimer un canal ou un onglet de groupe, et vous pouvez autoriser les utilisateurs à reconfigurer votre onglet après l’installation. En outre, l’expérience de suppression d’onglets offre aux utilisateurs des options de post-suppression permettant de supprimer ou d’archiver du contenu.

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

## <a name="enable-your-tab-to-be-reconfigured-after-installation"></a>Activer la reconfiguration de votre onglet après l’installation

Votre `manifest.json` définit les fonctionnalités et fonctionnalités de votre onglet. L’instance de tabulation `canUpdateConfiguration` propriété prend une valeur booléenne qui indique si un utilisateur peut modifier ou reconfigurer l’onglet après sa création. Le tableau suivant fournit les détails de la propriété :

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`canUpdateConfiguration`|Booléen|||Valeur indiquant si une instance de la configuration de l’onglet peut être mise à jour par l’utilisateur après sa création. La valeur par défaut est `true`. |

Lorsque votre onglet est chargé dans un canal ou une conversation de groupe, Teams ajoute un menu déroulant contextuel de clic droit pour votre onglet. Les options disponibles sont déterminées par le paramètre `canUpdateConfiguration`. Le tableau suivant fournit les détails du paramètre :

| `canUpdateConfiguration`| true   | false | description |
| ----------------------- | :----: | ----- | ----------- |
|     Paramètres            |   √    |       |La page `configurationUrl` est rechargée dans un IFrame permettant à l’utilisateur de reconfigurer l’onglet. |
|     Renommer              |   √    |   √   | L’utilisateur peut modifier le nom de l’onglet tel qu’il apparaît dans la barre d’onglets.          |
|     Supprimer              |   √    |   √   |  Si la propriété et la valeur `removeURL` sont incluses dans la **page de configuration**, la **page de suppression** est chargée dans un IFrame et présentée à l’utilisateur. Si aucune page de suppression n’est incluse, une boîte de dialogue de confirmation s’affiche à l’utilisateur.          |

## <a name="create-a-tab-removal-page-for-your-application"></a>Créer une page de suppression d’onglet pour votre application

La page de suppression facultative est une page HTML que vous hébergez et qui s’affiche lorsque l’onglet est supprimé. L’URL de la page de suppression est désignée par la `setConfig()` méthode (anciennement `setSettings()`) dans votre page de configuration. Comme pour toutes les pages de votre application, la page de suppression doit respecter [conditions préalables de l’onglet Teams](../../../tabs/how-to/tab-requirements.md).

### <a name="register-a-remove-handler"></a>Inscrire un gestionnaire de suppression

Si vous le souhaitez, dans votre logique de page de suppression, vous pouvez appeler le `registerOnRemoveHandler((RemoveEvent) => {}` gestionnaire d’événements lorsque l’utilisateur supprime une configuration d’onglet existante. La méthode accepte l’interface [`RemoveEvent`](/javascript/api/@microsoft/teams-js/pages.config.removeevent?view=msteams-client-js-latest&preserve-view=true) et exécute le code dans le gestionnaire lorsqu’un utilisateur tente de supprimer du contenu. La méthode est utilisée pour effectuer des opérations de nettoyage telles que la suppression de la ressource sous-jacente qui alimente le contenu de l’onglet. À la fois, un seul gestionnaire de suppression peut être inscrit.

L’interface `RemoveEvent` décrit un objet avec deux méthodes :

* La fonction `notifySuccess()` est requise. Il indique que la suppression de la ressource sous-jacente a réussi et que son contenu peut être supprimé.

* La fonction `notifyFailure(string)` est facultative. Il indique que la suppression de la ressource sous-jacente a échoué et que son contenu ne peut pas être supprimé. Le paramètre de chaîne facultatif spécifie une raison de l’échec. Si elle est fournie, cette chaîne s’affiche pour l’utilisateur ; sinon, une erreur générique s’affiche.

#### <a name="use-the-getconfig-function"></a>Utiliser la fonction `getConfig()`

Vous pouvez utiliser `getConfig()` (anciennement `getSettings()`) pour affecter le contenu de l’onglet à supprimer. La `getConfig()` fonction retourne une promesse qui se résout avec l’objet Config et fournit les valeurs de propriété de paramètres valides qui peuvent être récupérées.

#### <a name="use-the-getcontext-function"></a>Utiliser la fonction `getContext()`

Vous pouvez utiliser `getContext()` pour obtenir le contexte actuel dans lequel le frame s’exécute. La `getContext()` fonction retourne une promesse qui sera résolue avec l’objet Context. L’objet Context fournit des valeurs de propriété valides `Context` que vous pouvez utiliser dans votre logique de page de suppression pour déterminer le contenu à afficher dans la page de suppression.

#### <a name="include-authentication"></a>Inclure l’authentification

L’authentification est requise avant de permettre à un utilisateur de supprimer le contenu de l’onglet. Les informations de contexte peuvent être utilisées pour aider à construire des demandes d’authentification et des URL de page d’autorisation. Consultez [flux d’authentification Microsoft Teams pour les onglets](~/tabs/how-to/authentication/auth-flow-tab.md). Assurez-vous que tous les domaines utilisés dans vos pages d’onglets sont répertoriés dans le tableau `manifest.json``validDomains`.

Voici un exemple de bloc de code de suppression d’onglet :

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

```html
<body>
  <button onclick="onClick()">Delete this tab and all underlying data?</button>
  <script>
    app.initialize();
    pages.config.registerOnRemoveHandler((removeEvent) => {
      // Here you can designate the tab content to be removed and/or archived.
        const configPromise = pages.getConfig();
        configPromise.
            then((configuration) => {
                configuration.contentUrl = "...";
                removeEvent.notifySuccess()}).
            catch((error) => {removeEvent.notifyFailure("failure message")});
    });

    const onClick() => {
        pages.config.setValidityState(true);
    }
  </script>
</body>
```

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

```html
<body>
  <button onclick="onClick()">Delete this tab and all underlying data?</button>
  <script>
    microsoftTeams.initialize();
    microsoftTeams.settings.registerOnRemoveHandler((removeEvent) => {
      // Here you can designate the tab content to be removed and/or archived.
        microsoftTeams.settings.getSettings((settings) => {
        settings.contentUrl = "..."
        });
        removeEvent.notifySuccess();
    });

    const onClick() => {
        microsoftTeams.settings.setValidityState(true);
    }
  </script>
</body>
```

***

Lorsqu’un utilisateur sélectionne **Supprimer** dans le menu déroulant de l’onglet, Teams charge la page de `removeUrl` facultative affectée dans votre **page de configuration**, dans un IFrame. L’utilisateur voit un bouton chargé avec la fonction `onClick()` qui appelle `pages.config.setValidityState(true)` et active le bouton **Supprimer** affiché en bas de l’IFrame de la page de suppression.

Une fois le gestionnaire de suppression exécuté, `removeEvent.notifySuccess()` ou `removeEvent.notifyFailure()` informe Teams du résultat de la suppression du contenu.

>[!NOTE]
>
> * Pour garantir que le contrôle d’un utilisateur autorisé sur un onglet n’est pas empêché, Teams supprime l’onglet dans les cas de réussite et d’échec.
> * Après avoir appelé le gestionnaire d’événements `registerOnRemoveHandler`, vous aurez 15 secondes pour répondre à la méthode. Par défaut, Teams active le bouton **Supprimer** après cinq secondes, même si vous n’appelez pas `setValidityState(true)`.
> * Lorsque l’utilisateur sélectionne **Supprimer**, Teams supprime l’onglet après 30 secondes, que les actions aient été effectuées ou non.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Onglets sur les appareils mobiles](~/tabs/design/tabs-mobile.md)

## <a name="see-also"></a>Voir aussi

* [onglets Teams](~/tabs/what-are-tabs.md)
* [Créer un onglet personnel](~/tabs/how-to/create-personal-tab.md)
* [Créer un onglet de canal ou de groupe](~/tabs/how-to/create-channel-group-tab.md)
* [Créer une page de configuration](~/tabs/how-to/create-tab-pages/configuration-page.md)
