---
title: "Azure에서 PowerShell을 사용하여 Windows VM 크기 조정 | Microsoft Docs"
description: "Azure Powershell을 사용하여 Resource Manager 배포 모델에서 만든 Windows 가상 컴퓨터의 크기를 조정합니다."
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
ms.openlocfilehash: 742efd1496de9ce76b1e5636297ef30f546bd108
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="resize-a-windows-vm"></a><span data-ttu-id="b2d77-103">Windows VM 크기 조정</span><span class="sxs-lookup"><span data-stu-id="b2d77-103">Resize a Windows VM</span></span>
<span data-ttu-id="b2d77-104">이 문서에서는 Azure Powershell을 사용하여 Resource Manager 배포 모델에서 만든 Windows VM의 크기를 조정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b2d77-104">This article shows you how to resize a Windows VM, created in the Resource Manager deployment model using Azure Powershell.</span></span>

<span data-ttu-id="b2d77-105">VM(가상 컴퓨터)을 만든 후 VM 크기를 변경하여 VM의 크기를 확장 또는 축소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2d77-105">After you create a virtual machine (VM), you can scale the VM up or down by changing the VM size.</span></span> <span data-ttu-id="b2d77-106">경우에 따라 먼저 VM의 할당을 취소해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2d77-106">In some cases, you must deallocate the VM first.</span></span> <span data-ttu-id="b2d77-107">이는 현재 VM을 호스트하는 하드웨어 클러스터에서 새 크기를 사용할 수 없는 경우에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2d77-107">This can happen if the new size is not available on the hardware cluster that is currently hosting the VM.</span></span>

## <a name="resize-a-windows-vm-not-in-an-availability-set"></a><span data-ttu-id="b2d77-108">가용성 집합에 없는 Windows VM의 크기 조정</span><span class="sxs-lookup"><span data-stu-id="b2d77-108">Resize a Windows VM not in an availability set</span></span>
1. <span data-ttu-id="b2d77-109">VM이 호스트되는 하드웨어 클러스터에서 사용할 수 있는 VM 크기를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="b2d77-109">List the VM sizes that are available on the hardware cluster where the VM is hosted.</span></span> 
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName> 
    ```
2. <span data-ttu-id="b2d77-110">원하는 크기가 목록에 나열된 경우 다음 명령을 실행하여 VM 크기를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="b2d77-110">If the desired size is listed, run the following commands to resize the VM.</span></span> <span data-ttu-id="b2d77-111">원하는 크기가 목록에 나열되지 않으면 3단계로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b2d77-111">If the desired size is not listed, go on to step 3.</span></span>
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVMsize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. <span data-ttu-id="b2d77-112">원하는 크기가 나열되지 않은 경우에는 다음 명령을 실행하여 VM의 할당을 취소하고 크기를 조정한 다음 VM을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b2d77-112">If the desired size is not listed, run the following commands to deallocate the VM, resize it, and restart the VM.</span></span>
   
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
> <span data-ttu-id="b2d77-113">VM의 할당이 취소되면 VM에 할당된 모든 동적 IP 주소가 해제됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2d77-113">Deallocating the VM releases any dynamic IP addresses assigned to the VM.</span></span> <span data-ttu-id="b2d77-114">OS 및 데이터 디스크는 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b2d77-114">The OS and data disks are not affected.</span></span> 
> 
> 

## <a name="resize-a-windows-vm-in-an-availability-set"></a><span data-ttu-id="b2d77-115">가용성 집합에 있는 Windows VM의 크기 조정</span><span class="sxs-lookup"><span data-stu-id="b2d77-115">Resize a Windows VM in an availability set</span></span>
<span data-ttu-id="b2d77-116">가용성 집합에서 VM에 대한 새 크기를 현재 VM을 호스트하는 하드웨어 클러스터에서 사용할 수 없는 경우 가용성 집합의 모든 VM을 할당 취소하여 VM 크기를 조정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2d77-116">If the new size for a VM in an availability set is not available on the hardware cluster currently hosting the VM, then all VMs in the availability set will need to be deallocated to resize the VM.</span></span> <span data-ttu-id="b2d77-117">또한 VM 크기를 조정한 후 가용성 집합에서 다른 VM의 크기를 업데이트해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2d77-117">You also might need to update the size of other VMs in the availability set after one VM has been resized.</span></span> <span data-ttu-id="b2d77-118">가용성 집합에서 VM의 크기를 조정하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b2d77-118">To resize a VM in an availability set, perform the following steps.</span></span>

1. <span data-ttu-id="b2d77-119">VM이 호스트되는 하드웨어 클러스터에서 사용할 수 있는 VM 크기를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="b2d77-119">List the VM sizes that are available on the hardware cluster where the VM is hosted.</span></span>
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName>
    ```
2. <span data-ttu-id="b2d77-120">원하는 크기가 목록에 나열된 경우 다음 명령을 실행하여 VM 크기를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="b2d77-120">If the desired size is listed, run the following commands to resize the VM.</span></span> <span data-ttu-id="b2d77-121">나열되지 않으면 3단계로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b2d77-121">If it is not listed, go to step 3.</span></span>
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVmSize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. <span data-ttu-id="b2d77-122">원하는 크기가 목록에 나열되지 않는 경우 다음 단계를 진행하여 가용성 집합의 모든 VM을 할당 취소하고 VM 크기를 조정한 후 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b2d77-122">If the desired size is not listed, continue with the following steps to deallocate all VMs in the availability set, resize VMs, and restart them.</span></span>
4. <span data-ttu-id="b2d77-123">가용성 집합의 VM을 모두 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="b2d77-123">Stop all VMs in the availability set.</span></span>
   
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
5. <span data-ttu-id="b2d77-124">가용성 집합의 VM을 크기 조정하고 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b2d77-124">Resize and restart the VMs in the availability set.</span></span>
   
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

## <a name="next-steps"></a><span data-ttu-id="b2d77-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b2d77-125">Next steps</span></span>
* <span data-ttu-id="b2d77-126">확장성을 높이기 위해서는 여러 VM 인스턴스를 실행하고 규모를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="b2d77-126">For additional scalability, run multiple VM instances and scale out.</span></span> <span data-ttu-id="b2d77-127">자세한 내용은 [가상 컴퓨터 확장 집합에서 Windows 컴퓨터 자동 확장](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b2d77-127">For more information, see [Automatically scale Windows machines in a Virtual Machine Scale Set](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md).</span></span>

