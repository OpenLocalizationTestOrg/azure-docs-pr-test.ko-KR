---
title: "가 중 aaaConfigure 라운드 로빈 트래픽 라우팅 방법 Azure 트래픽 관리자를 사용 하 여 | Microsoft Docs"
description: "이 문서에서는 tooload 트래픽 관리자의 라운드 로빈 메서드를 사용 하 여 트래픽을 분산 하는 방법을 설명 합니다."
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
ms.openlocfilehash: 7e2866ead0b2b653845435dd420a763c5e175f4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-weighted-traffic-routing-method-in-traffic-manager"></a><span data-ttu-id="d9afb-103">트래픽 관리자의가 중 hello 트래픽 라우팅 방법 구성</span><span class="sxs-lookup"><span data-stu-id="d9afb-103">Configure hello weighted traffic routing method in Traffic Manager</span></span>

<span data-ttu-id="d9afb-104">일반적인 트래픽 라우팅 메서드 패턴은 tooprovide 클라우드 서비스 및 웹 사이트를 포함 하는 라운드 로빈 방식으로 트래픽을 tooeach 보낼 동일한 끝점의 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="d9afb-104">A common traffic routing method pattern is tooprovide a set of identical endpoints, which include cloud services and websites, and send traffic tooeach in a round-robin fashion.</span></span> <span data-ttu-id="d9afb-105">단계를 수행 하는 hello 어떻게 tooconfigure이 유형의 설명 트래픽 라우팅 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="d9afb-105">hello following steps outline how tooconfigure this type of traffic routing method.</span></span>

> [!NOTE]
> <span data-ttu-id="d9afb-106">Azure Websites는 데이터 센터(지역이라고도 함) 내의 웹 사이트에 대해 이미 라운드 로빈 부하 분산 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d9afb-106">Azure Websites already provide round-robin load balancing functionality for websites within a datacenter (also known as a region).</span></span> <span data-ttu-id="d9afb-107">트래픽 관리자 다른 데이터 센터의 웹 사이트에 대 한 라운드 로빈 트래픽 라우팅 방법을 toospecify를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9afb-107">Traffic Manager allows you toospecify round-robin traffic routing method for websites in different datacenters.</span></span>

## <a name="tooconfigure-hello-weighted-traffic-routing-method"></a><span data-ttu-id="d9afb-108">tooconfigure 가중치 hello 트래픽 라우팅 방법</span><span class="sxs-lookup"><span data-stu-id="d9afb-108">tooconfigure hello weighted traffic routing method</span></span>

