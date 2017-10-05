---
title: "Azure Traffic Manager를 사용한 지리적 트래픽 라우팅 방법 구성 | Microsoft Docs"
description: "이 문서에서는 Azure Traffic Manager를 사용하여 지리적 트래픽 라우팅 방법을 구성하는 방법을 설명합니다."
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
ms.date: 03/22/2017
ms.author: kumud
ms.openlocfilehash: 13190189074b24b2d28cd3ce46cf8571f3e1e1d1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="configure-the-geographic-traffic-routing-method-using-traffic-manager"></a><span data-ttu-id="2707d-103">Traffic Manager를 사용한 지리적 트래픽 라우팅 방법 구성</span><span class="sxs-lookup"><span data-stu-id="2707d-103">Configure the geographic traffic routing method using Traffic Manager</span></span>

<span data-ttu-id="2707d-104">지리적 트래픽 라우팅 방법을 사용하면 요청이 발생하는 지리적 위치를 기반으로 특정 끝점에 트래픽을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2707d-104">The Geographic traffic routing method allows you to direct traffic to specific endpoints based on the geographic location where the requests originate.</span></span> <span data-ttu-id="2707d-105">이 자습서는 이 라우팅 방법을 사용하여 Traffic Manager 프로필을 만들고, 특정 지역에서 트래픽을 받도록 끝점을 구성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2707d-105">This tutorial shows you how to create a Traffic Manager profile with this routing method and configure the endpoints to receive traffic from specific geographies.</span></span>

## <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="2707d-106">Traffic Manager 프로필 만들기</span><span class="sxs-lookup"><span data-stu-id="2707d-106">Create a Traffic Manager Profile</span></span>

