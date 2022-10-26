---
title: Utiliser Microsoft Graph pour récupérer les transcriptions d'une réunion Teams
description: Décrit le processus, les scénarios et les API permettant de récupérer les transcriptions dans le scénario post-réunion.
ms.localizationpriority: high
ms.topic: conceptual
ms.openlocfilehash: 4953c5bd77700becb92e71881222eb70fbc401a0
ms.sourcegitcommit: 372aade09e62ac7e5936215173a6632fbb042c9d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/26/2022
ms.locfileid: "68699156"
---
# <a name="get-meeting-transcripts-using-graph-apis"></a>Obtenir des transcriptions de réunion à l'aide des API graphiques

Vous pouvez maintenant configurer votre application pour récupérer les transcriptions des réunions Microsoft Teams dans le scénario post-réunion. Votre application peut utiliser les API REST de Microsoft Graph pour accéder et récupérer les transcriptions générées pour une réunion Teams programmée au préalable.

Voici quelques cas d'utilisation pour récupérer les transcriptions de réunions à l'aide de l'API graphique :

| Cas d’utilisation | Comment les API de Transcript aident... |
| --- | --- |
| Vous devez obtenir des transcriptions pour capturer des informations significatives à partir de plusieurs réunions dans le secteur des ventes. Il est fastidieux et inefficace de garder la trace de toutes les réunions et de récupérer manuellement les notes de réunion. Une fois la réunion terminée, vous devrez examiner les conversations de toutes ces réunions pour obtenir des informations utiles. | L'utilisation des API graphiques dans votre application pour récupérer les transcriptions des réunions permet de récupérer automatiquement les transcriptions de toutes les réunions pertinentes pour votre objectif. Votre application peut recevoir des notifications de réunion, et obtenir la transcription lorsqu'elle est générée après la fin de la réunion. Ces données peuvent ensuite être utilisées pour gagner : <br> • Informations agrégées et analyse des renseignements <br> • Nouvelles pistes et faits marquants <br> • Suivi et résumé des réunions |
| Dans le cadre d'une initiative des RH, vous organisez une séance de brainstorming pour comprendre et améliorer la santé et la productivité des employés. Le fait de devoir continuellement prendre des notes pour fournir un résumé après la réunion peut entraver le flux de pensées, et vous risquez de ne pas saisir toutes les suggestions précieuses. Après la session, vous devrez analyser la discussion afin de recueillir des points de données pour planifier des améliorations. | L'utilisation des API graphiques dans votre application pour récupérer les transcriptions après la réunion vous permet, ainsi qu'aux participants, de vous concentrer pleinement sur la discussion. Le contenu de la transcription de la réunion est disponible pour : <br> • Analyse de l'engagement et du sentiment <br> • Lister les tâches ou les problèmes <br> • Réunions de suivi et notifications |

> [!NOTE]
> À l’avenir, Microsoft pourra exiger que vous ou vos clients payiez des frais supplémentaires en fonction du volume de données accessible via l’API.

Pour récupérer la transcription d'une réunion particulière :

- [Configurer les permissions sur Azure AD pour accéder à la transcription](#configure-permissions-on-azure-ad-to-access-transcript)
- [Obtenir l'ID de la réunion et l'ID de l'organisateur](fetch-id.md)
- [Utiliser les API graphiques pour récupérer les transcriptions](/graph/api/resources/calltranscript)

## <a name="configure-permissions-on-azure-ad-to-access-transcript"></a>Configurer les permissions sur Azure AD pour accéder à la transcription

Votre application doit disposer des autorisations nécessaires pour récupérer les transcriptions. Il peut accéder aux transcriptions d'une réunion Teams et les récupérer en utilisant les autorisations d'application à l'échelle de l'organisation ou les autorisations d'application de consentement spécifique aux ressources (RSC) pour une réunion particulière.

### <a name="use-organization-wide-application-permissions"></a>Utiliser des autorisations d'application à l'échelle de l'organisation

Vous pouvez configurer votre application pour accéder aux transcriptions des réunions à travers le locataire. Dans ce cas, l'organisateur de la réunion n'a pas besoin d'installer votre application dans la conversation de la réunion Teams. Lorsque l'administrateur du locataire autorise les autorisations de l'application à l'échelle de l'organisation, votre application peut lire et accéder aux transcriptions de toutes les réunions du locataire.

Pour plus d'informations sur les autorisations d'application à l'échelle de l'organisation qui peuvent être accordées à votre application, voir [Autorisations de réunion en ligne](/graph/permissions-reference#online-meetings-permissions).

### <a name="use-meeting-specific-rsc-application-permissions"></a>Utiliser les autorisations d'application RSC propres à la réunion

Si vous souhaitez que votre application récupère les transcriptions uniquement pour la réunion Teams où elle est installée, configurez l'autorisation RSC spécifique à la réunion pour votre application. Les utilisateurs autorisés peuvent installer votre application dans le chat de la réunion. Une fois la réunion terminée, votre application peut passer l'appel API pour obtenir la transcription de cette réunion.

Pour plus d'informations sur les autorisations RSC spécifiques aux réunions qui peuvent être accordées à votre application, voir [Autorisation spécifique aux ressources](../rsc/resource-specific-consent.md#resource-specific-permissions-for-a-chat).

Après avoir configuré les autorisations, configurez votre application pour recevoir des notifications de modification pour tous les événements de réunion pertinents. Les notifications contiennent l'ID de la réunion et l'ID de l'organisateur qui permettent d'accéder au contenu de la transcription. Votre application peut récupérer la transcription d'une réunion lorsqu'elle est générée après sa fin. Le contenu de la transcription est disponible sous forme de fichier `.vtt`ou`.docx`.

Pour plus d'informations sur la façon dont votre application peut savoir quand les réunions se terminent, voir [S'abonner aux notifications de changement ](fetch-id.md#subscribe-to-change-notifications)et[ Utiliser la structure Bot pour obtenir l'ID de la réunion et l'ID de l'organisateur](fetch-id.md#use-bot-framework-to-get-meeting-id-and-organizer-id).

> [!NOTE]
> Le processus d'appel des API graphiques pour accéder aux transcriptions et les récupérer reste le même, qu'il s'agisse d'autorisations d'application spécifiques à une réunion du CSR ou d'autorisations d'application à l'échelle de l'organisation. Ces API ne prennent actuellement en charge que les réunions programmées.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Obtenir l'ID de la réunion et l'ID de l'organisateur](fetch-id.md)

## <a name="see-also"></a>Voir aussi

- [API de réunion avancées](../../apps-in-teams-meetings/meeting-apps-apis.md)
