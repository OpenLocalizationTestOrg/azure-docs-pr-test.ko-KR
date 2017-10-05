---
title: "Azure 트래픽 관리자에서 끝점 관리 | Microsoft Docs"
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
ms.openlocfilehash: 765d12bc283d991783fb3190ce7917b573f9fc78
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="add-disable-enable-or-delete-endpoints"></a><span data-ttu-id="3de44-103">끝점 추가, 사용 안 함, 사용 또는 삭제</span><span class="sxs-lookup"><span data-stu-id="3de44-103">Add, disable, enable, or delete endpoints</span></span>

<span data-ttu-id="3de44-104">Azure 앱 서비스의 웹앱은 웹 사이트 모드에 관계없이 데이터 센터 내의 웹 사이트에 대해 이미 장애 조치(Failover) 및 라운드 로빈 트래픽 라우팅 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-104">The Web Apps feature in Azure App Service already provides failover and round-robin traffic routing functionality for websites within a datacenter, regardless of the website mode.</span></span> <span data-ttu-id="3de44-105">Azure 트래픽 관리자를 통해 다른 데이터 센터의 웹 사이트와 클라우드 서비스에 대해 장애 조치(Failover) 및 라운드 로빈 트래픽 라우팅을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-105">Azure Traffic Manager allows you to specify failover and round-robin traffic routing for websites and cloud services in different datacenters.</span></span> <span data-ttu-id="3de44-106">해당 기능을 제공하는 데 필요한 첫 번째 단계는 트래픽 관리자에 클라우드 서비스 또는 웹 사이트 끝점을 추가하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-106">The first step necessary to provide that functionality is to add the cloud service or website endpoint to Traffic Manager.</span></span>

<span data-ttu-id="3de44-107">트래픽 관리자 프로필의 일부인 개별 끝점을 사용하지 않도록 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-107">You can also disable individual endpoints that are part of a Traffic Manager profile.</span></span> <span data-ttu-id="3de44-108">끝점을 사용하지 않도록 설정하는 경우 프로필의 일부로 유지되지만 끝점이 없는 것처럼 프로필이 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-108">Disabling an endpoint leaves it as part of the profile, but the profile acts as if the endpoint is not included in it.</span></span> <span data-ttu-id="3de44-109">이 작업은 유지 관리 모드에 있거나 다시 배포할 끝점을 일시적으로 제거하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-109">This action is useful for temporarily removing an endpoint that is in maintenance mode or being redeployed.</span></span> <span data-ttu-id="3de44-110">끝점이 다시 작동하여 실행되면 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-110">Once the endpoint is up and running again, it can be enabled.</span></span>

> [!NOTE]
> <span data-ttu-id="3de44-111">끝점을 사용하지 않도록 설정하는 경우 Azure의 끝점 배포 상태에는 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-111">Disabling an endpoint has nothing to do with its deployment state in Azure.</span></span> <span data-ttu-id="3de44-112">정상 끝점은 실행 상태로 유지되며 Traffic Manager에서 사용하지 않도록 설정된 경우에도 트래픽을 수신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-112">A healthy endpoint remains up and able to receive traffic even when disabled in Traffic Manager.</span></span> <span data-ttu-id="3de44-113">또한 한 프로필에서 끝점을 사용하지 않도록 설정해도 다른 프로필의 해당 끝점 상태에는 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-113">Additionally, disabling an endpoint in one profile does not affect its status in another profile.</span></span>

## <a name="to-add-a-cloud-service-or-an-app-service-endpoint-to-a-traffic-manager-profile"></a><span data-ttu-id="3de44-114">Traffic Manager 프로필에 클라우드 서비스 또는 App Service 끝점을 추가하려면</span><span class="sxs-lookup"><span data-stu-id="3de44-114">To add a cloud service or an App service endpoint to a Traffic Manager profile</span></span>

