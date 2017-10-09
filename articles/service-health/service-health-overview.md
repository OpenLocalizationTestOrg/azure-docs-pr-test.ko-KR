---
title: "aaaAzure 서비스 상태 개요 | Microsoft Docs"
description: "Azure 앱이 현재 및 향후 Azure 서비스 문제 및 유지 관리에 의해 어떤 영향을 받는지에 대한 개인 설정된 정보입니다."
services: Resource health
documentationcenter: 
author: rboucher
manager: 
editor: 
ms.assetid: 
ms.service: service-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 07/07/2017
ms.author: robb
ms.openlocfilehash: 2b536ee2f19757d4f2baf5529866c3d159a4670c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-health"></a><span data-ttu-id="b1881-103">Azure Service Health</span><span class="sxs-lookup"><span data-stu-id="b1881-103">Azure Service Health</span></span>
<span data-ttu-id="b1881-104">Azure Service Health는 Azure 서비스의 문제가 사용 중인 서비스에 영향을 줄 때 시기적절하고 개인 설정된 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b1881-104">Azure Service Health provides timely and personalized information when problems in Azure services impact your services.</span></span>  <span data-ttu-id="b1881-105">향후 계획된 유지 관리에 대해 준비하는 데도 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1881-105">It also helps you prepare for upcoming planned maintenance.</span></span>

## <a name="service-health-events"></a><span data-ttu-id="b1881-106">Service Health 이벤트</span><span class="sxs-lookup"><span data-stu-id="b1881-106">Service Health Events</span></span>
<span data-ttu-id="b1881-107">Service Health는 리소스에 영향을 줄 수 있는 다음과 같은 세 가지 유형의 상태 이벤트를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="b1881-107">Service Health tracks three types of health events that may impact your resources:</span></span>
1. <span data-ttu-id="b1881-108">**서비스 문제** -문제 hello 지금 바로 영향을 주는 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="b1881-108">**Service issues** - Problems in hello Azure services that affect you right now.</span></span> 
2. <span data-ttu-id="b1881-109">**계획 된 유지 관리** -hello 나중에 서비스의 hello 가용성에 영향을 줄 수 있는 향후 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1881-109">**Planned maintenance** - Upcoming maintenance that can affect hello availability of your services in hello future.</span></span>  
3. <span data-ttu-id="b1881-110">**상태 자문** - 주의가 필요한 Azure 서비스의 변경 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="b1881-110">**Health advisories** - Changes in Azure services that require your attention.</span></span> <span data-ttu-id="b1881-111">Azure 기능이 사용되지 않거나 사용 할당량을 초과하는 경우를 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1881-111">Examples include when Azure features are deprecated or if you exceed a usage quota.</span></span>

    ![Service Health 이벤트](./media/service-health-overview/azure-service-health-overview-7.png)

## <a name="get-started-with-service-health"></a><span data-ttu-id="b1881-113">Service Health 시작</span><span class="sxs-lookup"><span data-stu-id="b1881-113">Get started with Service Health</span></span>
<span data-ttu-id="b1881-114">toolaunch 서비스 상태 대시보드를 선택 hello 서비스 상태 대시보드에서 타일을 사용자 포털.</span><span class="sxs-lookup"><span data-stu-id="b1881-114">toolaunch your Service Health dashboard, select hello Service Health tile on your portal dashboard.</span></span> <span data-ttu-id="b1881-115">이전에 제거한 hello 타일 또는 사용자 지정 대시보드를 사용 하는 경우에 "더 많은 서비스" 서비스 상태 서비스에 대 한 검색 (동영상이 대시보드에서 왼쪽 아래).</span><span class="sxs-lookup"><span data-stu-id="b1881-115">If you have previously removed hello tile or you're using custom dashboard, search for Service Health service in "More services" (bottom left on your dashboard).</span></span>
<span data-ttu-id="b1881-116">![Service Health 시작](./media/service-health-overview/azure-service-health-overview-1.png)</span><span class="sxs-lookup"><span data-stu-id="b1881-116">![Get started with Service Health](./media/service-health-overview/azure-service-health-overview-1.png)</span></span>

## <a name="see-current-issues-which-impact-your-services"></a><span data-ttu-id="b1881-117">서비스에 영향을 주는 현재 문제 확인</span><span class="sxs-lookup"><span data-stu-id="b1881-117">See current issues which impact your services</span></span>
<span data-ttu-id="b1881-118">hello **서비스 문제** 보기 리소스에 영향을 주지는 Azure 서비스에서 진행 중인 문제를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1881-118">hello **Service issues** view shows any ongoing problems in Azure services that are impacting your resources.</span></span> <span data-ttu-id="b1881-119">Hello 문제 시작 되었을 때와 서비스 및 영역 영향을 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1881-119">You can understand when hello issue began, and what services and regions are impacted.</span></span> <span data-ttu-id="b1881-120">읽을 수 있습니다 hello 가장 최근의 업데이트 toounderstand 어떤 Azure tooresolve hello 문제를 수행 하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="b1881-120">You can also read hello most recent update toounderstand what Azure is doing tooresolve hello issue.</span></span> 
<span data-ttu-id="b1881-121">![서비스 문제 관리](./media/service-health-overview/azure-service-health-overview-2.png)</span><span class="sxs-lookup"><span data-stu-id="b1881-121">![Manage service issue](./media/service-health-overview/azure-service-health-overview-2.png)</span></span>

