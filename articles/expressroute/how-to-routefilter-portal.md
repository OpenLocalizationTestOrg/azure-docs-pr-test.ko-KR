---
title: "Azure ExpressRoute Microsoft 피어링에 대한 경로 필터 구성: Portal | Microsoft Docs"
description: "이 문서에서 설명 하는 방법을 사용 하 여 Microsoft 피어 링에 대 한 경로 필터 tooconfigure hello Azure 포털"
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
ms.openlocfilehash: 2a47d465ec5f175d9510cef94606f70f036f0862
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-route-filters-for-microsoft-peering"></a><span data-ttu-id="08a3d-103">Microsoft 피어링에 대한 경로 필터 구성</span><span class="sxs-lookup"><span data-stu-id="08a3d-103">Configure route filters for Microsoft peering</span></span>

<span data-ttu-id="08a3d-104">경로 필터는 방식으로 tooconsume Microsoft 피어 링을 통해 지원 되는 서비스의 하위 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-104">Route filters are a way tooconsume a subset of supported services through Microsoft peering.</span></span> <span data-ttu-id="08a3d-105">이 문서 도움말 구성 하 고 ExpressRoute 회로 대 한 경로 필터 관리에 hello 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-105">hello steps in this article help you configure and manage route filters for ExpressRoute circuits.</span></span>

