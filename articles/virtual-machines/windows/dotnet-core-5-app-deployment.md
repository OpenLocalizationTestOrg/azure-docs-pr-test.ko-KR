---
title: "가상 컴퓨터 확장을 사용하여 응용 프로그램 배포 자동화 | Microsoft Docs"
description: "Azure 가상 컴퓨터 DotNet Core 자습서"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 79c91304-6c1b-4354-a185-fecc129b139d
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f2996eef71b39c6240fac5484854f72d3e657d0f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="application-deployment-with-azure-resource-manager-templates-for-windows-vms"></a><span data-ttu-id="52711-103">Windows VM용 Azure Resource Manager 템플릿을 사용하는 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="52711-103">Application deployment with Azure Resource Manager templates for Windows VMs</span></span>

<span data-ttu-id="52711-104">모든 Azure 인프라 요구 사항을 파악하고 배포 템플릿으로 변환한 후에는 실제 응용 프로그램 배포를 해결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="52711-104">Once all Azure infrastructural requirements have been identified and translated into a deployment template, the actual application deployment needs to be addressed.</span></span> <span data-ttu-id="52711-105">여기서 진행되는 응용 프로그램 배포에서는 Azure 리소스에 실제 응용 프로그램 이진 파일이 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="52711-105">Application deployment here is referring to installing the actual application binaries onto Azure resources.</span></span> <span data-ttu-id="52711-106">Music Store 샘플의 경우 .Net Core 및 IIS를 각 가상 컴퓨터에서 설치 및 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="52711-106">For the Music Store sample, .Net Core and IIS need to be installed and configured on each virtual machine.</span></span> <span data-ttu-id="52711-107">Music Store 이진 파일을 가상 컴퓨터에 설치해야 하며 Music Store 데이터베이스를 미리 생성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="52711-107">The Music Store binaries need to be installed onto the virtual machine, and the Music Store database pre-created.</span></span>

<span data-ttu-id="52711-108">이 문서는 가상 컴퓨터 확장이 Azure 가상 컴퓨터에 대한 응용 프로그램 배포 및 구성을 자동화하는 방법을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="52711-108">This document details how Virtual Machine extensions can automate application deployment and configuration to Azure virtual machines.</span></span> <span data-ttu-id="52711-109">모든 종속성 및 고유한 구성이 강조 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="52711-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="52711-110">최상의 환경을 위해서는 솔루션 인스턴스를 Azure 구독에 미리 배포하고 Azure Resource Manager 템플릿을 따라 작업하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="52711-110">For the best experience, pre-deploy an instance of the solution to your Azure subscription and work along with the Azure Resource Manager template.</span></span> <span data-ttu-id="52711-111">전체 템플릿은 [Windows의 Music Store 배포](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52711-111">The complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="configuration-script"></a><span data-ttu-id="52711-112">구성 스크립트</span><span class="sxs-lookup"><span data-stu-id="52711-112">Configuration script</span></span>
<span data-ttu-id="52711-113">가상 컴퓨터 확장은 구성 자동화를 제공하기 위해 가상 컴퓨터에 대해 실행되는 특수한 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="52711-113">Virtual Machine extensions are specialized programs that execute against virtual machines to provide configuration automation.</span></span> <span data-ttu-id="52711-114">바이러스 백신, 로깅 구성 및 Docker 구성과 같은 여러 특정 용도로 확장을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52711-114">Extensions are available for many specific purposes such as anti-virus, logging configuration, and Docker configuration.</span></span> <span data-ttu-id="52711-115">가상 컴퓨터에 대한 스크립트를 실행하는 데 사용자 지정 스크립트 확장을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52711-115">The Custom Script extension can be used to run any script against a virtual machine.</span></span> <span data-ttu-id="52711-116">Music Store 샘플을 사용하는 경우 Windows 가상 컴퓨터를 구성하고 Music Store 응용 프로그램을 설치하는 작업은 사용자 지정 스크립트 확장이 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="52711-116">With the Music Store sample, it is up to the custom script extension to configure the Windows virtual machines and install the Music Store application.</span></span>

<span data-ttu-id="52711-117">Azure Resource Manager 템플릿에서 가상 컴퓨터 확장이 선언되는 방식을 자세히 살펴보기 전에 실행되는 스크립트를 검토해보세요.</span><span class="sxs-lookup"><span data-stu-id="52711-117">Before detailing how virtual machine extensions are declared in an Azure Resource Manager template, examine the script that is run.</span></span> <span data-ttu-id="52711-118">이 스크립트는 Music Store 응용 프로그램을 호스트하도록 Windows 가상 컴퓨터를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="52711-118">This script configures the Windows virtual machine to host the Music Store application.</span></span> <span data-ttu-id="52711-119">실행 시 이 스크립트는 필요한 모든 소프트웨어를 설치하고, 소스 제어에서 Music Store 응용 프로그램을 설치하고, 데이터베이스를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="52711-119">When run, the script installs all needed software, install the Music store application from source control, and prepare the database.</span></span> 

