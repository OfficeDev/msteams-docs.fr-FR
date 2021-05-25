---
title: Distribuer vos applications
description: Découvrez comment distribuer vos applications à l’aide du portail de développement pour Microsoft Teams.
keywords: mise en place des équipes du portail de développement
localization_priority: Normal
ms.topic: Conceptual
ms.openlocfilehash: d1d098b295492a7dc3b691db4625307b6c3170ce
ms.sourcegitcommit: d972953994e405c6afc42e4d4a76b48c6d4cfb5f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/24/2021
ms.locfileid: "52635075"
---
# <a name="distribute-your-apps"></a>Distribuer vos applications

## <a name="distribute"></a>Distribuer

Une fois que vous avez terminé la définition de votre application, la **section** Distribuer vous permet d’exporter la définition de votre application en tant que fichier zip qui peut ensuite être partagé et chargé dans le client Teams pour les tester. Cliquer sur Exporter télécharge le fichier zip sous **appname.zip** dans votre répertoire de téléchargement par défaut.

:::image type="content" source="~/assets/images/tdp/tdp_distribute_1.png" alt-text="Screenshot showing the Distribute page of Teams Developer Portal.":::

### <a name="manifest"></a>Manifeste

Le manifeste décrit la configuration de votre application, notamment ses fonctionnalités, les ressources requises et d’autres attributs importants. Pour plus [d’informations, voir](~/resources/schema/manifest-schema.md) schéma de manifeste.

### <a name="flights"></a>Vols

Contrôler qui obtient les mises à jour de l’application. Par exemple, vous pouvez publier une mise à jour pour les employés de Microsoft afin d’identifier et de corriger les bogues avant de les publier au public. Sélectionnez **Créer une nouvelle demande** pour créer une demande de vol.

### <a name="publish-to-org"></a>Publier dans l’organisation

Rendez votre application disponible pour les personnes de votre organisation. Une fois approuvée par votre administrateur informatique, votre application sera Teams sous Applications > conçues pour votre organisation.

### <a name="publish-your-app-to-teams-store"></a>Publier votre application dans Teams store

Sur la page d’accueil de votre projet, vous pouvez télécharger votre application dans une équipe, l’envoyer sur le magasin d’applications personnalisé de votre entreprise pour les utilisateurs de votre organisation ou envoyer votre application à la source de l’application pour tous les utilisateurs Teams. Votre administrateur informatique examine ces envois. Vous pouvez revenir à la page **Publier** pour vérifier l’état de votre envoi et savoir si votre application a été approuvée ou refusée par votre administrateur informatique. C’est également ici que vous pouvez envoyer des mises à jour à votre application ou annuler les envois en cours.

## <a name="see-also"></a>Voir aussi

* [Vue d’ensemble Teams portail du développeur](~/concepts/build-and-test/teams-developer-portal.md)
* [Configurer Teams portail pour les développeurs](~/concepts/tdp-configuration.md)
* [Outils du portail Teams développeur](~/concepts/tdp-tools.md)