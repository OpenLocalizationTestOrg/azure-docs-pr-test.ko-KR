---
title: "aaaConfigure 성능 트래픽 라우팅 방법 Azure 트래픽 관리자를 사용 하 여 | Microsoft Docs"
description: "이 문서에서는 어떻게 tooconfigure 트래픽 관리자 tooroute 트래픽에만 toohello 끝점 대기 시간이 가장 짧은 설명"
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
ms.openlocfilehash: d0ccd4c9de411844c6f36068859265244f4aa52b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-performance-traffic-routing-method"></a><span data-ttu-id="c5170-103">Hello 성능 트래픽 라우팅 방법 구성</span><span class="sxs-lookup"><span data-stu-id="c5170-103">Configure hello performance traffic routing method</span></span>

<span data-ttu-id="c5170-104">hello 성능 트래픽 라우팅 방법을 hello 클라이언트의 네트워크에서 hello 가장 낮은 대기 시간으로 toodirect 트래픽 toohello 끝점을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5170-104">hello Performance traffic routing method allows you toodirect traffic toohello endpoint with hello lowest latency from hello client's network.</span></span> <span data-ttu-id="c5170-105">일반적으로 hello 가장 낮은 대기 시간으로 hello 데이터 센터는 지리적으로 거리가 가장 가까운 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5170-105">Typically, hello datacenter with hello lowest latency is hello closest in geographic distance.</span></span> <span data-ttu-id="c5170-106">이 트래픽 라우팅 방법은 네트워크 구성이나 로드의 실시간 변경 내용을 고려할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c5170-106">This traffic routing method cannot account for real-time changes in network configuration or load.</span></span>

##  <a name="tooconfigure-performance-routing-method"></a><span data-ttu-id="c5170-107">tooconfigure 성능 라우팅 방법</span><span class="sxs-lookup"><span data-stu-id="c5170-107">tooconfigure performance routing method</span></span>

