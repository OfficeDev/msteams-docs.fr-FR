---
title: 'Quickstart: Créez un onglet personnel personnalisé avec Node.js et le générateur Yeoman pour Microsoft Teams'
author: laujan
description: Un guide rapide pour créer un onglet personnel avec le générateur Yeoman pour Microsoft Teams.
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 88ad05aacaed69d695bc918e3e8a44ec18e560ae
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566603"
---
# <a name="create-a-custom-personal-tab-using-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a>Créez un onglet personnel personnalisé à l’aide Node.js et du générateur Yeoman pour Microsoft Teams

>[!NOTE]
>Ce quickstart suit les étapes décrites dans [le Wiki Build Your First Microsoft Teams App](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) trouvé dans le référentiel microsoft OfficeDev GitHub’ordinateur.

Dans ce quickstart nous allons walk-through créer un onglet personnel personnalisé en utilisant [le Teams générateur Yeoman](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App). Nous téléchargerons également l’application sur Team.

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

**Créer un onglet configurable ou statique**

Utilisez les touches fléchées pour sélectionner l’onglet statique.

>[!IMPORTANT]
>Le composant de *chemin yourDefaultTabNameTab*, référencé dans ce quickstart, est la valeur que vous avez entré dans le générateur pour *nom d’onglet par* défaut plus le mot *Onglet*.
>
>Par exemple: DefaultTabName: *MyTab*  =>  */MyTabTab/*

## <a name="create-your-personal-tab"></a>Créez votre onglet personnel

Pour ajouter un onglet personnel à cette application, vous créerez une page de contenu et mettrez à jour les fichiers existants :

- Dans votre éditeur de code, créez un nouveau fichier HTML, **personal.html** et ajoutez la majoration suivante :

    ```html
    <!DOCTYPE html>
    <html>
        <head>
            <meta charset="UTF-8">
            <title>
                <!-- Todo: add your a title here -->
            </title>
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <!-- inject:css -->
            <!-- endinject -->
        </head>
            <body>
                <h1>Personal Tab</h1>
                <p><img src="/assets/icon.png"></p>
                <p>This is your personal tab!</p>
            </body>
    </html>
    ```

- Enregistrez **personal.html** dans le dossier Web de **votre** application :

    ```bash
    ./src/app/web/<yourDefaultTabNameTab>/personal.html
    ```

- Ouvrez **manifest.jsdans** votre éditeur de code :

    ```bash
    ./src/manifest/manifest.json/
    ```

Ajouter ce qui suit au tableau `staticTabs` vide ( ) et ajouter `staticTabs":[]` l’objet JSON suivant:

```json
{
    "entityId": "personalTab",
    "name": "Personal Tab ",
    "contentUrl": "https://{{HOSTNAME}}/<yourDefaultTabNameTab>/personal.html",
    "websiteUrl": "https://{{HOSTNAME}}",
    "scopes": ["personal"]
}

```

N’oubliez pas de mettre à jour le composant de chemin **« contentURL »** **yourDefaultTabNameTab** avec votre nom d’onglet réel.

- Enregistrez la mise **à jourmanifest.jssur**.

- Votre page de contenu doit être servie dans un IFrame. Ouvrez **Tab.ts dans** votre éditeur de code :

    ```bash
    ./src/app/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
    ```

- Ajoutez ce qui suit à la liste des décorateurs IFrame :

    ```typescript
     @PreventIframe("/<yourDefaultAppName>TabNameTab>/personal.html")
    ```

- Assurez-vous d’enregistrer le fichier **Tab.ts mis à** jour. Votre code d’onglet est complet.

## <a name="build-and-run-your-application"></a>Créez et exécutez votre application

Ouvrez une invite de commande dans votre répertoire de projet pour accomplir les tâches suivantes.

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

Pour voir votre onglet personnel, rendez-vous sur `http://localhost:3007/<yourDefaultAppNameTab>/personal.html`

>![capture d’écran onglet personnel](/microsoftteams/platform/assets/images/tab-images/personalTab.PNG)

## <a name="establish-a-secure-tunnel-to-your-tab"></a>Établissez un tunnel sécurisé à votre onglet

Microsoft Teams est un produit entièrement basé sur le cloud et exige que le contenu de votre onglet soit disponible à partir du cloud à l’aide des paramètres HTTPS. Teams n’autorise pas l’hébergement local, par conséquent, vous devez soit publier votre onglet sur une URL publique ou utiliser un proxy qui exposera votre port local à une URL orientée vers Internet.

Pour tester votre extension d’onglet, vous [utiliserez ngrok](https://ngrok.com/docs), qui est intégré dans cette application. Ngrok est un outil logiciel proxy inversé qui créera un tunnel vers les points de terminaison HTTPS accessibles au public de votre serveur Web en cours d’exécution locale. Les paramètres Web de votre serveur seront disponibles pendant la session en cours sur votre machine locale. Lorsque la machine est arrêtée ou s’enort, le service ne sera plus disponible.

Dans votre invite de commande, sortez localhost et entrez ce qui suit :

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> Une fois que votre onglet a été téléchargé sur les équipes Microsoft, via **ngrok**, et enregistré avec succès, vous pouvez le voir en Teams jusqu’à la fin de votre session tunnel.

## <a name="upload-your-application-to-teams"></a>Télécharger votre demande à Teams

- Ouvrez le Microsoft Teams client. Si vous utilisez la [version Web, vous pouvez](https://teams.microsoft.com) inspecter votre code front-end à l’aide des outils de développement de votre [navigateur](~/tabs/how-to/developer-tools.md).
- Dans le **panneau YourTeams** à gauche, sélectionnez le `...` menu à côté de l’équipe que vous utilisez pour tester votre onglet et choisir **l’équipe Manage**.
- Dans le panneau principal, **sélectionnez Apps** à partir de la barre d’onglet **et choisissez Télécharger une application** personnalisée située dans le coin inférieur droit de la page.
- Ouvrez votre répertoire de projet, parcourez **le dossier ./package,** sélectionnez le dossier zip, cliquez à droite et choisissez **Open**. Votre onglet sera téléchargé dans Teams.

## <a name="view-your-personal-tabs"></a>Consultez vos onglets personnels

Dans le navbar situé à l’extrême gauche du client Teams, sélectionnez le `...` menu et choisissez votre application dans la liste.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créez un onglet personnel à l’aide d’ASP.NETCore](~/tabs/quickstarts/create-personal-tab-dotnet-core.md)
