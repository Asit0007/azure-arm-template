# Azure Resource Manager (ARM) Template Deployment

This repository contains an example of how to create, deploy, and update an Azure Resource Manager (ARM) template using Visual Studio Code and Azure PowerShell. The goal is to demonstrate the process of deploying an ARM template to Azure, adding parameters, outputs, and resources like an Azure Storage Account.

## Table of Contents
- [Overview](#overview)
- [Prerequisites](#prerequisites)
- [Steps](#steps)
  - [Create the ARM Template](#create-the-arm-template)
  - [Deploy the ARM Template](#deploy-the-arm-template)
  - [Add a Resource to the ARM Template](#add-a-resource-to-the-arm-template)
  - [Deploy the Updated ARM Template](#deploy-the-updated-arm-template)
- [Commands](#commands)

## Overview
The ARM template we create will be used to deploy an Azure Storage Account. This ARM template is a JSON file that describes the resources and configurations to be deployed to Azure. The template includes parameters, variables, resources, and outputs.

The template starts with a blank configuration, and we later update it to add a storage account resource, set the location and SKU type, and then deploy it to Azure using Azure PowerShell.

## Prerequisites
1. **Visual Studio Code**: Installed on your local machine.
2. **Azure Resource Manager Tools**: Installed in Visual Studio Code to help with ARM template syntax.
3. **Azure PowerShell**: Installed in Visual Studio Code to manage your Azure resources.

Make sure you have signed into your Azure account from Visual Studio Code and activated your sandbox environment (if applicable).

## Steps

### Create the ARM Template
1. Open Visual Studio Code and create a new file called `azuredeploy.json`.
2. Use the ARM template snippet provided by the Azure Resource Manager Tools extension in Visual Studio Code.

    Your initial `azuredeploy.json` file will look like this:

    ```json
    {
    "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {},
    "functions": [],
    "variables": {},
    "resources": [],
    "outputs": {}
    }


### Deploy the ARM Template

To deploy the ARM template to Azure, follow these steps:

 **Open the terminal in Visual Studio Code** 

 **Sign in to Azure** using the following command:

  ```powershell
    Connect-AzAccount
```
Set the default subscription for the session:

  ```powershell
    Get-AzSubscription
    $context = Get-AzSubscription -SubscriptionId {Your subscription ID}
    Set-AzContext $context
```
