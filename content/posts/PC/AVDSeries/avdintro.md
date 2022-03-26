---
title: "Azure Virtual Desktop - Introduction"
subtitle: "Part 1: Requirements management"
date: 2022-01-28T11:18:26+02:00
draft: true
author: "pawel.en"
description: "First part of Azure Virtual Desktop Series. In this series I'll show how to plan deployment in few steps."

page:
    theme: "wide"

upd: ""
authorComment: "Introduction to Azure Virtual Desktop"

tags: [Microsoft Azure, Azure Virtual Desktops]
categories: [Microsoft Azure, Remote Work, Virtual Desktops]

hiddenFromHomePage: false
hiddenFromSearch: false

resources:
- name: "featured-image-preview"
  src: "/img/global/Featured Image 1.jpg"
- name: "featured-image"
  src: "/img/PC/AVDSeries/img/Azure Virtual Desktop - Introduction 3.jpg"

featuredImage: "/img/PC/AVDSeries/img/Azure Virtual Desktop - Introduction 3.jpg"
featuredImagePreview: "/img/global/Featured Image 1.jpg"
images: [""]

toc:
  enable: true
math:
  enable: false

license: ""
---

<!--more-->

## Introduction

There is many articles describing how to implement virtual desktops in Microsoft Azure. I'll try to take full picture of this service in this blog post series. In first part I'll introduce requirements management. Starting from basic architecture I'll add new features and possibilities in next articles.  

## About Azure Virtual Desktop

Azure Virtual Desktop is an cloud service that provides possibility to organize remote work via virtual desktops and remote apps. That helps IT teams to handle access to company resoureces in COVID-19 pandemic time and not only then. If You consider to use this solution I hope this articles will help You to realize how to implement AVD. 

## Requirements

+ Azure Subscription - it can be any type (I'll talk about pricing at the end of this article)
+ Requirements defined (eg. applications, number of users - described below)
+ Licenses (described in next point)
+ Some time to configure everything

## Licensing requirements

To use Azure Virtual Desktop You need one of the following licenses:
For VM with Windows client OS (eg. Windows 10 Multisession, Windows 7):
+ Microsoft 365 E3/E5, A3/A5/Student use Benefit
+ Microsoft 365 Business Premium
+ Windows 10 Enterprise E3/E5, A3/A5
+ Windows 10 VDA

All licenses in "per user" model.

For VM with Windows Server:
+ RDS CAL with Software Assurance

## Requirements management

To simplify this process I'll recommed to use table below. All requirements in one place - it is better way to keep everything in documented form. 
If requirements will change You just need to update values.

| Requirement          | Type                | Value              |
|----------------------|---------------------|--------------------|
| Number of users      | required            | 50                 |
| Type of load         | required            | light              |
| OS                   | required            | Windows 10         |
| List of apps         | recommended         | O365 apps          |
| Work Hours           | recommended         | 24/7               |
| Security             | recommended         | Defender for Cloud |
| Profile redirection  | optional            | no                 |
| Access type          | required            | pooled             |
| Concurrency          | required            | 60%                |
| Connection to local environment | required         | no connection      |


In my case I have light load in environment (apps need less resources to work). 
I don't need profile redirection and I'll use Defender for Cloud as a security tool to detect weak points of config. For VM OS I want to use Windows 10 Multisession with O365 apps installed.


## Azure Costs

For my environment 

| Resource name         | Quantity            | Unit price          | Total price       |
|-----------------------|---------------------|---------------------|-------------------|
| Azure Virtual Desktop * | 1 | 353.18 € | 353.18€ |

*) in this position we have 2 virtual machines that will be work for 730 hours per month with managed premium OS disks 127 GB. 

## Next steps

In next 2 weeks I'll add next articles:
+ Different deployment scenerios with scripts and templates
+ Cost optimization
+ Profiles redirection

## Copyrights & links 

+ <a href="https://pl.freepik.com/zdjecia/biznes" target="_blank">Header picture in this article created by Jannoon028</a>
+ <a href="https://azure.microsoft.com/en-us/services/virtual-desktop/" target="_blank">Azure Virtual Desktop - Microsoft site</a>
+ <a href="https://github.com/pchylak/inCloud.blog/tree/main/AzureVirtualDesktop/BasicScenerio">GitHub - AVD Basic Scenerio</a>

