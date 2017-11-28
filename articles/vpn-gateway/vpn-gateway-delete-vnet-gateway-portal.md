---
title: "가상 네트워크 게이트웨이 삭제: Azure portal: Resource Manager | Microsoft Docs"
description: "Resource Manager 배포 모델에서 Azure Portal을 사용하여 가상 네트워크 게이트웨이를 삭제합니다."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: 
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: cherylmc
ms.openlocfilehash: 1d289c09465cb8d5e4bfa569441dffcbf562b3bf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="delete-a-virtual-network-gateway-using-the-portal"></a><span data-ttu-id="223a6-103">포털을 사용하여 가상 네트워크 게이트웨이 삭제</span><span class="sxs-lookup"><span data-stu-id="223a6-103">Delete a virtual network gateway using the portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="223a6-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="223a6-104">Azure portal</span></span>](vpn-gateway-delete-vnet-gateway-portal.md)
> * [<span data-ttu-id="223a6-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="223a6-105">PowerShell</span></span>](vpn-gateway-delete-vnet-gateway-powershell.md)
> * [<span data-ttu-id="223a6-106">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="223a6-106">PowerShell (classic)</span></span>](vpn-gateway-delete-vnet-gateway-classic-powershell.md)

<span data-ttu-id="223a6-107">VPN 게이트웨이 구성에 대한 가상 네트워크 게이트웨이 삭제하려는 경우에 몇 가지 다른 접근 방법을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="223a6-107">There are a couple of different approaches you can take when you want to delete a virtual network gateway for a VPN gateway configuration.</span></span>

- <span data-ttu-id="223a6-108">테스트 환경의 경우처럼 모든 항목을 삭제하고 다시 시작하려면 전체 리소스 그룹을 삭제하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="223a6-108">If you want to delete everything and start over, as in the case of a test environment, you can delete the resource group.</span></span> <span data-ttu-id="223a6-109">리소스 그룹을 삭제하면 그룹 내의 모든 리소스가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="223a6-109">When you delete a resource group, it deletes all the resources within the group.</span></span> <span data-ttu-id="223a6-110">이 방법은 리소스 그룹에 리소스를 유지하지 않으려는 경우에만 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="223a6-110">This is method is only recommended if you don't want to keep any of the resources in the resource group.</span></span> <span data-ttu-id="223a6-111">이 방법을 사용할 때는 몇 가지 리소스만 선택적으로 삭제할 수가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="223a6-111">You can't selectively delete only a few resources using this approach.</span></span>

- <span data-ttu-id="223a6-112">리소스 그룹에 일부 리소스를 유지하려는 경우 가상 네트워크 게이트웨이를 삭제하는 작업이 좀 더 복잡해집니다.</span><span class="sxs-lookup"><span data-stu-id="223a6-112">If you want to keep some of the resources in your resource group, deleting a virtual network gateway becomes slightly more complicated.</span></span> <span data-ttu-id="223a6-113">가상 네트워크 게이트웨이를 삭제하려면 먼저 게이트웨이에 의존하는 모든 리소스를 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="223a6-113">Before you can delete the virtual network gateway, you must first delete any resources that are dependent on the gateway.</span></span> <span data-ttu-id="223a6-114">수행하는 단계는 만든 연결의 유형 및 각 연결에 대한 종속 리소스에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="223a6-114">The steps you follow depend on the type of connections that you created and the dependent resources for each connection.</span></span>

## <a name="delete-a-vpn-gateway"></a><span data-ttu-id="223a6-115">VPN Gateway 삭제</span><span class="sxs-lookup"><span data-stu-id="223a6-115">Delete a VPN gateway</span></span>

<span data-ttu-id="223a6-116">가상 네트워크 게이트웨이를 삭제하려면 먼저 가상 네트워크 게이트웨이와 관련된 각 리소스를 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="223a6-116">To delete a virtual network gateway, you must first delete each resource that pertains to the virtual network gateway.</span></span> <span data-ttu-id="223a6-117">리소스는 종속성으로 인해 특정 순서로 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="223a6-117">Resources must be deleted in a certain order due to dependencies.</span></span>

[!INCLUDE [delete gateway](../../includes/vpn-gateway-delete-vnet-gateway-portal-include.md)]

<span data-ttu-id="223a6-118">이때 가상 네트워크 게이트웨이가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="223a6-118">At this point, the virtual network gateway is deleted.</span></span> <span data-ttu-id="223a6-119">다음 단계는 더 이상 사용되지 않는 모든 리소스를 삭제하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="223a6-119">The next steps help you delete any resources that are no longer being used.</span></span>

### <a name="to-delete-the-local-network-gateway"></a><span data-ttu-id="223a6-120">로컬 네트워크 게이트웨이를 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="223a6-120">To delete the local network gateway</span></span>

1. <span data-ttu-id="223a6-121">**모든 리소스**에서 각 연결에 연결된 로컬 네트워크 게이트웨이를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="223a6-121">In **All resources**, locate the local network gateways that were associated with each connection.</span></span>
2. <span data-ttu-id="223a6-122">로컬 네트워크 게이트웨이의 **개요** 블레이드에서 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="223a6-122">On the **Overview** blade for the local network gateway, click **Delete**.</span></span>

### <a name="to-delete-the-public-ip-address-resource-for-the-gateway"></a><span data-ttu-id="223a6-123">게이트웨이에 대한 공용 IP 주소 리소스를 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="223a6-123">To delete the Public IP address resource for the gateway</span></span>

1. <span data-ttu-id="223a6-124">**모든 리소스**에서 게이트웨이와 연결된 공용 IP 주소 리소스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="223a6-124">In **All resources**, locate the Public IP address resource that was associated to the gateway.</span></span> <span data-ttu-id="223a6-125">가상 네트워크 게이트웨이가 활성-활성인 경우 두 개의 공용 IP 주소가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="223a6-125">If the virtual network gateway was active-active, you will see two Public IP addresses.</span></span> 
2. <span data-ttu-id="223a6-126">공용 IP 주소에 대한 **개요** 페이지에서 **삭제**, **예**를 차례로 클릭하여 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="223a6-126">On the **Overview** page for the Public IP address, click **Delete**, then **Yes** to confirm.</span></span>

### <a name="to-delete-the-gateway-subnet"></a><span data-ttu-id="223a6-127">게이트웨이 서브넷을 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="223a6-127">To delete the gateway subnet</span></span>

1. <span data-ttu-id="223a6-128">**모든 리소스**에서 가상 네트워크를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="223a6-128">In **All resources**, locate the virtual network.</span></span> 
2. <span data-ttu-id="223a6-129">**서브넷** 블레이드에서 **게이트웨이 서브넷**, **삭제**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="223a6-129">On the **Subnets** blade, click the **GatewaySubnet**, then click **Delete**.</span></span> 
3. <span data-ttu-id="223a6-130">**예**를 클릭하여 게이트웨이 서브넷 삭제를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="223a6-130">Click **Yes** to confirm that you want to delete the gateway subnet.</span></span>

## <span data-ttu-id="223a6-131"><a name="deleterg"></a>리소스 그룹을 삭제하여 VPN 게이트웨이 삭제</span><span class="sxs-lookup"><span data-stu-id="223a6-131"><a name="deleterg"></a>Delete a VPN gateway by deleting the resource group</span></span>

<span data-ttu-id="223a6-132">리소스 그룹에 리소스를 유지하지 않고 새로 시작하려는 경우 전체 리소스 그룹을 삭제하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="223a6-132">If you are not concerned about keeping any of your resources in the resource group and you just want to start over, you can delete an entire resource group.</span></span> <span data-ttu-id="223a6-133">모든 항목을 제거하는 빠른 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="223a6-133">This is a quick way to remove everything.</span></span> <span data-ttu-id="223a6-134">다음 단계는 Resource Manager 배포 모델에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="223a6-134">The following steps apply only to the Resource Manager deployment model.</span></span>

1. <span data-ttu-id="223a6-135">**모든 리소스**에서 리소스 그룹을 찾고 클릭하여 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="223a6-135">In **All resources**, locate the resource group and click to open the blade.</span></span>
2. <span data-ttu-id="223a6-136">**삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="223a6-136">Click **Delete**.</span></span> <span data-ttu-id="223a6-137">삭제 블레이드에서 영향을 받는 리소스를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="223a6-137">On the Delete blade, view the affected resources.</span></span> <span data-ttu-id="223a6-138">해당 리소스를 모두 삭제할 것인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="223a6-138">Make sure that you want to delete all of these resources.</span></span> <span data-ttu-id="223a6-139">그렇지 않은 경우 이 문서의 맨 위에 있는 [VPN Gateway 삭제](#deletegw) 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="223a6-139">If not, use the steps in [Delete a VPN gateway](#deletegw) at the top of this article.</span></span>
3. <span data-ttu-id="223a6-140">계속하려면 삭제할 리소스 그룹의 이름을 입력한 다음 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="223a6-140">To proceed, type the name of the resource group that you want to delete, then click **Delete**.</span></span>