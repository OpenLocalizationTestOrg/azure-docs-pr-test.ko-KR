---
title: "Azure 가상 네트워크 피어링 만들기 - 서로 다른 배포 모델 - 서로 다른 구독 | Microsoft Docs"
description: "서로 다른 Azure 구독에 존재하는 서로 다른 Azure 배포 모델을 통해 만든 가상 네트워크 간의 가상 네트워크 피어링을 만드는 방법을 학습합니다."
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
ms.openlocfilehash: 93d5676e9188e67f1f6a9bba1d4d30a93b3883d8
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="create-a-virtual-network-peering---different-deployment-models-and-subscriptions"></a><span data-ttu-id="7638b-103">가상 네트워크 피어링 만들기 - 서로 다른 배포 모델 및 구독</span><span class="sxs-lookup"><span data-stu-id="7638b-103">Create a virtual network peering - different deployment models and subscriptions</span></span>

<span data-ttu-id="7638b-104">이 자습서에서는 서로 다른 배포 모델을 통해 만들어진 가상 네트워크 간의 가상 네트워크 피어링을 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-104">In this tutorial, you learn to create a virtual network peering between virtual networks created through different deployment models.</span></span> <span data-ttu-id="7638b-105">가상 네트워크가 서로 다른 구독에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-105">The virtual networks exist in different subscriptions.</span></span> <span data-ttu-id="7638b-106">두 가상 네트워크를 피어링하면 서로 다른 가상 네트워크에 있는 리소스가 같은 가상 네트워크에 있는 리소스인 것처럼 같은 대역폭 및 대기 시간으로 서로 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-106">Peering two virtual networks enables resources in different virtual networks to communicate with each other with the same bandwidth and latency as though the resources were in the same virtual network.</span></span> <span data-ttu-id="7638b-107">[가상 네트워크 피어링](virtual-network-peering-overview.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="7638b-107">Learn more about [Virtual network peering](virtual-network-peering-overview.md).</span></span> 

<span data-ttu-id="7638b-108">가상 네트워크 피어링을 만드는 단계는 가상 네트워크가 동일한 구독에 있는지 아니면 다른 구독에 있는지에 따라, 그리고 가상 네트워크가 어느 [Azure 배포 모델](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json)를 통해 생성되었는지에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-108">The steps to create a virtual network peering are different, depending on whether the virtual networks are in the same, or different, subscriptions, and which [Azure deployment model](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) the virtual networks are created through.</span></span> <span data-ttu-id="7638b-109">다음 표에 나온 시나리오를 클릭하여 다른 시나리오에서 가상 네트워크 피어링을 만드는 방법을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="7638b-109">Learn how to create a virtual network peering in other scenarios by clicking the scenario from the following table:</span></span>

|<span data-ttu-id="7638b-110">Azure 배포 모델</span><span class="sxs-lookup"><span data-stu-id="7638b-110">Azure deployment model</span></span>  | <span data-ttu-id="7638b-111">Azure 구독</span><span class="sxs-lookup"><span data-stu-id="7638b-111">Azure subscription</span></span>  |
|--------- |---------|
|[<span data-ttu-id="7638b-112">둘 다 리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="7638b-112">Both Resource Manager</span></span>](virtual-network-create-peering.md) |<span data-ttu-id="7638b-113">동일</span><span class="sxs-lookup"><span data-stu-id="7638b-113">Same</span></span>|
|[<span data-ttu-id="7638b-114">둘 다 리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="7638b-114">Both Resource Manager</span></span>](create-peering-different-subscriptions.md) |<span data-ttu-id="7638b-115">다름</span><span class="sxs-lookup"><span data-stu-id="7638b-115">Different</span></span>|
|[<span data-ttu-id="7638b-116">하나는 Resource Manager, 하나는 클래식</span><span class="sxs-lookup"><span data-stu-id="7638b-116">One Resource Manager, one classic</span></span>](create-peering-different-deployment-models.md) |<span data-ttu-id="7638b-117">동일</span><span class="sxs-lookup"><span data-stu-id="7638b-117">Same</span></span>|

<span data-ttu-id="7638b-118">클래식 배포 모델을 통해 배포된 두 가상 네트워크 간에는 가상 네트워크 피어링을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-118">A virtual network peering cannot be created between two virtual networks deployed through the classic deployment model.</span></span> <span data-ttu-id="7638b-119">가상 네트워크 피어링은 같은 Azure 지역에 있는 두 가상 네트워크 간에만 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-119">A virtual network peering can only be created between two virtual networks that exist in the same Azure region.</span></span> <span data-ttu-id="7638b-120">서로 다른 구독에 존재하는 가상 네트워크 간의 가상 네트워크 피어링을 만들 때는 구독이 모두 동일한 Azure Active Directory 테넌트에 연결되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-120">When creating a virtual network peering between virtual networks that exist in different subscriptions, the subscriptions must both be associated to the same Azure Active Directory tenant.</span></span> <span data-ttu-id="7638b-121">아직 Azure Active Directory 테넌트가 없는 경우 신속히 하나 [만들](../active-directory/develop/active-directory-howto-tenant.md?toc=%2fazure%2fvirtual-network%2ftoc.json#start-from-scratch) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-121">If you don't already have an Azure Active Directory tenant, you can quickly [create one](../active-directory/develop/active-directory-howto-tenant.md?toc=%2fazure%2fvirtual-network%2ftoc.json#start-from-scratch).</span></span> <span data-ttu-id="7638b-122">둘 다 클래식 배포 모델을 통해 생성된 가상 네트워크 또는 서로 다른 Azure 지역에 있는 가상 네트워크를 연결해야 하거나 서로 다른 Azure Active Directory 테넌트에 연결된 구독에 존재하는 경우 Azure [VPN Gateway](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)를 사용하여 가상 네트워크를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-122">If you need to connect virtual networks that were both created through the classic deployment model, or that exist in different Azure regions, or that exist in subscriptions associated to different Azure Active Directory tenants, you can use an Azure [VPN Gateway](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) to connect the virtual networks.</span></span> 

