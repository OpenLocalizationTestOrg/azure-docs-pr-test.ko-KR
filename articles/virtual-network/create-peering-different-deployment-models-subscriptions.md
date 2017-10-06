---
title: "aaaCreate는 Azure 가상 네트워크 피어 링-다양 한 배포 모델-서로 다른 구독 | Microsoft Docs"
description: "Toocreate 가상 네트워크 간의 피어 링 가상 네트워크를 만드는 방법을 각기 다른 Azure 구독에 있는 다른 Azure 배포 모델을 통해에 대해 알아봅니다."
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
ms.openlocfilehash: 865bdabb5b87523ba943d7b5dcbdc2475b78bdb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---different-deployment-models-and-subscriptions"></a><span data-ttu-id="b728d-103">가상 네트워크 피어링 만들기 - 서로 다른 배포 모델 및 구독</span><span class="sxs-lookup"><span data-stu-id="b728d-103">Create a virtual network peering - different deployment models and subscriptions</span></span>

<span data-ttu-id="b728d-104">이 자습서에서는 toocreate 다양 한 배포 모델을 통해 만든 가상 네트워크 간의 피어 링 하는 가상 네트워크를 학습 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-104">In this tutorial, you learn toocreate a virtual network peering between virtual networks created through different deployment models.</span></span> <span data-ttu-id="b728d-105">hello 가상 네트워크는 서로 다른 구독에 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-105">hello virtual networks exist in different subscriptions.</span></span> <span data-ttu-id="b728d-106">Hello에 hello 리소스 것 처럼 동일한 대역폭 및 대기 시간으로 서로 toocommunicate 서로 다른 가상 네트워크의에서 피어 링 두 가상 네트워크 사용 리소스 hello 동일한 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-106">Peering two virtual networks enables resources in different virtual networks toocommunicate with each other with hello same bandwidth and latency as though hello resources were in hello same virtual network.</span></span> <span data-ttu-id="b728d-107">[가상 네트워크 피어링](virtual-network-peering-overview.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="b728d-107">Learn more about [Virtual network peering](virtual-network-peering-overview.md).</span></span> 

