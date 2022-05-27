---
title: Créer un bot
description: Décrit comment créer des bots dans Microsoft Teams
ms.topic: how-to
keywords: création de bots Teams
ms.localizationpriority: medium
ms.date: 12/07/2018
ms.openlocfilehash: 92d4593290d1332b86b370a49b20daaf43868a51
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/27/2022
ms.locfileid: "65757387"
---
# <a name="create-a-bot"></a>Créer un bot

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Tous les bots créés à l’aide de la Microsoft Bot Framework sont configurés et prêts à fonctionner dans Microsoft Teams.

Pour plus d’informations, consultez [la documentation bot framework](/azure/bot-service/?view=azure-bot-service-3.0&preserve-view=true) pour obtenir des informations générales sur les bots.

## <a name="create-a-bot-for-microsoft-teams"></a>Créer un bot dans Microsoft Teams

**Teams App Studio** est un outil qui peut vous aider à créer votre bot et un package d’application qui fait référence à votre bot. Elle contient également une bibliothèque de contrôle React et des exemples configurables pour les cartes. Pour plus d’informations, consultez [Prise en main de Teams App Studio](~/concepts/build-and-test/app-studio-overview.md). Les étapes qui suivent supposent que vous configurez manuellement votre bot et que vous n’utilisez pas **Teams App Studio** :

1. Créez le bot à l’aide de [Bot Framework](https://dev.botframework.com/bots/new). **Veillez à ajouter Microsoft Teams sous la forme d’un canal à partir de la liste de chaînes proposées après avoir créé votre bot.** N’hésitez pas à réutiliser tout ID d’application Microsoft que vous avez généré si vous avez déjà créé votre package d’application/manifeste.

   ![Page d’inscription de Bot Framework](~/assets/images/bots/bfregister.png)

> [!NOTE]
> Si vous ne souhaitez pas créer votre bot dans Azure, vous **devez** utiliser ce lien pour créer un bot : [Bot Framework](https://dev.botframework.com/bots/new). Si vous cliquez sur **Créer un bot** dans le portail Bot Framework à la place, vous [allez créer votre bot dans Microsoft Azure](#bots-and-microsoft-azure) à la place.

2. Générez le bot à l’aide du package [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet, du [Kit de développement logiciel (SDK) Bot Framework](https://github.com/microsoft/botframework-sdk) ou de l’API [Bot Connector](/bot-framework/rest-api/bot-framework-rest-connector-api-reference).

3. Testez le bot à l’aide de la [Bot Framework Emulator](/bot-framework/debug-bots-emulator).

4. Déployez le bot sur un service cloud, tel que [Microsoft Azure](https://azure.microsoft.com/). Vous pouvez également exécuter votre application localement et utiliser un service de tunneling tel [que ngrok](https://ngrok.com) pour exposer un point de terminaison https:// pour votre bot, tel que `https://45az0eb1.ngrok.io/api/messages`.

> [!NOTE]
>
> ## <a name="bots-and-microsoft-azure"></a>Bots et Microsoft Azure
>
> À compter de décembre 2017, le portail Bot Framework est optimisé pour l’inscription de bots dans Microsoft Azure. Voici quelques opérations que vous pouvez prendre en compte :
>
> * Le canal Microsoft Teams pour les bots inscrits sur Azure est gratuit. Les messages envoyés sur le canal Teams ne sont pas comptabilisés dans les messages consommés pour le bot.
> * Bien qu’il soit possible de [créer un bot Bot Framework](https://dev.botframework.com/bots/new) sans utiliser Azure, vous devez utiliser [créer un bot Bot Framework](https://dev.botframework.com/bots/new), qui n’est plus exposé dans le portail Bot Framework.
> * Lorsque vous modifiez les propriétés d’un bot existant dans la [liste de vos bots dans Bot Framework](https://dev.botframework.com/bots), comme son « point de terminaison de messagerie », ce qui est courant lors du premier développement d’un bot, en particulier si vous utilisez [ngrok](https://ngrok.com), vous verrez la colonne « État de la migration » et un bouton bleu « Migrer » qui vous amènera dans le portail Microsoft Azure. Ne cliquez pas sur le bouton « Migrer », sauf si c’est ce que vous voulez faire ; Cliquez plutôt sur le nom du bot et vous pouvez modifier ses propriétés :</br>
   ![Modifier les propriétés du bot](~/assets/images/bots/bf-migrate-bot-to-azure.png)
> * Si vous inscrivez votre bot à l’aide de Microsoft Azure, votre code de bot n’a pas besoin d’être *hébergé* sur Microsoft Azure.
> * Si vous inscrivez un bot à l’aide de Portail Azure, vous devez disposer d’un compte Microsoft Azure. Vous pouvez [en créer un gratuitement](https://azure.microsoft.com/free/). Pour vérifier votre identité lorsque vous en créez une, vous devez fournir une carte de crédit, mais elle ne sera pas facturée; il est toujours libre de créer et d’utiliser des bots avec Microsoft Teams.
> * Vous pouvez maintenant utiliser App Studio pour inscrire/mettre à jour les informations d’application et de bot directement dans Microsoft Teams. Vous devez uniquement utiliser le Portail Azure pour ajouter ou configurer d’autres canaux Bot Framework tels que Direct Line, Chat Web, Skype et Facebook Messenger.

> [!WARNING]
>* Si vous utilisez App Studio, nous vous recommandons d’essayer le Developer Portal pour configurer, distribuer et gérer vos applications Teams. App Studio sera déconseillé d’ici le 30 juin 2022

## <a name="see-also"></a>Voir aussi

[Exemples Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)
