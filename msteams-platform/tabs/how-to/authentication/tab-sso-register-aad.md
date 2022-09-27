---
title: Inscrire votre application d’onglet auprès d’Azure AD
description: Configurez l’authentification unique (SSO) avec Azure AD en configurant l’URI d’ID d’application, l’étendue du jeton d’accès et la pré-autorisation des clients approuvés.
ms.topic: how-to
ms.localizationpriority: high
keywords: onglets d’authentification Teams Microsoft Azure Active Directory (Azure AD) étendue de l’authentification unique du jeton d’accès
ms.openlocfilehash: 92b974840262fedb268aa7c160aa28fc0a33e2cb
ms.sourcegitcommit: c1032ea4f48c4bbf5446798ff7d46d7e6e9f55d2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2022
ms.locfileid: "68027094"
---
# <a name="register-your-tab-app-in-azure-ad"></a>Inscrire votre application d’onglet dans Azure AD

Azure AD fournit un accès à votre application d’onglet en fonction de l’identité Teams de l’utilisateur de l’application. Vous devez inscrire votre application d’onglet auprès d’Azure AD afin que l’utilisateur de l’application qui s’est connecté à Teams puisse avoir accès à votre application d’onglet.

## <a name="enabling-sso-on-azure-ad"></a>Activation de l’authentification unique sur Azure AD

L’inscription de votre application d’onglet dans Azure AD et son activation pour l’authentification unique nécessitent des configurations d’application, telles qu’une génération d’ID d’application, une définition de l’étendue de l’API et la pré-autorisation des ID clients pour les applications approuvées.

:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/register-azure-ad.png" alt-text="Configurer Azure AD pour envoyer un jeton d’accès à l’application cliente Teams":::

Créez une inscription d’application dans Azure AD et exposez son API (web) à l’aide d’étendues (autorisations). Configurez une relation d’approbation entre l’API exposée sur Azure AD et votre application. Il permet au client Teams d’obtenir un jeton d’accès pour le compte de votre application et de l’utilisateur connecté. Vous pouvez ajouter des ID clients pour les applications mobiles, de bureau et web approuvées que vous souhaitez autoriser préalablement.

Vous devrez peut-être également configurer des détails supplémentaires, tels que l’authentification des utilisateurs d’application sur la plateforme ou l’appareil sur lequel vous souhaitez cibler votre application d’onglet.

Les autorisations de l'API Graph au niveau de l'utilisateur sont prises en charge. Il s’agit de l’e-mail, du profil, de offline_access, et d’OpenId. Si vous devez avoir accès à d'autres étendues Microsoft Graph telles que `User.Read` ou `Mail.Read`, consultez [Obtenir un jeton d'accès avec des autorisations Graph](tab-sso-graph-api.md).

La configuration d’Azure AD active l’authentification unique pour votre application d’onglet dans Teams. Elle répond avec un jeton d’accès pour valider l’utilisateur de l’application.

> [!NOTE]
> Le Kit de ressources Microsoft Teams inscrit l’application Azure AD dans un projet d’authentification unique.

### <a name="before-you-register-with-azure-ad"></a>Avant de vous inscrire auprès d’Azure AD

Vous devez d’abord vous informer sur la configuration de l’inscription de votre application sur Azure AD. Assurez-vous que vous êtes prêt à configurer les détails suivants avant d’inscrire votre application :

- **Options à locataire unique ou multilocataire : votre application sera-t-elle** utilisée uniquement dans le locataire Microsoft 365 où elle est inscrite, ou de nombreux locataires Microsoft 365 l’utiliseront-ils ? Les applications écrites pour une entreprise sont généralement à locataire unique. Les applications écrites par un fournisseur de logiciels indépendant et utilisées par de nombreux clients doivent être mutualisées afin que le locataire de chaque client puisse accéder à l’application.
- **URI de l’ID d’application** : il s’agit d’un URI global unique qui identifie l’API web que vous exposez pour l’accès de votre application via des étendues. Il est également appelé URI d’identificateur. L’URI de l’ID d’application inclut l’ID d’application et le sous-domaine où votre application est hébergée. Le nom de domaine de votre application et le nom de domaine que vous inscrivez pour votre application Azure AD doivent être identiques. Actuellement, la prise en charge de plusieurs domaines pour une application est impossible.
- **Étendue** : il s’agit de la permission qu’un utilisateur d’application autorisé ou que votre application peut accorder pour accéder à une ressource exposée par l’API.

> [!NOTE]
>
> - **Applications métier** : votre organisation peut rendre les applications métier disponibles via Microsoft Store. Ces applications sont personnalisées pour votre organisation. Elles sont internes ou spécifiques au sein de votre organisation ou de votre entreprise.
> - **Applications appartenant au client** : l’authentification unique est également prise en charge pour les applications appartenant au client au sein des clients Azure AD B2C.

