---
title: "어떻게 tooconfigure (피어 링)에 대 한 라우팅 ExpressRoute 회로: 리소스 관리자: Azure | Microsoft Docs"
description: "이 문서를 만들고 hello private, public 및 Microsoft 피어 링 express 경로 회로 프로 비전에 대 한 hello 단계를 안내 합니다. 또한이 문서를 보면 toocheck hello 상태 업데이트 또는 회로 대 한 피어 링 삭제 방법을 알 수 있습니다."
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
ms.openlocfilehash: a8ca25f488dde728cb3b06cd2c91873f3069feaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit"></a><span data-ttu-id="856e2-104">ExpressRoute 회로의 피어링 만들기 및 수정</span><span class="sxs-lookup"><span data-stu-id="856e2-104">Create and modify peering for an ExpressRoute circuit</span></span>

<span data-ttu-id="856e2-105">이 문서를 사용 하 여 만들고 hello Azure 포털을 사용 하 여 hello 리소스 관리자를 배포 하는 모델의 ExpressRoute 회로 대 한 라우팅 구성을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in hello Resource Manager deployment model using hello Azure portal.</span></span> <span data-ttu-id="856e2-106">Hello 상태, 업데이트 또는 삭제를 확인 하 고 피어 링 express 경로 회로 대 한 프로 비전을 해제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-106">You can also check hello status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="856e2-107">다른 방법 toowork toouse 회로 사용 하려는 경우 hello 다음 목록에서에서 아티클을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-107">If you want toouse a different method toowork with your circuit, select an article from hello following list:</span></span>


## <a name="configuration-prerequisites"></a><span data-ttu-id="856e2-108">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="856e2-108">Configuration prerequisites</span></span>

* <span data-ttu-id="856e2-109">Hello 검토 했는지 확인 [필수 구성 요소](expressroute-prerequisites.md) 페이지 hello [라우팅 요구 사항](expressroute-routing.md) 페이지 및 hello [워크플로](expressroute-workflows.md) 구성을 시작 하기 전에 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-109">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md) page, hello [routing requirements](expressroute-routing.md) page, and hello [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="856e2-110">활성화된 Express 경로 회로가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-110">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="856e2-111">너무 hello 지침에 따라[ExpressRoute 회로 만들기](expressroute-howto-circuit-portal-resource-manager.md) 있고 계속 hello 회로 하기 전에 연결 공급자가 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-111">Follow hello instructions too[Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="856e2-112">ExpressRoute 회로 hello hello 다음 섹션의 toobe 수 toorun hello cmdlet을 가능 하 고 프로 비전 된 상태에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-112">hello ExpressRoute circuit must be in a provisioned and enabled state for you toobe able toorun hello cmdlets in hello next sections.</span></span>
* <span data-ttu-id="856e2-113">Toouse 공유 키/MD5 해시를 사용 하도록 하려는 경우 수 있는지 toouse이 문자 tooa 최대 25의 hello 터널 및 제한 hello 번호의 양쪽 모두에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-113">If you plan toouse a shared key/MD5 hash, be sure toouse this on both sides of hello tunnel and limit hello number of characters tooa maximum of 25.</span></span>

<span data-ttu-id="856e2-114">이러한 지침은 계층 2 연결 서비스를 제공 하는 서비스 공급자를 사용 하 여 만든 toocircuits만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-114">These instructions only apply toocircuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="856e2-115">관리된 3계층 서비스(일반적으로 MPLS와 같은 IPVPN)를 제공하는 서비스 공급자를 사용하는 경우 연결 공급자는 사용자를 위해 라우팅을 구성하고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-115">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider configures and manages routing for you.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="856e2-116">에서는 현재 보급 되지 않고 피어 링 hello 서비스 관리 포털을 통해 서비스 공급자가 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-116">We currently do not advertise peerings configured by service providers through hello service management portal.</span></span> <span data-ttu-id="856e2-117">이 기능을 곧 사용할 수 있도록 개발 중입니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-117">We are working on enabling this capability soon.</span></span> <span data-ttu-id="856e2-118">BGP 피어링을 구성하기 전에 서비스 공급자에게 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="856e2-118">Check with your service provider before configuring BGP peerings.</span></span>
> 
> 

