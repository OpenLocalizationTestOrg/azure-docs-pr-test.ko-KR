---
title: "hello 클래식 배포 모델-Azure에에서 Windows VM aaaResize | Microsoft Docs"
description: "Azure Powershell을 사용 하 여 hello 클래식 배포 모델에서 만든 Windows 가상 컴퓨터 크기를 조정 합니다."
services: virtual-machines-windows
documentationcenter: 
author: Drewm3
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: e3038215-001c-406e-904d-e0f4e326a4c7
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: drewm
ms.openlocfilehash: 39fab14431e2351c9515b0611e850eccfec7a798
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-windows-vm-created-in-hello-classic-deployment-model"></a>Hello 클래식 배포 모델에서 만든 Windows VM의 크기를 조정합니다
이 문서에서는 tooresize Windows VM을 만드는 방법은 Azure Powershell을 사용 하 여 hello 클래식 배포 모델에서 설명 합니다.

Hello 기능 tooresize VM을 고려할 때는 사용할 수 있는 tooresize hello 가상 컴퓨터 크기의 hello 범위를 제어 하는 두 가지 개념이 있습니다. hello 첫 번째 개념은 VM 배포 된 hello 영역입니다. 지역에서 사용할 수 있는 VM 크기의 hello 목록은 hello Azure 지역 웹 페이지의 hello 서비스 탭입니다. hello 두 번째 개념은 VM을 현재 호스팅하고 hello 물리적 하드웨어입니다. Vm을 호스트 하는 hello 실제 서버는 일반적인 물리적 하드웨어의 클러스터에서 함께 그룹화 됩니다. VM 크기를 변경의 hello 방법이 hello 새 VM 크기에서 지원 되는지 hello hello VM을 현재 호스팅하고 클러스터 하드웨어에 따라 다릅니다.

> [!IMPORTANT] 
> Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다. 수도 있습니다 [hello 리소스 관리자 배포 모델에서 만든 VM의 크기를 조정](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

## <a name="add-your-account"></a>사용자 계정 추가
클래식 Azure 리소스에 Azure PowerShell toowork를 구성 해야 합니다. Tooconfigure Azure PowerShell toomanage 클래식 리소스는 다음 hello 단계를 따릅니다.

1. Hello PowerShell 프롬프트에서 입력 `Add-AzureAccount` 클릭 **Enter**합니다. 
2. Azure 구독에 연결 된 hello 전자 메일 주소에 입력 하 고 클릭 **계속**합니다. 
3. Hello 계정의 암호를 입력 합니다. 
4. **로그인**을 클릭합니다. 

## <a name="resize-in-hello-same-hardware-cluster"></a>Hello에 동일한 조정 하드웨어 클러스터
hello VM을 호스팅하는 hello 하드웨어 클러스터에서 사용할 수 있는 VM tooa 크기 tooresize hello 다음 단계를 수행 합니다.

1. 다음 PowerShell 명령을 포함 하는 hello 클라우드 서비스를 호스트 하는 hello 하드웨어 클러스터에서 사용할 수 있는 toolist hello VM 크기 hello VM hello를 실행 합니다.
   
    ```powershell
    Get-AzureService | where {$_.ServiceName -eq "<cloudServiceName>"}
    ```
2. 다음 명령을 tooresize hello VM hello를 실행 합니다.
   
    ```powershell
    Get-AzureVM -ServiceName <cloudServiceName> -Name <vmName> | Set-AzureVMSize -InstanceSize <newVMSize> | Update-AzureVM
    ```

## <a name="resize-on-a-new-hardware-cluster"></a>새 하드웨어 클러스터에서 크기 조정
hello 클러스터 호스트 하드웨어에서 사용할 수 없는 VM tooa 크기 tooresize hello VM, hello 클라우드 서비스 및 hello 클라우드 서비스의 모든 Vm을 다시 만들어야 합니다. 각 클라우드 서비스 이므로 hello 클라우드 서비스의 모든 Vm 하드웨어 클러스터에서 사용할 수 있는 크기 이어야 합니다. 단일 하드웨어 클러스터에서 호스트 됩니다. hello 다음 단계는 설명 tooresize 삭제 한 다음 다시 만들어 하 여 VM 클라우드를 hello 방법을 서비스입니다.

1. 다음 PowerShell 명령을 toolist hello VM 크기를 사용할 수 hello 영역의 hello를 실행 합니다. 
   
    ```powershell
    Get-AzureLocation | where {$_.Name -eq "<locationName>"}
    ```
2. 각 VM에 대 한 모든 구성 설정 기록 크기를 조정 하는 hello VM toobe 포함 된 hello 클라우드 서비스에서 확인 합니다. 
3. 각 VM에 대 한 hello 옵션 tooretain hello 디스크를 선택 하는 hello 클라우드 서비스의 모든 Vm을 삭제 합니다.
4. Hello 필요한 VM 크기를 사용 하 여 조정 hello VM toobe를 다시 만듭니다.
5. 이제 hello 클라우드 서비스를 호스트 하는 hello 하드웨어 클러스터에서 사용할 수 있는 VM 크기를 사용 하 여 hello 클라우드 서비스에서 다른 모든 Vm을 다시 만듭니다.

새 VM 크기를 사용하여 클라우드 서비스를 삭제하고 다시 만드는 샘플 스크립트는 [여기](https://github.com/Azure/azure-vm-scripts)에서 확인할 수 있습니다. 

## <a name="next-steps"></a>다음 단계
* [Hello 리소스 관리자 배포 모델에서 만든 VM의 크기를 조정](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

