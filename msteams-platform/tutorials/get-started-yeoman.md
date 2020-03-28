---
title: Prise en main du générateur Yeoman pour Microsoft teams
description: Commencer à créer des applications intéressantes avec le générateur Yeoman pour Microsoft teams
keywords: nœud de mise en route. js NodeJS Yeoman
ms.topic: tutorial
ms.custom: scenarios:getting-started
ms.openlocfilehash: 217c0900e067a61e083e7ffb0b121afdaa51c49f
ms.sourcegitcommit: b13b38a104946c32cd5245a7af706070e534927d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2020
ms.locfileid: "43034042"
---
# <a name="build-your-first-microsoft-teams-app"></a>Créer votre première application Microsoft teams

>[!Note]
>Ce didacticiel provient du [Générateur Yeoman pour le wiki teams](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)

Dans ce didacticiel, nous allons passer par la création de votre première application Microsoft teams à l’aide du générateur Yeoman de Microsoft Teams. Il part du principe que vous avez [activé le chargement latéral des applications Microsoft teams](~/concepts/build-and-test/prepare-your-o365-tenant.md).

![git du générateur Yeoman](~/assets/yeoman-demo.gif)

## <a name="setup-and-prepare-your-machine"></a>Configurer et préparer votre ordinateur

Vous devez installer les éléments suivants sur votre ordinateur avant de commencer à utiliser le générateur teams.

### <a name="install-node"></a>Nœud Installer

