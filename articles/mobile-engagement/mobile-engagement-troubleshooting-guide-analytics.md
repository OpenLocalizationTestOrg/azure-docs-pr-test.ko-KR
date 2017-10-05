---
title: "Azure Mobile Engagement 문제 해결 가이드 - 분석"
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
ms.openlocfilehash: e30c9ac0a8421ffcf4fc3e2548cfd7ac49701900
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-guide-for-analytics-monitoring-segmentation-and-dashboard-issues"></a><span data-ttu-id="0bf1f-103">분석, 모니터링, 구분 및 대시보드 문제에 대한 문제 해결 가이드</span><span class="sxs-lookup"><span data-stu-id="0bf1f-103">Troubleshooting guide for Analytics, Monitoring, Segmentation, and Dashboard issues</span></span>
<span data-ttu-id="0bf1f-104">다음은 Azure Mobile Engagement에서 응용 프로그램, 장치 및 사용자에 대한 정보를 수집하는 방법과 관련해서 발생할 수 있는 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="0bf1f-104">The following are possible issues you may encounter with how Azure Mobile Engagement gathers information about your applications, devices, and users.</span></span>

## <a name="missingdelayed-information"></a><span data-ttu-id="0bf1f-105">정보 누락/지연</span><span class="sxs-lookup"><span data-stu-id="0bf1f-105">Missing/Delayed information</span></span>
### <a name="issue"></a><span data-ttu-id="0bf1f-106">문제</span><span class="sxs-lookup"><span data-stu-id="0bf1f-106">Issue</span></span>
* <span data-ttu-id="0bf1f-107">분석, 구분 또는 대시보드에서 정보 표시가 지연됩니다.</span><span class="sxs-lookup"><span data-stu-id="0bf1f-107">Information is delayed in appearing in Analytics, Segmentation, or Dashboard.</span></span>
* <span data-ttu-id="0bf1f-108">모니터링에서 정보가 누락됩니다.</span><span class="sxs-lookup"><span data-stu-id="0bf1f-108">Information is missing from Monitoring.</span></span>
* <span data-ttu-id="0bf1f-109">분석, 구분 또는 대시보드에서 정보가 누락됩니다.</span><span class="sxs-lookup"><span data-stu-id="0bf1f-109">Information is missing from Analytics, Segmentation, or Dashboard.</span></span>
* <span data-ttu-id="0bf1f-110">구분 제한에 도달합니다.</span><span class="sxs-lookup"><span data-stu-id="0bf1f-110">Hitting segmentation limits.</span></span>

### <a name="causes"></a><span data-ttu-id="0bf1f-111">원인</span><span class="sxs-lookup"><span data-stu-id="0bf1f-111">Causes</span></span>
* <span data-ttu-id="0bf1f-112">분석 API, 모니터 API 및 세그먼트 API를 사용하여 UI에서 누락된 데이터가 API에서는 표시되는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bf1f-112">You can use the Analytics API, Monitor API, and Segments API to see if any data you are missing from the UI is visible through the APIs.</span></span>
* <span data-ttu-id="0bf1f-113">Azure Mobile Engagement SDK가 앱에 올바르게 통합되어 있지 않으면 분석, 구분, 모니터링 또는 대시보드에서 정보를 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0bf1f-113">If the Azure Mobile Engagement SDK is not correctly integrated into your app then you won't be able to see information in the Analytics, Segmentation, Monitoring, or Dashboards.</span></span>
* <span data-ttu-id="0bf1f-114">세그먼트는 작성하고 나면 변경할 수 없으며 "복제"(복사) 또는 "소멸"(삭제)만 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="0bf1f-114">Segments can't be changed once they are created, segments can only be "cloned" (copied) or "destroyed" (deleted).</span></span> <span data-ttu-id="0bf1f-115">세그먼트는 기준을 10개만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bf1f-115">Segments can only contain 10 criteria.</span></span>
* <span data-ttu-id="0bf1f-116">모니터링에서 정보가 누락되었는지 테스트하는 가장 효율적인 방법은 테스트 장치를 설정한 다음 해당 장치에서 앱을 제거 및/또는 다시 설치하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0bf1f-116">The best way to test missing information from monitoring is to setup a test device, uninstall and/or reinstall the app on the test device.</span></span>
* <span data-ttu-id="0bf1f-117">분석, 구분 또는 대시보드의 경우 정보는 24시간마다 갱신됩니다.</span><span class="sxs-lookup"><span data-stu-id="0bf1f-117">Information is refreshed every 24 hours for Analytics, Segmentation, or Dashboards.</span></span>
* <span data-ttu-id="0bf1f-118">세그먼트가 이전 정보를 기준으로 하더라도 새 세그먼트의 정보는 작성된 후 24시간 동안 표시되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bf1f-118">Information in new segments may not be displayed until 24 hours after they are created even if the segment is based on previous information.</span></span>
* <span data-ttu-id="0bf1f-119">UI에서 분석 데이터를 필터링하면 앱 버전에 관계없이 해당 형식의 모든 예제가 표시됩니다. 예를 들어 "크래시"를 이름으로 필터링하면 앱 버전 1과 2의 예제가 모두 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0bf1f-119">Filtering your analytics data in the UI will show all examples of this type regardless of the version of your app (e.g. "Crashes" filtered by name will show from version 1 and version 2 of your app).</span></span>
* <span data-ttu-id="0bf1f-120">분석 기간은 사용자 장치 설정의 날짜를 기준으로 하므로 휴대폰에 날짜가 잘못 설정된 사용자의 경우 잘못된 기간의 데이터가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0bf1f-120">The time period for Analytics is based on the date from the users' device settings, so a user whose phone has the date incorrectly set could show up in the wrong time period.</span></span>
* <span data-ttu-id="0bf1f-121">푸시를 "테스트"하는 단추를 사용할 때는 서버 쪽 데이터가 기록되지 않으며 실제 푸시 캠페인에 대해서만 데이터기 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="0bf1f-121">No server side data is logged when you use the button to "test" pushes, data is only logged for real push campaigns.</span></span>

