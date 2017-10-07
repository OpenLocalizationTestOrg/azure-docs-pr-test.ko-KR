---
title: "지리적 aaaConfigure 트래픽 라우팅 방법 Azure 트래픽 관리자를 사용 하 여 | Microsoft Docs"
description: "이 문서에서는 어떻게 tooconfigure hello Azure 트래픽 관리자를 사용 하 여 지리적 트래픽 라우팅 방법 설명"
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
ms.openlocfilehash: 4142389211ae54e7feea6564641e01e4477491e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-geographic-traffic-routing-method-using-traffic-manager"></a><span data-ttu-id="44b22-103">트래픽 관리자를 사용 하 여 hello 지리적 트래픽 라우팅 방법 구성</span><span class="sxs-lookup"><span data-stu-id="44b22-103">Configure hello geographic traffic routing method using Traffic Manager</span></span>

<span data-ttu-id="44b22-104">hello 지리적 트래픽 라우팅 방법을 toodirect 트래픽 hello 요청 발생 한 위치 hello 지리적 위치에 따라 toospecific 끝점을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44b22-104">hello Geographic traffic routing method allows you toodirect traffic toospecific endpoints based on hello geographic location where hello requests originate.</span></span> <span data-ttu-id="44b22-105">이 자습서 toocreate 트래픽 관리자 라우팅이 방법으로 프로 파일링 하는 방법을 보여 주고 hello 끝점 tooreceive 트래픽을 특정 지역에서 구성.</span><span class="sxs-lookup"><span data-stu-id="44b22-105">This tutorial shows you how toocreate a Traffic Manager profile with this routing method and configure hello endpoints tooreceive traffic from specific geographies.</span></span>

## <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="44b22-106">Traffic Manager 프로필 만들기</span><span class="sxs-lookup"><span data-stu-id="44b22-106">Create a Traffic Manager Profile</span></span>

