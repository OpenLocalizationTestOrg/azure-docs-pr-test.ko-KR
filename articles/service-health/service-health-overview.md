---
title: "Azure Service Health 개요 | Microsoft Docs"
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
ms.openlocfilehash: 001dc1fa2a0fd7e132101944a87be3f8552d8738
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="azure-service-health"></a><span data-ttu-id="b4c41-103">Azure Service Health</span><span class="sxs-lookup"><span data-stu-id="b4c41-103">Azure Service Health</span></span>
<span data-ttu-id="b4c41-104">Azure Service Health는 Azure 서비스의 문제가 사용 중인 서비스에 영향을 줄 때 시기적절하고 개인 설정된 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c41-104">Azure Service Health provides timely and personalized information when problems in Azure services impact your services.</span></span>  <span data-ttu-id="b4c41-105">향후 계획된 유지 관리에 대해 준비하는 데도 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4c41-105">It also helps you prepare for upcoming planned maintenance.</span></span>

## <a name="service-health-events"></a><span data-ttu-id="b4c41-106">Service Health 이벤트</span><span class="sxs-lookup"><span data-stu-id="b4c41-106">Service Health Events</span></span>
<span data-ttu-id="b4c41-107">Service Health는 리소스에 영향을 줄 수 있는 다음과 같은 세 가지 유형의 상태 이벤트를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c41-107">Service Health tracks three types of health events that may impact your resources:</span></span>
1. <span data-ttu-id="b4c41-108">**서비스 문제** - 즉시 사용자에게 영향을 주는 Azure 서비스의 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="b4c41-108">**Service issues** - Problems in the Azure services that affect you right now.</span></span> 
2. <span data-ttu-id="b4c41-109">**계획된 유지 관리** - 나중에 서비스의 가용성에 영향을 줄 수 있는 예정된 유지 관리입니다.</span><span class="sxs-lookup"><span data-stu-id="b4c41-109">**Planned maintenance** - Upcoming maintenance that can affect the availability of your services in the future.</span></span>  
3. <span data-ttu-id="b4c41-110">**상태 자문** - 주의가 필요한 Azure 서비스의 변경 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="b4c41-110">**Health advisories** - Changes in Azure services that require your attention.</span></span> <span data-ttu-id="b4c41-111">Azure 기능이 사용되지 않거나 사용 할당량을 초과하는 경우를 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4c41-111">Examples include when Azure features are deprecated or if you exceed a usage quota.</span></span>

    ![Service Health 이벤트](./media/service-health-overview/azure-service-health-overview-7.png)

## <a name="get-started-with-service-health"></a><span data-ttu-id="b4c41-113">Service Health 시작</span><span class="sxs-lookup"><span data-stu-id="b4c41-113">Get started with Service Health</span></span>
<span data-ttu-id="b4c41-114">Service Health 대시보드를 시작하려면 포털 대시보드에서 Service Health 타일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c41-114">To launch your Service Health dashboard, select the Service Health tile on your portal dashboard.</span></span> <span data-ttu-id="b4c41-115">이전에 타일을 제거했거나 사용자 지정 대시보드를 사용 중인 경우 “추가 서비스”(대시보드의 왼쪽 아래)에서 Service Health 서비스를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c41-115">If you have previously removed the tile or you're using custom dashboard, search for Service Health service in "More services" (bottom left on your dashboard).</span></span>
<span data-ttu-id="b4c41-116">![Service Health 시작](./media/service-health-overview/azure-service-health-overview-1.png)</span><span class="sxs-lookup"><span data-stu-id="b4c41-116">![Get started with Service Health](./media/service-health-overview/azure-service-health-overview-1.png)</span></span>

## <a name="see-current-issues-which-impact-your-services"></a><span data-ttu-id="b4c41-117">서비스에 영향을 주는 현재 문제 확인</span><span class="sxs-lookup"><span data-stu-id="b4c41-117">See current issues which impact your services</span></span>
<span data-ttu-id="b4c41-118">**서비스 문제** 보기에는 리소스에 영향을 주고 있는 Azure 서비스의 진행 중인 문제가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4c41-118">The **Service issues** view shows any ongoing problems in Azure services that are impacting your resources.</span></span> <span data-ttu-id="b4c41-119">문제가 시작된 시점 및 영향을 받는 서비스 및 지역을 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4c41-119">You can understand when the issue began, and what services and regions are impacted.</span></span> <span data-ttu-id="b4c41-120">또한 최신 업데이트를 읽어 문제를 해결하기 위해 Azure에서 수행 중인 내용을 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4c41-120">You can also read the most recent update to understand what Azure is doing to resolve the issue.</span></span> 
<span data-ttu-id="b4c41-121">![서비스 문제 관리](./media/service-health-overview/azure-service-health-overview-2.png)</span><span class="sxs-lookup"><span data-stu-id="b4c41-121">![Manage service issue](./media/service-health-overview/azure-service-health-overview-2.png)</span></span>

