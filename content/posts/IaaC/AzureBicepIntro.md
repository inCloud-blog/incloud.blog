---
title: "Infrastructure as a Code - Azure Bicep - First steps"
subtitle: ""
date: 2022-04-03T11:00:00+02:00
draft: true
author: "pawel.en"
description: "Infrastructure as a Code Series."
page:
    theme: "wide"
upd: ""
authorComment: "Introduction to Azure Virtual Desktop"
tags: [Infrastructure as a Code, Public Cloud, Azure Bicep]
categories: [Microsoft Azure, Infrastructure as a Code]
hiddenFromHomePage: false
hiddenFromSearch: false
featuredImage: "/img/global/Featured Image 2.jpg"
featuredImagePreview: "/img/global/Featured Image 2.jpg"
images: [""]

toc:
  enable: true
math:
  enable: false

license: ""
---

<!--more-->
## Benefits of using Azure Bicep

- Simple syntax - if You are using JSON teplates You'll see that Bicep is easier to read. 
- Repeatable results - overtime You will use Your template You'll see that results are deployed in a consistent manner.
- Modularity - You don't need to build one big template - it can be split to modules that covers set of resources.
- Integration with Azure
- No state or state files to manage
- It's totally free

## Tools

- [Own environment](http://localhost:1313/environmentpreparationpart1/)
- [Bicep playground](https://bicepdemo.z22.web.core.windows.net/)

## First template

Our first template will contain: 
- Resource group
- Azure Virtual Network

main.bicep file:
```azurecli
## scope of template - default scope is resource group but we will use subscription
targetScope = 'subscription'

## global parameters
param location string 
param rgName string
param vnetName string
param vnetAddressSpace string
param snetName_1 string
param snetAddressSpace_1 string
param snetName_2 string
param snetAddressSpace_2 string

## modules
module 'rg.bicep' = {
    
}

module 'vnet.bicep' = {


}
```
rg.bicep file:
```azurecli

```


How to run deployment? <br/>
Azure Cli:
```azurecli
az deployment subscription create \
    --name firstBicepDeployment \
    --subscription 'xxxx-yyyyy-zzzz-yyyy'
    --template-file main.bicep
    --parameters param1=value1, param2=value2
```
Powershell:
```azurepowershell
New-AzSubscriptionDeployment `
    -name firstBicepDeployment `
    -subscription 'xxxx-yyyy-zzzz-yyyy' `
    -templatefile main.bicep `
    -param1 value1 
```

## Converting

If we have JSON template from work environment we can decompile it to Bicep template. 

```azurecli
az bicep decompile --file myfile.json
```

This command will create myfile.bicep file in directory where it was run. There can be some warnings and errors that You will need to fix after decompiling. 

## Useful links

[JSON decompile to Bicep](https://docs.microsoft.com/en-us/azure/azure-resource-manager/bicep/decompile?tabs=azure-cli)<br/>
[What is Bicep?](https://docs.microsoft.com/en-us/azure/azure-resource-manager/bicep/overview?tabs=bicep)
