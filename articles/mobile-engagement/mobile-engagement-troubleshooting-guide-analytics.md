---
title: "Mobile Engagement 문제 해결 가이드-aaaAzure 분석"
description: "Azure Mobile Engagement에서 분석, 모니터링, 구분 및 대시보드 문제 해결"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 04a7020a-ad74-4491-be69-0bd574890029
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 69c6ff8f5c8540f8ba8b85b9ffec55acc59329fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-analytics-monitoring-segmentation-and-dashboard-issues"></a><span data-ttu-id="89e3a-103">분석, 모니터링, 구분 및 대시보드 문제에 대한 문제 해결 가이드</span><span class="sxs-lookup"><span data-stu-id="89e3a-103">Troubleshooting guide for Analytics, Monitoring, Segmentation, and Dashboard issues</span></span>
<span data-ttu-id="89e3a-104">hello 다음은 가능한 문제 Azure Mobile Engagement 응용 프로그램, 장치 및 사용자에 대 한 정보를 수집 하는 방법에서 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89e3a-104">hello following are possible issues you may encounter with how Azure Mobile Engagement gathers information about your applications, devices, and users.</span></span>

## <a name="missingdelayed-information"></a><span data-ttu-id="89e3a-105">정보 누락/지연</span><span class="sxs-lookup"><span data-stu-id="89e3a-105">Missing/Delayed information</span></span>
### <a name="issue"></a><span data-ttu-id="89e3a-106">문제</span><span class="sxs-lookup"><span data-stu-id="89e3a-106">Issue</span></span>
* <span data-ttu-id="89e3a-107">분석, 구분 또는 대시보드에서 정보 표시가 지연됩니다.</span><span class="sxs-lookup"><span data-stu-id="89e3a-107">Information is delayed in appearing in Analytics, Segmentation, or Dashboard.</span></span>
* <span data-ttu-id="89e3a-108">모니터링에서 정보가 누락됩니다.</span><span class="sxs-lookup"><span data-stu-id="89e3a-108">Information is missing from Monitoring.</span></span>
* <span data-ttu-id="89e3a-109">분석, 구분 또는 대시보드에서 정보가 누락됩니다.</span><span class="sxs-lookup"><span data-stu-id="89e3a-109">Information is missing from Analytics, Segmentation, or Dashboard.</span></span>
* <span data-ttu-id="89e3a-110">구분 제한에 도달합니다.</span><span class="sxs-lookup"><span data-stu-id="89e3a-110">Hitting segmentation limits.</span></span>

