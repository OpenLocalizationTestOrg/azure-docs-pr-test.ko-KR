---
title: "서비스 맵 솔루션 자가 진행식 데모 | Microsoft Docs"
description: "서비스 맵은 Windows 및 Linux 시스템에서 응용 프로그램 구성 요소를 자동으로 검색하여 서비스 간 통신을 매핑하는 OMS(Operations Management Suite)의 솔루션입니다.  서비스 맵을 사용하여 웹 응용 프로그램에서 시뮬레이션된 문제를 식별하고 진단하는 방법을 설명하는 자가 진행식 데모입니다."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 9dc437b9-e83c-45da-917c-cb4f4d8d6333
ms.service: operations-management-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: bwren
ms.openlocfilehash: c3548d24c74f8ad865b22d6af3490d0b5cc77a84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="operations-management-suite-oms-self-paced-demo---service-map"></a><span data-ttu-id="931e5-104">OMS(Operations Management Suite) 자가 진행식 데모 - 서비스 맵</span><span class="sxs-lookup"><span data-stu-id="931e5-104">Operations Management Suite (OMS) self paced demo - Service Map</span></span>
<span data-ttu-id="931e5-105">OMS(Operations Management Suite)에서 [서비스 맵 솔루션](operations-management-suite-service-map.md)을 사용하여 웹 응용 프로그램에서 시뮬레이션된 문제를 식별하고 진단하는 방법을 설명하는 자가 진행식 데모입니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-105">This is a self paced demo that walks through using the [Service Map solution](operations-management-suite-service-map.md) in Operations Management Suite (OMS) to identify and diagnose a simulated problem in a web application.</span></span>  <span data-ttu-id="931e5-106">서비스 맵은 Windows 및 Linux 시스템에서 응용 프로그램 구성 요소를 자동으로 검색하고 서비스 간 통신을 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-106">Service Map automatically discovers application components on Windows and Linux systems and maps the communication between services.</span></span>  <span data-ttu-id="931e5-107">또한 다른 OMS 서비스에서 수집된 데이터를 통합하여 성능을 분석하고 문제를 식별하는 데 도움을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-107">It also consolidates data collected by other OMS services to assist you in analyzing performance and identifying issues.</span></span>  <span data-ttu-id="931e5-108">또한 [Log Analytics에서 로그 검색](../log-analytics/log-analytics-log-searches.md)을 사용하여 근본적인 문제를 식별하기 위해 수집된 데이터를 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-108">You'll also use [log searches in Log Analytics](../log-analytics/log-analytics-log-searches.md) to drill down on collected data in order to identify the root problem.</span></span>


## <a name="scenario-description"></a><span data-ttu-id="931e5-109">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="931e5-109">Scenario description</span></span>
<span data-ttu-id="931e5-110">방금 ACME 고객 포털 응용 프로그램에 성능 문제가 있다는 알림을 받았습니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-110">You've just received a notification that the ACME Customer Portal application is having performance issues.</span></span>  <span data-ttu-id="931e5-111">유일한 정보는 이러한 문제가 오늘 오전 4시(PST) 정도에 발생했다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-111">The only information that you have is that these issues started about 4:00 am PST today.</span></span>  <span data-ttu-id="931e5-112">웹 서버 집합이 아닌 포털이 종속된 모든 구성 요소를 전적으로 확신할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-112">You aren't entirely sure of all the components that the portal is dependent on other than a set of web servers.</span></span>  

## <a name="components-and-features-used"></a><span data-ttu-id="931e5-113">사용된 구성 요소 및 기능</span><span class="sxs-lookup"><span data-stu-id="931e5-113">Components and features used</span></span>
- [<span data-ttu-id="931e5-114">서비스 맵 솔루션</span><span class="sxs-lookup"><span data-stu-id="931e5-114">Service Map solution</span></span>](operations-management-suite-service-map.md)
- [<span data-ttu-id="931e5-115">Log Analytics 로그 검색</span><span class="sxs-lookup"><span data-stu-id="931e5-115">Log Analytics log searches</span></span>](../log-analytics/log-analytics-log-searches.md)


