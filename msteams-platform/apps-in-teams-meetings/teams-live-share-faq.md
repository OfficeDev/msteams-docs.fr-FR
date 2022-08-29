---
title: FAQ sur Live Share
author: surbhigupta
description: Dans ce module, découvrez-en plus sur la FAQ Live Share.
ms.topic: overview
ms.localizationpriority: high
ms.author: v-ypalikila
ms.date: 04/07/2022
ms.openlocfilehash: b53d7c01722faa51824e0df17586bc8a385438b0
ms.sourcegitcommit: 134ce9381891e51e6327f1f611fdfd60c90cca18
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/24/2022
ms.locfileid: "67425609"
---
---

# <a name="live-share-sdk-faq"></a>FAQ sur le Kit de développement logiciel (SDK) de partage en direct

Obtenez des réponses aux questions courantes lors de l’utilisation de Live Share.<br>

<br>

<details>

<summary><b>Puis-je utiliser mon propre service Relais Azure Fluid ?</b></summary>

Oui. Lors de la construction de la classe `TeamsFluidClient`, vous pouvez définir votre propre `AzureConnectionConfig`. Live Share associe des conteneurs que vous créez à des réunions, mais vous devez implémenter l’interface `ITokenProvider` pour signer des jetons pour vos conteneurs. Par exemple, vous pouvez utiliser un fourni `AzureFunctionTokenProvider`, qui utilise une fonction cloud Azure pour demander un jeton d’accès à partir d’un serveur.

Bien que la plupart d’entre vous trouvent utile d’utiliser notre service hébergé gratuit, il peut toujours arriver qu’il soit avantageux d’utiliser votre propre service Azure Fluid Relay pour votre application Live Share. Envisagez d’utiliser une connexion de service AFR personnalisée si vous :

* Exiger le stockage des données dans des conteneurs Fluid au-delà de la durée de vie d’une réunion.
* Transmettez des données sensibles via le service qui nécessite une stratégie de sécurité personnalisée.
* Développez des fonctionnalités via Fluid Framework, par exemple, `SharedMap`pour votre application en dehors de Teams.

Pour plus d’informations, consultez [la](./teams-live-share-how-to/how-to-custom-azure-fluid-relay.md) [documentation d’Azure Fluid Relay](/azure/azure-fluid-relay/).

<br>

</details>

<details>

<summary><b>Combien de temps les données stockées dans le service hébergé de Live Share sont-elles accessibles ?</b></summary>

Toutes les données envoyées ou stockées via les conteneurs Fluid créés per le service Relais Azure Fluid de Live Share sont accessibles pendant 24 heures. Si vous souhaitez conserver les données au-delà de 24 heures, vous pouvez remplacer notre service Relais Azure Fluid hébergé par le vôtre. Vous pouvez également utiliser votre propre fournisseur de stockage en parallèle au service hébergé de Live Share.

<br>

</details>

<details>

<summary><b>Quels types de réunions prend Live Share en charge ?</b></summary>

Pendant la préversion, seules les réunions planifiées sont prises en charge et tous les participants doivent figurer dans le calendrier des réunions. Les types de réunion tels que les appels en tête-à-tête, les appels de groupe et les réunions instantanées ne sont pas pris en charge.

<br>

</details>

<details>

<summary><b>Le package multimédia de Live Share fonctionne-t-il avec le contenu DRM ?</b></summary>

