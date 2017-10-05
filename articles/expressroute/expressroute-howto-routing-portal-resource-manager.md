---
title: "ExpressRoute 회로에 라우팅을 구성하는 방법(피어링): Resource Manager: Azure | Microsoft Docs"
description: "이 문서에서는 ExpressRoute 회로의 개인, 공용 및 Microsoft 피어링을 만들고 프로비전하는 단계를 안내합니다. 또한 회로의 상태를 확인하고 업데이트 또는 삭제하는 방법을 보여줍니다."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8c2a7ed2-ae5c-4e49-81f6-77cf9f2b2ac9
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: cherylmc
ms.openlocfilehash: 55ccadfea55b8098ee58dcaef942f6ba54093665
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit"></a><span data-ttu-id="f24ea-104">ExpressRoute 회로의 피어링 만들기 및 수정</span><span class="sxs-lookup"><span data-stu-id="f24ea-104">Create and modify peering for an ExpressRoute circuit</span></span>

<span data-ttu-id="f24ea-105">이 문서는 Azure Portal을 사용하여 Resource Manager 배포 모델에서 ExpressRoute 회로에 라우팅 구성을 만들고 관리하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in the Resource Manager deployment model using the Azure portal.</span></span> <span data-ttu-id="f24ea-106">ExpressRoute 회로에 대한 피어링의 상태를 확인, 업데이트 또는 삭제 및 프로비전 해제를 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-106">You can also check the status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="f24ea-107">회로를 사용하는 다른 메서드를 사용하려는 경우 다음 목록에서 문서를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-107">If you want to use a different method to work with your circuit, select an article from the following list:</span></span>


## <a name="configuration-prerequisites"></a><span data-ttu-id="f24ea-108">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="f24ea-108">Configuration prerequisites</span></span>

* <span data-ttu-id="f24ea-109">구성을 시작하기 전에 [필수 구성 요소](expressroute-prerequisites.md) 페이지, [라우팅 요구 사항](expressroute-routing.md) 페이지 및 [워크플로](expressroute-workflows.md) 페이지를 검토했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-109">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md) page, the [routing requirements](expressroute-routing.md) page, and the [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="f24ea-110">활성화된 ExpressRoute 회로가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-110">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="f24ea-111">지침을 수행하여 [ExpressRoute 회로를 만들고](expressroute-howto-circuit-portal-resource-manager.md) 진행하기 전에 연결 공급자를 통해 회로를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-111">Follow the instructions to [Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="f24ea-112">ExpressRoute 회로는 다음 섹션에서 cmdlet을 실행할 수 있도록 프로비전되고 활성화된 상태여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-112">The ExpressRoute circuit must be in a provisioned and enabled state for you to be able to run the cmdlets in the next sections.</span></span>
* <span data-ttu-id="f24ea-113">공유 키/MD5 해시를 사용하려는 경우 터널의 양쪽 모두에서 이를 사용하고 최대 25로 문자 수를 제한해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-113">If you plan to use a shared key/MD5 hash, be sure to use this on both sides of the tunnel and limit the number of characters to a maximum of 25.</span></span>

<span data-ttu-id="f24ea-114">이 지침은 2계층 연결 서비스를 제공하는 서비스 공급자를 사용하여 만든 회로에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-114">These instructions only apply to circuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="f24ea-115">관리된 3계층 서비스(일반적으로 MPLS와 같은 IPVPN)를 제공하는 서비스 공급자를 사용하는 경우 연결 공급자는 사용자를 위해 라우팅을 구성하고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-115">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider configures and manages routing for you.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="f24ea-116">현재는 서비스 관리 포털을 통해 서비스 공급자가 구성한 피어링을 보급하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-116">We currently do not advertise peerings configured by service providers through the service management portal.</span></span> <span data-ttu-id="f24ea-117">이 기능을 곧 사용할 수 있도록 개발 중입니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-117">We are working on enabling this capability soon.</span></span> <span data-ttu-id="f24ea-118">BGP 피어링을 구성하기 전에 서비스 공급자에게 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="f24ea-118">Check with your service provider before configuring BGP peerings.</span></span>
> 
> 

<span data-ttu-id="f24ea-119">ExpressRoute 회로에 한 가지, 두 가지 또는 세 가지 피어링을 구성할 수 있습니다.(개인, Azure 공용 Azure 및 Microsoft)</span><span class="sxs-lookup"><span data-stu-id="f24ea-119">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="f24ea-120">선택한 순서로 피어링을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-120">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="f24ea-121">그러나 각 피어링의 구성을 한 번에 하나 씩 완료하도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-121">However, you must make sure that you complete the configuration of each peering one at a time.</span></span>

