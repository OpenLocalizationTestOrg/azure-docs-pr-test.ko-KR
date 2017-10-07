---
title: "Azure에서 Windows VM 리소스 aaaMove | Microsoft Docs"
description: "Hello 리소스 관리자 배포 모델에서 Windows VM tooanother Azure 구독 또는 리소스 그룹을 이동 합니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4e383427-4aff-4bf3-a0f4-dbff5c6f0c81
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 859e78dce9acf1168780d4ee8e9f6dac0e3c11cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-windows-vm-tooanother-azure-subscription-or-resource-group"></a><span data-ttu-id="c2d8f-103">Windows VM tooanother Azure 구독 또는 리소스 그룹 이동</span><span class="sxs-lookup"><span data-stu-id="c2d8f-103">Move a Windows VM tooanother Azure subscription or resource group</span></span>
<span data-ttu-id="c2d8f-104">이 문서는 방법을 단계별로 설명 toomove Windows VM의 리소스 그룹 또는 구독 간에 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d8f-104">This article walks you through how toomove a Windows VM between resource groups or subscriptions.</span></span> <span data-ttu-id="c2d8f-105">개인 구독에서 원래 VM을 만든 경우에 유용 수 있고 toomove 할 구독 간에 이동 하기 tooyour 회사의 구독 toocontinue 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d8f-105">Moving between subscriptions can be handy if you originally created a VM in a personal subscription and now want toomove it tooyour company's subscription toocontinue your work.</span></span>

> [!IMPORTANT]
><span data-ttu-id="c2d8f-106">지금은 Managed Disks를 이동할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c2d8f-106">You cannot move Managed Disks at this time.</span></span> 
>
><span data-ttu-id="c2d8f-107">새 리소스 Id는 hello 이동의 일부로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2d8f-107">New resource IDs are created as part of hello move.</span></span> <span data-ttu-id="c2d8f-108">Hello VM 이동 되었거나, 해야 tooupdate 도구 및 스크립트 toouse hello 새 리소스 Id입니다.</span><span class="sxs-lookup"><span data-stu-id="c2d8f-108">Once hello VM has been moved, you need tooupdate your tools and scripts toouse hello new resource IDs.</span></span> 
> 
> 

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="use-powershell-toomove-a-vm"></a><span data-ttu-id="c2d8f-109">Powershell toomove VM을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="c2d8f-109">Use Powershell toomove a VM</span></span>
<span data-ttu-id="c2d8f-110">가상 컴퓨터 tooanother 리소스 그룹 toomove toomake도 이동 해야 hello 종속 리소스를 모두 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d8f-110">toomove a virtual machine tooanother resource group, you need toomake sure that you also move all of hello dependent resources.</span></span> <span data-ttu-id="c2d8f-111">toouse hello Move-azurermresource cmdlet hello 리소스 이름과 리소스의 hello 유형을 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d8f-111">toouse hello Move-AzureRMResource cmdlet, you need hello resource name and hello type of resource.</span></span> <span data-ttu-id="c2d8f-112">모두 찾기 AzureRMResource hello cmdlet에서 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2d8f-112">You can get both from hello Find-AzureRMResource cmdlet.</span></span>

    Find-AzureRMResource -ResourceGroupNameContains "<sourceResourceGroupName>"


<span data-ttu-id="c2d8f-113">toomove VM toomove 여러 리소스가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d8f-113">toomove a VM we need toomove multiple resources.</span></span> <span data-ttu-id="c2d8f-114">지금 막 각 리소스에 대한 별도의 변수를 만들고 나열했습니다.</span><span class="sxs-lookup"><span data-stu-id="c2d8f-114">We can just create separate variables for each resource and then list them.</span></span> <span data-ttu-id="c2d8f-115">이 예제는 VM에 대 한 대부분의 hello 기본 리소스를 포함 하지만 필요에 따라 더 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2d8f-115">This example includes most of hello basic resources for a VM, but you can add more as needed.</span></span>

    $sourceRG = "<sourceResourceGroupName>"
    $destinationRG = "<destinationResourceGroupName>"

    $vm = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Compute/virtualMachines" -ResourceName "<vmName>"
    $storageAccount = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Storage/storageAccounts" -ResourceName "<storageAccountName>"
    $diagStorageAccount = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Storage/storageAccounts" -ResourceName "<diagnosticStorageAccountName>"
    $vNet = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/virtualNetworks" -ResourceName "<vNetName>"
    $nic = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/networkInterfaces" -ResourceName "<nicName>"
    $ip = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/publicIPAddresses" -ResourceName "<ipName>"
    $nsg = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/networkSecurityGroups" -ResourceName "<nsgName>"

    Move-AzureRmResource -DestinationResourceGroupName $destinationRG -ResourceId $vm.ResourceId, $storageAccount.ResourceId, $diagStorageAccount.ResourceId, $vNet.ResourceId, $nic.ResourceId, $ip.ResourceId, $nsg.ResourceId

<span data-ttu-id="c2d8f-116">toomove 리소스 toodifferent 구독 hello, hello 포함 **-DestinationSubscriptionId** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="c2d8f-116">toomove hello resources toodifferent subscription, include hello **-DestinationSubscriptionId** parameter.</span></span> 

    Move-AzureRmResource -DestinationSubscriptionId "<destinationSubscriptionID>" -DestinationResourceGroupName $destinationRG -ResourceId $vm.ResourceId, $storageAccount.ResourceId, $diagStorageAccount.ResourceId, $vNet.ResourceId, $nic.ResourceId, $ip.ResourceId, $nsg.ResourceId



<span data-ttu-id="c2d8f-117">묻는 tooconfirm toomove hello 원하는 리소스를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d8f-117">You will be asked tooconfirm that you want toomove hello specified resources.</span></span> <span data-ttu-id="c2d8f-118">형식 **Y** tooconfirm toomove hello 리소스 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d8f-118">Type **Y** tooconfirm that you want toomove hello resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c2d8f-119">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c2d8f-119">Next steps</span></span>
<span data-ttu-id="c2d8f-120">리소스 그룹 및 구독 간의 다양한 유형의 리소스를 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2d8f-120">You can move many different types of resources between resource groups and subscriptions.</span></span> <span data-ttu-id="c2d8f-121">자세한 내용은 참조 [리소스 toonew 리소스 그룹이 나 구독 이동](../../resource-group-move-resources.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c2d8f-121">For more information, see [Move resources toonew resource group or subscription](../../resource-group-move-resources.md).</span></span>    

