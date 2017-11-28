---
title: "가상 컴퓨터 확장으로 응용 프로그램 배포 aaaAutomating | Microsoft Docs"
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
ms.openlocfilehash: 38a02a4271d6b9ba02a473a51794a7bd90ca3a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="application-deployment-with-azure-resource-manager-templates-for-linux-vms"></a><span data-ttu-id="f6e1c-103">Linux VM용 Azure Resource Manager 템플릿을 사용하는 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="f6e1c-103">Application deployment with Azure Resource Manager templates for Linux VMs</span></span>

<span data-ttu-id="f6e1c-104">모든 Azure 인프라 요구 사항 파악 고 배포 템플릿을로 변환 되었습니다, 해결 toobe hello 실제 응용 프로그램 배포에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6e1c-104">Once all Azure infrastructural requirements have been identified and translated into a deployment template, hello actual application deployment needs toobe addressed.</span></span> <span data-ttu-id="f6e1c-105">여기에 응용 프로그램 배포를 Azure 리소스 tooinstalling hello 실제 응용 프로그램 이진 파일을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6e1c-105">Application deployment here is referring tooinstalling hello actual application binaries onto Azure resources.</span></span> <span data-ttu-id="f6e1c-106">Hello Music Store 샘플을.Net Core, NGINX, 및 감독자 toobe 각 가상 컴퓨터에 설치 및 구성 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6e1c-106">For hello Music Store sample, .Net Core, NGINX, and Supervisor need toobe installed and configured on each virtual machine.</span></span> <span data-ttu-id="f6e1c-107">이진 파일 toobe hello 가상 컴퓨터에 설치 해야 하는 Music Store hello 및 hello Music Store 데이터베이스 미리 만들어 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6e1c-107">hello Music Store binaries need toobe installed onto hello virtual machine, and hello Music Store database pre-created.</span></span>

<span data-ttu-id="f6e1c-108">이 문서는 가상 컴퓨터 확장 응용 프로그램 배포 및 구성 tooAzure 가상 컴퓨터를 자동화할 수 방법을 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6e1c-108">This document details how Virtual Machine extensions can automate application deployment and configuration tooAzure virtual machines.</span></span> <span data-ttu-id="f6e1c-109">모든 종속성 및 고유한 구성이 강조 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6e1c-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="f6e1c-110">Hello 최상의 경험에 대 한 미리 hello 솔루션 tooyour Azure 구독 및 Azure 리소스 관리자 템플릿 hello와 함께 작업의 인스턴스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6e1c-110">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="f6e1c-111">hello 완전 한 템플릿 여기 – 있습니다 [ubuntu 음악 스토어 배포](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux)합니다.</span><span class="sxs-lookup"><span data-stu-id="f6e1c-111">hello complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span>

## <a name="configuration-script"></a><span data-ttu-id="f6e1c-112">구성 스크립트</span><span class="sxs-lookup"><span data-stu-id="f6e1c-112">Configuration script</span></span>
<span data-ttu-id="f6e1c-113">가상 컴퓨터 확장은 tooprovide 구성 자동화 가상 컴퓨터에 대해 실행 되는 특별 한 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="f6e1c-113">Virtual Machine extensions are specialized programs that execute against virtual machines tooprovide configuration automation.</span></span> <span data-ttu-id="f6e1c-114">바이러스 백신, 로깅 구성 및 Docker 구성과 같은 여러 특정 용도로 확장을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6e1c-114">Extensions are available for many specific purposes such as anti-virus, logging configuration, and Docker configuration.</span></span> <span data-ttu-id="f6e1c-115">사용자 지정 스크립트 확장에는 모든 가상 컴퓨터에 대 한 스크립트를 사용 하는 toorun 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6e1c-115">A custom script extension can be used toorun any script against a virtual machine.</span></span> <span data-ttu-id="f6e1c-116">Hello Music Store 샘플 toohello 사용자 지정 스크립트 확장 tooconfigure hello Ubuntu 가상 컴퓨터를 사용 되며 hello 음악 스토어 응용 프로그램을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6e1c-116">With hello Music Store sample, it is up toohello custom script extension tooconfigure hello Ubuntu virtual machines and install hello Music Store application.</span></span> 

