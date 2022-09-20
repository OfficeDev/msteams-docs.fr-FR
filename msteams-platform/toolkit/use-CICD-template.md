---
title: Modèles CI/CD
author: MuyangAmigo
description: Dans ce module, découvrez comment utiliser des modèles de pipeline CI/CD dans GitHub, Azure DevOps et Jenkins pour les modèles Développeurs d’applications Teams/CD
ms.author: ruhe
ms.localizationpriority: medium
ms.topic: overview
ms.date: 04/20/2022
ms.openlocfilehash: 05f797afcf54cab2d23ee24aae2c4985f3d724f2
ms.sourcegitcommit: dccb48902e08484692ab927415bcd3d61dc50db2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/19/2022
ms.locfileid: "67806871"
---
# <a name="set-up-cicd-pipelines"></a>Mettre en place des pipelines CI/CD

TeamsFx permet d’automatiser votre flux de travail de développement lors de la création d’une application Teams. Voici les outils et modèles que vous pouvez utiliser pour configurer des pipelines CI/CD, créer des modèles de flux de travail et personnaliser le flux de travail CI/CD avec GitHub, Azure DevOps, Jenkins et d’autres plateformes. Pour provisionner et déployer des ressources, vous pouvez créer des principaux de service Azure et publier l’application Teams à l’aide de Teams Developer Portal. Pour publier manuellement l’application Teams, vous pouvez tirer profit du [Portail des développeurs pour Teams](https://dev.teams.microsoft.com/home).

|Outils et modèles | Description |
|---|---|
|[TeamsFx-CLI-Action](https://github.com/OfficeDev/teamsfx-cli-action)|Action GitHub qui s’intègre à l’interface CLI TeamsFx.|
|[Teams Toolkit dans Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)| Extension Visual Studio Code qui vous aide à développer une application Teams et des flux de travail d’automatisation pour GitHub, Azure DevOps et Jenkins. |
|[TeamsFx CLI](https://www.npmjs.com/package/@microsoft/teamsfx-cli) | Outil en ligne de commande qui vous aide à développer une application Teams et des flux de travail d’automatisation pour GitHub, Azure DevOps et Jenkins.|
|[script-ci-template.sh](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh) and [script-cd-template.sh](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)| Modèles de script pour l’automatisation en dehors de GitHub, Azure DevOps ou Jenkins. |

## <a name="set-up-pipelines"></a>Configurer des pipelines

Vous pouvez configurer des pipelines avec les plateformes suivantes :

1. [Définissez les pipelines avec GitHub](#set-up-pipelines-with-github)
1. [Définissez les pipelines avec Azure DevOps](#set-up-pipelines-with-azure-devops)
1. [Définissez les pipelines avec Jenkins](#set-up-pipelines-with-jenkins)
1. [Définissez les pipelines pour les autres plateformes](#set-up-pipelines-for-other-platforms)

## <a name="set-up-pipelines-with-github"></a>Configurer des pipelines avec GitHub

Pour configurer des pipelines avec GitHub pour CI/CD :

* Créez des modèles de flux de travail.

  * Visual Studio Code
  * TeamsFx CLI

* Personnalisez le flux de travail CI/CD.

### <a name="create-workflow-templates"></a>Créer des modèles de flux de travail

Vous pouvez créer les modèles de flux de travail suivants avec GitHub :

**Teams Toolkit dans Visual Studio Code**

1. Créez un projet d’application Teams à l’aide du Kit de ressources Teams.

1. Sélectionnez l’icône :::image type="icon" source="../assets/images/teams-toolkit-v2/add-API/api-add-icon.png"::: du **Kit de ressources Teams** dans le volet gauche.

1. Sélectionner **Ajouter des fonctionnalités**

   :::image type="content" source="../assets/images/teams-toolkit-v2/add-feature.png" alt-text="Ajout d’une fonctionnalité":::

1. Sélectionnez **Add CI/CD Workflows**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/toolkit-ci-cd-workflow.png" alt-text="Sélectionner le flux de travail CI/CD":::

1. Sélectionnez un environnement à partir de l’invite de commandes.
1. Sélectionnez **GitHub** comme fournisseur CI/CD.
1. Sélectionnez au moins un modèle parmi ces options : CI, CD, Provisionner ou Publier dans Teams.
1. Ouvrez le modèle et personnalisez les flux de travail qui s’intègrent à vos scénarios.
1. Suivez les fichiers README sous `.github/workflows` pour configurer le workflow dans GitHub.

**TeamsFx CLI**

1. Entrez `cd` dans le répertoire de votre projet d’application Teams.
2. Entrez `teamsfx add cicd` commande pour démarrer le processus de commande interactif.
3. Sélectionnez un environnement à partir de l’invite de commandes.
4. Sélectionnez **GitHub** comme fournisseur CI/CD.
5. Sélectionnez au moins un modèle parmi ces options : CI, CD, Provisionner ou Publier dans Teams.
7. Ouvrez le modèle et personnalisez les flux de travail qui s’intègrent à vos scénarios.
8. Suivez les fichiers README sous `.github/workflows` pour configurer le workflow dans GitHub.

> [!NOTE]
> Si vous devez ajouter des modèles de flux de travail supplémentaires, vous pouvez suivre la même procédure pour créer un modèle de flux de travail dans Visual Studio Code ou TeamsFx CLI.

### <a name="customize-cicd-workflow"></a>Personnaliser le flux de travail CI/CD

Vous pouvez modifier ou supprimer les scripts de test pour personnaliser le flux de travail CI/CD :

1. Par défaut, le flux de travail cd est déclenché lorsque de nouvelles validations sont apportées à la branche `main`.
1. Modifiez les scripts de build si nécessaire.
1. Supprimez les scripts de test si nécessaire.

## <a name="set-up-pipelines-with-azure-devops"></a>Configurer des pipelines avec Azure DevOps

Pour configurer des pipelines avec Azure DevOps pour CI/CD :

* Créez des modèles de flux de travail.

  * Visual Studio Code
  * TeamsFx CLI

* Personnalisez le flux de travail CI/CD.

### <a name="create-workflow-templates"></a>Créer des modèles de flux de travail

Vous pouvez créer les modèles de flux de travail suivants avec Azure DevOps :

**Teams Toolkit dans Visual Studio Code**

1. Créez un projet d’application Teams à l’aide du Kit de ressources Teams.
2. Sélectionnez l’icône :::image type="icon" source="../assets/images/teams-toolkit-v2/add-API/api-add-icon.png"::: du **Kit de ressources Teams** dans le volet gauche.
1. Sélectionnez **Add CI/CD Workflows**.
1. Sélectionnez un environnement à partir de l’invite de commandes.
1. Sélectionnez **Azure DevOps** en tant que fournisseur CI/CD.
1. Sélectionnez au moins un modèle parmi ces options : CI, CD, Provisionner et Publier dans Teams.
1. Ouvrez le modèle et personnalisez les flux de travail qui s’intègrent à vos scénarios.
1. Suivez les fichiers README sous `.azure/pipelines` pour configurer le workflow dans Azure DevOps.

**TeamsFx CLI**

1. Entrez `cd` dans le répertoire de votre projet d’application Teams.
2. Entrez `teamsfx add cicd` commande pour démarrer le processus de commande interactif.
3. Sélectionnez un environnement à partir de l’invite de commandes.
4. Sélectionnez **Azure DevOps** en tant que fournisseur CI/CD.
5. Sélectionnez au moins un modèle parmi ces options : CI, CD, Provisionner ou Publier dans Teams.
7. Ouvrez le modèle et personnalisez les flux de travail qui s’intègrent à vos scénarios.
8. Suivez les fichiers README sous `.azure/pipelines` pour configurer le workflow dans Azure DevOps.

> [!NOTE]
> Si vous devez ajouter des modèles de flux de travail supplémentaires, vous pouvez suivre la même procédure pour créer un modèle de flux de travail dans Visual Studio Code ou TeamsFx CLI.

### <a name="customize-ci-workflow"></a>Personnaliser le flux de travail CI

Vous pouvez apporter les modifications suivantes pour le script ou la définition de workflow :

1. Utilisez le script de build npm ou personnalisez la façon dont vous générez dans le code Automation.
1. Utilisez le script de test npm qui retourne zéro pour la réussite et modifiez les commandes de test.

### <a name="customize-cd-workflow"></a>Personnaliser le flux de travail cd

Vous pouvez apporter les modifications suivantes pour le script ou la définition de workflow :

1. Vérifiez que vous disposez d’un script de build npm ou personnalisez la façon dont vous générez dans le code d’automatisation.
1. Vérifiez que vous disposez d’un script de test npm qui retourne zéro en cas de réussite ou modifiez les commandes de test.

## <a name="set-up-pipelines-with-jenkins"></a>Configurer des pipelines avec Jenkins

Pour configurer des pipelines avec Jenkins pour CI/CD :

* Créez des modèles de flux de travail.

  * Visual Studio Code
  * TeamsFx CLI

* Personnalisez le flux de travail CI/CD.

### <a name="create-workflow-templates"></a>Créer des modèles de flux de travail

Vous pouvez créer les modèles de flux de travail suivants avec Jenkins :

**Teams Toolkit dans Visual Studio Code**

1. Créez un projet d’application Teams à l’aide du Kit de ressources Teams.
2. Sélectionnez l’icône :::image type="icon" source="../assets/images/teams-toolkit-v2/add-API/api-add-icon.png"::: du **Kit de ressources Teams** dans le volet gauche.
3. Sélectionnez **Add CI/CD Workflows**.
4. Sélectionnez un environnement à partir de l’invite de commandes.
5. Sélectionnez **Jenkins** en tant que fournisseur CI/CD.
6. Sélectionnez au moins un modèle parmi ces options : CI, CD, Provisionner ou Publier dans Teams.
7. Ouvrez le modèle et personnalisez les flux de travail qui s’intègrent à vos scénarios.
8. Suivez les fichiers README sous `.jenkins/pipelines` pour configurer le workflow avec Jenkins.

**TeamsFx CLI**

1. Entrez `cd` dans le répertoire de votre projet d’application Teams.
2. Entrez `teamsfx add cicd` commande pour démarrer le processus de commande interactif.
3. Sélectionnez un environnement à partir de l’invite de commandes.
4. Sélectionnez **Jenkins** en tant que fournisseur CI/CD.
5. Sélectionnez au moins un modèle parmi ces options : CI, CD, Provisionner ou Publier dans Teams.
7. Ouvrez le modèle et personnalisez les flux de travail qui s’intègrent à vos scénarios.
8. Suivez les fichiers README sous `.jenkins/pipelines` pour configurer le workflow avec Jenkins.

> [!NOTE]
> Si vous devez ajouter des modèles de flux de travail supplémentaires, vous pouvez suivre la même procédure pour créer un modèle de flux de travail dans Visual Studio Code ou TeamsFx CLI.

### <a name="customize-ci-workflow"></a>Personnaliser le flux de travail CI

Vous pouvez apporter les modifications suivantes à votre projet :

1. Modifiez la façon dont le flux CI est déclenché. La valeur par défaut consiste à utiliser les déclencheurs de **pollSCM** lorsqu’une nouvelle modification est envoyée dans la branche **dev**.
1. Vérifiez que vous disposez d’un script de build npm ou personnalisez la façon dont vous générez dans le code d’automatisation.
1. Vérifiez que vous disposez d’un script de test npm qui retourne zéro en cas de réussite ou modifiez les commandes de test.

### <a name="customize-cd-workflow"></a>Personnaliser le flux de travail cd

Effectuez les étapes suivantes pour personnaliser le pipeline CD :

1. Modifiez le flux CD. La valeur par défaut consiste à utiliser les déclencheurs de `pollSCM` lorsqu’une nouvelle modification est envoyée dans la branche `main`.
1. Modifiez les scripts de build si nécessaire.
1. Supprimez les scripts de test si vous n’avez pas de tests.

## <a name="set-up-pipelines-for-other-platforms"></a>Configurer des pipelines pour d’autres plateformes

Vous pouvez suivre les exemples de scripts bash répertoriés prédéfinis pour générer et personnaliser des pipelines CI/CD sur les autres plateformes :

* [Scripts CI](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh)
* [Scripts CD](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)

Les scripts sont basés sur un outil de ligne de commande TeamsFx multiplateforme, [TeamsFx-CLI.](https://www.npmjs.com/package/@microsoft/teamsfx-cli) Vous pouvez l'installer avec `npm install -g @microsoft/teamsfx-cli` et suivre la [documentation](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md)  pour personnaliser les scripts.

> [!NOTE]
>
> * Pour activer `@microsoft/teamsfx-cli` s’exécutant en mode CI, activez `CI_ENABLED` en `export CI_ENABLED=true`. En mode CI, `@microsoft/teamsfx-cli` est convivial pour CI/CD.
> * Pour activer `@microsoft/teamsfx-cli` s’exécutant en mode non interactif, définissez une configuration globale avec la commande : `teamsfx config set -g interactive false`. En mode non interactif, `@microsoft/teamsfx-cli` n’invite pas les entrées.

Veillez à configurer azure et Microsoft 365 les informations d’identification dans vos variables d’environnement en toute sécurité. Par exemple, si vous utilisez GitHub comme référentiel de code source, consultez [GitHub Secrets](https://docs.github.com/en/actions/reference/encrypted-secrets).

## <a name="provision-and-deploy-resources"></a>Provisionner et déployer des ressources

Pour provisionner et déployer des ressources ciblant Azure dans CI/CD, vous devez créer un principal de service Azure à utiliser.

Procédez comme suit pour créer des principaux de service Azure :

1. Inscrivez une application Microsoft Azure Active Directory (Azure AD) dans un seul locataire.
2. Attribuez un rôle à votre application Azure AD pour accéder à votre abonnement Azure. Le rôle `Contributor` est conseillé.
3. Créez un secret d’application Azure AD.

> [!TIP]
> Enregistrez votre ID de locataire, l’ID d’application (AZURE_SERVICE_PRINCIPAL_NAME) et le secret (AZURE_SERVICE_PRINCIPAL_PASSWORD) pour une utilisation ultérieure.

Pour plus d’informations, consultez [Instructions relatives aux principaux de service Azure](/azure/active-directory/develop/howto-create-service-principal-portal). Les trois méthodes suivantes permettent de créer des principaux de service :

* [Portail Microsoft Azure](/azure/active-directory/develop/howto-create-service-principal-portal)
* [Windows PowerShell](/azure/active-directory/develop/howto-authenticate-service-principal-powershell)
* [Microsoft Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli)

## <a name="publish-teams-app-using-teams-developer-portal"></a>Publier une application Teams à l’aide de Teams Developer Portal

Si des modifications sont apportées au fichier manifeste de l’application Teams, vous pouvez mettre à jour le manifeste et publier à nouveau l’application Teams. Pour publier manuellement l’application Teams, vous pouvez tirer profit du [Portail des développeurs pour Teams](https://dev.teams.microsoft.com/home).

Procédez comme suit pour publier votre application :

1. Connectez-vous au [portail des développeurs pour Teams](https://dev.teams.microsoft.com) à l’aide du compte correspondant.
2. Importez votre package d’application dans zip, sélectionnez `App -> Import app -> Replace`.
3. Sélectionnez l’application cible dans la liste des applications.
4. Publiez votre application, sélectionnez `Publish -> Publish to your org`.

## <a name="see-also"></a>Voir aussi

* [Démarrage rapide pour GitHub Actions](https://docs.github.com/en/actions/quickstart#creating-your-first-workflow)
* [Créez votre premier pipeline Azure DevOps](/azure/devops/pipelines/create-first-pipeline)
* [Créez votre premier pipeline Jenkins](https://www.jenkins.io/doc/pipeline/tour/hello-world/)
* [Gérer vos applications avec le Portail des développeurs pour Microsoft Teams](../concepts/build-and-test/teams-developer-portal.md)
