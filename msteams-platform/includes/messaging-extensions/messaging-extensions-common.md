## <a name="add-a-message-extension-to-your-app"></a>Ajouter une extension de message à votre application

Une extension de message est un service hébergé dans le cloud qui écoute les demandes des utilisateurs et répond avec des données structurées, telles qu’une [carte](~/task-modules-and-cards/what-are-cards.md). Vous intégrez votre service à Microsoft Teams via des objets Bot Framework`Activity`. Nos extensions .NET et Node.js pour le Kit de développement logiciel (SDK) Bot Builder peuvent vous aider à ajouter des fonctionnalités d’extension de message à votre application.

![Diagramme du flux de messages pour les extensions de message](~/assets/images/compose-extensions/ceflow.png)

### <a name="register-in-the-bot-framework"></a>S’inscrire dans Bot Framework

Si vous ne l’avez pas déjà fait, vous devez d’abord inscrire un bot auprès du Microsoft Bot Framework. L’ID d’application Microsoft et les points de terminaison de rappel de votre bot, tels qu’ils y sont définis, seront utilisés dans votre extension de message pour recevoir et répondre aux demandes des utilisateurs. N’oubliez pas d’activer le canal Microsoft Teams pour votre bot.

Enregistrez votre ID d’application bot et votre mot de passe d’application. Vous devez fournir l’ID d’application dans le manifeste de votre application.

### <a name="update-your-app-manifest"></a>Mettre à jour le manifeste de votre application

Comme avec les bots et les onglets, vous mettez à jour le [manifeste](~/resources/schema/manifest-schema.md#composeextensions) de votre application pour inclure les propriétés de l’extension de message. Ces propriétés régissent la façon dont votre extension de message apparaît et se comporte dans le client Microsoft Teams. Les extensions de message sont prises en charge à partir de la version 1.0 du manifeste.

#### <a name="declare-your-message-extension"></a>Déclarer votre extension de message

Pour ajouter une extension de message, incluez une nouvelle structure JSON de niveau supérieur dans votre manifeste avec la `composeExtensions` propriété. Actuellement, vous êtes limité à la création d’une extension de message unique pour votre application.

> [!NOTE]
> Le manifeste fait référence aux extensions de message sous la forme `composeExtensions`. Il s’agit de maintenir la compatibilité descendante.

La définition d’extension est un objet qui a la structure suivante :

| Nom de la propriété | Objectif | Obligatoire ? |
|---|---|---|
| `botId` | ID d’application Microsoft unique pour le bot inscrit dans le Bot Framework. Cela doit généralement être le même que l’ID de votre application Teams globale. | Oui |
| `scopes` | Tableau indiquant si cette extension peut être ajoutée à ou `team` à `personal` des étendues (ou les deux). | Oui |
| `canUpdateConfiguration` | Active **Paramètres** élément de menu. | Non |
| `commands` | Tableau de commandes prises en charge par cette extension de message. Vous êtes limité à 10 commandes. | Oui |

#### <a name="define-commands"></a>Définir des commandes

Votre extension de message doit déclarer une commande, qui s’affiche lorsque l’utilisateur sélectionne votre application à partir du bouton **Plus d’options** (**&#8943;**) dans la zone de composition.

![Capture d’écran de la liste des extensions de message dans Teams](~/assets/images/compose-extensions/compose-extension-list.png)

Dans le manifeste de l’application, votre élément de commande est un objet avec la structure suivante :

| Nom de la propriété | Objectif | Obligatoire ? | Version minimale du manifeste |
|---|---|---|---|
| `id` | ID unique que vous affectez à cette commande. La demande de l’utilisateur inclut cet ID. | Oui | 1.0 |
| `title` | Nom de la commande. Cette valeur apparaît dans l’interface utilisateur. | Oui | 1.0 |
| `description` | Texte d’aide indiquant ce que fait cette commande. Cette valeur apparaît dans l’interface utilisateur. | Oui | 1.0 |
| `type` | Définissez le type de commande. Les valeurs possibles sont `query` et `action`. Si elle n’est pas présente, la valeur par défaut est définie sur `query`. | Non | 1.4 |
| `initialRun` | Paramètre facultatif, utilisé avec `query` les commandes. Si la valeur **est true**, indique que cette commande doit être exécutée dès que l’utilisateur choisit cette commande dans l’interface utilisateur. | Non | 1.0 |
| `fetchTask` | Paramètre facultatif, utilisé avec `action` les commandes. Défini sur **true** pour extraire la carte adaptative ou l’URL web à afficher dans le [module de tâche](~/task-modules-and-cards/what-are-task-modules.md). Il est utilisé lorsque les entrées de la `action` commande sont dynamiques par opposition à un ensemble statique de paramètres. Notez que si la valeur est **true** , la liste des paramètres statiques de la commande est ignorée. | Non | 1.4 |
| `parameters` | Liste statique des paramètres pour la commande. | Oui | 1.0 |
| `parameter.name` | Le nom du paramètre. Il est envoyé à votre service dans la demande de l’utilisateur. | Oui | 1.0 |
| `parameter.description` | Décrit les objectifs de ce paramètre ou l’exemple de la valeur qui doit être fournie. Cette valeur apparaît dans l’interface utilisateur. | Oui | 1.0 |
| `parameter.title` | Titre ou étiquette de paramètre convivial court. | Oui | 1.0 |
| `parameter.inputType` | Définissez le type d’entrée requis. Les valeurs possibles sont : `text`, `textarea`, `number``date`, `toggle``time`. La valeur par défaut est `text`. | Non | 1.4 |
| `context` | Tableau facultatif de valeurs qui définit le contexte dans lequel l’action de message est disponible. Les valeurs possibles sont `message`, `compose`ou `commandBox`. La valeur par défaut est `["compose", "commandBox"]`. | Non | 1,5 |