NodeJS doit être installé sur votre ordinateur. Vous devez utiliser la dernière [version d’LTS](https://nodejs.org/dist/latest-v8.x/).

### <a name="install-a-code-editor"></a>Installer un éditeur de code

Vous avez également besoin d’un éditeur de code, n’hésitez pas à utiliser l’éditeur de texte de votre choix. Toutefois, la plupart de ces documents et captures d’écran font référence à l’utilisation de [Visual Studio code](https://code.visualstudio.com).

### <a name="install-yeoman-and-gulp-cli"></a>Installer Yeoman et Gulp CLI

Pour être en mesure de structurer des projets à l’aide du générateur Teams, vous devez installer l’outil Yeoman ainsi que le gestionnaire des tâches CLI de Gulp.

Ouvrez une invite de commandes et tapez ce qui suit :

```bash
npm install yo gulp-cli --global
```

## <a name="install-the-microsoft-teams-apps-generator---yo-teams"></a>Installer le générateur d’applications Microsoft teams-Yo teams

Le générateur Yeoman pour les applications Microsoft teams est installé avec la commande suivante :

```bash
npm install generator-teams --global
```

#### <a name="install-preview-versions"></a>Installer les versions d’évaluation

Si vous souhaitez installer des versions d’évaluation du générateur teams à l’aide de cette commande, procédez comme suit :

```bash
npm install generator-teams@preview --global
```

## <a name="generate-your-project"></a>Générer votre projet

Ouvrez une invite de commandes et créez un répertoire dans lequel vous souhaitez créer votre projet, puis tapez la commande `yo teams`dans ce répertoire. Cette opération démarre le générateur d’applications teams et vous demande un ensemble de questions.

![Yo teams](~/assets/yeoman-images/teams-first-app-1.png)

La première question concerne le nom de votre projet, vous pouvez la laisser telle quelle en appuyant sur entrée. La question suivante vous demande si vous souhaitez créer un nouveau répertoire ou utiliser le répertoire actuel. Comme nous l’avons déjà fait dans le répertoire que nous souhaitons, nous appuyons simplement sur entrée.

L’étape suivante demande un titre de votre projet, ce titre sera utilisé dans le manifeste et la description de votre application. Puis vous serez invité à indiquer un nom d’entreprise, qui sera également utilisé dans le manifeste.

La cinquième question vous demande quelle version du manifeste vous souhaitez utiliser. Pour ce didacticiel, `v1.5`sélectionnez, qui est le schéma actuellement disponible général.

Une fois que ce générateur vous demandera quels éléments vous souhaitez ajouter à votre projet. Vous pouvez sélectionner une seule combinaison ou une combinaison d’éléments. Pour le moment, il vous suffit de sélectionner *un onglet*.

![sélection de l’élément](~/assets/yeoman-images/teams-first-app-2.png)

En fonction des éléments que vous sélectionnez, vous serez invité à un ensemble de questions de suivi.

À présent, vous devez entrer une URL où vous allez héberger votre solution. Il peut s’agir de n’importe quelle URL, mais par défaut, le générateur suggère une URL de sites Web Azure.

Le générateur dispose d’un grand nombre de fonctionnalités avancées intégrées que vous pouvez accepter ou refuser. À la suite de la question URL, vous serez invité à indiquer si vous souhaitez inclure des tests unitaires pour votre solution, la valeur par défaut est oui. Si vous choisissez cette option, le projet généré disposera d’une infrastructure de test d’unité et de tests d’unité par défaut pour les différents éléments en cours de génération. Pour ce didacticiel, choisissez de ne pas inclure d’infrastructure de test.

Pour faciliter la journalisation, vous serez également invité à indiquer si vous souhaitez utiliser Azure application Insights pour la journalisation. Si vous choisissez Oui, vous devrez fournir une clé Insights d’application Azure. Pour ce didacticiel, n’utilisez pas les informations d’application.

Le prochain ensemble de questions sera basé sur votre sélection d’éléments précédemment. Pour un onglet, vous devez uniquement fournir un nom et éventuellement choisir si vous souhaitez pouvoir utiliser cette application en tant que composant WebPart SharePoint Online. Une fois que vous avez fourni ce nom, le générateur génère le projet et installe toutes les dépendances. Cette opération prend une ou deux minutes.

## <a name="add-some-code-to-your-tab"></a>Ajouter du code à votre onglet

Une fois le générateur exécuté, vous pouvez ouvrir la solution dans votre éditeur de code favori. Prenez une ou deux minutes et familiarisez-vous avec la façon dont le code est organisé, vous pouvez en savoir plus à ce sujet dans la documentation sur la [structure du projet](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure) .

Votre onglet sera situé dans le `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` fichier. Il s’agit de la classe basée sur les réplications de `render()` type dactylographié pour votre onglet. Recherchez la méthode `<PanelBody>` et ajoutez une ligne de code à l’intérieur du contrôle afin qu’elle se présente comme suit :

``` TypeScript
<PanelBody>
    <div style={styles.section}>
    Hello World! Yo Teams rocks!
    </div>
</PanelBody>
```

Enregistrez le fichier et revenez à l’invite de commandes.

## <a name="build-your-app"></a>Créer votre application

Vous pouvez maintenant générer votre projet. Cette opération est réalisée en deux étapes (ou une seule étape, voir ci-dessous).

Tout d’abord, vous devez créer le fichier manifeste de l’application teams que vous téléchargez/chargement dans Microsoft Teams. Cette opération est exécutée par la `gulp manifest`tâche Gulp. Cela permet de valider le manifeste et de créer un fichier zip `./package` dans le répertoire.

Pour créer votre solution, utilisez la `gulp build` commande. Cela permet de transpiler votre solution `./dist` dans le dossier. 

## <a name="run-your-app"></a>Exécuter votre application

Pour exécuter votre application, vous utilisez `gulp serve` la commande. Cela permet de créer et de démarrer un serveur Web local pour tester votre application. La commande reconstruira également l’application chaque fois que vous enregistrerez un fichier dans votre projet. 

Vous devez maintenant être en mesure d’accéder `http://localhost:3007/myFirstAppTab/` à pour vérifier que votre onglet est rendu. Toutefois, vous ne disposez pas encore de Microsoft Teams.

![afficher votre site dans un navigateur](~/assets/yeoman-images/teams-first-app-3.png)

## <a name="run-your-app-in-microsoft-teams"></a>Exécuter votre application dans Microsoft teams

Microsoft Teams ne vous permet pas d’héberger votre application sur localhost, c’est pourquoi vous devez la publier sur une URL publique ou utiliser un proxy tel que ngrok.

La bonne nouvelle est que le projet de génération de modèles automatique dispose de cette configuration intégrée. Lorsque vous exécutez `gulp ngrok-serve` le service ngrok est démarré en arrière-plan, avec une entrée DNS unique et publique, et il compresse également le manifeste avec cette URL unique, puis effectue exactement la même chose que `gulp serve`.

Après avoir `gulp ngrok-serve`exécuté, créez une nouvelle équipe Microsoft teams et, lorsqu’elle est créée, cliquez sur le nom de l’équipe, pour accéder aux paramètres Teams, puis sélectionnez *applications*. Dans le coin inférieur droit, vous devriez voir un lien *charger une application personnalisée*, sélectionnez-le, puis accédez à votre dossier de projet et le `package`sous-dossier appelé. Sélectionnez le fichier zip dans ce dossier, puis cliquez sur Ouvrir. Votre application est désormais versions test chargées dans Microsoft Teams.

![application versions test chargées](~/assets/yeoman-images/teams-first-app-4.png)

Revenez à la chaîne *général* et sélectionnez *+* pour ajouter un nouvel onglet. Votre onglet doit apparaître dans la liste des onglets.

![onglet configurer](~/assets/yeoman-images/teams-first-app-5.png)

Choisissez votre onglet et suivez les instructions pour l’ajouter. Notez que vous disposez d’une boîte de dialogue de configuration personnalisée, pour laquelle vous pouvez modifier la source. Sélectionnez *Enregistrer* pour ajouter votre onglet au canal. Une fois que vous avez fini de charger votre onglet dans Microsoft teams !

![onglet en cours d’exécution dans teams](~/assets/yeoman-images/teams-first-app-6.png)

**Félicitations ! Vous avez créé et déployé votre première application Microsoft teams**