<span data-ttu-id="b1881-122">Hello 선택 **잠재적인 영향** 탭 toosee hello 특정 리소스 목록을 소유 하는 hello 문제의 영향을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1881-122">Choose hello **Potential impact** tab toosee hello specific list of resources you own that might be impacted by hello issue.</span></span> <span data-ttu-id="b1881-123">팀과 함께 이러한 리소스 tooshare CSV 목록이 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1881-123">You can  download a CSV list of these resources tooshare with your team.</span></span>
<span data-ttu-id="b1881-124">![서비스 문제 관리 - 영향](./media/service-health-overview/azure-service-health-overview-4.png)</span><span class="sxs-lookup"><span data-stu-id="b1881-124">![Manage service issue - Impact](./media/service-health-overview/azure-service-health-overview-4.png)</span></span>

## <a name="get-links-and-downloadable-explanations"></a><span data-ttu-id="b1881-125">링크 및 다운로드할 수 있는 설명 가져오기</span><span class="sxs-lookup"><span data-stu-id="b1881-125">Get links and downloadable explanations</span></span> 
<span data-ttu-id="b1881-126">문제 관리 시스템에 문제가 toouse hello에 대 한 링크를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1881-126">You can get a link for hello issue toouse in your problem management system.</span></span> <span data-ttu-id="b1881-127">PDF 및 경우에 따라 CSV 파일 tooshare 액세스 toohello Azure 포털에 없는 사용자를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1881-127">You can download PDF and sometimes CSV files tooshare with people who don’t have access toohello Azure portal.</span></span>   
![서비스 문제 관리 - 문제 관리](./media/service-health-overview/azure-service-health-overview-3.png)

## <a name="get-support-from-microsoft"></a><span data-ttu-id="b1881-129">Microsoft에서 지원 받기</span><span class="sxs-lookup"><span data-stu-id="b1881-129">Get support from Microsoft</span></span>
<span data-ttu-id="b1881-130">리소스는 잘못 된 상태로 남아 hello 해결 한 후에 지원을 문의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="b1881-130">Contact support if your resource is left in a bad state even after hello issue is resolved.</span></span>  <span data-ttu-id="b1881-131">Hello 지원 링크를 사용 하 여 hello hello 페이지의 오른쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1881-131">Use hello support links on hello right of hello page.</span></span>  

## <a name="pin-a-personalized-health-map-tooyour-dashboard"></a><span data-ttu-id="b1881-132">개인 설정 된 상태 맵 tooyour 대시보드 고정</span><span class="sxs-lookup"><span data-stu-id="b1881-132">Pin a personalized health map tooyour dashboard</span></span>
<span data-ttu-id="b1881-133">비즈니스에 중요 한 구독, 지역 및 리소스 종류에는 서비스 상태 tooshow를 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1881-133">Filter Service Health tooshow your business-critical subscriptions, regions, and resource types.</span></span> <span data-ttu-id="b1881-134">Hello 필터 및 개인 설정 된 상태 세계 지도 tooyour 포털 대시보드 pin를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1881-134">Save hello filter and pin a personalized health world map tooyour portal dashboard.</span></span> 
<span data-ttu-id="b1881-135">![개인 설정된 상태 지도 필터링](./media/service-health-overview/azure-service-health-overview-6a.png)
![개인 설정된 상태 지도 고정](./media/service-health-overview/azure-service-health-overview-6b.png)</span><span class="sxs-lookup"><span data-stu-id="b1881-135">![Filter personalized health map](./media/service-health-overview/azure-service-health-overview-6a.png)
![Pin a personalized health map](./media/service-health-overview/azure-service-health-overview-6b.png)</span></span>

## <a name="configure-service-health-alerts"></a><span data-ttu-id="b1881-136">Service Health 경고 구성</span><span class="sxs-lookup"><span data-stu-id="b1881-136">Configure Service Health alerts</span></span>
<span data-ttu-id="b1881-137">Azure 서비스 상태와 통합 되어 Azure 모니터 tooalert 하면 전자 메일, 문자 메시지 및 webhook 알림을 통해 비즈니스에 중요 한 리소스의 영향을 받는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="b1881-137">Azure Service Health integrates with Azure Monitor tooalert you via emails, text messages, and webhook notifications when your business-critical resources are impacted.</span></span> <span data-ttu-id="b1881-138">Hello 적절 한 서비스 상태 이벤트에 대 한 활동 로그 경고를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1881-138">Set up an activity log alert for hello appropriate Service Health event.</span></span> <span data-ttu-id="b1881-139">동작 그룹을 사용 하 여 조직에 적절 한 사람이 toohello 경고는 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="b1881-139">Route that alert toohello appropriate people in your organization using Action Groups.</span></span> <span data-ttu-id="b1881-140">자세한 내용은 [Service Health에 대한 경고 구성](../monitoring-and-diagnostics/monitoring-activity-log-alerts-on-service-notifications.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b1881-140">For more information, see [Configure Alerts for Service Health](../monitoring-and-diagnostics/monitoring-activity-log-alerts-on-service-notifications.md)</span></span>

# <a name="next-steps"></a><span data-ttu-id="b1881-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b1881-141">Next Steps</span></span>
<span data-ttu-id="b1881-142">상태 문제 알림을 받도록 경고를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b1881-142">Set up alerts so you are notified of health issues.</span></span> <span data-ttu-id="b1881-143">자세한 내용은 [Service Health에 대한 경고 구성](../monitoring-and-diagnostics/monitoring-activity-log-alerts-on-service-notifications.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b1881-143">For more information, see [Configure Alerts for Service Health](../monitoring-and-diagnostics/monitoring-activity-log-alerts-on-service-notifications.md).</span></span> 