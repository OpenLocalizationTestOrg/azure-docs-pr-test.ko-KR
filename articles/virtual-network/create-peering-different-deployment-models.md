---
title: "Azure 가상 네트워크 피어링 만들기 - 서로 다른 배포 모델 - 같은 구독 | Microsoft Docs"
description: "같은 Azure 구독에 존재하는 서로 다른 Azure 배포 모델을 통해 만든 가상 네트워크 간의 가상 네트워크 피어링을 만드는 방법을 학습합니다."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: jdial;narayan;annahar
ms.openlocfilehash: 7d75d85863ce4b06ef1f552e0d583dec302f7ace
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="create-a-virtual-network-peering---different-deployment-models-same-subscription"></a><span data-ttu-id="4c0c5-103">가상 네트워크 피어링 만들기 - 서로 다른 배포 모델 및 같은 구독</span><span class="sxs-lookup"><span data-stu-id="4c0c5-103">Create a virtual network peering - different deployment models, same subscription</span></span> 

<span data-ttu-id="4c0c5-104">이 자습서에서는 서로 다른 배포 모델을 통해 만들어진 가상 네트워크 간의 가상 네트워크 피어링을 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-104">In this tutorial, you learn to create a virtual network peering between virtual networks created through different deployment models.</span></span> <span data-ttu-id="4c0c5-105">두 가상 네트워크는 동일한 구독에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-105">Both virtual networks exist in the same subscription.</span></span> <span data-ttu-id="4c0c5-106">두 가상 네트워크를 피어링하면 서로 다른 가상 네트워크에 있는 리소스가 같은 가상 네트워크에 있는 리소스인 것처럼 같은 대역폭 및 대기 시간으로 서로 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-106">Peering two virtual networks enables resources in different virtual networks to communicate with each other with the same bandwidth and latency as though the resources were in the same virtual network.</span></span> <span data-ttu-id="4c0c5-107">[가상 네트워크 피어링](virtual-network-peering-overview.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-107">Learn more about [Virtual network peering](virtual-network-peering-overview.md).</span></span> 

<span data-ttu-id="4c0c5-108">가상 네트워크 피어링을 만드는 단계는 가상 네트워크가 동일한 구독에 있는지 아니면 다른 구독에 있는지에 따라, 그리고 가상 네트워크가 어느 [Azure 배포 모델](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json)를 통해 생성되었는지에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-108">The steps to create a virtual network peering are different, depending on whether the virtual networks are in the same, or different, subscriptions, and which [Azure deployment model](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) the virtual networks are created through.</span></span> <span data-ttu-id="4c0c5-109">다음 표에 나온 시나리오를 클릭하여 다른 시나리오에서 가상 네트워크 피어링을 만드는 방법을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-109">Learn how to create a virtual network peering in other scenarios by clicking the scenario from the following table:</span></span>

|<span data-ttu-id="4c0c5-110">Azure 배포 모델</span><span class="sxs-lookup"><span data-stu-id="4c0c5-110">Azure deployment model</span></span>  | <span data-ttu-id="4c0c5-111">Azure 구독</span><span class="sxs-lookup"><span data-stu-id="4c0c5-111">Azure subscription</span></span>  |
|--------- |---------|
|[<span data-ttu-id="4c0c5-112">둘 다 리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="4c0c5-112">Both Resource Manager</span></span>](virtual-network-create-peering.md) |<span data-ttu-id="4c0c5-113">동일</span><span class="sxs-lookup"><span data-stu-id="4c0c5-113">Same</span></span>|
|[<span data-ttu-id="4c0c5-114">둘 다 리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="4c0c5-114">Both Resource Manager</span></span>](create-peering-different-subscriptions.md) |<span data-ttu-id="4c0c5-115">다름</span><span class="sxs-lookup"><span data-stu-id="4c0c5-115">Different</span></span>|
|[<span data-ttu-id="4c0c5-116">하나는 리소스 관리자, 다른 하나는 클래식</span><span class="sxs-lookup"><span data-stu-id="4c0c5-116">One Resource Manager, one classic</span></span>](create-peering-different-deployment-models-subscriptions.md) |<span data-ttu-id="4c0c5-117">다름</span><span class="sxs-lookup"><span data-stu-id="4c0c5-117">Different</span></span>|

<span data-ttu-id="4c0c5-118">클래식 배포 모델을 통해 배포된 두 가상 네트워크 간에는 가상 네트워크 피어링을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-118">A virtual network peering cannot be created between two virtual networks deployed through the classic deployment model.</span></span> <span data-ttu-id="4c0c5-119">가상 네트워크 피어링은 같은 Azure 지역에 있는 두 가상 네트워크 간에만 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-119">A virtual network peering can only be created between two virtual networks that exist in the same Azure region.</span></span> <span data-ttu-id="4c0c5-120">둘 다 클래식 배포 모델을 통해 생성된 가상 네트워크 또는 서로 다른 Azure 지역에 있는 가상 네트워크를 연결해야 할 경우 Azure [VPN Gateway](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)를 사용하여 가상 네트워크를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-120">If you need to connect virtual networks that were both created through the classic deployment model, or that exist in different Azure regions, you can use an Azure [VPN Gateway](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) to connect the virtual networks.</span></span> 