<span data-ttu-id="b728d-108">hello 단계 toocreate 피어 링 가상 네트워크는 hello 가상 네트워크는 hello 같거나 다른 데이터 집합, 구독 및 있는에 있는지 여부에 따라 다른 [Azure 배포 모델](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello 가상 네트워크가 만들어집니다. 통해</span><span class="sxs-lookup"><span data-stu-id="b728d-108">hello steps toocreate a virtual network peering are different, depending on whether hello virtual networks are in hello same, or different, subscriptions, and which [Azure deployment model](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello virtual networks are created through.</span></span> <span data-ttu-id="b728d-109">가상 a toocreate 네트워크 hello 시나리오 hello 다음 표를에서 클릭 하 여 다른 시나리오에서는 피어 링 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-109">Learn how toocreate a virtual network peering in other scenarios by clicking hello scenario from hello following table:</span></span>

|<span data-ttu-id="b728d-110">Azure 배포 모델</span><span class="sxs-lookup"><span data-stu-id="b728d-110">Azure deployment model</span></span>  | <span data-ttu-id="b728d-111">Azure 구독</span><span class="sxs-lookup"><span data-stu-id="b728d-111">Azure subscription</span></span>  |
|--------- |---------|
|[<span data-ttu-id="b728d-112">둘 다 리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="b728d-112">Both Resource Manager</span></span>](virtual-network-create-peering.md) |<span data-ttu-id="b728d-113">동일</span><span class="sxs-lookup"><span data-stu-id="b728d-113">Same</span></span>|
|[<span data-ttu-id="b728d-114">둘 다 리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="b728d-114">Both Resource Manager</span></span>](create-peering-different-subscriptions.md) |<span data-ttu-id="b728d-115">다름</span><span class="sxs-lookup"><span data-stu-id="b728d-115">Different</span></span>|
|[<span data-ttu-id="b728d-116">하나는 Resource Manager, 하나는 클래식</span><span class="sxs-lookup"><span data-stu-id="b728d-116">One Resource Manager, one classic</span></span>](create-peering-different-deployment-models.md) |<span data-ttu-id="b728d-117">동일</span><span class="sxs-lookup"><span data-stu-id="b728d-117">Same</span></span>|

<span data-ttu-id="b728d-118">Hello 클래식 배포 모델을 통해 배포 된 두 개의 가상 네트워크 간의 피어 링 가상 네트워크를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-118">A virtual network peering cannot be created between two virtual networks deployed through hello classic deployment model.</span></span> <span data-ttu-id="b728d-119">동일한 hello에 존재 하는 두 개의 가상 네트워크 간에 만들 수는 가상 네트워크 피어 링 Azure 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-119">A virtual network peering can only be created between two virtual networks that exist in hello same Azure region.</span></span> <span data-ttu-id="b728d-120">Toohello 연결 된 다른 구독을 구독은 둘 다 hello에 존재 하는 가상 네트워크 간의 피어 링 가상 네트워크를 만들 때 동일한 Azure Active Directory 테 넌 트.</span><span class="sxs-lookup"><span data-stu-id="b728d-120">When creating a virtual network peering between virtual networks that exist in different subscriptions, hello subscriptions must both be associated toohello same Azure Active Directory tenant.</span></span> <span data-ttu-id="b728d-121">아직 Azure Active Directory 테넌트가 없는 경우 신속히 하나 [만들](../active-directory/develop/active-directory-howto-tenant.md?toc=%2fazure%2fvirtual-network%2ftoc.json#start-from-scratch) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-121">If you don't already have an Azure Active Directory tenant, you can quickly [create one](../active-directory/develop/active-directory-howto-tenant.md?toc=%2fazure%2fvirtual-network%2ftoc.json#start-from-scratch).</span></span> <span data-ttu-id="b728d-122">hello 클래식 배포 모델을 통해 생성 된 또는 서로 다른 Azure 지역에 있는 또는 구독에 속해 있는 네트워크 연결 toodifferent Azure Active Directory 테 넌 트를 Azure를사용할수있습니다tooconnect가상필요한경우[VPN 게이트웨이](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-122">If you need tooconnect virtual networks that were both created through hello classic deployment model, or that exist in different Azure regions, or that exist in subscriptions associated toodifferent Azure Active Directory tenants, you can use an Azure [VPN Gateway](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello virtual networks.</span></span> 

> [!WARNING]
> <span data-ttu-id="b728d-123">서로 다른 Azure 구독에 존재하는 동서로 다른 Azure 배포 모델을 통해 만든 가상 네트워크 간의 가상 네트워크 피어링을 만드는 것은 현재 미리 보기 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-123">Creating a virtual network peering between virtual networks in created through different Azure deployment models that exist in different subscriptions is currently in preview.</span></span> <span data-ttu-id="b728d-124">이 시나리오에서 만든 가상 네트워크 피어 링 없을 수 있습니다 가능성 및 안정성이 피어 링 시나리오에서 일반적 공급 릴리스 가상 네트워크를 만드는 것과 동일한 수준의 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-124">Virtual network peerings created in this scenario may not have hello same level of availability and reliability as creating a virtual network peering in scenarios in general availability release.</span></span> <span data-ttu-id="b728d-125">이 시나리오에서 만든 가상 네트워크 피어링은 지원되지 않으며, 기능상의 제약이 있거나, 일부 Azure 지역에서 사용하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-125">Virtual network peerings created in this scenario are not supported, may have constrained capabilities, and may not be available in all Azure regions.</span></span> <span data-ttu-id="b728d-126">에 대 한 hello 최신 알림을 가능 여부와이 기능의 상태를 확인 hello [Azure 가상 네트워크를 업데이트](https://azure.microsoft.com/updates/?product=virtual-network) 페이지.</span><span class="sxs-lookup"><span data-stu-id="b728d-126">For hello most up-to-date notifications on availability and status of this feature, check hello [Azure Virtual Network updates](https://azure.microsoft.com/updates/?product=virtual-network) page.</span></span>

<span data-ttu-id="b728d-127">Hello를 사용할 수 있습니다 [Azure 포털](#portal), Azure hello [명령줄 인터페이스](#cli) (CLI) 또는 Azure [PowerShell](#powershell) toocreate 가상 네트워크 피어 링입니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-127">You can use hello [Azure portal](#portal), hello Azure [command-line interface](#cli) (CLI), or Azure [PowerShell](#powershell) toocreate a virtual network peering.</span></span> <span data-ttu-id="b728d-128">Toohello 원하는 도구를 사용 하 여 가상 네트워크 피어 링을 만들기 위한 단계를 직접 hello 이전 도구 링크 toogo 중 하나를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-128">Click any of hello previous tool links toogo directly toohello steps for creating a virtual network peering using your tool of choice.</span></span>

## <span data-ttu-id="b728d-129"><a name="register"></a>Hello 미리 보기에 대 한 등록</span><span class="sxs-lookup"><span data-stu-id="b728d-129"><a name="register"></a>Register for hello preview</span></span>

<span data-ttu-id="b728d-130">hello 미리 보기에 대 한 tooregister, hello 가상 네트워크를 포함 하는 두 구독에 대해 수행 하는 전체 hello 단계 toopeer를 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-130">tooregister for hello preview, complete hello steps that follow for both subscriptions that contain hello virtual networks you want toopeer.</span></span> <span data-ttu-id="b728d-131">hello만 도구 tooregister를 사용 하 여 hello 미리 보기에는 PowerShell입니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-131">hello only tool you can use tooregister for hello preview is PowerShell.</span></span>

1. <span data-ttu-id="b728d-132">Hello hello PowerShell의 최신 버전을 설치 [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-132">Install hello latest version of hello PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="b728d-133">새 tooAzure PowerShell 인 경우 참조 [Azure PowerShell 개요](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-133">If you're new tooAzure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="b728d-134">PowerShell 세션을 시작 하 고 tooAzure hello를 사용 하 여 로그인 `login-azurermaccount` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-134">Start a PowerShell session and log in tooAzure using hello `login-azurermaccount` command.</span></span>
3. <span data-ttu-id="b728d-135">Hello 다음 명령을 입력 하 여 hello 미리 보기에 대 한 구독을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-135">Register your subscription for hello preview by entering hello following commands:</span></span>

    ```powershell
    Register-AzureRmProviderFeature `
      -FeatureName AllowClassicCrossSubscriptionPeering `
      -ProviderNamespace Microsoft.Network
    
    Register-AzureRmResourceProvider `
      -ProviderNamespace Microsoft.Network
    ```
    <span data-ttu-id="b728d-136">Hello 될 때까지이 문서의 hello 포털, Azure CLI 또는 PowerShell 섹션의 hello 단계를 완료 하지 않으면 **RegistrationState** 는 hello 다음 명령을 입력 한 후 수신 출력 **등록 된** 대 한 두 구독:</span><span class="sxs-lookup"><span data-stu-id="b728d-136">Do not complete hello steps in hello Portal, Azure CLI, or PowerShell sections of this article until hello **RegistrationState** output you receive after entering hello following command is **Registered** for both subscriptions:</span></span>

    ```powershell    
    Get-AzureRmProviderFeature `
      -FeatureName AllowClassicCrossSubscriptionPeering `
      -ProviderNamespace Microsoft.Network
    ```

## <span data-ttu-id="b728d-137"><a name="portal"></a>피어링 만들기 - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b728d-137"><a name="portal"></a>Create peering - Azure portal</span></span>

<span data-ttu-id="b728d-138">이 자습서에서는 각 구독에 대해 다른 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-138">This tutorial uses different accounts for each subscription.</span></span> <span data-ttu-id="b728d-139">Tooboth 구독 사용 권한을 가진 계정으로를 사용 하는 모든 단계에 대 한 계정 동일한에서 로그 아웃 hello 포털에 대 한 hello 단계를 건너뛰고 항목과 toohello 가상 네트워크 사용 권한을 다른 사용자를 할당 하기 위한 hello 단계를 건너뛸 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-139">If you're using an account that has permissions tooboth subscriptions, you can use hello same account for all steps, skip hello steps for logging out of hello portal, and skip hello steps for assigning another user permissions toohello virtual networks.</span></span> <span data-ttu-id="b728d-140">Hello 다음 단계를 완료 하기 전에 hello 미리 보기에 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-140">Before completing any of hello following steps, you must register for hello preview.</span></span> <span data-ttu-id="b728d-141">tooregister, hello에서 단계를 완료 하는 hello [hello 미리 보기를 등록할](#register) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="b728d-141">tooregister, complete hello steps in hello [Register for hello preview](#register) section of this article.</span></span> <span data-ttu-id="b728d-142">두 구독 hello 미리 보기에 등록 될 때까지 단계를 남은 hello로 계속 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="b728d-142">Do not continue with hello remaining steps until both subscriptions are registered for hello preview.</span></span>
 
1. <span data-ttu-id="b728d-143">Toohello 로그인 [Azure 포털](https://portal.azure.com) UserA로 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-143">Log in toohello [Azure portal](https://portal.azure.com) as UserA.</span></span> <span data-ttu-id="b728d-144">가상 네트워크 피어 링 hello 필요한 권한을 toocreate 사용 하 여 로그인 하는 hello 계정에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-144">hello account you log in with must have hello necessary permissions toocreate a virtual network peering.</span></span> <span data-ttu-id="b728d-145">Hello 참조 [권한을](#permissions) 대 한 자세한 내용은이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="b728d-145">See hello [Permissions](#permissions) section of this article for details.</span></span>
2. <span data-ttu-id="b728d-146">**+ 새로 만들기**, **네트워킹**, **가상 네트워크**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-146">Click **+ New**, click **Networking**, then click **Virtual network**.</span></span>
3. <span data-ttu-id="b728d-147">Hello에 **가상 네트워크 만들기** 블레이드에서 입력 하거나 hello 설정, 다음에 대 한 값을 선택한 다음 클릭 **만들기**:</span><span class="sxs-lookup"><span data-stu-id="b728d-147">In hello **Create virtual network** blade, enter, or select values for hello following settings, then click **Create**:</span></span>
    - <span data-ttu-id="b728d-148">**이름**: *myVnetA*</span><span class="sxs-lookup"><span data-stu-id="b728d-148">**Name**: *myVnetA*</span></span>
    - <span data-ttu-id="b728d-149">**주소 공간**: *10.0.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="b728d-149">**Address space**: *10.0.0.0/16*</span></span>
    - <span data-ttu-id="b728d-150">**서브넷 이름**: *기본값*</span><span class="sxs-lookup"><span data-stu-id="b728d-150">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="b728d-151">**서브넷 주소 범위**: *10.0.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="b728d-151">**Subnet address range**: *10.0.0.0/24*</span></span>
    - <span data-ttu-id="b728d-152">**구독**: 구독 A를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-152">**Subscription**: Select subscription A.</span></span>
    - <span data-ttu-id="b728d-153">**리소스 그룹**: **새로 만들기**를 선택하고 *myResourceGroupA*를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-153">**Resource group**: Select **Create new** and enter *myResourceGroupA*</span></span>
    - <span data-ttu-id="b728d-154">**위치**: *미국 동부*</span><span class="sxs-lookup"><span data-stu-id="b728d-154">**Location**: *East US*</span></span>
4. <span data-ttu-id="b728d-155">Hello에 **리소스 검색** 형식 hello 포털의 hello 상단 상자 *myVnetA*합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-155">In hello **Search resources** box at hello top of hello portal, type *myVnetA*.</span></span> <span data-ttu-id="b728d-156">클릭 **myVnetA** hello 검색 결과에 표시 되 면입니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-156">Click **myVnetA** when it appears in hello search results.</span></span> <span data-ttu-id="b728d-157">블레이드 hello에 대 한 표시 **myVnetA** 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-157">A blade appears for hello **myVnetA** virtual network.</span></span>
5. <span data-ttu-id="b728d-158">Hello에 **myVnetA** 블레이드를 놓고 클릭 **액세스 제어 (IAM)** hello 세로 hello hello 블레이드의 왼쪽에 옵션 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-158">In hello **myVnetA** blade that appears, click **Access control (IAM)** from hello vertical list of options on hello left side of hello blade.</span></span>
6. <span data-ttu-id="b728d-159">Hello에 **myVnetA-액세스 제어 (IAM)** 블레이드를 놓고 클릭 **+ 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-159">In hello **myVnetA - Access control (IAM)** blade that appears, click **+ Add**.</span></span>
7. <span data-ttu-id="b728d-160">Hello에 **사용 권한을 추가** 선택 표시 되 면 블레이드 **네트워크 참가자** hello에 **역할** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-160">In hello **Add permissions** blade that appears, select **Network contributor** in hello **Role** box.</span></span>
8. <span data-ttu-id="b728d-161">Hello에 **선택** 상자 UserB 선택 하거나 입력 한 사용자 b의 전자 메일 주소 toosearch 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-161">In hello **Select** box, select UserB, or type UserB's email address toosearch for it.</span></span> <span data-ttu-id="b728d-162">hello 표시 된 사용자의 목록은 다음과 같이 hello에서 hello에 대 한 피어 링을 설정 하 고 hello 가상 네트워크와 같은 Azure Active Directory 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-162">hello list of users shown is from hello same Azure Active Directory tenant as hello virtual network you're setting up hello peering for.</span></span> <span data-ttu-id="b728d-163">Hello 목록에 표시 되 면 UserB를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-163">Click UserB when it appears in hello list.</span></span>
9. <span data-ttu-id="b728d-164">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-164">Click **Save**.</span></span>
10. <span data-ttu-id="b728d-165">UserA로 hello 포털에서 기록 한 다음 사용자 b로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-165">Log out of hello portal as UserA, then log in as UserB.</span></span>
11. <span data-ttu-id="b728d-166">클릭 **+ 새로 만들기**, 형식 *가상 네트워크* hello에 **검색 hello 마켓플레이스** 클릭 한 다음 상자 **가상 네트워크** hello 검색 결과에서 .</span><span class="sxs-lookup"><span data-stu-id="b728d-166">Click **+ New**, type *Virtual network* in hello **Search hello Marketplace** box, then click **Virtual network** in hello search results.</span></span>
12. <span data-ttu-id="b728d-167">Hello에 **가상 네트워크** 선택 표시 되 면 블레이드 **클래식** hello에 **배포 모델 선택** 클릭 한 다음 상자 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-167">In hello **Virtual Network** blade that appears, select **Classic** in hello **Select a deployment model** box, then click **Create**.</span></span>
13.   <span data-ttu-id="b728d-168">Hello 만들기 가상 네트워크 (클래식) 상자가 표시 되 면 hello 다음 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-168">In hello Create virtual network (classic) box that appears, enter hello following values:</span></span>

    - <span data-ttu-id="b728d-169">**이름**: *myVnetB*</span><span class="sxs-lookup"><span data-stu-id="b728d-169">**Name**: *myVnetB*</span></span>
    - <span data-ttu-id="b728d-170">**주소 공간**: *10.1.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="b728d-170">**Address space**: *10.1.0.0/16*</span></span>
    - <span data-ttu-id="b728d-171">**서브넷 이름**: *기본값*</span><span class="sxs-lookup"><span data-stu-id="b728d-171">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="b728d-172">**서브넷 주소 범위**: *10.1.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="b728d-172">**Subnet address range**: *10.1.0.0/24*</span></span>
    - <span data-ttu-id="b728d-173">**구독**: 구독 B를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-173">**Subscription**: Select subscription B.</span></span>
    - <span data-ttu-id="b728d-174">**리소스 그룹**: **새로 만들기**를 선택하고 *myResourceGroupB*를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-174">**Resource group**: Select **Create new** and enter *myResourceGroupB*</span></span>
    - <span data-ttu-id="b728d-175">**위치**: *미국 동부*</span><span class="sxs-lookup"><span data-stu-id="b728d-175">**Location**: *East US*</span></span>

14. <span data-ttu-id="b728d-176">Hello에 **리소스 검색** 형식 hello 포털의 hello 상단 상자 *myVnetB*합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-176">In hello **Search resources** box at hello top of hello portal, type *myVnetB*.</span></span> <span data-ttu-id="b728d-177">클릭 **myVnetB** hello 검색 결과에 표시 되 면입니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-177">Click **myVnetB** when it appears in hello search results.</span></span> <span data-ttu-id="b728d-178">블레이드 hello에 대 한 표시 **myVnetB** 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-178">A blade appears for hello **myVnetB** virtual network.</span></span>
15. <span data-ttu-id="b728d-179">Hello에 **myVnetB** 블레이드를 놓고 클릭 **속성** hello 세로 hello hello 블레이드의 왼쪽에 옵션 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-179">In hello **myVnetB** blade that appears, click **Properties** from hello vertical list of options on hello left side of hello blade.</span></span> <span data-ttu-id="b728d-180">복사 hello **리소스 ID**, 이후 단계에서 사용 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-180">Copy hello **RESOURCE ID**, which is used in a later step.</span></span> <span data-ttu-id="b728d-181">hello 리소스 ID는 다음 예제와 비슷한 toohello: /subscriptions/<Susbscription ID>/resourceGroups/myResoureGroupB/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB</span><span class="sxs-lookup"><span data-stu-id="b728d-181">hello resource ID is similar toohello following example: /subscriptions/<Susbscription ID>/resourceGroups/myResoureGroupB/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB</span></span>
16. <span data-ttu-id="b728d-182">MyVnetB에 대해 5-9단계를 완료하고 8단계에서 **사용자 A**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-182">Complete steps 5-9 for myVnetB, entering **UserA** in step 8.</span></span>
17. <span data-ttu-id="b728d-183">로그 UserB으로 hello 포털 아웃 한 UserA로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-183">Log out of hello portal as UserB and log in as UserA.</span></span>
18. <span data-ttu-id="b728d-184">Hello에 **리소스 검색** 형식 hello 포털의 hello 상단 상자 *myVnetA*합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-184">In hello **Search resources** box at hello top of hello portal, type *myVnetA*.</span></span> <span data-ttu-id="b728d-185">클릭 **myVnetA** hello 검색 결과에 표시 되 면입니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-185">Click **myVnetA** when it appears in hello search results.</span></span> <span data-ttu-id="b728d-186">블레이드 hello에 대 한 표시 **myVnet** 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-186">A blade appears for hello **myVnet** virtual network.</span></span>
19. <span data-ttu-id="b728d-187">**myVnetA**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-187">Click **myVnetA**.</span></span>
20. <span data-ttu-id="b728d-188">Hello에 **myVnetA** 블레이드를 놓고 클릭 **피어 링** hello 세로 hello hello 블레이드의 왼쪽에 옵션 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-188">In hello **myVnetA** blade that appears, click **Peerings** from hello vertical list of options on hello left side of hello blade.</span></span>
21. <span data-ttu-id="b728d-189">Hello에 **myVnetA-피어 링** 나타나면 블레이드 클릭 **+ 추가**</span><span class="sxs-lookup"><span data-stu-id="b728d-189">In hello **myVnetA - Peerings** blade that appeared, click **+ Add**</span></span>
22. <span data-ttu-id="b728d-190">Hello에 **추가 피어 링** 나타나는 블레이드를 입력 하거나 hello 다음 옵션을 선택한 다음 클릭 **확인**:</span><span class="sxs-lookup"><span data-stu-id="b728d-190">In hello **Add peering** blade that appears, enter, or select hello following options, then click **OK**:</span></span>
     - <span data-ttu-id="b728d-191">**이름**: *myVnetAToMyVnetB*</span><span class="sxs-lookup"><span data-stu-id="b728d-191">**Name**: *myVnetAToMyVnetB*</span></span>
     - <span data-ttu-id="b728d-192">**가상 네트워크 배포 모델**: **클래식**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-192">**Virtual network deployment model**:  Select **Classic**.</span></span>
     - <span data-ttu-id="b728d-193">**리소스 ID를 알고 있음**: 이 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-193">**I know my resource ID**: Check this box.</span></span>
     - <span data-ttu-id="b728d-194">**리소스 ID**: 15 단계에서 myVnetB의 hello 리소스 ID를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-194">**Resource ID**: Enter hello resource ID of myVnetB from step 15.</span></span>
     - <span data-ttu-id="b728d-195">**가상 네트워크 액세스 허용:** **사용**이 선택되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-195">**Allow virtual network access:** Ensure that **Enabled** is selected.</span></span>
    <span data-ttu-id="b728d-196">이 자습서에서 다른 설정은 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-196">No other settings are used in this tutorial.</span></span> <span data-ttu-id="b728d-197">모든 피어 링 설정에 대 한 toolearn 읽을 [관리 가상 네트워크 피어 링](virtual-network-manage-peering.md#create-a-peering)합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-197">toolearn about all peering settings, read [Manage virtual network peerings](virtual-network-manage-peering.md#create-a-peering).</span></span>
23. <span data-ttu-id="b728d-198">클릭 한 후 **확인** hello 이전 단계에서 hello **추가 피어 링** 블레이드를 닫고 hello 참조 **myVnetA-피어 링** 블레이드를 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-198">After clicking **OK** in hello previous step, hello **Add peering** blade closes and you see hello **myVnetA - Peerings** blade again.</span></span> <span data-ttu-id="b728d-199">몇 초 후 사용자가 만든 피어 링 hello hello 블레이드에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-199">After a few seconds, hello peering you created appears in hello blade.</span></span> <span data-ttu-id="b728d-200">**연결** hello에 나열 된 **피어 링 상태** hello에 대 한 열 **myVnetAToMyVnetB** 만든 피어 링 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-200">**Connected** is listed in hello **PEERING STATUS** column for hello **myVnetAToMyVnetB** peering you created.</span></span> <span data-ttu-id="b728d-201">hello 피어 링 이제 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-201">hello peering is now established.</span></span> <span data-ttu-id="b728d-202">네트워크가 없습니다 필요 toopeer hello 가상 네트워크 (클래식) toohello 가상 (리소스 관리자)입니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-202">There is no need toopeer hello virtual network (classic) toohello virtual network (Resource Manager).</span></span>

    <span data-ttu-id="b728d-203">가상 네트워크 중 하나에서 만드는 모든 Azure 리소스의 IP 주소를 통해 서로 수 toocommunicate 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-203">Any Azure resources you create in either virtual network are now able toocommunicate with each other through their IP addresses.</span></span> <span data-ttu-id="b728d-204">Hello 가상 네트워크에 대 한 기본 Azure 이름 확인을 사용 중인 경우 hello hello 가상 네트워크의 리소스가 하지 수 tooresolve 이름을 hello 가상 네트워크를 통해입니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-204">If you're using default Azure name resolution for hello virtual networks, hello resources in hello virtual networks are not able tooresolve names across hello virtual networks.</span></span> <span data-ttu-id="b728d-205">피어 링의 가상 네트워크에서 tooresolve 이름을 하려는 경우 자체 DNS 서버를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-205">If you want tooresolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="b728d-206">자세한 방법을를 tooset [자체 DNS 서버를 사용 하 여 이름 확인](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-206">Learn how tooset up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

24. <span data-ttu-id="b728d-207">**선택적**: 가상 컴퓨터를 만들어이 자습서에서 다루지 않습니다, 경우에 각 가상 네트워크에서 가상 컴퓨터를 만들 하 고 기타, 하나의 가상 컴퓨터 toohello toovalidate 연결에서에서 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-207">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
25. <span data-ttu-id="b728d-208">**선택적**:이 자습서에서 만드는 toodelete hello 리소스 hello에서 단계를 완료 hello [리소스를 삭제](#delete-portal) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="b728d-208">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in hello [Delete resources](#delete-portal) section of this article.</span></span>

## <span data-ttu-id="b728d-209"><a name="cli"></a>피어링 만들기 - Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b728d-209"><a name="cli"></a>Create peering - Azure CLI</span></span>

<span data-ttu-id="b728d-210">이 자습서에서는 각 구독에 대해 다른 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-210">This tutorial uses different accounts for each subscription.</span></span> <span data-ttu-id="b728d-211">사용 권한을 tooboth 구독이 있는 계정을 사용 하는 모든 단계에 대 한 계정을 동일한 Azure에서 로깅에 대 한 hello 단계를 건너뛸 및 사용자 역할 할당을 만드는 스크립트의 hello 줄을 제거 하는 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-211">If you're using an account that has permissions tooboth subscriptions, you can use hello same account for all steps, skip hello steps for logging out of Azure, and remove hello lines of script that create user role assignments.</span></span> <span data-ttu-id="b728d-212">대체 UserA@azure.com 및 UserB@azure.com 의 UserA와 사용자 b에 사용할 hello 사용자 이름 사용 하 여 스크립트를 다음 hello 모든 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-212">Replace UserA@azure.com and UserB@azure.com in all of hello following scripts with hello usernames you're using for UserA and UserB.</span></span> 

<span data-ttu-id="b728d-213">Hello 다음 단계를 완료 하기 전에 hello 미리 보기에 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-213">Before completing any of hello following steps, you must register for hello preview.</span></span> <span data-ttu-id="b728d-214">tooregister, hello에서 단계를 완료 하는 hello [hello 미리 보기를 등록할](#register) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="b728d-214">tooregister, complete hello steps in hello [Register for hello preview](#register) section of this article.</span></span> <span data-ttu-id="b728d-215">두 구독 hello 미리 보기에 등록 될 때까지 단계를 남은 hello로 계속 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="b728d-215">Do not continue with hello remaining steps until both subscriptions are registered for hello preview.</span></span>

1. <span data-ttu-id="b728d-216">[설치](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello Azure CLI 1.0 toocreate hello 가상 네트워크 (클래식).</span><span class="sxs-lookup"><span data-stu-id="b728d-216">[Install](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello Azure CLI 1.0 toocreate hello virtual network (classic).</span></span>
2. <span data-ttu-id="b728d-217">CLI 세션을 열고 tooAzure hello를 사용 하 여 사용자 b로 로그인 `azure login` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-217">Open a CLI session and log in tooAzure as UserB using hello `azure login` command.</span></span>
3. <span data-ttu-id="b728d-218">Hello를 입력 하 여 hello CLI 서비스 관리 모드에서 실행 `azure config mode asm` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-218">Run hello CLI in Service Management mode by entering hello `azure config mode asm` command.</span></span>
4. <span data-ttu-id="b728d-219">Hello 다음 toocreate hello 가상 네트워크 (클래식) 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-219">Enter hello following command toocreate hello virtual network (classic):</span></span>
 
    ```azurecli
    azure network vnet create --vnet myVnetB --address-space 10.1.0.0 --cidr 16 --location "East US"
    ```
5. <span data-ttu-id="b728d-220">Azure CLI 2.0.4 hello로 bash 셸의 사용 하 여 hello 나머지 단계를 완료 해야 이상 [설치](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json), 또는 Azure 클라우드 셸 hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-220">hello remaining steps must be completed using a bash shell with hello Azure CLI 2.0.4 or later [installed](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json), or by using hello Azure Cloud Shell.</span></span> <span data-ttu-id="b728d-221">Azure 클라우드 셸 hello hello Azure 포털 내에서 직접 실행할 수 있는 무료 Bash 셸의입니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-221">hello Azure Cloud Shell is a free Bash shell that you can run directly within hello Azure portal.</span></span> <span data-ttu-id="b728d-222">Hello Azure CLI 사전 설치 및 toouse 사용자 계정으로 구성 된이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-222">It has hello Azure CLI preinstalled and configured toouse with your account.</span></span> <span data-ttu-id="b728d-223">Hello 클릭 **실습** hello 단추 tooyour Azure 계정이 로그인 하는 클라우드 셸을 엽니다. 나오는 스크립팅 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-223">Click hello **Try it** button in hello scripts that follow, which opens a Cloud Shell that logs you in tooyour Azure account.</span></span> <span data-ttu-id="b728d-224">옵션 실행 중에 Windows 클라이언트에서 CLI 스크립트를 이용한 적, 참조 [hello Azure CLI Windows에서 실행 중인](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-224">For options on running bash CLI scripts on a Windows client, see [Running hello Azure CLI in Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> 
6. <span data-ttu-id="b728d-225">Hello 나오는 스크립트 tooa 텍스트 편집기를 사용자 PC에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-225">Copy hello following script tooa text editor on your PC.</span></span> <span data-ttu-id="b728d-226">`<SubscriptionB-Id>`는 구독 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-226">Replace `<SubscriptionB-Id>` with your subscription ID.</span></span> <span data-ttu-id="b728d-227">구독 Id를 모르는 경우 입력 hello `az account show` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-227">If you don't know your subscription Id, enter hello `az account show` command.</span></span> <span data-ttu-id="b728d-228">값에 대 한 hello **id** hello 출력은 구독 id입니다. 수정 하는 hello 스크립트 tooyour CLI 2.0 세션에 붙여 복사한 다음 키를 누릅니다 `Enter`합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-228">hello value for **id** in hello output is your subscription Id. Copy hello modified script, paste it in tooyour CLI 2.0 session, and then press `Enter`.</span></span> 

    ```azurecli-interactive
    az role assignment create \
      --assignee UserA@azure.com \
      --role "Classic Network Contributor" \
      --scope /subscriptions/<SubscriptionB-Id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

    <span data-ttu-id="b728d-229">Azure의 hello hello 가상 네트워크를 만든을 만들 때 hello 가상 네트워크 (클래식) 4 단계에서 *기본 네트워킹* 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-229">When you created hello virtual network (classic) in step 4, Azure created hello virtual network in hello *Default-Networking* resource group.</span></span>
7. <span data-ttu-id="b728d-230">Azure와 로그에 도달 하면 UserB UserA로 hello CLI 2.0 로그인 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-230">Log UserB out of Azure and log in as UserA in hello CLI 2.0.</span></span>
8. <span data-ttu-id="b728d-231">리소스 그룹 및 가상 네트워크(리소스 관리자)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-231">Create a resource group and a virtual network (Resource Manager).</span></span> <span data-ttu-id="b728d-232">복사 hello 다음 스크립트 tooyour CLI 세션에 붙여 넣고 다음 키를 누릅니다 `Enter`합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-232">Copy hello following script, paste it in tooyour CLI session, and then press `Enter`.</span></span> 

    ```azurecli-interactive
    #!/bin/bash

    # Variables for common values used throughout hello script.
    rgName="myResourceGroupA"
    location="eastus"

    # Create a resource group.
    az group create \
      --name $rgName \
      --location $location

    # Create virtual network A (Resource Manager).
    az network vnet create \
      --name myVnetA \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.0.0.0/16

    # Get hello id for myVnetA.
    vNetAId=$(az network vnet show \
      --resource-group $rgName \
      --name myVnetA \
      --query id --out tsv)

    # Assign UserB permissions toomyVnetA.
    az role assignment create \
      --assignee UserB@azure.com \
      --role "Network Contributor" \
      --scope $vNetAId
    ```

9. <span data-ttu-id="b728d-233">Hello 다양 한 배포 모델을 통해 만든 hello 두 가상 네트워크 간의 피어 링 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-233">Create a virtual network peering between hello two virtual networks created through hello different deployment models.</span></span> <span data-ttu-id="b728d-234">Hello 나오는 스크립트 tooa 텍스트 편집기를 사용자 PC에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-234">Copy hello following script tooa text editor on your PC.</span></span> <span data-ttu-id="b728d-235">`<SubscriptionB-id>`는 구독 ID로 바꿉니다. 구독 Id를 모르는 경우 입력 hello `az account show` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-235">Replace `<SubscriptionB-id>` with your subscription Id. If you don't know your subscription Id, enter hello `az account show` command.</span></span> <span data-ttu-id="b728d-236">값에 대 한 hello **id** hello 출력은 구독 id입니다. Azure 명명 된 리소스 그룹의 4 단계에서 만든 가상 hello 네트워크 (클래식)를 만든 *기본 네트워킹*합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-236">hello value for **id** in hello output is your subscription Id. Azure created hello virtual network (classic) you created in step 4 in a resource group named *Default-Networking*.</span></span> <span data-ttu-id="b728d-237">CLI 세션에서 수정 하는 hello 스크립트를 붙여 넣고 다음 키를 누릅니다 `Enter`합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-237">Paste hello modified script in your CLI session, and then press `Enter`.</span></span>

    ```azurecli-interactive
    # Peer VNet1 tooVNet2.
    az network vnet peering create \
      --name myVnetAToMyVnetB \
      --resource-group $rgName \
      --vnet-name myVnetA \
      --remote-vnet-id  /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB \
      --allow-vnet-access
    ```

10. <span data-ttu-id="b728d-238">Hello 스크립트를 실행 한 후에 hello 가상 네트워크 (리소스 관리자)에 대 한 피어 링 hello를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-238">After hello script executes, review hello peering for hello virtual network (Resource Manager).</span></span> <span data-ttu-id="b728d-239">다음 스크립트를 hello 복사한 CLI 세션에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-239">Copy hello following script, and then paste it in your CLI session:</span></span>

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group $rgName \
      --vnet-name myVnetA \
      --output table
    ```
    <span data-ttu-id="b728d-240">hello 출력 있는지 보여 줍니다 **연결 됨** hello에 **PeeringState** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-240">hello output shows **Connected** in hello **PeeringState** column.</span></span>

    <span data-ttu-id="b728d-241">가상 네트워크 중 하나에서 만드는 모든 Azure 리소스의 IP 주소를 통해 서로 수 toocommunicate 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-241">Any Azure resources you create in either virtual network are now able toocommunicate with each other through their IP addresses.</span></span> <span data-ttu-id="b728d-242">Hello 가상 네트워크에 대 한 기본 Azure 이름 확인을 사용 중인 경우 hello hello 가상 네트워크의 리소스가 하지 수 tooresolve 이름을 hello 가상 네트워크를 통해입니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-242">If you're using default Azure name resolution for hello virtual networks, hello resources in hello virtual networks are not able tooresolve names across hello virtual networks.</span></span> <span data-ttu-id="b728d-243">피어 링의 가상 네트워크에서 tooresolve 이름을 하려는 경우 자체 DNS 서버를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-243">If you want tooresolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="b728d-244">자세한 방법을를 tooset [자체 DNS 서버를 사용 하 여 이름 확인](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-244">Learn how tooset up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

11. <span data-ttu-id="b728d-245">**선택적**: 가상 컴퓨터를 만들어이 자습서에서 다루지 않습니다, 경우에 각 가상 네트워크에서 가상 컴퓨터를 만들 하 고 기타, 하나의 가상 컴퓨터 toohello toovalidate 연결에서에서 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-245">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
12. <span data-ttu-id="b728d-246">**선택적**:이 자습서에서 만드는 toodelete hello 리소스의 단계를 완료 hello [리소스를 삭제](#delete-cli) 이 문서의 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-246">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in [Delete resources](#delete-cli) in this article.</span></span>

## <span data-ttu-id="b728d-247"><a name="powershell"></a>피어링 만들기 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="b728d-247"><a name="powershell"></a>Create peering - PowerShell</span></span>

<span data-ttu-id="b728d-248">이 자습서에서는 각 구독에 대해 다른 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-248">This tutorial uses different accounts for each subscription.</span></span> <span data-ttu-id="b728d-249">사용 권한을 tooboth 구독이 있는 계정을 사용 하는 모든 단계에 대 한 계정을 동일한 Azure에서 로깅에 대 한 hello 단계를 건너뛸 및 사용자 역할 할당을 만드는 스크립트의 hello 줄을 제거 하는 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-249">If you're using an account that has permissions tooboth subscriptions, you can use hello same account for all steps, skip hello steps for logging out of Azure, and remove hello lines of script that create user role assignments.</span></span> <span data-ttu-id="b728d-250">대체 UserA@azure.com 및 UserB@azure.com 의 UserA와 사용자 b에 사용할 hello 사용자 이름 사용 하 여 스크립트를 다음 hello 모든 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-250">Replace UserA@azure.com and UserB@azure.com in all of hello following scripts with hello usernames you're using for UserA and UserB.</span></span> 

<span data-ttu-id="b728d-251">Hello 다음 단계를 완료 하기 전에 hello 미리 보기에 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-251">Before completing any of hello following steps, you must register for hello preview.</span></span> <span data-ttu-id="b728d-252">tooregister, hello에서 단계를 완료 하는 hello [hello 미리 보기를 등록할](#register) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="b728d-252">tooregister, complete hello steps in hello [Register for hello preview](#register) section of this article.</span></span> <span data-ttu-id="b728d-253">두 구독 hello 미리 보기에 등록 될 때까지 단계를 남은 hello로 계속 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="b728d-253">Do not continue with hello remaining steps until both subscriptions are registered for hello preview.</span></span>

1. <span data-ttu-id="b728d-254">Hello hello PowerShell의 최신 버전을 설치 [Azure](https://www.powershellgallery.com/packages/Azure) 및 [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-254">Install hello latest version of hello PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) and [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modules.</span></span> <span data-ttu-id="b728d-255">새 tooAzure PowerShell 인 경우 참조 [Azure PowerShell 개요](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-255">If you're new tooAzure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="b728d-256">PowerShell 세션을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-256">Start a PowerShell session.</span></span>
3. <span data-ttu-id="b728d-257">PowerShell에서 UserB tooUserB의 구독에 입력 하 여 로그인 hello `Add-AzureAccount` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-257">In PowerShell, log in tooUserB's subscription as UserB by entering hello `Add-AzureAccount` command.</span></span>
4. <span data-ttu-id="b728d-258">PowerShell 사용 하 여 가상 네트워크 (클래식) toocreate 있습니다 새로 만들거나 수정 해야는 기존 네트워크 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-258">toocreate a virtual network (classic) with PowerShell, you must create a new, or modify an existing, network configuration file.</span></span> <span data-ttu-id="b728d-259">너무 방법에 대해 알아봅니다[내보내기, 업데이트 및 네트워크 구성 파일을 가져올](virtual-networks-using-network-configuration-file.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-259">Learn how too[export, update, and import network configuration files](virtual-networks-using-network-configuration-file.md).</span></span> <span data-ttu-id="b728d-260">hello 파일에 포함할지 hello 다음 **VirtualNetworkSite** 이 자습서에 사용 된 hello 가상 네트워크에 대 한 요소:</span><span class="sxs-lookup"><span data-stu-id="b728d-260">hello file should include hello following **VirtualNetworkSite** element for hello virtual network used in this tutorial:</span></span>

    ```xml
    <VirtualNetworkSite name="myVnetB" Location="East US">
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
    > <span data-ttu-id="b728d-261">변경 된 네트워크 구성 파일을 가져오는 변경 될 수 tooexisting 가상 네트워크 (클래식)를 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-261">Importing a changed network configuration file can cause changes tooexisting virtual networks (classic) in your subscription.</span></span> <span data-ttu-id="b728d-262">만 hello 이전 가상 네트워크를 추가 하 고 변경 하거나 구독에서 기존 가상 네트워크를 제거 하지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-262">Ensure you only add hello previous virtual network and that you don't change or remove any existing virtual networks from your subscription.</span></span> 

5. <span data-ttu-id="b728d-263">Hello를 입력 하 여 UserB toouse 리소스 관리자 명령으로 tooUserB의 구독에 로그인 `login-azurermaccount` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-263">Log in tooUserB's subscription as UserB toouse Resource Manager commands by entering hello `login-azurermaccount` command.</span></span>
6. <span data-ttu-id="b728d-264">2. 복사 hello 다음 스크립트 PC에서 tooa 텍스트 편집기 및 바꾸기 할당 UserA 권한 toovirtual 네트워크 `<SubscriptionB-id>` hello 2. 구독 ID로 Hello 구독 Id를 모르는 경우 입력 hello `Get-AzureRmSubscription` 명령 tooview 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-264">Assign UserA permissions toovirtual network B. Copy hello following script tooa text editor on your PC and replace `<SubscriptionB-id>` with hello ID of subscription B. If you don't know hello subscription Id, enter hello `Get-AzureRmSubscription` command tooview it.</span></span> <span data-ttu-id="b728d-265">값에 대 한 hello **Id** hello 반환 출력은 프로그램 구독 id입니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-265">hello value for **Id** in hello returned output is your subscription ID.</span></span> <span data-ttu-id="b728d-266">Azure 명명 된 리소스 그룹의 4 단계에서 만든 가상 hello 네트워크 (클래식)를 만든 *기본 네트워킹*합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-266">Azure created hello virtual network (classic) you created in step 4 in a resource group named *Default-Networking*.</span></span> <span data-ttu-id="b728d-267">tooexecute hello 스크립트 복사 hello 수정 된 스크립트 tooPowerShell에 붙여 넣고 다음 키를 누릅니다 `Enter`합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-267">tooexecute hello script, copy hello modified script, paste it in tooPowerShell, and then press `Enter`.</span></span>
    
    ```powershell 
    New-AzureRmRoleAssignment `
      -SignInName UserA@azure.com `
      -RoleDefinitionName "Classic Network Contributor" `
      -Scope /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

7. <span data-ttu-id="b728d-268">UserB으로 Azure에서 로그 아웃 하 고 hello를 입력 하 여 UserA tooUserA의 구독에 로그인 `login-azurermaccount` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-268">Log out of Azure as UserB and log in tooUserA's subscription as UserA by entering hello `login-azurermaccount` command.</span></span> <span data-ttu-id="b728d-269">가상 네트워크 피어 링 hello 필요한 권한을 toocreate 사용 하 여 로그인 하는 hello 계정에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-269">hello account you log in with must have hello necessary permissions toocreate a virtual network peering.</span></span> <span data-ttu-id="b728d-270">Hello 참조 [권한을](#permissions) 대 한 자세한 내용은이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="b728d-270">See hello [Permissions](#permissions) section of this article for details.</span></span>
8. <span data-ttu-id="b728d-271">다음 스크립트를 tooPowerShell, 한 키를 눌러 다음에 붙여 넣어 hello를 복사 하 여 hello 가상 네트워크 (리소스 관리자)을 만들 `Enter`:</span><span class="sxs-lookup"><span data-stu-id="b728d-271">Create hello virtual network (Resource Manager) by copying hello following script, pasting it in tooPowerShell, and then pressing `Enter`:</span></span>

    ```powershell
    # Variables for common values
      $rgName='MyResourceGroupA'
      $location='eastus'

    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name $rgName `
      -Location $location

    # Create virtual network A.
    $vnetA = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnetA' `
      -AddressPrefix '10.0.0.0/16' `
      -Location $location
    ```

9. <span data-ttu-id="b728d-272">사용 권한 toomyVnetA UserB를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-272">Assign UserB permissions toomyVnetA.</span></span> <span data-ttu-id="b728d-273">복사 hello 다음 스크립트 PC에서 tooa 텍스트 편집기 및 바꾸기 `<SubscriptionA-Id>` hello 1. 구독 ID로 Hello 구독 Id를 모르는 경우 입력 hello `Get-AzureRmSubscription` 명령 tooview 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-273">Copy hello following script tooa text editor on your PC and replace `<SubscriptionA-Id>` with hello ID of subscription A. If you don't know hello subscription Id, enter hello `Get-AzureRmSubscription` command tooview it.</span></span> <span data-ttu-id="b728d-274">값에 대 한 hello **Id** hello 반환 출력은 프로그램 구독 id입니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-274">hello value for **Id** in hello returned output is your subscription ID.</span></span> <span data-ttu-id="b728d-275">PowerShell에서 hello hello 스크립트의 수정된 버전을 붙여 넣고 다음 키를 누릅니다 `Enter` tooexecute 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-275">Paste hello modified version of hello script in PowerShell, and then press `Enter` tooexecute it.</span></span>

    ```powershell
    New-AzureRmRoleAssignment `
      -SignInName UserB@azure.com `
      -RoleDefinitionName "Network Contributor" `
      -Scope /subscriptions/<SubscriptionA-Id>/resourceGroups/myResourceGroupA/providers/Microsoft.Network/VirtualNetworks/myVnetA
    ```

10. <span data-ttu-id="b728d-276">복사 hello 다음 스크립트 pc에서는 tooa 텍스트 편집기 및 바꾸기 `<SubscriptionB-id>` 구독 B. toopeer myVnetA toomyVNetB의 hello ID로 수정 hello 스크립트, tooPowerShell에 붙여 복사한 다음 키를 누릅니다 `Enter`합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-276">Copy hello following script tooa text editor on your PC, and replace `<SubscriptionB-id>` with hello ID of subscription B. toopeer myVnetA toomyVNetB, copy hello modified script, paste it in tooPowerShell, and then press `Enter`.</span></span>

    ```powershell
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnetAToMyVnetB' `
      -VirtualNetwork $vnetA `
      -RemoteVirtualNetworkId /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

11. <span data-ttu-id="b728d-277">다음 스크립트를 PowerShell 및 키를 눌러에 붙여 넣어 hello를 복사 하 여 myVnetA의 hello 피어 링 상태를 볼 `Enter`합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-277">View hello peering state of myVnetA by copying hello following script, pasting it into PowerShell, and pressing `Enter`.</span></span>

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName $rgName `
      -VirtualNetworkName myVnetA `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    <span data-ttu-id="b728d-278">hello 상태가 **연결 됨**합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-278">hello state is **Connected**.</span></span> <span data-ttu-id="b728d-279">너무 변경**연결 됨** hello 피어 링 toomyVnetA myVnetB에서 설정 되 면입니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-279">It changes too**Connected** once you setup hello peering toomyVnetA from myVnetB.</span></span>

    <span data-ttu-id="b728d-280">가상 네트워크 중 하나에서 만드는 모든 Azure 리소스의 IP 주소를 통해 서로 수 toocommunicate 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-280">Any Azure resources you create in either virtual network are now able toocommunicate with each other through their IP addresses.</span></span> <span data-ttu-id="b728d-281">Hello 가상 네트워크에 대 한 기본 Azure 이름 확인을 사용 중인 경우 hello hello 가상 네트워크의 리소스가 하지 수 tooresolve 이름을 hello 가상 네트워크를 통해입니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-281">If you're using default Azure name resolution for hello virtual networks, hello resources in hello virtual networks are not able tooresolve names across hello virtual networks.</span></span> <span data-ttu-id="b728d-282">피어 링의 가상 네트워크에서 tooresolve 이름을 하려는 경우 자체 DNS 서버를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-282">If you want tooresolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="b728d-283">자세한 방법을를 tooset [자체 DNS 서버를 사용 하 여 이름 확인](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-283">Learn how tooset up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

12. <span data-ttu-id="b728d-284">**선택적**: 가상 컴퓨터를 만들어이 자습서에서 다루지 않습니다, 경우에 각 가상 네트워크에서 가상 컴퓨터를 만들 하 고 기타, 하나의 가상 컴퓨터 toohello toovalidate 연결에서에서 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-284">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
13. <span data-ttu-id="b728d-285">**선택적**:이 자습서에서 만드는 toodelete hello 리소스의 단계를 완료 hello [리소스를 삭제](#delete-powershell) 이 문서의 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-285">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in [Delete resources](#delete-powershell) in this article.</span></span>

## <span data-ttu-id="b728d-286"><a name="permissions"></a>권한</span><span class="sxs-lookup"><span data-stu-id="b728d-286"><a name="permissions"></a>Permissions</span></span>

<span data-ttu-id="b728d-287">hello 계정 toocreate 가상 네트워크 피어 링을 사용 하 여 hello 필요한 역할 또는 사용 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-287">hello accounts you use toocreate a virtual network peering must have hello necessary role or permissions.</span></span> <span data-ttu-id="b728d-288">예를 들어 myVnetA 및 myVnetB 라는 두 개의 가상 네트워크, 피어 링 된 경우 사용자 계정에 할당 해야 최소 역할 또는 각 가상 네트워크에 대 한 사용 권한을 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="b728d-288">For example, if you were peering two virtual networks named myVnetA and myVnetB, your account must be assigned hello following minimum role or permissions for each virtual network:</span></span>
    
|<span data-ttu-id="b728d-289">가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="b728d-289">Virtual network</span></span>|<span data-ttu-id="b728d-290">배포 모델</span><span class="sxs-lookup"><span data-stu-id="b728d-290">Deployment model</span></span>|<span data-ttu-id="b728d-291">역할</span><span class="sxs-lookup"><span data-stu-id="b728d-291">Role</span></span>|<span data-ttu-id="b728d-292">권한</span><span class="sxs-lookup"><span data-stu-id="b728d-292">Permissions</span></span>|
|---|---|---|---|
|<span data-ttu-id="b728d-293">myVnetA</span><span class="sxs-lookup"><span data-stu-id="b728d-293">myVnetA</span></span>|<span data-ttu-id="b728d-294">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="b728d-294">Resource Manager</span></span>|[<span data-ttu-id="b728d-295">네트워크 참여자</span><span class="sxs-lookup"><span data-stu-id="b728d-295">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="b728d-296">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span><span class="sxs-lookup"><span data-stu-id="b728d-296">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span></span>|
| |<span data-ttu-id="b728d-297">클래식</span><span class="sxs-lookup"><span data-stu-id="b728d-297">Classic</span></span>|[<span data-ttu-id="b728d-298">클래식 네트워크 참여자</span><span class="sxs-lookup"><span data-stu-id="b728d-298">Classic Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|<span data-ttu-id="b728d-299">해당 없음</span><span class="sxs-lookup"><span data-stu-id="b728d-299">N/A</span></span>|
|<span data-ttu-id="b728d-300">myVnetB</span><span class="sxs-lookup"><span data-stu-id="b728d-300">myVnetB</span></span>|<span data-ttu-id="b728d-301">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="b728d-301">Resource Manager</span></span>|[<span data-ttu-id="b728d-302">네트워크 참여자</span><span class="sxs-lookup"><span data-stu-id="b728d-302">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="b728d-303">Microsoft.Network/virtualNetworks/peer</span><span class="sxs-lookup"><span data-stu-id="b728d-303">Microsoft.Network/virtualNetworks/peer</span></span>|
||<span data-ttu-id="b728d-304">클래식</span><span class="sxs-lookup"><span data-stu-id="b728d-304">Classic</span></span>|[<span data-ttu-id="b728d-305">클래식 네트워크 참여자</span><span class="sxs-lookup"><span data-stu-id="b728d-305">Classic Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|<span data-ttu-id="b728d-306">Microsoft.ClassicNetwork/virtualNetworks/peer</span><span class="sxs-lookup"><span data-stu-id="b728d-306">Microsoft.ClassicNetwork/virtualNetworks/peer</span></span>|

<span data-ttu-id="b728d-307">에 대 한 자세한 내용은 [기본 제공 역할](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) 너무 특정 사용 권한을 할당 하 고[사용자 정의 역할](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (리소스 관리자에만 해당).</span><span class="sxs-lookup"><span data-stu-id="b728d-307">Learn more about [built-in roles](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) and assigning specific permissions too[custom roles](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (Resource Manager only).</span></span>

## <span data-ttu-id="b728d-308"><a name="delete"></a>리소스 삭제</span><span class="sxs-lookup"><span data-stu-id="b728d-308"><a name="delete"></a>Delete resources</span></span>
<span data-ttu-id="b728d-309">이 자습서를 마친 toodelete hello 리소스 사용량에 따른 요금을 발생 하지 않습니다 하므로 hello 자습서에서 만든 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-309">When you've finished this tutorial, you might want toodelete hello resources you created in hello tutorial, so you don't incur usage charges.</span></span> <span data-ttu-id="b728d-310">리소스 그룹을 삭제 하면 hello 리소스 그룹에는 모든 리소스를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-310">Deleting a resource group also deletes all resources that are in hello resource group.</span></span>

### <span data-ttu-id="b728d-311"><a name="delete-portal"></a>Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b728d-311"><a name="delete-portal"></a>Azure portal</span></span>

1. <span data-ttu-id="b728d-312">Hello 포털 검색 상자에 입력 **myResourceGroupA**합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-312">In hello portal search box, enter **myResourceGroupA**.</span></span> <span data-ttu-id="b728d-313">Hello 검색 결과에서 클릭 **myResourceGroupA**합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-313">In hello search results, click **myResourceGroupA**.</span></span>
2. <span data-ttu-id="b728d-314">Hello에 **myResourceGroupA** 블레이드에서 hello 클릭 **삭제** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-314">On hello **myResourceGroupA** blade, click hello **Delete** icon.</span></span>
3. <span data-ttu-id="b728d-315">hello에 tooconfirm hello 삭제 **형식 hello 리소스 그룹 이름은** 상자에 입력 **myResourceGroupA**, 클릭 하 고 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-315">tooconfirm hello deletion, in hello **TYPE hello RESOURCE GROUP NAME** box, enter **myResourceGroupA**, and then click **Delete**.</span></span>
4. <span data-ttu-id="b728d-316">Hello에 **리소스 검색** 형식 hello 포털의 hello 상단 상자 *myVnetB*합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-316">In hello **Search resources** box at hello top of hello portal, type *myVnetB*.</span></span> <span data-ttu-id="b728d-317">클릭 **myVnetB** hello 검색 결과에 표시 되 면입니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-317">Click **myVnetB** when it appears in hello search results.</span></span> <span data-ttu-id="b728d-318">블레이드 hello에 대 한 표시 **myVnetB** 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-318">A blade appears for hello **myVnetB** virtual network.</span></span>
5. <span data-ttu-id="b728d-319">Hello에 **myVnetB** 블레이드에서 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-319">In hello **myVnetB** blade, click **Delete**.</span></span>
6. <span data-ttu-id="b728d-320">tooconfirm hello 삭제 클릭 **예** hello에 **가상 네트워크 삭제** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-320">tooconfirm hello deletion, click **Yes** in hello **Delete virtual network** box.</span></span>

### <span data-ttu-id="b728d-321"><a name="delete-cli"></a>Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b728d-321"><a name="delete-cli"></a>Azure CLI</span></span>

1. <span data-ttu-id="b728d-322">다음 명령을 hello로 CLI 2.0 toodelete hello 가상 네트워크 (리소스 관리자) tooAzure hello를 사용 하 여에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-322">Log in tooAzure using hello CLI 2.0 toodelete hello virtual network (Resource Manager) with hello following command:</span></span>

    ```azurecli-interactive
    az group delete --name myResourceGroupA --yes
    ```

2. <span data-ttu-id="b728d-323">명령 다음 hello로 Azure CLI 1.0 toodelete hello 가상 네트워크 (클래식) tooAzure hello를 사용 하 여에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-323">Log in tooAzure using hello Azure CLI 1.0 toodelete hello virtual network (classic) with hello following commands:</span></span>

    ```azurecli
    azure config mode asm 

    azure network vnet delete --vnet myVnetB --quiet
    ```

### <span data-ttu-id="b728d-324"><a name="delete-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="b728d-324"><a name="delete-powershell"></a>PowerShell</span></span>

1. <span data-ttu-id="b728d-325">Hello PowerShell 명령 프롬프트에서 다음 명령을 toodelete hello 가상 네트워크 (리소스 관리자) hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-325">At hello PowerShell command prompt, enter hello following command toodelete hello virtual network (Resource Manager):</span></span>

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroupA -Force
    ```

2. <span data-ttu-id="b728d-326">toodelete hello 가상 네트워크 (클래식) PowerShell과 함께 기존 네트워크 구성 파일을 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-326">toodelete hello virtual network (classic) with PowerShell, you must modify an existing network configuration file.</span></span> <span data-ttu-id="b728d-327">너무 방법에 대해 알아봅니다[내보내기, 업데이트 및 네트워크 구성 파일을 가져올](virtual-networks-using-network-configuration-file.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-327">Learn how too[export, update, and import network configuration files](virtual-networks-using-network-configuration-file.md).</span></span> <span data-ttu-id="b728d-328">이 자습서에 사용 된 hello 가상 네트워크에 대 한 VirtualNetworkSite 요소 다음에 오는 hello를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-328">Remove hello following VirtualNetworkSite element for hello virtual network used in this tutorial:</span></span>

    ```xml
    <VirtualNetworkSite name="myVnetB" Location="East US">
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
    > <span data-ttu-id="b728d-329">변경 된 네트워크 구성 파일을 가져오는 변경 될 수 tooexisting 가상 네트워크 (클래식)를 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-329">Importing a changed network configuration file can cause changes tooexisting virtual networks (classic) in your subscription.</span></span> <span data-ttu-id="b728d-330">만 hello 이전 가상 네트워크를 제거 하 고 변경 하거나 구독에서 다른 기존 가상 네트워크를 제거 하지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-330">Ensure you only remove hello previous virtual network and that you don't change or remove any other existing virtual networks from your subscription.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b728d-331">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b728d-331">Next steps</span></span>

- <span data-ttu-id="b728d-332">프로덕션 환경에 사용하기 위한 가상 네트워크 피어링을 만들기 전에 먼저 중요한 [가상 네트워크 피어링 제약 조건 및 동작](virtual-network-manage-peering.md#requirements-and-constraints)에 철저하게 익숙해집니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-332">Thoroughly familiarize yourself with important [virtual network peering constraints and behaviors](virtual-network-manage-peering.md#requirements-and-constraints) before creating a virtual network peering for production use.</span></span>
- <span data-ttu-id="b728d-333">모든 [가상 네트워크 피어링 설정](virtual-network-manage-peering.md#create-a-peering)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-333">Learn about all [virtual network peering settings](virtual-network-manage-peering.md#create-a-peering).</span></span>
- <span data-ttu-id="b728d-334">너무 방법에 대해 알아봅니다[허브를 만들고 네트워크 토폴로지 스포크](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) 가상 네트워크 피어 링을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b728d-334">Learn how too[create a hub and spoke network topology](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) with virtual network peering.</span></span>
