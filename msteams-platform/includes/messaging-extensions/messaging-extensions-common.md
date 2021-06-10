## <a name="add-a-messaging-extension-to-your-app"></a>Ajouter une extension de messagerie à votre application

Une extension de messagerie est un service hébergé dans le cloud qui écoute les demandes des utilisateurs et répond avec des données structurées, telles qu’une [carte.](~/task-modules-and-cards/what-are-cards.md) Vous intégrez votre service à Microsoft Teams via des objets Bot `Activity` Framework. Nos extensions .NET et Node.js pour le SDK Bot Builder peuvent vous aider à ajouter des fonctionnalités d’extension de messagerie à votre application.

![Diagramme du flux de messages pour les extensions de messagerie](~/assets/images/compose-extensions/ceflow.png)

### <a name="register-in-the-bot-framework"></a>S’inscrire dans Bot Framework

Si ce n’est pas déjà fait, vous devez d’abord inscrire un bot auprès du Microsoft Bot Framework. L’ID d’application Microsoft et les points de terminaison de rappel pour votre bot, tels que définis ici, seront utilisés dans votre extension de messagerie pour recevoir et répondre aux demandes des utilisateurs. N’oubliez pas d’activer Microsoft Teams canal de recherche pour votre bot.

Enregistrez votre ID d’application de bot et votre mot de passe d’application. Vous devez fournir l’ID de l’application dans le manifeste de votre application.

### <a name="update-your-app-manifest"></a>Mettre à jour le manifeste de votre application

Comme avec les bots et [](~/resources/schema/manifest-schema.md#composeextensions) les onglets, vous mettez à jour le manifeste de votre application pour inclure les propriétés d’extension de messagerie. Ces propriétés régissent l’apparition et le comportement de votre extension de messagerie dans le client Microsoft Teams messagerie. Les extensions de messagerie sont pris en charge à partir de la v1.0 du manifeste.

#### <a name="declare-your-messaging-extension"></a>Déclarer votre extension de messagerie

Pour ajouter une extension de messagerie, incluez une nouvelle structure JSON de niveau supérieur dans votre manifeste avec la `composeExtensions` propriété. Actuellement, vous êtes limité à la création d’une extension de messagerie unique pour votre application.

> [!NOTE]
> Le manifeste fait référence aux extensions de messagerie comme `composeExtensions` . Il s’agit de maintenir la compatibilité ascendante.

La définition d’extension est un objet qui a la structure suivante :

| Nom de la propriété | Objectif | Obligatoire ? |
|---|---|---|
| `botId` | ID d’application Microsoft unique pour le bot inscrit dans le Bot Framework. Il doit généralement être identique à l’ID de votre application Teams globale. | Oui |
| `scopes` | Tableau déclarant si cette extension peut être ajoutée à ou `personal` à des `team` étendues (ou les deux). | Oui |
| `canUpdateConfiguration` | Active **Paramètres’élément** de menu. | Non |
| `commands` | Tableau de commandes pris en charge par cette extension de messagerie. Vous êtes limité à 10 commandes. | Oui |

#### <a name="define-commands"></a>Définir des commandes

Votre extension de messagerie doit déclarer une commande, qui s’affiche lorsque l’utilisateur sélectionne votre application à partir du bouton Plus **d’options** (**&#8943;**) dans la zone de composition.

![Capture d’écran de la liste des extensions de messagerie dans Teams](~/assets/images/compose-extensions/compose-extension-list.png)

Dans le manifeste de l’application, votre élément de commande est un objet avec la structure suivante :

| Nom de la propriété | Objectif | Obligatoire ? | Version minimale du manifeste |
|---|---|---|---|
| `id` | ID unique que vous affectez à cette commande. La demande de l’utilisateur inclut cet ID. | Oui | 1.0 |
| `title` | Nom de la commande. Cette valeur apparaît dans l’interface utilisateur. | Oui | 1.0 |
| `description` | Texte d’aide indiquant ce que fait cette commande. Cette valeur apparaît dans l’interface utilisateur. | Oui | 1.0 |
| `type` | Définissez le type de commande. Les valeurs possibles sont `query` et `action`. Si elle n’est pas présente, la valeur par défaut est définie sur `query` . | Non | 1.4 |
| `initialRun` | Paramètre facultatif, utilisé avec `query` les commandes. Si la valeur **est true,** indique que cette commande doit être exécutée dès que l’utilisateur choisit cette commande dans l’interface utilisateur. | Non | 1.0 |
| `fetchTask` | Paramètre facultatif, utilisé avec `action` les commandes. Définissez sur **true** pour récupérer la carte adaptative ou l’URL web à afficher dans le [module de tâche](~/task-modules-and-cards/what-are-task-modules.md). Cette valeur est utilisée lorsque les entrées de la commande sont dynamiques par opposition à un `action` ensemble statique de paramètres. Notez que si la valeur true **est définie,** la liste des paramètres statiques de la commande est ignorée. | Non | 1.4 |
| `parameters` | Liste statique des paramètres de la commande. | Oui | 1.0 |
| `parameter.name` | Le nom du paramètre. Cette information est envoyée à votre service dans la demande de l’utilisateur. | Oui | 1.0 |
| `parameter.description` | Décrit les objectifs de ce paramètre ou un exemple de la valeur à fournir. Cette valeur apparaît dans l’interface utilisateur. | Oui | 1.0 |
| `parameter.title` | Titre ou étiquette de paramètre court et convivial. | Oui | 1.0 |
| `parameter.inputType` | Définir sur le type d’entrée requis. Les valeurs `text` possibles sont , , , , `textarea` `number` `date` `time` `toggle` . La valeur par défaut est définie sur `text` . | Non | 1.4 |
| `context` | Tableau facultatif de valeurs qui définit le contexte dans lequel l’action de message est disponible. Les valeurs possibles `message` sont , `compose` ou `commandBox` . La valeur par défaut est `["compose", "commandBox"]`. | Non | 1,5 |