<span data-ttu-id="4c0c5-121">[Azure Portal](#portal), Azure [CLI(Command Line Interface)](#cli) 또는 Azure [PowerShell](#powershell)을 사용하여 가상 네트워크 피어링을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-121">You can use the [Azure portal](#portal), the Azure [command-line interface](#cli) (CLI), or Azure [PowerShell](#powershell) to create a virtual network peering.</span></span> <span data-ttu-id="4c0c5-122">앞의 도구 링크 중 원하는 도구 링크를 클릭하여 원하는 도구를 사용하여 가상 네트워크 피어링을 만드는 단계로 바로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-122">Click any of the previous tool links to go directly to the steps for creating a virtual network peering using your tool of choice.</span></span>

## <span data-ttu-id="4c0c5-123"><a name="cli"></a>피어링 만들기 - 포털</span><span class="sxs-lookup"><span data-stu-id="4c0c5-123"><a name="cli"></a>Create peering - Portal</span></span>

1. <span data-ttu-id="4c0c5-124">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-124">Log in to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4c0c5-125">로그인하는 데 사용하는 계정에 가상 네트워크 피어링을 만드는 데 필요한 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-125">The account you log in with must have the necessary permissions to create a virtual network peering.</span></span> <span data-ttu-id="4c0c5-126">자세한 내용은 이 문서의 [권한](#permissions) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-126">See the [Permissions](#permissions) section of this article for details.</span></span>
2. <span data-ttu-id="4c0c5-127">**+ 새로 만들기**, **네트워킹**, **가상 네트워크**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-127">Click **+ New**, click **Networking**, then click **Virtual network**.</span></span>
3. <span data-ttu-id="4c0c5-128">**가상 네트워크 만들기** 블레이드에서 다음 설정에 대한 값을 입력하거나 선택한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-128">In the **Create virtual network** blade, enter, or select values for the following settings, then click **Create**:</span></span>
    - <span data-ttu-id="4c0c5-129">**이름**: *myVnet1*</span><span class="sxs-lookup"><span data-stu-id="4c0c5-129">**Name**: *myVnet1*</span></span>
    - <span data-ttu-id="4c0c5-130">**주소 공간**: *10.0.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="4c0c5-130">**Address space**: *10.0.0.0/16*</span></span>
    - <span data-ttu-id="4c0c5-131">**서브넷 이름**: *기본값*</span><span class="sxs-lookup"><span data-stu-id="4c0c5-131">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="4c0c5-132">**서브넷 주소 범위**: *10.0.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="4c0c5-132">**Subnet address range**: *10.0.0.0/24*</span></span>
    - <span data-ttu-id="4c0c5-133">**구독**: 사용자의 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-133">**Subscription**: Select your subscription</span></span>
    - <span data-ttu-id="4c0c5-134">**리소스 그룹**: **새로 만들기**를 선택하고 *myResourceGroup*을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-134">**Resource group**: Select **Create new** and enter *myResourceGroup*</span></span>
    - <span data-ttu-id="4c0c5-135">**위치**: *미국 동부*</span><span class="sxs-lookup"><span data-stu-id="4c0c5-135">**Location**: *East US*</span></span>
4. <span data-ttu-id="4c0c5-136">**+새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-136">Click **+ New**.</span></span> <span data-ttu-id="4c0c5-137">**Marketplace 검색** 상자에 *가상 네트워크*를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-137">In the **Search the Marketplace** box, type *Virtual network*.</span></span> <span data-ttu-id="4c0c5-138">검색 결과에 표시되는 **가상 네트워크**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-138">Click **Virtual network** when it appears in the search results.</span></span> 
5. <span data-ttu-id="4c0c5-139">**가상 네트워크** 블레이드의 **배포 모델 선택** 상자에서 **클래식**을 선택한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-139">In the **Virtual network** blade, select **Classic** in the **Select a deployment model** box, and then click **Create**.</span></span>
6. <span data-ttu-id="4c0c5-140">**가상 네트워크 만들기** 블레이드에서 다음 설정에 대한 값을 입력하거나 선택한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-140">In the **Create virtual network** blade, enter, or select values for the following settings, then click **Create**:</span></span>
    - <span data-ttu-id="4c0c5-141">**이름**: *myVnet2*</span><span class="sxs-lookup"><span data-stu-id="4c0c5-141">**Name**: *myVnet2*</span></span>
    - <span data-ttu-id="4c0c5-142">**주소 공간**: *10.1.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="4c0c5-142">**Address space**: *10.1.0.0/16*</span></span>
    - <span data-ttu-id="4c0c5-143">**서브넷 이름**: *기본값*</span><span class="sxs-lookup"><span data-stu-id="4c0c5-143">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="4c0c5-144">**서브넷 주소 범위**: *10.1.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="4c0c5-144">**Subnet address range**: *10.1.0.0/24*</span></span>
    - <span data-ttu-id="4c0c5-145">**구독**: 사용자의 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-145">**Subscription**: Select your subscription</span></span>
    - <span data-ttu-id="4c0c5-146">**리소스 그룹**: **기존 항목 사용**을 선택하고 *myResourceGroup*을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-146">**Resource group**: Select **Use existing** and select *myResourceGroup*</span></span>
    - <span data-ttu-id="4c0c5-147">**위치**: *미국 동부*</span><span class="sxs-lookup"><span data-stu-id="4c0c5-147">**Location**: *East US*</span></span>
7. <span data-ttu-id="4c0c5-148">포털 위쪽에 있는 **리소스 검색** 상자에 *myResourceGroup*을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-148">In the **Search resources** box at the top of the portal, type *myResourceGroup*.</span></span> <span data-ttu-id="4c0c5-149">**myResourceGroup**이 검색 결과에 표시되면 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-149">Click **myResourceGroup** when it appears in the search results.</span></span> <span data-ttu-id="4c0c5-150">**myresourcegroup** 리소스 그룹에 대한 블레이드가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-150">A blade appears for the **myresourcegroup** resource group.</span></span> <span data-ttu-id="4c0c5-151">리소스 그룹에는 이전 단계에서 만든 두 가상 네트워크가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-151">The resource group contains the two virtual networks created in previous steps.</span></span>
8. <span data-ttu-id="4c0c5-152">**myVNet1**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-152">Click **myVNet1**.</span></span>
9. <span data-ttu-id="4c0c5-153">나타나는 **myVnet1** 블레이드의 왼쪽에 있는 세로 옵션 목록에서 **피어링**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-153">In the **myVnet1** blade that appears, click **Peerings** from the vertical list of options on the left side of the blade.</span></span>
10. <span data-ttu-id="4c0c5-154">나타난 **myVnet1 - 피어링** 블레이드에서 **+ 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-154">In the **myVnet1 - Peerings** blade that appeared, click **+ Add**</span></span>
11. <span data-ttu-id="4c0c5-155">나타나는 **피어링 추가** 블레이드에서 다음 옵션을 입력하거나 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-155">In the **Add peering** blade that appears, enter, or select the following options, then click **OK**:</span></span>
     - <span data-ttu-id="4c0c5-156">**이름**: *myVnet1ToMyVnet2*</span><span class="sxs-lookup"><span data-stu-id="4c0c5-156">**Name**: *myVnet1ToMyVnet2*</span></span>
     - <span data-ttu-id="4c0c5-157">**가상 네트워크 배포 모델**: **클래식**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-157">**Virtual network deployment model**:  Select **Classic**.</span></span> 
     - <span data-ttu-id="4c0c5-158">**구독**: 사용자의 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-158">**Subscription**: Select your subscription</span></span>
     - <span data-ttu-id="4c0c5-159">**가상 네트워크**: **가상 네트워크 선택**을 클릭한 다음 **myVnet2**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-159">**Virtual network**:  Click **Choose a virtual network**, then click **myVnet2**.</span></span>
     - <span data-ttu-id="4c0c5-160">**가상 네트워크 액세스 허용:** **사용**이 선택되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-160">**Allow virtual network access:** Ensure that **Enabled** is selected.</span></span>
    <span data-ttu-id="4c0c5-161">이 자습서에서 다른 설정은 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-161">No other settings are used in this tutorial.</span></span> <span data-ttu-id="4c0c5-162">모든 피어링 설정에 대해 알아보려면 [가상 네트워크 피어링 관리](virtual-network-manage-peering.md#create-a-peering)를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-162">To learn about all peering settings, read [Manage virtual network peerings](virtual-network-manage-peering.md#create-a-peering).</span></span>
12. <span data-ttu-id="4c0c5-163">이전 단계에서 **확인**을 클릭한 후 **피어링 추가** 블레이드가 닫히고 **myVnet1 - 피어링** 블레이드가 다시 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-163">After clicking **OK** in the previous step, the **Add peering** blade closes and you see the **myVnet1 - Peerings** blade again.</span></span> <span data-ttu-id="4c0c5-164">몇 초 후 만든 피어링이 블레이드에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-164">After a few seconds, the peering you created appears in the blade.</span></span> <span data-ttu-id="4c0c5-165">만든 **myVnet1ToMyVnet2** 피어링의 **PEERING STATUS** 열에**Connected**가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-165">**Connected** is listed in the **PEERING STATUS** column for the **myVnet1ToMyVnet2** peering you created.</span></span>

    <span data-ttu-id="4c0c5-166">이제 피어링이 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-166">The peering is now established.</span></span> <span data-ttu-id="4c0c5-167">어느 쪽 가상 네트워크에서든 만든 모든 Azure 리소스는 이제 해당 IP 주소를 통해 서로 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-167">Any Azure resources you create in either virtual network are now able to communicate with each other through their IP addresses.</span></span> <span data-ttu-id="4c0c5-168">가상 네트워크에 대해 기본 Azure 이름 확인을 사용 중인 경우 가상 네트워크의 리소스가 가상 네트워크에서 이름을 확인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-168">If you're using default Azure name resolution for the virtual networks, the resources in the virtual networks are not able to resolve names across the virtual networks.</span></span> <span data-ttu-id="4c0c5-169">피어링의 가상 네트워크에서 이름을 확인하려면 자체 DNS 서버를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-169">If you want to resolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="4c0c5-170">[자체 DNS 서버를 이용한 이름 확인](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) 설정 방법을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-170">Learn how to set up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>
13. <span data-ttu-id="4c0c5-171">**선택 사항**: 이 자습서에서 가상 컴퓨터를 만드는 내용은 다루지 않지만, 각 가상 네트워크에서 가상 컴퓨터를 만들고 한 가상 컴퓨터에서 다른 가상 컴퓨터로 연결하여 연결의 유효성을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-171">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine to the other, to validate connectivity.</span></span>
14. <span data-ttu-id="4c0c5-172">**선택 사항**: 이 자습서에서 만든 리소스를 삭제하려면 이 문서의 [리소스 삭제](#delete-portal) 섹션에서 설명하는 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-172">**Optional**: To delete the resources that you create in this tutorial, complete the steps in the [Delete resources](#delete-portal) section of this article.</span></span>

## <span data-ttu-id="4c0c5-173"><a name="cli"></a>피어링 만들기 - Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4c0c5-173"><a name="cli"></a>Create peering - Azure CLI</span></span>

1. <span data-ttu-id="4c0c5-174">가상 네트워크(클래식)를 만들려면 Azure CLI 1.0을 [설치](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-174">[Install](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) the Azure CLI 1.0 to create the virtual network (classic).</span></span>
2. <span data-ttu-id="4c0c5-175">명령 세션을 열고 `azure login` 명령을 사용하여 Azure에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-175">Open a command session and log in to Azure using the `azure login` command.</span></span>
3. <span data-ttu-id="4c0c5-176">`azure config mode asm` 명령을 입력하여 CLI를 서비스 관리 모드에서 실행합니다. </span><span class="sxs-lookup"><span data-stu-id="4c0c5-176">Run the CLI in Service Management mode by entering the `azure config mode asm` command.</span></span>
4. <span data-ttu-id="4c0c5-177">다음 명령을 입력하여 가상 네트워크(클래식)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-177">Enter the following command to create the virtual network (classic):</span></span>
 
    ```azurecli
    azure network vnet create --vnet myVnet2 --address-space 10.1.0.0 --cidr 16 --location "East US"
    ```

5. <span data-ttu-id="4c0c5-178">리소스 그룹 및 가상 네트워크(리소스 관리자)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-178">Create a resource group and a virtual network (Resource Manager).</span></span> <span data-ttu-id="4c0c5-179">CLI 1.0 또는 2.0을 사용할 수 있습니다([설치](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="4c0c5-179">You can use either the CLI 1.0 or 2.0 ([install](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)).</span></span> <span data-ttu-id="4c0c5-180">피어링을 만들 때는 CLI 2.0을 사용해야 하기 때문에 이 자습서에서는 2.0을 사용하여 가상 네트워크(리소스 관리자)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-180">In this tutorial, the CLI 2.0 is used to create the virtual network (Resource Manager), since 2.0 must be used to create the peering.</span></span> <span data-ttu-id="4c0c5-181">CLI 2.0.4 이상을 설치한 로컬 컴퓨터에서 다음 Bash CLI 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-181">Execute the following bash CLI script from your local machine with the CLI 2.0.4 or later installed.</span></span> <span data-ttu-id="4c0c5-182">Windows 클라이언트에서의 Bash CLI 스크립트 실행과 관련한 옵션은 [Windows에서 Azure CLI 실행](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-182">For options on running bash CLI scripts on Windows client, see [Running the Azure CLI in Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="4c0c5-183">Azure Cloud Shell을 사용하여 스크립트를 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-183">You can also run the script using the Azure Cloud Shell.</span></span> <span data-ttu-id="4c0c5-184">Azure Cloud Shell은 Azure Portal에서 직접 실행할 수 있는 평가판 Bash 셸입니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-184">The Azure Cloud Shell is a free Bash shell that you can run directly within the Azure portal.</span></span> <span data-ttu-id="4c0c5-185">Azure CLI가 사전 설치되어 계정에서 사용하도록 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-185">It has the Azure CLI preinstalled and configured to use with your account.</span></span> <span data-ttu-id="4c0c5-186">다음 스크립트에서 **사용해보기** 단추를 클릭하면 Azure 계정 로그인 가능성을 기록하는 Cloud Shell이 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-186">Click the **Try it** button in the script that follows, which invokes a Cloud Shell that logs you can log in to your Azure account with.</span></span> <span data-ttu-id="4c0c5-187">스크립트를 실행하려면 **복사** 단추를 클릭하여 내용을 Cloud Shell에 붙여 넣고 `Enter`를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-187">To execute the script, click the **Copy** button and paste, the contents into your Cloud Shell, then press `Enter`.</span></span>

    ```azurecli-interactive
    #!/bin/bash

    # Create a resource group.
    az group create \
      --name myResourceGroup \
      --location eastus

    # Create the virtual network (Resource Manager).
    az network vnet create \
      --name myVnet1 \
      --resource-group myResourceGroup \
      --location eastus \
      --address-prefix 10.0.0.0/16
    ```

6. <span data-ttu-id="4c0c5-188">서로 다른 배포 모델을 통해 만들어진 두 가상 네트워크 사이에 가상 네트워크 피어링을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-188">Create a virtual network peering between the two virtual networks created through the different deployment models.</span></span> <span data-ttu-id="4c0c5-189">PC의 텍스트 편집기에 다음 스크립트를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-189">Copy the following script to a text editor on your PC.</span></span> <span data-ttu-id="4c0c5-190">`<subscription id>`는 구독 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-190">Replace `<subscription id>` with your subscription Id.</span></span> <span data-ttu-id="4c0c5-191">구독 ID를 모르는 경우 `az account show` 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-191">If you don't know your subscription Id, enter the `az account show` command.</span></span> <span data-ttu-id="4c0c5-192">출력에 표시되는 **id** 값이 구독 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-192">The value for **id** in the output is your subscription Id.</span></span> <span data-ttu-id="4c0c5-193">CLI 세션에 수정된 스크립트를 붙여 넣고 `Enter`를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-193">Paste the modified script in to your CLI session, and then press `Enter`.</span></span>

    ```azurecli-interactive
    # Get the id for VNet1.
    vnet1Id=$(az network vnet show \
      --resource-group myResourceGroup \
      --name myVnet1 \
      --query id --out tsv)

    # Peer VNet1 to VNet2.
    az network vnet peering create \
      --name myVnet1ToMyVnet2 \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --remote-vnet-id /subscriptions/<subscription id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnet2 \
      --allow-vnet-access
    ```
7. <span data-ttu-id="4c0c5-194">스크립트를 실행한 후 가상 네트워크에 대한 피어링을 검토합니다(리소스 관리자).</span><span class="sxs-lookup"><span data-stu-id="4c0c5-194">After the script executes, review the peering for the virtual network (Resource Manager).</span></span> <span data-ttu-id="4c0c5-195">다음 명령을 복사하여 CLI 세션에 붙여 넣고 `Enter`를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-195">Copy the following command, paste it in your CLI session, and then press `Enter`:</span></span>

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --output table
    ```
    
    <span data-ttu-id="4c0c5-196">출력에서 **PeeringState** 열에 **Connected**가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-196">The output shows **Connected** in the **PeeringState** column.</span></span> 

    <span data-ttu-id="4c0c5-197">어느 쪽 가상 네트워크에서든 만든 모든 Azure 리소스는 이제 해당 IP 주소를 통해 서로 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-197">Any Azure resources you create in either virtual network are now able to communicate with each other through their IP addresses.</span></span> <span data-ttu-id="4c0c5-198">가상 네트워크에 대해 기본 Azure 이름 확인을 사용 중인 경우 가상 네트워크의 리소스가 가상 네트워크에서 이름을 확인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-198">If you're using default Azure name resolution for the virtual networks, the resources in the virtual networks are not able to resolve names across the virtual networks.</span></span> <span data-ttu-id="4c0c5-199">피어링의 가상 네트워크에서 이름을 확인하려면 자체 DNS 서버를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-199">If you want to resolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="4c0c5-200">[자체 DNS 서버를 이용한 이름 확인](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) 설정 방법을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-200">Learn how to set up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>
8. <span data-ttu-id="4c0c5-201">**선택 사항**: 이 자습서에서 가상 컴퓨터를 만드는 내용은 다루지 않지만, 각 가상 네트워크에서 가상 컴퓨터를 만들고 한 가상 컴퓨터에서 다른 가상 컴퓨터로 연결하여 연결의 유효성을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-201">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine to the other, to validate connectivity.</span></span>
9. <span data-ttu-id="4c0c5-202">**선택 사항**: 이 자습서에서 만든 리소스를 삭제하려면 이 문서의 [리소스 삭제](#delete-cli)에서 설명하는 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-202">**Optional**: To delete the resources that you create in this tutorial, complete the steps in [Delete resources](#delete-cli) in this article.</span></span>

## <span data-ttu-id="4c0c5-203"><a name="powershell"></a>피어링 만들기 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="4c0c5-203"><a name="powershell"></a>Create peering - PowerShell</span></span>

1. <span data-ttu-id="4c0c5-204">최신 버전의 PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) 및 [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-204">Install the latest version of the PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) and [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modules.</span></span> <span data-ttu-id="4c0c5-205">Azure PowerShell을 처음 사용하는 경우 [Azure PowerShell 개요](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-205">If you're new to Azure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="4c0c5-206">PowerShell 세션을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-206">Start a PowerShell session.</span></span>
3. <span data-ttu-id="4c0c5-207">PowerShell에서 `Add-AzureAccount` 명령을 입력하여 Azure에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-207">In PowerShell, log in to Azure by entering the `Add-AzureAccount` command.</span></span>
4. <span data-ttu-id="4c0c5-208">PowerShell에 가상 네트워크(클래식)를 만들려면 기존 네트워크 구성 파일을 새로 만들거나 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-208">To create a virtual network (classic) with PowerShell, you must create a new, or modify an existing, network configuration file.</span></span> <span data-ttu-id="4c0c5-209">[네트워크 구성 파일 내보내기, 업데이트 및 가져오기](virtual-networks-using-network-configuration-file.md) 방법을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-209">Learn how to [export, update, and import network configuration files](virtual-networks-using-network-configuration-file.md).</span></span> <span data-ttu-id="4c0c5-210">파일에는 이 자습서에서 사용되는 가상 네트워크에 대한 **VirtualNetworkSite** 요소가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-210">The file should include the following **VirtualNetworkSite** element for the virtual network used in this tutorial:</span></span>

    ```xml
    <VirtualNetworkSite name="myVnet2" Location="East US">
      <AddressSpace>
        <AddressPrefix>10.1.0.0/16</AddressPrefix>
      </AddressSpace>
      <Subnets>
        <Subnet name="default">
          <AddressPrefix>10.1.0.0/24</AddressPrefix>
        </Subnet>
      </Subnets>
    </VirtualNetworkSite>
    ```

    > [!WARNING]
    > <span data-ttu-id="4c0c5-211">변경된 네트워크 구성 파일을 가져오면 구독의 기존 가상 네트워크(클래식)에 변경을 초래할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-211">Importing a changed network configuration file can cause changes to existing virtual networks (classic) in your subscription.</span></span> <span data-ttu-id="4c0c5-212">이전 가상 네트워크만 추가하고, 구독에서 기존 가상 네트워크를 변경하거나 제거하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-212">Ensure you only add the previous virtual network and that you don't change or remove any existing virtual networks from your subscription.</span></span> 
5. <span data-ttu-id="4c0c5-213">`login-azurermaccount` 명령을 입력하여 Azure에 로그인하고 가상 네트워크(리소스 관리자)를 만듭니다. </span><span class="sxs-lookup"><span data-stu-id="4c0c5-213">Log in to Azure to create the virtual network (Resource Manager) by entering the `login-azurermaccount` command.</span></span> <span data-ttu-id="4c0c5-214">로그인하는 데 사용한 계정에 가상 네트워크 피어링을 만드는 데 필요한 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-214">The account you log in with must have the necessary permissions to create a virtual network peering.</span></span> <span data-ttu-id="4c0c5-215">자세한 내용은 이 문서의 [권한](#permissions) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-215">See the [Permissions](#permissions) section of this article for details.</span></span>
6. <span data-ttu-id="4c0c5-216">리소스 그룹 및 가상 네트워크(리소스 관리자)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-216">Create a resource group and a virtual network (Resource Manager).</span></span> <span data-ttu-id="4c0c5-217">스크립트 복사하여 PowerShell에 붙여 넣고 `Enter`를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-217">Copy the script, paste it into PowerShell, and then press `Enter`.</span></span>

    ```powershell
    # Create a resource group.
      New-AzureRmResourceGroup -Name myResourceGroup -Location eastus

    # Create the virtual network (Resource Manager).
      $vnet1 = New-AzureRmVirtualNetwork `
      -ResourceGroupName myResourceGroup `
      -Name 'myVnet1' `
      -AddressPrefix '10.0.0.0/16' `
      -Location eastus
    ```

7. <span data-ttu-id="4c0c5-218">서로 다른 배포 모델을 통해 만들어진 두 가상 네트워크 사이에 가상 네트워크 피어링을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-218">Create a virtual network peering between the two virtual networks created through the different deployment models.</span></span> <span data-ttu-id="4c0c5-219">PC의 텍스트 편집기에 다음 스크립트를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-219">Copy the following script to a text editor on your PC.</span></span> <span data-ttu-id="4c0c5-220">`<subscription id>`는 구독 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-220">Replace `<subscription id>` with your subscription Id.</span></span> <span data-ttu-id="4c0c5-221">구독 ID를 모르는 경우 `Get-AzureRmSubscription` 명령을 입력하여 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-221">If you don't know your subscription Id, enter the `Get-AzureRmSubscription` command to view it.</span></span> <span data-ttu-id="4c0c5-222">반환된 출력의 **ID** 값이 구독 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-222">The value for **Id** in the returned output is your subscription ID.</span></span> <span data-ttu-id="4c0c5-223">스크립트를 실행하려면 텍스트 편집기에서 수정된 스크립트를 복사한 다음 PowerShell 세션을 마우스 오른쪽 단추로 클릭하고 `Enter`를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-223">To execute the script, copy the modified script from your text editor, then right-click in your PowerShell session, and then press `Enter`.</span></span>

    ```powershell
    # Peer VNet1 to VNet2.
    Add-AzureRmVirtualNetworkPeering `
      -Name myVnet1ToMyVnet2 `
      -VirtualNetwork $vnet1 `
      -RemoteVirtualNetworkId /subscriptions/<subscription Id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnet2
    ```

8. <span data-ttu-id="4c0c5-224">스크립트를 실행한 후 가상 네트워크에 대한 피어링을 검토합니다(리소스 관리자).</span><span class="sxs-lookup"><span data-stu-id="4c0c5-224">After the script executes, review the peering for the virtual network (Resource Manager).</span></span> <span data-ttu-id="4c0c5-225">다음 명령을 복사하여 PowerShell 세션에 붙여 넣고 `Enter`를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-225">Copy the following command, paste it in your PowerShell session, and then press `Enter`:</span></span>

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroup `
      -VirtualNetworkName myVnet1 `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    <span data-ttu-id="4c0c5-226">출력에서 **PeeringState** 열에 **Connected**가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-226">The output shows **Connected** in the **PeeringState** column.</span></span>

    <span data-ttu-id="4c0c5-227">어느 쪽 가상 네트워크에서든 만든 모든 Azure 리소스는 이제 해당 IP 주소를 통해 서로 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-227">Any Azure resources you create in either virtual network are now able to communicate with each other through their IP addresses.</span></span> <span data-ttu-id="4c0c5-228">가상 네트워크에 대해 기본 Azure 이름 확인을 사용 중인 경우 가상 네트워크의 리소스가 가상 네트워크에서 이름을 확인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-228">If you're using default Azure name resolution for the virtual networks, the resources in the virtual networks are not able to resolve names across the virtual networks.</span></span> <span data-ttu-id="4c0c5-229">피어링의 가상 네트워크에서 이름을 확인하려면 자체 DNS 서버를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-229">If you want to resolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="4c0c5-230">[자체 DNS 서버를 이용한 이름 확인](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) 설정 방법을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-230">Learn how to set up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

9. <span data-ttu-id="4c0c5-231">**선택 사항**: 이 자습서에서 가상 컴퓨터를 만드는 내용은 다루지 않지만, 각 가상 네트워크에서 가상 컴퓨터를 만들고 한 가상 컴퓨터에서 다른 가상 컴퓨터로 연결하여 연결의 유효성을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-231">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine to the other, to validate connectivity.</span></span>
10. <span data-ttu-id="4c0c5-232">**선택 사항**: 이 자습서에서 만든 리소스를 삭제하려면 이 문서의 [리소스 삭제](#delete-powershell)에서 설명하는 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-232">**Optional**: To delete the resources that you create in this tutorial, complete the steps in [Delete resources](#delete-powershell) in this article.</span></span>
 
## <span data-ttu-id="4c0c5-233"><a name="permissions"></a>권한</span><span class="sxs-lookup"><span data-stu-id="4c0c5-233"><a name="permissions"></a>Permissions</span></span>

<span data-ttu-id="4c0c5-234">가상 네트워크 피어링을 만드는 데 사용하는 계정에 필요한 역할 또는 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-234">The accounts you use to create a virtual network peering must have the necessary role or permissions.</span></span> <span data-ttu-id="4c0c5-235">예를 들어 myVnet1과 myVnet2라는 두 가상 네트워크를 피어링하는 경우 계정에는 각 가상 네트워크에 대한 다음과 같은 최소 역할 또는 권한이 할당되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-235">For example, if you were peering two virtual networks named myVnet1 and myVnet2, your account must be assigned the following minimum role or permissions for each virtual network:</span></span>
    
|<span data-ttu-id="4c0c5-236">가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="4c0c5-236">Virtual network</span></span>|<span data-ttu-id="4c0c5-237">배포 모델</span><span class="sxs-lookup"><span data-stu-id="4c0c5-237">Deployment model</span></span>|<span data-ttu-id="4c0c5-238">역할</span><span class="sxs-lookup"><span data-stu-id="4c0c5-238">Role</span></span>|<span data-ttu-id="4c0c5-239">권한</span><span class="sxs-lookup"><span data-stu-id="4c0c5-239">Permissions</span></span>|
|---|---|---|---|
|<span data-ttu-id="4c0c5-240">myVnet1</span><span class="sxs-lookup"><span data-stu-id="4c0c5-240">myVnet1</span></span>|<span data-ttu-id="4c0c5-241">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="4c0c5-241">Resource Manager</span></span>|[<span data-ttu-id="4c0c5-242">네트워크 참여자</span><span class="sxs-lookup"><span data-stu-id="4c0c5-242">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="4c0c5-243">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span><span class="sxs-lookup"><span data-stu-id="4c0c5-243">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span></span>|
| |<span data-ttu-id="4c0c5-244">클래식</span><span class="sxs-lookup"><span data-stu-id="4c0c5-244">Classic</span></span>|[<span data-ttu-id="4c0c5-245">클래식 네트워크 참여자</span><span class="sxs-lookup"><span data-stu-id="4c0c5-245">Classic Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|<span data-ttu-id="4c0c5-246">해당 없음</span><span class="sxs-lookup"><span data-stu-id="4c0c5-246">N/A</span></span>|
|<span data-ttu-id="4c0c5-247">myVnet2</span><span class="sxs-lookup"><span data-stu-id="4c0c5-247">myVnet2</span></span>|<span data-ttu-id="4c0c5-248">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="4c0c5-248">Resource Manager</span></span>|[<span data-ttu-id="4c0c5-249">네트워크 참여자</span><span class="sxs-lookup"><span data-stu-id="4c0c5-249">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="4c0c5-250">Microsoft.Network/virtualNetworks/peer</span><span class="sxs-lookup"><span data-stu-id="4c0c5-250">Microsoft.Network/virtualNetworks/peer</span></span>|
||<span data-ttu-id="4c0c5-251">클래식</span><span class="sxs-lookup"><span data-stu-id="4c0c5-251">Classic</span></span>|[<span data-ttu-id="4c0c5-252">클래식 네트워크 참여자</span><span class="sxs-lookup"><span data-stu-id="4c0c5-252">Classic Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|<span data-ttu-id="4c0c5-253">Microsoft.ClassicNetwork/virtualNetworks/peer</span><span class="sxs-lookup"><span data-stu-id="4c0c5-253">Microsoft.ClassicNetwork/virtualNetworks/peer</span></span>|

<span data-ttu-id="4c0c5-254">[기본 제공 역할](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) 및 [사용자 지정 역할](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json)에 특정 권한 할당(Resource Manager만 해당)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-254">Learn more about [built-in roles](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) and assigning specific permissions to [custom roles](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (Resource Manager only).</span></span>

## <span data-ttu-id="4c0c5-255"><a name="delete"></a>리소스 삭제</span><span class="sxs-lookup"><span data-stu-id="4c0c5-255"><a name="delete"></a>Delete resources</span></span>
<span data-ttu-id="4c0c5-256">이 자습서를 마친 경우 사용 요금이 발생하지 않도록 자습서에서 만든 리소스를 삭제하려고 할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-256">When you've finished this tutorial, you might want to delete the resources you created in the tutorial, so you don't incur usage charges.</span></span> <span data-ttu-id="4c0c5-257">리소스 그룹을 삭제하면 리소스 그룹에 있는 리소스도 모두 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-257">Deleting a resource group also deletes all resources that are in the resource group.</span></span>

### <span data-ttu-id="4c0c5-258"><a name="delete-portal"></a>Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4c0c5-258"><a name="delete-portal"></a>Azure portal</span></span>

1. <span data-ttu-id="4c0c5-259">포털 검색 상자에 **myResourceGroup**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-259">In the portal search box, enter **myResourceGroup**.</span></span> <span data-ttu-id="4c0c5-260">검색 결과에서 **myResourceGroup**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-260">In the search results, click **myResourceGroup**.</span></span>
2. <span data-ttu-id="4c0c5-261">**myResourceGroup** 블레이드에서 **삭제** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-261">On the **myResourceGroup** blade, click the **Delete** icon.</span></span>
3. <span data-ttu-id="4c0c5-262">삭제를 확인하려면 **리소스 그룹 이름 입력** 상자에 **myResourceGroup**을 입력한 다음 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-262">To confirm the deletion, in the **TYPE THE RESOURCE GROUP NAME** box, enter **myResourceGroup**, and then click **Delete**.</span></span>

### <span data-ttu-id="4c0c5-263"><a name="delete-cli"></a>Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4c0c5-263"><a name="delete-cli"></a>Azure CLI</span></span>

1. <span data-ttu-id="4c0c5-264">Azure CLI 2.0을 사용하여 다음 명령을 통해 가상 네트워크(리소스 관리자)를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-264">Use the Azure CLI 2.0 to delete the virtual network (Resource Manager) with the following command:</span></span>

    ```azurecli-interactive
    az group delete --name myResourceGroup --yes
    ```

2. <span data-ttu-id="4c0c5-265">Azure CLI 1.0을 사용하여 다음 명령을 통해 가상 네트워크(클래식)를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-265">Use the Azure CLI 1.0 to delete the virtual network (classic) with the following commands:</span></span>

    ```azurecli
    azure config mode asm

    azure network vnet delete --vnet myVnet2 --quiet
    ```

### <span data-ttu-id="4c0c5-266"><a name="delete-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="4c0c5-266"><a name="delete-powershell"></a>PowerShell</span></span>

1. <span data-ttu-id="4c0c5-267">다음 명령을 입력하여 가상 네트워크(리소스 관리자)를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-267">Enter the following command to delete the virtual network (Resource Manager):</span></span>

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroup -Force
    ```

2. <span data-ttu-id="4c0c5-268">PowerShell을 통해 가상 네트워크(클래식)를 삭제하려면 기존 네트워크 구성 파일을 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-268">To delete the virtual network (classic) with PowerShell, you must modify an existing network configuration file.</span></span> <span data-ttu-id="4c0c5-269">[네트워크 구성 파일 내보내기, 업데이트 및 가져오기](virtual-networks-using-network-configuration-file.md) 방법을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-269">Learn how to [export, update, and import network configuration files](virtual-networks-using-network-configuration-file.md).</span></span> <span data-ttu-id="4c0c5-270">이 자습서에서 사용되는 가상 네트워크에 대한 다음 VirtualNetworkSite 요소를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-270">Remove the following VirtualNetworkSite element for the virtual network used in this tutorial:</span></span>

    ```xml
    <VirtualNetworkSite name="myVnet2" Location="East US">
      <AddressSpace>
        <AddressPrefix>10.1.0.0/16</AddressPrefix>
      </AddressSpace>
      <Subnets>
        <Subnet name="default">
          <AddressPrefix>10.1.0.0/24</AddressPrefix>
        </Subnet>
      </Subnets>
    </VirtualNetworkSite>
    ```

    > [!WARNING]
    > <span data-ttu-id="4c0c5-271">변경된 네트워크 구성 파일을 가져오면 구독의 기존 가상 네트워크(클래식)에 변경을 초래할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-271">Importing a changed network configuration file can cause changes to existing virtual networks (classic) in your subscription.</span></span> <span data-ttu-id="4c0c5-272">이전 가상 네트워크만 제거하고, 구독에서 다른 기존 가상 네트워크를 변경하거나 제거하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-272">Ensure you only remove the previous virtual network and that you don't change or remove any other existing virtual networks from your subscription.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="4c0c5-273">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4c0c5-273">Next steps</span></span>

- <span data-ttu-id="4c0c5-274">프로덕션 환경에 사용하기 위한 가상 네트워크 피어링을 만들기 전에 먼저 중요한 [가상 네트워크 피어링 제약 조건 및 동작](virtual-network-manage-peering.md#requirements-and-constraints)에 철저하게 익숙해집니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-274">Thoroughly familiarize yourself with important [virtual network peering constraints and behaviors](virtual-network-manage-peering.md#requirements-and-constraints) before creating a virtual network peering for production use.</span></span>
- <span data-ttu-id="4c0c5-275">모든 [가상 네트워크 피어링 설정](virtual-network-manage-peering.md#create-a-peering)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-275">Learn about all [virtual network peering settings](virtual-network-manage-peering.md#create-a-peering).</span></span>
- <span data-ttu-id="4c0c5-276">가상 네트워크 피어링을 통해 [허브 및 스포크 네트워크 토폴로지를 만드는](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4c0c5-276">Learn how to [create a hub and spoke network topology](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) with virtual network peering.</span></span>
