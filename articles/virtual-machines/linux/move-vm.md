---
title: "Azure에서 Linux VM aaaMove | Microsoft Docs"
description: "Hello 리소스 관리자 배포 모델에서 Linux VM tooanother Azure 구독 또는 리소스 그룹을 이동 합니다."
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
ms.openlocfilehash: 938d04234059111912f03e72d14dabd338bc0678
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-linux-vm-tooanother-subscription-or-resource-group"></a><span data-ttu-id="9fb44-103">Linux VM tooanother 구독 또는 리소스 그룹 이동</span><span class="sxs-lookup"><span data-stu-id="9fb44-103">Move a Linux VM tooanother subscription or resource group</span></span>
<span data-ttu-id="9fb44-104">이 문서는 방법을 단계별로 설명 toomove 리소스 그룹 또는 구독 간에 Linux VM입니다.</span><span class="sxs-lookup"><span data-stu-id="9fb44-104">This article walks you through how toomove a Linux VM between resource groups or subscriptions.</span></span> <span data-ttu-id="9fb44-105">개인 구독에서 VM을 만든 경우에 유용 수 있고 toomove 할 구독 간에 VM 이동 것 tooyour 회사의 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="9fb44-105">Moving a VM between subscriptions can be handy if you created a VM in a personal subscription and now want toomove it tooyour company's subscription.</span></span>

> [!IMPORTANT]
><span data-ttu-id="9fb44-106">지금은 Managed Disks를 이동할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9fb44-106">You cannot move Managed Disks at this time.</span></span> 
>
><span data-ttu-id="9fb44-107">새 리소스 Id는 hello 이동의 일부로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9fb44-107">New resource IDs are created as part of hello move.</span></span> <span data-ttu-id="9fb44-108">Hello VM 이동 되었거나, 해야 tooupdate 도구 및 스크립트 toouse hello 새 리소스 Id입니다.</span><span class="sxs-lookup"><span data-stu-id="9fb44-108">Once hello VM has been moved, you need tooupdate your tools and scripts toouse hello new resource IDs.</span></span> 
> 
> 

## <a name="use-hello-azure-cli-toomove-a-vm"></a><span data-ttu-id="9fb44-109">Hello Azure CLI toomove VM을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="9fb44-109">Use hello Azure CLI toomove a VM</span></span>
<span data-ttu-id="9fb44-110">toosuccessfully VM 이동 toomove hello VM 및 해당 관련 리소스를 모두 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb44-110">toosuccessfully move a VM, you need toomove hello VM and all its supporting resources.</span></span> <span data-ttu-id="9fb44-111">사용 하 여 hello **으로 azure 그룹 표시** 리소스 그룹 및 Id의 모든 hello 리소스 toolist 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="9fb44-111">Use hello **azure group show** command toolist all hello resources in a resource group and their IDs.</span></span> <span data-ttu-id="9fb44-112">이 명령은 tooa 파일의 toopipe hello 출력을 복사 하 고 hello Id 이후 명령에 붙여 넣을 수 있도록 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="9fb44-112">It helps toopipe hello output of this command tooa file so you can copy and paste hello IDs into later commands.</span></span>

    azure group show <resourceGroupName>

<span data-ttu-id="9fb44-113">toomove VM 및 해당 리소스 tooanother 리소스 그룹을 사용 하 여 hello **azure 리소스 이동** CLI 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="9fb44-113">toomove a VM and its resources tooanother resource group, use hello **azure resource move** CLI command.</span></span> <span data-ttu-id="9fb44-114">다음 예제는 hello 방법을 toomove VM 및 hello 가장 일반적인 리소스 필요한 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9fb44-114">hello following example shows how toomove a VM and hello most common resources it requires.</span></span> <span data-ttu-id="9fb44-115">사용 하 여 hello **-i** 매개 변수 및는 쉼표로 구분 된 목록 (공백) Id의 리소스 toomove hello에 대 한 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb44-115">We use hello **-i** parameter and pass in a comma-separated list (without spaces) of IDs for hello resources toomove.</span></span>

    vm=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Compute/virtualMachines/<vmName>
    nic=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkInterfaces/<nicName>
    nsg=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkSecurityGroups/<nsgName>
    pip=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/publicIPAddresses/<publicIPName>
    vnet=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/virtualNetworks/<vnetName>
    diag=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<diagnosticStorageAccountName>
    storage=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<storageAcountName>      

    azure resource move --ids $vm,$nic,$nsg,$pip,$vnet,$storage,$diag -d "<destinationResourceGroup>"

<span data-ttu-id="9fb44-116">Toomove 하려는 경우 VM과 해당 리소스 tooa 다른 구독 hello, hello 추가 **-대상 subscriptionId &#60; destinationSubscriptionID &#62;** toospecify hello 대상 구독 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="9fb44-116">If you want toomove hello VM and its resources tooa different subscription, add hello **--destination-subscriptionId &#60;destinationSubscriptionID&#62;** parameter toospecify hello destination subscription.</span></span>

<span data-ttu-id="9fb44-117">Tooadd 해야 Windows 컴퓨터에 hello 명령 프롬프트에서에서 작업 하는 경우는  **$**  hello 선언할 때 변수 이름 앞에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fb44-117">If you are working from hello Command Prompt on a Windows computer, you need tooadd a **$** in front of hello variable names when you declare them.</span></span> <span data-ttu-id="9fb44-118">Linux에서는 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9fb44-118">This isn't needed in Linux.</span></span>

<span data-ttu-id="9fb44-119">요청 tooconfirm toomove hello 원하는 리소스를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb44-119">You are asked tooconfirm that you want toomove hello specified resource.</span></span> <span data-ttu-id="9fb44-120">형식 **Y** tooconfirm toomove hello 리소스 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb44-120">Type **Y** tooconfirm that you want toomove hello resources.</span></span>

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="next-steps"></a><span data-ttu-id="9fb44-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9fb44-121">Next steps</span></span>
<span data-ttu-id="9fb44-122">리소스 그룹 및 구독 간의 다양한 유형의 리소스를 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fb44-122">You can move many different types of resources between resource groups and subscriptions.</span></span> <span data-ttu-id="9fb44-123">자세한 내용은 참조 [리소스 toonew 리소스 그룹이 나 구독 이동](../../resource-group-move-resources.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9fb44-123">For more information, see [Move resources toonew resource group or subscription](../../resource-group-move-resources.md).</span></span>    

