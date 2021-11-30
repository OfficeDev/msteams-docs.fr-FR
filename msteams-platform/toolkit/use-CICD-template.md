---
title: Prise en charge ci ou CD pour Teams développeurs d’applications
author: MuyangAmigo
description: Modèles TORS
ms.author: ruhe
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: ff5b77b7891d36e63f2fd3260ae114cbf536384d
ms.sourcegitcommit: f1e6f90fb6f7f5825e55a6d18ccf004d0091fb6d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/30/2021
ms.locfileid: "61227964"
---
# <a name="ci-or-cd-support-for-teams-application-developers"></a>Prise en charge ci ou CD-TEAMS développeurs d’applications

TeamsFx permet d’automatiser votre flux de travail de développement tout en Teams application. Le document fournit des outils et des modèles pré-modèles pour commencer lors de la configuration des pipelines CI ou CD avec les plateformes de développement les plus populaires, notamment GitHub, Azure Devops et Jenkins.


|Outils et modèles|Description|
|---|---|
|[teamsfx-cli-action](https://github.com/OfficeDev/teamsfx-cli-action)|Une action de GitHub prêt à l’emploi qui s’intègre à l’CLI TeamsFx.|
|[github-ci-template.yml](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/github-ci-template.yml) et [github-cd-template.yml](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/github-cd-template.yml)| GitHub modèles CI ou CD pour une Teams application. |
|[jenkins-ci-template. Jenkinsfile](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/jenkins-ci-template.Jenkinsfile) et [jenkins-cd-template. Jenkinsfile](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/jenkins-cd-template.Jenkinsfile)|Modèles CI ou CD Jenkins pour une Teams application.|
|[script-ci-template.sh](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh) et [script-cd-template.sh](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)| Modèles de script pour l’automatisation partout ailleurs en dehors de GitHub. |

## <a name="ci-or-cd-workflow-templates-in-github"></a>Modèles de flux de travail CI ou CD dans GitHub

Pour inclure des flux de travail CI ou CD pour automatiser Teams processus de **développement d’applications dans GitHub**:

1. Créer un dossier sous `.github/workflows`
1. Copiez les fichiers modèles (l’un d’eux ou les deux) :
    * [github-ci-template.yml pour le](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/github-ci-template.yml) flux de travail CI.
    * [github-cd-template.yml pour le](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/github-cd-template.yml) flux de travail CD.
1. Personnalisez ces flux de travail pour les adapter à vos scénarios.

### <a name="customize-ci-workflow"></a>Personnaliser le flux de travail CI

Vous pouvez apporter les modifications suivantes pour adapter le flux de travail à votre projet :

1. Modifier la façon dont le flux CI est déclenché. Par défaut, nous avons créé une requête de pull ciblant la `dev` branche.
1. Utilisez un script de build npm ou personnalisez la façon dont vous créez le projet dans le code d’automatisation.
1. Utilisez un script de test npm qui renvoie zéro pour la réussite et/ou modifiez les commandes de test.

### <a name="customize-cd-workflow"></a>Personnaliser le flux de travail CD

Les étapes suivantes pour personnaliser le flux de travail CD :

1. Par défaut, le flux de travail CD est déclenché lorsque de nouvelles validations sont réalisées dans la `main` branche.
1. Créez GitHub [secrets de référentiel](https://docs.github.com/en/actions/reference/encrypted-secrets) par environnement pour contenir les informations d’identification Azure Microsoft 365 connexion. Le tableau suivant répertorie toutes les secrets que vous devez créer sur GitHub, et pour une utilisation détaillée, reportez-vous à la GitHub actions [README.md](https://github.com/OfficeDev/teamsfx-cli-action/blob/main/README.md).
1. Modifiez les scripts de build si nécessaire.
1. Supprimez les scripts de test si vous n’avez pas de tests.

> [!Note]
> L’étape de mise en service n’est pas incluse dans le modèle CD, car elle n’est généralement exécutée qu’une seule fois. Vous pouvez exécuter la mise en service dans Teams Shared Computer Toolkit, CLI TeamsFx ou à l’aide d’un flux de travail séperated. N’oubliez pas de valider après l’approvisionnement (les résultats de l’approvisionnement seront déposés dans le dossier) et d’enregistrer le contenu du fichier dans les secrets du référentiel GitHub avec un nom pour une utilisation `.fx` `.fx/states/{YOUR_ENV_NAME}.userdata` [](https://docs.github.com/en/actions/reference/encrypted-secrets) `USERDATA_CONTENT` ultérieure.

### <a name="environment-variables"></a>Variables d’environnement

Étapes pour créer des variables d’environnement GitHub :

1. Dans la page **Paramètres** projet, accédez à la section **Environnements** et sélectionnez **Nouvel environnement.**
1. Entrez un nom pour votre environnement. Le nom d’environnement par défaut fourni dans le modèle est `test_environment` . Sélectionnez **Configurer l’environnement** pour continuer.
1. Dans la page suivante, **sélectionnez Ajouter une secret** pour ajouter des secrets pour chacun des éléments répertoriés dans le tableau ci-dessous.

|Nom|Description|
|---|---|
|AZURE_ACCOUNT_NAME|Nom de compte Azure utilisé pour mettre en service des ressources.|
|AZURE_ACCOUNT_PASSWORD|Mot de passe du compte Azure.|
|AZURE_SUBSCRIPTION_ID|Pour identifier l’abonnement dans lequel les ressources seront mise en service.|
|AZURE_TENANT_ID|Pour identifier le client dans lequel réside l’abonnement.|
|Microsoft 365_ACCOUNT_NAME|Le Microsoft 365 pour la création et la publication de l’Teams app.|
|Microsoft 365_ACCOUNT_PASSWORD|Mot de passe du compte Microsoft 365 client.|
|Microsoft 365_TENANT_ID|Pour identifier le client dans lequel l’application Teams sera créée/publiée. Cette valeur est facultative, sauf si vous avez un compte multi-locataire et que vous souhaitez utiliser un autre client. En savoir plus [sur la façon de trouver votre ID Microsoft 365 client.](/azure/active-directory/fundamentals/active-directory-how-to-find-tenant)|
> Remarque : reportez-vous aux informations d’identification Configurer [Microsoft 365/Azure](https://github.com/OfficeDev/teamsfx-cli-action/blob/main/README.md#configure-m365azure-credentials-as-github-secret) pour vous assurer que vous avez désactivé l’authentification multifacteur et les paramètres de sécurité par défaut pour les informations d’identification utilisées dans le flux de travail.

## <a name="set-up-ci-or-cd-pipelines-with-azure-devops"></a>Configurer des Pipelines CD ou CI avec Azure DevOps

Vous pouvez configurer des pipelines automatisés dans Azure DevOps et créer une référence sur les scripts. Suivez les étapes ci-dessous pour commencer :

* [CI Scripts](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh)
* [CD Scripts](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)

### <a name="set-up-ci-pipeline"></a>Configurer le pipeline CI

1. Ajoutez [des scripts CI](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh) dans votre référentiel Azure DevOps et faites les personnalisations nécessaires, comme vous pouvez en déduire à partir des commentaires dans le fichier de script.
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

Les modifications potentielles que vous pouvez apporter au script ou à la définition de flux de travail :

1. Modifier la façon dont le flux CI est déclenché. Par défaut, une nouvelle validation est poussée dans la `dev` branche.
1. Modifier la façon d’installer les nœuds et npm.
1. Utilisez le script de build npm ou personnalisez la façon dont vous créez le code d’automatisation.
1. Utilisez un script de test npm qui renvoie zéro pour la réussite et/ou modifiez les commandes de test.

### <a name="set-up-cd-pipeline"></a>Configurer le pipeline CD

1. Ajoutez [des scripts](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh) CD dans votre référentiel Azure DevOps et faites les personnalisations nécessaires, comme vous pouvez en déduire à partir des commentaires dans le fichier de script.
1. Créez votre Azure DevOps pipeline pour CD,comme vous pouvez vous référer [à ce lien.](/azure/devops/pipelines/create-first-pipeline) La définition du pipeline peut être référente à l’exemple de définition suivant pour le pipeline CI.
1. Ajoutez les variables nécessaires [par définir des variables](/azure/devops/pipelines/process/variables)et faites-les secrètes si nécessaire.

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

- task: DownloadSecureFile@1
  name: userdata
  inputs:
    secureFile: 'staging.userdata'
- task: Bash@3
  inputs:
    targetType: 'inline'
    script: |
      mkdir -p .fx/states/
      cp $(userdata.secureFilePath) .fx/states/staging.userdata
  
- task: Bash@3
  env:
    AZURE_ACCOUNT_NAME: $(AZURE_ACCOUNT_NAME)
    AZURE_ACCOUNT_PASSWORD: $(AZURE_ACCOUNT_PASSWORD)
    AZURE_SUBSCRIPTION_ID: $(AZURE_SUBSCRIPTION_ID)
    AZURE_TENANT_ID: $(AZURE_TENANT_ID)
    Microsoft 365_ACCOUNT_NAME: $(Microsoft 365_ACCOUNT_NAME)
    Microsoft 365_ACCOUNT_PASSWORD: $(Microsoft 365_ACCOUNT_PASSWORD)
  inputs:
    filePath: './others-script-cd-template.sh'
```

Les modifications potentielles que vous pouvez apporter au script ou à la définition de flux de travail :

1. La façon dont le flux cd est déclenché. Par défaut, cela se produit lorsque de nouvelles validations sont réalisées sur **la branche** principale.
1. Modifier la façon d’installer les nœuds et npm.
1. Modifiez le nom de l’environnement, par défaut sa **zone de transit.**
1. Assurez-vous que vous avez un script de build npm ou personnalisez la façon dont vous créez le code d’automatisation.
1. Assurez-vous que vous avez un script de test npm qui renvoie zéro pour la réussite et/ou modifiez les commandes de test.

> [!Note]
> L’étape de mise en service n’est pas incluse dans le modèle CD, car elle n’est généralement exécutée qu’une seule fois. Vous pouvez exécuter la mise en service dans Teams Shared Computer Toolkit, CLI TeamsFx ou à l’aide d’un flux de travail séperated. N’oubliez pas de valider après l’approvisionnement (les résultats de l’approvisionnement seront déposés dans le dossier) et de télécharger dans Azure DevOps fichiers sécurisés pour une `.fx` `.fx/states/{YOUR_ENV_NAME}.userdata` utilisation ultérieure. [](/azure/devops/pipelines/library/secure-files)

### <a name="environment-variables-for-azure-devops"></a>Variables d’environnement pour Azure DevOps

Étapes pour créer des variables de pipeline dans Azure DevOps :

1. Dans la page Modification du pipeline, sélectionnez **Variables** en haut à droite et **sélectionnez Nouvelle variable.**
1. Entrez la paire Nom/Valeur pour votre variable.
1. Basculez la case à cocher **conserver cette valeur secrète** si nécessaire.
1. Sélectionnez **OK** pour créer la variable.

|Nom|Description|
|---|---|
|AZURE_ACCOUNT_NAME|Nom de compte Azure utilisé pour mettre en service des ressources.|
|AZURE_ACCOUNT_PASSWORD|Mot de passe du compte Azure.|
|AZURE_SUBSCRIPTION_ID|Pour identifier l’abonnement dans lequel les ressources seront mise en service.|
|AZURE_TENANT_ID|Pour identifier le client dans lequel réside l’abonnement.|
|Microsoft 365_ACCOUNT_NAME|Le Microsoft 365 pour la création et la publication de l’Teams app.|
|Microsoft 365_ACCOUNT_PASSWORD|Mot de passe du compte Microsoft 365 client.|
|Microsoft 365_TENANT_ID|Pour identifier le client dans lequel l’application Teams sera créée/publiée. Cette valeur est facultative, sauf si vous avez un compte multi-locataire et que vous souhaitez utiliser un autre client. En savoir plus [sur la façon de trouver votre ID Microsoft 365 client.](/azure/active-directory/fundamentals/active-directory-how-to-find-tenant)|

> ! Veuillez vous référer aux informations d’identification [Microsoft 365/Azure](https://github.com/OfficeDev/teamsfx-cli-action/blob/main/README.md#configure-m365azure-credentials-as-github-secret) pour vous assurer que vous avez désactivé l’authentification multifacteur et les paramètres de sécurité par défaut pour les informations d’identification utilisées dans le flux de travail.

## <a name="ci-or-cd-pipeline-templates-in-jenkins"></a>Modèles de pipeline CI ou CD dans Jenkins

Pour ajouter ces modèles à votre référentiel, vous aurez besoin de vos versions [de jenkins-ci-template. Jenkinsfile](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/jenkins-ci-template.Jenkinsfile) et  [jenkins-cd-template. Le fichier Jenkinsfile](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/jenkins-cd-template.Jenkinsfile) doit se trouver dans votre référentiel par branche.

En outre, vous devez créer des pipelines CI ou CD dans Jenkins qui pointent vers le **fichier Jenkinsfile** spécifique correspondant.

Suivez les étapes pour vérifier comment connecter Jenkins avec différentes plateformes SCM :

1. [Jenkins avec GitHub](https://www.jenkins.io/solutions/github/)
2. [Jenkins avec Azure DevOps](https://www.dragonspears.com/blog/ci-cd-with-jenkins-and-azure-devops-services)
3. [Jenkins avec GitLab](https://docs.gitlab.com/ee/integration/jenkins.html)
4. [Jenkins avec Bitbucket](https://medium.com/ampersand-academy/integrate-bitbucket-jenkins-c6e51103d0fe)

### <a name="customize-ci-pipeline"></a>Personnaliser le pipeline CI

Vous pouvez apporter certaines modifications potentielles pour adapter votre projet :

1. Renommons le fichier modèle **en Jenkinsfile** car il s’agit d’une pratique courante et placez-le sous la branche cible, par exemple, la branche **dev.**
1. Modifier la façon dont le flux CI est déclenché. Par défaut, nous utilisons les déclencheurs de **pollSCM** lorsqu’une nouvelle modification est poussée dans **la branche dev.**
1. Assurez-vous que vous avez un script de build npm ou personnalisez la façon dont vous créez le code d’automatisation.
1. Assurez-vous que vous avez un script de test npm qui renvoie zéro pour la réussite et/ou modifiez les commandes de test.

### <a name="customize-cd-pipeline"></a>Personnaliser le pipeline CD

Modifiez les étapes suivantes pour personnaliser le pipeline CD :

1. Renommons le fichier modèle **en Jenkinsfile** car il s’agit d’une pratique courante et placez-le sous la branche cible, par exemple, **la branche** principale.
1. La façon dont le flux cd est déclenché. Par défaut, nous utilisons les déclencheurs de **pollSCM** lorsqu’une nouvelle modification est poussée dans **la branche** principale.
1. Créez des informations [d’identification du pipeline](https://www.jenkins.io/doc/book/using/using-credentials/) Jenkins pour contenir les informations d’identification Azure/Microsoft 365 connexion. Le tableau ci-dessous répertorie toutes les informations d’identification que vous devez créer dans Jenkins.
1. Modifiez les scripts de build si nécessaire.
1. Supprimez les scripts de test si vous n’avez pas de tests.

> [!Note]
 L’étape de mise en service n’est pas incluse dans le modèle CD, car elle n’est généralement exécutée qu’une seule fois. Vous pouvez exécuter la mise en service dans Teams Shared Computer Toolkit, CLI TeamsFx ou à l’aide d’un flux de travail séperated. N’oubliez pas de valider après l’approvisionnement (les résultats de l’approvisionnement seront déposés dans le dossier) et d’enregistrer le contenu du fichier dans les informations d’identification Jenkins pour une `.fx` `.fx/states/{YOUR_ENV_NAME}.userdata` utilisation ultérieure.

### <a name="environment-variables-for-jenkins"></a>Variables d’environnement pour Jenkins

Suivez [using-credentials pour](https://www.jenkins.io/doc/book/using/using-credentials/) créer des informations d’identification sur Jenkins.

|Nom|Description|
|---|---|
|AZURE_ACCOUNT_NAME|Nom de compte Azure utilisé pour mettre en service des ressources.|
|AZURE_ACCOUNT_PASSWORD|Mot de passe du compte Azure.|
|AZURE_SUBSCRIPTION_ID|Pour identifier l’abonnement dans lequel les ressources seront mise en service.|
|AZURE_TENANT_ID|Pour identifier le client dans lequel réside l’abonnement.|
|Microsoft 365_ACCOUNT_NAME|Compte M3icrosoft 365 pour la création et la publication de l Teams applique.|
|Microsoft 365_ACCOUNT_PASSWORD|Mot de passe du compte Microsoft 365 client.|
|Microsoft 365_TENANT_ID|Pour identifier le client dans lequel l’application Teams sera créée/publiée. Cette valeur est facultative, sauf si vous avez un compte multi-locataire et que vous souhaitez utiliser un autre client. En savoir plus [sur la façon de trouver votre ID Microsoft 365 client.](/azure/active-directory/fundamentals/active-directory-how-to-find-tenant)|
> Remarque : reportez-vous aux informations d’identification Configurer [Microsoft 365/Azure](https://github.com/OfficeDev/teamsfx-cli-action/blob/main/README.md#configure-m365azure-credentials-as-github-secret) pour vous assurer que vous avez désactivé l’authentification multifacteur et les paramètres de sécurité par défaut pour les informations d’identification utilisées dans le pipeline.

## <a name="get-started-guide-for-other-platforms"></a>Guide de mise en place pour d’autres plateformes

Vous pouvez suivre les exemples de scripts Bash répertoriés pour créer et personnaliser des pipelines CI ou CD sur d’autres plateformes :

* [CI Scripts](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh)
* [Scripts CD](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh) Les scripts sont relativement simples et la plupart d’entre eux sont des CLI sur plusieurs plateformes. Il est donc facile de les transformer en d’autres types de scripts, par exemple, PowerShell.

Les scripts sont basés sur un outil de ligne de commande TeamsFx sur plusieurs plateformes [TeamsFx-CLI.](https://www.npmjs.com/package/@microsoft/teamsfx-cli) Vous pouvez l’installer avec `npm install -g @microsoft/teamsfx-cli` et suivre la [documentation](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) pour personnaliser les scripts.

> [!Note]
> Pour activer `@microsoft/teamsfx-cli` l’exécution en mode CI, `CI_ENABLED` activez le mode `export CI_ENABLED=true` . En mode CI, `@microsoft/teamsfx-cli` est convivial pour CI ou CD.

Veillez à définir les informations d’identification Azure et M365 dans les variables de votre environnement en toute sécurité. Par exemple, si vous utilisez GitHub comme référentiel de code source, vous pouvez utiliser [github Secrets](https://docs.github.com/en/actions/reference/encrypted-secrets) pour stocker en toute sécurité vos variables d’environnement.

### <a name="see-also"></a>Voir aussi

* [Démarrage rapide des actions de GitHub](https://docs.github.com/en/actions/quickstart#creating-your-first-workflow)
* [Créer votre premier Azure DevOps pipeline](/azure/devops/pipelines/create-first-pipeline)
* [Créer votre premier pipeline Jenkins](https://www.jenkins.io/doc/pipeline/tour/hello-world/)
