---
title: Ajouter des données de test à votre client test Microsoft 365
description: Configurer votre abonnement au programme pour les développeurs Office 365 pour tester les applications Microsoft Teams
ms.topic: how-to
keywords: test des équipes de programme pour les développeurs d’applications
ms.date: 11/01/2019
ms.openlocfilehash: 9e23b9054f45ccff6c08b97c72f4d5375fef58ea
ms.sourcegitcommit: 5b3ba227c2e5e6f7a2c629961993f168da6a504d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/08/2021
ms.locfileid: "51634719"
---
# <a name="add-test-data-to-your-microsoft-365-test-tenant"></a><span data-ttu-id="b3efb-104">Ajouter des données de test à votre client test Microsoft 365</span><span class="sxs-lookup"><span data-stu-id="b3efb-104">Add test data to your Microsoft 365 test tenant</span></span>

<span data-ttu-id="b3efb-105">Avec un abonnement Microsoft 365 Développeur, vous pouvez utiliser votre application Microsoft Teams avec des équipes de test, des canaux et des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="b3efb-105">With a Microsoft 365 developer subscription, you can use your Microsoft Teams app with test teams, channels, and users.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b3efb-106">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="b3efb-106">Prerequisites</span></span>

1. <span data-ttu-id="b3efb-107">Rejoignez le programme pour les développeurs [Microsoft 365,](/office/developer-program/office-365-developer-program)si vous n’avez pas de client de test.</span><span class="sxs-lookup"><span data-stu-id="b3efb-107">[Join the Microsoft 365 Developer Program](/office/developer-program/office-365-developer-program), if you do not have a test tenant.</span></span>
2. <span data-ttu-id="b3efb-108">[Configurer un abonnement Microsoft 365 Développeur.](/office/developer-program/office-365-developer-program-get-started)</span><span class="sxs-lookup"><span data-stu-id="b3efb-108">[Set up a Microsoft 365 Developer Subscription](/office/developer-program/office-365-developer-program-get-started).</span></span>
3. <span data-ttu-id="b3efb-109">[Utilisez des packs d’exemples](/office/developer-program/install-sample-packs)de données avec votre abonnement Microsoft 365 Développeur pour installer le pack de contenu Utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="b3efb-109">[Use sample data packs with your Microsoft 365 developer subscription to install the Users content pack](/office/developer-program/install-sample-packs).</span></span>
4. <span data-ttu-id="b3efb-110">[Installez le module PowerShell Teams.](https://www.powershellgallery.com/packages/MicrosoftTeams/1.0.2)</span><span class="sxs-lookup"><span data-stu-id="b3efb-110">[Install the Teams PowerShell module](https://www.powershellgallery.com/packages/MicrosoftTeams/1.0.2).</span></span>
5. <span data-ttu-id="b3efb-111">[Installez le module Azure AD PowerShell.](/powershell/azure/active-directory/install-adv2?view=azureadps-2.0#installing-the-azure-ad-module&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="b3efb-111">[Install the Azure AD PowerShell module](/powershell/azure/active-directory/install-adv2?view=azureadps-2.0#installing-the-azure-ad-module&preserve-view=true).</span></span>

> [!NOTE]
> <span data-ttu-id="b3efb-112">Pour tout client que vous utilisez, vous devez obtenir les autorisations d’administrateur général pour exécuter les scripts.</span><span class="sxs-lookup"><span data-stu-id="b3efb-112">For any tenant that you use, you must get the global administrator permissions to run the scripts.</span></span>

## <a name="enable-custom-app-sideloading"></a><span data-ttu-id="b3efb-113">Activer le chargement de version de version d’application personnalisée</span><span class="sxs-lookup"><span data-stu-id="b3efb-113">Enable custom app sideloading</span></span>

<span data-ttu-id="b3efb-114">L’activation du chargement de version de version d’application personnalisée est facultative.</span><span class="sxs-lookup"><span data-stu-id="b3efb-114">Enabling custom app sideloading is optional.</span></span> <span data-ttu-id="b3efb-115">Par défaut, seuls les administrateurs globaux ou les administrateurs du service Teams peuvent télécharger des applications personnalisées dans le catalogue d’applications client.</span><span class="sxs-lookup"><span data-stu-id="b3efb-115">By default, only global admins or Teams service admins can upload custom apps into the tenant app catalog.</span></span> <span data-ttu-id="b3efb-116">Vous pouvez également autoriser les utilisateurs à télécharger des applications personnalisées dans Teams.</span><span class="sxs-lookup"><span data-stu-id="b3efb-116">You can also allow users to upload custom apps to Teams.</span></span> <span data-ttu-id="b3efb-117">Pour plus d’informations, voir [gérer les stratégies de configuration d’application dans Teams.](/microsoftteams/teams-app-setup-policies)</span><span class="sxs-lookup"><span data-stu-id="b3efb-117">For more information, see [manage app setup policies in Teams](/microsoftteams/teams-app-setup-policies).</span></span>

## <a name="create-teams-and-channels"></a><span data-ttu-id="b3efb-118">Créer des équipes et des canaux</span><span class="sxs-lookup"><span data-stu-id="b3efb-118">Create teams and channels</span></span>

1. <span data-ttu-id="b3efb-119">Enregistrez l’extrait de code suivant en tant **que fichier .xml** et notez le chemin d’accès du fichier.</span><span class="sxs-lookup"><span data-stu-id="b3efb-119">Save the following snippet as a **.xml** file and note the file path.</span></span> <span data-ttu-id="b3efb-120">Ce XML définit la structure de l’équipe et du canal créés avec ses membres :</span><span class="sxs-lookup"><span data-stu-id="b3efb-120">This XML defines the structure of the team and channel that is created along with its members:</span></span>

    ```xml
    <?xml version="1.0"?>
    <Teams>
      <Team Name="Store Portal" ID="storeportal" Description="" Type="Private" Creator="admin">
        <Members>
          <Member UserName="AlexW" IsOwner="false"/>
          <Member UserName="PattiF" IsOwner="false"/>
          <Member UserName="PradeepG" IsOwner="false"/>
          <Member UserName="JoniS" IsOwner="false"/>
          <Member UserName="JohannaL" IsOwner="false"/>
          <Member UserName="NestorW" IsOwner="false"/>
          <Member UserName="IsaiahL" IsOwner="false"/>
          <Member UserName="AdeleV" IsOwner="false"/>
          <Member UserName="LeeG" IsOwner="false"/>
          <Member UserName="MeganB" IsOwner="true"/>
          <Member UserName="LynneR" IsOwner="false"/>
          <Member UserName="GradyA" IsOwner="false"/>
          <Member UserName="LidiaH" IsOwner="false"/>
          <Member UserName="DiegoS" IsOwner="false"/>
          <Member UserName="MiriamG" IsOwner="true"/>
        </Members>
        <Channels>
          <Channel Name="Sales" ID="sales" Description="" Creator="Admin" />
          <Channel Name="Inventory" ID="inventory" Description="" Creator="Admin" />
          <Channel Name="Los Angeles Store 239" ID="losangelesstore239" Description="" Creator="Admin" />
          <Channel Name="Seattle Store 121" ID="seattlestore121" Description="" Creator="Admin" />
          <Channel Name="Online" ID="online" Description="" Creator="Admin" />
          <Channel Name="Store Layout" ID="storelayout" Description="" Creator="Admin" />
          <Channel Name="Promotions" ID="promotions" Description="" Creator="Admin" />
        </Channels>
      </Team>
      <Team Name="Mark 8 Project Team" ID="Mark8ProjectTeam" Description="Welcome to the team that we've assembled to create the Mark 8." Type="Private" Creator="admin">
        <Members>
          <Member UserName="meganb" IsOwner="true" />
          <Member UserName="alexw" IsOwner="false" />
          <Member UserName="lynner" IsOwner="false" />
          <Member UserName="isaiahl" IsOwner="false" />
          <Member UserName="leeg" IsOwner="false" />
          <Member UserName="pradeepg" IsOwner="false" />
          <Member UserName="lidiah" IsOwner="false" />
          <Member UserName="diegos" IsOwner="false" />
          <Member UserName="johannal" IsOwner="false" />
          <Member UserName="miriamg" IsOwner="false" />
          <Member UserName="adelev" IsOwner="false" />
          <Member UserName="jonis" IsOwner="false" />
          <Member UserName="nestorw" IsOwner="false" />
          <Member UserName="gradya" IsOwner="false" />
          <Member UserName="pattif" IsOwner="false" />
        </Members>
        <Channels>
          <Channel Name="Research and Development" ID="researchanddevelopment" Description="Channel for Research and Development!" Creator="meganb" />
          <Channel Name="Design" ID="design" Description="Discuss design projects." Creator="meganb" />
          <Channel Name="Digital Assets Web" ID="digitalassetsweb" Description="Discuss digital assets." Creator="meganb" />
          <Channel Name="Go to Market Plan" ID="gotomarketplan" Description="Our go-to-market plan!" Creator="meganb" />
        </Channels>
      </Team>
      <Team Name="District 9 Road Safety Audit" ID="district9roadsafetyaudit" Description="" Type="Private" Creator="admin">
        <Members>
          <Member UserName="meganb" IsOwner="true" />
          <Member UserName="alexw" IsOwner="false" />
          <Member UserName="lynner" IsOwner="false" />
          <Member UserName="isaiahl" IsOwner="false" />
          <Member UserName="leeg" IsOwner="false" />
          <Member UserName="pradeepg" IsOwner="false" />
          <Member UserName="lidiah" IsOwner="false" />
          <Member UserName="diegos" IsOwner="false" />
          <Member UserName="johannal" IsOwner="false" />
          <Member UserName="miriamg" IsOwner="false" />
          <Member UserName="adelev" IsOwner="false" />
          <Member UserName="jonis" IsOwner="false" />
          <Member UserName="nestorw" IsOwner="false" />
          <Member UserName="gradya" IsOwner="false" />
          <Member UserName="pattif" IsOwner="false" />
        </Members>
        <Channels>
          <Channel Name="Audit Planning" ID="auditplanning" Description="" Creator="Admin" />
          <Channel Name="Delivery" ID="delivery" Description="" Creator="Admin" />
          <Channel Name="Findings" ID="findings" Description="" Creator="Admin" />
          <Channel Name="Recommended Actions" ID="recommendedactions" Description="" Creator="Admin" />
          <Channel Name="Survey" ID="survey" Description="" Creator="Admin" />
        </Channels>
      </Team>
      <Team Name="ACC-1000 Product Team" ID="acc1000productteam" Description="" Type="Private" Creator="admin" >
        <Members>
          <Member UserName="meganb" IsOwner="true" />
          <Member UserName="alexw" IsOwner="false" />
          <Member UserName="lynner" IsOwner="false" />
          <Member UserName="isaiahl" IsOwner="false" />
          <Member UserName="leeg" IsOwner="false" />
          <Member UserName="pradeepg" IsOwner="false" />
          <Member UserName="lidiah" IsOwner="false" />
          <Member UserName="diegos" IsOwner="false" />
          <Member UserName="johannal" IsOwner="false" />
          <Member UserName="miriamg" IsOwner="false" />
          <Member UserName="adelev" IsOwner="false" />
          <Member UserName="jonis" IsOwner="false" />
          <Member UserName="nestorw" IsOwner="false" />
          <Member UserName="gradya" IsOwner="false" />
          <Member UserName="pattif" IsOwner="false" />
        </Members>
        <Channels>
          <Channel Name="Corporate Communication" ID="corporatecommunication" Description="" Creator="Admin" />
          <Channel Name="Lean Process Improvement" ID="corporatecommunication" Description="" Creator="Admin" />
          <Channel Name="Training and Certification" ID="trainingandcertification" Description="" Creator="Admin" />
          <Channel Name="Production" ID="production" Description="" Creator="Admin" />
          <Channel Name="Research and Development" ID="researchanddevelopment" Description="" Creator="Admin" />
          <Channel Name="Supplier Collaboration" ID="suppliercollaboration" Description="" Creator="Admin" />
        </Channels>
      </Team>
    </Teams>
    ```

2. <span data-ttu-id="b3efb-121">Enregistrez l’extrait de code suivant en tant que script PowerShell (.ps1) et notez l’endroit où vous l’avez enregistré.</span><span class="sxs-lookup"><span data-stu-id="b3efb-121">Save the following snippet as a PowerShell script (.ps1) and note where you have saved it.</span></span> <span data-ttu-id="b3efb-122">Ce script exécute les étapes pour créer l’équipe et le canal, et y ajouter des membres :</span><span class="sxs-lookup"><span data-stu-id="b3efb-122">This script executes the steps to create the team and channel, and add members to them:</span></span>

    ```powershell
    Param(
        [Parameter(Mandatory = $true)]

        # This specifies the location of your configuration XML.

        [string] $teamsFilePath 
    )

    [xml]$XmlDocument = Get-Content -Path $teamsFilePath.ToString()

    if ($XmlDocument.Teams.Team.Count -gt 0) {

        try {

            # 1. Login with the global administrator account for your O365 Developer Program tenant. This script uses these credentials to connect to the powershell modules for Azure Active Directory and Microsoft Teams

            $creds = Get-Credential

            # Connecting to AAD PowerShell
            Connect-AzureAD -Credential $creds | Out-Null

            # Connect to Microsoft Teams PowerShell
            Connect-MicrosoftTeams -Credential $creds | Out-Null

            Write-Host "Connected to Microsoft 365 and configuring your organization with test teams and channels"

            # 2. Create the teams as specified in the XML.

            foreach ($team in $XmlDocument.Teams.Team ) {
                try {
                    $group = New-Team -DisplayName $team.Name -Description $teams.description -visibility public 
                    Write-Host "Successfully created team: " $group.DisplayName
                }
                catch {
                    Write-Host "Unable to create team: $_"
                }

                # 3. Add users to the newly created teams.
                foreach ($user in $team.Members.Member) {
                    try {
                        $newUserPrincipalName = (Get-AzureADUser -SearchString $user.UserName).UserPrincipalName

                        if($user.IsOwner -eq $true){
                            Add-TeamUser -GroupId $group.GroupId -User $newUserPrincipalName -Role Owner | Out-Null
                        }else{
                            Add-TeamUser -GroupId $group.GroupId -User $newUserPrincipalName | Out-Null
                        }

                        Write-Host "Successfully added user : " $user.UserName
                    }
                    catch {
                        Write-Host "Unable to add team user: $_"
                    }

                }

                # 4. Add a set of channels to each newly created team
                foreach ($channel in $team.Channels.Channel) {
                    try {
                        # Adding each team channel
                        New-TeamChannel -GroupId $group.GroupId -DisplayName $channel.Name -Description $channel.Description | Out-Null
                        Write-Host "Successfully created channel: " $channel.Name
                    }
                    catch {
                        Write-Host "Unable to add new Team Channel: $_"
                    }   
                }

                Clear-Variable -Name group
            }

            Clear-Variable -Name creds

            # 5. Disconnect from all PowerShell sessions

            Write-Host "Completed execution and disconnecting from Microsoft 365 PowerShell sessions."
            Disconnect-MicrosoftTeams
            Disconnect-AzureAD
        }
        catch {
            Write-Host "Unable to complete the operation: $_"
        }
    }
    else {
        Write-Host "Content file has invalid data."
    }
    ```

3. <span data-ttu-id="b3efb-123">Ouvrez une session Windows PowerShell en mode Administrateur et exécutez le script que vous viennent d’écrire.</span><span class="sxs-lookup"><span data-stu-id="b3efb-123">Open a Windows PowerShell session in Administrator mode, and run the script that you just saved.</span></span>
4. <span data-ttu-id="b3efb-124">Lorsque vous êtes invité à fournir les informations d’identification, entrez les informations d’identification d’administrateur général que vous avez reçues lors de votre première inscription à votre abonnement développeur.</span><span class="sxs-lookup"><span data-stu-id="b3efb-124">When you are prompted to provide the credentials, enter the Global Administrator credentials you received when you first signed up for your developer subscription.</span></span>

    > [!Note]
    > <span data-ttu-id="b3efb-125">Ne fermez pas votre session PowerShell, car l’exécution du script prend plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="b3efb-125">Do not close your PowerShell session as the script takes several minutes to execute.</span></span> <span data-ttu-id="b3efb-126">Si vous avez modifié les utilisateurs de votre abonnement à partir de ce qui est créé dans le pack de contenu par défaut, certains utilisateurs peuvent ne pas être ajoutés à Teams.</span><span class="sxs-lookup"><span data-stu-id="b3efb-126">If you have modified the users in your subscription from what is created in the default content pack, some users may not be added to Teams.</span></span> <span data-ttu-id="b3efb-127">Lorsque le script s’exécute, il affiche les actions réussies ou échouées.</span><span class="sxs-lookup"><span data-stu-id="b3efb-127">As the script executes it displays successful or failed actions.</span></span>

5. <span data-ttu-id="b3efb-128">Une fois l’exécution du script terminée, vous pouvez vous inscrire au client Teams avec l’un des comptes d’utilisateur et afficher les équipes nouvellement créées.</span><span class="sxs-lookup"><span data-stu-id="b3efb-128">After the script has finished execution, you can sign in to the Teams client with one of the user accounts and view the newly created teams.</span></span>

## <a name="see-also"></a><span data-ttu-id="b3efb-129">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="b3efb-129">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b3efb-130">Déboguer votre onglet</span><span class="sxs-lookup"><span data-stu-id="b3efb-130">Debug your tab</span></span>](~/tabs/how-to/developer-tools.md)
 
> [!div class="nextstepaction"]
> [<span data-ttu-id="b3efb-131">Déboguer vos bots</span><span class="sxs-lookup"><span data-stu-id="b3efb-131">Debug your bots</span></span>](~/bots/how-to/debug/locally-with-an-ide.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="b3efb-132">Tester les autorisations RSC</span><span class="sxs-lookup"><span data-stu-id="b3efb-132">Test RSC permissions</span></span>](~/graph-api/rsc/test-resource-specific-consent.md)

