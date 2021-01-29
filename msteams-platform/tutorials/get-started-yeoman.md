---
title: 'Didacticiel : créer votre première application à l’aide du générateur Yeoman'
description: Découvrez comment commencer à créer des applications Microsoft Teams avec le générateur Yeoman.
keywords: mise en node.js nodejs yeoman
ms.topic: tutorial
ms.custom: scenarios:getting-started
ms.openlocfilehash: f7f0fb3ba1be28dfa7d343be3af9d122b4ad090d
ms.sourcegitcommit: fa64b83c0b534bf7a89f256880d5b5ca193e4b04
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/28/2021
ms.locfileid: "50037003"
---
# <a name="create-your-first-microsoft-teams-app-using-the-yeoman-generator"></a>Créer votre première application Microsoft Teams à l’aide du générateur Yeoman

>[!Note]
>Ce didacticiel provient du [générateur Yeoman pour le wiki Teams.](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)

Dans ce didacticiel, nous allons passer en premier lieu à la création de votre toute première application Microsoft Teams à l’aide du générateur Yeoman Microsoft Teams. Il part du principe que vous avez un compte Teams qui permet le chargement de version de [l’application.](~/concepts/build-and-test/prepare-your-o365-tenant.md)

![Git du générateur yeoman](~/assets/yeoman-demo.gif)

## <a name="setup-and-prepare-your-machine"></a>Installer et préparer votre ordinateur

Vous devez installer ce qui suit sur votre ordinateur avant de commencer à utiliser le générateur Yeoman.

### <a name="install-nodejs"></a>Installer Node.js.

