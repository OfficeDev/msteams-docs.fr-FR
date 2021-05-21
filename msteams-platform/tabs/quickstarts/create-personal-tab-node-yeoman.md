---
title: 'Démarrage rapide : créer un onglet personnel personnalisé avec Node.js et le générateur Yeoman pour Microsoft Teams'
author: laujan
description: Guide de démarrage rapide sur la création d’un onglet personnel avec le générateur Yeoman pour Microsoft Teams.
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
# <a name="create-a-custom-personal-tab-using-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a>Créer un onglet personnel personnalisé à l'Node.js et le générateur Yeoman pour Microsoft Teams

>[!NOTE]
>Ce démarrage rapide suit les étapes décrites dans le [Wiki](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) de votre première application Microsoft Teams dans le référentiel d’GitHub Microsoft OfficeDev.

Dans ce démarrage rapide, nous allons créer un onglet personnel personnalisé à l’aide Teams [générateur Yeoman.](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Nous allons également télécharger l’application dans Team.

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

**Créer un onglet configurable ou statique**

Utilisez les touches de direction pour sélectionner l’onglet statique.

>[!IMPORTANT]
>The path component *yourDefaultTabNameTab*, referenced in this quickstart, is the value that you entered in the generator for *Default Tab Name* plus the word *Tab*.
>
>Par exemple : DefaultTabName: *MyTab*  =>  */MyTabTab/*

## <a name="create-your-personal-tab"></a>Créer votre onglet personnel

Pour ajouter un onglet personnel à cette application, vous allez créer une page de contenu et mettre à jour les fichiers existants :

- Dans votre éditeur de code, créez un fichier HTML, **personal.html** et ajoutez le code suivant :

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

- Enregistrez **personal.html** dans le dossier **web de votre** application :

    ```bash
    ./src/app/web/<yourDefaultTabNameTab>/personal.html
    ```

- Ouvrez **manifest.jsdans** votre éditeur de code :

    ```bash
    ./src/manifest/manifest.json/
    ```

Ajoutez ce qui suit au tableau `staticTabs` vide ( ) et `staticTabs":[]` ajoutez l’objet JSON suivant :

```json
{
    "entityId": "personalTab",
    "name": "Personal Tab ",
    "contentUrl": "https://{{HOSTNAME}}/<yourDefaultTabNameTab>/personal.html",
    "websiteUrl": "https://{{HOSTNAME}}",
    "scopes": ["personal"]
}

```

N’oubliez pas de mettre à jour le composant de chemin d’accès **« contentURL** **» yourDefaultTabNameTab** avec votre nom d’onglet réel.

- Enregistrez lemanifest.js **mis à jour sur**.

- Votre page de contenu doit être servie dans un IFrame. Ouvrez **Tab.ts dans** votre éditeur de code :

    ```bash
    ./src/app/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
    ```

- Ajoutez ce qui suit à la liste descorateurs IFrame :

    ```typescript
     @PreventIframe("/<yourDefaultAppName>TabNameTab>/personal.html")
    ```

- Veillez à enregistrer le fichier **Tab.ts** mis à jour. Le code de l’onglet est terminé.

## <a name="build-and-run-your-application"></a>Créer et exécuter votre application

Ouvrez une invite de commandes dans le répertoire de votre projet pour effectuer les tâches suivantes.

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

Pour afficher votre onglet personnel, consultez la page `http://localhost:3007/<yourDefaultAppNameTab>/personal.html`

>![capture d’écran de l’onglet personnel](/microsoftteams/platform/assets/images/tab-images/personalTab.PNG)

## <a name="establish-a-secure-tunnel-to-your-tab"></a>Établir un tunnel sécurisé vers votre onglet

Microsoft Teams est un produit entièrement basé sur le cloud et nécessite que le contenu de votre onglet soit disponible à partir du cloud à l’aide de points de terminaison HTTPS. Teams n’autorise pas l’hébergement local, par conséquent, vous devez publier votre onglet sur une URL publique ou utiliser un proxy qui exposera votre port local à une URL internet.

Pour tester votre extension d’onglet, vous allez utiliser [ngrok,](https://ngrok.com/docs)qui est intégré à cette application. Ngrok est un outil logiciel de proxy inverse qui crée un tunnel vers les points de terminaison HTTPS disponibles publiquement de votre serveur web exécutant localement. Les points de terminaison web de votre serveur seront disponibles pendant la session en cours sur votre ordinateur local. Lorsque l’ordinateur est arrêté ou mis en veille, le service n’est plus disponible.

Dans votre invite de commandes, quittez localhost et entrez les commandes suivantes :

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> Une fois que votre onglet a été téléchargé vers Microsoft Teams, via **ngrok** et enregistré, vous pouvez l’afficher dans Teams jusqu’à la fin de votre session tunnel.

## <a name="upload-your-application-to-teams"></a>Télécharger votre application à Teams

- Ouvrez le client Microsoft Teams client. Si vous utilisez la [version web,](https://teams.microsoft.com) vous pouvez inspecter votre code frontal à l’aide des outils de développement [de votre navigateur.](~/tabs/how-to/developer-tools.md)
- Dans le **panneau YourTeams sur** la gauche, sélectionnez le menu en face de l’équipe que vous utilisez pour tester votre onglet et choisissez `...` Gérer **l’équipe.**
- Dans le panneau  principal, sélectionnez Applications dans la barre d’onglets et **choisissez Télécharger** une application personnalisée située dans le coin inférieur droit de la page.
- Ouvrez le répertoire de votre projet, accédez au dossier **./package,** sélectionnez le dossier zip, cliquez avec le bouton droit, puis choisissez **Ouvrir**. Votre onglet est chargé dans Teams.

## <a name="view-your-personal-tabs"></a>Afficher vos onglets personnels

Dans la barre de navigation située à l’extrême gauche du client Teams, sélectionnez le menu et choisissez votre application dans `...` la liste.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créer un onglet personnel à l’aide d’ASP.NETCore](~/tabs/quickstarts/create-personal-tab-dotnet-core.md)
