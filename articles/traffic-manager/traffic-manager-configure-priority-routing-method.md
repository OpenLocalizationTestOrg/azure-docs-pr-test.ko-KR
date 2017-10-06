---
title: "aaaConfigure 우선 순위 트래픽 라우팅 방법 Azure 트래픽 관리자를 사용 하 여 | Microsoft Docs"
description: "이 문서에서는 tooconfigure hello 우선 순위 트래픽 라우팅 방법 트래픽 관리자에서 어떻게 설명"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 6dca6de1-18f7-4962-bd98-6055771fab22
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/20/2017
ms.author: kumud
ms.openlocfilehash: dd3e3bb2a727e5ea087cee35962c8e6f7c357282
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-priority-traffic-routing-method-in-traffic-manager"></a><span data-ttu-id="814dd-103">Traffic Manager에서 우선 순위 트래픽 라우팅 방법 구성</span><span class="sxs-lookup"><span data-stu-id="814dd-103">Configure priority traffic routing method in Traffic Manager</span></span>

<span data-ttu-id="814dd-104">Hello 웹 사이트 모드에 관계 없이 Azure 웹 사이트는 데이터 센터 (지역이 라고도 함) 내 웹 사이트에 대 한 장애 조치 기능을 이미 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="814dd-104">Regardless of hello website mode, Azure Websites already provide failover functionality for websites within a datacenter (also known as a region).</span></span> <span data-ttu-id="814dd-105">Traffic Manager는 다른 데이터 센터의 웹 사이트에 대해 장애 조치(Failover)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="814dd-105">Traffic Manager provides failover for websites in different datacenters.</span></span>

<span data-ttu-id="814dd-106">일반적인 서비스 장애 조치 패턴 toosend 트래픽 tooa 기본 서비스 이며의 장애 조치에 대해 동일한 백업 서비스 집합을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="814dd-106">A common pattern for service failover is toosend traffic tooa primary service and provide a set of identical backup services for failover.</span></span> <span data-ttu-id="814dd-107">hello 다음 단계에서는 설명 어떻게 tooconfigure이 우선 순위가 지정 된 Azure 클라우드 서비스 및 웹 사이트 장애 조치:</span><span class="sxs-lookup"><span data-stu-id="814dd-107">hello following steps explain how tooconfigure this prioritized failover with Azure cloud services and websites:</span></span>

## <a name="tooconfigure-hello-priority-traffic-routing-method"></a><span data-ttu-id="814dd-108">tooconfigure hello 우선 순위 트래픽 라우팅 방법</span><span class="sxs-lookup"><span data-stu-id="814dd-108">tooconfigure hello priority traffic routing method</span></span>

