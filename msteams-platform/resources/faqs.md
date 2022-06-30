---
title: Foire aux questions sur Moodle
description: Dans cet article, récupérez les réponses à certaines questions fréquemment posées lors de l’utilisation de Moodle LMS.
ms.topic: Frequently asked questions on Moodle LMS
ms.localizationpriority: high
ms.author: Surbhigupta
ms.openlocfilehash: c617b3db7982e192db6cde9375be751e2cf2bf26
ms.sourcegitcommit: c398dfdae9ed96f12e1401ac7c8d0228ff9c0a2b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/30/2022
ms.locfileid: "66558295"
---
# <a name="moodle-faq"></a>FAQ sur Moodle

Obtenez des réponses à certaines de vos requêtes lors de l’utilisation de Moodle LMS.<br>

<br>

<details>

<summary><b>Que dois-je faire si une ou plusieurs équipes de cours n’ont pas été créées après la synchronisation ?</b></summary>

Chaque cours Moodle doit avoir au moins un enseignant et un étudiant associés à un compte UPN Microsoft 365 AAD. L’équipe ne peut pas être créée si la synchronisation ne trouve pas de correspondance.

Chaque instance de cours en équipe doit avoir un propriétaire, et la synchronisation définit l’enseignant comme propriétaire, en supposant que la faculté possède la licence Teams.

<br>

</details>

<details>

<summary><b>Que devons-nous faire pour supprimer la page de connexion Moodle lorsque vous travaillez dans Teams ? Pouvons-nous forcer l’authentification unique (SSO) ?</b></summary>

Les utilisateurs disposent de plusieurs options de connexion à partir de la page de connexion Moodle.