## <a name="cant-locate-items-in-ui"></a><span data-ttu-id="0bf1f-122">UI에서 항목을 찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="0bf1f-122">Can't locate items in UI</span></span>
### <a name="issue"></a><span data-ttu-id="0bf1f-123">문제</span><span class="sxs-lookup"><span data-stu-id="0bf1f-123">Issue</span></span>
* <span data-ttu-id="0bf1f-124">특정 기본 제공 앱 또는 사용자 지정 앱의 정보 태그를 기준으로 세그먼트를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0bf1f-124">Can't create segments based on certain built in or custom app info tag criteria.</span></span>
* <span data-ttu-id="0bf1f-125">분석, 모니터링 또는 대시보드에서 특정 기본 제공 앱 또는 사용자 지정 앱의 정보 태그 기준을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0bf1f-125">Can't find certain built in or custom app info tag criteria in Analytics, Monitoring, or Dashboards.</span></span>
* <span data-ttu-id="0bf1f-126">분석, 모니터링, 구분 또는 대시보드에서 데이터를 해석할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0bf1f-126">Can't interpret the data in Analytics, Monitoring, Segmentation, or Dashboards.</span></span>

### <a name="causes"></a><span data-ttu-id="0bf1f-127">원인</span><span class="sxs-lookup"><span data-stu-id="0bf1f-127">Causes</span></span>
* <span data-ttu-id="0bf1f-128">일부 기본 제공 항목 및 앱 정보 태그는 푸시 기준으로만 제공되며 분석, 모니터링 또는 대시보드에서 보거나 세그먼트에 추가하지는 못할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bf1f-128">Some built in items and app info tags are only available as push criteria but may not be added to a segment or visible from Analytics, Monitoring, or Dashboard.</span></span> 
* <span data-ttu-id="0bf1f-129">세그먼트에 추가할 수 없는 기본 제공 항목 및 앱 정보 태그의 경우 세그먼트 기준 대상 지정과 같은 기능을 수행하도록 각 캠페인에서 대상 기준 목록을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bf1f-129">For built in items and app info tags that can't be added to a segment, you will need to setup list of targeting criteria in each campaign to perform the same function as targeting based on a segment.</span></span>
* <span data-ttu-id="0bf1f-130">자세한 도움말과 방법 정보는 Azure Mobile Engagement UI에서 분석, 모니터링, 구분 또는 대시보드 섹션의 상황에 맞는 메뉴를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0bf1f-130">See the context menus in the Analytics, Monitoring, Segmentation, and Dashboards sections of the Azure Mobile Engagement UI for more help and how to information.</span></span>

## <a name="crash-troubleshooting"></a><span data-ttu-id="0bf1f-131">작동 중단 문제 해결</span><span class="sxs-lookup"><span data-stu-id="0bf1f-131">Crash troubleshooting</span></span>
### <a name="issue"></a><span data-ttu-id="0bf1f-132">문제</span><span class="sxs-lookup"><span data-stu-id="0bf1f-132">Issue</span></span>
* <span data-ttu-id="0bf1f-133">분석, 모니터링 또는 대시보드에서 응용 프로그램 작동 중단 현상이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0bf1f-133">Application Crashes appearing in Analytics, Monitoring, or Dashboard.</span></span>

### <a name="causes"></a><span data-ttu-id="0bf1f-134">원인</span><span class="sxs-lookup"><span data-stu-id="0bf1f-134">Causes</span></span>
* <span data-ttu-id="0bf1f-135">분석, 모니터링 또는 대시보드에서 나타나는 응용 프로그램 작동 중단 문제를 해결하려면 릴리스 정보에서 이전 버전 SDK의 알려진 문제를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="0bf1f-135">To troubleshoot Application Crashes seen in Analytics, Monitoring, or Dashboard make sure to check the release notes for known issues with previous versions of the SDK.</span></span>
* <span data-ttu-id="0bf1f-136">응용 프로그램 작동 중단 문제를 추가로 해결하려면 응용 프로그램이 설치된 테스트 장치에서 이벤트를 수행한 다음 Azure Mobile Engagement UI의 "모니터 - 이벤트" 섹션에서 장치 ID를 조회합니다.</span><span class="sxs-lookup"><span data-stu-id="0bf1f-136">To further troubleshoot application crashes perform an event from a test device with your application installed and look up your device ID in the “Monitor – Events” section of the Azure Mobile Engagement UI.</span></span> <span data-ttu-id="0bf1f-137">그런 다음 응용 프로그램 작동 중단의 원인이 되는 이벤트를 수행하여 Azure Mobile Engagement UI의 "모니터 - 이벤트" 섹션에서 추가 정보를 조회합니다.</span><span class="sxs-lookup"><span data-stu-id="0bf1f-137">Then perform the event that is causing your application to crash and look up additional information in the “Monitor – Crash” section of the Azure Mobile Engagement UI.</span></span> 