1. <span data-ttu-id="814dd-109">Toohello 브라우저에서 로그인 [Azure 포털](http://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="814dd-109">From a browser, sign in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="814dd-110">아직 계정이 없는 경우 [1개월 무료 평가판](https://azure.microsoft.com/free/)을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="814dd-110">If you don’t already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free/).</span></span> 
2. <span data-ttu-id="814dd-111">Hello hello 포털 검색 창에서 검색할 **트래픽 관리자 프로필** tooconfigure hello에 대 한 라우팅 메서드를 원하는 hello 프로필 이름을 클릭 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="814dd-111">In hello portal’s search bar, search for hello **Traffic Manager profiles** and then click hello profile name that you want tooconfigure hello routing method for.</span></span>
3. <span data-ttu-id="814dd-112">Hello에 **트래픽 관리자 프로필** 블레이드를 둘 다 hello 클라우드 서비스를 구성에서 tooinclude 되도록 웹 사이트를 사용할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="814dd-112">In hello **Traffic Manager profile** blade, verify that both hello cloud services and websites that you want tooinclude in your configuration are present.</span></span>
4. <span data-ttu-id="814dd-113">Hello에 **설정** 섹션에서 클릭 **구성**, 및 hello **구성** 블레이드를 다음과 같이 완료:</span><span class="sxs-lookup"><span data-stu-id="814dd-113">In hello **Settings** section, click **Configuration**, and in hello **Configuration** blade, complete as follows:</span></span>
    1. <span data-ttu-id="814dd-114">에 대 한 **트래픽 라우팅 방법 설정**, hello 트래픽 라우팅 방법 인지 확인 **우선 순위**합니다.</span><span class="sxs-lookup"><span data-stu-id="814dd-114">For **traffic routing method settings**, verify that hello traffic routing method is **Priority**.</span></span> <span data-ttu-id="814dd-115">없는 경우 클릭 **우선 순위** hello 드롭다운 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="814dd-115">If it is not, click **Priority** from hello dropdown list.</span></span>
    2. <span data-ttu-id="814dd-116">집합 hello **끝점 모니터 설정** 다음과 같이이 프로필 내의 모든 모든 끝점에 대해 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="814dd-116">Set hello **Endpoint monitor settings** identical for all every endpoint within this profile as follows:</span></span>
        1. <span data-ttu-id="814dd-117">적절 한 선택 hello **프로토콜**, hello 지정 **포트** 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="814dd-117">Select hello appropriate **Protocol**, and specify hello **Port** number.</span></span> 
        2. <span data-ttu-id="814dd-118">**경로**에서 슬래시  */* 를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="814dd-118">For **Path** type a forward slash */*.</span></span> <span data-ttu-id="814dd-119">toomonitor 끝점 경로 파일 이름을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="814dd-119">toomonitor endpoints, you must specify a path and filename.</span></span> <span data-ttu-id="814dd-120">A 슬래시 "/" hello 상대 경로 대 한 유효한 항목 및 hello이 파일은 hello 루트 디렉터리 (기본값)를 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="814dd-120">A forward slash "/" is a valid entry for hello relative path and implies that hello file is in hello root directory (default).</span></span>
        3. <span data-ttu-id="814dd-121">Hello hello 페이지의 위쪽에 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="814dd-121">At hello top of hello page, click **Save**.</span></span>
5. <span data-ttu-id="814dd-122">Hello에 **설정** 섹션에서 클릭 **끝점**합니다.</span><span class="sxs-lookup"><span data-stu-id="814dd-122">In hello **Settings** section, click **Endpoints**.</span></span>
6. <span data-ttu-id="814dd-123">Hello에 **끝점** 블레이드를 끝점에 대 한 hello 우선 순위 순서를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="814dd-123">In hello **Endpoints** blade, review hello priority order for your endpoints.</span></span> <span data-ttu-id="814dd-124">Hello를 선택 하는 경우 **우선 순위** 트래픽 라우팅 방법을 선택 하는 hello 끝점의 hello 순서가 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="814dd-124">When you select hello **Priority** traffic routing method, hello order of hello selected endpoints matters.</span></span> <span data-ttu-id="814dd-125">끝점의 hello 우선 순위 순서를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="814dd-125">Verify hello priority order of endpoints.</span></span>  <span data-ttu-id="814dd-126">hello 기본 끝점 위에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="814dd-126">hello primary endpoint is on top.</span></span> <span data-ttu-id="814dd-127">표시 되는 hello 순서에 다시 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="814dd-127">Double-check on hello order it is displayed.</span></span> <span data-ttu-id="814dd-128">모든 요청 라우트된 toohello 첫 번째 끝점을 트래픽 관리자에서 감지할 경우 수 정상, hello 트래픽 toohello 다음 끝점을 통해 자동으로 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="814dd-128">all requests will be routed toohello first endpoint and if Traffic Manager detects it be unhealthy, hello traffic automatically fails over toohello next endpoint.</span></span> 
7. <span data-ttu-id="814dd-129">toochange hello 끝점 우선 순위 순서를 hello 끝점을 클릭 하 고 hello에 **끝점** 블레이드에 표시 되는 클릭 **편집** hello를 변경 하 고 **우선 순위** 필요에 따라 값 .</span><span class="sxs-lookup"><span data-stu-id="814dd-129">toochange hello endpoint priority order, click hello endpoint, and in hello **Endpoint** blade that is displayed, click **Edit** and change hello **Priority** value as needed.</span></span> 
8. <span data-ttu-id="814dd-130">클릭 **저장** toosave hello 끝점 설정을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="814dd-130">Click **Save** toosave change hello endpoint settings.</span></span>
9. <span data-ttu-id="814dd-131">구성 변경을 완료 한 후 클릭 **저장** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="814dd-131">After you complete your configuration changes, click **Save** at hello bottom of hello page.</span></span>
10. <span data-ttu-id="814dd-132">다음과 같이 구성에서 hello 변경 내용 테스트:</span><span class="sxs-lookup"><span data-stu-id="814dd-132">Test hello changes in your configuration as follows:</span></span>
    1.  <span data-ttu-id="814dd-133">Hello 포털 검색 표시줄에 hello 트래픽 관리자 프로필 이름을 검색 하 고 표시 하는 hello hello 결과에 hello 트래픽 관리자 프로필을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="814dd-133">In hello portal’s search bar, search for hello Traffic Manager profile name and click hello Traffic Manager profile in hello results that hello displayed.</span></span>
    2.  <span data-ttu-id="814dd-134">Hello에 **트래픽 관리자** 블레이드 프로필을 클릭 하 여 **개요**합니다.</span><span class="sxs-lookup"><span data-stu-id="814dd-134">In hello **Traffic Manager** profile blade, click **Overview**.</span></span>
    3.  <span data-ttu-id="814dd-135">hello **트래픽 관리자 프로필** 블레이드를 새로 만든된 트래픽 관리자 프로필의 hello DNS 이름을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="814dd-135">hello **Traffic Manager profile** blade displays hello DNS name of your newly created Traffic Manager profile.</span></span> <span data-ttu-id="814dd-136">이 끝점에 의해 모든 클라이언트 (예를 들어 이동 하 여 웹 브라우저를 사용 하 여 tooit) 라우팅된 tooget toohello 오른쪽 hello 라우팅 유형을 기준으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="814dd-136">This can be used by any clients (for example, by navigating tooit using a web browser) tooget routed toohello right endpoint as determined by hello routing type.</span></span> <span data-ttu-id="814dd-137">이 경우 모든 요청 라우트된 toohello 첫 번째 끝점은 트래픽 관리자에서 감지할 경우가 되는 하지 정상 hello 트래픽 toohello 다음 끝점으로 자동으로 장애 조치 합니다.</span><span class="sxs-lookup"><span data-stu-id="814dd-137">In this case all requests are routed toohello first endpoint and if Traffic Manager detects it be unhealthy, hello traffic automatically fails over toohello next endpoint.</span></span>
11. <span data-ttu-id="814dd-138">트래픽 관리자 프로필 작동 되 면 hello DNS 레코드에 권한 있는 DNS 서버 toopoint에 회사 도메인 이름 toohello 트래픽 관리자 도메인 이름을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="814dd-138">Once your Traffic Manager profile is working, edit hello DNS record on your authoritative DNS server toopoint your company domain name toohello Traffic Manager domain name.</span></span>

![Traffic Manager를 사용한 우선 순위 트래픽 라우팅 방법 구성][1]

## <a name="next-steps"></a><span data-ttu-id="814dd-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="814dd-140">Next steps</span></span>


- <span data-ttu-id="814dd-141">[가중치 적용 트래픽 라우팅 방법](traffic-manager-configure-weighted-routing-method.md)에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="814dd-141">Learn about [weighted traffic routing method](traffic-manager-configure-weighted-routing-method.md).</span></span>
- <span data-ttu-id="814dd-142">[성능 라우팅 방법](traffic-manager-configure-performance-routing-method.md)에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="814dd-142">Learn about [performance routing method](traffic-manager-configure-performance-routing-method.md).</span></span>
- <span data-ttu-id="814dd-143">[지리적 라우팅 방법](traffic-manager-configure-geographic-routing-method.md)에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="814dd-143">Learn about [geographic routing method](traffic-manager-configure-geographic-routing-method.md).</span></span>
- <span data-ttu-id="814dd-144">너무 방법에 대해 알아봅니다[트래픽 관리자 설정을 테스트](traffic-manager-testing-settings.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="814dd-144">Learn how too[test Traffic Manager settings](traffic-manager-testing-settings.md).</span></span>

<!--Image references-->
[1]: ./media/traffic-manager-priority-routing-method/traffic-manager-priority-routing-method.png