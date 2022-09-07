---
title: Tester le comportement de l’application dans un environnement différent
author: surbhigupta
description: Dans ce module, découvrez comment tester le comportement de l’application dans un environnement différent
ms.author: v-amprasad
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/03/2022
ms.openlocfilehash: 187219fec76830119e795d1dd60a36b2374c65ac
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/07/2022
ms.locfileid: "67617221"
---
# <a name="test-app-behavior-in-different-environment"></a>Tester le comportement de l’application dans un environnement différent

Vous pouvez tester votre application Teams après l’intégration à Microsoft Teams. Pour tester votre application Teams, vous devez créer au moins un espace de travail dans votre environnement. Vous pouvez utiliser le Kit de ressources Teams pour tester votre application Teams :

* **Hébergé localement dans Teams** : Le Kit de ressources Teams héberge localement votre application Teams en la chargeant dans Teams à des fins de test dans un environnement local.

* **Hébergé dans le cloud dans Teams** : pour tester votre application Teams à distance, vous devez l’héberger dans le cloud à l’aide de l’approvisionnement et du déploiement sur Microsoft Azure Active Directory (Azure AD). Cela implique le chargement de votre solution dans Azure AD, puis le chargement dans Teams.

> [!NOTE]
> Pour le débogage et le test à l’échelle de la production, nous vous recommandons de suivre les instructions de votre propre entreprise pour vous assurer que vous êtes en mesure de prendre en charge les tests, la mise en lots et le déploiement par le biais de vos propres processus.

## <a name="locally-hosted-environment"></a>Environnement hébergé localement

Teams est un produit cloud qui exige que tous les services auxquels il accède soient disponibles publiquement à l’aide de points de terminaison HTTPS. L’hébergement local concerne le chargement indépendant dans Teams à des fins de test dans l’environnement local.

> [!NOTE]
> Bien que vous puissiez utiliser n’importe quel outil de votre choix pour le test, nous vous recommandons [d’utiliser ngrok](https://ngrok.com/download)

## <a name="cloud-hosted-environment"></a>Environnement hébergé dans le cloud

Pour héberger votre code de développement et de production et leurs points de terminaison HTTPS, vous devez tester à distance votre application Teams à l’aide du provisionnement et du déploiement sur Azure AD. Vous devez vous assurer que tous les domaines sont accessibles à partir de votre application Teams répertoriée dans l’objet [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) dans le `manifest.jason` fichier

> [!NOTE]
> Pour garantir un environnement sécurisé, soyez explicite sur le domaine et les sous-domaines exacts que vous référencez, et ces domaines doivent être sous votre contrôle. Par exemple, `*.azurewebsites.net` n’est pas recommandé, mais `contoso.azurewebsites.net` est recommandé.

## <a name="see-also"></a>Voir aussi

* [Déboguer votre application Microsoft Teams localement](debug-local.md)
* [Processus de débogage en arrière-plan](debug-background-process.md)
* [Utiliser Teams Shared Computer Toolkit pour mettre en service des ressources cloud](provision.md)
* [Déployer à partir du cloud](deploy.md)
* [Prévisualiser et personnaliser le manifeste de l'application Teams](TeamsFx-preview-and-customize-app-manifest.md)
* [Gérer plusieurs environnements](TeamsFx-multi-env.md)
