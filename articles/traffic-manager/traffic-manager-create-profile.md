---
title: "Azure에서 Traffic Manager 프로필 만들기 | Microsoft Docs"
description: "이 문서는 Traffic Manager 프로필을 만드는 방법을 설명합니다."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: kumud
ms.openlocfilehash: 3792c9eca3d3a281cc12d241d46fbf5e5bc8e6b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="cdf3d-103">Traffic Manager 프로필 만들기</span><span class="sxs-lookup"><span data-stu-id="cdf3d-103">Create a Traffic Manager profile</span></span>

<span data-ttu-id="cdf3d-104">이 문서에서는 사용자를 두 Azure Web Apps 끝점으로 라우팅하도록 **우선 순위** 라우팅 형식을 사용하는 프로필을 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf3d-104">This article describes how a profile with **Priority** routing type can be created to route users to two Azure Web Apps endpoints.</span></span> <span data-ttu-id="cdf3d-105">**우선 순위** 라우팅 형식을 사용하면 두 번째 끝점은 백업으로 유지되는 동안 첫 번째 끝점으로 모든 트래픽이 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdf3d-105">By using the **Priority** routing type, all traffic is routed to the first endpoint while the second is kept as a backup.</span></span> <span data-ttu-id="cdf3d-106">결과적으로, 첫 번째 끝점이 비정상 상태가 되면 사용자는 두 번째 끝점으로 라우팅될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf3d-106">As a result, users can be routed to the second endpoint if the first endpoint becomes unhealthy.</span></span>

