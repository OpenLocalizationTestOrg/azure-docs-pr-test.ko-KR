---
title: "가상 컴퓨터 확장을 사용하여 응용 프로그램 배포 자동화 | Microsoft Docs"
description: "Azure 가상 컴퓨터 DotNet Core 자습서"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 9fc8b1ba-60f5-410b-8190-9f1ff885e50e
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2f972fef75aa8e13af7dab908c2b0e2ec28f1324
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="application-deployment-with-azure-resource-manager-templates-for-linux-vms"></a><span data-ttu-id="8bab0-103">Linux VM용 Azure Resource Manager 템플릿을 사용하는 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="8bab0-103">Application deployment with Azure Resource Manager templates for Linux VMs</span></span>

<span data-ttu-id="8bab0-104">모든 Azure 인프라 요구 사항을 파악하고 배포 템플릿으로 변환한 후에는 실제 응용 프로그램 배포를 해결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bab0-104">Once all Azure infrastructural requirements have been identified and translated into a deployment template, the actual application deployment needs to be addressed.</span></span> <span data-ttu-id="8bab0-105">여기서 진행되는 응용 프로그램 배포에서는 Azure 리소스에 실제 응용 프로그램 이진 파일이 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bab0-105">Application deployment here is referring to installing the actual application binaries onto Azure resources.</span></span> <span data-ttu-id="8bab0-106">Music Store 샘플의 경우 .Net Core, NGINX 및 Supervisor를 각 가상 컴퓨터에서 설치 및 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bab0-106">For the Music Store sample, .Net Core, NGINX, and Supervisor need to be installed and configured on each virtual machine.</span></span> <span data-ttu-id="8bab0-107">Music Store 이진 파일을 가상 컴퓨터에 설치해야 하며 Music Store 데이터베이스를 미리 생성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bab0-107">The Music Store binaries need to be installed onto the virtual machine, and the Music Store database pre-created.</span></span>

