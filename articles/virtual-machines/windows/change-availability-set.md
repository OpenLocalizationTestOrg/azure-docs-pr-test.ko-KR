---
title: "Vm 가용성 집합 aaaChange | Microsoft Docs"
description: "Azure PowerShell 및 hello 리소스 관리자 배포 모델을 사용 하 여 가상 컴퓨터에 대 한 toochange hello 가용성을 설정 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 3b1cc010a6d4c4883f2e34da9cfca4372aec92cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-availability-set-for-a-windows-vm"></a><span data-ttu-id="354af-103">Windows VM에 대 한 설정 hello 응답 가능 여부 변경</span><span class="sxs-lookup"><span data-stu-id="354af-103">Change hello availability set for a Windows VM</span></span>
<span data-ttu-id="354af-104">단계를 수행 하는 hello 방법을 toochange hello Azure PowerShell을 사용 하는 VM의 가용성 집합에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="354af-104">hello following steps describe how toochange hello availability set of a VM using Azure PowerShell.</span></span> <span data-ttu-id="354af-105">만 VM은 만들 때 설정할 tooan 가용성을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="354af-105">A VM can only be added tooan availability set when it is created.</span></span> <span data-ttu-id="354af-106">순서 toochange hello 가용성 집합에 필요한 toodelete 고 hello 가상 컴퓨터를 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="354af-106">In order toochange hello availability set, you need toodelete and recreate hello virtual machine.</span></span> 

