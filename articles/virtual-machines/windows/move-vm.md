---
title: "Azure에서 Windows VM 리소스 이동 | Microsoft Docs"
description: "Resource Manager 배포 모델에서 다른 Azure 구독 또는 리소스 그룹으로 Windows VM을 이동합니다."
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
ms.openlocfilehash: 1db25a5d9ff5cb6aa2787a0cafa40cfb010e3b06
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="move-a-windows-vm-to-another-azure-subscription-or-resource-group"></a><span data-ttu-id="66669-103">다른 Azure 구독 또는 리소스 그룹으로 Windows VM 이동</span><span class="sxs-lookup"><span data-stu-id="66669-103">Move a Windows VM to another Azure subscription or resource group</span></span>
<span data-ttu-id="66669-104">이 문서에서는 리소스 그룹 또는 구독 간에 Windows VM을 이동하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="66669-104">This article walks you through how to move a Windows VM between resource groups or subscriptions.</span></span> <span data-ttu-id="66669-105">개인 구독에서 원래 VM을 만들고 회사 구독으로 이동한 후 작업을 계속하려는 경우에 구독 간의 이동이 편리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66669-105">Moving between subscriptions can be handy if you originally created a VM in a personal subscription and now want to move it to your company's subscription to continue your work.</span></span>

> [!IMPORTANT]
><span data-ttu-id="66669-106">지금은 Managed Disks를 이동할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="66669-106">You cannot move Managed Disks at this time.</span></span> 
>
><span data-ttu-id="66669-107">새 리소스 ID는 이동의 일부로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="66669-107">New resource IDs are created as part of the move.</span></span> <span data-ttu-id="66669-108">VM을 이동하면 새 리소스 ID를 사용하도록 도구 및 스크립트를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66669-108">Once the VM has been moved, you need to update your tools and scripts to use the new resource IDs.</span></span> 
> 
> 

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="use-powershell-to-move-a-vm"></a><span data-ttu-id="66669-109">PowerShell을 사용하여 VM 이동</span><span class="sxs-lookup"><span data-stu-id="66669-109">Use Powershell to move a VM</span></span>
<span data-ttu-id="66669-110">가상 컴퓨터를 다른 리소스 그룹에 이동하려면 모든 종속 리소스를 이동하는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66669-110">To move a virtual machine to another resource group, you need to make sure that you also move all of the dependent resources.</span></span> <span data-ttu-id="66669-111">AzureRMResource cmdlet을 사용하려면 리소스 이름과 리소스의 유형이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="66669-111">To use the Move-AzureRMResource cmdlet, you need the resource name and the type of resource.</span></span> <span data-ttu-id="66669-112">AzureRMResource cmdlet에서 둘 모두를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66669-112">You can get both from the Find-AzureRMResource cmdlet.</span></span>

    Find-AzureRMResource -ResourceGroupNameContains "<sourceResourceGroupName>"


<span data-ttu-id="66669-113">VM을 이동하려면 여러 리소스를 이동해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66669-113">To move a VM we need to move multiple resources.</span></span> <span data-ttu-id="66669-114">지금 막 각 리소스에 대한 별도의 변수를 만들고 나열했습니다.</span><span class="sxs-lookup"><span data-stu-id="66669-114">We can just create separate variables for each resource and then list them.</span></span> <span data-ttu-id="66669-115">이 예제는 VM에 대한 대부분의 기본 리소스를 포함하지만 필요에 따라 더 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66669-115">This example includes most of the basic resources for a VM, but you can add more as needed.</span></span>

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

<span data-ttu-id="66669-116">리소스를 다른 구독으로 이동하기 위해 **-DestinationSubscriptionId** 매개 변수를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="66669-116">To move the resources to different subscription, include the **-DestinationSubscriptionId** parameter.</span></span> 

    Move-AzureRmResource -DestinationSubscriptionId "<destinationSubscriptionID>" -DestinationResourceGroupName $destinationRG -ResourceId $vm.ResourceId, $storageAccount.ResourceId, $diagStorageAccount.ResourceId, $vNet.ResourceId, $nic.ResourceId, $ip.ResourceId, $nsg.ResourceId



<span data-ttu-id="66669-117">지정한 리소스를 이동할 것인지 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="66669-117">You will be asked to confirm that you want to move the specified resources.</span></span> <span data-ttu-id="66669-118">**Y** 를 입력하여 리소스를 이동할 것인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="66669-118">Type **Y** to confirm that you want to move the resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66669-119">다음 단계</span><span class="sxs-lookup"><span data-stu-id="66669-119">Next steps</span></span>
<span data-ttu-id="66669-120">리소스 그룹 및 구독 간의 다양한 유형의 리소스를 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66669-120">You can move many different types of resources between resource groups and subscriptions.</span></span> <span data-ttu-id="66669-121">자세한 내용을 보려면 [새 리소스 그룹 또는 구독으로 리소스 이동](../../resource-group-move-resources.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="66669-121">For more information, see [Move resources to new resource group or subscription](../../resource-group-move-resources.md).</span></span>    