Vous devez avoir installé Node.js sur votre ordinateur. Vous devez utiliser la dernière [version de LTS.](https://nodejs.org)

### <a name="install-a-code-editor"></a>Installer un éditeur de code

Vous avez également besoin d’un éditeur de code, n’hésitez pas à utiliser l’éditeur de texte de votre choix. Toutefois, la plupart de cette documentation et captures d’écran font référence à [l’utilisation Visual Studio Code](https://code.visualstudio.com).

### <a name="install-yeoman-and-gulp-cli"></a>Installer Yeoman et Gulp CLI

Pour pouvoir échafauder des projets à l’aide du générateur Teams, vous devez installer l’outil Yeoman ainsi que le gestionnaire des tâches gulp CLI.

Ouvrez une invite de commandes et tapez ce qui suit :

```bash
npm install yo gulp-cli --global
```

## <a name="install-the-generator"></a>Installer le générateur

Installez le générateur Yeoman teams avec la commande suivante :

```bash
npm install generator-teams --global
```

Pour installer les versions d’aperçu du générateur, exécutez la commande ci-après :

```bash
npm install generator-teams@preview --global
```

## <a name="generate-your-project"></a>Générer votre projet

Ouvrez une invite de commandes et créez un répertoire dans lequel vous souhaitez créer votre projet et dans ce répertoire exécutez la `yo teams` commande.

Cela démarre le générateur, qui vous invite à répondre à un ensemble de questions.

![équipes yo](~/assets/yeoman-images/teams-first-app-1.png)

La première question porte sur le nom de votre projet, vous pouvez le laisser tel qu’il est en appuyant sur Entrée. La question suivante vous demande si vous souhaitez créer un répertoire ou utiliser le répertoire actuel. Comme nous sommes déjà dans le répertoire que nous voulons, nous appuyons simplement sur Entrée.

L’étape suivante demande un titre de votre projet, ce titre sera utilisé dans le manifeste et la description de votre application. Vous serez ensuite invité à obtenir un nom de société, qui sera également utilisé dans le manifeste.

La cinquième question vous demande quelle version du manifeste vous souhaitez utiliser. Pour ce didacticiel, `v1.5` sélectionnez, qui est le schéma général disponible actuel.

Après cela, le générateur vous demandera quels éléments vous souhaitez ajouter à votre projet. Vous pouvez sélectionner un seul ou n’importe quelle combinaison d’éléments. Pour l’instant, sélectionnez *simplement un onglet.*

![sélection d’élément](~/assets/yeoman-images/teams-first-app-2.png)

En fonction des éléments que vous sélectionnez, vous serez invité à répondre à un ensemble de questions de suivi.

Vous devez maintenant entrer une URL de l’endroit où vous hébergez votre solution. Il peut s’agit de n’importe quelle URL, mais par défaut, le générateur suggère une URL de sites web Azure.

Le générateur comporte un grand nombre de fonctionnalités avancées intégrées que vous pouvez choisir d’utiliser ou de refuser. À la suite de la question d’URL qui vous sera posée si vous souhaitez inclure un test unitaire pour votre solution, la valeur par défaut est oui. Si vous choisissez cette option, le projet généré aura une infrastructure de test unitaire et certains tests unitaires par défaut pour les différents éléments en cours de structure. Pour ce didacticiel, choisissez de ne pas inclure d’infrastructure de test.

Pour faciliter la journalisation, vous serez également invité à utiliser Azure Application Insights pour la journalisation. Si vous choisissez Oui, vous devez fournir une clé Azure Application Insights. Pour ce didacticiel, dés optez pour l’utilisation d’Application Insights.

L’ensemble de questions suivant sera basé sur votre sélection d’éléments précédemment. Pour un onglet, vous devez uniquement fournir un nom et éventuellement choisir si vous souhaitez être en mesure d’utiliser cette application en tant que partie Web SharePoint Online. Une fois que vous avez fourni ce nom, le générateur génère le projet et installe toutes les dépendances. Cela prendra une minute ou deux.

## <a name="add-some-code-to-your-tab"></a>Ajouter du code à votre onglet

Une fois le générateur terminé, vous pouvez ouvrir la solution dans votre éditeur de code favori. Prenez une ou deux minutes et familiarisez-vous avec la façon dont le code est organisé . Vous pouvez en savoir plus à ce sujet dans la documentation [de structure de](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure) projet.

Votre onglet se trouve dans le `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` fichier. Il s’agit de la classe React TypeScript pour votre onglet. Recherchez la méthode et ajoutez une ligne de code à l’intérieur du contrôle afin qu’elle `render()` `<PanelBody>` ressemble à ceci :

``` TypeScript
<PanelBody>
    <div style={styles.section}>
    Hello World! Yo Teams rocks!
    </div>
</PanelBody>
```

Enregistrez le fichier et revenir à l’invite de commandes.

## <a name="build-your-app"></a>Créer votre application

Vous pouvez maintenant créer votre projet. Cette étape est effectuée en deux étapes (ou une étape, voir ci-dessous).

Tout d’abord, vous devez créer le fichier manifeste de l’application Teams, que vous téléchargez/chargez de nouveau dans Microsoft Teams. Cette tâche est effectuée par la tâche Gulp `gulp manifest` . Cela valide le manifeste et crée un fichier zip dans `./package` le répertoire.

Pour créer votre solution, utilisez la `gulp build` commande. Cela transpile votre solution dans le `./dist` dossier. 

## <a name="run-your-app"></a>Exécuter votre application

Pour exécuter votre application, utilisez la `gulp serve` commande. Cela permet de créer et de démarrer un serveur web local pour tester votre application. La commande reconstruira également l’application chaque fois que vous enregistrez un fichier dans votre projet. 

Vous devez maintenant être en mesure de parcourir pour `http://localhost:3007/myFirstAppTab/` vous assurer que votre onglet est rendu. Toutefois, pas encore dans Microsoft Teams.

![afficher votre site dans un navigateur](~/assets/yeoman-images/teams-first-app-3.png)

## <a name="run-your-app-in-microsoft-teams"></a>Exécuter votre application dans Microsoft Teams

Microsoft Teams ne vous permet pas d’héberger votre application sur localhost. Vous devez donc la publier sur une URL publique ou utiliser un proxy tel que ngrok.

La bonne nouvelle est que le projet échafaudé dispose de ce projet intégré. Lorsque vous exécutez le service ngrok, il est démarré en arrière-plan, avec une entrée DNS unique et publique, et il inséra également le manifeste avec cette URL unique, puis il fera exactement la même chose que `gulp ngrok-serve` `gulp serve` .

Après l’exécution, créez une équipe Microsoft Teams et, lorsqu’elle est créée, cliquez sur le nom de l’équipe, pour aller aux paramètres d’équipe, puis `gulp ngrok-serve` sélectionnez *Applications.* Dans le coin inférieur droit, vous devez voir un lien Télécharger une application *personnalisée,* sélectionnez-la, puis accédez au dossier de votre projet et au sous-dossier `package` appelé. Sélectionnez le fichier zip dans ce dossier, puis ouvrez. Votre application est désormais rechargée de nouveau dans Microsoft Teams.

![application sideloaded](~/assets/yeoman-images/teams-first-app-4.png)

Revenir au canal *Général* et choisir *+* d’ajouter un nouvel onglet. Votre onglet doit s’y voir dans la liste des onglets.

![configurer l’onglet](~/assets/yeoman-images/teams-first-app-5.png)

Choisissez votre onglet et suivez les instructions pour l’ajouter. Notez que vous avez une boîte de dialogue de configuration personnalisée, pour laquelle vous pouvez modifier la source. Sélectionnez *Enregistrer* pour ajouter votre onglet au canal. Une fois que vous avez terminé, votre onglet doit être chargé dans Microsoft Teams !

![exécution de l’onglet dans teams](~/assets/yeoman-images/teams-first-app-6.png)

**Félicitations ! Vous avez créé et déployé votre première application Microsoft Teams**