1. <span data-ttu-id="3de44-115">브라우저에서 [Azure Portal](http://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-115">From a browser, sign in to the [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="3de44-116">포털의 검색 창에서 수정하려는 **Traffic Manager 프로필** 이름을 검색한 다음 표시되는 결과에서 Traffic Manager 프로필을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-116">In the portal’s search bar, search for the **Traffic Manager profile** name that you want to modify, and then click the Traffic Manager profile in the results that the displayed.</span></span>
3. <span data-ttu-id="3de44-117">**Traffic Manager 프로필** 블레이드에서 **설정** 섹션의 **끝점**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-117">In the **Traffic Manager profile** blade, in the **Settings** section, click **Endpoints**.</span></span>
4. <span data-ttu-id="3de44-118">표시되는 **끝점** 블레이드에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-118">In the **Endpoints** blade that is displayed, click **Add**.</span></span>
5. <span data-ttu-id="3de44-119">**끝점 추가** 블레이드에서 다음과 같이 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-119">In the **Add endpoint** blade, complete as follows:</span></span>
    1. <span data-ttu-id="3de44-120">**형식**의 경우 **Azure 끝점**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-120">For **Type**, click **Azure endpoint**.</span></span>
    2. <span data-ttu-id="3de44-121">이 끝점을 인식하는 기준으로 사용할 **이름**을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-121">Provide a **Name** by which you want to recognize this endpoint.</span></span>
    3. <span data-ttu-id="3de44-122">**대상 리소스 형식**의 경우 드롭다운 목록에서 적절한 리소스 형식을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-122">For **Target resource type**, from the drop-down, choose the appropriate resource type.</span></span>
    4. <span data-ttu-id="3de44-123">**대상 리소스**의 경우 드롭다운 목록에서 적절한 대상 리소스를 선택하여 **리소스 블레이드**의 동일한 구독 아래에서 나열된 리소스를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-123">For **Target resource**, from the drop-down, choose the appropriate target resource to show the listing resources under the same subscription in the **Resources blade**.</span></span> <span data-ttu-id="3de44-124">표시되는 **리소스** 블레이드에서 첫 번째 끝점으로 추가할 서비스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-124">In the **Resource** blade that is displayed, pick the service that you want to add as the first endpoint.</span></span>
    5. <span data-ttu-id="3de44-125">**우선 순위**의 경우 **1**로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-125">For **Priority**, select as **1**.</span></span> <span data-ttu-id="3de44-126">이제 모든 트래픽이 정상일 경우 이 끝점으로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-126">This results in all traffic going to this endpoint if it is healthy.</span></span>
    6. <span data-ttu-id="3de44-127">**사용 안 함으로 추가**를 선택 취소 상태로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-127">Keep **Add as disabled** unchecked.</span></span>
    7. <span data-ttu-id="3de44-128">**확인**</span><span class="sxs-lookup"><span data-stu-id="3de44-128">Click **OK**</span></span>
6.  <span data-ttu-id="3de44-129">다음 Azure 끝점을 추가하려면 4, 5 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-129">Repeat steps 4 and 5 to add the next Azure endpoint.</span></span> <span data-ttu-id="3de44-130">**우선 순위** 값을 **2**로 설정한 상태에서 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-130">Make sure to add it with its **Priority** value set at **2**.</span></span>
7.  <span data-ttu-id="3de44-131">두 끝점 추가가 완료되면 **온라인**인 모니터링 상태와 함께 **Traffic Manager 프로필** 블레이드에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-131">When the addition of both endpoints is complete, they are displayed in the **Traffic Manager profile** blade along with their monitoring status as **Online**.</span></span>

> [!NOTE]
> <span data-ttu-id="3de44-132">*장애 조치* 트래픽 라우팅 방법을 사용하여 프로필에서 끝점을 추가하거나 제거한 후에는 장애 조치 우선 순위 목록을 원하는 방식으로 정렬할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-132">After you add or remove an endpoint from a profile using the *Failover* traffic routing method, the failover priority list may not be ordered they way you want.</span></span> <span data-ttu-id="3de44-133">대신 구성 페이지에서 장애 조치 우선 순위 목록의 순서를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-133">You can adjust the order of the Failover Priority List on the Configuration page.</span></span> <span data-ttu-id="3de44-134">자세한 내용은 [장애 조치(Failover) 트래픽 라우팅 구성](traffic-manager-configure-failover-routing-method.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3de44-134">For more information, see [Configure Failover traffic routing](traffic-manager-configure-failover-routing-method.md).</span></span>

## <a name="to-disable-an-endpoint"></a><span data-ttu-id="3de44-135">끝점을 사용하지 않도록 설정하려면</span><span class="sxs-lookup"><span data-stu-id="3de44-135">To disable an endpoint</span></span>

1. <span data-ttu-id="3de44-136">브라우저에서 [Azure Portal](http://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-136">From a browser, sign in to the [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="3de44-137">포털의 검색 창에서 수정하려는 **Traffic Manager 프로필** 이름을 검색한 다음 표시되는 결과에서 Traffic Manager 프로필을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-137">In the portal’s search bar, search for the  **Traffic Manager profile** name that you want to modify, and then click the Traffic Manager profile in the results that are displayed.</span></span>
3. <span data-ttu-id="3de44-138">**Traffic Manager 프로필** 블레이드에서 **설정** 섹션의 **끝점**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-138">In the **Traffic Manager profile** blade, in the **Settings** section, click **Endpoints**.</span></span> 
4. <span data-ttu-id="3de44-139">사용하지 않으려는 끝점을 클릭한 다음 표시되는 **끝점** 블레이드에서 **편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-139">Click the endpoint that you want to disable, and then on the **Endpoint** blade that is displayed, click **Edit**.</span></span>
5. <span data-ttu-id="3de44-140">**끝점** 블레이드에서 끝점 상태를 **비활성화**로 변경하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-140">In the **Endpoint** blade, change the endpoint status to **Disabled**, and then click **Save**.</span></span>
6. <span data-ttu-id="3de44-141">클라이언트에서 트래픽을 TTL(활성 시간) 기간의 끝점으로 계속 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-141">Clients continue to send traffic to the endpoint for the duration of Time-to-Live (TTL).</span></span> <span data-ttu-id="3de44-142">Traffic Manager 프로필의 구성 페이지에서 TTL을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-142">You can change the TTL on the Configuration page of the Traffic Manager profile.</span></span>

## <a name="to-enable-an-endpoint"></a><span data-ttu-id="3de44-143">끝점을 사용하도록 설정하려면</span><span class="sxs-lookup"><span data-stu-id="3de44-143">To enable an endpoint</span></span>

1. <span data-ttu-id="3de44-144">브라우저에서 [Azure Portal](http://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-144">From a browser, sign in to the [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="3de44-145">포털의 검색 창에서 수정하려는 **Traffic Manager 프로필** 이름을 검색한 다음 표시되는 결과에서 Traffic Manager 프로필을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-145">In the portal’s search bar, search for the  **Traffic Manager profile** name that you want to modify, and then click the Traffic Manager profile in the results that are displayed.</span></span>
3. <span data-ttu-id="3de44-146">**Traffic Manager 프로필** 블레이드에서 **설정** 섹션의 **끝점**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-146">In the **Traffic Manager profile** blade, in the **Settings** section, click **Endpoints**.</span></span> 
4. <span data-ttu-id="3de44-147">사용하지 않으려는 끝점을 클릭한 다음 표시되는 **끝점** 블레이드에서 **편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-147">Click the endpoint that you want to disable, and then on the **Endpoint** blade that is displayed, click **Edit**.</span></span>
5. <span data-ttu-id="3de44-148">**끝점** 블레이드에서 끝점 상태를 **활성화**로 변경하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-148">In the **Endpoint** blade, change the endpoint status to **Enabled**, and then click **Save**.</span></span>
6. <span data-ttu-id="3de44-149">클라이언트에서 트래픽을 TTL(활성 시간) 기간의 끝점으로 계속 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-149">Clients continue to send traffic to the endpoint for the duration of Time-to-Live (TTL).</span></span> <span data-ttu-id="3de44-150">Traffic Manager 프로필의 구성 페이지에서 TTL을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-150">You can change the TTL on the Configuration page of the Traffic Manager profile.</span></span>

## <a name="to-delete-an-endpoint"></a><span data-ttu-id="3de44-151">끝점을 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="3de44-151">To delete an endpoint</span></span>

1. <span data-ttu-id="3de44-152">브라우저에서 [Azure Portal](http://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-152">From a browser, sign in to the [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="3de44-153">포털의 검색 창에서 수정하려는 **Traffic Manager 프로필** 이름을 검색한 다음 표시되는 결과에서 Traffic Manager 프로필을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-153">In the portal’s search bar, search for the  **Traffic Manager profile** name that you want to modify, and then click the Traffic Manager profile in the results that are displayed.</span></span>
3. <span data-ttu-id="3de44-154">**Traffic Manager 프로필** 블레이드에서 **설정** 섹션의 **끝점**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-154">In the **Traffic Manager profile** blade, in the **Settings** section, click **Endpoints**.</span></span> 
4. <span data-ttu-id="3de44-155">사용하지 않으려는 끝점을 클릭한 다음 표시되는 **끝점** 블레이드에서 **편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-155">Click the endpoint that you want to disable, and then on the **Endpoint** blade that is displayed, click **Edit**.</span></span>
5. <span data-ttu-id="3de44-156">**끝점** 블레이드에서 끝점 상태를 **활성화**로 변경하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3de44-156">In the **Endpoint** blade, change the endpoint status to **Enabled**, and then click **Save**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="3de44-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3de44-157">Next steps</span></span>

* [<span data-ttu-id="3de44-158">Traffic Manager 프로필 관리</span><span class="sxs-lookup"><span data-stu-id="3de44-158">Manage Traffic Manager profiles</span></span>](traffic-manager-manage-profiles.md)
* [<span data-ttu-id="3de44-159">라우팅 방법 구성</span><span class="sxs-lookup"><span data-stu-id="3de44-159">Configure routing methods</span></span>](traffic-manager-configure-routing-method.md)
* [<span data-ttu-id="3de44-160">트래픽 관리자 성능 저하 상태 문제 해결</span><span class="sxs-lookup"><span data-stu-id="3de44-160">Troubleshooting Traffic Manager degraded state</span></span>](traffic-manager-troubleshooting-degraded.md)
* [<span data-ttu-id="3de44-161">트래픽 관리자 성능 고려 사항</span><span class="sxs-lookup"><span data-stu-id="3de44-161">Traffic Manager performance considerations</span></span>](traffic-manager-performance-considerations.md)
* [<span data-ttu-id="3de44-162">트래픽 관리자 작업(REST API 참조)</span><span class="sxs-lookup"><span data-stu-id="3de44-162">Operations on Traffic Manager (REST API Reference)</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=313584)