<span data-ttu-id="856e2-119">ExpressRoute 회로에 한 가지, 두 가지 또는 세 가지 피어링을 구성할 수 있습니다.(개인, Azure 공용 Azure 및 Microsoft)</span><span class="sxs-lookup"><span data-stu-id="856e2-119">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="856e2-120">선택한 순서로 피어링을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-120">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="856e2-121">그러나 한 번에 하나씩 피어 링의 hello 구성을 완료 되었는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-121">However, you must make sure that you complete hello configuration of each peering one at a time.</span></span>

## <a name="azure-private-peering"></a><span data-ttu-id="856e2-122">Azure 개인 피어링</span><span class="sxs-lookup"><span data-stu-id="856e2-122">Azure private peering</span></span>

<span data-ttu-id="856e2-123">이 섹션을 사용 하면 만들기, 가져오기, 업데이트 및 삭제 hello ExpressRoute 회로 대 한 개인 피어 링 구성을 Azure 있습니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-123">This section helps you create, get, update, and delete hello Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-private-peering"></a><span data-ttu-id="856e2-124">Azure 개인 피어 링 toocreate</span><span class="sxs-lookup"><span data-stu-id="856e2-124">toocreate Azure private peering</span></span>

1. <span data-ttu-id="856e2-125">Hello ExpressRoute 회로 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-125">Configure hello ExpressRoute circuit.</span></span> <span data-ttu-id="856e2-126">계속 하기 전에 hello 회로 hello 연결 공급자에 의해 제공 완벽 하 게 되 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-126">Ensure that hello circuit is fully provisioned by hello connectivity provider before continuing.</span></span>

  ![list](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="856e2-128">Azure 개인 피어 링 hello 회로 대 한 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-128">Configure Azure private peering for hello circuit.</span></span> <span data-ttu-id="856e2-129">Hello 다음 단계를 진행 하기 전에 다음 항목 hello 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-129">Make sure that you have hello following items before you proceed with hello next steps:</span></span>

  * <span data-ttu-id="856e2-130">/ 30 서브넷 hello 기본 링크에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-130">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="856e2-131">hello 서브넷에 가상 네트워크에 대 한 예약 된 모든 주소 공간의 일부가 아니어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-131">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="856e2-132">/ 30 서브넷 hello 보조 링크에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-132">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="856e2-133">hello 서브넷에 가상 네트워크에 대 한 예약 된 모든 주소 공간의 일부가 아니어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-133">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="856e2-134">유효한 VLAN ID tooestablish이 피어 링을 합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-134">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="856e2-135">없는 다른 피어 링 되도록 hello 회로에 사용 하 여 hello 동일한 VLAN ID</span><span class="sxs-lookup"><span data-stu-id="856e2-135">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="856e2-136">피어링에 대한 AS 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-136">AS number for peering.</span></span> <span data-ttu-id="856e2-137">2바이트 및 4바이트 AS 번호를 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-137">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="856e2-138">이 피어링에 개인 AS 숫자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-138">You can use a private AS number for this peering.</span></span> <span data-ttu-id="856e2-139">65515를 사용하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-139">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="856e2-140">**선택 사항-** toouse 하나를 선택 하는 경우 MD5 해시입니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-140">**Optional -** An MD5 hash if you choose toouse one.</span></span>
3. <span data-ttu-id="856e2-141">다음 예제는 hello와 같이 hello Azure 개인 피어 링 행을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-141">Select hello Azure Private peering row, as shown in hello following example:</span></span>

  ![개인](./media/expressroute-howto-routing-portal-resource-manager/rprivate1.png)
4. <span data-ttu-id="856e2-143">개인 피어링을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-143">Configure private peering.</span></span> <span data-ttu-id="856e2-144">다음 이미지는 hello 구성 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-144">hello following image shows a configuration example:</span></span>

  ![개인 피어링 구성](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)
5. <span data-ttu-id="856e2-146">모든 매개 변수를 지정 했으면 hello 구성을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-146">Save hello configuration once you have specified all parameters.</span></span> <span data-ttu-id="856e2-147">Hello 구성이 성공적으로 수락 하는 후에 다음 예제는 다음과 유사한 toohello를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-147">After hello configuration has been accepted successfully, you see something similar toohello following example:</span></span>

  ![개인 피어링 저장](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="tooview-azure-private-peering-details"></a><span data-ttu-id="856e2-149">세부 정보를 피어 링 개인 Azure tooview</span><span class="sxs-lookup"><span data-stu-id="856e2-149">tooview Azure private peering details</span></span>

<span data-ttu-id="856e2-150">Azure 개인 피어 링 hello 피어 링을 선택 하 여의 hello 속성을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-150">You can view hello properties of Azure private peering by selecting hello peering.</span></span>

![개인 피어링 보기](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="tooupdate-azure-private-peering-configuration"></a><span data-ttu-id="856e2-152">tooupdate Azure 개인 피어 링 구성</span><span class="sxs-lookup"><span data-stu-id="856e2-152">tooupdate Azure private peering configuration</span></span>

<span data-ttu-id="856e2-153">피어 링 용 hello 행을 선택 하 고 hello 피어 링 속성을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-153">You can select hello row for peering and modify hello peering properties.</span></span>

![개인 피어링 업데이트](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)

### <a name="toodelete-azure-private-peering"></a><span data-ttu-id="856e2-155">Azure 개인 피어 링 toodelete</span><span class="sxs-lookup"><span data-stu-id="856e2-155">toodelete Azure private peering</span></span>

<span data-ttu-id="856e2-156">Hello 다음 이미지와 같이 hello 삭제 아이콘을 선택 하 여 피어 링 구성을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-156">You can remove your peering configuration by selecting hello delete icon, as shown in hello following image:</span></span>

![개인 피어링 삭제](./media/expressroute-howto-routing-portal-resource-manager/rprivate4.png)

## <a name="azure-public-peering"></a><span data-ttu-id="856e2-158">Azure 공용 피어링</span><span class="sxs-lookup"><span data-stu-id="856e2-158">Azure public peering</span></span>

<span data-ttu-id="856e2-159">이 섹션을 사용 하면 생성, 가져오기, 업데이트 및 삭제 hello ExpressRoute 회로 대 한 Azure 공용 피어 링 구성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-159">This section helps you create, get, update, and delete hello Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-public-peering"></a><span data-ttu-id="856e2-160">Azure 공용 피어 링 toocreate</span><span class="sxs-lookup"><span data-stu-id="856e2-160">toocreate Azure public peering</span></span>

1. <span data-ttu-id="856e2-161">ExpressRoute 회로를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-161">Configure ExpressRoute circuit.</span></span> <span data-ttu-id="856e2-162">Hello 회로 완벽 하 게 비전 되도록 hello 연결 공급자가 추가 되었는지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-162">Ensure that hello circuit is fully provisioned by hello connectivity provider before continuing further.</span></span>

  ![공용 피어링 나열](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="856e2-164">Azure 공용 피어 링 hello 회로 대 한 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-164">Configure Azure public peering for hello circuit.</span></span> <span data-ttu-id="856e2-165">Hello 다음 단계를 진행 하기 전에 다음 항목 hello 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-165">Make sure that you have hello following items before you proceed with hello next steps:</span></span>

  * <span data-ttu-id="856e2-166">/ 30 서브넷 hello 기본 링크에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-166">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="856e2-167">유효한 공용 IPv4 접두사여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-167">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="856e2-168">/ 30 서브넷 hello 보조 링크에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-168">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="856e2-169">유효한 공용 IPv4 접두사여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-169">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="856e2-170">유효한 VLAN ID tooestablish이 피어 링을 합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-170">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="856e2-171">없는 다른 피어 링 되도록 hello 회로에 사용 하 여 hello 동일한 VLAN ID</span><span class="sxs-lookup"><span data-stu-id="856e2-171">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="856e2-172">피어링에 대한 AS 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-172">AS number for peering.</span></span> <span data-ttu-id="856e2-173">2바이트 및 4바이트 AS 번호를 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-173">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="856e2-174">**선택 사항-** toouse 하나를 선택 하는 경우 MD5 해시입니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-174">**Optional -** An MD5 hash if you choose toouse one.</span></span>
3. <span data-ttu-id="856e2-175">다음 이미지는 hello와 같이 hello Azure 공용 피어 링 행을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-175">Select hello Azure public peering row, as shown in hello following image:</span></span>

  ![공용 피어링 행 선택](./media/expressroute-howto-routing-portal-resource-manager/rpublic1.png)
4. <span data-ttu-id="856e2-177">공용 피어링을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-177">Configure public peering.</span></span> <span data-ttu-id="856e2-178">다음 이미지는 hello 구성 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-178">hello following image shows a configuration example:</span></span>

  ![공용 피어링 구성](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)
5. <span data-ttu-id="856e2-180">모든 매개 변수를 지정 했으면 hello 구성을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-180">Save hello configuration once you have specified all parameters.</span></span> <span data-ttu-id="856e2-181">Hello 구성이 성공적으로 수락 하는 후에 다음 예제는 다음과 유사한 toohello를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-181">After hello configuration has been accepted successfully, you see something similar toohello following example:</span></span>

  ![공용 피어링 구성 저장](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="tooview-azure-public-peering-details"></a><span data-ttu-id="856e2-183">세부 정보를 피어 링 공용 Azure tooview</span><span class="sxs-lookup"><span data-stu-id="856e2-183">tooview Azure public peering details</span></span>

<span data-ttu-id="856e2-184">Azure 공용 피어 링 hello 피어 링을 선택 하 여의 hello 속성을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-184">You can view hello properties of Azure public peering by selecting hello peering.</span></span>

![공용 피어 링 속성 보기](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="tooupdate-azure-public-peering-configuration"></a><span data-ttu-id="856e2-186">tooupdate Azure 공용 피어 링 구성</span><span class="sxs-lookup"><span data-stu-id="856e2-186">tooupdate Azure public peering configuration</span></span>

<span data-ttu-id="856e2-187">피어 링 용 hello 행을 선택 하 고 hello 피어 링 속성을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-187">You can select hello row for peering and modify hello peering properties.</span></span>

![공용 피어링 행 선택](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)

### <a name="toodelete-azure-public-peering"></a><span data-ttu-id="856e2-189">Azure 공용 피어 링 toodelete</span><span class="sxs-lookup"><span data-stu-id="856e2-189">toodelete Azure public peering</span></span>

<span data-ttu-id="856e2-190">다음 예제는 hello와 같이 hello 삭제 아이콘을 선택 하 여 구성에 피어 링을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-190">You can remove your peering configuration by selecting hello delete icon, as shown in hello following example:</span></span>

![공용 피어링 삭제](./media/expressroute-howto-routing-portal-resource-manager/rpublic4.png)

## <a name="microsoft-peering"></a><span data-ttu-id="856e2-192">Microsoft 피어링</span><span class="sxs-lookup"><span data-stu-id="856e2-192">Microsoft peering</span></span>

<span data-ttu-id="856e2-193">이 섹션을 사용 하면 생성, 가져오기, 업데이트 및 삭제 hello ExpressRoute 회로 대 한 Microsoft 피어 링 구성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-193">This section helps you create, get, update, and delete hello Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="856e2-194">이전 tooAugust 1에 구성 된 ExpressRoute 회로의 Microsoft 피어 링, 경로 필터 정의 되어 있지 않은 경우에 2017 hello Microsoft 피어 링을 통해 보급 되는 모든 서비스 접두사를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-194">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through hello Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="856e2-195">Microsoft 또는 그 이후에 2017 년 8 월 1 구성한 ExpressRoute 회로의 피어 링 수는 없습니다 모든 접두사 필터는 연결 될 때까지 보급 toohello 회로 합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-195">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span> <span data-ttu-id="856e2-196">자세한 내용은 [Microsoft 피어링에 경로 필터 구성](how-to-routefilter-powershell.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="856e2-196">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="toocreate-microsoft-peering"></a><span data-ttu-id="856e2-197">toocreate Microsoft 피어 링</span><span class="sxs-lookup"><span data-stu-id="856e2-197">toocreate Microsoft peering</span></span>

1. <span data-ttu-id="856e2-198">ExpressRoute 회로를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-198">Configure ExpressRoute circuit.</span></span> <span data-ttu-id="856e2-199">Hello 회로 완벽 하 게 비전 되도록 hello 연결 공급자가 추가 되었는지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-199">Ensure that hello circuit is fully provisioned by hello connectivity provider before continuing further.</span></span>

  ![Microsoft 피어링 나열](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="856e2-201">Microsoft hello 회로 대 한 피어 링을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-201">Configure Microsoft peering for hello circuit.</span></span> <span data-ttu-id="856e2-202">계속 하기 전에 정보 다음 hello 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-202">Make sure that you have hello following information before you proceed.</span></span>

  * <span data-ttu-id="856e2-203">/ 30 서브넷 hello 기본 링크에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-203">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="856e2-204">사용자가 소유하고 RIR/IRR에 등록된 유효한 공용 IPv4 접두사여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-204">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="856e2-205">/ 30 서브넷 hello 보조 링크에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-205">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="856e2-206">사용자가 소유하고 RIR/IRR에 등록된 유효한 공용 IPv4 접두사여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-206">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="856e2-207">유효한 VLAN ID tooestablish이 피어 링을 합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-207">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="856e2-208">없는 다른 피어 링 되도록 hello 회로에 사용 하 여 hello 동일한 VLAN ID</span><span class="sxs-lookup"><span data-stu-id="856e2-208">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="856e2-209">피어링에 대한 AS 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-209">AS number for peering.</span></span> <span data-ttu-id="856e2-210">2바이트 및 4바이트 AS 번호를 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-210">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="856e2-211">접두사를 보급: 목록을 제공 해야 모든 접두사의 hello BGP 세션을 통해 tooadvertise 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-211">Advertised prefixes: You must provide a list of all prefixes you plan tooadvertise over hello BGP session.</span></span> <span data-ttu-id="856e2-212">공용 IP 주소 접두사만 수락됩니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-212">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="856e2-213">Toosend 접두사를 사용 하도록 하려는 경우 쉼표로 구분 된 목록을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-213">If you plan toosend a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="856e2-214">이 접두사는 RIR에 등록 된 tooyou 여야 / IRR입니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-214">These prefixes must be registered tooyou in an RIR / IRR.</span></span>
  * <span data-ttu-id="856e2-215">**선택 사항-** 고객 ASN: 광고 접두사 수로 등록 된 toohello 피어 링 되지 않은 경우 등록 된 숫자 toowhich로 hello를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-215">**Optional -** Customer ASN: If you are advertising prefixes that are not registered toohello peering AS number, you can specify hello AS number toowhich they are registered.</span></span>
  * <span data-ttu-id="856e2-216">라우팅 레지스트리 이름을: hello RIR 지정할 수 있습니다는 hello에 대 한 번호 매기기로이 앞에 추가 IRR를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-216">Routing Registry Name: You can specify hello RIR / IRR against which hello AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="856e2-217">**선택 사항-** toouse 하나를 선택 하는 경우 MD5 해시입니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-217">**Optional -** An MD5 hash if you choose toouse one.</span></span>
3. <span data-ttu-id="856e2-218">Hello 피어 링 tooconfigure, 원하는 hello 다음 예와 같이 선택할 수 있습니다 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-218">You can select hello peering you wish tooconfigure, as shown in hello following example.</span></span> <span data-ttu-id="856e2-219">Hello Microsoft 피어 링 행을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-219">Select hello Microsoft peering row.</span></span>

  ![Microsoft 피어링 행 선택](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft1.png)
4. <span data-ttu-id="856e2-221">Microsoft 피어링을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-221">Configure Microsoft peering.</span></span> <span data-ttu-id="856e2-222">다음 이미지는 hello 구성 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-222">hello following image shows a configuration example:</span></span>

  ![Microsoft 피어링 구성](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft2.png)
5. <span data-ttu-id="856e2-224">모든 매개 변수를 지정 했으면 hello 구성을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-224">Save hello configuration once you have specified all parameters.</span></span>

  <span data-ttu-id="856e2-225">회로 가져오면 tooa '유효성 검사 필요' (그림과 같이 hello) 상태 이면 hello 접두사 tooour 지원 팀 소유권 증명 지원 티켓 tooshow 열어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-225">If your circuit gets tooa 'Validation needed' state (as shown in hello image), you must open a support ticket tooshow proof of ownership of hello prefixes tooour support team.</span></span>

  ![Microsoft 피어링 구성 저장](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft5.png)

  <span data-ttu-id="856e2-227">다음 예제는 hello와 같이 hello 포털에서 직접 지원 티켓을 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-227">You can open a support ticket directly from hello portal, as shown in hello following example:</span></span>

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft6.png)


1. <span data-ttu-id="856e2-228">Hello 구성이 성공적으로 수락 하는 후 다음 이미지는 다음과 유사한 toohello를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-228">After hello configuration has been accepted successfully, you see something similar toohello following image:</span></span>

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="tooview-microsoft-peering-details"></a><span data-ttu-id="856e2-229">tooview Microsoft 피어 링 세부 정보</span><span class="sxs-lookup"><span data-stu-id="856e2-229">tooview Microsoft peering details</span></span>

<span data-ttu-id="856e2-230">Azure 공용 피어 링 hello 피어 링을 선택 하 여의 hello 속성을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-230">You can view hello properties of Azure public peering by selecting hello peering.</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft3.png)

### <a name="tooupdate-microsoft-peering-configuration"></a><span data-ttu-id="856e2-231">tooupdate Microsoft 피어 링 구성</span><span class="sxs-lookup"><span data-stu-id="856e2-231">tooupdate Microsoft peering configuration</span></span>

<span data-ttu-id="856e2-232">피어 링 용 hello 행을 선택 하 고 hello 피어 링 속성을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-232">You can select hello row for peering and modify hello peering properties.</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="toodelete-microsoft-peering"></a><span data-ttu-id="856e2-233">toodelete Microsoft 피어 링</span><span class="sxs-lookup"><span data-stu-id="856e2-233">toodelete Microsoft peering</span></span>

<span data-ttu-id="856e2-234">Hello 다음 이미지와 같이 hello 삭제 아이콘을 선택 하 여 피어 링 구성을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="856e2-234">You can remove your peering configuration by selecting hello delete icon, as shown in hello following image:</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft4.png)

## <a name="next-steps"></a><span data-ttu-id="856e2-235">다음 단계</span><span class="sxs-lookup"><span data-stu-id="856e2-235">Next steps</span></span>

<span data-ttu-id="856e2-236">다음 단계 [VNet tooan ExpressRoute 회로 연결](expressroute-howto-linkvnet-portal-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="856e2-236">Next step, [Link a VNet tooan ExpressRoute circuit](expressroute-howto-linkvnet-portal-resource-manager.md)</span></span>
* <span data-ttu-id="856e2-237">Express 경로 워크플로에 대한 자세한 내용은 [Express 경로 워크플로](expressroute-workflows.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="856e2-237">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="856e2-238">회로 피어링에 대한 자세한 내용은 [Express 경로 회로 및 라우팅 도메인](expressroute-circuit-peerings.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="856e2-238">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="856e2-239">가상 네트워크 작업에 대한 자세한 내용은 [가상 네트워크 개요](../virtual-network/virtual-networks-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="856e2-239">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>
