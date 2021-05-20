---
title: Tutoriel - Créez votre première application à l’aide du générateur Yeoman
description: Découvrez comment commencer à créer des Microsoft Teams applications avec le générateur Yeoman.
keywords: commencer node.js nodejs yeoman
localization_priority: Normal
ms.topic: tutorial
ms.custom: scenarios:getting-started
ms.openlocfilehash: 96a4f64d487e1d16bf25abd978759fedeac1061c
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566823"
---
# <a name="create-your-first-microsoft-teams-app-using-the-yeoman-generator"></a>Créez votre première application Microsoft Teams utilisant le générateur Yeoman

> [!Note]
> Ce tutoriel provient du [générateur Yeoman pour Teams wiki](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).

Dans ce tutoriel, nous allons marcher à travers la création de votre toute première application Microsoft Teams en utilisant le Microsoft Teams générateur Yeoman. Il vous guide également à travers le processus de mise à niveau de votre Teams en utilisant le générateur Yeoman. La condition préalable pour commencer avec ce tutoriel est que vous avez un compte Teams qui permet [le chargement latéral de l’application](~/concepts/build-and-test/prepare-your-o365-tenant.md).

![générateur yeoman git](~/assets/yeoman-demo.gif)

## <a name="setup-and-prepare-your-machine"></a>Configurez et préparez votre machine

Vous devez installer ce qui suit sur votre machine avant de commencer à utiliser le générateur Yeoman.

### <a name="install-nodejs"></a>Installer Node.js.