### <a name="causes"></a><span data-ttu-id="89e3a-111">원인</span><span class="sxs-lookup"><span data-stu-id="89e3a-111">Causes</span></span>
* <span data-ttu-id="89e3a-112">Hello 분석 API 모니터 API를 사용할 수 있습니다 되며 hello UI에에서 없는 데이터가 있는 경우 세그먼트 API toosee hello Api 통해 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89e3a-112">You can use hello Analytics API, Monitor API, and Segments API toosee if any data you are missing from hello UI is visible through hello APIs.</span></span>
* <span data-ttu-id="89e3a-113">앱에 Azure Mobile Engagement SDK hello 제대로 통합 되지 않은 경우 다음 됩니다 수 toosee 정보 분석, 분할, 모니터링, 또는 대시보드 hello에 합니다.</span><span class="sxs-lookup"><span data-stu-id="89e3a-113">If hello Azure Mobile Engagement SDK is not correctly integrated into your app then you won't be able toosee information in hello Analytics, Segmentation, Monitoring, or Dashboards.</span></span>
* <span data-ttu-id="89e3a-114">세그먼트는 작성하고 나면 변경할 수 없으며 "복제"(복사) 또는 "소멸"(삭제)만 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="89e3a-114">Segments can't be changed once they are created, segments can only be "cloned" (copied) or "destroyed" (deleted).</span></span> <span data-ttu-id="89e3a-115">세그먼트는 기준을 10개만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89e3a-115">Segments can only contain 10 criteria.</span></span>
* <span data-ttu-id="89e3a-116">모니터링에서 정보가 누락 hello 가장 좋은 방법은 tootest toosetup 테스트 장치는, 제거 및/또는 hello 테스트 장치의 hello 앱을 다시 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="89e3a-116">hello best way tootest missing information from monitoring is toosetup a test device, uninstall and/or reinstall hello app on hello test device.</span></span>
* <span data-ttu-id="89e3a-117">분석, 구분 또는 대시보드의 경우 정보는 24시간마다 갱신됩니다.</span><span class="sxs-lookup"><span data-stu-id="89e3a-117">Information is refreshed every 24 hours for Analytics, Segmentation, or Dashboards.</span></span>
* <span data-ttu-id="89e3a-118">Hello 세그먼트 이전 정보를 바탕으로 하는 경우에 생성 된 후 24 시간까지 새 세그먼트에 대 한 정보를 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89e3a-118">Information in new segments may not be displayed until 24 hours after they are created even if hello segment is based on previous information.</span></span>
* <span data-ttu-id="89e3a-119">Hello UI 사용 하 여 분석 데이터 필터링 나타납니다 hello 버전의 응용 프로그램에 관계 없이 이러한 종류의 모든 예 (예: 예를 들어 "크래시"를 이름으로 필터링하면 앱 버전 1과 2의 예제가 모두 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="89e3a-119">Filtering your analytics data in hello UI will show all examples of this type regardless of hello version of your app (e.g. "Crashes" filtered by name will show from version 1 and version 2 of your app).</span></span>
* <span data-ttu-id="89e3a-120">hello 분석에 대 한 시간 동안은 기반 hello 사용자의 장치 설정에서 hello 날짜 하므로 해당 휴대폰 잘못 설정 하는 hello 날짜에 사용자 표시 될 수 hello에 잘못 된 시간 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="89e3a-120">hello time period for Analytics is based on hello date from hello users' device settings, so a user whose phone has hello date incorrectly set could show up in hello wrong time period.</span></span>
* <span data-ttu-id="89e3a-121">푸시 hello 단추를 사용 하는 경우 데이터는 기록 되지 서버 쪽 너무 "test", 실제 푸시 캠페인에 대 한 데이터는 기록만 합니다.</span><span class="sxs-lookup"><span data-stu-id="89e3a-121">No server side data is logged when you use hello button too"test" pushes, data is only logged for real push campaigns.</span></span>

## <a name="cant-locate-items-in-ui"></a><span data-ttu-id="89e3a-122">UI에서 항목을 찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="89e3a-122">Can't locate items in UI</span></span>
### <a name="issue"></a><span data-ttu-id="89e3a-123">문제</span><span class="sxs-lookup"><span data-stu-id="89e3a-123">Issue</span></span>
* <span data-ttu-id="89e3a-124">특정 기본 제공 앱 또는 사용자 지정 앱의 정보 태그를 기준으로 세그먼트를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="89e3a-124">Can't create segments based on certain built in or custom app info tag criteria.</span></span>
* <span data-ttu-id="89e3a-125">분석, 모니터링 또는 대시보드에서 특정 기본 제공 앱 또는 사용자 지정 앱의 정보 태그 기준을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="89e3a-125">Can't find certain built in or custom app info tag criteria in Analytics, Monitoring, or Dashboards.</span></span>
* <span data-ttu-id="89e3a-126">Hello 데이터 분석, 모니터링, 분할 또는 대시보드를 해석할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="89e3a-126">Can't interpret hello data in Analytics, Monitoring, Segmentation, or Dashboards.</span></span>

### <a name="causes"></a><span data-ttu-id="89e3a-127">원인</span><span class="sxs-lookup"><span data-stu-id="89e3a-127">Causes</span></span>
* <span data-ttu-id="89e3a-128">일부 항목에 빌드되고 태그는만 밀어넣기 조건으로 사용할 수 있지만 수의 앱 정보 tooa 세그먼트를 추가 또는 분석, 모니터링, 또는 대시보드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="89e3a-128">Some built in items and app info tags are only available as push criteria but may not be added tooa segment or visible from Analytics, Monitoring, or Dashboard.</span></span> 
* <span data-ttu-id="89e3a-129">항목 및 수 없는 태그가 tooa 세그먼트를 추가 하는 응용 프로그램 정보에는 기본 제공, toosetup 목록이 각 캠페인 tooperform hello 동일한 세그먼트에 따라 대상 역할의 조건을 대상으로 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89e3a-129">For built in items and app info tags that can't be added tooa segment, you will need toosetup list of targeting criteria in each campaign tooperform hello same function as targeting based on a segment.</span></span>
* <span data-ttu-id="89e3a-130">Hello 상황에 맞는 메뉴에 대 한 자세한 도움말 hello Azure Mobile Engagement UI의 hello 분석, 모니터링, 분할 및 대시보드 섹션에서 참조 하 고 어떻게 tooinformation 합니다.</span><span class="sxs-lookup"><span data-stu-id="89e3a-130">See hello context menus in hello Analytics, Monitoring, Segmentation, and Dashboards sections of hello Azure Mobile Engagement UI for more help and how tooinformation.</span></span>

## <a name="crash-troubleshooting"></a><span data-ttu-id="89e3a-131">작동 중단 문제 해결</span><span class="sxs-lookup"><span data-stu-id="89e3a-131">Crash troubleshooting</span></span>
### <a name="issue"></a><span data-ttu-id="89e3a-132">문제</span><span class="sxs-lookup"><span data-stu-id="89e3a-132">Issue</span></span>
* <span data-ttu-id="89e3a-133">분석, 모니터링 또는 대시보드에서 응용 프로그램 작동 중단 현상이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="89e3a-133">Application Crashes appearing in Analytics, Monitoring, or Dashboard.</span></span>

### <a name="causes"></a><span data-ttu-id="89e3a-134">원인</span><span class="sxs-lookup"><span data-stu-id="89e3a-134">Causes</span></span>
* <span data-ttu-id="89e3a-135">tootroubleshoot 응용 프로그램이 크래시 되 분석, 모니터링, 또는 대시보드 시에 이전 버전의 hello SDK의 알려진된 문제에 대 한 있는지 toocheck hello 릴리스 정보를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="89e3a-135">tootroubleshoot Application Crashes seen in Analytics, Monitoring, or Dashboard make sure toocheck hello release notes for known issues with previous versions of hello SDK.</span></span>
* <span data-ttu-id="89e3a-136">toofurther 응용 프로그램 충돌 이벤트를 응용 프로그램이 설치를 사용 하 여 테스트 장치에서 수행할 및 hello Azure Mobile Engagement UI의 hello 모니터 "– 이벤트" 섹션에 장치 ID를 조회를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="89e3a-136">toofurther troubleshoot application crashes perform an event from a test device with your application installed and look up your device ID in hello “Monitor – Events” section of hello Azure Mobile Engagement UI.</span></span> <span data-ttu-id="89e3a-137">Hello 이벤트를 발생 시킨 응용 프로그램 toocrash 수행 하 고 hello hello Azure Mobile Engagement UI의 "모니터-충돌" 섹션에서에서 추가 정보를 조회 합니다.</span><span class="sxs-lookup"><span data-stu-id="89e3a-137">Then perform hello event that is causing your application toocrash and look up additional information in hello “Monitor – Crash” section of hello Azure Mobile Engagement UI.</span></span> 

