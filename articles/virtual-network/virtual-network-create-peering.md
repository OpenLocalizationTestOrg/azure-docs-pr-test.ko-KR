---
title: "aaaCreate는 Azure 가상 네트워크 피어 링-리소스 관리자-동일한 구독 | Microsoft Docs"
description: "Toocreate 리소스 관리자를 통해 동일한 hello에 존재 하는 가상 네트워크 간의 가상 네트워크 피어 링 생성 하는 방법을 알아보려면 Azure 구독."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 026bca75-2946-4c03-b4f6-9f3c5809c69a
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: jdial;narayan;annahar
ms.openlocfilehash: c2d24fdc8103c09c3bfb8e59be12e301d9e9a55a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---resource-manager-same-subscription"></a><span data-ttu-id="507d7-103">가상 네트워크 피어링 만들기 - Resource Manager, 동일한 구독</span><span class="sxs-lookup"><span data-stu-id="507d7-103">Create a virtual network peering - Resource Manager, same subscription</span></span>

<span data-ttu-id="507d7-104">이 자습서에서는 toocreate 리소스 관리자를 통해 만든 가상 네트워크 간의 피어 링 하는 가상 네트워크를 학습 합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-104">In this tutorial, you learn toocreate a virtual network peering between virtual networks created through Resource Manager.</span></span> <span data-ttu-id="507d7-105">Hello에 두 가상 네트워크가 있는 동일한 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-105">Both virtual networks exist in hello same subscription.</span></span> <span data-ttu-id="507d7-106">Hello에 hello 리소스 것 처럼 동일한 대역폭 및 대기 시간으로 서로 toocommunicate 서로 다른 가상 네트워크의에서 피어 링 두 가상 네트워크 사용 리소스 hello 동일한 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-106">Peering two virtual networks enables resources in different virtual networks toocommunicate with each other with hello same bandwidth and latency as though hello resources were in hello same virtual network.</span></span> <span data-ttu-id="507d7-107">[가상 네트워크 피어링](virtual-network-peering-overview.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="507d7-107">Learn more about [Virtual network peering](virtual-network-peering-overview.md).</span></span> 

