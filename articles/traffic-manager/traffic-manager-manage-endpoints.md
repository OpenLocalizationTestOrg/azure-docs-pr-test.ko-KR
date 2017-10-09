---
title: "Azure 트래픽 관리자의 aaaManage 끝점 | Microsoft Docs"
description: "이 문서는 Azure 트래픽 관리자에서 끝점을 추가, 제거 및 사용하거나 사용하지 않도록 설정하는 데 도움이 됩니다."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: ade2bbc2-35a7-43c5-8001-4698f7254526
ms.service: traffic-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/08/2017
ms.author: kumud
ms.openlocfilehash: fc65874ae2eaeb6fca5d8c4f33403c258307bdb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-disable-enable-or-delete-endpoints"></a><span data-ttu-id="90b60-103">끝점 추가, 사용 안 함, 사용 또는 삭제</span><span class="sxs-lookup"><span data-stu-id="90b60-103">Add, disable, enable, or delete endpoints</span></span>

<span data-ttu-id="90b60-104">장애 조치 및 라운드 로빈 트래픽 hello 웹 사이트 모드에 관계 없이 데이터 센터 내 웹 사이트에 대 한 라우팅 기능을 이미 제공 하는 hello Azure 앱 서비스 웹 앱 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-104">hello Web Apps feature in Azure App Service already provides failover and round-robin traffic routing functionality for websites within a datacenter, regardless of hello website mode.</span></span> <span data-ttu-id="90b60-105">Azure 트래픽 관리자 toospecify 장애 조치 및 다른 데이터 센터의 웹 사이트 및 클라우드 서비스에 대 한 라운드 로빈 트래픽을 라우팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-105">Azure Traffic Manager allows you toospecify failover and round-robin traffic routing for websites and cloud services in different datacenters.</span></span> <span data-ttu-id="90b60-106">hello 첫 번째 단계 필요한 tooprovide 기능 tooadd hello 클라우드 서비스나 웹 사이트 끝점 tooTraffic 관리자 인지 합니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-106">hello first step necessary tooprovide that functionality is tooadd hello cloud service or website endpoint tooTraffic Manager.</span></span>

<span data-ttu-id="90b60-107">트래픽 관리자 프로필의 일부인 개별 끝점을 사용하지 않도록 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-107">You can also disable individual endpoints that are part of a Traffic Manager profile.</span></span> <span data-ttu-id="90b60-108">끝점을 해제 하면 열은 그대로 hello 프로필의 일부로 남겨두면 hello 프로필 처럼 hello 끝점에 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-108">Disabling an endpoint leaves it as part of hello profile, but hello profile acts as if hello endpoint is not included in it.</span></span> <span data-ttu-id="90b60-109">이 작업은 유지 관리 모드에 있거나 다시 배포할 끝점을 일시적으로 제거하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-109">This action is useful for temporarily removing an endpoint that is in maintenance mode or being redeployed.</span></span> <span data-ttu-id="90b60-110">Hello 끝점은 다시 실행을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-110">Once hello endpoint is up and running again, it can be enabled.</span></span>

> [!NOTE]
> <span data-ttu-id="90b60-111">끝점을 해제 하면 영향을 주지 toodo Azure에서 배포 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-111">Disabling an endpoint has nothing toodo with its deployment state in Azure.</span></span> <span data-ttu-id="90b60-112">정상 끝점 수를 유지 됩니다. tooreceive 트래픽을 트래픽 관리자에서 사용 하지 않도록 설정 하는 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-112">A healthy endpoint remains up and able tooreceive traffic even when disabled in Traffic Manager.</span></span> <span data-ttu-id="90b60-113">또한 한 프로필에서 끝점을 사용하지 않도록 설정해도 다른 프로필의 해당 끝점 상태에는 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-113">Additionally, disabling an endpoint in one profile does not affect its status in another profile.</span></span>

## <a name="tooadd-a-cloud-service-or-an-app-service-endpoint-tooa-traffic-manager-profile"></a><span data-ttu-id="90b60-114">tooadd 클라우드 서비스 또는 응용 프로그램 서비스 끝점 tooa 트래픽 관리자 프로필</span><span class="sxs-lookup"><span data-stu-id="90b60-114">tooadd a cloud service or an App service endpoint tooa Traffic Manager profile</span></span>