<span data-ttu-id="f6e1c-117">가상 컴퓨터 확장 된 Azure 리소스 관리자 템플릿을에서 선언 되는 방법을 자세히 보여 주는 하기 전에를 실행 하는 hello 스크립트를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6e1c-117">Before detailing how virtual machine extensions are declared in an Azure Resource Manager template, examine hello script that is run.</span></span> <span data-ttu-id="f6e1c-118">이 스크립트는 hello Ubuntu 가상 컴퓨터 toohost hello 음악 스토어 응용 프로그램을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f6e1c-118">This script configures hello Ubuntu virtual machine toohost hello Music Store application.</span></span> <span data-ttu-id="f6e1c-119">Hello 스크립트에 필요한 모든 소프트웨어 설치를 실행 하는 경우 소스 제어를 hello 음악 스토어 응용 프로그램을 설치 하 고 hello 데이터베이스를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6e1c-119">When run, hello script installs all needed software, install hello Music store application from source control, and prepare hello database.</span></span> 

<span data-ttu-id="f6e1c-120">.NET 호스팅에 대 한 더 toolearn 핵심 응용 프로그램 참조 linux [게시 tooa Linux 프로덕션 환경](https://docs.asp.net/en/latest/publishing/linuxproduction.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="f6e1c-120">toolearn more about hosting a .Net Core application on Linux, see [Publish tooa Linux production environment](https://docs.asp.net/en/latest/publishing/linuxproduction.html).</span></span>

> <span data-ttu-id="f6e1c-121">이 샘플은 데모용입니다.</span><span class="sxs-lookup"><span data-stu-id="f6e1c-121">This sample is for demonstration purposes.</span></span>
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

## <a name="vm-script-extension"></a><span data-ttu-id="f6e1c-122">VM 스크립트 확장</span><span class="sxs-lookup"><span data-stu-id="f6e1c-122">VM Script Extension</span></span>
<span data-ttu-id="f6e1c-123">VM 확장 수에 대해 실행할 수는 가상 컴퓨터 빌드 시 hello Azure 리소스 관리자 템플릿을에 hello 확장을 리소스를 포함 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6e1c-123">VM Extensions can be run against a virtual machine at build time by including hello extension resource in hello Azure Resource Manager template.</span></span> <span data-ttu-id="f6e1c-124">hello Visual Studio 추가 리소스 마법사를 사용 하거나 hello 서식 파일에 유효한 JSON을 삽입 하 여 hello 확장을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6e1c-124">hello extension can be added with hello Visual Studio Add Resource wizard, or by inserting valid JSON into hello template.</span></span> <span data-ttu-id="f6e1c-125">가상 컴퓨터 리소스; hello 안에 중첩 hello 스크립트 확장을 리소스 이 hello 다음 예제에서에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6e1c-125">hello Script Extension resource is nested inside hello Virtual Machine resource; this can be seen in hello following example.</span></span>

<span data-ttu-id="f6e1c-126">Hello 리소스 관리자 템플릿-내에서이 링크 toosee hello JSON 샘플을 따라 [VM 스크립트 확장](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L359)합니다.</span><span class="sxs-lookup"><span data-stu-id="f6e1c-126">Follow this link toosee hello JSON sample within hello Resource Manager template – [VM Script Extension](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L359).</span></span> 

<span data-ttu-id="f6e1c-127">아래 스크립트 hello JSON hello에서는 GitHub에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6e1c-127">Notice in hello below JSON that hello script is stored in GitHub.</span></span> <span data-ttu-id="f6e1c-128">이 스크립트를 Azure Blob 저장소에 저장할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6e1c-128">This script could also be stored in Azure Blob storage.</span></span> <span data-ttu-id="f6e1c-129">또한 Azure 리소스 관리자 템플릿을 사용 hello 스크립트 실행 문자열 tooconstructed는 스크립트 실행에 대 한 템플릿 매개 변수 값을 매개 변수로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6e1c-129">Also, Azure Resource Manager templates allow hello script execution string tooconstructed such that template parameters values can be used as parameters for script execution.</span></span> <span data-ttu-id="f6e1c-130">Hello 서식 파일을 배포 하는 경우 데이터는 제공 하는 경우에 되며 이러한 값 hello 스크립트를 실행할 때 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6e1c-130">In this case data is provided when deploying hello templates, and these values can then be used when executing hello script.</span></span>

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

<span data-ttu-id="f6e1c-131">Hello 사용자 지정 스크립트 확장을 사용 하 여에 대 한 자세한 내용은 참조 하십시오. [사용자 지정 스크립트 확장을 리소스 관리자 템플릿으로](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="f6e1c-131">For more information on using hello custom script extension, see [Custom script extensions with Resource Manager templates](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="next-step"></a><span data-ttu-id="f6e1c-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f6e1c-132">Next Step</span></span>
<hr>

[<span data-ttu-id="f6e1c-133">추가 Azure Resource Manager 템플릿 살펴보기</span><span class="sxs-lookup"><span data-stu-id="f6e1c-133">Explore More Azure Resource Manager Templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

