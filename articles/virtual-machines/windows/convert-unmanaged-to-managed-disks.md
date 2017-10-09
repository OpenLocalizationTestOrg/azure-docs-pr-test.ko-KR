---
title: "Windows 가상 컴퓨터에서 관리 되지 않는 aaaConvert toomanaged 디스크-Azure 관리 되는 디스크의 디스크 | Microsoft Docs"
description: "Windows VM에서 관리 되지 않는 디스크 toomanaged tooconvert hello 리소스 관리자 배포 모델에서 PowerShell을 사용 하 여 디스크 방법"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: cynthn
ms.openlocfilehash: e8ed8694b0e776d22df26261e2fc8340bfe5cafa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="convert-a-windows-virtual-machine-from-unmanaged-disks-toomanaged-disks"></a>관리 되지 않는 디스크 toomanaged 디스크에서 Windows 가상 컴퓨터 변환

기존 Windows 가상 컴퓨터 (Vm) 관리 되지 않는 디스크를 사용 하는 경우 hello 통해 hello Vm toouse 관리 되는 디스크를 변환할 수 있습니다 [Azure 관리 되는 디스크](managed-disks-overview.md) 서비스입니다. 이 프로세스는 hello OS 디스크 및 연결 된 데이터 디스크를 모두 변환합니다.

이 문서에서는 Azure PowerShell을 사용 하 여 Vm tooconvert 합니다. Tooinstall 필요 하거나 업그레이드할 참조 [설치 Azure PowerShell을 구성 하 고](/powershell/azure/install-azurerm-ps.md)합니다.

## <a name="before-you-begin"></a>시작하기 전에


* 검토 [hello 마이그레이션 계획 tooManaged 디스크](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks)합니다.

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]




## <a name="convert-single-instance-vms"></a>단일 인스턴스 VM 변환
이 섹션에서는 tooconvert 단일 인스턴스 Azure Vm에서 관리 되지 않는 toomanaged 디스크 디스크 하는 방법을 설명 합니다. (Vm 가용성 집합에 있는 경우 hello 다음 섹션 참조 합니다.) 

1. Hello를 사용 하 여 hello VM 할당을 취소 [중지 AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet. hello 다음 예제에서는 할당 취소 hello 라는 VM `myVM` 이라는 hello 리소스 그룹에 `myResourceGroup`: 

  ```powershell
  $rgName = "myResourceGroup"
  $vmName = "myVM"
  Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
  ```

2. Hello를 사용 하 여 hello VM toomanaged 디스크 변환 [ConvertTo AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk) cmdlet. 변환 프로세스를 수행 하는 hello hello OS 디스크 및 데이터 디스크를 포함 하 여 이전 VM을 hello:

  ```powershell
  ConvertTo-AzureRmVMManagedDisk -ResourceGroupName $rgName -VMName $vmName
  ```

3. 사용 하 여 hello 변환 toomanaged 디스크 후 hello VM 시작 [시작 AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm)합니다. 다음 예제에서는 다시 시작 하는 hello hello 이전 VM:

  ```powershell
  Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
  ```


## <a name="convert-vms-in-an-availability-set"></a>가용성 집합의 VM 변환

경우 tooconvert toomanaged 디스크 가용성 집합에는 원하는 hello Vm을 먼저 tooconvert hello 가용성 집합 tooa 관리 되는 가용성 집합입니다.

1. Hello를 사용 하 여 설정 하는 hello 가용성 변환 [업데이트 AzureRmAvailabilitySet](/powershell/module/azurerm.compute/update-azurermavailabilityset) cmdlet. 다음 예에서는 업데이트 hello 가용성 명명 된 집합 hello `myAvailabilitySet` 이라는 hello 리소스 그룹에 `myResourceGroup`:

  ```powershell
  $rgName = 'myResourceGroup'
  $avSetName = 'myAvailabilitySet'

  $avSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rgName -Name $avSetName
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned 
  ```

  가용성 집합은 있는 hello 영역에는 관리 되는 장애 도메인 2 하지만 hello 관리 되지 않는 장애 도메인 수는 3이이 명령은 유사한 오류가 표시 너무 "hello" 지정 된 장애 도메인 수 3 hello 범위는 1 too2에 포함 되어야 합니다. 오류, 업데이트 hello 오류 도메인 too2 및 update tooresolve hello `Sku` 너무`Aligned` 다음과 같습니다.

  ```powershell
  $avSet.PlatformFaultDomainCount = 2
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned
  ```

2. Hello 가용성 집합의 hello Vm 변환 및 할당을 취소 합니다. hello 다음 스크립트의 할당을 취소할 각 VM hello를 사용 하 여 [중지 AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet을 사용 하 여 변환 [ConvertTo AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk)를 사용 하 여 다시 시작 하 고 [AzureRmVM 시작 ](/powershell/module/azurerm.compute/start-azurermvm):

  ```powershell
  $avSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rgName -Name $avSetName

  foreach($vmInfo in $avSet.VirtualMachinesReferences)
  {
     $vm = Get-AzureRmVM -ResourceGroupName $rgName | Where-Object {$_.Id -eq $vmInfo.id}
     Stop-AzureRmVM -ResourceGroupName $rgName -Name $vm.Name -Force
     ConvertTo-AzureRmVMManagedDisk -ResourceGroupName $rgName -VMName $vm.Name
     Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
  }
  ```


## <a name="troubleshooting"></a>문제 해결

변환 하는 동안 오류가 발생 하는 경우 또는 이전 변환에서 문제로 인해 오류 상태에 있는 VM이 실행 hello `ConvertTo-AzureRmVMManagedDisk` 다시 cmdlet. 간단한 재시도는 일반적으로 hello 상황 차단 해제합니다.


## <a name="next-steps"></a>다음 단계

[표준 관리 디스크 toopremium 변환](convert-disk-storage.md)

[스냅숏](snapshot-copy-managed-disk.md)을 사용하여 VM의 읽기 전용 복사본을 만듭니다.

