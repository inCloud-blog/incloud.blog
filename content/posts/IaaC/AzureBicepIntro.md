---
title: "IaaC - Azure Bicep - Pierwszy szablon"
subtitle: ""
date: 2022-05-02T11:00:00+02:00
draft: false
author: "pawel.en"
description: "Seria Infrastructure as a Code. W tej serii postaram się przedstawić wszystkie aspekty pracy z IaaC od przygotowania środowiska pracy do jego wykorzystania."
page:
    theme: "wide"

authorComment: "Introduction to Azure Virtual Desktop"
tags: [Infrastructure as a Code, Public Cloud, Azure Bicep]
categories: [Microsoft Azure, Infrastructure as a Code, Azure Bicep]
hiddenFromHomePage: false
hiddenFromSearch: false
featuredImage: "/img/global/Featured Image 1.jpg"
featuredImagePreview: "/img/global/Featured Image 1.jpg"
images: [""]

toc:
  enable: true
math:
  enable: false

license: ""
---

<!--more-->
## Korzyści

- Prosta składnia - jeśli używałeś już szablonów JSON zauważysz że Bicep jest łatwiejszy do czytania i co za tym idzie pisania
- Powtarzalne rezultaty - za każdym razem wykorzystując szablon zobaczysz dokłądenie ten sam efekt
- Modułowość - nie potrzebujemy tworzyć wielkich i ciężkich do redagowania "potworków" - możemy podzielić nasze środowisko na moduły, które są reużywalne
- Posiada integrację z Microsoft Azure
- Brak konieczności zarządzania plikami stanu
- Jest całkowicie darmowy

## Narzędzia

- [Jak przygotować środowisko](https://incloud.blog/environmentpreparationpart1/)
- [Bicep playground](https://bicepdemo.z22.web.core.windows.net/)

## Pierwszy szablon

Nasz pierwszy szablon będzie zawierał: 
- Resource group
- Azure Virtual Network

plik main.bicep:
```powershell
//określenie zakresu szablonu
targetScope = 'subscription'

//sekcja parametrów
param location string 
param rgName string
param vnetName string
param vnetAddrSpace string
param snet1AddrSpace string 
param snet2AddrSpace string
param snet3AddrSpace string  

//sekcja modułów
module resourceGroup1 'rg.bicep' = {
  name: rgName
  params: {
    location: location
    rgName: rgName
  }
}

//referencja do instniejącego wcześniej utworzonego zasobu
resource resGrp 'Microsoft.Resources/resourceGroups@2021-04-01' existing = {
  name: rgName
}

module vNetwork 'vnet.bicep' = {
  name: rgName
  scope: resGrp
  params: {
    location: location
    vnetName: vnetName
    vnetAddrSpace: vnetAddrSpace
    snet1AddrSpace: snet1AddrSpace
    snet2AddrSpace: snet2AddrSpace
    snet3AddrSpace: snet3AddrSpace
  }
}
```

plik rg.bicep:
```powershell
//określenie zakresu szablonu
targetScope = 'subscription'

//sekcja parametrów
param rgName string
param location string

//sekcja zasobów
resource resGrp 'Microsoft.Resources/resourceGroups@2021-04-01' = {
  name: rgName
  location: location
}
```

plik vnet.bicep:
```powershell
//sekcja parametrów
param vnetName string
param vnetAddrSpace string
param snet1AddrSpace string 
param snet2AddrSpace string
param snet3AddrSpace string  
param location string
//sekcja zmiennych
var snet2Name = 'AzureBastionSubnet'
var snet3Name = 'GatewaySubnet'
var snet1Name = 'default'

//sekcja zasobów
resource vnet 'Microsoft.Network/virtualNetworks@2019-11-01' = {
    name: vnetName
    location: location
    properties: {
      addressSpace: {
        addressPrefixes: [
          vnetAddrSpace
        ]
      }
      subnets: [
        {
          name: snet1Name
          properties: {
            addressPrefix: snet1AddrSpace
          }
        }
        {
          name: snet2Name
          properties: {
            addressPrefix: snet2AddrSpace
          }
        }
        {
          name: snet3Name
          properties: {
            addressPrefix: snet3AddrSpace
          }
        }
      ]
    }
}
```

Jak uruchomić wdrożenie? <br/>
Azure Cli:
```azurecli
az deployment sub create \
    --name firstBicepDeployment \
    --subscription 'xxxx-yyyyy-zzzz-yyyy'
    --template-file main.bicep
    --parameters param1=value1, param2=value2
    --location westeurope
```

PowerShell:
```azurepowershell
New-AzSubscriptionDeployment `
    -name firstBicepDeployment `
    -subscription 'xxxx-yyyy-zzzz-yyyy' `
    -templatefile main.bicep `
    -param1 value1 
    -param2 value2
```

Ja użyłem takiego zestawu parametrów: 
```azurecli
az deployment sub create \
    --name firstBicepDeployment \
    --subscription 'xxxx-yyyyy-zzzz-yyyy'
    --template-file main.bicep
    --parameters location=westeurope rgName=azr-tst-rg vnetName=azr-tst-vnet-001 vnetAddrSpace=10.0.0.0/16 snet1AddrSpace=10.0.0.0/24 snet2AddrSpace=10.0.253.0/24 snet3AddrSpace=10.0.254.0/24
    --location westeurope
```


## Konwertowanie

Jeśli posiadamy szablon JSON wyeksportowany z działającego środowiska możemy go przekonwertować na Bicep za pomocą poniższej komendy: 

```azurecli
az bicep decompile --file myfile.json
```

Komenda ta utworzy plik mybicep.bicep w katalogu, w którym zostanie uruchomiona. Mogą pojawić się ostrzeżenia lub błędy podczas dekompilowania - będziemy musieli się nimi zając przed użyciem takiego szablonu ale o tym w osobnym artykule.

## Przydatne Linki

[JSON decompile to Bicep](https://docs.microsoft.com/en-us/azure/azure-resource-manager/bicep/decompile?tabs=azure-cli)<br/>
[What is Bicep?](https://docs.microsoft.com/en-us/azure/azure-resource-manager/bicep/overview?tabs=bicep)<br/>
[GitHub Repo](https://github.com/pchylak/inCloud.blog/tree/main/IaaC/AzureBicepIntro)
