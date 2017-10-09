---
title: "aaaCreate Azure 가상 네트워크 피어 링-다양 한 배포 모델-동일한 구독 | Microsoft Docs"
description: "Toocreate 동일 hello에 존재 하는 다른 Azure 배포 모델을 통해 만든 가상 네트워크 간의 가상 네트워크 피어 링 방법을 알아보려면 Azure 구독."
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
ms.openlocfilehash: 365156d651c9042ed52baeb15bf629fcc5329af8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---different-deployment-models-same-subscription"></a><span data-ttu-id="8c4a4-103">가상 네트워크 피어링 만들기 - 서로 다른 배포 모델 및 같은 구독</span><span class="sxs-lookup"><span data-stu-id="8c4a4-103">Create a virtual network peering - different deployment models, same subscription</span></span> 

<span data-ttu-id="8c4a4-104">이 자습서에서는 toocreate 다양 한 배포 모델을 통해 만든 가상 네트워크 간의 피어 링 하는 가상 네트워크를 학습 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-104">In this tutorial, you learn toocreate a virtual network peering between virtual networks created through different deployment models.</span></span> <span data-ttu-id="8c4a4-105">Hello에 두 가상 네트워크가 있는 동일한 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-105">Both virtual networks exist in hello same subscription.</span></span> <span data-ttu-id="8c4a4-106">Hello에 hello 리소스 것 처럼 동일한 대역폭 및 대기 시간으로 서로 toocommunicate 서로 다른 가상 네트워크의에서 피어 링 두 가상 네트워크 사용 리소스 hello 동일한 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-106">Peering two virtual networks enables resources in different virtual networks toocommunicate with each other with hello same bandwidth and latency as though hello resources were in hello same virtual network.</span></span> <span data-ttu-id="8c4a4-107">[가상 네트워크 피어링](virtual-network-peering-overview.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-107">Learn more about [Virtual network peering](virtual-network-peering-overview.md).</span></span> 

