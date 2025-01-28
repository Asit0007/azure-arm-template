# Azure Resource Manager (ARM) Template Deployment Guide

Welcome to this repository! This guide will walk you through creating and deploying an Azure Resource Manager (ARM) template to manage resources in your Azure environment. ARM templates provide a way to define and deploy infrastructure as code in a repeatable, consistent manner.

## Overview

This repository contains an example ARM template for creating an Azure Storage Account. ARM templates are JSON-based configuration files that allow you to automate the deployment of resources to Azure. You will learn how to:

- Create an ARM template.
- Add a new resource to the ARM template.
- Deploy the updated template.
- Verify the deployment in the Azure portal.

By the end of this guide, you will have a functional ARM template that you can customize and deploy as needed for your Azure projects.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Setting Up the ARM Template](#setting-up-the-arm-template)
- [Adding a Resource to the ARM Template](#adding-a-resource-to-the-arm-template)
- [Deploying the Updated ARM Template](#deploying-the-updated-arm-template)
- [Checking Your Deployment](#checking-your-deployment)

## Prerequisites

Before you begin, ensure you have the following tools installed and configured:

1. **Visual Studio Code**:
   - If you don't have it installed, download and install Visual Studio Code from [here](https://code.visualstudio.com/).
   
2. **Azure PowerShell**:
   - Install Azure PowerShell from [here](https://learn.microsoft.com/en-us/powershell/azure/install-az-ps).
   - Make sure you have the latest version installed.

3. **Azure Subscription**:
   - You will need an active Azure subscription. If you don't have one, you can create a free account [here](https://azure.microsoft.com/en-us/free/).

4. **Basic Knowledge of Azure and ARM Templates**:
   - This guide assumes you have basic knowledge of Azure resources and ARM templates.

## Setting Up the ARM Template

###  Open the File in Visual Studio Code

Once you have created the (`azuredeploy.json`) file, open it in Visual Studio Code. If you have the Azure Resource Manager Tools extension installed, you will get syntax highlighting and IntelliSense for easier editing.

Use the ARM template snippet provided by the Azure Resource Manager Tools extension in Visual Studio Code.

Here is the basic structure of an ARM template (`azuredeploy.json`):

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
```
- $schema: Specifies the schema for the ARM template.
- contentVersion: A version number for the template.
- parameters: A section where you can define input parameters for the template.
- functions: Custom functions for the template (optional).
- variables: Variables that can be reused throughout the template.
- resources: The resources that will be deployed to Azure.
- outputs: Values that are returned after deployment.


## Adding a Resource to the ARM Template

###  Add a Storage Resource to the ARM Template:

To add an Azure Storage Account to your ARM template:

- Inside the resources section of (`azuredeploy.json`), add the following resource snippet:

```json
{
  "type": "Microsoft.Storage/storageAccounts",
  "apiVersion": "2023-05-01",
  "name": "storageaccount1",
  "tags": {
    "displayName": "storageaccount1"
  },
  "location": "[resourceGroup().location]",
  "kind": "StorageV2",
  "sku": {
    "name": "Premium_LRS"
  }
}
```
- type: Specifies the resource type (Microsoft.Storage/storageAccounts for a storage account).
- apiVersion: The API version of the resource.
- name: The name of the storage account.
- tags: Metadata for the resource.
- location: The location of the resource group.
- kind: The type of storage account (e.g., StorageV2).
- sku: The SKU of the storage account (e.g., Premium_LRS).
- Modify the name and displayName to something unique, change the sku to Standard_LRS, and adjust other values as needed.
- Save the file

## Deploying the Updated ARM Template

###  Deploy the ARM Template

 **1. Open the terminal in Visual Studio Code** 

 **2. Sign in to Azure** using the following command:**

  ```powershell
    Connect-AzAccount
  ```
- This will open a prompt for you to enter your Azure credentials. Once you sign in, you will be connected to your Azure subscription.

**3. Run the following command to obtain your subscription(s) and their ID(s).**

```powershell
    Get-AzSubscription
```

**4. Set the default subscription for the session:**

  ```powershell
    $context = Get-AzSubscription -SubscriptionId {Your subscription ID}
    Set-AzContext $context
  ```
- Replace {Your subscription ID} with your actual subscription ID.

**5. Set the Default Resource Group for the session**

- If you have multiple subscriptions, set the default subscription to the one where you want to deploy the resources:

```powershell
  Set-AzDefault -ResourceGroupName [sandbox resource group name]
```

- Replace [sandbox resource group name] with your desired resource group name.

**6. Deploy ARM Template:**

```powershell
$templateFile="azuredeploy.json"
$today=Get-Date -Format "MM-dd-yyyy"
$deploymentName="addstorage-"+"$today"
New-AzResourceGroupDeployment -Name $deploymentName -TemplateFile $templateFile
```

## Checking your deployment

**When the deployment finishes, go back to the Azure portal in your browser. Go to your resource group, and you see that there is now 1 Succeeded deployment. Select that link.**

Notice that the storage account is deployed.