## <a name="azure-private-peering"></a><span data-ttu-id="f24ea-122">Azure 개인 피어링</span><span class="sxs-lookup"><span data-stu-id="f24ea-122">Azure private peering</span></span>

<span data-ttu-id="f24ea-123">이 섹션은 ExpressRoute 회로에 Azure 개인 피어링 구성을 만들고 가져오며 업데이트하고 삭제하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-123">This section helps you create, get, update, and delete the Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-private-peering"></a><span data-ttu-id="f24ea-124">Azure 개인 피어링을 만들려면</span><span class="sxs-lookup"><span data-stu-id="f24ea-124">To create Azure private peering</span></span>

1. <span data-ttu-id="f24ea-125">ExpressRoute 회로를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-125">Configure the ExpressRoute circuit.</span></span> <span data-ttu-id="f24ea-126">계속하기 전에 연결 공급자에 의해 회로가 완전이 프로비전되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-126">Ensure that the circuit is fully provisioned by the connectivity provider before continuing.</span></span>

  ![list](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="f24ea-128">회로에 Azure 개인 피어링을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-128">Configure Azure private peering for the circuit.</span></span> <span data-ttu-id="f24ea-129">다음 단계를 계속 진행하기 전에 다음 항목이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-129">Make sure that you have the following items before you proceed with the next steps:</span></span>

  * <span data-ttu-id="f24ea-130">기본 링크에 대한 /30 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-130">A /30 subnet for the primary link.</span></span> <span data-ttu-id="f24ea-131">서브넷은 가상 네트워크에 예약된 주소 공간의 일부가 아니어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-131">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="f24ea-132">보조 링크에 대한 /30 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-132">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="f24ea-133">서브넷은 가상 네트워크에 예약된 주소 공간의 일부가 아니어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-133">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="f24ea-134">피어링을 설정할 유효한 VLAN ID입니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-134">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="f24ea-135">회로에 다른 피어링이 동일한 VLAN ID를 사용하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-135">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="f24ea-136">피어링에 대한 AS 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-136">AS number for peering.</span></span> <span data-ttu-id="f24ea-137">2바이트 및 4바이트 AS 번호를 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-137">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="f24ea-138">이 피어링에 개인 AS 숫자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-138">You can use a private AS number for this peering.</span></span> <span data-ttu-id="f24ea-139">65515를 사용하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-139">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="f24ea-140">**선택 사항 -** 사용하기로 선택한 경우 MD5 해시를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-140">**Optional -** An MD5 hash if you choose to use one.</span></span>
3. <span data-ttu-id="f24ea-141">다음 예제와 같이 Azure 개인 피어링 행을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-141">Select the Azure Private peering row, as shown in the following example:</span></span>

  ![개인](./media/expressroute-howto-routing-portal-resource-manager/rprivate1.png)
4. <span data-ttu-id="f24ea-143">개인 피어링을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-143">Configure private peering.</span></span> <span data-ttu-id="f24ea-144">다음 이미지는 구성 예를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-144">The following image shows a configuration example:</span></span>

  ![개인 피어링 구성](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)
5. <span data-ttu-id="f24ea-146">모든 매개 변수를 지정한 후에 구성을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-146">Save the configuration once you have specified all parameters.</span></span> <span data-ttu-id="f24ea-147">구성이 성공적으로 수락되고 나면 다음 예와 유사한 내용을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-147">After the configuration has been accepted successfully, you see something similar to the following example:</span></span>

  ![개인 피어링 저장](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="to-view-azure-private-peering-details"></a><span data-ttu-id="f24ea-149">Azure 개인 피어링 세부 정보를 보려면</span><span class="sxs-lookup"><span data-stu-id="f24ea-149">To view Azure private peering details</span></span>

<span data-ttu-id="f24ea-150">피어링을 선택하면 Azure 개인 피어링의 속성을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-150">You can view the properties of Azure private peering by selecting the peering.</span></span>

![개인 피어링 보기](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="to-update-azure-private-peering-configuration"></a><span data-ttu-id="f24ea-152">Azure 개인 피어링 구성을 업데이트하려면</span><span class="sxs-lookup"><span data-stu-id="f24ea-152">To update Azure private peering configuration</span></span>

<span data-ttu-id="f24ea-153">피어링의 행을 선택하고 피어링 속성을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-153">You can select the row for peering and modify the peering properties.</span></span>

![개인 피어링 업데이트](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)

### <a name="to-delete-azure-private-peering"></a><span data-ttu-id="f24ea-155">Azure 개인 피어링을 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="f24ea-155">To delete Azure private peering</span></span>

<span data-ttu-id="f24ea-156">다음 이미지처럼 삭제 아이콘을 선택하면 피어링 구성을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-156">You can remove your peering configuration by selecting the delete icon, as shown in the following image:</span></span>

![개인 피어링 삭제](./media/expressroute-howto-routing-portal-resource-manager/rprivate4.png)

## <a name="azure-public-peering"></a><span data-ttu-id="f24ea-158">Azure 공용 피어링</span><span class="sxs-lookup"><span data-stu-id="f24ea-158">Azure public peering</span></span>

<span data-ttu-id="f24ea-159">이 섹션은 ExpressRoute 회로에 Azure 공용 피어링 구성을 만들고 가져오며 업데이트하고 삭제하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-159">This section helps you create, get, update, and delete the Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-public-peering"></a><span data-ttu-id="f24ea-160">Azure 공용 피어링을 만들려면</span><span class="sxs-lookup"><span data-stu-id="f24ea-160">To create Azure public peering</span></span>

1. <span data-ttu-id="f24ea-161">ExpressRoute 회로를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-161">Configure ExpressRoute circuit.</span></span> <span data-ttu-id="f24ea-162">계속하기 전에 연결 공급자에 의해 회로가 완전이 프로비전되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-162">Ensure that the circuit is fully provisioned by the connectivity provider before continuing further.</span></span>

  ![공용 피어링 나열](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="f24ea-164">회로에 Azure 공용 피어링을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-164">Configure Azure public peering for the circuit.</span></span> <span data-ttu-id="f24ea-165">다음 단계를 계속 진행하기 전에 다음 항목이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-165">Make sure that you have the following items before you proceed with the next steps:</span></span>

  * <span data-ttu-id="f24ea-166">기본 링크에 대한 /30 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-166">A /30 subnet for the primary link.</span></span> <span data-ttu-id="f24ea-167">유효한 공용 IPv4 접두사여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-167">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="f24ea-168">보조 링크에 대한 /30 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-168">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="f24ea-169">유효한 공용 IPv4 접두사여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-169">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="f24ea-170">피어링을 설정할 유효한 VLAN ID입니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-170">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="f24ea-171">회로에 다른 피어링이 동일한 VLAN ID를 사용하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-171">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="f24ea-172">피어링에 대한 AS 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-172">AS number for peering.</span></span> <span data-ttu-id="f24ea-173">2바이트 및 4바이트 AS 번호를 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-173">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="f24ea-174">**선택 사항 -** 사용하기로 선택한 경우 MD5 해시를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-174">**Optional -** An MD5 hash if you choose to use one.</span></span>
3. <span data-ttu-id="f24ea-175">다음 이미지와 같이 Azure 공용 피어링 행을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-175">Select the Azure public peering row, as shown in the following image:</span></span>

  ![공용 피어링 행 선택](./media/expressroute-howto-routing-portal-resource-manager/rpublic1.png)
4. <span data-ttu-id="f24ea-177">공용 피어링을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-177">Configure public peering.</span></span> <span data-ttu-id="f24ea-178">다음 이미지는 구성 예를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-178">The following image shows a configuration example:</span></span>

  ![공용 피어링 구성](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)
5. <span data-ttu-id="f24ea-180">모든 매개 변수를 지정한 후에 구성을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-180">Save the configuration once you have specified all parameters.</span></span> <span data-ttu-id="f24ea-181">구성이 성공적으로 수락되고 나면 다음 예와 유사한 내용을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-181">After the configuration has been accepted successfully, you see something similar to the following example:</span></span>

  ![공용 피어링 구성 저장](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="to-view-azure-public-peering-details"></a><span data-ttu-id="f24ea-183">Azure 공용 피어링 세부 정보를 보려면</span><span class="sxs-lookup"><span data-stu-id="f24ea-183">To view Azure public peering details</span></span>

<span data-ttu-id="f24ea-184">피어링을 선택하면 Azure 공용 피어링의 속성을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-184">You can view the properties of Azure public peering by selecting the peering.</span></span>

![공용 피어 링 속성 보기](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="to-update-azure-public-peering-configuration"></a><span data-ttu-id="f24ea-186">Azure 공용 피어링 구성을 업데이트하려면</span><span class="sxs-lookup"><span data-stu-id="f24ea-186">To update Azure public peering configuration</span></span>

<span data-ttu-id="f24ea-187">피어링의 행을 선택하고 피어링 속성을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-187">You can select the row for peering and modify the peering properties.</span></span>

![공용 피어링 행 선택](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)

### <a name="to-delete-azure-public-peering"></a><span data-ttu-id="f24ea-189">Azure 공용 피어링을 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="f24ea-189">To delete Azure public peering</span></span>

<span data-ttu-id="f24ea-190">다음 예제와 같이 삭제 아이콘을 선택하면 피어링 구성을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-190">You can remove your peering configuration by selecting the delete icon, as shown in the following example:</span></span>

![공용 피어링 삭제](./media/expressroute-howto-routing-portal-resource-manager/rpublic4.png)

## <a name="microsoft-peering"></a><span data-ttu-id="f24ea-192">Microsoft 피어링</span><span class="sxs-lookup"><span data-stu-id="f24ea-192">Microsoft peering</span></span>

<span data-ttu-id="f24ea-193">이 섹션은 ExpressRoute 회로에 Microsoft 피어링 구성을 만들고 가져오며 업데이트하고 삭제하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-193">This section helps you create, get, update, and delete the Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f24ea-194">경로 필터를 정의하지 않은 경우에도 2017년 8월 1일 이전에 구성된 ExpressRoute 회로의 Microsoft 피어링에는 Microsoft 피어링을 통해 보급된 모든 서비스 접두사가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-194">Microsoft peering of ExpressRoute circuits that were configured prior to August 1, 2017 will have all service prefixes advertised through the Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="f24ea-195">2017년 8월 1일 이후에 구성된 ExpressRoute 회로의 Microsoft 피어링에는 경로 필터가 회로에 연결될 때까지 접두사가 보급되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-195">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached to the circuit.</span></span> <span data-ttu-id="f24ea-196">자세한 내용은 [Microsoft 피어링에 경로 필터 구성](how-to-routefilter-powershell.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f24ea-196">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="to-create-microsoft-peering"></a><span data-ttu-id="f24ea-197">Microsoft 피어링을 만들려면</span><span class="sxs-lookup"><span data-stu-id="f24ea-197">To create Microsoft peering</span></span>

1. <span data-ttu-id="f24ea-198">ExpressRoute 회로를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-198">Configure ExpressRoute circuit.</span></span> <span data-ttu-id="f24ea-199">계속하기 전에 연결 공급자에 의해 회로가 완전이 프로비전되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-199">Ensure that the circuit is fully provisioned by the connectivity provider before continuing further.</span></span>

  ![Microsoft 피어링 나열](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="f24ea-201">회로에 Microsoft 피어링을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-201">Configure Microsoft peering for the circuit.</span></span> <span data-ttu-id="f24ea-202">진행하기 전에 다음 정보가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-202">Make sure that you have the following information before you proceed.</span></span>

  * <span data-ttu-id="f24ea-203">기본 링크에 대한 /30 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-203">A /30 subnet for the primary link.</span></span> <span data-ttu-id="f24ea-204">사용자가 소유하고 RIR/IRR에 등록된 유효한 공용 IPv4 접두사여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-204">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="f24ea-205">보조 링크에 대한 /30 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-205">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="f24ea-206">사용자가 소유하고 RIR/IRR에 등록된 유효한 공용 IPv4 접두사여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-206">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="f24ea-207">피어링을 설정할 유효한 VLAN ID입니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-207">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="f24ea-208">회로에 다른 피어링이 동일한 VLAN ID를 사용하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-208">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="f24ea-209">피어링에 대한 AS 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-209">AS number for peering.</span></span> <span data-ttu-id="f24ea-210">2바이트 및 4바이트 AS 번호를 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-210">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="f24ea-211">보급된 접두사: BGP 세션을 통해 보급하려는 모든 접두사 목록을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-211">Advertised prefixes: You must provide a list of all prefixes you plan to advertise over the BGP session.</span></span> <span data-ttu-id="f24ea-212">공용 IP 주소 접두사만 수락됩니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-212">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="f24ea-213">접두사 집합을 보내려는 경우 쉼표로 구분된 목록을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-213">If you plan to send a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="f24ea-214">이 접두사는 RIR/IRR에 등록되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-214">These prefixes must be registered to you in an RIR / IRR.</span></span>
  * <span data-ttu-id="f24ea-215">**선택 사항 -** 고객 ASN: 피어링 AS 숫자에 등록되지 않은 광고 접두사인 경우 등록된 AS 번호를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-215">**Optional -** Customer ASN: If you are advertising prefixes that are not registered to the peering AS number, you can specify the AS number to which they are registered.</span></span>
  * <span data-ttu-id="f24ea-216">라우팅 레지스트리 이름: AS 번호 및 접두사가 등록된 RIR/ IRR를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-216">Routing Registry Name: You can specify the RIR / IRR against which the AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="f24ea-217">**선택 사항 -** 사용하기로 선택한 경우 MD5 해시를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-217">**Optional -** An MD5 hash if you choose to use one.</span></span>
3. <span data-ttu-id="f24ea-218">다음 예제와 같이 구성하려는 피어링을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-218">You can select the peering you wish to configure, as shown in the following example.</span></span> <span data-ttu-id="f24ea-219">Microsoft 피어링 행을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-219">Select the Microsoft peering row.</span></span>

  ![Microsoft 피어링 행 선택](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft1.png)
4. <span data-ttu-id="f24ea-221">Microsoft 피어링을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-221">Configure Microsoft peering.</span></span> <span data-ttu-id="f24ea-222">다음 이미지는 구성 예를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-222">The following image shows a configuration example:</span></span>

  ![Microsoft 피어링 구성](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft2.png)
5. <span data-ttu-id="f24ea-224">모든 매개 변수를 지정한 후에 구성을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-224">Save the configuration once you have specified all parameters.</span></span>

  <span data-ttu-id="f24ea-225">회로가 ‘유효성 검사가 필요’한 상태가 되면(이미지에 표시됨), 지원 팀에 접두사에 대한 소유권의 증거를 보여주는 지원 티켓을 열어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-225">If your circuit gets to a 'Validation needed' state (as shown in the image), you must open a support ticket to show proof of ownership of the prefixes to our support team.</span></span>

  ![Microsoft 피어링 구성 저장](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft5.png)

  <span data-ttu-id="f24ea-227">다음 예제와 같이 포털에서 바로 지원 티켓을 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-227">You can open a support ticket directly from the portal, as shown in the following example:</span></span>

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft6.png)


1. <span data-ttu-id="f24ea-228">구성이 성공적으로 수락되고 나면 다음 이미지와 유사한 내용을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-228">After the configuration has been accepted successfully, you see something similar to the following image:</span></span>

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="to-view-microsoft-peering-details"></a><span data-ttu-id="f24ea-229">Microsoft 피어링 세부 정보를 보려면</span><span class="sxs-lookup"><span data-stu-id="f24ea-229">To view Microsoft peering details</span></span>

<span data-ttu-id="f24ea-230">피어링을 선택하면 Azure 공용 피어링의 속성을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-230">You can view the properties of Azure public peering by selecting the peering.</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft3.png)

### <a name="to-update-microsoft-peering-configuration"></a><span data-ttu-id="f24ea-231">Microsoft 피어링 구성을 업데이트하려면</span><span class="sxs-lookup"><span data-stu-id="f24ea-231">To update Microsoft peering configuration</span></span>

<span data-ttu-id="f24ea-232">피어링의 행을 선택하고 피어링 속성을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-232">You can select the row for peering and modify the peering properties.</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="to-delete-microsoft-peering"></a><span data-ttu-id="f24ea-233">Microsoft 피어링을 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="f24ea-233">To delete Microsoft peering</span></span>

<span data-ttu-id="f24ea-234">다음 이미지처럼 삭제 아이콘을 선택하면 피어링 구성을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-234">You can remove your peering configuration by selecting the delete icon, as shown in the following image:</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft4.png)

## <a name="next-steps"></a><span data-ttu-id="f24ea-235">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f24ea-235">Next steps</span></span>

<span data-ttu-id="f24ea-236">다음 단계로 [VNet을 ExpressRoute 회로에 연결](expressroute-howto-linkvnet-portal-resource-manager.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f24ea-236">Next step, [Link a VNet to an ExpressRoute circuit](expressroute-howto-linkvnet-portal-resource-manager.md)</span></span>
* <span data-ttu-id="f24ea-237">ExpressRoute 워크플로에 대한 자세한 내용은 [ExpressRoute 워크플로](expressroute-workflows.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f24ea-237">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="f24ea-238">회로 피어링에 대한 자세한 내용은 [Express 경로 회로 및 라우팅 도메인](expressroute-circuit-peerings.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f24ea-238">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="f24ea-239">가상 네트워크 작업에 대한 자세한 내용은 [가상 네트워크 개요](../virtual-network/virtual-networks-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f24ea-239">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>
