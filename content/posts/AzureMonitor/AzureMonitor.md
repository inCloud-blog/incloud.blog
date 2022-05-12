---
title: "Azure Monitor"
subtitle: ""
date: 2021-08-10T21:18:26+02:00
draft: true
author: "pawel.en"
description: ""

page:
    theme: "wide"

upd: ""
authorComment: ""

tags: [Microsoft Azure, Azure Monitor]
categories: [Microsoft Azure]

hiddenFromHomePage: false
hiddenFromSearch: false

resources:
- name: "featured-image"
  src: "/img/PC/AzureMonitor/img/featured-image.png"
- name: "featured-image-preview"
  src: "/img/PC/AzureMonitor/img/featured-image-preview.png"

featuredImage: "/img/PC/AzureMonitor/img/featured-image.png"
featuredImagePreview: "/img/PC/AzureMonitor/img/featured-image-preview.png"
images: [""]

toc:
  enable: true
math:
  enable: false

license: ""
---

## Prologue

In this time, in modern IT departments cloud computing and especialy public cloud is something normal. Most of workloads are running in local datacenter but we don’t afraid new posibilities of public cloud - it’s a fact. We know how to build and use environments and how to deliver necessary resources to business need. But do we really have ability and knowledge to extract and visualize important data from our public cloud environments? Do we know what’s more important - security logs, sys logs or usage/performance data?

In next four articles I’ll try to demonstrate three most popular utilities to collect, visualize and share operational dashboards.
I don't show You which data is more important but i will show You how to visualize it.

This article is first in this series:

[x] [Azure Monitor](/azuremonitor/)

[ ] [Azure Monitor and Grafana integration](/azuremonitor-grafana/)

[ ] [Azure Monitor and Elasticsearch/Kibana integration](/azuremonitor-elkkibana/)


## Prerequisites

+ Azure Subscription - it can be any type (I'll talk about pricing at the end of this article)
+ Monitored resources with Azure Monitor deployer
+ Some time to configure everything

## Azure Monitor configuration

Azure Monitor is a native Microsft Azure tool. It provides ability to collect, visualize and respond to our environment needs. 
We can colelct:
- logs
- metrics

Regarding to this data we can create alerts and notifications. 
In the second hand we can visualize metrics from our environment.
First thing that we must consider is how to implement Azure Monitor Agent - there is two ways to archive that:
- automatic installation on all Virtual Machines 
- manual installation 

Difference is obvious and i don't need to explain that first way is comfortable. Don't go into manual tasks, it's wrong way. 
To setup automatic installation we need to use ARM Templates, Azure Automation or VM Extension, more details maybe in another article. 

ARM Template:
```JSON
{
    "type": "extensions",
    "name": "OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "*WorkspaceId*"
        },
        "protectedSettings": {
            "workspaceKey": "*WorkspaceKey*"
        }
    }
}
```
Az cli:
```bash
az vm extension set --name AzureMonitorWindowsAgent --publisher Microsoft.Azure.Monitor --ids "full id of VM"
```
or
```bash
az vm extension set --name AzureMonitorLinuxAgent --publisher Microsoft.Azure.Monitor --ids "full id of VM"
```
Azure powershell: 
```powershell
Set-AzVMExtension -Name AMAWindows -ExtensionType AzureMonitorWindowsAgent -Publisher Microsoft.Azure.Monitor -ResourceGroupName "RG_name" -VMName "VM_name" -Location "Location" -TypeHandlerVersion 1.0
```

## Data visualization

Next steps are more interesting because we have data and we can develop a views and dashboards. First step is to realize what we need to know about environment. 

## Pricing

How much it costs? 

Current pricing list is updated on Microsoft site -> [here](https://azure.microsoft.com/en-us/pricing/details/monitor/#pricing)

## Summary