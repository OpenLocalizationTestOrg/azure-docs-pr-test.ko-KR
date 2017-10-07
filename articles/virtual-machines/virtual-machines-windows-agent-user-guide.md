---
title: "가상 컴퓨터 에이전트 개요 aaaAzure | Microsoft Docs"
description: "Azure Virtual Machines 에이전트 개요"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 0a1f212e-053e-4a39-9910-8d622959f594
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/28/2017
ms.author: nepeters
ms.openlocfilehash: 178766925673419cd661dbb460b8427bbfaf54e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-agent-overview"></a>Azure Virtual Machines 에이전트 개요

Microsoft Azure 가상 컴퓨터 에이전트 (VM 에이전트) hello는 hello Azure 패브릭 컨트롤러와 VM의 상호 작용을 관리 하는 안전 하 고 간단한 프로세스입니다. hello VM 에이전트를 사용 하도록 설정 하 고 Azure 가상 컴퓨터 확장 실행에서 기본 역할을 있습니다. VM 확장은 소프트웨어 설치 및 구성과 같은 가상 컴퓨터의 배포 후 구성을 가능하게 합니다. 또한 가상 컴퓨터 확장 hello 가상 컴퓨터의 관리자 암호를 재설정 하는 등의 복구 기능을 활성화 합니다. Hello Azure VM 에이전트 없이 가상 컴퓨터 확장을 실행할 수 없습니다.

설치, 검색, 및의 hello Azure 가상 컴퓨터 에이전트 제거가이 문서에 자세히 설명합니다.

## <a name="install-hello-vm-agent"></a>Hello VM 에이전트를 설치 합니다.

### <a name="azure-gallery-image"></a>Azure 갤러리 이미지

hello Azure VM 에이전트는 Azure 갤러리 이미지에서 배포 된 모든 Windows 가상 컴퓨터에서 기본적으로 설치 됩니다. Hello 포털, PowerShell, 명령줄 인터페이스 또는 Azure 리소스 관리자 템플릿에서 Azure 갤러리 이미지를 배포할 때 hello Azure VM 에이전트는도 설치할 수 있습니다. 

### <a name="manual-installation"></a>수동 설치

Windows installer 패키지를 사용 하 여 hello Windows VM 에이전트를 수동으로 설치할 수 있습니다. Azure에 배포되는 사용자 지정 가상 컴퓨터 이미지를 만들 때 수동 설치가 필요할 수 있습니다. 이 위치에서 hello VM 에이전트 설치 관리자를 다운로드 하는 Windows VM 에이전트 toomanually 설치 hello [Windows Azure VM 에이전트 다운로드](http://go.microsoft.com/fwlink/?LinkID=394789)합니다. 

hello windows installer 파일을 두 번 클릭 하 여 hello VM 에이전트를 설치할 수 있습니다. Hello VM 에이전트의 자동 또는 무인 설치를 hello 다음 명령을 실행 합니다.

```cmd
msiexec.exe /i WindowsAzureVmAgent.2.7.1198.778.rd_art_stable.160617-1120.fre /quiet
```

## <a name="detect-hello-vm-agent"></a>Hello VM 에이전트를 검색 합니다.

### <a name="powershell"></a>PowerShell

hello Azure 리소스 관리자 PowerShell 모듈 사용된 tooretrieve 정보에 대 한 Azure 가상 컴퓨터를 수 있습니다. 실행 `Get-AzureRmVM` 많은 양의 hello 프로비저닝 hello Azure VM 에이전트에 대 한 상태 등의 정보를 반환 합니다.

```PowerShell
Get-AzureRmVM
```

hello 다음은 hello의 일부만 `Get-AzureRmVM` 출력 합니다. 공지 hello `ProvisionVMAgent` 속성 내에 중첩 된 `OSProfile`, hello VM 에이전트가 가상 컴퓨터 배포 toohello 되어 있으면이 속성 사용된 toodetermine 될 수 있습니다.

```PowerShell
OSProfile                  :
  ComputerName             : myVM
  AdminUsername            : muUserName
  WindowsConfiguration     :
    ProvisionVMAgent       : True
    EnableAutomaticUpdates : True
```

다음 스크립트는 hello 사용된 tooreturn 간결 하 게 가상 컴퓨터 이름 및 hello VM 에이전트의 hello 상태 목록이 될 수 있습니다.

```PowerShell
$vms = Get-AzureRmVM

foreach ($vm in $vms) {
    $agent = $vm | Select -ExpandProperty OSProfile | Select -ExpandProperty Windowsconfiguration | Select ProvisionVMAgent
    Write-Host $vm.Name $agent.ProvisionVMAgent
}
```

### <a name="manual-detection"></a>수동 검색

Windows Azure VM tooa 로그인, 작업 관리자 실행 중인 프로세스에 사용 되는 tooexamine 될 수 있습니다. toocheck hello Azure VM 에이전트에 대 한 작업 관리자를 열고 > hello 세부 정보 탭을 클릭 하 고 프로세스 이름에 대 한 확인 `WindowsAzureGuestAgent.exe`합니다. 이 프로세스의 hello 존재 해당 hello VM 에이전트가 설치 된 것을 나타냅니다.

## <a name="upgrade-hello-vm-agent"></a>Hello VM 에이전트를 업그레이드 합니다.

Windows 용 hello Azure VM 에이전트 자동 업그레이드 됩니다. 새 가상 컴퓨터에 배포 된 tooAzure로 hello 최신 VM 에이전트를 받습니다. 사용자 지정 VM 이미지를 수동으로 업데이트 tooinclude hello 새 VM 에이전트가 있어야 합니다.