Pour créer et configurer votre application dans Azure AD pour activer l’authentification unique :

- [Inscrivez et configurez l’application Azure AD](#create-an-app-registration-in-azure-ad)
- [Configurez l’étendue du jeton d’accès.](#configure-scope-for-access-token)
- [Configurez la version du jeton d’accès.](#configure-access-token-version)

## <a name="create-an-app-registration-in-azure-ad"></a>Créer une inscription d’application Azure AD

Inscrivez une nouvelle application dans Azure AD et configurez la location et la plateforme de l’application. Vous allez générer un nouvel ID d’application qui sera mis à jour ultérieurement dans votre fichier manifeste d’application Teams.

### <a name="to-register-a-new-app-in-azure-ad"></a>Pour inscrire une nouvelle application dans Azure AD

1. Ouvrez le [Portail Azure](https://ms.portal.azure.com/) sur votre navigateur web.
   La page du portail Microsoft Azure AD s’ouvre.

2. Sélectionnez l’icône **Inscriptions d'applications**.

   :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/azure-portal.png" alt-text="Page du portail Azure AD.":::

   La page **Inscriptions d'applications** s’affiche.

3. Sélectionnez l’icône **+ Nouvelle inscription**.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/app-registrations.png" alt-text="Nouvelle page d’inscription sur le portail Azure AD.":::

    La page **Inscrire une application** s’affiche.

4. Entrez le nom de l’application que vous souhaitez afficher à l’utilisateur de l’application. Vous pouvez modifier ce nom ultérieurement, si vous le souhaitez.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/register-app.png" alt-text="Page d’inscription d’application sur le portail Azure AD.":::

5. Sélectionnez le type de compte d’utilisateur qui peut accéder à votre application. Vous pouvez choisir entre l’option client unique ou mutualisé, ou un compte Microsoft privé.

    <details>
    <summary><b>Options pour les types de comptes pris en charge</b></summary>

    | Option | Sélectionnez cette option pour... |
    | --- | --- |
    | Comptes dans cet annuaire d’organisation uniquement (Microsoft uniquement, client unique) | Créez une application pour une utilisation uniquement par des utilisateurs (ou des invités) dans votre client. <br> Souvent appelée application métier, cette application est une application à client unique dans la plateforme d'identités Microsoft. |
    | Comptes de tout répertoire organisationnel (n’importe quel répertoire Azure AD, mutualisé) | Permet aux utilisateurs de n’importe quel client Azure AD d’utiliser votre application. Cette option est appropriée si, par exemple, vous créez une application SaaS et que vous envisagez de la mettre à la disposition de plusieurs organisations. <br> Ce type d’application est appelé « application mutualisée » dans la plateforme d'identités Microsoft.|
    | Comptes dans n’importe quel annuaire organisationnel (tout annuaire Azure AD, mutualisé) et comptes Microsoft personnels | Ciblez un large ensemble de clients. <br> En sélectionnant cette option, vous inscrivez une application mutualisée qui peut également aider les utilisateurs d’applications disposant de comptes Microsoft personnels. |
    | Comptes Microsoft personnels uniquement | Créez une application uniquement pour les utilisateurs disposant de comptes Microsoft personnels. |

    </details>

    > [!NOTE]
    > Vous n’avez pas besoin d’entrer **l’URI de redirection** pour activer l’authentification unique pour une application d’onglet.

7. Sélectionnez **Inscrire**.
    Un message s’affiche sur le navigateur indiquant que l’application a été créée.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/app-created-msg.png" alt-text="Inscrire une application sur le portail Azure AD.":::

    La page avec l’ID d’application et d’autres configurations s’affiche.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/tab-app-created.png" alt-text="Inscription de l’application réussite.":::

8. Notez et enregistrez l’ID d’application à partir de **l’ID d’application (client)**. Vous en aurez besoin pour mettre à jour le manifeste de l’application Teams ultérieurement.

    Votre application native est désormais inscrite auprès d'Azure AD. Vous devez maintenant avoir un ID d’application pour votre application d’onglet.

## <a name="configure-scope-for-access-token"></a>Configurer l’étendue du jeton d’accès

Une fois que vous avez créé une inscription d’application, configurez les options d’étendue (autorisation) pour l’envoi d’un jeton d’accès au client Teams et l’autorisation des applications clientes approuvées pour activer l’authentification unique.

Pour configurer l’étendue et autoriser les applications clientes approuvées, vous devez :

- [Pour exposer une API](#to-expose-an-api) : configurez les options d’étendue (autorisation) pour votre application. Vous allez exposer une API web et configurer l’URI de l’ID d’application.
- [Pour configurer l’étendue de l’API](#to-configure-api-scope) : définissez l’étendue de l’API et les utilisateurs qui peuvent donner leur consentement pour une étendue. Vous pouvez autoriser uniquement les administrateurs à donner leur consentement pour des autorisations à privilèges plus élevés.
- [Pour configurer une application cliente autorisée](#to-configure-authorized-client-application) : créez des ID clients autorisés pour les applications que vous souhaitez autoriser préalablement. Cela permet à l’utilisateur de l’application d’accéder aux étendues d’application (autorisations) que vous avez configurées, sans nécessiter de consentement supplémentaire. Autorisez préalablement uniquement les applications clientes auxquelles vous faites confiance, car les utilisateurs de votre application n’auront pas la possibilité de refuser le consentement.

### <a name="to-expose-an-api"></a>Pour exposer une API

1. Sélectionnez **Gérer** > **Exposer une API** dans le volet gauche.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/expose-api-menu.png" alt-text="Exposer une option de menu API.":::

    La page **Exposer une API** s’affiche.

1. Sélectionnez **Définir** pour générer l'URI de l'ID d'application sous la forme de`api://{AppID}`.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/expose-an-api.png" alt-text="Définir l’URI de l’ID d’application":::

    La section relative à la définition de l’URI de l’ID d’application s’affiche.

1. Entrez l’URI de l’ID d’application au format expliqué ici.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/set-app-id-uri.png" alt-text="URI de l’ID d’application":::

    - **L’URI de l’ID d’application** est prérempli avec l’ID d’application (GUID) au format `api://{AppID}`.
    - Le format d’URI de l’ID d’application doit être : `api://fully-qualified-domain-name.com/{AppID}`.
    - Insérez le `fully-qualified-domain-name.com` entre `api://` et `{AppID}` (autrement dit, le GUID). Par exemple, api://example.com/{AppID}.

    où,
    - `fully-qualified-domain-name.com` est le nom de domaine lisible par l’utilisateur à partir duquel votre application d’onglet est traitée. Le nom de domaine de votre application et le nom de domaine que vous inscrivez pour votre application Azure AD doivent être identiques.

      Si vous utilisez un service de tunneling tel que ngrok, vous devez mettre à jour cette valeur chaque fois que votre sous-domaine ngrok change.
    - `AppID` est l’ID d’application (GUID) qui a été généré lors de l’inscription de votre application. Vous pouvez l’afficher dans la section **Vue d’ensemble**.

    > [!IMPORTANT]
    >
    > - **URI de l’ID d’application pour l’application avec plusieurs fonctionnalités** : si vous créez une application avec un bot, une extension de messagerie et un onglet, entrez l’URI de l’ID d’application `api://fully-qualified-domain-name.com/BotId-{YourClientId}`, où BotID est votre ID d’application bot.
    >
    > - **Format du nom de domaine** : utilisez des lettres minuscules pour le nom de domaine. N’utilisez pas de majuscules.
    >
    >   Par exemple, pour créer un service d’application ou une application web avec le nom de la ressource « demoapplication » :
    >
    >   | Si le nom de la ressource de base utilisé est | l’URL sera... | Le format est pris en charge dans... |
    >   | --- | --- | --- |
    >   | *demoapplication* | `https://demoapplication.example.net` | Toutes les plateformes.|
    >   | *DemoApplication* | `https://DemoApplication.example.net` | Bureau, web et iOS uniquement. Ce n’est pas pris en charge sur Android. |
    >
    >    Utilisez l’option en minuscules *demoapplication* comme nom de la ressource de base.

1. Sélectionnez **Enregistrer**.

    Un message s’affiche sur le navigateur indiquant que l’URI de l’ID d’application a été mis à jour.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/app-id-uri-msg.png" alt-text="Message d’URI de l’ID d’application":::

    L’URI d’ID d’application apparaît sur la page.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/app-id-uri-added.png" alt-text="URI de l’ID d’application mis à jour":::

1. Notez et enregistrez l’URI de l’ID d’application. Vous en aurez besoin pour mettre à jour le manifeste de l’application Teams ultérieurement.

### <a name="to-configure-api-scope"></a>Pour configurer l’étendue de l’API

1. Sélectionnez **+ Ajouter une étendue** dans les **étendues définies par cette section d’API**.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/select-scope.png" alt-text="Sélectionnez l’étendue":::

    La page **Ajouter une étendue** s’affiche.

1. Entrez les détails de la configuration de l’étendue.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/add-scope.png" alt-text="Ajouter des détails d’étendue":::

    1. Entrez le nom de l’étendue. Ce champ est obligatoire.
    2. Sélectionnez l’utilisateur qui peut donner son consentement pour cette étendue. L’option par défaut est **Admins uniquement**.
    3. Entrez le **nom d’affichage du consentement de l’administrateur**. Ce champ est obligatoire.
    4. Entrez la description du consentement de l’administrateur. Ce champ est obligatoire.
    5. Entrez le **nom d’affichage du consentement de l’utilisateur**.
    6. Entrez la description du consentement de l’utilisateur.
    7. Sélectionnez l’option **Activé** pour l’état.
    8. Sélectionnez **Ajouter une étendue**.

    Un message s’affiche sur le navigateur indiquant que l’étendue a été ajoutée.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/scope-added-msg.png" alt-text="Message d’étendue ajoutée":::

    La nouvelle étendue que vous avez définie s’affiche sur la page.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/scope-added.png" alt-text="Étendue ajoutée et affichée":::

### <a name="to-configure-authorized-client-application"></a>Pour configurer une application cliente autorisée

1. Parcourez la page **Exposer une API** dans la section **Application cliente autorisée**, puis sélectionnez **+ Ajouter une application cliente**.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/auth-client-apps.png" alt-text="Application cliente autorisée":::

    La page **Ajouter une application cliente** s’affiche.

1. Entrez l’ID client Microsoft 365 approprié pour le client Teams pour les applications que vous souhaitez autoriser pour l’application web de votre application.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/add-client-app.png" alt-text="Ajouter une application cliente":::

    > [!NOTE]
    >
    > - Les ID clients Microsoft 365 pour les applications mobiles, de bureau et web pour Teams, Office et Outlook sont les ID réels que vous devez ajouter.
    > - Pour une application d’onglet Teams, vous avez besoin d’une application web ou SPA, car vous ne pouvez pas avoir d’application cliente mobile ou de bureau dans Teams.

    1. Choisissez un des ID suivants :

       | Utiliser l’ID client | Pour autoriser... |
       | --- | --- |
       | 1fec8e78-bce4-4aaf-ab1b-5451cc387264 | Application Teams mobile ou de bureau |
       | 5e3ce6c0-2b1f-4285-8d4b-75ee78787346 | Application Teams web |
       | 4765445b-32c6-49b0-83e6-1d93765276ca | Application web Office |
       | 0ec893e0-5785-4de6-99da-4ed124e5296c | Application de bureau Office |
       | d3590ed6-52b3-4102-aeff-aad2292ab01c | Bureau Outlook, application mobile |
       | bc59ab01-8403-45c6-8796-ac3ef710b3e3 | Application web Outlook |

    1. Sélectionnez l’URI de l’ID d’application que vous avez créé pour votre application dans **Étendues autorisées** pour ajouter l’étendue à l’API web que vous avez exposée.

    1. Sélectionnez **Ajouter une application**.

    Un message s’affiche sur le navigateur indiquant que l’application cliente autorisée a été ajoutée.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/update-app-auth-msg.png" alt-text="Message d’ajout de l’application cliente":::

    L’ID client apparaît sur la page.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/client-app-added.png" alt-text="Application cliente ajoutée et affichée":::

> [!NOTE]
> Vous pouvez autoriser plusieurs applications clientes. Répétez les étapes de cette procédure pour configurer une autre application cliente autorisée.

## <a name="configure-access-token-version"></a>Configurer la version du jeton d’accès

Vous devez définir la version du jeton d’accès acceptable pour votre application. Cette configuration est effectuée dans le manifeste de l’application Azure AD.

### <a name="to-define-the-access-token-version"></a>Pour définir la version du jeton d’accès

1. Sélectionnez **Gérer** > **Manifeste** dans le volet gauche.

   :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/azure-portal-manifest.png" alt-text="Manifeste du portail Azure AD":::

    Le manifeste de l’application Azure AD s’affiche.

1. Entrez **2** comme valeur pour la propriété `accessTokenAcceptedVersion`.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/azure-manifest-value.png" alt-text="Valeur de la version du jeton d’accès accepté":::

1. Sélectionnez **Enregistrer**.

    Un message s’affiche sur le navigateur indiquant que le manifeste a été mis à jour avec succès.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/update-aad-manifest-msg.png" alt-text="Message de mise à jour du manifeste":::

Félicitations ! Vous avez terminé la configuration de l’application dans Azure AD requise pour activer l’authentification unique pour votre application d’onglet.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Configurer le code pour activer l’authentification unique](tab-sso-code.md)

## <a name="see-also"></a>Voir aussi

- [Clients dans Azure Active Directory](/azure/active-directory/develop/single-and-multi-tenant-apps)
- [Étendre l’application d’onglet avec des autorisations et une étendue Microsoft Graph](tab-sso-graph-api.md)
- [Démarrage rapide : inscrire une application sur la plateforme d’identités Microsoft](/azure/active-directory/develop/quickstart-register-app)
- [Démarrage rapide : configurer une application pour exposer une API web](/azure/active-directory/develop/quickstart-configure-app-expose-web-apis)
- [Flux de code d’autorisation OAuth 2.0](/azure/active-directory/develop/v2-oauth2-auth-code-flow)
