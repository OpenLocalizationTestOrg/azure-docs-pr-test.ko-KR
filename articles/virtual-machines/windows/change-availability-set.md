---
title: "VM 가용성 집합 변경 | Microsoft Docs"
description: "Azure PowerShell 및 Resource Manager 배포 모델을 사용하여 가상 컴퓨터에 대한 가용성 집합을 변경하는 방법에 대해 알아봅니다."
keywords: 
services: virtual-machines-windows
documentationcenter: 
author: Drewm3
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 44c90f90-bc9a-4260-a36f-5465e2a1ef94
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/15/2016
ms.author: drewm
ms.openlocfilehash: d1daa01191480eaeb81727416b2134b00c698dc3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="change-the-availability-set-for-a-windows-vm"></a><span data-ttu-id="76ae9-103">Windows VM에 대한 가용성 집합 변경</span><span class="sxs-lookup"><span data-stu-id="76ae9-103">Change the availability set for a Windows VM</span></span>
<span data-ttu-id="76ae9-104">다음 단계에서는 Azure PowerShell을 사용하여 VM의 가용성 집합을 변경하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="76ae9-104">The following steps describe how to change the availability set of a VM using Azure PowerShell.</span></span> <span data-ttu-id="76ae9-105">VM은 생성될 때만 가용성 집합에 추가될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76ae9-105">A VM can only be added to an availability set when it is created.</span></span> <span data-ttu-id="76ae9-106">가용성 집합을 변경하려면 가상 컴퓨터를 삭제했다가 다시 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76ae9-106">In order to change the availability set, you need to delete and recreate the virtual machine.</span></span> 