<span data-ttu-id="b4c41-122">**잠재적 영향** 탭을 선택하여 소유한 리소스 중에서 문제의 영향을 받을 수 있는 특정 리소스 목록을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4c41-122">Choose the **Potential impact** tab to see the specific list of resources you own that might be impacted by the issue.</span></span> <span data-ttu-id="b4c41-123">이러한 리소스의 CSV 목록을 다운로드하여 팀과 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4c41-123">You can  download a CSV list of these resources to share with your team.</span></span>
<span data-ttu-id="b4c41-124">![서비스 문제 관리 - 영향](./media/service-health-overview/azure-service-health-overview-4.png)</span><span class="sxs-lookup"><span data-stu-id="b4c41-124">![Manage service issue - Impact](./media/service-health-overview/azure-service-health-overview-4.png)</span></span>

## <a name="get-links-and-downloadable-explanations"></a><span data-ttu-id="b4c41-125">링크 및 다운로드할 수 있는 설명 가져오기</span><span class="sxs-lookup"><span data-stu-id="b4c41-125">Get links and downloadable explanations</span></span> 
<span data-ttu-id="b4c41-126">문제 관리 시스템에서 사용할 문제의 링크를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4c41-126">You can get a link for the issue to use in your problem management system.</span></span> <span data-ttu-id="b4c41-127">PDF 및 경우에 따라 CSV 파일을 다운로드하여 Azure Portal에 액세스할 수 없는 사용자와 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4c41-127">You can download PDF and sometimes CSV files to share with people who don’t have access to the Azure portal.</span></span>   
![서비스 문제 관리 - 문제 관리](./media/service-health-overview/azure-service-health-overview-3.png)

## <a name="get-support-from-microsoft"></a><span data-ttu-id="b4c41-129">Microsoft에서 지원 받기</span><span class="sxs-lookup"><span data-stu-id="b4c41-129">Get support from Microsoft</span></span>
<span data-ttu-id="b4c41-130">문제가 해결된 후에도 리소스가 잘못된 상태로 남아 있는 경우 지원에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="b4c41-130">Contact support if your resource is left in a bad state even after the issue is resolved.</span></span>  <span data-ttu-id="b4c41-131">페이지 오른쪽에 있는 지원 링크를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="b4c41-131">Use the support links on the right of the page.</span></span>  

## <a name="pin-a-personalized-health-map-to-your-dashboard"></a><span data-ttu-id="b4c41-132">대시보드에 개인 설정된 상태 지도 고정</span><span class="sxs-lookup"><span data-stu-id="b4c41-132">Pin a personalized health map to your dashboard</span></span>
<span data-ttu-id="b4c41-133">Service Health를 필터링하여 업무상 중요한 구독, 지역 및 리소스 종류를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c41-133">Filter Service Health to show your business-critical subscriptions, regions, and resource types.</span></span> <span data-ttu-id="b4c41-134">필터를 저장하고 개인 설정된 상태 세계 지도를 포털 대시보드에 고정합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c41-134">Save the filter and pin a personalized health world map to your portal dashboard.</span></span> 
<span data-ttu-id="b4c41-135">![개인 설정된 상태 지도 필터링](./media/service-health-overview/azure-service-health-overview-6a.png)
![개인 설정된 상태 지도 고정](./media/service-health-overview/azure-service-health-overview-6b.png)</span><span class="sxs-lookup"><span data-stu-id="b4c41-135">![Filter personalized health map](./media/service-health-overview/azure-service-health-overview-6a.png)
![Pin a personalized health map](./media/service-health-overview/azure-service-health-overview-6b.png)</span></span>

## <a name="configure-service-health-alerts"></a><span data-ttu-id="b4c41-136">Service Health 경고 구성</span><span class="sxs-lookup"><span data-stu-id="b4c41-136">Configure Service Health alerts</span></span>
<span data-ttu-id="b4c41-137">Azure Service Health는 Azure Monitor와 통합되어 업무상 중요한 리소스가 영향을 받는 경우 메일, 문자 메시지 및 웹후크 알림을 통해 경고합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c41-137">Azure Service Health integrates with Azure Monitor to alert you via emails, text messages, and webhook notifications when your business-critical resources are impacted.</span></span> <span data-ttu-id="b4c41-138">적절한 Service Health 이벤트에 대한 활동 로그 경고를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c41-138">Set up an activity log alert for the appropriate Service Health event.</span></span> <span data-ttu-id="b4c41-139">작업 그룹을 사용하여 조직 내의 해당하는 사람들에게 해당 경고를 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c41-139">Route that alert to the appropriate people in your organization using Action Groups.</span></span> <span data-ttu-id="b4c41-140">자세한 내용은 [Service Health에 대한 경고 구성](../monitoring-and-diagnostics/monitoring-activity-log-alerts-on-service-notifications.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4c41-140">For more information, see [Configure Alerts for Service Health](../monitoring-and-diagnostics/monitoring-activity-log-alerts-on-service-notifications.md)</span></span>

# <a name="next-steps"></a><span data-ttu-id="b4c41-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b4c41-141">Next Steps</span></span>
<span data-ttu-id="b4c41-142">상태 문제 알림을 받도록 경고를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c41-142">Set up alerts so you are notified of health issues.</span></span> <span data-ttu-id="b4c41-143">자세한 내용은 [Service Health에 대한 경고 구성](../monitoring-and-diagnostics/monitoring-activity-log-alerts-on-service-notifications.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4c41-143">For more information, see [Configure Alerts for Service Health](../monitoring-and-diagnostics/monitoring-activity-log-alerts-on-service-notifications.md).</span></span> 