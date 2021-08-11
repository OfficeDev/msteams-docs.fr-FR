---
title: Créer une page de suppression d’onglets
author: surbhigupta
description: Comment créer une page de suppression d’onglets
keywords: suppression des onglets teams du canal de groupe configurable
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 5cfe79bc026f7326f258b994540958aab0a83c29f08846447d2b5859f10794dd
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/07/2021
ms.locfileid: "57706785"
---
# <a name="create-a-removal-page"></a>Créer une page de suppression

Vous pouvez étendre et améliorer l’expérience utilisateur en prendre en charge les options de suppression et de modification dans votre application. Teams permet aux utilisateurs de renommer ou de supprimer un onglet de canal ou de groupe et vous pouvez permettre aux utilisateurs de reconfigurer votre onglet après l’installation. En outre, l’expérience de suppression d’onglet offre aux utilisateurs des options post-suppression pour supprimer ou archiver du contenu.

## <a name="enable-your-tab-to-be-reconfigured-after-installation"></a>Activer la reconfiguration de votre onglet après l’installation

Votre **manifest.jsdéfinit** les fonctionnalités et fonctionnalités de votre onglet. La propriété d’instance d’onglet prend une valeur boolé générale qui indique si un utilisateur peut modifier ou reconfigurer l’onglet `canUpdateConfiguration` après sa création. Le tableau suivant fournit les détails de la propriété :

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`canUpdateConfiguration`|Boolean|||Valeur indiquant si une instance de la configuration de l’onglet peut être mise à jour par l’utilisateur après sa création. La valeur par défaut est `true`. |

Lorsque votre onglet est téléchargé vers un canal ou une conversation de groupe, Teams un menu déroulant de clic droit pour votre onglet. Les options disponibles sont déterminées par le `canUpdateConfiguration` paramètre. Le tableau suivant fournit les détails des paramètres :

| `canUpdateConfiguration`| true   | false | description |
| ----------------------- | :----: | ----- | ----------- |
|     Paramètres            |   √    |       |La page est rechargée dans un IFrame, ce qui permet à l’utilisateur de `configurationUrl` reconfigurer l’onglet. |
|     Renommer              |   √    |   √   | L’utilisateur peut modifier le nom de l’onglet tel qu’il apparaît dans la barre d’onglets.          |
|     Supprimer              |   √    |   √   |  Si la propriété et la valeur sont incluses dans la page de configuration, la page de suppression est chargée dans un IFrame et présentée `removeURL` à l’utilisateur.   Si une page de suppression n’est pas incluse, une boîte de dialogue de confirmation est présentée à l’utilisateur.          |

## <a name="create-a-tab-removal-page-for-your-application"></a>Créer une page de suppression d’onglets pour votre application

La page de suppression facultative est une page HTML que vous hébergez et qui s’affiche lorsque l’onglet est supprimé. L’URL de la page de suppression est désignée par la `setSettings()` méthode dans votre page de configuration. Comme pour toutes les pages de votre application, la page de suppression doit respecter les conditions préalables [Teams’onglet.](../../../tabs/how-to/tab-requirements.md)

### <a name="register-a-remove-handler"></a>Inscrire un remove handler

Si vous le souhaitez, dans votre logique de page de suppression, vous pouvez appeler le handler d’événements lorsque l’utilisateur supprime une `registerOnRemoveHandler((RemoveEvent) => {}` configuration d’onglet existante. La méthode prend l’interface et exécute le code dans le handler lorsqu’un utilisateur tente [`RemoveEvent`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.removeevent?view=msteams-client-js-latest&preserve-view=true) de supprimer du contenu. La méthode permet d’effectuer des opérations de nettoyage, telles que la suppression de la ressource sous-jacente qui alimentera le contenu de l’onglet. À la fois, un seul handler de suppression peut être inscrit.

`RemoveEvent`L’interface décrit un objet avec deux méthodes :

* La `notifySuccess()` fonction est obligatoire. Il indique que la suppression de la ressource sous-jacente a réussi et que son contenu peut être supprimé.

* La `notifyFailure(string)` fonction est facultative. Il indique que la suppression de la ressource sous-jacente a échoué et que son contenu ne peut pas être supprimé. Le paramètre de chaîne facultatif spécifie la raison de l’échec. Si elle est fournie, cette chaîne s’affiche pour l’utilisateur ; sinon, une erreur générique s’affiche.

#### <a name="use-the-getsettings-function"></a>Utiliser la `getSettings()` fonction

Vous pouvez `getSettings()` l’utiliser pour affecter le contenu de l’onglet à supprimer. La fonction prend dans et fournit les valeurs de propriété `getSettings((Settings) =>{})` de [`Settings interface`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true) paramètres valides qui peuvent être récupérées.

#### <a name="use-the-getcontext-function"></a>Utiliser la `getContext()` fonction

Vous pouvez utiliser `getContext()` pour obtenir le contexte actuel dans lequel l’image est en cours d’exécution. La `getContext((Context) =>{})` fonction prend dans le [`Context interface`](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) . La fonction fournit des valeurs de propriété valides que vous pouvez utiliser dans la logique de votre page de suppression pour déterminer le contenu à afficher `Context` dans la page de suppression.

#### <a name="include-authentication"></a>Inclure l’authentification

L’authentification est requise avant de permettre à un utilisateur de supprimer le contenu de l’onglet. Les informations de contexte peuvent être utilisées pour créer des demandes d’authentification et des URL de page d’autorisation. Voir [Microsoft Teams flux d’authentification pour les onglets.](~/tabs/how-to/authentication/auth-flow-tab.md) Assurez-vous que tous les domaines utilisés dans vos pages d’onglets sont répertoriés dans le `manifest.json` `validDomains` tableau.

Voici un exemple de bloc de code de suppression d’onglet :

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

Lorsqu’un utilisateur  sélectionne Supprimer du menu déroulant de l’onglet, Teams charge la page facultative affectée dans votre page de `removeUrl` **configuration,** dans un IFrame. L’utilisateur voit un bouton chargé avec la fonction qui appelle et active le bouton Supprimer affiché en bas de `onClick()` `microsoftTeams.settings.setValidityState(true)` l’IFrame de la page de suppression. 

Une fois le handler de suppression exécuté, ou avertit Teams `removeEvent.notifySuccess()` du résultat de suppression de `removeEvent.notifyFailure()` contenu.

>[!NOTE]
> * Pour vous assurer que le contrôle d’un utilisateur autorisé sur un onglet n’est pas inhibé, Teams supprime l’onglet dans les cas de réussite et d’échec.
> * Teams active le bouton **Supprimer** après cinq secondes, même si votre onglet n’a pas `setValidityState()` appelé.
> * Lorsque l’utilisateur sélectionne **Supprimer,** Teams l’onglet après 30 secondes, que les actions soient terminées ou non.

## <a name="see-also"></a>Voir aussi

* [Teams onglets](~/tabs/what-are-tabs.md)
* [Créer un onglet personnel](~/tabs/how-to/create-personal-tab.md)
* [Créer un onglet de canal ou de groupe](~/tabs/how-to/create-channel-group-tab.md)
* [Créer une page de configuration](~/tabs/how-to/create-tab-pages/configuration-page.md)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Onglets sur les appareils mobiles](~/tabs/design/tabs-mobile.md)