<span data-ttu-id="8bab0-108">이 문서는 가상 컴퓨터 확장이 Azure 가상 컴퓨터에 대한 응용 프로그램 배포 및 구성을 자동화하는 방법을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8bab0-108">This document details how Virtual Machine extensions can automate application deployment and configuration to Azure virtual machines.</span></span> <span data-ttu-id="8bab0-109">모든 종속성 및 고유한 구성이 강조 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bab0-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="8bab0-110">최상의 환경을 위해서는 솔루션 인스턴스를 Azure 구독에 미리 배포하고 Azure Resource Manager 템플릿을 따라 작업하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8bab0-110">For the best experience, pre-deploy an instance of the solution to your Azure subscription and work along with the Azure Resource Manager template.</span></span> <span data-ttu-id="8bab0-111">전체 템플릿은 [Ubuntu의 Music Store 배포](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bab0-111">The complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span>

## <a name="configuration-script"></a><span data-ttu-id="8bab0-112">구성 스크립트</span><span class="sxs-lookup"><span data-stu-id="8bab0-112">Configuration script</span></span>
<span data-ttu-id="8bab0-113">가상 컴퓨터 확장은 구성 자동화를 제공하기 위해 가상 컴퓨터에 대해 실행되는 특수한 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="8bab0-113">Virtual Machine extensions are specialized programs that execute against virtual machines to provide configuration automation.</span></span> <span data-ttu-id="8bab0-114">바이러스 백신, 로깅 구성 및 Docker 구성과 같은 여러 특정 용도로 확장을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bab0-114">Extensions are available for many specific purposes such as anti-virus, logging configuration, and Docker configuration.</span></span> <span data-ttu-id="8bab0-115">가상 컴퓨터에 대한 스크립트를 실행하는 데 사용자 지정 스크립트 확장을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bab0-115">A custom script extension can be used to run any script against a virtual machine.</span></span> <span data-ttu-id="8bab0-116">Music Store 샘플을 사용하는 경우 Ubuntu 가상 컴퓨터를 구성하고 Music Store 응용 프로그램을 설치하는 작업은 사용자 지정 스크립트 확장이 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="8bab0-116">With the Music Store sample, it is up to the custom script extension to configure the Ubuntu virtual machines and install the Music Store application.</span></span> 

<span data-ttu-id="8bab0-117">Azure Resource Manager 템플릿에서 가상 컴퓨터 확장이 선언되는 방식을 자세히 살펴보기 전에 실행되는 스크립트를 검토해보세요.</span><span class="sxs-lookup"><span data-stu-id="8bab0-117">Before detailing how virtual machine extensions are declared in an Azure Resource Manager template, examine the script that is run.</span></span> <span data-ttu-id="8bab0-118">이 스크립트는 Music Store 응용 프로그램을 호스트하도록 Ubuntu 가상 컴퓨터를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8bab0-118">This script configures the Ubuntu virtual machine to host the Music Store application.</span></span> <span data-ttu-id="8bab0-119">실행 시 이 스크립트는 필요한 모든 소프트웨어를 설치하고, 소스 제어에서 Music Store 응용 프로그램을 설치하고, 데이터베이스를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="8bab0-119">When run, the script installs all needed software, install the Music store application from source control, and prepare the database.</span></span> 

<span data-ttu-id="8bab0-120">Linux의 .Net Core 응용 프로그램 호스트에 대한 자세한 내용은 [Linux 프로덕션 환경에 게시](https://docs.asp.net/en/latest/publishing/linuxproduction.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8bab0-120">To learn more about hosting a .Net Core application on Linux, see [Publish to a Linux production environment](https://docs.asp.net/en/latest/publishing/linuxproduction.html).</span></span>

> <span data-ttu-id="8bab0-121">이 샘플은 데모용입니다.</span><span class="sxs-lookup"><span data-stu-id="8bab0-121">This sample is for demonstration purposes.</span></span>
> 
> 

```bash
#!/bin/bash

# install dotnet core
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list'
sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
sudo apt-get update
sudo apt-get install -y dotnet-dev-1.0.0-preview2-003121

# download application
sudo wget https://raw.github.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/music-app/music-store-azure-demo-pub.tar /
sudo mkdir /opt/music
sudo tar -xf music-store-azure-demo-pub.tar -C /opt/music

# install nginx, update config file
sudo apt-get install -y nginx
sudo service nginx start
sudo touch /etc/nginx/sites-available/default
sudo wget https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/music-app/nginx-config/default -O /etc/nginx/sites-available/default
sudo cp /opt/music/nginx-config/default /etc/nginx/sites-available/
sudo nginx -s reload

# update and secure music config file
sed -i "s/<replaceserver>/$1/g" /opt/music/config.json
sed -i "s/<replaceuser>/$2/g" /opt/music/config.json
sed -i "s/<replacepass>/$3/g" /opt/music/config.json
sudo chown $2 /opt/music/config.json
sudo chmod 0400 /opt/music/config.json

# config supervisor
sudo apt-get install -y supervisor
sudo touch /etc/supervisor/conf.d/music.conf
sudo wget https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/music-app/supervisor/music.conf -O /etc/supervisor/conf.d/music.conf
sudo service supervisor stop
sudo service supervisor start

# pre-create music store database
/usr/bin/dotnet /opt/music/MusicStore.dll &
```

## <a name="vm-script-extension"></a><span data-ttu-id="8bab0-122">VM 스크립트 확장</span><span class="sxs-lookup"><span data-stu-id="8bab0-122">VM Script Extension</span></span>
<span data-ttu-id="8bab0-123">VM 확장은 Azure Resource Manager 템플릿에 확장 리소스를 포함하여 빌드 시에 가상 컴퓨터에 대해 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bab0-123">VM Extensions can be run against a virtual machine at build time by including the extension resource in the Azure Resource Manager template.</span></span> <span data-ttu-id="8bab0-124">확장은 Visual Studio 리소스 추가 마법사를 사용하거나 유효한 JSON을 템플릿에 삽입하여 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bab0-124">The extension can be added with the Visual Studio Add Resource wizard, or by inserting valid JSON into the template.</span></span> <span data-ttu-id="8bab0-125">스크립트 확장 리소스는 가상 컴퓨터 리소스 내에 중첩되며 다음 예제에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bab0-125">The Script Extension resource is nested inside the Virtual Machine resource; this can be seen in the following example.</span></span>

<span data-ttu-id="8bab0-126">[VM 스크립트 확장](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L359)링크를 따라 Resource Manager 템플릿 내의 JSON 샘플을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bab0-126">Follow this link to see the JSON sample within the Resource Manager template – [VM Script Extension](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L359).</span></span> 

<span data-ttu-id="8bab0-127">GitHub에서 JSON 아래에 이 스크립트가 저장되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bab0-127">Notice in the below JSON that the script is stored in GitHub.</span></span> <span data-ttu-id="8bab0-128">이 스크립트를 Azure Blob 저장소에 저장할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bab0-128">This script could also be stored in Azure Blob storage.</span></span> <span data-ttu-id="8bab0-129">또한 Azure Resource Manager 템플릿을 사용하면 템플릿 매개 변수 값을 스크립트 실행에 대한 매개 변수로 사용할 수 있도록 스크립트 실행 문자열을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bab0-129">Also, Azure Resource Manager templates allow the script execution string to constructed such that template parameters values can be used as parameters for script execution.</span></span> <span data-ttu-id="8bab0-130">이 경우 템플릿을 배포할 때 데이터가 제공되며, 이러한 값을 스크립트 실행 시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bab0-130">In this case data is provided when deploying the templates, and these values can then be used when executing the script.</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

<span data-ttu-id="8bab0-131">사용자 지정 스크립트 확장 사용에 대한 자세한 내용은 [Resource Manager 템플릿을 사용한 사용자 지정 스크립트 확장](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8bab0-131">For more information on using the custom script extension, see [Custom script extensions with Resource Manager templates](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="next-step"></a><span data-ttu-id="8bab0-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8bab0-132">Next Step</span></span>
<hr>

[<span data-ttu-id="8bab0-133">추가 Azure Resource Manager 템플릿 살펴보기</span><span class="sxs-lookup"><span data-stu-id="8bab0-133">Explore More Azure Resource Manager Templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

