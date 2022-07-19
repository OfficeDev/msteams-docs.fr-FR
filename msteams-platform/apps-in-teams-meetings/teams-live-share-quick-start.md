---
title: Démarrage rapide de Live Share
author: surbhigupta
description: Dans ce module, découvrez comment essayer rapidement l’exemple Dice Roller
ms.topic: conceptual
ms.localizationpriority: high
ms.author: stevenic
ms.date: 04/07/2022
ms.openlocfilehash: 10bf4b3ce67322c25517d82af2d06a654a4d8668
ms.sourcegitcommit: 79d525c0be309200e930cdd942bc2c753d0b718c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/19/2022
ms.locfileid: "66841784"
---
# <a name="quick-start-guide"></a>Guide de démarrage rapide

Démarrage avec Live Share Kit de développement logiciel (SDK) à l’aide de l’exemple Dice Roller est une évolution du [Démarrage rapide Fluid Framework](https://fluidframework.com/docs/start/quick-start/) et est conçu pour exécuter rapidement un [exemple dice Roller](https://github.com/microsoft/live-share-sdk/tree/main/samples/01.dice-roller) basé sur le SDK Live Share sur l’hôte local de votre ordinateur.

:::image type="content" source="../assets/images/teams-live-share/dice-roller.png" alt-text="Exemple DiceRoller":::

> [!NOTE]
> Ce guide vous guide tout au long de l’utilisation de Live Share localement dans un navigateur. Pour en savoir plus sur l’utilisation du Kit de développement logiciel (SDK) dans une réunion Teams, essayez notre [Didacticiel Agile Poker](../sbs-teams-live-share.yml).

## <a name="set-up-your-development-environment"></a>Configuration de votre environnement de développement

Pour commencer, installez :

* [Node.js](https://nodejs.org/en/download): le Kit de développement logiciel (SDK) Live Share prend en charge Node.js LTS versions 12.17 et ultérieures.
* [Dernière version de Visual Studio Code](https://code.visualstudio.com/).
* [Git](https://git-scm.com/downloads)

## <a name="build-and-run-the-dice-roller-app"></a>Création et exécution de l’application Dice Roller

1. Accédez à l’exemple d’application [Dice Roller](https://github.com/microsoft/live-share-sdk/tree/main/samples/01.dice-roller).

1. Clonez le référentiel [Kit de développement logiciel (SDK) Live Share](https://github.com/microsoft/live-share-sdk) pour tester l’exemple d’application :

    ```bash
    git clone https://github.com/microsoft/live-share-sdk.git
    ```

1. Exécutez la commande suivante pour accéder au dossier de l’exemple d’application Dice Roller :

   ```bash
    cd live-share-sdk\samples\01.dice-roller
   ```

1. Exécutez la commande suivante pour installer le package de dépendance :

    ```bash
    npm install
    ```

1. Exécutez la commande suivante pour démarrer le serveur web local et le client :

   ```bash
   npm start
   ```
  
     Un nouvel onglet de navigateur ouvre une URL `http://localhost:8080` et le jeu Dice Roller s’affiche.

1. Copiez l’URL complète dans le navigateur, y compris l’ID, puis collez-la dans une nouvelle fenêtre ou un autre navigateur.

   Un deuxième client pour votre application Dice Roller s’ouvre.

1. Ouvrez les deux fenêtres, puis sélectionnez le bouton **Roll** dans une fenêtre. L’état des dés change dans les deux clients.

    :::image type="content" source="../assets/images/teams-live-share/dice-roller.png" alt-text="Onglets multiples de Dice Roller":::
  
   **Félicitations**, vous avez appris à créer et exécuter une application à l’aide du Kit de développement logiciel (SDK) Live Share.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Didacticiel Dice Roller](teams-live-share-tutorial.md)

## <a name="see-also"></a>Voir aussi

* [Référentiel GitHub](https://github.com/microsoft/live-share-sdk)
* [ Documents de référence du kit SDK Live Share](/javascript/api/@microsoft/live-share/)
* [Documents de référence du Kit de développement logiciel (SDK) Live Share Media](/javascript/api/@microsoft/live-share-media/)
* [Fonctionnalités de Live Share](teams-live-share-capabilities.md)
* [FAQ sur Live Share](teams-live-share-faq.md)
* [Applications Teams dans les réunions](teams-apps-in-meetings.md)
