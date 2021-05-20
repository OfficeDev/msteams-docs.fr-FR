---
title: Créer un bot
description: Décrit comment créer des bots dans Microsoft Teams
ms.topic: how-to
keywords: équipes bots création
localization_priority: Normal
ms.date: 12/07/2018
ms.openlocfilehash: 67aa3e2cfd1950dced84785a9f6f35cfd4d5ff85
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566774"
---
# <a name="create-a-bot"></a>Créer un bot

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Tous les bots créés à l’aide Microsoft Bot Framework sont configurés et prêts à fonctionner dans Microsoft Teams.

Pour plus d’informations, consultez [bot framework documentation pour](/azure/bot-service/?view=azure-bot-service-3.0&preserve-view=true) plus d’informations générales sur les bots.

## <a name="create-a-bot-for-microsoft-teams"></a>Créer un bot dans Microsoft Teams

**Teams App Studio est** un outil qui peut aider à créer votre bot, et un paquet d’applications qui fait référence à votre bot. Elle contient également une bibliothèque de contrôle React et des exemples configurables pour les cartes. Pour plus d’informations, [voir Getting started with Teams App Studio](~/concepts/build-and-test/app-studio-overview.md). Les étapes qui suivent supposent que vous configurez votre bot à la main et que vous **n’utilisez pas Teams App Studio**:

1. Créer le bot en utilisant ce lien: https://dev.botframework.com/bots/new . **Veillez à ajouter Microsoft Teams sous la forme d’un canal à partir de la liste de chaînes proposées après avoir créé votre bot.** N’hésitez pas à réutiliser tout ID d’application Microsoft que vous avez généré si vous avez déjà créé votre package d’application/manifeste.

   ![Page d’inscription de Bot Framework](~/assets/images/bots/bfregister.png)

> [!NOTE]
> Si vous ne souhaitez pas créer votre bot dans Azure, vous **devez** utiliser ce lien pour créer un nouveau bot : https://dev.botframework.com/bots/new . Si vous cliquez sur le **créer un bot dans le** portail Bot Framework à la place, vous allez créer votre bot dans Microsoft Azure [place.](#bots-and-microsoft-azure)

2. Construisez le bot à [l’aide du package Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet, [du Bot Framework SDK](https://github.com/microsoft/botframework-sdk)ou de [l’API Bot Connector](/bot-framework/rest-api/bot-framework-rest-connector-api-reference).

3. Testez le bot à [l’aide de la Bot Framework Emulator](/bot-framework/debug-bots-emulator).

4. Déployez le bot sur un service cloud, tel [que Microsoft Azure](https://azure.microsoft.com/). Alternativement, exécutez votre application localement et utilisez un service de tunneling [tel ngrok](https://ngrok.com) pour exposer un https:// point final pour votre bot, tels que `https://45az0eb1.ngrok.io/api/messages` .

> [!NOTE]
> ## <a name="bots-and-microsoft-azure"></a>Bots et Microsoft Azure
> Depuis décembre 2017, le portail Bot Framework est optimisé pour l’enregistrement des bots en Microsoft Azure. Voici quelques opérations que vous pouvez prendre en compte :
>
> * Le canal Microsoft Teams pour les bots inscrits sur Azure est gratuit. Les messages envoyés sur Teams canal ne compteront pas pour les messages consommés pour le bot.
> * Bien qu’il soit possible [de créer un nouveau bot Bot Framework sans](https://dev.botframework.com/bots/new) utiliser Azure, vous devez utiliser cette URL ( , qui https://dev.botframework.com/bots/new) n’est plus exposée dans le portail Bot Framework.
> * Lorsque vous modifiez les propriétés d’un bot existant dans la [liste de vos bots dans Bot Framework](https://dev.botframework.com/bots) tels que son « point de terminaison de messagerie », qui est commun lors du développement d’abord un bot, surtout si vous utilisez [ngrok](https://ngrok.com), vous verrez « Statut de migration » colonne et un bleu « Migrer » bouton qui vous emmènera dans le portail Microsoft Azure. Ne cliquez pas sur le bouton « Migrer » sauf si c’est ce que vous voulez faire; au lieu de cela, cliquez sur le nom du bot et vous pouvez modifier ses propriétés:</br>
   ![Modifier les propriétés du bot](~/assets/images/bots/bf-migrate-bot-to-azure.png)
> * Si vous enregistrez votre bot à l’Microsoft Azure, votre code bot n’a pas besoin *d’être* hébergé Microsoft Azure.
> * Si vous inscrivez un bot à l’aide du Portail Microsoft Azure, vous devez disposer d’un compte Microsoft Azure. Vous pouvez [en créer un gratuitement](https://azure.microsoft.com/free/). Pour vérifier votre identité lorsque vous en créez une, vous devez fournir une carte de crédit, mais elle ne sera pas débitée; il est toujours libre de créer et d’utiliser des bots avec Microsoft Teams.
> * Vous pouvez maintenant utiliser App Studio pour enregistrer/mettre à jour les informations sur les applications et les bots directement dans Microsoft Teams. Vous n’aurez qu’à utiliser le portail Microsoft Azure pour ajouter ou configurer d’autres canaux Bot Framework tels que Direct Line, Web Chat, Skype et Facebook Messenger.

## <a name="see-also"></a>Voir aussi

[Échantillons bot framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).