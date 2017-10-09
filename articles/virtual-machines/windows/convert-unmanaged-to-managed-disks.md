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
# <a name="convert-a-windows-virtual-machine-from-unmanaged-disks-toomanaged-disks"></a><span data-ttu-id="1d52b-103">관리 되지 않는 디스크 toomanaged 디스크에서 Windows 가상 컴퓨터 변환</span><span class="sxs-lookup"><span data-stu-id="1d52b-103">Convert a Windows virtual machine from unmanaged disks toomanaged disks</span></span>

<span data-ttu-id="1d52b-104">기존 Windows 가상 컴퓨터 (Vm) 관리 되지 않는 디스크를 사용 하는 경우 hello 통해 hello Vm toouse 관리 되는 디스크를 변환할 수 있습니다 [Azure 관리 되는 디스크](managed-disks-overview.md) 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="1d52b-104">If you have existing Windows virtual machines (VMs) that use unmanaged disks, you can convert hello VMs toouse managed disks through hello [Azure Managed Disks](managed-disks-overview.md) service.</span></span> <span data-ttu-id="1d52b-105">이 프로세스는 hello OS 디스크 및 연결 된 데이터 디스크를 모두 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="1d52b-105">This process converts both hello OS disk and any attached data disks.</span></span>

<span data-ttu-id="1d52b-106">이 문서에서는 Azure PowerShell을 사용 하 여 Vm tooconvert 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d52b-106">This article shows you how tooconvert VMs by using Azure PowerShell.</span></span> <span data-ttu-id="1d52b-107">Tooinstall 필요 하거나 업그레이드할 참조 [설치 Azure PowerShell을 구성 하 고](/powershell/azure/install-azurerm-ps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1d52b-107">If you need tooinstall or upgrade it, see [Install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1d52b-108">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="1d52b-108">Before you begin</span></span>


* <span data-ttu-id="1d52b-109">검토 [hello 마이그레이션 계획 tooManaged 디스크](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks)합니다.</span><span class="sxs-lookup"><span data-stu-id="1d52b-109">Review [Plan for hello migration tooManaged Disks](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks).</span></span>

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]




## <a name="convert-single-instance-vms"></a><span data-ttu-id="1d52b-110">단일 인스턴스 VM 변환</span><span class="sxs-lookup"><span data-stu-id="1d52b-110">Convert single-instance VMs</span></span>
<span data-ttu-id="1d52b-111">이 섹션에서는 tooconvert 단일 인스턴스 Azure Vm에서 관리 되지 않는 toomanaged 디스크 디스크 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d52b-111">This section covers how tooconvert single-instance Azure VMs from unmanaged disks toomanaged disks.</span></span> <span data-ttu-id="1d52b-112">(Vm 가용성 집합에 있는 경우 hello 다음 섹션 참조 합니다.)</span><span class="sxs-lookup"><span data-stu-id="1d52b-112">(If your VMs are in an availability set, see hello next section.)</span></span> 