## <a name="walk-through"></a><span data-ttu-id="931e5-116">방법 설명</span><span class="sxs-lookup"><span data-stu-id="931e5-116">Walk through</span></span>

### <a name="1-connect-to-the-oms-experience-center"></a><span data-ttu-id="931e5-117">1. OMS 환경 센터에 연결</span><span class="sxs-lookup"><span data-stu-id="931e5-117">1. Connect to the OMS Experience Center</span></span>
<span data-ttu-id="931e5-118">이 연습은 샘플 데이터에서 완벽한 OMS 환경을 제공하는 [Operations Management Suite 환경 센터](https://experience.mms.microsoft.com/)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-118">This walk through uses the [Operations Management Suite Experience Center](https://experience.mms.microsoft.com/) which provides a complete OMS environment with sample data.</span></span> <span data-ttu-id="931e5-119">이 링크를 따라 시작하고 정보를 입력한 다음 **Insight and Analytics** 시나리오를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-119">Start by following this link, provide your information and then select the **Insight and Analytics** scenario.</span></span>


### <a name="2-start-service-map"></a><span data-ttu-id="931e5-120">2. 서비스 맵 시작</span><span class="sxs-lookup"><span data-stu-id="931e5-120">2. Start Service Map</span></span>
<span data-ttu-id="931e5-121">**서비스 맵** 타일을 클릭하여 서비스 맵 솔루션을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-121">Start the Service Map solution by clicking on the **Service Map** tile.</span></span>

![서비스 맵 타일](media/operations-management-suite-walkthrough-servicemap/tile.png)

<span data-ttu-id="931e5-123">서비스 맵 콘솔이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-123">The Service Map console is displayed.</span></span>  <span data-ttu-id="931e5-124">왼쪽 창에는 서비스 맵 에이전트가 설치된 환경에 있는 컴퓨터 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-124">In the left pane is a list of computers in your environment with the Service Map agent installed.</span></span>  <span data-ttu-id="931e5-125">이 목록에서 보려는 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-125">You'll select the computer that you want to view from this list.</span></span>

![컴퓨터 목록](media/operations-management-suite-walkthrough-servicemap/computer-list.png)


### <a name="3-view-computer"></a><span data-ttu-id="931e5-127">3. 컴퓨터 보기</span><span class="sxs-lookup"><span data-stu-id="931e5-127">3. View computer</span></span>
<span data-ttu-id="931e5-128">이미 알고 있는 AcmeWFE001 및 AcmeWFE002라는 웹 서버에서 시작하는 것이 적절합니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-128">We know that the web servers are called AcmeWFE001 and AcmeWFE002, so this seems like a reasonable place to start.</span></span>  <span data-ttu-id="931e5-129">**AcmeWFE001**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-129">Click on **AcmeWFE001**.</span></span>  <span data-ttu-id="931e5-130">AcmeWFE001의 맵 및 모든 해당 종속성을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-130">This displays the map for AcmeWFE001 and all of its dependencies.</span></span>  <span data-ttu-id="931e5-131">선택한 컴퓨터에서 실행 중인 프로세스 및 통신하는 외부 서비스를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-131">You can see which processes are running on the selected computer and which external services they communicate with.</span></span>

![웹 서버](media/operations-management-suite-walkthrough-servicemap/web-server.png)

<span data-ttu-id="931e5-133">웹 응용 프로그램의 성능에 관심이 있으므로 **AcmeAppPool(IIS 앱 풀)** 프로세스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-133">We're concerned about the performance of our web application so click on the **AcmeAppPool (IIS App Pool)** process.</span></span>  <span data-ttu-id="931e5-134">이 프로세스의 세부 정보를 표시하고 해당 종속성을 강조 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-134">This displays the details for this process and highlights its dependencies.</span></span>  

![앱 풀](media/operations-management-suite-walkthrough-servicemap/app-pool.png)


### <a name="4-change-time-window"></a><span data-ttu-id="931e5-136">4. 기간 변경</span><span class="sxs-lookup"><span data-stu-id="931e5-136">4. Change time window</span></span>

<span data-ttu-id="931e5-137">문제가 오전 4시에 발생했다면 당시에 상황이 어땠는지 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-137">We heard that the problem started at 4:00 AM so let's have a look at what was happening at that time.</span></span> <span data-ttu-id="931e5-138">**시간 범위**를 클릭하고 20분의 기간을 두고 오전 4시(PST)로 시간을 변경(현재 날짜를 유지하고 현지 표준 시간대 조정)합니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-138">Click on **Time Range** and change the time to 4:00 AM PST (keep the current date and adjust for your local time zone) with a duration of 20 minutes.</span></span>

![시간 선택](./media/operations-management-suite-walkthrough-servicemap/time-picker.png)


### <a name="5-view-alert"></a><span data-ttu-id="931e5-140">5. 경고 보기</span><span class="sxs-lookup"><span data-stu-id="931e5-140">5. View alert</span></span>

<span data-ttu-id="931e5-141">이제 **acmetomcat** 종속성에 경고가 표시되면 잠재적인 문제가 있다는 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-141">We now see that the **acmetomcat** dependency has an alert displayed, so that's our potential problem.</span></span>  <span data-ttu-id="931e5-142">**acmetomcat**에서 경고 아이콘을 클릭하여 경고에 대한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-142">Click on the alert icon in **acmetomcat** to show the details for the alert.</span></span>  <span data-ttu-id="931e5-143">여기서 중요한 CPU 사용률을 확인하고 자세한 내용을 보기 위해 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-143">We can see that we have critical CPU utilization and can expand it for more detail.</span></span>  <span data-ttu-id="931e5-144">이 때문에 성능이 저하될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-144">This is probably what's causing our slow performance.</span></span> 

![경고](./media/operations-management-suite-walkthrough-servicemap/alert.png)


### <a name="6-view-performance"></a><span data-ttu-id="931e5-146">6. 성능 보기</span><span class="sxs-lookup"><span data-stu-id="931e5-146">6. View performance</span></span>

<span data-ttu-id="931e5-147">**acmetomcat**을 자세히 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-147">Let's have a closer look at **acmetomcat**.</span></span>  <span data-ttu-id="931e5-148">**acmetomcat**의 오른쪽 상단을 클릭하고 **서버 맵 로드**를 선택하여 이 컴퓨터의 세부 데이터 및 종속성을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-148">Click in the top right of **acmetomcat** and select **Load Server Map** to show the detail and dependencies for this machine.</span></span> <span data-ttu-id="931e5-149">의문점을 확인하기 위해 해당 성능 카운터를 좀 더 살펴볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-149">We can then look a bit more into those performance counters to verify our suspicion.</span></span>  <span data-ttu-id="931e5-150">**성능** 탭을 선택하여 시간 범위 동안 [Log Analytics에서 수집된 성능 카운터](../log-analytics/log-analytics-data-sources-performance-counters.md)를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-150">Select the **Performance** tab to display the [performance counters collected by Log Analytics](../log-analytics/log-analytics-data-sources-performance-counters.md) over the time range.</span></span>  <span data-ttu-id="931e5-151">프로세서와 메모리에서 주기적으로 급격한 변화를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-151">We can see that we're getting periodic spikes in the processor and memory.</span></span>

![성능](./media/operations-management-suite-walkthrough-servicemap/performance.png)


### <a name="7-view-change-tracking"></a><span data-ttu-id="931e5-153">7. 변경 내용 추적 보기</span><span class="sxs-lookup"><span data-stu-id="931e5-153">7. View change tracking</span></span>
<span data-ttu-id="931e5-154">이 높은 사용률을 일으킨 원인을 확인해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-154">Let's see if we can find out what might have caused this high utilization.</span></span>  <span data-ttu-id="931e5-155">**요약** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-155">Click on the **Summary** tab.</span></span>  <span data-ttu-id="931e5-156">실패한 연결, 중요한 알림 및 소프트웨어 변경 내용과 같이 OMS가 컴퓨터에서 수집한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-156">This provides information that OMS has collected from the computer such as failed connections, critical alerts, and software changes.</span></span>  <span data-ttu-id="931e5-157">흥미로운 최근 정보를 포함하는 섹션이 확장되어야 하고 포함된 정보를 검사하는 다른 섹션을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-157">Sections with interesting recent information should already be expanded, and you can expand other sections to inspect information that they contain.</span></span>


<span data-ttu-id="931e5-158">**변경 내용 추적**이 열려 있지 않은 경우 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-158">If **Change Tracking** isn't already open, then expand it.</span></span>  <span data-ttu-id="931e5-159">그러면 [변경 내용 추적 솔루션](../log-analytics/log-analytics-change-tracking.md)에서 수집한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-159">This shows information collected by the [Change Tracking solution](../log-analytics/log-analytics-change-tracking.md).</span></span>  <span data-ttu-id="931e5-160">이 기간 동안 소프트웨어가 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-160">It looks like there was a software change made during this time window.</span></span>  <span data-ttu-id="931e5-161">**소프트웨어**를 클릭하여 세부 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-161">Click on **Software** to get details.</span></span>  <span data-ttu-id="931e5-162">오전 4시 직후에 백업 프로세스가 컴퓨터에 추가되었으므로 리소스를 과도하게 사용하는 원인으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-162">A backup process was added to the machine just after 4:00 AM, so this appears to be the culprit for the excessive resources being consumed.</span></span>

![변경 내용 추적](./media/operations-management-suite-walkthrough-servicemap/change-tracking.png)



### <a name="8-view-details-in-log-search"></a><span data-ttu-id="931e5-164">8. 로그 검색에서 세부 정보 보기</span><span class="sxs-lookup"><span data-stu-id="931e5-164">8. View details in Log Search</span></span>
<span data-ttu-id="931e5-165">Log Analytics 리포지토리에서 수집된 자세한 성능 정보를 확인하여 추가로 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-165">We can further verify this by looking at the detailed performance information collected in the Log Analytics repository.</span></span>  <span data-ttu-id="931e5-166">**경고** 탭을 다시 클릭한 다음 **높은 CPU** 경고 중 하나를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-166">Click on the **Alerts** tab again and then on one of the **High CPU** alerts.</span></span>  <span data-ttu-id="931e5-167">**로그 검색에 표시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-167">Click on  **Show in Log Search**.</span></span>  <span data-ttu-id="931e5-168">그러면 리포지토리에서 저장된 데이터에 대해 [검색 로그](../log-analytics/log-analytics-log-searches.md)를 수행할 수 있는 로그 검색 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-168">This opens the Log Search window where you can perform [log searches](../log-analytics/log-analytics-log-searches.md) against any data stored in the repository.</span></span>  <span data-ttu-id="931e5-169">서비스 맵은 관심이 있는 경고를 검색하기 위해 쿼리를 이미 입력했습니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-169">Service Map already filled in a queriy for us to retrieve the alert we're interested in.</span></span>  

![로그 검색](./media/operations-management-suite-walkthrough-servicemap/log-search.png)


### <a name="9-open-saved-search"></a><span data-ttu-id="931e5-171">9. 저장된 검색 열기</span><span class="sxs-lookup"><span data-stu-id="931e5-171">9. Open saved search</span></span>
<span data-ttu-id="931e5-172">이 경고를 생성한 성능 수집에 대한 몇 가지 자세한 내용을 보고 문제가 해당 백업 프로세스에 의해 발생했는지에 대한 의문을 확인할 수 있는지 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-172">Let's see if we can get some more detail on the performance collection that generated this alert and verify our suspicion that the problems are being caused by that backup process.</span></span>  <span data-ttu-id="931e5-173">시간 범위를 **6시간**으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-173">Change the time range to **6 hours**.</span></span>  <span data-ttu-id="931e5-174">**즐겨찾기**를 클릭하고 **서비스 맵**에 대한 저장된 검색까지 아래로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-174">Then click on **Favorites** and scroll down to the saved searches for **Service Map**.</span></span>  <span data-ttu-id="931e5-175">이 분석을 위해 특별히 만들어진 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-175">These are queries that we created specifically for this analysis.</span></span>  <span data-ttu-id="931e5-176">**acmetomcat의 CPU에 따른 상위 5개 프로세스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-176">Click on **Top 5 Processes by CPU for acmetomcat**.</span></span>

![저장된 검색](./media/operations-management-suite-walkthrough-servicemap/saved-search.png)


<span data-ttu-id="931e5-178">이 쿼리는 **acmetomcat**의 프로세스에서 사용하는 상위 5개 프로세스의 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-178">This query returns a list of the top 5 processes consuming processor on **acmetomcat**.</span></span>  <span data-ttu-id="931e5-179">쿼리를 검사하여 로그 검색에 사용되는 쿼리 언어 소개로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-179">You can inspect the query to get an introduction to the query language used for log searches.</span></span>  <span data-ttu-id="931e5-180">다른 컴퓨터에 대한 프로세스에 관심이 있는 경우 해당 정보를 검색하도록 쿼리를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-180">If you were interested in the processes on other computers, you could modify the query to retrieve that information.</span></span>

<span data-ttu-id="931e5-181">이 경우에 백업 프로세스가 앱 서버의 CPU 중 약 60%를 일관되게 사용하고 있는 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-181">In this case, we can see that the backup process is consistently consuming about 60% of the app server’s CPU.</span></span>  <span data-ttu-id="931e5-182">새 프로세스가 성능 문제의 원인임이 분명합니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-182">It's pretty obvious that this new process is responsible for our performance problem.</span></span>  <span data-ttu-id="931e5-183">솔루션은 새 백업 소프트웨어를 응용 프로그램 서버에서 제거하는 것이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-183">Our solution would obviously be to remove this new backup software off the application server.</span></span>  <span data-ttu-id="931e5-184">실제로 Azure Automation에 의해 관리되는 DSC(필요한 상태 구성)를 활용하여 이 프로세스가 이러한 중요한 시스템에서 실행되지 않도록 정책을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-184">We could actually leverage Desired State Configuration (DSC) managed by Azure Automation to define policies that ensure this process never runs on these critical systems.</span></span>


## <a name="summary-points"></a><span data-ttu-id="931e5-185">요약 지점</span><span class="sxs-lookup"><span data-stu-id="931e5-185">Summary points</span></span>
- <span data-ttu-id="931e5-186">[서비스 맵](operations-management-suite-service-map.md)은 해당 서버 및 종속성을 모두 알 수 없더라도 전체 응용 프로그램의 보기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-186">[Service Map](operations-management-suite-service-map.md) provides you with a view of your entire application even if you don't know all of its servers and dependencies.</span></span>
- <span data-ttu-id="931e5-187">서비스 맵이 다른 OMS 솔루션에 의해 수집된 데이터를 표시하여 응용 프로그램 및 기본 인프라에 발생한 문제를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-187">Service Map surfaces data collected by other OMS solutions to help you identify issues with your application and its underlying infrastructure.</span></span>
- <span data-ttu-id="931e5-188">[로그 검색](../log-analytics/log-analytics-log-searches.md)을 사용하면 Log Analytics 리포지토리에 수집된 특정 데이터를 살펴볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-188">[Log searches](../log-analytics/log-analytics-log-searches.md) allow you to drill down into specific data collected in the Log Analytics repository.</span></span>    

## <a name="next-steps"></a><span data-ttu-id="931e5-189">다음 단계</span><span class="sxs-lookup"><span data-stu-id="931e5-189">Next steps</span></span>
- <span data-ttu-id="931e5-190">[서비스 맵](operations-management-suite-service-map.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-190">Learn more about [Service Map](operations-management-suite-service-map.md).</span></span>
- <span data-ttu-id="931e5-191">서비스 맵을 [배포 및 구성](operations-management-suite-service-map-configure.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-191">[Deploy and configure](operations-management-suite-service-map-configure.md) Service Map.</span></span>
- <span data-ttu-id="931e5-192">서비스 맵에 필요하고 에이전트에서 저장하는 작업 데이터를 저장하는 [Log Analytics](../log-analytics/log-analytics-overview.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="931e5-192">Learn about [Log Analytics](../log-analytics/log-analytics-overview.md) which is required for Service Map and stores operational data stored by agents.</span></span>