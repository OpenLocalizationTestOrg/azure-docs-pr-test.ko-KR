---
title: "azure에서 트래픽 관리자 프로필 aaaCreate | Microsoft Docs"
description: "이 문서에서는 설명 방법을 toocreate 트래픽 관리자 프로필"
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
ms.openlocfilehash: 5cd3d2903552c9a0427da41a73f6f38f6b0afc1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="5e1f1-103">Traffic Manager 프로필 만들기</span><span class="sxs-lookup"><span data-stu-id="5e1f1-103">Create a Traffic Manager profile</span></span>

<span data-ttu-id="5e1f1-104">이 문서에 설명 된 프로필 **우선 순위** 라우팅 유형을 tooroute 사용자 tootwo Azure 웹 앱 끝점을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e1f1-104">This article describes how a profile with **Priority** routing type can be created tooroute users tootwo Azure Web Apps endpoints.</span></span> <span data-ttu-id="5e1f1-105">Hello를 사용 하 여 **우선 순위** 라우팅 유형을, 모든 트래픽이 상태인 라우트된 toohello 첫 번째 끝점 둘째 hello 백업으로 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e1f1-105">By using hello **Priority** routing type, all traffic is routed toohello first endpoint while hello second is kept as a backup.</span></span> <span data-ttu-id="5e1f1-106">결과적으로, 사용자가 첫 번째 끝점 hello 비정상 상태가 되 라우트된 toohello 두 번째 끝점 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e1f1-106">As a result, users can be routed toohello second endpoint if hello first endpoint becomes unhealthy.</span></span>

