---
title: Créer un bouton de partage pour Teams
description: Découvrez comment ajouter le bouton Partager Teams incorporé sur votre site web, avec un aperçu du site web, à l’aide d’exemples de code
ms.topic: reference
ms.localizationpriority: medium
keywords: Partager Teams-à-Teams
ms.openlocfilehash: 05e64033d16d4b94c6ac2f9f230c296218f75517
ms.sourcegitcommit: 2fdca6fb0ade3f6b460eb9a4dfea0a8e2ab8d3b9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/08/2022
ms.locfileid: "63355873"
---
# <a name="create-share-to-teams-button"></a>Créer un bouton de partage pour Teams

Les sites web tiers peuvent utiliser le script de lancement pour incorporer des boutons De partage à Teams sur leurs pages web. Lorsque vous la sélectionnez, elle lance l’expérience de partage à Teams dans une fenêtre pop-up. Cela vous permet de partager un lien directement avec n’importe quelle personne Microsoft Teams canal sans changer de contexte. Ce document vous guide sur la création et l’incorporation d’un bouton Share-to-Teams pour votre site web, la création de l’aperçu de votre site web et l’extension de Share-to-Teams pour l'éducation.

> [!NOTE]
> * Seules les versions de bureau de MicrosoftEdge&nbsp; et Google Chrome sont pris en charge.
> * L’utilisation de freemium ou de comptes invités n’est pas prise en charge.  

L’image suivante affiche l’expérience Teams de partage :

![Fenêtre fenêtre Teams partage à la fois](~/assets/images/share-to-teams-popup.png)

## <a name="embed-a-share-to-teams-button"></a>Incorporer un partage à Teams bouton

1. Ajoutez le `launcher.js` script sur votre page web.

    ```html
    <script async defer src="https://teams.microsoft.com/share/launcher.js"></script>
    ```

1. Ajoutez un élément HTML sur votre page web avec l’attribut `teams-share-button` de classe et le lien à partager dans l’attribut `data-href` .

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>">
    </div>
    ```

    Une fois l’exécution de cette Microsoft Teams, l’icône est ajoutée à votre site web. L’image suivante illustre l’icône Partager Teams-à-vous :

    ![Icône Partager Teams partage](~/assets/icons/share-to-teams-icon.png)

1. Sinon, si vous souhaitez une taille d’icône différente pour le bouton Teams partage, utilisez l’attribut`data-icon-px-size`.

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-icon-px-size="64">
    </div>
    ```
1. Si le lien partagé nécessite l’authentification de l’utilisateur et que l’aperçu de l’URL de votre lien à partager ne s’affiche pas bien dans Teams, vous pouvez désactiver l’aperçu de l’URL `data-preview` `false`en ajoutant le jeu d’attributs à .

    ```html
    <div
      class="teams-share-button"
      data-href="https://<link-to-be-shared>"
      data-preview="false">
    </div>
    ```

1. Si votre page restituera dynamiquement le contenu, `shareToMicrosoftTeams.renderButtons()` vous pouvez utiliser la  méthode pour forcer le rendu du partage à l’endroit approprié dans le pipeline.

## <a name="craft-your-website-preview"></a>Création de la prévisualisation de votre site web

Lorsque votre site web est partagé avec Teams, la carte insérée dans le canal sélectionné contient un aperçu de votre site web. Vous pouvez contrôler le comportement de cet aperçu en vous assurant que les métadon données appropriées sont ajoutées au site web en cours de partage, telles que l’URL `data-href` .  

**Pour afficher l’aperçu**

* Vous devez inclure soit une **image miniature**, soit un **titre** et une **description**. Pour obtenir de meilleurs résultats, incluez les trois.
* L’URL partagée ne nécessite pas d’authentification. Si elle nécessite une authentification, vous pouvez la partager, mais l’aperçu n’est pas créé.

Le tableau suivant présente les balises nécessaires :

|Valeur|Balise META| Ouvrez Graph|
|----|----|----|
|Title|`<meta name="title" content="Example Page Title">`|`<meta property="og:title" content="Example Page Title">`|
|Description|`<meta name="description" content="Example Page Description">`|`<meta property="og:description" content="Example Page Description">`|
|Image miniature| aucun. |`<meta property="og:image" content="http://example.com/image.jpg">`|

Vous pouvez utiliser les versions HTML par défaut ou la version Open Graph.

## <a name="share-to-teams-for-education"></a>Partager à Teams pour l'éducation

Pour les enseignants qui utilisent le bouton Partager Teams, il existe une option supplémentaire pour .`Create an Assignment` Cela vous permet de créer rapidement une affectation dans l’équipe sélectionnée, en fonction du lien partagé. L’image suivante affiche Share-to-Teams pour l’éducation : 

![Partager pour Teams l’éducation popup](~/assets/images/share-to-teams-popup-edu.png)

## <a name="full-launcherjs-definition"></a>Définition launcher.js complète

| Propriété | Attribut HTML | Type | Par défaut | Description |
| -------------- | ---------------------- | --------------------- | ------- | ---------------------------------------------------------------------- |
| href | `data-href` | string | s/o | Href du contenu à partager. |
| preview | `data-preview` | Booléen (en tant que chaîne) | `true` | Indique si un aperçu du contenu à partager doit être présenté ou non. |
| iconPxSize | `data-icon-px-size` | number (sous la mesure d’une chaîne) | `32` | Taille en pixels du bouton De partage à Teams à restituer. |
| msgText | `data-msg-text` | string | s/o | Texte par défaut à insérer avant le lien dans la zone de composition du message. Le nombre maximal de caractères est de 200. |
| assignInstr | `data-assign-instr` | string | s/o | Texte par défaut à insérer dans le champ « Instructions » des affectations. Le nombre maximal de caractères est de 200. |
| assignTitle | `data-assign-title` | string | s/o | Texte par défaut à insérer dans le champ « Titre » des affectations. Le nombre maximal de caractères est de 50. |

### <a name="methods"></a>Méthodes

**`shareToMicrosoftTeams.renderButtons(options)`**

`options` (facultatif) : `{ elements?: HTMLElement[] }`

Actuellement, tous les boutons de partage sont restituer sur la page. Si un objet facultatif `options` est fourni avec une liste d’éléments, ces éléments sont restituer dans des boutons de partage.

### <a name="set-default-form-values"></a>Définir les valeurs de formulaire par défaut

Vous pouvez choisir de définir des valeurs par défaut pour les champs suivants sur le formulaire de partage Teams formulaire :

* Dites quelque chose à ce sujet : `msgText`
* Instructions d’affectation : `assignInstr`
* Titre de l’affectation : `assignTitle`

#### <a name="example"></a>Exemple

 Les valeurs de formulaire par défaut sont données dans l’exemple suivant :

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

[Intégrer les applications Web](~/samples/integrate-web-apps-overview.md)