> <span data-ttu-id="52711-120">이 샘플은 데모용입니다.</span><span class="sxs-lookup"><span data-stu-id="52711-120">This sample is for demonstration purposes.</span></span>

```PowerShell
<#
    .SYNOPSIS
        Downloads and configures .Net Core Music Store application sample across IIS and Azure SQL DB.
#>

Param (
    [string]$user,
    [string]$password,
    [string]$sqlserver
)

# Firewall
netsh advfirewall firewall add rule name="http" dir=in action=allow protocol=TCP localport=80

# Folders
New-Item -ItemType Directory c:\temp
New-Item -ItemType Directory c:\music

# Install iis
Install-WindowsFeature web-server -IncludeManagementTools

# Install dot.net core sdk
Invoke-WebRequest http://go.microsoft.com/fwlink/?LinkID=615460 -outfile c:\temp\vc_redistx64.exe
Start-Process c:\temp\vc_redistx64.exe -ArgumentList '/quiet' -Wait
Invoke-WebRequest https://go.microsoft.com/fwlink/?LinkID=809122 -outfile c:\temp\DotNetCore.1.0.0-SDK.Preview2-x64.exe
Start-Process c:\temp\DotNetCore.1.0.0-SDK.Preview2-x64.exe -ArgumentList '/quiet' -Wait
Invoke-WebRequest https://go.microsoft.com/fwlink/?LinkId=817246 -outfile c:\temp\DotNetCore.WindowsHosting.exe
Start-Process c:\temp\DotNetCore.WindowsHosting.exe -ArgumentList '/quiet' -Wait

# Download music app
Invoke-WebRequest  https://github.com/Microsoft/dotnet-core-sample-templates/raw/master/dotnet-core-music-windows/music-app/music-store-azure-demo-pub.zip -OutFile c:\temp\musicstore.zip
Expand-Archive C:\temp\musicstore.zip c:\music

# Azure SQL connection sting in environment variable
[Environment]::SetEnvironmentVariable("Data:DefaultConnection:ConnectionString", "Server=$sqlserver;Database=MusicStore;Integrated Security=False;User Id=$user;Password=$password;MultipleActiveResultSets=True;Connect Timeout=30",[EnvironmentVariableTarget]::Machine)

# Pre-create database
$env:Data:DefaultConnection:ConnectionString = "Server=$sqlserver;Database=MusicStore;Integrated Security=False;User Id=$user;Password=$password;MultipleActiveResultSets=True;Connect Timeout=30"
Start-Process 'C:\Program Files\dotnet\dotnet.exe' -ArgumentList 'c:\music\MusicStore.dll'

# Configure iis
Remove-WebSite -Name "Default Web Site"
Set-ItemProperty IIS:\AppPools\DefaultAppPool\ managedRuntimeVersion ""
New-Website -Name "MusicStore" -Port 80 -PhysicalPath C:\music\ -ApplicationPool DefaultAppPool
& iisreset
```

## <a name="vm-script-extension"></a><span data-ttu-id="52711-121">VM 스크립트 확장</span><span class="sxs-lookup"><span data-stu-id="52711-121">VM Script Extension</span></span>
<span data-ttu-id="52711-122">VM 확장은 Azure Resource Manager 템플릿에 확장 리소스를 포함하여 빌드 시에 가상 컴퓨터에 대해 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52711-122">VM Extensions can be run against a virtual machine at build time by including the extension resource in the Azure Resource Manager template.</span></span> <span data-ttu-id="52711-123">확장은 Visual Studio 리소스 추가 마법사를 사용하거나 유효한 JSON을 템플릿에 삽입하여 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52711-123">The extension can be added with the Visual Studio Add Resource wizard, or by inserting valid JSON into the template.</span></span> <span data-ttu-id="52711-124">스크립트 확장 리소스는 가상 컴퓨터 리소스 내에 중첩되며 다음 예제에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52711-124">The Script Extension resource is nested inside the Virtual Machine resource; this can be seen in the following example.</span></span>

<span data-ttu-id="52711-125">[VM 스크립트 확장](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L339)링크를 따라 Resource Manager 템플릿 내의 JSON 샘플을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52711-125">Follow this link to see the JSON sample within the Resource Manager template – [VM Script Extension](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L339).</span></span> 