<span data-ttu-id="8c4a4-108">hello 단계 toocreate 피어 링 가상 네트워크는 hello 가상 네트워크는 hello 같거나 다른 데이터 집합, 구독 및 있는에 있는지 여부에 따라 다른 [Azure 배포 모델](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello 가상 네트워크가 만들어집니다. 통해</span><span class="sxs-lookup"><span data-stu-id="8c4a4-108">hello steps toocreate a virtual network peering are different, depending on whether hello virtual networks are in hello same, or different, subscriptions, and which [Azure deployment model](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello virtual networks are created through.</span></span> <span data-ttu-id="8c4a4-109">가상 a toocreate 네트워크 hello 시나리오 hello 다음 표를에서 클릭 하 여 다른 시나리오에서는 피어 링 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-109">Learn how toocreate a virtual network peering in other scenarios by clicking hello scenario from hello following table:</span></span>

|<span data-ttu-id="8c4a4-110">Azure 배포 모델</span><span class="sxs-lookup"><span data-stu-id="8c4a4-110">Azure deployment model</span></span>  | <span data-ttu-id="8c4a4-111">Azure 구독</span><span class="sxs-lookup"><span data-stu-id="8c4a4-111">Azure subscription</span></span>  |
|--------- |---------|
|[<span data-ttu-id="8c4a4-112">둘 다 리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="8c4a4-112">Both Resource Manager</span></span>](virtual-network-create-peering.md) |<span data-ttu-id="8c4a4-113">동일</span><span class="sxs-lookup"><span data-stu-id="8c4a4-113">Same</span></span>|
|[<span data-ttu-id="8c4a4-114">둘 다 리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="8c4a4-114">Both Resource Manager</span></span>](create-peering-different-subscriptions.md) |<span data-ttu-id="8c4a4-115">다름</span><span class="sxs-lookup"><span data-stu-id="8c4a4-115">Different</span></span>|
|[<span data-ttu-id="8c4a4-116">하나는 리소스 관리자, 다른 하나는 클래식</span><span class="sxs-lookup"><span data-stu-id="8c4a4-116">One Resource Manager, one classic</span></span>](create-peering-different-deployment-models-subscriptions.md) |<span data-ttu-id="8c4a4-117">다름</span><span class="sxs-lookup"><span data-stu-id="8c4a4-117">Different</span></span>|

<span data-ttu-id="8c4a4-118">Hello 클래식 배포 모델을 통해 배포 된 두 개의 가상 네트워크 간의 피어 링 가상 네트워크를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-118">A virtual network peering cannot be created between two virtual networks deployed through hello classic deployment model.</span></span> <span data-ttu-id="8c4a4-119">동일한 hello에 존재 하는 두 개의 가상 네트워크 간에 만들 수는 가상 네트워크 피어 링 Azure 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-119">A virtual network peering can only be created between two virtual networks that exist in hello same Azure region.</span></span> <span data-ttu-id="8c4a4-120">Azure를 사용할 수 있는 hello 클래식 배포 모델을 통해 생성 된 또는 서로 다른 Azure 지역에 있는 가상 네트워크 tooconnect 해야 할 경우 [VPN 게이트웨이](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-120">If you need tooconnect virtual networks that were both created through hello classic deployment model, or that exist in different Azure regions, you can use an Azure [VPN Gateway](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello virtual networks.</span></span> 

<span data-ttu-id="8c4a4-121">Hello를 사용할 수 있습니다 [Azure 포털](#portal), Azure hello [명령줄 인터페이스](#cli) (CLI) 또는 Azure [PowerShell](#powershell) toocreate 가상 네트워크 피어 링입니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-121">You can use hello [Azure portal](#portal), hello Azure [command-line interface](#cli) (CLI), or Azure [PowerShell](#powershell) toocreate a virtual network peering.</span></span> <span data-ttu-id="8c4a4-122">Toohello 원하는 도구를 사용 하 여 가상 네트워크 피어 링을 만들기 위한 단계를 직접 hello 이전 도구 링크 toogo 중 하나를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-122">Click any of hello previous tool links toogo directly toohello steps for creating a virtual network peering using your tool of choice.</span></span>

## <span data-ttu-id="8c4a4-123"><a name="cli"></a>피어링 만들기 - 포털</span><span class="sxs-lookup"><span data-stu-id="8c4a4-123"><a name="cli"></a>Create peering - Portal</span></span>

1. <span data-ttu-id="8c4a4-124">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-124">Log in toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="8c4a4-125">가상 네트워크 피어 링 hello 필요한 권한을 toocreate 사용 하 여 로그인 하는 hello 계정에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-125">hello account you log in with must have hello necessary permissions toocreate a virtual network peering.</span></span> <span data-ttu-id="8c4a4-126">Hello 참조 [권한을](#permissions) 대 한 자세한 내용은이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-126">See hello [Permissions](#permissions) section of this article for details.</span></span>
2. <span data-ttu-id="8c4a4-127">**+ 새로 만들기**, **네트워킹**, **가상 네트워크**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-127">Click **+ New**, click **Networking**, then click **Virtual network**.</span></span>
3. <span data-ttu-id="8c4a4-128">Hello에 **가상 네트워크 만들기** 블레이드에서 입력 하거나 hello 설정, 다음에 대 한 값을 선택한 다음 클릭 **만들기**:</span><span class="sxs-lookup"><span data-stu-id="8c4a4-128">In hello **Create virtual network** blade, enter, or select values for hello following settings, then click **Create**:</span></span>
    - <span data-ttu-id="8c4a4-129">**이름**: *myVnet1*</span><span class="sxs-lookup"><span data-stu-id="8c4a4-129">**Name**: *myVnet1*</span></span>
    - <span data-ttu-id="8c4a4-130">**주소 공간**: *10.0.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="8c4a4-130">**Address space**: *10.0.0.0/16*</span></span>
    - <span data-ttu-id="8c4a4-131">**서브넷 이름**: *기본값*</span><span class="sxs-lookup"><span data-stu-id="8c4a4-131">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="8c4a4-132">**서브넷 주소 범위**: *10.0.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="8c4a4-132">**Subnet address range**: *10.0.0.0/24*</span></span>
    - <span data-ttu-id="8c4a4-133">**구독**: 사용자의 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-133">**Subscription**: Select your subscription</span></span>
    - <span data-ttu-id="8c4a4-134">**리소스 그룹**: **새로 만들기**를 선택하고 *myResourceGroup*을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-134">**Resource group**: Select **Create new** and enter *myResourceGroup*</span></span>
    - <span data-ttu-id="8c4a4-135">**위치**: *미국 동부*</span><span class="sxs-lookup"><span data-stu-id="8c4a4-135">**Location**: *East US*</span></span>
4. <span data-ttu-id="8c4a4-136">**+새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-136">Click **+ New**.</span></span> <span data-ttu-id="8c4a4-137">Hello에 **검색 hello 마켓플레이스** 상자에서 입력 *가상 네트워크*합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-137">In hello **Search hello Marketplace** box, type *Virtual network*.</span></span> <span data-ttu-id="8c4a4-138">클릭 **가상 네트워크** hello 검색 결과에 표시 되 면입니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-138">Click **Virtual network** when it appears in hello search results.</span></span> 
5. <span data-ttu-id="8c4a4-139">Hello에 **가상 네트워크** 블레이드를 **클래식** hello에 **배포 모델 선택** 상자를 선택한 다음 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-139">In hello **Virtual network** blade, select **Classic** in hello **Select a deployment model** box, and then click **Create**.</span></span>
6. <span data-ttu-id="8c4a4-140">Hello에 **가상 네트워크 만들기** 블레이드에서 입력 하거나 hello 설정, 다음에 대 한 값을 선택한 다음 클릭 **만들기**:</span><span class="sxs-lookup"><span data-stu-id="8c4a4-140">In hello **Create virtual network** blade, enter, or select values for hello following settings, then click **Create**:</span></span>
    - <span data-ttu-id="8c4a4-141">**이름**: *myVnet2*</span><span class="sxs-lookup"><span data-stu-id="8c4a4-141">**Name**: *myVnet2*</span></span>
    - <span data-ttu-id="8c4a4-142">**주소 공간**: *10.1.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="8c4a4-142">**Address space**: *10.1.0.0/16*</span></span>
    - <span data-ttu-id="8c4a4-143">**서브넷 이름**: *기본값*</span><span class="sxs-lookup"><span data-stu-id="8c4a4-143">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="8c4a4-144">**서브넷 주소 범위**: *10.1.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="8c4a4-144">**Subnet address range**: *10.1.0.0/24*</span></span>
    - <span data-ttu-id="8c4a4-145">**구독**: 사용자의 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-145">**Subscription**: Select your subscription</span></span>
    - <span data-ttu-id="8c4a4-146">**리소스 그룹**: **기존 항목 사용**을 선택하고 *myResourceGroup*을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-146">**Resource group**: Select **Use existing** and select *myResourceGroup*</span></span>
    - <span data-ttu-id="8c4a4-147">**위치**: *미국 동부*</span><span class="sxs-lookup"><span data-stu-id="8c4a4-147">**Location**: *East US*</span></span>
7. <span data-ttu-id="8c4a4-148">Hello에 **리소스 검색** 형식 hello 포털의 hello 상단 상자 *myResourceGroup*합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-148">In hello **Search resources** box at hello top of hello portal, type *myResourceGroup*.</span></span> <span data-ttu-id="8c4a4-149">클릭 **myResourceGroup** hello 검색 결과에 표시 되 면입니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-149">Click **myResourceGroup** when it appears in hello search results.</span></span> <span data-ttu-id="8c4a4-150">블레이드 hello에 대 한 표시 **myresourcegroup** 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-150">A blade appears for hello **myresourcegroup** resource group.</span></span> <span data-ttu-id="8c4a4-151">hello 리소스 그룹 이전 단계에서 만든 hello 두 가상 네트워크를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-151">hello resource group contains hello two virtual networks created in previous steps.</span></span>
8. <span data-ttu-id="8c4a4-152">**myVNet1**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-152">Click **myVNet1**.</span></span>
9. <span data-ttu-id="8c4a4-153">Hello에 **myVnet1** 블레이드를 놓고 클릭 **피어 링** hello 세로 hello hello 블레이드의 왼쪽에 옵션 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-153">In hello **myVnet1** blade that appears, click **Peerings** from hello vertical list of options on hello left side of hello blade.</span></span>
10. <span data-ttu-id="8c4a4-154">Hello에 **myVnet1-피어 링** 나타나면 블레이드 클릭 **+ 추가**</span><span class="sxs-lookup"><span data-stu-id="8c4a4-154">In hello **myVnet1 - Peerings** blade that appeared, click **+ Add**</span></span>
11. <span data-ttu-id="8c4a4-155">Hello에 **추가 피어 링** 나타나는 블레이드를 입력 하거나 hello 다음 옵션을 선택한 다음 클릭 **확인**:</span><span class="sxs-lookup"><span data-stu-id="8c4a4-155">In hello **Add peering** blade that appears, enter, or select hello following options, then click **OK**:</span></span>
     - <span data-ttu-id="8c4a4-156">**이름**: *myVnet1ToMyVnet2*</span><span class="sxs-lookup"><span data-stu-id="8c4a4-156">**Name**: *myVnet1ToMyVnet2*</span></span>
     - <span data-ttu-id="8c4a4-157">**가상 네트워크 배포 모델**: **클래식**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-157">**Virtual network deployment model**:  Select **Classic**.</span></span> 
     - <span data-ttu-id="8c4a4-158">**구독**: 사용자의 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-158">**Subscription**: Select your subscription</span></span>
     - <span data-ttu-id="8c4a4-159">**가상 네트워크**: **가상 네트워크 선택**을 클릭한 다음 **myVnet2**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-159">**Virtual network**:  Click **Choose a virtual network**, then click **myVnet2**.</span></span>
     - <span data-ttu-id="8c4a4-160">**가상 네트워크 액세스 허용:** **사용**이 선택되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-160">**Allow virtual network access:** Ensure that **Enabled** is selected.</span></span>
    <span data-ttu-id="8c4a4-161">이 자습서에서 다른 설정은 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-161">No other settings are used in this tutorial.</span></span> <span data-ttu-id="8c4a4-162">모든 피어 링 설정에 대 한 toolearn 읽을 [관리 가상 네트워크 피어 링](virtual-network-manage-peering.md#create-a-peering)합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-162">toolearn about all peering settings, read [Manage virtual network peerings](virtual-network-manage-peering.md#create-a-peering).</span></span>
12. <span data-ttu-id="8c4a4-163">클릭 한 후 **확인** hello 이전 단계에서 hello **추가 피어 링** 블레이드를 닫고 hello 참조 **myVnet1-피어 링** 블레이드를 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-163">After clicking **OK** in hello previous step, hello **Add peering** blade closes and you see hello **myVnet1 - Peerings** blade again.</span></span> <span data-ttu-id="8c4a4-164">몇 초 후 사용자가 만든 피어 링 hello hello 블레이드에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-164">After a few seconds, hello peering you created appears in hello blade.</span></span> <span data-ttu-id="8c4a4-165">**연결** hello에 나열 된 **피어 링 상태** hello에 대 한 열 **myVnet1ToMyVnet2** 만든 피어 링 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-165">**Connected** is listed in hello **PEERING STATUS** column for hello **myVnet1ToMyVnet2** peering you created.</span></span>

    <span data-ttu-id="8c4a4-166">hello 피어 링 이제 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-166">hello peering is now established.</span></span> <span data-ttu-id="8c4a4-167">가상 네트워크 중 하나에서 만드는 모든 Azure 리소스의 IP 주소를 통해 서로 수 toocommunicate 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-167">Any Azure resources you create in either virtual network are now able toocommunicate with each other through their IP addresses.</span></span> <span data-ttu-id="8c4a4-168">Hello 가상 네트워크에 대 한 기본 Azure 이름 확인을 사용 중인 경우 hello hello 가상 네트워크의 리소스가 하지 수 tooresolve 이름을 hello 가상 네트워크를 통해입니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-168">If you're using default Azure name resolution for hello virtual networks, hello resources in hello virtual networks are not able tooresolve names across hello virtual networks.</span></span> <span data-ttu-id="8c4a4-169">피어 링의 가상 네트워크에서 tooresolve 이름을 하려는 경우 자체 DNS 서버를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-169">If you want tooresolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="8c4a4-170">자세한 방법을를 tooset [자체 DNS 서버를 사용 하 여 이름 확인](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-170">Learn how tooset up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>
13. <span data-ttu-id="8c4a4-171">**선택적**: 가상 컴퓨터를 만들어이 자습서에서 다루지 않습니다, 경우에 각 가상 네트워크에서 가상 컴퓨터를 만들 하 고 기타, 하나의 가상 컴퓨터 toohello toovalidate 연결에서에서 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-171">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
14. <span data-ttu-id="8c4a4-172">**선택적**:이 자습서에서 만드는 toodelete hello 리소스 hello에서 단계를 완료 hello [리소스를 삭제](#delete-portal) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-172">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in hello [Delete resources](#delete-portal) section of this article.</span></span>

## <span data-ttu-id="8c4a4-173"><a name="cli"></a>피어링 만들기 - Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8c4a4-173"><a name="cli"></a>Create peering - Azure CLI</span></span>

1. <span data-ttu-id="8c4a4-174">[설치](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello Azure CLI 1.0 toocreate hello 가상 네트워크 (클래식).</span><span class="sxs-lookup"><span data-stu-id="8c4a4-174">[Install](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello Azure CLI 1.0 toocreate hello virtual network (classic).</span></span>
2. <span data-ttu-id="8c4a4-175">명령 세션을 열고 tooAzure hello를 사용 하 여 로그인 `azure login` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-175">Open a command session and log in tooAzure using hello `azure login` command.</span></span>
3. <span data-ttu-id="8c4a4-176">Hello를 입력 하 여 hello CLI 서비스 관리 모드에서 실행 `azure config mode asm` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-176">Run hello CLI in Service Management mode by entering hello `azure config mode asm` command.</span></span>
4. <span data-ttu-id="8c4a4-177">Hello 다음 toocreate hello 가상 네트워크 (클래식) 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-177">Enter hello following command toocreate hello virtual network (classic):</span></span>
 
    ```azurecli
    azure network vnet create --vnet myVnet2 --address-space 10.1.0.0 --cidr 16 --location "East US"
    ```

5. <span data-ttu-id="8c4a4-178">리소스 그룹 및 가상 네트워크(리소스 관리자)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-178">Create a resource group and a virtual network (Resource Manager).</span></span> <span data-ttu-id="8c4a4-179">Hello CLI 1.0 또는 2.0을 사용할 수 있습니다 ([설치](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="8c4a4-179">You can use either hello CLI 1.0 or 2.0 ([install](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)).</span></span> <span data-ttu-id="8c4a4-180">이 자습서에서는 hello CLI 2.0는 2.0을 사용 하는 toocreate hello 피어 링 되어야 하므로 사용 되는 toocreate hello 가상 네트워크 (리소스 관리자)입니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-180">In this tutorial, hello CLI 2.0 is used toocreate hello virtual network (Resource Manager), since 2.0 must be used toocreate hello peering.</span></span> <span data-ttu-id="8c4a4-181">Hello 다음 CLI 2.0.4 hello로 로컬 컴퓨터에서 CLI 스크립트를 이용한 적 또는 이상이 설치 되어 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-181">Execute hello following bash CLI script from your local machine with hello CLI 2.0.4 or later installed.</span></span> <span data-ttu-id="8c4a4-182">옵션 실행 중에 Windows 클라이언트에서 CLI 스크립트를 이용한 적, 참조 [hello Azure CLI Windows에서 실행 중인](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-182">For options on running bash CLI scripts on Windows client, see [Running hello Azure CLI in Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="8c4a4-183">Azure 클라우드 셸 hello를 사용 하 여 hello 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-183">You can also run hello script using hello Azure Cloud Shell.</span></span> <span data-ttu-id="8c4a4-184">Azure 클라우드 셸 hello hello Azure 포털 내에서 직접 실행할 수 있는 무료 Bash 셸의입니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-184">hello Azure Cloud Shell is a free Bash shell that you can run directly within hello Azure portal.</span></span> <span data-ttu-id="8c4a4-185">Hello Azure CLI 사전 설치 및 toouse 사용자 계정으로 구성 된이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-185">It has hello Azure CLI preinstalled and configured toouse with your account.</span></span> <span data-ttu-id="8c4a4-186">Hello 클릭 **실습** 된 Azure 계정 로그는 클라우드 셸을 호출 하는 다음과 같이 tooyour 로그인 할 수 있는 hello 스크립트에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-186">Click hello **Try it** button in hello script that follows, which invokes a Cloud Shell that logs you can log in tooyour Azure account with.</span></span> <span data-ttu-id="8c4a4-187">tooexecute 스크립트 hello를 hello 클릭 **복사** 단추 및 붙여넣기, 클라우드 셸에 hello 내용 누릅니다 `Enter`합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-187">tooexecute hello script, click hello **Copy** button and paste, hello contents into your Cloud Shell, then press `Enter`.</span></span>

    ```azurecli-interactive
    #!/bin/bash

    # Create a resource group.
    az group create \
      --name myResourceGroup \
      --location eastus

    # Create hello virtual network (Resource Manager).
    az network vnet create \
      --name myVnet1 \
      --resource-group myResourceGroup \
      --location eastus \
      --address-prefix 10.0.0.0/16
    ```

6. <span data-ttu-id="8c4a4-188">Hello 다양 한 배포 모델을 통해 만든 hello 두 가상 네트워크 간의 피어 링 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-188">Create a virtual network peering between hello two virtual networks created through hello different deployment models.</span></span> <span data-ttu-id="8c4a4-189">Hello 나오는 스크립트 tooa 텍스트 편집기를 사용자 PC에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-189">Copy hello following script tooa text editor on your PC.</span></span> <span data-ttu-id="8c4a4-190">`<subscription id>`는 구독 ID로 바꿉니다. 구독 Id를 모르는 경우 입력 hello `az account show` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-190">Replace `<subscription id>` with your subscription Id. If you don't know your subscription Id, enter hello `az account show` command.</span></span> <span data-ttu-id="8c4a4-191">값에 대 한 hello **id** hello 출력은 구독 id입니다. Tooyour CLI 세션에서 수정 하는 hello 스크립트를 붙여 넣고 다음 키를 누릅니다 `Enter`합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-191">hello value for **id** in hello output is your subscription Id. Paste hello modified script in tooyour CLI session, and then press `Enter`.</span></span>

    ```azurecli-interactive
    # Get hello id for VNet1.
    vnet1Id=$(az network vnet show \
      --resource-group myResourceGroup \
      --name myVnet1 \
      --query id --out tsv)

    # Peer VNet1 tooVNet2.
    az network vnet peering create \
      --name myVnet1ToMyVnet2 \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --remote-vnet-id /subscriptions/<subscription id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnet2 \
      --allow-vnet-access
    ```
7. <span data-ttu-id="8c4a4-192">Hello 스크립트를 실행 한 후에 hello 가상 네트워크 (리소스 관리자)에 대 한 피어 링 hello를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-192">After hello script executes, review hello peering for hello virtual network (Resource Manager).</span></span> <span data-ttu-id="8c4a4-193">복사 hello 다음 명령 CLI 세션에 붙여 넣고 다음 키를 누릅니다 `Enter`:</span><span class="sxs-lookup"><span data-stu-id="8c4a4-193">Copy hello following command, paste it in your CLI session, and then press `Enter`:</span></span>

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --output table
    ```
    
    <span data-ttu-id="8c4a4-194">hello 출력 있는지 보여 줍니다 **연결 됨** hello에 **PeeringState** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-194">hello output shows **Connected** in hello **PeeringState** column.</span></span> 

    <span data-ttu-id="8c4a4-195">가상 네트워크 중 하나에서 만드는 모든 Azure 리소스의 IP 주소를 통해 서로 수 toocommunicate 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-195">Any Azure resources you create in either virtual network are now able toocommunicate with each other through their IP addresses.</span></span> <span data-ttu-id="8c4a4-196">Hello 가상 네트워크에 대 한 기본 Azure 이름 확인을 사용 중인 경우 hello hello 가상 네트워크의 리소스가 하지 수 tooresolve 이름을 hello 가상 네트워크를 통해입니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-196">If you're using default Azure name resolution for hello virtual networks, hello resources in hello virtual networks are not able tooresolve names across hello virtual networks.</span></span> <span data-ttu-id="8c4a4-197">피어 링의 가상 네트워크에서 tooresolve 이름을 하려는 경우 자체 DNS 서버를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-197">If you want tooresolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="8c4a4-198">자세한 방법을를 tooset [자체 DNS 서버를 사용 하 여 이름 확인](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-198">Learn how tooset up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>
8. <span data-ttu-id="8c4a4-199">**선택적**: 가상 컴퓨터를 만들어이 자습서에서 다루지 않습니다, 경우에 각 가상 네트워크에서 가상 컴퓨터를 만들 하 고 기타, 하나의 가상 컴퓨터 toohello toovalidate 연결에서에서 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-199">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
9. <span data-ttu-id="8c4a4-200">**선택적**:이 자습서에서 만드는 toodelete hello 리소스의 단계를 완료 hello [리소스를 삭제](#delete-cli) 이 문서의 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-200">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in [Delete resources](#delete-cli) in this article.</span></span>

## <span data-ttu-id="8c4a4-201"><a name="powershell"></a>피어링 만들기 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c4a4-201"><a name="powershell"></a>Create peering - PowerShell</span></span>

1. <span data-ttu-id="8c4a4-202">Hello hello PowerShell의 최신 버전을 설치 [Azure](https://www.powershellgallery.com/packages/Azure) 및 [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-202">Install hello latest version of hello PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) and [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modules.</span></span> <span data-ttu-id="8c4a4-203">새 tooAzure PowerShell 인 경우 참조 [Azure PowerShell 개요](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-203">If you're new tooAzure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="8c4a4-204">PowerShell 세션을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-204">Start a PowerShell session.</span></span>
3. <span data-ttu-id="8c4a4-205">PowerShell에서 로그인 tooAzure hello를 입력 하 여 `Add-AzureAccount` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-205">In PowerShell, log in tooAzure by entering hello `Add-AzureAccount` command.</span></span>
4. <span data-ttu-id="8c4a4-206">PowerShell 사용 하 여 가상 네트워크 (클래식) toocreate 있습니다 새로 만들거나 수정 해야는 기존 네트워크 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-206">toocreate a virtual network (classic) with PowerShell, you must create a new, or modify an existing, network configuration file.</span></span> <span data-ttu-id="8c4a4-207">너무 방법에 대해 알아봅니다[내보내기, 업데이트 및 네트워크 구성 파일을 가져올](virtual-networks-using-network-configuration-file.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-207">Learn how too[export, update, and import network configuration files](virtual-networks-using-network-configuration-file.md).</span></span> <span data-ttu-id="8c4a4-208">hello 파일에 포함할지 hello 다음 **VirtualNetworkSite** 이 자습서에 사용 된 hello 가상 네트워크에 대 한 요소:</span><span class="sxs-lookup"><span data-stu-id="8c4a4-208">hello file should include hello following **VirtualNetworkSite** element for hello virtual network used in this tutorial:</span></span>

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
    > <span data-ttu-id="8c4a4-209">변경 된 네트워크 구성 파일을 가져오는 변경 될 수 tooexisting 가상 네트워크 (클래식)를 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-209">Importing a changed network configuration file can cause changes tooexisting virtual networks (classic) in your subscription.</span></span> <span data-ttu-id="8c4a4-210">만 hello 이전 가상 네트워크를 추가 하 고 변경 하거나 구독에서 기존 가상 네트워크를 제거 하지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-210">Ensure you only add hello previous virtual network and that you don't change or remove any existing virtual networks from your subscription.</span></span> 
5. <span data-ttu-id="8c4a4-211">Hello를 입력 하 여 tooAzure toocreate hello 가상 네트워크 (리소스 관리자)에 로그인 `login-azurermaccount` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-211">Log in tooAzure toocreate hello virtual network (Resource Manager) by entering hello `login-azurermaccount` command.</span></span> <span data-ttu-id="8c4a4-212">가상 네트워크 피어 링 hello 필요한 권한을 toocreate 사용 하 여 로그인 하는 hello 계정에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-212">hello account you log in with must have hello necessary permissions toocreate a virtual network peering.</span></span> <span data-ttu-id="8c4a4-213">Hello 참조 [권한을](#permissions) 대 한 자세한 내용은이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-213">See hello [Permissions](#permissions) section of this article for details.</span></span>
6. <span data-ttu-id="8c4a4-214">리소스 그룹 및 가상 네트워크(리소스 관리자)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-214">Create a resource group and a virtual network (Resource Manager).</span></span> <span data-ttu-id="8c4a4-215">Hello 스크립트 복사 PowerShell에 붙여 넣고 다음 키를 누릅니다 `Enter`합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-215">Copy hello script, paste it into PowerShell, and then press `Enter`.</span></span>

    ```powershell
    # Create a resource group.
      New-AzureRmResourceGroup -Name myResourceGroup -Location eastus

    # Create hello virtual network (Resource Manager).
      $vnet1 = New-AzureRmVirtualNetwork `
      -ResourceGroupName myResourceGroup `
      -Name 'myVnet1' `
      -AddressPrefix '10.0.0.0/16' `
      -Location eastus
    ```

7. <span data-ttu-id="8c4a4-216">Hello 다양 한 배포 모델을 통해 만든 hello 두 가상 네트워크 간의 피어 링 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-216">Create a virtual network peering between hello two virtual networks created through hello different deployment models.</span></span> <span data-ttu-id="8c4a4-217">Hello 나오는 스크립트 tooa 텍스트 편집기를 사용자 PC에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-217">Copy hello following script tooa text editor on your PC.</span></span> <span data-ttu-id="8c4a4-218">`<subscription id>`는 구독 ID로 바꿉니다. 구독 Id를 모르는 경우 입력 hello `Get-AzureRmSubscription` 명령 tooview 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-218">Replace `<subscription id>` with your subscription Id. If you don't know your subscription Id, enter hello `Get-AzureRmSubscription` command tooview it.</span></span> <span data-ttu-id="8c4a4-219">값에 대 한 hello **Id** hello 반환 출력은 프로그램 구독 id입니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-219">hello value for **Id** in hello returned output is your subscription ID.</span></span> <span data-ttu-id="8c4a4-220">tooexecute hello 스크립트 복사 hello 수정 된 스크립트를 텍스트 편집기에서 PowerShell 세션에서 마우스 오른쪽 단추로 클릭 하 고 다음 키를 누릅니다 `Enter`합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-220">tooexecute hello script, copy hello modified script from your text editor, then right-click in your PowerShell session, and then press `Enter`.</span></span>

    ```powershell
    # Peer VNet1 tooVNet2.
    Add-AzureRmVirtualNetworkPeering `
      -Name myVnet1ToMyVnet2 `
      -VirtualNetwork $vnet1 `
      -RemoteVirtualNetworkId /subscriptions/<subscription Id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnet2
    ```

8. <span data-ttu-id="8c4a4-221">Hello 스크립트를 실행 한 후에 hello 가상 네트워크 (리소스 관리자)에 대 한 피어 링 hello를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-221">After hello script executes, review hello peering for hello virtual network (Resource Manager).</span></span> <span data-ttu-id="8c4a4-222">복사 hello 다음 명령 PowerShell 세션에 붙여 넣고 다음 키를 누릅니다 `Enter`:</span><span class="sxs-lookup"><span data-stu-id="8c4a4-222">Copy hello following command, paste it in your PowerShell session, and then press `Enter`:</span></span>

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroup `
      -VirtualNetworkName myVnet1 `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    <span data-ttu-id="8c4a4-223">hello 출력 있는지 보여 줍니다 **연결 됨** hello에 **PeeringState** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-223">hello output shows **Connected** in hello **PeeringState** column.</span></span>

    <span data-ttu-id="8c4a4-224">가상 네트워크 중 하나에서 만드는 모든 Azure 리소스의 IP 주소를 통해 서로 수 toocommunicate 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-224">Any Azure resources you create in either virtual network are now able toocommunicate with each other through their IP addresses.</span></span> <span data-ttu-id="8c4a4-225">Hello 가상 네트워크에 대 한 기본 Azure 이름 확인을 사용 중인 경우 hello hello 가상 네트워크의 리소스가 하지 수 tooresolve 이름을 hello 가상 네트워크를 통해입니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-225">If you're using default Azure name resolution for hello virtual networks, hello resources in hello virtual networks are not able tooresolve names across hello virtual networks.</span></span> <span data-ttu-id="8c4a4-226">피어 링의 가상 네트워크에서 tooresolve 이름을 하려는 경우 자체 DNS 서버를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-226">If you want tooresolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="8c4a4-227">자세한 방법을를 tooset [자체 DNS 서버를 사용 하 여 이름 확인](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-227">Learn how tooset up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

9. <span data-ttu-id="8c4a4-228">**선택적**: 가상 컴퓨터를 만들어이 자습서에서 다루지 않습니다, 경우에 각 가상 네트워크에서 가상 컴퓨터를 만들 하 고 기타, 하나의 가상 컴퓨터 toohello toovalidate 연결에서에서 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-228">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
10. <span data-ttu-id="8c4a4-229">**선택적**:이 자습서에서 만드는 toodelete hello 리소스의 단계를 완료 hello [리소스를 삭제](#delete-powershell) 이 문서의 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-229">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in [Delete resources](#delete-powershell) in this article.</span></span>
 
## <span data-ttu-id="8c4a4-230"><a name="permissions"></a>권한</span><span class="sxs-lookup"><span data-stu-id="8c4a4-230"><a name="permissions"></a>Permissions</span></span>

<span data-ttu-id="8c4a4-231">hello 계정 toocreate 가상 네트워크 피어 링을 사용 하 여 hello 필요한 역할 또는 사용 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-231">hello accounts you use toocreate a virtual network peering must have hello necessary role or permissions.</span></span> <span data-ttu-id="8c4a4-232">예를 들어 myVnet1 및 myVnet2 라는 두 개의 가상 네트워크, 피어 링 된 경우 사용자 계정에 할당 해야 최소 역할 또는 각 가상 네트워크에 대 한 사용 권한을 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="8c4a4-232">For example, if you were peering two virtual networks named myVnet1 and myVnet2, your account must be assigned hello following minimum role or permissions for each virtual network:</span></span>
    
|<span data-ttu-id="8c4a4-233">가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="8c4a4-233">Virtual network</span></span>|<span data-ttu-id="8c4a4-234">배포 모델</span><span class="sxs-lookup"><span data-stu-id="8c4a4-234">Deployment model</span></span>|<span data-ttu-id="8c4a4-235">역할</span><span class="sxs-lookup"><span data-stu-id="8c4a4-235">Role</span></span>|<span data-ttu-id="8c4a4-236">권한</span><span class="sxs-lookup"><span data-stu-id="8c4a4-236">Permissions</span></span>|
|---|---|---|---|
|<span data-ttu-id="8c4a4-237">myVnet1</span><span class="sxs-lookup"><span data-stu-id="8c4a4-237">myVnet1</span></span>|<span data-ttu-id="8c4a4-238">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="8c4a4-238">Resource Manager</span></span>|[<span data-ttu-id="8c4a4-239">네트워크 참여자</span><span class="sxs-lookup"><span data-stu-id="8c4a4-239">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="8c4a4-240">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span><span class="sxs-lookup"><span data-stu-id="8c4a4-240">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span></span>|
| |<span data-ttu-id="8c4a4-241">클래식</span><span class="sxs-lookup"><span data-stu-id="8c4a4-241">Classic</span></span>|[<span data-ttu-id="8c4a4-242">클래식 네트워크 참여자</span><span class="sxs-lookup"><span data-stu-id="8c4a4-242">Classic Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|<span data-ttu-id="8c4a4-243">해당 없음</span><span class="sxs-lookup"><span data-stu-id="8c4a4-243">N/A</span></span>|
|<span data-ttu-id="8c4a4-244">myVnet2</span><span class="sxs-lookup"><span data-stu-id="8c4a4-244">myVnet2</span></span>|<span data-ttu-id="8c4a4-245">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="8c4a4-245">Resource Manager</span></span>|[<span data-ttu-id="8c4a4-246">네트워크 참여자</span><span class="sxs-lookup"><span data-stu-id="8c4a4-246">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="8c4a4-247">Microsoft.Network/virtualNetworks/peer</span><span class="sxs-lookup"><span data-stu-id="8c4a4-247">Microsoft.Network/virtualNetworks/peer</span></span>|
||<span data-ttu-id="8c4a4-248">클래식</span><span class="sxs-lookup"><span data-stu-id="8c4a4-248">Classic</span></span>|[<span data-ttu-id="8c4a4-249">클래식 네트워크 참여자</span><span class="sxs-lookup"><span data-stu-id="8c4a4-249">Classic Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|<span data-ttu-id="8c4a4-250">Microsoft.ClassicNetwork/virtualNetworks/peer</span><span class="sxs-lookup"><span data-stu-id="8c4a4-250">Microsoft.ClassicNetwork/virtualNetworks/peer</span></span>|

<span data-ttu-id="8c4a4-251">에 대 한 자세한 내용은 [기본 제공 역할](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) 너무 특정 사용 권한을 할당 하 고[사용자 정의 역할](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (리소스 관리자에만 해당).</span><span class="sxs-lookup"><span data-stu-id="8c4a4-251">Learn more about [built-in roles](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) and assigning specific permissions too[custom roles](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (Resource Manager only).</span></span>

## <span data-ttu-id="8c4a4-252"><a name="delete"></a>리소스 삭제</span><span class="sxs-lookup"><span data-stu-id="8c4a4-252"><a name="delete"></a>Delete resources</span></span>
<span data-ttu-id="8c4a4-253">이 자습서를 마친 toodelete hello 리소스 사용량에 따른 요금을 발생 하지 않습니다 하므로 hello 자습서에서 만든 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-253">When you've finished this tutorial, you might want toodelete hello resources you created in hello tutorial, so you don't incur usage charges.</span></span> <span data-ttu-id="8c4a4-254">리소스 그룹을 삭제 하면 hello 리소스 그룹에는 모든 리소스를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-254">Deleting a resource group also deletes all resources that are in hello resource group.</span></span>

### <span data-ttu-id="8c4a4-255"><a name="delete-portal"></a>Azure Portal</span><span class="sxs-lookup"><span data-stu-id="8c4a4-255"><a name="delete-portal"></a>Azure portal</span></span>

1. <span data-ttu-id="8c4a4-256">Hello 포털 검색 상자에 입력 **myResourceGroup**합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-256">In hello portal search box, enter **myResourceGroup**.</span></span> <span data-ttu-id="8c4a4-257">Hello 검색 결과에서 클릭 **myResourceGroup**합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-257">In hello search results, click **myResourceGroup**.</span></span>
2. <span data-ttu-id="8c4a4-258">Hello에 **myResourceGroup** 블레이드에서 hello 클릭 **삭제** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-258">On hello **myResourceGroup** blade, click hello **Delete** icon.</span></span>
3. <span data-ttu-id="8c4a4-259">hello에 tooconfirm hello 삭제 **형식 hello 리소스 그룹 이름은** 상자에 입력 **myResourceGroup**, 클릭 하 고 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-259">tooconfirm hello deletion, in hello **TYPE hello RESOURCE GROUP NAME** box, enter **myResourceGroup**, and then click **Delete**.</span></span>

### <span data-ttu-id="8c4a4-260"><a name="delete-cli"></a>Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8c4a4-260"><a name="delete-cli"></a>Azure CLI</span></span>

1. <span data-ttu-id="8c4a4-261">다음 명령을 hello로 hello Azure CLI 2.0 toodelete hello 가상 네트워크 (리소스 관리자)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-261">Use hello Azure CLI 2.0 toodelete hello virtual network (Resource Manager) with hello following command:</span></span>

    ```azurecli-interactive
    az group delete --name myResourceGroup --yes
    ```

2. <span data-ttu-id="8c4a4-262">다음 명령은 hello로 hello Azure CLI 1.0 toodelete hello 가상 네트워크 (클래식)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-262">Use hello Azure CLI 1.0 toodelete hello virtual network (classic) with hello following commands:</span></span>

    ```azurecli
    azure config mode asm

    azure network vnet delete --vnet myVnet2 --quiet
    ```

### <span data-ttu-id="8c4a4-263"><a name="delete-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c4a4-263"><a name="delete-powershell"></a>PowerShell</span></span>

1. <span data-ttu-id="8c4a4-264">Hello 다음 toodelete hello 가상 네트워크 (리소스 관리자) 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-264">Enter hello following command toodelete hello virtual network (Resource Manager):</span></span>

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroup -Force
    ```

2. <span data-ttu-id="8c4a4-265">toodelete hello 가상 네트워크 (클래식) PowerShell과 함께 기존 네트워크 구성 파일을 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-265">toodelete hello virtual network (classic) with PowerShell, you must modify an existing network configuration file.</span></span> <span data-ttu-id="8c4a4-266">너무 방법에 대해 알아봅니다[내보내기, 업데이트 및 네트워크 구성 파일을 가져올](virtual-networks-using-network-configuration-file.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-266">Learn how too[export, update, and import network configuration files](virtual-networks-using-network-configuration-file.md).</span></span> <span data-ttu-id="8c4a4-267">이 자습서에 사용 된 hello 가상 네트워크에 대 한 VirtualNetworkSite 요소 다음에 오는 hello를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-267">Remove hello following VirtualNetworkSite element for hello virtual network used in this tutorial:</span></span>

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
    > <span data-ttu-id="8c4a4-268">변경 된 네트워크 구성 파일을 가져오는 변경 될 수 tooexisting 가상 네트워크 (클래식)를 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-268">Importing a changed network configuration file can cause changes tooexisting virtual networks (classic) in your subscription.</span></span> <span data-ttu-id="8c4a4-269">만 hello 이전 가상 네트워크를 제거 하 고 변경 하거나 구독에서 다른 기존 가상 네트워크를 제거 하지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-269">Ensure you only remove hello previous virtual network and that you don't change or remove any other existing virtual networks from your subscription.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8c4a4-270">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8c4a4-270">Next steps</span></span>

- <span data-ttu-id="8c4a4-271">프로덕션 환경에 사용하기 위한 가상 네트워크 피어링을 만들기 전에 먼저 중요한 [가상 네트워크 피어링 제약 조건 및 동작](virtual-network-manage-peering.md#requirements-and-constraints)에 철저하게 익숙해집니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-271">Thoroughly familiarize yourself with important [virtual network peering constraints and behaviors](virtual-network-manage-peering.md#requirements-and-constraints) before creating a virtual network peering for production use.</span></span>
- <span data-ttu-id="8c4a4-272">모든 [가상 네트워크 피어링 설정](virtual-network-manage-peering.md#create-a-peering)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-272">Learn about all [virtual network peering settings](virtual-network-manage-peering.md#create-a-peering).</span></span>
- <span data-ttu-id="8c4a4-273">너무 방법에 대해 알아봅니다[허브를 만들고 네트워크 토폴로지 스포크](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) 가상 네트워크 피어 링을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a4-273">Learn how too[create a hub and spoke network topology](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) with virtual network peering.</span></span>
