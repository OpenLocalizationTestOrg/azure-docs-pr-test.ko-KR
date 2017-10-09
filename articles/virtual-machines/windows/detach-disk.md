---
title: "Windows VM-Azure에서에서 데이터 디스크 aaaDetach | Microsoft Docs"
description: "Toodetach hello 리소스 관리자 배포 모델을 사용 하 여 Azure에서 가상 컴퓨터에서 데이터 디스크에 알아봅니다."
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
ms.openlocfilehash: f3f581d3f33329db2ecb7d25a68bc59af7361aad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodetach-a-data-disk-from-a-windows-virtual-machine"></a><span data-ttu-id="7eb5f-103">Windows 가상 컴퓨터에서 toodetach 데이터 디스크 하는 방법</span><span class="sxs-lookup"><span data-stu-id="7eb5f-103">How toodetach a data disk from a Windows virtual machine</span></span>
<span data-ttu-id="7eb5f-104">연결 된 tooa 가상 컴퓨터가 있는 데이터 디스크를 더 이상 해야 하는 경우 쉽게 분리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-104">When you no longer need a data disk that's attached tooa virtual machine, you can easily detach it.</span></span> <span data-ttu-id="7eb5f-105">이 hello 디스크 hello 가상 컴퓨터에서 제거 하지만 저장소에서 제거 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-105">This removes hello disk from hello virtual machine, but doesn't remove it from storage.</span></span>

> [!WARNING]
> <span data-ttu-id="7eb5f-106">디스크를 분리해도 자동으로 삭제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-106">If you detach a disk it is not automatically deleted.</span></span> <span data-ttu-id="7eb5f-107">TooPremium 저장소를 구독 하는 경우에 hello 디스크에 대 한 저장소 비용은 tooincur 계속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-107">If you have subscribed tooPremium storage, you will continue tooincur storage charges for hello disk.</span></span> <span data-ttu-id="7eb5f-108">자세한 내용은 참조 너무[가격 및 프리미엄 저장소를 사용 하는 경우 청구](../../storage/common/storage-premium-storage.md#pricing-and-billing)합니다.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-108">For more information refer too[Pricing and Billing when using Premium Storage](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span></span>
>
>

<span data-ttu-id="7eb5f-109">Hello toouse hello 디스크에 기존 데이터를 다시 선택 하면 다시 연결할 수 toohello 동일한 가상 컴퓨터 이거나 다른 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-109">If you want toouse hello existing data on hello disk again, you can reattach it toohello same virtual machine, or another one.</span></span>

## <a name="detach-a-data-disk-using-hello-portal"></a><span data-ttu-id="7eb5f-110">Hello 포털을 사용 하 여 데이터 디스크를 분리</span><span class="sxs-lookup"><span data-stu-id="7eb5f-110">Detach a data disk using hello portal</span></span>
1. <span data-ttu-id="7eb5f-111">Hello 포털 허브에서 선택 **가상 컴퓨터**합니다.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-111">In hello portal hub, select **Virtual Machines**.</span></span>
2. <span data-ttu-id="7eb5f-112">Hello 가상 컴퓨터를 누르고 원하는 toodetach hello 데이터 디스크 선택 **중지** toodeallocate hello VM입니다.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-112">Select hello virtual machine that has hello data disk you want toodetach and click **Stop** toodeallocate hello VM.</span></span>
3. <span data-ttu-id="7eb5f-113">Hello 가상 컴퓨터 블레이드 선택 **디스크**합니다.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-113">In hello virtual machine blade, select **Disks**.</span></span>
4. <span data-ttu-id="7eb5f-114">Hello의 hello 위쪽 **디스크** 블레이드를 **편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-114">At hello top of hello **Disks** blade, select **Edit**.</span></span>
5. <span data-ttu-id="7eb5f-115">Hello에 **디스크** 블레이드에서 toohello 싶다는 의사를 toodetach, hello 데이터 디스크의 맨 오른쪽 클릭 hello ![분리 단추 이미지](./media/detach-disk/detach.png) 단추를 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-115">In hello **Disks** blade, toohello far right of hello data disk that you would like toodetach, click hello ![Detach button image](./media/detach-disk/detach.png) detach button.</span></span>
5. <span data-ttu-id="7eb5f-116">Hello 디스크를 제거한 후 hello 블레이드 맨 hello에서 저장을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-116">After hello disk has been removed, click Save on hello top of hello blade.</span></span>
6. <span data-ttu-id="7eb5f-117">Hello 가상 컴퓨터 블레이드 클릭 **개요** hello를 클릭 한 다음 **시작** hello 블레이드 toorestart hello VM hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-117">In hello virtual machine blade, click **Overview** and then click hello **Start** button at hello top of hello blade toorestart hello VM.</span></span>



<span data-ttu-id="7eb5f-118">hello 디스크 저장소에 남아 있지만 더 이상 연결 된 tooa 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-118">hello disk remains in storage but is no longer attached tooa virtual machine.</span></span>

## <a name="detach-a-data-disk-using-powershell"></a><span data-ttu-id="7eb5f-119">PowerShell을 사용하여 데이터 디스크 분리</span><span class="sxs-lookup"><span data-stu-id="7eb5f-119">Detach a data disk using PowerShell</span></span>
<span data-ttu-id="7eb5f-120">이 예제에서는 첫 번째 명령은 가상 컴퓨터 v를 hello 가져옵니다 hello **MyVM07** hello에 **RG11** hello AzureRmVM Get cmdlet을 사용 하는 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-120">In this example, hello first command gets hello virtual machine named **MyVM07** in hello **RG11** resource group using hello Get-AzureRmVM cmdlet.</span></span> <span data-ttu-id="7eb5f-121">저장소 hello hello에 가상 컴퓨터 명령 hello **$VirtualMachine** 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-121">hello command stores hello virtual machine in hello **$VirtualMachine** variable.</span></span>

<span data-ttu-id="7eb5f-122">두 번째 명령은 hello DataDisk3 hello 가상 컴퓨터에서 명명 된 hello 데이터 디스크를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-122">hello second command removes hello data disk named DataDisk3 from hello virtual machine.</span></span>

<span data-ttu-id="7eb5f-123">마지막 명령은 hello hello 데이터 디스크를 제거할 경우의 hello toocomplete hello 프로세스를 가상 컴퓨터의 hello 상태를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-123">hello final command updates hello state of hello virtual machine toocomplete hello process of removing hello data disk.</span></span>

```powershell
$VirtualMachine = Get-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07"
Remove-AzureRmVMDataDisk -VM $VirtualMachine -Name "DataDisk3"
Update-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07" -VM $VirtualMachine
```

<span data-ttu-id="7eb5f-124">자세한 내용은 [Remove-AzureRmVMDataDisk](/powershell/module/azurerm.compute/remove-azurermvmdatadisk)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7eb5f-124">For more information, see [Remove-AzureRmVMDataDisk](/powershell/module/azurerm.compute/remove-azurermvmdatadisk).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7eb5f-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7eb5f-125">Next steps</span></span>
<span data-ttu-id="7eb5f-126">Tooreuse hello 데이터 디스크를 사용 하도록 하려는 경우 수 방금 [tooanother VM 연결](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="7eb5f-126">If you want tooreuse hello data disk, you can just [attach it tooanother VM](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

