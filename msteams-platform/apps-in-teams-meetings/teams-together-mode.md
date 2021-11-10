---
title: Scènes personnalisées en mode ensemble
description: Travailler avec des scènes personnalisées du mode Ensemble
ms.topic: conceptual
ms.localizationpriority: none
ms.openlocfilehash: 051924aa8a8f02c6e9a075639014e4fc3290d8c0
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/10/2021
ms.locfileid: "60887629"
---
# <a name="custom-together-mode-scenes-in-teams"></a>Scènes personnalisées en mode Ensemble dans Teams

Les scènes personnalisées en mode ensemble Microsoft Teams un environnement de réunion immersif et attrayant avec les actions suivantes :

* Rassemblez les personnes et encouragez-les à activer leur vidéo. 
* Combinez numériquement les participants dans une scène virtuelle unique. 
* Placez les flux vidéo des participants dans des sièges pré-déterminés conçus et corrigés par le créateur de scène.

> [!VIDEO https://www.youtube-nocookie.com/embed/MGsNmYKgeTA]

Dans les scènes personnalisées du mode Ensemble, la scène est un artefact. La scène est créée par le développeur de scène à l’aide de Microsoft Scene studio. Dans un paramètre de scène en cours, les participants ont des sièges avec des flux vidéo. Les vidéos sont restituer dans ces sièges. Les applications de scène uniquement sont recommandées, car l’expérience pour ces applications est claire.

Le processus suivant donne une vue d’ensemble pour créer une application de scène uniquement :

:::image type="content" source="../assets/images/apps-in-meetings/create-together-mode-scene-flow.png" alt-text="Créer une application de scène uniquement" border="false":::

Une application de scène uniquement est toujours une application dans Microsoft Teams. Le studio Scene gère la création de package d’application en arrière-plan. Plusieurs scènes d’un package d’application unique s’affichent sous la forme d’une liste plate pour les utilisateurs.

> [!NOTE]
> Les utilisateurs ne peuvent pas lancer le mode Ensemble à partir d’un appareil mobile. Toutefois, une fois qu’un utilisateur rejoint une réunion via mobile et le mode Ensemble est allumé à partir du bureau, les utilisateurs mobiles qui ont allumé la vidéo apparaissent en mode Ensemble sur le bureau. 

## <a name="prerequisites"></a>Configuration requise

Vous devez avoir une connaissance de base des éléments suivants pour utiliser des scènes personnalisées du mode Ensemble :

* Définir une scène et des sièges dans une scène.
* Vous avez un compte de développeur Microsoft et familiarisez-vous avec le portail Microsoft Teams [développeur et](../concepts/build-and-test/teams-developer-portal.md) App Studio.
* Comprendre le [concept de chargement de version de version d’application.](../concepts/deploy-and-publish/apps-upload.md)
* Assurez-vous que l’administrateur a accordé l’autorisation [**Télécharger**](../concepts/deploy-and-publish/apps-upload.md) une application personnalisée et de sélectionner tous les filtres dans le cadre de la configuration de l’application et des stratégies de réunion, respectivement.

## <a name="best-practices"></a>Meilleures pratiques

Prenons les pratiques suivantes pour une expérience de création de scène :

* Assurez-vous que toutes les images sont au format PNG.
* Assurez-vous que le package final avec toutes les images rassemblées ne doit pas dépasser la résolution 1920x1080. La résolution est un nombre even. Cette résolution est une condition requise pour que les scènes soient affichées correctement.
* Assurez-vous que la taille de scène maximale est de 10 Mo.
* Assurez-vous que la taille maximale de chaque image est de 5 Mo. Une scène est une collection de plusieurs images. La limite est pour chaque image individuelle.
* Veillez à sélectionner **Transparent** selon les besoins. Cette case à cocher est disponible dans le panneau droit lorsqu’une image est sélectionnée. Les images qui se chevauchent doivent être marquées comme **transparentes** pour indiquer qu’elles se chevauchent dans la scène.

## <a name="build-a-scene-using-the-scene-studio"></a>Créer une scène à l’aide de Scene studio

Microsoft dispose d’un studio de scène qui vous permet de créer des scènes. Il est disponible sur [l’éditeur de scènes - Teams portail du développeur.](https://dev.teams.microsoft.com/scenes) Ce document fait référence à Scene studio dans le portail Microsoft Teams développeur. L’interface et les fonctionnalités sont identiques dans Le Concepteur de scène App Studio.

Une scène dans le contexte du studio de scène est un artefact qui contient les éléments suivants :

* Sièges réservés aux organisateurs et présentateurs de réunion. Le présentateur ne fait pas référence à l’utilisateur qui partage activement. Il fait référence au rôle [de réunion.](https://support.microsoft.com/en-us/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)

* Siège et image pour chaque participant avec une largeur et une hauteur réglables. Seul le format PNG est pris en charge pour l’image.

* Coordonnées XYZ de tous les sièges et images.

* Collection d’images qui sont en tant qu’une seule image.

L’image suivante montre chaque siège représenté en tant qu’avatar pour la création des scènes :

![Studio de scène](../assets/images/apps-in-meetings/scene-design-studio.png)

**Pour créer une scène à l’aide de Scene studio**

1. Go to [Scenes Editor - Teams Developer Portal](https://dev.teams.microsoft.com/scenes).

    Vous pouvez également ouvrir Scene studio sur la page d’accueil du [portail Teams développeur](https://dev.teams.microsoft.com/home):
    * Sélectionnez **Créer des scènes personnalisées pour les réunions.**
    * Sélectionnez **Outils** dans la section de gauche, puis **Scene studio dans** la section **Outils.**

1. Dans **l’Éditeur de** scènes, **sélectionnez Créer une scène.**

1. Dans **le nom de** la scène, entrez un nom pour la scène.

    * Vous pouvez sélectionner **Fermer** pour faire bascule entre la fermeture ou la réouverture du volet droit.
    * Vous pouvez effectuer un zoom avant ou arrière de la scène à l’aide de la barre de zoom pour une meilleure vue de la scène.

1. Sélectionnez **Ajouter des images** pour ajouter l’image dans l’environnement :

    ![Ajouter des images dans l’environnement](../assets/images/apps-in-meetings/addimages.png)

    >[!NOTE]
    > * Vous pouvez télécharger les [ fichiersSampleScene.zip](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform/apps-in-teams-meetings/SampleScene.zip) et [SampleApp.zip](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform/apps-in-teams-meetings/SampleApp.zip) avec les images.

1. Sélectionnez l’image que vous avez ajoutée.

1. Dans le volet droit, sélectionnez un alignement pour l’image ou utilisez **Resize** pour ajuster la taille de l’image :

    ![Alignement des images](../assets/images/apps-in-meetings/image-alignment.png)

1. Sélectionnez une zone en dehors de l’image.

1. Dans le coin supérieur droit, sélectionnez **Participants** sous **Calques.**

1. Sélectionnez le nombre de participants pour la scène dans la zone Nombre **de participants,** puis sélectionnez **Ajouter**. Une fois la scène livrée, les emplacements d’avatar sont remplacés par les flux vidéo du participant réel. Vous pouvez faire glisser les images des participants autour de la scène et les placer à la position requise. Vous pouvez les re tailler à l’aide de la flèche de re resize.

1. Sélectionnez n’importe quelle image de participant, puis **sélectionnez Affecter** une place pour affecter la place au participant.

1. Sélectionnez **le rôle Organisateur** de réunion ou **Présentateur** pour le participant. Au cours d’une réunion, un participant doit avoir le rôle d’organisateur de la réunion :

    ![Affecter un emplacement](../assets/images/apps-in-meetings/assign-spot.png)

1. Sélectionnez **Enregistrer** et **sélectionner Afficher dans Teams** pour tester rapidement votre scène dans Microsoft Teams.

    * La sélection **de l’affichage Teams** crée automatiquement une application Microsoft Teams qui peut être vue dans la page Applications du portail Teams développeur. 
    * La sélection **de l’affichage Teams** crée automatiquement un package d’application qui est appmanifest.json derrière la scène. Vous pouvez accéder aux  **applications à** partir du menu et accéder au package d’application créé automatiquement.
    * Pour supprimer une scène que vous avez créée, **sélectionnez Supprimer la scène** dans la barre supérieure.

1. In **View in Teams**, select Preview in **Teams**.
1. Dans la boîte de dialogue qui s’affiche, sélectionnez **Ajouter.**

    La scène est testée ou accessible en créant une réunion de test et en lançant des scènes personnalisées du mode Ensemble. Pour plus d’informations, voir [activer des scènes personnalisées du mode Ensemble](#activate-custom-together-mode-scenes):

    ![Lancer des scènes personnalisées du mode Ensemble](../assets/images/apps-in-meetings/launchtogethermode.png)

    La scène peut ensuite être vue dans la galerie personnalisée des scènes du mode Ensemble.

Si vous le souhaitez, vous pouvez sélectionner **Partager** **dans** le menu déroulant Enregistrer. Vous pouvez créer un lien partageable pour distribuer vos scènes à d’autres personnes. L’utilisateur peut ouvrir le lien pour installer la scène et commencer à l’utiliser.

Après la prévisualisation, la scène est livrée en tant qu’application Teams en suivant les étapes de soumission de l’application. Cette étape nécessite le package d’application. Le package d’application est différent du package de scène, pour la scène qui a été conçue. Le package d’application créé automatiquement se trouve dans la section **Applications** du Teams développeur.

Le package de scène est éventuellement récupéré  en sélectionnant **Exporter** dans le menu déroulant Enregistrer. Un **.zip** de scène, c’est-à-dire le package de scène, est téléchargé. Le package de scène inclut un scene.json et les ressources PNG utilisées pour créer une scène. Le package de scène est examiné pour l’incorporation d’autres modifications :

![Exporter une scène](../assets/images/apps-in-meetings/build-a-scene.png)

Une scène complexe qui utilise l’axe Z est illustré dans l’exemple de mise en marche pas à pas.

## <a name="sample-scenejson"></a>Exemple scene.json

Scene.json et les images indiquent la position exacte des sièges. Une scène se compose d’images bitmap, de sprites et de rectangles dans lequel placer les vidéos des participants. Ces sprites et zones de participants sont définis dans un système de coordonnées du monde. L’axe X pointe vers la droite et l’axe Y pointe vers le bas.

Les scènes personnalisées en mode ensemble prise en charge le zoom avant sur les participants actuels. Cette fonctionnalité est utile pour les petites réunions dans une grande scène. Un sprite est une image bitmap statique positionnée dans le monde. La valeur Z du sprite détermine la position du sprite. Le rendu commence par le sprite avec la valeur Z la plus faible, donc une valeur Z plus élevée signifie qu’il est plus proche de la caméra. Chaque participant possède son propre flux vidéo, qui est segmenté afin que seul le premier plan soit rendu.

Le code suivant est l’exemple scene.json :

```json
{
   "protocolVersion": "1.0",
   "id": "A",
   "autoZoom": true,
   "mirrorParticipants ": true,
   "extent":{
      "left":0.0,
      "top":0.0,
      "width":16.0,
      "height":9.0
   },
   "sprites":[
      {
         "filename":"background.png",
         "cx":8.0,
         "cy":4.5,
         "width":16.0,
         "height":9.0,
         "zOrder":0.0,
   "isAlpha":false
      },
      {
         "filename":"table.png",
         "cx":8.0,
         "cy":7.0,
         "width":12.0,
         "height":4.0,
         "zOrder":3.0,
   "isAlpha":true
      },
      {
         "filename":"row0.png",
         "cx":12.0,
         "cy":15.0,
         "width":8.0,
         "height":4.0,
         "zOrder":2.0,
   "isAlpha":true
      }

   ],
   "participants":[
      {
         "cx":5.0,
         "cy":4.0,
         "width":4.0,
         "height":2.25,
         "zOrder":1.0,
         "seatingOrder":0
      },
      {
         "cx":11.0,
         "cy":4.0,
         "width":4.0,
         "height":2.25,
         "zOrder":1.0,
         "seatingOrder":1
      }
   ]
}
```

Chaque scène possède un ID et un nom uniques. Le JSON de scène contient également des informations sur toutes les ressources utilisées pour la scène. Chaque bien contient un nom de fichier, une largeur, une hauteur et une position sur les axes X et Y. De même, chaque siège contient un ID de siège, sa largeur, sa hauteur et sa position sur les axes X et Y. L’ordre d’altération est généré automatiquement et modifié selon les préférences. Le numéro de l’ordre d’appel correspond à l’ordre des personnes qui rejoignent l’appel.

Représente `zOrder` l’ordre de placement des images et des sièges le long de l’axe Z. Elle donne une idée de profondeur ou de partition si nécessaire. Consultez l’exemple de mise en place pas à pas. L’exemple utilise `zOrder` le .

Maintenant que vous avez passé par l’exemple scene.json, vous pouvez activer les scènes personnalisées du mode Ensemble pour vous engager dans des scènes.

## <a name="activate-custom-together-mode-scenes"></a>Activer des scènes personnalisées du mode Ensemble

Obtenez plus d’informations sur la façon dont un utilisateur s’engage avec des scènes dans des scènes personnalisées du mode Ensemble.

**Pour sélectionner des scènes et activer des scènes personnalisées en mode Ensemble**

1. Créez une réunion de test.

    >[!NOTE]
    > Lors de la sélection **de l’aperçu** dans Le studio de scène, la scène est installée en tant qu’application dans Microsoft Teams. Il s’agit du modèle pour qu’un développeur teste et teste des scènes à partir du studio Scene studio. Une fois qu’une scène est livrée en tant qu’application, les utilisateurs voient ces scènes dans la galerie de scène.

1. Dans la **page de la** galerie dans le coin supérieur gauche, sélectionnez Mode **Ensemble.** La **boîte de dialogue s’affiche** et la scène ajoutée est disponible.

1. Sélectionnez **Modifier la scène** pour modifier la scène par défaut.

1. Dans la **galerie de scène,** sélectionnez la scène que vous souhaitez utiliser pour votre réunion.

    L’organisateur et le présentateur de la réunion peuvent éventuellement modifier **la scène pour tous** les participants à la réunion.

    >[!NOTE]
    > À tout moment, une seule scène est utilisée de manière homogène pour la réunion. Si un présentateur ou un organisateur modifie une scène, elle change pour tout. Le basculement dans ou hors des scènes personnalisées du mode Ensemble est la responsabilité des participants individuels, mais dans les scènes personnalisées du mode Ensemble, tous les participants ont la même scène.

1. Sélectionnez **Appliquer**. Teams installe l’application pour l’utilisateur et applique la scène.

## <a name="open-a-custom-together-mode-scenes-scene-package"></a>Ouvrir un package de scène de scène en mode ensemble personnalisé

Vous pouvez partager le package de scène qui est un fichier .zip extrait du studio scene studio à d’autres créateurs pour améliorer davantage la scène. La **fonctionnalité Importer une** scène permet de déballer un package de scène pour laisser le créateur continuer à créer la scène.

![Fichier zip de scène](../assets/images/apps-in-meetings/scene-zip-file.png)

## <a name="see-also"></a>Voir aussi

[Applications pour Teams réunions](teams-apps-in-meetings.md) 
 [Bots d’appels et de réunions](~/bots/calls-and-meetings/calls-meetings-bots-overview.md) 
 [Appels et réunions multimédias en temps réel avec Microsoft Teams](~/bots/calls-and-meetings/real-time-media-concepts.md)
