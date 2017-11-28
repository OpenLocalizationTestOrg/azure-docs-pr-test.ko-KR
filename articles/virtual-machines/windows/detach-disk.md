---
title: "Windows VM에서 데이터 디스크 분리 - Azure| Microsoft Docs"
description: "Resource Manager 배포 모델을 사용하여 Azure의 가상 컴퓨터에서 데이터 디스크를 분리하는 방법을 알아봅니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 13180343-ac49-4a3a-85d8-0ead95e2028c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/21/2017
ms.author: cynthn
ms.openlocfilehash: 97aa69745d200ee76f9f859eb3a8b0ad2f202bad
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-detach-a-data-disk-from-a-windows-virtual-machine"></a><span data-ttu-id="c01cc-103">Windows 가상 컴퓨터에서 데이터 디스크를 분리하는 방법</span><span class="sxs-lookup"><span data-stu-id="c01cc-103">How to detach a data disk from a Windows virtual machine</span></span>
<span data-ttu-id="c01cc-104">가상 컴퓨터에 연결된 데이터 디스크가 더 이상 필요하지 않은 경우 쉽게 분리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c01cc-104">When you no longer need a data disk that's attached to a virtual machine, you can easily detach it.</span></span> <span data-ttu-id="c01cc-105">디스크를 분리하면 가상 컴퓨터에서 디스크가 제거되지만, 저장소에서는 제거되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c01cc-105">This removes the disk from the virtual machine, but doesn't remove it from storage.</span></span>

> [!WARNING]
> <span data-ttu-id="c01cc-106">디스크를 분리해도 자동으로 삭제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c01cc-106">If you detach a disk it is not automatically deleted.</span></span> <span data-ttu-id="c01cc-107">프리미엄 저장소를 구독하는 경우 디스크에 대한 저장소 요금이 계속 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="c01cc-107">If you have subscribed to Premium storage, you will continue to incur storage charges for the disk.</span></span> <span data-ttu-id="c01cc-108">자세한 내용은 [프리미엄 저장소 사용 시 가격 책정 및 청구](../../storage/common/storage-premium-storage.md#pricing-and-billing)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c01cc-108">For more information refer to [Pricing and Billing when using Premium Storage](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span></span>
>
>

<span data-ttu-id="c01cc-109">디스크에 있는 기존 데이터를 다시 사용하려는 경우 동일한 또는 다른 가상 컴퓨터에 다시 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c01cc-109">If you want to use the existing data on the disk again, you can reattach it to the same virtual machine, or another one.</span></span>

## <a name="detach-a-data-disk-using-the-portal"></a><span data-ttu-id="c01cc-110">포털을 사용하여 데이터 디스크 분리</span><span class="sxs-lookup"><span data-stu-id="c01cc-110">Detach a data disk using the portal</span></span>
1. <span data-ttu-id="c01cc-111">포털 허브에서 **가상 컴퓨터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c01cc-111">In the portal hub, select **Virtual Machines**.</span></span>
2. <span data-ttu-id="c01cc-112">분리할 데이터 디스크가 있는 가상 컴퓨터를 선택하고 **중지**를 클릭하여 VM을 할당 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="c01cc-112">Select the virtual machine that has the data disk you want to detach and click **Stop** to deallocate the VM.</span></span>
3. <span data-ttu-id="c01cc-113">가상 컴퓨터 블레이드에서 **디스크**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c01cc-113">In the virtual machine blade, select **Disks**.</span></span>
4. <span data-ttu-id="c01cc-114">**디스크** 블레이드 상단에서 **편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c01cc-114">At the top of the **Disks** blade, select **Edit**.</span></span>
5. <span data-ttu-id="c01cc-115">**디스크** 블레이드에서 분리할 데이터 디스크의 맨 오른쪽에 있는 ![분리 단추 이미지](./media/detach-disk/detach.png) 분리 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c01cc-115">In the **Disks** blade, to the far right of the data disk that you would like to detach, click the ![Detach button image](./media/detach-disk/detach.png) detach button.</span></span>
5. <span data-ttu-id="c01cc-116">디스크를 제거한 후에 블레이드 상단에서 저장을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c01cc-116">After the disk has been removed, click Save on the top of the blade.</span></span>
6. <span data-ttu-id="c01cc-117">가상 컴퓨터 블레이드에서 **개요**를 클릭한 다음 블레이드 상단에서 **시작** 단추를 클릭하여 VM을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c01cc-117">In the virtual machine blade, click **Overview** and then click the **Start** button at the top of the blade to restart the VM.</span></span>



<span data-ttu-id="c01cc-118">디스크가 저장소에 유지되지만 더 이상 가상 컴퓨터에 연결되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c01cc-118">The disk remains in storage but is no longer attached to a virtual machine.</span></span>

## <a name="detach-a-data-disk-using-powershell"></a><span data-ttu-id="c01cc-119">PowerShell을 사용하여 데이터 디스크 분리</span><span class="sxs-lookup"><span data-stu-id="c01cc-119">Detach a data disk using PowerShell</span></span>
<span data-ttu-id="c01cc-120">이 예제에서 첫 번째 명령은 Get-AzureRmVM cmdlet을 사용하여 **RG11** 리소스 그룹에 가상 컴퓨터 **MyVM07**을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c01cc-120">In this example, the first command gets the virtual machine named **MyVM07** in the **RG11** resource group using the Get-AzureRmVM cmdlet.</span></span> <span data-ttu-id="c01cc-121">이 명령은 가상 컴퓨터를 **$VirtualMachine** 변수에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c01cc-121">The command stores the virtual machine in the **$VirtualMachine** variable.</span></span>

<span data-ttu-id="c01cc-122">두 번째 명령은 가상 컴퓨터에서 DataDisk3이라는 데이터 디스크를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="c01cc-122">The second command removes the data disk named DataDisk3 from the virtual machine.</span></span>

<span data-ttu-id="c01cc-123">마지막 명령은 가상 컴퓨터의 상태를 업데이트하여 데이터 디스크 제거 프로세스를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="c01cc-123">The final command updates the state of the virtual machine to complete the process of removing the data disk.</span></span>

```powershell
$VirtualMachine = Get-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07"
Remove-AzureRmVMDataDisk -VM $VirtualMachine -Name "DataDisk3"
Update-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07" -VM $VirtualMachine
```

<span data-ttu-id="c01cc-124">자세한 내용은 [Remove-AzureRmVMDataDisk](/powershell/module/azurerm.compute/remove-azurermvmdatadisk)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c01cc-124">For more information, see [Remove-AzureRmVMDataDisk](/powershell/module/azurerm.compute/remove-azurermvmdatadisk).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c01cc-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c01cc-125">Next steps</span></span>
<span data-ttu-id="c01cc-126">데이터 디스크를 다시 사용하려는 경우 [다른 VM에 연결](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="c01cc-126">If you want to reuse the data disk, you can just [attach it to another VM](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

