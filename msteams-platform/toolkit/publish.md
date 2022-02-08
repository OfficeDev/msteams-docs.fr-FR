---
title: Publier des applications Teams à l’aide du Kit de ressources Teams
author: zyxiaoyuer
description: publier Teams applications
ms.author: yanjiang
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
---


# <a name="publish-teams-apps-using-teams-toolkit"></a>Publier des applications Teams à l’aide du Kit de ressources Teams

Après avoir créé l’application, vous pouvez distribuer votre application à différentes étendues, telles qu’une personne, une équipe, une organisation ou toute autre personne. La distribution dépend de plusieurs facteurs, notamment les besoins, les besoins commerciaux et techniques, ainsi que votre objectif pour l’application. La distribution à une étendue différente peut avoir besoin d’un processus de révision différent. En règle générale, plus l’étendue est grande, plus l’application doit passer en revue les problèmes de sécurité et de conformité.

## <a name="prerequisite"></a>Conditions préalables

* [Installez Teams Shared Computer Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) version v3.0.0+.

> [!TIP]
> Assurez-vous que vous Teams projet d’application dans du code VS.

## <a name="publish-to-individual-scope-or-sideload-permission"></a>Publier sur une étendue individuelle ou une autorisation sideload

Les utilisateurs peuvent ajouter une application personnalisée à Teams en chargeant un package d’application dans un fichier *.zip directement dans une équipe ou dans un contexte personnel. L’ajout d’une application personnalisée en chargeant un package d’application est appelé chargement de version test et vous permet de tester l’application lors du développement, avant que l’application soit prête à être largement distribuée, comme mentionné dans les scénarios suivants :

* Testez et déboguer une application localement.
* Créez une application pour vous-même, par exemple pour automatiser un flux de travail.
* Créez une application pour un petit groupe d’utilisateurs, par exemple, votre groupe de travail.

Vous pouvez créer une application pour un usage interne uniquement et la partager avec votre équipe sans la soumettre au catalogue d’applications Teams dans le Teams’application store.

**Pour créer votre application pour créer *.zip de package d’application**

Vous pouvez créer le package d’application en sélectionnant `Zip Teams metadata package` **à partir de DEPLOYMENT** dans Treeview de Teams Shared Computer Toolkit. Vous devez exécuter en `Provision in the cloud` premier. Le package d’application généré se trouve dans `{your project folder}/build/appPackage/appPackage.{env}.zip`.

Pour télécharger le package d’application, effectuez les étapes suivantes :

1. Dans le Teams client, sélectionnez **Applications dans** la barre de gauche.
2. **Sélectionnez Gérer vos applications**.
3. Sélectionner **publier une application**

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/pub.png" alt-text="Publication":::

4. **Sélectionnez Télécharger une application personnalisée** :

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/uplo.png" alt-text="upload":::

## <a name="publish-to-your-organization"></a>Publier pour votre organisation 

Lorsque l’application est prête à être en production, vous pouvez la soumettre à l’aide de l’API de soumission d’application Teams, appelée à partir de l’API Graph, un environnement de développement intégré tel que Microsoft Visual Studio Code installé avec le kit de ressources Teams. Vous pouvez soit sélectionner Publier sur **Teams** à partir de **DEPLOYMENT** dans TreeView de Teams Shared Computer Toolkit, soit déclencher Teams **:** Publier sur Teams à partir de la palette de commandes. Sélectionnez **Ensuite Installer pour votre organisation** :

![Installation pour votre organisation](./images/installforyourorganization.png)

L’application est disponible dans  le Centre d’administration Microsoft Teams, où vous et l’administrateur pouvez l’examiner et l’approuver.

En tant qu’administrateur, **la** gestion des applications dans le [centre d’administration Microsoft Teams](https://admin.teams.microsoft.com/policies/manage-apps) est l’endroit où vous pouvez afficher et gérer toutes les applications Teams pour votre organisation. Vous pouvez voir l’état et les propriétés des applications au niveau de l’organisation, approuver ou télécharger de nouvelles applications personnalisées dans le magasin d’applications de votre organisation, bloquer ou autoriser des applications au niveau de l’organisation, ajouter des applications à des équipes, acheter des services pour des applications tierces, afficher les autorisations demandées par les applications, accorder le consentement administrateur aux applications et gérer les [paramètres](https://admin.teams.microsoft.com/policies/manage-apps) d’application à l’échelle de l’organisation.

Teams kit de ressources pour Visual Studio Code intégré à l’API de soumission d’application Teams et il vous permet d’automatiser le processus de soumission à approbation pour les applications personnalisées sur Teams.

> [!NOTE]
> L’application ne publie pas encore dans le magasin d’applications de votre organisation. L’étape envoie l’application au Centre d’administration Microsoft Teams où vous pouvez l’approuver pour la publication dans le magasin d’applications de votre organisation.

## <a name="admin-approval-for-teams-apps"></a>Approbation de l’administrateur pour Teams applications

L’administrateur de votre client Teams peut ensuite se rendre sur Gérer les  applications dans le Centre d’administration Microsoft Teams, dans le navigation de gauche, pour Teams applications > Gérer les applications. Vous pouvez afficher toutes les applications Teams pour votre organisation. Dans le widget d’approbation en attente en haut de la page, vous pouvez savoir quand une application personnalisée est soumise pour approbation.
Dans le tableau, une application nouvellement soumise publie automatiquement l’état des applications soumises et bloquées. Vous pouvez trier la colonne d’état de publication dans l’ordre décroit pour trouver l’application :

 :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/admin-approval-for-teams-app-1.png" alt-text="approbation":::

Sélectionnez le nom de l’application pour aller à la page des détails de l’application. Sous l’onglet À propos de, vous pouvez afficher des détails sur l’application, notamment la description, l’état et l’ID de l’application :

 :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/about-submitted-app-1.png" alt-text="application soumise":::

Effectuez les étapes suivantes pour publier l’application :

1. Dans le navigation gauche du centre d Microsoft Teams d’administration, Teams applications > **gérer les applications**.
2. Sélectionnez le nom de l’application pour aller à la page des détails de l’application, puis dans la zone d’état, sélectionnez **Publier**.
Une fois que vous avez publié l’application, l’état de publication passe à publié et l’état passe automatiquement à autorisé.

## <a name="publish-to-microsoft-store"></a>Publier dans le Microsoft Store

Vous pouvez distribuer votre application directement dans le Store Microsoft Teams et atteindre des millions d’utilisateurs dans le monde entier. Si votre application est également présente dans le Store, vous pouvez immédiatement atteindre des clients potentiels. Les applications publiées dans Teams store sont également répertoriées automatiquement sur Microsoft AppSource, qui est la place de marché officielle pour Microsoft 365 applications et solutions.

Pour plus d’informations, [voir publier dans le microsoft Teams store]([Publish your app to the Microsoft Teams store](../concepts/deploy-and-publish/appsource/publish.md#publish-your-app-to-the-microsoft-teams-store))

## <a name="see-also"></a>Voir aussi

* [Gérer plusieurs environnements](TeamsFx-multi-env.md)
* [Collaborer avec d’autres développeurs sur Teams projet](TeamsFx-collaboration.md)