---
title: "Infrastructure as a Code - Przygotwanie środowiska pracy - Część 2"
subtitle: "MacOS"
date: 2022-04-23T12:00:00+02:00
draft: true
author: "pawel.en"
description: "Seria Infrastructure as a Code. W tej serii postaram się przedstawić wszystkie aspekty pracy z IaaC od przygotowania środowiska do jego wykorzystania."
page:
    theme: "wide"
upd: ""
authorComment: "Wprowadzenie do IaaC"
tags: [Infrastructure as a Code, Public Cloud]
categories: [Microsoft Azure]
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
## Wprowadzenie

Po co wykorzystywać Infrastructure as a Code? 

Pierwsza odpowiedź, która się nasuwa to: aby uniknąć ludzkich błędów. Dodatkowo jestem dość leniwy więc automatyzacja i szablony są bardzo pomocne aby upodobanie to pielęgnować.
Jeśli masz zrobić coś więcej niż raz - jest to odpowiedni moment do zastosowania szablonów, skryptów i automatyzacji. 

Każdy zasób chmurowy może być zdefiniowany jako szablon, obraz lub skrypt - kiedy potrzebujemy utworzyć lub zmodyfikować środowisko używamy gotowych szablonów uzupełniając je o niezbędne parametry. W chmurze publicznej pomyłka może okazać się dość kosztowna więc aby uniknąć dodatkowych wydatków ... zaczynajmy przygodę.

Jeśli zaczynasz przygodę z Infrastructure as a Code będziesz potrzebował odpowiednio przygotowanego środowiska do pracy z szablonami (ARM, Bicep, Terraform), obrazami kontenerów, skryptami.

Ta część poświęcona jest konfiguracji systemu MacOS.

## Konfiguracja

W moim przypadku wykorzystałem Chocolatey do pełnej konfiguracji środowiska, pobrania i zainstalowania niezbędnych binariów. Wszystko można wykonać ręcznie korzystając z przeglądarki i ręcznie wszystko instalować ale środowisko będzie zapewne powoływane nie jeden raz więc proces automatyzacji zaczynamy od tego miejsca! Uruchamiamy następujące polecenia w PowerShell/Terminal-u: 

``` Powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; 
[System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; 
iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1')) 
```

Po instalacji należy uruchomić Terminal/PowerShell ponownie. Drugi krok to instalacja Visual Studio Code oraz jego rozszerzeń do Bicep, Terraform, PowerShell, etc.

``` Powershell
choco install vscode -y
```

Należy ponownie uruchomić Terminal/PowerShell.

``` Powershell
code --install-extension ms-azuretools.vscode-bicep; 
code --install-extension ms-azuretools.vscode-azureterraform 
code --install-extension ms-vscode.azure-account 
code --install-extension ms-vscode.powershell 
code --install-extension redhat.vscode-yaml
code --install-extension ms-azuretools.vscode-docker 
```

Następnie instalujemy pakiety Azure CLI, git oraz Docker - wspomogą nasze prace.

``` Powershell
choco install azure-cli -y
choco install docker-desktop -y
choco install docker-engine -y
choco install git -y
```

Po instalacji mamy środowisko gotowe do pracy. Wystarczy uruchomić Visual Studio Code i wydzielonym katalogu zacząć tworzyć szablony, skrypty oraz obrazy. To jest temat na kolejne artykuły.

## Change Log

Poniżej będą przedstawione zmiany w dokumencie.

v1.0 - Publikacja dokumentu


## Linki

[Github Repo](https://github.com/pchylak/inCloud.blog/blob/main/IaaC/WindowsEnvScript.md)