---
title: "가상 컴퓨터 확장으로 응용 프로그램 배포 aaaAutomating | Microsoft Docs"
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
ms.openlocfilehash: 6d52537fbd4e935f19d3864def11484f519f8598
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="application-deployment-with-azure-resource-manager-templates-for-windows-vms"></a>Windows VM용 Azure Resource Manager 템플릿을 사용하는 응용 프로그램 배포

모든 Azure 인프라 요구 사항 파악 고 배포 템플릿을로 변환 되었습니다, 해결 toobe hello 실제 응용 프로그램 배포에 필요 합니다. 여기에 응용 프로그램 배포를 Azure 리소스 tooinstalling hello 실제 응용 프로그램 이진 파일을 참조 합니다. Hello Music Store 샘플을.Net Core 및 IIS toobe 각 가상 컴퓨터에 설치 및 구성 해야 합니다. 이진 파일 toobe hello 가상 컴퓨터에 설치 해야 하는 Music Store hello 및 hello Music Store 데이터베이스 미리 만들어 합니다.

이 문서는 가상 컴퓨터 확장 응용 프로그램 배포 및 구성 tooAzure 가상 컴퓨터를 자동화할 수 방법을 자세히 설명 합니다. 모든 종속성 및 고유한 구성이 강조 표시됩니다. Hello 최상의 경험에 대 한 미리 hello 솔루션 tooyour Azure 구독 및 Azure 리소스 관리자 템플릿 hello와 함께 작업의 인스턴스를 배포 합니다. hello 완전 한 템플릿 여기 – 있습니다 [Windows에서 음악 스토어 배포](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows)합니다.

## <a name="configuration-script"></a>구성 스크립트
가상 컴퓨터 확장은 tooprovide 구성 자동화 가상 컴퓨터에 대해 실행 되는 특별 한 프로그램입니다. 바이러스 백신, 로깅 구성 및 Docker 구성과 같은 여러 특정 용도로 확장을 사용할 수 있습니다. 사용자 지정 스크립트 확장 hello 모든 가상 컴퓨터에 대 한 스크립트를 사용 하는 toorun 될 수 있습니다. Hello Music Store 샘플 toohello 사용자 지정 스크립트 확장 tooconfigure hello Windows 가상 컴퓨터를 사용 되며 hello 음악 스토어 응용 프로그램을 설치 합니다.

가상 컴퓨터 확장 된 Azure 리소스 관리자 템플릿을에서 선언 되는 방법을 자세히 보여 주는 하기 전에를 실행 하는 hello 스크립트를 검사 합니다. 이 스크립트는 hello Windows 가상 컴퓨터 toohost hello 음악 스토어 응용 프로그램을 구성합니다. Hello 스크립트에 필요한 모든 소프트웨어 설치를 실행 하는 경우 소스 제어를 hello 음악 스토어 응용 프로그램을 설치 하 고 hello 데이터베이스를 준비 합니다. 

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
VM 확장 수에 대해 실행할 수는 가상 컴퓨터 빌드 시 hello Azure 리소스 관리자 템플릿을에 hello 확장을 리소스를 포함 하 여 합니다. hello Visual Studio 추가 리소스 마법사를 사용 하거나 hello 서식 파일에 유효한 JSON을 삽입 하 여 hello 확장을 추가할 수 있습니다. 가상 컴퓨터 리소스; hello 안에 중첩 hello 스크립트 확장을 리소스 이 hello 다음 예제에서에서 볼 수 있습니다.

Hello 리소스 관리자 템플릿-내에서이 링크 toosee hello JSON 샘플을 따라 [VM 스크립트 확장](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L339)합니다. 

아래 스크립트 hello JSON hello에서는 GitHub에 저장 됩니다. 이 스크립트를 Azure Blob 저장소에 저장할 수도 있습니다. 또한 Azure 리소스 관리자 템플릿을 사용 hello 스크립트 실행 문자열 toobe 생성 하는 스크립트 실행에 대 한 템플릿 매개 변수 값을 매개 변수로 사용할 수 있습니다. Hello 서식 파일을 배포 하는 경우 데이터는 제공 하는 경우에 되며 이러한 값 hello 스크립트를 실행할 때 사용할 수 있습니다.

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

위에서 설명한 대로 Azure Blob 저장소에 스크립트를 사용자 지정 가능한 toostore 이기도 합니다. 두 가지 옵션이 있습니다; blob 저장소에 hello 스크립트 리소스를 저장 하기 위한 컨테이너/스크립트 공용 hello 및 hello 위와 동일한 접근 방식에 따라 수행 하거나 tooprovide hello storageAccountName 및 storageAccountKey toohello CustomScriptExtension 리소스 정의 요구 하는 개인 blob 저장소에 보관할 수도 있습니다.

아래의 hello 예에서 म 모두 수행한 단계를 추가 합니다. 있지만 가능한 tooprovide hello 저장소 계정 이름과 키 매개 변수 또는 변수도 배포 중, 리소스 관리자 템플릿을 제공 hello `listKeys` 함수 hello 저장소 계정을 얻을 수 있는 키를 프로그래밍 방식으로 toohello 삽입 합니다. 배포 시 사용자에 대 한 템플릿입니다.

Hello 예제 CustomScriptExtension 리소스 정의 아래의 사용자 지정 스크립트에 업로드 된 tooan 이미 Azure 저장소 계정 호출 `mystorageaccount9999` 라는 다른 리소스 그룹에 존재 하는 `mysa999rgname`합니다. 이 리소스를 포함 하는 서식 파일을 배포 했습니다 hello `listKeys` 함수 hello 저장소 계정에 대 한 hello 저장소 계정 키를 프로그래밍 방식으로 가져옵니다 `mystorageaccount9999` hello 리소스 그룹에에서 `mysa999rgname` 을 수행해 줍니다 toohello 서식 파일에 삽입 합니다.

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

이 방법의 주요 장점은 hello 필요 하지 않습니다 있습니다 toochange 서식 파일 또는 저장소 계정 키 변경의 hello 이벤트에서 배포 매개 변수 hello은 합니다.

Hello 사용자 지정 스크립트 확장을 사용 하 여에 대 한 자세한 내용은 참조 하십시오. [사용자 지정 스크립트 확장을 리소스 관리자 템플릿으로](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

## <a name="next-step"></a>다음 단계
<hr>

[추가 Azure Resource Manager 템플릿 살펴보기](https://github.com/Azure/azure-quickstart-templates)