<span data-ttu-id="507d7-108">hello 단계 toocreate 피어 링 가상 네트워크는 hello 가상 네트워크는 hello 같거나 다른 데이터 집합, 구독 및 있는에 있는지 여부에 따라 다른 [Azure 배포 모델](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello 가상 네트워크가 만들어집니다. 통해</span><span class="sxs-lookup"><span data-stu-id="507d7-108">hello steps toocreate a virtual network peering are different, depending on whether hello virtual networks are in hello same, or different, subscriptions, and which [Azure deployment model](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello virtual networks are created through.</span></span> <span data-ttu-id="507d7-109">가상 a toocreate 네트워크 hello 시나리오 hello 다음 표를에서 클릭 하 여 다른 시나리오에서는 피어 링 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-109">Learn how toocreate a virtual network peering in other scenarios by clicking hello scenario from hello following table:</span></span>

|<span data-ttu-id="507d7-110">Azure 배포 모델</span><span class="sxs-lookup"><span data-stu-id="507d7-110">Azure deployment model</span></span>  | <span data-ttu-id="507d7-111">Azure 구독</span><span class="sxs-lookup"><span data-stu-id="507d7-111">Azure subscription</span></span>  |
|--------- |---------|
|[<span data-ttu-id="507d7-112">둘 다 Resource Manager</span><span class="sxs-lookup"><span data-stu-id="507d7-112">Both Resource Manager</span></span>](create-peering-different-subscriptions.md) |<span data-ttu-id="507d7-113">다름</span><span class="sxs-lookup"><span data-stu-id="507d7-113">Different</span></span>|
|[<span data-ttu-id="507d7-114">하나는 Resource Manager, 하나는 클래식</span><span class="sxs-lookup"><span data-stu-id="507d7-114">One Resource Manager, one classic</span></span>](create-peering-different-deployment-models.md) |<span data-ttu-id="507d7-115">동일</span><span class="sxs-lookup"><span data-stu-id="507d7-115">Same</span></span>|
|[<span data-ttu-id="507d7-116">하나는 Resource Manager, 하나는 클래식</span><span class="sxs-lookup"><span data-stu-id="507d7-116">One Resource Manager, one classic</span></span>](create-peering-different-deployment-models-subscriptions.md) |<span data-ttu-id="507d7-117">다름</span><span class="sxs-lookup"><span data-stu-id="507d7-117">Different</span></span>|

<span data-ttu-id="507d7-118">Hello 클래식 배포 모델을 통해 배포 된 두 개의 가상 네트워크 간의 피어 링 가상 네트워크를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-118">A virtual network peering cannot be created between two virtual networks deployed through hello classic deployment model.</span></span> <span data-ttu-id="507d7-119">동일한 hello에 존재 하는 두 개의 가상 네트워크 간에 만들 수는 가상 네트워크 피어 링 Azure 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-119">A virtual network peering can only be created between two virtual networks that exist in hello same Azure region.</span></span> <span data-ttu-id="507d7-120">Azure를 사용할 수 있는 hello 클래식 배포 모델을 통해 생성 된 또는 서로 다른 Azure 지역에 있는 가상 네트워크 tooconnect 해야 할 경우 [VPN 게이트웨이](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-120">If you need tooconnect virtual networks that were both created through hello classic deployment model, or that exist in different Azure regions, you can use an Azure [VPN Gateway](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello virtual networks.</span></span> 

<span data-ttu-id="507d7-121">Hello를 사용할 수 있습니다 [Azure 포털](#portal), Azure hello [명령줄 인터페이스](#cli) (CLI) Azure [PowerShell](#powershell), 또는 [Azure리소스관리자템플릿](#template) toocreate 가상 네트워크 피어 링입니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-121">You can use hello [Azure portal](#portal), hello Azure [command-line interface](#cli) (CLI), Azure [PowerShell](#powershell), or an [Azure Resource Manager template](#template) toocreate a virtual network peering.</span></span> <span data-ttu-id="507d7-122">Toohello 원하는 도구를 사용 하 여 가상 네트워크 피어 링을 만들기 위한 단계를 직접 hello 이전 도구 링크 toogo 중 하나를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-122">Click any of hello previous tool links toogo directly toohello steps for creating a virtual network peering using your tool of choice.</span></span>

## <span data-ttu-id="507d7-123"><a name="portal"></a>피어링 만들기 - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="507d7-123"><a name="portal"></a>Create peering - Azure portal</span></span>

1. <span data-ttu-id="507d7-124">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-124">Log in toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="507d7-125">가상 네트워크 피어 링 hello 필요한 권한을 toocreate 사용 하 여 로그인 하는 hello 계정에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-125">hello account you log in with must have hello necessary permissions toocreate a virtual network peering.</span></span> <span data-ttu-id="507d7-126">Hello 참조 [권한을](#permissions) 대 한 자세한 내용은이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="507d7-126">See hello [Permissions](#permissions) section of this article for details.</span></span>
2. <span data-ttu-id="507d7-127">**+ 새로 만들기**, **네트워킹**, **가상 네트워크**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-127">Click **+ New**, click **Networking**, then click **Virtual network**.</span></span>
3. <span data-ttu-id="507d7-128">Hello에 **가상 네트워크 만들기** 블레이드에서 입력 하거나 hello 설정, 다음에 대 한 값을 선택한 다음 클릭 **만들기**:</span><span class="sxs-lookup"><span data-stu-id="507d7-128">In hello **Create virtual network** blade, enter, or select values for hello following settings, then click **Create**:</span></span>
    - <span data-ttu-id="507d7-129">**이름**: *myVnet1*</span><span class="sxs-lookup"><span data-stu-id="507d7-129">**Name**: *myVnet1*</span></span>
    - <span data-ttu-id="507d7-130">**주소 공간**: *10.0.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="507d7-130">**Address space**: *10.0.0.0/16*</span></span>
    - <span data-ttu-id="507d7-131">**서브넷 이름**: *기본값*</span><span class="sxs-lookup"><span data-stu-id="507d7-131">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="507d7-132">**서브넷 주소 범위**: *10.0.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="507d7-132">**Subnet address range**: *10.0.0.0/24*</span></span>
    - <span data-ttu-id="507d7-133">**구독**: 사용자의 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-133">**Subscription**: Select your subscription</span></span>
    - <span data-ttu-id="507d7-134">**리소스 그룹**: **새로 만들기**를 선택하고 *myResourceGroup*을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-134">**Resource group**: Select **Create new** and enter *myResourceGroup*</span></span>
    - <span data-ttu-id="507d7-135">**위치**: *미국 동부*</span><span class="sxs-lookup"><span data-stu-id="507d7-135">**Location**: *East US*</span></span>
4. <span data-ttu-id="507d7-136">단계 2-3 다음 3 단계에서 값에는 hello를 다시 지정을 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-136">Complete steps 2-3 again specifying hello following values in step 3:</span></span>
    - <span data-ttu-id="507d7-137">**이름**: *myVnet2*</span><span class="sxs-lookup"><span data-stu-id="507d7-137">**Name**: *myVnet2*</span></span>
    - <span data-ttu-id="507d7-138">**주소 공간**: *10.1.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="507d7-138">**Address space**: *10.1.0.0/16*</span></span>
    - <span data-ttu-id="507d7-139">**서브넷 이름**: *기본값*</span><span class="sxs-lookup"><span data-stu-id="507d7-139">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="507d7-140">**서브넷 주소 범위**: *10.1.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="507d7-140">**Subnet address range**: *10.1.0.0/24*</span></span>
    - <span data-ttu-id="507d7-141">**구독**: 사용자의 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-141">**Subscription**: Select your subscription</span></span>
    - <span data-ttu-id="507d7-142">**리소스 그룹**: **기존 항목 사용**을 선택하고 *myResourceGroup*을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-142">**Resource group**: Select **Use existing** and select *myResourceGroup*</span></span>
    - <span data-ttu-id="507d7-143">**위치**: *미국 동부*</span><span class="sxs-lookup"><span data-stu-id="507d7-143">**Location**: *East US*</span></span>
5. <span data-ttu-id="507d7-144">Hello에 **리소스 검색** 형식 hello 포털의 hello 상단 상자 *myResourceGroup*합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-144">In hello **Search resources** box at hello top of hello portal, type *myResourceGroup*.</span></span> <span data-ttu-id="507d7-145">클릭 **myResourceGroup** hello 검색 결과에 표시 되 면입니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-145">Click **myResourceGroup** when it appears in hello search results.</span></span> <span data-ttu-id="507d7-146">블레이드 hello에 대 한 표시 **myresourcegroup** 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-146">A blade appears for hello **myresourcegroup** resource group.</span></span> <span data-ttu-id="507d7-147">hello 리소스 그룹 이전 단계에서 만든 hello 두 가상 네트워크를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-147">hello resource group contains hello two virtual networks created in previous steps.</span></span>
6. <span data-ttu-id="507d7-148">**myVNet1**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-148">Click **myVNet1**.</span></span>
7. <span data-ttu-id="507d7-149">Hello에 **myVnet1** 블레이드를 놓고 클릭 **피어 링** hello 세로 hello hello 블레이드의 왼쪽에 옵션 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-149">In hello **myVnet1** blade that appears, click **Peerings** from hello vertical list of options on hello left side of hello blade.</span></span>
8. <span data-ttu-id="507d7-150">Hello에 **myVnet1-피어 링** 나타나면 블레이드 클릭 **+ 추가**</span><span class="sxs-lookup"><span data-stu-id="507d7-150">In hello **myVnet1 - Peerings** blade that appeared, click **+ Add**</span></span>
9. <span data-ttu-id="507d7-151">Hello에 **추가 피어 링** 나타나는 블레이드를 입력 하거나 hello 다음 옵션을 선택한 다음 클릭 **확인**:</span><span class="sxs-lookup"><span data-stu-id="507d7-151">In hello **Add peering** blade that appears, enter, or select hello following options, then click **OK**:</span></span>
     - <span data-ttu-id="507d7-152">**이름**: *myVnet1ToMyVnet2*</span><span class="sxs-lookup"><span data-stu-id="507d7-152">**Name**: *myVnet1ToMyVnet2*</span></span>
     - <span data-ttu-id="507d7-153">**가상 네트워크 배포 모델**: **Resource Manager**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-153">**Virtual network deployment model**:  Select **Resource Manager**.</span></span> 
     - <span data-ttu-id="507d7-154">**구독**: 사용자의 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-154">**Subscription**: Select your subscription</span></span>
     - <span data-ttu-id="507d7-155">**가상 네트워크**: **가상 네트워크 선택**을 클릭한 다음 **myVnet2**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-155">**Virtual network**:  Click **Choose a virtual network**, then click **myVnet2**.</span></span>
     - <span data-ttu-id="507d7-156">**가상 네트워크 액세스 허용:** **사용**이 선택되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-156">**Allow virtual network access:** Ensure that **Enabled** is selected.</span></span>
    <span data-ttu-id="507d7-157">이 자습서에서 다른 설정은 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-157">No other settings are used in this tutorial.</span></span> <span data-ttu-id="507d7-158">모든 피어 링 설정에 대 한 toolearn 읽을 [관리 가상 네트워크 피어 링](virtual-network-manage-peering.md#create-a-peering)합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-158">toolearn about all peering settings, read [Manage virtual network peerings](virtual-network-manage-peering.md#create-a-peering).</span></span>
10. <span data-ttu-id="507d7-159">클릭 한 후 **확인** hello 이전 단계에서 hello **추가 피어 링** 블레이드를 닫고 hello 참조 **myVnet1-피어 링** 블레이드를 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-159">After clicking **OK** in hello previous step, hello **Add peering** blade closes and you see hello **myVnet1 - Peerings** blade again.</span></span> <span data-ttu-id="507d7-160">몇 초 후 사용자가 만든 피어 링 hello hello 블레이드에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-160">After a few seconds, hello peering you created appears in hello blade.</span></span> <span data-ttu-id="507d7-161">**시작** hello에 나열 된 **피어 링 상태** hello에 대 한 열 **myVnet1ToMyVnet2** 만든 피어 링 있습니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-161">**Initiated** is listed in hello **PEERING STATUS** column for hello **myVnet1ToMyVnet2** peering you created.</span></span> <span data-ttu-id="507d7-162">Vnet1 tooVnet2 살펴본 하지만 myVnet2 toomyVnet1 피어 투 피어 해야 이제 합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-162">You've peered Vnet1 tooVnet2, but now you must peer myVnet2 toomyVnet1.</span></span> <span data-ttu-id="507d7-163">hello 피어 링 만들어야 양방향에서 hello 가상 네트워크 toocommunicate의 tooenable 리소스 서로 합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-163">hello peering must be created in both directions tooenable resources in hello virtual networks toocommunicate with each other.</span></span>
11. <span data-ttu-id="507d7-164">myVnet2에 대해 5~10단계를 다시 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-164">Complete steps 5-10 again for myVnet2.</span></span>  <span data-ttu-id="507d7-165">이름 hello 피어 링 *myVnet2ToMyVnet1*합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-165">Name hello peering *myVnet2ToMyVnet1*.</span></span>
12. <span data-ttu-id="507d7-166">클릭 한 후 몇 초 **확인** toocreate hello 피어 링 MyVnet2에 대 한 hello **myVnet2ToMyVnet1** 방금 만든 피어 링이 함께 나열 **연결 됨** hello 에서 **피어 링 상태** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-166">A few seconds after clicking **OK** toocreate hello peering for MyVnet2, hello **myVnet2ToMyVnet1** peering you just created is listed with **Connected** in hello **PEERING STATUS** column.</span></span>
13. <span data-ttu-id="507d7-167">MyVnet1에 대해 5~7단계를 다시 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-167">Complete steps 5-7 again for MyVnet1.</span></span> <span data-ttu-id="507d7-168">hello **피어 링 상태** hello에 대 한 **myVnet1ToVNet2** 피어 링는 현재 **연결 됨**합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-168">hello **PEERING STATUS** for hello **myVnet1ToVNet2** peering is now also **Connected**.</span></span> <span data-ttu-id="507d7-169">hello 피어 링은 성공적으로 설정 확인 한 후 **연결 됨** hello에 **피어 링 상태** hello 피어 링에서 두 가상 네트워크에 대 한 열입니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-169">hello peering is successfully established after you see **Connected** in hello **PEERING STATUS** column for both virtual networks in hello peering.</span></span>
14. <span data-ttu-id="507d7-170">**선택적**: 가상 컴퓨터를 만들어이 자습서에서 다루지 않습니다, 경우에 각 가상 네트워크에서 가상 컴퓨터를 만들 하 고 기타, 하나의 가상 컴퓨터 toohello toovalidate 연결에서에서 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-170">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
15. <span data-ttu-id="507d7-171">**선택적**:이 자습서에서 만드는 toodelete hello 리소스 hello에서 단계를 완료 hello [리소스를 삭제](#delete-portal) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="507d7-171">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in hello [Delete resources](#delete-portal) section of this article.</span></span>

<span data-ttu-id="507d7-172">가상 네트워크 중 하나에서 만드는 모든 Azure 리소스의 IP 주소를 통해 서로 수 toocommunicate 됩니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-172">Any Azure resources you create in either virtual network are now able toocommunicate with each other through their IP addresses.</span></span> <span data-ttu-id="507d7-173">Hello 가상 네트워크에 대 한 기본 Azure 이름 확인을 사용 중인 경우 hello hello 가상 네트워크의 리소스가 하지 수 tooresolve 이름을 hello 가상 네트워크를 통해입니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-173">If you're using default Azure name resolution for hello virtual networks, hello resources in hello virtual networks are not able tooresolve names across hello virtual networks.</span></span> <span data-ttu-id="507d7-174">피어 링의 가상 네트워크에서 tooresolve 이름을 하려는 경우 자체 DNS 서버를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-174">If you want tooresolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="507d7-175">자세한 방법을를 tooset [자체 DNS 서버를 사용 하 여 이름 확인](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-175">Learn how tooset up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

## <span data-ttu-id="507d7-176"><a name="cli"></a>피어링 만들기 - Azure CLI</span><span class="sxs-lookup"><span data-stu-id="507d7-176"><a name="cli"></a>Create peering - Azure CLI</span></span>

<span data-ttu-id="507d7-177">다음 스크립트는 hello:</span><span class="sxs-lookup"><span data-stu-id="507d7-177">hello following script:</span></span>

- <span data-ttu-id="507d7-178">Hello Azure CLI 버전 2.0.4 필요 이상.</span><span class="sxs-lookup"><span data-stu-id="507d7-178">Requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="507d7-179">toofind hello 버전을 실행 hello `az --version` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-179">toofind hello version, run hello `az --version` command.</span></span> <span data-ttu-id="507d7-180">Tooupgrade 필요한 경우 참조 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-180">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
- <span data-ttu-id="507d7-181">Bash 셸에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-181">Works in a Bash shell.</span></span> <span data-ttu-id="507d7-182">Windows 클라이언트에서 Azure CLI 스크립트를 실행 하는 옵션에 대 한 참조 [hello Azure CLI Windows에서 실행 중인](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-182">For options on running Azure CLI scripts on Windows client, see [Running hello Azure CLI in Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> 

<span data-ttu-id="507d7-183">CLI hello 및 해당 종속성을 설치 하는 대신 Azure 클라우드 셸 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-183">Instead of installing hello CLI and its dependencies, you can use hello Azure Cloud Shell.</span></span> <span data-ttu-id="507d7-184">Azure 클라우드 셸 hello hello Azure 포털 내에서 직접 실행할 수 있는 무료 Bash 셸의입니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-184">hello Azure Cloud Shell is a free Bash shell that you can run directly within hello Azure portal.</span></span> <span data-ttu-id="507d7-185">Hello Azure CLI 사전 설치 및 toouse 사용자 계정으로 구성 된이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-185">It has hello Azure CLI preinstalled and configured toouse with your account.</span></span> <span data-ttu-id="507d7-186">Hello 클릭 **실습** 된 Azure 계정 로그는 클라우드 셸을 호출 하는 다음과 같이 tooyour 로그인 할 수 있는 hello 스크립트에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-186">Click hello **Try it** button in hello script that follows, which invokes a Cloud Shell that logs you can log in tooyour Azure account with.</span></span> <span data-ttu-id="507d7-187">tooexecute 스크립트 hello를 hello 클릭 **복사** 단추 및 클라우드 Shell에 hello 내용을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-187">tooexecute hello script, click hello **Copy** button and paste hello contents into your Cloud Shell.</span></span>

1. <span data-ttu-id="507d7-188">리소스 그룹 하나와 두 개의 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-188">Create a resource group and two virtual networks.</span></span>

    ```azurecli-interactive
    #!/bin/bash

    # Variables for common values used throughout hello script.
    rgName="myResourceGroup"
    location="eastus"

    # Create a resource group.
    az group create \
      --name $rgName \
      --location $location

    # Create virtual network 1.
    az network vnet create \
      --name myVnet1 \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.0.0.0/16

    # Create virtual network 2.
    az network vnet create \
      --name myVnet2 \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.1.0.0/16
    ```

2. <span data-ttu-id="507d7-189">Hello 두 가상 네트워크 간의 피어 링 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-189">Create a virtual network peering between hello two virtual networks.</span></span>
 
    ```azurecli-interactive
    # Get hello id for VNet1.
    vnet1Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet1 \
      --query id --out tsv)

    # Get hello id for VNet2.
    vnet2Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet2 \
      --query id \
      --out tsv)

    # Peer VNet1 tooVNet2.
    az network vnet peering create \
      --name myVnet1ToMyVnet2 \
      --resource-group $rgName \
      --vnet-name myVnet1 \
      --remote-vnet-id $vnet2Id \
      --allow-vnet-access

    # Peer VNet2 tooVNet1.
    az network vnet peering create \
      --name myVnet2ToMyVnet1 \
      --resource-group $rgName \
      --vnet-name myVnet2 \
      --remote-vnet-id $vnet1Id \
      --allow-vnet-access
    ```

3. <span data-ttu-id="507d7-190">Hello 스크립트를 실행 한 후 각 가상 네트워크에 대 한 hello 피어 링을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-190">After hello script executes, review hello peerings for each virtual network.</span></span> 

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --output table
    ```
    
    <span data-ttu-id="507d7-191">Hello 이전 명령의 다시 실행 하 여 대체 *myVnet1* 와 *myVnet2*합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-191">Run hello previous command again, replacing *myVnet1* with *myVnet2*.</span></span> <span data-ttu-id="507d7-192">hello 출력 둘 다의 명령을 보여 줍니다 **연결 됨** hello에 **PeeringState** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-192">hello output of both commands shows **Connected** in hello **PeeringState** column.</span></span>

     <span data-ttu-id="507d7-193">가상 네트워크 중 하나에서 만드는 모든 Azure 리소스의 IP 주소를 통해 서로 수 toocommunicate 됩니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-193">Any Azure resources you create in either virtual network are now able toocommunicate with each other through their IP addresses.</span></span> <span data-ttu-id="507d7-194">Hello 가상 네트워크에 대 한 기본 Azure 이름 확인을 사용 중인 경우 hello hello 가상 네트워크의 리소스가 하지 수 tooresolve 이름을 hello 가상 네트워크를 통해입니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-194">If you're using default Azure name resolution for hello virtual networks, hello resources in hello virtual networks are not able tooresolve names across hello virtual networks.</span></span> <span data-ttu-id="507d7-195">피어 링의 가상 네트워크에서 tooresolve 이름을 하려는 경우 자체 DNS 서버를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-195">If you want tooresolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="507d7-196">자세한 방법을를 tooset [자체 DNS 서버를 사용 하 여 이름 확인](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-196">Learn how tooset up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

4. <span data-ttu-id="507d7-197">**선택적**: 가상 컴퓨터를 만들어이 자습서에서 다루지 않습니다, 경우에 각 가상 네트워크에서 가상 컴퓨터를 만들 하 고 기타, 하나의 가상 컴퓨터 toohello toovalidate 연결에서에서 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-197">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
5. <span data-ttu-id="507d7-198">**선택적**:이 자습서에서 만드는 toodelete hello 리소스의 단계를 완료 hello [리소스를 삭제](#delete-cli) 이 문서의 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-198">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in [Delete resources](#delete-cli) in this article.</span></span>


## <span data-ttu-id="507d7-199"><a name="powershell"></a>피어링 만들기 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="507d7-199"><a name="powershell"></a>Create peering - PowerShell</span></span>

1. <span data-ttu-id="507d7-200">Hello hello PowerShell의 최신 버전을 설치 [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-200">Install hello latest version of hello PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="507d7-201">새 tooAzure PowerShell 인 경우 참조 [Azure PowerShell 개요](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-201">If you're new tooAzure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="507d7-202">PowerShell 세션 toostart 너무 이동**시작**, 입력 **powershell**, 클릭 하 고 **PowerShell**합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-202">toostart a PowerShell session, go too**Start**, enter **powershell**, and then click **PowerShell**.</span></span>
3. <span data-ttu-id="507d7-203">PowerShell에서 로그인 tooAzure hello를 입력 하 여 `login-azurermaccount` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-203">In PowerShell, log in tooAzure by entering hello `login-azurermaccount` command.</span></span> <span data-ttu-id="507d7-204">가상 네트워크 피어 링 hello 필요한 권한을 toocreate 사용 하 여 로그인 하는 hello 계정에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-204">hello account you log in with must have hello necessary permissions toocreate a virtual network peering.</span></span> <span data-ttu-id="507d7-205">Hello 참조 [권한을](#permissions) 대 한 자세한 내용은이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="507d7-205">See hello [Permissions](#permissions) section of this article for details.</span></span>
4. <span data-ttu-id="507d7-206">리소스 그룹 하나와 두 개의 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-206">Create a resource group and two virtual networks.</span></span> <span data-ttu-id="507d7-207">tooexecute hello 스크립트 복사 hello 다음 스크립트, PowerShell에 붙여을 누릅니다 `Enter` hello 마지막 줄 hello 화면에 표시 된 후:</span><span class="sxs-lookup"><span data-stu-id="507d7-207">tooexecute hello script, copy hello following script, paste it into PowerShell, and then press `Enter` after hello last line appears on hello screen:</span></span>

    ```powershell
    # Variables for common values used throughout hello script.
    $rgName='myResourceGroup'
    $location='eastus'

    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name $rgName `
      -Location $location

    # Create virtual network 1.
    $vnet1 = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnet1' `
      -AddressPrefix '10.0.0.0/16' `
      -Location $location

    # Create virtual network 2.
    $vnet2 = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnet2' `
      -AddressPrefix '10.1.0.0/16' `
      -Location $location
    ```

5. <span data-ttu-id="507d7-208">Hello 두 가상 네트워크 간의 피어 링 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-208">Create a virtual network peering between hello two virtual networks.</span></span> <span data-ttu-id="507d7-209">복사 hello 다음 스크립트 tooPowerShell에 붙여 넣고 다음 키를 누릅니다 `Enter` hello 마지막 줄 hello 화면에 표시 된 후:</span><span class="sxs-lookup"><span data-stu-id="507d7-209">Copy hello following script, paste in tooPowerShell, and then press `Enter` after hello last line appears on hello screen:</span></span>
    ```powershell
    # Peer VNet1 tooVNet2.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet1ToMyVnet2' `
      -VirtualNetwork $vnet1 `
      -RemoteVirtualNetworkId $vnet2.Id

    # Peer VNet2 tooVNet1.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet2ToMyVnet1' `
      -VirtualNetwork $vnet2 `
      -RemoteVirtualNetworkId $vnet1.Id
    ```
6. <span data-ttu-id="507d7-210">tooreview hello 서브넷 hello 가상 네트워크에 대 한 복사 hello 다음 명령, tooPowerShell, 붙여 및 키를 누릅니다 `Enter`:</span><span class="sxs-lookup"><span data-stu-id="507d7-210">tooreview hello subnets for hello virtual network, copy hello following command, paste in tooPowerShell, and then press `Enter`:</span></span>

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroup `
      -VirtualNetworkName myVnet1 `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    <span data-ttu-id="507d7-211">Hello 이전 명령의 다시 실행 하 여 대체 *myVnet1* 와 *myVnet2*합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-211">Run hello previous command again, replacing *myVnet1* with *myVnet2*.</span></span> <span data-ttu-id="507d7-212">hello 출력 둘 다의 명령을 보여 줍니다 **연결 됨** hello에 **PeeringState** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-212">hello output of both commands shows **Connected** in hello **PeeringState** column.</span></span>
7. <span data-ttu-id="507d7-213">**선택적**: 가상 컴퓨터를 만들어이 자습서에서 다루지 않습니다, 경우에 각 가상 네트워크에서 가상 컴퓨터를 만들 하 고 기타, 하나의 가상 컴퓨터 toohello toovalidate 연결에서에서 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-213">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
8. <span data-ttu-id="507d7-214">**선택적**:이 자습서에서 만드는 toodelete hello 리소스의 단계를 완료 hello [리소스를 삭제](#delete-powershell) 이 문서의 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-214">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in [Delete resources](#delete-powershell) in this article.</span></span>

<span data-ttu-id="507d7-215">가상 네트워크 중 하나에서 만드는 모든 Azure 리소스의 IP 주소를 통해 서로 수 toocommunicate 됩니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-215">Any Azure resources you create in either virtual network are now able toocommunicate with each other through their IP addresses.</span></span> <span data-ttu-id="507d7-216">Hello 가상 네트워크에 대 한 기본 Azure 이름 확인을 사용 중인 경우 hello hello 가상 네트워크의 리소스가 하지 수 tooresolve 이름을 hello 가상 네트워크를 통해입니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-216">If you're using default Azure name resolution for hello virtual networks, hello resources in hello virtual networks are not able tooresolve names across hello virtual networks.</span></span> <span data-ttu-id="507d7-217">피어 링의 가상 네트워크에서 tooresolve 이름을 하려는 경우 자체 DNS 서버를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-217">If you want tooresolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="507d7-218">자세한 방법을를 tooset [자체 DNS 서버를 사용 하 여 이름 확인](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-218">Learn how tooset up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

## <span data-ttu-id="507d7-219"><a name="template"></a>피어링 만들기 - Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="507d7-219"><a name="template"></a>Create peering - Resource Manager template</span></span>

1. <span data-ttu-id="507d7-220">[가상 네트워크 피어링 만들기](https://azure.microsoft.com/resources/templates/201-vnet-to-vnet-peering) Resource Manager 템플릿을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-220">Reference [Create a virtual network peering](https://azure.microsoft.com/resources/templates/201-vnet-to-vnet-peering) Resource Manager template.</span></span> <span data-ttu-id="507d7-221">지침에는 Azure 포털, PowerShell 또는 Azure CLI hello hello를 사용 하 여 hello 서식 파일을 배포 하기 위한 hello 템플릿과 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-221">Instructions are provided with hello template for deploying hello template using hello Azure portal, PowerShell, or hello Azure CLI.</span></span> <span data-ttu-id="507d7-222">로그에 있는 계정을 사용 하 여 toodeploy hello 템플릿을 선택 하면 toowhichever 도구 가상 네트워크 피어 링 필요한 권한을 toocreate hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-222">Log in toowhichever tool you choose toodeploy hello template with using an account that has hello necessary permissions toocreate a virtual network peering.</span></span> <span data-ttu-id="507d7-223">Hello 참조 [권한을](#permissions) 대 한 자세한 내용은이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="507d7-223">See hello [Permissions](#permissions) section of this article for details.</span></span>
2. <span data-ttu-id="507d7-224">**선택적**: 가상 컴퓨터를 만들어이 자습서에서 다루지 않습니다, 경우에 각 가상 네트워크에서 가상 컴퓨터를 만들 하 고 기타, 하나의 가상 컴퓨터 toohello toovalidate 연결에서에서 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-224">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
3. <span data-ttu-id="507d7-225">**선택적**:이 자습서에서 만드는 toodelete hello 리소스 hello에서 단계를 완료 hello [리소스를 삭제](#delete) 중 하나를 사용 하 여이 문서의 섹션 hello Azure 포털, PowerShell 또는 Azure CLI hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-225">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in hello [Delete resources](#delete) section of this article, using either hello Azure portal, PowerShell, or hello Azure CLI.</span></span>

## <span data-ttu-id="507d7-226"><a name="permissions"></a>권한</span><span class="sxs-lookup"><span data-stu-id="507d7-226"><a name="permissions"></a>Permissions</span></span>

<span data-ttu-id="507d7-227">hello 계정 toocreate 가상 네트워크 피어 링을 사용 하 여 hello 필요한 역할 또는 사용 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-227">hello accounts you use toocreate a virtual network peering must have hello necessary role or permissions.</span></span> <span data-ttu-id="507d7-228">예를 들어 VNet1 및 VNet2 라는 두 개의 가상 네트워크, 피어 링 된 경우 사용자 계정에 할당 해야 최소 역할 또는 각 가상 네트워크에 대 한 사용 권한을 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="507d7-228">For example, if you were peering two virtual networks named VNet1 and VNet2, your account must be assigned hello following minimum role or permissions for each virtual network:</span></span>
    
|<span data-ttu-id="507d7-229">가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="507d7-229">Virtual network</span></span>|<span data-ttu-id="507d7-230">역할</span><span class="sxs-lookup"><span data-stu-id="507d7-230">Role</span></span>|<span data-ttu-id="507d7-231">권한</span><span class="sxs-lookup"><span data-stu-id="507d7-231">Permissions</span></span>|
|---|---|---|
|<span data-ttu-id="507d7-232">VNet1</span><span class="sxs-lookup"><span data-stu-id="507d7-232">VNet1</span></span>|[<span data-ttu-id="507d7-233">네트워크 참여자</span><span class="sxs-lookup"><span data-stu-id="507d7-233">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="507d7-234">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span><span class="sxs-lookup"><span data-stu-id="507d7-234">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span></span>|
|<span data-ttu-id="507d7-235">VNet2</span><span class="sxs-lookup"><span data-stu-id="507d7-235">VNet2</span></span>|[<span data-ttu-id="507d7-236">네트워크 참여자</span><span class="sxs-lookup"><span data-stu-id="507d7-236">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="507d7-237">Microsoft.Network/virtualNetworks/peer</span><span class="sxs-lookup"><span data-stu-id="507d7-237">Microsoft.Network/virtualNetworks/peer</span></span>|

<span data-ttu-id="507d7-238">에 대 한 자세한 내용은 [기본 제공 역할](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) 너무 특정 사용 권한을 할당 하 고[사용자 정의 역할](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (리소스 관리자에만 해당).</span><span class="sxs-lookup"><span data-stu-id="507d7-238">Learn more about [built-in roles](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) and assigning specific permissions too[custom roles](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (Resource Manager only).</span></span>

## <span data-ttu-id="507d7-239"><a name="delete"></a>리소스 삭제</span><span class="sxs-lookup"><span data-stu-id="507d7-239"><a name="delete"></a>Delete resources</span></span>
<span data-ttu-id="507d7-240">이 자습서를 마친 toodelete hello 리소스 사용량에 따른 요금을 발생 하지 않습니다 하므로 hello 자습서에서 만든 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-240">When you've finished this tutorial, you might want toodelete hello resources you created in hello tutorial, so you don't incur usage charges.</span></span> <span data-ttu-id="507d7-241">리소스 그룹을 삭제 하면 hello 리소스 그룹에는 모든 리소스를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-241">Deleting a resource group also deletes all resources that are in hello resource group.</span></span>

### <span data-ttu-id="507d7-242"><a name="delete-portal"></a>Azure Portal</span><span class="sxs-lookup"><span data-stu-id="507d7-242"><a name="delete-portal"></a>Azure portal</span></span>

1. <span data-ttu-id="507d7-243">Hello 포털 검색 상자에 입력 **myResourceGroup**합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-243">In hello portal search box, enter **myResourceGroup**.</span></span> <span data-ttu-id="507d7-244">Hello 검색 결과에서 클릭 **myResourceGroup**합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-244">In hello search results, click **myResourceGroup**.</span></span>
2. <span data-ttu-id="507d7-245">Hello에 **myResourceGroup** 블레이드에서 hello 클릭 **삭제** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-245">On hello **myResourceGroup** blade, click hello **Delete** icon.</span></span>
3. <span data-ttu-id="507d7-246">hello에 tooconfirm hello 삭제 **형식 hello 리소스 그룹 이름은** 상자에 입력 **myResourceGroup**, 클릭 하 고 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-246">tooconfirm hello deletion, in hello **TYPE hello RESOURCE GROUP NAME** box, enter **myResourceGroup**, and then click **Delete**.</span></span>

### <span data-ttu-id="507d7-247"><a name="delete-cli"></a>Azure CLI</span><span class="sxs-lookup"><span data-stu-id="507d7-247"><a name="delete-cli"></a>Azure CLI</span></span>

<span data-ttu-id="507d7-248">Hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-248">Enter hello following command:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

### <span data-ttu-id="507d7-249"><a name="delete-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="507d7-249"><a name="delete-powershell"></a>PowerShell</span></span>

<span data-ttu-id="507d7-250">Hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-250">Enter hello following command:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -force
```

## <a name="next-steps"></a><span data-ttu-id="507d7-251">다음 단계</span><span class="sxs-lookup"><span data-stu-id="507d7-251">Next steps</span></span>

- <span data-ttu-id="507d7-252">프로덕션 환경에 사용하기 위한 가상 네트워크 피어링을 만들기 전에 먼저 중요한 [가상 네트워크 피어링 제약 조건 및 동작](virtual-network-manage-peering.md#requirements-and-constraints)에 철저하게 익숙해집니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-252">Thoroughly familiarize yourself with important [virtual network peering constraints and behaviors](virtual-network-manage-peering.md#requirements-and-constraints) before creating a virtual network peering for production use.</span></span>
- <span data-ttu-id="507d7-253">모든 [가상 네트워크 피어링 설정](virtual-network-manage-peering.md#create-a-peering)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-253">Learn about all [virtual network peering settings](virtual-network-manage-peering.md#create-a-peering).</span></span>
- <span data-ttu-id="507d7-254">너무 방법에 대해 알아봅니다[허브를 만들고 네트워크 토폴로지 스포크](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) 가상 네트워크 피어 링을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="507d7-254">Learn how too[create a hub and spoke network topology](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) with virtual network peering.</span></span>
