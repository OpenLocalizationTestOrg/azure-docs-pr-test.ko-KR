---
title: "Azure의 Linux VM 이동 | Microsoft Docs"
description: "Resource Manager 배포 모델에서 다른 Azure 구독 또는 리소스 그룹으로 Linux VM을 이동합니다."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d635f0a5-4458-4b95-a5f8-eed4f41eb4d4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 4695a9c934f97f2b2d448c4990e7ad5533e38e9f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="move-a-linux-vm-to-another-subscription-or-resource-group"></a><span data-ttu-id="5177c-103">Linux VM을 다른 구독 또는 리소스 그룹으로 이동</span><span class="sxs-lookup"><span data-stu-id="5177c-103">Move a Linux VM to another subscription or resource group</span></span>
<span data-ttu-id="5177c-104">이 문서에서는 리소스 그룹 또는 구독 간에 Linux VM을 이동하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="5177c-104">This article walks you through how to move a Linux VM between resource groups or subscriptions.</span></span> <span data-ttu-id="5177c-105">개인 구독에서 VM을 만들고 회사 구독으로 이동하려면 구독 간의 VM 이동이 편리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5177c-105">Moving a VM between subscriptions can be handy if you created a VM in a personal subscription and now want to move it to your company's subscription.</span></span>

> [!IMPORTANT]
><span data-ttu-id="5177c-106">지금은 Managed Disks를 이동할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5177c-106">You cannot move Managed Disks at this time.</span></span> 
>
><span data-ttu-id="5177c-107">새 리소스 ID는 이동의 일부로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="5177c-107">New resource IDs are created as part of the move.</span></span> <span data-ttu-id="5177c-108">VM을 이동하면 새 리소스 ID를 사용하도록 도구 및 스크립트를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5177c-108">Once the VM has been moved, you need to update your tools and scripts to use the new resource IDs.</span></span> 
> 
> 

## <a name="use-the-azure-cli-to-move-a-vm"></a><span data-ttu-id="5177c-109">Azure CLI를 사용하여 VM 이동</span><span class="sxs-lookup"><span data-stu-id="5177c-109">Use the Azure CLI to move a VM</span></span>
<span data-ttu-id="5177c-110">VM을 성공적으로 이동하려면 VM 및 모든 지원 리소스를 이동해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5177c-110">To successfully move a VM, you need to move the VM and all its supporting resources.</span></span> <span data-ttu-id="5177c-111">**azure group show** 명령을 사용하여 리소스 그룹 및 해당 ID에서 모든 리소스를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="5177c-111">Use the **azure group show** command to list all the resources in a resource group and their IDs.</span></span> <span data-ttu-id="5177c-112">이후 명령에 ID를 복사하고 붙여넣을 수 있도록 파일에이 명령의 출력을 파이프할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5177c-112">It helps to pipe the output of this command to a file so you can copy and paste the IDs into later commands.</span></span>

    azure group show <resourceGroupName>

<span data-ttu-id="5177c-113">다른 리소스 그룹에 VM 또는 해당 리소스를 이동하려면 **azure resource move** CLI 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5177c-113">To move a VM and its resources to another resource group, use the **azure resource move** CLI command.</span></span> <span data-ttu-id="5177c-114">다음 예제에서는 필요한 VM 및 가장 일반적인 리소스를 이동하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5177c-114">The following example shows how to move a VM and the most common resources it requires.</span></span> <span data-ttu-id="5177c-115">**-i** 매개 변수를 사용하고 이동할 리소스에 대한 ID의 쉼표로 구분된 목록에 공백 없이 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="5177c-115">We use the **-i** parameter and pass in a comma-separated list (without spaces) of IDs for the resources to move.</span></span>

    vm=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Compute/virtualMachines/<vmName>
    nic=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkInterfaces/<nicName>
    nsg=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkSecurityGroups/<nsgName>
    pip=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/publicIPAddresses/<publicIPName>
    vnet=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/virtualNetworks/<vnetName>
    diag=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<diagnosticStorageAccountName>
    storage=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<storageAcountName>      

    azure resource move --ids $vm,$nic,$nsg,$pip,$vnet,$storage,$diag -d "<destinationResourceGroup>"

<span data-ttu-id="5177c-116">VM 및 해당 리소스를 다른 구독으로 이동하려는 경우 **--destination-subscriptionId &#60;destinationSubscriptionID&#62;** 매개 변수를 추가하여 대상 구독을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5177c-116">If you want to move the VM and its resources to a different subscription, add the **--destination-subscriptionId &#60;destinationSubscriptionID&#62;** parameter to specify the destination subscription.</span></span>

<span data-ttu-id="5177c-117">Windows 컴퓨터의 명령 프롬프트에서 작업하는 경우 선언할 때 변수 이름 앞에 **$** 를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5177c-117">If you are working from the Command Prompt on a Windows computer, you need to add a **$** in front of the variable names when you declare them.</span></span> <span data-ttu-id="5177c-118">Linux에서는 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5177c-118">This isn't needed in Linux.</span></span>

<span data-ttu-id="5177c-119">지정한 리소스를 이동할 것인지 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="5177c-119">You are asked to confirm that you want to move the specified resource.</span></span> <span data-ttu-id="5177c-120">**Y** 를 입력하여 리소스를 이동할 것인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5177c-120">Type **Y** to confirm that you want to move the resources.</span></span>

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="next-steps"></a><span data-ttu-id="5177c-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5177c-121">Next steps</span></span>
<span data-ttu-id="5177c-122">리소스 그룹 및 구독 간의 다양한 유형의 리소스를 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5177c-122">You can move many different types of resources between resource groups and subscriptions.</span></span> <span data-ttu-id="5177c-123">자세한 내용을 보려면 [새 리소스 그룹 또는 구독으로 리소스 이동](../../resource-group-move-resources.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5177c-123">For more information, see [Move resources to new resource group or subscription](../../resource-group-move-resources.md).</span></span>    

