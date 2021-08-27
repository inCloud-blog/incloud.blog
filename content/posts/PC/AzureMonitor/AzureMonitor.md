---
title: "Azure Monitor"
subtitle: ""
date: 2021-08-10T21:18:26+02:00
draft: false
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
  src: "featured-image.jpg"
- name: featured-image-preview
  src: featured-image-preview.jpg

featuredImage: ""
featuredImagePreview: ""
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
- autoinstallation on all Virtual Machines 
- manual installation 
Difference is obvious and i don't need to explain that first way is comfortable and the second give us more control on cost and configuration. 
To setup automatic installation we need to modify properties of log analytics workspace that is used with Azure Monitor. 

## Data visualization



## Pricing

How much it costs? 

Current pricing list is updated on Microsoft site -> [here](https://azure.microsoft.com/en-us/pricing/details/monitor/#pricing)

## Summary