1. <span data-ttu-id="44b22-107">Toohello 브라우저에서 로그인 [Azure 포털](http://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="44b22-107">From a browser, sign in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="44b22-108">아직 계정이 없는 경우 [1개월 무료 평가판](https://azure.microsoft.com/free/)을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44b22-108">If you don’t already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free/).</span></span>
2. <span data-ttu-id="44b22-109">Hello 허브 메뉴에서를 클릭 **새로** > **네트워킹** > **스크롤하게**, 클릭 하 고 **트래픽 관리자 프로필**tooopen hello **만들 트래픽 관리자 프로필** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="44b22-109">On hello Hub menu, click **New** > **Networking** > **See all**, and then click **Traffic Manager profile** tooopen hello **Create Traffic Manager profile** blade.</span></span>
3. <span data-ttu-id="44b22-110">Hello에 **만들 트래픽 관리자 프로필** 블레이드:</span><span class="sxs-lookup"><span data-stu-id="44b22-110">On hello **Create Traffic Manager profile** blade:</span></span>
    1. <span data-ttu-id="44b22-111">사용자의 프로필에 사용할 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="44b22-111">Provide a name for your profile.</span></span> <span data-ttu-id="44b22-112">이 이름은 toobe hello trafficmanager.net 영역 내에서 고유 해야 하며 hello DNS 이름이 됩니다 <profilename>, 있으며 trafficmanager.net tooaccess 사용 되는 트래픽 관리자 프로필을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44b22-112">This name needs toobe unique within hello trafficmanager.net zone and will result in hello DNS name <profilename>,trafficmanager.net which will be used tooaccess your Traffic Manager profile.</span></span>
    2. <span data-ttu-id="44b22-113">선택 hello **지리** 라우팅 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="44b22-113">Select hello **Geographic** routing method.</span></span>
    3. <span data-ttu-id="44b22-114">Hello 구독 toocreate 아래에서이 프로필을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="44b22-114">Select hello subscription you want toocreate this profile under.</span></span>
    4. <span data-ttu-id="44b22-115">기존 리소스 그룹을 사용 하거나 새 리소스 그룹 tooplace 아래에서이 프로필을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="44b22-115">Use an existing resource group or create a new resource group tooplace this profile under.</span></span> <span data-ttu-id="44b22-116">Hello를 사용 하 여 toocreate 새 리소스 그룹을 선택 하면 **리소스 그룹 위치** hello 리소스 그룹의 드롭다운 toospecify hello 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="44b22-116">If you choose toocreate a new resource group, use hello **Resource Group location** dropdown toospecify hello location of hello resource group.</span></span> <span data-ttu-id="44b22-117">이 설정은 toohello 위치 hello 리소스 그룹의 나타내며 hello 전체적으로 배포 되는 트래픽 관리자 프로필에는 영향이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="44b22-117">This setting refers toohello location of hello resource group, and has no impact on hello Traffic Manager profile which will be deployed globally.</span></span>
    5. <span data-ttu-id="44b22-118">**만들기**를 클릭하면 사용자의 Traffic Manager 프로필이 생성되고 전역적으로 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="44b22-118">After you click **Create**, your Traffic Manager profile is created and deployed globally.</span></span>

![Traffic Manager 프로필 만들기](./media/traffic-manager-geographic-routing-method/create-traffic-manager-profile.png)

## <a name="add-endpoints"></a><span data-ttu-id="44b22-120">끝점 추가</span><span class="sxs-lookup"><span data-stu-id="44b22-120">Add endpoints</span></span>

1. <span data-ttu-id="44b22-121">Hello 포털 검색 표시줄에 방금 만든 hello 트래픽 관리자 프로필 이름을 검색 하 고 표시 되 면 hello 결과 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="44b22-121">Search for hello Traffic Manager profile name you just created in hello portal’s search bar and click on hello result when it is shown.</span></span>
2. <span data-ttu-id="44b22-122">너무 이동**설정** -> **끝점** hello 트래픽 관리자 블레이드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="44b22-122">Navigate too**Settings** -> **Endpoints** in hello Traffic Manager blade.</span></span>
3. <span data-ttu-id="44b22-123">클릭 **추가** tooshow hello **끝점 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="44b22-123">Click **Add** tooshow hello **Add Endpoint** blade.</span></span>
3. <span data-ttu-id="44b22-124">Hello에 **끝점** 블레이드에서 클릭 **추가** 및 hello **끝점 추가** 블레이드에 표시 되는 다음과 같이 완료:</span><span class="sxs-lookup"><span data-stu-id="44b22-124">In hello **Endpoints** blade, click **Add** and in hello **Add endpoint** blade that is displayed, complete as follows:</span></span>
4. <span data-ttu-id="44b22-125">선택 **형식** 추가 하는 끝점의 hello 유형에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="44b22-125">Select **Type** depending upon hello type of endpoint you are adding.</span></span> <span data-ttu-id="44b22-126">프로덕션에 사용되는 지리적 라우팅 프로필의 경우 둘 이상의 끝점이 있는 자식 프로필을 포함하는 중첩 끝점 형식을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="44b22-126">For geographic routing profiles used in production, we strongly recommend using nested endpoint types containing a child profile with more than one endpoint.</span></span> <span data-ttu-id="44b22-127">자세한 내용은 [지리적 트래픽 라우팅 방법에 대한 FAQ](traffic-manager-FAQs.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="44b22-127">For more details, see [FAQs about geographic traffic routing methods](traffic-manager-FAQs.md).</span></span>
5. <span data-ttu-id="44b22-128">제공 된 **이름** 기준이 될 toorecognize이이 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="44b22-128">Provide a **Name** by which you want toorecognize this endpoint.</span></span>
6. <span data-ttu-id="44b22-129">이 블레이드의 특정 필드를 추가 하는 끝점의 hello 형식에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="44b22-129">Certain fields in this blade depend on hello type of endpoint you are adding:</span></span>
    1. <span data-ttu-id="44b22-130">Azure 끝점을 추가 하는 경우 선택 hello **대상 리소스 종류** 및 hello **대상** hello 리소스에 따라 원하는 toodirect 트래픽을</span><span class="sxs-lookup"><span data-stu-id="44b22-130">If you are adding an Azure endpoint, select hello **Target resource type** and hello **Target** based on hello resource you want toodirect traffic to</span></span>
    2. <span data-ttu-id="44b22-131">추가 하는 경우는 **외부** 끝점 hello 제공 **정규화 된 도메인 이름 (FQDN)** 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="44b22-131">If you are adding an **External** endpoint, provide hello **Fully-qualified domain name (FQDN)** for your endpoint.</span></span>
    3. <span data-ttu-id="44b22-132">추가 하는 경우는 **Nested 끝점**선택, hello **대상 리소스** 해당 toohello 자식 프로필 toouse을 hello를 지정 하는 **최소 자식 끝점계산**.</span><span class="sxs-lookup"><span data-stu-id="44b22-132">If you are adding a **Nested endpoint**, select hello **Target resource** that corresponds toohello child profile you want toouse and specify hello **Minimum child endpoints count**.</span></span>
7. <span data-ttu-id="44b22-133">Hello 지도 섹션을 사용 하 여 hello 트래픽을 전송 toobe toothis 끝점 저장할에서 tooadd hello 지역 드롭다운입니다.</span><span class="sxs-lookup"><span data-stu-id="44b22-133">In hello Geo-mapping section, use hello drop down tooadd hello regions from where you want traffic toobe sent toothis endpoint.</span></span> <span data-ttu-id="44b22-134">하나 이상의 영역을 추가해야 하며 여러 지역을 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44b22-134">You must add at least one region, and you can have multiple regions mapped.</span></span>
8. <span data-ttu-id="44b22-135">모든 끝점에 대해이 단계를 반복이 프로필에서 tooadd 원하는</span><span class="sxs-lookup"><span data-stu-id="44b22-135">Repeat this for all endpoints you want tooadd under this profile</span></span>

![Traffic Manager 끝점 추가](./media/traffic-manager-geographic-routing-method/add-traffic-manager-endpoint.png)

## <a name="use-hello-traffic-manager-profile"></a><span data-ttu-id="44b22-137">Hello 트래픽 관리자 프로필을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="44b22-137">Use hello Traffic Manager profile</span></span>
1.  <span data-ttu-id="44b22-138">Hello hello 포털 검색 창에서 검색할 **트래픽 관리자 프로필** 이름 hello 섹션 앞에서 만든 하 고 결과 표시 하는 hello hello에 hello 트래픽 관리자 프로필을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="44b22-138">In hello portal’s search bar, search for hello **Traffic Manager profile** name that you created in hello preceding section and click on hello traffic manager profile in hello results that hello displayed.</span></span>
2. <span data-ttu-id="44b22-139">Hello에 **트래픽 관리자 프로필** 블레이드에서 클릭 **개요**합니다.</span><span class="sxs-lookup"><span data-stu-id="44b22-139">In hello **Traffic Manager profile** blade, click **Overview**.</span></span>
3. <span data-ttu-id="44b22-140">hello **트래픽 관리자 프로필** 블레이드를 새로 만든된 트래픽 관리자 프로필의 hello DNS 이름을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="44b22-140">hello **Traffic Manager profile** blade displays hello DNS name of your newly created Traffic Manager profile.</span></span> <span data-ttu-id="44b22-141">이 끝점에 의해 모든 클라이언트 (예를 들어 이동 하 여 웹 브라우저를 사용 하 여 tooit) 라우팅된 tooget toohello 오른쪽 hello 라우팅 유형을 기준으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44b22-141">This can be used by any clients (for example, by navigating tooit using a web browser) tooget routed toohello right endpoint as determined by hello routing type.</span></span>  <span data-ttu-id="44b22-142">Hello 지리적 라우팅의 경우에서 트래픽 관리자 hello 들어오는 요청의 소스 IP hello 찾은 hello 영역을 발생 하는 것을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="44b22-142">In hello case of geographic routing, Traffic Manager looks at hello source IP of hello incoming request and determines hello region from which it is originating.</span></span> <span data-ttu-id="44b22-143">해당 지역의 매핑된 tooan 끝점 이면 트래픽은 라우트된 toothere입니다.</span><span class="sxs-lookup"><span data-stu-id="44b22-143">If that region is mapped tooan endpoint, traffic is routed toothere.</span></span> <span data-ttu-id="44b22-144">이 영역의 매핑된 tooan 끝점이 없는 경우 트래픽 관리자는 NODATA 쿼리 응답을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="44b22-144">If this region is not mapped tooan endpoint, then Traffic Manager returns a NODATA query response.</span></span>

## <a name="next-steps"></a><span data-ttu-id="44b22-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="44b22-145">Next steps</span></span>

- <span data-ttu-id="44b22-146">[지리적 트래픽 라우팅 방법](traffic-manager-routing-methods.md#geographic)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="44b22-146">Learn more about [Geographic traffic routing method](traffic-manager-routing-methods.md#geographic).</span></span>
- <span data-ttu-id="44b22-147">너무 방법에 대해 알아봅니다[트래픽 관리자 설정을 테스트](traffic-manager-testing-settings.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="44b22-147">Learn how too[test Traffic Manager settings](traffic-manager-testing-settings.md).</span></span>
