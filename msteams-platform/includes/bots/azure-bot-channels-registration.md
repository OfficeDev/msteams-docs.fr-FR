1. Dans le [Azure Portal] [Azure-Portal], dans le volet de navigation de gauche, sélectionnez **créer une ressource**.
1. Dans la zone de sélection du volet de droite, entrez « bot ». Dans la liste déroulante, sélectionnez **enregistrement des canaux de robots**.
1. Cliquez sur le bouton **Créer**.
1. Dans le panneau **d’enregistrement du canal bot** , fournissez les informations requises concernant votre robot.
1. Laissez la zone **point de terminaison de messagerie** vide pour le moment, vous entrez l’URL requise après le déploiement du bot. L’image suivante montre un exemple des paramètres d’enregistrement :

    ![inscription des canaux de l’application bot](../../assets/images/authentication/auth-bot-channels-registration.png)

1. Cliquez sur **ID d’application Microsoft et mot de passe** , puis **créez nouveau**.
1. Cliquez sur **créer un ID d’application dans le lien portail d’inscription des applications** .
1. Dans la fenêtre **inscription** de l’application affichée, cliquez sur l’onglet **nouvelle inscription** dans le coin supérieur gauche.
1. Entrez le nom de l’application bot que vous enregistrez, nous avons utilisé *BotTeamsAuth* (vous devez sélectionner votre propre nom unique).
1. Pour les **types de comptes pris en charge** , sélectionnez *comptes dans n’importe quel annuaire d’organisation (tout annuaire Azure ad-client) et comptes Microsoft personnels (par exemple, Skype, Xbox)*.
1. Cliquez sur le bouton **Enregistrer** . Une fois terminé, Azure affiche la page de *vue d’ensemble* de l’application.
1. Copier et enregistrer dans un fichier la valeur de l' **ID d’application (client)** .
1. Dans le volet gauche, cliquez sur **certificat et secrets**.
    1. Sous *secrets client*, cliquez sur **nouvelle clé secrète client**.
    1. Ajoutez une description pour identifier cette clé secrète auprès d’autres personnes que vous devrez peut-être créer pour cette application.
    1. Définit *expire* à votre sélection.
    1. Cliquez sur **Ajouter**.
    1. Copiez la clé secrète client et enregistrez-la dans un fichier.
1. Revenez à la fenêtre **d’enregistrement du canal bot** et copiez l’ID de l' *application* et la *clé secrète client* dans les zones ID de l’application et **mot de passe** **Microsoft** , respectivement.
1. Cliquez sur **OK**.
1. Enfin, cliquez sur **créer**.