* Pour vous connecter exclusivement à l’aide d’informations d’identification Microsoft 365, activez les paramètres de configuration **Forcer la redirection** pour le **plug-in auth_oidc**. Si le service est activé, l’utilisateur peut voir la page de connexion Microsoft.
* Pour vous connecter manuellement au portail Moodle, consultez [Moodle](https://moodle.org/login/index.php).

<br>

</details>

<details>

<summary><b>Comment puis-je spécifier les utilisateurs à synchroniser ? Je ne souhaite pas que tous les utilisateurs d'Azure AD soient synchronisés avec le site Web de Moodle. </b></summary>

Utilisez l’option **Restriction de création d’utilisateur** pour spécifier les utilisateurs en synchronisant les options de configuration du plug-in **local_o365**. Le menu déroulant à gauche du **filtre** propose des options telles que le pays, le nom de la société et la langue.

> [!TIP]
> Créez un groupe dynamique Microsoft 365 pour activer l'option de **filtre** avec plusieurs propriétés de profil.

L’image suivante montre les options de restrictions de création d’utilisateur :

:::image type="content" source="../assets/images/MoodleInstructions/faq-2.png" alt-text="synchro":::

:::image type="content" source="../assets/images/MoodleInstructions/faq-3.png" alt-text="Azure AD":::

<br>

</details>

<details>

<summary><b>Nous souhaiterions que nos enseignants puissent synchroniser leurs cours avec Teams. Les administrateurs de Moodle sont-ils les seuls à pouvoir contrôler la synchronisation des cours ?</b></summary>

Par défaut, seuls les administrateurs Moodle peuvent configurer la synchronisation. Le propriétaire de l'équipe peut contrôler si un cours est synchronisé avec les équipes et **Autoriser la configuration de la synchronisation de cours dans le cours** est activé. Dans ce cas, l’enseignant est le propriétaire de l’équipe. Le bloc affiche l’option de configuration pour les personnes ayant les autorisations de propriétaire appropriées.

<!-- For more information, see Microsoft 365 block within the Moodle course interface. -->

L’image suivante montre l’option **Autoriser la configuration de la synchronisation de cours dans le cours** :

:::image type="content" source="../assets/images/MoodleInstructions/faq-4.png" alt-text="administrateur":::

L’image suivante illustre la synchronisation des cours :

:::image type="content" source="../assets/images/MoodleInstructions/faq-5.png" alt-text="synchronisation":::

<br>

</details>

<details>

<summary><b>Nous avons suivi la documentation, mais les comptes utilisateurs ne parviennent pas à synchroniser Moodle à AAD. Que devons-nous faire ?</b></summary>

Le problème peut être résolu avant que les utilisateurs n'effectuent le **Nettoyage du jeton Delta** comme étape finale de dépannage.

Le tableau suivant fournit les actions et dépendances à effectuer et à vérifier :

| Dépendance | Action | Référence|
|-------|------------|----------|
| Version stable| Vérifiez que la version de Moodle est répertoriée comme **stable**.| Pour plus d’informations, consultez [Prise en charge de la version](https://docs.moodle.org/dev/Releases#Version_support).|
|Autorisations| Vérifiez que l’application Azure dispose des autorisations nécessaires pour exécuter la synchronisation.| Pour plus d’informations, consultez [Autorisations Microsoft](https://docs.moodle.org/311/en/Microsoft_365#Permissions).|
| Synchronisation complète| Vérifiez que l'option **Effectuer une synchronisation complète à chaque exécution** est activée, et examinez les **Journaux des tâches** pour **Synchroniser les utilisateurs avec Azure AD**.| Pour plus d’informations, consultez [Activer la synchronisation complète](https://docs.moodle.org/311/en/local_o365)</br>Pour plus d’informations, consultez [Vérifier les journaux des tâches](https://docs.moodle.org/311/en/local_o365#Sync_users_with_Azure_AD). |
|Actualisation du jeton|Nettoyez le **Jeton delta de synchronisation utilisateur** dans le plug-in local_o365.| Pour plus d’informations, consultez [Actualisation du jeton](https://docs.moodle.org/38/en/Office365).|
<!-- |Actualisation du jeton|Nettoyer le **Jeton delta de synchronisation utilisateur** dans le plug-in local_o365| {moodle_url}\local_o365\acp.php? Mode=maintenance_cleandeltatoken| -->
<br>

</details>

<details>

<summary><b>Un ou plusieurs utilisateurs ne parviennent pas à se connecter à l'aide de leurs informations d'identification Microsoft 365, alors que la plupart des utilisateurs peuvent se connecter sans problème. Quelle serait la cause de cette incohérence ?</b></summary>

La raison des incohérences avec les utilisateurs qui ne peuvent pas signer en utilisant leurs informations d'identification Microsoft 365 peut être liée à l'opération de mappage des utilisateurs pendant la synchronisation. Pour résoudre ce problème, procédez comme suit :

* Vérifiez si le type d’authentification de l’utilisateur est **OpenID**.
* Vérifiez si le **Nom d’utilisateur** Moodle correspond au nom d’utilisateur AAD.
* Nettoyez le **Problème de jeton et** réessayez.
* Vérifiez si les utilisateurs ont des **Autorisations** pour accéder à l'application Azure.

<br>

</details>

<details>

<summary><b>Tous les utilisateurs ne parviennent pas à se connecter à l'aide de leurs informations d'identification Microsoft 365. Que pouvons-nous faire pour résoudre ce problème ?</b></summary>

Les utilisateurs qui n’ont pas pu se connecter au démarrage doivent signaler le problème et vérifier que la **Clé secrète du client** de l’application n’a pas expiré.

L'image suivante montre le message d'erreur reçu lorsque l'utilisateur signe en utilisant ses informations d'identification Microsoft 365 :

:::image type="content" source="../assets/images/MoodleInstructions/faq-6.png" alt-text="signaler un problème":::

L'image suivante montre l'erreur dans le portail Azure :

:::image type="content" source="../assets/images/MoodleInstructions/faq-7.png" alt-text="Portail Azure":::

Si la **clé secrète du client** a expiré, l’utilisateur doit en générer une nouvelle **clé secrète** et mettre à jour la configuration trouvée sur la page. Les utilisateurs peuvent se reconnecter après la mise à jour de la **clé secrète du client**, ce qui peut prendre jusqu’à 24 heures.

<br>

</details>

<details>

<summary><b>Comment modifier l’instance d’équipe liée à un cours ?</b></summary>

Les administrateurs peuvent modifier l’instance d’équipe associée à un cours via la page **Gérer les connexions d’équipes**. Sélectionnez **Connecter** à côté du cours à modifier et sélectionnez l’instance d’équipe. Si vous utilisez la réinitialisation de cours pour archiver une équipe, vous pouvez la lier à l’équipe précédente.

L'image suivante montre l'instance des équipes :

:::image type="content" source="../assets/images/MoodleInstructions/faq-8.png" alt-text="instance des équipes":::

<br>

</details>

<details>

<summary><b>Pourquoi l'intégration des réunions Atto Teams ne s'affiche-t-elle pas dans l'éditeur Atto ?</b></summary>

L'utilisateur peut être confronté à un problème de réunion Atto Teams si la référence à l'icône est absente de la **Configuration de la barre d'outils**, qui affiche l'icône Teams dans l'éditeur Atto. L'utilisateur doit ajouter l'icône de réunion Teams à droite de l'icône de liens en suivant les étapes suivantes :

* Installez le plug-in.
* Mettre à jour la **Configuration de la barre d’outils** avec une **réunion Teams**.

Les images suivantes montrent l’icône de la barre d’outils après ajustement de la configuration de la barre d’outils :

:::image type="content" source="../assets/images/MoodleInstructions/faq-9.png" alt-text="barre d’outils":::

:::image type="content" source="../assets/images/MoodleInstructions/faq-10.png" alt-text="icône liens":::

Pour plus d’informations sur la modification de la barre d’outils Atto, consultez :

* [Éditeur Atto-ModdleDocs](https://docs.moodle.org/311/en/Atto_editor)
* [Éditeur Atto-Mappage des icônes](https://docs.moodle.org/311/en/Atto_editor#:~:text=in%20the%20editor.-,Atto%20editor%20toolbar,-Atto%20Row%201)
<br>

</details>

<details>

<summary><b>Les réunions programmées via l'intégration Microsoft apparaissent-elles dans les calendriers d'Outlook ou de Teams ? Quel est le délai standard d'affichage des réunions ?</b></summary>

Les réunions programmées via l'application n'apparaissent pas dans le calendrier Outlook ou Teams du planificateur, car elles sont similaires aux réunions de canal. Tous les membres du canal de cours peuvent assister à la réunion directement à partir du lien du canal intégré. Pour plus d’informations, consultez [Réunions de canal](https://www.knowledgewave.com/blog/benefits-of-channel-meetings-in-microsoft-teams).

Toutefois, vous pouvez accéder à l'invitation et ajouter manuellement les noms des participants aux champs **Obligatoires** ou **Facultatifs** de l'invitation à la réunion pour afficher la réunion à distance sur leurs calendriers. Les chronologies standard sont basés sur la date que l'utilisateur indique lors de la création de la réunion. Pour plus d’informations, consultez [Limites et spécifications pour Teams](/microsoftteams/limits-specifications-teams).

<br>

</details>

<details>

<summary><b>Existe-t-il un site de support où nous pouvons obtenir plus d’aide sur les produits et d’autres problèmes ?</b></summary>

Pour obtenir de l'aide et de l'assistance sur les questions relatives aux produits et aux services ou pour obtenir de l'aide de la communauté des développeurs, consultez [Support et commentaires](/microsoftteams/platform/feedback).