<span data-ttu-id="52711-126">GitHub에서 JSON 아래에 이 스크립트가 저장되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52711-126">Notice in the below JSON that the script is stored in GitHub.</span></span> <span data-ttu-id="52711-127">이 스크립트를 Azure Blob 저장소에 저장할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52711-127">This script could also be stored in Azure Blob storage.</span></span> <span data-ttu-id="52711-128">또한 Azure Resource Manager 템플릿을 사용하면 템플릿 매개 변수 값을 스크립트 실행에 대한 매개 변수로 사용할 수 있도록 스크립트 실행 문자열을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52711-128">Also, Azure Resource Manager templates allow the script execution string to be constructed such that template parameters values can be used as parameters for script execution.</span></span> <span data-ttu-id="52711-129">이 경우 템플릿을 배포할 때 데이터가 제공되며, 이러한 값을 스크립트 실행 시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52711-129">In this case data is provided when deploying the templates, and these values can then be used when executing the script.</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
  }
}
```

<span data-ttu-id="52711-130">위에서 설명한 대로 Azure Blob Storage에 사용자 지정 스크립트를 저장할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52711-130">As mentioned above, it is also possible to store your custom scripts in Azure Blob storage.</span></span> <span data-ttu-id="52711-131">Blob Storage에 스크립트 리소스를 저장하는 두 가지 옵션이 있습니다. 컨테이너/스크립트를 공용으로 지정하고 위와 동일한 방법을 따르거나, CustomScriptExtension 리소스 정의에 storageAccountName 및 storageAccountKey를 제공해야 사설 Blob Storage에 저장할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52711-131">There are two options for storing the script resources in blob storage; either make the container/script public and follow the same approach as above, or it can also be kept in private blob storage which requires you to provide the storageAccountName and storageAccountKey to the CustomScriptExtension resource definition.</span></span>

<span data-ttu-id="52711-132">아래 예제에서는 한 단계 더 발전한 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="52711-132">In the example below we have gone a step further.</span></span> <span data-ttu-id="52711-133">배포하는 동안 저장소 계정 이름 및 키를 매개 변수 또는 변수로 제공할 수 있지만 Resource Manager 템플릿에서는 저장소 계정 키를 프로그래밍 방식으로 가져와 배포 시 템플릿에 삽입할 수 있는 `listKeys` 함수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="52711-133">While it is possible to provide the storage account name and key as a parameter or variable during deployment, Resource Manager templates provide the `listKeys` function that can obtain the storage account key programmatically and insert it in to the template for you at deployment time.</span></span>

<span data-ttu-id="52711-134">아래의 CustomScriptExtension 리소스 정의 예제에서는 사용자 지정 스크립트가 `mysa999rgname`이라는 다른 리소스 그룹에 있는 `mystorageaccount9999`라는 Azure Storage 계정에 이미 업로드되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52711-134">In the example CustomScriptExtension resource definition below, our custom script has already been uploaded to an Azure storage account called `mystorageaccount9999` which exists in another Resource Group called `mysa999rgname`.</span></span> <span data-ttu-id="52711-135">이 리소스가 포함된 템플릿을 배포하면 `listKeys` 함수가 `mysa999rgname` 리소스 그룹의 `mystorageaccount9999` 저장소 계정에 대한 저장소 계정 키를 가져와 템플릿에 자동으로 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="52711-135">When we deploy a template containing this resource, the `listKeys` function programmatically obtains the storage account key for the storage account `mystorageaccount9999` in the Resource Group `mysa999rgname` and inserts it in to the template for us.</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.7",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://mystorageaccount9999.blob.core.windows.net/container/configure-music-app.ps1"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]",
      "storageAccountName": "mystorageaccount9999",
      "storageAccountKey": "[listKeys(resourceId('mysa999rgname','Microsoft.Storage/storageAccounts', mystorageaccount9999), '2015-06-15').key1]"
    }
  }
}
```

<span data-ttu-id="52711-136">이 방법의 주요 이점은 저장소 계정 키가 변경된 경우 템플릿 또는 배포 매개 변수를 변경할 필요가 없다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="52711-136">The main benefit of this approach is that it does not require you to change your template or deployment parameters in the event of the storage account key changing.</span></span>

<span data-ttu-id="52711-137">사용자 지정 스크립트 확장 사용에 대한 자세한 내용은 [Resource Manager 템플릿을 사용한 사용자 지정 스크립트 확장](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="52711-137">For more information on using the custom script extension, see [Custom script extensions with Resource Manager templates](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-step"></a><span data-ttu-id="52711-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="52711-138">Next Step</span></span>
<hr>

[<span data-ttu-id="52711-139">추가 Azure Resource Manager 템플릿 살펴보기</span><span class="sxs-lookup"><span data-stu-id="52711-139">Explore More Azure Resource Manager Templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

