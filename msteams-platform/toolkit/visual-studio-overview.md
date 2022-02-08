---
title: Créer des applications avec les Teams Shared Computer Toolkit et Visual Studio
description: 'Commencer à créer d’excellentes applications personnalisées directement Visual Studio l’aide Microsoft Teams Shared Computer Toolkit. Découvrez comment configurer votre application dans Visual Studio, valider votre application et la publier à partir de Visual Studio portail de développement.'
keywords: boîte à outils visual studio teams
ms.localizationpriority: medium
ms.topic: overview
ms.author: johmil
---

# <a name="build-apps-with-the-teams-toolkit-and-microsoft-visual-studio"></a>Créer des applications avec les Teams Shared Computer Toolkit et Microsoft Visual Studio

Le Kit de ressources Microsoft Teams vous permet de créer des applications personnalisées d’équipes directement dans l’environnement de développement intégré (IDE) Visual Studio. Le kit de ressources Microsoft Teams vous guide au cours du processus et vous fournit toutes les fonctionnalités nécessaires pour créer, déboguer et lancer votre application Teams.

## <a name="prerequisites"></a>Conditions préalables

1. [Activer la prévisualisation pour les développeurs](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview).

2. Assurez-vous que **<span>le module ASP.NET</span>** de développement web a été ajouté à votre instance Visual Studio web. Pour plus d’informations, [voir Modifier Visual Studio en ajoutant ou en supprimant des charges de travail et des composants](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true).

![Module de asp.net Visual Studio](../assets/images/visual-studio-web-dev-module.png)

## <a name="install-the-teams-toolkit"></a>Installer le Teams Shared Computer Toolkit

Le Microsoft Teams Shared Computer Toolkit pour Visual Studio est disponible en téléchargement à partir de [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=msft-vsteamstoolkit.vsteamstoolkit) ou directement à partir du menu **Extensions** dans Visual Studio.

## <a name="use-the-toolkit"></a>Utiliser le kit de ressources

- [Configurer un nouveau projet](#set-up-a-new-teams-project)
- [Configurer votre application](#configure-your-app)
- [Exécuter votre application dans Teams](#install-and-run-your-app-locally)
- [Valider votre application](#validate-your-app)
- [Publier votre application](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a>Configurer un nouveau projet Teams projet

1. Lancez Visual Studio 2019.
2. **Sélectionnez Créer un projet**.
3. Recherchez Microsoft Teams **app, puis** sélectionnez **Suivant**.
4. Dans configurer **votre nouveau projet**, entrez le **Project,** **l’emplacement** et le **nom de la solution**.
5. **Sélectionnez Suivant** pour entrer un nom pour l’application.
6. Dans l’écran Informations supplémentaires, entrez un nom **d’application** et un nom de développeur ou de **société pour votre** Teams app.

## <a name="configure-your-app"></a>Configurer votre application

L’application Teams principale englobe trois composants :

- Le Microsoft Teams client (web, de bureau ou mobile) où les utilisateurs interagissent avec votre application.
- Serveur qui répond aux demandes de contenu affichées dans Teams. Par exemple, le contenu d’onglet HTML ou une carte adaptative de bot.
- Un package Teams’application se compose de trois fichiers :

    > [!div class="checklist"]
    >
    > - Manifest.json
    > - Icône [de couleur que](../resources/schema/manifest-schema.md#icons) votre application peut afficher dans le catalogue d’applications public ou d’organisation.
    > - Icône [de plan à](../resources/schema/manifest-schema.md#icons) afficher dans la barre Teams’activité.

Lorsqu’une application est installée, le client Teams pare le fichier manifeste pour déterminer les informations nécessaires, telles que le nom de votre application et l’URL où se trouvent les services.

> [!NOTE]
>Si ce n’est pas déjà fait, vous devez vous Microsoft 365 votre compte d’utilisateur pour poursuivre le processus de développement.
>
> Si vous n’avez pas de compte Microsoft 365, vous pouvez vous inscrire à un abonnement [Microsoft 365 programme pour les développeurs](https://developer.microsoft.com/microsoft-365/dev-program). Il est gratuit pendant 90 jours et renouvelé tant que vous l’utilisez pour l’activité de développement. Si vous avez un abonnement Visual Studio Enterprise ou Professional, les deux programmes incluent un abonnement Microsoft 365 [développeur gratuit,](https://aka.ms/MyVisualStudioBenefits) actif pendant toute la durée de Visual Studio abonnement. Pour plus d’informations, [voir configurer un abonnement Microsoft 365 développeur.](/office/developer-program/office-365-developer-program-get-started)

### <a name="configuration-steps"></a>Étapes de configuration

1. Pour configurer votre application, sélectionnez le menu **Project > TeamsFx > configurer pour l’électrable SSO...**.

Lorsque vous y invitez, connectez-vous à votre compte Microsoft qui possède un client M365.

## <a name="install-and-run-your-app-locally"></a>Installer et exécuter votre application localement

Appuyez sur F5 pour démarrer le débogage. La boîte de dialogue d’installation de l’application s’affiche dans Teams client.

## <a name="validate-your-app"></a>Valider votre application

Le menu **Project > validation teamsFx > Teams manifeste** vous permet de vérifier que votre package d’application est valide.

## <a name="publish-your-app-to-teams"></a>Publier votre application sur Teams

Dans le [portail du développeur Teams](https://dev.teams.microsoft.com/home), vous pouvez télécharger votre application vers une équipe, soumettre votre application au magasin d’applications personnalisé de votre entreprise pour les utilisateurs de votre organisation ou soumettre votre application à la source de l’application pour tous les Teams utilisateurs.

- Votre administrateur informatique examine ces envois.
- Vous pouvez revenir **à la page** Publier pour vérifier l’état de votre soumission et savoir si votre application a été approuvée ou rejetée par votre administrateur informatique. C’est également là que vous pouvez soumettre des mises à jour à votre application ou annuler les soumissions actives.
