---
title: 'QuickStart : créer un onglet personnel personnalisé avec node. js et le générateur Yeoman pour Microsoft teams'
author: laujan
description: Guide de démarrage rapide pour la création d’un onglet personnel avec le générateur Yeoman pour Microsoft Teams.
ms.topic: quickstart
ms.author: laujan
ms.openlocfilehash: 2d1b17360b92a161179091c1f6ba06ffa194e958
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673532"
---
# <a name="quickstart-create-a-custom-personal-tab-with-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a>QuickStart : créer un onglet personnel personnalisé avec node. js et le générateur Yeoman pour Microsoft teams

>[!NOTE]
>Ce démarrage rapide suit les étapes décrites dans le wiki de [création de votre première application Microsoft teams](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) dans le référentiel GitHub de Microsoft OfficeDev.

Dans ce démarrage rapide, nous allons passer en revue la création d’un onglet personnel personnalisé à l’aide du [Générateur Yeoman teams](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App). Nous allons également télécharger l’application vers Team.

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

**Voulez-vous créer un onglet configurable ou statique ?**

Utilisez les touches de direction pour sélectionner l’onglet statique.

>[!IMPORTANT]
>Le composant de chemin d’accès *yourDefaultTabNameTab*, référencé dans ce démarrage rapide, est la valeur que vous avez entrée dans le générateur pour le nom de l' *onglet par défaut* , ainsi que l' *onglet*mot.
>
>Par exemple : DefaultTabName : *MyTab* => */MyTabTab/*

## <a name="create-your-personal-tab"></a>Créer votre onglet personnel

Pour ajouter un onglet personnel à cette application, vous allez créer une page de contenu et mettre à jour les fichiers existants :

- Dans votre éditeur de code, créez un fichier HTML, **Personal. html** et ajoutez le balisage suivant :

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

- Enregistrez **Personal. html** dans le dossier **Web** de votre application :

```bash
./src/app/web/<yourDefaultTabNameTab>/personal.html
```

- Ouvrez **Manifest. JSON** dans votre éditeur de code :

```bash
./src/manifest/manifest.json/
```

Ajoutez ce qui suit dans le `staticTabs` tableau vide`staticTabs":[]`() et ajoutez l’objet JSON suivant :

```json
{
    "entityId": "personalTab",
    "name": "Personal Tab ",
    "contentUrl": "https://{{HOSTNAME}}/<yourDefaultTabNameTab>/personal.html",
    "websiteUrl": "https://{{HOSTNAME}}",
    "scopes": ["personal"]
}

```

N’oubliez pas de mettre à jour le composant de chemin d’accès **« contentURL »** **yourDefaultTabNameTab** avec votre nom d’onglet réel.

- Enregistrez la mise à jour de **Manifest. JSON**.

- Votre page de contenu doit être fournie dans un IFrame. Ouvrez **Tab. TS** dans votre éditeur de code :

 ```bash
./src/app/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
```

- Ajoutez les éléments suivants à la liste des décorateurs IFrame :

```typescript
 @PreventIframe("/<yourDefaultAppName>TabNameTab>/personal.html")
```

- Veillez à enregistrer le fichier **Tab. TS** mis à jour. Votre code d’onglet est complet.

## <a name="build-and-run-your-application"></a>Création et exécution de votre application

Ouvrez une invite de commandes dans le répertoire de votre projet pour effectuer les tâches suivantes.

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

Pour afficher votre onglet personnel, accédez à`http://localhost:3007/<yourDefaultAppNameTab>/personal.html`

>![capture d’écran de l’onglet personnel](/microsoftteams/platform/assets/images/tab-images/personalTab.PNG)

## <a name="establish-a-secure-tunnel-to-your-tab"></a>Établir un tunnel sécurisé vers votre onglet

Microsoft teams est un produit entièrement basé sur le Cloud et nécessite que le contenu de votre onglet soit disponible dans le nuage à l’aide de points de terminaison HTTPs. Teams n’autorise pas l’hébergement local ; par conséquent, vous devez publier votre onglet sur une URL publique ou utiliser un proxy qui exposera votre port local à une URL accessible sur Internet.

Pour tester votre extension d’onglet, vous utiliserez [ngrok](https://ngrok.com/docs), qui est intégré à cette application. Ngrok est un outil logiciel de proxy inverse qui crée un tunnel vers vos points de terminaison HTTPs de serveur Web en cours d’exécution locaux. Les points de terminaison Web de votre serveur seront disponibles pendant la session en cours sur votre ordinateur local. Lorsque l’ordinateur est arrêté ou passe en mode veille, le service n’est plus disponible.

À l’invite de commandes, quittez localhost et entrez ce qui suit :

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> Une fois que votre onglet a été téléchargé dans Microsoft Teams, via *ngrok*, et enregistré correctement, vous pouvez l’afficher dans teams jusqu’à ce que la session de tunnel se termine.

## <a name="upload-your-application-to-teams"></a>Chargement de votre application dans teams

- Ouvrez le client Microsoft Teams. Si vous utilisez la [version basée sur le Web](https://teams.microsoft.com) , vous pouvez inspecter votre code frontal à l’aide des [outils de développement](~/tabs/how-to/developer-tools.md)de votre navigateur.
- Dans le volet *YourTeams* à gauche, sélectionnez le `...` menu en regard de l’équipe que vous utilisez pour tester votre onglet, puis sélectionnez **gérer l’équipe**.
- Dans le panneau principal, sélectionnez **applications** dans la barre d’onglets et choisissez **Télécharger une application personnalisée** située dans l’angle inférieur droit de la page.
- Ouvrez le répertoire de votre projet, accédez au dossier **./Package** , sélectionnez le dossier zip, cliquez avec le bouton droit, puis choisissez **ouvrir**. Votre onglet est chargé dans Teams.

## <a name="view-your-personal-tabs"></a>Afficher vos onglets personnels

Dans la barre de navigation située à l’extrême gauche du client Teams, sélectionnez `...` le menu et choisissez votre application dans la liste.