## <a name="change-the-availability-set-using-powershell"></a><span data-ttu-id="76ae9-107">PowerShell을 사용하여 가용성 집합 변경</span><span class="sxs-lookup"><span data-stu-id="76ae9-107">Change the availability set using PowerShell</span></span>
1. <span data-ttu-id="76ae9-108">수정할 VM에서 다음 주요 세부 정보를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="76ae9-108">Capture the following key details from the VM to be modified.</span></span>
   
    <span data-ttu-id="76ae9-109">VM의 이름</span><span class="sxs-lookup"><span data-stu-id="76ae9-109">Name of the VM</span></span>
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <Name-of-resource-group> -Name <name-of-VM>
    $vm.Name
    ```
   
    <span data-ttu-id="76ae9-110">VM 크기</span><span class="sxs-lookup"><span data-stu-id="76ae9-110">VM Size</span></span>
   
    ```powershell
    $vm.HardwareProfile.VmSize
    ```
   
    <span data-ttu-id="76ae9-111">VM에 있는 경우 네트워크 기본 네트워크 인터페이스 및 선택적 네트워크 인터페이스</span><span class="sxs-lookup"><span data-stu-id="76ae9-111">Network primary network interface and optional network interfaces if they exist on the VM</span></span>
   
    ```powershell
    $vm.NetworkProfile.NetworkInterfaces[0].Id
    ```
   
    <span data-ttu-id="76ae9-112">OS 디스크 프로필</span><span class="sxs-lookup"><span data-stu-id="76ae9-112">OS Disk Profile</span></span>
   
    ```powershell
    $vm.StorageProfile.OsDisk.OsType
    $vm.StorageProfile.OsDisk.Name
    $vm.StorageProfile.OsDisk.Vhd.Uri
    ```
   
    <span data-ttu-id="76ae9-113">각 데이터 디스크에 대한 디스크 프로필</span><span class="sxs-lookup"><span data-stu-id="76ae9-113">Disk profiles for each data disk</span></span> 
   
    ```powershell
    $vm.StorageProfile.DataDisks[<index>].Lun
    $vm.StorageProfile.DataDisks[<index>].Vhd.Uri
    ```
   
    <span data-ttu-id="76ae9-114">설치된 VM 확장</span><span class="sxs-lookup"><span data-stu-id="76ae9-114">VM extensions installed</span></span> 
   
    ```powershell
    $vm.Extensions
    ```
2. <span data-ttu-id="76ae9-115">디스크 또는 네트워크 인터페이스 중 어느 것도 삭제하지 않고 VM을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="76ae9-115">Delete the VM without deleting any of the disks or the network interfaces.</span></span>
   
    ```powershell
    Remove-AzureRmVM -ResourceGroupName <resourceGroupName> -Name <vmName> 
    ```
3. <span data-ttu-id="76ae9-116">아직 없는 경우 가용성 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="76ae9-116">Create the availability set if it does not already exist</span></span>
   
    ```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName <resourceGroupName> -Name <availabilitySetName> -Location "<location>" 
    ```
4. <span data-ttu-id="76ae9-117">새 가용성 집합을 사용하여 VM을 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="76ae9-117">Recreate the VM using the new availability set</span></span>
   
    ```powershell
    $vm2 = New-AzureRmVMConfig -VMName <VM-name> -VMSize <vm-size> -AvailabilitySetId <availability-set-id>
   
    Set-AzureRmVMOSDisk -CreateOption "Attach" -VM <vmConfig> -VhdUri <osDiskURI> -Name <osDiskName> [-Windows | -Linux]
   
    Add-AzureRmVMNetworkInterface -VM <vmConfig> -Id  <nicId> 
   
    New-AzureRmVM -ResourceGroupName <resourceGroupName> -Location <location> -VM <vmConfig>
    ``` 
5. <span data-ttu-id="76ae9-118">데이터 디스크 및 확장을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="76ae9-118">Add data disks and extensions.</span></span> <span data-ttu-id="76ae9-119">자세한 내용은 [VM에 데이터 디스크 연결](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 및 [Resource Manager 템플릿에서의 확장](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="76ae9-119">For more information, see [Attach Data Disk to VM](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Extensions in Resource Manager templates](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).</span></span> <span data-ttu-id="76ae9-120">PowerShell 또는 Azure CLI를 사용하여 VM에 데이터 디스크 및 확장을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76ae9-120">Data disks and extensions can be added to the VM using PowerShell or Azure CLI.</span></span>

## <a name="example-script"></a><span data-ttu-id="76ae9-121">예제 스크립트</span><span class="sxs-lookup"><span data-stu-id="76ae9-121">Example Script</span></span>
<span data-ttu-id="76ae9-122">다음 스크립트는 필요한 정보를 수집하고, 원본 VM을 삭제한 다음 새 가용성 집합에서 다시 만드는 예제를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="76ae9-122">The following script provides an example of gathering the required information, deleting the original VM and then recreating it in a new availability set.</span></span>

```powershell
    #set variables
    $rg = "demo-resource-group"
    $vmName = "demo-vm"
    $newAvailSetName = "demo-as"
    $outFile = "C:\temp\outfile.txt"

    #Get VM Details
    $OriginalVM = get-azurermvm -ResourceGroupName $rg -Name $vmName

    #Output VM details to file
    "VM Name: " | Out-File -FilePath $outFile 
    $OriginalVM.Name | Out-File -FilePath $outFile -Append

    "Extensions: " | Out-File -FilePath $outFile -Append
    $OriginalVM.Extensions | Out-File -FilePath $outFile -Append

    "VMSize: " | Out-File -FilePath $outFile -Append
    $OriginalVM.HardwareProfile.VmSize | Out-File -FilePath $outFile -Append

    "NIC: " | Out-File -FilePath $outFile -Append
    $OriginalVM.NetworkProfile.NetworkInterfaces[0].Id | Out-File -FilePath $outFile -Append

    "OSType: " | Out-File -FilePath $outFile -Append
    $OriginalVM.StorageProfile.OsDisk.OsType | Out-File -FilePath $outFile -Append

    "OS Disk: " | Out-File -FilePath $outFile -Append
    $OriginalVM.StorageProfile.OsDisk.Vhd.Uri | Out-File -FilePath $outFile -Append

    if ($OriginalVM.StorageProfile.DataDisks) {
    "Data Disk(s): " | Out-File -FilePath $outFile -Append
    $OriginalVM.StorageProfile.DataDisks | Out-File -FilePath $outFile -Append
    }

    #Remove the original VM
    Remove-AzureRmVM -ResourceGroupName $rg -Name $vmName

    #Create new availability set if it does not exist
    $availSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rg -Name $newAvailSetName -ErrorAction Ignore
    if (-Not $availSet) {
    $availset = New-AzureRmAvailabilitySet -ResourceGroupName $rg -Name $newAvailSetName -Location $OriginalVM.Location
    }

    #Create the basic configuration for the replacement VM
    $newVM = New-AzureRmVMConfig -VMName $OriginalVM.Name -VMSize $OriginalVM.HardwareProfile.VmSize -AvailabilitySetId $availSet.Id
    Set-AzureRmVMOSDisk -VM $NewVM -VhdUri $OriginalVM.StorageProfile.OsDisk.Vhd.Uri  -Name $OriginalVM.Name -CreateOption Attach -Windows

    #Add Data Disks
    foreach ($disk in $OriginalVM.StorageProfile.DataDisks ) { 
    Add-AzureRmVMDataDisk -VM $newVM -Name $disk.Name -VhdUri $disk.Vhd.Uri -Caching $disk.Caching -Lun $disk.Lun -CreateOption Attach -DiskSizeInGB $disk.DiskSizeGB
    }

    #Add NIC(s)
    foreach ($nic in $OriginalVM.NetworkInterfaceIDs) {
        Add-AzureRmVMNetworkInterface -VM $NewVM -Id $nic
    }

    #Create the VM
    New-AzureRmVM -ResourceGroupName $rg -Location $OriginalVM.Location -VM $NewVM -DisableBginfoExtension
```

## <a name="next-steps"></a><span data-ttu-id="76ae9-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="76ae9-123">Next steps</span></span>
<span data-ttu-id="76ae9-124">[데이터 디스크](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 더 추가하여 VM에 저장소를 좀 더 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="76ae9-124">Add additional storage to your VM by adding an additional [data disk](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

