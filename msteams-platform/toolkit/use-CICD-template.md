---
title: Découvrez comment utiliser des modèles de pipeline CI/CD dans GitHub, Azure DevOps et Jenkins pour les développeurs d’applications Teams
author: MuyangAmigo
description: Modèles CI/CD
ms.author: ruhe
ms.localizationpriority: medium
ms.topic: overview
ms.date: 04/20/2022
ms.openlocfilehash: 66560b1f228c32b0faf6569ff0ae536a81dc33c0
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073292"
---
# <a name="set-up-cicd-pipelines"></a>Configurer des pipelines CI/CD

TeamsFx permet d’automatiser votre flux de travail de développement lors de la création d’Teams application. Voici les outils et modèles que vous pouvez utiliser pour configurer des pipelines CI/CD, créer des modèles de flux de travail et personnaliser le flux de travail CI/CD avec GitHub, Azure DevOps, Jenkins et d’autres plateformes. Pour provisionner et déployer des ressources, vous pouvez créer des principaux de service Azure et publier l’application Teams à l’aide Teams Portail des développeurs. Pour publier manuellement Teams application, vous pouvez tirer parti [du portail des développeurs pour Teams](https://dev.teams.microsoft.com/home).


|Outils et modèles | Description |
|---|---|
|[TeamsFx-CLI-Action](https://github.com/OfficeDev/teamsfx-cli-action)|GitHub Action qui s’intègre à l’interface CLI TeamsFx.|
|[Teams Shared Computer Toolkit dans Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)| Visual Studio Code extension qui vous aide à développer Teams application ainsi que des workflows d’automatisation pour GitHub, Azure DevOps et Jenkins. |
|[TeamsFx CLI](https://www.npmjs.com/package/@microsoft/teamsfx-cli) | Outil en ligne de commande qui vous aide à développer Teams application ainsi que des workflows d’automatisation pour GitHub, Azure DevOps et Jenkins.|
|[script-ci-template.sh](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh) et [script-cd-template.sh](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)| Modèles de script pour l’automatisation en dehors de GitHub, Azure DevOps ou Jenkins. |


## <a name="set-up-pipelines"></a>Configurer des pipelines

Vous pouvez configurer des pipelines avec les plateformes suivantes :

1. [Configurer des pipelines avec GitHub](#set-up-pipelines-with-github)
1. [Configurer des pipelines avec Azure DevOps](#set-up-pipelines-with-azure-devops)
1. [Configurer des pipelines avec Jenkins](#set-up-pipelines-with-jenkins)
1. [Configurer des pipelines pour d’autres plateformes](#set-up-pipelines-for-other-platforms)


### <a name="set-up-pipelines-with-github"></a>Configurer des pipelines avec GitHub

Pour configurer des pipelines avec GitHub pour CI/CD :

1. Créez des modèles de flux de travail.

   * Visual Studio Code
   * TeamsFx CLI

1. Personnalisez le flux de travail CI/CD.


## <a name="create-workflow-templates-with-github"></a>Créer des modèles de flux de travail avec GitHub

**Créer des modèles de flux de travail à l’aide de la Teams Shared Computer Toolkit dans Visual Studio Code**

1. Créez un projet d’application Teams à l’aide de Teams Shared Computer Toolkit.
1. Sélectionnez **Teams Shared Computer Toolkit** icône dans la barre d’activité Visual Studio Code.
1. Sélectionnez **Ajouter des flux de travail CI/CD**.
1. Sélectionnez un environnement dans l’invite de commandes.
1. Sélectionnez **GitHub** comme fournisseur CI/CD.
1. Sélectionnez au moins un modèle parmi ces options : CI, CD, Provision ou Publier sur Teams.
1. Ouvrez le modèle et personnalisez les flux de travail qui s’intègrent dans vos scénarios.
1. Suivez les fichiers README sous `.github/workflows` pour configurer le flux de travail dans GitHub.

**Créer des modèles de flux de travail à l’aide de l’interface CLI TeamsFx**

1. Entrez `cd` le répertoire de votre projet d’application Teams.
2. Entrez `teamsfx add cicd` la commande pour démarrer le processus de commande interactif.
3. Sélectionnez un environnement dans l’invite de commandes.
4. Sélectionnez **GitHub** comme fournisseur CI/CD.
5. Sélectionnez au moins un modèle parmi ces options : CI, CD, Provision ou Publier sur Teams.
7. Ouvrez le modèle et personnalisez les flux de travail qui s’intègrent dans vos scénarios.
8. Suivez les fichiers README sous `.github/workflows` pour configurer le flux de travail dans GitHub.

> [!NOTE]
> Si vous devez ajouter des modèles de flux de travail supplémentaires, vous pouvez suivre la même procédure pour créer un modèle de flux de travail dans Visual Studio Code ou l’interface CLI TeamsFx.

### <a name="customize-cicd-workflow"></a>Personnaliser le flux de travail CI/CD

Vous pouvez modifier ou supprimer les scripts de test pour personnaliser le flux de travail CI/CD :

1. Par défaut, le flux de travail cd est déclenché lorsque de nouvelles validations sont effectuées dans la `main` branche.
1. Modifiez les scripts de build si nécessaire.
1. Supprimez les scripts de test selon les besoins.

### <a name="set-up-pipelines-with-azure-devops"></a>Configurer des pipelines avec Azure DevOps

Pour configurer des pipelines avec Azure DevOps pour CI/CD :

1. Créez des modèles de flux de travail.

   * Visual Studio Code
   * TeamsFx CLI

1. Personnalisez le flux de travail CI/CD.


## <a name="create-workflow-templates-with-azure-devops"></a>Créer des modèles de flux de travail avec Azure DevOps

**Créer des modèles de flux de travail à l’aide de la Teams Shared Computer Toolkit dans Visual Studio Code**

1. Créez un projet d’application Teams à l’aide de Teams Shared Computer Toolkit.
2. Sélectionnez **Teams Shared Computer Toolkit** icône dans la barre d’activité Visual Studio Code.
3. Sélectionnez **Ajouter des flux de travail CI/CD**.
4. Sélectionnez un environnement dans l’invite de commandes.
5. Sélectionnez **Azure DevOps** en tant que fournisseur CI/CD.
6. Sélectionnez au moins un modèle parmi ces options : CI, CD, Provision et Publish to Teams.
7. Ouvrez le modèle et personnalisez les flux de travail qui s’intègrent dans vos scénarios.
8. Suivez les fichiers README sous `.azure/pipelines` pour configurer le flux de travail dans Azure DevOps.

**Créer des modèles de flux de travail à l’aide de l’interface CLI TeamsFx**

1. Entrez `cd` le répertoire de votre projet d’application Teams.
2. Entrez `teamsfx add cicd` la commande pour démarrer le processus de commande interactif.
3. Sélectionnez un environnement dans l’invite de commandes.
4. Sélectionnez **Azure DevOps** en tant que fournisseur CI/CD.
5. Sélectionnez au moins un modèle parmi ces options : CI, CD, Provision ou Publier sur Teams.
7. Ouvrez le modèle et personnalisez les flux de travail qui s’intègrent dans vos scénarios.
8. Suivez les fichiers README sous `.azure/pipelines` pour configurer le flux de travail dans Azure DevOps.

> [!NOTE]
> Si vous devez ajouter des modèles de flux de travail supplémentaires, vous pouvez suivre la même procédure pour créer un modèle de flux de travail dans Visual Studio Code ou l’interface CLI TeamsFx.

### <a name="customize-ci-workflow"></a>Personnaliser le flux de travail CI

Voici les modifications que vous pouvez apporter à la définition de script ou de flux de travail :

1. Utilisez le script de build npm ou personnalisez la façon dont vous générez dans le code Automation.
1. Utilisez le script de test npm qui retourne zéro pour la réussite et modifiez les commandes de test.

### <a name="customize-cd-workflow"></a>Personnaliser le flux de travail cd

Voici les modifications que vous pouvez apporter à la définition de script ou de flux de travail :

1. Vérifiez que vous disposez d’un script de build npm ou personnalisez la façon dont vous générez dans le code Automation.
1. Vérifiez que vous disposez d’un script de test npm qui retourne zéro en cas de réussite ou modifiez les commandes de test.

### <a name="set-up-pipelines-with-jenkins"></a>Configurer des pipelines avec Jenkins

Pour configurer des pipelines avec Jenkins pour CI/CD :

1. Créez des modèles de flux de travail.

   * Visual Studio Code
   * TeamsFx CLI

1. Personnalisez le flux de travail CI/CD.

## <a name="create-workflow-templates-with-jenkins"></a>Créer des modèles de flux de travail avec Jenkins

**Créer des modèles de flux de travail à l’aide de la Teams Shared Computer Toolkit dans Visual Studio Code**

1. Créez un projet d’application Teams à l’aide de Teams Shared Computer Toolkit.
2. Sélectionnez **Teams Shared Computer Toolkit** icône dans la barre latérale Visual Studio Code.
3. Sélectionnez **Ajouter des flux de travail CI/CD**.
4. Sélectionnez un environnement dans l’invite de commandes.
5. Sélectionnez **Jenkins** comme fournisseur CI/CD.
6. Sélectionnez au moins un modèle parmi ces options : CI, CD, Provision ou Publier sur Teams.
7. Ouvrez le modèle et personnalisez les flux de travail qui s’intègrent dans vos scénarios.
8. Suivez les fichiers README sous `.jenkins/pipelines` pour configurer le flux de travail avec Jenkins.

**Créer des modèles de flux de travail à l’aide de l’interface CLI TeamsFx**

1. Entrez `cd` le répertoire de votre projet d’application Teams.
2. Entrez `teamsfx add cicd` la commande pour démarrer le processus de commande interactif.
3. Sélectionnez un environnement dans l’invite de commandes.
4. Sélectionnez **Jenkins** comme fournisseur CI/CD.
5. Sélectionnez au moins un modèle parmi ces options : CI, CD, Provision ou Publier sur Teams.
7. Ouvrez le modèle et personnalisez les flux de travail qui s’intègrent dans vos scénarios.
8. Suivez les fichiers README sous `.jenkins/pipelines` pour configurer le flux de travail avec Jenkins.

> [!NOTE]
> Si vous devez ajouter des modèles de flux de travail supplémentaires, vous pouvez suivre la même procédure pour créer un modèle de flux de travail dans Visual Studio Code ou l’interface CLI TeamsFx.

### <a name="customize-ci-workflow"></a>Personnaliser le flux de travail CI

Voici quelques-unes des modifications que vous pouvez apporter à votre projet :

1. Modifiez le mode de déclenchement du flux CI. La valeur par défaut est d’utiliser les déclencheurs de **pollSCM** lorsqu’une nouvelle modification est envoyée dans la branche **de développement** .
1. Vérifiez que vous disposez d’un script de build npm ou personnalisez la façon dont vous générez dans le code Automation.
1. Vérifiez que vous disposez d’un script de test npm qui retourne zéro en cas de réussite ou modifiez les commandes de test.


### <a name="customize-cd-workflow"></a>Personnaliser le flux de travail cd

Effectuez les étapes suivantes pour personnaliser le pipeline CD :

1. Modifiez le flux de CD. La valeur par défaut consiste à utiliser les déclencheurs lorsqu’une `pollSCM` nouvelle modification est envoyée (push) dans la `main` branche.
1. Si nécessaire, modifiez les scripts de génération.
1. Supprimez les scripts de test si vous n’avez pas de tests.


### <a name="set-up-pipelines-for-other-platforms"></a>Configurer des pipelines pour d’autres plateformes

Vous pouvez suivre les exemples de scripts Bash répertoriés prédéfinis pour générer et personnaliser des pipelines CI/CD sur les autres plateformes :

* [CI Scripts](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh)
* [CD Scripts](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)

Les scripts sont basés sur un outil en ligne de commande TeamsFx multiplateforme [TeamsFx-CLI](https://www.npmjs.com/package/@microsoft/teamsfx-cli). Vous pouvez l’installer avec `npm install -g @microsoft/teamsfx-cli` et suivre la [documentation](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) pour personnaliser les scripts.

> [!NOTE]
>
> * Pour activer `@microsoft/teamsfx-cli` l’exécution en mode CI, activez .`CI_ENABLED` `export CI_ENABLED=true` En mode CI, `@microsoft/teamsfx-cli` il est convivial pour CI/CD.
> * Pour activer `@microsoft/teamsfx-cli` l’exécution en mode non interactif, définissez une configuration globale avec la commande : `teamsfx config set -g interactive false`. En mode non interactif, `@microsoft/teamsfx-cli` ne demande pas d’entrées.

Veillez à configurer Azure et Microsoft 365 les informations d’identification dans vos variables d’environnement en toute sécurité. Par exemple, si vous utilisez GitHub comme référentiel de code source, consultez [Secrets Github](https://docs.github.com/en/actions/reference/encrypted-secrets).


## <a name="provision-and-deploy-resources"></a>Provisionner et déployer des ressources

Pour provisionner et déployer des ressources ciblant Azure dans CI/CD, vous devez créer un principal de service Azure à utiliser.

Effectuez les étapes suivantes pour créer des principaux de service Azure :

1. Inscrivez une application Microsoft Azure Active Directory (Azure AD) dans un seul locataire.
2. Attribuez un rôle à votre application Azure AD pour accéder à votre abonnement Azure. Le `Contributor` rôle est recommandé.
3. Créez un secret d’application Azure AD.

> [!TIP]
> Enregistrez votre ID de locataire, l’ID d’application (AZURE_SERVICE_PRINCIPAL_NAME) et le secret (AZURE_SERVICE_PRINCIPAL_PASSWORD) pour une utilisation ultérieure.

Pour plus d’informations, consultez [les instructions relatives aux principaux de service Azure](/azure/active-directory/develop/howto-create-service-principal-portal). Voici les trois façons de créer des principaux de service :

* [portail Microsoft Azure](/azure/active-directory/develop/howto-create-service-principal-portal)
* [Windows PowerShell](/azure/active-directory/develop/howto-authenticate-service-principal-powershell)
* [Microsoft Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli)

## <a name="publish-teams-app-using-teams-developer-portal"></a>Publier Teams application à l’aide du portail des développeurs Teams

Si des modifications sont apportées au fichier manifeste de Teams application, vous pouvez mettre à jour le manifeste et publier à nouveau l’application Teams.

Pour publier manuellement Teams application, vous pouvez tirer parti [du portail des développeurs pour Teams](https://dev.teams.microsoft.com/home).

Effectuez les étapes suivantes pour publier votre application :

1. Connectez-vous au [portail des développeurs pour Teams](https://dev.teams.microsoft.com) à l’aide du compte correspondant.
2. Importez votre package d’application dans zip en sélectionnant `App -> Import app -> Replace`.
3. Sélectionnez l’application cible dans la liste des applications.
4. Publiez votre application en sélectionnant `Publish -> Publish to your org`.

### <a name="see-also"></a>Voir aussi

* [Démarrage rapide pour GitHub Actions](https://docs.github.com/en/actions/quickstart#creating-your-first-workflow)
* [Créer votre premier pipeline Azure DevOps](/azure/devops/pipelines/create-first-pipeline)
* [Créer votre premier pipeline Jenkins](https://www.jenkins.io/doc/pipeline/tour/hello-world/)
* [Gérer vos applications avec le Portail des développeurs pour Microsoft Teams](/concepts/build-and-test/teams-developer-portal)
