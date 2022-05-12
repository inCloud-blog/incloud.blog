---
title: "Infrastructure as a Code - Environment preparation - Part 1"
subtitle: "Windows 10/11"
date: 2022-03-26T12:00:00+02:00
draft: true
author: "pawel.en"
description: "Infrastructure as a Code Series. In this series I'll show how to start with IaaC"
page:
    theme: "wide"
upd: ""
authorComment: "Introduction to IaaC"
tags: [Infrastructure as a Code, Public Cloud]
categories: [Microsoft Azure]
hiddenFromHomePage: false
hiddenFromSearch: false
featuredImage: "/img/global/Featured Image 3.jpg"
featuredImagePreview: "/img/global/Featured Image 3.jpg"
images: [""]

toc:
  enable: true
math:
  enable: false

license: ""
---

<!--more-->
## Introduction

Why to use Infrastructure as a Code? 

My first think is: to reduce natural human mistakes. Second is that I'm little lazy so I like to use some automations in my work and bicep, ARM templates are very helpfull. 

Every resource is defined by template, image or script - when we need to create resources we are using prepared templates and fill only parameter values. 
In public cloud one mistake can cost a lot of money so... let's start.

If You are starting with Infrastructure as a Code, You'll need ready environment to work with templates, images, etc. 
The main goal of this article is creating that environment.
First article describes how to configure Windows 10/11 OS client.

## Configuration

In case of preparing environment I'll use chocolatey as package provider for Windows 10/11. After installation we need to restart Powershell Console or Terminal.

``` Powershell
 Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1')) 
```

Second step is installation of Visual Studio Code and extensions to Bicep, Terraform, Powershell

``` Powershell
choco install vscode -y

code --install-extension ms-azuretools.vscode-bicep; 
code --install-extension ms-azuretools.vscode-azureterraform 
code --install-extension ms-vscode.azure-account 
code --install-extension ms-vscode.powershell 
code --install-extension redhat.vscode-yaml
code --install-extension ms-azuretools.vscode-docker 
```

Next step is installing packages that we need is Azure Cli to operate with our Cloud Environments and Docker to manage images, containers, etc.

``` Powershell
choco install azure-cli -y
choco install docker-desktop -y
```

After installation You can start work with templates, images, scripts.

## Updates

Everything You can update by using

``` Powershell
choco update [Package Name]
```

## Links

[Github Repo](https://github.com/pchylak/inCloud.blog/blob/main/IaaC/WindowsEnvScript.md)