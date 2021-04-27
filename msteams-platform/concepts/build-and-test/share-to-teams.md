---
title: Bouton Créer un partage avec Teams
description: Comment ajouter le bouton Share to Teams incorporé sur votre site web
ms.topic: reference
localization_priority: Normal
keywords: Partager Teams entre équipes
ms.openlocfilehash: c77c4149c95685e17e8f789a9536b4d81e05d13f
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020822"
---
# <a name="create-share-to-teams-button"></a>Bouton Créer un partage avec Teams

Les sites web tiers peuvent utiliser le script de lancement pour incorporer des boutons Share-to-Teams sur leurs pages web. Lorsque vous la sélectionnez, elle lance l'expérience Partager avec Teams dans une fenêtre fenêtre. Cela vous permet de partager un lien directement avec une personne ou un canal Microsoft Teams sans changer de contexte. Ce document vous guide sur la création et l'incorporation d'un bouton Partager avec Teams pour votre site web, la création de l'aperçu de votre site web et l'extension de Share-to-Teams pour l'Éducation.

> [!NOTE]
> * Seules les versions de bureau de Edge et Chrome sont pris en charge.
> * L'utilisation de freemium ou de comptes invités n'est pas prise en charge.  

L'image suivante affiche l'expérience de partage à teams :

![Fenêtre popup Share-to-Teams](~/assets/images/share-to-teams-popup.png)

## <a name="embed-a-share-to-teams-button"></a>Incorporer un bouton Partager dans Teams

1. Ajoutez `launcher.js` le script sur votre page web.

    ```html
    <script async defer src="https://teams.microsoft.com/share/launcher.js"></script>
    ```

1. Ajoutez un élément HTML sur votre page web avec l'attribut de classe et `teams-share-button` le lien à partager dans l'attribut. `data-href`

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>">
    </div>
    ```

    Une fois que vous avez terminé, l'icône Microsoft Teams est ajoutée à votre site web. L'image suivante montre l'icône Partager avec Teams :

    ![Icône Partager avec Teams](~/assets/icons/share-to-teams-icon.png)

1. Sinon, si vous souhaitez une taille d'icône différente pour le bouton Partager avec Teams, utilisez `data-icon-px-size` l'attribut.

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-icon-px-size="64">
    </div>
    ```
1. Si le lien partagé nécessite l'authentification de l'utilisateur et que l'aperçu de l'URL de votre lien à partager ne s'affiche pas bien dans Teams, vous pouvez désactiver l'aperçu de l'URL en ajoutant le jeu d'attributs à `data-preview` `false` .

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-preview="false">
    </div>
    ```

1. Si votre page restituera dynamiquement le contenu, vous pouvez utiliser la méthode pour forcer le bouton Partager à s'restituer à `shareToMicrosoftTeams.renderButtons()` l'endroit approprié dans le pipeline. 

## <a name="craft-your-website-preview"></a>Création de la prévisualisation de votre site web

Lorsque votre site web est partagé avec Teams, la carte insérée dans le canal sélectionné contient un aperçu de votre site web. Vous pouvez contrôler le comportement de cet aperçu en vous assurant que les métadon données appropriées sont ajoutées au site web en cours de partage, telles que `data-href` l'URL.  

**Pour afficher l'aperçu**

* Vous devez inclure soit une **image miniature,** soit un **titre** et une **description.** Pour obtenir de meilleurs résultats, incluez les trois.
* L'URL partagée ne nécessite pas d'authentification. Si elle nécessite une authentification, vous pouvez la partager, mais l'aperçu n'est pas créé.

Le tableau suivant présente les balises nécessaires :

|Valeur|Balise META| Open Graph|
|----|----|----|
|Titre|`<meta name="title" content="Example Page Title">`|`<meta property="og:title" content="Example Page Title">`|
|Description|`<meta name="description" content="Example Page Description">`|`<meta property="og:description" content="Example Page Description">`|
|Image miniature| aucun. |`<meta property="og:image" content="http://example.com/image.jpg">`|

Vous pouvez utiliser les versions html par défaut ou la version Open Graph.

## <a name="share-to-teams-for-education"></a>Partager avec Teams pour l'Éducation

Pour les enseignants qui utilisent le bouton Partager avec Teams, il existe une option supplémentaire pour `Create an Assignment` . Cela vous permet de créer rapidement une affectation dans l'équipe sélectionnée, en fonction du lien partagé. L'image suivante affiche Share-to-Teams pour l'éducation : 

![Partager avec l'éducation popup Teams](~/assets/images/share-to-teams-popup-edu.png)

## <a name="full-launcherjs-definition"></a>Définition launcher.js complète

| Propriété | Attribut HTML | Type | Par défaut | Description |
| -------------- | ---------------------- | --------------------- | ------- | ---------------------------------------------------------------------- |
| href | `data-href` | string | s/o | Href du contenu à partager. |
| preview | `data-preview` | booléen (sous la mesure d'une chaîne) | `true` | Indique si un aperçu du contenu à partager est à afficher ou non. |
| iconPxSize | `data-icon-px-size` | number (en tant que chaîne) | `32` | Taille en pixels du bouton Partager avec Teams à restituer. |
| msgText | `data-msg-text` | string | s/o | Texte par défaut à insérer avant le lien dans la zone de composition du message. Le nombre maximal de caractères est de 200. |
| assignInstr | `data-assign-instr` | string | s/o | Texte par défaut à insérer dans le champ « Instructions » des affectations. Le nombre maximal de caractères est de 200. |
| assignTitle | `data-assign-title` | string | s/o | Texte par défaut à insérer dans le champ « Titre » des affectations. Le nombre maximal de caractères est de 50. |

### <a name="methods"></a>Méthodes

**`shareToMicrosoftTeams.renderButtons(options)`**

`options` (facultatif) : `{ elements?: HTMLElement[] }`

Actuellement, tous les boutons de partage sont restituer sur la page. Si un objet facultatif est fourni avec une liste d'éléments, ces éléments sont restituer dans `options` des boutons de partage.

### <a name="set-default-form-values"></a>Définir les valeurs de formulaire par défaut

Vous pouvez choisir de définir des valeurs par défaut pour les champs suivants dans le formulaire Partager avec Teams :

* Dites quelque chose à ce sujet : `msgText`
* Instructions d'affectation : `assignInstr`
* Titre de l'affectation : `assignTitle`

#### <a name="example"></a>Exemple

 Les valeurs de formulaire par défaut sont données dans l'exemple suivant :

```html
<span
    class="teams-share-button"
    data-href="https://www.microsoft.com/education/products/teams"
    data-msg-text="Default Message"
    data-assign-title="Default Assignment Title"
    data-assign-instr="Default Assignment Instructions"
></span>
```

## <a name="see-also"></a>Voir aussi

> [!div class="nextstepaction"]
> [Intégrer les applications Web](~/samples/integrate-web-apps-overview.md)