1. <span data-ttu-id="90b60-115">Toohello 브라우저에서 로그인 [Azure 포털](http://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-115">From a browser, sign in toohello [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="90b60-116">Hello hello 포털 검색 창에서 검색할 **트래픽 관리자 프로필** 이름을 toomodify를 원하고 hello에 hello 트래픽 관리자 프로필을 클릭 한 다음 결과 표시 하는 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-116">In hello portal’s search bar, search for hello **Traffic Manager profile** name that you want toomodify, and then click hello Traffic Manager profile in hello results that hello displayed.</span></span>
3. <span data-ttu-id="90b60-117">Hello에 **트래픽 관리자 프로필** 블레이드 hello **설정** 섹션에서 클릭 **끝점**합니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-117">In hello **Traffic Manager profile** blade, in hello **Settings** section, click **Endpoints**.</span></span>
4. <span data-ttu-id="90b60-118">Hello에 **끝점** 블레이드에 표시 되는 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-118">In hello **Endpoints** blade that is displayed, click **Add**.</span></span>
5. <span data-ttu-id="90b60-119">Hello에 **끝점 추가** 블레이드를 다음과 같이 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-119">In hello **Add endpoint** blade, complete as follows:</span></span>
    1. <span data-ttu-id="90b60-120">**형식**의 경우 **Azure 끝점**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-120">For **Type**, click **Azure endpoint**.</span></span>
    2. <span data-ttu-id="90b60-121">제공 된 **이름** 기준이 될 toorecognize이이 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-121">Provide a **Name** by which you want toorecognize this endpoint.</span></span>
    3. <span data-ttu-id="90b60-122">에 대 한 **대상 리소스 종류**에서 드롭 다운 hello, hello 적절 한 리소스 종류를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-122">For **Target resource type**, from hello drop-down, choose hello appropriate resource type.</span></span>
    4. <span data-ttu-id="90b60-123">에 대 한 **대상 리소스**드롭 다운 hello에서 hello 적절 한 대상 리소스를 선택, tooshow hello 목록 아래에 있는 리소스 hello hello에 동일한 구독 **리소스 블레이드**합니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-123">For **Target resource**, from hello drop-down, choose hello appropriate target resource tooshow hello listing resources under hello same subscription in hello **Resources blade**.</span></span> <span data-ttu-id="90b60-124">Hello에 **리소스** 블레이드를 표시 되 면 hello 첫 번째 끝점으로 tooadd 않겠다고 선택 hello 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-124">In hello **Resource** blade that is displayed, pick hello service that you want tooadd as hello first endpoint.</span></span>
    5. <span data-ttu-id="90b60-125">**우선 순위**의 경우 **1**로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-125">For **Priority**, select as **1**.</span></span> <span data-ttu-id="90b60-126">따라서 정상 상태 이면 toothis 끝점이 모든 트래픽이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-126">This results in all traffic going toothis endpoint if it is healthy.</span></span>
    6. <span data-ttu-id="90b60-127">**사용 안 함으로 추가**를 선택 취소 상태로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-127">Keep **Add as disabled** unchecked.</span></span>
    7. <span data-ttu-id="90b60-128">**확인**</span><span class="sxs-lookup"><span data-stu-id="90b60-128">Click **OK**</span></span>
6.  <span data-ttu-id="90b60-129">4 단계와 5 tooadd hello 다음 Azure 끝점을 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-129">Repeat steps 4 and 5 tooadd hello next Azure endpoint.</span></span> <span data-ttu-id="90b60-130">있는지 tooadd 확인 사용 하 여 해당 **우선 순위** 값 설정에서 **2**합니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-130">Make sure tooadd it with its **Priority** value set at **2**.</span></span>
7.  <span data-ttu-id="90b60-131">Hello에 표시 된 두 끝점 모두의 hello 추가 완료 되 면 **트래픽 관리자 프로필** 블레이드로 모니터링 상태와 함께 **온라인**합니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-131">When hello addition of both endpoints is complete, they are displayed in hello **Traffic Manager profile** blade along with their monitoring status as **Online**.</span></span>

> [!NOTE]
> <span data-ttu-id="90b60-132">Hello를 사용 하 여 프로필에서 끝점을 제거 하거나 추가 하면 *장애 조치* 트래픽 라우팅 방법, hello 장애 조치 우선 순위 목록 수 정렬 되지 않습니다 수 있습니다 원하는대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-132">After you add or remove an endpoint from a profile using hello *Failover* traffic routing method, hello failover priority list may not be ordered they way you want.</span></span> <span data-ttu-id="90b60-133">Hello 구성 페이지에서 장애 조치 우선 순위 목록 hello hello 순서를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-133">You can adjust hello order of hello Failover Priority List on hello Configuration page.</span></span> <span data-ttu-id="90b60-134">자세한 내용은 [장애 조치(Failover) 트래픽 라우팅 구성](traffic-manager-configure-failover-routing-method.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="90b60-134">For more information, see [Configure Failover traffic routing](traffic-manager-configure-failover-routing-method.md).</span></span>

## <a name="toodisable-an-endpoint"></a><span data-ttu-id="90b60-135">toodisable 끝점</span><span class="sxs-lookup"><span data-stu-id="90b60-135">toodisable an endpoint</span></span>

1. <span data-ttu-id="90b60-136">Toohello 브라우저에서 로그인 [Azure 포털](http://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-136">From a browser, sign in toohello [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="90b60-137">Hello hello 포털 검색 창에서 검색할 **트래픽 관리자 프로필** 이름 toomodify를 원하고 표시 되는 hello 결과의 hello 트래픽 관리자 프로필을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-137">In hello portal’s search bar, search for hello  **Traffic Manager profile** name that you want toomodify, and then click hello Traffic Manager profile in hello results that are displayed.</span></span>
3. <span data-ttu-id="90b60-138">Hello에 **트래픽 관리자 프로필** 블레이드 hello **설정** 섹션에서 클릭 **끝점**합니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-138">In hello **Traffic Manager profile** blade, in hello **Settings** section, click **Endpoints**.</span></span> 
4. <span data-ttu-id="90b60-139">Toodisable, hello 끝점을 클릭 한 다음 hello **끝점** 블레이드에 표시 되는 클릭 **편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-139">Click hello endpoint that you want toodisable, and then on hello **Endpoint** blade that is displayed, click **Edit**.</span></span>
5. <span data-ttu-id="90b60-140">Hello에 **끝점** 블레이드에서 hello 끝점 상태 변경**비활성화**, 클릭 하 고 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-140">In hello **Endpoint** blade, change hello endpoint status too**Disabled**, and then click **Save**.</span></span>
6. <span data-ttu-id="90b60-141">클라이언트는 hello 지속 될 시간 to Live (TTL) toosend 트래픽 toohello 끝점을 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-141">Clients continue toosend traffic toohello endpoint for hello duration of Time-to-Live (TTL).</span></span> <span data-ttu-id="90b60-142">Hello TTL hello 트래픽 관리자 프로필의 hello 구성 페이지에서 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-142">You can change hello TTL on hello Configuration page of hello Traffic Manager profile.</span></span>

## <a name="tooenable-an-endpoint"></a><span data-ttu-id="90b60-143">tooenable 끝점</span><span class="sxs-lookup"><span data-stu-id="90b60-143">tooenable an endpoint</span></span>

1. <span data-ttu-id="90b60-144">Toohello 브라우저에서 로그인 [Azure 포털](http://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-144">From a browser, sign in toohello [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="90b60-145">Hello hello 포털 검색 창에서 검색할 **트래픽 관리자 프로필** 이름 toomodify를 원하고 표시 되는 hello 결과의 hello 트래픽 관리자 프로필을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-145">In hello portal’s search bar, search for hello  **Traffic Manager profile** name that you want toomodify, and then click hello Traffic Manager profile in hello results that are displayed.</span></span>
3. <span data-ttu-id="90b60-146">Hello에 **트래픽 관리자 프로필** 블레이드 hello **설정** 섹션에서 클릭 **끝점**합니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-146">In hello **Traffic Manager profile** blade, in hello **Settings** section, click **Endpoints**.</span></span> 
4. <span data-ttu-id="90b60-147">Toodisable, hello 끝점을 클릭 한 다음 hello **끝점** 블레이드에 표시 되는 클릭 **편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-147">Click hello endpoint that you want toodisable, and then on hello **Endpoint** blade that is displayed, click **Edit**.</span></span>
5. <span data-ttu-id="90b60-148">Hello에 **끝점** 블레이드에서 hello 끝점 상태 변경**Enabled**, 클릭 하 고 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-148">In hello **Endpoint** blade, change hello endpoint status too**Enabled**, and then click **Save**.</span></span>
6. <span data-ttu-id="90b60-149">클라이언트는 hello 지속 될 시간 to Live (TTL) toosend 트래픽 toohello 끝점을 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-149">Clients continue toosend traffic toohello endpoint for hello duration of Time-to-Live (TTL).</span></span> <span data-ttu-id="90b60-150">Hello TTL hello 트래픽 관리자 프로필의 hello 구성 페이지에서 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-150">You can change hello TTL on hello Configuration page of hello Traffic Manager profile.</span></span>

## <a name="toodelete-an-endpoint"></a><span data-ttu-id="90b60-151">toodelete 끝점</span><span class="sxs-lookup"><span data-stu-id="90b60-151">toodelete an endpoint</span></span>

1. <span data-ttu-id="90b60-152">Toohello 브라우저에서 로그인 [Azure 포털](http://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-152">From a browser, sign in toohello [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="90b60-153">Hello hello 포털 검색 창에서 검색할 **트래픽 관리자 프로필** 이름 toomodify를 원하고 표시 되는 hello 결과의 hello 트래픽 관리자 프로필을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-153">In hello portal’s search bar, search for hello  **Traffic Manager profile** name that you want toomodify, and then click hello Traffic Manager profile in hello results that are displayed.</span></span>
3. <span data-ttu-id="90b60-154">Hello에 **트래픽 관리자 프로필** 블레이드 hello **설정** 섹션에서 클릭 **끝점**합니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-154">In hello **Traffic Manager profile** blade, in hello **Settings** section, click **Endpoints**.</span></span> 
4. <span data-ttu-id="90b60-155">Toodisable, hello 끝점을 클릭 한 다음 hello **끝점** 블레이드에 표시 되는 클릭 **편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-155">Click hello endpoint that you want toodisable, and then on hello **Endpoint** blade that is displayed, click **Edit**.</span></span>
5. <span data-ttu-id="90b60-156">Hello에 **끝점** 블레이드에서 hello 끝점 상태 변경**Enabled**, 클릭 하 고 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="90b60-156">In hello **Endpoint** blade, change hello endpoint status too**Enabled**, and then click **Save**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="90b60-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="90b60-157">Next steps</span></span>

* [<span data-ttu-id="90b60-158">Traffic Manager 프로필 관리</span><span class="sxs-lookup"><span data-stu-id="90b60-158">Manage Traffic Manager profiles</span></span>](traffic-manager-manage-profiles.md)
* [<span data-ttu-id="90b60-159">라우팅 방법 구성</span><span class="sxs-lookup"><span data-stu-id="90b60-159">Configure routing methods</span></span>](traffic-manager-configure-routing-method.md)
* [<span data-ttu-id="90b60-160">트래픽 관리자 성능 저하 상태 문제 해결</span><span class="sxs-lookup"><span data-stu-id="90b60-160">Troubleshooting Traffic Manager degraded state</span></span>](traffic-manager-troubleshooting-degraded.md)
* [<span data-ttu-id="90b60-161">트래픽 관리자 성능 고려 사항</span><span class="sxs-lookup"><span data-stu-id="90b60-161">Traffic Manager performance considerations</span></span>](traffic-manager-performance-considerations.md)
* [<span data-ttu-id="90b60-162">트래픽 관리자 작업(REST API 참조)</span><span class="sxs-lookup"><span data-stu-id="90b60-162">Operations on Traffic Manager (REST API Reference)</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=313584)