## <a name="change-hello-availability-set-using-powershell"></a><span data-ttu-id="354af-107">PowerShell을 사용 하 여 설정 hello 응답 가능 여부 변경</span><span class="sxs-lookup"><span data-stu-id="354af-107">Change hello availability set using PowerShell</span></span>
1. <span data-ttu-id="354af-108">Hello를 수정 hello VM toobe에서 다음 키 세부 정보를 캡처하십시오.</span><span class="sxs-lookup"><span data-stu-id="354af-108">Capture hello following key details from hello VM toobe modified.</span></span>
   
    <span data-ttu-id="354af-109">Hello VM의 이름</span><span class="sxs-lookup"><span data-stu-id="354af-109">Name of hello VM</span></span>
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <Name-of-resource-group> -Name <name-of-VM>
    $vm.Name
    ```
   
    <span data-ttu-id="354af-110">VM 크기</span><span class="sxs-lookup"><span data-stu-id="354af-110">VM Size</span></span>
   
    ```powershell
    $vm.HardwareProfile.VmSize
    ```
   
    <span data-ttu-id="354af-111">네트워크 주 네트워크 인터페이스와 hello VM에 있는 선택적 네트워크 인터페이스</span><span class="sxs-lookup"><span data-stu-id="354af-111">Network primary network interface and optional network interfaces if they exist on hello VM</span></span>
   
    ```powershell
    $vm.NetworkProfile.NetworkInterfaces[0].Id
    ```
   
    <span data-ttu-id="354af-112">OS 디스크 프로필</span><span class="sxs-lookup"><span data-stu-id="354af-112">OS Disk Profile</span></span>
   
    ```powershell
    $vm.StorageProfile.OsDisk.OsType
    $vm.StorageProfile.OsDisk.Name
    $vm.StorageProfile.OsDisk.Vhd.Uri
    ```
   
    <span data-ttu-id="354af-113">각 데이터 디스크에 대한 디스크 프로필</span><span class="sxs-lookup"><span data-stu-id="354af-113">Disk profiles for each data disk</span></span> 
   
    ```powershell
    $vm.StorageProfile.DataDisks[<index>].Lun
    $vm.StorageProfile.DataDisks[<index>].Vhd.Uri
    ```
   
    <span data-ttu-id="354af-114">설치된 VM 확장</span><span class="sxs-lookup"><span data-stu-id="354af-114">VM extensions installed</span></span> 
   
    ```powershell
    $vm.Extensions
    ```
2. <span data-ttu-id="354af-115">Hello 디스크나 hello 네트워크 인터페이스 중 하나를 삭제 하지 않고 hello VM을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="354af-115">Delete hello VM without deleting any of hello disks or hello network interfaces.</span></span>
   
    ```powershell
    Remove-AzureRmVM -ResourceGroupName <resourceGroupName> -Name <vmName> 
    ```
3. <span data-ttu-id="354af-116">Hello 가용성 아직 없는 경우 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="354af-116">Create hello availability set if it does not already exist</span></span>
   
    ```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName <resourceGroupName> -Name <availabilitySetName> -Location "<location>" 
    ```
4. <span data-ttu-id="354af-117">다시 hello hello 새 가용성 집합을 사용 하 여 VM</span><span class="sxs-lookup"><span data-stu-id="354af-117">Recreate hello VM using hello new availability set</span></span>
   
    ```powershell
    $vm2 = New-AzureRmVMConfig -VMName <VM-name> -VMSize <vm-size> -AvailabilitySetId <availability-set-id>
   
    Set-AzureRmVMOSDisk -CreateOption "Attach" -VM <vmConfig> -VhdUri <osDiskURI> -Name <osDiskName> [-Windows | -Linux]
   
    Add-AzureRmVMNetworkInterface -VM <vmConfig> -Id  <nicId> 
   
    New-AzureRmVM -ResourceGroupName <resourceGroupName> -Location <location> -VM <vmConfig>
    ``` 
5. <span data-ttu-id="354af-118">데이터 디스크 및 확장을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="354af-118">Add data disks and extensions.</span></span> <span data-ttu-id="354af-119">자세한 내용은 참조 [데이터 디스크 연결 tooVM](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 및 [리소스 관리자 템플릿 확장](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions)합니다.</span><span class="sxs-lookup"><span data-stu-id="354af-119">For more information, see [Attach Data Disk tooVM](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Extensions in Resource Manager templates](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).</span></span> <span data-ttu-id="354af-120">데이터 디스크와 확장 추가할 수 있습니다 toohello VM PowerShell 또는 Azure CLI를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="354af-120">Data disks and extensions can be added toohello VM using PowerShell or Azure CLI.</span></span>

## <a name="example-script"></a><span data-ttu-id="354af-121">예제 스크립트</span><span class="sxs-lookup"><span data-stu-id="354af-121">Example Script</span></span>
<span data-ttu-id="354af-122">hello 다음 스크립트 예제를 제공 hello 필요한 정보를 수집 하는 원본 VM 하 고 다음 새 가용성 집합에 다시 hello 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="354af-122">hello following script provides an example of gathering hello required information, deleting hello original VM and then recreating it in a new availability set.</span></span>

```powershell
    #set variables
    $rg = "demo-resource-group"
    $vmName = "demo-vm"
    $newAvailSetName = "demo-as"
    $outFile = "C:\temp\outfile.txt"

    #Get VM Details
    $OriginalVM = get-azurermvm -ResourceGroupName $rg -Name $vmName

    #Output VM details toofile
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

    #Remove hello original VM
    Remove-AzureRmVM -ResourceGroupName $rg -Name $vmName

    #Create new availability set if it does not exist
    $availSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rg -Name $newAvailSetName -ErrorAction Ignore
    if (-Not $availSet) {
    $availset = New-AzureRmAvailabilitySet -ResourceGroupName $rg -Name $newAvailSetName -Location $OriginalVM.Location
    }

    #Create hello basic configuration for hello replacement VM
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

    #Create hello VM
    New-AzureRmVM -ResourceGroupName $rg -Location $OriginalVM.Location -VM $NewVM -DisableBginfoExtension
```

## <a name="next-steps"></a><span data-ttu-id="354af-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="354af-123">Next steps</span></span>
<span data-ttu-id="354af-124">추가 추가 하 여 추가 저장소 tooyour VM을 추가할 [데이터 디스크](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="354af-124">Add additional storage tooyour VM by adding an additional [data disk](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

