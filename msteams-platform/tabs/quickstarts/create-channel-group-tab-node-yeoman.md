---
title: Créer un onglet de canal et de groupe personnalisé avec Node.js et le générateur Yeoman pour Microsoft teams
author: laujan
description: Guide de démarrage rapide pour la création d’un onglet de canal et de groupe avec le générateur Yeoman pour Microsoft Teams.
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 77081f83c753f812032ccfebe2accd3cb8859f99
ms.sourcegitcommit: e8dfcb167274e996395b77d65999991a18f2051a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/15/2020
ms.locfileid: "47818933"
---
# <a name="create-a-custom-channel-and-group-tab-with-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a>Créer un onglet de canal et de groupe personnalisé avec Node.js et le générateur Yeoman pour Microsoft teams

>[!NOTE]
>Ce démarrage rapide suit les étapes décrites dans le wiki de [création de votre première application Microsoft teams](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) dans le référentiel GitHub de Microsoft OfficeDev.

Dans ce démarrage rapide, nous allons passer en revue la création d’un onglet de canal et de groupe personnalisé à l’aide du [Générateur Yeoman teams](https://github.com/OfficeDev/generator-teams/).

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

**Voulez-vous créer un onglet configurable ou statique ?**

Utilisez les touches de direction pour sélectionner l’onglet configurable.

**Quelles étendues envisagez-vous d’utiliser pour votre onglet ?**

Vous pouvez sélectionner une équipe et/ou une conversation de groupe

**Voulez-vous que cet onglet soit disponible dans SharePoint Online ? (O/n)** 

Sélectionnez **n**.

>[!IMPORTANT]
>Le composant de chemin d’accès **yourDefaultTabNameTab**, référencé dans ce démarrage rapide, est la valeur que vous avez entrée dans le générateur pour le nom de l' **onglet par défaut** , ainsi que l' **onglet**mot.
>
>Par exemple : DefaultTabName : **MyTab**  =>  **/MyTabTab/**

Dans le répertoire de votre projet, accédez à l’un des éléments suivants :

```bash
./src/app/scripts/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.tsx
```

C’est ici que vous trouverez votre logique d’onglet. Recherchez la `render()` méthode et ajoutez la `<div>` balise et le contenu suivants en haut du `<PanelBody>` Code de conteneur :

```html
    <PanelBody>
        <div style={styles.section}>
            Hello World! Yo Teams rocks!
        </div>
    </PanelBody>
```

Veillez à enregistrer le fichier mis à jour.

## <a name="build-and-run-your-application"></a>Création et exécution de votre application

Ouvrez une invite de commandes dans le répertoire de votre projet pour effectuer les tâches suivantes.

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

Pour afficher la page de configuration de votre onglet, accédez à `https://localhost:3007/<yourDefaultAppNameTab>/config.html` . Vous devez voir les éléments ci-après :

![capture d’écran de la page de configuration](~/assets/images/tab-images/configurationPage.png)

## <a name="establish-a-secure-tunnel-to-your-tab"></a>Établir un tunnel sécurisé vers votre onglet

Microsoft teams est un produit entièrement basé sur le Cloud et nécessite que le contenu de votre onglet soit disponible dans le nuage à l’aide de points de terminaison HTTPs. Teams n’autorise pas l’hébergement local ; par conséquent, vous devez publier votre onglet sur une URL publique ou utiliser un proxy qui exposera votre port local à une URL accessible sur Internet.

Pour tester votre extension d’onglet, vous utiliserez [ngrok](https://ngrok.com/docs), qui est intégré à cette application. Ngrok est un outil logiciel de proxy inverse qui crée un tunnel vers vos points de terminaison HTTPs de serveur Web en cours d’exécution locaux. Les points de terminaison Web de votre serveur seront disponibles pendant la session en cours sur votre ordinateur local. Lorsque l’ordinateur est arrêté ou passe en mode veille, le service n’est plus disponible.

À l’invite de commandes, quittez localhost et entrez ce qui suit :

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> Une fois que votre onglet a été téléchargé dans Microsoft teams et enregistré correctement, vous pouvez l’afficher dans la Galerie des onglets, l’ajouter à la barre d’onglets et interagir avec lui jusqu’à la fin de votre session de tunnel ngrok. Si vous redémarrez votre session ngrok, vous devrez mettre à jour votre application avec la nouvelle URL.

## <a name="upload-your-application-to-teams"></a>Chargement de votre application dans teams

- Ouvrez le client Microsoft Teams. Si vous utilisez la [version basée sur le Web](https://teams.microsoft.com) , vous pouvez inspecter votre code frontal à l’aide des [outils de développement](~/tabs/how-to/developer-tools.md)de votre navigateur.
- Dans le volet *YourTeams* à gauche, sélectionnez le `...` menu en regard de l’équipe que vous utilisez pour tester votre onglet, puis sélectionnez **gérer l’équipe**.
- Dans le panneau principal, sélectionnez **applications** dans la barre d’onglets et choisissez **Télécharger une application personnalisée** située dans l’angle inférieur droit de la page.
- Ouvrez le répertoire de votre projet, accédez au dossier **./Package** , sélectionnez le dossier zip du package d’application, puis choisissez **ouvrir**. Votre onglet est chargé dans Teams.
- Revenez à votre équipe, choisissez le canal où vous souhaitez afficher l’onglet, sélectionnez ➕ dans la barre d’onglets, puis choisissez votre onglet dans la Galerie.
- Suivez les instructions relatives à l’ajout d’un onglet. Notez qu’il existe une boîte de dialogue de configuration personnalisée pour l’onglet canal/groupe.
- Sélectionnez **Enregistrer** et votre onglet est ajouté à la barre d’onglets de la chaîne.