Vous devez avoir Node.js installé sur votre machine. Vous devez utiliser la dernière [version LTS](https://nodejs.org).

### <a name="install-a-code-editor"></a>Installer un éditeur de code

Vous avez besoin d’un éditeur de code. La plupart de cette documentation et images se réfèrent à [l’utilisation Visual Studio Code](https://code.visualstudio.com). Cependant, n’hésitez pas à utiliser n’importe quel éditeur de texte que vous préférez.

### <a name="install-yeoman-and-gulp-cli"></a>Installer Yeoman et Gulp CLI

Pour échafauder les projets à l’aide du générateur, vous devez installer l’outil Yeoman et gulp CLI gestionnaire de tâches.

Ouvrez une invite de commande et tapez ce qui suit :

```bash
npm install yo gulp-cli --global
```

## <a name="install-the-generator"></a>Installer le générateur

Installez le Teams générateur Yeoman avec la commande suivante :

```bash
npm install generator-teams --global
```

Installez la version d’aperçu du générateur avec la commande suivante :

```bash
npm install generator-teams@preview --global
```

## <a name="generate-your-project"></a>Générer votre projet

Cette section vous guide à travers les étapes pour générer votre projet.

**Pour générer votre projet**

1. Ouvrez une invite de commande et créez un nouvel annuaire où vous souhaitez créer votre projet, et dans ce répertoire exécuter la commande `yo teams` . Le généra teur démarre.
1. Répondez à l’ensemble des questions suscitées par le générateur :

   ![yo équipes](~/assets/yeoman-images/teams-first-app-1.png)

   1. La première question concerne le nom de votre projet, vous pouvez le laisser tel qu’il est en appuyant sur entrer.
   1. La question suivante vous demande si vous souhaitez créer un nouvel annuaire ou utiliser l’annuaire actuel. Comme vous êtes déjà dans l’annuaire que vous voulez, il suffit d’appuyer sur entrer.
   1. Dans la question suivante, tapez le titre de votre projet. Ce titre sera utilisé dans le manifeste et la description de votre application. 
   1. Ensuite, on vous demandera un nom d’entreprise, qui sera également utilisé dans le manifeste.
   1. La cinquième question vous pose quelle version du manifeste vous souhaitez utiliser. Pour ce tutoriel `v1.5` sélectionnez , qui est le schéma général actuel disponible.
   1. Ensuite, le générateur vous demandera quels éléments vous souhaitez ajouter à votre projet. Vous pouvez sélectionner un seul ou n’importe quelle combinaison d’éléments. Pour ce tutoriel, il suffit de sélectionner *un onglet*:

    ![sélection d’articles](~/assets/yeoman-images/teams-first-app-2.png)

1. Répondez à la prochaine série de questions de suivi qui apparaissent en fonction des éléments que vous avez sélectionnés à l’étape 2.
1. Entrez une URL de l’endroit où vous hébergez votre solution. 

   > [!NOTE]
   > L’URL peut être n’importe quelle URL, mais par défaut le générateur suggère une URL de site Web Azure.

1. Dans la question suivante, confirmez si vous souhaitez inclure des tests unitaires pour votre solution. La réponse par défaut est *oui*. Si vous choisissez d’inclure des tests unitaires, le projet généré aura un cadre de test unitaire et quelques tests unitaires par défaut pour les différents éléments en cours d’échafaudage. 
   > [!NOTE]
   > * Pour ce tutoriel choisissez de ne pas inclure un cadre de test.
   > * Le générateur a beaucoup de fonctionnalités avancées intégrées que vous pouvez opter pour ou désactiver.

1. Afin de faciliter votre inscription, il vous sera également demandé si vous souhaitez utiliser Azure Application Insights pour vous inscrire. Si vous choisissez *Oui,* vous devrez fournir une clé Azure Application Insights. 

   > [!NOTE]
   > Pour ce tutoriel, désinscris de l’utilisation d’Application Insights.

La prochaine série de questions sera basée sur les éléments précédemment sélectionnés. Pour un onglet, vous n’avez qu’à fournir un nom et choisir en option si vous voulez être en mesure d’utiliser cette application comme une SharePoint web en ligne. Après avoir fourni le nom, le générateur générera le projet et installera toutes les dépendances. Cela prendra une minute ou deux.

## <a name="add-some-code-to-your-tab"></a>Ajoutez du code à votre onglet

Une fois le générateur terminé, vous pouvez ouvrir la solution dans votre éditeur de code préféré. Prenez une minute ou deux et familiarisez-vous avec la façon dont le code est organisé. Pour plus d’informations, [consultez Project documentation structure.](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure)

Votre onglet est dans le `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` fichier. Il s’agit de la classe React typescript basée sur le web pour votre onglet. Localiser la méthode `render()` et ajouter une ligne de code à l’intérieur du contrôle de sorte `<PanelBody>` qu’il ressemble à ceci:

``` TypeScript
<PanelBody>
    <div style={styles.section}>
    Hello World! Yo Teams rocks!
    </div>
</PanelBody>
```

Enregistrez le fichier et retournez à l’invite de commande.

## <a name="build-your-app"></a>Créer votre application

Vous pouvez maintenant construire votre projet. Cela se fait en deux étapes (ou une étape, voir ci-dessous).

Tout d’abord, vous devez créer Teams fichier manifeste app, que vous téléchargez / sideload dans Microsoft Teams. Ceci est fait par la tâche Gulp `gulp manifest` . Cela validera le manifeste et créera un fichier zip dans `./package` l’annuaire.

Pour créer votre solution, vous utilisez la `gulp build` commande. Cela transpile votre solution dans le `./dist` dossier. 

## <a name="run-your-app"></a>Exécuter votre application

Pour exécuter votre application, vous utilisez la `gulp serve` commande. Cela permettra de créer et de démarrer un serveur Web local pour vous de tester votre application. La commande reconstruira également l’application chaque fois que vous enregistrez un fichier dans votre projet. 

Vous devriez maintenant être en mesure de naviguer pour `http://localhost:3007/myFirstAppTab/` vous assurer que votre onglet est rendu. Cependant, pas encore Microsoft Teams:

![voir votre site dans un navigateur](~/assets/yeoman-images/teams-first-app-3.png)

## <a name="run-your-app-in-microsoft-teams"></a>Exécutez votre application dans Microsoft Teams

Microsoft Teams vous permet de faire hébergé votre application sur localhost, vous devez donc soit la publier sur une URL publique, soit utiliser un proxy tel que ngrok.

La bonne nouvelle, c’est que le projet d’échafaudage a intégré ce projet. Lorsque vous `gulp ngrok-serve` exécutez le service ngrok sera commencé en arrière-plan, avec une entrée DNS unique et publique et il sera également emballer le manifeste avec cette URL unique, puis faire exactement la même chose que `gulp serve` .

Après avoir `gulp ngrok-serve` couru, créez une nouvelle équipe Microsoft Teams et quand il est créé cliquez sur le nom de l’équipe, pour aller dans les paramètres des équipes, puis sélectionnez *Apps*. Dans le coin inférieur droit, vous devriez voir un *lien Télécharger une application personnalisée,* le sélectionner, puis parcourir à votre dossier de projet et le sous-foldeur appelé `package` . Sélectionnez le fichier zip dans ce dossier et choisissez ouvert. Votre application est maintenant sideloaded dans Microsoft Teams:

![application sideloaded](~/assets/yeoman-images/teams-first-app-4.png)

Retournez sur le *canal Général* et sélectionnez pour ajouter un *+* nouvel onglet. Vous devriez voir votre onglet dans la liste des onglets:

![configurer l’onglet](~/assets/yeoman-images/teams-first-app-5.png)

Choisissez votre onglet et suivez les instructions pour l’ajouter. Notez que vous avez un dialogue de configuration personnalisé, pour lequel vous pouvez modifier la source. Sélectionnez *Enregistrer* pour ajouter votre onglet au canal. Une fois fait votre onglet doit être chargé à l’intérieur Microsoft Teams!

![onglet de course dans les équipes](~/assets/yeoman-images/teams-first-app-6.png)

## <a name="upgrade-microsoft-teams"></a>Mise à niveau Microsoft Teams

Vous pouvez également mettre à niveau votre version Microsoft Teams de la dernière version en utilisant le Microsoft Teams générateur Yeoman.

**Pour mettre à Microsoft Teams**

1. Obtenez la version actuelle de Teams avec la commande suivante :

   ```PowerShell
    yo teams --version
   ```
2. Utilisez la commande suivante pour sélectionner la mise à jour de votre générateur :

   ```PowerShell
    yo
   ```
3. Utilisez les touches fléchées pour choisir **mettre à jour vos générateurs**:

   ![image de YoSelectUpdatGen](~/assets/images/Update-Teams/YoSelectUpdateGen.png)

4. Sélectionnez le générateur que vous souhaitez à partir de la liste des générateurs :
   > [!NOTE]
   > Utilisez la barre d’espace pour sélectionner ou effacer une version Teams sélectionnée à partir des options disponibles.

    ![image de UseSpaceToSelectGenerators](~/assets/images/Update-Teams/UseSpaceToSelectGenerators.png)
    

   > [!NOTE]
   > Il faut quelques secondes à quelques minutes pour Teams’installation de l’installation.

5. Une fois l’installation terminée, utilisez la commande suivante pour vérifier la version installée :

   ```PowerShell
    yo teams --version
   ```
   
**Félicitations! Vous avez construit et déployé votre première application Microsoft Teams' argent. Vous avez également mis à Microsoft Teams.**