1. <span data-ttu-id="d9afb-109">Toohello 브라우저에서 로그인 [Azure 포털](http://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="d9afb-109">From a browser, sign in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="d9afb-110">아직 계정이 없는 경우 [1개월 무료 평가판](https://azure.microsoft.com/free/)을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9afb-110">If you don’t already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free/).</span></span> 
2. <span data-ttu-id="d9afb-111">Hello hello 포털 검색 창에서 검색할 **트래픽 관리자 프로필** tooconfigure hello에 대 한 라우팅 메서드를 원하는 hello 프로필 이름을 클릭 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9afb-111">In hello portal’s search bar, search for hello **Traffic Manager profiles** and then click hello profile name that you want tooconfigure hello routing method for.</span></span>
3. <span data-ttu-id="d9afb-112">Hello에 **트래픽 관리자 프로필** 블레이드를 둘 다 hello 클라우드 서비스를 구성에서 tooinclude 되도록 웹 사이트를 사용할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9afb-112">In hello **Traffic Manager profile** blade, verify that both hello cloud services and websites that you want tooinclude in your configuration are present.</span></span>
4. <span data-ttu-id="d9afb-113">Hello에 **설정** 섹션에서 클릭 **구성**, 및 hello **구성** 블레이드를 다음과 같이 완료:</span><span class="sxs-lookup"><span data-stu-id="d9afb-113">In hello **Settings** section, click **Configuration**, and in hello **Configuration** blade, complete as follows:</span></span>
    1. <span data-ttu-id="d9afb-114">에 대 한 **트래픽 라우팅 방법 설정**, hello 트래픽 라우팅 방법 인지 확인 **가 중**합니다.</span><span class="sxs-lookup"><span data-stu-id="d9afb-114">For **traffic routing method settings**, verify that hello traffic routing method is **Weighted**.</span></span> <span data-ttu-id="d9afb-115">없는 경우 클릭 **가 중** hello 드롭다운 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9afb-115">If it is not, click **Weighted** from hello dropdown list.</span></span>
    2. <span data-ttu-id="d9afb-116">집합 hello **끝점 모니터 설정** 다음과 같이이 프로필 내의 모든 모든 끝점에 대해 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9afb-116">Set hello **Endpoint monitor settings** identical for all every endpoint within this profile as follows:</span></span>
        1. <span data-ttu-id="d9afb-117">적절 한 선택 hello **프로토콜**, hello 지정 **포트** 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="d9afb-117">Select hello appropriate **Protocol**, and specify hello **Port** number.</span></span> 
        2. <span data-ttu-id="d9afb-118">**경로**에서 슬래시  */* 를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d9afb-118">For **Path** type a forward slash */*.</span></span> <span data-ttu-id="d9afb-119">toomonitor 끝점 경로 파일 이름을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9afb-119">toomonitor endpoints, you must specify a path and filename.</span></span> <span data-ttu-id="d9afb-120">A 슬래시 "/" hello 상대 경로 대 한 유효한 항목 및 hello이 파일은 hello 루트 디렉터리 (기본값)를 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9afb-120">A forward slash "/" is a valid entry for hello relative path and implies that hello file is in hello root directory (default).</span></span>
        3. <span data-ttu-id="d9afb-121">Hello hello 페이지의 위쪽에 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="d9afb-121">At hello top of hello page, click **Save**.</span></span>
5. <span data-ttu-id="d9afb-122">다음과 같이 구성에서 hello 변경 내용 테스트:</span><span class="sxs-lookup"><span data-stu-id="d9afb-122">Test hello changes in your configuration as follows:</span></span>
    1.  <span data-ttu-id="d9afb-123">Hello 포털 검색 표시줄에 hello 트래픽 관리자 프로필 이름을 검색 하 고 표시 하는 hello hello 결과에 hello 트래픽 관리자 프로필을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9afb-123">In hello portal’s search bar, search for hello Traffic Manager profile name and click hello Traffic Manager profile in hello results that hello displayed.</span></span>
    2.  <span data-ttu-id="d9afb-124">Hello에 **트래픽 관리자** 블레이드 프로필을 클릭 하 여 **개요**합니다.</span><span class="sxs-lookup"><span data-stu-id="d9afb-124">In hello **Traffic Manager** profile blade, click **Overview**.</span></span>
    3.  <span data-ttu-id="d9afb-125">hello **트래픽 관리자 프로필** 블레이드를 새로 만든된 트래픽 관리자 프로필의 hello DNS 이름을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9afb-125">hello **Traffic Manager profile** blade displays hello DNS name of your newly created Traffic Manager profile.</span></span> <span data-ttu-id="d9afb-126">이 끝점에 의해 모든 클라이언트 (예를 들어 이동 하 여 웹 브라우저를 사용 하 여 tooit) 라우팅된 tooget toohello 오른쪽 hello 라우팅 유형을 기준으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9afb-126">This can be used by any clients (for example,by navigating tooit using a web browser) tooget routed toohello right endpoint as determined by hello routing type.</span></span> <span data-ttu-id="d9afb-127">이 경우 모든 요청이 라운드 로빈 방식으로 각 끝점에 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9afb-127">In this case all requests are routed each endpoint in a round-robin fashion.</span></span>
6. <span data-ttu-id="d9afb-128">트래픽 관리자 프로필 작동 되 면 hello DNS 레코드에 권한 있는 DNS 서버 toopoint에 회사 도메인 이름 toohello 트래픽 관리자 도메인 이름을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9afb-128">Once your Traffic Manager profile is working, edit hello DNS record on your authoritative DNS server toopoint your company domain name toohello Traffic Manager domain name.</span></span>

![Traffic Manager를 사용한 가중치 적용 트래픽 라우팅 방법 구성][1]

## <a name="next-steps"></a><span data-ttu-id="d9afb-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d9afb-130">Next steps</span></span>

- <span data-ttu-id="d9afb-131">[우선 순위 트래픽 라우팅 방법](traffic-manager-configure-priority-routing-method.md)에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="d9afb-131">Learn about [priority traffic routing method](traffic-manager-configure-priority-routing-method.md).</span></span>
- <span data-ttu-id="d9afb-132">[성능 트래픽 라우팅 방법](traffic-manager-configure-performance-routing-method.md)에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="d9afb-132">Learn about [performance traffic routing method](traffic-manager-configure-performance-routing-method.md).</span></span>
- <span data-ttu-id="d9afb-133">[지리적 라우팅 방법](traffic-manager-configure-geographic-routing-method.md)에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="d9afb-133">Learn about [geographic routing method](traffic-manager-configure-geographic-routing-method.md).</span></span>
- <span data-ttu-id="d9afb-134">너무 방법에 대해 알아봅니다[트래픽 관리자 설정을 테스트](traffic-manager-testing-settings.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d9afb-134">Learn how too[test Traffic Manager settings](traffic-manager-testing-settings.md).</span></span>

<!--Image references-->
[1]: ./media/traffic-manager-weighted-routing-method/traffic-manager-weighted-routing-method.png