1. <span data-ttu-id="1d52b-113">Hello를 사용 하 여 hello VM 할당을 취소 [중지 AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1d52b-113">Deallocate hello VM by using hello [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet.</span></span> <span data-ttu-id="1d52b-114">hello 다음 예제에서는 할당 취소 hello 라는 VM `myVM` 이라는 hello 리소스 그룹에 `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="1d52b-114">hello following example deallocates hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span> 

  ```powershell
  $rgName = "myResourceGroup"
  $vmName = "myVM"
  Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
  ```

2. <span data-ttu-id="1d52b-115">Hello를 사용 하 여 hello VM toomanaged 디스크 변환 [ConvertTo AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1d52b-115">Convert hello VM toomanaged disks by using hello [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk) cmdlet.</span></span> <span data-ttu-id="1d52b-116">변환 프로세스를 수행 하는 hello hello OS 디스크 및 데이터 디스크를 포함 하 여 이전 VM을 hello:</span><span class="sxs-lookup"><span data-stu-id="1d52b-116">hello following process converts hello previous VM, including hello OS disk and any data disks:</span></span>

  ```powershell
  ConvertTo-AzureRmVMManagedDisk -ResourceGroupName $rgName -VMName $vmName
  ```

3. <span data-ttu-id="1d52b-117">사용 하 여 hello 변환 toomanaged 디스크 후 hello VM 시작 [시작 AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm)합니다.</span><span class="sxs-lookup"><span data-stu-id="1d52b-117">Start hello VM after hello conversion toomanaged disks by using [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm).</span></span> <span data-ttu-id="1d52b-118">다음 예제에서는 다시 시작 하는 hello hello 이전 VM:</span><span class="sxs-lookup"><span data-stu-id="1d52b-118">hello following example restarts hello previous VM:</span></span>

  ```powershell
  Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
  ```


## <a name="convert-vms-in-an-availability-set"></a><span data-ttu-id="1d52b-119">가용성 집합의 VM 변환</span><span class="sxs-lookup"><span data-stu-id="1d52b-119">Convert VMs in an availability set</span></span>

<span data-ttu-id="1d52b-120">경우 tooconvert toomanaged 디스크 가용성 집합에는 원하는 hello Vm을 먼저 tooconvert hello 가용성 집합 tooa 관리 되는 가용성 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="1d52b-120">If hello VMs that you want tooconvert toomanaged disks are in an availability set, you first need tooconvert hello availability set tooa managed availability set.</span></span>

1. <span data-ttu-id="1d52b-121">Hello를 사용 하 여 설정 하는 hello 가용성 변환 [업데이트 AzureRmAvailabilitySet](/powershell/module/azurerm.compute/update-azurermavailabilityset) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1d52b-121">Convert hello availability set by using hello [Update-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/update-azurermavailabilityset) cmdlet.</span></span> <span data-ttu-id="1d52b-122">다음 예에서는 업데이트 hello 가용성 명명 된 집합 hello `myAvailabilitySet` 이라는 hello 리소스 그룹에 `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="1d52b-122">hello following example updates hello availability set named `myAvailabilitySet` in hello resource group named `myResourceGroup`:</span></span>

  ```powershell
  $rgName = 'myResourceGroup'
  $avSetName = 'myAvailabilitySet'

  $avSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rgName -Name $avSetName
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned 
  ```

  <span data-ttu-id="1d52b-123">가용성 집합은 있는 hello 영역에는 관리 되는 장애 도메인 2 하지만 hello 관리 되지 않는 장애 도메인 수는 3이이 명령은 유사한 오류가 표시 너무 "hello" 지정 된 장애 도메인 수 3 hello 범위는 1 too2에 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d52b-123">If hello region where your availability set is located has only 2 managed fault domains but hello number of unmanaged fault domains is 3, this command shows an error similar too"hello specified fault domain count 3 must fall in hello range 1 too2."</span></span> <span data-ttu-id="1d52b-124">오류, 업데이트 hello 오류 도메인 too2 및 update tooresolve hello `Sku` 너무`Aligned` 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1d52b-124">tooresolve hello error, update hello fault domain too2 and update `Sku` too`Aligned` as follows:</span></span>

  ```powershell
  $avSet.PlatformFaultDomainCount = 2
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned
  ```

2. <span data-ttu-id="1d52b-125">Hello 가용성 집합의 hello Vm 변환 및 할당을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d52b-125">Deallocate and convert hello VMs in hello availability set.</span></span> <span data-ttu-id="1d52b-126">hello 다음 스크립트의 할당을 취소할 각 VM hello를 사용 하 여 [중지 AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet을 사용 하 여 변환 [ConvertTo AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk)를 사용 하 여 다시 시작 하 고 [AzureRmVM 시작 ](/powershell/module/azurerm.compute/start-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="1d52b-126">hello following script deallocates each VM by using hello [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet, converts it by using [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk), and restarts it by using [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

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


## <a name="troubleshooting"></a><span data-ttu-id="1d52b-127">문제 해결</span><span class="sxs-lookup"><span data-stu-id="1d52b-127">Troubleshooting</span></span>

<span data-ttu-id="1d52b-128">변환 하는 동안 오류가 발생 하는 경우 또는 이전 변환에서 문제로 인해 오류 상태에 있는 VM이 실행 hello `ConvertTo-AzureRmVMManagedDisk` 다시 cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1d52b-128">If there is an error during conversion, or if a VM is in a failed state because of issues in a previous conversion, run hello `ConvertTo-AzureRmVMManagedDisk` cmdlet again.</span></span> <span data-ttu-id="1d52b-129">간단한 재시도는 일반적으로 hello 상황 차단 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="1d52b-129">A simple retry usually unblocks hello situation.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1d52b-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1d52b-130">Next steps</span></span>

[<span data-ttu-id="1d52b-131">표준 관리 디스크 toopremium 변환</span><span class="sxs-lookup"><span data-stu-id="1d52b-131">Convert standard managed disks toopremium</span></span>](convert-disk-storage.md)

<span data-ttu-id="1d52b-132">[스냅숏](snapshot-copy-managed-disk.md)을 사용하여 VM의 읽기 전용 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1d52b-132">Take a read-only copy of a VM by using [snapshots](snapshot-copy-managed-disk.md).</span></span>