> [!WARNING]
> <span data-ttu-id="7638b-123">서로 다른 Azure 구독에 존재하는 동서로 다른 Azure 배포 모델을 통해 만든 가상 네트워크 간의 가상 네트워크 피어링을 만드는 것은 현재 미리 보기 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-123">Creating a virtual network peering between virtual networks in created through different Azure deployment models that exist in different subscriptions is currently in preview.</span></span> <span data-ttu-id="7638b-124">이 시나리오에서 만든 가상 네트워크 피어링은 일반 가용성 릴리스의 시나리오에서 가상 네트워크 피어링을 만드는 것과는 가용성과 신뢰성의 수준이 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-124">Virtual network peerings created in this scenario may not have the same level of availability and reliability as creating a virtual network peering in scenarios in general availability release.</span></span> <span data-ttu-id="7638b-125">이 시나리오에서 만든 가상 네트워크 피어링은 지원되지 않으며, 기능상의 제약이 있거나, 일부 Azure 지역에서 사용하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-125">Virtual network peerings created in this scenario are not supported, may have constrained capabilities, and may not be available in all Azure regions.</span></span> <span data-ttu-id="7638b-126">이 기능의 가용성 및 상태에 대한 최신 알림을 보려면 [Azure 가상 네트워크 업데이트](https://azure.microsoft.com/updates/?product=virtual-network) 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7638b-126">For the most up-to-date notifications on availability and status of this feature, check the [Azure Virtual Network updates](https://azure.microsoft.com/updates/?product=virtual-network) page.</span></span>

<span data-ttu-id="7638b-127">[Azure Portal](#portal), Azure [CLI(Command Line Interface)](#cli) 또는 Azure [PowerShell](#powershell)을 사용하여 가상 네트워크 피어링을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-127">You can use the [Azure portal](#portal), the Azure [command-line interface](#cli) (CLI), or Azure [PowerShell](#powershell) to create a virtual network peering.</span></span> <span data-ttu-id="7638b-128">앞의 도구 링크 중 원하는 도구 링크를 클릭하여 원하는 도구를 사용하여 가상 네트워크 피어링을 만드는 단계로 바로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="7638b-128">Click any of the previous tool links to go directly to the steps for creating a virtual network peering using your tool of choice.</span></span>

## <span data-ttu-id="7638b-129"><a name="register"></a>미리 보기에 등록 </span><span class="sxs-lookup"><span data-stu-id="7638b-129"><a name="register"></a>Register for the preview</span></span>

<span data-ttu-id="7638b-130">미리 보기에 등록하려면 피어링할 가상 네트워크를 포함하는 두 구독에 대해 다음 절차를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-130">To register for the preview, complete the steps that follow for both subscriptions that contain the virtual networks you want to peer.</span></span> <span data-ttu-id="7638b-131">미리 보기에 등록하는 데는 PowerShell만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-131">The only tool you can use to register for the preview is PowerShell.</span></span>

1. <span data-ttu-id="7638b-132">최신 버전의 PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-132">Install the latest version of the PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="7638b-133">Azure PowerShell을 처음 사용하는 경우 [Azure PowerShell 개요](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7638b-133">If you're new to Azure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="7638b-134">PowerShell 세션을 시작하고 `login-azurermaccount` 명령을 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-134">Start a PowerShell session and log in to Azure using the `login-azurermaccount` command.</span></span>
3. <span data-ttu-id="7638b-135">다음 명령을 입력하여 미리 보기에 해당하는 구독을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-135">Register your subscription for the preview by entering the following commands:</span></span>

    ```powershell
    Register-AzureRmProviderFeature `
      -FeatureName AllowClassicCrossSubscriptionPeering `
      -ProviderNamespace Microsoft.Network
    
    Register-AzureRmResourceProvider `
      -ProviderNamespace Microsoft.Network
    ```
    <span data-ttu-id="7638b-136">두 구독에 대해 모두 다음 명령을 입력하여 받은 **RegistrationState** 출력이 **Registered**가 되기 전까지는 이 문서의 포털, Azure CLI 또는 PowerShell 섹션에 있는 절차를 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-136">Do not complete the steps in the Portal, Azure CLI, or PowerShell sections of this article until the **RegistrationState** output you receive after entering the following command is **Registered** for both subscriptions:</span></span>

    ```powershell    
    Get-AzureRmProviderFeature `
      -FeatureName AllowClassicCrossSubscriptionPeering `
      -ProviderNamespace Microsoft.Network
    ```

## <span data-ttu-id="7638b-137"><a name="portal"></a>피어링 만들기 - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7638b-137"><a name="portal"></a>Create peering - Azure portal</span></span>

<span data-ttu-id="7638b-138">이 자습서에서는 각 구독에 대해 다른 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-138">This tutorial uses different accounts for each subscription.</span></span> <span data-ttu-id="7638b-139">두 구독 모두에 대해 권한이 있는 계정을 사용할 경우 모든 단계에 동일한 계정을 사용하고, 포털 로그아웃 절차와 가상 네트워크에 다른 사용자 권한을 할당하는 절차를 생략할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-139">If you're using an account that has permissions to both subscriptions, you can use the same account for all steps, skip the steps for logging out of the portal, and skip the steps for assigning another user permissions to the virtual networks.</span></span> <span data-ttu-id="7638b-140">다음 단계 중 하나를 완료하기 전에 미리 보기에 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-140">Before completing any of the following steps, you must register for the preview.</span></span> <span data-ttu-id="7638b-141">등록하려면 이 문서의 [미리 보기에 등록](#register) 섹션의 절차를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-141">To register, complete the steps in the [Register for the preview](#register) section of this article.</span></span> <span data-ttu-id="7638b-142">두 구독 모두 미리 보기에 등록되기 전에는 남은 단계를 진행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-142">Do not continue with the remaining steps until both subscriptions are registered for the preview.</span></span>
 
1. <span data-ttu-id="7638b-143">[Azure Portal](https://portal.azure.com)에 사용자 A로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-143">Log in to the [Azure portal](https://portal.azure.com) as UserA.</span></span> <span data-ttu-id="7638b-144">로그인하는 데 사용하는 계정에 가상 네트워크 피어링을 만드는 데 필요한 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-144">The account you log in with must have the necessary permissions to create a virtual network peering.</span></span> <span data-ttu-id="7638b-145">자세한 내용은 이 문서의 [권한](#permissions) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7638b-145">See the [Permissions](#permissions) section of this article for details.</span></span>
2. <span data-ttu-id="7638b-146">**+ 새로 만들기**, **네트워킹**, **가상 네트워크**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-146">Click **+ New**, click **Networking**, then click **Virtual network**.</span></span>
3. <span data-ttu-id="7638b-147">**가상 네트워크 만들기** 블레이드에서 다음 설정에 대한 값을 입력하거나 선택한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-147">In the **Create virtual network** blade, enter, or select values for the following settings, then click **Create**:</span></span>
    - <span data-ttu-id="7638b-148">**이름**: *myVnetA*</span><span class="sxs-lookup"><span data-stu-id="7638b-148">**Name**: *myVnetA*</span></span>
    - <span data-ttu-id="7638b-149">**주소 공간**: *10.0.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="7638b-149">**Address space**: *10.0.0.0/16*</span></span>
    - <span data-ttu-id="7638b-150">**서브넷 이름**: *기본값*</span><span class="sxs-lookup"><span data-stu-id="7638b-150">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="7638b-151">**서브넷 주소 범위**: *10.0.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="7638b-151">**Subnet address range**: *10.0.0.0/24*</span></span>
    - <span data-ttu-id="7638b-152">**구독**: 구독 A를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-152">**Subscription**: Select subscription A.</span></span>
    - <span data-ttu-id="7638b-153">**리소스 그룹**: **새로 만들기**를 선택하고 *myResourceGroupA*를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-153">**Resource group**: Select **Create new** and enter *myResourceGroupA*</span></span>
    - <span data-ttu-id="7638b-154">**위치**: *미국 동부*</span><span class="sxs-lookup"><span data-stu-id="7638b-154">**Location**: *East US*</span></span>
4. <span data-ttu-id="7638b-155">포털 위쪽에 있는 **리소스 검색** 상자에 *myVnetA*를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-155">In the **Search resources** box at the top of the portal, type *myVnetA*.</span></span> <span data-ttu-id="7638b-156">**myVnetA**가 검색 결과에 표시되면 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-156">Click **myVnetA** when it appears in the search results.</span></span> <span data-ttu-id="7638b-157">**myVnetA** 가상 네트워크에 대한 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-157">A blade appears for the **myVnetA** virtual network.</span></span>
5. <span data-ttu-id="7638b-158">나타나는 **myVnetA** 블레이드의 왼쪽에 있는 세로 옵션 목록에서 **액세스 제어(IAM)**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-158">In the **myVnetA** blade that appears, click **Access control (IAM)** from the vertical list of options on the left side of the blade.</span></span>
6. <span data-ttu-id="7638b-159">나타나는 **myVnetA - ID 및 액세스 제어(IAM)** 블레이드에서 **+ 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-159">In the **myVnetA - Access control (IAM)** blade that appears, click **+ Add**.</span></span>
7. <span data-ttu-id="7638b-160">나타나는 **권한 추가** 블레이드의 **역할** 상자에서 **네트워크 참가자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-160">In the **Add permissions** blade that appears, select **Network contributor** in the **Role** box.</span></span>
8. <span data-ttu-id="7638b-161">**선택** 상자에서 사용자 B를 선택하거나 사용자 B의 이메일 주소를 입력하여 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-161">In the **Select** box, select UserB, or type UserB's email address to search for it.</span></span> <span data-ttu-id="7638b-162">피어링을 설정 중인 가상 네트워크와 같은 Azure Active Directory 테넌트의 사용자 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-162">The list of users shown is from the same Azure Active Directory tenant as the virtual network you're setting up the peering for.</span></span> <span data-ttu-id="7638b-163">목록에 표시되면 사용자 B를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-163">Click UserB when it appears in the list.</span></span>
9. <span data-ttu-id="7638b-164">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-164">Click **Save**.</span></span>
10. <span data-ttu-id="7638b-165">사용자 A를 포털에서 로그아웃한 다음 사용자 B로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-165">Log out of the portal as UserA, then log in as UserB.</span></span>
11. <span data-ttu-id="7638b-166">**+ 새로 만들기**를 클릭하고 **Marketplace 검색** 상자에 *가상 네트워크*를 입력한 다음 검색 결과에서 **가상 네트워크**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-166">Click **+ New**, type *Virtual network* in the **Search the Marketplace** box, then click **Virtual network** in the search results.</span></span>
12. <span data-ttu-id="7638b-167">표시되는 **가상 네트워크** 블레이드의 **배포 모델 선택** 상자에서 **클래식**을 선택한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-167">In the **Virtual Network** blade that appears, select **Classic** in the **Select a deployment model** box, then click **Create**.</span></span>
13.   <span data-ttu-id="7638b-168">가상 네트워크 만들기(클래식) 상자가 나타나면 다음 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-168">In the Create virtual network (classic) box that appears, enter the following values:</span></span>

    - <span data-ttu-id="7638b-169">**이름**: *myVnetB*</span><span class="sxs-lookup"><span data-stu-id="7638b-169">**Name**: *myVnetB*</span></span>
    - <span data-ttu-id="7638b-170">**주소 공간**: *10.1.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="7638b-170">**Address space**: *10.1.0.0/16*</span></span>
    - <span data-ttu-id="7638b-171">**서브넷 이름**: *기본값*</span><span class="sxs-lookup"><span data-stu-id="7638b-171">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="7638b-172">**서브넷 주소 범위**: *10.1.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="7638b-172">**Subnet address range**: *10.1.0.0/24*</span></span>
    - <span data-ttu-id="7638b-173">**구독**: 구독 B를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-173">**Subscription**: Select subscription B.</span></span>
    - <span data-ttu-id="7638b-174">**리소스 그룹**: **새로 만들기**를 선택하고 *myResourceGroupB*를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-174">**Resource group**: Select **Create new** and enter *myResourceGroupB*</span></span>
    - <span data-ttu-id="7638b-175">**위치**: *미국 동부*</span><span class="sxs-lookup"><span data-stu-id="7638b-175">**Location**: *East US*</span></span>

14. <span data-ttu-id="7638b-176">포털 위쪽에 있는 **리소스 검색** 상자에 *myVnetB*를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-176">In the **Search resources** box at the top of the portal, type *myVnetB*.</span></span> <span data-ttu-id="7638b-177">**myVnetB**가 검색 결과에 표시되면 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-177">Click **myVnetB** when it appears in the search results.</span></span> <span data-ttu-id="7638b-178">**myVnetB** 가상 네트워크에 대한 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-178">A blade appears for the **myVnetB** virtual network.</span></span>
15. <span data-ttu-id="7638b-179">나타나는 **myVnetB** 블레이드의 왼쪽에 있는 세로 옵션 목록에서 **속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-179">In the **myVnetB** blade that appears, click **Properties** from the vertical list of options on the left side of the blade.</span></span> <span data-ttu-id="7638b-180">이후의 단계에서 사용하는**RESOURCE ID**를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-180">Copy the **RESOURCE ID**, which is used in a later step.</span></span> <span data-ttu-id="7638b-181">리소스 ID는 /subscriptions/<Susbscription ID>/resourceGroups/myResoureGroupB/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-181">The resource ID is similar to the following example: /subscriptions/<Susbscription ID>/resourceGroups/myResoureGroupB/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB</span></span>
16. <span data-ttu-id="7638b-182">MyVnetB에 대해 5-9단계를 완료하고 8단계에서 **사용자 A**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-182">Complete steps 5-9 for myVnetB, entering **UserA** in step 8.</span></span>
17. <span data-ttu-id="7638b-183">사용자 B를 포털에서 로그아웃한 다음 사용자 A로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-183">Log out of the portal as UserB and log in as UserA.</span></span>
18. <span data-ttu-id="7638b-184">포털 위쪽에 있는 **리소스 검색** 상자에 *myVnetA*를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-184">In the **Search resources** box at the top of the portal, type *myVnetA*.</span></span> <span data-ttu-id="7638b-185">**myVnetA**가 검색 결과에 표시되면 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-185">Click **myVnetA** when it appears in the search results.</span></span> <span data-ttu-id="7638b-186">**myVnet** 가상 네트워크에 대한 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-186">A blade appears for the **myVnet** virtual network.</span></span>
19. <span data-ttu-id="7638b-187">**myVnetA**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-187">Click **myVnetA**.</span></span>
20. <span data-ttu-id="7638b-188">나타나는 **myVnetA** 블레이드의 왼쪽에 있는 세로 옵션 목록에서 **피어링**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-188">In the **myVnetA** blade that appears, click **Peerings** from the vertical list of options on the left side of the blade.</span></span>
21. <span data-ttu-id="7638b-189">나타난 **myVnetA - 피어링** 블레이드에서 **+ 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-189">In the **myVnetA - Peerings** blade that appeared, click **+ Add**</span></span>
22. <span data-ttu-id="7638b-190">나타나는 **피어링 추가** 블레이드에서 다음 옵션을 입력하거나 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-190">In the **Add peering** blade that appears, enter, or select the following options, then click **OK**:</span></span>
     - <span data-ttu-id="7638b-191">**이름**: *myVnetAToMyVnetB*</span><span class="sxs-lookup"><span data-stu-id="7638b-191">**Name**: *myVnetAToMyVnetB*</span></span>
     - <span data-ttu-id="7638b-192">**가상 네트워크 배포 모델**: **클래식**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-192">**Virtual network deployment model**:  Select **Classic**.</span></span>
     - <span data-ttu-id="7638b-193">**리소스 ID를 알고 있음**: 이 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-193">**I know my resource ID**: Check this box.</span></span>
     - <span data-ttu-id="7638b-194">**리소스 ID**: 15단계에서 얻은 myVnetB의 리소스 ID를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-194">**Resource ID**: Enter the resource ID of myVnetB from step 15.</span></span>
     - <span data-ttu-id="7638b-195">**가상 네트워크 액세스 허용:** **사용**이 선택되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-195">**Allow virtual network access:** Ensure that **Enabled** is selected.</span></span>
    <span data-ttu-id="7638b-196">이 자습서에서 다른 설정은 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-196">No other settings are used in this tutorial.</span></span> <span data-ttu-id="7638b-197">모든 피어링 설정에 대해 알아보려면 [가상 네트워크 피어링 관리](virtual-network-manage-peering.md#create-a-peering)를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="7638b-197">To learn about all peering settings, read [Manage virtual network peerings](virtual-network-manage-peering.md#create-a-peering).</span></span>
23. <span data-ttu-id="7638b-198">이전 단계에서 **확인**을 클릭한 후 **피어링 추가** 블레이드가 닫히고 **myVnetA - 피어링** 블레이드가 다시 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-198">After clicking **OK** in the previous step, the **Add peering** blade closes and you see the **myVnetA - Peerings** blade again.</span></span> <span data-ttu-id="7638b-199">몇 초 후 만든 피어링이 블레이드에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-199">After a few seconds, the peering you created appears in the blade.</span></span> <span data-ttu-id="7638b-200">만든 **myVnetAToMyVnetB** 피어링에 대해 **PEERING STATUS** 열에 **Connected**가 열거됩니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-200">**Connected** is listed in the **PEERING STATUS** column for the **myVnetAToMyVnetB** peering you created.</span></span> <span data-ttu-id="7638b-201">이제 피어링이 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-201">The peering is now established.</span></span> <span data-ttu-id="7638b-202">가상 네트워크(리소스 관리자)에 가상 네트워크(클래식)를 피어링할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-202">There is no need to peer the virtual network (classic) to the virtual network (Resource Manager).</span></span>

    <span data-ttu-id="7638b-203">어느 쪽 가상 네트워크에서든 만든 모든 Azure 리소스는 이제 해당 IP 주소를 통해 서로 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-203">Any Azure resources you create in either virtual network are now able to communicate with each other through their IP addresses.</span></span> <span data-ttu-id="7638b-204">가상 네트워크에 대해 기본 Azure 이름 확인을 사용 중인 경우 가상 네트워크의 리소스가 가상 네트워크에서 이름을 확인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-204">If you're using default Azure name resolution for the virtual networks, the resources in the virtual networks are not able to resolve names across the virtual networks.</span></span> <span data-ttu-id="7638b-205">피어링의 가상 네트워크에서 이름을 확인하려면 자체 DNS 서버를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-205">If you want to resolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="7638b-206">[자체 DNS 서버를 이용한 이름 확인](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) 설정 방법을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="7638b-206">Learn how to set up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

24. <span data-ttu-id="7638b-207">**선택 사항**: 이 자습서에서 가상 컴퓨터를 만드는 내용은 다루지 않지만, 각 가상 네트워크에서 가상 컴퓨터를 만들고 한 가상 컴퓨터에서 다른 가상 컴퓨터로 연결하여 연결의 유효성을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-207">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine to the other, to validate connectivity.</span></span>
25. <span data-ttu-id="7638b-208">**선택 사항**: 이 자습서에서 만든 리소스를 삭제하려면 이 문서의 [리소스 삭제](#delete-portal) 섹션에서 설명하는 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-208">**Optional**: To delete the resources that you create in this tutorial, complete the steps in the [Delete resources](#delete-portal) section of this article.</span></span>

## <span data-ttu-id="7638b-209"><a name="cli"></a>피어링 만들기 - Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7638b-209"><a name="cli"></a>Create peering - Azure CLI</span></span>

<span data-ttu-id="7638b-210">이 자습서에서는 각 구독에 대해 다른 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-210">This tutorial uses different accounts for each subscription.</span></span> <span data-ttu-id="7638b-211">두 구독 모두에 대해 권한이 있는 계정을 사용할 경우 모든 단계에 동일한 계정을 사용하고, Azure 로그아웃 절차를 생략하며 사용자 역할 할당을 만드는 스크립트 줄을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-211">If you're using an account that has permissions to both subscriptions, you can use the same account for all steps, skip the steps for logging out of Azure, and remove the lines of script that create user role assignments.</span></span> <span data-ttu-id="7638b-212">다음 스크립트 전체에서 UserA@azure.com 및 UserB@azure.com은 사용자 A와 사용자 B에 사용하는 사용자 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-212">Replace UserA@azure.com and UserB@azure.com in all of the following scripts with the usernames you're using for UserA and UserB.</span></span> 

<span data-ttu-id="7638b-213">다음 단계 중 하나를 완료하기 전에 미리 보기에 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-213">Before completing any of the following steps, you must register for the preview.</span></span> <span data-ttu-id="7638b-214">등록하려면 이 문서의 [미리 보기에 등록](#register) 섹션의 절차를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-214">To register, complete the steps in the [Register for the preview](#register) section of this article.</span></span> <span data-ttu-id="7638b-215">두 구독 모두 미리 보기에 등록되기 전에는 남은 단계를 진행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-215">Do not continue with the remaining steps until both subscriptions are registered for the preview.</span></span>

1. <span data-ttu-id="7638b-216">가상 네트워크(클래식)를 만들려면 Azure CLI 1.0을 [설치](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-216">[Install](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) the Azure CLI 1.0 to create the virtual network (classic).</span></span>
2. <span data-ttu-id="7638b-217">CLI 세션을 열고 `azure login` 명령을 사용하여 사용자 B로 Azure에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-217">Open a CLI session and log in to Azure as UserB using the `azure login` command.</span></span>
3. <span data-ttu-id="7638b-218">`azure config mode asm` 명령을 입력하여 CLI를 서비스 관리 모드에서 실행합니다. </span><span class="sxs-lookup"><span data-stu-id="7638b-218">Run the CLI in Service Management mode by entering the `azure config mode asm` command.</span></span>
4. <span data-ttu-id="7638b-219">다음 명령을 입력하여 가상 네트워크(클래식)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-219">Enter the following command to create the virtual network (classic):</span></span>
 
    ```azurecli
    azure network vnet create --vnet myVnetB --address-space 10.1.0.0 --cidr 16 --location "East US"
    ```
5. <span data-ttu-id="7638b-220">나머지 단계는 Azure CLI 2.0.4 이상이 [설치된](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json) Bash 셸이나 Azure Cloud Shell을 사용하여 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-220">The remaining steps must be completed using a bash shell with the Azure CLI 2.0.4 or later [installed](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json), or by using the Azure Cloud Shell.</span></span> <span data-ttu-id="7638b-221">Azure Cloud Shell은 Azure Portal에서 직접 실행할 수 있는 평가판 Bash 셸입니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-221">The Azure Cloud Shell is a free Bash shell that you can run directly within the Azure portal.</span></span> <span data-ttu-id="7638b-222">Azure CLI가 사전 설치되어 계정에서 사용하도록 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-222">It has the Azure CLI preinstalled and configured to use with your account.</span></span> <span data-ttu-id="7638b-223">다음 스크립트에서 **사용해보기** 단추를 클릭하면 Azure 계정에 로그인하는 Cloud Shell이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-223">Click the **Try it** button in the scripts that follow, which opens a Cloud Shell that logs you in to your Azure account.</span></span> <span data-ttu-id="7638b-224">Windows 클라이언트에서 Bash CLI 스크립트 실행과 관련된 옵션은 [Windows에서 Azure CLI 실행](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7638b-224">For options on running bash CLI scripts on a Windows client, see [Running the Azure CLI in Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> 
6. <span data-ttu-id="7638b-225">PC의 텍스트 편집기에 다음 스크립트를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-225">Copy the following script to a text editor on your PC.</span></span> <span data-ttu-id="7638b-226">`<SubscriptionB-Id>`는 구독 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-226">Replace `<SubscriptionB-Id>` with your subscription ID.</span></span> <span data-ttu-id="7638b-227">구독 ID를 모르는 경우 `az account show` 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-227">If you don't know your subscription Id, enter the `az account show` command.</span></span> <span data-ttu-id="7638b-228">출력에 표시되는 **id** 값이 구독 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-228">The value for **id** in the output is your subscription Id.</span></span> <span data-ttu-id="7638b-229">수정된 스크립트를 복사하여 CLI 2.0 세션에 붙여 넣고 `Enter`를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-229">Copy the modified script, paste it in to your CLI 2.0 session, and then press `Enter`.</span></span> 

    ```azurecli-interactive
    az role assignment create \
      --assignee UserA@azure.com \
      --role "Classic Network Contributor" \
      --scope /subscriptions/<SubscriptionB-Id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

    <span data-ttu-id="7638b-230">4단계에서 가상 네트워크(클래식)를 만들었을 때 Azure는 *Default-Networking* 리소스 그룹에 가상 네트워크를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-230">When you created the virtual network (classic) in step 4, Azure created the virtual network in the *Default-Networking* resource group.</span></span>
7. <span data-ttu-id="7638b-231">Azure에서 사용자 B를 로그아웃하고 CLI 2.0에 사용자 A로 로그인합니다. </span><span class="sxs-lookup"><span data-stu-id="7638b-231">Log UserB out of Azure and log in as UserA in the CLI 2.0.</span></span>
8. <span data-ttu-id="7638b-232">리소스 그룹 및 가상 네트워크(리소스 관리자)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-232">Create a resource group and a virtual network (Resource Manager).</span></span> <span data-ttu-id="7638b-233">다음 스크립트를 복사하여 CLI 세션에 붙여 넣고 `Enter`를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-233">Copy the following script, paste it in to your CLI session, and then press `Enter`.</span></span> 

    ```azurecli-interactive
    #!/bin/bash

    # Variables for common values used throughout the script.
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

    # Get the id for myVnetA.
    vNetAId=$(az network vnet show \
      --resource-group $rgName \
      --name myVnetA \
      --query id --out tsv)

    # Assign UserB permissions to myVnetA.
    az role assignment create \
      --assignee UserB@azure.com \
      --role "Network Contributor" \
      --scope $vNetAId
    ```

9. <span data-ttu-id="7638b-234">서로 다른 배포 모델을 통해 만들어진 두 가상 네트워크 사이에 가상 네트워크 피어링을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-234">Create a virtual network peering between the two virtual networks created through the different deployment models.</span></span> <span data-ttu-id="7638b-235">PC의 텍스트 편집기에 다음 스크립트를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-235">Copy the following script to a text editor on your PC.</span></span> <span data-ttu-id="7638b-236">`<SubscriptionB-id>`는 구독 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-236">Replace `<SubscriptionB-id>` with your subscription Id.</span></span> <span data-ttu-id="7638b-237">구독 ID를 모르는 경우 `az account show` 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-237">If you don't know your subscription Id, enter the `az account show` command.</span></span> <span data-ttu-id="7638b-238">출력에 표시되는 **id** 값이 구독 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-238">The value for **id** in the output is your subscription Id.</span></span> <span data-ttu-id="7638b-239">Azure는 이름이 *Default-Networking*인 리소스 그룹에 4단계에서 만든 가상 네트워크(클래식)를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-239">Azure created the virtual network (classic) you created in step 4 in a resource group named *Default-Networking*.</span></span> <span data-ttu-id="7638b-240">CLI 세션에 수정된 스크립트를 붙여 넣고 `Enter`를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-240">Paste the modified script in your CLI session, and then press `Enter`.</span></span>

    ```azurecli-interactive
    # Peer VNet1 to VNet2.
    az network vnet peering create \
      --name myVnetAToMyVnetB \
      --resource-group $rgName \
      --vnet-name myVnetA \
      --remote-vnet-id  /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB \
      --allow-vnet-access
    ```

10. <span data-ttu-id="7638b-241">스크립트를 실행한 후 가상 네트워크에 대한 피어링을 검토합니다(리소스 관리자).</span><span class="sxs-lookup"><span data-stu-id="7638b-241">After the script executes, review the peering for the virtual network (Resource Manager).</span></span> <span data-ttu-id="7638b-242">다음 스크립트를 복사하여 CLI 세션에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-242">Copy the following script, and then paste it in your CLI session:</span></span>

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group $rgName \
      --vnet-name myVnetA \
      --output table
    ```
    <span data-ttu-id="7638b-243">출력에서 **PeeringState** 열에 **Connected**가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-243">The output shows **Connected** in the **PeeringState** column.</span></span>

    <span data-ttu-id="7638b-244">어느 쪽 가상 네트워크에서든 만든 모든 Azure 리소스는 이제 해당 IP 주소를 통해 서로 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-244">Any Azure resources you create in either virtual network are now able to communicate with each other through their IP addresses.</span></span> <span data-ttu-id="7638b-245">가상 네트워크에 대해 기본 Azure 이름 확인을 사용 중인 경우 가상 네트워크의 리소스가 가상 네트워크에서 이름을 확인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-245">If you're using default Azure name resolution for the virtual networks, the resources in the virtual networks are not able to resolve names across the virtual networks.</span></span> <span data-ttu-id="7638b-246">피어링의 가상 네트워크에서 이름을 확인하려면 자체 DNS 서버를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-246">If you want to resolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="7638b-247">[자체 DNS 서버를 이용한 이름 확인](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) 설정 방법을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="7638b-247">Learn how to set up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

11. <span data-ttu-id="7638b-248">**선택 사항**: 이 자습서에서 가상 컴퓨터를 만드는 내용은 다루지 않지만, 각 가상 네트워크에서 가상 컴퓨터를 만들고 한 가상 컴퓨터에서 다른 가상 컴퓨터로 연결하여 연결의 유효성을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-248">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine to the other, to validate connectivity.</span></span>
12. <span data-ttu-id="7638b-249">**선택 사항**: 이 자습서에서 만든 리소스를 삭제하려면 이 문서의 [리소스 삭제](#delete-cli)에서 설명하는 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-249">**Optional**: To delete the resources that you create in this tutorial, complete the steps in [Delete resources](#delete-cli) in this article.</span></span>

## <span data-ttu-id="7638b-250"><a name="powershell"></a>피어링 만들기 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="7638b-250"><a name="powershell"></a>Create peering - PowerShell</span></span>

<span data-ttu-id="7638b-251">이 자습서에서는 각 구독에 대해 다른 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-251">This tutorial uses different accounts for each subscription.</span></span> <span data-ttu-id="7638b-252">두 구독 모두에 대해 권한이 있는 계정을 사용할 경우 모든 단계에 동일한 계정을 사용하고, Azure 로그아웃 절차를 생략하며 사용자 역할 할당을 만드는 스크립트 줄을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-252">If you're using an account that has permissions to both subscriptions, you can use the same account for all steps, skip the steps for logging out of Azure, and remove the lines of script that create user role assignments.</span></span> <span data-ttu-id="7638b-253">다음 스크립트 전체에서 UserA@azure.com 및 UserB@azure.com은 사용자 A와 사용자 B에 사용하는 사용자 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-253">Replace UserA@azure.com and UserB@azure.com in all of the following scripts with the usernames you're using for UserA and UserB.</span></span> 

<span data-ttu-id="7638b-254">다음 단계 중 하나를 완료하기 전에 미리 보기에 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-254">Before completing any of the following steps, you must register for the preview.</span></span> <span data-ttu-id="7638b-255">등록하려면 이 문서의 [미리 보기에 등록](#register) 섹션의 절차를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-255">To register, complete the steps in the [Register for the preview](#register) section of this article.</span></span> <span data-ttu-id="7638b-256">두 구독 모두 미리 보기에 등록되기 전에는 남은 단계를 진행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-256">Do not continue with the remaining steps until both subscriptions are registered for the preview.</span></span>

1. <span data-ttu-id="7638b-257">최신 버전의 PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) 및 [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-257">Install the latest version of the PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) and [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modules.</span></span> <span data-ttu-id="7638b-258">Azure PowerShell을 처음 사용하는 경우 [Azure PowerShell 개요](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7638b-258">If you're new to Azure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="7638b-259">PowerShell 세션을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-259">Start a PowerShell session.</span></span>
3. <span data-ttu-id="7638b-260">PowerShell에서 `Add-AzureAccount` 명령을 입력하여 사용자 B의 구독에 사용자 B로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-260">In PowerShell, log in to UserB's subscription as UserB by entering the `Add-AzureAccount` command.</span></span>
4. <span data-ttu-id="7638b-261">PowerShell에 가상 네트워크(클래식)를 만들려면 기존 네트워크 구성 파일을 새로 만들거나 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-261">To create a virtual network (classic) with PowerShell, you must create a new, or modify an existing, network configuration file.</span></span> <span data-ttu-id="7638b-262">[네트워크 구성 파일 내보내기, 업데이트 및 가져오기](virtual-networks-using-network-configuration-file.md) 방법을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-262">Learn how to [export, update, and import network configuration files](virtual-networks-using-network-configuration-file.md).</span></span> <span data-ttu-id="7638b-263">파일에는 이 자습서에서 사용되는 가상 네트워크에 대한 **VirtualNetworkSite** 요소가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-263">The file should include the following **VirtualNetworkSite** element for the virtual network used in this tutorial:</span></span>

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
    > <span data-ttu-id="7638b-264">변경된 네트워크 구성 파일을 가져오면 구독의 기존 가상 네트워크(클래식)에 변경을 초래할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-264">Importing a changed network configuration file can cause changes to existing virtual networks (classic) in your subscription.</span></span> <span data-ttu-id="7638b-265">이전 가상 네트워크만 추가하고, 구독에서 기존 가상 네트워크를 변경하거나 제거하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-265">Ensure you only add the previous virtual network and that you don't change or remove any existing virtual networks from your subscription.</span></span> 

5. <span data-ttu-id="7638b-266">`login-azurermaccount` 명령을 입력하여, 리소스 관리자 명령을 사용하기 위해 사용자 B로 사용자 B의 구독에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-266">Log in to UserB's subscription as UserB to use Resource Manager commands by entering the `login-azurermaccount` command.</span></span>
6. <span data-ttu-id="7638b-267">사용자 A 권한을 가상 네트워크 B에 할당합니다. 다음 스크립트를 복사하여 PC의 텍스트 편집기에 붙여 넣고 `<SubscriptionB-id>`는 구독 B의 ID로 교체합니다. 구독 ID를 모를 경우 `Get-AzureRmSubscription` 명령을 입력하여 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-267">Assign UserA permissions to virtual network B. Copy the following script to a text editor on your PC and replace `<SubscriptionB-id>` with the ID of subscription B. If you don't know the subscription Id, enter the `Get-AzureRmSubscription` command to view it.</span></span> <span data-ttu-id="7638b-268">반환된 출력의 **ID** 값이 구독 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-268">The value for **Id** in the returned output is your subscription ID.</span></span> <span data-ttu-id="7638b-269">Azure는 이름이 *Default-Networking*인 리소스 그룹에 4단계에서 만든 가상 네트워크(클래식)를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-269">Azure created the virtual network (classic) you created in step 4 in a resource group named *Default-Networking*.</span></span> <span data-ttu-id="7638b-270">스크립트를 실행하려면 수정된 스크립트를 복사하여 PowerShell에 붙여 넣은 다음 `Enter`를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-270">To execute the script, copy the modified script, paste it in to PowerShell, and then press `Enter`.</span></span>
    
    ```powershell 
    New-AzureRmRoleAssignment `
      -SignInName UserA@azure.com `
      -RoleDefinitionName "Classic Network Contributor" `
      -Scope /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

7. <span data-ttu-id="7638b-271">사용자 B로 Azure에서 로그아웃하고 `login-azurermaccount` 명령을 입력하여 사용자 A의 구독에 사용자 A로 로그인합니다. </span><span class="sxs-lookup"><span data-stu-id="7638b-271">Log out of Azure as UserB and log in to UserA's subscription as UserA by entering the `login-azurermaccount` command.</span></span> <span data-ttu-id="7638b-272">로그인하는 데 사용하는 계정에 가상 네트워크 피어링을 만드는 데 필요한 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-272">The account you log in with must have the necessary permissions to create a virtual network peering.</span></span> <span data-ttu-id="7638b-273">자세한 내용은 이 문서의 [권한](#permissions) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7638b-273">See the [Permissions](#permissions) section of this article for details.</span></span>
8. <span data-ttu-id="7638b-274">다음 스크립트를 복사하여 PowerShell에 붙여 넣은 다음 `Enter`를 눌러 가상 네트워크(리소스 관리자)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-274">Create the virtual network (Resource Manager) by copying the following script, pasting it in to PowerShell, and then pressing `Enter`:</span></span>

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

9. <span data-ttu-id="7638b-275">MyVnetA에 사용자 B 권한을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-275">Assign UserB permissions to myVnetA.</span></span> <span data-ttu-id="7638b-276">다음 스크립트를 복사하여 PC의 텍스트 편집기에 붙여 넣고 `<SubscriptionA-Id>`는 구독 A의 ID로 교체합니다. 구독 ID를 모를 경우 `Get-AzureRmSubscription` 명령을 입력하여 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-276">Copy the following script to a text editor on your PC and replace `<SubscriptionA-Id>` with the ID of subscription A. If you don't know the subscription Id, enter the `Get-AzureRmSubscription` command to view it.</span></span> <span data-ttu-id="7638b-277">반환된 출력의 **ID** 값이 구독 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-277">The value for **Id** in the returned output is your subscription ID.</span></span> <span data-ttu-id="7638b-278">PowerShell에서 스크립트의 수정된 버전을 붙여 넣은 다음 `Enter`를 눌러 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-278">Paste the modified version of the script in PowerShell, and then press `Enter` to execute it.</span></span>

    ```powershell
    New-AzureRmRoleAssignment `
      -SignInName UserB@azure.com `
      -RoleDefinitionName "Network Contributor" `
      -Scope /subscriptions/<SubscriptionA-Id>/resourceGroups/myResourceGroupA/providers/Microsoft.Network/VirtualNetworks/myVnetA
    ```

10. <span data-ttu-id="7638b-279">다음 스크립트를 PC의 텍스트 편집기에 복사하고 `<SubscriptionB-id>`는 구독 B의 ID로 교체합니다. myVnetA를 myVNetB와 피어링하기 위해 수정된 스크립트를 복사하여 PowerShell에 붙여 넣은 다음 `Enter`를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-279">Copy the following script to a text editor on your PC, and replace `<SubscriptionB-id>` with the ID of subscription B. To peer myVnetA to myVNetB, copy the modified script, paste it in to PowerShell, and then press `Enter`.</span></span>

    ```powershell
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnetAToMyVnetB' `
      -VirtualNetwork $vnetA `
      -RemoteVirtualNetworkId /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

11. <span data-ttu-id="7638b-280">다음 스크립트를 복사하고 PowerShell에 붙여 넣은 다음 `Enter`를 눌러 myVnetA의 피어링 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-280">View the peering state of myVnetA by copying the following script, pasting it into PowerShell, and pressing `Enter`.</span></span>

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName $rgName `
      -VirtualNetworkName myVnetA `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    <span data-ttu-id="7638b-281">상태는 **Connected**입니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-281">The state is **Connected**.</span></span> <span data-ttu-id="7638b-282">myVnetB로부터 myVnetA로의 피어링을 설정한 뒤 **Connected**로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-282">It changes to **Connected** once you setup the peering to myVnetA from myVnetB.</span></span>

    <span data-ttu-id="7638b-283">어느 쪽 가상 네트워크에서든 만든 모든 Azure 리소스는 이제 해당 IP 주소를 통해 서로 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-283">Any Azure resources you create in either virtual network are now able to communicate with each other through their IP addresses.</span></span> <span data-ttu-id="7638b-284">가상 네트워크에 대해 기본 Azure 이름 확인을 사용 중인 경우 가상 네트워크의 리소스가 가상 네트워크에서 이름을 확인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-284">If you're using default Azure name resolution for the virtual networks, the resources in the virtual networks are not able to resolve names across the virtual networks.</span></span> <span data-ttu-id="7638b-285">피어링의 가상 네트워크에서 이름을 확인하려면 자체 DNS 서버를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-285">If you want to resolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="7638b-286">[자체 DNS 서버를 이용한 이름 확인](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) 설정 방법을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="7638b-286">Learn how to set up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

12. <span data-ttu-id="7638b-287">**선택 사항**: 이 자습서에서 가상 컴퓨터를 만드는 내용은 다루지 않지만, 각 가상 네트워크에서 가상 컴퓨터를 만들고 한 가상 컴퓨터에서 다른 가상 컴퓨터로 연결하여 연결의 유효성을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-287">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine to the other, to validate connectivity.</span></span>
13. <span data-ttu-id="7638b-288">**선택 사항**: 이 자습서에서 만든 리소스를 삭제하려면 이 문서의 [리소스 삭제](#delete-powershell)에서 설명하는 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-288">**Optional**: To delete the resources that you create in this tutorial, complete the steps in [Delete resources](#delete-powershell) in this article.</span></span>

## <span data-ttu-id="7638b-289"><a name="permissions"></a>권한</span><span class="sxs-lookup"><span data-stu-id="7638b-289"><a name="permissions"></a>Permissions</span></span>

<span data-ttu-id="7638b-290">가상 네트워크 피어링을 만드는 데 사용하는 계정에 필요한 역할 또는 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-290">The accounts you use to create a virtual network peering must have the necessary role or permissions.</span></span> <span data-ttu-id="7638b-291">예를 들어 이름이 myVnetA와 myVnetB인 두 가상 네트워크를 피어링하는 경우 계정에는 각 가상 네트워크에 대한 다음과 같은 최소 역할 또는 권한이 할당되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-291">For example, if you were peering two virtual networks named myVnetA and myVnetB, your account must be assigned the following minimum role or permissions for each virtual network:</span></span>
    
|<span data-ttu-id="7638b-292">가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="7638b-292">Virtual network</span></span>|<span data-ttu-id="7638b-293">배포 모델</span><span class="sxs-lookup"><span data-stu-id="7638b-293">Deployment model</span></span>|<span data-ttu-id="7638b-294">역할</span><span class="sxs-lookup"><span data-stu-id="7638b-294">Role</span></span>|<span data-ttu-id="7638b-295">권한</span><span class="sxs-lookup"><span data-stu-id="7638b-295">Permissions</span></span>|
|---|---|---|---|
|<span data-ttu-id="7638b-296">myVnetA</span><span class="sxs-lookup"><span data-stu-id="7638b-296">myVnetA</span></span>|<span data-ttu-id="7638b-297">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="7638b-297">Resource Manager</span></span>|[<span data-ttu-id="7638b-298">네트워크 참여자</span><span class="sxs-lookup"><span data-stu-id="7638b-298">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="7638b-299">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span><span class="sxs-lookup"><span data-stu-id="7638b-299">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span></span>|
| |<span data-ttu-id="7638b-300">클래식</span><span class="sxs-lookup"><span data-stu-id="7638b-300">Classic</span></span>|[<span data-ttu-id="7638b-301">클래식 네트워크 참여자</span><span class="sxs-lookup"><span data-stu-id="7638b-301">Classic Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|<span data-ttu-id="7638b-302">해당 없음</span><span class="sxs-lookup"><span data-stu-id="7638b-302">N/A</span></span>|
|<span data-ttu-id="7638b-303">myVnetB</span><span class="sxs-lookup"><span data-stu-id="7638b-303">myVnetB</span></span>|<span data-ttu-id="7638b-304">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="7638b-304">Resource Manager</span></span>|[<span data-ttu-id="7638b-305">네트워크 참여자</span><span class="sxs-lookup"><span data-stu-id="7638b-305">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="7638b-306">Microsoft.Network/virtualNetworks/peer</span><span class="sxs-lookup"><span data-stu-id="7638b-306">Microsoft.Network/virtualNetworks/peer</span></span>|
||<span data-ttu-id="7638b-307">클래식</span><span class="sxs-lookup"><span data-stu-id="7638b-307">Classic</span></span>|[<span data-ttu-id="7638b-308">클래식 네트워크 참여자</span><span class="sxs-lookup"><span data-stu-id="7638b-308">Classic Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|<span data-ttu-id="7638b-309">Microsoft.ClassicNetwork/virtualNetworks/peer</span><span class="sxs-lookup"><span data-stu-id="7638b-309">Microsoft.ClassicNetwork/virtualNetworks/peer</span></span>|

<span data-ttu-id="7638b-310">[기본 제공 역할](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) 및 [사용자 지정 역할](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json)에 특정 권한 할당(Resource Manager만 해당)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="7638b-310">Learn more about [built-in roles](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) and assigning specific permissions to [custom roles](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (Resource Manager only).</span></span>

## <span data-ttu-id="7638b-311"><a name="delete"></a>리소스 삭제</span><span class="sxs-lookup"><span data-stu-id="7638b-311"><a name="delete"></a>Delete resources</span></span>
<span data-ttu-id="7638b-312">이 자습서를 마친 경우 사용 요금이 발생하지 않도록 자습서에서 만든 리소스를 삭제하려고 할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-312">When you've finished this tutorial, you might want to delete the resources you created in the tutorial, so you don't incur usage charges.</span></span> <span data-ttu-id="7638b-313">리소스 그룹을 삭제하면 리소스 그룹에 있는 리소스도 모두 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-313">Deleting a resource group also deletes all resources that are in the resource group.</span></span>

### <span data-ttu-id="7638b-314"><a name="delete-portal"></a>Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7638b-314"><a name="delete-portal"></a>Azure portal</span></span>

1. <span data-ttu-id="7638b-315">포털 검색 상자에 **myResourceGroupA**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-315">In the portal search box, enter **myResourceGroupA**.</span></span> <span data-ttu-id="7638b-316">검색 결과에서 **myResourceGroupA**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-316">In the search results, click **myResourceGroupA**.</span></span>
2. <span data-ttu-id="7638b-317">**myResourceGroupA** 블레이드에서 **삭제** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-317">On the **myResourceGroupA** blade, click the **Delete** icon.</span></span>
3. <span data-ttu-id="7638b-318">삭제를 확인하려면 **TYPE THE RESOURCE GROUP NAME** 상자에 **myResourceGroupA**를 입력한 다음 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-318">To confirm the deletion, in the **TYPE THE RESOURCE GROUP NAME** box, enter **myResourceGroupA**, and then click **Delete**.</span></span>
4. <span data-ttu-id="7638b-319">포털 위쪽에 있는 **리소스 검색** 상자에 *myVnetB*를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-319">In the **Search resources** box at the top of the portal, type *myVnetB*.</span></span> <span data-ttu-id="7638b-320">**myVnetB**가 검색 결과에 표시되면 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-320">Click **myVnetB** when it appears in the search results.</span></span> <span data-ttu-id="7638b-321">**myVnetB** 가상 네트워크에 대한 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-321">A blade appears for the **myVnetB** virtual network.</span></span>
5. <span data-ttu-id="7638b-322">**myVnetB** 블레이드에서 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-322">In the **myVnetB** blade, click **Delete**.</span></span>
6. <span data-ttu-id="7638b-323">삭제를 확인하려면 **가상 네트워크 삭제** 상자에서 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-323">To confirm the deletion, click **Yes** in the **Delete virtual network** box.</span></span>

### <span data-ttu-id="7638b-324"><a name="delete-cli"></a>Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7638b-324"><a name="delete-cli"></a>Azure CLI</span></span>

1. <span data-ttu-id="7638b-325">가상 네트워크(리소스 관리자)를 삭제하기 위해 다음 명령을 통해 CLI 2.0을 사용하여 Azure에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-325">Log in to Azure using the CLI 2.0 to delete the virtual network (Resource Manager) with the following command:</span></span>

    ```azurecli-interactive
    az group delete --name myResourceGroupA --yes
    ```

2. <span data-ttu-id="7638b-326">가상 네트워크(클래식)를 삭제하기 위해 다음 명령을 통해 Azure CLI 1.0을 사용하여 Azure에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-326">Log in to Azure using the Azure CLI 1.0 to delete the virtual network (classic) with the following commands:</span></span>

    ```azurecli
    azure config mode asm 

    azure network vnet delete --vnet myVnetB --quiet
    ```

### <span data-ttu-id="7638b-327"><a name="delete-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="7638b-327"><a name="delete-powershell"></a>PowerShell</span></span>

1. <span data-ttu-id="7638b-328">PowerShell 명령 프롬프트에서 다음 명령을 입력하여 가상 네트워크(리소스 관리자)를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-328">At the PowerShell command prompt, enter the following command to delete the virtual network (Resource Manager):</span></span>

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroupA -Force
    ```

2. <span data-ttu-id="7638b-329">PowerShell을 통해 가상 네트워크(클래식)를 삭제하려면 기존 네트워크 구성 파일을 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-329">To delete the virtual network (classic) with PowerShell, you must modify an existing network configuration file.</span></span> <span data-ttu-id="7638b-330">[네트워크 구성 파일 내보내기, 업데이트 및 가져오기](virtual-networks-using-network-configuration-file.md) 방법을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-330">Learn how to [export, update, and import network configuration files](virtual-networks-using-network-configuration-file.md).</span></span> <span data-ttu-id="7638b-331">이 자습서에서 사용되는 가상 네트워크에 대한 다음 VirtualNetworkSite 요소를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-331">Remove the following VirtualNetworkSite element for the virtual network used in this tutorial:</span></span>

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
    > <span data-ttu-id="7638b-332">변경된 네트워크 구성 파일을 가져오면 구독의 기존 가상 네트워크(클래식)에 변경을 초래할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-332">Importing a changed network configuration file can cause changes to existing virtual networks (classic) in your subscription.</span></span> <span data-ttu-id="7638b-333">이전 가상 네트워크만 제거하고, 구독에서 다른 기존 가상 네트워크를 변경하거나 제거하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-333">Ensure you only remove the previous virtual network and that you don't change or remove any other existing virtual networks from your subscription.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="7638b-334">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7638b-334">Next steps</span></span>

- <span data-ttu-id="7638b-335">프로덕션 환경에 사용하기 위한 가상 네트워크 피어링을 만들기 전에 먼저 중요한 [가상 네트워크 피어링 제약 조건 및 동작](virtual-network-manage-peering.md#requirements-and-constraints)에 철저하게 익숙해집니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-335">Thoroughly familiarize yourself with important [virtual network peering constraints and behaviors](virtual-network-manage-peering.md#requirements-and-constraints) before creating a virtual network peering for production use.</span></span>
- <span data-ttu-id="7638b-336">모든 [가상 네트워크 피어링 설정](virtual-network-manage-peering.md#create-a-peering)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-336">Learn about all [virtual network peering settings](virtual-network-manage-peering.md#create-a-peering).</span></span>
- <span data-ttu-id="7638b-337">가상 네트워크 피어링을 통해 [허브 및 스포크 네트워크 토폴로지를 만드는](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7638b-337">Learn how to [create a hub and spoke network topology](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) with virtual network peering.</span></span>