Non. Teams ne prend actuellement pas en charge les médias chiffrés pour les applications de tabulation sur le bureau. Les clients Chrome, Edge et mobiles sont pris en charge. Pour plus d’informations, vous pouvez [suivre le problème ici](https://github.com/microsoft/live-share-sdk/issues/14).

<br>

</details>

<details>
<summary><b>Combien de personnes peuvent assister à une session Live Share ?</b></summary>

Actuellement, Live Share prend en charge un maximum de 100 participants par session. Si c’est quelque chose qui vous intéresse, vous pouvez [commencer une discussion ici](https://github.com/microsoft/live-share-sdk/discussions).

<br>

</details>

<details>
<summary><b>Puis-je utiliser les structures de données éphémères de Live Share en dehors de Teams ?</b></summary>

Actuellement, les packages Live Share nécessitent le SDK client Teams pour fonctionner correctement. Les fonctionnalités dans `@microsoft/live-share` Ou `@microsoft/live-share-media` ne fonctionneront pas en dehors de Microsoft Teams. Si c’est quelque chose qui vous intéresse, vous pouvez [commencer une discussion ici](https://github.com/microsoft/live-share-sdk/discussions).

<br>

</details>

<details>
<summary><b>Puis-je utiliser plusieurs conteneurs Fluid ?</b></summary>

Actuellement, Live Share ne prend en charge qu’un seul conteneur à l’aide de notre service Azure Fluid Relay fourni. Toutefois, il est possible d’utiliser à la fois un conteneur Live Share et un conteneur créé par votre propre instance Azure Fluid Relay.

<br>

</details>

<details>
<summary><b>Puis-je modifier mon schéma de conteneur Fluid après avoir créé le conteneur ?</b></summary>

Actuellement, Live Share ne prend pas en charge l’ajout de nouveaux `initialObjects` éléments au fluid `ContainerSchema` après la création ou la jonction d’un conteneur. Étant donné que les sessions Live Share sont de courte durée, il s’agit généralement d’un problème pendant le développement après l’ajout de nouvelles fonctionnalités à votre application.

> [!NOTE]
> Si vous utilisez la `dynamicObjectTypes` propriété dans le `ContainerSchema`, vous pouvez ajouter de nouveaux types à tout moment. Si vous supprimez ultérieurement des types du schéma, les instances DDS existantes de ces types échoueront correctement.

Pour corriger les erreurs résultant des modifications apportées lors `initialObjects` du test local dans votre navigateur, supprimez l’ID de conteneur haché de votre URL et rechargez la page. Si vous effectuez des tests dans une réunion Teams, démarrez une nouvelle réunion et réessayez.

Si vous envisagez de mettre à jour votre application fréquemment avec de nouvelles `SharedObject` instances ou `EphemeralObject` des instances, vous devez réfléchir à la façon dont vous déployez de nouvelles modifications de schéma en production. Bien que le risque réel soit relativement faible et de courte durée, il peut y avoir des sessions actives au moment où vous effectuez la modification. Les utilisateurs existants dans la session ne doivent pas être affectés, mais les utilisateurs qui rejoignent cette session après avoir déployé une modification cassante peuvent rencontrer des problèmes de connexion à la session. Pour atténuer ce problème, vous pouvez envisager certaines des solutions suivantes :

* Déployez les modifications de schéma pour votre application web en dehors des heures d’ouverture normales.
* Utilisez `dynamicObjectTypes` pour toutes les modifications apportées à votre schéma, au lieu de modifier `initialObjects`.

> [!NOTE]
> Live Share ne prend actuellement pas en charge le contrôle de version de votre `ContainerSchema`version et n’a pas d’API dédiées aux migrations.

<br>

</details>

<details>
<summary><b>Existe-t-il des limites au nombre d’événements de modification que je peux émettre via Live Share ?</b></summary>

Bien que Live Share soit en préversion, aucune limite aux événements émis via Live Share n’est appliquée. Pour des performances optimales, vous devez désactiver les modifications émises par le biais `SharedObject` ou `EphemeralObject` les instances d’un message par 50 millisecondes ou plus. Cela est particulièrement important lors de l’envoi de modifications basées sur des coordonnées tactiles ou de souris, par exemple lors de la synchronisation des positions des curseurs, de l’entrée manuscrite et du glissement d’objets autour d’une page.

<br>

</details>

## <a name="have-more-questions-or-feedback"></a>Vous avez d’autres questions ou commentaires ?

Soumettez des problèmes et des demandes de fonctionnalités au référentiel du Kit de développement logiciel (SDK) pour le [Kit de développement logiciel (SDK) Live Share](https://github.com/microsoft/live-share-sdk). Utilisez la balise `live-share` et `microsoft-teams` pour publier des questions de procédure sur le Kit de développement logiciel (SDK) sur [Stack Overflow](https://stackoverflow.com/questions/tagged/live-share+microsoft-teams).

## <a name="see-also"></a>Voir aussi

* [Référentiel GitHub](https://github.com/microsoft/live-share-sdk)
* [ Documents de référence du kit SDK Live Share](/javascript/api/@microsoft/live-share/)
* [Documents de référence du Kit de développement logiciel (SDK) Live Share Media](/javascript/api/@microsoft/live-share-media/)
* [Applications Teams dans les réunions](teams-apps-in-meetings.md)
