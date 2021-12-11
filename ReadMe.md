# 6 ways to get started with App Service in Azure

    Pre-Requisites
        1. .NET 6 SDK
        2. .NET CLI
        3. Azure CLI
        4. Visual Studio Code
        5. Azure Subscription


## Using CLI Tools

1. Create a new web application using the following command
```bash
dotnet new webapp --name CliWebApp
```
2. Check the application is working locally by executing the `dotnet run` command.

```bash
dotnet run
```
3. Login to your Azure account from the command line using the Azure CLI tool. If you are already signed in, please ignore the steps

To login 
```bash
az login
```
The login page for Azure will be opened in your browser and continue the process by entering the credentials. Once successful, you can close the page and return to the console. 

In the console, all your subscriptions will be listed. If you want to select another subscription, use the below command to do that.

```bash
az account set --subscription <subscription id>
```

4. Create Web app in Azure and deploy

The following command can be used to create a web app and deploy that into the newly created environment in Azure

```bash
az webapp up -g dnf2021-b-rg -n cliwebapp -l southindia -r "dotnet:6.0" --sku p1v2 -b
```

`az webapp up` - Creates a web app and deploys from the current folder where the command is run

`-g or --resource-group` - Resource group of the web app, will be created if its not existing

`-n or --name` - Name of the web app, should be unqiue
`-l or --location` - location of the azure region where your web app will be located
`-r` - specifies the runtime and the version

`--sku` - pricing tiers, p1v2 - Premium V2 Small

`-b or --launch-browser` - Launches the created app on the default browser

This command will create the resource group, app service plan and deploy the app into the app service

# 2 : Deploying using VS Code
## Step 1 : Create web app
Create a new vanila web app using the template
and open the code in VS Code

## Step 2 : Install App Service Extension for VS Code
Install and download the App Service extension for VS Code. This extension helps you to manage app services in your subscription directly from VS Code

Details available at [https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azureappservice](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azureappservice)

Once the installation is completed, the Azure icon will show in the left panel

## Step 3: Deploying App
To create the app, bring up the quick launch in VS Code and type in Create new web app. You will be presented with an option to Sign into Azure if you are trying it for the first time or your session has already expired

Once the sign up is done, you will be asked to select a subscription first.
Then provide an uniquely identifiable name for your web app, runtime stack, sku,  it will start creating the new resource group and app service plans and then deploy provisions a web app based on the options we chose earlier

There is an advanced option available which lets you have much more control over the provisioning of the resources. To use that, simply type create new web app and choose the one with advanaced option

Just like in the previous approach, choose a subscription from the list and in next prompt you will have to either choose a resource group or an option for creating a new one.

After that, choose .NET6 as runtime stack, and then I am going to chose Linux as the OS from the next prompt and then a location where you need to deploy the app

After that just like resource group, you will get to choose an existing app service plan or create a new one
and then option to choose a tier will be provided.

For the sake of the demo. I am going to skip the app insights resource  

After that it will start creating the web app service as per our selected configuration

If you choose Deploy to Web app option, it can create the web app service and then deploy the app in one go as web saw in our previous demo

# 3 Deploying with GitHub Actions

## Step 1 : Setup the web app locally
Create a web application using the default template, and I am going to slightly modify it by the adding the following lines to the index view

```html
<div class="text-center">
    
    <h1>.NET Version</h1>
    @System.Environment.Version

    <h2>Description</h2>
    @System.Runtime.InteropServices.RuntimeInformation.FrameworkDescription
</div>

```

## Step 2 : Set up GitHub repo 

Initialize a github repo and push the code from local to GitHub

```bash
git init -b main

git add . && git commit -m "initial commit"

git remote add origin https://github.com/amaldevv/DotNetConf2021-bdotnet.git
```
## Step 3 : Create Web app via Portal
Create a new web app servce and configure deployment using GitHub.

Modify the YAML file to select the correct source path


# Functions
Create function app from VS
deploy to azure
get path for the api
