# Assignment: Create, Manage & Secure Azure Resources

### Here are the steps I took to achieve my results
Get the base code:
  - forked Reza's dotnet-api-template too my github
  - Cloned it with visual studio code
  - ran the code locally to check if everything works ``dotnet run``

#### Section 1: Create a Web Application using Azure CLI
    1. Develop a .NET web API application and publish its code into a Git repository.
        - Made a .NET core api in visual code 2022 and pushed it to github

    2. Create a Resource Group with a randomly assigned unique name, serving as the central container for all subsequent resources, services, and components.
        - used ``az group create --name resourceGroupMark --location northeurope`` (forgot to make screenshot)
    3. Create and configure a Web Server to support web hosting in either a free or shared environment for cost-effectiveness (e.g. App Service Plan with a free or shared tier).
        - used ``az appservice plan create -g resourceGroupMark -n appServiceplanMark --sku F1`` (screen: 1.3.0_CreateAppServicePlan)
    4. Create a Web App with a distinctive name within the previously configured Web Server (e.g. a Web App hosted within the selected App Service Plan from the previous step).
        - used ``az webapp create -g resourceGroupMark -p appServicePlanMark -n webAppMark`` (screens: 1.4_CreateWebApp1, 2 & 3. 1.4_Azure_CreatedWebApp)
    5. Deploy your .NET web API to the Web App from the previous step.
        - Eventually I uploaded the web api trough visual studio's UI (screens: 1.5_DeployedDotnetApi. none of deployment, forgot)


#### Section 2: Create an Azure SQL Database & Secure it with a Firewall using Azure PowerShell
    !!NOTE: Azure Powershell did not play nice with me, to this moment I could not get it installed. It seems to conflict with AzureRM. I deleted that and it still won't install. I gave up after a whil since I'd like to move on.
    1. Use the Resource Group you created earlier and arrange all the resources into it.
        
    2. Create a Sql Database Server with necessary configurations and protect it with an admin username/password.
        - used ``az sql server create --name sqlMark --resource-group resourceGroupMark --location "Northeurope" --admin-user markenden@hotmail.com --admin-password ************`` (screen: 2.2_Create SqlServer & 2.2_CreatedSqlServer)
    3. Set up the firewall rule to connect and access the Azure SQL database from any source.
        - used ``az server firewall-rule create -g resourceGroupMark -s sqlmark -n ruleMark --start-ip-adress 1.2.3.4 --end-ip-adress 5.6.7.8`` (screen: 2.3_FirewallRule & 2.3_CreatedFirewallRule) (I know the start and end ip adress makes no sense, but I just wanted it to work.)
    4. Create a Database within SQL Database Server so that you can maintain tables to organize your data.
        - used ``az sql db create -g resourceGroupMark -s sqlmark - n dbMark --service-objective S0`` (screen:2.4_CreateSqlDb & 2.4_CreatedSqlDb)
    5. Login to the server and access the database. Create your own database scheme to satisfy your website needs and business requirements.
        - Sorry, from here on I did not make it.
    6. Use Query Editor to insert some records into the database.
    7. OPTIONAL - As an alternative to SQL Server Authentication, use Azure AD and connect to your Azure SQL Database by using any one of the Azure AD identities.

#### OPTIONAL - Section 3: Deploy & Authenticate Your Application with AzureAD using Azure Portal.
    1. Authorize various types of users to access your web application/website created earlier in Section 1. Perform necessary validation and authentication credentials to access the application. The credentials must be stored in Azure AD to identify and validate the application and the user.
    2. Deploy your application from the Git repository using Azure CLI and run the application to test the authentication. The website should be accessible to the public using a URL, and only authorized users should be able to access its resources.




















#### Made the docker/github CI/CD
  - made a access token in docker
  - added secrets for username and docker access token in github repository
  - updated/pushed my repository to see if it worked. Had to activate actions in github, since it blocked it at first. Worked fine afterwards.

#### Added the bicep files, made the resource group, app service & app service plan
  - took the bicep files from "ci-cd-iac-bicep", and ajusted some info (correction: I did this in the old files, not this one)
  - added all the local info in terminal/powershell:

  ``$ENV:ARM_CLIENT_ID = "668ccd6f-6d36-426e-b1a7-c158ac48d596"``

  ``$ENV:ARM_CLIENT_SECRET = "****************************************"``

  ``$ENV:ARM_SUBSCRIPTION_ID = "c8866fbf-71d6-4235-91cd-201c29ec1b0e"``

  ``$ENV:ARM_TENANT_ID = "a1d168fb-cc80-4836-8881-3ab4a0cd4630"``

  ``$env:AZURE_REGION = "NorthEurope"``

  ``$env:RG_NAME = "rg-bicep-webapp-mark"``

  ``$env:DOCKER_USR = "markenden"``

  ``$env:DOCKER_IMAGE = "dotnet-api-template"``

  - used "cd infrastructure" to navigate to relevent map -> ran the following command to build the Rg, app & app service plan (first as what-if to be sure)

   ``az deployment sub what-if -l ${env:AZURE_REGION} --name=rg-bicep-webapp-mark --template-file main.bicep --parameters rgName=${env:RG_NAME} location=${env:AZURE_REGION} dockerHubUser=${env:DOCKER_USR} dockerImage=${env:DOCKER_IMAGE}``

#### Add a webhook to docker
  - Asked Reza to make a webhook url for me since I did not have the privilege for that, and added it to the docker repo

#### Cleaned up a little
  - trew away the old bicep files
  - made this readme

#### Screenshots are added in the screenshots map in the .zip that I'll upload to Noroff Accelerate

#### final thoughts
Looking back and seeing it all written out it seems so simple, yet it took me a couple of tries and experimentations to get it right :D
At first I was overwhelmed with all the possibilities and uncertainties but it ended up being more straight forward than I anticipated, nice.

Thank you again and have a nice day!