<span data-ttu-id="cdf3d-107">이 문서에서는 이전에 만든 두 개의 Azure Web Apps 끝점이 새로 만든 이 Traffic Manager 프로필에 연결되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf3d-107">In this article, two previously created Azure Web App endpoints are associated to this newly created Traffic Manager profile.</span></span> <span data-ttu-id="cdf3d-108">Azure Web Apps 끝점을 만드는 방법에 대한 자세한 정보는 [Azure Web Apps 설명서 페이지](https://docs.microsoft.com/azure/app-service-web/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cdf3d-108">To learn more about how to create Azure Web App endpoints, visit the [Azure Web Apps documentation page](https://docs.microsoft.com/azure/app-service-web/).</span></span> <span data-ttu-id="cdf3d-109">예를 들어 DNS 이름이 있고 공용 인터넷에 연결할 수 있으며 Azure Web Apps 끝점을 사용하는 경우 모든 끝점을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf3d-109">You can add any endpoint that has a DNS name and is reachable over the public internet and that we are using Azure Web Apps endpoints as an example.</span></span>

### <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="cdf3d-110">Traffic Manager 프로필 만들기</span><span class="sxs-lookup"><span data-stu-id="cdf3d-110">Create a Traffic Manager profile</span></span>
1. <span data-ttu-id="cdf3d-111">브라우저에서 [Azure Portal](http://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf3d-111">From a browser, sign in to the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="cdf3d-112">계정이 아직 없는 경우 [1개월 무료 평가판](https://azure.microsoft.com/free/)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf3d-112">If you don’t already have an account, you can sign-up for a [free one-month trial](https://azure.microsoft.com/free/).</span></span> 
2. <span data-ttu-id="cdf3d-113">**허브** 메뉴에서 **새로 만들기** > **네트워킹** > **모두 보기**를 클릭하고, **Traffic Manager** 프로필을 클릭하여 **Traffic Manager 프로필 만들기** 블레이드를 연 다음, **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf3d-113">On the **Hub** menu, click **New** > **Networking** > **See all**, click **Traffic Manager** profile to open the **Create Traffic Manager profile** blade, then click **Create**.</span></span>
3. <span data-ttu-id="cdf3d-114">**Traffic Manager 프로필 만들기** 블레이드에서 다음과 같이 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf3d-114">On the **Create Traffic Manager profile** blade, complete as follows:</span></span>
    1. <span data-ttu-id="cdf3d-115">**이름**에서 사용자의 프로필에 사용할 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf3d-115">In **Name**, provide a name for your profile.</span></span> <span data-ttu-id="cdf3d-116">이 이름은 trafficmanager.net 내에서 고유해야 하며 DNS 이름 <name>,trafficmanager.net 형식으로 나타나고, Traffic Manager 프로필에 액세스하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdf3d-116">This name needs to be unique within the trafficmanager.net zone and results in the DNS name <name>,trafficmanager.net which is used to access your Traffic Manager profile.</span></span>
    2. <span data-ttu-id="cdf3d-117">**라우팅 정책**에서 **우선 순위** 라우팅 방법을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf3d-117">In **Routing method**, select the **Priority** routing method.</span></span>
    3. <span data-ttu-id="cdf3d-118">**구독**에서 이 프로필을 만들 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf3d-118">In **Subscription**, select the subscription you want to create this profile under</span></span>
    4. <span data-ttu-id="cdf3d-119">**리소스 그룹**에서 이 프로필을 배치할 새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cdf3d-119">In **Resource Group**, create a new resource group to place this profile under.</span></span>
    5. <span data-ttu-id="cdf3d-120">**리소스 그룹 위치**에서 리소스 그룹의 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf3d-120">In **Resource group location**, select the location of the resource group.</span></span> <span data-ttu-id="cdf3d-121">이 설정은 리소스 그룹의 위치를 나타내며 전역적으로 배포되는 Traffic Manager 프로필에는 영향을 미치지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf3d-121">This setting refers to the location of the resource group, and has no impact on the Traffic Manager profile that will be deployed globally.</span></span>
    6. <span data-ttu-id="cdf3d-122">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf3d-122">Click **Create**.</span></span>
    7. <span data-ttu-id="cdf3d-123">Traffic Manager 프로필의 전역 배포가 완료되면 리소스 중 하나로 해당 리소스 그룹에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdf3d-123">When the global deployment of your Traffic Manager profile is complete, it is listed in respective resource group as one of the resources.</span></span>

    ![Traffic Manager 프로필 만들기](./media/traffic-manager-create-profile/Create-traffic-manager-profile.png)

## <a name="add-traffic-manager-endpoints"></a><span data-ttu-id="cdf3d-125">Traffic Manager 끝점 추가</span><span class="sxs-lookup"><span data-stu-id="cdf3d-125">Add Traffic Manager endpoints</span></span>

1. <span data-ttu-id="cdf3d-126">포털의 검색 창에서 이전 섹션에서 만들었던 **Traffic Manager 프로필** 이름을 검색하고 표시되는 결과에서 해당 Traffic Manager 프로필을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf3d-126">In the portal’s search bar, search for the **Traffic Manager profile** name that you created in the preceding section and click the traffic manager profile in the results that the displayed.</span></span>
2. <span data-ttu-id="cdf3d-127">**Traffic Manager 프로필** 블레이드에서 **설정** 섹션의 **끝점**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf3d-127">In the **Traffic Manager profile** blade, in the **Settings** section, click **Endpoints**.</span></span>
3. <span data-ttu-id="cdf3d-128">표시되는 **끝점** 블레이드에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf3d-128">In the **Endpoints** blade that is displayed, click **Add**.</span></span>
4. <span data-ttu-id="cdf3d-129">**끝점 추가** 블레이드에서 다음과 같이 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf3d-129">In the **Add endpoint** blade, complete as follows:</span></span>
    1. <span data-ttu-id="cdf3d-130">**형식**의 경우 **Azure 끝점**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf3d-130">For **Type**, click **Azure endpoint**.</span></span>
    2. <span data-ttu-id="cdf3d-131">이 끝점을 인식하는 기준으로 사용할 **이름**을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf3d-131">Provide a **Name** by which you want to recognize this endpoint.</span></span>
    3. <span data-ttu-id="cdf3d-132">**대상 리소스 형식**의 경우 **App Service**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf3d-132">For **Target resource type**, click **App Service**.</span></span>
    4. <span data-ttu-id="cdf3d-133">**대상 리소스**의 경우 **앱 서비스 선택**을 클릭하여 동일한 구독에서 웹앱의 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf3d-133">For **Target resource**, click **Choose an app service** to show the listing of the Web Apps under the same subscription.</span></span> <span data-ttu-id="cdf3d-134">표시되는 **리소스** 블레이드에서 첫 번째 끝점으로 추가할 App Service를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf3d-134">In the **Resource** blade that is displayed, pick the App service that you want to add as the first endpoint.</span></span>
    5. <span data-ttu-id="cdf3d-135">**우선 순위**의 경우 **1**로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf3d-135">For **Priority**, select as **1**.</span></span> <span data-ttu-id="cdf3d-136">이제 모든 트래픽이 정상일 경우 이 끝점으로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdf3d-136">This results in all traffic going to this endpoint if it is healthy.</span></span>
    6. <span data-ttu-id="cdf3d-137">**사용 안 함으로 추가**를 선택 취소 상태로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf3d-137">Keep **Add as disabled** unchecked.</span></span>
    7. <span data-ttu-id="cdf3d-138">**확인**</span><span class="sxs-lookup"><span data-stu-id="cdf3d-138">Click **OK**</span></span>
5.  <span data-ttu-id="cdf3d-139">다음 Azure Web Apps 끝점에 대해 3, 4단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf3d-139">Repeat steps 3 and 4 for the next Azure Web Apps endpoint.</span></span> <span data-ttu-id="cdf3d-140">**우선 순위** 값을 **2**로 설정한 상태에서 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf3d-140">Make sure to add it with its **Priority** value set at **2**.</span></span>
6.  <span data-ttu-id="cdf3d-141">두 끝점 추가가 완료되면 **온라인**인 모니터링 상태와 함께 **Traffic Manager 프로필** 블레이드에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdf3d-141">When the addition of both endpoints is complete, they are displayed in the **Traffic Manager profile** blade along with their monitoring status as **Online**.</span></span>

    ![Traffic Manager 끝점 추가](./media/traffic-manager-create-profile/add-traffic-manager-endpoint.png)

## <a name="use-the-traffic-manager-profile"></a><span data-ttu-id="cdf3d-143">Traffic Manager 프로필 사용</span><span class="sxs-lookup"><span data-stu-id="cdf3d-143">Use the Traffic Manager profile</span></span>
1.  <span data-ttu-id="cdf3d-144">포털의 검색 창에서 이전 섹션에서 만든 **Traffic Manager 프로필** 이름을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf3d-144">In the portal’s search bar, search for the **Traffic Manager profile** name that you created in the preceding section.</span></span> <span data-ttu-id="cdf3d-145">표시되는 결과에서 Traffic Manager 프로필을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf3d-145">In the results that are displayed, click the traffic manager profile.</span></span>
2. <span data-ttu-id="cdf3d-146">**Traffic Manager 프로필** 블레이드에서 **개요**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf3d-146">In the **Traffic Manager profile** blade, click **Overview**.</span></span>
3. <span data-ttu-id="cdf3d-147">**Traffic Manager 프로필** 블레이드에 사용자의 새로 만든 Traffic Manager 프로필의 DNS 이름이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdf3d-147">The **Traffic Manager profile** blade displays the DNS name of your newly created Traffic Manager profile.</span></span> <span data-ttu-id="cdf3d-148">이는 라우팅 형식에서 결정된 대로 올바른 끝점으로 라우팅되도록 모든 클라이언트가 사용할 수 있습니다(예를 들어 웹 브라우저를 사용하여 이동).</span><span class="sxs-lookup"><span data-stu-id="cdf3d-148">This can be used by any clients (for example, by navigating to it using a web browser) to get routed to the right endpoint as determined by the routing type.</span></span> <span data-ttu-id="cdf3d-149">이 경우 모든 요청이 첫 번째 끝점으로 라우팅되고 Traffic Manager에서 이를 비정상으로 감지하면 트래픽은 자동으로 다음 끝점으로 장애 조치됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdf3d-149">In this case, all requests are routed to the first endpoint and if Traffic Manager detects it be unhealthy, the traffic automatically fails over to the next endpoint.</span></span>

## <a name="delete-the-traffic-manager-profile"></a><span data-ttu-id="cdf3d-150">Traffic Manager 프로필 삭제</span><span class="sxs-lookup"><span data-stu-id="cdf3d-150">Delete the Traffic Manager profile</span></span>
<span data-ttu-id="cdf3d-151">더 이상 필요하지 않으면 사용자가 만든 리소스 그룹 및 Traffic Manager 프로필을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf3d-151">When no longer needed, delete the resource group and the Traffic Manager profile that you have created.</span></span> <span data-ttu-id="cdf3d-152">이렇게 하려면 **Traffic Manager 프로필** 블레이드에서 리소스 그룹을 선택하고 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf3d-152">To do so, select the resource group from the **Traffic Manager profile** blade and click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cdf3d-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cdf3d-153">Next steps</span></span>

- <span data-ttu-id="cdf3d-154">[라우팅 형식](traffic-manager-routing-methods.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="cdf3d-154">Learn more about [routing types](traffic-manager-routing-methods.md).</span></span>
- <span data-ttu-id="cdf3d-155">[끝점 형식](traffic-manager-endpoint-types.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="cdf3d-155">Learn more about endpoint types [endpoint types](traffic-manager-endpoint-types.md).</span></span>
- <span data-ttu-id="cdf3d-156">[끝점 모니터링](traffic-manager-monitoring.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="cdf3d-156">Learn more about [endpoint monitoring](traffic-manager-monitoring.md).</span></span>