<span data-ttu-id="08a3d-106">Dynamics 365 서비스 및 비즈니스에 대 한 Exchange Online, SharePoint Online 및 Skype와 같은 Office 365 서비스는 hello Microsoft 피어 링을 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-106">Dynamics 365 services, and Office 365 services such as Exchange Online, SharePoint Online, and Skype for Business, are accessible through hello Microsoft peering.</span></span> <span data-ttu-id="08a3d-107">Microsoft 피어 링 express 경로 회로에 구성 되 면 모든 접두사 관련된 toothese 서비스는 설정 된 hello BGP 세션을 통해 보급 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-107">When Microsoft peering is configured in an ExpressRoute circuit, all prefixes related toothese services are advertised through hello BGP sessions that are established.</span></span> <span data-ttu-id="08a3d-108">BGP 커뮤니티 값은 연결 된 tooevery 접두사 tooidentify hello 서비스 hello 접두사를 통해 제공 된입니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-108">A BGP community value is attached tooevery prefix tooidentify hello service that is offered through hello prefix.</span></span> <span data-ttu-id="08a3d-109">Hello BGP 커뮤니티 값과 매핑되는 hello 서비스의 목록에 대 한 참조 [BGP 커뮤니티](expressroute-routing.md#bgp)합니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-109">For a list of hello BGP community values and hello services they  map to, see [BGP communities](expressroute-routing.md#bgp).</span></span>

<span data-ttu-id="08a3d-110">연결 tooall 서비스를 필요로 하는 경우 많은 수의 접두사는 BGP를 통해 보급 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-110">If you require connectivity tooall services, a large number of prefixes are advertised through BGP.</span></span> <span data-ttu-id="08a3d-111">이 네트워크 라우터에서 관리 hello 경로 테이블의 hello 크기 크게 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-111">This significantly increases hello size of hello route tables maintained by routers within your network.</span></span> <span data-ttu-id="08a3d-112">Microsoft 피어 링을 통해 제공 되는 서비스의 하위 집합만 tooconsume 하려는 경우 두 가지 방법으로 경로 테이블의 hello 크기를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-112">If you plan tooconsume only a subset of services offered through Microsoft peering, you can reduce hello size of your route tables in two ways.</span></span> <span data-ttu-id="08a3d-113">다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-113">You can:</span></span>

- <span data-ttu-id="08a3d-114">BGP 커뮤니티에 라우팅 필터를 적용하여 필요 없는 접두사를 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-114">Filter out unwanted prefixes by applying route filters on BGP communities.</span></span> <span data-ttu-id="08a3d-115">표준 네트워킹 방법은 많은 네트워크 내에서 일반적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-115">This is a standard networking practice and is used commonly within many networks.</span></span>

- <span data-ttu-id="08a3d-116">경로 필터를 정의 하 고 tooyour ExpressRoute 회로 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-116">Define route filters and apply them tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="08a3d-117">경로 필터는 새 리소스의 hello 목록을 선택할 수 있습니다 서비스를 Microsoft 피어 링을 통해 tooconsume 계획입니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-117">A route filter is a new resource that lets you select hello list of services you plan tooconsume through Microsoft peering.</span></span> <span data-ttu-id="08a3d-118">ExpressRoute 라우터는만 hello hello 경로 필터에서 식별 된 toohello 서비스에 속하는 접두사 목록을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-118">ExpressRoute routers only send hello list of prefixes that belong toohello services identified in hello route filter.</span></span>

### <span data-ttu-id="08a3d-119"><a name="about"></a>경로 필터 정보</span><span class="sxs-lookup"><span data-stu-id="08a3d-119"><a name="about"></a>About route filters</span></span>

<span data-ttu-id="08a3d-120">Microsoft 피어 링 express 경로 회로에 구성 되 면 hello Microsoft에 지 라우터는 한 쌍의 BGP 세션을 원하는 대로 이동해 왔거나 연결 공급자의에 지 라우터를 hello 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-120">When Microsoft peering is configured on your ExpressRoute circuit, hello Microsoft edge routers establish a pair of BGP sessions with hello edge routers (yours or your connectivity provider's).</span></span> <span data-ttu-id="08a3d-121">경로가 보급된 tooyour 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-121">No routes are advertised tooyour network.</span></span> <span data-ttu-id="08a3d-122">tooenable 경로 광고 tooyour 네트워크 경로 필터를 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-122">tooenable route advertisements tooyour network, you must associate a route filter.</span></span>

<span data-ttu-id="08a3d-123">경로 필터를 사용 하면 ExpressRoute 회로 Microsoft 피어 링을 통해 tooconsume 서비스를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-123">A route filter lets you identify services you want tooconsume through your ExpressRoute circuit's Microsoft peering.</span></span> <span data-ttu-id="08a3d-124">모든 hello BGP 커뮤니티 값의 허용 목록을 경우합니다</span><span class="sxs-lookup"><span data-stu-id="08a3d-124">It is essentially a white list of all hello BGP community values.</span></span> <span data-ttu-id="08a3d-125">경로 필터 리소스 정의 tooan ExpressRoute 회로 연결 되 면 toohello BGP 커뮤니티 값에 매핑되는 모든 접두사는 보급된 tooyour 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-125">Once a route filter resource is defined and attached tooan ExpressRoute circuit, all prefixes that map toohello BGP community values are advertised tooyour network.</span></span>

<span data-ttu-id="08a3d-126">Office 365 서비스에 toobe 수 tooattach 경로 필터, ExpressRoute 통해 권한 부여 tooconsume Office 365 서비스 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-126">toobe able tooattach route filters with Office 365 services on them, you must have authorization tooconsume Office 365 services through ExpressRoute.</span></span> <span data-ttu-id="08a3d-127">ExpressRoute 통해 권한 있는 tooconsume Office 365 서비스에 없으면 hello 작업 tooattach 경로 필터 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-127">If you are not authorized tooconsume Office 365 services through ExpressRoute, hello operation tooattach route filters fails.</span></span> <span data-ttu-id="08a3d-128">Hello 권한 부여 프로세스에 대 한 자세한 내용은 참조 [Office 365에 대 한 Azure ExpressRoute](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd)합니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-128">For more information about hello authorization process, see [Azure ExpressRoute for Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span></span> <span data-ttu-id="08a3d-129">연결 tooDynamics 365 서비스에 모든 권한을 가지 지 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-129">Connectivity tooDynamics 365 services does NOT require any prior authorization.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="08a3d-130">이전 tooAugust 1에 구성 된 ExpressRoute 회로의 Microsoft 피어 링, 경로 필터 정의 되어 있지 않은 경우에 2017 Microsoft 피어 링을 통해 보급 되는 모든 서비스 접두사를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-130">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="08a3d-131">Microsoft 또는 그 이후에 2017 년 8 월 1 구성한 ExpressRoute 회로의 피어 링 수는 없습니다 모든 접두사 필터는 연결 될 때까지 보급 toohello 회로 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-131">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span>
> 
> 

### <span data-ttu-id="08a3d-132"><a name="workflow"></a>워크플로</span><span class="sxs-lookup"><span data-stu-id="08a3d-132"><a name="workflow"></a>Workflow</span></span>

<span data-ttu-id="08a3d-133">toobe 수 toosuccessfully Microsoft 피어 링을 통해 tooservices 연결, hello 다음 구성 단계를 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-133">toobe able toosuccessfully connect tooservices through Microsoft peering, you must complete hello following configuration steps:</span></span>

- <span data-ttu-id="08a3d-134">Microsoft 피어링을 프로비전하는 활성 ExpressRoute 회로가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-134">You must have an active ExpressRoute circuit that has Microsoft peering provisioned.</span></span> <span data-ttu-id="08a3d-135">이러한 작업 지침 tooaccomplish 다음 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-135">You can use hello following instructions tooaccomplish these tasks:</span></span>
  - <span data-ttu-id="08a3d-136">[ExpressRoute 회로 만들기](expressroute-howto-circuit-portal-resource-manager.md) 있고 계속 hello 회로 하기 전에 연결 공급자가 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-136">[Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="08a3d-137">ExpressRoute 회로 hello 가능 하 고 프로 비전 된 상태에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-137">hello ExpressRoute circuit must be in a provisioned and enabled state.</span></span>
  - <span data-ttu-id="08a3d-138">[Microsoft 피어 링 만들기](expressroute-howto-routing-portal-resource-manager.md) 직접 hello BGP 세션을 관리 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="08a3d-138">[Create Microsoft peering](expressroute-howto-routing-portal-resource-manager.md) if you manage hello BGP session directly.</span></span> <span data-ttu-id="08a3d-139">또는 연결 공급자가 회로에 Microsoft 피어링을 프로비전하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-139">Or, have your connectivity provider provision Microsoft peering for your circuit.</span></span>

-  <span data-ttu-id="08a3d-140">경로 필터를 만들고 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-140">You must create and configure a route filter.</span></span>
    - <span data-ttu-id="08a3d-141">식별 hello tooconsume Microsoft 피어 링을 통해 서비스</span><span class="sxs-lookup"><span data-stu-id="08a3d-141">Identify hello services you with tooconsume through Microsoft peering</span></span>
    - <span data-ttu-id="08a3d-142">Hello 서비스와 관련 된 BGP 커뮤니티 값의 hello 목록 확인</span><span class="sxs-lookup"><span data-stu-id="08a3d-142">Identify hello list of BGP community values associated with hello services</span></span>
    - <span data-ttu-id="08a3d-143">한 규칙 tooallow hello 접두사 목록 일치 하는 hello BGP 커뮤니티 값을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-143">Create a rule tooallow hello prefix list matching hello BGP community values</span></span>

-  <span data-ttu-id="08a3d-144">Hello 경로 필터 toohello ExpressRoute 회로 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-144">You must attach hello route filter toohello ExpressRoute circuit.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="08a3d-145">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="08a3d-145">Before you begin</span></span>

<span data-ttu-id="08a3d-146">구성을 시작 하기 전에 hello 다음 조건을 충족 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-146">Before you begin configuration, make sure you meet hello following criteria:</span></span>

 - <span data-ttu-id="08a3d-147">검토 hello [필수 구성 요소](expressroute-prerequisites.md) 및 [워크플로](expressroute-workflows.md) 구성을 시작 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="08a3d-147">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

 - <span data-ttu-id="08a3d-148">활성화된 Express 경로 회로가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-148">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="08a3d-149">너무 hello 지침에 따라[ExpressRoute 회로 만들기](expressroute-howto-circuit-portal-resource-manager.md) 있고 계속 hello 회로 하기 전에 연결 공급자가 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-149">Follow hello instructions too[Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="08a3d-150">ExpressRoute 회로 hello 가능 하 고 프로 비전 된 상태에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-150">hello ExpressRoute circuit must be in a provisioned and enabled state.</span></span>

 - <span data-ttu-id="08a3d-151">활성 Microsoft 피어링이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-151">You must have an active Microsoft peering.</span></span> <span data-ttu-id="08a3d-152">[피어링 구성 수정 및 만들기](expressroute-howto-routing-portal-resource-manager.md)의 지침에 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-152">Follow instructions at [Create and modifying peering configuration](expressroute-howto-routing-portal-resource-manager.md)</span></span>


## <span data-ttu-id="08a3d-153"><a name="prefixes"></a>1단계.</span><span class="sxs-lookup"><span data-stu-id="08a3d-153"><a name="prefixes"></a>Step 1.</span></span> <span data-ttu-id="08a3d-154">접두사 및 BGP 커뮤니티 값의 목록 가져오기</span><span class="sxs-lookup"><span data-stu-id="08a3d-154">Get a list of prefixes and BGP community values</span></span>

### <a name="1-get-a-list-of-bgp-community-values"></a><span data-ttu-id="08a3d-155">1. BGP 커뮤니티 값의 목록 가져오기</span><span class="sxs-lookup"><span data-stu-id="08a3d-155">1. Get a list of BGP community values</span></span>

<span data-ttu-id="08a3d-156">Microsoft 피어 링을 통해 액세스할 수 있는 서비스와 관련 된 BGP 커뮤니티 값은 hello 영어로 [ExpressRoute 라우팅 요구 사항](expressroute-routing.md) 페이지.</span><span class="sxs-lookup"><span data-stu-id="08a3d-156">BGP community values associated with services accessible through Microsoft peering is available in hello [ExpressRoute routing requirements](expressroute-routing.md) page.</span></span>

### <a name="2-make-a-list-of-hello-values-that-you-want-toouse"></a><span data-ttu-id="08a3d-157">2. 원하는 toouse hello 값 목록을 확인합니다</span><span class="sxs-lookup"><span data-stu-id="08a3d-157">2. Make a list of hello values that you want toouse</span></span>

<span data-ttu-id="08a3d-158">Hello 경로 필터에 원하는 BGP 커뮤니티 값 목록이 toouse을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-158">Make a list of BGP community values you want toouse in hello route filter.</span></span> <span data-ttu-id="08a3d-159">예를 들어 hello Dynamics 365 서비스에 대 한 BGP 커뮤니티 값 12076:5040 됩니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-159">As an example, hello BGP community value for Dynamics 365 services is 12076:5040.</span></span>

## <span data-ttu-id="08a3d-160"><a name="filter"></a>2단계.</span><span class="sxs-lookup"><span data-stu-id="08a3d-160"><a name="filter"></a>Step 2.</span></span> <span data-ttu-id="08a3d-161">경로 필터 및 필터 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="08a3d-161">Create a route filter and a filter rule</span></span>

<span data-ttu-id="08a3d-162">경로 필터 규칙을 하나만 가질 수 있습니다 및 hello 규칙 '허용' 형식 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-162">A route filter can have only one rule, and hello rule must be of type 'Allow'.</span></span> <span data-ttu-id="08a3d-163">이 규칙에는 관련된 BGP 커뮤니티 값의 목록이 있을 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="08a3d-163">This rule can have a list of BGP community values associated with it.</span></span>

### <a name="1-create-a-route-filter"></a><span data-ttu-id="08a3d-164">1. 경로 필터 만들기</span><span class="sxs-lookup"><span data-stu-id="08a3d-164">1. Create a route filter</span></span>
<span data-ttu-id="08a3d-165">만들 수 있습니다 경로 필터 hello 옵션 toocreate를 선택 하 여 새 리소스.</span><span class="sxs-lookup"><span data-stu-id="08a3d-165">You can create a route filter by selecting hello option toocreate a new resource.</span></span> <span data-ttu-id="08a3d-166">클릭 **새로** > **네트워킹** > **RouteFilter**hello 다음 이미지에에서 나타난 것 처럼:</span><span class="sxs-lookup"><span data-stu-id="08a3d-166">Click **New** > **Networking** > **RouteFilter**, as shown in hello following image:</span></span>

![경로 필터 만들기](.\media\how-to-routefilter-portal\CreateRouteFilter1.png)

<span data-ttu-id="08a3d-168">리소스 그룹의 hello 경로 필터를 배치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-168">You must place hello route filter in a resource group.</span></span> 

![경로 필터 만들기](.\media\how-to-routefilter-portal\CreateRouteFilter.png)

### <a name="2-create-a-filter-rule"></a><span data-ttu-id="08a3d-170">2. 필터 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="08a3d-170">2. Create a filter rule</span></span>

<span data-ttu-id="08a3d-171">추가 하 고 hello를 선택 하 여 업데이트 규칙 관리 경로 필터에 대 한 규칙 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-171">You can add and update rules by selecting hello manage rule tab for your route filter.</span></span>

![경로 필터 만들기](.\media\how-to-routefilter-portal\ManageRouteFilter.png)


<span data-ttu-id="08a3d-173">Tooconnect toofrom hello 서비스를 드롭다운 목록 및 완료 한 후에 hello 규칙을 저장 하는 hello를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-173">You can select hello services you want tooconnect toofrom hello drop down list and save hello rule when done.</span></span>

![경로 필터 만들기](.\media\how-to-routefilter-portal\AddRouteFilterRule.png)


## <span data-ttu-id="08a3d-175"><a name="attach"></a>3단계.</span><span class="sxs-lookup"><span data-stu-id="08a3d-175"><a name="attach"></a>Step 3.</span></span> <span data-ttu-id="08a3d-176">Hello 경로 필터 tooan ExpressRoute 회로 연결</span><span class="sxs-lookup"><span data-stu-id="08a3d-176">Attach hello route filter tooan ExpressRoute circuit</span></span>

<span data-ttu-id="08a3d-177">Hello "회로 추가" 단추를 선택 하 고 hello 드롭다운 목록에서에서 hello ExpressRoute 회로 선택 하 여 hello 경로 필터 tooa 회로 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-177">You can attach hello route filter tooa circuit by selecting hello "add Circuit" button and selecting hello ExpressRoute circuit from hello drop down list.</span></span>

![경로 필터 만들기](.\media\how-to-routefilter-portal\AddCktToRouteFilter.png)

## <span data-ttu-id="08a3d-179"><a name="getproperties"></a>경로 필터의 tooget hello 속성</span><span class="sxs-lookup"><span data-stu-id="08a3d-179"><a name="getproperties"></a>tooget hello properties of a route filter</span></span>

<span data-ttu-id="08a3d-180">Hello 포털에서 hello 리소스를 열 때 경로 필터의 속성을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-180">You can view properties of a route filter when you open hello resource in hello portal.</span></span>

![경로 필터 만들기](.\media\how-to-routefilter-portal\ViewRouteFilter.png)


## <span data-ttu-id="08a3d-182"><a name="updateproperties"></a>경로 필터의 tooupdate hello 속성</span><span class="sxs-lookup"><span data-stu-id="08a3d-182"><a name="updateproperties"></a>tooupdate hello properties of a route filter</span></span>

<span data-ttu-id="08a3d-183">규칙 hello"관리" 단추를 선택 하 여 BGP 커뮤니티 값 연결 된 tooa 회로의 hello 목록을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-183">You can update hello list of BGP community values attached tooa circuit by selecting hello "Manage rule" button.</span></span>


![경로 필터 만들기](.\media\how-to-routefilter-portal\ManageRouteFilter.png)

![경로 필터 만들기](.\media\how-to-routefilter-portal\AddRouteFilterRule.png) 


## <span data-ttu-id="08a3d-186"><a name="detach"></a>ExpressRoute 회로에서 경로 필터 toodetach</span><span class="sxs-lookup"><span data-stu-id="08a3d-186"><a name="detach"></a>toodetach a route filter from an ExpressRoute circuit</span></span>

<span data-ttu-id="08a3d-187">hello 경로 필터에서 회로 toodetach hello 회로 마우스 오른쪽 단추로 클릭 하 고 "끊을"에서 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-187">toodetach a circuit from hello route filter, right click on hello circuit and click on "disassociate".</span></span>

![경로 필터 만들기](.\media\how-to-routefilter-portal\DetachRouteFilter.png) 


## <span data-ttu-id="08a3d-189"><a name="delete"></a>경로 필터 toodelete</span><span class="sxs-lookup"><span data-stu-id="08a3d-189"><a name="delete"></a>toodelete a route filter</span></span>

<span data-ttu-id="08a3d-190">Hello 삭제 단추를 선택 하 여 필터를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-190">You can delete a route filter by selecting hello delete button.</span></span> 

![경로 필터 만들기](.\media\how-to-routefilter-portal\DeleteRouteFilter.png) 

## <a name="next-steps"></a><span data-ttu-id="08a3d-192">다음 단계</span><span class="sxs-lookup"><span data-stu-id="08a3d-192">Next steps</span></span>

<span data-ttu-id="08a3d-193">ExpressRoute에 대 한 자세한 내용은 참조 hello [express 경로 FAQ](expressroute-faqs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="08a3d-193">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
