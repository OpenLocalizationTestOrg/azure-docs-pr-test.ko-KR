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
# <a name="application-deployment-with-azure-resource-manager-templates-for-windows-vms"></a>Windows VM용 Azure Resource Manager 템플릿을 사용하는 응용 프로그램 배포

모든 Azure 인프라 요구 사항을 파악하고 배포 템플릿으로 변환한 후에는 실제 응용 프로그램 배포를 해결해야 합니다. 여기서 진행되는 응용 프로그램 배포에서는 Azure 리소스에 실제 응용 프로그램 이진 파일이 설치됩니다. Music Store 샘플의 경우 .Net Core 및 IIS를 각 가상 컴퓨터에서 설치 및 구성해야 합니다. Music Store 이진 파일을 가상 컴퓨터에 설치해야 하며 Music Store 데이터베이스를 미리 생성해야 합니다.

이 문서는 가상 컴퓨터 확장이 Azure 가상 컴퓨터에 대한 응용 프로그램 배포 및 구성을 자동화하는 방법을 자세히 설명합니다. 모든 종속성 및 고유한 구성이 강조 표시됩니다. 최상의 환경을 위해서는 솔루션 인스턴스를 Azure 구독에 미리 배포하고 Azure Resource Manager 템플릿을 따라 작업하는 것이 좋습니다. 전체 템플릿은 [Windows의 Music Store 배포](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows)에서 확인할 수 있습니다.

## <a name="configuration-script"></a>구성 스크립트
가상 컴퓨터 확장은 구성 자동화를 제공하기 위해 가상 컴퓨터에 대해 실행되는 특수한 프로그램입니다. 바이러스 백신, 로깅 구성 및 Docker 구성과 같은 여러 특정 용도로 확장을 사용할 수 있습니다. 가상 컴퓨터에 대한 스크립트를 실행하는 데 사용자 지정 스크립트 확장을 사용할 수 있습니다. Music Store 샘플을 사용하는 경우 Windows 가상 컴퓨터를 구성하고 Music Store 응용 프로그램을 설치하는 작업은 사용자 지정 스크립트 확장이 담당합니다.

Azure Resource Manager 템플릿에서 가상 컴퓨터 확장이 선언되는 방식을 자세히 살펴보기 전에 실행되는 스크립트를 검토해보세요. 이 스크립트는 Music Store 응용 프로그램을 호스트하도록 Windows 가상 컴퓨터를 구성합니다. 실행 시 이 스크립트는 필요한 모든 소프트웨어를 설치하고, 소스 제어에서 Music Store 응용 프로그램을 설치하고, 데이터베이스를 준비합니다. 

> 이 샘플은 데모용입니다.

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

## <a name="vm-script-extension"></a>VM 스크립트 확장
VM 확장은 Azure Resource Manager 템플릿에 확장 리소스를 포함하여 빌드 시에 가상 컴퓨터에 대해 실행할 수 있습니다. 확장은 Visual Studio 리소스 추가 마법사를 사용하거나 유효한 JSON을 템플릿에 삽입하여 추가할 수 있습니다. 스크립트 확장 리소스는 가상 컴퓨터 리소스 내에 중첩되며 다음 예제에서 볼 수 있습니다.

[VM 스크립트 확장](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L339)링크를 따라 Resource Manager 템플릿 내의 JSON 샘플을 볼 수 있습니다. 

GitHub에서 JSON 아래에 이 스크립트가 저장되어 있습니다. 이 스크립트를 Azure Blob 저장소에 저장할 수도 있습니다. 또한 Azure Resource Manager 템플릿을 사용하면 템플릿 매개 변수 값을 스크립트 실행에 대한 매개 변수로 사용할 수 있도록 스크립트 실행 문자열을 구성할 수 있습니다. 이 경우 템플릿을 배포할 때 데이터가 제공되며, 이러한 값을 스크립트 실행 시 사용할 수 있습니다.

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

위에서 설명한 대로 Azure Blob Storage에 사용자 지정 스크립트를 저장할 수도 있습니다. Blob Storage에 스크립트 리소스를 저장하는 두 가지 옵션이 있습니다. 컨테이너/스크립트를 공용으로 지정하고 위와 동일한 방법을 따르거나, CustomScriptExtension 리소스 정의에 storageAccountName 및 storageAccountKey를 제공해야 사설 Blob Storage에 저장할 수도 있습니다.

아래 예제에서는 한 단계 더 발전한 방법을 보여 줍니다. 배포하는 동안 저장소 계정 이름 및 키를 매개 변수 또는 변수로 제공할 수 있지만 Resource Manager 템플릿에서는 저장소 계정 키를 프로그래밍 방식으로 가져와 배포 시 템플릿에 삽입할 수 있는 `listKeys` 함수를 제공합니다.

아래의 CustomScriptExtension 리소스 정의 예제에서는 사용자 지정 스크립트가 `mysa999rgname`이라는 다른 리소스 그룹에 있는 `mystorageaccount9999`라는 Azure Storage 계정에 이미 업로드되어 있습니다. 이 리소스가 포함된 템플릿을 배포하면 `listKeys` 함수가 `mysa999rgname` 리소스 그룹의 `mystorageaccount9999` 저장소 계정에 대한 저장소 계정 키를 가져와 템플릿에 자동으로 삽입합니다.

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

이 방법의 주요 이점은 저장소 계정 키가 변경된 경우 템플릿 또는 배포 매개 변수를 변경할 필요가 없다는 점입니다.

사용자 지정 스크립트 확장 사용에 대한 자세한 내용은 [Resource Manager 템플릿을 사용한 사용자 지정 스크립트 확장](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요.

## <a name="next-step"></a>다음 단계
<hr>

[추가 Azure Resource Manager 템플릿 살펴보기](https://github.com/Azure/azure-quickstart-templates)

