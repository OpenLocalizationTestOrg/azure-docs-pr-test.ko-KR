---
title: "Azure에서 Windows VM aaaUse PowerShell tooresize | Microsoft Docs"
description: "Azure Powershell을 사용 하 여 hello 리소스 관리자 배포 모델에서 만든 Windows 가상 컴퓨터 크기를 조정 합니다."
services: virtual-machines-windows
documentationcenter: 
author: Drewm3
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 057ff274-6dad-415e-891c-58f8eea9ed78
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: drewm
ms.openlocfilehash: a4a80f3bc99911e4f1a095f0ce63aca00fa50694
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-windows-vm"></a>Windows VM 크기 조정
이 문서에서는 tooresize Windows VM을 만드는 방법은 Azure Powershell을 사용 하 여 hello 리소스 관리자 배포 모델에서 설명 합니다.

가상 컴퓨터 (VM)를 만든 후 확장할 수 있습니다 hello VM 위로 또는 아래로 hello VM 크기를 변경 합니다. 경우에 따라 할당을 취소 해야 hello VM 먼저 합니다. 이 새 크기 hello hello VM을 현재 호스팅 중인 hello 하드웨어 클러스터에서 사용할 수 없는 경우 발생할 수 있습니다.

## <a name="resize-a-windows-vm-not-in-an-availability-set"></a>가용성 집합에 없는 Windows VM의 크기 조정
1. Hello VM 호스트 되는 hello 하드웨어 클러스터에서 사용할 수 있는 hello VM 크기를 나열 합니다. 
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName> 
    ```
2. Hello 원하는 크기 나열 된 경우 다음 명령을 tooresize hello VM hello를 실행 합니다. Hello 크기 나열 되지 않으면 원하는 경우 toostep 3 이동 합니다.
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVMsize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. Hello 크기 나열 되지 않으면 원하는 경우 hello 다음 toodeallocate hello VM 크기를 변경 하 고 hello VM을 다시 시작 명령을 실행 합니다.
   
    ```powershell
    $rgname = "<resourceGroupName>"
    $vmname = "<vmName>"
    Stop-AzureRmVM -ResourceGroupName $rgname -VMName $vmname -Force
    $vm = Get-AzureRmVM -ResourceGroupName $rgname -VMName $vmname
    $vm.HardwareProfile.VmSize = "<newVMSize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName $rgname
    Start-AzureRmVM -ResourceGroupName $rgname -Name $vmname
    ```

> [!WARNING]
> 할당 해제 hello VM toohello VM을 할당 하는 동적 IP 주소를 해제 합니다. hello OS 및 데이터 디스크 영향을 받지 않습니다. 
> 
> 

## <a name="resize-a-windows-vm-in-an-availability-set"></a>가용성 집합에 있는 Windows VM의 크기 조정
Hello 가용성 집합에 VM에 대 한 새 크기에서 사용할 수 없으면 hello 하드웨어 클러스터 hello을 호스팅 중인 VM을 다음 hello 가용성 집합에 있는 모든 Vm 할 경우 toobe tooresize hello VM 할당이 취소 합니다. 또한 하나의 VM 크기를 조정한 후 설정 hello 가용성의 다른 Vm의 tooupdate hello 크기를 해야 합니다. 가용성 집합에 VM tooresize hello 다음 단계를 수행 합니다.

1. Hello VM 호스트 되는 hello 하드웨어 클러스터에서 사용할 수 있는 hello VM 크기를 나열 합니다.
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName>
    ```
2. Hello 원하는 크기 나열 된 경우 다음 명령을 tooresize hello VM hello를 실행 합니다. 나열 되지 않으면 3 toostep을 이동 합니다.
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVmSize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. Hello 크기 나열 되지 않으면 원하는 경우 계속 진행 단계 toodeallocate 다음 hello hello 가용성 집합에 있는 모든 Vm, Vm의 크기를 조정 하 고 다시 시작 합니다.
4. Hello 가용성 집합에 있는 모든 Vm을 중지 합니다.
   
   ```powershell
   $rg = "<resourceGroupName>"
   $as = Get-AzureRmAvailabilitySet -ResourceGroupName $rg
   $vmIds = $as.VirtualMachinesReferences
   foreach ($vmId in $vmIDs){
     $string = $vmID.Id.Split("/")
     $vmName = $string[8]
     Stop-AzureRmVM -ResourceGroupName $rg -Name $vmName -Force
   } 
   ```
5. 크기를 조정 하 고 hello 가용성 집합에 Vm hello를 다시 시작 합니다.
   
   ```powershell
   $rg = "<resourceGroupName>"
   $newSize = "<newVmSize>"
   $as = Get-AzureRmAvailabilitySet -ResourceGroupName $rg
   $vmIds = $as.VirtualMachinesReferences
   foreach ($vmId in $vmIDs){
     $string = $vmID.Id.Split("/")
     $vmName = $string[8]
     $vm = Get-AzureRmVM -ResourceGroupName $rg -Name $vmName
     $vm.HardwareProfile.VmSize = $newSize
     Update-AzureRmVM -ResourceGroupName $rg -VM $vm
     Start-AzureRmVM -ResourceGroupName $rg -Name $vmName
   }
   ```

## <a name="next-steps"></a>다음 단계
* 확장성을 높이기 위해서는 여러 VM 인스턴스를 실행하고 규모를 확장합니다. 자세한 내용은 [가상 컴퓨터 확장 집합에서 Windows 컴퓨터 자동 확장](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md)을 참조하세요.