1. <span data-ttu-id="c5170-108">Toohello 브라우저에서 로그인 [Azure 포털](http://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="c5170-108">From a browser, sign in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="c5170-109">아직 계정이 없는 경우 [1개월 무료 평가판](https://azure.microsoft.com/free/)을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5170-109">If you don’t already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free/).</span></span> 
2. <span data-ttu-id="c5170-110">Hello hello 포털 검색 창에서 검색할 **트래픽 관리자 프로필** tooconfigure hello에 대 한 라우팅 메서드를 원하는 hello 프로필 이름을 클릭 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5170-110">In hello portal’s search bar, search for hello **Traffic Manager profiles** and then click hello profile name that you want tooconfigure hello routing method for.</span></span>
3. <span data-ttu-id="c5170-111">Hello에 **트래픽 관리자 프로필** 블레이드를 둘 다 hello 클라우드 서비스를 구성에서 tooinclude 되도록 웹 사이트를 사용할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5170-111">In hello **Traffic Manager profile** blade, verify that both hello cloud services and websites that you want tooinclude in your configuration are present.</span></span>
4. <span data-ttu-id="c5170-112">Hello에 **설정** 섹션에서 클릭 **구성**, 및 hello **구성** 블레이드를 다음과 같이 완료:</span><span class="sxs-lookup"><span data-stu-id="c5170-112">In hello **Settings** section, click **Configuration**, and in hello **Configuration** blade, complete as follows:</span></span>
    1. <span data-ttu-id="c5170-113">**트래픽 라우팅 방법 설정**의 경우 **라우팅 방법**에서 **성능**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c5170-113">For **traffic routing method settings**, for **Routing method** select **Performance**.</span></span>
    2. <span data-ttu-id="c5170-114">집합 hello **끝점 모니터 설정** 다음과 같이이 프로필 내의 모든 모든 끝점에 대해 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5170-114">Set hello **Endpoint monitor settings** identical for all every endpoint within this profile as follows:</span></span>
        1. <span data-ttu-id="c5170-115">적절 한 선택 hello **프로토콜**, hello 지정 **포트** 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="c5170-115">Select hello appropriate **Protocol**, and specify hello **Port** number.</span></span> 
        2. <span data-ttu-id="c5170-116">**경로**에서 슬래시  */* 를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c5170-116">For **Path** type a forward slash */*.</span></span> <span data-ttu-id="c5170-117">toomonitor 끝점 경로 파일 이름을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5170-117">toomonitor endpoints, you must specify a path and filename.</span></span> <span data-ttu-id="c5170-118">A 슬래시 "/" hello 상대 경로 대 한 유효한 항목 및 hello이 파일은 hello 루트 디렉터리 (기본값)를 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5170-118">A forward slash "/" is a valid entry for hello relative path and implies that hello file is in hello root directory (default).</span></span>
        3. <span data-ttu-id="c5170-119">Hello hello 페이지의 위쪽에 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="c5170-119">At hello top of hello page, click **Save**.</span></span>
5.  <span data-ttu-id="c5170-120">다음과 같이 구성에서 hello 변경 내용 테스트:</span><span class="sxs-lookup"><span data-stu-id="c5170-120">Test hello changes in your configuration as follows:</span></span>
    1.  <span data-ttu-id="c5170-121">Hello 포털 검색 표시줄에 hello 트래픽 관리자 프로필 이름을 검색 하 고 표시 하는 hello hello 결과에 hello 트래픽 관리자 프로필을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5170-121">In hello portal’s search bar, search for hello Traffic Manager profile name and click hello Traffic Manager profile in hello results that hello displayed.</span></span>
    2.  <span data-ttu-id="c5170-122">Hello에 **트래픽 관리자** 블레이드 프로필을 클릭 하 여 **개요**합니다.</span><span class="sxs-lookup"><span data-stu-id="c5170-122">In hello **Traffic Manager** profile blade, click **Overview**.</span></span>
    3.  <span data-ttu-id="c5170-123">hello **트래픽 관리자 프로필** 블레이드를 새로 만든된 트래픽 관리자 프로필의 hello DNS 이름을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5170-123">hello **Traffic Manager profile** blade displays hello DNS name of your newly created Traffic Manager profile.</span></span> <span data-ttu-id="c5170-124">이 끝점에 의해 모든 클라이언트 (예를 들어 이동 하 여 웹 브라우저를 사용 하 여 tooit) 라우팅된 tooget toohello 오른쪽 hello 라우팅 유형을 기준으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5170-124">This can be used by any clients (for example, by navigating tooit using a web browser) tooget routed toohello right endpoint as determined by hello routing type.</span></span> <span data-ttu-id="c5170-125">이 경우 모든 요청은 hello 클라이언트의 네트워크에서 hello 가장 낮은 대기 시간으로 라우팅된 toohello 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="c5170-125">In this case all requests are routed toohello endpoint with hello lowest latency from hello client's network.</span></span>
6. <span data-ttu-id="c5170-126">트래픽 관리자 프로필 작동 되 면 hello DNS 레코드에 권한 있는 DNS 서버 toopoint에 회사 도메인 이름 toohello 트래픽 관리자 도메인 이름을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5170-126">Once your Traffic Manager profile is working, edit hello DNS record on your authoritative DNS server toopoint your company domain name toohello Traffic Manager domain name.</span></span>

![Traffic Manager를 사용한 성능 트래픽 라우팅 방법 구성][1]

## <a name="next-steps"></a><span data-ttu-id="c5170-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c5170-128">Next steps</span></span>

- <span data-ttu-id="c5170-129">[가중치 적용 트래픽 라우팅 방법](traffic-manager-configure-weighted-routing-method.md)에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="c5170-129">Learn about [weighted traffic routing method](traffic-manager-configure-weighted-routing-method.md).</span></span>
- <span data-ttu-id="c5170-130">[우선 순위 라우팅 방법](traffic-manager-configure-priority-routing-method.md)에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="c5170-130">Learn about [priority routing method](traffic-manager-configure-priority-routing-method.md).</span></span>
- <span data-ttu-id="c5170-131">[지리적 라우팅 방법](traffic-manager-configure-geographic-routing-method.md)에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="c5170-131">Learn about [geographic routing method](traffic-manager-configure-geographic-routing-method.md).</span></span>
- <span data-ttu-id="c5170-132">너무 방법에 대해 알아봅니다[트래픽 관리자 설정을 테스트](traffic-manager-testing-settings.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c5170-132">Learn how too[test Traffic Manager settings](traffic-manager-testing-settings.md).</span></span>

<!--Image references-->
[1]: ./media/traffic-manager-performance-routing-method/traffic-manager-performance-routing-method.png