<span data-ttu-id="5e1f1-107">이 문서에서는 두 개의 이전에 만든된 Azure 웹 앱 끝점은 새로 만든 연결된 toothis 트래픽 관리자 프로필입니다.</span><span class="sxs-lookup"><span data-stu-id="5e1f1-107">In this article, two previously created Azure Web App endpoints are associated toothis newly created Traffic Manager profile.</span></span> <span data-ttu-id="5e1f1-108">방법에 대 한 자세한 toolearn toocreate Azure 웹 앱 끝점 방문 hello [Azure 웹 앱 설명서 페이지](https://docs.microsoft.com/azure/app-service-web/)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1f1-108">toolearn more about how toocreate Azure Web App endpoints, visit hello [Azure Web Apps documentation page](https://docs.microsoft.com/azure/app-service-web/).</span></span> <span data-ttu-id="5e1f1-109">DNS 이름이 고를 통해 연결할 수 있는 모든 끝점을 추가할 수 있습니다 hello 공용 인터넷 및 예를 들어 Azure 웹 앱 끝점을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1f1-109">You can add any endpoint that has a DNS name and is reachable over hello public internet and that we are using Azure Web Apps endpoints as an example.</span></span>

### <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="5e1f1-110">Traffic Manager 프로필 만들기</span><span class="sxs-lookup"><span data-stu-id="5e1f1-110">Create a Traffic Manager profile</span></span>
1. <span data-ttu-id="5e1f1-111">Toohello 브라우저에서 로그인 [Azure 포털](http://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1f1-111">From a browser, sign in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="5e1f1-112">계정이 아직 없는 경우 [1개월 무료 평가판](https://azure.microsoft.com/free/)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e1f1-112">If you don’t already have an account, you can sign-up for a [free one-month trial](https://azure.microsoft.com/free/).</span></span> 
2. <span data-ttu-id="5e1f1-113">Hello에 **허브** 메뉴를 클릭 **새로** > **네트워킹** > **스크롤하게**, 클릭 **트래픽 관리자** 프로필 tooopen hello **만들 트래픽 관리자 프로필** 블레이드에서 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1f1-113">On hello **Hub** menu, click **New** > **Networking** > **See all**, click **Traffic Manager** profile tooopen hello **Create Traffic Manager profile** blade, then click **Create**.</span></span>
3. <span data-ttu-id="5e1f1-114">Hello에 **만들 트래픽 관리자 프로필** 블레이드를 다음과 같이 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1f1-114">On hello **Create Traffic Manager profile** blade, complete as follows:</span></span>
    1. <span data-ttu-id="5e1f1-115">**이름**에서 사용자의 프로필에 사용할 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1f1-115">In **Name**, provide a name for your profile.</span></span> <span data-ttu-id="5e1f1-116">이 이름은 toobe hello trafficmanager.net 영역 내에서 고유 해야 하며 hello DNS 이름으로 인해 <name>, 사용 되는 tooaccess 인 trafficmanager.net 트래픽 관리자 프로필.</span><span class="sxs-lookup"><span data-stu-id="5e1f1-116">This name needs toobe unique within hello trafficmanager.net zone and results in hello DNS name <name>,trafficmanager.net which is used tooaccess your Traffic Manager profile.</span></span>
    2. <span data-ttu-id="5e1f1-117">**라우팅 메서드**선택, hello **우선 순위** 라우팅 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="5e1f1-117">In **Routing method**, select hello **Priority** routing method.</span></span>
    3. <span data-ttu-id="5e1f1-118">**구독**, toocreate 아래에서이 프로필을 원하는 hello 구독 선택</span><span class="sxs-lookup"><span data-stu-id="5e1f1-118">In **Subscription**, select hello subscription you want toocreate this profile under</span></span>
    4. <span data-ttu-id="5e1f1-119">**리소스 그룹**, 새 리소스 그룹 tooplace 아래에서이 프로필을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5e1f1-119">In **Resource Group**, create a new resource group tooplace this profile under.</span></span>
    5. <span data-ttu-id="5e1f1-120">**리소스 그룹 위치**, hello 리소스 그룹의 hello 위치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1f1-120">In **Resource group location**, select hello location of hello resource group.</span></span> <span data-ttu-id="5e1f1-121">이 설정은 hello 리소스 그룹의 toohello 위치를 나타내며 hello 전체적으로 배포 될 트래픽 관리자 프로필에 어떠한 영향도 미치지.</span><span class="sxs-lookup"><span data-stu-id="5e1f1-121">This setting refers toohello location of hello resource group, and has no impact on hello Traffic Manager profile that will be deployed globally.</span></span>
    6. <span data-ttu-id="5e1f1-122">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1f1-122">Click **Create**.</span></span>
    7. <span data-ttu-id="5e1f1-123">트래픽 관리자 프로필의 hello 전역 배포 완료 되 면 hello 리소스 중 하나로 각 리소스 그룹에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e1f1-123">When hello global deployment of your Traffic Manager profile is complete, it is listed in respective resource group as one of hello resources.</span></span>

    ![Traffic Manager 프로필 만들기](./media/traffic-manager-create-profile/Create-traffic-manager-profile.png)

## <a name="add-traffic-manager-endpoints"></a><span data-ttu-id="5e1f1-125">Traffic Manager 끝점 추가</span><span class="sxs-lookup"><span data-stu-id="5e1f1-125">Add Traffic Manager endpoints</span></span>

1. <span data-ttu-id="5e1f1-126">Hello hello 포털 검색 창에서 검색할 **트래픽 관리자 프로필** 결과 표시 하는 hello hello hello에서 섹션을 클릭 하 고 hello 트래픽 관리자 프로필을 앞에서 만든 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5e1f1-126">In hello portal’s search bar, search for hello **Traffic Manager profile** name that you created in hello preceding section and click hello traffic manager profile in hello results that hello displayed.</span></span>
2. <span data-ttu-id="5e1f1-127">Hello에 **트래픽 관리자 프로필** 블레이드 hello **설정** 섹션에서 클릭 **끝점**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1f1-127">In hello **Traffic Manager profile** blade, in hello **Settings** section, click **Endpoints**.</span></span>
3. <span data-ttu-id="5e1f1-128">Hello에 **끝점** 블레이드에 표시 되는 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1f1-128">In hello **Endpoints** blade that is displayed, click **Add**.</span></span>
4. <span data-ttu-id="5e1f1-129">Hello에 **끝점 추가** 블레이드를 다음과 같이 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1f1-129">In hello **Add endpoint** blade, complete as follows:</span></span>
    1. <span data-ttu-id="5e1f1-130">**형식**의 경우 **Azure 끝점**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1f1-130">For **Type**, click **Azure endpoint**.</span></span>
    2. <span data-ttu-id="5e1f1-131">제공 된 **이름** 기준이 될 toorecognize이이 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="5e1f1-131">Provide a **Name** by which you want toorecognize this endpoint.</span></span>
    3. <span data-ttu-id="5e1f1-132">**대상 리소스 형식**의 경우 **App Service**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1f1-132">For **Target resource type**, click **App Service**.</span></span>
    4. <span data-ttu-id="5e1f1-133">에 대 한 **대상 리소스**, 클릭 **앱 서비스 선택** tooshow hello 목록이 hello에서 웹 앱 hello 동일한 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1f1-133">For **Target resource**, click **Choose an app service** tooshow hello listing of hello Web Apps under hello same subscription.</span></span> <span data-ttu-id="5e1f1-134">Hello에 **리소스** 블레이드를 표시 되 면 선택 hello hello 첫 번째 끝점으로 tooadd 되도록 응용 프로그램 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="5e1f1-134">In hello **Resource** blade that is displayed, pick hello App service that you want tooadd as hello first endpoint.</span></span>
    5. <span data-ttu-id="5e1f1-135">**우선 순위**의 경우 **1**로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1f1-135">For **Priority**, select as **1**.</span></span> <span data-ttu-id="5e1f1-136">따라서 정상 상태 이면 toothis 끝점이 모든 트래픽이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e1f1-136">This results in all traffic going toothis endpoint if it is healthy.</span></span>
    6. <span data-ttu-id="5e1f1-137">**사용 안 함으로 추가**를 선택 취소 상태로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1f1-137">Keep **Add as disabled** unchecked.</span></span>
    7. <span data-ttu-id="5e1f1-138">**확인**</span><span class="sxs-lookup"><span data-stu-id="5e1f1-138">Click **OK**</span></span>
5.  <span data-ttu-id="5e1f1-139">Hello 다음 Azure 웹 앱 끝점에 대해 3 및 4 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1f1-139">Repeat steps 3 and 4 for hello next Azure Web Apps endpoint.</span></span> <span data-ttu-id="5e1f1-140">있는지 tooadd 확인 사용 하 여 해당 **우선 순위** 값 설정에서 **2**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1f1-140">Make sure tooadd it with its **Priority** value set at **2**.</span></span>
6.  <span data-ttu-id="5e1f1-141">Hello에 표시 된 두 끝점 모두의 hello 추가 완료 되 면 **트래픽 관리자 프로필** 블레이드로 모니터링 상태와 함께 **온라인**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1f1-141">When hello addition of both endpoints is complete, they are displayed in hello **Traffic Manager profile** blade along with their monitoring status as **Online**.</span></span>

    ![Traffic Manager 끝점 추가](./media/traffic-manager-create-profile/add-traffic-manager-endpoint.png)

## <a name="use-hello-traffic-manager-profile"></a><span data-ttu-id="5e1f1-143">Hello 트래픽 관리자 프로필을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="5e1f1-143">Use hello Traffic Manager profile</span></span>
1.  <span data-ttu-id="5e1f1-144">Hello hello 포털 검색 창에서 검색할 **트래픽 관리자 프로필** hello 섹션 앞에서 만든 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5e1f1-144">In hello portal’s search bar, search for hello **Traffic Manager profile** name that you created in hello preceding section.</span></span> <span data-ttu-id="5e1f1-145">표시 되는 hello 결과 hello 트래픽 관리자 프로필을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1f1-145">In hello results that are displayed, click hello traffic manager profile.</span></span>
2. <span data-ttu-id="5e1f1-146">Hello에 **트래픽 관리자 프로필** 블레이드에서 클릭 **개요**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1f1-146">In hello **Traffic Manager profile** blade, click **Overview**.</span></span>
3. <span data-ttu-id="5e1f1-147">hello **트래픽 관리자 프로필** 블레이드를 새로 만든된 트래픽 관리자 프로필의 hello DNS 이름을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1f1-147">hello **Traffic Manager profile** blade displays hello DNS name of your newly created Traffic Manager profile.</span></span> <span data-ttu-id="5e1f1-148">이 끝점에 의해 모든 클라이언트 (예를 들어 이동 하 여 웹 브라우저를 사용 하 여 tooit) 라우팅된 tooget toohello 오른쪽 hello 라우팅 유형을 기준으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e1f1-148">This can be used by any clients (for example, by navigating tooit using a web browser) tooget routed toohello right endpoint as determined by hello routing type.</span></span> <span data-ttu-id="5e1f1-149">이 경우 모든 요청 라우트된 toohello 첫 번째 끝점은 및 트래픽 관리자에서 감지할 경우 수 정상 경우 hello 트래픽 toohello 다음 끝점을 통해 자동으로 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1f1-149">In this case, all requests are routed toohello first endpoint and if Traffic Manager detects it be unhealthy, hello traffic automatically fails over toohello next endpoint.</span></span>

## <a name="delete-hello-traffic-manager-profile"></a><span data-ttu-id="5e1f1-150">Hello 트래픽 관리자 프로필 삭제</span><span class="sxs-lookup"><span data-stu-id="5e1f1-150">Delete hello Traffic Manager profile</span></span>
<span data-ttu-id="5e1f1-151">더 이상 필요 hello 리소스 그룹 및 사용자가 만든 hello 트래픽 관리자 프로필을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1f1-151">When no longer needed, delete hello resource group and hello Traffic Manager profile that you have created.</span></span> <span data-ttu-id="5e1f1-152">따라서 toodo hello에서 hello 리소스 그룹을 선택 **트래픽 관리자 프로필** 블레이드에 대 한 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e1f1-152">toodo so, select hello resource group from hello **Traffic Manager profile** blade and click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e1f1-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5e1f1-153">Next steps</span></span>

- <span data-ttu-id="5e1f1-154">[라우팅 형식](traffic-manager-routing-methods.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="5e1f1-154">Learn more about [routing types](traffic-manager-routing-methods.md).</span></span>
- <span data-ttu-id="5e1f1-155">[끝점 형식](traffic-manager-endpoint-types.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="5e1f1-155">Learn more about endpoint types [endpoint types](traffic-manager-endpoint-types.md).</span></span>
- <span data-ttu-id="5e1f1-156">[끝점 모니터링](traffic-manager-monitoring.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="5e1f1-156">Learn more about [endpoint monitoring](traffic-manager-monitoring.md).</span></span>



