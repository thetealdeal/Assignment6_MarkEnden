﻿# Assignment: Create, Manage & Secure Azure Resources


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
    !!NOTE: I documented the powershell commands I think I'd use in the .txt file

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
