﻿---
title: How to use Azure CLI 2.0 and the IoT extension to manage device provisioning services | Microsoft Docs
description: Learn how to use Azure CLI 2.0 and the IoT extension to manage device provisioning services
services: iot-dps 
keywords: 
author: chrissie926
ms.author: menchi
ms.date: 01/17/2018
ms.topic: tutorial
ms.service: iot-dps

documentationcenter: ''
manager: timlt
ms.devlang: na
ms.custom: mvc
---

# How to use Azure CLI 2.0 and the IoT extension to manage device provisioning services

[Azure CLI 2.0](https://docs.microsoft.com/cli/azure?view=azure-cli-latest) is an open-source cross platform command-line tool for managing Azure resources such as IoT Edge. Azure CLI 2.0 is available on Windows, Linux, and MacOS. Azure CLI 2.0 enables you to manage Azure IoT Hub resources, device provisioning service instances, and linked-hubs out of the box.

The IoT extension enriches Azure CLI 2.0 with features such as device management and full IoT Edge capability.

In this tutorial, you first complete the steps to setup Azure CLI 2.0 and the IoT extension. Then you learn how to run CLI commands to perform basic device provisioning service operations. 

## Installation 

### Step 1 - Install Python

[Python 2.7x or Python 3.x](https://www.python.org/downloads/) is required.

### Step 2 - Install Azure CLI 2.0

Follow the [installation instruction](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) to setup Azure CLI 2.0 in your environment. At a minimum, your Azure CLI 2.0 version must be 2.0.24 or above. Use `az –version` to validate. This version supports az extension commands and introduces the Knack command framework. One simple way to install on Windows is to download and install the [MSI](https://aka.ms/InstallAzureCliWindows).

### Step 3 - Install IoT extension

[The IoT extension readme](https://github.com/Azure/azure-iot-cli-extension) describes several ways to install the extension. The simplest way is to run `az extension add --name azure-cli-iot-ext`. After installation, you can use `az extension list` to validate the currently installed extensions or `az extension show --name azure-cli-iot-ext` to see details about the IoT extension. To remove the extension, you can use `az extension remove --name azure-cli-iot-ext`.


## Basic device provisioning service operations
The example shows you how to log in to your Azure account, create an Azure Resource Group (a container that holds related resources for an Azure solution), create an IoT Hub, create a device provisioning servie, list the existing device provisioning services and create a linked IoT hub with CLI commands. 

Complete the installation steps described previously before you begin. If you don't have an Azure account yet, you can [create a free account](https://azure.microsoft.com/free/?v=17.39a) today. 


### 1. Log in to the Azure account
  
    az login

![login][1]

### 2. Create a resource group IoTHubBlogDemo in eastus

    az group create -l eastus -n IoTHubBlogDemo

![Create resource group][2]


### 3. Create two device provisioning services

    az iot dps create --resource-group IoTHubBlogDemo --name demodps

![Create DPS][3]

    az iot dps create --resource-group IoTHubBlogDemo --name demodps2

### 4. List all the existing device provisioning services under this resource group

    az iot dps list --resource-group IoTHubBlogDemo

![List DPS][4]


### 5. Create an IoT Hub blogDemoHub under the newly created resource group

    az iot hub create --name blogDemoHub --resource-group IoTHubBlogDemo

![Create IoT Hub][5]

### 6. Link one existing IoT Hub to a device provisioning service

    az iot dps linked-hub create --resource-group IoTHubBlogDemo --dps-name demodps --connection-string <connection string> -l westus

![Link Hub][5]

<!-- Images -->
[1]: ./media/how-to-manage-dps-with-cli/login.jpg
[2]: ./media/how-to-manage-dps-with-cli/create-resource-group.jpg
[3]: ./media/how-to-manage-dps-with-cli/create-dps.jpg
[4]: ./media/how-to-manage-dps-with-cli/list-dps.jpg
[5]: ./media/how-to-manage-dps-with-cli/create-hub.jpg
[6]: ./media/how-to-manage-dps-with-cli/link-hub.jpg


## Next steps
In this tutorial, you learned how to:

> [!div class="checklist"]
> * Enroll the device
> * Start the device
> * Verify the device is registered

Advance to the next tutorial to learn how to provision multiple devices across load-balanced hubs. 

> [!div class="nextstepaction"]
> [Provision devices across load-balanced IoT hubs](./tutorial-provision-multiple-hubs.md)
