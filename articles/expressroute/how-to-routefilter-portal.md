---
title: "Azure ExpressRoute Microsoft 피어링에 대한 경로 필터 구성: Portal | Microsoft Docs"
description: "이 문서에서는 Azure Portal을 사용하여 Microsoft 피어링에 대한 경로 필터를 구성하는 방법을 설명합니다."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/25/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: f17bf3e475a33cfc617e8a026e9606b3792101f3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="configure-route-filters-for-microsoft-peering"></a><span data-ttu-id="b3c3a-103">Microsoft 피어링에 대한 경로 필터 구성</span><span class="sxs-lookup"><span data-stu-id="b3c3a-103">Configure route filters for Microsoft peering</span></span>

<span data-ttu-id="b3c3a-104">경로 필터는 Microsoft 피어링을 통해 지원되는 서비스의 하위 집합을 사용하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-104">Route filters are a way to consume a subset of supported services through Microsoft peering.</span></span> <span data-ttu-id="b3c3a-105">이 문서의 단계는 ExpressRoute 회로에 대한 경로 필터를 구성하고 관리하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-105">The steps in this article help you configure and manage route filters for ExpressRoute circuits.</span></span>

<span data-ttu-id="b3c3a-106">Dynamics 365 서비스 및 Exchange Online, SharePoint Online 및 비즈니스용 Skype와 같은 Office 365 서비스는 Microsoft 피어링을 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-106">Dynamics 365 services, and Office 365 services such as Exchange Online, SharePoint Online, and Skype for Business, are accessible through the Microsoft peering.</span></span> <span data-ttu-id="b3c3a-107">Microsoft 피어링이 ExpressRoute 회로에 구성되면 설정된 BGP 세션을 통해 이러한 서비스와 관련된 모든 접두사가 보급됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-107">When Microsoft peering is configured in an ExpressRoute circuit, all prefixes related to these services are advertised through the BGP sessions that are established.</span></span> <span data-ttu-id="b3c3a-108">BGP 커뮤니티 값은 접두사를 통해 제공되는 서비스를 식별하는 모든 접두사에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-108">A BGP community value is attached to every prefix to identify the service that is offered through the prefix.</span></span> <span data-ttu-id="b3c3a-109">BGP 커뮤니티 값과 매핑되는 서비스의 목록은 [BGP 커뮤니티](expressroute-routing.md#bgp)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-109">For a list of the BGP community values and the services they  map to, see [BGP communities](expressroute-routing.md#bgp).</span></span>

<span data-ttu-id="b3c3a-110">모든 서비스에 연결해야 하는 경우 많은 수의 접두사가 BGP를 통해 보급됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-110">If you require connectivity to all services, a large number of prefixes are advertised through BGP.</span></span> <span data-ttu-id="b3c3a-111">그러면 네트워크 내의 라우터에서 유지 관리되는 경로 테이블의 크기가 상당히 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-111">This significantly increases the size of the route tables maintained by routers within your network.</span></span> <span data-ttu-id="b3c3a-112">Microsoft 피어링을 통해 제공되는 서비스의 하위 집합만 사용하려는 경우 두 가지 방법으로 경로 테이블의 크기를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-112">If you plan to consume only a subset of services offered through Microsoft peering, you can reduce the size of your route tables in two ways.</span></span> <span data-ttu-id="b3c3a-113">다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-113">You can:</span></span>

- <span data-ttu-id="b3c3a-114">BGP 커뮤니티에 라우팅 필터를 적용하여 필요 없는 접두사를 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-114">Filter out unwanted prefixes by applying route filters on BGP communities.</span></span> <span data-ttu-id="b3c3a-115">표준 네트워킹 방법은 많은 네트워크 내에서 일반적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-115">This is a standard networking practice and is used commonly within many networks.</span></span>

- <span data-ttu-id="b3c3a-116">경로 필터를 정의하고 ExpressRoute 회로에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-116">Define route filters and apply them to your ExpressRoute circuit.</span></span> <span data-ttu-id="b3c3a-117">경로 필터는 Microsoft 피어링을 통해 사용하려는 서비스 목록을 선택할 수 있는 새 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-117">A route filter is a new resource that lets you select the list of services you plan to consume through Microsoft peering.</span></span> <span data-ttu-id="b3c3a-118">ExpressRoute 라우터는 경로 필터에서 식별된 서비스에 속하는 접두사 목록만을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-118">ExpressRoute routers only send the list of prefixes that belong to the services identified in the route filter.</span></span>

### <span data-ttu-id="b3c3a-119"><a name="about"></a>경로 필터 정보</span><span class="sxs-lookup"><span data-stu-id="b3c3a-119"><a name="about"></a>About route filters</span></span>

<span data-ttu-id="b3c3a-120">Microsoft 피어링이 ExpressRoute 회로에 구성되면 Microsoft 에지 라우터는 에지 라우터(사용자 또는 연결 공급자 소유)를 사용하여 한 쌍의 BGP 세션을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-120">When Microsoft peering is configured on your ExpressRoute circuit, the Microsoft edge routers establish a pair of BGP sessions with the edge routers (yours or your connectivity provider's).</span></span> <span data-ttu-id="b3c3a-121">경로는 네트워크에 보급되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-121">No routes are advertised to your network.</span></span> <span data-ttu-id="b3c3a-122">네트워크에 경로 보급을 사용하려면 경로 필터를 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-122">To enable route advertisements to your network, you must associate a route filter.</span></span>

<span data-ttu-id="b3c3a-123">경로 필터를 사용하면 ExpressRoute 회로의 Microsoft 피어링을 통해 사용하려는 서비스를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-123">A route filter lets you identify services you want to consume through your ExpressRoute circuit's Microsoft peering.</span></span> <span data-ttu-id="b3c3a-124">특히 모든 BGP 커뮤니티 값의 허용 목록입니다</span><span class="sxs-lookup"><span data-stu-id="b3c3a-124">It is essentially a white list of all the BGP community values.</span></span> <span data-ttu-id="b3c3a-125">경로 필터 리소스가 정의되고 ExpressRoute 회로에 연결되면 BGP 커뮤니티 값에 매핑되는 모든 접두사는 네트워크에 보급됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-125">Once a route filter resource is defined and attached to an ExpressRoute circuit, all prefixes that map to the BGP community values are advertised to your network.</span></span>

<span data-ttu-id="b3c3a-126">경로 필터를 Office 365 서비스에 연결할 수 있으려면 ExpressRoute를 통해 Office 365 서비스를 사용할 수 있는 권한이 부여되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-126">To be able to attach route filters with Office 365 services on them, you must have authorization to consume Office 365 services through ExpressRoute.</span></span> <span data-ttu-id="b3c3a-127">ExpressRoute를 통해 Office 365 서비스를 사용할 수 있는 권한이 없는 경우 경로 필터를 연결하는 작업에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-127">If you are not authorized to consume Office 365 services through ExpressRoute, the operation to attach route filters fails.</span></span> <span data-ttu-id="b3c3a-128">권한 부여 프로세스에 대한 자세한 내용은 [Office 365용 Azure ExpressRoute](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-128">For more information about the authorization process, see [Azure ExpressRoute for Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span></span> <span data-ttu-id="b3c3a-129">Dynamics 365 서비스에 대한 연결에는 사전 권한 부여가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-129">Connectivity to Dynamics 365 services does NOT require any prior authorization.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b3c3a-130">경로 필터를 정의하지 않은 경우에도 2017년 8월 1일 이전에 구성된 ExpressRoute 회로의 Microsoft 피어링에는 Microsoft 피어링을 통해 보급된 모든 서비스 접두사가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-130">Microsoft peering of ExpressRoute circuits that were configured prior to August 1, 2017 will have all service prefixes advertised through Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="b3c3a-131">2017년 8월 1일 이후에 구성된 ExpressRoute 회로의 Microsoft 피어링에는 경로 필터가 회로에 연결될 때까지 접두사가 보급되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-131">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached to the circuit.</span></span>
> 
> 

### <span data-ttu-id="b3c3a-132"><a name="workflow"></a>워크플로</span><span class="sxs-lookup"><span data-stu-id="b3c3a-132"><a name="workflow"></a>Workflow</span></span>

<span data-ttu-id="b3c3a-133">Microsoft 피어링을 통해 서비스에 성공적으로 연결할 수 있으려면 다음 구성 단계를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-133">To be able to successfully connect to services through Microsoft peering, you must complete the following configuration steps:</span></span>

- <span data-ttu-id="b3c3a-134">Microsoft 피어링을 프로비전하는 활성 ExpressRoute 회로가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-134">You must have an active ExpressRoute circuit that has Microsoft peering provisioned.</span></span> <span data-ttu-id="b3c3a-135">다음 지침을 사용하여 이러한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-135">You can use the following instructions to accomplish these tasks:</span></span>
  - <span data-ttu-id="b3c3a-136">[ExpressRoute 회로를 만들고](expressroute-howto-circuit-portal-resource-manager.md) 진행하기 전에 연결 공급자를 통해 회로를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-136">[Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="b3c3a-137">ExpressRoute 회로는 프로비전되고 활성화된 상태여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-137">The ExpressRoute circuit must be in a provisioned and enabled state.</span></span>
  - <span data-ttu-id="b3c3a-138">직접 BGP 세션을 관리하는 경우 [Microsoft 피어링을 만듭니다](expressroute-howto-routing-portal-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="b3c3a-138">[Create Microsoft peering](expressroute-howto-routing-portal-resource-manager.md) if you manage the BGP session directly.</span></span> <span data-ttu-id="b3c3a-139">또는 연결 공급자가 회로에 Microsoft 피어링을 프로비전하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-139">Or, have your connectivity provider provision Microsoft peering for your circuit.</span></span>

-  <span data-ttu-id="b3c3a-140">경로 필터를 만들고 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-140">You must create and configure a route filter.</span></span>
    - <span data-ttu-id="b3c3a-141">Microsoft 피어링을 통해 사용하려는 서비스를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-141">Identify the services you with to consume through Microsoft peering</span></span>
    - <span data-ttu-id="b3c3a-142">서비스와 연결된 BGP 커뮤니티 값의 목록을 식별합니다</span><span class="sxs-lookup"><span data-stu-id="b3c3a-142">Identify the list of BGP community values associated with the services</span></span>
    - <span data-ttu-id="b3c3a-143">BGP 커뮤니티 값과 일치하는 접두사 목록을 허용하는 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-143">Create a rule to allow the prefix list matching the BGP community values</span></span>

-  <span data-ttu-id="b3c3a-144">경로 필터를 ExpressRoute 회로에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-144">You must attach the route filter to the ExpressRoute circuit.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b3c3a-145">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="b3c3a-145">Before you begin</span></span>

<span data-ttu-id="b3c3a-146">구성을 시작하기 전에 다음 조건을 충족하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-146">Before you begin configuration, make sure you meet the following criteria:</span></span>

 - <span data-ttu-id="b3c3a-147">구성을 시작하기 전에 [필수 조건](expressroute-prerequisites.md) 및 [워크플로](expressroute-workflows.md)를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-147">Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

 - <span data-ttu-id="b3c3a-148">활성화된 Express 경로 회로가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-148">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="b3c3a-149">지침을 수행하여 [Express 경로 회로를 만들고](expressroute-howto-circuit-portal-resource-manager.md) 진행하기 전에 연결 공급자를 통해 회로를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-149">Follow the instructions to [Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="b3c3a-150">ExpressRoute 회로는 프로비전되고 활성화된 상태여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-150">The ExpressRoute circuit must be in a provisioned and enabled state.</span></span>

 - <span data-ttu-id="b3c3a-151">활성 Microsoft 피어링이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-151">You must have an active Microsoft peering.</span></span> <span data-ttu-id="b3c3a-152">[피어링 구성 수정 및 만들기](expressroute-howto-routing-portal-resource-manager.md)의 지침에 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-152">Follow instructions at [Create and modifying peering configuration](expressroute-howto-routing-portal-resource-manager.md)</span></span>


## <span data-ttu-id="b3c3a-153"><a name="prefixes"></a>1단계.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-153"><a name="prefixes"></a>Step 1.</span></span> <span data-ttu-id="b3c3a-154">접두사 및 BGP 커뮤니티 값의 목록 가져오기</span><span class="sxs-lookup"><span data-stu-id="b3c3a-154">Get a list of prefixes and BGP community values</span></span>

### <a name="1-get-a-list-of-bgp-community-values"></a><span data-ttu-id="b3c3a-155">1. BGP 커뮤니티 값의 목록 가져오기</span><span class="sxs-lookup"><span data-stu-id="b3c3a-155">1. Get a list of BGP community values</span></span>

<span data-ttu-id="b3c3a-156">Microsoft 피어링을 통해 액세스할 수 있는 서비스와 관련된 BGP 커뮤니티 값은 [ExpressRoute 라우팅 요구 사항](expressroute-routing.md) 페이지에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-156">BGP community values associated with services accessible through Microsoft peering is available in the [ExpressRoute routing requirements](expressroute-routing.md) page.</span></span>

### <a name="2-make-a-list-of-the-values-that-you-want-to-use"></a><span data-ttu-id="b3c3a-157">2. 사용하려는 값의 목록 확인</span><span class="sxs-lookup"><span data-stu-id="b3c3a-157">2. Make a list of the values that you want to use</span></span>

<span data-ttu-id="b3c3a-158">경로 필터에 사용하려는 BGP 커뮤니티 값 목록을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-158">Make a list of BGP community values you want to use in the route filter.</span></span> <span data-ttu-id="b3c3a-159">예를 들어, Dynamics 365 서비스의 BGP 커뮤니티 값은 12076:5040입니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-159">As an example, the BGP community value for Dynamics 365 services is 12076:5040.</span></span>

## <span data-ttu-id="b3c3a-160"><a name="filter"></a>2단계.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-160"><a name="filter"></a>Step 2.</span></span> <span data-ttu-id="b3c3a-161">경로 필터 및 필터 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="b3c3a-161">Create a route filter and a filter rule</span></span>

<span data-ttu-id="b3c3a-162">경로 필터에는 하나의 규칙만이 있을 수 있고 규칙은 '허용' 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-162">A route filter can have only one rule, and the rule must be of type 'Allow'.</span></span> <span data-ttu-id="b3c3a-163">이 규칙에는 관련된 BGP 커뮤니티 값의 목록이 있을 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="b3c3a-163">This rule can have a list of BGP community values associated with it.</span></span>

### <a name="1-create-a-route-filter"></a><span data-ttu-id="b3c3a-164">1. 경로 필터 만들기</span><span class="sxs-lookup"><span data-stu-id="b3c3a-164">1. Create a route filter</span></span>
<span data-ttu-id="b3c3a-165">새 리소스를 만드는 옵션을 선택하여 경로 필터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-165">You can create a route filter by selecting the option to create a new resource.</span></span> <span data-ttu-id="b3c3a-166">다음 이미지에 표시된 대로, **새로 만들기** > **네트워킹** > **RouteFilter**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-166">Click **New** > **Networking** > **RouteFilter**, as shown in the following image:</span></span>

![경로 필터 만들기](.\media\how-to-routefilter-portal\CreateRouteFilter1.png)

<span data-ttu-id="b3c3a-168">경로 필터를 리소스 그룹에 배치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-168">You must place the route filter in a resource group.</span></span> 

![경로 필터 만들기](.\media\how-to-routefilter-portal\CreateRouteFilter.png)

### <a name="2-create-a-filter-rule"></a><span data-ttu-id="b3c3a-170">2. 필터 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="b3c3a-170">2. Create a filter rule</span></span>

<span data-ttu-id="b3c3a-171">경로 필터에 대한 관리 규칙 탭을 선택하여 규칙을 추가하고 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-171">You can add and update rules by selecting the manage rule tab for your route filter.</span></span>

![경로 필터 만들기](.\media\how-to-routefilter-portal\ManageRouteFilter.png)


<span data-ttu-id="b3c3a-173">드롭다운 목록에서 연결할 서비스를 선택하고 완료한 후에 규칙을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-173">You can select the services you want to connect to from the drop down list and save the rule when done.</span></span>

![경로 필터 만들기](.\media\how-to-routefilter-portal\AddRouteFilterRule.png)


## <span data-ttu-id="b3c3a-175"><a name="attach"></a>3단계.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-175"><a name="attach"></a>Step 3.</span></span> <span data-ttu-id="b3c3a-176">경로 필터를 ExpressRoute 회로에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-176">Attach the route filter to an ExpressRoute circuit</span></span>

<span data-ttu-id="b3c3a-177">“회로 추가” 단추를 선택하고 드롭다운 목록에서 ExpressRoute 회로를 선택하여 경로 필터를 회로에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-177">You can attach the route filter to a circuit by selecting the "add Circuit" button and selecting the ExpressRoute circuit from the drop down list.</span></span>

![경로 필터 만들기](.\media\how-to-routefilter-portal\AddCktToRouteFilter.png)

## <span data-ttu-id="b3c3a-179"><a name="getproperties"></a>경로 필터의 속성을 가져오려면</span><span class="sxs-lookup"><span data-stu-id="b3c3a-179"><a name="getproperties"></a>To get the properties of a route filter</span></span>

<span data-ttu-id="b3c3a-180">포털에서 리소스를 열 때 경로 필터의 속성을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-180">You can view properties of a route filter when you open the resource in the portal.</span></span>

![경로 필터 만들기](.\media\how-to-routefilter-portal\ViewRouteFilter.png)


## <span data-ttu-id="b3c3a-182"><a name="updateproperties"></a>경로 필터의 속성을 업데이트하려면</span><span class="sxs-lookup"><span data-stu-id="b3c3a-182"><a name="updateproperties"></a>To update the properties of a route filter</span></span>

<span data-ttu-id="b3c3a-183">“관리 규칙” 단추를 선택하여 회로에 연결된 BGP 커뮤니티 값 목록을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-183">You can update the list of BGP community values attached to a circuit by selecting the "Manage rule" button.</span></span>


![경로 필터 만들기](.\media\how-to-routefilter-portal\ManageRouteFilter.png)

![경로 필터 만들기](.\media\how-to-routefilter-portal\AddRouteFilterRule.png) 


## <span data-ttu-id="b3c3a-186"><a name="detach"></a>ExpressRoute 회로에서 경로 필터를 분리하려면</span><span class="sxs-lookup"><span data-stu-id="b3c3a-186"><a name="detach"></a>To detach a route filter from an ExpressRoute circuit</span></span>

<span data-ttu-id="b3c3a-187">경로 필터에서 회로를 분리하려면 회로를 마우스 오른쪽 단추로 클릭하고 "연결 해제"를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-187">To detach a circuit from the route filter, right click on the circuit and click on "disassociate".</span></span>

![경로 필터 만들기](.\media\how-to-routefilter-portal\DetachRouteFilter.png) 


## <span data-ttu-id="b3c3a-189"><a name="delete"></a>경로 필터를 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="b3c3a-189"><a name="delete"></a>To delete a route filter</span></span>

<span data-ttu-id="b3c3a-190">삭제 단추를 선택하여 경로 필터를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-190">You can delete a route filter by selecting the delete button.</span></span> 

![경로 필터 만들기](.\media\how-to-routefilter-portal\DeleteRouteFilter.png) 

## <a name="next-steps"></a><span data-ttu-id="b3c3a-192">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b3c3a-192">Next steps</span></span>

<span data-ttu-id="b3c3a-193">ExpressRoute에 대한 자세한 내용은 [ExpressRoute FAQ](expressroute-faqs.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b3c3a-193">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>