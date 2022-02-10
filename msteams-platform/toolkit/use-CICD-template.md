---
title: Prise en charge ci ou CD pour Teams développeurs d’applications
author: MuyangAmigo
description: Modèles TORS
ms.author: ruhe
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: f8de6dd66b281f8cf842e5439d3a217598f46047
ms.sourcegitcommit: 90587b1ec04bf20d716ed6feb8ccca4313e87f8c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/10/2022
ms.locfileid: "62518113"
---
# <a name="cicd-guide"></a>Guide CI/CD

TeamsFx permet d’automatiser votre flux de travail de développement tout en Teams application. Le document fournit des outils et des modèles pour vous aider à commencer à définir des pipelines CI ou CD avec GitHub, Azure Devops et Jenkins.

|Outils et modèles|Description| 
|---|---|
|[teamsfx-cli-action](https://github.com/OfficeDev/teamsfx-cli-action)|GitHub action qui s’intègre à l’CLI TeamsFx.|
|[github-ci-template.yml](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/github-ci-template.yml) et [github-cd-template.yml](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/github-cd-template.yml)| GitHub modèles CI ou CD pour Teams application. |
|[jenkins-ci-template. Jenkinsfile](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/jenkins-ci-template.Jenkinsfile) et [jenkins-cd-template. Jenkinsfile](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/jenkins-cd-template.Jenkinsfile)|Modèles CI ou CD Jenkins pour une Teams application.|
|[script-ci-template.sh](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh) et [script-cd-template.sh](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)| Modèles de script pour l’automatisation en dehors GitHub. |

## <a name="ci-or-cd-workflow-templates-in-github"></a>Modèles de flux de travail CI ou CD dans GitHub

**Pour inclure des flux de travail CI ou CD pour automatiser Teams processus de développement d’applications dans GitHub** :

1. Créer un dossier sous `.github/workflows`
1. Copiez l’un des fichiers de modèle suivants :
    * [github-ci-template.yml pour le](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/github-ci-template.yml) flux de travail CI.
    * [github-cd-template.yml pour le](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/github-cd-template.yml) flux de travail CD.
1. Personnalisez les flux de travail qui correspondent à vos scénarios.

### <a name="customize-ci-workflow"></a>Personnaliser le flux de travail CI

Pour adapter le flux de travail à votre projet, effectuez les étapes suivantes :

1. Modifier le flux CI. 
1. Utilisez le script de build npm ou personnalisez la façon dont vous créez le projet dans le code d’automatisation.
1. Utilisez un script de test npm qui renvoie zéro pour la réussite et modifiez les commandes de test.

### <a name="customize-cd-workflow"></a>Personnaliser le flux de travail CD

Effectuez les étapes suivantes pour personnaliser le flux de travail CD :

1. Par défaut, le flux de travail CD est déclenché lorsque de nouvelles validations sont réalisées dans la `main` branche.
1. Créez GitHub [de référentiel](https://docs.github.com/en/actions/reference/encrypted-secrets) par environnement pour contenir les informations d’identification de connexion au principal de service Azure et Microsoft 365 compte. Pour plus d’informations, [voir GitHub Actions](https://github.com/OfficeDev/teamsfx-cli-action/blob/main/README.md).
1. Modifiez les scripts de build si nécessaire.
1. Supprimez les scripts de test selon les besoins.

> [!NOTE]
> L’étape de mise en service n’est pas incluse dans le modèle CD, car elle n’est généralement exécutée qu’une seule fois. Vous pouvez exécuter une mise en service au sein Teams Shared Computer Toolkit, l’CLI TeamsFx ou à l’aide d’un flux de travail distinct. Veillez à valider après l’approvisionnement. Les résultats de l’approvisionnement sont déposés dans le `.fx` dossier.

### <a name="github-secrets"></a>Secrets Github

Le tableau suivant répertorie toutes les clés secrètes dont vous avez besoin pour créer un environnement GitHub :

1. Sélectionnez **Paramètres**.
1. Go to **Environments** section.
1. **Sélectionnez Nouvel environnement**.
1. Entrez un nom pour votre environnement. Le nom d’environnement par défaut fourni dans le modèle est `test_environment`. 
1. **Sélectionnez Configurer l’environnement**.
1. **Sélectionnez Ajouter une secret**.

Le tableau suivant répertorie toutes les clés secrètes requises pour créer un environnement :

|Nom|Description|
|---|---|
|`AZURE_SERVICE_PRINCIPAL_NAME`|Nom principal de service d’Azure utilisé pour mettre en service des ressources.|
|`AZURE_SERVICE_PRINCIPAL_PASSWORD`|Mot de passe du principal de service Azure.|
|`AZURE_SUBSCRIPTION_ID`|Pour identifier l’abonnement dans lequel les ressources seront mise en service.|
|`AZURE_TENANT_ID`|Pour identifier le client dans lequel réside l’abonnement.|
|`M365_ACCOUNT_NAME`|Le Microsoft 365 pour créer et publier Teams application.|
|`M365_ACCOUNT_PASSWORD`|Mot de passe du compte Microsoft 365 client.|
|`M365_TENANT_ID`|Pour identifier le client dans lequel l’application Teams sera créée/publiée. Cette valeur est facultative, sauf si vous avez un compte multi-locataire et que vous souhaitez utiliser un autre client. Pour plus d’informations, [voir comment trouver votre ID Microsoft 365 client.](/azure/active-directory/fundamentals/active-directory-how-to-find-tenant)|

> [!NOTE]
> Actuellement, le principal de service pour Azure est utilisé dans les flux de travail CI/CD. Pour plus d’informations, voir [créer des principes de service Azure](#create-azure-service-principals).

## <a name="set-up-ci-or-cd-pipelines-with-azure-devops"></a>Configurer des pipelines CI ou CD avec Azure DevOps

Vous pouvez configurer des pipelines automatisés dans Azure DevOps et créer une référence sur les scripts.

Pour commencer, effectuez les étapes suivantes :

* [CI Scripts](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh)
* [CD Scripts](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)

### <a name="set-up-ci-pipeline"></a>Configurer le pipeline CI

1. [Ajoutez des scripts CI](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh) à votre référentiel Azure DevOps, et faites les personnalisations nécessaires, comme vous pouvez en déduire à partir des commentaires dans le fichier de script.
1. Suivez les [étapes pour créer votre pipeline Azure DevOps pour CI](/azure/devops/pipelines/create-first-pipeline).
Voici un scénario de scripts de pipeline CI courants :

```yml
trigger:
- dev 

pool:
  vmImage: ubuntu-latest

steps:
- task: NodeTool@0
  inputs:
    versionSpec: '14.17.0'
    checkLatest: true
  
- task: Bash@3
  inputs:
    filePath: './others-script-ci-template.sh'
```

Voici les modifications que vous pouvez apporter au script ou à la définition de flux de travail :

1. Modifier le flux CI. Par défaut, une nouvelle validation est poussée dans la `dev` branche.
1. Modifier la façon d’installer les nœuds et npm.
1. Utilisez le script de build npm ou personnalisez la façon dont vous créez le code d’automatisation.
1. Utilisez un script de test npm qui renvoie zéro pour la réussite et modifiez les commandes de test.

### <a name="set-up-cd-pipeline"></a>Configurer le pipeline CD

1. [Ajoutez des scripts](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh) CD dans votre référentiel Azure DevOps et faites les personnalisations nécessaires, comme vous pouvez en déduire à partir des commentaires dans le fichier de script.
1. Créez votre pipeline Azure DevOps pour CD-CSV. Pour plus d’informations, voir [créer le premier pipeline](/azure/devops/pipelines/create-first-pipeline). La définition du pipeline peut être référente à l’exemple de définition suivant pour le pipeline CI.
1. Ajoutez les variables nécessaires [par Définir des variables](/azure/devops/pipelines/process/variables) et faites-les secrètes si nécessaire.

```yml
trigger:
- main 

pool:
  vmImage: ubuntu-latest

steps:
- task: NodeTool@0
  inputs:
    versionSpec: '14.17.0'
    checkLatest: true
  
- task: Bash@3
  env:
    SP_NAME: $(AZURE_SERVICE_PRINCIPAL_NAME)
    SP_PASSWORD: $(AZURE_SERVICE_PRINCIPAL_PASSWORD)
    TENANT_ID: $(AZURE_TENANT_ID)
    AZURE_SUBSCRIPTION_ID: $(AZURE_SUBSCRIPTION_ID)
    M365_ACCOUNT_NAME: $(M365_ACCOUNT_NAME)
    M365_ACCOUNT_PASSWORD: $(M365_ACCOUNT_PASSWORD)
  inputs:
    filePath: './others-script-cd-template.sh'
```

Voici les modifications que vous pouvez apporter au script ou à la définition de flux de travail :

1. La façon dont le flux cd est déclenché. Par défaut, cela se produit lorsque de nouvelles validations sont réalisées sur **la branche** principale.
1. Modifier la façon d’installer les nœuds et npm.
1. Modifiez le nom de l’environnement, par défaut sa **zone de transit**.
1. Assurez-vous que vous avez un script de build npm ou personnalisez la façon dont vous créez le code d’automatisation.
1. Assurez-vous que vous avez un script de test npm qui renvoie zéro pour la réussite et/ou modifiez les commandes de test.

### <a name="pipeline-variables-for-azure-devops"></a>Variables de pipeline pour Azure DevOps

Effectuez les étapes suivantes pour créer des variables de pipeline dans Azure DevOps :

1. Dans la page Modification du pipeline, sélectionnez **Variables** et **sélectionnez Nouvelle variable**.
1. Entrez la paire Nom ou Valeur pour votre variable.
1. Basculez la case à cocher **conserver cette valeur secrète** si nécessaire.
1. **Sélectionnez OK** pour créer la variable.

|Nom|Description|
|---|---|
|`AZURE_SERVICE_PRINCIPAL_NAME`|Nom principal de service d’Azure utilisé pour mettre en service des ressources.|
|`AZURE_SERVICE_PRINCIPAL_PASSWORD`|Mot de passe du principal de service Azure.|
|`AZURE_SUBSCRIPTION_ID`|Pour identifier l’abonnement dans lequel les ressources seront mise en service.|
|`AZURE_TENANT_ID`|Pour identifier le client dans lequel réside l’abonnement.|
|`M365_ACCOUNT_NAME`|Le Microsoft 365 pour la création et la publication de l’Teams app.|
|`M365_ACCOUNT_PASSWORD`|Mot de passe du compte Microsoft 365 client.|
|`M365_TENANT_ID`|Pour identifier le client dans lequel l’application Teams sera créée/publiée. Cette valeur est facultative, sauf si vous avez un compte multi-locataire et que vous souhaitez utiliser un autre client. En savoir plus [sur la façon de trouver votre ID Microsoft 365 client.](/azure/active-directory/fundamentals/active-directory-how-to-find-tenant)|

## <a name="ci-or-cd-pipeline-templates-in-jenkins"></a>Modèles de pipeline CI ou CD dans Jenkins

Pour ajouter ces modèles à votre référentiel, vous devez utiliser les versions [de jenkins-ci-template. Jenkinsfile](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/jenkins-ci-template.Jenkinsfile) et  [jenkins-cd-template. Le fichier Jenkinsfile](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/jenkins-cd-template.Jenkinsfile) doit se trouver dans votre référentiel par branche.

En outre, vous devez créer des pipelines CI ou CD dans Jenkins qui pointent vers le **fichier Jenkinsfile** spécifique correspondant.

Suivez les étapes pour vérifier comment connecter Jenkins avec différentes plateformes SCM :

1. [Jenkins avec GitHub](https://www.jenkins.io/solutions/github/)
2. [Jenkins avec Azure DevOps](https://www.dragonspears.com/blog/ci-cd-with-jenkins-and-azure-devops-services)
3. [Jenkins avec GitLab](https://docs.gitlab.com/ee/integration/jenkins.html)
4. [Jenkins avec Bitbucket](https://medium.com/ampersand-academy/integrate-bitbucket-jenkins-c6e51103d0fe)

### <a name="customize-ci-pipeline"></a>Personnaliser le pipeline CI

Voici quelques-unes des modifications que vous pouvez apporter pour adapter votre projet :

1. Renommons le fichier modèle **en Jenkinsfile** et placez-le sous la branche cible, par exemple, **la branche dev** .
1. Modifier la façon dont le flux CI est déclenché. Par défaut, nous utilisons les déclencheurs de **pollSCM** lorsqu’une nouvelle modification est poussée dans **la branche dev** .
1. Assurez-vous que vous avez un script de build npm ou personnalisez la façon dont vous créez le code d’automatisation.
1. Assurez-vous que vous avez un script de test npm qui renvoie zéro pour la réussite et/ou modifiez les commandes de test.

### <a name="customize-cd-pipeline"></a>Personnaliser le pipeline CD

Effectuez les étapes suivantes pour personnaliser le pipeline CD :

1. Renommons le fichier modèle **en Jenkinsfile** et placez-le sous la branche cible, par exemple, **la branche** principale.
1. Modifiez le flux de CD- Par défaut, nous utilisons les déclencheurs de **pollSCM** lorsqu’une nouvelle modification est poussée dans **la branche** principale.
1. Créez des informations [d’identification du pipeline](https://www.jenkins.io/doc/book/using/using-credentials/) Jenkins pour contenir les informations d’identification du principal de service Azure Microsoft 365 de connexion au compte.
1. Modifiez les scripts de build si nécessaire.
1. Supprimez les scripts de test si vous n’avez pas de tests.

### <a name="credentials-for-jenkins"></a>Informations d’identification pour Jenkins

Suivez [using-credentials pour](https://www.jenkins.io/doc/book/using/using-credentials/) créer des informations d’identification sur Jenkins.

|Nom|Description|
|---|---|
|`AZURE_SERVICE_PRINCIPAL_NAME`|Nom principal de service d’Azure utilisé pour mettre en service des ressources.|
|`AZURE_SERVICE_PRINCIPAL_PASSWORD`|Mot de passe du principal de service Azure.|
|`AZURE_SUBSCRIPTION_ID`|Pour identifier l’abonnement dans lequel les ressources seront mise en service.|
|`AZURE_TENANT_ID`|Pour identifier le client dans lequel réside l’abonnement.|
|`M365_ACCOUNT_NAME`|Le Microsoft 365 pour la création et la publication de l’Teams app.|
|`M365_ACCOUNT_PASSWORD`|Mot de passe du compte Microsoft 365 client.|
|`M365_TENANT_ID`|Pour identifier le client dans lequel l’application Teams est créée ou publiée. La valeur est facultative, sauf si vous avez un compte multi-locataire et que vous souhaitez utiliser un autre client. En savoir plus [sur la façon de trouver votre ID Microsoft 365 client.](/azure/active-directory/fundamentals/active-directory-how-to-find-tenant)|

## <a name="get-started-guide-for-other-platforms"></a>Guide de mise en place pour d’autres plateformes

Vous pouvez suivre les exemples de scripts Bash répertoriés pour créer et personnaliser des pipelines CI ou CD sur d’autres plateformes :

* [CI Scripts](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh)
* [CD Scripts](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)

Les scripts sont basés sur un outil de ligne de commande TeamsFx sur plusieurs plateformes [TeamsFx-CLI](https://www.npmjs.com/package/@microsoft/teamsfx-cli). Vous pouvez l’installer avec `npm install -g @microsoft/teamsfx-cli` et suivre [la documentation](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) pour personnaliser les scripts.

> [!NOTE]
> * Pour activer l’exécution `@microsoft/teamsfx-cli` en mode CI, activez `CI_ENABLED` le mode `export CI_ENABLED=true`. En mode CI, est `@microsoft/teamsfx-cli` convivial pour CI ou CD.
> * Pour activer l’exécution `@microsoft/teamsfx-cli` en mode non interactif, définissez une config globale avec la commande : `teamsfx config set -g interactive false`. En mode non interactif, vous ne `@microsoft/teamsfx-cli` poserez pas de questions sur les entrées de manière interactive.

Veillez à définir les informations d’identification Azure et Microsoft365 dans les variables de votre environnement en toute sécurité. Par exemple, si vous utilisez GitHub comme référentiel de code source. Pour plus d’informations, [voir Secrets Github](https://docs.github.com/en/actions/reference/encrypted-secrets).

## <a name="create-azure-service-principals"></a>Créer des principaux de service Azure

Pour mettre en service et déployer des ressources ciblant Azure à l’intérieur de CI/CD, vous devez créer un principal de service Azure à utiliser.

Pour créer des principaux de service Azure, effectuez les étapes suivantes :
1. Inscrivez une application Microsoft Azure Active Directory (Azure AD) dans un seul client.
2. Attribuez un rôle à votre application Microsoft Azure Active Directory (Azure AD) pour accéder à votre abonnement Azure et `Contributor` le rôle est recommandé. 
3. Créez une nouvelle Microsoft Azure Active Directory (Azure AD) d’application.

> [!TIP]
> Enregistrez votre ID de client, votre ID d’application(AZURE_SERVICE_PRINCIPAL_NAME) et le secret(AZURE_SERVICE_PRINCIPAL_PASSWORD) pour une utilisation ultérieure.

Pour plus d’informations, [consultez les instructions relatives aux principaux de service Azure](/azure/active-directory/develop/howto-create-service-principal-portal). Les trois méthodes de création du principal de service sont les suivantes : 
* [Microsoft Azure portail](/azure/active-directory/develop/howto-create-service-principal-portal)
* [Windows PowerShell](/azure/active-directory/develop/howto-authenticate-service-principal-powershell)
* [Microsoft Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli)

## <a name="publish-teams-app-using-teams-developer-portal"></a>Publier une Teams à l’aide Teams portail du développeur
Si des modifications sont apportées au fichier manifeste Teams’application, vous pouvez publier à nouveau l’application Teams pour mettre à jour le manifeste.

Pour publier Teams’application manuellement, vous pouvez tirer parti du [Portail des développeurs pour Teams](https://dev.teams.microsoft.com/home).

Pour publier votre application, effectuez les étapes suivantes :
1. Connectez-vous [au portail développeur pour Teams](https://dev.teams.microsoft.com) à l’aide du compte correspondant.
2. Importez votre package d’application dans zip en sélectionnant `App -> Import app -> Replace`.
3. Sélectionnez l’application cible dans la liste des applications.
4. Publier votre application en sélectionnant `Publish -> Publish to your org`

### <a name="see-also"></a>Voir aussi

* [Démarrage rapide des actions de GitHub](https://docs.github.com/en/actions/quickstart#creating-your-first-workflow)
* [Créer votre premier Azure DevOps pipeline](/azure/devops/pipelines/create-first-pipeline)
* [Créer votre premier pipeline Jenkins](https://www.jenkins.io/doc/pipeline/tour/hello-world/)
* [Gérer vos applications avec le Portail des développeurs pour Microsoft Teams](/concepts/build-and-test/teams-developer-portal)