1. <span data-ttu-id="2707d-107">브라우저에서 [Azure Portal](http://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="2707d-107">From a browser, sign in to the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="2707d-108">아직 계정이 없는 경우 [1개월 무료 평가판](https://azure.microsoft.com/free/)을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2707d-108">If you don’t already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free/).</span></span>
2. <span data-ttu-id="2707d-109">허브 메뉴에서 **새로 만들기** > **네트워킹** > **모두 보기**를 클릭한 다음, **Traffic Manager 프로필**을 클릭하여 **Traffic Manager 프로필 만들기** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2707d-109">On the Hub menu, click **New** > **Networking** > **See all**, and then click **Traffic Manager profile** to open the **Create Traffic Manager profile** blade.</span></span>
3. <span data-ttu-id="2707d-110">**Traffic Manager 프로필 만들기** 블레이드에서</span><span class="sxs-lookup"><span data-stu-id="2707d-110">On the **Create Traffic Manager profile** blade:</span></span>
    1. <span data-ttu-id="2707d-111">사용자의 프로필에 사용할 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2707d-111">Provide a name for your profile.</span></span> <span data-ttu-id="2707d-112">이 이름은 trafficmanager.net 내에서 고유해야 하며 사용자의 Traffic Manager 프로필에 액세스하는 데 사용되는 DNS 이름 <profilename>,trafficmanager.net으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2707d-112">This name needs to be unique within the trafficmanager.net zone and will result in the DNS name <profilename>,trafficmanager.net which will be used to access your Traffic Manager profile.</span></span>
    2. <span data-ttu-id="2707d-113">**지리적** 라우팅 방법을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2707d-113">Select the **Geographic** routing method.</span></span>
    3. <span data-ttu-id="2707d-114">이 프로필에서 만들려는 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2707d-114">Select the subscription you want to create this profile under.</span></span>
    4. <span data-ttu-id="2707d-115">기존 리소스 그룹을 사용하거나 이 프로필에서 대체할 새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2707d-115">Use an existing resource group or create a new resource group to place this profile under.</span></span> <span data-ttu-id="2707d-116">새 리소스 그룹을 만드는 경우 **리소스 그룹 위치** 드롭다운을 사용하여 리소스 그룹의 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2707d-116">If you choose to create a new resource group, use the **Resource Group location** dropdown to specify the location of the resource group.</span></span> <span data-ttu-id="2707d-117">이 설정은 리소스 그룹의 위치를 나타내며 전역적으로 배포되는 Traffic Manager 프로필에는 영향을 미치지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2707d-117">This setting refers to the location of the resource group, and has no impact on the Traffic Manager profile which will be deployed globally.</span></span>
    5. <span data-ttu-id="2707d-118">**만들기**를 클릭하면 사용자의 Traffic Manager 프로필이 생성되고 전역적으로 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="2707d-118">After you click **Create**, your Traffic Manager profile is created and deployed globally.</span></span>

![Traffic Manager 프로필 만들기](./media/traffic-manager-geographic-routing-method/create-traffic-manager-profile.png)

## <a name="add-endpoints"></a><span data-ttu-id="2707d-120">끝점 추가</span><span class="sxs-lookup"><span data-stu-id="2707d-120">Add endpoints</span></span>

1. <span data-ttu-id="2707d-121">포털의 검색 창에서 방금 만든 Traffic Manager 프로필 이름을 검색하고 표시되면 결과를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2707d-121">Search for the Traffic Manager profile name you just created in the portal’s search bar and click on the result when it is shown.</span></span>
2. <span data-ttu-id="2707d-122">Traffic Manager 블레이드에서 **설정** -> **끝점**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2707d-122">Navigate to **Settings** -> **Endpoints** in the Traffic Manager blade.</span></span>
3. <span data-ttu-id="2707d-123">**추가**를 클릭하여 **끝점 추가** 블레이드를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="2707d-123">Click **Add** to show the **Add Endpoint** blade.</span></span>
3. <span data-ttu-id="2707d-124">**끝점** 블레이드에서 **추가**를 클릭하고 표시되는 **끝점 추가** 블레이드에서 다음과 같이 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="2707d-124">In the **Endpoints** blade, click **Add** and in the **Add endpoint** blade that is displayed, complete as follows:</span></span>
4. <span data-ttu-id="2707d-125">추가하려는 끝점의 형식에 따라 **형식**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2707d-125">Select **Type** depending upon the type of endpoint you are adding.</span></span> <span data-ttu-id="2707d-126">프로덕션에 사용되는 지리적 라우팅 프로필의 경우 둘 이상의 끝점이 있는 자식 프로필을 포함하는 중첩 끝점 형식을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2707d-126">For geographic routing profiles used in production, we strongly recommend using nested endpoint types containing a child profile with more than one endpoint.</span></span> <span data-ttu-id="2707d-127">자세한 내용은 [지리적 트래픽 라우팅 방법에 대한 FAQ](traffic-manager-FAQs.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2707d-127">For more details, see [FAQs about geographic traffic routing methods](traffic-manager-FAQs.md).</span></span>
5. <span data-ttu-id="2707d-128">이 끝점을 인식하는 기준으로 사용할 **이름**을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2707d-128">Provide a **Name** by which you want to recognize this endpoint.</span></span>
6. <span data-ttu-id="2707d-129">이 블레이드에서 특정 필드는 사용자가 추가하는 끝점의 형식에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="2707d-129">Certain fields in this blade depend on the type of endpoint you are adding:</span></span>
    1. <span data-ttu-id="2707d-130">Azure 끝점을 추가하는 경우 트래픽을 보낼 리소스에 따라 **대상 리소스 형식** 및 **대상**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2707d-130">If you are adding an Azure endpoint, select the **Target resource type** and the **Target** based on the resource you want to direct traffic to</span></span>
    2. <span data-ttu-id="2707d-131">**외부** 끝점을 추가하는 경우 사용자의 끝점에 사용할 **FQDN(정규화된 도메인 이름)**을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2707d-131">If you are adding an **External** endpoint, provide the **Fully-qualified domain name (FQDN)** for your endpoint.</span></span>
    3. <span data-ttu-id="2707d-132">**중첩 끝점**을 추가하는 경우 사용할 자식 프로필에 해당하는 **대상 리소스**를 선택하고 **최소 자식 끝점 수**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2707d-132">If you are adding a **Nested endpoint**, select the **Target resource** that corresponds to the child profile you want to use and specify the **Minimum child endpoints count**.</span></span>
7. <span data-ttu-id="2707d-133">지역 매핑 섹션에서 드롭다운을 사용하여 이 끝점으로 전송할 트래픽이 발생되는 지역을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2707d-133">In the Geo-mapping section, use the drop down to add the regions from where you want traffic to be sent to this endpoint.</span></span> <span data-ttu-id="2707d-134">하나 이상의 영역을 추가해야 하며 여러 지역을 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2707d-134">You must add at least one region, and you can have multiple regions mapped.</span></span>
8. <span data-ttu-id="2707d-135">이 프로필에서 추가하려는 모든 끝점에 대해 이 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="2707d-135">Repeat this for all endpoints you want to add under this profile</span></span>

![Traffic Manager 끝점 추가](./media/traffic-manager-geographic-routing-method/add-traffic-manager-endpoint.png)

## <a name="use-the-traffic-manager-profile"></a><span data-ttu-id="2707d-137">Traffic Manager 프로필 사용</span><span class="sxs-lookup"><span data-stu-id="2707d-137">Use the Traffic Manager profile</span></span>
1.  <span data-ttu-id="2707d-138">포털의 검색 창에서 이전 섹션에서 만들었던 **Traffic Manager 프로필** 이름을 검색하고 표시되는 결과에서 해당 Traffic Manager 프로필을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2707d-138">In the portal’s search bar, search for the **Traffic Manager profile** name that you created in the preceding section and click on the traffic manager profile in the results that the displayed.</span></span>
2. <span data-ttu-id="2707d-139">**Traffic Manager 프로필** 블레이드에서 **개요**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2707d-139">In the **Traffic Manager profile** blade, click **Overview**.</span></span>
3. <span data-ttu-id="2707d-140">**Traffic Manager 프로필** 블레이드에 사용자의 새로 만든 Traffic Manager 프로필의 DNS 이름이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2707d-140">The **Traffic Manager profile** blade displays the DNS name of your newly created Traffic Manager profile.</span></span> <span data-ttu-id="2707d-141">이는 라우팅 형식에서 결정된 대로 올바른 끝점으로 라우팅되도록 모든 클라이언트가 사용할 수 있습니다(예를 들어 웹 브라우저를 사용하여 이동).</span><span class="sxs-lookup"><span data-stu-id="2707d-141">This can be used by any clients (for example, by navigating to it using a web browser) to get routed to the right endpoint as determined by the routing type.</span></span>  <span data-ttu-id="2707d-142">지리적 라우팅의 경우 Traffic Manager는 들어오는 요청의 원본 IP를 찾아 그 발생 지역을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="2707d-142">In the case of geographic routing, Traffic Manager looks at the source IP of the incoming request and determines the region from which it is originating.</span></span> <span data-ttu-id="2707d-143">해당 지역이 끝점에 매핑된 경우 트래픽은 그곳으로 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="2707d-143">If that region is mapped to an endpoint, traffic is routed to there.</span></span> <span data-ttu-id="2707d-144">이 지역이 끝점에 매핑되지 않은 경우 Traffic Manager는 NODATA 쿼리 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="2707d-144">If this region is not mapped to an endpoint, then Traffic Manager returns a NODATA query response.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2707d-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2707d-145">Next steps</span></span>

- <span data-ttu-id="2707d-146">[지리적 트래픽 라우팅 방법](traffic-manager-routing-methods.md#geographic)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2707d-146">Learn more about [Geographic traffic routing method](traffic-manager-routing-methods.md#geographic).</span></span>
- <span data-ttu-id="2707d-147">[Traffic Manager 설정 테스트](traffic-manager-testing-settings.md)에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="2707d-147">Learn how to [test Traffic Manager settings](traffic-manager-testing-settings.md).</span></span>
